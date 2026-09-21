:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorExportPreset.xml.

.. _class_EditorExportPreset:

EditorExportPreset
==================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cấu hình preset export.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đại diện cho cấu hình của một export preset, được tạo bởi hộp thoại export của editor. Một instance **EditorExportPreset** được dùng như một cấu hình chỉ đọc, truyền vào các phương thức :ref:`EditorExportPlatform<class_EditorExportPlatform>` khi export project.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`are_advanced_options_enabled<class_EditorExportPreset_method_are_advanced_options_enabled>`\ (\ ) |const|                                                                                                  |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_custom_features<class_EditorExportPreset_method_get_custom_features>`\ (\ ) |const|                                                                                                                    |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                               | :ref:`get_customized_files<class_EditorExportPreset_method_get_customized_files>`\ (\ ) |const|                                                                                                                  |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                             | :ref:`get_customized_files_count<class_EditorExportPreset_method_get_customized_files_count>`\ (\ ) |const|                                                                                                      |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`get_encrypt_directory<class_EditorExportPreset_method_get_encrypt_directory>`\ (\ ) |const|                                                                                                                |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`get_encrypt_pck<class_EditorExportPreset_method_get_encrypt_pck>`\ (\ ) |const|                                                                                                                            |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_encryption_ex_filter<class_EditorExportPreset_method_get_encryption_ex_filter>`\ (\ ) |const|                                                                                                          |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_encryption_in_filter<class_EditorExportPreset_method_get_encryption_in_filter>`\ (\ ) |const|                                                                                                          |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_encryption_key<class_EditorExportPreset_method_get_encryption_key>`\ (\ ) |const|                                                                                                                      |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_exclude_filter<class_EditorExportPreset_method_get_exclude_filter>`\ (\ ) |const|                                                                                                                      |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>`         | :ref:`get_export_filter<class_EditorExportPreset_method_get_export_filter>`\ (\ ) |const|                                                                                                                        |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_export_path<class_EditorExportPreset_method_get_export_path>`\ (\ ) |const|                                                                                                                            |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>`     | :ref:`get_file_export_mode<class_EditorExportPreset_method_get_file_export_mode>`\ (\ path\: :ref:`String<class_String>`, default\: :ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` = 0\ ) |const| |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                 | :ref:`get_files_to_export<class_EditorExportPreset_method_get_files_to_export>`\ (\ ) |const|                                                                                                                    |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_include_filter<class_EditorExportPreset_method_get_include_filter>`\ (\ ) |const|                                                                                                                      |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                     | :ref:`get_or_env<class_EditorExportPreset_method_get_or_env>`\ (\ name\: :ref:`StringName<class_StringName>`, env_var\: :ref:`String<class_String>`\ ) |const|                                                   |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                 | :ref:`get_patches<class_EditorExportPreset_method_get_patches>`\ (\ ) |const|                                                                                                                                    |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_preset_name<class_EditorExportPreset_method_get_preset_name>`\ (\ ) |const|                                                                                                                            |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                     | :ref:`get_project_setting<class_EditorExportPreset_method_get_project_setting>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ScriptExportMode<enum_EditorExportPreset_ScriptExportMode>` | :ref:`get_script_export_mode<class_EditorExportPreset_method_get_script_export_mode>`\ (\ ) |const|                                                                                                              |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                       | :ref:`get_version<class_EditorExportPreset_method_get_version>`\ (\ name\: :ref:`StringName<class_StringName>`, windows_version\: :ref:`bool<class_bool>`\ ) |const|                                             |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`has<class_EditorExportPreset_method_has>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                    |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`has_export_file<class_EditorExportPreset_method_has_export_file>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                                |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`is_dedicated_server<class_EditorExportPreset_method_is_dedicated_server>`\ (\ ) |const|                                                                                                                    |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                           | :ref:`is_runnable<class_EditorExportPreset_method_is_runnable>`\ (\ ) |const|                                                                                                                                    |
   +-------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_EditorExportPreset_ExportFilter:

.. rst-class:: classref-enumeration

enum **ExportFilter**: :ref:`🔗<enum_EditorExportPreset_ExportFilter>`

.. _class_EditorExportPreset_constant_EXPORT_ALL_RESOURCES:

.. rst-class:: classref-enumeration-constant

:ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>` **EXPORT_ALL_RESOURCES** = ``0``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_EXPORT_SELECTED_SCENES:

.. rst-class:: classref-enumeration-constant

:ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>` **EXPORT_SELECTED_SCENES** = ``1``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_EXPORT_SELECTED_RESOURCES:

.. rst-class:: classref-enumeration-constant

:ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>` **EXPORT_SELECTED_RESOURCES** = ``2``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_EXCLUDE_SELECTED_RESOURCES:

.. rst-class:: classref-enumeration-constant

:ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>` **EXCLUDE_SELECTED_RESOURCES** = ``3``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_EXPORT_CUSTOMIZED:

.. rst-class:: classref-enumeration-constant

:ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>` **EXPORT_CUSTOMIZED** = ``4``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. rst-class:: classref-item-separator

----

.. _enum_EditorExportPreset_FileExportMode:

.. rst-class:: classref-enumeration

enum **FileExportMode**: :ref:`🔗<enum_EditorExportPreset_FileExportMode>`

.. _class_EditorExportPreset_constant_MODE_FILE_NOT_CUSTOMIZED:

.. rst-class:: classref-enumeration-constant

:ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` **MODE_FILE_NOT_CUSTOMIZED** = ``0``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_MODE_FILE_STRIP:

.. rst-class:: classref-enumeration-constant

:ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` **MODE_FILE_STRIP** = ``1``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_MODE_FILE_KEEP:

.. rst-class:: classref-enumeration-constant

:ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` **MODE_FILE_KEEP** = ``2``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_MODE_FILE_REMOVE:

.. rst-class:: classref-enumeration-constant

:ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` **MODE_FILE_REMOVE** = ``3``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. rst-class:: classref-item-separator

----

.. _enum_EditorExportPreset_ScriptExportMode:

.. rst-class:: classref-enumeration

enum **ScriptExportMode**: :ref:`🔗<enum_EditorExportPreset_ScriptExportMode>`

.. _class_EditorExportPreset_constant_MODE_SCRIPT_TEXT:

.. rst-class:: classref-enumeration-constant

:ref:`ScriptExportMode<enum_EditorExportPreset_ScriptExportMode>` **MODE_SCRIPT_TEXT** = ``0``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_MODE_SCRIPT_BINARY_TOKENS:

.. rst-class:: classref-enumeration-constant

:ref:`ScriptExportMode<enum_EditorExportPreset_ScriptExportMode>` **MODE_SCRIPT_BINARY_TOKENS** = ``1``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. _class_EditorExportPreset_constant_MODE_SCRIPT_BINARY_TOKENS_COMPRESSED:

.. rst-class:: classref-enumeration-constant

:ref:`ScriptExportMode<enum_EditorExportPreset_ScriptExportMode>` **MODE_SCRIPT_BINARY_TOKENS_COMPRESSED** = ``2``

.. container:: contribute

	Hiện chưa có mô tả cho enum này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_EditorExportPreset_method_are_advanced_options_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **are_advanced_options_enabled**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_are_advanced_options_enabled>`

Trả về ``true`` nếu nút chuyển đổi "Advanced" được bật trong hộp thoại export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_custom_features:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_custom_features**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_custom_features>`

Trả về danh sách các custom feature được thêm vào preset này, phân tách bằng dấu phẩy, dưới dạng chuỗi. Xem :doc:`Feature tags <../tutorials/export/feature_tags>` trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_customized_files:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_customized_files**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_customized_files>`

Trả về một dictionary gồm các tệp được chọn trong tab "Resources" của hộp thoại export. Các key của dictionary là đường dẫn tệp, còn value là các export mode tương ứng: ``"strip"``, ``"keep"`` hoặc ``"remove"``. Xem thêm :ref:`get_file_export_mode()<class_EditorExportPreset_method_get_file_export_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_customized_files_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_customized_files_count**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_customized_files_count>`

Trả về số lượng tệp được chọn trong tab "Resources" của hộp thoại export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_encrypt_directory:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_encrypt_directory**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_encrypt_directory>`

Trả về ``true`` nếu mã hóa thư mục PCK được bật trong hộp thoại export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_encrypt_pck:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_encrypt_pck**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_encrypt_pck>`

Trả về ``true`` nếu mã hóa PCK được bật trong hộp thoại export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_encryption_ex_filter:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_encryption_ex_filter**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_encryption_ex_filter>`

Trả về các bộ lọc tệp cần loại trừ trong quá trình mã hóa PCK.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_encryption_in_filter:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_encryption_in_filter**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_encryption_in_filter>`

Trả về các bộ lọc tệp cần đưa vào trong quá trình mã hóa PCK.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_encryption_key:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_encryption_key**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_encryption_key>`

Trả về khóa mã hóa PCK.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_exclude_filter:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_exclude_filter**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_exclude_filter>`

Trả về các bộ lọc tệp cần loại trừ trong quá trình export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_export_filter:

.. rst-class:: classref-method

:ref:`ExportFilter<enum_EditorExportPreset_ExportFilter>` **get_export_filter**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_export_filter>`

Trả về chế độ bộ lọc tệp export được chọn trong tab "Resources" của hộp thoại export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_export_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_export_path**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_export_path>`

Trả về đường dẫn đích của export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_file_export_mode:

.. rst-class:: classref-method

:ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` **get_file_export_mode**\ (\ path\: :ref:`String<class_String>`, default\: :ref:`FileExportMode<enum_EditorExportPreset_FileExportMode>` = 0\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_file_export_mode>`

Trả về export mode của tệp được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_files_to_export:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_files_to_export**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_files_to_export>`

Trả về mảng các tệp cần export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_include_filter:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_include_filter**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_include_filter>`

Trả về các bộ lọc tệp cần đưa vào trong quá trình export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_or_env:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_or_env**\ (\ name\: :ref:`StringName<class_StringName>`, env_var\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_or_env>`

Trả về giá trị của tùy chọn export hoặc giá trị của biến môi trường nếu biến đó được thiết lập.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_patches:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_patches**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_patches>`

Trả về danh sách các pack làm cơ sở cho một patch export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_preset_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_preset_name**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_preset_name>`

Trả về tên của export preset này.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_project_setting:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_project_setting**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EditorExportPreset_method_get_project_setting>`

Trả về giá trị của setting được xác định bởi ``name``, sử dụng các override feature tag của export preset thay vì các feature của OS hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_script_export_mode:

.. rst-class:: classref-method

:ref:`ScriptExportMode<enum_EditorExportPreset_ScriptExportMode>` **get_script_export_mode**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_script_export_mode>`

Trả về export mode được sử dụng bởi các tệp GDScript. ``0`` cho "Text", ``1`` cho "Binary tokens" và ``2`` cho "Compressed binary tokens (smaller files)".

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_get_version:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_version**\ (\ name\: :ref:`StringName<class_StringName>`, windows_version\: :ref:`bool<class_bool>`\ ) |const| :ref:`🔗<class_EditorExportPreset_method_get_version>`

Trả về số phiên bản của preset hoặc dùng setting project :ref:`ProjectSettings.application/config/version<class_ProjectSettings_property_application/config/version>` nếu setting này được đặt thành chuỗi rỗng.

Nếu ``windows_version`` là ``true``, định dạng số phiên bản được trả về để tương thích với metadata của tệp thực thi Windows.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_has:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_EditorExportPreset_method_has>`

Trả về ``true`` nếu preset có property có tên ``property``.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_has_export_file:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_export_file**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorExportPreset_method_has_export_file>`

Trả về ``true`` nếu tệp tại ``path`` được chỉ định sẽ được export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_is_dedicated_server:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_dedicated_server**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_is_dedicated_server>`

Trả về ``true`` nếu chế độ export dedicated server được chọn trong hộp thoại export.

.. rst-class:: classref-item-separator

----

.. _class_EditorExportPreset_method_is_runnable:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_runnable**\ (\ ) |const| :ref:`🔗<class_EditorExportPreset_method_is_runnable>`

Trả về ``true`` nếu nút chuyển đổi "Runnable" được bật trong hộp thoại export.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
