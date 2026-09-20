.. _doc_navigation_using_navigationagents:

Sử dụng NavigationAgents
========================

NavigationAgents là các node trợ giúp kết hợp chức năng tìm đường, bám đường đi và tránh agent cho một node cha kế thừa Node2D/3D. Chúng hỗ trợ thực hiện các lệnh gọi phổ biến đến API NavigationServer thay cho node actor cha theo cách thuận tiện hơn cho người mới bắt đầu.

Phiên bản 2D và 3D của NavigationAgents có sẵn dưới dạng
:ref:`NavigationAgent2D<class_NavigationAgent2D>` and
:ref:`NavigationAgent3D<class_NavigationAgent3D>` respectively.

New NavigationAgent nodes will automatically join the default navigation map on the :ref:`World2D<class_World2D>`/:ref:`World3D<class_World3D>`.

Các node NavigationAgent là tùy chọn và không bắt buộc để sử dụng hệ thống navigation. Toàn bộ chức năng của chúng có thể được thay thế bằng các script và lệnh gọi trực tiếp đến API NavigationServer.

.. tip::

    Đối với các trường hợp sử dụng nâng cao hơn, hãy cân nhắc :ref:`doc_navigation_using_navigationpathqueryobjects` thay cho các node NavigationAgent.

Tìm đường với NavigationAgent
-----------------------------

NavigationAgents sẽ truy vấn một navigation path mới trên navigation map hiện tại khi ``target_position`` của chúng được đặt bằng một global position.

Kết quả tìm đường có thể bị ảnh hưởng bởi các thuộc tính sau.

- Bitmask ``navigation_layers`` có thể được dùng để giới hạn các navigation mesh mà agent được phép sử dụng. - ``pathfinding_algorithm`` kiểm soát cách quá trình tìm đường đi qua các polygon của navigation mesh trong quá trình tìm kiếm đường đi. - ``path_postprocessing`` thiết lập xem và bằng cách nào raw path corridor do quá trình tìm đường tìm thấy sẽ được thay đổi trước khi trả về. - ``path_metadata_flags`` cho phép thu thập thêm metadata của các path point được path trả về. - Các thuộc tính ``simplify_path`` và ``simplify_epsilon`` có thể được dùng để loại bỏ các point ít quan trọng hơn khỏi path.

.. warning::

    Việc tắt các path meta flag sẽ tắt các signal emission liên quan trên agent.

Bám đường đi với NavigationAgent
--------------------------------

Sau khi ``target_position`` được đặt cho agent, có thể lấy vị trí tiếp theo cần đi theo trên path bằng hàm ``get_next_path_position()``.

Sau khi nhận được vị trí tiếp theo trên path, hãy dùng mã movement của riêng bạn để di chuyển node actor cha của agent về phía vị trí này.

.. note::

    Hệ thống navigation không bao giờ di chuyển node cha của NavigationAgent. Việc di chuyển hoàn toàn do người dùng và các script tùy chỉnh của họ thực hiện.

NavigationAgents có logic nội bộ riêng để tiếp tục đi theo path hiện tại và yêu cầu cập nhật.

Hàm ``get_next_path_position()`` chịu trách nhiệm cập nhật nhiều trạng thái và thuộc tính nội bộ của agent. Hàm này nên được gọi lặp lại *một lần* mỗi ``physics_process`` cho đến khi ``is_navigation_finished()`` cho biết path đã hoàn tất. Không nên gọi hàm này sau khi đã đến vị trí đích hoặc điểm cuối của path, vì việc cập nhật path lặp lại có thể khiến agent rung tại chỗ. Luôn kiểm tra từ rất sớm trong script bằng ``is_navigation_finished()`` xem path đã hoàn tất hay chưa.

Các thuộc tính khoảng cách sau đây ảnh hưởng đến hành vi bám đường đi.

- Khi còn cách vị trí tiếp theo trên path ``path_desired_distance``, agent sẽ chuyển path index nội bộ sang vị trí tiếp theo sau đó. - Khi còn cách vị trí đích trên path ``target_desired_distance``, agent xem vị trí đích là đã đạt được và path đã kết thúc. - Khi cách path lý tưởng đến vị trí tiếp theo trên path ``path_max_distance``, agent sẽ yêu cầu một path mới vì đã bị đẩy lệch quá xa.

