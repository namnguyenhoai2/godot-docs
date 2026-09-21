:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Line2D.xml.

.. _class_Line2D:

Line2D
======

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một polyline 2D có thể được áp dụng texture tùy chọn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này vẽ một polyline 2D, tức là một hình dạng gồm nhiều điểm được nối với nhau bằng các đoạn. **Line2D** không phải là một polyline toán học, tức là các đoạn không mỏng vô hạn. Node này được thiết kế để render và có thể được tô màu cũng như áp dụng texture tùy chọn.

\ **Cảnh báo:** Một số cấu hình có thể không thể vẽ đẹp, chẳng hạn như các góc rất nhọn. Trong những trường hợp này, node sử dụng logic vẽ dự phòng để hiển thị trông hợp lý.

\ **Lưu ý:** **Line2D** được vẽ bằng mesh 2D.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Matrix Transform Demo <https://godotengine.org/asset-library/asset/2787>`__

- `2.5D Game Demo <https://godotengine.org/asset-library/asset/2783>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`antialiased<class_Line2D_property_antialiased>`         | ``false``                |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`LineCapMode<enum_Line2D_LineCapMode>`         | :ref:`begin_cap_mode<class_Line2D_property_begin_cap_mode>`   | ``0``                    |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`closed<class_Line2D_property_closed>`                   | ``false``                |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`                           | :ref:`default_color<class_Line2D_property_default_color>`     | ``Color(1, 1, 1, 1)``    |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`LineCapMode<enum_Line2D_LineCapMode>`         | :ref:`end_cap_mode<class_Line2D_property_end_cap_mode>`       | ``0``                    |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`Gradient<class_Gradient>`                     | :ref:`gradient<class_Line2D_property_gradient>`               |                          |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`LineJointMode<enum_Line2D_LineJointMode>`     | :ref:`joint_mode<class_Line2D_property_joint_mode>`           | ``0``                    |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`points<class_Line2D_property_points>`                   | ``PackedVector2Array()`` |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`int<class_int>`                               | :ref:`round_precision<class_Line2D_property_round_precision>` | ``8``                    |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`sharp_limit<class_Line2D_property_sharp_limit>`         | ``2.0``                  |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`Texture2D<class_Texture2D>`                   | :ref:`texture<class_Line2D_property_texture>`                 |                          |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`LineTextureMode<enum_Line2D_LineTextureMode>` | :ref:`texture_mode<class_Line2D_property_texture_mode>`       | ``0``                    |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`width<class_Line2D_property_width>`                     | ``10.0``                 |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+
   | :ref:`Curve<class_Curve>`                           | :ref:`width_curve<class_Line2D_property_width_curve>`         |                          |
   +-----------------------------------------------------+---------------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`add_point<class_Line2D_method_add_point>`\ (\ position\: :ref:`Vector2<class_Vector2>`, index\: :ref:`int<class_int>` = -1\ )              |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`clear_points<class_Line2D_method_clear_points>`\ (\ )                                                                                      |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_point_count<class_Line2D_method_get_point_count>`\ (\ ) |const|                                                                        |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_point_position<class_Line2D_method_get_point_position>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                   |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`remove_point<class_Line2D_method_remove_point>`\ (\ index\: :ref:`int<class_int>`\ )                                                       |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_point_position<class_Line2D_method_set_point_position>`\ (\ index\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ ) |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Line2D_LineJointMode:

.. rst-class:: classref-enumeration

enum **LineJointMode**: :ref:`🔗<enum_Line2D_LineJointMode>`

.. _class_Line2D_constant_LINE_JOINT_SHARP:

.. rst-class:: classref-enumeration-constant

:ref:`LineJointMode<enum_Line2D_LineJointMode>` **LINE_JOINT_SHARP** = ``0``

Làm cho các mối nối của polyline nhọn, nối các cạnh của hai đoạn bằng cách kéo dài chúng cho đến khi giao nhau. Nếu góc xoay của một mối nối quá lớn (dựa trên :ref:`sharp_limit<class_Line2D_property_sharp_limit>`), mối nối sẽ chuyển sang :ref:`LINE_JOINT_BEVEL<class_Line2D_constant_LINE_JOINT_BEVEL>` để ngăn các miter quá dài.

