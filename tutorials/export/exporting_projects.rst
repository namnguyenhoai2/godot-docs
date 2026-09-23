.. _doc_exporting_projects:

Xuất dự án
==========

.. highlight:: none

Tại sao cần xuất?
-----------------

Ban đầu, Godot không có cách nào để xuất dự án. Các nhà phát triển phải tự biên dịch các binary phù hợp và tạo các gói cho từng nền tảng.

Khi ngày càng có nhiều nhà phát triển (và thậm chí cả những người không lập trình) bắt đầu sử dụng nó, đồng thời công ty của chúng tôi bắt đầu thực hiện nhiều dự án hơn cùng lúc, việc này trở thành một điểm nghẽn rõ rệt.

Trên PC
~~~~~~~

Phân phối một dự án game trên PC bằng Godot khá dễ dàng. Đặt binary của Godot trong cùng thư mục với tệp ``project.godot``, sau đó nén thư mục dự án là xong.

Nghe có vẻ đơn giản, nhưng có lẽ nhà phát triển không muốn làm vậy vì một vài lý do. Lý do đầu tiên là việc phân phối quá nhiều tệp có thể không đáng mong muốn. Một số nhà phát triển không thích việc những người dùng tò mò xem cách game được tạo ra, những người khác có thể thấy cách này không thanh lịch, v.v. Một lý do khác là nhà phát triển có thể thích một binary được biên dịch riêng, có kích thước nhỏ hơn, được tối ưu hơn và không bao gồm các công cụ như editor và debugger.

Cuối cùng, Godot có một hệ thống đơn giản nhưng hiệu quả để
:ref:`tạo DLC dưới dạng các tệp gói bổ sung <doc_exporting_pcks>`.

Trên mobile
~~~~~~~~~~~

Cùng kịch bản đó trên các nền tảng mobile có phần phức tạp hơn. Để phân phối một dự án trên các thiết bị này, một binary cho từng nền tảng được tạo, sau đó được thêm vào một dự án native cùng với dữ liệu game.

Điều này có thể gây phiền phức vì nhà phát triển phải làm quen với SDK của từng nền tảng trước khi có thể xuất. Mặc dù việc học từng SDK luôn được khuyến khích, thật khó chịu khi bị buộc phải làm điều đó vào một thời điểm không mong muốn.

Cách tiếp cận này còn có một vấn đề khác: các thiết bị khác nhau thích một số dữ liệu ở những định dạng khác nhau để chạy. Ví dụ điển hình là việc nén texture. Tất cả phần cứng PC đều sử dụng tính năng nén S3TC (BC), vốn đã được chuẩn hóa hơn một thập kỷ, nhưng các thiết bị mobile sử dụng những định dạng khác nhau để nén texture, chẳng hạn như ETC1 và ETC2.

Menu xuất
---------

Sau nhiều lần thử nghiệm các quy trình xuất khác nhau, quy trình hiện tại đã chứng minh là hoạt động tốt nhất. Tại thời điểm viết tài liệu này, chưa phải mọi nền tảng đều được hỗ trợ, nhưng các nền tảng được hỗ trợ vẫn tiếp tục tăng lên.

Để mở menu xuất, hãy nhấp vào nút :button:`Export`:

.. image:: img/export.webp

Menu xuất sẽ mở ra. Tuy nhiên, menu sẽ hoàn toàn trống. Đó là vì chúng ta cần thêm một export preset.

.. image:: img/export_dialog.webp

Để tạo một export preset, hãy nhấp vào nút **Add…** ở đầu menu xuất. Thao tác này sẽ mở một danh sách thả xuống gồm các nền tảng để chọn cho export preset.

.. image:: img/export_preset.webp

Các tùy chọn mặc định thường đã đủ để xuất, vì vậy thường không cần điều chỉnh chúng. Tuy nhiên, nhiều nền tảng yêu cầu cài đặt thêm các công cụ (SDK) để có thể xuất. Ngoài ra, Godot cần cài đặt export templates để tạo các gói. Menu xuất sẽ thông báo khi thiếu thành phần nào đó và sẽ không cho phép người dùng xuất cho nền tảng đó cho đến khi họ khắc phục vấn đề:

.. image:: img/export_error.webp

Khi đó, người dùng được mong đợi quay lại tài liệu và làm theo hướng dẫn về cách thiết lập đúng nền tảng đó.

Các nút ở cuối menu cho phép bạn xuất dự án theo một vài cách khác nhau:

