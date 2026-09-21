:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGPrimitive3D.xml.

.. _class_CSGPrimitive3D:

CSGPrimitive3D
==============

**Kế thừa:** :ref:`CSGShape3D<class_CSGShape3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CSGBox3D<class_CSGBox3D>`, :ref:`CSGCylinder3D<class_CSGCylinder3D>`, :ref:`CSGMesh3D<class_CSGMesh3D>`, :ref:`CSGPolygon3D<class_CSGPolygon3D>`, :ref:`CSGSphere3D<class_CSGSphere3D>`, :ref:`CSGTorus3D<class_CSGTorus3D>`

Lớp cơ sở cho các primitive CSG.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cha cho nhiều primitive CSG khác nhau. Lớp này chứa mã và chức năng dùng chung giữa chúng. Không thể sử dụng lớp này trực tiếp. Thay vào đó, hãy sử dụng một trong các lớp khác nhau kế thừa từ lớp này.

\ **Lưu ý:** Các node CSG được thiết kế để dùng cho việc dựng prototype của level. Việc tạo các node CSG có chi phí CPU đáng kể so với việc tạo một :ref:`MeshInstance3D<class_MeshInstance3D>` với một :ref:`PrimitiveMesh<class_PrimitiveMesh>`. Việc di chuyển một node CSG bên trong một node CSG khác cũng có chi phí CPU đáng kể, vì vậy nên tránh thực hiện việc này trong gameplay.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tạo nguyên mẫu level bằng CSG <../tutorials/3d/csg_tools>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+-------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`flip_faces<class_CSGPrimitive3D_property_flip_faces>` | ``false`` |
   +-------------------------+-------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CSGPrimitive3D_property_flip_faces:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **flip_faces** = ``false`` :ref:`🔗<class_CSGPrimitive3D_property_flip_faces>`

.. rst-class:: classref-property-setget

- |void| **set_flip_faces**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flip_faces**\ (\ )

Nếu được bật, thứ tự các đỉnh trong mỗi tam giác sẽ bị đảo ngược, khiến mặt sau của mesh được vẽ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
