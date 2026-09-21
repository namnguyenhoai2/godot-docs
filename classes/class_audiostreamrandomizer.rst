:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamRandomizer.xml.

.. _class_AudioStreamRandomizer:

AudioStreamRandomizer
=====================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Bọc một pool các audio stream với tính năng thay đổi pitch và volume.

.. rst-class:: classref-introduction-group

Mô tả
-----

Chọn ngẫu nhiên một AudioStream từ pool, tùy thuộc vào playback mode, rồi áp dụng thay đổi pitch và volume ngẫu nhiên trong khi phát.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>` | :ref:`playback_mode<class_AudioStreamRandomizer_property_playback_mode>`                     | ``0``   |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                                    | :ref:`random_pitch<class_AudioStreamRandomizer_property_random_pitch>`                       | ``1.0`` |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                                    | :ref:`random_pitch_semitones<class_AudioStreamRandomizer_property_random_pitch_semitones>`   | ``0.0`` |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                                    | :ref:`random_volume_offset_db<class_AudioStreamRandomizer_property_random_volume_offset_db>` | ``0.0`` |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`AudioStream<class_AudioStream>`                        | :ref:`stream_{index}/stream<class_AudioStreamRandomizer_property_stream_{index}/stream>`     |         |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                                    | :ref:`stream_{index}/weight<class_AudioStreamRandomizer_property_stream_{index}/weight>`     | ``1.0`` |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+
   | :ref:`int<class_int>`                                        | :ref:`streams_count<class_AudioStreamRandomizer_property_streams_count>`                     | ``0``   |
   +--------------------------------------------------------------+----------------------------------------------------------------------------------------------+---------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`add_stream<class_AudioStreamRandomizer_method_add_stream>`\ (\ index\: :ref:`int<class_int>`, stream\: :ref:`AudioStream<class_AudioStream>`, weight\: :ref:`float<class_float>` = 1.0\ ) |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStream<class_AudioStream>` | :ref:`get_stream<class_AudioStreamRandomizer_method_get_stream>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                                                                   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`             | :ref:`get_stream_probability_weight<class_AudioStreamRandomizer_method_get_stream_probability_weight>`\ (\ index\: :ref:`int<class_int>`\ ) |const|                                             |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`move_stream<class_AudioStreamRandomizer_method_move_stream>`\ (\ index_from\: :ref:`int<class_int>`, index_to\: :ref:`int<class_int>`\ )                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`remove_stream<class_AudioStreamRandomizer_method_remove_stream>`\ (\ index\: :ref:`int<class_int>`\ )                                                                                     |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_stream<class_AudioStreamRandomizer_method_set_stream>`\ (\ index\: :ref:`int<class_int>`, stream\: :ref:`AudioStream<class_AudioStream>`\ )                                           |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_stream_probability_weight<class_AudioStreamRandomizer_method_set_stream_probability_weight>`\ (\ index\: :ref:`int<class_int>`, weight\: :ref:`float<class_float>`\ )                 |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumerations
------------

.. _enum_AudioStreamRandomizer_PlaybackMode:

.. rst-class:: classref-enumeration

enum **PlaybackMode**: :ref:`🔗<enum_AudioStreamRandomizer_PlaybackMode>`

.. _class_AudioStreamRandomizer_constant_PLAYBACK_RANDOM_NO_REPEATS:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>` **PLAYBACK_RANDOM_NO_REPEATS** = ``0``

Chọn ngẫu nhiên một stream theo các trọng số xác suất được chọn cho từng stream, nhưng tránh phát cùng một stream hai lần liên tiếp whenever possible. Nếu pool chỉ có 1 sound, sound đó sẽ luôn được phát, cho phép việc lặp lại xảy ra.

.. _class_AudioStreamRandomizer_constant_PLAYBACK_RANDOM:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>` **PLAYBACK_RANDOM** = ``1``

Chọn ngẫu nhiên một stream theo các trọng số xác suất được chọn cho từng stream. Nếu pool chỉ có 1 sound, sound đó sẽ luôn được phát.

.. _class_AudioStreamRandomizer_constant_PLAYBACK_SEQUENTIAL:

.. rst-class:: classref-enumeration-constant

:ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>` **PLAYBACK_SEQUENTIAL** = ``2``

Phát các stream theo thứ tự xuất hiện trong stream pool. Nếu pool chỉ có 1 sound, sound đó sẽ luôn được phát.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_AudioStreamRandomizer_property_playback_mode:

.. rst-class:: classref-property

:ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>` **playback_mode** = ``0`` :ref:`🔗<class_AudioStreamRandomizer_property_playback_mode>`

.. rst-class:: classref-property-setget

