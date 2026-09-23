.. _doc_using_transforms:

Sử dụng phép biến đổi 3D
~~~~~~~~~~~~~~~~~~~~~~~~

Giới thiệu
----------

Nếu bạn chưa từng làm game 3D, việc xử lý phép quay trong không gian ba chiều lúc đầu có thể khá khó hiểu. Nếu xuất phát từ 2D, cách suy nghĩ tự nhiên sẽ là *"Ồ, nó cũng giống như xoay trong 2D thôi, chỉ khác là giờ phép quay diễn ra trên các trục X, Y và Z"*.

Thoạt đầu, cách này có vẻ dễ hiểu. Với các game đơn giản, cách suy nghĩ này thậm chí có thể là đủ. Đáng tiếc là nó thường không đúng.

Góc trong không gian ba chiều thường được gọi là "Euler Angles".

.. image:: img/transforms_euler.webp

Euler angles được nhà toán học Leonhard Euler giới thiệu vào đầu những năm 1700.

.. image:: img/transforms_euler_himself.png

Cách biểu diễn phép quay 3D này từng mang tính đột phá vào thời điểm đó, nhưng có một số hạn chế khi được sử dụng trong phát triển game (điều này cũng dễ hiểu ở một người đội chiếc mũ ngộ nghĩnh). Tài liệu này nhằm giải thích lý do, đồng thời trình bày các phương pháp tốt nhất để xử lý các phép biến đổi khi lập trình game 3D.


Các vấn đề của Euler angles
---------------------------

Mặc dù việc mỗi trục có một phép quay riêng có vẻ trực quan, sự thật là cách này không thực tế.

Thứ tự trục
===========

Lý do chính là không có một cách *duy nhất* để xây dựng một hướng từ các góc. Không có hàm toán học tiêu chuẩn nào nhận tất cả các góc cùng lúc và tạo ra một phép quay 3D thực sự. Cách duy nhất để tạo ra một hướng từ các góc là xoay đối tượng theo từng góc, theo một *thứ tự tùy ý*.

Có thể thực hiện việc này bằng cách xoay trước theo *X*, sau đó theo *Y* và cuối cùng theo *Z*. Ngoài ra, bạn có thể xoay trước theo *Y*, sau đó theo *Z* và cuối cùng theo *X*. Cách nào cũng được, nhưng tùy theo thứ tự, hướng cuối cùng của đối tượng *không nhất thiết giống nhau*. Điều này có nghĩa là có nhiều cách để xây dựng một hướng từ 3 góc khác nhau, tùy thuộc vào *thứ tự các phép quay*.

Dưới đây là hình minh họa các trục quay (theo thứ tự X, Y, Z) trong một gimbal (từ Wikipedia). Như bạn có thể thấy, hướng của mỗi trục phụ thuộc vào phép quay của trục trước đó:

.. image:: img/transforms_gimbal.gif

Bạn có thể đang thắc mắc điều này ảnh hưởng đến mình như thế nào. Hãy xem một ví dụ thực tế:

Hãy tưởng tượng bạn đang làm một first-person controller (ví dụ: game FPS). Di chuyển chuột sang trái và phải sẽ điều khiển góc nhìn song song với mặt đất, còn di chuyển chuột lên và xuống sẽ di chuyển góc nhìn của người chơi lên và xuống.

Trong trường hợp này, để đạt được hiệu ứng mong muốn, trước tiên phải áp dụng phép quay trên trục *Y* (trong trường hợp này là "lên", vì Godot sử dụng hướng "Y-Up"), sau đó áp dụng phép quay trên trục *X*.

.. image:: img/transforms_rotate1.gif

Nếu áp dụng phép quay trên trục *X* trước, rồi trên *Y*, hiệu ứng sẽ không như mong muốn:

.. image:: img/transforms_rotate2.gif

