:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FileSystemDock.xml.

.. _class_FileSystemDock:

FileSystemDock
==============

**Kế thừa:** :ref:`EditorDock<class_EditorDock>` **<** :ref:`MarginContainer<class_MarginContainer>` **<** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Dock của trình chỉnh sửa Godot dùng để quản lý các tệp trong project.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class này chỉ khả dụng trong :ref:`EditorPlugin<class_EditorPlugin>`\ s và không thể được khởi tạo. Bạn có thể truy cập nó bằng :ref:`EditorInterface.get_file_system_dock()<class_EditorInterface_method_get_file_system_dock>`.

Mặc dù **FileSystemDock** không cung cấp bất kỳ method nào để thao tác với tệp, nó có thể lắng nghe nhiều signal liên quan đến tệp.

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_resource_tooltip_plugin<class_FileSystemDock_method_add_resource_tooltip_plugin>`\ (\ plugin\: :ref:`EditorResourceTooltipPlugin<class_EditorResourceTooltipPlugin>`\ )       |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`navigate_to_path<class_FileSystemDock_method_navigate_to_path>`\ (\ path\: :ref:`String<class_String>`\ )                                                                         |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`remove_resource_tooltip_plugin<class_FileSystemDock_method_remove_resource_tooltip_plugin>`\ (\ plugin\: :ref:`EditorResourceTooltipPlugin<class_EditorResourceTooltipPlugin>`\ ) |
   +--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_FileSystemDock_signal_display_mode_changed:

.. rst-class:: classref-signal

**display_mode_changed**\ (\ ) :ref:`🔗<class_FileSystemDock_signal_display_mode_changed>`

Được phát khi người dùng chuyển đổi chế độ hiển thị tệp hoặc chế độ chia đôi.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_file_removed:

.. rst-class:: classref-signal

**file_removed**\ (\ file\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileSystemDock_signal_file_removed>`

Được phát khi ``file`` đã cho bị xóa.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_files_moved:

.. rst-class:: classref-signal

**files_moved**\ (\ old_file\: :ref:`String<class_String>`, new_file\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileSystemDock_signal_files_moved>`

Được phát khi một tệp được di chuyển từ đường dẫn ``old_file`` sang đường dẫn ``new_file``.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_folder_color_changed:

.. rst-class:: classref-signal

**folder_color_changed**\ (\ ) :ref:`🔗<class_FileSystemDock_signal_folder_color_changed>`

Được phát khi màu của các thư mục thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_folder_moved:

.. rst-class:: classref-signal

**folder_moved**\ (\ old_folder\: :ref:`String<class_String>`, new_folder\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileSystemDock_signal_folder_moved>`

Được phát khi một thư mục được di chuyển từ đường dẫn ``old_folder`` sang đường dẫn ``new_folder``.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_folder_removed:

.. rst-class:: classref-signal

**folder_removed**\ (\ folder\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileSystemDock_signal_folder_removed>`

Được phát khi ``folder`` đã cho bị xóa.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_inherit:

.. rst-class:: classref-signal

**inherit**\ (\ file\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileSystemDock_signal_inherit>`

Được phát khi một scene mới được tạo và kế thừa scene tại đường dẫn ``file``.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_instantiate:

.. rst-class:: classref-signal

**instantiate**\ (\ files\: :ref:`PackedStringArray<class_PackedStringArray>`\ ) :ref:`🔗<class_FileSystemDock_signal_instantiate>`

Được phát khi các scene đã cho đang được instantiate trong trình chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_resource_removed:

.. rst-class:: classref-signal

**resource_removed**\ (\ resource\: :ref:`Resource<class_Resource>`\ ) :ref:`🔗<class_FileSystemDock_signal_resource_removed>`

Được phát khi một ``resource`` bên ngoài bị xóa tệp.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_signal_selection_changed:

.. rst-class:: classref-signal

**selection_changed**\ (\ ) :ref:`🔗<class_FileSystemDock_signal_selection_changed>`

Được phát khi lựa chọn thay đổi. Sử dụng :ref:`EditorInterface.get_selected_paths()<class_EditorInterface_method_get_selected_paths>` trong method được kết nối để lấy các đường dẫn đã chọn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_FileSystemDock_method_add_resource_tooltip_plugin:

.. rst-class:: classref-method

|void| **add_resource_tooltip_plugin**\ (\ plugin\: :ref:`EditorResourceTooltipPlugin<class_EditorResourceTooltipPlugin>`\ ) :ref:`🔗<class_FileSystemDock_method_add_resource_tooltip_plugin>`

Đăng ký một :ref:`EditorResourceTooltipPlugin<class_EditorResourceTooltipPlugin>` mới.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_method_navigate_to_path:

.. rst-class:: classref-method

|void| **navigate_to_path**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_FileSystemDock_method_navigate_to_path>`

Đặt ``path`` đã cho làm mục hiện được chọn, đồng thời đảm bảo tệp/thư mục được chọn hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_FileSystemDock_method_remove_resource_tooltip_plugin:

.. rst-class:: classref-method

|void| **remove_resource_tooltip_plugin**\ (\ plugin\: :ref:`EditorResourceTooltipPlugin<class_EditorResourceTooltipPlugin>`\ ) :ref:`🔗<class_FileSystemDock_method_remove_resource_tooltip_plugin>`

Xóa một :ref:`EditorResourceTooltipPlugin<class_EditorResourceTooltipPlugin>`. Thao tác sẽ thất bại nếu plugin chưa từng được thêm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
