.. _doc_navigation_using_navigationservers:

Sử dụng NavigationServer
========================

Các phiên bản 2D và 3D của NavigationServer có sẵn dưới dạng
:ref:`NavigationServer2D<class_NavigationServer2D>` và
:ref:`NavigationServer3D<class_NavigationServer3D>` tương ứng.

Giao tiếp với NavigationServer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Làm việc với NavigationServer nghĩa là chuẩn bị các tham số cho một **truy vấn** có thể được gửi đến NavigationServer để cập nhật hoặc yêu cầu dữ liệu.

Để tham chiếu đến các đối tượng nội bộ của NavigationServer như map, region và agent, RID được dùng làm số nhận dạng. Mỗi node liên quan đến navigation trong scene tree đều có một hàm trả về RID của node đó.

Luồng và đồng bộ hóa
~~~~~~~~~~~~~~~~~~~~

NavigationServer không cập nhật mọi thay đổi ngay lập tức mà chờ đến cuối **khung hình physics** để đồng bộ tất cả thay đổi cùng lúc.

Cần chờ đồng bộ hóa để áp dụng các thay đổi cho tất cả map, region và agent. Việc đồng bộ hóa được thực hiện vì một số cập nhật, chẳng hạn như tính toán lại toàn bộ navigation map, rất tốn tài nguyên và yêu cầu dữ liệu đã được cập nhật từ tất cả đối tượng khác. Ngoài ra, NavigationServer mặc định sử dụng một **threadpool** cho một số chức năng như tính toán tránh va chạm giữa các agent.

Không cần chờ đối với hầu hết các hàm ``get()`` chỉ yêu cầu dữ liệu từ NavigationServer mà không thực hiện thay đổi. Lưu ý rằng không phải tất cả dữ liệu đều tính đến các thay đổi được thực hiện trong cùng khung hình. Ví dụ, nếu một avoidance agent thay đổi navigation map trong khung hình này, hàm ``agent_get_map()`` vẫn sẽ trả về map cũ trước khi đồng bộ hóa. Ngoại lệ là các node lưu trữ giá trị nội bộ trước khi gửi bản cập nhật đến NavigationServer. Khi sử dụng getter trên một node cho giá trị được cập nhật trong cùng khung hình, hàm này sẽ trả về giá trị đã được cập nhật và lưu trữ trên node.

NavigationServer **thread-safe** vì nó đưa tất cả API call muốn thực hiện thay đổi vào một queue để thực thi trong giai đoạn đồng bộ hóa. Việc đồng bộ hóa cho NavigationServer diễn ra ở giữa khung hình physics, sau khi tất cả scene input từ script và node đã hoàn tất.

.. note::
    Điểm quan trọng cần ghi nhớ là hầu hết thay đổi của NavigationServer có hiệu lực sau khung hình physics tiếp theo chứ không phải ngay lập tức. Điều này bao gồm mọi thay đổi được thực hiện bởi các node liên quan đến navigation trong scene tree hoặc thông qua script.

.. note::
    Tất cả setter và hàm delete đều yêu cầu đồng bộ hóa.

Sự khác biệt giữa NavigationServer 2D và 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NavigationServer2D và NavigationServer3D có chức năng tương đương trong không gian tương ứng.

Về mặt kỹ thuật, có thể sử dụng các công cụ tạo navigation mesh trong một không gian cho không gian còn lại, chẳng hạn như bake navigation mesh 2D bằng 3D NavigationMesh khi sử dụng geometry nguồn 3D phẳng, hoặc tạo navigation mesh 3D phẳng bằng các công cụ vẽ polygon outline của NavigationRegion2D và NavigationPolygons.

Chờ đồng bộ hóa
~~~~~~~~~~~~~~~

Khi bắt đầu game, một scene mới hoặc sau khi thay đổi navigation theo cách thủ tục, mọi path query đến NavigationServer sẽ trả về kết quả rỗng hoặc sai.

Lúc này navigation map vẫn còn rỗng hoặc chưa được cập nhật. Trước tiên, tất cả node trong scene tree cần tải dữ liệu liên quan đến navigation của chúng lên NavigationServer. Mỗi map, region hoặc agent được thêm vào hay thay đổi đều cần được đăng ký với NavigationServer. Sau đó, NavigationServer cần một **khung hình physics** để đồng bộ hóa và cập nhật các map, region và agent.

