:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsRayQueryParameters2D.xml.

.. _class_PhysicsRayQueryParameters2D:

PhysicsRayQueryParameters2D
===========================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho :ref:`PhysicsDirectSpaceState2D.intersect_ray()<class_PhysicsDirectSpaceState2D_method_intersect_ray>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi các thuộc tính khác nhau của đối tượng này, chẳng hạn như vị trí của ray, bạn có thể cấu hình các tham số cho :ref:`PhysicsDirectSpaceState2D.intersect_ray()<class_PhysicsDirectSpaceState2D_method_intersect_ray>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_areas<class_PhysicsRayQueryParameters2D_property_collide_with_areas>`   | ``false``         |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_bodies<class_PhysicsRayQueryParameters2D_property_collide_with_bodies>` | ``true``          |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                              | :ref:`collision_mask<class_PhysicsRayQueryParameters2D_property_collision_mask>`           | ``4294967295``    |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] | :ref:`exclude<class_PhysicsRayQueryParameters2D_property_exclude>`                         | ``[]``            |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`from<class_PhysicsRayQueryParameters2D_property_from>`                               | ``Vector2(0, 0)`` |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                            | :ref:`hit_from_inside<class_PhysicsRayQueryParameters2D_property_hit_from_inside>`         | ``false``         |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`to<class_PhysicsRayQueryParameters2D_property_to>`                                   | ``Vector2(0, 0)`` |
   +----------------------------------------------------+--------------------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PhysicsRayQueryParameters2D<class_PhysicsRayQueryParameters2D>` | :ref:`create<class_PhysicsRayQueryParameters2D_method_create>`\ (\ from\: :ref:`Vector2<class_Vector2>`, to\: :ref:`Vector2<class_Vector2>`, collision_mask\: :ref:`int<class_int>` = 4294967295, exclude\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] = []\ ) |static| |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsRayQueryParameters2D_property_collide_with_areas:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_areas** = ``false`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_collide_with_areas>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_areas**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_areas_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ tính đến :ref:`Area2D<class_Area2D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsRayQueryParameters2D_property_collide_with_bodies:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_bodies** = ``true`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_collide_with_bodies>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_bodies**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_bodies_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ tính đến :ref:`PhysicsBody2D<class_PhysicsBody2D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsRayQueryParameters2D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``4294967295`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà truy vấn sẽ phát hiện (dưới dạng bitmask). Theo mặc định, tất cả collision layer đều được phát hiện. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsRayQueryParameters2D_property_exclude:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **exclude** = ``[]`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_exclude>`

.. rst-class:: classref-property-setget

- |void| **set_exclude**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_exclude**\ (\ )

Danh sách các object :ref:`RID<class_RID>`\ s sẽ bị loại trừ khỏi các va chạm. Sử dụng :ref:`CollisionObject2D.get_rid()<class_CollisionObject2D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node bắt nguồn từ :ref:`CollisionObject2D<class_CollisionObject2D>`.

\ **Lưu ý:** Mảng được trả về là một bản sao và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về rồi gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsRayQueryParameters2D_property_from:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **from** = ``Vector2(0, 0)`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_from>`

.. rst-class:: classref-property-setget

- |void| **set_from**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_from**\ (\ )

Điểm bắt đầu của ray đang được truy vấn, trong tọa độ toàn cục.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsRayQueryParameters2D_property_hit_from_inside:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **hit_from_inside** = ``false`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_hit_from_inside>`

.. rst-class:: classref-property-setget

- |void| **set_hit_from_inside**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_hit_from_inside_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ phát hiện va chạm khi bắt đầu bên trong các shape. Trong trường hợp này, collision normal sẽ là ``Vector2(0, 0)``. Không ảnh hưởng đến các shape đa giác lõm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsRayQueryParameters2D_property_to:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **to** = ``Vector2(0, 0)`` :ref:`🔗<class_PhysicsRayQueryParameters2D_property_to>`

.. rst-class:: classref-property-setget

- |void| **set_to**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_to**\ (\ )

Điểm kết thúc của ray đang được truy vấn, trong tọa độ toàn cục.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicsRayQueryParameters2D_method_create:

.. rst-class:: classref-method

:ref:`PhysicsRayQueryParameters2D<class_PhysicsRayQueryParameters2D>` **create**\ (\ from\: :ref:`Vector2<class_Vector2>`, to\: :ref:`Vector2<class_Vector2>`, collision_mask\: :ref:`int<class_int>` = 4294967295, exclude\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] = []\ ) |static| :ref:`🔗<class_PhysicsRayQueryParameters2D_method_create>`

Trả về một đối tượng **PhysicsRayQueryParameters2D** mới đã được cấu hình sẵn. Sử dụng đối tượng này để nhanh chóng tạo các tham số truy vấn bằng những tùy chọn phổ biến nhất.

::

    var query = PhysicsRayQueryParameters2D.create(global_position, global_position + Vector2(0, 100))
    var collision = get_world_2d().direct_space_state.intersect_ray(query)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
