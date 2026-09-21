:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Light2D.xml.

.. _class_Light2D:

Light2D
=======

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`DirectionalLight2D<class_DirectionalLight2D>`, :ref:`PointLight2D<class_PointLight2D>`

Phát ánh sáng trong môi trường 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Phát ánh sáng trong môi trường 2D. Một ánh sáng được xác định bởi màu, giá trị năng lượng, chế độ (xem các hằng số) và nhiều tham số khác (liên quan đến phạm vi và bóng đổ).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Đèn và bóng đổ 2D <../tutorials/2d/2d_lights_and_shadows>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`BlendMode<enum_Light2D_BlendMode>`       | :ref:`blend_mode<class_Light2D_property_blend_mode>`                       | ``0``                 |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`                      | :ref:`color<class_Light2D_property_color>`                                 | ``Color(1, 1, 1, 1)`` |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                        | :ref:`editor_only<class_Light2D_property_editor_only>`                     | ``false``             |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                        | :ref:`enabled<class_Light2D_property_enabled>`                             | ``true``              |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                      | :ref:`energy<class_Light2D_property_energy>`                               | ``1.0``               |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                          | :ref:`range_item_cull_mask<class_Light2D_property_range_item_cull_mask>`   | ``1``                 |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                          | :ref:`range_layer_max<class_Light2D_property_range_layer_max>`             | ``0``                 |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                          | :ref:`range_layer_min<class_Light2D_property_range_layer_min>`             | ``0``                 |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                          | :ref:`range_z_max<class_Light2D_property_range_z_max>`                     | ``1024``              |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                          | :ref:`range_z_min<class_Light2D_property_range_z_min>`                     | ``-1024``             |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`                      | :ref:`shadow_color<class_Light2D_property_shadow_color>`                   | ``Color(0, 0, 0, 0)`` |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                        | :ref:`shadow_enabled<class_Light2D_property_shadow_enabled>`               | ``false``             |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`ShadowFilter<enum_Light2D_ShadowFilter>` | :ref:`shadow_filter<class_Light2D_property_shadow_filter>`                 | ``0``                 |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                      | :ref:`shadow_filter_smooth<class_Light2D_property_shadow_filter_smooth>`   | ``0.0``               |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                          | :ref:`shadow_item_cull_mask<class_Light2D_property_shadow_item_cull_mask>` | ``1``                 |
   +------------------------------------------------+----------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_height<class_Light2D_method_get_height>`\ (\ ) |const|                             |
   +---------------------------+----------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_height<class_Light2D_method_set_height>`\ (\ height\: :ref:`float<class_float>`\ ) |
   +---------------------------+----------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Light2D_ShadowFilter:

.. rst-class:: classref-enumeration

enum **ShadowFilter**: :ref:`🔗<enum_Light2D_ShadowFilter>`

.. _class_Light2D_constant_SHADOW_FILTER_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowFilter<enum_Light2D_ShadowFilter>` **SHADOW_FILTER_NONE** = ``0``

Không áp dụng bộ lọc nào cho shadow map. Điều này tạo ra các cạnh bóng cứng và là cách render nhanh nhất. Xem :ref:`shadow_filter<class_Light2D_property_shadow_filter>`.

.. _class_Light2D_constant_SHADOW_FILTER_PCF5:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowFilter<enum_Light2D_ShadowFilter>` **SHADOW_FILTER_PCF5** = ``1``

Áp dụng lọc phần trăm gần hơn (5 mẫu) cho shadow map. Cách này chậm hơn so với render bóng cứng. Xem :ref:`shadow_filter<class_Light2D_property_shadow_filter>`.

.. _class_Light2D_constant_SHADOW_FILTER_PCF13:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowFilter<enum_Light2D_ShadowFilter>` **SHADOW_FILTER_PCF13** = ``2``

Áp dụng lọc phần trăm gần hơn (13 mẫu) cho shadow map. Đây là chế độ lọc bóng chậm nhất và nên được sử dụng hạn chế. Xem :ref:`shadow_filter<class_Light2D_property_shadow_filter>`.

.. rst-class:: classref-item-separator

----

.. _enum_Light2D_BlendMode:

.. rst-class:: classref-enumeration

enum **BlendMode**: :ref:`🔗<enum_Light2D_BlendMode>`

.. _class_Light2D_constant_BLEND_MODE_ADD:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_Light2D_BlendMode>` **BLEND_MODE_ADD** = ``0``

