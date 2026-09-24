.. _doc_navigation_connecting_navmesh:

Kết nối các navigation mesh
===========================

Các NavigationMesh khác nhau sẽ được NavigationServer tự động hợp nhất khi ít nhất hai vị trí đỉnh của một cạnh trùng khớp hoàn toàn.

Để kết nối qua các khoảng cách tùy ý, hãy xem :ref:`doc_navigation_using_navigationlinks`.

.. image:: img/navigation_vertex_merge.png

Điều tương tự cũng đúng với nhiều tài nguyên NavigationPolygon. Miễn là các điểm đường viền của chúng trùng khớp hoàn toàn, NavigationServer sẽ hợp nhất chúng. Các đường viền NavigationPolygon phải thuộc các tài nguyên NavigationPolygon khác nhau thì mới có thể kết nối.

Các đường viền chồng lấn hoặc giao nhau trên cùng một NavigationPolygon sẽ khiến việc tạo navigation mesh thất bại. Các đường viền chồng lấn hoặc giao nhau từ những NavigationPolygon khác nhau thường sẽ khiến việc tạo kết nối cạnh của navigation region trên NavigationServer thất bại và nên tránh.

.. image:: img/navigation_vertex_merge2.png

.. warning::

    Đối với việc hợp nhất vị trí đỉnh, "chính xác" có nghĩa là chính xác tuyệt đối. Những sai số float nhỏ thường xảy ra với các mesh được import sẽ ngăn việc hợp nhất đỉnh thành công.

Ngoài ra, các navigation mesh không được hợp nhất nhưng vẫn được NavigationServer xem là **được kết nối** khi các cạnh của chúng gần song song và nằm trong khoảng cách cho phép của nhau. Khoảng cách kết nối được xác định bởi ``edge_connection_margin`` cho mỗi navigation map. Trong nhiều trường hợp, các cạnh navigation mesh không thể kết nối đúng cách khi chúng chồng lấn một phần. Để hành vi hợp nhất nhất quán, tốt nhất là luôn tránh mọi sự chồng lấn navigation mesh.

.. image:: img/navigation_edge_connection.png

Nếu navigation debug được bật và NavigationServer đang hoạt động, các kết nối navigation mesh đã thiết lập sẽ được trực quan hóa. Xem :ref:`doc_navigation_debug_tools` để biết thêm thông tin về các tùy chọn navigation debug.

``edge_connection_margin`` 2D mặc định có thể được thay đổi trong ProjectSettings tại ``navigation/2d/default_edge_connection_margin``.

``edge_connection_margin`` 3D mặc định có thể được thay đổi trong ProjectSettings tại ``navigation/3d/default_edge_connection_margin``.

Giá trị biên kết nối cạnh của bất kỳ navigation map nào cũng có thể được thay đổi trong runtime bằng NavigationServer API.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    func _ready() -> void:
        # Các giá trị biên 2D được thiết kế để hoạt động với các giá trị "pixel" 2D.
        var default_map_rid: RID = get_world_2d().get_navigation_map()
        NavigationServer2D.map_set_edge_connection_margin(default_map_rid, 50.0)

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        public override void _Ready()
        {
            // Các giá trị biên 2D được thiết kế để hoạt động với các giá trị "pixel" 2D.
            Rid defaultMapRid = GetWorld2D().NavigationMap;
            NavigationServer2D.MapSetEdgeConnectionMargin(defaultMapRid, 50.0f);
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    func _ready() -> void:
        # Các giá trị biên 3D được thiết kế để hoạt động với các giá trị đơn vị thế giới 3D.
        var default_map_rid: RID = get_world_3d().get_navigation_map()
        NavigationServer3D.map_set_edge_connection_margin(default_map_rid, 0.5)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            // Các giá trị biên 3D được thiết kế để hoạt động với các giá trị đơn vị thế giới 3D.
            Rid defaultMapRid = GetWorld3D().NavigationMap;
            NavigationServer3D.MapSetEdgeConnectionMargin(defaultMapRid, 0.5f);
        }
    }

.. note::

    Việc thay đổi giá trị biên kết nối cạnh sẽ kích hoạt quá trình cập nhật toàn bộ các kết nối navigation mesh trên NavigationServer.
