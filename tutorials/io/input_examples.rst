.. _doc_input_examples:

Các ví dụ về input
==================

Giới thiệu
----------

Trong tutorial này, bạn sẽ học cách sử dụng hệ thống :ref:`InputEvent <class_InputEvent>` của Godot để ghi nhận input từ người chơi. Có nhiều loại input khác nhau mà game của bạn có thể sử dụng - bàn phím, gamepad, chuột, v.v. - và cũng có nhiều cách khác nhau để chuyển những input đó thành các action trong game. Tài liệu này sẽ trình bày một số tình huống phổ biến nhất, để bạn có thể dùng làm điểm bắt đầu cho các project của riêng mình.

.. note:: For a detailed overview of how Godot's input event system works,
          xem :ref:`doc_inputevent`.

Event và polling
----------------

Đôi khi bạn muốn game phản hồi với một input event cụ thể - chẳng hạn như nhấn nút "jump". Trong những tình huống khác, bạn có thể muốn một việc xảy ra chừng nào một phím còn được nhấn, chẳng hạn như di chuyển. Trong trường hợp đầu tiên, bạn có thể sử dụng hàm ``_input()``, hàm này sẽ được gọi mỗi khi một input event xảy ra. Trong trường hợp thứ hai, Godot cung cấp singleton :ref:`Input <class_Input>`, bạn có thể dùng singleton này để truy vấn trạng thái của một input.

Ví dụ:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event.is_action_pressed("jump"):
            jump()


    func _physics_process(delta):
        if Input.is_action_pressed("move_right"):
            # Di chuyển chừng nào phím/nút còn được nhấn.
            position.x += speed * delta

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event.IsActionPressed("jump"))
        {
            Jump();
        }
    }

    public override void _PhysicsProcess(double delta)
    {
        if (Input.IsActionPressed("move_right"))
        {
            // Di chuyển chừng nào phím/nút còn được nhấn.
            position.X += speed * (float)delta;
        }
    }

Điều này giúp bạn linh hoạt kết hợp nhiều kiểu xử lý input khác nhau.

Trong phần còn lại của tutorial này, chúng ta sẽ tập trung vào việc ghi nhận từng event riêng lẻ trong ``_input()``.

Input event
-----------

Input event là các object kế thừa từ :ref:`InputEvent <class_InputEvent>`. Tùy thuộc vào loại event, object sẽ chứa các property cụ thể liên quan đến event đó. Để xem event thực tế trông như thế nào, hãy thêm một Node và gắn script sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node


    func _input(event):
        print(event.as_text())

 .. code-tab:: csharp

    using Godot;

    public partial class Node : Godot.Node
    {
        public override void _Input(InputEvent @event)
        {
            GD.Print(@event.AsText());
        }
    }

Khi bạn nhấn các phím, di chuyển chuột và thực hiện các input khác, bạn sẽ thấy từng event lần lượt xuất hiện trong cửa sổ output. Dưới đây là một ví dụ về output:

::

    A
    Mouse motion at position ((971, 5)) with velocity ((0, 0))
    Right Mouse Button
    Mouse motion at position ((870, 243)) with velocity ((0.454937, -0.454937))
    Left Mouse Button
    Mouse Wheel Up
    A
    B
    Shift
    Alt+Shift
    Alt
    Shift+T
    Mouse motion at position ((868, 242)) with velocity ((-2.134768, 2.134768))

Như bạn có thể thấy, kết quả rất khác nhau đối với từng loại input. Các key event thậm chí còn được in dưới dạng ký hiệu phím tương ứng. Ví dụ, hãy xét :ref:`InputEventMouseButton <class_InputEventMouseButton>`. Nó kế thừa từ các class sau:

- :ref:`InputEvent <class_InputEvent>` - class cơ sở cho mọi input event - :ref:`InputEventWithModifiers <class_InputEventWithModifiers>` - thêm khả năng kiểm tra xem các modifier có được nhấn hay không, chẳng hạn như :kbd:`Shift` hoặc :kbd:`Alt`. - :ref:`InputEventMouse <class_InputEventMouse>` - thêm các property của mouse event, chẳng hạn như ``position`` - :ref:`InputEventMouseButton <class_InputEventMouseButton>` - chứa index của nút đã được nhấn, cho biết đó có phải là double-click hay không, v.v.

.. tip:: It's a good idea to keep the class reference open while you're working
        với các event để bạn có thể kiểm tra những property và method có sẵn của loại event đó.

