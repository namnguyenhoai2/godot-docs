:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CapsuleMesh.xml.

.. _class_CapsuleMesh:

CapsuleMesh
===========

**Kế thừa:** :ref:`PrimitiveMesh<class_PrimitiveMesh>` **<** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp đại diện cho một :ref:`PrimitiveMesh<class_PrimitiveMesh>` hình viên nang.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp đại diện cho một :ref:`PrimitiveMesh<class_PrimitiveMesh>` hình viên nang.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`height<class_CapsuleMesh_property_height>`                   | ``2.0`` |
   +---------------------------+--------------------------------------------------------------------+---------+
   | :ref:`int<class_int>`     | :ref:`radial_segments<class_CapsuleMesh_property_radial_segments>` | ``64``  |
   +---------------------------+--------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`radius<class_CapsuleMesh_property_radius>`                   | ``0.5`` |
   +---------------------------+--------------------------------------------------------------------+---------+
   | :ref:`int<class_int>`     | :ref:`rings<class_CapsuleMesh_property_rings>`                     | ``8``   |
   +---------------------------+--------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CapsuleMesh_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``2.0`` :ref:`🔗<class_CapsuleMesh_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Tổng chiều cao của capsule mesh (bao gồm các đầu hình bán cầu).

\ **Lưu ý:** :ref:`height<class_CapsuleMesh_property_height>` của capsule phải ít nhất bằng hai lần :ref:`radius<class_CapsuleMesh_property_radius>` của nó. Nếu không, capsule sẽ trở thành một hình tròn. Nếu :ref:`height<class_CapsuleMesh_property_height>` nhỏ hơn hai lần :ref:`radius<class_CapsuleMesh_property_radius>`, các thuộc tính sẽ được điều chỉnh thành một giá trị hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_CapsuleMesh_property_radial_segments:

.. rst-class:: classref-property

:ref:`int<class_int>` **radial_segments** = ``64`` :ref:`🔗<class_CapsuleMesh_property_radial_segments>`

.. rst-class:: classref-property-setget

- |void| **set_radial_segments**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_radial_segments**\ (\ )

Số lượng radial segment trên capsule mesh.

.. rst-class:: classref-item-separator

----

.. _class_CapsuleMesh_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.5`` :ref:`🔗<class_CapsuleMesh_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của capsule mesh.

\ **Lưu ý:** :ref:`radius<class_CapsuleMesh_property_radius>` của capsule không thể lớn hơn một nửa :ref:`height<class_CapsuleMesh_property_height>` của nó. Nếu không, capsule sẽ trở thành một hình tròn. Nếu :ref:`radius<class_CapsuleMesh_property_radius>` lớn hơn một nửa :ref:`height<class_CapsuleMesh_property_height>`, các thuộc tính sẽ được điều chỉnh thành một giá trị hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_CapsuleMesh_property_rings:

.. rst-class:: classref-property

:ref:`int<class_int>` **rings** = ``8`` :ref:`🔗<class_CapsuleMesh_property_rings>`

.. rst-class:: classref-property-setget

- |void| **set_rings**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_rings**\ (\ )

Số lượng ring dọc theo chiều cao của capsule.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
