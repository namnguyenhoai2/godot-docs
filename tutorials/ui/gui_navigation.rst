.. _doc_gui_navigation:

Điều hướng và tiêu điểm bằng bàn phím/tay cầm
=============================================

Một yêu cầu phổ biến đối với giao diện người dùng là hỗ trợ đầy đủ bàn phím và tay cầm cho việc điều hướng và tương tác. Điều này mang lại lợi ích cho dự án vì hai lý do chính: cải thiện khả năng truy cập (không phải ai cũng có thể sử dụng chuột hoặc điều khiển cảm ứng để tương tác) và giúp dự án sẵn sàng cho các hệ máy console (hoặc chỉ đơn giản là phục vụ những người thích chơi game bằng tay cầm trên PC).

Việc điều hướng giữa các phần tử UI bằng bàn phím hoặc tay cầm được thực hiện bằng cách thay đổi node đang được chọn. Đây cũng được gọi là thay đổi focus của UI. Mọi node :ref:`Control <class_Control>` trong Godot đều có thể nhận focus. Theo mặc định, một số node Control có khả năng tự động nhận focus khi phản hồi các UI action tích hợp như ``ui_up``, ``ui_down``, ``ui_focus_next``, v.v. Bạn có thể xem các action này trong project settings, tại input map, và chỉnh sửa chúng.

.. warning::

    Vì các action này được dùng cho focus, bạn không nên sử dụng chúng trong bất kỳ code gameplay nào.

Thiết lập node
--------------

Ngoài logic tích hợp, bạn có thể xác định các focus neighbor cho từng node Control riêng lẻ. Điều này cho phép tinh chỉnh đường đi của UI focus trên giao diện người dùng của dự án. Bạn có thể tìm thấy thiết lập cho từng node trong dock Inspector, bên dưới danh mục "Focus" của phần "Control".

.. image:: img/focus_settings.png

Các tùy chọn neighbor được dùng để xác định node cho việc điều hướng 4 hướng, chẳng hạn như sử dụng các phím mũi tên hoặc D-pad trên tay cầm. Ví dụ, bottom neighbor sẽ được sử dụng khi điều hướng xuống bằng phím mũi tên xuống hoặc khi nhấn xuống trên D-pad. Các tùy chọn "Next" và "Previous" được dùng với nút chuyển focus, chẳng hạn như :kbd:`Tab` trên các hệ điều hành máy tính để bàn.

.. note::
    Một node có thể mất focus nếu bị ẩn.

Thiết lập mode xác định cách một node có thể nhận focus. **All** nghĩa là node có thể nhận focus bằng cách nhấp vào node bằng chuột hoặc chọn node bằng bàn phím hay tay cầm. **Click** nghĩa là node chỉ có thể nhận focus bằng cách nhấp vào. Cuối cùng, **None** nghĩa là node hoàn toàn không thể nhận focus. Các node Control khác nhau có thiết lập mặc định khác nhau dựa trên cách chúng thường được sử dụng; chẳng hạn, các node :ref:`Label <class_Label>` mặc định được đặt thành "None", trong khi :ref:`buttons <class_Button>` được đặt thành "All".

Hãy bảo đảm cấu hình đúng các scene để hỗ trợ focus và điều hướng. Nếu một node chưa được cấu hình focus neighbor, engine sẽ tự động cố gắng đoán control tiếp theo. Điều này có thể dẫn đến hành vi ngoài ý muốn, đặc biệt trong một giao diện người dùng phức tạp không có luồng điều hướng dọc hoặc ngang được xác định rõ ràng.

Code cần thiết
--------------

Để việc điều hướng bằng bàn phím và tay cầm hoạt động chính xác, bất kỳ node nào cũng phải được focus bằng code khi scene bắt đầu. Nếu không thực hiện điều này, việc nhấn các nút hoặc phím sẽ không có tác dụng.

Bạn có thể sử dụng phương thức :ref:`Control.grab_focus() <class_Control_method_grab_focus>` để focus một Control. Sau đây là ví dụ cơ bản về cách thiết lập focus ban đầu bằng code:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        $StartButton.grab_focus.call_deferred()

 .. code-tab:: csharp

    public override void _Ready()
    {
        GetNode<Button>("StartButton").GrabFocus.CallDeferred();
    }

Khi scene bắt đầu, node "Start Button" sẽ được focus, và bạn có thể sử dụng bàn phím hoặc tay cầm để điều hướng giữa node này với các phần tử UI khác.
