:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Light3D.xml.

.. _class_Light3D:

Light3D
=======

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AreaLight3D<class_AreaLight3D>`, :ref:`DirectionalLight3D<class_DirectionalLight3D>`, :ref:`OmniLight3D<class_OmniLight3D>`, :ref:`SpotLight3D<class_SpotLight3D>`

Cung cấp lớp cơ sở cho các loại light node khác nhau.

.. rst-class:: classref-introduction-group

Mô tả
-----

Light3D là lớp cơ sở *trừu tượng* cho các light node. Vì không thể được khởi tạo, lớp này không nên được sử dụng trực tiếp. Các loại light node khác kế thừa từ lớp này. Light3D chứa các biến và tham số chung được sử dụng cho việc chiếu sáng.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Đèn và bóng 3D <../tutorials/3d/lights_and_shadows>`

- :doc:`Giả lập global illumination <../tutorials/3d/global_illumination/faking_global_illumination>`

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`distance_fade_begin<class_Light3D_property_distance_fade_begin>`                 | ``40.0``              |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                | :ref:`distance_fade_enabled<class_Light3D_property_distance_fade_enabled>`             | ``false``             |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`distance_fade_length<class_Light3D_property_distance_fade_length>`               | ``10.0``              |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`distance_fade_shadow<class_Light3D_property_distance_fade_shadow>`               | ``50.0``              |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                | :ref:`editor_only<class_Light3D_property_editor_only>`                                 | ``false``             |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_angular_distance<class_Light3D_property_light_angular_distance>`           | ``0.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`BakeMode<enum_Light3D_BakeMode>` | :ref:`light_bake_mode<class_Light3D_property_light_bake_mode>`                         | ``2``                 |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`              | :ref:`light_color<class_Light3D_property_light_color>`                                 | ``Color(1, 1, 1, 1)`` |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                  | :ref:`light_cull_mask<class_Light3D_property_light_cull_mask>`                         | ``4294967295``        |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_energy<class_Light3D_property_light_energy>`                               | ``1.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_indirect_energy<class_Light3D_property_light_indirect_energy>`             | ``1.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_intensity_lumens<class_Light3D_property_light_intensity_lumens>`           |                       |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_intensity_lux<class_Light3D_property_light_intensity_lux>`                 |                       |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                | :ref:`light_negative<class_Light3D_property_light_negative>`                           | ``false``             |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Texture2D<class_Texture2D>`      | :ref:`light_projector<class_Light3D_property_light_projector>`                         |                       |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_size<class_Light3D_property_light_size>`                                   | ``0.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_specular<class_Light3D_property_light_specular>`                           | ``1.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_temperature<class_Light3D_property_light_temperature>`                     |                       |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`light_volumetric_fog_energy<class_Light3D_property_light_volumetric_fog_energy>` | ``1.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`shadow_bias<class_Light3D_property_shadow_bias>`                                 | ``0.1``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`shadow_blur<class_Light3D_property_shadow_blur>`                                 | ``1.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                  | :ref:`shadow_caster_mask<class_Light3D_property_shadow_caster_mask>`                   | ``4294967295``        |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                | :ref:`shadow_enabled<class_Light3D_property_shadow_enabled>`                           | ``false``             |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`shadow_normal_bias<class_Light3D_property_shadow_normal_bias>`                   | ``2.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`shadow_opacity<class_Light3D_property_shadow_opacity>`                           | ``1.0``               |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                | :ref:`shadow_reverse_cull_face<class_Light3D_property_shadow_reverse_cull_face>`       | ``false``             |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`              | :ref:`shadow_transmittance_bias<class_Light3D_property_shadow_transmittance_bias>`     | ``0.05``              |
   +----------------------------------------+----------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>` | :ref:`get_correlated_color<class_Light3D_method_get_correlated_color>`\ (\ ) |const|                                                |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param<class_Light3D_method_get_param>`\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|                            |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param<class_Light3D_method_set_param>`\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_Light3D_Param:

.. rst-class:: classref-enumeration

enum **Param**: :ref:`🔗<enum_Light3D_Param>`

.. _class_Light3D_constant_PARAM_ENERGY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_ENERGY** = ``0``