Tùy thuộc vào loại game hoặc hiệu ứng mong muốn, thứ tự áp dụng các phép quay theo trục có thể khác nhau. Vì vậy, chỉ áp dụng phép quay theo X, Y và Z là chưa đủ: bạn còn cần một *thứ tự quay*.

Nội suy
=======

Một vấn đề khác khi sử dụng Euler angles là nội suy. Hãy tưởng tượng bạn muốn chuyển đổi giữa hai vị trí khác nhau của camera hoặc kẻ địch (bao gồm cả phép quay). Một cách tiếp cận hợp lý là nội suy các góc từ vị trí này sang vị trí kia. Ta sẽ mong đợi kết quả trông như sau:

.. image:: img/transforms_interpolate1.gif

Nhưng khi sử dụng các góc, kết quả không phải lúc nào cũng như mong đợi:

.. image:: img/transforms_interpolate2.gif

Thực tế camera đã xoay theo hướng ngược lại!

Có một vài lý do khiến điều này xảy ra:

* Các phép quay không ánh xạ tuyến tính với hướng, vì vậy nội suy chúng không phải lúc nào cũng tạo ra đường đi ngắn nhất (tức là đi từ ``270`` đến ``0`` độ không giống với đi từ ``270`` đến ``360``, mặc dù các góc là tương đương).
* Gimbal lock đang xảy ra (trục được xoay đầu tiên và cuối cùng thẳng hàng, khiến mất một bậc tự do). Xem `trang Wikipedia về Gimbal Lock <https://en.wikipedia.org/wiki/Gimbal_lock>`_ để biết giải thích chi tiết về vấn đề này.

Nói không với Euler angles
==========================

Kết luận là bạn **không nên sử dụng** thuộc tính ``rotation`` của các node :ref:`class_Node3D` trong Godot cho game. Thuộc tính này chủ yếu được dùng trong editor, để nhất quán với engine 2D, và cho các phép quay đơn giản (thường chỉ trên một trục, hoặc trong một số trường hợp hạn chế là hai trục). Dù có thể bạn rất muốn sử dụng, đừng dùng nó.

Thay vào đó, có một cách tốt hơn để giải quyết các vấn đề về phép quay.

Giới thiệu về các phép biến đổi
-------------------------------

Godot sử dụng kiểu dữ liệu :ref:`class_Transform3D` cho các hướng. Mỗi node :ref:`class_Node3D` chứa một thuộc tính ``transform`` tương đối so với phép biến đổi của node cha, nếu node cha thuộc kiểu dẫn xuất từ Node3D.

Bạn cũng có thể truy cập phép biến đổi tọa độ thế giới thông qua thuộc tính ``global_transform``.

Một phép biến đổi có một :ref:`class_Basis` (thuộc tính con transform.basis), bao gồm ba vector :ref:`class_Vector3`. Bạn truy cập các vector này thông qua thuộc tính ``transform.basis`` và có thể truy cập trực tiếp bằng ``transform.basis.x``, ``transform.basis.y`` và ``transform.basis.z``. Mỗi vector chỉ theo hướng mà trục tương ứng đã xoay, vì vậy chúng mô tả hiệu quả toàn bộ phép quay của node. Scale (miễn là đồng nhất) cũng có thể được suy ra từ độ dài của các trục. Một *basis* cũng có thể được diễn giải như một ma trận 3x3 và được sử dụng như ``transform.basis[x][y]``.

Một basis mặc định (chưa chỉnh sửa) tương đương với:

.. tabs::
 .. code-tab:: gdscript GDScript

    var basis = Basis()
    # Chứa các giá trị mặc định sau:
    basis.x = Vector3(1, 0, 0) # Vector hướng dọc theo trục X
    basis.y = Vector3(0, 1, 0) # Vector hướng dọc theo trục Y
    basis.z = Vector3(0, 0, 1) # Vector hướng dọc theo trục Z

 .. code-tab:: csharp

    // Do các giới hạn kỹ thuật đối với struct trong C#, constructor mặc định
    // sẽ chứa giá trị 0 cho tất cả các trường.
    var defaultBasis = new Basis();
    GD.Print(defaultBasis); // in ra: ((0, 0, 0), (0, 0, 0), (0, 0, 0))

    // Thay vào đó, chúng ta có thể sử dụng thuộc tính Identity.
    var identityBasis = Basis.Identity;
    GD.Print(identityBasis.X); // in ra: (1, 0, 0)
    GD.Print(identityBasis.Y); // in ra: (0, 1, 0)
    GD.Print(identityBasis.Z); // in ra: (0, 0, 1)

    // Cơ sở Identity tương đương với:
    var basis = new Basis(Vector3.Right, Vector3.Up, Vector3.Back);
    GD.Print(basis); // in ra: ((1, 0, 0), (0, 1, 0), (0, 0, 1))

Đây cũng là một dạng tương tự của ma trận identity 3x3.

Theo quy ước của OpenGL, ``X`` là trục *Right*, ``Y`` là trục *Up* và ``Z`` là trục *Forward*.

Cùng với *basis*, một transform cũng có *origin*. Đây là một *Vector3* xác định khoảng cách từ origin thực tế ``(0, 0, 0)`` đến transform này. Kết hợp *basis* với *origin*, một *transform* biểu diễn hiệu quả một phép tịnh tiến, xoay và scale duy nhất trong không gian.

.. image:: img/transforms_camera.png


Một cách để hình dung transform là xem gizmo 3D của một đối tượng khi đang ở chế độ "local space".

.. image:: img/transforms_local_space.png

Các mũi tên của gizmo hiển thị các trục ``X``, ``Y`` và ``Z`` (lần lượt có màu đỏ, xanh lá và xanh dương) của basis, còn tâm của gizmo nằm tại origin của đối tượng.

.. image:: img/transforms_gizmo.png

Để biết thêm thông tin về toán học của vector và transform, hãy đọc các :ref:`doc_vector_math` tutorial.

Thao tác với transform
======================

Tất nhiên, transform không dễ thao tác như angle và cũng có những vấn đề riêng.

Có thể xoay một transform bằng cách nhân basis của nó với một basis khác (gọi là tích lũy), hoặc bằng cách sử dụng các phương thức xoay.

.. tabs::
 .. code-tab:: gdscript GDScript

    var axis = Vector3(1, 0, 0) # Hoặc Vector3.RIGHT
    var rotation_amount = 0.1
    # Xoay transform quanh trục X một góc 0.1 radian.
    transform.basis = Basis(axis, rotation_amount) * transform.basis
    # đã rút gọn
    transform.basis = transform.basis.rotated(axis, rotation_amount)

 .. code-tab:: csharp

    Transform3D transform = Transform;
    Vector3 axis = new Vector3(1, 0, 0); // Hoặc Vector3.Right
    float rotationAmount = 0.1f;

    // Xoay transform quanh trục X một góc 0.1 radian.
    transform.Basis = new Basis(axis, rotationAmount) * transform.Basis;
    // đã rút gọn
    transform.Basis = transform.Basis.Rotated(axis, rotationAmount);

    Transform = transform;

Một phương thức trong Node3D giúp đơn giản hóa việc này:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Xoay transform quanh trục X một góc 0.1 radian.
    rotate(Vector3(1, 0, 0), 0.1)
    # đã rút gọn
    rotate_x(0.1)

 .. code-tab:: csharp

    // Xoay transform quanh trục X một góc 0.1 radian.
    Rotate(new Vector3(1, 0, 0), 0.1f);
    // đã rút gọn
    RotateX(0.1f);

Thao tác này xoay node tương đối so với node cha.

Để xoay tương đối so với object space (transform riêng của node), hãy sử dụng như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Xoay quanh trục X cục bộ của đối tượng một góc 0.1 radian.
    rotate_object_local(Vector3(1, 0, 0), 0.1)

 .. code-tab:: csharp

    // Xoay quanh trục X cục bộ của đối tượng một góc 0.1 radian.
    RotateObjectLocal(new Vector3(1, 0, 0), 0.1f);

