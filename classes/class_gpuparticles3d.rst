:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticles3D.xml.

.. _class_GPUParticles3D:

GPUParticles3D
==============

**Kế thừa:** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một particle emitter 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node particle 3D dùng để tạo nhiều hệ thống và hiệu ứng particle khác nhau. **GPUParticles3D** có một emitter tạo ra một số lượng particle nhất định theo một tốc độ cho trước.

Sử dụng :ref:`process_material<class_GPUParticles3D_property_process_material>` để thêm một :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>` nhằm cấu hình giao diện và hành vi của particle. Ngoài ra, bạn có thể thêm một :ref:`ShaderMaterial<class_ShaderMaterial>`, đối tượng này sẽ được áp dụng cho tất cả particle.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

 :doc:`Hệ thống particle (3D) <../tutorials/3d/particles/index>`

- :doc:`Điều khiển hàng nghìn con cá bằng Particles <../tutorials/performance/vertex_animation/controlling_thousands_of_fish>`

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`amount<class_GPUParticles3D_property_amount>`                                                 | ``8``                         |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>`                                     | ``1.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`collision_base_size<class_GPUParticles3D_property_collision_base_size>`                       | ``0.01``                      |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>`                                                | :ref:`draw_order<class_GPUParticles3D_property_draw_order>`                                         | ``0``                         |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`Mesh<class_Mesh>`                                                                        | :ref:`draw_pass_1<class_GPUParticles3D_property_draw_pass_1>`                                       |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`Mesh<class_Mesh>`                                                                        | :ref:`draw_pass_2<class_GPUParticles3D_property_draw_pass_2>`                                       |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`Mesh<class_Mesh>`                                                                        | :ref:`draw_pass_3<class_GPUParticles3D_property_draw_pass_3>`                                       |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`Mesh<class_Mesh>`                                                                        | :ref:`draw_pass_4<class_GPUParticles3D_property_draw_pass_4>`                                       |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`draw_passes<class_GPUParticles3D_property_draw_passes>`                                       | ``1``                         |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`Skin<class_Skin>`                                                                        | :ref:`draw_skin<class_GPUParticles3D_property_draw_skin>`                                           |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`emitting<class_GPUParticles3D_property_emitting>`                                             | ``true``                      |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`explosiveness<class_GPUParticles3D_property_explosiveness>`                                   | ``0.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`fixed_fps<class_GPUParticles3D_property_fixed_fps>`                                           | ``30``                        |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`fract_delta<class_GPUParticles3D_property_fract_delta>`                                       | ``true``                      |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`interp_to_end<class_GPUParticles3D_property_interp_to_end>`                                   | ``0.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`interpolate<class_GPUParticles3D_property_interpolate>`                                       | ``true``                      |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`lifetime<class_GPUParticles3D_property_lifetime>`                                             | ``1.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`local_coords<class_GPUParticles3D_property_local_coords>`                                     | ``false``                     |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`one_shot<class_GPUParticles3D_property_one_shot>`                                             | ``false``                     |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`preprocess<class_GPUParticles3D_property_preprocess>`                                         | ``0.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`Material<class_Material>`                                                                | :ref:`process_material<class_GPUParticles3D_property_process_material>`                             |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`randomness<class_GPUParticles3D_property_randomness>`                                         | ``0.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`seed<class_GPUParticles3D_property_seed>`                                                     | ``0``                         |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`speed_scale<class_GPUParticles3D_property_speed_scale>`                                       | ``1.0``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`NodePath<class_NodePath>`                                                                | :ref:`sub_emitter<class_GPUParticles3D_property_sub_emitter>`                                       | ``NodePath("")``              |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`trail_enabled<class_GPUParticles3D_property_trail_enabled>`                                   | ``false``                     |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`trail_lifetime<class_GPUParticles3D_property_trail_lifetime>`                                 | ``0.3``                       |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>`                                      | :ref:`transform_align<class_GPUParticles3D_property_transform_align>`                               | ``0``                         |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`ParticlesTransformAlignAxis<enum_RenderingServer_ParticlesTransformAlignAxis>`           | :ref:`transform_align_axis<class_GPUParticles3D_property_transform_align_axis>`                     |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`ParticlesTransformAlignCustomSrc<enum_RenderingServer_ParticlesTransformAlignCustomSrc>` | :ref:`transform_align_channel_filter<class_GPUParticles3D_property_transform_align_channel_filter>` |                               |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`use_fixed_seed<class_GPUParticles3D_property_use_fixed_seed>`                                 | ``false``                     |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+
   | :ref:`AABB<class_AABB>`                                                                        | :ref:`visibility_aabb<class_GPUParticles3D_property_visibility_aabb>`                               | ``AABB(-4, -4, -4, 8, 8, 8)`` |
   +------------------------------------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------+-------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>` | :ref:`capture_aabb<class_GPUParticles3D_method_capture_aabb>`\ (\ ) |const|                                                                                                                                                                                          |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`convert_from_particles<class_GPUParticles3D_method_convert_from_particles>`\ (\ particles\: :ref:`Node<class_Node>`\ )                                                                                                                                         |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`emit_particle<class_GPUParticles3D_method_emit_particle>`\ (\ xform\: :ref:`Transform3D<class_Transform3D>`, velocity\: :ref:`Vector3<class_Vector3>`, color\: :ref:`Color<class_Color>`, custom\: :ref:`Color<class_Color>`, flags\: :ref:`int<class_int>`\ ) |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Mesh<class_Mesh>` | :ref:`get_draw_pass_mesh<class_GPUParticles3D_method_get_draw_pass_mesh>`\ (\ pass\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`request_particles_process<class_GPUParticles3D_method_request_particles_process>`\ (\ process_time\: :ref:`float<class_float>`, process_time_residual\: :ref:`float<class_float>` = 0.0\ )                                                                     |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`restart<class_GPUParticles3D_method_restart>`\ (\ keep_seed\: :ref:`bool<class_bool>` = false\ )                                                                                                                                                               |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_draw_pass_mesh<class_GPUParticles3D_method_set_draw_pass_mesh>`\ (\ pass\: :ref:`int<class_int>`, mesh\: :ref:`Mesh<class_Mesh>`\ )                                                                                                                        |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_GPUParticles3D_signal_finished:

.. rst-class:: classref-signal

**finished**\ (\ ) :ref:`🔗<class_GPUParticles3D_signal_finished>`

Được phát ra khi tất cả particle đang hoạt động đã xử lý xong. Để ngay lập tức khởi động lại chu kỳ phát, hãy gọi :ref:`restart()<class_GPUParticles3D_method_restart>`.

Tín hiệu này không bao giờ được phát khi :ref:`one_shot<class_GPUParticles3D_property_one_shot>` bị tắt, vì các particle sẽ liên tục được phát và xử lý.

\ **Lưu ý:** Đối với các emitter :ref:`one_shot<class_GPUParticles3D_property_one_shot>`, do particle được tính toán trên GPU, có thể có một khoảng thời gian ngắn sau khi nhận tín hiệu mà việc đặt :ref:`emitting<class_GPUParticles3D_property_emitting>` thành ``true`` sẽ không khởi động lại chu kỳ phát. Có thể tránh độ trễ này bằng cách gọi :ref:`restart()<class_GPUParticles3D_method_restart>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_GPUParticles3D_DrawOrder:

.. rst-class:: classref-enumeration

enum **DrawOrder**: :ref:`🔗<enum_GPUParticles3D_DrawOrder>`

.. _class_GPUParticles3D_constant_DRAW_ORDER_INDEX:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>` **DRAW_ORDER_INDEX** = ``0``

Particle được vẽ theo thứ tự phát ra.

.. _class_GPUParticles3D_constant_DRAW_ORDER_LIFETIME:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>` **DRAW_ORDER_LIFETIME** = ``1``

Particle được vẽ theo thứ tự thời gian sống còn lại. Nói cách khác, particle có thời gian sống cao nhất được vẽ ở phía trước.

.. _class_GPUParticles3D_constant_DRAW_ORDER_REVERSE_LIFETIME:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>` **DRAW_ORDER_REVERSE_LIFETIME** = ``2``

Particle được vẽ theo thứ tự ngược của thời gian sống còn lại. Nói cách khác, particle có thời gian sống thấp nhất được vẽ ở phía trước.

.. _class_GPUParticles3D_constant_DRAW_ORDER_VIEW_DEPTH:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>` **DRAW_ORDER_VIEW_DEPTH** = ``3``

Particle được vẽ theo thứ tự độ sâu.

.. rst-class:: classref-item-separator

----

.. _enum_GPUParticles3D_EmitFlags:

.. rst-class:: classref-enumeration

enum **EmitFlags**: :ref:`🔗<enum_GPUParticles3D_EmitFlags>`

.. _class_GPUParticles3D_constant_EMIT_FLAG_POSITION:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles3D_EmitFlags>` **EMIT_FLAG_POSITION** = ``1``

Particle bắt đầu tại vị trí được chỉ định.

.. _class_GPUParticles3D_constant_EMIT_FLAG_ROTATION_SCALE:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles3D_EmitFlags>` **EMIT_FLAG_ROTATION_SCALE** = ``2``

Particle bắt đầu với rotation và scale được chỉ định.

.. _class_GPUParticles3D_constant_EMIT_FLAG_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles3D_EmitFlags>` **EMIT_FLAG_VELOCITY** = ``4``

Particle bắt đầu với vector velocity được chỉ định, xác định hướng và tốc độ phát.

.. _class_GPUParticles3D_constant_EMIT_FLAG_COLOR:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles3D_EmitFlags>` **EMIT_FLAG_COLOR** = ``8``

Particle bắt đầu với màu được chỉ định.

.. _class_GPUParticles3D_constant_EMIT_FLAG_CUSTOM:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles3D_EmitFlags>` **EMIT_FLAG_CUSTOM** = ``16``

Particle bắt đầu với dữ liệu ``CUSTOM`` được chỉ định.

.. rst-class:: classref-item-separator

----

.. _enum_GPUParticles3D_TransformAlign:

.. rst-class:: classref-enumeration

enum **TransformAlign**: :ref:`🔗<enum_GPUParticles3D_TransformAlign>`

.. _class_GPUParticles3D_constant_TRANSFORM_ALIGN_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **TRANSFORM_ALIGN_DISABLED** = ``0``

Không căn chỉnh transform của particle theo camera hoặc velocity.

.. _class_GPUParticles3D_constant_TRANSFORM_ALIGN_Z_BILLBOARD:

.. rst-class:: classref-enumeration-constant

:ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **TRANSFORM_ALIGN_Z_BILLBOARD** = ``1``

Căn chỉnh trục Z của mỗi particle hướng về phía camera.

.. _class_GPUParticles3D_constant_TRANSFORM_ALIGN_Y_TO_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **TRANSFORM_ALIGN_Y_TO_VELOCITY** = ``2``

Căn chỉnh trục Y của mỗi particle theo vector velocity.

.. _class_GPUParticles3D_constant_TRANSFORM_ALIGN_Z_BILLBOARD_Y_TO_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **TRANSFORM_ALIGN_Z_BILLBOARD_Y_TO_VELOCITY** = ``3``

Căn chỉnh trục Z của mỗi particle hướng về phía camera và trục Y theo vector velocity.

.. _class_GPUParticles3D_constant_TRANSFORM_ALIGN_LOCAL_BILLBOARD:

.. rst-class:: classref-enumeration-constant

:ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **TRANSFORM_ALIGN_LOCAL_BILLBOARD** = ``4``

Căn chỉnh trục Z của mỗi particle hướng về phía camera, đồng thời giữ nguyên một trục nhất định (X hoặc Y).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_GPUParticles3D_constant_MAX_DRAW_PASSES:

.. rst-class:: classref-constant

**MAX_DRAW_PASSES** = ``4`` :ref:`🔗<class_GPUParticles3D_constant_MAX_DRAW_PASSES>`

Số lượng draw pass tối đa được hỗ trợ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticles3D_property_amount:

.. rst-class:: classref-property

:ref:`int<class_int>` **amount** = ``8`` :ref:`🔗<class_GPUParticles3D_property_amount>`

.. rst-class:: classref-property-setget

- |void| **set_amount**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_amount**\ (\ )

Số lượng particle phát ra trong một chu kỳ phát. Tốc độ phát thực tế là ``(amount * amount_ratio) / lifetime`` particle mỗi giây. Giá trị cao hơn sẽ làm tăng yêu cầu GPU, ngay cả khi không phải tất cả particle đều hiển thị tại một thời điểm nhất định hoặc khi :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>` bị giảm.

\ **Lưu ý:** Thay đổi giá trị này sẽ khiến hệ thống particle khởi động lại. Để tránh điều đó, hãy thay đổi :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_amount_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **amount_ratio** = ``1.0`` :ref:`🔗<class_GPUParticles3D_property_amount_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_amount_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_amount_ratio**\ (\ )

Tỷ lệ particle thực sự nên được phát ra. Nếu đặt thành giá trị thấp hơn ``1.0``, thuộc tính này sẽ đặt số lượng particle được phát trong suốt thời gian sống thành ``amount * amount_ratio``. Không giống như việc thay đổi :ref:`amount<class_GPUParticles3D_property_amount>`, thay đổi :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>` trong khi đang phát không ảnh hưởng đến các particle đã được phát và không khiến hệ thống particle khởi động lại. Có thể sử dụng :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>` để tạo các hiệu ứng làm thay đổi số lượng particle được phát theo thời gian.

\ **Lưu ý:** Việc giảm :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>` không mang lại lợi ích về hiệu năng, vì tài nguyên vẫn cần được cấp phát và xử lý cho tổng :ref:`amount<class_GPUParticles3D_property_amount>` particle bất kể :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>`. Nếu bạn không định thay đổi số lượng particle được phát trong khi particle đang phát, hãy đảm bảo :ref:`amount_ratio<class_GPUParticles3D_property_amount_ratio>` được đặt thành ``1`` và thay đổi :ref:`amount<class_GPUParticles3D_property_amount>` theo ý muốn.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_collision_base_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_base_size** = ``0.01`` :ref:`🔗<class_GPUParticles3D_property_collision_base_size>`

.. rst-class:: classref-property-setget

- |void| **set_collision_base_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_base_size**\ (\ )

Đường kính cơ sở tính theo mét dùng cho va chạm của particle. Nếu particle có vẻ chìm xuống mặt đất khi va chạm, hãy tăng giá trị này. Nếu particle có vẻ lơ lửng khi va chạm, hãy giảm giá trị này. Chỉ có hiệu lực khi :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` là :ref:`ParticleProcessMaterial.COLLISION_RIGID<class_ParticleProcessMaterial_constant_COLLISION_RIGID>` hoặc :ref:`ParticleProcessMaterial.COLLISION_HIDE_ON_CONTACT<class_ParticleProcessMaterial_constant_COLLISION_HIDE_ON_CONTACT>`.

\ **Lưu ý:** Particle luôn có hình dạng va chạm hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_order:

.. rst-class:: classref-property

:ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>` **draw_order** = ``0`` :ref:`🔗<class_GPUParticles3D_property_draw_order>`

.. rst-class:: classref-property-setget

- |void| **set_draw_order**\ (\ value\: :ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>`\ ) - :ref:`DrawOrder<enum_GPUParticles3D_DrawOrder>` **get_draw_order**\ (\ )

