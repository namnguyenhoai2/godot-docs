:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/HashingContext.xml.

.. _class_HashingContext:

HashingContext
==============

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp chức năng tính các cryptographic hash theo từng chunk.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp HashingContext cung cấp interface để tính cryptographic hash qua nhiều lần lặp. Hữu ích khi tính hash của các tệp lớn (để bạn không phải tải toàn bộ vào bộ nhớ), network stream và data stream nói chung (để bạn không phải giữ các buffer).

Enum :ref:`HashType<enum_HashingContext_HashType>` cho biết các hashing algorithm được hỗ trợ.


.. tabs::

 .. code-tab:: gdscript

    const CHUNK_SIZE = 1024

    func hash_file(path):
        # Kiểm tra xem tệp có tồn tại hay không.
        if not FileAccess.file_exists(path):
            return
        # Khởi tạo context SHA-256.
        var ctx = HashingContext.new()
        ctx.start(HashingContext.HASH_SHA256)
        # Mở tệp cần tính hash.
        var file = FileAccess.open(path, FileAccess.READ)
        # Cập nhật context sau khi đọc từng chunk.
        while file.get_position() < file.get_length():
            var remaining = file.get_length() - file.get_position()
            ctx.update(file.get_buffer(min(remaining, CHUNK_SIZE)))
        # Lấy hash đã được tính.
        var res = ctx.finish()
        # In kết quả dưới dạng chuỗi hex và array.
        printt(res.hex_encode(), Array(res))

 .. code-tab:: csharp

    public const int ChunkSize = 1024;

    public void HashFile(string path)
    {
        // Kiểm tra xem tệp có tồn tại hay không.
        if (!FileAccess.FileExists(path))
        {
            return;
        }
        // Khởi tạo context SHA-256.
        var ctx = new HashingContext();
        ctx.Start(HashingContext.HashType.Sha256);
        // Mở tệp cần tính hash.
        using var file = FileAccess.Open(path, FileAccess.ModeFlags.Read);
        // Cập nhật context sau khi đọc từng chunk.
        while (file.GetPosition() < file.GetLength())
        {
            int remaining = (int)(file.GetLength() - file.GetPosition());
            ctx.Update(file.GetBuffer(Mathf.Min(remaining, ChunkSize)));
        }
        // Lấy hash đã được tính.
        byte[] res = ctx.Finish();
        // In kết quả dưới dạng chuỗi hex và array.
        GD.PrintT(res.HexEncode(), (Variant)res);
    }



.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`finish<class_HashingContext_method_finish>`\ (\ )                                                        |
   +-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`         | :ref:`start<class_HashingContext_method_start>`\ (\ type\: :ref:`HashType<enum_HashingContext_HashType>`\ )    |
   +-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`         | :ref:`update<class_HashingContext_method_update>`\ (\ chunk\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |
   +-----------------------------------------------+----------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_HashingContext_HashType:

.. rst-class:: classref-enumeration

enum **HashType**: :ref:`🔗<enum_HashingContext_HashType>`

.. _class_HashingContext_constant_HASH_MD5:

.. rst-class:: classref-enumeration-constant

:ref:`HashType<enum_HashingContext_HashType>` **HASH_MD5** = ``0``

Hashing algorithm: MD5.

.. _class_HashingContext_constant_HASH_SHA1:

.. rst-class:: classref-enumeration-constant

:ref:`HashType<enum_HashingContext_HashType>` **HASH_SHA1** = ``1``

Hashing algorithm: SHA-1.

.. _class_HashingContext_constant_HASH_SHA256:

.. rst-class:: classref-enumeration-constant

:ref:`HashType<enum_HashingContext_HashType>` **HASH_SHA256** = ``2``

Hashing algorithm: SHA-256.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_HashingContext_method_finish:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **finish**\ (\ ) :ref:`🔗<class_HashingContext_method_finish>`

Đóng context hiện tại và trả về hash đã được tính.

.. rst-class:: classref-item-separator

----

.. _class_HashingContext_method_start:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **start**\ (\ type\: :ref:`HashType<enum_HashingContext_HashType>`\ ) :ref:`🔗<class_HashingContext_method_start>`

Bắt đầu phép tính hash mới với ``type`` đã cho (ví dụ: :ref:`HASH_SHA256<class_HashingContext_constant_HASH_SHA256>` để bắt đầu tính SHA-256).

.. rst-class:: classref-item-separator

----

.. _class_HashingContext_method_update:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **update**\ (\ chunk\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_HashingContext_method_update>`

Cập nhật phép tính với ``chunk`` dữ liệu đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
