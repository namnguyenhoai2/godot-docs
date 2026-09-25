.. _doc_physics_introduction:

Giới thiệu về vật lý
====================

Trong phát triển game, bạn thường cần biết khi nào hai đối tượng trong game giao nhau hoặc tiếp xúc với nhau. Điều này được gọi là **phát hiện va chạm**. Khi phát hiện va chạm, bạn thường muốn một điều gì đó xảy ra. Điều này được gọi là **phản hồi va chạm**.

Godot cung cấp nhiều loại đối tượng va chạm trong 2D và 3D để thực hiện cả việc phát hiện va chạm lẫn phản hồi va chạm. Việc quyết định nên sử dụng loại nào cho dự án có thể gây khó hiểu. Bạn có thể tránh được các vấn đề và đơn giản hóa quá trình phát triển nếu hiểu cách mỗi loại hoạt động cũng như ưu và nhược điểm của chúng.

Trong hướng dẫn này, bạn sẽ tìm hiểu:

-   Bốn loại đối tượng va chạm của Godot
-   Cách mỗi đối tượng va chạm hoạt động
-   Khi nào và tại sao nên chọn loại này thay vì loại khác

.. note:: Các ví dụ trong tài liệu này sẽ sử dụng các đối tượng 2D. Mọi đối tượng vật lý 2D và hình dạng va chạm đều có phiên bản tương đương trực tiếp trong 3D và trong hầu hết trường hợp, chúng hoạt động gần như giống nhau.

.. warning:: Vật lý trong Godot, bất kể physics engine nào, **không** mang tính tất định, bản chất của tính tất định trong physics engine rất phức tạp và liên quan đến nhiều yếu tố; điều này có nghĩa là không đảm bảo vật lý sẽ hoạt động theo cùng một cách trong những tình huống có vẻ giống hệt nhau.

Các đối tượng va chạm
---------------------

Godot cung cấp bốn loại đối tượng va chạm, tất cả đều kế thừa :ref:`CollisionObject2D <class_CollisionObject2D>`. Ba loại cuối được liệt kê bên dưới là các physics body và đồng thời kế thừa :ref:`PhysicsBody2D <class_PhysicsBody2D>`.

- :ref:`Area2D <class_Area2D>`
    Các node ``Area2D`` cung cấp khả năng **phát hiện** và **tác động**. Chúng có thể phát hiện khi các đối tượng chồng lấn lên nhau và có thể phát signal khi các body đi vào hoặc rời khỏi. Một ``Area2D`` cũng có thể được dùng để ghi đè các thuộc tính vật lý, chẳng hạn như gravity hoặc damping, trong một khu vực xác định.

- :ref:`StaticBody2D <class_StaticBody2D>`
    Static body là body không được physics engine di chuyển. Nó tham gia vào quá trình phát hiện va chạm nhưng không di chuyển để phản ứng với va chạm. Chúng thường được dùng cho các đối tượng thuộc môi trường hoặc không cần có hành vi động.

- :ref:`RigidBody2D <class_RigidBody2D>`
    Đây là node triển khai vật lý 2D mô phỏng. Bạn không điều khiển trực tiếp một ``RigidBody2D``, mà thay vào đó áp dụng các lực lên nó (gravity, impulse, v.v.), rồi physics engine tính toán chuyển động tạo ra.
    :ref:`Đọc thêm về cách sử dụng rigid body. <doc_rigid_body>`

- :ref:`CharacterBody2D <class_CharacterBody2D>`
    Một body cung cấp khả năng phát hiện va chạm nhưng không có vật lý. Mọi chuyển động và phản hồi va chạm đều phải được triển khai trong code.

Physics material
~~~~~~~~~~~~~~~~

Static body và rigid body có thể được cấu hình để sử dụng :ref:`PhysicsMaterial <class_PhysicsMaterial>`. Điều này cho phép điều chỉnh friction và bounce của một đối tượng, đồng thời đặt đối tượng có absorbent và/hoặc rough hay không.

Collision shapes
~~~~~~~~~~~~~~~~

