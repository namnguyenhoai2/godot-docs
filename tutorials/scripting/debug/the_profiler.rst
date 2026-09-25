.. _doc_the_profiler:

Profiler
========

Bạn chạy game từ Godot và chơi thử. Game rất thú vị, ngày càng hoàn thiện về tính năng, và bạn cảm thấy nó sắp được phát hành.

Nhưng rồi bạn mở cây kỹ năng, và game lập tức chậm hẳn khi có thứ gì đó mắc kẹt trong code. Việc xem cây kỹ năng cuộn qua như một trình chiếu là không thể chấp nhận được. Điều gì đã xảy ra? Vấn đề nằm ở việc định vị các phần tử của cây kỹ năng, UI hay quá trình rendering?

Bạn có thể thử tối ưu mọi thứ rồi chạy game nhiều lần, nhưng bạn có thể xử lý thông minh hơn bằng cách thu hẹp các khả năng. Đây là lúc profiler của Godot phát huy tác dụng.

Tổng quan về profiler
---------------------

Bạn có thể mở profiler bằng cách mở panel **Debugger** rồi nhấp vào tab **Profiler**.

.. image:: img/profiler.png

Profiler của Godot không tự động chạy vì profiling tiêu tốn nhiều hiệu năng. Nó phải liên tục đo lường mọi thứ đang diễn ra trong game và báo cáo lại cho debugger, nên mặc định profiler được tắt.

Để bắt đầu profiling, hãy chạy game rồi chuyển lại editor. Nhấp vào nút **Start** ở góc trên bên trái của tab **Profiler**. Bạn cũng có thể chọn **Autostart**, tùy chọn này sẽ khiến profiler tự động khởi động vào lần tiếp theo khi project được chạy. Lưu ý rằng trạng thái của ô chọn **Autostart** không được giữ lại giữa các phiên editor.

.. note::

    Hiện tại profiler không hỗ trợ script C#. Bạn có thể profile script C# bằng JetBrains Rider và JetBrains dotTrace với plugin hỗ trợ Godot.

Bạn có thể xóa dữ liệu bất cứ lúc nào bằng cách nhấp vào nút **Clear**. Sử dụng menu thả xuống **Measure** để thay đổi loại dữ liệu được đo. Panel đo lường và biểu đồ sẽ cập nhật tương ứng.

Dữ liệu được đo
---------------

Giao diện profiler được chia thành hai phần. Bên trái là danh sách các function, còn bên phải là biểu đồ hiệu năng.

Các phép đo chính là frame time, physics frame, idle time và physics time.

- **frame time** là khoảng thời gian Godot cần để thực thi toàn bộ logic cho một hình ảnh hoàn chỉnh, từ physics đến rendering.
- **Physics frame** là khoảng thời gian Godot phân bổ giữa các lần cập nhật physics. Trong trường hợp lý tưởng, frame time là giá trị bạn chọn: mặc định là 16,66 mili giây, tương ứng với 60FPS. Đây là mốc tham chiếu bạn có thể dùng cho mọi thứ khác.
- **Idle time** là khoảng thời gian Godot cần để cập nhật logic không liên quan đến physics, chẳng hạn như code nằm trong `_process` hoặc các timer và camera được thiết lập cập nhật theo **Idle**.
- **Physics time** là khoảng thời gian Godot cần để cập nhật các tác vụ physics, chẳng hạn như `_physics_process` và các node tích hợp được thiết lập cập nhật theo **Physics**.

.. note:: **Frame Time** bao gồm cả thời gian rendering. Giả sử bạn phát hiện một đợt lag bất thường trong game, nhưng physics và script đều chạy nhanh. Độ trễ có thể là do các particle hoặc hiệu ứng hình ảnh xuất hiện!

Theo mặc định, Godot đánh dấu Frame Time và Physics Time. Điều này cho bạn cái nhìn tổng quan về thời gian mỗi frame cần so với FPS physics mong muốn đã phân bổ. Bạn có thể bật hoặc tắt các function bằng cách nhấp vào các ô chọn ở bên trái. Khi đi xuống danh sách, bạn sẽ thấy thêm các thành phần khác như Physics 2D, Physics và Audio, trước khi đến các function Script, nơi code của bạn xuất hiện.

Nếu nhấp vào biểu đồ, bạn sẽ thay đổi frame có thông tin hiển thị ở bên trái. Ở góc trên bên phải còn có bộ đếm frame, cho phép bạn điều chỉnh thủ công frame đang xem với độ chi tiết cao hơn.

Phạm vi đo lường và các cửa sổ đo lường
---------------------------------------

