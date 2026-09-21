:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/HingeJoint3D.xml.

.. _class_HingeJoint3D:

HingeJoint3D
============

**Kế thừa:** :ref:`Joint3D<class_Joint3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics joint giới hạn chuyển động quay của một physics body 3D quanh một trục tương đối với một physics body khác.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một physics joint giới hạn chuyển động quay của một physics body 3D quanh một trục tương đối với một physics body khác. Ví dụ, Body A có thể là một :ref:`StaticBody3D<class_StaticBody3D>` đại diện cho bản lề cửa mà một :ref:`RigidBody3D<class_RigidBody3D>` quay quanh.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`angular_limit/bias<class_HingeJoint3D_property_angular_limit/bias>`             | ``0.3``        |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`bool<class_bool>`   | :ref:`angular_limit/enable<class_HingeJoint3D_property_angular_limit/enable>`         | ``false``      |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`angular_limit/lower<class_HingeJoint3D_property_angular_limit/lower>`           | ``-1.5707964`` |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`angular_limit/relaxation<class_HingeJoint3D_property_angular_limit/relaxation>` | ``1.0``        |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`angular_limit/softness<class_HingeJoint3D_property_angular_limit/softness>`     | ``0.9``        |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`angular_limit/upper<class_HingeJoint3D_property_angular_limit/upper>`           | ``1.5707964``  |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`bool<class_bool>`   | :ref:`motor/enable<class_HingeJoint3D_property_motor/enable>`                         | ``false``      |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`motor/max_impulse<class_HingeJoint3D_property_motor/max_impulse>`               | ``1.0``        |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`motor/target_velocity<class_HingeJoint3D_property_motor/target_velocity>`       | ``1.0``        |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`params/bias<class_HingeJoint3D_property_params/bias>`                           | ``0.3``        |
   +---------------------------+---------------------------------------------------------------------------------------+----------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`   | :ref:`get_flag<class_HingeJoint3D_method_get_flag>`\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`\ ) |const|                                 |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param<class_HingeJoint3D_method_get_param>`\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|                            |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_flag<class_HingeJoint3D_method_set_flag>`\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`, enabled\: :ref:`bool<class_bool>`\ )      |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param<class_HingeJoint3D_method_set_param>`\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_HingeJoint3D_Param:

.. rst-class:: classref-enumeration

enum **Param**: :ref:`🔗<enum_HingeJoint3D_Param>`

.. _class_HingeJoint3D_constant_PARAM_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_BIAS** = ``0``

Tốc độ mà hai body được kéo lại gần nhau khi chúng chuyển động theo các hướng khác nhau.

.. _class_HingeJoint3D_constant_PARAM_LIMIT_UPPER:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_LIMIT_UPPER** = ``1``

Góc quay tối đa. Chỉ hoạt động nếu :ref:`angular_limit/enable<class_HingeJoint3D_property_angular_limit/enable>` là ``true``.

.. _class_HingeJoint3D_constant_PARAM_LIMIT_LOWER:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_LIMIT_LOWER** = ``2``

Góc quay tối thiểu. Chỉ hoạt động nếu :ref:`angular_limit/enable<class_HingeJoint3D_property_angular_limit/enable>` là ``true``.

.. _class_HingeJoint3D_constant_PARAM_LIMIT_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_LIMIT_BIAS** = ``3``

Tốc độ hiệu chỉnh chuyển động quay trên trục vuông góc với bản lề.

.. _class_HingeJoint3D_constant_PARAM_LIMIT_SOFTNESS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_LIMIT_SOFTNESS** = ``4``

**Đã deprecated:** Thuộc tính này không bao giờ được engine sử dụng và được giữ lại vì mục đích tương thích.



.. _class_HingeJoint3D_constant_PARAM_LIMIT_RELAXATION:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_LIMIT_RELAXATION** = ``5``

Giá trị này càng thấp thì chuyển động quay càng bị giảm tốc nhiều hơn.

.. _class_HingeJoint3D_constant_PARAM_MOTOR_TARGET_VELOCITY:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_MOTOR_TARGET_VELOCITY** = ``6``

Tốc độ mục tiêu của motor.

.. _class_HingeJoint3D_constant_PARAM_MOTOR_MAX_IMPULSE:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_MOTOR_MAX_IMPULSE** = ``7``

Gia tốc tối đa của motor.

.. _class_HingeJoint3D_constant_PARAM_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_HingeJoint3D_Param>` **PARAM_MAX** = ``8``

Đại diện cho kích thước của enum :ref:`Param<enum_HingeJoint3D_Param>`.

.. rst-class:: classref-item-separator

----

.. _enum_HingeJoint3D_Flag:

.. rst-class:: classref-enumeration

enum **Flag**: :ref:`🔗<enum_HingeJoint3D_Flag>`

