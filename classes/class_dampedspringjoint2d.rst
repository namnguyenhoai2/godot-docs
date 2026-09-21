:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/DampedSpringJoint2D.xml.

.. _class_DampedSpringJoint2D:

DampedSpringJoint2D
===================

**Kế thừa:** :ref:`Joint2D<class_Joint2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics joint kết nối hai physics body 2D bằng một lực giống như lò xo.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một physics joint kết nối hai physics body 2D bằng một lực giống như lò xo. Nó hoạt động như một lò xo luôn muốn kéo giãn đến một độ dài nhất định.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`damping<class_DampedSpringJoint2D_property_damping>`         | ``1.0``  |
   +---------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`length<class_DampedSpringJoint2D_property_length>`           | ``50.0`` |
   +---------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`rest_length<class_DampedSpringJoint2D_property_rest_length>` | ``0.0``  |
   +---------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`stiffness<class_DampedSpringJoint2D_property_stiffness>`     | ``20.0`` |
   +---------------------------+--------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_DampedSpringJoint2D_property_damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **damping** = ``1.0`` :ref:`🔗<class_DampedSpringJoint2D_property_damping>`

.. rst-class:: classref-property-setget

- |void| **set_damping**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_damping**\ (\ )

Tỷ số damping của spring joint. Một giá trị nằm giữa ``0`` và ``1``. Khi hai body chuyển động theo các hướng khác nhau, hệ thống cố gắng căn chỉnh chúng lại theo trục của lò xo. Giá trị :ref:`damping<class_DampedSpringJoint2D_property_damping>` cao khiến các body được gắn căn chỉnh nhanh hơn.

.. rst-class:: classref-item-separator

----

.. _class_DampedSpringJoint2D_property_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **length** = ``50.0`` :ref:`🔗<class_DampedSpringJoint2D_property_length>`

.. rst-class:: classref-property-setget

- |void| **set_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_length**\ (\ )

Độ dài tối đa của spring joint. Hai body được gắn không thể kéo giãn nó vượt quá giá trị này.

.. rst-class:: classref-item-separator

----

.. _class_DampedSpringJoint2D_property_rest_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **rest_length** = ``0.0`` :ref:`🔗<class_DampedSpringJoint2D_property_rest_length>`

.. rst-class:: classref-property-setget

- |void| **set_rest_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rest_length**\ (\ )

Khi các body được gắn vào spring joint chuyển động, chúng kéo giãn hoặc nén nó. Joint luôn cố gắng điều chỉnh kích thước về độ dài này.

.. rst-class:: classref-item-separator

----

.. _class_DampedSpringJoint2D_property_stiffness:

.. rst-class:: classref-property

:ref:`float<class_float>` **stiffness** = ``20.0`` :ref:`🔗<class_DampedSpringJoint2D_property_stiffness>`

.. rst-class:: classref-property-setget

- |void| **set_stiffness**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_stiffness**\ (\ )

Giá trị càng cao thì các body được gắn vào joint càng ít làm biến dạng nó. Joint tác dụng một lực ngược lên các body, bằng tích của stiffness với độ chênh lệch kích thước so với độ dài nghỉ của nó.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
