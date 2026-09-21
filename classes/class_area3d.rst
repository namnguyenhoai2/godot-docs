:github_url: hide

.. meta::
	:keywords: trigger

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Area3D.xml.

.. _class_Area3D:

Area3D
======

**Kế thừa:** :ref:`CollisionObject3D<class_CollisionObject3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

A region of 3D space that detects other :ref:`CollisionObject3D<class_CollisionObject3D>`\ s entering or exiting it.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Area3D** is a region of 3D space defined by one or multiple :ref:`CollisionShape3D<class_CollisionShape3D>` or :ref:`CollisionPolygon3D<class_CollisionPolygon3D>` child nodes. It detects when other :ref:`CollisionObject3D<class_CollisionObject3D>`\ s enter or exit it, and it also keeps track of which collision objects haven't exited it yet (i.e. which one are overlapping it).

Node này cũng có thể thay đổi hoặc ghi đè cục bộ các tham số vật lý (gravity, damping) và định tuyến audio đến các audio bus tùy chỉnh.

\ **Lưu ý:** Các area và body được tạo bằng :ref:`PhysicsServer3D<class_PhysicsServer3D>` có thể không tương tác như mong đợi với **Area3D**\ s và có thể không phát signal hoặc theo dõi object chính xác.

\ **Warning:** Using a :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` inside a :ref:`CollisionShape3D<class_CollisionShape3D>` child of this node (created e.g. by using the **Create Trimesh Collision Sibling** option in the **Mesh** menu that appears when selecting a :ref:`MeshInstance3D<class_MeshInstance3D>` node) may give unexpected results, since this collision shape is hollow. If this is not desired, it has to be split into multiple :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>`\ s or primitive shapes like :ref:`BoxShape3D<class_BoxShape3D>`, or in some cases it may be replaceable by a :ref:`CollisionPolygon3D<class_CollisionPolygon3D>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using Area2D <../tutorials/physics/using_area_2d>`

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `GUI in 3D Viewport Demo <https://godotengine.org/asset-library/asset/2807>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`angular_damp<class_Area3D_property_angular_damp>`                               | ``0.1``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`SpaceOverride<enum_Area3D_SpaceOverride>` | :ref:`angular_damp_space_override<class_Area3D_property_angular_damp_space_override>` | ``0``                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`StringName<class_StringName>`             | :ref:`audio_bus_name<class_Area3D_property_audio_bus_name>`                           | ``&"Master"``         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                         | :ref:`audio_bus_override<class_Area3D_property_audio_bus_override>`                   | ``false``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`gravity<class_Area3D_property_gravity>`                                         | ``9.8``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`gravity_direction<class_Area3D_property_gravity_direction>`                     | ``Vector3(0, -1, 0)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                         | :ref:`gravity_point<class_Area3D_property_gravity_point>`                             | ``false``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`gravity_point_center<class_Area3D_property_gravity_point_center>`               | ``Vector3(0, -1, 0)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`gravity_point_unit_distance<class_Area3D_property_gravity_point_unit_distance>` | ``0.0``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`SpaceOverride<enum_Area3D_SpaceOverride>` | :ref:`gravity_space_override<class_Area3D_property_gravity_space_override>`           | ``0``                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`linear_damp<class_Area3D_property_linear_damp>`                                 | ``0.1``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`SpaceOverride<enum_Area3D_SpaceOverride>` | :ref:`linear_damp_space_override<class_Area3D_property_linear_damp_space_override>`   | ``0``                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                         | :ref:`monitorable<class_Area3D_property_monitorable>`                                 | ``true``              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                         | :ref:`monitoring<class_Area3D_property_monitoring>`                                   | ``true``              |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                           | :ref:`priority<class_Area3D_property_priority>`                                       | ``0``                 |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`reverb_bus_amount<class_Area3D_property_reverb_bus_amount>`                     | ``0.0``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                         | :ref:`reverb_bus_enabled<class_Area3D_property_reverb_bus_enabled>`                   | ``false``             |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`StringName<class_StringName>`             | :ref:`reverb_bus_name<class_Area3D_property_reverb_bus_name>`                         | ``&"Master"``         |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`reverb_bus_uniformity<class_Area3D_property_reverb_bus_uniformity>`             | ``0.0``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`wind_attenuation_factor<class_Area3D_property_wind_attenuation_factor>`         | ``0.0``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                       | :ref:`wind_force_magnitude<class_Area3D_property_wind_force_magnitude>`               | ``0.0``               |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+
   | :ref:`NodePath<class_NodePath>`                 | :ref:`wind_source_path<class_Area3D_property_wind_source_path>`                       | ``NodePath("")``      |
   +-------------------------------------------------+---------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Area3D<class_Area3D>`\] | :ref:`get_overlapping_areas<class_Area3D_method_get_overlapping_areas>`\ (\ ) |const|                 |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node3D<class_Node3D>`\] | :ref:`get_overlapping_bodies<class_Area3D_method_get_overlapping_bodies>`\ (\ ) |const|               |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`has_overlapping_areas<class_Area3D_method_has_overlapping_areas>`\ (\ ) |const|                 |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`has_overlapping_bodies<class_Area3D_method_has_overlapping_bodies>`\ (\ ) |const|               |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`overlaps_area<class_Area3D_method_overlaps_area>`\ (\ area\: :ref:`Node<class_Node>`\ ) |const| |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                  | :ref:`overlaps_body<class_Area3D_method_overlaps_body>`\ (\ body\: :ref:`Node<class_Node>`\ ) |const| |
   +----------------------------------------------------------+-------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_Area3D_signal_area_entered:

.. rst-class:: classref-signal

**area_entered**\ (\ area\: :ref:`Area3D<class_Area3D>`\ ) :ref:`🔗<class_Area3D_signal_area_entered>`

Được phát ra khi ``area`` nhận được đi vào area này. Yêu cầu :ref:`monitoring<class_Area3D_property_monitoring>` được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_area_exited:

.. rst-class:: classref-signal

**area_exited**\ (\ area\: :ref:`Area3D<class_Area3D>`\ ) :ref:`🔗<class_Area3D_signal_area_exited>`

Được phát ra khi ``area`` nhận được rời khỏi area này. Yêu cầu :ref:`monitoring<class_Area3D_property_monitoring>` được đặt thành ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_area_shape_entered:

.. rst-class:: classref-signal

**area_shape_entered**\ (\ area_rid\: :ref:`RID<class_RID>`, area\: :ref:`Area3D<class_Area3D>`, area_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area3D_signal_area_shape_entered>`

Được phát ra khi một :ref:`Shape3D<class_Shape3D>` của ``area`` nhận được đi vào một shape của area này. Yêu cầu :ref:`monitoring<class_Area3D_property_monitoring>` được đặt thành ``true``.

\ ``local_shape_index`` và ``area_shape_index`` lần lượt chứa các index của những shape tương tác từ area này và area còn lại. ``area_rid`` chứa :ref:`RID<class_RID>` của area còn lại. Có thể sử dụng các giá trị này với :ref:`PhysicsServer3D<class_PhysicsServer3D>`.

\ **Ví dụ:** Lấy node :ref:`CollisionShape3D<class_CollisionShape3D>` từ shape index:


.. tabs::

 .. code-tab:: gdscript

    var other_shape_owner = area.shape_find_owner(area_shape_index)
    var other_shape_node = area.shape_owner_get_owner(other_shape_owner)

    var local_shape_owner = shape_find_owner(local_shape_index)
    var local_shape_node = shape_owner_get_owner(local_shape_owner)



.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_area_shape_exited:

.. rst-class:: classref-signal

**area_shape_exited**\ (\ area_rid\: :ref:`RID<class_RID>`, area\: :ref:`Area3D<class_Area3D>`, area_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area3D_signal_area_shape_exited>`

Được phát ra khi một :ref:`Shape3D<class_Shape3D>` của ``area`` nhận được rời khỏi một shape của area này. Yêu cầu :ref:`monitoring<class_Area3D_property_monitoring>` được đặt thành ``true``.

Xem thêm :ref:`area_shape_entered<class_Area3D_signal_area_shape_entered>`.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_body_entered:

.. rst-class:: classref-signal

**body_entered**\ (\ body\: :ref:`Node3D<class_Node3D>`\ ) :ref:`🔗<class_Area3D_signal_body_entered>`

Emitted when the received ``body`` enters this area. ``body`` can be a :ref:`PhysicsBody3D<class_PhysicsBody3D>`, :ref:`SoftBody3D<class_SoftBody3D>` or :ref:`GridMap<class_GridMap>`. :ref:`GridMap<class_GridMap>`\ s are detected if their :ref:`MeshLibrary<class_MeshLibrary>` has collision shapes configured. Requires :ref:`monitoring<class_Area3D_property_monitoring>` to be set to ``true``.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các vùng chồng lấp với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy sẽ không phát signal này trong những trường hợp đó.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_body_exited:

.. rst-class:: classref-signal

**body_exited**\ (\ body\: :ref:`Node3D<class_Node3D>`\ ) :ref:`🔗<class_Area3D_signal_body_exited>`

Emitted when the received ``body`` exits this area. ``body`` can be a :ref:`PhysicsBody3D<class_PhysicsBody3D>`, :ref:`SoftBody3D<class_SoftBody3D>` or :ref:`GridMap<class_GridMap>`. :ref:`GridMap<class_GridMap>`\ s are detected if their :ref:`MeshLibrary<class_MeshLibrary>` has collision shapes configured. Requires :ref:`monitoring<class_Area3D_property_monitoring>` to be set to ``true``.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các vùng chồng lấp với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy sẽ không phát signal này trong những trường hợp đó.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_body_shape_entered:

.. rst-class:: classref-signal

**body_shape_entered**\ (\ body_rid\: :ref:`RID<class_RID>`, body\: :ref:`Node3D<class_Node3D>`, body_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area3D_signal_body_shape_entered>`

Emitted when a :ref:`Shape3D<class_Shape3D>` of the received ``body`` enters a shape of this area. ``body`` can be a :ref:`PhysicsBody3D<class_PhysicsBody3D>`, :ref:`SoftBody3D<class_SoftBody3D>` or :ref:`GridMap<class_GridMap>`. :ref:`GridMap<class_GridMap>`\ s are detected if their :ref:`MeshLibrary<class_MeshLibrary>` has collision shapes configured. Requires :ref:`monitoring<class_Area3D_property_monitoring>` to be set to ``true``.

\ ``local_shape_index`` và ``body_shape_index`` lần lượt chứa các index của những shape tương tác từ area này và body tương tác. ``body_rid`` chứa :ref:`RID<class_RID>` của body. Có thể sử dụng các giá trị này với :ref:`PhysicsServer3D<class_PhysicsServer3D>`.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các vùng chồng lấp với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy sẽ không phát signal này trong những trường hợp đó.

\ **Ví dụ:** Lấy node :ref:`CollisionShape3D<class_CollisionShape3D>` từ shape index:


.. tabs::

 .. code-tab:: gdscript

    var body_shape_owner = body.shape_find_owner(body_shape_index)
    var body_shape_node = body.shape_owner_get_owner(body_shape_owner)

    var local_shape_owner = shape_find_owner(local_shape_index)
    var local_shape_node = shape_owner_get_owner(local_shape_owner)



.. rst-class:: classref-item-separator

----

.. _class_Area3D_signal_body_shape_exited:

.. rst-class:: classref-signal

**body_shape_exited**\ (\ body_rid\: :ref:`RID<class_RID>`, body\: :ref:`Node3D<class_Node3D>`, body_shape_index\: :ref:`int<class_int>`, local_shape_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Area3D_signal_body_shape_exited>`

Emitted when a :ref:`Shape3D<class_Shape3D>` of the received ``body`` exits a shape of this area. ``body`` can be a :ref:`PhysicsBody3D<class_PhysicsBody3D>`, :ref:`SoftBody3D<class_SoftBody3D>` or :ref:`GridMap<class_GridMap>`. :ref:`GridMap<class_GridMap>`\ s are detected if their :ref:`MeshLibrary<class_MeshLibrary>` has collision shapes configured. Requires :ref:`monitoring<class_Area3D_property_monitoring>` to be set to ``true``.

Xem thêm :ref:`body_shape_entered<class_Area3D_signal_body_shape_entered>`.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các vùng chồng lấp với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy sẽ không phát signal này trong những trường hợp đó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_Area3D_SpaceOverride:

.. rst-class:: classref-enumeration

enum **SpaceOverride**: :ref:`🔗<enum_Area3D_SpaceOverride>`

.. _class_Area3D_constant_SPACE_OVERRIDE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **SPACE_OVERRIDE_DISABLED** = ``0``

Area này không ảnh hưởng đến gravity/damping.

.. _class_Area3D_constant_SPACE_OVERRIDE_COMBINE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **SPACE_OVERRIDE_COMBINE** = ``1``

Area này cộng các giá trị gravity/damping của nó vào kết quả đã tính đến thời điểm hiện tại (theo thứ tự :ref:`priority<class_Area3D_property_priority>`).

.. _class_Area3D_constant_SPACE_OVERRIDE_COMBINE_REPLACE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **SPACE_OVERRIDE_COMBINE_REPLACE** = ``2``

Area này cộng các giá trị gravity/damping của nó vào kết quả đã tính đến thời điểm hiện tại (theo thứ tự :ref:`priority<class_Area3D_property_priority>`), bỏ qua mọi area có priority thấp hơn.

.. _class_Area3D_constant_SPACE_OVERRIDE_REPLACE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **SPACE_OVERRIDE_REPLACE** = ``3``

Area này thay thế mọi gravity/damping, kể cả các giá trị mặc định, bỏ qua mọi area có priority thấp hơn.

.. _class_Area3D_constant_SPACE_OVERRIDE_REPLACE_COMBINE:

.. rst-class:: classref-enumeration-constant

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **SPACE_OVERRIDE_REPLACE_COMBINE** = ``4``

Area này thay thế mọi gravity/damping đã được tính đến thời điểm hiện tại (theo thứ tự :ref:`priority<class_Area3D_property_priority>`), nhưng vẫn tiếp tục tính toán các area còn lại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_Area3D_property_angular_damp:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_damp** = ``0.1`` :ref:`🔗<class_Area3D_property_angular_damp>`

.. rst-class:: classref-property-setget

- |void| **set_angular_damp**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angular_damp**\ (\ )

Tốc độ các object ngừng quay trong area này. Đại diện cho vận tốc góc bị mất đi mỗi giây.

Xem :ref:`ProjectSettings.physics/3d/default_angular_damp<class_ProjectSettings_property_physics/3d/default_angular_damp>` để biết thêm chi tiết về damping.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_angular_damp_space_override:

.. rst-class:: classref-property

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **angular_damp_space_override** = ``0`` :ref:`🔗<class_Area3D_property_angular_damp_space_override>`

.. rst-class:: classref-property-setget

- |void| **set_angular_damp_space_override_mode**\ (\ value\: :ref:`SpaceOverride<enum_Area3D_SpaceOverride>`\ ) - :ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **get_angular_damp_space_override_mode**\ (\ )

Chế độ ghi đè để tính angular damping trong area này.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_audio_bus_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **audio_bus_name** = ``&"Master"`` :ref:`🔗<class_Area3D_property_audio_bus_name>`

.. rst-class:: classref-property-setget

- |void| **set_audio_bus_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_audio_bus_name**\ (\ )

Tên audio bus của area.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_audio_bus_override:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **audio_bus_override** = ``false`` :ref:`🔗<class_Area3D_property_audio_bus_override>`

.. rst-class:: classref-property-setget

- |void| **set_audio_bus_override**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_overriding_audio_bus**\ (\ )

Nếu ``true``, audio bus của area sẽ ghi đè audio bus mặc định.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_gravity:

.. rst-class:: classref-property

:ref:`float<class_float>` **gravity** = ``9.8`` :ref:`🔗<class_Area3D_property_gravity>`

.. rst-class:: classref-property-setget

- |void| **set_gravity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gravity**\ (\ )

Cường độ gravity của area (tính bằng mét trên giây bình phương). Giá trị này nhân với hướng gravity. Điều này hữu ích khi muốn thay đổi lực gravity mà không thay đổi hướng của nó.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_gravity_direction:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **gravity_direction** = ``Vector3(0, -1, 0)`` :ref:`🔗<class_Area3D_property_gravity_direction>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_direction**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_gravity_direction**\ (\ )

Vector gravity của area (chưa được chuẩn hóa).

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_gravity_point:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **gravity_point** = ``false`` :ref:`🔗<class_Area3D_property_gravity_point>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_is_point**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_gravity_a_point**\ (\ )

Nếu ``true``, gravity được tính từ một điểm (được thiết lập qua :ref:`gravity_point_center<class_Area3D_property_gravity_point_center>`). Xem thêm :ref:`gravity_space_override<class_Area3D_property_gravity_space_override>`.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_gravity_point_center:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **gravity_point_center** = ``Vector3(0, -1, 0)`` :ref:`🔗<class_Area3D_property_gravity_point_center>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_point_center**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_gravity_point_center**\ (\ )

Nếu gravity là một điểm (xem :ref:`gravity_point<class_Area3D_property_gravity_point>`), đây sẽ là điểm hút.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_gravity_point_unit_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **gravity_point_unit_distance** = ``0.0`` :ref:`🔗<class_Area3D_property_gravity_point_unit_distance>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_point_unit_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gravity_point_unit_distance**\ (\ )

Khoảng cách tại đó cường độ trọng lực bằng :ref:`gravity<class_Area3D_property_gravity>`. Ví dụ, với một hành tinh có bán kính 100 mét và trọng lực bề mặt là 4.0 m/s², hãy đặt :ref:`gravity<class_Area3D_property_gravity>` thành 4.0 và khoảng cách đơn vị thành 100.0. Trọng lực sẽ suy giảm theo định luật nghịch đảo bình phương, vì vậy trong ví dụ này, ở cách tâm 200 mét, trọng lực sẽ là 1.0 m/s² (khoảng cách tăng gấp đôi, trọng lực còn 1/4), ở 50 mét sẽ là 16.0 m/s² (khoảng cách giảm một nửa, trọng lực tăng gấp 4 lần), v.v.

Điều trên chỉ đúng khi khoảng cách đơn vị là một số dương. Khi đặt giá trị này thành 0.0, trọng lực sẽ không đổi bất kể khoảng cách.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_gravity_space_override:

.. rst-class:: classref-property

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **gravity_space_override** = ``0`` :ref:`🔗<class_Area3D_property_gravity_space_override>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_space_override_mode**\ (\ value\: :ref:`SpaceOverride<enum_Area3D_SpaceOverride>`\ ) - :ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **get_gravity_space_override_mode**\ (\ )

Chế độ ghi đè cho các phép tính trọng lực trong khu vực này.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_linear_damp:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_damp** = ``0.1`` :ref:`🔗<class_Area3D_property_linear_damp>`

.. rst-class:: classref-property-setget

- |void| **set_linear_damp**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_linear_damp**\ (\ )

Tốc độ mà các đối tượng dừng chuyển động trong khu vực này. Đại diện cho vận tốc tuyến tính bị mất mỗi giây.

Xem :ref:`ProjectSettings.physics/3d/default_linear_damp<class_ProjectSettings_property_physics/3d/default_linear_damp>` để biết thêm chi tiết về damping.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_linear_damp_space_override:

.. rst-class:: classref-property

:ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **linear_damp_space_override** = ``0`` :ref:`🔗<class_Area3D_property_linear_damp_space_override>`

.. rst-class:: classref-property-setget

- |void| **set_linear_damp_space_override_mode**\ (\ value\: :ref:`SpaceOverride<enum_Area3D_SpaceOverride>`\ ) - :ref:`SpaceOverride<enum_Area3D_SpaceOverride>` **get_linear_damp_space_override_mode**\ (\ )

Chế độ ghi đè cho các phép tính damping tuyến tính trong khu vực này.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_monitorable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **monitorable** = ``true`` :ref:`🔗<class_Area3D_property_monitorable>`

.. rst-class:: classref-property-setget

- |void| **set_monitorable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_monitorable**\ (\ )

Nếu ``true``, các khu vực monitoring khác có thể phát hiện khu vực này.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_monitoring:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **monitoring** = ``true`` :ref:`🔗<class_Area3D_property_monitoring>`

.. rst-class:: classref-property-setget

- |void| **set_monitoring**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_monitoring**\ (\ )

Nếu ``true``, khu vực này sẽ phát hiện các body hoặc khu vực đi vào và rời khỏi nó.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **priority** = ``0`` :ref:`🔗<class_Area3D_property_priority>`

.. rst-class:: classref-property-setget

- |void| **set_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_priority**\ (\ )

Độ ưu tiên của khu vực. Các khu vực có độ ưu tiên cao hơn được xử lý trước. Vật lý của :ref:`World3D<class_World3D>` luôn được xử lý sau cùng, sau tất cả các khu vực.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_reverb_bus_amount:

.. rst-class:: classref-property

:ref:`float<class_float>` **reverb_bus_amount** = ``0.0`` :ref:`🔗<class_Area3D_property_reverb_bus_amount>`

.. rst-class:: classref-property-setget

- |void| **set_reverb_amount**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_reverb_amount**\ (\ )

Mức độ mà khu vực này áp dụng reverb cho âm thanh liên kết với nó. Có phạm vi từ ``0`` đến ``1`` với độ chính xác ``0.1``.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_reverb_bus_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **reverb_bus_enabled** = ``false`` :ref:`🔗<class_Area3D_property_reverb_bus_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_use_reverb_bus**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_reverb_bus**\ (\ )

Nếu ``true``, khu vực này áp dụng reverb cho âm thanh liên kết với nó.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_reverb_bus_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **reverb_bus_name** = ``&"Master"`` :ref:`🔗<class_Area3D_property_reverb_bus_name>`

.. rst-class:: classref-property-setget

- |void| **set_reverb_bus_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_reverb_bus_name**\ (\ )

Tên của reverb bus được sử dụng cho âm thanh liên kết với khu vực này.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_reverb_bus_uniformity:

.. rst-class:: classref-property

:ref:`float<class_float>` **reverb_bus_uniformity** = ``0.0`` :ref:`🔗<class_Area3D_property_reverb_bus_uniformity>`

.. rst-class:: classref-property-setget

- |void| **set_reverb_uniformity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_reverb_uniformity**\ (\ )

Mức độ mà reverb của khu vực này tạo ra hiệu ứng đồng nhất. Có phạm vi từ ``0`` đến ``1`` với độ chính xác ``0.1``.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_wind_attenuation_factor:

.. rst-class:: classref-property

:ref:`float<class_float>` **wind_attenuation_factor** = ``0.0`` :ref:`🔗<class_Area3D_property_wind_attenuation_factor>`

.. rst-class:: classref-property-setget

- |void| **set_wind_attenuation_factor**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_wind_attenuation_factor**\ (\ )

Tốc độ theo hàm mũ mà lực gió giảm dần theo khoảng cách từ nguồn gốc của nó.

\ **Lưu ý:** Lực gió này chỉ áp dụng cho các node :ref:`SoftBody3D<class_SoftBody3D>`. Các physics body khác hiện không bị ảnh hưởng bởi gió.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_wind_force_magnitude:

.. rst-class:: classref-property

:ref:`float<class_float>` **wind_force_magnitude** = ``0.0`` :ref:`🔗<class_Area3D_property_wind_force_magnitude>`

.. rst-class:: classref-property-setget

- |void| **set_wind_force_magnitude**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_wind_force_magnitude**\ (\ )

Độ lớn của lực gió dành riêng cho khu vực.

\ **Lưu ý:** Lực gió này chỉ áp dụng cho các node :ref:`SoftBody3D<class_SoftBody3D>`. Các physics body khác hiện không bị ảnh hưởng bởi gió.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_property_wind_source_path:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **wind_source_path** = ``NodePath("")`` :ref:`🔗<class_Area3D_property_wind_source_path>`

.. rst-class:: classref-property-setget

- |void| **set_wind_source_path**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_wind_source_path**\ (\ )

:ref:`Node3D<class_Node3D>` được sử dụng để xác định hướng và nguồn gốc của lực gió dành riêng cho khu vực. Hướng này ngược với trục z của local transform của :ref:`Node3D<class_Node3D>`, còn nguồn gốc là gốc của local transform của :ref:`Node3D<class_Node3D>`.

\ **Lưu ý:** Lực gió này chỉ áp dụng cho các node :ref:`SoftBody3D<class_SoftBody3D>`. Các physics body khác hiện không bị ảnh hưởng bởi gió.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Area3D_method_get_overlapping_areas:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Area3D<class_Area3D>`\] **get_overlapping_areas**\ (\ ) |const| :ref:`🔗<class_Area3D_method_get_overlapping_areas>`

Trả về danh sách các **Area3D**\ s giao nhau. :ref:`CollisionObject3D.collision_layer<class_CollisionObject3D_property_collision_layer>` của khu vực chồng lấn phải là một phần của :ref:`CollisionObject3D.collision_mask<class_CollisionObject3D_property_collision_mask>` của khu vực này thì mới được phát hiện.

Vì lý do hiệu năng (tất cả các va chạm được xử lý cùng lúc), danh sách này được cập nhật một lần trong bước physics, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_method_get_overlapping_bodies:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node3D<class_Node3D>`\] **get_overlapping_bodies**\ (\ ) |const| :ref:`🔗<class_Area3D_method_get_overlapping_bodies>`

Returns a list of intersecting :ref:`PhysicsBody3D<class_PhysicsBody3D>`\ s, :ref:`SoftBody3D<class_SoftBody3D>`\ s, and :ref:`GridMap<class_GridMap>`\ s. The overlapping body's :ref:`CollisionObject3D.collision_layer<class_CollisionObject3D_property_collision_layer>` must be part of this area's :ref:`CollisionObject3D.collision_mask<class_CollisionObject3D_property_collision_mask>` in order to be detected.

Vì lý do hiệu năng (tất cả các va chạm được xử lý cùng lúc), danh sách này được cập nhật một lần trong bước physics, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các phần chồng lấn với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy sẽ không trả về các body như vậy.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_method_has_overlapping_areas:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_overlapping_areas**\ (\ ) |const| :ref:`🔗<class_Area3D_method_has_overlapping_areas>`

Trả về ``true`` nếu giao nhau với bất kỳ **Area3D**\ s nào, nếu không thì trả về ``false``. :ref:`CollisionObject3D.collision_layer<class_CollisionObject3D_property_collision_layer>` của khu vực chồng lấn phải là một phần của :ref:`CollisionObject3D.collision_mask<class_CollisionObject3D_property_collision_mask>` của khu vực này thì mới được phát hiện.

Vì lý do hiệu năng, danh sách các khu vực chồng lấn được cập nhật một lần trong bước physics, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_method_has_overlapping_bodies:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_overlapping_bodies**\ (\ ) |const| :ref:`🔗<class_Area3D_method_has_overlapping_bodies>`

Returns ``true`` if intersecting any :ref:`PhysicsBody3D<class_PhysicsBody3D>`\ s, :ref:`SoftBody3D<class_SoftBody3D>`\ s, or :ref:`GridMap<class_GridMap>`\ s, otherwise returns ``false``. The overlapping body's :ref:`CollisionObject3D.collision_layer<class_CollisionObject3D_property_collision_layer>` must be part of this area's :ref:`CollisionObject3D.collision_mask<class_CollisionObject3D_property_collision_mask>` in order to be detected.

Vì lý do hiệu năng, danh sách các body chồng lấn được cập nhật một lần trong bước physics, không phải ngay sau khi các đối tượng được di chuyển. Hãy cân nhắc sử dụng signals thay thế.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các phần chồng lấn với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy sẽ không xem xét các body như vậy.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_method_overlaps_area:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **overlaps_area**\ (\ area\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Area3D_method_overlaps_area>`

Trả về ``true`` nếu **Area3D** đã cho giao nhau hoặc chồng lấn với **Area3D** này, nếu không thì trả về ``false``.

\ **Lưu ý:** Kết quả của phép kiểm tra này không được cập nhật ngay sau khi di chuyển các đối tượng. Vì lý do hiệu năng, danh sách các phần chồng lấn được cập nhật một lần mỗi frame và trước bước physics. Hãy cân nhắc sử dụng signals thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Area3D_method_overlaps_body:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **overlaps_body**\ (\ body\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Area3D_method_overlaps_body>`

Trả về ``true`` nếu physics body đã cho giao nhau hoặc chồng lấn với **Area3D** này, nếu không thì trả về ``false``.

\ Đối số ``body`` có thể là một instance của :ref:`PhysicsBody3D<class_PhysicsBody3D>`, :ref:`SoftBody3D<class_SoftBody3D>` hoặc :ref:`GridMap<class_GridMap>`. Mặc dù GridMaps không phải là physics body, chúng đăng ký các tile của mình với các collision shape dưới dạng một physics body ảo.

\ **Lưu ý:** Kết quả của phép kiểm tra này không được cập nhật ngay sau khi di chuyển các đối tượng. Vì lý do hiệu năng, danh sách các phần chồng lấn được cập nhật một lần mỗi frame và trước bước physics. Hãy cân nhắc sử dụng signals thay thế.

\ **Lưu ý:** Godot Physics không hỗ trợ báo cáo các phần chồng lấn với :ref:`SoftBody3D<class_SoftBody3D>`, vì vậy trong những trường hợp đó sẽ trả về ``false``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