.. _class_Line2D_constant_LINE_JOINT_BEVEL:

.. rst-class:: classref-enumeration-constant

:ref:`LineJointMode<enum_Line2D_LineJointMode>` **LINE_JOINT_BEVEL** = ``1``

Làm cho các mối nối của polyline được vát, nối các cạnh của hai đoạn bằng một đường thẳng đơn giản.

.. _class_Line2D_constant_LINE_JOINT_ROUND:

.. rst-class:: classref-enumeration-constant

:ref:`LineJointMode<enum_Line2D_LineJointMode>` **LINE_JOINT_ROUND** = ``2``

Làm cho các mối nối của polyline được bo tròn, nối các cạnh của hai đoạn bằng một cung tròn. Độ chi tiết của cung tròn này phụ thuộc vào :ref:`round_precision<class_Line2D_property_round_precision>`.

.. rst-class:: classref-item-separator

----

.. _enum_Line2D_LineCapMode:

.. rst-class:: classref-enumeration

enum **LineCapMode**: :ref:`🔗<enum_Line2D_LineCapMode>`

.. _class_Line2D_constant_LINE_CAP_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`LineCapMode<enum_Line2D_LineCapMode>` **LINE_CAP_NONE** = ``0``

Không vẽ đầu mút đường.

.. _class_Line2D_constant_LINE_CAP_BOX:

.. rst-class:: classref-enumeration-constant

:ref:`LineCapMode<enum_Line2D_LineCapMode>` **LINE_CAP_BOX** = ``1``

Vẽ đầu mút đường dưới dạng hình hộp, kéo dài nhẹ đoạn đầu/cuối.

.. _class_Line2D_constant_LINE_CAP_ROUND:

.. rst-class:: classref-enumeration-constant

:ref:`LineCapMode<enum_Line2D_LineCapMode>` **LINE_CAP_ROUND** = ``2``

Vẽ đầu mút đường dưới dạng hình bán nguyệt gắn với đoạn đầu/cuối.

.. rst-class:: classref-item-separator

----

.. _enum_Line2D_LineTextureMode:

.. rst-class:: classref-enumeration

enum **LineTextureMode**: :ref:`🔗<enum_Line2D_LineTextureMode>`

.. _class_Line2D_constant_LINE_TEXTURE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`LineTextureMode<enum_Line2D_LineTextureMode>` **LINE_TEXTURE_NONE** = ``0``

Lấy các pixel bên trái của texture và render chúng trên toàn bộ polyline.

.. _class_Line2D_constant_LINE_TEXTURE_TILE:

.. rst-class:: classref-enumeration-constant

:ref:`LineTextureMode<enum_Line2D_LineTextureMode>` **LINE_TEXTURE_TILE** = ``1``

Lặp texture trên toàn bộ polyline. :ref:`CanvasItem.texture_repeat<class_CanvasItem_property_texture_repeat>` của node **Line2D** phải là :ref:`CanvasItem.TEXTURE_REPEAT_ENABLED<class_CanvasItem_constant_TEXTURE_REPEAT_ENABLED>` hoặc :ref:`CanvasItem.TEXTURE_REPEAT_MIRROR<class_CanvasItem_constant_TEXTURE_REPEAT_MIRROR>` để hoạt động đúng cách.

.. _class_Line2D_constant_LINE_TEXTURE_STRETCH:

.. rst-class:: classref-enumeration-constant

:ref:`LineTextureMode<enum_Line2D_LineTextureMode>` **LINE_TEXTURE_STRETCH** = ``2``

Kéo giãn texture trên toàn bộ polyline. :ref:`CanvasItem.texture_repeat<class_CanvasItem_property_texture_repeat>` của node **Line2D** phải là :ref:`CanvasItem.TEXTURE_REPEAT_DISABLED<class_CanvasItem_constant_TEXTURE_REPEAT_DISABLED>` để đạt kết quả tốt nhất.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Line2D_property_antialiased:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **antialiased** = ``false`` :ref:`🔗<class_Line2D_property_antialiased>`

.. rst-class:: classref-property-setget

- |void| **set_antialiased**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_antialiased**\ (\ )

Nếu ``true``, đường viền của polyline sẽ được anti-alias.

