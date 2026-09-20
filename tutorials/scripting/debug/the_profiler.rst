.. _doc_the_profiler:

Profiler
========

Bạn chạy game từ Godot và chơi thử. Game rất thú vị, đã gần hoàn thiện tính năng, và bạn cảm thấy nó sắp được phát hành.

Nhưng rồi bạn mở cây kỹ năng, và game bị chậm hẳn vì một đoạn nào đó trong code gặp vấn đề. Việc xem cây kỹ năng cuộn qua như một trình chiếu slide là không thể chấp nhận được. Đã xảy ra lỗi gì? Vấn đề nằm ở việc định vị các phần tử của cây kỹ năng, UI hay quá trình rendering?

Bạn có thể thử tối ưu mọi thứ rồi chạy game nhiều lần, nhưng bạn có thể làm cách thông minh hơn để thu hẹp các khả năng. Hãy sử dụng profiler của Godot.

Tổng quan về profiler
---------------------

Bạn có thể mở profiler bằng cách mở panel **Debugger** rồi nhấp vào tab **Profiler**.

.. image:: img/profiler.png

Profiler của Godot không tự động chạy vì profiling tiêu tốn nhiều hiệu năng. Nó phải liên tục đo mọi thứ đang diễn ra trong game và gửi báo cáo về debugger, nên mặc định profiler bị tắt.

Để bắt đầu profiling, hãy chạy game rồi chuyển lại editor. Nhấp vào nút **Start** ở góc trên bên trái của tab **Profiler**. Bạn cũng có thể chọn **Autostart**, tùy chọn này sẽ khiến profiler tự động khởi động vào lần tiếp theo khi project được chạy. Lưu ý rằng trạng thái của ô chọn **Autostart** không được giữ lại giữa các phiên editor.

.. note::

    Profiler hiện chưa hỗ trợ các script C#. Bạn có thể profile các script C# bằng JetBrains Rider và JetBrains dotTrace cùng plugin hỗ trợ Godot.

Bạn có thể xóa dữ liệu bất cứ lúc nào bằng cách nhấp vào nút **Clear**. Sử dụng menu thả xuống **Measure** để thay đổi loại dữ liệu được đo. Panel measurements và biểu đồ sẽ cập nhật tương ứng.

Dữ liệu được đo
---------------

Giao diện profiler được chia thành hai phần. Bên trái là danh sách các hàm và bên phải là biểu đồ hiệu năng.

Các phép đo chính là frame time, physics frame, idle time và physics time.

- **Frame time** là thời gian Godot cần để thực thi toàn bộ logic cho một hình ảnh, từ physics đến rendering. - **Physics frame** là khoảng thời gian Godot phân bổ giữa các lần cập nhật physics. Trong trường hợp lý tưởng, frame time là giá trị bạn đã chọn: mặc định là 16,66 mili giây, tương ứng với 60FPS. Đây là mốc tham chiếu bạn có thể dùng cho mọi thứ khác xung quanh nó. - **Idle time** là thời gian Godot cần để cập nhật logic không phải physics, chẳng hạn như code nằm trong `_process` or timers and cameras set to update on **Idle**. - **Physics time** is the time Godot took to update physics tasks, like `_physics_process` và các node dựng sẵn được đặt để cập nhật **Physics**.

.. note:: **Frame Time** includes rendering time. Say you find a mysterious
          một đợt giật lag trong game, nhưng physics và các script của bạn đều chạy nhanh. Độ trễ có thể là do các hạt hoặc hiệu ứng hình ảnh xuất hiện!

Theo mặc định, Godot theo dõi Frame Time và Physics Time. Điều này cung cấp cho bạn tổng quan về thời gian mỗi frame cần so với FPS physics mong muốn đã được phân bổ. Bạn có thể bật và tắt các hàm bằng cách nhấp vào các ô chọn bên trái. Khi đi xuống danh sách, bạn sẽ thấy thêm các nhóm khác như Physics 2D, Physics và Audio, trước khi đến các hàm Script, nơi code của bạn xuất hiện.

Nếu nhấp vào biểu đồ, bạn sẽ thay đổi thông tin của frame được hiển thị ở bên trái. Ở góc trên bên phải còn có bộ đếm frame, cho phép bạn điều chỉnh thủ công frame đang xem một cách chi tiết hơn.

Phạm vi đo và các cửa sổ đo
---------------------------