- Export All: Xuất dự án dưới dạng một bản build có thể chơi được (executable của Godot và dữ liệu dự án) cho tất cả preset đã được xác định. Tất cả preset phải có **Export Path** thì mới hoạt động.
- Export Project: Xuất dự án dưới dạng một bản build có thể chơi được (executable của Godot và dữ liệu dự án) cho preset đã chọn.
- Export PCK/ZIP: Xuất tài nguyên dự án dưới dạng gói PCK hoặc ZIP. Đây không phải là bản build có thể chơi được; nó chỉ xuất dữ liệu dự án mà không có executable của Godot.

Export templates
~~~~~~~~~~~~~~~~

Phải cài đặt export templates để xuất dự án. Để quản lý export templates, hãy đi đến :menu:`Editor > Manage Export Templates...`.

.. image:: img/export_templates.webp

Thao tác này sẽ mở trình quản lý export template.

.. image:: img/export_template_manager.webp

Tại đây, bạn có thể xem tất cả export template đã và chưa được cài đặt. Có hai cách để cài đặt export template. Trước tiên, bạn có thể đánh dấu vào ô tương ứng với nền tảng và kiến trúc muốn sử dụng, sau đó nhấp vào nút :button:`Install Selected Templates`.

.. note:: Nếu không chắc mình cần kiến trúc nào, hãy xem trang export của nền tảng để biết mô tả chi tiết.

Bên dưới các tùy chọn nền tảng có một tùy chọn khác tên là :ui:`ICU Data`. Tùy chọn này là bắt buộc đối với emoji và các ngôn ngữ sau:

- Tiếng Miến Điện
- Tiếng Trung
- Tiếng Nhật
- Tiếng Hàn
- Tiếng Khmer Trung Tâm
- Tiếng Lào
- Tiếng Thái

Nếu nhấp vào nút ở góc trên bên phải cửa sổ, bạn có thể cài đặt template từ tệp TPZ (về cơ bản là một kho lưu trữ ZIP). Bạn có thể tải xuống tệp TPZ chứa tất cả export template từ `trang download của website <https://www.godotengine.org/download>`_.

Việc sử dụng tệp TPZ cho tất cả nền tảng không có lợi thế cố hữu nào. Về chức năng, nó hoàn toàn giống nhau và sẽ chiếm nhiều dung lượng hơn so với việc chỉ chọn những gì bạn cần.

.. _doc_exporting_projects_export_mode:

Tùy chọn tài nguyên
~~~~~~~~~~~~~~~~~~~

Khi xuất, Godot lập danh sách tất cả các tệp cần xuất rồi tạo gói. Có 5 chế độ xuất khác nhau:

-  Xuất tất cả tài nguyên trong dự án
-  Xuất các scene đã chọn (và các dependency)
-  Xuất các tài nguyên đã chọn (và các dependency)
-  Xuất tất cả tài nguyên trong dự án ngoại trừ các tài nguyên được đánh dấu bên dưới
-  Xuất dưới dạng dedicated server

.. image:: img/export_resources.webp

**Export all resources in the project** sẽ xuất mọi tài nguyên trong dự án. **Export selected scenes** và **Export selected resources** cung cấp cho bạn danh sách các scene hoặc tài nguyên trong dự án, và bạn phải chọn từng scene hoặc tài nguyên muốn xuất.

.. image:: img/export_selected.webp

**Export all resources in the project except resources checked below** thực hiện đúng như tên gọi: mọi thứ sẽ được xuất, ngoại trừ những gì bạn chọn trong danh sách.

**Export as dedicated server** sẽ loại bỏ tất cả phần hiển thị khỏi dự án và thay thế chúng bằng một placeholder. Điều này bao gồm Cubemap, CubemapArray, Material, Mesh, Texture2D, Texture2DArray, Texture3D. Bạn cũng có thể mở danh sách tệp và chỉ định những tài nguyên hiển thị cụ thể mà bạn muốn giữ lại.

.. note::

    Các tệp và thư mục có tên bắt đầu bằng dấu chấm sẽ không bao giờ được đưa vào project đã export. Điều này nhằm ngăn các thư mục version control như ``.git`` được đưa vào tệp PCK đã export.

Bên dưới danh sách resource là hai bộ lọc có thể thiết lập. Bộ lọc đầu tiên cho phép export các tệp không phải resource như ``.txt``, ``.json`` và ``.csv`` cùng với project. Bộ lọc thứ hai có thể được dùng để loại trừ mọi tệp thuộc một loại nhất định mà không cần bỏ chọn từng tệp. Ví dụ: các tệp ``.png``.

Các tệp cấu hình
----------------

Cấu hình export được lưu trong hai tệp, cả hai đều có thể tìm thấy trong thư mục project:

- ``export_presets.cfg``: Tệp này chứa phần lớn cấu hình export và có thể được commit an toàn vào version control. Tệp này không chứa thông tin nào mà thông thường bạn cần giữ bí mật.
- ``.godot/export_credentials.cfg``: Tệp này chứa các tùy chọn export được xem là bảo mật, chẳng hạn như mật khẩu và khóa mã hóa. Nhìn chung, tệp này **không nên** được commit vào version control hoặc chia sẻ với người khác, trừ khi bạn biết chính xác mình đang làm gì.

