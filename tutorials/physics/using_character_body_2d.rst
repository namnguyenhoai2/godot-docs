.. _doc_using_character_body_2d:

Sử dụng CharacterBody2D/3D
==========================

Giới thiệu
----------

Godot cung cấp một số đối tượng va chạm để hỗ trợ cả việc phát hiện và phản hồi va chạm. Việc quyết định nên sử dụng đối tượng nào cho dự án có thể gây khó hiểu. Bạn có thể tránh các vấn đề và đơn giản hóa quá trình phát triển nếu hiểu cách mỗi đối tượng hoạt động cũng như ưu, nhược điểm của chúng. Trong hướng dẫn này, chúng ta sẽ xem xét
:ref:`CharacterBody2D <class_CharacterBody2D>` và trình bày một số ví dụ về cách sử dụng nó.

.. note:: Mặc dù tài liệu này sử dụng ``CharacterBody2D`` trong các ví dụ, những khái niệm tương tự cũng áp dụng cho 3D.

Character body là gì?
---------------------

``CharacterBody2D`` dùng để triển khai các body được điều khiển bằng code. Character body phát hiện va chạm với các body khác khi di chuyển, nhưng không chịu ảnh hưởng của các thuộc tính vật lý của engine như trọng lực hoặc ma sát. Điều này có nghĩa là bạn phải viết một số code để tạo hành vi cho chúng, nhưng đồng thời bạn cũng có quyền kiểm soát chính xác hơn cách chúng di chuyển và phản ứng.

Mặc dù có tên là ``CharacterBody2D``, nó cũng có thể được dùng cho các đối tượng vật lý khác cần logic di chuyển thủ công chính xác và thông tin va chạm chi tiết, chẳng hạn như các platform di chuyển hoặc projectile phức tạp.

.. note:: Tài liệu này giả định rằng bạn đã quen thuộc với các physics body khác nhau của Godot. Trước tiên, hãy đọc :ref:`doc_physics_introduction` để xem tổng quan về các tùy chọn vật lý.

.. tip:: Một `CharacterBody2D` có thể chịu ảnh hưởng của trọng lực và các lực khác, nhưng bạn phải tính toán chuyển động trong code. Physics engine sẽ không tự di chuyển một `CharacterBody2D`.

Di chuyển và va chạm
--------------------

Khi di chuyển một ``CharacterBody2D``, bạn không nên đặt trực tiếp thuộc tính ``position`` của nó. Thay vào đó, hãy sử dụng các method ``move_and_collide()`` hoặc ``move_and_slide()``. Những method này di chuyển body theo một vector nhất định và phát hiện va chạm.

.. warning:: Bạn nên xử lý việc di chuyển physics body trong callback ``_physics_process()``.

Hai method di chuyển phục vụ các mục đích khác nhau; ở phần sau của hướng dẫn này, bạn sẽ thấy các ví dụ về cách chúng hoạt động.

move_and_collide
~~~~~~~~~~~~~~~~

Method này nhận một tham số bắt buộc: một :ref:`Vector2 <class_Vector2>` biểu thị chuyển động tương đối của body. Thông thường, đây là vector vận tốc nhân với timestep của frame (``delta``). Nếu engine phát hiện va chạm ở bất kỳ vị trí nào dọc theo vector này, body sẽ dừng di chuyển ngay lập tức. Nếu điều này xảy ra, method sẽ trả về một đối tượng :ref:`KinematicCollision2D <class_KinematicCollision2D>`.

``KinematicCollision2D`` là một đối tượng chứa dữ liệu về va chạm và đối tượng gây va chạm. Bạn có thể dùng dữ liệu này để tính toán phản hồi va chạm.

``move_and_collide`` hữu ích nhất khi bạn chỉ muốn di chuyển body và phát hiện va chạm, nhưng không cần phản hồi va chạm tự động. Ví dụ, nếu cần một viên đạn bật nảy khỏi tường, bạn có thể trực tiếp thay đổi góc của vận tốc khi phát hiện va chạm. Xem ví dụ bên dưới.

move_and_slide
~~~~~~~~~~~~~~

Method ``move_and_slide()`` nhằm đơn giản hóa việc phản hồi va chạm trong trường hợp phổ biến khi bạn muốn một body trượt dọc theo body kia. Chẳng hạn, method này đặc biệt hữu ích trong các game platformer hoặc game góc nhìn từ trên xuống.

