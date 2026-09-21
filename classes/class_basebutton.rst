:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/BaseButton.xml.

.. _class_BaseButton:

BaseButton
==========

**Kế thừa:** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`Button<class_Button>`, :ref:`LinkButton<class_LinkButton>`, :ref:`TextureButton<class_TextureButton>`

Lớp cơ sở trừu tượng cho các nút GUI.

.. rst-class:: classref-introduction-group

Mô tả
-----

**BaseButton** là một lớp cơ sở trừu tượng cho các nút GUI. Bản thân nó không hiển thị bất kỳ thứ gì.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`ActionMode<enum_BaseButton_ActionMode>`                           | :ref:`action_mode<class_BaseButton_property_action_mode>`                   | ``1``                                                               |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`ButtonGroup<class_ButtonGroup>`                                   | :ref:`button_group<class_BaseButton_property_button_group>`                 |                                                                     |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | |bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\] | :ref:`button_mask<class_BaseButton_property_button_mask>`                   | ``1``                                                               |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`button_pressed<class_BaseButton_property_button_pressed>`             | ``false``                                                           |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`disabled<class_BaseButton_property_disabled>`                         | ``false``                                                           |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>`                                | focus_mode                                                                  | ``2`` (overrides :ref:`Control<class_Control_property_focus_mode>`) |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`keep_pressed_outside<class_BaseButton_property_keep_pressed_outside>` | ``false``                                                           |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`Shortcut<class_Shortcut>`                                         | :ref:`shortcut<class_BaseButton_property_shortcut>`                         |                                                                     |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`shortcut_feedback<class_BaseButton_property_shortcut_feedback>`       | ``true``                                                            |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`shortcut_in_tooltip<class_BaseButton_property_shortcut_in_tooltip>`   | ``true``                                                            |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`toggle_mode<class_BaseButton_property_toggle_mode>`                   | ``false``                                                           |
   +-------------------------------------------------------------------------+-----------------------------------------------------------------------------+---------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`_pressed<class_BaseButton_private_method__pressed>`\ (\ ) |virtual|                                            |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`_toggled<class_BaseButton_private_method__toggled>`\ (\ toggled_on\: :ref:`bool<class_bool>`\ ) |virtual|      |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | :ref:`DrawMode<enum_BaseButton_DrawMode>` | :ref:`get_draw_mode<class_BaseButton_method_get_draw_mode>`\ (\ ) |const|                                            |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                   | :ref:`is_hovered<class_BaseButton_method_is_hovered>`\ (\ ) |const|                                                  |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`set_pressed_no_signal<class_BaseButton_method_set_pressed_no_signal>`\ (\ pressed\: :ref:`bool<class_bool>`\ ) |
   +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_BaseButton_signal_button_down:

.. rst-class:: classref-signal

**button_down**\ (\ ) :ref:`🔗<class_BaseButton_signal_button_down>`

Được phát ra khi nút bắt đầu được nhấn giữ.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_signal_button_up:

.. rst-class:: classref-signal

**button_up**\ (\ ) :ref:`🔗<class_BaseButton_signal_button_up>`

Được phát ra khi nút ngừng được nhấn giữ.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_signal_pressed:

.. rst-class:: classref-signal

**pressed**\ (\ ) :ref:`🔗<class_BaseButton_signal_pressed>`

Được phát ra khi nút được chuyển trạng thái hoặc được nhấn. Tín hiệu này ở :ref:`button_down<class_BaseButton_signal_button_down>` nếu :ref:`action_mode<class_BaseButton_property_action_mode>` là :ref:`ACTION_MODE_BUTTON_PRESS<class_BaseButton_constant_ACTION_MODE_BUTTON_PRESS>` và ở :ref:`button_up<class_BaseButton_signal_button_up>` trong các trường hợp khác.

Nếu bạn cần biết trạng thái được nhấn của nút (và :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` đang hoạt động), hãy sử dụng :ref:`toggled<class_BaseButton_signal_toggled>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_signal_toggled:

.. rst-class:: classref-signal

**toggled**\ (\ toggled_on\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_BaseButton_signal_toggled>`

