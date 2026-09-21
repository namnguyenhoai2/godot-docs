:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorDock.xml.

.. _class_EditorDock:

EditorDock
==========

**Thử nghiệm:** Class này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`MarginContainer<class_MarginContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`FileSystemDock<class_FileSystemDock>`

Container có thể dock cho editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

EditorDock là một node :ref:`Container<class_Container>` có thể được dock vào một trong các dock slot của editor. Các dock được plugin thêm vào để cung cấp không gian cho những control liên quan đến một :ref:`EditorPlugin<class_EditorPlugin>`. Editor đi kèm một số dock tích hợp sẵn, chẳng hạn như Scene dock, FileSystem dock, v.v.

Bạn có thể thêm một dock bằng cách sử dụng :ref:`EditorPlugin.add_dock()<class_EditorPlugin_method_add_dock>`. Dock có thể được tùy chỉnh bằng cách thay đổi các thuộc tính của nó.

::

    @tool
    extends EditorPlugin

    # Tham chiếu đến dock.
    var dock

    # Khởi tạo plugin.
    func _enter_tree():
        dock = EditorDock.new()
        dock.title = "My Dock"
        dock.dock_icon = preload("./dock_icon.png")
        dock.default_slot = EditorDock.DOCK_SLOT_RIGHT_UL
        var dock_content = preload("./dock_content.tscn").instantiate()
        dock.add_child(dock_content)
        add_dock(dock)

    # Dọn dẹp plugin.
    func _exit_tree():
        remove_dock(dock)
        dock.queue_free()
        dock = null

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Tạo plugin <../tutorials/plugins/editor/making_plugins>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | accessibility_region                                                  | ``true`` (overrides :ref:`Container<class_Container_property_accessibility_region>`) |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`DockLayout<enum_EditorDock_DockLayout>`\] | :ref:`available_layouts<class_EditorDock_property_available_layouts>` | ``5``                                                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`closable<class_EditorDock_property_closable>`                   | ``false``                                                                            |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`DockSlot<enum_EditorDock_DockSlot>`                   | :ref:`default_slot<class_EditorDock_property_default_slot>`           | ``-1``                                                                               |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`                           | :ref:`dock_icon<class_EditorDock_property_dock_icon>`                 |                                                                                      |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`Shortcut<class_Shortcut>`                             | :ref:`dock_shortcut<class_EditorDock_property_dock_shortcut>`         |                                                                                      |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`force_show_icon<class_EditorDock_property_force_show_icon>`     | ``false``                                                                            |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`global<class_EditorDock_property_global>`                       | ``true``                                                                             |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                         | :ref:`icon_name<class_EditorDock_property_icon_name>`                 | ``&""``                                                                              |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                 | :ref:`layout_key<class_EditorDock_property_layout_key>`               | ``""``                                                                               |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                 | :ref:`title<class_EditorDock_property_title>`                         | ``""``                                                                               |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                                   | :ref:`title_color<class_EditorDock_property_title_color>`             | ``Color(0, 0, 0, 0)``                                                                |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                     | :ref:`transient<class_EditorDock_property_transient>`                 | ``false``                                                                            |
   +-------------------------------------------------------------+-----------------------------------------------------------------------+--------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_load_layout_from_config<class_EditorDock_private_method__load_layout_from_config>`\ (\ config\: :ref:`ConfigFile<class_ConfigFile>`, section\: :ref:`String<class_String>`\ ) |virtual|     |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_save_layout_to_config<class_EditorDock_private_method__save_layout_to_config>`\ (\ config\: :ref:`ConfigFile<class_ConfigFile>`, section\: :ref:`String<class_String>`\ ) |virtual| |const| |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_update_layout<class_EditorDock_private_method__update_layout>`\ (\ layout\: :ref:`int<class_int>`\ ) |virtual|                                                                              |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`close<class_EditorDock_method_close>`\ (\ )                                                                                                                                                  |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`make_visible<class_EditorDock_method_make_visible>`\ (\ )                                                                                                                                    |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`open<class_EditorDock_method_open>`\ (\ )                                                                                                                                                    |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_EditorDock_signal_closed:

.. rst-class:: classref-signal

**closed**\ (\ ) :ref:`🔗<class_EditorDock_signal_closed>`

Được phát khi dock bị đóng bằng nút Close trong context popup, trước khi bị xóa khỏi parent. Xem :ref:`closable<class_EditorDock_property_closable>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_signal_opened:

.. rst-class:: classref-signal

