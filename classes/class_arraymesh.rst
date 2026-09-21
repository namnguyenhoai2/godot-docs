:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ArrayMesh.xml.

.. _class_ArrayMesh:

ArrayMesh
=========

**Kế thừa:** :ref:`Mesh<class_Mesh>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

:ref:`Mesh<class_Mesh>` type that provides utility for constructing a surface from arrays.

.. rst-class:: classref-introduction-group

Mô tả
-----

**ArrayMesh** được dùng để xây dựng một :ref:`Mesh<class_Mesh>` bằng cách chỉ định các thuộc tính dưới dạng các mảng.

Ví dụ cơ bản nhất là tạo một tam giác đơn:


.. tabs::

 .. code-tab:: gdscript

    var vertices = PackedVector3Array()
    vertices.push_back(Vector3(0, 1, 0))
    vertices.push_back(Vector3(1, 0, 0))
    vertices.push_back(Vector3(0, 0, 1))

    # Khởi tạo ArrayMesh.
    var arr_mesh = ArrayMesh.new()
    var arrays = []
    arrays.resize(Mesh.ARRAY_MAX)
    arrays[Mesh.ARRAY_VERTEX] = vertices

    # Tạo Mesh.
    arr_mesh.add_surface_from_arrays(Mesh.PRIMITIVE_TRIANGLES, arrays)
    var m = MeshInstance3D.new()
    m.mesh = arr_mesh

 .. code-tab:: csharp

    Vector3[] vertices =
    [
        new Vector3(0, 1, 0),
        new Vector3(1, 0, 0),
        new Vector3(0, 0, 1),
    ];

    // Khởi tạo ArrayMesh.
    var arrMesh = new ArrayMesh();
    Godot.Collections.Array arrays = [];
    arrays.Resize((int)Mesh.ArrayType.Max);
    arrays[(int)Mesh.ArrayType.Vertex] = vertices;

    // Tạo Mesh.
    arrMesh.AddSurfaceFromArrays(Mesh.PrimitiveType.Triangles, arrays);
    var m = new MeshInstance3D();
    m.Mesh = arrMesh;



:ref:`MeshInstance3D<class_MeshInstance3D>` đã sẵn sàng để được thêm vào :ref:`SceneTree<class_SceneTree>` nhằm hiển thị.

Xem thêm :ref:`ImmediateMesh<class_ImmediateMesh>`, :ref:`MeshDataTool<class_MeshDataTool>` và :ref:`SurfaceTool<class_SurfaceTool>` để tạo hình học theo quy trình.

\ **Lưu ý:** Godot sử dụng `winding order <https://learnopengl.com/Advanced-OpenGL/Face-culling>`__ theo chiều kim đồng hồ cho các mặt trước của các mode primitive tam giác.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Procedural geometry using the ArrayMesh <../tutorials/3d/procedural_geometry/arraymesh>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+--------------------------------------------------------------------+----------------------------+
   | :ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` | :ref:`blend_shape_mode<class_ArrayMesh_property_blend_shape_mode>` | ``1``                      |
   +-------------------------------------------------+--------------------------------------------------------------------+----------------------------+
   | :ref:`AABB<class_AABB>`                         | :ref:`custom_aabb<class_ArrayMesh_property_custom_aabb>`           | ``AABB(0, 0, 0, 0, 0, 0)`` |
   +-------------------------------------------------+--------------------------------------------------------------------+----------------------------+
   | :ref:`ArrayMesh<class_ArrayMesh>`               | :ref:`shadow_mesh<class_ArrayMesh_property_shadow_mesh>`           |                            |
   +-------------------------------------------------+--------------------------------------------------------------------+----------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`add_blend_shape<class_ArrayMesh_method_add_blend_shape>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                                                                                                                                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`add_surface_from_arrays<class_ArrayMesh_method_add_surface_from_arrays>`\ (\ primitive\: :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`, arrays\: :ref:`Array<class_Array>`, blend_shapes\: :ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\] = [], lods\: :ref:`Dictionary<class_Dictionary>` = {}, flags\: |bitfield|\[:ref:`ArrayFormat<enum_Mesh_ArrayFormat>`\] = 0\ ) |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`clear_blend_shapes<class_ArrayMesh_method_clear_blend_shapes>`\ (\ )                                                                                                                                                                                                                                                                                                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`clear_surfaces<class_ArrayMesh_method_clear_surfaces>`\ (\ )                                                                                                                                                                                                                                                                                                                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                   | :ref:`get_blend_shape_count<class_ArrayMesh_method_get_blend_shape_count>`\ (\ ) |const|                                                                                                                                                                                                                                                                                              |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                     | :ref:`get_blend_shape_name<class_ArrayMesh_method_get_blend_shape_name>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                 |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                   | :ref:`lightmap_unwrap<class_ArrayMesh_method_lightmap_unwrap>`\ (\ transform\: :ref:`Transform3D<class_Transform3D>`, texel_size\: :ref:`float<class_float>`\ )                                                                                                                                                                                                                       |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`regen_normal_maps<class_ArrayMesh_method_regen_normal_maps>`\ (\ )                                                                                                                                                                                                                                                                                                              |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`set_blend_shape_name<class_ArrayMesh_method_set_blend_shape_name>`\ (\ index\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                                                                                             |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                   | :ref:`surface_find_by_name<class_ArrayMesh_method_surface_find_by_name>`\ (\ name\: :ref:`String<class_String>`\ ) |const|                                                                                                                                                                                                                                                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                   | :ref:`surface_get_array_index_len<class_ArrayMesh_method_surface_get_array_index_len>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                   | :ref:`surface_get_array_len<class_ArrayMesh_method_surface_get_array_len>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                            |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`ArrayFormat<enum_Mesh_ArrayFormat>`\] | :ref:`surface_get_format<class_ArrayMesh_method_surface_get_format>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                             | :ref:`surface_get_name<class_ArrayMesh_method_surface_get_name>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                      |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`           | :ref:`surface_get_primitive_type<class_ArrayMesh_method_surface_get_primitive_type>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`surface_remove<class_ArrayMesh_method_surface_remove>`\ (\ surf_idx\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                  |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`surface_set_name<class_ArrayMesh_method_surface_set_name>`\ (\ surf_idx\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                                          |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`surface_update_attribute_region<class_ArrayMesh_method_surface_update_attribute_region>`\ (\ surf_idx\: :ref:`int<class_int>`, offset\: :ref:`int<class_int>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                                                          |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`surface_update_skin_region<class_ArrayMesh_method_surface_update_skin_region>`\ (\ surf_idx\: :ref:`int<class_int>`, offset\: :ref:`int<class_int>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                                                                    |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                  | :ref:`surface_update_vertex_region<class_ArrayMesh_method_surface_update_vertex_region>`\ (\ surf_idx\: :ref:`int<class_int>`, offset\: :ref:`int<class_int>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                                                                |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ArrayMesh_property_blend_shape_mode:

.. rst-class:: classref-property

:ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` **blend_shape_mode** = ``1`` :ref:`🔗<class_ArrayMesh_property_blend_shape_mode>`

.. rst-class:: classref-property-setget

- |void| **set_blend_shape_mode**\ (\ value\: :ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>`\ ) - :ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` **get_blend_shape_mode**\ (\ )

Mode của blend shape.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_property_custom_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **custom_aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_ArrayMesh_property_custom_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_custom_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_custom_aabb**\ (\ )

Ghi đè :ref:`AABB<class_AABB>` bằng một giá trị do người dùng xác định để sử dụng với frustum culling. Đặc biệt hữu ích để tránh việc culling ngoài dự kiến khi sử dụng shader để dịch chuyển các đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_property_shadow_mesh:

.. rst-class:: classref-property

:ref:`ArrayMesh<class_ArrayMesh>` **shadow_mesh** :ref:`🔗<class_ArrayMesh_property_shadow_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_mesh**\ (\ value\: :ref:`ArrayMesh<class_ArrayMesh>`\ ) - :ref:`ArrayMesh<class_ArrayMesh>` **get_shadow_mesh**\ (\ )

Một mesh tùy chọn có thể được sử dụng để render bóng và depth prepass. Có thể tăng hiệu năng bằng cách cung cấp một mesh có các đỉnh đã hợp nhất và chỉ có dữ liệu vị trí đỉnh (không có normal, UV, màu, v.v.).

\ **Lưu ý:** Mesh này phải có chính xác cùng vị trí đỉnh với mesh nguồn (bao gồm cả các LOD của mesh nguồn, nếu có). Nếu vị trí đỉnh khác nhau, mesh sẽ không được vẽ chính xác.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ArrayMesh_method_add_blend_shape:

.. rst-class:: classref-method

|void| **add_blend_shape**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_ArrayMesh_method_add_blend_shape>`

Thêm tên cho một blend shape sẽ được thêm bằng :ref:`add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>`. Phải được gọi trước khi thêm surface.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_add_surface_from_arrays:

.. rst-class:: classref-method

|void| **add_surface_from_arrays**\ (\ primitive\: :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`, arrays\: :ref:`Array<class_Array>`, blend_shapes\: :ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\] = [], lods\: :ref:`Dictionary<class_Dictionary>` = {}, flags\: |bitfield|\[:ref:`ArrayFormat<enum_Mesh_ArrayFormat>`\] = 0\ ) :ref:`🔗<class_ArrayMesh_method_add_surface_from_arrays>`

Tạo một surface mới. :ref:`Mesh.get_surface_count()<class_Mesh_method_get_surface_count>` sẽ trở thành ``surf_idx`` cho surface mới này.

Các surface được tạo để render bằng ``primitive``, có thể là bất kỳ giá trị nào được định nghĩa trong :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`.

Đối số ``arrays`` là một mảng các mảng. Mỗi phần tử :ref:`Mesh.ARRAY_MAX<class_Mesh_constant_ARRAY_MAX>` chứa một mảng với một phần dữ liệu mesh cho surface này, như được mô tả bởi thành phần tương ứng của :ref:`ArrayType<enum_Mesh_ArrayType>` hoặc ``null`` nếu nó không được surface sử dụng. Ví dụ, ``arrays[0]`` là mảng các đỉnh. Mảng con đỉnh đầu tiên luôn bắt buộc; các mảng khác là tùy chọn. Việc thêm một mảng chỉ mục sẽ đưa surface này vào "index mode", trong đó các mảng đỉnh và các mảng khác trở thành nguồn dữ liệu, còn mảng chỉ mục xác định thứ tự đỉnh. Tất cả mảng con phải có cùng độ dài với mảng đỉnh (hoặc là bội số chính xác của độ dài mảng đỉnh, khi nhiều phần tử của một mảng con tương ứng với một đỉnh) hoặc phải rỗng, ngoại trừ :ref:`Mesh.ARRAY_INDEX<class_Mesh_constant_ARRAY_INDEX>` nếu nó được sử dụng.

Đối số ``blend_shapes`` là một mảng dữ liệu đỉnh cho mỗi blend shape. Mỗi phần tử là một mảng có cùng cấu trúc với ``arrays``, nhưng :ref:`Mesh.ARRAY_VERTEX<class_Mesh_constant_ARRAY_VERTEX>`, :ref:`Mesh.ARRAY_NORMAL<class_Mesh_constant_ARRAY_NORMAL>` và :ref:`Mesh.ARRAY_TANGENT<class_Mesh_constant_ARRAY_TANGENT>` chỉ được thiết lập khi chúng được thiết lập trong ``arrays``, còn tất cả các mục khác là ``null``.

Đối số ``lods`` là một dictionary với các key :ref:`float<class_float>` và các value :ref:`PackedInt32Array<class_PackedInt32Array>`. Mỗi mục trong dictionary đại diện cho một mức LOD của surface, trong đó value là mảng :ref:`Mesh.ARRAY_INDEX<class_Mesh_constant_ARRAY_INDEX>` được sử dụng cho mức LOD, còn key gần tương ứng với khoảng cách tại đó các chỉ số LOD được sử dụng. Nghĩa là, tăng key của một LOD cũng làm tăng khoảng cách mà đối tượng phải cách camera trước khi LOD được sử dụng.

Đối số ``flags`` là phép OR theo bit của các giá trị cần thiết: Một giá trị :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` được dịch trái ``ARRAY_FORMAT_CUSTOMn_SHIFT`` bit cho mỗi kênh tùy chỉnh đang được sử dụng, :ref:`Mesh.ARRAY_FLAG_USE_DYNAMIC_UPDATE<class_Mesh_constant_ARRAY_FLAG_USE_DYNAMIC_UPDATE>`, :ref:`Mesh.ARRAY_FLAG_USE_8_BONE_WEIGHTS<class_Mesh_constant_ARRAY_FLAG_USE_8_BONE_WEIGHTS>` hoặc :ref:`Mesh.ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY<class_Mesh_constant_ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY>`.

\ **Lưu ý:** Khi sử dụng chỉ mục, bạn nên chỉ sử dụng point, line hoặc triangle.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_clear_blend_shapes:

.. rst-class:: classref-method

|void| **clear_blend_shapes**\ (\ ) :ref:`🔗<class_ArrayMesh_method_clear_blend_shapes>`

Xóa tất cả blend shape khỏi **ArrayMesh** này.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_clear_surfaces:

.. rst-class:: classref-method

|void| **clear_surfaces**\ (\ ) :ref:`🔗<class_ArrayMesh_method_clear_surfaces>`

Xóa tất cả surface khỏi **ArrayMesh** này.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_get_blend_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_blend_shape_count**\ (\ ) |const| :ref:`🔗<class_ArrayMesh_method_get_blend_shape_count>`

Trả về số lượng blend shape mà **ArrayMesh** đang chứa.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_get_blend_shape_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_blend_shape_name**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_get_blend_shape_name>`

Trả về tên của blend shape tại chỉ mục này.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_lightmap_unwrap:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **lightmap_unwrap**\ (\ transform\: :ref:`Transform3D<class_Transform3D>`, texel_size\: :ref:`float<class_float>`\ ) :ref:`🔗<class_ArrayMesh_method_lightmap_unwrap>`

Thực hiện UV unwrap trên **ArrayMesh** để chuẩn bị mesh cho lightmapping.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_regen_normal_maps:

.. rst-class:: classref-method

|void| **regen_normal_maps**\ (\ ) :ref:`🔗<class_ArrayMesh_method_regen_normal_maps>`

Tạo lại tangent cho từng surface của **ArrayMesh**.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_set_blend_shape_name:

.. rst-class:: classref-method

|void| **set_blend_shape_name**\ (\ index\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_ArrayMesh_method_set_blend_shape_name>`

Đặt tên cho blend shape tại chỉ mục này.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_find_by_name:

.. rst-class:: classref-method

:ref:`int<class_int>` **surface_find_by_name**\ (\ name\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_surface_find_by_name>`

Trả về chỉ mục của surface đầu tiên có tên này trong **ArrayMesh**. Nếu không tìm thấy, trả về -1.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_get_array_index_len:

.. rst-class:: classref-method

:ref:`int<class_int>` **surface_get_array_index_len**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_surface_get_array_index_len>`

Trả về độ dài theo số chỉ mục của mảng chỉ mục trong surface được yêu cầu (xem :ref:`add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>`).

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_get_array_len:

.. rst-class:: classref-method

:ref:`int<class_int>` **surface_get_array_len**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_surface_get_array_len>`

Trả về độ dài theo số đỉnh của mảng đỉnh trong surface được yêu cầu (xem :ref:`add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>`).

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_get_format:

.. rst-class:: classref-method

|bitfield|\[:ref:`ArrayFormat<enum_Mesh_ArrayFormat>`\] **surface_get_format**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_surface_get_format>`

Trả về mặt nạ format của surface được yêu cầu (xem :ref:`add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>`).

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_get_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **surface_get_name**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_surface_get_name>`

Lấy tên được gán cho surface này.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_get_primitive_type:

.. rst-class:: classref-method

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **surface_get_primitive_type**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ArrayMesh_method_surface_get_primitive_type>`

Trả về kiểu primitive của surface được yêu cầu (xem :ref:`add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>`).

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_remove:

.. rst-class:: classref-method

|void| **surface_remove**\ (\ surf_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ArrayMesh_method_surface_remove>`

Xóa surface tại chỉ mục đã cho khỏi Mesh, đồng thời dịch các surface có chỉ mục cao hơn xuống một bậc.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_set_name:

.. rst-class:: classref-method

|void| **surface_set_name**\ (\ surf_idx\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ArrayMesh_method_surface_set_name>`

Đặt tên cho surface đã cho.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_update_attribute_region:

.. rst-class:: classref-method

|void| **surface_update_attribute_region**\ (\ surf_idx\: :ref:`int<class_int>`, offset\: :ref:`int<class_int>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_ArrayMesh_method_surface_update_attribute_region>`

Cập nhật attribute buffer của surface trong mesh này bằng ``data`` đã cho. Dữ liệu dự kiến cho mỗi attribute là 12 hoặc 8 byte (4 byte cho mỗi float, 2 float cho mỗi :ref:`Vector2<class_Vector2>` và 3 float cho mỗi :ref:`Vector3<class_Vector3>`) tùy thuộc vào việc mesh sử dụng đỉnh :ref:`Vector3<class_Vector3>` hay :ref:`Vector2<class_Vector2>`. Giá trị này có thể được xác định bằng :ref:`RenderingServer.mesh_surface_get_format_attribute_stride()<class_RenderingServer_method_mesh_surface_get_format_attribute_stride>`.

Có thể thay đổi điểm bắt đầu cập nhật bằng ``offset``. Trong hầu hết trường hợp, giá trị của ``offset`` phải là bội số của 12 byte để căn chỉnh theo từng attribute.

Một :ref:`PackedVector3Array<class_PackedVector3Array>` các vị trí attribute có thể được chuyển đổi thành :ref:`PackedByteArray<class_PackedByteArray>` bằng :ref:`PackedVector3Array.to_byte_array()<class_PackedVector3Array_method_to_byte_array>` để sử dụng trong ``data``.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_update_skin_region:

.. rst-class:: classref-method

|void| **surface_update_skin_region**\ (\ surf_idx\: :ref:`int<class_int>`, offset\: :ref:`int<class_int>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_ArrayMesh_method_surface_update_skin_region>`

Cập nhật skin buffer của surface trong mesh này bằng ``data`` đã cho. Dữ liệu dự kiến cho mỗi skin là 12 hoặc 8 byte (4 byte cho mỗi float, 2 float cho mỗi :ref:`Vector2<class_Vector2>` và 3 float cho mỗi :ref:`Vector3<class_Vector3>`) tùy thuộc vào việc mesh sử dụng đỉnh :ref:`Vector3<class_Vector3>` hay :ref:`Vector2<class_Vector2>`. Giá trị này có thể được xác định bằng :ref:`RenderingServer.mesh_surface_get_format_skin_stride()<class_RenderingServer_method_mesh_surface_get_format_skin_stride>`.

Có thể thay đổi điểm bắt đầu cập nhật bằng ``offset``. Trong hầu hết trường hợp, giá trị của ``offset`` phải là bội số của 12 byte để căn chỉnh theo từng skin.

Một :ref:`PackedVector3Array<class_PackedVector3Array>` các vị trí skin có thể được chuyển đổi thành :ref:`PackedByteArray<class_PackedByteArray>` bằng :ref:`PackedVector3Array.to_byte_array()<class_PackedVector3Array_method_to_byte_array>` để sử dụng trong ``data``.

.. rst-class:: classref-item-separator

----

.. _class_ArrayMesh_method_surface_update_vertex_region:

.. rst-class:: classref-method

|void| **surface_update_vertex_region**\ (\ surf_idx\: :ref:`int<class_int>`, offset\: :ref:`int<class_int>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_ArrayMesh_method_surface_update_vertex_region>`

Cập nhật vertex buffer của surface của mesh này bằng ``data`` đã cho. Dữ liệu dự kiến cho mỗi vertex là 12 hoặc 8 byte (4 byte cho mỗi float, 2 float cho mỗi :ref:`Vector2<class_Vector2>` và 3 float cho mỗi :ref:`Vector3<class_Vector3>`), tùy thuộc vào việc mesh sử dụng vertex :ref:`Vector3<class_Vector3>` hay :ref:`Vector2<class_Vector2>`. Có thể xác định giá trị này bằng :ref:`RenderingServer.mesh_surface_get_format_vertex_stride()<class_RenderingServer_method_mesh_surface_get_format_vertex_stride>`.

Có thể thay đổi điểm bắt đầu của các bản cập nhật bằng ``offset``. Trong hầu hết trường hợp, giá trị của ``offset`` phải là bội số của 12 byte để căn chỉnh theo từng vertex.

Một :ref:`PackedVector3Array<class_PackedVector3Array>` gồm các vị trí vertex có thể được chuyển đổi thành :ref:`PackedByteArray<class_PackedByteArray>` bằng :ref:`PackedVector3Array.to_byte_array()<class_PackedVector3Array_method_to_byte_array>` để sử dụng trong ``data``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
