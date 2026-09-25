.. _doc_ray-casting:

Ray casting
===========

Giới thiệu
----------

Một trong những tác vụ phổ biến nhất trong phát triển game là phóng một tia (hoặc một đối tượng có hình dạng tùy chỉnh) và kiểm tra xem nó va vào gì. Điều này cho phép thực hiện các hành vi phức tạp, AI, v.v. Tutorial này sẽ giải thích cách thực hiện việc đó trong 2D và 3D.

Godot lưu trữ toàn bộ thông tin game cấp thấp trong các server, còn scene chỉ là frontend. Vì vậy, ray casting nhìn chung là một tác vụ cấp thấp hơn. Đối với các raycast đơn giản, những node như
:ref:`RayCast3D <class_RayCast3D>` và :ref:`RayCast2D <class_RayCast2D>` sẽ hoạt động, vì mỗi frame chúng đều trả về kết quả của raycast.

Tuy nhiên, nhiều khi ray casting cần là một quá trình tương tác hơn, nên phải có cách thực hiện việc này bằng code.

Space
-----

Trong thế giới vật lý, Godot lưu trữ toàn bộ thông tin va chạm và vật lý cấp thấp trong một *space*. Có thể lấy space 2d hiện tại (dành cho 2D Physics) bằng cách truy cập
:ref:`CanvasItem.get_world_2d().space <class_CanvasItem_method_get_world_2d>`. Đối với 3D, đó là :ref:`Node3D.get_world_3d().space <class_Node3D_method_get_world_3d>`.

Space thu được :ref:`RID <class_RID>` có thể được sử dụng trong
:ref:`PhysicsServer3D <class_PhysicsServer3D>` và
:ref:`PhysicsServer2D <class_PhysicsServer2D>` lần lượt cho 3D và 2D.

Truy cập space
--------------

Theo mặc định, Godot physics chạy trên cùng thread với game logic, nhưng có thể được thiết lập để chạy trên một thread riêng nhằm hoạt động hiệu quả hơn. Do đó, thời điểm duy nhất an toàn để truy cập space là trong callback
:ref:`Node._physics_process() <class_Node_private_method__physics_process>`. Việc truy cập nó bên ngoài hàm này có thể gây lỗi vì space đang bị *locked*.

Để thực hiện các truy vấn vào physics space, phải sử dụng
:ref:`PhysicsDirectSpaceState2D <class_PhysicsDirectSpaceState2D>` và :ref:`PhysicsDirectSpaceState3D <class_PhysicsDirectSpaceState3D>`.

Sử dụng đoạn code sau trong 2D:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _physics_process(delta):
        var space_rid = get_world_2d().space
        var space_state = PhysicsServer2D.space_get_direct_state(space_rid)

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        var spaceRid = GetWorld2D().Space;
        var spaceState = PhysicsServer2D.SpaceGetDirectState(spaceRid);
    }

Hoặc trực tiếp hơn:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _physics_process(delta):
        var space_state = get_world_2d().direct_space_state

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        var spaceState = GetWorld2D().DirectSpaceState;
    }

Và trong 3D:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _physics_process(delta):
        var space_state = get_world_3d().direct_space_state

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        var spaceState = GetWorld3D().DirectSpaceState;
    }

Truy vấn raycast
----------------

Để thực hiện truy vấn raycast 2D, có thể sử dụng phương thức
:ref:`PhysicsDirectSpaceState2D.intersect_ray() <class_PhysicsDirectSpaceState2D_method_intersect_ray>`. Ví dụ:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _physics_process(delta):
        var space_state = get_world_2d().direct_space_state
        # sử dụng tọa độ global, không phải tọa độ local của node
        var query = PhysicsRayQueryParameters2D.create(Vector2(0, 0), Vector2(50, 100))
        var result = space_state.intersect_ray(query)

 .. code-tab:: csharp

    public override void _PhysicsProcess(double delta)
    {
        var spaceState = GetWorld2D().DirectSpaceState;
        // sử dụng tọa độ global, không phải tọa độ local của node
        var query = PhysicsRayQueryParameters2D.Create(Vector2.Zero, new Vector2(50, 100));
        var result = spaceState.IntersectRay(query);
    }

Kết quả là một dictionary. Nếu tia không va vào gì, dictionary sẽ rỗng. Nếu có va vào một đối tượng, dictionary sẽ chứa thông tin va chạm:

.. tabs::
 .. code-tab:: gdscript GDScript

        if result:
            print("Hit at point: ", result.position)

 .. code-tab:: csharp

        if (result.Count > 0)
        {
            GD.Print("Hit at point: ", result["position"]);
        }

Dictionary ``result`` khi xảy ra va chạm chứa dữ liệu sau:

::

    {
       position: Vector2 # point in world space for collision
       normal: Vector2 # normal in world space for collision
       collider: Object # Object collided or null (if unassociated)
       collider_id: ObjectID # Object it collided against
       rid: RID # RID it collided against
       shape: int # shape index of collider
       metadata: Variant() # metadata of collider
    }

Dữ liệu trong 3D space cũng tương tự, sử dụng tọa độ Vector3. Lưu ý rằng để bật va chạm với Area3D, tham số boolean ``collide_with_areas`` phải được đặt thành ``true``.

