:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Mesh.xml.

.. _class_Mesh:

Mesh
====

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ArrayMesh<class_ArrayMesh>`, :ref:`ImmediateMesh<class_ImmediateMesh>`, :ref:`PlaceholderMesh<class_PlaceholderMesh>`, :ref:`PrimitiveMesh<class_PrimitiveMesh>`

Một :ref:`Resource<class_Resource>` chứa hình học dựa trên mảng đỉnh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Mesh là một loại :ref:`Resource<class_Resource>` chứa hình học dựa trên mảng đỉnh, được chia thành các *surface*. Mỗi surface chứa một mảng hoàn toàn riêng biệt và một material dùng để vẽ nó. Về mặt thiết kế, mesh có nhiều surface được ưu tiên hơn mesh chỉ có một surface, vì các đối tượng được tạo trong phần mềm chỉnh sửa 3D thường chứa nhiều material. Số surface tối đa trên mỗi mesh là :ref:`RenderingServer.MAX_MESH_SURFACES<class_RenderingServer_constant_MAX_MESH_SURFACES>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D Material Testers Demo <https://godotengine.org/asset-library/asset/2742>`__

- `3D Kinematic Character Demo <https://godotengine.org/asset-library/asset/2739>`__

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------+-------------------------------------------------------------------+--------------------+
   | :ref:`Vector2i<class_Vector2i>` | :ref:`lightmap_size_hint<class_Mesh_property_lightmap_size_hint>` | ``Vector2i(0, 0)`` |
   +---------------------------------+-------------------------------------------------------------------+--------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`                                   | :ref:`_get_aabb<class_Mesh_private_method__get_aabb>`\ (\ ) |virtual| |required| |const|                                                                                            |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`_get_blend_shape_count<class_Mesh_private_method__get_blend_shape_count>`\ (\ ) |virtual| |required| |const|                                                                  |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                       | :ref:`_get_blend_shape_name<class_Mesh_private_method__get_blend_shape_name>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                     |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`_get_surface_count<class_Mesh_private_method__get_surface_count>`\ (\ ) |virtual| |required| |const|                                                                          |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`_set_blend_shape_name<class_Mesh_private_method__set_blend_shape_name>`\ (\ index\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ ) |virtual| |required| |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`_surface_get_array_index_len<class_Mesh_private_method__surface_get_array_index_len>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                       |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`_surface_get_array_len<class_Mesh_private_method__surface_get_array_len>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                   |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                 | :ref:`_surface_get_arrays<class_Mesh_private_method__surface_get_arrays>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                         |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\]    | :ref:`_surface_get_blend_shape_arrays<class_Mesh_private_method__surface_get_blend_shape_arrays>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                 |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`_surface_get_format<class_Mesh_private_method__surface_get_format>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                         |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                       | :ref:`_surface_get_lods<class_Mesh_private_method__surface_get_lods>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                             |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Material<class_Material>`                           | :ref:`_surface_get_material<class_Mesh_private_method__surface_get_material>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                     |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`_surface_get_primitive_type<class_Mesh_private_method__surface_get_primitive_type>`\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                         |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`_surface_set_material<class_Mesh_private_method__surface_set_material>`\ (\ index\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ ) |virtual| |required| |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>`   | :ref:`create_convex_shape<class_Mesh_method_create_convex_shape>`\ (\ clean\: :ref:`bool<class_bool>` = true, simplify\: :ref:`bool<class_bool>` = false\ ) |const|                 |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Mesh<class_Mesh>`                                   | :ref:`create_outline<class_Mesh_method_create_outline>`\ (\ margin\: :ref:`float<class_float>`\ ) |const|                                                                           |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>`                           | :ref:`create_placeholder<class_Mesh_method_create_placeholder>`\ (\ ) |const|                                                                                                       |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` | :ref:`create_trimesh_shape<class_Mesh_method_create_trimesh_shape>`\ (\ ) |const|                                                                                                   |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TriangleMesh<class_TriangleMesh>`                   | :ref:`generate_triangle_mesh<class_Mesh_method_generate_triangle_mesh>`\ (\ ) |const|                                                                                               |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`                                   | :ref:`get_aabb<class_Mesh_method_get_aabb>`\ (\ ) |const|                                                                                                                           |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`       | :ref:`get_faces<class_Mesh_method_get_faces>`\ (\ ) |const|                                                                                                                         |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                     | :ref:`get_surface_count<class_Mesh_method_get_surface_count>`\ (\ ) |const|                                                                                                         |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                 | :ref:`surface_get_arrays<class_Mesh_method_surface_get_arrays>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                     |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\]    | :ref:`surface_get_blend_shape_arrays<class_Mesh_method_surface_get_blend_shape_arrays>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                             |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Material<class_Material>`                           | :ref:`surface_get_material<class_Mesh_method_surface_get_material>`\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const|                                                                 |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`surface_set_material<class_Mesh_method_surface_set_material>`\ (\ surf_idx\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ )                             |
   +-----------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Mesh_PrimitiveType:

.. rst-class:: classref-enumeration

enum **PrimitiveType**: :ref:`🔗<enum_Mesh_PrimitiveType>`

.. _class_Mesh_constant_PRIMITIVE_POINTS:

.. rst-class:: classref-enumeration-constant

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **PRIMITIVE_POINTS** = ``0``

Render mảng dưới dạng các điểm (mỗi đỉnh tương ứng với một điểm).

.. _class_Mesh_constant_PRIMITIVE_LINES:

.. rst-class:: classref-enumeration-constant

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **PRIMITIVE_LINES** = ``1``

Render mảng dưới dạng các đường (cứ mỗi hai đỉnh sẽ tạo thành một đường).

.. _class_Mesh_constant_PRIMITIVE_LINE_STRIP:

.. rst-class:: classref-enumeration-constant

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **PRIMITIVE_LINE_STRIP** = ``2``

Render mảng dưới dạng line strip.

.. _class_Mesh_constant_PRIMITIVE_TRIANGLES:

.. rst-class:: classref-enumeration-constant

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **PRIMITIVE_TRIANGLES** = ``3``

Render mảng dưới dạng các tam giác (cứ mỗi ba đỉnh sẽ tạo thành một tam giác).

.. _class_Mesh_constant_PRIMITIVE_TRIANGLE_STRIP:

.. rst-class:: classref-enumeration-constant

:ref:`PrimitiveType<enum_Mesh_PrimitiveType>` **PRIMITIVE_TRIANGLE_STRIP** = ``4``

Render mảng dưới dạng triangle strip.

.. rst-class:: classref-item-separator

----

.. _enum_Mesh_ArrayType:

.. rst-class:: classref-enumeration

enum **ArrayType**: :ref:`🔗<enum_Mesh_ArrayType>`

.. _class_Mesh_constant_ARRAY_VERTEX:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_VERTEX** = ``0``

:ref:`PackedVector3Array<class_PackedVector3Array>`, :ref:`PackedVector2Array<class_PackedVector2Array>`, hoặc :ref:`Array<class_Array>` của các vị trí đỉnh.

.. _class_Mesh_constant_ARRAY_NORMAL:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_NORMAL** = ``1``

:ref:`PackedVector3Array<class_PackedVector3Array>` của các vector pháp tuyến đỉnh.

\ **Lưu ý:** Mảng phải gồm các vector pháp tuyến, nếu không chúng sẽ được engine chuẩn hóa, có thể gây ra sai khác về hình ảnh.

.. _class_Mesh_constant_ARRAY_TANGENT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_TANGENT** = ``2``

:ref:`PackedFloat32Array<class_PackedFloat32Array>` của các tangent đỉnh. Mỗi phần tử gồm các nhóm 4 số thực, 3 số thực đầu tiên xác định tangent, còn số cuối xác định hướng binormal là -1 hoặc 1.

.. _class_Mesh_constant_ARRAY_COLOR:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_COLOR** = ``3``

:ref:`PackedColorArray<class_PackedColorArray>` của các màu đỉnh.

.. _class_Mesh_constant_ARRAY_TEX_UV:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_TEX_UV** = ``4``

:ref:`PackedVector2Array<class_PackedVector2Array>` cho các tọa độ UV.

.. _class_Mesh_constant_ARRAY_TEX_UV2:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_TEX_UV2** = ``5``

:ref:`PackedVector2Array<class_PackedVector2Array>` cho các tọa độ UV thứ hai.

.. _class_Mesh_constant_ARRAY_CUSTOM0:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_CUSTOM0** = ``6``

