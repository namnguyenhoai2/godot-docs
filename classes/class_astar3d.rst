:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AStar3D.xml.

.. _class_AStar3D:

AStar3D
=======

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một triển khai của A\* để tìm đường đi ngắn nhất giữa hai đỉnh trên một đồ thị liên thông trong không gian 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

A\* (A star) là một thuật toán máy tính được sử dụng trong pathfinding và duyệt đồ thị, tức quá trình vạch ra các đường đi ngắn giữa các đỉnh (điểm), đi qua một tập cạnh (đoạn) cho trước. Thuật toán này được sử dụng rộng rãi nhờ hiệu năng và độ chính xác. Triển khai A\* của Godot sử dụng các điểm trong không gian 3D và khoảng cách Euclidean theo mặc định.

Bạn phải thêm các điểm theo cách thủ công bằng :ref:`add_point()<class_AStar3D_method_add_point>` và tạo các đoạn theo cách thủ công bằng :ref:`connect_points()<class_AStar3D_method_connect_points>`. Sau khi hoàn tất, bạn có thể kiểm tra xem có đường đi giữa hai điểm bằng hàm :ref:`are_points_connected()<class_AStar3D_method_are_points_connected>`, lấy một đường đi chứa các chỉ số bằng :ref:`get_id_path()<class_AStar3D_method_get_id_path>`, hoặc một đường đi chứa các tọa độ thực bằng :ref:`get_point_path()<class_AStar3D_method_get_point_path>`.

