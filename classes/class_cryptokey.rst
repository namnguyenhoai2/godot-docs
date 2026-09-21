:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CryptoKey.xml.

.. _class_CryptoKey:

CryptoKey
=========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một khóa mật mã (RSA hoặc elliptic-curve).

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp CryptoKey đại diện cho một khóa mật mã. Các khóa có thể được tải và lưu như mọi :ref:`Resource<class_Resource>` khác.

Chúng có thể được sử dụng để tạo một :ref:`X509Certificate<class_X509Certificate>` tự ký thông qua :ref:`Crypto.generate_self_signed_certificate()<class_Crypto_method_generate_self_signed_certificate>` và làm khóa riêng tư trong :ref:`StreamPeerTLS.accept_stream()<class_StreamPeerTLS_method_accept_stream>` cùng với chứng chỉ thích hợp.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`SSL certificates <../tutorials/networking/ssl_certificates>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_public_only<class_CryptoKey_method_is_public_only>`\ (\ ) |const|                                                                                      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`load<class_CryptoKey_method_load>`\ (\ path\: :ref:`String<class_String>`, public_only\: :ref:`bool<class_bool>` = false\ )                               |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`load_from_string<class_CryptoKey_method_load_from_string>`\ (\ string_key\: :ref:`String<class_String>`, public_only\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`save<class_CryptoKey_method_save>`\ (\ path\: :ref:`String<class_String>`, public_only\: :ref:`bool<class_bool>` = false\ )                               |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`save_to_string<class_CryptoKey_method_save_to_string>`\ (\ public_only\: :ref:`bool<class_bool>` = false\ )                                               |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CryptoKey_method_is_public_only:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_public_only**\ (\ ) |const| :ref:`🔗<class_CryptoKey_method_is_public_only>`

Trả về ``true`` nếu CryptoKey này chỉ có phần công khai mà không có phần riêng tư.

.. rst-class:: classref-item-separator

----

.. _class_CryptoKey_method_load:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`, public_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_CryptoKey_method_load>`

Tải một khóa từ ``path``. Nếu ``public_only`` là ``true``, chỉ khóa công khai sẽ được tải.

\ **Lưu ý:** ``path`` phải là tệp "\*.pub" nếu ``public_only`` là ``true``, nếu không thì phải là tệp "\*.key".

.. rst-class:: classref-item-separator

----

.. _class_CryptoKey_method_load_from_string:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load_from_string**\ (\ string_key\: :ref:`String<class_String>`, public_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_CryptoKey_method_load_from_string>`

Tải một khóa từ ``string_key`` đã cho. Nếu ``public_only`` là ``true``, chỉ khóa công khai sẽ được tải.

.. rst-class:: classref-item-separator

----

.. _class_CryptoKey_method_save:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **save**\ (\ path\: :ref:`String<class_String>`, public_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_CryptoKey_method_save>`

Lưu một khóa vào ``path`` đã cho. Nếu ``public_only`` là ``true``, chỉ khóa công khai sẽ được lưu.

\ **Lưu ý:** ``path`` phải là tệp "\*.pub" nếu ``public_only`` là ``true``, nếu không thì phải là tệp "\*.key".

.. rst-class:: classref-item-separator

----

.. _class_CryptoKey_method_save_to_string:

.. rst-class:: classref-method

:ref:`String<class_String>` **save_to_string**\ (\ public_only\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_CryptoKey_method_save_to_string>`

Trả về một chuỗi chứa khóa ở định dạng PEM. Nếu ``public_only`` là ``true``, chỉ khóa công khai sẽ được bao gồm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
