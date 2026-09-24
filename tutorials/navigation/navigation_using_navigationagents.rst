.. _doc_navigation_using_navigationagents:

Sử dụng NavigationAgents
========================

NavigationAgents là các node trợ giúp kết hợp chức năng tìm đường, bám theo đường đi và tránh tác nhân cho node cha kế thừa Node2D/3D. Chúng thực hiện các lệnh gọi phổ biến đến API NavigationServer thay cho node tác nhân cha theo cách thuận tiện hơn cho người mới bắt đầu.

Phiên bản 2D và 3D của NavigationAgents có sẵn dưới dạng
:ref:`NavigationAgent2D<class_NavigationAgent2D>` và
:ref:`NavigationAgent3D<class_NavigationAgent3D>` tương ứng.

Các node NavigationAgent mới sẽ tự động tham gia bản đồ navigation mặc định trên :ref:`World2D<class_World2D>`/:ref:`World3D<class_World3D>`.

Các node NavigationAgent là tùy chọn và không bắt buộc để sử dụng hệ thống navigation. Toàn bộ chức năng của chúng có thể được thay thế bằng các script và các lệnh gọi trực tiếp đến API NavigationServer.

.. tip::

    Đối với các trường hợp sử dụng nâng cao hơn, hãy cân nhắc :ref:`doc_navigation_using_navigationpathqueryobjects` thay cho các node NavigationAgent.

Tìm đường bằng NavigationAgent
------------------------------

NavigationAgents truy vấn một đường đi navigation mới trên bản đồ navigation hiện tại của chúng khi ``target_position`` được đặt bằng một vị trí toàn cục.

Kết quả tìm đường có thể bị ảnh hưởng bởi các thuộc tính sau.

- Bitmask ``navigation_layers`` có thể được sử dụng để giới hạn các navigation mesh mà tác nhân có thể dùng.
- ``pathfinding_algorithm`` kiểm soát cách tìm đường đi qua các polygon của navigation mesh trong quá trình tìm đường.
- ``path_postprocessing`` xác định liệu và bằng cách nào hành lang đường đi thô được tìm thấy bởi quá trình tìm đường sẽ được thay đổi trước khi trả về.
- ``path_metadata_flags`` cho phép thu thập siêu dữ liệu bổ sung của các điểm trên đường đi được đường đi trả về.
- Các thuộc tính ``simplify_path`` và ``simplify_epsilon`` có thể được sử dụng để loại bỏ các điểm ít quan trọng hơn khỏi đường đi.

.. warning::

    Việc tắt các cờ siêu dữ liệu đường đi sẽ tắt các lần phát signal liên quan trên tác nhân.

Bám theo đường đi bằng NavigationAgent
--------------------------------------

Sau khi ``target_position`` được đặt cho tác nhân, có thể lấy vị trí tiếp theo cần bám theo trên đường đi bằng hàm ``get_next_path_position()``.

Sau khi nhận được vị trí tiếp theo trên đường đi, hãy dùng mã chuyển động của riêng bạn để di chuyển node tác nhân cha của tác nhân về phía vị trí này.

.. note::

    Hệ thống navigation không bao giờ di chuyển node cha của NavigationAgent. Chuyển động hoàn toàn do người dùng và các script tùy chỉnh của họ kiểm soát.

NavigationAgents có logic nội bộ riêng để tiếp tục đi theo đường đi hiện tại và yêu cầu các bản cập nhật.

Hàm ``get_next_path_position()`` chịu trách nhiệm cập nhật nhiều trạng thái và thuộc tính nội bộ của tác nhân. Hàm này cần được gọi lặp lại *once* mỗi ``physics_process`` cho đến khi ``is_navigation_finished()`` cho biết đường đi đã hoàn tất. Không nên gọi hàm này sau khi đã đến vị trí đích hoặc điểm cuối đường đi, vì các lần cập nhật đường đi lặp lại có thể khiến tác nhân rung tại chỗ. Luôn kiểm tra từ rất sớm trong script bằng ``is_navigation_finished()`` xem đường đi đã hoàn tất hay chưa.

Các thuộc tính khoảng cách sau đây ảnh hưởng đến hành vi bám theo đường đi.

