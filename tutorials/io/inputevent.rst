.. _doc_inputevent:

Sử dụng InputEvent
==================

Đó là gì?
---------

Việc xử lý input thường phức tạp, bất kể hệ điều hành hay nền tảng nào. Để giảm bớt phần nào sự phức tạp này, một kiểu tích hợp đặc biệt được cung cấp, :ref:`InputEvent <class_InputEvent>`. Kiểu dữ liệu này có thể được cấu hình để chứa một số kiểu sự kiện input. Các sự kiện input di chuyển qua engine và có thể được nhận ở nhiều vị trí, tùy theo mục đích.

Dưới đây là một ví dụ nhanh, đóng game khi nhấn phím escape:

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

Tuy nhiên, sử dụng tính năng :ref:`InputMap <class_InputMap>` được cung cấp sẽ rõ ràng và linh hoạt hơn; tính năng này cho phép bạn định nghĩa các input action và gán cho chúng những phím khác nhau. Nhờ vậy, bạn có thể định nghĩa nhiều phím cho cùng một action (ví dụ: phím escape trên bàn phím và nút start trên gamepad). Sau đó, bạn có thể dễ dàng thay đổi ánh xạ này trong project settings mà không cần cập nhật code, thậm chí còn có thể xây dựng một tính năng ánh xạ phím trên nền tảng đó để cho phép game thay đổi ánh xạ phím trong runtime!

Bạn có thể thiết lập InputMap trong **Project > Project Settings > Input Map**, sau đó sử dụng các action đó như sau:

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

Mọi input event đều bắt nguồn từ người dùng/người chơi (mặc dù bạn có thể tạo một InputEvent và đưa nó trở lại engine, điều này hữu ích cho gesture). DisplayServer của mỗi nền tảng sẽ đọc các event từ hệ điều hành, sau đó đưa chúng vào :ref:`Window <class_Window>` gốc.

:ref:`Viewport <class_Viewport>` của cửa sổ thực hiện khá nhiều việc với input nhận được, theo thứ tự:

.. image:: img/input_event_flow.webp

