:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/multiplayer/doc_classes/OfflineMultiplayerPeer.xml.

.. _class_OfflineMultiplayerPeer:

OfflineMultiplayerPeer
======================

**Kế thừa:** :ref:`MultiplayerPeer<class_MultiplayerPeer>` **<** :ref:`PacketPeer<class_PacketPeer>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`MultiplayerPeer<class_MultiplayerPeer>` luôn được kết nối và hoạt động như một server.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đây là :ref:`MultiplayerAPI.multiplayer_peer<class_MultiplayerAPI_property_multiplayer_peer>` mặc định cho :ref:`Node.multiplayer<class_Node_property_multiplayer>`. Nó mô phỏng hành vi của một server không có peer nào được kết nối.

Điều này có nghĩa là :ref:`SceneTree<class_SceneTree>` sẽ mặc định hoạt động như authority của multiplayer. Các lệnh gọi đến :ref:`MultiplayerAPI.is_server()<class_MultiplayerAPI_method_is_server>` sẽ trả về ``true``, và các lệnh gọi đến :ref:`MultiplayerAPI.get_unique_id()<class_MultiplayerAPI_method_get_unique_id>` sẽ trả về :ref:`MultiplayerPeer.TARGET_PEER_SERVER<class_MultiplayerPeer_constant_TARGET_PEER_SERVER>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
