.. _doc_navigation_overview_2d:

Tổng quan về điều hướng 2D
==========================

Godot cung cấp nhiều object, class và server để hỗ trợ điều hướng và tìm đường dựa trên lưới hoặc mesh cho game 2D và 3D. Phần sau đây cung cấp tổng quan nhanh về tất cả các object liên quan đến điều hướng hiện có trong Godot dành cho scene 2D và mục đích sử dụng chính của chúng.

Godot cung cấp các object và class sau cho điều hướng 2D:

- :ref:`Astar2D<class_Astar2D>` ``Astar2D`` object cung cấp tùy chọn tìm đường đi ngắn nhất trong một graph gồm các **điểm** có trọng số.

    Class AStar2D phù hợp nhất với gameplay 2D dựa trên cell, trong đó không yêu cầu actor phải đến được mọi vị trí có thể trong một khu vực mà chỉ đến các vị trí riêng biệt, được định nghĩa trước.

- :ref:`AstarGrid2D<class_AstarGrid2D>` ``AstarGrid2D`` là một biến thể của AStar2D, được chuyên biệt hóa cho các lưới 2D không đầy đủ.

    AstarGrid2D dễ sử dụng hơn trong những trường hợp phù hợp vì bạn không cần tự tạo các điểm và kết nối chúng với nhau.

- :ref:`NavigationServer2D<class_NavigationServer2D>` ``NavigationServer2D`` cung cấp một server API mạnh mẽ để tìm đường đi ngắn nhất giữa hai vị trí trong một khu vực được xác định bởi navigation mesh.

    NavigationServer phù hợp nhất với gameplay 2D realtime yêu cầu actor phải đến được mọi vị trí có thể trong khu vực được xác định bởi navigation mesh. Điều hướng dựa trên mesh mở rộng tốt với các thế giới game lớn, vì một khu vực rộng thường có thể được xác định bằng một polygon duy nhất, trong khi cách này sẽ yêu cầu rất nhiều cell của lưới.

    NavigationServer quản lý các navigation map khác nhau, mỗi map bao gồm các region chứa dữ liệu navigation mesh. Các agent có thể được đặt trên một map để tính toán avoidance. RID được sử dụng để tham chiếu các map, region và agent nội bộ khi giao tiếp với server.

    Các loại NavigationServer RID sau đây hiện có. - NavMap RID Tham chiếu đến một navigation map cụ thể chứa các region và agent. Map sẽ cố gắng kết hợp các navigation mesh của các region dựa trên khoảng cách gần nhau. Map sẽ đồng bộ các region và agent trong mỗi physics frame. - NavRegion RID Tham chiếu đến một navigation region cụ thể có thể chứa dữ liệu navigation mesh. Region có thể được bật / tắt hoặc bị hạn chế sử dụng bằng navigation layer bitmask. - NavLink RID Tham chiếu đến một navigation link cụ thể kết nối hai vị trí trên navigation mesh với khoảng cách tùy ý. - NavAgent RID Tham chiếu đến một avoidance agent cụ thể. Avoidance được xác định bằng một giá trị bán kính. - NavObstacle RID Tham chiếu đến một avoidance obstacle cụ thể, được sử dụng để tác động và giới hạn vận tốc avoidance của các agent.

Các node trong scene tree sau đây hiện có để hỗ trợ làm việc với NavigationServer2D API.

- :ref:`NavigationRegion2D<class_NavigationRegion2D>` Node Một Node chứa resource NavigationPolygon xác định navigation mesh cho NavigationServer2D.

    - Region có thể được bật / tắt. - Việc sử dụng trong pathfinding có thể được hạn chế thêm thông qua bitmask ``navigation_layers``. - NavigationServer2D sẽ kết hợp các navigation mesh của các region dựa trên khoảng cách gần nhau để tạo thành một navigation mesh hợp nhất.

- :ref:`NavigationLink2D<class_NavigationLink2D>` Node Một Node kết nối hai vị trí trên navigation mesh với khoảng cách tùy ý để pathfinding.

    - Link có thể được bật / tắt. - Link có thể là một chiều hoặc hai chiều. - Việc sử dụng trong pathfinding có thể được hạn chế thêm thông qua bitmask ``navigation_layers``.

    Link cho pathfinding biết rằng một kết nối tồn tại và chi phí của kết nối đó là bao nhiêu. Việc thực sự xử lý và di chuyển actor cần được thực hiện trong các script tùy chỉnh.

-  :ref:`NavigationAgent2D<class_NavigationAgent2D>` Node Một Node hỗ trợ thực hiện các lệnh gọi NavigationServer2D API phổ biến cho pathfinding và avoidance. Sử dụng Node này với một Node cha kế thừa từ Node2D.

-  :ref:`NavigationObstacle2D<class_NavigationObstacle2D>` Node Một Node có thể được sử dụng để tác động và giới hạn vận tốc avoidance của các agent đã bật avoidance. Node này KHÔNG tác động đến pathfinding của các agent. Thay vào đó, bạn cần thay đổi navigation mesh.

Navigation mesh 2D được xác định bằng các resource sau:

- :ref:`NavigationPolygon<class_NavigationPolygon>` Resource Một resource chứa dữ liệu navigation mesh 2D. Resource này cung cấp các công cụ vẽ polygon, cho phép xác định các khu vực điều hướng trong Editor cũng như tại runtime.

    - Node NavigationRegion2D sử dụng resource này để xác định khu vực điều hướng của nó. - NavigationServer2D sử dụng resource này để cập nhật navigation mesh của từng region. - TileSet Editor tạo và sử dụng resource này nội bộ khi xác định các khu vực điều hướng của tile.

.. seealso::

    Bạn có thể xem cách điều hướng 2D hoạt động trong thực tế thông qua các project demo `2D Navigation Polygon <https://github.com/godotengine/godot-demo-projects/tree/master/2d/navigation>`__ và `Grid-based Navigation with AStarGrid2D <https://github.com/godotengine/godot-demo-projects/tree/master/2d/navigation_astar>`__.

Thiết lập cho scene 2D
----------------------

Các bước sau đây trình bày cách thiết lập cơ bản để có navigation khả dụng tối thiểu trong 2D. Cách này sử dụng NavigationServer2D và NavigationAgent2D để di chuyển theo đường đi.

#. Thêm một Node NavigationRegion2D vào scene.

#. Nhấp vào node region và thêm một Resource NavigationPolygon mới vào node region.

   .. image:: img/nav_2d_min_setup_step1.png

#. Xác định khu vực điều hướng có thể di chuyển bằng công cụ vẽ NavigationPolygon. Sau đó nhấp vào nút :button:`Bake NavigationPolygon` trên thanh công cụ.

   .. image:: img/nav_2d_min_setup_step2.png

   .. note::

        Navigation mesh xác định khu vực mà actor có thể đứng và di chuyển bằng tâm của nó. Hãy chừa đủ khoảng cách giữa các cạnh của navigation polygon và các object collision để actor đi theo đường đi không bị mắc kẹt liên tục trên collision.

#. Thêm một node CharacterBody2D vào scene với collision shape cơ bản và một sprite hoặc mesh để hiển thị.

#. Thêm một node NavigationAgent2D bên dưới node character.

   .. image:: img/nav_2d_min_setup_step3.webp

#. Thêm script sau vào node CharacterBody2D. Chúng ta đảm bảo đặt movement target sau khi scene đã tải hoàn tất và NavigationServer có thời gian đồng bộ.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var movement_speed: float = 200.0
    var movement_target_position: Vector2 = Vector2(60.0,180.0)

    @onready var navigation_agent: NavigationAgent2D = $NavigationAgent2D

    func _ready():
        # Các giá trị này cần được điều chỉnh theo tốc độ của actor
        # và bố cục navigation.
        navigation_agent.path_desired_distance = 4.0
        navigation_agent.target_desired_distance = 4.0

        # Đảm bảo không await trong _ready.
        actor_setup.call_deferred()

    func actor_setup():
        # Chờ physics frame đầu tiên để NavigationServer có thể đồng bộ.
        await get_tree().physics_frame

        # Giờ navigation map không còn trống, hãy đặt movement target.
        set_movement_target(movement_target_position)

    func set_movement_target(movement_target: Vector2):
        navigation_agent.target_position = movement_target

    func _physics_process(delta):
        if navigation_agent.is_navigation_finished():
            return

        var current_agent_position: Vector2 = global_position
        var next_path_position: Vector2 = navigation_agent.get_next_path_position()

        velocity = current_agent_position.direction_to(next_path_position) * movement_speed
        move_and_slide()

 .. code-tab:: csharp C#

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        private NavigationAgent2D _navigationAgent;

        private float _movementSpeed = 200.0f;
        private Vector2 _movementTargetPosition = new Vector2(70.0f, 226.0f);

        public Vector2 MovementTarget
        {
            get { return _navigationAgent.TargetPosition; }
            set { _navigationAgent.TargetPosition = value; }
        }

        public override void _Ready()
        {
            base._Ready();

            _navigationAgent = GetNode<NavigationAgent2D>("NavigationAgent2D");

            // Các giá trị này cần được điều chỉnh theo tốc độ của actor
            // và bố cục navigation.
            _navigationAgent.PathDesiredDistance = 4.0f;
            _navigationAgent.TargetDesiredDistance = 4.0f;

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

            Vector2 currentAgentPosition = GlobalTransform.Origin;
            Vector2 nextPathPosition = _navigationAgent.GetNextPathPosition();

            Velocity = currentAgentPosition.DirectionTo(nextPathPosition) * _movementSpeed;
            MoveAndSlide();
        }

        private async void ActorSetup()
        {
            // Chờ physics frame đầu tiên để NavigationServer có thể đồng bộ.
            await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

            // Giờ navigation map không còn trống, hãy đặt movement target.
            MovementTarget = _movementTargetPosition;
        }
    }

.. note::

    Ở frame đầu tiên, map của NavigationServer chưa đồng bộ dữ liệu region và mọi truy vấn đường đi sẽ trả về kết quả trống. Hãy chờ NavigationServer đồng bộ bằng cách await một frame trong script.
