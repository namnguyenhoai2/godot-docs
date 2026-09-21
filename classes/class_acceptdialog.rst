:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AcceptDialog.xml.

.. _class_AcceptDialog:

AcceptDialog
============

**Kế thừa:** :ref:`Window<class_Window>` **<** :ref:`Viewport<class_Viewport>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ConfirmationDialog<class_ConfirmationDialog>`

Một dialog cơ sở dùng để thông báo cho người dùng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cách sử dụng mặc định của **AcceptDialog** là chỉ cho phép chấp nhận hoặc đóng dialog, với cùng một kết quả. Tuy nhiên, các signal :ref:`confirmed<class_AcceptDialog_signal_confirmed>` và :ref:`canceled<class_AcceptDialog_signal_canceled>` cho phép làm cho hai hành động này khác nhau, còn method :ref:`add_button()<class_AcceptDialog_method_add_button>` cho phép thêm các nút và hành động tùy chỉnh.

\ **Lưu ý:** Theo mặc định, **AcceptDialog** không hiển thị. Để làm cho nó hiển thị, hãy gọi một trong các method ``popup_*`` từ :ref:`Window<class_Window>` trên node, chẳng hạn như :ref:`Window.popup_centered_clamped()<class_Window_method_popup_centered_clamped>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`dialog_autowrap<class_AcceptDialog_property_dialog_autowrap>`               | ``false``                                                                    |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`dialog_close_on_escape<class_AcceptDialog_property_dialog_close_on_escape>` | ``true``                                                                     |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | :ref:`dialog_hide_on_ok<class_AcceptDialog_property_dialog_hide_on_ok>`           | ``true``                                                                     |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`dialog_text<class_AcceptDialog_property_dialog_text>`                       | ``""``                                                                       |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | exclusive                                                                         | ``true`` (overrides :ref:`Window<class_Window_property_exclusive>`)          |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | keep_title_visible                                                                | ``true`` (overrides :ref:`Window<class_Window_property_keep_title_visible>`) |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | maximize_disabled                                                                 | ``true`` (overrides :ref:`Window<class_Window_property_maximize_disabled>`)  |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | minimize_disabled                                                                 | ``true`` (overrides :ref:`Window<class_Window_property_minimize_disabled>`)  |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`ok_button_text<class_AcceptDialog_property_ok_button_text>`                 | ``""``                                                                       |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | title                                                                             | ``"Alert!"`` (overrides :ref:`Window<class_Window_property_title>`)          |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | transient                                                                         | ``true`` (overrides :ref:`Window<class_Window_property_transient>`)          |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | visible                                                                           | ``false`` (overrides :ref:`Window<class_Window_property_visible>`)           |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | wrap_controls                                                                     | ``true`` (overrides :ref:`Window<class_Window_property_wrap_controls>`)      |
   +-----------------------------+-----------------------------------------------------------------------------------+------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Button<class_Button>` | :ref:`add_button<class_AcceptDialog_method_add_button>`\ (\ text\: :ref:`String<class_String>`, right\: :ref:`bool<class_bool>` = false, action\: :ref:`String<class_String>` = ""\ ) |
   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Button<class_Button>` | :ref:`add_cancel_button<class_AcceptDialog_method_add_cancel_button>`\ (\ name\: :ref:`String<class_String>`\ )                                                                       |
   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Label<class_Label>`   | :ref:`get_label<class_AcceptDialog_method_get_label>`\ (\ )                                                                                                                           |
   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Button<class_Button>` | :ref:`get_ok_button<class_AcceptDialog_method_get_ok_button>`\ (\ )                                                                                                                   |
   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                      | :ref:`register_text_enter<class_AcceptDialog_method_register_text_enter>`\ (\ line_edit\: :ref:`LineEdit<class_LineEdit>`\ )                                                          |
   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                      | :ref:`remove_button<class_AcceptDialog_method_remove_button>`\ (\ button\: :ref:`Button<class_Button>`\ )                                                                             |
   +-----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các thuộc tính theme
--------------------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------+--------+
   | :ref:`int<class_int>`           | :ref:`buttons_min_height<class_AcceptDialog_theme_constant_buttons_min_height>` | ``0``  |
   +---------------------------------+---------------------------------------------------------------------------------+--------+
   | :ref:`int<class_int>`           | :ref:`buttons_min_width<class_AcceptDialog_theme_constant_buttons_min_width>`   | ``0``  |
   +---------------------------------+---------------------------------------------------------------------------------+--------+
   | :ref:`int<class_int>`           | :ref:`buttons_separation<class_AcceptDialog_theme_constant_buttons_separation>` | ``10`` |
   +---------------------------------+---------------------------------------------------------------------------------+--------+
   | :ref:`StyleBox<class_StyleBox>` | :ref:`panel<class_AcceptDialog_theme_style_panel>`                              |        |
   +---------------------------------+---------------------------------------------------------------------------------+--------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_AcceptDialog_signal_canceled:

.. rst-class:: classref-signal

**canceled**\ (\ ) :ref:`🔗<class_AcceptDialog_signal_canceled>`

Được phát ra khi dialog bị đóng hoặc khi nhấn nút được tạo bằng :ref:`add_cancel_button()<class_AcceptDialog_method_add_cancel_button>`.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_signal_confirmed:

.. rst-class:: classref-signal

**confirmed**\ (\ ) :ref:`🔗<class_AcceptDialog_signal_confirmed>`

Được phát ra khi dialog được chấp nhận, tức là khi nhấn nút OK.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_signal_custom_action:

.. rst-class:: classref-signal

**custom_action**\ (\ action\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AcceptDialog_signal_custom_action>`

