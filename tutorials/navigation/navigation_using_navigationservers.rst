.. _doc_navigation_using_navigationservers:

Sử dụng NavigationServer
========================

Phiên bản 2D và 3D của NavigationServer có sẵn dưới dạng
:ref:`NavigationServer2D<class_NavigationServer2D>` and
:ref:`NavigationServer3D<class_NavigationServer3D>` respectively.

Giao tiếp với NavigationServer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để làm việc với NavigationServer, bạn cần chuẩn bị các tham số cho một **truy vấn** có thể được gửi đến NavigationServer để cập nhật hoặc yêu cầu dữ liệu.

Để tham chiếu đến các đối tượng nội bộ của NavigationServer như map, region và agent, RID được sử dụng làm số nhận dạng. Mỗi node liên quan đến navigation trong scene tree đều có một hàm trả về RID của node đó.

Threading và đồng bộ hóa
~~~~~~~~~~~~~~~~~~~~~~~~

NavigationServer không cập nhật mọi thay đổi ngay lập tức mà chờ đến cuối **physics frame** để đồng bộ tất cả thay đổi cùng lúc.

Việc chờ đồng bộ hóa là cần thiết để áp dụng các thay đổi cho tất cả map, region và agent. Việc đồng bộ hóa được thực hiện vì một số cập nhật, chẳng hạn như tính toán lại toàn bộ navigation map, rất tốn tài nguyên và yêu cầu dữ liệu đã được cập nhật từ tất cả đối tượng khác. Ngoài ra, NavigationServer mặc định sử dụng **threadpool** cho một số chức năng như tính toán tránh va chạm giữa các agent.

Không cần chờ đối với hầu hết các hàm ``get()`` chỉ yêu cầu dữ liệu từ NavigationServer mà không tạo ra thay đổi. Lưu ý rằng không phải tất cả dữ liệu đều phản ánh các thay đổi được thực hiện trong cùng frame. Ví dụ: nếu một avoidance agent thay đổi navigation map trong frame này, hàm ``agent_get_map()`` vẫn sẽ trả về map cũ trước khi đồng bộ hóa. Ngoại lệ là các node lưu trữ giá trị của chúng nội bộ trước khi gửi bản cập nhật đến NavigationServer. Khi sử dụng getter trên một node để lấy giá trị đã được cập nhật trong cùng frame, getter sẽ trả về giá trị đã cập nhật được lưu trữ trên node.

NavigationServer **an toàn cho thread** vì nó đưa tất cả lời gọi API muốn tạo thay đổi vào một hàng đợi để thực thi trong giai đoạn đồng bộ hóa. Việc đồng bộ hóa cho NavigationServer diễn ra ở giữa physics frame, sau khi toàn bộ scene input từ script và node đã hoàn tất.

.. note::
    Điểm quan trọng cần nhớ là hầu hết thay đổi của NavigationServer có hiệu lực sau physics frame tiếp theo chứ không phải ngay lập tức. Điều này bao gồm tất cả thay đổi được thực hiện bởi các node liên quan đến navigation trong scene tree hoặc thông qua script.

.. note::
    Tất cả setter và hàm delete đều yêu cầu đồng bộ hóa.

Sự khác biệt giữa NavigationServer 2D và 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NavigationServer2D và NavigationServer3D có chức năng tương đương trong không gian tương ứng.

Về mặt kỹ thuật, có thể sử dụng các công cụ tạo navigation mesh trong một không gian cho không gian còn lại, ví dụ như bake navigation mesh 2D bằng NavigationMesh 3D khi sử dụng hình học nguồn 3D phẳng, hoặc tạo navigation mesh 3D phẳng bằng các công cụ vẽ polygon outline của NavigationRegion2D và NavigationPolygons.

Chờ đồng bộ hóa
~~~~~~~~~~~~~~~

Khi bắt đầu game, một scene mới hoặc các thay đổi navigation theo thủ tục sẽ khiến mọi truy vấn đường đi đến NavigationServer trả về kết quả rỗng hoặc sai.

Navigation map vẫn đang rỗng hoặc chưa được cập nhật tại thời điểm này. Trước tiên, tất cả node trong scene tree cần tải dữ liệu liên quan đến navigation của chúng lên NavigationServer. Mỗi map, region hoặc agent được thêm hoặc thay đổi đều cần được đăng ký với NavigationServer. Sau đó, NavigationServer cần một **physics frame** để đồng bộ hóa và cập nhật các map, region và agent.

