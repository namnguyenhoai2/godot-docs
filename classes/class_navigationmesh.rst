:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationMesh.xml.

.. _class_NavigationMesh:

NavigationMesh
==============

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một navigation mesh xác định các khu vực có thể đi qua và các chướng ngại vật.

.. rst-class:: classref-introduction-group

Mô tả
-----

Navigation mesh là một tập hợp các polygon xác định những khu vực nào trong môi trường có thể đi qua, giúp các agent tìm đường qua những không gian phức tạp.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationMesh <../tutorials/navigation/navigation_using_navigationmeshes>`

- `3D Navigation Demo <https://godotengine.org/asset-library/asset/2743>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`agent_height<class_NavigationMesh_property_agent_height>`                                         | ``1.5``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`agent_max_climb<class_NavigationMesh_property_agent_max_climb>`                                   | ``0.25``                            |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`agent_max_slope<class_NavigationMesh_property_agent_max_slope>`                                   | ``45.0``                            |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`agent_radius<class_NavigationMesh_property_agent_radius>`                                         | ``0.5``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`border_size<class_NavigationMesh_property_border_size>`                                           | ``0.0``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`cell_height<class_NavigationMesh_property_cell_height>`                                           | ``0.25``                            |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`cell_size<class_NavigationMesh_property_cell_size>`                                               | ``0.25``                            |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`detail_sample_distance<class_NavigationMesh_property_detail_sample_distance>`                     | ``6.0``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`detail_sample_max_error<class_NavigationMesh_property_detail_sample_max_error>`                   | ``1.0``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`edge_max_error<class_NavigationMesh_property_edge_max_error>`                                     | ``1.3``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`edge_max_length<class_NavigationMesh_property_edge_max_length>`                                   | ``0.0``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`AABB<class_AABB>`                                             | :ref:`filter_baking_aabb<class_NavigationMesh_property_filter_baking_aabb>`                             | ``AABB(0, 0, 0, 0, 0, 0)``          |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                       | :ref:`filter_baking_aabb_offset<class_NavigationMesh_property_filter_baking_aabb_offset>`               | ``Vector3(0, 0, 0)``                |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`filter_ledge_spans<class_NavigationMesh_property_filter_ledge_spans>`                             | ``false``                           |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`filter_low_hanging_obstacles<class_NavigationMesh_property_filter_low_hanging_obstacles>`         | ``false``                           |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`filter_walkable_low_height_spans<class_NavigationMesh_property_filter_walkable_low_height_spans>` | ``false``                           |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`int<class_int>`                                               | :ref:`geometry_collision_mask<class_NavigationMesh_property_geometry_collision_mask>`                   | ``4294967295``                      |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>`   | :ref:`geometry_parsed_geometry_type<class_NavigationMesh_property_geometry_parsed_geometry_type>`       | ``2``                               |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>`   | :ref:`geometry_source_geometry_mode<class_NavigationMesh_property_geometry_source_geometry_mode>`       | ``0``                               |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`StringName<class_StringName>`                                 | :ref:`geometry_source_group_name<class_NavigationMesh_property_geometry_source_group_name>`             | ``&"navigation_mesh_source_group"`` |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`region_merge_size<class_NavigationMesh_property_region_merge_size>`                               | ``20.0``                            |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`region_min_size<class_NavigationMesh_property_region_min_size>`                                   | ``2.0``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` | :ref:`sample_partition_type<class_NavigationMesh_property_sample_partition_type>`                       | ``0``                               |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+
   | :ref:`float<class_float>`                                           | :ref:`vertices_per_polygon<class_NavigationMesh_property_vertices_per_polygon>`                         | ``6.0``                             |
   +---------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------+-------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_polygon<class_NavigationMesh_method_add_polygon>`\ (\ polygon\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )                                       |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_NavigationMesh_method_clear>`\ (\ )                                                                                                              |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_polygons<class_NavigationMesh_method_clear_polygons>`\ (\ )                                                                                            |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`create_from_mesh<class_NavigationMesh_method_create_from_mesh>`\ (\ mesh\: :ref:`Mesh<class_Mesh>`\ )                                                        |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`get_collision_mask_value<class_NavigationMesh_method_get_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`get_polygon<class_NavigationMesh_method_get_polygon>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                     |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_polygon_count<class_NavigationMesh_method_get_polygon_count>`\ (\ ) |const|                                                                              |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_vertices<class_NavigationMesh_method_get_vertices>`\ (\ ) |const|                                                                                        |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_collision_mask_value<class_NavigationMesh_method_set_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_vertices<class_NavigationMesh_method_set_vertices>`\ (\ vertices\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ )                                |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các phép liệt kê
