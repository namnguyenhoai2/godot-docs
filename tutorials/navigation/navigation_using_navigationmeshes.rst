.. _doc_navigation_using_navigationmeshes:

Sử dụng navigation mesh
=======================

.. image:: img/nav_meshes.webp

Các phiên bản 2D và 3D của navigation mesh có sẵn dưới dạng
:ref:`NavigationPolygon<class_NavigationPolygon>` and
:ref:`NavigationMesh<class_NavigationMesh>`  respectively.

.. note::

    Navigation mesh chỉ mô tả một khu vực có thể đi qua đối với vị trí trung tâm của agent. Mọi giá trị bán kính mà agent có đều bị bỏ qua. Nếu muốn pathfinding tính đến kích thước (collision) của agent, bạn cần thu nhỏ navigation mesh tương ứng.

Navigation hoạt động độc lập với các phần khác của engine như rendering hoặc physics. Navigation mesh là yếu tố duy nhất được xét đến khi thực hiện pathfinding; chẳng hạn, hình ảnh và các hình dạng collision hoàn toàn bị hệ thống navigation bỏ qua. Nếu cần tính đến dữ liệu khác (chẳng hạn hình ảnh) khi thực hiện pathfinding, bạn cần điều chỉnh navigation mesh tương ứng. Quá trình đưa các giới hạn navigation vào navigation mesh thường được gọi là navigation mesh baking.

.. figure:: img/nav_mesh_vs_physics.webp
   :align: center
   :alt: Navigation mesh polygon convex vs concave comparison

   A navigation mesh describes a surface that an agent can stand on safely with its center compared to physics shapes that describe outer collision bounds.

Nếu gặp vấn đề clipping hoặc collision khi đi theo các đường dẫn navigation, hãy luôn nhớ rằng bạn cần cho hệ thống navigation biết ý định của mình thông qua một navigation mesh phù hợp. Tự bản thân hệ thống navigation sẽ không bao giờ biết "đây là một cây / tảng đá / hình dạng collision của tường hoặc visual mesh" vì nó chỉ biết rằng "tại đây, tôi được báo rằng có thể di chuyển an toàn vì nó nằm trên một navigation mesh".

.. _doc_navigation_navmesh_baking:

Navigation mesh baking có thể được thực hiện bằng cách sử dụng :ref:`NavigationRegion2D<class_NavigationRegion2D>` hoặc :ref:`NavigationRegion3D<class_NavigationRegion3D>`, hoặc bằng cách sử dụng
:ref:`NavigationServer2D<class_NavigationServer2D>` and :ref:`NavigationServer3D<class_NavigationServer3D>` API directly.

.. _doc_navigation_using_navigationmeshes_baking_navigation_mesh_with_navigationregion:

Baking navigation mesh bằng NavigationRegion
--------------------------------------------

.. figure:: img/nav_mesh_baking_steps.gif
   :align: center
   :alt: Navigation mesh baking steps

   Baking a navigation mesh with agent radius offset from geometry.

Navigation mesh baking trở nên dễ tiếp cận hơn với node NavigationRegion. Khi baking bằng node NavigationRegion, các bước parsing, baking và cập nhật region riêng lẻ đều được kết hợp thành một function.

Các node này có sẵn trong 2D và 3D lần lượt dưới dạng :ref:`NavigationRegion2D<class_NavigationRegion2D>` và :ref:`NavigationRegion3D<class_NavigationRegion3D>`.

.. tip::

    Navigation mesh ``source_geometry_mode`` có thể được chuyển sang parse các tên node group cụ thể để các node cần được bake có thể được đặt ở bất kỳ đâu trong scene.

