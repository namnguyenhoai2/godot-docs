:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CharacterBody2D.xml.

.. _class_CharacterBody2D:

CharacterBody2D
===============

**Kế thừa:** :ref:`PhysicsBody2D<class_PhysicsBody2D>` **<** :ref:`CollisionObject2D<class_CollisionObject2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics body 2D chuyên biệt dành cho các nhân vật được di chuyển bằng script.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CharacterBody2D** là một class chuyên biệt dành cho các physics body được điều khiển bởi người dùng. Chúng hoàn toàn không chịu tác động của physics, nhưng tác động đến các physics body khác trên đường đi. Chúng chủ yếu được dùng để cung cấp API cấp cao nhằm di chuyển các đối tượng với khả năng phát hiện tường và slope (phương thức :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`) bên cạnh khả năng phát hiện va chạm chung do :ref:`PhysicsBody2D.move_and_collide()<class_PhysicsBody2D_method_move_and_collide>` cung cấp. Điều này khiến chúng hữu ích cho các physics body có khả năng cấu hình cao, cần di chuyển theo những cách cụ thể và va chạm với thế giới, như thường thấy ở các nhân vật do người dùng điều khiển.

Đối với các đối tượng trong game không yêu cầu chuyển động hoặc phát hiện va chạm phức tạp, chẳng hạn như moving platform, :ref:`AnimatableBody2D<class_AnimatableBody2D>` sẽ dễ cấu hình hơn.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Physics introduction <../tutorials/physics/physics_introduction>`

- :doc:`Troubleshooting physics issues <../tutorials/physics/troubleshooting_physics_issues>`

- :doc:`Kinematic character (2D) <../tutorials/physics/kinematic_character_2d>`

- :doc:`Using CharacterBody2D <../tutorials/physics/using_character_body_2d>`

- `2D Kinematic Character Demo <https://godotengine.org/asset-library/asset/2719>`__

