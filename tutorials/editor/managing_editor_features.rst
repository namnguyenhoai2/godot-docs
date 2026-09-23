:article_outdated: Đúng

.. _doc_managing_editor_features:

Quản lý các tính năng của trình chỉnh sửa
=========================================

Giới thiệu
----------

Trong một số tình huống, bạn có thể muốn giới hạn những tính năng có thể sử dụng trong Godot editor. Ví dụ: một nhà thiết kế UI trong nhóm không cần xem các tính năng 3D, hoặc một nhà giáo dục muốn từ từ giới thiệu các tính năng cho học sinh. Godot có một hệ thống tích hợp sẵn gọi là "feature profiles" để thực hiện việc này.

Với feature profiles, các tính năng chính và node có thể bị ẩn khỏi editor. Việc này chỉ ẩn các phần của giao diện chứ không thực sự xóa hỗ trợ cho những tính năng đó, vì vậy các scene và script phụ thuộc vào chúng vẫn hoạt động bình thường. Điều này cũng có nghĩa là feature profiles không phải là một kỹ thuật tối ưu hóa. Để biết thông tin về cách tối ưu hóa Godot, hãy xem :ref:`doc_performance`.

Tạo profile
-----------

Để quản lý các tính năng của editor, hãy vào **Editor > Manage Editor Features**. Thao tác này sẽ mở cửa sổ **Manage Editor Feature Profiles**. Theo mặc định sẽ không có profile nào. Nhấp vào **Create Profile** và đặt tên cho profile. Sau đó, bạn sẽ thấy danh sách tất cả các tính năng trong Godot editor.

.. image:: img/configure_profile.png

Phần đầu tiên cho phép loại bỏ các tính năng chính của editor, chẳng hạn như 3D editor hoặc scripting editor. Bên dưới các tính năng chính là mọi class và node trong Godot, cũng có thể được vô hiệu hóa. Nhấp vào một node, tất cả thuộc tính và tùy chọn của node đó sẽ được liệt kê trong hộp **Extra Items**; bạn có thể vô hiệu hóa từng mục trong số đó.

.. image:: img/node_features.png

Chia sẻ profile
---------------

Để chia sẻ profile giữa các editor, hãy nhấp vào nút **Export**. Lưu profile tùy chỉnh ở đâu đó dưới dạng tệp ``.profile``. Để sử dụng profile này trong một editor khác, hãy mở cửa sổ **Manage Editor Feature Profiles** của editor đó và nhấp vào import, sau đó chọn tệp ``.profile``.

Tuy nhiên, quy trình này có thể khá bất tiện nếu cần thiết lập profile tùy chỉnh cho nhiều máy tính. Một lựa chọn khác là bật self-contained mode cho Godot, cho phép đặt toàn bộ cấu hình editor trong cùng thư mục với binary của editor. Xem :ref:`doc_data_paths_self_contained_mode` để biết chi tiết.
