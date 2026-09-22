.. _doc_variant_class:

Lớp Variant
===========

Giới thiệu
----------

Variant là kiểu dữ liệu quan trọng nhất trong Godot. Một Variant chỉ chiếm 24 byte trên các nền tảng 64-bit (20 byte trên các nền tảng 32-bit) và có thể lưu trữ gần như mọi kiểu dữ liệu của engine bên trong nó. Variant hiếm khi được dùng để lưu giữ thông tin trong thời gian dài; thay vào đó, chúng chủ yếu được dùng cho việc giao tiếp, chỉnh sửa, serialization và nói chung là di chuyển dữ liệu.

Variant có thể:

-  Lưu trữ gần như mọi kiểu dữ liệu.
-  Thực hiện các phép toán giữa nhiều Variant (GDScript sử dụng Variant làm kiểu dữ liệu nguyên tử/native).
-  Được băm, nhờ đó có thể nhanh chóng so sánh với các Variant khác.
-  Được dùng để chuyển đổi an toàn giữa các kiểu dữ liệu.
-  Được dùng để trừu tượng hóa việc gọi các phương thức và đối số của chúng (Godot xuất tất cả các hàm của mình thông qua Variant).
-  Được dùng để trì hoãn các lệnh gọi hoặc di chuyển dữ liệu giữa các thread.
-  Được serialization dưới dạng nhị phân và lưu vào đĩa, hoặc truyền qua mạng.
-  Được serialization thành văn bản và dùng để in các giá trị cũng như các thiết lập có thể chỉnh sửa.
-  Hoạt động như một thuộc tính được export, để trình chỉnh sửa có thể chỉnh sửa nó một cách thống nhất.
-  Được dùng cho dictionary, array, parser, v.v.

Về cơ bản, nhờ lớp Variant, việc tự viết Godot trở nên dễ dàng hơn rất, rất nhiều, vì nó cho phép tạo các cấu trúc có tính động cao vốn không phổ biến trong C++ với rất ít công sức. Hãy trở thành bạn của Variant ngay hôm nay.

.. note::

    Tất cả các kiểu trong Variant ngoại trừ Nil và Object **không thể** là ``null`` và luôn phải lưu trữ một giá trị hợp lệ. Vì vậy, các kiểu này trong Variant được gọi là kiểu *không nullable*.

    Một trong các kiểu của Variant là *Nil*, kiểu này chỉ có thể lưu trữ giá trị ``null``. Do đó, một Variant có thể chứa giá trị ``null``, mặc dù tất cả các kiểu của Variant, ngoại trừ Nil và Object, đều không nullable.

Tài liệu tham khảo
~~~~~~~~~~~~~~~~~~

-  `core/variant/variant.h <https://github.com/godotengine/godot/blob/master/core/variant/variant.h>`__

Danh sách các kiểu Variant
--------------------------

Các kiểu sau khả dụng trong Variant:

+-----------------------------------+-----------------------+
| Kiểu                              | Ghi chú               |
+===================================+=======================+
| Nil (chỉ có thể lưu trữ ``null``) | Kiểu nullable         |
+-----------------------------------+-----------------------+
| :ref:`class_bool`                 |                       |
+-----------------------------------+-----------------------+
| :ref:`class_int`                  |                       |
+-----------------------------------+-----------------------+
| :ref:`class_float`                |                       |
+-----------------------------------+-----------------------+
| :ref:`class_string`               |                       |
+-----------------------------------+-----------------------+
| :ref:`class_vector2`              |                       |
+-----------------------------------+-----------------------+
| :ref:`class_vector2i`             |                       |
+-----------------------------------+-----------------------+
| :ref:`class_rect2`                | Đối ngẫu 2D của AABB  |
+-----------------------------------+-----------------------+
| :ref:`class_rect2i`               |                       |
+-----------------------------------+-----------------------+
| :ref:`class_vector3`              |                       |
+-----------------------------------+-----------------------+
| :ref:`class_vector3i`             |                       |
+-----------------------------------+-----------------------+
| :ref:`class_transform2d`          |                       |
+-----------------------------------+-----------------------+
| :ref:`class_vector4`              |                       |
+-----------------------------------+-----------------------+
| :ref:`class_vector4i`             |                       |
+-----------------------------------+-----------------------+
| :ref:`class_plane`                |                       |
+-----------------------------------+-----------------------+
| :ref:`class_quaternion`           |                       |
+-----------------------------------+-----------------------+
| :ref:`class_aabb`                 | Đối ngẫu 3D của Rect2 |
+-----------------------------------+-----------------------+
| :ref:`class_basis`                |                       |
+-----------------------------------+-----------------------+
| :ref:`class_transform3d`          |                       |
+-----------------------------------+-----------------------+
| :ref:`class_projection`           |                       |
+-----------------------------------+-----------------------+
| :ref:`class_color`                |                       |
+-----------------------------------+-----------------------+
| :ref:`class_stringname`           |                       |
+-----------------------------------+-----------------------+
| :ref:`class_nodepath`             |                       |
+-----------------------------------+-----------------------+
| :ref:`class_rid`                  |                       |
+-----------------------------------+-----------------------+
| :ref:`class_object`               | Kiểu nullable         |
+-----------------------------------+-----------------------+
| :ref:`class_callable`             |                       |
+-----------------------------------+-----------------------+
| :ref:`class_signal`               |                       |
+-----------------------------------+-----------------------+
| :ref:`class_dictionary`           |                       |
+-----------------------------------+-----------------------+
| :ref:`class_array`                |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedbytearray`      |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedint32array`     |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedint64array`     |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedfloat32array`   |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedfloat64array`   |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedstringarray`    |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedvector2array`   |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedvector3array`   |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedcolorarray`     |                       |
+-----------------------------------+-----------------------+
| :ref:`class_packedvector4array`   |                       |
+-----------------------------------+-----------------------+

Container: Array và Dictionary
------------------------------

Cả :ref:`class_array` và :ref:`class_dictionary` đều được triển khai bằng Variant. Một Dictionary có thể ghép bất kỳ kiểu dữ liệu nào được dùng làm key với bất kỳ kiểu dữ liệu nào khác. Một Array chỉ chứa một mảng các Variant. Tất nhiên, một Variant cũng có thể chứa một Dictionary hoặc một Array bên trong, khiến nó càng linh hoạt hơn.

Các thay đổi đối với một container sẽ thay đổi tất cả các tham chiếu đến nó. Nên tạo một :ref:`Mutex <doc_core_concurrency_types>` để khóa container nếu
muốn có :ref:`truy cập đa luồng <doc_using_multiple_threads>`.

Tài liệu tham khảo
~~~~~~~~~~~~~~~~~~

-  `core/variant/dictionary.h <https://github.com/godotengine/godot/blob/master/core/variant/dictionary.h>`__
-  `core/variant/array.h <https://github.com/godotengine/godot/blob/master/core/variant/array.h>`__