- `2D Platformer Demo <https://godotengine.org/asset-library/asset/2727>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`floor_block_on_wall<class_CharacterBody2D_property_floor_block_on_wall>`     | ``true``           |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`floor_constant_speed<class_CharacterBody2D_property_floor_constant_speed>`   | ``false``          |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`float<class_float>`                                    | :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>`             | ``0.7853982``      |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`float<class_float>`                                    | :ref:`floor_snap_length<class_CharacterBody2D_property_floor_snap_length>`         | ``1.0``            |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`floor_stop_on_slope<class_CharacterBody2D_property_floor_stop_on_slope>`     | ``true``           |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`int<class_int>`                                        | :ref:`max_slides<class_CharacterBody2D_property_max_slides>`                       | ``4``              |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`MotionMode<enum_CharacterBody2D_MotionMode>`           | :ref:`motion_mode<class_CharacterBody2D_property_motion_mode>`                     | ``0``              |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`int<class_int>`                                        | :ref:`platform_floor_layers<class_CharacterBody2D_property_platform_floor_layers>` | ``4294967295``     |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>` | :ref:`platform_on_leave<class_CharacterBody2D_property_platform_on_leave>`         | ``0``              |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`int<class_int>`                                        | :ref:`platform_wall_layers<class_CharacterBody2D_property_platform_wall_layers>`   | ``0``              |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`float<class_float>`                                    | :ref:`safe_margin<class_CharacterBody2D_property_safe_margin>`                     | ``0.08``           |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`slide_on_ceiling<class_CharacterBody2D_property_slide_on_ceiling>`           | ``true``           |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`up_direction<class_CharacterBody2D_property_up_direction>`                   | ``Vector2(0, -1)`` |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`Vector2<class_Vector2>`                                | :ref:`velocity<class_CharacterBody2D_property_velocity>`                           | ``Vector2(0, 0)``  |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+
   | :ref:`float<class_float>`                                    | :ref:`wall_min_slide_angle<class_CharacterBody2D_property_wall_min_slide_angle>`   | ``0.2617994``      |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+--------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`apply_floor_snap<class_CharacterBody2D_method_apply_floor_snap>`\ (\ )                                                                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                               | :ref:`get_floor_angle<class_CharacterBody2D_method_get_floor_angle>`\ (\ up_direction\: :ref:`Vector2<class_Vector2>` = Vector2(0, -1)\ ) |const| |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                           | :ref:`get_floor_normal<class_CharacterBody2D_method_get_floor_normal>`\ (\ ) |const|                                                              |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                           | :ref:`get_last_motion<class_CharacterBody2D_method_get_last_motion>`\ (\ ) |const|                                                                |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`KinematicCollision2D<class_KinematicCollision2D>` | :ref:`get_last_slide_collision<class_CharacterBody2D_method_get_last_slide_collision>`\ (\ )                                                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                           | :ref:`get_platform_velocity<class_CharacterBody2D_method_get_platform_velocity>`\ (\ ) |const|                                                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                           | :ref:`get_position_delta<class_CharacterBody2D_method_get_position_delta>`\ (\ ) |const|                                                          |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                           | :ref:`get_real_velocity<class_CharacterBody2D_method_get_real_velocity>`\ (\ ) |const|                                                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`KinematicCollision2D<class_KinematicCollision2D>` | :ref:`get_slide_collision<class_CharacterBody2D_method_get_slide_collision>`\ (\ slide_idx\: :ref:`int<class_int>`\ )                             |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                   | :ref:`get_slide_collision_count<class_CharacterBody2D_method_get_slide_collision_count>`\ (\ ) |const|                                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                           | :ref:`get_wall_normal<class_CharacterBody2D_method_get_wall_normal>`\ (\ ) |const|                                                                |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`is_on_ceiling<class_CharacterBody2D_method_is_on_ceiling>`\ (\ ) |const|                                                                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`is_on_ceiling_only<class_CharacterBody2D_method_is_on_ceiling_only>`\ (\ ) |const|                                                          |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`is_on_floor<class_CharacterBody2D_method_is_on_floor>`\ (\ ) |const|                                                                        |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`is_on_floor_only<class_CharacterBody2D_method_is_on_floor_only>`\ (\ ) |const|                                                              |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`is_on_wall<class_CharacterBody2D_method_is_on_wall>`\ (\ ) |const|                                                                          |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`is_on_wall_only<class_CharacterBody2D_method_is_on_wall_only>`\ (\ ) |const|                                                                |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                 | :ref:`move_and_slide<class_CharacterBody2D_method_move_and_slide>`\ (\ )                                                                          |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CharacterBody2D_MotionMode:

.. rst-class:: classref-enumeration

enum **MotionMode**: :ref:`🔗<enum_CharacterBody2D_MotionMode>`

.. _class_CharacterBody2D_constant_MOTION_MODE_GROUNDED:

.. rst-class:: classref-enumeration-constant

:ref:`MotionMode<enum_CharacterBody2D_MotionMode>` **MOTION_MODE_GROUNDED** = ``0``

Áp dụng khi các khái niệm về tường, trần và sàn có liên quan. Ở chế độ này, chuyển động của body sẽ phản ứng với các slope (tăng tốc/giảm tốc). Chế độ này phù hợp với các game dạng màn hình ngang như platformer.

.. _class_CharacterBody2D_constant_MOTION_MODE_FLOATING:

.. rst-class:: classref-enumeration-constant

:ref:`MotionMode<enum_CharacterBody2D_MotionMode>` **MOTION_MODE_FLOATING** = ``1``

Áp dụng khi không có khái niệm về sàn hoặc trần. Tất cả va chạm sẽ được báo cáo là ``on_wall``. Ở chế độ này, khi trượt, tốc độ sẽ luôn không đổi. Chế độ này phù hợp với các game góc nhìn từ trên xuống.

.. rst-class:: classref-item-separator

----

.. _enum_CharacterBody2D_PlatformOnLeave:

.. rst-class:: classref-enumeration

enum **PlatformOnLeave**: :ref:`🔗<enum_CharacterBody2D_PlatformOnLeave>`

.. _class_CharacterBody2D_constant_PLATFORM_ON_LEAVE_ADD_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>` **PLATFORM_ON_LEAVE_ADD_VELOCITY** = ``0``

