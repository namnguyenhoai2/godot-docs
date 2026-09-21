:github_url: hide

.. meta::
	:keywords: network

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MultiplayerPeer.xml.

.. _class_MultiplayerPeer:

MultiplayerPeer
===============

**Kế thừa:** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ENetMultiplayerPeer<class_ENetMultiplayerPeer>`, :ref:`MultiplayerPeerExtension<class_MultiplayerPeerExtension>`, :ref:`OfflineMultiplayerPeer<class_OfflineMultiplayerPeer>`, :ref:`WebRTCMultiplayerPeer<class_WebRTCMultiplayerPeer>`, :ref:`WebSocketMultiplayerPeer<class_WebSocketMultiplayerPeer>`

Lớp trừu tượng dành cho các :ref:`PacketPeer<class_PacketPeer>`\ chuyên biệt được :ref:`MultiplayerAPI<class_MultiplayerAPI>` sử dụng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Quản lý kết nối với một hoặc nhiều peer từ xa hoạt động với vai trò server hoặc client, đồng thời gán ID duy nhất cho từng peer. Xem thêm :ref:`MultiplayerAPI<class_MultiplayerAPI>`.

\ **Lưu ý:** Giao thức :ref:`MultiplayerAPI<class_MultiplayerAPI>` là một chi tiết triển khai và không предназначено để các server không phải Godot sử dụng. Giao thức này có thể thay đổi mà không cần thông báo.

\ **Lưu ý:** Khi export sang Android, hãy bật quyền ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi hình thức giao tiếp mạng.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Multiplayer cấp cao <../tutorials/networking/high_level_multiplayer>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                | :ref:`refuse_new_connections<class_MultiplayerPeer_property_refuse_new_connections>` | ``false`` |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                  | :ref:`transfer_channel<class_MultiplayerPeer_property_transfer_channel>`             | ``0``     |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` | :ref:`transfer_mode<class_MultiplayerPeer_property_transfer_mode>`                   | ``2``     |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`close<class_MultiplayerPeer_method_close>`\ (\ )                                                                                            |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`disconnect_peer<class_MultiplayerPeer_method_disconnect_peer>`\ (\ peer\: :ref:`int<class_int>`, force\: :ref:`bool<class_bool>` = false\ ) |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`generate_unique_id<class_MultiplayerPeer_method_generate_unique_id>`\ (\ ) |const|                                                          |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` | :ref:`get_connection_status<class_MultiplayerPeer_method_get_connection_status>`\ (\ ) |const|                                                    |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`get_packet_channel<class_MultiplayerPeer_method_get_packet_channel>`\ (\ ) |const|                                                          |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`         | :ref:`get_packet_mode<class_MultiplayerPeer_method_get_packet_mode>`\ (\ ) |const|                                                                |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`get_packet_peer<class_MultiplayerPeer_method_get_packet_peer>`\ (\ ) |const|                                                                |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`get_unique_id<class_MultiplayerPeer_method_get_unique_id>`\ (\ ) |const|                                                                    |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                        | :ref:`is_server_relay_supported<class_MultiplayerPeer_method_is_server_relay_supported>`\ (\ ) |const|                                            |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`poll<class_MultiplayerPeer_method_poll>`\ (\ )                                                                                              |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`set_target_peer<class_MultiplayerPeer_method_set_target_peer>`\ (\ id\: :ref:`int<class_int>`\ )                                            |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_MultiplayerPeer_signal_peer_connected:

.. rst-class:: classref-signal

**peer_connected**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiplayerPeer_signal_peer_connected>`

Được phát ra khi một peer từ xa kết nối.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_signal_peer_disconnected:

.. rst-class:: classref-signal

**peer_disconnected**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiplayerPeer_signal_peer_disconnected>`

Được phát ra khi một peer từ xa đã ngắt kết nối.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_MultiplayerPeer_ConnectionStatus:

.. rst-class:: classref-enumeration

enum **ConnectionStatus**: :ref:`🔗<enum_MultiplayerPeer_ConnectionStatus>`

.. _class_MultiplayerPeer_constant_CONNECTION_DISCONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` **CONNECTION_DISCONNECTED** = ``0``

MultiplayerPeer đã ngắt kết nối.

.. _class_MultiplayerPeer_constant_CONNECTION_CONNECTING:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` **CONNECTION_CONNECTING** = ``1``

MultiplayerPeer hiện đang kết nối với server.

