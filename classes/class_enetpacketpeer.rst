:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/enet/doc_classes/ENetPacketPeer.xml.

.. _class_ENetPacketPeer:

ENetPacketPeer
==============

**Kế thừa:** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một lớp wrapper cho `ENetPeer <http://enet.bespin.org/group__peer.html>`__.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một triển khai PacketPeer đại diện cho một peer của :ref:`ENetConnection<class_ENetConnection>`.

Không thể khởi tạo trực tiếp lớp này, nhưng có thể lấy được trong :ref:`ENetConnection.service()<class_ENetConnection_method_service>` hoặc thông qua :ref:`ENetConnection.get_peers()<class_ENetConnection_method_get_peers>`.

\ **Lưu ý:** Khi export sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi hình thức giao tiếp mạng.

.. rst-class:: classref-introduction-group

Tutorials
---------

- `API documentation on the ENet website <http://enet.bespin.org/usergroup0.html>`__

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_channels<class_ENetPacketPeer_method_get_channels>`\ (\ ) |const|                                                                                                                   |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_packet_flags<class_ENetPacketPeer_method_get_packet_flags>`\ (\ ) |const|                                                                                                           |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                     | :ref:`get_remote_address<class_ENetPacketPeer_method_get_remote_address>`\ (\ ) |const|                                                                                                       |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_remote_port<class_ENetPacketPeer_method_get_remote_port>`\ (\ ) |const|                                                                                                             |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PeerState<enum_ENetPacketPeer_PeerState>` | :ref:`get_state<class_ENetPacketPeer_method_get_state>`\ (\ ) |const|                                                                                                                         |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`get_statistic<class_ENetPacketPeer_method_get_statistic>`\ (\ statistic\: :ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>`\ )                                                    |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_active<class_ENetPacketPeer_method_is_active>`\ (\ ) |const|                                                                                                                         |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`peer_disconnect<class_ENetPacketPeer_method_peer_disconnect>`\ (\ data\: :ref:`int<class_int>` = 0\ )                                                                                   |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`peer_disconnect_later<class_ENetPacketPeer_method_peer_disconnect_later>`\ (\ data\: :ref:`int<class_int>` = 0\ )                                                                       |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`peer_disconnect_now<class_ENetPacketPeer_method_peer_disconnect_now>`\ (\ data\: :ref:`int<class_int>` = 0\ )                                                                           |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`ping<class_ENetPacketPeer_method_ping>`\ (\ )                                                                                                                                           |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`ping_interval<class_ENetPacketPeer_method_ping_interval>`\ (\ ping_interval\: :ref:`int<class_int>`\ )                                                                                  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`reset<class_ENetPacketPeer_method_reset>`\ (\ )                                                                                                                                         |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`send<class_ENetPacketPeer_method_send>`\ (\ channel\: :ref:`int<class_int>`, packet\: :ref:`PackedByteArray<class_PackedByteArray>`, flags\: :ref:`int<class_int>`\ )                   |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_timeout<class_ENetPacketPeer_method_set_timeout>`\ (\ timeout\: :ref:`int<class_int>`, timeout_min\: :ref:`int<class_int>`, timeout_max\: :ref:`int<class_int>`\ )                  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`throttle_configure<class_ENetPacketPeer_method_throttle_configure>`\ (\ interval\: :ref:`int<class_int>`, acceleration\: :ref:`int<class_int>`, deceleration\: :ref:`int<class_int>`\ ) |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_ENetPacketPeer_PeerState:

.. rst-class:: classref-enumeration

enum **PeerState**: :ref:`🔗<enum_ENetPacketPeer_PeerState>`

.. _class_ENetPacketPeer_constant_STATE_DISCONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_DISCONNECTED** = ``0``

Peer đã ngắt kết nối.

.. _class_ENetPacketPeer_constant_STATE_CONNECTING:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_CONNECTING** = ``1``

Peer hiện đang cố gắng kết nối.

.. _class_ENetPacketPeer_constant_STATE_ACKNOWLEDGING_CONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_ACKNOWLEDGING_CONNECT** = ``2``

Peer đã xác nhận yêu cầu kết nối.

.. _class_ENetPacketPeer_constant_STATE_CONNECTION_PENDING:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_CONNECTION_PENDING** = ``3``

Peer hiện đang kết nối.

.. _class_ENetPacketPeer_constant_STATE_CONNECTION_SUCCEEDED:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_CONNECTION_SUCCEEDED** = ``4``

Peer đã kết nối thành công nhưng chưa sẵn sàng giao tiếp (:ref:`STATE_CONNECTED<class_ENetPacketPeer_constant_STATE_CONNECTED>`).

.. _class_ENetPacketPeer_constant_STATE_CONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_CONNECTED** = ``5``

Peer hiện đã kết nối và sẵn sàng giao tiếp.

.. _class_ENetPacketPeer_constant_STATE_DISCONNECT_LATER:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_DISCONNECT_LATER** = ``6``

Peer dự kiến sẽ ngắt kết nối sau khi không còn packet gửi đi nào.

.. _class_ENetPacketPeer_constant_STATE_DISCONNECTING:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_DISCONNECTING** = ``7``

Peer hiện đang ngắt kết nối.

.. _class_ENetPacketPeer_constant_STATE_ACKNOWLEDGING_DISCONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_ACKNOWLEDGING_DISCONNECT** = ``8``

Peer đã xác nhận yêu cầu ngắt kết nối.

.. _class_ENetPacketPeer_constant_STATE_ZOMBIE:

.. rst-class:: classref-enumeration-constant

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **STATE_ZOMBIE** = ``9``

Peer đã mất kết nối nhưng chưa được xem là thực sự ngắt kết nối (vì peer không xác nhận yêu cầu ngắt kết nối).

.. rst-class:: classref-item-separator

----

.. _enum_ENetPacketPeer_PeerStatistic:

.. rst-class:: classref-enumeration

enum **PeerStatistic**: :ref:`🔗<enum_ENetPacketPeer_PeerStatistic>`

.. _class_ENetPacketPeer_constant_PEER_PACKET_LOSS:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_LOSS** = ``0``

Tỷ lệ mất packet trung bình của các packet reliable so với :ref:`PACKET_LOSS_SCALE<class_ENetPacketPeer_constant_PACKET_LOSS_SCALE>`.

.. _class_ENetPacketPeer_constant_PEER_PACKET_LOSS_VARIANCE:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_LOSS_VARIANCE** = ``1``

Độ phương sai của việc mất packet.

.. _class_ENetPacketPeer_constant_PEER_PACKET_LOSS_EPOCH:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_LOSS_EPOCH** = ``2``

Thời điểm các thống kê mất packet được cập nhật lần cuối (tính bằng mili giây kể từ khi kết nối bắt đầu). Khoảng thời gian cập nhật thống kê mất packet là 10 giây và kể từ lần cập nhật thống kê gần nhất phải có ít nhất một packet được gửi đi.

.. _class_ENetPacketPeer_constant_PEER_ROUND_TRIP_TIME:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_ROUND_TRIP_TIME** = ``3``

Thời gian round trip trung bình của các packet reliable.

.. _class_ENetPacketPeer_constant_PEER_ROUND_TRIP_TIME_VARIANCE:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_ROUND_TRIP_TIME_VARIANCE** = ``4``

Độ phương sai của thời gian round trip trung bình.

.. _class_ENetPacketPeer_constant_PEER_LAST_ROUND_TRIP_TIME:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_LAST_ROUND_TRIP_TIME** = ``5``

Thời gian round trip gần nhất được ghi nhận của một packet reliable.

.. _class_ENetPacketPeer_constant_PEER_LAST_ROUND_TRIP_TIME_VARIANCE:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_LAST_ROUND_TRIP_TIME_VARIANCE** = ``6``

Độ phương sai của thời gian round trip gần nhất được ghi nhận.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE** = ``7``

Trạng thái throttle hiện tại của peer.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_LIMIT:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE_LIMIT** = ``8``

Số lượng packet unreliable tối đa không nên bị loại bỏ. Giá trị này luôn lớn hơn hoặc bằng ``1``. Giá trị ban đầu bằng :ref:`PACKET_THROTTLE_SCALE<class_ENetPacketPeer_constant_PACKET_THROTTLE_SCALE>`.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_COUNTER:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE_COUNTER** = ``9``

Giá trị nội bộ được dùng để tăng bộ đếm packet throttle. Giá trị này được hardcode thành ``7`` và không thể thay đổi. Có lẽ bạn muốn xem :ref:`PEER_PACKET_THROTTLE_ACCELERATION<class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_ACCELERATION>` thay vào đó.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_EPOCH:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE_EPOCH** = ``10``

Thời điểm các thống kê throttle được cập nhật lần cuối (tính bằng mili giây kể từ khi kết nối bắt đầu). Khoảng thời gian cập nhật thống kê throttle là :ref:`PEER_PACKET_THROTTLE_INTERVAL<class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_INTERVAL>`.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_ACCELERATION:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE_ACCELERATION** = ``11``

Hệ số acceleration của throttle. Giá trị cao hơn sẽ khiến ENet thích ứng với các điều kiện mạng thay đổi nhanh hơn, khiến các packet unreliable được gửi *thường xuyên hơn*. Giá trị mặc định là ``2``.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_DECELERATION:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE_DECELERATION** = ``12``

Hệ số deceleration của throttle. Giá trị cao hơn sẽ khiến ENet thích ứng với các điều kiện mạng thay đổi nhanh hơn, khiến các packet unreliable được gửi *ít thường xuyên hơn*. Giá trị mặc định là ``2``.

.. _class_ENetPacketPeer_constant_PEER_PACKET_THROTTLE_INTERVAL:

.. rst-class:: classref-enumeration-constant

:ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>` **PEER_PACKET_THROTTLE_INTERVAL** = ``13``

Khoảng thời gian dùng để đo thời gian round trip trung bình thấp nhất nhằm phục vụ cơ chế throttle (tính bằng mili giây). Giá trị mặc định là ``5000``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_ENetPacketPeer_constant_PACKET_LOSS_SCALE:

.. rst-class:: classref-constant

**PACKET_LOSS_SCALE** = ``65536`` :ref:`🔗<class_ENetPacketPeer_constant_PACKET_LOSS_SCALE>`

Thang đo tham chiếu cho việc mất packet. Xem :ref:`get_statistic()<class_ENetPacketPeer_method_get_statistic>` và :ref:`PEER_PACKET_LOSS<class_ENetPacketPeer_constant_PEER_PACKET_LOSS>`.

.. _class_ENetPacketPeer_constant_PACKET_THROTTLE_SCALE:

.. rst-class:: classref-constant

**PACKET_THROTTLE_SCALE** = ``32`` :ref:`🔗<class_ENetPacketPeer_constant_PACKET_THROTTLE_SCALE>`

Giá trị tham chiếu cho cấu hình throttle. Giá trị mặc định là ``32``. Xem :ref:`throttle_configure()<class_ENetPacketPeer_method_throttle_configure>`.

.. _class_ENetPacketPeer_constant_FLAG_RELIABLE:

.. rst-class:: classref-constant

**FLAG_RELIABLE** = ``1`` :ref:`🔗<class_ENetPacketPeer_constant_FLAG_RELIABLE>`

Đánh dấu packet sẽ được gửi là reliable.

.. _class_ENetPacketPeer_constant_FLAG_UNSEQUENCED:

.. rst-class:: classref-constant

**FLAG_UNSEQUENCED** = ``2`` :ref:`🔗<class_ENetPacketPeer_constant_FLAG_UNSEQUENCED>`

Đánh dấu packet sẽ được gửi là unsequenced (unreliable).

.. _class_ENetPacketPeer_constant_FLAG_UNRELIABLE_FRAGMENT:

.. rst-class:: classref-constant

**FLAG_UNRELIABLE_FRAGMENT** = ``8`` :ref:`🔗<class_ENetPacketPeer_constant_FLAG_UNRELIABLE_FRAGMENT>`

Đánh dấu packet sẽ được gửi là unreliable ngay cả khi packet quá lớn và cần fragmentation (làm tăng khả năng packet bị loại bỏ).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ENetPacketPeer_method_get_channels:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_channels**\ (\ ) |const| :ref:`🔗<class_ENetPacketPeer_method_get_channels>`

Trả về số lượng channel được cấp phát để giao tiếp với peer.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_get_packet_flags:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_packet_flags**\ (\ ) |const| :ref:`🔗<class_ENetPacketPeer_method_get_packet_flags>`

Trả về các flag ENet của packet tiếp theo trong hàng đợi nhận. Xem các hằng số ``FLAG_*`` để biết các flag packet khả dụng. Lưu ý rằng không phải tất cả flag đều được sao chép từ peer gửi sang peer nhận.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_get_remote_address:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_remote_address**\ (\ ) |const| :ref:`🔗<class_ENetPacketPeer_method_get_remote_address>`

Trả về địa chỉ IP của peer này.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_get_remote_port:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_remote_port**\ (\ ) |const| :ref:`🔗<class_ENetPacketPeer_method_get_remote_port>`

Trả về port từ xa của peer này.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_get_state:

.. rst-class:: classref-method

:ref:`PeerState<enum_ENetPacketPeer_PeerState>` **get_state**\ (\ ) |const| :ref:`🔗<class_ENetPacketPeer_method_get_state>`

Trả về trạng thái hiện tại của peer.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_get_statistic:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_statistic**\ (\ statistic\: :ref:`PeerStatistic<enum_ENetPacketPeer_PeerStatistic>`\ ) :ref:`🔗<class_ENetPacketPeer_method_get_statistic>`

Trả về ``statistic`` được yêu cầu cho peer này.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_is_active:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_active**\ (\ ) |const| :ref:`🔗<class_ENetPacketPeer_method_is_active>`

Trả về ``true`` nếu peer hiện đang active (tức là :ref:`ENetConnection<class_ENetConnection>` liên kết vẫn còn hợp lệ).

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_peer_disconnect:

.. rst-class:: classref-method

|void| **peer_disconnect**\ (\ data\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetPacketPeer_method_peer_disconnect>`

Yêu cầu ngắt kết nối khỏi một peer. Một :ref:`ENetConnection.EVENT_DISCONNECT<class_ENetConnection_constant_EVENT_DISCONNECT>` sẽ được tạo trong :ref:`ENetConnection.service()<class_ENetConnection_method_service>` sau khi hoàn tất ngắt kết nối.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_peer_disconnect_later:

.. rst-class:: classref-method

|void| **peer_disconnect_later**\ (\ data\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetPacketPeer_method_peer_disconnect_later>`

Yêu cầu ngắt kết nối khỏi một peer nhưng chỉ sau khi tất cả packet gửi đi đang xếp hàng đã được gửi. Một :ref:`ENetConnection.EVENT_DISCONNECT<class_ENetConnection_constant_EVENT_DISCONNECT>` sẽ được tạo trong :ref:`ENetConnection.service()<class_ENetConnection_method_service>` sau khi hoàn tất ngắt kết nối.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_peer_disconnect_now:

.. rst-class:: classref-method

|void| **peer_disconnect_now**\ (\ data\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetPacketPeer_method_peer_disconnect_now>`

Buộc ngắt kết nối ngay lập tức khỏi một peer. Sẽ không tạo :ref:`ENetConnection.EVENT_DISCONNECT<class_ENetConnection_constant_EVENT_DISCONNECT>`. Peer ở phía đối diện không được đảm bảo sẽ nhận thông báo ngắt kết nối và sẽ được reset ngay khi hàm này trả về.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_ping:

.. rst-class:: classref-method

|void| **ping**\ (\ ) :ref:`🔗<class_ENetPacketPeer_method_ping>`

Gửi yêu cầu ping đến một peer. ENet tự động ping tất cả peer đã kết nối theo các khoảng thời gian đều đặn; tuy nhiên, có thể gọi hàm này để đảm bảo các yêu cầu ping được gửi thường xuyên hơn.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_ping_interval:

.. rst-class:: classref-method

|void| **ping_interval**\ (\ ping_interval\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetPacketPeer_method_ping_interval>`

Thiết lập ``ping_interval`` tính bằng mili giây, là khoảng thời gian giữa các lần ping được gửi đến một peer. Ping được sử dụng vừa để giám sát trạng thái hoạt động của kết nối, vừa để tự động điều chỉnh throttle trong những giai đoạn lưu lượng thấp, ताकि throttle có khả năng phản hồi hợp lý khi lưu lượng tăng đột biến. Khoảng thời gian ping mặc định là ``500`` mili giây.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_reset:

.. rst-class:: classref-method

|void| **reset**\ (\ ) :ref:`🔗<class_ENetPacketPeer_method_reset>`

Buộc ngắt kết nối với một peer. Máy chủ từ xa được peer đại diện sẽ không được thông báo về việc ngắt kết nối và sẽ hết thời gian chờ đối với kết nối của nó đến máy chủ cục bộ.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_send:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **send**\ (\ channel\: :ref:`int<class_int>`, packet\: :ref:`PackedByteArray<class_PackedByteArray>`, flags\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetPacketPeer_method_send>`

Đưa một ``packet`` vào hàng đợi để gửi qua ``channel`` được chỉ định. Xem các hằng số ``FLAG_*`` để biết các cờ packet hiện có.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_set_timeout:

.. rst-class:: classref-method

|void| **set_timeout**\ (\ timeout\: :ref:`int<class_int>`, timeout_min\: :ref:`int<class_int>`, timeout_max\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetPacketPeer_method_set_timeout>`

Thiết lập các tham số timeout cho một peer. Các tham số timeout kiểm soát cách thức và thời điểm một peer timeout do không xác nhận được lưu lượng tin cậy. Các giá trị timeout được biểu thị bằng mili giây.

``timeout`` là một hệ số mà khi nhân với một giá trị dựa trên thời gian khứ hồi trung bình sẽ xác định giới hạn timeout cho một packet tin cậy. Khi đạt đến giới hạn đó, timeout sẽ được nhân đôi và peer sẽ bị ngắt kết nối nếu giới hạn đó đã đạt đến ``timeout_min``. Mặt khác, tham số ``timeout_max`` xác định một timeout cố định, trong khoảng thời gian đó mọi packet phải được xác nhận; nếu không, peer sẽ bị loại bỏ.

.. rst-class:: classref-item-separator

----

.. _class_ENetPacketPeer_method_throttle_configure:

.. rst-class:: classref-method

|void| **throttle_configure**\ (\ interval\: :ref:`int<class_int>`, acceleration\: :ref:`int<class_int>`, deceleration\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetPacketPeer_method_throttle_configure>`

Cấu hình tham số throttle cho một peer.

ENet sẽ loại bỏ các packet không tin cậy để phản ứng với những điều kiện thay đổi của kết nối Internet đến peer. Throttle biểu thị xác suất một packet không tin cậy không bị loại bỏ và do đó được ENet gửi đến peer. Bằng cách đo mức dao động trong thời gian khứ hồi của các packet tin cậy trong khoảng thời gian ``interval`` được chỉ định, ENet sẽ tăng xác suất theo lượng được chỉ định trong tham số ``acceleration``, hoặc giảm xác suất theo lượng được chỉ định trong tham số ``deceleration`` (cả hai đều là các tỷ lệ so với :ref:`PACKET_THROTTLE_SCALE<class_ENetPacketPeer_constant_PACKET_THROTTLE_SCALE>`).

Khi throttle có giá trị :ref:`PACKET_THROTTLE_SCALE<class_ENetPacketPeer_constant_PACKET_THROTTLE_SCALE>`, ENet không loại bỏ packet không tin cậy nào, vì vậy 100% packet không tin cậy sẽ được gửi.

Khi throttle có giá trị ``0``, ENet loại bỏ tất cả packet không tin cậy, vì vậy 0% packet không tin cậy sẽ được gửi.

Các giá trị trung gian của throttle biểu thị các xác suất trung gian từ 0% đến 100% packet không tin cậy được gửi. Giới hạn băng thông của máy chủ cục bộ và máy chủ từ xa được tính đến để xác định một giới hạn hợp lý cho xác suất throttle, trên giới hạn đó xác suất này không được tăng thêm ngay cả trong điều kiện tốt nhất.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
