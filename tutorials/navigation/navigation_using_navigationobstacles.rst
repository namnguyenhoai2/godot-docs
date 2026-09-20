.. _doc_navigation_using_navigationobstacles:

Sử dụng NavigationObstacles
===========================

Có các phiên bản 2D và 3D của node NavigationObstacles dưới dạng
:ref:`NavigationObstacle2D<class_NavigationObstacle2D>` and
:ref:`NavigationObstacle3D<class_NavigationObstacle3D>`  respectively.

Các chướng ngại vật điều hướng có hai mục đích: chúng có thể ảnh hưởng đến cả việc dựng navigation mesh và việc tránh né của agent.

- Khi bật ``affect_navigation_mesh``, chướng ngại vật sẽ ảnh hưởng đến navigation mesh khi được dựng. - Khi bật ``avoidance_enabled``, chướng ngại vật sẽ ảnh hưởng đến các agent tránh né.

.. tip::

    Tính năng tránh né được bật theo mặc định. Nếu chướng ngại vật không được dùng cho việc tránh né, hãy tắt ``enabled_avoidance`` để tiết kiệm hiệu năng.

Chướng ngại vật và navigation mesh
----------------------------------

.. figure:: img/nav_mesh_obstacles.webp
   :align: center
   :alt: Navigation obstacles affecting navigation mesh baking

   Navigation obstacles affecting navigation mesh baking.

Để dựng navigation mesh, có thể dùng chướng ngại vật nhằm loại bỏ các phần của toàn bộ geometry nguồn khác nằm bên trong hình dạng của chướng ngại vật.

Điều này có thể được dùng để ngăn navigation mesh được dựng ở những vị trí không mong muốn, ví dụ như bên trong geometry "đặc" như các bức tường dày hoặc trên các geometry khác không nên được đưa vào gameplay như mái nhà.

.. figure:: img/nav_mesh_obstacles_discard.webp
   :align: center
   :alt: Navigation obstacles discard of unwanted navigation mesh

   Navigation obstacles discard of unwanted navigation mesh.

Chướng ngại vật không thêm geometry trong quá trình dựng mà chỉ loại bỏ geometry. Nó thực hiện điều này bằng cách vô hiệu hóa tất cả các ô (voxel) chứa geometry nguồn đã được rasterize nằm bên trong hình dạng chướng ngại vật. Vì vậy, hiệu ứng và độ chi tiết hình dạng của nó bị giới hạn bởi độ phân giải ô được dùng trong quá trình dựng.

Để biết thêm chi tiết về việc dựng navigation mesh, hãy xem :ref:`doc_navigation_using_navigationmeshes`.

.. image:: img/nav_mesh_obstacles_properties.webp

Thuộc tính ``affect_navigation_mesh`` khiến chướng ngại vật tham gia vào quá trình dựng navigation mesh. Nó sẽ được phân tích hoặc không phân tích giống như mọi node object khác trong quá trình dựng navigation mesh.

Thuộc tính ``carve_navigation_mesh`` khiến hình dạng không bị ảnh hưởng bởi các offset của quá trình dựng, ví dụ offset được thêm bởi navigation mesh ``agent_radius``. Về cơ bản, nó sẽ hoạt động như một stencil và cắt vào bề mặt navigation mesh đã được offset. Nó vẫn chịu ảnh hưởng của các bước hậu xử lý tiếp theo trong quá trình dựng, chẳng hạn như đơn giản hóa cạnh.

Hình dạng và vị trí của chướng ngại vật được xác định bằng các thuộc tính ``height`` và ``vertices``, cùng với ``global_position`` của chướng ngại vật. Giá trị trục y của mọi Vector3 được dùng cho các đỉnh sẽ bị bỏ qua vì chướng ngại vật được chiếu lên một mặt phẳng ngang phẳng.

