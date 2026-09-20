.. _doc_cpu_optimization:

Tối ưu hóa CPU
==============

Đo hiệu năng
------------

Chúng ta phải biết các "nút thắt cổ chai" nằm ở đâu để biết cách tăng tốc chương trình. Nút thắt cổ chai là những phần chậm nhất của chương trình, giới hạn tốc độ mà mọi thứ có thể tiến triển. Tập trung vào các nút thắt cổ chai cho phép chúng ta dồn nỗ lực vào việc tối ưu hóa những khu vực mang lại mức cải thiện tốc độ lớn nhất, thay vì dành nhiều thời gian tối ưu hóa các hàm chỉ mang lại mức cải thiện hiệu năng nhỏ.

Đối với CPU, cách dễ nhất để xác định các nút thắt cổ chai là sử dụng profiler.

Profiler CPU
------------

Profiler chạy song song với chương trình và thực hiện các phép đo thời gian để xác định tỷ lệ thời gian được dành cho từng hàm.

Godot IDE có sẵn một profiler tích hợp rất tiện lợi. Profiler này không chạy mỗi khi bạn khởi động project: bạn phải tự khởi động và dừng nó. Lý do là, cũng như hầu hết profiler, việc ghi lại các phép đo thời gian này có thể làm project chậm đi đáng kể.

Sau khi profiling, bạn có thể xem lại kết quả của một frame.

.. figure:: img/godot_profiler.png
   :align: center
   :alt: Screenshot of the Godot profiler

   Results of a profile of one of the demo projects.

.. note:: We can see the cost of built-in processes such as physics and audio,
          cũng như xem chi phí của các hàm scripting do chúng ta viết ở phía dưới.

          Thời gian chờ các server tích hợp khác nhau có thể không được tính trong profiler. Đây là một bug đã biết.

Khi một project chạy chậm, bạn thường sẽ thấy một hàm hoặc process rõ ràng mất nhiều thời gian hơn những phần khác. Đây là nút thắt cổ chai chính của bạn, và thông thường bạn có thể tăng tốc bằng cách tối ưu hóa khu vực này.

Để biết thêm thông tin về cách sử dụng profiler tích hợp của Godot, hãy xem
:ref:`doc_debugger_panel`.

Profiler bên ngoài
------------------

Mặc dù profiler của Godot IDE rất tiện lợi và hữu ích, đôi khi bạn cần nhiều khả năng hơn và khả năng profiling chính mã nguồn của Godot engine.

Bạn có thể :ref:`use a number of third-party C++ profilers <doc_using_cpp_profilers>` để thực hiện việc này.

.. figure:: img/valgrind.png
   :alt: Screenshot of Callgrind

   Example results from Callgrind, which is part of Valgrind.

Từ trái sang phải, Callgrind liệt kê phần trăm thời gian bên trong một hàm và các hàm con của hàm đó (Inclusive), phần trăm thời gian dành cho bản thân hàm, không bao gồm các hàm con (Self), số lần hàm được gọi, tên hàm và file hoặc module.

Trong ví dụ này, chúng ta có thể thấy gần như toàn bộ thời gian được dành cho hàm ``Main::iteration()``. Đây là hàm chính trong mã nguồn Godot, được gọi lặp đi lặp lại. Hàm này khiến các frame được vẽ, các physics tick được mô phỏng, đồng thời các node và script được cập nhật. Một phần lớn thời gian được dành cho các hàm render canvas (66%), vì ví dụ này sử dụng một benchmark 2D. Bên dưới, chúng ta thấy gần 50% thời gian được dành bên ngoài mã Godot trong ``libglapi`` và ``i965_dri`` (graphics driver). Điều này cho chúng ta biết rằng một phần lớn thời gian CPU đang được sử dụng trong graphics driver.

