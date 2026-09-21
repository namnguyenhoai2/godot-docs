:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventWithModifiers.xml.

.. _class_InputEventWithModifiers:

InputEventWithModifiers
=======================

**Kế thừa:** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`InputEventGesture<class_InputEventGesture>`, :ref:`InputEventKey<class_InputEventKey>`, :ref:`InputEventMouse<class_InputEventMouse>`

Lớp cơ sở trừu tượng cho các sự kiện đầu vào chịu ảnh hưởng của các phím modifier như :kbd:`Shift` và :kbd:`Alt`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về các sự kiện đầu vào từ chuột, bàn phím và cử chỉ chạm. Thông tin này bao gồm các phím modifier nào đang được nhấn, chẳng hạn như :kbd:`Shift` hoặc :kbd:`Alt`. Xem :ref:`Node._input()<class_Node_private_method__input>`.

\ **Lưu ý:** Các phím modifier chỉ được xem là modifier khi được sử dụng kết hợp với một phím khác. Do đó, các biến thành viên tương ứng của chúng, chẳng hạn như :ref:`ctrl_pressed<class_InputEventWithModifiers_property_ctrl_pressed>`, sẽ trả về ``false`` nếu phím được nhấn riêng.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`alt_pressed<class_InputEventWithModifiers_property_alt_pressed>`                                   | ``false``                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`command_or_control_autoremap<class_InputEventWithModifiers_property_command_or_control_autoremap>` | ``false``                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`ctrl_pressed<class_InputEventWithModifiers_property_ctrl_pressed>`                                 | ``false``                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | device                                                                                                   | ``16`` (overrides :ref:`InputEvent<class_InputEvent_property_device>`) |
   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`meta_pressed<class_InputEventWithModifiers_property_meta_pressed>`                                 | ``false``                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`shift_pressed<class_InputEventWithModifiers_property_shift_pressed>`                               | ``false``                                                              |
   +-------------------------+----------------------------------------------------------------------------------------------------------+------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | |bitfield|\[:ref:`KeyModifierMask<enum_@GlobalScope_KeyModifierMask>`\] | :ref:`get_modifiers_mask<class_InputEventWithModifiers_method_get_modifiers_mask>`\ (\ ) |const|                       |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                                 | :ref:`is_command_or_control_pressed<class_InputEventWithModifiers_method_is_command_or_control_pressed>`\ (\ ) |const| |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventWithModifiers_property_alt_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **alt_pressed** = ``false`` :ref:`🔗<class_InputEventWithModifiers_property_alt_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_alt_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_alt_pressed**\ (\ )

Trạng thái của modifier :kbd:`Alt`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventWithModifiers_property_command_or_control_autoremap:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **command_or_control_autoremap** = ``false`` :ref:`🔗<class_InputEventWithModifiers_property_command_or_control_autoremap>`

.. rst-class:: classref-property-setget

- |void| **set_command_or_control_autoremap**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_command_or_control_autoremap**\ (\ )

Tự động sử dụng :kbd:`Meta` (:kbd:`Cmd`) trên macOS và :kbd:`Ctrl` trên các nền tảng khác. Nếu ``true``, không thể đặt :ref:`ctrl_pressed<class_InputEventWithModifiers_property_ctrl_pressed>` và :ref:`meta_pressed<class_InputEventWithModifiers_property_meta_pressed>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventWithModifiers_property_ctrl_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ctrl_pressed** = ``false`` :ref:`🔗<class_InputEventWithModifiers_property_ctrl_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_ctrl_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_ctrl_pressed**\ (\ )

Trạng thái của modifier :kbd:`Ctrl`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventWithModifiers_property_meta_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **meta_pressed** = ``false`` :ref:`🔗<class_InputEventWithModifiers_property_meta_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_meta_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_meta_pressed**\ (\ )

Trạng thái của modifier :kbd:`Meta`. Trên Windows và Linux, modifier này đại diện cho phím Windows (đôi khi được gọi là "meta" hoặc "super" trên Linux). Trên macOS, modifier này đại diện cho phím Command.

.. rst-class:: classref-item-separator

----

.. _class_InputEventWithModifiers_property_shift_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shift_pressed** = ``false`` :ref:`🔗<class_InputEventWithModifiers_property_shift_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_shift_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_shift_pressed**\ (\ )

Trạng thái của modifier :kbd:`Shift`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_InputEventWithModifiers_method_get_modifiers_mask:

.. rst-class:: classref-method

|bitfield|\[:ref:`KeyModifierMask<enum_@GlobalScope_KeyModifierMask>`\] **get_modifiers_mask**\ (\ ) |const| :ref:`🔗<class_InputEventWithModifiers_method_get_modifiers_mask>`

Trả về tổ hợp keycode của các phím modifier.

.. rst-class:: classref-item-separator

----

.. _class_InputEventWithModifiers_method_is_command_or_control_pressed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_command_or_control_pressed**\ (\ ) |const| :ref:`🔗<class_InputEventWithModifiers_method_is_command_or_control_pressed>`

Trên macOS, trả về ``true`` nếu :kbd:`Meta` (:kbd:`Cmd`) được nhấn.

Trên các nền tảng khác, trả về ``true`` nếu :kbd:`Ctrl` được nhấn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
