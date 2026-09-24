.. _doc_navigation_overview_2d:

Tổng quan về điều hướng 2D
==========================

Godot cung cấp nhiều đối tượng, lớp và server để hỗ trợ điều hướng và tìm đường dựa trên lưới hoặc mesh cho game 2D và 3D. Phần sau đây cung cấp tổng quan nhanh về tất cả các đối tượng liên quan đến điều hướng hiện có trong Godot dành cho scene 2D và mục đích sử dụng chính của chúng.

Godot cung cấp các đối tượng và lớp sau đây cho điều hướng 2D:

- :ref:`Astar2D<class_Astar2D>`
    Các đối tượng ``Astar2D`` cung cấp tùy chọn tìm đường đi ngắn nhất trong một đồ thị gồm các **điểm** có trọng số.

    Lớp AStar2D phù hợp nhất cho gameplay 2D dựa trên ô, không yêu cầu actor có thể đến mọi vị trí trong một khu vực mà chỉ đến các vị trí riêng biệt, được xác định trước.

- :ref:`AstarGrid2D<class_AstarGrid2D>`
    ``AstarGrid2D`` là một biến thể của AStar2D, được chuyên biệt hóa cho các lưới 2D không đầy đủ.

    AstarGrid2D dễ sử dụng hơn khi phù hợp, vì bạn không cần tự tạo các điểm và kết nối chúng với nhau.

- :ref:`NavigationServer2D<class_NavigationServer2D>`
    ``NavigationServer2D`` cung cấp một server API mạnh mẽ để tìm đường đi ngắn nhất giữa hai vị trí trong một khu vực được xác định bởi navigation mesh.

    NavigationServer phù hợp nhất cho gameplay 2D theo thời gian thực, trong đó actor cần đến mọi vị trí có thể có trong một khu vực được xác định bởi navigation mesh. Điều hướng dựa trên mesh có khả năng mở rộng tốt với các thế giới game lớn, vì một khu vực rộng thường có thể được xác định bằng một polygon duy nhất, trong khi cách này sẽ cần rất nhiều ô lưới.

    NavigationServer chứa các navigation map khác nhau, mỗi map gồm các region chứa dữ liệu navigation mesh. Có thể đặt các agent lên một map để tính toán tránh né. RID được dùng để tham chiếu đến các map, region và agent nội bộ khi giao tiếp với server.

    Các loại NavigationServer RID sau đây hiện có.
        - NavMap RID
            Tham chiếu đến một navigation map cụ thể chứa các region và agent. Map sẽ cố gắng nối các navigation mesh của các region dựa trên khoảng cách. Map sẽ đồng bộ các region và agent ở mỗi khung vật lý.
        - NavRegion RID
            Tham chiếu đến một navigation region cụ thể có thể chứa dữ liệu navigation mesh. Region có thể được bật / tắt hoặc giới hạn phạm vi sử dụng bằng bitmask của navigation layer.
        - NavLink RID
            Tham chiếu đến một navigation link cụ thể, kết nối hai vị trí trên navigation mesh qua các khoảng cách tùy ý.
        - NavAgent RID
            Tham chiếu đến một avoidance agent cụ thể. Việc tránh né được xác định bằng một giá trị bán kính.
        - NavObstacle RID
            Tham chiếu đến một avoidance obstacle cụ thể, được dùng để tác động và giới hạn vận tốc tránh né của các agent.

Các node sau trong scene tree hiện có để hỗ trợ làm việc với NavigationServer2D API.

- Node :ref:`NavigationRegion2D<class_NavigationRegion2D>`
    Một Node chứa tài nguyên NavigationPolygon, dùng để xác định navigation mesh cho NavigationServer2D.

    - Region có thể được bật / tắt.
    - Việc sử dụng trong tìm đường có thể được giới hạn thêm thông qua bitmask ``navigation_layers``.
    - NavigationServer2D sẽ nối các navigation mesh của các region dựa trên khoảng cách để tạo thành một navigation mesh hợp nhất.

- Node :ref:`NavigationLink2D<class_NavigationLink2D>`
    Một Node kết nối hai vị trí trên các navigation mesh qua các khoảng cách tùy ý để tìm đường.

    - Link có thể được bật / tắt.
    - Link có thể được đặt thành một chiều hoặc hai chiều.
    - Việc sử dụng trong tìm đường có thể được giới hạn thêm thông qua bitmask ``navigation_layers``.

    Các link cho hệ thống tìm đường biết rằng có một kết nối và chi phí của kết nối đó. Việc xử lý và di chuyển agent thực tế cần được thực hiện trong các script tùy chỉnh.

