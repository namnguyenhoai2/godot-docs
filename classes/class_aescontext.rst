:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AESContext.xml.

.. _class_AESContext:

AESContext
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp quyền truy cập vào chức năng mã hóa/giải mã dữ liệu thô bằng AES.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này lưu trữ thông tin context cần thiết cho các thao tác mã hóa và giải mã bằng AES (Advanced Encryption Standard). Cả hai chế độ AES-ECB và AES-CBC đều được hỗ trợ.


.. tabs::

 .. code-tab:: gdscript

    extends Node

    var aes = AESContext.new()

    func _ready():
        var key = "My secret key!!!" # Key phải có độ dài 16 hoặc 32 byte.
        var data = "My secret text!!" # Kích thước dữ liệu phải là bội số của 16 byte, hãy áp dụng padding nếu cần.
        # Mã hóa ECB
        aes.start(AESContext.MODE_ECB_ENCRYPT, key.to_utf8_buffer())
        var encrypted = aes.update(data.to_utf8_buffer())
        aes.finish()
        # Giải mã ECB
        aes.start(AESContext.MODE_ECB_DECRYPT, key.to_utf8_buffer())
        var decrypted = aes.update(encrypted)
        aes.finish()
        # Kiểm tra ECB
        assert(decrypted == data.to_utf8_buffer())

        var iv = "My secret iv!!!!" # IV phải có chính xác 16 byte.
        # Mã hóa CBC
        aes.start(AESContext.MODE_CBC_ENCRYPT, key.to_utf8_buffer(), iv.to_utf8_buffer())
        encrypted = aes.update(data.to_utf8_buffer())
        aes.finish()
        # Giải mã CBC
        aes.start(AESContext.MODE_CBC_DECRYPT, key.to_utf8_buffer(), iv.to_utf8_buffer())
        decrypted = aes.update(encrypted)
        aes.finish()
        # Kiểm tra CBC
        assert(decrypted == data.to_utf8_buffer())

 .. code-tab:: csharp

    using Godot;
    using System.Diagnostics;

    public partial class MyNode : Node
    {
        private AesContext _aes = new AesContext();

        public override void _Ready()
        {
            string key = "My secret key!!!"; // Key phải có độ dài 16 hoặc 32 byte.
            string data = "My secret text!!"; // Kích thước dữ liệu phải là bội số của 16 byte, hãy áp dụng padding nếu cần.
            // Mã hóa ECB
            _aes.Start(AesContext.Mode.EcbEncrypt, key.ToUtf8Buffer());
            byte[] encrypted = _aes.Update(data.ToUtf8Buffer());
            _aes.Finish();
            // Giải mã ECB
            _aes.Start(AesContext.Mode.EcbDecrypt, key.ToUtf8Buffer());
            byte[] decrypted = _aes.Update(encrypted);
            _aes.Finish();
            // Kiểm tra ECB
            Debug.Assert(decrypted == data.ToUtf8Buffer());

            string iv = "My secret iv!!!!"; // IV phải có chính xác 16 byte.
            // Mã hóa CBC
            _aes.Start(AesContext.Mode.EcbEncrypt, key.ToUtf8Buffer(), iv.ToUtf8Buffer());
            encrypted = _aes.Update(data.ToUtf8Buffer());
            _aes.Finish();
            // Giải mã CBC
            _aes.Start(AesContext.Mode.EcbDecrypt, key.ToUtf8Buffer(), iv.ToUtf8Buffer());
            decrypted = _aes.Update(encrypted);
            _aes.Finish();
            // Kiểm tra CBC
            Debug.Assert(decrypted == data.ToUtf8Buffer());
        }
    }



