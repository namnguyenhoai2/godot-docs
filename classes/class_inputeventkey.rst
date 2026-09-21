:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các source của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventKey.xml.

.. _class_InputEventKey:

InputEventKey
=============

**Kế thừa:** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một phím trên bàn phím đang được nhấn hoặc thả.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một input event dành cho các phím trên bàn phím. Hỗ trợ thao tác nhấn phím, thả phím và các event :ref:`echo<class_InputEventKey_property_echo>`. Nó cũng có thể được nhận trong :ref:`Node._unhandled_key_input()<class_Node_private_method__unhandled_key_input>`.

\ **Lưu ý:** Các event nhận được từ bàn phím thường có tất cả thuộc tính được thiết lập. Các ánh xạ event chỉ nên thiết lập một trong :ref:`keycode<class_InputEventKey_property_keycode>`, :ref:`physical_keycode<class_InputEventKey_property_physical_keycode>` hoặc :ref:`unicode<class_InputEventKey_property_unicode>`.

Khi các event được so sánh, các thuộc tính được kiểm tra theo thứ tự ưu tiên sau: :ref:`keycode<class_InputEventKey_property_keycode>`, :ref:`physical_keycode<class_InputEventKey_property_physical_keycode>` và :ref:`unicode<class_InputEventKey_property_unicode>`. Các event có giá trị trùng khớp đầu tiên sẽ được xem là bằng nhau.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`echo<class_InputEventKey_property_echo>`                         | ``false`` |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`Key<enum_@GlobalScope_Key>`                 | :ref:`key_label<class_InputEventKey_property_key_label>`               | ``0``     |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`Key<enum_@GlobalScope_Key>`                 | :ref:`keycode<class_InputEventKey_property_keycode>`                   | ``0``     |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`KeyLocation<enum_@GlobalScope_KeyLocation>` | :ref:`location<class_InputEventKey_property_location>`                 | ``0``     |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`Key<enum_@GlobalScope_Key>`                 | :ref:`physical_keycode<class_InputEventKey_property_physical_keycode>` | ``0``     |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`pressed<class_InputEventKey_property_pressed>`                   | ``false`` |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                             | :ref:`unicode<class_InputEventKey_property_unicode>`                   | ``0``     |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`       | :ref:`as_text_key_label<class_InputEventKey_method_as_text_key_label>`\ (\ ) |const|                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`       | :ref:`as_text_keycode<class_InputEventKey_method_as_text_keycode>`\ (\ ) |const|                                         |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`       | :ref:`as_text_location<class_InputEventKey_method_as_text_location>`\ (\ ) |const|                                       |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`       | :ref:`as_text_physical_keycode<class_InputEventKey_method_as_text_physical_keycode>`\ (\ ) |const|                       |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Key<enum_@GlobalScope_Key>` | :ref:`get_key_label_with_modifiers<class_InputEventKey_method_get_key_label_with_modifiers>`\ (\ ) |const|               |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Key<enum_@GlobalScope_Key>` | :ref:`get_keycode_with_modifiers<class_InputEventKey_method_get_keycode_with_modifiers>`\ (\ ) |const|                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Key<enum_@GlobalScope_Key>` | :ref:`get_physical_keycode_with_modifiers<class_InputEventKey_method_get_physical_keycode_with_modifiers>`\ (\ ) |const| |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventKey_property_echo:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **echo** = ``false`` :ref:`🔗<class_InputEventKey_property_echo>`

.. rst-class:: classref-property-setget

- |void| **set_echo**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_echo**\ (\ )

Nếu ``true``, phím đã được nhấn trước event này. Một echo event là một key event lặp lại được gửi khi người dùng đang giữ phím.

\ **Lưu ý:** Tốc độ gửi echo event thường vào khoảng 20 event mỗi giây (sau khi giữ phím trong khoảng nửa giây). Tuy nhiên, độ trễ/tốc độ lặp phím có thể được người dùng thay đổi hoặc tắt hoàn toàn trong cài đặt hệ điều hành. Để đảm bảo project của bạn hoạt động chính xác trên mọi cấu hình, không được giả định người dùng có một cấu hình lặp phím cụ thể trong hành vi của project.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_property_key_label:

.. rst-class:: classref-property

:ref:`Key<enum_@GlobalScope_Key>` **key_label** = ``0`` :ref:`🔗<class_InputEventKey_property_key_label>`

.. rst-class:: classref-property-setget

- |void| **set_key_label**\ (\ value\: :ref:`Key<enum_@GlobalScope_Key>`\ ) - :ref:`Key<enum_@GlobalScope_Key>` **get_key_label**\ (\ )

Đại diện cho nhãn được bản địa hóa in trên phím trong layout bàn phím hiện tại, tương ứng với một trong các hằng số :ref:`Key<enum_@GlobalScope_Key>` hoặc bất kỳ ký tự Unicode hợp lệ nào. Key label được dùng cho các lời nhắc về phím.

Đối với các layout bàn phím có một nhãn duy nhất trên phím, thuộc tính này tương đương với :ref:`keycode<class_InputEventKey_property_keycode>`.

Để lấy biểu diễn mà con người có thể đọc được của **InputEventKey**, hãy sử dụng ``OS.get_keycode_string(event.key_label)`` trong đó ``event`` là **InputEventKey**.

.. code:: text

    +-----+ +-----+
    | Q   | | Q   | - "Q" - keycode
    |   Й | |  ض | - "Й" and "ض" - key_label
    +-----+ +-----+

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_property_keycode:

.. rst-class:: classref-property

:ref:`Key<enum_@GlobalScope_Key>` **keycode** = ``0`` :ref:`🔗<class_InputEventKey_property_keycode>`

.. rst-class:: classref-property-setget

- |void| **set_keycode**\ (\ value\: :ref:`Key<enum_@GlobalScope_Key>`\ ) - :ref:`Key<enum_@GlobalScope_Key>` **get_keycode**\ (\ )

Nhãn Latin được in trên phím trong layout bàn phím hiện tại, tương ứng với một trong các hằng số :ref:`Key<enum_@GlobalScope_Key>`. Key code được dùng cho các shortcut được biểu diễn bằng bàn phím Latin tiêu chuẩn, chẳng hạn như :kbd:`Ctrl + S` cho shortcut "Lưu".

Để lấy biểu diễn mà con người có thể đọc được của **InputEventKey**, hãy sử dụng ``OS.get_keycode_string(event.keycode)`` trong đó ``event`` là **InputEventKey**.

.. code:: text

    +-----+ +-----+
    | Q   | | Q   | - "Q" - keycode
    |   Й | |  ض | - "Й" and "ض" - key_label
    +-----+ +-----+

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_property_location:

.. rst-class:: classref-property

:ref:`KeyLocation<enum_@GlobalScope_KeyLocation>` **location** = ``0`` :ref:`🔗<class_InputEventKey_property_location>`

.. rst-class:: classref-property-setget

- |void| **set_location**\ (\ value\: :ref:`KeyLocation<enum_@GlobalScope_KeyLocation>`\ ) - :ref:`KeyLocation<enum_@GlobalScope_KeyLocation>` **get_location**\ (\ )

Đại diện cho vị trí của một phím có cả phiên bản trái và phải, chẳng hạn như :kbd:`Shift` hoặc :kbd:`Alt`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_property_physical_keycode:

.. rst-class:: classref-property

:ref:`Key<enum_@GlobalScope_Key>` **physical_keycode** = ``0`` :ref:`🔗<class_InputEventKey_property_physical_keycode>`

.. rst-class:: classref-property-setget

- |void| **set_physical_keycode**\ (\ value\: :ref:`Key<enum_@GlobalScope_Key>`\ ) - :ref:`Key<enum_@GlobalScope_Key>` **get_physical_keycode**\ (\ )

Đại diện cho vị trí vật lý của một phím trên bàn phím US QWERTY 101/102 phím, tương ứng với một trong các hằng số :ref:`Key<enum_@GlobalScope_Key>`. Physical key code được dùng cho input trong game, chẳng hạn như thao tác di chuyển WASD, khi chỉ vị trí của các phím là quan trọng.

Để lấy biểu diễn mà con người có thể đọc được của **InputEventKey**, hãy sử dụng :ref:`OS.get_keycode_string()<class_OS_method_get_keycode_string>` kết hợp với :ref:`DisplayServer.keyboard_get_keycode_from_physical()<class_DisplayServer_method_keyboard_get_keycode_from_physical>` hoặc :ref:`DisplayServer.keyboard_get_label_from_physical()<class_DisplayServer_method_keyboard_get_label_from_physical>`:


.. tabs::

 .. code-tab:: gdscript

    func _input(event):
        if event is InputEventKey:
            var keycode = DisplayServer.keyboard_get_keycode_from_physical(event.physical_keycode)
            var label = DisplayServer.keyboard_get_label_from_physical(event.physical_keycode)
            print(OS.get_keycode_string(keycode))
            print(OS.get_keycode_string(label))

 .. code-tab:: csharp

    public override void _Input(InputEvent @event)
    {
        if (@event is InputEventKey inputEventKey)
        {
            var keycode = DisplayServer.KeyboardGetKeycodeFromPhysical(inputEventKey.PhysicalKeycode);
            var label = DisplayServer.KeyboardGetLabelFromPhysical(inputEventKey.PhysicalKeycode);
            GD.Print(OS.GetKeycodeString(keycode));
            GD.Print(OS.GetKeycodeString(label));
        }
    }



.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_property_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pressed** = ``false`` :ref:`🔗<class_InputEventKey_property_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pressed**\ (\ )

