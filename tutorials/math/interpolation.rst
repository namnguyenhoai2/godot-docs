.. _doc_interpolation:

Nội suy
=======

Nội suy là một thao tác phổ biến trong lập trình đồ họa, được dùng để pha trộn hoặc chuyển tiếp giữa hai giá trị. Nội suy cũng có thể được dùng để làm mượt chuyển động, phép xoay, v.v. Việc làm quen với nội suy sẽ giúp bạn mở rộng hiểu biết với tư cách là một game developer.

Ý tưởng cơ bản là bạn muốn chuyển tiếp từ A sang B. Một giá trị ``t`` biểu diễn các trạng thái ở giữa.

Ví dụ, nếu ``t`` là 0 thì trạng thái là A. Nếu ``t`` là 1 thì trạng thái là B. Mọi giá trị ở giữa đều là một *phép nội suy*.

Giữa hai số thực (floating-point), phép nội suy có thể được mô tả như sau:

::

    interpolation = A * (1 - t) + B * t

Và thường được rút gọn thành:

::

    interpolation = A + (B - A) * t

Tên của kiểu nội suy này, biến đổi một giá trị thành một giá trị khác với *tốc độ không đổi*, là *"tuyến tính"*. Vì vậy, khi nghe nói đến *Nội suy tuyến tính*, bạn sẽ biết họ đang đề cập đến công thức này.

Có những kiểu nội suy khác nhưng sẽ không được đề cập ở đây. Bạn nên đọc trang :ref:`Bezier <doc_beziers_and_curves>` sau đó.

Nội suy vector
--------------

Các kiểu vector (:ref:`Vector2 <class_Vector2>` và :ref:`Vector3 <class_Vector3>`) cũng có thể được nội suy; chúng cung cấp các hàm tiện dụng để thực hiện việc này
:ref:`Vector2.lerp() <class_Vector2_method_lerp>` and :ref:`Vector3.lerp() <class_Vector3_method_lerp>`.

Đối với nội suy cubic, cũng có :ref:`Vector2.cubic_interpolate() <class_Vector2_method_cubic_interpolate>` và :ref:`Vector3.cubic_interpolate() <class_Vector3_method_cubic_interpolate>`, thực hiện phép nội suy theo kiểu :ref:`Bezier <doc_beziers_and_curves>`.

Sau đây là pseudo-code ví dụ để đi từ điểm A đến B bằng nội suy:

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = 0.0

    func _physics_process(delta):
        t += delta * 0.4

        $Sprite2D.position = $A.position.lerp($B.position, t)

 .. code-tab:: csharp

    private float _t = 0.0f;

    public override void _PhysicsProcess(double delta)
    {
        _t += (float)delta * 0.4f;

        Marker2D a = GetNode<Marker2D>("A");
        Marker2D b = GetNode<Marker2D>("B");
        Sprite2D sprite = GetNode<Sprite2D>("Sprite2D");

        sprite.Position = a.Position.Lerp(b.Position, _t);
    }

Nó sẽ tạo ra chuyển động sau:

.. image:: img/interpolation_vector.gif

Nội suy transform
-----------------

Bạn cũng có thể nội suy toàn bộ transform (hãy đảm bảo chúng có scale đồng nhất hoặc ít nhất có cùng scale không đồng nhất). Để làm việc này, có thể sử dụng hàm :ref:`Transform3D.interpolate_with() <class_Transform3D_method_interpolate_with>`.

Sau đây là ví dụ về việc biến đổi một con khỉ từ Position1 đến Position2:

.. image:: img/interpolation_positions.png

Sử dụng pseudocode sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var t = 0.0

    func _physics_process(delta):
        t += delta

        $Monkey.transform = $Position1.transform.interpolate_with($Position2.transform, t)

 .. code-tab:: csharp

    private float _t = 0.0f;

    public override void _PhysicsProcess(double delta)
    {
        _t += (float)delta;

        Marker3D p1 = GetNode<Marker3D>("Position1");
        Marker3D p2 = GetNode<Marker3D>("Position2");
        CSGMesh3D monkey = GetNode<CSGMesh3D>("Monkey");

        monkey.Transform = p1.Transform.InterpolateWith(p2.Transform, _t);
    }

