:github_url: hide

.. meta::
	:keywords: network

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/multiplayer/doc_classes/MultiplayerSynchronizer.xml.

.. _class_MultiplayerSynchronizer:

MultiplayerSynchronizer
=======================

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Đồng bộ hóa các thuộc tính từ authority của multiplayer đến các peer từ xa.

.. rst-class:: classref-introduction-group

Mô tả
-----

Theo mặc định, **MultiplayerSynchronizer** đồng bộ hóa các thuộc tính đã cấu hình đến tất cả peer.

Tính khả kiến có thể được xử lý trực tiếp bằng :ref:`set_visibility_for()<class_MultiplayerSynchronizer_method_set_visibility_for>` hoặc khi cần bằng :ref:`add_visibility_filter()<class_MultiplayerSynchronizer_method_add_visibility_filter>` và :ref:`update_visibility()<class_MultiplayerSynchronizer_method_update_visibility>`.

\ :ref:`MultiplayerSpawner<class_MultiplayerSpawner>`\ sẽ xử lý các node theo tính khả kiến của các synchronizer, miễn là node tại :ref:`root_path<class_MultiplayerSynchronizer_property_root_path>` được một synchronizer tạo ra.

Về bên trong, **MultiplayerSynchronizer** sử dụng :ref:`MultiplayerAPI.object_configuration_add()<class_MultiplayerAPI_method_object_configuration_add>` để thông báo bắt đầu đồng bộ hóa, truyền :ref:`Node<class_Node>` tại :ref:`root_path<class_MultiplayerSynchronizer_property_root_path>` làm ``object`` và chính nó làm ``configuration``, đồng thời sử dụng :ref:`MultiplayerAPI.object_configuration_remove()<class_MultiplayerAPI_method_object_configuration_remove>` để thông báo kết thúc đồng bộ hóa theo cách tương tự.

\ **Lưu ý:** Không hỗ trợ đồng bộ hóa các thuộc tính thuộc kiểu :ref:`Object<class_Object>`, chẳng hạn như :ref:`Resource<class_Resource>`. Các thuộc tính riêng biệt với từng peer, chẳng hạn như instance ID của :ref:`Object<class_Object>`\ s (xem :ref:`Object.get_instance_id()<class_Object_method_get_instance_id>`) hoặc :ref:`RID<class_RID>`\ s, cũng sẽ không hoạt động khi đồng bộ hóa.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+
   | :ref:`float<class_float>`                                                      | :ref:`delta_interval<class_MultiplayerSynchronizer_property_delta_interval>`                 | ``0.0``            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`public_visibility<class_MultiplayerSynchronizer_property_public_visibility>`           | ``true``           |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+
   | :ref:`SceneReplicationConfig<class_SceneReplicationConfig>`                    | :ref:`replication_config<class_MultiplayerSynchronizer_property_replication_config>`         |                    |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+
   | :ref:`float<class_float>`                                                      | :ref:`replication_interval<class_MultiplayerSynchronizer_property_replication_interval>`     | ``0.0``            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+
   | :ref:`NodePath<class_NodePath>`                                                | :ref:`root_path<class_MultiplayerSynchronizer_property_root_path>`                           | ``NodePath("..")`` |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+
   | :ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>` | :ref:`visibility_update_mode<class_MultiplayerSynchronizer_property_visibility_update_mode>` | ``0``              |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+--------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`add_visibility_filter<class_MultiplayerSynchronizer_method_add_visibility_filter>`\ (\ filter\: :ref:`Callable<class_Callable>`\ )                  |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_visibility_for<class_MultiplayerSynchronizer_method_get_visibility_for>`\ (\ peer\: :ref:`int<class_int>`\ ) |const|                            |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`remove_visibility_filter<class_MultiplayerSynchronizer_method_remove_visibility_filter>`\ (\ filter\: :ref:`Callable<class_Callable>`\ )            |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_visibility_for<class_MultiplayerSynchronizer_method_set_visibility_for>`\ (\ peer\: :ref:`int<class_int>`, visible\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`update_visibility<class_MultiplayerSynchronizer_method_update_visibility>`\ (\ for_peer\: :ref:`int<class_int>` = 0\ )                              |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_MultiplayerSynchronizer_signal_delta_synchronized:

.. rst-class:: classref-signal

**delta_synchronized**\ (\ ) :ref:`🔗<class_MultiplayerSynchronizer_signal_delta_synchronized>`

Được phát ra khi synchronizer này nhận được trạng thái đồng bộ hóa delta mới sau khi các thuộc tính đã được cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_signal_synchronized:

.. rst-class:: classref-signal

**synchronized**\ (\ ) :ref:`🔗<class_MultiplayerSynchronizer_signal_synchronized>`

Được phát ra khi synchronizer này nhận được trạng thái đồng bộ hóa mới sau khi các thuộc tính đã được cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_signal_visibility_changed:

.. rst-class:: classref-signal

**visibility_changed**\ (\ for_peer\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiplayerSynchronizer_signal_visibility_changed>`