Nếu ``true``, trạng thái của phím là đang được nhấn. Nếu ``false``, trạng thái của phím là đã được thả.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_property_unicode:

.. rst-class:: classref-property

:ref:`int<class_int>` **unicode** = ``0`` :ref:`🔗<class_InputEventKey_property_unicode>`

.. rst-class:: classref-property-setget

- |void| **set_unicode**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_unicode**\ (\ )

Mã ký tự Unicode của phím (khi có liên quan), sau khi được thay đổi bởi các phím modifier. Mã ký tự Unicode cho các ký tự ghép và các script phức tạp có thể không khả dụng nếu chưa bật chế độ nhập IME. Xem :ref:`Window.set_ime_active()<class_Window_method_set_ime_active>` để biết thêm thông tin. Mã ký tự Unicode được dùng cho việc nhập văn bản.

\ **Lưu ý:** Engine chỉ thiết lập thuộc tính này cho event nhấn phím. Nếu event được gửi bởi IME hoặc bàn phím ảo, sẽ không có event thả phím tương ứng được gửi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_InputEventKey_method_as_text_key_label:

.. rst-class:: classref-method

:ref:`String<class_String>` **as_text_key_label**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_as_text_key_label>`

Trả về biểu diễn :ref:`String<class_String>` của :ref:`key_label<class_InputEventKey_property_key_label>` và các phím modifier của event.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_method_as_text_keycode:

.. rst-class:: classref-method

:ref:`String<class_String>` **as_text_keycode**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_as_text_keycode>`

