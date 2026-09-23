.. _doc_exporting_for_windows:

Xuất cho Windows
================

.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang Windows. Nếu bạn muốn biên dịch các tệp nhị phân của editor hoặc export template từ mã nguồn thay vào đó, hãy đọc :ref:`doc_compiling_for_windows`.

Cách đơn giản nhất để phân phối game cho PC là sao chép tệp thực thi (``godot.exe``), nén thư mục rồi gửi cho người khác. Tuy nhiên, cách này thường không được mong muốn.

Godot cung cấp một phương pháp thanh lịch hơn để phân phối cho PC khi sử dụng hệ thống export. Khi xuất cho Windows, exporter lấy tất cả tệp dự án và tạo một tệp ``data.pck``. Tệp này được đóng gói cùng một tệp nhị phân được tối ưu hóa đặc biệt, có kích thước nhỏ hơn, chạy nhanh hơn và không chứa editor cũng như debugger.

Kiến trúc
---------

Có 3 kiến trúc bộ xử lý khác nhau mà các dự án Godot đã xuất có thể chạy trên Windows:

- x86_64
- x86_32
- arm64

Mặc định là x86_64, đây là kiến trúc phổ biến nhất của các bộ xử lý PC hiện nay. Tất cả bộ xử lý Intel và AMD hiện đại tính đến thời điểm viết tài liệu này đều là x86_64.

x86_32 sẽ tạo một tệp thực thi 32-bit có thể chạy trên các phiên bản Windows chỉ hỗ trợ 32-bit cũng như các phiên bản hiện đại 64-bit. Bạn **không** nên sử dụng tùy chọn này trừ khi đang cố gắng chạy dự án trên một phiên bản Windows 32-bit cũ. Cũng cần lưu ý rằng không còn phiên bản Windows 32-bit nào nhận được hỗ trợ từ Microsoft.

Bộ xử lý arm64 hiện đại nhưng ít phổ biến hơn x86_64, và chạy Windows trên ARM. Snapdragon X Elite là một ví dụ về bộ xử lý Windows ARM hiện đại. Sử dụng tùy chọn export này sẽ cho phép dự án chạy nguyên bản trên các bộ xử lý arm mà không cần trình giả lập Prism của Microsoft. Các tệp thực thi được tạo bằng tùy chọn này **không** chạy trên Windows thông thường với bộ xử lý x86_64. Nếu bạn tải dự án lên một nền tảng cho phép nhiều tệp thực thi, chẳng hạn như itch.io, và tin chắc rằng bộ xử lý Snapdragon X Elite đủ mạnh để chạy dự án, chúng tôi khuyến nghị cung cấp một phiên bản ARM. Việc giả lập bằng Prism còn lâu mới hoàn hảo, và Godot không yêu cầu bạn xây dựng hoặc thiết kế game theo cách đặc biệt nào để chạy trên ARM.

Thay đổi biểu tượng tệp thực thi
--------------------------------

Godot sẽ tự động sử dụng hình ảnh được đặt làm biểu tượng của dự án trong phần cài đặt dự án và chuyển đổi hình ảnh đó thành tệp ICO cho dự án đã xuất. Nếu muốn tự tạo tệp ICO để kiểm soát tốt hơn diện mạo của biểu tượng ở các độ phân giải khác nhau, hãy xem trang :ref:`doc_changing_application_icon_for_windows`.

Nhúng PCK
---------

Tính năng nhúng PCK chỉ được hỗ trợ trên các tệp thực thi có kích thước tối đa khoảng 3,89 GB. Chỉ số này bao gồm cả kích thước tệp thực thi và PCK được nhúng, vì vậy trên thực tế, tệp PCK có thể chỉ có kích thước tối đa khoảng 3,75 GB. Con số này cũng có thể thay đổi tùy thuộc vào các tùy chọn build khi sử dụng export template tùy chỉnh.

.. _doc_exporting_for_windows_code_signing:

Ký mã
-----

Godot có khả năng tự động ký mã khi export. Để thực hiện việc này, bạn phải cài đặt ``Windows SDK`` (trên Windows) hoặc `osslsigncode <https://github.com/mtrojnar/osslsigncode>`__ (trên bất kỳ hệ điều hành nào khác). Bạn cũng sẽ cần chứng chỉ ký gói, thông tin về cách tạo chứng chỉ có thể tìm thấy `tại đây <https://learn.microsoft.com/en-us/windows/msix/package/create-certificate-package-signing>`__.

Thiết lập
~~~~~~~~~

Cần thay đổi cài đặt ở hai nơi. Trước tiên, trong cài đặt editor, bên dưới **Export > Windows**. Nhấp vào thư mục bên cạnh cài đặt ``Sign Tool``, nếu đang sử dụng Windows, hãy điều hướng đến và chọn ``SignTool.exe``, còn nếu đang ở một hệ điều hành khác, hãy chọn ``osslsigncode``.

.. image:: img/windows_editor_settings.webp

Vị trí thứ hai là export preset của Windows, có thể tìm thấy tại **Project > Export...**. Hãy thêm một preset cho máy tính Windows nếu bạn chưa thực hiện việc này. Trong phần tùy chọn có một danh mục ký mã.

.. image:: img/windows_export_codesign.webp

``Enabled`` phải được đặt thành ``true``, và ``Identity`` phải được đặt thành chứng chỉ ký. Các cài đặt khác có thể được điều chỉnh tùy nhu cầu. Sau khi hoàn tất, Godot sẽ ký dự án khi export.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè các giá trị bạn đã đặt trong menu export.

.. list-table:: Các biến môi trường export cho Windows
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Mã hóa / Khóa mã hóa
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``
   * - Tùy chọn / Codesign / Loại danh tính
     - ``GODOT_WINDOWS_CODESIGN_IDENTITY_TYPE``
   * - Tùy chọn / Codesign / Danh tính
     - ``GODOT_WINDOWS_CODESIGN_IDENTITY``
   * - Tùy chọn / Codesign / Mật khẩu
     - ``GODOT_WINDOWS_CODESIGN_PASSWORD``

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có trong
tài liệu tham chiếu lớp :ref:`class_EditorExportPlatformWindows`.
