.. _doc_submitting_to_assetlib:

Gửi lên Asset Library
=====================

Giới thiệu
----------

Hướng dẫn này nhằm chỉ cho bạn cách gửi các asset của riêng mình lên `Godot Asset Library <https://godotengine.org/asset-library/asset>`_ và chia sẻ chúng với cộng đồng Godot.

Như đã đề cập trong tài liệu :ref:`doc_using_assetlib`, để có thể gửi asset lên AssetLib, bạn cần có một tài khoản đã đăng ký và phải đăng nhập.

Hướng dẫn gửi
-------------

Trước khi gửi asset, hãy đảm bảo asset tuân thủ tất cả các yêu cầu, đồng thời cân nhắc làm theo các khuyến nghị.

Yêu cầu
~~~~~~~

Nói chung, hầu hết các asset mà mọi người gửi lên thư viện asset đều được chấp nhận. Tuy nhiên, để asset của bạn được chấp nhận, asset cần đáp ứng một số yêu cầu để được phê duyệt.

* Asset phải **hoạt động**. Nếu asset không chạy hoặc không hoạt động theo cách khác trong phiên bản Godot đã chỉ định, asset sẽ bị từ chối.

* Asset phải có tệp **.gitignore** phù hợp. Việc loại bỏ dữ liệu dư thừa khỏi kho lưu trữ là rất quan trọng. `Đây là một mẫu. <https://raw.githubusercontent.com/aaronfranke/gitignore/godot/Godot.gitignore>`_

* Không được có **submodule**, hoặc mọi submodule phải không thiết yếu. GitHub không bao gồm submodule trong tệp ZIP đã tải xuống, vì vậy nếu asset cần nội dung của submodule thì asset sẽ không hoạt động.

* **Giấy phép** phải chính xác. Giấy phép được liệt kê trên thư viện asset phải khớp với giấy phép trong kho lưu trữ. Repo BẮT BUỘC phải có tệp giấy phép, được đặt tên là "LICENSE" hoặc "LICENSE.md". Tệp này phải chứa chính nội dung giấy phép và một tuyên bố bản quyền bao gồm (các) năm cùng chủ sở hữu bản quyền.

* Hãy sử dụng **tiếng Anh** chuẩn cho tên và phần mô tả asset. Điều này bao gồm việc viết hoa đúng cách và sử dụng các câu đầy đủ trong phần mô tả. Bạn cũng có thể thêm các ngôn ngữ khác, nhưng ít nhất phải có phiên bản tiếng Anh.

* Liên kết biểu tượng phải là **liên kết trực tiếp**. Đối với các biểu tượng được lưu trữ trên GitHub, liên kết phải bắt đầu bằng "raw.githubusercontent.com", không phải "github.com".

Khuyến nghị
~~~~~~~~~~~

Những điều này không bắt buộc để asset của bạn được phê duyệt, nhưng nếu làm theo các khuyến nghị này, bạn có thể góp phần giúp thư viện asset trở thành một nơi tốt hơn cho tất cả người dùng.