Một cách khắc phục là thực hiện một lời gọi trì hoãn đến hàm setup tùy chỉnh (để tất cả node đều sẵn sàng). Hàm setup thực hiện mọi thay đổi navigation, chẳng hạn như thêm các thành phần được tạo theo thủ tục. Sau đó, hàm chờ đến physics frame tiếp theo trước khi tiếp tục với các truy vấn đường đi.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node3D

    func _ready():
        # Sử dụng call deferred để đảm bảo tất cả node trong scene tree đã được thiết lập
        # nếu không, await trên 'physics_frame' trong _ready() có thể bị kẹt.
        custom_setup.call_deferred()

    func custom_setup():

        # Tạo một navigation map mới.
        var map: RID = NavigationServer3D.map_create()
        NavigationServer3D.map_set_up(map, Vector3.UP)
        NavigationServer3D.map_set_active(map, true)

        # Tạo một navigation region mới và thêm nó vào map.
        var region: RID = NavigationServer3D.region_create()
        NavigationServer3D.region_set_transform(region, Transform3D())
        NavigationServer3D.region_set_map(region, map)

        # Tạo một navigation mesh theo thủ tục cho region.
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

        # Chờ NavigationServer đồng bộ để áp dụng các thay đổi đã thực hiện.
        await get_tree().physics_frame

        # Truy vấn đường đi từ navigation server.
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
            // Sử dụng call deferred để đảm bảo tất cả node trong scene tree đã được thiết lập
            // nếu không, await trên 'physics_frame' trong _Ready() có thể bị kẹt.
            CallDeferred(MethodName.CustomSetup);
        }

        private async void CustomSetup()
        {
            // Tạo một navigation map mới.
            Rid map = NavigationServer3D.MapCreate();
            NavigationServer3D.MapSetUp(map, Vector3.Up);
            NavigationServer3D.MapSetActive(map, true);

            // Tạo một navigation region mới và thêm nó vào map.
            Rid region = NavigationServer3D.RegionCreate();
            NavigationServer3D.RegionSetTransform(region, Transform3D.Identity);
            NavigationServer3D.RegionSetMap(region, map);

            // Tạo một navigation mesh theo thủ tục cho region.
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

            // Chờ NavigationServer đồng bộ để áp dụng các thay đổi đã thực hiện.
            await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

            // Truy vấn đường đi từ navigation server.
            var startPosition = new Vector3(0.1f, 0.0f, 0.1f);
            var targetPosition = new Vector3(1.0f, 0.0f, 1.0f);

            Vector3[] path = NavigationServer3D.MapGetPath(map, startPosition, targetPosition, optimize: true);

            GD.Print("Found a path!");
            GD.Print((Variant)path);
        }
    }

Callback tránh va chạm của Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu các avoidance agent RVO được đăng ký để nhận callback tránh va chạm, NavigationServer sẽ phân phối các signal ``velocity_computed`` của chúng ngay trước khi PhysicsServer đồng bộ hóa.

Để tìm hiểu thêm về NavigationAgents, hãy xem :ref:`doc_navigation_using_navigationagents`.

Thứ tự thực thi được đơn giản hóa đối với NavigationAgents sử dụng tính năng tránh va chạm:

- physics frame bắt đầu. - ``_physics_process(delta)``. - Thuộc tính ``velocity`` được thiết lập trên node NavigationAgent. - Agent gửi vận tốc và vị trí đến NavigationServer. - NavigationServer chờ đồng bộ hóa. - NavigationServer đồng bộ hóa và tính toán vận tốc tránh va chạm cho tất cả avoidance agent đã đăng ký. - NavigationServer gửi vector vận tốc an toàn cùng với signal cho từng avoidance agent đã đăng ký. - Các agent nhận signal và di chuyển parent của chúng, chẳng hạn bằng ``move_and_slide`` hoặc ``linear_velocity``. - PhysicsServer đồng bộ hóa. - physics frame kết thúc.

Do đó, việc di chuyển một physicsbody actor trong hàm callback bằng vận tốc an toàn là hoàn toàn an toàn đối với thread và physics, vì mọi việc diễn ra trong cùng một physics frame trước khi PhysicsServer ghi nhận các thay đổi và thực hiện các phép tính của riêng nó.
