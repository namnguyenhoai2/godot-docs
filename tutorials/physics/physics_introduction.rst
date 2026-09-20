.. _doc_physics_introduction:

Giới thiệu về Physics
=====================

Trong phát triển game, bạn thường cần biết khi nào hai đối tượng trong game giao nhau hoặc tiếp xúc với nhau. Điều này được gọi là **collision detection**. Khi phát hiện va chạm, bạn thường muốn một điều gì đó xảy ra. Điều này được gọi là **collision response**.

Godot cung cấp một số collision object trong 2D và 3D để hỗ trợ cả collision detection và collision response. Việc quyết định nên dùng loại nào cho project của bạn có thể gây bối rối. Bạn có thể tránh được các vấn đề và đơn giản hóa quá trình phát triển nếu hiểu cách từng loại hoạt động cũng như ưu và nhược điểm của chúng.

Trong hướng dẫn này, bạn sẽ học:

-   Bốn loại collision object của Godot - Cách từng collision object hoạt động - Khi nào và tại sao nên chọn loại này thay vì loại khác

.. note:: This document's examples will use 2D objects. Every 2D physics object
          và mỗi collision shape đều có một đối tượng tương đương trực tiếp trong 3D, và trong hầu hết trường hợp chúng hoạt động gần như giống nhau.

.. warning:: Physics in Godot, regardless of physics engine, is **not** deterministic,
             bản chất của tính tất định trong physics engine rất phức tạp và liên quan đến nhiều yếu tố, điều này có nghĩa là physics không được đảm bảo sẽ chạy theo cùng một cách trong những tình huống có vẻ giống hệt nhau.

Collision objects
-----------------

Godot cung cấp bốn loại collision object, tất cả đều kế thừa :ref:`CollisionObject2D <class_CollisionObject2D>`. Ba loại cuối được liệt kê dưới đây là physics body và đồng thời kế thừa :ref:`PhysicsBody2D <class_PhysicsBody2D>`.

- Các node :ref:`Area2D <class_Area2D>` ``Area2D`` cung cấp khả năng **phát hiện** và **tác động**. Chúng có thể phát hiện khi các object chồng lấn lên nhau và phát signal khi các body đi vào hoặc rời khỏi. Một ``Area2D`` cũng có thể được dùng để ghi đè các thuộc tính physics, chẳng hạn như gravity hoặc damping, trong một khu vực xác định.

- :ref:`StaticBody2D <class_StaticBody2D>` Static body là body không được physics engine di chuyển. Nó tham gia vào collision detection nhưng không di chuyển để phản ứng với va chạm. Chúng thường được dùng cho các object thuộc môi trường hoặc không cần có hành vi động.

- :ref:`RigidBody2D <class_RigidBody2D>` Đây là node triển khai physics 2D được mô phỏng. Bạn không điều khiển trực tiếp một ``RigidBody2D``, mà thay vào đó áp dụng lực lên nó (gravity, impulse, v.v.), rồi physics engine sẽ tính toán chuyển động kết quả.
    :ref:`Read more about using rigid bodies. <doc_rigid_body>`

- :ref:`CharacterBody2D <class_CharacterBody2D>` Một body cung cấp collision detection nhưng không có physics. Mọi chuyển động và collision response đều phải được triển khai trong code.

Physics material
~~~~~~~~~~~~~~~~

Static body và rigid body có thể được cấu hình để sử dụng một :ref:`PhysicsMaterial <class_PhysicsMaterial>`. Điều này cho phép điều chỉnh friction và bounce của một object, đồng thời thiết lập xem nó có khả năng hấp thụ và/hoặc thô ráp hay không.

Collision shapes
~~~~~~~~~~~~~~~~

Một physics body có thể chứa bất kỳ số lượng object :ref:`Shape2D <class_Shape2D>` nào làm node con. Các shape này được dùng để xác định giới hạn va chạm của object và phát hiện tiếp xúc với các object khác.

.. note:: In order to detect collisions, at least one ``Shape2D`` must be
          được gán cho object.

