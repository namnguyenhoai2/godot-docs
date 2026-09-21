:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Crypto.xml.

.. _class_Crypto:

Crypto
======

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp quyền truy cập vào các chức năng mật mã nâng cao.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp Crypto cung cấp quyền truy cập vào các chức năng mật mã nâng cao.

Currently, this includes asymmetric key encryption/decryption, signing/verification, and generating cryptographically secure random bytes, RSA keys, HMAC digests, and self-signed :ref:`X509Certificate<class_X509Certificate>`\ s.


.. tabs::

 .. code-tab:: gdscript

    var crypto = Crypto.new()

    # Tạo khóa RSA mới.
    var key = crypto.generate_rsa(4096)

    # Tạo chứng chỉ tự ký mới với khóa đã cho.
    var cert = crypto.generate_self_signed_certificate(key, "CN=mydomain.com,O=My Game Company,C=IT")

    # Lưu khóa và chứng chỉ vào thư mục người dùng.
    key.save("user://generated.key")
    cert.save("user://generated.crt")

    # Mã hóa
    var data = "Some data"
    var encrypted = crypto.encrypt(key, data.to_utf8_buffer())

    # Giải mã
    var decrypted = crypto.decrypt(key, encrypted)

    # Ký
    var signature = crypto.sign(HashingContext.HASH_SHA256, data.sha256_buffer(), key)

    # Xác minh
    var verified = crypto.verify(HashingContext.HASH_SHA256, data.sha256_buffer(), signature, key)

    # Kiểm tra
    assert(verified)
    assert(data.to_utf8_buffer() == decrypted)

 .. code-tab:: csharp

    using Godot;
    using System.Diagnostics;

    Crypto crypto = new Crypto();

    // Tạo khóa RSA mới.
    CryptoKey key = crypto.GenerateRsa(4096);

    // Tạo chứng chỉ tự ký mới với khóa đã cho.
    X509Certificate cert = crypto.GenerateSelfSignedCertificate(key, "CN=mydomain.com,O=My Game Company,C=IT");

    // Lưu khóa và chứng chỉ vào thư mục người dùng.
    key.Save("user://generated.key");
    cert.Save("user://generated.crt");

    // Mã hóa
    string data = "Some data";
    byte[] encrypted = crypto.Encrypt(key, data.ToUtf8Buffer());

    // Giải mã
    byte[] decrypted = crypto.Decrypt(key, encrypted);

    // Ký
    byte[] signature = crypto.Sign(HashingContext.HashType.Sha256, Data.Sha256Buffer(), key);

    // Xác minh
    bool verified = crypto.Verify(HashingContext.HashType.Sha256, Data.Sha256Buffer(), signature, key);

    // Kiểm tra
    Debug.Assert(verified);
    Debug.Assert(data.ToUtf8Buffer() == decrypted);



