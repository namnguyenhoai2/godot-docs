:github_url: hide

.. meta::
	:keywords: sound, sfx

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPlayer2D.xml.

.. _class_AudioStreamPlayer2D:

AudioStreamPlayer2D
===================

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Phát âm thanh theo vị trí trong không gian 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Phát âm thanh được giảm cường độ theo khoảng cách đến listener.

Theo mặc định, âm thanh được nghe từ trung tâm màn hình. Bạn có thể thay đổi điều này bằng cách thêm một node :ref:`AudioListener2D<class_AudioListener2D>` vào scene và bật nó bằng cách gọi :ref:`AudioListener2D.make_current()<class_AudioListener2D_method_make_current>` trên node đó.

Xem thêm :ref:`AudioStreamPlayer<class_AudioStreamPlayer>` để phát âm thanh không theo vị trí.

\ **Lưu ý:** Việc ẩn node **AudioStreamPlayer2D** không vô hiệu hóa đầu ra âm thanh của node đó. Để tạm thời vô hiệu hóa đầu ra âm thanh của **AudioStreamPlayer2D**, hãy đặt :ref:`volume_db<class_AudioStreamPlayer2D_property_volume_db>` thành một giá trị rất thấp như ``-100`` (mức này không thể nghe được đối với tai người).

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Luồng âm thanh <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`                              | :ref:`area_mask<class_AudioStreamPlayer2D_property_area_mask>`               | ``0``         |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`attenuation<class_AudioStreamPlayer2D_property_attenuation>`           | ``1.0``       |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                            | :ref:`autoplay<class_AudioStreamPlayer2D_property_autoplay>`                 | ``false``     |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`StringName<class_StringName>`                | :ref:`bus<class_AudioStreamPlayer2D_property_bus>`                           | ``&"Master"`` |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`max_distance<class_AudioStreamPlayer2D_property_max_distance>`         | ``2000.0``    |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`                              | :ref:`max_polyphony<class_AudioStreamPlayer2D_property_max_polyphony>`       | ``1``         |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`panning_strength<class_AudioStreamPlayer2D_property_panning_strength>` | ``1.0``       |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`pitch_scale<class_AudioStreamPlayer2D_property_pitch_scale>`           | ``1.0``       |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`PlaybackType<enum_AudioServer_PlaybackType>` | :ref:`playback_type<class_AudioStreamPlayer2D_property_playback_type>`       | ``0``         |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                            | :ref:`playing<class_AudioStreamPlayer2D_property_playing>`                   | ``false``     |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`AudioStream<class_AudioStream>`              | :ref:`stream<class_AudioStreamPlayer2D_property_stream>`                     |               |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                            | :ref:`stream_paused<class_AudioStreamPlayer2D_property_stream_paused>`       | ``false``     |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`volume_db<class_AudioStreamPlayer2D_property_volume_db>`               | ``0.0``       |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                          | :ref:`volume_linear<class_AudioStreamPlayer2D_property_volume_linear>`       |               |
   +----------------------------------------------------+------------------------------------------------------------------------------+---------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_playback_position<class_AudioStreamPlayer2D_method_get_playback_position>`\ (\ )                |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` | :ref:`get_stream_playback<class_AudioStreamPlayer2D_method_get_stream_playback>`\ (\ )                    |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`has_stream_playback<class_AudioStreamPlayer2D_method_has_stream_playback>`\ (\ )                    |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`play<class_AudioStreamPlayer2D_method_play>`\ (\ from_position\: :ref:`float<class_float>` = 0.0\ ) |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`seek<class_AudioStreamPlayer2D_method_seek>`\ (\ to_position\: :ref:`float<class_float>`\ )         |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`stop<class_AudioStreamPlayer2D_method_stop>`\ (\ )                                                  |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_AudioStreamPlayer2D_signal_finished:

.. rst-class:: classref-signal

**finished**\ (\ ) :ref:`🔗<class_AudioStreamPlayer2D_signal_finished>`

Được phát ra khi âm thanh dừng phát.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamPlayer2D_property_area_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **area_mask** = ``0`` :ref:`🔗<class_AudioStreamPlayer2D_property_area_mask>`

