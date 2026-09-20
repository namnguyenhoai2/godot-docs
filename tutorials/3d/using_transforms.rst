.. _doc_using_transforms:

Sử dụng phép biến đổi 3D
~~~~~~~~~~~~~~~~~~~~~~~~

Giới thiệu
----------

Nếu bạn chưa từng làm game 3D, việc làm việc với phép xoay trong không gian ba chiều lúc đầu có thể gây khó hiểu. Xuất phát từ 2D, cách suy nghĩ tự nhiên sẽ là *"Ồ, nó cũng giống như xoay trong 2D thôi, chỉ khác là bây giờ phép xoay diễn ra trên X, Y và Z"*.

Thoạt đầu, điều này có vẻ dễ dàng. Với các game đơn giản, cách suy nghĩ này thậm chí có thể là đủ. Đáng tiếc là nó thường không đúng.

Các góc trong không gian ba chiều thường được gọi là "Góc Euler".

.. image:: img/transforms_euler.webp

Góc Euler được nhà toán học Leonhard Euler giới thiệu vào đầu những năm 1700.

.. image:: img/transforms_euler_himself.png

Cách biểu diễn phép xoay 3D này mang tính đột phá vào thời điểm đó, nhưng có một số hạn chế khi được sử dụng trong phát triển game (điều này có thể dự đoán được ở một người đội chiếc mũ buồn cười). Tài liệu này nhằm giải thích lý do, đồng thời trình bày các phương pháp tốt nhất để xử lý transform khi lập trình game 3D.


Các vấn đề của góc Euler
------------------------

Mặc dù có vẻ trực quan khi cho rằng mỗi trục có một phép xoay, sự thật là cách này hoàn toàn không thực tế.

Thứ tự trục
===========

Lý do chính là không có một cách *duy nhất* để tạo orientation từ các góc. Không có hàm toán học tiêu chuẩn nào nhận tất cả các góc và tạo ra một phép xoay 3D thực sự. Cách duy nhất để tạo orientation từ các góc là xoay đối tượng lần lượt theo từng góc, theo một *thứ tự tùy ý*.

Bạn có thể xoay theo *X* trước, sau đó là *Y* rồi đến *Z*. Hoặc bạn có thể xoay theo *Y* trước, sau đó là *Z* và cuối cùng là *X*. Cách nào cũng được, nhưng tùy vào thứ tự, orientation cuối cùng của đối tượng sẽ *không nhất thiết giống nhau*. Thật vậy, điều này có nghĩa là có nhiều cách để tạo orientation từ 3 góc khác nhau, tùy thuộc vào *thứ tự của các phép xoay*.

Sau đây là hình ảnh trực quan hóa các trục xoay (theo thứ tự X, Y, Z) trong một gimbal (từ Wikipedia). Như bạn có thể thấy, orientation của mỗi trục phụ thuộc vào phép xoay của trục trước đó:

.. image:: img/transforms_gimbal.gif

Có thể bạn đang thắc mắc điều này ảnh hưởng đến mình như thế nào. Hãy xem một ví dụ thực tế:

Hãy tưởng tượng bạn đang làm một first-person controller (ví dụ: game FPS). Di chuyển chuột sang trái và phải sẽ điều khiển góc nhìn song song với mặt đất, còn di chuyển chuột lên và xuống sẽ di chuyển góc nhìn của người chơi lên và xuống.

Trong trường hợp này, để đạt được hiệu ứng mong muốn, trước tiên phải áp dụng phép xoay trên trục *Y* ("lên" trong trường hợp này, vì Godot sử dụng orientation "Y-Up"), sau đó áp dụng phép xoay trên trục *X*.

.. image:: img/transforms_rotate1.gif

Nếu áp dụng phép xoay trên trục *X* trước, rồi trên *Y*, hiệu ứng sẽ không như mong muốn:

.. image:: img/transforms_rotate2.gif

Tùy thuộc vào loại game hoặc hiệu ứng mong muốn, thứ tự áp dụng các phép xoay trục có thể khác nhau. Vì vậy, chỉ áp dụng phép xoay trên X, Y và Z là chưa đủ: bạn còn cần một *thứ tự xoay*.

Nội suy
=======

Một vấn đề khác khi sử dụng góc Euler là nội suy. Hãy tưởng tượng bạn muốn chuyển tiếp giữa hai vị trí camera hoặc kẻ địch khác nhau (bao gồm cả phép xoay). Một cách tiếp cận hợp lý là nội suy các góc từ vị trí này sang vị trí tiếp theo. Bạn có thể mong đợi kết quả trông như sau:

.. image:: img/transforms_interpolate1.gif

Nhưng khi sử dụng góc, điều này không phải lúc nào cũng tạo ra hiệu ứng như mong đợi:

.. image:: img/transforms_interpolate2.gif

Camera thực sự đã xoay theo hướng ngược lại!

Có một vài lý do khiến điều này xảy ra:

* Các phép xoay không ánh xạ tuyến tính với orientation, vì vậy việc nội suy chúng không phải lúc nào cũng tạo ra đường đi ngắn nhất (tức là đi từ ``270`` đến ``0`` độ không giống với đi từ ``270`` đến ``360``, dù các góc tương đương nhau). * Gimbal lock cũng có tác động (trục được xoay đầu tiên và cuối cùng thẳng hàng, do đó mất một bậc tự do). Xem `Wikipedia's page on Gimbal Lock <https://en.wikipedia.org/wiki/Gimbal_lock>`_ để biết giải thích chi tiết về vấn đề này.

Nói không với góc Euler
=======================

Kết quả của tất cả những điều này là bạn **không nên sử dụng** thuộc tính ``rotation`` của các node :ref:`class_Node3D` trong Godot cho game. Thuộc tính này chủ yếu dùng trong editor, để nhất quán với engine 2D, và cho các phép xoay đơn giản (thường chỉ trên một trục, hoặc trên hai trục trong một số trường hợp hạn chế). Dù bạn có thể bị cám dỗ đến đâu, cũng đừng sử dụng nó.

Thay vào đó, có một cách tốt hơn để giải quyết các vấn đề về phép xoay.

Giới thiệu về transform
-----------------------

Godot sử dụng kiểu dữ liệu :ref:`class_Transform3D` cho orientation. Mỗi node :ref:`class_Node3D` chứa một thuộc tính ``transform`` tương đối với transform của node cha, nếu node cha là kiểu dẫn xuất từ Node3D.

Bạn cũng có thể truy cập transform tọa độ thế giới thông qua thuộc tính ``global_transform``.

Một transform có một :ref:`class_Basis` (thuộc tính con transform.basis), bao gồm ba vector :ref:`class_Vector3`. Các vector này được truy cập thông qua thuộc tính ``transform.basis`` và có thể được truy cập trực tiếp bằng ``transform.basis.x``, ``transform.basis.y`` và ``transform.basis.z``. Mỗi vector chỉ theo hướng mà trục tương ứng đã được xoay, vì vậy về cơ bản chúng mô tả toàn bộ phép xoay của node. Scale (miễn là đồng nhất) cũng có thể được suy ra từ độ dài của các trục. Một *basis* cũng có thể được hiểu là một ma trận 3x3 và được sử dụng như ``transform.basis[x][y]``.

Một basis mặc định (chưa được chỉnh sửa) tương đương với:

.. tabs::
 .. code-tab:: gdscript GDScript

    var basis = Basis()
    # Chứa các giá trị mặc định sau:
    basis.x = Vector3(1, 0, 0) # Vector trỏ dọc theo trục X
    basis.y = Vector3(0, 1, 0) # Vector trỏ dọc theo trục Y
    basis.z = Vector3(0, 0, 1) # Vector trỏ dọc theo trục Z

 .. code-tab:: csharp

    // Do các hạn chế kỹ thuật đối với struct trong C#, constructor mặc định
    // sẽ chứa giá trị 0 cho tất cả các trường.
    var defaultBasis = new Basis();
    GD.Print(defaultBasis); // in ra: ((0, 0, 0), (0, 0, 0), (0, 0, 0))

    // Thay vào đó, chúng ta có thể sử dụng thuộc tính Identity.
    var identityBasis = Basis.Identity;
    GD.Print(identityBasis.X); // in ra: (1, 0, 0)
    GD.Print(identityBasis.Y); // in ra: (0, 1, 0)
    GD.Print(identityBasis.Z); // in ra: (0, 0, 1)

    // Basis Identity tương đương với:
    var basis = new Basis(Vector3.Right, Vector3.Up, Vector3.Back);
    GD.Print(basis); // in ra: ((1, 0, 0), (0, 1, 0), (0, 0, 1))

Đây cũng là dạng tương đương của ma trận đơn vị 3x3.

