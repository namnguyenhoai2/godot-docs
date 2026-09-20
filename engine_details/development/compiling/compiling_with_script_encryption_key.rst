.. _doc_compiling_with_script_encryption_key:

Biên dịch với khóa mã hóa PCK
=============================

.. highlight:: shell

Hộp thoại export cho phép bạn mã hóa tệp PCK bằng khóa AES 256-bit khi phát hành dự án. Điều này đảm bảo các cảnh, tập lệnh và tài nguyên khác của bạn không được lưu dưới dạng văn bản thuần túy và không dễ dàng bị trích xuất bởi một script kiddie nào đó.

Tất nhiên, khóa này cần được lưu trong tệp nhị phân, nhưng nếu tệp đã được biên dịch, tối ưu hóa và không có symbol thì sẽ cần một chút công sức để tìm thấy khóa.

Để tính năng này hoạt động, bạn cần build các export template từ mã nguồn với cùng khóa đó.

.. warning::

    Điều này **sẽ không** hoạt động nếu bạn sử dụng các export template chính thức, được biên dịch sẵn. Bạn **bắt buộc** phải tự biên dịch các export template của mình để sử dụng tính năng mã hóa PCK.

Từng bước
---------

1. Tạo khóa AES 256-bit ở định dạng hệ thập lục phân. Bạn có thể sử dụng biến thể aes-256-cbc từ `dịch vụ này <https://asecuritysite.com/encryption/keygen>`_.

   Ngoài ra, bạn có thể tự tạo khóa bằng các công cụ dòng lệnh `OpenSSL <https://www.openssl.org/>`__:

   ::

       openssl rand -hex 32 > godot.gdkey

   Đầu ra trong ``godot.gdkey`` sẽ tương tự như sau:

   ::

       # NOTE: Do not use the key below! Generate your own key instead.
       aeb1bc56aaf580cc31784e9c41551e9ed976ecba10d315db591e749f3f64890f

   Bạn có thể tạo khóa mà không chuyển hướng đầu ra vào một tệp, nhưng làm như vậy có thể giảm thiểu nguy cơ để lộ khóa.

2. Đặt khóa này làm biến môi trường trong console mà bạn sẽ sử dụng để biên dịch Godot, như sau:

   .. tabs::
    .. code-tab:: bash Linux/macOS

       export SCRIPT_AES256_ENCRYPTION_KEY="your_generated_key"

    .. code-tab:: bat Windows (cmd)

       set SCRIPT_AES256_ENCRYPTION_KEY=your_generated_key

    .. code-tab:: bat Windows (PowerShell)

       $env:SCRIPT_AES256_ENCRYPTION_KEY="your_generated_key"

   Lưu ý rằng các lệnh được đề xuất ở trên **không** lưu các biến này qua các phiên terminal.

3. Biên dịch các export template của Godot và đặt chúng làm export template tùy chỉnh trong các tùy chọn export preset. Nếu biến môi trường được đặt chính xác, thông báo sau sẽ được in ở đầu quá trình biên dịch:

   ::

      *** IMPORTANT: Compiling Godot with custom `SCRIPT_AES256_ENCRYPTION_KEY` set as environment variable.
      *** Make sure to use templates compiled with this key when exporting a project with encryption.

4. Đặt khóa mã hóa trong tab **Encryption** của export preset:

   .. image:: img/encryption_key.png

   Nếu thực hiện export từ :ref:`command line <doc_command_line_tutorial>`, trước khi export, hãy đặt biến môi trường ``GODOT_SCRIPT_ENCRYPTION_KEY`` thành cùng giá trị với giá trị được sử dụng để biên dịch các export template (``SCRIPT_AES256_ENCRYPTION_KEY``).

5. Thêm bộ lọc cho các tệp/thư mục cần mã hóa. **Theo mặc định**, các bộ lọc bao gồm đều trống và **sẽ không có gì được mã hóa**.

6. Export dự án. Bây giờ dự án sẽ chạy với các tệp đã được mã hóa.

Khắc phục sự cố
---------------

Nếu bạn gặp lỗi như bên dưới, điều đó có nghĩa là khóa chưa được đưa đúng cách vào bản build Godot của bạn. Godot đang mã hóa tệp PCK trong quá trình export nhưng không thể đọc tệp này lúc chạy.

::

   ERROR: open_and_parse: Condition "String::md5(md5.digest) != String::md5(md5d)" is true. Returning: ERR_FILE_CORRUPT
      At: core/io/file_access_encrypted.cpp:103
