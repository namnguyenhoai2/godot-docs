:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ImporterMesh.xml.

.. _class_ImporterMesh:

ImporterMesh
============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`Resource<class_Resource>` chứa hình học dựa trên mảng đỉnh trong quá trình import.

.. rst-class:: classref-introduction-group

Mô tả
-----

ImporterMesh là một kiểu :ref:`Resource<class_Resource>` tương tự như :ref:`ArrayMesh<class_ArrayMesh>`. Nó chứa hình học dựa trên mảng đỉnh, được chia thành các *surface*. Mỗi surface chứa một mảng hoàn toàn riêng biệt và một material dùng để vẽ nó. Về mặt thiết kế, mesh có nhiều surface được ưu tiên hơn mesh chỉ có một surface, vì các object được tạo trong phần mềm chỉnh sửa 3D thường chứa nhiều material.

Không giống đối tượng tương ứng trong runtime, **ImporterMesh** chứa dữ liệu mesh trước khi thực hiện các bước import khác nhau, chẳng hạn như tạo LOD và shadow mesh. Sửa đổi dữ liệu surface bằng cách gọi :ref:`clear()<class_ImporterMesh_method_clear>`, sau đó gọi :ref:`add_surface()<class_ImporterMesh_method_add_surface>` cho từng surface.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`add_blend_shape<class_ImporterMesh_method_add_blend_shape>`\ (\ name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                                                                                                                |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`add_surface<class_ImporterMesh_method_add_surface>`\ (\ primitive\: :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`, arrays\: :ref:`Array<class_Array>`, blend_shapes\: :ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\] = [], lods\: :ref:`Dictionary<class_Dictionary>` = {}, material\: :ref:`Material<class_Material>` = null, name\: :ref:`String<class_String>` = "", flags\: :ref:`int<class_int>` = 0\ ) |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`clear<class_ImporterMesh_method_clear>`\ (\ )                                                                                                                                                                                                                                                                                                                                                                        |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ImporterMesh<class_ImporterMesh>`         | :ref:`from_mesh<class_ImporterMesh_method_from_mesh>`\ (\ mesh\: :ref:`Mesh<class_Mesh>`\ ) |static|                                                                                                                                                                                                                                                                                                                       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`generate_lods<class_ImporterMesh_method_generate_lods>`\ (\ normal_merge_angle\: :ref:`float<class_float>`, normal_split_angle\: :ref:`float<class_float>`, bone_transform_array\: :ref:`Array<class_Array>`\ )                                                                                                                                                                                                      |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_blend_shape_count<class_ImporterMesh_method_get_blend_shape_count>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` | :ref:`get_blend_shape_mode<class_ImporterMesh_method_get_blend_shape_mode>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                  |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                     | :ref:`get_blend_shape_name<class_ImporterMesh_method_get_blend_shape_name>`\ (\ blend_shape_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                         |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2i<class_Vector2i>`                 | :ref:`get_lightmap_size_hint<class_ImporterMesh_method_get_lightmap_size_hint>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ArrayMesh<class_ArrayMesh>`               | :ref:`get_mesh<class_ImporterMesh_method_get_mesh>`\ (\ base_mesh\: :ref:`ArrayMesh<class_ArrayMesh>` = null\ )                                                                                                                                                                                                                                                                                                            |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                       | :ref:`get_surface_arrays<class_ImporterMesh_method_get_surface_arrays>`\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                       | :ref:`get_surface_blend_shape_arrays<class_ImporterMesh_method_get_surface_blend_shape_arrays>`\ (\ surface_idx\: :ref:`int<class_int>`, blend_shape_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_surface_count<class_ImporterMesh_method_get_surface_count>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                        |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_surface_format<class_ImporterMesh_method_get_surface_format>`\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_surface_lod_count<class_ImporterMesh_method_get_surface_lod_count>`\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                           |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`get_surface_lod_indices<class_ImporterMesh_method_get_surface_lod_indices>`\ (\ surface_idx\: :ref:`int<class_int>`, lod_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                      |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`get_surface_lod_size<class_ImporterMesh_method_get_surface_lod_size>`\ (\ surface_idx\: :ref:`int<class_int>`, lod_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                            |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Material<class_Material>`                 | :ref:`get_surface_material<class_ImporterMesh_method_get_surface_material>`\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                     | :ref:`get_surface_name<class_ImporterMesh_method_get_surface_name>`\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                                                     |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`   | :ref:`get_surface_primitive_type<class_ImporterMesh_method_get_surface_primitive_type>`\ (\ surface_idx\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                         |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ImporterMesh<class_ImporterMesh>`         | :ref:`merge_importer_meshes<class_ImporterMesh_method_merge_importer_meshes>`\ (\ importer_meshes\: :ref:`Array<class_Array>`\[:ref:`ImporterMesh<class_ImporterMesh>`\], relative_transforms\: :ref:`Array<class_Array>`\[:ref:`Transform3D<class_Transform3D>`\], deduplicate_surfaces\: :ref:`bool<class_bool>` = true\ ) |static|                                                                                      |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_blend_shape_mode<class_ImporterMesh_method_set_blend_shape_mode>`\ (\ mode\: :ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>`\ )                                                                                                                                                                                                                                                                                  |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_lightmap_size_hint<class_ImporterMesh_method_set_lightmap_size_hint>`\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ )                                                                                                                                                                                                                                                                                              |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_surface_material<class_ImporterMesh_method_set_surface_material>`\ (\ surface_idx\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ )                                                                                                                                                                                                                                                         |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_surface_name<class_ImporterMesh_method_set_surface_name>`\ (\ surface_idx\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                                                                         |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_ImporterMesh_method_add_blend_shape:

.. rst-class:: classref-method

|void| **add_blend_shape**\ (\ name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ImporterMesh_method_add_blend_shape>`

Thêm name cho một blend shape sẽ được thêm bằng :ref:`add_surface()<class_ImporterMesh_method_add_surface>`. Phải được gọi trước khi thêm surface.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_add_surface:

.. rst-class:: classref-method

|void| **add_surface**\ (\ primitive\: :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`, arrays\: :ref:`Array<class_Array>`, blend_shapes\: :ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\] = [], lods\: :ref:`Dictionary<class_Dictionary>` = {}, material\: :ref:`Material<class_Material>` = null, name\: :ref:`String<class_String>` = "", flags\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ImporterMesh_method_add_surface>`

Tạo một surface mới. :ref:`Mesh.get_surface_count()<class_Mesh_method_get_surface_count>` sẽ trở thành ``surf_idx`` cho surface mới này.

Các surface được tạo để kết xuất bằng ``primitive``, có thể là bất kỳ giá trị nào được định nghĩa trong :ref:`PrimitiveType<enum_Mesh_PrimitiveType>`.

Đối số ``arrays`` là một mảng các mảng. Mỗi phần tử :ref:`Mesh.ARRAY_MAX<class_Mesh_constant_ARRAY_MAX>` chứa một mảng với một phần dữ liệu mesh của surface này như được mô tả bởi thành viên tương ứng của :ref:`ArrayType<enum_Mesh_ArrayType>` hoặc ``null`` nếu surface không sử dụng nó. Ví dụ, ``arrays[0]`` là mảng các đỉnh. Mảng con đỉnh đầu tiên luôn bắt buộc; các mảng còn lại là tùy chọn. Việc thêm một mảng chỉ mục sẽ đưa surface này vào "chế độ chỉ mục", trong đó mảng đỉnh và các mảng khác trở thành nguồn dữ liệu, còn mảng chỉ mục xác định thứ tự đỉnh. Tất cả các mảng con phải có cùng độ dài với mảng đỉnh (hoặc là bội số chính xác của độ dài mảng đỉnh, khi nhiều phần tử của một mảng con tương ứng với một đỉnh) hoặc phải rỗng, ngoại trừ :ref:`Mesh.ARRAY_INDEX<class_Mesh_constant_ARRAY_INDEX>` nếu được sử dụng.

Đối số ``blend_shapes`` là một mảng dữ liệu đỉnh cho mỗi blend shape. Mỗi phần tử là một mảng có cùng cấu trúc với ``arrays``, nhưng :ref:`Mesh.ARRAY_VERTEX<class_Mesh_constant_ARRAY_VERTEX>`, :ref:`Mesh.ARRAY_NORMAL<class_Mesh_constant_ARRAY_NORMAL>` và :ref:`Mesh.ARRAY_TANGENT<class_Mesh_constant_ARRAY_TANGENT>` được thiết lập khi và chỉ khi chúng được thiết lập trong ``arrays``, còn tất cả các mục khác là ``null``.

Đối số ``lods`` là một dictionary với các key :ref:`float<class_float>` và các value :ref:`PackedInt32Array<class_PackedInt32Array>`. Mỗi mục trong dictionary biểu diễn một cấp độ LOD của surface, trong đó value là mảng :ref:`Mesh.ARRAY_INDEX<class_Mesh_constant_ARRAY_INDEX>` cần dùng cho cấp độ LOD, còn key tỷ lệ gần đúng với khoảng cách tại đó các thiết lập LOD được sử dụng. Tức là, việc tăng key của một LOD cũng làm tăng khoảng cách mà object phải cách camera trước khi LOD được sử dụng.

Đối số ``flags`` là phép OR theo bit của các giá trị cần thiết: một giá trị :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` dịch trái ``ARRAY_FORMAT_CUSTOMn_SHIFT`` bit cho mỗi custom channel đang được sử dụng, :ref:`Mesh.ARRAY_FLAG_USE_DYNAMIC_UPDATE<class_Mesh_constant_ARRAY_FLAG_USE_DYNAMIC_UPDATE>`, :ref:`Mesh.ARRAY_FLAG_USE_8_BONE_WEIGHTS<class_Mesh_constant_ARRAY_FLAG_USE_8_BONE_WEIGHTS>` hoặc :ref:`Mesh.ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY<class_Mesh_constant_ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY>`.

\ **Lưu ý:** Khi sử dụng chỉ mục, bạn chỉ nên dùng points, lines hoặc triangles.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_ImporterMesh_method_clear>`

Xóa tất cả surface và blend shape khỏi **ImporterMesh** này.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_from_mesh:

.. rst-class:: classref-method

:ref:`ImporterMesh<class_ImporterMesh>` **from_mesh**\ (\ mesh\: :ref:`Mesh<class_Mesh>`\ ) |static| :ref:`🔗<class_ImporterMesh_method_from_mesh>`

Chuyển :ref:`Mesh<class_Mesh>` đã cho thành một **ImporterMesh** bằng cách sao chép tất cả surface, blend shape, material và metadata của nó vào một object **ImporterMesh** mới.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_generate_lods:

.. rst-class:: classref-method

|void| **generate_lods**\ (\ normal_merge_angle\: :ref:`float<class_float>`, normal_split_angle\: :ref:`float<class_float>`, bone_transform_array\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_ImporterMesh_method_generate_lods>`

Tạo tất cả LOD cho ImporterMesh này.

\ ``normal_merge_angle`` tính theo độ và được sử dụng giống như các thiết lập import trong ``lods``.

\ ``normal_split_angle`` không được sử dụng và chỉ còn lại để tương thích với các phiên bản API cũ hơn.

Có thể truy cập số lượng LOD được tạo bằng :ref:`get_surface_lod_count()<class_ImporterMesh_method_get_surface_lod_count>`, và từng LOD có sẵn trong :ref:`get_surface_lod_size()<class_ImporterMesh_method_get_surface_lod_size>` và :ref:`get_surface_lod_indices()<class_ImporterMesh_method_get_surface_lod_indices>`.

\ ``bone_transform_array`` là một :ref:`Array<class_Array>`, có thể rỗng hoặc chứa các :ref:`Transform3D<class_Transform3D>`\ s. Với mỗi bone ID của mesh, các giá trị này sẽ áp dụng mesh skinning khi tạo các biến thể mesh LOD. Điều này thường được dùng để xử lý sự khác biệt về tỷ lệ giữa bản thân mesh và dữ liệu skinning của nó.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_blend_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_blend_shape_count**\ (\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_blend_shape_count>`

Trả về số lượng blend shape mà mesh chứa.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_blend_shape_mode:

.. rst-class:: classref-method

:ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` **get_blend_shape_mode**\ (\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_blend_shape_mode>`

Trả về chế độ blend shape của Mesh này.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_blend_shape_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_blend_shape_name**\ (\ blend_shape_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_blend_shape_name>`

Trả về name của blend shape tại chỉ mục này.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_lightmap_size_hint:

.. rst-class:: classref-method

:ref:`Vector2i<class_Vector2i>` **get_lightmap_size_hint**\ (\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_lightmap_size_hint>`

Trả về gợi ý kích thước của mesh này để unwrap lightmap trong không gian UV.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_mesh:

.. rst-class:: classref-method

:ref:`ArrayMesh<class_ArrayMesh>` **get_mesh**\ (\ base_mesh\: :ref:`ArrayMesh<class_ArrayMesh>` = null\ ) :ref:`🔗<class_ImporterMesh_method_get_mesh>`

Trả về dữ liệu mesh được biểu diễn bởi **ImporterMesh** này dưới dạng một :ref:`ArrayMesh<class_ArrayMesh>` có thể sử dụng.

Method này lưu vào cache mesh được trả về, và các lần gọi sau sẽ trả về dữ liệu trong cache cho đến khi gọi :ref:`clear()<class_ImporterMesh_method_clear>`.

Nếu chưa được lưu vào cache và ``base_mesh`` được cung cấp, ``base_mesh`` sẽ được sử dụng và thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_surface_arrays**\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_arrays>`

Trả về các mảng của đỉnh, normal, UV, v.v. tạo nên surface được yêu cầu. Xem :ref:`add_surface()<class_ImporterMesh_method_add_surface>`.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_blend_shape_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_surface_blend_shape_arrays**\ (\ surface_idx\: :ref:`int<class_int>`, blend_shape_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_blend_shape_arrays>`

Trả về một tập mảng blend shape cho chỉ mục blend shape được yêu cầu của một surface.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_surface_count**\ (\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_count>`

Trả về số lượng surface mà mesh chứa.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_format:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_surface_format**\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_format>`

Trả về format của surface mà mesh chứa.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_lod_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_surface_lod_count**\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_lod_count>`

Trả về số lượng LOD mà mesh chứa trên một surface cụ thể.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_lod_indices:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_surface_lod_indices**\ (\ surface_idx\: :ref:`int<class_int>`, lod_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_lod_indices>`

Trả về index buffer của một LOD cho một surface.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_lod_size:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_surface_lod_size**\ (\ surface_idx\: :ref:`int<class_int>`, lod_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_lod_size>`

Trả về tỷ lệ màn hình kích hoạt một LOD cho một surface.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_material:

.. rst-class:: classref-method

:ref:`Material<class_Material>` **get_surface_material**\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_material>`

Trả về một :ref:`Material<class_Material>` trong một surface cụ thể. Surface được kết xuất bằng material này.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_surface_name**\ (\ surface_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ImporterMesh_method_get_surface_name>`

Lấy name được gán cho surface này.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_get_surface_primitive_type:

.. rst-class:: classref-method

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **get_surface_primitive_type**\ (\ surface_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ImporterMesh_method_get_surface_primitive_type>`

Trả về kiểu primitive của surface được yêu cầu (xem :ref:`add_surface()<class_ImporterMesh_method_add_surface>`).

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_merge_importer_meshes:

.. rst-class:: classref-method

:ref:`ImporterMesh<class_ImporterMesh>` **merge_importer_meshes**\ (\ importer_meshes\: :ref:`Array<class_Array>`\[:ref:`ImporterMesh<class_ImporterMesh>`\], relative_transforms\: :ref:`Array<class_Array>`\[:ref:`Transform3D<class_Transform3D>`\], deduplicate_surfaces\: :ref:`bool<class_bool>` = true\ ) |static| :ref:`🔗<class_ImporterMesh_method_merge_importer_meshes>`

Hợp nhất nhiều **ImporterMesh**\ es thành một **ImporterMesh** duy nhất. Mỗi mesh đầu vào được biến đổi bởi :ref:`Transform3D<class_Transform3D>` tương ứng trong mảng ``relative_transforms``, mảng này phải có cùng kích thước với ``importer_meshes``. Các scale âm được hỗ trợ và thứ tự winding trong dữ liệu mesh sẽ được điều chỉnh để phù hợp.

Nếu ``deduplicate_surfaces`` là ``true`` và nhiều mesh có các surface cùng tên và định dạng, các surface sẽ được hợp nhất với nhau khi các mesh được hợp nhất và sẽ sử dụng material từ surface khớp đầu tiên. Điều này hữu ích để giảm số lượng surface trong mesh kết quả và tránh nhân bản material. Các surface có bone weight sẽ không bao giờ được loại bỏ trùng lặp. Nếu ``deduplicate_surfaces`` là ``false``, các surface sẽ luôn được giữ riêng biệt và được đặt tên duy nhất.

\ **Cảnh báo:** Blend shape và LOD không được hỗ trợ và sẽ bị loại bỏ. Không sử dụng hàm này để loại bỏ blend shape và LOD, vì trong tương lai các tính năng này có thể được hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_set_blend_shape_mode:

.. rst-class:: classref-method

|void| **set_blend_shape_mode**\ (\ mode\: :ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>`\ ) :ref:`🔗<class_ImporterMesh_method_set_blend_shape_mode>`

Thiết lập chế độ blend shape.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_set_lightmap_size_hint:

.. rst-class:: classref-method

|void| **set_lightmap_size_hint**\ (\ size\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_ImporterMesh_method_set_lightmap_size_hint>`

Thiết lập gợi ý kích thước của mesh này để unwrap lightmap trong không gian UV.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_set_surface_material:

.. rst-class:: classref-method

|void| **set_surface_material**\ (\ surface_idx\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ ) :ref:`🔗<class_ImporterMesh_method_set_surface_material>`

Thiết lập một :ref:`Material<class_Material>` cho surface đã cho. Surface sẽ được render bằng material này.

.. rst-class:: classref-item-separator

----

.. _class_ImporterMesh_method_set_surface_name:

.. rst-class:: classref-method

|void| **set_surface_name**\ (\ surface_idx\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ImporterMesh_method_set_surface_name>`

Thiết lập tên cho surface đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