.. tabs::

   .. tab:: Baking with a NavigationRegion2D

        Khi một node NavigationRegion2D được chọn trong Editor, các tùy chọn bake cũng như các công cụ vẽ polygon sẽ xuất hiện trên thanh trên cùng của Editor.

        .. image:: img/nav_region_baking_01.webp

        Để region hoạt động, cần thêm một resource :ref:`NavigationPolygon<class_NavigationPolygon>`.

        Các thuộc tính dùng để parse và bake navigation mesh sau đó sẽ thuộc resource được sử dụng và có thể tìm thấy trong resource Inspector.

        .. image:: img/nav_region_baking_02.webp

        Kết quả parsing source geometry có thể được điều chỉnh bằng các thuộc tính sau.

        - - ``parsed_geometry_type`` dùng để lọc xem các đối tượng visual, các đối tượng physics hay cả hai sẽ được parse từ :ref:`SceneTree<class_SceneTree>`. Để biết thêm chi tiết về các đối tượng được parse và cách parse, hãy xem phần parsing source geometry bên dưới. - ``collision_mask`` lọc các đối tượng physics collision nào được đưa vào khi ``parsed_geometry_type`` bao gồm các static collider. - ``source_geometry_mode`` xác định node nào sẽ bắt đầu quá trình parsing và cách duyệt qua :ref:`SceneTree<class_SceneTree>`. - ``source_geometry_group_name`` được sử dụng khi chỉ một node group nhất định cần được parse. Phụ thuộc vào ``source_geometry_mode`` đã chọn.

        Sau khi source geometry được thêm vào, kết quả baking có thể được kiểm soát bằng các thuộc tính sau.

        - - ``cell_size`` thiết lập kích thước rasterization grid và nên khớp với kích thước navigation map. - ``agent_radius`` thu nhỏ navigation mesh đã bake để có đủ khoảng đệm cho kích thước (collision) của agent.

        NavigationRegion2D baking cũng có thể được sử dụng tại runtime bằng scripts.

        .. tabs::
         .. code-tab:: gdscript GDScript

            var on_thread: bool = true
            bake_navigation_polygon(on_thread)

         .. code-tab:: csharp

            bool onThread = true;
            BakeNavigationPolygon(onThread);

        Để nhanh chóng kiểm thử 2D baking với các thiết lập mặc định:

        - Thêm một :ref:`NavigationRegion2D<class_NavigationRegion2D>`. - Thêm resource :ref:`NavigationPolygon<class_NavigationPolygon>` vào NavigationRegion2D. - Thêm một :ref:`Polygon2D<class_Polygon2D>` bên dưới NavigationRegion2D. - Vẽ 1 đường bao NavigationPolygon bằng công cụ vẽ NavigationRegion2D đang được chọn. - Vẽ 1 đường bao Polygon2D bên trong đường bao NavigationPolygon bằng công cụ vẽ Polygon2D đang được chọn. - Nhấn nút bake của Editor và một navigation mesh sẽ xuất hiện.

        .. image:: img/nav_region_baking_01.webp

        .. image:: img/nav_mesh_mini_2d.webp

   .. tab:: Baking with a NavigationRegion3D

        Khi một node NavigationRegion3D được chọn trong Editor, các tùy chọn bake sẽ xuất hiện trên thanh trên cùng của Editor.

        .. image:: img/nav_mesh_bake_toolbar.webp

        Để region hoạt động, cần thêm một resource :ref:`NavigationMesh<class_NavigationMesh>`.

        Các thuộc tính dùng để parse và bake navigation mesh sau đó sẽ thuộc resource được sử dụng và có thể tìm thấy trong resource Inspector.

        .. image:: img/nav_region3d_baking_01.webp

        Kết quả parsing source geometry có thể được điều chỉnh bằng các thuộc tính sau.

        - - ``parsed_geometry_type`` dùng để lọc xem các đối tượng visual, các đối tượng physics hay cả hai sẽ được parse từ :ref:`SceneTree<class_SceneTree>`. Để biết thêm chi tiết về các đối tượng được parse và cách parse, hãy xem phần parsing source geometry bên dưới. - ``collision_mask`` lọc các đối tượng physics collision nào được đưa vào khi ``parsed_geometry_type`` bao gồm các static collider. - ``source_geometry_mode`` xác định node nào sẽ bắt đầu quá trình parsing và cách duyệt qua :ref:`SceneTree<class_SceneTree>`. - ``source_geometry_group_name`` được sử dụng khi chỉ một node group nhất định cần được parse. Phụ thuộc vào ``source_geometry_mode`` đã chọn.

        Sau khi source geometry được thêm vào, kết quả baking có thể được kiểm soát bằng các thuộc tính sau.

        - - ``cell_size`` và ``cell_height`` thiết lập kích thước voxel grid của rasterization và nên khớp với kích thước navigation map. - ``agent_radius`` thu nhỏ navigation mesh đã bake để có đủ khoảng đệm cho kích thước (collision) của agent. - ``agent_height`` loại trừ các khu vực khỏi navigation mesh nơi agent quá cao để có thể đi qua. - ``agent_max_climb`` và ``agent_max_slope`` loại bỏ các khu vực mà chênh lệch độ cao giữa các voxel lân cận quá lớn hoặc bề mặt của chúng quá dốc.

        .. warning::

            ``cell_size`` hoặc ``cell_height`` quá nhỏ có thể tạo ra nhiều voxel đến mức khiến game bị treo hoặc thậm chí bị crash.


        NavigationRegion3D baking cũng có thể được sử dụng tại runtime bằng scripts.

        .. tabs::
         .. code-tab:: gdscript GDScript

            var on_thread: bool = true
            bake_navigation_mesh(on_thread)

         .. code-tab:: csharp

            bool onThread = true;
            BakeNavigationMesh(onThread);

        Để nhanh chóng kiểm thử 3D baking với các thiết lập mặc định:

        - Thêm một :ref:`NavigationRegion3D<class_NavigationRegion3D>`. - Thêm resource :ref:`NavigationMesh<class_NavigationMesh>` vào NavigationRegion3D. - Thêm một :ref:`MeshInstance3D<class_MeshInstance3D>` bên dưới NavigationRegion3D. - Thêm một :ref:`PlaneMesh<class_PlaneMesh>` vào MeshInstance3D. - Nhấn nút bake của Editor và một navigation mesh sẽ xuất hiện.

        .. image:: img/nav_mesh_bake_toolbar.webp

        .. image:: img/nav_mesh_mini_3d.webp

