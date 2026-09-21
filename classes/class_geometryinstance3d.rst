:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GeometryInstance3D.xml.

.. _class_GeometryInstance3D:

GeometryInstance3D
==================

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CPUParticles3D<class_CPUParticles3D>`, :ref:`CSGShape3D<class_CSGShape3D>`, :ref:`GPUParticles3D<class_GPUParticles3D>`, :ref:`Label3D<class_Label3D>`, :ref:`MeshInstance3D<class_MeshInstance3D>`, :ref:`MultiMeshInstance3D<class_MultiMeshInstance3D>`, :ref:`SpriteBase3D<class_SpriteBase3D>`

Node cơ sở cho các visual instance dựa trên hình học.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node cơ sở cho các visual instance dựa trên hình học. Chia sẻ một số chức năng chung như khả năng hiển thị và material tùy chỉnh.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Các khoảng khả năng hiển thị (HLOD) <../tutorials/3d/visibility_ranges>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>`       | :ref:`cast_shadow<class_GeometryInstance3D_property_cast_shadow>`                                     | ``1``                      |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`AABB<class_AABB>`                                                         | :ref:`custom_aabb<class_GeometryInstance3D_property_custom_aabb>`                                     | ``AABB(0, 0, 0, 0, 0, 0)`` |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`extra_cull_margin<class_GeometryInstance3D_property_extra_cull_margin>`                         | ``0.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>`                     | :ref:`gi_lightmap_scale<class_GeometryInstance3D_property_gi_lightmap_scale>`                         | ``0``                      |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`             | ``1.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`GIMode<enum_GeometryInstance3D_GIMode>`                                   | :ref:`gi_mode<class_GeometryInstance3D_property_gi_mode>`                                             | ``1``                      |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                                         | :ref:`ignore_occlusion_culling<class_GeometryInstance3D_property_ignore_occlusion_culling>`           | ``false``                  |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`lod_bias<class_GeometryInstance3D_property_lod_bias>`                                           | ``1.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Material<class_Material>`                                                 | :ref:`material_overlay<class_GeometryInstance3D_property_material_overlay>`                           |                            |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Material<class_Material>`                                                 | :ref:`material_override<class_GeometryInstance3D_property_material_override>`                         |                            |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`transparency<class_GeometryInstance3D_property_transparency>`                                   | ``0.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`visibility_range_begin<class_GeometryInstance3D_property_visibility_range_begin>`               | ``0.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`visibility_range_begin_margin<class_GeometryInstance3D_property_visibility_range_begin_margin>` | ``0.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`visibility_range_end<class_GeometryInstance3D_property_visibility_range_end>`                   | ``0.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                                                       | :ref:`visibility_range_end_margin<class_GeometryInstance3D_property_visibility_range_end_margin>`     | ``0.0``                    |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>` | :ref:`visibility_range_fade_mode<class_GeometryInstance3D_property_visibility_range_fade_mode>`       | ``0``                      |
   +---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>` | :ref:`get_instance_shader_parameter<class_GeometryInstance3D_method_get_instance_shader_parameter>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_instance_shader_parameter<class_GeometryInstance3D_method_set_instance_shader_parameter>`\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) |
   +-------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_GeometryInstance3D_ShadowCastingSetting:

.. rst-class:: classref-enumeration

enum **ShadowCastingSetting**: :ref:`🔗<enum_GeometryInstance3D_ShadowCastingSetting>`

.. _class_GeometryInstance3D_constant_SHADOW_CASTING_SETTING_OFF:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` **SHADOW_CASTING_SETTING_OFF** = ``0``

Sẽ không tạo ra bất kỳ bóng nào. Sử dụng tùy chọn này để cải thiện hiệu năng cho hình học nhỏ, khó có khả năng tạo ra bóng đáng chú ý (chẳng hạn như mảnh vụn).

.. _class_GeometryInstance3D_constant_SHADOW_CASTING_SETTING_ON:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` **SHADOW_CASTING_SETTING_ON** = ``1``

Sẽ tạo bóng từ tất cả các mặt nhìn thấy trong GeometryInstance3D.

