:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PacketPeerDTLS.xml.

.. _class_PacketPeerDTLS:

PacketPeerDTLS
==============

**Kế thừa:** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Peer gói tin DTLS.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này đại diện cho một kết nối peer DTLS. Có thể dùng lớp này để kết nối đến máy chủ DTLS, và nó được trả về bởi :ref:`DTLSServer.take_connection()<class_DTLSServer_method_take_connection>`.

\ **Lưu ý:** Khi export sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong preset export Android trước khi export project hoặc sử dụng one-click deploy. Nếu không, mọi loại giao tiếp mạng sẽ bị Android chặn.

\ **Cảnh báo:** Hiện tại chưa hỗ trợ thu hồi chứng chỉ TLS và certificate pinning. Các chứng chỉ đã bị thu hồi vẫn được chấp nhận miễn là chúng vẫn hợp lệ theo các tiêu chí khác. Nếu đây là vấn đề đáng lo ngại, bạn có thể muốn sử dụng các chứng chỉ được quản lý tự động với thời hạn hiệu lực ngắn.

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`     | :ref:`connect_to_peer<class_PacketPeerDTLS_method_connect_to_peer>`\ (\ packet_peer\: :ref:`PacketPeerUDP<class_PacketPeerUDP>`, hostname\: :ref:`String<class_String>`, client_options\: :ref:`TLSOptions<class_TLSOptions>` = null\ ) |
   +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`disconnect_from_peer<class_PacketPeerDTLS_method_disconnect_from_peer>`\ (\ )                                                                                                                                                     |
   +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Status<enum_PacketPeerDTLS_Status>` | :ref:`get_status<class_PacketPeerDTLS_method_get_status>`\ (\ ) |const|                                                                                                                                                                 |
   +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                    | :ref:`poll<class_PacketPeerDTLS_method_poll>`\ (\ )                                                                                                                                                                                     |
   +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_PacketPeerDTLS_Status:

.. rst-class:: classref-enumeration

enum **Status**: :ref:`🔗<enum_PacketPeerDTLS_Status>`

.. _class_PacketPeerDTLS_constant_STATUS_DISCONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_PacketPeerDTLS_Status>` **STATUS_DISCONNECTED** = ``0``

Trạng thái biểu thị một **PacketPeerDTLS** đã ngắt kết nối.

.. _class_PacketPeerDTLS_constant_STATUS_HANDSHAKING:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_PacketPeerDTLS_Status>` **STATUS_HANDSHAKING** = ``1``

Trạng thái biểu thị một **PacketPeerDTLS** hiện đang thực hiện handshake với peer từ xa.

.. _class_PacketPeerDTLS_constant_STATUS_CONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_PacketPeerDTLS_Status>` **STATUS_CONNECTED** = ``2``

Trạng thái biểu thị một **PacketPeerDTLS** đã kết nối với peer từ xa.

.. _class_PacketPeerDTLS_constant_STATUS_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_PacketPeerDTLS_Status>` **STATUS_ERROR** = ``3``

Trạng thái biểu thị một **PacketPeerDTLS** đang ở trạng thái lỗi chung.

.. _class_PacketPeerDTLS_constant_STATUS_ERROR_HOSTNAME_MISMATCH:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_PacketPeerDTLS_Status>` **STATUS_ERROR_HOSTNAME_MISMATCH** = ``4``

Trạng thái lỗi cho biết domain trong chứng chỉ DTLS do host cung cấp không khớp với domain được yêu cầu để xác thực.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PacketPeerDTLS_method_connect_to_peer:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **connect_to_peer**\ (\ packet_peer\: :ref:`PacketPeerUDP<class_PacketPeerUDP>`, hostname\: :ref:`String<class_String>`, client_options\: :ref:`TLSOptions<class_TLSOptions>` = null\ ) :ref:`🔗<class_PacketPeerDTLS_method_connect_to_peer>`

Kết nối một ``packet_peer`` và bắt đầu handshake DTLS bằng :ref:`PacketPeerUDP<class_PacketPeerUDP>` bên dưới, đối tượng này phải được kết nối (xem :ref:`PacketPeerUDP.connect_to_host()<class_PacketPeerUDP_method_connect_to_host>`). Bạn có thể tùy chọn chỉ định ``client_options`` sẽ được sử dụng khi xác minh các kết nối TLS. Xem :ref:`TLSOptions.client()<class_TLSOptions_method_client>` và :ref:`TLSOptions.client_unsafe()<class_TLSOptions_method_client_unsafe>`.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerDTLS_method_disconnect_from_peer:

.. rst-class:: classref-method

|void| **disconnect_from_peer**\ (\ ) :ref:`🔗<class_PacketPeerDTLS_method_disconnect_from_peer>`

Ngắt kết nối peer này, kết thúc phiên DTLS.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerDTLS_method_get_status:

.. rst-class:: classref-method

:ref:`Status<enum_PacketPeerDTLS_Status>` **get_status**\ (\ ) |const| :ref:`🔗<class_PacketPeerDTLS_method_get_status>`

Trả về trạng thái của kết nối.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerDTLS_method_poll:

.. rst-class:: classref-method

|void| **poll**\ (\ ) :ref:`🔗<class_PacketPeerDTLS_method_poll>`

Thăm dò kết nối để kiểm tra các gói tin đến. Hãy gọi phương thức này thường xuyên để cập nhật trạng thái và duy trì hoạt động của kết nối.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
