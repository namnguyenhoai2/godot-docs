.. _doc_debugger_panel:

Bảng Debugger
=============

Nhiều công cụ debugging của Godot, bao gồm debugger, có thể được tìm thấy trong bảng debugger ở cuối màn hình. Nhấp vào **Debugger** để mở.

.. image:: img/overview_debugger.webp

Bảng debugger được chia thành một số tab, mỗi tab tập trung vào một tác vụ cụ thể.

Stack Trace
-----------

Tab Stack Trace tự động mở khi trình biên dịch GDScript gặp breakpoint trong code của bạn.

Tab này cung cấp cho bạn `stack trace <https://en.wikipedia.org/wiki/Stack_trace>`__, thông tin về trạng thái của object và các nút để điều khiển quá trình thực thi của chương trình. Khi debugger dừng tại một breakpoint, một mũi tên tam giác màu xanh lá sẽ hiển thị trong gutter của script editor. Mũi tên này cho biết dòng code mà debugger đã dừng tại đó.

.. tip::

    Bạn có thể tạo breakpoint bằng cách nhấp vào gutter ở bên trái script editor (bên trái số dòng). Khi di chuột lên gutter này, bạn sẽ thấy một chấm đỏ trong suốt xuất hiện; chấm này sẽ chuyển thành chấm đỏ đậm sau khi breakpoint được đặt bằng cách nhấp chuột. Nhấp lại vào chấm đỏ để xóa breakpoint. Các breakpoint được tạo theo cách này vẫn tồn tại qua các lần khởi động lại editor, ngay cả khi script chưa được lưu lúc thoát editor.

    Bạn cũng có thể sử dụng từ khóa ``breakpoint`` trong GDScript để tạo một breakpoint được lưu ngay trong script. Không giống các breakpoint được tạo bằng cách nhấp vào gutter, breakpoint dựa trên từ khóa này vẫn tồn tại trên các máy khác nhau khi sử dụng version control.

Bạn có thể sử dụng các nút ở góc trên bên phải để:

- Bỏ qua tất cả breakpoint. Nhờ đó, bạn có thể lưu breakpoint cho các phiên debugging sau. - Sao chép thông báo lỗi hiện tại. - **Step Into** code. Nút này đưa bạn đến dòng code tiếp theo; nếu đó là một function, nút sẽ thực hiện từng dòng một trong function. - **Step Over** code. Nút này chuyển đến dòng code tiếp theo, nhưng không thực hiện từng dòng một trong các function. - **Break**. Nút này tạm dừng quá trình thực thi game. - **Continue**. Nút này tiếp tục game sau một breakpoint hoặc lần tạm dừng.

.. note::

    Hiện tại, việc sử dụng debugger và breakpoint trên :ref:`tool scripts <doc_running_code_in_the_editor>` chưa được hỗ trợ. Các breakpoint được đặt trong script editor hoặc sử dụng từ khóa ``breakpoint`` sẽ bị bỏ qua. Thay vào đó, bạn có thể sử dụng các câu lệnh print để hiển thị nội dung của các biến.

Errors
------

Đây là nơi các thông báo lỗi và cảnh báo được in ra trong khi game đang chạy.

Bạn có thể tắt các cảnh báo cụ thể trong **Project Settings > Debug > GDScript**.

Evaluator
---------

Tab này chứa một expression evaluator, còn được gọi là :abbr:`REPL (Read-Eval-Print Loop)`. Đây là phần bổ trợ mạnh mẽ hơn cho cây Stack Variables có trong tab Stack Trace.

Khi project bị ngắt trong debugger (do breakpoint hoặc lỗi script), bạn có thể nhập một expression vào trường văn bản ở phía trên. Nếu project đang chạy, trường expression sẽ không thể chỉnh sửa, vì vậy trước tiên bạn cần đặt một breakpoint. Các expression có thể được duy trì qua nhiều lần chạy bằng cách bỏ chọn **Clear on Run**, dù chúng sẽ bị mất khi editor thoát.

Các expression được đánh giá bằng :ref:`Godot's expression language <doc_evaluating_expressions>`, cho phép bạn thực hiện phép tính số học và gọi một số function trong expression. Expression có thể tham chiếu đến các member variable hoặc local variable trong cùng scope với dòng đặt breakpoint. Bạn cũng có thể nhập các giá trị hằng, nhờ đó sử dụng công cụ này như một calculator tích hợp.

