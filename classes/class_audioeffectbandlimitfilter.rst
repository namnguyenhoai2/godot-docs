:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectBandLimitFilter.xml.

.. _class_AudioEffectBandLimitFilter:

AudioEffectBandLimitFilter
==========================

**Kế thừa:** :ref:`AudioEffectFilter<class_AudioEffectFilter>` **<** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm bộ lọc giới hạn dải tần vào một audio bus.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bộ lọc "giới hạn dải tần" làm suy giảm các tần số tại :ref:`AudioEffectFilter.cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>`, đồng thời cho phép các tần số nằm ngoài ngưỡng tần số đi qua mà không thay đổi. Đây là phiên bản rộng hơn và yếu hơn của :ref:`AudioEffectNotchFilter<class_AudioEffectNotchFilter>`, đồng thời ngược lại với :ref:`AudioEffectBandPassFilter<class_AudioEffectBandPassFilter>`.

Có thể sử dụng bộ lọc này để tạo thêm khoảng trống cho các âm thanh khác phát ở tần số đó.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- :doc:`Audio effects <../tutorials/audio/audio_effects>`

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
