:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPlayback.xml.

.. _class_AudioStreamPlayback:

AudioStreamPlayback
===================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioStreamPlaybackInteractive<class_AudioStreamPlaybackInteractive>`, :ref:`AudioStreamPlaybackPlaylist<class_AudioStreamPlaybackPlaylist>`, :ref:`AudioStreamPlaybackPolyphonic<class_AudioStreamPlaybackPolyphonic>`, :ref:`AudioStreamPlaybackResampled<class_AudioStreamPlaybackResampled>`, :ref:`AudioStreamPlaybackSynchronized<class_AudioStreamPlaybackSynchronized>`

Lớp meta để phát âm thanh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Có thể phát, lặp, tạm dừng và tua qua âm thanh. Xem :ref:`AudioStream<class_AudioStream>` và :ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>` để biết cách sử dụng.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Audio Generator Demo <https://godotengine.org/asset-library/asset/2759>`__

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`_get_loop_count<class_AudioStreamPlayback_private_method__get_loop_count>`\ (\ ) |virtual| |const|                                                                                |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                         | :ref:`_get_parameter<class_AudioStreamPlayback_private_method__get_parameter>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |virtual| |const|                                      |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`_get_playback_position<class_AudioStreamPlayback_private_method__get_playback_position>`\ (\ ) |virtual| |required| |const|                                                       |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`_is_playing<class_AudioStreamPlayback_private_method__is_playing>`\ (\ ) |virtual| |required| |const|                                                                             |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`_mix<class_AudioStreamPlayback_private_method__mix>`\ (\ buffer\: ``AudioFrame*``, rate_scale\: :ref:`float<class_float>`, frames\: :ref:`int<class_int>`\ ) |virtual| |required| |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`_seek<class_AudioStreamPlayback_private_method__seek>`\ (\ position\: :ref:`float<class_float>`\ ) |virtual|                                                                      |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`_set_parameter<class_AudioStreamPlayback_private_method__set_parameter>`\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) |virtual|       |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`_start<class_AudioStreamPlayback_private_method__start>`\ (\ from_pos\: :ref:`float<class_float>`\ ) |virtual| |required|                                                         |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`_stop<class_AudioStreamPlayback_private_method__stop>`\ (\ ) |virtual| |required|                                                                                                 |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`_tag_used_streams<class_AudioStreamPlayback_private_method__tag_used_streams>`\ (\ ) |virtual|                                                                                    |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_loop_count<class_AudioStreamPlayback_method_get_loop_count>`\ (\ ) |const|                                                                                                    |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_playback_position<class_AudioStreamPlayback_method_get_playback_position>`\ (\ ) |const|                                                                                      |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioSamplePlayback<class_AudioSamplePlayback>` | :ref:`get_sample_playback<class_AudioStreamPlayback_method_get_sample_playback>`\ (\ ) |const|                                                                                          |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_playing<class_AudioStreamPlayback_method_is_playing>`\ (\ ) |const|                                                                                                            |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`   | :ref:`mix_audio<class_AudioStreamPlayback_method_mix_audio>`\ (\ rate_scale\: :ref:`float<class_float>`, frames\: :ref:`int<class_int>`\ )                                              |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`seek<class_AudioStreamPlayback_method_seek>`\ (\ time\: :ref:`float<class_float>` = 0.0\ )                                                                                        |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_sample_playback<class_AudioStreamPlayback_method_set_sample_playback>`\ (\ playback_sample\: :ref:`AudioSamplePlayback<class_AudioSamplePlayback>`\ )                         |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`start<class_AudioStreamPlayback_method_start>`\ (\ from_pos\: :ref:`float<class_float>` = 0.0\ )                                                                                  |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`stop<class_AudioStreamPlayback_method_stop>`\ (\ )                                                                                                                                |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamPlayback_private_method__get_loop_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_loop_count**\ (\ ) |virtual| |const| :ref:`🔗<class_AudioStreamPlayback_private_method__get_loop_count>`

Phương thức có thể ghi đè. Phương thức này phải trả về số lần audio stream đã lặp. Hầu hết các playback tích hợp sẵn luôn trả về ``0``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__get_parameter:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get_parameter**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |virtual| |const| :ref:`🔗<class_AudioStreamPlayback_private_method__get_parameter>`

Trả về giá trị hiện tại của một playback parameter theo tên (xem :ref:`AudioStream._get_parameter_list()<class_AudioStream_private_method__get_parameter_list>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__get_playback_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **_get_playback_position**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_AudioStreamPlayback_private_method__get_playback_position>`

Phương thức có thể ghi đè. Phương thức này phải trả về tiến trình hiện tại dọc theo audio stream, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__is_playing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_playing**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_AudioStreamPlayback_private_method__is_playing>`

Phương thức có thể ghi đè. Phương thức này phải trả về ``true`` nếu playback này đang hoạt động và đang phát audio stream.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__mix:

.. rst-class:: classref-method

