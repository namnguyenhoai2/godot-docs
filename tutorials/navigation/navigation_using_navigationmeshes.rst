.. _doc_navigation_using_navigationmeshes:

Sử dụng navigation mesh
=======================

.. image:: img/nav_meshes.webp

Các phiên bản 2D và 3D của navigation mesh có sẵn dưới dạng
:ref:`NavigationPolygon<class_NavigationPolygon>` và
:ref:`NavigationMesh<class_NavigationMesh>` tương ứng.

.. note::

    Navigation mesh chỉ mô tả một khu vực có thể đi qua đối với vị trí trung tâm của agent. Mọi giá trị bán kính mà agent có thể có đều bị bỏ qua. Nếu muốn việc tìm đường tính đến kích thước (collision) của agent, bạn cần thu nhỏ navigation mesh tương ứng.

Navigation hoạt động độc lập với các thành phần khác của engine như rendering hoặc physics. Khi thực hiện tìm đường, chỉ navigation mesh được xem xét; chẳng hạn, hình ảnh và các hình dạng collision hoàn toàn bị hệ thống navigation bỏ qua. Nếu cần tính đến dữ liệu khác (chẳng hạn như hình ảnh) khi tìm đường, bạn cần điều chỉnh navigation mesh tương ứng. Quá trình đưa các hạn chế về navigation vào navigation mesh thường được gọi là navigation mesh baking.

.. figure:: img/nav_mesh_vs_physics.webp
   :align: center
   :alt: So sánh đa giác navigation mesh lồi và lõm

   Navigation mesh mô tả một bề mặt mà agent có thể đứng an toàn bằng tâm của nó, khác với các hình dạng physics mô tả các giới hạn collision bên ngoài.

Nếu gặp vấn đề bị xuyên cắt hoặc collision khi đi theo các đường dẫn navigation, hãy luôn nhớ rằng bạn cần cho hệ thống navigation biết ý định của mình thông qua một navigation mesh phù hợp. Tự thân hệ thống navigation sẽ không bao giờ biết "đây là hình dạng collision hoặc visual mesh của cây / đá / tường" vì nó chỉ biết rằng "ở đây, tôi được cho biết là có thể tìm đường an toàn vì nó nằm trên navigation mesh".

.. _doc_navigation_navmesh_baking:

Navigation mesh baking có thể được thực hiện bằng cách sử dụng :ref:`NavigationRegion2D<class_NavigationRegion2D>` hoặc :ref:`NavigationRegion3D<class_NavigationRegion3D>`, hoặc bằng cách sử dụng trực tiếp API
:ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _doc_navigation_using_navigationmeshes_baking_navigation_mesh_with_navigationregion:

Baking navigation mesh bằng NavigationRegion
--------------------------------------------

.. figure:: img/nav_mesh_baking_steps.gif
   :align: center
   :alt: Các bước baking navigation mesh

   Baking navigation mesh với độ lệch bán kính agent so với hình học.

Việc baking navigation mesh trở nên dễ tiếp cận hơn nhờ node NavigationRegion. Khi baking bằng node NavigationRegion, các bước phân tích, baking và cập nhật region riêng lẻ đều được kết hợp thành một function.

Các node này có sẵn ở dạng 2D và 3D lần lượt là :ref:`NavigationRegion2D<class_NavigationRegion2D>` và :ref:`NavigationRegion3D<class_NavigationRegion3D>`.

.. tip::

    Có thể chuyển ``source_geometry_mode`` của navigation mesh sang chế độ phân tích các tên nhóm node cụ thể, để các node cần được bake có thể được đặt ở bất kỳ đâu trong scene.