Một physics body có thể chứa bất kỳ số lượng đối tượng :ref:`Shape2D <class_Shape2D>` nào dưới dạng node con. Các shape này được dùng để xác định giới hạn va chạm của đối tượng và phát hiện tiếp xúc với các đối tượng khác.

.. note:: Để phát hiện va chạm, đối tượng phải được gán ít nhất một ``Shape2D``.

Cách phổ biến nhất để gán một shape là thêm một :ref:`CollisionShape2D <class_CollisionShape2D>` hoặc :ref:`CollisionPolygon2D <class_CollisionPolygon2D>` làm node con của đối tượng. Các node này cho phép bạn vẽ trực tiếp shape trong không gian làm việc của editor.

.. important:: Hãy cẩn thận và không bao giờ scale collision shape trong editor. Thuộc tính "Scale" trong Inspector phải luôn là ``(1, 1)``. Khi thay đổi kích thước collision shape, bạn luôn nên sử dụng các nút điều chỉnh kích thước, **không phải** các ``Node2D`` nút điều chỉnh scale. Scale một shape có thể dẫn đến hành vi va chạm không mong muốn.

.. image:: img/player_coll_shape.webp

Physics process callback
~~~~~~~~~~~~~~~~~~~~~~~~

Physics engine chạy với tần suất cố định (mặc định là 60 lần lặp mỗi giây). Tần suất này thường khác với frame rate, vốn dao động tùy theo nội dung được render và tài nguyên khả dụng.

Điều quan trọng là mọi code liên quan đến vật lý đều chạy ở tần suất cố định này. Vì vậy, Godot phân biệt :ref:`giữa xử lý vật lý và xử lý idle <doc_idle_and_physics_processing>`. Code chạy ở mỗi frame được gọi là idle processing, còn code chạy ở mỗi physics tick được gọi là physics processing. Godot cung cấp hai callback khác nhau, mỗi callback dành cho một trong hai tần suất xử lý đó.

Physics callback, :ref:`Node._physics_process() <class_Node_private_method__physics_process>`, được gọi trước mỗi physics step. Mọi code cần truy cập các thuộc tính của body nên được chạy tại đây. Phương thức này sẽ nhận một tham số ``delta``, là một số dấu phẩy động bằng khoảng thời gian đã trôi qua tính bằng *giây* kể từ step trước. Khi sử dụng tần suất cập nhật vật lý mặc định là 60 Hz, giá trị này thường bằng ``0.01666...`` (nhưng không phải lúc nào cũng vậy, xem bên dưới).

.. note::

    Bạn nên luôn sử dụng tham số ``delta`` khi phù hợp trong các phép tính vật lý, để game hoạt động chính xác nếu bạn thay đổi tần suất cập nhật vật lý hoặc thiết bị của người chơi không theo kịp.

.. _doc_physics_introduction_collision_layers_and_masks:

Collision layers và masks
~~~~~~~~~~~~~~~~~~~~~~~~~

Một trong những tính năng va chạm mạnh mẽ nhất nhưng thường bị hiểu sai là hệ thống collision layer. Hệ thống này cho phép bạn xây dựng các tương tác phức tạp giữa nhiều loại đối tượng. Các khái niệm chính là **layer** và **mask**. Mỗi ``CollisionObject2D`` có 32 physics layer khác nhau mà nó có thể tương tác.

Hãy lần lượt xem xét từng thuộc tính:

- collision_layer
    Thuộc tính này mô tả các layer mà đối tượng **nằm trên**. Theo mặc định, tất cả body đều nằm trên layer ``1``.

- collision_mask
    Thuộc tính này mô tả các layer mà body sẽ **quét** để tìm va chạm. Nếu một đối tượng không nằm trong một trong các layer của mask, body sẽ bỏ qua đối tượng đó. Theo mặc định, tất cả body đều quét layer ``1``.

Các thuộc tính này có thể được cấu hình bằng code hoặc chỉnh sửa trong Inspector.

Việc theo dõi mục đích sử dụng của từng layer có thể khó khăn, vì vậy bạn có thể thấy hữu ích khi đặt tên cho các layer đang sử dụng. Có thể đặt tên trong **Project Settings > Layer Names > 2D Physics**.

.. image:: img/physics_layer_names.webp