Chứa kênh màu tùy chỉnh 0. :ref:`PackedByteArray<class_PackedByteArray>` nếu ``(format >> Mesh.ARRAY_FORMAT_CUSTOM0_SHIFT) & Mesh.ARRAY_FORMAT_CUSTOM_MASK`` là :ref:`ARRAY_CUSTOM_RGBA8_UNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_UNORM>`, :ref:`ARRAY_CUSTOM_RGBA8_SNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_SNORM>`, :ref:`ARRAY_CUSTOM_RG_HALF<class_Mesh_constant_ARRAY_CUSTOM_RG_HALF>`, hoặc :ref:`ARRAY_CUSTOM_RGBA_HALF<class_Mesh_constant_ARRAY_CUSTOM_RGBA_HALF>`. Nếu không thì :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. _class_Mesh_constant_ARRAY_CUSTOM1:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_CUSTOM1** = ``7``

Chứa kênh màu tùy chỉnh 1. :ref:`PackedByteArray<class_PackedByteArray>` nếu ``(format >> Mesh.ARRAY_FORMAT_CUSTOM1_SHIFT) & Mesh.ARRAY_FORMAT_CUSTOM_MASK`` là :ref:`ARRAY_CUSTOM_RGBA8_UNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_UNORM>`, :ref:`ARRAY_CUSTOM_RGBA8_SNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_SNORM>`, :ref:`ARRAY_CUSTOM_RG_HALF<class_Mesh_constant_ARRAY_CUSTOM_RG_HALF>`, hoặc :ref:`ARRAY_CUSTOM_RGBA_HALF<class_Mesh_constant_ARRAY_CUSTOM_RGBA_HALF>`. Nếu không thì :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. _class_Mesh_constant_ARRAY_CUSTOM2:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_CUSTOM2** = ``8``

Chứa kênh màu tùy chỉnh 2. :ref:`PackedByteArray<class_PackedByteArray>` nếu ``(format >> Mesh.ARRAY_FORMAT_CUSTOM2_SHIFT) & Mesh.ARRAY_FORMAT_CUSTOM_MASK`` là :ref:`ARRAY_CUSTOM_RGBA8_UNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_UNORM>`, :ref:`ARRAY_CUSTOM_RGBA8_SNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_SNORM>`, :ref:`ARRAY_CUSTOM_RG_HALF<class_Mesh_constant_ARRAY_CUSTOM_RG_HALF>`, hoặc :ref:`ARRAY_CUSTOM_RGBA_HALF<class_Mesh_constant_ARRAY_CUSTOM_RGBA_HALF>`. Nếu không thì :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. _class_Mesh_constant_ARRAY_CUSTOM3:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_CUSTOM3** = ``9``

Chứa kênh màu tùy chỉnh 3. :ref:`PackedByteArray<class_PackedByteArray>` nếu ``(format >> Mesh.ARRAY_FORMAT_CUSTOM3_SHIFT) & Mesh.ARRAY_FORMAT_CUSTOM_MASK`` là :ref:`ARRAY_CUSTOM_RGBA8_UNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_UNORM>`, :ref:`ARRAY_CUSTOM_RGBA8_SNORM<class_Mesh_constant_ARRAY_CUSTOM_RGBA8_SNORM>`, :ref:`ARRAY_CUSTOM_RG_HALF<class_Mesh_constant_ARRAY_CUSTOM_RG_HALF>`, hoặc :ref:`ARRAY_CUSTOM_RGBA_HALF<class_Mesh_constant_ARRAY_CUSTOM_RGBA_HALF>`. Nếu không thì :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. _class_Mesh_constant_ARRAY_BONES:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_BONES** = ``10``

:ref:`PackedFloat32Array<class_PackedFloat32Array>` hoặc :ref:`PackedInt32Array<class_PackedInt32Array>` của các chỉ số xương. Chứa 4 hoặc 8 số trên mỗi đỉnh, tùy thuộc vào sự hiện diện của cờ :ref:`ARRAY_FLAG_USE_8_BONE_WEIGHTS<class_Mesh_constant_ARRAY_FLAG_USE_8_BONE_WEIGHTS>`.

.. _class_Mesh_constant_ARRAY_WEIGHTS:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_WEIGHTS** = ``11``

