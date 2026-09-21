:github_url: hide

.. meta::
	:keywords: network

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MultiplayerAPI.xml.

.. _class_MultiplayerAPI:

MultiplayerAPI
==============

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`MultiplayerAPIExtension<class_MultiplayerAPIExtension>`, :ref:`SceneMultiplayer<class_SceneMultiplayer>`

Interface API multiplayer cấp cao.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho các triển khai API multiplayer cấp cao. Xem thêm :ref:`MultiplayerPeer<class_MultiplayerPeer>`.

Theo mặc định, :ref:`SceneTree<class_SceneTree>` tham chiếu đến một triển khai của lớp này và sử dụng nó để cung cấp các khả năng multiplayer (tức là RPC) trên toàn bộ scene.

Có thể ghi đè instance MultiplayerAPI được các nhánh cụ thể của tree sử dụng bằng cách gọi phương thức :ref:`SceneTree.set_multiplayer()<class_SceneTree_method_set_multiplayer>`, qua đó cho phép chạy cả client và server trong cùng một scene.

Cũng có thể mở rộng hoặc thay thế triển khai mặc định bằng scripting hoặc native extension. Xem :ref:`MultiplayerAPIExtension<class_MultiplayerAPIExtension>` để biết chi tiết về extension, và :ref:`SceneMultiplayer<class_SceneMultiplayer>` để biết chi tiết về triển khai mặc định.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------+-------------------------------------------------------------------------+
   | :ref:`MultiplayerPeer<class_MultiplayerPeer>` | :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` |
   +-----------------------------------------------+-------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MultiplayerAPI<class_MultiplayerAPI>`     | :ref:`create_default_interface<class_MultiplayerAPI_method_create_default_interface>`\ (\ ) |static|                                                                                                            |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`             | :ref:`get_default_interface<class_MultiplayerAPI_method_get_default_interface>`\ (\ ) |static|                                                                                                                  |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`get_peers<class_MultiplayerAPI_method_get_peers>`\ (\ )                                                                                                                                                   |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_remote_sender_id<class_MultiplayerAPI_method_get_remote_sender_id>`\ (\ )                                                                                                                             |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`get_unique_id<class_MultiplayerAPI_method_get_unique_id>`\ (\ )                                                                                                                                           |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`has_multiplayer_peer<class_MultiplayerAPI_method_has_multiplayer_peer>`\ (\ )                                                                                                                             |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_server<class_MultiplayerAPI_method_is_server>`\ (\ )                                                                                                                                                   |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`object_configuration_add<class_MultiplayerAPI_method_object_configuration_add>`\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ )                                |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`object_configuration_remove<class_MultiplayerAPI_method_object_configuration_remove>`\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ )                          |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`poll<class_MultiplayerAPI_method_poll>`\ (\ )                                                                                                                                                             |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`rpc<class_MultiplayerAPI_method_rpc>`\ (\ peer\: :ref:`int<class_int>`, object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, arguments\: :ref:`Array<class_Array>` = []\ ) |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_default_interface<class_MultiplayerAPI_method_set_default_interface>`\ (\ interface_name\: :ref:`StringName<class_StringName>`\ ) |static|                                                            |
   +-------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_MultiplayerAPI_signal_connected_to_server:

.. rst-class:: classref-signal

**connected_to_server**\ (\ ) :ref:`🔗<class_MultiplayerAPI_signal_connected_to_server>`

Được phát ra khi :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này kết nối thành công đến một server. Chỉ được phát ra trên client.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_signal_connection_failed:

.. rst-class:: classref-signal

**connection_failed**\ (\ ) :ref:`🔗<class_MultiplayerAPI_signal_connection_failed>`

Được phát ra khi :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này không thể thiết lập kết nối đến một server. Chỉ được phát ra trên client.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_signal_peer_connected:

.. rst-class:: classref-signal

**peer_connected**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiplayerAPI_signal_peer_connected>`

Được phát ra khi :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này kết nối với một peer mới. ID là peer ID của peer mới. Client sẽ được thông báo khi các client khác kết nối đến cùng một server. Khi kết nối đến một server, client cũng nhận được signal này cho server (với ID là 1).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_signal_peer_disconnected:

.. rst-class:: classref-signal

**peer_disconnected**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiplayerAPI_signal_peer_disconnected>`

Được phát ra khi :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này ngắt kết nối khỏi một peer. Client sẽ được thông báo khi các client khác ngắt kết nối khỏi cùng một server.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_signal_server_disconnected:

.. rst-class:: classref-signal

**server_disconnected**\ (\ ) :ref:`🔗<class_MultiplayerAPI_signal_server_disconnected>`

Được phát ra khi :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này ngắt kết nối khỏi server. Chỉ được phát ra trên client.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_MultiplayerAPI_RPCMode:

.. rst-class:: classref-enumeration

