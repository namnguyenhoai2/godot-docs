:article_outdated: True

.. _doc_custom_gui_controls:

Các control GUI tùy chỉnh
=========================

Có quá nhiều control...
-----------------------

Tuy vậy, chúng vẫn không bao giờ đủ. Việc tạo các control tùy chỉnh của riêng bạn, hoạt động chính xác theo cách bạn muốn, là một nỗi ám ảnh của hầu hết mọi lập trình viên GUI. Godot cung cấp rất nhiều control, nhưng chúng có thể không hoạt động chính xác theo cách bạn muốn. Trước khi liên hệ với các nhà phát triển bằng một pull request để hỗ trợ thanh cuộn chéo, ít nhất bạn cũng nên biết cách dễ dàng tạo các control này từ script.

Vẽ
---

Để vẽ, bạn nên xem tutorial :ref:`doc_custom_drawing_in_2d`. Điều tương tự cũng được áp dụng. Một số hàm đáng được đề cập vì tính hữu ích của chúng khi vẽ, nên sẽ được trình bày chi tiết dưới đây:

Kiểm tra kích thước của control
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Không giống các node 2D, "size" rất quan trọng đối với control, vì nó giúp sắp xếp chúng trong các layout phù hợp. Vì vậy,
:ref:`Control.size <class_Control_property_size>`
property được cung cấp. Việc kiểm tra nó trong ``_draw()`` là rất quan trọng để đảm bảo mọi thứ luôn nằm trong giới hạn.

Kiểm tra focus
~~~~~~~~~~~~~~

Một số control (chẳng hạn như button hoặc trình soạn thảo văn bản) có thể cung cấp input focus cho input từ bàn phím hoặc joypad. Ví dụ về việc này là nhập văn bản hoặc nhấn một button. Điều này được kiểm soát bằng
:ref:`Control.focus_mode <class_Control_property_focus_mode>`
property. Khi vẽ, nếu control hỗ trợ input focus, bạn luôn nên hiển thị một dạng chỉ báo nào đó (vùng highlight, hộp, v.v.) để cho biết đây là control hiện đang được focus. Để kiểm tra trạng thái này, phương thức :ref:`Control.has_focus() <class_Control_method_has_focus>` tồn tại. Ví dụ

.. tabs::
 .. code-tab:: gdscript GDScript

    func _draw():
        if has_focus():
             draw_selected()
        else:
             draw_normal()

 .. code-tab:: csharp

    public override void _Draw()
    {
        if (HasFocus())
        {
            DrawSelected()
        }
        else
        {
            DrawNormal();
        }
    }

Định kích thước
---------------

Như đã đề cập trước đó, size rất quan trọng đối với control. Điều này cho phép chúng được bố trí đúng cách khi đặt vào grid, container hoặc sử dụng anchor. Hầu hết thời gian, control cung cấp một *kích thước tối thiểu* để giúp bố trí chúng đúng cách. Ví dụ, nếu các control được đặt theo chiều dọc chồng lên nhau bằng một :ref:`VBoxContainer <class_VBoxContainer>`, kích thước tối thiểu sẽ đảm bảo control tùy chỉnh của bạn không bị các control khác trong container ép nhỏ lại.

Để cung cấp callback này, chỉ cần override
:ref:`Control._get_minimum_size() <class_Control_private_method__get_minimum_size>`,
ví dụ:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _get_minimum_size():
        return Vector2(30, 30)

 .. code-tab:: csharp

    public override Vector2 _GetMinimumSize()
    {
        return new Vector2(20, 20);
    }

Ngoài ra, hãy thiết lập nó bằng một function:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        set_custom_minimum_size(Vector2(30, 30))

 .. code-tab:: csharp

    public override void _Ready()
    {
        CustomMinimumSize = new Vector2(20, 20);
    }

Input
-----

Control cung cấp một số helper giúp việc quản lý các sự kiện input dễ dàng hơn nhiều so với các node thông thường.

Các sự kiện input
~~~~~~~~~~~~~~~~~

Có một vài tutorial về input trước tutorial này, nhưng cần lưu ý rằng control có một phương thức input đặc biệt chỉ hoạt động khi:

-  Con trỏ chuột đang ở trên control. - Button được nhấn trên control này (control luôn bắt input cho đến khi button được nhả ra) - Control cung cấp focus cho bàn phím/joypad thông qua
   :ref:`Control.focus_mode <class_Control_property_focus_mode>`.

Hàm này là
:ref:`Control._gui_input() <class_Control_private_method__gui_input>`.
Để sử dụng, hãy override nó trong control của bạn. Không cần thiết lập processing.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Control

    func _gui_input(event):
       if event is InputEventMouseButton and event.button_index == MOUSE_BUTTON_LEFT and event.pressed:
           print("Left mouse button was pressed!")

 .. code-tab:: csharp

    public override void _GuiInput(InputEvent @event)
    {
        if (@event is InputEventMouseButton mbe && mbe.ButtonIndex == MouseButton.Left && mbe.Pressed)
        {
            GD.Print("Left mouse button was pressed!");
        }
    }

Để biết thêm thông tin về bản thân các event, hãy xem tutorial :ref:`doc_inputevent`.

Notification
~~~~~~~~~~~~

Control cũng có nhiều notification hữu ích không có callback chuyên dụng, nhưng có thể được kiểm tra bằng callback _notification:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _notification(what):
        match what:
            NOTIFICATION_MOUSE_ENTER:
                pass # Chuột đi vào vùng của control này.
            NOTIFICATION_MOUSE_EXIT:
                pass # Chuột rời khỏi vùng của control này.
            NOTIFICATION_FOCUS_ENTER:
                pass # Control nhận focus.
            NOTIFICATION_FOCUS_EXIT:
                pass # Control mất focus.
            NOTIFICATION_THEME_CHANGED:
                pass # Theme dùng để vẽ control đã thay đổi;
                # khuyến nghị cập nhật và vẽ lại nếu đang sử dụng theme.
            NOTIFICATION_VISIBILITY_CHANGED:
                pass # Control trở nên hiển thị/ẩn;
                # kiểm tra trạng thái mới bằng is_visible().
            NOTIFICATION_RESIZED:
                pass # Control đã thay đổi kích thước; kiểm tra kích thước mới
                # bằng get_size().
            NOTIFICATION_MODAL_CLOSE:
                pass # Đối với các cửa sổ bật lên modal, notification
                # cho biết cửa sổ bật lên đã được đóng.

 .. code-tab:: csharp

    public override void _Notification(int what)
    {
        switch (what)
        {
            case NotificationMouseEnter:
                // Chuột đi vào vùng của control này.
                break;

            case NotificationMouseExit:
                // Chuột rời khỏi vùng của control này.
                break;

            case NotificationFocusEnter:
                // Control nhận focus.
                break;

            case NotificationFocusExit:
                // Control mất focus.
                break;

            case NotificationThemeChanged:
                // Theme dùng để vẽ control đã thay đổi;
                // khuyến nghị cập nhật và vẽ lại nếu đang sử dụng theme.
                break;

            case NotificationVisibilityChanged:
                // Control trở nên hiển thị/ẩn;
                // kiểm tra trạng thái mới bằng is_visible().
                break;

            case NotificationResized:
                // Control đã thay đổi kích thước; kiểm tra kích thước mới bằng get_size().
                break;

            case NotificationModalClose:
                // Đối với các cửa sổ bật lên modal, notification cho biết cửa sổ bật lên đã được đóng.
                break;
        }
    }
