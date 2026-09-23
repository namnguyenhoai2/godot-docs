.. _doc_exporting_for_linux:

Xuất cho Linux
==============

.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang Linux. Nếu bạn muốn biên dịch editor hoặc các binary của export template từ mã nguồn, hãy đọc :ref:`doc_compiling_for_linuxbsd`.

Cách đơn giản nhất để phân phối một game cho PC là sao chép tệp thực thi (``godot``), nén thư mục rồi gửi cho người khác. Tuy nhiên, cách này thường không được mong muốn.

Godot cung cấp một cách tiếp cận tinh tế hơn để phân phối cho PC khi sử dụng hệ thống export. Khi export cho Linux, exporter sẽ lấy tất cả tệp dự án và tạo một tệp ``data.pck``. Tệp này được đóng gói cùng một binary được tối ưu hóa đặc biệt, có kích thước nhỏ hơn, nhanh hơn và không chứa editor cùng debugger.

Kiến trúc
---------

Có 7 kiến trúc bộ xử lý khác nhau mà các dự án Godot đã export có thể chạy trên Linux:

- x86_64
- x86_32
- arm64
- arm32
- rv64
- ppc64
- loongarch64

Mặc định là x86_64, đây là kiến trúc phổ biến nhất của các bộ xử lý PC hiện nay. Tại thời điểm viết tài liệu này, tất cả bộ xử lý Intel và AMD hiện đại đều là x86_64.

x86_32 sẽ cung cấp cho bạn một tệp thực thi 32 bit, có thể chạy trên các bản phân phối Linux chỉ hỗ trợ 32 bit cũng như một số bản phân phối hiện đại hỗ trợ 64 bit. KHÔNG khuyến nghị sử dụng tùy chọn này trừ khi bạn đang cố chạy dự án trên một bản phân phối và bộ xử lý 32 bit cũ. Cũng cần lưu ý rằng một số bản phân phối lớn, chẳng hạn như Fedora, đã thảo luận về việc loại bỏ các thư viện 32 bit, điều này sẽ ngăn các tệp thực thi được tạo theo cách này chạy trên các phiên bản tương lai của bản phân phối đó.

Các tệp thực thi arm64 có thể chạy trên bộ xử lý ARM 64 bit. Nếu bạn quen thuộc với Raspberry Pi, các thiết bị này đã sử dụng bộ xử lý ARM 64 bit kể từ Pi 3 (các phiên bản cũ hơn sử dụng bộ xử lý ARM 32 bit). Nếu bạn tải lên một nền tảng hỗ trợ nhiều tệp thực thi, chẳng hạn như itch.io, và tin rằng game của mình có thể chạy trên một máy tính ARM phổ biến như Pi 5, chúng tôi khuyến nghị export phiên bản này và cung cấp nó như một tùy chọn.

Các tệp thực thi arm32 dành cho những bộ xử lý arm 32 bit cũ hơn, chẳng hạn như loại được Raspberry Pi 1 và 2 sử dụng. Vì hiện nay chúng hoàn toàn không phổ biến, chúng tôi không khuyến nghị export cho kiến trúc này trừ khi bạn có một máy tính sử dụng một trong các bộ xử lý đó, biết rằng mình có thể và muốn chạy game trên máy tính ấy.

rv64 dành cho bộ xử lý RISC-V, ppc64 dành cho bộ xử lý PowerPC 64 bit, còn loongarch64 dành cho bộ xử lý LoongArch 64 bit. Tất cả các kiến trúc này đều ít phổ biến hơn đáng kể khi chạy trò chơi điện tử. Chúng tôi chỉ khuyến nghị export cho các kiến trúc này nếu bạn có lý do cụ thể, chẳng hạn như là một người đam mê sở hữu phần cứng tương ứng. Godot không cung cấp các export template chính thức; bạn sẽ phải tự tạo chúng. Bạn có thể tìm thấy hướng dẫn biên dịch engine cho RISC-V và tạo export template trên trang :ref:`doc_compiling_for_linuxbsd`.


Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè những giá trị bạn đã đặt trong menu export.

.. list-table:: Các biến môi trường export cho Linux
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có trong
tài liệu tham chiếu lớp :ref:`class_EditorExportPlatformLinuxBSD`.
