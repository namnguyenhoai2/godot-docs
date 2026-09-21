:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectCompressor.xml.

.. _class_AudioEffectCompressor:

AudioEffectCompressor
=====================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm một hiệu ứng âm thanh compressor giảm mức vào một audio bus.

Cho phép kiểm soát dynamic range thông qua ngưỡng âm lượng và các điều khiển thời gian.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một "compressor" làm giảm âm lượng của âm thanh khi âm lượng đó vượt quá một mức ngưỡng nhất định.

Một compressor có thể được sử dụng cho nhiều mục đích trong một bản mix:

- Để nén toàn bộ âm lượng trong Master bus (mặc dù :ref:`AudioEffectHardLimiter<class_AudioEffectHardLimiter>` có lẽ phù hợp hơn).

- Để đảm bảo sự cân bằng của các audio clip giọng nói.

- Để sidechain, sử dụng một bus khác làm trigger. Cách này làm giảm âm lượng của bus mà nó được gắn vào bằng cách sử dụng âm lượng từ một audio bus khác để phát hiện ngưỡng. Kỹ thuật này thường được dùng trong việc mix video game để giảm âm lượng của nhạc và SFX trong khi có giọng nói. Hiệu ứng này còn được gọi là "ducking".

- Để làm nổi bật các transient bằng cách sử dụng attack dài, cho phép âm thanh vượt quá mức ngưỡng âm lượng trong một khoảng thời gian ngắn trước khi nén chúng. Cách này có thể được dùng để làm cho SFX mạnh và rõ hơn.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`attack_us<class_AudioEffectCompressor_property_attack_us>`   | ``20.0``  |
   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`gain<class_AudioEffectCompressor_property_gain>`             | ``0.0``   |
   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`mix<class_AudioEffectCompressor_property_mix>`               | ``1.0``   |
   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`ratio<class_AudioEffectCompressor_property_ratio>`           | ``4.0``   |
   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`release_ms<class_AudioEffectCompressor_property_release_ms>` | ``250.0`` |
   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`StringName<class_StringName>` | :ref:`sidechain<class_AudioEffectCompressor_property_sidechain>`   | ``&""``   |
   +-------------------------------------+--------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`           | :ref:`threshold<class_AudioEffectCompressor_property_threshold>`   | ``0.0``   |
   +-------------------------------------+--------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectCompressor_property_attack_us:

.. rst-class:: classref-property

:ref:`float<class_float>` **attack_us** = ``20.0`` :ref:`🔗<class_AudioEffectCompressor_property_attack_us>`

.. rst-class:: classref-property-setget

- |void| **set_attack_us**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_attack_us**\ (\ )

Thời gian phản ứng của compressor khi âm thanh vượt quá mức ngưỡng âm lượng, tính bằng microsecond. Giá trị có thể nằm trong khoảng từ 20 đến 2000.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCompressor_property_gain:

.. rst-class:: classref-property

:ref:`float<class_float>` **gain** = ``0.0`` :ref:`🔗<class_AudioEffectCompressor_property_gain>`

.. rst-class:: classref-property-setget

- |void| **set_gain**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gain**\ (\ )

Gain của tín hiệu âm thanh, tính bằng dB. Giá trị có thể nằm trong khoảng từ -20 đến 20.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCompressor_property_mix:

.. rst-class:: classref-property

:ref:`float<class_float>` **mix** = ``1.0`` :ref:`🔗<class_AudioEffectCompressor_property_mix>`

.. rst-class:: classref-property-setget

- |void| **set_mix**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mix**\ (\ )

Cân bằng giữa âm thanh gốc và âm thanh đã nén. Giá trị có thể nằm trong khoảng từ 0 (hoàn toàn dry) đến 1 (hoàn toàn wet).

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCompressor_property_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **ratio** = ``4.0`` :ref:`🔗<class_AudioEffectCompressor_property_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_ratio**\ (\ )

Mức độ nén được áp dụng cho âm thanh sau khi âm thanh vượt qua mức ngưỡng âm lượng. Ratio càng cao thì mức nén áp dụng cho các tín hiệu âm thanh vượt qua mức ngưỡng âm lượng càng mạnh. Giá trị có thể nằm trong khoảng từ 1 đến 48.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCompressor_property_release_ms:

.. rst-class:: classref-property

:ref:`float<class_float>` **release_ms** = ``250.0`` :ref:`🔗<class_AudioEffectCompressor_property_release_ms>`

.. rst-class:: classref-property-setget

- |void| **set_release_ms**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_release_ms**\ (\ )

Thời gian trễ của compressor trước khi ngừng giảm âm lượng sau khi âm lượng giảm xuống dưới mức ngưỡng âm lượng, tính bằng millisecond. Giá trị có thể nằm trong khoảng từ 20 đến 2000.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCompressor_property_sidechain:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **sidechain** = ``&""`` :ref:`🔗<class_AudioEffectCompressor_property_sidechain>`

.. rst-class:: classref-property-setget

- |void| **set_sidechain**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_sidechain**\ (\ )

Audio bus được sử dụng để phát hiện ngưỡng âm lượng.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectCompressor_property_threshold:

.. rst-class:: classref-property

:ref:`float<class_float>` **threshold** = ``0.0`` :ref:`🔗<class_AudioEffectCompressor_property_threshold>`

.. rst-class:: classref-property-setget

- |void| **set_threshold**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_threshold**\ (\ )

Mức âm lượng mà trên đó compression được áp dụng cho âm thanh, tính bằng dB. Giá trị có thể nằm trong khoảng từ -60 đến 0.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