Thứ tự vẽ particle.

\ **Lưu ý:** :ref:`DRAW_ORDER_INDEX<class_GPUParticles3D_constant_DRAW_ORDER_INDEX>` là tùy chọn duy nhất hỗ trợ motion vector cho các hiệu ứng như TAA. Nếu particle đục, nên sử dụng thứ tự vẽ này để khắc phục hiện tượng ghosting.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_pass_1:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **draw_pass_1** :ref:`🔗<class_GPUParticles3D_property_draw_pass_1>`

.. rst-class:: classref-property-setget

- |void| **set_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`, mesh\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`\ ) |const|

:ref:`Mesh<class_Mesh>` được vẽ cho draw pass đầu tiên.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_pass_2:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **draw_pass_2** :ref:`🔗<class_GPUParticles3D_property_draw_pass_2>`

.. rst-class:: classref-property-setget

- |void| **set_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`, mesh\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`\ ) |const|

:ref:`Mesh<class_Mesh>` được vẽ cho draw pass thứ hai.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_pass_3:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **draw_pass_3** :ref:`🔗<class_GPUParticles3D_property_draw_pass_3>`

.. rst-class:: classref-property-setget

- |void| **set_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`, mesh\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`\ ) |const|

:ref:`Mesh<class_Mesh>` được vẽ cho draw pass thứ ba.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_pass_4:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **draw_pass_4** :ref:`🔗<class_GPUParticles3D_property_draw_pass_4>`