Ví dụ về GUI
^^^^^^^^^^^^

Trong game của bạn có bốn loại node: Walls, Player, Enemy và Coin. Cả Player và Enemy đều phải va chạm với Walls. Node Player phải phát hiện va chạm với cả Enemy và Coin, nhưng Enemy và Coin phải bỏ qua nhau.

Bắt đầu bằng cách đặt tên cho các layer 1-4 lần lượt là "walls", "player", "enemies" và "coins", rồi đặt từng loại node vào layer tương ứng bằng thuộc tính "Layer". Sau đó, đặt thuộc tính "Mask" của từng node bằng cách chọn các layer mà node đó cần tương tác. Ví dụ, các thiết lập của Player sẽ như sau:

.. image:: img/player_collision_layers.webp
.. image:: img/player_collision_mask.webp

.. _doc_physics_introduction_collision_layer_code_example:

Ví dụ về code
^^^^^^^^^^^^^

Trong các lệnh gọi hàm, các layer được chỉ định dưới dạng bitmask. Khi một hàm bật tất cả layer theo mặc định, layer mask sẽ được cung cấp dưới dạng ``0xffffffff``. Mã của bạn có thể sử dụng ký hiệu nhị phân, thập lục phân hoặc thập phân cho layer mask, tùy theo sở thích.

Tương đương mã của ví dụ trên, trong đó các layer 1, 3 và 4 được bật, sẽ như sau:

::

    # Example: Setting mask value for enabling layers 1, 3 and 4

    # Binary - set the bit corresponding to the layers you want to enable (1, 3, and 4) to 1, set all other bits to 0.
    # Note: Layer 32 is the first bit, layer 1 is the last. The mask for layers 4, 3 and 1 is therefore:
    0b00000000_00000000_00000000_00001101
    # (This can be shortened to 0b1101)

    # Hexadecimal equivalent (1101 binary converted to hexadecimal).
    0x000d
    # (This value can be shortened to 0xd.)

    # Decimal - Add the results of 2 to the power of (layer to be enabled - 1).
    # (2^(1-1)) + (2^(3-1)) + (2^(4-1)) = 1 + 4 + 8 = 13
    #
    # We can use the `<<` operator to shift the bit to the left by the layer number we want to enable.
    # This is a faster way to multiply by powers of 2 than `pow()`.
    # Additionally, we use the `|` (binary OR) operator to combine the results of each layer.
    # This ensures we don't add the same layer multiple times, which would behave incorrectly.
    (1 << 1 - 1) | (1 << 3 - 1) | (1 << 4 - 1)

    # The above can alternatively be written as:
    # pow(2, 1 - 1) + pow(2, 3 - 1) + pow(2, 4 - 1)

Bạn cũng có thể đặt các bit độc lập bằng cách gọi ``set_collision_layer_value(layer_number, value)`` hoặc ``set_collision_mask_value(layer_number, value)`` trên bất kỳ :ref:`CollisionObject2D <class_CollisionObject2D>` nào như sau:

::

    # Example: Setting mask value to enable layers 1, 3, and 4.

    var collider: CollisionObject2D = $CollisionObject2D  # Any given collider.
    collider.set_collision_mask_value(1, true)
    collider.set_collision_mask_value(3, true)
    collider.set_collision_mask_value(4, true)

Có thể sử dụng các export annotation để export bitmask trong editor bằng GUI thân thiện với người dùng:

::

    @export_flags_2d_physics var layers_2d_physics

Các export annotation bổ sung khả dụng cho render layer và navigation layer, trong cả 2D và 3D. Xem :ref:`doc_gdscript_exports_exporting_bit_flags`.

Area2D
------

Các Area node cung cấp khả năng **phát hiện** và **tác động**. Chúng có thể phát hiện khi các object chồng lấp nhau và phát signal khi các body đi vào hoặc rời khỏi. Area cũng có thể được dùng để ghi đè các thuộc tính vật lý, chẳng hạn như gravity hoặc damping, trong một khu vực xác định.

Có ba cách sử dụng chính cho :ref:`Area2D <class_Area2D>`:

- Ghi đè các tham số vật lý (chẳng hạn như gravity) trong một khu vực nhất định.

- Phát hiện khi các body khác đi vào hoặc rời khỏi một khu vực, hoặc những body nào hiện đang ở trong một khu vực.

- Kiểm tra các area khác để tìm chồng lấp.

Theo mặc định, area cũng nhận input từ chuột và màn hình cảm ứng.

StaticBody2D
------------

Static body là body không được physics engine di chuyển. Nó tham gia vào quá trình phát hiện va chạm, nhưng không di chuyển để phản ứng với va chạm. Tuy nhiên, nó có thể truyền chuyển động hoặc chuyển động xoay cho body va chạm **như thể** nó đang di chuyển, bằng cách sử dụng các thuộc tính ``constant_linear_velocity`` và ``constant_angular_velocity`` của nó.

Các node ``StaticBody2D`` thường được dùng nhất cho những object thuộc về môi trường hoặc không cần có hành vi động.

Các trường hợp sử dụng ``StaticBody2D``:

-   Platform (bao gồm cả moving platform)
-   Băng chuyền
-   Tường và các chướng ngại vật khác

RigidBody2D
-----------

Đây là node triển khai physics 2D mô phỏng. Bạn không điều khiển một
:ref:`RigidBody2D <class_RigidBody2D>` trực tiếp. Thay vào đó, bạn tác dụng lực lên nó và physics engine sẽ tính toán chuyển động kết quả, bao gồm va chạm với các body khác và phản ứng va chạm, chẳng hạn như nảy, xoay, v.v.

Bạn có thể thay đổi hành vi của rigid body thông qua các thuộc tính như "Mass", "Friction" hoặc "Bounce", có thể được thiết lập trong Inspector.

Hành vi của body cũng chịu ảnh hưởng bởi các thuộc tính của world, được thiết lập trong **Project Settings > Physics**, hoặc bằng cách đưa vào một :ref:`Area2D <class_Area2D>` đang ghi đè các thuộc tính vật lý toàn cục.

Khi một rigid body đứng yên và không di chuyển trong một khoảng thời gian, nó sẽ chuyển sang trạng thái ngủ. Body đang ngủ hoạt động như một static body và các lực tác dụng lên nó không được physics engine tính toán. Body sẽ thức dậy khi có lực được tác dụng, do va chạm hoặc thông qua code.

Sử dụng RigidBody2D
~~~~~~~~~~~~~~~~~~~

Một trong những lợi ích của việc sử dụng rigid body là bạn có thể có được rất nhiều hành vi "miễn phí" mà không cần viết code. Ví dụ, nếu bạn tạo một game kiểu "Angry Birds" với các khối rơi xuống, bạn chỉ cần tạo các RigidBody2D và điều chỉnh thuộc tính của chúng. Việc xếp chồng, rơi và nảy sẽ được physics engine tự động tính toán.

Tuy nhiên, nếu bạn muốn kiểm soát body ở một mức độ nào đó, hãy cẩn thận - việc thay đổi ``position``, ``linear_velocity`` hoặc các thuộc tính vật lý khác của rigid body có thể dẫn đến hành vi không mong đợi. Nếu cần thay đổi bất kỳ thuộc tính nào liên quan đến vật lý, bạn nên sử dụng callback :ref:`_integrate_forces() <class_RigidBody2D_private_method__integrate_forces>` thay vì ``_physics_process()``. Trong callback này, bạn có quyền truy cập vào :ref:`PhysicsDirectBodyState2D <class_PhysicsDirectBodyState2D>` của body, cho phép thay đổi các thuộc tính một cách an toàn và đồng bộ chúng với physics engine.

Ví dụ, sau đây là code cho một phi thuyền kiểu "Asteroids":

