:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MeshInstance3D.xml.

.. _class_MeshInstance3D:

MeshInstance3D
==============

**Kế thừa:** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`SoftBody3D<class_SoftBody3D>`

Node tạo các instance của mesh trong một scenario.

.. rst-class:: classref-introduction-group

Mô tả
-----

MeshInstance3D là một node nhận một resource :ref:`Mesh<class_Mesh>` và thêm nó vào scenario hiện tại bằng cách tạo một instance của resource đó. Đây là class thường được dùng nhất để render hình học 3D và có thể tạo instance của một :ref:`Mesh<class_Mesh>` duy nhất ở nhiều vị trí. Điều này cho phép tái sử dụng hình học, giúp tiết kiệm tài nguyên. Khi một :ref:`Mesh<class_Mesh>` cần được tạo instance hơn hàng nghìn lần ở khoảng cách gần nhau, hãy cân nhắc sử dụng :ref:`MultiMesh<class_MultiMesh>` trong một :ref:`MultiMeshInstance3D<class_MultiMeshInstance3D>` thay thế.

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

   +---------------------------------+---------------------------------------------------------+------------------+
   | :ref:`Mesh<class_Mesh>`         | :ref:`mesh<class_MeshInstance3D_property_mesh>`         |                  |
   +---------------------------------+---------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`skeleton<class_MeshInstance3D_property_skeleton>` | ``NodePath("")`` |
   +---------------------------------+---------------------------------------------------------+------------------+
   | :ref:`Skin<class_Skin>`         | :ref:`skin<class_MeshInstance3D_property_skin>`         |                  |
   +---------------------------------+---------------------------------------------------------+------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ArrayMesh<class_ArrayMesh>`         | :ref:`bake_mesh_from_current_blend_shape_mix<class_MeshInstance3D_method_bake_mesh_from_current_blend_shape_mix>`\ (\ existing\: :ref:`ArrayMesh<class_ArrayMesh>` = null\ )                                   |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ArrayMesh<class_ArrayMesh>`         | :ref:`bake_mesh_from_current_skeleton_pose<class_MeshInstance3D_method_bake_mesh_from_current_skeleton_pose>`\ (\ existing\: :ref:`ArrayMesh<class_ArrayMesh>` = null\ )                                       |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`create_convex_collision<class_MeshInstance3D_method_create_convex_collision>`\ (\ clean\: :ref:`bool<class_bool>` = true, simplify\: :ref:`bool<class_bool>` = false\ )                                  |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`create_debug_tangents<class_MeshInstance3D_method_create_debug_tangents>`\ (\ )                                                                                                                          |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`create_multiple_convex_collisions<class_MeshInstance3D_method_create_multiple_convex_collisions>`\ (\ settings\: :ref:`MeshConvexDecompositionSettings<class_MeshConvexDecompositionSettings>` = null\ ) |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`create_trimesh_collision<class_MeshInstance3D_method_create_trimesh_collision>`\ (\ )                                                                                                                    |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                     | :ref:`find_blend_shape_by_name<class_MeshInstance3D_method_find_blend_shape_by_name>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                        |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Material<class_Material>`           | :ref:`get_active_material<class_MeshInstance3D_method_get_active_material>`\ (\ surface\: :ref:`int<class_int>`\ ) |const|                                                                                     |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                     | :ref:`get_blend_shape_count<class_MeshInstance3D_method_get_blend_shape_count>`\ (\ ) |const|                                                                                                                  |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                 | :ref:`get_blend_shape_value<class_MeshInstance3D_method_get_blend_shape_value>`\ (\ blend_shape_idx\: :ref:`int<class_int>`\ ) |const|                                                                         |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SkinReference<class_SkinReference>` | :ref:`get_skin_reference<class_MeshInstance3D_method_get_skin_reference>`\ (\ ) |const|                                                                                                                        |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Material<class_Material>`           | :ref:`get_surface_override_material<class_MeshInstance3D_method_get_surface_override_material>`\ (\ surface\: :ref:`int<class_int>`\ ) |const|                                                                 |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                     | :ref:`get_surface_override_material_count<class_MeshInstance3D_method_get_surface_override_material_count>`\ (\ ) |const|                                                                                      |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`set_blend_shape_value<class_MeshInstance3D_method_set_blend_shape_value>`\ (\ blend_shape_idx\: :ref:`int<class_int>`, value\: :ref:`float<class_float>`\ )                                              |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`set_surface_override_material<class_MeshInstance3D_method_set_surface_override_material>`\ (\ surface\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ )                             |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MeshInstance3D_property_mesh:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **mesh** :ref:`🔗<class_MeshInstance3D_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_mesh**\ (\ )

Resource :ref:`Mesh<class_Mesh>` của instance.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_property_skeleton:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **skeleton** = ``NodePath("")`` :ref:`🔗<class_MeshInstance3D_property_skeleton>`

.. rst-class:: classref-property-setget

- |void| **set_skeleton_path**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_skeleton_path**\ (\ )

:ref:`NodePath<class_NodePath>` đến :ref:`Skeleton3D<class_Skeleton3D>` được liên kết với instance.

\ **Lưu ý:** Giá trị mặc định của thuộc tính này đã thay đổi trong Godot 4.6. Bật :ref:`ProjectSettings.animation/compatibility/default_parent_skeleton_in_mesh_instance_3d<class_ProjectSettings_property_animation/compatibility/default_parent_skeleton_in_mesh_instance_3d>` nếu cần hành vi cũ để đảm bảo khả năng tương thích.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_property_skin:

.. rst-class:: classref-property

:ref:`Skin<class_Skin>` **skin** :ref:`🔗<class_MeshInstance3D_property_skin>`

.. rst-class:: classref-property-setget

- |void| **set_skin**\ (\ value\: :ref:`Skin<class_Skin>`\ ) - :ref:`Skin<class_Skin>` **get_skin**\ (\ )

:ref:`Skin<class_Skin>` sẽ được instance này sử dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MeshInstance3D_method_bake_mesh_from_current_blend_shape_mix:

.. rst-class:: classref-method

:ref:`ArrayMesh<class_ArrayMesh>` **bake_mesh_from_current_blend_shape_mix**\ (\ existing\: :ref:`ArrayMesh<class_ArrayMesh>` = null\ ) :ref:`🔗<class_MeshInstance3D_method_bake_mesh_from_current_blend_shape_mix>`

Chụp ảnh nhanh :ref:`ArrayMesh<class_ArrayMesh>` hiện tại với tất cả blend shape được áp dụng theo các trọng số hiện tại, rồi bake vào mesh ``existing`` được cung cấp. Nếu không cung cấp mesh ``existing``, một :ref:`ArrayMesh<class_ArrayMesh>` mới sẽ được tạo, bake và trả về. Vật liệu của các surface mesh không được sao chép.

\ **Hiệu năng:** Dữ liệu :ref:`Mesh<class_Mesh>` cần được nhận từ GPU, khiến :ref:`RenderingServer<class_RenderingServer>` bị đình trệ trong quá trình này.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_bake_mesh_from_current_skeleton_pose:

.. rst-class:: classref-method

:ref:`ArrayMesh<class_ArrayMesh>` **bake_mesh_from_current_skeleton_pose**\ (\ existing\: :ref:`ArrayMesh<class_ArrayMesh>` = null\ ) :ref:`🔗<class_MeshInstance3D_method_bake_mesh_from_current_skeleton_pose>`

Chụp ảnh nhanh pose skeleton đang được animate của skinned mesh hiện tại và bake vào mesh ``existing`` được cung cấp. Nếu không cung cấp mesh ``existing``, một :ref:`ArrayMesh<class_ArrayMesh>` mới sẽ được tạo, bake và trả về. Cần có skeleton đã đăng ký skin để hoạt động. Blendshape bị bỏ qua. Vật liệu của các surface mesh không được sao chép.

\ **Hiệu năng:** Dữ liệu :ref:`Mesh<class_Mesh>` cần được lấy từ GPU, khiến :ref:`RenderingServer<class_RenderingServer>` bị đình trệ trong quá trình này.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_create_convex_collision:

.. rst-class:: classref-method

|void| **create_convex_collision**\ (\ clean\: :ref:`bool<class_bool>` = true, simplify\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_MeshInstance3D_method_create_convex_collision>`

