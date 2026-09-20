.. _doc_exporting_for_windows:

Xuất bản cho Windows
====================

.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang Windows. Nếu bạn muốn biên dịch editor hoặc các binary export template từ source thay vào đó, hãy đọc :ref:`doc_compiling_for_windows`.

Cách đơn giản nhất để phân phối một game cho PC là sao chép tệp thực thi (``godot.exe``), nén thư mục rồi gửi cho người khác. Tuy nhiên, cách này thường không được mong muốn.

Godot cung cấp một phương pháp thanh lịch hơn để phân phối cho PC khi sử dụng hệ thống export. Khi export cho Windows, exporter lấy tất cả các tệp dự án và tạo một tệp ``data.pck``. Tệp này được đóng gói cùng với một binary được tối ưu hóa đặc biệt, có kích thước nhỏ hơn, nhanh hơn và không chứa editor cũng như debugger.

Kiến trúc
---------

Có 3 kiến trúc bộ xử lý khác nhau mà các dự án Godot đã export có thể chạy trên Windows:

- x86_64 - x86_32 - arm64

Mặc định là x86_64, đây là kiến trúc phổ biến nhất của các bộ xử lý PC hiện nay. Tất cả bộ xử lý Intel và AMD hiện đại tại thời điểm viết nội dung này đều là x86_64.

x86_32 sẽ cung cấp cho bạn một tệp thực thi 32bit có thể chạy trên các phiên bản Windows chỉ hỗ trợ 32bit cũng như các phiên bản hiện đại 64bit. **Không** nên sử dụng tùy chọn này trừ khi bạn muốn dự án của mình chạy trên một phiên bản Windows 32bit cũ. Cũng cần lưu ý rằng hiện không còn phiên bản Windows 32bit nào nhận được hỗ trợ từ Microsoft.

Bộ xử lý arm64 hiện đại nhưng ít phổ biến hơn x86_64 và chạy Windows trên ARM. Snapdragon X Elite là một ví dụ về bộ xử lý Windows ARM hiện đại. Sử dụng tùy chọn export này sẽ cho phép dự án của bạn chạy nguyên bản trên các bộ xử lý arm mà không cần trình giả lập Prism của Microsoft. Các tệp thực thi được tạo bằng tùy chọn này sẽ **không** chạy trên Windows thông thường với bộ xử lý x86_64. Nếu bạn tải dự án lên một nền tảng cho phép nhiều tệp thực thi, chẳng hạn như itch.io, và tin chắc rằng bộ xử lý Snapdragon X Elite đủ mạnh để chạy dự án, chúng tôi khuyến nghị cung cấp một phiên bản ARM. Việc giả lập bằng Prism còn lâu mới hoàn hảo, và Godot không yêu cầu bạn xây dựng hoặc thiết kế game theo bất kỳ cách đặc biệt nào để chạy trên ARM.

Thay đổi biểu tượng tệp thực thi
--------------------------------

Godot sẽ tự động sử dụng hình ảnh được đặt làm biểu tượng của dự án trong phần cài đặt dự án và chuyển đổi hình ảnh đó thành tệp ICO cho dự án đã export. Nếu bạn muốn tự tạo tệp ICO để kiểm soát tốt hơn cách biểu tượng hiển thị ở các độ phân giải khác nhau, hãy xem trang :ref:`doc_changing_application_icon_for_windows`.

Nhúng PCK
---------

Tính năng nhúng PCK chỉ được hỗ trợ trên các tệp thực thi có kích thước tối đa khoảng 3.89 GB. Chỉ số này bao gồm cả kích thước của tệp thực thi và PCK được nhúng, vì vậy trên thực tế, tệp PCK có thể chỉ có kích thước tối đa khoảng 3.75 GB. Kích thước này cũng có thể thay đổi tùy theo các tùy chọn build khi sử dụng export template tùy chỉnh.

.. _doc_exporting_for_windows_code_signing:

Ký code
-------

Godot có khả năng tự động ký code khi export. Để thực hiện việc này, bạn phải cài đặt ``Windows SDK`` (trên Windows) hoặc `osslsigncode <https://github.com/mtrojnar/osslsigncode>`__ (trên bất kỳ hệ điều hành nào khác). Bạn cũng sẽ cần một chứng chỉ ký package; thông tin về cách tạo chứng chỉ có thể tìm thấy `here <https://learn.microsoft.com/en-us/windows/msix/package/create-certificate-package-signing>`__.

Thiết lập
~~~~~~~~~

Cần thay đổi cài đặt ở hai nơi. Trước tiên, trong phần cài đặt editor, tại **Export > Windows**. Nhấp vào thư mục bên cạnh cài đặt ``Sign Tool``; nếu bạn đang sử dụng Windows, hãy điều hướng đến và chọn ``SignTool.exe``; nếu bạn đang sử dụng hệ điều hành khác, hãy chọn ``osslsigncode``.

.. image:: img/windows_editor_settings.webp

Vị trí thứ hai là export preset cho Windows, có thể tìm thấy tại **Project > Export...**. Hãy thêm một preset desktop cho Windows nếu bạn chưa thêm. Trong phần tùy chọn có một danh mục ký code.

.. image:: img/windows_export_codesign.webp

``Enabled`` phải được đặt thành ``true``, và ``Identity`` phải được đặt thành chứng chỉ ký. Có thể điều chỉnh các cài đặt khác tùy nhu cầu. Sau khi hoàn tất, Godot sẽ ký dự án của bạn khi export.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập các tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè các giá trị bạn đã đặt trong menu export.

.. list-table:: Windows export environment variables
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``
   * - Options / Codesign / Identity Type
     - ``GODOT_WINDOWS_CODESIGN_IDENTITY_TYPE``
   * - Options / Codesign / Identity
     - ``GODOT_WINDOWS_CODESIGN_IDENTITY``
   * - Options / Codesign / Password
     - ``GODOT_WINDOWS_CODESIGN_PASSWORD``

Các tùy chọn export
-------------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export khả dụng trong
:ref:`class_EditorExportPlatformWindows` class reference.