.. _doc_navigation_using_navigationmeshes_baking_navigation_mesh_with_navigationserver:

Baking navigation mesh bằng NavigationServer
--------------------------------------------

:ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>` có các function API để gọi riêng từng bước của quy trình navigation mesh baking.

- ``parse_source_geometry_data()`` có thể được dùng để parse source geometry thành một resource có thể tái sử dụng và serialize. - ``bake_from_source_geometry_data()`` có thể được dùng để bake navigation mesh từ dữ liệu đã parse, chẳng hạn để tránh các vấn đề hiệu năng runtime do parsing (dư thừa). - ``bake_from_source_geometry_data_async()`` cũng tương tự nhưng bake navigation mesh theo cách deferred bằng threads, không chặn main thread.

So với NavigationRegion, NavigationServer cung cấp khả năng kiểm soát tinh vi hơn đối với quy trình navigation mesh baking. Đổi lại, nó phức tạp hơn khi sử dụng nhưng cũng cung cấp các tùy chọn nâng cao hơn.

Một số ưu điểm khác của NavigationServer so với NavigationRegion là:

- - Server có thể parse source geometry mà không baking, chẳng hạn để cache và sử dụng sau. - Server cho phép chọn thủ công root node nơi bắt đầu parsing source geometry. - Server có thể nhận và bake từ dữ liệu source geometry được tạo theo procedural. - Server có thể bake nhiều navigation mesh theo trình tự trong khi tái sử dụng cùng một source geometry data.

Để bake navigation mesh bằng NavigationServer, cần có source geometry. Source geometry là dữ liệu geometry cần được xem xét trong quy trình navigation mesh baking. Cả navigation mesh 2D và 3D đều được tạo bằng cách baking từ source geometry.

Các phiên bản 2D và 3D của resource source geometry có sẵn dưới dạng
:ref:`NavigationMeshSourceGeometryData2D<class_NavigationMeshSourceGeometryData2D>` and
:ref:`NavigationMeshSourceGeometryData3D<class_NavigationMeshSourceGeometryData3D>`  respectively.

Source geometry có thể là geometry được parse từ visual mesh, từ physics collision hoặc các mảng dữ liệu được tạo theo procedural, chẳng hạn như đường bao (2D) và các mặt tam giác (3D). Để thuận tiện, source geometry thường được parse trực tiếp từ các thiết lập node trong SceneTree. Đối với navigation mesh (re)bake tại runtime, hãy lưu ý rằng quá trình parsing geometry luôn diễn ra trên main thread.

.. note::

    SceneTree không thread-safe. Việc parse source geometry từ SceneTree chỉ có thể được thực hiện trên main thread.

.. warning::

    Dữ liệu từ visual mesh và polygon cần được nhận từ GPU, khiến RenderingServer bị đình trệ trong quá trình này. Khi (re)baking tại runtime, nên ưu tiên sử dụng physics shape làm source geometry đã parse.

Source geometry được lưu bên trong các resource để geometry đã tạo có thể được tái sử dụng cho nhiều lần bake. Ví dụ, bake nhiều navigation mesh cho các kích thước agent khác nhau từ cùng một source geometry. Điều này cũng cho phép lưu source geometry vào ổ đĩa để có thể tải sau, chẳng hạn nhằm tránh chi phí parsing lại tại runtime.

Nhìn chung, dữ liệu geometry nên được giữ thật đơn giản. Có bao nhiêu cạnh cần thiết thì dùng bấy nhiêu, nhưng càng ít càng tốt. Đặc biệt trong 2D, nên tránh geometry bị trùng lặp và lồng nhau vì điều đó buộc phải tính toán lỗ polygon, có thể dẫn đến polygon bị lật. Một ví dụ về geometry lồng nhau là một shape StaticBody2D nhỏ hơn được đặt hoàn toàn bên trong phạm vi của một shape StaticBody2D khác.

Baking các chunk navigation mesh cho những thế giới lớn
-------------------------------------------------------

.. figure:: img/navmesh_chunk_build.gif
   :align: center
   :alt: Building navigation mesh chunks

   Building and updating individual navigation mesh chunks at runtime.

.. seealso::

    Bạn có thể xem quá trình baking chunk navigation mesh hoạt động trong các dự án demo `Navigation Mesh Chunks 2D <https://github.com/godotengine/godot-demo-projects/tree/master/2d/navigation_mesh_chunks>`__ và `Navigation Mesh Chunks 3D <https://github.com/godotengine/godot-demo-projects/tree/master/3d/navigation_mesh_chunks>`__.

