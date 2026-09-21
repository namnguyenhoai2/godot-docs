:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorFileSystemDirectory.xml.

.. _class_EditorFileSystemDirectory:

EditorFileSystemDirectory
=========================

**Kế thừa:** :ref:`Object<class_Object>`

Một thư mục dành cho resource filesystem.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một biến thể tổng quát hơn, cấp thấp hơn của khái niệm thư mục.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                             | :ref:`find_dir_index<class_EditorFileSystemDirectory_method_find_dir_index>`\ (\ name\: :ref:`String<class_String>`\ ) |const|                        |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                             | :ref:`find_file_index<class_EditorFileSystemDirectory_method_find_file_index>`\ (\ name\: :ref:`String<class_String>`\ ) |const|                      |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_file<class_EditorFileSystemDirectory_method_get_file>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                           |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                             | :ref:`get_file_count<class_EditorFileSystemDirectory_method_get_file_count>`\ (\ ) |const|                                                            |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`get_file_import_is_valid<class_EditorFileSystemDirectory_method_get_file_import_is_valid>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|           |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_file_path<class_EditorFileSystemDirectory_method_get_file_path>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                 |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_file_script_class_extends<class_EditorFileSystemDirectory_method_get_file_script_class_extends>`\ (\ idx\: :ref:`int<class_int>`\ ) |const| |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_file_script_class_name<class_EditorFileSystemDirectory_method_get_file_script_class_name>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|       |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                               | :ref:`get_file_type<class_EditorFileSystemDirectory_method_get_file_type>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                 |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_name<class_EditorFileSystemDirectory_method_get_name>`\ (\ )                                                                                |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` | :ref:`get_parent<class_EditorFileSystemDirectory_method_get_parent>`\ (\ )                                                                            |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_path<class_EditorFileSystemDirectory_method_get_path>`\ (\ ) |const|                                                                        |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` | :ref:`get_subdir<class_EditorFileSystemDirectory_method_get_subdir>`\ (\ idx\: :ref:`int<class_int>`\ )                                               |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                             | :ref:`get_subdir_count<class_EditorFileSystemDirectory_method_get_subdir_count>`\ (\ ) |const|                                                        |
   +-------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorFileSystemDirectory_method_find_dir_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **find_dir_index**\ (\ name\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_find_dir_index>`

Trả về chỉ mục của thư mục có tên ``name`` hoặc ``-1`` nếu không tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_find_file_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **find_file_index**\ (\ name\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_find_file_index>`

Trả về chỉ mục của tệp có tên ``name`` hoặc ``-1`` nếu không tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file>`

Trả về tên của tệp tại chỉ mục ``idx``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_file_count**\ (\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file_count>`

Trả về số lượng tệp trong thư mục này.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file_import_is_valid:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_file_import_is_valid**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file_import_is_valid>`

Trả về ``true`` nếu tệp tại chỉ mục ``idx`` được import đúng cách.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file_path**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file_path>`

Trả về đường dẫn đến tệp tại chỉ mục ``idx``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file_script_class_extends:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file_script_class_extends**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file_script_class_extends>`

Trả về base class của script class được định nghĩa trong tệp tại chỉ mục ``idx``. Nếu tệp không định nghĩa script class bằng cú pháp ``class_name``, phương thức này sẽ trả về một chuỗi rỗng.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file_script_class_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file_script_class_name**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file_script_class_name>`

Trả về tên của script class được định nghĩa trong tệp tại chỉ mục ``idx``. Nếu tệp không định nghĩa script class bằng cú pháp ``class_name``, phương thức này sẽ trả về một chuỗi rỗng.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_file_type:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_file_type**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_file_type>`

Trả về loại resource của tệp tại chỉ mục ``idx``. Giá trị trả về là một chuỗi như ``"Resource"`` hoặc ``"GDScript"``, *không phải* phần mở rộng tệp như ``".gd"``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_name**\ (\ ) :ref:`🔗<class_EditorFileSystemDirectory_method_get_name>`

Trả về tên của thư mục này.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_parent:

.. rst-class:: classref-method

:ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` **get_parent**\ (\ ) :ref:`🔗<class_EditorFileSystemDirectory_method_get_parent>`

Trả về thư mục cha của thư mục này hoặc ``null`` nếu được gọi trên một thư mục tại ``res://`` hoặc ``user://``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_path**\ (\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_path>`

Trả về đường dẫn đến thư mục này.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_subdir:

.. rst-class:: classref-method

:ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>` **get_subdir**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EditorFileSystemDirectory_method_get_subdir>`

Trả về thư mục con tại chỉ mục ``idx``.

.. rst-class:: classref-item-separator

----

.. _class_EditorFileSystemDirectory_method_get_subdir_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_subdir_count**\ (\ ) |const| :ref:`🔗<class_EditorFileSystemDirectory_method_get_subdir_count>`

Trả về số lượng thư mục con trong thư mục này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
