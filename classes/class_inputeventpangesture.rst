:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/InputEventPanGesture.xml.

.. _class_InputEventPanGesture:

InputEventPanGesture
====================

**Kế thừa:** :ref:`InputEventGesture<class_InputEventGesture>` **<** :ref:`InputEventWithModifiers<class_InputEventWithModifiers>` **<** :ref:`InputEventFromWindow<class_InputEventFromWindow>` **<** :ref:`InputEvent<class_InputEvent>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đại diện cho một cử chỉ vuốt để di chuyển.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lưu trữ thông tin về các cử chỉ vuốt để di chuyển. Cử chỉ này được thực hiện khi người dùng vuốt màn hình cảm ứng bằng hai ngón tay. Cử chỉ này thường được dùng để di chuyển/cuộn.

\ **Lưu ý:** Trên Android, cần bật thiết lập project :ref:`ProjectSettings.input_devices/pointing/android/enable_pan_and_scale_gestures<class_ProjectSettings_property_input_devices/pointing/android/enable_pan_and_scale_gestures>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng InputEvent <../tutorials/inputs/inputevent>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`delta<class_InputEventPanGesture_property_delta>` | ``Vector2(0, 0)`` |
   +-------------------------------+---------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_InputEventPanGesture_property_delta:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **delta** = ``Vector2(0, 0)`` :ref:`🔗<class_InputEventPanGesture_property_delta>`

.. rst-class:: classref-property-setget

- |void| **set_delta**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_delta**\ (\ )

Lượng di chuyển kể từ sự kiện pan trước đó.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
