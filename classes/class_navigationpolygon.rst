:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationPolygon.xml.

.. _class_NavigationPolygon:

NavigationPolygon
=================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một navigation mesh 2D mô tả bề mặt có thể đi qua để pathfinding.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một navigation mesh có thể được tạo bằng cách bake với sự trợ giúp của :ref:`NavigationServer2D<class_NavigationServer2D>`, hoặc bằng cách thêm thủ công các mảng chỉ mục vertex và polygon lồi.

Để bake một navigation mesh, cần thêm ít nhất một outline xác định ranh giới bên ngoài của khu vực được bake.


.. tabs::

 .. code-tab:: gdscript

    var new_navigation_mesh = NavigationPolygon.new()
    var bounding_outline = PackedVector2Array([Vector2(0, 0), Vector2(0, 50), Vector2(50, 50), Vector2(50, 0)])
    new_navigation_mesh.add_outline(bounding_outline)
    NavigationServer2D.bake_from_source_geometry_data(new_navigation_mesh, NavigationMeshSourceGeometryData2D.new());
    $NavigationRegion2D.navigation_polygon = new_navigation_mesh

 .. code-tab:: csharp

    var newNavigationMesh = new NavigationPolygon();
    Vector2[] boundingOutline = [new Vector2(0, 0), new Vector2(0, 50), new Vector2(50, 50), new Vector2(50, 0)];
    newNavigationMesh.AddOutline(boundingOutline);
    NavigationServer2D.BakeFromSourceGeometryData(newNavigationMesh, new NavigationMeshSourceGeometryData2D());
    GetNode<NavigationRegion2D>("NavigationRegion2D").NavigationPolygon = newNavigationMesh;



Thêm thủ công các vertex và chỉ mục polygon.


.. tabs::

 .. code-tab:: gdscript

    var new_navigation_mesh = NavigationPolygon.new()
    var new_vertices = PackedVector2Array([Vector2(0, 0), Vector2(0, 50), Vector2(50, 50), Vector2(50, 0)])
    new_navigation_mesh.vertices = new_vertices
    var new_polygon_indices = PackedInt32Array([0, 1, 2, 3])
    new_navigation_mesh.add_polygon(new_polygon_indices)
    $NavigationRegion2D.navigation_polygon = new_navigation_mesh

 .. code-tab:: csharp

    var newNavigationMesh = new NavigationPolygon();
    Vector2[] newVertices = [new Vector2(0, 0), new Vector2(0, 50), new Vector2(50, 50), new Vector2(50, 0)];
    newNavigationMesh.Vertices = newVertices;
    int[] newPolygonIndices = [0, 1, 2, 3];
    newNavigationMesh.AddPolygon(newPolygonIndices);
    GetNode<NavigationRegion2D>("NavigationRegion2D").NavigationPolygon = newNavigationMesh;



