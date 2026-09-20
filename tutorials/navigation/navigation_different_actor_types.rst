.. _doc_navigation_different_actor_types:

Hỗ trợ các loại actor khác nhau
===============================

.. image:: img/nav_actor_sizes.png

Để hỗ trợ các loại actor khác nhau, chẳng hạn do kích thước của chúng, mỗi loại cần có navigation map và navigation mesh riêng được bake với bán kính và chiều cao agent phù hợp. Có thể sử dụng cùng cách tiếp cận để phân biệt giữa các agent đi bộ trên mặt đất, bơi hoặc bay.

.. note::

   Các agent chỉ được xác định bằng giá trị bán kính và chiều cao để bake navigation mesh, tìm đường và tránh né. Không hỗ trợ các hình dạng phức tạp hơn.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo một resource navigation mesh cho mỗi kích thước actor.
    var navigation_mesh_standard_size: NavigationMesh = NavigationMesh.new()
    var navigation_mesh_small_size: NavigationMesh = NavigationMesh.new()
    var navigation_mesh_huge_size: NavigationMesh = NavigationMesh.new()

    # Thiết lập các tham số agent phù hợp.
    navigation_mesh_standard_size.agent_radius = 0.5
    navigation_mesh_standard_size.agent_height = 1.8
    navigation_mesh_small_size.agent_radius = 0.25
    navigation_mesh_small_size.agent_height = 0.7
    navigation_mesh_huge_size.agent_radius = 1.5
    navigation_mesh_huge_size.agent_height = 2.5

    # Lấy node gốc để phân tích hình học phục vụ việc baking.
    var root_node: Node3D = get_node("NavigationMeshBakingRootNode")

    # Tạo resource source geometry để lưu dữ liệu hình học đã được phân tích.
    var source_geometry_data: NavigationMeshSourceGeometryData3D = NavigationMeshSourceGeometryData3D.new()

    # Phân tích source geometry từ scene tree trên main thread.
    # Navigation mesh chỉ cần thiết cho các thiết lập phân tích, vì vậy dùng bất kỳ một trong ba navigation mesh đều được.
    NavigationServer3D.parse_source_geometry_data(navigation_mesh_standard_size, source_geometry_data, root_node)

    # Bake navigation geometry cho mỗi kích thước agent từ cùng một source geometry.
    # Nếu cần để cải thiện hiệu năng, bước baking này cũng có thể được thực hiện trên các background thread.
    NavigationServer3D.bake_from_source_geometry_data(navigation_mesh_standard_size, source_geometry_data)
    NavigationServer3D.bake_from_source_geometry_data(navigation_mesh_small_size, source_geometry_data)
    NavigationServer3D.bake_from_source_geometry_data(navigation_mesh_huge_size, source_geometry_data)

    # Tạo các navigation map khác nhau trên NavigationServer.
    var navigation_map_standard: RID = NavigationServer3D.map_create()
    var navigation_map_small: RID = NavigationServer3D.map_create()
    var navigation_map_huge: RID = NavigationServer3D.map_create()

    # Đặt các navigation map mới làm active.
    NavigationServer3D.map_set_active(navigation_map_standard, true)
    NavigationServer3D.map_set_active(navigation_map_small, true)
    NavigationServer3D.map_set_active(navigation_map_huge, true)

    # Tạo một region cho mỗi map.
    var navigation_region_standard: RID = NavigationServer3D.region_create()
    var navigation_region_small: RID = NavigationServer3D.region_create()
    var navigation_region_huge: RID = NavigationServer3D.region_create()

    # Thêm các region vào các map.
    NavigationServer3D.region_set_map(navigation_region_standard, navigation_map_standard)
    NavigationServer3D.region_set_map(navigation_region_small, navigation_map_small)
    NavigationServer3D.region_set_map(navigation_region_huge, navigation_map_huge)

    # Thiết lập navigation mesh cho mỗi region.
    NavigationServer3D.region_set_navigation_mesh(navigation_region_standard, navigation_mesh_standard_size)
    NavigationServer3D.region_set_navigation_mesh(navigation_region_small, navigation_mesh_small_size)
    NavigationServer3D.region_set_navigation_mesh(navigation_region_huge, navigation_mesh_huge_size)

    # Tạo vị trí bắt đầu và kết thúc cho truy vấn navigation path.
    var start_pos: Vector3 = Vector3(0.0, 0.0, 0.0)
    var end_pos: Vector3 = Vector3(2.0, 0.0, 0.0)
    var use_corridorfunnel: bool = true

    # Truy vấn path cho mỗi kích thước agent.
    var path_standard_agent = NavigationServer3D.map_get_path(navigation_map_standard, start_pos, end_pos, use_corridorfunnel)
    var path_small_agent = NavigationServer3D.map_get_path(navigation_map_small, start_pos, end_pos, use_corridorfunnel)
    var path_huge_agent = NavigationServer3D.map_get_path(navigation_map_huge, start_pos, end_pos, use_corridorfunnel)

 .. code-tab:: csharp

    // Tạo một resource navigation mesh cho mỗi kích thước actor.
    NavigationMesh navigationMeshStandardSize = new NavigationMesh();
    NavigationMesh navigationMeshSmallSize = new NavigationMesh();
    NavigationMesh navigationMeshHugeSize = new NavigationMesh();

    // Thiết lập các tham số agent phù hợp.
    navigationMeshStandardSize.AgentRadius = 0.5f;
    navigationMeshStandardSize.AgentHeight = 1.8f;
    navigationMeshSmallSize.AgentRadius = 0.25f;
    navigationMeshSmallSize.AgentHeight = 0.7f;
    navigationMeshHugeSize.AgentRadius = 1.5f;
    navigationMeshHugeSize.AgentHeight = 2.5f;

    // Lấy node gốc để phân tích hình học phục vụ việc baking.
    Node3D rootNode = GetNode<Node3D>("NavigationMeshBakingRootNode");

    // Tạo resource source geometry để lưu dữ liệu hình học đã được phân tích.
    NavigationMeshSourceGeometryData3D sourceGeometryData = new NavigationMeshSourceGeometryData3D();

    // Phân tích source geometry từ scene tree trên main thread.
    // Navigation mesh chỉ cần thiết cho các thiết lập phân tích, vì vậy dùng bất kỳ một trong ba navigation mesh đều được.
    NavigationServer3D.ParseSourceGeometryData(navigationMeshStandardSize, sourceGeometryData, rootNode);

    // Bake navigation geometry cho mỗi kích thước agent từ cùng một source geometry.
    // Nếu cần để cải thiện hiệu năng, bước baking này cũng có thể được thực hiện trên các background thread.
    NavigationServer3D.BakeFromSourceGeometryData(navigationMeshStandardSize, sourceGeometryData);
    NavigationServer3D.BakeFromSourceGeometryData(navigationMeshSmallSize, sourceGeometryData);
    NavigationServer3D.BakeFromSourceGeometryData(navigationMeshHugeSize, sourceGeometryData);

    // Tạo các navigation map khác nhau trên NavigationServer.
    Rid navigationMapStandard = NavigationServer3D.MapCreate();
    Rid navigationMapSmall = NavigationServer3D.MapCreate();
    Rid navigationMapHuge = NavigationServer3D.MapCreate();

    // Đặt các navigation map mới làm active.
    NavigationServer3D.MapSetActive(navigationMapStandard, true);
    NavigationServer3D.MapSetActive(navigationMapSmall, true);
    NavigationServer3D.MapSetActive(navigationMapHuge, true);

    // Tạo một region cho mỗi map.
    Rid navigationRegionStandard = NavigationServer3D.RegionCreate();
    Rid navigationRegionSmall = NavigationServer3D.RegionCreate();
    Rid navigationRegionHuge = NavigationServer3D.RegionCreate();

    // Thêm các region vào các map.
    NavigationServer3D.RegionSetMap(navigationRegionStandard, navigationMapStandard);
    NavigationServer3D.RegionSetMap(navigationRegionSmall, navigationMapSmall);
    NavigationServer3D.RegionSetMap(navigationRegionHuge, navigationMapHuge);

    // Thiết lập navigation mesh cho mỗi region.
    NavigationServer3D.RegionSetNavigationMesh(navigationRegionStandard, navigationMeshStandardSize);
    NavigationServer3D.RegionSetNavigationMesh(navigationRegionSmall, navigationMeshSmallSize);
    NavigationServer3D.RegionSetNavigationMesh(navigationRegionHuge, navigationMeshHugeSize);

    // Tạo vị trí bắt đầu và kết thúc cho truy vấn navigation path.
    Vector3 startPos = new Vector3(0.0f, 0.0f, 0.0f);
    Vector3 endPos = new Vector3(2.0f, 0.0f, 0.0f);
    bool useCorridorFunnel = true;

    // Truy vấn path cho mỗi kích thước agent.
    var pathStandardAgent = NavigationServer3D.MapGetPath(navigationMapStandard, startPos, endPos, useCorridorFunnel);
    var pathSmallAgent = NavigationServer3D.MapGetPath(navigationMapSmall, startPos, endPos, useCorridorFunnel);
    var pathHugeAgent = NavigationServer3D.MapGetPath(navigationMapHuge, startPos, endPos, useCorridorFunnel);
