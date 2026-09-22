.. _doc_submitting_to_assetlib:

Gửi lên Asset Library
=====================

Giới thiệu
----------

Hướng dẫn này nhằm cung cấp chỉ dẫn về cách bạn có thể gửi các asset của riêng mình lên `Godot Asset Library <https://godotengine.org/asset-library/asset>`_ và chia sẻ chúng với cộng đồng Godot.

Như đã đề cập trong tài liệu :ref:`doc_using_assetlib`, để có thể gửi tài sản lên AssetLib, bạn cần có tài khoản đã đăng ký và đăng nhập vào tài khoản đó.

Nguyên tắc gửi
--------------

Trước khi gửi asset, hãy đảm bảo asset đáp ứng tất cả các yêu cầu, đồng thời cân nhắc làm theo các khuyến nghị.

Yêu cầu
~~~~~~~

Nói chung, hầu hết các asset mà mọi người gửi lên asset library đều được chấp nhận. Tuy nhiên, để asset của bạn được chấp nhận, asset cần đáp ứng một số yêu cầu để được phê duyệt.

* Asset phải **hoạt động**. Nếu asset không chạy hoặc không hoạt động theo cách khác trong phiên bản Godot đã chỉ định, asset sẽ bị từ chối.

* Asset phải có tệp **.gitignore** phù hợp. Điều quan trọng là phải loại bỏ dữ liệu dư thừa khỏi repository. `Đây là một mẫu. <https://raw.githubusercontent.com/aaronfranke/gitignore/godot/Godot.gitignore>`_

* Không được có **submodule**, hoặc mọi submodule phải không thiết yếu. GitHub không đưa submodule vào tệp ZIP đã tải xuống, vì vậy nếu asset cần nội dung của submodule thì asset của bạn sẽ không hoạt động.

* **Giấy phép** cần chính xác. Giấy phép được liệt kê trên asset library phải khớp với giấy phép trong repository. Repo BẮT BUỘC phải có tệp giấy phép, được đặt tên là "LICENSE" hoặc "LICENSE.md". Tệp này phải chứa chính nội dung giấy phép và một tuyên bố bản quyền bao gồm (các) năm và chủ sở hữu bản quyền.

* Hãy sử dụng **tiếng Anh** chuẩn cho tên và phần mô tả asset. Điều này bao gồm việc viết hoa đúng cách và sử dụng các câu đầy đủ trong phần mô tả. Bạn cũng có thể thêm các ngôn ngữ khác, nhưng ít nhất phải có một phiên bản tiếng Anh.

* Liên kết biểu tượng phải là một **liên kết trực tiếp**. Đối với các biểu tượng được lưu trữ trên GitHub, liên kết phải bắt đầu bằng "raw.githubusercontent.com", không phải "github.com".

Khuyến nghị
~~~~~~~~~~~

Những điều này không bắt buộc để asset của bạn được phê duyệt, nhưng nếu làm theo các khuyến nghị này, bạn có thể góp phần làm cho asset library trở thành nơi tốt hơn cho mọi người dùng.

