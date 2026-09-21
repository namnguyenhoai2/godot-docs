:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CPUParticles3D.xml.

.. _class_CPUParticles3D:

CPUParticles3D
==============

**Kế thừa:** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Emitter particle 3D dựa trên CPU.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node particle 3D dựa trên CPU, dùng để tạo nhiều hệ thống và hiệu ứng particle khác nhau.

Xem thêm :ref:`GPUParticles3D<class_GPUParticles3D>`, cung cấp cùng chức năng với hardware acceleration, nhưng có thể không chạy trên các thiết bị cũ hơn.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

 :doc:`Hệ thống particle (3D) <../tutorials/3d/particles/index>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`int<class_int>`                                   | :ref:`amount<class_CPUParticles3D_property_amount>`                                         | ``8``                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`angle_curve<class_CPUParticles3D_property_angle_curve>`                               |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`angle_max<class_CPUParticles3D_property_angle_max>`                                   | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`angle_min<class_CPUParticles3D_property_angle_min>`                                   | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`angular_velocity_curve<class_CPUParticles3D_property_angular_velocity_curve>`         |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`angular_velocity_max<class_CPUParticles3D_property_angular_velocity_max>`             | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`angular_velocity_min<class_CPUParticles3D_property_angular_velocity_min>`             | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`anim_offset_curve<class_CPUParticles3D_property_anim_offset_curve>`                   |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`anim_offset_max<class_CPUParticles3D_property_anim_offset_max>`                       | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`anim_offset_min<class_CPUParticles3D_property_anim_offset_min>`                       | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`anim_speed_curve<class_CPUParticles3D_property_anim_speed_curve>`                     |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`anim_speed_max<class_CPUParticles3D_property_anim_speed_max>`                         | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`anim_speed_min<class_CPUParticles3D_property_anim_speed_min>`                         | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Color<class_Color>`                               | :ref:`color<class_CPUParticles3D_property_color>`                                           | ``Color(1, 1, 1, 1)``      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Gradient<class_Gradient>`                         | :ref:`color_initial_ramp<class_CPUParticles3D_property_color_initial_ramp>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Gradient<class_Gradient>`                         | :ref:`color_ramp<class_CPUParticles3D_property_color_ramp>`                                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`damping_curve<class_CPUParticles3D_property_damping_curve>`                           |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`damping_max<class_CPUParticles3D_property_damping_max>`                               | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`damping_min<class_CPUParticles3D_property_damping_min>`                               | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Vector3<class_Vector3>`                           | :ref:`direction<class_CPUParticles3D_property_direction>`                                   | ``Vector3(1, 0, 0)``       |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>`         | :ref:`draw_order<class_CPUParticles3D_property_draw_order>`                                 | ``0``                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Vector3<class_Vector3>`                           | :ref:`emission_box_extents<class_CPUParticles3D_property_emission_box_extents>`             |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>`         | :ref:`emission_colors<class_CPUParticles3D_property_emission_colors>`                       | ``PackedColorArray()``     |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`     | :ref:`emission_normals<class_CPUParticles3D_property_emission_normals>`                     |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`     | :ref:`emission_points<class_CPUParticles3D_property_emission_points>`                       |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Vector3<class_Vector3>`                           | :ref:`emission_ring_axis<class_CPUParticles3D_property_emission_ring_axis>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`emission_ring_cone_angle<class_CPUParticles3D_property_emission_ring_cone_angle>`     |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`emission_ring_height<class_CPUParticles3D_property_emission_ring_height>`             |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`emission_ring_inner_radius<class_CPUParticles3D_property_emission_ring_inner_radius>` |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`emission_ring_radius<class_CPUParticles3D_property_emission_ring_radius>`             |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` | :ref:`emission_shape<class_CPUParticles3D_property_emission_shape>`                         | ``0``                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`emission_sphere_radius<class_CPUParticles3D_property_emission_sphere_radius>`         |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`emitting<class_CPUParticles3D_property_emitting>`                                     | ``true``                   |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`explosiveness<class_CPUParticles3D_property_explosiveness>`                           | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`int<class_int>`                                   | :ref:`fixed_fps<class_CPUParticles3D_property_fixed_fps>`                                   | ``0``                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`flatness<class_CPUParticles3D_property_flatness>`                                     | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`fract_delta<class_CPUParticles3D_property_fract_delta>`                               | ``true``                   |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Vector3<class_Vector3>`                           | :ref:`gravity<class_CPUParticles3D_property_gravity>`                                       | ``Vector3(0, -9.8, 0)``    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`hue_variation_curve<class_CPUParticles3D_property_hue_variation_curve>`               |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`hue_variation_max<class_CPUParticles3D_property_hue_variation_max>`                   | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`hue_variation_min<class_CPUParticles3D_property_hue_variation_min>`                   | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`initial_velocity_max<class_CPUParticles3D_property_initial_velocity_max>`             | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`initial_velocity_min<class_CPUParticles3D_property_initial_velocity_min>`             | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`lifetime<class_CPUParticles3D_property_lifetime>`                                     | ``1.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`lifetime_randomness<class_CPUParticles3D_property_lifetime_randomness>`               | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`linear_accel_curve<class_CPUParticles3D_property_linear_accel_curve>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`linear_accel_max<class_CPUParticles3D_property_linear_accel_max>`                     | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`linear_accel_min<class_CPUParticles3D_property_linear_accel_min>`                     | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`local_coords<class_CPUParticles3D_property_local_coords>`                             | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Mesh<class_Mesh>`                                 | :ref:`mesh<class_CPUParticles3D_property_mesh>`                                             |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`one_shot<class_CPUParticles3D_property_one_shot>`                                     | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`orbit_velocity_curve<class_CPUParticles3D_property_orbit_velocity_curve>`             |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`orbit_velocity_max<class_CPUParticles3D_property_orbit_velocity_max>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`orbit_velocity_min<class_CPUParticles3D_property_orbit_velocity_min>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`particle_flag_align_y<class_CPUParticles3D_property_particle_flag_align_y>`           | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`particle_flag_disable_z<class_CPUParticles3D_property_particle_flag_disable_z>`       | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`particle_flag_rotate_y<class_CPUParticles3D_property_particle_flag_rotate_y>`         | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`preprocess<class_CPUParticles3D_property_preprocess>`                                 | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`radial_accel_curve<class_CPUParticles3D_property_radial_accel_curve>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`radial_accel_max<class_CPUParticles3D_property_radial_accel_max>`                     | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`radial_accel_min<class_CPUParticles3D_property_radial_accel_min>`                     | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`randomness<class_CPUParticles3D_property_randomness>`                                 | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`scale_amount_curve<class_CPUParticles3D_property_scale_amount_curve>`                 |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`scale_amount_max<class_CPUParticles3D_property_scale_amount_max>`                     | ``1.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`scale_amount_min<class_CPUParticles3D_property_scale_amount_min>`                     | ``1.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`scale_curve_x<class_CPUParticles3D_property_scale_curve_x>`                           |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`scale_curve_y<class_CPUParticles3D_property_scale_curve_y>`                           |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`scale_curve_z<class_CPUParticles3D_property_scale_curve_z>`                           |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`int<class_int>`                                   | :ref:`seed<class_CPUParticles3D_property_seed>`                                             | ``0``                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`speed_scale<class_CPUParticles3D_property_speed_scale>`                               | ``1.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`split_scale<class_CPUParticles3D_property_split_scale>`                               | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`spread<class_CPUParticles3D_property_spread>`                                         | ``45.0``                   |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Curve<class_Curve>`                               | :ref:`tangential_accel_curve<class_CPUParticles3D_property_tangential_accel_curve>`         |                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`tangential_accel_max<class_CPUParticles3D_property_tangential_accel_max>`             | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`                               | :ref:`tangential_accel_min<class_CPUParticles3D_property_tangential_accel_min>`             | ``0.0``                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`use_fixed_seed<class_CPUParticles3D_property_use_fixed_seed>`                         | ``false``                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`AABB<class_AABB>`                                 | :ref:`visibility_aabb<class_CPUParticles3D_property_visibility_aabb>`                       | ``AABB(0, 0, 0, 0, 0, 0)`` |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`   | :ref:`capture_aabb<class_CPUParticles3D_method_capture_aabb>`\ (\ ) |const|                                                                                                                      |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`convert_from_particles<class_CPUParticles3D_method_convert_from_particles>`\ (\ particles\: :ref:`Node<class_Node>`\ )                                                                     |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Curve<class_Curve>` | :ref:`get_param_curve<class_CPUParticles3D_method_get_param_curve>`\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|                                                       |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param_max<class_CPUParticles3D_method_get_param_max>`\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|                                                           |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param_min<class_CPUParticles3D_method_get_param_min>`\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|                                                           |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`get_particle_flag<class_CPUParticles3D_method_get_particle_flag>`\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`\ ) |const|                                   |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`request_particles_process<class_CPUParticles3D_method_request_particles_process>`\ (\ process_time\: :ref:`float<class_float>`, process_time_residual\: :ref:`float<class_float>` = 0.0\ ) |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`restart<class_CPUParticles3D_method_restart>`\ (\ keep_seed\: :ref:`bool<class_bool>` = false\ )                                                                                           |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param_curve<class_CPUParticles3D_method_set_param_curve>`\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ )                            |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param_max<class_CPUParticles3D_method_set_param_max>`\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ )                                |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param_min<class_CPUParticles3D_method_set_param_min>`\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ )                                |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_particle_flag<class_CPUParticles3D_method_set_particle_flag>`\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`, enable\: :ref:`bool<class_bool>`\ )         |
   +---------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_CPUParticles3D_signal_finished:

.. rst-class:: classref-signal

**finished**\ (\ ) :ref:`🔗<class_CPUParticles3D_signal_finished>`

Được phát ra khi tất cả particle đang hoạt động đã xử lý xong. Khi :ref:`one_shot<class_CPUParticles3D_property_one_shot>` bị tắt, các particle sẽ được xử lý liên tục, nên signal này không bao giờ được phát ra.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumerations
------------

.. _enum_CPUParticles3D_DrawOrder:

.. rst-class:: classref-enumeration

enum **DrawOrder**: :ref:`🔗<enum_CPUParticles3D_DrawOrder>`

.. _class_CPUParticles3D_constant_DRAW_ORDER_INDEX:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>` **DRAW_ORDER_INDEX** = ``0``

Các particle được vẽ theo thứ tự phát ra.

.. _class_CPUParticles3D_constant_DRAW_ORDER_LIFETIME:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>` **DRAW_ORDER_LIFETIME** = ``1``

Các particle được vẽ theo thứ tự thời gian sống còn lại. Nói cách khác, particle có thời gian sống cao nhất được vẽ ở phía trước.

.. _class_CPUParticles3D_constant_DRAW_ORDER_VIEW_DEPTH:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>` **DRAW_ORDER_VIEW_DEPTH** = ``2``

Các particle được vẽ theo thứ tự độ sâu.

.. rst-class:: classref-item-separator

----

.. _enum_CPUParticles3D_Parameter:

.. rst-class:: classref-enumeration

enum **Parameter**: :ref:`🔗<enum_CPUParticles3D_Parameter>`

.. _class_CPUParticles3D_constant_PARAM_INITIAL_LINEAR_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_INITIAL_LINEAR_VELOCITY** = ``0``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính vận tốc ban đầu.

.. _class_CPUParticles3D_constant_PARAM_ANGULAR_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_ANGULAR_VELOCITY** = ``1``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính vận tốc góc.

.. _class_CPUParticles3D_constant_PARAM_ORBIT_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_ORBIT_VELOCITY** = ``2``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính vận tốc quỹ đạo.

.. _class_CPUParticles3D_constant_PARAM_LINEAR_ACCEL:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_LINEAR_ACCEL** = ``3``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính gia tốc tuyến tính.

.. _class_CPUParticles3D_constant_PARAM_RADIAL_ACCEL:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_RADIAL_ACCEL** = ``4``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính gia tốc hướng tâm.

.. _class_CPUParticles3D_constant_PARAM_TANGENTIAL_ACCEL:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_TANGENTIAL_ACCEL** = ``5``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính gia tốc tiếp tuyến.

.. _class_CPUParticles3D_constant_PARAM_DAMPING:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_DAMPING** = ``6``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính damping.

.. _class_CPUParticles3D_constant_PARAM_ANGLE:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_ANGLE** = ``7``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính góc.

.. _class_CPUParticles3D_constant_PARAM_SCALE:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_SCALE** = ``8``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính tỉ lệ.

.. _class_CPUParticles3D_constant_PARAM_HUE_VARIATION:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_HUE_VARIATION** = ``9``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính biến thiên sắc độ.

.. _class_CPUParticles3D_constant_PARAM_ANIM_SPEED:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_ANIM_SPEED** = ``10``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính tốc độ animation.

.. _class_CPUParticles3D_constant_PARAM_ANIM_OFFSET:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_ANIM_OFFSET** = ``11``

Dùng với :ref:`set_param_min()<class_CPUParticles3D_method_set_param_min>`, :ref:`set_param_max()<class_CPUParticles3D_method_set_param_max>` và :ref:`set_param_curve()<class_CPUParticles3D_method_set_param_curve>` để thiết lập các thuộc tính độ lệch animation.

.. _class_CPUParticles3D_constant_PARAM_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Parameter<enum_CPUParticles3D_Parameter>` **PARAM_MAX** = ``12``