Tất cả các cập nhật quan trọng đều được kích hoạt bằng hàm ``get_next_path_position()`` khi được gọi trong ``_physics_process()``.

NavigationAgents có thể được sử dụng với ``process``, nhưng vẫn bị giới hạn ở một lần cập nhật diễn ra trong ``physics_process``.

Bạn có thể tìm thấy các ví dụ script cho nhiều node thường được sử dụng với NavigationAgents ở phần bên dưới.

Các vấn đề thường gặp khi bám đường đi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có một số vấn đề phổ biến của người dùng và các điểm cần lưu ý quan trọng khi viết script di chuyển cho agent.

- Path được trả về rỗng Nếu agent truy vấn path trước khi navigation map được đồng bộ, chẳng hạn trong một hàm ``_ready()``, path có thể được trả về rỗng. Trong trường hợp này, hàm ``get_next_path_position()`` sẽ trả về cùng vị trí với node cha của agent và agent sẽ xem như đã đến cuối path. Có thể khắc phục bằng cách thực hiện một deferred call hoặc sử dụng callback, chẳng hạn như chờ signal navigation map changed.

- Agent bị kẹt và nhảy qua lại giữa hai vị trí Điều này thường do path được cập nhật quá thường xuyên ở mỗi frame, dù cố ý hay vô tình (ví dụ: max path distance được đặt quá ngắn). Quá trình tìm đường cần tìm vị trí gần nhất hợp lệ trên navigation mesh. Nếu yêu cầu path mới ở mỗi frame, các vị trí đầu tiên trên path có thể liên tục chuyển đổi giữa phía trước và phía sau vị trí hiện tại của agent, khiến agent nhảy qua lại giữa hai vị trí.

- Agent đôi khi đi ngược lại Nếu agent di chuyển quá nhanh, nó có thể vượt qua bước kiểm tra path_desired_distance mà không bao giờ tăng path index. Điều này có thể khiến agent quay lại điểm trên path hiện đang ở phía sau nó cho đến khi vượt qua bước kiểm tra khoảng cách để tăng path index. Việc tăng các khoảng cách mong muốn tương ứng với tốc độ và tần suất cập nhật của agent thường cũng khắc phục được vấn đề này, cùng với cách bố trí polygon của navigation mesh cân bằng hơn, không có quá nhiều cạnh polygon bị dồn vào những không gian nhỏ.

- Agent đôi khi nhìn về phía sau trong một frame Tương tự như trường hợp agent bị kẹt và nhảy qua lại giữa hai vị trí, nguyên nhân thường là path được cập nhật quá thường xuyên ở mỗi frame. Tùy thuộc vào cách bố trí navigation mesh, đặc biệt khi agent được đặt trực tiếp trên một cạnh navigation mesh hoặc edge connection, hãy dự kiến rằng các vị trí trên path đôi khi sẽ hơi "ở phía sau" hướng hiện tại của actor. Điều này xảy ra do các vấn đề về độ chính xác và không phải lúc nào cũng có thể tránh được. Đây thường chỉ là vấn đề về hiển thị nếu actor ngay lập tức xoay mặt về phía vị trí hiện tại trên path.

Tránh với NavigationAgent
-------------------------

Phần này giải thích cách sử dụng tính năng tránh dành riêng cho NavigationAgents.

Để NavigationAgents sử dụng tính năng tránh, thuộc tính ``avoidance_enabled`` phải được đặt thành ``true``.

.. image:: img/agent_avoidance_enabled.png

Signal ``velocity_computed`` của node NavigationAgent phải được kết nối để nhận kết quả tính toán safe velocity.

.. image:: img/agent_safevelocity_signal.png

Đặt ``velocity`` của node NavigationAgent trong ``_physics_process()`` để cập nhật agent bằng velocity hiện tại của node cha của agent.

Trong khi tính năng tránh được bật trên agent, vector ``safe_velocity`` sẽ được nhận cùng signal velocity_computed ở mỗi physics frame. Vector velocity này nên được dùng để di chuyển node cha của NavigationAgent nhằm tránh va chạm với các agent khác đang sử dụng tính năng tránh hoặc với các chướng ngại vật tránh.

.. note::

    Chỉ những agent khác trên cùng map và đã tự đăng ký sử dụng tính năng tránh mới được xem xét trong phép tính tránh.

