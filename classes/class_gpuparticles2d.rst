:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticles2D.xml.

.. _class_GPUParticles2D:

GPUParticles2D
==============

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Bộ phát particle 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node particle 2D được dùng để tạo nhiều hệ thống và hiệu ứng particle khác nhau. **GPUParticles2D** có một emitter tạo ra một số lượng particle nhất định với tốc độ cho trước.

Sử dụng thuộc tính :ref:`process_material<class_GPUParticles2D_property_process_material>` để thêm một :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>` nhằm cấu hình hình thức và hành vi của particle. Ngoài ra, bạn có thể thêm một :ref:`ShaderMaterial<class_ShaderMaterial>`, đối tượng này sẽ được áp dụng cho tất cả particle.

Particle 2D có thể tùy chọn va chạm với :ref:`LightOccluder2D<class_LightOccluder2D>`, nhưng không va chạm với các node :ref:`PhysicsBody2D<class_PhysicsBody2D>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

 :doc:`Hệ thống particle (2D) <../tutorials/2d/particle_systems_2d>`

- `2D Particles Demo <https://godotengine.org/asset-library/asset/2724>`__

- `2D Dodge The Creeps Demo (uses GPUParticles2D for the trail behind the player) <https://godotengine.org/asset-library/asset/2712>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`int<class_int>`                           | :ref:`amount<class_GPUParticles2D_property_amount>`                                         | ``8``                           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>`                             | ``1.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`collision_base_size<class_GPUParticles2D_property_collision_base_size>`               | ``1.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>` | :ref:`draw_order<class_GPUParticles2D_property_draw_order>`                                 | ``1``                           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`emitting<class_GPUParticles2D_property_emitting>`                                     | ``true``                        |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`explosiveness<class_GPUParticles2D_property_explosiveness>`                           | ``0.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`int<class_int>`                           | :ref:`fixed_fps<class_GPUParticles2D_property_fixed_fps>`                                   | ``30``                          |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`fract_delta<class_GPUParticles2D_property_fract_delta>`                               | ``true``                        |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`interp_to_end<class_GPUParticles2D_property_interp_to_end>`                           | ``0.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`interpolate<class_GPUParticles2D_property_interpolate>`                               | ``true``                        |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`lifetime<class_GPUParticles2D_property_lifetime>`                                     | ``1.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`local_coords<class_GPUParticles2D_property_local_coords>`                             | ``false``                       |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`one_shot<class_GPUParticles2D_property_one_shot>`                                     | ``false``                       |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`preprocess<class_GPUParticles2D_property_preprocess>`                                 | ``0.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`Material<class_Material>`                 | :ref:`process_material<class_GPUParticles2D_property_process_material>`                     |                                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`randomness<class_GPUParticles2D_property_randomness>`                                 | ``0.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`int<class_int>`                           | :ref:`seed<class_GPUParticles2D_property_seed>`                                             | ``0``                           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`speed_scale<class_GPUParticles2D_property_speed_scale>`                               | ``1.0``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`NodePath<class_NodePath>`                 | :ref:`sub_emitter<class_GPUParticles2D_property_sub_emitter>`                               | ``NodePath("")``                |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`Texture2D<class_Texture2D>`               | :ref:`texture<class_GPUParticles2D_property_texture>`                                       |                                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`trail_enabled<class_GPUParticles2D_property_trail_enabled>`                           | ``false``                       |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`float<class_float>`                       | :ref:`trail_lifetime<class_GPUParticles2D_property_trail_lifetime>`                         | ``0.3``                         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`int<class_int>`                           | :ref:`trail_section_subdivisions<class_GPUParticles2D_property_trail_section_subdivisions>` | ``4``                           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`int<class_int>`                           | :ref:`trail_sections<class_GPUParticles2D_property_trail_sections>`                         | ``8``                           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`use_fixed_seed<class_GPUParticles2D_property_use_fixed_seed>`                         | ``false``                       |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+
   | :ref:`Rect2<class_Rect2>`                       | :ref:`visibility_rect<class_GPUParticles2D_property_visibility_rect>`                       | ``Rect2(-100, -100, 200, 200)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------------------------+---------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Rect2<class_Rect2>` | :ref:`capture_rect<class_GPUParticles2D_method_capture_rect>`\ (\ ) |const|                                                                                                                                                                                          |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`convert_from_particles<class_GPUParticles2D_method_convert_from_particles>`\ (\ particles\: :ref:`Node<class_Node>`\ )                                                                                                                                         |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`emit_particle<class_GPUParticles2D_method_emit_particle>`\ (\ xform\: :ref:`Transform2D<class_Transform2D>`, velocity\: :ref:`Vector2<class_Vector2>`, color\: :ref:`Color<class_Color>`, custom\: :ref:`Color<class_Color>`, flags\: :ref:`int<class_int>`\ ) |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`request_particles_process<class_GPUParticles2D_method_request_particles_process>`\ (\ process_time\: :ref:`float<class_float>`, process_time_residual\: :ref:`float<class_float>` = 0\ )                                                                       |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`restart<class_GPUParticles2D_method_restart>`\ (\ keep_seed\: :ref:`bool<class_bool>` = false\ )                                                                                                                                                               |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_GPUParticles2D_signal_finished:

