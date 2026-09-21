:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PinJoint3D.xml.

.. _class_PinJoint3D:

PinJoint3D
==========

**Kế thừa:** :ref:`Joint3D<class_Joint3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics joint gắn hai physics body 3D tại một điểm duy nhất, cho phép chúng tự do xoay.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một physics joint gắn hai physics body 3D tại một điểm duy nhất, cho phép chúng tự do xoay. Ví dụ: một :ref:`RigidBody3D<class_RigidBody3D>` có thể được gắn vào một :ref:`StaticBody3D<class_StaticBody3D>` để tạo thành con lắc hoặc bập bênh.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`params/bias<class_PinJoint3D_property_params/bias>`                   | ``0.3`` |
   +---------------------------+-----------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`params/damping<class_PinJoint3D_property_params/damping>`             | ``1.0`` |
   +---------------------------+-----------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`params/impulse_clamp<class_PinJoint3D_property_params/impulse_clamp>` | ``0.0`` |
   +---------------------------+-----------------------------------------------------------------------------+---------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param<class_PinJoint3D_method_get_param>`\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`\ ) |const|                            |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param<class_PinJoint3D_method_set_param>`\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_PinJoint3D_Param:

.. rst-class:: classref-enumeration

enum **Param**: :ref:`🔗<enum_PinJoint3D_Param>`

.. _class_PinJoint3D_constant_PARAM_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_PinJoint3D_Param>` **PARAM_BIAS** = ``0``

Lực giữ các object được ghim duy trì mối quan hệ về vị trí với nhau. Giá trị càng cao thì lực càng mạnh.

.. _class_PinJoint3D_constant_PARAM_DAMPING:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_PinJoint3D_Param>` **PARAM_DAMPING** = ``1``

Lực giữ các object được ghim duy trì mối quan hệ về vận tốc với nhau. Giá trị càng cao thì lực càng mạnh.

.. _class_PinJoint3D_constant_PARAM_IMPULSE_CLAMP:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_PinJoint3D_Param>` **PARAM_IMPULSE_CLAMP** = ``2``

Nếu lớn hơn 0, giá trị này là giá trị tối đa của impulse mà Joint3D này tạo ra.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PinJoint3D_property_params/bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **params/bias** = ``0.3`` :ref:`🔗<class_PinJoint3D_property_params/bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`\ ) |const|

Lực giữ các object được ghim duy trì mối quan hệ về vị trí với nhau. Giá trị càng cao thì lực càng mạnh.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint3D_property_params/damping:

.. rst-class:: classref-property

:ref:`float<class_float>` **params/damping** = ``1.0`` :ref:`🔗<class_PinJoint3D_property_params/damping>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`\ ) |const|

Lực giữ các object được ghim duy trì mối quan hệ về vận tốc với nhau. Giá trị càng cao thì lực càng mạnh.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint3D_property_params/impulse_clamp:

.. rst-class:: classref-property

:ref:`float<class_float>` **params/impulse_clamp** = ``0.0`` :ref:`🔗<class_PinJoint3D_property_params/impulse_clamp>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`\ ) |const|

Nếu lớn hơn 0, giá trị này là giá trị tối đa của impulse mà Joint3D này tạo ra.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PinJoint3D_method_get_param:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`\ ) |const| :ref:`🔗<class_PinJoint3D_method_get_param>`

Trả về giá trị của parameter được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_PinJoint3D_method_set_param:

.. rst-class:: classref-method

|void| **set_param**\ (\ param\: :ref:`Param<enum_PinJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_PinJoint3D_method_set_param>`

Thiết lập giá trị của parameter được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
