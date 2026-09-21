:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Joint2D.xml.

.. _class_Joint2D:

Joint2D
=======

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`DampedSpringJoint2D<class_DampedSpringJoint2D>`, :ref:`GrooveJoint2D<class_GrooveJoint2D>`, :ref:`PinJoint2D<class_PinJoint2D>`

Lớp cơ sở trừu tượng cho tất cả joint vật lý 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở trừu tượng cho tất cả joint trong vật lý 2D. Các joint 2D liên kết hai physics body (:ref:`node_a<class_Joint2D_property_node_a>` và :ref:`node_b<class_Joint2D_property_node_b>`) với nhau và áp dụng một constraint.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------+--------------------------------------------------------------------+------------------+
   | :ref:`float<class_float>`       | :ref:`bias<class_Joint2D_property_bias>`                           | ``0.0``          |
   +---------------------------------+--------------------------------------------------------------------+------------------+
   | :ref:`bool<class_bool>`         | :ref:`disable_collision<class_Joint2D_property_disable_collision>` | ``true``         |
   +---------------------------------+--------------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`node_a<class_Joint2D_property_node_a>`                       | ``NodePath("")`` |
   +---------------------------------+--------------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`node_b<class_Joint2D_property_node_b>`                       | ``NodePath("")`` |
   +---------------------------------+--------------------------------------------------------------------+------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------+------------------------------------------------------------+
   | :ref:`RID<class_RID>` | :ref:`get_rid<class_Joint2D_method_get_rid>`\ (\ ) |const| |
   +-----------------------+------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Joint2D_property_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **bias** = ``0.0`` :ref:`🔗<class_Joint2D_property_bias>`

.. rst-class:: classref-property-setget

- |void| **set_bias**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bias**\ (\ )

Khi :ref:`node_a<class_Joint2D_property_node_a>` và :ref:`node_b<class_Joint2D_property_node_b>` di chuyển theo các hướng khác nhau, :ref:`bias<class_Joint2D_property_bias>` sẽ kiểm soát tốc độ joint kéo chúng trở lại vị trí ban đầu. :ref:`bias<class_Joint2D_property_bias>` càng thấp thì hai body càng có thể kéo lên joint.

Khi được đặt thành ``0``, giá trị mặc định từ :ref:`ProjectSettings.physics/2d/solver/default_constraint_bias<class_ProjectSettings_property_physics/2d/solver/default_constraint_bias>` sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_Joint2D_property_disable_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disable_collision** = ``true`` :ref:`🔗<class_Joint2D_property_disable_collision>`

.. rst-class:: classref-property-setget

- |void| **set_exclude_nodes_from_collision**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_exclude_nodes_from_collision**\ (\ )

Nếu ``true``, hai body được liên kết với nhau sẽ không va chạm với nhau.

.. rst-class:: classref-item-separator

----

.. _class_Joint2D_property_node_a:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **node_a** = ``NodePath("")`` :ref:`🔗<class_Joint2D_property_node_a>`

.. rst-class:: classref-property-setget

- |void| **set_node_a**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_node_a**\ (\ )

Đường dẫn đến body thứ nhất (A) được gắn vào joint. Node này phải kế thừa :ref:`PhysicsBody2D<class_PhysicsBody2D>`.

.. rst-class:: classref-item-separator

----

.. _class_Joint2D_property_node_b:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **node_b** = ``NodePath("")`` :ref:`🔗<class_Joint2D_property_node_b>`

.. rst-class:: classref-property-setget

- |void| **set_node_b**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_node_b**\ (\ )

Đường dẫn đến body thứ hai (B) được gắn vào joint. Node này phải kế thừa :ref:`PhysicsBody2D<class_PhysicsBody2D>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Joint2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_Joint2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` nội bộ của joint từ :ref:`PhysicsServer2D<class_PhysicsServer2D>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