\ **Lưu ý:** **Line2D** không được batching tăng tốc khi sử dụng anti-alias.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_begin_cap_mode:

.. rst-class:: classref-property

:ref:`LineCapMode<enum_Line2D_LineCapMode>` **begin_cap_mode** = ``0`` :ref:`🔗<class_Line2D_property_begin_cap_mode>`

.. rst-class:: classref-property-setget

- |void| **set_begin_cap_mode**\ (\ value\: :ref:`LineCapMode<enum_Line2D_LineCapMode>`\ ) - :ref:`LineCapMode<enum_Line2D_LineCapMode>` **get_begin_cap_mode**\ (\ )

Kiểu dáng của phần đầu polyline, nếu :ref:`closed<class_Line2D_property_closed>` là ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_closed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **closed** = ``false`` :ref:`🔗<class_Line2D_property_closed>`

.. rst-class:: classref-property-setget

- |void| **set_closed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_closed**\ (\ )

Nếu ``true`` và polyline có hơn 2 điểm, điểm cuối và điểm đầu sẽ được nối với nhau bằng một đoạn.

\ **Lưu ý:** Hình dạng của đoạn đóng không được đảm bảo liền mạch nếu cung cấp :ref:`width_curve<class_Line2D_property_width_curve>`.

\ **Lưu ý:** Mối nối giữa đoạn đóng và đoạn đầu tiên được vẽ trước, đồng thời lấy mẫu :ref:`gradient<class_Line2D_property_gradient>` và :ref:`width_curve<class_Line2D_property_width_curve>` tại phần đầu. Đây là chi tiết triển khai có thể thay đổi trong phiên bản tương lai.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_default_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **default_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Line2D_property_default_color>`

.. rst-class:: classref-property-setget

- |void| **set_default_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_default_color**\ (\ )

Màu của polyline. Sẽ không được sử dụng nếu đã đặt gradient.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_end_cap_mode:

.. rst-class:: classref-property

:ref:`LineCapMode<enum_Line2D_LineCapMode>` **end_cap_mode** = ``0`` :ref:`🔗<class_Line2D_property_end_cap_mode>`

.. rst-class:: classref-property-setget

- |void| **set_end_cap_mode**\ (\ value\: :ref:`LineCapMode<enum_Line2D_LineCapMode>`\ ) - :ref:`LineCapMode<enum_Line2D_LineCapMode>` **get_end_cap_mode**\ (\ )

Kiểu dáng của phần cuối polyline, nếu :ref:`closed<class_Line2D_property_closed>` là ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_gradient:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **gradient** :ref:`🔗<class_Line2D_property_gradient>`

.. rst-class:: classref-property-setget

- |void| **set_gradient**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_gradient**\ (\ )

Gradient được vẽ xuyên suốt toàn bộ đường từ đầu đến cuối. :ref:`default_color<class_Line2D_property_default_color>` sẽ không được sử dụng nếu thuộc tính này được đặt.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_joint_mode:

.. rst-class:: classref-property

:ref:`LineJointMode<enum_Line2D_LineJointMode>` **joint_mode** = ``0`` :ref:`🔗<class_Line2D_property_joint_mode>`

.. rst-class:: classref-property-setget

- |void| **set_joint_mode**\ (\ value\: :ref:`LineJointMode<enum_Line2D_LineJointMode>`\ ) - :ref:`LineJointMode<enum_Line2D_LineJointMode>` **get_joint_mode**\ (\ )

Kiểu dáng của các kết nối giữa những đoạn của polyline.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_points:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **points** = ``PackedVector2Array()`` :ref:`🔗<class_Line2D_property_points>`

.. rst-class:: classref-property-setget

- |void| **set_points**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_points**\ (\ )

Các điểm của polyline, được diễn giải theo tọa độ 2D cục bộ. Các đoạn được vẽ giữa những điểm liền kề trong mảng này.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_round_precision:

.. rst-class:: classref-property

:ref:`int<class_int>` **round_precision** = ``8`` :ref:`🔗<class_Line2D_property_round_precision>`

.. rst-class:: classref-property-setget

- |void| **set_round_precision**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_round_precision**\ (\ )

Độ mượt được sử dụng cho các mối nối và đầu mút bo tròn. Giá trị cao hơn tạo ra các góc mượt hơn, nhưng yêu cầu nhiều tài nguyên hơn để render và cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_sharp_limit:

.. rst-class:: classref-property

:ref:`float<class_float>` **sharp_limit** = ``2.0`` :ref:`🔗<class_Line2D_property_sharp_limit>`

.. rst-class:: classref-property-setget

- |void| **set_sharp_limit**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_sharp_limit**\ (\ )

Xác định giới hạn miter của polyline. Thông thường, khi :ref:`joint_mode<class_Line2D_property_joint_mode>` được đặt thành :ref:`LINE_JOINT_SHARP<class_Line2D_constant_LINE_JOINT_SHARP>`, các góc nhọn sẽ chuyển sang sử dụng logic của các mối nối :ref:`LINE_JOINT_BEVEL<class_Line2D_constant_LINE_JOINT_BEVEL>` để ngăn miter quá dài. Giá trị cao hơn của thuộc tính này có nghĩa là việc chuyển sang mối nối vát sẽ xảy ra ở các góc nhọn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_Line2D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

Texture được sử dụng cho polyline. Sử dụng :ref:`texture_mode<class_Line2D_property_texture_mode>` để xác định kiểu vẽ.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_texture_mode:

.. rst-class:: classref-property

:ref:`LineTextureMode<enum_Line2D_LineTextureMode>` **texture_mode** = ``0`` :ref:`🔗<class_Line2D_property_texture_mode>`

.. rst-class:: classref-property-setget

- |void| **set_texture_mode**\ (\ value\: :ref:`LineTextureMode<enum_Line2D_LineTextureMode>`\ ) - :ref:`LineTextureMode<enum_Line2D_LineTextureMode>` **get_texture_mode**\ (\ )

Kiểu dùng để render :ref:`texture<class_Line2D_property_texture>` của polyline.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_width:

.. rst-class:: classref-property

:ref:`float<class_float>` **width** = ``10.0`` :ref:`🔗<class_Line2D_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_width**\ (\ )

