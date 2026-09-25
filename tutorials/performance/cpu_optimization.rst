.. _doc_cpu_optimization:

Tối ưu hóa CPU
==============

Đo hiệu năng
------------

Chúng ta cần biết các "nút thắt cổ chai" nằm ở đâu để biết cách tăng tốc chương trình. Nút thắt cổ chai là những phần chậm nhất của chương trình, giới hạn tốc độ tiến triển của mọi thứ. Tập trung vào các nút thắt cổ chai giúp chúng ta dồn nỗ lực vào việc tối ưu hóa những khu vực mang lại mức cải thiện tốc độ lớn nhất, thay vì dành nhiều thời gian tối ưu hóa các hàm chỉ đem lại cải thiện hiệu năng nhỏ.

Đối với CPU, cách dễ nhất để xác định các nút thắt cổ chai là sử dụng profiler.

CPU profiler
------------

Profiler chạy song song với chương trình và thực hiện các phép đo thời gian để xác định tỷ lệ thời gian được dành cho từng hàm.

Godot IDE có sẵn profiler tích hợp rất tiện lợi. Profiler không chạy mỗi khi bạn khởi động project: bạn phải tự khởi động và dừng nó. Lý do là, giống như hầu hết profiler, việc ghi lại các phép đo thời gian này có thể làm project chậm đi đáng kể.

Sau khi profiling, bạn có thể xem lại kết quả của một frame.

.. figure:: img/godot_profiler.png
   :align: center
   :alt: Ảnh chụp màn hình profiler của Godot

   Kết quả profile của một trong các project demo.

.. note:: Chúng ta có thể thấy chi phí của các process tích hợp như physics và audio, đồng thời thấy chi phí của các hàm scripting do chúng ta viết ở bên dưới.

          Thời gian chờ các server tích hợp khác nhau có thể không được tính trong profiler. Đây là một lỗi đã được biết đến.

Khi project chạy chậm, bạn thường sẽ thấy một hàm hoặc process rõ ràng nào đó tốn nhiều thời gian hơn những phần khác. Đây là nút thắt cổ chai chính, và bạn thường có thể tăng tốc bằng cách tối ưu hóa khu vực này.

Để biết thêm thông tin về cách sử dụng profiler tích hợp của Godot, hãy xem
:ref:`doc_debugger_panel`.

Profiler bên ngoài
------------------

Mặc dù profiler của Godot IDE rất tiện lợi và hữu ích, đôi khi bạn cần nhiều khả năng hơn, cùng với khả năng profile chính mã nguồn của Godot engine.

Bạn có thể :ref:`sử dụng một số profiler C++ của bên thứ ba <doc_using_cpp_profilers>` để thực hiện việc này.

.. figure:: img/valgrind.png
   :alt: Ảnh chụp màn hình Callgrind

   Ví dụ về kết quả từ Callgrind, một phần của Valgrind.

Từ trái sang phải, Callgrind liệt kê phần trăm thời gian bên trong một hàm và các hàm con của hàm đó (Inclusive), phần trăm thời gian dành cho chính hàm đó, không bao gồm các hàm con (Self), số lần hàm được gọi, tên hàm và file hoặc module.

Trong ví dụ này, chúng ta có thể thấy gần như toàn bộ thời gian được dành cho hàm ``Main::iteration()``. Đây là hàm chính trong mã nguồn Godot, được gọi lặp đi lặp lại. Hàm này khiến các frame được vẽ, các tick physics được mô phỏng, đồng thời các node và script được cập nhật. Một phần lớn thời gian được dành cho các hàm render canvas (66%), vì ví dụ này sử dụng benchmark 2D. Bên dưới, chúng ta thấy gần 50% thời gian được dành bên ngoài mã Godot cho ``libglapi`` và ``i965_dri`` (graphics driver). Điều này cho chúng ta biết rằng một phần lớn thời gian CPU đang được dành cho graphics driver.