:ref:`PackedFloat32Array<class_PackedFloat32Array>` hoặc :ref:`PackedFloat64Array<class_PackedFloat64Array>` của các trọng số xương trong khoảng từ ``0.0`` đến ``1.0`` (bao gồm cả hai đầu mút). Chứa 4 hoặc 8 số trên mỗi đỉnh, tùy thuộc vào sự hiện diện của cờ :ref:`ARRAY_FLAG_USE_8_BONE_WEIGHTS<class_Mesh_constant_ARRAY_FLAG_USE_8_BONE_WEIGHTS>`.

.. _class_Mesh_constant_ARRAY_INDEX:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_INDEX** = ``12``

:ref:`PackedInt32Array<class_PackedInt32Array>` gồm các số nguyên được dùng làm chỉ số tham chiếu đến các đỉnh, màu, pháp tuyến, tangent và texture. Tất cả các mảng đó phải có cùng số phần tử với mảng đỉnh. Không chỉ số nào được vượt quá kích thước mảng đỉnh. Khi có mảng chỉ số này, hàm sẽ chuyển sang "index mode", trong đó chỉ số chọn đỉnh, pháp tuyến, tangent, màu, UV, v.v. thứ *i*. Điều này có nghĩa là nếu muốn có các pháp tuyến hoặc màu khác nhau dọc theo một cạnh, bạn phải nhân bản các đỉnh.

Đối với các tam giác, mảng chỉ số được diễn giải thành các bộ ba, tham chiếu đến các đỉnh của mỗi tam giác. Đối với các đường, mảng chỉ số được chia thành các cặp chỉ vị trí bắt đầu và kết thúc của mỗi đường.

.. _class_Mesh_constant_ARRAY_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayType<enum_Mesh_ArrayType>` **ARRAY_MAX** = ``13``

Biểu thị kích thước của enum :ref:`ArrayType<enum_Mesh_ArrayType>`.

.. rst-class:: classref-item-separator

----

.. _enum_Mesh_ArrayCustomFormat:

.. rst-class:: classref-enumeration

enum **ArrayCustomFormat**: :ref:`🔗<enum_Mesh_ArrayCustomFormat>`

.. _class_Mesh_constant_ARRAY_CUSTOM_RGBA8_UNORM:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RGBA8_UNORM** = ``0``

Cho biết kênh tùy chỉnh này chứa các màu byte unsigned normalized từ 0 đến 1, được mã hóa dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`.

.. _class_Mesh_constant_ARRAY_CUSTOM_RGBA8_SNORM:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RGBA8_SNORM** = ``1``

Cho biết kênh tùy chỉnh này chứa các màu byte signed normalized từ -1 đến 1, được mã hóa dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`.

.. _class_Mesh_constant_ARRAY_CUSTOM_RG_HALF:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RG_HALF** = ``2``

Cho biết kênh tùy chỉnh này chứa các màu float độ chính xác nửa, được mã hóa dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`. Chỉ sử dụng các kênh đỏ và xanh lá.

.. _class_Mesh_constant_ARRAY_CUSTOM_RGBA_HALF:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RGBA_HALF** = ``3``

Cho biết kênh tùy chỉnh này chứa các màu float độ chính xác nửa, được mã hóa dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`.

.. _class_Mesh_constant_ARRAY_CUSTOM_R_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_R_FLOAT** = ``4``

Cho biết kênh tùy chỉnh này chứa các màu float độ chính xác đầy đủ, trong một :ref:`PackedFloat32Array<class_PackedFloat32Array>`. Chỉ sử dụng kênh đỏ.

.. _class_Mesh_constant_ARRAY_CUSTOM_RG_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RG_FLOAT** = ``5``

Cho biết kênh tùy chỉnh này chứa các màu float độ chính xác đầy đủ, trong một :ref:`PackedFloat32Array<class_PackedFloat32Array>`. Chỉ sử dụng các kênh đỏ và xanh lá.

.. _class_Mesh_constant_ARRAY_CUSTOM_RGB_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RGB_FLOAT** = ``6``

Cho biết kênh tùy chỉnh này chứa các màu float độ chính xác đầy đủ, trong một :ref:`PackedFloat32Array<class_PackedFloat32Array>`. Chỉ sử dụng các kênh đỏ, xanh lá và xanh dương.

.. _class_Mesh_constant_ARRAY_CUSTOM_RGBA_FLOAT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_RGBA_FLOAT** = ``7``

Cho biết kênh tùy chỉnh này chứa các màu float độ chính xác đầy đủ, trong một :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. _class_Mesh_constant_ARRAY_CUSTOM_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` **ARRAY_CUSTOM_MAX** = ``8``

