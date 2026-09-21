:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorFileDialog.xml.

.. _class_EditorFileDialog:

EditorFileDialog
================

**Kế thừa:** :ref:`FileDialog<class_FileDialog>` **<** :ref:`ConfirmationDialog<class_ConfirmationDialog>` **<** :ref:`AcceptDialog<class_AcceptDialog>` **<** :ref:`Window<class_Window>` **<** :ref:`Viewport<class_Viewport>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một phiên bản đã được sửa đổi của :ref:`FileDialog<class_FileDialog>` được editor sử dụng.

.. rst-class:: classref-introduction-group

Mô tả
-----

**EditorFileDialog** là một :ref:`FileDialog<class_FileDialog>` được tinh chỉnh để hoạt động trong editor. Nó tự động xử lý các danh sách thư mục yêu thích và thư mục gần đây, đồng thời đồng bộ một số thuộc tính với các editor setting tương ứng.

\ **EditorFileDialog** sẽ tự động hiển thị một native dialog dựa trên editor setting :ref:`EditorSettings.interface/editor/appearance/use_native_file_dialogs<class_EditorSettings_property_interface/editor/appearance/use_native_file_dialogs>` và bỏ qua :ref:`FileDialog.use_native_dialog<class_FileDialog_property_use_native_dialog>`.

\ **Lưu ý:** Theo mặc định, **EditorFileDialog** không hiển thị. Để hiển thị nó, hãy gọi một trong các phương thức ``popup_*`` từ :ref:`Window<class_Window>` trên node, chẳng hạn như :ref:`Window.popup_centered_clamped()<class_Window_method_popup_centered_clamped>`.

\ **Lưu ý:** Trên Linux và macOS, các ứng dụng sandbox luôn sử dụng native dialog để truy cập hệ thống tệp của host.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`disable_overwrite_warning<class_EditorFileDialog_property_disable_overwrite_warning>` | ``false`` |
   +-------------------------+---------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`add_side_menu<class_EditorFileDialog_method_add_side_menu>`\ (\ menu\: :ref:`Control<class_Control>`, title\: :ref:`String<class_String>` = ""\ ) |
   +--------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorFileDialog_property_disable_overwrite_warning:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disable_overwrite_warning** = ``false`` :ref:`🔗<class_EditorFileDialog_property_disable_overwrite_warning>`

.. rst-class:: classref-property-setget

- |void| **set_disable_overwrite_warning**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_overwrite_warning_disabled**\ (\ )

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`FileDialog.overwrite_warning_enabled<class_FileDialog_property_overwrite_warning_enabled>`.

Nếu ``true``, **EditorFileDialog** sẽ không cảnh báo người dùng trước khi ghi đè tệp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorFileDialog_method_add_side_menu:

.. rst-class:: classref-method

|void| **add_side_menu**\ (\ menu\: :ref:`Control<class_Control>`, title\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_EditorFileDialog_method_add_side_menu>`

**Đã lỗi thời:** Tính năng này không còn được hỗ trợ.

Phương thức này được giữ lại để tương thích và không thực hiện thao tác nào. Thay vào đó, bạn có thể hiển thị một dialog khác sau khi hiển thị file dialog.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
