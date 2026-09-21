:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PCKPacker.xml.

.. _class_PCKPacker:

PCKPacker
=========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Tạo các package có thể được tải vào một project đang chạy.

.. rst-class:: classref-introduction-group

Mô tả
-----

**PCKPacker** được dùng để tạo các package có thể được tải vào một project đang chạy bằng :ref:`ProjectSettings.load_resource_pack()<class_ProjectSettings_method_load_resource_pack>`.


.. tabs::

 .. code-tab:: gdscript

    var packer = PCKPacker.new()
    packer.pck_start("test.pck")
    packer.add_file("res://text.txt", "text.txt")
    packer.flush()

 .. code-tab:: csharp

    var packer = new PckPacker();
    packer.PckStart("test.pck");
    packer.AddFile("res://text.txt", "text.txt");
    packer.Flush();



**PCKPacker** ở trên tạo package ``test.pck``, sau đó thêm một tệp có tên ``text.txt`` vào thư mục gốc của package.

\ **Lưu ý:** PCK là định dạng tệp pack riêng của Godot. Để tạo các kho lưu trữ ZIP có thể được đọc bởi bất kỳ chương trình nào, hãy dùng :ref:`ZIPPacker<class_ZIPPacker>` thay thế.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`add_file<class_PCKPacker_method_add_file>`\ (\ target_path\: :ref:`String<class_String>`, source_path\: :ref:`String<class_String>`, encrypt\: :ref:`bool<class_bool>` = false\ )                                                                                                               |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`add_file_from_buffer<class_PCKPacker_method_add_file_from_buffer>`\ (\ target_path\: :ref:`String<class_String>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`, encrypt\: :ref:`bool<class_bool>` = false\ )                                                                            |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`add_file_removal<class_PCKPacker_method_add_file_removal>`\ (\ target_path\: :ref:`String<class_String>`\ )                                                                                                                                                                                     |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`flush<class_PCKPacker_method_flush>`\ (\ verbose\: :ref:`bool<class_bool>` = false\ )                                                                                                                                                                                                           |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`pck_start<class_PCKPacker_method_pck_start>`\ (\ pck_path\: :ref:`String<class_String>`, alignment\: :ref:`int<class_int>` = 32, key\: :ref:`String<class_String>` = "0000000000000000000000000000000000000000000000000000000000000000", encrypt_directory\: :ref:`bool<class_bool>` = false\ ) |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PCKPacker_method_add_file:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **add_file**\ (\ target_path\: :ref:`String<class_String>`, source_path\: :ref:`String<class_String>`, encrypt\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PCKPacker_method_add_file>`

Thêm tệp ``source_path`` vào package PCK hiện tại tại đường dẫn nội bộ ``target_path``. Tiền tố ``res://`` của ``target_path`` là tùy chọn và sẽ được loại bỏ nội bộ. Nội dung tệp được ghi ngay vào PCK.

.. rst-class:: classref-item-separator

----

.. _class_PCKPacker_method_add_file_from_buffer:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **add_file_from_buffer**\ (\ target_path\: :ref:`String<class_String>`, data\: :ref:`PackedByteArray<class_PackedByteArray>`, encrypt\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PCKPacker_method_add_file_from_buffer>`

Thêm ``data`` vào package PCK hiện tại tại đường dẫn nội bộ ``target_path``. Tiền tố ``res://`` của ``target_path`` là tùy chọn và sẽ được loại bỏ nội bộ. Nội dung tệp được ghi ngay vào PCK.

.. rst-class:: classref-item-separator

----

.. _class_PCKPacker_method_add_file_removal:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **add_file_removal**\ (\ target_path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PCKPacker_method_add_file_removal>`

Đăng ký việc xóa tệp tại đường dẫn nội bộ ``target_path`` khỏi PCK. Tính năng này chủ yếu được dùng cho các bản patch. Nếu tệp tại đường dẫn này đã được tải từ một PCK trước đó, tệp sẽ bị xóa. Tiền tố ``res://`` của ``target_path`` là tùy chọn và sẽ được loại bỏ nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_PCKPacker_method_flush:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **flush**\ (\ verbose\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PCKPacker_method_flush>`

Ghi thư mục tệp và đóng PCK. Nếu ``verbose`` là ``true``, danh sách các tệp đã thêm sẽ được in ra console để dễ dàng debug hơn.

\ **Lưu ý:** **PCKPacker** sẽ tự động flush khi được giải phóng, xảy ra khi đối tượng ra khỏi phạm vi hoặc khi được gán ``null``. Trong C#, phải dispose reference sau khi sử dụng, entweder bằng câu lệnh ``using`` hoặc bằng cách gọi trực tiếp phương thức ``Dispose``.

.. rst-class:: classref-item-separator

----

.. _class_PCKPacker_method_pck_start:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **pck_start**\ (\ pck_path\: :ref:`String<class_String>`, alignment\: :ref:`int<class_int>` = 32, key\: :ref:`String<class_String>` = "0000000000000000000000000000000000000000000000000000000000000000", encrypt_directory\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PCKPacker_method_pck_start>`

Tạo một tệp PCK mới tại đường dẫn tệp ``pck_path``. Phần mở rộng tệp ``.pck`` không được tự động thêm vào, vì vậy nó phải là một phần của ``pck_path`` (dù không bắt buộc).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
