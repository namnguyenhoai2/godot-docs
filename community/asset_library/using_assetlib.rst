.. _doc_using_assetlib:

Sử dụng Asset Library
=====================

Trên trang web
--------------

Tổng quan
~~~~~~~~~

Như đã đề cập trước đó, bạn có thể truy cập frontend web của Asset Library trên `trang web chính thức của Godot <https://godotengine.org/asset-library/asset>`_. Đây là giao diện khi bạn truy cập lần đầu:

|image0|

Ở trên cùng, bạn sẽ thấy **header**, phần này đưa bạn đến nhiều khu vực khác của AssetLib - hiện tại, nó đang trống vì chúng ta chưa đăng nhập.

Tìm kiếm
~~~~~~~~

Trong thanh bên trái là phần **thanh tìm kiếm + cài đặt**, còn phần **assets** chiếm khu vực nội dung chính ở bên phải. Bên dưới thanh tìm kiếm, bạn có thể lọc asset theo **danh mục** (chẳng hạn như công cụ 2D, script và bản demo), **mức độ hỗ trợ**, **phiên bản engine** và **giấy phép**. Bạn cũng có thể thay đổi **thứ tự sắp xếp** để sắp xếp theo giấy phép, tên hoặc ngày cập nhật.

Mặc dù hầu hết các cài đặt bộ lọc khác đều khá dễ hiểu, bạn vẫn nên tìm hiểu ý nghĩa của "mức độ hỗ trợ" trong Asset Library. Hiện có ba mức độ hỗ trợ và mỗi asset chỉ có thể thuộc một mức.

Các asset **Nổi bật** là những tài nguyên được tuyển chọn thủ công vì có giá trị đối với cộng đồng.

Các asset **Cộng đồng** do các thành viên của cộng đồng Godot gửi lên và duy trì.

Các asset **Đang thử nghiệm** là những sản phẩm đang trong quá trình phát triển và có thể chứa lỗi cũng như vấn đề về khả năng sử dụng. Chúng không được khuyến nghị dùng trong các dự án nghiêm túc, nhưng bạn được khuyến khích tải xuống, kiểm thử và gửi vấn đề cho tác giả ban đầu.

Bạn có thể kết hợp tùy ý các bộ lọc và tiêu chí tìm kiếm, rồi sau khi nhấp vào nút Search, nhận được danh sách tất cả asset trong Library phù hợp với chúng.

|image1|

Lưu ý rằng kết quả tìm kiếm không được cập nhật theo thời gian thực, vì vậy bạn sẽ phải gửi lại truy vấn tìm kiếm mỗi khi thay đổi cài đặt truy vấn.

Phân tích một asset
~~~~~~~~~~~~~~~~~~~

Bây giờ hãy cùng xem trang của một asset trông như thế nào và có những nội dung gì.

|image2|

1. Hình thu nhỏ/biểu tượng của asset. 2. Tên asset. 3. Số phiên bản hiện tại của asset. 4. Danh mục, phiên bản Godot và trạng thái hỗ trợ của asset. 5. Tác giả/người gửi ban đầu của asset. 6. Giấy phép mà asset được phân phối theo đó. 7. Ngày chỉnh sửa/cập nhật gần nhất của asset. 8. Mô tả bằng văn bản về asset. 9. Các liên kết liên quan đến asset (liên kết tải xuống, danh sách tệp, trình theo dõi vấn đề). 10. Hình ảnh và video giới thiệu asset.

Đăng ký và đăng nhập
~~~~~~~~~~~~~~~~~~~~

Để tải asset lên AssetLib, bạn cần đăng nhập, và để làm vậy, bạn cần có tài khoản người dùng đã đăng ký. Trong tương lai, điều này cũng có thể cho phép bạn sử dụng các tính năng khác, chẳng hạn như bình luận hoặc đánh giá các asset hiện có. Bạn *không* cần đăng nhập để duyệt và tải xuống các asset.

Bạn có thể truy cập trang đăng nhập/đăng ký từ header của AssetLib.

|image3|

Từ đây, bạn có thể đăng ký tài khoản, với yêu cầu phải có địa chỉ email hợp lệ, tên người dùng và mật khẩu (tốt nhất là mật khẩu mạnh).

|image4|

Sau đó, bạn có thể sử dụng tên người dùng và mật khẩu để đăng nhập.

|image5|

Điều này sẽ thay đổi giao diện header của AssetLib. Bây giờ bạn có quyền truy cập vào một số chức năng mới:

- Feed, hiển thị danh sách các cập nhật trạng thái về những asset bạn đã gửi lên (và có thể nhiều hơn trong tương lai). - Danh sách các asset bạn đã tải lên. - Khả năng gửi asset mới.

