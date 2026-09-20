.. _doc_navigation_connecting_navmesh:

Kết nối các navigation mesh
===========================

Các NavigationMesh khác nhau sẽ được NavigationServer tự động hợp nhất khi ít nhất hai vị trí đỉnh của một cạnh trùng khớp hoàn toàn.

Để kết nối qua các khoảng cách tùy ý, hãy xem :ref:`doc_navigation_using_navigationlinks`.

.. image:: img/navigation_vertex_merge.png

Điều tương tự cũng áp dụng cho nhiều resource NavigationPolygon. Miễn là các điểm đường bao của chúng trùng khớp hoàn toàn, NavigationServer sẽ hợp nhất chúng. Các đường bao NavigationPolygon phải thuộc các resource NavigationPolygon khác nhau thì mới có thể kết nối.

Các đường bao chồng lấp hoặc giao nhau trên cùng một NavigationPolygon sẽ khiến quá trình tạo navigation mesh thất bại. Các đường bao chồng lấp hoặc giao nhau thuộc các NavigationPolygon khác nhau thường sẽ khiến việc tạo kết nối cạnh của navigation region trên NavigationServer thất bại và nên được tránh.

.. image:: img/navigation_vertex_merge2.png

.. warning::

    Đối với việc hợp nhất vị trí đỉnh, "chính xác" có nghĩa là chính xác tuyệt đối. Các sai số float nhỏ thường xuyên xảy ra với các mesh được import sẽ ngăn việc hợp nhất đỉnh thành công.

Ngoài ra, các navigation mesh không được hợp nhất nhưng vẫn được NavigationServer xem là **connected** khi các cạnh của chúng gần song song và nằm trong khoảng cách cho phép với nhau. Khoảng cách kết nối được xác định bởi ``edge_connection_margin`` cho mỗi navigation map. Trong nhiều trường hợp, các cạnh navigation mesh không thể kết nối đúng cách khi chúng chồng lấp một phần. Để behavior hợp nhất nhất quán, tốt nhất là luôn tránh mọi sự chồng lấp giữa các navigation mesh.

.. image:: img/navigation_edge_connection.png

Nếu navigation debug được bật và NavigationServer đang hoạt động, các kết nối navigation mesh đã được thiết lập sẽ được hiển thị trực quan. Xem :ref:`doc_navigation_debug_tools` để biết thêm thông tin về các tùy chọn navigation debug.

``edge_connection_margin`` 2D mặc định có thể được thay đổi trong ProjectSettings tại ``navigation/2d/default_edge_connection_margin``.

``edge_connection_margin`` 3D mặc định có thể được thay đổi trong ProjectSettings tại ``navigation/3d/default_edge_connection_margin``.

Giá trị edge connection margin của bất kỳ navigation map nào cũng có thể được thay đổi trong runtime bằng NavigationServer API.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    func _ready() -> void:
        # Các margin 2D được thiết kế để hoạt động với các giá trị "pixel" 2D.
        var default_map_rid: RID = get_world_2d().get_navigation_map()
        NavigationServer2D.map_set_edge_connection_margin(default_map_rid, 50.0)

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        public override void _Ready()
        {
            // Các margin 2D được thiết kế để hoạt động với các giá trị "pixel" 2D.
            Rid defaultMapRid = GetWorld2D().NavigationMap;
            NavigationServer2D.MapSetEdgeConnectionMargin(defaultMapRid, 50.0f);
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    func _ready() -> void:
        # Các margin 3D được thiết kế để hoạt động với các giá trị đơn vị thế giới 3D.
        var default_map_rid: RID = get_world_3d().get_navigation_map()
        NavigationServer3D.map_set_edge_connection_margin(default_map_rid, 0.5)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            // Các margin 3D được thiết kế để hoạt động với các giá trị đơn vị thế giới 3D.
            Rid defaultMapRid = GetWorld3D().NavigationMap;
            NavigationServer3D.MapSetEdgeConnectionMargin(defaultMapRid, 0.5f);
        }
    }

.. note::

    Việc thay đổi edge connection margin sẽ kích hoạt quá trình cập nhật toàn bộ các kết nối navigation mesh trên NavigationServer.