.. tabs::

   .. tab:: Baking bằng NavigationRegion2D

        Khi chọn node NavigationRegion2D trong Editor, các tùy chọn bake cũng như các công cụ vẽ đa giác sẽ xuất hiện trên thanh trên cùng của Editor.

        .. image:: img/nav_region_baking_01.webp

        Để region hoạt động, cần thêm một resource :ref:`NavigationPolygon<class_NavigationPolygon>`.

        Các thuộc tính để phân tích và bake navigation mesh sau đó thuộc về resource được sử dụng và có thể tìm thấy trong resource Inspector.

        .. image:: img/nav_region_baking_02.webp

        Kết quả phân tích hình học nguồn có thể được kiểm soát bằng các thuộc tính sau.

        - ``parsed_geometry_type`` lọc xem các đối tượng visual, các đối tượng physics hay cả hai cần được phân tích từ :ref:`SceneTree<class_SceneTree>`. Để biết thêm chi tiết về những đối tượng nào được phân tích và cách phân tích, hãy xem phần về phân tích hình học nguồn bên dưới.
        - ``collision_mask`` lọc các đối tượng physics collision nào được bao gồm khi ``parsed_geometry_type`` bao gồm các static collider.
        - ``source_geometry_mode`` xác định node nào sẽ bắt đầu quá trình phân tích và cách duyệt qua :ref:`SceneTree<class_SceneTree>`.
        - ``source_geometry_group_name`` được sử dụng khi chỉ nên phân tích một nhóm node nhất định. Phụ thuộc vào ``source_geometry_mode`` đã chọn.

        Sau khi thêm hình học nguồn, kết quả baking có thể được kiểm soát bằng các thuộc tính sau.

        - ``cell_size`` đặt kích thước lưới rasterization và nên khớp với kích thước navigation map.
        - ``agent_radius`` thu nhỏ navigation mesh đã bake để tạo đủ khoảng đệm cho kích thước (collision) của agent.

        Việc baking NavigationRegion2D cũng có thể được sử dụng trong runtime bằng scripts.

        .. tabs::
         .. code-tab:: gdscript GDScript

            var on_thread: bool = true
            bake_navigation_polygon(on_thread)

         .. code-tab:: csharp

            bool onThread = true;
            BakeNavigationPolygon(onThread);

        Để nhanh chóng kiểm thử baking 2D với các thiết lập mặc định:

        - Thêm một :ref:`NavigationRegion2D<class_NavigationRegion2D>`.
        - Thêm resource :ref:`NavigationPolygon<class_NavigationPolygon>` vào NavigationRegion2D.
        - Thêm một :ref:`Polygon2D<class_Polygon2D>` bên dưới NavigationRegion2D.
        - Vẽ 1 đường bao NavigationPolygon bằng công cụ vẽ NavigationRegion2D đã chọn.
        - Vẽ 1 đường bao Polygon2D bên trong đường bao NavigationPolygon bằng công cụ vẽ Polygon2D đã chọn.
        - Nhấn nút bake của Editor và navigation mesh sẽ xuất hiện.

        .. image:: img/nav_region_baking_01.webp

        .. image:: img/nav_mesh_mini_2d.webp

   .. tab:: Baking bằng NavigationRegion3D

        Khi chọn node NavigationRegion3D trong Editor, các tùy chọn bake sẽ xuất hiện trên thanh trên cùng của Editor.

        .. image:: img/nav_mesh_bake_toolbar.webp

        Để region hoạt động, cần thêm một resource :ref:`NavigationMesh<class_NavigationMesh>`.

        Các thuộc tính để phân tích và bake navigation mesh sau đó thuộc về resource được sử dụng và có thể tìm thấy trong resource Inspector.

        .. image:: img/nav_region3d_baking_01.webp

        Kết quả phân tích hình học nguồn có thể được kiểm soát bằng các thuộc tính sau.

        - ``parsed_geometry_type`` lọc xem các đối tượng visual, các đối tượng physics hay cả hai cần được phân tích từ :ref:`SceneTree<class_SceneTree>`. Để biết thêm chi tiết về những đối tượng nào được phân tích và cách phân tích, hãy xem phần về phân tích hình học nguồn bên dưới.
        - ``collision_mask`` lọc các đối tượng physics collision nào được bao gồm khi ``parsed_geometry_type`` bao gồm các static collider.
        - ``source_geometry_mode`` xác định node nào sẽ bắt đầu quá trình phân tích và cách duyệt qua :ref:`SceneTree<class_SceneTree>`.
        - ``source_geometry_group_name`` được sử dụng khi chỉ nên phân tích một nhóm node nhất định. Phụ thuộc vào ``source_geometry_mode`` đã chọn.

        Sau khi thêm hình học nguồn, kết quả baking có thể được kiểm soát bằng các thuộc tính sau.

        - ``cell_size`` và ``cell_height`` xác định kích thước lưới voxel rasterization và phải khớp với kích thước bản đồ điều hướng.
        - ``agent_radius`` thu nhỏ navigation mesh đã bake để tạo đủ khoảng đệm cho kích thước (collision) của agent.
        - ``agent_height`` loại trừ khỏi navigation mesh những khu vực mà agent quá cao để đi qua.
        - ``agent_max_climb`` và ``agent_max_slope`` loại bỏ những khu vực có chênh lệch độ cao giữa các voxel liền kề quá lớn hoặc có bề mặt quá dốc.

        .. warning::

            ``cell_size`` hoặc ``cell_height`` quá nhỏ có thể tạo ra quá nhiều voxel, đến mức có khả năng làm game bị treo hoặc thậm chí bị crash.


        Tính năng baking của NavigationRegion3D cũng có thể được sử dụng khi runtime bằng scripts.

        .. tabs::
         .. code-tab:: gdscript GDScript

            var on_thread: bool = true
            bake_navigation_mesh(on_thread)

         .. code-tab:: csharp

            bool onThread = true;
            BakeNavigationMesh(onThread);

        Để nhanh chóng kiểm thử baking 3D với các thiết lập mặc định:

        - Thêm một :ref:`NavigationRegion3D<class_NavigationRegion3D>`.
        - Thêm resource :ref:`NavigationMesh<class_NavigationMesh>` vào NavigationRegion3D.
        - Thêm một :ref:`MeshInstance3D<class_MeshInstance3D>` bên dưới NavigationRegion3D.
        - Thêm một :ref:`PlaneMesh<class_PlaneMesh>` vào MeshInstance3D.
        - Nhấn nút bake của Editor và navigation mesh sẽ xuất hiện.

        .. image:: img/nav_mesh_bake_toolbar.webp

        .. image:: img/nav_mesh_mini_3d.webp