- Khi cách vị trí tiếp theo trên đường đi ``path_desired_distance``, tác nhân tiến chỉ mục đường đi nội bộ đến vị trí tiếp theo sau đó.
- Khi cách vị trí đường đi đích ``target_desired_distance``, tác nhân xem vị trí đích đã đạt được và đường đi đã kết thúc.
- Khi cách đường đi lý tưởng đến vị trí tiếp theo trên đường đi ``path_max_distance``, tác nhân yêu cầu một đường đi mới vì đã bị đẩy lệch quá xa.

Tất cả các bản cập nhật quan trọng đều được kích hoạt bằng hàm ``get_next_path_position()`` khi được gọi trong ``_physics_process()``.

NavigationAgents có thể được sử dụng với ``process`` nhưng vẫn bị giới hạn ở một lần cập nhật duy nhất diễn ra trong ``physics_process``.

Các ví dụ script cho nhiều node thường được sử dụng cùng NavigationAgents có thể được tìm thấy ở phần bên dưới.

Các vấn đề thường gặp khi bám theo đường đi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một số vấn đề thường gặp của người dùng và các lưu ý quan trọng cần cân nhắc khi viết script chuyển động cho tác nhân.

- Đường đi được trả về rỗng
    Nếu tác nhân truy vấn đường đi trước khi quá trình đồng bộ hóa bản đồ navigation hoàn tất, chẳng hạn trong hàm ``_ready()``, đường đi có thể được trả về rỗng. Trong trường hợp này, hàm ``get_next_path_position()`` sẽ trả về cùng vị trí với node cha của tác nhân và tác nhân sẽ xem như đã đến cuối đường đi. Có thể khắc phục bằng cách thực hiện lệnh gọi trì hoãn hoặc sử dụng callback, chẳng hạn như chờ signal navigation map changed.

- Tác nhân bị kẹt, liên tục di chuyển qua lại giữa hai vị trí
    Điều này thường do đường đi được cập nhật quá thường xuyên ở mỗi frame, dù cố ý hay vô tình (chẳng hạn max path distance được đặt quá ngắn). Quá trình tìm đường cần tìm vị trí gần nhất hợp lệ trên navigation mesh. Nếu yêu cầu đường đi mới ở mỗi frame, các vị trí đầu tiên trên đường đi có thể liên tục chuyển đổi giữa phía trước và phía sau vị trí hiện tại của tác nhân, khiến tác nhân di chuyển qua lại giữa hai vị trí.

- Tác nhân đôi khi đi lùi
    Nếu tác nhân di chuyển quá nhanh, nó có thể vượt qua bước kiểm tra path_desired_distance mà không bao giờ tiến chỉ mục đường đi. Điều này có thể khiến tác nhân quay lại điểm trên đường đi hiện đang ở phía sau nó cho đến khi vượt qua bước kiểm tra khoảng cách để tăng chỉ mục đường đi. Việc tăng các khoảng cách mong muốn tương ứng với tốc độ và tần suất cập nhật của tác nhân thường cũng khắc phục được vấn đề này, cũng như việc bố trí các polygon của navigation mesh cân bằng hơn, không có quá nhiều cạnh polygon chen chúc trong không gian nhỏ.

- Tác nhân đôi khi nhìn về phía sau trong một frame
    Tương tự như trường hợp tác nhân bị kẹt khi di chuyển qua lại giữa hai vị trí, điều này thường do đường đi được cập nhật quá thường xuyên ở mỗi frame. Tùy thuộc vào bố cục navigation mesh của bạn, đặc biệt khi tác nhân được đặt trực tiếp trên một cạnh navigation mesh hoặc kết nối cạnh, hãy dự kiến rằng các vị trí trên đường đi đôi khi sẽ hơi "ở phía sau" hướng hiện tại của tác nhân. Điều này xảy ra do các vấn đề về độ chính xác và không phải lúc nào cũng có thể tránh được. Đây thường chỉ là vấn đề có thể nhìn thấy khi các tác nhân được xoay ngay lập tức để hướng về vị trí hiện tại trên đường đi.

Tránh va chạm bằng NavigationAgent
----------------------------------

Phần này giải thích cách sử dụng tính năng tránh va chạm dành riêng cho NavigationAgents.

Để NavigationAgents sử dụng tính năng tránh va chạm, thuộc tính ``avoidance_enabled`` phải được đặt thành ``true``.

.. image:: img/agent_avoidance_enabled.png

