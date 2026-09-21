:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationMeshSourceGeometryData3D.xml.

.. _class_NavigationMeshSourceGeometryData3D:

NavigationMeshSourceGeometryData3D
==================================

**Thử nghiệm:** Class này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Container chứa dữ liệu hình học nguồn đã được phân tích cú pháp, dùng trong quá trình baking navigation mesh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Container chứa dữ liệu hình học nguồn đã được phân tích cú pháp, dùng trong quá trình baking navigation mesh.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_faces<class_NavigationMeshSourceGeometryData3D_method_add_faces>`\ (\ faces\: :ref:`PackedVector3Array<class_PackedVector3Array>`, xform\: :ref:`Transform3D<class_Transform3D>`\ )                                                                                                 |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_mesh<class_NavigationMeshSourceGeometryData3D_method_add_mesh>`\ (\ mesh\: :ref:`Mesh<class_Mesh>`, xform\: :ref:`Transform3D<class_Transform3D>`\ )                                                                                                                                |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_mesh_array<class_NavigationMeshSourceGeometryData3D_method_add_mesh_array>`\ (\ mesh_array\: :ref:`Array<class_Array>`, xform\: :ref:`Transform3D<class_Transform3D>`\ )                                                                                                            |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_projected_obstruction<class_NavigationMeshSourceGeometryData3D_method_add_projected_obstruction>`\ (\ vertices\: :ref:`PackedVector3Array<class_PackedVector3Array>`, elevation\: :ref:`float<class_float>`, height\: :ref:`float<class_float>`, carve\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`append_arrays<class_NavigationMeshSourceGeometryData3D_method_append_arrays>`\ (\ vertices\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`, indices\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )                                                                          |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_NavigationMeshSourceGeometryData3D_method_clear>`\ (\ )                                                                                                                                                                                                                     |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_projected_obstructions<class_NavigationMeshSourceGeometryData3D_method_clear_projected_obstructions>`\ (\ )                                                                                                                                                                       |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`                             | :ref:`get_bounds<class_NavigationMeshSourceGeometryData3D_method_get_bounds>`\ (\ )                                                                                                                                                                                                           |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`get_indices<class_NavigationMeshSourceGeometryData3D_method_get_indices>`\ (\ ) |const|                                                                                                                                                                                                 |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                           | :ref:`get_projected_obstructions<class_NavigationMeshSourceGeometryData3D_method_get_projected_obstructions>`\ (\ ) |const|                                                                                                                                                                   |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`get_vertices<class_NavigationMeshSourceGeometryData3D_method_get_vertices>`\ (\ ) |const|                                                                                                                                                                                               |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`has_data<class_NavigationMeshSourceGeometryData3D_method_has_data>`\ (\ )                                                                                                                                                                                                               |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`merge<class_NavigationMeshSourceGeometryData3D_method_merge>`\ (\ other_geometry\: :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`\ )                                                                                                               |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_indices<class_NavigationMeshSourceGeometryData3D_method_set_indices>`\ (\ indices\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )                                                                                                                                              |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_projected_obstructions<class_NavigationMeshSourceGeometryData3D_method_set_projected_obstructions>`\ (\ projected_obstructions\: :ref:`Array<class_Array>`\ )                                                                                                                       |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_vertices<class_NavigationMeshSourceGeometryData3D_method_set_vertices>`\ (\ vertices\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ )                                                                                                                                       |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationMeshSourceGeometryData3D_method_add_faces:

.. rst-class:: classref-method

|void| **add_faces**\ (\ faces\: :ref:`PackedVector3Array<class_PackedVector3Array>`, xform\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_add_faces>`

Thêm một mảng các vị trí đỉnh vào dữ liệu hình học để baking navigation mesh, tạo thành các mặt tam giác. Với mỗi mặt, mảng phải có ba vị trí đỉnh theo thứ tự winding clockwise. Vì các resource :ref:`NavigationMesh<class_NavigationMesh>` không có transform, tất cả vị trí đỉnh cần được offset theo transform của node bằng ``xform``.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_add_mesh:

.. rst-class:: classref-method

|void| **add_mesh**\ (\ mesh\: :ref:`Mesh<class_Mesh>`, xform\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_add_mesh>`

Thêm dữ liệu hình học của một resource :ref:`Mesh<class_Mesh>` vào dữ liệu baking navigation mesh. Mesh phải có dữ liệu mesh tam giác hợp lệ để được xem xét. Vì các resource :ref:`NavigationMesh<class_NavigationMesh>` không có transform, tất cả vị trí đỉnh cần được offset theo transform của node bằng ``xform``.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_add_mesh_array:

.. rst-class:: classref-method

|void| **add_mesh_array**\ (\ mesh_array\: :ref:`Array<class_Array>`, xform\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_add_mesh_array>`

Thêm một :ref:`Array<class_Array>` có kích thước :ref:`Mesh.ARRAY_MAX<class_Mesh_constant_ARRAY_MAX>`, với các đỉnh tại index :ref:`Mesh.ARRAY_VERTEX<class_Mesh_constant_ARRAY_VERTEX>` và các index tại index :ref:`Mesh.ARRAY_INDEX<class_Mesh_constant_ARRAY_INDEX>`, vào dữ liệu baking navigation mesh. Mảng phải có dữ liệu mesh tam giác hợp lệ để được xem xét. Vì các resource :ref:`NavigationMesh<class_NavigationMesh>` không có transform, tất cả vị trí đỉnh cần được offset theo transform của node bằng ``xform``.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_add_projected_obstruction:

.. rst-class:: classref-method

|void| **add_projected_obstruction**\ (\ vertices\: :ref:`PackedVector3Array<class_PackedVector3Array>`, elevation\: :ref:`float<class_float>`, height\: :ref:`float<class_float>`, carve\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_add_projected_obstruction>`

Thêm một hình dạng vật cản được chiếu vào hình học nguồn. Các ``vertices`` được xem là được chiếu lên một mặt phẳng trục xz, đặt tại ``elevation`` của trục y toàn cục và kéo dài theo ``height``. Nếu ``carve`` là ``true``, hình dạng đã carve sẽ không bị ảnh hưởng bởi các offset bổ sung (ví dụ: bán kính agent) trong quá trình baking navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_append_arrays:

.. rst-class:: classref-method

|void| **append_arrays**\ (\ vertices\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`, indices\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_append_arrays>`

Nối các mảng ``vertices`` và ``indices`` vào cuối các mảng hiện có. Thêm index hiện có làm offset cho các index được nối thêm.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_clear>`

Xóa dữ liệu nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_clear_projected_obstructions:

.. rst-class:: classref-method

|void| **clear_projected_obstructions**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_clear_projected_obstructions>`

Xóa tất cả các vật cản được chiếu.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_get_bounds:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **get_bounds**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_get_bounds>`

Trả về một bounding box căn chỉnh theo trục, bao phủ toàn bộ dữ liệu hình học được lưu trữ. Các giới hạn được tính khi gọi phương thức này và kết quả được cache cho đến khi có thay đổi hình học tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_get_indices:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_indices**\ (\ ) |const| :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_get_indices>`

Trả về mảng indices của dữ liệu hình học nguồn đã được phân tích cú pháp.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_get_projected_obstructions:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_projected_obstructions**\ (\ ) |const| :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_get_projected_obstructions>`

Trả về các vật cản được chiếu dưới dạng một :ref:`Array<class_Array>` gồm các dictionary. Mỗi :ref:`Dictionary<class_Dictionary>` chứa các mục sau:

- ``vertices`` - Một :ref:`PackedFloat32Array<class_PackedFloat32Array>` xác định các điểm tạo đường bao của hình dạng được chiếu.

- ``elevation`` - Một :ref:`float<class_float>` xác định vị trí của hình dạng được chiếu trên trục y.

- ``height`` - Một :ref:`float<class_float>` xác định mức độ kéo dài của hình dạng được chiếu dọc theo trục y.

- ``carve`` - Một :ref:`bool<class_bool>` xác định cách vật cản ảnh hưởng đến quá trình baking navigation mesh. Nếu ``true``, hình dạng được chiếu sẽ không bị ảnh hưởng bởi các offset bổ sung, ví dụ như bán kính agent.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_get_vertices:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_vertices**\ (\ ) |const| :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_get_vertices>`

Trả về mảng vertices của dữ liệu hình học nguồn đã được phân tích cú pháp.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_has_data:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_data**\ (\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_has_data>`

Trả về ``true`` khi dữ liệu hình học nguồn đã được phân tích cú pháp tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_merge:

.. rst-class:: classref-method

|void| **merge**\ (\ other_geometry\: :ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_merge>`

Thêm dữ liệu hình học của một **NavigationMeshSourceGeometryData3D** khác vào dữ liệu baking navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_set_indices:

.. rst-class:: classref-method

|void| **set_indices**\ (\ indices\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_set_indices>`

Thiết lập indices của dữ liệu hình học nguồn đã được phân tích cú pháp. Các indices cần tương ứng với các vertices phù hợp.

\ **Cảnh báo:** Dữ liệu không phù hợp có thể làm tiến trình baking của các thư viện bên thứ ba liên quan bị crash.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_set_projected_obstructions:

.. rst-class:: classref-method

|void| **set_projected_obstructions**\ (\ projected_obstructions\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_set_projected_obstructions>`

Thiết lập các vật cản được chiếu bằng một Array các Dictionary với các cặp key-value sau:


.. tabs::

 .. code-tab:: gdscript

    "vertices" : PackedFloat32Array
    "elevation" : float
    "height" : float
    "carve" : bool



.. rst-class:: classref-item-separator

----

.. _class_NavigationMeshSourceGeometryData3D_method_set_vertices:

.. rst-class:: classref-method

|void| **set_vertices**\ (\ vertices\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_NavigationMeshSourceGeometryData3D_method_set_vertices>`

Thiết lập các vertices của dữ liệu hình học nguồn đã được phân tích cú pháp. Các vertices cần tương ứng với các indices phù hợp.

\ **Cảnh báo:** Dữ liệu không phù hợp có thể làm tiến trình baking của các thư viện bên thứ ba liên quan bị crash.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
