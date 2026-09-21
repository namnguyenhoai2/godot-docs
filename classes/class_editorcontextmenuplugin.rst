:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorContextMenuPlugin.xml.

.. _class_EditorContextMenuPlugin:

EditorContextMenuPlugin
=======================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Plugin để thêm các context menu tùy chỉnh trong editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorContextMenuPlugin** cho phép thêm các tùy chọn tùy chỉnh vào context menu của editor.

Hiện tại, context menu được hỗ trợ cho ba khu vực thường dùng: hệ thống tệp, scene tree và panel danh sách script của editor.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_popup_menu<class_EditorContextMenuPlugin_private_method__popup_menu>`\ (\ paths\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual|                                                                                                     |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_context_menu_item<class_EditorContextMenuPlugin_method_add_context_menu_item>`\ (\ name\: :ref:`String<class_String>`, callback\: :ref:`Callable<class_Callable>`, icon\: :ref:`Texture2D<class_Texture2D>` = null\ )                             |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_context_menu_item_from_shortcut<class_EditorContextMenuPlugin_method_add_context_menu_item_from_shortcut>`\ (\ name\: :ref:`String<class_String>`, shortcut\: :ref:`Shortcut<class_Shortcut>`, icon\: :ref:`Texture2D<class_Texture2D>` = null\ ) |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_context_submenu_item<class_EditorContextMenuPlugin_method_add_context_submenu_item>`\ (\ name\: :ref:`String<class_String>`, menu\: :ref:`PopupMenu<class_PopupMenu>`, icon\: :ref:`Texture2D<class_Texture2D>` = null\ )                         |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_menu_shortcut<class_EditorContextMenuPlugin_method_add_menu_shortcut>`\ (\ shortcut\: :ref:`Shortcut<class_Shortcut>`, callback\: :ref:`Callable<class_Callable>`\ )                                                                              |
   +--------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_EditorContextMenuPlugin_ContextMenuSlot:

.. rst-class:: classref-enumeration

enum **ContextMenuSlot**: :ref:`🔗<enum_EditorContextMenuPlugin_ContextMenuSlot>`

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_SCENE_TREE:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_SCENE_TREE** = ``0``

Context menu của dock Scene. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` sẽ được gọi với danh sách các path đến những node hiện đang được chọn, trong khi callback của tùy chọn sẽ nhận danh sách các node hiện đang được chọn.

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_FILESYSTEM:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_FILESYSTEM** = ``1``

Context menu của dock FileSystem. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` và callback của tùy chọn sẽ được gọi với danh sách path của các tệp hiện đang được chọn.

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_SCRIPT_EDITOR:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_SCRIPT_EDITOR** = ``2``

Context menu của các tab script trong editor Script. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` sẽ được gọi với path đến script hiện đang được chỉnh sửa, trong khi callback của tùy chọn sẽ nhận tham chiếu đến script đó.

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_FILESYSTEM_CREATE:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_FILESYSTEM_CREATE** = ``3``

Submenu "Create..." của context menu trong dock FileSystem, hoặc phần "New" của context menu chính khi nhấp vào khoảng trống. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` và callback của tùy chọn sẽ được gọi với path của thư mục hiện đang được chọn. Khi nhấp vào khoảng trống, danh sách path dành cho phương thức popup sẽ trống.

::

    func _popup_menu(paths):
        if paths.is_empty():
            add_context_menu_item("New Image File...", create_image)
        else:
            add_context_menu_item("Image File...", create_image)

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_SCRIPT_EDITOR_CODE:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_SCRIPT_EDITOR_CODE** = ``4``

Context menu của trình soạn thảo code trong editor Script. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` sẽ được gọi với path đến node :ref:`CodeEdit<class_CodeEdit>`. Bạn có thể lấy node này bằng đoạn code sau:

::

    func _popup_menu(paths):
        var code_edit = Engine.get_main_loop().root.get_node(paths[0]);

Callback của tùy chọn sẽ nhận tham chiếu đến node đó. Bạn có thể sử dụng các phương thức của :ref:`CodeEdit<class_CodeEdit>` để thực hiện tra cứu symbol, v.v.

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_SCENE_TABS:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_SCENE_TABS** = ``5``

Context menu của các tab scene. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` sẽ được gọi với path của scene được nhấp, hoặc :ref:`PackedStringArray<class_PackedStringArray>` rỗng nếu menu được mở trên khoảng trống. Callback của tùy chọn sẽ nhận path của scene được nhấp, hoặc :ref:`String<class_String>` rỗng nếu không có scene nào được nhấp.

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_2D_EDITOR:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_2D_EDITOR** = ``6``

Context menu cơ bản khi nhấp chuột phải trong editor 2D. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` sẽ được gọi với path của tất cả các node :ref:`CanvasItem<class_CanvasItem>` bên dưới con trỏ. Bạn có thể lấy chúng bằng đoạn code sau:

::

    func _popup_menu(paths):
        var canvas_item = Engine.get_main_loop().root.get_node(paths[0]); # Thay 0 bằng index mong muốn.

Mảng path sẽ trống nếu không có node nào bên dưới con trỏ. Callback của tùy chọn sẽ nhận một typed array gồm các node :ref:`CanvasItem<class_CanvasItem>`.

.. _class_EditorContextMenuPlugin_constant_CONTEXT_SLOT_INSPECTOR_PROPERTY:

.. rst-class:: classref-enumeration-constant

:ref:`ContextMenuSlot<enum_EditorContextMenuPlugin_ContextMenuSlot>` **CONTEXT_SLOT_INSPECTOR_PROPERTY** = ``7``

