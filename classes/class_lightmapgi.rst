:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LightmapGI.xml.

.. _class_LightmapGI:

LightmapGI
==========

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Tính toán và lưu lightmap đã bake để global illumination hoạt động nhanh hơn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node **LightmapGI** được dùng để tính toán và lưu các lightmap đã bake. Lightmap được dùng để cung cấp indirect lighting chất lượng cao với rất ít hiện tượng rò rỉ ánh sáng. **LightmapGI** cũng có thể cung cấp phản xạ thô bằng spherical harmonics nếu :ref:`directional<class_LightmapGI_property_directional>` được bật. Các đối tượng động có thể nhận indirect lighting nhờ *light probe*, có thể được tự động đặt bằng cách đặt :ref:`generate_probes_subdiv<class_LightmapGI_property_generate_probes_subdiv>` thành giá trị khác :ref:`GENERATE_PROBES_DISABLED<class_LightmapGI_constant_GENERATE_PROBES_DISABLED>`. Bạn cũng có thể thêm các lightmap probe khác bằng cách tạo các node :ref:`LightmapProbe<class_LightmapProbe>`. Nhược điểm là lightmap hoàn toàn tĩnh và không thể được bake trong project đã export. Việc bake node **LightmapGI** cũng chậm hơn so với :ref:`VoxelGI<class_VoxelGI>`.

\ **Tạo theo quy trình:** Chức năng bake lightmap chỉ khả dụng trong editor. Điều này có nghĩa **LightmapGI** không phù hợp với các level được tạo theo quy trình hoặc do người dùng xây dựng. Đối với các level được tạo theo quy trình hoặc do người dùng xây dựng, hãy sử dụng :ref:`VoxelGI<class_VoxelGI>` hoặc SDFGI (xem :ref:`Environment.sdfgi_enabled<class_Environment_property_sdfgi_enabled>`).

\ **Hiệu năng:** **LightmapGI** cung cấp hiệu năng run-time tốt nhất có thể cho global illumination. Nó phù hợp với phần cứng cấp thấp, bao gồm cả đồ họa tích hợp và thiết bị di động.

\ **Lưu ý:** Do cách lightmap hoạt động, hầu hết thuộc tính chỉ có hiệu lực rõ rệt sau khi lightmap được bake lại.

\ **Lưu ý:** Không hỗ trợ bake lightmap trên :ref:`CSGShape3D<class_CSGShape3D>`\ s và :ref:`PrimitiveMesh<class_PrimitiveMesh>`\ es vì các node này không thể lưu dữ liệu UV2 cần thiết cho việc bake.

\ **Lưu ý:** Nếu không cài đặt custom lightmapper nào, **LightmapGI** chỉ có thể được bake từ các thiết bị hỗ trợ renderer Forward+ hoặc Mobile.