|image6|

Bạn có thể tìm hiểu cách gửi asset lên Library và các nguyên tắc gửi asset trong phần tiếp theo của hướng dẫn này, :ref:`doc_submitting_to_assetlib`.

.. _doc_using_assetlib_editor:

Trong trình chỉnh sửa
---------------------

.. note::

    Trình chỉnh sửa sẽ hiển thị các danh mục asset khác nhau tùy thuộc vào việc bạn đang duyệt thẻ **Asset Library Projects** của Project Manager hay thẻ **AssetLib** của trình chỉnh sửa.

    Thẻ **Asset Library Projects** của Project Manager sẽ chỉ hiển thị những asset tự chúng là các dự án độc lập. Điều này được biểu thị trong asset library bằng các danh mục *Templates*, *Demos* và *Projects*.

    Thẻ **AssetLib** của trình chỉnh sửa sẽ chỉ hiển thị những asset không phải là các dự án độc lập. Nói cách khác, thẻ này sẽ hiển thị asset từ tất cả danh mục ngoại trừ *Templates*, *Demos* và *Projects*.

Bạn cũng có thể truy cập AssetLib trực tiếp từ Godot:

|image7|

|image14|

Nhấp vào đó, Godot sẽ lấy thông tin về các asset từ AssetLib. Khi hoàn tất, bạn sẽ thấy một cửa sổ tương tự giao diện trang web AssetLib, với một số điểm khác biệt:

|image8|

Tương tự phiên bản web của AssetLib, tại đây bạn có thể tìm kiếm asset theo danh mục, tên và sắp xếp chúng theo các yếu tố như tên hoặc ngày chỉnh sửa.

Đáng chú ý, bạn chỉ có thể lấy asset cho phiên bản Godot hiện tại đang chạy. Projects, Demos và Templates có thể được tải xuống từ giao diện Project Manager của AssetLib. Addons (công cụ, script, vật liệu, v.v.) có thể được tải xuống từ AssetLib trong dự án và thêm vào dự án hiện tại. Ngoài ra, không giống khi sử dụng frontend web, kết quả tìm kiếm được cập nhật theo thời gian thực (bạn không phải nhấn Search sau mỗi lần thay đổi truy vấn tìm kiếm để các thay đổi có hiệu lực).

Trong tương lai, bạn sẽ có thể chọn một nhà cung cấp AssetLib khác để lấy asset (bằng menu thả xuống Site), tuy nhiên hiện tại chỉ phiên bản AssetLib trên `trang web chính thức của Godot <https://godotengine.org>`_ được hỗ trợ, cùng với phiên bản có thể đang chạy trên máy chủ web của máy cục bộ (tùy chọn localhost).

Khi nhấp vào một asset, bạn sẽ thấy thêm thông tin về asset đó.

|image9|

Nếu nhấp vào nút Install, Godot sẽ lấy một bản lưu trữ của asset và theo dõi tiến trình tải xuống ở cuối cửa sổ trình chỉnh sửa. Nếu quá trình tải xuống thất bại, bạn có thể thử lại bằng nút Retry.

|image10|

Khi quá trình hoàn tất, bạn có thể tiếp tục cài đặt bằng nút Install. Thao tác này sẽ mở cửa sổ Package Installer.

|image11|

Tại đây, bạn có thể xem danh sách tất cả các tệp sẽ được cài đặt. Bạn có thể bỏ chọn bất kỳ tệp nào không muốn cài đặt, và Godot cũng sẽ thông báo cho bạn về mọi vấn đề với các tệp mà nó không thể cài đặt. Các tệp này sẽ được hiển thị bằng màu đỏ, và khi di chuột lên chúng, bạn sẽ thấy thông báo nêu rõ lý do không thể cài đặt.

|image12|

Sau khi hoàn tất, bạn có thể nhấn nút Install, thao tác này sẽ giải nén tất cả tệp trong bản lưu trữ và import mọi asset chứa trong đó, chẳng hạn như hình ảnh hoặc mô hình 3D. Khi hoàn tất, bạn sẽ thấy thông báo cho biết quá trình cài đặt Package đã hoàn tất.

|image13|

Bạn cũng có thể sử dụng nút Import để import các bản lưu trữ asset lấy từ nơi khác (chẳng hạn như tải chúng trực tiếp từ frontend web của AssetLib), thao tác này sẽ đưa bạn qua cùng quy trình cài đặt package như với các asset được tải trực tiếp qua Godot mà chúng ta vừa đề cập.

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
