:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRDpadBindingModifier.xml.

.. _class_OpenXRDpadBindingModifier:

OpenXRDpadBindingModifier
=========================

**Kế thừa:** :ref:`OpenXRIPBindingModifier<class_OpenXRIPBindingModifier>` **<** :ref:`OpenXRBindingModifier<class_OpenXRBindingModifier>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

DPad binding modifier chuyển đổi đầu vào của một axis thành đầu ra dpad.

.. rst-class:: classref-introduction-group

Mô tả
-----

DPad binding modifier chuyển đổi đầu vào của một axis thành đầu ra dpad, mô phỏng một DPad. Các input path mới cho từng hướng dpad sẽ được thêm vào interaction profile. Khi được liên kết với các action, tính năng mô phỏng DPad sẽ được kích hoạt. Bạn **không nên** kết hợp đầu vào dpad với đầu vào thông thường trong cùng một action set cho cùng một control; điều này sẽ khiến OpenXR trả về lỗi khi các suggested binding được gửi đi.

Xem `XR_EXT_dpad_binding <https://registry.khronos.org/OpenXR/specs/1.1/html/xrspec.html#XR_EXT_dpad_binding>`__ để biết chi tiết chuyên sâu.

\ **Lưu ý:** Nếu extension DPad binding modifier được bật, tất cả dpad binding path sẽ có sẵn trong action map. Việc thêm modifier vào interaction profile cho phép bạn tùy chỉnh thêm hành vi.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`OpenXRActionSet<class_OpenXRActionSet>`   | :ref:`action_set<class_OpenXRDpadBindingModifier_property_action_set>`                 |               |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                       | :ref:`center_region<class_OpenXRDpadBindingModifier_property_center_region>`           | ``0.1``       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`String<class_String>`                     | :ref:`input_path<class_OpenXRDpadBindingModifier_property_input_path>`                 | ``""``        |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_sticky<class_OpenXRDpadBindingModifier_property_is_sticky>`                   | ``false``     |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` | :ref:`off_haptic<class_OpenXRDpadBindingModifier_property_off_haptic>`                 |               |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` | :ref:`on_haptic<class_OpenXRDpadBindingModifier_property_on_haptic>`                   |               |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                       | :ref:`threshold<class_OpenXRDpadBindingModifier_property_threshold>`                   | ``0.6``       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                       | :ref:`threshold_released<class_OpenXRDpadBindingModifier_property_threshold_released>` | ``0.4``       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                       | :ref:`wedge_angle<class_OpenXRDpadBindingModifier_property_wedge_angle>`               | ``1.5707964`` |
   +-------------------------------------------------+----------------------------------------------------------------------------------------+---------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRDpadBindingModifier_property_action_set:

.. rst-class:: classref-property

:ref:`OpenXRActionSet<class_OpenXRActionSet>` **action_set** :ref:`🔗<class_OpenXRDpadBindingModifier_property_action_set>`

.. rst-class:: classref-property-setget

- |void| **set_action_set**\ (\ value\: :ref:`OpenXRActionSet<class_OpenXRActionSet>`\ ) - :ref:`OpenXRActionSet<class_OpenXRActionSet>` **get_action_set**\ (\ )

Action set mà dpad binding modifier này hoạt động trên đó.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_center_region:

.. rst-class:: classref-property

:ref:`float<class_float>` **center_region** = ``0.1`` :ref:`🔗<class_OpenXRDpadBindingModifier_property_center_region>`

.. rst-class:: classref-property-setget

- |void| **set_center_region**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_center_region**\ (\ )

Vùng trung tâm mà tại đó vị trí trung tâm của dpad trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_input_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **input_path** = ``""`` :ref:`🔗<class_OpenXRDpadBindingModifier_property_input_path>`

.. rst-class:: classref-property-setget

- |void| **set_input_path**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_input_path**\ (\ )

Input path cho dpad binding modifier này.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_is_sticky:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **is_sticky** = ``false`` :ref:`🔗<class_OpenXRDpadBindingModifier_property_is_sticky>`

.. rst-class:: classref-property-setget

- |void| **set_is_sticky**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_is_sticky**\ (\ )

Nếu ``false``, khi joystick đi vào một vùng dpad mới, giá trị này trở thành ``true``.

Nếu ``true``, khi joystick vẫn ở trong vùng dpad đang hoạt động, giá trị này vẫn là ``true`` ngay cả khi chồng lấn với một vùng khác.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_off_haptic:

.. rst-class:: classref-property

:ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **off_haptic** :ref:`🔗<class_OpenXRDpadBindingModifier_property_off_haptic>`

.. rst-class:: classref-property-setget

- |void| **set_off_haptic**\ (\ value\: :ref:`OpenXRHapticBase<class_OpenXRHapticBase>`\ ) - :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **get_off_haptic**\ (\ )

Xung haptic sẽ phát ra khi người dùng nhả đầu vào.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_on_haptic:

.. rst-class:: classref-property

:ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **on_haptic** :ref:`🔗<class_OpenXRDpadBindingModifier_property_on_haptic>`

.. rst-class:: classref-property-setget

- |void| **set_on_haptic**\ (\ value\: :ref:`OpenXRHapticBase<class_OpenXRHapticBase>`\ ) - :ref:`OpenXRHapticBase<class_OpenXRHapticBase>` **get_on_haptic**\ (\ )

Xung haptic sẽ phát ra khi người dùng nhấn đầu vào.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **threshold** = ``0.6`` :ref:`🔗<class_OpenXRDpadBindingModifier_property_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_threshold**\ (\ )

Khi giá trị đầu vào bằng hoặc lớn hơn giá trị này, dpad theo hướng đó sẽ trở thành ``true``. Nó giữ nguyên ``true`` cho đến khi giảm xuống dưới giá trị :ref:`threshold_released<class_OpenXRDpadBindingModifier_property_threshold_released>`.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_threshold_released:

.. rst-class:: classref-property

:ref:`float<class_float>` **threshold_released** = ``0.4`` :ref:`🔗<class_OpenXRDpadBindingModifier_property_threshold_released>`

.. rst-class:: classref-property-setget

- |void| **set_threshold_released**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_threshold_released**\ (\ )

Khi giá trị đầu vào giảm xuống dưới giá trị này, đầu ra sẽ trở thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRDpadBindingModifier_property_wedge_angle:

.. rst-class:: classref-property

:ref:`float<class_float>` **wedge_angle** = ``1.5707964`` :ref:`🔗<class_OpenXRDpadBindingModifier_property_wedge_angle>`

.. rst-class:: classref-property-setget

- |void| **set_wedge_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_wedge_angle**\ (\ )

Góc của mỗi hình quạt xác định 4 hướng của dpad được mô phỏng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
