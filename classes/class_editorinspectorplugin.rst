:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorInspectorPlugin.xml.

.. _class_EditorInspectorPlugin:

EditorInspectorPlugin
=====================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Plugin dùng để thêm các property editor tùy chỉnh vào inspector.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorInspectorPlugin** cho phép thêm các property editor tùy chỉnh vào :ref:`EditorInspector<class_EditorInspector>`.

Khi một object được chỉnh sửa, hàm :ref:`_can_handle()<class_EditorInspectorPlugin_private_method__can_handle>` được gọi và phải trả về ``true`` nếu kiểu của object được hỗ trợ.

Nếu được hỗ trợ, hàm :ref:`_parse_begin()<class_EditorInspectorPlugin_private_method__parse_begin>` sẽ được gọi, cho phép đặt các control tùy chỉnh ở đầu class.

Sau đó, :ref:`_parse_category()<class_EditorInspectorPlugin_private_method__parse_category>` và :ref:`_parse_property()<class_EditorInspectorPlugin_private_method__parse_property>` được gọi cho từng category và property. Chúng cũng cho phép thêm các control tùy chỉnh vào inspector.

Cuối cùng, :ref:`_parse_end()<class_EditorInspectorPlugin_private_method__parse_end>` sẽ được gọi.

Trong mỗi lần gọi này, có thể gọi các hàm "add".

