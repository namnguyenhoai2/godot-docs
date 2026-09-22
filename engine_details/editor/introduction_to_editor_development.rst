.. _doc_introduction_to_editor_development:

Giới thiệu về phát triển editor
===============================

Trong trang này, bạn sẽ tìm hiểu:

- Các **quyết định thiết kế** đằng sau editor của Godot.
- Cách làm việc hiệu quả với mã C++ của editor Godot.

Hướng dẫn này dành cho những người hiện đang hoặc sẽ đóng góp cho engine. Để tạo các plugin cho editor bằng GDScript, hãy xem :ref:`doc_making_plugins` thay vào đó.

.. seealso::

    Nếu bạn mới làm quen với Godot, chúng tôi khuyến nghị bạn đọc
    :ref:`doc_godot_design_philosophy` trước khi tiếp tục. Vì editor Godot là một project Godot được viết bằng C++, phần lớn triết lý của engine cũng được áp dụng cho editor.

Các lựa chọn kỹ thuật
---------------------

Editor Godot được dựng bằng renderer của Godot và
hệ thống :ref:`UI <doc_user_interface>`. Nó *không* phụ thuộc vào toolkit như GTK hoặc Qt. Điều này tương tự về mặt ý tưởng với các phần mềm như Blender. Mặc dù sử dụng toolkit giúp dễ đạt được giao diện "native" hơn, chúng cũng khá nặng và giấy phép của chúng không tương thích với giấy phép của Godot.

Editor được viết hoàn toàn bằng C++. Nó không thể chứa mã GDScript hoặc C#.

Cấu trúc thư mục
----------------

Mã của editor được chứa hoàn toàn trong thư mục `editor/ <https://github.com/godotengine/godot/tree/master/editor>`__ của repository mã nguồn Godot.

Một số chức năng của editor cũng được triển khai thông qua
:ref:`modules <doc_custom_modules_in_cpp>`. Một số module trong đó chỉ được bật trong các bản build của editor để giảm kích thước binary của các export template. Hãy xem thư mục `modules/ <https://github.com/godotengine/godot/tree/master/modules>`__ trong repository mã nguồn Godot.

Một số tệp quan trọng trong editor gồm:

- `editor/editor_node.cpp <https://github.com/godotengine/godot/blob/master/editor/editor_node.cpp>`__: Tệp khởi tạo editor chính. Về cơ bản là "cảnh chính" của editor.
- `editor/project_manager/project_manager.cpp <https://github.com/godotengine/godot/blob/master/editor/project_manager/project_manager.cpp>`__: Tệp khởi tạo Project Manager chính. Về cơ bản là "cảnh chính" của Project Manager.
- `editor/scene/canvas_item_editor_plugin.cpp <https://github.com/godotengine/godot/blob/master/editor/scene/canvas_item_editor_plugin.cpp>`__: Viewport editor 2D và các chức năng liên quan (thanh công cụ ở trên cùng, các chế độ chỉnh sửa, các trình trợ giúp/panel phủ lên trên, …).
- `editor/scene/3d/node_3d_editor_plugin.cpp <https://github.com/godotengine/godot/blob/master/editor/scene/3d/node_3d_editor_plugin.cpp>`__: Viewport editor 3D và các chức năng liên quan (thanh công cụ ở trên cùng, các chế độ chỉnh sửa, các panel phủ lên trên, …).
- `editor/scene/3d/node_3d_editor_gizmos.cpp <https://github.com/godotengine/godot/blob/master/editor/scene/3d/node_3d_editor_gizmos.cpp>`__: Nơi định nghĩa và vẽ các gizmo của editor 3D. Tệp này không có phiên bản tương ứng cho 2D vì các gizmo 2D được chính các node vẽ.

Các dependency của editor trong các tệp ``scene/``
--------------------------------------------------

Khi làm việc trên một tính năng của editor, bạn có thể phải chỉnh sửa các tệp trong các GUI node của Godot, nằm trong thư mục ``scene/``.

Một quy tắc cần ghi nhớ là bạn **không** được thêm dependency mới vào các include ``editor/`` trong những thư mục khác như ``scene/``. Quy tắc này vẫn áp dụng ngay cả khi bạn sử dụng ``#ifdef TOOLS_ENABLED``.

Để giúp codebase dễ theo dõi và tự chứa hơn, thứ tự dependency được cho phép là:

- ``editor/`` -> ``scene/`` -> ``servers/`` -> ``core/``

Điều này có nghĩa là các tệp trong ``editor/`` có thể phụ thuộc vào các include từ ``scene/``, ``servers/`` và ``core/``. Tuy nhiên, chẳng hạn như ``scene/`` có thể phụ thuộc vào các include từ ``servers/`` và ``core/``, nhưng không thể phụ thuộc vào các include từ ``editor/``.

Hiện tại, có một số dependency đến các include ``editor/`` trong các tệp ``scene/``, nhưng `chúng đang trong quá trình được loại bỏ <https://github.com/godotengine/godot/issues/53295>`__.

Mẹo phát triển
--------------

Để nhanh chóng lặp lại quá trình phát triển editor, chúng tôi khuyến nghị thiết lập một project thử nghiệm và
:ref:`mở project đó từ dòng lệnh <doc_command_line_tutorial>` sau khi biên dịch editor. Nhờ vậy, bạn không phải đi qua Project Manager mỗi lần khởi động Godot.
