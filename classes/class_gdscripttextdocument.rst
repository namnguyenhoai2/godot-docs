:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gdscript/doc_classes/GDScriptTextDocument.xml.

.. _class_GDScriptTextDocument:

GDScriptTextDocument
====================

**Đã lỗi thời:** Lớp này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp chức năng language server liên quan đến tài liệu.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp chức năng language server liên quan đến tài liệu.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`codeLens<class_GDScriptTextDocument_method_codeLens>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                    |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`colorPresentation<class_GDScriptTextDocument_method_colorPresentation>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                  |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`completion<class_GDScriptTextDocument_method_completion>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`declaration<class_GDScriptTextDocument_method_declaration>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                              |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`definition<class_GDScriptTextDocument_method_definition>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`didChange<class_GDScriptTextDocument_method_didChange>`\ (\ params\: :ref:`Variant<class_Variant>`\ )                                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`didClose<class_GDScriptTextDocument_method_didClose>`\ (\ params\: :ref:`Variant<class_Variant>`\ )                                          |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`didOpen<class_GDScriptTextDocument_method_didOpen>`\ (\ params\: :ref:`Variant<class_Variant>`\ )                                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`didSave<class_GDScriptTextDocument_method_didSave>`\ (\ params\: :ref:`Variant<class_Variant>`\ )                                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`documentLink<class_GDScriptTextDocument_method_documentLink>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`documentSymbol<class_GDScriptTextDocument_method_documentSymbol>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`foldingRange<class_GDScriptTextDocument_method_foldingRange>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`hover<class_GDScriptTextDocument_method_hover>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                          |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`nativeSymbol<class_GDScriptTextDocument_method_nativeSymbol>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                            |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`prepareRename<class_GDScriptTextDocument_method_prepareRename>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                          |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`           | :ref:`references<class_GDScriptTextDocument_method_references>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`rename<class_GDScriptTextDocument_method_rename>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`resolve<class_GDScriptTextDocument_method_resolve>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                      |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`show_native_symbol_in_editor<class_GDScriptTextDocument_method_show_native_symbol_in_editor>`\ (\ symbol_id\: :ref:`String<class_String>`\ ) |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`signatureHelp<class_GDScriptTextDocument_method_signatureHelp>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                          |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`willSaveWaitUntil<class_GDScriptTextDocument_method_willSaveWaitUntil>`\ (\ params\: :ref:`Variant<class_Variant>`\ )                        |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_GDScriptTextDocument_method_codeLens:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **codeLens**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_codeLens>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_colorPresentation:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **colorPresentation**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_colorPresentation>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_completion:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **completion**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_completion>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_declaration:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **declaration**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_declaration>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_definition:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **definition**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_definition>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_didChange:

.. rst-class:: classref-method

|void| **didChange**\ (\ params\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_didChange>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_didClose:

.. rst-class:: classref-method

|void| **didClose**\ (\ params\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_didClose>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_didOpen:

.. rst-class:: classref-method

|void| **didOpen**\ (\ params\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_didOpen>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_didSave:

.. rst-class:: classref-method

|void| **didSave**\ (\ params\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_didSave>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_documentLink:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **documentLink**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_documentLink>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_documentSymbol:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **documentSymbol**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_documentSymbol>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_foldingRange:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **foldingRange**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_foldingRange>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_hover:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **hover**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_hover>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_nativeSymbol:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **nativeSymbol**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_nativeSymbol>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_prepareRename:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **prepareRename**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_prepareRename>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_references:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **references**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_references>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_rename:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **rename**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_rename>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_resolve:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **resolve**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_resolve>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_show_native_symbol_in_editor:

.. rst-class:: classref-method

|void| **show_native_symbol_in_editor**\ (\ symbol_id\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_show_native_symbol_in_editor>`

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`ScriptEditor.goto_help()<class_ScriptEditor_method_goto_help>`.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_signatureHelp:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **signatureHelp**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_signatureHelp>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptTextDocument_method_willSaveWaitUntil:

.. rst-class:: classref-method

|void| **willSaveWaitUntil**\ (\ params\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_GDScriptTextDocument_method_willSaveWaitUntil>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các endpoint LSP có thể dẫn đến những side effect không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