.. note::

    NavigationAgent **phải** được cung cấp thuộc tính ``target_position``, ngay cả khi bạn chỉ sử dụng agent cho tính năng tránh. Nếu không, ``safe_velocity`` nhận được từ signal ``velocity_computed`` sẽ luôn là vector không.

Các thuộc tính NavigationAgent sau đây có liên quan đến tính năng tránh:

  - Thuộc tính ``height`` chỉ có trong 3D. Chiều cao cùng với vị trí global hiện tại trên trục y của agent xác định vị trí theo chiều dọc của agent trong mô phỏng tránh. Các agent sử dụng tính năng tránh 2D sẽ tự động bỏ qua những agent hoặc chướng ngại vật ở bên dưới hoặc bên trên chúng. - Thuộc tính ``radius`` kiểm soát bán kính của hình tròn tránh, hoặc hình cầu trong 3D, xung quanh agent. Khu vực này mô tả phần thân của agent, không phải khoảng cách thực hiện thao tác tránh. - Thuộc tính ``neighbor_distance`` kiểm soát bán kính tìm kiếm của agent khi tìm các agent khác cần tránh. Giá trị thấp hơn sẽ giảm chi phí xử lý. - Thuộc tính ``max_neighbors`` kiểm soát số lượng agent khác được xem xét trong phép tính tránh nếu tất cả chúng có bán kính chồng lấn. Giá trị thấp hơn sẽ giảm chi phí xử lý, nhưng giá trị quá thấp có thể khiến các agent bỏ qua việc tránh. - Các thuộc tính ``time_horizon_agents`` và ``time_horizon_obstacles`` kiểm soát thời gian dự đoán tránh đối với các agent hoặc chướng ngại vật khác, tính bằng giây. Khi tính toán safe velocity, các agent sẽ chọn những velocity có thể được duy trì trong khoảng thời gian này mà không va chạm với một đối tượng tránh khác. Nên giữ thời gian dự đoán ở mức thấp nhất có thể vì agent sẽ giảm velocity để tránh va chạm trong khoảng thời gian đó. - Thuộc tính ``max_speed`` kiểm soát velocity tối đa được phép dùng trong phép tính tránh của agent. Nếu node cha của agent di chuyển nhanh hơn giá trị này, ``safe_velocity`` tránh có thể không đủ chính xác để tránh va chạm. - Thuộc tính ``use_3d_avoidance`` chuyển agent giữa tính năng tránh 2D (trục xz) và tránh 3D (trục xyz) trong lần cập nhật tiếp theo. Lưu ý rằng tính năng tránh 2D và tránh 3D chạy trong các mô phỏng tránh riêng biệt, vì vậy các agent được phân chia giữa chúng sẽ không ảnh hưởng lẫn nhau. - Các thuộc tính ``avoidance_layers`` và ``avoidance_mask`` là các bitmask tương tự như physics layer. Agent sẽ chỉ tránh những đối tượng tránh khác nằm trên một avoidance layer khớp với ít nhất một bit trong avoidance mask của chúng. - ``avoidance_priority`` khiến các agent có priority cao hơn bỏ qua các agent có priority thấp hơn. Có thể dùng thuộc tính này để tăng mức độ ưu tiên cho một số agent nhất định trong mô phỏng tránh, chẳng hạn như các nhân vật không thể chơi quan trọng, mà không cần liên tục thay đổi toàn bộ avoidance layer hoặc mask của chúng.


Cơ chế tránh tồn tại trong không gian riêng và không có thông tin từ navigation mesh hoặc va chạm vật lý. Phía sau hậu trường, các tác nhân tránh chỉ là những hình tròn có bán kính khác nhau trên một mặt phẳng 2D hoặc những hình cầu trong một không gian 3D trống rỗng. Có thể dùng NavigationObstacles để thêm một số ràng buộc môi trường vào mô phỏng tránh, xem :ref:`doc_navigation_using_navigationobstacles`.

.. note::

    Cơ chế tránh không ảnh hưởng đến pathfinding. Bạn nên xem đây là một tùy chọn bổ sung dành cho các đối tượng di chuyển liên tục không thể (re)bake vào navigation mesh một cách hiệu quả để di chuyển vòng quanh chúng.