1. Nếu Viewport đang nhúng các Windows, Viewport sẽ cố gắng diễn giải event dựa trên khả năng của nó với vai trò Window-Manager (ví dụ: thay đổi kích thước hoặc di chuyển các Windows). 2. Tiếp theo, nếu một Window được nhúng đang được focus, event sẽ được gửi đến Window đó và được xử lý trong Viewport của Window, sau đó được xem là đã xử lý. Nếu không có Window được nhúng nào đang được focus, event sẽ được gửi đến các node của viewport hiện tại theo thứ tự sau. 3. Trước hết, hàm :ref:`Node._input() <class_Node_private_method__input>` tiêu chuẩn sẽ được gọi trên mọi node override hàm này (và chưa vô hiệu hóa việc xử lý input bằng :ref:`Node.set_process_input() <class_Node_method_set_process_input>`). Nếu bất kỳ hàm nào tiêu thụ event, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và event sẽ không lan truyền thêm. Điều này đảm bảo bạn có thể lọc tất cả event cần quan tâm, ngay cả trước GUI. Đối với input trong gameplay, :ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>` thường phù hợp hơn, vì nó cho phép GUI chặn các event. 4. Thứ hai, engine sẽ cố gắng đưa input vào GUI và kiểm tra xem control nào có thể nhận nó. Nếu có, :ref:`Control <class_Control>` sẽ được gọi thông qua hàm ảo :ref:`Control._gui_input() <class_Control_private_method__gui_input>` và signal "gui_input" sẽ được phát ra (hàm này có thể được triển khai lại bằng script thông qua việc kế thừa từ nó). Nếu control muốn "tiêu thụ" event, nó sẽ gọi :ref:`Control.accept_event() <class_Control_method_accept_event>` và event sẽ không lan truyền thêm. Sử dụng thuộc tính :ref:`Control.mouse_filter <class_Control_property_mouse_filter>` để kiểm soát việc một :ref:`Control <class_Control>` có được thông báo về các event chuột thông qua callback :ref:`Control._gui_input() <class_Control_private_method__gui_input>` hay không, cũng như việc các event này có được truyền tiếp hay không. 5. Nếu đến thời điểm này vẫn chưa có thành phần nào tiêu thụ event, callback :ref:`Node._shortcut_input() <class_Node_private_method__shortcut_input>` sẽ được gọi nếu được override (và không bị vô hiệu hóa bằng
   :ref:`Node.set_process_shortcut_input() <class_Node_method_set_process_shortcut_input>`).
   Điều này chỉ xảy ra đối với :ref:`InputEventKey <class_InputEventKey>`,
   :ref:`InputEventShortcut <class_InputEventShortcut>` and :ref:`InputEventJoypadButton <class_InputEventJoypadButton>`.
   Nếu bất kỳ hàm nào tiêu thụ event, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và event sẽ không lan truyền thêm. Callback input shortcut rất phù hợp để xử lý các event được dùng làm shortcut. 6. Nếu đến thời điểm này vẫn chưa có thành phần nào tiêu thụ event, callback :ref:`Node._unhandled_key_input() <class_Node_private_method__unhandled_key_input>` sẽ được gọi nếu được override (và không bị vô hiệu hóa bằng
   :ref:`Node.set_process_unhandled_key_input() <class_Node_method_set_process_unhandled_key_input>`).
   Điều này chỉ xảy ra khi event là một :ref:`InputEventKey <class_InputEventKey>`. Nếu bất kỳ hàm nào tiêu thụ event, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và event sẽ không lan truyền thêm. Callback unhandled key input rất phù hợp cho các event phím. 7. Nếu đến thời điểm này vẫn chưa có thành phần nào tiêu thụ event, callback :ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>` sẽ được gọi nếu được override (và không bị vô hiệu hóa bằng
   :ref:`Node.set_process_unhandled_input() <class_Node_method_set_process_unhandled_input>`).
   Nếu bất kỳ hàm nào tiêu thụ event, hàm đó có thể gọi :ref:`Viewport.set_input_as_handled() <class_Viewport_method_set_input_as_handled>`, và event sẽ không lan truyền thêm. Callback unhandled input rất phù hợp cho các event gameplay toàn màn hình, để chúng không được nhận khi GUI đang hoạt động. 8. Nếu đến thời điểm này không có thành phần nào muốn nhận event và :ref:`Object Picking <class_viewport_property_physics_object_picking>` đang được bật, event sẽ được dùng để picking object. Đối với viewport gốc, tính năng này cũng có thể được bật trong :ref:`Project Settings <class_ProjectSettings_property_physics/common/enable_object_picking>`. Trong trường hợp scene 3D, nếu một :ref:`Camera3D <class_Camera3D>` được gán cho Viewport, một tia đến physics world (theo hướng tia từ điểm nhấp chuột) sẽ được chiếu. Nếu tia này va vào một object, hàm :ref:`CollisionObject3D._input_event() <class_CollisionObject3D_private_method__input_event>` sẽ được gọi trong physics object tương ứng. Trong trường hợp scene 2D, về mặt khái niệm cũng xảy ra điều tương tự với :ref:`CollisionObject2D._input_event() <class_CollisionObject2D_private_method__input_event>`.

Khi gửi event đến các node con và node hậu duệ, viewport sẽ thực hiện việc này như minh họa trong hình sau, theo thứ tự depth-first ngược, bắt đầu từ node ở cuối scene tree và kết thúc ở node gốc. Windows và SubViewports không tham gia vào quá trình này.

.. image:: img/input_event_scene_flow.webp

.. note::

   Thứ tự này không áp dụng cho :ref:`Control._gui_input() <class_Control_private_method__gui_input>`, vốn sử dụng một phương thức khác dựa trên vị trí của event hoặc Control đang được focus. Các event **mouse** của GUI cũng di chuyển lên scene tree, tuân theo các hạn chế :ref:`Control.mouse_filter <class_Control_property_mouse_filter>` được mô tả ở trên. Tuy nhiên, vì các event này nhắm đến những Control cụ thể, chỉ các ancestor trực tiếp của node Control đích mới nhận được event. Các event **keyboard and joypad** của GUI *không* di chuyển lên scene tree và chỉ có thể được xử lý bởi Control đã nhận chúng. Nếu không, chúng sẽ được truyền đi dưới dạng event không thuộc GUI thông qua :ref:`Node._unhandled_input() <class_Node_private_method__unhandled_input>`.

Vì Viewport không gửi event đến các :ref:`SubViewports <class_SubViewport>` khác, nên phải sử dụng một trong các phương thức sau:

1. Sử dụng một :ref:`SubViewportContainer <class_SubViewportContainer>`, tự động gửi event đến :ref:`SubViewports <class_SubViewport>` con của nó sau
   :ref:`Node._input() <class_Node_private_method__input>` or :ref:`Control._gui_input() <class_Control_private_method__gui_input>`.
2. Triển khai việc truyền event dựa trên các yêu cầu riêng.

Phù hợp với thiết kế dựa trên node của Godot, cơ chế này cho phép các node con chuyên biệt xử lý và tiêu thụ những event cụ thể, trong khi các ancestor của chúng và cuối cùng là scene root có thể cung cấp hành vi tổng quát hơn khi cần.

