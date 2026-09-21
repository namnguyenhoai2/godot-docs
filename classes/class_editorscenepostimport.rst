:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorScenePostImport.xml.

.. _class_EditorScenePostImport:

EditorScenePostImport
=====================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Xử lý hậu kỳ các scene sau khi import.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các scene đã import có thể được tự động sửa đổi ngay sau khi import bằng cách đặt thuộc tính Import **Custom Script** của chúng thành một script ``tool`` kế thừa từ class này.

Callback :ref:`_post_import()<class_EditorScenePostImport_private_method__post_import>` nhận node gốc của scene đã import và trả về phiên bản đã sửa đổi của scene:


.. tabs::

 .. code-tab:: gdscript

    @tool # Cần thiết để nó chạy trong editor.
    extends EditorScenePostImport

    # Mẫu này thay đổi tên của tất cả các node.
    # Được gọi ngay sau khi scene được import và nhận node gốc.
    func _post_import(scene):
        # Thay đổi tên của tất cả các node thành "modified_[oldnodename]"
        iterate(scene)
        return scene # Hãy nhớ trả về scene đã import

    func iterate(node):
        if node != null:
            node.name = "modified_" + node.name
            for child in node.get_children():
                iterate(child)

 .. code-tab:: csharp

    using Godot;

    // Mẫu này thay đổi tên của tất cả các node.
    // Được gọi ngay sau khi scene được import và nhận node gốc.
    [Tool]
    public partial class NodeRenamer : EditorScenePostImport
    {
        public override GodotObject _PostImport(Node scene)
        {
            // Thay đổi tên của tất cả các node thành "modified_[oldnodename]"
            Iterate(scene);
            return scene; // Hãy nhớ trả về scene đã import
        }

        public void Iterate(Node node)
        {
            if (node != null)
            {
                node.Name = $"modified_{node.Name}";
                foreach (Node child in node.GetChildren())
                {
                    Iterate(child);
                }
            }
        }
    }



.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Importing 3D scenes: Configuration: Using import scripts for automation <../tutorials/assets_pipeline/importing_3d_scenes/import_configuration.html#using-import-scripts-for-automation>`__

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>` | :ref:`_post_import<class_EditorScenePostImport_private_method__post_import>`\ (\ scene\: :ref:`Node<class_Node>`\ ) |virtual| |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`get_source_file<class_EditorScenePostImport_method_get_source_file>`\ (\ ) |const|                                      |
   +-----------------------------+-------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorScenePostImport_private_method__post_import:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **_post_import**\ (\ scene\: :ref:`Node<class_Node>`\ ) |virtual| :ref:`🔗<class_EditorScenePostImport_private_method__post_import>`

Được gọi sau khi scene được import. Phương thức này phải trả về phiên bản đã sửa đổi của scene.

.. rst-class:: classref-item-separator

----

.. _class_EditorScenePostImport_method_get_source_file:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_source_file**\ (\ ) |const| :ref:`🔗<class_EditorScenePostImport_method_get_source_file>`

Trả về đường dẫn tệp nguồn đã được import (ví dụ: ``res://scene.dae``).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
