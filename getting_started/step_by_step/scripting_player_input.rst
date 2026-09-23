.. Intention: only introduce one necessary input method at this point. The
   Inputs section of the docs should provide more guides comparing the various
   tools you have to manage the complexity of user input.

.. _doc_scripting_player_input:

Lắng nghe input của người chơi
==============================

Dựa trên bài học trước, :ref:`doc_scripting_first_script`, hãy cùng xem xét một tính năng quan trọng khác của mọi game: trao quyền điều khiển cho người chơi. Để thêm tính năng này, chúng ta cần sửa đổi code ``sprite_2d.gd``.

.. image:: img/scripting_first_script_moving_with_input.gif

Trong Godot, bạn có hai công cụ chính để xử lý input của người chơi:

1. Các input callback tích hợp sẵn, chủ yếu là ``_unhandled_input()``. Giống như ``_process()``, đây là một hàm ảo tích hợp sẵn được Godot gọi mỗi khi người chơi nhấn một phím. Đây là công cụ bạn nên dùng để phản hồi các sự kiện không xảy ra ở mỗi frame, chẳng hạn như nhấn :kbd:`Space` để nhảy. Để tìm hiểu thêm về input callback, hãy xem :ref:`doc_inputevent`.
2. Singleton ``Input``. Singleton là một object có thể truy cập trên toàn cục. Godot cung cấp quyền truy cập đến một số singleton trong các script. Đây là công cụ phù hợp để kiểm tra input ở mỗi frame.

Ở đây, chúng ta sẽ sử dụng singleton ``Input`` vì cần biết người chơi có muốn xoay hoặc di chuyển ở mỗi frame hay không.

Để xoay, chúng ta nên sử dụng một biến mới: ``direction``. Trong hàm ``_process()``, hãy thay dòng ``rotation += angular_speed * delta`` bằng đoạn code bên dưới.

.. tabs::
 .. code-tab:: gdscript GDScript

    var direction = 0
    if Input.is_action_pressed("ui_left"):
        direction = -1
    if Input.is_action_pressed("ui_right"):
        direction = 1

    rotation += angular_speed * direction * delta

 .. code-tab:: csharp C#

    var direction = 0;
    if (Input.IsActionPressed("ui_left"))
    {
        direction = -1;
    }
    if (Input.IsActionPressed("ui_right"))
    {
        direction = 1;
    }

    Rotation += _angularSpeed * direction * (float)delta;

Biến cục bộ ``direction`` là một hệ số nhân biểu thị hướng mà người chơi muốn xoay. Giá trị ``0`` có nghĩa là người chơi không nhấn phím mũi tên trái hoặc phải. Giá trị ``1`` có nghĩa là người chơi muốn xoay sang phải, còn ``-1`` có nghĩa là họ muốn xoay sang trái.

Để tạo ra các giá trị này, chúng ta giới thiệu câu lệnh điều kiện và cách sử dụng ``Input``. Một câu lệnh điều kiện bắt đầu bằng từ khóa ``if`` trong GDScript và kết thúc bằng dấu hai chấm. Điều kiện chính là biểu thức nằm giữa từ khóa và dấu hai chấm ở cuối dòng.

Để kiểm tra xem một phím có được nhấn trong frame này hay không, chúng ta gọi ``Input.is_action_pressed()``. Method này nhận một chuỗi văn bản đại diện cho một input action và trả về ``true`` nếu action đó đang được nhấn, nếu không thì trả về ``false``.

Hai action chúng ta sử dụng ở trên, "ui_left" và "ui_right", được định nghĩa sẵn trong mọi project Godot. Chúng lần lượt được kích hoạt khi người chơi nhấn phím mũi tên trái và phải trên bàn phím, hoặc nhấn trái và phải trên D-pad của gamepad.

.. note:: Bạn có thể xem và chỉnh sửa các input action trong project bằng cách đi tới
          :menu:`Project > Project Settings` and clicking on the :ui:`Input Map` tab.

Cuối cùng, chúng ta sử dụng ``direction`` làm hệ số nhân khi cập nhật ``rotation`` của node: ``rotation += angular_speed * direction * delta``.

Hãy comment các dòng ``var velocity = Vector2.UP.rotated(rotation) * speed`` và ``position += velocity * delta`` như sau:

.. tabs::

 .. code-tab:: gdscript GDScript

    #var velocity = Vector2.UP.rotated(rotation) * speed

    #position += velocity * delta

 .. code-tab:: csharp C#

    //var velocity = Vector2.Up.Rotated(Rotation) * _speed;

    //Position += velocity * (float)delta;