Hằng số để truy cập :ref:`light_energy<class_Light3D_property_light_energy>`.

.. _class_Light3D_constant_PARAM_INDIRECT_ENERGY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_INDIRECT_ENERGY** = ``1``

Hằng số để truy cập :ref:`light_indirect_energy<class_Light3D_property_light_indirect_energy>`.

.. _class_Light3D_constant_PARAM_VOLUMETRIC_FOG_ENERGY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_VOLUMETRIC_FOG_ENERGY** = ``2``

Hằng số để truy cập :ref:`light_volumetric_fog_energy<class_Light3D_property_light_volumetric_fog_energy>`.

.. _class_Light3D_constant_PARAM_SPECULAR:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SPECULAR** = ``3``

Hằng số để truy cập :ref:`light_specular<class_Light3D_property_light_specular>`.

.. _class_Light3D_constant_PARAM_RANGE:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_RANGE** = ``4``

Hằng số để truy cập :ref:`OmniLight3D.omni_range<class_OmniLight3D_property_omni_range>` hoặc :ref:`SpotLight3D.spot_range<class_SpotLight3D_property_spot_range>`.

.. _class_Light3D_constant_PARAM_SIZE:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SIZE** = ``5``

Hằng số để truy cập :ref:`light_size<class_Light3D_property_light_size>`.

.. _class_Light3D_constant_PARAM_ATTENUATION:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_ATTENUATION** = ``6``

Hằng số để truy cập :ref:`OmniLight3D.omni_attenuation<class_OmniLight3D_property_omni_attenuation>` hoặc :ref:`SpotLight3D.spot_attenuation<class_SpotLight3D_property_spot_attenuation>`.

.. _class_Light3D_constant_PARAM_SPOT_ANGLE:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SPOT_ANGLE** = ``7``

Hằng số để truy cập :ref:`SpotLight3D.spot_angle<class_SpotLight3D_property_spot_angle>`.

.. _class_Light3D_constant_PARAM_SPOT_ATTENUATION:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SPOT_ATTENUATION** = ``8``

Hằng số để truy cập :ref:`SpotLight3D.spot_angle_attenuation<class_SpotLight3D_property_spot_angle_attenuation>`.

.. _class_Light3D_constant_PARAM_SHADOW_MAX_DISTANCE:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_MAX_DISTANCE** = ``9``

Hằng số để truy cập :ref:`DirectionalLight3D.directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>`.

.. _class_Light3D_constant_PARAM_SHADOW_SPLIT_1_OFFSET:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_SPLIT_1_OFFSET** = ``10``

Hằng số để truy cập :ref:`DirectionalLight3D.directional_shadow_split_1<class_DirectionalLight3D_property_directional_shadow_split_1>`.

.. _class_Light3D_constant_PARAM_SHADOW_SPLIT_2_OFFSET:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_SPLIT_2_OFFSET** = ``11``

Hằng số để truy cập :ref:`DirectionalLight3D.directional_shadow_split_2<class_DirectionalLight3D_property_directional_shadow_split_2>`.

.. _class_Light3D_constant_PARAM_SHADOW_SPLIT_3_OFFSET:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_SPLIT_3_OFFSET** = ``12``

Hằng số để truy cập :ref:`DirectionalLight3D.directional_shadow_split_3<class_DirectionalLight3D_property_directional_shadow_split_3>`.

.. _class_Light3D_constant_PARAM_SHADOW_FADE_START:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_FADE_START** = ``13``

Hằng số để truy cập :ref:`DirectionalLight3D.directional_shadow_fade_start<class_DirectionalLight3D_property_directional_shadow_fade_start>`.

.. _class_Light3D_constant_PARAM_SHADOW_NORMAL_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_NORMAL_BIAS** = ``14``

Hằng số để truy cập :ref:`shadow_normal_bias<class_Light3D_property_shadow_normal_bias>`.

.. _class_Light3D_constant_PARAM_SHADOW_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_BIAS** = ``15``

Hằng số để truy cập :ref:`shadow_bias<class_Light3D_property_shadow_bias>`.

.. _class_Light3D_constant_PARAM_SHADOW_PANCAKE_SIZE:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_PANCAKE_SIZE** = ``16``

