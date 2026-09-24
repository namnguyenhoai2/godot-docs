.. _doc_navigation_overview_3d:

Tổng quan về điều hướng 3D
==========================

Godot cung cấp nhiều đối tượng, class và server để hỗ trợ điều hướng và tìm đường dựa trên grid hoặc mesh cho game 2D và 3D. Phần sau đây cung cấp tổng quan nhanh về tất cả các đối tượng liên quan đến điều hướng hiện có trong Godot dành cho các scene 3D và công dụng chính của chúng.

Godot cung cấp các đối tượng và class sau cho điều hướng 3D:

- :ref:`Astar3D<class_Astar3D>`
    Các đối tượng ``Astar3D`` cung cấp tùy chọn tìm đường đi ngắn nhất trong một graph gồm các **điểm** có trọng số.

    Class AStar3D phù hợp nhất cho gameplay 3D dựa trên cell, không yêu cầu actor tiếp cận mọi vị trí có thể trong một khu vực mà chỉ cần tiếp cận các vị trí riêng biệt được định trước.

- :ref:`NavigationServer3D<class_NavigationServer3D>`
    ``NavigationServer3D`` cung cấp một server API mạnh mẽ để tìm đường đi ngắn nhất giữa hai vị trí trong một khu vực được xác định bởi navigation mesh.

    NavigationServer phù hợp nhất cho gameplay 3D realtime, trong đó actor cần tiếp cận mọi vị trí có thể trong một khu vực được xác định bởi navigation mesh. Điều hướng dựa trên mesh có khả năng mở rộng tốt với các thế giới game lớn, vì một khu vực rộng thường có thể được xác định bằng một polygon duy nhất, trong khi sẽ cần rất nhiều grid cell.

    NavigationServer lưu giữ các navigation map khác nhau, mỗi map gồm các region chứa dữ liệu navigation mesh. Có thể đặt agent trên một map để tính toán tránh né. RID được dùng để tham chiếu các map, region và agent nội bộ khi giao tiếp với server.

    Có các loại NavigationServer RID sau.
        - NavMap RID
            Tham chiếu đến một navigation map cụ thể chứa các region và agent. Map sẽ cố gắng nối các navigation mesh của các region dựa trên khoảng cách gần nhau. Map sẽ đồng bộ các region và agent trong mỗi frame vật lý.
        - NavRegion RID
            Tham chiếu đến một navigation region cụ thể có thể chứa dữ liệu navigation mesh. Region có thể được bật / tắt hoặc giới hạn việc sử dụng bằng navigation layer bitmask.
        - NavLink RID
            Tham chiếu đến một navigation link cụ thể, kết nối hai vị trí trên navigation mesh qua khoảng cách tùy ý.
        - NavAgent RID
            Tham chiếu đến một avoidance agent cụ thể. Việc tránh né được xác định bằng một giá trị bán kính.
        - NavObstacle RID
            Tham chiếu đến một avoidance obstacle cụ thể, được dùng để tác động và giới hạn vận tốc tránh né của các agent.

Các node trong scene tree sau đây có sẵn dưới dạng helper để làm việc với NavigationServer3D API.

- Node :ref:`NavigationRegion3D<class_NavigationRegion3D>`
    Một Node chứa tài nguyên Navigation Mesh xác định navigation mesh cho NavigationServer3D.

    - Region có thể được bật / tắt.
    - Việc sử dụng trong quá trình tìm đường có thể được giới hạn thêm thông qua bitmask ``navigation_layers``.
    - NavigationServer3D sẽ nối các navigation mesh của các region dựa trên khoảng cách gần nhau để tạo thành một navigation mesh kết hợp.

- Node :ref:`NavigationLink3D<class_NavigationLink3D>`
    Một Node kết nối hai vị trí trên navigation mesh qua khoảng cách tùy ý để tìm đường.

    - Link có thể được bật / tắt.
    - Link có thể được thiết lập một chiều hoặc hai chiều.
    - Việc sử dụng trong quá trình tìm đường có thể được giới hạn thêm thông qua bitmask ``navigation_layers``.

    Link cho quá trình tìm đường biết rằng có một kết nối tồn tại và chi phí của kết nối đó. Việc xử lý và di chuyển agent thực tế cần được thực hiện trong các script tùy chỉnh.

