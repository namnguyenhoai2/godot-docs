:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventGesture.xml.

.. _class_InputEventGesture:

InputEventGesture
=================

**Kế thừa:** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`InputEventMagnifyGesture<class_InputEventMagnifyGesture>`, :ref:`InputEventPanGesture<class_InputEventPanGesture>`

Lớp cơ sở trừu tượng cho các cử chỉ cảm ứng.

.. rst-class:: classref-introduction-group

Mô tả
-----

InputEventGesture được gửi khi người dùng thực hiện một cử chỉ được hỗ trợ trên màn hình cảm ứng. Không thể mô phỏng các cử chỉ bằng chuột, vì chúng thường yêu cầu multi-touch.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`int<class_int>`         | device                                                     | ``0`` (overrides :ref:`InputEvent<class_InputEvent_property_device>`) |
   +-------------------------------+------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`position<class_InputEventGesture_property_position>` | ``Vector2(0, 0)``                                                     |
   +-------------------------------+------------------------------------------------------------+-----------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventGesture_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventGesture_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector2<class_Vector2>` \) - :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Vị trí cử chỉ cục bộ tương đối với :ref:`Viewport<class_Viewport>`. Nếu được sử dụng trong :ref:`Control._gui_input()<class_Control_private_method__gui_input>`, vị trí sẽ tương đối với :ref:`Control<class_Control>` hiện tại đã nhận cử chỉ này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