Bạn có thể gặp lỗi nếu cố truy cập một property trên một loại input không chứa property đó - chẳng hạn như gọi ``position`` trên ``InputEventKey``. Để tránh điều này, hãy kiểm tra loại event trước:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event is InputEventMouseButton:
            print("mouse button event at ", event.position)

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventMouseButton mouseEvent)
        {
            GD.Print("mouse button event at ", mouseEvent.Position);
        }
    }

.. _doc_input_examples_input_map:

InputMap
--------

:ref:`InputMap <class_InputMap>` là cách linh hoạt nhất để xử lý nhiều loại input. Bạn thực hiện việc này bằng cách tạo các *action* input có tên, sau đó có thể gán cho chúng bất kỳ số lượng input event nào, chẳng hạn như thao tác nhấn phím hoặc click chuột. Để xem chúng và thêm action của riêng bạn, hãy mở Project -> Project Settings rồi chọn tab InputMap:

.. image:: img/inputs_inputmap.webp

.. tip::

    Một project Godot mới đã bao gồm một số action mặc định được định nghĩa sẵn. Để xem chúng, hãy bật :button:`Show Built-in Actions` trong hộp thoại InputMap.

    Mặc dù không bắt buộc, bạn nên sử dụng quy ước đặt tên ``snake_case`` cho tên các input action.

Ghi nhận action
~~~~~~~~~~~~~~~

Sau khi định nghĩa các action, bạn có thể xử lý chúng trong script bằng ``is_action_pressed()`` và ``is_action_released()`` bằng cách truyền vào tên của action mà bạn muốn tìm:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event.is_action_pressed("my_action"):
            print("my_action occurred!")

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event.IsActionPressed("my_action"))
        {
            GD.Print("my_action occurred!");
        }
    }

Keyboard event
--------------

Keyboard event được ghi nhận trong :ref:`InputEventKey <class_InputEventKey>`. Mặc dù nên sử dụng input action thay thế, có thể có những trường hợp bạn muốn kiểm tra cụ thể các key event. Trong ví dụ này, hãy kiểm tra :kbd:`T`:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event is InputEventKey and event.pressed:
            if event.keycode == KEY_T:
                print("T was pressed")

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventKey keyEvent && keyEvent.Pressed)
        {
            if (keyEvent.Keycode == Key.T)
            {
                GD.Print("T was pressed");
            }
        }
    }

.. tip:: See :ref:`@GlobalScope_Key <enum_@GlobalScope_Key>` for a list of keycode
        các hằng số.

.. warning::

    Do hiện tượng *keyboard ghosting*, không phải mọi input phím đều có thể được ghi nhận tại một thời điểm nhất định nếu bạn nhấn quá nhiều phím cùng lúc. Do vị trí trên bàn phím, một số phím dễ gặp hiện tượng ghosting hơn những phím khác. Một số bàn phím có tính năng antighosting ở cấp độ phần cứng, nhưng tính năng này thường không có trên bàn phím cấp thấp và bàn phím laptop.

    Do đó, bạn nên sử dụng một bố cục bàn phím mặc định được thiết kế để hoạt động tốt trên bàn phím không có antighosting. Xem `this Gamedev Stack Exchange question <https://gamedev.stackexchange.com/a/109002>`__ để biết thêm thông tin.

Modifier trên bàn phím
~~~~~~~~~~~~~~~~~~~~~~

Các property của modifier được kế thừa từ
:ref:`InputEventWithModifiers <class_InputEventWithModifiers>`. This allows
để bạn kiểm tra các tổ hợp modifier bằng các property boolean. Hãy giả sử bạn muốn một việc xảy ra khi nhấn :kbd:`T`, nhưng một việc khác xảy ra khi nó là :kbd:`Shift + T`:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event is InputEventKey and event.pressed:
            if event.keycode == KEY_T:
                if event.shift_pressed:
                    print("Shift+T was pressed")
                else:
                    print("T was pressed")

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventKey keyEvent && keyEvent.Pressed)
        {
            switch (keyEvent.Keycode)
            {
                case Key.T:
                    GD.Print(keyEvent.ShiftPressed ? "Shift+T was pressed" : "T was pressed");
                    break;
            }
        }
    }

.. tip:: See :ref:`@GlobalScope_Key <enum_@GlobalScope_Key>` for a list of keycode
        các hằng số.

Mouse event
-----------