Biểu thị kích thước của enum :ref:`Parameter<enum_CPUParticles3D_Parameter>`.

.. rst-class:: classref-item-separator

----

.. _enum_CPUParticles3D_ParticleFlags:

.. rst-class:: classref-enumeration

enum **ParticleFlags**: :ref:`🔗<enum_CPUParticles3D_ParticleFlags>`

.. _class_CPUParticles3D_constant_PARTICLE_FLAG_ALIGN_Y_TO_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>` **PARTICLE_FLAG_ALIGN_Y_TO_VELOCITY** = ``0``

Dùng với :ref:`set_particle_flag()<class_CPUParticles3D_method_set_particle_flag>` để thiết lập :ref:`particle_flag_align_y<class_CPUParticles3D_property_particle_flag_align_y>`.

.. _class_CPUParticles3D_constant_PARTICLE_FLAG_ROTATE_Y:

.. rst-class:: classref-enumeration-constant

:ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>` **PARTICLE_FLAG_ROTATE_Y** = ``1``

Dùng với :ref:`set_particle_flag()<class_CPUParticles3D_method_set_particle_flag>` để thiết lập :ref:`particle_flag_rotate_y<class_CPUParticles3D_property_particle_flag_rotate_y>`.

.. _class_CPUParticles3D_constant_PARTICLE_FLAG_DISABLE_Z:

.. rst-class:: classref-enumeration-constant

:ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>` **PARTICLE_FLAG_DISABLE_Z** = ``2``

Dùng với :ref:`set_particle_flag()<class_CPUParticles3D_method_set_particle_flag>` để thiết lập :ref:`particle_flag_disable_z<class_CPUParticles3D_property_particle_flag_disable_z>`.

.. _class_CPUParticles3D_constant_PARTICLE_FLAG_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>` **PARTICLE_FLAG_MAX** = ``3``

Biểu thị kích thước của enum :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`.

.. rst-class:: classref-item-separator

----

.. _enum_CPUParticles3D_EmissionShape:

.. rst-class:: classref-enumeration

enum **EmissionShape**: :ref:`🔗<enum_CPUParticles3D_EmissionShape>`

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_POINT:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_POINT** = ``0``

Tất cả particle sẽ được phát ra từ một điểm duy nhất.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_SPHERE:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_SPHERE** = ``1``

Particle sẽ được phát ra trong thể tích của một hình cầu.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_SPHERE_SURFACE:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_SPHERE_SURFACE** = ``2``

Particle sẽ được phát ra trên bề mặt của một hình cầu.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_BOX:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_BOX** = ``3``

Particle sẽ được phát ra trong thể tích của một hình hộp.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_POINTS:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_POINTS** = ``4``

Particle sẽ được phát ra tại một vị trí được chọn ngẫu nhiên trong số :ref:`emission_points<class_CPUParticles3D_property_emission_points>`. Màu của particle sẽ được điều biến bởi :ref:`emission_colors<class_CPUParticles3D_property_emission_colors>`.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_DIRECTED_POINTS:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_DIRECTED_POINTS** = ``5``

Particle sẽ được phát ra tại một vị trí được chọn ngẫu nhiên trong số :ref:`emission_points<class_CPUParticles3D_property_emission_points>`. Vận tốc và phép xoay của particle sẽ được thiết lập dựa trên :ref:`emission_normals<class_CPUParticles3D_property_emission_normals>`. Màu của particle sẽ được điều biến bởi :ref:`emission_colors<class_CPUParticles3D_property_emission_colors>`.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_RING:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_RING** = ``6``

Particle sẽ được phát ra theo dạng vòng tròn hoặc hình trụ.

.. _class_CPUParticles3D_constant_EMISSION_SHAPE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **EMISSION_SHAPE_MAX** = ``7``

Biểu thị kích thước của enum :ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_CPUParticles3D_property_amount:

.. rst-class:: classref-property

:ref:`int<class_int>` **amount** = ``8`` :ref:`🔗<class_CPUParticles3D_property_amount>`

.. rst-class:: classref-property-setget

- |void| **set_amount**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_amount**\ (\ )

Số lượng particle được phát ra trong một chu kỳ phát.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_angle_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **angle_curve** :ref:`🔗<class_CPUParticles3D_property_angle_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Phép xoay của mỗi particle sẽ được animation theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_angle_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **angle_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_angle_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Góc tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_angle_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **angle_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_angle_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Góc tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_angular_velocity_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **angular_velocity_curve** :ref:`🔗<class_CPUParticles3D_property_angular_velocity_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Vận tốc góc (tốc độ xoay) của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này trong suốt thời gian sống của nó. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_angular_velocity_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_velocity_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_angular_velocity_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Vận tốc góc ban đầu tối đa (tốc độ xoay) được áp dụng cho mỗi particle, tính theo *độ* trên giây.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_angular_velocity_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_velocity_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_angular_velocity_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Vận tốc góc ban đầu tối thiểu (tốc độ xoay) được áp dụng cho mỗi particle, tính theo *độ* trên giây.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_anim_offset_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **anim_offset_curve** :ref:`🔗<class_CPUParticles3D_property_anim_offset_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Độ lệch animation của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_anim_offset_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **anim_offset_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_anim_offset_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Độ lệch animation tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_anim_offset_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **anim_offset_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_anim_offset_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Độ lệch animation tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_anim_speed_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **anim_speed_curve** :ref:`🔗<class_CPUParticles3D_property_anim_speed_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Tốc độ animation của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_anim_speed_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **anim_speed_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_anim_speed_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Tốc độ animation particle tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_anim_speed_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **anim_speed_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_anim_speed_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Tốc độ animation particle tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_CPUParticles3D_property_color>`