Context menu khi nhấp chuột phải trong inspector. :ref:`_popup_menu()<class_EditorContextMenuPlugin_private_method__popup_menu>` sẽ được gọi với một mảng gồm hai phần tử: Phần tử đầu tiên là ID của object, phần tử thứ hai là tên property. Có thể lấy một object từ ID của nó thông qua :ref:`@GlobalScope.instance_from_id()<class_@GlobalScope_method_instance_from_id>` sau khi chuyển ID đó thành int. Callback của tùy chọn sẽ nhận trực tiếp EditorProperty.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_EditorContextMenuPlugin_private_method__popup_menu:

.. rst-class:: classref-method

|void| **_popup_menu**\ (\ paths\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) |virtual| :ref:`🔗<class_EditorContextMenuPlugin_private_method__popup_menu>`

Được gọi khi tạo context menu; có thể thêm các tùy chọn tùy chỉnh bằng cách sử dụng các hàm :ref:`add_context_menu_item()<class_EditorContextMenuPlugin_method_add_context_menu_item>` hoặc :ref:`add_context_menu_item_from_shortcut()<class_EditorContextMenuPlugin_method_add_context_menu_item_from_shortcut>`. ``paths`` chứa các path hiện đang được chọn (tùy thuộc vào menu), có thể được dùng để thêm tùy chọn một cách có điều kiện.

.. rst-class:: classref-item-separator

----

.. _class_EditorContextMenuPlugin_method_add_context_menu_item:

.. rst-class:: classref-method

|void| **add_context_menu_item**\ (\ name\: :ref:`String<class_String>`, callback\: :ref:`Callable<class_Callable>`, icon\: :ref:`Texture2D<class_Texture2D>` = null\ ) :ref:`🔗<class_EditorContextMenuPlugin_method_add_context_menu_item>`

Thêm tùy chọn tùy chỉnh vào context menu của slot được chỉ định cho plugin. Khi tùy chọn được kích hoạt, ``callback`` sẽ được gọi. Callback phải nhận một đối số :ref:`Array<class_Array>` duy nhất; nội dung của mảng phụ thuộc vào context menu slot.

::

    func _popup_menu(paths):
        add_context_menu_item("File Custom options", handle, ICON)

Nếu muốn gán shortcut cho mục menu, hãy sử dụng :ref:`add_context_menu_item_from_shortcut()<class_EditorContextMenuPlugin_method_add_context_menu_item_from_shortcut>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_EditorContextMenuPlugin_method_add_context_menu_item_from_shortcut:

.. rst-class:: classref-method

|void| **add_context_menu_item_from_shortcut**\ (\ name\: :ref:`String<class_String>`, shortcut\: :ref:`Shortcut<class_Shortcut>`, icon\: :ref:`Texture2D<class_Texture2D>` = null\ ) :ref:`🔗<class_EditorContextMenuPlugin_method_add_context_menu_item_from_shortcut>`

Thêm tùy chọn tùy chỉnh vào context menu của slot được chỉ định cho plugin. Tùy chọn này sẽ được gán ``shortcut`` và sử dụng lại callback của nó. Shortcut phải được đăng ký trước bằng :ref:`add_menu_shortcut()<class_EditorContextMenuPlugin_method_add_menu_shortcut>`.

::

    func _init():
        add_menu_shortcut(SHORTCUT, handle)

    func _popup_menu(paths):
        add_context_menu_item_from_shortcut("File Custom options", SHORTCUT, ICON)

.. rst-class:: classref-item-separator

----

.. _class_EditorContextMenuPlugin_method_add_context_submenu_item:

.. rst-class:: classref-method

|void| **add_context_submenu_item**\ (\ name\: :ref:`String<class_String>`, menu\: :ref:`PopupMenu<class_PopupMenu>`, icon\: :ref:`Texture2D<class_Texture2D>` = null\ ) :ref:`🔗<class_EditorContextMenuPlugin_method_add_context_submenu_item>`

Thêm một submenu vào context menu của slot được chỉ định cho plugin. Submenu không được tự động xử lý; bạn cần tự kết nối với các signal của nó. Ngoài ra, submenu sẽ được giải phóng sau mỗi lần popup, vì vậy hãy cung cấp một :ref:`PopupMenu<class_PopupMenu>` mới mỗi lần.

::

    func _popup_menu(paths):
        var popup_menu = PopupMenu.new()
        popup_menu.add_item("Blue")
        popup_menu.add_item("White")
        popup_menu.id_pressed.connect(_on_color_submenu_option)

        add_context_submenu_item("Set Node Color", popup_menu)

.. rst-class:: classref-item-separator

----

.. _class_EditorContextMenuPlugin_method_add_menu_shortcut:

.. rst-class:: classref-method

|void| **add_menu_shortcut**\ (\ shortcut\: :ref:`Shortcut<class_Shortcut>`, callback\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_EditorContextMenuPlugin_method_add_menu_shortcut>`

Đăng ký một shortcut liên kết với context menu của plugin. Phương thức này nên được gọi một lần (ví dụ: trong :ref:`Object._init()<class_Object_private_method__init>` của plugin). ``callback`` sẽ được gọi khi người dùng nhấn ``shortcut`` được chỉ định trong lúc context của menu đang có hiệu lực (ví dụ: dock FileSystem đang được focus). Callback phải nhận một đối số :ref:`Array<class_Array>` duy nhất; nội dung của mảng phụ thuộc vào context menu slot.

::

    func _init():
        add_menu_shortcut(SHORTCUT, handle)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
