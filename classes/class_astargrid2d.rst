:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AStarGrid2D.xml.

.. _class_AStarGrid2D:

AStarGrid2D
===========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một triển khai của A\* để tìm đường đi ngắn nhất giữa hai điểm trên một grid 2D không đầy đủ.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AStarGrid2D** là một biến thể của :ref:`AStar2D<class_AStar2D>` được chuyên biệt hóa cho các grid 2D không đầy đủ. Lớp này dễ sử dụng hơn vì không yêu cầu bạn phải tự tạo các điểm và kết nối chúng với nhau. Lớp này cũng hỗ trợ nhiều loại heuristic, các chế độ di chuyển theo đường chéo và chế độ jumping để tăng tốc độ tính toán.

Để sử dụng **AStarGrid2D**, bạn chỉ cần đặt :ref:`region<class_AStarGrid2D_property_region>` của grid, tùy chọn đặt :ref:`cell_size<class_AStarGrid2D_property_cell_size>`, sau đó gọi phương thức :ref:`update()<class_AStarGrid2D_method_update>`:


.. tabs::

 .. code-tab:: gdscript

    var astar_grid = AStarGrid2D.new()
    astar_grid.region = Rect2i(0, 0, 32, 32)
    astar_grid.cell_size = Vector2(16, 16)
    astar_grid.update()
    print(astar_grid.get_id_path(Vector2i(0, 0), Vector2i(3, 4))) # In ra [(0, 0), (1, 1), (2, 2), (3, 3), (3, 4)]
    print(astar_grid.get_point_path(Vector2i(0, 0), Vector2i(3, 4))) # In ra [(0, 0), (16, 16), (32, 32), (48, 48), (48, 64)]

 .. code-tab:: csharp

    AStarGrid2D astarGrid = new AStarGrid2D();
    astarGrid.Region = new Rect2I(0, 0, 32, 32);
    astarGrid.CellSize = new Vector2I(16, 16);
    astarGrid.Update();
    GD.Print(astarGrid.GetIdPath(Vector2I.Zero, new Vector2I(3, 4))); // In ra [(0, 0), (1, 1), (2, 2), (3, 3), (3, 4)]
    GD.Print(astarGrid.GetPointPath(Vector2I.Zero, new Vector2I(3, 4))); // In ra [(0, 0), (16, 16), (32, 32), (48, 48), (48, 64)]



