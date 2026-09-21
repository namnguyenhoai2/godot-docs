:github_url: hide

.. meta::
	:keywords: sound, music, song

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPlayer.xml.

.. _class_AudioStreamPlayer:

AudioStreamPlayer
=================

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node dùng để phát âm thanh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node **AudioStreamPlayer** phát một audio stream không theo vị trí. Node này phù hợp cho giao diện người dùng, menu hoặc nhạc nền.

Để sử dụng node này, cần đặt :ref:`stream<class_AudioStreamPlayer_property_stream>` thành một resource :ref:`AudioStream<class_AudioStream>` hợp lệ. Node cũng hỗ trợ phát nhiều âm thanh cùng lúc, xem :ref:`max_polyphony<class_AudioStreamPlayer_property_max_polyphony>`.

Nếu cần phát âm thanh tại một vị trí cụ thể, hãy sử dụng :ref:`AudioStreamPlayer2D<class_AudioStreamPlayer2D>` hoặc :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>` thay thế.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

- `Audio Device Changer Demo <https://godotengine.org/asset-library/asset/2758>`__

- `Audio Generator Demo <https://godotengine.org/asset-library/asset/2759>`__

- `Audio Microphone Record Demo <https://godotengine.org/asset-library/asset/2760>`__

- `Audio Spectrum Visualizer Demo <https://godotengine.org/asset-library/asset/2762>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                            | :ref:`autoplay<class_AudioStreamPlayer_property_autoplay>`           | ``false``     |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`StringName<class_StringName>`                | :ref:`bus<class_AudioStreamPlayer_property_bus>`                     | ``&"Master"`` |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`                              | :ref:`max_polyphony<class_AudioStreamPlayer_property_max_polyphony>` | ``1``         |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>` | :ref:`mix_target<class_AudioStreamPlayer_property_mix_target>`       | ``0``         |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`pitch_scale<class_AudioStreamPlayer_property_pitch_scale>`     | ``1.0``       |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`PlaybackType<enum_AudioServer_PlaybackType>` | :ref:`playback_type<class_AudioStreamPlayer_property_playback_type>` | ``0``         |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                            | :ref:`playing<class_AudioStreamPlayer_property_playing>`             | ``false``     |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`AudioStream<class_AudioStream>`              | :ref:`stream<class_AudioStreamPlayer_property_stream>`               |               |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                            | :ref:`stream_paused<class_AudioStreamPlayer_property_stream_paused>` | ``false``     |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`volume_db<class_AudioStreamPlayer_property_volume_db>`         | ``0.0``       |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`volume_linear<class_AudioStreamPlayer_property_volume_linear>` |               |
   +----------------------------------------------------+----------------------------------------------------------------------+---------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_playback_position<class_AudioStreamPlayer_method_get_playback_position>`\ (\ )                |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` | :ref:`get_stream_playback<class_AudioStreamPlayer_method_get_stream_playback>`\ (\ )                    |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`has_stream_playback<class_AudioStreamPlayer_method_has_stream_playback>`\ (\ )                    |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`play<class_AudioStreamPlayer_method_play>`\ (\ from_position\: :ref:`float<class_float>` = 0.0\ ) |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`seek<class_AudioStreamPlayer_method_seek>`\ (\ to_position\: :ref:`float<class_float>`\ )         |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`stop<class_AudioStreamPlayer_method_stop>`\ (\ )                                                  |
   +-------------------------------------------------------+---------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_AudioStreamPlayer_signal_finished:

.. rst-class:: classref-signal

**finished**\ (\ ) :ref:`🔗<class_AudioStreamPlayer_signal_finished>`

Được phát khi âm thanh phát xong mà không bị gián đoạn. Signal này *không* được phát khi gọi :ref:`stop()<class_AudioStreamPlayer_method_stop>`, hoặc khi thoát khỏi tree trong lúc âm thanh đang phát.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumeration
-----------

.. _enum_AudioStreamPlayer_MixTarget:

.. rst-class:: classref-enumeration

enum **MixTarget**: :ref:`🔗<enum_AudioStreamPlayer_MixTarget>`

.. _class_AudioStreamPlayer_constant_MIX_TARGET_STEREO:

.. rst-class:: classref-enumeration-constant

:ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>` **MIX_TARGET_STEREO** = ``0``

Âm thanh sẽ chỉ được phát trên channel đầu tiên. Đây là giá trị mặc định.

.. _class_AudioStreamPlayer_constant_MIX_TARGET_SURROUND:

.. rst-class:: classref-enumeration-constant

:ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>` **MIX_TARGET_SURROUND** = ``1``

Âm thanh sẽ được phát trên tất cả các channel surround.

.. _class_AudioStreamPlayer_constant_MIX_TARGET_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>` **MIX_TARGET_CENTER** = ``2``