.. rst-class:: classref-signal

**finished**\ (\ ) :ref:`🔗<class_GPUParticles2D_signal_finished>`

Được phát ra khi tất cả particle đang hoạt động đã xử lý xong. Để ngay lập tức khởi động lại chu kỳ phát, hãy gọi :ref:`restart()<class_GPUParticles2D_method_restart>`.

Signal này không bao giờ được phát khi :ref:`one_shot<class_GPUParticles2D_property_one_shot>` bị tắt, vì particle sẽ được phát và xử lý liên tục.

\ **Lưu ý:** Đối với các emitter :ref:`one_shot<class_GPUParticles2D_property_one_shot>`, do particle được tính toán trên GPU, có thể có một khoảng thời gian ngắn sau khi nhận signal trong đó việc đặt :ref:`emitting<class_GPUParticles2D_property_emitting>` thành ``true`` sẽ không khởi động lại chu kỳ phát. Có thể tránh độ trễ này bằng cách gọi :ref:`restart()<class_GPUParticles2D_method_restart>` thay thế.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_GPUParticles2D_DrawOrder:

.. rst-class:: classref-enumeration

enum **DrawOrder**: :ref:`🔗<enum_GPUParticles2D_DrawOrder>`

.. _class_GPUParticles2D_constant_DRAW_ORDER_INDEX:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>` **DRAW_ORDER_INDEX** = ``0``

Particle được vẽ theo thứ tự phát.

.. _class_GPUParticles2D_constant_DRAW_ORDER_LIFETIME:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>` **DRAW_ORDER_LIFETIME** = ``1``

Particle được vẽ theo thứ tự thời gian sống còn lại. Nói cách khác, particle có thời gian sống cao nhất được vẽ ở phía trước.

.. _class_GPUParticles2D_constant_DRAW_ORDER_REVERSE_LIFETIME:

.. rst-class:: classref-enumeration-constant

:ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>` **DRAW_ORDER_REVERSE_LIFETIME** = ``2``

Particle được vẽ theo thứ tự ngược của thời gian sống còn lại. Nói cách khác, particle có thời gian sống thấp nhất được vẽ ở phía trước.

.. rst-class:: classref-item-separator

----

.. _enum_GPUParticles2D_EmitFlags:

.. rst-class:: classref-enumeration

enum **EmitFlags**: :ref:`🔗<enum_GPUParticles2D_EmitFlags>`

.. _class_GPUParticles2D_constant_EMIT_FLAG_POSITION:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles2D_EmitFlags>` **EMIT_FLAG_POSITION** = ``1``

Particle bắt đầu tại vị trí được chỉ định.

.. _class_GPUParticles2D_constant_EMIT_FLAG_ROTATION_SCALE:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles2D_EmitFlags>` **EMIT_FLAG_ROTATION_SCALE** = ``2``

Particle bắt đầu với rotation và scale được chỉ định.

.. _class_GPUParticles2D_constant_EMIT_FLAG_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles2D_EmitFlags>` **EMIT_FLAG_VELOCITY** = ``4``

Particle bắt đầu với vector vận tốc được chỉ định, xác định hướng và tốc độ phát.