Cộng vận tốc cuối cùng của platform vào :ref:`velocity<class_CharacterBody2D_property_velocity>` khi bạn rời khỏi một moving platform.

.. _class_CharacterBody2D_constant_PLATFORM_ON_LEAVE_ADD_UPWARD_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>` **PLATFORM_ON_LEAVE_ADD_UPWARD_VELOCITY** = ``1``

Cộng vận tốc cuối cùng của platform vào :ref:`velocity<class_CharacterBody2D_property_velocity>` khi bạn rời khỏi một moving platform, nhưng bỏ qua mọi chuyển động hướng xuống. Điều này hữu ích để duy trì độ cao nhảy tối đa ngay cả khi platform đang di chuyển xuống.

.. _class_CharacterBody2D_constant_PLATFORM_ON_LEAVE_DO_NOTHING:

.. rst-class:: classref-enumeration-constant

:ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>` **PLATFORM_ON_LEAVE_DO_NOTHING** = ``2``

Không làm gì khi rời khỏi một platform.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CharacterBody2D_property_floor_block_on_wall:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **floor_block_on_wall** = ``true`` :ref:`🔗<class_CharacterBody2D_property_floor_block_on_wall>`

.. rst-class:: classref-property-setget

- |void| **set_floor_block_on_wall_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_floor_block_on_wall_enabled**\ (\ )

Nếu ``true``, body sẽ chỉ có thể di chuyển trên sàn. Tùy chọn này ngăn body đi trên tường, tuy nhiên vẫn cho phép body trượt xuống dọc theo tường.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_floor_constant_speed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **floor_constant_speed** = ``false`` :ref:`🔗<class_CharacterBody2D_property_floor_constant_speed>`

.. rst-class:: classref-property-setget

- |void| **set_floor_constant_speed_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_floor_constant_speed_enabled**\ (\ )

Nếu ``false`` (theo mặc định), body sẽ di chuyển nhanh hơn trên các slope hướng xuống và chậm hơn trên các slope hướng lên.

Nếu ``true``, body sẽ luôn di chuyển với cùng tốc độ trên mặt đất bất kể slope. Lưu ý rằng bạn cần dùng :ref:`floor_snap_length<class_CharacterBody2D_property_floor_snap_length>` để bám dọc theo một slope hướng xuống với tốc độ không đổi.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_floor_max_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **floor_max_angle** = ``0.7853982`` :ref:`🔗<class_CharacterBody2D_property_floor_max_angle>`

.. rst-class:: classref-property-setget

- |void| **set_floor_max_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_floor_max_angle**\ (\ )

Góc tối đa (tính bằng radian) mà tại đó một slope vẫn được xem là sàn (hoặc trần), thay vì tường, khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`. Giá trị mặc định bằng 45 độ.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_floor_snap_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **floor_snap_length** = ``1.0`` :ref:`🔗<class_CharacterBody2D_property_floor_snap_length>`

.. rst-class:: classref-property-setget

- |void| **set_floor_snap_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_floor_snap_length**\ (\ )

Thiết lập khoảng cách snap. Khi được đặt thành một giá trị khác ``0.0``, body sẽ được giữ bám vào các slope khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`. Vector snap được xác định bởi khoảng cách đã cho theo hướng ngược lại với :ref:`up_direction<class_CharacterBody2D_property_up_direction>`.

Miễn là vector snap tiếp xúc với mặt đất và body di chuyển ngược với :ref:`up_direction<class_CharacterBody2D_property_up_direction>`, body sẽ vẫn bám vào bề mặt. Snap không được áp dụng nếu body di chuyển theo :ref:`up_direction<class_CharacterBody2D_property_up_direction>`, nghĩa là nó có vận tốc hướng lên theo phương dọc, vì vậy body có thể tách khỏi mặt đất khi nhảy hoặc khi bị vật gì đó đẩy lên. Nếu muốn áp dụng snap mà không xét đến vận tốc, hãy dùng :ref:`apply_floor_snap()<class_CharacterBody2D_method_apply_floor_snap>`.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_floor_stop_on_slope:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **floor_stop_on_slope** = ``true`` :ref:`🔗<class_CharacterBody2D_property_floor_stop_on_slope>`

