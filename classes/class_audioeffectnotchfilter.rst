:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioEffectNotchFilter.xml.

.. _class_AudioEffectNotchFilter:

AudioEffectNotchFilter
======================

**Kế thừa:** :ref:`AudioEffectFilter<class_AudioEffectFilter>` **<** :ref:`AudioEffect<class_AudioEffect>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Thêm một bộ lọc notch vào bus âm thanh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Bộ lọc "notch" làm suy giảm các tần số tại :ref:`AudioEffectFilter.cutoff_hz<class_AudioEffectFilter_property_cutoff_hz>` và cho phép các tần số nằm ngoài ngưỡng tần số đi qua mà không thay đổi. Đây là phiên bản hẹp hơn và mạnh hơn của :ref:`AudioEffectBandLimitFilter<class_AudioEffectBandLimitFilter>`, đồng thời là đối lập của :ref:`AudioEffectBandPassFilter<class_AudioEffectBandPassFilter>`.

Bộ lọc này có thể được dùng để tạo thêm không gian cho các âm thanh khác phát ở tần số đó. Do làm suy giảm tần số mạnh đến mức nào, nó cũng có thể được dùng để loại bỏ hoàn toàn các tần số không mong muốn.

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