Biểu thị kích thước của enum :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>`.

.. rst-class:: classref-item-separator

----

.. _enum_Mesh_ArrayFormat:

.. rst-class:: classref-enumeration

flags **ArrayFormat**: :ref:`🔗<enum_Mesh_ArrayFormat>`

.. _class_Mesh_constant_ARRAY_FORMAT_VERTEX:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_VERTEX** = ``1``

Mảng Mesh chứa các đỉnh. Mọi mesh đều yêu cầu một mảng đỉnh, vì vậy mảng này luôn phải hiện diện.

.. _class_Mesh_constant_ARRAY_FORMAT_NORMAL:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_NORMAL** = ``2``

Mảng Mesh chứa các pháp tuyến.

.. _class_Mesh_constant_ARRAY_FORMAT_TANGENT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_TANGENT** = ``4``

Mảng Mesh chứa các tangent.

.. _class_Mesh_constant_ARRAY_FORMAT_COLOR:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_COLOR** = ``8``

Mảng Mesh chứa các màu.

.. _class_Mesh_constant_ARRAY_FORMAT_TEX_UV:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_TEX_UV** = ``16``

Mảng Mesh chứa các UV.

.. _class_Mesh_constant_ARRAY_FORMAT_TEX_UV2:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_TEX_UV2** = ``32``

Mảng Mesh chứa UV thứ hai.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM0:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM0** = ``64``

Mảng Mesh chứa kênh tùy chỉnh có chỉ số 0.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM1:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM1** = ``128``

Mảng Mesh chứa kênh tùy chỉnh có chỉ số 1.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM2:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM2** = ``256``

Mảng Mesh chứa kênh tùy chỉnh có chỉ số 2.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM3:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM3** = ``512``

Mảng Mesh chứa kênh tùy chỉnh có chỉ số 3.

.. _class_Mesh_constant_ARRAY_FORMAT_BONES:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_BONES** = ``1024``

Mảng Mesh chứa các xương.

.. _class_Mesh_constant_ARRAY_FORMAT_WEIGHTS:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_WEIGHTS** = ``2048``

Mảng Mesh chứa các trọng số xương.

.. _class_Mesh_constant_ARRAY_FORMAT_INDEX:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_INDEX** = ``4096``

Mảng Mesh sử dụng các chỉ số.

.. _class_Mesh_constant_ARRAY_FORMAT_BLEND_SHAPE_MASK:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_BLEND_SHAPE_MASK** = ``7``

Mặt nạ của các kênh mesh được cho phép trong blend shape.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM_BASE:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM_BASE** = ``13``

Độ dịch của kênh tùy chỉnh đầu tiên.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM_BITS:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM_BITS** = ``3``

Số bit định dạng trên mỗi kênh tùy chỉnh. Xem :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>`.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM0_SHIFT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM0_SHIFT** = ``13``

Lượng cần dịch chuyển :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` cho chỉ mục kênh tùy chỉnh 0.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM1_SHIFT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM1_SHIFT** = ``16``

Lượng cần dịch chuyển :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` cho chỉ mục kênh tùy chỉnh 1.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM2_SHIFT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM2_SHIFT** = ``19``

Lượng cần dịch chuyển :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` cho chỉ mục kênh tùy chỉnh 2.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM3_SHIFT:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM3_SHIFT** = ``22``

Lượng cần dịch chuyển :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>` cho chỉ mục kênh tùy chỉnh 3.

.. _class_Mesh_constant_ARRAY_FORMAT_CUSTOM_MASK:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FORMAT_CUSTOM_MASK** = ``7``

Mask của các bit định dạng tùy chỉnh trên mỗi kênh tùy chỉnh. Phải được dịch chuyển bằng một trong các hằng số SHIFT. Xem :ref:`ArrayCustomFormat<enum_Mesh_ArrayCustomFormat>`.

.. _class_Mesh_constant_ARRAY_COMPRESS_FLAGS_BASE:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_COMPRESS_FLAGS_BASE** = ``25``

