:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/KinematicCollision2D.xml.

.. _class_KinematicCollision2D:

KinematicCollision2D
====================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lưu trữ dữ liệu va chạm từ chuyển động của một :ref:`PhysicsBody2D<class_PhysicsBody2D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ dữ liệu va chạm từ chuyển động của một :ref:`PhysicsBody2D<class_PhysicsBody2D>`, thường là từ :ref:`PhysicsBody2D.move_and_collide()<class_PhysicsBody2D_method_move_and_collide>`. Khi một :ref:`PhysicsBody2D<class_PhysicsBody2D>` được di chuyển, nó sẽ dừng lại nếu phát hiện va chạm với một body khác. Nếu phát hiện va chạm, một đối tượng **KinematicCollision2D** sẽ được trả về.

Dữ liệu va chạm bao gồm đối tượng va chạm, chuyển động còn lại và vị trí va chạm. Dữ liệu này có thể được sử dụng để xác định phản hồi tùy chỉnh đối với va chạm.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_angle<class_KinematicCollision2D_method_get_angle>`\ (\ up_direction\: :ref:`Vector2<class_Vector2>` = Vector2(0, -1)\ ) |const| |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_collider<class_KinematicCollision2D_method_get_collider>`\ (\ ) |const|                                                          |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collider_id<class_KinematicCollision2D_method_get_collider_id>`\ (\ ) |const|                                                    |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`         | :ref:`get_collider_rid<class_KinematicCollision2D_method_get_collider_rid>`\ (\ ) |const|                                                  |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_collider_shape<class_KinematicCollision2D_method_get_collider_shape>`\ (\ ) |const|                                              |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collider_shape_index<class_KinematicCollision2D_method_get_collider_shape_index>`\ (\ ) |const|                                  |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_collider_velocity<class_KinematicCollision2D_method_get_collider_velocity>`\ (\ ) |const|                                        |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_depth<class_KinematicCollision2D_method_get_depth>`\ (\ ) |const|                                                                |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_local_shape<class_KinematicCollision2D_method_get_local_shape>`\ (\ ) |const|                                                    |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_normal<class_KinematicCollision2D_method_get_normal>`\ (\ ) |const|                                                              |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_position<class_KinematicCollision2D_method_get_position>`\ (\ ) |const|                                                          |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_remainder<class_KinematicCollision2D_method_get_remainder>`\ (\ ) |const|                                                        |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_travel<class_KinematicCollision2D_method_get_travel>`\ (\ ) |const|                                                              |
   +-------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_KinematicCollision2D_method_get_angle:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_angle**\ (\ up_direction\: :ref:`Vector2<class_Vector2>` = Vector2(0, -1)\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_angle>`

Trả về góc va chạm theo ``up_direction``, mặc định là :ref:`Vector2.UP<class_Vector2_constant_UP>`. Giá trị này luôn dương.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_collider:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_collider**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_collider>`

Trả về :ref:`Object<class_Object>` được gắn vào body đang va chạm.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_collider_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collider_id**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_collider_id>`

Trả về ID instance duy nhất của :ref:`Object<class_Object>` được gắn vào body đang va chạm. Xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_collider_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_collider_rid**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_collider_rid>`

Trả về :ref:`RID<class_RID>` của body đang va chạm được :ref:`PhysicsServer2D<class_PhysicsServer2D>` sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_collider_shape:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_collider_shape**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_collider_shape>`

Trả về shape của body đang va chạm.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_collider_shape_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collider_shape_index**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_collider_shape_index>`

Trả về chỉ mục shape của body đang va chạm. Xem :ref:`CollisionObject2D<class_CollisionObject2D>`.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_collider_velocity:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_collider_velocity**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_collider_velocity>`

Trả về vận tốc của body đang va chạm.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_depth:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_depth**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_depth>`

Trả về độ dài phần chồng lấn của body đang va chạm dọc theo pháp tuyến va chạm.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_local_shape:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_local_shape**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_local_shape>`

Trả về shape va chạm của đối tượng đang di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_normal:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_normal**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_normal>`

Trả về pháp tuyến của shape thuộc body đang va chạm tại điểm va chạm.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_position**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_position>`

Trả về điểm va chạm trong hệ tọa độ toàn cục.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_remainder:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_remainder**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_remainder>`

Trả về vector chuyển động còn lại của đối tượng đang di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision2D_method_get_travel:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_travel**\ (\ ) |const| :ref:`🔗<class_KinematicCollision2D_method_get_travel>`

Trả về quãng đường đối tượng đang di chuyển đã đi trước khi va chạm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
