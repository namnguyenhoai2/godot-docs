.. _doc_introduction_to_editor_development:

Giới thiệu về phát triển trình chỉnh sửa
========================================

Trên trang này, bạn sẽ tìm hiểu:

- **Các quyết định thiết kế** đằng sau trình chỉnh sửa Godot. - Cách làm việc hiệu quả với mã C++ của trình chỉnh sửa Godot.

Hướng dẫn này dành cho những người đang hoặc sẽ đóng góp cho engine. Để tạo plugin trình chỉnh sửa bằng GDScript, hãy xem :ref:`doc_making_plugins`.

.. seealso::

    Nếu bạn mới làm quen với Godot, chúng tôi khuyên bạn nên đọc
    :ref:`doc_godot_design_philosophy` before continuing. Since the Godot editor
    là một dự án Godot được viết bằng C++, nên phần lớn triết lý của engine cũng được áp dụng cho trình chỉnh sửa.

Các lựa chọn kỹ thuật
---------------------

Trình chỉnh sửa Godot được vẽ bằng trình kết xuất của Godot và
:ref:`UI system <doc_user_interface>`. It does *not* rely on a toolkit
chẳng hạn như GTK hoặc Qt. Xét về tinh thần, cách này tương tự các phần mềm như Blender. Mặc dù việc sử dụng các bộ công cụ giúp dễ đạt được giao diện "bản địa" hơn, chúng cũng khá nặng và giấy phép của chúng không tương thích với Godot.

Trình chỉnh sửa được viết hoàn toàn bằng C++. Nó không thể chứa mã GDScript hoặc C#.

Cấu trúc thư mục
----------------

Mã của trình chỉnh sửa được chứa hoàn toàn trong thư mục `editor/ <https://github.com/godotengine/godot/tree/master/editor>`__ của kho mã nguồn Godot.

Một số chức năng của trình chỉnh sửa cũng được triển khai thông qua
:ref:`modules <doc_custom_modules_in_cpp>`. Some of these are only enabled in
các bản dựng của trình chỉnh sửa để giảm kích thước nhị phân của các mẫu xuất. Hãy xem thư mục `modules/ <https://github.com/godotengine/godot/tree/master/modules>`__ trong kho mã nguồn Godot.

Một số tệp quan trọng trong trình chỉnh sửa là:

- `editor/editor_node.cpp <https://github.com/godotengine/godot/blob/master/editor/editor_node.cpp>`__: Tệp khởi tạo chính của trình chỉnh sửa. Về cơ bản là "cảnh chính" của trình chỉnh sửa. - `editor/project_manager/project_manager.cpp <https://github.com/godotengine/godot/blob/master/editor/project_manager/project_manager.cpp>`__: Tệp khởi tạo chính của Project Manager. Về cơ bản là "cảnh chính" của Project Manager. - `editor/scene/canvas_item_editor_plugin.cpp <https://github.com/godotengine/godot/blob/master/editor/scene/canvas_item_editor_plugin.cpp>`__: Khung nhìn trình chỉnh sửa 2D và các chức năng liên quan (thanh công cụ ở trên cùng, các chế độ chỉnh sửa, các trình trợ giúp/bảng phủ lên, …). - `editor/scene/3d/node_3d_editor_plugin.cpp <https://github.com/godotengine/godot/blob/master/editor/scene/3d/node_3d_editor_plugin.cpp>`__: Khung nhìn trình chỉnh sửa 3D và các chức năng liên quan (thanh công cụ ở trên cùng, các chế độ chỉnh sửa, các bảng phủ lên, …). - `editor/scene/3d/node_3d_editor_gizmos.cpp <https://github.com/godotengine/godot/blob/master/editor/scene/3d/node_3d_editor_gizmos.cpp>`__: Nơi các gizmo của trình chỉnh sửa 3D được định nghĩa và vẽ. Tệp này không có bản tương ứng cho 2D vì các gizmo 2D được chính các node vẽ.

Các dependency của trình chỉnh sửa trong các tệp ``scene/``
-----------------------------------------------------------

Khi làm việc trên một tính năng của trình chỉnh sửa, bạn có thể phải chỉnh sửa các tệp trong các node GUI của Godot, nằm trong thư mục ``scene/``.

Một quy tắc cần ghi nhớ là bạn **không được** thêm các dependency mới đến các include của ``editor/`` trong những thư mục khác như ``scene/``. Quy tắc này vẫn áp dụng ngay cả khi bạn sử dụng ``#ifdef TOOLS_ENABLED``.

Để cơ sở mã dễ theo dõi và tự chứa hơn, thứ tự dependency được phép là:

- ``editor/`` -> ``scene/`` -> ``servers/`` -> ``core/``

Điều này có nghĩa là các tệp trong ``editor/`` có thể phụ thuộc vào các include từ ``scene/``, ``servers/`` và ``core/``. Tuy nhiên, ví dụ, mặc dù ``scene/`` có thể phụ thuộc vào các include từ ``servers/`` và ``core/``, nó không thể phụ thuộc vào các include từ ``editor/``.

Hiện tại, có một số dependency đến các include của ``editor/`` trong các tệp ``scene/``, nhưng `chúng đang được loại bỏ <https://github.com/godotengine/godot/issues/53295>`__.

Mẹo phát triển
--------------

Để nhanh chóng lặp lại quá trình phát triển trình chỉnh sửa, chúng tôi khuyên bạn thiết lập một dự án kiểm thử và
:ref:`open it from the command line <doc_command_line_tutorial>` after compiling
trình chỉnh sửa. Bằng cách này, bạn không phải đi qua Project Manager mỗi khi khởi động Godot.
