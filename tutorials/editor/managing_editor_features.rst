:article_outdated: True

.. _doc_managing_editor_features:

Quản lý các tính năng của editor
================================

Giới thiệu
----------

Trong một số tình huống, bạn có thể muốn giới hạn những tính năng được sử dụng trong Godot editor. Ví dụ: một UI designer trong nhóm không cần xem các tính năng 3D, hoặc một giảng viên muốn giới thiệu các tính năng cho học viên theo từng bước. Godot có một hệ thống tích hợp sẵn gọi là "feature profiles" để thực hiện việc này.

Với feature profiles, các tính năng và node chính có thể bị ẩn khỏi editor. Việc này chỉ ẩn một phần giao diện chứ không thực sự xóa hỗ trợ cho các tính năng đó, vì vậy các scene và script phụ thuộc vào những tính năng này vẫn hoạt động bình thường. Điều này cũng có nghĩa là feature profiles không phải là một kỹ thuật tối ưu hóa. Để biết thông tin về cách tối ưu hóa Godot, hãy xem :ref:`doc_performance`.

Tạo profile
-----------

Để quản lý các tính năng của editor, hãy vào **Editor > Manage Editor Features**. Thao tác này sẽ mở cửa sổ **Manage Editor Feature Profiles**. Theo mặc định sẽ không có profile nào. Nhấp vào **Create Profile** và đặt tên cho profile. Sau đó, bạn sẽ thấy danh sách tất cả các tính năng trong Godot editor.

.. image:: img/configure_profile.png

Phần đầu tiên cho phép xóa các tính năng chính của editor, chẳng hạn như 3D editor hoặc scripting editor. Bên dưới các tính năng chính là mọi class và node trong Godot, cũng có thể được vô hiệu hóa. Nhấp vào một node và tất cả thuộc tính cùng tùy chọn của node đó sẽ được liệt kê trong ô **Extra Items**; bạn có thể vô hiệu hóa từng mục riêng lẻ.

.. image:: img/node_features.png

Chia sẻ profile
---------------

Để chia sẻ profile giữa các editor, hãy nhấp vào nút **Export**. Lưu profile tùy chỉnh ở đâu đó dưới dạng tệp ``.profile``. Để sử dụng profile này trong một editor khác, hãy mở cửa sổ **Manage Editor Feature Profiles** của editor đó và nhấp vào import, sau đó chọn tệp ``.profile``.

Tuy nhiên, quy trình này có thể trở nên bất tiện nếu cần áp dụng profile tùy chỉnh cho nhiều máy tính. Một giải pháp thay thế là bật self-contained mode cho Godot, cho phép đặt toàn bộ cấu hình của editor trong cùng thư mục với editor binary. Xem :ref:`doc_data_paths_self_contained_mode` để biết chi tiết.