.. tabs::
 .. code-tab:: gdscript GDScript

    extends RigidBody2D

    var thrust = Vector2(0, -250)
    var torque = 20000

    func _integrate_forces(state):
        if Input.is_action_pressed("ui_up"):
            state.apply_force(thrust.rotated(rotation))
        else:
            state.apply_force(Vector2())
        var rotation_direction = 0
        if Input.is_action_pressed("ui_right"):
            rotation_direction += 1
        if Input.is_action_pressed("ui_left"):
            rotation_direction -= 1
        state.apply_torque(rotation_direction * torque)

 .. code-tab:: csharp

    using Godot;

    public partial class Spaceship : RigidBody2D
    {
        private Vector2 _thrust = new Vector2(0, -250);
        private float _torque = 20000;

        public override void _IntegrateForces(PhysicsDirectBodyState2D state)
        {
            if (Input.IsActionPressed("ui_up"))
            {
                state.ApplyForce(_thrust.Rotated(Rotation));
            }
            else
            {
                state.ApplyForce(new Vector2());
            }

            var rotationDir = 0;
            if (Input.IsActionPressed("ui_right"))
            {
                rotationDir += 1;
            }
            if (Input.IsActionPressed("ui_left"))
            {
                rotationDir -= 1;
            }
            state.ApplyTorque(rotationDir * _torque);
        }
    }

Lưu ý rằng chúng ta không thiết lập trực tiếp các thuộc tính ``linear_velocity`` hoặc ``angular_velocity``, mà thay vào đó tác dụng các lực (``thrust`` và ``torque``) lên body và để physics engine tính toán chuyển động kết quả.

.. note:: Khi một rigid body chuyển sang trạng thái ngủ, hàm ``_integrate_forces()`` sẽ không được gọi. Để ghi đè hành vi này, bạn cần giữ cho body luôn thức bằng cách tạo va chạm, tác dụng lực lên nó hoặc tắt thuộc tính :ref:`can_sleep <class_RigidBody2D_property_can_sleep>`. Hãy lưu ý rằng điều này có thể ảnh hưởng tiêu cực đến hiệu năng.

Báo cáo tiếp xúc
~~~~~~~~~~~~~~~~

Theo mặc định, rigid body không theo dõi các tiếp xúc, vì việc này có thể yêu cầu một lượng bộ nhớ rất lớn nếu có nhiều body trong scene. Để bật tính năng báo cáo tiếp xúc, hãy đặt thuộc tính :ref:`max_contacts_reported <class_RigidBody2D_property_max_contacts_reported>` thành một giá trị khác không. Sau đó, có thể lấy các tiếp xúc thông qua
:ref:`PhysicsDirectBodyState2D.get_contact_count() <class_PhysicsDirectBodyState2D_method_get_contact_count>` và các hàm liên quan.

Có thể bật tính năng theo dõi tiếp xúc thông qua signal bằng thuộc tính :ref:`contact_monitor <class_RigidBody2D_property_contact_monitor>`. Xem :ref:`RigidBody2D <class_RigidBody2D>` để biết danh sách các signal khả dụng.

CharacterBody2D
---------------

Các body :ref:`CharacterBody2D <class_CharacterBody2D>` phát hiện va chạm với các body khác, nhưng không chịu ảnh hưởng của các thuộc tính vật lý như gravity hoặc friction. Thay vào đó, chúng phải được người dùng điều khiển thông qua code. Physics engine sẽ không di chuyển character body.

Khi di chuyển character body, bạn không nên thiết lập trực tiếp ``position`` của nó. Thay vào đó, hãy sử dụng các phương thức ``move_and_collide()`` hoặc ``move_and_slide()``. Các phương thức này di chuyển body dọc theo một vector nhất định và body sẽ dừng ngay lập tức nếu phát hiện va chạm với một body khác. Sau khi body va chạm, mọi phản ứng va chạm phải được lập trình thủ công.

Phản ứng va chạm của character
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau một va chạm, bạn có thể muốn body nảy lên, trượt dọc theo tường hoặc thay đổi các thuộc tính của object mà nó va phải. Cách xử lý phản ứng va chạm phụ thuộc vào phương thức bạn đã dùng để di chuyển CharacterBody2D.