----------------

.. _enum_NavigationMesh_SamplePartitionType:

.. rst-class:: classref-enumeration

enum **SamplePartitionType**: :ref:`🔗<enum_NavigationMesh_SamplePartitionType>`

.. _class_NavigationMesh_constant_SAMPLE_PARTITION_WATERSHED:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` **SAMPLE_PARTITION_WATERSHED** = ``0``

Phân vùng Watershed. Thường là lựa chọn tốt nhất nếu bạn tiền tính navigation mesh; hãy sử dụng tùy chọn này khi có các khu vực mở rộng lớn.

.. _class_NavigationMesh_constant_SAMPLE_PARTITION_MONOTONE:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` **SAMPLE_PARTITION_MONOTONE** = ``1``

Phân vùng Monotone. Sử dụng tùy chọn này nếu bạn muốn tạo navigation mesh nhanh.

.. _class_NavigationMesh_constant_SAMPLE_PARTITION_LAYERS:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` **SAMPLE_PARTITION_LAYERS** = ``2``

Phân vùng theo Layer. Là lựa chọn tốt cho navigation mesh dạng tile với các tile có kích thước vừa và nhỏ.

.. _class_NavigationMesh_constant_SAMPLE_PARTITION_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` **SAMPLE_PARTITION_MAX** = ``3``

Biểu thị kích thước của enum :ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>`.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationMesh_ParsedGeometryType:

.. rst-class:: classref-enumeration

enum **ParsedGeometryType**: :ref:`🔗<enum_NavigationMesh_ParsedGeometryType>`

.. _class_NavigationMesh_constant_PARSED_GEOMETRY_MESH_INSTANCES:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>` **PARSED_GEOMETRY_MESH_INSTANCES** = ``0``

Phân tích các mesh instance dưới dạng geometry. Bao gồm các node :ref:`MeshInstance3D<class_MeshInstance3D>`, :ref:`CSGShape3D<class_CSGShape3D>` và :ref:`GridMap<class_GridMap>`.

.. _class_NavigationMesh_constant_PARSED_GEOMETRY_STATIC_COLLIDERS:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>` **PARSED_GEOMETRY_STATIC_COLLIDERS** = ``1``

Phân tích các collider :ref:`StaticBody3D<class_StaticBody3D>` dưới dạng geometry. Collider phải nằm trong một trong các layer được chỉ định bởi :ref:`geometry_collision_mask<class_NavigationMesh_property_geometry_collision_mask>`.

.. _class_NavigationMesh_constant_PARSED_GEOMETRY_BOTH:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>` **PARSED_GEOMETRY_BOTH** = ``2``

Cả :ref:`PARSED_GEOMETRY_MESH_INSTANCES<class_NavigationMesh_constant_PARSED_GEOMETRY_MESH_INSTANCES>` và :ref:`PARSED_GEOMETRY_STATIC_COLLIDERS<class_NavigationMesh_constant_PARSED_GEOMETRY_STATIC_COLLIDERS>`.

.. _class_NavigationMesh_constant_PARSED_GEOMETRY_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>` **PARSED_GEOMETRY_MAX** = ``3``

Biểu thị kích thước của enum :ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>`.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationMesh_SourceGeometryMode:

.. rst-class:: classref-enumeration

enum **SourceGeometryMode**: :ref:`🔗<enum_NavigationMesh_SourceGeometryMode>`

.. _class_NavigationMesh_constant_SOURCE_GEOMETRY_ROOT_NODE_CHILDREN:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>` **SOURCE_GEOMETRY_ROOT_NODE_CHILDREN** = ``0``

Quét đệ quy các node con của node gốc để tìm geometry.

.. _class_NavigationMesh_constant_SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>` **SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN** = ``1``