Để tránh các cạnh bị lệch giữa những chunk vùng khác nhau, navigation mesh có hai thuộc tính quan trọng đối với quy trình bake navigation mesh: baking bound và kích thước border. Kết hợp với nhau, chúng có thể được dùng để bảo đảm các cạnh giữa những chunk vùng được căn chỉnh hoàn hảo.

.. figure:: img/navmesh_bound_bordersize.webp
   :align: center
   :alt: Navigation mesh chunk with bake bound and border size

   Navigation mesh chunk baked with bake bound or baked with additional border size.

Baking bound, là một :ref:`Rect2<class_Rect2>` căn chỉnh theo trục cho 2D và :ref:`AABB<class_AABB>` cho 3D, giới hạn geometry nguồn được sử dụng bằng cách loại bỏ toàn bộ geometry nằm ngoài bound.

Các thuộc tính :ref:`NavigationPolygon<class_NavigationPolygon>` ``baking_rect`` và ``baking_rect_offset`` có thể được dùng để tạo và đặt baking bound 2D.

Các thuộc tính :ref:`NavigationMesh<class_NavigationMesh>` ``filter_baking_aabb`` và ``filter_baking_aabb_offset`` có thể được dùng để tạo và đặt baking bound 3D.

Ngay cả khi chỉ thiết lập baking bound, vẫn còn một vấn đề khác. Navigation mesh kết quả chắc chắn sẽ bị ảnh hưởng bởi các offset cần thiết như ``agent_radius``, khiến các cạnh không được căn chỉnh đúng.

.. figure:: img/navmesh_chunk_gaps.webp
   :align: center
   :alt: Navigation mesh chunks with gaps

   Navigation mesh chunks with noticeable gaps due to baked agent radius offset.

Đây là lúc thuộc tính ``border_size`` của navigation mesh phát huy tác dụng. Kích thước border là một lề hướng vào trong tính từ baking bound. Đặc điểm quan trọng của kích thước border là nó không bị ảnh hưởng bởi hầu hết offset và quá trình hậu xử lý như ``agent_radius``.

Thay vì loại bỏ geometry nguồn, kích thước border sẽ loại bỏ các phần của bề mặt cuối cùng của navigation mesh đã bake. Nếu baking bound đủ lớn, kích thước border có thể loại bỏ các phần bề mặt có vấn đề để chỉ còn lại kích thước chunk mong muốn.

.. figure:: img/navmesh_chunks.webp
   :align: center
   :alt: Navigation mesh chunks without gaps

   Navigation mesh chunks with aligned edges and without gaps.