Mouse event bắt nguồn từ class :ref:`InputEventMouse <class_InputEventMouse>` và được chia thành hai loại: :ref:`InputEventMouseButton <class_InputEventMouseButton>` và :ref:`InputEventMouseMotion <class_InputEventMouseMotion>`. Lưu ý rằng điều này có nghĩa là mọi mouse event đều sẽ chứa một property ``position``.

Nút chuột
~~~~~~~~~

Việc ghi nhận các nút chuột rất giống với việc xử lý key event. :ref:`@GlobalScope_MouseButton <enum_@GlobalScope_MouseButton>` chứa một danh sách các hằng số ``MOUSE_BUTTON_*`` cho mỗi nút có thể có, và các nút này sẽ được báo cáo trong property ``button_index`` của event. Lưu ý rằng con lăn chuột cũng được tính là một nút - chính xác là hai nút, trong đó ``MOUSE_BUTTON_WHEEL_UP`` và ``MOUSE_BUTTON_WHEEL_DOWN`` là các event riêng biệt.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event is InputEventMouseButton:
            if event.button_index == MOUSE_BUTTON_LEFT and event.pressed:
                print("Left button was clicked at ", event.position)
            if event.button_index == MOUSE_BUTTON_WHEEL_UP and event.pressed:
                print("Wheel up")

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventMouseButton mouseEvent && mouseEvent.Pressed)
        {
            switch (mouseEvent.ButtonIndex)
            {
                case MouseButton.Left:
                    GD.Print($"Left button was clicked at {mouseEvent.Position}");
                    break;
                case MouseButton.WheelUp:
                    GD.Print("Wheel up");
                    break;
            }
        }
    }

Chuyển động chuột
~~~~~~~~~~~~~~~~~

:ref:`InputEventMouseMotion <class_InputEventMouseMotion>` events occur whenever
khi chuột di chuyển. Bạn có thể tìm khoảng cách di chuyển bằng property ``relative``.

Dưới đây là một ví dụ sử dụng mouse event để kéo và thả một node :ref:`Sprite2D <class_Sprite2D>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node


    var dragging = false
    var click_radius = 32 # Kích thước của sprite.


    func _input(event):
        if event is InputEventMouseButton and event.button_index == MOUSE_BUTTON_LEFT:
            if (event.position - $Sprite2D.position).length() < click_radius:
                # Bắt đầu kéo nếu click nằm trên sprite.
                if not dragging and event.pressed:
                    dragging = true
            # Dừng kéo nếu nút được nhả.
            if dragging and not event.pressed:
                dragging = false

        if event is InputEventMouseMotion and dragging:
            # Trong khi kéo, di chuyển sprite bằng chuột.
            $Sprite2D.position = event.position

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private bool _dragging = false;
        private int _clickRadius = 32; // Kích thước của sprite.

        public override void _Input(InputEvent @event)
        {
            Sprite2D sprite = GetNodeOrNull<Sprite2D>("Sprite2D");
            if (sprite == null)
            {
                return; // Không tìm thấy node phù hợp.
            }

            if (@event is InputEventMouseButton mouseEvent && mouseEvent.ButtonIndex == MouseButton.Left)
            {
                if ((mouseEvent.Position - sprite.Position).Length() < _clickRadius)
                {
                    // Bắt đầu kéo nếu click nằm trên sprite.
                    if (!_dragging && mouseEvent.Pressed)
                    {
                        _dragging = true;
                    }
                }
                // Dừng kéo nếu nút được nhả.
                if (_dragging && !mouseEvent.Pressed)
                {
                    _dragging = false;
                }
            }
            else
            {
                if (@event is InputEventMouseMotion motionEvent && _dragging)
                {
                    // Trong khi kéo, di chuyển sprite bằng chuột.
                    sprite.Position = motionEvent.Position;
                }
            }
        }
    }

Touch event
-----------

Nếu bạn đang sử dụng thiết bị màn hình cảm ứng, bạn có thể tạo touch event.
:ref:`InputEventScreenTouch <class_InputEventScreenTouch>` is equivalent to
một mouse click event, và :ref:`InputEventScreenDrag <class_InputEventScreenDrag>` hoạt động gần như giống với mouse motion.

.. tip:: To test your touch events on a non-touchscreen device, open Project
        Settings và chuyển đến phần "Input Devices/Pointing". Bật "Emulate Touch From Mouse" để project của bạn diễn giải các click và chuyển động của chuột thành touch event.