Để xóa một điểm khỏi grid pathfinding, điểm đó phải được đặt là "solid" bằng :ref:`set_point_solid()<class_AStarGrid2D_method_set_point_solid>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Grid-based Navigation with AStarGrid2D Demo <https://godotengine.org/asset-library/asset/2723>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`CellShape<enum_AStarGrid2D_CellShape>`       | :ref:`cell_shape<class_AStarGrid2D_property_cell_shape>`                                 | ``0``                  |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`cell_size<class_AStarGrid2D_property_cell_size>`                                   | ``Vector2(1, 1)``      |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`Heuristic<enum_AStarGrid2D_Heuristic>`       | :ref:`default_compute_heuristic<class_AStarGrid2D_property_default_compute_heuristic>`   | ``0``                  |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`Heuristic<enum_AStarGrid2D_Heuristic>`       | :ref:`default_estimate_heuristic<class_AStarGrid2D_property_default_estimate_heuristic>` | ``0``                  |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` | :ref:`diagonal_mode<class_AStarGrid2D_property_diagonal_mode>`                           | ``0``                  |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`bool<class_bool>`                            | :ref:`jumping_enabled<class_AStarGrid2D_property_jumping_enabled>`                       | ``false``              |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`Vector2<class_Vector2>`                      | :ref:`offset<class_AStarGrid2D_property_offset>`                                         | ``Vector2(0, 0)``      |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`Rect2i<class_Rect2i>`                        | :ref:`region<class_AStarGrid2D_property_region>`                                         | ``Rect2i(0, 0, 0, 0)`` |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+
   | :ref:`Vector2i<class_Vector2i>`                    | :ref:`size<class_AStarGrid2D_property_size>`                                             | ``Vector2i(0, 0)``     |
   +----------------------------------------------------+------------------------------------------------------------------------------------------+------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`_compute_cost<class_AStarGrid2D_private_method__compute_cost>`\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, to_id\: :ref:`Vector2i<class_Vector2i>`\ ) |virtual| |const|                               |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`_estimate_cost<class_AStarGrid2D_private_method__estimate_cost>`\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, end_id\: :ref:`Vector2i<class_Vector2i>`\ ) |virtual| |const|                            |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`clear<class_AStarGrid2D_method_clear>`\ (\ )                                                                                                                                                             |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`fill_solid_region<class_AStarGrid2D_method_fill_solid_region>`\ (\ region\: :ref:`Rect2i<class_Rect2i>`, solid\: :ref:`bool<class_bool>` = true\ )                                                       |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`fill_weight_scale_region<class_AStarGrid2D_method_fill_weight_scale_region>`\ (\ region\: :ref:`Rect2i<class_Rect2i>`, weight_scale\: :ref:`float<class_float>`\ )                                       |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector2i<class_Vector2i>`\]     | :ref:`get_id_path<class_AStarGrid2D_method_get_id_path>`\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, to_id\: :ref:`Vector2i<class_Vector2i>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ )       |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_point_data_in_region<class_AStarGrid2D_method_get_point_data_in_region>`\ (\ region\: :ref:`Rect2i<class_Rect2i>`\ ) |const|                                                                         |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`              | :ref:`get_point_path<class_AStarGrid2D_method_get_point_path>`\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, to_id\: :ref:`Vector2i<class_Vector2i>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ ) |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                    | :ref:`get_point_position<class_AStarGrid2D_method_get_point_position>`\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const|                                                                                     |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_point_weight_scale<class_AStarGrid2D_method_get_point_weight_scale>`\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const|                                                                             |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_dirty<class_AStarGrid2D_method_is_dirty>`\ (\ ) |const|                                                                                                                                               |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_in_bounds<class_AStarGrid2D_method_is_in_bounds>`\ (\ x\: :ref:`int<class_int>`, y\: :ref:`int<class_int>`\ ) |const|                                                                                 |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_in_boundsv<class_AStarGrid2D_method_is_in_boundsv>`\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const|                                                                                               |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_point_solid<class_AStarGrid2D_method_is_point_solid>`\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const|                                                                                             |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_point_solid<class_AStarGrid2D_method_set_point_solid>`\ (\ id\: :ref:`Vector2i<class_Vector2i>`, solid\: :ref:`bool<class_bool>` = true\ )                                                           |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_point_weight_scale<class_AStarGrid2D_method_set_point_weight_scale>`\ (\ id\: :ref:`Vector2i<class_Vector2i>`, weight_scale\: :ref:`float<class_float>`\ )                                           |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`update<class_AStarGrid2D_method_update>`\ (\ )                                                                                                                                                           |
   +------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AStarGrid2D_Heuristic:

.. rst-class:: classref-enumeration

enum **Heuristic**: :ref:`🔗<enum_AStarGrid2D_Heuristic>`

.. _class_AStarGrid2D_constant_HEURISTIC_EUCLIDEAN:

.. rst-class:: classref-enumeration-constant

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **HEURISTIC_EUCLIDEAN** = ``0``

`Euclidean heuristic <https://en.wikipedia.org/wiki/Euclidean_distance>`__ được sử dụng cho pathfinding theo công thức sau:

::

    dx = abs(to_id.x - from_id.x)
    dy = abs(to_id.y - from_id.y)
    result = sqrt(dx * dx + dy * dy)

\ **Lưu ý:** Đây cũng là heuristic nội bộ được sử dụng mặc định trong :ref:`AStar3D<class_AStar3D>` và :ref:`AStar2D<class_AStar2D>` (bao gồm cả tọa độ trục z nếu có).

.. _class_AStarGrid2D_constant_HEURISTIC_MANHATTAN:

.. rst-class:: classref-enumeration-constant

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **HEURISTIC_MANHATTAN** = ``1``

`Manhattan heuristic <https://en.wikipedia.org/wiki/Taxicab_geometry>`__ được sử dụng cho pathfinding theo công thức sau:

::

    dx = abs(to_id.x - from_id.x)
    dy = abs(to_id.y - from_id.y)
    result = dx + dy

\ **Lưu ý:** Heuristic này được sử dụng với các chuyển động trực giao 4 hướng, được cung cấp bằng cách đặt :ref:`diagonal_mode<class_AStarGrid2D_property_diagonal_mode>` thành :ref:`DIAGONAL_MODE_NEVER<class_AStarGrid2D_constant_DIAGONAL_MODE_NEVER>`.

.. _class_AStarGrid2D_constant_HEURISTIC_OCTILE:

.. rst-class:: classref-enumeration-constant

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **HEURISTIC_OCTILE** = ``2``

Heuristic Octile được sử dụng cho pathfinding theo công thức sau:

::

    dx = abs(to_id.x - from_id.x)
    dy = abs(to_id.y - from_id.y)
    f = sqrt(2) - 1
    result = (dx < dy) ? f * dx + dy : f * dy + dx;

.. _class_AStarGrid2D_constant_HEURISTIC_CHEBYSHEV:

.. rst-class:: classref-enumeration-constant

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **HEURISTIC_CHEBYSHEV** = ``3``

`Chebyshev heuristic <https://en.wikipedia.org/wiki/Chebyshev_distance>`__ được sử dụng cho pathfinding theo công thức sau:

::

    dx = abs(to_id.x - from_id.x)
    dy = abs(to_id.y - from_id.y)
    result = max(dx, dy)

.. _class_AStarGrid2D_constant_HEURISTIC_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **HEURISTIC_MAX** = ``4``

Biểu thị kích thước của enum :ref:`Heuristic<enum_AStarGrid2D_Heuristic>`.

.. rst-class:: classref-item-separator

----

.. _enum_AStarGrid2D_DiagonalMode:

.. rst-class:: classref-enumeration

enum **DiagonalMode**: :ref:`🔗<enum_AStarGrid2D_DiagonalMode>`

.. _class_AStarGrid2D_constant_DIAGONAL_MODE_ALWAYS:

.. rst-class:: classref-enumeration-constant

:ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **DIAGONAL_MODE_ALWAYS** = ``0``

Thuật toán pathfinding sẽ bỏ qua các ô lân cận solid xung quanh ô đích và cho phép đi qua bằng đường chéo.

.. _class_AStarGrid2D_constant_DIAGONAL_MODE_NEVER:

.. rst-class:: classref-enumeration-constant

:ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **DIAGONAL_MODE_NEVER** = ``1``

Thuật toán pathfinding sẽ bỏ qua mọi đường chéo và đường đi sẽ luôn là đường trực giao.

.. _class_AStarGrid2D_constant_DIAGONAL_MODE_AT_LEAST_ONE_WALKABLE:

.. rst-class:: classref-enumeration-constant

:ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **DIAGONAL_MODE_AT_LEAST_ONE_WALKABLE** = ``2``

Thuật toán pathfinding sẽ tránh sử dụng đường chéo nếu có ít nhất hai chướng ngại vật được đặt xung quanh các ô lân cận của đoạn đường cụ thể.

.. _class_AStarGrid2D_constant_DIAGONAL_MODE_ONLY_IF_NO_OBSTACLES:

.. rst-class:: classref-enumeration-constant

:ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **DIAGONAL_MODE_ONLY_IF_NO_OBSTACLES** = ``3``

Thuật toán pathfinding sẽ tránh sử dụng đường chéo nếu có bất kỳ chướng ngại vật nào được đặt xung quanh các ô lân cận của đoạn đường cụ thể.

.. _class_AStarGrid2D_constant_DIAGONAL_MODE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **DIAGONAL_MODE_MAX** = ``4``