.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng NavigationMeshes <../tutorials/navigation/navigation_using_navigationmeshes>`

- `Navigation Polygon 2D Demo <https://godotengine.org/asset-library/asset/2722>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`float<class_float>`                                              | :ref:`agent_radius<class_NavigationPolygon_property_agent_radius>`                             | ``10.0``                                        |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`Rect2<class_Rect2>`                                              | :ref:`baking_rect<class_NavigationPolygon_property_baking_rect>`                               | ``Rect2(0, 0, 0, 0)``                           |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                          | :ref:`baking_rect_offset<class_NavigationPolygon_property_baking_rect_offset>`                 | ``Vector2(0, 0)``                               |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`float<class_float>`                                              | :ref:`border_size<class_NavigationPolygon_property_border_size>`                               | ``0.0``                                         |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`float<class_float>`                                              | :ref:`cell_size<class_NavigationPolygon_property_cell_size>`                                   | ``1.0``                                         |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`int<class_int>`                                                  | :ref:`parsed_collision_mask<class_NavigationPolygon_property_parsed_collision_mask>`           | ``4294967295``                                  |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>`   | :ref:`parsed_geometry_type<class_NavigationPolygon_property_parsed_geometry_type>`             | ``2``                                           |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>` | :ref:`sample_partition_type<class_NavigationPolygon_property_sample_partition_type>`           | ``0``                                           |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`StringName<class_StringName>`                                    | :ref:`source_geometry_group_name<class_NavigationPolygon_property_source_geometry_group_name>` | ``&"navigation_polygon_source_geometry_group"`` |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+
   | :ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>`   | :ref:`source_geometry_mode<class_NavigationPolygon_property_source_geometry_mode>`             | ``0``                                           |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------------------------+-------------------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_outline<class_NavigationPolygon_method_add_outline>`\ (\ outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                  |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_outline_at_index<class_NavigationPolygon_method_add_outline_at_index>`\ (\ outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, index\: :ref:`int<class_int>`\ ) |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_polygon<class_NavigationPolygon_method_add_polygon>`\ (\ polygon\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ )                                                      |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_NavigationPolygon_method_clear>`\ (\ )                                                                                                                             |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_outlines<class_NavigationPolygon_method_clear_outlines>`\ (\ )                                                                                                           |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_polygons<class_NavigationPolygon_method_clear_polygons>`\ (\ )                                                                                                           |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NavigationMesh<class_NavigationMesh>`         | :ref:`get_navigation_mesh<class_NavigationPolygon_method_get_navigation_mesh>`\ (\ )                                                                                                 |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`get_outline<class_NavigationPolygon_method_get_outline>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                            |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_outline_count<class_NavigationPolygon_method_get_outline_count>`\ (\ ) |const|                                                                                             |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`get_parsed_collision_mask_value<class_NavigationPolygon_method_get_parsed_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                           |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`get_polygon<class_NavigationPolygon_method_get_polygon>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                                    |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_polygon_count<class_NavigationPolygon_method_get_polygon_count>`\ (\ ) |const|                                                                                             |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`get_vertices<class_NavigationPolygon_method_get_vertices>`\ (\ ) |const|                                                                                                       |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`make_polygons_from_outlines<class_NavigationPolygon_method_make_polygons_from_outlines>`\ (\ )                                                                                 |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_outline<class_NavigationPolygon_method_remove_outline>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                              |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_outline<class_NavigationPolygon_method_set_outline>`\ (\ idx\: :ref:`int<class_int>`, outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                     |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_parsed_collision_mask_value<class_NavigationPolygon_method_set_parsed_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )  |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_vertices<class_NavigationPolygon_method_set_vertices>`\ (\ vertices\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                               |
   +-----------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_NavigationPolygon_SamplePartitionType:

.. rst-class:: classref-enumeration

enum **SamplePartitionType**: :ref:`🔗<enum_NavigationPolygon_SamplePartitionType>`

.. _class_NavigationPolygon_constant_SAMPLE_PARTITION_CONVEX_PARTITION:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>` **SAMPLE_PARTITION_CONVEX_PARTITION** = ``0``

Phân vùng lồi, tạo ra một navigation mesh với các polygon lồi.

.. _class_NavigationPolygon_constant_SAMPLE_PARTITION_TRIANGULATE:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>` **SAMPLE_PARTITION_TRIANGULATE** = ``1``

Phân vùng tam giác hóa, tạo ra một navigation mesh với các polygon tam giác.

.. _class_NavigationPolygon_constant_SAMPLE_PARTITION_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>` **SAMPLE_PARTITION_MAX** = ``2``

Biểu thị kích thước của enum :ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>`.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationPolygon_ParsedGeometryType:

.. rst-class:: classref-enumeration

enum **ParsedGeometryType**: :ref:`🔗<enum_NavigationPolygon_ParsedGeometryType>`

.. _class_NavigationPolygon_constant_PARSED_GEOMETRY_MESH_INSTANCES:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>` **PARSED_GEOMETRY_MESH_INSTANCES** = ``0``

Phân tích các mesh instance dưới dạng geometry cản trở. Bao gồm các node :ref:`Polygon2D<class_Polygon2D>`, :ref:`MeshInstance2D<class_MeshInstance2D>`, :ref:`MultiMeshInstance2D<class_MultiMeshInstance2D>` và :ref:`TileMap<class_TileMap>`.

Mesh chỉ được phân tích khi sử dụng định dạng surface 2D vertices.

.. _class_NavigationPolygon_constant_PARSED_GEOMETRY_STATIC_COLLIDERS:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>` **PARSED_GEOMETRY_STATIC_COLLIDERS** = ``1``

Phân tích các collider :ref:`StaticBody2D<class_StaticBody2D>` và :ref:`TileMap<class_TileMap>` dưới dạng geometry cản trở. Collider phải nằm trong một trong các layer được chỉ định bởi :ref:`parsed_collision_mask<class_NavigationPolygon_property_parsed_collision_mask>`.

.. _class_NavigationPolygon_constant_PARSED_GEOMETRY_BOTH:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>` **PARSED_GEOMETRY_BOTH** = ``2``

Cả :ref:`PARSED_GEOMETRY_MESH_INSTANCES<class_NavigationPolygon_constant_PARSED_GEOMETRY_MESH_INSTANCES>` và :ref:`PARSED_GEOMETRY_STATIC_COLLIDERS<class_NavigationPolygon_constant_PARSED_GEOMETRY_STATIC_COLLIDERS>`.

.. _class_NavigationPolygon_constant_PARSED_GEOMETRY_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>` **PARSED_GEOMETRY_MAX** = ``3``

Biểu thị kích thước của enum :ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>`.

.. rst-class:: classref-item-separator

----

.. _enum_NavigationPolygon_SourceGeometryMode:

.. rst-class:: classref-enumeration

enum **SourceGeometryMode**: :ref:`🔗<enum_NavigationPolygon_SourceGeometryMode>`

.. _class_NavigationPolygon_constant_SOURCE_GEOMETRY_ROOT_NODE_CHILDREN:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>` **SOURCE_GEOMETRY_ROOT_NODE_CHILDREN** = ``0``

Quét đệ quy các node con của node gốc để tìm geometry.

.. _class_NavigationPolygon_constant_SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>` **SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN** = ``1``

Quét các node trong một group và các node con của chúng một cách đệ quy để tìm geometry. Group được chỉ định bởi :ref:`source_geometry_group_name<class_NavigationPolygon_property_source_geometry_group_name>`.

.. _class_NavigationPolygon_constant_SOURCE_GEOMETRY_GROUPS_EXPLICIT:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>` **SOURCE_GEOMETRY_GROUPS_EXPLICIT** = ``2``

Sử dụng các node trong một group làm geometry. Group được chỉ định bởi :ref:`source_geometry_group_name<class_NavigationPolygon_property_source_geometry_group_name>`.

.. _class_NavigationPolygon_constant_SOURCE_GEOMETRY_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>` **SOURCE_GEOMETRY_MAX** = ``3``

Biểu thị kích thước của enum :ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_NavigationPolygon_property_agent_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **agent_radius** = ``10.0`` :ref:`🔗<class_NavigationPolygon_property_agent_radius>`

.. rst-class:: classref-property-setget

- |void| **set_agent_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_agent_radius**\ (\ )

Khoảng cách dùng để bào mòn/thu nhỏ bề mặt có thể đi qua khi bake navigation mesh.

\ **Lưu ý:** Bán kính phải lớn hơn hoặc bằng ``0.0``. Nếu bán kính là ``0.0``, sẽ không thể sửa các phần outline chồng lấn không hợp lệ và những lỗi về độ chính xác khác trong quá trình baking. Do đó, một số obstacle có thể bị loại trừ không chính xác khỏi navigation mesh cuối cùng hoặc có thể xóa các polygon của navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_baking_rect:

.. rst-class:: classref-property

:ref:`Rect2<class_Rect2>` **baking_rect** = ``Rect2(0, 0, 0, 0)`` :ref:`🔗<class_NavigationPolygon_property_baking_rect>`

.. rst-class:: classref-property-setget

- |void| **set_baking_rect**\ (\ value\: :ref:`Rect2<class_Rect2>`\ ) - :ref:`Rect2<class_Rect2>` **get_baking_rect**\ (\ )

Nếu :ref:`Rect2<class_Rect2>` baking có diện tích, quá trình baking navigation mesh sẽ bị giới hạn trong vùng bao quanh nó.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_baking_rect_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **baking_rect_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationPolygon_property_baking_rect_offset>`

.. rst-class:: classref-property-setget

- |void| **set_baking_rect_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_baking_rect_offset**\ (\ )

Độ lệch vị trí được áp dụng cho :ref:`baking_rect<class_NavigationPolygon_property_baking_rect>` :ref:`Rect2<class_Rect2>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_border_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **border_size** = ``0.0`` :ref:`🔗<class_NavigationPolygon_property_border_size>`

.. rst-class:: classref-property-setget

- |void| **set_border_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_border_size**\ (\ )

Kích thước của đường viền không thể điều hướng xung quanh vùng giới hạn bake được xác định bởi :ref:`baking_rect<class_NavigationPolygon_property_baking_rect>` :ref:`Rect2<class_Rect2>`.

Kết hợp với :ref:`baking_rect<class_NavigationPolygon_property_baking_rect>`, border size có thể được dùng để bake các navigation mesh căn chỉnh theo tile mà không làm các cạnh tile bị thu nhỏ bởi :ref:`agent_radius<class_NavigationPolygon_property_agent_radius>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_cell_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **cell_size** = ``1.0`` :ref:`🔗<class_NavigationPolygon_property_cell_size>`

.. rst-class:: classref-property-setget

- |void| **set_cell_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_cell_size**\ (\ )

Kích thước cell được dùng để rasterize các vertex của navigation mesh. Phải khớp với kích thước cell trên navigation map.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_parsed_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **parsed_collision_mask** = ``4294967295`` :ref:`🔗<class_NavigationPolygon_property_parsed_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_parsed_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_parsed_collision_mask**\ (\ )

Các physics layer cần quét để tìm static collider.

Chỉ được sử dụng khi :ref:`parsed_geometry_type<class_NavigationPolygon_property_parsed_geometry_type>` là :ref:`PARSED_GEOMETRY_STATIC_COLLIDERS<class_NavigationPolygon_constant_PARSED_GEOMETRY_STATIC_COLLIDERS>` hoặc :ref:`PARSED_GEOMETRY_BOTH<class_NavigationPolygon_constant_PARSED_GEOMETRY_BOTH>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_parsed_geometry_type:

.. rst-class:: classref-property

:ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>` **parsed_geometry_type** = ``2`` :ref:`🔗<class_NavigationPolygon_property_parsed_geometry_type>`

.. rst-class:: classref-property-setget

- |void| **set_parsed_geometry_type**\ (\ value\: :ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>`\ ) - :ref:`ParsedGeometryType<enum_NavigationPolygon_ParsedGeometryType>` **get_parsed_geometry_type**\ (\ )

Xác định loại node nào sẽ được phân tích dưới dạng geometry.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_sample_partition_type:

.. rst-class:: classref-property

:ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>` **sample_partition_type** = ``0`` :ref:`🔗<class_NavigationPolygon_property_sample_partition_type>`

.. rst-class:: classref-property-setget

- |void| **set_sample_partition_type**\ (\ value\: :ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>`\ ) - :ref:`SamplePartitionType<enum_NavigationPolygon_SamplePartitionType>` **get_sample_partition_type**\ (\ )

Thuật toán phân vùng để tạo các polygon của navigation mesh.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_source_geometry_group_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **source_geometry_group_name** = ``&"navigation_polygon_source_geometry_group"`` :ref:`🔗<class_NavigationPolygon_property_source_geometry_group_name>`

.. rst-class:: classref-property-setget

- |void| **set_source_geometry_group_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_source_geometry_group_name**\ (\ )

Tên group của các node cần được phân tích để lấy geometry nguồn cho baking.

Chỉ được sử dụng khi :ref:`source_geometry_mode<class_NavigationPolygon_property_source_geometry_mode>` là :ref:`SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN<class_NavigationPolygon_constant_SOURCE_GEOMETRY_GROUPS_WITH_CHILDREN>` hoặc :ref:`SOURCE_GEOMETRY_GROUPS_EXPLICIT<class_NavigationPolygon_constant_SOURCE_GEOMETRY_GROUPS_EXPLICIT>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_property_source_geometry_mode:

.. rst-class:: classref-property

:ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>` **source_geometry_mode** = ``0`` :ref:`🔗<class_NavigationPolygon_property_source_geometry_mode>`

.. rst-class:: classref-property-setget

- |void| **set_source_geometry_mode**\ (\ value\: :ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>`\ ) - :ref:`SourceGeometryMode<enum_NavigationPolygon_SourceGeometryMode>` **get_source_geometry_mode**\ (\ )

Nguồn geometry được sử dụng khi baking.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_NavigationPolygon_method_add_outline:

.. rst-class:: classref-method

|void| **add_outline**\ (\ outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_NavigationPolygon_method_add_outline>`

Thêm một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa các vertex của một outline vào mảng nội bộ chứa tất cả outline.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_add_outline_at_index:

.. rst-class:: classref-method

|void| **add_outline_at_index**\ (\ outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_NavigationPolygon_method_add_outline_at_index>`

Thêm một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa các vertex của một outline vào mảng nội bộ chứa tất cả outline tại một vị trí cố định.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_add_polygon:

.. rst-class:: classref-method

|void| **add_polygon**\ (\ polygon\: :ref:`PackedInt32Array<class_PackedInt32Array>`\ ) :ref:`🔗<class_NavigationPolygon_method_add_polygon>`

Thêm một polygon bằng các chỉ mục của các vertex nhận được khi gọi :ref:`get_vertices()<class_NavigationPolygon_method_get_vertices>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_NavigationPolygon_method_clear>`

Xóa các mảng nội bộ chứa vertex và chỉ mục polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_clear_outlines:

.. rst-class:: classref-method

|void| **clear_outlines**\ (\ ) :ref:`🔗<class_NavigationPolygon_method_clear_outlines>`

Xóa mảng outline, nhưng không xóa các vertex và polygon được tạo từ chúng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_clear_polygons:

.. rst-class:: classref-method

|void| **clear_polygons**\ (\ ) :ref:`🔗<class_NavigationPolygon_method_clear_polygons>`

Xóa mảng polygon, nhưng không xóa mảng outline và vertex.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_navigation_mesh:

.. rst-class:: classref-method

:ref:`NavigationMesh<class_NavigationMesh>` **get_navigation_mesh**\ (\ ) :ref:`🔗<class_NavigationPolygon_method_get_navigation_mesh>`

Trả về :ref:`NavigationMesh<class_NavigationMesh>` thu được từ navigation polygon này. Navigation mesh này có thể được dùng để cập nhật navigation mesh của một region trực tiếp bằng API :ref:`NavigationServer3D.region_set_navigation_mesh()<class_NavigationServer3D_method_region_set_navigation_mesh>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_outline:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_outline**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationPolygon_method_get_outline>`

Trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa các đỉnh của một đường bao được tạo trong editor hoặc bằng script.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_outline_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_outline_count**\ (\ ) |const| :ref:`🔗<class_NavigationPolygon_method_get_outline_count>`

Trả về số lượng đường bao được tạo trong editor hoặc bằng script.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_parsed_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_parsed_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationPolygon_method_get_parsed_collision_mask_value>`

Trả về việc lớp được chỉ định của :ref:`parsed_collision_mask<class_NavigationPolygon_property_parsed_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_polygon:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_polygon**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_NavigationPolygon_method_get_polygon>`

Trả về một :ref:`PackedInt32Array<class_PackedInt32Array>` chứa các chỉ số của các đỉnh thuộc một polygon đã tạo.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_polygon_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_polygon_count**\ (\ ) |const| :ref:`🔗<class_NavigationPolygon_method_get_polygon_count>`

Trả về số lượng của tất cả polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_get_vertices:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_vertices**\ (\ ) |const| :ref:`🔗<class_NavigationPolygon_method_get_vertices>`

Trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa tất cả các đỉnh đang được dùng để tạo polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_make_polygons_from_outlines:

.. rst-class:: classref-method

|void| **make_polygons_from_outlines**\ (\ ) :ref:`🔗<class_NavigationPolygon_method_make_polygons_from_outlines>`

**Đã ngừng sử dụng:** Thay vào đó, hãy dùng :ref:`NavigationServer2D.parse_source_geometry_data()<class_NavigationServer2D_method_parse_source_geometry_data>` và :ref:`NavigationServer2D.bake_from_source_geometry_data()<class_NavigationServer2D_method_bake_from_source_geometry_data>`.

Tạo các polygon từ những đường bao được thêm trong editor hoặc bằng script.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_remove_outline:

.. rst-class:: classref-method

|void| **remove_outline**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_NavigationPolygon_method_remove_outline>`

Xóa một đường bao được tạo trong editor hoặc bằng script. Bạn phải gọi :ref:`make_polygons_from_outlines()<class_NavigationPolygon_method_make_polygons_from_outlines>` để cập nhật các polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_set_outline:

.. rst-class:: classref-method

|void| **set_outline**\ (\ idx\: :ref:`int<class_int>`, outline\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_NavigationPolygon_method_set_outline>`

Thay đổi một đường bao được tạo trong editor hoặc bằng script. Bạn phải gọi :ref:`make_polygons_from_outlines()<class_NavigationPolygon_method_make_polygons_from_outlines>` để cập nhật các polygon.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_set_parsed_collision_mask_value:

.. rst-class:: classref-method

|void| **set_parsed_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationPolygon_method_set_parsed_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt lớp được chỉ định trong :ref:`parsed_collision_mask<class_NavigationPolygon_property_parsed_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationPolygon_method_set_vertices:

.. rst-class:: classref-method

|void| **set_vertices**\ (\ vertices\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_NavigationPolygon_method_set_vertices>`

Thiết lập các đỉnh mà sau đó có thể được lập chỉ mục để tạo polygon bằng phương thức :ref:`add_polygon()<class_NavigationPolygon_method_add_polygon>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