Cách phổ biến nhất để gán shape là thêm một :ref:`CollisionShape2D <class_CollisionShape2D>` hoặc :ref:`CollisionPolygon2D <class_CollisionPolygon2D>` làm node con của object. Các node này cho phép bạn vẽ shape trực tiếp trong workspace của editor.

.. important:: Be careful to never scale your collision shapes in the editor.
                Thuộc tính "Scale" trong Inspector nên giữ nguyên ``(1, 1)``. Khi thay đổi kích thước của collision shape, bạn luôn nên sử dụng các tay nắm điều chỉnh kích thước, **không phải** các tay nắm scale của ``Node2D``. Việc scale một shape có thể dẫn đến hành vi va chạm không mong muốn.

.. image:: img/player_coll_shape.webp

Physics process callback
~~~~~~~~~~~~~~~~~~~~~~~~

Physics engine chạy ở một tần suất cố định (mặc định là 60 lần lặp mỗi giây). Tần suất này thường khác với frame rate, vốn dao động tùy theo nội dung được render và tài nguyên khả dụng.

Điều quan trọng là mọi code liên quan đến physics phải chạy ở tần suất cố định này. Vì vậy, Godot phân biệt :ref:`between physics and idle processing <doc_idle_and_physics_processing>`. Code chạy ở mỗi frame được gọi là idle processing, còn code chạy ở mỗi physics tick được gọi là physics processing. Godot cung cấp hai callback khác nhau, mỗi callback tương ứng với một trong hai tần suất xử lý đó.

Physics callback, :ref:`Node._physics_process() <class_Node_private_method__physics_process>`, được gọi trước mỗi physics step. Mọi code cần truy cập các thuộc tính của body nên được chạy tại đây. Method này sẽ nhận một tham số ``delta``, là một số dấu phẩy động bằng khoảng thời gian đã trôi qua tính bằng *giây* kể từ step trước. Khi sử dụng physics update rate mặc định là 60 Hz, giá trị này thường sẽ bằng ``0.01666...`` (nhưng không phải lúc nào cũng vậy, xem bên dưới).

.. note::

    Bạn nên luôn sử dụng tham số ``delta`` khi phù hợp trong các phép tính physics, để game hoạt động chính xác nếu bạn thay đổi physics update rate hoặc nếu thiết bị của người chơi không thể theo kịp.

.. _doc_physics_introduction_collision_layers_and_masks:

Collision layers và masks
~~~~~~~~~~~~~~~~~~~~~~~~~

Một trong những tính năng collision mạnh mẽ nhất nhưng thường bị hiểu sai là hệ thống collision layer. Hệ thống này cho phép bạn xây dựng các tương tác phức tạp giữa nhiều loại object. Các khái niệm chính là **layer** và **mask**. Mỗi ``CollisionObject2D`` có 32 physics layer khác nhau mà nó có thể tương tác.

Hãy lần lượt xem từng thuộc tính:

- collision_layer Thuộc tính này mô tả các layer mà object xuất hiện **trong** đó. Theo mặc định, tất cả body đều nằm trên layer ``1``.

- collision_mask Thuộc tính này mô tả các layer mà body sẽ **quét** để tìm va chạm. Nếu một object không nằm trong một trong các layer của mask, body sẽ bỏ qua nó. Theo mặc định, tất cả body đều quét layer ``1``.

Các thuộc tính này có thể được cấu hình bằng code hoặc chỉnh sửa trong Inspector.

Việc theo dõi mục đích sử dụng của từng layer có thể khó khăn, vì vậy bạn có thể thấy hữu ích khi đặt tên cho các layer đang sử dụng. Có thể đặt tên trong **Project Settings > Layer Names > 2D Physics**.

.. image:: img/physics_layer_names.webp

Ví dụ về GUI
^^^^^^^^^^^^

Bạn có bốn loại node trong game: Walls, Player, Enemy và Coin. Cả Player và Enemy đều phải va chạm với Walls. Node Player phải phát hiện va chạm với cả Enemy và Coin, nhưng Enemy và Coin phải bỏ qua nhau.

