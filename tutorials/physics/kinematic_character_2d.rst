.. _doc_kinematic_character_2d:

Nhân vật động học (2D)
======================

Giới thiệu
~~~~~~~~~~

Đúng vậy, cái tên nghe khá lạ. "Nhân vật động học". Đó là gì? Lý do có cái tên này là khi các physics engine ra đời, chúng được gọi là các engine "Dynamics" (vì chủ yếu xử lý phản hồi va chạm). Đã có nhiều nỗ lực tạo character controller bằng các dynamics engine, nhưng việc đó không dễ như vẻ ngoài. Godot có một trong những triển khai dynamic character controller tốt nhất mà bạn có thể tìm thấy (như trong bản demo 2d/platformer), nhưng để sử dụng nó cần có trình độ đáng kể về physics engine và hiểu biết về vật lý (hoặc rất nhiều kiên nhẫn với việc thử và sai).

Một số physics engine, chẳng hạn như Havok, dường như tin chắc rằng dynamic character controller là lựa chọn tốt nhất, trong khi các engine khác (PhysX) lại muốn quảng bá kinematic controller hơn.

Vậy, sự khác biệt là gì?

-  Một **dynamic character controller** sử dụng một rigid body với tensor quán tính vô hạn. Đây là một rigid body không thể xoay. Physics engine luôn cho phép các đối tượng di chuyển và va chạm, sau đó giải quyết tất cả các va chạm của chúng cùng nhau. Điều này giúp dynamic character controller có thể tương tác liền mạch với các đối tượng vật lý khác, như trong bản demo platformer. Tuy nhiên, những tương tác này không phải lúc nào cũng có thể dự đoán. Việc giải quyết va chạm có thể mất hơn một frame, vì vậy một vài va chạm có vẻ như làm đối tượng lệch đi một chút. Những vấn đề đó có thể được khắc phục, nhưng cần một mức độ kỹ năng nhất định.
-  Một **kinematic character controller** được giả định là luôn bắt đầu ở trạng thái không va chạm và luôn di chuyển đến một trạng thái không va chạm. Nếu bắt đầu ở trạng thái đang va chạm, nó sẽ cố tự giải phóng như rigid body, nhưng đây là ngoại lệ chứ không phải quy tắc. Điều này khiến việc điều khiển và chuyển động của chúng dễ dự đoán hơn nhiều và dễ lập trình hơn. Tuy nhiên, nhược điểm là chúng không thể trực tiếp tương tác với các đối tượng vật lý khác, trừ khi được thực hiện thủ công trong code.

Bài hướng dẫn ngắn này tập trung vào kinematic character controller. Nó sử dụng cách xử lý va chạm kiểu cũ, không nhất thiết đơn giản hơn ở bên dưới, nhưng được che giấu kỹ và cung cấp dưới dạng API.

Physics process
~~~~~~~~~~~~~~~

Để quản lý logic của một kinematic body hoặc character, bạn luôn nên sử dụng :ref:`physics process <doc_idle_and_physics_processing>`, vì nó được gọi trước physics step và quá trình thực thi của nó đồng bộ với physics server; ngoài ra, nó luôn được gọi với cùng số lần mỗi giây. Điều này giúp việc tính toán vật lý và chuyển động hoạt động dễ dự đoán hơn so với việc sử dụng regular process, vốn có thể xuất hiện các đợt tăng đột biến hoặc mất độ chính xác nếu frame rate quá cao hoặc quá thấp.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    func _physics_process(delta):
        pass

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        public override void _PhysicsProcess(double delta)
        {
        }
    }


Thiết lập scene
~~~~~~~~~~~~~~~

Để có thứ gì đó dùng thử, đây là scene (từ bài hướng dẫn tilemap): `kinematic_character_2d_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/kinematic_character_2d_starter.zip>`_. Chúng ta sẽ tạo một scene mới cho character. Sử dụng sprite robot và tạo một scene như sau:

.. image:: img/kbscene.webp

Bạn sẽ nhận thấy có một biểu tượng cảnh báo bên cạnh node CollisionShape2D; đó là vì chúng ta chưa xác định shape cho nó. Hãy tạo một CircleShape2D mới trong thuộc tính shape của CollisionShape2D. Nhấp vào <CircleShape2D> để chuyển đến các tùy chọn của nó, rồi đặt radius thành 30:

.. image:: img/kbradius.webp

