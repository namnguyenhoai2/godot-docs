.. _doc_exporting_projects:

Xuất project
============

.. highlight:: none

Tại sao cần xuất?
-----------------

Ban đầu, Godot không có cách nào để xuất project. Các developer phải tự biên dịch binary phù hợp và build package cho từng platform.

Khi ngày càng có nhiều developer (và thậm chí cả những người không lập trình) bắt đầu sử dụng nó, đồng thời công ty của chúng tôi bắt đầu thực hiện nhiều project cùng lúc hơn, rõ ràng đây là một nút thắt cổ chai.

Trên PC
~~~~~~~

Phân phối một game project trên PC bằng Godot khá dễ. Đặt Godot binary vào cùng thư mục với file ``project.godot``, sau đó nén thư mục project là xong.

Nghe có vẻ đơn giản, nhưng có lẽ có một vài lý do khiến developer không muốn làm vậy. Lý do đầu tiên là việc phân phối quá nhiều file có thể không phù hợp. Một số developer có thể không thích việc những người dùng tò mò xem cách game được tạo ra, những người khác có thể thấy cách này thiếu gọn gàng, v.v. Một lý do khác là developer có thể muốn sử dụng một binary được biên dịch đặc biệt, có kích thước nhỏ hơn, được tối ưu hơn và không bao gồm các tool như editor và debugger.

Cuối cùng, Godot có một hệ thống đơn giản nhưng hiệu quả cho
:ref:`creating DLCs as extra package files <doc_exporting_pcks>`.

Trên mobile
~~~~~~~~~~~

Tình huống tương tự trên các mobile platform tệ hơn một chút. Để phân phối một project trên các thiết bị đó, binary cho từng platform được build, sau đó được thêm vào một native project cùng với game data.

Điều này có thể gây phiền phức vì developer phải làm quen với SDK của từng platform trước khi có thể export. Mặc dù việc học từng SDK luôn được khuyến khích, việc bị buộc phải làm điều đó vào một thời điểm không mong muốn có thể gây khó chịu.

Cách tiếp cận này còn có một vấn đề khác: các thiết bị khác nhau ưu tiên một số data ở các format khác nhau để chạy. Ví dụ điển hình là texture compression. Tất cả phần cứng PC đều sử dụng compression S3TC (BC), và chuẩn này đã được chuẩn hóa hơn một thập kỷ, nhưng các thiết bị mobile sử dụng những format khác nhau cho texture compression, chẳng hạn như ETC1 và ETC2.

Menu export
-----------

Sau nhiều lần thử các workflow export khác nhau, workflow hiện tại đã chứng minh là hoạt động tốt nhất. Tại thời điểm viết tài liệu này, chưa phải tất cả platform đều được hỗ trợ, nhưng các platform được hỗ trợ vẫn tiếp tục tăng lên.

Để mở menu export, hãy nhấp vào nút :button:`Export`:

.. image:: img/export.webp

Menu export sẽ mở ra. Tuy nhiên, menu sẽ hoàn toàn trống. Đó là vì chúng ta cần thêm một export preset.

.. image:: img/export_dialog.webp

Để tạo một export preset, hãy nhấp vào nút **Add…** ở phía trên menu export. Thao tác này sẽ mở một danh sách thả xuống gồm các platform để chọn cho export preset.

.. image:: img/export_preset.webp

Các tùy chọn mặc định thường đã đủ để export, vì vậy thông thường không cần tinh chỉnh chúng. Tuy nhiên, nhiều platform yêu cầu cài đặt các tool bổ sung (SDK) để có thể export. Ngoài ra, Godot cần cài đặt export template để tạo package. Menu export sẽ thông báo khi thiếu thành phần nào đó và sẽ không cho phép người dùng export cho platform đó cho đến khi vấn đề được giải quyết:

.. image:: img/export_error.webp

Khi đó, người dùng được kỳ vọng sẽ quay lại tài liệu và làm theo hướng dẫn để thiết lập platform đó đúng cách.

Các nút ở cuối menu cho phép bạn export project theo một vài cách khác nhau:

- Export All: Export project dưới dạng một playable build (Godot executable và project data) cho tất cả preset đã định nghĩa. Tất cả preset phải có **Export Path** thì mới hoạt động. - Export Project: Export project dưới dạng một playable build (Godot executable và project data) cho preset được chọn. - Export PCK/ZIP: Export resource của project dưới dạng package PCK hoặc ZIP. Đây không phải là một playable build; thao tác này chỉ export project data mà không có Godot executable.

