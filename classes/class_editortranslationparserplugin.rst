:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorTranslationParserPlugin.xml.

.. _class_EditorTranslationParserPlugin:

EditorTranslationParserPlugin
=============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Plugin dùng để thêm các trình phân tích cú pháp tùy chỉnh nhằm trích xuất các chuỗi cần được dịch từ các tệp tùy chỉnh (.csv, .json, v.v.).

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorTranslationParserPlugin** được gọi khi một tệp đang được phân tích cú pháp để trích xuất các chuỗi cần dịch. Để xác định logic phân tích cú pháp và trích xuất chuỗi, hãy override phương thức :ref:`_parse_file()<class_EditorTranslationParserPlugin_private_method__parse_file>` trong script.

Giá trị trả về phải là một :ref:`Array<class_Array>` gồm các :ref:`PackedStringArray<class_PackedStringArray>`\ s, mỗi phần tử tương ứng với một chuỗi có thể dịch được trích xuất. Mỗi mục phải chứa ``[msgid, msgctxt, msgid_plural, comment, source_line]``, trong đó tất cả các trường ngoại trừ ``msgid`` đều là tùy chọn. Các chuỗi rỗng sẽ bị bỏ qua.

Các chuỗi được trích xuất sẽ được ghi vào tệp mẫu bản dịch do người dùng chọn trong mục "Template Generation" của tab "Localization" trong menu "Project Settings".

Dưới đây là ví dụ về một parser tùy chỉnh trích xuất các chuỗi từ tệp CSV để ghi vào một mẫu.


.. tabs::

 .. code-tab:: gdscript

    @tool
    extends EditorTranslationParserPlugin

    func _parse_file(path):
        var ret: Array[PackedStringArray] = []
        var file = FileAccess.open(path, FileAccess.READ)
        var text = file.get_as_text()
        var split_strs = text.split(",", false)
        for s in split_strs:
            ret.append(PackedStringArray([s]))
            #print("Extracted string: " + s)

        return ret

    func _get_recognized_extensions():
        return ["csv"]

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class CustomParser : EditorTranslationParserPlugin
    {
        public override Godot.Collections.Array<string[]> _ParseFile(string path)
        {
            Godot.Collections.Array<string[]> ret;
            using var file = FileAccess.Open(path, FileAccess.ModeFlags.Read);
            string text = file.GetAsText();
            string[] splitStrs = text.Split(",", allowEmpty: false);
            foreach (string s in splitStrs)
            {
                ret.Add([s]);
                //GD.Print($"Extracted string: {s}");
            }
            return ret;
        }

        public override string[] _GetRecognizedExtensions()
        {
            return ["csv"];
        }
    }



Để thêm một chuỗi có thể dịch được kèm theo context, plural, comment hoặc dòng mã nguồn:


.. tabs::

 .. code-tab:: gdscript

    # Thao tác này sẽ thêm một message với msgid "Test 1", msgctxt "context", msgid_plural "test 1 plurals", comment "test 1 comment" và dòng mã nguồn "7".
    ret.append(PackedStringArray(["Test 1", "context", "test 1 plurals", "test 1 comment", "7"]))
    # Thao tác này sẽ thêm một message với msgid "A test without context" và msgid_plural "plurals".
    ret.append(PackedStringArray(["A test without context", "", "plurals"]))
    # Thao tác này sẽ thêm một message với msgid "Only with context" và msgctxt "a friendly context".
    ret.append(PackedStringArray(["Only with context", "a friendly context"]))

 .. code-tab:: csharp

    // Thao tác này sẽ thêm một message với msgid "Test 1", msgctxt "context", msgid_plural "test 1 plurals", comment "test 1 comment" và dòng mã nguồn "7".
    ret.Add(["Test 1", "context", "test 1 plurals", "test 1 comment", "7"]);
    // Thao tác này sẽ thêm một message với msgid "A test without context" và msgid_plural "plurals".
    ret.Add(["A test without context", "", "plurals"]);
    // Thao tác này sẽ thêm một message với msgid "Only with context" và msgctxt "a friendly context".
    ret.Add(["Only with context", "a friendly context"]);



