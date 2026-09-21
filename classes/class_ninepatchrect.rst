:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/NinePatchRect.xml.

.. _class_NinePatchRect:

NinePatchRect
=============

**Kế thừa:** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một control hiển thị texture bằng cách giữ nguyên các góc, nhưng lát các cạnh và phần trung tâm.

.. rst-class:: classref-introduction-group

Mô tả
-----

Còn được gọi là panel 9-slice, **NinePatchRect** tạo ra các panel gọn gàng với mọi kích thước dựa trên một texture nhỏ. Để thực hiện việc này, nó chia texture thành một lưới 3×3. Khi scale node, nó lát các cạnh của texture theo chiều ngang hoặc chiều dọc, lát phần trung tâm trên cả hai trục và giữ nguyên các góc.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` | :ref:`axis_stretch_horizontal<class_NinePatchRect_property_axis_stretch_horizontal>` | ``0``                                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` | :ref:`axis_stretch_vertical<class_NinePatchRect_property_axis_stretch_vertical>`     | ``0``                                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                    | :ref:`draw_center<class_NinePatchRect_property_draw_center>`                         | ``true``                                                              |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`MouseFilter<enum_Control_MouseFilter>`               | mouse_filter                                                                         | ``2`` (overrides :ref:`Control<class_Control_property_mouse_filter>`) |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`                                      | :ref:`patch_margin_bottom<class_NinePatchRect_property_patch_margin_bottom>`         | ``0``                                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`                                      | :ref:`patch_margin_left<class_NinePatchRect_property_patch_margin_left>`             | ``0``                                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`                                      | :ref:`patch_margin_right<class_NinePatchRect_property_patch_margin_right>`           | ``0``                                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`                                      | :ref:`patch_margin_top<class_NinePatchRect_property_patch_margin_top>`               | ``0``                                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`                                  | :ref:`region_rect<class_NinePatchRect_property_region_rect>`                         | ``Rect2(0, 0, 0, 0)``                                                 |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`                          | :ref:`texture<class_NinePatchRect_property_texture>`                                 |                                                                       |
   +------------------------------------------------------------+--------------------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`get_patch_margin<class_NinePatchRect_method_get_patch_margin>`\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                        |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                | :ref:`set_patch_margin<class_NinePatchRect_method_set_patch_margin>`\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, value\: :ref:`int<class_int>`\ ) |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_NinePatchRect_signal_texture_changed:

.. rst-class:: classref-signal

**texture_changed**\ (\ ) :ref:`🔗<class_NinePatchRect_signal_texture_changed>`

Được phát ra khi texture của node thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumeration
-----------

.. _enum_NinePatchRect_AxisStretchMode:

.. rst-class:: classref-enumeration

enum **AxisStretchMode**: :ref:`🔗<enum_NinePatchRect_AxisStretchMode>`

.. _class_NinePatchRect_constant_AXIS_STRETCH_MODE_STRETCH:

.. rst-class:: classref-enumeration-constant

:ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **AXIS_STRETCH_MODE_STRETCH** = ``0``

Kéo giãn texture trung tâm trên toàn bộ NinePatchRect. Điều này có thể khiến texture bị biến dạng.

.. _class_NinePatchRect_constant_AXIS_STRETCH_MODE_TILE:

.. rst-class:: classref-enumeration-constant

:ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **AXIS_STRETCH_MODE_TILE** = ``1``

Lặp lại texture trung tâm trên toàn bộ NinePatchRect. Cách này sẽ không gây biến dạng nhìn thấy được. Texture phải liền mạch để hoạt động mà không hiển thị hiện tượng lỗi giữa các cạnh.

.. _class_NinePatchRect_constant_AXIS_STRETCH_MODE_TILE_FIT:

.. rst-class:: classref-enumeration-constant

:ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **AXIS_STRETCH_MODE_TILE_FIT** = ``2``

Lặp lại texture trung tâm trên toàn bộ NinePatchRect, đồng thời kéo giãn texture để đảm bảo mỗi tile đều hiển thị đầy đủ. Điều này có thể khiến texture bị biến dạng, nhưng ít hơn :ref:`AXIS_STRETCH_MODE_STRETCH<class_NinePatchRect_constant_AXIS_STRETCH_MODE_STRETCH>`. Texture phải liền mạch để hoạt động mà không hiển thị hiện tượng lỗi giữa các cạnh.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NinePatchRect_property_axis_stretch_horizontal:

.. rst-class:: classref-property

:ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **axis_stretch_horizontal** = ``0`` :ref:`🔗<class_NinePatchRect_property_axis_stretch_horizontal>`

.. rst-class:: classref-property-setget