.. note::

    Các baking bound cần đủ lớn để bao gồm một lượng geometry nguồn hợp lý từ tất cả các chunk lân cận.

.. warning::

    Trong 3D, chức năng của kích thước border bị giới hạn trên trục xz.

Các vấn đề thường gặp khi bake navigation mesh
----------------------------------------------

Có một số vấn đề thường gặp của người dùng và các điểm cần lưu ý quan trọng khi tạo hoặc bake navigation mesh.

- Bake navigation mesh gây ra vấn đề về frame rate khi runtime Việc bake navigation mesh mặc định được thực hiện trên một background thread, vì vậy miễn là platform hỗ trợ thread, quá trình bake thực tế hiếm khi là nguồn gây ra vấn đề hiệu năng (với điều kiện geometry có kích thước và độ phức tạp hợp lý cho việc rebake khi runtime).

    Nguồn phổ biến gây ra vấn đề hiệu năng khi runtime là bước phân tích geometry nguồn, trong đó có các node và SceneTree. SceneTree không an toàn khi chạy trên thread, vì vậy tất cả node cần được phân tích trên main thread. Một số node chứa nhiều dữ liệu có thể rất nặng và chậm khi phân tích lúc runtime; ví dụ, một TileMap có một hoặc nhiều polygon cho mỗi cell và TileMapLayer được sử dụng cần phân tích. Các node chứa mesh cần yêu cầu dữ liệu từ RenderingServer, làm đình trệ quá trình render.

    Để cải thiện hiệu năng, hãy sử dụng các shape được tối ưu hơn, chẳng hạn collision shape thay cho mesh hiển thị chi tiết, đồng thời gộp và đơn giản hóa nhiều geometry nhất có thể ngay từ đầu. Nếu không cách nào hiệu quả, đừng phân tích SceneTree mà hãy thêm geometry nguồn theo cách procedural bằng script. Nếu chỉ sử dụng các mảng dữ liệu thuần túy làm geometry nguồn, toàn bộ quá trình bake có thể được thực hiện trên một background thread.

- Navigation mesh tạo ra các lỗ ngoài ý muốn trong 2D. Việc bake navigation mesh trong 2D được thực hiện bằng các thao tác cắt polygon dựa trên các đường outline. Polygon có "lỗ" là một điều bất đắc dĩ cần thiết để tạo các polygon 2D phức tạp hơn, nhưng có thể trở nên khó đoán đối với người dùng khi có nhiều shape phức tạp tham gia.

    Để tránh các vấn đề không mong muốn khi tính toán lỗ của polygon, hãy tránh lồng bất kỳ outline nào bên trong các outline khác cùng loại (có thể đi qua / vật cản). Điều này bao gồm cả các shape được phân tích từ node. Ví dụ, đặt một shape StaticBody2D nhỏ hơn bên trong một shape StaticBody2D lớn hơn có thể khiến polygon kết quả bị đảo chiều.

- Navigation mesh xuất hiện bên trong geometry trong 3D. Việc bake navigation mesh trong 3D không có khái niệm "bên trong". Các voxel cell được dùng để rasterize geometry либо được chiếm giữ hoặc không. Hãy xóa geometry nằm trên mặt đất bên trong geometry khác. Nếu không thể làm vậy, hãy thêm geometry "dummy" nhỏ hơn vào bên trong với số triangle ít nhất có thể để các cell được chiếm giữ bởi một thứ gì đó.

    Có thể sử dụng một shape :ref:`NavigationObstacle3D<class_NavigationObstacle3D>` được đặt để bake cùng navigation mesh nhằm loại bỏ geometry.

.. figure:: img/nav_mesh_obstacles_discard.webp
   :align: center
   :alt: NavigationObstacle3D unwanted geometry discard

   A NavigationObstacle3D shape can be used to discard unwanted navigation mesh parts.

Các template script cho navigation mesh
---------------------------------------