Biểu thị kích thước của enum :ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>`.

.. rst-class:: classref-item-separator

----

.. _enum_AStarGrid2D_CellShape:

.. rst-class:: classref-enumeration

enum **CellShape**: :ref:`🔗<enum_AStarGrid2D_CellShape>`

.. _class_AStarGrid2D_constant_CELL_SHAPE_SQUARE:

.. rst-class:: classref-enumeration-constant

:ref:`CellShape<enum_AStarGrid2D_CellShape>` **CELL_SHAPE_SQUARE** = ``0``

Hình dạng ô chữ nhật.

.. _class_AStarGrid2D_constant_CELL_SHAPE_ISOMETRIC_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`CellShape<enum_AStarGrid2D_CellShape>` **CELL_SHAPE_ISOMETRIC_RIGHT** = ``1``

Hình dạng ô kim cương (dùng cho giao diện isometric). Bố cục tọa độ ô trong đó trục ngang hướng lên-phải và trục dọc hướng xuống-phải.

.. _class_AStarGrid2D_constant_CELL_SHAPE_ISOMETRIC_DOWN:

.. rst-class:: classref-enumeration-constant

:ref:`CellShape<enum_AStarGrid2D_CellShape>` **CELL_SHAPE_ISOMETRIC_DOWN** = ``2``

Hình dạng ô kim cương (dùng cho giao diện isometric). Bố cục tọa độ ô trong đó trục ngang hướng xuống-phải và trục dọc hướng xuống-trái.

.. _class_AStarGrid2D_constant_CELL_SHAPE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`CellShape<enum_AStarGrid2D_CellShape>` **CELL_SHAPE_MAX** = ``3``

Biểu thị kích thước của enum :ref:`CellShape<enum_AStarGrid2D_CellShape>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AStarGrid2D_property_cell_shape:

.. rst-class:: classref-property

:ref:`CellShape<enum_AStarGrid2D_CellShape>` **cell_shape** = ``0`` :ref:`🔗<class_AStarGrid2D_property_cell_shape>`

.. rst-class:: classref-property-setget

- |void| **set_cell_shape**\ (\ value\: :ref:`CellShape<enum_AStarGrid2D_CellShape>`\ ) - :ref:`CellShape<enum_AStarGrid2D_CellShape>` **get_cell_shape**\ (\ )

Hình dạng ô. Ảnh hưởng đến cách các vị trí được sắp xếp trong grid. Nếu thay đổi, cần gọi :ref:`update()<class_AStarGrid2D_method_update>` trước khi tìm đường đi tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_cell_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **cell_size** = ``Vector2(1, 1)`` :ref:`🔗<class_AStarGrid2D_property_cell_size>`

.. rst-class:: classref-property-setget

- |void| **set_cell_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_cell_size**\ (\ )

Kích thước của ô điểm được áp dụng để tính vị trí điểm kết quả do :ref:`get_point_path()<class_AStarGrid2D_method_get_point_path>` trả về. Nếu thay đổi, cần gọi :ref:`update()<class_AStarGrid2D_method_update>` trước khi tìm đường đi tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_default_compute_heuristic:

.. rst-class:: classref-property

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **default_compute_heuristic** = ``0`` :ref:`🔗<class_AStarGrid2D_property_default_compute_heuristic>`

.. rst-class:: classref-property-setget