.. rst-class:: classref-property-setget

- |void| **set_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_color**\ (\ )

Màu ban đầu của mỗi particle.

\ **Lưu ý:** :ref:`color<class_CPUParticles3D_property_color>` nhân với màu vertex của mesh particle. Để tạo hiệu ứng nhìn thấy được trên :ref:`BaseMaterial3D<class_BaseMaterial3D>`, :ref:`BaseMaterial3D.vertex_color_use_as_albedo<class_BaseMaterial3D_property_vertex_color_use_as_albedo>` *phải* là ``true``. Đối với :ref:`ShaderMaterial<class_ShaderMaterial>`, ``ALBEDO *= COLOR.rgb;`` phải được chèn vào hàm ``fragment()`` của shader. Nếu không, :ref:`color<class_CPUParticles3D_property_color>` sẽ không tạo ra hiệu ứng nhìn thấy được.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_color_initial_ramp:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **color_initial_ramp** :ref:`🔗<class_CPUParticles3D_property_color_initial_ramp>`

.. rst-class:: classref-property-setget

- |void| **set_color_initial_ramp**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_color_initial_ramp**\ (\ )

Màu ban đầu của mỗi particle sẽ thay đổi theo :ref:`Gradient<class_Gradient>` này (được nhân với :ref:`color<class_CPUParticles3D_property_color>`).

\ **Lưu ý:** :ref:`color_initial_ramp<class_CPUParticles3D_property_color_initial_ramp>` nhân với màu vertex của mesh particle. Để tạo hiệu ứng nhìn thấy được trên :ref:`BaseMaterial3D<class_BaseMaterial3D>`, :ref:`BaseMaterial3D.vertex_color_use_as_albedo<class_BaseMaterial3D_property_vertex_color_use_as_albedo>` *phải* là ``true``. Đối với :ref:`ShaderMaterial<class_ShaderMaterial>`, ``ALBEDO *= COLOR.rgb;`` phải được chèn vào hàm ``fragment()`` của shader. Nếu không, :ref:`color_initial_ramp<class_CPUParticles3D_property_color_initial_ramp>` sẽ không tạo ra hiệu ứng nhìn thấy được.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_color_ramp:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **color_ramp** :ref:`🔗<class_CPUParticles3D_property_color_ramp>`

.. rst-class:: classref-property-setget

- |void| **set_color_ramp**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_color_ramp**\ (\ )

Màu của mỗi particle sẽ thay đổi theo :ref:`Gradient<class_Gradient>` này trong suốt thời gian sống của nó (được nhân với :ref:`color<class_CPUParticles3D_property_color>`).

\ **Lưu ý:** :ref:`color_ramp<class_CPUParticles3D_property_color_ramp>` nhân với màu vertex của mesh hạt. Để tạo ra hiệu ứng nhìn thấy được trên một :ref:`BaseMaterial3D<class_BaseMaterial3D>`, :ref:`BaseMaterial3D.vertex_color_use_as_albedo<class_BaseMaterial3D_property_vertex_color_use_as_albedo>` *phải* là ``true``. Đối với một :ref:`ShaderMaterial<class_ShaderMaterial>`, ``ALBEDO *= COLOR.rgb;`` phải được chèn vào hàm ``fragment()`` của shader. Nếu không, :ref:`color_ramp<class_CPUParticles3D_property_color_ramp>` sẽ không tạo ra hiệu ứng nhìn thấy được.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_damping_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **damping_curve** :ref:`🔗<class_CPUParticles3D_property_damping_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Độ giảm chấn sẽ thay đổi dọc theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_damping_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **damping_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_damping_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Độ giảm chấn tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_damping_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **damping_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_damping_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Độ giảm chấn tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_direction:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **direction** = ``Vector3(1, 0, 0)`` :ref:`🔗<class_CPUParticles3D_property_direction>`

.. rst-class:: classref-property-setget

- |void| **set_direction**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_direction**\ (\ )

Vector đơn vị chỉ định hướng phát ra của các hạt.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_draw_order:

.. rst-class:: classref-property

:ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>` **draw_order** = ``0`` :ref:`🔗<class_CPUParticles3D_property_draw_order>`

.. rst-class:: classref-property-setget

