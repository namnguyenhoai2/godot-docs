:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/DPITexture.xml.

.. _class_DPITexture:

DPITexture
==========

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`Texture2D<class_Texture2D>` có khả năng tự động thay đổi kích thước dựa trên ảnh SVG.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một :ref:`Texture2D<class_Texture2D>` có khả năng tự động thay đổi kích thước dựa trên ảnh SVG. **DPITexture**\ s được dùng để tự động rasterize lại các biểu tượng và những phần tử UI khác của theme dựa trên texture nhằm khớp với tỷ lệ viewport và mức oversampling của font. Xem thêm :ref:`ProjectSettings.display/window/stretch/mode<class_ProjectSettings_property_display/window/stretch/mode>` (chế độ "canvas_items") và :ref:`Viewport.oversampling_override<class_Viewport_property_oversampling_override>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`base_scale<class_DPITexture_property_base_scale>`             | ``1.0``                                                                                |
   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`color_map<class_DPITexture_property_color_map>`               | ``{}``                                                                                 |
   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`fix_alpha_border<class_DPITexture_property_fix_alpha_border>` | ``false``                                                                              |
   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`premult_alpha<class_DPITexture_property_premult_alpha>`       | ``false``                                                                              |
   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | resource_local_to_scene                                             | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`saturation<class_DPITexture_property_saturation>`             | ``1.0``                                                                                |
   +-------------------------------------+---------------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`DPITexture<class_DPITexture>` | :ref:`create_from_string<class_DPITexture_method_create_from_string>`\ (\ source\: :ref:`String<class_String>`, scale\: :ref:`float<class_float>` = 1.0, saturation\: :ref:`float<class_float>` = 1.0, color_map\: :ref:`Dictionary<class_Dictionary>` = {}\ ) |static| |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`               | :ref:`get_scaled_rid<class_DPITexture_method_get_scaled_rid>`\ (\ ) |const|                                                                                                                                                                                             |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`         | :ref:`get_source<class_DPITexture_method_get_source>`\ (\ ) |const|                                                                                                                                                                                                     |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_size_override<class_DPITexture_method_set_size_override>`\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ )                                                                                                                                                       |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_source<class_DPITexture_method_set_source>`\ (\ source\: :ref:`String<class_String>`\ )                                                                                                                                                                       |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_DPITexture_property_base_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **base_scale** = ``1.0`` :ref:`🔗<class_DPITexture_property_base_scale>`

.. rst-class:: classref-property-setget

- |void| **set_base_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_base_scale**\ (\ )

Tỷ lệ texture. ``1.0`` là kích thước SVG ban đầu. Giá trị cao hơn sẽ tạo ra hình ảnh lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_property_color_map:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **color_map** = ``{}`` :ref:`🔗<class_DPITexture_property_color_map>`

.. rst-class:: classref-property-setget

- |void| **set_color_map**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_color_map**\ (\ )

If set, remaps texture colors according to :ref:`Color<class_Color>`-:ref:`Color<class_Color>` map.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_property_fix_alpha_border:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **fix_alpha_border** = ``false`` :ref:`🔗<class_DPITexture_property_fix_alpha_border>`

.. rst-class:: classref-property-setget

- |void| **set_fix_alpha_border**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_fix_alpha_border**\ (\ )

Nếu là ``true``, đặt các pixel có cùng màu xung quanh vào vùng chuyển tiếp từ trong suốt sang không trong suốt. Đối với texture được hiển thị bằng bộ lọc song tuyến tính, tùy chọn này giúp giảm hiệu ứng đường viền khi xuất hình ảnh từ trình chỉnh sửa ảnh.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_property_premult_alpha:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **premult_alpha** = ``false`` :ref:`🔗<class_DPITexture_property_premult_alpha>`

.. rst-class:: classref-property-setget

- |void| **set_premult_alpha**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_premult_alpha**\ (\ )

Một cách thay thế cho việc sửa các đường viền bị tối bằng :ref:`fix_alpha_border<class_DPITexture_property_fix_alpha_border>` là sử dụng alpha nhân trước (premultiplied alpha). Khi bật tùy chọn này, texture sẽ được chuyển đổi sang định dạng này. Texture alpha nhân trước yêu cầu các material cụ thể để được hiển thị chính xác:

- Trong 2D, cần tạo một :ref:`CanvasItemMaterial<class_CanvasItemMaterial>` và cấu hình để sử dụng chế độ blend :ref:`CanvasItemMaterial.BLEND_MODE_PREMULT_ALPHA<class_CanvasItemMaterial_constant_BLEND_MODE_PREMULT_ALPHA>` trên :ref:`CanvasItem<class_CanvasItem>`\ s sử dụng texture này. Trong các shader ``canvas_item`` tùy chỉnh, nên sử dụng ``render_mode blend_premul_alpha;``.

- Trong 3D, cần tạo một :ref:`BaseMaterial3D<class_BaseMaterial3D>` và cấu hình để sử dụng chế độ blend :ref:`BaseMaterial3D.BLEND_MODE_PREMULT_ALPHA<class_BaseMaterial3D_constant_BLEND_MODE_PREMULT_ALPHA>` trên các material sử dụng texture này. Trong các shader ``spatial`` tùy chỉnh, nên sử dụng ``render_mode blend_premul_alpha;``.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_property_saturation:

.. rst-class:: classref-property

:ref:`float<class_float>` **saturation** = ``1.0`` :ref:`🔗<class_DPITexture_property_saturation>`

.. rst-class:: classref-property-setget

- |void| **set_saturation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_saturation**\ (\ )

Ghi đè độ bão hòa của texture.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_DPITexture_method_create_from_string:

.. rst-class:: classref-method

:ref:`DPITexture<class_DPITexture>` **create_from_string**\ (\ source\: :ref:`String<class_String>`, scale\: :ref:`float<class_float>` = 1.0, saturation\: :ref:`float<class_float>` = 1.0, color_map\: :ref:`Dictionary<class_Dictionary>` = {}\ ) |static| :ref:`🔗<class_DPITexture_method_create_from_string>`

Tạo một **DPITexture** mới và khởi tạo nó bằng cách cấp phát và thiết lập dữ liệu SVG thành ``source``.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_method_get_scaled_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_scaled_rid**\ (\ ) |const| :ref:`🔗<class_DPITexture_method_get_scaled_rid>`

Trả về :ref:`RID<class_RID>` của texture đã được rasterize để khớp với mức oversampling của canvas item hiện đang được vẽ.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_method_get_source:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_source**\ (\ ) |const| :ref:`🔗<class_DPITexture_method_get_source>`

Trả về mã nguồn của texture SVG này.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_method_set_size_override:

.. rst-class:: classref-method

|void| **set_size_override**\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_DPITexture_method_set_size_override>`

Thay đổi kích thước texture theo các chiều được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_DPITexture_method_set_source:

.. rst-class:: classref-method

|void| **set_source**\ (\ source\: :ref:`String<class_String>`\ ) :ref:`🔗<class_DPITexture_method_set_source>`

Thiết lập mã nguồn của texture SVG này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
