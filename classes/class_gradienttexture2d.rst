:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GradientTexture2D.xml.

.. _class_GradientTexture2D:

GradientTexture2D
=================

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture 2D tạo ra một mẫu với các màu lấy từ một :ref:`Gradient<class_Gradient>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một texture 2D lấy các màu từ một :ref:`Gradient<class_Gradient>` để điền dữ liệu texture. Texture này có thể chuyển đổi sự chuyển tiếp màu thành các mẫu khác nhau, chẳng hạn như gradient tuyến tính hoặc gradient xuyên tâm. Theo mặc định, texture được điền bằng cách nội suy màu, bắt đầu từ các offset :ref:`fill_from<class_GradientTexture2D_property_fill_from>` đến :ref:`fill_to<class_GradientTexture2D_property_fill_to>`, nhưng phần điền gradient có thể được lặp lại để phủ toàn bộ texture.

Gradient được lấy mẫu riêng cho từng pixel nên không nhất thiết thể hiện bản sao chính xác của gradient (xem :ref:`width<class_GradientTexture2D_property_width>` và :ref:`height<class_GradientTexture2D_property_height>`). Xem thêm :ref:`GradientTexture1D<class_GradientTexture1D>`, :ref:`CurveTexture<class_CurveTexture>` và :ref:`CurveXYZTexture<class_CurveXYZTexture>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Fill<enum_GradientTexture2D_Fill>`     | :ref:`fill<class_GradientTexture2D_property_fill>`           | ``0``                                                                                  |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                | :ref:`fill_from<class_GradientTexture2D_property_fill_from>` | ``Vector2(0, 0)``                                                                      |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                | :ref:`fill_to<class_GradientTexture2D_property_fill_to>`     | ``Vector2(1, 0)``                                                                      |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Gradient<class_Gradient>`              | :ref:`gradient<class_GradientTexture2D_property_gradient>`   |                                                                                        |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                        | :ref:`height<class_GradientTexture2D_property_height>`       | ``64``                                                                                 |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Repeat<enum_GradientTexture2D_Repeat>` | :ref:`repeat<class_GradientTexture2D_property_repeat>`       | ``0``                                                                                  |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                      | resource_local_to_scene                                      | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                      | :ref:`use_hdr<class_GradientTexture2D_property_use_hdr>`     | ``false``                                                                              |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                        | :ref:`width<class_GradientTexture2D_property_width>`         | ``64``                                                                                 |
   +----------------------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_GradientTexture2D_Fill:

.. rst-class:: classref-enumeration

enum **Fill**: :ref:`🔗<enum_GradientTexture2D_Fill>`

.. _class_GradientTexture2D_constant_FILL_LINEAR:

.. rst-class:: classref-enumeration-constant

:ref:`Fill<enum_GradientTexture2D_Fill>` **FILL_LINEAR** = ``0``

Các màu được nội suy tuyến tính theo một đường thẳng.

.. _class_GradientTexture2D_constant_FILL_RADIAL:

.. rst-class:: classref-enumeration-constant

:ref:`Fill<enum_GradientTexture2D_Fill>` **FILL_RADIAL** = ``1``

Các màu được nội suy tuyến tính theo một mẫu hình tròn.

.. _class_GradientTexture2D_constant_FILL_SQUARE:

.. rst-class:: classref-enumeration-constant

:ref:`Fill<enum_GradientTexture2D_Fill>` **FILL_SQUARE** = ``2``

Các màu được nội suy tuyến tính theo một mẫu hình vuông.

.. _class_GradientTexture2D_constant_FILL_CONIC:

.. rst-class:: classref-enumeration-constant

:ref:`Fill<enum_GradientTexture2D_Fill>` **FILL_CONIC** = ``3``

Các màu được nội suy tuyến tính theo một mẫu hình nón.

.. rst-class:: classref-item-separator

----

.. _enum_GradientTexture2D_Repeat:

.. rst-class:: classref-enumeration

enum **Repeat**: :ref:`🔗<enum_GradientTexture2D_Repeat>`

.. _class_GradientTexture2D_constant_REPEAT_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`Repeat<enum_GradientTexture2D_Repeat>` **REPEAT_NONE** = ``0``

Phần điền gradient bị giới hạn trong phạm vi được xác định bởi các offset từ :ref:`fill_from<class_GradientTexture2D_property_fill_from>` đến :ref:`fill_to<class_GradientTexture2D_property_fill_to>`.

.. _class_GradientTexture2D_constant_REPEAT:

.. rst-class:: classref-enumeration-constant

:ref:`Repeat<enum_GradientTexture2D_Repeat>` **REPEAT** = ``1``

Texture được điền bắt đầu từ các offset :ref:`fill_from<class_GradientTexture2D_property_fill_from>` đến :ref:`fill_to<class_GradientTexture2D_property_fill_to>`, lặp lại cùng một mẫu theo cả hai hướng.

.. _class_GradientTexture2D_constant_REPEAT_MIRROR:

.. rst-class:: classref-enumeration-constant

:ref:`Repeat<enum_GradientTexture2D_Repeat>` **REPEAT_MIRROR** = ``2``

Texture được điền bắt đầu từ các offset :ref:`fill_from<class_GradientTexture2D_property_fill_from>` đến :ref:`fill_to<class_GradientTexture2D_property_fill_to>`, phản chiếu mẫu theo cả hai hướng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GradientTexture2D_property_fill:

.. rst-class:: classref-property

:ref:`Fill<enum_GradientTexture2D_Fill>` **fill** = ``0`` :ref:`🔗<class_GradientTexture2D_property_fill>`

.. rst-class:: classref-property-setget

- |void| **set_fill**\ (\ value\: :ref:`Fill<enum_GradientTexture2D_Fill>`\ ) - :ref:`Fill<enum_GradientTexture2D_Fill>` **get_fill**\ (\ )

Kiểu điền của gradient.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_fill_from:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **fill_from** = ``Vector2(0, 0)`` :ref:`🔗<class_GradientTexture2D_property_fill_from>`

.. rst-class:: classref-property-setget

- |void| **set_fill_from**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_fill_from**\ (\ )

Offset ban đầu được sử dụng để điền texture, được chỉ định trong tọa độ UV.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_fill_to:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **fill_to** = ``Vector2(1, 0)`` :ref:`🔗<class_GradientTexture2D_property_fill_to>`

.. rst-class:: classref-property-setget

- |void| **set_fill_to**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_fill_to**\ (\ )

Offset cuối cùng được sử dụng để điền texture, được chỉ định trong tọa độ UV.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_gradient:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **gradient** :ref:`🔗<class_GradientTexture2D_property_gradient>`

.. rst-class:: classref-property-setget

- |void| **set_gradient**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_gradient**\ (\ )

:ref:`Gradient<class_Gradient>` được sử dụng để điền texture.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_height:

.. rst-class:: classref-property

:ref:`int<class_int>` **height** = ``64`` :ref:`🔗<class_GradientTexture2D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_height**\ (\ )

