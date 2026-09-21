:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRAnalogThresholdModifier.xml.

.. _class_OpenXRAnalogThresholdModifier:

OpenXRAnalogThresholdModifier
=============================

**Kế thừa:** :ref:`OpenXRActionBindingModifier<class_OpenXRActionBindingModifier>` **<** :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Modifier liên kết ngưỡng analog có thể chuyển đổi đầu vào float thành đầu vào boolean với các ngưỡng được chỉ định.

.. rst-class:: classref-introduction-group

Mô tả
-----

Modifier liên kết ngưỡng analog có thể chuyển đổi đầu vào float thành đầu vào boolean với các ngưỡng được chỉ định.

Xem `XR_VALVE_analog_threshold <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_VALVE_analog_threshold>`__ để biết thông tin chi tiết.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+----------------------------------------------------------------------------------+---------+
   | :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` | :ref:`off_haptic<class_OpenXRAnalogThresholdModifier_property_off_haptic>`       |         |
   +-------------------------------------------------+----------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                       | :ref:`off_threshold<class_OpenXRAnalogThresholdModifier_property_off_threshold>` | ``0.4`` |
   +-------------------------------------------------+----------------------------------------------------------------------------------+---------+
   | :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` | :ref:`on_haptic<class_OpenXRAnalogThresholdModifier_property_on_haptic>`         |         |
   +-------------------------------------------------+----------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                       | :ref:`on_threshold<class_OpenXRAnalogThresholdModifier_property_on_threshold>`   | ``0.6`` |
   +-------------------------------------------------+----------------------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRAnalogThresholdModifier_property_off_haptic:

.. rst-class:: classref-property

:ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **off_haptic** :ref:`🔗<class_OpenXRAnalogThresholdModifier_property_off_haptic>`

.. rst-class:: classref-property-setget

- |void| **set_off_haptic**\ (\ value\: :ref:`OpenXRHapticBase<class_OpenXRHapticBase>`\ ) - :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **get_off_haptic**\ (\ )

Xung haptic sẽ phát ra khi người dùng nhả đầu vào.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRAnalogThresholdModifier_property_off_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **off_threshold** = ``0.4`` :ref:`🔗<class_OpenXRAnalogThresholdModifier_property_off_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_off_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_off_threshold**\ (\ )

Khi giá trị đầu vào giảm xuống dưới mức này, đầu ra sẽ trở thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRAnalogThresholdModifier_property_on_haptic:

.. rst-class:: classref-property

:ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **on_haptic** :ref:`🔗<class_OpenXRAnalogThresholdModifier_property_on_haptic>`

.. rst-class:: classref-property-setget

- |void| **set_on_haptic**\ (\ value\: :ref:`OpenXRHapticBase<class_OpenXRHapticBase>`\ ) - :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **get_on_haptic**\ (\ )

Xung haptic sẽ phát ra khi người dùng nhấn đầu vào.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRAnalogThresholdModifier_property_on_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **on_threshold** = ``0.6`` :ref:`🔗<class_OpenXRAnalogThresholdModifier_property_on_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_on_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_on_threshold**\ (\ )

Khi giá trị đầu vào bằng hoặc lớn hơn giá trị này, đầu ra sẽ trở thành ``true``. Đầu ra vẫn là ``true`` cho đến khi giảm xuống dưới giá trị :ref:`off_threshold<class_OpenXRAnalogThresholdModifier_property_off_threshold>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
