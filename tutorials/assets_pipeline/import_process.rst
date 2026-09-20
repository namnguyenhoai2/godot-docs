.. _doc_import_process:

Quy trình import
================

Import asset trong Godot
------------------------

Để import asset trong Godot, hãy đặt asset của bạn (tệp hình ảnh, scene, tệp âm thanh, font, v.v.) trực tiếp vào thư mục dự án. Có 2 cách để thực hiện việc này:

- **Với mọi loại tệp:** Sao chép tệp thủ công bằng trình quản lý tệp của hệ điều hành. - **Với các loại tệp có thể được Godot import:** Kéo và thả tệp từ trình quản lý tệp của hệ điều hành vào dock FileSystem của editor. Cách này chỉ hoạt động với các loại tệp *resource* (tức là những loại tệp mà Godot có thể import).

Godot sẽ tự động import các tệp này ở bên trong và giữ các resource đã import ở chế độ ẩn trong một thư mục ``res://.godot/imported/``.

Điều này có nghĩa là khi cố gắng truy cập các asset đã import thông qua code, bạn cần sử dụng :ref:`Resource Loader<class_ResourceLoader>`, vì nó sẽ tự động tính đến vị trí lưu các tệp bên trong. Nếu bạn cố gắng truy cập một asset đã import bằng class :ref:`FileAccess <class_FileAccess>`, thao tác này sẽ hoạt động trong editor, nhưng **sẽ bị lỗi trong project đã export**.

Tuy nhiên, :ref:`Resource Loader<class_ResourceLoader>` không thể truy cập các tệp chưa được import. Chỉ class :ref:`FileAccess <class_FileAccess>` mới có thể làm vậy.

Thay đổi tham số import
-----------------------

.. note::

    Các tham số import chỉ xuất hiện trong những loại resource Godot *không phải native*. Điều này có nghĩa là các định dạng tệp scene và resource riêng của Godot (``.tscn``, ``.scn``, ``.tres``, ``.res``) không có các tùy chọn import để bạn chọn trong dock Import.

Để thay đổi tham số import của một asset trong Godot, hãy chọn resource tương ứng trong dock FileSystem:

.. image:: img/import_process_example.webp

Sau khi điều chỉnh các tham số, hãy nhấp vào **Reimport**. Hãy cẩn thận: nếu bạn chọn một tệp khác trong dock FileSystem trước khi nhấp vào **Reimport**, các thay đổi sẽ bị hủy. Sau khi nhấp vào **Reimport**, các tham số đã chọn sẽ chỉ được sử dụng cho asset này và trong những lần reimport sau.

Bạn cũng có thể thay đổi tham số import của nhiều asset cùng lúc. Hãy chọn tất cả chúng trong dock FileSystem, các tham số được hiển thị sẽ được áp dụng cho tất cả khi reimport.

Reimport nhiều asset
--------------------

Trong quá trình làm việc với một dự án, bạn có thể thấy cần thay đổi cùng một tham số cho nhiều asset, chẳng hạn như bật mipmap, nhưng chỉ muốn thay đổi những tham số cụ thể đó. Để thực hiện việc này, hãy chọn mọi asset mà bạn muốn reimport trong hệ thống tệp. Trong tab Import lúc này sẽ có một hộp kiểm ở bên trái mỗi tham số import.

.. image:: img/reimport_multiple.webp

Hãy chọn hộp kiểm của các tham số mà bạn muốn thay đổi trên các asset đã import, sau đó thay đổi các tham số như bình thường. Cuối cùng, hãy nhấp vào nút reimport và mọi asset đã chọn sẽ được reimport với chỉ những tham số đó được thay đổi.

Reimport tự động
----------------

Khi checksum MD5 của asset nguồn thay đổi, Godot sẽ tự động reimport asset đó và áp dụng preset đã cấu hình cho asset cụ thể đó.

Bỏ qua các thư mục cụ thể
-------------------------

Đôi khi, bạn có những tệp không muốn Godot import, chẳng hạn như hình ảnh được dùng trong press kit hoặc tài liệu quảng bá của trò chơi. Bạn có thể đặt các tệp đó vào một thư mục mà bạn chỉ định để Godot bỏ qua. Việc bỏ qua một thư mục đảm bảo thư mục đó không được Godot import; đồng thời, thư mục cũng bị ẩn khỏi dock FileSystem. Việc bỏ qua một thư mục cũng khiến nội dung của thư mục đó không được export cùng project, nhờ đó giảm kích thước PCK đã export.

Xem :ref:`doc_project_organization_ignoring_specific_folders` trong tutorial tổ chức project để biết thêm chi tiết.

Các tệp được tạo
----------------

Thao tác import sẽ thêm một tệp ``<asset>.import`` bổ sung bên cạnh tệp nguồn, chứa cấu hình import.

**Hãy đảm bảo commit các tệp này vào hệ thống version control của bạn**, vì các tệp này chứa metadata quan trọng.

::

    ls
    example.png
    example.png.import
    project.godot

Ngoài ra, các asset bổ sung sẽ nằm trong thư mục ``res://.godot/imported/`` bị ẩn:

::

    ls .godot/imported
    example.png-218a8f2b3041327d8a5756f3a245f83b.ctex
    example.png-218a8f2b3041327d8a5756f3a245f83b.md5

Nếu bất kỳ tệp nào trong thư mục này bị xóa (hoặc toàn bộ thư mục bị xóa), asset hoặc các asset đó sẽ tự động được reimport. Vì vậy, không nên commit thư mục ``.godot/`` vào hệ thống version control. Mặc dù việc commit thư mục này có thể rút ngắn thời gian reimport khi checkout trên một máy tính khác, nó lại yêu cầu nhiều không gian lưu trữ và băng thông hơn đáng kể.

Metadata version control mặc định có thể được tạo khi tạo project sẽ tự động bỏ qua thư mục ``.godot/``.

Thay đổi loại resource import
-----------------------------

Một số asset nguồn có thể được import thành các loại resource khác nhau. Để thực hiện việc này, hãy chọn loại resource mong muốn tương ứng, sau đó nhấp vào **Reimport**:

.. image:: img/import_process_changing_import_type.webp

Chọn ``Keep File (exported as is)`` làm loại resource để bỏ qua việc import tệp; các tệp thuộc loại resource này sẽ được giữ nguyên trong quá trình export project.

Chọn ``Skip File (not exported)`` làm loại resource để bỏ qua việc import tệp và bỏ qua tệp đó trong quá trình export project.

Thay đổi tham số import mặc định
--------------------------------

Các loại project khác nhau có thể yêu cầu các giá trị mặc định khác nhau. Bạn có thể thay đổi các tùy chọn import thành một tập hợp tùy chọn được định trước bằng cách sử dụng menu **Preset...**. Ngoài việc một số loại resource cung cấp preset, bạn cũng có thể lưu và xóa các thiết lập mặc định:

.. image:: img/import_process_change_preset.webp

Có thể thay đổi các tham số import mặc định cho một loại resource nhất định trên toàn project bằng tab **Import Defaults** trong hộp thoại Project Settings:

.. image:: img/import_process_import_defaults.webp

Đọc thêm
--------

Quy trình này cần một chút thời gian để làm quen, nhưng nó thúc đẩy một cách xử lý resource đúng đắn hơn.

Có nhiều loại asset có thể được import. Hãy tiếp tục đọc để hiểu cách làm việc với tất cả chúng:

- :ref:`doc_importing_images` - :ref:`doc_importing_audio_samples` - :ref:`doc_importing_3d_scenes` - :ref:`doc_importing_translations`
