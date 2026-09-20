.. _doc_custom_mouse_cursor:

Tùy chỉnh con trỏ chuột
=======================

Bạn có thể muốn thay đổi giao diện của con trỏ chuột trong game để phù hợp với thiết kế tổng thể. Có hai cách để tùy chỉnh con trỏ chuột:

1. Sử dụng cài đặt dự án. Cách này đơn giản hơn nhưng bị giới hạn hơn. 2. Sử dụng script. Cách này có nhiều tùy chỉnh hơn nhưng yêu cầu viết script.

.. note::

    Bạn có thể hiển thị con trỏ chuột "software" bằng cách ẩn con trỏ chuột và di chuyển một Sprite2D đến vị trí con trỏ trong phương thức ``_process()``, nhưng cách này sẽ tạo ra độ trễ ít nhất một frame so với con trỏ chuột "hardware". Do đó, bạn nên sử dụng phương pháp được mô tả ở đây bất cứ khi nào có thể.

    Nếu phải sử dụng phương pháp "software", hãy cân nhắc thêm một bước ngoại suy để hiển thị chính xác hơn dữ liệu đầu vào thực tế từ chuột.

Sử dụng cài đặt dự án
---------------------

Mở **Project Settings** và đi tới **Display > Mouse Cursor**. Bạn sẽ thấy các cài đặt
:ref:`Custom Image <class_ProjectSettings_property_display/mouse_cursor/custom_image>`,
:ref:`Custom Image Hotspot <class_ProjectSettings_property_display/mouse_cursor/custom_image_hotspot>`,
và :ref:`Tooltip Position Offset <class_ProjectSettings_property_display/mouse_cursor/tooltip_position_offset>`.

.. image:: img/cursor_project_settings.webp

**Custom Image** là hình ảnh bạn muốn đặt làm con trỏ chuột. **Custom Hotspot** là điểm trong hình ảnh mà bạn muốn sử dụng làm điểm phát hiện của con trỏ.

.. warning::

    Hình ảnh tùy chỉnh **phải** có kích thước tối đa là 256×256 pixel. Để tránh các vấn đề khi kết xuất, nên sử dụng kích thước 128×128 hoặc nhỏ hơn.

    Trên nền tảng web, kích thước hình ảnh con trỏ tối đa được cho phép là 128×128.

Sử dụng script
--------------

Tạo một Node và gắn script sau vào đó.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node


    # Tải các hình ảnh tùy chỉnh cho con trỏ chuột.
    var arrow = load("res://arrow.png")
    var beam = load("res://beam.png")


    func _ready():
        # Chỉ thay đổi hình dạng mũi tên của con trỏ.
        # Tương tự như khi thay đổi trong cài đặt dự án.
        Input.set_custom_mouse_cursor(arrow)

        # Thay đổi một hình dạng cụ thể của con trỏ (ở đây là hình dạng I-beam).
        Input.set_custom_mouse_cursor(beam, Input.CURSOR_IBEAM)

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode : Node
    {
        public override void _Ready()
        {
            // Tải các hình ảnh tùy chỉnh cho con trỏ chuột.
            var arrow = ResourceLoader.Load("res://arrow.png");
            var beam = ResourceLoader.Load("res://beam.png");

            // Chỉ thay đổi hình dạng mũi tên của con trỏ.
            // Tương tự như khi thay đổi trong cài đặt dự án.
            Input.SetCustomMouseCursor(arrow);

            // Thay đổi một hình dạng cụ thể của con trỏ (ở đây là hình dạng I-beam).
            Input.SetCustomMouseCursor(beam, Input.CursorShape.Ibeam);
        }
    }

.. seealso::

    Xem tài liệu của :ref:`Input.set_custom_mouse_cursor() <class_Input_method_set_custom_mouse_cursor>` để biết thêm thông tin về cách sử dụng và những điểm cần lưu ý riêng theo từng nền tảng.

Danh sách con trỏ
-----------------

Bạn có thể định nghĩa nhiều con trỏ chuột, được ghi lại trong
:ref:`Input.CursorShape <enum_Input_CursorShape>` enum. Which ones you want to use
tùy thuộc vào trường hợp sử dụng của bạn.