Khi dựng navigation mesh trong các script, có thể thêm chướng ngại vật theo cách procedural dưới dạng vật cản được chiếu. Chướng ngại vật không tham gia vào việc phân tích geometry nguồn, vì vậy chỉ cần thêm chúng ngay trước khi dựng là đủ.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    var obstacle_outline = PackedVector2Array([
        Vector2(-50, -50),
        Vector2(50, -50),
        Vector2(50, 50),
        Vector2(-50, 50)
    ])

    var navigation_mesh = NavigationPolygon.new()
    var source_geometry = NavigationMeshSourceGeometryData2D.new()

    NavigationServer2D.parse_source_geometry_data(navigation_mesh, source_geometry, $MyTestRootNode)

    var obstacle_carve: bool = true

    source_geometry.add_projected_obstruction(obstacle_outline, obstacle_carve)

    NavigationServer2D.bake_from_source_geometry_data(navigation_mesh, source_geometry)

 .. code-tab:: csharp 2D C#

    Vector2[] obstacleOutline
    [
        new Vector2(-50, -50),
        new Vector2(50, -50),
        new Vector2(50, 50),
        new Vector2(-50, 50),
    ];

    var navigationMesh = new NavigationPolygon();
    var sourceGeometry = new NavigationMeshSourceGeometryData2D();

    NavigationServer2D.ParseSourceGeometryData(navigationMesh, sourceGeometry, GetNode<Node2D>("MyTestRootNode"));

    bool obstacleCarve = true;

    sourceGeometry.AddProjectedObstruction(obstacleOutline, obstacleCarve);
    NavigationServer2D.BakeFromSourceGeometryData(navigationMesh, sourceGeometry);

 .. code-tab:: gdscript 3D GDScript

    var obstacle_outline = PackedVector3Array([
        Vector3(-5, 0, -5),
        Vector3(5, 0, -5),
        Vector3(5, 0, 5),
        Vector3(-5, 0, 5)
    ])

    var navigation_mesh = NavigationMesh.new()
    var source_geometry = NavigationMeshSourceGeometryData3D.new()

    NavigationServer3D.parse_source_geometry_data(navigation_mesh, source_geometry, $MyTestRootNode)

    var obstacle_elevation: float = $MyTestObstacleNode.global_position.y
    var obstacle_height: float = 50.0
    var obstacle_carve: bool = true

    source_geometry.add_projected_obstruction(obstacle_outline, obstacle_elevation, obstacle_height, obstacle_carve)

    NavigationServer3D.bake_from_source_geometry_data(navigation_mesh, source_geometry)

 .. code-tab:: csharp 3D C#

    Vector3[] obstacleOutline =
    [
        new Vector3(-5, 0, -5),
        new Vector3(5, 0, -5),
        new Vector3(5, 0, 5),
        new Vector3(-5, 0, 5),
    ];

    var navigationMesh = new NavigationMesh();
    var sourceGeometry = new NavigationMeshSourceGeometryData3D();

    NavigationServer3D.ParseSourceGeometryData(navigationMesh, sourceGeometry, GetNode<Node3D>("MyTestRootNode"));

    float obstacleElevation = GetNode<Node3D>("MyTestObstacleNode").GlobalPosition.Y;
    float obstacleHeight = 50.0f;
    bool obstacleCarve = true;

    sourceGeometry.AddProjectedObstruction(obstacleOutline, obstacleElevation, obstacleHeight, obstacleCarve);
    NavigationServer3D.BakeFromSourceGeometryData(navigationMesh, sourceGeometry);

Chướng ngại vật và việc tránh né của agent
------------------------------------------

Đối với việc tránh né, có thể dùng chướng ngại vật điều hướng dưới dạng chướng ngại vật tĩnh hoặc động để ảnh hưởng đến các agent được điều khiển bằng tính năng tránh né.

- Khi được dùng ở dạng tĩnh, NavigationObstacles giới hạn các agent được điều khiển bằng tính năng tránh né ở bên ngoài hoặc bên trong một khu vực được xác định bởi polygon. - Khi được dùng ở dạng động, NavigationObstacles đẩy các agent được điều khiển bằng tính năng tránh né ra xa trong một bán kính xung quanh chúng.

Chướng ngại vật tránh né tĩnh
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một chướng ngại vật tránh né được xem là tĩnh khi thuộc tính ``vertices`` của nó chứa một mảng outline gồm các vị trí để tạo thành một polygon.

.. figure:: img/nav_static_obstacle_build.gif
   :align: center
   :alt: Static obstacle drawn in the editor to block or contain navigation agents

   Static obstacle drawn in the editor to block or contain navigation agents.