Quét các node trong một group và các node con của chúng theo cách đệ quy để tìm geometry. Group được chỉ định bởi :ref:`geometry_source_group_name<class_NavigationMesh_property_geometry_source_group_name>`.

.. _class_NavigationMesh_constant_SOURCE_GEOMETRY_GROUPS_EXPLICIT:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>` **SOURCE_GEOMETRY_GROUPS_EXPLICIT** = ``2``

Sử dụng các node trong một group làm geometry. Group được chỉ định bởi :ref:`geometry_source_group_name<class_NavigationMesh_property_geometry_source_group_name>`.

.. _class_NavigationMesh_constant_SOURCE_GEOMETRY_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>` **SOURCE_GEOMETRY_MAX** = ``3``

Biểu thị kích thước của enum :ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationMesh_property_agent_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **agent_height** = ``1.5`` :ref:`🔗<class_NavigationMesh_property_agent_height>`

.. rst-class:: classref-property-setget

- |void| **set_agent_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_agent_height**\ (\ )

Chiều cao sàn đến trần tối thiểu mà tại đó khu vực sàn vẫn được xem là có thể đi bộ.

\ **Lưu ý:** Trong khi baking, giá trị này sẽ được làm tròn lên bội số gần nhất của :ref:`cell_height<class_NavigationMesh_property_cell_height>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_agent_max_climb:

.. rst-class:: classref-property

:ref:`float<class_float>` **agent_max_climb** = ``0.25`` :ref:`🔗<class_NavigationMesh_property_agent_max_climb>`

.. rst-class:: classref-property-setget

- |void| **set_agent_max_climb**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_agent_max_climb**\ (\ )

Độ cao gờ tối thiểu được xem là vẫn có thể đi qua.

\ **Lưu ý:** Trong khi baking, giá trị này sẽ được làm tròn xuống bội số gần nhất của :ref:`cell_height<class_NavigationMesh_property_cell_height>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_agent_max_slope:

.. rst-class:: classref-property

:ref:`float<class_float>` **agent_max_slope** = ``45.0`` :ref:`🔗<class_NavigationMesh_property_agent_max_slope>`

.. rst-class:: classref-property-setget

- |void| **set_agent_max_slope**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_agent_max_slope**\ (\ )

Độ dốc tối đa được xem là có thể đi bộ, tính bằng độ.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_agent_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **agent_radius** = ``0.5`` :ref:`🔗<class_NavigationMesh_property_agent_radius>`

.. rst-class:: classref-property-setget

- |void| **set_agent_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_agent_radius**\ (\ )

Khoảng cách dùng để bào mòn/thu nhỏ khu vực có thể đi bộ của heightfield tính từ các vật cản.

\ **Lưu ý:** Trong khi baking, giá trị này sẽ được làm tròn lên bội số gần nhất của :ref:`cell_size<class_NavigationMesh_property_cell_size>`.

\ **Lưu ý:** Bán kính phải bằng hoặc lớn hơn ``0.0``. Nếu bán kính là ``0.0``, sẽ không thể sửa các phần giao nhau không hợp lệ của outline và các lỗi về độ chính xác khác trong quá trình baking. Do đó, một số chướng ngại vật có thể bị loại không chính xác khỏi navigation mesh cuối cùng hoặc có thể xóa các polygon của navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_border_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **border_size** = ``0.0`` :ref:`🔗<class_NavigationMesh_property_border_size>`

.. rst-class:: classref-property-setget

- |void| **set_border_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_border_size**\ (\ )

Kích thước của đường viền không thể điều hướng xung quanh khu vực bounding dùng để bake.

Kết hợp với :ref:`filter_baking_aabb<class_NavigationMesh_property_filter_baking_aabb>` và giá trị :ref:`edge_max_error<class_NavigationMesh_property_edge_max_error>` bằng ``1.0`` hoặc thấp hơn, kích thước đường viền có thể được dùng để bake navigation mesh căn theo tile mà không làm các cạnh tile bị thu nhỏ bởi :ref:`agent_radius<class_NavigationMesh_property_agent_radius>`.