Trục phải được xác định trong hệ tọa độ cục bộ của đối tượng. Ví dụ, để xoay quanh trục X, Y hoặc Z cục bộ của đối tượng, hãy sử dụng ``Vector3.RIGHT`` cho trục X, ``Vector3.UP`` cho trục Y và ``Vector3.FORWARD`` cho trục Z.

Lỗi độ chính xác
================

Thực hiện các thao tác liên tiếp trên transform sẽ làm giảm độ chính xác do lỗi số thực dấu phẩy động. Điều này có nghĩa là scale của mỗi trục có thể không còn chính xác là ``1.0``, và chúng có thể không còn cách nhau chính xác ``90`` độ.

Nếu một transform được xoay ở mỗi frame, theo thời gian nó sẽ dần bị biến dạng. Điều này không thể tránh khỏi.

Có hai cách khác nhau để xử lý việc này. Cách đầu tiên là *orthonormalize* transform sau một khoảng thời gian (có thể là một lần mỗi frame nếu bạn sửa đổi nó ở mỗi frame):

.. tabs::
 .. code-tab:: gdscript GDScript

    transform = transform.orthonormalized()

 .. code-tab:: csharp

    transform = transform.Orthonormalized();

Thao tác này sẽ đưa tất cả các trục về độ dài ``1.0`` và cách nhau ``90`` độ. Tuy nhiên, mọi scale được áp dụng cho transform sẽ bị mất.

Bạn nên tránh scale các node sẽ được thao tác; thay vào đó, hãy scale các node con của chúng (chẳng hạn như MeshInstance3D). Nếu nhất thiết phải scale node, hãy áp dụng lại scale đó ở cuối:

.. tabs::
 .. code-tab:: gdscript GDScript

    transform = transform.orthonormalized()
    transform = transform.scaled(scale)

 .. code-tab:: csharp

    transform = transform.Orthonormalized();
    transform = transform.Scaled(scale);

Lấy thông tin
=============

Có thể lúc này bạn đang nghĩ: **"Được rồi, nhưng làm thế nào để lấy angle từ một transform?"**. Câu trả lời một lần nữa là: không thể. Bạn phải cố gắng không suy nghĩ theo angle nữa.

Hãy tưởng tượng bạn cần bắn một viên đạn theo hướng mà người chơi đang nhìn. Chỉ cần sử dụng trục forward.

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

Kẻ địch có đang nhìn người chơi không? Hãy sử dụng tích vô hướng cho việc này (xem :ref:`doc_vector_math` tutorial để biết giải thích về tích vô hướng):

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

Mọi hành vi và logic phổ biến đều có thể được thực hiện chỉ bằng vector.

Thiết lập thông tin
===================

Tất nhiên, có những trường hợp bạn muốn thiết lập thông tin cho một transform. Hãy hình dung một bộ điều khiển góc nhìn thứ nhất hoặc camera orbit. Những trường hợp này chắc chắn được thực hiện bằng các góc, vì bạn *thực sự muốn* các transform diễn ra theo một thứ tự cụ thể.

Trong những trường hợp như vậy, hãy giữ các góc và rotation *bên ngoài* transform rồi thiết lập chúng ở mỗi frame. Đừng cố lấy lại và tái sử dụng chúng, vì transform không được thiết kế để dùng theo cách này.

Ví dụ về việc nhìn xung quanh theo kiểu FPS:

.. tabs::
 .. code-tab:: gdscript GDScript

    # các biến tích lũy
    var rot_x = 0
    var rot_y = 0

    func _input(event):
        if event is InputEventMouseMotion and event.button_mask & 1:
            # thay đổi rotation của chuột đã tích lũy
            rot_x -= event.screen_relative.x * LOOKAROUND_SPEED
            rot_y -= event.screen_relative.y * LOOKAROUND_SPEED
            transform.basis = Basis() # đặt lại rotation
            rotate_object_local(Vector3(0, 1, 0), rot_x) # xoay theo Y trước
            rotate_object_local(Vector3(1, 0, 0), rot_y) # sau đó xoay theo X

 .. code-tab:: csharp

    // các biến tích lũy
    private float _rotationX = 0f;
    private float _rotationY = 0f;

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventMouseMotion mouseMotion)
        {
            // thay đổi rotation của chuột đã tích lũy
            _rotationX -= mouseMotion.ScreenRelative.X * LookAroundSpeed;
            _rotationY -= mouseMotion.ScreenRelative.Y * LookAroundSpeed;

            // đặt lại rotation
            Transform3D transform = Transform;
            transform.Basis = Basis.Identity;
            Transform = transform;

            RotateObjectLocal(Vector3.Up, _rotationX); // xoay quanh Y trước
            RotateObjectLocal(Vector3.Right, _rotationY); // sau đó xoay quanh X
        }
    }

Như bạn có thể thấy, trong những trường hợp như vậy, việc giữ rotation ở bên ngoài rồi dùng transform làm hướng *cuối cùng* thậm chí còn đơn giản hơn.

Nội suy bằng quaternion
=======================

Có thể nội suy hiệu quả giữa hai transform bằng quaternion. Bạn có thể tìm thêm thông tin về cách quaternion hoạt động ở những nơi khác trên Internet. Để sử dụng trong thực tế, chỉ cần hiểu rằng công dụng chính của chúng là thực hiện nội suy theo đường đi gần nhất. Nghĩa là, nếu bạn có hai rotation, quaternion sẽ cho phép nội suy mượt mà giữa chúng bằng cách sử dụng trục gần nhất.

Việc chuyển một rotation sang quaternion rất đơn giản.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Chuyển basis sang quaternion, lưu ý rằng scale sẽ bị mất
    var a = Quaternion(transform.basis)
    var b = Quaternion(transform2.basis)
    # Nội suy bằng spherical-linear interpolation (SLERP).
    var c = a.slerp(b,0.5) # tìm điểm giữa a và b
    # Áp dụng ngược lại
    transform.basis = Basis(c)

 .. code-tab:: csharp

    // Chuyển basis sang quaternion, lưu ý rằng scale sẽ bị mất
    var a = new Quaternion(transform.Basis);
    var b = new Quaternion(transform2.Basis);
    // Nội suy bằng spherical-linear interpolation (SLERP).
    var c = a.Slerp(b, 0.5f); // tìm điểm giữa a và b
    // Áp dụng ngược lại
    transform.Basis = new Basis(c);

Tham chiếu kiểu :ref:`class_Quaternion` cung cấp thêm thông tin về kiểu dữ liệu này (nó cũng có thể thực hiện tích lũy transform, biến đổi các điểm, v.v., mặc dù việc này ít được dùng hơn). Nếu bạn nội suy hoặc áp dụng các phép toán cho quaternion nhiều lần, hãy nhớ rằng cuối cùng chúng cần được chuẩn hóa. Nếu không, chúng cũng sẽ gặp lỗi độ chính xác số.

Quaternion rất hữu ích khi thực hiện nội suy camera/path/v.v., vì kết quả sẽ luôn chính xác và mượt mà.

Transform là người bạn của bạn
------------------------------

Với hầu hết người mới bắt đầu, việc làm quen với cách làm việc cùng transform có thể mất một khoảng thời gian. Tuy nhiên, một khi đã quen, bạn sẽ đánh giá cao sự đơn giản và mạnh mẽ của chúng.

Đừng ngần ngại yêu cầu trợ giúp về chủ đề này trong bất kỳ `cộng đồng trực tuyến <https://godotengine.org/community>`_ nào của Godot và khi đã đủ tự tin, hãy giúp đỡ những người khác!

.. _`Wikipedia's page on Gimbal Lock`: https://en.wikipedia.org/wiki/Gimbal_lock
.. _`online communities`: https://godotengine.org/community
