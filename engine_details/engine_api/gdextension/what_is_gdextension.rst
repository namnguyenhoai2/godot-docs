.. _doc_what_is_gdextension:

GDExtension là gì?
==================

**GDExtension** là một công nghệ dành riêng cho Godot, cho phép engine tương tác với các `thư viện dùng chung <https://en.wikipedia.org/wiki/Shared_library>`__ native trong thời gian chạy. Bạn có thể sử dụng công nghệ này để chạy mã native mà không cần biên dịch mã đó cùng với engine.

Có ba phương thức chính để thực hiện việc này:

* ``gdextension_interface.h``: Một tập hợp các hàm C mà Godot và GDExtension có thể sử dụng để giao tiếp với nhau.
* ``extension_api.json``: Một danh sách các hàm C được cung cấp từ các API của Godot (:ref:`Core Features <doc_scripting_core_features>`).
* :ref:`*.gdextension <doc_gdextension_file>`: Định dạng tệp được Godot đọc để tải một GDExtension.

Hầu hết mọi người tạo GDExtension bằng một language binding có sẵn, chẳng hạn như :ref:`godot-cpp (for C++) <doc_godot_cpp>`, hoặc một trong các language binding :ref:`do cộng đồng tạo ra <doc_what_is_gdnative_third_party_bindings>`.

Khả năng tương thích phiên bản
------------------------------

Xem :ref:`godot-cpp Version Compatibility <doc_what_is_gdextension_version_compatibility>`, nội dung này áp dụng cho tất cả GDExtension.