Export template
~~~~~~~~~~~~~~~

Phải cài đặt export template để export project. Để quản lý export template, hãy vào :menu:`Editor > Manage Export Templates...`.

.. image:: img/export_templates.webp

Thao tác này sẽ mở trình quản lý export template.

.. image:: img/export_template_manager.webp

Tại đây, bạn có thể xem tất cả export template đã và chưa được cài đặt. Có hai cách để cài đặt export template. Trước tiên, bạn có thể đánh dấu vào ô của platform và architecture muốn sử dụng, sau đó nhấp vào nút :button:`Install Selected Templates`.

.. note:: If you're unsure which architecture you need, check your platform's export
          để xem mô tả chi tiết.

Bên dưới các tùy chọn platform có một tùy chọn khác tên là :ui:`ICU Data`. Tùy chọn này cần thiết cho emoji và các ngôn ngữ sau:

- Tiếng Myanmar - Tiếng Trung - Tiếng Nhật - Tiếng Hàn - Tiếng Khmer Trung tâm - Tiếng Lào - Tiếng Thái

Nếu nhấp vào nút ở góc trên bên phải của cửa sổ, bạn có thể cài đặt template từ file TPZ (về cơ bản là một ZIP archive). Bạn có thể tải file TPZ chứa tất cả export template từ `download page of the website <https://www.godotengine.org/download>`_.

Việc sử dụng file TPZ cho tất cả platform không có lợi thế vốn có nào. Về chức năng, nó giống hệt nhau và sẽ chiếm nhiều dung lượng hơn so với việc chỉ chọn những gì bạn cần.

.. _doc_exporting_projects_export_mode:

Tùy chọn resource
~~~~~~~~~~~~~~~~~

Khi export, Godot lập danh sách tất cả file cần export rồi tạo package. Có 5 mode export khác nhau:

-  Export tất cả resource trong project - Export các scene được chọn (và dependency) - Export các resource được chọn (và dependency) - Export tất cả resource trong project ngoại trừ các resource được đánh dấu bên dưới - Export dưới dạng dedicated server

.. image:: img/export_resources.webp

**Export tất cả resource trong project** sẽ export mọi resource trong project. **Export các scene được chọn** và **Export các resource được chọn** cung cấp cho bạn danh sách các scene hoặc resource trong project, và bạn phải chọn từng scene hoặc resource muốn export.

.. image:: img/export_selected.webp

**Export tất cả resource trong project ngoại trừ các resource được đánh dấu bên dưới** thực hiện đúng như tên gọi: mọi thứ sẽ được export ngoại trừ những gì bạn chọn trong danh sách.

**Export dưới dạng dedicated server** sẽ xóa toàn bộ phần hiển thị khỏi project và thay thế chúng bằng placeholder. Điều này bao gồm Cubemap, CubemapArray, Material, Mesh, Texture2D, Texture2DArray, Texture3D. Bạn cũng có thể vào danh sách file và chỉ định các visual resource cụ thể mà bạn muốn giữ lại.

.. note::

    Các file và thư mục có tên bắt đầu bằng dấu chấm sẽ không bao giờ được đưa vào project đã export. Điều này nhằm ngăn các thư mục version control như ``.git`` được đưa vào file PCK đã export.

Bên dưới danh sách resource có hai bộ lọc có thể được thiết lập. Bộ lọc đầu tiên cho phép export các file không phải resource như ``.txt``, ``.json`` và ``.csv`` cùng với project. Bộ lọc thứ hai có thể được dùng để loại trừ mọi file thuộc một loại nhất định mà không cần bỏ chọn từng file. Ví dụ: các file ``.png``.

File cấu hình
-------------

Cấu hình export được lưu trong hai file, cả hai đều có thể tìm thấy trong thư mục project:

- ``export_presets.cfg``: File này chứa phần lớn cấu hình export và có thể commit an toàn vào version control. Thông thường, trong file này không có thông tin nào cần giữ bí mật. - ``.godot/export_credentials.cfg``: File này chứa các tùy chọn export được xem là confidential, chẳng hạn như password và encryption key. Nhìn chung, file này **không nên** được commit vào version control hoặc chia sẻ với người khác, trừ khi bạn biết chính xác mình đang làm gì.

