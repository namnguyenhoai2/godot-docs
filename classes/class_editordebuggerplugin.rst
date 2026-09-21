:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorDebuggerPlugin.xml.

.. _class_EditorDebuggerPlugin:

EditorDebuggerPlugin
====================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp cơ sở để triển khai các plugin debugger.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorDebuggerPlugin** cung cấp các hàm liên quan đến phía editor của debugger.

Để tương tác với debugger, một instance của lớp này phải được thêm vào editor thông qua :ref:`EditorPlugin.add_debugger_plugin()<class_EditorPlugin_method_add_debugger_plugin>`.

Sau khi được thêm, callback :ref:`_setup_session()<class_EditorDebuggerPlugin_private_method__setup_session>` sẽ được gọi cho mọi :ref:`EditorDebuggerSession<class_EditorDebuggerSession>` khả dụng với plugin và khi có các session mới được tạo (các session có thể không hoạt động trong giai đoạn này).

Bạn có thể lấy các :ref:`EditorDebuggerSession<class_EditorDebuggerSession>`\ s khả dụng thông qua :ref:`get_sessions()<class_EditorDebuggerPlugin_method_get_sessions>` hoặc lấy một session cụ thể thông qua :ref:`get_session()<class_EditorDebuggerPlugin_method_get_session>`.


.. tabs::

 .. code-tab:: gdscript

    @tool
    extends EditorPlugin

    class ExampleEditorDebugger extends EditorDebuggerPlugin:

        func _has_capture(capture):
            # Trả về true nếu bạn muốn xử lý các message có tiền tố "my_plugin:".
            return capture == "my_plugin"

        func _capture(message, data, session_id):
            if message == "my_plugin:ping":
                get_session(session_id).send_message("my_plugin:echo", data)
                return true
            return false

        func _setup_session(session_id):
            # Thêm một tab mới vào giao diện session của debugger, trong đó có một label.
            var label = Label.new()
            label.name = "Example plugin" # Sẽ được dùng làm tiêu đề tab.
            label.text = "Example plugin"
            var session = get_session(session_id)
            # Lắng nghe các signal session started và stopped.
            session.started.connect(func (): print("Session started"))
            session.stopped.connect(func (): print("Session stopped"))
            session.add_session_tab(label)

    var debugger = ExampleEditorDebugger.new()

    func _enter_tree():
        add_debugger_plugin(debugger)

    func _exit_tree():
        remove_debugger_plugin(debugger)



Để kết nối ở phía game đang chạy, hãy sử dụng singleton :ref:`EngineDebugger<class_EngineDebugger>`:


.. tabs::

 .. code-tab:: gdscript

    extends Node

    func _ready():
        EngineDebugger.register_message_capture("my_plugin", _capture)
        EngineDebugger.send_message("my_plugin:ping", ["test"])

    func _capture(message, data):
        # Note that the "my_plugin:" prefix is not used here.
        if message == "echo":
            prints("Echo received:", data)
            return true
        return false



\ **Lưu ý:** Khi game đang chạy, :ref:`@GlobalScope.print()<class_@GlobalScope_method_print>` và các hàm tương tự *được gọi trong editor* sẽ không in gì; Output Log chỉ in các message của game.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`_breakpoint_set_in_tree<class_EditorDebuggerPlugin_private_method__breakpoint_set_in_tree>`\ (\ script\: :ref:`Script<class_Script>`, line\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) |virtual| |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`_breakpoints_cleared_in_tree<class_EditorDebuggerPlugin_private_method__breakpoints_cleared_in_tree>`\ (\ ) |virtual|                                                                                              |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`_capture<class_EditorDebuggerPlugin_private_method__capture>`\ (\ message\: :ref:`String<class_String>`, data\: :ref:`Array<class_Array>`, session_id\: :ref:`int<class_int>`\ ) |virtual|                         |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`_goto_script_line<class_EditorDebuggerPlugin_private_method__goto_script_line>`\ (\ script\: :ref:`Script<class_Script>`, line\: :ref:`int<class_int>`\ ) |virtual|                                                |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                   | :ref:`_has_capture<class_EditorDebuggerPlugin_private_method__has_capture>`\ (\ capture\: :ref:`String<class_String>`\ ) |virtual| |const|                                                                               |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                    | :ref:`_setup_session<class_EditorDebuggerPlugin_private_method__setup_session>`\ (\ session_id\: :ref:`int<class_int>`\ ) |virtual|                                                                                      |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`EditorDebuggerSession<class_EditorDebuggerSession>` | :ref:`get_session<class_EditorDebuggerPlugin_method_get_session>`\ (\ id\: :ref:`int<class_int>`\ )                                                                                                                      |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                 | :ref:`get_sessions<class_EditorDebuggerPlugin_method_get_sessions>`\ (\ )                                                                                                                                                |
   +-----------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorDebuggerPlugin_private_method__breakpoint_set_in_tree:

.. rst-class:: classref-method

|void| **_breakpoint_set_in_tree**\ (\ script\: :ref:`Script<class_Script>`, line\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorDebuggerPlugin_private_method__breakpoint_set_in_tree>`

Ghi đè phương thức này để được thông báo khi một breakpoint được đặt trong editor.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_private_method__breakpoints_cleared_in_tree:

.. rst-class:: classref-method

|void| **_breakpoints_cleared_in_tree**\ (\ ) |virtual| :ref:`🔗<class_EditorDebuggerPlugin_private_method__breakpoints_cleared_in_tree>`

Ghi đè phương thức này để được thông báo khi tất cả breakpoint được xóa trong editor.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_private_method__capture:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_capture**\ (\ message\: :ref:`String<class_String>`, data\: :ref:`Array<class_Array>`, session_id\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorDebuggerPlugin_private_method__capture>`

Ghi đè phương thức này để xử lý các message đến. ``session_id`` là ID của :ref:`EditorDebuggerSession<class_EditorDebuggerSession>` đã nhận ``message``. Sử dụng :ref:`get_session()<class_EditorDebuggerPlugin_method_get_session>` để lấy session. Phương thức này phải trả về ``true`` nếu message được nhận diện.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_private_method__goto_script_line:

.. rst-class:: classref-method

|void| **_goto_script_line**\ (\ script\: :ref:`Script<class_Script>`, line\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorDebuggerPlugin_private_method__goto_script_line>`

Ghi đè phương thức này để được thông báo khi một dòng breakpoint được nhấp trong panel breakpoint của debugger.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_private_method__has_capture:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_has_capture**\ (\ capture\: :ref:`String<class_String>`\ ) |virtual| |const| :ref:`🔗<class_EditorDebuggerPlugin_private_method__has_capture>`

Ghi đè phương thức này để bật khả năng nhận message từ debugger. Nếu ``capture`` là "my_message" thì các message bắt đầu bằng "my_message:" sẽ được truyền đến phương thức :ref:`_capture()<class_EditorDebuggerPlugin_private_method__capture>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_private_method__setup_session:

.. rst-class:: classref-method

|void| **_setup_session**\ (\ session_id\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_EditorDebuggerPlugin_private_method__setup_session>`

Ghi đè phương thức này để được thông báo mỗi khi một :ref:`EditorDebuggerSession<class_EditorDebuggerSession>` mới được tạo. Lưu ý rằng session có thể không hoạt động trong giai đoạn này.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_method_get_session:

.. rst-class:: classref-method

:ref:`EditorDebuggerSession<class_EditorDebuggerSession>` **get_session**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EditorDebuggerPlugin_method_get_session>`

Trả về :ref:`EditorDebuggerSession<class_EditorDebuggerSession>` có ``id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_EditorDebuggerPlugin_method_get_sessions:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_sessions**\ (\ ) :ref:`🔗<class_EditorDebuggerPlugin_method_get_sessions>`

Trả về một mảng các :ref:`EditorDebuggerSession<class_EditorDebuggerSession>` hiện khả dụng với plugin debugger này.

\ **Lưu ý:** Các session trong mảng có thể không hoạt động; hãy kiểm tra trạng thái của chúng thông qua :ref:`EditorDebuggerSession.is_active()<class_EditorDebuggerSession_method_is_active>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