Khi gọi ``move_and_slide()``, function sử dụng một số thuộc tính của node để tính toán hành vi trượt. Bạn có thể tìm thấy các thuộc tính này trong Inspector hoặc thiết lập chúng trong code.

- ``velocity`` - *giá trị mặc định:* ``Vector2( 0, 0 )``

    Thuộc tính này biểu thị vector vận tốc của body tính bằng pixel trên giây. ``move_and_slide()`` sẽ tự động sửa đổi giá trị này khi xảy ra va chạm.

- ``motion_mode`` - *giá trị mặc định:* ``MOTION_MODE_GROUNDED``

    Thuộc tính này thường được dùng để phân biệt chuyển động cuộn ngang và chuyển động từ trên xuống. Khi sử dụng giá trị mặc định, bạn có thể dùng các method ``is_on_floor()``, ``is_on_wall()`` và ``is_on_ceiling()`` để phát hiện loại bề mặt mà body đang tiếp xúc, đồng thời body sẽ tương tác với các slope. Khi sử dụng ``MOTION_MODE_FLOATING``, mọi va chạm đều được xem là "tường".

- ``up_direction`` - *giá trị mặc định:* ``Vector2( 0, -1 )``

    Thuộc tính này cho phép bạn xác định những bề mặt nào engine nên xem là sàn. Giá trị của nó cho phép bạn dùng các method ``is_on_floor()``, ``is_on_wall()`` và ``is_on_ceiling()`` để phát hiện loại bề mặt mà body đang tiếp xúc. Giá trị mặc định có nghĩa là mặt trên của các bề mặt nằm ngang sẽ được xem là "mặt đất".

- ``floor_stop_on_slope`` - *giá trị mặc định:* ``true``

    Thuộc tính này ngăn body trượt xuống các slope khi đang đứng yên.

- ``wall_min_slide_angle`` - *giá trị mặc định:* ``0.261799`` (tính bằng radian, tương đương ``15`` độ)

    Thuộc tính này là góc nhỏ nhất tại đó body được phép trượt khi chạm vào slope.

- ``floor_max_angle`` - *giá trị mặc định:* ``0.785398`` (tính bằng radian, tương đương ``45`` độ)

    Thuộc tính này là góc tối đa trước khi một bề mặt không còn được xem là "sàn".

Có nhiều thuộc tính khác có thể được dùng để sửa đổi hành vi của body trong những trường hợp cụ thể. Xem tài liệu :ref:`CharacterBody2D <class_CharacterBody2D>` để biết đầy đủ chi tiết.

Phát hiện va chạm
-----------------

Khi sử dụng ``move_and_collide()``, function trực tiếp trả về một ``KinematicCollision2D``, và bạn có thể dùng giá trị này trong code.

Khi sử dụng ``move_and_slide()``, có thể xảy ra nhiều va chạm trong quá trình tính toán phản hồi trượt. Để xử lý các va chạm này, hãy sử dụng ``get_slide_collision_count()`` và ``get_slide_collision()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Sử dụng move_and_collide.
    var collision = move_and_collide(velocity * delta)
    if collision:
        print("I collided with ", collision.get_collider().name)

    # Sử dụng move_and_slide.
    move_and_slide()
    for i in get_slide_collision_count():
        var collision = get_slide_collision(i)
        print("I collided with ", collision.get_collider().name)

 .. code-tab:: csharp

    // Sử dụng MoveAndCollide.
    var collision = MoveAndCollide(Velocity * (float)delta);
    if (collision != null)
    {
        GD.Print("I collided with ", ((Node)collision.GetCollider()).Name);
    }

    // Sử dụng MoveAndSlide.
    MoveAndSlide();
    for (int i = 0; i < GetSlideCollisionCount(); i++)
    {
        var collision = GetSlideCollision(i);
        GD.Print("I collided with ", ((Node)collision.GetCollider()).Name);
    }

.. note:: `get_slide_collision_count()` chỉ đếm số lần body đã va chạm và đổi hướng.

Xem :ref:`KinematicCollision2D <class_KinematicCollision2D>` để biết chi tiết về dữ liệu va chạm được trả về.

Nên sử dụng method di chuyển nào?
---------------------------------