Đây thực sự là một ví dụ tuyệt vời vì trong một thế giới lý tưởng, chỉ một phần rất nhỏ thời gian được dành cho graphics driver. Đây là dấu hiệu cho thấy có vấn đề do quá nhiều hoạt động giao tiếp và xử lý được thực hiện trong graphics API. Hoạt động profiling cụ thể này đã dẫn đến việc phát triển 2D batching, giúp tăng tốc đáng kể quá trình render 2D bằng cách giảm các nút thắt cổ chai trong khu vực này.

Đo thời gian hàm thủ công
-------------------------

Một kỹ thuật hữu ích khác, đặc biệt sau khi bạn đã xác định được nút thắt cổ chai bằng profiler, là tự đo thời gian của hàm hoặc khu vực đang được kiểm tra. Chi tiết cụ thể phụ thuộc vào ngôn ngữ, nhưng trong GDScript, bạn sẽ thực hiện như sau:

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

Khi tự đo thời gian hàm, thông thường bạn nên chạy hàm nhiều lần (1.000 lần trở lên), thay vì chỉ chạy một lần (trừ khi đó là một hàm rất chậm). Lý do là các bộ hẹn giờ thường có độ chính xác hạn chế. Hơn nữa, CPU sẽ lên lịch cho các process theo cách không cố định. Vì vậy, giá trị trung bình qua một loạt lần chạy chính xác hơn một phép đo đơn lẻ.

Khi cố gắng tối ưu hóa các hàm, hãy đảm bảo bạn liên tục profile hoặc đo thời gian của chúng trong quá trình thực hiện. Việc này sẽ cung cấp phản hồi quan trọng cho biết quá trình tối ưu hóa có hiệu quả hay không.

Cache
-----

CPU cache là một yếu tố khác cần đặc biệt lưu ý, nhất là khi so sánh kết quả đo thời gian của hai phiên bản khác nhau của một hàm. Kết quả có thể phụ thuộc rất nhiều vào việc dữ liệu có nằm trong CPU cache hay không. CPU không tải dữ liệu trực tiếp từ system RAM, mặc dù system RAM lớn hơn rất nhiều so với CPU cache (vài gigabyte thay vì vài megabyte). Đó là vì system RAM truy cập rất chậm. Thay vào đó, CPU tải dữ liệu từ một vùng bộ nhớ nhỏ hơn và nhanh hơn gọi là cache. Việc tải dữ liệu từ cache rất nhanh, nhưng mỗi khi bạn cố tải một địa chỉ bộ nhớ không được lưu trong cache, cache phải truy cập bộ nhớ chính và tải dữ liệu vào một cách chậm chạp. Độ trễ này có thể khiến CPU nhàn rỗi trong thời gian dài, và được gọi là "cache miss".

Điều này có nghĩa là lần đầu tiên bạn chạy một hàm, hàm có thể chạy chậm vì dữ liệu chưa nằm trong CPU cache. Từ lần thứ hai trở đi, hàm có thể chạy nhanh hơn nhiều vì dữ liệu đã nằm trong cache. Vì vậy, hãy luôn sử dụng giá trị trung bình khi đo thời gian và lưu ý đến ảnh hưởng của cache.

Hiểu về caching cũng rất quan trọng đối với việc tối ưu hóa CPU. Nếu bạn có một thuật toán (routine) tải các mẩu dữ liệu nhỏ từ những khu vực phân tán ngẫu nhiên trong bộ nhớ chính, điều này có thể gây ra rất nhiều cache miss; phần lớn thời gian CPU sẽ phải chờ dữ liệu thay vì thực hiện công việc. Ngược lại, nếu bạn có thể thực hiện việc truy cập dữ liệu cục bộ hơn, hoặc tốt hơn nữa là truy cập bộ nhớ theo cách tuyến tính (như một danh sách liên tục), cache sẽ hoạt động tối ưu và CPU có thể làm việc nhanh nhất có thể.