- |void| **set_default_compute_heuristic**\ (\ value\: :ref:`Heuristic<enum_AStarGrid2D_Heuristic>`\ ) - :ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **get_default_compute_heuristic**\ (\ )

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` mặc định được sử dụng để tính chi phí giữa hai điểm nếu :ref:`_compute_cost()<class_AStarGrid2D_private_method__compute_cost>` chưa được ghi đè.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_default_estimate_heuristic:

.. rst-class:: classref-property

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **default_estimate_heuristic** = ``0`` :ref:`🔗<class_AStarGrid2D_property_default_estimate_heuristic>`

.. rst-class:: classref-property-setget

- |void| **set_default_estimate_heuristic**\ (\ value\: :ref:`Heuristic<enum_AStarGrid2D_Heuristic>`\ ) - :ref:`Heuristic<enum_AStarGrid2D_Heuristic>` **get_default_estimate_heuristic**\ (\ )

:ref:`Heuristic<enum_AStarGrid2D_Heuristic>` mặc định được sử dụng để tính chi phí giữa điểm và điểm kết thúc nếu :ref:`_estimate_cost()<class_AStarGrid2D_private_method__estimate_cost>` chưa được ghi đè.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_diagonal_mode:

.. rst-class:: classref-property

:ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **diagonal_mode** = ``0`` :ref:`🔗<class_AStarGrid2D_property_diagonal_mode>`

.. rst-class:: classref-property-setget

- |void| **set_diagonal_mode**\ (\ value\: :ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>`\ ) - :ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` **get_diagonal_mode**\ (\ )

Chế độ :ref:`DiagonalMode<enum_AStarGrid2D_DiagonalMode>` cụ thể sẽ buộc đường đi tránh hoặc chấp nhận các đường chéo được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_jumping_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **jumping_enabled** = ``false`` :ref:`🔗<class_AStarGrid2D_property_jumping_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_jumping_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_jumping_enabled**\ (\ )

Bật hoặc tắt jumping để bỏ qua các điểm trung gian và tăng tốc thuật toán tìm kiếm.

\ **Lưu ý:** Hiện tại, việc bật tùy chọn này sẽ tắt việc xét đến việc scale trọng số trong pathfinding.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_AStarGrid2D_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Offset của grid được áp dụng để tính vị trí điểm kết quả do :ref:`get_point_path()<class_AStarGrid2D_method_get_point_path>` trả về. Nếu thay đổi, cần gọi :ref:`update()<class_AStarGrid2D_method_update>` trước khi tìm đường đi tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_region:

.. rst-class:: classref-property

:ref:`Rect2i<class_Rect2i>` **region** = ``Rect2i(0, 0, 0, 0)`` :ref:`🔗<class_AStarGrid2D_property_region>`

.. rst-class:: classref-property-setget

- |void| **set_region**\ (\ value\: :ref:`Rect2i<class_Rect2i>`\ ) - :ref:`Rect2i<class_Rect2i>` **get_region**\ (\ )

Vùng các ô grid khả dụng cho pathfinding. Nếu thay đổi, cần gọi :ref:`update()<class_AStarGrid2D_method_update>` trước khi tìm đường đi tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_property_size:

.. rst-class:: classref-property

:ref:`Vector2i<class_Vector2i>` **size** = ``Vector2i(0, 0)`` :ref:`🔗<class_AStarGrid2D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector2i<class_Vector2i>`\ ) - :ref:`Vector2i<class_Vector2i>` **get_size**\ (\ )

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`region<class_AStarGrid2D_property_region>`.

Kích thước của grid (số ô có kích thước :ref:`cell_size<class_AStarGrid2D_property_cell_size>` trên mỗi trục). Nếu thay đổi, cần gọi :ref:`update()<class_AStarGrid2D_method_update>` trước khi tìm đường đi tiếp theo.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AStarGrid2D_private_method__compute_cost:

.. rst-class:: classref-method

:ref:`float<class_float>` **_compute_cost**\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, to_id\: :ref:`Vector2i<class_Vector2i>`\ ) |virtual| |const| :ref:`🔗<class_AStarGrid2D_private_method__compute_cost>`

Được gọi khi tính chi phí giữa hai điểm được kết nối.

Lưu ý rằng hàm này bị ẩn trong lớp **AStarGrid2D** mặc định.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_private_method__estimate_cost:

.. rst-class:: classref-method

:ref:`float<class_float>` **_estimate_cost**\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, end_id\: :ref:`Vector2i<class_Vector2i>`\ ) |virtual| |const| :ref:`🔗<class_AStarGrid2D_private_method__estimate_cost>`

Được gọi khi ước tính chi phí giữa một điểm và điểm kết thúc của đường đi.

