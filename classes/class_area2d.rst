:github_url: hide

.. meta::
	:keywords: trigger

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Area2D.xml.

.. _class_Area2D:

Area2D
======

**Kế thừa:** :ref:`CollisionObject2D<class_CollisionObject2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

A region of 2D space that detects other :ref:`CollisionObject2D<class_CollisionObject2D>`\ s entering or exiting it.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Area2D** is a region of 2D space defined by one or multiple :ref:`CollisionShape2D<class_CollisionShape2D>` or :ref:`CollisionPolygon2D<class_CollisionPolygon2D>` child nodes. It detects when other :ref:`CollisionObject2D<class_CollisionObject2D>`\ s enter or exit it, and it also keeps track of which collision objects haven't exited it yet (i.e. which one are overlapping it).

Node này cũng có thể thay đổi hoặc ghi đè cục bộ các tham số vật lý (gravity, damping) và định tuyến âm thanh đến các audio bus tùy chỉnh.

\ **Lưu ý:** Các area và body được tạo bằng :ref:`PhysicsServer2D<class_PhysicsServer2D>` có thể không tương tác như mong đợi với **Area2D**\ s, đồng thời có thể không phát signal hoặc theo dõi đối tượng chính xác.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using Area2D <../tutorials/physics/using_area_2d>`

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

- `2D Pong Demo <https://godotengine.org/asset-library/asset/2728>`__

- `2D Platformer Demo <https://godotengine.org/asset-library/asset/2727>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                       | :ref:`angular_damp<class_Area2D_property_angular_damp>`                               | ``1.0``           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`SpaceOverride<enum_Area2D_SpaceOverride>` | :ref:`angular_damp_space_override<class_Area2D_property_angular_damp_space_override>` | ``0``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`StringName<class_StringName>`             | :ref:`audio_bus_name<class_Area2D_property_audio_bus_name>`                           | ``&"Master"``     |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                         | :ref:`audio_bus_override<class_Area2D_property_audio_bus_override>`                   | ``false``         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                       | :ref:`gravity<class_Area2D_property_gravity>`                                         | ``980.0``         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                   | :ref:`gravity_direction<class_Area2D_property_gravity_direction>`                     | ``Vector2(0, 1)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                         | :ref:`gravity_point<class_Area2D_property_gravity_point>`                             | ``false``         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                   | :ref:`gravity_point_center<class_Area2D_property_gravity_point_center>`               | ``Vector2(0, 1)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                       | :ref:`gravity_point_unit_distance<class_Area2D_property_gravity_point_unit_distance>` | ``0.0``           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`SpaceOverride<enum_Area2D_SpaceOverride>` | :ref:`gravity_space_override<class_Area2D_property_gravity_space_override>`           | ``0``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                       | :ref:`linear_damp<class_Area2D_property_linear_damp>`                                 | ``0.1``           |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`SpaceOverride<enum_Area2D_SpaceOverride>` | :ref:`linear_damp_space_override<class_Area2D_property_linear_damp_space_override>`   | ``0``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                         | :ref:`monitorable<class_Area2D_property_monitorable>`                                 | ``true``          |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                         | :ref:`monitoring<class_Area2D_property_monitoring>`                                   | ``true``          |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                           | :ref:`priority<class_Area2D_property_priority>`                                       | ``0``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Area2D<class_Area2D>`\] | :ref:`get_overlapping_areas<class_Area2D_method_get_overlapping_areas>`\ (\ ) |const|                 |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node2D<class_Node2D>`\] | :ref:`get_overlapping_bodies<class_Area2D_method_get_overlapping_bodies>`\ (\ ) |const|               |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`has_overlapping_areas<class_Area2D_method_has_overlapping_areas>`\ (\ ) |const|                 |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`has_overlapping_bodies<class_Area2D_method_has_overlapping_bodies>`\ (\ ) |const|               |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`overlaps_area<class_Area2D_method_overlaps_area>`\ (\ area\: :ref:`Node<class_Node>`\ ) |const| |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`overlaps_body<class_Area2D_method_overlaps_body>`\ (\ body\: :ref:`Node<class_Node>`\ ) |const| |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_Area2D_signal_area_entered:

.. rst-class:: classref-signal

**area_entered**\ (\ area\: :ref:`Area2D<class_Area2D>`\ ) :ref:`🔗<class_Area2D_signal_area_entered>`

Được phát khi ``area`` nhận được đi vào area này. Yêu cầu :ref:`monitoring<class_Area2D_property_monitoring>` được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_area_exited:

.. rst-class:: classref-signal

**area_exited**\ (\ area\: :ref:`Area2D<class_Area2D>`\ ) :ref:`🔗<class_Area2D_signal_area_exited>`

Được phát khi ``area`` nhận được rời khỏi area này. Yêu cầu :ref:`monitoring<class_Area2D_property_monitoring>` được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_area_shape_entered:

.. rst-class:: classref-signal

**area_shape_entered**\ (\ area_rid\: :ref:`RID<class_RID>`, area\: :ref:`Area2D<class_Area2D>`, area_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area2D_signal_area_shape_entered>`