Signal ``velocity_computed`` của node NavigationAgent phải được kết nối để nhận kết quả tính toán vận tốc an toàn.

.. image:: img/agent_safevelocity_signal.png

Đặt ``velocity`` của node NavigationAgent trong ``_physics_process()`` để cập nhật agent với vận tốc hiện tại của node cha của agent.

Khi avoidance được bật trên agent, vector ``safe_velocity`` sẽ được nhận cùng signal velocity_computed ở mỗi khung hình vật lý. Vector vận tốc này nên được dùng để di chuyển node cha của NavigationAgent nhằm tránh va chạm với các agent khác đang sử dụng avoidance hoặc các chướng ngại vật avoidance.

.. note::

    Chỉ những agent khác trên cùng map đã đăng ký avoidance cho chính chúng mới được xem xét trong phép tính avoidance.

.. note::

    NavigationAgent **must** được cung cấp thuộc tính ``target_position``, ngay cả khi bạn chỉ sử dụng agent cho avoidance. Nếu không, ``safe_velocity`` nhận được từ signal ``velocity_computed`` sẽ luôn là vector không.

Các thuộc tính NavigationAgent sau đây liên quan đến avoidance:

  - Thuộc tính ``height`` chỉ khả dụng trong 3D. Chiều cao cùng với vị trí global hiện tại trên trục y của agent xác định vị trí theo chiều dọc của agent trong mô phỏng avoidance. Các agent sử dụng avoidance 2D sẽ tự động bỏ qua những agent hoặc chướng ngại vật nằm bên dưới hoặc bên trên chúng.
  - Thuộc tính ``radius`` kiểm soát bán kính của vòng tròn avoidance, hoặc hình cầu trong 3D, xung quanh agent. Khu vực này mô tả phần thân của agent chứ không phải khoảng cách di chuyển để avoidance.
  - Thuộc tính ``neighbor_distance`` kiểm soát bán kính tìm kiếm của agent khi tìm những agent khác cần tránh. Giá trị thấp hơn sẽ giảm chi phí xử lý.
  - Thuộc tính ``max_neighbors`` kiểm soát số lượng agent khác được xem xét trong phép tính avoidance nếu tất cả chúng có bán kính chồng lấn. Giá trị thấp hơn sẽ giảm chi phí xử lý, nhưng giá trị quá thấp có thể khiến các agent bỏ qua avoidance.
  - Các thuộc tính ``time_horizon_agents`` và ``time_horizon_obstacles`` kiểm soát thời gian dự đoán avoidance đối với các agent hoặc chướng ngại vật khác, tính bằng giây. Khi tính toán vận tốc an toàn, các agent chọn những vận tốc có thể được duy trì trong khoảng thời gian này mà không va chạm với một đối tượng avoidance khác. Nên giữ thời gian dự đoán ở mức thấp nhất có thể, vì các agent sẽ giảm vận tốc để tránh va chạm trong khoảng thời gian đó.
  - Thuộc tính ``max_speed`` kiểm soát vận tốc tối đa được phép trong phép tính avoidance của agent. Nếu node cha của agent di chuyển nhanh hơn giá trị này, ``safe_velocity`` avoidance có thể không đủ chính xác để tránh va chạm.
  - Thuộc tính ``use_3d_avoidance`` chuyển agent giữa avoidance 2D (trục xz) và avoidance 3D (trục xyz) ở lần cập nhật tiếp theo. Lưu ý rằng avoidance 2D và avoidance 3D chạy trong các mô phỏng avoidance riêng biệt, vì vậy các agent được chia giữa chúng sẽ không ảnh hưởng lẫn nhau.
  - Các thuộc tính ``avoidance_layers`` và ``avoidance_mask`` là các bitmask tương tự như, chẳng hạn, các physics layer. Các agent sẽ chỉ tránh những đối tượng avoidance khác nằm trên avoidance layer khớp với ít nhất một bit trong avoidance mask của chúng.
  - ``avoidance_priority`` khiến các agent có độ ưu tiên cao hơn bỏ qua các agent có độ ưu tiên thấp hơn. Điều này có thể được dùng để tăng mức độ quan trọng của một số agent trong mô phỏng avoidance, chẳng hạn như các non-playable character quan trọng, mà không cần liên tục thay đổi toàn bộ avoidance layer hoặc mask của chúng.


