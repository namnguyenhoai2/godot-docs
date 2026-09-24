.. _doc_inputevent:

Sử dụng InputEvent
==================

Nó là gì?
---------

Việc quản lý input thường phức tạp, bất kể hệ điều hành hay nền tảng nào. Để đơn giản hóa phần nào, một kiểu tích hợp đặc biệt được cung cấp là :ref:`InputEvent <class_InputEvent>`. Kiểu dữ liệu này có thể được cấu hình để chứa nhiều kiểu sự kiện input. Các sự kiện input đi qua engine và có thể được nhận tại nhiều vị trí, tùy theo mục đích.

Sau đây là một ví dụ nhanh, đóng game nếu nhấn phím escape:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _unhandled_input(event):
        if event is InputEventKey:
            if event.pressed and event.keycode == KEY_ESCAPE:
                get_tree().quit()

 .. code-tab:: csharp

    public override void _UnhandledInput(InputEvent @event)
    {
        if (@event is InputEventKey eventKey)
        {
            if (eventKey.Pressed && eventKey.Keycode == Key.Escape)
            {
                GetTree().Quit();
            }
        }
    }

Tuy nhiên, sử dụng tính năng :ref:`InputMap <class_InputMap>` được cung cấp sẽ gọn gàng và linh hoạt hơn. Tính năng này cho phép bạn định nghĩa các input action và gán cho chúng những phím khác nhau. Nhờ đó, bạn có thể định nghĩa nhiều phím cho cùng một action (ví dụ: phím escape trên bàn phím và nút start trên gamepad). Sau đó, bạn có thể dễ dàng thay đổi ánh xạ này trong phần cài đặt project mà không cần cập nhật code, thậm chí còn có thể xây dựng một tính năng ánh xạ phím dựa trên đó để cho phép game thay đổi ánh xạ phím trong runtime!

Bạn có thể thiết lập InputMap tại **Project > Project Settings > Input Map** rồi sử dụng các action đó như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _process(delta):
        if Input.is_action_pressed("ui_right"):
            # Di chuyển sang phải.

 .. code-tab:: csharp

    public override void _Process(double delta)
    {
        if (Input.IsActionPressed("ui_right"))
        {
            // Di chuyển sang phải.
        }
    }

Nó hoạt động như thế nào?
-------------------------

Mọi sự kiện input đều bắt nguồn từ người dùng/người chơi (mặc dù bạn có thể tạo một InputEvent rồi gửi lại cho engine, điều này hữu ích cho gesture). DisplayServer của mỗi nền tảng sẽ đọc các sự kiện từ hệ điều hành, sau đó gửi chúng đến :ref:`Window <class_Window>` gốc.

:ref:`Viewport <class_Viewport>` của cửa sổ xử lý input nhận được qua khá nhiều bước, theo thứ tự:

.. image:: img/input_event_flow.webp

1. Nếu Viewport đang nhúng các Windows, Viewport sẽ cố gắng diễn giải sự kiện trong khả năng của nó với tư cách Window-Manager (ví dụ: để thay đổi kích thước hoặc di chuyển các Windows).
2. Tiếp theo, nếu một Window được nhúng đang được focus, sự kiện sẽ được gửi đến Window đó và được xử lý trong Viewport của Window, sau đó được xem là đã xử lý. Nếu không có Window được nhúng nào đang được focus, sự kiện sẽ được gửi đến các node của viewport hiện tại theo thứ tự sau.
3. Trước hết, hàm :ref:`Node._input() <class_Node_private_method__input>` tiêu chuẩn sẽ được gọi trong mọi node override hàm này (và chưa tắt xử lý input bằng :ref:`Node.set_process_input() <class_Node_method_set_process_input>`). Nếu một hàm tiêu thụ sự kiện, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và sự kiện sẽ không lan truyền thêm. Điều này đảm bảo bạn có thể lọc tất cả sự kiện cần quan tâm, ngay cả trước GUI. Đối với input gameplay, :ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>` thường phù hợp hơn, vì nó cho phép GUI chặn các sự kiện.
4. Thứ hai, engine sẽ cố gắng gửi input đến GUI và kiểm tra xem có control nào có thể nhận nó hay không. Nếu có, :ref:`Control <class_Control>` sẽ được gọi thông qua hàm ảo :ref:`Control._gui_input() <class_Control_private_method__gui_input>` và signal "gui_input" sẽ được phát (hàm này có thể được triển khai lại bằng script thông qua việc kế thừa từ nó). Nếu control muốn "tiêu thụ" sự kiện, nó sẽ gọi :ref:`Control.accept_event() <class_Control_method_accept_event>` và sự kiện sẽ không lan truyền thêm. Sử dụng thuộc tính :ref:`Control.mouse_filter <class_Control_property_mouse_filter>` để kiểm soát việc :ref:`Control <class_Control>` có được thông báo về các sự kiện chuột thông qua callback :ref:`Control._gui_input() <class_Control_private_method__gui_input>` hay không, cũng như việc các sự kiện này có được truyền tiếp hay không.
5. Nếu đến thời điểm này vẫn chưa có đối tượng nào tiêu thụ sự kiện, callback :ref:`Node._shortcut_input() <class_Node_private_method__shortcut_input>` sẽ được gọi nếu đã override (và không bị tắt bằng
   :ref:`Node.set_process_shortcut_input() <class_Node_method_set_process_shortcut_input>`). Điều này chỉ xảy ra đối với :ref:`InputEventKey <class_InputEventKey>`,
   :ref:`InputEventShortcut <class_InputEventShortcut>` và :ref:`InputEventJoypadButton <class_InputEventJoypadButton>`. Nếu một hàm tiêu thụ sự kiện, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và sự kiện sẽ không lan truyền thêm. Callback shortcut input phù hợp nhất để xử lý các sự kiện được dùng làm shortcut.
6. Nếu đến thời điểm này vẫn chưa có đối tượng nào tiêu thụ sự kiện, callback :ref:`Node._unhandled_key_input() <class_Node_private_method__unhandled_key_input>` sẽ được gọi nếu đã override (và không bị tắt bằng
   :ref:`Node.set_process_unhandled_key_input() <class_Node_method_set_process_unhandled_key_input>`). Điều này chỉ xảy ra nếu sự kiện là :ref:`InputEventKey <class_InputEventKey>`. Nếu một hàm tiêu thụ sự kiện, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và sự kiện sẽ không lan truyền thêm. Callback unhandled key input phù hợp nhất cho các sự kiện phím.
7. Nếu đến thời điểm này vẫn chưa có đối tượng nào tiêu thụ sự kiện, callback :ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>` sẽ được gọi nếu đã override (và không bị tắt bằng
   :ref:`Node.set_process_unhandled_input() <class_Node_method_set_process_unhandled_input>`). Nếu một hàm tiêu thụ sự kiện, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và sự kiện sẽ không lan truyền thêm. Callback unhandled input phù hợp nhất cho các sự kiện gameplay toàn màn hình, để chúng không được nhận khi GUI đang hoạt động.
