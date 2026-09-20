.. Mục đích: tại thời điểm này, chỉ giới thiệu một phương thức nhập cần thiết. Phần Inputs trong tài liệu nên cung cấp thêm các hướng dẫn so sánh những công cụ khác nhau mà bạn có để quản lý độ phức tạp của dữ liệu đầu vào từ người dùng.

.. _doc_scripting_player_input:

Lắng nghe dữ liệu đầu vào từ người chơi
=======================================

Dựa trên bài học trước, :ref:`doc_scripting_first_script`, hãy cùng xem xét một tính năng quan trọng khác của mọi trò chơi: trao quyền điều khiển cho người chơi. Để thêm tính năng này, chúng ta cần chỉnh sửa mã ``sprite_2d.gd``.

.. image:: img/scripting_first_script_moving_with_input.gif

Bạn có hai công cụ chính để xử lý dữ liệu đầu vào của người chơi trong Godot:

1. Các callback đầu vào tích hợp sẵn, chủ yếu là ``_unhandled_input()``. Giống như ``_process()``, đây là một hàm ảo tích hợp sẵn được Godot gọi mỗi khi người chơi nhấn một phím. Đây là công cụ bạn nên dùng để phản hồi các sự kiện không xảy ra ở mỗi khung hình, chẳng hạn như nhấn :kbd:`Space` để nhảy. Để tìm hiểu thêm về các callback đầu vào, hãy xem :ref:`doc_inputevent`. 2. Singleton ``Input``. Singleton là một đối tượng có thể truy cập trên toàn cục. Godot cung cấp quyền truy cập đến một số singleton trong các script. Đây là công cụ phù hợp để kiểm tra dữ liệu đầu vào ở mỗi khung hình.

Ở đây chúng ta sẽ sử dụng singleton ``Input`` vì cần biết liệu người chơi có muốn xoay hoặc di chuyển ở mỗi khung hình hay không.

Để xoay, chúng ta nên sử dụng một biến mới: ``direction``. Trong hàm ``_process()``, hãy thay dòng ``rotation += angular_speed * delta`` bằng đoạn mã dưới đây.

.. tabs::
 .. code-tab:: gdscript GDScript

    var direction = 0 if Input.is_action_pressed("ui_left"): direction = -1 if Input.is_action_pressed("ui_right"): direction = 1

    rotation += angular_speed * direction * delta

 .. code-tab:: csharp C#

    var direction = 0; if (Input.IsActionPressed("ui_left")) { direction = -1; } if (Input.IsActionPressed("ui_right")) { direction = 1; }

    Rotation += _angularSpeed * direction * (float)delta;

Biến cục bộ ``direction`` là một hệ số biểu thị hướng mà người chơi muốn xoay. Giá trị ``0`` có nghĩa là người chơi không nhấn phím mũi tên trái hay phải. Giá trị ``1`` có nghĩa là người chơi muốn xoay sang phải, còn ``-1`` có nghĩa là họ muốn xoay sang trái.

Để tạo ra các giá trị này, chúng ta giới thiệu câu lệnh điều kiện và cách sử dụng ``Input``. Một câu lệnh điều kiện bắt đầu bằng từ khóa ``if`` trong GDScript và kết thúc bằng dấu hai chấm. Điều kiện chính là biểu thức nằm giữa từ khóa và dấu hai chấm ở cuối dòng.

Để kiểm tra xem một phím có được nhấn trong khung hình này hay không, chúng ta gọi ``Input.is_action_pressed()``. Phương thức này nhận một chuỗi văn bản biểu thị một hành động đầu vào và trả về ``true`` nếu hành động đó đang được nhấn, nếu không thì trả về ``false``.

Hai hành động chúng ta sử dụng ở trên, "ui_left" và "ui_right", được định nghĩa sẵn trong mọi dự án Godot. Tương ứng, chúng được kích hoạt khi người chơi nhấn phím mũi tên trái và phải trên bàn phím, hoặc nhấn trái và phải trên D-pad của tay cầm chơi game.

.. note:: You can see and edit input actions in your project by going to
          :menu:`Project > Project Settings` and clicking on the :ui:`Input Map` tab.

Cuối cùng, chúng ta sử dụng ``direction`` làm hệ số khi cập nhật ``rotation`` của node: ``rotation += angular_speed * direction * delta``.

Hãy chú thích các dòng ``var velocity = Vector2.UP.rotated(rotation) * speed`` và ``position += velocity * delta`` như sau:

.. tabs::

 .. code-tab:: gdscript GDScript

    #var velocity = Vector2.UP.rotated(rotation) * speed

    #position += velocity * delta

 .. code-tab:: csharp C#

    //var velocity = Vector2.Up.Rotated(Rotation) * _speed;

    //Position += velocity * (float)delta;