Được phát ra khi tính khả kiến của ``for_peer`` được cập nhật. Xem :ref:`update_visibility()<class_MultiplayerSynchronizer_method_update_visibility>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_MultiplayerSynchronizer_VisibilityUpdateMode:

.. rst-class:: classref-enumeration

enum **VisibilityUpdateMode**: :ref:`🔗<enum_MultiplayerSynchronizer_VisibilityUpdateMode>`

.. _class_MultiplayerSynchronizer_constant_VISIBILITY_PROCESS_IDLE:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>` **VISIBILITY_PROCESS_IDLE** = ``0``

Các bộ lọc tính khả kiến được cập nhật trong các frame process (xem :ref:`Node.NOTIFICATION_INTERNAL_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PROCESS>`).

.. _class_MultiplayerSynchronizer_constant_VISIBILITY_PROCESS_PHYSICS:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>` **VISIBILITY_PROCESS_PHYSICS** = ``1``

Các bộ lọc tính khả kiến được cập nhật trong các frame physics (xem :ref:`Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS>`).

.. _class_MultiplayerSynchronizer_constant_VISIBILITY_PROCESS_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>` **VISIBILITY_PROCESS_NONE** = ``2``

Các bộ lọc tính khả kiến không được tự động cập nhật và phải được cập nhật thủ công bằng cách gọi :ref:`update_visibility()<class_MultiplayerSynchronizer_method_update_visibility>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiplayerSynchronizer_property_delta_interval:

.. rst-class:: classref-property

:ref:`float<class_float>` **delta_interval** = ``0.0`` :ref:`🔗<class_MultiplayerSynchronizer_property_delta_interval>`

.. rst-class:: classref-property-setget

- |void| **set_delta_interval**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_delta_interval**\ (\ )

Khoảng thời gian giữa các lần đồng bộ hóa delta. Được sử dụng khi replication được đặt thành :ref:`SceneReplicationConfig.REPLICATION_MODE_ON_CHANGE<class_SceneReplicationConfig_constant_REPLICATION_MODE_ON_CHANGE>`. Nếu được đặt thành ``0.0`` (mặc định), đồng bộ hóa delta sẽ diễn ra ở mỗi network process frame.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_property_public_visibility:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **public_visibility** = ``true`` :ref:`🔗<class_MultiplayerSynchronizer_property_public_visibility>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_public**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_visibility_public**\ (\ )

Cho biết theo mặc định việc đồng bộ hóa có nên hiển thị với tất cả peer hay không. Xem :ref:`set_visibility_for()<class_MultiplayerSynchronizer_method_set_visibility_for>` và :ref:`add_visibility_filter()<class_MultiplayerSynchronizer_method_add_visibility_filter>` để biết các cách cấu hình tùy chọn khả kiến chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_property_replication_config:

.. rst-class:: classref-property

:ref:`SceneReplicationConfig<class_SceneReplicationConfig>` **replication_config** :ref:`🔗<class_MultiplayerSynchronizer_property_replication_config>`

.. rst-class:: classref-property-setget

