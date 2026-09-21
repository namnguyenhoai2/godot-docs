:github_url: hide

.. meta::
	:keywords: sound, sfx

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPlayer3D.xml.

.. _class_AudioStreamPlayer3D:

AudioStreamPlayer3D
===================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Phát âm thanh có định vị trong không gian 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Phát âm thanh với các hiệu ứng âm thanh có định vị, dựa trên vị trí tương đối của audio listener. Các hiệu ứng định vị bao gồm suy giảm theo khoảng cách, tính định hướng và hiệu ứng Doppler. Để tăng tính chân thực, một bộ lọc low-pass được áp dụng cho các âm thanh ở xa. Có thể tắt bộ lọc này bằng cách đặt :ref:`attenuation_filter_cutoff_hz<class_AudioStreamPlayer3D_property_attenuation_filter_cutoff_hz>` thành ``20500``.

Theo mặc định, âm thanh được nghe từ vị trí camera. Có thể thay đổi điều này bằng cách thêm một node :ref:`AudioListener3D<class_AudioListener3D>` vào scene và bật node đó bằng cách gọi :ref:`AudioListener3D.make_current()<class_AudioListener3D_method_make_current>` trên nó.

Xem thêm :ref:`AudioStreamPlayer<class_AudioStreamPlayer>` để phát âm thanh không có định vị.

\ **Lưu ý:** Việc ẩn node **AudioStreamPlayer3D** không tắt đầu ra âm thanh của node. Để tạm thời tắt đầu ra âm thanh của **AudioStreamPlayer3D**, hãy đặt :ref:`volume_db<class_AudioStreamPlayer3D_property_volume_db>` thành một giá trị rất thấp như ``-100`` (không thể nghe thấy bằng tai người).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`                                              | :ref:`area_mask<class_AudioStreamPlayer3D_property_area_mask>`                                                       | ``0``         |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`attenuation_filter_cutoff_hz<class_AudioStreamPlayer3D_property_attenuation_filter_cutoff_hz>`                 | ``5000.0``    |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`attenuation_filter_db<class_AudioStreamPlayer3D_property_attenuation_filter_db>`                               | ``-24.0``     |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` | :ref:`attenuation_model<class_AudioStreamPlayer3D_property_attenuation_model>`                                       | ``0``         |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                                            | :ref:`autoplay<class_AudioStreamPlayer3D_property_autoplay>`                                                         | ``false``     |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`StringName<class_StringName>`                                | :ref:`bus<class_AudioStreamPlayer3D_property_bus>`                                                                   | ``&"Master"`` |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>`   | :ref:`doppler_tracking<class_AudioStreamPlayer3D_property_doppler_tracking>`                                         | ``0``         |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`emission_angle_degrees<class_AudioStreamPlayer3D_property_emission_angle_degrees>`                             | ``45.0``      |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                                            | :ref:`emission_angle_enabled<class_AudioStreamPlayer3D_property_emission_angle_enabled>`                             | ``false``     |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`emission_angle_filter_attenuation_db<class_AudioStreamPlayer3D_property_emission_angle_filter_attenuation_db>` | ``-12.0``     |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`max_db<class_AudioStreamPlayer3D_property_max_db>`                                                             | ``3.0``       |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`max_distance<class_AudioStreamPlayer3D_property_max_distance>`                                                 | ``0.0``       |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`                                              | :ref:`max_polyphony<class_AudioStreamPlayer3D_property_max_polyphony>`                                               | ``1``         |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`panning_strength<class_AudioStreamPlayer3D_property_panning_strength>`                                         | ``1.0``       |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`pitch_scale<class_AudioStreamPlayer3D_property_pitch_scale>`                                                   | ``1.0``       |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`PlaybackType<enum_AudioServer_PlaybackType>`                 | :ref:`playback_type<class_AudioStreamPlayer3D_property_playback_type>`                                               | ``0``         |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                                            | :ref:`playing<class_AudioStreamPlayer3D_property_playing>`                                                           | ``false``     |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`AudioStream<class_AudioStream>`                              | :ref:`stream<class_AudioStreamPlayer3D_property_stream>`                                                             |               |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`bool<class_bool>`                                            | :ref:`stream_paused<class_AudioStreamPlayer3D_property_stream_paused>`                                               | ``false``     |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`unit_size<class_AudioStreamPlayer3D_property_unit_size>`                                                       | ``10.0``      |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`volume_db<class_AudioStreamPlayer3D_property_volume_db>`                                                       | ``0.0``       |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`                                          | :ref:`volume_linear<class_AudioStreamPlayer3D_property_volume_linear>`                                               |               |
   +--------------------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------+---------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_playback_position<class_AudioStreamPlayer3D_method_get_playback_position>`\ (\ )                |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` | :ref:`get_stream_playback<class_AudioStreamPlayer3D_method_get_stream_playback>`\ (\ )                    |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`has_stream_playback<class_AudioStreamPlayer3D_method_has_stream_playback>`\ (\ )                    |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`play<class_AudioStreamPlayer3D_method_play>`\ (\ from_position\: :ref:`float<class_float>` = 0.0\ ) |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`seek<class_AudioStreamPlayer3D_method_seek>`\ (\ to_position\: :ref:`float<class_float>`\ )         |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`stop<class_AudioStreamPlayer3D_method_stop>`\ (\ )                                                  |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_AudioStreamPlayer3D_signal_finished:

.. rst-class:: classref-signal

**finished**\ (\ ) :ref:`🔗<class_AudioStreamPlayer3D_signal_finished>`

Được phát ra khi âm thanh dừng phát.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AudioStreamPlayer3D_AttenuationModel:

.. rst-class:: classref-enumeration

enum **AttenuationModel**: :ref:`🔗<enum_AudioStreamPlayer3D_AttenuationModel>`

.. _class_AudioStreamPlayer3D_constant_ATTENUATION_INVERSE_DISTANCE:

.. rst-class:: classref-enumeration-constant

:ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` **ATTENUATION_INVERSE_DISTANCE** = ``0``

