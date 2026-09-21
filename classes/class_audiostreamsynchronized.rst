:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/interactive_music/doc_classes/AudioStreamSynchronized.xml.

.. _class_AudioStreamSynchronized:

AudioStreamSynchronized
=======================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Stream có thể được gắn các sub-stream và chúng sẽ được phát đồng bộ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là một stream có thể được gắn các sub-stream và chúng sẽ được phát đồng bộ. Các stream bắt đầu chính xác cùng một thời điểm khi nhấn play và sẽ kết thúc khi stream cuối cùng kết thúc. Nếu một trong các sub-stream lặp lại, quá trình phát sẽ tiếp tục.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`stream_count<class_AudioStreamSynchronized_property_stream_count>` | ``0`` |
   +-----------------------+--------------------------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AudioStream<class_AudioStream>` | :ref:`get_sync_stream<class_AudioStreamSynchronized_method_get_sync_stream>`\ (\ stream_index\: :ref:`int<class_int>`\ ) |const|                                               |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`             | :ref:`get_sync_stream_volume<class_AudioStreamSynchronized_method_get_sync_stream_volume>`\ (\ stream_index\: :ref:`int<class_int>`\ ) |const|                                 |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_sync_stream<class_AudioStreamSynchronized_method_set_sync_stream>`\ (\ stream_index\: :ref:`int<class_int>`, audio_stream\: :ref:`AudioStream<class_AudioStream>`\ ) |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_sync_stream_volume<class_AudioStreamSynchronized_method_set_sync_stream_volume>`\ (\ stream_index\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ )  |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_AudioStreamSynchronized_constant_MAX_STREAMS:

.. rst-class:: classref-constant

**MAX_STREAMS** = ``32`` :ref:`🔗<class_AudioStreamSynchronized_constant_MAX_STREAMS>`

Số lượng stream tối đa có thể được đồng bộ hóa.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamSynchronized_property_stream_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **stream_count** = ``0`` :ref:`🔗<class_AudioStreamSynchronized_property_stream_count>`

.. rst-class:: classref-property-setget

- |void| **set_stream_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_stream_count**\ (\ )

Đặt tổng số stream sẽ được phát lại đồng bộ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_AudioStreamSynchronized_method_get_sync_stream:

.. rst-class:: classref-method

:ref:`AudioStream<class_AudioStream>` **get_sync_stream**\ (\ stream_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamSynchronized_method_get_sync_stream>`

Lấy một trong các stream được đồng bộ hóa theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamSynchronized_method_get_sync_stream_volume:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_sync_stream_volume**\ (\ stream_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_AudioStreamSynchronized_method_get_sync_stream_volume>`

Lấy âm lượng của một trong các stream được đồng bộ hóa theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamSynchronized_method_set_sync_stream:

.. rst-class:: classref-method

|void| **set_sync_stream**\ (\ stream_index\: :ref:`int<class_int>`, audio_stream\: :ref:`AudioStream<class_AudioStream>`\ ) :ref:`🔗<class_AudioStreamSynchronized_method_set_sync_stream>`

Đặt một trong các stream được đồng bộ hóa theo chỉ mục.

.. rst-class:: classref-item-separator

----

.. _class_AudioStreamSynchronized_method_set_sync_stream_volume:

.. rst-class:: classref-method

|void| **set_sync_stream_volume**\ (\ stream_index\: :ref:`int<class_int>`, volume_db\: :ref:`float<class_float>`\ ) :ref:`🔗<class_AudioStreamSynchronized_method_set_sync_stream_volume>`

Đặt âm lượng của một trong các stream được đồng bộ hóa theo chỉ mục.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
