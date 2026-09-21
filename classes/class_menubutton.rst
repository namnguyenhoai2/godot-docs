:github_url: hide

.. meta::
	:keywords: dropdown

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MenuButton.xml.

.. _class_MenuButton:

MenuButton
==========

**Kế thừa:** :ref:`Button<class_Button>` **<** :ref:`BaseButton<class_BaseButton>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một button hiển thị :ref:`PopupMenu<class_PopupMenu>` khi được nhấp.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một button hiển thị :ref:`PopupMenu<class_PopupMenu>` khi được nhấp. Để tạo các mục mới bên trong :ref:`PopupMenu<class_PopupMenu>` này, hãy sử dụng ``get_popup().add_item("My Item Name")``. Bạn cũng có thể tạo chúng trực tiếp từ inspector của Godot editor.

Xem thêm :ref:`BaseButton<class_BaseButton>`, nơi chứa các thuộc tính và phương thức phổ biến liên quan đến node này.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`ActionMode<enum_BaseButton_ActionMode>` | action_mode                                                                                 | ``0`` (overrides :ref:`BaseButton<class_BaseButton_property_action_mode>`)    |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | flat                                                                                        | ``true`` (overrides :ref:`Button<class_Button_property_flat>`)                |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>`      | focus_mode                                                                                  | ``3`` (overrides :ref:`Control<class_Control_property_focus_mode>`)           |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                         | :ref:`item_count<class_MenuButton_property_item_count>`                                     | ``0``                                                                         |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                         | :ref:`popup/item_{index}/checkable<class_MenuButton_property_popup/item_{index}/checkable>` | ``0``                                                                         |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`popup/item_{index}/checked<class_MenuButton_property_popup/item_{index}/checked>`     | ``false``                                                                     |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`popup/item_{index}/disabled<class_MenuButton_property_popup/item_{index}/disabled>`   | ``false``                                                                     |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`             | :ref:`popup/item_{index}/icon<class_MenuButton_property_popup/item_{index}/icon>`           |                                                                               |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                         | :ref:`popup/item_{index}/id<class_MenuButton_property_popup/item_{index}/id>`               | ``0``                                                                         |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`popup/item_{index}/separator<class_MenuButton_property_popup/item_{index}/separator>` | ``false``                                                                     |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                   | :ref:`popup/item_{index}/text<class_MenuButton_property_popup/item_{index}/text>`           | ``""``                                                                        |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`switch_on_hover<class_MenuButton_property_switch_on_hover>`                           | ``false``                                                                     |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | toggle_mode                                                                                 | ``true`` (overrides :ref:`BaseButton<class_BaseButton_property_toggle_mode>`) |
   +-----------------------------------------------+---------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | :ref:`PopupMenu<class_PopupMenu>` | :ref:`get_popup<class_MenuButton_method_get_popup>`\ (\ ) |const|                                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | |void|                            | :ref:`set_disable_shortcuts<class_MenuButton_method_set_disable_shortcuts>`\ (\ disabled\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+
   | |void|                            | :ref:`show_popup<class_MenuButton_method_show_popup>`\ (\ )                                                           |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_MenuButton_signal_about_to_popup:

.. rst-class:: classref-signal

**about_to_popup**\ (\ ) :ref:`🔗<class_MenuButton_signal_about_to_popup>`

Được phát ra khi :ref:`PopupMenu<class_PopupMenu>` của MenuButton này sắp hiển thị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MenuButton_property_item_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **item_count** = ``0`` :ref:`🔗<class_MenuButton_property_item_count>`

.. rst-class:: classref-property-setget

- |void| **set_item_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_item_count**\ (\ )

Số lượng mục hiện có trong danh sách.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/checkable:

.. rst-class:: classref-property

:ref:`int<class_int>` **popup/item_{index}/checkable** = ``0`` :ref:`🔗<class_MenuButton_property_popup/item_{index}/checkable>`

Kiểu mục có thể đánh dấu của mục tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/checked:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **popup/item_{index}/checked** = ``false`` :ref:`🔗<class_MenuButton_property_popup/item_{index}/checked>`

Nếu ``true``, mục tại ``index`` được đánh dấu.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/disabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **popup/item_{index}/disabled** = ``false`` :ref:`🔗<class_MenuButton_property_popup/item_{index}/disabled>`

Nếu ``true``, mục tại ``index`` bị vô hiệu hóa.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/icon:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **popup/item_{index}/icon** :ref:`🔗<class_MenuButton_property_popup/item_{index}/icon>`

Icon của mục tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/id:

.. rst-class:: classref-property

:ref:`int<class_int>` **popup/item_{index}/id** = ``0`` :ref:`🔗<class_MenuButton_property_popup/item_{index}/id>`

ID của mục tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/separator:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **popup/item_{index}/separator** = ``false`` :ref:`🔗<class_MenuButton_property_popup/item_{index}/separator>`

Nếu ``true``, mục tại ``index`` là một dấu phân cách.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_popup/item_{index}/text:

.. rst-class:: classref-property

:ref:`String<class_String>` **popup/item_{index}/text** = ``""`` :ref:`🔗<class_MenuButton_property_popup/item_{index}/text>`

Văn bản của mục tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. item_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_property_switch_on_hover:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **switch_on_hover** = ``false`` :ref:`🔗<class_MenuButton_property_switch_on_hover>`

.. rst-class:: classref-property-setget

- |void| **set_switch_on_hover**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_switch_on_hover**\ (\ )

Nếu ``true``, khi con trỏ di chuột qua một **MenuButton** khác trong cùng parent cũng bật :ref:`switch_on_hover<class_MenuButton_property_switch_on_hover>`, nó sẽ đóng **MenuButton** hiện tại và mở button kia.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MenuButton_method_get_popup:

.. rst-class:: classref-method

:ref:`PopupMenu<class_PopupMenu>` **get_popup**\ (\ ) |const| :ref:`🔗<class_MenuButton_method_get_popup>`

Trả về :ref:`PopupMenu<class_PopupMenu>` được chứa trong button này.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng node này có thể gây crash. Nếu muốn ẩn node này hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`Window.visible<class_Window_property_visible>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_method_set_disable_shortcuts:

.. rst-class:: classref-method

|void| **set_disable_shortcuts**\ (\ disabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_MenuButton_method_set_disable_shortcuts>`

Nếu ``true``, các shortcut bị vô hiệu hóa và không thể được dùng để kích hoạt button.

.. rst-class:: classref-item-separator

----

.. _class_MenuButton_method_show_popup:

.. rst-class:: classref-method

|void| **show_popup**\ (\ ) :ref:`🔗<class_MenuButton_method_show_popup>`

Điều chỉnh vị trí và kích thước popup cho **MenuButton**, sau đó hiển thị :ref:`PopupMenu<class_PopupMenu>`. Nên dùng phương thức này thay cho ``get_popup().popup()``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