Được phát ra khi nhấn một nút tùy chỉnh có action. Xem :ref:`add_button()<class_AcceptDialog_method_add_button>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AcceptDialog_property_dialog_autowrap:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **dialog_autowrap** = ``false`` :ref:`🔗<class_AcceptDialog_property_dialog_autowrap>`

.. rst-class:: classref-property-setget

- |void| **set_autowrap**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_autowrap**\ (\ )

Thiết lập tự động xuống dòng cho văn bản trong dialog.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_property_dialog_close_on_escape:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **dialog_close_on_escape** = ``true`` :ref:`🔗<class_AcceptDialog_property_dialog_close_on_escape>`

.. rst-class:: classref-property-setget

- |void| **set_close_on_escape**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_close_on_escape**\ (\ )

Nếu ``true``, dialog sẽ bị ẩn khi action ``ui_close_dialog`` được nhấn (theo mặc định, action này được liên kết với :kbd:`Escape`, hoặc :kbd:`Cmd + W` trên macOS).

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_property_dialog_hide_on_ok:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **dialog_hide_on_ok** = ``true`` :ref:`🔗<class_AcceptDialog_property_dialog_hide_on_ok>`

.. rst-class:: classref-property-setget

- |void| **set_hide_on_ok**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_hide_on_ok**\ (\ )

Nếu ``true``, dialog sẽ bị ẩn khi nhấn nút OK. Bạn có thể đặt thành ``false`` nếu muốn thực hiện, chẳng hạn, việc kiểm tra tính hợp lệ của input khi nhận signal :ref:`confirmed<class_AcceptDialog_signal_confirmed>`, rồi tự xử lý việc ẩn dialog trong logic của mình.

\ **Lưu ý:** Một số node dẫn xuất từ class này có thể có giá trị mặc định khác và có thể có logic tích hợp riêng ghi đè thiết lập này. Ví dụ, :ref:`FileDialog<class_FileDialog>` mặc định là ``false`` và có mã kiểm tra input riêng được gọi khi bạn nhấn OK; mã này cuối cùng sẽ ẩn dialog nếu input hợp lệ. Vì vậy, không thể sử dụng thuộc tính này trong :ref:`FileDialog<class_FileDialog>` để tắt việc ẩn dialog khi nhấn OK.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_property_dialog_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **dialog_text** = ``""`` :ref:`🔗<class_AcceptDialog_property_dialog_text>`

.. rst-class:: classref-property-setget

- |void| **set_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_text**\ (\ )

Văn bản được hiển thị bởi dialog.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_property_ok_button_text:

.. rst-class:: classref-property

:ref:`String<class_String>` **ok_button_text** = ``""`` :ref:`🔗<class_AcceptDialog_property_ok_button_text>`

.. rst-class:: classref-property-setget

- |void| **set_ok_button_text**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_ok_button_text**\ (\ )

Văn bản được hiển thị bởi nút OK (xem :ref:`get_ok_button()<class_AcceptDialog_method_get_ok_button>`). Nếu rỗng, văn bản mặc định sẽ được sử dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_AcceptDialog_method_add_button:

.. rst-class:: classref-method

:ref:`Button<class_Button>` **add_button**\ (\ text\: :ref:`String<class_String>`, right\: :ref:`bool<class_bool>` = false, action\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_AcceptDialog_method_add_button>`

Thêm một nút có nhãn ``text`` và ``action`` tùy chỉnh vào dialog, rồi trả về nút đã tạo.

