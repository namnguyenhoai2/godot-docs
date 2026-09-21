:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/AudioStreamPolyphonic.xml.

.. _class_AudioStreamPolyphonic:

AudioStreamPolyphonic
=====================

**Kế thừa:** :ref:`AudioStream<class_AudioStream>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

AudioStream cho phép người dùng phát các stream tùy chỉnh bất kỳ lúc nào từ code, đồng thời sử dụng một player duy nhất.

.. rst-class:: classref-introduction-group

Mô tả
-----

AudioStream cho phép người dùng phát các stream tùy chỉnh bất kỳ lúc nào từ code, đồng thời sử dụng một player duy nhất.

Việc điều khiển playback được thực hiện thông qua instance :ref:`AudioStreamPlaybackPolyphonic<class_AudioStreamPlaybackPolyphonic>` được thiết lập bên trong player, có thể lấy được bằng các phương thức :ref:`AudioStreamPlayer.get_stream_playback()<class_AudioStreamPlayer_method_get_stream_playback>`, :ref:`AudioStreamPlayer2D.get_stream_playback()<class_AudioStreamPlayer2D_method_get_stream_playback>` hoặc :ref:`AudioStreamPlayer3D.get_stream_playback()<class_AudioStreamPlayer3D_method_get_stream_playback>`. Chỉ có thể lấy instance playback sau khi thuộc tính ``stream`` được thiết lập thành **AudioStreamPolyphonic** trong các player đó.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Audio streams <../tutorials/audio/audio_streams>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+------------------------------------------------------------------+--------+
   | :ref:`int<class_int>` | :ref:`polyphony<class_AudioStreamPolyphonic_property_polyphony>` | ``32`` |
   +-----------------------+------------------------------------------------------------------+--------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AudioStreamPolyphonic_property_polyphony:

.. rst-class:: classref-property

:ref:`int<class_int>` **polyphony** = ``32`` :ref:`🔗<class_AudioStreamPolyphonic_property_polyphony>`

.. rst-class:: classref-property-setget

- |void| **set_polyphony**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_polyphony**\ (\ )

Số lượng stream đồng thời tối đa có thể phát.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