Helper này tạo một node con :ref:`StaticBody3D<class_StaticBody3D>` với collision shape :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>` được tính toán từ hình học của mesh. Nó chủ yếu được dùng để kiểm thử.

Nếu ``clean`` là ``true`` (mặc định), các vertex trùng lặp và nằm bên trong sẽ được tự động loại bỏ. Bạn có thể đặt thành ``false`` để quá trình nhanh hơn nếu không cần bước này.

Nếu ``simplify`` là ``true``, hình học có thể được đơn giản hóa thêm để giảm số lượng vertex. Mặc định bị tắt.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_create_debug_tangents:

.. rst-class:: classref-method

|void| **create_debug_tangents**\ (\ ) :ref:`🔗<class_MeshInstance3D_method_create_debug_tangents>`

Helper này tạo một node con **MeshInstance3D** với gizmo tại mỗi vertex được tính toán từ hình học của mesh. Nó chủ yếu được dùng để kiểm thử.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_create_multiple_convex_collisions:

.. rst-class:: classref-method

|void| **create_multiple_convex_collisions**\ (\ settings\: :ref:`MeshConvexDecompositionSettings<class_MeshConvexDecompositionSettings>` = null\ ) :ref:`🔗<class_MeshInstance3D_method_create_multiple_convex_collisions>`

Helper này tạo một node con :ref:`StaticBody3D<class_StaticBody3D>` với nhiều collision shape :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>` được tính toán từ hình học của mesh thông qua phân rã lồi. Có thể điều khiển thao tác phân rã lồi bằng các tham số từ ``settings`` tùy chọn.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_create_trimesh_collision:

.. rst-class:: classref-method

|void| **create_trimesh_collision**\ (\ ) :ref:`🔗<class_MeshInstance3D_method_create_trimesh_collision>`

Helper này tạo một node con :ref:`StaticBody3D<class_StaticBody3D>` với collision shape :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` được tính toán từ hình học của mesh. Nó chủ yếu được dùng để kiểm thử.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_find_blend_shape_by_name:

.. rst-class:: classref-method

:ref:`int<class_int>` **find_blend_shape_by_name**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_MeshInstance3D_method_find_blend_shape_by_name>`

Trả về chỉ mục của blend shape có ``name`` đã cho. Trả về ``-1`` nếu không tồn tại blend shape nào có tên này, kể cả khi :ref:`mesh<class_MeshInstance3D_property_mesh>` là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_get_active_material:

.. rst-class:: classref-method

:ref:`Material<class_Material>` **get_active_material**\ (\ surface\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MeshInstance3D_method_get_active_material>`

Trả về :ref:`Material<class_Material>` sẽ được :ref:`Mesh<class_Mesh>` sử dụng khi vẽ. Kết quả có thể là :ref:`GeometryInstance3D.material_override<class_GeometryInstance3D_property_material_override>`, :ref:`Material<class_Material>` ghi đè surface được định nghĩa trong **MeshInstance3D** này, hoặc :ref:`Material<class_Material>` surface được định nghĩa trong :ref:`mesh<class_MeshInstance3D_property_mesh>`. Ví dụ, nếu sử dụng :ref:`GeometryInstance3D.material_override<class_GeometryInstance3D_property_material_override>`, tất cả surface sẽ trả về material ghi đè.

Trả về ``null`` nếu không có material nào đang hoạt động, kể cả khi :ref:`mesh<class_MeshInstance3D_property_mesh>` là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_get_blend_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_blend_shape_count**\ (\ ) |const| :ref:`🔗<class_MeshInstance3D_method_get_blend_shape_count>`

Trả về số lượng blend shape hiện có. Phát sinh lỗi nếu :ref:`mesh<class_MeshInstance3D_property_mesh>` là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_get_blend_shape_value:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_blend_shape_value**\ (\ blend_shape_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MeshInstance3D_method_get_blend_shape_value>`

Trả về giá trị của blend shape tại ``blend_shape_idx`` đã cho. Trả về ``0.0`` và phát sinh lỗi nếu :ref:`mesh<class_MeshInstance3D_property_mesh>` là ``null`` hoặc không có blend shape tại chỉ mục đó.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_get_skin_reference:

.. rst-class:: classref-method

:ref:`SkinReference<class_SkinReference>` **get_skin_reference**\ (\ ) |const| :ref:`🔗<class_MeshInstance3D_method_get_skin_reference>`

Trả về :ref:`SkinReference<class_SkinReference>` nội bộ chứa :ref:`RID<class_RID>` của skeleton được gắn vào RID này. Xem thêm :ref:`Resource.get_rid()<class_Resource_method_get_rid>`, :ref:`SkinReference.get_skeleton()<class_SkinReference_method_get_skeleton>` và :ref:`RenderingServer.instance_attach_skeleton()<class_RenderingServer_method_instance_attach_skeleton>`.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_get_surface_override_material:

.. rst-class:: classref-method

:ref:`Material<class_Material>` **get_surface_override_material**\ (\ surface\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MeshInstance3D_method_get_surface_override_material>`

Trả về :ref:`Material<class_Material>` ghi đè cho ``surface`` được chỉ định của resource :ref:`Mesh<class_Mesh>`. Xem thêm :ref:`get_surface_override_material_count()<class_MeshInstance3D_method_get_surface_override_material_count>`.

\ **Lưu ý:** Hàm này trả về :ref:`Material<class_Material>` được liên kết với các thuộc tính Surface Material Override của **MeshInstance3D**, không phải material bên trong resource :ref:`Mesh<class_Mesh>`. Để lấy material bên trong resource :ref:`Mesh<class_Mesh>`, hãy sử dụng :ref:`Mesh.surface_get_material()<class_Mesh_method_surface_get_material>`.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_get_surface_override_material_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_surface_override_material_count**\ (\ ) |const| :ref:`🔗<class_MeshInstance3D_method_get_surface_override_material_count>`

Trả về số lượng material ghi đè surface. Giá trị này tương đương với :ref:`Mesh.get_surface_count()<class_Mesh_method_get_surface_count>`. Xem thêm :ref:`get_surface_override_material()<class_MeshInstance3D_method_get_surface_override_material>`.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_set_blend_shape_value:

.. rst-class:: classref-method

|void| **set_blend_shape_value**\ (\ blend_shape_idx\: :ref:`int<class_int>`, value\: :ref:`float<class_float>`\ ) :ref:`🔗<class_MeshInstance3D_method_set_blend_shape_value>`

Đặt giá trị của blend shape tại ``blend_shape_idx`` thành ``value``. Phát sinh lỗi nếu :ref:`mesh<class_MeshInstance3D_property_mesh>` là ``null`` hoặc không có blend shape tại chỉ mục đó.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance3D_method_set_surface_override_material:

.. rst-class:: classref-method

|void| **set_surface_override_material**\ (\ surface\: :ref:`int<class_int>`, material\: :ref:`Material<class_Material>`\ ) :ref:`🔗<class_MeshInstance3D_method_set_surface_override_material>`

Đặt ``material`` ghi đè cho ``surface`` được chỉ định của resource :ref:`Mesh<class_Mesh>`. Material này được liên kết với **MeshInstance3D** này thay vì với :ref:`mesh<class_MeshInstance3D_property_mesh>`.

\ **Lưu ý:** Hàm này gán :ref:`Material<class_Material>` được liên kết với các thuộc tính Surface Material Override của **MeshInstance3D**, không phải material bên trong resource :ref:`Mesh<class_Mesh>`. Để đặt material bên trong resource :ref:`Mesh<class_Mesh>`, hãy sử dụng :ref:`Mesh.surface_set_material()<class_Mesh_method_surface_set_material>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
