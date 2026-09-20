.. _doc_exporting_for_linux:

Xuất bản cho Linux
==================

.. seealso::

    Trang này mô tả cách xuất một dự án Godot cho Linux. Nếu bạn muốn biên dịch các binary của editor hoặc export template từ source thay vào đó, hãy đọc :ref:`doc_compiling_for_linuxbsd`.

Cách đơn giản nhất để phân phối một game cho PC là sao chép executable (``godot``), nén thư mục rồi gửi cho người khác. Tuy nhiên, cách này thường không được mong muốn.

Godot cung cấp một cách tiếp cận tinh tế hơn để phân phối game cho PC khi sử dụng hệ thống export. Khi xuất bản cho Linux, exporter lấy tất cả các tệp của dự án và tạo một tệp ``data.pck``. Tệp này được đóng gói cùng với một binary được tối ưu hóa đặc biệt, có kích thước nhỏ hơn, tốc độ nhanh hơn và không chứa editor cũng như debugger.

Kiến trúc
---------

Có 7 kiến trúc bộ xử lý khác nhau mà các dự án Godot đã export có thể chạy trên Linux:

- x86_64 - x86_32 - arm64 - arm32 - rv64 - ppc64 - loongarch64

Mặc định là x86_64; đây là kiến trúc phổ biến nhất của các bộ xử lý PC hiện nay. Tại thời điểm viết tài liệu này, tất cả bộ xử lý Intel và AMD hiện đại đều là x86_64.

x86_32 sẽ cung cấp cho bạn một executable 32bit có thể chạy trên các bản phân phối Linux chỉ hỗ trợ 32bit, cũng như một số bản phân phối hiện đại là 64bit. KHÔNG khuyến nghị sử dụng tùy chọn này trừ khi bạn đang cố gắng để dự án chạy trên một bản phân phối và bộ xử lý 32bit cũ. Cũng cần lưu ý rằng một số bản phân phối nổi bật, chẳng hạn như Fedora, đã thảo luận về việc loại bỏ các thư viện 32bit của họ, điều này sẽ khiến các executable được tạo theo cách này không thể chạy trên các phiên bản tương lai của bản phân phối đó.

Các executable arm64 có thể chạy trên bộ xử lý ARM 64bit. Nếu bạn quen thuộc với Raspberry Pi, các thiết bị này đã sử dụng bộ xử lý ARM 64bit kể từ Pi 3 (các phiên bản cũ hơn sử dụng bộ xử lý ARM 32bit). Nếu bạn tải lên một nền tảng hỗ trợ nhiều executable, chẳng hạn như itch.io, và tin rằng game của mình có thể chạy trên một máy tính ARM phổ biến, chẳng hạn như Pi 5, thì chúng tôi khuyến nghị xuất bản phiên bản này và cung cấp nó như một tùy chọn.

Các executable arm32 dành cho những bộ xử lý arm 32bit cũ hơn, chẳng hạn như loại được Raspberry Pi 1 và 2 sử dụng. Vì hiện nay chúng hoàn toàn không phổ biến, chúng tôi không khuyến nghị xuất bản cho kiến trúc này trừ khi bạn có một máy tính sử dụng một trong các bộ xử lý đó, biết chắc rằng game có thể chạy trên máy tính ấy và muốn game của mình chạy trên đó.

rv64 dành cho các bộ xử lý RISC-V, ppc64 dành cho các bộ xử lý PowerPC 64bit, còn loongarch64 dành cho các bộ xử lý LoongArch 64bit. Tất cả các kiến trúc này đều ít phổ biến hơn đáng kể khi chạy videogame. Chúng tôi chỉ khuyến nghị xuất bản cho các kiến trúc này nếu bạn có lý do phù hợp, chẳng hạn như là một người đam mê sở hữu phần cứng tương ứng. Godot không cung cấp các export template chính thức; bạn sẽ phải tự tạo chúng. Hướng dẫn biên dịch engine cho RISC-V và tạo export template có trên trang :ref:`doc_compiling_for_linuxbsd`.


Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập các tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè các giá trị bạn đã thiết lập trong menu export.

.. list-table:: Linux export environment variables
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Mã hóa / Khóa mã hóa
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``

Các tùy chọn export
-------------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có sẵn trong
:ref:`class_EditorExportPlatformLinuxBSD` class reference.
