:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/DTLSServer.xml.

.. _class_DTLSServer:

DTLSServer
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp trợ giúp để triển khai máy chủ DTLS.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được sử dụng để lưu trữ trạng thái của máy chủ DTLS. Khi :ref:`setup()<class_DTLSServer_method_setup>`, lớp này chuyển đổi :ref:`PacketPeerUDP<class_PacketPeerUDP>` đã kết nối thành :ref:`PacketPeerDTLS<class_PacketPeerDTLS>` và chấp nhận chúng thông qua :ref:`take_connection()<class_DTLSServer_method_take_connection>` dưới dạng các client DTLS. Bên dưới, lớp này được sử dụng để lưu trữ trạng thái DTLS và cookie của máy chủ. Lý do cần trạng thái và cookie nằm ngoài phạm vi của tài liệu này.

Dưới đây là một ví dụ nhỏ về cách sử dụng lớp này:


.. tabs::

 .. code-tab:: gdscript

    # server_node.gd
    extends Node

    var dtls = DTLSServer.new()
    var server = UDPServer.new()
    var peers = []

    func _ready():
        server.listen(4242)
        var key = load("key.key") # Private key của bạn.
        var cert = load("cert.crt") # Chứng chỉ X509 của bạn.
        dtls.setup(TlsOptions.server(key, cert))

    func _process(delta):
        while server.is_connection_available():
            var peer = server.take_connection()
            var dtls_peer = dtls.take_connection(peer)
            if dtls_peer.get_status() != PacketPeerDTLS.STATUS_HANDSHAKING:
                continue # Việc 50% kết nối không thành công do quá trình trao đổi cookie là điều bình thường.
            print("Peer connected!")
            peers.append(dtls_peer)

        for p in peers:
            p.poll() # Phải gọi poll để cập nhật trạng thái.
            if p.get_status() == PacketPeerDTLS.STATUS_CONNECTED:
                while p.get_available_packet_count() > 0:
                    print("Received message from client: %s" % p.get_packet().get_string_from_utf8())
                    p.put_packet("Hello DTLS client".to_utf8_buffer())

 .. code-tab:: csharp

    // ServerNode.cs
    using Godot;

    public partial class ServerNode : Node
    {
        private DtlsServer _dtls = new DtlsServer();
        private UdpServer _server = new UdpServer();
        private Godot.Collections.Array<PacketPeerDtls> _peers = [];

        public override void _Ready()
        {
            _server.Listen(4242);
            var key = GD.Load<CryptoKey>("key.key"); // Private key của bạn.
            var cert = GD.Load<X509Certificate>("cert.crt"); // Chứng chỉ X509 của bạn.
            _dtls.Setup(TlsOptions.Server(key, cert));
        }

        public override void _Process(double delta)
        {
            while (_server.IsConnectionAvailable())
            {
                PacketPeerUdp peer = _server.TakeConnection();
                PacketPeerDtls dtlsPeer = _dtls.TakeConnection(peer);
                if (dtlsPeer.GetStatus() != PacketPeerDtls.Status.Handshaking)
                {
                    continue; // Việc 50% kết nối không thành công do quá trình trao đổi cookie là điều bình thường.
                }
                GD.Print("Peer connected!");
                _peers.Add(dtlsPeer);
            }

            foreach (var p in _peers)
            {
                p.Poll(); // Phải gọi poll để cập nhật trạng thái.
                if (p.GetStatus() == PacketPeerDtls.Status.Connected)
                {
                    while (p.GetAvailablePacketCount() > 0)
                    {
                        GD.Print($"Received Message From Client: {p.GetPacket().GetStringFromUtf8()}");
                        p.PutPacket("Hello DTLS Client".ToUtf8Buffer());
                    }
                }
            }
        }
    }




.. tabs::

 .. code-tab:: gdscript

    # client_node.gd
    extends Node

    var dtls = PacketPeerDTLS.new()
    var udp = PacketPeerUDP.new()
    var connected = false

    func _ready():
        udp.connect_to_host("127.0.0.1", 4242)
        dtls.connect_to_peer(udp, false) # Hãy dùng true trong môi trường production để xác thực chứng chỉ!

    func _process(delta):
        dtls.poll()
        if dtls.get_status() == PacketPeerDTLS.STATUS_CONNECTED:
            if !connected:
                # Thử liên hệ với máy chủ
                dtls.put_packet("The answer is... 42!".to_utf8_buffer())
            while dtls.get_available_packet_count() > 0:
                print("Connected: %s" % dtls.get_packet().get_string_from_utf8())
                connected = true

 .. code-tab:: csharp

    // ClientNode.cs
    using Godot;
    using System.Text;

    public partial class ClientNode : Node
    {
        private PacketPeerDtls _dtls = new PacketPeerDtls();
        private PacketPeerUdp _udp = new PacketPeerUdp();
        private bool _connected = false;

        public override void _Ready()
        {
            _udp.ConnectToHost("127.0.0.1", 4242);
            _dtls.ConnectToPeer(_udp, validateCerts: false); // Hãy dùng true trong môi trường production để xác thực chứng chỉ!
        }

        public override void _Process(double delta)
        {
            _dtls.Poll();
            if (_dtls.GetStatus() == PacketPeerDtls.Status.Connected)
            {
                if (!_connected)
                {
                    // Thử liên hệ với máy chủ
                    _dtls.PutPacket("The Answer Is..42!".ToUtf8Buffer());
                }
                while (_dtls.GetAvailablePacketCount() > 0)
                {
                    GD.Print($"Connected: {_dtls.GetPacket().GetStringFromUtf8()}");
                    _connected = true;
                }
            }
        }
    }



.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`       | :ref:`setup<class_DTLSServer_method_setup>`\ (\ server_options\: :ref:`TLSOptions<class_TLSOptions>`\ )                     |
   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PacketPeerDTLS<class_PacketPeerDTLS>` | :ref:`take_connection<class_DTLSServer_method_take_connection>`\ (\ udp_peer\: :ref:`PacketPeerUDP<class_PacketPeerUDP>`\ ) |
   +---------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_DTLSServer_method_setup:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **setup**\ (\ server_options\: :ref:`TLSOptions<class_TLSOptions>`\ ) :ref:`🔗<class_DTLSServer_method_setup>`

Thiết lập máy chủ DTLS để sử dụng ``server_options`` đã cho. Xem :ref:`TLSOptions.server()<class_TLSOptions_method_server>`.

.. rst-class:: classref-item-separator

----

.. _class_DTLSServer_method_take_connection:

.. rst-class:: classref-method

:ref:`PacketPeerDTLS<class_PacketPeerDTLS>` **take_connection**\ (\ udp_peer\: :ref:`PacketPeerUDP<class_PacketPeerUDP>`\ ) :ref:`🔗<class_DTLSServer_method_take_connection>`

Thử khởi tạo quá trình bắt tay DTLS với ``udp_peer`` đã cho; đối tượng này phải được kết nối trước (xem :ref:`PacketPeerUDP.connect_to_host()<class_PacketPeerUDP_method_connect_to_host>`).

\ **Lưu ý:** Bạn phải kiểm tra trạng thái của PacketPeerUDP được trả về là :ref:`PacketPeerDTLS.STATUS_HANDSHAKING<class_PacketPeerDTLS_constant_STATUS_HANDSHAKING>`, vì việc 50% kết nối mới không hợp lệ do quá trình trao đổi cookie là điều bình thường.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
