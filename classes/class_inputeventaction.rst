:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventAction.xml.

.. _class_InputEventAction:

InputEventAction
================

**Kế thừa:** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một loại input event dành cho các action.

.. rst-class:: classref-introduction-group

Mô tả
-----

Chứa một action chung có thể được nhắm đến từ nhiều loại input. Có thể thiết lập các action và event của chúng trong tab **Input Map** tại **Project > Project Settings**, hoặc bằng class :ref:`InputMap<class_InputMap>`.

\ **Lưu ý:** Không giống các lớp con :ref:`InputEvent<class_InputEvent>` khác, vốn ánh xạ tới các sự kiện vật lý riêng biệt, virtual event này không được engine phát ra. Class này hữu ích để phát các action thủ công bằng :ref:`Input.parse_input_event()<class_Input_method_parse_input_event>`, sau đó chúng sẽ được nhận trong :ref:`Node._input()<class_Node_private_method__input>`. Để kiểm tra một sự kiện vật lý có khớp với một action trong Input Map hay không, hãy sử dụng :ref:`InputEvent.is_action()<class_InputEvent_method_is_action>` và :ref:`InputEvent.is_action_pressed()<class_InputEvent_method_is_action_pressed>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Using InputEvent: Actions <../tutorials/inputs/inputevent.html#actions>`__

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------+-----------+
   | :ref:`StringName<class_StringName>` | :ref:`action<class_InputEventAction_property_action>`           | ``&""``   |
   +-------------------------------------+-----------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`               | :ref:`event_index<class_InputEventAction_property_event_index>` | ``-1``    |
   +-------------------------------------+-----------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`             | :ref:`pressed<class_InputEventAction_property_pressed>`         | ``false`` |
   +-------------------------------------+-----------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`strength<class_InputEventAction_property_strength>`       | ``1.0``   |
   +-------------------------------------+-----------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventAction_property_action:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **action** = ``&""`` :ref:`🔗<class_InputEventAction_property_action>`

.. rst-class:: classref-property-setget

- |void| **set_action**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_action**\ (\ )

Tên của action. Đây thường là tên của một action hiện có trong :ref:`InputMap<class_InputMap>` mà bạn muốn custom event này khớp với nó.

.. rst-class:: classref-item-separator

----

.. _class_InputEventAction_property_event_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **event_index** = ``-1`` :ref:`🔗<class_InputEventAction_property_event_index>`

.. rst-class:: classref-property-setget

- |void| **set_event_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_event_index**\ (\ )

Chỉ mục event thực trong action mà event này tương ứng với (từ các event được định nghĩa cho action này trong :ref:`InputMap<class_InputMap>`). Nếu ``-1``, một ID duy nhất sẽ được sử dụng và các action được nhấn bằng ID này sẽ cần được nhả bằng một **InputEventAction** khác.

.. rst-class:: classref-item-separator

----

.. _class_InputEventAction_property_pressed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **pressed** = ``false`` :ref:`🔗<class_InputEventAction_property_pressed>`

.. rst-class:: classref-property-setget

- |void| **set_pressed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pressed**\ (\ )

Nếu ``true``, trạng thái của action là được nhấn. Nếu ``false``, trạng thái của action là được nhả.

.. rst-class:: classref-item-separator

----

.. _class_InputEventAction_property_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **strength** = ``1.0`` :ref:`🔗<class_InputEventAction_property_strength>`

.. rst-class:: classref-property-setget

- |void| **set_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_strength**\ (\ )

Độ mạnh của action trong khoảng từ 0 đến 1. Giá trị này được xem là bằng 0 nếu pressed là ``false``. Độ mạnh của event cho phép giả lập các event chuyển động analog của joypad bằng cách chỉ định mức độ trục joypad bị nghiêng hoặc nhấn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
