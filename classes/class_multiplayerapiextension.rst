:github_url: hide

.. meta::
	:keywords: network

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MultiplayerAPIExtension.xml.

.. _class_MultiplayerAPIExtension:

MultiplayerAPIExtension
=======================

**Kế thừa:** :ref:`MultiplayerAPI<class_MultiplayerAPI>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp cơ sở dùng để mở rộng :ref:`MultiplayerAPI<class_MultiplayerAPI>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Có thể sử dụng lớp này để mở rộng hoặc thay thế triển khai :ref:`MultiplayerAPI<class_MultiplayerAPI>` mặc định thông qua script hoặc extension.

Ví dụ sau mở rộng triển khai mặc định (:ref:`SceneMultiplayer<class_SceneMultiplayer>`) bằng cách ghi log mọi RPC được thực hiện và mọi object được cấu hình để replication.


.. tabs::

 .. code-tab:: gdscript

    extends MultiplayerAPIExtension
    class_name LogMultiplayer

    # Chúng ta muốn mở rộng SceneMultiplayer mặc định.
    var base_multiplayer = SceneMultiplayer.new()

    func _init():
        # Chỉ chuyển tiếp các signal cơ sở (được sao chép vào var để tránh tham chiếu vòng)
        var cts = connected_to_server
        var cf = connection_failed
        var sd = server_disconnected
        var pc = peer_connected
        var pd = peer_disconnected
        base_multiplayer.connected_to_server.connect(func(): cts.emit())
        base_multiplayer.connection_failed.connect(func(): cf.emit())
        base_multiplayer.server_disconnected.connect(func(): sd.emit())
        base_multiplayer.peer_connected.connect(func(id): pc.emit(id))
        base_multiplayer.peer_disconnected.connect(func(id): pd.emit(id))

    func _poll():
        return base_multiplayer.poll()

    # Ghi log RPC đang được thực hiện và chuyển tiếp nó đến multiplayer mặc định.
    func _rpc(peer: int, object: Object, method: StringName, args: Array) -> Error:
        print("Got RPC for %d: %s::%s(%s)" % [peer, object, method, args])
        return base_multiplayer.rpc(peer, object, method, args)

    # Ghi log việc thêm cấu hình. Ví dụ: root path (nullptr, NodePath), replication (Node, Spawner|Synchronizer), tùy chỉnh.
    func _object_configuration_add(object, config: Variant) -> Error:
        if config is MultiplayerSynchronizer:
            print("Adding synchronization configuration for %s. Synchronizer: %s" % [object, config])
        elif config is MultiplayerSpawner:
            print("Adding node %s to the spawn list. Spawner: %s" % [object, config])
        return base_multiplayer.object_configuration_add(object, config)

    # Ghi log việc xóa cấu hình. Ví dụ: root path (nullptr, NodePath), replication (Node, Spawner|Synchronizer), tùy chỉnh.
    func _object_configuration_remove(object, config: Variant) -> Error:
        if config is MultiplayerSynchronizer:
            print("Removing synchronization configuration for %s. Synchronizer: %s" % [object, config])
        elif config is MultiplayerSpawner:
            print("Removing node %s from the spawn list. Spawner: %s" % [object, config])
        return base_multiplayer.object_configuration_remove(object, config)

    # Các thành phần này có thể là tùy chọn, nhưng trong trường hợp của chúng ta, ta muốn mở rộng SceneMultiplayer, nên hãy chuyển tiếp mọi thứ.
    func _set_multiplayer_peer(p_peer: MultiplayerPeer):
        base_multiplayer.multiplayer_peer = p_peer

    func _get_multiplayer_peer() -> MultiplayerPeer:
        return base_multiplayer.multiplayer_peer

    func _get_unique_id() -> int:
        return base_multiplayer.get_unique_id()

    func _get_remote_sender_id() -> int:
        return base_multiplayer.get_remote_sender_id()

    func _get_peer_ids() -> PackedInt32Array:
        return base_multiplayer.get_peers()



Sau đó, trong main scene hoặc trong một autoload, hãy gọi :ref:`SceneTree.set_multiplayer()<class_SceneTree_method_set_multiplayer>` để bắt đầu sử dụng :ref:`MultiplayerAPI<class_MultiplayerAPI>` tùy chỉnh của bạn:


.. tabs::

 .. code-tab:: gdscript

    # autoload.gd
    func _enter_tree():
        # Đặt multiplayer tùy chỉnh của chúng ta làm multiplayer chính trong SceneTree.
        get_tree().set_multiplayer(LogMultiplayer.new())