Hằng số để truy cập :ref:`DirectionalLight3D.directional_shadow_pancake_size<class_DirectionalLight3D_property_directional_shadow_pancake_size>`.

.. _class_Light3D_constant_PARAM_SHADOW_OPACITY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_OPACITY** = ``17``

Hằng số để truy cập :ref:`shadow_opacity<class_Light3D_property_shadow_opacity>`.

.. _class_Light3D_constant_PARAM_SHADOW_BLUR:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_SHADOW_BLUR** = ``18``

Hằng số để truy cập :ref:`shadow_blur<class_Light3D_property_shadow_blur>`.

.. _class_Light3D_constant_PARAM_TRANSMITTANCE_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_TRANSMITTANCE_BIAS** = ``19``

Hằng số để truy cập :ref:`shadow_transmittance_bias<class_Light3D_property_shadow_transmittance_bias>`.

.. _class_Light3D_constant_PARAM_INTENSITY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_INTENSITY** = ``20``

Hằng số để truy cập :ref:`light_intensity_lumens<class_Light3D_property_light_intensity_lumens>` và :ref:`light_intensity_lux<class_Light3D_property_light_intensity_lux>`. Chỉ được sử dụng khi :ref:`ProjectSettings.rendering/lights_and_shadows/use_physical_light_units<class_ProjectSettings_property_rendering/lights_and_shadows/use_physical_light_units>` là ``true``.

.. _class_Light3D_constant_PARAM_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_Light3D_Param>` **PARAM_MAX** = ``21``

Đại diện cho kích thước của enum :ref:`Param<enum_Light3D_Param>`.

.. rst-class:: classref-item-separator

----

.. _enum_Light3D_BakeMode:

.. rst-class:: classref-enumeration

enum **BakeMode**: :ref:`🔗<enum_Light3D_BakeMode>`

.. _class_Light3D_constant_BAKE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`BakeMode<enum_Light3D_BakeMode>` **BAKE_DISABLED** = ``0``

Light bị bỏ qua khi baking. Đây là chế độ nhanh nhất, nhưng light sẽ không được tính đến khi baking global illumination. Chế độ này nhìn chung nên được sử dụng cho các light động thay đổi nhanh, vì hiệu ứng global illumination ít đáng chú ý hơn trên những light đó.

\ **Lưu ý:** Việc ẩn một light *không* ảnh hưởng đến baking :ref:`LightmapGI<class_LightmapGI>`. Việc ẩn một light vẫn ảnh hưởng đến baking :ref:`VoxelGI<class_VoxelGI>` và SDFGI (xem :ref:`Environment.sdfgi_enabled<class_Environment_property_sdfgi_enabled>`).

.. _class_Light3D_constant_BAKE_STATIC:

.. rst-class:: classref-enumeration-constant

:ref:`BakeMode<enum_Light3D_BakeMode>` **BAKE_STATIC** = ``1``

Light được tính đến trong static baking (:ref:`VoxelGI<class_VoxelGI>`, :ref:`LightmapGI<class_LightmapGI>`, SDFGI (:ref:`Environment.sdfgi_enabled<class_Environment_property_sdfgi_enabled>`)). Light có thể được di chuyển hoặc sửa đổi, nhưng global illumination của nó sẽ không được cập nhật theo thời gian thực. Điều này phù hợp với các thay đổi nhỏ (chẳng hạn như đuốc chập chờn), nhưng nhìn chung không phù hợp với các thay đổi lớn như bật hoặc tắt light.

\ **Lưu ý:** Light không được bake trong :ref:`LightmapGI<class_LightmapGI>` nếu :ref:`editor_only<class_Light3D_property_editor_only>` là ``true``.

.. _class_Light3D_constant_BAKE_DYNAMIC:

.. rst-class:: classref-enumeration-constant

:ref:`BakeMode<enum_Light3D_BakeMode>` **BAKE_DYNAMIC** = ``2``

Light được tính đến trong dynamic baking (chỉ :ref:`VoxelGI<class_VoxelGI>` và SDFGI (:ref:`Environment.sdfgi_enabled<class_Environment_property_sdfgi_enabled>`)). Light có thể được di chuyển hoặc sửa đổi, đồng thời global illumination được cập nhật theo thời gian thực. Hình thức global illumination của light sẽ hơi khác so với :ref:`BAKE_STATIC<class_Light3D_constant_BAKE_STATIC>`. Chế độ này có chi phí hiệu năng cao hơn so với :ref:`BAKE_STATIC<class_Light3D_constant_BAKE_STATIC>`. Khi sử dụng SDFGI, tốc độ cập nhật của các light động bị ảnh hưởng bởi :ref:`ProjectSettings.rendering/global_illumination/sdfgi/frames_to_update_lights<class_ProjectSettings_property_rendering/global_illumination/sdfgi/frames_to_update_lights>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Light3D_property_distance_fade_begin:

.. rst-class:: classref-property

:ref:`float<class_float>` **distance_fade_begin** = ``40.0`` :ref:`🔗<class_Light3D_property_distance_fade_begin>`

.. rst-class:: classref-property-setget

- |void| **set_distance_fade_begin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_distance_fade_begin**\ (\ )

Khoảng cách tính từ camera mà tại đó light bắt đầu mờ dần (tính theo đơn vị 3D).

\ **Lưu ý:** Chỉ có hiệu lực đối với :ref:`OmniLight3D<class_OmniLight3D>` và :ref:`SpotLight3D<class_SpotLight3D>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_distance_fade_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **distance_fade_enabled** = ``false`` :ref:`🔗<class_Light3D_property_distance_fade_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enable_distance_fade**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_distance_fade_enabled**\ (\ )

Nếu ``true``, light sẽ mờ dần một cách mượt mà khi ở xa :ref:`Camera3D<class_Camera3D>` đang hoạt động, bắt đầu từ :ref:`distance_fade_begin<class_Light3D_property_distance_fade_begin>`. Đây là một dạng level of detail (LOD). Light sẽ mờ dần trong khoảng :ref:`distance_fade_begin<class_Light3D_property_distance_fade_begin>` + :ref:`distance_fade_length<class_Light3D_property_distance_fade_length>`, sau đó sẽ bị culling và hoàn toàn không được gửi đến shader. Hãy sử dụng tùy chọn này để giảm số lượng light đang hoạt động trong scene và từ đó cải thiện hiệu năng.

\ **Lưu ý:** Chỉ có hiệu lực đối với :ref:`OmniLight3D<class_OmniLight3D>` và :ref:`SpotLight3D<class_SpotLight3D>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_distance_fade_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **distance_fade_length** = ``10.0`` :ref:`🔗<class_Light3D_property_distance_fade_length>`

.. rst-class:: classref-property-setget

- |void| **set_distance_fade_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_distance_fade_length**\ (\ )

Khoảng cách mà light và bóng của nó mờ dần. Năng lượng của light và độ mờ của bóng sẽ giảm dần trong khoảng cách này, rồi hoàn toàn không còn nhìn thấy ở cuối khoảng cách.

\ **Lưu ý:** Chỉ có hiệu lực đối với :ref:`OmniLight3D<class_OmniLight3D>` và :ref:`SpotLight3D<class_SpotLight3D>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_distance_fade_shadow:

.. rst-class:: classref-property

:ref:`float<class_float>` **distance_fade_shadow** = ``50.0`` :ref:`🔗<class_Light3D_property_distance_fade_shadow>`

.. rst-class:: classref-property-setget

- |void| **set_distance_fade_shadow**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_distance_fade_shadow**\ (\ )

Khoảng cách tính từ camera mà tại đó bóng của light bị cắt (tính theo đơn vị 3D). Đặt giá trị này thấp hơn :ref:`distance_fade_begin<class_Light3D_property_distance_fade_begin>` + :ref:`distance_fade_length<class_Light3D_property_distance_fade_length>` để cải thiện hiệu năng hơn nữa, vì việc render bóng thường tốn nhiều chi phí hơn chính việc render light.