Script sau sử dụng NavigationServer để phân tích geometry nguồn từ scene tree, bake một navigation mesh và cập nhật một navigation region bằng navigation mesh đã được cập nhật.

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

        # Bật region và đặt nó vào navigation map mặc định.
        NavigationServer2D.region_set_enabled(region_rid, true)
        NavigationServer2D.region_set_map(region_rid, get_world_2d().get_navigation_map())

        # Một số mega-node như TileMap thường chưa sẵn sàng ở frame đầu tiên.
        # Ngoài ra, việc phân tích cần diễn ra trên main thread.
        # Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
        parse_source_geometry.call_deferred()

    func parse_source_geometry() -> void:
        source_geometry.clear()
        var root_node: Node2D = self

        # Mặc định, phân tích các outline vật cản từ tất cả node con của node gốc.
        NavigationServer2D.parse_source_geometry_data(
            navigation_mesh,
            source_geometry,
            root_node,
            callback_parsing
        )

    func on_parsing_done() -> void:
        # Nếu chúng ta không phân tích một TileMap có các cell navigation mesh, lúc này có thể chúng ta chỉ
        # có các outline vật cản, vì vậy hãy thêm ít nhất một outline có thể đi qua
        # để các outline vật cản có thứ gì đó để "cắt" vào.
        source_geometry.add_traversable_outline(PackedVector2Array([
            Vector2(0.0, 0.0),
            Vector2(500.0, 0.0),
            Vector2(500.0, 500.0),
            Vector2(0.0, 500.0)
        ]))

        # Bake navigation mesh trên một thread bằng dữ liệu geometry nguồn.
        NavigationServer2D.bake_from_source_geometry_data_async(
            navigation_mesh,
            source_geometry,
            callback_baking
        )

    func on_baking_done() -> void:
        # Cập nhật region bằng navigation mesh đã được cập nhật.
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

            // Bật region và đặt nó vào navigation map mặc định.
            NavigationServer2D.RegionSetEnabled(_regionRid, true);
            NavigationServer2D.RegionSetMap(_regionRid, GetWorld2D().NavigationMap);

            // Một số mega-node như TileMap thường chưa sẵn sàng ở frame đầu tiên.
            // Ngoài ra, việc phân tích cần diễn ra trên main thread.
            // Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
            CallDeferred(MethodName.ParseSourceGeometry);
        }

        private void ParseSourceGeometry()
        {
            _sourceGeometry.Clear();
            Node2D rootNode = this;

            // Mặc định, phân tích các outline vật cản từ tất cả node con của node gốc.
            NavigationServer2D.ParseSourceGeometryData(
                _navigationMesh,
                _sourceGeometry,
                rootNode,
                _callbackParsing
            );
        }

        private void OnParsingDone()
        {
            // Nếu chúng ta không phân tích một TileMap có các cell navigation mesh, lúc này có thể chúng ta chỉ
            // có các outline vật cản, vì vậy hãy thêm ít nhất một outline có thể đi qua
            // để các outline vật cản có thứ gì đó để "cắt" vào.
            _sourceGeometry.AddTraversableOutline(
            [
                new Vector2(0.0f, 0.0f),
                new Vector2(500.0f, 0.0f),
                new Vector2(500.0f, 500.0f),
                new Vector2(0.0f, 500.0f),
            ]);

            // Bake navigation mesh trên một thread bằng dữ liệu geometry nguồn.
            NavigationServer2D.BakeFromSourceGeometryDataAsync(_navigationMesh, _sourceGeometry, _callbackBaking);
        }

        private void OnBakingDone()
        {
            // Cập nhật region bằng navigation mesh đã được cập nhật.
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

        # Bật region và đặt nó vào navigation map mặc định.
        NavigationServer3D.region_set_enabled(region_rid, true)
        NavigationServer3D.region_set_map(region_rid, get_world_3d().get_navigation_map())

        # Một số mega-node như GridMap thường chưa sẵn sàng ở frame đầu tiên.
        # Ngoài ra, việc phân tích cần diễn ra trên main thread.
        # Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
        parse_source_geometry.call_deferred()

    func parse_source_geometry() -> void:
        source_geometry.clear()
        var root_node: Node3D = self

        # Mặc định, phân tích geometry từ tất cả node con chứa mesh của node gốc.
        NavigationServer3D.parse_source_geometry_data(
            navigation_mesh,
            source_geometry,
            root_node,
            callback_parsing
        )

    func on_parsing_done() -> void:
        # Bake navigation mesh trên một thread bằng dữ liệu geometry nguồn.
        NavigationServer3D.bake_from_source_geometry_data_async(
            navigation_mesh,
            source_geometry,
            callback_baking
        )

    func on_baking_done() -> void:
        # Cập nhật region bằng navigation mesh đã được cập nhật.
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

            // Bật region và đặt nó vào navigation map mặc định.
            NavigationServer3D.RegionSetEnabled(_regionRid, true);
            NavigationServer3D.RegionSetMap(_regionRid, GetWorld3D().NavigationMap);

            // Một số mega-node như GridMap thường chưa sẵn sàng ở frame đầu tiên.
            // Ngoài ra, việc phân tích cần diễn ra trên main thread.
            // Vì vậy, hãy thực hiện một deferred call để tránh các vấn đề phân tích thường gặp.
            CallDeferred(MethodName.ParseSourceGeometry);
        }

        private void ParseSourceGeometry ()
        {
            _sourceGeometry.Clear();
            Node3D rootNode = this;

            // Mặc định, phân tích geometry từ tất cả node con chứa mesh của node gốc.
            NavigationServer3D.ParseSourceGeometryData(
                _navigationMesh,
                _sourceGeometry,
                rootNode,
                _callbackParsing
            );
        }

        private void OnParsingDone()
        {
            // Bake navigation mesh trên một thread bằng dữ liệu geometry nguồn.
            NavigationServer3D.BakeFromSourceGeometryDataAsync(_navigationMesh, _sourceGeometry, _callbackBaking);
        }

        private void OnBakingDone()
        {
            // Cập nhật region bằng navigation mesh đã được cập nhật.
            NavigationServer3D.RegionSetNavigationMesh(_regionRid, _navigationMesh);
        }
    }

