.. _doc_filesystem:

Hệ thống tệp
============

Giới thiệu
----------

Hệ thống tệp quản lý cách các tài nguyên được lưu trữ và cách chúng được truy cập. Một hệ thống tệp được thiết kế tốt cũng cho phép nhiều developer chỉnh sửa cùng các tệp nguồn và tài nguyên trong khi cộng tác. Godot lưu trữ tất cả tài nguyên dưới dạng tệp trong hệ thống tệp của mình.

Triển khai
----------

Hệ thống tệp lưu trữ các resource trên ổ đĩa. Mọi thứ, từ script, scene đến ảnh PNG, đều là một resource đối với engine. Nếu một resource chứa các thuộc tính tham chiếu đến những resource khác trên ổ đĩa, các đường dẫn đến những resource đó cũng được bao gồm. Nếu một resource có các sub-resource tích hợp sẵn, resource đó sẽ được lưu trong một tệp duy nhất cùng với tất cả sub-resource đi kèm. Ví dụ: một resource phông chữ thường được đóng gói cùng với các texture phông chữ.

Hệ thống tệp của Godot tránh sử dụng các tệp siêu dữ liệu. Các trình quản lý tài nguyên và VCS hiện có tốt hơn bất kỳ thứ gì chúng ta có thể triển khai, vì vậy Godot cố gắng phối hợp tốt nhất với Subversion, Git, Mercurial, v.v.

Ví dụ về nội dung hệ thống tệp:

.. code-block:: none

    /project.godot
    /enemy/enemy.tscn
    /enemy/enemy.gd
    /enemy/enemysprite.png
    /player/player.gd

project.godot
-------------

Tệp ``project.godot`` là tệp mô tả project và luôn nằm ở thư mục gốc của project. Thực tế, vị trí của tệp này xác định thư mục gốc. Đây là tệp đầu tiên Godot tìm khi mở một project.

Tệp này chứa cấu hình project ở dạng văn bản thuần túy, sử dụng định dạng win.ini. Ngay cả một ``project.godot`` trống cũng có thể hoạt động như định nghĩa cơ bản cho một project trống.

Dấu phân cách đường dẫn
-----------------------

Godot chỉ hỗ trợ ``/`` làm dấu phân cách đường dẫn. Điều này được thực hiện vì lý do tính di động. Tất cả hệ điều hành đều hỗ trợ cách này, kể cả Windows, vì vậy một đường dẫn như ``C:\project\project.godot`` cần được nhập là ``C:/project/project.godot``.

Đường dẫn resource
------------------

Khi truy cập các resource, việc sử dụng bố cục hệ thống tệp của hệ điều hành máy chủ có thể rườm rà và không portable. Để giải quyết vấn đề này, đường dẫn đặc biệt ``res://`` đã được tạo.

Đường dẫn ``res://`` sẽ luôn trỏ đến thư mục gốc của project (nơi ``project.godot`` nằm, vì vậy ``res://project.godot`` luôn hợp lệ).

Hệ thống tệp này chỉ có quyền đọc-ghi khi chạy project cục bộ từ editor. Khi export hoặc khi chạy trên các thiết bị khác (chẳng hạn như điện thoại hay console, hoặc chạy từ DVD), hệ thống tệp sẽ chuyển thành chỉ đọc và không còn cho phép ghi.

Đường dẫn người dùng
--------------------

Việc ghi vào ổ đĩa vẫn cần thiết cho các tác vụ như lưu trạng thái game hoặc tải xuống các content pack. Vì mục đích này, engine đảm bảo có một đường dẫn đặc biệt ``user://`` luôn cho phép ghi. Đường dẫn này được phân giải khác nhau tùy thuộc vào hệ điều hành mà project đang chạy. Việc phân giải đường dẫn cục bộ được giải thích thêm trong :ref:`doc_data_paths`.

Hệ thống tệp máy chủ
--------------------

Ngoài ra, cũng có thể sử dụng các đường dẫn hệ thống tệp máy chủ, nhưng không nên làm vậy cho sản phẩm đã phát hành vì các đường dẫn này không được đảm bảo hoạt động trên mọi nền tảng. Tuy nhiên, việc sử dụng các đường dẫn hệ thống tệp máy chủ có thể hữu ích khi viết các công cụ phát triển trong Godot.

Nhược điểm
----------

Thiết kế hệ thống tệp này có một số nhược điểm. Vấn đề đầu tiên là việc di chuyển tài nguyên (đổi tên hoặc di chuyển chúng từ đường dẫn này sang đường dẫn khác trong project) sẽ làm hỏng các tham chiếu hiện có đến những tài nguyên đó. Các tham chiếu này sẽ phải được định nghĩa lại để trỏ đến vị trí mới của tài nguyên.

Để tránh điều này, hãy thực hiện mọi thao tác di chuyển, xóa và đổi tên từ bên trong Godot, trên dock FileSystem. Khi bạn xóa tệp trong Godot, Godot sẽ hiển thị hộp thoại xác nhận liệt kê tất cả tệp đã chọn và mọi scene phụ thuộc vào các tệp đó. Không bao giờ di chuyển tài nguyên từ bên ngoài Godot, nếu không các dependency sẽ phải được sửa thủ công (Godot phát hiện điều này và vẫn giúp bạn sửa chúng, nhưng tại sao phải chọn cách khó?).

Vấn đề thứ hai là trên Windows và macOS, tên tệp và đường dẫn không phân biệt chữ hoa chữ thường. Nếu một developer làm việc trên hệ thống tệp máy chủ không phân biệt chữ hoa chữ thường lưu một tài nguyên là ``myfile.PNG``, nhưng sau đó tham chiếu đến nó là ``myfile.png``, tài nguyên sẽ hoạt động bình thường trên nền tảng của họ nhưng không hoạt động trên các nền tảng khác như Linux, Android, v.v. Điều này cũng có thể áp dụng cho các binary đã export, vốn sử dụng một gói nén để lưu trữ tất cả tệp.

Bạn nên thống nhất rõ ràng quy ước đặt tên tệp trong nhóm khi làm việc với Godot. Một quy ước chắc chắn không gây lỗi là chỉ cho phép tên tệp và đường dẫn viết bằng chữ thường.