Đây thực sự là một ví dụ tuyệt vời vì trong một thế giới lý tưởng, chỉ một phần thời gian rất nhỏ được dành cho graphics driver. Đây là dấu hiệu cho thấy có quá nhiều giao tiếp và công việc được thực hiện trong graphics API. Kết quả profiling cụ thể này đã dẫn đến sự phát triển của 2D batching, giúp tăng tốc đáng kể việc render 2D bằng cách giảm các nút thắt cổ chai trong khu vực này.

Đo thời gian hàm thủ công
-------------------------

Một kỹ thuật hữu ích khác, đặc biệt sau khi bạn đã xác định được nút thắt cổ chai bằng profiler, là tự đo thời gian của hàm hoặc khu vực đang được kiểm tra. Chi tiết cụ thể sẽ khác nhau tùy thuộc vào ngôn ngữ, nhưng trong GDScript, bạn sẽ thực hiện như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var time_start = Time.get_ticks_usec()

    # Hàm bạn muốn đo thời gian
    update_enemies()

    var time_end = Time.get_ticks_usec()
    print("update_enemies() took %d microseconds" % (time_end - time_start))

 .. code-tab:: csharp

    var timeStart = Time.GetTicksUsec();

    // Hàm bạn muốn đo thời gian.
    UpdateEnemies();

    var timeEnd = Time.GetTicksUsec();
    GD.Print($"UpdateEnemies() took {timeEnd - timeStart} microseconds");

Khi tự đo thời gian các hàm, thông thường bạn nên chạy hàm nhiều lần (1.000 lần trở lên), thay vì chỉ chạy một lần (trừ khi đó là một hàm rất chậm). Lý do là các bộ hẹn giờ thường có độ chính xác hạn chế. Ngoài ra, CPU sẽ lập lịch cho các process theo cách không cố định. Vì vậy, giá trị trung bình qua một loạt lần chạy sẽ chính xác hơn một phép đo duy nhất.

Khi cố gắng tối ưu hóa các hàm, hãy đảm bảo bạn liên tục profile hoặc đo thời gian của chúng trong quá trình thực hiện. Điều này sẽ cung cấp phản hồi quan trọng về việc tối ưu hóa có hiệu quả hay không.

Cache
-----

CPU cache là một yếu tố khác cần đặc biệt lưu ý, nhất là khi so sánh kết quả đo thời gian của hai phiên bản khác nhau của một hàm. Kết quả có thể phụ thuộc rất nhiều vào việc dữ liệu có nằm trong CPU cache hay không. CPU không tải dữ liệu trực tiếp từ system RAM, dù system RAM lớn hơn rất nhiều so với CPU cache (vài gigabyte thay vì vài megabyte). Đó là vì system RAM truy cập rất chậm. Thay vào đó, CPU tải dữ liệu từ một vùng bộ nhớ nhỏ hơn và nhanh hơn gọi là cache. Việc tải dữ liệu từ cache rất nhanh, nhưng mỗi khi bạn cố tải một địa chỉ bộ nhớ không được lưu trong cache, cache phải truy cập bộ nhớ chính và từ từ tải một lượng dữ liệu vào. Độ trễ này có thể khiến CPU ở trạng thái nhàn rỗi trong thời gian dài và được gọi là "cache miss".

Điều này có nghĩa là lần đầu tiên bạn chạy một hàm, hàm có thể chạy chậm vì dữ liệu chưa nằm trong CPU cache. Từ lần thứ hai trở đi, hàm có thể chạy nhanh hơn nhiều vì dữ liệu đã nằm trong cache. Vì vậy, hãy luôn sử dụng giá trị trung bình khi đo thời gian và lưu ý đến ảnh hưởng của cache.

Hiểu về caching cũng rất quan trọng đối với việc tối ưu hóa CPU. Nếu bạn có một algorithm (routine) tải các phần dữ liệu nhỏ từ những khu vực phân tán ngẫu nhiên trong bộ nhớ chính, điều này có thể dẫn đến nhiều cache miss; phần lớn thời gian, CPU sẽ phải chờ dữ liệu thay vì thực hiện công việc. Ngược lại, nếu bạn có thể thực hiện các lần truy cập dữ liệu cục bộ hơn, hoặc tốt hơn nữa là truy cập bộ nhớ theo cách tuyến tính (giống như một danh sách liên tục), thì cache sẽ hoạt động tối ưu và CPU có thể làm việc nhanh nhất có thể.