.. rst-class:: classref-property-setget

- |void| **set_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`, mesh\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`\ ) |const|

:ref:`Mesh<class_Mesh>` được vẽ cho draw pass thứ tư.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_passes:

.. rst-class:: classref-property

:ref:`int<class_int>` **draw_passes** = ``1`` :ref:`🔗<class_GPUParticles3D_property_draw_passes>`

.. rst-class:: classref-property-setget

- |void| **set_draw_passes**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_draw_passes**\ (\ )

Số lượng draw pass khi render particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_draw_skin:

.. rst-class:: classref-property

:ref:`Skin<class_Skin>` **draw_skin** :ref:`🔗<class_GPUParticles3D_property_draw_skin>`

.. rst-class:: classref-property-setget

- |void| **set_skin**\ (\ value\: :ref:`Skin<class_Skin>`\ ) - :ref:`Skin<class_Skin>` **get_skin**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_emitting:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **emitting** = ``true`` :ref:`🔗<class_GPUParticles3D_property_emitting>`

.. rst-class:: classref-property-setget

- |void| **set_emitting**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_emitting**\ (\ )

Nếu ``true``, các particle đang được phát. Có thể sử dụng :ref:`emitting<class_GPUParticles3D_property_emitting>` để bắt đầu và dừng việc phát particle. Tuy nhiên, nếu :ref:`one_shot<class_GPUParticles3D_property_one_shot>` là ``true``, việc đặt :ref:`emitting<class_GPUParticles3D_property_emitting>` thành ``true`` sẽ không khởi động lại chu kỳ phát trừ khi tất cả particle đang hoạt động đã xử lý xong. Sử dụng signal :ref:`finished<class_GPUParticles3D_signal_finished>` để được thông báo khi tất cả particle đang hoạt động xử lý xong.

