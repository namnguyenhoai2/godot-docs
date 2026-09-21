:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorScript.xml.

.. _class_EditorScript:

EditorScript
============

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Base script có thể được sử dụng để thêm các hàm mở rộng vào editor.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các script mở rộng class này và triển khai method :ref:`_run()<class_EditorScript_private_method__run>` có thể được thực thi từ tùy chọn **File > Run** của Script Editor (hoặc bằng cách nhấn :kbd:`Ctrl + Shift + X`) khi editor đang chạy. Điều này hữu ích để thêm chức năng tùy chỉnh trong editor cho Godot. Đối với các phần bổ sung phức tạp hơn, hãy cân nhắc sử dụng :ref:`EditorPlugin<class_EditorPlugin>`\ s thay thế.

Nếu một script mở rộng class này cũng có global class name, nó sẽ được đưa vào command palette của editor.

\ **Lưu ý:** Các script mở rộng cần bật chế độ ``tool``.

\ **Ví dụ:** Chạy script sau sẽ in ra "Hello from the Godot Editor!":


.. tabs::

 .. code-tab:: gdscript

    @tool
    extends EditorScript

    func _run():
        print("Hello from the Godot Editor!")

 .. code-tab:: csharp

    using Godot;

    [Tool]
    public partial class HelloEditor : EditorScript
    {
        public override void _Run()
        {
            GD.Print("Hello from the Godot Editor!");
        }
    }



\ **Lưu ý:** EditorScript là :ref:`RefCounted<class_RefCounted>`, nghĩa là nó sẽ bị hủy khi không còn đối tượng nào tham chiếu đến nó. Điều này có thể gây lỗi trong các thao tác bất đồng bộ nếu không có tham chiếu nào đến script.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-----------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | |void|                                        | :ref:`_run<class_EditorScript_private_method__run>`\ (\ ) |virtual| |required|                      |
   +-----------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | |void|                                        | :ref:`add_root_node<class_EditorScript_method_add_root_node>`\ (\ node\: :ref:`Node<class_Node>`\ ) |
   +-----------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | :ref:`EditorInterface<class_EditorInterface>` | :ref:`get_editor_interface<class_EditorScript_method_get_editor_interface>`\ (\ ) |const|           |
   +-----------------------------------------------+-----------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                       | :ref:`get_scene<class_EditorScript_method_get_scene>`\ (\ ) |const|                                 |
   +-----------------------------------------------+-----------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_EditorScript_private_method__run:

.. rst-class:: classref-method

|void| **_run**\ (\ ) |virtual| |required| :ref:`🔗<class_EditorScript_private_method__run>`

Method này được Editor thực thi khi sử dụng **File > Run**.

.. rst-class:: classref-item-separator

----

.. _class_EditorScript_method_add_root_node:

.. rst-class:: classref-method

|void| **add_root_node**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_EditorScript_method_add_root_node>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`EditorInterface.add_root_node()<class_EditorInterface_method_add_root_node>`.

Đặt ``node`` làm root của scene hiện đang mở. Chỉ hoạt động nếu scene trống. Nếu ``node`` là một scene instance, một scene kế thừa sẽ được tạo.

.. rst-class:: classref-item-separator

----

.. _class_EditorScript_method_get_editor_interface:

.. rst-class:: classref-method

:ref:`EditorInterface<class_EditorInterface>` **get_editor_interface**\ (\ ) |const| :ref:`🔗<class_EditorScript_method_get_editor_interface>`

**Đã deprecated:** :ref:`EditorInterface<class_EditorInterface>` là một global singleton và có thể được truy cập trực tiếp bằng tên của nó.

Trả về instance singleton :ref:`EditorInterface<class_EditorInterface>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorScript_method_get_scene:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **get_scene**\ (\ ) |const| :ref:`🔗<class_EditorScript_method_get_scene>`

**Đã deprecated:** Thay vào đó, hãy sử dụng :ref:`EditorInterface.get_edited_scene_root()<class_EditorInterface_method_get_edited_scene_root>`.

Trả về :ref:`Node<class_Node>` root của scene đang được chỉnh sửa (hiện tại). Tương đương với :ref:`EditorInterface.get_edited_scene_root()<class_EditorInterface_method_get_edited_scene_root>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
