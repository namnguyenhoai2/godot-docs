.. _doc_2d_movement:

Tổng quan về chuyển động 2D
===========================

Giới thiệu
----------

Mọi người mới bắt đầu đều từng hỏi: "Làm thế nào để di chuyển nhân vật của mình?" Tùy thuộc vào phong cách trò chơi bạn đang tạo, bạn có thể có những yêu cầu đặc biệt, nhưng nhìn chung, chuyển động trong hầu hết trò chơi 2D dựa trên một số ít thiết kế.

Chúng ta sẽ sử dụng :ref:`CharacterBody2D <class_CharacterBody2D>` cho các ví dụ này, nhưng những nguyên tắc này cũng áp dụng cho các loại node khác (Area2D, RigidBody2D).

.. _doc_2d_movement_setup:

Thiết lập
---------

Mỗi ví dụ dưới đây đều sử dụng cùng một thiết lập scene. Bắt đầu với một ``CharacterBody2D`` có hai node con: ``Sprite2D`` và ``CollisionShape2D``. Bạn có thể sử dụng biểu tượng Godot (``icon.svg``) làm texture cho Sprite2D hoặc sử dụng bất kỳ hình ảnh 2D nào khác mà bạn có.

Mở ``Project -> Project Settings`` và chọn tab "Input Map". Thêm các hành động đầu vào sau (xem :ref:`InputEvent <doc_inputevent>` để biết chi tiết):

.. image:: img/movement_inputs.webp

Chuyển động 8 hướng
-------------------

Trong trường hợp này, bạn muốn người dùng nhấn bốn phím định hướng (lên/trái/xuống/phải hoặc W/A/S/D) và di chuyển theo hướng đã chọn. Tên gọi "chuyển động 8 hướng" xuất phát từ việc người chơi có thể di chuyển theo đường chéo bằng cách nhấn hai phím cùng lúc.

.. video:: video/movement_8way.webm
    :alt: 8-way movement
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

Gắn một script vào thân nhân vật và thêm đoạn mã sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @export var speed = 400

    func get_input(): var input_direction = Input.get_vector("left", "right", "up", "down") velocity = input_direction * speed

    func _physics_process(delta): get_input() move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D { [Export] public int Speed { get; set; } = 400;

        public void GetInput() {

            Vector2 inputDirection = Input.GetVector("left", "right", "up", "down"); Velocity = inputDirection * Speed; }

        public override void _PhysicsProcess(double delta) { GetInput(); MoveAndSlide(); } }

Trong hàm ``get_input()``, chúng ta sử dụng :ref:`Input <class_Input>` ``get_vector()`` để kiểm tra bốn sự kiện phím và cộng, trả về một vector hướng.

Sau đó, chúng ta có thể đặt vận tốc bằng cách nhân vector hướng này, có độ dài là ``1``, với tốc độ mong muốn.

.. tip:: If you've never used vector math before, or need a refresher,
         Bạn có thể xem phần giải thích về cách sử dụng vector trong Godot tại :ref:`doc_vector_math`.

.. note::

    Nếu đoạn mã trên không làm gì khi bạn nhấn các phím, hãy kiểm tra lại xem bạn đã thiết lập đúng các hành động đầu vào như mô tả trong
    :ref:`doc_2d_movement_setup` part of this tutorial.

Xoay + chuyển động
------------------

Kiểu chuyển động này đôi khi được gọi là "phong cách Asteroids" vì nó tương tự cách trò chơi arcade kinh điển đó hoạt động. Nhấn trái/phải sẽ xoay nhân vật, còn lên/xuống sẽ di chuyển nhân vật về phía trước hoặc phía sau theo bất kỳ hướng nào mà nhân vật đang đối mặt.

.. video:: video/movement_rotate_keyboard.webm
    :alt: Rotation + movement
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @export var speed = 400 @export var rotation_speed = 1.5

    var rotation_direction = 0

    func get_input(): rotation_direction = Input.get_axis("left", "right") velocity = transform.x * Input.get_axis("down", "up") * speed

    func _physics_process(delta): get_input() rotation += rotation_direction * rotation_speed * delta move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D { [Export] public int Speed { get; set; } = 400;

        [Export] public float RotationSpeed { get; set; } = 1.5f;

        private float _rotationDirection;

        public void GetInput() { _rotationDirection = Input.GetAxis("left", "right"); Velocity = Transform.X * Input.GetAxis("down", "up") * Speed; }

        public override void _PhysicsProcess(double delta) { GetInput(); Rotation += _rotationDirection * RotationSpeed * (float)delta; MoveAndSlide(); } }