**opened**\ (\ ) :ref:`🔗<class_EditorDock_signal_opened>`

Được phát khi dock được mở qua menu Editor > Editor Docks, trước khi được hiển thị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_EditorDock_DockLayout:

.. rst-class:: classref-enumeration

flags **DockLayout**: :ref:`🔗<enum_EditorDock_DockLayout>`

.. _class_EditorDock_constant_DOCK_LAYOUT_VERTICAL:

.. rst-class:: classref-enumeration-constant

:ref:`DockLayout<enum_EditorDock_DockLayout>` **DOCK_LAYOUT_VERTICAL** = ``1``

Cho phép đặt dock vào các dock slot dọc ở hai bên editor.

.. _class_EditorDock_constant_DOCK_LAYOUT_HORIZONTAL:

.. rst-class:: classref-enumeration-constant

:ref:`DockLayout<enum_EditorDock_DockLayout>` **DOCK_LAYOUT_HORIZONTAL** = ``2``

Cho phép đặt dock vào các dock slot ngang ở phía dưới.

.. _class_EditorDock_constant_DOCK_LAYOUT_FLOATING:

.. rst-class:: classref-enumeration-constant

:ref:`DockLayout<enum_EditorDock_DockLayout>` **DOCK_LAYOUT_FLOATING** = ``4``

Cho phép làm dock nổi (được mở dưới dạng một cửa sổ riêng).

.. _class_EditorDock_constant_DOCK_LAYOUT_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`DockLayout<enum_EditorDock_DockLayout>` **DOCK_LAYOUT_ALL** = ``7``

Cho phép đặt dock vào tất cả các slot hiện có.

.. rst-class:: classref-item-separator

----

.. _enum_EditorDock_DockSlot:

.. rst-class:: classref-enumeration

enum **DockSlot**: :ref:`🔗<enum_EditorDock_DockSlot>`

.. _class_EditorDock_constant_DOCK_SLOT_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_NONE** = ``-1``

Dock đã đóng.

.. _class_EditorDock_constant_DOCK_SLOT_LEFT_UL:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_LEFT_UL** = ``0``

Dock slot, bên trái, phía trên bên trái (trống trong layout mặc định).

.. _class_EditorDock_constant_DOCK_SLOT_LEFT_BL:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_LEFT_BL** = ``1``

Dock slot, bên trái, phía dưới bên trái (trống trong layout mặc định).

.. _class_EditorDock_constant_DOCK_SLOT_LEFT_UR:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_LEFT_UR** = ``2``

Dock slot, bên trái, phía trên bên phải (trong layout mặc định bao gồm các dock Scene và Import).

.. _class_EditorDock_constant_DOCK_SLOT_LEFT_BR:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_LEFT_BR** = ``3``

Dock slot, bên trái, phía dưới bên phải (trong layout mặc định bao gồm các dock FileSystem và History).

.. _class_EditorDock_constant_DOCK_SLOT_RIGHT_UL:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_RIGHT_UL** = ``4``

Dock slot, bên phải, phía trên bên trái (trong layout mặc định bao gồm các dock Inspector, Signal và Group).

.. _class_EditorDock_constant_DOCK_SLOT_RIGHT_BL:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_RIGHT_BL** = ``5``

Dock slot, bên phải, phía dưới bên trái (trống trong layout mặc định).

.. _class_EditorDock_constant_DOCK_SLOT_RIGHT_UR:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_RIGHT_UR** = ``6``

Dock slot, bên phải, phía trên bên phải (trống trong layout mặc định).

.. _class_EditorDock_constant_DOCK_SLOT_RIGHT_BR:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_RIGHT_BR** = ``7``

Dock slot, bên phải, phía dưới bên phải (trống trong layout mặc định).

.. _class_EditorDock_constant_DOCK_SLOT_BOTTOM:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_BOTTOM** = ``8``

Bottom panel.

.. _class_EditorDock_constant_DOCK_SLOT_BOTTOM_L:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_BOTTOM_L** = ``9``

Dock slot ở phía dưới, bên dưới bottom panel, ở phía bên trái.

.. _class_EditorDock_constant_DOCK_SLOT_BOTTOM_R:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_BOTTOM_R** = ``10``

Dock slot ở phía dưới, bên dưới bottom panel, ở phía bên phải.

.. _class_EditorDock_constant_DOCK_SLOT_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`DockSlot<enum_EditorDock_DockSlot>` **DOCK_SLOT_MAX** = ``11``

