:github_url: hide

.. meta::
	:keywords: tilemap

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/gridmap/doc_classes/GridMap.xml.

.. _class_GridMap:

GridMap
=======

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node dành cho các map 3D dựa trên tile.

.. rst-class:: classref-introduction-group

Mô tả
-----

GridMap cho phép bạn tương tác đặt các mesh trên một grid. Nó hoạt động cả trong editor lẫn từ các script, giúp bạn tạo các level editor trong game.

GridMap sử dụng một :ref:`MeshLibrary<class_MeshLibrary>` chứa danh sách các tile. Mỗi tile là một mesh kèm các material, cùng với các shape collision và navigation tùy chọn.

Một GridMap chứa một tập hợp các cell. Mỗi cell trong grid tham chiếu đến một tile trong :ref:`MeshLibrary<class_MeshLibrary>`. Tất cả cell trong map đều có cùng kích thước.

Bên trong, một GridMap được chia thành một tập hợp octant thưa để render và xử lý physics hiệu quả. Mọi octant đều có cùng kích thước và có thể chứa nhiều cell.

\ **Lưu ý:** GridMap không kế thừa :ref:`VisualInstance3D<class_VisualInstance3D>` và do đó không thể bị ẩn hoặc áp dụng cull mask dựa trên :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>`. Nếu bạn đặt một light không tác động đến layer đầu tiên, toàn bộ GridMap sẽ không được light đó chiếu sáng.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng gridmap <../tutorials/3d/using_gridmaps>`

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `3D Kinematic Character Demo <https://godotengine.org/asset-library/asset/2739>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`bake_navigation<class_GridMap_property_bake_navigation>`                     | ``false``            |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`cell_center_x<class_GridMap_property_cell_center_x>`                         | ``true``             |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`cell_center_y<class_GridMap_property_cell_center_y>`                         | ``true``             |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`cell_center_z<class_GridMap_property_cell_center_z>`                         | ``true``             |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                        | :ref:`cell_octant_size<class_GridMap_property_cell_octant_size>`                   | ``8``                |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                    | :ref:`cell_scale<class_GridMap_property_cell_scale>`                               | ``1.0``              |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                                | :ref:`cell_size<class_GridMap_property_cell_size>`                                 | ``Vector3(2, 2, 2)`` |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                        | :ref:`collision_layer<class_GridMap_property_collision_layer>`                     | ``1``                |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                        | :ref:`collision_mask<class_GridMap_property_collision_mask>`                       | ``1``                |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                    | :ref:`collision_priority<class_GridMap_property_collision_priority>`               | ``1.0``              |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>` | :ref:`collision_visibility_mode<class_GridMap_property_collision_visibility_mode>` | ``0``                |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`MeshLibrary<class_MeshLibrary>`                        | :ref:`mesh_library<class_GridMap_property_mesh_library>`                           |                      |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+
   | :ref:`PhysicsMaterial<class_PhysicsMaterial>`                | :ref:`physics_material<class_GridMap_property_physics_material>`                   |                      |
   +--------------------------------------------------------------+------------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`clear<class_GridMap_method_clear>`\ (\ )                                                                                                                                              |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`clear_baked_meshes<class_GridMap_method_clear_baked_meshes>`\ (\ )                                                                                                                    |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                        | :ref:`get_bake_mesh_instance<class_GridMap_method_get_bake_mesh_instance>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                               |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                    | :ref:`get_bake_meshes<class_GridMap_method_get_bake_meshes>`\ (\ )                                                                                                                          |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`                                    | :ref:`get_basis_with_orthogonal_index<class_GridMap_method_get_basis_with_orthogonal_index>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                   |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`get_cell_item<class_GridMap_method_get_cell_item>`\ (\ position\: :ref:`Vector3i<class_Vector3i>`\ ) |const|                                                                          |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`                                    | :ref:`get_cell_item_basis<class_GridMap_method_get_cell_item_basis>`\ (\ position\: :ref:`Vector3i<class_Vector3i>`\ ) |const|                                                              |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`get_cell_item_orientation<class_GridMap_method_get_cell_item_orientation>`\ (\ position\: :ref:`Vector3i<class_Vector3i>`\ ) |const|                                                  |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`get_collision_layer_value<class_GridMap_method_get_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                        |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                      | :ref:`get_collision_mask_value<class_GridMap_method_get_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                          |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                    | :ref:`get_meshes<class_GridMap_method_get_meshes>`\ (\ ) |const|                                                                                                                            |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                        | :ref:`get_navigation_map<class_GridMap_method_get_navigation_map>`\ (\ ) |const|                                                                                                            |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3i<class_Vector3i>`                              | :ref:`get_octant_coords_from_cell_coords<class_GridMap_method_get_octant_coords_from_cell_coords>`\ (\ cell_coords\: :ref:`Vector3i<class_Vector3i>`\ ) |const|                             |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_octants_in_bounds<class_GridMap_method_get_octants_in_bounds>`\ (\ bounds\: :ref:`AABB<class_AABB>`\ ) |const|                                                                    |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                        | :ref:`get_orthogonal_index_from_basis<class_GridMap_method_get_orthogonal_index_from_basis>`\ (\ basis\: :ref:`Basis<class_Basis>`\ ) |const|                                               |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_cells<class_GridMap_method_get_used_cells>`\ (\ ) |const|                                                                                                                    |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_cells_by_item<class_GridMap_method_get_used_cells_by_item>`\ (\ item\: :ref:`int<class_int>`\ ) |const|                                                                      |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_cells_in_octant<class_GridMap_method_get_used_cells_in_octant>`\ (\ octant_coords\: :ref:`Vector3i<class_Vector3i>`\ ) |const|                                               |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_cells_in_octant_by_item<class_GridMap_method_get_used_cells_in_octant_by_item>`\ (\ octant_coords\: :ref:`Vector3i<class_Vector3i>`, item\: :ref:`int<class_int>`\ ) |const| |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_octants<class_GridMap_method_get_used_octants>`\ (\ ) |const|                                                                                                                |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_octants_by_item<class_GridMap_method_get_used_octants_by_item>`\ (\ item\: :ref:`int<class_int>`\ ) |const|                                                                  |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] | :ref:`get_used_octants_in_bounds<class_GridMap_method_get_used_octants_in_bounds>`\ (\ bounds\: :ref:`AABB<class_AABB>`\ ) |const|                                                          |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3i<class_Vector3i>`                              | :ref:`local_to_map<class_GridMap_method_local_to_map>`\ (\ local_position\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                        |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`make_baked_meshes<class_GridMap_method_make_baked_meshes>`\ (\ gen_lightmap_uv\: :ref:`bool<class_bool>` = false, lightmap_uv_texel_size\: :ref:`float<class_float>` = 0.1\ )         |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                | :ref:`map_to_local<class_GridMap_method_map_to_local>`\ (\ map_position\: :ref:`Vector3i<class_Vector3i>`\ ) |const|                                                                        |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`resource_changed<class_GridMap_method_resource_changed>`\ (\ resource\: :ref:`Resource<class_Resource>`\ )                                                                            |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_cell_item<class_GridMap_method_set_cell_item>`\ (\ position\: :ref:`Vector3i<class_Vector3i>`, item\: :ref:`int<class_int>`, orientation\: :ref:`int<class_int>` = 0\ )           |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_collision_layer_value<class_GridMap_method_set_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                               |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_collision_mask_value<class_GridMap_method_set_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                                 |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                       | :ref:`set_navigation_map<class_GridMap_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                                                            |
   +--------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_GridMap_signal_cell_size_changed:

.. rst-class:: classref-signal

**cell_size_changed**\ (\ cell_size\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_GridMap_signal_cell_size_changed>`