Sẽ tính đến việc culling, vì vậy các mặt không được render sẽ không được tính đến khi tạo bóng.

.. _class_GeometryInstance3D_constant_SHADOW_CASTING_SETTING_DOUBLE_SIDED:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` **SHADOW_CASTING_SETTING_DOUBLE_SIDED** = ``2``

Sẽ tạo bóng từ tất cả các mặt nhìn thấy trong GeometryInstance3D.

Sẽ không tính đến việc culling, vì vậy tất cả các mặt sẽ được tính đến khi tạo bóng.

.. _class_GeometryInstance3D_constant_SHADOW_CASTING_SETTING_SHADOWS_ONLY:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` **SHADOW_CASTING_SETTING_SHADOWS_ONLY** = ``3``

Chỉ hiển thị các bóng do đối tượng này tạo ra.

Nói cách khác, mesh thực tế sẽ không hiển thị, chỉ các bóng do mesh tạo ra mới hiển thị.

.. rst-class:: classref-item-separator

----

.. _enum_GeometryInstance3D_GIMode:

.. rst-class:: classref-enumeration

enum **GIMode**: :ref:`🔗<enum_GeometryInstance3D_GIMode>`

.. _class_GeometryInstance3D_constant_GI_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`GIMode<enum_GeometryInstance3D_GIMode>` **GI_MODE_DISABLED** = ``0``

Chế độ global illumination bị tắt. Sử dụng cho các đối tượng động không đóng góp vào global illumination (chẳng hạn như nhân vật). Khi sử dụng :ref:`VoxelGI<class_VoxelGI>` và SDFGI, hình học sẽ *nhận* ánh sáng gián tiếp và phản xạ, nhưng sẽ không được tính đến trong quá trình baking GI.

.. _class_GeometryInstance3D_constant_GI_MODE_STATIC:

.. rst-class:: classref-enumeration-constant

:ref:`GIMode<enum_GeometryInstance3D_GIMode>` **GI_MODE_STATIC** = ``1``

Chế độ global illumination đã bake. Sử dụng cho các đối tượng tĩnh đóng góp vào global illumination (chẳng hạn như hình học của level). Chế độ GI này có hiệu lực khi sử dụng :ref:`VoxelGI<class_VoxelGI>`, SDFGI và :ref:`LightmapGI<class_LightmapGI>`.

.. _class_GeometryInstance3D_constant_GI_MODE_DYNAMIC:

.. rst-class:: classref-enumeration-constant

:ref:`GIMode<enum_GeometryInstance3D_GIMode>` **GI_MODE_DYNAMIC** = ``2``

Chế độ global illumination động. Sử dụng cho các đối tượng động đóng góp vào global illumination. Chế độ GI này chỉ có hiệu lực khi sử dụng :ref:`VoxelGI<class_VoxelGI>`, nhưng ảnh hưởng đến hiệu năng nhiều hơn :ref:`GI_MODE_STATIC<class_GeometryInstance3D_constant_GI_MODE_STATIC>`. Khi sử dụng các phương thức GI khác, chế độ này sẽ hoạt động giống như :ref:`GI_MODE_DISABLED<class_GeometryInstance3D_constant_GI_MODE_DISABLED>`. Khi sử dụng :ref:`LightmapGI<class_LightmapGI>`, đối tượng sẽ nhận ánh sáng gián tiếp bằng lightmap probe thay vì texture lightmap đã bake.

.. rst-class:: classref-item-separator

----

.. _enum_GeometryInstance3D_LightmapScale:

.. rst-class:: classref-enumeration

enum **LightmapScale**: :ref:`🔗<enum_GeometryInstance3D_LightmapScale>`

.. _class_GeometryInstance3D_constant_LIGHTMAP_SCALE_1X:

.. rst-class:: classref-enumeration-constant

:ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **LIGHTMAP_SCALE_1X** = ``0``

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`.

Mật độ texel tiêu chuẩn cho lightmapping với :ref:`LightmapGI<class_LightmapGI>`.

.. _class_GeometryInstance3D_constant_LIGHTMAP_SCALE_2X:

.. rst-class:: classref-enumeration-constant

:ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **LIGHTMAP_SCALE_2X** = ``1``

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`.