.. _class_HingeJoint3D_constant_FLAG_USE_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_HingeJoint3D_Flag>` **FLAG_USE_LIMIT** = ``0``

Nếu ``true``, góc quay tối đa và tối thiểu của bản lề, được xác định bởi :ref:`angular_limit/lower<class_HingeJoint3D_property_angular_limit/lower>` và :ref:`angular_limit/upper<class_HingeJoint3D_property_angular_limit/upper>`, sẽ có hiệu lực.

.. _class_HingeJoint3D_constant_FLAG_ENABLE_MOTOR:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_HingeJoint3D_Flag>` **FLAG_ENABLE_MOTOR** = ``1``

Khi được kích hoạt, một motor sẽ quay bản lề.

.. _class_HingeJoint3D_constant_FLAG_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Flag<enum_HingeJoint3D_Flag>` **FLAG_MAX** = ``2``

Đại diện cho kích thước của enum :ref:`Flag<enum_HingeJoint3D_Flag>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_HingeJoint3D_property_angular_limit/bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit/bias** = ``0.3`` :ref:`🔗<class_HingeJoint3D_property_angular_limit/bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Tốc độ hiệu chỉnh chuyển động quay trên trục vuông góc với bản lề.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_angular_limit/enable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **angular_limit/enable** = ``false`` :ref:`🔗<class_HingeJoint3D_property_angular_limit/enable>`

.. rst-class:: classref-property-setget

- |void| **set_flag**\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag**\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`\ ) |const|

Nếu ``true``, góc quay tối đa và tối thiểu của bản lề, được xác định bởi :ref:`angular_limit/lower<class_HingeJoint3D_property_angular_limit/lower>` và :ref:`angular_limit/upper<class_HingeJoint3D_property_angular_limit/upper>`, sẽ có hiệu lực.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_angular_limit/lower:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit/lower** = ``-1.5707964`` :ref:`🔗<class_HingeJoint3D_property_angular_limit/lower>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Góc quay tối thiểu. Chỉ hoạt động nếu :ref:`angular_limit/enable<class_HingeJoint3D_property_angular_limit/enable>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_angular_limit/relaxation:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit/relaxation** = ``1.0`` :ref:`🔗<class_HingeJoint3D_property_angular_limit/relaxation>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Giá trị này càng thấp thì chuyển động quay càng bị giảm tốc nhiều hơn.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_angular_limit/softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit/softness** = ``0.9`` :ref:`🔗<class_HingeJoint3D_property_angular_limit/softness>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

**Đã deprecated:** Thuộc tính này không bao giờ được engine thiết lập và được giữ lại vì mục đích tương thích.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_angular_limit/upper:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_limit/upper** = ``1.5707964`` :ref:`🔗<class_HingeJoint3D_property_angular_limit/upper>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Góc quay tối đa. Chỉ hoạt động nếu :ref:`angular_limit/enable<class_HingeJoint3D_property_angular_limit/enable>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_motor/enable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **motor/enable** = ``false`` :ref:`🔗<class_HingeJoint3D_property_motor/enable>`

.. rst-class:: classref-property-setget

- |void| **set_flag**\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`, enabled\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flag**\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`\ ) |const|

Khi được kích hoạt, một motor sẽ quay bản lề.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_motor/max_impulse:

.. rst-class:: classref-property

:ref:`float<class_float>` **motor/max_impulse** = ``1.0`` :ref:`🔗<class_HingeJoint3D_property_motor/max_impulse>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Gia tốc tối đa của motor.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_motor/target_velocity:

.. rst-class:: classref-property

:ref:`float<class_float>` **motor/target_velocity** = ``1.0`` :ref:`🔗<class_HingeJoint3D_property_motor/target_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Tốc độ mục tiêu của motor.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_property_params/bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **params/bias** = ``0.3`` :ref:`🔗<class_HingeJoint3D_property_params/bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const|

Tốc độ mà hai body được kéo lại gần nhau khi chúng chuyển động theo các hướng khác nhau.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_HingeJoint3D_method_get_flag:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_flag**\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`\ ) |const| :ref:`🔗<class_HingeJoint3D_method_get_flag>`

Trả về giá trị của flag được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_method_get_param:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`\ ) |const| :ref:`🔗<class_HingeJoint3D_method_get_param>`

Trả về giá trị của parameter được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_method_set_flag:

.. rst-class:: classref-method

|void| **set_flag**\ (\ flag\: :ref:`Flag<enum_HingeJoint3D_Flag>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_HingeJoint3D_method_set_flag>`

Nếu ``true``, bật flag được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_HingeJoint3D_method_set_param:

.. rst-class:: classref-method

|void| **set_param**\ (\ param\: :ref:`Param<enum_HingeJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_HingeJoint3D_method_set_param>`

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