Script sau sử dụng NavigationServer để cập nhật một navigation region bằng dữ liệu navigation mesh được tạo theo cách procedural.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends Node2D

    var navigation_mesh: NavigationPolygon
    var region_rid: RID

    func _ready() -> void:
        navigation_mesh = NavigationPolygon.new()
        region_rid = NavigationServer2D.region_create()

        # Bật region và đặt nó vào navigation map mặc định.
        NavigationServer2D.region_set_enabled(region_rid, true)
        NavigationServer2D.region_set_map(region_rid, get_world_2d().get_navigation_map())

        # Thêm các vertex cho một polygon lồi.
        navigation_mesh.vertices = PackedVector2Array([
            Vector2(0.0, 0.0),
            Vector2(100.0, 0.0),
            Vector2(100.0, 100.0),
            Vector2(0.0, 100.0),
        ])

        # Thêm các index cho polygon.
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

            // Bật region và đặt nó vào navigation map mặc định.
            NavigationServer2D.RegionSetEnabled(_regionRid, true);
            NavigationServer2D.RegionSetMap(_regionRid, GetWorld2D().NavigationMap);

            // Thêm các vertex cho một polygon lồi.
            _navigationMesh.Vertices =
            [
                new Vector2(0, 0),
                new Vector2(100.0f, 0),
                new Vector2(100.0f, 100.0f),
                new Vector2(0, 100.0f),
            ];

            // Thêm các index cho polygon.
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

        # Bật region và đặt nó vào navigation map mặc định.
        NavigationServer3D.region_set_enabled(region_rid, true)
        NavigationServer3D.region_set_map(region_rid, get_world_3d().get_navigation_map())

        # Thêm các vertex cho một polygon lồi.
        navigation_mesh.vertices = PackedVector3Array([
            Vector3(-1.0, 0.0, 1.0),
            Vector3(1.0, 0.0, 1.0),
            Vector3(1.0, 0.0, -1.0),
            Vector3(-1.0, 0.0, -1.0),
        ])

        # Thêm các index cho polygon.
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

            // Bật region và đặt nó vào navigation map mặc định.
            NavigationServer3D.RegionSetEnabled(_regionRid, true);
            NavigationServer3D.RegionSetMap(_regionRid, GetWorld3D().NavigationMap);

            // Thêm các vertex cho một polygon lồi.
            _navigationMesh.Vertices =
            [
                new Vector3(-1.0f, 0.0f, 1.0f),
                new Vector3(1.0f, 0.0f, 1.0f),
                new Vector3(1.0f, 0.0f, -1.0f),
                new Vector3(-1.0f, 0.0f, -1.0f),
            ];

            // Thêm các index cho polygon.
            _navigationMesh.AddPolygon([0, 1, 2, 3]);

            NavigationServer3D.RegionSetNavigationMesh(_regionRid, _navigationMesh);
        }
    }