.. rst-class:: classref-property-setget

- |void| **set_floor_stop_on_slope_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_floor_stop_on_slope_enabled**\ (\ )

Nếu ``true``, body sẽ không trượt trên các slope khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` trong lúc body đang đứng yên.

Nếu ``false``, body sẽ trượt trên các slope của sàn khi :ref:`velocity<class_CharacterBody2D_property_velocity>` tác dụng một lực hướng xuống.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_max_slides:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_slides** = ``4`` :ref:`🔗<class_CharacterBody2D_property_max_slides>`

.. rst-class:: classref-property-setget

- |void| **set_max_slides**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_slides**\ (\ )

Số lần tối đa body có thể đổi hướng trước khi dừng lại khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`. Phải lớn hơn không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_motion_mode:

.. rst-class:: classref-property

:ref:`MotionMode<enum_CharacterBody2D_MotionMode>` **motion_mode** = ``0`` :ref:`🔗<class_CharacterBody2D_property_motion_mode>`

.. rst-class:: classref-property-setget

- |void| **set_motion_mode**\ (\ value\: :ref:`MotionMode<enum_CharacterBody2D_MotionMode>`\ ) - :ref:`MotionMode<enum_CharacterBody2D_MotionMode>` **get_motion_mode**\ (\ )

Thiết lập motion mode xác định hành vi của :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_platform_floor_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **platform_floor_layers** = ``4294967295`` :ref:`🔗<class_CharacterBody2D_property_platform_floor_layers>`

.. rst-class:: classref-property-setget

- |void| **set_platform_floor_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_platform_floor_layers**\ (\ )

Các collision layer sẽ được đưa vào để phát hiện những floor body hoạt động như moving platform mà **CharacterBody2D** sẽ đi theo. Theo mặc định, tất cả floor body đều được phát hiện và truyền vận tốc của chúng.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_platform_on_leave:

.. rst-class:: classref-property

:ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>` **platform_on_leave** = ``0`` :ref:`🔗<class_CharacterBody2D_property_platform_on_leave>`

.. rst-class:: classref-property-setget

- |void| **set_platform_on_leave**\ (\ value\: :ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>`\ ) - :ref:`PlatformOnLeave<enum_CharacterBody2D_PlatformOnLeave>` **get_platform_on_leave**\ (\ )

Thiết lập hành vi cần áp dụng khi bạn rời khỏi một moving platform. Theo mặc định, để đảm bảo chính xác về mặt vật lý, vận tốc của platform cuối cùng sẽ được áp dụng khi bạn rời đi.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_platform_wall_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **platform_wall_layers** = ``0`` :ref:`🔗<class_CharacterBody2D_property_platform_wall_layers>`

.. rst-class:: classref-property-setget

- |void| **set_platform_wall_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_platform_wall_layers**\ (\ )

Các collision layer sẽ được đưa vào để phát hiện những wall body hoạt động như moving platform mà **CharacterBody2D** sẽ đi theo. Theo mặc định, tất cả wall body đều bị bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_safe_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **safe_margin** = ``0.08`` :ref:`🔗<class_CharacterBody2D_property_safe_margin>`

.. rst-class:: classref-property-setget

- |void| **set_safe_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_safe_margin**\ (\ )

