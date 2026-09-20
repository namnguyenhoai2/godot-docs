.. _doc_how_to_read_the_godot_api:

Cách đọc Godot API
==================

Trong trang này, bạn sẽ học cách đọc tài liệu tham chiếu lớp cho Godot API.

API, hay Application Programming Interface, là mục lục về những gì Godot cung cấp cho người dùng. API cung cấp phần tóm tắt ngắn gọn về các lớp hiện có, mối quan hệ giữa chúng, các tính năng của chúng và cách sử dụng chúng.

Kế thừa
-------

.. image:: img/class_api_inheritance.webp

Ở đầu mỗi tệp, bạn sẽ thấy tên của lớp.

Phần "Inherits" liệt kê từng lớp mà lớp hiện tại kế thừa. Ở đây ``CanvasItem`` kế thừa ``Node`` và ``Node`` kế thừa ``Object``.

Phần "Inherited By" liệt kê từng lớp trực tiếp kế thừa lớp hiện tại. Ở đây cả ``Control`` và ``Node2D`` đều kế thừa ``CanvasItem``.

Mô tả ngắn gọn
--------------

.. image:: img/class_api_brief_description.webp

Tiếp theo là phần mô tả ngắn gọn về lớp. Văn bản này xuất hiện trong các cửa sổ bật lên của Godot Editor để tạo Nodes, Resources và các kiểu khác.

Mô tả
-----

.. image:: img/class_api_description.webp

Tiếp theo là phần mô tả chi tiết hơn về lớp, các tính năng và trường hợp sử dụng của lớp.

Những nội dung bạn có thể tìm thấy ở đây:

1. Các chi tiết cụ thể về cách lớp hoạt động.

2. Các mẫu code về những trường hợp sử dụng phổ biến.

3. Các chi tiết sử dụng được dùng chung giữa từng method của lớp.

4. Các cảnh báo về dependency hoặc configuration bắt buộc.

5. Các liên kết đến những phần liên quan khác của Godot API.

Tutorials
---------

.. image:: img/class_api_tutorials.webp

Sau đó, trang cung cấp các liên kết đến những phần của manual có đề cập hoặc sử dụng lớp hiện tại.

Properties
----------

.. image:: img/class_api_properties_table.webp

Bảng Properties liệt kê các biến thuộc về từng instance của lớp, còn được gọi là "properties".

Cột bên trái chứa data type của property. Văn bản này cũng là một liên kết đến trang Godot API của data type đó.

Cột ở giữa chứa tên của property. Văn bản này cũng là một liên kết đến phần mô tả đầy đủ của property trên trang. Sử dụng tên này để lấy dữ liệu của property hoặc đặt giá trị mới cho nó.

Cột bên phải chứa giá trị mặc định của property. Để khởi tạo property bằng một giá trị khác, bạn phải đặt giá trị khác thông qua script hoặc Inspector.

Methods
-------

.. image:: img/class_api_methods_table.webp

Bảng Methods liệt kê các function thuộc về từng instance của lớp, còn được gọi là "methods".

Cột bên trái chứa data type của giá trị trả về từ method.

Cột bên phải chứa tên, parameters và qualifiers của method. Tên là phần văn bản đứng trước dấu ngoặc đơn mở. Đây cũng là một liên kết đến phần mô tả đầy đủ của method trên trang. Sử dụng tên này để gọi method.

Với mỗi parameter, trang nêu chi tiết data type, tên và giá trị mặc định của parameter, nếu có.

Các qualifier có thể bao gồm...

- ``const``: method không thay đổi bất kỳ dữ liệu nào trong instance của lớp. - ``virtual``: method không làm gì ngoài việc chờ một script override nó. - ``vararg``: method có thể nhận một số lượng arguments tùy ý.

Signals
-------

.. image:: img/class_api_signals.webp

Danh sách Signals nêu chi tiết tên và parameters của các event "signal" một thay đổi trong trạng thái game đến những instance lớp khác.

Giống như bảng Methods, mọi parameter đều bao gồm data type và tên của parameter.

Mỗi signal cũng có phần giải thích chi tiết về thời điểm signal được phát.

Enumerations
------------

.. image:: img/class_api_enumerations.webp

Danh sách Enumerations nêu chi tiết các enumerable data type được liên kết với lớp hiện tại.

Với mỗi enumeration, trang nêu tên của enumeration rồi liệt kê các giá trị có thể có.

Với mỗi giá trị enumeration, trang nêu tên, giá trị integer và phần giải thích về trường hợp sử dụng và/hoặc ảnh hưởng của giá trị đó.

Constants
---------

.. image:: img/class_api_constants.webp

Danh sách Constants nêu chi tiết các hằng số integer có tên trong lớp hiện tại.

Với mỗi constant, trang nêu tên, giá trị integer và phần giải thích về trường hợp sử dụng và/hoặc ảnh hưởng của constant đó.

Mô tả của các constant ``NOTIFICATION_*`` sẽ nêu engine event nào kích hoạt notification.

Mô tả Property
--------------

.. image:: img/class_api_property_descriptions.webp

Danh sách Property Descriptions nêu chi tiết mọi thông tin về từng property.

Phần này nhắc lại data type và tên của property.

Mọi property trong Godot API đều được liên kết với một cặp setter và getter function. Sử dụng một trong hai là tương đương nhau. Chúng được liệt kê ở đây.

Bên dưới là phần tóm tắt chi tiết về ý nghĩa dữ liệu của property, các trường hợp sử dụng và/hoặc ảnh hưởng của việc thay đổi property. Phần này có thể bao gồm các mẫu code và/hoặc liên kết đến những phần liên quan của Godot API.

.. note:: Knowing the setter and getter names is useful when one must bind a
          tên method hoặc :ref:`Callable<class_Callable>` thành một thứ gì đó.

Mô tả Method
------------

.. image:: img/class_api_method_descriptions.webp

Danh sách Method Descriptions nêu chi tiết mọi thông tin về từng method.

Phần này nhắc lại data type giá trị trả về của method, tên/type/default của các parameter và các qualifier.

Bên dưới là phần tóm tắt chi tiết về chức năng của method và các trường hợp sử dụng của method. Phần này có thể bao gồm các mẫu code và/hoặc liên kết đến những phần liên quan của Godot API.
