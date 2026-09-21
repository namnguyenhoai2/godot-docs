:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PrimitiveMesh.xml.

.. _class_PrimitiveMesh:

PrimitiveMesh
=============

**Kế thừa:** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`BoxMesh<class_BoxMesh>`, :ref:`CapsuleMesh<class_CapsuleMesh>`, :ref:`CylinderMesh<class_CylinderMesh>`, :ref:`PlaneMesh<class_PlaneMesh>`, :ref:`PointMesh<class_PointMesh>`, :ref:`PrismMesh<class_PrismMesh>`, :ref:`RibbonTrailMesh<class_RibbonTrailMesh>`, :ref:`SphereMesh<class_SphereMesh>`, :ref:`TextMesh<class_TextMesh>`, :ref:`TorusMesh<class_TorusMesh>`, :ref:`TubeTrailMesh<class_TubeTrailMesh>`

Lớp cơ sở cho tất cả mesh nguyên thủy. Xử lý việc áp dụng một :ref:`Material<class_Material>` vào mesh nguyên thủy.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho tất cả mesh nguyên thủy. Xử lý việc áp dụng một :ref:`Material<class_Material>` vào mesh nguyên thủy. Các ví dụ bao gồm :ref:`BoxMesh<class_BoxMesh>`, :ref:`CapsuleMesh<class_CapsuleMesh>`, :ref:`CylinderMesh<class_CylinderMesh>`, :ref:`PlaneMesh<class_PlaneMesh>`, :ref:`PrismMesh<class_PrismMesh>` và :ref:`SphereMesh<class_SphereMesh>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------+--------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`         | :ref:`add_uv2<class_PrimitiveMesh_property_add_uv2>`         | ``false``                  |
   +---------------------------------+--------------------------------------------------------------+----------------------------+
   | :ref:`AABB<class_AABB>`         | :ref:`custom_aabb<class_PrimitiveMesh_property_custom_aabb>` | ``AABB(0, 0, 0, 0, 0, 0)`` |
   +---------------------------------+--------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`         | :ref:`flip_faces<class_PrimitiveMesh_property_flip_faces>`   | ``false``                  |
   +---------------------------------+--------------------------------------------------------------+----------------------------+
   | :ref:`Material<class_Material>` | :ref:`material<class_PrimitiveMesh_property_material>`       |                            |
   +---------------------------------+--------------------------------------------------------------+----------------------------+
   | :ref:`float<class_float>`       | :ref:`uv2_padding<class_PrimitiveMesh_property_uv2_padding>` | ``2.0``                    |
   +---------------------------------+--------------------------------------------------------------+----------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`_create_mesh_array<class_PrimitiveMesh_private_method__create_mesh_array>`\ (\ ) |virtual| |const| |
   +---------------------------+----------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>` | :ref:`get_mesh_arrays<class_PrimitiveMesh_method_get_mesh_arrays>`\ (\ ) |const|                         |
   +---------------------------+----------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`request_update<class_PrimitiveMesh_method_request_update>`\ (\ )                                   |
   +---------------------------+----------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PrimitiveMesh_property_add_uv2:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **add_uv2** = ``false`` :ref:`🔗<class_PrimitiveMesh_property_add_uv2>`

.. rst-class:: classref-property-setget

- |void| **set_add_uv2**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_add_uv2**\ (\ )

Nếu được thiết lập, sẽ tạo các tọa độ UV2 bằng cách áp dụng phần đệm (padding) theo thiết lập :ref:`uv2_padding<class_PrimitiveMesh_property_uv2_padding>`. UV2 cần thiết cho lightmapping.

.. rst-class:: classref-item-separator

----

.. _class_PrimitiveMesh_property_custom_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **custom_aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_PrimitiveMesh_property_custom_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_custom_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_custom_aabb**\ (\ )

