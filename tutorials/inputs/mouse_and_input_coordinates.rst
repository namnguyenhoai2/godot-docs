.. _doc_mouse_and_input_coordinates:

Tọa độ chuột và tọa độ đầu vào
==============================

Giới thiệu
----------

Mục đích của hướng dẫn ngắn này là làm rõ nhiều lỗi phổ biến về tọa độ đầu vào, cách lấy vị trí chuột và độ phân giải màn hình, v.v.

Tọa độ hiển thị phần cứng
-------------------------

Việc sử dụng tọa độ phần cứng phù hợp khi viết các UI phức tạp предназнач cho PC, chẳng hạn như trình chỉnh sửa, MMO, công cụ, v.v. Tuy nhiên, cách này không phù hợp bằng khi nằm ngoài phạm vi đó.

Tọa độ hiển thị viewport
------------------------

Godot sử dụng viewport để hiển thị nội dung và viewport có thể được scale bằng một số tùy chọn (xem hướng dẫn :ref:`doc_multiple_resolutions`). Vì vậy, hãy sử dụng các hàm trong node để lấy tọa độ chuột và kích thước viewport, ví dụ:

.. tabs::
 .. code-tab:: gdscript GDScript

    func _input(event):
        # Chuột trong tọa độ viewport.
        if event is InputEventMouseButton:
            print("Mouse Click/Unclick at: ", event.position)
        elif event is InputEventMouseMotion:
            print("Mouse Motion at: ", event.position)

        # In kích thước của viewport.
        print("Viewport Resolution is: ", get_viewport().get_visible_rect().size)

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        // Chuột trong tọa độ viewport.
        if (@event is InputEventMouseButton eventMouseButton)
        {
            GD.Print("Mouse Click/Unclick at: ", eventMouseButton.Position);
        }
        else if (@event is InputEventMouseMotion eventMouseMotion)
        {
            GD.Print("Mouse Motion at: ", eventMouseMotion.Position);
        }

        // In kích thước của viewport.
        GD.Print("Viewport Resolution is: ", GetViewport().GetVisibleRect().Size);
    }

Ngoài ra, bạn có thể yêu cầu viewport cung cấp vị trí chuột:

.. tabs::
 .. code-tab:: gdscript GDScript

    get_viewport().get_mouse_position()

 .. code-tab:: csharp

    GetViewport().GetMousePosition();

.. note::

    Khi mouse mode được đặt thành ``Input.MOUSE_MODE_CAPTURED``, giá trị ``event.position`` từ ``InputEventMouseMotion`` là tâm màn hình. Hãy sử dụng ``event.relative`` thay vì ``event.position`` và ``event.velocity`` để xử lý chuyển động chuột và các thay đổi vị trí.

    Khi triển khai các tính năng như mouselook, bạn nên sử dụng ``event.screen_relative`` và ``event.screen_velocity`` thay vì ``event.relative`` và ``event.velocity`` để chuyển động chuột hoạt động giống nhau trên
    :ref:`nhiều độ phân giải <doc_multiple_resolutions>`.