- |void| **set_draw_order**\ (\ value\: :ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>`\ ) - :ref:`DrawOrder<enum_CPUParticles3D_DrawOrder>` **get_draw_order**\ (\ )

Thứ tự vẽ hạt.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_box_extents:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **emission_box_extents** :ref:`🔗<class_CPUParticles3D_property_emission_box_extents>`

.. rst-class:: classref-property-setget

- |void| **set_emission_box_extents**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_emission_box_extents**\ (\ )

Phạm vi của hình chữ nhật nếu :ref:`emission_shape<class_CPUParticles3D_property_emission_shape>` được đặt thành :ref:`EMISSION_SHAPE_BOX<class_CPUParticles3D_constant_EMISSION_SHAPE_BOX>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_colors:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **emission_colors** = ``PackedColorArray()`` :ref:`🔗<class_CPUParticles3D_property_emission_colors>`

.. rst-class:: classref-property-setget

- |void| **set_emission_colors**\ (\ value\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) - :ref:`PackedColorArray<class_PackedColorArray>` **get_emission_colors**\ (\ )

Sets the :ref:`Color<class_Color>`\ s to modulate particles by when using :ref:`EMISSION_SHAPE_POINTS<class_CPUParticles3D_constant_EMISSION_SHAPE_POINTS>` or :ref:`EMISSION_SHAPE_DIRECTED_POINTS<class_CPUParticles3D_constant_EMISSION_SHAPE_DIRECTED_POINTS>`.

\ **Lưu ý:** :ref:`emission_colors<class_CPUParticles3D_property_emission_colors>` nhân với màu vertex của mesh hạt. Để tạo ra hiệu ứng nhìn thấy được trên một :ref:`BaseMaterial3D<class_BaseMaterial3D>`, :ref:`BaseMaterial3D.vertex_color_use_as_albedo<class_BaseMaterial3D_property_vertex_color_use_as_albedo>` *phải* là ``true``. Đối với một :ref:`ShaderMaterial<class_ShaderMaterial>`, ``ALBEDO *= COLOR.rgb;`` phải được chèn vào hàm ``fragment()`` của shader. Nếu không, :ref:`emission_colors<class_CPUParticles3D_property_emission_colors>` sẽ không tạo ra hiệu ứng nhìn thấy được.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_normals:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **emission_normals** :ref:`🔗<class_CPUParticles3D_property_emission_normals>`

.. rst-class:: classref-property-setget

- |void| **set_emission_normals**\ (\ value\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) - :ref:`PackedVector3Array<class_PackedVector3Array>` **get_emission_normals**\ (\ )

Đặt hướng phát ra của các hạt khi sử dụng :ref:`EMISSION_SHAPE_DIRECTED_POINTS<class_CPUParticles3D_constant_EMISSION_SHAPE_DIRECTED_POINTS>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_points:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **emission_points** :ref:`🔗<class_CPUParticles3D_property_emission_points>`

.. rst-class:: classref-property-setget

- |void| **set_emission_points**\ (\ value\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) - :ref:`PackedVector3Array<class_PackedVector3Array>` **get_emission_points**\ (\ )

Đặt các vị trí ban đầu để tạo hạt khi sử dụng :ref:`EMISSION_SHAPE_POINTS<class_CPUParticles3D_constant_EMISSION_SHAPE_POINTS>` hoặc :ref:`EMISSION_SHAPE_DIRECTED_POINTS<class_CPUParticles3D_constant_EMISSION_SHAPE_DIRECTED_POINTS>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_ring_axis:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **emission_ring_axis** :ref:`🔗<class_CPUParticles3D_property_emission_ring_axis>`

.. rst-class:: classref-property-setget

- |void| **set_emission_ring_axis**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_emission_ring_axis**\ (\ )

Trục của vòng khi sử dụng emitter :ref:`EMISSION_SHAPE_RING<class_CPUParticles3D_constant_EMISSION_SHAPE_RING>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_ring_cone_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_ring_cone_angle** :ref:`🔗<class_CPUParticles3D_property_emission_ring_cone_angle>`

.. rst-class:: classref-property-setget

- |void| **set_emission_ring_cone_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_ring_cone_angle**\ (\ )

Góc của hình nón khi sử dụng emitter :ref:`EMISSION_SHAPE_RING<class_CPUParticles3D_constant_EMISSION_SHAPE_RING>`. Góc mặc định 90 độ tạo ra một vòng, trong khi góc 0 độ tạo ra một hình nón. Các giá trị trung gian sẽ tạo ra một vòng có một đầu lớn hơn đầu kia.

\ **Lưu ý:** Tùy thuộc vào :ref:`emission_ring_height<class_CPUParticles3D_property_emission_ring_height>`, góc có thể bị giới hạn khi chạm đến đầu vòng để tạo thành một hình nón hoàn hảo.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_ring_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_ring_height** :ref:`🔗<class_CPUParticles3D_property_emission_ring_height>`

.. rst-class:: classref-property-setget

- |void| **set_emission_ring_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_ring_height**\ (\ )

Chiều cao của vòng khi sử dụng emitter :ref:`EMISSION_SHAPE_RING<class_CPUParticles3D_constant_EMISSION_SHAPE_RING>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_ring_inner_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_ring_inner_radius** :ref:`🔗<class_CPUParticles3D_property_emission_ring_inner_radius>`

.. rst-class:: classref-property-setget

- |void| **set_emission_ring_inner_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_ring_inner_radius**\ (\ )

Bán kính trong của vòng khi sử dụng emitter :ref:`EMISSION_SHAPE_RING<class_CPUParticles3D_constant_EMISSION_SHAPE_RING>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_ring_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_ring_radius** :ref:`🔗<class_CPUParticles3D_property_emission_ring_radius>`

.. rst-class:: classref-property-setget

- |void| **set_emission_ring_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_ring_radius**\ (\ )

Bán kính của vòng khi sử dụng emitter :ref:`EMISSION_SHAPE_RING<class_CPUParticles3D_constant_EMISSION_SHAPE_RING>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_shape:

.. rst-class:: classref-property

:ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **emission_shape** = ``0`` :ref:`🔗<class_CPUParticles3D_property_emission_shape>`

.. rst-class:: classref-property-setget

- |void| **set_emission_shape**\ (\ value\: :ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>`\ ) - :ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` **get_emission_shape**\ (\ )

Các hạt sẽ được phát ra bên trong vùng này.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emission_sphere_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_sphere_radius** :ref:`🔗<class_CPUParticles3D_property_emission_sphere_radius>`

.. rst-class:: classref-property-setget

- |void| **set_emission_sphere_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_sphere_radius**\ (\ )

Bán kính của hình cầu nếu :ref:`EmissionShape<enum_CPUParticles3D_EmissionShape>` được đặt thành :ref:`EMISSION_SHAPE_SPHERE<class_CPUParticles3D_constant_EMISSION_SHAPE_SPHERE>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_emitting:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **emitting** = ``true`` :ref:`🔗<class_CPUParticles3D_property_emitting>`

.. rst-class:: classref-property-setget

- |void| **set_emitting**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_emitting**\ (\ )

Nếu ``true``, các hạt đang được phát ra. Có thể sử dụng :ref:`emitting<class_CPUParticles3D_property_emitting>` để bắt đầu và dừng phát hạt. Tuy nhiên, nếu :ref:`one_shot<class_CPUParticles3D_property_one_shot>` là ``true``, việc đặt :ref:`emitting<class_CPUParticles3D_property_emitting>` thành ``true`` sẽ không khởi động lại chu kỳ phát cho đến khi tất cả các hạt đang hoạt động hoàn tất quá trình xử lý. Bạn có thể sử dụng signal :ref:`finished<class_CPUParticles3D_signal_finished>` để được thông báo khi tất cả các hạt đang hoạt động hoàn tất quá trình xử lý.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_explosiveness:

.. rst-class:: classref-property

:ref:`float<class_float>` **explosiveness** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_explosiveness>`

.. rst-class:: classref-property-setget

- |void| **set_explosiveness_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_explosiveness_ratio**\ (\ )

Tốc độ phát các hạt trong một chu kỳ phát. Nếu lớn hơn ``0``, sẽ có khoảng ngắt giữa các lần phát trước khi chu kỳ tiếp theo bắt đầu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_fixed_fps:

.. rst-class:: classref-property

:ref:`int<class_int>` **fixed_fps** = ``0`` :ref:`🔗<class_CPUParticles3D_property_fixed_fps>`

.. rst-class:: classref-property-setget

- |void| **set_fixed_fps**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_fixed_fps**\ (\ )

Tốc độ khung hình của hệ thống hạt được cố định ở một giá trị. Ví dụ, thay đổi giá trị thành 2 sẽ khiến các hạt được kết xuất ở tốc độ 2 khung hình mỗi giây. Lưu ý rằng điều này không làm chậm bản thân hệ thống hạt.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_flatness:

.. rst-class:: classref-property

:ref:`float<class_float>` **flatness** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_flatness>`

.. rst-class:: classref-property-setget

- |void| **set_flatness**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_flatness**\ (\ )

Mức độ :ref:`spread<class_CPUParticles3D_property_spread>` trong mặt phẳng Y/Z. Giá trị ``1`` giới hạn các hạt trong mặt phẳng X/Z.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_fract_delta:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **fract_delta** = ``true`` :ref:`🔗<class_CPUParticles3D_property_fract_delta>`

.. rst-class:: classref-property-setget

- |void| **set_fractional_delta**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_fractional_delta**\ (\ )

Nếu ``true``, kết quả là phép tính delta phân số, tạo hiệu ứng hiển thị hạt mượt hơn.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_gravity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **gravity** = ``Vector3(0, -9.8, 0)`` :ref:`🔗<class_CPUParticles3D_property_gravity>`

.. rst-class:: classref-property-setget

- |void| **set_gravity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_gravity**\ (\ )

Trọng lực được áp dụng cho mọi hạt.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_hue_variation_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **hue_variation_curve** :ref:`🔗<class_CPUParticles3D_property_hue_variation_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Sắc độ của mỗi hạt sẽ thay đổi dọc theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_hue_variation_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **hue_variation_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_hue_variation_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Mức biến thiên sắc độ tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_hue_variation_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **hue_variation_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_hue_variation_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Mức biến thiên sắc độ tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_initial_velocity_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **initial_velocity_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_initial_velocity_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Giá trị tối đa của vận tốc ban đầu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_initial_velocity_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **initial_velocity_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_initial_velocity_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Giá trị tối thiểu của vận tốc ban đầu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_lifetime:

.. rst-class:: classref-property

:ref:`float<class_float>` **lifetime** = ``1.0`` :ref:`🔗<class_CPUParticles3D_property_lifetime>`

.. rst-class:: classref-property-setget

- |void| **set_lifetime**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lifetime**\ (\ )

Khoảng thời gian mỗi hạt tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_lifetime_randomness:

.. rst-class:: classref-property

:ref:`float<class_float>` **lifetime_randomness** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_lifetime_randomness>`

.. rst-class:: classref-property-setget

- |void| **set_lifetime_randomness**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lifetime_randomness**\ (\ )

Tỷ lệ ngẫu nhiên của thời gian tồn tại hạt.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_linear_accel_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **linear_accel_curve** :ref:`🔗<class_CPUParticles3D_property_linear_accel_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc tuyến tính của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_linear_accel_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_accel_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_linear_accel_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc tuyến tính tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_linear_accel_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_accel_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_linear_accel_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc tuyến tính tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_local_coords:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **local_coords** = ``false`` :ref:`🔗<class_CPUParticles3D_property_local_coords>`

.. rst-class:: classref-property-setget

- |void| **set_use_local_coordinates**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_local_coordinates**\ (\ )

Nếu ``true``, các particle sử dụng không gian tọa độ của node cha (được gọi là tọa độ cục bộ). Điều này khiến các particle di chuyển và xoay cùng với node **CPUParticles3D** (và các node cha của nó) khi node này được di chuyển hoặc xoay. Nếu ``false``, các particle sử dụng tọa độ toàn cục; chúng sẽ không di chuyển hoặc xoay cùng với node **CPUParticles3D** (và các node cha của nó) khi node này được di chuyển hoặc xoay.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_mesh:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **mesh** :ref:`🔗<class_CPUParticles3D_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_mesh**\ (\ )

:ref:`Mesh<class_Mesh>` được sử dụng cho mỗi particle. Nếu ``null``, các particle sẽ là hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_one_shot:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **one_shot** = ``false`` :ref:`🔗<class_CPUParticles3D_property_one_shot>`

.. rst-class:: classref-property-setget

- |void| **set_one_shot**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_one_shot**\ (\ )

Nếu ``true``, chỉ một chu kỳ phát sinh xảy ra. Nếu đặt thành ``true`` trong một chu kỳ, quá trình phát sinh sẽ dừng khi chu kỳ kết thúc.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_orbit_velocity_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **orbit_velocity_curve** :ref:`🔗<class_CPUParticles3D_property_orbit_velocity_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Vận tốc quỹ đạo của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_orbit_velocity_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **orbit_velocity_max** :ref:`🔗<class_CPUParticles3D_property_orbit_velocity_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Vận tốc quỹ đạo tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_orbit_velocity_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **orbit_velocity_min** :ref:`🔗<class_CPUParticles3D_property_orbit_velocity_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Vận tốc quỹ đạo tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_particle_flag_align_y:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **particle_flag_align_y** = ``false`` :ref:`🔗<class_CPUParticles3D_property_particle_flag_align_y>`

.. rst-class:: classref-property-setget

- |void| **set_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`, enable\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`\ ) |const|

Căn chỉnh trục Y của particle theo hướng vận tốc của nó.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_particle_flag_disable_z:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **particle_flag_disable_z** = ``false`` :ref:`🔗<class_CPUParticles3D_property_particle_flag_disable_z>`

.. rst-class:: classref-property-setget

- |void| **set_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`, enable\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`\ ) |const|