- Chướng ngại vật tĩnh hoạt động như các ranh giới cứng không được vượt qua đối với các agent dùng tính năng tránh né, tương tự va chạm vật lý nhưng dành cho tránh né. - Chướng ngại vật tĩnh xác định ranh giới bằng một mảng outline ``vertices`` (các vị trí), và trong trường hợp 3D có thêm thuộc tính ``height``. - Chướng ngại vật tĩnh chỉ hoạt động với các agent dùng chế độ tránh né 2D. - Chướng ngại vật tĩnh xác định thông qua thứ tự winding của các đỉnh liệu agent sẽ bị đẩy ra ngoài hay bị hút vào trong. - Chướng ngại vật tĩnh không thể thay đổi vị trí. Chúng chỉ có thể được warp đến một vị trí mới và dựng lại từ đầu. Vì vậy, chướng ngại vật tĩnh không phù hợp với các trường hợp sử dụng mà vị trí thay đổi mỗi frame, do việc dựng lại liên tục có chi phí hiệu năng cao. - Các chướng ngại vật tĩnh được warp đến vị trí khác không thể được agent dự đoán. Điều này tạo ra nguy cơ agent bị mắc kẹt nếu chướng ngại vật tĩnh được warp chồng lên agent.

Khi sử dụng tránh né 2D trong 3D, trục y của các đỉnh Vector3 sẽ bị bỏ qua. Thay vào đó, vị trí trục y toàn cục của chướng ngại vật được dùng làm độ cao. Agent sẽ bỏ qua các chướng ngại vật tĩnh trong 3D nằm bên dưới hoặc bên trên chúng. Điều này được tự động xác định bằng vị trí trục y toàn cục của cả chướng ngại vật và agent, được dùng làm độ cao, cùng với các thuộc tính chiều cao tương ứng của chúng.

Chướng ngại vật tránh né động
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một chướng ngại vật tránh né được xem là động khi thuộc tính ``radius`` của nó lớn hơn không.

- Chướng ngại vật động hoạt động như một đối tượng mềm có ý nghĩa "hãy tránh xa tôi" đối với các agent dùng tính năng tránh né, tương tự cách chúng tránh các agent khác. - Chướng ngại vật động xác định ranh giới bằng một ``radius`` duy nhất cho hình tròn 2D, hoặc hình cầu trong trường hợp tránh né 3D. - Chướng ngại vật động có thể thay đổi vị trí mỗi frame mà không phát sinh thêm chi phí hiệu năng. - Các chướng ngại vật động có velocity được thiết lập có thể được agent dự đoán chuyển động. - Chướng ngại vật động không phải là cách đáng tin cậy để giới hạn agent trong không gian đông đúc hoặc chật hẹp.

Mặc dù cả thuộc tính tĩnh và động có thể đồng thời hoạt động trên cùng một chướng ngại vật, điều này không được khuyến nghị vì lý do hiệu năng. Tốt nhất, khi một chướng ngại vật đang di chuyển, hãy xóa các đỉnh tĩnh và thay vào đó kích hoạt bán kính. Khi chướng ngại vật đến vị trí cuối mới, nó nên từ từ tăng bán kính để đẩy tất cả agent khác ra xa. Sau khi tạo đủ không gian an toàn xung quanh chướng ngại vật, hãy thêm lại các đỉnh tĩnh và xóa bán kính. Điều này giúp tránh việc agent bị mắc kẹt trong chướng ngại vật tĩnh đột ngột xuất hiện khi ranh giới tĩnh được dựng lại hoàn tất.

Tương tự agent, chướng ngại vật có thể sử dụng bitmask ``avoidance_layers``. Tất cả agent có bit tương ứng trên avoidance mask của riêng chúng sẽ tránh chướng ngại vật.

Chướng ngại vật procedural
--------------------------

Có thể tạo chướng ngại vật mới trong script mà không cần Node bằng cách sử dụng trực tiếp NavigationServer.