Một cách khắc phục là gọi deferred đến một hàm thiết lập tùy chỉnh (để tất cả node đã sẵn sàng). Hàm thiết lập thực hiện mọi thay đổi navigation, chẳng hạn như thêm các thành phần được tạo theo cách thủ tục. Sau đó, hàm chờ đến khung hình physics tiếp theo trước khi tiếp tục thực hiện các path query.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node3D

    func _ready():
        # Sử dụng call deferred để đảm bảo toàn bộ node trong scene tree đã được thiết lập
        # nếu không, await trên 'physics_frame' trong _ready() có thể bị kẹt.
        custom_setup.call_deferred()

    func custom_setup():

        # Tạo một navigation map mới.
        var map: RID = NavigationServer3D.map_create()
        NavigationServer3D.map_set_up(map, Vector3.UP)
        NavigationServer3D.map_set_active(map, true)

        # Tạo một navigation region mới và thêm region đó vào map.
        var region: RID = NavigationServer3D.region_create()
        NavigationServer3D.region_set_transform(region, Transform3D())
        NavigationServer3D.region_set_map(region, map)

        # Tạo một navigation mesh theo cách thủ tục cho region.
        var new_navigation_mesh: NavigationMesh = NavigationMesh.new()
        var vertices: PackedVector3Array = PackedVector3Array([
            Vector3(0, 0, 0),
            Vector3(9.0, 0, 0),
            Vector3(0, 0, 9.0)
        ])
        new_navigation_mesh.set_vertices(vertices)
        var polygon: PackedInt32Array = PackedInt32Array([0, 1, 2])
        new_navigation_mesh.add_polygon(polygon)
        NavigationServer3D.region_set_navigation_mesh(region, new_navigation_mesh)

        # Chờ NavigationServer sync để thích ứng với các thay đổi đã thực hiện.
        await get_tree().physics_frame

        # Truy vấn path từ navigation server.
        var start_position: Vector3 = Vector3(0.1, 0.0, 0.1)
        var target_position: Vector3 = Vector3(1.0, 0.0, 1.0)
        var optimize_path: bool = true

        var path: PackedVector3Array = NavigationServer3D.map_get_path(
            map,
            start_position,
            target_position,
            optimize_path
        )

        print("Found a path!")
        print(path)

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            // Sử dụng call deferred để đảm bảo toàn bộ node trong scene tree đã được thiết lập
            // nếu không, await trên 'physics_frame' trong _Ready() có thể bị kẹt.
            CallDeferred(MethodName.CustomSetup);
        }

        private async void CustomSetup()
        {
            // Tạo một navigation map mới.
            Rid map = NavigationServer3D.MapCreate();
            NavigationServer3D.MapSetUp(map, Vector3.Up);
            NavigationServer3D.MapSetActive(map, true);

            // Tạo một navigation region mới và thêm region đó vào map.
            Rid region = NavigationServer3D.RegionCreate();
            NavigationServer3D.RegionSetTransform(region, Transform3D.Identity);
            NavigationServer3D.RegionSetMap(region, map);

            // Tạo một navigation mesh theo cách thủ tục cho region.
            var newNavigationMesh = new NavigationMesh()
            {
                Vertices =
                [
                    new Vector3(0.0f, 0.0f, 0.0f),
                    new Vector3(9.0f, 0.0f, 0.0f),
                    new Vector3(0.0f, 0.0f, 9.0f),
                ],
            };
            int[] polygon = [0, 1, 2];
            newNavigationMesh.AddPolygon(polygon);
            NavigationServer3D.RegionSetNavigationMesh(region, newNavigationMesh);

            // Chờ NavigationServer sync để thích ứng với các thay đổi đã thực hiện.
            await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

            // Truy vấn path từ navigation server.
            var startPosition = new Vector3(0.1f, 0.0f, 0.1f);
            var targetPosition = new Vector3(1.0f, 0.0f, 1.0f);

            Vector3[] path = NavigationServer3D.MapGetPath(map, startPosition, targetPosition, optimize: true);

            GD.Print("Found a path!");
            GD.Print((Variant)path);
        }
    }

Callback tránh va chạm của server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu các avoidance agent RVO được đăng ký để nhận callback tránh va chạm, NavigationServer sẽ dispatch các ``velocity_computed`` signal của chúng ngay trước khi PhysicsServer đồng bộ hóa.

Để tìm hiểu thêm về NavigationAgents, hãy xem :ref:`doc_navigation_using_navigationagents`.

Thứ tự thực thi đơn giản hóa đối với các NavigationAgents sử dụng avoidance:

- khung hình physics bắt đầu.
- ``_physics_process(delta)``.
- Thuộc tính ``velocity`` được thiết lập trên Node NavigationAgent.
- Agent gửi velocity và position đến NavigationServer.
- NavigationServer chờ đồng bộ hóa.
- NavigationServer đồng bộ hóa và tính toán velocity tránh va chạm cho tất cả avoidance agent đã đăng ký.
- NavigationServer gửi vector velocity an toàn kèm signal cho từng avoidance agent đã đăng ký.
- Các agent nhận tín hiệu và di chuyển đối tượng cha của chúng, chẳng hạn bằng ``move_and_slide`` hoặc ``linear_velocity``.
- PhysicsServer thực hiện đồng bộ hóa.
- khung hình vật lý kết thúc.

Do đó, việc di chuyển một physicsbody actor trong hàm callback bằng vận tốc an toàn là hoàn toàn an toàn về thread và vật lý, vì mọi thứ đều diễn ra trong cùng một khung hình vật lý, trước khi PhysicsServer ghi nhận các thay đổi và thực hiện các phép tính riêng của nó.
