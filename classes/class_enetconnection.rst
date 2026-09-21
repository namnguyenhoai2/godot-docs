:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/enet/doc_classes/ENetConnection.xml.

.. _class_ENetConnection:

ENetConnection
==============

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một lớp wrapper cho một `ENetHost <http://enet.bespin.org/group__host.html>`__.

.. rst-class:: classref-introduction-group

Mô tả
-----

Mục đích của ENet là cung cấp một tầng giao tiếp mạng tương đối mỏng, đơn giản và mạnh mẽ trên UDP (User Datagram Protocol).

.. rst-class:: classref-introduction-group

Tutorial
--------

- `API documentation on the ENet website <http://enet.bespin.org/usergroup0.html>`__

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`bandwidth_limit<class_ENetConnection_method_bandwidth_limit>`\ (\ in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ )                                                                                                                                                                      |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`broadcast<class_ENetConnection_method_broadcast>`\ (\ channel\: :ref:`int<class_int>`, packet\: :ref:`PackedByteArray<class_PackedByteArray>`, flags\: :ref:`int<class_int>`\ )                                                                                                                                               |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`channel_limit<class_ENetConnection_method_channel_limit>`\ (\ limit\: :ref:`int<class_int>`\ )                                                                                                                                                                                                                                |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`compress<class_ENetConnection_method_compress>`\ (\ mode\: :ref:`CompressionMode<enum_ENetConnection_CompressionMode>`\ )                                                                                                                                                                                                     |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ENetPacketPeer<class_ENetPacketPeer>`                              | :ref:`connect_to_host<class_ENetConnection_method_connect_to_host>`\ (\ address\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`, channels\: :ref:`int<class_int>` = 0, data\: :ref:`int<class_int>` = 0\ )                                                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                                    | :ref:`create_host<class_ENetConnection_method_create_host>`\ (\ max_peers\: :ref:`int<class_int>` = 32, max_channels\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ )                                                                                            |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                                    | :ref:`create_host_bound<class_ENetConnection_method_create_host_bound>`\ (\ bind_address\: :ref:`String<class_String>`, bind_port\: :ref:`int<class_int>`, max_peers\: :ref:`int<class_int>` = 32, max_channels\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ ) |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`destroy<class_ENetConnection_method_destroy>`\ (\ )                                                                                                                                                                                                                                                                           |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                                    | :ref:`dtls_client_setup<class_ENetConnection_method_dtls_client_setup>`\ (\ hostname\: :ref:`String<class_String>`, client_options\: :ref:`TLSOptions<class_TLSOptions>` = null\ )                                                                                                                                                  |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                                    | :ref:`dtls_server_setup<class_ENetConnection_method_dtls_server_setup>`\ (\ server_options\: :ref:`TLSOptions<class_TLSOptions>`\ )                                                                                                                                                                                                 |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`flush<class_ENetConnection_method_flush>`\ (\ )                                                                                                                                                                                                                                                                               |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                    | :ref:`get_local_port<class_ENetConnection_method_get_local_port>`\ (\ ) |const|                                                                                                                                                                                                                                                     |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                    | :ref:`get_max_channels<class_ENetConnection_method_get_max_channels>`\ (\ ) |const|                                                                                                                                                                                                                                                 |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`ENetPacketPeer<class_ENetPacketPeer>`\] | :ref:`get_peers<class_ENetConnection_method_get_peers>`\ (\ )                                                                                                                                                                                                                                                                       |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                                | :ref:`pop_statistic<class_ENetConnection_method_pop_statistic>`\ (\ statistic\: :ref:`HostStatistic<enum_ENetConnection_HostStatistic>`\ )                                                                                                                                                                                          |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`refuse_new_connections<class_ENetConnection_method_refuse_new_connections>`\ (\ refuse\: :ref:`bool<class_bool>`\ )                                                                                                                                                                                                           |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                                | :ref:`service<class_ENetConnection_method_service>`\ (\ timeout\: :ref:`int<class_int>` = 0\ )                                                                                                                                                                                                                                      |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                   | :ref:`socket_send<class_ENetConnection_method_socket_send>`\ (\ destination_address\: :ref:`String<class_String>`, destination_port\: :ref:`int<class_int>`, packet\: :ref:`PackedByteArray<class_PackedByteArray>`\ )                                                                                                              |
   +--------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_ENetConnection_CompressionMode:

.. rst-class:: classref-enumeration

enum **CompressionMode**: :ref:`🔗<enum_ENetConnection_CompressionMode>`

.. _class_ENetConnection_constant_COMPRESS_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`CompressionMode<enum_ENetConnection_CompressionMode>` **COMPRESS_NONE** = ``0``

Không nén. Tùy chọn này sử dụng nhiều băng thông nhất, nhưng có ưu điểm là yêu cầu ít tài nguyên CPU nhất. Tùy chọn này cũng có thể được dùng để giúp việc debug mạng bằng các công cụ như Wireshark dễ dàng hơn.

.. _class_ENetConnection_constant_COMPRESS_RANGE_CODER:

.. rst-class:: classref-enumeration-constant

:ref:`CompressionMode<enum_ENetConnection_CompressionMode>` **COMPRESS_RANGE_CODER** = ``1``

Mã hóa range tích hợp của ENet. Hoạt động tốt trên các packet nhỏ, nhưng không phải là thuật toán hiệu quả nhất trên các packet lớn hơn 4 KB.

.. _class_ENetConnection_constant_COMPRESS_FASTLZ:

.. rst-class:: classref-enumeration-constant

:ref:`CompressionMode<enum_ENetConnection_CompressionMode>` **COMPRESS_FASTLZ** = ``2``

Nén bằng `FastLZ <https://fastlz.org/>`__. Tùy chọn này sử dụng ít tài nguyên CPU hơn so với :ref:`COMPRESS_ZLIB<class_ENetConnection_constant_COMPRESS_ZLIB>`, đổi lại sử dụng nhiều băng thông hơn.

.. _class_ENetConnection_constant_COMPRESS_ZLIB:

.. rst-class:: classref-enumeration-constant

:ref:`CompressionMode<enum_ENetConnection_CompressionMode>` **COMPRESS_ZLIB** = ``3``

Nén bằng `Zlib <https://www.zlib.net/>`__. Tùy chọn này sử dụng ít băng thông hơn so với :ref:`COMPRESS_FASTLZ<class_ENetConnection_constant_COMPRESS_FASTLZ>`, đổi lại sử dụng nhiều tài nguyên CPU hơn.

.. _class_ENetConnection_constant_COMPRESS_ZSTD:

.. rst-class:: classref-enumeration-constant

:ref:`CompressionMode<enum_ENetConnection_CompressionMode>` **COMPRESS_ZSTD** = ``4``

Nén bằng `Zstandard <https://facebook.github.io/zstd/>`__. Lưu ý rằng thuật toán này không hiệu quả lắm trên các packet nhỏ hơn 4 KB. Do đó, trong hầu hết trường hợp, bạn nên sử dụng các thuật toán nén khác.

.. rst-class:: classref-item-separator

----

.. _enum_ENetConnection_EventType:

.. rst-class:: classref-enumeration

enum **EventType**: :ref:`🔗<enum_ENetConnection_EventType>`

.. _class_ENetConnection_constant_EVENT_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`EventType<enum_ENetConnection_EventType>` **EVENT_ERROR** = ``-1``

Đã xảy ra lỗi trong quá trình :ref:`service()<class_ENetConnection_method_service>`. Có thể bạn sẽ cần :ref:`destroy()<class_ENetConnection_method_destroy>` host rồi tạo lại nó.

.. _class_ENetConnection_constant_EVENT_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`EventType<enum_ENetConnection_EventType>` **EVENT_NONE** = ``0``

Không có sự kiện nào xảy ra trong khoảng thời gian được chỉ định.

.. _class_ENetConnection_constant_EVENT_CONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`EventType<enum_ENetConnection_EventType>` **EVENT_CONNECT** = ``1``

Một yêu cầu kết nối được khởi tạo bởi enet_host_connect đã hoàn tất. Mảng sẽ chứa peer đã kết nối thành công.

.. _class_ENetConnection_constant_EVENT_DISCONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`EventType<enum_ENetConnection_EventType>` **EVENT_DISCONNECT** = ``2``

