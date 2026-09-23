.. _doc_project_manager:

Sử dụng Project Manager
=======================

Khi khởi chạy Godot, cửa sổ đầu tiên bạn thấy là Project Manager. Cửa sổ này cho phép bạn tạo, xóa, import hoặc chạy các project game:

.. image:: img/editor_ui_intro_project_manager_01.webp

Để thay đổi ngôn ngữ của editor, hãy nhấp vào nút **Settings** ở góc trên bên phải:

.. image:: img/editor_ui_intro_project_manager_02.webp

Trong Project Manager Settings, bạn có thể thay đổi **language** của giao diện từ menu thả xuống ngôn ngữ, mặc định là ngôn ngữ hệ thống.

Bạn cũng có thể thay đổi **theme** và **color preset** của editor, **display scale** để điều chỉnh kích thước các thành phần giao diện khác nhau, cũng như khả năng sử dụng các chức năng trực tuyến bằng **network mode**. Nếu network mode là online, Godot cũng sẽ kiểm tra và thông báo cho bạn về các phiên bản Godot mới.

Bạn cũng có thể thay đổi **directory naming convention** để thay thế khoảng trắng theo định dạng đã chọn khi tự động tạo thư mục.

.. image:: img/editor_ui_intro_project_manager_10.webp

.. _doc_creating_and_importing_projects:

Tạo và import project
---------------------

Để tạo một project mới:

1. Nhấp vào nút **Create** ở phía trên bên trái cửa sổ.
2. Đặt tên cho project, sau đó mở trình duyệt tệp bằng nút **Browse** và chọn một thư mục trống trên máy tính để lưu các tệp. Ngoài ra, bạn có thể bật tùy chọn **Create Folder** để tự động tạo một thư mục con mới có tên project, tuân theo directory naming convention được thiết lập trong phần cài đặt. Thư mục trống sẽ hiển thị dấu kiểm màu xanh ở bên phải.
3. Chọn một trong các renderer (bạn cũng có thể thay đổi lựa chọn này sau).
4. Nhấp vào nút :ui:`Create` để tạo thư mục project và mở thư mục đó trong editor.

.. image:: img/editor_ui_intro_project_manager_04.webp

.. note:: Bạn có thể tùy chọn một hệ thống version control. Hiện tại, chỉ `git <https://git-scm.com>`__ được hỗ trợ và hệ thống này yêu cầu Godot Git Plugin đã được cài đặt, είτε thủ công hoặc bằng :ref:`Asset Library <doc_using_assetlib>`. Để tìm hiểu thêm về Godot Git Plugin, hãy xem `wiki <https://github.com/godotengine/godot-git-plugin/wiki>`__ của plugin.

Sử dụng trình duyệt tệp
~~~~~~~~~~~~~~~~~~~~~~~

Trong cửa sổ **Create New Project**, nhấp vào nút **Browse** để mở trình duyệt tệp của Godot. Bạn có thể chọn một vị trí hoặc nhập đường dẫn thư mục vào trường **Path** sau khi chọn một ổ đĩa.

Ở bên trái trường đường dẫn trên hàng đầu tiên có các mũi tên để điều hướng lùi và tiến qua những vị trí đã truy cập gần đây. Mũi tên lên sẽ điều hướng đến thư mục cha. Ở bên phải trường đường dẫn có các nút để làm mới nội dung của thư mục hiện tại, thêm hoặc bỏ thư mục hiện tại khỏi mục yêu thích và hiển thị hoặc ẩn các thư mục ẩn.

Tiếp theo là các nút để chuyển kiểu hiển thị của các thư mục và tệp giữa chế độ xem lưới và chế độ xem danh sách.

Nút cuối cùng ở bên phải sẽ tạo một thư mục mới.

Các thư mục được yêu thích sẽ hiển thị ở bên trái, trong phần **Favorites**. Bạn có thể sắp xếp các mục yêu thích bằng các nút lên và xuống trong phần này. Các thư mục được chọn gần đây nhất sẽ được liệt kê trong danh sách **Recent**.

.. image:: img/editor_ui_intro_project_manager_05.webp

Mở và import project
--------------------

Lần tới khi mở Project Manager, bạn sẽ thấy project mới của mình trong danh sách. Nhấp đúp vào project để mở project đó trong editor.

.. image:: img/editor_ui_intro_project_manager_06.webp