Biểu thị kích thước của enum :ref:`DockSlot<enum_EditorDock_DockSlot>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorDock_property_available_layouts:

.. rst-class:: classref-property

|bitfield|\[:ref:`DockLayout<enum_EditorDock_DockLayout>`\] **available_layouts** = ``5`` :ref:`🔗<class_EditorDock_property_available_layouts>`

.. rst-class:: classref-property-setget

- |void| **set_available_layouts**\ (\ value\: |bitfield|\[:ref:`DockLayout<enum_EditorDock_DockLayout>`\]\ ) - |bitfield|\[:ref:`DockLayout<enum_EditorDock_DockLayout>`\] **get_available_layouts**\ (\ )

Các layout hiện có cho dock này, dưới dạng bitmask. Theo mặc định, dock cho phép các layout dọc và nổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_closable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **closable** = ``false`` :ref:`🔗<class_EditorDock_property_closable>`

.. rst-class:: classref-property-setget

- |void| **set_closable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_closable**\ (\ )

Nếu ``true``, dock có thể được đóng bằng nút Close trong context popup. Các dock bật :ref:`global<class_EditorDock_property_global>` luôn có thể đóng.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_default_slot:

.. rst-class:: classref-property

:ref:`DockSlot<enum_EditorDock_DockSlot>` **default_slot** = ``-1`` :ref:`🔗<class_EditorDock_property_default_slot>`

.. rst-class:: classref-property-setget

- |void| **set_default_slot**\ (\ value\: :ref:`DockSlot<enum_EditorDock_DockSlot>`\ ) - :ref:`DockSlot<enum_EditorDock_DockSlot>` **get_default_slot**\ (\ )

Dock slot mặc định được sử dụng khi thêm dock bằng :ref:`EditorPlugin.add_dock()<class_EditorPlugin_method_add_dock>`.

Sau khi dock được thêm, bạn có thể di chuyển nó sang slot khác và editor sẽ tự động ghi nhớ vị trí giữa các phiên. Nếu bạn xóa rồi thêm lại dock, nó sẽ được đặt lại về mặc định.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_dock_icon:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **dock_icon** :ref:`🔗<class_EditorDock_property_dock_icon>`

.. rst-class:: classref-property-setget

- |void| **set_dock_icon**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_dock_icon**\ (\ )

Icon của dock, dưới dạng một texture. Nếu được chỉ định, nó sẽ ghi đè :ref:`icon_name<class_EditorDock_property_icon_name>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_dock_shortcut:

.. rst-class:: classref-property

:ref:`Shortcut<class_Shortcut>` **dock_shortcut** :ref:`🔗<class_EditorDock_property_dock_shortcut>`

.. rst-class:: classref-property-setget

- |void| **set_dock_shortcut**\ (\ value\: :ref:`Shortcut<class_Shortcut>`\ ) - :ref:`Shortcut<class_Shortcut>` **get_dock_shortcut**\ (\ )

Phím tắt được sử dụng để mở dock.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_force_show_icon:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **force_show_icon** = ``false`` :ref:`🔗<class_EditorDock_property_force_show_icon>`

.. rst-class:: classref-property-setget

- |void| **set_force_show_icon**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_force_show_icon**\ (\ )

Nếu ``true``, dock sẽ luôn hiển thị icon, bất kể :ref:`EditorSettings.interface/editor/docks/dock_tab_style<class_EditorSettings_property_interface/editor/docks/dock_tab_style>` hay :ref:`EditorSettings.interface/editor/docks/bottom_dock_tab_style<class_EditorSettings_property_interface/editor/docks/bottom_dock_tab_style>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_global:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **global** = ``true`` :ref:`🔗<class_EditorDock_property_global>`

.. rst-class:: classref-property-setget

- |void| **set_global**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_global**\ (\ )

Nếu ``true``, dock sẽ xuất hiện trong menu **Editor > Editor Docks** và có thể được đóng. Các dock không global vẫn có thể được đóng bằng :ref:`close()<class_EditorDock_method_close>` hoặc khi :ref:`closable<class_EditorDock_property_closable>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_icon_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **icon_name** = ``&""`` :ref:`🔗<class_EditorDock_property_icon_name>`

.. rst-class:: classref-property-setget

- |void| **set_icon_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_icon_name**\ (\ )

Icon của dock, dưới dạng tên lấy từ loại theme ``EditorIcons`` trong editor theme. Bạn có thể tìm danh sách icon hiện có `here <https://godot-editor-icons.github.io/>`__.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_layout_key:

.. rst-class:: classref-property

:ref:`String<class_String>` **layout_key** = ``""`` :ref:`🔗<class_EditorDock_property_layout_key>`