\ **Lưu ý:** Đối với các emitter :ref:`one_shot<class_GPUParticles3D_property_one_shot>`, do các particle được tính toán trên GPU, có thể có một khoảng thời gian ngắn sau khi nhận signal :ref:`finished<class_GPUParticles3D_signal_finished>` mà trong đó việc đặt giá trị này thành ``true`` sẽ không khởi động lại chu kỳ phát.

\ **Mẹo:** Nếu emitter :ref:`one_shot<class_GPUParticles3D_property_one_shot>` của bạn cần ngay lập tức khởi động lại việc phát particle khi nhận được signal :ref:`finished<class_GPUParticles3D_signal_finished>`, hãy cân nhắc gọi :ref:`restart()<class_GPUParticles3D_method_restart>` thay vì đặt :ref:`emitting<class_GPUParticles3D_property_emitting>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_explosiveness:

.. rst-class:: classref-property

:ref:`float<class_float>` **explosiveness** = ``0.0`` :ref:`🔗<class_GPUParticles3D_property_explosiveness>`

.. rst-class:: classref-property-setget

- |void| **set_explosiveness_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_explosiveness_ratio**\ (\ )

Tỷ lệ thời gian giữa mỗi lần phát. Nếu ``0``, các particle được phát liên tục. Nếu ``1``, tất cả particle được phát đồng thời.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_fixed_fps:

.. rst-class:: classref-property

:ref:`int<class_int>` **fixed_fps** = ``30`` :ref:`🔗<class_GPUParticles3D_property_fixed_fps>`

.. rst-class:: classref-property-setget

- |void| **set_fixed_fps**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_fixed_fps**\ (\ )

Frame rate của particle system được cố định ở một giá trị. Ví dụ, thay đổi giá trị thành 2 sẽ khiến các particle được render ở 2 frame mỗi giây. Lưu ý rằng điều này không làm chậm quá trình mô phỏng của particle system.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_fract_delta:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **fract_delta** = ``true`` :ref:`🔗<class_GPUParticles3D_property_fract_delta>`

.. rst-class:: classref-property-setget

- |void| **set_fractional_delta**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_fractional_delta**\ (\ )

Nếu ``true``, kết quả là phép tính delta phân số, tạo hiệu ứng hiển thị particle mượt hơn.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_interp_to_end:

.. rst-class:: classref-property

:ref:`float<class_float>` **interp_to_end** = ``0.0`` :ref:`🔗<class_GPUParticles3D_property_interp_to_end>`

.. rst-class:: classref-property-setget

- |void| **set_interp_to_end**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_interp_to_end**\ (\ )

Khiến tất cả particle trong node này nội suy về cuối vòng đời của chúng.

\ **Lưu ý:** Tính năng này chỉ hoạt động khi được sử dụng với :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>`. Cần triển khai thủ công cho các custom process shader.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_interpolate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **interpolate** = ``true`` :ref:`🔗<class_GPUParticles3D_property_interpolate>`

