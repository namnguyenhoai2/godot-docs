:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventMouse.xml.

.. _class_InputEventMouse:

InputEventMouse
===============

**Kế thừa:** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`InputEventMouseButton<class_InputEventMouseButton>`, :ref:`InputEventMouseMotion<class_InputEventMouseMotion>`

Kiểu input event cơ sở cho các sự kiện chuột.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin chung về các sự kiện chuột.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------------------------+------------------------------------------------------------------------+------------------------------------------------------------------------+
   | |bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\] | :ref:`button_mask<class_InputEventMouse_property_button_mask>`         | ``0``                                                                  |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                   | device                                                                 | ``32`` (overrides :ref:`InputEvent<class_InputEvent_property_device>`) |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                           | :ref:`global_position<class_InputEventMouse_property_global_position>` | ``Vector2(0, 0)``                                                      |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------+------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                           | :ref:`position<class_InputEventMouse_property_position>`               | ``Vector2(0, 0)``                                                      |
   +-------------------------------------------------------------------------+------------------------------------------------------------------------+------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventMouse_property_button_mask:

.. rst-class:: classref-property

|bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\] **button_mask** = ``0`` :ref:`🔗<class_InputEventMouse_property_button_mask>`

.. rst-class:: classref-property-setget

- |void| **set_button_mask**\ (\ value\: |bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\]\ ) - |bitfield|\[:ref:`MouseButtonMask<enum_@GlobalScope_MouseButtonMask>`\] **get_button_mask**\ (\ )

Identifier mặt nạ nút chuột, là một trong các mặt nạ nút :ref:`MouseButton<enum_@GlobalScope_MouseButton>` hoặc một tổ hợp bitwise của chúng.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouse_property_global_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **global_position** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouse_property_global_position>`

.. rst-class:: classref-property-setget

- |void| **set_global_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_global_position**\ (\ )

Khi được nhận trong :ref:`Node._input()<class_Node_private_method__input>` hoặc :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>`, trả về vị trí của chuột trong :ref:`Viewport<class_Viewport>` gốc bằng hệ tọa độ của :ref:`Viewport<class_Viewport>` gốc.

Khi được nhận trong :ref:`Control._gui_input()<class_Control_private_method__gui_input>`, trả về vị trí của chuột trong :ref:`CanvasLayer<class_CanvasLayer>` mà :ref:`Control<class_Control>` đang ở đó, bằng hệ tọa độ của :ref:`CanvasLayer<class_CanvasLayer>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouse_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventMouse_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Khi được nhận trong :ref:`Node._input()<class_Node_private_method__input>` hoặc :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>`, trả về vị trí của chuột trong :ref:`Viewport<class_Viewport>` mà :ref:`Node<class_Node>` này đang ở đó, bằng hệ tọa độ của :ref:`Viewport<class_Viewport>` này.

Khi được nhận trong :ref:`Control._gui_input()<class_Control_private_method__gui_input>`, trả về vị trí của chuột trong :ref:`Control<class_Control>` bằng hệ tọa độ cục bộ của :ref:`Control<class_Control>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
