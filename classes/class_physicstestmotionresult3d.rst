:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsTestMotionResult3D.xml.

.. _class_PhysicsTestMotionResult3D:

PhysicsTestMotionResult3D
=========================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Mô tả kết quả chuyển động và va chạm từ :ref:`PhysicsServer3D.body_test_motion()<class_PhysicsServer3D_method_body_test_motion>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Mô tả kết quả chuyển động và va chạm từ :ref:`PhysicsServer3D.body_test_motion()<class_PhysicsServer3D_method_body_test_motion>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`   | :ref:`get_collider<class_PhysicsTestMotionResult3D_method_get_collider>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                           |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collider_id<class_PhysicsTestMotionResult3D_method_get_collider_id>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                     |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`         | :ref:`get_collider_rid<class_PhysicsTestMotionResult3D_method_get_collider_rid>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|                   |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collider_shape<class_PhysicsTestMotionResult3D_method_get_collider_shape>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|               |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_collider_velocity<class_PhysicsTestMotionResult3D_method_get_collider_velocity>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|         |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collision_count<class_PhysicsTestMotionResult3D_method_get_collision_count>`\ (\ ) |const|                                                          |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_collision_depth<class_PhysicsTestMotionResult3D_method_get_collision_depth>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|             |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_collision_local_shape<class_PhysicsTestMotionResult3D_method_get_collision_local_shape>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_collision_normal<class_PhysicsTestMotionResult3D_method_get_collision_normal>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|           |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_collision_point<class_PhysicsTestMotionResult3D_method_get_collision_point>`\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const|             |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_collision_safe_fraction<class_PhysicsTestMotionResult3D_method_get_collision_safe_fraction>`\ (\ ) |const|                                          |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_collision_unsafe_fraction<class_PhysicsTestMotionResult3D_method_get_collision_unsafe_fraction>`\ (\ ) |const|                                      |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_remainder<class_PhysicsTestMotionResult3D_method_get_remainder>`\ (\ ) |const|                                                                      |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`get_travel<class_PhysicsTestMotionResult3D_method_get_travel>`\ (\ ) |const|                                                                            |
   +-------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_PhysicsTestMotionResult3D_method_get_collider:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_collider**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collider>`

Trả về :ref:`Object<class_Object>` được gắn vào body đang va chạm với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collider_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collider_id**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collider_id>`

Trả về ID instance duy nhất của :ref:`Object<class_Object>` được gắn vào body đang va chạm với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm. Xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collider_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_collider_rid**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collider_rid>`

Trả về :ref:`RID<class_RID>` của body đang va chạm được :ref:`PhysicsServer3D<class_PhysicsServer3D>` sử dụng với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collider_shape:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collider_shape**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collider_shape>`

Trả về chỉ số shape của body đang va chạm với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm. Xem :ref:`CollisionObject3D<class_CollisionObject3D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collider_velocity:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_collider_velocity**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collider_velocity>`

Trả về vận tốc của body đang va chạm với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collision_count**\ (\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_count>`

Trả về số lượng va chạm được phát hiện.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_depth:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_collision_depth**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_depth>`

Trả về độ dài phần chồng lấn theo pháp tuyến va chạm với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_local_shape:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_collision_local_shape**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_local_shape>`

Trả về shape đang va chạm của object đang di chuyển với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_normal:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_collision_normal**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_normal>`

Trả về pháp tuyến của shape thuộc body đang va chạm tại điểm va chạm với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_point:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_collision_point**\ (\ collision_index\: :ref:`int<class_int>` = 0\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_point>`

Trả về điểm va chạm trong tọa độ toàn cục với chỉ số va chạm đã cho (mặc định là va chạm sâu nhất), nếu đã xảy ra va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_safe_fraction:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_collision_safe_fraction**\ (\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_safe_fraction>`

Trả về phần phân số tối đa của chuyển động có thể diễn ra mà không xảy ra va chạm, nằm giữa ``0`` và ``1``.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_collision_unsafe_fraction:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_collision_unsafe_fraction**\ (\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_collision_unsafe_fraction>`

Trả về phần phân số tối thiểu của chuyển động cần thiết để xảy ra va chạm, nếu đã xảy ra va chạm, nằm giữa ``0`` và ``1``.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_remainder:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_remainder**\ (\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_remainder>`

Trả về vector chuyển động còn lại của object đang di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsTestMotionResult3D_method_get_travel:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_travel**\ (\ ) |const| :ref:`🔗<class_PhysicsTestMotionResult3D_method_get_travel>`

Trả về quãng đường object đang di chuyển đã đi trước khi va chạm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