.. _doc_navigation_using_navigationmeshes_baking_navigation_mesh_with_navigationserver:

Baking navigation mesh bằng NavigationServer
--------------------------------------------

:ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>` có các hàm API để gọi riêng từng bước của quy trình baking navigation mesh.

- Có thể sử dụng ``parse_source_geometry_data()`` để phân tích source geometry thành một resource có thể tái sử dụng và serialize.
- Có thể sử dụng ``bake_from_source_geometry_data()`` để bake navigation mesh từ dữ liệu đã được phân tích, chẳng hạn để tránh các vấn đề về hiệu năng runtime do việc phân tích (dư thừa).
- ``bake_from_source_geometry_data_async()`` cũng làm điều tương tự nhưng bake navigation mesh một cách deferred bằng threads, không chặn main thread.

So với NavigationRegion, NavigationServer cung cấp quyền kiểm soát chi tiết hơn đối với quy trình baking navigation mesh. Đổi lại, nó phức tạp hơn khi sử dụng nhưng cũng cung cấp nhiều tùy chọn nâng cao hơn.

Một số ưu điểm khác của NavigationServer so với NavigationRegion là:

- Server có thể phân tích source geometry mà không bake, chẳng hạn để cache source geometry cho lần sử dụng sau.
- Server cho phép chọn thủ công root node nơi bắt đầu phân tích source geometry.
- Server có thể tiếp nhận và bake từ dữ liệu source geometry được tạo theo thủ tục.
- Server có thể bake nhiều navigation mesh theo trình tự trong khi tái sử dụng cùng một dữ liệu source geometry.

Để bake navigation mesh bằng NavigationServer, cần có source geometry. Source geometry là dữ liệu hình học cần được xem xét trong quy trình baking navigation mesh. Navigation mesh cho cả 2D và 3D đều được tạo bằng cách bake từ source geometry.

Các resource source geometry cho phiên bản 2D và 3D có sẵn dưới dạng
:ref:`NavigationMeshSourceGeometryData2D<class_NavigationMeshSourceGeometryData2D>` và
:ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>` tương ứng.

Source geometry có thể là hình học được phân tích từ visual mesh, từ physics collision hoặc các mảng dữ liệu được tạo theo thủ tục, chẳng hạn như các đường bao (2D) và các mặt tam giác (3D). Để thuận tiện, source geometry thường được phân tích trực tiếp từ các node setup trong SceneTree. Khi (re)bake navigation mesh lúc runtime, hãy lưu ý rằng việc phân tích hình học luôn diễn ra trên main thread.