Nếu ``true``, các particle sẽ không di chuyển trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_particle_flag_rotate_y:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **particle_flag_rotate_y** = ``false`` :ref:`🔗<class_CPUParticles3D_property_particle_flag_rotate_y>`

.. rst-class:: classref-property-setget

- |void| **set_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`, enable\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`\ ) |const|

Nếu ``true``, các particle sẽ xoay quanh trục Y một góc :ref:`angle_min<class_CPUParticles3D_property_angle_min>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_preprocess:

.. rst-class:: classref-property

:ref:`float<class_float>` **preprocess** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_preprocess>`

.. rst-class:: classref-property-setget

- |void| **set_pre_process_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pre_process_time**\ (\ )

Hệ thống particle bắt đầu như thể đã chạy được số giây này.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_radial_accel_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **radial_accel_curve** :ref:`🔗<class_CPUParticles3D_property_radial_accel_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc hướng tâm của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_radial_accel_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **radial_accel_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_radial_accel_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc hướng tâm tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_radial_accel_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **radial_accel_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_radial_accel_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc hướng tâm tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_randomness:

.. rst-class:: classref-property

:ref:`float<class_float>` **randomness** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_randomness>`

.. rst-class:: classref-property-setget

- |void| **set_randomness_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_randomness_ratio**\ (\ )