Godot thường xử lý các chi tiết cấp thấp như vậy cho bạn. Ví dụ, các Server API đảm bảo dữ liệu đã được tối ưu cho caching đối với những tác vụ như rendering và physics. Tuy nhiên, bạn vẫn nên đặc biệt lưu ý đến caching khi viết GDExtensions.

Ngôn ngữ
--------

Godot hỗ trợ nhiều ngôn ngữ khác nhau, và bạn nên ghi nhớ rằng chúng có những sự đánh đổi nhất định. Một số ngôn ngữ được thiết kế để dễ sử dụng với cái giá là tốc độ, trong khi những ngôn ngữ khác nhanh hơn nhưng khó làm việc hơn.

Các hàm engine tích hợp chạy ở cùng một tốc độ bất kể bạn chọn ngôn ngữ scripting nào. Nếu project của bạn thực hiện nhiều phép tính trong code riêng, hãy cân nhắc chuyển các phép tính đó sang một ngôn ngữ nhanh hơn.

GDScript
~~~~~~~~

:ref:`GDScript <doc_gdscript>` được thiết kế để dễ sử dụng và lặp lại, đồng thời rất phù hợp để tạo nhiều loại game. Tuy nhiên, trong ngôn ngữ này, tính dễ sử dụng được xem là quan trọng hơn hiệu năng. Nếu cần thực hiện các phép tính nặng, hãy cân nhắc chuyển một phần project sang một trong các ngôn ngữ khác.

C#
~~

:ref:`C# <doc_c_sharp>` rất phổ biến và được Godot hỗ trợ đầy đủ. Ngôn ngữ này mang lại sự cân bằng tốt giữa tốc độ và tính dễ sử dụng. Tuy nhiên, hãy lưu ý về các lần tạm dừng và rò rỉ bộ nhớ có thể xảy ra trong quá trình chơi. Một cách phổ biến để khắc phục các vấn đề với garbage collection là sử dụng *object pooling*, nội dung này nằm ngoài phạm vi của hướng dẫn.

Các ngôn ngữ khác
~~~~~~~~~~~~~~~~~

Bên thứ ba cung cấp hỗ trợ cho một số ngôn ngữ khác, bao gồm `Rust <https://github.com/godot-rust/gdext>`_.

C++
~~~

Godot được viết bằng C++. Việc sử dụng C++ thường sẽ cho ra code nhanh nhất. Tuy nhiên, trên phương diện thực tế, đây là ngôn ngữ khó triển khai nhất lên máy của người dùng cuối trên các nền tảng khác nhau. Các tùy chọn để sử dụng C++ bao gồm GDExtensions và
:ref:`custom modules <doc_custom_modules_in_cpp>`.

Threads
-------

Hãy cân nhắc sử dụng threads khi thực hiện nhiều phép tính có thể chạy song song với nhau. Các CPU hiện đại có nhiều lõi, mỗi lõi có khả năng thực hiện một lượng công việc giới hạn. Bằng cách phân chia công việc cho nhiều threads, bạn có thể tiến gần hơn đến hiệu suất CPU tối đa.

Nhược điểm của threads là bạn phải cực kỳ cẩn thận. Vì mỗi lõi CPU hoạt động độc lập, chúng có thể cố truy cập cùng một vùng nhớ tại cùng một thời điểm. Một thread có thể đang đọc một biến trong khi thread khác đang ghi vào biến đó: đây được gọi là *race condition*. Trước khi sử dụng threads, hãy đảm bảo bạn hiểu rõ các nguy hiểm và cách ngăn chặn những race condition này. Threads có thể khiến việc debug khó khăn hơn đáng kể.

Để biết thêm thông tin về threads, hãy xem :ref:`doc_using_multiple_threads`.

SceneTree
---------

