.. _doc_navigation_overview_3d:

Tổng quan về điều hướng 3D
==========================

Godot cung cấp nhiều object, class và server để hỗ trợ điều hướng và tìm đường dựa trên lưới hoặc mesh cho game 2D và 3D. Phần sau đây cung cấp tổng quan nhanh về tất cả object liên quan đến điều hướng hiện có trong Godot dành cho các scene 3D và công dụng chính của chúng.

Godot cung cấp các object và class sau cho điều hướng 3D:

- :ref:`Astar3D<class_Astar3D>` ``Astar3D`` object cung cấp tùy chọn tìm đường đi ngắn nhất trong một graph gồm các **điểm** có trọng số.

    Class AStar3D phù hợp nhất với gameplay 3D dựa trên cell, trong đó không yêu cầu actor có thể đến bất kỳ vị trí nào trong một khu vực mà chỉ đến các vị trí riêng biệt, được định nghĩa trước.

- :ref:`NavigationServer3D<class_NavigationServer3D>` ``NavigationServer3D`` cung cấp một server API mạnh mẽ để tìm đường đi ngắn nhất giữa hai vị trí trong một khu vực được xác định bởi navigation mesh.

    NavigationServer phù hợp nhất với gameplay realtime 3D yêu cầu actor có thể đến bất kỳ vị trí nào trong khu vực được xác định bởi navigation mesh. Điều hướng dựa trên mesh có khả năng mở rộng tốt với các thế giới game lớn, vì một khu vực rộng thường có thể được xác định bằng một polygon duy nhất, trong khi cách này sẽ cần rất nhiều cell lưới.

    NavigationServer quản lý các navigation map khác nhau, mỗi map gồm các region chứa dữ liệu navigation mesh. Có thể đặt agent trên một map để tính toán tránh va chạm. RID được dùng để tham chiếu các map, region và agent nội bộ khi giao tiếp với server.

    Các loại NavigationServer RID sau đây hiện có. - NavMap RID Tham chiếu đến một navigation map cụ thể chứa các region và agent. Map sẽ cố gắng kết hợp navigation mesh của các region dựa trên khoảng cách gần nhau. Map sẽ đồng bộ các region và agent ở mỗi physics frame. - NavRegion RID Tham chiếu đến một navigation region cụ thể có thể chứa dữ liệu navigation mesh. Region có thể được bật / tắt hoặc giới hạn việc sử dụng bằng bitmask của navigation layer. - NavLink RID Tham chiếu đến một navigation link cụ thể kết nối hai vị trí trên navigation mesh qua các khoảng cách tùy ý. - NavAgent RID Tham chiếu đến một avoidance agent cụ thể. Việc tránh va chạm được xác định bằng giá trị bán kính. - NavObstacle RID Tham chiếu đến một avoidance obstacle cụ thể, được dùng để tác động và giới hạn vận tốc tránh va chạm của agent.

Các node trong scene tree sau đây có sẵn dưới dạng helper để làm việc với NavigationServer3D API.

- :ref:`NavigationRegion3D<class_NavigationRegion3D>` Node Một Node chứa resource Navigation Mesh, dùng để xác định navigation mesh cho NavigationServer3D.

    - Region có thể được bật / tắt. - Việc sử dụng trong quá trình tìm đường có thể được giới hạn thêm thông qua bitmask ``navigation_layers``. - NavigationServer3D sẽ kết hợp navigation mesh của các region dựa trên khoảng cách gần nhau để tạo thành một navigation mesh hợp nhất.

- :ref:`NavigationLink3D<class_NavigationLink3D>` Node Một Node kết nối hai vị trí trên navigation mesh qua các khoảng cách tùy ý để tìm đường.

    - Link có thể được bật / tắt. - Link có thể là một chiều hoặc hai chiều. - Việc sử dụng trong quá trình tìm đường có thể được giới hạn thêm thông qua bitmask ``navigation_layers``.

    Link cho hệ thống tìm đường biết rằng một kết nối tồn tại và chi phí của kết nối đó là bao nhiêu. Việc thực sự xử lý và di chuyển agent cần được thực hiện trong các script tùy chỉnh.

-  :ref:`NavigationAgent3D<class_NavigationAgent3D>` Node Một Node helper được dùng để hỗ trợ các lệnh gọi NavigationServer3D API phổ biến cho việc tìm đường và tránh va chạm. Sử dụng Node này với một Node cha kế thừa từ Node3D.

-  :ref:`NavigationObstacle3D<class_NavigationObstacle3D>` Node Một Node có thể được dùng để tác động và giới hạn vận tốc tránh va chạm của các agent đã bật tính năng tránh va chạm. Node này KHÔNG ảnh hưởng đến việc tìm đường của agent. Thay vào đó, bạn cần thay đổi navigation mesh.

Navigation mesh 3D được xác định bằng các resource sau:

- :ref:`NavigationMesh<class_NavigationMesh>` Resource Một resource chứa dữ liệu navigation mesh 3D. Resource này cung cấp các tùy chọn baking hình học 3D để xác định các khu vực điều hướng trong Editor cũng như tại runtime.

    - Node NavigationRegion3D sử dụng resource này để xác định khu vực điều hướng. - NavigationServer3D sử dụng resource này để cập nhật navigation mesh của từng region. - GridMap Editor sử dụng resource này khi các navigation mesh cụ thể được xác định cho từng cell của lưới.