Một peer đã ngắt kết nối. Sự kiện này được tạo khi hoàn tất thành công việc ngắt kết nối được khởi tạo bởi :ref:`ENetPacketPeer.peer_disconnect()<class_ENetPacketPeer_method_peer_disconnect>`, khi một peer hết thời gian chờ hoặc khi một yêu cầu kết nối được khởi tạo bởi :ref:`connect_to_host()<class_ENetConnection_method_connect_to_host>` hết thời gian chờ. Mảng sẽ chứa peer đã ngắt kết nối. Trường data chứa dữ liệu do người dùng cung cấp để mô tả việc ngắt kết nối hoặc bằng 0 nếu không có dữ liệu.

.. _class_ENetConnection_constant_EVENT_RECEIVE:

.. rst-class:: classref-enumeration-constant

:ref:`EventType<enum_ENetConnection_EventType>` **EVENT_RECEIVE** = ``3``

Một packet đã được nhận từ một peer. Mảng sẽ chứa peer đã gửi packet và số channel mà packet được nhận trên đó. Packet đã nhận sẽ được xếp hàng vào :ref:`ENetPacketPeer<class_ENetPacketPeer>` tương ứng.

.. rst-class:: classref-item-separator

----

.. _enum_ENetConnection_HostStatistic:

.. rst-class:: classref-enumeration

enum **HostStatistic**: :ref:`🔗<enum_ENetConnection_HostStatistic>`

.. _class_ENetConnection_constant_HOST_TOTAL_SENT_DATA:

.. rst-class:: classref-enumeration-constant

:ref:`HostStatistic<enum_ENetConnection_HostStatistic>` **HOST_TOTAL_SENT_DATA** = ``0``

Tổng dữ liệu đã gửi.

.. _class_ENetConnection_constant_HOST_TOTAL_SENT_PACKETS:

.. rst-class:: classref-enumeration-constant

:ref:`HostStatistic<enum_ENetConnection_HostStatistic>` **HOST_TOTAL_SENT_PACKETS** = ``1``

Tổng số packet UDP đã gửi.

.. _class_ENetConnection_constant_HOST_TOTAL_RECEIVED_DATA:

.. rst-class:: classref-enumeration-constant

:ref:`HostStatistic<enum_ENetConnection_HostStatistic>` **HOST_TOTAL_RECEIVED_DATA** = ``2``

Tổng dữ liệu đã nhận.

.. _class_ENetConnection_constant_HOST_TOTAL_RECEIVED_PACKETS:

.. rst-class:: classref-enumeration-constant

:ref:`HostStatistic<enum_ENetConnection_HostStatistic>` **HOST_TOTAL_RECEIVED_PACKETS** = ``3``

Tổng số packet UDP đã nhận.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ENetConnection_method_bandwidth_limit:

.. rst-class:: classref-method