Godot thường xử lý các chi tiết cấp thấp như vậy cho bạn. Ví dụ, các Server API đảm bảo dữ liệu đã được tối ưu hóa cho caching đối với những việc như rendering và physics. Tuy nhiên, bạn vẫn nên đặc biệt chú ý đến caching khi viết GDExtensions.

Ngôn ngữ
--------

Godot hỗ trợ nhiều ngôn ngữ khác nhau và bạn nên ghi nhớ rằng mỗi ngôn ngữ đều có những đánh đổi. Một số ngôn ngữ được thiết kế để dễ sử dụng nhưng phải đánh đổi bằng tốc độ, trong khi những ngôn ngữ khác nhanh hơn nhưng khó làm việc hơn.

Các hàm engine tích hợp chạy với cùng tốc độ bất kể bạn chọn ngôn ngữ scripting nào. Nếu project của bạn thực hiện nhiều phép tính trong mã riêng, hãy cân nhắc chuyển các phép tính đó sang một ngôn ngữ nhanh hơn.

GDScript
~~~~~~~~

:ref:`GDScript <doc_gdscript>` is designed to be easy to use and iterate,
và rất phù hợp để tạo nhiều loại game. Tuy nhiên, trong ngôn ngữ này, tính dễ sử dụng được xem là quan trọng hơn hiệu năng. Nếu bạn cần thực hiện các phép tính nặng, hãy cân nhắc chuyển một phần project sang một trong những ngôn ngữ khác.

C# ~~

:ref:`C# <doc_c_sharp>` is popular and has first-class support in Godot. It
mang lại sự cân bằng tốt giữa tốc độ và tính dễ sử dụng. Tuy nhiên, hãy cẩn thận với các khoảng dừng và rò rỉ garbage collection có thể xảy ra trong khi chơi game. Một cách tiếp cận phổ biến để khắc phục các vấn đề với garbage collection là sử dụng *object pooling*, nội dung này nằm ngoài phạm vi của hướng dẫn.

Các ngôn ngữ khác
~~~~~~~~~~~~~~~~~

Bên thứ ba cung cấp hỗ trợ cho một số ngôn ngữ khác, bao gồm `Rust <https://github.com/godot-rust/gdext>`_.

C++
~~~

Godot được viết bằng C++. Sử dụng C++ thường sẽ cho ra mã nhanh nhất. Tuy nhiên, trên thực tế, đây là ngôn ngữ khó triển khai nhất đến máy của người dùng cuối trên các platform khác nhau. Các lựa chọn để sử dụng C++ bao gồm GDExtensions và
:ref:`custom modules <doc_custom_modules_in_cpp>`.

Thread
------

Hãy cân nhắc sử dụng thread khi thực hiện nhiều phép tính có thể chạy song song với nhau. CPU hiện đại có nhiều core, mỗi core có khả năng thực hiện một lượng công việc giới hạn. Bằng cách phân chia công việc qua nhiều thread, bạn có thể tiến gần hơn đến hiệu suất CPU tối đa.

Nhược điểm của thread là bạn phải cực kỳ cẩn thận. Vì mỗi CPU core hoạt động độc lập, chúng có thể cùng cố gắng truy cập một vùng bộ nhớ tại cùng một thời điểm. Một thread có thể đang đọc một variable trong khi thread khác đang ghi vào đó: đây được gọi là *race condition*. Trước khi sử dụng thread, hãy đảm bảo bạn hiểu các mối nguy hiểm và cách cố gắng ngăn chặn những race condition này. Thread có thể khiến việc debugging trở nên khó khăn hơn đáng kể.