.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`constant_time_compare<class_Crypto_method_constant_time_compare>`\ (\ trusted\: :ref:`PackedByteArray<class_PackedByteArray>`, received\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                                                       |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`decrypt<class_Crypto_method_decrypt>`\ (\ key\: :ref:`CryptoKey<class_CryptoKey>`, ciphertext\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                                                                                                 |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`encrypt<class_Crypto_method_encrypt>`\ (\ key\: :ref:`CryptoKey<class_CryptoKey>`, plaintext\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                                                                                                  |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`generate_random_bytes<class_Crypto_method_generate_random_bytes>`\ (\ size\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                            |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`CryptoKey<class_CryptoKey>`             | :ref:`generate_rsa<class_Crypto_method_generate_rsa>`\ (\ size\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                              |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`X509Certificate<class_X509Certificate>` | :ref:`generate_self_signed_certificate<class_Crypto_method_generate_self_signed_certificate>`\ (\ key\: :ref:`CryptoKey<class_CryptoKey>`, issuer_name\: :ref:`String<class_String>` = "CN=myserver,O=myorganisation,C=IT", not_before\: :ref:`String<class_String>` = "20140101000000", not_after\: :ref:`String<class_String>` = "20340101000000"\ ) |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`hmac_digest<class_Crypto_method_hmac_digest>`\ (\ hash_type\: :ref:`HashType<enum_HashingContext_HashType>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`, msg\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                         |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`sign<class_Crypto_method_sign>`\ (\ hash_type\: :ref:`HashType<enum_HashingContext_HashType>`, hash\: :ref:`PackedByteArray<class_PackedByteArray>`, key\: :ref:`CryptoKey<class_CryptoKey>`\ )                                                                                                                                                  |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`verify<class_Crypto_method_verify>`\ (\ hash_type\: :ref:`HashType<enum_HashingContext_HashType>`, hash\: :ref:`PackedByteArray<class_PackedByteArray>`, signature\: :ref:`PackedByteArray<class_PackedByteArray>`, key\: :ref:`CryptoKey<class_CryptoKey>`\ )                                                                                   |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Crypto_method_constant_time_compare:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **constant_time_compare**\ (\ trusted\: :ref:`PackedByteArray<class_PackedByteArray>`, received\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_Crypto_method_constant_time_compare>`

Compares two :ref:`PackedByteArray<class_PackedByteArray>`\ s for equality without leaking timing information in order to prevent timing attacks.

Xem `this blog post <https://paragonie.com/blog/2015/11/preventing-timing-attacks-on-string-comparison-with-double-hmac-strategy>`__ để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_decrypt:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **decrypt**\ (\ key\: :ref:`CryptoKey<class_CryptoKey>`, ciphertext\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_Crypto_method_decrypt>`

Giải mã ``ciphertext`` đã cho bằng ``key`` riêng được cung cấp.

\ **Lưu ý:** Kích thước tối đa của ciphertext được chấp nhận bị giới hạn bởi kích thước khóa.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_encrypt:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **encrypt**\ (\ key\: :ref:`CryptoKey<class_CryptoKey>`, plaintext\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_Crypto_method_encrypt>`

Mã hóa ``plaintext`` đã cho bằng ``key`` công khai được cung cấp.

\ **Lưu ý:** Kích thước tối đa của plaintext được chấp nhận bị giới hạn bởi kích thước khóa.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_generate_random_bytes:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **generate_random_bytes**\ (\ size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Crypto_method_generate_random_bytes>`

Tạo một :ref:`PackedByteArray<class_PackedByteArray>` gồm các byte ngẫu nhiên an toàn về mặt mật mã với ``size`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_generate_rsa:

.. rst-class:: classref-method

:ref:`CryptoKey<class_CryptoKey>` **generate_rsa**\ (\ size\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Crypto_method_generate_rsa>`

Tạo một :ref:`CryptoKey<class_CryptoKey>` RSA có thể được dùng để tạo chứng chỉ tự ký và truyền vào :ref:`StreamPeerTLS.accept_stream()<class_StreamPeerTLS_method_accept_stream>`.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_generate_self_signed_certificate:

.. rst-class:: classref-method

:ref:`X509Certificate<class_X509Certificate>` **generate_self_signed_certificate**\ (\ key\: :ref:`CryptoKey<class_CryptoKey>`, issuer_name\: :ref:`String<class_String>` = "CN=myserver,O=myorganisation,C=IT", not_before\: :ref:`String<class_String>` = "20140101000000", not_after\: :ref:`String<class_String>` = "20340101000000"\ ) :ref:`🔗<class_Crypto_method_generate_self_signed_certificate>`

Tạo một :ref:`X509Certificate<class_X509Certificate>` tự ký từ :ref:`CryptoKey<class_CryptoKey>` và ``issuer_name`` đã cho. Thời hạn hiệu lực của chứng chỉ sẽ được xác định bởi ``not_before`` và ``not_after`` (ngày bắt đầu và ngày hết hạn). ``issuer_name`` phải chứa ít nhất "CN=" (common name, tức tên miền), "O=" (organization, tức tên công ty của bạn), "C=" (country, tức mã ISO-3166 gồm 2 chữ cái của quốc gia nơi tổ chức đặt trụ sở).

Một ví dụ nhỏ để tạo khóa RSA và chứng chỉ tự ký X509.


.. tabs::

 .. code-tab:: gdscript

    var crypto = Crypto.new()
    # Tạo khóa RSA 4096 bit.
    var key = crypto.generate_rsa(4096)
    # Tạo chứng chỉ tự ký bằng khóa đã cho.
    var cert = crypto.generate_self_signed_certificate(key, "CN=example.com,O=A Game Company,C=IT")

 .. code-tab:: csharp

    var crypto = new Crypto();
    // Tạo khóa RSA 4096 bit.
    CryptoKey key = crypto.GenerateRsa(4096);
    // Tạo chứng chỉ tự ký bằng khóa đã cho.
    X509Certificate cert = crypto.GenerateSelfSignedCertificate(key, "CN=mydomain.com,O=My Game Company,C=IT");



.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_hmac_digest:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **hmac_digest**\ (\ hash_type\: :ref:`HashType<enum_HashingContext_HashType>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`, msg\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_Crypto_method_hmac_digest>`

Tạo digest `HMAC <https://en.wikipedia.org/wiki/HMAC>`__ từ ``msg`` bằng ``key``. Tham số ``hash_type`` là thuật toán hashing được dùng cho các hash bên trong và bên ngoài.

Hiện tại, chỉ :ref:`HashingContext.HASH_SHA256<class_HashingContext_constant_HASH_SHA256>` và :ref:`HashingContext.HASH_SHA1<class_HashingContext_constant_HASH_SHA1>` được hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_sign:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **sign**\ (\ hash_type\: :ref:`HashType<enum_HashingContext_HashType>`, hash\: :ref:`PackedByteArray<class_PackedByteArray>`, key\: :ref:`CryptoKey<class_CryptoKey>`\ ) :ref:`🔗<class_Crypto_method_sign>`

Ký ``hash`` đã cho thuộc kiểu ``hash_type`` bằng ``key`` riêng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_Crypto_method_verify:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **verify**\ (\ hash_type\: :ref:`HashType<enum_HashingContext_HashType>`, hash\: :ref:`PackedByteArray<class_PackedByteArray>`, signature\: :ref:`PackedByteArray<class_PackedByteArray>`, key\: :ref:`CryptoKey<class_CryptoKey>`\ ) :ref:`🔗<class_Crypto_method_verify>`

Xác minh ``signature`` đã cho đối với ``hash`` thuộc kiểu ``hash_type`` bằng ``key`` công khai được cung cấp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