\ **Lưu ý:** Chỉ có hiệu lực đối với :ref:`OmniLight3D<class_OmniLight3D>` và :ref:`SpotLight3D<class_SpotLight3D>`, và chỉ khi :ref:`shadow_enabled<class_Light3D_property_shadow_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_editor_only:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editor_only** = ``false`` :ref:`🔗<class_Light3D_property_editor_only>`

.. rst-class:: classref-property-setget

- |void| **set_editor_only**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_editor_only**\ (\ )

Nếu ``true``, light chỉ xuất hiện trong editor và sẽ không hiển thị khi runtime. Nếu ``true``, light sẽ không bao giờ được bake trong :ref:`LightmapGI<class_LightmapGI>` bất kể :ref:`light_bake_mode<class_Light3D_property_light_bake_mode>` của nó.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_angular_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_angular_distance** = ``0.0`` :ref:`🔗<class_Light3D_property_light_angular_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Kích thước góc của light tính theo độ. Việc tăng giá trị này sẽ làm bóng mềm hơn ở khoảng cách lớn (còn gọi là percentage-closer soft shadows, hay PCSS). Chỉ khả dụng cho :ref:`DirectionalLight3D<class_DirectionalLight3D>`\ s. Để tham khảo, Mặt Trời nhìn từ Trái Đất có kích thước xấp xỉ ``0.5``. Việc tăng giá trị này vượt quá ``0.0`` đối với các light bật bóng sẽ gây ảnh hưởng đáng kể đến hiệu năng do PCSS.

\ **Lưu ý:** :ref:`light_angular_distance<class_Light3D_property_light_angular_distance>` không bị ảnh hưởng bởi :ref:`Node3D.scale<class_Node3D_property_scale>` (scale của light hoặc scale của parent).

\ **Lưu ý:** PCSS cho đèn định hướng chỉ được hỗ trợ trong phương thức kết xuất Forward+, không được hỗ trợ trong Mobile hoặc Compatibility.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_bake_mode:

.. rst-class:: classref-property

:ref:`BakeMode<enum_Light3D_BakeMode>` **light_bake_mode** = ``2`` :ref:`🔗<class_Light3D_property_light_bake_mode>`

.. rst-class:: classref-property-setget

- |void| **set_bake_mode**\ (\ value\: :ref:`BakeMode<enum_Light3D_BakeMode>`\ ) - :ref:`BakeMode<enum_Light3D_BakeMode>` **get_bake_mode**\ (\ )

Chế độ bake của đèn. Chế độ này sẽ ảnh hưởng đến các kỹ thuật global illumination tác động đến quá trình kết xuất đèn.

\ **Lưu ý:** Chế độ global illumination của mesh cũng sẽ ảnh hưởng đến quá trình kết xuất global illumination. Xem :ref:`GeometryInstance3D.gi_mode<class_GeometryInstance3D_property_gi_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **light_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_Light3D_property_light_color>`

.. rst-class:: classref-property-setget

- |void| **set_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_color**\ (\ )

Màu của đèn ở dạng mã hóa sRGB phi tuyến. Có thể sử dụng màu *overbright* để đạt được kết quả tương đương với việc tăng :ref:`light_energy<class_Light3D_property_light_energy>` của đèn.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **light_cull_mask** = ``4294967295`` :ref:`🔗<class_Light3D_property_light_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_cull_mask**\ (\ )

Đèn sẽ tác động đến các đối tượng trong những layer đã chọn.

\ **Lưu ý:** Light cull mask bị :ref:`VoxelGI<class_VoxelGI>`, SDFGI, :ref:`LightmapGI<class_LightmapGI>` và volumetric fog bỏ qua. Các thành phần này luôn kết xuất đèn theo cách bỏ qua cull mask. Xem thêm :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_energy** = ``1.0`` :ref:`🔗<class_Light3D_property_light_energy>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Hệ số nhân cường độ của đèn (đây không phải là một đơn vị vật lý). Đối với :ref:`OmniLight3D<class_OmniLight3D>` và :ref:`SpotLight3D<class_SpotLight3D>`, việc thay đổi giá trị này chỉ thay đổi cường độ màu của đèn, không thay đổi bán kính của đèn.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_indirect_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_indirect_energy** = ``1.0`` :ref:`🔗<class_Light3D_property_light_indirect_energy>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Hệ số nhân thứ cấp được sử dụng với indirect light (ánh sáng dội). Được sử dụng với :ref:`VoxelGI<class_VoxelGI>` và SDFGI (xem :ref:`Environment.sdfgi_enabled<class_Environment_property_sdfgi_enabled>`).

\ **Lưu ý:** Thuộc tính này bị bỏ qua nếu :ref:`light_energy<class_Light3D_property_light_energy>` bằng ``0.0``, vì khi đó đèn hoàn toàn không xuất hiện trong GI shader.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_intensity_lumens:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_intensity_lumens** :ref:`🔗<class_Light3D_property_light_intensity_lumens>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Được sử dụng bởi các đèn vị trí (:ref:`OmniLight3D<class_OmniLight3D>` và :ref:`SpotLight3D<class_SpotLight3D>`) khi :ref:`ProjectSettings.rendering/lights_and_shadows/use_physical_light_units<class_ProjectSettings_property_rendering/lights_and_shadows/use_physical_light_units>` là ``true``. Thiết lập cường độ của nguồn sáng, được đo bằng Lumen. Lumen là đơn vị đo quang thông, tức tổng lượng ánh sáng nhìn thấy được phát ra từ một nguồn sáng trong một đơn vị thời gian.

