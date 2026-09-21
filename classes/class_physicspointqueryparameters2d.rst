:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsPointQueryParameters2D.xml.

.. _class_PhysicsPointQueryParameters2D:

PhysicsPointQueryParameters2D
=============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho :ref:`PhysicsDirectSpaceState2D.intersect_point()<class_PhysicsDirectSpaceState2D_method_intersect_point>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi các thuộc tính khác nhau của đối tượng này, chẳng hạn như vị trí điểm, bạn có thể cấu hình các tham số cho :ref:`PhysicsDirectSpaceState2D.intersect_point()<class_PhysicsDirectSpaceState2D_method_intersect_point>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                              | :ref:`canvas_instance_id<class_PhysicsPointQueryParameters2D_property_canvas_instance_id>`   | ``0``             |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_areas<class_PhysicsPointQueryParameters2D_property_collide_with_areas>`   | ``false``         |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_bodies<class_PhysicsPointQueryParameters2D_property_collide_with_bodies>` | ``true``          |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                              | :ref:`collision_mask<class_PhysicsPointQueryParameters2D_property_collision_mask>`           | ``4294967295``    |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] | :ref:`exclude<class_PhysicsPointQueryParameters2D_property_exclude>`                         | ``[]``            |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`position<class_PhysicsPointQueryParameters2D_property_position>`                       | ``Vector2(0, 0)`` |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsPointQueryParameters2D_property_canvas_instance_id:

.. rst-class:: classref-property

:ref:`int<class_int>` **canvas_instance_id** = ``0`` :ref:`🔗<class_PhysicsPointQueryParameters2D_property_canvas_instance_id>`

.. rst-class:: classref-property-setget

- |void| **set_canvas_instance_id**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_canvas_instance_id**\ (\ )

Nếu khác ``0``, giới hạn truy vấn vào một lớp canvas cụ thể được chỉ định bằng instance ID của nó. Xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`.

Nếu là ``0``, giới hạn truy vấn vào lớp canvas mặc định của Viewport.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters2D_property_collide_with_areas:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_areas** = ``false`` :ref:`🔗<class_PhysicsPointQueryParameters2D_property_collide_with_areas>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_areas**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_areas_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ xét đến :ref:`Area2D<class_Area2D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters2D_property_collide_with_bodies:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_bodies** = ``true`` :ref:`🔗<class_PhysicsPointQueryParameters2D_property_collide_with_bodies>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_bodies**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_bodies_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ xét đến :ref:`PhysicsBody2D<class_PhysicsBody2D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters2D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``4294967295`` :ref:`🔗<class_PhysicsPointQueryParameters2D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà truy vấn sẽ phát hiện (dưới dạng bitmask). Theo mặc định, tất cả collision layer đều được phát hiện. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters2D_property_exclude:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **exclude** = ``[]`` :ref:`🔗<class_PhysicsPointQueryParameters2D_property_exclude>`

.. rst-class:: classref-property-setget

- |void| **set_exclude**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_exclude**\ (\ )

Danh sách các object :ref:`RID<class_RID>`\ s sẽ bị loại trừ khỏi các va chạm. Sử dụng :ref:`CollisionObject2D.get_rid()<class_CollisionObject2D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node bắt nguồn từ :ref:`CollisionObject2D<class_CollisionObject2D>`.

\ **Lưu ý:** Mảng được trả về là một bản sao và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về, sau đó gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters2D_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_PhysicsPointQueryParameters2D_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Vị trí đang được truy vấn, theo tọa độ toàn cục.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