enum **RPCMode**: :ref:`🔗<enum_MultiplayerAPI_RPCMode>`

.. _class_MultiplayerAPI_constant_RPC_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`RPCMode<enum_MultiplayerAPI_RPCMode>` **RPC_MODE_DISABLED** = ``0``

Được sử dụng với :ref:`Node.rpc_config()<class_Node_method_rpc_config>` để vô hiệu hóa một method hoặc property cho tất cả các lời gọi RPC, khiến nó không khả dụng. Đây là giá trị mặc định cho tất cả method.

.. _class_MultiplayerAPI_constant_RPC_MODE_ANY_PEER:

.. rst-class:: classref-enumeration-constant

:ref:`RPCMode<enum_MultiplayerAPI_RPCMode>` **RPC_MODE_ANY_PEER** = ``1``

Được sử dụng với :ref:`Node.rpc_config()<class_Node_method_rpc_config>` để đặt một method có thể được gọi từ xa bởi bất kỳ peer nào. Tương tự annotation ``@rpc("any_peer")``. Lời gọi được chấp nhận từ tất cả peer từ xa, bất kể chúng có phải là authority của node hay không.

.. _class_MultiplayerAPI_constant_RPC_MODE_AUTHORITY:

.. rst-class:: classref-enumeration-constant

:ref:`RPCMode<enum_MultiplayerAPI_RPCMode>` **RPC_MODE_AUTHORITY** = ``2``

Được sử dụng với :ref:`Node.rpc_config()<class_Node_method_rpc_config>` để đặt một method chỉ có thể được gọi từ xa bởi multiplayer authority hiện tại (theo mặc định là server). Tương tự annotation ``@rpc("authority")``. Xem :ref:`Node.set_multiplayer_authority()<class_Node_method_set_multiplayer_authority>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiplayerAPI_property_multiplayer_peer:

.. rst-class:: classref-property

:ref:`MultiplayerPeer<class_MultiplayerPeer>` **multiplayer_peer** :ref:`🔗<class_MultiplayerAPI_property_multiplayer_peer>`

.. rst-class:: classref-property-setget

- |void| **set_multiplayer_peer**\ (\ value\: :ref:`MultiplayerPeer<class_MultiplayerPeer>`\ ) - :ref:`MultiplayerPeer<class_MultiplayerPeer>` **get_multiplayer_peer**\ (\ )

Đối tượng peer dùng để xử lý hệ thống RPC (bật networking khi được thiết lập). Tùy thuộc vào chính peer đó, MultiplayerAPI sẽ trở thành một network server (kiểm tra bằng :ref:`is_server()<class_MultiplayerAPI_method_is_server>`) và đặt network mode của root node thành authority, hoặc sẽ trở thành một client peer thông thường. Theo mặc định, tất cả child node được đặt để kế thừa network mode. Việc xử lý các sự kiện liên quan đến networking (kết nối, ngắt kết nối, client mới) được thực hiện bằng cách kết nối tới các signal của MultiplayerAPI.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiplayerAPI_method_create_default_interface:

.. rst-class:: classref-method

:ref:`MultiplayerAPI<class_MultiplayerAPI>` **create_default_interface**\ (\ ) |static| :ref:`🔗<class_MultiplayerAPI_method_create_default_interface>`

Trả về một instance mới của MultiplayerAPI mặc định.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_get_default_interface:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_default_interface**\ (\ ) |static| :ref:`🔗<class_MultiplayerAPI_method_get_default_interface>`

Trả về tên lớp triển khai MultiplayerAPI mặc định. Tên này thường là ``"SceneMultiplayer"`` khi :ref:`SceneMultiplayer<class_SceneMultiplayer>` khả dụng. Xem :ref:`set_default_interface()<class_MultiplayerAPI_method_set_default_interface>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_get_peers:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_peers**\ (\ ) :ref:`🔗<class_MultiplayerAPI_method_get_peers>`

Trả về peer ID của tất cả peer đã kết nối với :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_get_remote_sender_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_remote_sender_id**\ (\ ) :ref:`🔗<class_MultiplayerAPI_method_get_remote_sender_id>`

Trả về peer ID của sender cho RPC hiện đang được thực thi.

\ **Lưu ý:** Phương thức này trả về ``0`` khi được gọi bên ngoài một RPC. Do đó, peer ID ban đầu có thể bị mất khi việc thực thi code bị trì hoãn (chẳng hạn với keyword ``await`` của GDScript).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_get_unique_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_unique_id**\ (\ ) :ref:`🔗<class_MultiplayerAPI_method_get_unique_id>`

Trả về peer ID duy nhất của :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_has_multiplayer_peer:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_multiplayer_peer**\ (\ ) :ref:`🔗<class_MultiplayerAPI_method_has_multiplayer_peer>`