Thao tác này sẽ bỏ qua đoạn code đã di chuyển vị trí của icon theo hình tròn mà không cần input của người dùng trong bài tập trước.

Nếu chạy scene với đoạn code này, icon sẽ xoay khi bạn nhấn
:kbd:`Left` và :kbd:`Right`.

Di chuyển khi nhấn "up"
-----------------------

Để chỉ di chuyển khi nhấn một phím, chúng ta cần sửa đổi đoạn code tính velocity. Hãy bỏ comment đoạn code và thay dòng bắt đầu bằng ``var velocity`` bằng đoạn code bên dưới.

.. tabs::
 .. code-tab:: gdscript GDScript

    var velocity = Vector2.ZERO
    if Input.is_action_pressed("ui_up"):
        velocity = Vector2.UP.rotated(rotation) * speed

 .. code-tab:: csharp C#

    var velocity = Vector2.Zero;
    if (Input.IsActionPressed("ui_up"))
    {
        velocity = Vector2.Up.Rotated(Rotation) * _speed;
    }

Chúng ta khởi tạo ``velocity`` với giá trị ``Vector2.ZERO``, một hằng số khác thuộc kiểu ``Vector`` tích hợp sẵn, đại diện cho một vector 2D có độ dài bằng 0.

Nếu người chơi nhấn action "ui_up", chúng ta sẽ cập nhật giá trị của velocity, khiến sprite di chuyển về phía trước.

Script hoàn chỉnh
-----------------

Dưới đây là file ``sprite_2d.gd`` hoàn chỉnh để bạn tham khảo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400
    var angular_speed = PI


    func _process(delta):
        var direction = 0
        if Input.is_action_pressed("ui_left"):
            direction = -1
        if Input.is_action_pressed("ui_right"):
            direction = 1

        rotation += angular_speed * direction * delta

        var velocity = Vector2.ZERO
        if Input.is_action_pressed("ui_up"):
            velocity = Vector2.UP.rotated(rotation) * speed

        position += velocity * delta

 .. code-tab:: csharp C#

    using Godot;

    public partial class MySprite2D : Sprite2D
    {
        private float _speed = 400;
        private float _angularSpeed = Mathf.Pi;

        public override void _Process(double delta)
        {
            var direction = 0;
            if (Input.IsActionPressed("ui_left"))
            {
                direction = -1;
            }
            if (Input.IsActionPressed("ui_right"))
            {
                direction = 1;
            }

            Rotation += _angularSpeed * direction * (float)delta;

            var velocity = Vector2.Zero;
            if (Input.IsActionPressed("ui_up"))
            {
                velocity = Vector2.Up.Rotated(Rotation) * _speed;
            }

            Position += velocity * (float)delta;
        }
    }

Nếu chạy scene, giờ đây bạn có thể xoay bằng các phím mũi tên trái và phải, đồng thời di chuyển về phía trước bằng cách nhấn :kbd:`Up`.

.. image:: img/scripting_first_script_moving_with_input.gif

Tóm tắt
-------

Tóm lại, mọi script trong Godot đều đại diện cho một class và kế thừa một trong các class tích hợp sẵn của engine. Các kiểu node mà class của bạn kế thừa cung cấp quyền truy cập đến các property, chẳng hạn như ``rotation`` và ``position`` trong trường hợp của sprite. Bạn cũng kế thừa nhiều function, nhưng chúng ta chưa có dịp sử dụng trong ví dụ này.

Trong GDScript, các biến bạn đặt ở đầu file là các property của class, còn được gọi là member variable. Ngoài biến, bạn có thể định nghĩa các function; phần lớn trong số đó sẽ là method của class.

Godot cung cấp một số function ảo mà bạn có thể định nghĩa để kết nối class của mình với engine. Trong đó có ``_process()``, dùng để áp dụng các thay đổi cho node ở mỗi frame, và ``_unhandled_input()``, dùng để nhận các input event như thao tác nhấn phím và nút từ người dùng. Ngoài ra còn khá nhiều function khác.

Singleton ``Input`` cho phép bạn phản hồi input của người chơi ở bất kỳ đâu trong code. Cụ thể, bạn sẽ được sử dụng nó trong vòng lặp ``_process()``.

Trong bài học tiếp theo, :ref:`doc_signals`, chúng ta sẽ xây dựng thêm mối quan hệ giữa script và node bằng cách để các node kích hoạt code trong script.