Theo quy ước OpenGL, ``X`` là trục *Right*, ``Y`` là trục *Up* và ``Z`` là trục *Forward*.

Cùng với *basis*, một transform còn có *origin*. Đây là một *Vector3* xác định khoảng cách từ origin thực tế ``(0, 0, 0)`` đến transform này. Kết hợp *basis* với *origin*, một *transform* biểu diễn hiệu quả một phép tịnh tiến, phép xoay và scale duy nhất trong không gian.

.. image:: img/transforms_camera.png


Một cách để hình dung transform là xem gizmo 3D của đối tượng khi đang ở chế độ "local space".

.. image:: img/transforms_local_space.png

Các mũi tên của gizmo biểu thị các trục ``X``, ``Y`` và ``Z`` (lần lượt có màu đỏ, xanh lá và xanh dương) của basis, còn tâm của gizmo nằm tại origin của đối tượng.

.. image:: img/transforms_gizmo.png

Để biết thêm thông tin về toán học của vector và transform, vui lòng đọc các tutorial :ref:`doc_vector_math`.

Thao tác với transform
======================

Tất nhiên, transform không dễ thao tác như các góc và bản thân chúng cũng có những vấn đề riêng.

Bạn có thể xoay một transform bằng cách nhân basis của nó với một basis khác (được gọi là tích lũy), hoặc bằng cách sử dụng các phương thức xoay.

.. tabs::
 .. code-tab:: gdscript GDScript

    var axis = Vector3(1, 0, 0) # Hoặc Vector3.RIGHT
    var rotation_amount = 0.1
    # Xoay transform quanh trục X 0.1 radian.
    transform.basis = Basis(axis, rotation_amount) * transform.basis
    # viết rút gọn
    transform.basis = transform.basis.rotated(axis, rotation_amount)

 .. code-tab:: csharp

    Transform3D transform = Transform;
    Vector3 axis = new Vector3(1, 0, 0); // Hoặc Vector3.Right
    float rotationAmount = 0.1f;

    // Xoay transform quanh trục X 0.1 radian.
    transform.Basis = new Basis(axis, rotationAmount) * transform.Basis;
    // viết rút gọn
    transform.Basis = transform.Basis.Rotated(axis, rotationAmount);

    Transform = transform;

Một phương thức trong Node3D đơn giản hóa việc này:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Xoay transform quanh trục X 0.1 radian.
    rotate(Vector3(1, 0, 0), 0.1)
    # viết rút gọn
    rotate_x(0.1)

 .. code-tab:: csharp

    // Xoay transform quanh trục X 0.1 radian.
    Rotate(new Vector3(1, 0, 0), 0.1f);
    // viết rút gọn
    RotateX(0.1f);

Thao tác này xoay node tương đối với node cha.

Để xoay tương đối với object space (transform của chính node), hãy sử dụng như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Xoay quanh trục X cục bộ của đối tượng 0.1 radian.
    rotate_object_local(Vector3(1, 0, 0), 0.1)

 .. code-tab:: csharp

    // Xoay quanh trục X cục bộ của đối tượng 0.1 radian.
    RotateObjectLocal(new Vector3(1, 0, 0), 0.1f);

Trục phải được xác định trong hệ tọa độ cục bộ của đối tượng. Ví dụ, để xoay quanh các trục X, Y hoặc Z cục bộ của đối tượng, hãy sử dụng ``Vector3.RIGHT`` cho trục X, ``Vector3.UP`` cho trục Y và ``Vector3.FORWARD`` cho trục Z.

Lỗi độ chính xác
================

Việc thực hiện các thao tác liên tiếp trên transform sẽ làm mất độ chính xác do lỗi số dấu phẩy động. Điều này có nghĩa là scale của mỗi trục có thể không còn chính xác là ``1.0``, và các trục có thể không còn cách nhau chính xác ``90`` độ.

Nếu một transform được xoay trong mỗi frame, cuối cùng nó sẽ bắt đầu bị biến dạng theo thời gian. Điều này là không thể tránh khỏi.

Có hai cách khác nhau để xử lý việc này. Cách đầu tiên là *orthonormalize* transform sau một khoảng thời gian (có thể là một lần mỗi frame nếu bạn chỉnh sửa nó trong mỗi frame):

.. tabs::
 .. code-tab:: gdscript GDScript

    transform = transform.orthonormalized()

 .. code-tab:: csharp

    transform = transform.Orthonormalized();