Được phát ra khi nút vừa được chuyển đổi giữa trạng thái được nhấn và trạng thái bình thường (chỉ khi :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` đang hoạt động). Trạng thái mới được chứa trong đối số ``toggled_on``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_BaseButton_DrawMode:

.. rst-class:: classref-enumeration

enum **DrawMode**: :ref:`🔗<enum_BaseButton_DrawMode>`

.. _class_BaseButton_constant_DRAW_NORMAL:

.. rst-class:: classref-enumeration-constant

:ref:`DrawMode<enum_BaseButton_DrawMode>` **DRAW_NORMAL** = ``0``

Trạng thái bình thường của các nút (tức là không được nhấn, không được di chuột qua, không được chuyển trạng thái và đang bật).

.. _class_BaseButton_constant_DRAW_PRESSED:

.. rst-class:: classref-enumeration-constant

:ref:`DrawMode<enum_BaseButton_DrawMode>` **DRAW_PRESSED** = ``1``

Trạng thái các nút được nhấn.

.. _class_BaseButton_constant_DRAW_HOVER:

.. rst-class:: classref-enumeration-constant

:ref:`DrawMode<enum_BaseButton_DrawMode>` **DRAW_HOVER** = ``2``

Trạng thái các nút được di chuột qua.

.. _class_BaseButton_constant_DRAW_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`DrawMode<enum_BaseButton_DrawMode>` **DRAW_DISABLED** = ``3``

Trạng thái các nút bị vô hiệu hóa.

.. _class_BaseButton_constant_DRAW_HOVER_PRESSED:

.. rst-class:: classref-enumeration-constant

:ref:`DrawMode<enum_BaseButton_DrawMode>` **DRAW_HOVER_PRESSED** = ``4``

Trạng thái các nút vừa được di chuột qua vừa được nhấn.

.. rst-class:: classref-item-separator

----

.. _enum_BaseButton_ActionMode:

.. rst-class:: classref-enumeration

enum **ActionMode**: :ref:`🔗<enum_BaseButton_ActionMode>`

.. _class_BaseButton_constant_ACTION_MODE_BUTTON_PRESS:

.. rst-class:: classref-enumeration-constant

:ref:`ActionMode<enum_BaseButton_ActionMode>` **ACTION_MODE_BUTTON_PRESS** = ``0``

Chỉ cần nhấn một lần để nút được xem là đã nhấp.

.. _class_BaseButton_constant_ACTION_MODE_BUTTON_RELEASE:

.. rst-class:: classref-enumeration-constant

:ref:`ActionMode<enum_BaseButton_ActionMode>` **ACTION_MODE_BUTTON_RELEASE** = ``1``

Yêu cầu nhấn và sau đó nhả ra trước khi nút được xem là đã nhấp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BaseButton_property_action_mode:

.. rst-class:: classref-property

:ref:`ActionMode<enum_BaseButton_ActionMode>` **action_mode** = ``1`` :ref:`🔗<class_BaseButton_property_action_mode>`

.. rst-class:: classref-property-setget

- |void| **set_action_mode**\ (\ value\: :ref:`ActionMode<enum_BaseButton_ActionMode>`\ ) - :ref:`ActionMode<enum_BaseButton_ActionMode>` **get_action_mode**\ (\ )

Xác định thời điểm nút được xem là đã nhấp.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_button_group:

.. rst-class:: classref-property

:ref:`ButtonGroup<class_ButtonGroup>` **button_group** :ref:`🔗<class_BaseButton_property_button_group>`

.. rst-class:: classref-property-setget

- |void| **set_button_group**\ (\ value\: :ref:`ButtonGroup<class_ButtonGroup>`\ ) - :ref:`ButtonGroup<class_ButtonGroup>` **get_button_group**\ (\ )

:ref:`ButtonGroup<class_ButtonGroup>` được liên kết với nút. Không được nhầm lẫn với các node group.

\ **Lưu ý:** Nút sẽ được cấu hình thành radio button nếu một :ref:`ButtonGroup<class_ButtonGroup>` được gán cho nó.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_button_mask:

.. rst-class:: classref-property

|bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\] **button_mask** = ``1`` :ref:`🔗<class_BaseButton_property_button_mask>`

.. rst-class:: classref-property-setget

- |void| **set_button_mask**\ (\ value\: |bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\]\ ) - |bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\] **get_button_mask**\ (\ )

Mặt nạ nhị phân để chọn các nút chuột mà nút này sẽ phản hồi.

Để cho phép cả nhấp chuột trái và nhấp chuột phải, hãy sử dụng ``MOUSE_BUTTON_MASK_LEFT | MOUSE_BUTTON_MASK_RIGHT``.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_button_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **button_pressed** = ``false`` :ref:`🔗<class_BaseButton_property_button_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pressed**\ (\ )

Nếu ``true``, trạng thái của nút là được nhấn. Điều này có nghĩa là nút đang được nhấn hoặc đã được chuyển trạng thái (nếu :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` đang hoạt động). Chỉ hoạt động khi :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` là ``true``.

\ **Lưu ý:** Thay đổi giá trị của :ref:`button_pressed<class_BaseButton_property_button_pressed>` sẽ khiến :ref:`toggled<class_BaseButton_signal_toggled>` được phát ra. Nếu bạn muốn thay đổi trạng thái được nhấn mà không phát ra tín hiệu đó, hãy sử dụng :ref:`set_pressed_no_signal()<class_BaseButton_method_set_pressed_no_signal>`.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_disabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disabled** = ``false`` :ref:`🔗<class_BaseButton_property_disabled>`

.. rst-class:: classref-property-setget

- |void| **set_disabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_disabled**\ (\ )

Nếu ``true``, nút ở trạng thái bị vô hiệu hóa và không thể được nhấp hoặc chuyển trạng thái.

\ **Lưu ý:** Nếu nút bị vô hiệu hóa trong khi đang được nhấn giữ, :ref:`button_up<class_BaseButton_signal_button_up>` sẽ được phát ra.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_keep_pressed_outside:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **keep_pressed_outside** = ``false`` :ref:`🔗<class_BaseButton_property_keep_pressed_outside>`

.. rst-class:: classref-property-setget

- |void| **set_keep_pressed_outside**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_keep_pressed_outside**\ (\ )

Nếu ``true``, nút vẫn ở trạng thái được nhấn khi di chuyển con trỏ ra ngoài nút trong lúc nhấn nút.

\ **Lưu ý:** Thuộc tính này chỉ ảnh hưởng đến giao diện trực quan của nút. Các tín hiệu sẽ được phát ra cùng một thời điểm bất kể giá trị của thuộc tính này.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_shortcut:

.. rst-class:: classref-property

:ref:`Shortcut<class_Shortcut>` **shortcut** :ref:`🔗<class_BaseButton_property_shortcut>`

.. rst-class:: classref-property-setget

- |void| **set_shortcut**\ (\ value\: :ref:`Shortcut<class_Shortcut>`\ ) - :ref:`Shortcut<class_Shortcut>` **get_shortcut**\ (\ )

:ref:`Shortcut<class_Shortcut>` associated to the button.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_shortcut_feedback:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shortcut_feedback** = ``true`` :ref:`🔗<class_BaseButton_property_shortcut_feedback>`

.. rst-class:: classref-property-setget

- |void| **set_shortcut_feedback**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_shortcut_feedback**\ (\ )

Nếu ``true``, nút sẽ được làm nổi bật trong một khoảng thời gian ngắn khi shortcut của nó được kích hoạt. Nếu ``false`` và :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` là ``false``, shortcut sẽ được kích hoạt mà không có phản hồi trực quan nào.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_shortcut_in_tooltip:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shortcut_in_tooltip** = ``true`` :ref:`🔗<class_BaseButton_property_shortcut_in_tooltip>`

.. rst-class:: classref-property-setget

- |void| **set_shortcut_in_tooltip**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_shortcut_in_tooltip_enabled**\ (\ )

Nếu ``true``, nút sẽ thêm thông tin về shortcut của nó vào tooltip. Thông tin này bao gồm các event của shortcut và :ref:`Resource.resource_name<class_Resource_property_resource_name>` của nó. Nếu cả các event và tên đều trống, shortcut sẽ không được đưa vào.

\ **Lưu ý:** Thuộc tính này không có tác dụng khi control tooltip được tùy chỉnh bằng :ref:`Control._make_custom_tooltip()<class_Control_private_method__make_custom_tooltip>`.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_property_toggle_mode:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **toggle_mode** = ``false`` :ref:`🔗<class_BaseButton_property_toggle_mode>`

.. rst-class:: classref-property-setget

- |void| **set_toggle_mode**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_toggle_mode**\ (\ )

Nếu ``true``, nút ở chế độ toggle. Khiến nút chuyển đổi giữa trạng thái được nhấn và không được nhấn mỗi khi vùng của nó được nhấp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_BaseButton_private_method__pressed:

.. rst-class:: classref-method

|void| **_pressed**\ (\ ) |virtual| :ref:`🔗<class_BaseButton_private_method__pressed>`

Được gọi khi nút được nhấn. Nếu bạn cần biết trạng thái được nhấn của nút (và :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` đang hoạt động), hãy sử dụng :ref:`_toggled()<class_BaseButton_private_method__toggled>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_private_method__toggled:

.. rst-class:: classref-method

|void| **_toggled**\ (\ toggled_on\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_BaseButton_private_method__toggled>`

Được gọi khi nút được chuyển trạng thái (chỉ khi :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` đang hoạt động).

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_method_get_draw_mode:

.. rst-class:: classref-method

:ref:`DrawMode<enum_BaseButton_DrawMode>` **get_draw_mode**\ (\ ) |const| :ref:`🔗<class_BaseButton_method_get_draw_mode>`

Trả về trạng thái trực quan được dùng để vẽ nút. Điều này chủ yếu hữu ích khi triển khai mã vẽ của riêng bạn bằng cách ghi đè _draw() hoặc kết nối với tín hiệu "draw". Trạng thái trực quan của nút được xác định bởi enum :ref:`DrawMode<enum_BaseButton_DrawMode>`.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_method_is_hovered:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_hovered**\ (\ ) |const| :ref:`🔗<class_BaseButton_method_is_hovered>`

Trả về ``true`` nếu chuột đã đi vào nút và chưa rời khỏi nút.

.. rst-class:: classref-item-separator

----

.. _class_BaseButton_method_set_pressed_no_signal:

.. rst-class:: classref-method

|void| **set_pressed_no_signal**\ (\ pressed\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_BaseButton_method_set_pressed_no_signal>`

Thay đổi trạng thái :ref:`button_pressed<class_BaseButton_property_button_pressed>` của nút mà không phát ra :ref:`toggled<class_BaseButton_signal_toggled>`. Sử dụng khi bạn chỉ muốn thay đổi trạng thái của nút mà không gửi sự kiện pressed (ví dụ: khi khởi tạo scene). Chỉ hoạt động khi :ref:`toggle_mode<class_BaseButton_property_toggle_mode>` là ``true``.

\ **Lưu ý:** Phương thức này không bỏ nhấn các nút khác trong :ref:`button_group<class_BaseButton_property_button_group>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