.. rst-class:: classref-property-setget

- |void| **set_layout_key**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_layout_key**\ (\ )

Key đại diện cho dock này trong layout file của editor. Nếu để trống, tên hiển thị của dock sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_title:

.. rst-class:: classref-property

:ref:`String<class_String>` **title** = ``""`` :ref:`🔗<class_EditorDock_property_title>`

.. rst-class:: classref-property-setget

- |void| **set_title**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_title**\ (\ )

Tiêu đề của tab dock. Nếu để trống, :ref:`Node.name<class_Node_property_name>` của dock sẽ được sử dụng. Nếu tên được tự động tạo (chứa ``@``), tên của child đầu tiên sẽ được sử dụng thay thế.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_title_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **title_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_EditorDock_property_title_color>`

.. rst-class:: classref-property-setget

- |void| **set_title_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_title_color**\ (\ )

Màu tiêu đề của tab dock. Nếu alpha của nó là ``0.0``, màu font mặc định sẽ được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_property_transient:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **transient** = ``false`` :ref:`🔗<class_EditorDock_property_transient>`

.. rst-class:: classref-property-setget

- |void| **set_transient**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_transient**\ (\ )

Nếu ``true``, dock sẽ không tự động được mở hoặc đóng khi tải editor layout, mà chỉ được di chuyển. Dock cũng không thể được mở bằng phím tắt. Thuộc tính này dành cho các dock được mở và đóng trong những trường hợp cụ thể, chẳng hạn khi chọn một node :ref:`TileMap<class_TileMap>` hoặc :ref:`AnimationTree<class_AnimationTree>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorDock_private_method__load_layout_from_config:

.. rst-class:: classref-method

|void| **_load_layout_from_config**\ (\ config\: :ref:`ConfigFile<class_ConfigFile>`, section\: :ref:`String<class_String>`\ ) |virtual| :ref:`🔗<class_EditorDock_private_method__load_layout_from_config>`

Triển khai phương thức này để xử lý việc tải bố cục của dock này. Nó tương đương với :ref:`EditorPlugin._set_window_layout()<class_EditorPlugin_private_method__set_window_layout>`. ``section`` là một section duy nhất dựa trên :ref:`layout_key<class_EditorDock_property_layout_key>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_private_method__save_layout_to_config:

.. rst-class:: classref-method

|void| **_save_layout_to_config**\ (\ config\: :ref:`ConfigFile<class_ConfigFile>`, section\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorDock_private_method__save_layout_to_config>`

Triển khai phương thức này để xử lý việc lưu bố cục của dock này. Nó tương đương với :ref:`EditorPlugin._get_window_layout()<class_EditorPlugin_private_method__get_window_layout>`. ``section`` là một section duy nhất dựa trên :ref:`layout_key<class_EditorDock_property_layout_key>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_private_method__update_layout:

.. rst-class:: classref-method

|void| **_update_layout**\ (\ layout\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorDock_private_method__update_layout>`

Triển khai phương thức này để xử lý việc chuyển đổi bố cục cho dock này. ``layout`` là một trong các hằng số :ref:`DockLayout<enum_EditorDock_DockLayout>`.

::

    func _update_layout(layout):
        box_container.vertical = (layout == DOCK_LAYOUT_VERTICAL)

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_method_close:

.. rst-class:: classref-method

|void| **close**\ (\ ) :ref:`🔗<class_EditorDock_method_close>`

Đóng dock, khiến tab của dock bị ẩn.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_method_make_visible:

.. rst-class:: classref-method

|void| **make_visible**\ (\ ) :ref:`🔗<class_EditorDock_method_make_visible>`

Đưa tiêu điểm vào tab của dock (hoặc cửa sổ nếu dock đang ở trạng thái floating). Nếu dock đã đóng, dock sẽ được mở. Nếu là dock ở dưới, bảng điều khiển phía dưới sẽ hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_EditorDock_method_open:

.. rst-class:: classref-method

|void| **open**\ (\ ) :ref:`🔗<class_EditorDock_method_open>`

Mở dock. Dock sẽ xuất hiện ở vị trí dock được sử dụng lần cuối. Nếu dock không có vị trí mặc định, dock sẽ được mở ở trạng thái floating.

\ **Lưu ý:** Thao tác này không đưa tiêu điểm vào dock. Nếu bạn muốn mở và đưa tiêu điểm vào dock, hãy sử dụng :ref:`make_visible()<class_EditorDock_method_make_visible>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
