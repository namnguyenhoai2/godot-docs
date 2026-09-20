.. _doc_ssl_certificates:

Chứng chỉ TLS/SSL
=================

Giới thiệu
----------

Thông thường, người dùng muốn sử dụng các kết nối :abbr:`TLS (Transport Layer Security)` (còn được gọi là các kết nối :abbr:`SSL (Secure Sockets Layer)`) để liên lạc nhằm tránh các cuộc tấn công "man in the middle". Godot có một wrapper kết nối
:ref:`StreamPeerTLS <class_StreamPeerTLS>`, which can take a regular connection
và bổ sung tính bảo mật cho nó. :ref:`HTTPClient <class_HTTPClient>` và
:ref:`HTTPRequest <class_HTTPRequest>` classes also support HTTPS using
chính wrapper này.

Godot sẽ cố gắng sử dụng bundle chứng chỉ TLS do hệ điều hành cung cấp, nhưng cũng bao gồm `TLS certificate bundle from Mozilla <https://github.com/godotengine/godot/blob/master/thirdparty/certs/ca-certificates.crt>`__ để dự phòng.

Ngoài ra, bạn có thể buộc sử dụng bundle chứng chỉ của riêng mình trong Project Settings:

.. figure:: img/tls_certificates_project_setting.webp
   :align: center
   :alt: Setting the TLS certificate bundle override project setting

   Setting the TLS certificate bundle override project setting

Khi được thiết lập, theo mặc định, tệp này sẽ *ghi đè* bundle do hệ điều hành cung cấp. Tệp này có thể chứa bất kỳ số lượng chứng chỉ công khai nào ở định dạng `PEM format <https://en.wikipedia.org/wiki/Privacy-enhanced_Electronic_Mail>`__.

Có hai cách để lấy chứng chỉ:

Lấy chứng chỉ từ một certificate authority
------------------------------------------

Cách chính để lấy chứng chỉ là sử dụng một certificate authority (CA), chẳng hạn như `Let's Encrypt <https://letsencrypt.org/>`__. Quy trình này rườm rà hơn so với chứng chỉ tự ký, nhưng "chính thức" hơn và đảm bảo danh tính của bạn được thể hiện rõ ràng. Chứng chỉ tạo ra cũng được các ứng dụng như trình duyệt web tin cậy, không giống như chứng chỉ tự ký, vốn yêu cầu cấu hình bổ sung ở phía client trước khi được xem là đáng tin cậy.

Các chứng chỉ này không yêu cầu client phải cấu hình để hoạt động, vì Godot đã tích hợp bundle chứng chỉ Mozilla trong editor và các project đã export.

Tạo chứng chỉ tự ký
-------------------

Trong hầu hết trường hợp sử dụng, bạn nên sử dụng certificate authority, vì quy trình này miễn phí với các certificate authority như Let's Encrypt. Tuy nhiên, nếu không thể sử dụng certificate authority, bạn có thể tạo chứng chỉ tự ký và cho client biết rằng chứng chỉ tự ký của bạn là đáng tin cậy.

Để tạo chứng chỉ tự ký, hãy tạo một cặp private key và public key, sau đó thêm public key (ở định dạng PEM) vào tệp CRT được chỉ định trong Project Settings.

.. warning::

    Private key **chỉ** được đưa lên server của bạn. Client không được phép truy cập vào key này; nếu không, tính bảo mật của chứng chỉ sẽ bị xâm phạm.

.. warning::

    Khi chỉ định chứng chỉ tự ký làm TLS bundle trong project settings, việc xác thực tên miền thông thường sẽ được thực thi thông qua chứng chỉ
    :abbr:`CN (common name)` and alternative names. See
    :ref:`TLSOptions <class_TLSOptions>` to customize domain name validation.

Để phục vụ mục đích phát triển, Godot có thể tạo chứng chỉ tự ký thông qua
:ref:`Crypto.generate_self_signed_certificate
<class_Crypto_method_generate_self_signed_certificate>`.

Ngoài ra, OpenSSL có tài liệu về `generating keys <https://raw.githubusercontent.com/openssl/openssl/master/doc/HOWTO/keys.txt>`__ và `certificates <https://raw.githubusercontent.com/openssl/openssl/master/doc/HOWTO/certificates.txt>`__.
