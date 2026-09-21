:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PacketPeer.xml.

.. _class_PacketPeer:

PacketPeer
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ENetPacketPeer<class_ENetPacketPeer>`, :ref:`MultiplayerPeer<class_MultiplayerPeer>`, :ref:`PacketPeerDTLS<class_PacketPeerDTLS>`, :ref:`PacketPeerExtension<class_PacketPeerExtension>`, :ref:`PacketPeerStream<class_PacketPeerStream>`, :ref:`PacketPeerUDP<class_PacketPeerUDP>`, :ref:`WebRTCDataChannel<class_WebRTCDataChannel>`, :ref:`WebSocketPeer<class_WebSocketPeer>`

Lớp trừu tượng và lớp cơ sở cho các giao thức dựa trên gói tin.

.. rst-class:: classref-introduction-group

Mô tả
-----

PacketPeer là lớp trừu tượng và lớp cơ sở cho các giao thức dựa trên gói tin (chẳng hạn như UDP). Lớp này cung cấp API để gửi và nhận các gói tin dưới dạng dữ liệu thô hoặc biến. Điều này giúp dễ dàng truyền dữ liệu qua một giao thức mà không cần mã hóa dữ liệu thành các byte cấp thấp hoặc phải lo lắng về thứ tự mạng.

\ **Lưu ý:** Khi export sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi loại giao tiếp mạng.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+---------------------------------------------------------------------------------+-------------+
   | :ref:`int<class_int>` | :ref:`encode_buffer_max_size<class_PacketPeer_property_encode_buffer_max_size>` | ``8388608`` |
   +-----------------------+---------------------------------------------------------------------------------+-------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                         | :ref:`get_available_packet_count<class_PacketPeer_method_get_available_packet_count>`\ (\ ) |const|                                        |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>` | :ref:`get_packet<class_PacketPeer_method_get_packet>`\ (\ )                                                                                |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`         | :ref:`get_packet_error<class_PacketPeer_method_get_packet_error>`\ (\ ) |const|                                                            |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                 | :ref:`get_var<class_PacketPeer_method_get_var>`\ (\ allow_objects\: :ref:`bool<class_bool>` = false\ )                                     |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`         | :ref:`put_packet<class_PacketPeer_method_put_packet>`\ (\ buffer\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                        |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`         | :ref:`put_var<class_PacketPeer_method_put_var>`\ (\ var\: :ref:`Variant<class_Variant>`, full_objects\: :ref:`bool<class_bool>` = false\ ) |
   +-----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PacketPeer_property_encode_buffer_max_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **encode_buffer_max_size** = ``8388608`` :ref:`🔗<class_PacketPeer_property_encode_buffer_max_size>`

.. rst-class:: classref-property-setget

- |void| **set_encode_buffer_max_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_encode_buffer_max_size**\ (\ )

Kích thước bộ đệm tối đa được phép khi mã hóa :ref:`Variant<class_Variant>`\ s. Tăng giá trị này để hỗ trợ việc cấp phát bộ nhớ lớn hơn.

Phương thức :ref:`put_var()<class_PacketPeer_method_put_var>` cấp phát bộ nhớ trên stack, và bộ đệm được sử dụng sẽ tự động tăng đến lũy thừa của hai gần nhất phù hợp với kích thước của :ref:`Variant<class_Variant>`. Nếu :ref:`Variant<class_Variant>` lớn hơn :ref:`encode_buffer_max_size<class_PacketPeer_property_encode_buffer_max_size>`, phương thức sẽ báo lỗi với :ref:`@GlobalScope.ERR_OUT_OF_MEMORY<class_@GlobalScope_constant_ERR_OUT_OF_MEMORY>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PacketPeer_method_get_available_packet_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_available_packet_count**\ (\ ) |const| :ref:`🔗<class_PacketPeer_method_get_available_packet_count>`

Trả về số lượng gói tin hiện đang có trong bộ đệm vòng.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeer_method_get_packet:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **get_packet**\ (\ ) :ref:`🔗<class_PacketPeer_method_get_packet>`

Lấy một gói tin thô.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeer_method_get_packet_error:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **get_packet_error**\ (\ ) |const| :ref:`🔗<class_PacketPeer_method_get_packet_error>`

Trả về trạng thái lỗi của gói tin cuối cùng được nhận (thông qua :ref:`get_packet()<class_PacketPeer_method_get_packet>` và :ref:`get_var()<class_PacketPeer_method_get_var>`).

.. rst-class:: classref-item-separator

----

.. _class_PacketPeer_method_get_var:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_var**\ (\ allow_objects\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PacketPeer_method_get_var>`

Lấy một Variant. Nếu ``allow_objects`` là ``true``, cho phép giải mã các object.

Về nội bộ, phương thức này sử dụng cùng cơ chế giải mã như phương thức :ref:`@GlobalScope.bytes_to_var()<class_@GlobalScope_method_bytes_to_var>`.

\ **Cảnh báo:** Các object được deserialized có thể chứa mã được thực thi. Không sử dụng tùy chọn này nếu object được serialized đến từ các nguồn không đáng tin cậy để tránh các mối đe dọa bảo mật tiềm ẩn như thực thi mã từ xa.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeer_method_put_packet:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **put_packet**\ (\ buffer\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_PacketPeer_method_put_packet>`

Gửi một gói tin thô.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeer_method_put_var:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **put_var**\ (\ var\: :ref:`Variant<class_Variant>`, full_objects\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_PacketPeer_method_put_var>`

Gửi một :ref:`Variant<class_Variant>` dưới dạng gói tin. Nếu ``full_objects`` là ``true``, cho phép mã hóa các object (và có khả năng bao gồm mã).

Về nội bộ, phương thức này sử dụng cùng cơ chế mã hóa như phương thức :ref:`@GlobalScope.var_to_bytes()<class_@GlobalScope_method_var_to_bytes>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