Bắt đầu bằng cách đặt tên cho các layer 1-4 lần lượt là "walls", "player", "enemies" và "coins", rồi đặt từng loại node vào layer tương ứng bằng thuộc tính "Layer". Sau đó thiết lập thuộc tính "Mask" của từng node bằng cách chọn các layer mà node đó cần tương tác. Ví dụ, các thiết lập của Player sẽ như sau:

.. image:: img/player_collision_layers.webp
.. image:: img/player_collision_mask.webp

.. _doc_physics_introduction_collision_layer_code_example:

Ví dụ về code
^^^^^^^^^^^^^

Trong các lời gọi function, layer được chỉ định dưới dạng bitmask. Khi một function mặc định bật tất cả layer, layer mask sẽ được cho là ``0xffffffff``. Code của bạn có thể sử dụng ký hiệu nhị phân, thập lục phân hoặc thập phân cho layer mask, tùy theo lựa chọn của bạn.

Phần tương đương bằng code của ví dụ trên, trong đó các layer 1, 3 và 4 được bật, sẽ như sau:

::

    # Ví dụ: Đặt giá trị mask để bật các layer 1, 3 và 4

    # Nhị phân - đặt bit tương ứng với các layer bạn muốn bật (1, 3 và 4) thành 1, đặt tất cả bit còn lại thành 0.
    # Note: Layer 32 is the first bit, layer 1 is the last. The mask for layers 4, 3 and 1 is therefore:
    0b00000000_00000000_00000000_00001101
    # (Có thể rút gọn thành 0b1101)

    # Giá trị tương đương ở hệ thập lục phân (1101 ở hệ nhị phân được chuyển đổi sang hệ thập lục phân).
    0x000d
    # (Có thể rút gọn giá trị này thành 0xd.)

    # Thập phân - Cộng các kết quả của 2 lũy thừa (layer cần bật - 1).
    # (2^(1-1)) + (2^(3-1)) + (2^(4-1)) = 1 + 4 + 8 = 13
    #
    # Chúng ta có thể sử dụng toán tử `<<` để dịch bit sang trái theo số layer mà chúng ta muốn bật.
    # Đây là cách nhân với lũy thừa của 2 nhanh hơn so với `pow()`.
    # Ngoài ra, chúng ta sử dụng toán tử `|` (OR nhị phân) để kết hợp kết quả của từng layer.
    # Điều này đảm bảo chúng ta không cộng cùng một layer nhiều lần, vì việc đó sẽ cho kết quả không chính xác.
    (1 << 1 - 1) | (1 << 3 - 1) | (1 << 4 - 1)

    # Cách viết khác của phần trên là:
    # pow(2, 1 - 1) + pow(2, 3 - 1) + pow(2, 4 - 1)

Bạn cũng có thể thiết lập các bit một cách độc lập bằng cách gọi ``set_collision_layer_value(layer_number, value)`` hoặc ``set_collision_mask_value(layer_number, value)`` trên bất kỳ :ref:`CollisionObject2D <class_CollisionObject2D>` nào như sau:

::

    # Ví dụ: Đặt giá trị mask để bật các layer 1, 3 và 4.

    var collider: CollisionObject2D = $CollisionObject2D  # Bất kỳ collider nào.
    collider.set_collision_mask_value(1, true)
    collider.set_collision_mask_value(3, true)
    collider.set_collision_mask_value(4, true)

Có thể sử dụng export annotation để export bitmask trong editor bằng GUI thân thiện với người dùng:

::

    @export_flags_2d_physics var layers_2d_physics

Có thêm các export annotation cho render layer và navigation layer, trong cả 2D và 3D. Xem :ref:`doc_gdscript_exports_exporting_bit_flags`.

Area2D
------

Area node cung cấp khả năng **phát hiện** và **tác động**. Chúng có thể phát hiện khi các object chồng lấn lên nhau và phát signal khi các body đi vào hoặc rời khỏi. Area cũng có thể được dùng để ghi đè các thuộc tính physics, chẳng hạn như gravity hoặc damping, trong một khu vực xác định.

Có ba cách sử dụng chính cho :ref:`Area2D <class_Area2D>`:

- Ghi đè các tham số physics (chẳng hạn như gravity) trong một khu vực nhất định.

- Phát hiện khi các body khác đi vào hoặc rời khỏi một khu vực, hoặc xác định những body hiện đang ở trong một khu vực.

- Kiểm tra các area khác để phát hiện chồng lấn.

Theo mặc định, area cũng nhận input từ chuột và màn hình cảm ứng.

StaticBody2D
------------

Static body là body không được physics engine di chuyển. Nó tham gia vào collision detection nhưng không di chuyển để phản ứng với va chạm. Tuy nhiên, nó có thể truyền chuyển động hoặc rotation cho một body đang va chạm **như thể** nó đang di chuyển, bằng cách sử dụng các thuộc tính ``constant_linear_velocity`` và ``constant_angular_velocity``.

Các node ``StaticBody2D`` thường được dùng cho những object thuộc môi trường hoặc không cần có hành vi động.

Các trường hợp sử dụng ``StaticBody2D``:

-   Platform (bao gồm cả moving platform) - Băng chuyền - Tường và các chướng ngại vật khác

RigidBody2D
-----------

Đây là node triển khai physics 2D mô phỏng. Bạn không điều khiển một
:ref:`RigidBody2D <class_RigidBody2D>` directly. Instead, you apply forces
đến nó, mà physics engine sẽ tính toán chuyển động kết quả, bao gồm va chạm với các body khác và phản hồi va chạm, chẳng hạn như nảy, xoay, v.v.

Bạn có thể sửa đổi hành vi của rigid body thông qua các thuộc tính như "Mass", "Friction" hoặc "Bounce", có thể được thiết lập trong Inspector.

Hành vi của body cũng chịu ảnh hưởng bởi các thuộc tính của thế giới, được thiết lập trong **Project Settings > Physics**, hoặc bằng cách nhập một :ref:`Area2D <class_Area2D>` đang ghi đè các thuộc tính physics toàn cục.

Khi một rigid body ở trạng thái nghỉ và không di chuyển trong một khoảng thời gian, nó sẽ chuyển sang trạng thái ngủ. Body đang ngủ hoạt động như một static body và các lực tác động lên nó không được physics engine tính toán. Body sẽ thức dậy khi có lực được áp dụng, είτε do va chạm hoặc thông qua code.

Sử dụng RigidBody2D
~~~~~~~~~~~~~~~~~~~

Một trong những lợi ích của việc sử dụng rigid body là bạn có thể có được rất nhiều hành vi "miễn phí" mà không cần viết code. Ví dụ, nếu bạn đang tạo một game theo phong cách "Angry Birds" với các khối rơi xuống, bạn chỉ cần tạo các RigidBody2D và điều chỉnh thuộc tính của chúng. Việc xếp chồng, rơi và nảy sẽ được physics engine tự động tính toán.

Tuy nhiên, nếu bạn muốn kiểm soát body, hãy cẩn thận — việc thay đổi ``position``, ``linear_velocity`` hoặc các thuộc tính physics khác của rigid body có thể dẫn đến hành vi không mong muốn. Nếu cần thay đổi bất kỳ thuộc tính nào liên quan đến physics, bạn nên sử dụng callback :ref:`_integrate_forces() <class_RigidBody2D_private_method__integrate_forces>` thay vì ``_physics_process()``. Trong callback này, bạn có quyền truy cập vào :ref:`PhysicsDirectBodyState2D <class_PhysicsDirectBodyState2D>` của body, cho phép thay đổi các thuộc tính một cách an toàn và đồng bộ hóa chúng với physics engine.

Ví dụ, sau đây là code cho một phi thuyền theo phong cách "Asteroids":

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

Lưu ý rằng chúng ta không thiết lập trực tiếp các thuộc tính ``linear_velocity`` hoặc ``angular_velocity``, mà thay vào đó áp dụng các lực (``thrust`` và ``torque``) lên body và để physics engine tính toán chuyển động kết quả.