.. rst-class:: classref-property-setget

- |void| **set_interpolate**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_interpolate**\ (\ )

Bật nội suy particle, giúp chuyển động của particle mượt hơn khi :ref:`fixed_fps<class_GPUParticles3D_property_fixed_fps>` của chúng thấp hơn refresh rate của màn hình.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_lifetime:

.. rst-class:: classref-property

:ref:`float<class_float>` **lifetime** = ``1.0`` :ref:`🔗<class_GPUParticles3D_property_lifetime>`

.. rst-class:: classref-property-setget

- |void| **set_lifetime**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lifetime**\ (\ )

Khoảng thời gian mỗi particle tồn tại (tính bằng giây). Tốc độ phát hiệu dụng là ``(amount * amount_ratio) / lifetime`` particle mỗi giây.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_local_coords:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **local_coords** = ``false`` :ref:`🔗<class_GPUParticles3D_property_local_coords>`

.. rst-class:: classref-property-setget

- |void| **set_use_local_coordinates**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_local_coordinates**\ (\ )

Nếu ``true``, các particle sử dụng không gian tọa độ của node cha (được gọi là tọa độ local). Điều này khiến các particle di chuyển và xoay theo node **GPUParticles3D** (và các node cha của nó) khi node này được di chuyển hoặc xoay. Nếu ``false``, các particle sử dụng tọa độ global; chúng sẽ không di chuyển hoặc xoay theo node **GPUParticles3D** (và các node cha của nó) khi node này được di chuyển hoặc xoay.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_one_shot:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **one_shot** = ``false`` :ref:`🔗<class_GPUParticles3D_property_one_shot>`