Tỷ lệ ngẫu nhiên của thời gian tồn tại khi phát sinh.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_scale_amount_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **scale_amount_curve** :ref:`🔗<class_CPUParticles3D_property_scale_amount_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Scale của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_scale_amount_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **scale_amount_max** = ``1.0`` :ref:`🔗<class_CPUParticles3D_property_scale_amount_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Scale tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_scale_amount_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **scale_amount_min** = ``1.0`` :ref:`🔗<class_CPUParticles3D_property_scale_amount_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Scale tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_scale_curve_x:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **scale_curve_x** :ref:`🔗<class_CPUParticles3D_property_scale_curve_x>`

.. rst-class:: classref-property-setget

- |void| **set_scale_curve_x**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_scale_curve_x**\ (\ )

Curve cho scale trong suốt vòng đời, theo trục x.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_scale_curve_y:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **scale_curve_y** :ref:`🔗<class_CPUParticles3D_property_scale_curve_y>`

.. rst-class:: classref-property-setget

- |void| **set_scale_curve_y**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_scale_curve_y**\ (\ )

Curve cho scale trong suốt vòng đời, theo trục y.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_scale_curve_z:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **scale_curve_z** :ref:`🔗<class_CPUParticles3D_property_scale_curve_z>`

.. rst-class:: classref-property-setget

- |void| **set_scale_curve_z**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_scale_curve_z**\ (\ )

Curve cho scale trong suốt vòng đời, theo trục z.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_seed:

.. rst-class:: classref-property

:ref:`int<class_int>` **seed** = ``0`` :ref:`🔗<class_CPUParticles3D_property_seed>`

.. rst-class:: classref-property-setget

- |void| **set_seed**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_seed**\ (\ )

Đặt seed ngẫu nhiên được hệ thống particle sử dụng. Chỉ có hiệu lực nếu :ref:`use_fixed_seed<class_CPUParticles3D_property_use_fixed_seed>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **speed_scale** = ``1.0`` :ref:`🔗<class_CPUParticles3D_property_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_speed_scale**\ (\ )

Tỷ lệ scale tốc độ chạy của hệ thống particle. Có thể sử dụng giá trị ``0`` để tạm dừng các particle.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_split_scale:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **split_scale** = ``false`` :ref:`🔗<class_CPUParticles3D_property_split_scale>`

.. rst-class:: classref-property-setget

- |void| **set_split_scale**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_split_scale**\ (\ )

Nếu đặt thành ``true``, có thể chỉ định ba curve scale khác nhau, mỗi curve cho một trục scale.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_spread:

.. rst-class:: classref-property

:ref:`float<class_float>` **spread** = ``45.0`` :ref:`🔗<class_CPUParticles3D_property_spread>`

.. rst-class:: classref-property-setget

- |void| **set_spread**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_spread**\ (\ )

Khoảng hướng ban đầu của mỗi particle từ ``+spread`` đến ``-spread`` độ. Áp dụng cho các mặt phẳng X/Z và Y/Z.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_tangential_accel_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **tangential_accel_curve** :ref:`🔗<class_CPUParticles3D_property_tangential_accel_curve>`

.. rst-class:: classref-property-setget

- |void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc tiếp tuyến của mỗi particle sẽ thay đổi theo :ref:`Curve<class_Curve>` này. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_tangential_accel_max:

.. rst-class:: classref-property

:ref:`float<class_float>` **tangential_accel_max** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_tangential_accel_max>`

