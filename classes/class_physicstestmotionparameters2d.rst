:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsTestMotionParameters2D.xml.

.. _class_PhysicsTestMotionParameters2D:

PhysicsTestMotionParameters2D
=============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho :ref:`PhysicsServer2D.body_test_motion()<class_PhysicsServer2D_method_body_test_motion>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi nhiều thuộc tính khác nhau của đối tượng này, chẳng hạn như motion, bạn có thể cấu hình các tham số cho :ref:`PhysicsServer2D.body_test_motion()<class_PhysicsServer2D_method_body_test_motion>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_separation_ray<class_PhysicsTestMotionParameters2D_property_collide_separation_ray>` | ``false``                         |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] | :ref:`exclude_bodies<class_PhysicsTestMotionParameters2D_property_exclude_bodies>`                 | ``[]``                            |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`int<class_int>`\] | :ref:`exclude_objects<class_PhysicsTestMotionParameters2D_property_exclude_objects>`               | ``[]``                            |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Transform2D<class_Transform2D>`              | :ref:`from<class_PhysicsTestMotionParameters2D_property_from>`                                     | ``Transform2D(1, 0, 0, 1, 0, 0)`` |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`                          | :ref:`margin<class_PhysicsTestMotionParameters2D_property_margin>`                                 | ``0.08``                          |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`motion<class_PhysicsTestMotionParameters2D_property_motion>`                                 | ``Vector2(0, 0)``                 |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`recovery_as_collision<class_PhysicsTestMotionParameters2D_property_recovery_as_collision>`   | ``false``                         |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsTestMotionParameters2D_property_collide_separation_ray:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_separation_ray** = ``false`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_collide_separation_ray>`

.. rst-class:: classref-property-setget

- |void| **set_collide_separation_ray_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_separation_ray_enabled**\ (\ )

Nếu được đặt thành ``true``, các shape thuộc loại :ref:`PhysicsServer2D.SHAPE_SEPARATION_RAY<class_PhysicsServer2D_constant_SHAPE_SEPARATION_RAY>` sẽ được sử dụng để phát hiện va chạm và có thể dừng motion. Có thể hữu ích khi snap vào mặt đất.

Nếu được đặt thành ``false``, các shape thuộc loại :ref:`PhysicsServer2D.SHAPE_SEPARATION_RAY<class_PhysicsServer2D_constant_SHAPE_SEPARATION_RAY>` chỉ được sử dụng để tách khi chồng lấn với các body khác. Đây là công dụng chính của các shape separation ray.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters2D_property_exclude_bodies:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **exclude_bodies** = ``[]`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_exclude_bodies>`

.. rst-class:: classref-property-setget

- |void| **set_exclude_bodies**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_exclude_bodies**\ (\ )

Mảng tùy chọn các :ref:`RID<class_RID>` của body cần loại trừ khỏi va chạm. Sử dụng :ref:`CollisionObject2D.get_rid()<class_CollisionObject2D_method_get_rid>` để lấy :ref:`RID<class_RID>` được liên kết với một node dẫn xuất từ :ref:`CollisionObject2D<class_CollisionObject2D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters2D_property_exclude_objects:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`int<class_int>`\] **exclude_objects** = ``[]`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_exclude_objects>`

.. rst-class:: classref-property-setget

- |void| **set_exclude_objects**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`int<class_int>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`int<class_int>`\] **get_exclude_objects**\ (\ )

Mảng tùy chọn gồm ID instance duy nhất của các object cần loại trừ khỏi va chạm. Xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters2D_property_from:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **from** = ``Transform2D(1, 0, 0, 1, 0, 0)`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_from>`

.. rst-class:: classref-property-setget

- |void| **set_from**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_from**\ (\ )

Transform trong global space, nơi motion sẽ bắt đầu. Thường được đặt thành :ref:`Node2D.global_transform<class_Node2D_property_global_transform>` cho transform của body hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters2D_property_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **margin** = ``0.08`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_margin>`

.. rst-class:: classref-property-setget

- |void| **set_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_margin**\ (\ )

Tăng kích thước của các shape tham gia vào quá trình phát hiện va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters2D_property_motion:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **motion** = ``Vector2(0, 0)`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_motion>`

.. rst-class:: classref-property-setget

- |void| **set_motion**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_motion**\ (\ )

Vector motion dùng để xác định độ dài và hướng của motion cần kiểm tra.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionParameters2D_property_recovery_as_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **recovery_as_collision** = ``false`` :ref:`🔗<class_PhysicsTestMotionParameters2D_property_recovery_as_collision>`

.. rst-class:: classref-property-setget

- |void| **set_recovery_as_collision_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_recovery_as_collision_enabled**\ (\ )

Nếu được đặt thành ``true``, mọi quá trình depenetration từ giai đoạn recovery sẽ được báo cáo là một va chạm; ví dụ, :ref:`CharacterBody2D<class_CharacterBody2D>` sử dụng điều này để cải thiện việc phát hiện sàn trong quá trình floor snapping.

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