\ **Lưu ý:** Nếu giá trị này không phải là ``0.0``, nó sẽ được làm tròn lên bội số gần nhất của :ref:`cell_size<class_NavigationMesh_property_cell_size>` trong quá trình baking.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_cell_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **cell_height** = ``0.25`` :ref:`🔗<class_NavigationMesh_property_cell_height>`

.. rst-class:: classref-property-setget

- |void| **set_cell_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cell_height**\ (\ )

Chiều cao cell được dùng để rasterize các đỉnh của navigation mesh trên trục Y. Phải khớp với chiều cao cell trên navigation map.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_cell_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **cell_size** = ``0.25`` :ref:`🔗<class_NavigationMesh_property_cell_size>`

.. rst-class:: classref-property-setget

- |void| **set_cell_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cell_size**\ (\ )

Kích thước cell được dùng để rasterize các đỉnh của navigation mesh trên mặt phẳng XZ. Phải khớp với kích thước cell trên navigation map.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_detail_sample_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **detail_sample_distance** = ``6.0`` :ref:`🔗<class_NavigationMesh_property_detail_sample_distance>`

.. rst-class:: classref-property-setget

- |void| **set_detail_sample_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_detail_sample_distance**\ (\ )

Khoảng cách lấy mẫu được sử dụng khi tạo detail mesh, tính theo đơn vị cell.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_detail_sample_max_error:

.. rst-class:: classref-property

:ref:`float<class_float>` **detail_sample_max_error** = ``1.0`` :ref:`🔗<class_NavigationMesh_property_detail_sample_max_error>`

.. rst-class:: classref-property-setget

- |void| **set_detail_sample_max_error**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_detail_sample_max_error**\ (\ )

Khoảng cách tối đa mà bề mặt detail mesh được phép lệch so với heightfield, tính theo đơn vị cell.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_edge_max_error:

.. rst-class:: classref-property

:ref:`float<class_float>` **edge_max_error** = ``1.3`` :ref:`🔗<class_NavigationMesh_property_edge_max_error>`

.. rst-class:: classref-property-setget

- |void| **set_edge_max_error**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_edge_max_error**\ (\ )

Khoảng cách tối đa mà các cạnh biên của contour đã được đơn giản hóa được phép lệch so với contour thô ban đầu.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_edge_max_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **edge_max_length** = ``0.0`` :ref:`🔗<class_NavigationMesh_property_edge_max_length>`

.. rst-class:: classref-property-setget

- |void| **set_edge_max_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_edge_max_length**\ (\ )

Độ dài tối đa cho phép của các cạnh contour dọc theo đường biên của mesh. Giá trị ``0.0`` sẽ tắt tính năng này.

\ **Lưu ý:** Trong khi baking, giá trị này sẽ được làm tròn lên bội số gần nhất của :ref:`cell_size<class_NavigationMesh_property_cell_size>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_filter_baking_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **filter_baking_aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_NavigationMesh_property_filter_baking_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_filter_baking_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_filter_baking_aabb**\ (\ )

Nếu baking :ref:`AABB<class_AABB>` có volume, quá trình baking navigation mesh sẽ bị giới hạn trong khu vực bao quanh nó.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_filter_baking_aabb_offset:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **filter_baking_aabb_offset** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_NavigationMesh_property_filter_baking_aabb_offset>`

.. rst-class:: classref-property-setget

- |void| **set_filter_baking_aabb_offset**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_filter_baking_aabb_offset**\ (\ )

