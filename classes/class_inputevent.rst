:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEvent.xml.

.. _class_InputEvent:

InputEvent
==========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`InputEventAction<class_InputEventAction>`, :ref:`InputEventFromWindow<class_InputEventFromWindow>`, :ref:`InputEventJoypadButton<class_InputEventJoypadButton>`, :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`, :ref:`InputEventMIDI<class_InputEventMIDI>`, :ref:`InputEventShortcut<class_InputEventShortcut>`

Lớp cơ sở trừu tượng cho các sự kiện đầu vào.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở trừu tượng của tất cả các loại sự kiện đầu vào. Xem :ref:`Node._input()<class_Node_private_method__input>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

- :doc:`Các phép biến đổi viewport và canvas <../tutorials/2d/2d_transforms>`

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------+-------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`device<class_InputEvent_property_device>` | ``0`` |
   +-----------------------+-------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`accumulate<class_InputEvent_method_accumulate>`\ (\ with_event\: :ref:`InputEvent<class_InputEvent>`\ )                                                                                                                |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`         | :ref:`as_text<class_InputEvent_method_as_text>`\ (\ ) |const|                                                                                                                                                                |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`get_action_strength<class_InputEvent_method_get_action_strength>`\ (\ action\: :ref:`StringName<class_StringName>`, exact_match\: :ref:`bool<class_bool>` = false\ ) |const|                                           |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_action<class_InputEvent_method_is_action>`\ (\ action\: :ref:`StringName<class_StringName>`, exact_match\: :ref:`bool<class_bool>` = false\ ) |const|                                                               |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_action_pressed<class_InputEvent_method_is_action_pressed>`\ (\ action\: :ref:`StringName<class_StringName>`, allow_echo\: :ref:`bool<class_bool>` = false, exact_match\: :ref:`bool<class_bool>` = false\ ) |const| |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_action_released<class_InputEvent_method_is_action_released>`\ (\ action\: :ref:`StringName<class_StringName>`, exact_match\: :ref:`bool<class_bool>` = false\ ) |const|                                             |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_action_type<class_InputEvent_method_is_action_type>`\ (\ ) |const|                                                                                                                                                  |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_canceled<class_InputEvent_method_is_canceled>`\ (\ ) |const|                                                                                                                                                        |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_echo<class_InputEvent_method_is_echo>`\ (\ ) |const|                                                                                                                                                                |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_match<class_InputEvent_method_is_match>`\ (\ event\: :ref:`InputEvent<class_InputEvent>`, exact_match\: :ref:`bool<class_bool>` = true\ ) |const|                                                                   |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_pressed<class_InputEvent_method_is_pressed>`\ (\ ) |const|                                                                                                                                                          |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_released<class_InputEvent_method_is_released>`\ (\ ) |const|                                                                                                                                                        |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`InputEvent<class_InputEvent>` | :ref:`xformed_by<class_InputEvent_method_xformed_by>`\ (\ xform\: :ref:`Transform2D<class_Transform2D>`, local_ofs\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |const|                                                |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_InputEvent_constant_DEVICE_ID_EMULATION:

.. rst-class:: classref-constant

**DEVICE_ID_EMULATION** = ``-1`` :ref:`🔗<class_InputEvent_constant_DEVICE_ID_EMULATION>`

ID thiết bị được dùng cho đầu vào chuột mô phỏng từ màn hình cảm ứng hoặc đầu vào cảm ứng mô phỏng từ chuột. Có thể dùng giá trị này để phân biệt đầu vào chuột mô phỏng với đầu vào chuột vật lý hoặc đầu vào cảm ứng mô phỏng với đầu vào cảm ứng vật lý.

.. _class_InputEvent_constant_DEVICE_ID_KEYBOARD:

.. rst-class:: classref-constant

**DEVICE_ID_KEYBOARD** = ``16`` :ref:`🔗<class_InputEvent_constant_DEVICE_ID_KEYBOARD>`

ID thiết bị được dùng cho đầu vào từ bàn phím. Có thể dùng giá trị này để phân biệt các sự kiện đầu vào từ bàn phím với các sự kiện đầu vào từ joypad.

.. _class_InputEvent_constant_DEVICE_ID_MOUSE:

.. rst-class:: classref-constant

**DEVICE_ID_MOUSE** = ``32`` :ref:`🔗<class_InputEvent_constant_DEVICE_ID_MOUSE>`

ID thiết bị được dùng cho đầu vào từ chuột. Có thể dùng giá trị này để phân biệt các sự kiện đầu vào từ chuột với các sự kiện đầu vào từ joypad.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEvent_property_device:

.. rst-class:: classref-property

:ref:`int<class_int>` **device** = ``0`` :ref:`🔗<class_InputEvent_property_device>`

.. rst-class:: classref-property-setget

- |void| **set_device**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_device**\ (\ )

ID thiết bị của sự kiện.

\ **Lưu ý:** :ref:`device<class_InputEvent_property_device>` có thể là số âm trong các trường hợp đặc biệt không tham chiếu đến các thiết bị thực sự hiện diện trên hệ thống. Xem :ref:`DEVICE_ID_EMULATION<class_InputEvent_constant_DEVICE_ID_EMULATION>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_InputEvent_method_accumulate:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **accumulate**\ (\ with_event\: :ref:`InputEvent<class_InputEvent>`\ ) :ref:`🔗<class_InputEvent_method_accumulate>`

Trả về ``true`` nếu sự kiện đầu vào được cung cấp và sự kiện đầu vào này có thể được cộng với nhau (chỉ áp dụng cho các sự kiện thuộc loại :ref:`InputEventMouseMotion<class_InputEventMouseMotion>`).

Vị trí, vị trí toàn cục và tốc độ của sự kiện đầu vào được cung cấp sẽ được sao chép. ``relative`` kết quả là tổng của cả hai sự kiện. Các modifier của cả hai sự kiện phải giống hệt nhau.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_as_text:

.. rst-class:: classref-method

:ref:`String<class_String>` **as_text**\ (\ ) |const| :ref:`🔗<class_InputEvent_method_as_text>`

Trả về biểu diễn :ref:`String<class_String>` của sự kiện.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_get_action_strength:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_action_strength**\ (\ action\: :ref:`StringName<class_StringName>`, exact_match\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_InputEvent_method_get_action_strength>`

Trả về một giá trị từ 0.0 đến 1.0 tùy thuộc vào trạng thái của các action được cung cấp. Hữu ích để lấy giá trị của các sự kiện thuộc loại :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

Nếu ``exact_match`` là ``false``, phương thức sẽ bỏ qua các input modifier bổ sung đối với các sự kiện :ref:`InputEventKey<class_InputEventKey>` và :ref:`InputEventMouseButton<class_InputEventMouseButton>`, cũng như hướng đối với các sự kiện :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_action:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_action**\ (\ action\: :ref:`StringName<class_StringName>`, exact_match\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_InputEvent_method_is_action>`

Trả về ``true`` nếu sự kiện đầu vào này khớp với một action được định nghĩa trước thuộc bất kỳ loại nào.

Nếu ``exact_match`` là ``false``, phương thức sẽ bỏ qua các input modifier bổ sung đối với các sự kiện :ref:`InputEventKey<class_InputEventKey>` và :ref:`InputEventMouseButton<class_InputEventMouseButton>`, cũng như hướng đối với các sự kiện :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_action_pressed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_action_pressed**\ (\ action\: :ref:`StringName<class_StringName>`, allow_echo\: :ref:`bool<class_bool>` = false, exact_match\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_InputEvent_method_is_action_pressed>`

Trả về ``true`` nếu action được cung cấp khớp với sự kiện này và đang được nhấn (đồng thời không phải là sự kiện echo đối với các sự kiện :ref:`InputEventKey<class_InputEventKey>`, trừ khi ``allow_echo`` là ``true``). Không áp dụng cho các sự kiện thuộc loại :ref:`InputEventMouseMotion<class_InputEventMouseMotion>` hoặc :ref:`InputEventScreenDrag<class_InputEventScreenDrag>`.

Nếu ``exact_match`` là ``false``, phương thức sẽ bỏ qua các input modifier bổ sung đối với các sự kiện :ref:`InputEventKey<class_InputEventKey>` và :ref:`InputEventMouseButton<class_InputEventMouseButton>`, cũng như hướng đối với các sự kiện :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

\ **Lưu ý:** Do hiện tượng keyboard ghosting, :ref:`is_action_pressed()<class_InputEvent_method_is_action_pressed>` có thể trả về ``false`` ngay cả khi một trong các phím của action đang được nhấn. Xem `Input examples <../tutorials/inputs/input_examples.html#keyboard-events>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_action_released:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_action_released**\ (\ action\: :ref:`StringName<class_StringName>`, exact_match\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_InputEvent_method_is_action_released>`

Trả về ``true`` nếu action được cung cấp khớp với sự kiện này và đã được nhả (tức là không được nhấn). Không áp dụng cho các sự kiện thuộc loại :ref:`InputEventMouseMotion<class_InputEventMouseMotion>` hoặc :ref:`InputEventScreenDrag<class_InputEventScreenDrag>`.

Nếu ``exact_match`` là ``false``, phương thức sẽ bỏ qua các input modifier bổ sung đối với các sự kiện :ref:`InputEventKey<class_InputEventKey>` và :ref:`InputEventMouseButton<class_InputEventMouseButton>`, cũng như hướng đối với các sự kiện :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_action_type:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_action_type**\ (\ ) |const| :ref:`🔗<class_InputEvent_method_is_action_type>`

Trả về ``true`` nếu loại của sự kiện đầu vào này là loại có thể được gán cho một input action: :ref:`InputEventKey<class_InputEventKey>`, :ref:`InputEventMouseButton<class_InputEventMouseButton>`, :ref:`InputEventJoypadButton<class_InputEventJoypadButton>`, :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`, :ref:`InputEventAction<class_InputEventAction>`. Trả về ``false`` đối với tất cả các loại sự kiện đầu vào khác.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_canceled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_canceled**\ (\ ) |const| :ref:`🔗<class_InputEvent_method_is_canceled>`

Trả về ``true`` nếu sự kiện đầu vào này đã bị hủy.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_echo:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_echo**\ (\ ) |const| :ref:`🔗<class_InputEvent_method_is_echo>`

Trả về ``true`` nếu sự kiện đầu vào này là sự kiện echo (chỉ áp dụng cho các sự kiện thuộc loại :ref:`InputEventKey<class_InputEventKey>`). Sự kiện echo là một sự kiện phím lặp lại được gửi khi người dùng giữ phím. Mọi loại sự kiện khác đều trả về ``false``.

\ **Lưu ý:** Tần suất gửi các sự kiện echo thường vào khoảng 20 sự kiện mỗi giây (sau khi giữ phím trong khoảng nửa giây). Tuy nhiên, người dùng có thể thay đổi độ trễ/tốc độ lặp phím hoặc tắt hoàn toàn tính năng này trong phần cài đặt hệ điều hành. Để bảo đảm dự án hoạt động chính xác trên mọi cấu hình, không giả định rằng người dùng có một cấu hình lặp phím cụ thể trong hành vi của dự án.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_match:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_match**\ (\ event\: :ref:`InputEvent<class_InputEvent>`, exact_match\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_InputEvent_method_is_match>`

Trả về ``true`` nếu ``event`` được chỉ định khớp với sự kiện này. Chỉ hợp lệ đối với các sự kiện action, bao gồm các sự kiện phím (:ref:`InputEventKey<class_InputEventKey>`), nút (:ref:`InputEventMouseButton<class_InputEventMouseButton>` hoặc :ref:`InputEventJoypadButton<class_InputEventJoypadButton>`), trục :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>` và action (:ref:`InputEventAction<class_InputEventAction>`).

Nếu ``exact_match`` là ``false``, phép kiểm tra sẽ bỏ qua các input modifier bổ sung đối với các sự kiện :ref:`InputEventKey<class_InputEventKey>` và :ref:`InputEventMouseButton<class_InputEventMouseButton>`, cũng như hướng đối với các sự kiện :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

\ **Lưu ý:** Phương thức này chỉ xem xét cấu hình của sự kiện (chẳng hạn như phím bàn phím hoặc trục joypad), không xem xét thông tin trạng thái như :ref:`is_pressed()<class_InputEvent_method_is_pressed>`, :ref:`is_released()<class_InputEvent_method_is_released>`, :ref:`is_echo()<class_InputEvent_method_is_echo>` hoặc :ref:`is_canceled()<class_InputEvent_method_is_canceled>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_pressed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_pressed**\ (\ ) |const| :ref:`🔗<class_InputEvent_method_is_pressed>`

Trả về ``true`` nếu sự kiện đầu vào này đang được nhấn. Không áp dụng cho các sự kiện thuộc loại :ref:`InputEventMouseMotion<class_InputEventMouseMotion>` hoặc :ref:`InputEventScreenDrag<class_InputEventScreenDrag>`.

\ **Lưu ý:** Do hiện tượng keyboard ghosting, :ref:`is_pressed()<class_InputEvent_method_is_pressed>` có thể trả về ``false`` ngay cả khi một trong các phím của action đang được nhấn. Xem `Input examples <../tutorials/inputs/input_examples.html#keyboard-events>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_is_released:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_released**\ (\ ) |const| :ref:`🔗<class_InputEvent_method_is_released>`

Trả về ``true`` nếu sự kiện đầu vào này đã được nhả. Không áp dụng cho các sự kiện thuộc loại :ref:`InputEventMouseMotion<class_InputEventMouseMotion>` hoặc :ref:`InputEventScreenDrag<class_InputEventScreenDrag>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEvent_method_xformed_by:

.. rst-class:: classref-method

:ref:`InputEvent<class_InputEvent>` **xformed_by**\ (\ xform\: :ref:`Transform2D<class_Transform2D>`, local_ofs\: :ref:`Vector2<class_Vector2>` = Vector2(0, 0)\ ) |const| :ref:`🔗<class_InputEvent_method_xformed_by>`

Trả về một bản sao của sự kiện đầu vào được cung cấp, đã được dịch chuyển một khoảng ``local_ofs`` và biến đổi bởi ``xform``. Áp dụng cho các sự kiện thuộc loại :ref:`InputEventMouseButton<class_InputEventMouseButton>`, :ref:`InputEventMouseMotion<class_InputEventMouseMotion>`, :ref:`InputEventScreenTouch<class_InputEventScreenTouch>`, :ref:`InputEventScreenDrag<class_InputEventScreenDrag>`, :ref:`InputEventMagnifyGesture<class_InputEventMagnifyGesture>` và :ref:`InputEventPanGesture<class_InputEventPanGesture>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