Nhân mật độ texel lên 2× cho lightmapping với :ref:`LightmapGI<class_LightmapGI>`. Để đảm bảo mật độ texel nhất quán, hãy sử dụng tùy chọn này khi scale mesh theo hệ số từ 1.5 đến 3.0.

.. _class_GeometryInstance3D_constant_LIGHTMAP_SCALE_4X:

.. rst-class:: classref-enumeration-constant

:ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **LIGHTMAP_SCALE_4X** = ``2``

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`.

Nhân mật độ texel lên 4× cho lightmapping với :ref:`LightmapGI<class_LightmapGI>`. Để đảm bảo mật độ texel nhất quán, hãy sử dụng tùy chọn này khi scale mesh theo hệ số từ 3.0 đến 6.0.

.. _class_GeometryInstance3D_constant_LIGHTMAP_SCALE_8X:

.. rst-class:: classref-enumeration-constant

:ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **LIGHTMAP_SCALE_8X** = ``3``

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`.

Nhân mật độ texel lên 8× cho lightmapping với :ref:`LightmapGI<class_LightmapGI>`. Để đảm bảo mật độ texel nhất quán, hãy sử dụng tùy chọn này khi scale mesh theo hệ số lớn hơn 6.0.

.. _class_GeometryInstance3D_constant_LIGHTMAP_SCALE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **LIGHTMAP_SCALE_MAX** = ``4``

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`.

Biểu thị kích thước của enum :ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>`.

.. rst-class:: classref-item-separator

----

.. _enum_GeometryInstance3D_VisibilityRangeFadeMode:

.. rst-class:: classref-enumeration

enum **VisibilityRangeFadeMode**: :ref:`🔗<enum_GeometryInstance3D_VisibilityRangeFadeMode>`

.. _class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>` **VISIBILITY_RANGE_FADE_DISABLED** = ``0``

Sẽ không fade chính nó hoặc các visibility dependency của nó; thay vào đó sẽ sử dụng hysteresis. Đây là cách nhanh nhất để thực hiện LOD thủ công, nhưng có thể dẫn đến các chuyển đổi LOD dễ nhận thấy tùy thuộc vào cách tạo các mesh LOD. Xem :ref:`visibility_range_begin<class_GeometryInstance3D_property_visibility_range_begin>` và :ref:`Node3D.visibility_parent<class_Node3D_property_visibility_parent>` để biết thêm thông tin.

.. _class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_SELF:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>` **VISIBILITY_RANGE_FADE_SELF** = ``1``

Sẽ fade-out chính nó khi đạt đến các giới hạn trong khoảng khả năng hiển thị của nó. Cách này chậm hơn :ref:`VISIBILITY_RANGE_FADE_DISABLED<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED>`, nhưng có thể tạo ra các chuyển đổi mượt mà hơn. Khoảng fade được xác định bởi :ref:`visibility_range_begin_margin<class_GeometryInstance3D_property_visibility_range_begin_margin>` và :ref:`visibility_range_end_margin<class_GeometryInstance3D_property_visibility_range_end_margin>`.

\ **Lưu ý:** Chỉ được hỗ trợ khi sử dụng phương thức render Forward+. Khi sử dụng phương thức render Mobile hoặc Compatibility, chế độ này hoạt động như :ref:`VISIBILITY_RANGE_FADE_DISABLED<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED>` nhưng không bật hysteresis.