.. note::

    SceneTree không thread-safe. Chỉ có thể phân tích source geometry từ SceneTree trên main thread.

.. warning::

    Dữ liệu từ visual mesh và polygon cần được nhận từ GPU, khiến RenderingServer bị đình trệ trong quá trình này. Khi (re)bake lúc runtime, nên sử dụng physics shape làm source geometry đã được phân tích.

Source geometry được lưu bên trong các resource để có thể tái sử dụng hình học đã tạo cho nhiều lần bake. Ví dụ, có thể bake nhiều navigation mesh cho các kích thước agent khác nhau từ cùng một source geometry. Điều này cũng cho phép lưu source geometry vào đĩa để tải lại sau, chẳng hạn nhằm tránh chi phí phân tích lại lúc runtime.

Nhìn chung, dữ liệu hình học nên được giữ thật đơn giản. Cần bao nhiêu cạnh thì dùng bấy nhiêu, nhưng càng ít càng tốt. Đặc biệt trong 2D, nên tránh hình học bị trùng lặp và lồng nhau, vì điều đó buộc phải tính toán lỗ polygon và có thể khiến polygon bị lật. Ví dụ về hình học lồng nhau là một shape StaticBody2D nhỏ hơn được đặt hoàn toàn bên trong phạm vi của một shape StaticBody2D khác.

Baking các chunk navigation mesh cho thế giới lớn
-------------------------------------------------

.. figure:: img/navmesh_chunk_build.gif
   :align: center
   :alt: Xây dựng chunk navigation mesh

   Xây dựng và cập nhật từng chunk navigation mesh riêng lẻ lúc runtime.

.. seealso::

    Bạn có thể xem hoạt động baking chunk navigation mesh trong các project demo `Navigation Mesh Chunks 2D <https://github.com/godotengine/godot-demo-projects/tree/master/2d/navigation_mesh_chunks>`__ và `Navigation Mesh Chunks 3D <https://github.com/godotengine/godot-demo-projects/tree/master/3d/navigation_mesh_chunks>`__.

Để tránh các cạnh bị lệch giữa những chunk region khác nhau, navigation mesh có hai thuộc tính quan trọng đối với quy trình baking navigation mesh: bake bound và border size. Kết hợp với nhau, chúng có thể được dùng để đảm bảo các cạnh giữa những chunk region được căn chỉnh hoàn toàn.

.. figure:: img/navmesh_bound_bordersize.webp
   :align: center
   :alt: Chunk navigation mesh với bake bound và border size

   Chunk navigation mesh được bake với bake bound hoặc được bake cùng border size bổ sung.

Bake bound, là một :ref:`Rect2<class_Rect2>` cho 2D và :ref:`AABB<class_AABB>` cho 3D được căn chỉnh theo trục, giới hạn source geometry được sử dụng bằng cách loại bỏ toàn bộ hình học nằm ngoài phạm vi.

Có thể sử dụng các thuộc tính :ref:`NavigationPolygon<class_NavigationPolygon>`, ``baking_rect`` và ``baking_rect_offset`` để tạo và đặt giới hạn baking 2D.

Có thể sử dụng các thuộc tính :ref:`NavigationMesh<class_NavigationMesh>`, ``filter_baking_aabb`` và ``filter_baking_aabb_offset`` để tạo và đặt giới hạn baking 3D.

Ngay cả khi chỉ thiết lập giới hạn baking, vẫn còn một vấn đề khác. Navigation mesh kết quả chắc chắn sẽ bị ảnh hưởng bởi các offset cần thiết như ``agent_radius``, khiến các cạnh không thẳng hàng.

.. figure:: img/navmesh_chunk_gaps.webp
   :align: center
   :alt: Các chunk navigation mesh có khoảng trống

   Các chunk navigation mesh có những khoảng trống rõ rệt do offset theo bán kính agent khi baking.

Đây là lúc thuộc tính ``border_size`` của navigation mesh phát huy tác dụng. Kích thước viền là một lề hướng vào trong tính từ giới hạn baking. Đặc điểm quan trọng của kích thước viền là nó không bị ảnh hưởng bởi hầu hết offset và các bước postprocessing như ``agent_radius``.

Thay vì loại bỏ hình học nguồn, kích thước viền loại bỏ các phần của bề mặt cuối cùng của navigation mesh đã baking. Nếu giới hạn baking đủ lớn, kích thước viền có thể loại bỏ các phần bề mặt có vấn đề để chỉ còn lại kích thước chunk mong muốn.