Suy giảm độ lớn theo khoảng cách tuyến tính.

.. _class_AudioStreamPlayer3D_constant_ATTENUATION_INVERSE_SQUARE_DISTANCE:

.. rst-class:: classref-enumeration-constant

:ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` **ATTENUATION_INVERSE_SQUARE_DISTANCE** = ``1``

Suy giảm độ lớn theo bình phương khoảng cách.

.. _class_AudioStreamPlayer3D_constant_ATTENUATION_LOGARITHMIC:

.. rst-class:: classref-enumeration-constant

:ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` **ATTENUATION_LOGARITHMIC** = ``2``

Suy giảm độ lớn theo khoảng cách logarithmic.

.. _class_AudioStreamPlayer3D_constant_ATTENUATION_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` **ATTENUATION_DISABLED** = ``3``

Không suy giảm độ lớn theo khoảng cách. Âm thanh vẫn được nghe theo vị trí, không giống như :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`. :ref:`ATTENUATION_DISABLED<class_AudioStreamPlayer3D_constant_ATTENUATION_DISABLED>` có thể kết hợp với giá trị :ref:`max_distance<class_AudioStreamPlayer3D_property_max_distance>` lớn hơn ``0.0`` để đạt được suy giảm tuyến tính được giới hạn trong một hình cầu có kích thước xác định.

.. rst-class:: classref-item-separator

----

.. _enum_AudioStreamPlayer3D_DopplerTracking:

.. rst-class:: classref-enumeration

enum **DopplerTracking**: :ref:`🔗<enum_AudioStreamPlayer3D_DopplerTracking>`

.. _class_AudioStreamPlayer3D_constant_DOPPLER_TRACKING_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>` **DOPPLER_TRACKING_DISABLED** = ``0``

Tắt theo dõi Doppler.

.. _class_AudioStreamPlayer3D_constant_DOPPLER_TRACKING_IDLE_STEP:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>` **DOPPLER_TRACKING_IDLE_STEP** = ``1``

Thực hiện theo dõi Doppler trong các frame process (xem :ref:`Node.NOTIFICATION_INTERNAL_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PROCESS>`).

.. _class_AudioStreamPlayer3D_constant_DOPPLER_TRACKING_PHYSICS_STEP:

.. rst-class:: classref-enumeration-constant

:ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>` **DOPPLER_TRACKING_PHYSICS_STEP** = ``2``

Thực hiện theo dõi Doppler trong các frame physics (xem :ref:`Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamPlayer3D_property_area_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **area_mask** = ``0`` :ref:`🔗<class_AudioStreamPlayer3D_property_area_mask>`

.. rst-class:: classref-property-setget

- |void| **set_area_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_area_mask**\ (\ )

Determines which :ref:`Area3D<class_Area3D>` layers affect the sound for reverb and audio bus effects. Areas can be used to redirect :ref:`AudioStream<class_AudioStream>`\ s so that they play in a certain audio bus. An example of how you might use this is making a "water" area so that sounds played in the water are redirected through an audio bus to make them sound like they are being played underwater.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_attenuation_filter_cutoff_hz:

.. rst-class:: classref-property

:ref:`float<class_float>` **attenuation_filter_cutoff_hz** = ``5000.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_attenuation_filter_cutoff_hz>`

.. rst-class:: classref-property-setget

- |void| **set_attenuation_filter_cutoff_hz**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_attenuation_filter_cutoff_hz**\ (\ )

Tần số cutoff của bộ lọc low-pass suy giảm, tính bằng Hz. Âm thanh trên tần số này bị suy giảm nhiều hơn âm thanh dưới tần số này. Để tắt hiệu ứng này, hãy đặt giá trị này thành ``20500`` vì tần số này cao hơn giới hạn nghe được của tai người.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_attenuation_filter_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **attenuation_filter_db** = ``-24.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_attenuation_filter_db>`

.. rst-class:: classref-property-setget

- |void| **set_attenuation_filter_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_attenuation_filter_db**\ (\ )

Mức độ bộ lọc ảnh hưởng đến độ lớn, tính bằng decibel.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_attenuation_model:

.. rst-class:: classref-property

:ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` **attenuation_model** = ``0`` :ref:`🔗<class_AudioStreamPlayer3D_property_attenuation_model>`

.. rst-class:: classref-property-setget

- |void| **set_attenuation_model**\ (\ value\: :ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>`\ ) - :ref:`AttenuationModel<enum_AudioStreamPlayer3D_AttenuationModel>` **get_attenuation_model**\ (\ )

Xác định âm thanh sẽ nhỏ đi theo khoảng cách một cách tuyến tính, theo bình phương, logarithmic hay không bị ảnh hưởng bởi khoảng cách, qua đó tắt suy giảm.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_autoplay:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **autoplay** = ``false`` :ref:`🔗<class_AudioStreamPlayer3D_property_autoplay>`

.. rst-class:: classref-property-setget

- |void| **set_autoplay**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_autoplay_enabled**\ (\ )

Nếu ``true``, âm thanh sẽ phát khi node AudioStreamPlayer3D được thêm vào scene tree.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_bus:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **bus** = ``&"Master"`` :ref:`🔗<class_AudioStreamPlayer3D_property_bus>`

.. rst-class:: classref-property-setget

- |void| **set_bus**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_bus**\ (\ )

Audio bus mà âm thanh này đang phát trên đó.

\ **Lưu ý:** Khi đặt thuộc tính này, hãy nhớ rằng không có bước validation nào được thực hiện để kiểm tra xem tên đã cho có khớp với một bus hiện có hay không. Điều này là do các audio bus layout có thể được tải sau khi thuộc tính này được đặt. Nếu không thể phân giải tên đã cho tại runtime, tên đó sẽ chuyển về ``"Master"``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_doppler_tracking:

.. rst-class:: classref-property

:ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>` **doppler_tracking** = ``0`` :ref:`🔗<class_AudioStreamPlayer3D_property_doppler_tracking>`

.. rst-class:: classref-property-setget

- |void| **set_doppler_tracking**\ (\ value\: :ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>`\ ) - :ref:`DopplerTracking<enum_AudioStreamPlayer3D_DopplerTracking>` **get_doppler_tracking**\ (\ )

Xác định hiệu ứng Doppler sẽ được tính toán ở bước nào.

\ **Note:** If :ref:`doppler_tracking<class_AudioStreamPlayer3D_property_doppler_tracking>` is not :ref:`DOPPLER_TRACKING_DISABLED<class_AudioStreamPlayer3D_constant_DOPPLER_TRACKING_DISABLED>` but the current :ref:`Camera3D<class_Camera3D>`/:ref:`AudioListener3D<class_AudioListener3D>` has doppler tracking disabled, the Doppler effect will be heard but will not take the movement of the current listener into account. If accurate Doppler effect is desired, doppler tracking should be enabled on both the **AudioStreamPlayer3D** and the current :ref:`Camera3D<class_Camera3D>`/:ref:`AudioListener3D<class_AudioListener3D>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_emission_angle_degrees:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_angle_degrees** = ``45.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_emission_angle_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_emission_angle**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_angle**\ (\ )

Góc mà tại đó âm thanh đến listener mà không bị suy giảm.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_emission_angle_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **emission_angle_enabled** = ``false`` :ref:`🔗<class_AudioStreamPlayer3D_property_emission_angle_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_emission_angle_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_emission_angle_enabled**\ (\ )

