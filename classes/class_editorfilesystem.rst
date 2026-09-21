:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorFileSystem.xml.

.. _class_EditorFileSystem:

EditorFileSystem
================

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Hệ thống tệp tài nguyên theo cách editor nhìn thấy.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng này lưu giữ thông tin về tất cả tài nguyên trong hệ thống tệp, loại của chúng, v.v.

\ **Lưu ý:** Không nên khởi tạo trực tiếp class này. Thay vào đó, hãy truy cập singleton bằng :ref:`EditorInterface.get_resource_filesystem()<class_EditorInterface_method_get_resource_filesystem>`.

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_file_type<class_EditorFileSystem_method_get_file_type>`\ (\ path\: :ref:`String<class_String>`\ ) |const|                  |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` | :ref:`get_filesystem<class_EditorFileSystem_method_get_filesystem>`\ (\ )                                                            |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` | :ref:`get_filesystem_path<class_EditorFileSystem_method_get_filesystem_path>`\ (\ path\: :ref:`String<class_String>`\ )              |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                         | :ref:`get_scanning_progress<class_EditorFileSystem_method_get_scanning_progress>`\ (\ ) |const|                                      |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`is_importing<class_EditorFileSystem_method_is_importing>`\ (\ ) |const|                                                        |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`is_scanning<class_EditorFileSystem_method_is_scanning>`\ (\ ) |const|                                                          |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                            | :ref:`reimport_files<class_EditorFileSystem_method_reimport_files>`\ (\ files\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                            | :ref:`scan<class_EditorFileSystem_method_scan>`\ (\ )                                                                                |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                            | :ref:`scan_sources<class_EditorFileSystem_method_scan_sources>`\ (\ )                                                                |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                            | :ref:`update_file<class_EditorFileSystem_method_update_file>`\ (\ path\: :ref:`String<class_String>`\ )                              |
   +-------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_EditorFileSystem_signal_filesystem_changed:

.. rst-class:: classref-signal

**filesystem_changed**\ (\ ) :ref:`🔗<class_EditorFileSystem_signal_filesystem_changed>`

Được phát ra nếu hệ thống tệp đã thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_signal_resources_reimported:

.. rst-class:: classref-signal

**resources_reimported**\ (\ resources\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_EditorFileSystem_signal_resources_reimported>`

Được phát ra nếu một tài nguyên được reimport.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_signal_resources_reimporting:

.. rst-class:: classref-signal

**resources_reimporting**\ (\ resources\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_EditorFileSystem_signal_resources_reimporting>`

Được phát ra trước khi một tài nguyên được reimport.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_signal_resources_reload:

.. rst-class:: classref-signal

**resources_reload**\ (\ resources\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_EditorFileSystem_signal_resources_reload>`

Được phát ra nếu có ít nhất một tài nguyên được reload khi hệ thống tệp được quét.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_signal_script_classes_updated:

.. rst-class:: classref-signal

**script_classes_updated**\ (\ ) :ref:`🔗<class_EditorFileSystem_signal_script_classes_updated>`

Được phát ra khi danh sách các global script class được cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_signal_sources_changed:

.. rst-class:: classref-signal

**sources_changed**\ (\ exist\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorFileSystem_signal_sources_changed>`

Được phát ra nếu source của bất kỳ tệp nào đã import thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorFileSystem_method_get_file_type:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file_type**\ (\ path\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_EditorFileSystem_method_get_file_type>`

Trả về loại tài nguyên của tệp, dựa trên đường dẫn đầy đủ. Phương thức này trả về một chuỗi như ``"Resource"`` hoặc ``"GDScript"``, *không phải* phần mở rộng tệp như ``".gd"``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_get_filesystem:

.. rst-class:: classref-method

:ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` **get_filesystem**\ (\ ) :ref:`🔗<class_EditorFileSystem_method_get_filesystem>`

Lấy đối tượng thư mục gốc.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_get_filesystem_path:

.. rst-class:: classref-method

:ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` **get_filesystem_path**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorFileSystem_method_get_filesystem_path>`

Trả về một chế độ xem vào hệ thống tệp tại ``path``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_get_scanning_progress:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_scanning_progress**\ (\ ) |const| :ref:`🔗<class_EditorFileSystem_method_get_scanning_progress>`

Trả về tiến độ quét từ 0 đến 1 nếu FS đang được quét.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_is_importing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_importing**\ (\ ) |const| :ref:`🔗<class_EditorFileSystem_method_is_importing>`

Trả về ``true`` nếu các tài nguyên hiện đang được import.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_is_scanning:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_scanning**\ (\ ) |const| :ref:`🔗<class_EditorFileSystem_method_is_scanning>`

Trả về ``true`` nếu hệ thống tệp đang được quét.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_reimport_files:

.. rst-class:: classref-method

|void| **reimport_files**\ (\ files\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_EditorFileSystem_method_reimport_files>`

Reimport một tập hợp tệp. Gọi phương thức này nếu các tệp này hoặc các tệp ``.import`` của chúng được chỉnh sửa trực tiếp bằng script hoặc chương trình bên ngoài.

Nếu loại tệp đã thay đổi hoặc tệp vừa được tạo, hãy sử dụng :ref:`update_file()<class_EditorFileSystem_method_update_file>` hoặc :ref:`scan()<class_EditorFileSystem_method_scan>`.

\ **Lưu ý:** Hàm này chặn cho đến khi quá trình import hoàn tất. Tuy nhiên, lượt lặp main loop, bao gồm timer và :ref:`Node._process()<class_Node_private_method__process>`, sẽ diễn ra trong quá trình import do các cập nhật của thanh tiến trình. Tránh gọi :ref:`reimport_files()<class_EditorFileSystem_method_reimport_files>` hoặc :ref:`scan()<class_EditorFileSystem_method_scan>` khi đang import.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_scan:

.. rst-class:: classref-method

|void| **scan**\ (\ ) :ref:`🔗<class_EditorFileSystem_method_scan>`

Quét hệ thống tệp để tìm thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_scan_sources:

.. rst-class:: classref-method

|void| **scan_sources**\ (\ ) :ref:`🔗<class_EditorFileSystem_method_scan_sources>`

Kiểm tra xem source của bất kỳ tài nguyên nào đã import có thay đổi hay không.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystem_method_update_file:

.. rst-class:: classref-method

|void| **update_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorFileSystem_method_update_file>`

Thêm một tệp vào thư mục hiện có hoặc lên lịch cập nhật thông tin tệp khi editor khởi động lại. Có thể dùng để cập nhật các tệp văn bản được lưu bởi một chương trình bên ngoài.

Thao tác này sẽ không import tệp. Để reimport, hãy gọi các phương thức :ref:`reimport_files()<class_EditorFileSystem_method_reimport_files>` hoặc :ref:`scan()<class_EditorFileSystem_method_scan>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