.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                        | :ref:`finish<class_AESContext_method_finish>`\ (\ )                                                                                                                                                                      |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`get_iv_state<class_AESContext_method_get_iv_state>`\ (\ )                                                                                                                                                          |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`         | :ref:`start<class_AESContext_method_start>`\ (\ mode\: :ref:`Mode<enum_AESContext_Mode>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`, iv\: :ref:`PackedByteArray<class_PackedByteArray>` = PackedByteArray()\ ) |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`update<class_AESContext_method_update>`\ (\ src\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                                 |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AESContext_Mode:

.. rst-class:: classref-enumeration

enum **Mode**: :ref:`🔗<enum_AESContext_Mode>`

.. _class_AESContext_constant_MODE_ECB_ENCRYPT:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AESContext_Mode>` **MODE_ECB_ENCRYPT** = ``0``

Chế độ mã hóa electronic codebook của AES.

.. _class_AESContext_constant_MODE_ECB_DECRYPT:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AESContext_Mode>` **MODE_ECB_DECRYPT** = ``1``

Chế độ giải mã electronic codebook của AES.

.. _class_AESContext_constant_MODE_CBC_ENCRYPT:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AESContext_Mode>` **MODE_CBC_ENCRYPT** = ``2``

Chế độ mã hóa cipher block chaining của AES.

.. _class_AESContext_constant_MODE_CBC_DECRYPT:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AESContext_Mode>` **MODE_CBC_DECRYPT** = ``3``

Chế độ giải mã cipher block chaining của AES.

.. _class_AESContext_constant_MODE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_AESContext_Mode>` **MODE_MAX** = ``4``

Giá trị tối đa của enum mode.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AESContext_method_finish:

.. rst-class:: classref-method

|void| **finish**\ (\ ) :ref:`🔗<class_AESContext_method_finish>`

Đóng context AES này để có thể khởi động lại. Xem :ref:`start()<class_AESContext_method_start>`.

.. rst-class:: classref-item-separator

----

.. _class_AESContext_method_get_iv_state:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **get_iv_state**\ (\ ) :ref:`🔗<class_AESContext_method_get_iv_state>`

Lấy trạng thái IV hiện tại của context này (IV được cập nhật khi gọi :ref:`update()<class_AESContext_method_update>`). Thông thường bạn không cần hàm này.

\ **Lưu ý:** Hàm này chỉ có ý nghĩa khi context được khởi động bằng :ref:`MODE_CBC_ENCRYPT<class_AESContext_constant_MODE_CBC_ENCRYPT>` hoặc :ref:`MODE_CBC_DECRYPT<class_AESContext_constant_MODE_CBC_DECRYPT>`.

.. rst-class:: classref-item-separator

----

.. _class_AESContext_method_start:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **start**\ (\ mode\: :ref:`Mode<enum_AESContext_Mode>`, key\: :ref:`PackedByteArray<class_PackedByteArray>`, iv\: :ref:`PackedByteArray<class_PackedByteArray>` = PackedByteArray()\ ) :ref:`🔗<class_AESContext_method_start>`

Khởi động context AES ở ``mode`` đã cho. Luôn phải cung cấp một ``key`` có độ dài 16 hoặc 32 byte, trong khi ``iv`` (vector khởi tạo) có chính xác 16 byte chỉ cần thiết khi ``mode`` là :ref:`MODE_CBC_ENCRYPT<class_AESContext_constant_MODE_CBC_ENCRYPT>` hoặc :ref:`MODE_CBC_DECRYPT<class_AESContext_constant_MODE_CBC_DECRYPT>`.

.. rst-class:: classref-item-separator

----

.. _class_AESContext_method_update:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **update**\ (\ src\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_AESContext_method_update>`

Thực hiện thao tác mong muốn cho context AES này. Sẽ trả về một :ref:`PackedByteArray<class_PackedByteArray>` chứa kết quả mã hóa (hoặc giải mã) ``src`` đã cho. Xem :ref:`start()<class_AESContext_method_start>` để biết mode hoạt động.

\ **Lưu ý:** Kích thước của ``src`` phải là bội số của 16. Hãy áp dụng padding nếu cần.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
