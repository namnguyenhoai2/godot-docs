.. _doc_submitting_to_asset_store:

Gửi lên Asset Store
===================

Giới thiệu
----------

Hướng dẫn này nhằm cung cấp chỉ dẫn về cách bạn có thể gửi asset của riêng mình lên `Godot Asset Store <https://store.godotengine.org/>`_ và chia sẻ chúng với cộng đồng Godot.

Như đã đề cập trên :ref:`doc_using_asset_store_website` trang này, để có thể gửi asset lên Asset Store, bạn cần có một tài khoản đã đăng ký và đăng nhập vào tài khoản đó.

Hướng dẫn gửi
-------------

Trước khi gửi asset, hãy đảm bảo asset đáp ứng tất cả các yêu cầu và cũng cân nhắc làm theo các khuyến nghị.

Yêu cầu
~~~~~~~

Nói chung, hầu hết các asset mà mọi người gửi lên Asset Store đều được chấp nhận. Tuy nhiên, để asset của bạn được chấp nhận, asset cần đáp ứng một số yêu cầu để được phê duyệt.

* Asset phải **hoạt động**. Nếu asset không chạy hoặc không hoạt động theo cách khác trong phiên bản Godot đã chỉ định, asset sẽ bị từ chối.

* Asset phải có tệp **.gitignore** phù hợp. Việc loại bỏ dữ liệu dư thừa khỏi repository là rất quan trọng. `Đây là một mẫu. <https://raw.githubusercontent.com/aaronfranke/gitignore/godot/Godot.gitignore>`_

* Không được có **submodule**, hoặc mọi submodule phải không thiết yếu. GitHub không đưa submodule vào tệp ZIP đã tải xuống, vì vậy nếu asset cần nội dung của submodule thì asset của bạn sẽ không hoạt động.

* **Giấy phép** phải chính xác. Giấy phép được liệt kê trên Asset Store phải khớp với giấy phép trong repository. Repo **phải** có một tệp giấy phép, được đặt tên là "LICENSE" hoặc "LICENSE.md". Tệp này phải chứa chính văn bản giấy phép và một tuyên bố bản quyền bao gồm (các) năm và chủ sở hữu bản quyền.

* Sử dụng **tiếng Anh** chuẩn cho tên và mô tả asset của bạn. Điều này bao gồm việc viết hoa đúng cách và sử dụng các câu đầy đủ trong phần mô tả. Bạn cũng có thể thêm các ngôn ngữ khác, nhưng ít nhất phải có phiên bản tiếng Anh.

* Liên kết biểu tượng phải là một **liên kết trực tiếp**. Đối với các biểu tượng được lưu trữ trên GitHub, liên kết phải bắt đầu bằng "raw.githubusercontent.com", không phải "github.com".

Khuyến nghị
~~~~~~~~~~~

Những điều này không bắt buộc để asset của bạn được phê duyệt, nhưng nếu làm theo các khuyến nghị này, bạn có thể góp phần làm cho Asset Store trở thành một nơi tốt hơn cho tất cả người dùng.

