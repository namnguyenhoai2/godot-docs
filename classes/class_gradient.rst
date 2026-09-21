:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Gradient.xml.

.. _class_Gradient:

Gradient
========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một chuyển tiếp màu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Resource này mô tả một chuyển tiếp màu bằng cách xác định một tập hợp các điểm màu và cách nội suy giữa chúng.

Xem thêm :ref:`Curve<class_Curve>`, hỗ trợ các phương pháp easing phức tạp hơn nhưng không hỗ trợ màu.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>`           | :ref:`colors<class_Gradient_property_colors>`                                       | ``PackedColorArray(0, 0, 0, 1, 1, 1, 1, 1)`` |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------+
   | :ref:`ColorSpace<enum_Gradient_ColorSpace>`               | :ref:`interpolation_color_space<class_Gradient_property_interpolation_color_space>` | ``0``                                        |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------+
   | :ref:`InterpolationMode<enum_Gradient_InterpolationMode>` | :ref:`interpolation_mode<class_Gradient_property_interpolation_mode>`               | ``0``                                        |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>`       | :ref:`offsets<class_Gradient_property_offsets>`                                     | ``PackedFloat32Array(0, 1)``                 |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------+----------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`add_point<class_Gradient_method_add_point>`\ (\ offset\: :ref:`float<class_float>`, color\: :ref:`Color<class_Color>`\ ) |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>` | :ref:`get_color<class_Gradient_method_get_color>`\ (\ point\: :ref:`int<class_int>`\ )                                         |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_offset<class_Gradient_method_get_offset>`\ (\ point\: :ref:`int<class_int>`\ )                                       |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`get_point_count<class_Gradient_method_get_point_count>`\ (\ ) |const|                                                    |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`remove_point<class_Gradient_method_remove_point>`\ (\ point\: :ref:`int<class_int>`\ )                                   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`reverse<class_Gradient_method_reverse>`\ (\ )                                                                            |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>` | :ref:`sample<class_Gradient_method_sample>`\ (\ offset\: :ref:`float<class_float>`\ )                                          |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_color<class_Gradient_method_set_color>`\ (\ point\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ )      |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_offset<class_Gradient_method_set_offset>`\ (\ point\: :ref:`int<class_int>`, offset\: :ref:`float<class_float>`\ )   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Gradient_InterpolationMode:

.. rst-class:: classref-enumeration

enum **InterpolationMode**: :ref:`🔗<enum_Gradient_InterpolationMode>`

.. _class_Gradient_constant_GRADIENT_INTERPOLATE_LINEAR:

.. rst-class:: classref-enumeration-constant

:ref:`InterpolationMode<enum_Gradient_InterpolationMode>` **GRADIENT_INTERPOLATE_LINEAR** = ``0``

Nội suy tuyến tính.

.. _class_Gradient_constant_GRADIENT_INTERPOLATE_CONSTANT:

.. rst-class:: classref-enumeration-constant

:ref:`InterpolationMode<enum_Gradient_InterpolationMode>` **GRADIENT_INTERPOLATE_CONSTANT** = ``1``

Nội suy hằng, màu thay đổi đột ngột tại mỗi điểm và giữ nguyên giữa các điểm. Trong một số trường hợp, điều này có thể gây aliasing rõ rệt khi được dùng cho texture gradient.

.. _class_Gradient_constant_GRADIENT_INTERPOLATE_CUBIC:

.. rst-class:: classref-enumeration-constant

:ref:`InterpolationMode<enum_Gradient_InterpolationMode>` **GRADIENT_INTERPOLATE_CUBIC** = ``2``

Nội suy cubic.

.. rst-class:: classref-item-separator

----

.. _enum_Gradient_ColorSpace:

.. rst-class:: classref-enumeration

enum **ColorSpace**: :ref:`🔗<enum_Gradient_ColorSpace>`

.. _class_Gradient_constant_GRADIENT_COLOR_SPACE_SRGB:

.. rst-class:: classref-enumeration-constant

:ref:`ColorSpace<enum_Gradient_ColorSpace>` **GRADIENT_COLOR_SPACE_SRGB** = ``0``

Không gian màu sRGB.

.. _class_Gradient_constant_GRADIENT_COLOR_SPACE_LINEAR_SRGB:

.. rst-class:: classref-enumeration-constant

:ref:`ColorSpace<enum_Gradient_ColorSpace>` **GRADIENT_COLOR_SPACE_LINEAR_SRGB** = ``1``

Không gian màu sRGB tuyến tính.

.. _class_Gradient_constant_GRADIENT_COLOR_SPACE_OKLAB:

.. rst-class:: classref-enumeration-constant

:ref:`ColorSpace<enum_Gradient_ColorSpace>` **GRADIENT_COLOR_SPACE_OKLAB** = ``2``

`Oklab <https://bottosson.github.io/posts/oklab/>`__ không gian màu. Không gian màu này tạo ra chuyển tiếp mượt mà và có vẻ đồng nhất giữa các màu.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Gradient_property_colors:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **colors** = ``PackedColorArray(0, 0, 0, 1, 1, 1, 1, 1)`` :ref:`🔗<class_Gradient_property_colors>`

.. rst-class:: classref-property-setget

- |void| **set_colors**\ (\ value\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) - :ref:`PackedColorArray<class_PackedColorArray>` **get_colors**\ (\ )

