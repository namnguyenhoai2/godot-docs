:github_url: hide

.. meta::
	:keywords: gamepad, controller

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventJoypadMotion.xml.

.. _class_InputEventJoypadMotion:

InputEventJoypadMotion
======================

**Kế thừa:** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho các chuyển động của trục (chẳng hạn như cần điều khiển hoặc trigger analog) từ gamepad.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về các chuyển động của cần điều khiển. Một **InputEventJoypadMotion** đại diện cho một trục tại một thời điểm. Đối với các nút của gamepad, xem :ref:`InputEventJoypadButton<class_InputEventJoypadButton>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------+---------------------------------------------------------------------+---------+
   | :ref:`JoyAxis<enum_@GlobalScope_JoyAxis>` | :ref:`axis<class_InputEventJoypadMotion_property_axis>`             | ``0``   |
   +-------------------------------------------+---------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                 | :ref:`axis_value<class_InputEventJoypadMotion_property_axis_value>` | ``0.0`` |
   +-------------------------------------------+---------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventJoypadMotion_property_axis:

.. rst-class:: classref-property

:ref:`JoyAxis<enum_@GlobalScope_JoyAxis>` **axis** = ``0`` :ref:`🔗<class_InputEventJoypadMotion_property_axis>`

.. rst-class:: classref-property-setget

- |void| **set_axis**\ (\ value\: :ref:`JoyAxis<enum_@GlobalScope_JoyAxis>`\ ) - :ref:`JoyAxis<enum_@GlobalScope_JoyAxis>` **get_axis**\ (\ )

Mã định danh của trục.

.. rst-class:: classref-item-separator

----

.. _class_InputEventJoypadMotion_property_axis_value:

.. rst-class:: classref-property

:ref:`float<class_float>` **axis_value** = ``0.0`` :ref:`🔗<class_InputEventJoypadMotion_property_axis_value>`

.. rst-class:: classref-property-setget

- |void| **set_axis_value**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_axis_value**\ (\ )

Vị trí hiện tại của cần điều khiển trên trục đã cho. Giá trị nằm trong khoảng từ ``-1.0`` đến ``1.0``. Giá trị ``0`` nghĩa là trục đang ở vị trí nghỉ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