.. rst-class:: classref-property-setget

- |void| **set_one_shot**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_one_shot**\ (\ )

Nếu ``true``, chỉ số particle bằng :ref:`amount<class_GPUParticles3D_property_amount>` mới được phát.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_preprocess:

.. rst-class:: classref-property

:ref:`float<class_float>` **preprocess** = ``0.0`` :ref:`🔗<class_GPUParticles3D_property_preprocess>`

.. rst-class:: classref-property-setget

- |void| **set_pre_process_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pre_process_time**\ (\ )

Khoảng thời gian tiền xử lý các particle trước khi animation bắt đầu. Cho phép bạn bắt đầu animation một khoảng thời gian sau khi các particle bắt đầu được phát.

\ **Lưu ý:** Điều này có thể rất tốn tài nguyên nếu đặt ở giá trị cao vì yêu cầu chạy particle shader một số lần bằng :ref:`fixed_fps<class_GPUParticles3D_property_fixed_fps>` (hoặc 30 nếu :ref:`fixed_fps<class_GPUParticles3D_property_fixed_fps>` là 0) cho mỗi giây. Trong các trường hợp cực đoan, điều này thậm chí có thể dẫn đến GPU bị crash do khối lượng công việc được thực hiện trong một frame đơn lẻ.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_process_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **process_material** :ref:`🔗<class_GPUParticles3D_property_process_material>`

.. rst-class:: classref-property-setget

- |void| **set_process_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_process_material**\ (\ )

:ref:`Material<class_Material>` để xử lý các particle. Có thể là một :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>` hoặc một :ref:`ShaderMaterial<class_ShaderMaterial>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_randomness:

.. rst-class:: classref-property

:ref:`float<class_float>` **randomness** = ``0.0`` :ref:`🔗<class_GPUParticles3D_property_randomness>`

.. rst-class:: classref-property-setget

- |void| **set_randomness_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_randomness_ratio**\ (\ )

Tỷ lệ ngẫu nhiên khi phát.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_seed:

.. rst-class:: classref-property

:ref:`int<class_int>` **seed** = ``0`` :ref:`🔗<class_GPUParticles3D_property_seed>`

.. rst-class:: classref-property-setget

- |void| **set_seed**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_seed**\ (\ )

Đặt random seed được particle system sử dụng. Chỉ có hiệu lực nếu :ref:`use_fixed_seed<class_GPUParticles3D_property_use_fixed_seed>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **speed_scale** = ``1.0`` :ref:`🔗<class_GPUParticles3D_property_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_speed_scale**\ (\ )

Tỷ lệ scale tốc độ. Có thể sử dụng giá trị ``0`` để tạm dừng các particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_sub_emitter:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **sub_emitter** = ``NodePath("")`` :ref:`🔗<class_GPUParticles3D_property_sub_emitter>`

.. rst-class:: classref-property-setget

- |void| **set_sub_emitter**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_sub_emitter**\ (\ )

Đường dẫn đến một node **GPUParticles3D** khác sẽ được sử dụng làm subemitter (xem :ref:`ParticleProcessMaterial.sub_emitter_mode<class_ParticleProcessMaterial_property_sub_emitter_mode>`). Subemitter có thể được sử dụng để tạo các hiệu ứng như pháo hoa, tia lửa khi va chạm, bong bóng vỡ thành các giọt nước và nhiều hiệu ứng khác.