\ **Lưu ý:** Node **LightmapGI** chỉ bake dữ liệu ánh sáng cho các node con của node cha. Các node nằm cao hơn trong hệ thống phân cấp của scene sẽ không được bake.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng global illumination của Lightmap <../tutorials/3d/global_illumination/using_lightmap_gi>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                 | :ref:`bias<class_LightmapGI_property_bias>`                                           | ``0.0005``            |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                 | :ref:`bounce_indirect_energy<class_LightmapGI_property_bounce_indirect_energy>`       | ``1.0``               |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                     | :ref:`bounces<class_LightmapGI_property_bounces>`                                     | ``3``                 |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`CameraAttributes<class_CameraAttributes>`           | :ref:`camera_attributes<class_LightmapGI_property_camera_attributes>`                 |                       |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                     | :ref:`denoiser_range<class_LightmapGI_property_denoiser_range>`                       | ``10``                |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                 | :ref:`denoiser_strength<class_LightmapGI_property_denoiser_strength>`                 | ``0.1``               |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`directional<class_LightmapGI_property_directional>`                             | ``false``             |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`                                 | :ref:`environment_custom_color<class_LightmapGI_property_environment_custom_color>`   | ``Color(1, 1, 1, 1)`` |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                 | :ref:`environment_custom_energy<class_LightmapGI_property_environment_custom_energy>` | ``1.0``               |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Sky<class_Sky>`                                     | :ref:`environment_custom_sky<class_LightmapGI_property_environment_custom_sky>`       |                       |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>`   | :ref:`environment_mode<class_LightmapGI_property_environment_mode>`                   | ``1``                 |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>`     | :ref:`generate_probes_subdiv<class_LightmapGI_property_generate_probes_subdiv>`       | ``2``                 |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`interior<class_LightmapGI_property_interior>`                                   | ``false``             |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`LightmapGIData<class_LightmapGIData>`               | :ref:`light_data<class_LightmapGI_property_light_data>`                               |                       |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                     | :ref:`max_texture_size<class_LightmapGI_property_max_texture_size>`                   | ``16384``             |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`BakeQuality<enum_LightmapGI_BakeQuality>`           | :ref:`quality<class_LightmapGI_property_quality>`                                     | ``1``                 |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>` | :ref:`shadowmask_mode<class_LightmapGI_property_shadowmask_mode>`                     | ``0``                 |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`supersampling<class_LightmapGI_property_supersampling>`                         | ``false``             |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                 | :ref:`supersampling_factor<class_LightmapGI_property_supersampling_factor>`           | ``2.0``               |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                 | :ref:`texel_scale<class_LightmapGI_property_texel_scale>`                             | ``1.0``               |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`use_denoiser<class_LightmapGI_property_use_denoiser>`                           | ``true``              |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`use_texture_for_bounces<class_LightmapGI_property_use_texture_for_bounces>`     | ``true``              |
   +-----------------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_LightmapGI_BakeQuality:

.. rst-class:: classref-enumeration

enum **BakeQuality**: :ref:`🔗<enum_LightmapGI_BakeQuality>`

.. _class_LightmapGI_constant_BAKE_QUALITY_LOW:

.. rst-class:: classref-enumeration-constant

:ref:`BakeQuality<enum_LightmapGI_BakeQuality>` **BAKE_QUALITY_LOW** = ``0``

Chất lượng bake thấp (thời gian bake nhanh nhất). Có thể điều chỉnh chất lượng của preset này bằng cách thay đổi :ref:`ProjectSettings.rendering/lightmapping/bake_quality/low_quality_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/low_quality_ray_count>` và :ref:`ProjectSettings.rendering/lightmapping/bake_quality/low_quality_probe_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/low_quality_probe_ray_count>`.

.. _class_LightmapGI_constant_BAKE_QUALITY_MEDIUM:

.. rst-class:: classref-enumeration-constant

:ref:`BakeQuality<enum_LightmapGI_BakeQuality>` **BAKE_QUALITY_MEDIUM** = ``1``

Chất lượng bake trung bình (thời gian bake nhanh). Có thể điều chỉnh chất lượng của preset này bằng cách thay đổi :ref:`ProjectSettings.rendering/lightmapping/bake_quality/medium_quality_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/medium_quality_ray_count>` và :ref:`ProjectSettings.rendering/lightmapping/bake_quality/medium_quality_probe_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/medium_quality_probe_ray_count>`.

.. _class_LightmapGI_constant_BAKE_QUALITY_HIGH:

.. rst-class:: classref-enumeration-constant

:ref:`BakeQuality<enum_LightmapGI_BakeQuality>` **BAKE_QUALITY_HIGH** = ``2``

Chất lượng bake cao (thời gian bake chậm). Có thể điều chỉnh chất lượng của preset này bằng cách thay đổi :ref:`ProjectSettings.rendering/lightmapping/bake_quality/high_quality_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/high_quality_ray_count>` và :ref:`ProjectSettings.rendering/lightmapping/bake_quality/high_quality_probe_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/high_quality_probe_ray_count>`.

.. _class_LightmapGI_constant_BAKE_QUALITY_ULTRA:

.. rst-class:: classref-enumeration-constant

:ref:`BakeQuality<enum_LightmapGI_BakeQuality>` **BAKE_QUALITY_ULTRA** = ``3``

Chất lượng bake cao nhất (thời gian bake chậm nhất). Có thể điều chỉnh chất lượng của preset này bằng cách thay đổi :ref:`ProjectSettings.rendering/lightmapping/bake_quality/ultra_quality_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/ultra_quality_ray_count>` và :ref:`ProjectSettings.rendering/lightmapping/bake_quality/ultra_quality_probe_ray_count<class_ProjectSettings_property_rendering/lightmapping/bake_quality/ultra_quality_probe_ray_count>`.

.. rst-class:: classref-item-separator

----

.. _enum_LightmapGI_GenerateProbes:

.. rst-class:: classref-enumeration

enum **GenerateProbes**: :ref:`🔗<enum_LightmapGI_GenerateProbes>`

.. _class_LightmapGI_constant_GENERATE_PROBES_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **GENERATE_PROBES_DISABLED** = ``0``

Không tạo lightmap probe cho việc chiếu sáng các đối tượng động.

.. _class_LightmapGI_constant_GENERATE_PROBES_SUBDIV_4:

.. rst-class:: classref-enumeration-constant

:ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **GENERATE_PROBES_SUBDIV_4** = ``1``

Mức subdivision thấp nhất (thời gian bake nhanh nhất, kích thước tệp nhỏ nhất).

.. _class_LightmapGI_constant_GENERATE_PROBES_SUBDIV_8:

.. rst-class:: classref-enumeration-constant

:ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **GENERATE_PROBES_SUBDIV_8** = ``2``

Mức subdivision thấp (thời gian bake nhanh, kích thước tệp nhỏ).

.. _class_LightmapGI_constant_GENERATE_PROBES_SUBDIV_16:

.. rst-class:: classref-enumeration-constant

:ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **GENERATE_PROBES_SUBDIV_16** = ``3``

Mức subdivision cao (thời gian bake chậm, kích thước tệp lớn).

.. _class_LightmapGI_constant_GENERATE_PROBES_SUBDIV_32:

.. rst-class:: classref-enumeration-constant

:ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **GENERATE_PROBES_SUBDIV_32** = ``4``

Mức subdivision cao nhất (thời gian bake chậm nhất, kích thước tệp lớn nhất).

.. rst-class:: classref-item-separator

----

.. _enum_LightmapGI_BakeError:

.. rst-class:: classref-enumeration

enum **BakeError**: :ref:`🔗<enum_LightmapGI_BakeError>`

.. _class_LightmapGI_constant_BAKE_ERROR_OK:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_OK** = ``0``

Bake lightmap thành công.

.. _class_LightmapGI_constant_BAKE_ERROR_NO_SCENE_ROOT:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_NO_SCENE_ROOT** = ``1``

Bake lightmap thất bại vì không thể truy cập node gốc của scene đang chỉnh sửa.

.. _class_LightmapGI_constant_BAKE_ERROR_FOREIGN_DATA:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_FOREIGN_DATA** = ``2``

Bake lightmap thất bại vì resource dữ liệu lightmap được nhúng trong một foreign resource.

.. _class_LightmapGI_constant_BAKE_ERROR_NO_LIGHTMAPPER:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_NO_LIGHTMAPPER** = ``3``

Bake lightmap thất bại vì không có lightmapper nào khả dụng trong bản build Godot này.

.. _class_LightmapGI_constant_BAKE_ERROR_NO_SAVE_PATH:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_NO_SAVE_PATH** = ``4``

Bake lightmap thất bại vì đường dẫn lưu :ref:`LightmapGIData<class_LightmapGIData>` chưa được cấu hình trong resource.

.. _class_LightmapGI_constant_BAKE_ERROR_NO_MESHES:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_NO_MESHES** = ``5``

Bake lightmap thất bại vì không có mesh nào có :ref:`GeometryInstance3D.gi_mode<class_GeometryInstance3D_property_gi_mode>` là :ref:`GeometryInstance3D.GI_MODE_STATIC<class_GeometryInstance3D_constant_GI_MODE_STATIC>` và có ánh xạ UV2 hợp lệ trong scene hiện tại. Bạn có thể cần chọn các scene 3D trong Import dock và thay đổi chế độ global illumination tương ứng.

.. _class_LightmapGI_constant_BAKE_ERROR_MESHES_INVALID:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_MESHES_INVALID** = ``6``

Bake lightmap thất bại vì lightmapper không thể phân tích một số mesh được đánh dấu là static để bake.

.. _class_LightmapGI_constant_BAKE_ERROR_CANT_CREATE_IMAGE:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_CANT_CREATE_IMAGE** = ``7``

Bake lightmap thất bại vì image kết quả không thể được lưu hoặc import bởi Godot sau khi lưu.

.. _class_LightmapGI_constant_BAKE_ERROR_USER_ABORTED:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_USER_ABORTED** = ``8``

Người dùng đã hủy thao tác bake lightmap (thường bằng cách nhấp vào nút **Cancel** trong hộp thoại tiến trình).

.. _class_LightmapGI_constant_BAKE_ERROR_TEXTURE_SIZE_TOO_SMALL:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_TEXTURE_SIZE_TOO_SMALL** = ``9``

Bake lightmap thất bại vì kích thước texture tối đa quá nhỏ để chứa một số mesh được đánh dấu để bake.

.. _class_LightmapGI_constant_BAKE_ERROR_LIGHTMAP_TOO_SMALL:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_LIGHTMAP_TOO_SMALL** = ``10``

Bake lightmap thất bại vì lightmap quá nhỏ.

.. _class_LightmapGI_constant_BAKE_ERROR_ATLAS_TOO_SMALL:

.. rst-class:: classref-enumeration-constant

:ref:`BakeError<enum_LightmapGI_BakeError>` **BAKE_ERROR_ATLAS_TOO_SMALL** = ``11``

Bake lightmap thất bại vì lightmap không thể vừa vào một atlas.

.. rst-class:: classref-item-separator

----

.. _enum_LightmapGI_EnvironmentMode:

.. rst-class:: classref-enumeration

enum **EnvironmentMode**: :ref:`🔗<enum_LightmapGI_EnvironmentMode>`

.. _class_LightmapGI_constant_ENVIRONMENT_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>` **ENVIRONMENT_MODE_DISABLED** = ``0``

