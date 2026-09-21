:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/EditorProperty.xml.

.. _class_EditorProperty:

EditorProperty
==============

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Control tùy chỉnh để chỉnh sửa các thuộc tính có thể được thêm vào :ref:`EditorInspector<class_EditorInspector>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Control tùy chỉnh để chỉnh sửa các thuộc tính có thể được thêm vào :ref:`EditorInspector<class_EditorInspector>`. Được thêm vào thông qua :ref:`EditorInspectorPlugin<class_EditorInspectorPlugin>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`checkable<class_EditorProperty_property_checkable>`               | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`checked<class_EditorProperty_property_checked>`                   | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`deletable<class_EditorProperty_property_deletable>`               | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`draw_background<class_EditorProperty_property_draw_background>`   | ``true``                                                            |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`draw_label<class_EditorProperty_property_draw_label>`             | ``true``                                                            |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`draw_warning<class_EditorProperty_property_draw_warning>`         | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`FocusMode<enum_Control_FocusMode>` | focus_mode                                                              | ``3`` (overrides :ref:`Control<class_Control_property_focus_mode>`) |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`keying<class_EditorProperty_property_keying>`                     | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`String<class_String>`              | :ref:`label<class_EditorProperty_property_label>`                       | ``""``                                                              |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`float<class_float>`                | :ref:`name_split_ratio<class_EditorProperty_property_name_split_ratio>` | ``0.5``                                                             |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`read_only<class_EditorProperty_property_read_only>`               | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`selectable<class_EditorProperty_property_selectable>`             | ``true``                                                            |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                  | :ref:`use_folding<class_EditorProperty_property_use_folding>`           | ``false``                                                           |
   +------------------------------------------+-------------------------------------------------------------------------+---------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`_set_read_only<class_EditorProperty_private_method__set_read_only>`\ (\ read_only\: :ref:`bool<class_bool>`\ ) |virtual|                                                                                                                            |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`_update_property<class_EditorProperty_private_method__update_property>`\ (\ ) |virtual|                                                                                                                                                             |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`add_focusable<class_EditorProperty_method_add_focusable>`\ (\ control\: :ref:`Control<class_Control>`\ )                                                                                                                                            |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`deselect<class_EditorProperty_method_deselect>`\ (\ )                                                                                                                                                                                               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`emit_changed<class_EditorProperty_method_emit_changed>`\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`, field\: :ref:`StringName<class_StringName>` = &"", changing\: :ref:`bool<class_bool>` = false\ ) |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`         | :ref:`get_edited_object<class_EditorProperty_method_get_edited_object>`\ (\ )                                                                                                                                                                             |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_edited_property<class_EditorProperty_method_get_edited_property>`\ (\ ) |const|                                                                                                                                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_selected<class_EditorProperty_method_is_selected>`\ (\ ) |const|                                                                                                                                                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`select<class_EditorProperty_method_select>`\ (\ focusable\: :ref:`int<class_int>` = -1\ )                                                                                                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_bottom_editor<class_EditorProperty_method_set_bottom_editor>`\ (\ editor\: :ref:`Control<class_Control>`\ )                                                                                                                                     |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_label_reference<class_EditorProperty_method_set_label_reference>`\ (\ control\: :ref:`Control<class_Control>`\ )                                                                                                                                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_object_and_property<class_EditorProperty_method_set_object_and_property>`\ (\ object\: :ref:`Object<class_Object>`, property\: :ref:`StringName<class_StringName>`\ )                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`update_property<class_EditorProperty_method_update_property>`\ (\ )                                                                                                                                                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_EditorProperty_signal_multiple_properties_changed:

.. rst-class:: classref-signal

**multiple_properties_changed**\ (\ properties\: :ref:`PackedStringArray<class_PackedStringArray>`, value\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_EditorProperty_signal_multiple_properties_changed>`

