:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGMesh3D.xml.

.. _class_CSGMesh3D:

CSGMesh3D
=========

**Kế thừa:** :ref:`CSGPrimitive3D<class_CSGPrimitive3D>` **<** :ref:`CSGShape3D<class_CSGShape3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một hình dạng CSG Mesh sử dụng một tài nguyên mesh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node CSG này cho phép bạn sử dụng bất kỳ tài nguyên mesh nào làm hình dạng CSG, với điều kiện nó là *manifold* (đa tạp). Một hình dạng manifold là hình dạng kín, không tự giao nhau, không chứa các mặt bên trong và không có cạnh nào kết nối với nhiều hơn hai mặt. Xem thêm :ref:`CSGPolygon3D<class_CSGPolygon3D>` để vẽ các đa giác 2D được đùn dùng làm node CSG.

\ **Lưu ý:** Các node CSG được dùng cho việc tạo nguyên mẫu level. Việc tạo node CSG có chi phí CPU đáng kể so với việc tạo một :ref:`MeshInstance3D<class_MeshInstance3D>` với một :ref:`PrimitiveMesh<class_PrimitiveMesh>`. Việc di chuyển một node CSG bên trong một node CSG khác cũng có chi phí CPU đáng kể, vì vậy nên tránh thực hiện việc này trong quá trình gameplay.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tạo nguyên mẫu level bằng CSG <../tutorials/3d/csg_tools>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------+
   | :ref:`Material<class_Material>` | :ref:`material<class_CSGMesh3D_property_material>` |
   +---------------------------------+----------------------------------------------------+
   | :ref:`Mesh<class_Mesh>`         | :ref:`mesh<class_CSGMesh3D_property_mesh>`         |
   +---------------------------------+----------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CSGMesh3D_property_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material** :ref:`🔗<class_CSGMesh3D_property_material>`

.. rst-class:: classref-property-setget

- |void| **set_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material**\ (\ )

:ref:`Material<class_Material>` được sử dụng để vẽ hình dạng CSG.

.. rst-class:: classref-item-separator

----

.. _class_CSGMesh3D_property_mesh:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **mesh** :ref:`🔗<class_CSGMesh3D_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_mesh**\ (\ )

Tài nguyên :ref:`Mesh<class_Mesh>` được sử dụng làm hình dạng CSG.

\ **Lưu ý:** Một số loại :ref:`Mesh<class_Mesh>` như :ref:`PlaneMesh<class_PlaneMesh>`, :ref:`PointMesh<class_PointMesh>`, :ref:`QuadMesh<class_QuadMesh>` và :ref:`RibbonTrailMesh<class_RibbonTrailMesh>` bị loại khỏi gợi ý kiểu cho thuộc tính này, vì các primitive này là *manifold* và do đó không tương thích với thuật toán CSG.

\ **Lưu ý:** Khi sử dụng một :ref:`ArrayMesh<class_ArrayMesh>`, mọi thuộc tính vertex ngoại trừ :ref:`Mesh.ARRAY_VERTEX<class_Mesh_constant_ARRAY_VERTEX>`, :ref:`Mesh.ARRAY_NORMAL<class_Mesh_constant_ARRAY_NORMAL>` và :ref:`Mesh.ARRAY_TEX_UV<class_Mesh_constant_ARRAY_TEX_UV>` đều không được sử dụng. Chỉ :ref:`Mesh.ARRAY_VERTEX<class_Mesh_constant_ARRAY_VERTEX>` và :ref:`Mesh.ARRAY_TEX_UV<class_Mesh_constant_ARRAY_TEX_UV>` được truyền đến GPU.

\ :ref:`Mesh.ARRAY_NORMAL<class_Mesh_constant_ARRAY_NORMAL>` chỉ được sử dụng để xác định những mặt nào cần dùng flat shading. Theo mặc định, CSGMesh sẽ bỏ qua các vertex normal của mesh, tính toán lại chúng cho từng vertex và sử dụng smooth shader. Nếu một mặt cần flat shader, hãy đảm bảo rằng tất cả vertex normal của mặt đó xấp xỉ bằng nhau.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
