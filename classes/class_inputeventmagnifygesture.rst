:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventMagnifyGesture.xml.

.. _class_InputEventMagnifyGesture:

InputEventMagnifyGesture
========================

**Kế thừa:** :ref:`InputEventGesture<class_InputEventGesture>` **<** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một cử chỉ cảm ứng phóng to.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu hệ số của một cử chỉ cảm ứng phóng to. Cử chỉ này thường được thực hiện khi người dùng chụm các ngón tay trên màn hình cảm ứng và được dùng để phóng to/thu nhỏ.

\ **Lưu ý:** Trên Android, yêu cầu phải bật thiết lập dự án :ref:`ProjectSettings.input_devices/pointing/android/enable_pan_and_scale_gestures<class_ProjectSettings_property_input_devices/pointing/android/enable_pan_and_scale_gestures>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`factor<class_InputEventMagnifyGesture_property_factor>` | ``1.0`` |
   +---------------------------+---------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventMagnifyGesture_property_factor:

.. rst-class:: classref-property

:ref:`float<class_float>` **factor** = ``1.0`` :ref:`🔗<class_InputEventMagnifyGesture_property_factor>`

.. rst-class:: classref-property-setget

- |void| **set_factor**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_factor**\ (\ )

Giá trị của sự kiện (hay delta). Giá trị này càng gần ``1.0`` thì cử chỉ được thực hiện càng chậm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
