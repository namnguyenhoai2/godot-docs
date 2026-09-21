:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ConfirmationDialog.xml.

.. _class_ConfirmationDialog:

ConfirmationDialog
==================

**Kế thừa:** :ref:`AcceptDialog<class_AcceptDialog>` **<** :ref:`Window<class_Window>` **<** :ref:`Viewport<class_Viewport>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`EditorCommandPalette<class_EditorCommandPalette>`, :ref:`FileDialog<class_FileDialog>`, :ref:`ScriptCreateDialog<class_ScriptCreateDialog>`

Một dialog dùng để xác nhận các hành động.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một dialog dùng để xác nhận các hành động. Cửa sổ này tương tự như :ref:`AcceptDialog<class_AcceptDialog>`, nhưng việc nhấn nút Cancel có thể cho kết quả khác với việc nhấn nút OK. Thứ tự của hai nút này thay đổi tùy thuộc vào hệ điều hành máy chủ.

Để lấy hành động hủy, bạn có thể dùng:


.. tabs::

 .. code-tab:: gdscript

    get_cancel_button().pressed.connect(_on_canceled)

 .. code-tab:: csharp

    GetCancelButton().Pressed += OnCanceled;



\ **Lưu ý:** :ref:`AcceptDialog<class_AcceptDialog>` mặc định không hiển thị. Để làm cho nó hiển thị, hãy gọi một trong các phương thức ``popup_*`` từ :ref:`Window<class_Window>` trên node, chẳng hạn như :ref:`Window.popup_centered_clamped()<class_Window_method_popup_centered_clamped>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | :ref:`String<class_String>`     | :ref:`cancel_button_text<class_ConfirmationDialog_property_cancel_button_text>` | ``"Cancel"``                                                                    |
   +---------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | :ref:`Vector2i<class_Vector2i>` | min_size                                                                        | ``Vector2i(200, 70)`` (overrides :ref:`Window<class_Window_property_min_size>`) |
   +---------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | :ref:`Vector2i<class_Vector2i>` | size                                                                            | ``Vector2i(200, 100)`` (overrides :ref:`Window<class_Window_property_size>`)    |
   +---------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | :ref:`String<class_String>`     | title                                                                           | ``"Please Confirm..."`` (overrides :ref:`Window<class_Window_property_title>`)  |
   +---------------------------------+---------------------------------------------------------------------------------+---------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------+-----------------------------------------------------------------------------------+
   | :ref:`Button<class_Button>` | :ref:`get_cancel_button<class_ConfirmationDialog_method_get_cancel_button>`\ (\ ) |
   +-----------------------------+-----------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConfirmationDialog_property_cancel_button_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **cancel_button_text** = ``"Cancel"`` :ref:`🔗<class_ConfirmationDialog_property_cancel_button_text>`

.. rst-class:: classref-property-setget

- |void| **set_cancel_button_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_cancel_button_text**\ (\ )

Văn bản được hiển thị bởi nút Cancel (xem :ref:`get_cancel_button()<class_ConfirmationDialog_method_get_cancel_button>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ConfirmationDialog_method_get_cancel_button:

.. rst-class:: classref-method

:ref:`Button<class_Button>` **get_cancel_button**\ (\ ) :ref:`🔗<class_ConfirmationDialog_method_get_cancel_button>`

Trả về nút Cancel.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng node này có thể gây crash. Nếu bạn muốn ẩn node này hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` của chúng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