- |void| **set_replication_config**\ (\ value\: :ref:`SceneReplicationConfig<class_SceneReplicationConfig>`\ ) - :ref:`SceneReplicationConfig<class_SceneReplicationConfig>` **get_replication_config**\ (\ )

Resource chứa các thuộc tính cần đồng bộ hóa.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_property_replication_interval:

.. rst-class:: classref-property

:ref:`float<class_float>` **replication_interval** = ``0.0`` :ref:`🔗<class_MultiplayerSynchronizer_property_replication_interval>`

.. rst-class:: classref-property-setget

- |void| **set_replication_interval**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_replication_interval**\ (\ )

Khoảng thời gian giữa các lần đồng bộ hóa. Được sử dụng khi replication được đặt thành :ref:`SceneReplicationConfig.REPLICATION_MODE_ALWAYS<class_SceneReplicationConfig_constant_REPLICATION_MODE_ALWAYS>`. Nếu được đặt thành ``0.0`` (mặc định), đồng bộ hóa sẽ diễn ra ở mỗi network process frame.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_property_root_path:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **root_path** = ``NodePath("..")`` :ref:`🔗<class_MultiplayerSynchronizer_property_root_path>`

.. rst-class:: classref-property-setget

- |void| **set_root_path**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_root_path**\ (\ )

Đường dẫn node mà các thuộc tính được replicated được tham chiếu tương đối đến.

Nếu :ref:`root_path<class_MultiplayerSynchronizer_property_root_path>` được spawn bởi một :ref:`MultiplayerSpawner<class_MultiplayerSpawner>`, node cũng sẽ được spawn và despawn dựa trên các tùy chọn khả kiến của synchronizer này.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_property_visibility_update_mode:

.. rst-class:: classref-property

:ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>` **visibility_update_mode** = ``0`` :ref:`🔗<class_MultiplayerSynchronizer_property_visibility_update_mode>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_update_mode**\ (\ value\: :ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>`\ ) - :ref:`VisibilityUpdateMode<enum_MultiplayerSynchronizer_VisibilityUpdateMode>` **get_visibility_update_mode**\ (\ )

Xác định thời điểm cập nhật các bộ lọc tính khả kiến.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiplayerSynchronizer_method_add_visibility_filter:

.. rst-class:: classref-method

|void| **add_visibility_filter**\ (\ filter\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_MultiplayerSynchronizer_method_add_visibility_filter>`

Thêm một bộ lọc khả kiến peer cho synchronizer này.

\ ``filter`` phải nhận một peer ID :ref:`int<class_int>` và trả về một :ref:`bool<class_bool>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_method_get_visibility_for:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_visibility_for**\ (\ peer\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MultiplayerSynchronizer_method_get_visibility_for>`

Truy vấn tính khả kiến hiện tại đối với peer ``peer``.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_method_remove_visibility_filter:

.. rst-class:: classref-method

|void| **remove_visibility_filter**\ (\ filter\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_MultiplayerSynchronizer_method_remove_visibility_filter>`

Xóa một bộ lọc khả kiến peer khỏi synchronizer này.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_method_set_visibility_for:

.. rst-class:: classref-method

|void| **set_visibility_for**\ (\ peer\: :ref:`int<class_int>`, visible\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_MultiplayerSynchronizer_method_set_visibility_for>`

Đặt tính khả kiến của ``peer`` thành ``visible``. Nếu ``peer`` là ``0``, giá trị của :ref:`public_visibility<class_MultiplayerSynchronizer_property_public_visibility>` sẽ được cập nhật thay thế.

.. rst-class:: classref-item-separator

----

.. _class_MultiplayerSynchronizer_method_update_visibility:

.. rst-class:: classref-method

|void| **update_visibility**\ (\ for_peer\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_MultiplayerSynchronizer_method_update_visibility>`

Cập nhật tính khả kiến của ``for_peer`` theo các bộ lọc khả kiến. Nếu ``for_peer`` là ``0`` (mặc định), tính khả kiến của tất cả peer sẽ được cập nhật.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