.. _class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DEPENDENCIES:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>` **VISIBILITY_RANGE_FADE_DEPENDENCIES** = ``2``

Sẽ fade-in các visibility dependency của nó (xem :ref:`Node3D.visibility_parent<class_Node3D_property_visibility_parent>`) khi đạt đến các giới hạn trong khoảng khả năng hiển thị của nó. Cách này chậm hơn :ref:`VISIBILITY_RANGE_FADE_DISABLED<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED>`, nhưng có thể tạo ra các chuyển đổi mượt mà hơn. Khoảng fade được xác định bởi :ref:`visibility_range_begin_margin<class_GeometryInstance3D_property_visibility_range_begin_margin>` và :ref:`visibility_range_end_margin<class_GeometryInstance3D_property_visibility_range_end_margin>`.

\ **Lưu ý:** Chỉ được hỗ trợ khi sử dụng phương thức render Forward+. Khi sử dụng phương thức render Mobile hoặc Compatibility, chế độ này hoạt động như :ref:`VISIBILITY_RANGE_FADE_DISABLED<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED>` nhưng không bật hysteresis.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GeometryInstance3D_property_cast_shadow:

.. rst-class:: classref-property

:ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` **cast_shadow** = ``1`` :ref:`🔗<class_GeometryInstance3D_property_cast_shadow>`

.. rst-class:: classref-property-setget

- |void| **set_cast_shadows_setting**\ (\ value\: :ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>`\ ) - :ref:`ShadowCastingSetting<enum_GeometryInstance3D_ShadowCastingSetting>` **get_cast_shadows_setting**\ (\ )

Chế độ được sử dụng để tạo bóng từ instance này.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_custom_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **custom_aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_GeometryInstance3D_property_custom_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_custom_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_custom_aabb**\ (\ )

Ghi đè bounding box của node này bằng một bounding box tùy chỉnh. Có thể sử dụng tùy chọn này để tránh việc tính toán lại :ref:`AABB<class_AABB>` tốn kém xảy ra khi một skeleton được sử dụng với :ref:`MeshInstance3D<class_MeshInstance3D>`, hoặc để kiểm soát chính xác bounding box của :ref:`MeshInstance3D<class_MeshInstance3D>`. Để sử dụng AABB mặc định, hãy đặt value thành một :ref:`AABB<class_AABB>` với tất cả các trường được đặt thành ``0.0``. Để tránh frustum culling, hãy đặt :ref:`custom_aabb<class_GeometryInstance3D_property_custom_aabb>` thành một AABB rất lớn bao phủ toàn bộ thế giới game, chẳng hạn như ``AABB(-10000, -10000, -10000, 20000, 20000, 20000)``. Để tắt mọi hình thức culling (bao gồm occlusion và layer culling), hãy gọi :ref:`RenderingServer.instance_set_ignore_culling()<class_RenderingServer_method_instance_set_ignore_culling>` trên :ref:`RID<class_RID>` của **GeometryInstance3D**.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_extra_cull_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **extra_cull_margin** = ``0.0`` :ref:`🔗<class_GeometryInstance3D_property_extra_cull_margin>`

.. rst-class:: classref-property-setget

- |void| **set_extra_cull_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_extra_cull_margin**\ (\ )

Khoảng cách bổ sung được thêm vào bounding box (:ref:`AABB<class_AABB>`) của GeometryInstance3D để mở rộng cull box của nó.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_gi_lightmap_scale:

.. rst-class:: classref-property

:ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **gi_lightmap_scale** = ``0`` :ref:`🔗<class_GeometryInstance3D_property_gi_lightmap_scale>`

.. rst-class:: classref-property-setget

- |void| **set_lightmap_scale**\ (\ value\: :ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>`\ ) - :ref:`LightmapScale<enum_GeometryInstance3D_LightmapScale>` **get_lightmap_scale**\ (\ )

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`.

Mật độ texel được sử dụng cho lightmapping trong :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_gi_lightmap_texel_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **gi_lightmap_texel_scale** = ``1.0`` :ref:`🔗<class_GeometryInstance3D_property_gi_lightmap_texel_scale>`

.. rst-class:: classref-property-setget

- |void| **set_lightmap_texel_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lightmap_texel_scale**\ (\ )

Mật độ texel được sử dụng cho lightmapping trong :ref:`LightmapGI<class_LightmapGI>`. Giá trị scale lớn hơn cung cấp độ phân giải cao hơn trong lightmap, có thể tạo ra bóng sắc nét hơn cho các nguồn sáng có cả ánh sáng trực tiếp và gián tiếp được bake. Tuy nhiên, giá trị scale lớn hơn cũng làm tăng không gian mesh chiếm dụng trong texture lightmap, từ đó làm tăng yêu cầu về bộ nhớ, dung lượng lưu trữ và thời gian bake. Khi sử dụng một mesh đơn ở các scale khác nhau, hãy cân nhắc điều chỉnh giá trị này để duy trì mật độ texel lightmap nhất quán giữa các mesh.

Ví dụ, tăng gấp đôi :ref:`gi_lightmap_texel_scale<class_GeometryInstance3D_property_gi_lightmap_texel_scale>` sẽ tăng gấp đôi độ phân giải texture lightmap của đối tượng này *trên mỗi trục*, vì vậy sẽ *tăng gấp bốn* số lượng texel.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_gi_mode:

.. rst-class:: classref-property

:ref:`GIMode<enum_GeometryInstance3D_GIMode>` **gi_mode** = ``1`` :ref:`🔗<class_GeometryInstance3D_property_gi_mode>`

.. rst-class:: classref-property-setget

- |void| **set_gi_mode**\ (\ value\: :ref:`GIMode<enum_GeometryInstance3D_GIMode>`\ ) - :ref:`GIMode<enum_GeometryInstance3D_GIMode>` **get_gi_mode**\ (\ )

Chế độ global illumination được sử dụng cho toàn bộ hình học. Để tránh kết quả không nhất quán, hãy sử dụng chế độ phù hợp với mục đích của mesh trong khi chơi (tĩnh/động).

\ **Lưu ý:** Chế độ bake của đèn cũng sẽ ảnh hưởng đến quá trình render global illumination. Xem :ref:`Light3D.light_bake_mode<class_Light3D_property_light_bake_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_ignore_occlusion_culling:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ignore_occlusion_culling** = ``false`` :ref:`🔗<class_GeometryInstance3D_property_ignore_occlusion_culling>`