**Lưu ý: Như đã đề cập trước đó trong bài hướng dẫn physics, physics engine không thể xử lý scale trên hầu hết các loại shape (chỉ collision polygon, plane và segment hoạt động được), vì vậy hãy luôn thay đổi các tham số (chẳng hạn như radius) của shape thay vì scale nó. Điều tương tự cũng đúng với bản thân kinematic/rigid/static body, vì scale của chúng ảnh hưởng đến scale của shape.**

Bây giờ, hãy tạo một script cho character; script được dùng làm ví dụ ở trên sẽ phù hợp để làm cơ sở.

Cuối cùng, hãy instance scene character đó trong tilemap và đặt map scene làm scene chính để nó chạy khi nhấn play.

.. image:: img/kbinstance.webp

Di chuyển kinematic character
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quay lại scene character và mở script; điều kỳ diệu bắt đầu từ bây giờ! Kinematic body mặc định sẽ không làm gì, nhưng nó có một function hữu ích tên là ``CharacterBody2D.move_and_collide()``. Function này nhận một :ref:`Vector2 <class_Vector2>` làm đối số và cố áp dụng chuyển động đó lên kinematic body. Nếu xảy ra va chạm, nó dừng lại ngay tại thời điểm va chạm.

Vậy hãy di chuyển sprite của chúng ta xuống dưới cho đến khi chạm sàn:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    func _physics_process(delta):
        move_and_collide(Vector2(0, 1)) # Di chuyển xuống 1 pixel mỗi physics frame

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        public override void _PhysicsProcess(double delta)
        {
            // Di chuyển xuống 1 pixel mỗi physics frame
            MoveAndCollide(new Vector2(0, 1));
        }
    }

Kết quả là character sẽ di chuyển, nhưng dừng lại ngay khi chạm sàn. Khá hay, phải không?

Bước tiếp theo là thêm gravity vào, để nó hoạt động giống character thông thường trong game hơn một chút:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    const GRAVITY = 200.0

    func _physics_process(delta):
        velocity.y += delta * GRAVITY

        var motion = velocity * delta
        move_and_collide(motion)

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        private const float Gravity = 200.0f;

        public override void _PhysicsProcess(double delta)
        {
            var velocity = Velocity;
            velocity.Y += (float)delta * Gravity;
            Velocity = velocity;

            var motion = velocity * (float)delta;
            MoveAndCollide(motion);
        }
    }

Bây giờ character rơi một cách mượt mà. Hãy cho nó đi sang hai bên, trái và phải khi nhấn các phím điều hướng. Hãy nhớ rằng các giá trị được sử dụng (ít nhất là đối với tốc độ) là pixel/giây.

Điều này bổ sung hỗ trợ cơ bản cho việc đi bộ khi nhấn trái và phải:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends CharacterBody2D

    const GRAVITY = 200.0
    const WALK_SPEED = 200

    func _physics_process(delta):
        velocity.y += delta * GRAVITY

        if Input.is_action_pressed("ui_left"):
            velocity.x = -WALK_SPEED
        elif Input.is_action_pressed("ui_right"):
            velocity.x =  WALK_SPEED
        else:
            velocity.x = 0

        # "move_and_slide" đã tính đến delta time.
        move_and_slide()

 .. code-tab:: csharp

    using Godot;

    public partial class MyCharacterBody2D : CharacterBody2D
    {
        private const float Gravity = 200.0f;
        private const int WalkSpeed = 200;

        public override void _PhysicsProcess(double delta)
        {
            var velocity = Velocity;

            velocity.Y += (float)delta * Gravity;

            if (Input.IsActionPressed("ui_left"))
            {
                velocity.X = -WalkSpeed;
            }
            else if (Input.IsActionPressed("ui_right"))
            {
                velocity.X = WalkSpeed;
            }
            else
            {
                velocity.X = 0;
            }

            Velocity = velocity;

            // "MoveAndSlide" đã tính đến delta time.
            MoveAndSlide();
        }
    }

Hãy thử xem.

Đây là điểm khởi đầu tốt cho một platformer. Bạn có thể tìm thấy một bản demo hoàn chỉnh hơn trong file zip demo được phân phối cùng engine hoặc tại https://github.com/godotengine/godot-demo-projects/tree/master/2d/kinematic_character.

.. _`kinematic_character_2d_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/kinematic_character_2d_starter.zip
