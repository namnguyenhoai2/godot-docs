:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorImportPlugin.xml.

.. _class_EditorImportPlugin:

EditorImportPlugin
==================

**Kế thừa:** :ref:`ResourceImporter<class_ResourceImporter>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đăng ký một resource importer tùy chỉnh trong editor. Sử dụng class này để phân tích bất kỳ tệp nào và import tệp đó thành một resource type mới.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorImportPlugin**\ s cung cấp cách mở rộng chức năng import resource của editor. Sử dụng chúng để import resource từ các tệp tùy chỉnh hoặc cung cấp các lựa chọn thay thế cho những importer hiện có của editor.

EditorImportPlugin hoạt động bằng cách liên kết với các phần mở rộng tệp cụ thể và một resource type. Xem :ref:`_get_recognized_extensions()<class_EditorImportPlugin_private_method__get_recognized_extensions>` và :ref:`_get_resource_type()<class_EditorImportPlugin_private_method__get_resource_type>`. Chúng có thể tùy chọn chỉ định một số import preset ảnh hưởng đến quá trình import. EditorImportPlugin chịu trách nhiệm tạo resource và lưu chúng trong thư mục ``.godot/imported`` (xem :ref:`ProjectSettings.application/config/use_hidden_project_data_directory<class_ProjectSettings_property_application/config/use_hidden_project_data_directory>`).

Dưới đây là một EditorImportPlugin mẫu, import một :ref:`Mesh<class_Mesh>` từ tệp có phần mở rộng ".special" hoặc ".spec":


.. tabs::

 .. code-tab:: gdscript

    @tool
    extends EditorImportPlugin

    func _get_importer_name():
        return "my.special.plugin"

    func _get_visible_name():
        return "Special Mesh"

    func _get_recognized_extensions():
        return ["special", "spec"]

    func _get_save_extension():
        return "mesh"

    func _get_resource_type():
        return "Mesh"

    func _get_preset_count():
        return 1

    func _get_preset_name(preset_index):
        return "Default"

    func _get_import_options(path, preset_index):
        return [{"name": "my_option", "default_value": false}]

    func _import(source_file, save_path, options, platform_variants, gen_files):
        var file = FileAccess.open(source_file, FileAccess.READ)
        if file == null:
            return FAILED
        var mesh = ArrayMesh.new()
        # Điền dữ liệu được đọc từ "file" vào Mesh, phần còn lại dành cho người đọc tự thực hiện.

        var filename = save_path + "." + _get_save_extension()
        return ResourceSaver.save(mesh, filename)

 .. code-tab:: csharp

    using Godot;

    public partial class MySpecialPlugin : EditorImportPlugin
    {
        public override string _GetImporterName()
        {
            return "my.special.plugin";
        }

        public override string _GetVisibleName()
        {
            return "Special Mesh";
        }

        public override string[] _GetRecognizedExtensions()
        {
            return ["special", "spec"];
        }

        public override string _GetSaveExtension()
        {
            return "mesh";
        }

        public override string _GetResourceType()
        {
            return "Mesh";
        }

        public override int _GetPresetCount()
        {
            return 1;
        }

        public override string _GetPresetName(int presetIndex)
        {
            return "Default";
        }

        public override Godot.Collections.Array<Godot.Collections.Dictionary> _GetImportOptions(string path, int presetIndex)
        {
            return
            [
                new Godot.Collections.Dictionary
                {
                    { "name", "myOption" },
                    { "default_value", false },
                },
            ];
        }

        public override Error _Import(string sourceFile, string savePath, Godot.Collections.Dictionary options, Godot.Collections.Array<string> platformVariants, Godot.Collections.Array<string> genFiles)
        {
            using var file = FileAccess.Open(sourceFile, FileAccess.ModeFlags.Read);
            if (file.GetError() != Error.Ok)
            {
                return Error.Failed;
            }

            var mesh = new ArrayMesh();
            // Điền dữ liệu được đọc từ "file" vào Mesh, phần còn lại dành cho người đọc tự thực hiện.
            string filename = $"{savePath}.{_GetSaveExtension()}";
            return ResourceSaver.Save(mesh, filename);
        }
    }



Để sử dụng **EditorImportPlugin**, trước tiên hãy đăng ký nó bằng method :ref:`EditorPlugin.add_import_plugin()<class_EditorPlugin_method_add_import_plugin>`.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Import plugins <../tutorials/plugins/editor/import_plugins>`

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_can_import_threaded<class_EditorImportPlugin_private_method__can_import_threaded>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                         |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_format_version<class_EditorImportPlugin_private_method__get_format_version>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                           |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_import_options<class_EditorImportPlugin_private_method__get_import_options>`\ (\ path\: :ref:`String<class_String>`, preset_index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                                                                                                                                                                      |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_import_order<class_EditorImportPlugin_private_method__get_import_order>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                               |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_importer_name<class_EditorImportPlugin_private_method__get_importer_name>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_get_option_visibility<class_EditorImportPlugin_private_method__get_option_visibility>`\ (\ path\: :ref:`String<class_String>`, option_name\: :ref:`StringName<class_StringName>`, options\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| |const|                                                                                                                               |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_preset_count<class_EditorImportPlugin_private_method__get_preset_count>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                               |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_preset_name<class_EditorImportPlugin_private_method__get_preset_name>`\ (\ preset_index\: :ref:`int<class_int>`\ ) |virtual| |required| |const|                                                                                                                                                                                                                                |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`_get_priority<class_EditorImportPlugin_private_method__get_priority>`\ (\ ) |virtual| |const|                                                                                                                                                                                                                                                                                       |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_recognized_extensions<class_EditorImportPlugin_private_method__get_recognized_extensions>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_resource_type<class_EditorImportPlugin_private_method__get_resource_type>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                                                                                                                  |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_save_extension<class_EditorImportPlugin_private_method__get_save_extension>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                                                                                                                |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_visible_name<class_EditorImportPlugin_private_method__get_visible_name>`\ (\ ) |virtual| |required| |const|                                                                                                                                                                                                                                                                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`_import<class_EditorImportPlugin_private_method__import>`\ (\ source_file\: :ref:`String<class_String>`, save_path\: :ref:`String<class_String>`, options\: :ref:`Dictionary<class_Dictionary>`, platform_variants\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\], gen_files\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]\ ) |virtual| |required| |const| |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`append_import_external_resource<class_EditorImportPlugin_method_append_import_external_resource>`\ (\ path\: :ref:`String<class_String>`, custom_options\: :ref:`Dictionary<class_Dictionary>` = {}, custom_importer\: :ref:`String<class_String>` = "", generator_parameters\: :ref:`Variant<class_Variant>` = null\ )                                                             |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_EditorImportPlugin_private_method__can_import_threaded:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_import_threaded**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorImportPlugin_private_method__can_import_threaded>`

Cho biết importer này có thể chạy song song trên các thread hay không, hoặc ngược lại, editor chỉ có thể gọi nó từ main thread một cách an toàn, mỗi lần một tệp.

Nếu implementation của importer này thread-safe và có thể chạy song song, hãy override giá trị này bằng ``true`` để tối ưu concurrency.

Nếu không được override, trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_format_version:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_format_version**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_format_version>`