.. rst-class:: classref-property-setget

- |void| **set_ignore_occlusion_culling**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_ignoring_occlusion_culling**\ (\ )

Nếu ``true``, tính năng occlusion culling sẽ bị vô hiệu hóa cho instance này. Hữu ích cho các gizmo phải được render ngay cả khi đang sử dụng occlusion culling.

\ **Lưu ý:** :ref:`ignore_occlusion_culling<class_GeometryInstance3D_property_ignore_occlusion_culling>` không ảnh hưởng đến frustum culling (xảy ra khi một đối tượng không hiển thị do góc nhìn của camera). Để tránh frustum culling, hãy đặt :ref:`custom_aabb<class_GeometryInstance3D_property_custom_aabb>` thành một AABB rất lớn bao phủ toàn bộ thế giới game của bạn, chẳng hạn như ``AABB(-10000, -10000, -10000, 20000, 20000, 20000)``.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_lod_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **lod_bias** = ``1.0`` :ref:`🔗<class_GeometryInstance3D_property_lod_bias>`

.. rst-class:: classref-property-setget

- |void| **set_lod_bias**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lod_bias**\ (\ )

Thay đổi tốc độ mesh chuyển sang level of detail thấp hơn. Giá trị 0 sẽ buộc mesh sử dụng level of detail thấp nhất, giá trị 1 sẽ sử dụng các thiết lập mặc định, còn các giá trị lớn hơn sẽ giữ mesh ở level of detail cao hơn khi ở khoảng cách xa hơn.

Hữu ích để kiểm thử quá trình chuyển đổi level of detail trong editor.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_material_overlay:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material_overlay** :ref:`🔗<class_GeometryInstance3D_property_material_overlay>`

.. rst-class:: classref-property-setget

- |void| **set_material_overlay**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material_overlay**\ (\ )

Material overlay cho toàn bộ hình học.

Nếu một material được gán cho thuộc tính này, nó sẽ được render bên trên mọi material đang hoạt động khác trên tất cả các bề mặt.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_material_override:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material_override** :ref:`🔗<class_GeometryInstance3D_property_material_override>`

.. rst-class:: classref-property-setget

- |void| **set_material_override**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material_override**\ (\ )

Material override cho toàn bộ hình học.