Đối với :ref:`SpotLight3D<class_SpotLight3D>`\ s, giả định rằng khu vực bên ngoài hình nón nhìn thấy được bao quanh bởi một vật liệu hấp thụ ánh sáng hoàn hảo. Theo đó, độ sáng biểu kiến của vùng hình nón không thay đổi khi hình nón tăng hoặc giảm kích thước.

Một bóng đèn gia dụng thông thường có thể có cường độ từ khoảng 600 lumen đến 1.200 lumen, một cây nến khoảng 13 lumen, trong khi đèn đường có thể đạt khoảng 60.000 lumen.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_intensity_lux:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_intensity_lux** :ref:`🔗<class_Light3D_property_light_intensity_lux>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Được sử dụng bởi :ref:`DirectionalLight3D<class_DirectionalLight3D>`\ s khi :ref:`ProjectSettings.rendering/lights_and_shadows/use_physical_light_units<class_ProjectSettings_property_rendering/lights_and_shadows/use_physical_light_units>` là ``true``. Thiết lập cường độ của nguồn sáng, được đo bằng Lux. Lux là đơn vị đo quang thông trên một đơn vị diện tích, bằng một lumen trên mỗi mét vuông. Lux đo lượng ánh sáng chiếu lên một bề mặt tại một thời điểm nhất định.

Vào một ngày nắng quang mây, một bề mặt trực tiếp dưới ánh nắng có thể đạt khoảng 100.000 lux, một căn phòng thông thường trong nhà có thể đạt khoảng 50 lux, trong khi mặt đất dưới ánh trăng có thể đạt khoảng 0,1 lux.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_negative:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **light_negative** = ``false`` :ref:`🔗<class_Light3D_property_light_negative>`

.. rst-class:: classref-property-setget

- |void| **set_negative**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_negative**\ (\ )

Nếu ``true``, hiệu ứng của đèn sẽ bị đảo ngược, làm tối các khu vực và tạo ra các bóng sáng.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_projector:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **light_projector** :ref:`🔗<class_Light3D_property_light_projector>`

.. rst-class:: classref-property-setget

- |void| **set_projector**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_projector**\ (\ )

:ref:`Texture2D<class_Texture2D>` được đèn chiếu lên. :ref:`shadow_enabled<class_Light3D_property_shadow_enabled>` phải được bật để projector hoạt động. Light projector khiến ánh sáng trông như đang chiếu xuyên qua một vật thể có màu nhưng trong suốt, gần giống ánh sáng chiếu qua kính màu.

\ **Lưu ý:** Không giống :ref:`BaseMaterial3D<class_BaseMaterial3D>`, trong đó filter mode có thể được điều chỉnh theo từng material, filter mode cho texture của light projector được thiết lập toàn cục bằng :ref:`ProjectSettings.rendering/textures/light_projectors/filter<class_ProjectSettings_property_rendering/textures/light_projectors/filter>`.

\ **Lưu ý:** Texture của light projector chỉ được hỗ trợ trong các phương thức kết xuất Forward+ và Mobile, không được hỗ trợ trong Compatibility.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_size** = ``0.0`` :ref:`🔗<class_Light3D_property_light_size>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Kích thước mô phỏng của đèn theo đơn vị Godot, ảnh hưởng đến shading và shadow. Đối với :ref:`OmniLight3D<class_OmniLight3D>`\ s và :ref:`SpotLight3D<class_SpotLight3D>`\ s, việc tăng giá trị này mô phỏng một đèn vùng hình cầu, mở rộng kích thước của các vùng highlight specular. Nếu bật shadow, penumbra sẽ được kết xuất, khiến bóng trông mờ hơn. Đối với :ref:`AreaLight3D<class_AreaLight3D>`\ s, chỉ shadow bị ảnh hưởng. Penumbra được mô phỏng bằng percentage-closer soft shadows, hay PCSS, gây ảnh hưởng đáng kể đến hiệu năng khi giá trị lớn hơn ``0.0``.