.. figure:: img/navmesh_chunks.webp
   :align: center
   :alt: Các chunk navigation mesh không có khoảng trống

   Các chunk navigation mesh có các cạnh thẳng hàng và không có khoảng trống.

.. note::

    Các giới hạn baking cần đủ lớn để bao gồm một lượng hình học nguồn hợp lý từ tất cả chunk lân cận.

.. warning::

    Trong 3D, chức năng của kích thước viền chỉ giới hạn trên trục xz.

Các vấn đề thường gặp khi baking navigation mesh
------------------------------------------------

Có một số vấn đề thường gặp của người dùng và các điểm cần lưu ý quan trọng khi tạo hoặc baking navigation mesh.

- Baking navigation mesh gây ra vấn đề về frame rate khi runtime
    Theo mặc định, việc baking navigation mesh được thực hiện trên background thread, vì vậy miễn là nền tảng hỗ trợ thread, bản thân quá trình baking hiếm khi là nguồn gây ra vấn đề hiệu năng (giả sử hình học có kích thước và độ phức tạp hợp lý khi rebake tại runtime).

    Nguồn phổ biến gây ra vấn đề hiệu năng khi runtime là bước phân tích hình học nguồn liên quan đến các node và SceneTree. SceneTree không thread-safe, vì vậy tất cả node cần được phân tích trên main thread. Một số node chứa nhiều dữ liệu có thể rất nặng và chậm khi phân tích tại runtime; ví dụ, một TileMap có một hoặc nhiều polygon cho mỗi cell và TileMapLayer được sử dụng cần phân tích. Các node chứa mesh cần yêu cầu dữ liệu từ RenderingServer, khiến quá trình rendering bị đình trệ.

    Để cải thiện hiệu năng, hãy sử dụng các shape được tối ưu hơn, chẳng hạn collision shape thay cho visual mesh chi tiết, đồng thời gộp và đơn giản hóa nhiều nhất có thể phần hình học ngay từ đầu. Nếu không cách nào hiệu quả, đừng phân tích SceneTree mà hãy thêm hình học nguồn bằng script theo cách procedural. Nếu chỉ sử dụng các mảng dữ liệu thuần túy làm hình học nguồn, toàn bộ quá trình baking có thể được thực hiện trên background thread.

- Navigation mesh tạo ra các lỗ ngoài ý muốn trong 2D.
    Việc baking navigation mesh trong 2D được thực hiện bằng các thao tác clipping polygon dựa trên các đường outline. Các polygon có "lỗ" là điều không thể tránh khỏi để tạo ra các polygon 2D phức tạp hơn, nhưng có thể trở nên khó đoán đối với người dùng khi có nhiều shape phức tạp liên quan.

    Để tránh các vấn đề không mong muốn khi tính toán lỗ của polygon, hãy tránh lồng bất kỳ outline nào bên trong outline khác cùng loại (traversable / obstruction). Điều này cũng áp dụng cho các shape được phân tích từ node. Ví dụ, đặt một shape StaticBody2D nhỏ hơn bên trong một shape StaticBody2D lớn hơn có thể khiến polygon kết quả bị đảo chiều.

- Navigation mesh xuất hiện bên trong hình học trong 3D.
    Việc baking navigation mesh trong 3D không có khái niệm "bên trong". Các voxel cell được dùng để rasterize hình học либо bị chiếm dụng либо không. Hãy loại bỏ phần hình học nằm trên mặt đất bên trong phần hình học khác. Nếu không thể thực hiện việc đó, hãy thêm hình học "dummy" nhỏ hơn vào bên trong với ít triangle nhất có thể để các cell được chiếm dụng bởi một đối tượng nào đó.

    Có thể sử dụng một shape :ref:`NavigationObstacle3D<class_NavigationObstacle3D>` được thiết lập để baking với navigation mesh nhằm loại bỏ hình học.

.. figure:: img/nav_mesh_obstacles_discard.webp
   :align: center
   :alt: Loại bỏ hình học không mong muốn bằng NavigationObstacle3D

   Có thể sử dụng shape NavigationObstacle3D để loại bỏ các phần navigation mesh không mong muốn.

Các template script cho navigation mesh
---------------------------------------

