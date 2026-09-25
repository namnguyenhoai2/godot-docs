.. _doc_installing_plugins:

Cài đặt plugin
==============

Godot có một hệ thống plugin cho editor với nhiều plugin do cộng đồng phát triển. Plugin có thể mở rộng chức năng của editor bằng các node mới, dock bổ sung, các tính năng tiện lợi và nhiều hơn nữa.

Tìm plugin
~~~~~~~~~~

Cách được khuyến nghị để tìm plugin Godot là sử dụng `Asset Library <https://godotengine.org/asset-library/>`_. Bạn có thể duyệt thư viện này trực tuyến, nhưng sử dụng trực tiếp từ editor sẽ thuận tiện hơn. Để làm vậy, hãy nhấp vào tab **AssetLib** ở đầu editor:

.. image:: img/installing_plugins_assetlib_tab.webp

Bạn cũng có thể tìm asset trên các website lưu trữ mã nguồn như GitHub.

.. note::

    Một số repository tự mô tả là "plugin" nhưng thực tế có thể không phải là plugin *editor*. Điều này đặc biệt đúng với các script được sử dụng trong một project đang chạy. Bạn không cần bật những plugin như vậy để sử dụng chúng. Hãy tải chúng xuống và giải nén các tệp vào thư mục project của bạn.

    Một cách để phân biệt plugin editor với plugin không dành cho editor là tìm tệp ``plugin.cfg`` trong repository chứa plugin. Nếu repository có tệp ``plugin.cfg`` trong một thư mục được đặt trong thư mục ``addons/``, thì đó là plugin editor.

Cài đặt một plugin
~~~~~~~~~~~~~~~~~~

Để cài đặt plugin, hãy tải plugin xuống dưới dạng tệp lưu trữ ZIP. Trong Asset Library, bạn có thể thực hiện việc này bằng nút **Download**, từ editor hoặc qua giao diện Web.

Trên GitHub, nếu plugin có khai báo *tags* (phiên bản), hãy chuyển đến tab **Releases** để tải xuống bản phát hành ổn định. Điều này đảm bảo bạn tải xuống phiên bản được tác giả xác nhận là ổn định.

Trên GitHub, nếu plugin không khai báo *tags* nào, hãy sử dụng nút **Download ZIP** để tải xuống tệp ZIP của bản sửa đổi mới nhất:

.. image:: img/installing_plugins_github_download_zip.png

Hãy giải nén tệp lưu trữ ZIP và di chuyển thư mục ``addons/`` có trong đó vào thư mục project của bạn. Nếu project đã có thư mục ``addons/``, hãy di chuyển thư mục ``addons/`` của plugin vào thư mục project để hợp nhất nội dung của thư mục mới với thư mục hiện có. Trình quản lý tệp có thể hỏi bạn có muốn ghi vào thư mục hay không; hãy trả lời **Yes**. Không có tệp nào bị ghi đè trong quá trình này.

.. _doc_installing_plugins_enabling_a_plugin:

Bật plugin
~~~~~~~~~~

Để bật plugin vừa cài đặt, hãy mở **Project > Project Settings** ở đầu editor, sau đó chuyển đến tab **Plugins**. Nếu plugin được đóng gói đúng cách, bạn sẽ thấy plugin đó trong danh sách plugin. Nhấp vào hộp kiểm **Enable** để bật plugin.

.. image:: img/installing_plugins_project_settings.webp


Bạn có thể sử dụng plugin ngay sau khi bật; không cần khởi động lại editor. Tương tự, bạn có thể tắt plugin mà không cần khởi động lại editor.

.. _`Asset Library`: https://godotengine.org/asset-library/
