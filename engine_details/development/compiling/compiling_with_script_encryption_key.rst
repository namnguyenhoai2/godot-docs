.. _doc_compiling_with_script_encryption_key:

Biên dịch bằng khóa mã hóa PCK
==============================

.. highlight:: shell

Hộp thoại export cho phép bạn mã hóa tệp PCK bằng khóa AES 256 bit khi phát hành project. Điều này đảm bảo các scene, script và tài nguyên khác của bạn không được lưu dưới dạng văn bản thuần túy và không thể dễ dàng bị trích xuất bởi những kẻ phá hoại nghiệp dư.

Tất nhiên, khóa cần được lưu trong binary, nhưng nếu binary được biên dịch, tối ưu hóa và không có symbol thì sẽ cần khá nhiều công sức để tìm thấy khóa.

Để việc này hoạt động, bạn cần build export template từ source bằng chính khóa đó.

.. warning::

    Điều này **không** hoạt động nếu bạn sử dụng các export template chính thức được biên dịch sẵn. Việc tự biên dịch export template là **bắt buộc** để sử dụng mã hóa PCK.

Từng bước
---------

1. Tạo khóa AES 256 bit ở định dạng thập lục phân. Bạn có thể sử dụng biến thể aes-256-cbc từ `dịch vụ này <https://asecuritysite.com/encryption/keygen>`_.

   Ngoài ra, bạn có thể tự tạo khóa bằng các công cụ dòng lệnh `OpenSSL <https://www.openssl.org/>`__:

   ::

       openssl rand -hex 32 > godot.gdkey

   Đầu ra trong ``godot.gdkey`` phải tương tự như:

   ::

       # NOTE: Do not use the key below! Generate your own key instead.
       aeb1bc56aaf580cc31784e9c41551e9ed976ecba10d315db591e749f3f64890f

   Bạn có thể tạo khóa mà không chuyển hướng đầu ra vào tệp, nhưng cách đó giúp giảm thiểu nguy cơ làm lộ khóa.

2. Đặt khóa này làm biến môi trường trong console mà bạn sẽ dùng để biên dịch Godot, như sau:

   .. tabs::
    .. code-tab:: bash Linux/macOS

       export SCRIPT_AES256_ENCRYPTION_KEY="your_generated_key"

    .. code-tab:: bat Windows (cmd)

       set SCRIPT_AES256_ENCRYPTION_KEY=your_generated_key

    .. code-tab:: bat Windows (PowerShell)

       $env:SCRIPT_AES256_ENCRYPTION_KEY="your_generated_key"

   Lưu ý rằng các lệnh được đề xuất ở trên **không** duy trì các biến qua nhiều phiên terminal.

3. Biên dịch các export template của Godot và đặt chúng làm export template tùy chỉnh trong các tùy chọn export preset. Nếu biến môi trường được đặt chính xác, thông báo sau sẽ được in ở đầu quá trình biên dịch:

   ::

      *** IMPORTANT: Compiling Godot with custom `SCRIPT_AES256_ENCRYPTION_KEY` set as environment variable.
      *** Make sure to use templates compiled with this key when exporting a project with encryption.

4. Đặt khóa mã hóa trong tab **Encryption** của export preset:

   .. image:: img/encryption_key.png

   Nếu thực hiện export từ :ref:`dòng lệnh <doc_command_line_tutorial>`, trước khi export, hãy đặt biến môi trường ``GODOT_SCRIPT_ENCRYPTION_KEY`` thành cùng giá trị với giá trị được sử dụng để biên dịch export template (``SCRIPT_AES256_ENCRYPTION_KEY``).

5. Thêm bộ lọc cho các tệp/thư mục cần mã hóa. **Theo mặc định**, các bộ lọc include đều trống và **sẽ không có gì được mã hóa**.

6. Export project. Bây giờ project sẽ chạy với các tệp đã được mã hóa.

Khắc phục sự cố
---------------

Nếu bạn gặp lỗi như bên dưới, điều đó có nghĩa là khóa chưa được đưa vào bản build Godot đúng cách. Godot đang mã hóa tệp PCK trong khi export nhưng không thể đọc tệp này khi runtime.

::

   ERROR: open_and_parse: Condition "String::md5(md5.digest) != String::md5(md5d)" is true. Returning: ERR_FILE_CORRUPT
      At: core/io/file_access_encrypted.cpp:103

.. _`this service`: https://asecuritysite.com/encryption/keygen