.. _class_GPUParticles2D_constant_EMIT_FLAG_COLOR:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles2D_EmitFlags>` **EMIT_FLAG_COLOR** = ``8``

Particle bắt đầu với màu được chỉ định.

.. _class_GPUParticles2D_constant_EMIT_FLAG_CUSTOM:

.. rst-class:: classref-enumeration-constant

:ref:`EmitFlags<enum_GPUParticles2D_EmitFlags>` **EMIT_FLAG_CUSTOM** = ``16``

Particle bắt đầu với dữ liệu ``CUSTOM`` được chỉ định.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticles2D_property_amount:

.. rst-class:: classref-property

:ref:`int<class_int>` **amount** = ``8`` :ref:`🔗<class_GPUParticles2D_property_amount>`

.. rst-class:: classref-property-setget

- |void| **set_amount**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_amount**\ (\ )

Số lượng particle sẽ phát trong một chu kỳ phát. Tốc độ phát hiệu dụng là ``(amount * amount_ratio) / lifetime`` particle mỗi giây. Giá trị cao hơn sẽ làm tăng yêu cầu GPU, ngay cả khi không phải tất cả particle đều hiển thị tại một thời điểm nhất định hoặc khi :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>` bị giảm.

\ **Lưu ý:** Thay đổi giá trị này sẽ khiến hệ thống particle khởi động lại. Để tránh điều này, hãy thay đổi :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_amount_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **amount_ratio** = ``1.0`` :ref:`🔗<class_GPUParticles2D_property_amount_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_amount_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_amount_ratio**\ (\ )

Tỷ lệ particle thực sự sẽ được phát. Nếu đặt thành giá trị thấp hơn ``1.0``, thuộc tính này sẽ đặt số particle được phát trong suốt thời gian sống thành ``amount * amount_ratio``. Không giống như việc thay đổi :ref:`amount<class_GPUParticles2D_property_amount>`, thay đổi :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>` trong khi đang phát không ảnh hưởng đến các particle đã được phát và không khiến hệ thống particle khởi động lại. Có thể sử dụng :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>` để tạo các hiệu ứng khiến số lượng particle được phát thay đổi theo thời gian.

\ **Lưu ý:** Việc giảm :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>` không mang lại lợi ích về hiệu năng, vì tài nguyên vẫn cần được cấp phát và xử lý cho tổng :ref:`amount<class_GPUParticles2D_property_amount>` particle bất kể :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>`. Nếu bạn không có ý định thay đổi số lượng particle được phát trong khi particle đang phát, hãy đảm bảo :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>` được đặt thành ``1`` và thay đổi :ref:`amount<class_GPUParticles2D_property_amount>` theo ý muốn.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_collision_base_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_base_size** = ``1.0`` :ref:`🔗<class_GPUParticles2D_property_collision_base_size>`

.. rst-class:: classref-property-setget

- |void| **set_collision_base_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_base_size**\ (\ )

Hệ số nhân cho bán kính va chạm của particle. ``1.0`` tương ứng với kích thước của sprite. Nếu particle có vẻ bị chìm xuống đất khi va chạm, hãy tăng giá trị này. Nếu particle có vẻ lơ lửng khi va chạm, hãy giảm giá trị này. Chỉ có hiệu lực khi :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` là :ref:`ParticleProcessMaterial.COLLISION_RIGID<class_ParticleProcessMaterial_constant_COLLISION_RIGID>` hoặc :ref:`ParticleProcessMaterial.COLLISION_HIDE_ON_CONTACT<class_ParticleProcessMaterial_constant_COLLISION_HIDE_ON_CONTACT>`.

\ **Lưu ý:** Particle luôn có hình dạng va chạm hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_draw_order:

.. rst-class:: classref-property

:ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>` **draw_order** = ``1`` :ref:`🔗<class_GPUParticles2D_property_draw_order>`

.. rst-class:: classref-property-setget