Ghi đè :ref:`AABB<class_AABB>` bằng một giá trị do người dùng xác định để sử dụng với frustum culling. Đặc biệt hữu ích nhằm tránh việc culling ngoài dự kiến khi sử dụng shader để dịch chuyển các đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_PrimitiveMesh_property_flip_faces:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **flip_faces** = ``false`` :ref:`🔗<class_PrimitiveMesh_property_flip_faces>`

.. rst-class:: classref-property-setget

- |void| **set_flip_faces**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_flip_faces**\ (\ )

Nếu ``true``, thứ tự các đỉnh trong mỗi tam giác sẽ bị đảo ngược, khiến mặt sau của mesh được vẽ.

Điều này cho kết quả tương tự như sử dụng :ref:`BaseMaterial3D.CULL_FRONT<class_BaseMaterial3D_constant_CULL_FRONT>` trong :ref:`BaseMaterial3D.cull_mode<class_BaseMaterial3D_property_cull_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_PrimitiveMesh_property_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material** :ref:`🔗<class_PrimitiveMesh_property_material>`

.. rst-class:: classref-property-setget

- |void| **set_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material**\ (\ )

:ref:`Material<class_Material>` hiện tại của mesh nguyên thủy.

.. rst-class:: classref-item-separator

----

.. _class_PrimitiveMesh_property_uv2_padding:

.. rst-class:: classref-property

:ref:`float<class_float>` **uv2_padding** = ``2.0`` :ref:`🔗<class_PrimitiveMesh_property_uv2_padding>`

.. rst-class:: classref-property-setget

- |void| **set_uv2_padding**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_uv2_padding**\ (\ )

Nếu :ref:`add_uv2<class_PrimitiveMesh_property_add_uv2>` được thiết lập, chỉ định phần đệm tính theo pixel được áp dụng dọc theo các đường nối của mesh. Giá trị phần đệm thấp hơn cho phép tận dụng tốt hơn texture lightmap (dẫn đến mật độ texel cao hơn), nhưng có thể tạo ra hiện tượng lightmap bleeding rõ rệt dọc theo các cạnh.

Nếu không thể xác định kích thước của texture lightmap khi tạo mesh, UV2 sẽ được tính toán với giả định kích thước texture là 1024x1024.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PrimitiveMesh_private_method__create_mesh_array:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **_create_mesh_array**\ (\ ) |virtual| |const| :ref:`🔗<class_PrimitiveMesh_private_method__create_mesh_array>`

Ghi đè phương thức này để tùy chỉnh cách tạo mesh nguyên thủy này. Phương thức này sẽ trả về một :ref:`Array<class_Array>`, trong đó mỗi phần tử là một Array khác chứa các giá trị cần thiết cho mesh (xem các hằng số :ref:`ArrayType<enum_Mesh_ArrayType>`).

.. rst-class:: classref-item-separator

----

.. _class_PrimitiveMesh_method_get_mesh_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_mesh_arrays**\ (\ ) |const| :ref:`🔗<class_PrimitiveMesh_method_get_mesh_arrays>`

Trả về các mảng mesh được sử dụng để cấu thành bề mặt của mesh nguyên thủy này.

\ **Ví dụ:** Truyền kết quả cho :ref:`ArrayMesh.add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>` để tạo một bề mặt mới:


.. tabs::

 .. code-tab:: gdscript

    var c = CylinderMesh.new()
    var arr_mesh = ArrayMesh.new()
    arr_mesh.add_surface_from_arrays(Mesh.PRIMITIVE_TRIANGLES, c.get_mesh_arrays())

 .. code-tab:: csharp

    var c = new CylinderMesh();
    var arrMesh = new ArrayMesh();
    arrMesh.AddSurfaceFromArrays(Mesh.PrimitiveType.Triangles, c.GetMeshArrays());



.. rst-class:: classref-item-separator

----

.. _class_PrimitiveMesh_method_request_update:

.. rst-class:: classref-method

|void| **request_update**\ (\ ) :ref:`🔗<class_PrimitiveMesh_method_request_update>`

Yêu cầu cập nhật mesh nguyên thủy này dựa trên các thuộc tính của nó.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