-  Node :ref:`NavigationAgent3D<class_NavigationAgent3D>`
    Một Node helper được dùng để hỗ trợ các lệnh gọi NavigationServer3D API phổ biến cho việc tìm đường và tránh né. Sử dụng Node này với một Node cha kế thừa từ Node3D.

-  Node :ref:`NavigationObstacle3D<class_NavigationObstacle3D>`
    Một Node có thể được dùng để tác động và giới hạn vận tốc tránh né của các agent đã bật tính năng tránh né. Node này KHÔNG tác động đến việc tìm đường của agent. Thay vào đó, bạn cần thay đổi các navigation mesh.

Navigation mesh 3D được xác định bằng các resource sau:

- Resource :ref:`NavigationMesh<class_NavigationMesh>`
    Một resource chứa dữ liệu navigation mesh 3D. Resource này cung cấp các tùy chọn baking hình học 3D để xác định các khu vực điều hướng trong Editor cũng như trong runtime.

    - Node NavigationRegion3D sử dụng resource này để xác định khu vực điều hướng của nó.
    - NavigationServer3D sử dụng resource này để cập nhật navigation mesh của từng region.
    - GridMap Editor sử dụng resource này khi các navigation mesh cụ thể được xác định cho từng grid cell.

.. seealso::

    Bạn có thể xem cách điều hướng 3D hoạt động thực tế trong project demo `3D Navigation demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/navigation>`__.

Thiết lập cho scene 3D
----------------------

Các bước sau đây trình bày cách thiết lập cơ bản để có điều hướng tối thiểu khả dụng trong 3D. Thiết lập này sử dụng NavigationServer3D và NavigationAgent3D để di chuyển theo đường đi.

#. Thêm một Node NavigationRegion3D vào scene.

#. Nhấp vào region node và thêm một :ref:`NavigationMesh<class_NavigationMesh>` Resource mới vào region node.

   .. image:: img/nav_3d_min_setup_step1.png

#. Thêm một node MeshInstance3D mới làm node con của region node.

#. Chọn node MeshInstance3D, thêm một PlaneMesh mới và tăng kích thước xy lên 10.

#. Chọn lại region node và nhấn nút "Bake Navmesh" trên thanh trên cùng.

   .. image:: img/nav_3d_min_setup_step2.png

#. Lúc này, một navigation mesh trong suốt xuất hiện, nằm lơ lửng cách một khoảng phía trên PlaneMesh.

   .. image:: img/nav_3d_min_setup_step3.png

#. Thêm một node CharacterBody3D vào scene với một collision shape cơ bản và một mesh để hiển thị.

#. Thêm một node NavigationAgent3D bên dưới node character.

   .. image:: img/nav_3d_min_setup_step4.webp

#. Thêm một script vào node CharacterBody3D với nội dung sau. Chúng ta đảm bảo đặt movement target sau khi scene đã tải hoàn toàn và NavigationServer đã có thời gian đồng bộ. Ngoài ra, thêm một Camera3D cùng một số ánh sáng và environment để có thể quan sát được.

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
        # Chờ khung hình vật lý đầu tiên để NavigationServer có thể đồng bộ.
        await get_tree().physics_frame

        # Giờ bản đồ điều hướng không còn trống, hãy đặt mục tiêu di chuyển.
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
            // Chờ khung hình vật lý đầu tiên để NavigationServer có thể đồng bộ.
            await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

            // Giờ bản đồ điều hướng không còn trống, hãy đặt mục tiêu di chuyển.
            MovementTarget = _movementTargetPosition;
        }
    }

.. note::

    Ở khung hình đầu tiên, bản đồ NavigationServer chưa đồng bộ dữ liệu vùng, vì vậy mọi truy vấn đường đi sẽ trả về kết quả trống. Hãy chờ NavigationServer đồng bộ bằng cách await một khung hình trong script.
