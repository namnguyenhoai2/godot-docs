.. _doc_using_assetlib:

Sử dụng Asset Library
=====================

Trên website
------------

Tổng quan
~~~~~~~~~

Như đã đề cập trước đó, bạn có thể truy cập frontend web của Asset Library trên `website chính thức của Godot <https://godotengine.org/asset-library/asset>`_. Đây là giao diện bạn thấy khi lần đầu truy cập:

|image0|

Ở trên cùng, bạn thấy **header**, dẫn bạn đến nhiều phần khác của AssetLib - hiện tại phần này trống vì chúng ta chưa đăng nhập.

Tìm kiếm
~~~~~~~~

Ở thanh bên trái là phần **thanh tìm kiếm + cài đặt**, còn phần **tài nguyên** chiếm khu vực nội dung chính ở bên phải. Bên dưới thanh tìm kiếm, bạn có thể lọc tài nguyên theo **danh mục** (chẳng hạn như công cụ 2D, script và bản demo), **mức độ hỗ trợ**, **phiên bản engine** và **giấy phép**. Bạn cũng có thể thay đổi **thứ tự sắp xếp** để sắp xếp theo giấy phép, tên hoặc ngày cập nhật.

Mặc dù hầu hết các cài đặt bộ lọc khác khá dễ hiểu, bạn nên tìm hiểu ý nghĩa của "mức độ hỗ trợ" trong Asset Library. Hiện có ba mức độ hỗ trợ và mỗi tài nguyên chỉ có thể thuộc một mức.

Tài nguyên **Featured** là những tài nguyên được lựa chọn thủ công vì giá trị của chúng đối với cộng đồng.

Tài nguyên **Community** do các thành viên của cộng đồng Godot gửi lên và duy trì.

Tài nguyên **Testing** đang trong quá trình phát triển và có thể chứa lỗi cũng như vấn đề về khả năng sử dụng
issues. Chúng không được khuyến nghị sử dụng trong các dự án nghiêm túc, nhưng bạn được
khuyến khích tải xuống, kiểm thử và gửi issue cho tác giả ban đầu.

Bạn có thể kết hợp tùy ý các bộ lọc và tiêu chí tìm kiếm, rồi khi nhấp vào nút Search, nhận được danh sách tất cả tài nguyên trong Library khớp với các tiêu chí đó.

|image1|

Lưu ý rằng kết quả tìm kiếm không được cập nhật theo thời gian thực, vì vậy bạn phải gửi lại truy vấn tìm kiếm mỗi lần thay đổi cài đặt truy vấn.

Phân tích một tài nguyên
~~~~~~~~~~~~~~~~~~~~~~~~

Bây giờ hãy xem trang của một tài nguyên trông như thế nào và chứa những gì.

|image2|

1. Thumbnail/icon của tài nguyên.
2. Tên tài nguyên.
3. Số phiên bản hiện tại của tài nguyên.
4. Danh mục, phiên bản Godot và trạng thái hỗ trợ của tài nguyên.
5. Tác giả/người gửi ban đầu của tài nguyên.
6. Giấy phép mà tài nguyên được phân phối theo đó.
7. Ngày chỉnh sửa/cập nhật gần nhất của tài nguyên.
8. Mô tả bằng văn bản về tài nguyên.
9. Các liên kết liên quan đến tài nguyên (liên kết tải xuống, danh sách tệp, trình theo dõi issue).
10. Hình ảnh và video giới thiệu tài nguyên.

Đăng ký và đăng nhập
~~~~~~~~~~~~~~~~~~~~

Để tải tài nguyên lên AssetLib, bạn cần đăng nhập, và để làm vậy, bạn cần có tài khoản người dùng đã đăng ký. Trong tương lai, việc này cũng có thể cho phép bạn sử dụng các tính năng khác, chẳng hạn như bình luận hoặc đánh giá các tài nguyên hiện có. Bạn *không* cần đăng nhập để duyệt và tải xuống tài nguyên.

Bạn có thể truy cập trang đăng nhập/đăng ký từ header của AssetLib.

|image3|

Từ đây, bạn có thể đăng ký tài khoản, yêu cầu một địa chỉ email hợp lệ, tên người dùng và mật khẩu (tốt nhất là mật khẩu mạnh).

|image4|

Sau đó, bạn có thể dùng tên người dùng và mật khẩu để đăng nhập.

|image5|

Thao tác này sẽ thay đổi giao diện header của AssetLib. Giờ đây bạn có quyền truy cập vào một số chức năng mới:

- Feed, hiển thị danh sách các cập nhật trạng thái về những tài nguyên bạn đã gửi lên (và có thể có thêm nội dung trong tương lai).
- Danh sách các tài nguyên bạn đã tải lên.
- Khả năng gửi tài nguyên mới.

|image6|

Bạn có thể tìm hiểu cách gửi tài nguyên lên Library và các hướng dẫn gửi tài nguyên trong phần tiếp theo của bài hướng dẫn này, :ref:`doc_submitting_to_assetlib`.

.. _doc_using_assetlib_editor:

Trong editor
------------

.. note::

    Editor sẽ hiển thị các danh mục tài nguyên khác nhau tùy thuộc vào việc bạn đang duyệt tab **Asset Library Projects** của Project Manager hay tab **AssetLib** của editor.

    Tab **Asset Library Projects** của Project Manager chỉ hiển thị những tài nguyên vốn là các project độc lập. Trên asset library, điều này được biểu thị bằng các danh mục *Templates*, *Demos* và *Projects*.

    Tab **AssetLib** của editor chỉ hiển thị những tài nguyên *không phải* là các project độc lập. Nói cách khác, tab này sẽ hiển thị tài nguyên thuộc mọi danh mục ngoại trừ *Templates*, *Demos* và *Projects*.

Bạn cũng có thể truy cập AssetLib trực tiếp từ Godot:

|image7|

|image14|

Nhấp vào đó, Godot sẽ lấy thông tin về các tài nguyên từ AssetLib. Khi hoàn tất, bạn sẽ thấy một cửa sổ tương tự giao diện website AssetLib, với một số điểm khác biệt:

|image8|

Tương tự phiên bản web của AssetLib, tại đây bạn có thể tìm kiếm tài nguyên theo danh mục, tên và sắp xếp chúng theo các yếu tố như tên hoặc ngày chỉnh sửa.

Đáng chú ý là bạn chỉ có thể lấy tài nguyên cho phiên bản Godot hiện tại đang chạy. Có thể tải Projects, Demos và Templates xuống từ giao diện Project Manager của AssetLib. Có thể tải Addons (tools, scripts, materials, v.v.) xuống từ AssetLib trong project và thêm chúng vào project hiện tại. Ngoài ra, không giống khi sử dụng frontend web, kết quả tìm kiếm được cập nhật theo thời gian thực (bạn không phải nhấn Search sau mỗi thay đổi đối với truy vấn tìm kiếm để các thay đổi có hiệu lực).

Trong tương lai, bạn sẽ có thể chọn một provider AssetLib khác để lấy tài nguyên (bằng menu thả xuống Site), tuy nhiên hiện tại chỉ phiên bản AssetLib chính thức trên `website Godot <https://godotengine.org>`_ được hỗ trợ, cùng với phiên bản có thể đang chạy trên web server của máy cục bộ (tùy chọn localhost).

Khi nhấp vào một tài nguyên, bạn sẽ thấy thêm thông tin về tài nguyên đó.

|image9|

Nếu nhấp vào nút Install, Godot sẽ lấy một archive của tài nguyên và theo dõi tiến trình tải xuống ở cuối cửa sổ editor. Nếu quá trình tải xuống thất bại, bạn có thể thử lại bằng nút Retry.

|image10|

Khi hoàn tất, bạn có thể tiến hành cài đặt bằng nút Install. Thao tác này sẽ mở cửa sổ Package Installer.

|image11|

Tại đây, bạn có thể xem danh sách tất cả các tệp sẽ được cài đặt. Bạn có thể bỏ chọn bất kỳ tệp nào mà mình không muốn cài đặt, và Godot cũng sẽ thông báo cho bạn về mọi sự cố với các tệp mà Godot không thể cài đặt. Các tệp này sẽ được hiển thị bằng màu đỏ, và khi di chuột lên chúng, bạn sẽ thấy thông báo nêu rõ lý do không thể cài đặt.

|image12|

Sau khi hoàn tất, bạn có thể nhấn nút Install để giải nén tất cả các tệp trong kho lưu trữ và import mọi asset có trong đó, chẳng hạn như hình ảnh hoặc mô hình 3D. Khi hoàn tất, bạn sẽ thấy thông báo cho biết quá trình Package installation đã hoàn tất.

|image13|

Bạn cũng có thể sử dụng nút Import để import các kho lưu trữ asset lấy từ nơi khác (chẳng hạn như tải trực tiếp từ frontend web AssetLib), thao tác này sẽ đưa bạn qua cùng quy trình cài đặt package như với các asset được tải trực tiếp qua Godot mà chúng ta vừa đề cập.

.. |image0| image:: img/assetlib_website.webp
.. |image1| image:: img/assetlib_search.webp
.. |image2| image:: img/assetlib_asset.webp
.. |image3| image:: img/assetlib_register-login.webp
.. |image4| image:: img/assetlib_register.webp
.. |image5| image:: img/assetlib_login.webp
.. |image6| image:: img/assetlib_login_header.webp
.. |image7| image:: img/assetlib_editor_workspace.png
.. |image8| image:: img/assetlib_editor.png
.. |image9| image:: img/assetlib_editor_asset.png
.. |image10| image:: img/assetlib_editor_download.png
.. |image11| image:: img/assetlib_editor_installer.png
.. |image12| image:: img/assetlib_editor_installer_error.png
.. |image13| image:: img/assetlib_editor_installer_success.png
.. |image14| image:: img/assetlib_editor_projects.webp

.. _`Godot's official website`: https://godotengine.org/asset-library/asset
.. _`Godot website`: https://godotengine.org
