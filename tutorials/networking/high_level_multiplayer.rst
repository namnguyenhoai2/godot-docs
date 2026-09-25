.. _doc_high_level_multiplayer:

Multiplayer cấp cao
===================

API cấp cao và cấp thấp
-----------------------

Phần sau giải thích sự khác biệt giữa networking cấp cao và cấp thấp trong Godot, cùng với một số kiến thức nền tảng. Nếu bạn muốn bắt tay ngay vào việc thêm networking cho các node đầu tiên, hãy chuyển xuống phần `Khởi tạo mạng <Initializing the network_>`_ bên dưới. Nhưng hãy nhớ đọc phần còn lại sau đó!

Godot luôn hỗ trợ networking cấp thấp tiêu chuẩn thông qua :abbr:`UDP (User Datagram Protocol)`, :abbr:`TCP (Transmission Control Protocol)` và một số giao thức cấp cao hơn như :abbr:`HTTP (Hypertext Transfer Protocol)` và :abbr:`SSL (Secure Sockets Layer)`. Các giao thức này rất linh hoạt và có thể được dùng cho gần như mọi mục đích. Tuy nhiên, việc sử dụng chúng để tự đồng bộ hóa trạng thái trò chơi có thể đòi hỏi rất nhiều công sức. Đôi khi không thể tránh được công việc đó hoặc việc này hoàn toàn đáng làm, chẳng hạn khi làm việc với một triển khai server tùy chỉnh ở backend. Nhưng trong hầu hết trường hợp, bạn nên cân nhắc API networking cấp cao của Godot, vốn hy sinh một phần khả năng kiểm soát chi tiết của networking cấp thấp để đổi lấy sự dễ sử dụng cao hơn.

Điều này là do những hạn chế vốn có của các giao thức cấp thấp:

- TCP đảm bảo các packet luôn đến nơi một cách đáng tin cậy và đúng thứ tự, nhưng độ trễ thường cao hơn do cơ chế sửa lỗi. Đây cũng là một giao thức khá phức tạp vì nó hiểu khái niệm "connection" và tối ưu cho những mục tiêu thường không phù hợp với các ứng dụng như trò chơi multiplayer. Các packet được đệm để gửi theo những lô lớn hơn, đánh đổi chi phí xử lý trên từng packet thấp hơn lấy độ trễ cao hơn. Điều này có thể hữu ích với những thứ như HTTP, nhưng nhìn chung không phù hợp với trò chơi. Một phần trong số này có thể được cấu hình và vô hiệu hóa (ví dụ: vô hiệu hóa "Nagle's algorithm" cho kết nối TCP).
- UDP là một giao thức đơn giản hơn, chỉ gửi các packet (và không có khái niệm về "connection"). Không có cơ chế sửa lỗi nên giao thức này khá nhanh (độ trễ thấp), nhưng packet có thể bị mất trên đường truyền hoặc được nhận không đúng thứ tự. Ngoài ra, MTU (kích thước packet tối đa) của UDP thường nhỏ (chỉ vài trăm byte), vì vậy việc truyền các packet lớn hơn đòi hỏi phải chia nhỏ, sắp xếp lại và thử lại nếu một phần bị lỗi.

