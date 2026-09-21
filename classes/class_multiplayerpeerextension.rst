:github_url: hide

.. meta::
	:keywords: network

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MultiplayerPeerExtension.xml.

.. _class_MultiplayerPeerExtension:

MultiplayerPeerExtension
========================

**Kế thừa:** :ref:`MultiplayerPeer<class_MultiplayerPeer>` **<** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp có thể được kế thừa để triển khai các lớp networking API multiplayer tùy chỉnh thông qua GDExtension.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được thiết kế để được kế thừa từ một plugin GDExtension nhằm triển khai các lớp networking tùy chỉnh cho multiplayer API (chẳng hạn như WebRTC). Tất cả các phương thức bên dưới **phải** được triển khai để có một triển khai multiplayer tùy chỉnh hoạt động. Xem thêm :ref:`MultiplayerAPI<class_MultiplayerAPI>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_close<class_MultiplayerPeerExtension_private_method__close>`\ (\ ) |virtual| |required|                                                                                        |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_disconnect_peer<class_MultiplayerPeerExtension_private_method__disconnect_peer>`\ (\ peer\: :ref:`int<class_int>`, force\: :ref:`bool<class_bool>`\ ) |virtual| |required|     |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`_get_available_packet_count<class_MultiplayerPeerExtension_private_method__get_available_packet_count>`\ (\ ) |virtual| |required| |const|                                      |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` | :ref:`_get_connection_status<class_MultiplayerPeerExtension_private_method__get_connection_status>`\ (\ ) |virtual| |required| |const|                                                |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`_get_max_packet_size<class_MultiplayerPeerExtension_private_method__get_max_packet_size>`\ (\ ) |virtual| |required| |const|                                                    |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                          | :ref:`_get_packet<class_MultiplayerPeerExtension_private_method__get_packet>`\ (\ r_buffer\: ``const uint8_t **``, r_buffer_size\: ``int32_t*``\ ) |virtual|                          |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`_get_packet_channel<class_MultiplayerPeerExtension_private_method__get_packet_channel>`\ (\ ) |virtual| |required| |const|                                                      |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`         | :ref:`_get_packet_mode<class_MultiplayerPeerExtension_private_method__get_packet_mode>`\ (\ ) |virtual| |required| |const|                                                            |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`_get_packet_peer<class_MultiplayerPeerExtension_private_method__get_packet_peer>`\ (\ ) |virtual| |required| |const|                                                            |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`                  | :ref:`_get_packet_script<class_MultiplayerPeerExtension_private_method__get_packet_script>`\ (\ ) |virtual|                                                                           |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`_get_transfer_channel<class_MultiplayerPeerExtension_private_method__get_transfer_channel>`\ (\ ) |virtual| |required| |const|                                                  |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`         | :ref:`_get_transfer_mode<class_MultiplayerPeerExtension_private_method__get_transfer_mode>`\ (\ ) |virtual| |required| |const|                                                        |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                          | :ref:`_get_unique_id<class_MultiplayerPeerExtension_private_method__get_unique_id>`\ (\ ) |virtual| |required| |const|                                                                |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                        | :ref:`_is_refusing_new_connections<class_MultiplayerPeerExtension_private_method__is_refusing_new_connections>`\ (\ ) |virtual| |const|                                               |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                        | :ref:`_is_server<class_MultiplayerPeerExtension_private_method__is_server>`\ (\ ) |virtual| |required| |const|                                                                        |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                        | :ref:`_is_server_relay_supported<class_MultiplayerPeerExtension_private_method__is_server_relay_supported>`\ (\ ) |virtual| |const|                                                   |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_poll<class_MultiplayerPeerExtension_private_method__poll>`\ (\ ) |virtual| |required|                                                                                          |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                          | :ref:`_put_packet<class_MultiplayerPeerExtension_private_method__put_packet>`\ (\ buffer\: ``const uint8_t*``, buffer_size\: :ref:`int<class_int>`\ ) |virtual|                       |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                          | :ref:`_put_packet_script<class_MultiplayerPeerExtension_private_method__put_packet_script>`\ (\ buffer\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |virtual|                   |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_set_refuse_new_connections<class_MultiplayerPeerExtension_private_method__set_refuse_new_connections>`\ (\ enable\: :ref:`bool<class_bool>`\ ) |virtual|                       |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_set_target_peer<class_MultiplayerPeerExtension_private_method__set_target_peer>`\ (\ peer\: :ref:`int<class_int>`\ ) |virtual| |required|                                      |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_set_transfer_channel<class_MultiplayerPeerExtension_private_method__set_transfer_channel>`\ (\ channel\: :ref:`int<class_int>`\ ) |virtual| |required|                         |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                         | :ref:`_set_transfer_mode<class_MultiplayerPeerExtension_private_method__set_transfer_mode>`\ (\ mode\: :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`\ ) |virtual| |required| |
   +----------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiplayerPeerExtension_private_method__close:

.. rst-class:: classref-method

|void| **_close**\ (\ ) |virtual| |required| :ref:`🔗<class_MultiplayerPeerExtension_private_method__close>`

Được gọi khi multiplayer peer cần được đóng ngay lập tức (xem :ref:`MultiplayerPeer.close()<class_MultiplayerPeer_method_close>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__disconnect_peer:

.. rst-class:: classref-method

|void| **_disconnect_peer**\ (\ peer\: :ref:`int<class_int>`, force\: :ref:`bool<class_bool>`\ ) |virtual| |required| :ref:`🔗<class_MultiplayerPeerExtension_private_method__disconnect_peer>`

Được gọi khi ``peer`` đã kết nối cần bị ngắt kết nối bắt buộc (xem :ref:`MultiplayerPeer.disconnect_peer()<class_MultiplayerPeer_method_disconnect_peer>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_available_packet_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_available_packet_count**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_available_packet_count>`

Được gọi khi số lượng packet khả dụng được :ref:`MultiplayerAPI<class_MultiplayerAPI>` yêu cầu nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_connection_status:

.. rst-class:: classref-method

:ref:`ConnectionStatus<enum_MultiplayerPeer_ConnectionStatus>` **_get_connection_status**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_connection_status>`

Được gọi khi trạng thái kết nối được yêu cầu trên :ref:`MultiplayerPeer<class_MultiplayerPeer>` (xem :ref:`MultiplayerPeer.get_connection_status()<class_MultiplayerPeer_method_get_connection_status>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_max_packet_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_max_packet_size**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_max_packet_size>`

Được gọi khi kích thước packet tối đa được phép (tính bằng byte) được :ref:`MultiplayerAPI<class_MultiplayerAPI>` yêu cầu.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_packet:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_get_packet**\ (\ r_buffer\: ``const uint8_t **``, r_buffer_size\: ``int32_t*``\ ) |virtual| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_packet>`

Được gọi khi :ref:`MultiplayerAPI<class_MultiplayerAPI>` cần nhận một packet, trong đó ``r_buffer_size`` là kích thước tính bằng byte của ``r_buffer`` nhị phân.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_packet_channel:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_packet_channel**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_packet_channel>`

Được gọi để lấy channel mà packet khả dụng tiếp theo đã được nhận qua. Xem :ref:`MultiplayerPeer.get_packet_channel()<class_MultiplayerPeer_method_get_packet_channel>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_packet_mode:

.. rst-class:: classref-method

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **_get_packet_mode**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_packet_mode>`

Được gọi để lấy transfer mode mà remote peer đã sử dụng để gửi packet khả dụng tiếp theo. Xem :ref:`MultiplayerPeer.get_packet_mode()<class_MultiplayerPeer_method_get_packet_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_packet_peer:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_packet_peer**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_packet_peer>`

Được gọi khi ID của :ref:`MultiplayerPeer<class_MultiplayerPeer>` đã gửi packet gần đây nhất được yêu cầu (xem :ref:`MultiplayerPeer.get_packet_peer()<class_MultiplayerPeer_method_get_packet_peer>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_packet_script:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **_get_packet_script**\ (\ ) |virtual| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_packet_script>`

Được gọi khi :ref:`MultiplayerAPI<class_MultiplayerAPI>` cần nhận một packet nếu :ref:`_get_packet()<class_MultiplayerPeerExtension_private_method__get_packet>` chưa được triển khai. Sử dụng phương thức này khi mở rộng lớp thông qua GDScript.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_transfer_channel:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_transfer_channel**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_transfer_channel>`

Được gọi khi transfer channel cần sử dụng được đọc trên :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.transfer_channel<class_MultiplayerPeer_property_transfer_channel>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_transfer_mode:

.. rst-class:: classref-method

:ref:`TransferMode<enum_MultiplayerPeer_TransferMode>` **_get_transfer_mode**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_transfer_mode>`

Được gọi khi transfer mode cần sử dụng được đọc trên :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.transfer_mode<class_MultiplayerPeer_property_transfer_mode>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__get_unique_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_unique_id**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__get_unique_id>`

Được gọi khi unique ID của :ref:`MultiplayerPeer<class_MultiplayerPeer>` này được yêu cầu (xem :ref:`MultiplayerPeer.get_unique_id()<class_MultiplayerPeer_method_get_unique_id>`). Giá trị phải nằm giữa ``1`` và ``2147483647``.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__is_refusing_new_connections:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_refusing_new_connections**\ (\ ) |virtual| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__is_refusing_new_connections>`

Được gọi khi trạng thái "refuse new connections" được yêu cầu trên :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.refuse_new_connections<class_MultiplayerPeer_property_refuse_new_connections>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__is_server:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_server**\ (\ ) |virtual| |required| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__is_server>`

Được gọi khi trạng thái "is server" được yêu cầu trên :ref:`MultiplayerAPI<class_MultiplayerAPI>`. Xem :ref:`MultiplayerAPI.is_server()<class_MultiplayerAPI_method_is_server>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__is_server_relay_supported:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_is_server_relay_supported**\ (\ ) |virtual| |const| :ref:`🔗<class_MultiplayerPeerExtension_private_method__is_server_relay_supported>`

Được gọi để kiểm tra xem server có thể hoạt động như một relay trong cấu hình hiện tại hay không. Xem :ref:`MultiplayerPeer.is_server_relay_supported()<class_MultiplayerPeer_method_is_server_relay_supported>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__poll:

.. rst-class:: classref-method

|void| **_poll**\ (\ ) |virtual| |required| :ref:`🔗<class_MultiplayerPeerExtension_private_method__poll>`

Được gọi khi :ref:`MultiplayerAPI<class_MultiplayerAPI>` được poll. Xem :ref:`MultiplayerAPI.poll()<class_MultiplayerAPI_method_poll>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__put_packet:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_put_packet**\ (\ buffer\: ``const uint8_t*``, buffer_size\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_MultiplayerPeerExtension_private_method__put_packet>`

Được gọi khi :ref:`MultiplayerAPI<class_MultiplayerAPI>` cần gửi một packet, trong đó ``buffer_size`` là kích thước tính bằng byte của ``buffer`` nhị phân.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__put_packet_script:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_put_packet_script**\ (\ buffer\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |virtual| :ref:`🔗<class_MultiplayerPeerExtension_private_method__put_packet_script>`

Được gọi khi :ref:`MultiplayerAPI<class_MultiplayerAPI>` cần gửi một packet nếu :ref:`_put_packet()<class_MultiplayerPeerExtension_private_method__put_packet>` chưa được triển khai. Sử dụng phương thức này khi mở rộng lớp thông qua GDScript.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__set_refuse_new_connections:

.. rst-class:: classref-method

|void| **_set_refuse_new_connections**\ (\ enable\: :ref:`bool<class_bool>`\ ) |virtual| :ref:`🔗<class_MultiplayerPeerExtension_private_method__set_refuse_new_connections>`

Được gọi khi trạng thái "refuse new connections" được thiết lập trên :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.refuse_new_connections<class_MultiplayerPeer_property_refuse_new_connections>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__set_target_peer:

.. rst-class:: classref-method

|void| **_set_target_peer**\ (\ peer\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_MultiplayerPeerExtension_private_method__set_target_peer>`

Được gọi khi target peer cần sử dụng được thiết lập cho :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.set_target_peer()<class_MultiplayerPeer_method_set_target_peer>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__set_transfer_channel:

.. rst-class:: classref-method

|void| **_set_transfer_channel**\ (\ channel\: :ref:`int<class_int>`\ ) |virtual| |required| :ref:`🔗<class_MultiplayerPeerExtension_private_method__set_transfer_channel>`

Được gọi khi channel cần sử dụng được thiết lập (set) cho :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.transfer_channel<class_MultiplayerPeer_property_transfer_channel>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerPeerExtension_private_method__set_transfer_mode:

.. rst-class:: classref-method

|void| **_set_transfer_mode**\ (\ mode\: :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`\ ) |virtual| |required| :ref:`🔗<class_MultiplayerPeerExtension_private_method__set_transfer_mode>`

Được gọi khi transfer mode được thiết lập trên :ref:`MultiplayerPeer<class_MultiplayerPeer>` này (xem :ref:`MultiplayerPeer.transfer_mode<class_MultiplayerPeer_property_transfer_mode>`).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