Các native extension cũng có thể sử dụng phương thức :ref:`MultiplayerAPI.set_default_interface()<class_MultiplayerAPI_method_set_default_interface>` trong quá trình khởi tạo để tự cấu hình làm triển khai mặc định.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`MultiplayerPeer<class_MultiplayerPeer>`   | :ref:`_get_multiplayer_peer<class_MultiplayerAPIExtension_private_method__get_multiplayer_peer>`\ (\ ) |virtual|                                                                                                                   |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`_get_peer_ids<class_MultiplayerAPIExtension_private_method__get_peer_ids>`\ (\ ) |virtual| |const|                                                                                                                           |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`_get_remote_sender_id<class_MultiplayerAPIExtension_private_method__get_remote_sender_id>`\ (\ ) |virtual| |const|                                                                                                           |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`_get_unique_id<class_MultiplayerAPIExtension_private_method__get_unique_id>`\ (\ ) |virtual| |const|                                                                                                                         |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`_object_configuration_add<class_MultiplayerAPIExtension_private_method__object_configuration_add>`\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ ) |virtual|                      |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`_object_configuration_remove<class_MultiplayerAPIExtension_private_method__object_configuration_remove>`\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ ) |virtual|                |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`_poll<class_MultiplayerAPIExtension_private_method__poll>`\ (\ ) |virtual|                                                                                                                                                   |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`_rpc<class_MultiplayerAPIExtension_private_method__rpc>`\ (\ peer\: :ref:`int<class_int>`, object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, args\: :ref:`Array<class_Array>`\ ) |virtual| |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_set_multiplayer_peer<class_MultiplayerAPIExtension_private_method__set_multiplayer_peer>`\ (\ multiplayer_peer\: :ref:`MultiplayerPeer<class_MultiplayerPeer>`\ ) |virtual|                                                 |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiplayerAPIExtension_private_method__get_multiplayer_peer:

.. rst-class:: classref-method

:ref:`MultiplayerPeer<class_MultiplayerPeer>` **_get_multiplayer_peer**\ (\ ) |virtual| :ref:`🔗<class_MultiplayerAPIExtension_private_method__get_multiplayer_peer>`

Được gọi khi :ref:`MultiplayerAPI.multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` được lấy.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__get_peer_ids:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **_get_peer_ids**\ (\ ) |virtual| |const| :ref:`🔗<class_MultiplayerAPIExtension_private_method__get_peer_ids>`

Callback cho :ref:`MultiplayerAPI.get_peers()<class_MultiplayerAPI_method_get_peers>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__get_remote_sender_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_remote_sender_id**\ (\ ) |virtual| |const| :ref:`🔗<class_MultiplayerAPIExtension_private_method__get_remote_sender_id>`

Callback cho :ref:`MultiplayerAPI.get_remote_sender_id()<class_MultiplayerAPI_method_get_remote_sender_id>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__get_unique_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **_get_unique_id**\ (\ ) |virtual| |const| :ref:`🔗<class_MultiplayerAPIExtension_private_method__get_unique_id>`

Callback cho :ref:`MultiplayerAPI.get_unique_id()<class_MultiplayerAPI_method_get_unique_id>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__object_configuration_add:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_object_configuration_add**\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ ) |virtual| :ref:`🔗<class_MultiplayerAPIExtension_private_method__object_configuration_add>`

Callback cho :ref:`MultiplayerAPI.object_configuration_add()<class_MultiplayerAPI_method_object_configuration_add>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__object_configuration_remove:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_object_configuration_remove**\ (\ object\: :ref:`Object<class_Object>`, configuration\: :ref:`Variant<class_Variant>`\ ) |virtual| :ref:`🔗<class_MultiplayerAPIExtension_private_method__object_configuration_remove>`

Callback cho :ref:`MultiplayerAPI.object_configuration_remove()<class_MultiplayerAPI_method_object_configuration_remove>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__poll:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_poll**\ (\ ) |virtual| :ref:`🔗<class_MultiplayerAPIExtension_private_method__poll>`

Callback cho :ref:`MultiplayerAPI.poll()<class_MultiplayerAPI_method_poll>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__rpc:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_rpc**\ (\ peer\: :ref:`int<class_int>`, object\: :ref:`Object<class_Object>`, method\: :ref:`StringName<class_StringName>`, args\: :ref:`Array<class_Array>`\ ) |virtual| :ref:`🔗<class_MultiplayerAPIExtension_private_method__rpc>`

Callback cho :ref:`MultiplayerAPI.rpc()<class_MultiplayerAPI_method_rpc>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerAPIExtension_private_method__set_multiplayer_peer:

.. rst-class:: classref-method

|void| **_set_multiplayer_peer**\ (\ multiplayer_peer\: :ref:`MultiplayerPeer<class_MultiplayerPeer>`\ ) |virtual| :ref:`🔗<class_MultiplayerAPIExtension_private_method__set_multiplayer_peer>`

Được gọi khi :ref:`MultiplayerAPI.multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` được thiết lập.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
