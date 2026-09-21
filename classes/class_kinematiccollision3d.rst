:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/KinematicCollision3D.xml.

.. _class_KinematicCollision3D:

KinematicCollision3D
====================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lưu trữ dữ liệu va chạm từ chuyển động của một :ref:`PhysicsBody3D<class_PhysicsBody3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ dữ liệu va chạm từ chuyển động của một :ref:`PhysicsBody3D<class_PhysicsBody3D>`, thường là từ :ref:`PhysicsBody3D.move_and_collide()<class_PhysicsBody3D_method_move_and_collide>`. Khi một :ref:`PhysicsBody3D<class_PhysicsBody3D>` được di chuyển, nó sẽ dừng lại nếu phát hiện va chạm với một body khác. Nếu phát hiện va chạm, một đối tượng **KinematicCollision3D** sẽ được trả về.

Dữ liệu va chạm bao gồm đối tượng va chạm, chuyển động còn lại và vị trí va chạm. Dữ liệu này có thể được sử dụng để xác định phản hồi tùy chỉnh đối với va chạm.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_angle<class_KinematicCollision3D_method_get_angle>`\ (\ collision_index\: :ref:`int<class_int>` = 0, up_direction\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0)\ ) |const| |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_collider<class_KinematicCollision3D_method_get_collider>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                            |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collider_id<class_KinematicCollision3D_method_get_collider_id>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                      |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`         | :ref:`get_collider_rid<class_KinematicCollision3D_method_get_collider_rid>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                    |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_collider_shape<class_KinematicCollision3D_method_get_collider_shape>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collider_shape_index<class_KinematicCollision3D_method_get_collider_shape_index>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                    |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_collider_velocity<class_KinematicCollision3D_method_get_collider_velocity>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                          |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collision_count<class_KinematicCollision3D_method_get_collision_count>`\ (\ ) |const|                                                                                           |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_depth<class_KinematicCollision3D_method_get_depth>`\ (\ ) |const|                                                                                                               |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_local_shape<class_KinematicCollision3D_method_get_local_shape>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                      |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_normal<class_KinematicCollision3D_method_get_normal>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                                |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_position<class_KinematicCollision3D_method_get_position>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                                                            |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_remainder<class_KinematicCollision3D_method_get_remainder>`\ (\ ) |const|                                                                                                       |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_travel<class_KinematicCollision3D_method_get_travel>`\ (\ ) |const|                                                                                                             |
   +-------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_KinematicCollision3D_method_get_angle:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_angle**\ (\ collision_index\: :ref:`int<class_int>` = 0, up_direction\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0)\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_angle>`

Trả về góc va chạm theo ``up_direction``, mặc định là :ref:`Vector3.UP<class_Vector3_constant_UP>`. Giá trị này luôn dương.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collider:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_collider**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collider>`

Trả về :ref:`Object<class_Object>` được gắn với body va chạm, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collider_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collider_id**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collider_id>`

Trả về ID instance duy nhất của :ref:`Object<class_Object>` được gắn với body va chạm, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất). Xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collider_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_collider_rid**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collider_rid>`

Trả về :ref:`RID<class_RID>` của body va chạm được :ref:`PhysicsServer3D<class_PhysicsServer3D>` sử dụng, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collider_shape:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_collider_shape**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collider_shape>`

Trả về hình dạng của body va chạm, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collider_shape_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collider_shape_index**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collider_shape_index>`

Trả về chỉ số hình dạng của body va chạm, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất). Xem :ref:`CollisionObject3D<class_CollisionObject3D>`.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collider_velocity:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_collider_velocity**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collider_velocity>`

Trả về vận tốc của body va chạm, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_collision_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collision_count**\ (\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_collision_count>`

Trả về số lượng va chạm đã phát hiện.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_depth:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_depth**\ (\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_depth>`

Trả về độ dài phần chồng lấn của body va chạm dọc theo pháp tuyến va chạm.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_local_shape:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_local_shape**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_local_shape>`

Trả về hình dạng đang va chạm của đối tượng di chuyển, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_normal:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_normal**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_normal>`

Trả về pháp tuyến của hình dạng thuộc body va chạm tại điểm va chạm, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_position**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_position>`

Trả về điểm va chạm trong tọa độ toàn cục, dựa trên chỉ số va chạm (mặc định là va chạm sâu nhất).

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_remainder:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_remainder**\ (\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_remainder>`

Trả về vector chuyển động còn lại của đối tượng di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_KinematicCollision3D_method_get_travel:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_travel**\ (\ ) |const| :ref:`🔗<class_KinematicCollision3D_method_get_travel>`

Trả về quãng đường di chuyển của đối tượng di chuyển trước khi va chạm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