Và một lần nữa, nó sẽ tạo ra chuyển động sau:

.. image:: img/interpolation_monkey.gif


Làm mượt chuyển động
--------------------

Nội suy có thể được dùng để bám theo mượt mà một giá trị mục tiêu đang chuyển động, chẳng hạn như vị trí hoặc phép xoay. Ở mỗi frame, ``lerp()`` di chuyển giá trị hiện tại về phía giá trị mục tiêu theo một phần trăm cố định của phần chênh lệch còn lại giữa hai giá trị. Giá trị hiện tại sẽ di chuyển mượt mà về phía mục tiêu và chậm dần khi tiến gần hơn. Sau đây là ví dụ về một hình tròn bám theo chuột bằng cách làm mượt nội suy:

.. tabs::
 .. code-tab:: gdscript GDScript

    const FOLLOW_SPEED = 4.0

    func _physics_process(delta):
        var mouse_pos = get_local_mouse_position()

        $Sprite2D.position = $Sprite2D.position.lerp(mouse_pos, delta * FOLLOW_SPEED)

 .. code-tab:: csharp

    private const float FollowSpeed = 4.0f;

    public override void _PhysicsProcess(double delta)
    {
        Vector2 mousePos = GetLocalMousePosition();

        Sprite2D sprite = GetNode<Sprite2D>("Sprite2D");

        sprite.Position = sprite.Position.Lerp(mousePos, (float)delta * FollowSpeed);
    }

Sau đây là kết quả:

.. image:: img/interpolation_follow.gif

Điều này hữu ích để làm mượt chuyển động của camera, cho các đồng minh bám theo người chơi (đảm bảo họ luôn ở trong một khoảng nhất định), và cho nhiều game pattern phổ biến khác.

.. note::
    Mặc dù sử dụng ``delta``, công thức ở trên phụ thuộc vào framerate, vì tham số ``weight`` của ``lerp()`` biểu diễn một *phần trăm* của phần chênh lệch giá trị còn lại, chứ không phải một *lượng tuyệt đối cần thay đổi*. Trong ``_physics_process()``, điều này thường không ảnh hưởng vì physics được kỳ vọng sẽ duy trì framerate không đổi, và do đó ``delta`` cũng được kỳ vọng sẽ giữ nguyên.

    Để có phiên bản làm mượt nội suy không phụ thuộc vào framerate và cũng có thể được dùng trong ``process()``, hãy sử dụng công thức sau:

    .. tabs::
        .. code-tab:: gdscript GDScript

            const FOLLOW_SPEED = 4.0

            func _process(delta):
                var mouse_pos = get_local_mouse_position()
                var weight = 1 - exp(-FOLLOW_SPEED * delta)
                $Sprite2D.position = $Sprite2D.position.lerp(mouse_pos, weight)

        .. code-tab:: csharp

            private const float FollowSpeed = 4.0f;

            public override void _Process(double delta)
            {
                Vector2 mousePos = GetLocalMousePosition();

                Sprite2D sprite = GetNode<Sprite2D>("Sprite2D");
                float weight = 1f - Mathf.Exp(-FollowSpeed * (float)delta);
                sprite.Position = sprite.Position.Lerp(mousePos, weight);
            }

    Việc suy ra công thức này nằm ngoài phạm vi của trang này. Để xem lời giải thích, hãy xem `Improved Lerp Smoothing <https://www.gamedeveloper.com/programming/improved-lerp-smoothing->`__ hoặc xem `Lerp smoothing is broken <https://www.youtube.com/watch?v=LSNQuFEDOyQ>`__.