Vì tệp thông tin xác thực thường không được đưa vào các hệ thống version control, một số tùy chọn export sẽ bị thiếu nếu bạn clone project sang máy mới. Cách dễ nhất để xử lý việc này là sao chép tệp theo cách thủ công từ vị trí cũ sang vị trí mới.

Export từ command line
----------------------

Trong môi trường production, việc tự động hóa các bản build rất hữu ích, và Godot hỗ trợ điều này bằng các tham số command line ``--export-release`` và ``--export-debug``. Việc export từ command line vẫn yêu cầu một export preset để xác định các tham số export. Cách gọi lệnh cơ bản là:

.. code-block:: shell

    godot --export-release "Windows Desktop" some_name.exe

Lệnh này sẽ export đến ``some_name.exe``, với điều kiện có một preset tên là "Windows Desktop" và template có thể được tìm thấy. (Tên export preset phải được đặt trong dấu ngoặc kép nếu chứa khoảng trắng hoặc ký tự đặc biệt.) Đường dẫn đầu ra là *tương đối* hoặc *tuyệt đối* so với đường dẫn project; **đường dẫn này không phụ thuộc vào thư mục nơi lệnh được gọi**.

Phần mở rộng của tệp đầu ra phải khớp với phần mở rộng được quy trình export của Godot sử dụng:

- Windows: ``.exe``
- macOS: ``.app`` hoặc ``.zip`` (hoặc ``.dmg`` khi export *từ* macOS)
- Linux: Bất kỳ phần mở rộng nào (kể cả không có). ``.x86_64`` thường được dùng cho các binary x86 64-bit.
- HTML5: ``.zip``
- Android: ``.apk``
- iOS: ``.zip``

Bạn cũng có thể cấu hình để *chỉ* export tệp PCK hoặc ZIP, cho phép sử dụng một tệp main pack duy nhất đã export với nhiều executable Godot. Khi làm vậy, tên export preset vẫn phải được chỉ định trên command line:

.. code-block:: shell

    godot --export-pack "Windows Desktop" some_name.pck

Thường sẽ hữu ích khi kết hợp flag ``--export-release`` với flag ``--path``, để bạn không cần ``cd`` đến thư mục project trước khi chạy lệnh:

.. code-block:: shell

    godot --path /path/to/project --export-release "Windows Desktop" some_name.exe

.. seealso::

    Xem :ref:`doc_command_line_tutorial` để biết thêm thông tin về việc sử dụng Godot từ command line.

.. _doc_exporting_projects_pck_versus_zip:

Định dạng tệp pack PCK so với ZIP
---------------------------------

Mỗi định dạng đều có ưu điểm và nhược điểm. PCK là định dạng mặc định và được khuyến nghị cho hầu hết trường hợp sử dụng, nhưng tùy theo nhu cầu, bạn có thể muốn dùng một ZIP archive thay thế.

**Định dạng PCK:**

- Định dạng không nén. Kích thước tệp lớn hơn nhưng tốc độ đọc/ghi nhanh hơn.
- Không thể đọc và ghi bằng các công cụ thường có sẵn trên hệ điều hành của người dùng, mặc dù có `công cụ bên thứ ba <https://github.com/hhyyrylainen/GodotPckTool>`__ để giải nén và tạo tệp PCK.

**Định dạng ZIP:**

- Định dạng đã nén. Kích thước tệp nhỏ hơn nhưng tốc độ đọc/ghi chậm hơn.
- Có thể đọc và ghi bằng các công cụ thường có sẵn trên hệ điều hành của người dùng. Điều này có thể hữu ích để giúp việc modding trở nên dễ dàng hơn (xem thêm :ref:`doc_exporting_pcks`).

.. warning::

    Do một `lỗi đã biết <https://github.com/godotengine/godot/pull/42123>`__, khi dùng tệp ZIP làm tệp pack, binary đã export sẽ không tự động thử sử dụng tệp đó. Vì vậy, bạn phải tạo một *launcher script* mà người chơi có thể nhấp đúp hoặc chạy từ terminal để khởi chạy project:

    ::

        :: launch.bat (Windows)
        @echo off
        my_project.exe --main-pack my_project.zip

        # launch.sh (Linux)
        ./my_project.x86_64 --main-pack my_project.zip

    Lưu launcher script và đặt nó trong cùng thư mục với binary đã export. Trên Linux, hãy cấp quyền thực thi cho launcher script bằng lệnh ``chmod +x launch.sh``.

.. _`download page of the website`: https://www.godotengine.org/download