Offset vị trí được áp dụng cho :ref:`filter_baking_aabb<class_NavigationMesh_property_filter_baking_aabb>` :ref:`AABB<class_AABB>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_filter_ledge_spans:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **filter_ledge_spans** = ``false`` :ref:`🔗<class_NavigationMesh_property_filter_ledge_spans>`

.. rst-class:: classref-property-setget

- |void| **set_filter_ledge_spans**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_filter_ledge_spans**\ (\ )

Nếu là ``true``, đánh dấu các span là gờ và không thể đi bộ.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_filter_low_hanging_obstacles:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **filter_low_hanging_obstacles** = ``false`` :ref:`🔗<class_NavigationMesh_property_filter_low_hanging_obstacles>`

.. rst-class:: classref-property-setget

- |void| **set_filter_low_hanging_obstacles**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_filter_low_hanging_obstacles**\ (\ )

Nếu ``true``, đánh dấu các đoạn không thể đi lại là có thể đi lại nếu giá trị tối đa của chúng nằm trong phạm vi :ref:`agent_max_climb<class_NavigationMesh_property_agent_max_climb>` so với một vùng lân cận có thể đi lại.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_filter_walkable_low_height_spans:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **filter_walkable_low_height_spans** = ``false`` :ref:`🔗<class_NavigationMesh_property_filter_walkable_low_height_spans>`

.. rst-class:: classref-property-setget

- |void| **set_filter_walkable_low_height_spans**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_filter_walkable_low_height_spans**\ (\ )

Nếu ``true``, đánh dấu các đoạn có thể đi lại là không thể đi lại nếu khoảng thông thoáng phía trên đoạn đó nhỏ hơn :ref:`agent_height<class_NavigationMesh_property_agent_height>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_geometry_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **geometry_collision_mask** = ``4294967295`` :ref:`🔗<class_NavigationMesh_property_geometry_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer cần quét để tìm static collider.

Chỉ được sử dụng khi :ref:`geometry_parsed_geometry_type<class_NavigationMesh_property_geometry_parsed_geometry_type>` là :ref:`PARSED_GEOMETRY_STATIC_COLLIDERS<class_NavigationMesh_constant_PARSED_GEOMETRY_STATIC_COLLIDERS>` hoặc :ref:`PARSED_GEOMETRY_BOTH<class_NavigationMesh_constant_PARSED_GEOMETRY_BOTH>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_geometry_parsed_geometry_type:

.. rst-class:: classref-property

:ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>` **geometry_parsed_geometry_type** = ``2`` :ref:`🔗<class_NavigationMesh_property_geometry_parsed_geometry_type>`

.. rst-class:: classref-property-setget

- |void| **set_parsed_geometry_type**\ (\ value\: :ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>`\ ) - :ref:`ParsedGeometryType<enum_NavigationMesh_ParsedGeometryType>` **get_parsed_geometry_type**\ (\ )

Xác định loại node nào sẽ được phân tích dưới dạng geometry.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_geometry_source_geometry_mode:

.. rst-class:: classref-property

:ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>` **geometry_source_geometry_mode** = ``0`` :ref:`🔗<class_NavigationMesh_property_geometry_source_geometry_mode>`

.. rst-class:: classref-property-setget

- |void| **set_source_geometry_mode**\ (\ value\: :ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>`\ ) - :ref:`SourceGeometryMode<enum_NavigationMesh_SourceGeometryMode>` **get_source_geometry_mode**\ (\ )

Nguồn geometry được sử dụng khi baking.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_geometry_source_group_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **geometry_source_group_name** = ``&"navigation_mesh_source_group"`` :ref:`🔗<class_NavigationMesh_property_geometry_source_group_name>`

.. rst-class:: classref-property-setget

- |void| **set_source_group_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_source_group_name**\ (\ )

Tên của group cần quét để tìm geometry.

Chỉ được sử dụng khi :ref:`geometry_source_geometry_mode<class_NavigationMesh_property_geometry_source_geometry_mode>` là :ref:`SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN<class_NavigationMesh_constant_SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN>` hoặc :ref:`SOURCE_GEOMETRY_GROUPS_EXPLICIT<class_NavigationMesh_constant_SOURCE_GEOMETRY_GROUPS_EXPLICIT>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_region_merge_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **region_merge_size** = ``20.0`` :ref:`🔗<class_NavigationMesh_property_region_merge_size>`

.. rst-class:: classref-property-setget

- |void| **set_region_merge_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_region_merge_size**\ (\ )

Mọi region có kích thước nhỏ hơn giá trị này sẽ được gộp với các region lớn hơn nếu có thể.

\ **Lưu ý:** Giá trị này sẽ được bình phương để tính số lượng cell. Ví dụ, giá trị 20 sẽ đặt số lượng cell là 400.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_region_min_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **region_min_size** = ``2.0`` :ref:`🔗<class_NavigationMesh_property_region_min_size>`

.. rst-class:: classref-property-setget

- |void| **set_region_min_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_region_min_size**\ (\ )

Kích thước tối thiểu của một region để region đó được tạo.

\ **Lưu ý:** Giá trị này sẽ được bình phương để tính số lượng cell tối thiểu được phép dùng để tạo các khu vực đảo biệt lập. Ví dụ, giá trị 8 sẽ đặt số lượng cell là 64.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_sample_partition_type:

.. rst-class:: classref-property

:ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` **sample_partition_type** = ``0`` :ref:`🔗<class_NavigationMesh_property_sample_partition_type>`

