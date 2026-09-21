:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PrismMesh.xml.

.. _class_PrismMesh:

PrismMesh
=========

**Kế thừa:** :ref:`PrimitiveMesh<class_PrimitiveMesh>` **<** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp biểu diễn một :ref:`PrimitiveMesh<class_PrimitiveMesh>` dạng lăng trụ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp biểu diễn một :ref:`PrimitiveMesh<class_PrimitiveMesh>` dạng lăng trụ.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`left_to_right<class_PrismMesh_property_left_to_right>`       | ``0.5``              |
   +-------------------------------+--------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`size<class_PrismMesh_property_size>`                         | ``Vector3(1, 1, 1)`` |
   +-------------------------------+--------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`subdivide_depth<class_PrismMesh_property_subdivide_depth>`   | ``0``                |
   +-------------------------------+--------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`subdivide_height<class_PrismMesh_property_subdivide_height>` | ``0``                |
   +-------------------------------+--------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`subdivide_width<class_PrismMesh_property_subdivide_width>`   | ``0``                |
   +-------------------------------+--------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PrismMesh_property_left_to_right:

.. rst-class:: classref-property

:ref:`float<class_float>` **left_to_right** = ``0.5`` :ref:`🔗<class_PrismMesh_property_left_to_right>`

.. rst-class:: classref-property-setget

- |void| **set_left_to_right**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_left_to_right**\ (\ )

Độ dịch chuyển của cạnh trên dọc theo trục X. Giá trị 0.0 đặt cạnh này thẳng ngay phía trên cạnh dưới bên trái.

.. rst-class:: classref-item-separator

----

.. _class_PrismMesh_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(1, 1, 1)`` :ref:`🔗<class_PrismMesh_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của lăng trụ.

.. rst-class:: classref-item-separator

----

.. _class_PrismMesh_property_subdivide_depth:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_depth** = ``0`` :ref:`🔗<class_PrismMesh_property_subdivide_depth>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_depth**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_depth**\ (\ )

Số vòng cạnh được thêm vào dọc theo trục Z.

.. rst-class:: classref-item-separator

----

.. _class_PrismMesh_property_subdivide_height:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_height** = ``0`` :ref:`🔗<class_PrismMesh_property_subdivide_height>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_height**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_height**\ (\ )

Số vòng cạnh được thêm vào dọc theo trục Y.

.. rst-class:: classref-item-separator

----

.. _class_PrismMesh_property_subdivide_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_width** = ``0`` :ref:`🔗<class_PrismMesh_property_subdivide_width>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_width**\ (\ )

Số vòng cạnh được thêm vào dọc theo trục X.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