- |void| **set_draw_order**\ (\ value\: :ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>`\ ) - :ref:`DrawOrder<enum_GPUParticles2D_DrawOrder>` **get_draw_order**\ (\ )

Thứ tự vẽ particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_emitting:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **emitting** = ``true`` :ref:`🔗<class_GPUParticles2D_property_emitting>`

.. rst-class:: classref-property-setget

- |void| **set_emitting**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_emitting**\ (\ )

Nếu ``true``, particle đang được phát. Có thể sử dụng :ref:`emitting<class_GPUParticles2D_property_emitting>` để bắt đầu và dừng việc phát particle. Tuy nhiên, nếu :ref:`one_shot<class_GPUParticles2D_property_one_shot>` là ``true``, việc đặt :ref:`emitting<class_GPUParticles2D_property_emitting>` thành ``true`` sẽ không khởi động lại chu kỳ phát trừ khi tất cả particle đang hoạt động đã xử lý xong. Sử dụng signal :ref:`finished<class_GPUParticles2D_signal_finished>` để được thông báo khi tất cả particle đang hoạt động xử lý xong.

\ **Lưu ý:** Đối với các emitter :ref:`one_shot<class_GPUParticles2D_property_one_shot>`, do particle được tính toán trên GPU, có thể có một khoảng thời gian ngắn sau khi nhận signal :ref:`finished<class_GPUParticles2D_signal_finished>` trong đó việc đặt thuộc tính này thành ``true`` sẽ không khởi động lại chu kỳ phát.

\ **Mẹo:** Nếu emitter :ref:`one_shot<class_GPUParticles2D_property_one_shot>` của bạn cần ngay lập tức khởi động lại việc phát particle khi nhận signal :ref:`finished<class_GPUParticles2D_signal_finished>`, hãy cân nhắc gọi :ref:`restart()<class_GPUParticles2D_method_restart>` thay vì đặt :ref:`emitting<class_GPUParticles2D_property_emitting>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_explosiveness:

.. rst-class:: classref-property

:ref:`float<class_float>` **explosiveness** = ``0.0`` :ref:`🔗<class_GPUParticles2D_property_explosiveness>`

.. rst-class:: classref-property-setget

- |void| **set_explosiveness_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_explosiveness_ratio**\ (\ )

Tốc độ particle được phát trong một chu kỳ phát. Nếu lớn hơn ``0``, sẽ có một khoảng ngắt trong việc phát trước khi chu kỳ tiếp theo bắt đầu.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_fixed_fps:

.. rst-class:: classref-property

:ref:`int<class_int>` **fixed_fps** = ``30`` :ref:`🔗<class_GPUParticles2D_property_fixed_fps>`

.. rst-class:: classref-property-setget

- |void| **set_fixed_fps**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_fixed_fps**\ (\ )

Tốc độ khung hình của hệ thống particle được cố định ở một giá trị. Ví dụ, thay đổi giá trị thành 2 sẽ khiến particle được render ở tốc độ 2 khung hình mỗi giây. Lưu ý rằng điều này không làm chậm simulation của chính hệ thống particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_fract_delta:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **fract_delta** = ``true`` :ref:`🔗<class_GPUParticles2D_property_fract_delta>`

.. rst-class:: classref-property-setget

- |void| **set_fractional_delta**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_fractional_delta**\ (\ )

Nếu ``true``, phép tính delta phân số sẽ cho hiệu ứng hiển thị particle mượt hơn.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_interp_to_end:

.. rst-class:: classref-property

:ref:`float<class_float>` **interp_to_end** = ``0.0`` :ref:`🔗<class_GPUParticles2D_property_interp_to_end>`

.. rst-class:: classref-property-setget

- |void| **set_interp_to_end**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_interp_to_end**\ (\ )

Khiến tất cả particle trong node này nội suy về cuối thời gian sống của chúng.

\ **Lưu ý:** Tính năng này chỉ hoạt động khi được sử dụng với :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>`. Cần tự triển khai tính năng này cho các process shader tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_interpolate:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **interpolate** = ``true`` :ref:`🔗<class_GPUParticles2D_property_interpolate>`

.. rst-class:: classref-property-setget

- |void| **set_interpolate**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_interpolate**\ (\ )

Bật nội suy particle, giúp chuyển động của particle mượt hơn khi :ref:`fixed_fps<class_GPUParticles2D_property_fixed_fps>` của chúng thấp hơn tốc độ làm mới màn hình.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_lifetime:

.. rst-class:: classref-property

:ref:`float<class_float>` **lifetime** = ``1.0`` :ref:`🔗<class_GPUParticles2D_property_lifetime>`

.. rst-class:: classref-property-setget

- |void| **set_lifetime**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_lifetime**\ (\ )

Khoảng thời gian mỗi particle sẽ tồn tại (tính bằng giây). Tốc độ phát hiệu dụng là ``(amount * amount_ratio) / lifetime`` particle mỗi giây.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_local_coords:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **local_coords** = ``false`` :ref:`🔗<class_GPUParticles2D_property_local_coords>`

.. rst-class:: classref-property-setget

- |void| **set_use_local_coordinates**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_local_coordinates**\ (\ )

Nếu ``true``, particle sử dụng không gian tọa độ của node cha (được gọi là tọa độ cục bộ). Điều này khiến particle di chuyển và xoay theo node **GPUParticles2D** (và các node cha của nó) khi node này được di chuyển hoặc xoay. Nếu ``false``, particle sử dụng tọa độ toàn cục; chúng sẽ không di chuyển hoặc xoay theo node **GPUParticles2D** (và các node cha của nó) khi node này được di chuyển hoặc xoay.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_one_shot:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **one_shot** = ``false`` :ref:`🔗<class_GPUParticles2D_property_one_shot>`

.. rst-class:: classref-property-setget

- |void| **set_one_shot**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_one_shot**\ (\ )

Nếu ``true``, chỉ có một chu kỳ phát diễn ra. Nếu được đặt thành ``true`` trong một chu kỳ, quá trình phát sẽ dừng khi chu kỳ kết thúc.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_preprocess:

.. rst-class:: classref-property

:ref:`float<class_float>` **preprocess** = ``0.0`` :ref:`🔗<class_GPUParticles2D_property_preprocess>`

.. rst-class:: classref-property-setget

- |void| **set_pre_process_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pre_process_time**\ (\ )

Hệ thống particle bắt đầu như thể nó đã chạy trong khoảng thời gian này tính bằng giây.

\ **Lưu ý:** Việc này có thể rất tốn tài nguyên nếu đặt một giá trị cao, vì nó yêu cầu chạy particle shader số lần bằng :ref:`fixed_fps<class_GPUParticles2D_property_fixed_fps>` (hoặc 30 nếu :ref:`fixed_fps<class_GPUParticles2D_property_fixed_fps>` bằng 0) cho mỗi giây. Trong những trường hợp cực đoan, việc này thậm chí có thể khiến GPU bị crash do khối lượng công việc được thực hiện trong một frame đơn lẻ.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_process_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **process_material** :ref:`🔗<class_GPUParticles2D_property_process_material>`

.. rst-class:: classref-property-setget

- |void| **set_process_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_process_material**\ (\ )

:ref:`Material<class_Material>` dùng để xử lý particle. Có thể là một :ref:`ParticleProcessMaterial<class_ParticleProcessMaterial>` hoặc một :ref:`ShaderMaterial<class_ShaderMaterial>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_randomness:

.. rst-class:: classref-property

:ref:`float<class_float>` **randomness** = ``0.0`` :ref:`🔗<class_GPUParticles2D_property_randomness>`

.. rst-class:: classref-property-setget

- |void| **set_randomness_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_randomness_ratio**\ (\ )

Tỷ lệ ngẫu nhiên của thời gian sống khi phát.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_seed:

.. rst-class:: classref-property

:ref:`int<class_int>` **seed** = ``0`` :ref:`🔗<class_GPUParticles2D_property_seed>`

.. rst-class:: classref-property-setget

- |void| **set_seed**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_seed**\ (\ )

Đặt seed ngẫu nhiên được hệ thống particle sử dụng. Chỉ có hiệu lực nếu :ref:`use_fixed_seed<class_GPUParticles2D_property_use_fixed_seed>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **speed_scale** = ``1.0`` :ref:`🔗<class_GPUParticles2D_property_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_speed_scale**\ (\ )

Tỷ lệ điều chỉnh tốc độ chạy của hệ thống particle. Có thể sử dụng giá trị ``0`` để tạm dừng các particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_sub_emitter:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **sub_emitter** = ``NodePath("")`` :ref:`🔗<class_GPUParticles2D_property_sub_emitter>`

.. rst-class:: classref-property-setget

- |void| **set_sub_emitter**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_sub_emitter**\ (\ )

Đường dẫn đến một node **GPUParticles2D** khác sẽ được sử dụng làm subemitter (xem :ref:`ParticleProcessMaterial.sub_emitter_mode<class_ParticleProcessMaterial_property_sub_emitter_mode>`). Subemitter có thể được dùng để tạo các hiệu ứng như pháo hoa, tia lửa khi va chạm, bong bóng vỡ thành giọt nước và nhiều hiệu ứng khác.

\ **Lưu ý:** Khi :ref:`sub_emitter<class_GPUParticles2D_property_sub_emitter>` được đặt, node **GPUParticles2D** đích sẽ không còn tự phát particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_GPUParticles2D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

Texture của particle. Nếu ``null``, particle sẽ là các hình vuông có kích thước 1×1 pixel.

\ **Lưu ý:** Để sử dụng texture flipbook, hãy gán một :ref:`CanvasItemMaterial<class_CanvasItemMaterial>` mới cho thuộc tính :ref:`CanvasItem.material<class_CanvasItem_property_material>` của **GPUParticles2D**, sau đó bật :ref:`CanvasItemMaterial.particles_animation<class_CanvasItemMaterial_property_particles_animation>` và đặt :ref:`CanvasItemMaterial.particles_anim_h_frames<class_CanvasItemMaterial_property_particles_anim_h_frames>`, :ref:`CanvasItemMaterial.particles_anim_v_frames<class_CanvasItemMaterial_property_particles_anim_v_frames>` cùng :ref:`CanvasItemMaterial.particles_anim_loop<class_CanvasItemMaterial_property_particles_anim_loop>` cho khớp với texture flipbook.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_trail_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **trail_enabled** = ``false`` :ref:`🔗<class_GPUParticles2D_property_trail_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_trail_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_trail_enabled**\ (\ )

Nếu ``true``, bật trail của particle bằng hệ thống mesh skinning.

\ **Lưu ý:** Không giống :ref:`GPUParticles3D<class_GPUParticles3D>`, số lượng phần trail và subdivision được đặt bằng các thuộc tính :ref:`trail_sections<class_GPUParticles2D_property_trail_sections>` và :ref:`trail_section_subdivisions<class_GPUParticles2D_property_trail_section_subdivisions>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_trail_lifetime:

.. rst-class:: classref-property

:ref:`float<class_float>` **trail_lifetime** = ``0.3`` :ref:`🔗<class_GPUParticles2D_property_trail_lifetime>`

.. rst-class:: classref-property-setget

- |void| **set_trail_lifetime**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_trail_lifetime**\ (\ )

Khoảng thời gian mà trail của particle biểu thị (tính bằng giây). Chỉ có hiệu lực nếu :ref:`trail_enabled<class_GPUParticles2D_property_trail_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_trail_section_subdivisions:

.. rst-class:: classref-property

:ref:`int<class_int>` **trail_section_subdivisions** = ``4`` :ref:`🔗<class_GPUParticles2D_property_trail_section_subdivisions>`

.. rst-class:: classref-property-setget

- |void| **set_trail_section_subdivisions**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_trail_section_subdivisions**\ (\ )

Số lượng subdivision được sử dụng để render trail của particle. Giá trị cao hơn có thể tạo ra các đường cong trail mượt hơn, nhưng làm giảm hiệu năng do độ phức tạp của mesh tăng lên. Xem thêm :ref:`trail_sections<class_GPUParticles2D_property_trail_sections>`. Chỉ có hiệu lực nếu :ref:`trail_enabled<class_GPUParticles2D_property_trail_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_trail_sections:

.. rst-class:: classref-property

:ref:`int<class_int>` **trail_sections** = ``8`` :ref:`🔗<class_GPUParticles2D_property_trail_sections>`

.. rst-class:: classref-property-setget

- |void| **set_trail_sections**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_trail_sections**\ (\ )

Số lượng phần được sử dụng để render trail của particle. Giá trị cao hơn có thể tạo ra các đường cong trail mượt hơn, nhưng làm giảm hiệu năng do độ phức tạp của mesh tăng lên. Xem thêm :ref:`trail_section_subdivisions<class_GPUParticles2D_property_trail_section_subdivisions>`. Chỉ có hiệu lực nếu :ref:`trail_enabled<class_GPUParticles2D_property_trail_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_use_fixed_seed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_fixed_seed** = ``false`` :ref:`🔗<class_GPUParticles2D_property_use_fixed_seed>`

.. rst-class:: classref-property-setget

- |void| **set_use_fixed_seed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_fixed_seed**\ (\ )

Nếu ``true``, particle sẽ sử dụng cùng một seed cho mọi lần mô phỏng, bằng seed được xác định trong :ref:`seed<class_GPUParticles2D_property_seed>`. Điều này hữu ích trong các trường hợp kết quả hình ảnh cần nhất quán giữa các lần phát lại, chẳng hạn khi sử dụng chế độ Movie Maker.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_property_visibility_rect:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **visibility_rect** = ``Rect2(-100, -100, 200, 200)`` :ref:`🔗<class_GPUParticles2D_property_visibility_rect>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_rect**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_visibility_rect**\ (\ )

:ref:`Rect2<class_Rect2>` xác định vùng của node cần hiển thị trên màn hình để hệ thống particle hoạt động.

Hãy mở rộng hình chữ nhật nếu particle đột nhiên xuất hiện/biến mất khi node đi vào/rời khỏi màn hình. Có thể mở rộng :ref:`Rect2<class_Rect2>` bằng code hoặc bằng công cụ editor **Particles → Generate Visibility Rect**.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GPUParticles2D_method_capture_rect:

.. rst-class:: classref-method

:ref:`Rect2<class_Rect2>` **capture_rect**\ (\ ) |const| :ref:`🔗<class_GPUParticles2D_method_capture_rect>`

Trả về một hình chữ nhật chứa vị trí của tất cả particle hiện có.

\ **Lưu ý:** Khi sử dụng threaded rendering, phương thức này sẽ đồng bộ rendering thread. Việc gọi phương thức thường xuyên có thể ảnh hưởng tiêu cực đến hiệu năng.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_method_convert_from_particles:

.. rst-class:: classref-method

|void| **convert_from_particles**\ (\ particles\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_GPUParticles2D_method_convert_from_particles>`

Đặt các thuộc tính của node này để khớp với một node :ref:`CPUParticles2D<class_CPUParticles2D>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_method_emit_particle:

.. rst-class:: classref-method

|void| **emit_particle**\ (\ xform\: :ref:`Transform2D<class_Transform2D>`, velocity\: :ref:`Vector2<class_Vector2>`, color\: :ref:`Color<class_Color>`, custom\: :ref:`Color<class_Color>`, flags\: :ref:`int<class_int>`\ ) :ref:`🔗<class_GPUParticles2D_method_emit_particle>`

Việc phát một particle đơn lẻ, cũng như việc ``xform``, ``velocity``, ``color`` và ``custom`` có được áp dụng hay không, phụ thuộc vào giá trị của ``flags``. Xem :ref:`EmitFlags<enum_GPUParticles2D_EmitFlags>`.

ParticleProcessMaterial mặc định sẽ ghi đè ``color`` và sử dụng nội dung của ``custom`` làm ``(rotation, age, animation, lifetime)``.

\ **Lưu ý:** :ref:`emit_particle()<class_GPUParticles2D_method_emit_particle>` chỉ được hỗ trợ trên các phương thức rendering Forward+ và Mobile, không được hỗ trợ trên Compatibility.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_method_request_particles_process:

.. rst-class:: classref-method

|void| **request_particles_process**\ (\ process_time\: :ref:`float<class_float>`, process_time_residual\: :ref:`float<class_float>` = 0\ ) :ref:`🔗<class_GPUParticles2D_method_request_particles_process>`

Yêu cầu particle xử lý thêm trong khoảng thời gian xử lý bổ sung trong một frame đơn lẻ.

\ ``process_time`` xác định khoảng thời gian particle sẽ xử lý khi đang bật phát. ``process_time_residual`` xác định khoảng thời gian particle sẽ xử lý khi đã tắt phát trong mô phỏng. Khi kết hợp với :ref:`speed_scale<class_GPUParticles2D_property_speed_scale>` được đặt thành ``0.0``, tùy chọn này hữu ích để tua đến một thời điểm trong timeline của hệ thống particle.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticles2D_method_restart:

.. rst-class:: classref-method

|void| **restart**\ (\ keep_seed\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_GPUParticles2D_method_restart>`

Khởi động lại chu kỳ phát hạt, xóa các hạt hiện có. Để tránh các hạt biến mất khỏi viewport, hãy đợi tín hiệu :ref:`finished<class_GPUParticles2D_signal_finished>` trước khi gọi.

\ **Lưu ý:** Tín hiệu :ref:`finished<class_GPUParticles2D_signal_finished>` chỉ được phát ra bởi các emitter :ref:`one_shot<class_GPUParticles2D_property_one_shot>`.

Nếu ``keep_seed`` là ``true``, seed ngẫu nhiên hiện tại sẽ được giữ lại. Hữu ích khi tua và phát lại.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
