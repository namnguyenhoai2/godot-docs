:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffect.xml.

.. _class_AudioEffect:

AudioEffect
===========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioEffectAmplify<class_AudioEffectAmplify>`, :ref:`AudioEffectCapture<class_AudioEffectCapture>`, :ref:`AudioEffectChorus<class_AudioEffectChorus>`, :ref:`AudioEffectCompressor<class_AudioEffectCompressor>`, :ref:`AudioEffectDelay<class_AudioEffectDelay>`, :ref:`AudioEffectDistortion<class_AudioEffectDistortion>`, :ref:`AudioEffectEQ<class_AudioEffectEQ>`, :ref:`AudioEffectFilter<class_AudioEffectFilter>`, :ref:`AudioEffectHardLimiter<class_AudioEffectHardLimiter>`, :ref:`AudioEffectLimiter<class_AudioEffectLimiter>`, :ref:`AudioEffectPanner<class_AudioEffectPanner>`, :ref:`AudioEffectPhaser<class_AudioEffectPhaser>`, :ref:`AudioEffectPitchShift<class_AudioEffectPitchShift>`, :ref:`AudioEffectRecord<class_AudioEffectRecord>`, :ref:`AudioEffectReverb<class_AudioEffectReverb>`, :ref:`AudioEffectSpectrumAnalyzer<class_AudioEffectSpectrumAnalyzer>`, :ref:`AudioEffectStereoEnhance<class_AudioEffectStereoEnhance>`

Lớp cơ sở cho các resource hiệu ứng âm thanh.

.. rst-class:: classref-introduction-group

Mô tả
-----

:ref:`Resource<class_Resource>` cơ sở cho mọi hiệu ứng âm thanh. Trong editor, có thể thêm hiệu ứng âm thanh vào bố cục bus hiện tại thông qua bảng Audio. Khi chạy, cũng có thể thao tác với các hiệu ứng âm thanh thông qua :ref:`AudioServer.add_bus_effect()<class_AudioServer_method_add_bus_effect>`, :ref:`AudioServer.remove_bus_effect()<class_AudioServer_method_remove_bus_effect>` và :ref:`AudioServer.get_bus_effect()<class_AudioServer_method_get_bus_effect>`.

Khi được áp dụng trên một bus, hiệu ứng âm thanh sẽ tạo một :ref:`AudioEffectInstance<class_AudioEffectInstance>` tương ứng. Instance này chịu trách nhiệm trực tiếp trong việc thao tác với âm thanh, dựa trên các thuộc tính của hiệu ứng âm thanh ban đầu.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

- `Audio Microphone Record Demo <https://godotengine.org/asset-library/asset/2760>`__

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`AudioEffectInstance<class_AudioEffectInstance>` | :ref:`_instantiate<class_AudioEffect_private_method__instantiate>`\ (\ ) |virtual| |required| |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioEffect_private_method__instantiate:

.. rst-class:: classref-method

:ref:`AudioEffectInstance<class_AudioEffectInstance>` **_instantiate**\ (\ ) |virtual| |required| :ref:`🔗<class_AudioEffect_private_method__instantiate>`

Ghi đè phương thức này để tùy chỉnh :ref:`AudioEffectInstance<class_AudioEffectInstance>` được tạo khi hiệu ứng này được áp dụng trên một bus trong bảng Audio của editor hoặc thông qua :ref:`AudioServer.add_bus_effect()<class_AudioServer_method_add_bus_effect>`.

::

    extends AudioEffect

    @export var strength = 4.0

    func _instantiate():
        var effect = CustomAudioEffectInstance.new()
        effect.base = self

        return effect

\ **Lưu ý:** Bạn nên giữ tham chiếu đến **AudioEffect** ban đầu trong instance mới. Tùy thuộc vào cách triển khai, điều này cho phép instance của hiệu ứng lắng nghe các thay đổi khi chạy và được sửa đổi tương ứng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