Được phát khi một :ref:`Shape2D<class_Shape2D>` của ``area`` nhận được đi vào một shape của area này. Yêu cầu :ref:`monitoring<class_Area2D_property_monitoring>` được đặt thành ``true``.

\ ``local_shape_index`` và ``area_shape_index`` lần lượt chứa các chỉ mục của những shape tương tác từ area này và area còn lại. ``area_rid`` chứa :ref:`RID<class_RID>` của area còn lại. Có thể sử dụng các giá trị này với :ref:`PhysicsServer2D<class_PhysicsServer2D>`.

\ **Ví dụ:** Lấy node :ref:`CollisionShape2D<class_CollisionShape2D>` từ chỉ mục shape:


.. tabs::

 .. code-tab:: gdscript

    var other_shape_owner = area.shape_find_owner(area_shape_index)
    var other_shape_node = area.shape_owner_get_owner(other_shape_owner)

    var local_shape_owner = shape_find_owner(local_shape_index)
    var local_shape_node = shape_owner_get_owner(local_shape_owner)



.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_area_shape_exited:

.. rst-class:: classref-signal

**area_shape_exited**\ (\ area_rid\: :ref:`RID<class_RID>`, area\: :ref:`Area2D<class_Area2D>`, area_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area2D_signal_area_shape_exited>`

Được phát khi một :ref:`Shape2D<class_Shape2D>` của ``area`` nhận được rời khỏi một shape của area này. Yêu cầu :ref:`monitoring<class_Area2D_property_monitoring>` được đặt thành ``true``.

Xem thêm :ref:`area_shape_entered<class_Area2D_signal_area_shape_entered>`.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_body_entered:

.. rst-class:: classref-signal

**body_entered**\ (\ body\: :ref:`Node2D<class_Node2D>`\ ) :ref:`🔗<class_Area2D_signal_body_entered>`

Emitted when the received ``body`` enters this area. ``body`` can be a :ref:`PhysicsBody2D<class_PhysicsBody2D>` or a :ref:`TileMap<class_TileMap>`. :ref:`TileMap<class_TileMap>`\ s are detected if their :ref:`TileSet<class_TileSet>` has collision shapes configured. Requires :ref:`monitoring<class_Area2D_property_monitoring>` to be set to ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_body_exited:

.. rst-class:: classref-signal

**body_exited**\ (\ body\: :ref:`Node2D<class_Node2D>`\ ) :ref:`🔗<class_Area2D_signal_body_exited>`

Emitted when the received ``body`` exits this area. ``body`` can be a :ref:`PhysicsBody2D<class_PhysicsBody2D>` or a :ref:`TileMap<class_TileMap>`. :ref:`TileMap<class_TileMap>`\ s are detected if their :ref:`TileSet<class_TileSet>` has collision shapes configured. Requires :ref:`monitoring<class_Area2D_property_monitoring>` to be set to ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_body_shape_entered:

.. rst-class:: classref-signal

**body_shape_entered**\ (\ body_rid\: :ref:`RID<class_RID>`, body\: :ref:`Node2D<class_Node2D>`, body_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area2D_signal_body_shape_entered>`

Emitted when a :ref:`Shape2D<class_Shape2D>` of the received ``body`` enters a shape of this area. ``body`` can be a :ref:`PhysicsBody2D<class_PhysicsBody2D>` or a :ref:`TileMap<class_TileMap>`. :ref:`TileMap<class_TileMap>`\ s are detected if their :ref:`TileSet<class_TileSet>` has collision shapes configured. Requires :ref:`monitoring<class_Area2D_property_monitoring>` to be set to ``true``.

\ ``local_shape_index`` và ``body_shape_index`` lần lượt chứa các chỉ mục của những shape tương tác từ area này và body tương tác. ``body_rid`` chứa :ref:`RID<class_RID>` của body. Có thể sử dụng các giá trị này với :ref:`PhysicsServer2D<class_PhysicsServer2D>`.

\ **Ví dụ:** Lấy node :ref:`CollisionShape2D<class_CollisionShape2D>` từ chỉ mục shape:


.. tabs::

 .. code-tab:: gdscript

    var body_shape_owner = body.shape_find_owner(body_shape_index)
    var body_shape_node = body.shape_owner_get_owner(body_shape_owner)

    var local_shape_owner = shape_find_owner(local_shape_index)
    var local_shape_node = shape_owner_get_owner(local_shape_owner)



.. rst-class:: classref-item-separator

----

.. _class_Area2D_signal_body_shape_exited:

.. rst-class:: classref-signal

**body_shape_exited**\ (\ body_rid\: :ref:`RID<class_RID>`, body\: :ref:`Node2D<class_Node2D>`, body_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area2D_signal_body_shape_exited>`

Emitted when a :ref:`Shape2D<class_Shape2D>` of the received ``body`` exits a shape of this area. ``body`` can be a :ref:`PhysicsBody2D<class_PhysicsBody2D>` or a :ref:`TileMap<class_TileMap>`. :ref:`TileMap<class_TileMap>`\ s are detected if their :ref:`TileSet<class_TileSet>` has collision shapes configured. Requires :ref:`monitoring<class_Area2D_property_monitoring>` to be set to ``true``.

Xem thêm :ref:`body_shape_entered<class_Area2D_signal_body_shape_entered>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Area2D_SpaceOverride:

.. rst-class:: classref-enumeration

enum **SpaceOverride**: :ref:`🔗<enum_Area2D_SpaceOverride>`

.. _class_Area2D_constant_SPACE_OVERRIDE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **SPACE_OVERRIDE_DISABLED** = ``0``

Area này không ảnh hưởng đến gravity/damping.

.. _class_Area2D_constant_SPACE_OVERRIDE_COMBINE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **SPACE_OVERRIDE_COMBINE** = ``1``

Area này cộng các giá trị gravity/damping của nó vào kết quả đã được tính cho đến thời điểm hiện tại (theo thứ tự :ref:`priority<class_Area2D_property_priority>`).

.. _class_Area2D_constant_SPACE_OVERRIDE_COMBINE_REPLACE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **SPACE_OVERRIDE_COMBINE_REPLACE** = ``2``

Area này cộng các giá trị gravity/damping của nó vào kết quả đã được tính cho đến thời điểm hiện tại (theo thứ tự :ref:`priority<class_Area2D_property_priority>`), bỏ qua mọi area có độ ưu tiên thấp hơn.

.. _class_Area2D_constant_SPACE_OVERRIDE_REPLACE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **SPACE_OVERRIDE_REPLACE** = ``3``

Area này thay thế mọi gravity/damping, kể cả các giá trị mặc định, bỏ qua mọi area có độ ưu tiên thấp hơn.

.. _class_Area2D_constant_SPACE_OVERRIDE_REPLACE_COMBINE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **SPACE_OVERRIDE_REPLACE_COMBINE** = ``4``

Area này thay thế mọi gravity/damping đã được tính cho đến thời điểm hiện tại (theo thứ tự :ref:`priority<class_Area2D_property_priority>`), nhưng vẫn tiếp tục tính các area còn lại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Area2D_property_angular_damp:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_damp** = ``1.0`` :ref:`🔗<class_Area2D_property_angular_damp>`

.. rst-class:: classref-property-setget

- |void| **set_angular_damp**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angular_damp**\ (\ )

Tốc độ các đối tượng ngừng quay trong area này. Đại diện cho vận tốc góc bị mất đi mỗi giây.

Xem :ref:`ProjectSettings.physics/2d/default_angular_damp<class_ProjectSettings_property_physics/2d/default_angular_damp>` để biết thêm chi tiết về damping.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_angular_damp_space_override:

.. rst-class:: classref-property

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **angular_damp_space_override** = ``0`` :ref:`🔗<class_Area2D_property_angular_damp_space_override>`

.. rst-class:: classref-property-setget

- |void| **set_angular_damp_space_override_mode**\ (\ value\: :ref:`SpaceOverride<enum_Area2D_SpaceOverride>`\ ) - :ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **get_angular_damp_space_override_mode**\ (\ )

Chế độ ghi đè dùng cho các phép tính damping góc trong area này.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_audio_bus_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **audio_bus_name** = ``&"Master"`` :ref:`🔗<class_Area2D_property_audio_bus_name>`

.. rst-class:: classref-property-setget

- |void| **set_audio_bus_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_audio_bus_name**\ (\ )

Tên audio bus của area.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_audio_bus_override:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **audio_bus_override** = ``false`` :ref:`🔗<class_Area2D_property_audio_bus_override>`

.. rst-class:: classref-property-setget

- |void| **set_audio_bus_override**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_overriding_audio_bus**\ (\ )

Nếu ``true``, audio bus của area sẽ ghi đè audio bus mặc định.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_gravity:

.. rst-class:: classref-property

:ref:`float<class_float>` **gravity** = ``980.0`` :ref:`🔗<class_Area2D_property_gravity>`

.. rst-class:: classref-property-setget

- |void| **set_gravity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gravity**\ (\ )

Cường độ gravity của area (tính bằng pixel trên giây bình phương). Giá trị này nhân với hướng gravity. Điều này hữu ích để thay đổi lực gravity mà không thay đổi hướng của nó.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_gravity_direction:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **gravity_direction** = ``Vector2(0, 1)`` :ref:`🔗<class_Area2D_property_gravity_direction>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_direction**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_gravity_direction**\ (\ )

Vector gravity của area (chưa được chuẩn hóa).

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_gravity_point:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **gravity_point** = ``false`` :ref:`🔗<class_Area2D_property_gravity_point>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_is_point**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_gravity_a_point**\ (\ )

Nếu ``true``, gravity được tính từ một điểm (được thiết lập qua :ref:`gravity_point_center<class_Area2D_property_gravity_point_center>`). Xem thêm :ref:`gravity_space_override<class_Area2D_property_gravity_space_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_gravity_point_center:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **gravity_point_center** = ``Vector2(0, 1)`` :ref:`🔗<class_Area2D_property_gravity_point_center>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_point_center**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_gravity_point_center**\ (\ )

Nếu gravity là một điểm (xem :ref:`gravity_point<class_Area2D_property_gravity_point>`), đây sẽ là điểm hút.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_gravity_point_unit_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **gravity_point_unit_distance** = ``0.0`` :ref:`🔗<class_Area2D_property_gravity_point_unit_distance>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_point_unit_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gravity_point_unit_distance**\ (\ )

Khoảng cách tại đó cường độ gravity bằng :ref:`gravity<class_Area2D_property_gravity>`. Ví dụ: trên một hành tinh có bán kính 100 pixel và gravity bề mặt là 4.0 px/s², đặt :ref:`gravity<class_Area2D_property_gravity>` thành 4.0 và khoảng cách đơn vị thành 100.0. Gravity sẽ suy giảm theo định luật nghịch đảo bình phương, vì vậy trong ví dụ này, tại khoảng cách 200 pixel từ tâm, gravity sẽ là 1.0 px/s² (gấp đôi khoảng cách, 1/4 gravity), tại 50 pixel, gravity sẽ là 16.0 px/s² (một nửa khoảng cách, gấp 4 gravity), v.v.

Điều trên chỉ đúng khi khoảng cách đơn vị là một số dương. Khi đặt giá trị này thành 0.0, gravity sẽ không đổi bất kể khoảng cách.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_gravity_space_override:

.. rst-class:: classref-property

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **gravity_space_override** = ``0`` :ref:`🔗<class_Area2D_property_gravity_space_override>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_space_override_mode**\ (\ value\: :ref:`SpaceOverride<enum_Area2D_SpaceOverride>`\ ) - :ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **get_gravity_space_override_mode**\ (\ )

Chế độ ghi đè dùng cho các phép tính gravity trong area này.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_linear_damp:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_damp** = ``0.1`` :ref:`🔗<class_Area2D_property_linear_damp>`

.. rst-class:: classref-property-setget

- |void| **set_linear_damp**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_linear_damp**\ (\ )

Tốc độ các đối tượng ngừng chuyển động trong area này. Đại diện cho vận tốc tuyến tính bị mất đi mỗi giây.

Xem :ref:`ProjectSettings.physics/2d/default_linear_damp<class_ProjectSettings_property_physics/2d/default_linear_damp>` để biết thêm chi tiết về damping.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_linear_damp_space_override:

.. rst-class:: classref-property

:ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **linear_damp_space_override** = ``0`` :ref:`🔗<class_Area2D_property_linear_damp_space_override>`

.. rst-class:: classref-property-setget

- |void| **set_linear_damp_space_override_mode**\ (\ value\: :ref:`SpaceOverride<enum_Area2D_SpaceOverride>`\ ) - :ref:`SpaceOverride<enum_Area2D_SpaceOverride>` **get_linear_damp_space_override_mode**\ (\ )

Chế độ ghi đè cho các phép tính giảm chấn tuyến tính trong vùng này.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_monitorable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **monitorable** = ``true`` :ref:`🔗<class_Area2D_property_monitorable>`

.. rst-class:: classref-property-setget

- |void| **set_monitorable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_monitorable**\ (\ )

Nếu ``true``, các vùng đang monitoring khác có thể phát hiện vùng này.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_monitoring:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **monitoring** = ``true`` :ref:`🔗<class_Area2D_property_monitoring>`

.. rst-class:: classref-property-setget

- |void| **set_monitoring**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_monitoring**\ (\ )

Nếu ``true``, vùng này phát hiện các body hoặc vùng đi vào và rời khỏi nó.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_property_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **priority** = ``0`` :ref:`🔗<class_Area2D_property_priority>`

.. rst-class:: classref-property-setget

- |void| **set_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_priority**\ (\ )

Độ ưu tiên của vùng. Các vùng có độ ưu tiên cao hơn được xử lý trước. Vật lý của :ref:`World2D<class_World2D>` luôn được xử lý sau cùng, sau tất cả các vùng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_Area2D_method_get_overlapping_areas:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Area2D<class_Area2D>`\] **get_overlapping_areas**\ (\ ) |const| :ref:`🔗<class_Area2D_method_get_overlapping_areas>`

Trả về danh sách các **Area2D**\ s giao nhau. :ref:`CollisionObject2D.collision_layer<class_CollisionObject2D_property_collision_layer>` của vùng chồng lấn phải là một phần của :ref:`CollisionObject2D.collision_mask<class_CollisionObject2D_property_collision_mask>` của vùng này thì vùng đó mới được phát hiện.

Vì lý do hiệu năng (tất cả va chạm được xử lý cùng lúc), danh sách này được thay đổi một lần trong bước vật lý, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_method_get_overlapping_bodies:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node2D<class_Node2D>`\] **get_overlapping_bodies**\ (\ ) |const| :ref:`🔗<class_Area2D_method_get_overlapping_bodies>`

Returns a list of intersecting :ref:`PhysicsBody2D<class_PhysicsBody2D>`\ s and :ref:`TileMap<class_TileMap>`\ s. The overlapping body's :ref:`CollisionObject2D.collision_layer<class_CollisionObject2D_property_collision_layer>` must be part of this area's :ref:`CollisionObject2D.collision_mask<class_CollisionObject2D_property_collision_mask>` in order to be detected.

Vì lý do hiệu năng (tất cả va chạm được xử lý cùng lúc), danh sách này được thay đổi một lần trong bước vật lý, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_method_has_overlapping_areas:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_overlapping_areas**\ (\ ) |const| :ref:`🔗<class_Area2D_method_has_overlapping_areas>`

Trả về ``true`` nếu giao nhau với bất kỳ **Area2D**\ s nào, nếu không thì trả về ``false``. :ref:`CollisionObject2D.collision_layer<class_CollisionObject2D_property_collision_layer>` của vùng chồng lấn phải là một phần của :ref:`CollisionObject2D.collision_mask<class_CollisionObject2D_property_collision_mask>` của vùng này thì vùng đó mới được phát hiện.

Vì lý do hiệu năng (tất cả va chạm được xử lý cùng lúc), danh sách các vùng chồng lấn được thay đổi một lần trong bước vật lý, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_method_has_overlapping_bodies:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_overlapping_bodies**\ (\ ) |const| :ref:`🔗<class_Area2D_method_has_overlapping_bodies>`

Returns ``true`` if intersecting any :ref:`PhysicsBody2D<class_PhysicsBody2D>`\ s or :ref:`TileMap<class_TileMap>`\ s, otherwise returns ``false``. The overlapping body's :ref:`CollisionObject2D.collision_layer<class_CollisionObject2D_property_collision_layer>` must be part of this area's :ref:`CollisionObject2D.collision_mask<class_CollisionObject2D_property_collision_mask>` in order to be detected.

Vì lý do hiệu năng (tất cả va chạm được xử lý cùng lúc), danh sách các body chồng lấn được thay đổi một lần trong bước vật lý, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_method_overlaps_area:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **overlaps_area**\ (\ area\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Area2D_method_overlaps_area>`

Trả về ``true`` nếu **Area2D** được chỉ định giao nhau hoặc chồng lấn với **Area2D** này, nếu không thì trả về ``false``.

\ **Lưu ý:** Kết quả của phép kiểm tra này không cập nhật ngay sau khi di chuyển các đối tượng. Để đảm bảo hiệu năng, danh sách các đối tượng chồng lấn được cập nhật một lần mỗi frame và trước bước vật lý. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area2D_method_overlaps_body:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **overlaps_body**\ (\ body\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Area2D_method_overlaps_body>`

Trả về ``true`` nếu physics body được chỉ định giao nhau hoặc chồng lấn với **Area2D** này, nếu không thì trả về ``false``.

\ **Lưu ý:** Kết quả của phép kiểm tra này không cập nhật ngay sau khi di chuyển các đối tượng. Để đảm bảo hiệu năng, danh sách các đối tượng chồng lấn được cập nhật một lần mỗi frame và trước bước vật lý. Hãy cân nhắc sử dụng signals thay thế.

Đối số ``body`` có thể là một instance :ref:`PhysicsBody2D<class_PhysicsBody2D>` hoặc :ref:`TileMap<class_TileMap>`. Mặc dù TileMaps bản thân không phải là physics body, chúng đăng ký các tile của mình với các collision shape dưới dạng một physics body ảo.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
