:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PlaneMesh.xml.

.. _class_PlaneMesh:

PlaneMesh
=========

**Kế thừa:** :ref:`PrimitiveMesh<class_PrimitiveMesh>` **<** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`QuadMesh<class_QuadMesh>`

Class đại diện cho một :ref:`PrimitiveMesh<class_PrimitiveMesh>` phẳng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class đại diện cho một :ref:`PrimitiveMesh<class_PrimitiveMesh>` phẳng. Lưới phẳng này không có độ dày. Theo mặc định, lưới này được căn chỉnh theo các trục X và Z; góc xoay mặc định này không phù hợp để sử dụng với các material billboard. Đối với các material billboard, hãy thay đổi :ref:`orientation<class_PlaneMesh_property_orientation>` thành :ref:`FACE_Z<class_PlaneMesh_constant_FACE_Z>`.

\ **Lưu ý:** Khi sử dụng một **PlaneMesh** có texture lớn (ví dụ như làm sàn), bạn có thể gặp vấn đề UV bị rung tùy thuộc vào góc camera. Để khắc phục, hãy tăng :ref:`subdivide_depth<class_PlaneMesh_property_subdivide_depth>` và :ref:`subdivide_width<class_PlaneMesh_property_subdivide_width>` cho đến khi bạn không còn nhận thấy hiện tượng UV bị rung.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +------------------------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                  | :ref:`center_offset<class_PlaneMesh_property_center_offset>`     | ``Vector3(0, 0, 0)`` |
   +------------------------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`Orientation<enum_PlaneMesh_Orientation>` | :ref:`orientation<class_PlaneMesh_property_orientation>`         | ``1``                |
   +------------------------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`Vector2<class_Vector2>`                  | :ref:`size<class_PlaneMesh_property_size>`                       | ``Vector2(2, 2)``    |
   +------------------------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                          | :ref:`subdivide_depth<class_PlaneMesh_property_subdivide_depth>` | ``0``                |
   +------------------------------------------------+------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                          | :ref:`subdivide_width<class_PlaneMesh_property_subdivide_width>` | ``0``                |
   +------------------------------------------------+------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_PlaneMesh_Orientation:

.. rst-class:: classref-enumeration

enum **Orientation**: :ref:`🔗<enum_PlaneMesh_Orientation>`

.. _class_PlaneMesh_constant_FACE_X:

.. rst-class:: classref-enumeration-constant

:ref:`Orientation<enum_PlaneMesh_Orientation>` **FACE_X** = ``0``

**PlaneMesh** sẽ hướng về trục X dương.

.. _class_PlaneMesh_constant_FACE_Y:

.. rst-class:: classref-enumeration-constant

:ref:`Orientation<enum_PlaneMesh_Orientation>` **FACE_Y** = ``1``

**PlaneMesh** sẽ hướng về trục Y dương. Điều này khớp với cách **PlaneMesh** hoạt động trong Godot 3.x.

.. _class_PlaneMesh_constant_FACE_Z:

.. rst-class:: classref-enumeration-constant

:ref:`Orientation<enum_PlaneMesh_Orientation>` **FACE_Z** = ``2``

**PlaneMesh** sẽ hướng về trục Z dương. Điều này khớp với cách QuadMesh hoạt động trong Godot 3.x.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PlaneMesh_property_center_offset:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **center_offset** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_PlaneMesh_property_center_offset>`

.. rst-class:: classref-property-setget

- |void| **set_center_offset**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_center_offset**\ (\ )

Độ lệch của mặt phẳng được tạo. Hữu ích cho particle.

.. rst-class:: classref-item-separator

----

.. _class_PlaneMesh_property_orientation:

.. rst-class:: classref-property

:ref:`Orientation<enum_PlaneMesh_Orientation>` **orientation** = ``1`` :ref:`🔗<class_PlaneMesh_property_orientation>`

.. rst-class:: classref-property-setget

- |void| **set_orientation**\ (\ value\: :ref:`Orientation<enum_PlaneMesh_Orientation>`\ ) - :ref:`Orientation<enum_PlaneMesh_Orientation>` **get_orientation**\ (\ )

Hướng mà **PlaneMesh** đang quay mặt về.

.. rst-class:: classref-item-separator

----

.. _class_PlaneMesh_property_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **size** = ``Vector2(2, 2)`` :ref:`🔗<class_PlaneMesh_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_size**\ (\ )

Kích thước của mặt phẳng được tạo.

.. rst-class:: classref-item-separator

----

.. _class_PlaneMesh_property_subdivide_depth:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_depth** = ``0`` :ref:`🔗<class_PlaneMesh_property_subdivide_depth>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_depth**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_depth**\ (\ )

Số lần chia nhỏ dọc theo trục Z.

.. rst-class:: classref-item-separator

----

.. _class_PlaneMesh_property_subdivide_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **subdivide_width** = ``0`` :ref:`🔗<class_PlaneMesh_property_subdivide_width>`

.. rst-class:: classref-property-setget

- |void| **set_subdivide_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_subdivide_width**\ (\ )

Số lần chia nhỏ dọc theo trục X.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
