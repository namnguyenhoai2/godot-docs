:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectDelay.xml.

.. _class_AudioEffectDelay:

AudioEffectDelay
================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng delay âm thanh vào một audio bus.

Mô phỏng tiếng vọng bằng cách phát lại audio đầu vào sau một khoảng thời gian.

.. rst-class:: classref-introduction-group

Mô tả
-----

Hiệu ứng "delay" phát lại tín hiệu audio đầu vào sau một khoảng thời gian. Mỗi lần lặp được gọi là một "delay tap" hoặc đơn giản là "tap". Các delay tap có thể được phát lại nhiều lần để tạo ra âm thanh của tiếng vọng lặp lại và suy giảm dần. Hiệu ứng delay có thể tạo ra từ tiếng vọng nhẹ đến sự hòa trộn rõ rệt giữa âm thanh trước đó và âm thanh mới.

Xem thêm :ref:`AudioEffectReverb<class_AudioEffectReverb>` để biết về tiếng vọng mờ, liên tục.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`dry<class_AudioEffectDelay_property_dry>`                             | ``1.0``     |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`bool<class_bool>`   | :ref:`feedback_active<class_AudioEffectDelay_property_feedback_active>`     | ``false``   |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`feedback_delay_ms<class_AudioEffectDelay_property_feedback_delay_ms>` | ``340.0``   |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`feedback_level_db<class_AudioEffectDelay_property_feedback_level_db>` | ``-6.0``    |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`feedback_lowpass<class_AudioEffectDelay_property_feedback_lowpass>`   | ``16000.0`` |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`bool<class_bool>`   | :ref:`tap1_active<class_AudioEffectDelay_property_tap1_active>`             | ``true``    |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`tap1_delay_ms<class_AudioEffectDelay_property_tap1_delay_ms>`         | ``250.0``   |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`tap1_level_db<class_AudioEffectDelay_property_tap1_level_db>`         | ``-6.0``    |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`tap1_pan<class_AudioEffectDelay_property_tap1_pan>`                   | ``0.2``     |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`bool<class_bool>`   | :ref:`tap2_active<class_AudioEffectDelay_property_tap2_active>`             | ``true``    |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`tap2_delay_ms<class_AudioEffectDelay_property_tap2_delay_ms>`         | ``500.0``   |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`tap2_level_db<class_AudioEffectDelay_property_tap2_level_db>`         | ``-12.0``   |
   +---------------------------+-----------------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`tap2_pan<class_AudioEffectDelay_property_tap2_pan>`                   | ``-0.4``    |
   +---------------------------+-----------------------------------------------------------------------------+-------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectDelay_property_dry:

.. rst-class:: classref-property

:ref:`float<class_float>` **dry** = ``1.0`` :ref:`🔗<class_AudioEffectDelay_property_dry>`

.. rst-class:: classref-property-setget

- |void| **set_dry**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_dry**\ (\ )

Tỷ lệ âm lượng của audio gốc. Giá trị có thể nằm trong khoảng từ 0 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_feedback_active:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **feedback_active** = ``false`` :ref:`🔗<class_AudioEffectDelay_property_feedback_active>`

.. rst-class:: classref-property-setget

- |void| **set_feedback_active**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_feedback_active**\ (\ )

Nếu ``true``, feedback được bật và các tap sẽ lặp lại sau khi được phát.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_feedback_delay_ms:

.. rst-class:: classref-property

:ref:`float<class_float>` **feedback_delay_ms** = ``340.0`` :ref:`🔗<class_AudioEffectDelay_property_feedback_delay_ms>`

.. rst-class:: classref-property-setget

- |void| **set_feedback_delay_ms**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_feedback_delay_ms**\ (\ )

Thời gian delay của feedback tính bằng mili giây. Giá trị có thể nằm trong khoảng từ 0 đến 1500.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_feedback_level_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **feedback_level_db** = ``-6.0`` :ref:`🔗<class_AudioEffectDelay_property_feedback_level_db>`

.. rst-class:: classref-property-setget

- |void| **set_feedback_level_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_feedback_level_db**\ (\ )