:ref:`int<class_int>` **_mix**\ (\ buffer\: ``AudioFrame*``, rate_scale\: :ref:`float<class_float>`, frames\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_AudioStreamPlayback_private_method__mix>`

Ghi đè phương thức này để tùy chỉnh cách audio stream được mix. Phương thức này được gọi ngay cả khi playback không hoạt động.

\ **Lưu ý:** Việc ghi đè phương thức này trong GDScript hoặc C# không có tác dụng. Chỉ GDExtension mới có thể tận dụng phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__seek:

.. rst-class:: classref-method

|void| **_seek**\ (\ position\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_AudioStreamPlayback_private_method__seek>`

Ghi đè phương thức này để tùy chỉnh điều xảy ra khi tua audio stream đến ``position`` đã cho, chẳng hạn bằng cách gọi :ref:`AudioStreamPlayer.seek()<class_AudioStreamPlayer_method_seek>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__set_parameter:

.. rst-class:: classref-method

|void| **_set_parameter**\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) |virtual| :ref:`🔗<class_AudioStreamPlayback_private_method__set_parameter>`

Đặt giá trị hiện tại của một playback parameter theo tên (xem :ref:`AudioStream._get_parameter_list()<class_AudioStream_private_method__get_parameter_list>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__start:

.. rst-class:: classref-method

|void| **_start**\ (\ from_pos\: :ref:`float<class_float>`\ ) |virtual| |required| :ref:`🔗<class_AudioStreamPlayback_private_method__start>`

Ghi đè phương thức này để tùy chỉnh điều xảy ra khi playback bắt đầu tại vị trí đã cho, chẳng hạn bằng cách gọi :ref:`AudioStreamPlayer.play()<class_AudioStreamPlayer_method_play>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__stop:

.. rst-class:: classref-method

|void| **_stop**\ (\ ) |virtual| |required| :ref:`🔗<class_AudioStreamPlayback_private_method__stop>`

Ghi đè phương thức này để tùy chỉnh điều xảy ra khi playback dừng, chẳng hạn bằng cách gọi :ref:`AudioStreamPlayer.stop()<class_AudioStreamPlayer_method_stop>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_private_method__tag_used_streams:

.. rst-class:: classref-method

|void| **_tag_used_streams**\ (\ ) |virtual| :ref:`🔗<class_AudioStreamPlayback_private_method__tag_used_streams>`

Phương thức có thể ghi đè. Được gọi mỗi khi audio stream được mix nếu playback đang hoạt động và :ref:`AudioServer.set_enable_tagging_used_audio_streams()<class_AudioServer_method_set_enable_tagging_used_audio_streams>` đã được đặt thành ``true``. Các editor plugin có thể sử dụng phương thức này để "gắn thẻ" vị trí hiện tại dọc theo audio stream và hiển thị vị trí đó trong bản xem trước.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_get_loop_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_loop_count**\ (\ ) |const| :ref:`🔗<class_AudioStreamPlayback_method_get_loop_count>`

Trả về số lần stream đã lặp.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_get_playback_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_playback_position**\ (\ ) |const| :ref:`🔗<class_AudioStreamPlayback_method_get_playback_position>`

Trả về vị trí hiện tại trong stream, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_get_sample_playback:

.. rst-class:: classref-method

:ref:`AudioSamplePlayback<class_AudioSamplePlayback>` **get_sample_playback**\ (\ ) |const| :ref:`🔗<class_AudioStreamPlayback_method_get_sample_playback>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Trả về :ref:`AudioSamplePlayback<class_AudioSamplePlayback>` được liên kết với **AudioStreamPlayback** này để phát audio sample của stream này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_is_playing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_playing**\ (\ ) |const| :ref:`🔗<class_AudioStreamPlayback_method_is_playing>`

Trả về ``true`` nếu stream đang phát.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_mix_audio:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **mix_audio**\ (\ rate_scale\: :ref:`float<class_float>`, frames\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioStreamPlayback_method_mix_audio>`

Mix tối đa ``frames`` âm thanh từ stream, bắt đầu từ vị trí hiện tại, với tốc độ ``rate_scale``, đồng thời tiến stream về phía trước.

Trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` trong đó mỗi phần tử chứa các mức âm lượng của kênh trái và phải của mỗi frame.

\ **Lưu ý:** Có thể trả về ít frame hơn số lượng được yêu cầu; hãy đảm bảo sử dụng kích thước của giá trị trả về.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_seek:

.. rst-class:: classref-method

|void| **seek**\ (\ time\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_AudioStreamPlayback_method_seek>`

Tua stream đến ``time`` đã cho, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_set_sample_playback:

.. rst-class:: classref-method

|void| **set_sample_playback**\ (\ playback_sample\: :ref:`AudioSamplePlayback<class_AudioSamplePlayback>`\ ) :ref:`🔗<class_AudioStreamPlayback_method_set_sample_playback>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Liên kết :ref:`AudioSamplePlayback<class_AudioSamplePlayback>` với **AudioStreamPlayback** này để phát audio sample của stream này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_start:

.. rst-class:: classref-method

|void| **start**\ (\ from_pos\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_AudioStreamPlayback_method_start>`

Bắt đầu stream từ ``from_pos`` đã cho, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayback_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AudioStreamPlayback_method_stop>`

Dừng stream.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
