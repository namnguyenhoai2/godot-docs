:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/vorbis/doc_classes/AudioStreamOggVorbis.xml.

.. _class_AudioStreamOggVorbis:

AudioStreamOggVorbis
====================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một class đại diện cho audio stream Ogg Vorbis.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class AudioStreamOggVorbis là một :ref:`AudioStream<class_AudioStream>` chuyên dụng để xử lý các định dạng tệp Ogg Vorbis. Class này cung cấp chức năng tải và phát lại các tệp Ogg Vorbis, cũng như quản lý việc lặp và các thuộc tính phát lại khác. Bạn có thể tìm thêm thông tin trong :ref:`ResourceImporterOggVorbis<class_ResourceImporterOggVorbis>`.

Class này thuộc hệ thống audio stream, hệ thống cũng hỗ trợ các tệp WAV thông qua class :ref:`AudioStreamWAV<class_AudioStreamWAV>` và các tệp MP3 thông qua class :ref:`AudioStreamMP3<class_AudioStreamMP3>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

- :doc:`Runtime file loading and saving <../tutorials/io/runtime_file_loading_and_saving>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                             | :ref:`bar_beats<class_AudioStreamOggVorbis_property_bar_beats>`             | ``4``     |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                             | :ref:`beat_count<class_AudioStreamOggVorbis_property_beat_count>`           | ``0``     |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`bpm<class_AudioStreamOggVorbis_property_bpm>`                         | ``0.0``   |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                           | :ref:`loop<class_AudioStreamOggVorbis_property_loop>`                       | ``false`` |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                         | :ref:`loop_offset<class_AudioStreamOggVorbis_property_loop_offset>`         | ``0.0``   |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`OggPacketSequence<class_OggPacketSequence>` | :ref:`packet_sequence<class_AudioStreamOggVorbis_property_packet_sequence>` |           |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`tags<class_AudioStreamOggVorbis_property_tags>`                       | ``{}``    |
   +---------------------------------------------------+-----------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>` | :ref:`load_from_buffer<class_AudioStreamOggVorbis_method_load_from_buffer>`\ (\ stream_data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |static| |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>` | :ref:`load_from_file<class_AudioStreamOggVorbis_method_load_from_file>`\ (\ path\: :ref:`String<class_String>`\ ) |static|                              |
   +---------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamOggVorbis_property_bar_beats:

.. rst-class:: classref-property

:ref:`int<class_int>` **bar_beats** = ``4`` :ref:`🔗<class_AudioStreamOggVorbis_property_bar_beats>`

.. rst-class:: classref-property-setget

- |void| **set_bar_beats**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bar_beats**\ (\ )

Số nhịp trong một ô nhịp của audio track.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_property_beat_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **beat_count** = ``0`` :ref:`🔗<class_AudioStreamOggVorbis_property_beat_count>`

.. rst-class:: classref-property-setget

- |void| **set_beat_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_beat_count**\ (\ )

Độ dài của audio track, tính theo nhịp. Thời lượng thực tế của tệp âm thanh có thể dài hơn giá trị được chỉ định bởi thuộc tính này. Thuộc tính này xác định điểm kết thúc của audio để lặp, :ref:`AudioStreamPlaylist<class_AudioStreamPlaylist>`, và :ref:`AudioStreamInteractive<class_AudioStreamInteractive>`.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_property_bpm:

.. rst-class:: classref-property

:ref:`float<class_float>` **bpm** = ``0.0`` :ref:`🔗<class_AudioStreamOggVorbis_property_bpm>`

.. rst-class:: classref-property-setget

- |void| **set_bpm**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bpm**\ (\ )

Tempo của audio track, được đo bằng số nhịp mỗi phút.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_property_loop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **loop** = ``false`` :ref:`🔗<class_AudioStreamOggVorbis_property_loop>`

.. rst-class:: classref-property-setget

- |void| **set_loop**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_loop**\ (\ )

Nếu ``true``, stream sẽ phát lại từ :ref:`loop_offset<class_AudioStreamOggVorbis_property_loop_offset>` đã chỉ định khi đạt đến cuối audio track hoặc khi đạt đến cuối nhịp cuối cùng theo số lượng được chỉ định trong :ref:`beat_count<class_AudioStreamOggVorbis_property_beat_count>`. Hữu ích cho âm thanh môi trường và nhạc nền.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_property_loop_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **loop_offset** = ``0.0`` :ref:`🔗<class_AudioStreamOggVorbis_property_loop_offset>`

.. rst-class:: classref-property-setget

- |void| **set_loop_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_loop_offset**\ (\ )

Thời điểm tính bằng giây mà stream bắt đầu sau khi được lặp.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_property_packet_sequence:

.. rst-class:: classref-property

:ref:`OggPacketSequence<class_OggPacketSequence>` **packet_sequence** :ref:`🔗<class_AudioStreamOggVorbis_property_packet_sequence>`

.. rst-class:: classref-property-setget

- |void| **set_packet_sequence**\ (\ value\: :ref:`OggPacketSequence<class_OggPacketSequence>`\ ) - :ref:`OggPacketSequence<class_OggPacketSequence>` **get_packet_sequence**\ (\ )

Chứa dữ liệu Ogg thô của stream này.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_property_tags:

.. rst-class:: classref-property

:ref:`Dictionary<class_Dictionary>` **tags** = ``{}`` :ref:`🔗<class_AudioStreamOggVorbis_property_tags>`

.. rst-class:: classref-property-setget

- |void| **set_tags**\ (\ value\: :ref:`Dictionary<class_Dictionary>`\ ) - :ref:`Dictionary<class_Dictionary>` **get_tags**\ (\ )

Chứa các tag do người dùng định nghĩa nếu được tìm thấy trong dữ liệu Ogg Vorbis.

Các tag thường được sử dụng bao gồm ``title``, ``artist``, ``album``, ``tracknumber`` và ``date`` (``date`` không có định dạng ngày tiêu chuẩn).

\ **Lưu ý:** Không có tag nào được *đảm bảo* luôn có mặt trong mọi tệp, vì vậy hãy đảm bảo xử lý trường hợp các key không tồn tại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamOggVorbis_method_load_from_buffer:

.. rst-class:: classref-method

:ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>` **load_from_buffer**\ (\ stream_data\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |static| :ref:`🔗<class_AudioStreamOggVorbis_method_load_from_buffer>`

Tạo một instance **AudioStreamOggVorbis** mới từ buffer được cung cấp. Buffer phải chứa dữ liệu Ogg Vorbis.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamOggVorbis_method_load_from_file:

.. rst-class:: classref-method

:ref:`AudioStreamOggVorbis<class_AudioStreamOggVorbis>` **load_from_file**\ (\ path\: :ref:`String<class_String>`\ ) |static| :ref:`🔗<class_AudioStreamOggVorbis_method_load_from_file>`

Tạo một instance **AudioStreamOggVorbis** mới từ đường dẫn tệp được cung cấp. Tệp phải ở định dạng Ogg Vorbis.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