Cộng giá trị của các pixel tương ứng với Light2D vào giá trị của các pixel bên dưới nó. Đây là hành vi phổ biến của ánh sáng.

.. _class_Light2D_constant_BLEND_MODE_SUB:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_Light2D_BlendMode>` **BLEND_MODE_SUB** = ``1``

Trừ giá trị của các pixel tương ứng với Light2D khỏi giá trị của các pixel bên dưới nó, tạo ra hiệu ứng ánh sáng đảo ngược.

.. _class_Light2D_constant_BLEND_MODE_MIX:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_Light2D_BlendMode>` **BLEND_MODE_MIX** = ``2``

Trộn giá trị của các pixel tương ứng với Light2D với giá trị của các pixel bên dưới nó bằng phép nội suy tuyến tính.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Light2D_property_blend_mode:

.. rst-class:: classref-property

:ref:`BlendMode<enum_Light2D_BlendMode>` **blend_mode** = ``0`` :ref:`🔗<class_Light2D_property_blend_mode>`

.. rst-class:: classref-property-setget

- |void| **set_blend_mode**\ (\ value\: :ref:`BlendMode<enum_Light2D_BlendMode>`\ ) - :ref:`BlendMode<enum_Light2D_BlendMode>` **get_blend_mode**\ (\ )

Chế độ blend của Light2D.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Light2D_property_color>`

.. rst-class:: classref-property-setget

- |void| **set_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_color**\ (\ )

The Light2D's :ref:`Color<class_Color>`.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_editor_only:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editor_only** = ``false`` :ref:`🔗<class_Light2D_property_editor_only>`

.. rst-class:: classref-property-setget

- |void| **set_editor_only**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_editor_only**\ (\ )

Nếu ``true``, Light2D sẽ chỉ xuất hiện khi đang chỉnh sửa scene.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** = ``true`` :ref:`🔗<class_Light2D_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_enabled**\ (\ )

Nếu ``true``, Light2D sẽ phát sáng.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **energy** = ``1.0`` :ref:`🔗<class_Light2D_property_energy>`

.. rst-class:: classref-property-setget

- |void| **set_energy**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_energy**\ (\ )

Giá trị năng lượng của Light2D. Giá trị càng lớn thì ánh sáng càng mạnh.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_range_item_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **range_item_cull_mask** = ``1`` :ref:`🔗<class_Light2D_property_range_item_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_item_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_item_cull_mask**\ (\ )

Layer mask. Chỉ các đối tượng có :ref:`CanvasItem.light_mask<class_CanvasItem_property_light_mask>` tương ứng mới chịu ảnh hưởng của Light2D. Xem thêm :ref:`shadow_item_cull_mask<class_Light2D_property_shadow_item_cull_mask>`, thuộc tính này xác định các đối tượng nào có thể tạo bóng.

\ **Lưu ý:** :ref:`range_item_cull_mask<class_Light2D_property_range_item_cull_mask>` bị :ref:`DirectionalLight2D<class_DirectionalLight2D>` bỏ qua; thuộc tính này sẽ luôn chiếu sáng một node 2D bất kể :ref:`CanvasItem.light_mask<class_CanvasItem_property_light_mask>` của node 2D đó.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_range_layer_max:

.. rst-class:: classref-property

:ref:`int<class_int>` **range_layer_max** = ``0`` :ref:`🔗<class_Light2D_property_range_layer_max>`

.. rst-class:: classref-property-setget

- |void| **set_layer_range_max**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_layer_range_max**\ (\ )

Giá trị layer tối đa của các đối tượng chịu ảnh hưởng của Light2D.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_range_layer_min:

.. rst-class:: classref-property

:ref:`int<class_int>` **range_layer_min** = ``0`` :ref:`🔗<class_Light2D_property_range_layer_min>`

.. rst-class:: classref-property-setget

- |void| **set_layer_range_min**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_layer_range_min**\ (\ )

Giá trị layer tối thiểu của các đối tượng chịu ảnh hưởng của Light2D.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_range_z_max:

.. rst-class:: classref-property

:ref:`int<class_int>` **range_z_max** = ``1024`` :ref:`🔗<class_Light2D_property_range_z_max>`

.. rst-class:: classref-property-setget

- |void| **set_z_range_max**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_z_range_max**\ (\ )

Giá trị ``z`` tối đa của các đối tượng chịu ảnh hưởng của Light2D.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_range_z_min:

.. rst-class:: classref-property

:ref:`int<class_int>` **range_z_min** = ``-1024`` :ref:`🔗<class_Light2D_property_range_z_min>`

.. rst-class:: classref-property-setget

- |void| **set_z_range_min**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_z_range_min**\ (\ )

Giá trị ``z`` tối thiểu của các đối tượng chịu ảnh hưởng của Light2D.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_shadow_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **shadow_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_Light2D_property_shadow_color>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_shadow_color**\ (\ )

:ref:`Color<class_Color>` của các bóng do Light2D tạo ra.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_shadow_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shadow_enabled** = ``false`` :ref:`🔗<class_Light2D_property_shadow_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_shadow_enabled**\ (\ )