Được phát ra khi :ref:`cell_size<class_GridMap_property_cell_size>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_signal_changed:

.. rst-class:: classref-signal

**changed**\ (\ ) :ref:`🔗<class_GridMap_signal_changed>`

Được phát ra khi :ref:`MeshLibrary<class_MeshLibrary>` của GridMap này thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_GridMap_DebugVisibilityMode:

.. rst-class:: classref-enumeration

enum **DebugVisibilityMode**: :ref:`🔗<enum_GridMap_DebugVisibilityMode>`

.. _class_GridMap_constant_DEBUG_VISIBILITY_MODE_DEFAULT:

.. rst-class:: classref-enumeration-constant

:ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>` **DEBUG_VISIBILITY_MODE_DEFAULT** = ``0``

Ẩn các shape debug collision trong editor và sử dụng các thiết lập debug để xác định khả năng hiển thị của chúng trong game (tức là :ref:`SceneTree.debug_collisions_hint<class_SceneTree_property_debug_collisions_hint>` hoặc :ref:`SceneTree.debug_navigation_hint<class_SceneTree_property_debug_navigation_hint>`).

.. _class_GridMap_constant_DEBUG_VISIBILITY_MODE_FORCE_SHOW:

.. rst-class:: classref-enumeration-constant

:ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>` **DEBUG_VISIBILITY_MODE_FORCE_SHOW** = ``1``

Luôn hiển thị các shape debug collision.

.. _class_GridMap_constant_DEBUG_VISIBILITY_MODE_FORCE_HIDE:

.. rst-class:: classref-enumeration-constant

:ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>` **DEBUG_VISIBILITY_MODE_FORCE_HIDE** = ``2``