Vị trí dịch chuyển của cờ nén đầu tiên. Các cờ nén phải được truyền vào :ref:`ArrayMesh.add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>` và :ref:`SurfaceTool.commit()<class_SurfaceTool_method_commit>`.

.. _class_Mesh_constant_ARRAY_FLAG_USE_2D_VERTICES:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FLAG_USE_2D_VERTICES** = ``33554432``

Cờ dùng để đánh dấu rằng mảng chứa các đỉnh 2D.

.. _class_Mesh_constant_ARRAY_FLAG_USE_DYNAMIC_UPDATE:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FLAG_USE_DYNAMIC_UPDATE** = ``67108864``

Cờ dùng để đánh dấu rằng dữ liệu mesh sẽ sử dụng ``GL_DYNAMIC_DRAW`` trên GLES. Không được sử dụng trên Vulkan.

.. _class_Mesh_constant_ARRAY_FLAG_USE_8_BONE_WEIGHTS:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FLAG_USE_8_BONE_WEIGHTS** = ``134217728``

Cờ dùng để đánh dấu rằng mesh chứa tối đa 8 ảnh hưởng xương trên mỗi đỉnh. Cờ này cho biết các phần tử :ref:`ARRAY_BONES<class_Mesh_constant_ARRAY_BONES>` và :ref:`ARRAY_WEIGHTS<class_Mesh_constant_ARRAY_WEIGHTS>` sẽ có độ dài gấp đôi.

.. _class_Mesh_constant_ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FLAG_USES_EMPTY_VERTEX_ARRAY** = ``268435456``

Cờ dùng để đánh dấu rằng mesh cố ý không chứa mảng đỉnh.

.. _class_Mesh_constant_ARRAY_FLAG_COMPRESS_ATTRIBUTES:

.. rst-class:: classref-enumeration-constant

:ref:`ArrayFormat<enum_Mesh_ArrayFormat>` **ARRAY_FLAG_COMPRESS_ATTRIBUTES** = ``536870912``

Cờ dùng để đánh dấu rằng mesh đang sử dụng các thuộc tính đã nén (đỉnh, pháp tuyến, tiếp tuyến, UV). Khi bật dạng nén này, vị trí đỉnh sẽ được đóng gói vào một thuộc tính RGBA16UNORM và được scale trong vertex shader. Pháp tuyến và tiếp tuyến sẽ được đóng gói vào một RG16UNORM biểu diễn một trục, cùng với một số thực 16 bit được lưu trong kênh A của đỉnh. UV sẽ sử dụng các số thực chuẩn hóa 16 bit thay vì các số thực có dấu 32 bit đầy đủ. Khi sử dụng chế độ nén này, bạn phải sử dụng либо đỉnh, pháp tuyến và tiếp tuyến, hoặc chỉ đỉnh. Bạn không thể sử dụng pháp tuyến mà không có tiếp tuyến. Importer sẽ tự động bật chế độ nén này nếu có thể.

.. rst-class:: classref-item-separator

----

.. _enum_Mesh_BlendShapeMode:

.. rst-class:: classref-enumeration

enum **BlendShapeMode**: :ref:`🔗<enum_Mesh_BlendShapeMode>`

.. _class_Mesh_constant_BLEND_SHAPE_MODE_NORMALIZED:

.. rst-class:: classref-enumeration-constant

:ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` **BLEND_SHAPE_MODE_NORMALIZED** = ``0``

Blend shape được chuẩn hóa.

.. _class_Mesh_constant_BLEND_SHAPE_MODE_RELATIVE:

.. rst-class:: classref-enumeration-constant

:ref:`BlendShapeMode<enum_Mesh_BlendShapeMode>` **BLEND_SHAPE_MODE_RELATIVE** = ``1``

Blend shape tương đối với trọng số cơ sở.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Mesh_property_lightmap_size_hint:

.. rst-class:: classref-property

:ref:`Vector2i<class_Vector2i>` **lightmap_size_hint** = ``Vector2i(0, 0)`` :ref:`🔗<class_Mesh_property_lightmap_size_hint>`

.. rst-class:: classref-property-setget

- |void| **set_lightmap_size_hint**\ (\ value\: :ref:`Vector2i<class_Vector2i>`\ ) - :ref:`Vector2i<class_Vector2i>` **get_lightmap_size_hint**\ (\ )

Đặt gợi ý được sử dụng cho độ phân giải lightmap.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Mesh_private_method__get_aabb:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **_get_aabb**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__get_aabb>`

