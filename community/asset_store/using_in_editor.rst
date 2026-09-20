.. _doc_using_asset_store_editor:

Sử dụng Asset Store trong Engine
================================

Truy cập
--------

Có thể truy cập Asset Store từ bên trong Godot thông qua trình quản lý dự án.

.. image:: img/asset_store_editor_projects.webp

Cũng như từ trong trình chỉnh sửa.

.. image:: img/asset_store_editor_workspace.webp

Tab :button:`Asset Store` của Trình quản lý dự án sẽ chỉ hiển thị các tài sản là dự án độc lập. Điều này được biểu thị trên Asset Store bằng thẻ *Template*.

Tab :button:`Asset Store` của trình chỉnh sửa sẽ chỉ hiển thị các tài sản *không* phải là dự án độc lập. Nói cách khác, tab này sẽ hiển thị các tài sản thuộc mọi danh mục ngoại trừ *Templates*.

Nếu đây là lần đầu tiên bạn cần Engine truy cập Internet, bạn sẽ phải nhấp vào nút :button:`Go Online`.

.. image:: img/go_online.webp

Tải xuống và cài đặt tài sản
----------------------------

Nhấp vào một tài sản, và Godot sẽ lấy thông tin về tài sản đó từ Asset Store. Sau khi hoàn tất, bạn sẽ thấy một cửa sổ có giao diện tương tự trang web Asset Store, với một số điểm khác biệt:

.. image:: img/asset_store_editor.webp

Tương tự phiên bản web của Asset Store, tại đây bạn có thể tìm kiếm tài sản theo danh mục hoặc tên, cũng như sắp xếp chúng theo những tiêu chí như tên hoặc ngày chỉnh sửa. Không giống khi sử dụng giao diện web, kết quả tìm kiếm được cập nhật theo thời gian thực (bạn không phải nhấn :button:`Search` sau mỗi thay đổi đối với truy vấn tìm kiếm để các thay đổi có hiệu lực).

Khi nhấp vào một tài sản, bạn sẽ thấy thêm thông tin về tài sản đó.

.. image:: img/asset_store_editor_asset.webp

Nếu nhấp vào nút :button:`Download`, Godot sẽ lấy một tệp lưu trữ của tài sản và theo dõi tiến trình tải xuống ở cuối cửa sổ trình chỉnh sửa. Nếu quá trình tải xuống không thành công, bạn có thể thử lại bằng nút :button:`Retry`.

Khi quá trình tải xuống hoàn tất, cửa sổ Configure Asset sẽ tự động mở.

.. image:: img/asset_store_editor_configure.webp

Tại đây, bạn có thể xem danh sách tất cả các tệp sẽ được cài đặt. Nếu nhấp vào mũi tên ở phía trên bên trái, một cửa sổ sẽ mở ra, tại đó bạn có thể bỏ chọn bất kỳ tệp nào mà mình không muốn cài đặt. Mọi tệp không thể cài đặt sẽ được hiển thị bằng màu đỏ; khi di chuột lên chúng, bạn sẽ thấy thông báo nêu rõ lý do không thể cài đặt.

.. image:: img/asset_store_editor_installer_error.webp

Sau khi hoàn tất, bạn có thể nhấn nút :button:`Install`, thao tác này sẽ giải nén tất cả các tệp trong tệp lưu trữ và nhập mọi tài sản chứa trong đó, chẳng hạn như hình ảnh hoặc mô hình 3D. Sau khi hoàn tất, bạn sẽ thấy thông báo cho biết quá trình cài đặt gói đã hoàn tất.

.. image:: img/asset_store_editor_installer_success.webp

Bạn cũng có thể sử dụng nút :button:`Import` để nhập các tệp lưu trữ tài sản lấy từ nơi khác (chẳng hạn như tải chúng trực tiếp từ giao diện web Asset Store), thao tác này sẽ đưa bạn qua cùng quy trình cài đặt gói như với các tài sản được tải trực tiếp qua Godot mà chúng ta vừa đề cập.
