:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CapsuleShape3D.xml.

.. _class_CapsuleShape3D:

CapsuleShape3D
==============

**Kế thừa:** :ref:`Shape3D<class_Shape3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một capsule shape 3D được sử dụng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một capsule shape 3D, предназначена để sử dụng trong vật lý. Thường được dùng để cung cấp một shape cho :ref:`CollisionShape3D<class_CollisionShape3D>`.

\ **Hiệu năng:** **CapsuleShape3D** kiểm tra va chạm rất nhanh. Nó nhanh hơn :ref:`CylinderShape3D<class_CylinderShape3D>`, nhưng chậm hơn :ref:`SphereShape3D<class_SphereShape3D>` và :ref:`BoxShape3D<class_BoxShape3D>`.

.. rst-class:: classref-introduction-group

Tutorials
---------

- `3D Physics Tests Demo <https://godotengine.org/asset-library/asset/2747>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`height<class_CapsuleShape3D_property_height>`         | ``2.0`` |
   +---------------------------+-------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`mid_height<class_CapsuleShape3D_property_mid_height>` |         |
   +---------------------------+-------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`radius<class_CapsuleShape3D_property_radius>`         | ``0.5`` |
   +---------------------------+-------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CapsuleShape3D_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``2.0`` :ref:`🔗<class_CapsuleShape3D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Chiều cao đầy đủ của capsule, bao gồm cả hai bán cầu.

\ **Lưu ý:** :ref:`height<class_CapsuleShape3D_property_height>` của capsule phải ít nhất bằng hai lần :ref:`radius<class_CapsuleShape3D_property_radius>` của nó. Nếu không, capsule sẽ trở thành một hình cầu. Nếu :ref:`height<class_CapsuleShape3D_property_height>` nhỏ hơn hai lần :ref:`radius<class_CapsuleShape3D_property_radius>`, các thuộc tính sẽ được điều chỉnh thành một giá trị hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_CapsuleShape3D_property_mid_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **mid_height** :ref:`🔗<class_CapsuleShape3D_property_mid_height>`

.. rst-class:: classref-property-setget

- |void| **set_mid_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mid_height**\ (\ )

Chiều cao của capsule, không bao gồm hai bán cầu. Đây là chiều cao của phần hình trụ trung tâm ở giữa capsule, đồng thời là khoảng cách giữa tâm của hai bán cầu. Đây là một wrapper cho :ref:`height<class_CapsuleShape3D_property_height>`.

.. rst-class:: classref-item-separator

----

.. _class_CapsuleShape3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.5`` :ref:`🔗<class_CapsuleShape3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của capsule.

\ **Lưu ý:** :ref:`radius<class_CapsuleShape3D_property_radius>` của capsule không thể lớn hơn một nửa :ref:`height<class_CapsuleShape3D_property_height>` của nó. Nếu không, capsule sẽ trở thành một hình cầu. Nếu :ref:`radius<class_CapsuleShape3D_property_radius>` lớn hơn một nửa :ref:`height<class_CapsuleShape3D_property_height>`, các thuộc tính sẽ được điều chỉnh thành một giá trị hợp lệ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