Phương thức ảo dùng để override :ref:`AABB<class_AABB>` cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__get_blend_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_blend_shape_count**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__get_blend_shape_count>`

Phương thức ảo dùng để override số lượng blend shape cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__get_blend_shape_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **_get_blend_shape_name**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__get_blend_shape_name>`

Phương thức ảo dùng để override việc lấy tên blend shape cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__get_surface_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_surface_count**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__get_surface_count>`

Phương thức ảo dùng để override số lượng surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__set_blend_shape_name:

.. rst-class:: classref-method

|void| **_set_blend_shape_name**\ (\ index\: :ref:`int<class_int>`, name\: :ref:`StringName<class_StringName>`\ ) |virtual| |required| :ref:`🔗<class_Mesh_private_method__set_blend_shape_name>`

Phương thức ảo dùng để override tên của các blend shape cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_array_index_len:

.. rst-class:: classref-method

:ref:`int<class_int>` **_surface_get_array_index_len**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_array_index_len>`

Phương thức ảo dùng để override độ dài chỉ mục mảng của surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_array_len:

.. rst-class:: classref-method

:ref:`int<class_int>` **_surface_get_array_len**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_array_len>`

Phương thức ảo dùng để override độ dài mảng của surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **_surface_get_arrays**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_arrays>`

Phương thức ảo dùng để override các mảng surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_blend_shape_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\] **_surface_get_blend_shape_arrays**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_blend_shape_arrays>`

Phương thức ảo dùng để override các mảng blend shape cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_format:

.. rst-class:: classref-method

:ref:`int<class_int>` **_surface_get_format**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_format>`

Phương thức ảo dùng để override định dạng surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_lods:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **_surface_get_lods**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_lods>`

Phương thức ảo dùng để override các LOD của surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_material:

.. rst-class:: classref-method

:ref:`Material<class_Material>` **_surface_get_material**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_material>`

Phương thức ảo dùng để override material của surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_get_primitive_type:

.. rst-class:: classref-method