Các màu của Gradient dưới dạng một :ref:`PackedColorArray<class_PackedColorArray>`.

\ **Lưu ý:** Việc thiết lập thuộc tính này sẽ cập nhật tất cả màu cùng lúc. Để cập nhật riêng lẻ từng màu, hãy dùng :ref:`set_color()<class_Gradient_method_set_color>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_property_interpolation_color_space:

.. rst-class:: classref-property

:ref:`ColorSpace<enum_Gradient_ColorSpace>` **interpolation_color_space** = ``0`` :ref:`🔗<class_Gradient_property_interpolation_color_space>`

.. rst-class:: classref-property-setget

- |void| **set_interpolation_color_space**\ (\ value\: :ref:`ColorSpace<enum_Gradient_ColorSpace>`\ ) - :ref:`ColorSpace<enum_Gradient_ColorSpace>` **get_interpolation_color_space**\ (\ )

Không gian màu được dùng để nội suy giữa các điểm của gradient. Nó không ảnh hưởng đến các màu được trả về; các màu này luôn sử dụng encoding sRGB phi tuyến.

\ **Lưu ý:** Thiết lập này không có tác dụng khi :ref:`interpolation_mode<class_Gradient_property_interpolation_mode>` được đặt thành :ref:`GRADIENT_INTERPOLATE_CONSTANT<class_Gradient_constant_GRADIENT_INTERPOLATE_CONSTANT>`.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_property_interpolation_mode:

.. rst-class:: classref-property

:ref:`InterpolationMode<enum_Gradient_InterpolationMode>` **interpolation_mode** = ``0`` :ref:`🔗<class_Gradient_property_interpolation_mode>`

.. rst-class:: classref-property-setget

- |void| **set_interpolation_mode**\ (\ value\: :ref:`InterpolationMode<enum_Gradient_InterpolationMode>`\ ) - :ref:`InterpolationMode<enum_Gradient_InterpolationMode>` **get_interpolation_mode**\ (\ )

Thuật toán được dùng để nội suy giữa các điểm của gradient.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_property_offsets:

.. rst-class:: classref-property

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **offsets** = ``PackedFloat32Array(0, 1)`` :ref:`🔗<class_Gradient_property_offsets>`

.. rst-class:: classref-property-setget

- |void| **set_offsets**\ (\ value\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) - :ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_offsets**\ (\ )

Các offset của Gradient dưới dạng một :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

\ **Lưu ý:** Việc thiết lập thuộc tính này sẽ cập nhật tất cả offset cùng lúc. Để cập nhật riêng lẻ từng offset, hãy dùng :ref:`set_offset()<class_Gradient_method_set_offset>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat32Array<class_PackedFloat32Array>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Gradient_method_add_point:

.. rst-class:: classref-method

|void| **add_point**\ (\ offset\: :ref:`float<class_float>`, color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_Gradient_method_add_point>`

Thêm màu được chỉ định vào gradient, với offset được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_get_color:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_color**\ (\ point\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Gradient_method_get_color>`

Trả về màu của màu gradient tại chỉ mục ``point``.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_get_offset:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_offset**\ (\ point\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Gradient_method_get_offset>`

Trả về offset của màu gradient tại chỉ mục ``point``.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_get_point_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_point_count**\ (\ ) |const| :ref:`🔗<class_Gradient_method_get_point_count>`

Trả về số lượng màu trong gradient.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_remove_point:

.. rst-class:: classref-method

|void| **remove_point**\ (\ point\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Gradient_method_remove_point>`

Xóa màu tại chỉ mục ``point``.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_reverse:

.. rst-class:: classref-method

|void| **reverse**\ (\ ) :ref:`🔗<class_Gradient_method_reverse>`

Đảo ngược/phản chiếu gradient.

\ **Lưu ý:** Phương thức này phản chiếu tất cả các điểm quanh trung điểm của gradient, điều này có thể tạo ra kết quả không mong muốn khi :ref:`interpolation_mode<class_Gradient_property_interpolation_mode>` được đặt thành :ref:`GRADIENT_INTERPOLATE_CONSTANT<class_Gradient_constant_GRADIENT_INTERPOLATE_CONSTANT>`.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_sample:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **sample**\ (\ offset\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Gradient_method_sample>`

Trả về màu được nội suy do ``offset`` chỉ định. ``offset`` phải nằm giữa ``0.0`` và ``1.0`` (bao gồm cả hai). Sử dụng giá trị nhỏ hơn ``0.0`` sẽ trả về cùng màu với ``0.0``, còn sử dụng giá trị lớn hơn ``1.0`` sẽ trả về cùng màu với ``1.0``. Nếu giá trị đầu vào không nằm trong phạm vi này, hãy cân nhắc sử dụng :ref:`@GlobalScope.remap()<class_@GlobalScope_method_remap>` trên giá trị đầu vào với các giá trị đầu ra được đặt thành ``0.0`` và ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_set_color:

.. rst-class:: classref-method

|void| **set_color**\ (\ point\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_Gradient_method_set_color>`

Đặt màu của màu gradient tại chỉ mục ``point``.

.. rst-class:: classref-item-separator

----

.. _class_Gradient_method_set_offset:

.. rst-class:: classref-method

|void| **set_offset**\ (\ point\: :ref:`int<class_int>`, offset\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Gradient_method_set_offset>`

Đặt offset cho màu gradient tại chỉ mục ``point``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
