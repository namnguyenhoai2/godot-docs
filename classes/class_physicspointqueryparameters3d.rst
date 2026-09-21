:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsPointQueryParameters3D.xml.

.. _class_PhysicsPointQueryParameters3D:

PhysicsPointQueryParameters3D
=============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho :ref:`PhysicsDirectSpaceState3D.intersect_point()<class_PhysicsDirectSpaceState3D_method_intersect_point>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi nhiều thuộc tính khác nhau của đối tượng này, chẳng hạn như vị trí của điểm, bạn có thể cấu hình các tham số cho :ref:`PhysicsDirectSpaceState3D.intersect_point()<class_PhysicsDirectSpaceState3D_method_intersect_point>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_areas<class_PhysicsPointQueryParameters3D_property_collide_with_areas>`   | ``false``            |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_bodies<class_PhysicsPointQueryParameters3D_property_collide_with_bodies>` | ``true``             |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                              | :ref:`collision_mask<class_PhysicsPointQueryParameters3D_property_collision_mask>`           | ``4294967295``       |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] | :ref:`exclude<class_PhysicsPointQueryParameters3D_property_exclude>`                         | ``[]``               |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                      | :ref:`position<class_PhysicsPointQueryParameters3D_property_position>`                       | ``Vector3(0, 0, 0)`` |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsPointQueryParameters3D_property_collide_with_areas:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_areas** = ``false`` :ref:`🔗<class_PhysicsPointQueryParameters3D_property_collide_with_areas>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_areas**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_areas_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ tính đến :ref:`Area3D<class_Area3D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters3D_property_collide_with_bodies:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_bodies** = ``true`` :ref:`🔗<class_PhysicsPointQueryParameters3D_property_collide_with_bodies>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_bodies**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_bodies_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ tính đến :ref:`PhysicsBody3D<class_PhysicsBody3D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters3D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``4294967295`` :ref:`🔗<class_PhysicsPointQueryParameters3D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà truy vấn sẽ phát hiện (dưới dạng bitmask). Theo mặc định, tất cả collision layer đều được phát hiện. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters3D_property_exclude:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **exclude** = ``[]`` :ref:`🔗<class_PhysicsPointQueryParameters3D_property_exclude>`

.. rst-class:: classref-property-setget

- |void| **set_exclude**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_exclude**\ (\ )

Danh sách :ref:`RID<class_RID>`\ s của các đối tượng sẽ bị loại trừ khỏi các va chạm. Sử dụng :ref:`CollisionObject3D.get_rid()<class_CollisionObject3D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node dẫn xuất từ :ref:`CollisionObject3D<class_CollisionObject3D>`.

\ **Lưu ý:** Mảng được trả về là một bản sao và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về, sau đó gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsPointQueryParameters3D_property_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_PhysicsPointQueryParameters3D_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_position**\ (\ )

Vị trí được truy vấn, tính theo tọa độ toàn cục.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