Một câu hỏi phổ biến của người dùng Godot mới là: "Làm thế nào để quyết định nên sử dụng function di chuyển nào?" Thông thường, câu trả lời là sử dụng ``move_and_slide()`` vì nó có vẻ đơn giản hơn, nhưng không nhất thiết là như vậy. Một cách để hình dung là ``move_and_slide()`` là trường hợp đặc biệt, còn ``move_and_collide()`` tổng quát hơn. Ví dụ, hai đoạn code sau cho kết quả phản hồi va chạm giống nhau:

.. image:: img/k2d_compare.gif

.. tabs::
 .. code-tab:: gdscript GDScript

    # sử dụng move_and_collide
    var collision = move_and_collide(velocity * delta)
    if collision:
        velocity = velocity.slide(collision.get_normal())

    # sử dụng move_and_slide
    move_and_slide()

 .. code-tab:: csharp

    // sử dụng MoveAndCollide
    var collision = MoveAndCollide(Velocity * (float)delta);
    if (collision != null)
    {
        Velocity = Velocity.Slide(collision.GetNormal());
    }

    // sử dụng MoveAndSlide
    MoveAndSlide();

Mọi việc bạn làm với ``move_and_slide()`` cũng có thể thực hiện bằng ``move_and_collide()``, nhưng có thể cần thêm một chút mã. Tuy nhiên, như chúng ta sẽ thấy trong các ví dụ bên dưới, có những trường hợp ``move_and_slide()`` không cung cấp kết quả bạn muốn.

Trong ví dụ trên, ``move_and_slide()`` tự động thay đổi biến ``velocity``. Điều này là do khi nhân vật va chạm với môi trường, hàm sẽ tính toán lại tốc độ nội bộ để phản ánh sự giảm tốc.

Ví dụ, nếu nhân vật của bạn rơi xuống sàn, bạn không muốn nó tích lũy tốc độ theo phương dọc do tác động của trọng lực. Thay vào đó, bạn muốn tốc độ theo phương dọc của nó được đặt lại về 0.

``move_and_slide()`` cũng có thể tính toán lại vận tốc của vật thể động học nhiều lần trong một vòng lặp vì để tạo ra chuyển động mượt mà, nó di chuyển nhân vật và xử lý va chạm tối đa năm lần theo mặc định. Khi quá trình kết thúc, vận tốc mới của nhân vật sẽ sẵn sàng để sử dụng trong frame tiếp theo.

Ví dụ
-----

Để xem các ví dụ này hoạt động, hãy tải xuống project mẫu: `character_body_2d_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/character_body_2d_starter.zip>`_

Di chuyển và tường
~~~~~~~~~~~~~~~~~~

Nếu bạn đã tải project mẫu, ví dụ này nằm trong "basic_movement.tscn".

Trong ví dụ này, hãy thêm một ``CharacterBody2D`` với hai node con: một ``Sprite2D`` và một ``CollisionShape2D``. Sử dụng "icon.svg" của Godot làm texture của Sprite2D (kéo nó từ dock Filesystem vào thuộc tính *Texture* của ``Sprite2D``). Trong thuộc tính *Shape* của ``CollisionShape2D``, chọn "New RectangleShape2D" và điều chỉnh kích thước hình chữ nhật để phủ vừa hình ảnh sprite.

.. note:: Xem :ref:`doc_2d_movement` để biết các ví dụ về cách triển khai các cơ chế di chuyển 2D.

Gắn một script vào CharacterBody2D và thêm đoạn mã sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var speed = 300

    func get_input():
        var input_dir = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
        velocity = input_dir * speed

    func _physics_process(delta):
        get_input()
        move_and_collide(velocity * delta)

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        private int _speed = 300;

        public void GetInput()
        {
            Vector2 inputDir = Input.GetVector("ui_left", "ui_right", "ui_up", "ui_down");
            Velocity = inputDir * _speed;
        }

        public override void _PhysicsProcess(double delta)
        {
            GetInput();
            MoveAndCollide(Velocity * (float)delta);
        }
    }


Chạy scene này và bạn sẽ thấy ``move_and_collide()`` hoạt động như mong đợi, di chuyển body dọc theo vector vận tốc. Bây giờ hãy xem điều gì xảy ra khi bạn thêm một số chướng ngại vật. Thêm một :ref:`StaticBody2D <class_StaticBody2D>` với shape va chạm hình chữ nhật. Để dễ quan sát, bạn có thể sử dụng Sprite2D, Polygon2D hoặc bật "Visible Collision Shapes" từ menu "Debug".