Nếu ``true``, Light2D sẽ tạo bóng.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_shadow_filter:

.. rst-class:: classref-property

:ref:`ShadowFilter<enum_Light2D_ShadowFilter>` **shadow_filter** = ``0`` :ref:`🔗<class_Light2D_property_shadow_filter>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_filter**\ (\ value\: :ref:`ShadowFilter<enum_Light2D_ShadowFilter>`\ ) - :ref:`ShadowFilter<enum_Light2D_ShadowFilter>` **get_shadow_filter**\ (\ )

Kiểu bộ lọc bóng.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_shadow_filter_smooth:

.. rst-class:: classref-property

:ref:`float<class_float>` **shadow_filter_smooth** = ``0.0`` :ref:`🔗<class_Light2D_property_shadow_filter_smooth>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_smooth**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_shadow_smooth**\ (\ )

Giá trị làm mượt cho bóng. Giá trị cao hơn sẽ tạo ra bóng mềm hơn, nhưng phải đánh đổi bằng các vệt nhìn thấy được có thể xuất hiện khi render bóng. :ref:`shadow_filter_smooth<class_Light2D_property_shadow_filter_smooth>` chỉ có tác dụng nếu :ref:`shadow_filter<class_Light2D_property_shadow_filter>` là :ref:`SHADOW_FILTER_PCF5<class_Light2D_constant_SHADOW_FILTER_PCF5>` hoặc :ref:`SHADOW_FILTER_PCF13<class_Light2D_constant_SHADOW_FILTER_PCF13>`.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_property_shadow_item_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **shadow_item_cull_mask** = ``1`` :ref:`🔗<class_Light2D_property_shadow_item_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_item_shadow_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_item_shadow_cull_mask**\ (\ )

Shadow mask. Được sử dụng cùng với :ref:`LightOccluder2D<class_LightOccluder2D>` để tạo bóng. Chỉ các occluder có :ref:`CanvasItem.light_mask<class_CanvasItem_property_light_mask>` tương ứng mới tạo bóng. Xem thêm :ref:`range_item_cull_mask<class_Light2D_property_range_item_cull_mask>`, thuộc tính này xác định các đối tượng nào có thể *nhận* ánh sáng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Light2D_method_get_height:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_height**\ (\ ) |const| :ref:`🔗<class_Light2D_method_get_height>`

Trả về chiều cao của ánh sáng, được sử dụng trong normal mapping 2D. Xem :ref:`PointLight2D.height<class_PointLight2D_property_height>` và :ref:`DirectionalLight2D.height<class_DirectionalLight2D_property_height>`.

.. rst-class:: classref-item-separator

----

.. _class_Light2D_method_set_height:

.. rst-class:: classref-method

|void| **set_height**\ (\ height\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Light2D_method_set_height>`

Đặt chiều cao của ánh sáng, được sử dụng trong normal mapping 2D. Xem :ref:`PointLight2D.height<class_PointLight2D_property_height>` và :ref:`DirectionalLight2D.height<class_DirectionalLight2D_property_height>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