Script sau sử dụng NavigationServer để phân tích hình học nguồn từ scene tree, baking một navigation mesh và cập nhật một navigation region bằng navigation mesh đã cập nhật.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    var navigation_mesh: NavigationPolygon
    var source_geometry : NavigationMeshSourceGeometryData2D
    var callback_parsing : Callable
    var callback_baking : Callable
    var region_rid: RID

    func _ready() -> void:
        navigation_mesh = NavigationPolygon.new()
        navigation_mesh.agent_radius = 10.0
        source_geometry = NavigationMeshSourceGeometryData2D.new()
        callback_parsing = on_parsing_done
        callback_baking = on_baking_done
        region_rid = NavigationServer2D.region_create()

        # Bật region và đặt region vào navigation map mặc định.
        NavigationServer2D.region_set_enabled(region_rid, true)
        NavigationServer2D.region_set_map(region_rid, get_world_2d().get_navigation_map())

        # Một số mega-node như TileMap thường chưa sẵn sàng ở frame đầu tiên.
        # Ngoài ra, quá trình phân tích cần diễn ra trên main thread.
        # Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
        parse_source_geometry.call_deferred()

    func parse_source_geometry() -> void:
        source_geometry.clear()
        var root_node: Node2D = self

        # Theo mặc định, phân tích các outline obstruction từ tất cả node con của root node.
        NavigationServer2D.parse_source_geometry_data(
            navigation_mesh,
            source_geometry,
            root_node,
            callback_parsing
        )

    func on_parsing_done() -> void:
        # Nếu không phân tích một TileMap có các cell navigation mesh, lúc này chúng ta có thể chỉ
        # có các outline obstruction, vì vậy hãy thêm ít nhất một outline traversable
        # để các outline obstruction có thứ gì đó để "cắt" vào.
        source_geometry.add_traversable_outline(PackedVector2Array([
            Vector2(0.0, 0.0),
            Vector2(500.0, 0.0),
            Vector2(500.0, 500.0),
            Vector2(0.0, 500.0)
        ]))

        # Baking navigation mesh trên một thread bằng dữ liệu hình học nguồn.
        NavigationServer2D.bake_from_source_geometry_data_async(
            navigation_mesh,
            source_geometry,
            callback_baking
        )

    func on_baking_done() -> void:
        # Cập nhật region bằng navigation mesh đã cập nhật.
        NavigationServer2D.region_set_navigation_polygon(region_rid, navigation_mesh)

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private NavigationPolygon _navigationMesh;
        private NavigationMeshSourceGeometryData2D _sourceGeometry;
        private Callable _callbackParsing;
        private Callable _callbackBaking;
        private Rid _regionRid;

        public override void _Ready()
        {
            _navigationMesh = new NavigationPolygon();
            _navigationMesh.AgentRadius = 10.0f;
            _sourceGeometry = new NavigationMeshSourceGeometryData2D();
            _callbackParsing = Callable.From(OnParsingDone);
            _callbackBaking = Callable.From(OnBakingDone);
            _regionRid = NavigationServer2D.RegionCreate();

            // Bật region và đặt region vào navigation map mặc định.
            NavigationServer2D.RegionSetEnabled(_regionRid, true);
            NavigationServer2D.RegionSetMap(_regionRid, GetWorld2D().NavigationMap);

            // Một số mega-node như TileMap thường chưa sẵn sàng ở frame đầu tiên.
            // Ngoài ra, quá trình phân tích cần diễn ra trên main thread.
            // Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
            CallDeferred(MethodName.ParseSourceGeometry);
        }

        private void ParseSourceGeometry()
        {
            _sourceGeometry.Clear();
            Node2D rootNode = this;

            // Theo mặc định, phân tích các đường bao vật cản từ tất cả node con của node gốc.
            NavigationServer2D.ParseSourceGeometryData(
                _navigationMesh,
                _sourceGeometry,
                rootNode,
                _callbackParsing
            );
        }

        private void OnParsingDone()
        {
            // Nếu chúng ta chưa phân tích một TileMap có các ô navigation mesh thì hiện tại chúng ta có thể chỉ
            // có các đường bao vật cản, vì vậy hãy thêm ít nhất một đường bao có thể đi qua
            // để các đường bao vật cản có thứ gì đó để "cắt" vào.
            _sourceGeometry.AddTraversableOutline(
            [
                new Vector2(0.0f, 0.0f),
                new Vector2(500.0f, 0.0f),
                new Vector2(500.0f, 500.0f),
                new Vector2(0.0f, 500.0f),
            ]);

            // Bake navigation mesh trên một thread với dữ liệu hình học nguồn.
            NavigationServer2D.BakeFromSourceGeometryDataAsync(_navigationMesh, _sourceGeometry, _callbackBaking);
        }

        private void OnBakingDone()
        {
            // Cập nhật region bằng navigation mesh đã cập nhật.
            NavigationServer2D.RegionSetNavigationPolygon(_regionRid, _navigationMesh);
        }
    }


 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    var navigation_mesh: NavigationMesh
    var source_geometry : NavigationMeshSourceGeometryData3D
    var callback_parsing : Callable
    var callback_baking : Callable
    var region_rid: RID

    func _ready() -> void:
        navigation_mesh = NavigationMesh.new()
        navigation_mesh.agent_radius = 0.5
        source_geometry = NavigationMeshSourceGeometryData3D.new()
        callback_parsing = on_parsing_done
        callback_baking = on_baking_done
        region_rid = NavigationServer3D.region_create()

        # Bật region và đặt region vào navigation map mặc định.
        NavigationServer3D.region_set_enabled(region_rid, true)
        NavigationServer3D.region_set_map(region_rid, get_world_3d().get_navigation_map())

        # Một số mega-node như GridMap thường chưa sẵn sàng ngay ở frame đầu tiên.
        # Ngoài ra, quá trình phân tích cần diễn ra trên main thread.
        # Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
        parse_source_geometry.call_deferred()

    func parse_source_geometry() -> void:
        source_geometry.clear()
        var root_node: Node3D = self

        # Theo mặc định, phân tích hình học từ tất cả node con dạng mesh của node gốc.
        NavigationServer3D.parse_source_geometry_data(
            navigation_mesh,
            source_geometry,
            root_node,
            callback_parsing
        )

    func on_parsing_done() -> void:
        # Baking navigation mesh trên một thread bằng dữ liệu hình học nguồn.
        NavigationServer3D.bake_from_source_geometry_data_async(
            navigation_mesh,
            source_geometry,
            callback_baking
        )

    func on_baking_done() -> void:
        # Cập nhật region bằng navigation mesh đã cập nhật.
        NavigationServer3D.region_set_navigation_mesh(region_rid, navigation_mesh)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private NavigationMesh _navigationMesh;
        private NavigationMeshSourceGeometryData3D _sourceGeometry;
        private Callable _callbackParsing;
        private Callable _callbackBaking;
        private Rid _regionRid;

        public override void _Ready()
        {
            _navigationMesh = new NavigationMesh();
            _navigationMesh.AgentRadius = 0.5f;
            _sourceGeometry = new NavigationMeshSourceGeometryData3D();
            _callbackParsing = Callable.From(OnParsingDone);
            _callbackBaking = Callable.From(OnBakingDone);
            _regionRid = NavigationServer3D.RegionCreate();

            // Bật region và đặt region vào navigation map mặc định.
            NavigationServer3D.RegionSetEnabled(_regionRid, true);
            NavigationServer3D.RegionSetMap(_regionRid, GetWorld3D().NavigationMap);

            // Một số mega-node như GridMap thường chưa sẵn sàng ngay ở frame đầu tiên.
            // Ngoài ra, quá trình phân tích cần diễn ra trên main thread.
            // Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
            CallDeferred(MethodName.ParseSourceGeometry);
        }

        private void ParseSourceGeometry ()
        {
            _sourceGeometry.Clear();
            Node3D rootNode = this;

            // Theo mặc định, phân tích hình học từ tất cả node con dạng mesh của node gốc.
            NavigationServer3D.ParseSourceGeometryData(
                _navigationMesh,
                _sourceGeometry,
                rootNode,
                _callbackParsing
            );
        }

        private void OnParsingDone()
        {
            // Bake navigation mesh trên một thread với dữ liệu hình học nguồn.
            NavigationServer3D.BakeFromSourceGeometryDataAsync(_navigationMesh, _sourceGeometry, _callbackBaking);
        }

        private void OnBakingDone()
        {
            // Cập nhật region bằng navigation mesh đã cập nhật.
            NavigationServer3D.RegionSetNavigationMesh(_regionRid, _navigationMesh);
        }
    }

