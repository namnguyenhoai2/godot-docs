.. _doc_input_examples:

Ví dụ đầu vào
=============

Giới thiệu
----------

Trong hướng dẫn này, bạn sẽ học cách sử dụng hệ thống :ref:`InputEvent <class_InputEvent>` của Godot để thu nhận đầu vào từ người chơi. Trò chơi của bạn có thể sử dụng nhiều loại đầu vào khác nhau - bàn phím, gamepad, chuột, v.v. - và có nhiều cách khác nhau để chuyển những đầu vào đó thành các hành động trong trò chơi. Tài liệu này sẽ trình bày một số tình huống phổ biến nhất, mà bạn có thể dùng làm điểm khởi đầu cho các dự án của riêng mình.

.. note:: Để xem tổng quan chi tiết về cách hệ thống sự kiện đầu vào của Godot hoạt động, hãy xem :ref:`doc_inputevent`.

Sự kiện và thăm dò trạng thái
-----------------------------

Đôi khi bạn muốn trò chơi phản hồi một sự kiện đầu vào cụ thể - chẳng hạn như nhấn nút "nhảy". Trong những tình huống khác, bạn có thể muốn một việc xảy ra miễn là một phím đang được nhấn, chẳng hạn như di chuyển. Trong trường hợp đầu tiên, bạn có thể sử dụng hàm ``_input()``, hàm này sẽ được gọi bất cứ khi nào một sự kiện đầu vào xảy ra. Trong trường hợp thứ hai, Godot cung cấp singleton :ref:`Input <class_Input>`, mà bạn có thể dùng để truy vấn trạng thái của một đầu vào.

Ví dụ:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        if event.is_action_pressed("jump"):
            jump()


    func _physics_process(delta):
        if Input.is_action_pressed("move_right"):
            # Di chuyển miễn là phím/nút đang được nhấn.
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
            // Di chuyển miễn là phím/nút đang được nhấn.
            position.X += speed * (float)delta;
        }
    }

Điều này giúp bạn linh hoạt kết hợp các kiểu xử lý đầu vào khác nhau.

Trong phần còn lại của hướng dẫn này, chúng ta sẽ tập trung vào việc thu nhận từng sự kiện riêng lẻ trong ``_input()``.

Sự kiện đầu vào
---------------

Sự kiện đầu vào là các đối tượng kế thừa từ :ref:`InputEvent <class_InputEvent>`. Tùy thuộc vào loại sự kiện, đối tượng sẽ chứa các thuộc tính cụ thể liên quan đến sự kiện đó. Để xem các sự kiện thực sự trông như thế nào, hãy thêm một Node và gắn script sau:

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

Khi bạn nhấn phím, di chuyển chuột và thực hiện các thao tác đầu vào khác, bạn sẽ thấy từng sự kiện lần lượt xuất hiện trong cửa sổ output. Dưới đây là một ví dụ về output:

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

Như bạn có thể thấy, kết quả rất khác nhau đối với các loại đầu vào khác nhau. Các sự kiện phím thậm chí còn được in dưới dạng ký hiệu phím tương ứng. Ví dụ, hãy xét :ref:`InputEventMouseButton <class_InputEventMouseButton>`. Nó kế thừa từ các lớp sau:

- :ref:`InputEvent <class_InputEvent>` - lớp cơ sở cho mọi sự kiện đầu vào
- :ref:`InputEventWithModifiers <class_InputEventWithModifiers>` - bổ sung khả năng kiểm tra xem các phím bổ trợ có đang được nhấn hay không, chẳng hạn như :kbd:`Shift` hoặc :kbd:`Alt`.
- :ref:`InputEventMouse <class_InputEventMouse>` - bổ sung các thuộc tính sự kiện chuột, chẳng hạn như ``position``
- :ref:`InputEventMouseButton <class_InputEventMouseButton>` - chứa chỉ mục của nút đã được nhấn, cho biết đó có phải là thao tác nhấp đúp hay không, v.v.

.. tip:: Bạn nên mở phần tham chiếu lớp trong khi làm việc với các sự kiện để có thể kiểm tra những thuộc tính và phương thức khả dụng của loại sự kiện.

Bạn có thể gặp lỗi nếu cố truy cập một thuộc tính trên một kiểu đầu vào không chứa thuộc tính đó - chẳng hạn như gọi ``position`` trên ``InputEventKey``. Để tránh điều này, trước tiên hãy kiểm tra loại sự kiện:

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

:ref:`InputMap <class_InputMap>` là cách linh hoạt nhất để xử lý nhiều loại đầu vào. Bạn sử dụng nó bằng cách tạo các *action* đầu vào có tên, sau đó có thể gán cho chúng bất kỳ số lượng sự kiện đầu vào nào, chẳng hạn như thao tác nhấn phím hoặc nhấp chuột. Để xem các action đó và thêm action của riêng bạn, hãy mở Project -> Project Settings rồi chọn tab InputMap:

.. image:: img/inputs_inputmap.webp

.. tip::

    Một dự án Godot mới đã có sẵn một số action mặc định được định nghĩa. Để xem chúng, hãy bật :button:`Show Built-in Actions` trong hộp thoại InputMap.

    Mặc dù không bắt buộc nghiêm ngặt, bạn nên sử dụng quy ước đặt tên ``snake_case`` cho tên các action đầu vào.