Nếu một material được gán cho thuộc tính này, nó sẽ được sử dụng thay cho bất kỳ material nào được đặt trong bất kỳ material slot nào của mesh.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_transparency:

.. rst-class:: classref-property

:ref:`float<class_float>` **transparency** = ``0.0`` :ref:`🔗<class_GeometryInstance3D_property_transparency>`

.. rst-class:: classref-property-setget

- |void| **set_transparency**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_transparency**\ (\ )

Độ trong suốt được áp dụng cho toàn bộ hình học (dưới dạng hệ số nhân với độ trong suốt hiện có của các material). ``0.0`` hoàn toàn không trong suốt, còn ``1.0`` hoàn toàn trong suốt. Các giá trị lớn hơn ``0.0`` (không bao gồm giá trị này) sẽ buộc material của hình học đi qua transparent pipeline, vốn render chậm hơn và có thể phát sinh vấn đề render do sắp xếp độ trong suốt không chính xác. Tuy nhiên, không giống như khi sử dụng material trong suốt, việc đặt :ref:`transparency<class_GeometryInstance3D_property_transparency>` thành giá trị lớn hơn ``0.0`` (không bao gồm giá trị này) *sẽ không* vô hiệu hóa việc render shadow.

Trong các spatial shader, ``1.0 - transparency`` được đặt làm giá trị mặc định của built-in ``ALPHA``.

\ **Lưu ý:** :ref:`transparency<class_GeometryInstance3D_property_transparency>` được giới hạn trong khoảng từ ``0.0`` đến ``1.0``, vì vậy không thể sử dụng thuộc tính này để làm cho material trong suốt trở nên đục hơn mức ban đầu.

\ **Lưu ý:** Chỉ được hỗ trợ khi sử dụng phương thức render Forward+. Khi sử dụng phương thức render Mobile hoặc Compatibility, :ref:`transparency<class_GeometryInstance3D_property_transparency>` sẽ bị bỏ qua và được xem như luôn có giá trị ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_visibility_range_begin:

.. rst-class:: classref-property

:ref:`float<class_float>` **visibility_range_begin** = ``0.0`` :ref:`🔗<class_GeometryInstance3D_property_visibility_range_begin>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_range_begin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_visibility_range_begin**\ (\ )

Khoảng cách bắt đầu từ đó GeometryInstance3D sẽ hiển thị, đồng thời cũng tính đến :ref:`visibility_range_begin_margin<class_GeometryInstance3D_property_visibility_range_begin_margin>`. Giá trị mặc định 0 được sử dụng để tắt kiểm tra phạm vi.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_visibility_range_begin_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **visibility_range_begin_margin** = ``0.0`` :ref:`🔗<class_GeometryInstance3D_property_visibility_range_begin_margin>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_range_begin_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_visibility_range_begin_margin**\ (\ )

Khoảng đệm cho ngưỡng :ref:`visibility_range_begin<class_GeometryInstance3D_property_visibility_range_begin>`. GeometryInstance3D sẽ chỉ thay đổi trạng thái hiển thị khi vượt qua hoặc thấp hơn ngưỡng :ref:`visibility_range_begin<class_GeometryInstance3D_property_visibility_range_begin>` một khoảng bằng giá trị này.

Nếu :ref:`visibility_range_fade_mode<class_GeometryInstance3D_property_visibility_range_fade_mode>` là :ref:`VISIBILITY_RANGE_FADE_DISABLED<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED>`, giá trị này hoạt động như một khoảng cách hysteresis. Nếu :ref:`visibility_range_fade_mode<class_GeometryInstance3D_property_visibility_range_fade_mode>` là :ref:`VISIBILITY_RANGE_FADE_SELF<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_SELF>` hoặc :ref:`VISIBILITY_RANGE_FADE_DEPENDENCIES<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DEPENDENCIES>`, giá trị này hoạt động như một khoảng cách chuyển tiếp fade và phải được đặt thành giá trị lớn hơn ``0.0`` để có thể nhận thấy hiệu ứng.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_visibility_range_end:

.. rst-class:: classref-property

