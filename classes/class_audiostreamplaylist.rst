:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/interactive_music/doc_classes/AudioStreamPlaylist.xml.

.. _class_AudioStreamPlaylist:

AudioStreamPlaylist
===================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

:ref:`AudioStream<class_AudioStream>` that includes sub-streams and plays them back like a playlist.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một audio stream có thể phát các stream con theo thứ tự. Có thể thêm stream vào Playlist bằng :ref:`set_list_stream()<class_AudioStreamPlaylist_method_set_list_stream>` và xáo trộn bằng :ref:`shuffle<class_AudioStreamPlaylist_property_shuffle>`.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>` | :ref:`fade_time<class_AudioStreamPlaylist_property_fade_time>`       | ``0.3``   |
   +---------------------------+----------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`loop<class_AudioStreamPlaylist_property_loop>`                 | ``true``  |
   +---------------------------+----------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`   | :ref:`shuffle<class_AudioStreamPlaylist_property_shuffle>`           | ``false`` |
   +---------------------------+----------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`     | :ref:`stream_count<class_AudioStreamPlaylist_property_stream_count>` | ``0``     |
   +---------------------------+----------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`             | :ref:`get_bpm<class_AudioStreamPlaylist_method_get_bpm>`\ (\ ) |const|                                                                                                     |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStream<class_AudioStream>` | :ref:`get_list_stream<class_AudioStreamPlaylist_method_get_list_stream>`\ (\ stream_index\: :ref:`int<class_int>`\ ) |const|                                               |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_list_stream<class_AudioStreamPlaylist_method_set_list_stream>`\ (\ stream_index\: :ref:`int<class_int>`, audio_stream\: :ref:`AudioStream<class_AudioStream>`\ ) |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_AudioStreamPlaylist_constant_MAX_STREAMS:

.. rst-class:: classref-constant

**MAX_STREAMS** = ``64`` :ref:`🔗<class_AudioStreamPlaylist_constant_MAX_STREAMS>`

Số lượng stream tối đa được hỗ trợ trong playlist.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamPlaylist_property_fade_time:

.. rst-class:: classref-property

:ref:`float<class_float>` **fade_time** = ``0.3`` :ref:`🔗<class_AudioStreamPlaylist_property_fade_time>`

.. rst-class:: classref-property-setget

- |void| **set_fade_time**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_fade_time**\ (\ )

Thời gian fade được sử dụng khi một stream kết thúc và chuyển sang stream tiếp theo. Các stream được kỳ vọng có thêm một đoạn âm thanh sau phần kết thúc để hỗ trợ fade.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaylist_property_loop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **loop** = ``true`` :ref:`🔗<class_AudioStreamPlaylist_property_loop>`

.. rst-class:: classref-property-setget

- |void| **set_loop**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **has_loop**\ (\ )

Nếu ``true``, playlist sẽ lặp lại; nếu không, playlist sẽ kết thúc khi stream cuối cùng phát xong.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaylist_property_shuffle:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **shuffle** = ``false`` :ref:`🔗<class_AudioStreamPlaylist_property_shuffle>`

.. rst-class:: classref-property-setget

- |void| **set_shuffle**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_shuffle**\ (\ )

Nếu ``true``, playlist sẽ xáo trộn mỗi khi bắt đầu phát và mỗi khi lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaylist_property_stream_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **stream_count** = ``0`` :ref:`🔗<class_AudioStreamPlaylist_property_stream_count>`

.. rst-class:: classref-property-setget

- |void| **set_stream_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_stream_count**\ (\ )

Số lượng stream trong playlist.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamPlaylist_method_get_bpm:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_bpm**\ (\ ) |const| :ref:`🔗<class_AudioStreamPlaylist_method_get_bpm>`

Trả về BPM của playlist, giá trị này có thể thay đổi tùy thuộc vào clip đang được phát.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaylist_method_get_list_stream:

.. rst-class:: classref-method

:ref:`AudioStream<class_AudioStream>` **get_list_stream**\ (\ stream_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamPlaylist_method_get_list_stream>`

Trả về stream tại vị trí phát có chỉ mục index.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamPlaylist_method_set_list_stream:

.. rst-class:: classref-method

|void| **set_list_stream**\ (\ stream_index\: :ref:`int<class_int>`, audio_stream\: :ref:`AudioStream<class_AudioStream>`\ ) :ref:`🔗<class_AudioStreamPlaylist_method_set_list_stream>`

Đặt stream tại vị trí phát có chỉ mục index.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