Tương tự, bạn có thể import các project hiện có bằng nút **Import**. Tìm đến thư mục chứa project hoặc tệp **project.godot** để import và chỉnh sửa project đó.

.. image:: img/editor_ui_intro_project_manager_08.webp

Ngoài ra, bạn có thể chọn một tệp zip để Godot tự động giải nén.

Khi đường dẫn thư mục chính xác, bạn sẽ thấy một dấu kiểm màu xanh.

.. image:: img/editor_ui_intro_project_manager_09.webp

.. _doc_project_manager_downloading_demos:

Tải xuống demo và template
--------------------------

Từ tab **Asset Library**, bạn có thể tải xuống các template project và demo mã nguồn mở từ :ref:`Asset Library <toc-learn-features-assetlib>` để bắt đầu nhanh hơn.

Lần đầu mở tab này, bạn sẽ thấy tab yêu cầu bạn chuyển sang chế độ trực tuyến. Vì lý do riêng tư, project manager và Godot editor không thể truy cập internet theo mặc định. Để bật quyền truy cập internet, hãy nhấp vào nút **Go Online**. Thao tác này cũng cho phép project manager thông báo cho bạn về các bản cập nhật. Nếu muốn tắt tính năng này trong tương lai, hãy mở phần cài đặt của project manager và đổi **Network Mode** thành "Offline"

Bây giờ Godot đã kết nối với internet, bạn có thể tải xuống một demo hoặc template theo các bước sau:

1. Nhấp vào tiêu đề của demo hoặc template.
2. Trên trang mở ra, nhấp vào nút tải xuống.
3. Sau khi quá trình tải xuống hoàn tất, hãy nhấp vào nút cài đặt và chọn nơi bạn muốn lưu project.

.. image:: img/editor_ui_intro_project_manager_03.webp

Quản lý project bằng tag
------------------------

Đối với người dùng có nhiều project trên một PC, việc theo dõi chúng có thể khá khó khăn. Để hỗ trợ việc này, Godot cho phép bạn tạo các tag cho project. Để thêm tag vào một project, hãy nhấp vào project trong project manager, sau đó nhấp vào nút **Manage Tags**

.. image:: img/editor_ui_intro_project_manager_11.webp

Cửa sổ manage project tags sẽ mở ra. Để thêm tag, hãy nhấp vào nút dấu cộng.

.. image:: img/editor_ui_intro_project_manager_12.webp

Nhập tên tag rồi nhấp vào **OK**. Project của bạn giờ sẽ có thêm tag. Các tag này có thể được sử dụng cho bất kỳ project nào khác trong project manager.

Để chỉ hiển thị các project có một tag cụ thể, bạn có thể nhấp vào tag hoặc nhập ``tag:`` rồi nhập tag muốn tìm vào thanh bộ lọc. Để giới hạn kết quả bằng nhiều tag, bạn có thể nhấp vào một tag khác hoặc thêm ``tag:`` sau một khoảng trắng rồi nhập tag khác vào thanh bộ lọc.

Ngoài ra, các tag sẽ đi cùng project. Vì vậy, nếu bạn gắn tag cho project, gửi project đó sang một máy khác và import vào project manager, bạn sẽ thấy các tag đã tạo.

Để xóa một tag khỏi project manager, tag đó phải được xóa khỏi tất cả các project đang sử dụng nó. Sau khi hoàn tất, hãy đóng project manager rồi mở lại; tag đó sẽ biến mất.

Recovery Mode
-------------

Nếu một project bị crash ngay khi khởi động hoặc thường xuyên bị crash trong quá trình chỉnh sửa, bạn có thể mở project ở recovery mode để thử làm cho project ổn định hơn trong khi tìm nguyên nhân gây crash và khắc phục nguyên nhân đó.

Thông thường, một project sẽ tự động mở ở recovery mode khi bạn mở lại project sau khi bị crash. Nếu không, bạn có thể mở recovery mode theo cách thủ công bằng cách chọn project trong project manager; để thực hiện việc này, hãy chọn project từ danh sách project, nhấp vào nút dropdown bên cạnh edit node và chọn ``Edit in recovery mode``.

.. image:: img/editor_ui_intro_project_manager_13.webp

Khi ở recovery mode, các mục sau sẽ bị vô hiệu hóa:

- Tool scripts
- Editor plugins
- GDExtension addons
- Automatic scene restoring
- Running the project

Bạn nên backup project trước khi chỉnh sửa project ở recovery mode.