Xét script sau:

::

    var counter = 0

    func _process(delta):
        counter += 1
        if counter == 5:
            var text = "Some text"
            breakpoint
        elif counter >= 6:
            var other_text = "Some other text"
            breakpoint

Nếu debugger dừng tại dòng **đầu tiên** chứa ``breakpoint``, các expression sau sẽ trả về giá trị khác null:

- **Constant expression:** ``2 * PI + 5`` - **Member variable:** ``counter``, ``counter ** 2``, ``sqrt(counter)`` - **Local variable hoặc function parameter:** ``delta``, ``text``, ``text.to_upper()``

Nếu debugger dừng tại dòng **thứ hai** chứa ``breakpoint``, các expression sau sẽ trả về giá trị khác null:

- **Constant expression:** ``2 * PI + 5`` - **Member variable:** ``counter``, ``counter ** 2``, ``sqrt(counter)`` - **Local variable hoặc function parameter:** ``delta``, ``other_text``, ``other_text.to_upper()``

Profiler
--------

Profiler được dùng để xem code nào đang chạy trong khi project được sử dụng và điều đó ảnh hưởng đến hiệu năng như thế nào.

.. seealso::

    Bạn có thể tìm thấy phần giải thích chi tiết về cách sử dụng profiler trong trang :ref:`doc_the_profiler` chuyên dụng.

.. _doc_debugger_panel_visual_profiler:

Visual Profiler
---------------

Visual Profiler có thể được sử dụng để theo dõi tác vụ nào chiếm nhiều thời gian nhất khi render một frame, lần lượt trên CPU và GPU. Điều này cho phép theo dõi các nguồn có khả năng gây ra bottleneck CPU và GPU do việc render.

.. warning::

    Visual Profiler chỉ đo thời gian CPU dành cho các tác vụ render, chẳng hạn như thực hiện các draw call. Visual Profiler **không** bao gồm thời gian CPU dành cho các tác vụ khác như scripting và physics. Hãy sử dụng tab Profiler tiêu chuẩn để theo dõi các tác vụ CPU không liên quan đến render.

Để sử dụng visual profiler, hãy chạy project, chuyển sang tab **Visual Profiler** trong bảng Debugger ở phía dưới, sau đó nhấp vào **Start**:

.. figure:: img/debugger_visual_profiler_results.webp
   :alt: Visual Profiler tab after clicking Start, waiting for a few seconds, then clicking Stop

   Visual Profiler tab after clicking **Start**, waiting for a few seconds, then clicking **Stop**

.. tip::

    Bạn cũng có thể chọn **Autostart**; tùy chọn này sẽ khiến visual profiler tự động khởi động khi project được chạy vào lần tiếp theo. Lưu ý rằng trạng thái của checkbox **Autostart** không được lưu lại giữa các phiên editor.

Bạn sẽ thấy các danh mục và kết quả xuất hiện khi profiler đang chạy. Các đường biểu đồ cũng xuất hiện, với phía bên trái là framegraph CPU và phía bên phải là framegraph GPU.

Nhấp vào **Stop** để kết thúc profiling; kết quả sẽ vẫn hiển thị nhưng được cố định tại chỗ. Kết quả vẫn hiển thị sau khi dừng project đang chạy, nhưng không còn sau khi thoát editor.

Nhấp vào các danh mục kết quả ở bên trái để làm nổi bật chúng trong biểu đồ CPU và GPU ở bên phải. Bạn cũng có thể nhấp vào biểu đồ để di chuyển con trỏ đến một số frame cụ thể và làm nổi bật kiểu dữ liệu đã chọn trong các danh mục kết quả ở bên trái.

Bạn có thể chuyển đổi cách hiển thị kết quả giữa giá trị thời gian (tính bằng mili giây trên mỗi frame) hoặc phần trăm frametime mục tiêu. 
:ref:`debugger/profiler_target_fps <class_EditorSettings_property_debugger/profiler_target_fps>`
Thiết lập editor kiểm soát giá trị frametime mục tiêu theo FPS được chỉ định.