.. seealso::

    Bạn có thể xem cách điều hướng 3D hoạt động trong thực tế bằng cách sử dụng `3D Navigation demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/navigation>`__.

Thiết lập cho scene 3D
----------------------

Các bước sau đây trình bày cách thiết lập cơ bản để có chức năng điều hướng tối thiểu trong 3D. Cách này sử dụng NavigationServer3D và NavigationAgent3D để di chuyển theo đường đi.

#. Thêm một Node NavigationRegion3D vào scene.

#. Nhấp vào node region và thêm một resource :ref:`NavigationMesh<class_NavigationMesh>` mới vào node region.

   .. image:: img/nav_3d_min_setup_step1.png

#. Thêm một node MeshInstance3D mới làm node con của node region.

#. Chọn node MeshInstance3D và thêm một PlaneMesh mới, sau đó tăng kích thước xy lên 10.

#. Chọn lại node region và nhấn nút "Bake Navmesh" trên thanh trên cùng.

   .. image:: img/nav_3d_min_setup_step2.png

#. Lúc này, một navigation mesh trong suốt sẽ xuất hiện, lơ lửng cách một khoảng phía trên PlaneMesh.

   .. image:: img/nav_3d_min_setup_step3.png

#. Thêm một node CharacterBody3D vào scene với một collision shape cơ bản và một mesh để hiển thị.

#. Thêm một node NavigationAgent3D bên dưới node character.

   .. image:: img/nav_3d_min_setup_step4.webp

#. Thêm một script vào node CharacterBody3D với nội dung sau. Chúng ta đảm bảo đặt movement target sau khi scene đã tải hoàn toàn và NavigationServer đã có thời gian đồng bộ. Ngoài ra, hãy thêm một Camera3D, một số nguồn sáng và environment để có thể nhìn thấy mọi thứ.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody3D

    var movement_speed: float = 2.0
    var movement_target_position: Vector3 = Vector3(-3.0,0.0,2.0)

    @onready var navigation_agent: NavigationAgent3D = $NavigationAgent3D

    func _ready():
        # Các giá trị này cần được điều chỉnh theo tốc độ của actor
        # và bố cục điều hướng.
        navigation_agent.path_desired_distance = 0.5
        navigation_agent.target_desired_distance = 0.5

        # Đảm bảo không await trong _ready.
        actor_setup.call_deferred()

    func actor_setup():
        # Chờ physics frame đầu tiên để NavigationServer có thể đồng bộ.
        await get_tree().physics_frame

        # Bây giờ navigation map không còn trống, hãy đặt movement target.
        set_movement_target(movement_target_position)

    func set_movement_target(movement_target: Vector3):
        navigation_agent.set_target_position(movement_target)

    func _physics_process(delta):
        if navigation_agent.is_navigation_finished():
            return

        var current_agent_position: Vector3 = global_position
        var next_path_position: Vector3 = navigation_agent.get_next_path_position()

        velocity = current_agent_position.direction_to(next_path_position) * movement_speed
        move_and_slide()

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyCharacterBody3D : CharacterBody3D
    {
        private NavigationAgent3D _navigationAgent;

        private float _movementSpeed = 2.0f;
        private Vector3 _movementTargetPosition = new Vector3(-3.0f, 0.0f, 2.0f);

        public Vector3 MovementTarget
        {
            get { return _navigationAgent.TargetPosition; }
            set { _navigationAgent.TargetPosition = value; }
        }

        public override void _Ready()
        {
            base._Ready();

            _navigationAgent = GetNode<NavigationAgent3D>("NavigationAgent3D");

            // Các giá trị này cần được điều chỉnh theo tốc độ của actor
            // và bố cục điều hướng.
            _navigationAgent.PathDesiredDistance = 0.5f;
            _navigationAgent.TargetDesiredDistance = 0.5f;

            // Đảm bảo không await trong _Ready.
            Callable.From(ActorSetup).CallDeferred();
        }

        public override void _PhysicsProcess(double delta)
        {
            base._PhysicsProcess(delta);

            if (_navigationAgent.IsNavigationFinished())
            {
                return;
            }

            Vector3 currentAgentPosition = GlobalTransform.Origin;
            Vector3 nextPathPosition = _navigationAgent.GetNextPathPosition();

            Velocity = currentAgentPosition.DirectionTo(nextPathPosition) * _movementSpeed;
            MoveAndSlide();
        }

        private async void ActorSetup()
        {
            // Chờ physics frame đầu tiên để NavigationServer có thể đồng bộ.
            await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

            // Bây giờ navigation map không còn trống, hãy đặt movement target.
            MovementTarget = _movementTargetPosition;
        }
    }

.. note::

    Trong frame đầu tiên, map của NavigationServer chưa đồng bộ dữ liệu region nên mọi truy vấn đường đi sẽ trả về kết quả trống. Hãy chờ NavigationServer đồng bộ bằng cách await một frame trong script.
