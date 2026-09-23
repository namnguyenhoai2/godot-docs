.. _doc_2d_movement:

Tổng quan về di chuyển 2D
=========================

Giới thiệu
----------

Mọi người mới bắt đầu đều từng đặt câu hỏi: "Làm thế nào để di chuyển nhân vật?" Tùy thuộc vào phong cách trò chơi bạn đang tạo, bạn có thể có những yêu cầu đặc biệt, nhưng nhìn chung, chuyển động trong hầu hết trò chơi 2D dựa trên một số ít kiểu thiết kế.

Chúng ta sẽ sử dụng :ref:`CharacterBody2D <class_CharacterBody2D>` cho các ví dụ này, nhưng các nguyên tắc cũng áp dụng cho những loại node khác (Area2D, RigidBody2D).

.. _doc_2d_movement_setup:

Thiết lập
---------

Mỗi ví dụ dưới đây đều sử dụng cùng một thiết lập scene. Bắt đầu với một ``CharacterBody2D`` có hai node con: ``Sprite2D`` và ``CollisionShape2D``. Bạn có thể sử dụng biểu tượng Godot (``icon.svg``) làm texture cho Sprite2D hoặc dùng bất kỳ hình ảnh 2D nào khác mà bạn có.

Mở ``Project -> Project Settings`` và chọn tab "Input Map". Thêm các input action sau (xem :ref:`InputEvent <doc_inputevent>` để biết chi tiết):

.. image:: img/movement_inputs.webp

Di chuyển 8 hướng
-----------------

Trong tình huống này, bạn muốn người dùng nhấn bốn phím điều hướng (lên/trái/xuống/phải hoặc W/A/S/D) và di chuyển theo hướng đã chọn. Tên gọi "di chuyển 8 hướng" xuất phát từ việc người chơi có thể di chuyển theo đường chéo bằng cách nhấn hai phím cùng lúc.

.. video:: video/movement_8way.webm
    :alt: 8-way movement
    :autoplay:
    :loop:
    :muted:
    :align: default
    :width: 100%

Gắn một script vào character body và thêm đoạn mã sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    @export var speed = 400

    func get_input():
        var input_direction = Input.get_vector("left", "right", "up", "down")
        velocity = input_direction * speed

    func _physics_process(delta):
        get_input()
        move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D
    {
        [Export]
        public int Speed { get; set; } = 400;

        public void GetInput()
        {

            Vector2 inputDirection = Input.GetVector("left", "right", "up", "down");
            Velocity = inputDirection * Speed;
        }

        public override void _PhysicsProcess(double delta)
        {
            GetInput();
            MoveAndSlide();
        }
    }

Trong hàm ``get_input()``, chúng ta sử dụng :ref:`Input <class_Input>` ``get_vector()`` để kiểm tra bốn sự kiện phím và cộng lại thành một vector hướng.

Sau đó, chúng ta có thể thiết lập velocity bằng cách nhân vector hướng này, vốn có độ dài ``1``, với tốc độ mong muốn.

.. tip:: Nếu bạn chưa từng sử dụng phép toán vector trước đây hoặc cần ôn lại, bạn có thể xem phần giải thích về cách sử dụng vector trong Godot tại :ref:`doc_vector_math`.

.. note::

    Nếu đoạn mã trên không làm gì khi bạn nhấn các phím, hãy kiểm tra lại rằng bạn đã thiết lập input action đúng như mô tả trong phần
    :ref:`doc_2d_movement_setup` của bài hướng dẫn này.

Xoay + di chuyển
----------------

Kiểu di chuyển này đôi khi được gọi là "phong cách Asteroids" vì nó giống với cách trò chơi arcade kinh điển đó vận hành. Nhấn trái/phải sẽ xoay nhân vật, còn lên/xuống sẽ di chuyển nhân vật tiến hoặc lùi theo hướng mà nó đang đối mặt.

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

    @export var speed = 400
    @export var rotation_speed = 1.5

    var rotation_direction = 0

    func get_input():
        rotation_direction = Input.get_axis("left", "right")
        velocity = transform.x * Input.get_axis("down", "up") * speed

    func _physics_process(delta):
        get_input()
        rotation += rotation_direction * rotation_speed * delta
        move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D
    {
        [Export]
        public int Speed { get; set; } = 400;

        [Export]
        public float RotationSpeed { get; set; } = 1.5f;

        private float _rotationDirection;

        public void GetInput()
        {
            _rotationDirection = Input.GetAxis("left", "right");
            Velocity = Transform.X * Input.GetAxis("down", "up") * Speed;
        }

        public override void _PhysicsProcess(double delta)
        {
            GetInput();
            Rotation += _rotationDirection * RotationSpeed * (float)delta;
            MoveAndSlide();
        }
    }