Cấu tạo của InputEvent
----------------------

:ref:`InputEvent <class_InputEvent>` is just a base built-in type, it does not represent
bất kỳ thứ gì và chỉ chứa một số thông tin cơ bản, chẳng hạn như event ID (được tăng lên sau mỗi event), device index, v.v.

Có một số kiểu InputEvent chuyên biệt, được mô tả trong bảng dưới đây:

+-------------------------------------------------------------------+-----------------------------------------+
| Event                                                             | Description                             |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEvent <class_InputEvent>`                              | Empty Input Event.                      |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventKey <class_InputEventKey>`                        | Contains a keycode and Unicode value,   |
|                                                                   | as well as modifiers.                   |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventMouseButton <class_InputEventMouseButton>`        | Contains click information, such as     |
|                                                                   | button, modifiers, etc.                 |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventMouseMotion <class_InputEventMouseMotion>`        | Contains motion information, such as    |
|                                                                   | relative and absolute positions and     |
|                                                                   | speed.                                  |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventJoypadMotion <class_InputEventJoypadMotion>`      | Contains Joystick/Joypad analog axis    |
|                                                                   | information.                            |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventJoypadButton <class_InputEventJoypadButton>`      | Contains Joystick/Joypad button         |
|                                                                   | information.                            |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventScreenTouch <class_InputEventScreenTouch>`        | Contains multi-touch press/release      |
|                                                                   | information. (only available on mobile  |
|                                                                   | devices)                                |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventScreenDrag <class_InputEventScreenDrag>`          | Contains multi-touch drag information.  |
|                                                                   | (only available on mobile devices)      |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventMagnifyGesture <class_InputEventMagnifyGesture>`  | Contains a position, a factor as well   |
|                                                                   | as modifiers.                           |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventPanGesture <class_InputEventPanGesture>`          | Contains a position, a delta as well as |
|                                                                   | modifiers.                              |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventMIDI <class_InputEventMIDI>`                      | Contains MIDI-related information.      |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventShortcut <class_InputEventShortcut>`              | Contains a shortcut.                    |
+-------------------------------------------------------------------+-----------------------------------------+
| :ref:`InputEventAction <class_InputEventAction>`                  | Contains a generic action. These events |
|                                                                   | are often generated by the programmer   |
|                                                                   | as feedback. (more on this below)       |
+-------------------------------------------------------------------+-----------------------------------------+

Input actions
-------------

Input actions là nhóm gồm từ 0 InputEvent trở lên, được gắn với một tên gọi dễ hiểu chung (ví dụ: action "ui_left" mặc định, nhóm cả input joypad-left và phím mũi tên trái trên bàn phím). Chúng không bắt buộc phải đại diện cho một InputEvent, nhưng hữu ích vì chúng trừu tượng hóa nhiều input khác nhau khi lập trình logic game.

Điều này cho phép:

-  Cùng một code hoạt động trên các thiết bị khác nhau với các input khác nhau (ví dụ: bàn phím trên PC, Joypad trên console). - Có thể cấu hình lại input trong runtime. - Có thể kích hoạt action theo cách lập trình trong runtime.

Có thể tạo action từ menu Project Settings trong tab **Input Map** và gán các input event cho chúng.

Mọi event đều có các phương thức :ref:`InputEvent.is_action() <class_InputEvent_method_is_action>`,
:ref:`InputEvent.is_pressed() <class_InputEvent_method_is_pressed>` and :ref:`InputEvent.is_echo() <class_InputEvent_method_is_echo>`.

Ngoài ra, bạn có thể muốn cung cấp lại cho game một action từ game code (một ví dụ điển hình là phát hiện gesture). Singleton Input có một phương thức cho việc này:
:ref:`Input.parse_input_event() <class_input_method_parse_input_event>`. You would normally use it like this:

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

   Xem :ref:`doc_first_3d_game_input_actions` để tìm hướng dẫn về cách thêm input actions trong project settings.

InputMap
--------

Việc tùy chỉnh và ánh xạ lại input từ code thường là nhu cầu cần thiết. Nếu toàn bộ workflow của bạn phụ thuộc vào các action, singleton :ref:`InputMap <class_InputMap>` là lựa chọn lý tưởng để gán lại hoặc tạo các action khác nhau trong runtime. Singleton này không được lưu (phải được sửa đổi thủ công) và trạng thái của nó được chạy từ project settings (project.godot). Vì vậy, mọi hệ thống động kiểu này cần lưu trữ các thiết lập theo cách mà lập trình viên cho là phù hợp nhất.
