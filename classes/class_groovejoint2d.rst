:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GrooveJoint2D.xml.

.. _class_GrooveJoint2D:

GrooveJoint2D
=============

**Kế thừa:** :ref:`Joint2D<class_Joint2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một khớp vật lý giới hạn chuyển động của hai body vật lý 2D trên một trục cố định.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một khớp vật lý giới hạn chuyển động của hai body vật lý 2D trên một trục cố định. Ví dụ, một :ref:`StaticBody2D<class_StaticBody2D>` đại diện cho đế piston có thể được gắn với một :ref:`RigidBody2D<class_RigidBody2D>` đại diện cho đầu piston để chuyển động lên xuống.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`initial_offset<class_GrooveJoint2D_property_initial_offset>` | ``25.0`` |
   +---------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`length<class_GrooveJoint2D_property_length>`                 | ``50.0`` |
   +---------------------------+--------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GrooveJoint2D_property_initial_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **initial_offset** = ``25.0`` :ref:`🔗<class_GrooveJoint2D_property_initial_offset>`

.. rst-class:: classref-property-setget

- |void| **set_initial_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_initial_offset**\ (\ )

Vị trí neo ban đầu của body B, được xác định bởi gốc của joint và một offset cục bộ :ref:`initial_offset<class_GrooveJoint2D_property_initial_offset>` dọc theo trục Y của joint (dọc theo rãnh).

.. rst-class:: classref-item-separator

----

.. _class_GrooveJoint2D_property_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **length** = ``50.0`` :ref:`🔗<class_GrooveJoint2D_property_length>`

.. rst-class:: classref-property-setget

- |void| **set_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_length**\ (\ )

Độ dài của rãnh. Rãnh kéo dài từ gốc của joint về phía :ref:`length<class_GrooveJoint2D_property_length>` dọc theo trục Y cục bộ của joint.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
