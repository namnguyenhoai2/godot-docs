.. _doc_viewport_and_canvas_transforms:

Các phép biến đổi viewport và canvas
====================================

Giới thiệu
----------

Đây là phần tổng quan về các phép biến đổi 2D diễn ra đối với các node, từ thời điểm chúng vẽ nội dung cục bộ cho đến khi nội dung được vẽ lên màn hình. Phần tổng quan này đề cập đến các chi tiết rất cấp thấp của engine.

Mục tiêu của hướng dẫn này là hướng dẫn cách truyền các sự kiện đầu vào đến Input với một vị trí trong hệ tọa độ chính xác.

Mô tả chi tiết hơn về tất cả các hệ tọa độ và phép biến đổi 2D có tại :ref:`doc_2d_coordinate_systems`.

Phép biến đổi canvas
--------------------

Như đã đề cập trong hướng dẫn trước, :ref:`doc_canvas_layers`, mọi node CanvasItem (hãy nhớ rằng các node dựa trên Node2D và Control sử dụng CanvasItem làm gốc chung) sẽ nằm trong một *Canvas Layer*. Mỗi canvas layer có một phép biến đổi (tịnh tiến, xoay, co giãn, v.v.) có thể được truy cập dưới dạng :ref:`Transform2D <class_Transform2D>`.

Cũng được đề cập trong hướng dẫn trước, các node theo mặc định được vẽ trong Layer 0, thuộc canvas tích hợp sẵn. Để đặt các node vào một layer khác, có thể sử dụng node :ref:`CanvasLayer <class_CanvasLayer>`.

Phép biến đổi canvas toàn cục
-----------------------------

Các viewport cũng có phép biến đổi Global Canvas (cũng là một
:ref:`Transform2D <class_Transform2D>`). This is the master transform and
ảnh hưởng đến tất cả các phép biến đổi *Canvas Layer* riêng lẻ. Nhìn chung, phép biến đổi này chủ yếu được sử dụng trong CanvasItem Editor của Godot.

Phép biến đổi co giãn
---------------------

Cuối cùng, các viewport có một *Stretch Transform*, được sử dụng khi thay đổi kích thước hoặc co giãn màn hình. Phép biến đổi này được sử dụng nội bộ (như mô tả trong :ref:`doc_multiple_resolutions`), nhưng cũng có thể được thiết lập thủ công trên từng viewport.

Các sự kiện đầu vào được nhân với phép biến đổi này, nhưng không có các phép biến đổi ở trên. Để chuyển đổi tọa độ InputEvent sang tọa độ CanvasItem cục bộ, 
:ref:`CanvasItem.make_input_local() <class_CanvasItem_method_make_input_local>`
hàm đã được thêm vào để thuận tiện.

Phép biến đổi cửa sổ
--------------------

Viewport gốc là một :ref:`Window <class_Window>`. Để co giãn và định vị nội dung của *Window* như mô tả trong :ref:`doc_multiple_resolutions`, mỗi :ref:`Window <class_Window>` chứa một *window transform*. Ví dụ, phép biến đổi này chịu trách nhiệm tạo ra các dải đen ở hai bên của *Window* để *Viewport* được hiển thị với tỷ lệ khung hình cố định.

Thứ tự các phép biến đổi
------------------------

Để chuyển đổi một tọa độ cục bộ của CanvasItem thành tọa độ màn hình thực tế, cần áp dụng chuỗi các phép biến đổi sau:

.. image:: img/viewport_transforms3.webp

Các hàm biến đổi
----------------

Hình minh họa ở trên cho thấy một số hàm biến đổi hiện có. Tất cả các phép biến đổi đều được định hướng từ phải sang trái; điều này có nghĩa là khi nhân một phép biến đổi với một tọa độ, ta thu được một hệ tọa độ nằm xa hơn về bên trái; khi nhân :ref:`affine inverse <class_Transform2D_method_affine_inverse>` của một phép biến đổi, ta thu được một hệ tọa độ nằm xa hơn về bên phải:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Called from a CanvasItem. canvas_pos = get_global_transform() * local_pos local_pos = get_global_transform().affine_inverse() * canvas_pos

 .. code-tab:: csharp

    // Called from a CanvasItem. canvasPos = GetGlobalTransform() * localPos; localPos = GetGlobalTransform().AffineInverse() * canvasPos;

Cuối cùng, để chuyển đổi tọa độ cục bộ của CanvasItem sang tọa độ màn hình, chỉ cần nhân theo thứ tự sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var screen_coord = get_viewport().get_screen_transform() * get_global_transform_with_canvas() * local_pos

 .. code-tab:: csharp

    var screenCoord = GetViewport().GetScreenTransform() * GetGlobalTransformWithCanvas() * localPos;

Tuy nhiên, hãy lưu ý rằng nhìn chung không nên làm việc với tọa độ màn hình. Cách tiếp cận được khuyến nghị là chỉ làm việc trong tọa độ Canvas (``CanvasItem.get_global_transform()``), để việc tự động thay đổi độ phân giải màn hình hoạt động đúng cách.

Truyền các sự kiện đầu vào tùy chỉnh
------------------------------------

Việc truyền các sự kiện đầu vào tùy chỉnh vào game thường là điều cần thiết. Với kiến thức trên, để thực hiện việc này một cách chính xác trong cửa sổ đang được lấy nét, cần làm như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    var local_pos = Vector2(10, 20) # Local to Control/Node2D. var ie = InputEventMouseButton.new() ie.button_index = MOUSE_BUTTON_LEFT ie.position = get_viewport().get_screen_transform() * get_global_transform_with_canvas() * local_pos Input.parse_input_event(ie)

 .. code-tab:: csharp

    var localPos = new Vector2(10,20); // Local to Control/Node2D. var ie = new InputEventMouseButton() { ButtonIndex = MouseButton.Left, Position = GetViewport().GetScreenTransform() * GetGlobalTransformWithCanvas() * localPos, }; Input.ParseInputEvent(ie);