Ở đây, chúng ta đã thêm hai biến để theo dõi hướng và tốc độ xoay. Phép xoay được áp dụng trực tiếp vào thuộc tính ``rotation`` của body.

Để thiết lập velocity, chúng ta sử dụng ``transform.x`` của body, đây là một vector trỏ theo hướng "tiến" của body, rồi nhân vector đó với tốc độ.

Xoay + di chuyển (chuột)
------------------------

Kiểu di chuyển này là một biến thể của kiểu trước. Lần này, hướng được xác định bởi vị trí chuột thay vì bàn phím. Nhân vật sẽ luôn "nhìn về phía" con trỏ chuột. Tuy nhiên, các input tiến/lùi vẫn giữ nguyên.

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

    func get_input():
        look_at(get_global_mouse_position())
        velocity = transform.x * Input.get_axis("down", "up") * speed

    func _physics_process(delta):
        get_input()
        move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D
    {
        [Export]
        public int Speed { get; set; } = 400;

        public void GetInput()
        {
            LookAt(GetGlobalMousePosition());
            Velocity = Transform.X * Input.GetAxis("down", "up") * Speed;
        }

        public override void _PhysicsProcess(double delta)
        {
            GetInput();
            MoveAndSlide();
        }
    }

Ở đây, chúng ta sử dụng phương thức :ref:`Node2D <class_Node2D>` ``look_at()`` để hướng người chơi về phía vị trí của chuột. Nếu không có hàm này, bạn có thể đạt được hiệu ứng tương tự bằng cách thiết lập angle như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    rotation = get_global_mouse_position().angle_to_point(position)

 .. code-tab:: csharp

    var rotation = GetGlobalMousePosition().AngleToPoint(Position);


Di chuyển bằng cách nhấp chuột
------------------------------

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

    func _input(event):
        # Chỉ sử dụng is_action_pressed để chấp nhận thao tác nhấn đơn thay vì kéo chuột.
        if event.is_action_pressed(&"click"):
            target = get_global_mouse_position()

    func _physics_process(delta):
        velocity = position.direction_to(target) * speed
        # look_at(target)
        if position.distance_to(target) > 10:
            move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Movement : CharacterBody2D
    {
        [Export]
        public int Speed { get; set; } = 400;

        private Vector2 _target;

        public override void _Input(InputEvent @event)
        {
            // Chỉ sử dụng IsActionPressed để chấp nhận thao tác nhấn đơn thay vì kéo chuột.
            if (@event.IsActionPressed("click"))
            {
                _target = GetGlobalMousePosition();
            }
        }

        public override void _PhysicsProcess(double delta)
        {
            Velocity = Position.DirectionTo(_target) * Speed;
            // LookAt(_target);
            if (Position.DistanceTo(_target) > 10)
            {
                MoveAndSlide();
            }
        }
    }


Lưu ý việc kiểm tra ``distance_to()`` mà chúng ta thực hiện trước khi di chuyển. Nếu không có kiểm tra này, body sẽ "rung" khi đến vị trí đích, vì nó di chuyển hơi vượt quá vị trí đó rồi cố gắng quay lại, nhưng lại di chuyển quá xa và lặp lại quá trình này.

Bỏ chú thích dòng ``look_at()`` cũng sẽ khiến body xoay theo hướng chuyển động nếu bạn muốn.

.. tip:: Kỹ thuật này cũng có thể được dùng làm cơ sở cho một nhân vật "đi theo". Vị trí ``target`` có thể là vị trí của bất kỳ đối tượng nào mà bạn muốn di chuyển đến.

Tóm tắt
-------

Bạn có thể thấy các mẫu mã này hữu ích làm điểm khởi đầu cho những dự án của riêng mình. Hãy thoải mái sử dụng và thử nghiệm với chúng để xem bạn có thể tạo ra điều gì.

Bạn có thể tải xuống dự án mẫu tại đây: `2d_movement_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/2d_movement_starter.zip>`_

.. _`2d_movement_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/2d_movement_starter.zip