Nếu ``true``, âm thanh sẽ được suy giảm theo hướng của âm thanh.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_emission_angle_filter_attenuation_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **emission_angle_filter_attenuation_db** = ``-12.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_emission_angle_filter_attenuation_db>`

.. rst-class:: classref-property-setget

- |void| **set_emission_angle_filter_attenuation_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_emission_angle_filter_attenuation_db**\ (\ )

Hệ số suy giảm được sử dụng nếu listener nằm ngoài :ref:`emission_angle_degrees<class_AudioStreamPlayer3D_property_emission_angle_degrees>` và :ref:`emission_angle_enabled<class_AudioStreamPlayer3D_property_emission_angle_enabled>` được đặt, tính bằng decibel.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_max_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_db** = ``3.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_max_db>`

.. rst-class:: classref-property-setget

- |void| **set_max_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_db**\ (\ )

Đặt mức tối đa tuyệt đối của âm thanh, tính bằng decibel.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_distance** = ``0.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_distance**\ (\ )

Khoảng cách mà vượt quá đó thì hoàn toàn không thể nghe thấy âm thanh. Chỉ có tác dụng nếu được đặt thành giá trị lớn hơn ``0.0``. :ref:`max_distance<class_AudioStreamPlayer3D_property_max_distance>` hoạt động kết hợp với :ref:`unit_size<class_AudioStreamPlayer3D_property_unit_size>`. Tuy nhiên, không giống như :ref:`unit_size<class_AudioStreamPlayer3D_property_unit_size>`, hành vi của nó phụ thuộc vào :ref:`attenuation_model<class_AudioStreamPlayer3D_property_attenuation_model>`, :ref:`max_distance<class_AudioStreamPlayer3D_property_max_distance>` luôn hoạt động theo cách tuyến tính. Điều này có thể ngăn **AudioStreamPlayer3D** yêu cầu audio mixing khi listener ở xa, nhờ đó tiết kiệm tài nguyên CPU.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_max_polyphony:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_polyphony** = ``1`` :ref:`🔗<class_AudioStreamPlayer3D_property_max_polyphony>`

.. rst-class:: classref-property-setget

- |void| **set_max_polyphony**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_polyphony**\ (\ )

Số lượng âm thanh tối đa mà node này có thể phát cùng lúc. Việc phát thêm âm thanh sau khi đạt đến giá trị này sẽ cắt âm thanh cũ nhất.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_panning_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **panning_strength** = ``1.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_panning_strength>`

.. rst-class:: classref-property-setget

- |void| **set_panning_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_panning_strength**\ (\ )

Điều chỉnh độ mạnh panning của node này bằng cách nhân :ref:`ProjectSettings.audio/general/3d_panning_strength<class_ProjectSettings_property_audio/general/3d_panning_strength>` cơ sở với hệ số này. Nếu tích bằng ``0.0`` thì stereo panning bị tắt và âm lượng giống nhau trên mọi channel. Nếu tích bằng ``1.0`` thì một trong các channel sẽ bị tắt tiếng khi âm thanh nằm chính xác về bên trái (hoặc bên phải) của listener.

Hai cách bố trí stereo với hai loa triển khai `WebAudio standard for StereoPannerNode Panning <https://webaudio.github.io/web-audio-api/#stereopanner-algorithm>`__, trong đó âm lượng là cosine của một nửa góc phương vị đến tai.