Bạn có thể thay đổi phép đo đang xem bằng menu thả xuống **Measure**. Theo mặc định, menu bắt đầu với Frame Time và liệt kê thời gian cần để đi qua frame, tính bằng mili giây. Thời gian trung bình là thời gian trung bình mà một function bất kỳ cần khi được gọi nhiều hơn một lần. Ví dụ, một function mất 0,05 mili giây để chạy năm lần sẽ có thời gian trung bình là 0,01 mili giây.

Nếu việc đếm mili giây chính xác không quan trọng và bạn muốn xem tỷ lệ thời gian so với phần còn lại của frame, hãy dùng các phép đo phần trăm. Frame % là tương đối so với Frame Time, còn Physics % là tương đối so với Physics Time.

Tùy chọn cuối cùng là phạm vi thời gian. **Inclusive** đo thời gian một function cần khi chạy **with** cả các lần gọi function lồng bên trong. Ví dụ:

.. image:: img/split_curve.png

`get_neighbors`, `find_nearest_neighbor` và `move_subject` đều mất rất nhiều thời gian. Bạn có thể lầm tưởng rằng nguyên nhân là cả ba function đều chậm.

Nhưng khi chuyển sang **Self**, Godot sẽ đo thời gian dành cho phần thân function mà không tính các lần gọi function do chính function đó thực hiện.

.. image:: img/self_curve.png

Bạn có thể thấy `get_neighbors` và `move_subject` đã mất đi phần lớn mức độ quan trọng. Điều đó có nghĩa là `get_neighbors` và `move_subject` dành nhiều thời gian chờ một lần gọi function khác hoàn tất hơn là tự thực thi, còn `find_nearest_neighbor` thì **thực sự** chậm.

Gỡ lỗi code chậm bằng profiler
------------------------------

Việc tìm code chậm bằng profiler chủ yếu là chạy game và theo dõi biểu đồ hiệu năng khi biểu đồ được vẽ. Khi xuất hiện một đỉnh tăng không thể chấp nhận trong frame time, bạn có thể nhấp vào biểu đồ để tạm dừng game và thu hẹp _Frame #_ về thời điểm bắt đầu của đỉnh đó. Bạn có thể phải chuyển qua lại giữa các frame và function để tìm nguyên nhân gốc.

Trong phần Script functions, hãy bật các ô chọn của một số function để tìm ra function nào tốn thời gian. Đây là những function bạn cần xem xét và tối ưu.

Đo thủ công theo micro giây
---------------------------

Nếu function của bạn phức tạp, việc xác định phần nào cần tối ưu có thể rất khó. Vấn đề nằm ở phép tính hay cách bạn truy cập các phần dữ liệu khác để thực hiện phép tính? Có phải là `for` loop? Hay các câu lệnh `if`?

Bạn có thể thu hẹp phép đo bằng cách đếm thủ công các tick khi code chạy với một số function tạm thời. Hai function này thuộc về đối tượng class `Time`. Chúng là `get_ticks_msec` và `get_ticks_usec`. Function đầu tiên đo bằng mili giây (1.000 mili giây mỗi giây), còn function thứ hai đo bằng micro giây (1.000.000 micro giây mỗi giây).

Mỗi function đều trả về khoảng thời gian kể từ khi game engine khởi động, tính theo đơn vị thời gian tương ứng.

Nếu bạn bao quanh một đoạn code bằng số đếm micro giây ở đầu và cuối, chênh lệch giữa hai số đó chính là khoảng thời gian cần để chạy đoạn code.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Đo thời gian cần để chạy worker_function()
    var start = Time.get_ticks_usec()
    worker_function()
    var end = Time.get_ticks_usec()
    var worker_time = (end-start)/1000000.0

    # Đo thời gian chạy một phép tính trên từng phần tử của một mảng
    start = Time.get_ticks_usec()
    for calc in calculations:
        result = pow(2, calc.power) * calc.product
    end = Time.get_ticks_usec()
    var loop_time = (end-start)/1000000.0

    print("Worker time: %s\nLoop time: %s" % [worker_time, loop_time])

Khi trở thành một lập trình viên giàu kinh nghiệm hơn, bạn sẽ ít cần đến kỹ thuật này hơn. Bạn bắt đầu học cách nhận biết những phần nào của chương trình đang chạy bị chậm. Việc biết rằng các vòng lặp và nhánh có thể chạy chậm là nhờ kinh nghiệm, và bạn có được kinh nghiệm bằng cách đo lường và nghiên cứu.

Tuy nhiên, với profiler và các hàm ticks, bạn sẽ có đủ công cụ để bắt đầu tìm ra những phần nào trong mã của mình cần được tối ưu hóa.