Gain của feedback, tính bằng dB. Giá trị có thể nằm trong khoảng từ -60 đến 0.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_feedback_lowpass:

.. rst-class:: classref-property

:ref:`float<class_float>` **feedback_lowpass** = ``16000.0`` :ref:`🔗<class_AudioEffectDelay_property_feedback_lowpass>`

.. rst-class:: classref-property-setget

- |void| **set_feedback_lowpass**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_feedback_lowpass**\ (\ )

Bộ lọc low-pass cho feedback, tính bằng Hz. Các tần số cao hơn giá trị này sẽ bị lọc. Giá trị có thể nằm trong khoảng từ 1 đến 16000.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap1_active:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **tap1_active** = ``true`` :ref:`🔗<class_AudioEffectDelay_property_tap1_active>`

.. rst-class:: classref-property-setget

- |void| **set_tap1_active**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_tap1_active**\ (\ )

Nếu ``true``, tap đầu tiên sẽ được bật.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap1_delay_ms:

.. rst-class:: classref-property

:ref:`float<class_float>` **tap1_delay_ms** = ``250.0`` :ref:`🔗<class_AudioEffectDelay_property_tap1_delay_ms>`

.. rst-class:: classref-property-setget

- |void| **set_tap1_delay_ms**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_tap1_delay_ms**\ (\ )

Thời gian delay của tap đầu tiên tính bằng mili giây, so với audio gốc. Giá trị có thể nằm trong khoảng từ 0 đến 1500.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap1_level_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **tap1_level_db** = ``-6.0`` :ref:`🔗<class_AudioEffectDelay_property_tap1_level_db>`

.. rst-class:: classref-property-setget

- |void| **set_tap1_level_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_tap1_level_db**\ (\ )

Gain của tap đầu tiên, tính bằng dB. Giá trị có thể nằm trong khoảng từ -60 đến 0.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap1_pan:

.. rst-class:: classref-property

:ref:`float<class_float>` **tap1_pan** = ``0.2`` :ref:`🔗<class_AudioEffectDelay_property_tap1_pan>`

.. rst-class:: classref-property-setget

- |void| **set_tap1_pan**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_tap1_pan**\ (\ )

Vị trí pan của tap đầu tiên. Giá trị âm sẽ pan âm thanh sang trái, giá trị dương sẽ pan sang phải. Giá trị có thể nằm trong khoảng từ -1 đến 1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap2_active:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **tap2_active** = ``true`` :ref:`🔗<class_AudioEffectDelay_property_tap2_active>`

.. rst-class:: classref-property-setget

- |void| **set_tap2_active**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_tap2_active**\ (\ )

Nếu ``true``, tap thứ hai sẽ được bật.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap2_delay_ms:

.. rst-class:: classref-property

:ref:`float<class_float>` **tap2_delay_ms** = ``500.0`` :ref:`🔗<class_AudioEffectDelay_property_tap2_delay_ms>`

.. rst-class:: classref-property-setget

- |void| **set_tap2_delay_ms**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_tap2_delay_ms**\ (\ )

Thời gian delay của tap thứ hai tính bằng mili giây, so với audio gốc. Giá trị có thể nằm trong khoảng từ 0 đến 1500.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap2_level_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **tap2_level_db** = ``-12.0`` :ref:`🔗<class_AudioEffectDelay_property_tap2_level_db>`

.. rst-class:: classref-property-setget

- |void| **set_tap2_level_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_tap2_level_db**\ (\ )

Gain của tap thứ hai, tính bằng dB. Giá trị có thể nằm trong khoảng từ -60 đến 0.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectDelay_property_tap2_pan:

.. rst-class:: classref-property

:ref:`float<class_float>` **tap2_pan** = ``-0.4`` :ref:`🔗<class_AudioEffectDelay_property_tap2_pan>`

.. rst-class:: classref-property-setget

- |void| **set_tap2_pan**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_tap2_pan**\ (\ )

Vị trí pan của tap thứ hai. Giá trị âm sẽ pan âm thanh sang trái, giá trị dương sẽ pan sang phải. Giá trị có thể nằm trong khoảng từ -1 đến 1.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