:ref:`int<class_int>` **_surface_get_primitive_type**\ (\ index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_Mesh_private_method__surface_get_primitive_type>`

Phương thức ảo dùng để override loại primitive của surface cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_private_method__surface_set_material:

.. rst-class:: classref-method

|void| **_surface_set_material**\ (\ index\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ ) |virtual| |required| :ref:`🔗<class_Mesh_private_method__surface_set_material>`

Phương thức ảo dùng để override việc thiết lập ``material`` tại ``index`` đã cho cho một custom class mở rộng **Mesh**.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_create_convex_shape:

.. rst-class:: classref-method

:ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>` **create_convex_shape**\ (\ clean\: :ref:`bool<class_bool>` = true, simplify\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Mesh_method_create_convex_shape>`

Tính toán một :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>` từ mesh.

Nếu ``clean`` là ``true`` (mặc định), các đỉnh trùng lặp và nằm bên trong sẽ tự động bị loại bỏ. Bạn có thể đặt thành ``false`` để quá trình nhanh hơn nếu không cần loại bỏ.

Nếu ``simplify`` là ``true``, hình học có thể được đơn giản hóa thêm để giảm số lượng đỉnh. Theo mặc định, tính năng này bị tắt.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_create_outline:

.. rst-class:: classref-method

:ref:`Mesh<class_Mesh>` **create_outline**\ (\ margin\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Mesh_method_create_outline>`

Tính toán một mesh đường bao tại một offset (margin) được xác định từ mesh gốc.

\ **Lưu ý:** Phương thức này thường trả về các đỉnh theo thứ tự ngược lại (ví dụ: theo chiều kim đồng hồ thành ngược chiều kim đồng hồ).

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_create_placeholder:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **create_placeholder**\ (\ ) |const| :ref:`🔗<class_Mesh_method_create_placeholder>`

Tạo một phiên bản placeholder của resource này (:ref:`PlaceholderMesh<class_PlaceholderMesh>`).

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_create_trimesh_shape:

.. rst-class:: classref-method

:ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` **create_trimesh_shape**\ (\ ) |const| :ref:`🔗<class_Mesh_method_create_trimesh_shape>`

Tính toán một :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` từ mesh.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_generate_triangle_mesh:

.. rst-class:: classref-method

:ref:`TriangleMesh<class_TriangleMesh>` **generate_triangle_mesh**\ (\ ) |const| :ref:`🔗<class_Mesh_method_generate_triangle_mesh>`

Tạo một :ref:`TriangleMesh<class_TriangleMesh>` từ mesh. Chỉ xét các surface sử dụng một trong các loại primitive sau: :ref:`PRIMITIVE_TRIANGLES<class_Mesh_constant_PRIMITIVE_TRIANGLES>`, :ref:`PRIMITIVE_TRIANGLE_STRIP<class_Mesh_constant_PRIMITIVE_TRIANGLE_STRIP>`.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_get_aabb:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **get_aabb**\ (\ ) |const| :ref:`🔗<class_Mesh_method_get_aabb>`

Trả về :ref:`AABB<class_AABB>` nhỏ nhất bao quanh mesh này trong local space. Không bị ảnh hưởng bởi ``custom_aabb``.

\ **Lưu ý:** Tính năng này chỉ được triển khai cho :ref:`ArrayMesh<class_ArrayMesh>` và :ref:`PrimitiveMesh<class_PrimitiveMesh>`.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_get_faces:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_faces**\ (\ ) |const| :ref:`🔗<class_Mesh_method_get_faces>`

Trả về tất cả các đỉnh tạo nên các mặt của mesh. Mỗi ba đỉnh biểu diễn một tam giác.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_get_surface_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_surface_count**\ (\ ) |const| :ref:`🔗<class_Mesh_method_get_surface_count>`

Trả về số lượng surface mà **Mesh** chứa. Giá trị này tương đương với :ref:`MeshInstance3D.get_surface_override_material_count()<class_MeshInstance3D_method_get_surface_override_material_count>`.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_surface_get_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **surface_get_arrays**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Mesh_method_surface_get_arrays>`

Trả về các array của vertex, normal, UV, v.v. cấu thành surface được yêu cầu (xem :ref:`ArrayMesh.add_surface_from_arrays()<class_ArrayMesh_method_add_surface_from_arrays>`).

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_surface_get_blend_shape_arrays:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Array<class_Array>`\] **surface_get_blend_shape_arrays**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Mesh_method_surface_get_blend_shape_arrays>`

Trả về các array blend shape của surface được yêu cầu.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_surface_get_material:

.. rst-class:: classref-method

:ref:`Material<class_Material>` **surface_get_material**\ (\ surf_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Mesh_method_surface_get_material>`

Trả về một :ref:`Material<class_Material>` trong surface đã cho. Surface được render bằng material này.

\ **Lưu ý:** Lệnh này trả về material bên trong resource **Mesh**, không phải :ref:`Material<class_Material>` liên kết với các thuộc tính Surface Material Override của :ref:`MeshInstance3D<class_MeshInstance3D>`. Để lấy :ref:`Material<class_Material>` liên kết với các thuộc tính Surface Material Override của :ref:`MeshInstance3D<class_MeshInstance3D>`, hãy sử dụng :ref:`MeshInstance3D.get_surface_override_material()<class_MeshInstance3D_method_get_surface_override_material>`.

.. rst-class:: classref-item-separator

----

.. _class_Mesh_method_surface_set_material:

.. rst-class:: classref-method

|void| **surface_set_material**\ (\ surf_idx\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ ) :ref:`🔗<class_Mesh_method_surface_set_material>`

Thiết lập một :ref:`Material<class_Material>` cho surface đã cho. Surface sẽ được render bằng material này.

\ **Lưu ý:** Lệnh này gán material bên trong resource **Mesh**, không phải :ref:`Material<class_Material>` liên kết với các thuộc tính Surface Material Override của :ref:`MeshInstance3D<class_MeshInstance3D>`. Để thiết lập :ref:`Material<class_Material>` liên kết với các thuộc tính Surface Material Override của :ref:`MeshInstance3D<class_MeshInstance3D>`, hãy sử dụng :ref:`MeshInstance3D.set_surface_override_material()<class_MeshInstance3D_method_set_surface_override_material>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
