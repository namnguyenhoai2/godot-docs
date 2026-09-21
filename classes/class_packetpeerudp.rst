:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PacketPeerUDP.xml.

.. _class_PacketPeerUDP:

PacketPeerUDP
=============

**Kế thừa:** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Đối tượng ngang hàng gói UDP.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đối tượng ngang hàng gói UDP. Có thể được dùng để gửi và nhận các gói UDP thô, cũng như :ref:`Variant<class_Variant>`\ s.

\ **Ví dụ:** Gửi một gói:

::

    var peer = PacketPeerUDP.new()

    # Ngoài ra, bạn có thể chọn cổng cục bộ được dùng để gửi gói.
    peer.bind(4444)

    peer.set_dest_address("1.1.1.1", 4433)
    peer.put_packet("hello".to_utf8_buffer())

\ **Ví dụ:** Lắng nghe các gói:

::

    var peer

    func _ready():
        peer = PacketPeerUDP.new()
        peer.bind(4433)


    func _process(_delta):
        if peer.get_available_packet_count() > 0:
            var array_bytes = peer.get_packet()
            var packet_string = array_bytes.get_string_from_ascii()
            print("Received message: ", packet_string)

\ **Lưu ý:** Khi export sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong preset export Android trước khi export project hoặc sử dụng one-click deploy. Nếu không, mọi hình thức giao tiếp mạng sẽ bị Android chặn.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`bind<class_PacketPeerUDP_method_bind>`\ (\ port\: :ref:`int<class_int>`, bind_address\: :ref:`String<class_String>` = "*", recv_buf_size\: :ref:`int<class_int>` = 65536\ )   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`close<class_PacketPeerUDP_method_close>`\ (\ )                                                                                                                                |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`connect_to_host<class_PacketPeerUDP_method_connect_to_host>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ )                                          |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`get_local_port<class_PacketPeerUDP_method_get_local_port>`\ (\ ) |const|                                                                                                      |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`           | :ref:`get_packet_ip<class_PacketPeerUDP_method_get_packet_ip>`\ (\ ) |const|                                                                                                        |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`get_packet_port<class_PacketPeerUDP_method_get_packet_port>`\ (\ ) |const|                                                                                                    |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_bound<class_PacketPeerUDP_method_is_bound>`\ (\ ) |const|                                                                                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`is_socket_connected<class_PacketPeerUDP_method_is_socket_connected>`\ (\ ) |const|                                                                                            |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`join_multicast_group<class_PacketPeerUDP_method_join_multicast_group>`\ (\ multicast_address\: :ref:`String<class_String>`, interface_name\: :ref:`String<class_String>`\ )   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`leave_multicast_group<class_PacketPeerUDP_method_leave_multicast_group>`\ (\ multicast_address\: :ref:`String<class_String>`, interface_name\: :ref:`String<class_String>`\ ) |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_broadcast_enabled<class_PacketPeerUDP_method_set_broadcast_enabled>`\ (\ enabled\: :ref:`bool<class_bool>`\ )                                                             |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`set_dest_address<class_PacketPeerUDP_method_set_dest_address>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ )                                        |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`wait<class_PacketPeerUDP_method_wait>`\ (\ )                                                                                                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PacketPeerUDP_method_bind:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **bind**\ (\ port\: :ref:`int<class_int>`, bind_address\: :ref:`String<class_String>` = "*", recv_buf_size\: :ref:`int<class_int>` = 65536\ ) :ref:`🔗<class_PacketPeerUDP_method_bind>`

Bind **PacketPeerUDP** này vào ``port`` và ``bind_address`` được chỉ định với kích thước bộ đệm ``recv_buf_size``, cho phép nó nhận các gói đến.

Nếu ``bind_address`` được đặt thành ``"*"`` (mặc định), đối tượng ngang hàng sẽ được bind trên tất cả các địa chỉ khả dụng (cả IPv4 và IPv6).

Nếu ``bind_address`` được đặt thành ``"0.0.0.0"`` (đối với IPv4) hoặc ``"::"`` (đối với IPv6), đối tượng ngang hàng sẽ được bind trên tất cả các địa chỉ khả dụng khớp với loại IP đó.

Nếu ``bind_address`` được đặt thành bất kỳ địa chỉ hợp lệ nào (ví dụ: ``"192.168.1.101"``, ``"::1"``, v.v.), đối tượng ngang hàng sẽ chỉ được bind vào interface có địa chỉ đó (hoặc thất bại nếu không tồn tại interface nào có địa chỉ đã cho).

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_close:

.. rst-class:: classref-method

|void| **close**\ (\ ) :ref:`🔗<class_PacketPeerUDP_method_close>`

Đóng socket UDP bên dưới của **PacketPeerUDP**.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_connect_to_host:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **connect_to_host**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PacketPeerUDP_method_connect_to_host>`

Calling this method connects this UDP peer to the given ``host``/``port`` pair. UDP is in reality connectionless, so this option only means that incoming packets from different addresses are automatically discarded, and that outgoing packets are always sent to the connected address (future calls to :ref:`set_dest_address()<class_PacketPeerUDP_method_set_dest_address>` are not allowed). This method does not send any data to the remote peer, to do that, use :ref:`PacketPeer.put_var()<class_PacketPeer_method_put_var>` or :ref:`PacketPeer.put_packet()<class_PacketPeer_method_put_packet>` as usual. See also :ref:`UDPServer<class_UDPServer>`.

