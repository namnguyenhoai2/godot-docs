:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/gdscript/doc_classes/GDScriptWorkspace.xml.

.. _class_GDScriptWorkspace:

GDScriptWorkspace
=================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Chức năng language server liên quan đến workspace.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp chức năng language server liên quan đến workspace.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`apply_new_signal<class_GDScriptWorkspace_method_apply_new_signal>`\ (\ obj\: :ref:`Object<class_Object>`, function\: :ref:`String<class_String>`, args\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`didDeleteFiles<class_GDScriptWorkspace_method_didDeleteFiles>`\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ )                                                                                            |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`   | :ref:`generate_script_api<class_GDScriptWorkspace_method_generate_script_api>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                            |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_file_path<class_GDScriptWorkspace_method_get_file_path>`\ (\ uri\: :ref:`String<class_String>`\ )                                                                                                         |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_file_uri<class_GDScriptWorkspace_method_get_file_uri>`\ (\ path\: :ref:`String<class_String>`\ ) |const|                                                                                                  |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`parse_local_script<class_GDScriptWorkspace_method_parse_local_script>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`parse_script<class_GDScriptWorkspace_method_parse_script>`\ (\ path\: :ref:`String<class_String>`, content\: :ref:`String<class_String>`\ )                                                                   |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`publish_diagnostics<class_GDScriptWorkspace_method_publish_diagnostics>`\ (\ path\: :ref:`String<class_String>`\ )                                                                                            |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GDScriptWorkspace_method_apply_new_signal:

.. rst-class:: classref-method

|void| **apply_new_signal**\ (\ obj\: :ref:`Object<class_Object>`, function\: :ref:`String<class_String>`, args\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_apply_new_signal>`

**Đã lỗi thời:** Có thể gây ra các tác dụng phụ không mong muốn đối với các client đã kết nối.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_didDeleteFiles:

.. rst-class:: classref-method

|void| **didDeleteFiles**\ (\ params\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_didDeleteFiles>`

**Đã lỗi thời:** Việc truy cập trực tiếp vào các LSP endpoint có thể dẫn đến những tác dụng phụ không mong muốn. Hãy kết nối với server qua TCP như một language server client thông thường.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_generate_script_api:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **generate_script_api**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_generate_script_api>`

Trả về interface của script dưới dạng máy có thể đọc được.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_get_file_path:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file_path**\ (\ uri\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_get_file_path>`

Chuyển đổi URI thành đường dẫn tệp.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_get_file_uri:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_file_uri**\ (\ path\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_GDScriptWorkspace_method_get_file_uri>`

Chuyển đổi đường dẫn tệp thành URI.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_parse_local_script:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **parse_local_script**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_parse_local_script>`

**Đã lỗi thời:** Có thể gây ra các tác dụng phụ không mong muốn đối với các client đã kết nối.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_parse_script:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **parse_script**\ (\ path\: :ref:`String<class_String>`, content\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_parse_script>`

**Đã lỗi thời:** Có thể gây ra các tác dụng phụ không mong muốn đối với các client đã kết nối.

.. rst-class:: classref-item-separator

----

.. _class_GDScriptWorkspace_method_publish_diagnostics:

.. rst-class:: classref-method

|void| **publish_diagnostics**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_GDScriptWorkspace_method_publish_diagnostics>`

**Đã lỗi thời:** Có thể gây ra các tác dụng phụ không mong muốn đối với các client đã kết nối.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
