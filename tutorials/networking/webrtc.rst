:article_outdated: Đúng

.. _doc_webrtc:

WebRTC
======

HTML5, WebSocket, WebRTC
------------------------

Một trong những tính năng tuyệt vời của Godot là khả năng xuất sang nền tảng HTML5/WebAssembly, cho phép trò chơi của bạn chạy trực tiếp trong trình duyệt khi người dùng truy cập trang web của bạn.

Đây là một cơ hội tuyệt vời cho cả bản demo lẫn trò chơi hoàn chỉnh, nhưng trước đây vẫn có một số hạn chế. Về networking, cho đến gần đây các trình duyệt chỉ hỗ trợ HTTPRequests, sau đó WebSocket và rồi WebRTC lần lượt được đề xuất làm các tiêu chuẩn.

WebSocket
~~~~~~~~~

Khi giao thức WebSocket được tiêu chuẩn hóa vào tháng 12 năm 2011, nó cho phép các trình duyệt tạo các kết nối ổn định và hai chiều đến một máy chủ WebSocket. Giao thức này là một công cụ rất mạnh để gửi thông báo push đến các trình duyệt, và đã được dùng để triển khai chat, trò chơi theo lượt, v.v.

Tuy nhiên, WebSocket vẫn sử dụng kết nối TCP, vốn tốt cho độ tin cậy nhưng không tốt về độ trễ, nên không phù hợp với các ứng dụng thời gian thực như VoIP và các trò chơi có nhịp độ nhanh.

WebRTC
~~~~~~

Vì lý do này, từ năm 2010, Google bắt đầu phát triển một công nghệ mới có tên WebRTC, sau đó vào năm 2017 trở thành một đề xuất tiêu chuẩn của W3C. WebRTC là một tập hợp các đặc tả phức tạp hơn nhiều, đồng thời dựa vào nhiều công nghệ khác ở phía sau (ICE, DTLS, SDP) để cung cấp khả năng giao tiếp nhanh, thời gian thực và an toàn giữa hai peer.

Ý tưởng là tìm tuyến đường nhanh nhất giữa hai peer và thiết lập kết nối trực tiếp khi có thể (tức là cố gắng tránh sử dụng máy chủ relay).

Tuy nhiên, điều này phải đánh đổi bằng việc một số thông tin media phải được trao đổi giữa hai peer trước khi giao tiếp có thể bắt đầu (dưới dạng các chuỗi Session Description Protocol - SDP). Việc này thường được thực hiện thông qua một WebRTC Signaling Server.

.. image:: img/webrtc_signaling.png

Các peer kết nối đến một signaling server (ví dụ: một WebSocket server) và gửi thông tin media của mình. Sau đó, server chuyển tiếp thông tin này đến các peer khác, cho phép chúng thiết lập kết nối trực tiếp mong muốn. Khi hoàn tất bước này, các peer có thể ngắt kết nối khỏi signaling server và duy trì kết nối Peer-to-Peer (P2P) trực tiếp.

Sử dụng WebRTC trong Godot
--------------------------

WebRTC được triển khai trong Godot thông qua hai class chính :ref:`WebRTCPeerConnection <class_WebRTCPeerConnection>` và :ref:`WebRTCDataChannel <class_WebRTCDataChannel>`, cùng với triển khai multiplayer API :ref:`WebRTCMultiplayerPeer <class_WebRTCMultiplayerPeer>`. Xem phần về :ref:`multiplayer cấp cao <doc_high_level_multiplayer>` để biết thêm chi tiết.

.. note:: Các class này tự động khả dụng trong HTML5, nhưng **cần một plugin GDExtension bên ngoài trên các nền tảng native (không phải HTML5)**. Hãy xem `kho lưu trữ plugin webrtc-native <https://github.com/godotengine/webrtc-native>`__ để biết hướng dẫn và tải `bản phát hành <https://github.com/godotengine/webrtc-native/releases>`__ mới nhất.

.. warning::

    Khi xuất sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong export preset của Android trước khi xuất project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi hình thức giao tiếp mạng.

Ví dụ kết nối tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~

Ví dụ này sẽ hướng dẫn bạn cách tạo kết nối WebRTC giữa hai peer trong cùng một ứng dụng. Điều này không mấy hữu ích trong thực tế, nhưng sẽ giúp bạn có cái nhìn tổng quan về cách thiết lập một kết nối WebRTC.