Đối với các cách bố trí loa khác như 5.1 và 7.1, thuật toán SPCAP (Speaker-Placement Correction Amplitude) được triển khai.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_pitch_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **pitch_scale** = ``1.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_pitch_scale>`

.. rst-class:: classref-property-setget

- |void| **set_pitch_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_pitch_scale**\ (\ )

Cao độ và tempo của âm thanh, dưới dạng hệ số nhân của sample rate của sample âm thanh.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_playback_type:

.. rst-class:: classref-property

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **playback_type** = ``0`` :ref:`🔗<class_AudioStreamPlayer3D_property_playback_type>`

.. rst-class:: classref-property-setget

- |void| **set_playback_type**\ (\ value\: :ref:`PlaybackType<enum_AudioServer_PlaybackType>`\ ) - :ref:`PlaybackType<enum_AudioServer_PlaybackType>` **get_playback_type**\ (\ )

**Thử nghiệm:** Thuộc tính này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Kiểu playback của stream player. Nếu được đặt khác giá trị mặc định, nó sẽ buộc sử dụng kiểu playback đó.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_playing:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **playing** = ``false`` :ref:`🔗<class_AudioStreamPlayer3D_property_playing>`

.. rst-class:: classref-property-setget

- |void| **set_playing**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_playing**\ (\ )

Nếu ``true``, âm thanh đang phát hoặc đã được xếp hàng để phát (xem :ref:`play()<class_AudioStreamPlayer3D_method_play>`).

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_stream:

.. rst-class:: classref-property

:ref:`AudioStream<class_AudioStream>` **stream** :ref:`🔗<class_AudioStreamPlayer3D_property_stream>`

.. rst-class:: classref-property-setget

- |void| **set_stream**\ (\ value\: :ref:`AudioStream<class_AudioStream>`\ ) - :ref:`AudioStream<class_AudioStream>` **get_stream**\ (\ )

Tài nguyên :ref:`AudioStream<class_AudioStream>` sẽ được phát.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_stream_paused:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **stream_paused** = ``false`` :ref:`🔗<class_AudioStreamPlayer3D_property_stream_paused>`

.. rst-class:: classref-property-setget

- |void| **set_stream_paused**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_stream_paused**\ (\ )

Nếu ``true``, quá trình phát sẽ bị tạm dừng. Bạn có thể tiếp tục bằng cách đặt :ref:`stream_paused<class_AudioStreamPlayer3D_property_stream_paused>` thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_unit_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **unit_size** = ``10.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_unit_size>`

.. rst-class:: classref-property-setget

- |void| **set_unit_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_unit_size**\ (\ )

Hệ số của hiệu ứng suy giảm âm thanh. Giá trị cao hơn khiến âm thanh có thể nghe được ở khoảng cách lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_volume_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_db** = ``0.0`` :ref:`🔗<class_AudioStreamPlayer3D_property_volume_db>`

.. rst-class:: classref-property-setget

- |void| **set_volume_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_db**\ (\ )

Mức âm thanh cơ bản trước khi suy giảm, tính bằng decibel.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_property_volume_linear:

.. rst-class:: classref-property

:ref:`float<class_float>` **volume_linear** :ref:`🔗<class_AudioStreamPlayer3D_property_volume_linear>`

.. rst-class:: classref-property-setget

- |void| **set_volume_linear**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_volume_linear**\ (\ )

Mức âm thanh cơ bản trước khi suy giảm, dưới dạng giá trị tuyến tính.

\ **Lưu ý:** Thành viên này sửa đổi :ref:`volume_db<class_AudioStreamPlayer3D_property_volume_db>` để thuận tiện. Giá trị trả về tương đương với kết quả của :ref:`@GlobalScope.db_to_linear()<class_@GlobalScope_method_db_to_linear>` trên :ref:`volume_db<class_AudioStreamPlayer3D_property_volume_db>`. Việc thiết lập thành viên này tương đương với việc đặt :ref:`volume_db<class_AudioStreamPlayer3D_property_volume_db>` thành kết quả của :ref:`@GlobalScope.linear_to_db()<class_@GlobalScope_method_linear_to_db>` trên một giá trị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamPlayer3D_method_get_playback_position:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_playback_position**\ (\ ) :ref:`🔗<class_AudioStreamPlayer3D_method_get_playback_position>`

Trả về vị trí trong :ref:`AudioStream<class_AudioStream>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_method_get_stream_playback:

.. rst-class:: classref-method

:ref:`AudioStreamPlayback<class_AudioStreamPlayback>` **get_stream_playback**\ (\ ) :ref:`🔗<class_AudioStreamPlayer3D_method_get_stream_playback>`

Trả về đối tượng :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` được liên kết với **AudioStreamPlayer3D** này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_method_has_stream_playback:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_stream_playback**\ (\ ) :ref:`🔗<class_AudioStreamPlayer3D_method_has_stream_playback>`

Trả về liệu :ref:`AudioStreamPlayer<class_AudioStreamPlayer>` có thể trả về đối tượng :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` hay không.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_method_play:

.. rst-class:: classref-method

|void| **play**\ (\ from_position\: :ref:`float<class_float>` = 0.0\ ) :ref:`🔗<class_AudioStreamPlayer3D_method_play>`

Xếp âm thanh vào hàng đợi để phát ở frame vật lý tiếp theo, bắt đầu từ vị trí ``from_position`` đã cho, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_method_seek:

.. rst-class:: classref-method

|void| **seek**\ (\ to_position\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamPlayer3D_method_seek>`

Đặt vị trí bắt đầu phát âm thanh, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlayer3D_method_stop:

.. rst-class:: classref-method

|void| **stop**\ (\ ) :ref:`🔗<class_AudioStreamPlayer3D_method_stop>`

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
