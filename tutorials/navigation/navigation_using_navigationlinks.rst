.. _doc_navigation_using_navigationlinks:

Sử dụng NavigationLinks
=======================

.. image:: img/nav_navmesh_links.png

NavigationLinks được dùng để kết nối các polygon của navigation mesh từ :ref:`NavigationRegion2D<class_NavigationRegion2D>` và :ref:`NavigationRegion3D<class_NavigationRegion3D>` qua các khoảng cách tùy ý nhằm tìm đường.

NavigationLinks cũng được dùng để xem xét các lối tắt di chuyển trong quá trình tìm đường, có thể sử dụng thông qua việc tương tác với các đối tượng gameplay, chẳng hạn như thang, bệ nhảy hoặc cổng dịch chuyển.

Có các phiên bản 2D và 3D của node NavigationJumplinks dưới dạng
:ref:`NavigationLink2D<class_NavigationLink2D>` và
:ref:`NavigationLink3D<class_NavigationLink3D>` tương ứng.

Các NavigationRegion khác nhau có thể kết nối navigation mesh của chúng mà không cần NavigationLink, miễn là chúng có các cạnh chồng lấn hoặc các cạnh nằm trong phạm vi ``edge_connection_margin`` của navigation map. Khi khoảng cách trở nên quá lớn, việc tạo các kết nối hợp lệ sẽ trở thành một vấn đề — NavigationLinks có thể giải quyết vấn đề này.

Xem :ref:`doc_navigation_using_navigationregions` để tìm hiểu thêm về cách sử dụng các navigation region. Xem :ref:`doc_navigation_connecting_navmesh` để tìm hiểu thêm về cách kết nối các navigation mesh.

.. image:: img/nav_link_properties.png

NavigationLinks có nhiều thuộc tính giống với NavigationRegions, chẳng hạn như ``navigation_layers``. NavigationLinks tạo một kết nối duy nhất giữa hai vị trí qua một khoảng cách tùy ý, trong khi NavigationRegions bổ sung một khu vực có thể đi qua mang tính cục bộ hơn cùng với tài nguyên navigation mesh.

NavigationLinks có ``start_position`` và ``end_position``, đồng thời có thể đi theo cả hai hướng khi bật ``bidirectional``. Khi được đặt, một navigationlink sẽ kết nối các polygon của navigation mesh gần ``start_position`` và ``end_position`` nhất trong bán kính tìm kiếm để tìm đường.

Bán kính tìm kiếm polygon có thể được cấu hình trên toàn cục trong ProjectSettings tại ``navigation/2d_or_3d/default_link_connection_radius``, hoặc được đặt riêng cho từng navigation **map** bằng hàm ``NavigationServer.map_set_link_connection_radius()``.

Cả ``start_position`` và ``end_position`` đều có các marker gỡ lỗi trong Editor. Các mũi tên cho biết hướng mà link có thể được đi qua, còn bán kính hiển thị của một vị trí cho biết bán kính tìm kiếm polygon. Tất cả polygon của navigation mesh bên trong bán kính sẽ được so sánh và polygon gần nhất sẽ được chọn để kết nối cạnh. Nếu không tìm thấy polygon hợp lệ nào trong bán kính tìm kiếm, navigation link sẽ bị vô hiệu hóa.

.. image:: img/nav_link_debug_visuals.webp

Các hình ảnh trực quan gỡ lỗi của link có thể được thay đổi trong Editor :ref:`ProjectSettings<class_ProjectSettings>` tại ``debug/shapes/navigation``. Bạn cũng có thể điều khiển khả năng hiển thị thông tin gỡ lỗi trong menu gizmo của 3D Viewport trong Editor.

Navigation link không cung cấp bất kỳ cơ chế di chuyển chuyên biệt nào qua link. Thay vào đó, khi agent đến vị trí của một link, game code cần phản hồi (chẳng hạn thông qua các area trigger) và cung cấp phương thức để agent di chuyển qua link, đến vị trí còn lại của link (chẳng hạn thông qua teleport hoặc animation). Nếu không có điều đó, agent sẽ cố tự di chuyển dọc theo đường đi của link. Kết quả có thể là agent đi qua một hố không đáy thay vì chờ một moving platform, hoặc đi xuyên qua teleporter rồi tiếp tục đi xuyên qua tường.

Mẫu script cho navigation link
------------------------------

