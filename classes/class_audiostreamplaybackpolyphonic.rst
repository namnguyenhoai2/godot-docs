:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPlaybackPolyphonic.xml.

.. _class_AudioStreamPlaybackPolyphonic:

AudioStreamPlaybackPolyphonic
=============================

**Kế thừa:** :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Instance phát lại cho :ref:`AudioStreamPolyphonic<class_AudioStreamPolyphonic>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Instance phát lại cho :ref:`AudioStreamPolyphonic<class_AudioStreamPolyphonic>`. Sau khi thiết lập thuộc tính ``stream`` của :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`, :ref:`AudioStreamPlayer2D<class_AudioStreamPlayer2D>` hoặc :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>`, có thể lấy instance phát lại bằng cách gọi các phương thức :ref:`AudioStreamPlayer.get_stream_playback()<class_AudioStreamPlayer_method_get_stream_playback>`, :ref:`AudioStreamPlayer2D.get_stream_playback()<class_AudioStreamPlayer2D_method_get_stream_playback>` hoặc :ref:`AudioStreamPlayer3D.get_stream_playback()<class_AudioStreamPlayer3D_method_get_stream_playback>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_stream_playing<class_AudioStreamPlaybackPolyphonic_method_is_stream_playing>`\ (\ stream\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                                                                   |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | :ref:`play_stream<class_AudioStreamPlaybackPolyphonic_method_play_stream>`\ (\ stream\: :ref:`AudioStream<class_AudioStream>`, from_offset\: :ref:`float<class_float>` = 0, volume_db\: :ref:`float<class_float>` = 0, pitch_scale\: :ref:`float<class_float>` = 1.0, playback_type\: :ref:`PlaybackType<enum_AudioServer_PlaybackType>` = 0, bus\: :ref:`StringName<class_StringName>` = &"Master"\ ) |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_stream_pitch_scale<class_AudioStreamPlaybackPolyphonic_method_set_stream_pitch_scale>`\ (\ stream\: :ref:`int<class_int>`, pitch_scale\: :ref:`float<class_float>`\ )                                                                                                                                                                                                                        |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_stream_volume<class_AudioStreamPlaybackPolyphonic_method_set_stream_volume>`\ (\ stream\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ )                                                                                                                                                                                                                                    |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`stop_stream<class_AudioStreamPlaybackPolyphonic_method_stop_stream>`\ (\ stream\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                                                                       |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_AudioStreamPlaybackPolyphonic_constant_INVALID_ID:

.. rst-class:: classref-constant

**INVALID_ID** = ``-1`` :ref:`🔗<class_AudioStreamPlaybackPolyphonic_constant_INVALID_ID>`

Được :ref:`play_stream()<class_AudioStreamPlaybackPolyphonic_method_play_stream>` trả về trong trường hợp không thể cấp phát một stream để phát lại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_AudioStreamPlaybackPolyphonic_method_is_stream_playing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_stream_playing**\ (\ stream\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamPlaybackPolyphonic_method_is_stream_playing>`

Trả về ``true`` nếu stream được liên kết với ID số nguyên đã cho vẫn đang phát. Kiểm tra :ref:`play_stream()<class_AudioStreamPlaybackPolyphonic_method_play_stream>` để biết thông tin về thời điểm ID này trở nên không hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaybackPolyphonic_method_play_stream:

.. rst-class:: classref-method

:ref:`int<class_int>` **play_stream**\ (\ stream\: :ref:`AudioStream<class_AudioStream>`, from_offset\: :ref:`float<class_float>` = 0, volume_db\: :ref:`float<class_float>` = 0, pitch_scale\: :ref:`float<class_float>` = 1.0, playback_type\: :ref:`PlaybackType<enum_AudioServer_PlaybackType>` = 0, bus\: :ref:`StringName<class_StringName>` = &"Master"\ ) :ref:`🔗<class_AudioStreamPlaybackPolyphonic_method_play_stream>`

Phát một :ref:`AudioStream<class_AudioStream>` tại offset, âm lượng, hệ số scale cao độ, kiểu phát lại và bus đã cho. Việc phát lại bắt đầu ngay lập tức.

Giá trị trả về là một ID số nguyên duy nhất được liên kết với stream phát lại này và có thể được dùng để điều khiển stream.

ID này trở nên không hợp lệ khi stream kết thúc (nếu không lặp), khi **AudioStreamPlaybackPolyphonic** bị dừng hoặc khi :ref:`stop_stream()<class_AudioStreamPlaybackPolyphonic_method_stop_stream>` được gọi.

Hàm này trả về :ref:`INVALID_ID<class_AudioStreamPlaybackPolyphonic_constant_INVALID_ID>` nếu số stream đang phát hiện tại bằng :ref:`AudioStreamPolyphonic.polyphony<class_AudioStreamPolyphonic_property_polyphony>`. Nếu cần số lượng polyphony tối đa cao hơn, hãy tăng giá trị này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaybackPolyphonic_method_set_stream_pitch_scale:

.. rst-class:: classref-method

|void| **set_stream_pitch_scale**\ (\ stream\: :ref:`int<class_int>`, pitch_scale\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamPlaybackPolyphonic_method_set_stream_pitch_scale>`

Thay đổi hệ số scale cao độ của stream. Đối số ``stream`` là một ID số nguyên do :ref:`play_stream()<class_AudioStreamPlaybackPolyphonic_method_play_stream>` trả về.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaybackPolyphonic_method_set_stream_volume:

.. rst-class:: classref-method

|void| **set_stream_volume**\ (\ stream\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamPlaybackPolyphonic_method_set_stream_volume>`

Thay đổi âm lượng stream (tính bằng dB). Đối số ``stream`` là một ID số nguyên do :ref:`play_stream()<class_AudioStreamPlaybackPolyphonic_method_play_stream>` trả về.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaybackPolyphonic_method_stop_stream:

.. rst-class:: classref-method

|void| **stop_stream**\ (\ stream\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioStreamPlaybackPolyphonic_method_stop_stream>`

Dừng một stream. Đối số ``stream`` là một ID số nguyên do :ref:`play_stream()<class_AudioStreamPlaybackPolyphonic_method_play_stream>` trả về; ID này trở nên không hợp lệ sau khi gọi hàm này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