Nếu ``action`` không rỗng, việc nhấn nút sẽ phát signal :ref:`custom_action<class_AcceptDialog_signal_custom_action>` với chuỗi action được chỉ định.

Nếu ``true``, ``right`` sẽ đặt nút ở bên phải mọi nút cùng cấp.

Bạn có thể sử dụng method :ref:`remove_button()<class_AcceptDialog_method_remove_button>` để xóa một nút được tạo bằng method này khỏi dialog.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_method_add_cancel_button:

.. rst-class:: classref-method

:ref:`Button<class_Button>` **add_cancel_button**\ (\ name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AcceptDialog_method_add_cancel_button>`

Thêm một nút có nhãn ``name`` và action hủy vào dialog, rồi trả về nút đã tạo.

Bạn có thể sử dụng method :ref:`remove_button()<class_AcceptDialog_method_remove_button>` để xóa một nút được tạo bằng method này khỏi dialog.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_method_get_label:

.. rst-class:: classref-method

:ref:`Label<class_Label>` **get_label**\ (\ ) :ref:`🔗<class_AcceptDialog_method_get_label>`

Trả về nhãn được sử dụng cho văn bản tích hợp.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng node này có thể gây crash. Nếu muốn ẩn node này hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_method_get_ok_button:

.. rst-class:: classref-method

:ref:`Button<class_Button>` **get_ok_button**\ (\ ) :ref:`🔗<class_AcceptDialog_method_get_ok_button>`

Trả về instance :ref:`Button<class_Button>` OK.

\ **Cảnh báo:** Đây là node nội bộ bắt buộc; việc xóa và giải phóng node này có thể gây crash. Nếu muốn ẩn node này hoặc bất kỳ node con nào của nó, hãy sử dụng thuộc tính :ref:`CanvasItem.visible<class_CanvasItem_property_visible>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_method_register_text_enter:

.. rst-class:: classref-method

|void| **register_text_enter**\ (\ line_edit\: :ref:`LineEdit<class_LineEdit>`\ ) :ref:`🔗<class_AcceptDialog_method_register_text_enter>`

Đăng ký một :ref:`LineEdit<class_LineEdit>` trong dialog. Khi nhấn phím Enter, dialog sẽ được chấp nhận.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_method_remove_button:

.. rst-class:: classref-method

|void| **remove_button**\ (\ button\: :ref:`Button<class_Button>`\ ) :ref:`🔗<class_AcceptDialog_method_remove_button>`

Xóa ``button`` khỏi dialog. Không giải phóng ``button``. ``button`` phải là một :ref:`Button<class_Button>` được thêm bằng method :ref:`add_button()<class_AcceptDialog_method_add_button>` hoặc :ref:`add_cancel_button()<class_AcceptDialog_method_add_cancel_button>`. Sau khi xóa, việc nhấn ``button`` sẽ không còn phát các signal :ref:`custom_action<class_AcceptDialog_signal_custom_action>` hoặc :ref:`canceled<class_AcceptDialog_signal_canceled>` của dialog này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính theme
----------------------

.. _class_AcceptDialog_theme_constant_buttons_min_height:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **buttons_min_height** = ``0`` :ref:`🔗<class_AcceptDialog_theme_constant_buttons_min_height>`

Chiều cao tối thiểu tính bằng pixel của mỗi nút trong hàng dưới cùng (chẳng hạn như OK/Cancel). Có thể tăng giá trị này để các nút có văn bản ngắn dễ nhấp/chạm hơn.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_theme_constant_buttons_min_width:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **buttons_min_width** = ``0`` :ref:`🔗<class_AcceptDialog_theme_constant_buttons_min_width>`

Chiều rộng tối thiểu tính bằng pixel của mỗi nút trong hàng dưới cùng (chẳng hạn như OK/Cancel). Có thể tăng giá trị này để các nút có văn bản ngắn dễ nhấp/chạm hơn.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_theme_constant_buttons_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **buttons_separation** = ``10`` :ref:`🔗<class_AcceptDialog_theme_constant_buttons_separation>`

Kích thước của khoảng trống theo chiều dọc giữa nội dung của dialog và hàng nút.

.. rst-class:: classref-item-separator

----

.. _class_AcceptDialog_theme_style_panel:

.. rst-class:: classref-themeproperty

:ref:`StyleBox<class_StyleBox>` **panel** :ref:`🔗<class_AcceptDialog_theme_style_panel>`

Panel lấp đầy nền của cửa sổ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