.. note:: When a rigid body goes to sleep, the ``_integrate_forces()``
          function sẽ không được gọi. Để ghi đè hành vi này, bạn cần giữ cho body luôn thức bằng cách tạo một va chạm, áp dụng lực lên nó hoặc vô hiệu hóa thuộc tính :ref:`can_sleep <class_RigidBody2D_property_can_sleep>`. Hãy lưu ý rằng điều này có thể ảnh hưởng tiêu cực đến hiệu năng.

Báo cáo tiếp xúc
~~~~~~~~~~~~~~~~

Theo mặc định, rigid body không theo dõi các tiếp xúc, vì việc này có thể yêu cầu một lượng bộ nhớ khổng lồ nếu có nhiều body trong scene. Để bật tính năng báo cáo tiếp xúc, hãy đặt thuộc tính :ref:`max_contacts_reported <class_RigidBody2D_property_max_contacts_reported>` thành một giá trị khác không. Sau đó, bạn có thể lấy các tiếp xúc thông qua
:ref:`PhysicsDirectBodyState2D.get_contact_count() <class_PhysicsDirectBodyState2D_method_get_contact_count>`
và các function liên quan.

Có thể bật tính năng theo dõi tiếp xúc thông qua signal bằng thuộc tính :ref:`contact_monitor <class_RigidBody2D_property_contact_monitor>`. Xem :ref:`RigidBody2D <class_RigidBody2D>` để biết danh sách các signal khả dụng.

CharacterBody2D
---------------

:ref:`CharacterBody2D <class_CharacterBody2D>` bodies detect collisions with
với các body khác, nhưng không chịu ảnh hưởng của các thuộc tính physics như gravity hoặc friction. Thay vào đó, chúng phải được người dùng điều khiển thông qua code. Physics engine sẽ không di chuyển character body.

Khi di chuyển character body, bạn không nên thiết lập trực tiếp ``position`` của nó. Thay vào đó, hãy sử dụng các method ``move_and_collide()`` hoặc ``move_and_slide()``. Các method này di chuyển body theo một vector đã cho và body sẽ dừng ngay lập tức nếu phát hiện va chạm với body khác. Sau khi body đã va chạm, mọi phản hồi va chạm phải được lập trình thủ công.

Phản hồi va chạm của character
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sau một vụ va chạm, bạn có thể muốn body nảy lên, trượt dọc theo tường hoặc thay đổi các thuộc tính của đối tượng mà nó va phải. Cách bạn xử lý phản hồi va chạm phụ thuộc vào method bạn đã sử dụng để di chuyển CharacterBody2D.

:ref:`move_and_collide <class_PhysicsBody2D_method_move_and_collide>`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Khi sử dụng ``move_and_collide()``, function trả về một
:ref:`KinematicCollision2D <class_KinematicCollision2D>` object, which contains
thông tin về va chạm và body va chạm. Bạn có thể sử dụng thông tin này để xác định phản hồi.

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

Hoặc để nảy khỏi đối tượng va chạm:

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

Trượt là một phản hồi va chạm phổ biến; hãy hình dung một người chơi di chuyển dọc theo các bức tường trong game góc nhìn từ trên xuống hoặc chạy lên xuống các sườn dốc trong một platformer. Mặc dù bạn có thể tự viết code cho phản hồi này sau khi sử dụng ``move_and_collide()``, ``move_and_slide()`` cung cấp một cách thuận tiện để triển khai chuyển động trượt mà không cần viết nhiều code.

.. warning:: ``move_and_slide()`` automatically includes the timestep in its
             tính toán, vì vậy bạn **không** nên nhân vector vận tốc với ``delta``. Điều này **không** áp dụng cho ``gravity`` vì đây là một gia tốc phụ thuộc vào thời gian và cần được scale theo ``delta``.

Ví dụ, hãy sử dụng code sau để tạo một character có thể đi bộ trên mặt đất (bao gồm cả các sườn dốc) và nhảy khi đang đứng trên mặt đất:

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


Xem :ref:`doc_kinematic_character_2d` để biết thêm chi tiết về cách sử dụng ``move_and_slide()``, bao gồm một demo project với code chi tiết.
