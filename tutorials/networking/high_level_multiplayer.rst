.. _doc_high_level_multiplayer:

Multiplayer cấp cao
===================

API cấp cao so với API cấp thấp
-------------------------------

Phần sau giải thích sự khác biệt giữa networking cấp cao và cấp thấp trong Godot, cũng như một số kiến thức nền tảng. Nếu muốn bắt tay ngay vào việc thêm networking cho các node đầu tiên, hãy chuyển đến `Khởi tạo network`_ bên dưới. Nhưng hãy nhớ đọc phần còn lại sau đó!

Godot luôn hỗ trợ networking cấp thấp tiêu chuẩn thông qua :abbr:`UDP (User Datagram Protocol)`, :abbr:`TCP (Transmission Control Protocol)` và một số protocol cấp cao hơn như :abbr:`HTTP (Hypertext Transfer Protocol)` và :abbr:`SSL (Secure Sockets Layer)`. Các protocol này rất linh hoạt và có thể được dùng cho hầu hết mọi mục đích. Tuy nhiên, việc dùng chúng để đồng bộ state của game theo cách thủ công có thể đòi hỏi rất nhiều công sức. Đôi khi không thể tránh công việc đó hoặc việc này là đáng làm, chẳng hạn khi làm việc với một triển khai server tùy chỉnh ở backend. Nhưng trong hầu hết trường hợp, bạn nên cân nhắc API networking cấp cao của Godot, API này hy sinh một phần khả năng kiểm soát chi tiết của networking cấp thấp để đổi lấy sự dễ sử dụng cao hơn.

Điều này là do những hạn chế vốn có của các protocol cấp thấp:

- TCP đảm bảo các packet luôn đến nơi một cách đáng tin cậy và đúng thứ tự, nhưng độ trễ thường cao hơn do việc sửa lỗi. Đây cũng là một protocol khá phức tạp vì nó hiểu "connection" là gì và tối ưu cho những mục tiêu thường không phù hợp với các ứng dụng như game multiplayer. Các packet được đệm để gửi theo những batch lớn hơn, đánh đổi overhead trên mỗi packet thấp hơn để có độ trễ cao hơn. Điều này có thể hữu ích cho những thứ như HTTP, nhưng nhìn chung không phù hợp với game. Một phần trong số này có thể được cấu hình và tắt đi (ví dụ: tắt "Nagle's algorithm" cho TCP connection). - UDP là một protocol đơn giản hơn, chỉ gửi các packet (và không có khái niệm về một "connection"). Việc không sửa lỗi khiến nó khá nhanh (độ trễ thấp), nhưng packet có thể bị thất lạc trên đường truyền hoặc được nhận không đúng thứ tự. Ngoài ra, MTU (maximum packet size) của UDP thường thấp (chỉ vài trăm byte), vì vậy việc truyền các packet lớn hơn đồng nghĩa với việc phải chia nhỏ, sắp xếp lại và thử lại nếu một phần bị lỗi.