Margin bổ sung được dùng để khôi phục va chạm khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`.

Nếu body ở cách một body khác ít nhất khoảng cách này, nó sẽ xem hai body đang va chạm và bị đẩy ra trước khi thực hiện chuyển động thực tế.

Giá trị cao hơn có nghĩa là việc phát hiện va chạm linh hoạt hơn, giúp phát hiện tường và sàn một cách nhất quán.

Giá trị thấp hơn buộc thuật toán va chạm sử dụng phương pháp phát hiện chính xác hơn, vì vậy có thể dùng trong các trường hợp đặc biệt yêu cầu độ chính xác, chẳng hạn như ở scale rất thấp để tránh hiện tượng rung thấy rõ, hoặc để đảm bảo tính ổn định với một chồng character body.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_slide_on_ceiling:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **slide_on_ceiling** = ``true`` :ref:`🔗<class_CharacterBody2D_property_slide_on_ceiling>`

.. rst-class:: classref-property-setget

- |void| **set_slide_on_ceiling_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_slide_on_ceiling_enabled**\ (\ )

Nếu ``true``, body sẽ trượt khi nhảy lên và va vào trần; nếu ``false``, body sẽ dừng lại và rơi thẳng đứng.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_up_direction:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **up_direction** = ``Vector2(0, -1)`` :ref:`🔗<class_CharacterBody2D_property_up_direction>`

.. rst-class:: classref-property-setget

- |void| **set_up_direction**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_up_direction**\ (\ )

Vector hướng lên, được dùng để xác định đâu là tường và đâu là sàn (hoặc trần) khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`. Mặc định là :ref:`Vector2.UP<class_Vector2_constant_UP>`. Vì vector sẽ được chuẩn hóa nên không thể bằng :ref:`Vector2.ZERO<class_Vector2_constant_ZERO>`; nếu muốn tất cả va chạm được báo cáo là tường, hãy cân nhắc dùng :ref:`MOTION_MODE_FLOATING<class_CharacterBody2D_constant_MOTION_MODE_FLOATING>` làm :ref:`motion_mode<class_CharacterBody2D_property_motion_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_CharacterBody2D_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_velocity**\ (\ )

Vector vận tốc hiện tại tính bằng pixel trên giây, được sử dụng và sửa đổi trong các lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`.

\ **Lưu ý:** Một lỗi phổ biến là đặt thuộc tính này thành vận tốc mong muốn nhân với ``delta``, tạo ra một vector chuyển động tính bằng pixel.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_property_wall_min_slide_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **wall_min_slide_angle** = ``0.2617994`` :ref:`🔗<class_CharacterBody2D_property_wall_min_slide_angle>`

.. rst-class:: classref-property-setget

- |void| **set_wall_min_slide_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_wall_min_slide_angle**\ (\ )

Góc tối thiểu (tính bằng radian) mà body được phép trượt khi gặp tường. Giá trị mặc định bằng 15 độ. Thuộc tính này chỉ ảnh hưởng đến chuyển động khi :ref:`motion_mode<class_CharacterBody2D_property_motion_mode>` là :ref:`MOTION_MODE_FLOATING<class_CharacterBody2D_constant_MOTION_MODE_FLOATING>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CharacterBody2D_method_apply_floor_snap:

.. rst-class:: classref-method

|void| **apply_floor_snap**\ (\ ) :ref:`🔗<class_CharacterBody2D_method_apply_floor_snap>`

Cho phép áp dụng snap vào sàn theo cách thủ công bất kể vận tốc của body. Hàm này không làm gì khi :ref:`is_on_floor()<class_CharacterBody2D_method_is_on_floor>` trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_floor_angle:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_floor_angle**\ (\ up_direction\: :ref:`Vector2<class_Vector2>` = Vector2(0, -1)\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_floor_angle>`

Trả về góc va chạm của sàn tại điểm va chạm gần nhất theo ``up_direction``, mặc định là :ref:`Vector2.UP<class_Vector2_constant_UP>`. Giá trị này luôn dương và chỉ hợp lệ sau khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` và khi :ref:`is_on_floor()<class_CharacterBody2D_method_is_on_floor>` trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_floor_normal:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_floor_normal**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_floor_normal>`

Trả về pháp tuyến va chạm của sàn tại điểm va chạm gần nhất. Chỉ hợp lệ sau khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` và khi :ref:`is_on_floor()<class_CharacterBody2D_method_is_on_floor>` trả về ``true``.

\ **Warning:** Pháp tuyến va chạm không phải lúc nào cũng giống pháp tuyến bề mặt.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_last_motion:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_last_motion**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_last_motion>`

