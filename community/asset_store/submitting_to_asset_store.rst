.. _doc_submitting_to_asset_store:

Gửi lên Asset Store
===================

Giới thiệu
----------

Hướng dẫn này nhằm cung cấp chỉ dẫn về cách bạn có thể gửi các asset của mình lên `Godot Asset Store <https://store.godotengine.org/>`_ và chia sẻ chúng với cộng đồng Godot.

Như đã đề cập trên trang :ref:`doc_using_asset_store_website`, để có thể gửi asset lên Asset Store, bạn cần có một tài khoản đã đăng ký và đăng nhập vào tài khoản đó.

Hướng dẫn gửi
-------------

Trước khi gửi asset, hãy đảm bảo asset đáp ứng tất cả các yêu cầu, đồng thời cân nhắc làm theo các khuyến nghị.

Yêu cầu
~~~~~~~

Nói chung, hầu hết các asset mọi người gửi lên Asset Store đều được chấp nhận. Tuy nhiên, để asset được chấp nhận, asset cần đáp ứng một số yêu cầu để được phê duyệt.

* Asset phải **hoạt động**. Nếu asset không chạy hoặc không hoạt động theo cách nào đó trong phiên bản Godot đã chỉ định, asset sẽ bị từ chối.

* Asset phải có tệp **.gitignore** phù hợp. Việc loại bỏ dữ liệu dư thừa khỏi repository là rất quan trọng. `Đây là một mẫu. <https://raw.githubusercontent.com/aaronfranke/gitignore/godot/Godot.gitignore>`_

* Không được có **submodule**, hoặc mọi submodule phải không thiết yếu. GitHub không đưa submodule vào tệp ZIP đã tải xuống, vì vậy nếu asset cần nội dung của submodule thì asset sẽ không hoạt động.

* **Giấy phép** phải chính xác. Giấy phép được liệt kê trên Asset Store phải khớp với giấy phép trong repository. Repo **phải** có một tệp giấy phép, có tên là "LICENSE" hoặc "LICENSE.md". Tệp này phải chứa chính nội dung giấy phép và một tuyên bố bản quyền bao gồm (các) năm và chủ sở hữu bản quyền.

* Hãy sử dụng **tiếng Anh** đúng chuẩn cho tên và phần mô tả asset. Điều này bao gồm việc viết hoa đúng cách và sử dụng các câu hoàn chỉnh trong phần mô tả. Bạn cũng có thể thêm các ngôn ngữ khác, nhưng ít nhất phải có một phiên bản tiếng Anh.

* Liên kết biểu tượng phải là một **liên kết trực tiếp**. Đối với các biểu tượng được lưu trữ trên GitHub, liên kết phải bắt đầu bằng "raw.githubusercontent.com", không phải "github.com".

Khuyến nghị
~~~~~~~~~~~

Những điều này không bắt buộc để asset được phê duyệt, nhưng nếu làm theo các khuyến nghị này, bạn có thể góp phần làm cho asset store trở thành một nơi tốt hơn đối với tất cả người dùng.