8. Nếu đến thời điểm này vẫn chưa có đối tượng nào muốn xử lý sự kiện và :ref:`Object Picking <class_viewport_property_physics_object_picking>` được bật, sự kiện sẽ được dùng để picking object. Đối với root viewport, tính năng này cũng có thể được bật trong :ref:`Project Settings <class_ProjectSettings_property_physics/common/enable_object_picking>`. Trong scene 3D, nếu một :ref:`Camera3D <class_Camera3D>` được gán cho Viewport, một tia đến physics world (theo hướng tia từ vị trí click) sẽ được chiếu. Nếu tia này va vào một object, hàm :ref:`CollisionObject3D._input_event() <class_CollisionObject3D_private_method__input_event>` sẽ được gọi trong physics object tương ứng. Trong scene 2D, về mặt khái niệm, điều tương tự sẽ xảy ra với :ref:`CollisionObject2D._input_event() <class_CollisionObject2D_private_method__input_event>`.

Khi gửi sự kiện đến các node con và hậu duệ của nó, viewport sẽ thực hiện theo như hình minh họa bên dưới, theo thứ tự duyệt depth-first ngược, bắt đầu từ node ở cuối scene tree và kết thúc tại node gốc. Các Windows và SubViewports không thuộc quy trình này.

.. image:: img/input_event_scene_flow.webp