Để sử dụng **EditorInspectorPlugin**, trước tiên hãy đăng ký nó bằng phương thức :ref:`EditorPlugin.add_inspector_plugin()<class_EditorPlugin_method_add_inspector_plugin>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Inspector plugins <../tutorials/plugins/editor/inspector_plugins>`

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`_can_handle<class_EditorInspectorPlugin_private_method__can_handle>`\ (\ object\: :ref:`Object<class_Object>`\ ) |virtual| |const|                                                                                                                                                                                                                                                                                                                                          |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_parse_begin<class_EditorInspectorPlugin_private_method__parse_begin>`\ (\ object\: :ref:`Object<class_Object>`\ ) |virtual|                                                                                                                                                                                                                                                                                                                                                |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_parse_category<class_EditorInspectorPlugin_private_method__parse_category>`\ (\ object\: :ref:`Object<class_Object>`, category\: :ref:`String<class_String>`\ ) |virtual|                                                                                                                                                                                                                                                                                                  |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_parse_end<class_EditorInspectorPlugin_private_method__parse_end>`\ (\ object\: :ref:`Object<class_Object>`\ ) |virtual|                                                                                                                                                                                                                                                                                                                                                    |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_parse_group<class_EditorInspectorPlugin_private_method__parse_group>`\ (\ object\: :ref:`Object<class_Object>`, group\: :ref:`String<class_String>`\ ) |virtual|                                                                                                                                                                                                                                                                                                           |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`_parse_property<class_EditorInspectorPlugin_private_method__parse_property>`\ (\ object\: :ref:`Object<class_Object>`, type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, name\: :ref:`String<class_String>`, hint_type\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>`, hint_string\: :ref:`String<class_String>`, usage_flags\: |bitfield|\[:ref:`PropertyUsageFlags<enum_@GlobalScope_PropertyUsageFlags>`\], wide\: :ref:`bool<class_bool>`\ ) |virtual| |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`add_custom_control<class_EditorInspectorPlugin_method_add_custom_control>`\ (\ control\: :ref:`Control<class_Control>`\ )                                                                                                                                                                                                                                                                                                                                                   |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`add_property_editor<class_EditorInspectorPlugin_method_add_property_editor>`\ (\ property\: :ref:`String<class_String>`, editor\: :ref:`Control<class_Control>`, add_to_end\: :ref:`bool<class_bool>` = false, label\: :ref:`String<class_String>` = ""\ )                                                                                                                                                                                                                  |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`add_property_editor_for_multiple_properties<class_EditorInspectorPlugin_method_add_property_editor_for_multiple_properties>`\ (\ label\: :ref:`String<class_String>`, properties\: :ref:`PackedStringArray<class_PackedStringArray>`, editor\: :ref:`Control<class_Control>`\ )                                                                                                                                                                                             |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorInspectorPlugin_private_method__can_handle:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_can_handle**\ (\ object\: :ref:`Object<class_Object>`\ ) |virtual| |const| :ref:`🔗<class_EditorInspectorPlugin_private_method__can_handle>`

Trả về ``true`` nếu object này có thể được plugin xử lý.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_private_method__parse_begin:

.. rst-class:: classref-method

|void| **_parse_begin**\ (\ object\: :ref:`Object<class_Object>`\ ) |virtual| :ref:`🔗<class_EditorInspectorPlugin_private_method__parse_begin>`

Được gọi để cho phép thêm các control ở đầu danh sách property cho ``object``.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_private_method__parse_category:

.. rst-class:: classref-method

|void| **_parse_category**\ (\ object\: :ref:`Object<class_Object>`, category\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_EditorInspectorPlugin_private_method__parse_category>`

Được gọi để cho phép thêm các control ở đầu một category trong danh sách property cho ``object``.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_private_method__parse_end:

.. rst-class:: classref-method

|void| **_parse_end**\ (\ object\: :ref:`Object<class_Object>`\ ) |virtual| :ref:`🔗<class_EditorInspectorPlugin_private_method__parse_end>`

Được gọi để cho phép thêm các control ở cuối danh sách property cho ``object``.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_private_method__parse_group:

.. rst-class:: classref-method

|void| **_parse_group**\ (\ object\: :ref:`Object<class_Object>`, group\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_EditorInspectorPlugin_private_method__parse_group>`

Được gọi để cho phép thêm các control ở đầu một group hoặc sub-group trong danh sách property cho ``object``.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_private_method__parse_property:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_parse_property**\ (\ object\: :ref:`Object<class_Object>`, type\: :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`, name\: :ref:`String<class_String>`, hint_type\: :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>`, hint_string\: :ref:`String<class_String>`, usage_flags\: |bitfield|\[:ref:`PropertyUsageFlags<enum_@GlobalScope_PropertyUsageFlags>`\], wide\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorInspectorPlugin_private_method__parse_property>`

Được gọi để cho phép thêm các property editor dành riêng cho từng property vào danh sách property của ``object``. Control editor được thêm vào phải mở rộng :ref:`EditorProperty<class_EditorProperty>`. Trả về ``true`` sẽ loại bỏ editor tích hợp sẵn cho property này; nếu không, cho phép chèn một editor tùy chỉnh trước editor tích hợp sẵn.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_method_add_custom_control:

.. rst-class:: classref-method

|void| **add_custom_control**\ (\ control\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_EditorInspectorPlugin_method_add_custom_control>`

Thêm một control tùy chỉnh, không nhất thiết phải là một property editor.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_method_add_property_editor:

.. rst-class:: classref-method

|void| **add_property_editor**\ (\ property\: :ref:`String<class_String>`, editor\: :ref:`Control<class_Control>`, add_to_end\: :ref:`bool<class_bool>` = false, label\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_EditorInspectorPlugin_method_add_property_editor>`

Thêm một property editor cho một property riêng lẻ. Control ``editor`` phải mở rộng :ref:`EditorProperty<class_EditorProperty>`.

Một property có thể có nhiều property editor. Nếu ``add_to_end`` là ``true``, editor mới được thêm này sẽ hiển thị sau tất cả các editor khác của property có ``add_to_end`` là ``false``. Ví dụ: editor sử dụng tham số này để thêm nút "Edit Region" cho :ref:`Sprite2D.region_rect<class_Sprite2D_property_region_rect>` bên dưới editor :ref:`Rect2<class_Rect2>` thông thường.

\ ``label`` có thể được dùng để chọn nhãn tùy chỉnh cho property editor trong inspector. Nếu để trống, nhãn sẽ được tính toán từ tên của property.

.. rst-class:: classref-item-separator

----

.. _class_EditorInspectorPlugin_method_add_property_editor_for_multiple_properties:

.. rst-class:: classref-method

|void| **add_property_editor_for_multiple_properties**\ (\ label\: :ref:`String<class_String>`, properties\: :ref:`PackedStringArray<class_PackedStringArray>`, editor\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_EditorInspectorPlugin_method_add_property_editor_for_multiple_properties>`

Thêm một editor cho phép chỉnh sửa nhiều property. Control ``editor`` phải mở rộng :ref:`EditorProperty<class_EditorProperty>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
