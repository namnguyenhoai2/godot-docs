:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsShapeQueryParameters2D.xml.

.. _class_PhysicsShapeQueryParameters2D:

PhysicsShapeQueryParameters2D
=============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp các tham số cho các phương thức của :ref:`PhysicsDirectSpaceState2D<class_PhysicsDirectSpaceState2D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bằng cách thay đổi nhiều thuộc tính khác nhau của đối tượng này, chẳng hạn như shape, bạn có thể cấu hình các tham số cho các phương thức của :ref:`PhysicsDirectSpaceState2D<class_PhysicsDirectSpaceState2D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_areas<class_PhysicsShapeQueryParameters2D_property_collide_with_areas>`   | ``false``                         |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`collide_with_bodies<class_PhysicsShapeQueryParameters2D_property_collide_with_bodies>` | ``true``                          |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                              | :ref:`collision_mask<class_PhysicsShapeQueryParameters2D_property_collision_mask>`           | ``4294967295``                    |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] | :ref:`exclude<class_PhysicsShapeQueryParameters2D_property_exclude>`                         | ``[]``                            |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`                          | :ref:`margin<class_PhysicsShapeQueryParameters2D_property_margin>`                           | ``0.0``                           |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`motion<class_PhysicsShapeQueryParameters2D_property_motion>`                           | ``Vector2(0, 0)``                 |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Resource<class_Resource>`                    | :ref:`shape<class_PhysicsShapeQueryParameters2D_property_shape>`                             |                                   |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`RID<class_RID>`                              | :ref:`shape_rid<class_PhysicsShapeQueryParameters2D_property_shape_rid>`                     | ``RID()``                         |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Transform2D<class_Transform2D>`              | :ref:`transform<class_PhysicsShapeQueryParameters2D_property_transform>`                     | ``Transform2D(1, 0, 0, 1, 0, 0)`` |
   +----------------------------------------------------+----------------------------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicsShapeQueryParameters2D_property_collide_with_areas:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_areas** = ``false`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_collide_with_areas>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_areas**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_areas_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ tính đến :ref:`Area2D<class_Area2D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_collide_with_bodies:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **collide_with_bodies** = ``true`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_collide_with_bodies>`

.. rst-class:: classref-property-setget

- |void| **set_collide_with_bodies**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_collide_with_bodies_enabled**\ (\ )

Nếu ``true``, truy vấn sẽ tính đến :ref:`PhysicsBody2D<class_PhysicsBody2D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``4294967295`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà truy vấn sẽ phát hiện (dưới dạng bitmask). Theo mặc định, tất cả collision layer đều được phát hiện. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_exclude:

.. rst-class:: classref-property

:ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **exclude** = ``[]`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_exclude>`

.. rst-class:: classref-property-setget

- |void| **set_exclude**\ (\ value\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\]\ ) - :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\] **get_exclude**\ (\ )

Danh sách các :ref:`RID<class_RID>`\ s sẽ bị loại trừ khỏi các va chạm. Sử dụng :ref:`CollisionObject2D.get_rid()<class_CollisionObject2D_method_get_rid>` để lấy :ref:`RID<class_RID>` liên kết với một node bắt nguồn từ :ref:`CollisionObject2D<class_CollisionObject2D>`.

\ **Lưu ý:** Mảng được trả về là một bản sao và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Để cập nhật giá trị, bạn cần sửa đổi mảng được trả về, sau đó gán lại mảng đó cho thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **margin** = ``0.0`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_margin>`

.. rst-class:: classref-property-setget

- |void| **set_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_margin**\ (\ )

margin va chạm của shape.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_motion:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **motion** = ``Vector2(0, 0)`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_motion>`

.. rst-class:: classref-property-setget

- |void| **set_motion**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_motion**\ (\ )

Chuyển động của shape đang được truy vấn.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_shape:

.. rst-class:: classref-property

:ref:`Resource<class_Resource>` **shape** :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_shape>`

.. rst-class:: classref-property-setget

- |void| **set_shape**\ (\ value\: :ref:`Resource<class_Resource>`\ ) - :ref:`Resource<class_Resource>` **get_shape**\ (\ )

:ref:`Shape2D<class_Shape2D>` sẽ được sử dụng cho các truy vấn va chạm/giao nhau. Đối tượng này lưu trữ tham chiếu thực tế, giúp shape không bị giải phóng trong khi được sử dụng cho các truy vấn, vì vậy hãy luôn ưu tiên sử dụng nó thay cho :ref:`shape_rid<class_PhysicsShapeQueryParameters2D_property_shape_rid>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_shape_rid:

.. rst-class:: classref-property

:ref:`RID<class_RID>` **shape_rid** = ``RID()`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_shape_rid>`

.. rst-class:: classref-property-setget

- |void| **set_shape_rid**\ (\ value\: :ref:`RID<class_RID>`\ ) - :ref:`RID<class_RID>` **get_shape_rid**\ (\ )

:ref:`RID<class_RID>` của shape được truy vấn, sẽ được sử dụng cho các truy vấn va chạm/giao nhau. Hãy sử dụng nó thay cho :ref:`shape<class_PhysicsShapeQueryParameters2D_property_shape>` nếu bạn muốn tối ưu hiệu năng bằng cách sử dụng Servers API:


.. tabs::

 .. code-tab:: gdscript

    var shape_rid = PhysicsServer2D.circle_shape_create()
    var radius = 64
    PhysicsServer2D.shape_set_data(shape_rid, radius)

    var params = PhysicsShapeQueryParameters2D.new()
    params.shape_rid = shape_rid

    # Thực thi các truy vấn physics tại đây...

    # Giải phóng shape khi hoàn tất các truy vấn physics.
    PhysicsServer2D.free_rid(shape_rid)

 .. code-tab:: csharp

    RID shapeRid = PhysicsServer2D.CircleShapeCreate();
    int radius = 64;
    PhysicsServer2D.ShapeSetData(shapeRid, radius);

    var params = new PhysicsShapeQueryParameters2D();
    params.ShapeRid = shapeRid;

    // Thực thi các truy vấn physics tại đây...

    // Giải phóng shape khi hoàn tất các truy vấn physics.
    PhysicsServer2D.FreeRid(shapeRid);



.. rst-class:: classref-item-separator

----

.. _class_PhysicsShapeQueryParameters2D_property_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **transform** = ``Transform2D(1, 0, 0, 1, 0, 0)`` :ref:`🔗<class_PhysicsShapeQueryParameters2D_property_transform>`

.. rst-class:: classref-property-setget

- |void| **set_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_transform**\ (\ )

Ma trận transform của shape được truy vấn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
