:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Joint3D.xml.

.. _class_Joint3D:

Joint3D
=======

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ConeTwistJoint3D<class_ConeTwistJoint3D>`, :ref:`Generic6DOFJoint3D<class_Generic6DOFJoint3D>`, :ref:`HingeJoint3D<class_HingeJoint3D>`, :ref:`PinJoint3D<class_PinJoint3D>`, :ref:`SliderJoint3D<class_SliderJoint3D>`

Lớp cơ sở trừu tượng cho tất cả các joint vật lý 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở trừu tượng cho tất cả các joint trong vật lý 3D. Các joint 3D liên kết hai physics body (:ref:`node_a<class_Joint3D_property_node_a>` và :ref:`node_b<class_Joint3D_property_node_b>`) với nhau và áp dụng một constraint. Nếu chỉ xác định một body, body đó sẽ được gắn vào một :ref:`StaticBody3D<class_StaticBody3D>` cố định không có collision shape.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D Truck Town Demo <https://godotengine.org/asset-library/asset/2752>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+------------------------------------------------------------------------------------------+------------------+
   | :ref:`bool<class_bool>`         | :ref:`exclude_nodes_from_collision<class_Joint3D_property_exclude_nodes_from_collision>` | ``true``         |
   +---------------------------------+------------------------------------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`node_a<class_Joint3D_property_node_a>`                                             | ``NodePath("")`` |
   +---------------------------------+------------------------------------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`node_b<class_Joint3D_property_node_b>`                                             | ``NodePath("")`` |
   +---------------------------------+------------------------------------------------------------------------------------------+------------------+
   | :ref:`int<class_int>`           | :ref:`solver_priority<class_Joint3D_property_solver_priority>`                           | ``1``            |
   +---------------------------------+------------------------------------------------------------------------------------------+------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------+------------------------------------------------------------+
   | :ref:`RID<class_RID>` | :ref:`get_rid<class_Joint3D_method_get_rid>`\ (\ ) |const| |
   +-----------------------+------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Joint3D_property_exclude_nodes_from_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **exclude_nodes_from_collision** = ``true`` :ref:`🔗<class_Joint3D_property_exclude_nodes_from_collision>`

.. rst-class:: classref-property-setget

- |void| **set_exclude_nodes_from_collision**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_exclude_nodes_from_collision**\ (\ )

Nếu ``true``, hai body được liên kết với nhau sẽ không va chạm với nhau.

.. rst-class:: classref-item-separator

----

.. _class_Joint3D_property_node_a:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **node_a** = ``NodePath("")`` :ref:`🔗<class_Joint3D_property_node_a>`

.. rst-class:: classref-property-setget

- |void| **set_node_a**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_node_a**\ (\ )

Đường dẫn đến node đầu tiên (A) được gắn vào joint. Node này phải kế thừa :ref:`PhysicsBody3D<class_PhysicsBody3D>`.

Nếu để trống và :ref:`node_b<class_Joint3D_property_node_b>` được thiết lập, body sẽ được gắn vào một :ref:`StaticBody3D<class_StaticBody3D>` cố định không có collision shape.

.. rst-class:: classref-item-separator

----

.. _class_Joint3D_property_node_b:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **node_b** = ``NodePath("")`` :ref:`🔗<class_Joint3D_property_node_b>`

.. rst-class:: classref-property-setget

- |void| **set_node_b**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_node_b**\ (\ )

Đường dẫn đến node thứ hai (B) được gắn vào joint. Node này phải kế thừa :ref:`PhysicsBody3D<class_PhysicsBody3D>`.

Nếu để trống và :ref:`node_a<class_Joint3D_property_node_a>` được thiết lập, body sẽ được gắn vào một :ref:`StaticBody3D<class_StaticBody3D>` cố định không có collision shape.

.. rst-class:: classref-item-separator

----

.. _class_Joint3D_property_solver_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **solver_priority** = ``1`` :ref:`🔗<class_Joint3D_property_solver_priority>`

.. rst-class:: classref-property-setget

- |void| **set_solver_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_solver_priority**\ (\ )

Mức ưu tiên được dùng để xác định solver nào được thực thi trước đối với nhiều joint. Giá trị càng thấp thì mức ưu tiên càng cao.

\ **Lưu ý:** Chỉ được hỗ trợ khi sử dụng GodotPhysics3D. Thuộc tính này bị bỏ qua khi sử dụng Jolt Physics.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Joint3D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_Joint3D_method_get_rid>`

Trả về :ref:`RID<class_RID>` nội bộ của joint từ :ref:`PhysicsServer3D<class_PhysicsServer3D>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
