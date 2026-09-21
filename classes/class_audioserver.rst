:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioServer.xml.

.. _class_AudioServer:

AudioServer
===========

**Kế thừa:** :ref:`Object<class_Object>`

Giao diện server cấp thấp để truy cập âm thanh.

.. rst-class:: classref-introduction-group

Mô tả
-----

**AudioServer** là giao diện server cấp thấp để truy cập âm thanh. Nó chịu trách nhiệm tạo dữ liệu sample (âm thanh có thể phát) cũng như phát dữ liệu đó thông qua giao diện voice.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio buses <../tutorials/audio/audio_buses>`

- `Audio Device Changer Demo <https://godotengine.org/asset-library/asset/2758>`__

- `Audio Microphone Record Demo <https://godotengine.org/asset-library/asset/2760>`__

- `Audio Spectrum Visualizer Demo <https://godotengine.org/asset-library/asset/2762>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`int<class_int>`       | :ref:`bus_count<class_AudioServer_property_bus_count>`                       | ``1``         |
   +-----------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`String<class_String>` | :ref:`input_device<class_AudioServer_property_input_device>`                 | ``"Default"`` |
   +-----------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`String<class_String>` | :ref:`output_device<class_AudioServer_property_output_device>`               | ``"Default"`` |
   +-----------------------------+------------------------------------------------------------------------------+---------------+
   | :ref:`float<class_float>`   | :ref:`playback_speed_scale<class_AudioServer_property_playback_speed_scale>` | ``1.0``       |
   +-----------------------------+------------------------------------------------------------------------------+---------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`add_bus<class_AudioServer_method_add_bus>`\ (\ at_position\: :ref:`int<class_int>` = -1\ )                                                                                                 |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`add_bus_effect<class_AudioServer_method_add_bus_effect>`\ (\ bus_idx\: :ref:`int<class_int>`, effect\: :ref:`AudioEffect<class_AudioEffect>`, at_position\: :ref:`int<class_int>` = -1\ )  |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioBusLayout<class_AudioBusLayout>`           | :ref:`generate_bus_layout<class_AudioServer_method_generate_bus_layout>`\ (\ ) |const|                                                                                                           |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_bus_channels<class_AudioServer_method_get_bus_channels>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                                |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioEffect<class_AudioEffect>`                 | :ref:`get_bus_effect<class_AudioServer_method_get_bus_effect>`\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`\ )                                                        |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_bus_effect_count<class_AudioServer_method_get_bus_effect_count>`\ (\ bus_idx\: :ref:`int<class_int>`\ )                                                                                |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioEffectInstance<class_AudioEffectInstance>` | :ref:`get_bus_effect_instance<class_AudioServer_method_get_bus_effect_instance>`\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`, channel\: :ref:`int<class_int>` = 0\ ) |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_bus_index<class_AudioServer_method_get_bus_index>`\ (\ bus_name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                       |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                           | :ref:`get_bus_name<class_AudioServer_method_get_bus_name>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                                        |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_bus_peak_volume_left_db<class_AudioServer_method_get_bus_peak_volume_left_db>`\ (\ bus_idx\: :ref:`int<class_int>`, channel\: :ref:`int<class_int>`\ ) |const|                         |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_bus_peak_volume_right_db<class_AudioServer_method_get_bus_peak_volume_right_db>`\ (\ bus_idx\: :ref:`int<class_int>`, channel\: :ref:`int<class_int>`\ ) |const|                       |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                   | :ref:`get_bus_send<class_AudioServer_method_get_bus_send>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                                        |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_bus_volume_db<class_AudioServer_method_get_bus_volume_db>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                              |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_bus_volume_linear<class_AudioServer_method_get_bus_volume_linear>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                      |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                           | :ref:`get_driver_name<class_AudioServer_method_get_driver_name>`\ (\ ) |const|                                                                                                                   |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_input_buffer_length_frames<class_AudioServer_method_get_input_buffer_length_frames>`\ (\ )                                                                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`     | :ref:`get_input_device_list<class_AudioServer_method_get_input_device_list>`\ (\ )                                                                                                               |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`   | :ref:`get_input_frames<class_AudioServer_method_get_input_frames>`\ (\ frames\: :ref:`int<class_int>`\ )                                                                                         |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                 | :ref:`get_input_frames_available<class_AudioServer_method_get_input_frames_available>`\ (\ )                                                                                                     |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_input_mix_rate<class_AudioServer_method_get_input_mix_rate>`\ (\ ) |const|                                                                                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_mix_rate<class_AudioServer_method_get_mix_rate>`\ (\ ) |const|                                                                                                                         |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`     | :ref:`get_output_device_list<class_AudioServer_method_get_output_device_list>`\ (\ )                                                                                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_output_latency<class_AudioServer_method_get_output_latency>`\ (\ ) |const|                                                                                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SpeakerMode<enum_AudioServer_SpeakerMode>`      | :ref:`get_speaker_mode<class_AudioServer_method_get_speaker_mode>`\ (\ ) |const|                                                                                                                 |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_time_since_last_mix<class_AudioServer_method_get_time_since_last_mix>`\ (\ ) |const|                                                                                                   |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                             | :ref:`get_time_to_next_mix<class_AudioServer_method_get_time_to_next_mix>`\ (\ ) |const|                                                                                                         |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_bus_bypassing_effects<class_AudioServer_method_is_bus_bypassing_effects>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_bus_effect_enabled<class_AudioServer_method_is_bus_effect_enabled>`\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`\ ) |const|                                  |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_bus_mute<class_AudioServer_method_is_bus_mute>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                                          |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_bus_solo<class_AudioServer_method_is_bus_solo>`\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const|                                                                                          |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`is_stream_registered_as_sample<class_AudioServer_method_is_stream_registered_as_sample>`\ (\ stream\: :ref:`AudioStream<class_AudioStream>`\ )                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`lock<class_AudioServer_method_lock>`\ (\ )                                                                                                                                                 |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`move_bus<class_AudioServer_method_move_bus>`\ (\ index\: :ref:`int<class_int>`, to_index\: :ref:`int<class_int>`\ )                                                                        |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`register_stream_as_sample<class_AudioServer_method_register_stream_as_sample>`\ (\ stream\: :ref:`AudioStream<class_AudioStream>`\ )                                                       |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`remove_bus<class_AudioServer_method_remove_bus>`\ (\ index\: :ref:`int<class_int>`\ )                                                                                                      |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`remove_bus_effect<class_AudioServer_method_remove_bus_effect>`\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`\ )                                                  |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_bypass_effects<class_AudioServer_method_set_bus_bypass_effects>`\ (\ bus_idx\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ )                                          |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_effect_enabled<class_AudioServer_method_set_bus_effect_enabled>`\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ )     |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_layout<class_AudioServer_method_set_bus_layout>`\ (\ bus_layout\: :ref:`AudioBusLayout<class_AudioBusLayout>`\ )                                                                   |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_mute<class_AudioServer_method_set_bus_mute>`\ (\ bus_idx\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ )                                                              |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_name<class_AudioServer_method_set_bus_name>`\ (\ bus_idx\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ )                                                            |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_send<class_AudioServer_method_set_bus_send>`\ (\ bus_idx\: :ref:`int<class_int>`, send\: :ref:`StringName<class_StringName>`\ )                                                    |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_solo<class_AudioServer_method_set_bus_solo>`\ (\ bus_idx\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ )                                                              |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_volume_db<class_AudioServer_method_set_bus_volume_db>`\ (\ bus_idx\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ )                                               |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_bus_volume_linear<class_AudioServer_method_set_bus_volume_linear>`\ (\ bus_idx\: :ref:`int<class_int>`, volume_linear\: :ref:`float<class_float>`\ )                                   |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`set_enable_tagging_used_audio_streams<class_AudioServer_method_set_enable_tagging_used_audio_streams>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                 | :ref:`set_input_device_active<class_AudioServer_method_set_input_device_active>`\ (\ active\: :ref:`bool<class_bool>`\ )                                                                         |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`swap_bus_effects<class_AudioServer_method_swap_bus_effects>`\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`, by_effect_idx\: :ref:`int<class_int>`\ )             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                | :ref:`unlock<class_AudioServer_method_unlock>`\ (\ )                                                                                                                                             |
   +-------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_AudioServer_signal_bus_layout_changed:

.. rst-class:: classref-signal

**bus_layout_changed**\ (\ ) :ref:`🔗<class_AudioServer_signal_bus_layout_changed>`

Được phát ra khi một audio bus được thêm, xóa hoặc di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_signal_bus_renamed:

.. rst-class:: classref-signal

**bus_renamed**\ (\ bus_index\: :ref:`int<class_int>`, old_name\: :ref:`StringName<class_StringName>`, new_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AudioServer_signal_bus_renamed>`

Được phát ra khi audio bus tại ``bus_index`` được đổi tên từ ``old_name`` thành ``new_name``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_AudioServer_SpeakerMode:

.. rst-class:: classref-enumeration

enum **SpeakerMode**: :ref:`🔗<enum_AudioServer_SpeakerMode>`

.. _class_AudioServer_constant_SPEAKER_MODE_STEREO:

.. rst-class:: classref-enumeration-constant

:ref:`SpeakerMode<enum_AudioServer_SpeakerMode>` **SPEAKER_MODE_STEREO** = ``0``

Đã phát hiện hai loa trở xuống.

.. _class_AudioServer_constant_SPEAKER_SURROUND_31:

.. rst-class:: classref-enumeration-constant

:ref:`SpeakerMode<enum_AudioServer_SpeakerMode>` **SPEAKER_SURROUND_31** = ``1``

Đã phát hiện cấu hình âm thanh vòm 3.1 kênh.

.. _class_AudioServer_constant_SPEAKER_SURROUND_51:

.. rst-class:: classref-enumeration-constant

:ref:`SpeakerMode<enum_AudioServer_SpeakerMode>` **SPEAKER_SURROUND_51** = ``2``

Đã phát hiện cấu hình âm thanh vòm 5.1 kênh.

.. _class_AudioServer_constant_SPEAKER_SURROUND_71:

.. rst-class:: classref-enumeration-constant

:ref:`SpeakerMode<enum_AudioServer_SpeakerMode>` **SPEAKER_SURROUND_71** = ``3``

Đã phát hiện cấu hình âm thanh vòm 7.1 kênh.

.. rst-class:: classref-item-separator

----

.. _enum_AudioServer_PlaybackType:

.. rst-class:: classref-enumeration

enum **PlaybackType**: :ref:`🔗<enum_AudioServer_PlaybackType>`

.. _class_AudioServer_constant_PLAYBACK_TYPE_DEFAULT:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **PLAYBACK_TYPE_DEFAULT** = ``0``

**Thử nghiệm:** Hằng số này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Việc phát sẽ được coi là thuộc kiểu được khai báo tại :ref:`ProjectSettings.audio/general/default_playback_type<class_ProjectSettings_property_audio/general/default_playback_type>`.

.. _class_AudioServer_constant_PLAYBACK_TYPE_STREAM:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **PLAYBACK_TYPE_STREAM** = ``1``

**Thử nghiệm:** Hằng số này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Buộc việc phát được coi là một stream.

.. _class_AudioServer_constant_PLAYBACK_TYPE_SAMPLE:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **PLAYBACK_TYPE_SAMPLE** = ``2``

**Thử nghiệm:** Hằng số này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Buộc việc phát được coi là một sample. Điều này có thể cung cấp độ trễ thấp hơn và việc phát ổn định hơn (ít nguy cơ âm thanh bị rè hơn), đổi lại tính linh hoạt sẽ thấp hơn.

\ **Lưu ý:** Hiện chỉ được hỗ trợ trên nền tảng web.

\ **Note:** :ref:`AudioEffect<class_AudioEffect>`\ s are not supported when playback is considered as a sample.

.. _class_AudioServer_constant_PLAYBACK_TYPE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackType<enum_AudioServer_PlaybackType>` **PLAYBACK_TYPE_MAX** = ``3``

**Thử nghiệm:** Hằng số này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Biểu thị kích thước của enum :ref:`PlaybackType<enum_AudioServer_PlaybackType>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioServer_property_bus_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **bus_count** = ``1`` :ref:`🔗<class_AudioServer_property_bus_count>`

.. rst-class:: classref-property-setget

- |void| **set_bus_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bus_count**\ (\ )

Số lượng audio bus hiện có.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_property_input_device:

.. rst-class:: classref-property

:ref:`String<class_String>` **input_device** = ``"Default"`` :ref:`🔗<class_AudioServer_property_input_device>`

.. rst-class:: classref-property-setget

- |void| **set_input_device**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_input_device**\ (\ )

Tên thiết bị hiện tại dùng cho đầu vào âm thanh (xem :ref:`get_input_device_list()<class_AudioServer_method_get_input_device_list>`). Trên các hệ thống có nhiều đầu vào âm thanh (chẳng hạn như âm thanh analog, USB và HDMI), thuộc tính này có thể được dùng để chọn thiết bị đầu vào âm thanh. Giá trị ``"Default"`` sẽ ghi âm bằng thiết bị đầu vào âm thanh mặc định trên toàn hệ thống. Nếu đặt tên thiết bị không hợp lệ, giá trị sẽ được hoàn nguyên về ``"Default"``.

\ **Lưu ý:** :ref:`ProjectSettings.audio/driver/enable_input<class_ProjectSettings_property_audio/driver/enable_input>` phải là ``true`` để đầu vào âm thanh hoạt động. Xem thêm phần mô tả của thiết lập đó để biết các lưu ý liên quan đến quyền và cài đặt quyền riêng tư của hệ điều hành.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_property_output_device:

.. rst-class:: classref-property

:ref:`String<class_String>` **output_device** = ``"Default"`` :ref:`🔗<class_AudioServer_property_output_device>`

.. rst-class:: classref-property-setget

- |void| **set_output_device**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_output_device**\ (\ )

Tên thiết bị hiện tại dùng cho đầu ra âm thanh (xem :ref:`get_output_device_list()<class_AudioServer_method_get_output_device_list>`). Trên các hệ thống có nhiều đầu ra âm thanh (chẳng hạn như âm thanh analog, USB và HDMI), thuộc tính này có thể được dùng để chọn thiết bị đầu ra âm thanh. Giá trị ``"Default"`` sẽ phát âm thanh qua thiết bị đầu ra âm thanh mặc định trên toàn hệ thống. Nếu đặt tên thiết bị không hợp lệ, giá trị sẽ được hoàn nguyên về ``"Default"``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_property_playback_speed_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **playback_speed_scale** = ``1.0`` :ref:`🔗<class_AudioServer_property_playback_speed_scale>`

.. rst-class:: classref-property-setget

- |void| **set_playback_speed_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_playback_speed_scale**\ (\ )

Điều chỉnh tốc độ phát âm thanh (tức là đặt giá trị thành ``0.5`` sẽ khiến âm thanh được phát ở một nửa tốc độ). Xem thêm :ref:`Engine.time_scale<class_Engine_property_time_scale>` để ảnh hưởng đến tốc độ mô phỏng tổng thể, vốn độc lập với :ref:`playback_speed_scale<class_AudioServer_property_playback_speed_scale>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioServer_method_add_bus:

.. rst-class:: classref-method

|void| **add_bus**\ (\ at_position\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_AudioServer_method_add_bus>`

Thêm một bus tại ``at_position``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_add_bus_effect:

.. rst-class:: classref-method

|void| **add_bus_effect**\ (\ bus_idx\: :ref:`int<class_int>`, effect\: :ref:`AudioEffect<class_AudioEffect>`, at_position\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_AudioServer_method_add_bus_effect>`

Thêm một effect :ref:`AudioEffect<class_AudioEffect>` vào bus ``bus_idx`` tại ``at_position``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_generate_bus_layout:

.. rst-class:: classref-method

:ref:`AudioBusLayout<class_AudioBusLayout>` **generate_bus_layout**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_generate_bus_layout>`

Tạo một :ref:`AudioBusLayout<class_AudioBusLayout>` bằng các bus và effect hiện có.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_channels:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_bus_channels**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_channels>`

Trả về số kênh của bus tại chỉ mục ``bus_idx``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_effect:

.. rst-class:: classref-method

:ref:`AudioEffect<class_AudioEffect>` **get_bus_effect**\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_get_bus_effect>`

Trả về :ref:`AudioEffect<class_AudioEffect>` tại vị trí ``effect_idx`` trong bus ``bus_idx``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_effect_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_bus_effect_count**\ (\ bus_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_get_bus_effect_count>`

Trả về số effect trên bus tại ``bus_idx``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_effect_instance:

.. rst-class:: classref-method

:ref:`AudioEffectInstance<class_AudioEffectInstance>` **get_bus_effect_instance**\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`, channel\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_AudioServer_method_get_bus_effect_instance>`

Trả về :ref:`AudioEffectInstance<class_AudioEffectInstance>` được gán cho các chỉ mục bus và effect đã cho (và tùy chọn cả kênh).

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_bus_index**\ (\ bus_name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_index>`

Trả về chỉ mục của bus có tên ``bus_name``. Trả về ``-1`` nếu không tồn tại bus nào có tên được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_bus_name**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_name>`

Trả về tên của bus có chỉ mục ``bus_idx``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_peak_volume_left_db:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_bus_peak_volume_left_db**\ (\ bus_idx\: :ref:`int<class_int>`, channel\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_peak_volume_left_db>`

Trả về âm lượng đỉnh của loa trái tại chỉ mục bus ``bus_idx`` và chỉ mục kênh ``channel``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_peak_volume_right_db:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_bus_peak_volume_right_db**\ (\ bus_idx\: :ref:`int<class_int>`, channel\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_peak_volume_right_db>`

Trả về âm lượng đỉnh của loa phải tại chỉ mục bus ``bus_idx`` và chỉ mục kênh ``channel``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_send:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_bus_send**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_send>`

Trả về tên của bus mà bus tại chỉ mục ``bus_idx`` gửi âm thanh đến.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_volume_db:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_bus_volume_db**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_volume_db>`

Trả về âm lượng của bus tại chỉ mục ``bus_idx`` theo dB.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_bus_volume_linear:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_bus_volume_linear**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_get_bus_volume_linear>`

Trả về âm lượng của bus tại chỉ mục ``bus_idx`` dưới dạng giá trị tuyến tính.

\ **Lưu ý:** Giá trị trả về tương đương với kết quả của :ref:`@GlobalScope.db_to_linear()<class_@GlobalScope_method_db_to_linear>` trên kết quả của :ref:`get_bus_volume_db()<class_AudioServer_method_get_bus_volume_db>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_driver_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_driver_name**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_driver_name>`

Trả về tên audio driver hiện tại. Mặc định thường phụ thuộc vào hệ điều hành, nhưng có thể được ghi đè thông qua ``--audio-driver`` :doc:`command line argument <../tutorials/editor/command_line_tutorial>`. ``--headless`` cũng tự động đặt audio driver thành ``Dummy``. Xem thêm :ref:`ProjectSettings.audio/driver/driver<class_ProjectSettings_property_audio/driver/driver>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_input_buffer_length_frames:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_input_buffer_length_frames**\ (\ ) :ref:`🔗<class_AudioServer_method_get_input_buffer_length_frames>`

**Thử nghiệm:** Phương thức này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Trả về kích thước tuyệt đối của microphone input buffer. Giá trị này được đặt thành bội số của độ trễ âm thanh và có thể được dùng để ước tính tốc độ tối thiểu mà các frame cần được lấy.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_input_device_list:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_input_device_list**\ (\ ) :ref:`🔗<class_AudioServer_method_get_input_device_list>`

Trả về tên của tất cả thiết bị đầu vào âm thanh được phát hiện trên hệ thống.

\ **Lưu ý:** :ref:`ProjectSettings.audio/driver/enable_input<class_ProjectSettings_property_audio/driver/enable_input>` phải là ``true`` để đầu vào âm thanh hoạt động. Xem thêm phần mô tả của thiết lập đó để biết các lưu ý liên quan đến quyền và cài đặt quyền riêng tư của hệ điều hành.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_input_frames:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_input_frames**\ (\ frames\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_get_input_frames>`

**Thử nghiệm:** Phương thức này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` chứa chính xác ``frames`` sample âm thanh từ microphone buffer nội bộ nếu có; nếu không, trả về một :ref:`PackedVector2Array<class_PackedVector2Array>` rỗng.

Buffer được nạp với tốc độ :ref:`get_input_mix_rate()<class_AudioServer_method_get_input_mix_rate>` frame mỗi giây khi :ref:`set_input_device_active()<class_AudioServer_method_set_input_device_active>` đã được đặt thành công thành ``true``.

Các sample là giá trị PCM dấu phẩy động có dấu trong khoảng từ ``-1`` đến ``1``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_input_frames_available:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_input_frames_available**\ (\ ) :ref:`🔗<class_AudioServer_method_get_input_frames_available>`

**Thử nghiệm:** Phương thức này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Trả về số frame hiện có để đọc bằng :ref:`get_input_frames()<class_AudioServer_method_get_input_frames>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_input_mix_rate:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_input_mix_rate**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_input_mix_rate>`

Trả về sample rate tại đầu vào của **AudioServer**.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_mix_rate:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_mix_rate**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_mix_rate>`

Trả về sample rate tại đầu ra của **AudioServer**.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_output_device_list:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_output_device_list**\ (\ ) :ref:`🔗<class_AudioServer_method_get_output_device_list>`

Trả về tên của tất cả thiết bị đầu ra âm thanh được phát hiện trên hệ thống.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_output_latency:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_output_latency**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_output_latency>`

Trả về độ trễ đầu ra hiệu dụng của audio driver. Giá trị này dựa trên :ref:`ProjectSettings.audio/driver/output_latency<class_ProjectSettings_property_audio/driver/output_latency>`, nhưng giá trị trả về chính xác sẽ khác nhau tùy thuộc vào hệ điều hành và audio driver.

\ **Lưu ý:** Thao tác này có thể tốn tài nguyên; không nên gọi :ref:`get_output_latency()<class_AudioServer_method_get_output_latency>` ở mỗi frame.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_speaker_mode:

.. rst-class:: classref-method

:ref:`SpeakerMode<enum_AudioServer_SpeakerMode>` **get_speaker_mode**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_speaker_mode>`

Trả về cấu hình loa.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_time_since_last_mix:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_time_since_last_mix**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_time_since_last_mix>`

Trả về thời gian tương đối kể từ lần mix gần nhất, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_get_time_to_next_mix:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_time_to_next_mix**\ (\ ) |const| :ref:`🔗<class_AudioServer_method_get_time_to_next_mix>`

Trả về thời gian tương đối cho đến lần mix tiếp theo, tính bằng giây.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_is_bus_bypassing_effects:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_bus_bypassing_effects**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_is_bus_bypassing_effects>`

Nếu ``true``, bus tại chỉ mục ``bus_idx`` đang bỏ qua các effect.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_is_bus_effect_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_bus_effect_enabled**\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_is_bus_effect_enabled>`

Nếu ``true``, effect tại chỉ mục ``effect_idx`` trên bus tại chỉ mục ``bus_idx`` được bật.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_is_bus_mute:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_bus_mute**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_is_bus_mute>`

Nếu ``true``, bus tại chỉ mục ``bus_idx`` bị tắt tiếng.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_is_bus_solo:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_bus_solo**\ (\ bus_idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioServer_method_is_bus_solo>`

Nếu ``true``, bus tại index ``bus_idx`` đang ở chế độ solo.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_is_stream_registered_as_sample:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_stream_registered_as_sample**\ (\ stream\: :ref:`AudioStream<class_AudioStream>`\ ) :ref:`🔗<class_AudioServer_method_is_stream_registered_as_sample>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Nếu ``true``, stream được đăng ký dưới dạng sample. Engine sẽ không phải đăng ký nó trước khi phát sample.

Nếu ``false``, stream sẽ phải được đăng ký trước khi phát. Để tránh các đợt lag đột biến, hãy đăng ký stream dưới dạng sample bằng :ref:`register_stream_as_sample()<class_AudioServer_method_register_stream_as_sample>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_lock:

.. rst-class:: classref-method

|void| **lock**\ (\ ) :ref:`🔗<class_AudioServer_method_lock>`

Khóa vòng lặp chính của audio driver.

\ **Lưu ý:** Hãy nhớ mở khóa sau đó.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_move_bus:

.. rst-class:: classref-method

|void| **move_bus**\ (\ index\: :ref:`int<class_int>`, to_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_move_bus>`

Di chuyển bus từ index ``index`` đến index ``to_index``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_register_stream_as_sample:

.. rst-class:: classref-method

|void| **register_stream_as_sample**\ (\ stream\: :ref:`AudioStream<class_AudioStream>`\ ) :ref:`🔗<class_AudioServer_method_register_stream_as_sample>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Buộc đăng ký một stream dưới dạng sample.

\ **Lưu ý:** Có thể xảy ra các đợt lag đột biến khi gọi phương thức này, đặc biệt trong các bản build đơn luồng. Bạn nên gọi phương thức này trong khi tải asset, khi đó đợt lag đột biến có thể được che giấu, thay vì đăng ký sample ngay trước khi cần phát nó.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_remove_bus:

.. rst-class:: classref-method

|void| **remove_bus**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_remove_bus>`

Xóa bus tại index ``index``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_remove_bus_effect:

.. rst-class:: classref-method

|void| **remove_bus_effect**\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_remove_bus_effect>`

Xóa effect tại index ``effect_idx`` khỏi bus tại index ``bus_idx``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_bypass_effects:

.. rst-class:: classref-method

|void| **set_bus_bypass_effects**\ (\ bus_idx\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_bypass_effects>`

Nếu ``true``, bus tại index ``bus_idx`` đang bypass các effect.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_effect_enabled:

.. rst-class:: classref-method

|void| **set_bus_effect_enabled**\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`, enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_effect_enabled>`

Nếu ``true``, effect tại index ``effect_idx`` trên bus tại index ``bus_idx`` được bật.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_layout:

.. rst-class:: classref-method

|void| **set_bus_layout**\ (\ bus_layout\: :ref:`AudioBusLayout<class_AudioBusLayout>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_layout>`

Ghi đè :ref:`AudioBusLayout<class_AudioBusLayout>` hiện đang được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_mute:

.. rst-class:: classref-method

|void| **set_bus_mute**\ (\ bus_idx\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_mute>`

Nếu ``true``, bus tại index ``bus_idx`` bị tắt tiếng.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_name:

.. rst-class:: classref-method

|void| **set_bus_name**\ (\ bus_idx\: :ref:`int<class_int>`, name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_name>`

Đặt tên của bus tại index ``bus_idx`` thành ``name``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_send:

.. rst-class:: classref-method

|void| **set_bus_send**\ (\ bus_idx\: :ref:`int<class_int>`, send\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_send>`

Kết nối đầu ra của bus tại ``bus_idx`` với bus có tên ``send``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_solo:

.. rst-class:: classref-method

|void| **set_bus_solo**\ (\ bus_idx\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_solo>`

Nếu ``true``, bus tại index ``bus_idx`` đang ở chế độ solo.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_volume_db:

.. rst-class:: classref-method

|void| **set_bus_volume_db**\ (\ bus_idx\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_volume_db>`

Đặt âm lượng theo decibel của bus tại index ``bus_idx`` thành ``volume_db``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_bus_volume_linear:

.. rst-class:: classref-method

|void| **set_bus_volume_linear**\ (\ bus_idx\: :ref:`int<class_int>`, volume_linear\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioServer_method_set_bus_volume_linear>`

Đặt âm lượng dưới dạng giá trị tuyến tính của bus tại index ``bus_idx`` thành ``volume_linear``.

\ **Lưu ý:** Việc sử dụng phương thức này tương đương với việc gọi :ref:`set_bus_volume_db()<class_AudioServer_method_set_bus_volume_db>` với kết quả của :ref:`@GlobalScope.linear_to_db()<class_@GlobalScope_method_linear_to_db>` trên một giá trị.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_enable_tagging_used_audio_streams:

.. rst-class:: classref-method

|void| **set_enable_tagging_used_audio_streams**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioServer_method_set_enable_tagging_used_audio_streams>`

Nếu được đặt thành ``true``, tất cả các instance của :ref:`AudioStreamPlayback<class_AudioStreamPlayback>` sẽ gọi :ref:`AudioStreamPlayback._tag_used_streams()<class_AudioStreamPlayback_private_method__tag_used_streams>` ở mỗi bước mix.

\ **Lưu ý:** Tính năng này được bật theo mặc định trong editor vì được các plugin của editor sử dụng cho phần xem trước audio stream.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_set_input_device_active:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **set_input_device_active**\ (\ active\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_AudioServer_method_set_input_device_active>`

**Thử nghiệm:** Phương thức này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

Nếu ``active`` là ``true``, bắt đầu microphone input stream được chỉ định bởi :ref:`input_device<class_AudioServer_property_input_device>` hoặc trả về lỗi nếu không thành công.

Nếu ``active`` là ``false``, dừng input stream nếu nó đang chạy.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_swap_bus_effects:

.. rst-class:: classref-method

|void| **swap_bus_effects**\ (\ bus_idx\: :ref:`int<class_int>`, effect_idx\: :ref:`int<class_int>`, by_effect_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioServer_method_swap_bus_effects>`

Hoán đổi vị trí của hai effect trong bus ``bus_idx``.

.. rst-class:: classref-item-separator

----

.. _class_AudioServer_method_unlock:

.. rst-class:: classref-method

|void| **unlock**\ (\ ) :ref:`🔗<class_AudioServer_method_unlock>`

Mở khóa vòng lặp chính của audio driver. (Sau khi khóa, bạn luôn phải mở khóa.)

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
