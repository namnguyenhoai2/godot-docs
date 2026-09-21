:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PacketPeerStream.xml.

.. _class_PacketPeerStream:

PacketPeerStream
================

**Kế thừa:** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Wrapper để sử dụng một PacketPeer trên một StreamPeer.

.. rst-class:: classref-introduction-group

Mô tả
-----

PacketStreamPeer cung cấp một wrapper để làm việc với các packet trên một stream. Điều này cho phép sử dụng code dựa trên packet với các StreamPeer. PacketPeerStream triển khai một protocol tùy chỉnh trên StreamPeer, vì vậy người dùng không nên đọc hoặc ghi trực tiếp vào StreamPeer được bọc.

\ **Lưu ý:** Khi export sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi hình thức giao tiếp mạng.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`               | :ref:`input_buffer_max_size<class_PacketPeerStream_property_input_buffer_max_size>`   | ``65532`` |
   +-------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`               | :ref:`output_buffer_max_size<class_PacketPeerStream_property_output_buffer_max_size>` | ``65532`` |
   +-------------------------------------+---------------------------------------------------------------------------------------+-----------+
   | :ref:`StreamPeer<class_StreamPeer>` | :ref:`stream_peer<class_PacketPeerStream_property_stream_peer>`                       |           |
   +-------------------------------------+---------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PacketPeerStream_property_input_buffer_max_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **input_buffer_max_size** = ``65532`` :ref:`🔗<class_PacketPeerStream_property_input_buffer_max_size>`

.. rst-class:: classref-property-setget

- |void| **set_input_buffer_max_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_input_buffer_max_size**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerStream_property_output_buffer_max_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **output_buffer_max_size** = ``65532`` :ref:`🔗<class_PacketPeerStream_property_output_buffer_max_size>`

.. rst-class:: classref-property-setget

- |void| **set_output_buffer_max_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_output_buffer_max_size**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerStream_property_stream_peer:

.. rst-class:: classref-property

:ref:`StreamPeer<class_StreamPeer>` **stream_peer** :ref:`🔗<class_PacketPeerStream_property_stream_peer>`

.. rst-class:: classref-property-setget

- |void| **set_stream_peer**\ (\ value\: :ref:`StreamPeer<class_StreamPeer>`\ ) - :ref:`StreamPeer<class_StreamPeer>` **get_stream_peer**\ (\ )

Đối tượng :ref:`StreamPeer<class_StreamPeer>` được bọc.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
