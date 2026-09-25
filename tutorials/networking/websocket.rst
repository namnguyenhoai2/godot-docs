.. _doc_websocket:

Sử dụng WebSockets
==================

HTML5 và WebSocket
------------------

Giao thức WebSocket được chuẩn hóa vào năm 2011 với mục tiêu ban đầu là cho phép các trình duyệt tạo kết nối ổn định và hai chiều với máy chủ. Trước đó, trình duyệt chỉ hỗ trợ các yêu cầu HTTP, vốn không phù hợp để giao tiếp hai chiều.

Giao thức này dựa trên thông điệp và là một công cụ rất mạnh để gửi thông báo push đến trình duyệt. Nó đã được dùng để triển khai chat, trò chơi theo lượt và nhiều ứng dụng khác. Giao thức này vẫn sử dụng kết nối TCP, tốt về độ tin cậy nhưng không tốt về độ trễ, vì vậy không phù hợp cho các ứng dụng thời gian thực như VoIP và trò chơi có nhịp độ nhanh (xem :ref:`WebRTC <doc_webrtc>` cho các trường hợp sử dụng đó).

Nhờ sự đơn giản, khả năng tương thích rộng và dễ sử dụng hơn kết nối TCP thô, WebSocket bắt đầu lan rộng ra ngoài trình duyệt, vào các ứng dụng gốc như một phương tiện giao tiếp với máy chủ mạng.

Godot hỗ trợ WebSocket trong cả bản xuất native và web.

Sử dụng WebSocket trong Godot
-----------------------------

WebSocket được triển khai trong Godot thông qua :ref:`WebSocketPeer <class_WebSocketPeer>`. Việc triển khai WebSocket tương thích với High-Level Multiplayer. Xem phần về :ref:`high-level multiplayer <doc_high_level_multiplayer>` để biết thêm chi tiết.

.. warning::

    Khi xuất sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong Android export preset trước khi xuất project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi hình thức giao tiếp mạng.

Ví dụ client tối giản
~~~~~~~~~~~~~~~~~~~~~

Ví dụ này sẽ hướng dẫn bạn cách tạo kết nối WebSocket đến một máy chủ từ xa, cũng như cách gửi và nhận dữ liệu.

.. code-block::

    extends Node

    # URL mà chúng ta sẽ kết nối đến.
    # Sử dụng "ws://localhost:9080" nếu kiểm thử với ví dụ máy chủ tối giản bên dưới.
    # `wss://` được sử dụng cho các kết nối bảo mật,
    # còn `ws://` được sử dụng cho các kết nối văn bản thuần túy (không bảo mật).
    @export var websocket_url = "wss://echo.websocket.org"

    # Đối tượng WebSocketClient của chúng ta.
    var socket = WebSocketPeer.new()


    func _ready():
        # Bắt đầu kết nối đến URL đã cho.
        var err = socket.connect_to_url(websocket_url)
        if err == OK:
            print("Connecting to %s..." % websocket_url)
            # Chờ socket kết nối.
            await get_tree().create_timer(2).timeout

            # Gửi dữ liệu.
            print("> Sending test packet.")
            socket.send_text("Test packet")
        else:
            push_error("Unable to connect.")
            set_process(false)


    func _process(_delta):
        # Gọi hàm này trong `_process()` hoặc `_physics_process()`.
        # Việc truyền dữ liệu và cập nhật trạng thái chỉ diễn ra khi gọi hàm này.
        socket.poll()

        # get_ready_state() cho biết socket đang ở trạng thái nào.
        var state = socket.get_ready_state()

        # `WebSocketPeer.STATE_OPEN` nghĩa là socket đã kết nối và sẵn sàng
        # gửi và nhận dữ liệu.
        if state == WebSocketPeer.STATE_OPEN:
            while socket.get_available_packet_count():
                var packet = socket.get_packet()
                if socket.was_string_packet():
                    var packet_text = packet.get_string_from_utf8()
                    print("< Got text data from server: %s" % packet_text)
                else:
                    print("< Got binary data from server: %d bytes" % packet.size())

        # `WebSocketPeer.STATE_CLOSING` nghĩa là socket đang đóng.
        # Điều quan trọng là tiếp tục polling để đóng kết nối một cách hoàn chỉnh.
        elif state == WebSocketPeer.STATE_CLOSING:
            pass

        # `WebSocketPeer.STATE_CLOSED` nghĩa là kết nối đã đóng hoàn toàn.
        # Bây giờ có thể an toàn dừng polling.
        elif state == WebSocketPeer.STATE_CLOSED:
            # Mã sẽ là `-1` nếu việc ngắt kết nối không được peer từ xa thông báo đúng cách.
            var code = socket.get_close_code()
            print("WebSocket closed with code: %d. Clean: %s" % [code, code != -1])
            set_process(false) # Dừng xử lý.