Script sau sử dụng NavigationServer để tạo một navigation link mới.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    var link_rid: RID
    var link_start_position: Vector2
    var link_end_position: Vector2

    func _ready() -> void:
        link_rid = NavigationServer2D.link_create()

        var link_owner_id: int = get_instance_id()
        var link_enter_cost: float = 1.0
        var link_travel_cost: float = 1.0
        var link_navigation_layers: int = 1
        var link_bidirectional: bool = true

        NavigationServer2D.link_set_owner_id(link_rid, link_owner_id)
        NavigationServer2D.link_set_enter_cost(link_rid, link_enter_cost)
        NavigationServer2D.link_set_travel_cost(link_rid, link_travel_cost)
        NavigationServer2D.link_set_navigation_layers(link_rid, link_navigation_layers)
        NavigationServer2D.link_set_bidirectional(link_rid, link_bidirectional)

        # Bật link và đặt link vào navigation map mặc định.
        NavigationServer2D.link_set_enabled(link_rid, true)
        NavigationServer2D.link_set_map(link_rid, get_world_2d().get_navigation_map())

        # Di chuyển 2 vị trí của link đến các vị trí global mong muốn.
        NavigationServer2D.link_set_start_position(link_rid, link_start_position)
        NavigationServer2D.link_set_end_position(link_rid, link_end_position)

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private Rid _linkRid;
        private Vector2 _linkStartPosition;
        private Vector2 _linkEndPosition;

        public override void _Ready()
        {
            _linkRid = NavigationServer2D.LinkCreate();

            ulong linkOwnerId = GetInstanceId();
            float linkEnterCost = 1.0f;
            float linkTravelCost = 1.0f;
            uint linkNavigationLayers = 1;
            bool linkBidirectional = true;

            NavigationServer2D.LinkSetOwnerId(_linkRid, linkOwnerId);
            NavigationServer2D.LinkSetEnterCost(_linkRid, linkEnterCost);
            NavigationServer2D.LinkSetTravelCost(_linkRid, linkTravelCost);
            NavigationServer2D.LinkSetNavigationLayers(_linkRid, linkNavigationLayers);
            NavigationServer2D.LinkSetBidirectional(_linkRid, linkBidirectional);

            // Bật link và đặt link vào navigation map mặc định.
            NavigationServer2D.LinkSetEnabled(_linkRid, true);
            NavigationServer2D.LinkSetMap(_linkRid, GetWorld2D().NavigationMap);

            // Di chuyển 2 vị trí của link đến các vị trí global mong muốn.
            NavigationServer2D.LinkSetStartPosition(_linkRid, _linkStartPosition);
            NavigationServer2D.LinkSetEndPosition(_linkRid, _linkEndPosition);
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    var link_rid: RID
    var link_start_position: Vector3
    var link_end_position: Vector3

    func _ready() -> void:
        link_rid = NavigationServer3D.link_create()

        var link_owner_id: int = get_instance_id()
        var link_enter_cost: float = 1.0
        var link_travel_cost: float = 1.0
        var link_navigation_layers: int = 1
        var link_bidirectional: bool = true

        NavigationServer3D.link_set_owner_id(link_rid, link_owner_id)
        NavigationServer3D.link_set_enter_cost(link_rid, link_enter_cost)
        NavigationServer3D.link_set_travel_cost(link_rid, link_travel_cost)
        NavigationServer3D.link_set_navigation_layers(link_rid, link_navigation_layers)
        NavigationServer3D.link_set_bidirectional(link_rid, link_bidirectional)

        # Bật link và đặt link vào navigation map mặc định.
        NavigationServer3D.link_set_enabled(link_rid, true)
        NavigationServer3D.link_set_map(link_rid, get_world_3d().get_navigation_map())

        # Di chuyển 2 vị trí của link đến các vị trí global mong muốn.
        NavigationServer3D.link_set_start_position(link_rid, link_start_position)
        NavigationServer3D.link_set_end_position(link_rid, link_end_position)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private Rid _linkRid;
        private Vector3 _linkStartPosition;
        private Vector3 _linkEndPosition;

        public override void _Ready()
        {
            _linkRid = NavigationServer3D.LinkCreate();

            ulong linkOwnerId = GetInstanceId();
            float linkEnterCost = 1.0f;
            float linkTravelCost = 1.0f;
            uint linkNavigationLayers = 1;
            bool linkBidirectional = true;

            NavigationServer3D.LinkSetOwnerId(_linkRid, linkOwnerId);
            NavigationServer3D.LinkSetEnterCost(_linkRid, linkEnterCost);
            NavigationServer3D.LinkSetTravelCost(_linkRid, linkTravelCost);
            NavigationServer3D.LinkSetNavigationLayers(_linkRid, linkNavigationLayers);
            NavigationServer3D.LinkSetBidirectional(_linkRid, linkBidirectional);

            // Bật link và đặt link vào navigation map mặc định.
            NavigationServer3D.LinkSetEnabled(_linkRid, true);
            NavigationServer3D.LinkSetMap(_linkRid, GetWorld3D().NavigationMap);

            // Di chuyển 2 vị trí của link đến các vị trí global mong muốn.
            NavigationServer3D.LinkSetStartPosition(_linkRid, _linkStartPosition);
            NavigationServer3D.LinkSetEndPosition(_linkRid, _linkEndPosition);
        }
    }
