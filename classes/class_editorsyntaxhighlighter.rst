:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorSyntaxHighlighter.xml.

.. _class_EditorSyntaxHighlighter:

EditorSyntaxHighlighter
=======================

**Kế thừa:** :ref:`SyntaxHighlighter<class_SyntaxHighlighter>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`GDScriptSyntaxHighlighter<class_GDScriptSyntaxHighlighter>`

Lớp cơ sở cho :ref:`SyntaxHighlighter<class_SyntaxHighlighter>` được :ref:`ScriptEditor<class_ScriptEditor>` sử dụng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở mà tất cả :ref:`SyntaxHighlighter<class_SyntaxHighlighter>`\ s được :ref:`ScriptEditor<class_ScriptEditor>` sử dụng đều kế thừa từ đó.

Thêm một bộ tô sáng cú pháp vào từng script bằng cách gọi :ref:`ScriptEditorBase.add_syntax_highlighter()<class_ScriptEditorBase_method_add_syntax_highlighter>`. Để áp dụng cho tất cả script khi mở, hãy gọi :ref:`ScriptEditor.register_syntax_highlighter()<class_ScriptEditor_method_register_syntax_highlighter>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorSyntaxHighlighter<class_EditorSyntaxHighlighter>` | :ref:`_create<class_EditorSyntaxHighlighter_private_method__create>`\ (\ ) |virtual| |const|                                   |
   +---------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                   | :ref:`_get_name<class_EditorSyntaxHighlighter_private_method__get_name>`\ (\ ) |virtual| |const|                               |
   +---------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`             | :ref:`_get_supported_languages<class_EditorSyntaxHighlighter_private_method__get_supported_languages>`\ (\ ) |virtual| |const| |
   +---------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorSyntaxHighlighter_private_method__create:

.. rst-class:: classref-method

:ref:`EditorSyntaxHighlighter<class_EditorSyntaxHighlighter>` **_create**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorSyntaxHighlighter_private_method__create>`

Phương thức virtual tạo một instance mới của bộ tô sáng cú pháp.

.. rst-class:: classref-item-separator

----

.. _class_EditorSyntaxHighlighter_private_method__get_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_name**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorSyntaxHighlighter_private_method__get_name>`

Phương thức virtual có thể được override để trả về tên của bộ tô sáng cú pháp.

.. rst-class:: classref-item-separator

----

.. _class_EditorSyntaxHighlighter_private_method__get_supported_languages:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_supported_languages**\ (\ ) |virtual| |const| :ref:`🔗<class_EditorSyntaxHighlighter_private_method__get_supported_languages>`

Phương thức virtual có thể được override để trả về tên các ngôn ngữ được hỗ trợ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