Nếu xảy ra các đợt tăng đột biến framerate trong quá trình profiling, biểu đồ có thể được scale không phù hợp. Tắt **Fit to Frame** để biểu đồ phóng to vào phần 60 FPS+.

.. note::

    Hãy nhớ rằng kết quả Visual Profiler có thể thay đổi **rất nhiều** tùy theo độ phân giải viewport, được xác định bởi kích thước cửa sổ nếu sử dụng ``disabled`` hoặc ``canvas_items`` :ref:`stretch modes <doc_multiple_resolutions>`.

    Khi so sánh kết quả giữa các lần chạy khác nhau, hãy đảm bảo sử dụng cùng một kích thước viewport cho tất cả các lần chạy.

Visual Profiler được hỗ trợ khi sử dụng bất kỳ phương thức rendering nào (Forward+, Mobile hoặc Compatibility), nhưng các danh mục được báo cáo sẽ thay đổi tùy theo phương thức rendering hiện tại cũng như các tính năng đồ họa được bật. Ví dụ, khi sử dụng Forward+, một scene 2D đơn giản với các đèn tạo bóng sẽ cho ra các danh mục sau:

.. figure:: img/debugger_visual_profiler_2d_example.webp
   :alt: Example results from a 2D scene in the Visual Profiler

   Example results from a 2D scene in the Visual Profiler

Lấy một ví dụ khác với Forward+: một scene 3D có các đèn tạo bóng và nhiều hiệu ứng được bật sẽ cho ra các danh mục sau:

.. figure:: img/debugger_visual_profiler_3d_example.webp
   :alt: Example results from a 3D scene in the Visual Profiler

   Example results from a 3D scene in the Visual Profiler

Lưu ý rằng trong ví dụ 3D, một số danh mục có **(Parallel)** được thêm vào tên. Điều này cho thấy nhiều tác vụ đang được thực hiện song song trên GPU. Nhìn chung, điều này có nghĩa là việc chỉ tắt một trong các tính năng liên quan sẽ không cải thiện hiệu năng nhiều như dự kiến, vì tác vụ còn lại vẫn cần được thực hiện tuần tự.

.. note::

    Visual Profiler không được hỗ trợ khi sử dụng Compatibility renderer trên macOS do các giới hạn của nền tảng.

Network Profiler
----------------

Network Profiler chứa danh sách tất cả các node giao tiếp thông qua multiplayer API và, với mỗi node, một số bộ đếm về số lượng tương tác mạng đến và đi. Nó cũng có một bandwidth meter hiển thị tổng mức sử dụng băng thông tại bất kỳ thời điểm nào.

.. note::

    Bandwidth meter **không** tính đến hệ thống nén riêng của API :ref:`doc_high_level_multiplayer`. Điều này có nghĩa là việc thay đổi thuật toán nén được sử dụng sẽ không làm thay đổi các chỉ số do bandwidth meter báo cáo.

Monitors
--------

Các monitor là những biểu đồ về một số khía cạnh của game trong khi game đang chạy, chẳng hạn như FPS, mức sử dụng bộ nhớ, số lượng node trong một scene và nhiều thông tin khác. Tất cả monitor đều tự động theo dõi số liệu, vì vậy ngay cả khi một monitor không mở trong lúc game đang chạy, bạn vẫn có thể mở nó sau đó và xem các giá trị đã thay đổi như thế nào.

.. seealso::

    Ngoài các monitor hiệu năng mặc định, bạn cũng có thể tạo
    :ref:`custom performance monitors <doc_custom_performance_monitors>`
    để theo dõi các giá trị tùy ý trong project của mình.

Video RAM
---------

Tab **Video RAM** hiển thị mức sử dụng video RAM của game trong khi game đang chạy. Tab này cung cấp danh sách mọi resource đang sử dụng video RAM theo resource path, loại resource, định dạng của resource và lượng Video RAM mà resource đó đang sử dụng. Ở phía trên bên phải của bảng cũng có một con số thể hiện tổng mức sử dụng video RAM.

.. image:: img/video_ram.png

Misc
----

Tab **Misc** chứa các công cụ để xác định những control node mà bạn đang nhấp vào trong runtime:

- **Clicked Control** cho biết node được nhấp nằm ở đâu trong scene tree. - **Clicked Control Type** cho biết loại của node mà bạn đã nhấp vào.