Trả về chuyển động gần nhất được áp dụng cho **CharacterBody2D** trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Chuyển động có thể được chia thành nhiều chuyển động khi xảy ra trượt, và phương thức này trả về chuyển động cuối cùng, hữu ích để lấy hướng hiện tại của chuyển động.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_last_slide_collision:

.. rst-class:: classref-method

:ref:`KinematicCollision2D<class_KinematicCollision2D>` **get_last_slide_collision**\ (\ ) :ref:`🔗<class_CharacterBody2D_method_get_last_slide_collision>`

Trả về một :ref:`KinematicCollision2D<class_KinematicCollision2D>` nếu xảy ra va chạm. Giá trị trả về chứa thông tin về va chạm gần nhất xảy ra trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Trả về ``null`` nếu không xảy ra va chạm. Xem thêm :ref:`get_slide_collision()<class_CharacterBody2D_method_get_slide_collision>`.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_platform_velocity:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_platform_velocity**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_platform_velocity>`

Trả về vận tốc tuyến tính của nền tảng tại điểm va chạm gần nhất. Chỉ hợp lệ sau khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_position_delta:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_position_delta**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_position_delta>`

Trả về quãng đường di chuyển (độ dịch vị trí) xảy ra trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_real_velocity:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_real_velocity**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_real_velocity>`

Trả về vận tốc thực tế hiện tại kể từ lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Ví dụ, khi bạn đi lên một dốc, bạn sẽ di chuyển theo đường chéo dù vận tốc là theo phương ngang. Phương thức này trả về chuyển động theo đường chéo, trái với :ref:`velocity<class_CharacterBody2D_property_velocity>`, vốn trả về vận tốc được yêu cầu.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_slide_collision:

.. rst-class:: classref-method

:ref:`KinematicCollision2D<class_KinematicCollision2D>` **get_slide_collision**\ (\ slide_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CharacterBody2D_method_get_slide_collision>`

Trả về một :ref:`KinematicCollision2D<class_KinematicCollision2D>`, chứa thông tin về một va chạm xảy ra trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Vì body có thể va chạm nhiều lần trong một lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>`, bạn phải chỉ định chỉ mục của va chạm trong phạm vi từ 0 đến (:ref:`get_slide_collision_count()<class_CharacterBody2D_method_get_slide_collision_count>` - 1). Xem thêm :ref:`get_last_slide_collision()<class_CharacterBody2D_method_get_last_slide_collision>`.

\ **Example:** Duyệt qua các va chạm bằng vòng lặp ``for``:


.. tabs::

 .. code-tab:: gdscript

    for i in get_slide_collision_count():
        var collision = get_slide_collision(i)
        print("Collided with: ", collision.get_collider().name)

 .. code-tab:: csharp

    for (int i = 0; i < GetSlideCollisionCount(); i++)
    {
        KinematicCollision2D collision = GetSlideCollision(i);
        GD.Print("Collided with: ", (collision.GetCollider() as Node).Name);
    }



.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_slide_collision_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_slide_collision_count**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_slide_collision_count>`

Trả về số lần body va chạm và đổi hướng trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_get_wall_normal:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_wall_normal**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_get_wall_normal>`

Trả về pháp tuyến va chạm của tường tại điểm va chạm gần nhất. Chỉ hợp lệ sau khi gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` và khi :ref:`is_on_wall()<class_CharacterBody2D_method_is_on_wall>` trả về ``true``.