Bỏ qua lighting của environment khi bake lightmap.

.. _class_LightmapGI_constant_ENVIRONMENT_MODE_SCENE:

.. rst-class:: classref-enumeration-constant

:ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>` **ENVIRONMENT_MODE_SCENE** = ``1``

Sử dụng lighting của environment trong scene khi bake lightmap.

\ **Lưu ý:** Nếu bake lightmap trong một scene không có node :ref:`WorldEnvironment<class_WorldEnvironment>`, tùy chọn này sẽ hoạt động như :ref:`ENVIRONMENT_MODE_DISABLED<class_LightmapGI_constant_ENVIRONMENT_MODE_DISABLED>`. Sky và sun xem trước của editor *không* được **LightmapGI** tính đến khi bake lightmap.

.. _class_LightmapGI_constant_ENVIRONMENT_MODE_CUSTOM_SKY:

.. rst-class:: classref-enumeration-constant

:ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>` **ENVIRONMENT_MODE_CUSTOM_SKY** = ``2``

Sử dụng :ref:`environment_custom_sky<class_LightmapGI_property_environment_custom_sky>` làm nguồn lighting của environment khi bake lightmap.

.. _class_LightmapGI_constant_ENVIRONMENT_MODE_CUSTOM_COLOR:

.. rst-class:: classref-enumeration-constant

:ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>` **ENVIRONMENT_MODE_CUSTOM_COLOR** = ``3``

Sử dụng :ref:`environment_custom_color<class_LightmapGI_property_environment_custom_color>` nhân với :ref:`environment_custom_energy<class_LightmapGI_property_environment_custom_energy>` làm nguồn lighting không đổi của environment khi bake lightmap.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_LightmapGI_property_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **bias** = ``0.0005`` :ref:`🔗<class_LightmapGI_property_bias>`

.. rst-class:: classref-property-setget

- |void| **set_bias**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bias**\ (\ )

Độ bias dùng khi tính toán bóng. Việc tăng :ref:`bias<class_LightmapGI_property_bias>` có thể khắc phục shadow acne trên lightmap đã bake, nhưng có thể gây ra hiện tượng peter-panning (bóng không nối với vật thể tạo bóng). Bóng :ref:`Light3D<class_Light3D>` theo thời gian thực không bị ảnh hưởng bởi thuộc tính :ref:`bias<class_LightmapGI_property_bias>` này.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_bounce_indirect_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **bounce_indirect_energy** = ``1.0`` :ref:`🔗<class_LightmapGI_property_bounce_indirect_energy>`

.. rst-class:: classref-property-setget

- |void| **set_bounce_indirect_energy**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bounce_indirect_energy**\ (\ )

Hệ số năng lượng cho mỗi lần bounce. Giá trị cao hơn sẽ làm indirect lighting sáng hơn. Giá trị ``1.0`` biểu thị hành vi chính xác về mặt vật lý, nhưng có thể dùng giá trị cao hơn để indirect lighting lan truyền rõ hơn khi sử dụng số lần bounce thấp. Có thể dùng cách này để rút ngắn thời gian bake bằng cách giảm số lượng :ref:`bounces<class_LightmapGI_property_bounces>` rồi tăng :ref:`bounce_indirect_energy<class_LightmapGI_property_bounce_indirect_energy>`.

\ **Lưu ý:** :ref:`bounce_indirect_energy<class_LightmapGI_property_bounce_indirect_energy>` chỉ có hiệu lực nếu :ref:`bounces<class_LightmapGI_property_bounces>` được đặt thành giá trị lớn hơn hoặc bằng ``1``.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_bounces:

.. rst-class:: classref-property

:ref:`int<class_int>` **bounces** = ``3`` :ref:`🔗<class_LightmapGI_property_bounces>`

.. rst-class:: classref-property-setget

- |void| **set_bounces**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bounces**\ (\ )

Số lần ánh sáng bounce được tính đến trong quá trình bake. Giá trị cao hơn tạo ra ánh sáng sáng hơn và chân thực hơn, nhưng thời gian bake lâu hơn. Nếu đặt thành ``0``, chỉ environment lighting, direct light và emissive lighting được bake.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_camera_attributes:

.. rst-class:: classref-property

:ref:`CameraAttributes<class_CameraAttributes>` **camera_attributes** :ref:`🔗<class_LightmapGI_property_camera_attributes>`

.. rst-class:: classref-property-setget

- |void| **set_camera_attributes**\ (\ value\: :ref:`CameraAttributes<class_CameraAttributes>`\ ) - :ref:`CameraAttributes<class_CameraAttributes>` **get_camera_attributes**\ (\ )

Tài nguyên :ref:`CameraAttributes<class_CameraAttributes>` chỉ định các mức phơi sáng sẽ được bake. Các thuộc tính tự động phơi sáng và không phơi sáng sẽ bị bỏ qua. Nên sử dụng các thiết lập phơi sáng để giảm dải động hiện có khi bake. Nếu phơi sáng quá cao, **LightmapGI** sẽ xuất hiện hiện tượng banding hoặc các hiện tượng phơi sáng quá mức.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_denoiser_range:

.. rst-class:: classref-property

:ref:`int<class_int>` **denoiser_range** = ``10`` :ref:`🔗<class_LightmapGI_property_denoiser_range>`

.. rst-class:: classref-property-setget

- |void| **set_denoiser_range**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_denoiser_range**\ (\ )

Khoảng cách tính theo pixel mà denoiser sử dụng để lấy mẫu. Giá trị thấp hơn giữ lại nhiều chi tiết hơn, nhưng có thể cho kết quả lốm đốm nếu chất lượng lightmap không đủ cao. Chỉ có hiệu lực khi :ref:`use_denoiser<class_LightmapGI_property_use_denoiser>` là ``true`` và :ref:`ProjectSettings.rendering/lightmapping/denoising/denoiser<class_ProjectSettings_property_rendering/lightmapping/denoising/denoiser>` được đặt thành JNLM.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_denoiser_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **denoiser_strength** = ``0.1`` :ref:`🔗<class_LightmapGI_property_denoiser_strength>`

.. rst-class:: classref-property-setget

- |void| **set_denoiser_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_denoiser_strength**\ (\ )

Mức độ mạnh của bước khử nhiễu được áp dụng cho các lightmap đã tạo. Chỉ có hiệu lực khi :ref:`use_denoiser<class_LightmapGI_property_use_denoiser>` là ``true`` và :ref:`ProjectSettings.rendering/lightmapping/denoising/denoiser<class_ProjectSettings_property_rendering/lightmapping/denoising/denoiser>` được đặt thành JNLM.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_directional:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **directional** = ``false`` :ref:`🔗<class_LightmapGI_property_directional>`

.. rst-class:: classref-property-setget

- |void| **set_directional**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_directional**\ (\ )

Nếu ``true``, bake lightmap để chứa thông tin hướng dưới dạng spherical harmonics. Điều này tạo ra diện mạo chiếu sáng chân thực hơn, đặc biệt với các vật liệu có normal map và các nguồn sáng được bake direct light của chúng (:ref:`Light3D.light_bake_mode<class_Light3D_property_light_bake_mode>` được đặt thành :ref:`Light3D.BAKE_STATIC<class_Light3D_constant_BAKE_STATIC>` và :ref:`Light3D.editor_only<class_Light3D_property_editor_only>` được đặt thành ``false``). Thông tin hướng cũng được sử dụng để cung cấp phản xạ thô cho các đối tượng tĩnh và động. Điều này gây ra một chi phí hiệu năng run-time nhỏ vì shader phải thực hiện nhiều công việc hơn để diễn giải thông tin hướng từ lightmap. Lightmap có hướng cũng mất nhiều thời gian bake hơn và tạo ra kích thước tệp lớn hơn.

\ **Lưu ý:** Tên của thuộc tính không liên quan đến :ref:`DirectionalLight3D<class_DirectionalLight3D>`. :ref:`directional<class_LightmapGI_property_directional>` hoạt động với mọi loại ánh sáng.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_environment_custom_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **environment_custom_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_LightmapGI_property_environment_custom_color>`

