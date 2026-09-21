:github_url: hide

.. meta::
	:keywords: click, press

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventMouseButton.xml.

.. _class_InputEventMouseButton:

InputEventMouseButton
=====================

**Kế thừa:** :ref:`InputEventMouse<class_InputEventMouse>` **<** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho việc một nút chuột được nhấn hoặc nhả.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về các sự kiện nhấp chuột. Xem :ref:`Node._input()<class_Node_private_method__input>`.

\ **Lưu ý:** Trên các thiết bị Wear OS, thao tác nhập từ núm xoay được ánh xạ tới :ref:`@GlobalScope.MOUSE_BUTTON_WHEEL_UP<class_@GlobalScope_constant_MOUSE_BUTTON_WHEEL_UP>` và :ref:`@GlobalScope.MOUSE_BUTTON_WHEEL_DOWN<class_@GlobalScope_constant_MOUSE_BUTTON_WHEEL_DOWN>`. Có thể thay đổi thành :ref:`@GlobalScope.MOUSE_BUTTON_WHEEL_LEFT<class_@GlobalScope_constant_MOUSE_BUTTON_WHEEL_LEFT>` và :ref:`@GlobalScope.MOUSE_BUTTON_WHEEL_RIGHT<class_@GlobalScope_constant_MOUSE_BUTTON_WHEEL_RIGHT>` bằng setting :ref:`ProjectSettings.input_devices/pointing/android/rotary_input_scroll_axis<class_ProjectSettings_property_input_devices/pointing/android/rotary_input_scroll_axis>`.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

- :doc:`Tọa độ chuột và tọa độ đầu vào <../tutorials/inputs/mouse_and_input_coordinates>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`MouseButton<enum_@GlobalScope_MouseButton>` | :ref:`button_index<class_InputEventMouseButton_property_button_index>` | ``0``     |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`canceled<class_InputEventMouseButton_property_canceled>`         | ``false`` |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`double_click<class_InputEventMouseButton_property_double_click>` | ``false`` |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`factor<class_InputEventMouseButton_property_factor>`             | ``1.0``   |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`pressed<class_InputEventMouseButton_property_pressed>`           | ``false`` |
   +---------------------------------------------------+------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventMouseButton_property_button_index:

.. rst-class:: classref-property

:ref:`MouseButton<enum_@GlobalScope_MouseButton>` **button_index** = ``0`` :ref:`🔗<class_InputEventMouseButton_property_button_index>`

.. rst-class:: classref-property-setget

- |void| **set_button_index**\ (\ value\: :ref:`MouseButton<enum_@GlobalScope_MouseButton>`\ ) - :ref:`MouseButton<enum_@GlobalScope_MouseButton>` **get_button_index**\ (\ )

Mã định danh nút chuột, là một trong các hằng số nút hoặc bánh xe nút :ref:`MouseButton<enum_@GlobalScope_MouseButton>`.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseButton_property_canceled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **canceled** = ``false`` :ref:`🔗<class_InputEventMouseButton_property_canceled>`

.. rst-class:: classref-property-setget

- |void| **set_canceled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_canceled**\ (\ )

Nếu ``true``, sự kiện nút chuột đã bị hủy.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseButton_property_double_click:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **double_click** = ``false`` :ref:`🔗<class_InputEventMouseButton_property_double_click>`

.. rst-class:: classref-property-setget

- |void| **set_double_click**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_double_click**\ (\ )

Nếu ``true``, trạng thái của nút chuột là nhấp đúp.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseButton_property_factor:

.. rst-class:: classref-property

:ref:`float<class_float>` **factor** = ``1.0`` :ref:`🔗<class_InputEventMouseButton_property_factor>`

.. rst-class:: classref-property-setget

- |void| **set_factor**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_factor**\ (\ )

Giá trị (hoặc delta) của sự kiện. Khi được sử dụng cho các sự kiện cuộn có độ chính xác cao, giá trị này cho biết lượng cuộn (theo chiều dọc hoặc chiều ngang). Tính năng này chỉ được hỗ trợ trên một số nền tảng; độ nhạy được báo cáo thay đổi tùy theo nền tảng. Có thể là ``0`` nếu không được hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_InputEventMouseButton_property_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pressed** = ``false`` :ref:`🔗<class_InputEventMouseButton_property_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pressed**\ (\ )

Nếu ``true``, trạng thái của nút chuột là đang được nhấn. Nếu ``false``, trạng thái của nút chuột là đã được nhả.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