:ref:`float<class_float>` **visibility_range_end** = ``0.0`` :ref:`🔗<class_GeometryInstance3D_property_visibility_range_end>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_range_end**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_visibility_range_end**\ (\ )

Khoảng cách từ đó GeometryInstance3D sẽ bị ẩn, đồng thời cũng tính đến :ref:`visibility_range_end_margin<class_GeometryInstance3D_property_visibility_range_end_margin>`. Giá trị mặc định 0 được sử dụng để tắt kiểm tra phạm vi.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_visibility_range_end_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **visibility_range_end_margin** = ``0.0`` :ref:`🔗<class_GeometryInstance3D_property_visibility_range_end_margin>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_range_end_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_visibility_range_end_margin**\ (\ )

Khoảng đệm cho ngưỡng :ref:`visibility_range_end<class_GeometryInstance3D_property_visibility_range_end>`. GeometryInstance3D sẽ chỉ thay đổi trạng thái hiển thị khi vượt qua hoặc thấp hơn ngưỡng :ref:`visibility_range_end<class_GeometryInstance3D_property_visibility_range_end>` một khoảng bằng giá trị này.

Nếu :ref:`visibility_range_fade_mode<class_GeometryInstance3D_property_visibility_range_fade_mode>` là :ref:`VISIBILITY_RANGE_FADE_DISABLED<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DISABLED>`, giá trị này hoạt động như một khoảng cách hysteresis. Nếu :ref:`visibility_range_fade_mode<class_GeometryInstance3D_property_visibility_range_fade_mode>` là :ref:`VISIBILITY_RANGE_FADE_SELF<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_SELF>` hoặc :ref:`VISIBILITY_RANGE_FADE_DEPENDENCIES<class_GeometryInstance3D_constant_VISIBILITY_RANGE_FADE_DEPENDENCIES>`, giá trị này hoạt động như một khoảng cách chuyển tiếp fade và phải được đặt thành giá trị lớn hơn ``0.0`` để có thể nhận thấy hiệu ứng.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_property_visibility_range_fade_mode:

.. rst-class:: classref-property

:ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>` **visibility_range_fade_mode** = ``0`` :ref:`🔗<class_GeometryInstance3D_property_visibility_range_fade_mode>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_range_fade_mode**\ (\ value\: :ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>`\ ) - :ref:`VisibilityRangeFadeMode<enum_GeometryInstance3D_VisibilityRangeFadeMode>` **get_visibility_range_fade_mode**\ (\ )

Kiểm soát những instance nào sẽ được fade khi tiến gần đến các giới hạn của phạm vi hiển thị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GeometryInstance3D_method_get_instance_shader_parameter:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_instance_shader_parameter**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_GeometryInstance3D_method_get_instance_shader_parameter>`

Lấy giá trị của một shader parameter được đặt trên instance này.

.. rst-class:: classref-item-separator

----

.. _class_GeometryInstance3D_method_set_instance_shader_parameter:

.. rst-class:: classref-method

|void| **set_instance_shader_parameter**\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GeometryInstance3D_method_set_instance_shader_parameter>`

Đặt giá trị của một shader uniform chỉ cho instance này (`per-instance uniform <../tutorials/shaders/shader_reference/shading_language.html#per-instance-uniforms>`__). Xem thêm :ref:`ShaderMaterial.set_shader_parameter()<class_ShaderMaterial_method_set_shader_parameter>` để gán một uniform cho tất cả instance sử dụng cùng :ref:`ShaderMaterial<class_ShaderMaterial>`.

\ **Lưu ý:** Để có thể gán shader uniform theo từng instance, uniform đó *phải* được định nghĩa bằng ``instance uniform ...`` thay vì ``uniform ...`` trong shader code.

\ **Lưu ý:** ``name`` phân biệt chữ hoa chữ thường và phải khớp chính xác với tên của uniform trong code (không phải tên đã viết hoa trong inspector).

\ **Lưu ý:** Shader uniform theo từng instance chỉ khả dụng trong Spatial và CanvasItem shader, không khả dụng cho Fog, Sky hoặc Particles shader.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