.. rst-class:: classref-property-setget

- |void| **set_environment_custom_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_environment_custom_color**\ (\ )

Màu được sử dụng cho chiếu sáng môi trường. Chỉ có hiệu lực khi :ref:`environment_mode<class_LightmapGI_property_environment_mode>` là :ref:`ENVIRONMENT_MODE_CUSTOM_COLOR<class_LightmapGI_constant_ENVIRONMENT_MODE_CUSTOM_COLOR>`.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_environment_custom_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **environment_custom_energy** = ``1.0`` :ref:`🔗<class_LightmapGI_property_environment_custom_energy>`

.. rst-class:: classref-property-setget

- |void| **set_environment_custom_energy**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_environment_custom_energy**\ (\ )

Hệ số nhân màu được sử dụng cho chiếu sáng môi trường. Chỉ có hiệu lực khi :ref:`environment_mode<class_LightmapGI_property_environment_mode>` là :ref:`ENVIRONMENT_MODE_CUSTOM_COLOR<class_LightmapGI_constant_ENVIRONMENT_MODE_CUSTOM_COLOR>`.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_environment_custom_sky:

.. rst-class:: classref-property

:ref:`Sky<class_Sky>` **environment_custom_sky** :ref:`🔗<class_LightmapGI_property_environment_custom_sky>`