Các chướng ngại vật được tạo bằng script yêu cầu ít nhất một ``map`` và một ``position``. Để sử dụng động, cần có ``radius``. Để sử dụng tĩnh, cần có một mảng ``vertices``.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    # tạo một "obstacle" mới và đặt nó trên navigation map mặc định.
    var new_obstacle_rid: RID = NavigationServer2D.obstacle_create()
    var default_map_rid: RID = get_world_2d().get_navigation_map()

    NavigationServer2D.obstacle_set_map(new_obstacle_rid, default_map_rid)
    NavigationServer2D.obstacle_set_position(new_obstacle_rid, global_position)

    # Sử dụng obstacle ở dạng động bằng cách tăng radius lên trên không.
    NavigationServer2D.obstacle_set_radius(new_obstacle_rid, 5.0)

    # Sử dụng obstacle ở dạng tĩnh bằng cách thêm một hình vuông đẩy agent ra ngoài.
    var outline = PackedVector2Array([Vector2(-100, -100), Vector2(100, -100), Vector2(100, 100), Vector2(-100, 100)])
    NavigationServer2D.obstacle_set_vertices(new_obstacle_rid, outline)

    # Bật obstacle.
    NavigationServer2D.obstacle_set_avoidance_enabled(new_obstacle_rid, true)

 .. code-tab:: csharp 2D C#

    // Tạo một "obstacle" mới và đặt nó trên navigation map mặc định.
    Rid newObstacleRid = NavigationServer2D.ObstacleCreate();
    Rid defaultMapRid = GetWorld2D().NavigationMap;

    NavigationServer2D.ObstacleSetMap(newObstacleRid, defaultMapRid);
    NavigationServer2D.ObstacleSetPosition(newObstacleRid, GlobalPosition);

    // Sử dụng obstacle ở dạng động bằng cách tăng radius lên trên không.
    NavigationServer2D.ObstacleSetRadius(newObstacleRid, 5.0f);

    // Sử dụng obstacle ở dạng tĩnh bằng cách thêm một hình vuông đẩy agent ra ngoài.
    Vector2[] outline =
    [
        new Vector2(-100, -100),
        new Vector2(100, -100),
        new Vector2(100, 100),
        new Vector2(-100, 100),
    ];
    NavigationServer2D.ObstacleSetVertices(newObstacleRid, outline);

    // Bật obstacle.
    NavigationServer2D.ObstacleSetAvoidanceEnabled(newObstacleRid, true);

 .. code-tab:: gdscript 3D GDScript

    # Tạo một "obstacle" mới và đặt nó trên navigation map mặc định.
    var new_obstacle_rid: RID = NavigationServer3D.obstacle_create()
    var default_map_rid: RID = get_world_3d().get_navigation_map()

    NavigationServer3D.obstacle_set_map(new_obstacle_rid, default_map_rid)
    NavigationServer3D.obstacle_set_position(new_obstacle_rid, global_position)

    # Sử dụng obstacle ở dạng động bằng cách tăng radius lên trên không.
    NavigationServer3D.obstacle_set_radius(new_obstacle_rid, 0.5)

    # Sử dụng obstacle ở dạng tĩnh bằng cách thêm một hình vuông đẩy agent ra ngoài.
    var outline = PackedVector3Array([Vector3(-5, 0, -5), Vector3(5, 0, -5), Vector3(5, 0, 5), Vector3(-5, 0, 5)])
    NavigationServer3D.obstacle_set_vertices(new_obstacle_rid, outline)
    # Đặt chiều cao của obstacle trên trục y.
    NavigationServer3D.obstacle_set_height(new_obstacle_rid, 1.0)

    # Bật obstacle.
    NavigationServer3D.obstacle_set_avoidance_enabled(new_obstacle_rid, true)

 .. code-tab:: csharp 3D C#

    // Tạo một "obstacle" mới và đặt nó trên navigation map mặc định.
    Rid newObstacleRid = NavigationServer3D.ObstacleCreate();
    Rid defaultMapRid = GetWorld3D().NavigationMap;

    NavigationServer3D.ObstacleSetMap(newObstacleRid, defaultMapRid);
    NavigationServer3D.ObstacleSetPosition(newObstacleRid, GlobalPosition);

    // Sử dụng obstacle ở dạng động bằng cách tăng radius lên trên không.
    NavigationServer3D.ObstacleSetRadius(newObstacleRid, 5.0f);

    // Sử dụng obstacle ở dạng tĩnh bằng cách thêm một hình vuông đẩy agent ra ngoài.
    Vector3[] outline =
    [
        new Vector3(-5, 0, -5),
        new Vector3(5, 0, -5),
        new Vector3(5, 0, 5),
        new Vector3(-5, 0, 5),
    ];
    NavigationServer3D.ObstacleSetVertices(newObstacleRid, outline);
    // Đặt chiều cao của obstacle trên trục y.
    NavigationServer3D.ObstacleSetHeight(newObstacleRid, 1.0f);

    // Bật obstacle.
    NavigationServer3D.ObstacleSetAvoidanceEnabled(newObstacleRid, true);
