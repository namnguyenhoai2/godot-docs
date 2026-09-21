:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ConeTwistJoint3D.xml.

.. _class_ConeTwistJoint3D:

ConeTwistJoint3D
================

**Kế thừa:** :ref:`Joint3D<class_Joint3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một khớp vật lý kết nối hai vật thể vật lý 3D theo cách mô phỏng khớp cầu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một khớp vật lý kết nối hai vật thể vật lý 3D theo cách mô phỏng khớp cầu. Trục xoắn ban đầu là trục X của **ConeTwistJoint3D**. Sau khi các vật thể vật lý đung đưa, trục xoắn được tính là điểm giữa của các trục X của khớp trong không gian cục bộ của hai vật thể vật lý. Hữu ích cho các chi như vai và hông, đèn treo trên trần nhà, v.v.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`bias<class_ConeTwistJoint3D_property_bias>`             | ``0.3``       |
   +---------------------------+---------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`relaxation<class_ConeTwistJoint3D_property_relaxation>` | ``1.0``       |
   +---------------------------+---------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`softness<class_ConeTwistJoint3D_property_softness>`     | ``0.8``       |
   +---------------------------+---------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`swing_span<class_ConeTwistJoint3D_property_swing_span>` | ``0.7853982`` |
   +---------------------------+---------------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`twist_span<class_ConeTwistJoint3D_property_twist_span>` | ``3.1415927`` |
   +---------------------------+---------------------------------------------------------------+---------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`get_param<class_ConeTwistJoint3D_method_get_param>`\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const|                            |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`set_param<class_ConeTwistJoint3D_method_set_param>`\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) |
   +---------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_ConeTwistJoint3D_Param:

.. rst-class:: classref-enumeration

enum **Param**: :ref:`🔗<enum_ConeTwistJoint3D_Param>`

.. _class_ConeTwistJoint3D_constant_PARAM_SWING_SPAN:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_ConeTwistJoint3D_Param>` **PARAM_SWING_SPAN** = ``0``

Swing là chuyển động xoay từ bên này sang bên kia, quanh trục vuông góc với trục twist.

Độ rộng swing xác định mức độ xoay sẽ không được hiệu chỉnh dọc theo trục swing.

Có thể hiểu đây là độ lỏng của **ConeTwistJoint3D**.

Nếu nhỏ hơn 0.05, hành vi này sẽ bị khóa.

.. _class_ConeTwistJoint3D_constant_PARAM_TWIST_SPAN:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_ConeTwistJoint3D_Param>` **PARAM_TWIST_SPAN** = ``1``

Twist là chuyển động xoay quanh trục twist; giá trị này xác định khớp có thể xoắn đến mức nào.

Twist bị khóa nếu nhỏ hơn 0.05.

.. _class_ConeTwistJoint3D_constant_PARAM_BIAS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_ConeTwistJoint3D_Param>` **PARAM_BIAS** = ``2``

Tốc độ thực hiện swing hoặc twist.

Giá trị càng cao thì tốc độ càng nhanh.

.. _class_ConeTwistJoint3D_constant_PARAM_SOFTNESS:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_ConeTwistJoint3D_Param>` **PARAM_SOFTNESS** = ``3``

Mức độ dễ bắt đầu xoắn của khớp. Nếu giá trị quá thấp, cần nhiều lực hơn để bắt đầu xoắn khớp.

.. _class_ConeTwistJoint3D_constant_PARAM_RELAXATION:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_ConeTwistJoint3D_Param>` **PARAM_RELAXATION** = ``4``

Xác định tốc độ đồng bộ hóa chênh lệch tốc độ swing và twist ở cả hai phía.

.. _class_ConeTwistJoint3D_constant_PARAM_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Param<enum_ConeTwistJoint3D_Param>` **PARAM_MAX** = ``5``

Đại diện cho kích thước của enum :ref:`Param<enum_ConeTwistJoint3D_Param>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConeTwistJoint3D_property_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **bias** = ``0.3`` :ref:`🔗<class_ConeTwistJoint3D_property_bias>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const|

Tốc độ thực hiện swing hoặc twist.

Giá trị càng cao thì tốc độ càng nhanh.

.. rst-class:: classref-item-separator

----

.. _class_ConeTwistJoint3D_property_relaxation:

.. rst-class:: classref-property

:ref:`float<class_float>` **relaxation** = ``1.0`` :ref:`🔗<class_ConeTwistJoint3D_property_relaxation>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const|

Xác định tốc độ đồng bộ hóa chênh lệch tốc độ swing và twist ở cả hai phía.

.. rst-class:: classref-item-separator

----

.. _class_ConeTwistJoint3D_property_softness:

.. rst-class:: classref-property

:ref:`float<class_float>` **softness** = ``0.8`` :ref:`🔗<class_ConeTwistJoint3D_property_softness>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const|

Mức độ dễ bắt đầu xoắn của khớp. Nếu giá trị quá thấp, cần nhiều lực hơn để bắt đầu xoắn khớp.

.. rst-class:: classref-item-separator

----

.. _class_ConeTwistJoint3D_property_swing_span:

.. rst-class:: classref-property

:ref:`float<class_float>` **swing_span** = ``0.7853982`` :ref:`🔗<class_ConeTwistJoint3D_property_swing_span>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const|

Swing là chuyển động xoay từ bên này sang bên kia, quanh trục vuông góc với trục twist.

Độ rộng swing xác định mức độ xoay sẽ không được hiệu chỉnh dọc theo trục swing.

Có thể hiểu đây là độ lỏng của **ConeTwistJoint3D**.

Nếu nhỏ hơn 0.05, hành vi này sẽ bị khóa.

.. rst-class:: classref-item-separator

----

.. _class_ConeTwistJoint3D_property_twist_span:

.. rst-class:: classref-property

:ref:`float<class_float>` **twist_span** = ``3.1415927`` :ref:`🔗<class_ConeTwistJoint3D_property_twist_span>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const|

Twist là chuyển động xoay quanh trục twist; giá trị này xác định khớp có thể xoắn đến mức nào.

Twist bị khóa nếu nhỏ hơn 0.05.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ConeTwistJoint3D_method_get_param:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`\ ) |const| :ref:`🔗<class_ConeTwistJoint3D_method_get_param>`

Trả về giá trị của tham số được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_ConeTwistJoint3D_method_set_param:

.. rst-class:: classref-method

|void| **set_param**\ (\ param\: :ref:`Param<enum_ConeTwistJoint3D_Param>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_ConeTwistJoint3D_method_set_param>`

Thiết lập giá trị của tham số được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