Ở đây, chúng ta đã thêm hai biến để theo dõi hướng và tốc độ xoay. Việc xoay được áp dụng trực tiếp vào thuộc tính ``rotation`` của thân.

Để đặt vận tốc, chúng ta sử dụng ``transform.x`` của thân, đây là một vector trỏ theo hướng "tiến về phía trước" của thân, rồi nhân vector đó với tốc độ.

Xoay + chuyển động (chuột)
--------------------------

Kiểu chuyển động này là một biến thể của kiểu trước. Lần này, hướng được xác định bởi vị trí chuột thay vì bàn phím. Nhân vật sẽ luôn "nhìn về phía" con trỏ chuột. Tuy nhiên, các đầu vào tiến/lùi vẫn giữ nguyên.

.. video:: video/movement_rotate_mouse.webm
    :alt: Rotation + movement (mouse)
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @export var speed = 400

    func get_input(): look_at(get_global_mouse_position()) velocity = transform.x * Input.get_axis("down", "up") * speed

    func _physics_process(delta): get_input() move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D { [Export] public int Speed { get; set; } = 400;

        public void GetInput() { LookAt(GetGlobalMousePosition()); Velocity = Transform.X * Input.GetAxis("down", "up") * Speed; }

        public override void _PhysicsProcess(double delta) { GetInput(); MoveAndSlide(); } }

Ở đây, chúng ta sử dụng phương thức :ref:`Node2D <class_Node2D>` ``look_at()`` để hướng người chơi về phía vị trí của chuột. Nếu không có hàm này, bạn có thể đạt được hiệu ứng tương tự bằng cách đặt góc như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    rotation = get_global_mouse_position().angle_to_point(position)

 .. code-tab:: csharp

    var rotation = GetGlobalMousePosition().AngleToPoint(Position);


Nhấp và di chuyển
-----------------

Ví dụ cuối cùng này chỉ sử dụng chuột để điều khiển nhân vật. Nhấp vào màn hình sẽ khiến người chơi di chuyển đến vị trí đích.

.. video:: video/movement_click.webm
    :alt: Click-and-move
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @export var speed = 400

    var target = position

    func _input(event): # Sử dụng is_action_pressed để chỉ chấp nhận các lần nhấp đơn làm đầu vào thay vì thao tác kéo chuột. if event.is_action_pressed(&"click"): target = get_global_mouse_position()

    func _physics_process(delta): velocity = position.direction_to(target) * speed # look_at(target) if position.distance_to(target) > 10: move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D { [Export] public int Speed { get; set; } = 400;

        private Vector2 _target;

        public override void _Input(InputEvent @event) { // Sử dụng IsActionPressed để chỉ chấp nhận các lần nhấp đơn làm đầu vào thay vì thao tác kéo chuột. if (@event.IsActionPressed("click")) { _target = GetGlobalMousePosition(); } }

        public override void _PhysicsProcess(double delta) { Velocity = Position.DirectionTo(_target) * Speed; // LookAt(_target); if (Position.DistanceTo(_target) > 10) { MoveAndSlide(); } } }


Lưu ý bước kiểm tra ``distance_to()`` mà chúng ta thực hiện trước khi di chuyển. Nếu không có phép kiểm tra này, thân sẽ "rung" khi đến vị trí đích, vì nó di chuyển hơi vượt qua vị trí đó rồi cố gắng quay lại, nhưng lại di chuyển quá xa và lặp lại quá trình này.

Bỏ chú thích dòng ``look_at()`` cũng sẽ khiến thân xoay theo hướng chuyển động nếu bạn muốn.

.. tip:: This technique can also be used as the basis of a "following" character.
         Vị trí ``target`` có thể là vị trí của bất kỳ đối tượng nào mà bạn muốn di chuyển đến.

Tóm tắt
-------

Bạn có thể thấy các mẫu mã này hữu ích làm điểm khởi đầu cho những dự án của riêng mình. Hãy thoải mái sử dụng và thử nghiệm với chúng để xem bạn có thể tạo ra những gì.

Bạn có thể tải xuống dự án mẫu tại đây: `2d_movement_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/2d_movement_starter.zip>`_
