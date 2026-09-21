:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/EditorCommandPalette.xml.

.. _class_EditorCommandPalette:

EditorCommandPalette
====================

**Kế thừa:** :ref:`ConfirmationDialog<class_ConfirmationDialog>` **<** :ref:`AcceptDialog<class_AcceptDialog>` **<** :ref:`Window<class_Window>` **<** :ref:`Viewport<class_Viewport>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Command palette của Godot editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng lưu trữ tất cả các Command hiện có và văn bản shortcut của chúng. Có thể truy cập các Command này thông qua menu **Editor > Command Palette**.

Tên key của Command sử dụng dấu gạch chéo để phân biệt các phần, ví dụ: ``"example/command1"`` thì ``example`` sẽ là tên phần.


.. tabs::

 .. code-tab:: gdscript

    var command_palette = EditorInterface.get_command_palette()
    # external_command là một hàm sẽ được gọi khi command được thực thi.
    var command_callable = Callable(self, "external_command").bind(arguments)
    command_palette.add_command("command", "test/command",command_callable)

 .. code-tab:: csharp

    EditorCommandPalette commandPalette = EditorInterface.Singleton.GetCommandPalette();
    // ExternalCommand là một hàm sẽ được gọi khi command được thực thi.
    Callable commandCallable = new Callable(this, MethodName.ExternalCommand);
    commandPalette.AddCommand("command", "test/command", commandCallable)



\ **Lưu ý:** Không nên khởi tạo trực tiếp class này. Thay vào đó, hãy truy cập singleton bằng :ref:`EditorInterface.get_command_palette()<class_EditorInterface_method_get_command_palette>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_command<class_EditorCommandPalette_method_add_command>`\ (\ command_name\: :ref:`String<class_String>`, key_name\: :ref:`String<class_String>`, binded_callable\: :ref:`Callable<class_Callable>`, shortcut_text\: :ref:`String<class_String>` = "None"\ ) |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`remove_command<class_EditorCommandPalette_method_remove_command>`\ (\ key_name\: :ref:`String<class_String>`\ )                                                                                                                                                |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorCommandPalette_method_add_command:

.. rst-class:: classref-method

|void| **add_command**\ (\ command_name\: :ref:`String<class_String>`, key_name\: :ref:`String<class_String>`, binded_callable\: :ref:`Callable<class_Callable>`, shortcut_text\: :ref:`String<class_String>` = "None"\ ) :ref:`🔗<class_EditorCommandPalette_method_add_command>`

Thêm một command tùy chỉnh vào EditorCommandPalette.

- ``command_name``: :ref:`String<class_String>` (Tên của **Command**. Tên này được hiển thị cho người dùng.)

- ``key_name``: :ref:`String<class_String>` (Tên key của một **Command** cụ thể. Tên này được dùng để nhận diện duy nhất **Command**.)

- ``binded_callable``: :ref:`Callable<class_Callable>` (Callable của **Command**. Callable này sẽ được thực thi khi **Command** được chọn.)

- ``shortcut_text``: :ref:`String<class_String>` (Văn bản shortcut của **Command**, nếu có.)

.. rst-class:: classref-item-separator

----

.. _class_EditorCommandPalette_method_remove_command:

.. rst-class:: classref-method

|void| **remove_command**\ (\ key_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_EditorCommandPalette_method_remove_command>`

Xóa command tùy chỉnh khỏi EditorCommandPalette.

- ``key_name``: :ref:`String<class_String>` (Tên key của một **Command** cụ thể.)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