* Khi tạo asset không phải project, thông lệ phổ biến là đặt các tệp của bạn bên trong thư mục **addons/asset_name/**. Hãy làm vậy để tránh các tệp của bạn xung đột với những asset khác hoặc với các tệp của người dùng cài đặt asset của bạn. Thư mục này sẽ **không** được tự động tạo khi người dùng cài đặt asset của bạn.

* Sửa hoặc tắt tất cả **cảnh báo** của script. Hệ thống cảnh báo giúp xác định các vấn đề trong code của bạn, nhưng những người sử dụng asset không cần nhìn thấy chúng.

* Làm cho code của bạn tuân theo các **hướng dẫn về style** chính thức. Việc có style nhất quán giúp người khác đọc code của bạn và cũng hữu ích nếu người khác muốn đóng góp cho asset của bạn. Xem
  :ref:`doc_gdscript_styleguide` hoặc :ref:`doc_c_sharp_styleguide`.

* Nếu repo của bạn có ảnh chụp màn hình, hãy đặt chúng trong một thư mục con riêng và thêm một tệp **.gdignore** trống vào cùng thư mục đó (lưu ý: **gd**, không phải **git**). Điều này ngăn Godot import các ảnh chụp màn hình của bạn. Trên Windows, mở command prompt trong thư mục project và chạy ``type nul > .gdignore`` để tạo một tệp có tên bắt đầu bằng dấu chấm.

* Nếu asset của bạn là một thư viện dùng để làm việc với các tệp khác, hãy cân nhắc đưa **các tệp ví dụ** vào asset.

* Hãy cân nhắc thêm tệp **.gitattributes** vào repo của bạn. Tệp này cho phép cung cấp thêm chỉ dẫn cho Git, chẳng hạn như chỉ định ký tự kết thúc dòng và liệt kê các tệp không cần thiết để asset của bạn hoạt động với ``export-ignore``
  directive. Chỉ thị này loại bỏ các tệp đó khỏi tệp ZIP kết quả,
  ngăn không cho người dùng Asset Store tải chúng xuống. Sau đây là các ví dụ phổ biến về **.gitattributes**:

  .. tabs::

   .. tab:: Projects / Templates

      .. code-block:: shell

        # Normalize line endings for all files that Git considers text files.
        * text=auto eol=lf

   .. tab:: Addons / Asset Packs

      .. code-block:: shell

        # Normalize line endings for all files that Git considers text files.
        * text=auto eol=lf

        # Only include the addons folder when downloading from the Asset Store.
        /**        export-ignore
        /addons    !export-ignore
        /addons/** !export-ignore

* Nếu bạn đang gửi một plugin, hãy thêm một **bản sao** giấy phép và readme vào chính thư mục plugin. Đây là thư mục mà người dùng chắc chắn sẽ giữ lại cùng project của họ, vì vậy một bản sao đảm bảo họ luôn có sẵn các tệp đó (đồng thời giúp họ tuân thủ các điều khoản cấp phép của bạn).

* Mặc dù Asset Store hỗ trợ nhiều dịch vụ hơn chỉ GitHub, hãy cân nhắc lưu trữ source code của asset trên **GitHub**. Các dịch vụ khác có thể không hoạt động ổn định, và việc không quen thuộc với chúng có thể trở thành rào cản đối với những người đóng góp.

Gửi
---

Sau khi đăng nhập, hãy nhấp vào **Upload Asset** ở phía trên bên phải của website. Bạn sẽ được đưa đến trang sau:

.. image:: img/asset_store_submit.webp

Sau đây là giải thích về từng trường:

* **Publisher**: Đây là tên công khai gắn với asset. Ví dụ: asset XR Tools có publisher là "Godot XR".

* **Publisher Name**: Tên của publisher mới mà bạn đang tạo.

* **Publisher URL Slug**: cách publisher sẽ xuất hiện trong liên kết của nó. Ví dụ: asset XR Tools có URL sau: ``https://store.godotengine.org/asset/godot-xr/godot-xr-tools/``

  Publisher URL Slug trong liên kết đó là "godot-xr".

* **Asset Name**: Tên asset của bạn. Nên là một tiêu đề độc nhất, mang tính mô tả về asset của bạn.

* **Asset URL**: Cách asset sẽ được đặt tên trong liên kết của nó. Ví dụ: asset XR Tools có URL sau: ``https://store.godotengine.org/asset/godot-xr/godot-xr-tools/``

  Asset URL của liên kết đó là "godot-xr-tools".

Sau khi điền các trường đó, hãy đọc và đồng ý với điều khoản dịch vụ, rồi nhấp vào "Continue". Bạn sẽ được đưa đến trang quản lý asset, nơi bạn có thể chỉnh sửa gần như mọi thông tin về cách asset sẽ xuất hiện trên store, cũng như tải lên các phiên bản khác nhau.

.. image:: img/asset_store_management.webp

Các trang quản lý
-----------------

Tổng quan
~~~~~~~~~

Tab tổng quan cho phép bạn gửi asset để xét duyệt. Bạn cũng có thể xem các số liệu phân tích, bao gồm số lượt tải xuống, lượt truy cập trang và số người đã thêm asset vào thư viện của họ.

Bạn cũng có thể xóa asset ở cuối trang từ tab này.

Cài đặt
~~~~~~~

Đây là nơi bạn thiết lập các thông tin chung sau về asset của mình:

* Tóm tắt asset
* Mô tả chi tiết
* Tags
* Asset type (Full Project or Addon)
* License
* Link to source code
* AI usage disclosure (Đây là **bắt buộc** nếu bạn sử dụng AI)

Media
~~~~~

Tab Media là nơi bạn tải lên ảnh thu nhỏ, ảnh chụp màn hình, một hình ảnh cho trang nổi bật nếu muốn, và liên kết đến video YouTube nếu có.

Versions
~~~~~~~~

Đây là nơi bạn tải lên các tệp asset thực tế. Với mỗi phiên bản tải lên, bạn có thể đặt tên, viết changelog và chỉ định phiên bản Godot tối thiểu (và tối đa nếu có). Ngoài ra còn có một trường thông tin bổ sung dành cho mọi nội dung khác.

Mỗi phiên bản riêng lẻ có kích thước tệp tối đa là 1GB.

Pricing
~~~~~~~

Mặc dù hiện chưa thể tải lên các asset trả phí, vẫn có một số cài đặt liên quan đến asset miễn phí
assets. Bạn có thể liên kết đến một trang web khác nơi bạn nhận tiền quyên góp, chẳng hạn như Patreon
hoặc Ko-Fi. Bạn cũng có thể tắt đánh giá nếu muốn (trong tương lai, các asset trả phí sẽ **không** có tùy chọn này).

Submitting for review
---------------------

Khi hoàn tất, hãy nhấn "Submit". Asset của bạn sẽ được đưa vào hàng đợi xét duyệt. Bạn sẽ được thông báo khi asset của mình được xét duyệt. Nếu bị từ chối, bạn sẽ được cho biết lý do có thể dẫn đến việc đó và có thể gửi lại với những thay đổi phù hợp.

.. _`Godot Asset Store`: https://store.godotengine.org/
.. _`Here's a template.`: https://raw.githubusercontent.com/aaronfranke/gitignore/godot/Godot.gitignore
