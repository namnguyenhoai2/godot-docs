.. _doc_gdscript_warning_system:

Hệ thống cảnh báo của GDScript
==============================

Hệ thống cảnh báo của GDScript bổ trợ cho :ref:`static typing <doc_gdscript_static_typing>` (nhưng cũng có thể hoạt động mà không cần kiểu tĩnh). Hệ thống này giúp bạn tránh những lỗi khó phát hiện trong quá trình phát triển và có thể dẫn đến lỗi runtime.

Bạn có thể cấu hình các cảnh báo trong Project Settings, tại mục có tên **GDScript**:

.. image:: img/typed_gdscript_warning_system_settings.webp

.. note::
   Bạn phải bật **Advanced Settings** để thấy mục GDScript trong thanh bên. Bạn cũng có thể tìm kiếm "GDScript" khi Advanced Settings đang tắt.

Bạn có thể tìm thấy danh sách các cảnh báo cho tệp GDScript đang hoạt động trên thanh trạng thái của trình soạn thảo script. Ví dụ dưới đây có 2 cảnh báo:

.. image:: img/typed_gdscript_warning_example.webp

Để bỏ qua từng cảnh báo riêng lẻ trong một tệp, hãy sử dụng
:ref:`@warning_ignore <class_@GDScript_annotation_@warning_ignore>` annotation.
Bạn có thể nhấp vào liên kết ignore ở bên trái phần mô tả cảnh báo. Godot sẽ thêm một annotation phía trên dòng tương ứng và mã sẽ không còn kích hoạt cảnh báo tương ứng nữa:

.. image:: img/typed_gdscript_warning_system_ignore.webp

Để bỏ qua nhiều cảnh báo trong một vùng của tệp, hãy sử dụng
:ref:`@warning_ignore_start <class_@GDScript_annotation_@warning_ignore_start>`
và các annotation :ref:`@warning_ignore_restore <class_@GDScript_annotation_@warning_ignore_restore>`. Bạn có thể bỏ qua ``@warning_ignore_restore`` nếu muốn bỏ qua các loại cảnh báo được chỉ định cho đến hết tệp.

Tên của các cảnh báo cần bỏ qua trùng với tên của các thiết lập dự án. Ví dụ: để bỏ qua cảnh báo được cấu hình bởi
:ref:`debug/gdscript/warnings/unused_variable <class_ProjectSettings_property_debug/gdscript/warnings/unused_variable>`
thiết lập dự án, hãy sử dụng ``@warning_ignore("unused_variable")``. Một hộp thoại tự động hoàn thành sẽ hiển thị khi nhập tên cảnh báo trong annotation, liệt kê tất cả các cảnh báo khả dụng.

Các cảnh báo sẽ không ngăn trò chơi chạy, nhưng bạn có thể chuyển chúng thành lỗi nếu muốn. Theo cách này, trò chơi sẽ không biên dịch trừ khi bạn sửa tất cả cảnh báo. Hãy đi đến mục ``GDScript`` trong Project Settings để bật tùy chọn này cho cảnh báo mà bạn muốn. Dưới đây là cùng tệp với ví dụ trước, trong đó cảnh báo ``unused_variable`` đã được bật dưới dạng lỗi:

.. image:: img/typed_gdscript_warning_system_errors.webp