\ **Lưu ý:** :ref:`light_size<class_Light3D_property_light_size>` không bị ảnh hưởng bởi :ref:`Node3D.scale<class_Node3D_property_scale>` (scale của đèn hoặc scale của parent của đèn).

\ **Lưu ý:** PCSS cho đèn vị trí chỉ được hỗ trợ trong các phương thức kết xuất Forward+ và Mobile, không được hỗ trợ trong Compatibility.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_specular:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_specular** = ``1.0`` :ref:`🔗<class_Light3D_property_light_specular>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Cường độ của vùng specular trên các đối tượng chịu tác động của đèn. Ở ``0``, đèn trở thành đèn diffuse thuần túy. Khi không bake emission, thuộc tính này có thể được dùng để tránh các phản xạ không thực tế khi đặt đèn phía trên một bề mặt phát sáng.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_temperature:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_temperature** :ref:`🔗<class_Light3D_property_light_temperature>`

.. rst-class:: classref-property-setget

- |void| **set_temperature**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_temperature**\ (\ )

Thiết lập nhiệt độ màu của nguồn sáng, được đo bằng Kelvin. Giá trị này được dùng để tính nhiệt độ màu tương quan, từ đó nhuộm màu :ref:`light_color<class_Light3D_property_light_color>`.

Mặt trời vào ngày nhiều mây có nhiệt độ khoảng 6500 Kelvin, vào ngày quang mây là từ 5500 đến 6000 Kelvin, còn vào lúc bình minh hoặc hoàng hôn của một ngày quang mây thì vào khoảng 1850 Kelvin.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_light_volumetric_fog_energy:

.. rst-class:: classref-property

:ref:`float<class_float>` **light_volumetric_fog_energy** = ``1.0`` :ref:`🔗<class_Light3D_property_light_volumetric_fog_energy>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Hệ số nhân thứ cấp được nhân với :ref:`light_energy<class_Light3D_property_light_energy>`, sau đó được sử dụng với volumetric fog của :ref:`Environment<class_Environment>` (nếu được bật). Nếu đặt thành ``0.0``, quá trình tính volumetric fog sẽ được bỏ qua đối với đèn này, giúp cải thiện hiệu năng khi có số lượng lớn đèn và volumetric fog được bật.

\ **Lưu ý:** Để ngăn các hiệu ứng đèn động có thời gian tồn tại ngắn tương tác kém với volumetric fog, các đèn được sử dụng trong những hiệu ứng đó nên đặt :ref:`light_volumetric_fog_energy<class_Light3D_property_light_volumetric_fog_energy>` thành ``0.0``, trừ khi :ref:`Environment.volumetric_fog_temporal_reprojection_enabled<class_Environment_property_volumetric_fog_temporal_reprojection_enabled>` bị tắt (hoặc khi giảm đáng kể mức reprojection).

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **shadow_bias** = ``0.1`` :ref:`🔗<class_Light3D_property_shadow_bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Được sử dụng để điều chỉnh diện mạo của shadow. Giá trị quá nhỏ sẽ gây ra hiện tượng tự đổ bóng ("shadow acne"), trong khi giá trị quá lớn khiến shadow tách khỏi đối tượng đổ bóng ("peter-panning"). Điều chỉnh khi cần thiết.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_blur:

.. rst-class:: classref-property

:ref:`float<class_float>` **shadow_blur** = ``1.0`` :ref:`🔗<class_Light3D_property_shadow_blur>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Làm mờ các cạnh của shadow. Có thể dùng để ẩn các lỗi pixel trong shadow map có độ phân giải thấp. Giá trị cao có thể ảnh hưởng đến hiệu suất, khiến shadow trông có hạt và gây ra các lỗi không mong muốn khác. Hãy cố gắng giữ giá trị này gần với mặc định nhất có thể.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_caster_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **shadow_caster_mask** = ``4294967295`` :ref:`🔗<class_Light3D_property_shadow_caster_mask>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_caster_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_shadow_caster_mask**\ (\ )

Light sẽ chỉ tạo shadow bằng các object nằm trong các layer đã chọn.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shadow_enabled** = ``false`` :ref:`🔗<class_Light3D_property_shadow_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_shadow**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_shadow**\ (\ )