\ **Lưu ý:** Nếu bạn override logic phân tích cú pháp cho các loại script tiêu chuẩn (GDScript, C#, v.v.), tốt hơn hết là tải đối số ``path`` bằng :ref:`ResourceLoader.load()<class_ResourceLoader_method_load>`. Lý do là các script tích hợp sẵn được tải dưới dạng kiểu :ref:`Resource<class_Resource>`, không phải kiểu :ref:`FileAccess<class_FileAccess>`. Ví dụ:


.. tabs::

 .. code-tab:: gdscript

    func _parse_file(path):
        var res = ResourceLoader.load(path, "Script")
        var text = res.source_code
        # Logic phân tích cú pháp.

    func _get_recognized_extensions():
        return ["gd"]

 .. code-tab:: csharp

    public override Godot.Collections.Array<string[]> _ParseFile(string path)
    {
        var res = ResourceLoader.Load<Script>(path, "Script");
        string text = res.SourceCode;
        // Logic phân tích cú pháp.
    }

    public override string[] _GetRecognizedExtensions()
    {
        return ["gd"];
    }



Ngoài ra, plugin có thể trực tiếp sửa đổi danh sách chuỗi cuối cùng bằng cách triển khai :ref:`_customize_strings()<class_EditorTranslationParserPlugin_private_method__customize_strings>`.

Để sử dụng **EditorTranslationParserPlugin**, trước tiên hãy đăng ký nó bằng phương thức :ref:`EditorPlugin.add_translation_parser_plugin()<class_EditorPlugin_method_add_translation_parser_plugin>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] | :ref:`_customize_strings<class_EditorTranslationParserPlugin_private_method__customize_strings>`\ (\ strings\: :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\]\ ) |virtual| |const| |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                              | :ref:`_get_recognized_extensions<class_EditorTranslationParserPlugin_private_method__get_recognized_extensions>`\ (\ ) |virtual| |const|                                                                           |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] | :ref:`_parse_file<class_EditorTranslationParserPlugin_private_method__parse_file>`\ (\ path\: :ref:`String<class_String>`\ ) |virtual|                                                                             |
   +--------------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorTranslationParserPlugin_private_method__customize_strings:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] **_customize_strings**\ (\ strings\: :ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\]\ ) |virtual| |const| :ref:`🔗<class_EditorTranslationParserPlugin_private_method__customize_strings>`

Được gọi sau khi phân tích cú pháp tất cả các tệp. Bạn có thể sửa đổi mảng ``strings`` để thêm hoặc xóa các mục khỏi danh sách chuỗi cuối cùng, sau đó trả về mảng này sau khi sửa đổi. Mỗi mục là một :ref:`PackedStringArray<class_PackedStringArray>` như được giải thích trong phần mô tả của **EditorTranslationParserPlugin**.

::

    @tool
    extends EditorTranslationParserPlugin

    func _customize_strings(strings):
        # Thêm chuỗi mới.
        strings.append(["Test 1", "context", "test 1 plurals", "test 1 comment"])

        # Xóa tất cả các chuỗi bắt đầu bằng $.
        strings = strings.filter(func(s): return not s[0].begins_with("$"))

        return strings

.. rst-class:: classref-item-separator

----

.. _class_EditorTranslationParserPlugin_private_method__get_recognized_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_recognized_extensions**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorTranslationParserPlugin_private_method__get_recognized_extensions>`

Lấy danh sách phần mở rộng tệp cần liên kết với parser này, ví dụ ``["csv"]``.

.. rst-class:: classref-item-separator

----

.. _class_EditorTranslationParserPlugin_private_method__parse_file:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`PackedStringArray<class_PackedStringArray>`\] **_parse_file**\ (\ path\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_EditorTranslationParserPlugin_private_method__parse_file>`

Override phương thức này để xác định logic phân tích cú pháp tùy chỉnh nhằm trích xuất các chuỗi có thể dịch.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