.. code-block::

    extends Node

    # Tạo hai peer
    var p1 = WebRTCPeerConnection.new()
    var p2 = WebRTCPeerConnection.new()
    # Và một kênh đã thương lượng cho mỗi peer
    var ch1 = p1.create_data_channel("chat", {"id": 1, "negotiated": true})
    var ch2 = p2.create_data_channel("chat", {"id": 1, "negotiated": true})

    func _ready():
        # Kết nối session P1 đã được tạo với chính nó để thiết lập local description.
        p1.session_description_created.connect(p1.set_local_description)
        # Kết nối session và ICE đã được tạo của P1 với P2 để thiết lập remote description và các candidate.
        p1.session_description_created.connect(p2.set_remote_description)
        p1.ice_candidate_created.connect(p2.add_ice_candidate)

        # Tương tự cho P2
        p2.session_description_created.connect(p2.set_local_description)
        p2.session_description_created.connect(p1.set_remote_description)
        p2.ice_candidate_created.connect(p1.add_ice_candidate)

        # Để P1 tạo offer
        p1.create_offer()

        # Chờ một giây rồi gửi message từ P1.
        await get_tree().create_timer(1).timeout
        ch1.put_packet("Hi from P1".to_utf8_buffer())

        # Chờ một giây rồi gửi message từ P2.
        await get_tree().create_timer(1).timeout
        ch2.put_packet("Hi from P2".to_utf8_buffer())

    func _process(_delta):
        # Poll các kết nối
        p1.poll()
        p2.poll()

        # Kiểm tra message
        if ch1.get_ready_state() == ch1.STATE_OPEN and ch1.get_available_packet_count() > 0:
            print("P1 received: ", ch1.get_packet().get_string_from_utf8())
        if ch2.get_ready_state() == ch2.STATE_OPEN and ch2.get_available_packet_count() > 0:
            print("P2 received: ", ch2.get_packet().get_string_from_utf8())

Kết quả in ra sẽ là:

::

    P1 received: Hi from P1
    P2 received: Hi from P2

Ví dụ signaling cục bộ
~~~~~~~~~~~~~~~~~~~~~~

Ví dụ này mở rộng ví dụ trước bằng cách tách các peer vào hai scene khác nhau và sử dụng một :ref:`singleton <doc_singletons_autoload>` làm signaling server.

.. code-block::

    extends Node
    # Một client chat p2p mẫu.

    var peer = WebRTCPeerConnection.new()

    # Tạo data channel đã thương lượng.
    var channel = peer.create_data_channel("chat", {"negotiated": true, "id": 1})

    func _ready():
        # Kết nối tất cả các function.
        peer.ice_candidate_created.connect(self._on_ice_candidate)
        peer.session_description_created.connect(self._on_session)

        # Đăng ký với signaling server cục bộ (xem phần bên dưới để biết cách triển khai).
        Signaling.register(String(get_path()))


    func _on_ice_candidate(mid, index, sdp):
        # Gửi ICE candidate đến peer kia thông qua signaling server.
        Signaling.send_candidate(String(get_path()), mid, index, sdp)


    func _on_session(type, sdp):
        # Gửi session đến peer kia thông qua signaling server.
        Signaling.send_session(String(get_path()), type, sdp)
        # Đặt description đã tạo làm local.
        peer.set_local_description(type, sdp)


    func _process(delta):
        # Luôn poll kết nối thường xuyên.
        peer.poll()
        if channel.get_ready_state() == WebRTCDataChannel.STATE_OPEN:
            while channel.get_available_packet_count() > 0:
                print(String(get_path()), " received: ", channel.get_packet().get_string_from_utf8())


    func send_message(message):
        channel.put_packet(message.to_utf8_buffer())

Và bây giờ là signaling server cục bộ:

.. note:: Signaling server cục bộ này được dùng như một :ref:`singleton <doc_singletons_autoload>` để kết nối hai peer trong cùng một scene.

.. code-block::

    # Một signaling server cục bộ. Thêm nó vào autoloads với tên "Signaling" (/root/Signaling)
    extends Node

    # Chúng ta sẽ lưu hai peer ở đây
    var peers = []

    func register(path):
        assert(peers.size() < 2)
        peers.append(path)
        if peers.size() == 2:
            get_node(peers[0]).peer.create_offer()


    func _find_other(path):
        # Tìm peer đã đăng ký còn lại.
        for p in peers:
            if p != path:
                return p
        return ""


    func send_session(path, type, sdp):
        var other = _find_other(path)
        assert(other != "")
        get_node(other).peer.set_remote_description(type, sdp)


    func send_candidate(path, mid, index, sdp):
        var other = _find_other(path)
        assert(other != "")
        get_node(other).peer.add_ice_candidate(mid, index, sdp)

Sau đó bạn có thể sử dụng nó như sau:

.. code-block::

    # Scene chính (main.gd)
    extends Node

    const Chat = preload("res://chat.gd")

    func _ready():
        var p1 = Chat.new()
        var p2 = Chat.new()
        add_child(p1)
        add_child(p2)

        # Chờ một giây rồi gửi message từ P1
        await get_tree().create_timer(1).timeout
        p1.send_message("Hi from %s" % String(p1.get_path()))

        # Chờ một giây rồi gửi tin nhắn từ P2
        await get_tree().create_timer(1).timeout
        p2.send_message("Hi from %s" % String(p2.get_path()))

Thao tác này sẽ in ra nội dung tương tự như sau:

::

    /root/main/@@3 received: Hi from /root/main/@@2
    /root/main/@@2 received: Hi from /root/main/@@3

Signaling từ xa với WebSocket
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một bản demo nâng cao hơn sử dụng WebSocket để signaling giữa các peer và :ref:`WebRTCMultiplayerPeer <class_WebRTCMultiplayerPeer>` hiện có trong `các dự án demo của godot <https://github.com/godotengine/godot-demo-projects>`_ tại ``networking/webrtc_signaling``.

.. _`godot demo projects`: https://github.com/godotengine/godot-demo-projects