Lệnh này sẽ in ra nội dung tương tự như sau:

.. code:: text

    Connecting to wss://echo.websocket.org...
    < Got text data from server: Request served by 7811941c69e658
    > Sending test packet.
    < Got text data from server: Test packet

Ví dụ máy chủ tối giản
~~~~~~~~~~~~~~~~~~~~~~

Ví dụ này sẽ hướng dẫn bạn cách tạo một máy chủ WebSocket lắng nghe các kết nối từ xa, cũng như cách gửi và nhận dữ liệu.

.. code-block::

    extends Node

    # Cổng mà chúng ta sẽ lắng nghe.
    const PORT = 9080

    # Đối tượng TCP Server của chúng ta.
    var _tcp_server = TCPServer.new()

    # Danh sách các peer đã kết nối.
    var _peers: Dictionary[int, WebSocketPeer] = {}

    var last_peer_id := 1


    func _ready():
        # Bắt đầu lắng nghe trên cổng đã cho.
        var err = _tcp_server.listen(PORT)
        if err == OK:
            print("Server started.")
        else:
            push_error("Unable to start server.")
            set_process(false)


    func _process(_delta):
        while _tcp_server.is_connection_available():
            last_peer_id += 1
            print("+ Peer %d connected." % last_peer_id)
            var ws = WebSocketPeer.new()
            ws.accept_stream(_tcp_server.take_connection())
            _peers[last_peer_id] = ws

        # Duyệt qua tất cả peer đã kết nối bằng "keys()" để có thể xóa trong vòng lặp
        for peer_id in _peers.keys():
            var peer = _peers[peer_id]

            peer.poll()

            var peer_state = peer.get_ready_state()
            if peer_state == WebSocketPeer.STATE_OPEN:
                while peer.get_available_packet_count():
                    var packet = peer.get_packet()
                    if peer.was_string_packet():
                        var packet_text = packet.get_string_from_utf8()
                        print("< Got text data from peer %d: %s ... echoing" % [peer_id, packet_text])
                        # Gửi lại packet.
                        peer.send_text(packet_text)
                    else:
                        print("< Got binary data from peer %d: %d ... echoing" % [peer_id, packet.size()])
                        # Gửi lại packet.
                        peer.send(packet)
            elif peer_state == WebSocketPeer.STATE_CLOSED:
                # Xóa peer đã ngắt kết nối.
                _peers.erase(peer_id)
                var code = peer.get_close_code()
                var reason = peer.get_close_reason()
                print("- Peer %s closed with code: %d, reason %s. Clean: %s" % [peer_id, code, reason, code != -1])


Khi một client kết nối, lệnh này sẽ in ra nội dung tương tự như sau:

.. code:: text

    Server started.
    + Peer 2 connected.
    < Got text data from peer 2: Test packet ... echoing

Bản demo chat nâng cao
~~~~~~~~~~~~~~~~~~~~~~

Một bản demo chat nâng cao, tùy chọn sử dụng abstraction multiplayer mid-level, cùng với một bản demo multiplayer high-level, có sẵn trong `godot demo projects <https://github.com/godotengine/godot-demo-projects>`_ tại ``networking/websocket_chat`` và ``networking/websocket_multiplayer``.

.. _`godot demo projects`: https://github.com/godotengine/godot-demo-projects