Lưu ý rằng hàm này bị ẩn trong lớp **AStarGrid2D** mặc định.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_AStarGrid2D_method_clear>`

Xóa grid và đặt :ref:`region<class_AStarGrid2D_property_region>` thành ``Rect2i(0, 0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_fill_solid_region:

.. rst-class:: classref-method

|void| **fill_solid_region**\ (\ region\: :ref:`Rect2i<class_Rect2i>`, solid\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AStarGrid2D_method_fill_solid_region>`

Điền ``region`` đã cho trên grid bằng giá trị được chỉ định cho cờ solid.

\ **Lưu ý:** Không cần gọi :ref:`update()<class_AStarGrid2D_method_update>` sau khi gọi hàm này.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_fill_weight_scale_region:

.. rst-class:: classref-method

|void| **fill_weight_scale_region**\ (\ region\: :ref:`Rect2i<class_Rect2i>`, weight_scale\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AStarGrid2D_method_fill_weight_scale_region>`

Điền ``region`` đã cho trên grid bằng giá trị được chỉ định cho weight scale.

\ **Lưu ý:** Không cần gọi :ref:`update()<class_AStarGrid2D_method_update>` sau khi gọi hàm này.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_get_id_path:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector2i<class_Vector2i>`\] **get_id_path**\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, to_id\: :ref:`Vector2i<class_Vector2i>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AStarGrid2D_method_get_id_path>`

Trả về một mảng chứa ID của các điểm tạo thành đường đi được AStar2D tìm thấy giữa các điểm đã cho. Mảng được sắp xếp từ điểm bắt đầu đến điểm kết thúc của đường đi.

Nếu điểm ``from_id`` bị vô hiệu hóa, trả về một mảng rỗng (ngay cả khi ``from_id == to_id``).

Nếu điểm ``from_id`` không bị vô hiệu hóa, không có đường đi hợp lệ đến đích và ``allow_partial_path`` là ``true``, trả về đường đi đến điểm gần đích nhất có thể tiếp cận.

\ **Lưu ý:** Khi ``allow_partial_path`` là ``true`` và ``to_id`` là solid, quá trình tìm kiếm có thể mất thời gian lâu bất thường mới hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_get_point_data_in_region:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_point_data_in_region**\ (\ region\: :ref:`Rect2i<class_Rect2i>`\ ) |const| :ref:`🔗<class_AStarGrid2D_method_get_point_data_in_region>`