Chạy lại scene và thử di chuyển vào chướng ngại vật. Bạn sẽ thấy ``CharacterBody2D`` không thể xuyên qua chướng ngại vật. Tuy nhiên, hãy thử di chuyển vào chướng ngại vật theo một góc và bạn sẽ thấy chướng ngại vật hoạt động như keo - có cảm giác body bị mắc kẹt.

Điều này xảy ra vì không có *collision response*. ``move_and_collide()`` dừng chuyển động của body khi xảy ra va chạm. Chúng ta cần lập trình phản ứng mong muốn đối với va chạm.

Hãy thử thay đổi hàm thành ``move_and_slide()`` rồi chạy lại.

``move_and_slide()`` cung cấp phản ứng va chạm mặc định là trượt body dọc theo vật thể va chạm. Điều này hữu ích cho rất nhiều thể loại game và có thể là tất cả những gì bạn cần để đạt được hành vi mong muốn.

Nảy/phản xạ
~~~~~~~~~~~

Nếu bạn không muốn phản ứng va chạm kiểu trượt thì sao? Trong ví dụ này ("bounce_and_collide.tscn" trong project mẫu), chúng ta có một nhân vật bắn đạn và muốn những viên đạn nảy khỏi tường.

Ví dụ này sử dụng ba scene. Scene chính chứa Player và Walls. Bullet và Wall là các scene riêng biệt để có thể được instance.

Player được điều khiển bằng các phím ``w`` và ``s`` để tiến và lùi. Việc ngắm sử dụng con trỏ chuột. Đây là mã của Player, sử dụng ``move_and_slide()``:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var Bullet = preload("res://bullet.tscn")
    var speed = 200

    func get_input():
        # Thêm các action này trong Project Settings -> Input Map.
        var input_dir = Input.get_axis("backward", "forward")
        velocity = transform.x * input_dir * speed
        if Input.is_action_just_pressed("shoot"):
            shoot()

    func shoot():
        # "Muzzle" là một Marker2D được đặt ở nòng súng.
        var b = Bullet.instantiate()
        b.start($Muzzle.global_position, rotation)
        get_tree().root.add_child(b)

    func _physics_process(delta):
        get_input()
        var dir = get_global_mouse_position() - global_position
        # Không di chuyển nếu quá gần con trỏ chuột.
        if dir.length() > 5:
            rotation = dir.angle()
            move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        private PackedScene _bullet = GD.Load<PackedScene>("res://Bullet.tscn");
        private int _speed = 200;

        public void GetInput()
        {
            // Thêm các action này trong Project Settings -> Input Map.
            float inputDir = Input.GetAxis("backward", "forward");
            Velocity = Transform.X * inputDir * _speed;
            if (Input.IsActionPressed("shoot"))
            {
                Shoot();
            }
        }

        public void Shoot()
        {
            // "Muzzle" là một Marker2D được đặt ở nòng súng.
            var b = (Bullet)_bullet.Instantiate();
            b.Start(GetNode<Node2D>("Muzzle").GlobalPosition, Rotation);
            GetTree().Root.AddChild(b);
        }

        public override void _PhysicsProcess(double delta)
        {
            GetInput();
            var dir = GetGlobalMousePosition() - GlobalPosition;
            // Không di chuyển nếu quá gần con trỏ chuột.
            if (dir.Length() > 5)
            {
                Rotation = dir.Angle();
                MoveAndSlide();
            }
        }
    }


Và đây là mã của Bullet:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var speed = 750

    func start(_position, _direction):
        rotation = _direction
        position = _position
        velocity = Vector2(speed, 0).rotated(rotation)

    func _physics_process(delta):
        var collision = move_and_collide(velocity * delta)
        if collision:
            velocity = velocity.bounce(collision.get_normal())
            if collision.get_collider().has_method("hit"):
                collision.get_collider().hit()

    func _on_VisibilityNotifier2D_screen_exited():
        # Xóa viên đạn khi nó ra khỏi màn hình.
        queue_free()

 .. code-tab:: csharp

    using Godot;

    public partial class Bullet : CharacterBody2D
    {
        public int _speed = 750;

        public void Start(Vector2 position, float direction)
        {
            Rotation = direction;
            Position = position;
            Velocity = new Vector2(speed, 0).Rotated(Rotation);
        }

        public override void _PhysicsProcess(double delta)
        {
            var collision = MoveAndCollide(Velocity * (float)delta);
            if (collision != null)
            {
                Velocity = Velocity.Bounce(collision.GetNormal());
                if (collision.GetCollider().HasMethod("Hit"))
                {
                    collision.GetCollider().Call("Hit");
                }
            }
        }

        private void OnVisibilityNotifier2DScreenExited()
        {
            // Xóa viên đạn khi nó ra khỏi màn hình.
            QueueFree();
        }
    }


