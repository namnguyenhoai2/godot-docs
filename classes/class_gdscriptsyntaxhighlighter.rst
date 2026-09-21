:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gdscript/doc_classes/GDScriptSyntaxHighlighter.xml.

.. _class_GDScriptSyntaxHighlighter:

Bộ tô sáng cú pháp GDScript
===========================

**Kế thừa:** :ref:`EditorSyntaxHighlighter<class_EditorSyntaxHighlighter>` **<** :ref:`SyntaxHighlighter<class_SyntaxHighlighter>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một bộ tô sáng cú pháp GDScript có thể được sử dụng với các node :ref:`TextEdit<class_TextEdit>` và :ref:`CodeEdit<class_CodeEdit>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Lưu ý:** Class này chỉ có thể được sử dụng cho các editor plugin vì nó phụ thuộc vào các thiết lập của editor.


.. tabs::

 .. code-tab:: gdscript

    var code_preview = TextEdit.new()
    var highlighter = GDScriptSyntaxHighlighter.new()
    code_preview.syntax_highlighter = highlighter

 .. code-tab:: csharp

    var codePreview = new TextEdit();
    var highlighter = new GDScriptSyntaxHighlighter();
    codePreview.SyntaxHighlighter = highlighter;



.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