\ **Lưu ý:** Khi :ref:`sub_emitter<class_GPUParticles3D_property_sub_emitter>` được thiết lập, node **GPUParticles3D** đích sẽ không còn tự phát particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_trail_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **trail_enabled** = ``false`` :ref:`🔗<class_GPUParticles3D_property_trail_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_trail_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_trail_enabled**\ (\ )

Nếu ``true``, bật particle trail bằng hệ thống mesh skinning. Được thiết kế để hoạt động với :ref:`RibbonTrailMesh<class_RibbonTrailMesh>` và :ref:`TubeTrailMesh<class_TubeTrailMesh>`.

\ **Lưu ý:** :ref:`BaseMaterial3D.use_particle_trails<class_BaseMaterial3D_property_use_particle_trails>` cũng phải được bật trên material của mesh particle. Nếu không, việc đặt :ref:`trail_enabled<class_GPUParticles3D_property_trail_enabled>` thành ``true`` sẽ không có tác dụng.

\ **Lưu ý:** Không giống :ref:`GPUParticles2D<class_GPUParticles2D>`, số lượng section và subdivision của trail được đặt trong các thuộc tính của :ref:`RibbonTrailMesh<class_RibbonTrailMesh>` hoặc :ref:`TubeTrailMesh<class_TubeTrailMesh>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_trail_lifetime:

.. rst-class:: classref-property

:ref:`float<class_float>` **trail_lifetime** = ``0.3`` :ref:`🔗<class_GPUParticles3D_property_trail_lifetime>`

.. rst-class:: classref-property-setget

- |void| **set_trail_lifetime**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_trail_lifetime**\ (\ )

Khoảng thời gian mà trail của particle cần thể hiện (tính bằng giây). Chỉ có hiệu lực nếu :ref:`trail_enabled<class_GPUParticles3D_property_trail_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_transform_align:

.. rst-class:: classref-property

:ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **transform_align** = ``0`` :ref:`🔗<class_GPUParticles3D_property_transform_align>`

.. rst-class:: classref-property-setget

- |void| **set_transform_align**\ (\ value\: :ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>`\ ) - :ref:`TransformAlign<enum_GPUParticles3D_TransformAlign>` **get_transform_align**\ (\ )

Căn chỉnh particle. Sử dụng tùy chọn này cho billboarding và căn chỉnh theo velocity.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_transform_align_axis:

.. rst-class:: classref-property

:ref:`ParticlesTransformAlignAxis<enum_RenderingServer_ParticlesTransformAlignAxis>` **transform_align_axis** :ref:`🔗<class_GPUParticles3D_property_transform_align_axis>`

.. rst-class:: classref-property-setget

- |void| **set_transform_align_axis**\ (\ value\: :ref:`ParticlesTransformAlignAxis<enum_RenderingServer_ParticlesTransformAlignAxis>`\ ) - :ref:`ParticlesTransformAlignAxis<enum_RenderingServer_ParticlesTransformAlignAxis>` **get_transform_align_axis**\ (\ )

Khi sử dụng transform align local billboard, trục nào sẽ được sử dụng cho billboarding. Chỉ hỗ trợ X hoặc Y.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_transform_align_channel_filter:

.. rst-class:: classref-property

:ref:`ParticlesTransformAlignCustomSrc<enum_RenderingServer_ParticlesTransformAlignCustomSrc>` **transform_align_channel_filter** :ref:`🔗<class_GPUParticles3D_property_transform_align_channel_filter>`

.. rst-class:: classref-property-setget

- |void| **set_transform_align_channel_filter**\ (\ value\: :ref:`ParticlesTransformAlignCustomSrc<enum_RenderingServer_ParticlesTransformAlignCustomSrc>`\ ) - :ref:`ParticlesTransformAlignCustomSrc<enum_RenderingServer_ParticlesTransformAlignCustomSrc>` **get_transform_align_channel_filter**\ (\ )

Đối với các particle được billboard, custom channel nào sẽ được đọc để tính góc của chúng.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_use_fixed_seed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_fixed_seed** = ``false`` :ref:`🔗<class_GPUParticles3D_property_use_fixed_seed>`

.. rst-class:: classref-property-setget

- |void| **set_use_fixed_seed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_fixed_seed**\ (\ )