Lấy format version của importer này. Tăng version này khi thực hiện các thay đổi không tương thích với format của các resource đã import.

Nếu không được override, format version là ``0``.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_import_options:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_import_options**\ (\ path\: :ref:`String<class_String>`, preset_index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_import_options>`

Lấy các tùy chọn và giá trị mặc định cho preset tại index này. Trả về một Array gồm các Dictionary với những key sau: ``name``, ``default_value``, ``property_hint`` (tùy chọn), ``hint_string`` (tùy chọn), ``usage`` (tùy chọn).

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_import_order:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_import_order**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_import_order>`

Lấy thứ tự chạy của importer này khi import resource. Các importer có import order *thấp hơn* sẽ được gọi trước, còn các giá trị cao hơn sẽ được gọi sau. Sử dụng giá trị này để đảm bảo importer chạy sau khi các dependency đã được import. Import order mặc định là ``0``, trừ khi được một importer cụ thể override. Xem :ref:`ImportOrder<enum_ResourceImporter_ImportOrder>` để biết một số giá trị được định nghĩa sẵn.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_importer_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_importer_name**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_importer_name>`

Lấy tên duy nhất của importer.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_option_visibility:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_get_option_visibility**\ (\ path\: :ref:`String<class_String>`, option_name\: :ref:`StringName<class_StringName>`, options\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_option_visibility>`

Lấy thông tin cho biết import option được chỉ định bởi ``option_name`` có nên hiển thị trong Import dock hay không. Implementation mặc định luôn trả về ``true``, khiến mọi option đều hiển thị. Điều này chủ yếu hữu ích để ẩn các option phụ thuộc vào những option khác khi một trong số chúng bị tắt.


.. tabs::

 .. code-tab:: gdscript

    func _get_option_visibility(path, option_name, options):
        # Chỉ hiển thị thiết lập chất lượng lossy nếu compression mode được đặt thành "Lossy".
        if option_name == "compress/lossy_quality" and options.has("compress/mode"):
            return int(options["compress/mode"]) == COMPRESS_LOSSY # Đây là một hằng số mà bạn đặt

        return true

 .. code-tab:: csharp

    public override bool _GetOptionVisibility(string path, StringName optionName, Godot.Collections.Dictionary options)
    {
        // Chỉ hiển thị thiết lập chất lượng lossy nếu compression mode được đặt thành "Lossy".
        if (optionName == "compress/lossy_quality" && options.ContainsKey("compress/mode"))
        {
            return (int)options["compress/mode"] == CompressLossy; // Đây là một hằng số mà bạn đặt
        }

        return true;
    }



.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_preset_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_preset_count**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_preset_count>`

Lấy số lượng preset ban đầu được plugin định nghĩa. Sử dụng :ref:`_get_import_options()<class_EditorImportPlugin_private_method__get_import_options>` để lấy các option mặc định cho preset và :ref:`_get_preset_name()<class_EditorImportPlugin_private_method__get_preset_name>` để lấy tên của preset.

Theo mặc định, không có preset nào.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_preset_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_preset_name**\ (\ preset_index\: :ref:`int<class_int>`\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_preset_name>`

Lấy tên của options preset tại index này.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_priority:

.. rst-class:: classref-method

:ref:`float<class_float>` **_get_priority**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_priority>`

Lấy priority của plugin này đối với phần mở rộng đã nhận diện. Các plugin có priority cao hơn sẽ được ưu tiên. Priority mặc định là ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_recognized_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_recognized_extensions**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_recognized_extensions>`

Lấy danh sách các phần mở rộng tệp được liên kết với loader này (không phân biệt chữ hoa chữ thường). Ví dụ: ``["obj"]``.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_resource_type:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_resource_type**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_resource_type>`

Lấy Godot resource type được liên kết với loader này. Ví dụ: ``"Mesh"`` hoặc ``"Animation"``.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_save_extension:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_save_extension**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_save_extension>`

Lấy phần mở rộng được dùng để lưu resource này trong thư mục ``.godot/imported`` (xem :ref:`ProjectSettings.application/config/use_hidden_project_data_directory<class_ProjectSettings_property_application/config/use_hidden_project_data_directory>`).

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__get_visible_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_visible_name**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__get_visible_name>`

Lấy tên hiển thị trong cửa sổ import. Bạn nên chọn tên này như phần tiếp nối của "Import as", ví dụ: "Import as Special Mesh".

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_private_method__import:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_import**\ (\ source_file\: :ref:`String<class_String>`, save_path\: :ref:`String<class_String>`, options\: :ref:`Dictionary<class_Dictionary>`, platform_variants\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\], gen_files\: :ref:`Array<class_Array>`\[:ref:`String<class_String>`\]\ ) |virtual| |required| |const| :ref:`🔗<class_EditorImportPlugin_private_method__import>`

Import ``source_file`` với import ``options`` được chỉ định. Nên trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu import thành công; các giá trị khác cho biết đã xảy ra lỗi.

Resource đã import dự kiến được lưu vào ``save_path + "." + _get_save_extension()``. Nếu một variant khác được ưu tiên cho :doc:`feature tag <../tutorials/export/feature_tags>`, hãy lưu variant đó vào ``save_path + "." + tag + "." + _get_save_extension()`` và thêm feature tag vào ``platform_variants``.

Nếu các tệp resource bổ sung được tạo trong resource filesystem (``res://``), hãy thêm đường dẫn đầy đủ của chúng vào ``gen_files`` để editor biết chúng phụ thuộc vào ``source_file``.

Method này phải được override để thực hiện công việc import thực tế. Xem phần mô tả của class này để biết ví dụ override method này.

.. rst-class:: classref-item-separator

----

.. _class_EditorImportPlugin_method_append_import_external_resource:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **append_import_external_resource**\ (\ path\: :ref:`String<class_String>`, custom_options\: :ref:`Dictionary<class_Dictionary>` = {}, custom_importer\: :ref:`String<class_String>` = "", generator_parameters\: :ref:`Variant<class_Variant>` = null\ ) :ref:`🔗<class_EditorImportPlugin_method_append_import_external_resource>`

Function này chỉ có thể được gọi trong callback :ref:`_import()<class_EditorImportPlugin_private_method__import>` và cho phép import resource thủ công từ callback đó. Điều này hữu ích khi tệp đã import tạo ra các resource bên ngoài cần được import (ví dụ: hình ảnh). Có thể truyền các tham số tùy chỉnh cho tệp ".import" thông qua ``custom_options``. Ngoài ra, trong trường hợp có nhiều importer có thể xử lý một tệp, có thể chỉ định ``custom_importer`` để buộc sử dụng một importer cụ thể. Function này thực hiện import resource và trả về ngay lập tức cùng với mã thành công hoặc lỗi. ``generator_parameters`` định nghĩa metadata bổ sung tùy chọn, được lưu dưới dạng ``generator_parameters`` trong section ``remap`` của tệp ``.import``, chẳng hạn để lưu md5 hash của dữ liệu nguồn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