Nhìn chung, có thể xem TCP là đáng tin cậy, có thứ tự và chậm; còn UDP là không đáng tin cậy, không theo thứ tự và nhanh. Do sự khác biệt lớn về hiệu năng, việc xây dựng lại những phần của TCP cần thiết cho game (độ tin cậy và thứ tự packet tùy chọn), đồng thời tránh những phần không cần thiết (các tính năng kiểm soát tắc nghẽn/lưu lượng, Nagle's algorithm, v.v.) thường là hợp lý. Vì lý do này, hầu hết game engine đều đi kèm một triển khai như vậy, và Godot cũng không ngoại lệ.

Tóm lại, bạn có thể dùng API networking cấp thấp để kiểm soát tối đa và triển khai mọi thứ trên các network protocol thuần túy, hoặc dùng API cấp cao dựa trên :ref:`SceneTree <class_SceneTree>`, API này xử lý phần lớn công việc phức tạp ở phía sau theo một cách nhìn chung đã được tối ưu hóa.

.. note:: Most of Godot's supported platforms offer all or most of the mentioned high- and low-level networking
          các tính năng. Tuy nhiên, vì networking phần lớn luôn phụ thuộc vào phần cứng và hệ điều hành, một số tính năng có thể thay đổi hoặc không khả dụng trên một số platform đích. Đáng chú ý nhất, platform HTML5 hiện hỗ trợ WebSockets và WebRTC nhưng thiếu một số tính năng cấp cao, cũng như quyền truy cập thô vào các protocol cấp thấp như TCP và UDP.

.. note:: More about TCP/IP, UDP, and networking:
          https://gafferongames.com/post/udp_vs_tcp/

          Gaffer On Games có nhiều bài viết hữu ích về networking trong Games (`here <https://gafferongames.com/categories/game-networking/>`__), bao gồm `introduction to networking models in games <https://gafferongames.com/post/what_every_programmer_needs_to_know_about_game_networking/>`__ toàn diện.

.. warning:: Adding networking to your game comes with some responsibility.
             Nếu thực hiện không đúng, việc này có thể khiến ứng dụng của bạn dễ bị tấn công và có thể dẫn đến cheat hoặc exploit. Thậm chí, kẻ tấn công có thể xâm phạm các máy tính nơi ứng dụng của bạn đang chạy và sử dụng server của bạn để gửi spam, tấn công người khác hoặc đánh cắp dữ liệu của người dùng nếu họ chơi game của bạn.

             Điều này luôn đúng khi networking có liên quan và không liên quan gì đến Godot. Tất nhiên, bạn có thể thử nghiệm, nhưng khi phát hành một ứng dụng có networking, hãy luôn xử lý mọi vấn đề bảo mật có thể xảy ra.

Abstraction cấp trung
---------------------

Trước khi tìm hiểu cách chúng ta muốn đồng bộ một game qua network, việc hiểu cách API network cơ sở hoạt động cho mục đích đồng bộ có thể rất hữu ích.

Godot sử dụng một object cấp trung :ref:`MultiplayerPeer <class_MultiplayerPeer>`. Object này không được tạo trực tiếp, mà được thiết kế để một số triển khai C++ có thể cung cấp nó.

Object này kế thừa từ :ref:`PacketPeer <class_PacketPeer>`, vì vậy nó kế thừa tất cả các method hữu ích để serialize, gửi và nhận dữ liệu. Ngoài ra, nó bổ sung các method để thiết lập peer, transfer mode, v.v. Nó cũng bao gồm các signal cho phép bạn biết khi peer kết nối hoặc ngắt kết nối.

Interface của class này có thể abstraction hầu hết các loại network layer, topology và library. Theo mặc định, Godot cung cấp một triển khai dựa trên ENet (:ref:`ENetMultiplayerPeer <class_ENetMultiplayerPeer>`), một triển khai dựa trên WebRTC (:ref:`WebRTCMultiplayerPeer <class_WebRTCMultiplayerPeer>`) và một triển khai dựa trên WebSocket (:ref:`WebSocketMultiplayerPeer <class_WebSocketMultiplayerPeer>`), nhưng cũng có thể dùng nó để triển khai các mobile API (cho WiFi ad hoc, Bluetooth) hoặc các network API tùy chỉnh dành riêng cho thiết bị/console.

Trong hầu hết trường hợp phổ biến, không khuyến khích sử dụng trực tiếp object này, vì Godot cung cấp các tiện ích networking ở cấp cao hơn nữa. Tuy vậy, object này vẫn được cung cấp trong trường hợp game có nhu cầu cụ thể đối với API cấp thấp hơn.

Các lưu ý khi hosting
---------------------

Khi hosting một server, các client trong :abbr:`LAN (Local Area Network)` có thể kết nối bằng địa chỉ IP nội bộ, thường có dạng ``192.168.*.*``. Địa chỉ IP nội bộ này **không** thể được các client ngoài LAN/Internet truy cập.

Trên Windows, bạn có thể tìm địa chỉ IP nội bộ bằng cách mở command prompt và nhập ``ipconfig``. Trên macOS, mở Terminal và nhập ``ifconfig``. Trên Linux, mở terminal và nhập ``ip addr``.

Nếu bạn hosting server trên máy của mình và muốn các client ngoài LAN kết nối đến đó, có lẽ bạn sẽ phải *forward* port của server trên router. Đây là yêu cầu cần thiết để server có thể truy cập từ Internet, vì hầu hết kết nối gia đình đều sử dụng `NAT <https://en.wikipedia.org/wiki/Network_address_translation>`__. API multiplayer cấp cao của Godot chỉ sử dụng UDP, vì vậy bạn phải forward port bằng UDP, không chỉ TCP.

Sau khi forward một UDP port và đảm bảo server sử dụng port đó, bạn có thể dùng `this website <https://icanhazip.com/>`__ để tìm địa chỉ IP public của mình. Sau đó cung cấp địa chỉ IP public này cho mọi client Internet muốn kết nối đến server của bạn.

API multiplayer cấp cao của Godot sử dụng một phiên bản ENet đã được sửa đổi, cho phép hỗ trợ IPv6 đầy đủ.

Khởi tạo network
----------------

Networking cấp cao trong Godot được quản lý bởi :ref:`SceneTree <class_SceneTree>`.

Mỗi node có một property ``multiplayer``, là tham chiếu đến instance ``MultiplayerAPI`` được scene tree cấu hình cho node đó. Ban đầu, mọi node đều được cấu hình với cùng một object ``MultiplayerAPI`` mặc định.

Bạn có thể tạo một object ``MultiplayerAPI`` mới và gán nó cho một ``NodePath`` trong scene tree; thao tác này sẽ ghi đè ``multiplayer`` cho node tại path đó và tất cả node con của nó. Nhờ vậy, các node cùng cấp có thể được cấu hình với những peer khác nhau, cho phép chạy đồng thời một server và một client trong cùng một instance của Godot.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Theo mặc định, các expression này có thể dùng thay thế cho nhau.
    multiplayer # Lấy object MultiplayerAPI được cấu hình cho node này.
    get_tree().get_multiplayer() # Lấy object MultiplayerAPI mặc định.

 .. code-tab:: csharp

    // Theo mặc định, các expression này có thể dùng thay thế cho nhau.
    Multiplayer; // Lấy object MultiplayerAPI được cấu hình cho node này.
    GetTree().GetMultiplayer(); // Lấy object MultiplayerAPI mặc định.

Để khởi tạo networking, phải tạo một object ``MultiplayerPeer``, khởi tạo nó với vai trò server hoặc client, rồi truyền nó vào ``MultiplayerAPI``.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Tạo client.
    var peer = ENetMultiplayerPeer.new()
    peer.create_client(IP_ADDRESS, PORT)
    multiplayer.multiplayer_peer = peer

    # Tạo server.
    var peer = ENetMultiplayerPeer.new()
    peer.create_server(PORT, MAX_CLIENTS)
    multiplayer.multiplayer_peer = peer

 .. code-tab:: csharp

    // Tạo client.
    var peer = new ENetMultiplayerPeer();
    peer.CreateClient(IPAddress, Port);
    Multiplayer.MultiplayerPeer = peer;

    // Tạo server.
    var peer = new ENetMultiplayerPeer();
    peer.CreateServer(Port, MaxClients);
    Multiplayer.MultiplayerPeer = peer;

Để kết thúc networking:

.. tabs::
 .. code-tab:: gdscript GDScript

    multiplayer.multiplayer_peer = OfflineMultiplayerPeer.new()

 .. code-tab:: csharp

    Multiplayer.MultiplayerPeer = null;

.. warning::

    Khi export sang Android, hãy đảm bảo bật permission ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi hình thức giao tiếp network.

Quản lý connection
------------------

Mỗi peer được gán một ID duy nhất. ID của server luôn là 1, còn client được gán một số nguyên dương ngẫu nhiên.

Bạn có thể phản hồi việc kết nối hoặc ngắt kết nối bằng cách kết nối đến các signal của ``MultiplayerAPI``:

- ``peer_connected(id: int)`` Signal này được phát ra với ID của peer vừa kết nối trên mỗi peer khác, và trên peer mới nhiều lần, mỗi lần với ID của một peer khác. - ``peer_disconnected(id: int)`` Signal này được phát ra trên mọi peer còn lại khi một peer ngắt kết nối.

Các signal còn lại chỉ được phát ra trên client:

- ``connected_to_server()`` - ``connection_failed()`` - ``server_disconnected()``

Để lấy ID duy nhất của peer liên kết:

.. tabs::
 .. code-tab:: gdscript GDScript

    multiplayer.get_unique_id()

 .. code-tab:: csharp

    Multiplayer.GetUniqueId();


Để kiểm tra peer là server hay client:

.. tabs::
 .. code-tab:: gdscript GDScript

    multiplayer.is_server()

 .. code-tab:: csharp

    Multiplayer.IsServer();

.. _doc_high_level_multiplayer_rpcs:

Remote procedure call
---------------------

Remote procedure calls, or RPCs, are functions that can be called on other peers. To create one, use the ``@rpc`` annotation before a function definition. To call an RPC, use ``Callable``'s method ``rpc()`` to call in every peer, or ``rpc_id()`` to call in a specific peer.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _ready():
        if multiplayer.is_server():
            print_once_per_client.rpc()

    @rpc
    func print_once_per_client():
        print("I will be printed to the console once per each connected client.")

 .. code-tab:: csharp

    public override void _Ready()
    {
        if (Multiplayer.IsServer())
        {
            Rpc(MethodName.PrintOncePerClient);
        }
    }

    [Rpc]
    private void PrintOncePerClient()
    {
        GD.Print("I will be printed to the console once per each connected client.");
    }


RPC sẽ không serialize Object hoặc Callable.

Để một remote call thành công, node gửi và node nhận cần có cùng ``NodePath``, nghĩa là chúng phải có cùng name. Khi sử dụng ``add_child()`` cho các node dự kiến sẽ dùng RPC, hãy đặt argument ``force_readable_name`` thành ``true``.

.. warning::

    Nếu một hàm được chú thích bằng ``@rpc`` trong client script (tương ứng server script), thì hàm này cũng phải được khai báo trong server script (tương ứng client script). Cả hai RPC phải có cùng signature, được đánh giá bằng checksum của **tất cả RPC**. Tất cả RPC trong một script được kiểm tra cùng lúc, và mọi RPC phải được khai báo trong cả client script lẫn server script, **kể cả những hàm hiện không được sử dụng**.

    Signature của RPC bao gồm khai báo ``@rpc()``, hàm, kiểu trả về, **và** NodePath. Nếu một RPC nằm trong script được gắn vào ``/root/Main/Node1``, thì nó phải nằm chính xác trên cùng path và node trong cả client script lẫn server script. Các đối số của hàm không được kiểm tra sự tương ứng giữa mã server và client (ví dụ: ``func sendstuff():`` và ``func sendstuff(arg1, arg2):`` **sẽ vượt qua** việc đối chiếu signature).

    Nếu không đáp ứng các điều kiện này (nếu tất cả RPC không vượt qua việc đối chiếu signature), script có thể in ra lỗi hoặc gây ra hành vi không mong muốn. Thông báo lỗi có thể không liên quan đến hàm RPC mà bạn đang xây dựng và kiểm thử.

    Xem thêm phần giải thích và khắc phục sự cố tại `this post <https://github.com/godotengine/godot/issues/57869#issuecomment-1034215138>`__.

Chú thích này có thể nhận một số đối số, với các giá trị mặc định. ``@rpc`` tương đương với:

.. tabs::
 .. code-tab:: gdscript GDScript

    @rpc("authority", "call_remote", "reliable", 0)

 .. code-tab:: csharp

    [Rpc(MultiplayerApi.RpcMode.Authority, CallLocal = false, TransferMode = MultiplayerPeer.TransferModeEnum.Reliable, TransferChannel = 0)]

Các tham số và chức năng của chúng như sau:

``mode``:

- ``"authority"``: Chỉ authority của multiplayer mới có thể gọi từ xa. Theo mặc định, authority là server, nhưng có thể thay đổi theo từng node bằng cách sử dụng
  :ref:`Node.set_multiplayer_authority <class_Node_method_set_multiplayer_authority>`.
- ``"any_peer"``: Client được phép gọi từ xa. Hữu ích để truyền input của người dùng.

``sync``:

- ``"call_remote"``: Hàm sẽ không được gọi trên peer cục bộ. - ``"call_local"``: Hàm có thể được gọi trên peer cục bộ. Hữu ích khi server cũng là một player.

``transfer_mode``:

- ``"unreliable"`` Các packet không được xác nhận, có thể bị mất và có thể đến theo bất kỳ thứ tự nào. - ``"unreliable_ordered"`` Các packet được nhận theo thứ tự chúng được gửi đi. Điều này đạt được bằng cách bỏ qua các packet đến sau nếu một packet khác được gửi sau chúng đã được nhận. Có thể gây mất packet nếu sử dụng không đúng cách. - ``"reliable"`` Các lần thử gửi lại được thực hiện cho đến khi packet được xác nhận và thứ tự của chúng được giữ nguyên. Gây ảnh hưởng đáng kể đến hiệu năng.

``transfer_channel`` là chỉ mục channel.

3 mục đầu tiên có thể được truyền theo bất kỳ thứ tự nào, nhưng ``transfer_channel`` luôn phải ở cuối.

Có thể sử dụng hàm ``multiplayer.get_remote_sender_id()`` để lấy id duy nhất của người gửi rpc khi được sử dụng bên trong hàm được gọi bởi rpc.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_some_input(): # Được kết nối với một input nào đó.
        transfer_some_input.rpc_id(1) # Chỉ gửi input đến server.


    # Cần gọi local nếu server cũng là một player.
    @rpc("any_peer", "call_local", "reliable")
    func transfer_some_input():
        # Server biết ai đã gửi input.
        var sender_id = multiplayer.get_remote_sender_id()
        # Xử lý input và tác động đến game logic.

 .. code-tab:: csharp

    private void OnSomeInput() // Được kết nối với một input nào đó.
    {
        RpcId(1, MethodName.TransferSomeInput); // Chỉ gửi input đến server.
    }

    // Cần gọi local nếu server cũng là một player.
    [Rpc(MultiplayerApi.RpcMode.AnyPeer, CallLocal = true, TransferMode = MultiplayerPeer.TransferModeEnum.Reliable)]
    private void TransferSomeInput()
    {
        // Server biết ai đã gửi input.
        int senderId = Multiplayer.GetRemoteSenderId();
        // Xử lý input và tác động đến game logic.
    }

.. note::

    Các phương thức RPC phải được định nghĩa trên các class dẫn xuất từ :ref:`class_Node`. Việc cố gắng sử dụng các lệnh gọi RPC cấp cao trên các phương thức chỉ được định nghĩa trong những class không phải Node (chẳng hạn như Resource) sẽ dẫn đến lỗi runtime.

Channels
--------
Các giao thức networking hiện đại hỗ trợ channel, tức các kết nối riêng biệt bên trong một kết nối. Điều này cho phép có nhiều luồng packet mà không gây ảnh hưởng lẫn nhau.

Ví dụ: các message liên quan đến chat trong game và một số message gameplay cốt lõi đều nên được gửi một cách đáng tin cậy, nhưng một message gameplay không nên phải chờ message chat được xác nhận. Có thể đạt được điều này bằng cách sử dụng các channel khác nhau.

Channel cũng hữu ích khi được sử dụng với chế độ truyền unreliable ordered. Việc gửi các packet có kích thước thay đổi bằng chế độ truyền này có thể gây mất packet, vì các packet đến chậm hơn sẽ bị bỏ qua. Việc tách chúng thành nhiều luồng gồm các packet đồng nhất bằng cách sử dụng channel cho phép truyền theo thứ tự với ít mất packet, mà không chịu mức độ trễ do chế độ reliable gây ra.

Channel mặc định có chỉ mục 0 thực ra là ba channel khác nhau - mỗi channel tương ứng với một chế độ truyền.

Ví dụ triển khai lobby
----------------------

Đây là một lobby mẫu có thể xử lý việc peer tham gia và rời đi, thông báo cho các UI scene thông qua signal, đồng thời bắt đầu game sau khi tất cả client đã tải game scene.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node

    # Autoload có tên Lobby

    # Các signal này có thể được kết nối với một UI lobby scene hoặc game scene.
    signal player_connected(peer_id, player_info)
    signal player_disconnected(peer_id)
    signal server_disconnected

    const PORT = 7000
    const DEFAULT_SERVER_IP = "127.0.0.1" # IPv4 localhost
    const MAX_CONNECTIONS = 20

    # Nơi này sẽ chứa thông tin người chơi của mọi player,
    # với các key là ID duy nhất của từng player.
    var players = {}

    # Đây là thông tin của player cục bộ. Thông tin này nên được sửa đổi cục bộ
    # trước khi kết nối được thiết lập. Nó sẽ được truyền đến mọi peer khác.
    # Ví dụ, giá trị của "name" có thể được đặt thành nội dung mà player
    # đã nhập trong một UI scene.
    var player_info = {"name": "Name"}

    var players_loaded = 0



    func _ready():
        multiplayer.peer_connected.connect(_on_player_connected)
        multiplayer.peer_disconnected.connect(_on_player_disconnected)
        multiplayer.connected_to_server.connect(_on_connected_ok)
        multiplayer.connection_failed.connect(_on_connected_fail)
        multiplayer.server_disconnected.connect(_on_server_disconnected)


    func join_game(address = ""):
        if address.is_empty():
            address = DEFAULT_SERVER_IP
        var peer = ENetMultiplayerPeer.new()
        var error = peer.create_client(address, PORT)
        if error:
            return error
        multiplayer.multiplayer_peer = peer


    func create_game():
        var peer = ENetMultiplayerPeer.new()
        var error = peer.create_server(PORT, MAX_CONNECTIONS)
        if error:
            return error
        multiplayer.multiplayer_peer = peer

        players[1] = player_info
        player_connected.emit(1, player_info)


    func remove_multiplayer_peer():
        multiplayer.multiplayer_peer = OfflineMultiplayerPeer.new()
        players.clear()


    # Khi server quyết định bắt đầu game từ một UI scene,
    # do Lobby.load_game.rpc(filepath)
    @rpc("call_local", "reliable")
    func load_game(game_scene_path):
        get_tree().change_scene_to_file(game_scene_path)


    # Mỗi peer sẽ gọi hàm này khi đã tải game scene.
    @rpc("any_peer", "call_local", "reliable")
    func player_loaded():
        if multiplayer.is_server():
            players_loaded += 1
            if players_loaded == players.size():
                $/root/Game.start_game()
                players_loaded = 0


    # Khi một peer kết nối, hãy gửi thông tin player của tôi cho nó.
    # Điều này cho phép truyền toàn bộ dữ liệu mong muốn của từng player, không chỉ ID duy nhất.
    func _on_player_connected(id):
        _register_player.rpc_id(id, player_info)


    @rpc("any_peer", "reliable")
    func _register_player(new_player_info):
        var new_player_id = multiplayer.get_remote_sender_id()
        players[new_player_id] = new_player_info
        player_connected.emit(new_player_id, new_player_info)


    func _on_player_disconnected(id):
        players.erase(id)
        player_disconnected.emit(id)


    func _on_connected_ok():
        var peer_id = multiplayer.get_unique_id()
        players[peer_id] = player_info
        player_connected.emit(peer_id, player_info)


    func _on_connected_fail():
        remove_multiplayer_peer()


    func _on_server_disconnected():
        remove_multiplayer_peer()
        players.clear()
        server_disconnected.emit()

 .. code-tab:: csharp

    using Godot;

    public partial class Lobby : Node
    {
        public static Lobby Instance { get; private set; }

        // Các signal này có thể được kết nối với một UI lobby scene hoặc game scene.
        [Signal]
        public delegate void PlayerConnectedEventHandler(int peerId, Godot.Collections.Dictionary<string, string> playerInfo);
        [Signal]
        public delegate void PlayerDisconnectedEventHandler(int peerId);
        [Signal]
        public delegate void ServerDisconnectedEventHandler();

        private const int Port = 7000;
        private const string DefaultServerIP = "127.0.0.1"; // IPv4 localhost
        private const int MaxConnections = 20;

        // Nơi này sẽ chứa thông tin người chơi của mọi player,
        // với các key là ID duy nhất của từng player.
        private Godot.Collections.Dictionary<long, Godot.Collections.Dictionary<string, string>> _players = new Godot.Collections.Dictionary<long, Godot.Collections.Dictionary<string, string>>();

        // Đây là thông tin của player cục bộ. Thông tin này nên được sửa đổi cục bộ
        // trước khi kết nối được thiết lập. Nó sẽ được truyền đến mọi peer khác.
        // Ví dụ, giá trị của "name" có thể được đặt thành nội dung mà player
        // đã nhập trong một UI scene.
        private Godot.Collections.Dictionary<string, string> _playerInfo = new Godot.Collections.Dictionary<string, string>()
        {
            { "Name", "PlayerName" },
        };

        private int _playersLoaded = 0;

        public override void _Ready()
        {
            Instance = this;
            Multiplayer.PeerConnected += OnPlayerConnected;
            Multiplayer.PeerDisconnected += OnPlayerDisconnected;
            Multiplayer.ConnectedToServer += OnConnectOk;
            Multiplayer.ConnectionFailed += OnConnectionFail;
            Multiplayer.ServerDisconnected += OnServerDisconnected;
        }

        private Error JoinGame(string address = "")
        {
            if (string.IsNullOrEmpty(address))
            {
                address = DefaultServerIP;
            }

            var peer = new ENetMultiplayerPeer();
            Error error = peer.CreateClient(address, Port);

            if (error != Error.Ok)
            {
                return error;
            }

            Multiplayer.MultiplayerPeer = peer;
            return Error.Ok;
        }

        private Error CreateGame()
        {
            var peer = new ENetMultiplayerPeer();
            Error error = peer.CreateServer(Port, MaxConnections);

            if (error != Error.Ok)
            {
                return error;
            }

            Multiplayer.MultiplayerPeer = peer;
            _players[1] = _playerInfo;
            EmitSignal(SignalName.PlayerConnected, 1, _playerInfo);
            return Error.Ok;
        }

        private void RemoveMultiplayerPeer()
        {
            Multiplayer.MultiplayerPeer = null;
            _players.Clear();
        }

        // Khi server quyết định bắt đầu game từ một UI scene,
        // do Rpc(Lobby.MethodName.LoadGame, filePath);
        [Rpc(CallLocal = true,TransferMode = MultiplayerPeer.TransferModeEnum.Reliable)]
        private void LoadGame(string gameScenePath)
        {
            GetTree().ChangeSceneToFile(gameScenePath);
        }

        // Mỗi peer sẽ gọi hàm này khi đã tải game scene.
        [Rpc(MultiplayerApi.RpcMode.AnyPeer,CallLocal = true,TransferMode = MultiplayerPeer.TransferModeEnum.Reliable)]
        private void PlayerLoaded()
        {
            if (Multiplayer.IsServer())
            {
                _playersLoaded += 1;
                if (_playersLoaded == _players.Count)
                {
                    GetNode<Game>("/root/Game").StartGame();
                    _playersLoaded = 0;
                }
            }
        }

        // Khi một peer kết nối, hãy gửi thông tin player của tôi cho nó.
        // Điều này cho phép truyền toàn bộ dữ liệu mong muốn của từng player, không chỉ ID duy nhất.
        private void OnPlayerConnected(long id)
        {
            RpcId(id, MethodName.RegisterPlayer, _playerInfo);
        }

        [Rpc(MultiplayerApi.RpcMode.AnyPeer,TransferMode = MultiplayerPeer.TransferModeEnum.Reliable)]
        private void RegisterPlayer(Godot.Collections.Dictionary<string, string> newPlayerInfo)
        {
            int newPlayerId = Multiplayer.GetRemoteSenderId();
            _players[newPlayerId] = newPlayerInfo;
            EmitSignal(SignalName.PlayerConnected, newPlayerId, newPlayerInfo);
        }

        private void OnPlayerDisconnected(long id)
        {
            _players.Remove(id);
            EmitSignal(SignalName.PlayerDisconnected, id);
        }

        private void OnConnectOk()
        {
            int peerId = Multiplayer.GetUniqueId();
            _players[peerId] = _playerInfo;
            EmitSignal(SignalName.PlayerConnected, peerId, _playerInfo);
        }

        private void OnConnectionFail()
        {
            Multiplayer.MultiplayerPeer = null;
        }

        private void OnServerDisconnected()
        {
            Multiplayer.MultiplayerPeer = null;
            _players.Clear();
            EmitSignal(SignalName.ServerDisconnected);
        }
    }

Root node của game scene nên được đặt tên là Game. Trong script được gắn vào node đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node3D # Hoặc Node2D.



    func _ready():
        # Cấu hình trước game.

        Lobby.player_loaded.rpc_id(1) # Thông báo cho server rằng peer này đã tải xong.


    # Chỉ được gọi trên server.
    func start_game():
        # Tất cả peer đã sẵn sàng nhận RPC trong scene này.

 .. code-tab:: csharp

    using Godot;

    public partial class Game : Node3D // Hoặc Node2D.
    {
        public override void _Ready()
        {
            // Cấu hình trước game.

            Lobby.Instance.RpcId(1, Lobby.MethodName.PlayerLoaded); // Thông báo cho server rằng peer này đã tải xong.
        }

        // Chỉ được gọi trên server.
        public void StartGame()
        {
            // Tất cả peer đã sẵn sàng nhận RPC trong scene này.
        }
    }

Export cho dedicated server
---------------------------

Sau khi tạo xong một game multiplayer, bạn có thể muốn export game để chạy trên dedicated server không có GPU. Xem
:ref:`doc_exporting_for_dedicated_servers` for more information.

.. note::

    Các mẫu code trên trang này không được thiết kế để chạy trên dedicated server. Bạn sẽ phải sửa chúng để server không được xem là một player. Bạn cũng sẽ phải sửa cơ chế bắt đầu game để player đầu tiên tham gia có thể bắt đầu game.

Authentication
--------------

Trước khi host game online cho công chúng, bạn có thể cân nhắc thêm authentication và bảo vệ các RPC khỏi việc truy cập chưa được xác thực. Bạn có thể sử dụng cơ chế authentication tích hợp sẵn của :ref:`SceneMultiplayer <class_SceneMultiplayer>` cho việc này.

Trên server:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Đặt đoạn này sau `multiplayer.multiplayer_peer = peer`.
    multiplayer.auth_timout = 3
    multiplayer.auth_callback = func(peer_id: int, payload: PackedByteArray):
        var auth_data: Dictionary = JSON.parse_string(payload.get_string_from_utf8())
        # Logic authentication của bạn (chẳng hạn như kiểm tra username/password được cung cấp với cơ sở dữ liệu)

        # Thông báo cho MultiplayerAPI rằng authentication đã thành công
        if authentication_successful:
            multiplayer.complete_auth(peer_id)

Trên client:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Đặt đoạn này sau `multiplayer.multiplayer_peer = peer`.
    multiplayer.auth_callback = func:
        # Ta phải thiết lập điều này trên client để signal `peer_authenticating`
        # được phát.
        pass
    multiplayer.peer_authenticating.connect(func(peer_id: int):
            var auth_data = {
                "username": "username",
                "password": "password",
            }
            multiplayer.send_auth(1, JSON.stringify(auth_data).to_utf8_buffer())

            # Thông báo cho MultiplayerAPI rằng authentication đã thành công.
            multiplayer.complete_auth(peer_id)

Ngay khi các phương thức :ref:`complete_auth() <class_SceneMultiplayer_method_complete_auth>` của client và server đều đã được gọi, kết nối được xem là đã thiết lập và các signal ``connected_to_server`` và ``peer_connected`` sẽ được phát.

Thiết kế multiplayer an toàn
----------------------------

High-level multiplayer API của Godot giúp xây dựng game network dễ dàng hơn, nhưng không tự động làm cho game logic trở nên an toàn. Đối với game multiplayer cạnh tranh hoặc lâu dài, hãy xem mọi input từ client là không đáng tin cậy.

Một sai lầm phổ biến là để client toàn quyền quyết định các trạng thái game quan trọng, chẳng hạn như vị trí player, kết quả chiến đấu, thay đổi inventory hoặc kết quả trận đấu. Điều này có thể khiến việc gian lận dễ dàng hơn nhiều và dẫn đến tình trạng mất đồng bộ ("desync") thường xuyên hơn.

Nhìn chung, hãy ưu tiên các pattern sau:

- Sử dụng logic do server kiểm soát (server-authoritative) cho các quyết định quan trọng đối với gameplay. - Xác thực các đối số RPC trước khi áp dụng chúng vào trạng thái game. - Tránh tin tưởng các vị trí, bộ hẹn giờ, thời gian cooldown hoặc giá trị tài nguyên do client báo cáo mà không kiểm tra. - Thêm các bước kiểm tra an toàn và giới hạn tần suất cho những hành động có thể được kích hoạt thường xuyên.

Tóm lại, bạn nên thiết kế networking sao cho server vẫn là nguồn sự thật duy nhất đối với các trạng thái quan trọng.

Ví dụ, thay vì chấp nhận trực tiếp vị trí cuối cùng của client, hãy cân nhắc gửi input hoặc ý định di chuyển của người chơi đến authority/server, sau đó xác thực và áp dụng kết quả tại đó. Cách này đi kèm một số đánh đổi (chẳng hạn như hiệu năng phía server và độ phức tạp do cần prediction phía client), nhưng sẽ khiến kẻ tấn công khó gian lận hơn nhiều bằng cách gửi dữ liệu giả mạo.

Xem `Choosing the right network model for your multiplayer game <https://mas-bandwidth.com/choosing-the-right-network-model-for-your-multiplayer-game/>`__ để biết thêm thông tin về các mô hình multiplayer khác nhau và những ảnh hưởng của chúng đối với bảo mật.