Thao tác này sẽ bỏ qua đoạn mã đã di chuyển vị trí của biểu tượng theo vòng tròn mà không cần dữ liệu đầu vào từ người dùng trong bài tập trước.

Nếu chạy scene với đoạn mã này, biểu tượng sẽ xoay khi bạn nhấn
:kbd:`Left` and :kbd:`Right`.

Di chuyển khi nhấn "up"
-----------------------

Để chỉ di chuyển khi nhấn một phím, chúng ta cần chỉnh sửa đoạn mã tính toán vận tốc. Bỏ chú thích đoạn mã và thay dòng bắt đầu bằng ``var velocity`` bằng đoạn mã dưới đây.

.. tabs::
 .. code-tab:: gdscript GDScript

    var velocity = Vector2.ZERO if Input.is_action_pressed("ui_up"): velocity = Vector2.UP.rotated(rotation) * speed

 .. code-tab:: csharp C#

    var velocity = Vector2.Zero; if (Input.IsActionPressed("ui_up")) { velocity = Vector2.Up.Rotated(Rotation) * _speed; }

Chúng ta khởi tạo ``velocity`` với giá trị ``Vector2.ZERO``, một hằng số khác thuộc kiểu ``Vector`` tích hợp sẵn, biểu thị một vector 2D có độ dài bằng 0.

Nếu người chơi nhấn hành động "ui_up", chúng ta sẽ cập nhật giá trị của vận tốc, khiến sprite di chuyển về phía trước.

Script hoàn chỉnh
-----------------

Dưới đây là tệp ``sprite_2d.gd`` hoàn chỉnh để bạn tham khảo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Sprite2D

    var speed = 400 var angular_speed = PI


    func _process(delta): var direction = 0 if Input.is_action_pressed("ui_left"): direction = -1 if Input.is_action_pressed("ui_right"): direction = 1

        rotation += angular_speed * direction * delta

        var velocity = Vector2.ZERO if Input.is_action_pressed("ui_up"): velocity = Vector2.UP.rotated(rotation) * speed

        position += velocity * delta

 .. code-tab:: csharp C#

    using Godot;

    public partial class MySprite2D : Sprite2D { private float _speed = 400; private float _angularSpeed = Mathf.Pi;

        public override void _Process(double delta) { var direction = 0; if (Input.IsActionPressed("ui_left")) { direction = -1; } if (Input.IsActionPressed("ui_right")) { direction = 1; }

            Rotation += _angularSpeed * direction * (float)delta;

            var velocity = Vector2.Zero; if (Input.IsActionPressed("ui_up")) { velocity = Vector2.Up.Rotated(Rotation) * _speed; }

            Position += velocity * (float)delta; } }

Nếu chạy scene, giờ bạn có thể xoay bằng các phím mũi tên trái và phải, đồng thời di chuyển về phía trước bằng cách nhấn :kbd:`Up`.

.. image:: img/scripting_first_script_moving_with_input.gif

Tóm tắt
-------

Tóm lại, mọi script trong Godot đều biểu thị một lớp và kế thừa một trong các lớp tích hợp sẵn của engine. Các loại node mà lớp của bạn kế thừa cho phép bạn truy cập các thuộc tính, chẳng hạn như ``rotation`` và ``position`` trong trường hợp của sprite. Bạn cũng kế thừa nhiều hàm, nhưng chúng ta chưa có dịp sử dụng trong ví dụ này.

Trong GDScript, các biến bạn đặt ở đầu tệp là các thuộc tính của lớp, còn được gọi là biến thành viên. Ngoài biến, bạn có thể định nghĩa các hàm, mà phần lớn sẽ là các phương thức của lớp.

Godot cung cấp một số hàm ảo mà bạn có thể định nghĩa để kết nối lớp của mình với engine. Trong đó có ``_process()``, dùng để áp dụng các thay đổi cho node ở mỗi khung hình, và ``_unhandled_input()``, dùng để nhận các sự kiện đầu vào như thao tác nhấn phím và nút từ người dùng. Ngoài ra còn khá nhiều hàm khác.

Singleton ``Input`` cho phép bạn phản hồi dữ liệu đầu vào của người chơi ở bất kỳ đâu trong mã của mình. Cụ thể, bạn sẽ sử dụng nó trong vòng lặp ``_process()``.

Trong bài học tiếp theo, :ref:`doc_signals`, chúng ta sẽ xây dựng dựa trên mối quan hệ giữa script và node bằng cách cho các node kích hoạt mã trong script.