Avoidance tồn tại trong không gian riêng và không có thông tin từ navigation mesh hoặc va chạm vật lý. Phía sau màn hình, các agent avoidance chỉ là những hình tròn có bán kính khác nhau trên một mặt phẳng 2D hoặc những hình cầu trong một không gian 3D trống rỗng. Có thể dùng NavigationObstacles để thêm một số ràng buộc môi trường vào mô phỏng avoidance, xem :ref:`doc_navigation_using_navigationobstacles`.

.. note::

    Avoidance không ảnh hưởng đến pathfinding. Nên xem đây là một tùy chọn bổ sung cho các đối tượng di chuyển liên tục, không thể (tái) bake vào navigation mesh một cách hiệu quả để di chuyển vòng quanh chúng.

.. note::

    RVO avoidance đưa ra các giả định ngầm về hành vi tự nhiên của agent. Chẳng hạn, các agent di chuyển về những phía tránh nhau hợp lý có thể được xác định khi chúng gặp nhau. Điều này có nghĩa là các kịch bản kiểm thử avoidance quá máy móc thường sẽ thất bại. Chẳng hạn, các agent di chuyển trực tiếp về phía nhau với vận tốc đối nghịch hoàn toàn sẽ thất bại vì các agent không thể xác định được phía tránh của mình.

Sử dụng thuộc tính ``avoidance_enabled`` của NavigationAgent là tùy chọn được ưu tiên để bật hoặc tắt avoidance. Có thể dùng các đoạn mã sau để bật avoidance trên các agent, tạo hoặc xóa callback avoidance, hoặc chuyển đổi chế độ avoidance.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends NavigationAgent2D

    func _ready() -> void:
        var agent: RID = get_rid()
        # Bật avoidance
        NavigationServer2D.agent_set_avoidance_enabled(agent, true)
        # Tạo callback avoidance
        NavigationServer2D.agent_set_avoidance_callback(agent, Callable(self, "_avoidance_done"))

        # Tắt avoidance
        NavigationServer2D.agent_set_avoidance_enabled(agent, false)
        # Xóa callback avoidance
        NavigationServer2D.agent_set_avoidance_callback(agent, Callable())

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNavigationAgent2D : NavigationAgent2D
    {
        public override void _Ready()
        {
            Rid agent = GetRid();
            // Bật avoidance
            NavigationServer2D.AgentSetAvoidanceEnabled(agent, true);
            // Tạo callback avoidance
            NavigationServer2D.AgentSetAvoidanceCallback(agent, Callable.From(AvoidanceDone));

            // Tắt avoidance
            NavigationServer2D.AgentSetAvoidanceEnabled(agent, false);
            //Xóa callback avoidance
            NavigationServer2D.AgentSetAvoidanceCallback(agent, default);
        }

        private void AvoidanceDone() { }
    }

 .. code-tab:: gdscript 3D GDScript

    extends NavigationAgent3D

    func _ready() -> void:
        var agent: RID = get_rid()
        # Bật avoidance
        NavigationServer3D.agent_set_avoidance_enabled(agent, true)
        # Tạo callback avoidance
        NavigationServer3D.agent_set_avoidance_callback(agent, Callable(self, "_avoidance_done"))
        # Chuyển sang avoidance 3D
        NavigationServer3D.agent_set_use_3d_avoidance(agent, true)

        # Tắt avoidance
        NavigationServer3D.agent_set_avoidance_enabled(agent, false)
        # Xóa callback avoidance
        NavigationServer3D.agent_set_avoidance_callback(agent, Callable())
        # Chuyển sang avoidance 2D
        NavigationServer3D.agent_set_use_3d_avoidance(agent, false)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNavigationAgent3D : NavigationAgent3D
    {
        public override void _Ready()
        {
            Rid agent = GetRid();
            // Bật avoidance
            NavigationServer3D.AgentSetAvoidanceEnabled(agent, true);
            // Tạo callback avoidance
            NavigationServer3D.AgentSetAvoidanceCallback(agent, Callable.From(AvoidanceDone));
            // Chuyển sang avoidance 3D
            NavigationServer3D.AgentSetUse3DAvoidance(agent, true);

            // Tắt avoidance
            NavigationServer3D.AgentSetAvoidanceEnabled(agent, false);
            //Xóa callback avoidance
            NavigationServer3D.AgentSetAvoidanceCallback(agent, default);
            // Chuyển sang avoidance 2D
            NavigationServer3D.AgentSetUse3DAvoidance(agent, false);
        }

        private void AvoidanceDone() { }
    }

