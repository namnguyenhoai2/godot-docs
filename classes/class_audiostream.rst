:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStream.xml.

.. _class_AudioStream:

AudioStream
===========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioStreamGenerator<class_AudioStreamGenerator>`, :ref:`AudioStreamInteractive<class_AudioStreamInteractive>`, :ref:`AudioStreamMicrophone<class_AudioStreamMicrophone>`, :ref:`AudioStreamMP3<class_AudioStreamMP3>`, :ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>`, :ref:`AudioStreamPlaylist<class_AudioStreamPlaylist>`, :ref:`AudioStreamPolyphonic<class_AudioStreamPolyphonic>`, :ref:`AudioStreamRandomizer<class_AudioStreamRandomizer>`, :ref:`AudioStreamSynchronized<class_AudioStreamSynchronized>`, :ref:`AudioStreamWAV<class_AudioStreamWAV>`

Lớp cơ sở cho các audio stream.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho các audio stream. Audio stream được dùng để phát hiệu ứng âm thanh và nhạc, đồng thời hỗ trợ các định dạng tệp WAV (thông qua :ref:`AudioStreamWAV<class_AudioStreamWAV>`), Ogg (thông qua :ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>`) và MP3 (thông qua :ref:`AudioStreamMP3<class_AudioStreamMP3>`).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- `Audio Generator Demo <https://godotengine.org/asset-library/asset/2759>`__

- `Audio Microphone Record Demo <https://godotengine.org/asset-library/asset/2760>`__

- `Audio Spectrum Visualizer Demo <https://godotengine.org/asset-library/asset/2762>`__

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_bar_beats<class_AudioStream_private_method__get_bar_beats>`\ (\ ) |virtual| |const|                          |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`_get_beat_count<class_AudioStream_private_method__get_beat_count>`\ (\ ) |virtual| |const|                        |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`_get_bpm<class_AudioStream_private_method__get_bpm>`\ (\ ) |virtual| |const|                                      |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`_get_length<class_AudioStream_private_method__get_length>`\ (\ ) |virtual| |const|                                |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_parameter_list<class_AudioStream_private_method__get_parameter_list>`\ (\ ) |virtual| |const|                |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_get_stream_name<class_AudioStream_private_method__get_stream_name>`\ (\ ) |virtual| |const|                      |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`_get_tags<class_AudioStream_private_method__get_tags>`\ (\ ) |virtual| |const|                                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_has_loop<class_AudioStream_private_method__has_loop>`\ (\ ) |virtual| |const|                                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamPlayback<class_AudioStreamPlayback>`            | :ref:`_instantiate_playback<class_AudioStream_private_method__instantiate_playback>`\ (\ ) |virtual| |required| |const| |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_is_monophonic<class_AudioStream_private_method__is_monophonic>`\ (\ ) |virtual| |const|                          |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`can_be_sampled<class_AudioStream_method_can_be_sampled>`\ (\ ) |const|                                            |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioSample<class_AudioSample>`                            | :ref:`generate_sample<class_AudioStream_method_generate_sample>`\ (\ ) |const|                                          |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_length<class_AudioStream_method_get_length>`\ (\ ) |const|                                                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamPlayback<class_AudioStreamPlayback>`            | :ref:`instantiate_playback<class_AudioStream_method_instantiate_playback>`\ (\ )                                        |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_meta_stream<class_AudioStream_method_is_meta_stream>`\ (\ ) |const|                                            |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_monophonic<class_AudioStream_method_is_monophonic>`\ (\ ) |const|                                              |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_AudioStream_signal_parameter_list_changed:

.. rst-class:: classref-signal

**parameter_list_changed**\ (\ ) :ref:`🔗<class_AudioStream_signal_parameter_list_changed>`

Signal được phát để thông báo khi danh sách tham số thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_AudioStream_private_method__get_bar_beats:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_bar_beats**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_bar_beats>`

Ghi đè phương thức này để trả về số phách của stream này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__get_beat_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_beat_count**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_beat_count>`

Phương thức có thể ghi đè. Nên trả về tổng số phách của audio stream này. Được engine sử dụng để xác định vị trí của từng phách.

Lý tưởng nhất là giá trị trả về nên dựa trên sample rate của stream (:ref:`AudioStreamWAV.mix_rate<class_AudioStreamWAV_property_mix_rate>`, chẳng hạn).

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__get_bpm:

.. rst-class:: classref-method

:ref:`float<class_float>` **_get_bpm**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_bpm>`

Phương thức có thể ghi đè. Nên trả về tempo của audio stream này, tính bằng số phách mỗi phút (BPM). Được engine sử dụng để xác định vị trí của từng phách.

Lý tưởng nhất là giá trị trả về nên dựa trên sample rate của stream (:ref:`AudioStreamWAV.mix_rate<class_AudioStreamWAV_property_mix_rate>`, chẳng hạn).

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__get_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **_get_length**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_length>`

Ghi đè phương thức này để tùy chỉnh giá trị trả về của :ref:`get_length()<class_AudioStream_method_get_length>`. Nên trả về độ dài của audio stream này, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__get_parameter_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_parameter_list**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_parameter_list>`

Trả về các tham số có thể điều khiển của stream này. Mảng này chứa các dictionary với định dạng mô tả property info (xem :ref:`Object.get_property_list()<class_Object_method_get_property_list>`). Ngoài ra, giá trị mặc định của tham số này phải được thêm vào mỗi dictionary trong trường "default_value".

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__get_stream_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **_get_stream_name**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_stream_name>`

Ghi đè phương thức này để tùy chỉnh tên được gán cho audio stream này. Engine không sử dụng tên này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__get_tags:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **_get_tags**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__get_tags>`

Ghi đè phương thức này để tùy chỉnh các tag cho audio stream này. Nên trả về một :ref:`Dictionary<class_Dictionary>` gồm các chuỗi, với tag là key và nội dung của tag là value.

Các tag thường được sử dụng gồm ``title``, ``artist``, ``album``, ``tracknumber`` và ``date``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__has_loop:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_has_loop**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__has_loop>`

Ghi đè phương thức này để trả về ``true`` nếu stream này có vòng lặp.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__instantiate_playback:

.. rst-class:: classref-method

:ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **_instantiate_playback**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_AudioStream_private_method__instantiate_playback>`

Ghi đè phương thức này để tùy chỉnh giá trị trả về của :ref:`instantiate_playback()<class_AudioStream_method_instantiate_playback>`. Nên trả về một :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` mới được tạo khi stream được phát (chẳng hạn bởi một :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_private_method__is_monophonic:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_monophonic**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStream_private_method__is_monophonic>`

Ghi đè phương thức này để tùy chỉnh giá trị trả về của :ref:`is_monophonic()<class_AudioStream_method_is_monophonic>`. Nên trả về ``true`` nếu audio stream này chỉ hỗ trợ một channel.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_method_can_be_sampled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_be_sampled**\ (\ ) |const| :ref:`🔗<class_AudioStream_method_can_be_sampled>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Cho biết **AudioStream** hiện tại có thể được sử dụng làm sample hay không. Chỉ các static stream mới có thể được lấy mẫu.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_method_generate_sample:

.. rst-class:: classref-method

:ref:`AudioSample<class_AudioSample>` **generate_sample**\ (\ ) |const| :ref:`🔗<class_AudioStream_method_generate_sample>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Tạo một :ref:`AudioSample<class_AudioSample>` dựa trên stream hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_method_get_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_length**\ (\ ) |const| :ref:`🔗<class_AudioStream_method_get_length>`

Trả về độ dài của audio stream tính bằng giây. Nếu stream này là một :ref:`AudioStreamRandomizer<class_AudioStreamRandomizer>`, trả về độ dài của stream được phát gần nhất. Nếu stream này có độ dài vô hạn (chẳng hạn như :ref:`AudioStreamGenerator<class_AudioStreamGenerator>` và :ref:`AudioStreamMicrophone<class_AudioStreamMicrophone>`), trả về ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_method_instantiate_playback:

.. rst-class:: classref-method

:ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **instantiate_playback**\ (\ ) :ref:`🔗<class_AudioStream_method_instantiate_playback>`

Trả về một :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` mới được tạo, dùng để phát audio stream này. Hữu ích khi bạn muốn mở rộng :ref:`_instantiate_playback()<class_AudioStream_private_method__instantiate_playback>` nhưng gọi :ref:`instantiate_playback()<class_AudioStream_method_instantiate_playback>` từ một AudioStream subresource được lưu trữ bên trong. Bạn có thể tìm thấy ví dụ về việc này trong mã nguồn của ``AudioStreamRandomPitch::instantiate_playback``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_method_is_meta_stream:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_meta_stream**\ (\ ) |const| :ref:`🔗<class_AudioStream_method_is_meta_stream>`

Trả về ``true`` nếu stream là một tập hợp các stream khác, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStream_method_is_monophonic:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_monophonic**\ (\ ) |const| :ref:`🔗<class_AudioStream_method_is_monophonic>`

Trả về ``true`` nếu audio stream này chỉ hỗ trợ một channel (*đơn âm*), hoặc ``false`` nếu audio stream hỗ trợ từ hai channel trở lên (*đa âm*).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