Âm thanh sẽ được phát trên channel thứ hai, thường là channel trung tâm.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamPlayer_property_autoplay:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **autoplay** = ``false`` :ref:`🔗<class_AudioStreamPlayer_property_autoplay>`

.. rst-class:: classref-property-setget

- |void| **set_autoplay**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_autoplay_enabled**\ (\ )

Nếu ``true``, node này sẽ gọi :ref:`play()<class_AudioStreamPlayer_method_play>` khi đi vào tree.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_bus:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **bus** = ``&"Master"`` :ref:`🔗<class_AudioStreamPlayer_property_bus>`

.. rst-class:: classref-property-setget

- |void| **set_bus**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_bus**\ (\ )

Tên bus đích. Tất cả âm thanh từ node này sẽ được phát trên bus này.

\ **Lưu ý:** Trong runtime, nếu không tồn tại bus có tên đã cho, tất cả âm thanh sẽ chuyển sang ``"Master"``. Xem thêm :ref:`AudioServer.get_bus_name()<class_AudioServer_method_get_bus_name>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_max_polyphony:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_polyphony** = ``1`` :ref:`🔗<class_AudioStreamPlayer_property_max_polyphony>`

.. rst-class:: classref-property-setget

- |void| **set_max_polyphony**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_polyphony**\ (\ )

Số lượng âm thanh tối đa mà node này có thể phát cùng lúc. Việc gọi :ref:`play()<class_AudioStreamPlayer_method_play>` sau khi đạt đến giá trị này sẽ ngắt các âm thanh cũ nhất.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_mix_target:

.. rst-class:: classref-property

:ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>` **mix_target** = ``0`` :ref:`🔗<class_AudioStreamPlayer_property_mix_target>`

.. rst-class:: classref-property-setget