.. note::

    Cơ chế tránh RVO đưa ra các giả định ngầm về hành vi tự nhiên của tác nhân. Ví dụ: các tác nhân di chuyển về những phía vượt qua hợp lý có thể được chỉ định khi chúng gặp nhau. Điều này có nghĩa là các kịch bản kiểm thử tránh mang tính quá lý tưởng thường sẽ thất bại. Ví dụ: các tác nhân di chuyển trực tiếp về phía nhau với vận tốc hoàn toàn ngược chiều sẽ thất bại vì không thể chỉ định phía vượt qua cho các tác nhân.

Sử dụng thuộc tính ``avoidance_enabled`` của NavigationAgent là tùy chọn được ưu tiên để bật/tắt cơ chế tránh. Có thể sử dụng các đoạn mã sau để bật cơ chế tránh trên các tác nhân, tạo hoặc xóa callback tránh, hoặc chuyển đổi chế độ tránh.

.. tabs::
 .. code-tab:: gdscript 2D GDScript

    extends NavigationAgent2D

    func _ready() -> void:
        var agent: RID = get_rid()
        # Bật cơ chế tránh
        NavigationServer2D.agent_set_avoidance_enabled(agent, true)
        # Tạo callback tránh
        NavigationServer2D.agent_set_avoidance_callback(agent, Callable(self, "_avoidance_done"))

        # Tắt cơ chế tránh
        NavigationServer2D.agent_set_avoidance_enabled(agent, false)
        # Xóa callback tránh
        NavigationServer2D.agent_set_avoidance_callback(agent, Callable())

 .. code-tab:: csharp 2D C#

    using Godot;

    public partial class MyNavigationAgent2D : NavigationAgent2D
    {
        public override void _Ready()
        {
            Rid agent = GetRid();
            // Bật cơ chế tránh
            NavigationServer2D.AgentSetAvoidanceEnabled(agent, true);
            // Tạo callback tránh
            NavigationServer2D.AgentSetAvoidanceCallback(agent, Callable.From(AvoidanceDone));

            // Tắt cơ chế tránh
            NavigationServer2D.AgentSetAvoidanceEnabled(agent, false);
            //Xóa callback tránh
            NavigationServer2D.AgentSetAvoidanceCallback(agent, default);
        }

        private void AvoidanceDone() { }
    }

 .. code-tab:: gdscript 3D GDScript

    extends NavigationAgent3D

    func _ready() -> void:
        var agent: RID = get_rid()
        # Bật cơ chế tránh
        NavigationServer3D.agent_set_avoidance_enabled(agent, true)
        # Tạo callback tránh
        NavigationServer3D.agent_set_avoidance_callback(agent, Callable(self, "_avoidance_done"))
        # Chuyển sang cơ chế tránh 3D
        NavigationServer3D.agent_set_use_3d_avoidance(agent, true)

        # Tắt cơ chế tránh
        NavigationServer3D.agent_set_avoidance_enabled(agent, false)
        # Xóa callback tránh
        NavigationServer3D.agent_set_avoidance_callback(agent, Callable())
        # Chuyển sang cơ chế tránh 2D
        NavigationServer3D.agent_set_use_3d_avoidance(agent, false)

 .. code-tab:: csharp 3D C#

    using Godot;

    public partial class MyNavigationAgent3D : NavigationAgent3D
    {
        public override void _Ready()
        {
            Rid agent = GetRid();
            // Bật cơ chế tránh
            NavigationServer3D.AgentSetAvoidanceEnabled(agent, true);
            // Tạo callback tránh
            NavigationServer3D.AgentSetAvoidanceCallback(agent, Callable.From(AvoidanceDone));
            // Chuyển sang cơ chế tránh 3D
            NavigationServer3D.AgentSetUse3DAvoidance(agent, true);

            // Tắt cơ chế tránh
            NavigationServer3D.AgentSetAvoidanceEnabled(agent, false);
            //Xóa callback tránh
            NavigationServer3D.AgentSetAvoidanceCallback(agent, default);
            // Chuyển sang cơ chế tránh 2D
            NavigationServer3D.AgentSetUse3DAvoidance(agent, false);
        }

        private void AvoidanceDone() { }
    }

Mẫu script NavigationAgent
--------------------------

Các phần sau cung cấp mẫu script cho những node thường được sử dụng với NavigationAgent.

.. tabs::

   .. tab:: 2D GDScript

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
                # Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                # Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                # Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                    // Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                    // Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                    // Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                # Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                # Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                # Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                    // Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                    // Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
                    // Không thực hiện truy vấn khi map chưa từng được đồng bộ và đang trống.
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