* Khi tạo các asset không phải project, thông lệ phổ biến là đặt các tệp của bạn bên trong thư mục **addons/asset_name/**. Hãy làm như vậy để tránh các tệp của bạn xung đột với những asset khác hoặc với các tệp của người dùng cài đặt asset của bạn. Thư mục này sẽ **không** được tự động tạo khi người dùng cài đặt asset của bạn.

* Hãy sửa hoặc ẩn tất cả **cảnh báo** của script. Hệ thống cảnh báo nhằm giúp xác định các vấn đề trong mã của bạn, nhưng những người sử dụng asset của bạn không cần nhìn thấy chúng.

* Hãy đảm bảo mã của bạn tuân theo các **hướng dẫn về phong cách** chính thức. Việc duy trì phong cách nhất quán giúp người khác đọc mã của bạn, đồng thời cũng hữu ích nếu người khác muốn đóng góp cho asset của bạn. Xem
  :ref:`doc_gdscript_styleguide` or the :ref:`doc_c_sharp_styleguide`.

* Nếu repo của bạn có ảnh chụp màn hình, hãy đặt chúng trong một thư mục con riêng và thêm một tệp **.gdignore** trống vào cùng thư mục đó (lưu ý: **gd**, không phải **git**). Điều này ngăn Godot nhập các ảnh chụp màn hình của bạn. Trên Windows, hãy mở dấu nhắc lệnh trong thư mục project và chạy ``type nul > .gdignore`` để tạo một tệp có tên bắt đầu bằng dấu chấm.

* Nếu asset của bạn là một thư viện dùng để làm việc với các tệp khác, hãy cân nhắc đưa **các tệp ví dụ** vào asset.

* Hãy cân nhắc thêm một tệp **.gitattributes** vào repo của bạn. Tệp này cho phép cung cấp thêm hướng dẫn cho Git, chẳng hạn như chỉ định ký tự kết thúc dòng và liệt kê các tệp không cần thiết để asset hoạt động bằng chỉ thị ``export-ignore``. Chỉ thị này loại bỏ các tệp đó khỏi tệp ZIP kết quả, ngăn người dùng Asset Store tải chúng xuống. Sau đây là các ví dụ phổ biến về **.gitattributes**:

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

* Nếu bạn đang gửi một plugin, hãy thêm một **bản sao** giấy phép và readme vào chính thư mục plugin. Đây là thư mục mà người dùng chắc chắn sẽ giữ lại cùng với project của họ, vì vậy một bản sao đảm bảo họ luôn có sẵn các tệp đó (đồng thời giúp họ tuân thủ các điều khoản cấp phép của bạn).

* Mặc dù Asset Store hỗ trợ nhiều dịch vụ không chỉ GitHub, hãy cân nhắc lưu trữ mã nguồn asset của bạn trên **GitHub**. Các dịch vụ khác có thể không hoạt động ổn định, và việc thiếu sự quen thuộc có thể trở thành rào cản đối với những người đóng góp.

Gửi lên
-------

Sau khi đăng nhập, hãy nhấp vào **Upload Asset** ở phía trên bên phải trang web. Bạn sẽ được chuyển đến trang sau:

.. image:: img/asset_store_submit.webp

Dưới đây là giải thích về từng trường:

* **Publisher**: Đây là tên công khai gắn với asset. Ví dụ, asset XR Tools có publisher là "Godot XR".

* **Publisher Name**: Tên của publisher mới mà bạn đang tạo.

* **Publisher URL Slug**: cách publisher sẽ xuất hiện trong liên kết của nó. Ví dụ, asset XR Tools có URL sau: ``https://store.godotengine.org/asset/godot-xr/godot-xr-tools/``

  Publisher URL Slug trong đó là "godot-xr".

* **Asset Name**: Tên của asset. Nên là một tiêu đề độc đáo, mô tả rõ asset của bạn là gì.

* **Asset URL**: Cách asset sẽ được đặt tên trong liên kết của nó. Ví dụ, asset XR Tools có URL sau: ``https://store.godotengine.org/asset/godot-xr/godot-xr-tools/``

  Asset URL của liên kết đó là "godot-xr-tools".

Sau khi điền các trường đó, hãy đọc và đồng ý với điều khoản dịch vụ, rồi nhấp vào "Continue". Bạn sẽ được đưa đến trang quản lý của asset, nơi bạn có thể chỉnh sửa hầu hết mọi thông tin về cách asset sẽ xuất hiện trên cửa hàng, cũng như tải lên các phiên bản khác nhau.

.. image:: img/asset_store_management.webp

Các trang quản lý
-----------------

Tổng quan
~~~~~~~~~

Tab tổng quan cho phép bạn gửi asset để xem xét. Bạn cũng có thể xem các số liệu, bao gồm số lần asset được tải xuống, số lượt truy cập trang và số người đã thêm asset vào thư viện của họ.

Bạn cũng có thể xóa asset ở cuối trang từ tab này.

Cài đặt
~~~~~~~

Đây là tab nơi bạn thiết lập các thông tin chung sau về asset của mình:

* Tóm tắt asset * Mô tả chi tiết * Thẻ * Loại asset (Full Project hoặc Addon) * Giấy phép * Liên kết đến mã nguồn * Khai báo việc sử dụng AI (Điều này **bắt buộc** nếu bạn sử dụng AI)

Phương tiện
~~~~~~~~~~~

Tab phương tiện là nơi bạn tải lên hình thu nhỏ, ảnh chụp màn hình, một hình ảnh cho trang nổi bật nếu muốn và liên kết đến video YouTube nếu có.

Các phiên bản
~~~~~~~~~~~~~

Đây là nơi bạn tải lên các tệp asset thực tế. Với mỗi phiên bản tải lên, bạn có thể đặt tên, viết changelog và chỉ định phiên bản Godot tối thiểu (và tối đa nếu có). Ngoài ra còn có một trường thông tin bổ sung dành cho mọi nội dung khác.

Mỗi phiên bản riêng lẻ có kích thước tệp tối đa là 1GB.

Giá
~~~

Mặc dù hiện chưa thể tải lên các asset trả phí, một số cài đặt vẫn liên quan đến asset miễn phí. Bạn có thể liên kết đến một trang web khác để nhận tiền quyên góp, chẳng hạn như Patreon hoặc Ko-Fi. Bạn cũng có thể tắt đánh giá nếu muốn (trong tương lai, các asset trả phí sẽ **không** có tùy chọn này).

Gửi để xem xét
--------------

Sau khi hoàn tất, hãy nhấn "Submit". Asset của bạn sẽ được đưa vào hàng đợi xem xét. Bạn sẽ được thông báo khi asset được xem xét. Nếu bị từ chối, bạn sẽ được cho biết lý do có thể dẫn đến việc đó và có thể gửi lại asset sau khi thực hiện các thay đổi phù hợp.