:ref:`move_and_collide <class_PhysicsBody2D_method_move_and_collide>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Khi sử dụng ``move_and_collide()``, hàm sẽ trả về một
object :ref:`KinematicCollision2D <class_KinematicCollision2D>`, chứa thông tin về va chạm và body va chạm. Bạn có thể sử dụng thông tin này để xác định phản ứng.

Ví dụ, nếu bạn muốn tìm điểm trong không gian nơi xảy ra va chạm:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends PhysicsBody2D

    var velocity = Vector2(250, 250)

    func _physics_process(delta):
        var collision_info = move_and_collide(velocity * delta)
        if collision_info:
            var collision_point = collision_info.get_position()

 .. code-tab:: csharp

    using Godot;

    public partial class Body : PhysicsBody2D
    {
        private Vector2 _velocity = new Vector2(250, 250);

        public override void _PhysicsProcess(double delta)
        {
            var collisionInfo = MoveAndCollide(_velocity * (float)delta);
            if (collisionInfo != null)
            {
                var collisionPoint = collisionInfo.GetPosition();
            }
        }
    }

Hoặc để nảy khỏi object va chạm:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends PhysicsBody2D

    var velocity = Vector2(250, 250)

    func _physics_process(delta):
        var collision_info = move_and_collide(velocity * delta)
        if collision_info:
            velocity = velocity.bounce(collision_info.get_normal())

 .. code-tab:: csharp

    using Godot;

    public partial class Body : PhysicsBody2D
    {
        private Vector2 _velocity = new Vector2(250, 250);

        public override void _PhysicsProcess(double delta)
        {
            var collisionInfo = MoveAndCollide(_velocity * (float)delta);
            if (collisionInfo != null)
            {
                _velocity = _velocity.Bounce(collisionInfo.GetNormal());
            }
        }
    }

:ref:`move_and_slide <class_CharacterBody2D_method_move_and_slide>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Trượt là một phản ứng va chạm phổ biến; hãy hình dung một player di chuyển dọc theo các bức tường trong game nhìn từ trên xuống hoặc chạy lên xuống các con dốc trong game platformer. Mặc dù bạn có thể tự lập trình phản ứng này sau khi sử dụng ``move_and_collide()``, ``move_and_slide()`` cung cấp một cách thuận tiện để triển khai chuyển động trượt mà không cần viết nhiều code.

.. warning:: ``move_and_slide()`` tự động bao gồm timestep trong phép tính, vì vậy bạn **không** nên nhân vector vận tốc với ``delta``. Điều này **không** áp dụng cho ``gravity`` vì đây là gia tốc và phụ thuộc vào thời gian, nên cần được nhân với ``delta``.

Ví dụ: sử dụng đoạn mã sau để tạo một nhân vật có thể đi trên mặt đất (bao gồm cả các mặt dốc) và nhảy khi đang đứng trên mặt đất:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    var run_speed = 350
    var jump_speed = -1000
    var gravity = 2500

    func get_input():
        velocity.x = 0
        var right = Input.is_action_pressed('ui_right')
        var left = Input.is_action_pressed('ui_left')
        var jump = Input.is_action_just_pressed('ui_select')

        if is_on_floor() and jump:
            velocity.y = jump_speed
        if right:
            velocity.x += run_speed
        if left:
            velocity.x -= run_speed

    func _physics_process(delta):
        velocity.y += gravity * delta
        get_input()
        move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class Body : CharacterBody2D
    {
        private float _runSpeed = 350;
        private float _jumpSpeed = -1000;
        private float _gravity = 2500;

        private void GetInput()
        {
            var velocity = Velocity;
            velocity.X = 0;

            var right = Input.IsActionPressed("ui_right");
            var left = Input.IsActionPressed("ui_left");
            var jump = Input.IsActionPressed("ui_select");

            if (IsOnFloor() && jump)
            {
                velocity.Y = _jumpSpeed;
            }
            if (right)
            {
                velocity.X += _runSpeed;
            }
            if (left)
            {
                velocity.X -= _runSpeed;
            }

            Velocity = velocity;
        }

        public override void _PhysicsProcess(double delta)
        {
            var velocity = Velocity;
            velocity.Y += _gravity * (float)delta;
            Velocity = velocity;
            GetInput();
            MoveAndSlide();
        }
    }


Xem :ref:`doc_kinematic_character_2d` để biết thêm chi tiết về cách sử dụng ``move_and_slide()``, bao gồm một dự án demo với đoạn mã chi tiết.