.. tabs::
 .. code-tab:: gdscript GDScript

        const RAY_LENGTH = 1000

        func _physics_process(delta):
            var space_state = get_world_3d().direct_space_state
            var cam = $Camera3D
            var mousepos = get_viewport().get_mouse_position()

            var origin = cam.project_ray_origin(mousepos)
            var end = origin + cam.project_ray_normal(mousepos) * RAY_LENGTH
            var query = PhysicsRayQueryParameters3D.create(origin, end)
            query.collide_with_areas = true

            var result = space_state.intersect_ray(query)

 .. code-tab:: csharp

    private const int RayLength = 1000;

    public override void _PhysicsProcess(double delta)
    {
        var spaceState = GetWorld3D().DirectSpaceState;
        var cam = GetNode<Camera3D>("Camera3D");
        var mousePos = GetViewport().GetMousePosition();

        var origin = cam.ProjectRayOrigin(mousePos);
        var end = origin + cam.ProjectRayNormal(mousePos) * RayLength;
        var query = PhysicsRayQueryParameters3D.Create(origin, end);
        query.CollideWithAreas = true;

        var result = spaceState.IntersectRay(query);
    }

Ngoại lệ va chạm
----------------

Một trường hợp sử dụng phổ biến của ray casting là cho phép một character thu thập dữ liệu về thế giới xung quanh nó. Vấn đề là chính character đó cũng có collider, nên tia sẽ chỉ phát hiện collider của node cha, như minh họa trong hình sau:

.. image:: img/raycast_falsepositive.webp

Để tránh tự giao nhau, object tham số ``intersect_ray()`` có thể nhận một mảng các ngoại lệ thông qua thuộc tính ``exclude``. Đây là ví dụ về cách sử dụng nó từ CharacterBody2D hoặc bất kỳ node đối tượng va chạm nào khác:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    func _physics_process(delta):
        var space_state = get_world_2d().direct_space_state
        var query = PhysicsRayQueryParameters2D.create(global_position, player_position)
        query.exclude = [self]
        var result = space_state.intersect_ray(query)

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        public override void _PhysicsProcess(double delta)
        {
            var spaceState = GetWorld2D().DirectSpaceState;
            var query = PhysicsRayQueryParameters2D.Create(globalPosition, playerPosition);
            query.Exclude = [GetRid()];
            var result = spaceState.IntersectRay(query);
        }
    }

Mảng ngoại lệ có thể chứa các object hoặc RID.

Mặt nạ va chạm
--------------

Mặc dù phương thức ngoại lệ hoạt động tốt để loại trừ body cha, nó trở nên rất bất tiện nếu bạn cần một danh sách ngoại lệ lớn và/hoặc động. Trong trường hợp này, sử dụng hệ thống collision layer/mask sẽ hiệu quả hơn nhiều.

Object tham số ``intersect_ray()`` cũng có thể được cung cấp collision mask. Ví dụ, để sử dụng cùng mask với body cha, hãy dùng biến thành viên ``collision_mask``. Mảng ngoại lệ cũng có thể được cung cấp dưới dạng đối số cuối cùng:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    func _physics_process(delta):
        var space_state = get_world_2d().direct_space_state
        var query = PhysicsRayQueryParameters2D.create(global_position, target_position,
            collision_mask, [self])
        var result = space_state.intersect_ray(query)

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        public override void _PhysicsProcess(double delta)
        {
            var spaceState = GetWorld2D().DirectSpaceState;
            var query = PhysicsRayQueryParameters2D.Create(globalPosition, targetPosition,
                CollisionMask, [GetRid()]);
            var result = spaceState.IntersectRay(query);
        }
    }

Xem :ref:`doc_physics_introduction_collision_layer_code_example` để biết chi tiết về cách thiết lập collision mask.

Ray casting 3D từ màn hình
--------------------------

Phóng một tia từ màn hình vào 3D physics space rất hữu ích cho việc chọn object. Không cần làm việc này nhiều vì
:ref:`CollisionObject3D <class_CollisionObject3D>` có signal "input_event" cho bạn biết khi nó được nhấp, nhưng nếu muốn thực hiện thủ công thì cách làm như sau.

Để phóng một tia từ màn hình, bạn cần một node :ref:`Camera3D <class_Camera3D>`. Một ``Camera3D`` có thể sử dụng một trong hai chế độ projection: perspective và orthogonal. Vì vậy, cần lấy cả origin và direction của tia. Điều này là do ``origin`` thay đổi trong chế độ orthogonal, còn ``normal`` thay đổi trong chế độ perspective:

.. image:: img/raycast_projection.png

Để lấy chúng bằng camera, có thể sử dụng đoạn code sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    const RAY_LENGTH = 1000.0

    func _input(event):
        if event is InputEventMouseButton and event.pressed and event.button_index == 1:
            var camera3d = $Camera3D
            var from = camera3d.project_ray_origin(event.position)
            var to = from + camera3d.project_ray_normal(event.position) * RAY_LENGTH

 .. code-tab:: csharp

    private const float RayLength = 1000.0f;

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventMouseButton eventMouseButton && eventMouseButton.Pressed && eventMouseButton.ButtonIndex == MouseButton.Left)
        {
            var camera3D = GetNode<Camera3D>("Camera3D");
            var from = camera3D.ProjectRayOrigin(eventMouseButton.Position);
            var to = from + camera3D.ProjectRayNormal(eventMouseButton.Position) * RayLength;
        }
    }

Hãy nhớ rằng trong ``_input()``, space có thể bị khóa, vì vậy trên thực tế truy vấn này nên được chạy trong ``_physics_process()``.