\ **Warning:** Pháp tuyến va chạm không phải lúc nào cũng giống pháp tuyến bề mặt.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_is_on_ceiling:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_on_ceiling**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_is_on_ceiling>`

Trả về ``true`` nếu body va chạm với trần trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Nếu không, trả về ``false``. :ref:`up_direction<class_CharacterBody2D_property_up_direction>` và :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>` được dùng để xác định một bề mặt có phải là "ceiling" hay không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_is_on_ceiling_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_on_ceiling_only**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_is_on_ceiling_only>`

Trả về ``true`` nếu body chỉ va chạm với trần trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Nếu không, trả về ``false``. :ref:`up_direction<class_CharacterBody2D_property_up_direction>` và :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>` được dùng để xác định một bề mặt có phải là "ceiling" hay không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_is_on_floor:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_on_floor**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_is_on_floor>`

Trả về ``true`` nếu body va chạm với sàn trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Nếu không, trả về ``false``. :ref:`up_direction<class_CharacterBody2D_property_up_direction>` và :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>` được dùng để xác định một bề mặt có phải là "floor" hay không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_is_on_floor_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_on_floor_only**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_is_on_floor_only>`

Trả về ``true`` nếu body chỉ va chạm với sàn trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Nếu không, trả về ``false``. :ref:`up_direction<class_CharacterBody2D_property_up_direction>` và :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>` được dùng để xác định một bề mặt có phải là "floor" hay không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_is_on_wall:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_on_wall**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_is_on_wall>`

Trả về ``true`` nếu body va chạm với tường trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Nếu không, trả về ``false``. :ref:`up_direction<class_CharacterBody2D_property_up_direction>` và :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>` được dùng để xác định một bề mặt có phải là "wall" hay không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_is_on_wall_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_on_wall_only**\ (\ ) |const| :ref:`🔗<class_CharacterBody2D_method_is_on_wall_only>`

Trả về ``true`` nếu body chỉ va chạm với tường trong lần gọi :ref:`move_and_slide()<class_CharacterBody2D_method_move_and_slide>` gần nhất. Nếu không, trả về ``false``. :ref:`up_direction<class_CharacterBody2D_property_up_direction>` và :ref:`floor_max_angle<class_CharacterBody2D_property_floor_max_angle>` được dùng để xác định một bề mặt có phải là "wall" hay không.

.. rst-class:: classref-item-separator

----

.. _class_CharacterBody2D_method_move_and_slide:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **move_and_slide**\ (\ ) :ref:`🔗<class_CharacterBody2D_method_move_and_slide>`

Di chuyển body dựa trên :ref:`velocity<class_CharacterBody2D_property_velocity>`. Nếu body va chạm với một body khác, nó sẽ trượt dọc theo body đó (mặc định chỉ trên sàn) thay vì dừng ngay lập tức. Nếu body kia là **CharacterBody2D** hoặc :ref:`RigidBody2D<class_RigidBody2D>`, nó cũng sẽ chịu ảnh hưởng bởi chuyển động của body kia. Bạn có thể dùng điều này để tạo các nền tảng chuyển động và xoay, hoặc để khiến các node đẩy các node khác.

Nên sử dụng phương thức này trong :ref:`Node._physics_process()<class_Node_private_method__physics_process>` (hoặc trong một phương thức được gọi bởi :ref:`Node._physics_process()<class_Node_private_method__physics_process>`), vì nó tự động sử dụng giá trị ``delta`` của bước physics trong các phép tính. Nếu không, mô phỏng sẽ chạy với tốc độ không chính xác.

Điều chỉnh :ref:`velocity<class_CharacterBody2D_property_velocity>` nếu xảy ra va chạm trượt. Để lấy va chạm gần nhất, hãy gọi :ref:`get_last_slide_collision()<class_CharacterBody2D_method_get_last_slide_collision>`; để biết thông tin chi tiết về các va chạm đã xảy ra, hãy sử dụng :ref:`get_slide_collision()<class_CharacterBody2D_method_get_slide_collision>`.

Khi body chạm vào một nền tảng đang chuyển động, vận tốc của nền tảng sẽ tự động được cộng vào chuyển động của body. Nếu xảy ra va chạm do chuyển động của nền tảng, va chạm đó luôn đứng đầu trong các va chạm trượt.

Hành vi tổng quát và các thuộc tính khả dụng thay đổi tùy theo :ref:`motion_mode<class_CharacterBody2D_property_motion_mode>`.

Trả về ``true`` nếu body va chạm; nếu không, trả về ``false``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