.. note::

   Thứ tự này không áp dụng cho :ref:`Control._gui_input() <class_Control_private_method__gui_input>`, vì nó sử dụng một phương thức khác dựa trên vị trí sự kiện hoặc Control đang được focus. Các sự kiện GUI **mouse** cũng đi lên scene tree, tuân theo các giới hạn :ref:`Control.mouse_filter <class_Control_property_mouse_filter>` được mô tả ở trên. Tuy nhiên, vì các sự kiện này nhắm đến những Control cụ thể, chỉ các ancestor trực tiếp của node Control đích mới nhận được sự kiện. Các sự kiện GUI **keyboard and joypad** *do not* đi lên scene tree và chỉ có thể được xử lý bởi Control đã nhận chúng. Nếu không, chúng sẽ được truyền tiếp dưới dạng các sự kiện không thuộc GUI thông qua :ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>`.

Vì Viewport không gửi sự kiện đến các :ref:`SubViewports <class_SubViewport>` khác, phải sử dụng một trong các phương thức sau:

1. Sử dụng :ref:`SubViewportContainer <class_SubViewportContainer>`, tự động gửi sự kiện đến :ref:`SubViewports <class_SubViewport>` con của nó sau
   :ref:`Node._input() <class_Node_private_method__input>` hoặc :ref:`Control._gui_input() <class_Control_private_method__gui_input>`.
2. Triển khai việc truyền sự kiện dựa trên các yêu cầu riêng.

Phù hợp với thiết kế dựa trên node của Godot, điều này cho phép các node con chuyên biệt xử lý và tiêu thụ những sự kiện cụ thể, trong khi các ancestor của chúng và cuối cùng là scene root có thể cung cấp hành vi tổng quát hơn khi cần.

Cấu tạo của InputEvent
----------------------

:ref:`InputEvent <class_InputEvent>` chỉ là một kiểu tích hợp cơ sở, không đại diện cho bất cứ thứ gì và chỉ chứa một số thông tin cơ bản, chẳng hạn như ID sự kiện (được tăng lên sau mỗi sự kiện), chỉ mục thiết bị, v.v.

Có một số kiểu InputEvent chuyên biệt, được mô tả trong bảng dưới đây:

+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| Sự kiện                                                          | Mô tả                                                                                                      |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEvent <class_InputEvent>`                             | Input Event trống.                                                                                         |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventKey <class_InputEventKey>`                       | Chứa keycode và giá trị Unicode, cùng với các modifier.                                                    |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventMouseButton <class_InputEventMouseButton>`       | Chứa thông tin click, chẳng hạn như button, modifier, v.v.                                                 |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventMouseMotion <class_InputEventMouseMotion>`       | Chứa thông tin về chuyển động, chẳng hạn như vị trí tương đối và tuyệt đối cùng tốc độ.                    |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventJoypadMotion <class_InputEventJoypadMotion>`     | Chứa thông tin về trục analog của Joystick/Joypad.                                                         |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventJoypadButton <class_InputEventJoypadButton>`     | Chứa thông tin về nút của Joystick/Joypad.                                                                 |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventScreenTouch <class_InputEventScreenTouch>`       | Chứa thông tin nhấn/thả đa điểm. (chỉ khả dụng trên thiết bị di động)                                      |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventScreenDrag <class_InputEventScreenDrag>`         | Chứa thông tin kéo đa điểm. (chỉ khả dụng trên thiết bị di động)                                           |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventMagnifyGesture <class_InputEventMagnifyGesture>` | Chứa một vị trí, một hệ số và các modifier.                                                                |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventPanGesture <class_InputEventPanGesture>`         | Chứa một vị trí, một delta và các modifier.                                                                |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventMIDI <class_InputEventMIDI>`                     | Chứa thông tin liên quan đến MIDI.                                                                         |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventShortcut <class_InputEventShortcut>`             | Chứa một shortcut.                                                                                         |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+
| :ref:`InputEventAction <class_InputEventAction>`                 | Chứa một action chung. Những event này thường được lập trình viên tạo ra làm phản hồi. (xem thêm bên dưới) |
+------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------+

Các action đầu vào
------------------

Các action đầu vào là việc nhóm không hoặc nhiều InputEvent vào một tên gọi thường được hiểu (ví dụ: action mặc định "ui_left" nhóm cả input joypad-left và phím mũi tên trái trên bàn phím). Chúng không bắt buộc phải đại diện cho một InputEvent, nhưng hữu ích vì trừu tượng hóa nhiều input khác nhau khi lập trình logic của game.

Điều này cho phép:

-  Cùng một đoạn code hoạt động trên các thiết bị khác nhau với các input khác nhau (ví dụ: bàn phím trên PC, Joypad trên console).
-  Có thể cấu hình lại input trong runtime.
-  Có thể kích hoạt các action bằng code trong runtime.

Có thể tạo các action từ menu Project Settings trong thẻ **Input Map** và gán các input event cho chúng.

Mọi event đều có các method :ref:`InputEvent.is_action() <class_InputEvent_method_is_action>`,
:ref:`InputEvent.is_pressed() <class_InputEvent_method_is_pressed>` và :ref:`InputEvent.is_echo() <class_InputEvent_method_is_echo>`.

Ngoài ra, bạn có thể muốn gửi một action trở lại game từ code của game (một ví dụ điển hình là phát hiện gesture). Singleton Input có một method dành cho việc này:
:ref:`Input.parse_input_event() <class_input_method_parse_input_event>`. Thông thường, bạn sẽ sử dụng nó như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var ev = InputEventAction.new()
    # Đặt thành ui_left, đã nhấn.
    ev.action = "ui_left"
    ev.pressed = true
    # Phản hồi.
    Input.parse_input_event(ev)

 .. code-tab:: csharp

    var ev = new InputEventAction();
    // Đặt thành ui_left, đã nhấn.
    ev.Action = "ui_left";
    ev.Pressed = true;
    // Phản hồi.
    Input.ParseInputEvent(ev);


.. seealso::

   Xem :ref:`doc_first_3d_game_input_actions` để tìm hướng dẫn thêm action đầu vào trong phần cài đặt project.

InputMap
--------

Việc tùy chỉnh và ánh xạ lại input từ code thường là điều cần thiết. Nếu toàn bộ quy trình làm việc của bạn phụ thuộc vào các action, singleton :ref:`InputMap <class_InputMap>` là lựa chọn lý tưởng để gán lại hoặc tạo các action khác nhau trong runtime. Singleton này không được lưu (phải được sửa đổi thủ công) và trạng thái của nó được chạy từ phần cài đặt project (project.godot). Vì vậy, mọi hệ thống động thuộc loại này cần lưu trữ các cài đặt theo cách mà lập trình viên thấy phù hợp nhất.