.. rst-class:: classref-property-setget

- |void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc tiếp tuyến tối đa.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_tangential_accel_min:

.. rst-class:: classref-property

:ref:`float<class_float>` **tangential_accel_min** = ``0.0`` :ref:`🔗<class_CPUParticles3D_property_tangential_accel_min>`

.. rst-class:: classref-property-setget

- |void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const|

Gia tốc tiếp tuyến tối thiểu.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_use_fixed_seed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_fixed_seed** = ``false`` :ref:`🔗<class_CPUParticles3D_property_use_fixed_seed>`

.. rst-class:: classref-property-setget

- |void| **set_use_fixed_seed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_fixed_seed**\ (\ )

Nếu ``true``, các particle sẽ sử dụng cùng một seed cho mọi lần mô phỏng, sử dụng seed được xác định trong :ref:`seed<class_CPUParticles3D_property_seed>`. Điều này hữu ích trong các tình huống cần kết quả hình ảnh nhất quán giữa các lần phát lại, chẳng hạn khi sử dụng chế độ Movie Maker.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_property_visibility_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **visibility_aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_CPUParticles3D_property_visibility_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_visibility_aabb**\ (\ )

:ref:`AABB<class_AABB>` xác định vùng của node cần hiển thị trên màn hình để hệ thống particle hoạt động.

Mở rộng hộp nếu các hạt đột ngột xuất hiện/biến mất khi node đi vào/ra khỏi màn hình. :ref:`AABB<class_AABB>` có thể được mở rộng bằng code hoặc bằng công cụ editor **Particles → Generate AABB**.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CPUParticles3D_method_capture_aabb:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **capture_aabb**\ (\ ) |const| :ref:`🔗<class_CPUParticles3D_method_capture_aabb>`

Trả về hộp giới hạn căn chỉnh theo trục chứa tất cả các hạt đang hoạt động trong frame hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_convert_from_particles:

.. rst-class:: classref-method

|void| **convert_from_particles**\ (\ particles\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_CPUParticles3D_method_convert_from_particles>`

Thiết lập các thuộc tính của node này để khớp với một node :ref:`GPUParticles3D<class_GPUParticles3D>` nhất định có :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>` được gán.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_get_param_curve:

.. rst-class:: classref-method

:ref:`Curve<class_Curve>` **get_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const| :ref:`🔗<class_CPUParticles3D_method_get_param_curve>`

Trả về :ref:`Curve<class_Curve>` của tham số được chỉ định bởi :ref:`Parameter<enum_CPUParticles3D_Parameter>`.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_get_param_max:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const| :ref:`🔗<class_CPUParticles3D_method_get_param_max>`

Trả về khoảng giá trị tối đa cho tham số đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_get_param_min:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`\ ) |const| :ref:`🔗<class_CPUParticles3D_method_get_param_min>`

Trả về khoảng giá trị tối thiểu cho tham số đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_get_particle_flag:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`\ ) |const| :ref:`🔗<class_CPUParticles3D_method_get_particle_flag>`

Trả về trạng thái được bật của cờ hạt đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_request_particles_process:

.. rst-class:: classref-method

|void| **request_particles_process**\ (\ process_time\: :ref:`float<class_float>`, process_time_residual\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_CPUParticles3D_method_request_particles_process>`

Yêu cầu các hạt được process thêm trong một frame duy nhất.

\ ``process_time`` xác định khoảng thời gian các hạt sẽ process khi emitting đang bật. ``process_time_residual`` xác định khoảng thời gian các hạt sẽ process khi emitting bị tắt trong quá trình mô phỏng. Khi kết hợp với :ref:`speed_scale<class_CPUParticles3D_property_speed_scale>` được đặt thành ``0.0``, tùy chọn này hữu ích để seek đến một thời điểm trong timeline của particle system.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_restart:

.. rst-class:: classref-method

|void| **restart**\ (\ keep_seed\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_CPUParticles3D_method_restart>`

Khởi động lại particle emitter.

Nếu ``keep_seed`` là ``true``, seed ngẫu nhiên hiện tại sẽ được giữ lại. Hữu ích khi seek và playback.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_set_param_curve:

.. rst-class:: classref-method

|void| **set_param_curve**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, curve\: :ref:`Curve<class_Curve>`\ ) :ref:`🔗<class_CPUParticles3D_method_set_param_curve>`

Thiết lập :ref:`Curve<class_Curve>` của tham số được chỉ định bởi :ref:`Parameter<enum_CPUParticles3D_Parameter>`. Đây phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_set_param_max:

.. rst-class:: classref-method

|void| **set_param_max**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_CPUParticles3D_method_set_param_max>`

Thiết lập giá trị tối đa cho tham số đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_set_param_min:

.. rst-class:: classref-method

|void| **set_param_min**\ (\ param\: :ref:`Parameter<enum_CPUParticles3D_Parameter>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_CPUParticles3D_method_set_param_min>`

Thiết lập giá trị tối thiểu cho tham số đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CPUParticles3D_method_set_particle_flag:

.. rst-class:: classref-method

|void| **set_particle_flag**\ (\ particle_flag\: :ref:`ParticleFlags<enum_CPUParticles3D_ParticleFlags>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CPUParticles3D_method_set_particle_flag>`

Bật hoặc tắt cờ hạt đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
