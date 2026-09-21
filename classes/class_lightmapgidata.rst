:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LightmapGIData.xml.

.. _class_LightmapGIData:

LightmapGIData
==============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Chứa lightmap đã bake và dữ liệu probe của các đối tượng động cho :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**LightmapGIData** chứa lightmap đã bake và dữ liệu probe của các đối tượng động cho :ref:`LightmapGI<class_LightmapGI>`. Nó được thay thế mỗi khi lightmap được bake trong :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------+--------+
   | :ref:`TextureLayered<class_TextureLayered>`                              | :ref:`light_texture<class_LightmapGIData_property_light_texture>`             |        |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------+--------+
   | :ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\] | :ref:`lightmap_textures<class_LightmapGIData_property_lightmap_textures>`     | ``[]`` |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------+--------+
   | :ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\] | :ref:`shadowmask_textures<class_LightmapGIData_property_shadowmask_textures>` | ``[]`` |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`add_user<class_LightmapGIData_method_add_user>`\ (\ path\: :ref:`NodePath<class_NodePath>`, uv_scale\: :ref:`Rect2<class_Rect2>`, slice_index\: :ref:`int<class_int>`, sub_instance\: :ref:`int<class_int>`\ ) |
   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`clear_users<class_LightmapGIData_method_clear_users>`\ (\ )                                                                                                                                                    |
   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`           | :ref:`get_user_count<class_LightmapGIData_method_get_user_count>`\ (\ ) |const|                                                                                                                                      |
   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`get_user_path<class_LightmapGIData_method_get_user_path>`\ (\ user_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                      |
   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`is_using_spherical_harmonics<class_LightmapGIData_method_is_using_spherical_harmonics>`\ (\ ) |const|                                                                                                          |
   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                          | :ref:`set_uses_spherical_harmonics<class_LightmapGIData_method_set_uses_spherical_harmonics>`\ (\ uses_spherical_harmonics\: :ref:`bool<class_bool>`\ )                                                              |
   +---------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_LightmapGIData_ShadowmaskMode:

.. rst-class:: classref-enumeration

enum **ShadowmaskMode**: :ref:`🔗<enum_LightmapGIData_ShadowmaskMode>`

.. _class_LightmapGIData_constant_SHADOWMASK_MODE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>` **SHADOWMASK_MODE_NONE** = ``0``

Shadowmasking bị tắt. Không có texture shadowmask nào được tạo khi bake lightmap. Các texture shadowmask hiện có sẽ bị xóa trong quá trình bake.

.. _class_LightmapGIData_constant_SHADOWMASK_MODE_REPLACE:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>` **SHADOWMASK_MODE_REPLACE** = ``1``

Shadowmasking được bật. Các bóng định hướng nằm ngoài :ref:`DirectionalLight3D.directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>` sẽ được render bằng texture shadowmask. Các bóng nằm trong phạm vi sẽ chỉ được render bằng bóng real-time. Chế độ này cho phép bóng real-time ở khoảng cách gần chính xác hơn, không có hiệu ứng "smearing" tiềm ẩn có thể xảy ra khi sử dụng lightmap với texel size lớn. Nhược điểm là khi camera di chuyển nhanh, quá trình chuyển tiếp giữa ánh sáng real-time và shadowmask có thể trở nên rõ rệt. Ngoài ra, các đối tượng chỉ có bóng được bake trong shadowmask (và không có bóng real-time) sẽ không hiển thị bóng ở khoảng cách gần.

.. _class_LightmapGIData_constant_SHADOWMASK_MODE_OVERLAY:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>` **SHADOWMASK_MODE_OVERLAY** = ``2``

Shadowmasking được bật. Các bóng định hướng sẽ được render bằng bóng real-time phủ lên texture shadowmask. Chế độ này tạo ra quá trình chuyển tiếp bóng mượt hơn khi camera di chuyển nhanh, nhưng có thể gây hiệu ứng smearing đối với các bóng định hướng ở khoảng cách gần (do bóng real-time được trộn với shadowmask có độ phân giải thấp). Các đối tượng chỉ có bóng được bake trong shadowmask (và không có bóng real-time) sẽ giữ nguyên bóng ở khoảng cách gần.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_LightmapGIData_property_light_texture:

.. rst-class:: classref-property

:ref:`TextureLayered<class_TextureLayered>` **light_texture** :ref:`🔗<class_LightmapGIData_property_light_texture>`

.. rst-class:: classref-property-setget

- |void| **set_light_texture**\ (\ value\: :ref:`TextureLayered<class_TextureLayered>`\ ) - :ref:`TextureLayered<class_TextureLayered>` **get_light_texture**\ (\ )

**Đã deprecated:** Atlas lightmap hiện có thể chứa nhiều texture. Xem :ref:`lightmap_textures<class_LightmapGIData_property_lightmap_textures>`.

Texture atlas lightmap được tạo bởi lightmapper.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_property_lightmap_textures:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\] **lightmap_textures** = ``[]`` :ref:`🔗<class_LightmapGIData_property_lightmap_textures>`

.. rst-class:: classref-property-setget

- |void| **set_lightmap_textures**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\] **get_lightmap_textures**\ (\ )

Các texture atlas lightmap được tạo bởi lightmapper.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_property_shadowmask_textures:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\] **shadowmask_textures** = ``[]`` :ref:`🔗<class_LightmapGIData_property_shadowmask_textures>`

.. rst-class:: classref-property-setget

- |void| **set_shadowmask_textures**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`TextureLayered<class_TextureLayered>`\] **get_shadowmask_textures**\ (\ )

Các texture atlas shadowmask được tạo bởi lightmapper.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_LightmapGIData_method_add_user:

.. rst-class:: classref-method

|void| **add_user**\ (\ path\: :ref:`NodePath<class_NodePath>`, uv_scale\: :ref:`Rect2<class_Rect2>`, slice_index\: :ref:`int<class_int>`, sub_instance\: :ref:`int<class_int>`\ ) :ref:`🔗<class_LightmapGIData_method_add_user>`

Thêm một đối tượng được xem là đã bake trong **LightmapGIData** này.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_method_clear_users:

.. rst-class:: classref-method

|void| **clear_users**\ (\ ) :ref:`🔗<class_LightmapGIData_method_clear_users>`

Xóa tất cả đối tượng được xem là đã bake trong **LightmapGIData** này.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_method_get_user_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_user_count**\ (\ ) |const| :ref:`🔗<class_LightmapGIData_method_get_user_count>`

Trả về số lượng đối tượng được xem là đã bake trong **LightmapGIData** này.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_method_get_user_path:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_user_path**\ (\ user_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_LightmapGIData_method_get_user_path>`

Trả về :ref:`NodePath<class_NodePath>` của đối tượng đã bake tại chỉ mục ``user_idx``.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_method_is_using_spherical_harmonics:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_using_spherical_harmonics**\ (\ ) |const| :ref:`🔗<class_LightmapGIData_method_is_using_spherical_harmonics>`

Nếu ``true``, lightmap đã được bake với thông tin định hướng. Xem thêm :ref:`LightmapGI.directional<class_LightmapGI_property_directional>`.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGIData_method_set_uses_spherical_harmonics:

.. rst-class:: classref-method

|void| **set_uses_spherical_harmonics**\ (\ uses_spherical_harmonics\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_LightmapGIData_method_set_uses_spherical_harmonics>`

Nếu ``uses_spherical_harmonics`` là ``true``, cho engine biết phải xử lý dữ liệu lightmap như thể dữ liệu đó được bake với thông tin định hướng.

\ **Lưu ý:** Việc thay đổi giá trị này trên các lightmap đã bake sẽ không khiến chúng được bake lại. Điều này có nghĩa là diện mạo material sẽ không chính xác cho đến khi lightmap được bake lại; khi đó, giá trị được đặt ở đây sẽ bị loại bỏ vì toàn bộ resource **LightmapGIData** được lightmapper thay thế.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