- |void| **set_playback_mode**\ (\ value\: :ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>`\ ) - :ref:`PlaybackMode<enum_AudioStreamRandomizer_PlaybackMode>` **get_playback_mode**\ (\ )

Điều khiển cách AudioStreamRandomizer chọn AudioStream để phát tiếp theo.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_property_random_pitch:

.. rst-class:: classref-property

:ref:`float<class_float>` **random_pitch** = ``1.0`` :ref:`🔗<class_AudioStreamRandomizer_property_random_pitch>`

.. rst-class:: classref-property-setget

- |void| **set_random_pitch**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_random_pitch**\ (\ )

Hệ số tần số lớn nhất có thể có của biến thiên pitch ngẫu nhiên. Pitch sẽ được chọn ngẫu nhiên trong phạm vi từ ``1.0 / random_pitch`` đến ``random_pitch``. Giá trị ``1.0`` nghĩa là không có biến thiên. Giá trị ``2.0`` nghĩa là pitch sẽ được chọn ngẫu nhiên trong khoảng từ gấp đôi đến một nửa.

\ **Lưu ý:** Việc thiết lập property này cũng thiết lập :ref:`random_pitch_semitones<class_AudioStreamRandomizer_property_random_pitch_semitones>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_property_random_pitch_semitones:

.. rst-class:: classref-property

:ref:`float<class_float>` **random_pitch_semitones** = ``0.0`` :ref:`🔗<class_AudioStreamRandomizer_property_random_pitch_semitones>`

.. rst-class:: classref-property-setget

- |void| **set_random_pitch_semitones**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_random_pitch_semitones**\ (\ )

Khoảng cách lớn nhất có thể có, tính bằng semitone, của biến thiên pitch ngẫu nhiên. Giá trị ``0.0`` nghĩa là không có biến thiên.

\ **Lưu ý:** Việc thiết lập property này cũng thiết lập :ref:`random_pitch<class_AudioStreamRandomizer_property_random_pitch>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_property_random_volume_offset_db:

.. rst-class:: classref-property

:ref:`float<class_float>` **random_volume_offset_db** = ``0.0`` :ref:`🔗<class_AudioStreamRandomizer_property_random_volume_offset_db>`

.. rst-class:: classref-property-setget

- |void| **set_random_volume_offset_db**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_random_volume_offset_db**\ (\ )

Cường độ của biến thiên volume ngẫu nhiên. Volume sẽ được tăng hoặc giảm một giá trị ngẫu nhiên tối đa ``random_volume_offset_db``. Giá trị ``0.0`` nghĩa là không có biến thiên. Giá trị ``3.0`` nghĩa là volume sẽ được chọn ngẫu nhiên trong khoảng từ ``-3.0 dB`` đến ``+3.0 dB``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_property_stream_{index}/stream:

.. rst-class:: classref-property

:ref:`AudioStream<class_AudioStream>` **stream_{index}/stream** :ref:`🔗<class_AudioStreamRandomizer_property_stream_{index}/stream>`

:ref:`AudioStream<class_AudioStream>` tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. streams_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_property_stream_{index}/weight:

.. rst-class:: classref-property

:ref:`float<class_float>` **stream_{index}/weight** = ``1.0`` :ref:`🔗<class_AudioStreamRandomizer_property_stream_{index}/weight>`

Trọng số xác suất của :ref:`AudioStream<class_AudioStream>` tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. streams_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_property_streams_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **streams_count** = ``0`` :ref:`🔗<class_AudioStreamRandomizer_property_streams_count>`

.. rst-class:: classref-property-setget

- |void| **set_streams_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_streams_count**\ (\ )

Số lượng stream trong stream pool.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_AudioStreamRandomizer_method_add_stream:

.. rst-class:: classref-method

|void| **add_stream**\ (\ index\: :ref:`int<class_int>`, stream\: :ref:`AudioStream<class_AudioStream>`, weight\: :ref:`float<class_float>` = 1.0\ ) :ref:`🔗<class_AudioStreamRandomizer_method_add_stream>`

Chèn một stream tại index được chỉ định. Nếu index nhỏ hơn 0, thao tác chèn sẽ diễn ra ở cuối pool bên dưới.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_method_get_stream:

.. rst-class:: classref-method

:ref:`AudioStream<class_AudioStream>` **get_stream**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamRandomizer_method_get_stream>`

Trả về stream tại index được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_method_get_stream_probability_weight:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_stream_probability_weight**\ (\ index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamRandomizer_method_get_stream_probability_weight>`

Trả về trọng số xác suất liên kết với stream tại index đã cho.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_method_move_stream:

.. rst-class:: classref-method

|void| **move_stream**\ (\ index_from\: :ref:`int<class_int>`, index_to\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioStreamRandomizer_method_move_stream>`

Di chuyển một stream từ index này sang index khác.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_method_remove_stream:

.. rst-class:: classref-method

|void| **remove_stream**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_AudioStreamRandomizer_method_remove_stream>`

Xóa stream tại index được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_method_set_stream:

.. rst-class:: classref-method

|void| **set_stream**\ (\ index\: :ref:`int<class_int>`, stream\: :ref:`AudioStream<class_AudioStream>`\ ) :ref:`🔗<class_AudioStreamRandomizer_method_set_stream>`

Đặt AudioStream tại index được chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamRandomizer_method_set_stream_probability_weight:

.. rst-class:: classref-method

|void| **set_stream_probability_weight**\ (\ index\: :ref:`int<class_int>`, weight\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamRandomizer_method_set_stream_probability_weight>`

Đặt trọng số xác suất của stream tại index được chỉ định. Giá trị này càng cao thì randomizer càng có khả năng chọn stream này trong các playback mode ngẫu nhiên.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
