:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPlaybackResampled.xml.

.. _class_AudioStreamPlaybackResampled:

AudioStreamPlaybackResampled
============================

**Kế thừa:** :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioStreamGeneratorPlayback<class_AudioStreamGeneratorPlayback>`, :ref:`AudioStreamPlaybackOggVorbis<class_AudioStreamPlaybackOggVorbis>`

Playback class used for resampled :ref:`AudioStream<class_AudioStream>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp playback được dùng để trộn các mẫu âm thanh của :ref:`AudioStream<class_AudioStream>` vào :ref:`AudioServer.get_mix_rate()<class_AudioServer_method_get_mix_rate>` bằng phép nội suy cubic.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`_get_stream_sampling_rate<class_AudioStreamPlaybackResampled_private_method__get_stream_sampling_rate>`\ (\ ) |virtual| |required| |const|                                      |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`     | :ref:`_mix_resampled<class_AudioStreamPlaybackResampled_private_method__mix_resampled>`\ (\ dst_buffer\: ``AudioFrame*``, frame_count\: :ref:`int<class_int>`\ ) |virtual| |required| |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                    | :ref:`begin_resample<class_AudioStreamPlaybackResampled_method_begin_resample>`\ (\ )                                                                                                 |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamPlaybackResampled_private_method__get_stream_sampling_rate:

.. rst-class:: classref-method

:ref:`float<class_float>` **_get_stream_sampling_rate**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_AudioStreamPlaybackResampled_private_method__get_stream_sampling_rate>`

Trả về sample rate của :ref:`AudioStream<class_AudioStream>`, tính bằng Hz. Được dùng để thực hiện resampling.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaybackResampled_private_method__mix_resampled:

.. rst-class:: classref-method

:ref:`int<class_int>` **_mix_resampled**\ (\ dst_buffer\: ``AudioFrame*``, frame_count\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_AudioStreamPlaybackResampled_private_method__mix_resampled>`

Được :ref:`begin_resample()<class_AudioStreamPlaybackResampled_method_begin_resample>` gọi để trộn :ref:`AudioStream<class_AudioStream>` vào :ref:`AudioServer.get_mix_rate()<class_AudioServer_method_get_mix_rate>`. Sử dụng :ref:`_get_stream_sampling_rate()<class_AudioStreamPlaybackResampled_private_method__get_stream_sampling_rate>` làm sample rate nguồn. Trả về số frame đã trộn.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaybackResampled_method_begin_resample:

.. rst-class:: classref-method

|void| **begin_resample**\ (\ ) :ref:`🔗<class_AudioStreamPlaybackResampled_method_begin_resample>`

Được gọi khi :ref:`AudioStream<class_AudioStream>` được phát. Xóa lịch sử nội suy cubic và bắt đầu trộn bằng cách gọi :ref:`_mix_resampled()<class_AudioStreamPlaybackResampled_private_method__mix_resampled>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