Thu nhận action
~~~~~~~~~~~~~~~

Sau khi định nghĩa các action, bạn có thể xử lý chúng trong script bằng ``is_action_pressed()`` và ``is_action_released()`` bằng cách truyền vào tên của action mà bạn đang tìm kiếm:

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

Sự kiện bàn phím
----------------

Sự kiện bàn phím được thu nhận trong :ref:`InputEventKey <class_InputEventKey>`. Mặc dù nên sử dụng input action, có thể có những trường hợp bạn muốn kiểm tra cụ thể các sự kiện phím. Trong ví dụ này, hãy kiểm tra :kbd:`T`:

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

.. tip:: Xem :ref:`@GlobalScope_Key <enum_@GlobalScope_Key>` để biết danh sách các hằng số keycode.

.. warning::

    Do *keyboard ghosting*, không phải mọi đầu vào phím đều có thể được ghi nhận tại một thời điểm nhất định nếu bạn nhấn quá nhiều phím cùng lúc. Do vị trí của chúng trên bàn phím, một số phím dễ bị ghosting hơn những phím khác. Một số bàn phím có tính năng antighosting ở cấp phần cứng, nhưng tính năng này thường không có trên bàn phím giá rẻ và bàn phím máy tính xách tay.

    Do đó, bạn nên sử dụng bố cục bàn phím mặc định được thiết kế để hoạt động tốt trên bàn phím không có antighosting. Xem `this Gamedev Stack Exchange question <https://gamedev.stackexchange.com/a/109002>`__ để biết thêm thông tin.

Phím bổ trợ trên bàn phím
~~~~~~~~~~~~~~~~~~~~~~~~~

Các thuộc tính phím bổ trợ được kế thừa từ
:ref:`InputEventWithModifiers <class_InputEventWithModifiers>`. Điều này cho phép bạn kiểm tra các tổ hợp phím bổ trợ bằng các thuộc tính boolean. Hãy tưởng tượng bạn muốn một việc xảy ra khi nhấn :kbd:`T`, nhưng một việc khác xảy ra khi phím đó :kbd:`Shift + T`:

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

.. tip:: Xem :ref:`@GlobalScope_Key <enum_@GlobalScope_Key>` để biết danh sách các hằng số keycode.

Sự kiện chuột
-------------

Các sự kiện chuột bắt nguồn từ lớp :ref:`InputEventMouse <class_InputEventMouse>` và được chia thành hai loại: :ref:`InputEventMouseButton <class_InputEventMouseButton>` và :ref:`InputEventMouseMotion <class_InputEventMouseMotion>`. Lưu ý rằng điều này có nghĩa là mọi sự kiện chuột đều chứa thuộc tính ``position``.

Nút chuột
~~~~~~~~~

Việc thu nhận các nút chuột rất giống với việc xử lý các sự kiện phím. :ref:`@GlobalScope_MouseButton <enum_@GlobalScope_MouseButton>` chứa danh sách các hằng số ``MOUSE_BUTTON_*`` cho từng nút có thể có, và các hằng số này sẽ được báo cáo trong thuộc tính ``button_index`` của sự kiện. Lưu ý rằng con lăn chuột cũng được tính là một nút - chính xác là hai nút, với ``MOUSE_BUTTON_WHEEL_UP`` và ``MOUSE_BUTTON_WHEEL_DOWN`` là các sự kiện riêng biệt.

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

Các sự kiện :ref:`InputEventMouseMotion <class_InputEventMouseMotion>` xảy ra mỗi khi chuột di chuyển. Bạn có thể tìm khoảng cách di chuyển bằng thuộc tính ``relative``.

Dưới đây là một ví dụ sử dụng các sự kiện chuột để kéo và thả một node :ref:`Sprite2D <class_Sprite2D>`:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node


    var dragging = false
    var click_radius = 32 # Kích thước của sprite.


    func _input(event):
        if event is InputEventMouseButton and event.button_index == MOUSE_BUTTON_LEFT:
            if (event.position - $Sprite2D.position).length() < click_radius:
                # Bắt đầu kéo nếu thao tác nhấp nằm trên sprite.
                if not dragging and event.pressed:
                    dragging = true
            # Dừng kéo nếu nút được thả ra.
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
                    // Bắt đầu kéo nếu thao tác nhấp nằm trên sprite.
                    if (!_dragging && mouseEvent.Pressed)
                    {
                        _dragging = true;
                    }
                }
                // Dừng kéo khi nhả nút chuột.
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

Sự kiện cảm ứng
---------------

Nếu bạn đang sử dụng thiết bị màn hình cảm ứng, bạn có thể tạo các sự kiện cảm ứng.
:ref:`InputEventScreenTouch <class_InputEventScreenTouch>` tương đương với sự kiện nhấp chuột và :ref:`InputEventScreenDrag <class_InputEventScreenDrag>` hoạt động gần giống như chuyển động chuột.

.. tip:: Để kiểm thử các sự kiện cảm ứng trên thiết bị không có màn hình cảm ứng, hãy mở Project Settings và đi đến phần "Input Devices/Pointing". Bật "Emulate Touch From Mouse" để dự án của bạn diễn giải các thao tác nhấp và di chuyển chuột thành các sự kiện cảm ứng.
