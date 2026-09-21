:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectHighPassFilter.xml.

.. _class_AudioEffectHighPassFilter:

AudioEffectHighPassFilter
=========================

**Kế thừa:** :ref:`AudioEffectFilter<class_AudioEffectFilter>` **<** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm một bộ lọc thông cao vào một audio bus.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bộ lọc "thông cao" làm suy giảm các tần số thấp hơn :ref:`AudioEffectFilter.cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>` và cho phép các tần số cao hơn đi qua mà không thay đổi.

Bộ lọc này có thể được dùng để loại bỏ "độ mạnh" khỏi âm thanh, đồng thời tạo không gian ở dải tần thấp cho âm bass và âm thanh va chạm.

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
