:github_url: hide

.. meta::
	:keywords: gamepad, controller

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventJoypadButton.xml.

.. _class_InputEventJoypadButton:

InputEventJoypadButton
======================

**Kế thừa:** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một nút gamepad đang được nhấn hoặc nhả.

.. rst-class:: classref-introduction-group

Mô tả
-----

Loại sự kiện đầu vào dành cho các nút gamepad. Để biết về cần analog và joystick của gamepad, hãy xem :ref:`InputEventJoypadMotion<class_InputEventJoypadMotion>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`JoyButton<enum_@GlobalScope_JoyButton>` | :ref:`button_index<class_InputEventJoypadButton_property_button_index>` | ``0``     |
   +-----------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                       | :ref:`pressed<class_InputEventJoypadButton_property_pressed>`           | ``false`` |
   +-----------------------------------------------+-------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                     | :ref:`pressure<class_InputEventJoypadButton_property_pressure>`         | ``0.0``   |
   +-----------------------------------------------+-------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventJoypadButton_property_button_index:

.. rst-class:: classref-property

:ref:`JoyButton<enum_@GlobalScope_JoyButton>` **button_index** = ``0`` :ref:`🔗<class_InputEventJoypadButton_property_button_index>`

.. rst-class:: classref-property-setget

- |void| **set_button_index**\ (\ value\: :ref:`JoyButton<enum_@GlobalScope_JoyButton>`\ ) - :ref:`JoyButton<enum_@GlobalScope_JoyButton>` **get_button_index**\ (\ )

Mã định danh của nút. Một trong các hằng số nút :ref:`JoyButton<enum_@GlobalScope_JoyButton>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventJoypadButton_property_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pressed** = ``false`` :ref:`🔗<class_InputEventJoypadButton_property_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pressed**\ (\ )

Nếu ``true``, trạng thái của nút là đang được nhấn. Nếu ``false``, trạng thái của nút là đã nhả.

.. rst-class:: classref-item-separator

----

.. _class_InputEventJoypadButton_property_pressure:

.. rst-class:: classref-property

:ref:`float<class_float>` **pressure** = ``0.0`` :ref:`🔗<class_InputEventJoypadButton_property_pressure>`

.. rst-class:: classref-property-setget

- |void| **set_pressure**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pressure**\ (\ )

**Đã lỗi thời:** Thuộc tính này không bao giờ được engine thiết lập và luôn là ``0``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