Số lượng mẫu màu theo chiều dọc sẽ được lấy từ :ref:`Gradient<class_Gradient>`, đồng thời cũng biểu thị chiều cao của texture.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_repeat:

.. rst-class:: classref-property

:ref:`Repeat<enum_GradientTexture2D_Repeat>` **repeat** = ``0`` :ref:`🔗<class_GradientTexture2D_property_repeat>`

.. rst-class:: classref-property-setget

- |void| **set_repeat**\ (\ value\: :ref:`Repeat<enum_GradientTexture2D_Repeat>`\ ) - :ref:`Repeat<enum_GradientTexture2D_Repeat>` **get_repeat**\ (\ )

Kiểu lặp lại của gradient.

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_use_hdr:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_hdr** = ``false`` :ref:`🔗<class_GradientTexture2D_property_use_hdr>`

.. rst-class:: classref-property-setget

- |void| **set_use_hdr**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_hdr**\ (\ )

Nếu ``true``, texture được tạo sẽ hỗ trợ dải tương phản động cao (:ref:`Image.FORMAT_RGBAF<class_Image_constant_FORMAT_RGBAF>` format). Điều này cho phép các hiệu ứng phát sáng hoạt động nếu :ref:`Environment.glow_enabled<class_Environment_property_glow_enabled>` là ``true``. Nếu ``false``, texture được tạo sẽ sử dụng dải tương phản động thấp; các màu quá sáng sẽ bị giới hạn (:ref:`Image.FORMAT_RGBA8<class_Image_constant_FORMAT_RGBA8>` format).

.. rst-class:: classref-item-separator

----

.. _class_GradientTexture2D_property_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **width** = ``64`` :ref:`🔗<class_GradientTexture2D_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_width**\ (\ )

Số lượng mẫu màu theo chiều ngang sẽ được lấy từ :ref:`Gradient<class_Gradient>`, đồng thời cũng biểu thị chiều rộng của texture.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