Phát signal này nếu bạn muốn sửa đổi nhiều thuộc tính cùng lúc. Không sử dụng nếu được thêm thông qua :ref:`EditorInspectorPlugin._parse_property()<class_EditorInspectorPlugin_private_method__parse_property>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_object_id_selected:

.. rst-class:: classref-signal

**object_id_selected**\ (\ property\: :ref:`StringName<class_StringName>`, id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EditorProperty_signal_object_id_selected>`

Được các sub-inspector sử dụng. Phát signal này nếu đối tượng được chọn là Object ID.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_can_revert_changed:

.. rst-class:: classref-signal

**property_can_revert_changed**\ (\ property\: :ref:`StringName<class_StringName>`, can_revert\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorProperty_signal_property_can_revert_changed>`

Được phát khi khả năng hoàn nguyên (tức là liệu thuộc tính có giá trị khác mặc định và do đó được hiển thị bằng biểu tượng hoàn nguyên hay không) của một thuộc tính thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_changed:

.. rst-class:: classref-signal

**property_changed**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`, field\: :ref:`StringName<class_StringName>`, changing\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorProperty_signal_property_changed>`

Không phát signal này theo cách thủ công, hãy sử dụng phương thức :ref:`emit_changed()<class_EditorProperty_method_emit_changed>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_checked:

.. rst-class:: classref-signal

**property_checked**\ (\ property\: :ref:`StringName<class_StringName>`, checked\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorProperty_signal_property_checked>`

Được phát khi một thuộc tính được đánh dấu. Được sử dụng nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_deleted:

.. rst-class:: classref-signal

**property_deleted**\ (\ property\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EditorProperty_signal_property_deleted>`

Được phát khi một thuộc tính bị xóa. Được sử dụng nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_favorited:

.. rst-class:: classref-signal

**property_favorited**\ (\ property\: :ref:`StringName<class_StringName>`, favorited\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorProperty_signal_property_favorited>`

Phát signal này nếu bạn muốn đánh dấu một thuộc tính là yêu thích, khiến thuộc tính đó xuất hiện ở đầu inspector.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_keyed:

.. rst-class:: classref-signal

**property_keyed**\ (\ property\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EditorProperty_signal_property_keyed>`

Phát signal này nếu bạn muốn thêm giá trị này dưới dạng key animation (trước tiên hãy kiểm tra xem việc tạo key đã được bật hay chưa).

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_keyed_with_value:

.. rst-class:: classref-signal

**property_keyed_with_value**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_EditorProperty_signal_property_keyed_with_value>`

Phát signal này nếu bạn muốn tạo key cho một thuộc tính bằng một giá trị duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_overridden:

.. rst-class:: classref-signal

**property_overridden**\ (\ ) :ref:`🔗<class_EditorProperty_signal_property_overridden>`

Được phát khi có yêu cầu ghi đè một thiết lập cho project hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_property_pinned:

.. rst-class:: classref-signal

**property_pinned**\ (\ property\: :ref:`StringName<class_StringName>`, pinned\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_EditorProperty_signal_property_pinned>`

Phát signal này nếu bạn muốn đánh dấu (hoặc bỏ đánh dấu) giá trị của một thuộc tính để luôn được lưu, bất kể có bằng giá trị mặc định hay không.

Giá trị mặc định là giá trị mà thuộc tính sẽ nhận khi node vừa được khởi tạo và có thể đến từ một scene tổ tiên trong chuỗi kế thừa/khởi tạo, một script hoặc một class builtin.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_resource_selected:

.. rst-class:: classref-signal

**resource_selected**\ (\ path\: :ref:`String<class_String>`, resource\: :ref:`Resource<class_Resource>`\ ) :ref:`🔗<class_EditorProperty_signal_resource_selected>`

Nếu bạn muốn chỉnh sửa một sub-resource, hãy phát signal này cùng với resource đó.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_signal_selected:

.. rst-class:: classref-signal

**selected**\ (\ path\: :ref:`String<class_String>`, focusable_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_EditorProperty_signal_selected>`

Được phát khi được chọn. Được sử dụng nội bộ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_EditorProperty_property_checkable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **checkable** = ``false`` :ref:`🔗<class_EditorProperty_property_checkable>`

.. rst-class:: classref-property-setget

- |void| **set_checkable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_checkable**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính có thể được đánh dấu.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_checked:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **checked** = ``false`` :ref:`🔗<class_EditorProperty_property_checked>`

.. rst-class:: classref-property-setget

- |void| **set_checked**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_checked**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính được đánh dấu.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_deletable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **deletable** = ``false`` :ref:`🔗<class_EditorProperty_property_deletable>`

.. rst-class:: classref-property-setget

- |void| **set_deletable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_deletable**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi người dùng có thể xóa thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_draw_background:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **draw_background** = ``true`` :ref:`🔗<class_EditorProperty_property_draw_background>`

.. rst-class:: classref-property-setget

- |void| **set_draw_background**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_draw_background**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi nền của thuộc tính được vẽ.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_draw_label:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **draw_label** = ``true`` :ref:`🔗<class_EditorProperty_property_draw_label>`

.. rst-class:: classref-property-setget

- |void| **set_draw_label**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_draw_label**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi nhãn của thuộc tính được vẽ.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_draw_warning:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **draw_warning** = ``false`` :ref:`🔗<class_EditorProperty_property_draw_warning>`

.. rst-class:: classref-property-setget

- |void| **set_draw_warning**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_draw_warning**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính được vẽ bằng màu cảnh báo của editor theme. Tùy chọn này được sử dụng cho các thuộc tính của các node con có thể chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_keying:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **keying** = ``false`` :ref:`🔗<class_EditorProperty_property_keying>`

.. rst-class:: classref-property-setget

- |void| **set_keying**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_keying**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính có thể thêm key cho animation.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_label:

.. rst-class:: classref-property

:ref:`String<class_String>` **label** = ``""`` :ref:`🔗<class_EditorProperty_property_label>`

.. rst-class:: classref-property-setget

- |void| **set_label**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_label**\ (\ )

Đặt thuộc tính này để thay đổi nhãn (nếu bạn muốn hiển thị nhãn).

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_name_split_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **name_split_ratio** = ``0.5`` :ref:`🔗<class_EditorProperty_property_name_split_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_name_split_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_name_split_ratio**\ (\ )

Tỷ lệ phân bổ không gian giữa nhãn và trường chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_read_only:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **read_only** = ``false`` :ref:`🔗<class_EditorProperty_property_read_only>`

.. rst-class:: classref-property-setget

- |void| **set_read_only**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_read_only**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính ở chế độ chỉ đọc.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_selectable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **selectable** = ``true`` :ref:`🔗<class_EditorProperty_property_selectable>`

.. rst-class:: classref-property-setget

- |void| **set_selectable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_selectable**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính có thể được chọn.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_property_use_folding:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_folding** = ``false`` :ref:`🔗<class_EditorProperty_property_use_folding>`

.. rst-class:: classref-property-setget

- |void| **set_use_folding**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_folding**\ (\ )

Được inspector sử dụng, đặt thành ``true`` khi thuộc tính đang sử dụng folding.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_EditorProperty_private_method__set_read_only:

.. rst-class:: classref-method

|void| **_set_read_only**\ (\ read_only\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_EditorProperty_private_method__set_read_only>`

Được gọi khi trạng thái chỉ đọc của thuộc tính thay đổi. Có thể sử dụng để chuyển các control tùy chỉnh sang trạng thái chỉ đọc hoặc có thể sửa đổi.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_private_method__update_property:

.. rst-class:: classref-method

|void| **_update_property**\ (\ ) |virtual| :ref:`🔗<class_EditorProperty_private_method__update_property>`

Khi virtual function này được gọi, bạn phải cập nhật editor.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_add_focusable:

.. rst-class:: classref-method

|void| **add_focusable**\ (\ control\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_EditorProperty_method_add_focusable>`

Nếu bất kỳ control nào được thêm có thể nhận keyboard focus, hãy thêm nó vào đây. Điều này đảm bảo focus sẽ được khôi phục nếu inspector được làm mới.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_deselect:

.. rst-class:: classref-method

|void| **deselect**\ (\ ) :ref:`🔗<class_EditorProperty_method_deselect>`

Vẽ thuộc tính ở trạng thái không được chọn. Được inspector sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_emit_changed:

.. rst-class:: classref-method

|void| **emit_changed**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`, field\: :ref:`StringName<class_StringName>` = &"", changing\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_EditorProperty_method_emit_changed>`

Nếu một hoặc nhiều thuộc tính đã thay đổi, phải gọi phương thức này. ``field`` được sử dụng trong trường hợp editor của bạn có thể sửa đổi riêng từng field (ví dụ: Vector3.x). Đối số ``changing`` ngăn editor yêu cầu làm mới thuộc tính này (để là ``false`` nếu không chắc chắn).

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_get_edited_object:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **get_edited_object**\ (\ ) :ref:`🔗<class_EditorProperty_method_get_edited_object>`

Trả về object đã chỉnh sửa.

\ **Lưu ý:** Phương thức này có thể trả về ``null`` nếu editor chưa được liên kết với một property. Tuy nhiên, trong :ref:`_update_property()<class_EditorProperty_private_method__update_property>` và :ref:`_set_read_only()<class_EditorProperty_private_method__set_read_only>`, giá trị này *được đảm bảo* không phải là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_get_edited_property:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_edited_property**\ (\ ) |const| :ref:`🔗<class_EditorProperty_method_get_edited_property>`

Trả về property đã chỉnh sửa. Nếu editor của bạn dành cho một property duy nhất (được thêm qua :ref:`EditorInspectorPlugin._parse_property()<class_EditorInspectorPlugin_private_method__parse_property>`), phương thức này sẽ trả về property đó.

\ **Lưu ý:** Phương thức này có thể trả về ``null`` nếu editor chưa được liên kết với một property. Tuy nhiên, trong :ref:`_update_property()<class_EditorProperty_private_method__update_property>` và :ref:`_set_read_only()<class_EditorProperty_private_method__set_read_only>`, giá trị này *được đảm bảo* không phải là ``null``.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_is_selected:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_selected**\ (\ ) |const| :ref:`🔗<class_EditorProperty_method_is_selected>`

Trả về ``true`` nếu property được vẽ ở trạng thái đã chọn. Được inspector sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_select:

.. rst-class:: classref-method

|void| **select**\ (\ focusable\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_EditorProperty_method_select>`

Vẽ property ở trạng thái đã chọn. Được inspector sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_set_bottom_editor:

.. rst-class:: classref-method

|void| **set_bottom_editor**\ (\ editor\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_EditorProperty_method_set_bottom_editor>`

Đặt control ``editor`` bên dưới nhãn property. Control này trước đó phải được thêm bằng :ref:`Node.add_child()<class_Node_method_add_child>`.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_set_label_reference:

.. rst-class:: classref-method

|void| **set_label_reference**\ (\ control\: :ref:`Control<class_Control>`\ ) :ref:`🔗<class_EditorProperty_method_set_label_reference>`

Được inspector sử dụng, đặt thành một control sẽ được dùng làm tham chiếu để tính kích thước của nhãn.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_set_object_and_property:

.. rst-class:: classref-method

|void| **set_object_and_property**\ (\ object\: :ref:`Object<class_Object>`, property\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_EditorProperty_method_set_object_and_property>`

Gán object và property cần chỉnh sửa.

.. rst-class:: classref-item-separator

----

.. _class_EditorProperty_method_update_property:

.. rst-class:: classref-method

|void| **update_property**\ (\ ) :ref:`🔗<class_EditorProperty_method_update_property>`

Buộc làm mới phần hiển thị property.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