-  Node :ref:`NavigationAgent2D<class_NavigationAgent2D>`
    Một Node hỗ trợ, được dùng để tạo thuận tiện cho các lệnh gọi NavigationServer2D API phổ biến nhằm tìm đường và tránh né. Hãy sử dụng Node này cùng với một Node cha kế thừa từ Node2D.

-  Node :ref:`NavigationObstacle2D<class_NavigationObstacle2D>`
    Một Node có thể được dùng để tác động và giới hạn vận tốc tránh né của các agent đã bật tính năng tránh né. Node này KHÔNG ảnh hưởng đến việc tìm đường của agent. Thay vào đó, bạn cần thay đổi các navigation mesh.

Các navigation mesh 2D được xác định bằng các tài nguyên sau:

- Resource :ref:`NavigationPolygon<class_NavigationPolygon>`
    Một resource chứa dữ liệu navigation mesh 2D. Resource này cung cấp các công cụ vẽ polygon, cho phép xác định các khu vực điều hướng bên trong Editor cũng như trong runtime.

    - Node NavigationRegion2D sử dụng resource này để xác định khu vực điều hướng của nó.
    - NavigationServer2D sử dụng resource này để cập nhật navigation mesh của từng region.
    - TileSet Editor tạo và sử dụng resource này nội bộ khi xác định các khu vực điều hướng của tile.

.. seealso::

    Bạn có thể xem cách điều hướng 2D hoạt động trên thực tế qua các dự án demo `2D Navigation Polygon <https://github.com/godotengine/godot-demo-projects/tree/master/2d/navigation>`__ và `Grid-based Navigation with AStarGrid2D <https://github.com/godotengine/godot-demo-projects/tree/master/2d/navigation_astar>`__.

Thiết lập cho scene 2D
----------------------

Các bước sau đây trình bày cách thiết lập cơ bản để có chức năng điều hướng 2D tối thiểu nhưng hoạt động được. Cách này sử dụng NavigationServer2D và NavigationAgent2D để di chuyển theo đường đi.

#. Thêm một Node NavigationRegion2D vào scene.

#. Nhấp vào node region và thêm một Resource NavigationPolygon mới vào node region.

   .. image:: img/nav_2d_min_setup_step1.png

#. Xác định khu vực điều hướng có thể di chuyển bằng công cụ vẽ NavigationPolygon. Sau đó nhấp vào nút :button:`Bake NavigationPolygon` trên thanh công cụ.

   .. image:: img/nav_2d_min_setup_step2.png

   .. note::

        Navigation mesh xác định khu vực nơi actor có thể đứng và di chuyển bằng tâm của nó. Hãy chừa đủ khoảng cách giữa các cạnh của navigation polygon và các đối tượng va chạm để các actor đang đi theo đường không bị mắc kẹt liên tục khi va chạm.

#. Thêm một node CharacterBody2D vào scene với hình dạng va chạm cơ bản và một sprite hoặc mesh để hiển thị.

#. Thêm một node NavigationAgent2D bên dưới node character.

   .. image:: img/nav_2d_min_setup_step3.webp

#. Thêm script sau vào node CharacterBody2D. Chúng ta đảm bảo đặt mục tiêu di chuyển sau khi scene đã tải hoàn toàn và NavigationServer đã có thời gian đồng bộ.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var movement_speed: float = 200.0
    var movement_target_position: Vector2 = Vector2(60.0,180.0)

    @onready var navigation_agent: NavigationAgent2D = $NavigationAgent2D

    func _ready():
        # Các giá trị này cần được điều chỉnh theo tốc độ của actor
        # và bố cục điều hướng.
        navigation_agent.path_desired_distance = 4.0
        navigation_agent.target_desired_distance = 4.0

        # Đảm bảo không await trong _ready.
        actor_setup.call_deferred()

    func actor_setup():
        # Chờ frame vật lý đầu tiên để NavigationServer có thể đồng bộ.
        await get_tree().physics_frame

        # Giờ đây bản đồ điều hướng không còn trống, hãy đặt mục tiêu di chuyển.
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
            // và bố cục điều hướng.
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
            // Chờ frame vật lý đầu tiên để NavigationServer có thể đồng bộ.
            await ToSignal(GetTree(), SceneTree.SignalName.PhysicsFrame);

            // Giờ đây bản đồ điều hướng không còn trống, hãy đặt mục tiêu di chuyển.
            MovementTarget = _movementTargetPosition;
        }
    }

.. note::

    Ở frame đầu tiên, bản đồ NavigationServer chưa đồng bộ dữ liệu vùng, vì vậy mọi truy vấn đường đi sẽ trả về kết quả rỗng. Hãy chờ NavigationServer đồng bộ bằng cách await một frame trong script.
