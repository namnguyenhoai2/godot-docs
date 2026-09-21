:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/enet/doc_classes/ENetMultiplayerPeer.xml.

.. _class_ENetMultiplayerPeer:

ENetMultiplayerPeer
===================

**Kế thừa:** :ref:`MultiplayerPeer<class_MultiplayerPeer>` **<** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một implementation của MultiplayerPeer sử dụng thư viện `ENet <http://enet.bespin.org/index.html>`__.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một implementation của MultiplayerPeer cần được truyền vào :ref:`MultiplayerAPI.multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` sau khi được khởi tạo dưới dạng client, server hoặc mesh. Sau đó, các sự kiện có thể được xử lý bằng cách kết nối với các signal :ref:`MultiplayerAPI<class_MultiplayerAPI>`. Xem :ref:`ENetConnection<class_ENetConnection>` để biết thêm thông tin về lớp bao bọc thư viện ENet.

\ **Lưu ý:** ENet chỉ sử dụng UDP, không sử dụng TCP. Khi chuyển tiếp port của server để server có thể truy cập trên Internet công cộng, bạn chỉ cần chuyển tiếp port của server qua UDP. Bạn có thể sử dụng class :ref:`UPNP<class_UPNP>` để thử tự động chuyển tiếp port của server khi khởi động server.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Multiplayer cấp cao <../tutorials/networking/high_level_multiplayer>`

- `API documentation on the ENet website <http://enet.bespin.org/usergroup0.html>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------+------------------------------------------------------+
   | :ref:`ENetConnection<class_ENetConnection>` | :ref:`host<class_ENetMultiplayerPeer_property_host>` |
   +---------------------------------------------+------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`       | :ref:`add_mesh_peer<class_ENetMultiplayerPeer_method_add_mesh_peer>`\ (\ peer_id\: :ref:`int<class_int>`, host\: :ref:`ENetConnection<class_ENetConnection>`\ )                                                                                                                                                         |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`       | :ref:`create_client<class_ENetMultiplayerPeer_method_create_client>`\ (\ address\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`, channel_count\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0, local_port\: :ref:`int<class_int>` = 0\ ) |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`       | :ref:`create_mesh<class_ENetMultiplayerPeer_method_create_mesh>`\ (\ unique_id\: :ref:`int<class_int>`\ )                                                                                                                                                                                                               |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`       | :ref:`create_server<class_ENetMultiplayerPeer_method_create_server>`\ (\ port\: :ref:`int<class_int>`, max_clients\: :ref:`int<class_int>` = 32, max_channels\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ )                                       |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ENetPacketPeer<class_ENetPacketPeer>` | :ref:`get_peer<class_ENetMultiplayerPeer_method_get_peer>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                                                    |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                      | :ref:`set_bind_ip<class_ENetMultiplayerPeer_method_set_bind_ip>`\ (\ ip\: :ref:`String<class_String>`\ )                                                                                                                                                                                                                |
   +---------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ENetMultiplayerPeer_property_host:

.. rst-class:: classref-property

:ref:`ENetConnection<class_ENetConnection>` **host** :ref:`🔗<class_ENetMultiplayerPeer_property_host>`

.. rst-class:: classref-property-setget

- :ref:`ENetConnection<class_ENetConnection>` **get_host**\ (\ )

:ref:`ENetConnection<class_ENetConnection>` nền tảng được tạo sau :ref:`create_client()<class_ENetMultiplayerPeer_method_create_client>` và :ref:`create_server()<class_ENetMultiplayerPeer_method_create_server>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ENetMultiplayerPeer_method_add_mesh_peer:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **add_mesh_peer**\ (\ peer_id\: :ref:`int<class_int>`, host\: :ref:`ENetConnection<class_ENetConnection>`\ ) :ref:`🔗<class_ENetMultiplayerPeer_method_add_mesh_peer>`

Thêm một peer từ xa mới với ``peer_id`` đã cho được kết nối đến ``host`` đã cho.

\ **Lưu ý:** ``host`` phải có chính xác một peer ở trạng thái :ref:`ENetPacketPeer.STATE_CONNECTED<class_ENetPacketPeer_constant_STATE_CONNECTED>`.

.. rst-class:: classref-item-separator

----

.. _class_ENetMultiplayerPeer_method_create_client:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_client**\ (\ address\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`, channel_count\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0, local_port\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetMultiplayerPeer_method_create_client>`

Tạo client kết nối đến server tại ``address`` bằng ``port`` đã chỉ định. Địa chỉ đã cho cần là tên miền đầy đủ (ví dụ: ``"www.example.com"``) hoặc địa chỉ IP ở định dạng IPv4 hoặc IPv6 (ví dụ: ``"192.168.1.1"``). ``port`` là port mà server đang lắng nghe. Tham số ``channel_count`` có thể được dùng để chỉ định số lượng kênh ENet được cấp phát cho kết nối. Các tham số ``in_bandwidth`` và ``out_bandwidth`` có thể được dùng để giới hạn băng thông đến và đi ở số byte mỗi giây đã cho. Giá trị mặc định 0 có nghĩa là băng thông không giới hạn. Lưu ý rằng ENet sẽ chủ động loại bỏ các packet ở những phía cụ thể của kết nối giữa các peer để bảo đảm băng thông của peer không bị quá tải. Các tham số băng thông cũng xác định kích thước cửa sổ của một kết nối, qua đó giới hạn số packet tin cậy có thể đang truyền tại bất kỳ thời điểm nào. Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu client được tạo, :ref:`@GlobalScope.ERR_ALREADY_IN_USE<class_@GlobalScope_constant_ERR_ALREADY_IN_USE>` nếu instance ENetMultiplayerPeer này đã có kết nối đang mở (trong trường hợp đó, trước tiên bạn cần gọi :ref:`MultiplayerPeer.close()<class_MultiplayerPeer_method_close>`) hoặc :ref:`@GlobalScope.ERR_CANT_CREATE<class_@GlobalScope_constant_ERR_CANT_CREATE>` nếu không thể tạo client. Nếu chỉ định ``local_port``, client cũng sẽ lắng nghe port đã cho; điều này hữu ích cho một số kỹ thuật NAT traversal.

.. rst-class:: classref-item-separator

----

.. _class_ENetMultiplayerPeer_method_create_mesh:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_mesh**\ (\ unique_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ENetMultiplayerPeer_method_create_mesh>`

Khởi tạo :ref:`MultiplayerPeer<class_MultiplayerPeer>` này ở chế độ mesh. ``unique_id`` được cung cấp sẽ được dùng làm ID duy nhất của peer mạng cục bộ sau khi được gán làm :ref:`MultiplayerAPI.multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>`. Trong cấu hình mesh, bạn cần thiết lập thủ công từng peer mới bằng :ref:`ENetConnection<class_ENetConnection>` trước khi gọi :ref:`add_mesh_peer()<class_ENetMultiplayerPeer_method_add_mesh_peer>`. Mặc dù kỹ thuật này nâng cao hơn, nó cho phép kiểm soát tốt hơn quy trình kết nối (ví dụ: khi xử lý NAT punch-through) và phân phối tải mạng tốt hơn (nếu không sẽ gây tải lớn hơn cho server).

.. rst-class:: classref-item-separator

----

.. _class_ENetMultiplayerPeer_method_create_server:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create_server**\ (\ port\: :ref:`int<class_int>`, max_clients\: :ref:`int<class_int>` = 32, max_channels\: :ref:`int<class_int>` = 0, in_bandwidth\: :ref:`int<class_int>` = 0, out_bandwidth\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_ENetMultiplayerPeer_method_create_server>`

Tạo server lắng nghe các kết nối thông qua ``port``. Port cần là một port khả dụng, chưa được sử dụng, có giá trị từ 0 đến 65535. Lưu ý rằng các port dưới 1024 là port đặc quyền và có thể yêu cầu quyền nâng cao tùy theo nền tảng. Để thay đổi interface mà server lắng nghe, hãy sử dụng :ref:`set_bind_ip()<class_ENetMultiplayerPeer_method_set_bind_ip>`. IP mặc định là wildcard ``"*"``, lắng nghe trên tất cả interface khả dụng. ``max_clients`` là số client tối đa được phép kết nối cùng lúc; có thể sử dụng bất kỳ số nào tối đa 4095, mặc dù số client đồng thời có thể đạt được trên thực tế thấp hơn nhiều và phụ thuộc vào ứng dụng. Để biết thêm chi tiết về các tham số băng thông, hãy xem :ref:`create_client()<class_ENetMultiplayerPeer_method_create_client>`. Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu server được tạo, :ref:`@GlobalScope.ERR_ALREADY_IN_USE<class_@GlobalScope_constant_ERR_ALREADY_IN_USE>` nếu instance ENetMultiplayerPeer này đã có kết nối đang mở (trong trường hợp đó, trước tiên bạn cần gọi :ref:`MultiplayerPeer.close()<class_MultiplayerPeer_method_close>`) hoặc :ref:`@GlobalScope.ERR_CANT_CREATE<class_@GlobalScope_constant_ERR_CANT_CREATE>` nếu không thể tạo server.

.. rst-class:: classref-item-separator

----

.. _class_ENetMultiplayerPeer_method_get_peer:

.. rst-class:: classref-method

:ref:`ENetPacketPeer<class_ENetPacketPeer>` **get_peer**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_ENetMultiplayerPeer_method_get_peer>`

Trả về :ref:`ENetPacketPeer<class_ENetPacketPeer>` được liên kết với ``id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_ENetMultiplayerPeer_method_set_bind_ip:

.. rst-class:: classref-method

|void| **set_bind_ip**\ (\ ip\: :ref:`String<class_String>`\ ) :ref:`🔗<class_ENetMultiplayerPeer_method_set_bind_ip>`

IP được sử dụng khi tạo server. Theo mặc định, giá trị này là wildcard ``"*"``, liên kết với tất cả interface khả dụng. IP đã cho cần ở định dạng địa chỉ IPv4 hoặc IPv6, ví dụ: ``"192.168.1.1"``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