Hành động này diễn ra trong ``_physics_process()``. Sau khi sử dụng ``move_and_collide()``, nếu xảy ra va chạm, một đối tượng ``KinematicCollision2D`` sẽ được trả về (nếu không, giá trị trả về là ``null``).

Nếu có va chạm được trả về, chúng ta sử dụng ``normal`` của va chạm để phản xạ ``velocity`` của viên đạn bằng phương thức ``Vector2.bounce()``.

Nếu đối tượng va chạm (``collider``) có phương thức ``hit``, chúng ta cũng gọi phương thức đó. Trong project mẫu, chúng tôi đã thêm hiệu ứng màu nhấp nháy vào Wall để minh họa điều này.

.. image:: img/k2d_bullet_bounce.gif

Di chuyển kiểu platformer
~~~~~~~~~~~~~~~~~~~~~~~~~

Hãy thử thêm một ví dụ phổ biến nữa: platformer 2D. ``move_and_slide()`` rất lý tưởng để nhanh chóng xây dựng và chạy một character controller có đầy đủ chức năng. Nếu bạn đã tải project mẫu, bạn có thể tìm thấy ví dụ này trong "platformer.tscn".

Trong ví dụ này, chúng ta giả định bạn có một level được tạo từ một hoặc nhiều object ``StaticBody2D``. Chúng có thể có bất kỳ hình dạng và kích thước nào. Trong project mẫu, chúng ta sử dụng
:ref:`Polygon2D <class_Polygon2D>` để tạo các shape platform.

Đây là mã cho body của người chơi:


.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var speed = 300.0
    var jump_speed = -400.0

    func _physics_process(delta):
        # Thêm trọng lực.
        velocity += get_gravity() * delta

        # Xử lý Jump.
        if Input.is_action_just_pressed("jump") and is_on_floor():
            velocity.y = jump_speed

        # Lấy hướng đầu vào.
        var direction = Input.get_axis("ui_left", "ui_right")
        velocity.x = direction * speed

        move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        private float _speed = 100.0f;
        private float _jumpSpeed = -400.0f;

        // Lấy trọng lực từ project settings để bạn có thể đồng bộ với các node rigid body.

        public override void _PhysicsProcess(double delta)
        {
            Vector2 velocity = Velocity;

            // Thêm trọng lực.
            velocity += GetGravity() * (float)delta;

            // Xử lý jump.
            if (Input.IsActionJustPressed("jump") && IsOnFloor())
            {
                velocity.Y = _jumpSpeed;
            }

            // Lấy hướng đầu vào.
            float direction = Input.GetAxis("ui_left", "ui_right");
            velocity.X = direction * _speed;

            Velocity = velocity;
            MoveAndSlide();
        }
    }

.. image:: img/k2d_platform.gif

Trong đoạn mã này, chúng ta sử dụng ``move_and_slide()`` như đã mô tả ở trên để di chuyển body theo vector vận tốc của nó, trượt dọc theo mọi bề mặt va chạm như mặt đất hoặc một platform. Chúng ta cũng sử dụng ``is_on_floor()`` để kiểm tra xem có cho phép nhảy hay không. Nếu không có điều này, bạn sẽ có thể "nhảy" giữa không trung; rất phù hợp nếu bạn đang tạo Flappy Bird, nhưng không phù hợp với một game platformer.

Để tạo một nhân vật platformer hoàn chỉnh còn cần nhiều yếu tố khác: gia tốc, double-jump, coyote-time và nhiều yếu tố khác nữa. Đoạn mã trên chỉ là điểm khởi đầu. Bạn có thể dùng nó làm nền tảng để mở rộng thành bất kỳ hành vi di chuyển nào cần thiết cho các dự án của riêng mình.

.. _`character_body_2d_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/character_body_2d_starter.zip
