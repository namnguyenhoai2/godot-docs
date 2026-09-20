.. _doc_filesystem:

Hệ thống tệp
============

Giới thiệu
----------

Hệ thống tệp quản lý cách các asset được lưu trữ và cách chúng được truy cập. Một hệ thống tệp được thiết kế tốt cũng cho phép nhiều developer chỉnh sửa cùng các tệp nguồn và asset trong khi cộng tác. Godot lưu trữ tất cả asset dưới dạng tệp trong hệ thống tệp của mình.

Triển khai
----------

Hệ thống tệp lưu trữ các resource trên ổ đĩa. Mọi thứ, từ một script, một scene cho đến một ảnh PNG, đều là resource đối với engine. Nếu một resource chứa các thuộc tính tham chiếu đến những resource khác trên ổ đĩa, các path đến những resource đó cũng được bao gồm. Nếu một resource có các sub-resource tích hợp sẵn, resource đó sẽ được lưu trong một tệp duy nhất cùng với tất cả sub-resource đi kèm. Ví dụ, một font resource thường được đóng gói cùng với các texture của font.

Hệ thống tệp của Godot tránh sử dụng các tệp metadata. Các asset manager và VCS hiện có tốt hơn bất kỳ thứ gì chúng ta có thể triển khai, vì vậy Godot cố gắng hết sức để phối hợp với Subversion, Git, Mercurial, v.v.

Ví dụ về nội dung hệ thống tệp:

.. code-block:: none

    /project.godot
    /enemy/enemy.tscn
    /enemy/enemy.gd
    /enemy/enemysprite.png
    /player/player.gd

project.godot
-------------

Tệp ``project.godot`` là tệp mô tả project và luôn nằm ở thư mục gốc của project. Trên thực tế, vị trí của nó xác định đâu là thư mục gốc. Đây là tệp đầu tiên Godot tìm kiếm khi mở một project.

Tệp này chứa cấu hình project ở dạng văn bản thuần túy, sử dụng định dạng win.ini. Ngay cả một ``project.godot`` trống cũng có thể hoạt động như định nghĩa cơ bản của một project trống.

Dấu phân cách path
------------------

Godot chỉ hỗ trợ ``/`` làm dấu phân cách path. Điều này được thực hiện vì lý do khả chuyển. Mọi hệ điều hành đều hỗ trợ cách này, kể cả Windows, vì vậy một path như ``C:\project\project.godot`` cần được nhập thành ``C:/project/project.godot``.

Resource path
-------------

Khi truy cập các resource, việc sử dụng bố cục hệ thống tệp của OS máy host có thể rườm rà và không khả chuyển. Để giải quyết vấn đề này, path đặc biệt ``res://`` đã được tạo.

Path ``res://`` sẽ luôn trỏ đến thư mục gốc của project (nơi ``project.godot`` được đặt, vì vậy ``res://project.godot`` luôn hợp lệ).

Hệ thống tệp này chỉ có quyền đọc-ghi khi chạy project cục bộ từ editor. Khi được export hoặc khi chạy trên các thiết bị khác nhau (chẳng hạn như điện thoại hoặc console, hoặc chạy từ DVD), hệ thống tệp sẽ trở thành chỉ đọc và không còn cho phép ghi nữa.

User path
---------

Việc ghi vào ổ đĩa vẫn cần thiết cho các tác vụ như lưu trạng thái game hoặc tải xuống các content pack. Để thực hiện việc này, engine đảm bảo có một path đặc biệt ``user://`` luôn có thể ghi. Path này được resolve khác nhau tùy thuộc vào OS mà project đang chạy. Việc resolve path cục bộ được giải thích thêm trong :ref:`doc_data_paths`.

Hệ thống tệp của máy host
-------------------------

Ngoài ra, cũng có thể sử dụng các path của hệ thống tệp máy host, nhưng cách này không được khuyến nghị cho sản phẩm đã phát hành vì các path này không được đảm bảo hoạt động trên mọi platform. Tuy nhiên, việc sử dụng path của hệ thống tệp máy host có thể hữu ích khi viết các development tool trong Godot.

Nhược điểm
----------

Thiết kế hệ thống tệp này có một số nhược điểm. Vấn đề đầu tiên là việc di chuyển asset (đổi tên hoặc di chuyển chúng từ path này sang path khác bên trong project) sẽ làm hỏng các reference hiện có đến những asset đó. Các reference này sẽ phải được xác định lại để trỏ đến vị trí mới của asset.

Để tránh điều này, hãy thực hiện mọi thao tác di chuyển, xóa và đổi tên từ bên trong Godot, trên dock FileSystem. Khi bạn xóa tệp trong Godot, một hộp thoại xác nhận sẽ xuất hiện, liệt kê tất cả các tệp đã chọn và mọi scene phụ thuộc vào những tệp đó. Không bao giờ di chuyển asset từ bên ngoài Godot, nếu không các dependency sẽ phải được sửa thủ công (Godot phát hiện điều này và vẫn giúp bạn sửa chúng, nhưng tại sao phải chọn cách khó hơn?).

Vấn đề thứ hai là trên Windows và macOS, tên tệp và path không phân biệt chữ hoa chữ thường. Nếu một developer làm việc trên hệ thống tệp máy host không phân biệt chữ hoa chữ thường lưu một asset dưới dạng ``myfile.PNG``, nhưng sau đó tham chiếu đến nó dưới dạng ``myfile.png``, asset sẽ hoạt động bình thường trên platform của họ nhưng không hoạt động trên các platform khác như Linux, Android, v.v. Điều này cũng có thể áp dụng cho các binary đã export, vốn sử dụng một package được nén để lưu trữ tất cả tệp.

Bạn nên để team của mình xác định rõ quy ước đặt tên cho các tệp khi làm việc với Godot. Một quy ước chắc chắn không gây lỗi là chỉ cho phép tên tệp và path viết bằng chữ thường.