Bạn có thể thay đổi phép đo đang xem bằng menu thả xuống **Measure**. Theo mặc định, menu bắt đầu với Frame Time và liệt kê thời gian cần để đi qua một frame, tính bằng mili giây. Thời gian trung bình là thời gian trung bình mà một hàm cần khi được gọi nhiều hơn một lần. Ví dụ, một hàm mất 0,05 mili giây khi chạy năm lần sẽ cho thời gian trung bình là 0,01 mili giây.

Nếu số mili giây chính xác không quan trọng và bạn muốn xem tỷ lệ thời gian so với phần còn lại của frame, hãy sử dụng các phép đo phần trăm. Frame % là tỷ lệ so với Frame Time, còn Physics % là tỷ lệ so với Physics Time.

Tùy chọn cuối cùng là phạm vi của thời gian. **Inclusive** đo thời gian mà một hàm sử dụng **cùng với** mọi lệnh gọi hàm lồng bên trong. Ví dụ:

.. image:: img/split_curve.png

`get_neighbors`, `find_nearest_neighbor` và `move_subject` đều mất rất nhiều thời gian. Bạn có thể lầm tưởng rằng nguyên nhân là cả ba hàm đều chậm.

Nhưng khi chuyển sang **Self**, Godot sẽ đo thời gian dành cho phần thân hàm mà không tính các lệnh gọi hàm do chính hàm đó thực hiện.

.. image:: img/self_curve.png

Bạn có thể thấy `get_neighbors` và `move_subject` đã giảm đáng kể mức độ ảnh hưởng. Điều đó có nghĩa là `get_neighbors` và `move_subject` dành nhiều thời gian hơn để chờ một lệnh gọi hàm khác hoàn tất, thay vì thực sự thực thi; còn `find_nearest_neighbor` mới là hàm **thực sự** chậm.

Debug code chậm bằng profiler
-----------------------------

Việc tìm code chậm bằng profiler về cơ bản là chạy game và theo dõi biểu đồ hiệu năng khi biểu đồ được vẽ. Khi xuất hiện một spike không thể chấp nhận trong frame time, bạn có thể nhấp vào biểu đồ để tạm dừng game và đưa _Frame #_ về thời điểm bắt đầu spike. Bạn có thể cần chuyển qua lại giữa các frame và hàm để tìm nguyên nhân gốc rễ.

Trong mục Script functions, hãy bật các ô chọn của một số hàm để tìm ra hàm nào tiêu tốn thời gian. Đây là những hàm bạn cần xem xét và tối ưu.

Đo thủ công bằng micro giây
---------------------------

Nếu hàm của bạn phức tạp, việc xác định phần nào cần tối ưu có thể rất khó. Vấn đề nằm ở phép tính hay cách bạn truy cập các phần dữ liệu khác để thực hiện phép tính? Có phải là vòng lặp `for` không? Hay các câu lệnh `if`?

Bạn có thể thu hẹp phép đo bằng cách đếm thủ công các tick khi code chạy, sử dụng một số hàm tạm thời. Hai hàm này thuộc object lớp `Time`. Đó là `get_ticks_msec` và `get_ticks_usec`. Hàm đầu tiên đo bằng mili giây (1.000 mili giây mỗi giây), còn hàm thứ hai đo bằng micro giây (1.000.000 micro giây mỗi giây).

Cả hai đều trả về khoảng thời gian kể từ khi game engine khởi động, tính theo đơn vị thời gian tương ứng của chúng.

Nếu bạn bọc một đoạn code bằng một lần đếm micro giây ở đầu và cuối, chênh lệch giữa hai giá trị là thời gian cần để chạy đoạn code đó.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Đo thời gian cần để chạy worker_function()
    var start = Time.get_ticks_usec()
    worker_function()
    var end = Time.get_ticks_usec()
    var worker_time = (end-start)/1000000.0

    # Đo thời gian dành cho việc thực hiện một phép tính trên từng phần tử của một mảng
    start = Time.get_ticks_usec()
    for calc in calculations:
        result = pow(2, calc.power) * calc.product
    end = Time.get_ticks_usec()
    var loop_time = (end-start)/1000000.0

    print("Worker time: %s\nLoop time: %s" % [worker_time, loop_time])

Khi trở thành một programmer có nhiều kinh nghiệm hơn, kỹ thuật này sẽ ít cần thiết hơn. Bạn dần học được phần nào của một chương trình đang chạy là chậm. Việc biết rằng các vòng lặp và nhánh điều kiện có thể chậm là điều đến từ kinh nghiệm, và bạn có được kinh nghiệm bằng cách đo lường và nghiên cứu.

Nhưng giữa profiler và các hàm ticks, bạn sẽ có đủ công cụ để bắt đầu tìm ra những phần nào trong code cần được tối ưu.