Trả về một mảng các dictionary chứa dữ liệu điểm (``id``: :ref:`Vector2i<class_Vector2i>`, ``position``: :ref:`Vector2<class_Vector2>`, ``solid``: :ref:`bool<class_bool>`, ``weight_scale``: :ref:`float<class_float>`) trong một ``region``.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_get_point_path:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_point_path**\ (\ from_id\: :ref:`Vector2i<class_Vector2i>`, to_id\: :ref:`Vector2i<class_Vector2i>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AStarGrid2D_method_get_point_path>`

Trả về một mảng chứa các điểm nằm trên đường đi được **AStarGrid2D** tìm thấy giữa các điểm đã cho. Mảng được sắp xếp từ điểm bắt đầu đến điểm kết thúc của đường đi.

Nếu điểm ``from_id`` bị vô hiệu hóa, trả về một mảng rỗng (ngay cả khi ``from_id == to_id``).

Nếu điểm ``from_id`` không bị vô hiệu hóa, không có đường đi hợp lệ đến đích và ``allow_partial_path`` là ``true``, trả về đường đi đến điểm gần đích nhất có thể tiếp cận.

\ **Lưu ý:** Phương thức này không an toàn khi chạy đa luồng; tại một thời điểm, phương thức chỉ có thể được sử dụng từ một :ref:`Thread<class_Thread>` duy nhất. Hãy cân nhắc sử dụng :ref:`Mutex<class_Mutex>` để đảm bảo quyền truy cập độc quyền của một thread nhằm tránh race condition.

Ngoài ra, khi ``allow_partial_path`` là ``true`` và ``to_id`` là solid, quá trình tìm kiếm có thể mất thời gian lâu bất thường mới hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_get_point_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_point_position**\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const| :ref:`🔗<class_AStarGrid2D_method_get_point_position>`

Trả về vị trí của point liên kết với ``id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_get_point_weight_scale:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_point_weight_scale**\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const| :ref:`🔗<class_AStarGrid2D_method_get_point_weight_scale>`

Trả về weight scale của point liên kết với ``id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_is_dirty:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_dirty**\ (\ ) |const| :ref:`🔗<class_AStarGrid2D_method_is_dirty>`

Cho biết các tham số của grid đã được thay đổi và cần gọi :ref:`update()<class_AStarGrid2D_method_update>`.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_is_in_bounds:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_in_bounds**\ (\ x\: :ref:`int<class_int>`, y\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AStarGrid2D_method_is_in_bounds>`

Trả về ``true`` nếu ``x`` và ``y`` là một tọa độ grid (id) hợp lệ, tức là nếu nó nằm trong :ref:`region<class_AStarGrid2D_property_region>`. Tương đương với ``region.has_point(Vector2i(x, y))``.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_is_in_boundsv:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_in_boundsv**\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const| :ref:`🔗<class_AStarGrid2D_method_is_in_boundsv>`

Trả về ``true`` nếu vector ``id`` là một tọa độ grid hợp lệ, tức là nếu nó nằm trong :ref:`region<class_AStarGrid2D_property_region>`. Tương đương với ``region.has_point(id)``.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_is_point_solid:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_point_solid**\ (\ id\: :ref:`Vector2i<class_Vector2i>`\ ) |const| :ref:`🔗<class_AStarGrid2D_method_is_point_solid>`

Trả về ``true`` nếu một point bị vô hiệu hóa đối với pathfinding. Theo mặc định, tất cả point đều được bật.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_set_point_solid:

.. rst-class:: classref-method

|void| **set_point_solid**\ (\ id\: :ref:`Vector2i<class_Vector2i>`, solid\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AStarGrid2D_method_set_point_solid>`

Vô hiệu hóa hoặc bật point được chỉ định cho pathfinding. Hữu ích khi tạo chướng ngại vật. Theo mặc định, tất cả point đều được bật.

\ **Lưu ý:** Không cần gọi :ref:`update()<class_AStarGrid2D_method_update>` sau khi gọi hàm này.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_set_point_weight_scale:

.. rst-class:: classref-method

|void| **set_point_weight_scale**\ (\ id\: :ref:`Vector2i<class_Vector2i>`, weight_scale\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AStarGrid2D_method_set_point_weight_scale>`

Thiết lập ``weight_scale`` cho point có ``id`` đã cho. ``weight_scale`` được nhân với kết quả của :ref:`_compute_cost()<class_AStarGrid2D_private_method__compute_cost>` khi xác định tổng chi phí di chuyển qua một segment từ point lân cận đến point này.

\ **Lưu ý:** Không cần gọi :ref:`update()<class_AStarGrid2D_method_update>` sau khi gọi hàm này.

.. rst-class:: classref-item-separator

----

.. _class_AStarGrid2D_method_update:

.. rst-class:: classref-method

|void| **update**\ (\ ) :ref:`🔗<class_AStarGrid2D_method_update>`

Cập nhật trạng thái nội bộ của grid theo các tham số để chuẩn bị cho việc tìm kiếm đường đi. Cần gọi hàm này nếu các tham số như :ref:`region<class_AStarGrid2D_property_region>`, :ref:`cell_size<class_AStarGrid2D_property_cell_size>` hoặc :ref:`offset<class_AStarGrid2D_property_offset>` bị thay đổi. :ref:`is_dirty()<class_AStarGrid2D_method_is_dirty>` sẽ trả về ``true`` nếu xảy ra trường hợp này và cần gọi hàm này.

\ **Lưu ý:** Tất cả dữ liệu của point (độ rắn và weight scale) sẽ bị xóa.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