Thao tác này sẽ làm cho tất cả các trục có độ dài ``1.0`` trở lại và cách nhau ``90`` độ. Tuy nhiên, mọi scale được áp dụng cho transform sẽ bị mất.

Bạn nên tránh scale các node sẽ được thao tác; thay vào đó, hãy scale các node con của chúng (chẳng hạn như MeshInstance3D). Nếu bắt buộc phải scale node, hãy áp dụng lại scale ở cuối:

.. tabs::
 .. code-tab:: gdscript GDScript

    transform = transform.orthonormalized()
    transform = transform.scaled(scale)

 .. code-tab:: csharp

    transform = transform.Orthonormalized();
    transform = transform.Scaled(scale);

Thu thập thông tin
==================

Có thể lúc này bạn đang nghĩ: **"Được rồi, nhưng làm thế nào để lấy các góc từ một transform?"**. Câu trả lời một lần nữa là: bạn không làm vậy. Bạn phải cố gắng hết sức để ngừng suy nghĩ theo các góc.

Hãy tưởng tượng bạn cần bắn một viên đạn theo hướng mà nhân vật của bạn đang nhìn. Chỉ cần sử dụng trục forward.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Trên RigidBody3D.

    # Hãy nhớ rằng -Z là hướng forward.
    bullet.transform = transform
    bullet.linear_velocity = -transform.basis.z * BULLET_SPEED

 .. code-tab:: csharp

    // Trên RigidBody3D.

    // Hãy nhớ rằng -Z là hướng forward.
    bullet.Transform = Transform;
    bullet.LinearVelocity = -Transform.Basis.Z * BulletSpeed;

Kẻ địch có đang nhìn về phía người chơi không? Hãy sử dụng tích vô hướng (dot product) cho việc này (xem tutorial :ref:`doc_vector_math` để biết giải thích về tích vô hướng):

.. tabs::
 .. code-tab:: gdscript GDScript

    # Lấy vector hướng từ người chơi đến kẻ địch
    var direction = enemy.transform.origin - player.transform.origin
    if direction.dot(enemy.transform.basis.z) > 0:
        enemy.im_watching_you(player)

 .. code-tab:: csharp

    // Lấy vector hướng từ người chơi đến kẻ địch
    Vector3 direction = enemy.Transform.Origin - player.Transform.Origin;
    if (direction.Dot(enemy.Transform.Basis.Z) > 0)
    {
        enemy.ImWatchingYou(player);
    }

Di chuyển ngang sang trái:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Trên CharacterBody3D.

    # Hãy nhớ rằng -X là bên trái.
    if Input.is_action_pressed("strafe_left"):
        velocity = -transform.basis.x * MOVE_SPEED

    move_and_slide()

 .. code-tab:: csharp

    // Trên CharacterBody3D.

    // Hãy nhớ rằng -X là bên trái.
    if (Input.IsActionPressed("strafe_left"))
    {
        Velocity = -Transform.Basis.X * MoveSpeed;
    }

    MoveAndSlide();

Nhảy:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Trên CharacterBody3D.

    # Hãy nhớ rằng +Y là hướng lên.
    if Input.is_action_just_pressed("jump"):
        velocity.y = JUMP_SPEED

    move_and_slide()

 .. code-tab:: csharp

    // Trên CharacterBody3D.

    // Hãy nhớ rằng +Y là hướng lên.
    if (Input.IsActionJustPressed("jump"))
    {
        Velocity = Vector3.Up * JumpSpeed;
    }

    MoveAndSlide();

Mọi hành vi và logic phổ biến đều có thể được thực hiện chỉ bằng các vector.

Thiết lập thông tin
===================

Tất nhiên, có những trường hợp bạn muốn thiết lập thông tin cho một transform. Hãy hình dung một controller góc nhìn thứ nhất hoặc một camera quỹ đạo. Những trường hợp này chắc chắn được thực hiện bằng các góc, vì bạn *thực sự muốn* các transform diễn ra theo một thứ tự cụ thể.

Trong những trường hợp như vậy, hãy giữ các góc và rotation *bên ngoài* transform rồi thiết lập chúng ở mỗi frame. Đừng cố lấy lại và sử dụng lại chúng, vì transform không được thiết kế để sử dụng theo cách này.

Ví dụ về việc quan sát xung quanh theo phong cách FPS:

.. tabs::
 .. code-tab:: gdscript GDScript

    # các bộ tích lũy
    var rot_x = 0
    var rot_y = 0

    func _input(event):
        if event is InputEventMouseMotion and event.button_mask & 1:
            # thay đổi rotation chuột đã tích lũy
            rot_x -= event.screen_relative.x * LOOKAROUND_SPEED
            rot_y -= event.screen_relative.y * LOOKAROUND_SPEED
            transform.basis = Basis() # đặt lại rotation
            rotate_object_local(Vector3(0, 1, 0), rot_x) # đầu tiên xoay theo Y
            rotate_object_local(Vector3(1, 0, 0), rot_y) # sau đó xoay theo X

 .. code-tab:: csharp

    // các bộ tích lũy
    private float _rotationX = 0f;
    private float _rotationY = 0f;

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventMouseMotion mouseMotion)
        {
            // thay đổi rotation chuột đã tích lũy
            _rotationX -= mouseMotion.ScreenRelative.X * LookAroundSpeed;
            _rotationY -= mouseMotion.ScreenRelative.Y * LookAroundSpeed;

            // đặt lại rotation
            Transform3D transform = Transform;
            transform.Basis = Basis.Identity;
            Transform = transform;

            RotateObjectLocal(Vector3.Up, _rotationX); // đầu tiên xoay quanh Y
            RotateObjectLocal(Vector3.Right, _rotationY); // sau đó xoay quanh X
        }
    }

Như bạn có thể thấy, trong những trường hợp như vậy, việc giữ rotation ở bên ngoài rồi sử dụng transform làm hướng *cuối cùng* thậm chí còn đơn giản hơn.

Nội suy bằng quaternion
=======================

Có thể thực hiện nội suy giữa hai transform một cách hiệu quả bằng quaternion. Bạn có thể tìm thêm thông tin về cách quaternion hoạt động ở những nơi khác trên Internet. Để sử dụng trong thực tế, chỉ cần hiểu rằng công dụng chính của chúng gần như là thực hiện nội suy theo đường đi ngắn nhất. Nghĩa là, nếu bạn có hai rotation, một quaternion sẽ cho phép nội suy mượt mà giữa chúng bằng cách sử dụng trục gần nhất.

Việc chuyển một rotation thành quaternion khá đơn giản.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Chuyển basis thành quaternion, hãy nhớ rằng scale sẽ bị mất
    var a = Quaternion(transform.basis)
    var b = Quaternion(transform2.basis)
    # Nội suy bằng nội suy tuyến tính hình cầu (SLERP).
    var c = a.slerp(b,0.5) # tìm điểm giữa a và b
    # Áp dụng ngược lại
    transform.basis = Basis(c)

 .. code-tab:: csharp

    // Chuyển basis thành quaternion, hãy nhớ rằng scale sẽ bị mất
    var a = new Quaternion(transform.Basis);
    var b = new Quaternion(transform2.Basis);
    // Nội suy bằng nội suy tuyến tính hình cầu (SLERP).
    var c = a.Slerp(b, 0.5f); // tìm điểm giữa a và b
    // Áp dụng ngược lại
    transform.Basis = new Basis(c);

Tài liệu tham chiếu kiểu :ref:`class_Quaternion` có thêm thông tin về kiểu dữ liệu này (nó cũng có thể thực hiện tích lũy transform, biến đổi các điểm, v.v., mặc dù việc này ít được sử dụng hơn). Nếu bạn nội suy hoặc áp dụng các phép toán cho quaternion nhiều lần, hãy nhớ rằng cuối cùng chúng cần được chuẩn hóa. Nếu không, chúng cũng sẽ gặp lỗi do độ chính xác số.

Quaternion rất hữu ích khi thực hiện nội suy camera/path/v.v., vì kết quả luôn chính xác và mượt mà.

Transform là người bạn của bạn
------------------------------

Đối với hầu hết người mới bắt đầu, việc làm quen với cách làm việc cùng transform có thể mất một khoảng thời gian. Tuy nhiên, một khi đã quen, bạn sẽ đánh giá cao sự đơn giản và sức mạnh của chúng.

Đừng ngần ngại yêu cầu trợ giúp về chủ đề này trong bất kỳ `cộng đồng trực tuyến nào của Godot <https://godotengine.org/community>`_ và khi đã đủ tự tin, hãy giúp đỡ những người khác!
