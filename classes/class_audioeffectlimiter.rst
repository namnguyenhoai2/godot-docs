:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectLimiter.xml.

.. _class_AudioEffectLimiter:

AudioEffectLimiter
==================

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`AudioEffectHardLimiter<class_AudioEffectHardLimiter>`.

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng âm thanh limiter soft-clip vào một audio bus.

.. rst-class:: classref-introduction-group

Mô tả
-----

"Limiter" là một hiệu ứng âm thanh được thiết kế để ngăn tín hiệu âm thanh vượt quá mức ngưỡng âm lượng được chỉ định, và thường hoạt động bằng cách giảm âm lượng hoặc thực hiện soft-clipping cho âm thanh. Luôn khuyến nghị thêm một limiter vào bus Master để ngăn clipping khi âm lượng vượt quá 0 dB.

Soft clipping bắt đầu giảm nhẹ các đỉnh thấp hơn một chút so với mức ngưỡng âm lượng và tăng dần tác động khi âm lượng đầu vào tăng, nhờ đó mức ngưỡng không bao giờ bị vượt quá.

Nếu muốn hard clipping, hãy cân nhắc :ref:`AudioEffectDistortion.MODE_CLIP<class_AudioEffectDistortion_constant_MODE_CLIP>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`ceiling_db<class_AudioEffectLimiter_property_ceiling_db>`           | ``-0.1`` |
   +---------------------------+---------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`soft_clip_db<class_AudioEffectLimiter_property_soft_clip_db>`       | ``2.0``  |
   +---------------------------+---------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`soft_clip_ratio<class_AudioEffectLimiter_property_soft_clip_ratio>` | ``10.0`` |
   +---------------------------+---------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`threshold_db<class_AudioEffectLimiter_property_threshold_db>`       | ``0.0``  |
   +---------------------------+---------------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectLimiter_property_ceiling_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **ceiling_db** = ``-0.1`` :ref:`🔗<class_AudioEffectLimiter_property_ceiling_db>`

.. rst-class:: classref-property-setget

- |void| **set_ceiling_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_ceiling_db**\ (\ )

Giá trị tối đa được cho phép của dạng sóng, tính bằng dB. Giá trị có thể nằm trong khoảng từ -20 đến -0.1.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectLimiter_property_soft_clip_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **soft_clip_db** = ``2.0`` :ref:`🔗<class_AudioEffectLimiter_property_soft_clip_db>`

.. rst-class:: classref-property-setget

- |void| **set_soft_clip_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_soft_clip_db**\ (\ )

Điều chỉnh âm lượng của các sóng đã được giới hạn, tính bằng dB. Giá trị có thể nằm trong khoảng từ 0 đến 6.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectLimiter_property_soft_clip_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **soft_clip_ratio** = ``10.0`` :ref:`🔗<class_AudioEffectLimiter_property_soft_clip_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_soft_clip_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_soft_clip_ratio**\ (\ )

Thuộc tính này không có tác dụng đối với âm thanh. Thay vào đó, hãy sử dụng :ref:`AudioEffectHardLimiter<class_AudioEffectHardLimiter>`, vì hiệu ứng Limiter này đã lỗi thời.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectLimiter_property_threshold_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **threshold_db** = ``0.0`` :ref:`🔗<class_AudioEffectLimiter_property_threshold_db>`

.. rst-class:: classref-property-setget

- |void| **set_threshold_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_threshold_db**\ (\ )

Mức ngưỡng âm lượng từ đó limiter bắt đầu hoạt động, tính bằng dB. Giá trị có thể nằm trong khoảng từ -30 đến 0.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