.. rst-class:: classref-property-setget

- |void| **set_environment_custom_sky**\ (\ value\: :ref:`Sky<class_Sky>`\ ) - :ref:`Sky<class_Sky>` **get_environment_custom_sky**\ (\ )

Bầu trời được sử dụng làm nguồn chiếu sáng môi trường. Chỉ có hiệu lực khi :ref:`environment_mode<class_LightmapGI_property_environment_mode>` là :ref:`ENVIRONMENT_MODE_CUSTOM_SKY<class_LightmapGI_constant_ENVIRONMENT_MODE_CUSTOM_SKY>`.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_environment_mode:

.. rst-class:: classref-property

:ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>` **environment_mode** = ``1`` :ref:`🔗<class_LightmapGI_property_environment_mode>`

.. rst-class:: classref-property-setget

- |void| **set_environment_mode**\ (\ value\: :ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>`\ ) - :ref:`EnvironmentMode<enum_LightmapGI_EnvironmentMode>` **get_environment_mode**\ (\ )

Chế độ môi trường được sử dụng khi bake lightmap.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_generate_probes_subdiv:

.. rst-class:: classref-property

:ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **generate_probes_subdiv** = ``2`` :ref:`🔗<class_LightmapGI_property_generate_probes_subdiv>`

.. rst-class:: classref-property-setget