- |void| **set_mix_target**\ (\ value\: :ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>`\ ) - :ref:`MixTarget<enum_AudioStreamPlayer_MixTarget>` **get_mix_target**\ (\ )

Các channel đích của quá trình mix. Không có tác dụng khi phát hiện có từ hai loa trở xuống (xem :ref:`SpeakerMode<enum_AudioServer_SpeakerMode>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_pitch_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **pitch_scale** = ``1.0`` :ref:`🔗<class_AudioStreamPlayer_property_pitch_scale>`

.. rst-class:: classref-property-setget

- |void| **set_pitch_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pitch_scale**\ (\ )

Cao độ và nhịp độ của âm thanh, dưới dạng hệ số nhân của sample rate của :ref:`stream<class_AudioStreamPlayer_property_stream>`. Giá trị ``2.0`` sẽ tăng gấp đôi cao độ của âm thanh, còn giá trị ``0.5`` sẽ giảm một nửa cao độ.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_playback_type:

.. rst-class:: classref-property

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **playback_type** = ``0`` :ref:`🔗<class_AudioStreamPlayer_property_playback_type>`

.. rst-class:: classref-property-setget

- |void| **set_playback_type**\ (\ value\: :ref:`PlaybackType<enum_AudioServer_PlaybackType>`\ ) - :ref:`PlaybackType<enum_AudioServer_PlaybackType>` **get_playback_type**\ (\ )

**Thử nghiệm:** Thuộc tính này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Loại playback của stream player. Nếu được đặt khác giá trị mặc định, nó sẽ buộc sử dụng loại playback đó.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_playing:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **playing** = ``false`` :ref:`🔗<class_AudioStreamPlayer_property_playing>`

.. rst-class:: classref-property-setget

- |void| **set_playing**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_playing**\ (\ )

Nếu ``true``, node này đang phát âm thanh. Việc đặt thuộc tính này có tác dụng giống như :ref:`play()<class_AudioStreamPlayer_method_play>` và :ref:`stop()<class_AudioStreamPlayer_method_stop>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_stream:

.. rst-class:: classref-property

:ref:`AudioStream<class_AudioStream>` **stream** :ref:`🔗<class_AudioStreamPlayer_property_stream>`

.. rst-class:: classref-property-setget

- |void| **set_stream**\ (\ value\: :ref:`AudioStream<class_AudioStream>`\ ) - :ref:`AudioStream<class_AudioStream>` **get_stream**\ (\ )

Resource :ref:`AudioStream<class_AudioStream>` sẽ được phát. Việc đặt thuộc tính này sẽ dừng tất cả âm thanh đang phát. Nếu để trống, **AudioStreamPlayer** sẽ không hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_stream_paused:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **stream_paused** = ``false`` :ref:`🔗<class_AudioStreamPlayer_property_stream_paused>`

.. rst-class:: classref-property-setget

- |void| **set_stream_paused**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_stream_paused**\ (\ )

Nếu ``true``, các âm thanh sẽ bị tạm dừng. Đặt :ref:`stream_paused<class_AudioStreamPlayer_property_stream_paused>` thành ``false`` sẽ tiếp tục tất cả âm thanh.

\ **Lưu ý:** Thuộc tính này tự động thay đổi khi thoát khỏi hoặc đi vào tree, hoặc khi node này bị tạm dừng (xem :ref:`Node.process_mode<class_Node_property_process_mode>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_volume_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_db** = ``0.0`` :ref:`🔗<class_AudioStreamPlayer_property_volume_db>`

.. rst-class:: classref-property-setget

- |void| **set_volume_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_db**\ (\ )

Âm lượng của âm thanh, tính bằng decibel. Đây là độ lệch so với âm lượng của :ref:`stream<class_AudioStreamPlayer_property_stream>`.

\ **Lưu ý:** Để chuyển đổi giữa decibel và năng lượng tuyến tính (như hầu hết thanh trượt âm lượng thực hiện), hãy sử dụng :ref:`volume_linear<class_AudioStreamPlayer_property_volume_linear>`, hoặc :ref:`@GlobalScope.db_to_linear()<class_@GlobalScope_method_db_to_linear>` và :ref:`@GlobalScope.linear_to_db()<class_@GlobalScope_method_linear_to_db>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_property_volume_linear:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_linear** :ref:`🔗<class_AudioStreamPlayer_property_volume_linear>`

.. rst-class:: classref-property-setget

- |void| **set_volume_linear**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_linear**\ (\ )

Âm lượng của âm thanh, dưới dạng giá trị tuyến tính.

\ **Lưu ý:** Member này sửa đổi :ref:`volume_db<class_AudioStreamPlayer_property_volume_db>` để thuận tiện. Giá trị trả về tương đương với kết quả của :ref:`@GlobalScope.db_to_linear()<class_@GlobalScope_method_db_to_linear>` trên :ref:`volume_db<class_AudioStreamPlayer_property_volume_db>`. Việc đặt member này tương đương với việc đặt :ref:`volume_db<class_AudioStreamPlayer_property_volume_db>` thành kết quả của :ref:`@GlobalScope.linear_to_db()<class_@GlobalScope_method_linear_to_db>` trên một giá trị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamPlayer_method_get_playback_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_playback_position**\ (\ ) :ref:`🔗<class_AudioStreamPlayer_method_get_playback_position>`

Trả về vị trí trong :ref:`AudioStream<class_AudioStream>` của âm thanh mới nhất, tính bằng giây. Trả về ``0.0`` nếu không có âm thanh nào đang phát.

\ **Lưu ý:** Vị trí không phải lúc nào cũng chính xác, vì :ref:`AudioServer<class_AudioServer>` không mix âm thanh ở mỗi frame được xử lý. Để có kết quả chính xác hơn, hãy cộng :ref:`AudioServer.get_time_since_last_mix()<class_AudioServer_method_get_time_since_last_mix>` vào vị trí được trả về.

\ **Lưu ý:** Phương thức này luôn trả về ``0.0`` nếu :ref:`stream<class_AudioStreamPlayer_property_stream>` là :ref:`AudioStreamInteractive<class_AudioStreamInteractive>`, vì nó có thể phát nhiều clip cùng lúc.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_method_get_stream_playback:

.. rst-class:: classref-method

:ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **get_stream_playback**\ (\ ) :ref:`🔗<class_AudioStreamPlayer_method_get_stream_playback>`

Trả về :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` mới nhất của node này, thường là instance được tạo gần đây nhất bởi :ref:`play()<class_AudioStreamPlayer_method_play>`. Nếu không có âm thanh nào đang phát, phương thức này sẽ thất bại và trả về một playback trống.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_method_has_stream_playback:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_stream_playback**\ (\ ) :ref:`🔗<class_AudioStreamPlayer_method_has_stream_playback>`

Trả về ``true`` nếu bất kỳ âm thanh nào đang hoạt động, ngay cả khi :ref:`stream_paused<class_AudioStreamPlayer_property_stream_paused>` được đặt thành ``true``. Xem thêm :ref:`playing<class_AudioStreamPlayer_property_playing>` và :ref:`get_stream_playback()<class_AudioStreamPlayer_method_get_stream_playback>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_method_play:

.. rst-class:: classref-method

|void| **play**\ (\ from_position\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_AudioStreamPlayer_method_play>`

Phát âm thanh từ đầu hoặc từ ``from_position`` đã cho, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_method_seek:

.. rst-class:: classref-method

|void| **seek**\ (\ to_position\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamPlayer_method_seek>`

Khởi động lại tất cả âm thanh để phát từ ``to_position`` đã cho, tính bằng giây. Không làm gì nếu không có âm thanh nào đang phát.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AudioStreamPlayer_method_stop>`

Dừng tất cả âm thanh từ node này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
