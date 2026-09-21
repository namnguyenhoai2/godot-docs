:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectHardLimiter.xml.

.. _class_AudioEffectHardLimiter:

AudioEffectHardLimiter
======================

**Kế thừa:** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm hiệu ứng limiter vào một audio bus.

Ngăn các tín hiệu âm thanh vượt quá mức âm lượng được chỉ định.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một "limiter" ngăn các tín hiệu âm thanh vượt quá ngưỡng âm lượng nhất định, tính bằng dB. Hard limiter dự đoán các đỉnh âm lượng và sẽ áp dụng giảm gain một cách mượt mà khi một đỉnh vượt qua mức trần để ngăn clipping. Nó giữ nguyên dạng sóng và ngăn dạng sóng vượt qua mức trần. Bạn nên thêm một limiter vào bus Master như một biện pháp an toàn để ngăn các đỉnh âm lượng đột ngột xuất hiện, đồng thời ngăn hiện tượng méo do clipping khi âm lượng vượt quá 0 dB.

Nếu muốn clipping, hãy cân nhắc :ref:`AudioEffectDistortion.MODE_CLIP<class_AudioEffectDistortion_constant_MODE_CLIP>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+-----------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`ceiling_db<class_AudioEffectHardLimiter_property_ceiling_db>`   | ``-0.3`` |
   +---------------------------+-----------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`pre_gain_db<class_AudioEffectHardLimiter_property_pre_gain_db>` | ``0.0``  |
   +---------------------------+-----------------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`release<class_AudioEffectHardLimiter_property_release>`         | ``0.1``  |
   +---------------------------+-----------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioEffectHardLimiter_property_ceiling_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **ceiling_db** = ``-0.3`` :ref:`🔗<class_AudioEffectHardLimiter_property_ceiling_db>`

.. rst-class:: classref-property-setget

- |void| **set_ceiling_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_ceiling_db**\ (\ )

Giá trị tối đa được phép của dạng sóng, tính bằng dB. Giá trị này có thể nằm trong khoảng từ -24 đến 0.

Giá trị mặc định -0.3 ngăn các đỉnh giữa các mẫu (inter-sample peaks, ISP) có khả năng vượt quá 0 dB, điều này có thể gây méo nhẹ trên một số phần cứng cũ.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectHardLimiter_property_pre_gain_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **pre_gain_db** = ``0.0`` :ref:`🔗<class_AudioEffectHardLimiter_property_pre_gain_db>`

.. rst-class:: classref-property-setget

- |void| **set_pre_gain_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pre_gain_db**\ (\ )

Gain trước khi limiting, tính bằng dB. Giá trị có thể nằm trong khoảng từ -24 đến 24.

.. rst-class:: classref-item-separator

----

.. _class_AudioEffectHardLimiter_property_release:

.. rst-class:: classref-property

:ref:`float<class_float>` **release** = ``0.1`` :ref:`🔗<class_AudioEffectHardLimiter_property_release>`

.. rst-class:: classref-property-setget

- |void| **set_release**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_release**\ (\ )

Thời gian tính bằng giây để quá trình giảm gain được release hoàn toàn. Giá trị có thể nằm trong khoảng từ 0.01 đến 3.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