Script sau sử dụng NavigationServer để cập nhật một navigation region bằng dữ liệu navigation mesh được tạo theo thủ tục.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    var navigation_mesh: NavigationPolygon
    var region_rid: RID

    func _ready() -> void:
        navigation_mesh = NavigationPolygon.new()
        region_rid = NavigationServer2D.region_create()

        # Bật region và đặt region vào navigation map mặc định.
        NavigationServer2D.region_set_enabled(region_rid, true)
        NavigationServer2D.region_set_map(region_rid, get_world_2d().get_navigation_map())

        # Thêm các đỉnh cho một đa giác lồi.
        navigation_mesh.vertices = PackedVector2Array([
            Vector2(0.0, 0.0),
            Vector2(100.0, 0.0),
            Vector2(100.0, 100.0),
            Vector2(0.0, 100.0),
        ])

        # Thêm các chỉ mục cho đa giác.
        navigation_mesh.add_polygon(
            PackedInt32Array([0, 1, 2, 3])
        )

        NavigationServer2D.region_set_navigation_polygon(region_rid, navigation_mesh)

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private NavigationPolygon _navigationMesh;
        private Rid _regionRid;

        public override void _Ready()
        {
            _navigationMesh = new NavigationPolygon();
            _regionRid = NavigationServer2D.RegionCreate();

            // Bật region và đặt region vào navigation map mặc định.
            NavigationServer2D.RegionSetEnabled(_regionRid, true);
            NavigationServer2D.RegionSetMap(_regionRid, GetWorld2D().NavigationMap);

            // Thêm các đỉnh cho một đa giác lồi.
            _navigationMesh.Vertices =
            [
                new Vector2(0, 0),
                new Vector2(100.0f, 0),
                new Vector2(100.0f, 100.0f),
                new Vector2(0, 100.0f),
            ];

            // Thêm các chỉ mục cho đa giác.
            _navigationMesh.AddPolygon([0, 1, 2, 3]);

            NavigationServer2D.RegionSetNavigationPolygon(_regionRid, _navigationMesh);
        }
    }


 .. code-tab:: gdscript 3D GDScript

    extends Node3D

    var navigation_mesh: NavigationMesh
    var region_rid: RID

    func _ready() -> void:
        navigation_mesh = NavigationMesh.new()
        region_rid = NavigationServer3D.region_create()

        # Bật region và đặt region vào navigation map mặc định.
        NavigationServer3D.region_set_enabled(region_rid, true)
        NavigationServer3D.region_set_map(region_rid, get_world_3d().get_navigation_map())

        # Thêm các đỉnh cho một đa giác lồi.
        navigation_mesh.vertices = PackedVector3Array([
            Vector3(-1.0, 0.0, 1.0),
            Vector3(1.0, 0.0, 1.0),
            Vector3(1.0, 0.0, -1.0),
            Vector3(-1.0, 0.0, -1.0),
        ])

        # Thêm các chỉ mục cho đa giác.
        navigation_mesh.add_polygon(
            PackedInt32Array([0, 1, 2, 3])
        )

        NavigationServer3D.region_set_navigation_mesh(region_rid, navigation_mesh)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        private NavigationMesh _navigationMesh;
        private Rid _regionRid;

        public override void _Ready()
        {
            _navigationMesh = new NavigationMesh();
            _regionRid = NavigationServer3D.RegionCreate();

            // Bật region và đặt region vào navigation map mặc định.
            NavigationServer3D.RegionSetEnabled(_regionRid, true);
            NavigationServer3D.RegionSetMap(_regionRid, GetWorld3D().NavigationMap);

            // Thêm các đỉnh cho một đa giác lồi.
            _navigationMesh.Vertices =
            [
                new Vector3(-1.0f, 0.0f, 1.0f),
                new Vector3(1.0f, 0.0f, 1.0f),
                new Vector3(1.0f, 0.0f, -1.0f),
                new Vector3(-1.0f, 0.0f, -1.0f),
            ];

            // Thêm các chỉ mục cho đa giác.
            _navigationMesh.AddPolygon([0, 1, 2, 3]);

            NavigationServer3D.RegionSetNavigationMesh(_regionRid, _navigationMesh);
        }
    }