Trả về biểu diễn :ref:`String<class_String>` của :ref:`keycode<class_InputEventKey_property_keycode>` và các phím modifier của event.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_method_as_text_location:

.. rst-class:: classref-method

:ref:`String<class_String>` **as_text_location**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_as_text_location>`

Trả về biểu diễn :ref:`String<class_String>` của :ref:`location<class_InputEventKey_property_location>` của event. Đây sẽ là một chuỗi trống nếu event không dành riêng cho một vị trí.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_method_as_text_physical_keycode:

.. rst-class:: classref-method

:ref:`String<class_String>` **as_text_physical_keycode**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_as_text_physical_keycode>`

Trả về biểu diễn :ref:`String<class_String>` của :ref:`physical_keycode<class_InputEventKey_property_physical_keycode>` và các phím modifier của event.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_method_get_key_label_with_modifiers:

.. rst-class:: classref-method

:ref:`Key<enum_@GlobalScope_Key>` **get_key_label_with_modifiers**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_get_key_label_with_modifiers>`

Trả về key label được bản địa hóa kết hợp với các phím modifier như :kbd:`Shift` hoặc :kbd:`Alt`. Xem thêm :ref:`InputEventWithModifiers<class_InputEventWithModifiers>`.

Để lấy biểu diễn mà con người có thể đọc được của **InputEventKey** cùng các phím modifier, hãy sử dụng ``OS.get_keycode_string(event.get_key_label_with_modifiers())`` trong đó ``event`` là **InputEventKey**.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_method_get_keycode_with_modifiers:

.. rst-class:: classref-method

:ref:`Key<enum_@GlobalScope_Key>` **get_keycode_with_modifiers**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_get_keycode_with_modifiers>`

Trả về keycode Latin kết hợp với các phím modifier như :kbd:`Shift` hoặc :kbd:`Alt`. Xem thêm :ref:`InputEventWithModifiers<class_InputEventWithModifiers>`.

Để lấy biểu diễn mà con người có thể đọc được của **InputEventKey** cùng các phím modifier, hãy sử dụng ``OS.get_keycode_string(event.get_keycode_with_modifiers())`` trong đó ``event`` là **InputEventKey**.

.. rst-class:: classref-item-separator

----

.. _class_InputEventKey_method_get_physical_keycode_with_modifiers:

.. rst-class:: classref-method

:ref:`Key<enum_@GlobalScope_Key>` **get_physical_keycode_with_modifiers**\ (\ ) |const| :ref:`🔗<class_InputEventKey_method_get_physical_keycode_with_modifiers>`

Trả về physical keycode kết hợp với các phím modifier như :kbd:`Shift` hoặc :kbd:`Alt`. Xem thêm :ref:`InputEventWithModifiers<class_InputEventWithModifiers>`.

Để lấy biểu diễn mà con người có thể đọc được của **InputEventKey** cùng các phím modifier, hãy sử dụng ``OS.get_keycode_string(event.get_physical_keycode_with_modifiers())`` trong đó ``event`` là **InputEventKey**.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