Nếu ``true``, các hạt sẽ sử dụng cùng một seed cho mọi mô phỏng bằng seed được xác định trong :ref:`seed<class_GPUParticles3D_property_seed>`. Điều này hữu ích trong các trường hợp kết quả hiển thị cần nhất quán giữa các lần phát lại, chẳng hạn khi sử dụng chế độ Movie Maker.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_property_visibility_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **visibility_aabb** = ``AABB(-4, -4, -4, 8, 8, 8)`` :ref:`🔗<class_GPUParticles3D_property_visibility_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_visibility_aabb**\ (\ )

:ref:`AABB<class_AABB>` xác định vùng của node cần hiển thị trên màn hình để particle system hoạt động. :ref:`GeometryInstance3D.extra_cull_margin<class_GeometryInstance3D_property_extra_cull_margin>` được cộng thêm trên mỗi trục của AABB. Va chạm và lực hút giữa các hạt chỉ xảy ra trong vùng này.

Mở rộng hộp nếu các hạt đột ngột xuất hiện/biến mất khi node đi vào/ra khỏi màn hình. Có thể mở rộng :ref:`AABB<class_AABB>` bằng code hoặc bằng công cụ editor **Particles → Generate AABB**.

\ **Lưu ý:** :ref:`visibility_aabb<class_GPUParticles3D_property_visibility_aabb>` sẽ bị :ref:`GeometryInstance3D.custom_aabb<class_GeometryInstance3D_property_custom_aabb>` ghi đè nếu thuộc tính đó được đặt thành một giá trị không mặc định.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_GPUParticles3D_method_capture_aabb:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **capture_aabb**\ (\ ) |const| :ref:`🔗<class_GPUParticles3D_method_capture_aabb>`

Trả về bounding box căn chỉnh theo trục chứa tất cả các hạt đang hoạt động trong frame hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_method_convert_from_particles:

.. rst-class:: classref-method

|void| **convert_from_particles**\ (\ particles\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_GPUParticles3D_method_convert_from_particles>`

Đặt các thuộc tính của node này để khớp với một node :ref:`CPUParticles3D<class_CPUParticles3D>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_method_emit_particle:

.. rst-class:: classref-method

|void| **emit_particle**\ (\ xform\: :ref:`Transform3D<class_Transform3D>`, velocity\: :ref:`Vector3<class_Vector3>`, color\: :ref:`Color<class_Color>`, custom\: :ref:`Color<class_Color>`, flags\: :ref:`int<class_int>`\ ) :ref:`🔗<class_GPUParticles3D_method_emit_particle>`

Phát ra một hạt duy nhất. Việc ``xform``, ``velocity``, ``color`` và ``custom`` có được áp dụng hay không phụ thuộc vào giá trị của ``flags``. Xem :ref:`EmitFlags<enum_GPUParticles3D_EmitFlags>`.

ParticleProcessMaterial mặc định sẽ ghi đè ``color`` và sử dụng nội dung của ``custom`` làm ``(rotation, age, animation, lifetime)``.

\ **Lưu ý:** :ref:`emit_particle()<class_GPUParticles3D_method_emit_particle>` chỉ được hỗ trợ trên các phương thức render Forward+ và Mobile, không được hỗ trợ trên Compatibility.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_method_get_draw_pass_mesh:

.. rst-class:: classref-method

:ref:`Mesh<class_Mesh>` **get_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GPUParticles3D_method_get_draw_pass_mesh>`

Trả về :ref:`Mesh<class_Mesh>` được vẽ tại chỉ mục ``pass``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_method_request_particles_process:

.. rst-class:: classref-method

|void| **request_particles_process**\ (\ process_time\: :ref:`float<class_float>`, process_time_residual\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_GPUParticles3D_method_request_particles_process>`

Yêu cầu các hạt được process trong thêm một khoảng thời gian process ở một frame duy nhất.

\ ``process_time`` xác định khoảng thời gian các hạt sẽ được process khi emitting đang bật. ``process_time_residual`` xác định khoảng thời gian các hạt sẽ được process khi emitting được tắt trong mô phỏng. Khi kết hợp với :ref:`speed_scale<class_GPUParticles3D_property_speed_scale>` được đặt thành ``0.0``, điều này hữu ích để có thể seek timeline của particle system.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_method_restart:

.. rst-class:: classref-method

|void| **restart**\ (\ keep_seed\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_GPUParticles3D_method_restart>`

Khởi động lại chu kỳ phát hạt, xóa các hạt hiện có. Để tránh các hạt biến mất khỏi viewport, hãy chờ signal :ref:`finished<class_GPUParticles3D_signal_finished>` trước khi gọi.

\ **Lưu ý:** Signal :ref:`finished<class_GPUParticles3D_signal_finished>` chỉ được phát ra bởi các emitter :ref:`one_shot<class_GPUParticles3D_property_one_shot>`.

Nếu ``keep_seed`` là ``true``, seed ngẫu nhiên hiện tại sẽ được giữ nguyên. Hữu ích cho việc seek và playback.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles3D_method_set_draw_pass_mesh:

.. rst-class:: classref-method

|void| **set_draw_pass_mesh**\ (\ pass\: :ref:`int<class_int>`, mesh\: :ref:`Mesh<class_Mesh>`\ ) :ref:`🔗<class_GPUParticles3D_method_set_draw_pass_mesh>`

Đặt :ref:`Mesh<class_Mesh>` được vẽ tại chỉ mục ``pass``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
