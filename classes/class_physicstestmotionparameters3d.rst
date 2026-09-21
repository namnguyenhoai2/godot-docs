:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsTestMotionParameters3D.xml.

.. _class_PhysicsTestMotionParameters3D:

PhysicsTestMotionParameters3D
=============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho :ref:`PhysicsServer3D.body_test_motion()<class_PhysicsServer3D_method_body_test_motion>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi các thuộc tính khác nhau của đối tượng này, chẳng hạn như motion, bạn có thể cấu hình các tham số cho :ref:`PhysicsServer3D.body_test_motion()<class_PhysicsServer3D_method_body_test_motion>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_separation_ray<class_PhysicsTestMotionParameters3D_property_collide_separation_ray>` | ``false``                                           |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] | :ref:`exclude_bodies<class_PhysicsTestMotionParameters3D_property_exclude_bodies>`                 | ``[]``                                              |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`int<class_int>`\] | :ref:`exclude_objects<class_PhysicsTestMotionParameters3D_property_exclude_objects>`               | ``[]``                                              |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`              | :ref:`from<class_PhysicsTestMotionParameters3D_property_from>`                                     | ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                          | :ref:`margin<class_PhysicsTestMotionParameters3D_property_margin>`                                 | ``0.001``                                           |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`int<class_int>`                              | :ref:`max_collisions<class_PhysicsTestMotionParameters3D_property_max_collisions>`                 | ``1``                                               |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                      | :ref:`motion<class_PhysicsTestMotionParameters3D_property_motion>`                                 | ``Vector3(0, 0, 0)``                                |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`recovery_as_collision<class_PhysicsTestMotionParameters3D_property_recovery_as_collision>`   | ``false``                                           |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsTestMotionParameters3D_property_collide_separation_ray:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_separation_ray** = ``false`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_collide_separation_ray>`

.. rst-class:: classref-property-setget

- |void| **set_collide_separation_ray_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_separation_ray_enabled**\ (\ )

Nếu được đặt thành ``true``, các shape thuộc loại :ref:`PhysicsServer3D.SHAPE_SEPARATION_RAY<class_PhysicsServer3D_constant_SHAPE_SEPARATION_RAY>` sẽ được sử dụng để phát hiện va chạm và có thể dừng motion. Có thể hữu ích khi snap xuống mặt đất.

Nếu được đặt thành ``false``, các shape thuộc loại :ref:`PhysicsServer3D.SHAPE_SEPARATION_RAY<class_PhysicsServer3D_constant_SHAPE_SEPARATION_RAY>` chỉ được sử dụng để tách ra khi chồng lấn với các body khác. Đây là công dụng chính của các separation ray shape.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_exclude_bodies:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **exclude_bodies** = ``[]`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_exclude_bodies>`

.. rst-class:: classref-property-setget

- |void| **set_exclude_bodies**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_exclude_bodies**\ (\ )

Mảng body :ref:`RID<class_RID>` tùy chọn cần loại trừ khỏi va chạm. Sử dụng :ref:`CollisionObject3D.get_rid()<class_CollisionObject3D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node dẫn xuất từ :ref:`CollisionObject3D<class_CollisionObject3D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_exclude_objects:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`int<class_int>`\] **exclude_objects** = ``[]`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_exclude_objects>`

.. rst-class:: classref-property-setget

- |void| **set_exclude_objects**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`int<class_int>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`int<class_int>`\] **get_exclude_objects**\ (\ )

Mảng object unique instance ID tùy chọn cần loại trừ khỏi va chạm. Xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_from:

.. rst-class:: classref-property

:ref:`Transform3D<class_Transform3D>` **from** = ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_from>`

.. rst-class:: classref-property-setget

- |void| **set_from**\ (\ value\: :ref:`Transform3D<class_Transform3D>`\ ) - :ref:`Transform3D<class_Transform3D>` **get_from**\ (\ )

Transform trong global space tại vị trí motion sẽ bắt đầu. Thông thường được đặt thành :ref:`Node3D.global_transform<class_Node3D_property_global_transform>` cho transform của body hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **margin** = ``0.001`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_margin>`

.. rst-class:: classref-property-setget

- |void| **set_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_margin**\ (\ )

Tăng kích thước của các shape tham gia vào quá trình phát hiện va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_max_collisions:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_collisions** = ``1`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_max_collisions>`

.. rst-class:: classref-property-setget

- |void| **set_max_collisions**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_collisions**\ (\ )

Số lượng va chạm tối đa được trả về, trong khoảng từ ``1`` đến ``32``. Luôn trả về các va chạm được phát hiện có độ sâu lớn nhất.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_motion:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **motion** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_motion>`

.. rst-class:: classref-property-setget

- |void| **set_motion**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_motion**\ (\ )

Vector motion dùng để xác định độ dài và hướng của motion cần kiểm tra.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters3D_property_recovery_as_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **recovery_as_collision** = ``false`` :ref:`🔗<class_PhysicsTestMotionParameters3D_property_recovery_as_collision>`

.. rst-class:: classref-property-setget

- |void| **set_recovery_as_collision_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_recovery_as_collision_enabled**\ (\ )

Nếu được đặt thành ``true``, mọi quá trình depenetration từ recovery phase đều được báo cáo là một va chạm; ví dụ, điều này được :ref:`CharacterBody3D<class_CharacterBody3D>` sử dụng để cải thiện việc phát hiện sàn trong quá trình floor snapping.

Nếu được đặt thành ``false``, chỉ các va chạm phát sinh từ motion mới được báo cáo, đây thường là hành vi mong muốn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