Độ rộng của polyline.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_property_width_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **width_curve** :ref:`🔗<class_Line2D_property_width_curve>`

.. rst-class:: classref-property-setget

- |void| **set_curve**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_curve**\ (\ )

Đường cong độ rộng của polyline. Độ rộng của polyline trên toàn bộ chiều dài sẽ tương đương với giá trị của đường cong độ rộng trên miền xác định của nó. Đường cong độ rộng phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Line2D_method_add_point:

.. rst-class:: classref-method

|void| **add_point**\ (\ position\: :ref:`Vector2<class_Vector2>`, index\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_Line2D_method_add_point>`

Thêm một điểm với ``position`` được chỉ định, tương đối so với vị trí của polyline. Nếu không cung cấp ``index``, điểm mới sẽ được thêm vào cuối mảng điểm.

Nếu cung cấp ``index``, điểm mới sẽ được chèn trước điểm hiện có được xác định bởi index ``index``. Các index của những điểm sau điểm mới sẽ tăng thêm 1. ``index`` được cung cấp không được vượt quá số điểm hiện có trong polyline. Xem :ref:`get_point_count()<class_Line2D_method_get_point_count>`.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_method_clear_points:

.. rst-class:: classref-method

|void| **clear_points**\ (\ ) :ref:`🔗<class_Line2D_method_clear_points>`

Xóa tất cả các điểm khỏi polyline, khiến polyline trở thành rỗng.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_method_get_point_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_point_count**\ (\ ) |const| :ref:`🔗<class_Line2D_method_get_point_count>`

Trả về số điểm trong polyline.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_method_get_point_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_point_position**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Line2D_method_get_point_position>`

Trả về vị trí của điểm tại index ``index``.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_method_remove_point:

.. rst-class:: classref-method

|void| **remove_point**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Line2D_method_remove_point>`

Xóa điểm tại index ``index`` khỏi polyline.

.. rst-class:: classref-item-separator

----

.. _class_Line2D_method_set_point_position:

.. rst-class:: classref-method

|void| **set_point_position**\ (\ index\: :ref:`int<class_int>`, position\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Line2D_method_set_point_position>`

Ghi đè vị trí của điểm tại ``index`` đã cho bằng ``position`` được cung cấp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