.. rst-class:: classref-property-setget

- |void| **set_area_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_area_mask**\ (\ )

Xác định các layer của :ref:`Area2D<class_Area2D>` ảnh hưởng đến âm thanh đối với hiệu ứng reverb và audio bus. Có thể dùng các Area để chuyển hướng :ref:`AudioStream<class_AudioStream>`\ s để chúng phát trên một audio bus nhất định. Một ví dụ về cách sử dụng là tạo một Area "water" để các âm thanh phát trong nước được chuyển qua một audio bus, khiến chúng nghe như đang được phát dưới nước.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_attenuation:

.. rst-class:: classref-property

:ref:`float<class_float>` **attenuation** = ``1.0`` :ref:`🔗<class_AudioStreamPlayer2D_property_attenuation>`

.. rst-class:: classref-property-setget

- |void| **set_attenuation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_attenuation**\ (\ )

Âm lượng được giảm theo khoảng cách, với giá trị này làm số mũ.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_autoplay:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **autoplay** = ``false`` :ref:`🔗<class_AudioStreamPlayer2D_property_autoplay>`

.. rst-class:: classref-property-setget

- |void| **set_autoplay**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_autoplay_enabled**\ (\ )

Nếu ``true``, âm thanh sẽ phát khi được thêm vào scene tree.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_bus:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **bus** = ``&"Master"`` :ref:`🔗<class_AudioStreamPlayer2D_property_bus>`

.. rst-class:: classref-property-setget

- |void| **set_bus**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_bus**\ (\ )

Bus mà âm thanh này đang phát trên đó.

\ **Lưu ý:** Khi thiết lập thuộc tính này, hãy nhớ rằng không có bước validation nào được thực hiện để kiểm tra xem tên đã cho có khớp với một bus hiện có hay không. Nguyên nhân là audio bus layout có thể được tải sau khi thuộc tính này được thiết lập. Nếu không thể phân giải tên đã cho trong runtime, nó sẽ chuyển về ``"Master"``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_distance** = ``2000.0`` :ref:`🔗<class_AudioStreamPlayer2D_property_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_distance**\ (\ )

Khoảng cách tối đa mà từ đó vẫn có thể nghe thấy âm thanh.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_max_polyphony:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_polyphony** = ``1`` :ref:`🔗<class_AudioStreamPlayer2D_property_max_polyphony>`

.. rst-class:: classref-property-setget

- |void| **set_max_polyphony**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_polyphony**\ (\ )

Số lượng âm thanh tối đa mà node này có thể phát đồng thời. Việc phát thêm âm thanh sau khi đạt đến giá trị này sẽ ngắt các âm thanh cũ nhất.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_panning_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **panning_strength** = ``1.0`` :ref:`🔗<class_AudioStreamPlayer2D_property_panning_strength>`

.. rst-class:: classref-property-setget

- |void| **set_panning_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_panning_strength**\ (\ )

Điều chỉnh cường độ panning của node này bằng cách nhân :ref:`ProjectSettings.audio/general/2d_panning_strength<class_ProjectSettings_property_audio/general/2d_panning_strength>` cơ sở với hệ số này. Giá trị cao hơn sẽ pan âm thanh từ trái sang phải rõ rệt hơn so với giá trị thấp hơn.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_pitch_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **pitch_scale** = ``1.0`` :ref:`🔗<class_AudioStreamPlayer2D_property_pitch_scale>`

.. rst-class:: classref-property-setget

- |void| **set_pitch_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pitch_scale**\ (\ )

Cao độ và tempo của âm thanh, dưới dạng hệ số nhân với sample rate của audio sample.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_playback_type:

.. rst-class:: classref-property

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **playback_type** = ``0`` :ref:`🔗<class_AudioStreamPlayer2D_property_playback_type>`

.. rst-class:: classref-property-setget

- |void| **set_playback_type**\ (\ value\: :ref:`PlaybackType<enum_AudioServer_PlaybackType>`\ ) - :ref:`PlaybackType<enum_AudioServer_PlaybackType>` **get_playback_type**\ (\ )

**Experimental:** Thuộc tính này có thể bị thay đổi hoặc xóa trong các phiên bản tương lai.

Loại phát của stream player. Nếu được đặt khác giá trị mặc định, nó sẽ buộc sử dụng loại phát đó.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_playing:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **playing** = ``false`` :ref:`🔗<class_AudioStreamPlayer2D_property_playing>`

.. rst-class:: classref-property-setget

- |void| **set_playing**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_playing**\ (\ )

Nếu ``true``, âm thanh đang phát hoặc đã được xếp hàng để phát (xem :ref:`play()<class_AudioStreamPlayer2D_method_play>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_stream:

.. rst-class:: classref-property

:ref:`AudioStream<class_AudioStream>` **stream** :ref:`🔗<class_AudioStreamPlayer2D_property_stream>`

.. rst-class:: classref-property-setget

- |void| **set_stream**\ (\ value\: :ref:`AudioStream<class_AudioStream>`\ ) - :ref:`AudioStream<class_AudioStream>` **get_stream**\ (\ )

Đối tượng :ref:`AudioStream<class_AudioStream>` sẽ được phát.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_stream_paused:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **stream_paused** = ``false`` :ref:`🔗<class_AudioStreamPlayer2D_property_stream_paused>`

.. rst-class:: classref-property-setget

- |void| **set_stream_paused**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_stream_paused**\ (\ )

Nếu ``true``, quá trình phát sẽ tạm dừng. Bạn có thể tiếp tục bằng cách đặt :ref:`stream_paused<class_AudioStreamPlayer2D_property_stream_paused>` thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_volume_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_db** = ``0.0`` :ref:`🔗<class_AudioStreamPlayer2D_property_volume_db>`

.. rst-class:: classref-property-setget

- |void| **set_volume_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_db**\ (\ )

Âm lượng cơ sở trước khi giảm cường độ, tính bằng decibel.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_property_volume_linear:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_linear** :ref:`🔗<class_AudioStreamPlayer2D_property_volume_linear>`

.. rst-class:: classref-property-setget

- |void| **set_volume_linear**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_linear**\ (\ )

Âm lượng cơ sở trước khi giảm cường độ, dưới dạng giá trị tuyến tính.

\ **Lưu ý:** Member này sửa đổi :ref:`volume_db<class_AudioStreamPlayer2D_property_volume_db>` để thuận tiện. Giá trị trả về tương đương với kết quả của :ref:`@GlobalScope.db_to_linear()<class_@GlobalScope_method_db_to_linear>` trên :ref:`volume_db<class_AudioStreamPlayer2D_property_volume_db>`. Việc thiết lập member này tương đương với việc đặt :ref:`volume_db<class_AudioStreamPlayer2D_property_volume_db>` thành kết quả của :ref:`@GlobalScope.linear_to_db()<class_@GlobalScope_method_linear_to_db>` trên một giá trị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamPlayer2D_method_get_playback_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_playback_position**\ (\ ) :ref:`🔗<class_AudioStreamPlayer2D_method_get_playback_position>`

Trả về vị trí trong :ref:`AudioStream<class_AudioStream>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_method_get_stream_playback:

.. rst-class:: classref-method

:ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **get_stream_playback**\ (\ ) :ref:`🔗<class_AudioStreamPlayer2D_method_get_stream_playback>`

Trả về đối tượng :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` được liên kết với **AudioStreamPlayer2D** này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_method_has_stream_playback:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_stream_playback**\ (\ ) :ref:`🔗<class_AudioStreamPlayer2D_method_has_stream_playback>`

Trả về việc :ref:`AudioStreamPlayer<class_AudioStreamPlayer>` có thể trả về đối tượng :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` hay không.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_method_play:

.. rst-class:: classref-method

|void| **play**\ (\ from_position\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_AudioStreamPlayer2D_method_play>`

Xếp âm thanh vào hàng đợi để phát ở frame vật lý tiếp theo, từ vị trí ``from_position`` đã cho, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_method_seek:

.. rst-class:: classref-method

|void| **seek**\ (\ to_position\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamPlayer2D_method_seek>`

Đặt vị trí bắt đầu phát âm thanh, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer2D_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AudioStreamPlayer2D_method_stop>`

Dừng âm thanh.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