- |void| **set_generate_probes**\ (\ value\: :ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>`\ ) - :ref:`GenerateProbes<enum_LightmapGI_GenerateProbes>` **get_generate_probes**\ (\ )

Mức độ subdivision được sử dụng khi tự động tạo các :ref:`LightmapProbe<class_LightmapProbe>`\ s cho việc chiếu sáng đối tượng động. Giá trị cao hơn tạo ra chiếu sáng gián tiếp chính xác hơn trên các đối tượng động, nhưng phải đánh đổi bằng thời gian bake lâu hơn và kích thước tệp lớn hơn.

\ **Lưu ý:** Các :ref:`LightmapProbe<class_LightmapProbe>`\ s được tự động tạo sẽ không hiển thị dưới dạng node trong dock Scene tree và không thể được chỉnh sửa theo cách này sau khi đã tạo.

\ **Lưu ý:** Bất kể :ref:`generate_probes_subdiv<class_LightmapGI_property_generate_probes_subdiv>`, direct lighting trên các đối tượng động luôn được áp dụng bằng các node :ref:`Light3D<class_Light3D>` trong thời gian thực.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_interior:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **interior** = ``false`` :ref:`🔗<class_LightmapGI_property_interior>`

.. rst-class:: classref-property-setget

- |void| **set_interior**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_interior**\ (\ )

Nếu ``true``, bỏ qua chiếu sáng môi trường khi bake lightmap.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_light_data:

.. rst-class:: classref-property

:ref:`LightmapGIData<class_LightmapGIData>` **light_data** :ref:`🔗<class_LightmapGI_property_light_data>`

.. rst-class:: classref-property-setget

- |void| **set_light_data**\ (\ value\: :ref:`LightmapGIData<class_LightmapGIData>`\ ) - :ref:`LightmapGIData<class_LightmapGIData>` **get_light_data**\ (\ )

:ref:`LightmapGIData<class_LightmapGIData>` được liên kết với node **LightmapGI** này. Tài nguyên này được tự động tạo sau khi bake và không предназначен để tạo thủ công.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_max_texture_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_texture_size** = ``16384`` :ref:`🔗<class_LightmapGI_property_max_texture_size>`

.. rst-class:: classref-property-setget

- |void| **set_max_texture_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_texture_size**\ (\ )

Kích thước texture tối đa cho texture atlas được tạo. Giá trị cao hơn sẽ tạo ra ít slice hơn, nhưng có thể không hoạt động trên mọi phần cứng do giới hạn về kích thước texture của phần cứng. Giữ :ref:`max_texture_size<class_LightmapGI_property_max_texture_size>` ở giá trị mặc định là ``16384`` nếu không chắc chắn.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_quality:

.. rst-class:: classref-property

:ref:`BakeQuality<enum_LightmapGI_BakeQuality>` **quality** = ``1`` :ref:`🔗<class_LightmapGI_property_quality>`

.. rst-class:: classref-property-setget

- |void| **set_bake_quality**\ (\ value\: :ref:`BakeQuality<enum_LightmapGI_BakeQuality>`\ ) - :ref:`BakeQuality<enum_LightmapGI_BakeQuality>` **get_bake_quality**\ (\ )

Preset chất lượng được sử dụng khi bake lightmap. Thiết lập này ảnh hưởng đến thời gian bake, nhưng kích thước tệp đầu ra hầu như giống nhau giữa các mức chất lượng.

Để rút ngắn thêm thời gian bake, hãy giảm :ref:`bounces<class_LightmapGI_property_bounces>`, tắt :ref:`use_denoiser<class_LightmapGI_property_use_denoiser>` và/hoặc giảm :ref:`texel_scale<class_LightmapGI_property_texel_scale>`.

Để tăng thêm chất lượng, hãy bật :ref:`supersampling<class_LightmapGI_property_supersampling>` và/hoặc tăng :ref:`texel_scale<class_LightmapGI_property_texel_scale>`.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_shadowmask_mode:

.. rst-class:: classref-property

:ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>` **shadowmask_mode** = ``0`` :ref:`🔗<class_LightmapGI_property_shadowmask_mode>`

.. rst-class:: classref-property-setget

- |void| **set_shadowmask_mode**\ (\ value\: :ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>`\ ) - :ref:`ShadowmaskMode<enum_LightmapGIData_ShadowmaskMode>` **get_shadowmask_mode**\ (\ )

**Thử nghiệm:** Thuộc tính này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

Chính sách shadowmasking được sử dụng cho bóng định hướng trên các đối tượng tĩnh được bake bằng instance **LightmapGI** này.

Shadowmasking cho phép các node :ref:`DirectionalLight3D<class_DirectionalLight3D>` đổ bóng ngay cả bên ngoài phạm vi được xác định bởi thuộc tính :ref:`DirectionalLight3D.directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>` của chúng. Điều này được thực hiện bằng cách bake một texture chứa shadowmap cho ánh sáng định hướng, sau đó sử dụng texture này theo chế độ shadowmask hiện tại.

\ **Lưu ý:** Texture shadowmask chỉ được tạo nếu :ref:`shadowmask_mode<class_LightmapGI_property_shadowmask_mode>` không phải là :ref:`LightmapGIData.SHADOWMASK_MODE_NONE<class_LightmapGIData_constant_SHADOWMASK_MODE_NONE>`. Để thấy sự khác biệt, bạn cần bake lại lightmap sau khi chuyển từ :ref:`LightmapGIData.SHADOWMASK_MODE_NONE<class_LightmapGIData_constant_SHADOWMASK_MODE_NONE>` sang bất kỳ chế độ nào khác.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_supersampling:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **supersampling** = ``false`` :ref:`🔗<class_LightmapGI_property_supersampling>`

.. rst-class:: classref-property-setget

- |void| **set_supersampling_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_supersampling_enabled**\ (\ )

Nếu ``true``, lightmap được bake với texel scale được nhân với :ref:`supersampling_factor<class_LightmapGI_property_supersampling_factor>` và downsample trước khi lưu lightmap (do đó mật độ texel hiệu dụng giống hệt như khi tắt supersampling).

Supersampling cung cấp chất lượng lightmap cao hơn với ít nhiễu hơn, bóng mượt hơn và khả năng đổ bóng tốt hơn cho các chi tiết quy mô nhỏ trên đối tượng. Tuy nhiên, nó có thể làm tăng đáng kể thời gian bake và mức sử dụng bộ nhớ trong khi bake lightmap. Padding được tự động điều chỉnh để tránh làm tăng hiện tượng light leaking.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_supersampling_factor:

.. rst-class:: classref-property

:ref:`float<class_float>` **supersampling_factor** = ``2.0`` :ref:`🔗<class_LightmapGI_property_supersampling_factor>`

.. rst-class:: classref-property-setget

- |void| **set_supersampling_factor**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_supersampling_factor**\ (\ )

Hệ số nhân mật độ texel khi supersampling. Để có kết quả tốt nhất, hãy sử dụng giá trị nguyên. Mặc dù cho phép sử dụng giá trị phân số, chúng có thể làm tăng hiện tượng light leaking và khiến lightmap bị mờ.

Giá trị cao hơn có thể tạo ra chất lượng tốt hơn, nhưng cũng làm tăng thời gian bake và mức sử dụng bộ nhớ trong khi bake.

Xem :ref:`supersampling<class_LightmapGI_property_supersampling>` để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_texel_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **texel_scale** = ``1.0`` :ref:`🔗<class_LightmapGI_property_texel_scale>`

.. rst-class:: classref-property-setget

- |void| **set_texel_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_texel_scale**\ (\ )

Điều chỉnh mật độ texel của lightmap cho tất cả mesh trong lần bake hiện tại. Đây là một hệ số nhân được áp dụng trên kích thước texel lightmap hiện có được xác định trong từng scene 3D đã import, cùng với hệ số nhân mật độ theo từng mesh (được thiết kế để sử dụng khi cùng một mesh được dùng ở các tỷ lệ khác nhau). Giá trị thấp hơn sẽ giúp thời gian bake nhanh hơn.

Ví dụ, tăng gấp đôi :ref:`texel_scale<class_LightmapGI_property_texel_scale>` sẽ tăng gấp đôi độ phân giải texture lightmap cho tất cả đối tượng *trên mỗi trục*, vì vậy sẽ *tăng gấp bốn lần* số lượng texel.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_use_denoiser:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_denoiser** = ``true`` :ref:`🔗<class_LightmapGI_property_use_denoiser>`

.. rst-class:: classref-property-setget

- |void| **set_use_denoiser**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_denoiser**\ (\ )

Nếu ``true``, sử dụng thuật toán khử nhiễu dựa trên GPU cho lightmap được tạo. Thao tác này loại bỏ hầu hết nhiễu trong lightmap được tạo, nhưng phải đánh đổi bằng thời gian bake lâu hơn. Kích thước tệp nhìn chung không bị ảnh hưởng đáng kể khi sử dụng denoiser, mặc dù tính năng nén không mất dữ liệu có thể nén hình ảnh đã khử nhiễu tốt hơn.

.. rst-class:: classref-item-separator

----

.. _class_LightmapGI_property_use_texture_for_bounces:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_texture_for_bounces** = ``true`` :ref:`🔗<class_LightmapGI_property_use_texture_for_bounces>`

.. rst-class:: classref-property-setget

- |void| **set_use_texture_for_bounces**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_texture_for_bounces**\ (\ )

Nếu ``true``, một texture chứa thông tin chiếu sáng sẽ được tạo để tăng tốc quá trình tạo ánh sáng gián tiếp, nhưng phải đánh đổi bằng một phần độ chính xác. Hình học có thể xuất hiện thêm các hiện tượng rò rỉ ánh sáng khi sử dụng lightmap có độ phân giải thấp hoặc UV kéo giãn lightmap đáng kể trên các bề mặt. Nếu không chắc chắn, hãy giữ :ref:`use_texture_for_bounces<class_LightmapGI_property_use_texture_for_bounces>` ở giá trị mặc định là ``true``.

\ **Lưu ý:** :ref:`use_texture_for_bounces<class_LightmapGI_property_use_texture_for_bounces>` chỉ có hiệu lực nếu :ref:`bounces<class_LightmapGI_property_bounces>` được đặt thành giá trị lớn hơn hoặc bằng ``1``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