.. rst-class:: classref-property-setget

- |void| **set_sample_partition_type**\ (\ value\: :ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>`\ ) - :ref:`SamplePartitionType<enum_NavigationMesh_SamplePartitionType>` **get_sample_partition_type**\ (\ )

Thuật toán partition để tạo các polygon của navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_property_vertices_per_polygon:

.. rst-class:: classref-property

:ref:`float<class_float>` **vertices_per_polygon** = ``6.0`` :ref:`🔗<class_NavigationMesh_property_vertices_per_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_vertices_per_polygon**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_vertices_per_polygon**\ (\ )

Số lượng vertex tối đa được phép cho các polygon được tạo trong quá trình chuyển đổi contour thành polygon.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_NavigationMesh_method_add_polygon:

.. rst-class:: classref-method

|void| **add_polygon**\ (\ polygon\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_NavigationMesh_method_add_polygon>`

Thêm một polygon bằng cách sử dụng các index của các vertex nhận được khi gọi :ref:`get_vertices()<class_NavigationMesh_method_get_vertices>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_NavigationMesh_method_clear>`

Xóa các array nội bộ chứa vertex và index của polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_clear_polygons:

.. rst-class:: classref-method

|void| **clear_polygons**\ (\ ) :ref:`🔗<class_NavigationMesh_method_clear_polygons>`

Xóa array các polygon, nhưng không xóa array các vertex.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_create_from_mesh:

.. rst-class:: classref-method

|void| **create_from_mesh**\ (\ mesh\: :ref:`Mesh<class_Mesh>`\ ) :ref:`🔗<class_NavigationMesh_method_create_from_mesh>`

Khởi tạo navigation mesh bằng cách thiết lập các vertex và index theo một :ref:`Mesh<class_Mesh>`.

\ **Lưu ý:** ``mesh`` được cung cấp phải có kiểu :ref:`Mesh.PRIMITIVE_TRIANGLES<class_Mesh_constant_PRIMITIVE_TRIANGLES>` và có một index array.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_get_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationMesh_method_get_collision_mask_value>`

Trả về việc layer được chỉ định của :ref:`geometry_collision_mask<class_NavigationMesh_property_geometry_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_get_polygon:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_polygon**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_NavigationMesh_method_get_polygon>`

Trả về một :ref:`PackedInt32Array<class_PackedInt32Array>` chứa các index của các vertex thuộc một polygon đã tạo.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_get_polygon_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_polygon_count**\ (\ ) |const| :ref:`🔗<class_NavigationMesh_method_get_polygon_count>`

Trả về số lượng polygon trong navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_get_vertices:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_vertices**\ (\ ) |const| :ref:`🔗<class_NavigationMesh_method_get_vertices>`

Trả về một :ref:`PackedVector3Array<class_PackedVector3Array>` chứa tất cả các vertex đang được sử dụng để tạo polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_set_collision_mask_value:

.. rst-class:: classref-method

|void| **set_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationMesh_method_set_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`geometry_collision_mask<class_NavigationMesh_property_geometry_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationMesh_method_set_vertices:

.. rst-class:: classref-method

|void| **set_vertices**\ (\ vertices\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) :ref:`🔗<class_NavigationMesh_method_set_vertices>`

Thiết lập các vertex, sau đó có thể index để tạo polygon bằng method :ref:`add_polygon()<class_NavigationMesh_method_add_polygon>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