* Khi tạo asset không phải dự án, thông lệ phổ biến là đặt các tệp của bạn bên trong thư mục **addons/asset_name/**. Hãy làm vậy để tránh các tệp của bạn xung đột với những asset khác hoặc với các tệp của người dùng cài đặt asset của bạn. Thư mục này sẽ **không** được tự động tạo khi người dùng cài đặt asset của bạn.

* Sửa hoặc ẩn tất cả **cảnh báo** của tập lệnh. Hệ thống cảnh báo giúp xác định các vấn đề trong mã của bạn, nhưng những người sử dụng asset không cần phải thấy chúng.

* Hãy làm cho mã của bạn tuân theo các **hướng dẫn về phong cách** chính thức. Việc duy trì phong cách nhất quán giúp người khác đọc mã của bạn và cũng hữu ích nếu người khác muốn đóng góp cho asset của bạn. Xem:
  :ref:`doc_gdscript_styleguide` or the :ref:`doc_c_sharp_styleguide`.

* Nếu repo của bạn có ảnh chụp màn hình, hãy đặt chúng trong một thư mục con riêng và thêm một tệp **.gdignore** trống vào cùng thư mục đó (lưu ý: **gd**, không phải **git**). Điều này ngăn Godot nhập các ảnh chụp màn hình của bạn. Trên Windows, hãy mở dấu nhắc lệnh trong thư mục dự án và chạy ``type nul > .gdignore`` để tạo một tệp có tên bắt đầu bằng dấu chấm.

* Nếu asset của bạn là một thư viện dùng để làm việc với các tệp khác, hãy cân nhắc đưa **các tệp ví dụ** vào asset.

* Hãy cân nhắc thêm tệp **.gitattributes** vào repo của bạn. Tệp này cho phép cung cấp các chỉ dẫn bổ sung cho Git, chẳng hạn như chỉ định ký tự kết thúc dòng và liệt kê các tệp không cần thiết để asset hoạt động bằng chỉ thị ``export-ignore``. Chỉ thị này loại bỏ các tệp đó khỏi tệp ZIP kết quả, ngăn người dùng thư viện asset tải chúng xuống. Sau đây là các ví dụ phổ biến về **.gitattributes**:

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

* Nếu bạn đang gửi một plugin, hãy thêm một **bản sao** giấy phép và readme vào chính thư mục plugin. Đây là thư mục mà người dùng chắc chắn sẽ giữ lại cùng với dự án của họ, vì vậy bản sao đảm bảo họ luôn có sẵn các tệp đó (đồng thời giúp họ tuân thủ các điều khoản cấp phép của bạn).

* Mặc dù thư viện asset hỗ trợ nhiều dịch vụ hơn chỉ GitHub, hãy cân nhắc lưu trữ mã nguồn asset của bạn trên **GitHub**. Các dịch vụ khác có thể không hoạt động ổn định, và việc thiếu quen thuộc có thể trở thành rào cản đối với những người đóng góp.

Gửi lên
-------

Sau khi đăng nhập, bạn có thể chuyển đến trang "Submit Assets" của AssetLib, trang này sẽ có dạng như sau:

|image0|

Mặc dù có thể trông khá nhiều (và còn có thêm nội dung khi bạn cuộn xuống), mỗi trường đều được mô tả về nội dung bạn nên nhập. Tuy vậy, chúng ta vẫn sẽ xem qua các thông tin bắt buộc trong biểu mẫu gửi ở đây.

* **Asset Name**: Tên của asset. Nên là một tiêu đề duy nhất và có tính mô tả về asset của bạn. * **Category**: Danh mục mà asset của bạn thuộc về và sẽ được hiển thị trong kết quả tìm kiếm. Danh mục được chia thành **Addons** và **Projects**. Trong trình chỉnh sửa, các asset thuộc loại Project (Templates, Demos, Projects) chỉ hiển thị khi xem AssetLib từ Project Manager, trong khi các asset thuộc loại Addon chỉ hiển thị bên trong một dự án. * **Godot version**: Phiên bản engine mà asset hoạt động cùng. Hiện tại, một mục asset không thể chứa các bản tải xuống cho nhiều phiên bản engine, vì vậy bạn có thể cần gửi lại asset nhiều lần, với mỗi mục dành cho một phiên bản Godot mà asset hỗ trợ. Điều này đặc biệt quan trọng khi làm việc với các phiên bản chính của engine, chẳng hạn như Godot 2.x và Godot 3.x. * **Version**: Số phiên bản của asset. Mặc dù bạn có thể tự do chọn và sử dụng bất kỳ quy ước đánh số phiên bản nào, bạn có thể tham khảo một quy ước như `SemVer <https://semver.org>`_ nếu muốn quy ước phiên bản của asset rõ ràng và nhất quán. Lưu ý rằng cũng có một số phiên bản nội bộ, được tăng lên mỗi khi URL tải xuống asset được thay đổi hoặc cập nhật. * **Repository host**: Các asset được tải lên AssetLib không được lưu trữ trực tiếp trên đó. Thay vào đó, chúng trỏ đến các kho lưu trữ được lưu trữ trên các nhà cung cấp Git bên thứ ba, chẳng hạn như GitHub, GitLab hoặc Bitbucket. Đây là nơi bạn chọn nhà cung cấp mà asset sử dụng, để trang web có thể tính toán liên kết tải xuống cuối cùng. * **Repository URL**: URL đến các tệp/trang web của asset. URL này sẽ thay đổi tùy theo lựa chọn nhà cung cấp của bạn, nhưng sẽ có dạng tương tự `https://github.com/<user>/<project>`. * **Issues URL**: URL đến trình theo dõi vấn đề của asset. Một lần nữa, URL này sẽ khác nhau tùy từng nhà cung cấp kho lưu trữ, nhưng có thể sẽ có dạng tương tự `https://github.com/<user>/<project>/issues`. Bạn có thể để trống trường này nếu sử dụng trình theo dõi vấn đề của nhà cung cấp và trình theo dõi đó thuộc cùng một kho lưu trữ. * **Download Commit**: Commit của asset. Ví dụ: `b1d3172f89b86e52465a74f63a74ac84c491d3e1`. Trang web sẽ tính toán URL tải xuống thực tế từ giá trị này. * **Icon URL**: URL đến biểu tượng của asset (được dùng làm hình thu nhỏ trong kết quả tìm kiếm AssetLib và trên trang của asset). Phải là hình ảnh ở định dạng PNG hoặc JPG.

    **Biểu tượng** phải có dạng hình vuông (tỷ lệ khung hình 1:1). Biểu tượng nên có độ phân giải tối thiểu là 128×128 pixel.

.. note::

    Đối với các biểu tượng được lưu trữ trên GitHub, URL phải được cung cấp theo dạng `https://raw.githubusercontent.com/<user>/<project>/<branch>/Icon.png`.

* **License**: Giấy phép theo đó bạn phân phối asset. Danh sách bao gồm nhiều giấy phép phần mềm miễn phí và nguồn mở, chẳng hạn như GPL (v2 và v3), MIT, BSD và Boost Software License. Bạn có thể truy cập `OpenSource.org <https://opensource.org>`_ để xem mô tả chi tiết về từng giấy phép được liệt kê. * **Description**: Cuối cùng, bạn có thể sử dụng trường Description để trình bày tổng quan bằng văn bản về asset, các tính năng và hành vi của asset, nhật ký thay đổi, v.v. Trong tương lai, định dạng bằng Markdown sẽ được hỗ trợ, nhưng hiện tại, lựa chọn duy nhất của bạn là văn bản thuần túy.

Bạn cũng có thể thêm tối đa ba bản xem trước dạng video và/hoặc hình ảnh, chúng sẽ được hiển thị ở cuối trang asset. Sử dụng hộp kiểm "Enable" trên mỗi hộp gửi bản xem trước để bật chúng.

* **Type**: Hình ảnh hoặc video. * **Image/YouTube URL**: Liên kết đến hình ảnh hoặc video được lưu trữ trên YouTube. * **Thumbnail URL**: URL đến hình ảnh sẽ được sử dụng làm hình thu nhỏ cho bản xem trước. Tùy chọn này cuối cùng sẽ bị loại bỏ và hình thu nhỏ sẽ được tự động tính toán.

Khi hoàn tất, hãy nhấn "Submit". Asset của bạn sẽ được đưa vào hàng đợi đánh giá. Bạn có thể xem tất cả asset hiện đang chờ đánh giá `tại đây <https://godotengine.org/asset-library/asset/edit?&asset=-1>`_ . Quy trình phê duyệt được thực hiện thủ công và có thể mất đến vài ngày để asset của bạn được chấp nhận (hoặc bị từ chối), vì vậy hãy kiên nhẫn!

Bạn sẽ được thông báo khi asset của mình được đánh giá. Nếu bị từ chối, bạn sẽ được cho biết lý do có thể dẫn đến việc đó và có thể gửi lại asset với những thay đổi phù hợp.

.. |image0| image:: img/assetlib_submit.png
