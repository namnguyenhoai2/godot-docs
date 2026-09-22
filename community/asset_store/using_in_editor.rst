.. _doc_using_asset_store_editor:

Sử dụng Asset Store trong Engine
================================

Truy cập Asset Store
--------------------

Có thể truy cập Asset Store từ trình quản lý dự án trong Godot.

.. image:: img/asset_store_editor_projects.webp

Cũng như từ bên trong editor.

.. image:: img/asset_store_editor_workspace.webp

Tab :button:`Asset Store` của Project Manager chỉ hiển thị các asset là những dự án độc lập. Điều này được biểu thị trên Asset Store bằng thẻ *Template*.

Tab :button:`Asset Store` của editor chỉ hiển thị các asset *không* độc lập
projects. Nói cách khác, tab này sẽ hiển thị các asset thuộc mọi danh mục, ngoại trừ *Templates*.

Nếu đây là lần đầu tiên bạn cần Engine truy cập Internet, bạn sẽ cần nhấp vào nút :button:`Go Online`.

.. image:: img/go_online.webp

Tải xuống và cài đặt asset
--------------------------

Nhấp vào một asset, và Godot sẽ lấy thông tin về asset đó từ Asset Store. Khi hoàn tất, bạn sẽ thấy một cửa sổ có giao diện tương tự trang web Asset Store, với một số khác biệt:

.. image:: img/asset_store_editor.webp

Tương tự phiên bản web của Asset Store, tại đây bạn có thể tìm kiếm asset theo danh mục hoặc tên, đồng thời sắp xếp chúng theo những tiêu chí như tên hoặc ngày chỉnh sửa. Không giống như khi sử dụng giao diện web, kết quả tìm kiếm được cập nhật theo thời gian thực (bạn không phải nhấn :button:`Search` sau mỗi thay đổi đối với truy vấn tìm kiếm để các thay đổi có hiệu lực).

Khi nhấp vào một asset, bạn sẽ thấy thêm thông tin về asset đó.

.. image:: img/asset_store_editor_asset.webp

Nếu nhấp vào nút :button:`Download`, Godot sẽ lấy một archive của asset và theo dõi tiến trình tải xuống ở cuối cửa sổ editor. Nếu quá trình tải xuống thất bại, bạn có thể thử lại bằng nút :button:`Retry`.

Khi quá trình tải xuống hoàn tất, cửa sổ Configure Asset sẽ tự động mở.

.. image:: img/asset_store_editor_configure.webp

Tại đây, bạn có thể xem danh sách tất cả các tệp sẽ được cài đặt. Nếu nhấp vào mũi tên ở phía trên bên trái, một cửa sổ sẽ mở ra, tại đó bạn có thể bỏ chọn bất kỳ tệp nào không muốn cài đặt. Các tệp không thể cài đặt sẽ được hiển thị bằng màu đỏ; khi di chuột lên chúng, bạn sẽ thấy thông báo nêu rõ lý do không thể cài đặt.

.. image:: img/asset_store_editor_installer_error.webp

Sau khi hoàn tất, bạn có thể nhấn nút :button:`Install`. Nút này sẽ giải nén tất cả các tệp trong archive và import mọi asset có trong đó, chẳng hạn như hình ảnh hoặc model 3D. Khi hoàn tất, bạn sẽ thấy thông báo cho biết quá trình cài đặt package đã hoàn tất.

.. image:: img/asset_store_editor_installer_success.webp

Bạn cũng có thể sử dụng nút :button:`Import` để import các archive asset lấy từ nơi khác (chẳng hạn như tải trực tiếp từ giao diện web của Asset Store). Thao tác này sẽ đưa bạn qua cùng quy trình cài đặt package như với các asset được tải trực tiếp qua Godot mà chúng ta vừa đề cập.
