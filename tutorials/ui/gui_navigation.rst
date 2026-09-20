.. _doc_gui_navigation:

Điều hướng và lấy focus bằng Bàn phím/Controller
================================================

Một yêu cầu phổ biến đối với giao diện người dùng là phải hỗ trợ đầy đủ bàn phím và controller cho việc điều hướng và tương tác. Có hai lý do chính khiến điều này mang lại lợi ích cho các project: cải thiện khả năng accessibility (không phải ai cũng có thể sử dụng chuột hoặc thao tác cảm ứng để tương tác), và giúp project sẵn sàng cho console (hoặc đơn giản là phục vụ những người thích chơi game bằng controller trên PC).

Việc điều hướng giữa các phần tử UI bằng bàn phím hoặc controller được thực hiện bằng cách thay đổi node nào đang được chọn. Thao tác này còn được gọi là thay đổi UI focus. Mọi node :ref:`Control <class_Control>` trong Godot đều có khả năng nhận focus. Theo mặc định, một số control node có khả năng tự động lấy focus khi phản hồi các UI action tích hợp sẵn như ``ui_up``, ``ui_down``, ``ui_focus_next``, v.v. Bạn có thể xem các action này trong project settings, tại input map, và sửa đổi chúng.

.. warning::

    Vì các action này được dùng cho focus, không nên sử dụng chúng cho bất kỳ gameplay code nào.

Cài đặt node
------------

Ngoài logic tích hợp sẵn, bạn có thể định nghĩa thứ được gọi là focus neighbor cho từng control node riêng lẻ. Điều này cho phép tinh chỉnh chính xác đường đi của UI focus trong giao diện người dùng của project. Bạn có thể tìm thấy các cài đặt cho từng node trong Inspector dock, dưới danh mục "Focus" của phần "Control".

.. image:: img/focus_settings.png

Các tùy chọn neighbor được dùng để định nghĩa node cho việc điều hướng 4 hướng, chẳng hạn như sử dụng các phím mũi tên hoặc D-pad trên controller. Ví dụ, bottom neighbor sẽ được sử dụng khi điều hướng xuống bằng phím mũi tên xuống hoặc khi nhấn xuống trên D-pad. Các tùy chọn "Next" và "Previous" được sử dụng với nút chuyển focus, chẳng hạn như :kbd:`Tab` trên các hệ điều hành desktop.

.. note::
    Một node có thể mất focus nếu bị ẩn.

Cài đặt mode xác định cách một node có thể nhận focus. **All** nghĩa là node có thể nhận focus bằng cách nhấp vào nó bằng chuột hoặc chọn nó bằng bàn phím hay controller. **Click** nghĩa là node chỉ có thể nhận focus bằng cách nhấp vào nó. Cuối cùng, **None** nghĩa là node hoàn toàn không thể nhận focus. Các control node khác nhau có cài đặt mặc định khác nhau tùy theo cách chúng thường được sử dụng; ví dụ, các node :ref:`Label <class_Label>` được đặt thành "None" theo mặc định, trong khi :ref:`buttons <class_Button>` được đặt thành "All".

Hãy đảm bảo cấu hình đúng các scene cho focus và điều hướng. Nếu một node chưa được cấu hình focus neighbor, engine sẽ cố gắng tự động đoán control tiếp theo. Điều này có thể dẫn đến hành vi ngoài ý muốn, đặc biệt trong một giao diện người dùng phức tạp không có luồng điều hướng dọc hoặc ngang được xác định rõ ràng.

Code cần thiết
--------------

Để việc điều hướng bằng bàn phím và controller hoạt động chính xác, bất kỳ node nào cũng phải được focus bằng code khi scene bắt đầu. Nếu không thực hiện việc này, thao tác nhấn nút hoặc phím sẽ không có tác dụng.

Bạn có thể sử dụng method :ref:`Control.grab_focus() <class_Control_method_grab_focus>` để focus một control. Dưới đây là ví dụ cơ bản về cách thiết lập focus ban đầu bằng code:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        $StartButton.grab_focus.call_deferred()

 .. code-tab:: csharp

    public override void _Ready()
    {
        GetNode<Button>("StartButton").GrabFocus.CallDeferred();
    }

Khi scene bắt đầu, node "Start Button" sẽ được focus, và có thể sử dụng bàn phím hoặc controller để điều hướng giữa node này với các phần tử UI khác.