Mẫu script NavigationAgent
--------------------------

Các phần sau cung cấp các mẫu script cho những node thường được dùng với NavigationAgent.

.. tabs::

   .. tab:: GDScript 2D

      .. tabs::

         .. code-tab:: gdscript Node2D

            extends Node2D

            @export var movement_speed: float = 4.0
            @onready var navigation_agent: NavigationAgent2D = get_node("NavigationAgent2D")
            var movement_delta: float

            func _ready() -> void:
                navigation_agent.velocity_computed.connect(Callable(_on_velocity_computed))

            func set_movement_target(movement_target: Vector2):
                navigation_agent.set_target_position(movement_target)

            func _physics_process(delta):
                # Không truy vấn khi map chưa từng được đồng bộ hóa và đang trống.
                if NavigationServer2D.map_get_iteration_id(navigation_agent.get_navigation_map()) == 0:
                    return
                if navigation_agent.is_navigation_finished():
                    return

                movement_delta = movement_speed * delta
                var next_path_position: Vector2 = navigation_agent.get_next_path_position()
                var new_velocity: Vector2 = global_position.direction_to(next_path_position) * movement_delta
                if navigation_agent.avoidance_enabled:
                    navigation_agent.set_velocity(new_velocity)
                else:
                    _on_velocity_computed(new_velocity)

            func _on_velocity_computed(safe_velocity: Vector2) -> void:
                global_position = global_position.move_toward(global_position + safe_velocity, movement_delta)

         .. code-tab:: gdscript CharacterBody2D

            extends CharacterBody2D

            @export var movement_speed: float = 4.0
            @onready var navigation_agent: NavigationAgent2D = get_node("NavigationAgent2D")

            func _ready() -> void:
                navigation_agent.velocity_computed.connect(Callable(_on_velocity_computed))

            func set_movement_target(movement_target: Vector2):
                navigation_agent.set_target_position(movement_target)

            func _physics_process(delta):
                # Không truy vấn khi map chưa từng được đồng bộ hóa và đang trống.
                if NavigationServer2D.map_get_iteration_id(navigation_agent.get_navigation_map()) == 0:
                    return
                if navigation_agent.is_navigation_finished():
                    return

                var next_path_position: Vector2 = navigation_agent.get_next_path_position()
                var new_velocity: Vector2 = global_position.direction_to(next_path_position) * movement_speed
                if navigation_agent.avoidance_enabled:
                    navigation_agent.set_velocity(new_velocity)
                else:
                    _on_velocity_computed(new_velocity)

            func _on_velocity_computed(safe_velocity: Vector2):
                velocity = safe_velocity
                move_and_slide()

         .. code-tab:: gdscript RigidBody2D

            extends RigidBody2D

            @export var movement_speed: float = 4.0
            @onready var navigation_agent: NavigationAgent2D = get_node("NavigationAgent2D")

            func _ready() -> void:
                navigation_agent.velocity_computed.connect(Callable(_on_velocity_computed))

            func set_movement_target(movement_target: Vector2):
                navigation_agent.set_target_position(movement_target)

            func _physics_process(delta):
                # Không truy vấn khi map chưa từng được đồng bộ hóa và đang trống.
                if NavigationServer2D.map_get_iteration_id(navigation_agent.get_navigation_map()) == 0:
                    return
                if navigation_agent.is_navigation_finished():
                    return

                var next_path_position: Vector2 = navigation_agent.get_next_path_position()
                var new_velocity: Vector2 = global_position.direction_to(next_path_position) * movement_speed
                if navigation_agent.avoidance_enabled:
                    navigation_agent.set_velocity(new_velocity)
                else:
                    _on_velocity_computed(new_velocity)

            func _on_velocity_computed(safe_velocity: Vector2):
                linear_velocity = safe_velocity

   .. tab:: 2D C#

      .. tabs::

         .. code-tab:: csharp Node2D

            using Godot;

            public partial class MyNode2D : Node2D
            {
                [Export]
                public float MovementSpeed { get; set; } = 4.0f;
                NavigationAgent2D _navigationAgent;
                private float _movementDelta;

                public override void _Ready()
                {
                    _navigationAgent = GetNode<NavigationAgent2D>("NavigationAgent2D");
                    _navigationAgent.VelocityComputed += OnVelocityComputed;
                }

                private void SetMovementTarget(Vector2 movementTarget)
                {
                    _navigationAgent.TargetPosition = movementTarget;
                }

                public override void _PhysicsProcess(double delta)
                {
                    // Không truy vấn khi bản đồ chưa bao giờ đồng bộ hóa và đang trống.
                    if (NavigationServer2D.MapGetIterationId(_navigationAgent.GetNavigationMap()) == 0)
                    {
                        return;
                    }

                    if (_navigationAgent.IsNavigationFinished())
                    {
                        return;
                    }

                    _movementDelta = MovementSpeed * (float)delta;
                    Vector2 nextPathPosition = _navigationAgent.GetNextPathPosition();
                    Vector2 newVelocity = GlobalPosition.DirectionTo(nextPathPosition) * _movementDelta;
                    if (_navigationAgent.AvoidanceEnabled)
                    {
                        _navigationAgent.Velocity = newVelocity;
                    }
                    else
                    {
                        OnVelocityComputed(newVelocity);
                    }
                }

                private void OnVelocityComputed(Vector2 safeVelocity)
                {
                    GlobalPosition = GlobalPosition.MoveToward(GlobalPosition + safeVelocity, _movementDelta);
                }
            }

         .. code-tab:: csharp CharacterBody2D

            using Godot;

            public partial class MyCharacterBody2D : CharacterBody2D
            {
                [Export]
                public float MovementSpeed { get; set; } = 4.0f;
                NavigationAgent2D _navigationAgent;

                public override void _Ready()
                {
                    _navigationAgent = GetNode<NavigationAgent2D>("NavigationAgent2D");
                    _navigationAgent.VelocityComputed += OnVelocityComputed;
                }

                private void SetMovementTarget(Vector2 movementTarget)
                {
                    _navigationAgent.TargetPosition = movementTarget;
                }

                public override void _PhysicsProcess(double delta)
                {
                    // Không truy vấn khi bản đồ chưa bao giờ đồng bộ hóa và đang trống.
                    if (NavigationServer2D.MapGetIterationId(_navigationAgent.GetNavigationMap()) == 0)
                    {
                        return;
                    }

                    if (_navigationAgent.IsNavigationFinished())
                    {
                        return;
                    }

                    Vector2 nextPathPosition = _navigationAgent.GetNextPathPosition();
                    Vector2 newVelocity = GlobalPosition.DirectionTo(nextPathPosition) * MovementSpeed;
                    if (_navigationAgent.AvoidanceEnabled)
                    {
                        _navigationAgent.Velocity = newVelocity;
                    }
                    else
                    {
                        OnVelocityComputed(newVelocity);
                    }
                }

                private void OnVelocityComputed(Vector2 safeVelocity)
                {
                    Velocity = safeVelocity;
                    MoveAndSlide();
                }
            }

         .. code-tab:: csharp RigidBody2D

            using Godot;

            public partial class MyRigidBody2D : RigidBody2D
            {
                [Export]
                public float MovementSpeed { get; set; } = 4.0f;
                NavigationAgent2D _navigationAgent;

                public override void _Ready()
                {
                    _navigationAgent = GetNode<NavigationAgent2D>("NavigationAgent2D");
                    _navigationAgent.VelocityComputed += OnVelocityComputed;
                }

                private void SetMovementTarget(Vector2 movementTarget)
                {
                    _navigationAgent.TargetPosition = movementTarget;
                }

                public override void _PhysicsProcess(double delta)
                {
                    // Không truy vấn khi bản đồ chưa bao giờ đồng bộ hóa và đang trống.
                    if (NavigationServer2D.MapGetIterationId(_navigationAgent.GetNavigationMap()) == 0)
                    {
                        return;
                    }

                    if (_navigationAgent.IsNavigationFinished())
                    {
                        return;
                    }

                    Vector2 nextPathPosition = _navigationAgent.GetNextPathPosition();
                    Vector2 newVelocity = GlobalPosition.DirectionTo(nextPathPosition) * MovementSpeed;
                    if (_navigationAgent.AvoidanceEnabled)
                    {
                        _navigationAgent.Velocity = newVelocity;
                    }
                    else
                    {
                        OnVelocityComputed(newVelocity);
                    }
                }

                private void OnVelocityComputed(Vector2 safeVelocity)
                {
                    LinearVelocity = safeVelocity;
                }
            }

   .. tab:: 3D GDScript

      .. tabs::

         .. code-tab:: gdscript Node3D

            extends Node3D

            @export var movement_speed: float = 4.0
            @onready var navigation_agent: NavigationAgent3D = get_node("NavigationAgent3D")
            var physics_delta: float

            func _ready() -> void:
                navigation_agent.velocity_computed.connect(Callable(_on_velocity_computed))

            func set_movement_target(movement_target: Vector3):
                navigation_agent.set_target_position(movement_target)

            func _physics_process(delta):
                # Lưu delta để sử dụng trong _on_velocity_computed.
                physics_delta = delta
                # Không truy vấn khi map chưa từng được đồng bộ hóa và đang trống.
                if NavigationServer3D.map_get_iteration_id(navigation_agent.get_navigation_map()) == 0:
                    return
                if navigation_agent.is_navigation_finished():
                    return

                var next_path_position: Vector3 = navigation_agent.get_next_path_position()
                var new_velocity: Vector3 = global_position.direction_to(next_path_position) * movement_speed
                if navigation_agent.avoidance_enabled:
                    navigation_agent.set_velocity(new_velocity)
                else:
                    _on_velocity_computed(new_velocity)

            func _on_velocity_computed(safe_velocity: Vector3) -> void:
                global_position = global_position.move_toward(global_position + safe_velocity, physics_delta * movement_speed)

         .. code-tab:: gdscript CharacterBody3D

            extends CharacterBody3D

            @export var movement_speed: float = 4.0
            @onready var navigation_agent: NavigationAgent3D = get_node("NavigationAgent3D")

            func _ready() -> void:
                navigation_agent.velocity_computed.connect(Callable(_on_velocity_computed))

            func set_movement_target(movement_target: Vector3):
                navigation_agent.set_target_position(movement_target)

            func _physics_process(delta):
                # Không truy vấn khi map chưa từng được đồng bộ hóa và đang trống.
                if NavigationServer3D.map_get_iteration_id(navigation_agent.get_navigation_map()) == 0:
                    return
                if navigation_agent.is_navigation_finished():
                    return

                var next_path_position: Vector3 = navigation_agent.get_next_path_position()
                var new_velocity: Vector3 = global_position.direction_to(next_path_position) * movement_speed
                if navigation_agent.avoidance_enabled:
                    navigation_agent.set_velocity(new_velocity)
                else:
                    _on_velocity_computed(new_velocity)

            func _on_velocity_computed(safe_velocity: Vector3):
                velocity = safe_velocity
                move_and_slide()

         .. code-tab:: gdscript RigidBody3D

            extends RigidBody3D

            @export var movement_speed: float = 4.0
            @onready var navigation_agent: NavigationAgent3D = get_node("NavigationAgent3D")

            func _ready() -> void:
                navigation_agent.velocity_computed.connect(Callable(_on_velocity_computed))

            func set_movement_target(movement_target: Vector3):
                navigation_agent.set_target_position(movement_target)

            func _physics_process(delta):
                # Không truy vấn khi map chưa từng được đồng bộ hóa và đang trống.
                if NavigationServer3D.map_get_iteration_id(navigation_agent.get_navigation_map()) == 0:
                    return
                if navigation_agent.is_navigation_finished():
                    return

                var next_path_position: Vector3 = navigation_agent.get_next_path_position()
                var new_velocity: Vector3 = global_position.direction_to(next_path_position) * movement_speed
                if navigation_agent.avoidance_enabled:
                    navigation_agent.set_velocity(new_velocity)
                else:
                    _on_velocity_computed(new_velocity)

            func _on_velocity_computed(safe_velocity: Vector3):
                linear_velocity = safe_velocity

   .. tab:: 3D C#

      .. tabs::

         .. code-tab:: csharp Node3D

            using Godot;

            public partial class MyNode3D : Node3D
            {
                [Export]
                public float MovementSpeed { get; set; } = 4.0f;
                NavigationAgent3D _navigationAgent;
                private float _movementDelta;

                public override void _Ready()
                {
                    _navigationAgent = GetNode<NavigationAgent3D>("NavigationAgent3D");
                    _navigationAgent.VelocityComputed += OnVelocityComputed;
                }

                private void SetMovementTarget(Vector3 movementTarget)
                {
                    _navigationAgent.TargetPosition = movementTarget;
                }

                public override void _PhysicsProcess(double delta)
                {
                    // Không truy vấn khi bản đồ chưa bao giờ đồng bộ hóa và đang trống.
                    if (NavigationServer3D.MapGetIterationId(_navigationAgent.GetNavigationMap()) == 0)
                    {
                        return;
                    }

                    if (_navigationAgent.IsNavigationFinished())
                    {
                        return;
                    }

                    _movementDelta = MovementSpeed * (float)delta;
                    Vector3 nextPathPosition = _navigationAgent.GetNextPathPosition();
                    Vector3 newVelocity = GlobalPosition.DirectionTo(nextPathPosition) * _movementDelta;
                    if (_navigationAgent.AvoidanceEnabled)
                    {
                        _navigationAgent.Velocity = newVelocity;
                    }
                    else
                    {
                        OnVelocityComputed(newVelocity);
                    }
                }

                private void OnVelocityComputed(Vector3 safeVelocity)
                {
                    GlobalPosition = GlobalPosition.MoveToward(GlobalPosition + safeVelocity, _movementDelta);
                }
            }

         .. code-tab:: csharp CharacterBody3D

            using Godot;

            public partial class MyCharacterBody3D : CharacterBody3D
            {
                [Export]
                public float MovementSpeed { get; set; } = 4.0f;
                NavigationAgent3D _navigationAgent;

                public override void _Ready()
                {
                    _navigationAgent = GetNode<NavigationAgent3D>("NavigationAgent3D");
                    _navigationAgent.VelocityComputed += OnVelocityComputed;
                }

                private void SetMovementTarget(Vector3 movementTarget)
                {
                    _navigationAgent.TargetPosition = movementTarget;
                }

                public override void _PhysicsProcess(double delta)
                {
                    // Không truy vấn khi bản đồ chưa bao giờ đồng bộ hóa và đang trống.
                    if (NavigationServer3D.MapGetIterationId(_navigationAgent.GetNavigationMap()) == 0)
                    {
                        return;
                    }

                    if (_navigationAgent.IsNavigationFinished())
                    {
                        return;
                    }

                    Vector3 nextPathPosition = _navigationAgent.GetNextPathPosition();
                    Vector3 newVelocity = GlobalPosition.DirectionTo(nextPathPosition) * MovementSpeed;
                    if (_navigationAgent.AvoidanceEnabled)
                    {
                        _navigationAgent.Velocity = newVelocity;
                    }
                    else
                    {
                        OnVelocityComputed(newVelocity);
                    }
                }

                private void OnVelocityComputed(Vector3 safeVelocity)
                {
                    Velocity = safeVelocity;
                    MoveAndSlide();
                }
            }

         .. code-tab:: csharp RigidBody3D

            using Godot;

            public partial class MyRigidBody3D : RigidBody3D
            {
                [Export]
                public float MovementSpeed { get; set; } = 4.0f;
                NavigationAgent3D _navigationAgent;

                public override void _Ready()
                {
                    _navigationAgent = GetNode<NavigationAgent3D>("NavigationAgent3D");
                    _navigationAgent.VelocityComputed += OnVelocityComputed;
                }

                private void SetMovementTarget(Vector3 movementTarget)
                {
                    _navigationAgent.TargetPosition = movementTarget;
                }

                public override void _PhysicsProcess(double delta)
                {
                    // Không truy vấn khi bản đồ chưa bao giờ đồng bộ hóa và đang trống.
                    if (NavigationServer3D.MapGetIterationId(_navigationAgent.GetNavigationMap()) == 0)
                    {
                        return;
                    }

                    if (_navigationAgent.IsNavigationFinished())
                    {
                        return;
                    }

                    Vector3 nextPathPosition = _navigationAgent.GetNextPathPosition();
                    Vector3 newVelocity = GlobalPosition.DirectionTo(nextPathPosition) * MovementSpeed;
                    if (_navigationAgent.AvoidanceEnabled)
                    {
                        _navigationAgent.Velocity = newVelocity;
                    }
                    else
                    {
                        OnVelocityComputed(newVelocity);
                    }
                }

                private void OnVelocityComputed(Vector3 safeVelocity)
                {
                    LinearVelocity = safeVelocity;
                }
            }
