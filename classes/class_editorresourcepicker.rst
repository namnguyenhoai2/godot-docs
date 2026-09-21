:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorResourcePicker.xml.

.. _class_EditorResourcePicker:

EditorResourcePicker
====================

**Kế thừa:** :ref:`HBoxContainer<class_HBoxContainer>` **<** :ref:`BoxContainer<class_BoxContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`EditorScriptPicker<class_EditorScriptPicker>`

Control của trình soạn thảo Godot dùng để chọn các thuộc tính kiểu :ref:`Resource<class_Resource>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node :ref:`Control<class_Control>` này được dùng trong dock Inspector của trình soạn thảo để cho phép chỉnh sửa các thuộc tính kiểu :ref:`Resource<class_Resource>`. Nó cung cấp các tùy chọn để tạo, tải, lưu và chuyển đổi tài nguyên. Có thể dùng với :ref:`EditorInspectorPlugin<class_EditorInspectorPlugin>` để tái tạo hành vi tương tự.

\ **Lưu ý:** :ref:`Control<class_Control>` này không bao gồm trình soạn thảo cho tài nguyên, vì việc chỉnh sửa được điều khiển bởi chính dock Inspector hoặc các sub-Inspector.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>`     | :ref:`base_type<class_EditorResourcePicker_property_base_type>`             | ``""``    |
   +---------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`         | :ref:`editable<class_EditorResourcePicker_property_editable>`               | ``true``  |
   +---------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`Resource<class_Resource>` | :ref:`edited_resource<class_EditorResourcePicker_property_edited_resource>` |           |
   +---------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`         | :ref:`toggle_mode<class_EditorResourcePicker_property_toggle_mode>`         | ``false`` |
   +---------------------------------+-----------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`_handle_menu_selected<class_EditorResourcePicker_private_method__handle_menu_selected>`\ (\ id\: :ref:`int<class_int>`\ ) |virtual|          |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`_set_create_options<class_EditorResourcePicker_private_method__set_create_options>`\ (\ menu_node\: :ref:`Object<class_Object>`\ ) |virtual| |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_allowed_types<class_EditorResourcePicker_method_get_allowed_types>`\ (\ ) |const|                                                        |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_toggle_pressed<class_EditorResourcePicker_method_set_toggle_pressed>`\ (\ pressed\: :ref:`bool<class_bool>`\ )                           |
   +---------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_EditorResourcePicker_signal_resource_changed:

.. rst-class:: classref-signal

**resource_changed**\ (\ resource\: :ref:`Resource<class_Resource>`\ ) :ref:`🔗<class_EditorResourcePicker_signal_resource_changed>`

Được phát ra khi giá trị của tài nguyên đang được chỉnh sửa thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_signal_resource_selected:

.. rst-class:: classref-signal

**resource_selected**\ (\ resource\: :ref:`Resource<class_Resource>`, inspect\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorResourcePicker_signal_resource_selected>`

Được phát ra khi giá trị tài nguyên được thiết lập và người dùng nhấp vào để chỉnh sửa. Khi ``inspect`` là ``true``, signal này được gây ra bởi tùy chọn "Edit" hoặc "Inspect" trong context menu.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorResourcePicker_property_base_type:

.. rst-class:: classref-property

:ref:`String<class_String>` **base_type** = ``""`` :ref:`🔗<class_EditorResourcePicker_property_base_type>`

.. rst-class:: classref-property-setget

- |void| **set_base_type**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_base_type**\ (\ )

Kiểu cơ sở của các kiểu tài nguyên được phép. Có thể là danh sách nhiều tùy chọn được phân tách bằng dấu phẩy.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_property_editable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editable** = ``true`` :ref:`🔗<class_EditorResourcePicker_property_editable>`

.. rst-class:: classref-property-setget

- |void| **set_editable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_editable**\ (\ )

Nếu ``true``, giá trị có thể được chọn và chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_property_edited_resource:

.. rst-class:: classref-property

:ref:`Resource<class_Resource>` **edited_resource** :ref:`🔗<class_EditorResourcePicker_property_edited_resource>`

.. rst-class:: classref-property-setget

- |void| **set_edited_resource**\ (\ value\: :ref:`Resource<class_Resource>`\ ) - :ref:`Resource<class_Resource>` **get_edited_resource**\ (\ )

Giá trị tài nguyên đang được chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_property_toggle_mode:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **toggle_mode** = ``false`` :ref:`🔗<class_EditorResourcePicker_property_toggle_mode>`

.. rst-class:: classref-property-setget

- |void| **set_toggle_mode**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_toggle_mode**\ (\ )

Nếu ``true``, nút chính có phần xem trước tài nguyên sẽ hoạt động ở chế độ toggle. Dùng :ref:`set_toggle_pressed()<class_EditorResourcePicker_method_set_toggle_pressed>` để đặt trạng thái theo cách thủ công.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorResourcePicker_private_method__handle_menu_selected:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_handle_menu_selected**\ (\ id\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorResourcePicker_private_method__handle_menu_selected>`

Có thể triển khai virtual method này để xử lý các mục trong context menu chưa được xử lý theo mặc định. Xem :ref:`_set_create_options()<class_EditorResourcePicker_private_method__set_create_options>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_private_method__set_create_options:

.. rst-class:: classref-method

|void| **_set_create_options**\ (\ menu_node\: :ref:`Object<class_Object>`\ ) |virtual| :ref:`🔗<class_EditorResourcePicker_private_method__set_create_options>`

Virtual method này được gọi khi cập nhật context menu của một **EditorResourcePicker** :ref:`editable<class_EditorResourcePicker_property_editable>`. Triển khai method này để ghi đè phần các mục "New" bằng những tùy chọn của riêng bạn. ``menu_node`` là một tham chiếu đến node :ref:`PopupMenu<class_PopupMenu>`.

\ **Lưu ý:** Triển khai :ref:`_handle_menu_selected()<class_EditorResourcePicker_private_method__handle_menu_selected>` để xử lý các mục tùy chỉnh này.

\ **Lưu ý:** Các tùy chọn dựng sẵn liên quan ("Load", "Copy", "Paste", v.v.) sẽ tự động được thêm vào ``menu_node`` sau đó, bằng các ID được hard-code bắt đầu từ ``0``. Các tùy chọn tùy chỉnh cần sử dụng những ID không trùng nhau để được xử lý đúng cách. Sử dụng ``id = 100 + custom_option_index`` là an toàn (đây là giá trị mà các mục mặc định trong phần "New" sử dụng).

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_method_get_allowed_types:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_allowed_types**\ (\ ) |const| :ref:`🔗<class_EditorResourcePicker_method_get_allowed_types>`

Trả về danh sách tất cả các kiểu và kiểu con được phép tương ứng với :ref:`base_type<class_EditorResourcePicker_property_base_type>`. Nếu :ref:`base_type<class_EditorResourcePicker_property_base_type>` rỗng, một danh sách rỗng sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_EditorResourcePicker_method_set_toggle_pressed:

.. rst-class:: classref-method

|void| **set_toggle_pressed**\ (\ pressed\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorResourcePicker_method_set_toggle_pressed>`

Thiết lập trạng thái chế độ toggle cho nút chính. Chỉ hoạt động nếu :ref:`toggle_mode<class_EditorResourcePicker_property_toggle_mode>` được đặt thành ``true``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
