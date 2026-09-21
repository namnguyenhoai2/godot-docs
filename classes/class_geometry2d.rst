:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Geometry2D.xml.

.. _class_Geometry2D:

Geometry2D
==========

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp các phương thức cho một số thao tác hình học 2D phổ biến.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp một tập hợp các hàm trợ giúp để tạo hình dạng hình học, tính giao điểm giữa các hình dạng và xử lý nhiều thao tác hình học khác trong 2D.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector2i<class_Vector2i>`\]                     | :ref:`bresenham_line<class_Geometry2D_method_bresenham_line>`\ (\ from\: :ref:`Vector2i<class_Vector2i>`, to\: :ref:`Vector2i<class_Vector2i>`\ )                                                                                                                                                           |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`clip_polygons<class_Geometry2D_method_clip_polygons>`\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                         |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`clip_polyline_with_polygon<class_Geometry2D_method_clip_polyline_with_polygon>`\ (\ polyline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                  |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`                              | :ref:`convex_hull<class_Geometry2D_method_convex_hull>`\ (\ points\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                                                                                 |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`decompose_polygon_in_convex<class_Geometry2D_method_decompose_polygon_in_convex>`\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                                                |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`exclude_polygons<class_Geometry2D_method_exclude_polygons>`\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                   |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                    | :ref:`get_closest_point_to_segment<class_Geometry2D_method_get_closest_point_to_segment>`\ (\ point\: :ref:`Vector2<class_Vector2>`, s1\: :ref:`Vector2<class_Vector2>`, s2\: :ref:`Vector2<class_Vector2>`\ )                                                                                              |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                                    | :ref:`get_closest_point_to_segment_uncapped<class_Geometry2D_method_get_closest_point_to_segment_uncapped>`\ (\ point\: :ref:`Vector2<class_Vector2>`, s1\: :ref:`Vector2<class_Vector2>`, s2\: :ref:`Vector2<class_Vector2>`\ )                                                                            |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`                              | :ref:`get_closest_points_between_segments<class_Geometry2D_method_get_closest_points_between_segments>`\ (\ p1\: :ref:`Vector2<class_Vector2>`, q1\: :ref:`Vector2<class_Vector2>`, p2\: :ref:`Vector2<class_Vector2>`, q2\: :ref:`Vector2<class_Vector2>`\ )                                               |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`intersect_polygons<class_Geometry2D_method_intersect_polygons>`\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                               |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`intersect_polyline_with_polygon<class_Geometry2D_method_intersect_polyline_with_polygon>`\ (\ polyline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                        |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`is_point_in_circle<class_Geometry2D_method_is_point_in_circle>`\ (\ point\: :ref:`Vector2<class_Vector2>`, circle_position\: :ref:`Vector2<class_Vector2>`, circle_radius\: :ref:`float<class_float>`\ )                                                                                              |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`is_point_in_polygon<class_Geometry2D_method_is_point_in_polygon>`\ (\ point\: :ref:`Vector2<class_Vector2>`, polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                         |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`is_polygon_clockwise<class_Geometry2D_method_is_polygon_clockwise>`\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                                                              |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                                    | :ref:`line_intersects_line<class_Geometry2D_method_line_intersects_line>`\ (\ from_a\: :ref:`Vector2<class_Vector2>`, dir_a\: :ref:`Vector2<class_Vector2>`, from_b\: :ref:`Vector2<class_Vector2>`, dir_b\: :ref:`Vector2<class_Vector2>`\ )                                                               |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                                              | :ref:`make_atlas<class_Geometry2D_method_make_atlas>`\ (\ sizes\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                                                                                    |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`merge_polygons<class_Geometry2D_method_merge_polygons>`\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                       |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`offset_polygon<class_Geometry2D_method_offset_polygon>`\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`, delta\: :ref:`float<class_float>`, join_type\: :ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` = 0\ )                                                                    |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] | :ref:`offset_polyline<class_Geometry2D_method_offset_polyline>`\ (\ polyline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, delta\: :ref:`float<class_float>`, join_type\: :ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` = 0, end_type\: :ref:`PolyEndType<enum_Geometry2D_PolyEndType>` = 3\ ) |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                          | :ref:`point_is_inside_triangle<class_Geometry2D_method_point_is_inside_triangle>`\ (\ point\: :ref:`Vector2<class_Vector2>`, a\: :ref:`Vector2<class_Vector2>`, b\: :ref:`Vector2<class_Vector2>`, c\: :ref:`Vector2<class_Vector2>`\ ) |const|                                                             |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                        | :ref:`segment_intersects_circle<class_Geometry2D_method_segment_intersects_circle>`\ (\ segment_from\: :ref:`Vector2<class_Vector2>`, segment_to\: :ref:`Vector2<class_Vector2>`, circle_position\: :ref:`Vector2<class_Vector2>`, circle_radius\: :ref:`float<class_float>`\ )                             |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                                    | :ref:`segment_intersects_segment<class_Geometry2D_method_segment_intersects_segment>`\ (\ from_a\: :ref:`Vector2<class_Vector2>`, to_a\: :ref:`Vector2<class_Vector2>`, from_b\: :ref:`Vector2<class_Vector2>`, to_b\: :ref:`Vector2<class_Vector2>`\ )                                                     |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`                                  | :ref:`triangulate_delaunay<class_Geometry2D_method_triangulate_delaunay>`\ (\ points\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                                                               |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`                                  | :ref:`triangulate_polygon<class_Geometry2D_method_triangulate_polygon>`\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ )                                                                                                                                                                |
   +----------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Geometry2D_PolyBooleanOperation:

.. rst-class:: classref-enumeration

enum **PolyBooleanOperation**: :ref:`🔗<enum_Geometry2D_PolyBooleanOperation>`

.. _class_Geometry2D_constant_OPERATION_UNION:

.. rst-class:: classref-enumeration-constant

:ref:`PolyBooleanOperation<enum_Geometry2D_PolyBooleanOperation>` **OPERATION_UNION** = ``0``

Tạo các vùng mà polygon subject hoặc polygon clip (hoặc cả hai) được tô đầy.

.. _class_Geometry2D_constant_OPERATION_DIFFERENCE:

.. rst-class:: classref-enumeration-constant

:ref:`PolyBooleanOperation<enum_Geometry2D_PolyBooleanOperation>` **OPERATION_DIFFERENCE** = ``1``

Tạo các vùng mà polygon subject được tô đầy, ngoại trừ những nơi polygon clip được tô đầy.

.. _class_Geometry2D_constant_OPERATION_INTERSECTION:

.. rst-class:: classref-enumeration-constant

:ref:`PolyBooleanOperation<enum_Geometry2D_PolyBooleanOperation>` **OPERATION_INTERSECTION** = ``2``

Tạo các vùng mà cả polygon subject và polygon clip đều được tô đầy.

.. _class_Geometry2D_constant_OPERATION_XOR:

.. rst-class:: classref-enumeration-constant

:ref:`PolyBooleanOperation<enum_Geometry2D_PolyBooleanOperation>` **OPERATION_XOR** = ``3``

Tạo các vùng mà polygon subject hoặc polygon clip được tô đầy, nhưng không phải những nơi cả hai đều được tô đầy.

.. rst-class:: classref-item-separator

----

.. _enum_Geometry2D_PolyJoinType:

.. rst-class:: classref-enumeration

enum **PolyJoinType**: :ref:`🔗<enum_Geometry2D_PolyJoinType>`

.. _class_Geometry2D_constant_JOIN_SQUARE:

.. rst-class:: classref-enumeration-constant

:ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` **JOIN_SQUARE** = ``0``

Việc vuông hóa được áp dụng đồng nhất tại tất cả các điểm nối cạnh lồi ở ``1 * delta``.

.. _class_Geometry2D_constant_JOIN_ROUND:

.. rst-class:: classref-enumeration-constant

:ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` **JOIN_ROUND** = ``1``

Mặc dù các path được làm phẳng không thể bao sát một cung tròn hoàn hảo, chúng được xấp xỉ bằng một chuỗi các dây cung.

.. _class_Geometry2D_constant_JOIN_MITER:

.. rst-class:: classref-enumeration-constant

:ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` **JOIN_MITER** = ``2``

Có một giới hạn cần thiết đối với các điểm nối miter, vì việc offset các cạnh nối với nhau ở các góc rất nhọn sẽ tạo ra những "spike" quá dài và hẹp. Với mỗi điểm nối cạnh, khi việc offset miter vượt quá khoảng cách tối đa đó, kiểu nối "square" sẽ được áp dụng.

.. rst-class:: classref-item-separator

----

.. _enum_Geometry2D_PolyEndType:

.. rst-class:: classref-enumeration

enum **PolyEndType**: :ref:`🔗<enum_Geometry2D_PolyEndType>`

.. _class_Geometry2D_constant_END_POLYGON:

.. rst-class:: classref-enumeration-constant

:ref:`PolyEndType<enum_Geometry2D_PolyEndType>` **END_POLYGON** = ``0``

Các điểm cuối được nối bằng giá trị :ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` và path được tô đầy như một polygon.

.. _class_Geometry2D_constant_END_JOINED:

.. rst-class:: classref-enumeration-constant

:ref:`PolyEndType<enum_Geometry2D_PolyEndType>` **END_JOINED** = ``1``

Các điểm cuối được nối bằng giá trị :ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` và path được tô đầy như một polyline.

.. _class_Geometry2D_constant_END_BUTT:

.. rst-class:: classref-enumeration-constant

:ref:`PolyEndType<enum_Geometry2D_PolyEndType>` **END_BUTT** = ``2``

Các điểm cuối được cắt vuông, không kéo dài.

.. _class_Geometry2D_constant_END_SQUARE:

.. rst-class:: classref-enumeration-constant

:ref:`PolyEndType<enum_Geometry2D_PolyEndType>` **END_SQUARE** = ``3``

Các điểm cuối được cắt vuông và kéo dài thêm ``delta`` đơn vị.

.. _class_Geometry2D_constant_END_ROUND:

.. rst-class:: classref-enumeration-constant

:ref:`PolyEndType<enum_Geometry2D_PolyEndType>` **END_ROUND** = ``4``

Các điểm cuối được bo tròn và kéo dài thêm ``delta`` đơn vị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_Geometry2D_method_bresenham_line:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector2i<class_Vector2i>`\] **bresenham_line**\ (\ from\: :ref:`Vector2i<class_Vector2i>`, to\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_Geometry2D_method_bresenham_line>`

Trả về `Bresenham line <https://en.wikipedia.org/wiki/Bresenham%27s_line_algorithm>`__ giữa các điểm ``from`` và ``to``. Đường thẳng Bresenham là một chuỗi pixel dùng để vẽ một đường thẳng và luôn dày 1 pixel trên mỗi hàng và cột của bản vẽ (không hơn, không kém).

Mã ví dụ để vẽ một đường thẳng giữa hai node :ref:`Marker2D<class_Marker2D>` bằng một chuỗi lệnh gọi :ref:`CanvasItem.draw_rect()<class_CanvasItem_method_draw_rect>`:

::

    func _draw():
        for pixel in Geometry2D.bresenham_line($MarkerA.position, $MarkerB.position):
            draw_rect(Rect2(pixel, Vector2.ONE), Color.WHITE)

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_clip_polygons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **clip_polygons**\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_clip_polygons>`

Clip ``polygon_a`` với ``polygon_b`` và trả về một mảng các polygon đã clip. Thao tác này thực hiện :ref:`OPERATION_DIFFERENCE<class_Geometry2D_constant_OPERATION_DIFFERENCE>` giữa các polygon. Trả về một mảng rỗng nếu ``polygon_b`` chồng lấp hoàn toàn ``polygon_a``.

Nếu ``polygon_b`` được bao bởi ``polygon_a``, trả về một polygon bên ngoài (biên) và polygon bên trong (lỗ), có thể phân biệt bằng cách gọi :ref:`is_polygon_clockwise()<class_Geometry2D_method_is_polygon_clockwise>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_clip_polyline_with_polygon:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **clip_polyline_with_polygon**\ (\ polyline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_clip_polyline_with_polygon>`

Clip ``polyline`` với ``polygon`` và trả về một mảng các polyline đã clip. Thao tác này thực hiện :ref:`OPERATION_DIFFERENCE<class_Geometry2D_constant_OPERATION_DIFFERENCE>` giữa polyline và polygon. Có thể xem thao tác này như việc cắt một đường bằng một hình kín.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_convex_hull:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **convex_hull**\ (\ points\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_convex_hull>`

Với một mảng gồm các :ref:`Vector2<class_Vector2>`\ s, trả về convex hull dưới dạng danh sách các điểm theo thứ tự ngược chiều kim đồng hồ. Điểm cuối cùng giống với điểm đầu tiên.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_decompose_polygon_in_convex:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **decompose_polygon_in_convex**\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_decompose_polygon_in_convex>`

Phân rã ``polygon`` thành nhiều convex hull và trả về một mảng :ref:`PackedVector2Array<class_PackedVector2Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_exclude_polygons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **exclude_polygons**\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_exclude_polygons>`

Loại trừ lẫn nhau vùng chung được xác định bởi giao của ``polygon_a`` và ``polygon_b`` (xem :ref:`intersect_polygons()<class_Geometry2D_method_intersect_polygons>`) và trả về một mảng các polygon bị loại trừ. Thao tác này thực hiện :ref:`OPERATION_XOR<class_Geometry2D_constant_OPERATION_XOR>` giữa các polygon. Nói cách khác, trả về toàn bộ vùng giữa các polygon ngoại trừ vùng chung.

Thao tác này có thể tạo ra một polygon bên ngoài (biên) và polygon bên trong (lỗ), có thể phân biệt bằng cách gọi :ref:`is_polygon_clockwise()<class_Geometry2D_method_is_polygon_clockwise>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_get_closest_point_to_segment:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_closest_point_to_segment**\ (\ point\: :ref:`Vector2<class_Vector2>`, s1\: :ref:`Vector2<class_Vector2>`, s2\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Geometry2D_method_get_closest_point_to_segment>`

Trả về điểm 2D trên đoạn 2D (``s1``, ``s2``) gần ``point`` nhất. Điểm được trả về luôn nằm bên trong đoạn đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_get_closest_point_to_segment_uncapped:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_closest_point_to_segment_uncapped**\ (\ point\: :ref:`Vector2<class_Vector2>`, s1\: :ref:`Vector2<class_Vector2>`, s2\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Geometry2D_method_get_closest_point_to_segment_uncapped>`

Trả về điểm 2D trên đường thẳng 2D được xác định bởi (``s1``, ``s2``) gần ``point`` nhất. Điểm được trả về có thể nằm bên trong đoạn (``s1``, ``s2``) hoặc bên ngoài đoạn, tức là ở đâu đó trên đường thẳng kéo dài từ đoạn này.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_get_closest_points_between_segments:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_closest_points_between_segments**\ (\ p1\: :ref:`Vector2<class_Vector2>`, q1\: :ref:`Vector2<class_Vector2>`, p2\: :ref:`Vector2<class_Vector2>`, q2\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Geometry2D_method_get_closest_points_between_segments>`

Với hai đoạn 2D (``p1``, ``q1``) và (``p2``, ``q2``), tìm hai điểm trên hai đoạn gần nhau nhất. Trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa điểm này trên (``p1``, ``q1``) cùng với điểm tương ứng trên (``p2``, ``q2``).

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_intersect_polygons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **intersect_polygons**\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_intersect_polygons>`

Tìm giao của ``polygon_a`` với ``polygon_b`` và trả về một mảng các polygon giao nhau. Thao tác này thực hiện :ref:`OPERATION_INTERSECTION<class_Geometry2D_constant_OPERATION_INTERSECTION>` giữa các polygon. Nói cách khác, trả về vùng chung của các polygon. Trả về một mảng rỗng nếu không có giao điểm.

Thao tác này có thể tạo ra một polygon bên ngoài (biên) và polygon bên trong (lỗ), có thể phân biệt bằng cách gọi :ref:`is_polygon_clockwise()<class_Geometry2D_method_is_polygon_clockwise>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_intersect_polyline_with_polygon:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **intersect_polyline_with_polygon**\ (\ polyline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_intersect_polyline_with_polygon>`

Tìm giao của ``polyline`` với ``polygon`` và trả về một mảng các polyline giao nhau. Thao tác này thực hiện :ref:`OPERATION_INTERSECTION<class_Geometry2D_constant_OPERATION_INTERSECTION>` giữa polyline và polygon. Có thể xem thao tác này như việc chặt một đường bằng một hình kín.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_is_point_in_circle:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_point_in_circle**\ (\ point\: :ref:`Vector2<class_Vector2>`, circle_position\: :ref:`Vector2<class_Vector2>`, circle_radius\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Geometry2D_method_is_point_in_circle>`

Trả về ``true`` nếu ``point`` nằm trong hình tròn hoặc nằm chính xác *trên* biên của hình tròn; nếu không thì trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_is_point_in_polygon:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_point_in_polygon**\ (\ point\: :ref:`Vector2<class_Vector2>`, polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_is_point_in_polygon>`

Trả về ``true`` nếu ``point`` nằm trong ``polygon`` hoặc nằm chính xác *trên* biên của polygon; nếu không thì trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_is_polygon_clockwise:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_polygon_clockwise**\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_is_polygon_clockwise>`

Trả về ``true`` nếu các đỉnh của ``polygon`` được sắp xếp theo chiều kim đồng hồ; nếu không thì trả về ``false``.

\ **Lưu ý:** Giả định hệ tọa độ Descartes trong đó ``+x`` hướng sang phải và ``+y`` hướng lên trên. Nếu sử dụng tọa độ màn hình (``+y`` hướng xuống dưới), kết quả sẽ cần được đảo lại (tức là kết quả ``true`` sẽ biểu thị hướng ngược chiều kim đồng hồ).

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_line_intersects_line:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **line_intersects_line**\ (\ from_a\: :ref:`Vector2<class_Vector2>`, dir_a\: :ref:`Vector2<class_Vector2>`, from_b\: :ref:`Vector2<class_Vector2>`, dir_b\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Geometry2D_method_line_intersects_line>`

Trả về điểm giao nhau giữa hai đường thẳng (``from_a``, ``dir_a``) và (``from_b``, ``dir_b``). Trả về một :ref:`Vector2<class_Vector2>`, hoặc ``null`` nếu hai đường thẳng song song.

\ ``from`` và ``dir`` *không phải* là các đầu mút của một đoạn thẳng hoặc tia, mà là độ dốc (``dir``) và một điểm đã biết (``from``) trên đường thẳng đó. Để lấy giao điểm giữa hai đoạn thẳng, hãy sử dụng :ref:`segment_intersects_segment()<class_Geometry2D_method_segment_intersects_segment>`.


.. tabs::

 .. code-tab:: gdscript

    var from_a = Vector2.ZERO
    var dir_a = Vector2.RIGHT
    var from_b = Vector2.DOWN

    # Trả về Vector2(1, 0)
    Geometry2D.line_intersects_line(from_a, dir_a, from_b, Vector2(1, -1))
    # Trả về Vector2(-1, 0)
    Geometry2D.line_intersects_line(from_a, dir_a, from_b, Vector2(-1, -1))
    # Trả về null
    Geometry2D.line_intersects_line(from_a, dir_a, from_b, Vector2.RIGHT)

 .. code-tab:: csharp

    var fromA = Vector2.Zero;
    var dirA = Vector2.Right;
    var fromB = Vector2.Down;

    // Trả về new Vector2(1, 0)
    Geometry2D.LineIntersectsLine(fromA, dirA, fromB, new Vector2(1, -1));
    // Trả về new Vector2(-1, 0)
    Geometry2D.LineIntersectsLine(fromA, dirA, fromB, new Vector2(-1, -1));
    // Trả về null
    Geometry2D.LineIntersectsLine(fromA, dirA, fromB, Vector2.Right);



.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_make_atlas:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **make_atlas**\ (\ sizes\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_make_atlas>`

Với một mảng các :ref:`Vector2<class_Vector2>`\ s biểu diễn các tile, xây dựng một atlas. Dictionary được trả về có hai key: ``points`` là một :ref:`PackedVector2Array<class_PackedVector2Array>` chỉ định vị trí của từng tile, ``size`` chứa kích thước tổng thể của toàn bộ atlas dưới dạng :ref:`Vector2i<class_Vector2i>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_merge_polygons:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **merge_polygons**\ (\ polygon_a\: :ref:`PackedVector2Array<class_PackedVector2Array>`, polygon_b\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_merge_polygons>`

Gộp (kết hợp) ``polygon_a`` và ``polygon_b``, rồi trả về một mảng các polygon đã gộp. Thao tác này thực hiện :ref:`OPERATION_UNION<class_Geometry2D_constant_OPERATION_UNION>` giữa các polygon.

Thao tác này có thể tạo ra một polygon bên ngoài (boundary) và nhiều polygon bên trong (hole); có thể phân biệt chúng bằng cách gọi :ref:`is_polygon_clockwise()<class_Geometry2D_method_is_polygon_clockwise>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_offset_polygon:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **offset_polygon**\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`, delta\: :ref:`float<class_float>`, join_type\: :ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` = 0\ ) :ref:`🔗<class_Geometry2D_method_offset_polygon>`

Phóng to hoặc thu nhỏ ``polygon`` theo ``delta`` đơn vị (pixel). Nếu ``delta`` là số dương, polygon sẽ nở ra phía ngoài. Nếu ``delta`` là số âm, polygon sẽ co vào phía trong. Trả về một mảng các polygon vì việc phóng to/thu nhỏ có thể tạo ra nhiều polygon rời rạc. Trả về một mảng rỗng nếu ``delta`` là số âm và giá trị tuyệt đối của nó xấp xỉ vượt quá kích thước hình chữ nhật bao quanh nhỏ nhất của polygon.

Các đỉnh của mỗi polygon sẽ được bo tròn theo quy định của ``join_type``.

Thao tác này có thể tạo ra một polygon bên ngoài (boundary) và một polygon bên trong (hole); có thể phân biệt chúng bằng cách gọi :ref:`is_polygon_clockwise()<class_Geometry2D_method_is_polygon_clockwise>`.

\ **Lưu ý:** Để dịch chuyển riêng các đỉnh của polygon, hãy nhân chúng với một :ref:`Transform2D<class_Transform2D>`:


.. tabs::

 .. code-tab:: gdscript

    var polygon = PackedVector2Array([Vector2(0, 0), Vector2(100, 0), Vector2(100, 100), Vector2(0, 100)])
    var offset = Vector2(50, 50)
    polygon = Transform2D(0, offset) * polygon
    print(polygon) # In ra [(50.0, 50.0), (150.0, 50.0), (150.0, 150.0), (50.0, 150.0)]

 .. code-tab:: csharp

    Vector2[] polygon = [new Vector2(0, 0), new Vector2(100, 0), new Vector2(100, 100), new Vector2(0, 100)];
    var offset = new Vector2(50, 50);
    polygon = new Transform2D(0, offset) * polygon;
    GD.Print((Variant)polygon); // In ra [(50, 50), (150, 50), (150, 150), (50, 150)]



.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_offset_polyline:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedVector2Array<class_PackedVector2Array>`\] **offset_polyline**\ (\ polyline\: :ref:`PackedVector2Array<class_PackedVector2Array>`, delta\: :ref:`float<class_float>`, join_type\: :ref:`PolyJoinType<enum_Geometry2D_PolyJoinType>` = 0, end_type\: :ref:`PolyEndType<enum_Geometry2D_PolyEndType>` = 3\ ) :ref:`🔗<class_Geometry2D_method_offset_polyline>`

Phóng to hoặc thu nhỏ ``polyline`` theo ``delta`` đơn vị (pixel), tạo ra các polygon. Nếu ``delta`` là số dương, polyline sẽ nở ra phía ngoài. Trả về một mảng các polygon vì việc phóng to/thu nhỏ có thể tạo ra nhiều polygon rời rạc. Nếu ``delta`` là số âm, trả về một mảng rỗng.

Các đỉnh của mỗi polygon sẽ được bo tròn theo quy định của ``join_type``.

Các đầu mút của mỗi polygon sẽ được bo tròn theo quy định của ``end_type``.

Thao tác này có thể tạo ra một polygon bên ngoài (boundary) và một polygon bên trong (hole); có thể phân biệt chúng bằng cách gọi :ref:`is_polygon_clockwise()<class_Geometry2D_method_is_polygon_clockwise>`.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_point_is_inside_triangle:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **point_is_inside_triangle**\ (\ point\: :ref:`Vector2<class_Vector2>`, a\: :ref:`Vector2<class_Vector2>`, b\: :ref:`Vector2<class_Vector2>`, c\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Geometry2D_method_point_is_inside_triangle>`

Trả về liệu ``point`` có nằm trong tam giác được xác định bởi ``a``, ``b`` và ``c`` hay không.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_segment_intersects_circle:

.. rst-class:: classref-method

:ref:`float<class_float>` **segment_intersects_circle**\ (\ segment_from\: :ref:`Vector2<class_Vector2>`, segment_to\: :ref:`Vector2<class_Vector2>`, circle_position\: :ref:`Vector2<class_Vector2>`, circle_radius\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Geometry2D_method_segment_intersects_circle>`

Với đoạn thẳng 2D (``segment_from``, ``segment_to``), trả về vị trí trên đoạn thẳng (dưới dạng một số từ 0 đến 1) tại đó đoạn thẳng chạm vào đường tròn nằm tại vị trí ``circle_position`` và có bán kính ``circle_radius``. Nếu đoạn thẳng không giao với đường tròn, trả về -1 (điều này cũng xảy ra nếu đường thẳng kéo dài từ đoạn thẳng giao với đường tròn nhưng bản thân đoạn thẳng thì không).

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_segment_intersects_segment:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **segment_intersects_segment**\ (\ from_a\: :ref:`Vector2<class_Vector2>`, to_a\: :ref:`Vector2<class_Vector2>`, from_b\: :ref:`Vector2<class_Vector2>`, to_b\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Geometry2D_method_segment_intersects_segment>`

Kiểm tra xem hai đoạn thẳng có giao nhau hay không, trong đó đường thẳng ``a`` nằm giữa ``from_a`` và ``to_a``, còn đường thẳng ``b`` nằm giữa ``from_b`` và ``to_b``. Nếu hai đoạn thẳng giao nhau, điểm giao nhau được trả về dưới dạng :ref:`Vector2<class_Vector2>`. Nếu không có giao điểm, ``null`` được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_triangulate_delaunay:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **triangulate_delaunay**\ (\ points\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_triangulate_delaunay>`

Phân tam giác vùng được xác định bởi tập rời rạc các ``points`` sao cho không có điểm nào nằm bên trong đường tròn ngoại tiếp của bất kỳ tam giác nào được tạo ra. Trả về một :ref:`PackedInt32Array<class_PackedInt32Array>`, trong đó mỗi tam giác gồm ba chỉ số điểm liên tiếp trong ``points`` (tức là mảng được trả về sẽ có ``n * 3`` phần tử, với ``n`` là số tam giác được tìm thấy). Nếu không thể thực hiện phân tam giác, một :ref:`PackedInt32Array<class_PackedInt32Array>` rỗng sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Geometry2D_method_triangulate_polygon:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **triangulate_polygon**\ (\ polygon\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_Geometry2D_method_triangulate_polygon>`

Phân tam giác polygon được xác định bởi các điểm trong ``polygon``. Trả về một :ref:`PackedInt32Array<class_PackedInt32Array>`, trong đó mỗi tam giác gồm ba chỉ số điểm liên tiếp trong ``polygon`` (tức là mảng được trả về sẽ có ``n * 3`` phần tử, với ``n`` là số tam giác được tìm thấy). Các tam giác đầu ra luôn theo chiều ngược kim đồng hồ, và contour sẽ được lật nếu nó theo chiều kim đồng hồ. Nếu không thể thực hiện phân tam giác, một :ref:`PackedInt32Array<class_PackedInt32Array>` rỗng sẽ được trả về.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