Trả về ``true`` nếu đã thiết lập một :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_is_server:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_server**\ (\ ) :ref:`🔗<class_MultiplayerAPI_method_is_server>`

Trả về ``true`` nếu :ref:`multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` của MultiplayerAPI này hợp lệ và đang ở chế độ server (lắng nghe các kết nối).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_object_configuration_add:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **object_configuration_add**\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_MultiplayerAPI_method_object_configuration_add>`

Thông báo cho MultiplayerAPI về một ``configuration`` mới cho ``object`` đã cho. Phương thức này được :ref:`SceneTree<class_SceneTree>` sử dụng nội bộ để cấu hình root path cho MultiplayerAPI này (truyền ``null`` và một :ref:`NodePath<class_NodePath>` hợp lệ dưới dạng ``configuration``). Các triển khai MultiplayerAPI cũng có thể sử dụng thêm phương thức này để cung cấp các tính năng bổ sung; hãy tham khảo triển khai cụ thể (ví dụ: :ref:`SceneMultiplayer<class_SceneMultiplayer>`) để biết chi tiết về cách chúng sử dụng phương thức này.

\ **Lưu ý:** Phương thức này chủ yếu liên quan khi mở rộng hoặc ghi đè hành vi của MultiplayerAPI thông qua :ref:`MultiplayerAPIExtension<class_MultiplayerAPIExtension>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_object_configuration_remove:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **object_configuration_remove**\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_MultiplayerAPI_method_object_configuration_remove>`

Thông báo cho MultiplayerAPI xóa một ``configuration`` khỏi ``object`` đã cho. Phương thức này được :ref:`SceneTree<class_SceneTree>` sử dụng nội bộ để cấu hình root path cho MultiplayerAPI này (truyền ``null`` và một :ref:`NodePath<class_NodePath>` rỗng dưới dạng ``configuration``). Các triển khai MultiplayerAPI cũng có thể sử dụng thêm phương thức này để cung cấp các tính năng bổ sung; hãy tham khảo triển khai cụ thể (ví dụ: :ref:`SceneMultiplayer<class_SceneMultiplayer>`) để biết chi tiết về cách chúng sử dụng phương thức này.

\ **Lưu ý:** Phương thức này chủ yếu liên quan khi mở rộng hoặc ghi đè hành vi của MultiplayerAPI thông qua :ref:`MultiplayerAPIExtension<class_MultiplayerAPIExtension>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_poll:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **poll**\ (\ ) :ref:`🔗<class_MultiplayerAPI_method_poll>`

Phương thức dùng để polling MultiplayerAPI. Bạn chỉ cần quan tâm đến phương thức này nếu đặt :ref:`SceneTree.multiplayer_poll<class_SceneTree_property_multiplayer_poll>` thành ``false``. Theo mặc định, :ref:`SceneTree<class_SceneTree>` sẽ polling các MultiplayerAPI của bạn.

\ **Lưu ý:** Phương thức này khiến các RPC được gọi, vì vậy chúng sẽ được thực thi trong cùng context với hàm này (ví dụ: ``_process``, ``physics``, :ref:`Thread<class_Thread>`).

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_rpc:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **rpc**\ (\ peer\: :ref:`int<class_int>`, object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, arguments\: :ref:`Array<class_Array>` = []\ ) :ref:`🔗<class_MultiplayerAPI_method_rpc>`

Gửi một RPC đến ``peer`` đích. ``method`` đã cho sẽ được gọi trên ``object`` từ xa với ``arguments`` được cung cấp. RPC cũng có thể được gọi cục bộ tùy thuộc vào triển khai và cấu hình RPC. Xem :ref:`Node.rpc()<class_Node_method_rpc>` và :ref:`Node.rpc_config()<class_Node_method_rpc_config>`.

\ **Lưu ý:** Nên ưu tiên sử dụng :ref:`Node.rpc()<class_Node_method_rpc>`, :ref:`Node.rpc_id()<class_Node_method_rpc_id>` hoặc ``my_method.rpc(peer, arg1, arg2, ...)`` (trong GDScript) vì chúng nhanh hơn. Phương thức này chủ yếu hữu ích khi kết hợp với :ref:`MultiplayerAPIExtension<class_MultiplayerAPIExtension>` trong quá trình mở rộng hoặc thay thế các khả năng multiplayer.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPI_method_set_default_interface:

.. rst-class:: classref-method

|void| **set_default_interface**\ (\ interface_name\: :ref:`StringName<class_StringName>`\ ) |static| :ref:`🔗<class_MultiplayerAPI_method_set_default_interface>`

Đặt lớp triển khai MultiplayerAPI mặc định. Các module và extension có thể sử dụng phương thức này để cấu hình triển khai nào sẽ được :ref:`SceneTree<class_SceneTree>` sử dụng khi engine khởi động.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
