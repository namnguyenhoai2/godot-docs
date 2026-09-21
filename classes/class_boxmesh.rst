:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/BoxMesh.xml.

.. _class_BoxMesh:

BoxMesh
=======

**Kế thừa:** :ref:`PrimitiveMesh<class_PrimitiveMesh>` **<** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Tạo một hộp :ref:`PrimitiveMesh<class_PrimitiveMesh>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Tạo một hộp :ref:`PrimitiveMesh<class_PrimitiveMesh>`.

Bố cục UV của hộp được sắp xếp theo bố cục 3×2, cho phép áp dụng texture riêng cho từng mặt. Để áp dụng cùng một texture cho tất cả các mặt, hãy thay đổi thuộc tính UV của material thành ``Vector3(3, 2, 1)``. Điều này tương đương với việc thêm ``UV *= vec2(3.0, 2.0)`` vào vertex shader.

\ **Lưu ý:** Khi sử dụng một **BoxMesh** có texture lớn (ví dụ: làm sàn), bạn có thể gặp vấn đề UV bị rung tùy thuộc vào góc camera. Để khắc phục, hãy tăng :ref:`subdivide_depth<class_BoxMesh_property_subdivide_depth>`, :ref:`subdivide_height<class_BoxMesh_property_subdivide_height>` và :ref:`subdivide_width<class_BoxMesh_property_subdivide_width>` cho đến khi không còn nhận thấy hiện tượng UV bị rung.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`size<class_BoxMesh_property_size>`                         | ``Vector3(1, 1, 1)`` |
   +-------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`subdivide_depth<class_BoxMesh_property_subdivide_depth>`   | ``0``                |
   +-------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`subdivide_height<class_BoxMesh_property_subdivide_height>` | ``0``                |
   +-------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`subdivide_width<class_BoxMesh_property_subdivide_width>`   | ``0``                |
   +-------------------------------+------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BoxMesh_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(1, 1, 1)`` :ref:`🔗<class_BoxMesh_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Chiều rộng, chiều cao và chiều sâu của hộp.

.. rst-class:: classref-item-separator

----

.. _class_BoxMesh_property_subdivide_depth:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_depth** = ``0`` :ref:`🔗<class_BoxMesh_property_subdivide_depth>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_depth**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_depth**\ (\ )

Số lượng edge loop bổ sung được chèn dọc theo trục Z.

.. rst-class:: classref-item-separator

----

.. _class_BoxMesh_property_subdivide_height:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_height** = ``0`` :ref:`🔗<class_BoxMesh_property_subdivide_height>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_height**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_height**\ (\ )

Số lượng edge loop bổ sung được chèn dọc theo trục Y.

.. rst-class:: classref-item-separator

----

.. _class_BoxMesh_property_subdivide_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_width** = ``0`` :ref:`🔗<class_BoxMesh_property_subdivide_width>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_width**\ (\ )

Số lượng edge loop bổ sung được chèn dọc theo trục X.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