Nhìn chung, có thể xem TCP là đáng tin cậy, có thứ tự và chậm; còn UDP là không đáng tin cậy, không có thứ tự và nhanh. Do sự khác biệt lớn về hiệu năng, việc xây dựng lại những phần của TCP cần thiết cho trò chơi (khả năng tin cậy và thứ tự packet tùy chọn), đồng thời tránh những phần không mong muốn (các tính năng kiểm soát tắc nghẽn/lưu lượng, Nagle's algorithm, v.v.) thường là hợp lý. Vì vậy, hầu hết game engine đều đi kèm một triển khai như vậy và Godot cũng không ngoại lệ.

Tóm lại, bạn có thể sử dụng API networking cấp thấp để có quyền kiểm soát tối đa và tự triển khai mọi thứ trên các giao thức mạng cơ bản, hoặc sử dụng API cấp cao dựa trên :ref:`SceneTree <class_SceneTree>`, vốn đảm nhiệm phần lớn công việc phức tạp ở phía sau theo cách nhìn chung đã được tối ưu hóa.

.. note:: Hầu hết các nền tảng được Godot hỗ trợ đều cung cấp toàn bộ hoặc phần lớn các tính năng networking cấp cao và cấp thấp đã đề cập. Tuy nhiên, vì networking luôn phụ thuộc nhiều vào phần cứng và hệ điều hành, một số tính năng có thể thay đổi hoặc không khả dụng trên một số nền tảng đích. Đáng chú ý nhất, nền tảng HTML5 hiện hỗ trợ WebSockets và WebRTC nhưng thiếu một số tính năng cấp cao hơn, cũng như không cho phép truy cập trực tiếp vào các giao thức cấp thấp như TCP và UDP.

.. note:: Tìm hiểu thêm về TCP/IP, UDP và networking: https://gafferongames.com/post/udp_vs_tcp/

          Gaffer On Games có nhiều bài viết hữu ích về networking trong trò chơi (`tại đây <https://gafferongames.com/categories/game-networking/>`__), bao gồm `phần giới thiệu toàn diện về các mô hình networking trong trò chơi <https://gafferongames.com/post/what_every_programmer_needs_to_know_about_game_networking/>`__.

.. warning:: Việc thêm networking vào trò chơi đi kèm với một số trách nhiệm. Nếu thực hiện không đúng, việc này có thể khiến ứng dụng của bạn dễ bị tấn công và có thể dẫn đến gian lận hoặc khai thác lỗ hổng. Kẻ tấn công thậm chí có thể xâm phạm các máy mà ứng dụng của bạn chạy trên đó, rồi sử dụng server của bạn để gửi spam, tấn công người khác hoặc đánh cắp dữ liệu của người dùng nếu họ chơi trò chơi của bạn.

             Điều này luôn đúng khi có networking và không liên quan gì đến Godot. Tất nhiên, bạn có thể thử nghiệm, nhưng khi phát hành một ứng dụng có networking, hãy luôn xử lý mọi vấn đề bảo mật có thể xảy ra.

Trừu tượng hóa cấp trung
------------------------

Trước khi tìm hiểu cách chúng ta muốn đồng bộ hóa một trò chơi qua mạng, việc hiểu cách API mạng cơ sở dùng cho việc đồng bộ hóa hoạt động có thể rất hữu ích.

Godot sử dụng một object cấp trung :ref:`MultiplayerPeer <class_MultiplayerPeer>`. Object này không được thiết kế để tạo trực tiếp, mà được thiết kế để cho phép một số triển khai C++ cung cấp nó.

Object này kế thừa từ :ref:`PacketPeer <class_PacketPeer>`, vì vậy nó kế thừa tất cả các phương thức hữu ích để serialize, gửi và nhận dữ liệu. Ngoài ra, nó bổ sung các phương thức để thiết lập peer, transfer mode, v.v. Nó cũng bao gồm các signal cho phép bạn biết khi peer kết nối hoặc ngắt kết nối.

Giao diện class này có thể trừu tượng hóa hầu hết các loại network layer, topology và library. Theo mặc định, Godot cung cấp một triển khai dựa trên ENet (:ref:`ENetMultiplayerPeer <class_ENetMultiplayerPeer>`), một triển khai dựa trên WebRTC (:ref:`WebRTCMultiplayerPeer <class_WebRTCMultiplayerPeer>`) và một triển khai dựa trên WebSocket (:ref:`WebSocketMultiplayerPeer <class_WebSocketMultiplayerPeer>`), nhưng giao diện này cũng có thể được dùng để triển khai các API dành cho thiết bị di động (cho WiFi ad hoc, Bluetooth) hoặc các API networking tùy chỉnh dành riêng cho thiết bị/console.

Trong hầu hết trường hợp thông thường, không nên sử dụng trực tiếp object này, vì Godot cung cấp các tiện ích networking cấp cao hơn nữa. Tuy vậy, object này vẫn được cung cấp phòng khi trò chơi có những nhu cầu cụ thể đối với API cấp thấp hơn.

Các lưu ý khi hosting
---------------------

Khi hosting một server, các client trên :abbr:`LAN (Local Area Network)` của bạn có thể kết nối bằng địa chỉ IP nội bộ, thường có dạng ``192.168.*.*``. Địa chỉ IP nội bộ này **không** thể được các client ngoài LAN/Internet truy cập.

Trên Windows, bạn có thể tìm địa chỉ IP nội bộ bằng cách mở command prompt và nhập ``ipconfig``. Trên macOS, mở Terminal và nhập ``ifconfig``. Trên Linux, mở terminal và nhập ``ip addr``.

Nếu bạn hosting server trên máy của mình và muốn các client ngoài LAN kết nối đến đó, có lẽ bạn sẽ phải *forward* port của server trên router. Việc này cần thiết để server có thể được truy cập từ Internet, vì hầu hết các kết nối gia đình đều sử dụng `NAT <https://en.wikipedia.org/wiki/Network_address_translation>`__. API multiplayer cấp cao của Godot chỉ sử dụng UDP, vì vậy bạn phải forward port bằng UDP, không chỉ TCP.

Sau khi forward một port UDP và đảm bảo server sử dụng port đó, bạn có thể dùng `trang web này <https://icanhazip.com/>`__ để tìm địa chỉ IP công khai của mình. Sau đó, cung cấp địa chỉ IP công khai này cho mọi client Internet muốn kết nối đến server của bạn.

API multiplayer cấp cao của Godot sử dụng một phiên bản ENet đã được sửa đổi, cho phép hỗ trợ IPv6 đầy đủ.

.. _`Initializing the network`:

Khởi tạo mạng
-------------

Networking cấp cao trong Godot được quản lý bởi :ref:`SceneTree <class_SceneTree>`.

Mỗi node có một thuộc tính ``multiplayer``, là tham chiếu đến instance ``MultiplayerAPI`` được scene tree cấu hình cho node đó. Ban đầu, mọi node đều được cấu hình với cùng một object ``MultiplayerAPI`` mặc định.

Bạn có thể tạo một object ``MultiplayerAPI`` mới và gán nó cho một ``NodePath`` trong scene tree. Việc này sẽ ghi đè ``multiplayer`` cho node tại path đó và tất cả node con của nó. Nhờ đó, các node anh em có thể được cấu hình với những peer khác nhau, cho phép chạy đồng thời một server và một client trong cùng một instance Godot.

.. tabs::
 .. code-tab:: gdscript GDScript

    # Theo mặc định, các biểu thức này có thể thay thế cho nhau.
    multiplayer # Lấy đối tượng MultiplayerAPI được cấu hình cho node này.
    get_tree().get_multiplayer() # Lấy đối tượng MultiplayerAPI mặc định.

 .. code-tab:: csharp

    // Theo mặc định, các biểu thức này có thể thay thế cho nhau.
    Multiplayer; // Lấy đối tượng MultiplayerAPI được cấu hình cho node này.
    GetTree().GetMultiplayer(); // Lấy đối tượng MultiplayerAPI mặc định.

Để khởi tạo networking, phải tạo một đối tượng ``MultiplayerPeer``, khởi tạo đối tượng đó dưới dạng server hoặc client, rồi truyền vào ``MultiplayerAPI``.

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

    Khi export sang Android, hãy bật quyền ``INTERNET`` trong export preset của Android trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi dạng giao tiếp mạng.

Quản lý kết nối
---------------

Mỗi peer được gán một ID duy nhất. ID của server luôn là 1, còn các client được gán một số nguyên dương ngẫu nhiên.

Có thể phản hồi các kết nối hoặc ngắt kết nối bằng cách kết nối với các signal của ``MultiplayerAPI``:

- ``peer_connected(id: int)`` Signal này được phát với ID của peer vừa kết nối trên mỗi peer khác, và trên peer mới nhiều lần, mỗi lần với ID của một peer khác.
- ``peer_disconnected(id: int)`` Signal này được phát trên mọi peer còn lại khi một peer ngắt kết nối.

Các signal còn lại chỉ được phát trên client:

- ``connected_to_server()``
- ``connection_failed()``
- ``server_disconnected()``

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

Các lệnh gọi thủ tục từ xa
--------------------------

Các lệnh gọi thủ tục từ xa, hay RPC, là những hàm có thể được gọi trên các peer khác. Để tạo một RPC, hãy sử dụng annotation ``@rpc`` trước phần định nghĩa hàm. Để gọi một RPC, hãy sử dụng phương thức ``rpc()`` của ``Callable`` để gọi trên mọi peer, hoặc ``rpc_id()`` để gọi trên một peer cụ thể.

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

Để một lệnh gọi từ xa thành công, node gửi và node nhận phải có cùng ``NodePath``, nghĩa là chúng phải có cùng tên. Khi sử dụng ``add_child()`` cho các node dự kiến sử dụng RPC, hãy đặt đối số ``force_readable_name`` thành ``true``.

.. warning::

    Nếu một hàm được chú thích bằng ``@rpc`` trong client script (tương ứng là server script), thì hàm này cũng phải được khai báo trong server script (tương ứng là client script). Cả hai RPC phải có cùng signature, được đánh giá bằng checksum của **all RPCs**. Tất cả RPC trong một script được kiểm tra cùng lúc, và mọi RPC phải được khai báo trong cả client script lẫn server script, **kể cả các hàm hiện không được sử dụng**.

    Signature của RPC bao gồm khai báo ``@rpc()``, hàm, kiểu trả về, **và** NodePath. Nếu một RPC nằm trong script được gắn vào ``/root/Main/Node1``, thì nó phải nằm chính xác tại cùng path và node trong cả client script lẫn server script. Các đối số của hàm không được kiểm tra sự tương ứng giữa mã server và client (ví dụ: ``func sendstuff():`` và ``func sendstuff(arg1, arg2):`` **sẽ vượt qua** việc kiểm tra signature).

    Nếu không đáp ứng các điều kiện này (nếu tất cả RPC không vượt qua việc kiểm tra signature), script có thể in ra lỗi hoặc gây ra hành vi không mong muốn. Thông báo lỗi có thể không liên quan đến hàm RPC mà bạn đang xây dựng và kiểm thử.

    Xem phần giải thích và khắc phục sự cố chi tiết hơn trong `bài đăng này <https://github.com/godotengine/godot/issues/57869#issuecomment-1034215138>`__.

Annotation có thể nhận một số đối số, với các giá trị mặc định. ``@rpc`` tương đương với:

.. tabs::
 .. code-tab:: gdscript GDScript

    @rpc("authority", "call_remote", "reliable", 0)

 .. code-tab:: csharp

    [Rpc(MultiplayerApi.RpcMode.Authority, CallLocal = false, TransferMode = MultiplayerPeer.TransferModeEnum.Reliable, TransferChannel = 0)]

Các tham số và chức năng của chúng như sau:

``mode``:

- ``"authority"``: Chỉ multiplayer authority mới có thể gọi từ xa. Theo mặc định, authority là server, nhưng có thể thay đổi theo từng node bằng cách sử dụng
  :ref:`Node.set_multiplayer_authority <class_Node_method_set_multiplayer_authority>`.
- ``"any_peer"``: Client được phép gọi từ xa. Hữu ích để truyền input của người dùng.

``sync``:

- ``"call_remote"``: Hàm sẽ không được gọi trên peer cục bộ.
- ``"call_local"``: Hàm có thể được gọi trên peer cục bộ. Hữu ích khi server cũng là một player.

``transfer_mode``:

- ``"unreliable"`` Các packet không được xác nhận, có thể bị mất và có thể đến theo bất kỳ thứ tự nào.
- ``"unreliable_ordered"`` Các packet được nhận theo thứ tự chúng được gửi. Điều này đạt được bằng cách bỏ qua các packet đến muộn nếu một packet khác được gửi sau chúng đã được nhận. Có thể gây mất packet nếu sử dụng không đúng cách.
- ``"reliable"`` Các lần thử gửi lại sẽ tiếp tục được thực hiện cho đến khi packet được xác nhận, và thứ tự của chúng được giữ nguyên. Gây ảnh hưởng đáng kể đến hiệu năng.

``transfer_channel`` là chỉ mục của channel.

Ba mục đầu tiên có thể được truyền theo bất kỳ thứ tự nào, nhưng ``transfer_channel`` luôn phải ở cuối.

Có thể sử dụng hàm ``multiplayer.get_remote_sender_id()`` để lấy ID duy nhất của người gửi rpc khi được dùng bên trong hàm được gọi bởi rpc.

.. tabs::
 .. code-tab:: gdscript GDScript

    func _on_some_input(): # Đã kết nối với một input nào đó.
        transfer_some_input.rpc_id(1) # Chỉ gửi input đến server.


    # Cần Call local nếu server cũng là một player.
    @rpc("any_peer", "call_local", "reliable")
    func transfer_some_input():
        # Server biết ai đã gửi input.
        var sender_id = multiplayer.get_remote_sender_id()
        # Xử lý input và tác động đến logic game.

 .. code-tab:: csharp

    private void OnSomeInput() // Đã kết nối với một input nào đó.
    {
        RpcId(1, MethodName.TransferSomeInput); // Chỉ gửi input đến server.
    }

    // Cần Call local nếu server cũng là một player.
    [Rpc(MultiplayerApi.RpcMode.AnyPeer, CallLocal = true, TransferMode = MultiplayerPeer.TransferModeEnum.Reliable)]
    private void TransferSomeInput()
    {
        // Máy chủ biết ai đã gửi dữ liệu đầu vào.
        int senderId = Multiplayer.GetRemoteSenderId();
        // Xử lý dữ liệu đầu vào và tác động đến logic trò chơi.
    }

.. note::

    Các phương thức RPC phải được định nghĩa trên các lớp dẫn xuất từ :ref:`class_Node`. Việc cố sử dụng các lệnh gọi RPC cấp cao trên những phương thức chỉ được định nghĩa trong các lớp không phải Node (chẳng hạn như Resource) sẽ gây ra lỗi runtime.

Kênh
----
Các giao thức mạng hiện đại hỗ trợ các kênh, tức là những kết nối riêng biệt bên trong một kết nối. Điều này cho phép có nhiều luồng gói tin không gây ảnh hưởng lẫn nhau.

Ví dụ, các thông báo liên quan đến chat trong trò chơi và một số thông báo gameplay cốt lõi đều nên được gửi một cách đáng tin cậy, nhưng một thông báo gameplay không nên phải chờ thông báo chat được xác nhận. Có thể thực hiện điều này bằng cách sử dụng các kênh khác nhau.

Các kênh cũng hữu ích khi được dùng với chế độ truyền không đáng tin cậy có thứ tự. Việc gửi các gói tin có kích thước khác nhau ở chế độ truyền này có thể gây mất gói, vì những gói đến chậm hơn sẽ bị bỏ qua. Tách chúng thành nhiều luồng gồm các gói tin đồng nhất bằng cách sử dụng các kênh cho phép truyền có thứ tự với ít mất gói, mà không chịu độ trễ phát sinh do chế độ đáng tin cậy.

Kênh mặc định có chỉ mục 0 thực tế là ba kênh khác nhau - mỗi kênh tương ứng với một chế độ truyền.

Triển khai lobby mẫu
--------------------

Đây là một lobby mẫu có thể xử lý việc các peer tham gia và rời đi, thông báo cho các scene UI thông qua signal, đồng thời bắt đầu trò chơi sau khi tất cả client đã tải scene trò chơi.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node

    # Autoload có tên Lobby

    # Các signal này có thể được kết nối với một scene lobby UI hoặc scene trò chơi.
    signal player_connected(peer_id, player_info)
    signal player_disconnected(peer_id)
    signal server_disconnected

    const PORT = 7000
    const DEFAULT_SERVER_IP = "127.0.0.1" # localhost IPv4
    const MAX_CONNECTIONS = 20

    # Biến này sẽ chứa thông tin người chơi của mọi người chơi,
    # với các khóa là ID duy nhất của từng người chơi.
    var players = {}

    # Đây là thông tin của người chơi cục bộ. Thông tin này nên được sửa đổi cục bộ
    # trước khi kết nối được thiết lập. Nó sẽ được truyền đến mọi peer khác.
    # Ví dụ, giá trị của "name" có thể được đặt thành nội dung mà người chơi
    # đã nhập trong một scene UI.
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


    # Khi máy chủ quyết định bắt đầu trò chơi từ một scene UI,
    # do Lobby.load_game.rpc(filepath)
    @rpc("call_local", "reliable")
    func load_game(game_scene_path):
        get_tree().change_scene_to_file(game_scene_path)


    # Mọi peer sẽ gọi hàm này sau khi đã tải scene trò chơi.
    @rpc("any_peer", "call_local", "reliable")
    func player_loaded():
        if multiplayer.is_server():
            players_loaded += 1
            if players_loaded == players.size():
                $/root/Game.start_game()
                players_loaded = 0


    # Khi một peer kết nối, hãy gửi cho peer đó thông tin người chơi của tôi.
    # Điều này cho phép truyền toàn bộ dữ liệu mong muốn của từng người chơi, không chỉ ID duy nhất.
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

        // Các signal này có thể được kết nối với một scene lobby UI hoặc scene trò chơi.
        [Signal]
        public delegate void PlayerConnectedEventHandler(int peerId, Godot.Collections.Dictionary<string, string> playerInfo);
        [Signal]
        public delegate void PlayerDisconnectedEventHandler(int peerId);
        [Signal]
        public delegate void ServerDisconnectedEventHandler();

        private const int Port = 7000;
        private const string DefaultServerIP = "127.0.0.1"; // localhost IPv4
        private const int MaxConnections = 20;

        // Biến này sẽ chứa thông tin người chơi của mọi người chơi,
        // với các khóa là ID duy nhất của từng người chơi.
        private Godot.Collections.Dictionary<long, Godot.Collections.Dictionary<string, string>> _players = new Godot.Collections.Dictionary<long, Godot.Collections.Dictionary<string, string>>();

        // Đây là thông tin của người chơi cục bộ. Thông tin này nên được sửa đổi cục bộ
        // trước khi kết nối được thiết lập. Nó sẽ được truyền đến mọi peer khác.
        // Ví dụ, giá trị của "name" có thể được đặt thành nội dung mà người chơi
        // đã nhập trong một scene UI.
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

        // Khi máy chủ quyết định bắt đầu trò chơi từ một scene UI,
        // do Rpc(Lobby.MethodName.LoadGame, filePath);
        [Rpc(CallLocal = true,TransferMode = MultiplayerPeer.TransferModeEnum.Reliable)]
        private void LoadGame(string gameScenePath)
        {
            GetTree().ChangeSceneToFile(gameScenePath);
        }

        // Mọi peer sẽ gọi hàm này sau khi đã tải scene trò chơi.
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

        // Khi một peer kết nối, hãy gửi cho peer đó thông tin người chơi của tôi.
        // Điều này cho phép truyền toàn bộ dữ liệu mong muốn của từng người chơi, không chỉ ID duy nhất.
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

Node gốc của scene trò chơi nên có tên là Game. Trong script được gắn vào node đó:

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node3D # Hoặc Node2D.



    func _ready():
        # Cấu hình trước trò chơi.

        Lobby.player_loaded.rpc_id(1) # Cho máy chủ biết rằng peer này đã tải xong.


    # Chỉ được gọi trên máy chủ.
    func start_game():
        # Tất cả peer đã sẵn sàng nhận RPC trong scene này.

 .. code-tab:: csharp

    using Godot;

    public partial class Game : Node3D // Hoặc Node2D.
    {
        public override void _Ready()
        {
            // Cấu hình trước trò chơi.

            Lobby.Instance.RpcId(1, Lobby.MethodName.PlayerLoaded); // Cho máy chủ biết rằng peer này đã tải xong.
        }

        // Chỉ được gọi trên máy chủ.
        public void StartGame()
        {
            // Tất cả peer đã sẵn sàng nhận RPC trong scene này.
        }
    }

Export cho máy chủ chuyên dụng
------------------------------

Sau khi tạo xong một trò chơi nhiều người chơi, bạn có thể muốn export trò chơi để chạy trên máy chủ chuyên dụng không có GPU. Xem
:ref:`doc_exporting_for_dedicated_servers` để biết thêm thông tin.

.. note::

    Các mẫu mã trên trang này không được thiết kế để chạy trên một dedicated server. Bạn sẽ phải sửa đổi chúng để server không bị xem là một người chơi. Bạn cũng sẽ phải sửa đổi cơ chế bắt đầu game để người chơi đầu tiên tham gia có thể bắt đầu game.

Xác thực
--------

Trước khi host game của bạn trực tuyến cho công chúng, bạn nên cân nhắc việc thêm xác thực và bảo vệ các RPC khỏi quyền truy cập chưa được xác thực. Bạn có thể sử dụng cơ chế xác thực tích hợp sẵn của :ref:`SceneMultiplayer <class_SceneMultiplayer>` cho việc này.

Trên server:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phần này được đặt sau `multiplayer.multiplayer_peer = peer`.
    multiplayer.auth_timout = 3
    multiplayer.auth_callback = func(peer_id: int, payload: PackedByteArray):
        var auth_data: Dictionary = JSON.parse_string(payload.get_string_from_utf8())
        # Logic xác thực của bạn (chẳng hạn như kiểm tra username/password được cung cấp với cơ sở dữ liệu)

        # Thông báo cho MultiplayerAPI rằng quá trình xác thực đã thành công
        if authentication_successful:
            multiplayer.complete_auth(peer_id)

Trên client:

.. tabs::
 .. code-tab:: gdscript GDScript

    # Phần này được đặt sau `multiplayer.multiplayer_peer = peer`.
    multiplayer.auth_callback = func:
        # Chúng ta phải thiết lập điều này trên client để `peer_authenticating`
        # signal được phát ra.
        pass
    multiplayer.peer_authenticating.connect(func(peer_id: int):
            var auth_data = {
                "username": "username",
                "password": "password",
            }
            multiplayer.send_auth(1, JSON.stringify(auth_data).to_utf8_buffer())

            # Thông báo cho MultiplayerAPI rằng quá trình xác thực đã thành công.
            multiplayer.complete_auth(peer_id)

Ngay khi các phương thức :ref:`complete_auth() <class_SceneMultiplayer_method_complete_auth>` của client và server đều được gọi, kết nối được xem là đã thiết lập và các signal ``connected_to_server`` và ``peer_connected`` được phát ra.

Thiết kế multiplayer an toàn
----------------------------

Multiplayer API cấp cao của Godot giúp xây dựng game có kết nối mạng dễ dàng hơn, nhưng không tự động khiến logic gameplay trở nên an toàn. Đối với các game multiplayer cạnh tranh hoặc có trạng thái lâu dài, hãy xem mọi input từ client là không đáng tin cậy.

Một sai lầm phổ biến là để client tự quyết định một cách có thẩm quyền các trạng thái game quan trọng, chẳng hạn như vị trí người chơi, kết quả chiến đấu, thay đổi inventory hoặc kết quả trận đấu. Điều này có thể khiến việc gian lận dễ dàng hơn nhiều và dẫn đến tình trạng mất đồng bộ ("desync") thường xuyên hơn.

Nhìn chung, hãy ưu tiên các mẫu sau:

- Sử dụng logic do server quyết định cho các quyết định quan trọng đối với gameplay.
- Xác thực các đối số RPC trước khi áp dụng chúng vào trạng thái game.
- Tránh tin tưởng các vị trí, timer, cooldown hoặc giá trị tài nguyên do client báo cáo nếu chưa kiểm tra.
- Thêm các bước kiểm tra an toàn và giới hạn tần suất cho những hành động có thể được kích hoạt thường xuyên.

Tóm lại, bạn nên thiết kế networking sao cho server luôn là nguồn dữ liệu chính xác cho các trạng thái quan trọng.

Ví dụ, thay vì trực tiếp chấp nhận vị trí cuối cùng do client gửi, hãy cân nhắc gửi input của người chơi hoặc ý định di chuyển đến authority/server, sau đó xác thực và áp dụng kết quả tại đó. Cách này có một số đánh đổi (chẳng hạn như hiệu năng phía server và độ phức tạp do cần dự đoán phía client), nhưng sẽ khiến kẻ tấn công khó gian lận hơn nhiều bằng cách gửi dữ liệu giả mạo.

Xem `Chọn mô hình mạng phù hợp cho game multiplayer của bạn <https://mas-bandwidth.com/choosing-the-right-network-model-for-your-multiplayer-game/>`__ để biết thêm thông tin về các mô hình multiplayer khác nhau và những hệ quả bảo mật của chúng.