* Khi tạo các asset không phải project, thông lệ phổ biến là đặt các tệp của bạn bên trong thư mục **addons/asset_name/**. Hãy làm vậy để tránh các tệp của bạn xung đột với những asset khác hoặc với các tệp của người dùng cài đặt asset của bạn. Thư mục này sẽ **không** được tự động tạo khi người dùng cài đặt asset của bạn.

* Sửa hoặc ẩn tất cả **cảnh báo** của script. Hệ thống cảnh báo được dùng để giúp xác định các vấn đề trong code của bạn, nhưng những người sử dụng asset của bạn không cần nhìn thấy chúng.

* Làm cho code của bạn tuân theo **hướng dẫn về style** chính thức. Một style nhất quán giúp người khác đọc code của bạn, đồng thời cũng hữu ích nếu người khác muốn đóng góp cho asset của bạn. Xem:
  :ref:`doc_gdscript_styleguide` hoặc :ref:`doc_c_sharp_styleguide`.

* Nếu repo của bạn có ảnh chụp màn hình, hãy đặt chúng trong một thư mục con riêng và thêm một tệp **.gdignore** rỗng vào cùng thư mục đó (lưu ý: **gd**, không phải **git**). Điều này ngăn Godot import các ảnh chụp màn hình của bạn. Trên Windows, hãy mở command prompt trong thư mục project và chạy ``type nul > .gdignore`` để tạo một tệp có tên bắt đầu bằng dấu chấm.

* Nếu asset của bạn là một library dùng để làm việc với các tệp khác, hãy cân nhắc đưa **các tệp ví dụ** vào asset.

* Hãy cân nhắc thêm tệp **.gitattributes** vào repo. Tệp này cho phép cung cấp thêm chỉ dẫn cho Git, chẳng hạn như chỉ định ký tự kết thúc dòng và liệt kê các tệp không cần thiết để asset của bạn hoạt động với ``export-ignore``
  directive. Chỉ thị này loại bỏ các tệp đó khỏi tệp ZIP kết quả,
  ngăn không cho người dùng asset library tải chúng xuống. Đây là các ví dụ phổ biến về **.gitattributes**:

  .. tabs::

   .. tab:: Projects / Templates

      .. code-block:: shell

        # Normalize line endings for all files that Git considers text files.
        * text=auto eol=lf

   .. tab:: Addons / Asset Packs

      .. code-block:: shell

        # Normalize line endings for all files that Git considers text files.
        * text=auto eol=lf

        # Only include the addons folder when downloading from the Asset Library.
        /**        export-ignore
        /addons    !export-ignore
        /addons/** !export-ignore

* Nếu bạn đang gửi một plugin, hãy thêm một **bản sao** giấy phép và readme của bạn vào chính thư mục plugin. Đây là thư mục mà người dùng chắc chắn sẽ giữ lại cùng với project của họ, vì vậy một bản sao đảm bảo họ luôn có sẵn các tệp đó (đồng thời giúp họ tuân thủ các điều khoản cấp phép của bạn).

* Mặc dù asset library cho phép sử dụng nhiều dịch vụ chứ không chỉ GitHub, hãy cân nhắc lưu trữ source code của asset trên **GitHub**. Các dịch vụ khác có thể không hoạt động ổn định, và việc thiếu quen thuộc có thể trở thành rào cản đối với những người đóng góp.

Gửi
---

Sau khi đăng nhập, bạn có thể truy cập trang "Submit Assets" của AssetLib, trang này sẽ có dạng như sau:

|image0|

Mặc dù có thể trông khá nhiều thông tin (và còn nhiều hơn khi bạn cuộn xuống), mỗi trường đều được mô tả về nội dung bạn nên nhập. Tuy vậy, chúng ta vẫn sẽ xem qua những nội dung bắt buộc trong biểu mẫu gửi tại đây.

* **Asset Name**:
    Tên asset của bạn. Nên là tiêu đề duy nhất, mang tính mô tả về asset của bạn.
* **Category**:
    Danh mục mà asset của bạn thuộc về và sẽ được hiển thị trong kết quả tìm kiếm. Danh mục này được chia thành **Addons** và **Projects**. Trong editor, các asset thuộc loại Project (Templates, Demos, Projects) chỉ xuất hiện khi xem AssetLib từ Project Manager, còn các asset thuộc loại Addon chỉ hiển thị bên trong một project.
* **Godot version**:
    Phiên bản engine mà asset hoạt động cùng. Hiện tại, không thể để một mục asset duy nhất chứa các bản tải xuống cho nhiều phiên bản engine, vì vậy bạn có thể cần gửi lại asset nhiều lần, với một mục cho mỗi phiên bản Godot mà asset hỗ trợ. Điều này đặc biệt quan trọng khi làm việc với các phiên bản chính của engine, chẳng hạn như Godot 2.x và Godot 3.x.
* **Version**:
    Số phiên bản của asset. Mặc dù bạn có thể tự do chọn và sử dụng bất kỳ quy ước đánh số phiên bản nào, bạn có thể tìm hiểu một quy ước như `SemVer <https://semver.org>`_ nếu muốn quy ước phiên bản của asset rõ ràng và nhất quán. Lưu ý rằng cũng có một số phiên bản nội bộ, được tăng lên mỗi khi URL tải xuống asset bị thay đổi hoặc cập nhật.
* **Repository host**:
    Các asset được tải lên AssetLib không được lưu trữ trên đó
    directly. Thay vào đó, chúng trỏ đến các repository được lưu trữ trên các nhà cung cấp Git bên thứ ba,
    chẳng hạn như GitHub, GitLab hoặc Bitbucket. Đây là nơi bạn chọn provider mà asset của mình sử dụng, để site có thể tính toán liên kết tải xuống cuối cùng.
* **Repository URL**:
    URL đến các tệp/trang web của asset. URL này sẽ thay đổi tùy theo provider bạn chọn, nhưng thường sẽ có dạng tương tự `https://github.com/<user>/<project>`.
* **Issues URL**:
    URL đến issue tracker của asset. Tương tự, URL này sẽ khác nhau tùy repository host, nhưng có thể sẽ có dạng tương tự `https://github.com/<user>/<project>/issues`. Bạn có thể để trống trường này nếu sử dụng issue tracker của provider và issue tracker đó thuộc cùng một repository.
* **Download Commit**:
    Commit của asset. Ví dụ: `b1d3172f89b86e52465a74f63a74ac84c491d3e1`. Site sẽ dùng thông tin này để tính URL tải xuống thực tế.
* **Icon URL**:
    URL đến icon của asset (được dùng làm thumbnail trong kết quả tìm kiếm AssetLib và trên trang của asset). Đây phải là hình ảnh ở định dạng PNG hoặc JPG.

    **Icon** phải là hình vuông (tỷ lệ khung hình 1:1). Độ phân giải tối thiểu nên là 128×128 pixel.

.. note::

    Đối với các icon được lưu trữ trên GitHub, URL phải được cung cấp theo dạng `https://raw.githubusercontent.com/<user>/<project>/<branch>/Icon.png`.

* **License**:
    License theo đó bạn phân phối asset. Danh sách bao gồm nhiều license phần mềm miễn phí và mã nguồn mở, chẳng hạn như GPL (v2 và v3), MIT, BSD và Boost Software License. Bạn có thể truy cập `OpenSource.org <https://opensource.org>`_ để xem mô tả chi tiết về từng license trong danh sách.
* **Description**:
    Cuối cùng, bạn có thể sử dụng trường Description để trình bày bằng văn bản về asset, các tính năng và hành vi của asset, changelog, v.v. Trong tương lai, hệ thống sẽ hỗ trợ định dạng bằng Markdown, nhưng hiện tại, lựa chọn duy nhất của bạn là văn bản thuần túy.

Bạn cũng có thể thêm tối đa ba bản xem trước dạng video và/hoặc hình ảnh, được hiển thị ở cuối trang asset. Sử dụng checkbox "Enable" trên mỗi hộp gửi bản xem trước để bật chúng.

* **Type**:
    Hình ảnh hoặc video.
* **Image/YouTube URL**:
    Liên kết đến hình ảnh hoặc video được lưu trữ trên YouTube.
* **Thumbnail URL**:
    URL đến hình ảnh sẽ được dùng làm thumbnail cho
    preview. Tùy chọn này cuối cùng sẽ bị xóa và thumbnail sẽ được tự động
    tính toán thay thế.

Sau khi hoàn tất, hãy nhấn "Submit". Asset của bạn sẽ được đưa vào hàng đợi review. Bạn có thể xem tất cả asset hiện đang chờ review `here <https://godotengine.org/asset-library/asset/edit?&asset=-1>`_ . Quy trình phê duyệt được thực hiện thủ công và có thể mất vài ngày để asset của bạn được chấp thuận (hoặc từ chối), vì vậy hãy kiên nhẫn!

Bạn sẽ được thông báo khi asset của mình được review. Nếu bị từ chối, bạn sẽ được cho biết lý do và có thể gửi lại asset với những thay đổi phù hợp.

.. |image0| image:: img/assetlib_submit.png

.. _`Godot Asset Library`: https://godotengine.org/asset-library/asset
.. _`Here's a template.`: https://raw.githubusercontent.com/aaronfranke/gitignore/godot/Godot.gitignore
.. _`SemVer`: https://semver.org
.. _`OpenSource.org`: https://opensource.org
.. _`here`: https://godotengine.org/asset-library/asset/edit?&asset=-1