|void| **bandwidth_limit**\ (\ in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetConnection_method_bandwidth_limit>`

Điều chỉnh giới hạn băng thông của một host.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_broadcast:

.. rst-class:: classref-method

|void| **broadcast**\ (\ channel\: :ref:`int<class_int>`, packet\: :ref:`PackedByteArray<class_PackedByteArray>`, flags\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetConnection_method_broadcast>`

Xếp một ``packet`` vào hàng đợi để gửi đến tất cả peer liên kết với host thông qua ``channel`` được chỉ định. Xem các hằng số :ref:`ENetPacketPeer<class_ENetPacketPeer>` ``FLAG_*`` để biết các cờ packet khả dụng.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_channel_limit:

.. rst-class:: classref-method

|void| **channel_limit**\ (\ limit\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetConnection_method_channel_limit>`

Giới hạn số channel tối đa được phép cho các kết nối đến trong tương lai.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_compress:

.. rst-class:: classref-method

|void| **compress**\ (\ mode\: :ref:`CompressionMode<enum_ENetConnection_CompressionMode>`\ ) :ref:`🔗<class_ENetConnection_method_compress>`

Thiết lập phương thức nén được sử dụng cho các packet mạng. Các phương thức này có sự đánh đổi khác nhau giữa tốc độ nén và băng thông; nếu sử dụng nén, bạn có thể cần kiểm thử để xác định phương thức nào phù hợp nhất với trường hợp sử dụng của mình.

\ **Lưu ý:** Thiết kế mạng của hầu hết game đều liên quan đến việc gửi thường xuyên nhiều packet nhỏ (mỗi packet nhỏ hơn 4 KB). Nếu không chắc chắn, bạn nên giữ thuật toán nén mặc định vì nó hoạt động tốt nhất trên các packet nhỏ này.

\ **Lưu ý:** Chế độ nén phải được đặt thành cùng một giá trị trên server và tất cả client của server đó. Client sẽ không thể kết nối nếu chế độ nén được đặt trên client khác với chế độ trên server.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_connect_to_host:

.. rst-class:: classref-method

:ref:`ENetPacketPeer<class_ENetPacketPeer>` **connect_to_host**\ (\ address\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`, channels\: :ref:`int<class_int>` = 0, data\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetConnection_method_connect_to_host>`

Khởi tạo kết nối đến một ``address`` bên ngoài bằng ``port`` được chỉ định và cấp phát số ``channels`` được yêu cầu. Có thể truyền ``data`` tùy chọn trong quá trình kết nối dưới dạng số nguyên 32 bit.

\ **Lưu ý:** Bạn phải gọi :ref:`create_host()<class_ENetConnection_method_create_host>` hoặc :ref:`create_host_bound()<class_ENetConnection_method_create_host_bound>` ở cả hai đầu trước khi gọi phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_create_host:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_host**\ (\ max_peers\: :ref:`int<class_int>` = 32, max_channels\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetConnection_method_create_host>`

Tạo một ENetHost cho phép tối đa ``max_peers`` peer được kết nối, mỗi peer cấp phát tối đa ``max_channels`` channel, đồng thời có thể giới hạn băng thông ở mức ``in_bandwidth`` và ``out_bandwidth`` (nếu lớn hơn 0).

Phương thức này bind một cổng UDP động khả dụng ngẫu nhiên trên máy host tại địa chỉ *chưa được chỉ định*. Sử dụng :ref:`create_host_bound()<class_ENetConnection_method_create_host_bound>` để chỉ định địa chỉ và cổng.

\ **Lưu ý:** Cần tạo host ở cả client và server để thiết lập kết nối.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_create_host_bound:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_host_bound**\ (\ bind_address\: :ref:`String<class_String>`, bind_port\: :ref:`int<class_int>`, max_peers\: :ref:`int<class_int>` = 32, max_channels\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetConnection_method_create_host_bound>`

Tạo một ENetHost được bind với ``bind_address`` và ``bind_port`` đã cho, cho phép tối đa ``max_peers`` peer được kết nối, mỗi peer cấp phát tối đa ``max_channels`` channel, đồng thời có thể giới hạn băng thông ở mức ``in_bandwidth`` và ``out_bandwidth`` (nếu lớn hơn 0).

\ **Lưu ý:** Cần tạo host ở cả client và server để thiết lập kết nối.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_destroy:

.. rst-class:: classref-method

|void| **destroy**\ (\ ) :ref:`🔗<class_ENetConnection_method_destroy>`

Hủy host và tất cả tài nguyên liên kết với nó.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_dtls_client_setup:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **dtls_client_setup**\ (\ hostname\: :ref:`String<class_String>`, client_options\: :ref:`TLSOptions<class_TLSOptions>` = null\ ) :ref:`🔗<class_ENetConnection_method_dtls_client_setup>`

Cấu hình ENetHost này để sử dụng extension Godot tùy chỉnh, cho phép mã hóa DTLS cho các client ENet. Gọi phương thức này trước :ref:`connect_to_host()<class_ENetConnection_method_connect_to_host>` để ENet kết nối bằng DTLS và xác thực chứng chỉ server dựa trên ``hostname``. Bạn có thể truyền tham số ``client_options`` tùy chọn để tùy chỉnh các cơ quan cấp chứng chỉ được tin cậy hoặc tắt việc xác minh common name. Xem :ref:`TLSOptions.client()<class_TLSOptions_method_client>` và :ref:`TLSOptions.client_unsafe()<class_TLSOptions_method_client_unsafe>`.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_dtls_server_setup:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **dtls_server_setup**\ (\ server_options\: :ref:`TLSOptions<class_TLSOptions>`\ ) :ref:`🔗<class_ENetConnection_method_dtls_server_setup>`

Cấu hình ENetHost này để sử dụng extension Godot tùy chỉnh, cho phép mã hóa DTLS cho các server ENet. Gọi phương thức này ngay sau :ref:`create_host_bound()<class_ENetConnection_method_create_host_bound>` để ENetHost chờ các peer kết nối bằng DTLS. Xem :ref:`TLSOptions.server()<class_TLSOptions_method_server>`.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_flush:

.. rst-class:: classref-method

|void| **flush**\ (\ ) :ref:`🔗<class_ENetConnection_method_flush>`

Gửi mọi packet đang chờ trong host đến các peer được chỉ định của host đó.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_get_local_port:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_local_port**\ (\ ) |const| :ref:`🔗<class_ENetConnection_method_get_local_port>`

Trả về cổng cục bộ mà peer này được bind vào.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_get_max_channels:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_max_channels**\ (\ ) |const| :ref:`🔗<class_ENetConnection_method_get_max_channels>`

Trả về số channel tối đa được phép cho các peer đã kết nối.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_get_peers:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`ENetPacketPeer<class_ENetPacketPeer>`\] **get_peers**\ (\ ) :ref:`🔗<class_ENetConnection_method_get_peers>`

Trả về danh sách các peer liên kết với host này.

\ **Lưu ý:** Danh sách này có thể bao gồm một số peer chưa kết nối hoàn toàn hoặc vẫn đang được ngắt kết nối.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_pop_statistic:

.. rst-class:: classref-method

:ref:`float<class_float>` **pop_statistic**\ (\ statistic\: :ref:`HostStatistic<enum_ENetConnection_HostStatistic>`\ ) :ref:`🔗<class_ENetConnection_method_pop_statistic>`

Trả về và đặt lại các thống kê của máy chủ.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_refuse_new_connections:

.. rst-class:: classref-method

|void| **refuse_new_connections**\ (\ refuse\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_ENetConnection_method_refuse_new_connections>`

Cấu hình máy chủ DTLS để tự động loại bỏ các kết nối mới.

\ **Note:** Phương thức này chỉ liên quan sau khi gọi :ref:`dtls_server_setup()<class_ENetConnection_method_dtls_server_setup>`.

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_service:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **service**\ (\ timeout\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetConnection_method_service>`

Chờ các sự kiện trên kết nối này và chuyển tiếp các packet giữa host và các peer của nó, với ``timeout`` đã cho (tính bằng mili giây). :ref:`Array<class_Array>` được trả về sẽ có 4 phần tử: một :ref:`EventType<enum_ENetConnection_EventType>`, :ref:`ENetPacketPeer<class_ENetPacketPeer>` đã tạo ra sự kiện, dữ liệu liên kết với sự kiện (nếu có), và channel liên kết với sự kiện (nếu có). Nếu sự kiện được tạo ra là :ref:`EVENT_RECEIVE<class_ENetConnection_constant_EVENT_RECEIVE>`, packet nhận được sẽ được đưa vào hàng đợi của :ref:`ENetPacketPeer<class_ENetPacketPeer>` liên kết.

Gọi hàm này thường xuyên để xử lý các kết nối, ngắt kết nối và nhận các packet mới.

\ **Note:** Phương thức này phải được gọi ở cả hai đầu tham gia vào sự kiện (host gửi và host nhận).

.. rst-class:: classref-item-separator

----

.. _class_ENetConnection_method_socket_send:

.. rst-class:: classref-method

|void| **socket_send**\ (\ destination_address\: :ref:`String<class_String>`, destination_port\: :ref:`int<class_int>`, packet\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_ENetConnection_method_socket_send>`

Gửi một ``packet`` đến đích từ địa chỉ và port mà instance ENetConnection này hiện đang bind.

Điều này hữu ích vì nó giúp thiết lập các mục trong bảng định tuyến NAT trên tất cả thiết bị nằm giữa instance đã bind này và internet hướng ra công cộng, cho phép các packet kết nối của client tiềm năng được định tuyến ngược qua (các) thiết bị NAT nằm giữa internet công cộng và host này.

Điều này yêu cầu biết trước địa chỉ và port giao tiếp của client tiềm năng như được nhìn thấy từ internet công cộng — sau khi mọi thiết bị NAT đã xử lý yêu cầu kết nối của chúng. Thông tin này có thể lấy được từ một `STUN <https://en.wikipedia.org/wiki/STUN>`__ service và phải được chuyển cho host của bạn bởi một thực thể không phải là client tiềm năng. Điều này sẽ không bao giờ hoạt động với client phía sau Symmetric NAT do bản chất của thuật toán định tuyến Symmetric NAT, vì không thể biết trước IP và Port của chúng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