Bạn cũng có thể sử dụng khoảng cách không phải Euclidean. Để làm vậy, hãy tạo một script mở rộng **AStar3D** và override các phương thức :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` và :ref:`_estimate_cost()<class_AStar3D_private_method__estimate_cost>`. Cả hai phương thức đều phải nhận hai point ID và trả về khoảng cách giữa các điểm tương ứng.

\ **Ví dụ:** Sử dụng khoảng cách Manhattan thay vì khoảng cách Euclidean:


.. tabs::

 .. code-tab:: gdscript

    class_name MyAStar3D
    extends AStar3D

    func _compute_cost(u, v):
        var u_pos = get_point_position(u)
        var v_pos = get_point_position(v)
        return abs(u_pos.x - v_pos.x) + abs(u_pos.y - v_pos.y) + abs(u_pos.z - v_pos.z)

    func _estimate_cost(u, v):
        var u_pos = get_point_position(u)
        var v_pos = get_point_position(v)
        return abs(u_pos.x - v_pos.x) + abs(u_pos.y - v_pos.y) + abs(u_pos.z - v_pos.z)

 .. code-tab:: csharp

    using Godot;

    [GlobalClass]
    public partial class MyAStar3D : AStar3D
    {
        public override float _ComputeCost(long fromId, long toId)
        {
            Vector3 fromPoint = GetPointPosition(fromId);
            Vector3 toPoint = GetPointPosition(toId);

            return Mathf.Abs(fromPoint.X - toPoint.X) + Mathf.Abs(fromPoint.Y - toPoint.Y) + Mathf.Abs(fromPoint.Z - toPoint.Z);
        }

        public override float _EstimateCost(long fromId, long toId)
        {
            Vector3 fromPoint = GetPointPosition(fromId);
            Vector3 toPoint = GetPointPosition(toId);
            return Mathf.Abs(fromPoint.X - toPoint.X) + Mathf.Abs(fromPoint.Y - toPoint.Y) + Mathf.Abs(fromPoint.Z - toPoint.Z);
        }
    }



\ :ref:`_estimate_cost()<class_AStar3D_private_method__estimate_cost>` phải trả về cận dưới của khoảng cách, tức là ``_estimate_cost(u, v) <= _compute_cost(u, v)``. Điều này đóng vai trò gợi ý cho thuật toán vì :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` tùy chỉnh có thể yêu cầu nhiều phép tính. Nếu không phải như vậy, hãy để :ref:`_estimate_cost()<class_AStar3D_private_method__estimate_cost>` trả về cùng giá trị với :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` để cung cấp cho thuật toán thông tin chính xác nhất.

If the default :ref:`_estimate_cost()<class_AStar3D_private_method__estimate_cost>` and :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` methods are used, or if the supplied :ref:`_estimate_cost()<class_AStar3D_private_method__estimate_cost>` method returns a lower bound of the cost, then the paths returned by A\* will be the lowest-cost paths. Here, the cost of a path equals the sum of the :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` results of all segments in the path multiplied by the ``weight_scale``\ s of the endpoints of the respective segments. If the default methods are used and the ``weight_scale``\ s of all points are set to ``1.0``, then this equals the sum of Euclidean distances of all segments in the path.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`neighbor_filter_enabled<class_AStar3D_property_neighbor_filter_enabled>` | ``false`` |
   +-------------------------+--------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`_compute_cost<class_AStar3D_private_method__compute_cost>`\ (\ from_id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`\ ) |virtual| |const|                                        |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`_estimate_cost<class_AStar3D_private_method__estimate_cost>`\ (\ from_id\: :ref:`int<class_int>`, end_id\: :ref:`int<class_int>`\ ) |virtual| |const|                                     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`_filter_neighbor<class_AStar3D_private_method__filter_neighbor>`\ (\ from_id\: :ref:`int<class_int>`, neighbor_id\: :ref:`int<class_int>`\ ) |virtual| |const|                            |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_point<class_AStar3D_method_add_point>`\ (\ id\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`, weight_scale\: :ref:`float<class_float>` = 1.0\ )                    |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`are_points_connected<class_AStar3D_method_are_points_connected>`\ (\ id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, bidirectional\: :ref:`bool<class_bool>` = true\ ) |const| |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear<class_AStar3D_method_clear>`\ (\ )                                                                                                                                                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`connect_points<class_AStar3D_method_connect_points>`\ (\ id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, bidirectional\: :ref:`bool<class_bool>` = true\ )                     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`disconnect_points<class_AStar3D_method_disconnect_points>`\ (\ id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, bidirectional\: :ref:`bool<class_bool>` = true\ )               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_available_point_id<class_AStar3D_method_get_available_point_id>`\ (\ ) |const|                                                                                                        |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_closest_point<class_AStar3D_method_get_closest_point>`\ (\ to_position\: :ref:`Vector3<class_Vector3>`, include_disabled\: :ref:`bool<class_bool>` = false\ ) |const|                 |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`get_closest_position_in_segment<class_AStar3D_method_get_closest_position_in_segment>`\ (\ to_position\: :ref:`Vector3<class_Vector3>`\ ) |const|                                         |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt64Array<class_PackedInt64Array>`     | :ref:`get_id_path<class_AStar3D_method_get_id_path>`\ (\ from_id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ )                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_point_capacity<class_AStar3D_method_get_point_capacity>`\ (\ ) |const|                                                                                                                |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt64Array<class_PackedInt64Array>`     | :ref:`get_point_connections<class_AStar3D_method_get_point_connections>`\ (\ id\: :ref:`int<class_int>`\ )                                                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                               | :ref:`get_point_count<class_AStar3D_method_get_point_count>`\ (\ ) |const|                                                                                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt64Array<class_PackedInt64Array>`     | :ref:`get_point_ids<class_AStar3D_method_get_point_ids>`\ (\ )                                                                                                                                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_point_path<class_AStar3D_method_get_point_path>`\ (\ from_id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ )          |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`get_point_position<class_AStar3D_method_get_point_position>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                                    |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_point_weight_scale<class_AStar3D_method_get_point_weight_scale>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                            |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`has_point<class_AStar3D_method_has_point>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`is_point_disabled<class_AStar3D_method_is_point_disabled>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                                      |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_point<class_AStar3D_method_remove_point>`\ (\ id\: :ref:`int<class_int>`\ )                                                                                                        |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`reserve_space<class_AStar3D_method_reserve_space>`\ (\ num_nodes\: :ref:`int<class_int>`\ )                                                                                               |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_disabled<class_AStar3D_method_set_point_disabled>`\ (\ id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>` = true\ )                                                 |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_position<class_AStar3D_method_set_point_position>`\ (\ id\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ )                                                  |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_weight_scale<class_AStar3D_method_set_point_weight_scale>`\ (\ id\: :ref:`int<class_int>`, weight_scale\: :ref:`float<class_float>`\ )                                          |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AStar3D_property_neighbor_filter_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **neighbor_filter_enabled** = ``false`` :ref:`🔗<class_AStar3D_property_neighbor_filter_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_neighbor_filter_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_neighbor_filter_enabled**\ (\ )

Nếu ``true`` bật chức năng lọc các neighbor thông qua :ref:`_filter_neighbor()<class_AStar3D_private_method__filter_neighbor>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AStar3D_private_method__compute_cost:

.. rst-class:: classref-method

:ref:`float<class_float>` **_compute_cost**\ (\ from_id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_AStar3D_private_method__compute_cost>`

Được gọi khi tính toán chi phí giữa hai điểm được kết nối.

Lưu ý rằng hàm này bị ẩn trong class **AStar3D** mặc định.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_private_method__estimate_cost:

.. rst-class:: classref-method

:ref:`float<class_float>` **_estimate_cost**\ (\ from_id\: :ref:`int<class_int>`, end_id\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_AStar3D_private_method__estimate_cost>`

Được gọi khi ước tính chi phí giữa một điểm và điểm kết thúc của đường đi.

Lưu ý rằng hàm này bị ẩn trong class **AStar3D** mặc định.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_private_method__filter_neighbor:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_filter_neighbor**\ (\ from_id\: :ref:`int<class_int>`, neighbor_id\: :ref:`int<class_int>`\ ) |virtual| |const| :ref:`🔗<class_AStar3D_private_method__filter_neighbor>`

Được gọi khi điểm lân cận bắt đầu được xử lý và nếu :ref:`neighbor_filter_enabled<class_AStar3D_property_neighbor_filter_enabled>` là ``true``. Nếu trả về ``true``, điểm đó sẽ không được xử lý.

Lưu ý rằng hàm này bị ẩn trong class **AStar3D** mặc định.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_add_point:

.. rst-class:: classref-method

|void| **add_point**\ (\ id\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`, weight_scale\: :ref:`float<class_float>` = 1.0\ ) :ref:`🔗<class_AStar3D_method_add_point>`

Thêm một điểm mới tại vị trí đã cho với mã định danh đã cho. ``id`` phải bằng 0 hoặc lớn hơn, và ``weight_scale`` phải bằng 0.0 hoặc lớn hơn.

The ``weight_scale`` is multiplied by the result of :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` when determining the overall cost of traveling across a segment from a neighboring point to this point. Thus, all else being equal, the algorithm prefers points with lower ``weight_scale``\ s to form a path.


.. tabs::

 .. code-tab:: gdscript

    var astar = AStar3D.new()
    astar.add_point(1, Vector3(1, 0, 0), 4) # Thêm điểm (1, 0, 0) với weight_scale bằng 4 và id bằng 1

 .. code-tab:: csharp

    var astar = new AStar3D();
    astar.AddPoint(1, new Vector3(1, 0, 0), 4); // Thêm điểm (1, 0, 0) với weight_scale bằng 4 và id bằng 1



Nếu đã tồn tại một điểm với ``id`` đã cho, vị trí và weight scale của điểm đó sẽ được cập nhật thành các giá trị đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_are_points_connected:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **are_points_connected**\ (\ id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, bidirectional\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_AStar3D_method_are_points_connected>`

Trả về việc hai điểm đã cho có được kết nối trực tiếp bằng một đoạn hay không. Nếu ``bidirectional`` là ``false``, trả về việc có thể di chuyển từ ``id`` đến ``to_id`` qua đoạn này hay không.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_clear:

.. rst-class:: classref-method

|void| **clear**\ (\ ) :ref:`🔗<class_AStar3D_method_clear>`

Xóa tất cả các điểm và đoạn.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_connect_points:

.. rst-class:: classref-method

|void| **connect_points**\ (\ id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, bidirectional\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AStar3D_method_connect_points>`

Tạo một đoạn giữa các điểm đã cho. Nếu ``bidirectional`` là ``false``, chỉ cho phép di chuyển từ ``id`` đến ``to_id``, không cho phép di chuyển theo hướng ngược lại.


.. tabs::

 .. code-tab:: gdscript

    var astar = AStar3D.new()
    astar.add_point(1, Vector3(1, 1, 0))
    astar.add_point(2, Vector3(0, 5, 0))
    astar.connect_points(1, 2, false)

 .. code-tab:: csharp

    var astar = new AStar3D();
    astar.AddPoint(1, new Vector3(1, 1, 0));
    astar.AddPoint(2, new Vector3(0, 5, 0));
    astar.ConnectPoints(1, 2, false);



.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_disconnect_points:

.. rst-class:: classref-method

|void| **disconnect_points**\ (\ id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, bidirectional\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AStar3D_method_disconnect_points>`

Xóa đoạn giữa các điểm đã cho. Nếu ``bidirectional`` là ``false``, chỉ ngăn việc di chuyển từ ``id`` đến ``to_id``, và một đoạn một chiều có thể vẫn còn.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_available_point_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_available_point_id**\ (\ ) |const| :ref:`🔗<class_AStar3D_method_get_available_point_id>`

Trả về point ID khả dụng tiếp theo chưa được gắn với điểm nào.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_closest_point:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_closest_point**\ (\ to_position\: :ref:`Vector3<class_Vector3>`, include_disabled\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_AStar3D_method_get_closest_point>`

Trả về ID của điểm gần nhất với ``to_position``, tùy chọn tính cả các điểm bị vô hiệu hóa. Trả về ``-1`` nếu không có điểm nào trong points pool.

\ **Lưu ý:** Nếu có nhiều điểm cùng gần ``to_position`` nhất, điểm có ID nhỏ nhất sẽ được trả về, đảm bảo kết quả deterministic.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_closest_position_in_segment:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_closest_position_in_segment**\ (\ to_position\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_AStar3D_method_get_closest_position_in_segment>`

Trả về vị trí gần nhất với ``to_position`` nằm bên trong một đoạn giữa hai điểm được kết nối.


.. tabs::

 .. code-tab:: gdscript

    var astar = AStar3D.new()
    astar.add_point(1, Vector3(0, 0, 0))
    astar.add_point(2, Vector3(0, 5, 0))
    astar.connect_points(1, 2)
    var res = astar.get_closest_position_in_segment(Vector3(3, 3, 0)) # Trả về (0, 3, 0)

 .. code-tab:: csharp

    var astar = new AStar3D();
    astar.AddPoint(1, new Vector3(0, 0, 0));
    astar.AddPoint(2, new Vector3(0, 5, 0));
    astar.ConnectPoints(1, 2);
    Vector3 res = astar.GetClosestPositionInSegment(new Vector3(3, 3, 0)); // Trả về (0, 3, 0)



Kết quả nằm trên đoạn đi từ ``y = 0`` đến ``y = 5``. Đây là vị trí gần điểm đã cho nhất trên đoạn.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_id_path:

.. rst-class:: classref-method

:ref:`PackedInt64Array<class_PackedInt64Array>` **get_id_path**\ (\ from_id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AStar3D_method_get_id_path>`

Trả về một mảng chứa ID của các điểm tạo thành đường đi được AStar3D tìm thấy giữa hai điểm đã cho. Mảng được sắp xếp từ điểm bắt đầu đến điểm kết thúc của đường đi.

Nếu điểm ``from_id`` bị vô hiệu hóa, trả về một mảng rỗng (ngay cả khi ``from_id == to_id``).

Nếu điểm ``from_id`` không bị vô hiệu hóa, không có đường đi hợp lệ đến đích, và ``allow_partial_path`` là ``true``, trả về đường đi đến điểm gần đích nhất có thể tiếp cận.

\ **Lưu ý:** Khi ``allow_partial_path`` là ``true`` và ``to_id`` bị vô hiệu hóa, quá trình tìm kiếm có thể mất thời gian lâu bất thường để hoàn tất.


.. tabs::

 .. code-tab:: gdscript

    var astar = AStar3D.new()
    astar.add_point(1, Vector3(0, 0, 0))
    astar.add_point(2, Vector3(0, 1, 0), 1) # Trọng số mặc định là 1
    astar.add_point(3, Vector3(1, 1, 0))
    astar.add_point(4, Vector3(2, 0, 0))

    astar.connect_points(1, 2, false)
    astar.connect_points(2, 3, false)
    astar.connect_points(4, 3, false)
    astar.connect_points(1, 4, false)

    var res = astar.get_id_path(1, 3) # Trả về [1, 2, 3]

 .. code-tab:: csharp

    var astar = new AStar3D();
    astar.AddPoint(1, new Vector3(0, 0, 0));
    astar.AddPoint(2, new Vector3(0, 1, 0), 1); // Trọng số mặc định là 1
    astar.AddPoint(3, new Vector3(1, 1, 0));
    astar.AddPoint(4, new Vector3(2, 0, 0));
    astar.ConnectPoints(1, 2, false);
    astar.ConnectPoints(2, 3, false);
    astar.ConnectPoints(4, 3, false);
    astar.ConnectPoints(1, 4, false);
    long[] res = astar.GetIdPath(1, 3); // Trả về [1, 2, 3]



Nếu bạn thay đổi trọng số của điểm thứ 2 thành 3, kết quả khi đó sẽ là ``[1, 4, 3]``, vì mặc dù khoảng cách dài hơn, việc đi qua điểm 4 giờ đây "dễ dàng" hơn so với đi qua điểm 2.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_capacity:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_point_capacity**\ (\ ) |const| :ref:`🔗<class_AStar3D_method_get_point_capacity>`

Trả về capacity của cấu trúc hỗ trợ points, hữu ích khi dùng cùng với :ref:`reserve_space()<class_AStar3D_method_reserve_space>`.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_connections:

.. rst-class:: classref-method

:ref:`PackedInt64Array<class_PackedInt64Array>` **get_point_connections**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AStar3D_method_get_point_connections>`

Trả về một mảng chứa ID của các điểm tạo thành kết nối với điểm đã cho.


.. tabs::

 .. code-tab:: gdscript

    var astar = AStar3D.new()
    astar.add_point(1, Vector3(0, 0, 0))
    astar.add_point(2, Vector3(0, 1, 0))
    astar.add_point(3, Vector3(1, 1, 0))
    astar.add_point(4, Vector3(2, 0, 0))

    astar.connect_points(1, 2, true)
    astar.connect_points(1, 3, true)

    var neighbors = astar.get_point_connections(1) # Trả về [2, 3]

 .. code-tab:: csharp

    var astar = new AStar3D();
    astar.AddPoint(1, new Vector3(0, 0, 0));
    astar.AddPoint(2, new Vector3(0, 1, 0));
    astar.AddPoint(3, new Vector3(1, 1, 0));
    astar.AddPoint(4, new Vector3(2, 0, 0));
    astar.ConnectPoints(1, 2, true);
    astar.ConnectPoints(1, 3, true);

    long[] neighbors = astar.GetPointConnections(1); // Trả về [2, 3]



.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_point_count**\ (\ ) |const| :ref:`🔗<class_AStar3D_method_get_point_count>`

Trả về số điểm hiện có trong points pool.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_ids:

.. rst-class:: classref-method

:ref:`PackedInt64Array<class_PackedInt64Array>` **get_point_ids**\ (\ ) :ref:`🔗<class_AStar3D_method_get_point_ids>`

Trả về một mảng gồm tất cả point ID.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_path:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_point_path**\ (\ from_id\: :ref:`int<class_int>`, to_id\: :ref:`int<class_int>`, allow_partial_path\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_AStar3D_method_get_point_path>`

Trả về một mảng chứa các điểm nằm trên đường đi được AStar3D tìm thấy giữa hai điểm đã cho. Mảng được sắp xếp từ điểm bắt đầu đến điểm kết thúc của đường đi.

Nếu điểm ``from_id`` bị vô hiệu hóa, trả về một mảng rỗng (ngay cả khi ``from_id == to_id``).

Nếu điểm ``from_id`` không bị vô hiệu hóa, không có đường đi hợp lệ đến đích, và ``allow_partial_path`` là ``true``, trả về đường đi đến điểm gần đích nhất có thể tiếp cận.

\ **Lưu ý:** Phương thức này không thread-safe; chỉ có thể được sử dụng từ một :ref:`Thread<class_Thread>` duy nhất tại một thời điểm. Hãy cân nhắc sử dụng :ref:`Mutex<class_Mutex>` để đảm bảo quyền truy cập độc quyền của một thread, nhằm tránh race condition.

Ngoài ra, khi ``allow_partial_path`` là ``true`` và ``to_id`` bị vô hiệu hóa, quá trình tìm kiếm có thể mất thời gian lâu bất thường để hoàn tất.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_point_position**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AStar3D_method_get_point_position>`

Trả về vị trí của điểm được liên kết với ``id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_get_point_weight_scale:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_point_weight_scale**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AStar3D_method_get_point_weight_scale>`

Trả về weight scale của điểm được liên kết với ``id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_has_point:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_point**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AStar3D_method_has_point>`

Trả về việc có tồn tại điểm được liên kết với ``id`` đã cho hay không.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_is_point_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_point_disabled**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AStar3D_method_is_point_disabled>`

Trả về việc một điểm có bị vô hiệu hóa cho pathfinding hay không. Theo mặc định, tất cả các điểm đều được bật.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_remove_point:

.. rst-class:: classref-method

|void| **remove_point**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AStar3D_method_remove_point>`

Xóa điểm được liên kết với ``id`` đã cho khỏi points pool.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_reserve_space:

.. rst-class:: classref-method

|void| **reserve_space**\ (\ num_nodes\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AStar3D_method_reserve_space>`

Dành trước không gian nội bộ cho ``num_nodes`` điểm. Hữu ích nếu bạn thêm cùng lúc một số lượng lớn điểm đã biết trước, chẳng hạn như các điểm trên một lưới.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_set_point_disabled:

.. rst-class:: classref-method

|void| **set_point_disabled**\ (\ id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_AStar3D_method_set_point_disabled>`

Vô hiệu hóa hoặc bật điểm được chỉ định cho việc tìm đường. Hữu ích khi tạo một chướng ngại vật tạm thời.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_set_point_position:

.. rst-class:: classref-method

|void| **set_point_position**\ (\ id\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_AStar3D_method_set_point_position>`

Thiết lập ``position`` cho điểm có ``id`` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_AStar3D_method_set_point_weight_scale:

.. rst-class:: classref-method

|void| **set_point_weight_scale**\ (\ id\: :ref:`int<class_int>`, weight_scale\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AStar3D_method_set_point_weight_scale>`

Thiết lập ``weight_scale`` cho điểm có ``id`` được cung cấp. ``weight_scale`` được nhân với kết quả của :ref:`_compute_cost()<class_AStar3D_private_method__compute_cost>` khi xác định tổng chi phí di chuyển qua một đoạn từ điểm lân cận đến điểm này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