.. _class_MultiplayerPeer_constant_CONNECTION_CONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` **CONNECTION_CONNECTED** = ``2``

MultiplayerPeer này đã kết nối.

.. rst-class:: classref-item-separator

----

.. _enum_MultiplayerPeer_TransferMode:

.. rst-class:: classref-enumeration

enum **TransferMode**: :ref:`🔗<enum_MultiplayerPeer_TransferMode>`

.. _class_MultiplayerPeer_constant_TRANSFER_MODE_UNRELIABLE:

.. rst-class:: classref-enumeration-constant

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **TRANSFER_MODE_UNRELIABLE** = ``0``

Các packet không được xác nhận và không có nỗ lực gửi lại nào được thực hiện đối với packet bị mất. Packet có thể đến theo bất kỳ thứ tự nào. Có khả năng nhanh hơn :ref:`TRANSFER_MODE_UNRELIABLE_ORDERED<class_MultiplayerPeer_constant_TRANSFER_MODE_UNRELIABLE_ORDERED>`. Sử dụng cho dữ liệu không quan trọng và luôn cân nhắc xem thứ tự có quan trọng hay không.

.. _class_MultiplayerPeer_constant_TRANSFER_MODE_UNRELIABLE_ORDERED:

.. rst-class:: classref-enumeration-constant

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **TRANSFER_MODE_UNRELIABLE_ORDERED** = ``1``

Các packet không được xác nhận và không có nỗ lực gửi lại nào được thực hiện đối với packet bị mất. Packet được nhận theo đúng thứ tự đã gửi. Có khả năng nhanh hơn :ref:`TRANSFER_MODE_RELIABLE<class_MultiplayerPeer_constant_TRANSFER_MODE_RELIABLE>`. Sử dụng cho dữ liệu không quan trọng hoặc dữ liệu sẽ lỗi thời nếu nhận muộn do phải gửi lại, chẳng hạn như dữ liệu chuyển động và vị trí.

.. _class_MultiplayerPeer_constant_TRANSFER_MODE_RELIABLE:

.. rst-class:: classref-enumeration-constant

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **TRANSFER_MODE_RELIABLE** = ``2``

Các packet phải được nhận và cần tiếp tục thực hiện nỗ lực gửi lại cho đến khi packet được xác nhận. Packet phải được nhận theo đúng thứ tự đã gửi. Đây là transfer mode đáng tin cậy nhất, nhưng có khả năng chậm nhất do overhead. Sử dụng cho dữ liệu quan trọng phải được truyền và đến nơi theo đúng thứ tự, chẳng hạn như khi kích hoạt một ability hoặc gửi tin nhắn chat. Hãy cân nhắc kỹ xem thông tin đó có thực sự quan trọng hay không và sử dụng một cách tiết chế.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_MultiplayerPeer_constant_TARGET_PEER_BROADCAST:

.. rst-class:: classref-constant

**TARGET_PEER_BROADCAST** = ``0`` :ref:`🔗<class_MultiplayerPeer_constant_TARGET_PEER_BROADCAST>`

Packet được gửi đến tất cả peer đã kết nối.

.. _class_MultiplayerPeer_constant_TARGET_PEER_SERVER:

.. rst-class:: classref-constant

**TARGET_PEER_SERVER** = ``1`` :ref:`🔗<class_MultiplayerPeer_constant_TARGET_PEER_SERVER>`

Packet được gửi đến peer từ xa đang hoạt động với vai trò server.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiplayerPeer_property_refuse_new_connections:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **refuse_new_connections** = ``false`` :ref:`🔗<class_MultiplayerPeer_property_refuse_new_connections>`

.. rst-class:: classref-property-setget

- |void| **set_refuse_new_connections**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_refusing_new_connections**\ (\ )

Nếu ``true``, **MultiplayerPeer** này sẽ từ chối các kết nối mới.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_property_transfer_channel:

.. rst-class:: classref-property

:ref:`int<class_int>` **transfer_channel** = ``0`` :ref:`🔗<class_MultiplayerPeer_property_transfer_channel>`

.. rst-class:: classref-property-setget

- |void| **set_transfer_channel**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_transfer_channel**\ (\ )

Kênh được sử dụng để gửi packet. Nhiều network API như ENet và WebRTC cho phép tạo nhiều kênh độc lập, hoạt động theo một cách nào đó giống như các kết nối riêng biệt. Điều này có nghĩa là dữ liệu reliable chỉ chặn việc phân phối các packet khác trên kênh đó, và thứ tự chỉ được xét trong phạm vi kênh mà packet được gửi. Sử dụng các kênh khác nhau để gửi các bản cập nhật trạng thái **khác nhau và độc lập** là một cách phổ biến để tối ưu hóa việc sử dụng mạng và giảm độ trễ trong các game có nhịp độ nhanh.

\ **Lưu ý:** Kênh mặc định (``0``) thực tế hoạt động như 3 kênh riêng biệt (mỗi kênh dành cho một :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`) để :ref:`TRANSFER_MODE_RELIABLE<class_MultiplayerPeer_constant_TRANSFER_MODE_RELIABLE>` và :ref:`TRANSFER_MODE_UNRELIABLE_ORDERED<class_MultiplayerPeer_constant_TRANSFER_MODE_UNRELIABLE_ORDERED>` mặc định không tương tác với nhau. Hãy tham khảo tài liệu của network API cụ thể (ví dụ: ENet hoặc WebRTC) để tìm hiểu cách thiết lập kênh đúng cách.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_property_transfer_mode:

.. rst-class:: classref-property

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **transfer_mode** = ``2`` :ref:`🔗<class_MultiplayerPeer_property_transfer_mode>`

.. rst-class:: classref-property-setget

- |void| **set_transfer_mode**\ (\ value\: :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`\ ) - :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **get_transfer_mode**\ (\ )

Cách gửi packet đến peer đích. Xem phương thức :ref:`set_target_peer()<class_MultiplayerPeer_method_set_target_peer>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiplayerPeer_method_close:

.. rst-class:: classref-method

|void| **close**\ (\ ) :ref:`🔗<class_MultiplayerPeer_method_close>`

Đóng ngay multiplayer peer và đưa nó về trạng thái :ref:`CONNECTION_DISCONNECTED<class_MultiplayerPeer_constant_CONNECTION_DISCONNECTED>`. Các peer đã kết nối sẽ bị ngắt mà không phát ra :ref:`peer_disconnected<class_MultiplayerPeer_signal_peer_disconnected>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_disconnect_peer:

.. rst-class:: classref-method

|void| **disconnect_peer**\ (\ peer\: :ref:`int<class_int>`, force\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_MultiplayerPeer_method_disconnect_peer>`

Ngắt kết nối ``peer`` đã cho khỏi host này. Nếu ``force`` là ``true`` thì signal :ref:`peer_disconnected<class_MultiplayerPeer_signal_peer_disconnected>` sẽ không được phát ra cho peer này.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_generate_unique_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **generate_unique_id**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_generate_unique_id>`

Trả về một số nguyên được tạo ngẫu nhiên có thể dùng làm network unique ID.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_get_connection_status:

.. rst-class:: classref-method

:ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` **get_connection_status**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_get_connection_status>`

Trả về trạng thái hiện tại của kết nối.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_get_packet_channel:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_packet_channel**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_get_packet_channel>`

Trả về kênh mà packet khả dụng tiếp theo được nhận qua. Xem :ref:`PacketPeer.get_available_packet_count()<class_PacketPeer_method_get_available_packet_count>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_get_packet_mode:

.. rst-class:: classref-method

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **get_packet_mode**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_get_packet_mode>`

Trả về transfer mode mà peer từ xa đã sử dụng để gửi packet khả dụng tiếp theo. Xem :ref:`PacketPeer.get_available_packet_count()<class_PacketPeer_method_get_available_packet_count>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_get_packet_peer:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_packet_peer**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_get_packet_peer>`

Trả về ID của **MultiplayerPeer** đã gửi packet khả dụng tiếp theo. Xem :ref:`PacketPeer.get_available_packet_count()<class_PacketPeer_method_get_available_packet_count>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_get_unique_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_unique_id**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_get_unique_id>`

Trả về ID của **MultiplayerPeer** này.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_is_server_relay_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_server_relay_supported**\ (\ ) |const| :ref:`🔗<class_MultiplayerPeer_method_is_server_relay_supported>`

Trả về ``true`` nếu server có thể hoạt động như một relay trong cấu hình hiện tại. Nghĩa là nếu :ref:`MultiplayerAPI<class_MultiplayerAPI>` ở cấp cao hơn cần thông báo cho các client đã kết nối về những peer khác và triển khai một giao thức relay để cho phép chúng giao tiếp với nhau.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_poll:

.. rst-class:: classref-method

|void| **poll**\ (\ ) :ref:`🔗<class_MultiplayerPeer_method_poll>`

Chờ tối đa 1 giây để nhận một network event mới.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeer_method_set_target_peer:

.. rst-class:: classref-method

|void| **set_target_peer**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiplayerPeer_method_set_target_peer>`

Đặt peer mà packet sẽ được gửi đến.

``id`` có thể là một trong các giá trị sau: :ref:`TARGET_PEER_BROADCAST<class_MultiplayerPeer_constant_TARGET_PEER_BROADCAST>` để gửi đến tất cả peer đã kết nối, :ref:`TARGET_PEER_SERVER<class_MultiplayerPeer_constant_TARGET_PEER_SERVER>` để gửi đến peer đang hoạt động với vai trò server, một peer ID hợp lệ để gửi đến peer cụ thể đó, hoặc một peer ID âm để gửi đến tất cả peer ngoại trừ peer đó. Theo mặc định, peer đích là :ref:`TARGET_PEER_BROADCAST<class_MultiplayerPeer_constant_TARGET_PEER_BROADCAST>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
