.. _doc_ssl_certificates:

Chứng chỉ TLS/SSL
=================

Giới thiệu
----------

Thường nên sử dụng các kết nối :abbr:`TLS (Transport Layer Security)` (còn được gọi là kết nối :abbr:`SSL (Secure Sockets Layer)`) cho hoạt động liên lạc để tránh các cuộc tấn công "man in the middle". Godot có một trình bao bọc kết nối,
:ref:`StreamPeerTLS <class_StreamPeerTLS>`, có thể lấy một kết nối thông thường và bổ sung bảo mật cho kết nối đó. Các :ref:`HTTPClient <class_HTTPClient>` và
:ref:`HTTPRequest <class_HTTPRequest>` lớp cũng hỗ trợ HTTPS bằng cùng trình bao bọc này.

Godot sẽ thử sử dụng gói chứng chỉ TLS do hệ điều hành cung cấp, nhưng cũng bao gồm `TLS certificate bundle from Mozilla <https://github.com/godotengine/godot/blob/master/thirdparty/certs/ca-certificates.crt>`__ để dự phòng.

Ngoài ra, bạn có thể buộc sử dụng gói chứng chỉ riêng trong Project Settings:

.. figure:: img/tls_certificates_project_setting.webp
   :align: center
   :alt: Thiết lập project setting ghi đè gói chứng chỉ TLS

   Thiết lập project setting ghi đè gói chứng chỉ TLS

Khi được thiết lập, tệp này *ghi đè* gói do hệ điều hành cung cấp theo mặc định. Tệp này phải chứa bất kỳ số lượng chứng chỉ công khai nào ở `định dạng PEM <https://en.wikipedia.org/wiki/Privacy-enhanced_Electronic_Mail>`__.

Có hai cách để lấy chứng chỉ:

Lấy chứng chỉ từ certificate authority
--------------------------------------

Cách chính để lấy chứng chỉ là sử dụng một certificate authority (CA) như `Let's Encrypt <https://letsencrypt.org/>`__. Đây là quy trình rườm rà hơn so với chứng chỉ tự ký, nhưng "chính thức" hơn và đảm bảo danh tính của bạn được thể hiện rõ ràng. Chứng chỉ nhận được cũng được các ứng dụng như trình duyệt web tin cậy, không giống chứng chỉ tự ký, vốn cần cấu hình bổ sung ở phía client trước khi được xem là đáng tin cậy.

Các chứng chỉ này không yêu cầu cấu hình nào trên client để hoạt động, vì Godot đã tích hợp gói chứng chỉ Mozilla trong editor và các project đã export.

Tạo chứng chỉ tự ký
-------------------

Đối với hầu hết trường hợp sử dụng, bạn nên sử dụng certificate authority vì quy trình này miễn phí với các certificate authority như Let's Encrypt. Tuy nhiên, nếu không thể sử dụng certificate authority, bạn có thể tạo chứng chỉ tự ký và yêu cầu client coi chứng chỉ tự ký của bạn là đáng tin cậy.

Để tạo chứng chỉ tự ký, hãy tạo một cặp khóa riêng tư và khóa công khai, rồi thêm khóa công khai (ở định dạng PEM) vào tệp CRT được chỉ định trong Project Settings.

.. warning::

    Khóa riêng tư **chỉ** được đưa lên server của bạn. Client không được phép truy cập khóa này; nếu không, tính bảo mật của chứng chỉ sẽ bị xâm phạm.

.. warning::

    Khi chỉ định chứng chỉ tự ký làm gói TLS trong project settings, việc xác thực tên miền thông thường được thực thi thông qua
    :abbr:`CN (common name)` và các tên thay thế. Xem
    :ref:`TLSOptions <class_TLSOptions>` để tùy chỉnh việc xác thực tên miền.

Với mục đích phát triển, Godot có thể tạo chứng chỉ tự ký thông qua
:ref:`Crypto.generate_self_signed_certificate
<class_Crypto_method_generate_self_signed_certificate>`.

Ngoài ra, OpenSSL có một số tài liệu về `việc tạo khóa <https://raw.githubusercontent.com/openssl/openssl/master/doc/HOWTO/keys.txt>`__ và `chứng chỉ <https://raw.githubusercontent.com/openssl/openssl/master/doc/HOWTO/certificates.txt>`__.