\ **Lưu ý:** Việc kết nối với đối tượng ngang hàng từ xa không giúp bảo vệ khỏi các cuộc tấn công độc hại như giả mạo IP, v.v. Hãy cân nhắc sử dụng kỹ thuật mã hóa như TLS hoặc DTLS nếu ứng dụng của bạn truyền thông tin nhạy cảm.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_get_local_port:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_local_port**\ (\ ) |const| :ref:`🔗<class_PacketPeerUDP_method_get_local_port>`

Trả về cổng cục bộ mà đối tượng ngang hàng này được bind vào.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_get_packet_ip:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_packet_ip**\ (\ ) |const| :ref:`🔗<class_PacketPeerUDP_method_get_packet_ip>`

Trả về IP của đối tượng ngang hàng từ xa đã gửi gói cuối cùng (gói được nhận bằng :ref:`PacketPeer.get_packet()<class_PacketPeer_method_get_packet>` hoặc :ref:`PacketPeer.get_var()<class_PacketPeer_method_get_var>`).

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_get_packet_port:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_packet_port**\ (\ ) |const| :ref:`🔗<class_PacketPeerUDP_method_get_packet_port>`

Trả về cổng của đối tượng ngang hàng từ xa đã gửi gói cuối cùng (gói được nhận bằng :ref:`PacketPeer.get_packet()<class_PacketPeer_method_get_packet>` hoặc :ref:`PacketPeer.get_var()<class_PacketPeer_method_get_var>`).

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_is_bound:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_bound**\ (\ ) |const| :ref:`🔗<class_PacketPeerUDP_method_is_bound>`

Trả về liệu **PacketPeerUDP** này có được bind vào một địa chỉ và có thể nhận các gói hay không.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_is_socket_connected:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_socket_connected**\ (\ ) |const| :ref:`🔗<class_PacketPeerUDP_method_is_socket_connected>`

Trả về ``true`` nếu socket UDP đang mở và đã được kết nối với một địa chỉ từ xa. Xem :ref:`connect_to_host()<class_PacketPeerUDP_method_connect_to_host>`.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_join_multicast_group:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **join_multicast_group**\ (\ multicast_address\: :ref:`String<class_String>`, interface_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PacketPeerUDP_method_join_multicast_group>`

Tham gia nhóm multicast được chỉ định bởi ``multicast_address`` bằng interface được nhận diện bởi ``interface_name``.

Bạn có thể tham gia cùng một nhóm multicast bằng nhiều interface. Dùng :ref:`IP.get_local_interfaces()<class_IP_method_get_local_interfaces>` để biết những interface nào khả dụng.

\ **Lưu ý:** Một số thiết bị Android có thể yêu cầu quyền ``CHANGE_WIFI_MULTICAST_STATE`` để multicast hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_leave_multicast_group:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **leave_multicast_group**\ (\ multicast_address\: :ref:`String<class_String>`, interface_name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_PacketPeerUDP_method_leave_multicast_group>`

Xóa interface được nhận diện bởi ``interface_name`` khỏi nhóm multicast được chỉ định bởi ``multicast_address``.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_set_broadcast_enabled:

.. rst-class:: classref-method

|void| **set_broadcast_enabled**\ (\ enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_PacketPeerUDP_method_set_broadcast_enabled>`

Bật hoặc tắt việc gửi các gói broadcast (ví dụ: ``set_dest_address("255.255.255.255", 4343)``). Tùy chọn này bị tắt theo mặc định.

\ **Lưu ý:** Một số thiết bị Android có thể yêu cầu quyền ``CHANGE_WIFI_MULTICAST_STATE`` và tùy chọn này phải được bật để cũng nhận được các gói broadcast.

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_set_dest_address:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **set_dest_address**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ ) :ref:`🔗<class_PacketPeerUDP_method_set_dest_address>`

Đặt địa chỉ đích và cổng để gửi các gói và biến. Nếu cần, hostname sẽ được phân giải bằng DNS.

\ **Lưu ý:** Phải bật :ref:`set_broadcast_enabled()<class_PacketPeerUDP_method_set_broadcast_enabled>` trước khi gửi các gói đến địa chỉ broadcast (ví dụ: ``255.255.255.255``).

.. rst-class:: classref-item-separator

----

.. _class_PacketPeerUDP_method_wait:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **wait**\ (\ ) :ref:`🔗<class_PacketPeerUDP_method_wait>`

Chờ một gói đến địa chỉ đã bind. Xem :ref:`bind()<class_PacketPeerUDP_method_bind>`.

\ **Lưu ý:** Không thể ngắt :ref:`wait()<class_PacketPeerUDP_method_wait>` sau khi đã gọi. Có thể khắc phục điều này bằng cách cho phép bên còn lại gửi một gói "death pill" cụ thể như sau:


.. tabs::

 .. code-tab:: gdscript

    socket = PacketPeerUDP.new()
    # Máy chủ
    socket.set_dest_address("127.0.0.1", 789)
    socket.put_packet("Time to stop".to_ascii_buffer())

    # Máy khách
    while socket.wait() == OK:
        var data = socket.get_packet().get_string_from_ascii()
        if data == "Time to stop":
            return

 .. code-tab:: csharp

    var socket = new PacketPeerUdp();
    // Máy chủ
    socket.SetDestAddress("127.0.0.1", 789);
    socket.PutPacket("Time to stop".ToAsciiBuffer());

    // Máy khách
    while (socket.Wait() == OK)
    {
        string data = socket.GetPacket().GetStringFromASCII();
        if (data == "Time to stop")
        {
            return;
        }
    }



.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