Để biết thêm thông tin về thread, hãy xem :ref:`doc_using_multiple_threads`.

SceneTree
---------

Mặc dù Node là một khái niệm vô cùng mạnh mẽ và linh hoạt, hãy lưu ý rằng mỗi node đều có chi phí. Các hàm tích hợp như ``_process()`` và ``_physics_process()`` lan truyền qua tree. Công việc housekeeping này có thể làm giảm hiệu năng khi bạn có số lượng node rất lớn (con số chính xác phụ thuộc vào platform đích và có thể dao động từ hàng nghìn đến hàng chục nghìn, vì vậy hãy đảm bảo bạn profile hiệu năng trên tất cả platform đích trong quá trình phát triển).

Mỗi node được Godot renderer xử lý riêng lẻ. Do đó, số lượng node ít hơn nhưng mỗi node chứa nhiều thành phần hơn có thể mang lại hiệu năng tốt hơn.

Một điểm đáng chú ý của :ref:`SceneTree <class_SceneTree>` là đôi khi bạn có thể đạt hiệu năng tốt hơn nhiều bằng cách xóa node khỏi SceneTree, thay vì tạm dừng hoặc ẩn chúng. Bạn không cần phải xóa một node đã tách khỏi tree. Ví dụ, bạn có thể giữ một reference đến node, tách node đó khỏi scene tree bằng
:ref:`Node.remove_child(node) <class_Node_method_remove_child>`, then reattach
sau đó sử dụng :ref:`Node.add_child(node) <class_Node_method_add_child>` để thêm lại. Điều này có thể rất hữu ích khi thêm và xóa các khu vực khỏi game, chẳng hạn.

Bạn có thể hoàn toàn tránh sử dụng SceneTree bằng cách sử dụng Server API. Để biết thêm thông tin, hãy xem :ref:`doc_using_servers`.

Physics
-------

Trong một số tình huống, physics có thể trở thành điểm nghẽn. Điều này đặc biệt đúng với các world phức tạp và số lượng lớn physics object.

Dưới đây là một số kỹ thuật để tăng tốc physics:

- Hãy thử sử dụng các phiên bản đơn giản hóa của geometry đã render cho collision shape. Thông thường, người dùng cuối sẽ không nhận thấy điều này, nhưng hiệu năng có thể được cải thiện đáng kể. - Hãy thử loại bỏ các object khỏi physics khi chúng nằm ngoài tầm nhìn / bên ngoài khu vực hiện tại, hoặc tái sử dụng các physics object (ví dụ: bạn cho phép 8 quái vật trong mỗi khu vực và tái sử dụng chúng).

Một khía cạnh quan trọng khác của physics là physics tick rate. Trong một số game, bạn có thể giảm đáng kể tick rate, và thay vì cập nhật physics 60 lần mỗi giây, chẳng hạn, bạn có thể chỉ cập nhật 30 hoặc thậm chí 20 lần mỗi giây. Điều này có thể giảm đáng kể tải CPU.

Nhược điểm của việc thay đổi physics tick rate là chuyển động có thể bị giật hoặc jitter khi tốc độ cập nhật physics không khớp với số khung hình mỗi giây được render. Ngoài ra, việc giảm physics tick rate sẽ làm tăng input lag. Trong hầu hết các game có chuyển động người chơi theo thời gian thực, bạn nên giữ physics tick rate mặc định (60 Hz).

Giải pháp cho hiện tượng jitter là sử dụng *nội suy fixed timestep*, trong đó các vị trí và góc xoay được render sẽ được làm mượt qua nhiều frame để khớp với physics. Godot có tính năng physics interpolation tích hợp sẵn mà bạn có thể đọc thêm về
:ref:`here<doc_physics_interpolation>`.
Về hiệu năng, interpolation là một thao tác rất nhẹ so với việc chạy một physics tick. Nó nhanh hơn nhiều bậc độ lớn, vì vậy có thể mang lại lợi ích hiệu năng đáng kể đồng thời giảm jitter.
