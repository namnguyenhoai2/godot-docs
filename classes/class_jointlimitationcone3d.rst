:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/JointLimitationCone3D.xml.

.. _class_JointLimitationCone3D:

JointLimitationCone3D
=====================

**Kế thừa:** :ref:`JointLimitation3D<class_JointLimitation3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một giới hạn dạng hình nón tương tác với :ref:`ChainIK3D<class_ChainIK3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một giới hạn dạng hình nón tương tác với :ref:`ChainIK3D<class_ChainIK3D>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------+---------------+
   | :ref:`float<class_float>` | :ref:`angle<class_JointLimitationCone3D_property_angle>` | ``1.5707964`` |
   +---------------------------+----------------------------------------------------------+---------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_JointLimitationCone3D_property_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **angle** = ``1.5707964`` :ref:`🔗<class_JointLimitationCone3D_property_angle>`

.. rst-class:: classref-property-setget

- |void| **set_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angle**\ (\ )

Phạm vi bán kính của lỗ do hình nón tạo ra.

\ ``0`` độ tạo thành một hình cầu không có lỗ, ``180`` độ tạo thành một bán cầu và ``360`` độ trở thành rỗng (không giới hạn).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
