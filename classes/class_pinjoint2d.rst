:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PinJoint2D.xml.

.. _class_PinJoint2D:

PinJoint2D
==========

**Kế thừa:** :ref:`Joint2D<class_Joint2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics joint gắn hai physics body 2D tại một điểm duy nhất, cho phép chúng tự do xoay.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một physics joint gắn hai physics body 2D tại một điểm duy nhất, cho phép chúng tự do xoay. Ví dụ: có thể gắn một :ref:`RigidBody2D<class_RigidBody2D>` vào một :ref:`StaticBody2D<class_StaticBody2D>` để tạo ra con lắc hoặc bập bênh.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`angular_limit_enabled<class_PinJoint2D_property_angular_limit_enabled>` | ``false`` |
   +---------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_lower<class_PinJoint2D_property_angular_limit_lower>`     | ``0.0``   |
   +---------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`angular_limit_upper<class_PinJoint2D_property_angular_limit_upper>`     | ``0.0``   |
   +---------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`motor_enabled<class_PinJoint2D_property_motor_enabled>`                 | ``false`` |
   +---------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`motor_target_velocity<class_PinJoint2D_property_motor_target_velocity>` | ``0.0``   |
   +---------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`softness<class_PinJoint2D_property_softness>`                           | ``0.0``   |
   +---------------------------+-------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PinJoint2D_property_angular_limit_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_limit_enabled** = ``false`` :ref:`🔗<class_PinJoint2D_property_angular_limit_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_angular_limit_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_angular_limit_enabled**\ (\ )

Nếu ``true``, góc xoay tối đa và tối thiểu của pin, được xác định bởi :ref:`angular_limit_lower<class_PinJoint2D_property_angular_limit_lower>` và :ref:`angular_limit_upper<class_PinJoint2D_property_angular_limit_upper>`, sẽ được áp dụng.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint2D_property_angular_limit_lower:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_lower** = ``0.0`` :ref:`🔗<class_PinJoint2D_property_angular_limit_lower>`

.. rst-class:: classref-property-setget

- |void| **set_angular_limit_lower**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angular_limit_lower**\ (\ )

Góc xoay tối thiểu. Chỉ hoạt động nếu :ref:`angular_limit_enabled<class_PinJoint2D_property_angular_limit_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint2D_property_angular_limit_upper:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit_upper** = ``0.0`` :ref:`🔗<class_PinJoint2D_property_angular_limit_upper>`

.. rst-class:: classref-property-setget

- |void| **set_angular_limit_upper**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angular_limit_upper**\ (\ )

Góc xoay tối đa. Chỉ hoạt động nếu :ref:`angular_limit_enabled<class_PinJoint2D_property_angular_limit_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint2D_property_motor_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **motor_enabled** = ``false`` :ref:`🔗<class_PinJoint2D_property_motor_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_motor_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_motor_enabled**\ (\ )

Khi được kích hoạt, một motor sẽ làm pin xoay.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint2D_property_motor_target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **motor_target_velocity** = ``0.0`` :ref:`🔗<class_PinJoint2D_property_motor_target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_motor_target_velocity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_motor_target_velocity**\ (\ )

Tốc độ mục tiêu của motor. Tính bằng radian trên giây.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint2D_property_softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **softness** = ``0.0`` :ref:`🔗<class_PinJoint2D_property_softness>`

.. rst-class:: classref-property-setget

- |void| **set_softness**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_softness**\ (\ )

Giá trị này càng cao thì liên kết với đối tượng được ghim càng có thể uốn cong.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