Vì file credentials thường được giữ ngoài các hệ thống version control, một số tùy chọn export sẽ bị thiếu nếu bạn clone project sang một máy mới. Cách dễ nhất để xử lý việc này là tự sao chép file từ vị trí cũ sang vị trí mới.

Export từ command line
----------------------

Trong production, việc tự động hóa build rất hữu ích, và Godot hỗ trợ điều này bằng các command line parameter ``--export-release`` và ``--export-debug``. Export từ command line vẫn yêu cầu một export preset để định nghĩa các tham số export. Cách gọi lệnh cơ bản là:

.. code-block:: shell

    godot --export-release "Windows Desktop" some_name.exe

Lệnh này sẽ export vào ``some_name.exe``, với điều kiện có một preset tên là "Windows Desktop" và template có thể được tìm thấy. (Tên export preset phải được viết trong dấu ngoặc kép nếu chứa khoảng trắng hoặc ký tự đặc biệt.) Output path có thể là *relative to the project path* hoặc *absolute*; **nó không tuân theo thư mục nơi command được gọi**.

Phần mở rộng của output file phải khớp với phần mở rộng được sử dụng bởi quy trình Godot export:

- Windows: ``.exe`` - macOS: ``.app`` hoặc ``.zip`` (hoặc ``.dmg`` khi export *từ* macOS) - Linux: Bất kỳ phần mở rộng nào (kể cả không có). ``.x86_64`` thường được dùng cho binary x86 64-bit. - HTML5: ``.zip`` - Android: ``.apk`` - iOS: ``.zip``

Bạn cũng có thể cấu hình để chỉ export file PCK hoặc ZIP, cho phép sử dụng một main pack file đã export với nhiều Godot executable. Khi làm vậy, tên export preset vẫn phải được chỉ định trên command line:

.. code-block:: shell

    godot --export-pack "Windows Desktop" some_name.pck

Việc kết hợp flag ``--export-release`` với flag ``--path`` thường rất hữu ích, để bạn không cần ``cd`` vào thư mục project trước khi chạy command:

.. code-block:: shell

    godot --path /path/to/project --export-release "Windows Desktop" some_name.exe

.. seealso::

    Xem :ref:`doc_command_line_tutorial` để biết thêm thông tin về cách sử dụng Godot từ command line.

.. _doc_exporting_projects_pck_versus_zip:

Các format pack file PCK và ZIP
-------------------------------

Mỗi format đều có ưu điểm và nhược điểm. PCK là format mặc định và được khuyến nghị cho hầu hết trường hợp sử dụng, nhưng tùy theo nhu cầu, bạn có thể muốn sử dụng ZIP archive thay thế.

**Format PCK:**

- Định dạng không nén. Kích thước tệp lớn hơn nhưng đọc/ghi nhanh hơn. - Không thể đọc và ghi bằng các công cụ thường có trên hệ điều hành của người dùng, mặc dù có `third-party tools <https://github.com/hhyyrylainen/GodotPckTool>`__ để trích xuất và tạo các tệp PCK.

**Định dạng ZIP:**

- Định dạng nén. Kích thước tệp nhỏ hơn nhưng đọc/ghi chậm hơn. - Có thể đọc và ghi bằng các công cụ thường có trên hệ điều hành của người dùng. Điều này có thể giúp việc mod dễ dàng hơn (xem thêm :ref:`doc_exporting_pcks`).

.. warning::

    Do một `known bug <https://github.com/godotengine/godot/pull/42123>`__, khi sử dụng tệp ZIP làm tệp pack, binary đã xuất sẽ không tự động thử sử dụng tệp đó. Vì vậy, bạn phải tạo một *launcher script* mà người chơi có thể nhấp đúp hoặc chạy từ terminal để khởi chạy project:

    ::

        :: launch.bat (Windows)
        @echo off
        my_project.exe --main-pack my_project.zip

        # launch.sh (Linux)
        ./my_project.x86_64 --main-pack my_project.zip

    Lưu launcher script và đặt nó trong cùng thư mục với binary đã xuất. Trên Linux, hãy đảm bảo cấp quyền thực thi cho launcher script bằng lệnh ``chmod +x launch.sh``.
