.. _doc_navigation_using_navigationregions:

Sử dụng NavigationRegions
=========================

NavigationRegions là biểu diễn Node trực quan của một **region** thuộc **map** điều hướng trên NavigationServer. Mỗi node NavigationRegion chứa một resource cho dữ liệu navigation mesh.

Có sẵn cả phiên bản 2D và 3D, lần lượt là :ref:`NavigationRegion2D<class_NavigationRegion2D>` và :ref:`NavigationRegion3D<class_NavigationRegion3D>`.

Các NavigationRegion riêng lẻ tải dữ liệu resource NavigationPolygon 2D hoặc NavigationMesh 3D lên NavigationServer. Map của NavigationServer chuyển thông tin này thành một navigation map kết hợp để pathfinding.

Để tạo một navigation region bằng scene tree, hãy thêm node ``NavigationRegion2D`` hoặc ``NavigationRegion3D`` vào scene. Tất cả region đều cần một navigation mesh resource để hoạt động. Xem :ref:`doc_navigation_using_navigationmeshes` để tìm hiểu cách tạo và áp dụng navigation mesh.

NavigationRegions sẽ tự động đẩy các thay đổi ``global_transform`` đến region trên NavigationServer, nhờ đó phù hợp với các nền tảng di động. NavigationServer sẽ cố gắng kết nối navigation mesh của các region riêng lẻ khi chúng đủ gần nhau. Để biết thêm chi tiết, hãy xem :ref:`doc_navigation_connecting_navmesh`. Để kết nối các NavigationRegion qua những khoảng cách bất kỳ, hãy xem :ref:`doc_navigation_using_navigationlinks` để tìm hiểu cách tạo và sử dụng ``NavigationLinks``.

.. warning::

    Mặc dù thay đổi transform của node NavigationRegion sẽ cập nhật vị trí region trên NavigationServer, thay đổi scale thì không. Navigation mesh resource không có scale và cần được cập nhật hoàn toàn khi hình học nguồn thay đổi scale.

Có thể bật / tắt các region; nếu bị tắt, chúng sẽ không đóng góp vào các truy vấn pathfinding trong tương lai.

.. note::

    Các path hiện có sẽ không được tự động cập nhật khi một region được bật / tắt.

Tạo navigation region mới
~~~~~~~~~~~~~~~~~~~~~~~~~

Các node NavigationRegion mới sẽ tự động đăng ký với navigation map mặc định của world cho dimension 2D/3D tương ứng.

Sau đó có thể lấy RID của region từ các Node NavigationRegion bằng ``get_rid()``.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends NavigationRegion2D

    var navigationserver_region_rid: RID = get_rid()

 .. code-tab:: csharp 2D C#

    public partial class MyNavigationRegion2D : NavigationRegion2D
    {
        public override void _Ready()
        {
            Rid navigationServerRegionRid = GetRid();
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends NavigationRegion3D

    var navigationserver_region_rid: RID = get_rid()

 .. code-tab:: csharp 3D C#

    public partial class MyNavigationRegion3D : NavigationRegion3D
    {
        public override void _Ready()
        {
            Rid navigationServerRegionRid = GetRid();
        }
    }

Các region mới cũng có thể được tạo bằng NavigationServer API và thêm vào bất kỳ map hiện có nào.

Nếu region được tạo trực tiếp bằng NavigationServer API, chúng cần được gán navigation map theo cách thủ công.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    func _ready() -> void:
        var new_region_rid: RID = NavigationServer2D.region_create()
        var default_map_rid: RID = get_world_2d().get_navigation_map()
        NavigationServer2D.region_set_map(new_region_rid, default_map_rid)

 .. code-tab:: csharp 2D C#

    public partial class MyNode2D : Node2D
    {
        public override void _Ready()
        {
            Rid newRegionRid = NavigationServer2D.RegionCreate();
            Rid defaultMapRid = GetWorld2D().NavigationMap;
            NavigationServer2D.RegionSetMap(newRegionRid, defaultMapRid);
        }
    }

 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    func _ready() -> void:
        var new_region_rid: RID = NavigationServer3D.region_create()
        var default_map_rid: RID = get_world_3d().get_navigation_map()
        NavigationServer3D.region_set_map(new_region_rid, default_map_rid)

 .. code-tab:: csharp 3D C#

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            Rid newRegionRid = NavigationServer3D.RegionCreate();
            Rid defaultMapRid = GetWorld3D().NavigationMap;
            NavigationServer3D.RegionSetMap(newRegionRid, defaultMapRid);
        }
    }

.. note::

    Navigation region chỉ có thể được gán cho một navigation map duy nhất. Nếu một region hiện có được gán cho navigation map mới, nó sẽ rời khỏi map cũ.
