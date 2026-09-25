.. _doc_how_to_read_the_godot_api:

Cách đọc API Godot
==================

Trên trang này, bạn sẽ học cách đọc tài liệu tham chiếu lớp cho API Godot.

API, hay Giao diện Lập trình Ứng dụng (Application Programming Interface), là chỉ mục về những gì Godot cung cấp cho người dùng. API cung cấp bản tóm tắt ngắn gọn về các lớp hiện có, mối quan hệ giữa chúng, những tính năng chúng có và cách sử dụng chúng.

Kế thừa
-------

.. image:: img/class_api_inheritance.webp

Ở đầu mỗi tệp, bạn sẽ thấy tên của lớp.

Phần "Inherits" liệt kê từng lớp mà lớp hiện tại kế thừa. Ở đây ``CanvasItem`` kế thừa ``Node`` và ``Node`` kế thừa ``Object``.

Phần "Inherited By" liệt kê từng lớp trực tiếp kế thừa lớp hiện tại. Ở đây cả ``Control`` và ``Node2D`` đều kế thừa ``CanvasItem``.

Mô tả ngắn
----------

.. image:: img/class_api_brief_description.webp

Tiếp theo là phần mô tả ngắn về lớp. Văn bản này xuất hiện trong các cửa sổ bật lên của Godot Editor để tạo Nodes, Resources và các loại khác.

Mô tả
-----

.. image:: img/class_api_description.webp

Tiếp theo là phần mô tả chi tiết hơn về lớp, các tính năng và trường hợp sử dụng của lớp.

Những nội dung bạn có thể tìm thấy ở đây:

1. Chi tiết cụ thể về cách lớp hoạt động.

2. Các mẫu mã cho những trường hợp sử dụng phổ biến.

3. Các chi tiết sử dụng được dùng chung giữa từng phương thức của lớp.

4. Các cảnh báo về những dependency hoặc cấu hình bắt buộc.

5. Các liên kết đến những phần liên quan khác của API Godot.

Hướng dẫn
---------

.. image:: img/class_api_tutorials.webp

Sau đó, trang cung cấp các liên kết đến những phần của tài liệu có đề cập hoặc sử dụng lớp hiện tại.

Properties
----------

.. image:: img/class_api_properties_table.webp

Bảng Properties liệt kê các biến thuộc về mỗi instance của lớp, còn được gọi là "properties".

Cột bên trái chứa kiểu dữ liệu của property. Văn bản này cũng là liên kết đến trang API Godot của kiểu dữ liệu đó.

Cột ở giữa chứa tên của property. Văn bản này cũng là liên kết đến phần mô tả đầy đủ của property trên trang. Dùng tên này để lấy dữ liệu của property hoặc đặt giá trị mới cho nó.

Cột bên phải chứa giá trị mặc định của property. Để khởi tạo property bằng một giá trị khác, bạn phải đặt giá trị khác thông qua script hoặc Inspector.

Methods
-------

.. image:: img/class_api_methods_table.webp

Bảng Methods liệt kê các hàm thuộc về mỗi instance của lớp, còn được gọi là "methods".

Cột bên trái chứa kiểu dữ liệu của giá trị trả về của method.

Cột bên phải chứa tên, các tham số và các qualifier của method. Tên là phần văn bản trước dấu ngoặc đơn mở. Tên này cũng là liên kết đến phần mô tả đầy đủ của method trên trang. Dùng tên này để gọi method.

Đối với mỗi tham số, trang nêu chi tiết kiểu dữ liệu, tên và giá trị mặc định của tham số, nếu có.

Các qualifier có thể bao gồm...

- ``const``: method không thay đổi bất kỳ dữ liệu nào trong instance của lớp.
- ``virtual``: method không làm gì ngoài việc chờ một script override nó.
- ``vararg``: method có thể nhận một số lượng đối số tùy ý.

Signals
-------

.. image:: img/class_api_signals.webp

Danh sách Signals nêu chi tiết tên và các tham số của những sự kiện "signal" một thay đổi trong trạng thái trò chơi đến các instance lớp khác.

Giống như bảng Methods, mọi tham số đều bao gồm kiểu dữ liệu và tên.

Mỗi signal cũng có phần giải thích chi tiết về thời điểm signal được phát ra.

Enumerations
------------

.. image:: img/class_api_enumerations.webp

Danh sách Enumerations nêu chi tiết các kiểu dữ liệu có thể liệt kê liên kết với lớp hiện tại.

Đối với mỗi enumeration, trang nêu tên của nó rồi liệt kê các giá trị có thể có.

Đối với mỗi giá trị enumeration, trang nêu tên, giá trị integer và giải thích về trường hợp sử dụng và/hoặc tác động của nó.

Constants
---------

.. image:: img/class_api_constants.webp

Danh sách Constants nêu chi tiết các hằng số integer có tên trong lớp hiện tại.

Đối với mỗi constant, trang nêu tên, giá trị integer và giải thích về trường hợp sử dụng và/hoặc tác động của nó.

Mô tả của các constant ``NOTIFICATION_*`` sẽ nêu sự kiện engine nào kích hoạt thông báo.

Mô tả Property
--------------

.. image:: img/class_api_property_descriptions.webp

Danh sách Property Descriptions nêu chi tiết mọi thông tin về từng property.

Phần này nhắc lại kiểu dữ liệu và tên của property.

Mọi property trong API Godot đều được liên kết với một cặp hàm setter và getter. Sử dụng một trong hai là tương đương nhau. Chúng được liệt kê ở đây.

Bên dưới là phần tóm tắt chi tiết về nội dung dữ liệu của property biểu thị, các trường hợp sử dụng và/hoặc tác động của việc thay đổi property. Phần này có thể bao gồm các mẫu mã và/hoặc liên kết đến những phần liên quan của API Godot.

.. note:: Biết tên của setter và getter rất hữu ích khi cần liên kết tên method hoặc :ref:`Callable<class_Callable>` với một thứ gì đó.

Mô tả Method
------------

.. image:: img/class_api_method_descriptions.webp

Danh sách Method Descriptions nêu chi tiết mọi thông tin về từng method.

Phần này nhắc lại kiểu dữ liệu trả về của method, tên/kiểu/giá trị mặc định của các tham số và các qualifier.

Bên dưới là phần tóm tắt chi tiết về hoạt động của method và các trường hợp sử dụng của nó. Phần này có thể bao gồm các mẫu mã và/hoặc liên kết đến những phần liên quan của API Godot.