Mặc dù Nodes là một khái niệm cực kỳ mạnh mẽ và linh hoạt, hãy lưu ý rằng mỗi node đều có chi phí. Các hàm tích hợp như ``_process()`` và ``_physics_process()`` được lan truyền trong cây. Công việc quản lý này có thể làm giảm hiệu suất khi bạn có số lượng node rất lớn (con số chính xác phụ thuộc vào nền tảng đích và có thể dao động từ hàng nghìn đến hàng chục nghìn, vì vậy hãy đảm bảo bạn lập profile hiệu suất trên tất cả nền tảng đích trong quá trình phát triển).

Mỗi node được Godot renderer xử lý riêng lẻ. Vì vậy, số lượng node ít hơn nhưng mỗi node chứa nhiều thành phần hơn có thể mang lại hiệu suất tốt hơn.

Một điểm đặc biệt của :ref:`SceneTree <class_SceneTree>` là đôi khi bạn có thể đạt hiệu suất tốt hơn nhiều bằng cách xóa các node khỏi SceneTree, thay vì tạm dừng hoặc ẩn chúng. Bạn không cần xóa một node đã tách khỏi cây. Chẳng hạn, bạn có thể giữ một tham chiếu đến node, tách node đó khỏi scene tree bằng
:ref:`Node.remove_child(node) <class_Node_method_remove_child>`, sau đó gắn lại node bằng :ref:`Node.add_child(node) <class_Node_method_add_child>`. Điều này có thể rất hữu ích, chẳng hạn khi thêm và xóa các khu vực khỏi game.

Bạn có thể hoàn toàn không sử dụng SceneTree bằng cách dùng Server APIs. Để biết thêm thông tin, hãy xem :ref:`doc_using_servers`.

Physics
-------

Trong một số trường hợp, physics có thể trở thành một nút thắt cổ chai. Điều này đặc biệt xảy ra với các thế giới phức tạp và số lượng lớn physics object.

Dưới đây là một số kỹ thuật để tăng tốc physics:

- Hãy thử sử dụng các phiên bản đơn giản hóa của geometry được render để làm collision shape. Thông thường, người dùng cuối sẽ không nhận thấy điều này, nhưng hiệu suất có thể tăng đáng kể.
- Hãy thử xóa các object khỏi physics khi chúng nằm ngoài tầm nhìn hoặc bên ngoài khu vực hiện tại, hoặc tái sử dụng các physics object (chẳng hạn, bạn cho phép 8 quái vật trong mỗi khu vực và tái sử dụng các object này).

Một khía cạnh quan trọng khác của physics là tick rate. Trong một số game, bạn có thể giảm đáng kể tick rate; thay vì cập nhật physics 60 lần mỗi giây, bạn có thể chỉ cập nhật 30 hoặc thậm chí 20 lần mỗi giây. Điều này có thể giảm đáng kể tải CPU.

Nhược điểm của việc thay đổi tick rate của physics là chuyển động có thể bị giật hoặc jitter khi tốc độ cập nhật physics không khớp với số frame được render mỗi giây. Ngoài ra, việc giảm tick rate của physics sẽ làm tăng input lag. Trong hầu hết các game có chuyển động của người chơi theo thời gian thực, bạn nên giữ tick rate mặc định của physics (60 Hz).

Giải pháp cho jitter là sử dụng *fixed timestep interpolation*, trong đó các vị trí và góc xoay được render sẽ được làm mượt qua nhiều frame để khớp với physics. Godot có interpolation cho physics tích hợp sẵn, bạn có thể đọc thêm
:ref:`tại đây <doc_physics_interpolation>`. Về mặt hiệu suất, interpolation là một thao tác rất nhẹ so với việc chạy một physics tick. Nó nhanh hơn nhiều bậc độ lớn, vì vậy đây có thể là một cải thiện hiệu suất đáng kể đồng thời giảm jitter.

.. _`Rust`: https://github.com/godot-rust/gdext
