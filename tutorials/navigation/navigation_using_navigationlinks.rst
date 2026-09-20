.. _doc_navigation_using_navigationlinks:

Sử dụng NavigationLinks
=======================

.. image:: img/nav_navmesh_links.png

NavigationLinks được sử dụng để kết nối các polygon của navigation mesh từ :ref:`NavigationRegion2D<class_NavigationRegion2D>` và :ref:`NavigationRegion3D<class_NavigationRegion3D>` qua những khoảng cách bất kỳ nhằm pathfinding.

NavigationLinks cũng được sử dụng để tính đến các lối tắt di chuyển trong pathfinding, có thể thực hiện thông qua việc tương tác với các đối tượng gameplay, chẳng hạn như thang, jump pad hoặc dịch chuyển tức thời.

Có các phiên bản 2D và 3D của node NavigationJumplinks dưới dạng
:ref:`NavigationLink2D<class_NavigationLink2D>` and
:ref:`NavigationLink3D<class_NavigationLink3D>` respectively.

Các NavigationRegions khác nhau có thể kết nối navigation mesh của chúng mà không cần NavigationLink, miễn là chúng có các cạnh chồng lấn hoặc các cạnh nằm trong ``edge_connection_margin`` của navigation map. Khi khoảng cách trở nên quá lớn, việc xây dựng các kết nối hợp lệ sẽ trở thành một vấn đề — và NavigationLinks có thể giải quyết vấn đề đó.

Xem :ref:`doc_navigation_using_navigationregions` để tìm hiểu thêm về cách sử dụng navigation regions. Xem :ref:`doc_navigation_connecting_navmesh` để tìm hiểu thêm về cách kết nối navigation meshes.

.. image:: img/nav_link_properties.png

NavigationLinks có nhiều thuộc tính giống với NavigationRegions, chẳng hạn như ``navigation_layers``. NavigationLinks thêm một kết nối duy nhất giữa hai vị trí qua một khoảng cách bất kỳ, trong khi NavigationRegions thêm một khu vực có thể đi qua mang tính cục bộ hơn cùng một navigation mesh resource.

NavigationLinks có ``start_position`` và ``end_position``, đồng thời có thể hoạt động theo cả hai hướng khi ``bidirectional`` được bật. Khi được đặt, một navigationlink sẽ kết nối các polygon của navigation mesh gần nhất với ``start_position`` và ``end_position`` trong bán kính tìm kiếm để thực hiện pathfinding.

Bán kính tìm kiếm polygon có thể được cấu hình trên toàn cục trong ProjectSettings tại ``navigation/2d_or_3d/default_link_connection_radius``, hoặc được thiết lập riêng cho từng navigation **map** bằng hàm ``NavigationServer.map_set_link_connection_radius()``.

Cả ``start_position`` và ``end_position`` đều có các debug marker trong Editor. Các mũi tên cho biết link có thể được đi qua theo hướng nào, còn bán kính hiển thị của một vị trí cho biết bán kính tìm kiếm polygon. Tất cả polygon của navigation mesh bên trong bán kính này sẽ được so sánh và polygon gần nhất sẽ được chọn để kết nối cạnh. Nếu không tìm thấy polygon hợp lệ nào trong bán kính tìm kiếm, navigation link sẽ bị vô hiệu hóa.

.. image:: img/nav_link_debug_visuals.webp

Các debug visual của link có thể được thay đổi trong Editor :ref:`ProjectSettings<class_ProjectSettings>` tại ``debug/shapes/navigation``. Khả năng hiển thị debug cũng có thể được điều khiển trong menu gizmo của 3D Viewport trong Editor.

Một navigation link không cung cấp cơ chế di chuyển chuyên biệt qua link. Thay vào đó, khi một agent đến vị trí của link, game code cần phản hồi (ví dụ: thông qua area trigger) và cung cấp cách để agent di chuyển qua link, đến vị trí còn lại của link (ví dụ: thông qua teleport hoặc animation). Nếu không có cơ chế đó, agent sẽ cố tự di chuyển dọc theo đường đi của link. Kết quả có thể là agent đi bộ trên một vực không đáy thay vì chờ moving platform, hoặc đi xuyên qua teleporter rồi tiếp tục đi xuyên qua một bức tường.

Các script template của navigation link
---------------------------------------

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

        # Bật link và đặt nó vào navigation map mặc định.
        NavigationServer2D.link_set_enabled(link_rid, true)
        NavigationServer2D.link_set_map(link_rid, get_world_2d().get_navigation_map())

        # Di chuyển 2 vị trí của link đến các vị trí global dự kiến.
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

            // Bật link và đặt nó vào navigation map mặc định.
            NavigationServer2D.LinkSetEnabled(_linkRid, true);
            NavigationServer2D.LinkSetMap(_linkRid, GetWorld2D().NavigationMap);

            // Di chuyển 2 vị trí của link đến các vị trí global dự kiến.
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

        # Bật link và đặt nó vào navigation map mặc định.
        NavigationServer3D.link_set_enabled(link_rid, true)
        NavigationServer3D.link_set_map(link_rid, get_world_3d().get_navigation_map())

        # Di chuyển 2 vị trí của link đến các vị trí global dự kiến.
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

            // Bật link và đặt nó vào navigation map mặc định.
            NavigationServer3D.LinkSetEnabled(_linkRid, true);
            NavigationServer3D.LinkSetMap(_linkRid, GetWorld3D().NavigationMap);

            // Di chuyển 2 vị trí của link đến các vị trí global dự kiến.
            NavigationServer3D.LinkSetStartPosition(_linkRid, _linkStartPosition);
            NavigationServer3D.LinkSetEndPosition(_linkRid, _linkEndPosition);
        }
    }