- |void| **set_h_axis_stretch_mode**\ (\ value\: :ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>`\ ) - :ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **get_h_axis_stretch_mode**\ (\ )

Chế độ kéo giãn cần dùng cho việc kéo giãn/lát theo chiều ngang.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_axis_stretch_vertical:

.. rst-class:: classref-property

:ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **axis_stretch_vertical** = ``0`` :ref:`🔗<class_NinePatchRect_property_axis_stretch_vertical>`

.. rst-class:: classref-property-setget

- |void| **set_v_axis_stretch_mode**\ (\ value\: :ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>`\ ) - :ref:`AxisStretchMode<enum_NinePatchRect_AxisStretchMode>` **get_v_axis_stretch_mode**\ (\ )

Chế độ kéo giãn cần dùng cho việc kéo giãn/lát theo chiều dọc.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_draw_center:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **draw_center** = ``true`` :ref:`🔗<class_NinePatchRect_property_draw_center>`

.. rst-class:: classref-property-setget

- |void| **set_draw_center**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_draw_center_enabled**\ (\ )

Nếu ``true``, vẽ phần trung tâm của panel. Nếu không, chỉ vẽ các đường viền của 9-slice.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_patch_margin_bottom:

.. rst-class:: classref-property

:ref:`int<class_int>` **patch_margin_bottom** = ``0`` :ref:`🔗<class_NinePatchRect_property_patch_margin_bottom>`

.. rst-class:: classref-property-setget

- |void| **set_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Chiều cao của hàng dưới cùng của 9-slice. Margin bằng 16 nghĩa là các góc dưới và cạnh dưới của 9-slice sẽ có chiều cao 16 pixel. Bạn có thể đặt riêng lẻ cả 4 giá trị margin để tạo các panel có đường viền không đồng đều.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_patch_margin_left:

.. rst-class:: classref-property

:ref:`int<class_int>` **patch_margin_left** = ``0`` :ref:`🔗<class_NinePatchRect_property_patch_margin_left>`

.. rst-class:: classref-property-setget

- |void| **set_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Chiều rộng của cột bên trái của 9-slice. Margin bằng 16 nghĩa là các góc bên trái và cạnh bên trái của 9-slice sẽ có chiều rộng 16 pixel. Bạn có thể đặt riêng lẻ cả 4 giá trị margin để tạo các panel có đường viền không đồng đều.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_patch_margin_right:

.. rst-class:: classref-property

:ref:`int<class_int>` **patch_margin_right** = ``0`` :ref:`🔗<class_NinePatchRect_property_patch_margin_right>`

.. rst-class:: classref-property-setget

- |void| **set_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Chiều rộng của cột bên phải của 9-slice. Margin bằng 16 nghĩa là các góc bên phải và cạnh bên phải của 9-slice sẽ có chiều rộng 16 pixel. Bạn có thể đặt riêng lẻ cả 4 giá trị margin để tạo các panel có đường viền không đồng đều.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_patch_margin_top:

.. rst-class:: classref-property

:ref:`int<class_int>` **patch_margin_top** = ``0`` :ref:`🔗<class_NinePatchRect_property_patch_margin_top>`

.. rst-class:: classref-property-setget

- |void| **set_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Chiều cao của hàng trên cùng của 9-slice. Margin bằng 16 nghĩa là các góc trên và cạnh trên của 9-slice sẽ có chiều cao 16 pixel. Bạn có thể đặt riêng lẻ cả 4 giá trị margin để tạo các panel có đường viền không đồng đều.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_region_rect:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **region_rect** = ``Rect2(0, 0, 0, 0)`` :ref:`🔗<class_NinePatchRect_property_region_rect>`

.. rst-class:: classref-property-setget

- |void| **set_region_rect**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_region_rect**\ (\ )

Vùng hình chữ nhật của texture được lấy mẫu. Nếu bạn đang làm việc với atlas, hãy dùng thuộc tính này để xác định khu vực mà 9-slice sẽ sử dụng. Tất cả các thuộc tính khác đều tương đối so với vùng này. Nếu hình chữ nhật trống, NinePatchRect sẽ sử dụng toàn bộ texture.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_NinePatchRect_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

Resource texture của node.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NinePatchRect_method_get_patch_margin:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_NinePatchRect_method_get_patch_margin>`

Trả về kích thước margin trên :ref:`Side<enum_@GlobalScope_Side>` đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_NinePatchRect_method_set_patch_margin:

.. rst-class:: classref-method

|void| **set_patch_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, value\: :ref:`int<class_int>`\ ) :ref:`🔗<class_NinePatchRect_method_set_patch_margin>`

Đặt kích thước margin trên :ref:`Side<enum_@GlobalScope_Side>` đã chỉ định thành ``value`` pixel.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