Nếu ``true``, light sẽ tạo shadow theo thời gian thực. Điều này gây ảnh hưởng đáng kể đến hiệu suất. Chỉ bật việc render shadow khi nó tạo ra khác biệt đáng kể trong diện mạo của scene, đồng thời cân nhắc sử dụng :ref:`distance_fade_enabled<class_Light3D_property_distance_fade_enabled>` để ẩn light khi ở xa :ref:`Camera3D<class_Camera3D>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_normal_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **shadow_normal_bias** = ``2.0`` :ref:`🔗<class_Light3D_property_shadow_normal_bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Dịch vị trí tra cứu trong shadow map theo normal của object. Có thể dùng để giảm các lỗi self-shadowing mà không cần sử dụng :ref:`shadow_bias<class_Light3D_property_shadow_bias>`. Trên thực tế, nên tinh chỉnh giá trị này cùng với :ref:`shadow_bias<class_Light3D_property_shadow_bias>` để giảm lỗi nhiều nhất có thể.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_opacity:

.. rst-class:: classref-property

:ref:`float<class_float>` **shadow_opacity** = ``1.0`` :ref:`🔗<class_Light3D_property_shadow_opacity>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

Độ mờ được sử dụng khi render shadow map của light. Các giá trị thấp hơn ``1.0`` khiến light hiện xuyên qua shadow. Có thể dùng cách này để giả lập global illumination với chi phí hiệu suất thấp.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_reverse_cull_face:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shadow_reverse_cull_face** = ``false`` :ref:`🔗<class_Light3D_property_shadow_reverse_cull_face>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_reverse_cull_face**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_shadow_reverse_cull_face**\ (\ )

Nếu ``true``, đảo ngược thao tác backface culling của mesh. Điều này hữu ích khi bạn có một mesh phẳng với light ở phía sau nó. Nếu cần tạo shadow ở cả hai mặt của mesh, hãy đặt mesh sử dụng shadow hai mặt bằng :ref:`GeometryInstance3D.SHADOW_CASTING_SETTING_DOUBLE_SIDED<class_GeometryInstance3D_constant_SHADOW_CASTING_SETTING_DOUBLE_SIDED>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_property_shadow_transmittance_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **shadow_transmittance_bias** = ``0.05`` :ref:`🔗<class_Light3D_property_shadow_transmittance_bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const|

.. container:: contribute

	Hiện chưa có mô tả cho property này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_Light3D_method_get_correlated_color:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_correlated_color**\ (\ ) |const| :ref:`🔗<class_Light3D_method_get_correlated_color>`

Trả về :ref:`Color<class_Color>` của blackbody lý tưởng tại :ref:`light_temperature<class_Light3D_property_light_temperature>` đã cho. Giá trị này được tính nội bộ dựa trên :ref:`light_temperature<class_Light3D_property_light_temperature>`. :ref:`Color<class_Color>` này được nhân với :ref:`light_color<class_Light3D_property_light_color>` trước khi gửi đến :ref:`RenderingServer<class_RenderingServer>`.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_method_get_param:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`\ ) |const| :ref:`🔗<class_Light3D_method_get_param>`

Trả về giá trị của parameter :ref:`Param<enum_Light3D_Param>` được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Light3D_method_set_param:

.. rst-class:: classref-method

|void| **set_param**\ (\ param\: :ref:`Param<enum_Light3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Light3D_method_set_param>`

Đặt giá trị cho parameter :ref:`Param<enum_Light3D_Param>` được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