Luôn ẩn các shape debug collision.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_GridMap_constant_INVALID_CELL_ITEM:

.. rst-class:: classref-constant

**INVALID_CELL_ITEM** = ``-1`` :ref:`🔗<class_GridMap_constant_INVALID_CELL_ITEM>`

Cell item không hợp lệ, có thể được sử dụng trong :ref:`set_cell_item()<class_GridMap_method_set_cell_item>` để xóa các cell (hoặc biểu diễn một cell trống trong :ref:`get_cell_item()<class_GridMap_method_get_cell_item>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GridMap_property_bake_navigation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **bake_navigation** = ``false`` :ref:`🔗<class_GridMap_property_bake_navigation>`

.. rst-class:: classref-property-setget

- |void| **set_bake_navigation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_baking_navigation**\ (\ )

Nếu ``true``, GridMap này sẽ tạo một navigation region cho mỗi cell sử dụng item :ref:`mesh_library<class_GridMap_property_mesh_library>` có navigation mesh. Navigation region được tạo sẽ sử dụng bitmask navigation layer được gán cho item của :ref:`MeshLibrary<class_MeshLibrary>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_cell_center_x:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cell_center_x** = ``true`` :ref:`🔗<class_GridMap_property_cell_center_x>`

.. rst-class:: classref-property-setget

- |void| **set_center_x**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_center_x**\ (\ )

Nếu ``true``, các grid item được căn giữa trên trục X.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_cell_center_y:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cell_center_y** = ``true`` :ref:`🔗<class_GridMap_property_cell_center_y>`

.. rst-class:: classref-property-setget

- |void| **set_center_y**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_center_y**\ (\ )

Nếu ``true``, các grid item được căn giữa trên trục Y.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_cell_center_z:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **cell_center_z** = ``true`` :ref:`🔗<class_GridMap_property_cell_center_z>`

.. rst-class:: classref-property-setget

- |void| **set_center_z**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_center_z**\ (\ )

Nếu ``true``, các grid item được căn giữa trên trục Z.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_cell_octant_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **cell_octant_size** = ``8`` :ref:`🔗<class_GridMap_property_cell_octant_size>`

.. rst-class:: classref-property-setget

- |void| **set_octant_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_octant_size**\ (\ )

Kích thước của mỗi octant, được đo bằng số lượng cell. Thuộc tính này áp dụng cho cả ba trục.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_cell_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **cell_scale** = ``1.0`` :ref:`🔗<class_GridMap_property_cell_scale>`

.. rst-class:: classref-property-setget

- |void| **set_cell_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cell_scale**\ (\ )

Scale của các cell item.

Thuộc tính này không ảnh hưởng đến kích thước của chính các grid cell, mà chỉ ảnh hưởng đến các item bên trong chúng. Có thể sử dụng thuộc tính này để khiến các cell item chồng lấn lên các cell lân cận.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_cell_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **cell_size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_GridMap_property_cell_size>`

.. rst-class:: classref-property-setget

- |void| **set_cell_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_cell_size**\ (\ )

Kích thước của các cell trong grid.

Thuộc tính này không ảnh hưởng đến kích thước của các mesh. Xem :ref:`cell_scale<class_GridMap_property_cell_scale>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_collision_layer:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_layer** = ``1`` :ref:`🔗<class_GridMap_property_collision_layer>`

.. rst-class:: classref-property-setget

- |void| **set_collision_layer**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_layer**\ (\ )

Các physics layer mà GridMap này thuộc về.

GridMap hoạt động như các static body, nghĩa là chúng không bị tác động bởi gravity hoặc các lực khác. Chúng chỉ tác động đến các physics body khác va chạm với chúng.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``1`` :ref:`🔗<class_GridMap_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà GridMap này phát hiện va chạm. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_collision_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_priority** = ``1.0`` :ref:`🔗<class_GridMap_property_collision_priority>`

.. rst-class:: classref-property-setget

- |void| **set_collision_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_priority**\ (\ )

Mức độ ưu tiên được sử dụng để xử lý va chạm khi xảy ra hiện tượng xuyên lấn. Mức độ ưu tiên càng cao thì độ xuyên vào object càng thấp. Ví dụ, thuộc tính này có thể được dùng để ngăn player phá vỡ ranh giới của một level.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_collision_visibility_mode:

.. rst-class:: classref-property

:ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>` **collision_visibility_mode** = ``0`` :ref:`🔗<class_GridMap_property_collision_visibility_mode>`

.. rst-class:: classref-property-setget

- |void| **set_collision_visibility_mode**\ (\ value\: :ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>`\ ) - :ref:`DebugVisibilityMode<enum_GridMap_DebugVisibilityMode>` **get_collision_visibility_mode**\ (\ )

Hiển thị hoặc ẩn các collision shape của **GridMap**. Nếu được đặt thành :ref:`DEBUG_VISIBILITY_MODE_DEFAULT<class_GridMap_constant_DEBUG_VISIBILITY_MODE_DEFAULT>`, việc này phụ thuộc vào các thiết lập debug hiển thị collision.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_mesh_library:

.. rst-class:: classref-property

:ref:`MeshLibrary<class_MeshLibrary>` **mesh_library** :ref:`🔗<class_GridMap_property_mesh_library>`

.. rst-class:: classref-property-setget

- |void| **set_mesh_library**\ (\ value\: :ref:`MeshLibrary<class_MeshLibrary>`\ ) - :ref:`MeshLibrary<class_MeshLibrary>` **get_mesh_library**\ (\ )

:ref:`MeshLibrary<class_MeshLibrary>` được gán.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_property_physics_material:

.. rst-class:: classref-property

:ref:`PhysicsMaterial<class_PhysicsMaterial>` **physics_material** :ref:`🔗<class_GridMap_property_physics_material>`

.. rst-class:: classref-property-setget

- |void| **set_physics_material**\ (\ value\: :ref:`PhysicsMaterial<class_PhysicsMaterial>`\ ) - :ref:`PhysicsMaterial<class_PhysicsMaterial>` **get_physics_material**\ (\ )

Ghi đè các thuộc tính physics friction và bounce mặc định cho toàn bộ **GridMap**.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GridMap_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_GridMap_method_clear>`

Xóa tất cả cell.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_clear_baked_meshes:

.. rst-class:: classref-method

|void| **clear_baked_meshes**\ (\ ) :ref:`🔗<class_GridMap_method_clear_baked_meshes>`

Xóa tất cả mesh đã bake. Xem :ref:`make_baked_meshes()<class_GridMap_method_make_baked_meshes>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_bake_mesh_instance:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_bake_mesh_instance**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_GridMap_method_get_bake_mesh_instance>`

Trả về :ref:`RID<class_RID>` của một mesh đã bake với ``idx`` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_bake_meshes:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_bake_meshes**\ (\ ) :ref:`🔗<class_GridMap_method_get_bake_meshes>`

Trả về một mảng gồm các :ref:`ArrayMesh<class_ArrayMesh>`\ es và các reference :ref:`Transform3D<class_Transform3D>` của tất cả mesh bake hiện có trong GridMap hiện tại. Các index chẵn chứa các :ref:`ArrayMesh<class_ArrayMesh>`\ es, trong khi các index lẻ chứa các :ref:`Transform3D<class_Transform3D>`\ s luôn bằng :ref:`Transform3D.IDENTITY<class_Transform3D_constant_IDENTITY>`.

Phương thức này dựa trên kết quả đầu ra của :ref:`make_baked_meshes()<class_GridMap_method_make_baked_meshes>`, phương thức này sẽ được gọi với ``gen_lightmap_uv`` được đặt thành ``true`` và ``lightmap_uv_texel_size`` được đặt thành ``0.1`` nếu chưa được gọi trước đó.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_basis_with_orthogonal_index:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **get_basis_with_orthogonal_index**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GridMap_method_get_basis_with_orthogonal_index>`

Trả về một trong 24 rotation khả dĩ nằm dọc theo các vector (x,y,z), trong đó mỗi component có thể là -1, 0 hoặc 1. Để biết thêm chi tiết, hãy tham khảo mã nguồn Godot.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_cell_item:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_cell_item**\ (\ position\: :ref:`Vector3i<class_Vector3i>`\ ) |const| :ref:`🔗<class_GridMap_method_get_cell_item>`

Index của item :ref:`MeshLibrary<class_MeshLibrary>` nằm tại tọa độ grid đã cho. Nếu cell trống, :ref:`INVALID_CELL_ITEM<class_GridMap_constant_INVALID_CELL_ITEM>` sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_cell_item_basis:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **get_cell_item_basis**\ (\ position\: :ref:`Vector3i<class_Vector3i>`\ ) |const| :ref:`🔗<class_GridMap_method_get_cell_item_basis>`

Trả về basis xác định hướng của ô được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_cell_item_orientation:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_cell_item_orientation**\ (\ position\: :ref:`Vector3i<class_Vector3i>`\ ) |const| :ref:`🔗<class_GridMap_method_get_cell_item_orientation>`

Hướng của ô tại tọa độ lưới đã cho. Trả về ``-1`` nếu ô trống.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_collision_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GridMap_method_get_collision_layer_value>`

Trả về cho biết layer được chỉ định của :ref:`collision_layer<class_GridMap_property_collision_layer>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GridMap_method_get_collision_mask_value>`

Trả về cho biết layer được chỉ định của :ref:`collision_mask<class_GridMap_property_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_meshes:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_meshes**\ (\ ) |const| :ref:`🔗<class_GridMap_method_get_meshes>`

Trả về một mảng các tham chiếu :ref:`Transform3D<class_Transform3D>` và :ref:`Mesh<class_Mesh>` tương ứng với những ô không trống trong lưới. Các phép biến đổi được chỉ định trong local space. Các chỉ số chẵn chứa :ref:`Transform3D<class_Transform3D>`\ s, còn các chỉ số lẻ chứa :ref:`Mesh<class_Mesh>`\ es liên quan đến :ref:`Transform3D<class_Transform3D>` ở chỉ số liền trước.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_GridMap_method_get_navigation_map>`

Trả về :ref:`RID<class_RID>` của navigation map mà node GridMap này sử dụng cho các navigation mesh đã bake của ô.

Hàm này luôn trả về map được thiết lập trên node GridMap, không phải map trên NavigationServer. Nếu map được thay đổi trực tiếp bằng API NavigationServer, node GridMap sẽ không nhận biết được thay đổi của map.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_octant_coords_from_cell_coords:

.. rst-class:: classref-method

:ref:`Vector3i<class_Vector3i>` **get_octant_coords_from_cell_coords**\ (\ cell_coords\: :ref:`Vector3i<class_Vector3i>`\ ) |const| :ref:`🔗<class_GridMap_method_get_octant_coords_from_cell_coords>`

Trả về tọa độ octant :ref:`Vector3i<class_Vector3i>` của octant mà ô tại ``cell_coords`` thuộc về.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_octants_in_bounds:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_octants_in_bounds**\ (\ bounds\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_GridMap_method_get_octants_in_bounds>`

Trả về một mảng các tọa độ octant :ref:`Vector3i<class_Vector3i>` nằm trong ``bounds`` đã cho, bao gồm cả những octant không có ô nào đang được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_orthogonal_index_from_basis:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_orthogonal_index_from_basis**\ (\ basis\: :ref:`Basis<class_Basis>`\ ) |const| :ref:`🔗<class_GridMap_method_get_orthogonal_index_from_basis>`

Hàm này xem xét việc rời rạc hóa các phép quay thành 24 điểm trên hình cầu đơn vị, nằm dọc theo các vector (x,y,z), trong đó mỗi thành phần là -1, 0 hoặc 1, rồi trả về chỉ mục (trong khoảng từ 0 đến 23) của điểm biểu diễn chính xác nhất hướng của đối tượng. Để biết thêm chi tiết, hãy tham khảo mã nguồn Godot.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_cells:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_cells**\ (\ ) |const| :ref:`🔗<class_GridMap_method_get_used_cells>`

Trả về một mảng :ref:`Vector3<class_Vector3>` chứa tọa độ các ô không trống trong grid map.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_cells_by_item:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_cells_by_item**\ (\ item\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GridMap_method_get_used_cells_by_item>`

Trả về một mảng gồm tất cả các ô có chỉ mục item đã cho được chỉ định trong ``item``.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_cells_in_octant:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_cells_in_octant**\ (\ octant_coords\: :ref:`Vector3i<class_Vector3i>`\ ) |const| :ref:`🔗<class_GridMap_method_get_used_cells_in_octant>`

Trả về một mảng các :ref:`Vector3i<class_Vector3i>`\ s chứa tọa độ của những ô không trống bên trong octant tại ``octant_coords``.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_cells_in_octant_by_item:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_cells_in_octant_by_item**\ (\ octant_coords\: :ref:`Vector3i<class_Vector3i>`, item\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GridMap_method_get_used_cells_in_octant_by_item>`

Trả về một mảng các :ref:`Vector3i<class_Vector3i>`\ s chứa tọa độ của những ô bên trong octant tại ``octant_coords`` sử dụng ``item`` ô được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_octants:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_octants**\ (\ ) |const| :ref:`🔗<class_GridMap_method_get_used_octants>`

Trả về một mảng các :ref:`Vector3i<class_Vector3i>`\ s chứa tọa độ octant của những octant không trống trong grid map.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_octants_by_item:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_octants_by_item**\ (\ item\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GridMap_method_get_used_octants_by_item>`

Trả về một mảng các :ref:`Vector3i<class_Vector3i>`\ s chứa tọa độ octant của những octant sử dụng ``item`` đã chỉ định trong grid map.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_get_used_octants_in_bounds:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3i<class_Vector3i>`\] **get_used_octants_in_bounds**\ (\ bounds\: :ref:`AABB<class_AABB>`\ ) |const| :ref:`🔗<class_GridMap_method_get_used_octants_in_bounds>`

Trả về một mảng các :ref:`Vector3i<class_Vector3i>`\ s chứa tọa độ octant của những octant không trống nằm trong ``bounds`` cục bộ.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_local_to_map:

.. rst-class:: classref-method

:ref:`Vector3i<class_Vector3i>` **local_to_map**\ (\ local_position\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_GridMap_method_local_to_map>`

Trả về tọa độ map của ô chứa ``local_position`` đã cho. Nếu ``local_position`` ở tọa độ global, hãy cân nhắc sử dụng :ref:`Node3D.to_local()<class_Node3D_method_to_local>` trước khi truyền nó cho method này. Xem thêm :ref:`map_to_local()<class_GridMap_method_map_to_local>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_make_baked_meshes:

.. rst-class:: classref-method

|void| **make_baked_meshes**\ (\ gen_lightmap_uv\: :ref:`bool<class_bool>` = false, lightmap_uv_texel_size\: :ref:`float<class_float>` = 0.1\ ) :ref:`🔗<class_GridMap_method_make_baked_meshes>`

Tạo một mesh đã bake biểu diễn tất cả mesh trong :ref:`MeshLibrary<class_MeshLibrary>` được chỉ định để sử dụng với :ref:`LightmapGI<class_LightmapGI>`. Nếu ``gen_lightmap_uv`` là ``true``, dữ liệu UV2 sẽ được tạo cho mỗi mesh hiện đang được sử dụng trong **GridMap**. Nếu không, chỉ những mesh đã có dữ liệu UV2 mới có thể sử dụng baked lightmap. Khi tạo UV2, ``lightmap_uv_texel_size`` kiểm soát mật độ texel cho lightmap; các giá trị thấp hơn tạo ra lightmap chi tiết hơn. ``lightmap_uv_texel_size`` bị bỏ qua nếu ``gen_lightmap_uv`` là ``false``. Xem thêm :ref:`get_bake_meshes()<class_GridMap_method_get_bake_meshes>`, vốn phụ thuộc vào đầu ra của method này.

\ **Lưu ý:** Việc gọi method này thực tế sẽ không bake lightmap, vì quá trình bake lightmap được thực hiện bằng node :ref:`LightmapGI<class_LightmapGI>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_map_to_local:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **map_to_local**\ (\ map_position\: :ref:`Vector3i<class_Vector3i>`\ ) |const| :ref:`🔗<class_GridMap_method_map_to_local>`

Trả về vị trí của một ô lưới trong local coordinate space của GridMap. Để chuyển giá trị trả về thành tọa độ global, hãy sử dụng :ref:`Node3D.to_global()<class_Node3D_method_to_global>`. Xem thêm :ref:`local_to_map()<class_GridMap_method_local_to_map>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_resource_changed:

.. rst-class:: classref-method

|void| **resource_changed**\ (\ resource\: :ref:`Resource<class_Resource>`\ ) :ref:`🔗<class_GridMap_method_resource_changed>`

**Không còn được khuyến nghị:** Thay vào đó, hãy sử dụng :ref:`Resource.changed<class_Resource_signal_changed>`.

Method này không thực hiện thao tác nào.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_set_cell_item:

.. rst-class:: classref-method

|void| **set_cell_item**\ (\ position\: :ref:`Vector3i<class_Vector3i>`, item\: :ref:`int<class_int>`, orientation\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_GridMap_method_set_cell_item>`

Thiết lập chỉ mục mesh cho ô được tham chiếu bằng tọa độ lưới của ô đó.

Chỉ mục item âm, chẳng hạn như :ref:`INVALID_CELL_ITEM<class_GridMap_constant_INVALID_CELL_ITEM>`, sẽ xóa ô.

Có thể truyền thêm hướng của item. Để biết các giá trị hướng hợp lệ, hãy xem :ref:`get_orthogonal_index_from_basis()<class_GridMap_method_get_orthogonal_index_from_basis>`.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_set_collision_layer_value:

.. rst-class:: classref-method

|void| **set_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_GridMap_method_set_collision_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_layer<class_GridMap_property_collision_layer>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_set_collision_mask_value:

.. rst-class:: classref-method

|void| **set_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_GridMap_method_set_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_mask<class_GridMap_property_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_GridMap_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_GridMap_method_set_navigation_map>`

Thiết lập :ref:`RID<class_RID>` của navigation map mà node GridMap này sẽ sử dụng cho các navigation mesh đã bake của ô.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
