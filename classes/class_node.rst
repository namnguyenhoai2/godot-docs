:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Node.xml.

.. _class_Node:

Node
====

**Kế thừa:** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AnimationMixer<class_AnimationMixer>`, :ref:`AudioStreamPlayer<class_AudioStreamPlayer>`, :ref:`CanvasItem<class_CanvasItem>`, :ref:`CanvasLayer<class_CanvasLayer>`, :ref:`EditorFileSystem<class_EditorFileSystem>`, :ref:`EditorPlugin<class_EditorPlugin>`, :ref:`EditorResourcePreview<class_EditorResourcePreview>`, :ref:`HTTPRequest<class_HTTPRequest>`, :ref:`InstancePlaceholder<class_InstancePlaceholder>`, :ref:`MissingNode<class_MissingNode>`, :ref:`MultiplayerSpawner<class_MultiplayerSpawner>`, :ref:`MultiplayerSynchronizer<class_MultiplayerSynchronizer>`, :ref:`NavigationAgent2D<class_NavigationAgent2D>`, :ref:`NavigationAgent3D<class_NavigationAgent3D>`, :ref:`Node3D<class_Node3D>`, :ref:`ResourcePreloader<class_ResourcePreloader>`, :ref:`ShaderGlobalsOverride<class_ShaderGlobalsOverride>`, :ref:`StatusIndicator<class_StatusIndicator>`, :ref:`Timer<class_Timer>`, :ref:`Viewport<class_Viewport>`, :ref:`WorldEnvironment<class_WorldEnvironment>`

Lớp cơ sở cho mọi đối tượng scene.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node là các khối xây dựng của Godot. Chúng có thể được gán làm node con của một node khác, tạo thành một cấu trúc dạng cây. Một node có thể chứa bất kỳ số lượng node con nào, với yêu cầu tất cả các node cùng cấp (node con trực tiếp của một node) phải có tên duy nhất.

Một cây các node được gọi là một *scene*. Scene có thể được lưu vào đĩa rồi khởi tạo vào các scene khác. Điều này mang lại tính linh hoạt rất cao cho kiến trúc và mô hình dữ liệu của các dự án Godot.

\ **Cây scene:** :ref:`SceneTree<class_SceneTree>` chứa cây node đang hoạt động. Khi một node được thêm vào cây scene, nó nhận thông báo :ref:`NOTIFICATION_ENTER_TREE<class_Node_constant_NOTIFICATION_ENTER_TREE>` và callback :ref:`_enter_tree()<class_Node_private_method__enter_tree>` của nó được kích hoạt. Các node con luôn được thêm *sau* node cha, tức là callback :ref:`_enter_tree()<class_Node_private_method__enter_tree>` của node cha sẽ được kích hoạt trước callback của node con.

Sau khi tất cả node đã được thêm vào cây scene, chúng nhận thông báo :ref:`NOTIFICATION_READY<class_Node_constant_NOTIFICATION_READY>` và các callback :ref:`_ready()<class_Node_private_method__ready>` tương ứng của chúng được kích hoạt. Đối với các nhóm node, callback :ref:`_ready()<class_Node_private_method__ready>` được gọi theo thứ tự ngược lại, bắt đầu từ các node con và đi lên các node cha.

Điều này có nghĩa là khi thêm một node vào cây scene, thứ tự sau đây sẽ được dùng cho các callback: :ref:`_enter_tree()<class_Node_private_method__enter_tree>` của node cha, :ref:`_enter_tree()<class_Node_private_method__enter_tree>` của các node con, :ref:`_ready()<class_Node_private_method__ready>` của các node con và cuối cùng là :ref:`_ready()<class_Node_private_method__ready>` của node cha (đệ quy cho toàn bộ cây scene).

\ **Xử lý:** Node có thể ghi đè trạng thái "process" để nhận callback ở mỗi frame, yêu cầu chúng thực hiện xử lý (làm một việc gì đó). Xử lý thông thường (callback :ref:`_process()<class_Node_private_method__process>`, được bật/tắt bằng :ref:`set_process()<class_Node_method_set_process>`) diễn ra nhanh nhất có thể và phụ thuộc vào frame rate, vì vậy thời gian xử lý *delta* (tính bằng giây) được truyền vào làm đối số. Xử lý vật lý (callback :ref:`_physics_process()<class_Node_private_method__physics_process>`, được bật/tắt bằng :ref:`set_physics_process()<class_Node_method_set_physics_process>`) diễn ra với số lần cố định mỗi giây (mặc định là 60) và hữu ích cho mã liên quan đến physics engine.

Node cũng có thể xử lý các input event. Khi có mặt, hàm :ref:`_input()<class_Node_private_method__input>` sẽ được gọi cho mỗi input mà chương trình nhận được. Trong nhiều trường hợp, cách này có thể là quá mức cần thiết (trừ khi dùng cho các dự án đơn giản), và hàm :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>` có thể được ưu tiên; hàm này được gọi khi input event chưa được đối tượng nào khác xử lý (thường là các node GUI :ref:`Control<class_Control>`), đảm bảo node chỉ nhận những event được dành cho nó.

Để theo dõi hệ phân cấp scene (đặc biệt khi khởi tạo scene vào các scene khác), có thể đặt một "owner" cho node bằng property :ref:`owner<class_Node_property_owner>`. Property này theo dõi đối tượng nào đã khởi tạo đối tượng nào. Tuy nhiên, điều này chủ yếu hữu ích khi viết editor và tool.

Cuối cùng, khi một node được giải phóng bằng :ref:`Object.free()<class_Object_method_free>` hoặc :ref:`queue_free()<class_Node_method_queue_free>`, nó cũng sẽ giải phóng tất cả node con của mình.

\ **Group:** Node có thể được thêm vào bao nhiêu group tùy thích để dễ quản lý; chẳng hạn, bạn có thể tạo các group như "enemies" hoặc "collectables", tùy thuộc vào game của mình. Xem :ref:`add_to_group()<class_Node_method_add_to_group>`, :ref:`is_in_group()<class_Node_method_is_in_group>` và :ref:`remove_from_group()<class_Node_method_remove_from_group>`. Sau đó, bạn có thể lấy tất cả node trong các group này, lặp qua chúng và thậm chí gọi các method trên group thông qua các method của :ref:`SceneTree<class_SceneTree>`.

\ **Networking với node:** Sau khi kết nối đến một server (hoặc tạo một server, xem :ref:`ENetMultiplayerPeer<class_ENetMultiplayerPeer>`), bạn có thể dùng hệ thống RPC (remote procedure call) tích hợp sẵn để giao tiếp qua network. Bằng cách gọi :ref:`rpc()<class_Node_method_rpc>` với tên method, method đó sẽ được gọi cục bộ và trên tất cả peer đã kết nối (peer = client và server chấp nhận các kết nối). Để xác định node nào nhận lệnh gọi RPC, Godot sẽ sử dụng :ref:`NodePath<class_NodePath>` của node đó (hãy đảm bảo tên node giống nhau trên tất cả peer). Ngoài ra, hãy xem tutorial networking cấp cao và các bản demo tương ứng.

\ **Lưu ý:** Property ``script`` thuộc lớp :ref:`Object<class_Object>`, không phải **Node**. Property này không được expose như hầu hết property khác nhưng có setter và getter (xem :ref:`Object.set_script()<class_Object_method_set_script>` và :ref:`Object.get_script()<class_Object_method_get_script>`).

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Node và scene <../getting_started/step_by_step/nodes_and_scenes>`

- `All Demos <https://github.com/godotengine/godot-demo-projects/>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>`                       | :ref:`auto_translate_mode<class_Node_property_auto_translate_mode>`               | ``0``     |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>`                                                 | :ref:`editor_description<class_Node_property_editor_description>`                 | ``""``    |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`MultiplayerAPI<class_MultiplayerAPI>`                                 | :ref:`multiplayer<class_Node_property_multiplayer>`                               |           |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`StringName<class_StringName>`                                         | :ref:`name<class_Node_property_name>`                                             |           |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`Node<class_Node>`                                                     | :ref:`owner<class_Node_property_owner>`                                           |           |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>`         | :ref:`physics_interpolation_mode<class_Node_property_physics_interpolation_mode>` | ``0``     |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`ProcessMode<enum_Node_ProcessMode>`                                   | :ref:`process_mode<class_Node_property_process_mode>`                             | ``0``     |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                                       | :ref:`process_physics_priority<class_Node_property_process_physics_priority>`     | ``0``     |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                                       | :ref:`process_priority<class_Node_property_process_priority>`                     | ``0``     |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>`                     | :ref:`process_thread_group<class_Node_property_process_thread_group>`             | ``0``     |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                                       | :ref:`process_thread_group_order<class_Node_property_process_thread_group_order>` |           |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | |bitfield|\[:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>`\] | :ref:`process_thread_messages<class_Node_property_process_thread_messages>`       |           |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>`                                                 | :ref:`scene_file_path<class_Node_property_scene_file_path>`                       |           |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                     | :ref:`unique_name_in_owner<class_Node_property_unique_name_in_owner>`             | ``false`` |
   +-----------------------------------------------------------------------------+-----------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_enter_tree<class_Node_private_method__enter_tree>`\ (\ ) |virtual|                                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_exit_tree<class_Node_private_method__exit_tree>`\ (\ ) |virtual|                                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_accessibility_configuration_warnings<class_Node_private_method__get_accessibility_configuration_warnings>`\ (\ ) |virtual| |const|                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`_get_configuration_warnings<class_Node_private_method__get_configuration_warnings>`\ (\ ) |virtual| |const|                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                            | :ref:`_get_focused_accessibility_element<class_Node_private_method__get_focused_accessibility_element>`\ (\ ) |virtual| |const|                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_input<class_Node_private_method__input>`\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual|                                                                                                                            |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_physics_process<class_Node_private_method__physics_process>`\ (\ delta\: :ref:`float<class_float>`\ ) |virtual|                                                                                                                  |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_process<class_Node_private_method__process>`\ (\ delta\: :ref:`float<class_float>`\ ) |virtual|                                                                                                                                  |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_ready<class_Node_private_method__ready>`\ (\ ) |virtual|                                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_shortcut_input<class_Node_private_method__shortcut_input>`\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual|                                                                                                          |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_unhandled_input<class_Node_private_method__unhandled_input>`\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual|                                                                                                        |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_unhandled_key_input<class_Node_private_method__unhandled_key_input>`\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual|                                                                                                |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_child<class_Node_method_add_child>`\ (\ node\: :ref:`Node<class_Node>`, force_readable_name\: :ref:`bool<class_bool>` = false, internal\: :ref:`InternalMode<enum_Node_InternalMode>` = 0\ )                                  |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_sibling<class_Node_method_add_sibling>`\ (\ sibling\: :ref:`Node<class_Node>`, force_readable_name\: :ref:`bool<class_bool>` = false\ )                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_to_group<class_Node_method_add_to_group>`\ (\ group\: :ref:`StringName<class_StringName>`, persistent\: :ref:`bool<class_bool>` = false\ )                                                                                    |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`atr<class_Node_method_atr>`\ (\ message\: :ref:`String<class_String>`, context\: :ref:`StringName<class_StringName>` = ""\ ) |const|                                                                                              |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`atr_n<class_Node_method_atr_n>`\ (\ message\: :ref:`String<class_String>`, plural_message\: :ref:`StringName<class_StringName>`, n\: :ref:`int<class_int>`, context\: :ref:`StringName<class_StringName>` = ""\ ) |const|         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`call_deferred_thread_group<class_Node_method_call_deferred_thread_group>`\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`call_thread_safe<class_Node_method_call_thread_safe>`\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`can_auto_translate<class_Node_method_can_auto_translate>`\ (\ ) |const|                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`can_process<class_Node_method_can_process>`\ (\ ) |const|                                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Tween<class_Tween>`                                        | :ref:`create_tween<class_Node_method_create_tween>`\ (\ )                                                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`duplicate<class_Node_method_duplicate>`\ (\ flags\: :ref:`int<class_int>` = 15\ ) |const|                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`find_child<class_Node_method_find_child>`\ (\ pattern\: :ref:`String<class_String>`, recursive\: :ref:`bool<class_bool>` = true, owned\: :ref:`bool<class_bool>` = true\ ) |const|                                                |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\]             | :ref:`find_children<class_Node_method_find_children>`\ (\ pattern\: :ref:`String<class_String>`, type\: :ref:`String<class_String>` = "", recursive\: :ref:`bool<class_bool>` = true, owned\: :ref:`bool<class_bool>` = true\ ) |const| |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`find_parent<class_Node_method_find_parent>`\ (\ pattern\: :ref:`String<class_String>`\ ) |const|                                                                                                                                  |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                            | :ref:`get_accessibility_element<class_Node_method_get_accessibility_element>`\ (\ ) |const|                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`get_child<class_Node_method_get_child>`\ (\ idx\: :ref:`int<class_int>`, include_internal\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                            |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_child_count<class_Node_method_get_child_count>`\ (\ include_internal\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\]             | :ref:`get_children<class_Node_method_get_children>`\ (\ include_internal\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] | :ref:`get_groups<class_Node_method_get_groups>`\ (\ ) |const|                                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_index<class_Node_method_get_index>`\ (\ include_internal\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Window<class_Window>`                                      | :ref:`get_last_exclusive_window<class_Node_method_get_last_exclusive_window>`\ (\ ) |const|                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_multiplayer_authority<class_Node_method_get_multiplayer_authority>`\ (\ ) |const|                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`get_node<class_Node_method_get_node>`\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const|                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                        | :ref:`get_node_and_resource<class_Node_method_get_node_and_resource>`\ (\ path\: :ref:`NodePath<class_NodePath>`\ )                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`get_node_or_null<class_Node_method_get_node_or_null>`\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const|                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get_node_rpc_config<class_Node_method_get_node_rpc_config>`\ (\ ) |const|                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`int<class_int>`\]               | :ref:`get_orphan_node_ids<class_Node_method_get_orphan_node_ids>`\ (\ ) |static|                                                                                                                                                        |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node<class_Node>`                                          | :ref:`get_parent<class_Node_method_get_parent>`\ (\ ) |const|                                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                  | :ref:`get_path<class_Node_method_get_path>`\ (\ ) |const|                                                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                  | :ref:`get_path_to<class_Node_method_get_path_to>`\ (\ node\: :ref:`Node<class_Node>`, use_unique_path\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                      |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_physics_process_delta_time<class_Node_method_get_physics_process_delta_time>`\ (\ ) |const|                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_process_delta_time<class_Node_method_get_process_delta_time>`\ (\ ) |const|                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`get_scene_instance_load_placeholder<class_Node_method_get_scene_instance_load_placeholder>`\ (\ ) |const|                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`SceneTree<class_SceneTree>`                                | :ref:`get_tree<class_Node_method_get_tree>`\ (\ ) |const|                                                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`get_tree_string<class_Node_method_get_tree_string>`\ (\ )                                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`get_tree_string_pretty<class_Node_method_get_tree_string_pretty>`\ (\ )                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Viewport<class_Viewport>`                                  | :ref:`get_viewport<class_Node_method_get_viewport>`\ (\ ) |const|                                                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Window<class_Window>`                                      | :ref:`get_window<class_Node_method_get_window>`\ (\ ) |const|                                                                                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_node<class_Node_method_has_node>`\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const|                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_node_and_resource<class_Node_method_has_node_and_resource>`\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const|                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_ancestor_of<class_Node_method_is_ancestor_of>`\ (\ node\: :ref:`Node<class_Node>`\ ) |const|                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_displayed_folded<class_Node_method_is_displayed_folded>`\ (\ ) |const|                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_editable_instance<class_Node_method_is_editable_instance>`\ (\ node\: :ref:`Node<class_Node>`\ ) |const|                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_greater_than<class_Node_method_is_greater_than>`\ (\ node\: :ref:`Node<class_Node>`\ ) |const|                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_in_group<class_Node_method_is_in_group>`\ (\ group\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                            |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_inside_tree<class_Node_method_is_inside_tree>`\ (\ ) |const|                                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_multiplayer_authority<class_Node_method_is_multiplayer_authority>`\ (\ ) |const|                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_node_ready<class_Node_method_is_node_ready>`\ (\ ) |const|                                                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_part_of_edited_scene<class_Node_method_is_part_of_edited_scene>`\ (\ ) |const|                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_physics_interpolated<class_Node_method_is_physics_interpolated>`\ (\ ) |const|                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_physics_interpolated_and_enabled<class_Node_method_is_physics_interpolated_and_enabled>`\ (\ ) |const|                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_physics_processing<class_Node_method_is_physics_processing>`\ (\ ) |const|                                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_physics_processing_internal<class_Node_method_is_physics_processing_internal>`\ (\ ) |const|                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_processing<class_Node_method_is_processing>`\ (\ ) |const|                                                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_processing_input<class_Node_method_is_processing_input>`\ (\ ) |const|                                                                                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_processing_internal<class_Node_method_is_processing_internal>`\ (\ ) |const|                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_processing_shortcut_input<class_Node_method_is_processing_shortcut_input>`\ (\ ) |const|                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_processing_unhandled_input<class_Node_method_is_processing_unhandled_input>`\ (\ ) |const|                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_processing_unhandled_key_input<class_Node_method_is_processing_unhandled_key_input>`\ (\ ) |const|                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`move_child<class_Node_method_move_child>`\ (\ child_node\: :ref:`Node<class_Node>`, to_index\: :ref:`int<class_int>`\ )                                                                                                           |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`notify_deferred_thread_group<class_Node_method_notify_deferred_thread_group>`\ (\ what\: :ref:`int<class_int>`\ )                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`notify_thread_safe<class_Node_method_notify_thread_safe>`\ (\ what\: :ref:`int<class_int>`\ )                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`print_orphan_nodes<class_Node_method_print_orphan_nodes>`\ (\ ) |static|                                                                                                                                                          |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`print_tree<class_Node_method_print_tree>`\ (\ )                                                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`print_tree_pretty<class_Node_method_print_tree_pretty>`\ (\ )                                                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`propagate_call<class_Node_method_propagate_call>`\ (\ method\: :ref:`StringName<class_StringName>`, args\: :ref:`Array<class_Array>` = [], parent_first\: :ref:`bool<class_bool>` = false\ )                                      |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`propagate_notification<class_Node_method_propagate_notification>`\ (\ what\: :ref:`int<class_int>`\ )                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`queue_accessibility_update<class_Node_method_queue_accessibility_update>`\ (\ )                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`queue_free<class_Node_method_queue_free>`\ (\ )                                                                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_child<class_Node_method_remove_child>`\ (\ node\: :ref:`Node<class_Node>`\ )                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_from_group<class_Node_method_remove_from_group>`\ (\ group\: :ref:`StringName<class_StringName>`\ )                                                                                                                        |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`reparent<class_Node_method_reparent>`\ (\ new_parent\: :ref:`Node<class_Node>`, keep_global_transform\: :ref:`bool<class_bool>` = true\ )                                                                                         |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`replace_by<class_Node_method_replace_by>`\ (\ node\: :ref:`Node<class_Node>`, keep_groups\: :ref:`bool<class_bool>` = false\ )                                                                                                    |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`request_ready<class_Node_method_request_ready>`\ (\ )                                                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`reset_physics_interpolation<class_Node_method_reset_physics_interpolation>`\ (\ )                                                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`rpc<class_Node_method_rpc>`\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`rpc_config<class_Node_method_rpc_config>`\ (\ method\: :ref:`StringName<class_StringName>`, config\: :ref:`Variant<class_Variant>`\ )                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`rpc_id<class_Node_method_rpc_id>`\ (\ peer_id\: :ref:`int<class_int>`, method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                              |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_deferred_thread_group<class_Node_method_set_deferred_thread_group>`\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                              |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_display_folded<class_Node_method_set_display_folded>`\ (\ fold\: :ref:`bool<class_bool>`\ )                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_editable_instance<class_Node_method_set_editable_instance>`\ (\ node\: :ref:`Node<class_Node>`, is_editable\: :ref:`bool<class_bool>`\ )                                                                                      |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_multiplayer_authority<class_Node_method_set_multiplayer_authority>`\ (\ id\: :ref:`int<class_int>`, recursive\: :ref:`bool<class_bool>` = true\ )                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_physics_process<class_Node_method_set_physics_process>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_physics_process_internal<class_Node_method_set_physics_process_internal>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_process<class_Node_method_set_process>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_process_input<class_Node_method_set_process_input>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                                   |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_process_internal<class_Node_method_set_process_internal>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_process_shortcut_input<class_Node_method_set_process_shortcut_input>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                 |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_process_unhandled_input<class_Node_method_set_process_unhandled_input>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                               |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_process_unhandled_key_input<class_Node_method_set_process_unhandled_key_input>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_scene_instance_load_placeholder<class_Node_method_set_scene_instance_load_placeholder>`\ (\ load_placeholder\: :ref:`bool<class_bool>`\ )                                                                                     |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_thread_safe<class_Node_method_set_thread_safe>`\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                  |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_translation_domain_inherited<class_Node_method_set_translation_domain_inherited>`\ (\ )                                                                                                                                       |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`update_configuration_warnings<class_Node_method_update_configuration_warnings>`\ (\ )                                                                                                                                             |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_Node_signal_child_entered_tree:

.. rst-class:: classref-signal

**child_entered_tree**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_Node_signal_child_entered_tree>`

Được phát ra khi child ``node`` đi vào :ref:`SceneTree<class_SceneTree>`, thường là do node này đi vào cây (xem :ref:`tree_entered<class_Node_signal_tree_entered>`), hoặc :ref:`add_child()<class_Node_method_add_child>` đã được gọi.

Signal này được phát ra *sau* :ref:`NOTIFICATION_ENTER_TREE<class_Node_constant_NOTIFICATION_ENTER_TREE>` và :ref:`tree_entered<class_Node_signal_tree_entered>` của chính child node đó.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_child_exiting_tree:

.. rst-class:: classref-signal

**child_exiting_tree**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_Node_signal_child_exiting_tree>`

Được phát ra khi child ``node`` sắp rời khỏi :ref:`SceneTree<class_SceneTree>`, thường là do node này đang rời khỏi cây (xem :ref:`tree_exiting<class_Node_signal_tree_exiting>`), hoặc do child ``node`` đang bị xóa hoặc giải phóng.

Khi nhận signal này, child ``node`` vẫn có thể truy cập bên trong cây. Signal này được phát ra *sau* :ref:`tree_exiting<class_Node_signal_tree_exiting>` và :ref:`NOTIFICATION_EXIT_TREE<class_Node_constant_NOTIFICATION_EXIT_TREE>` của chính child node đó.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_child_order_changed:

.. rst-class:: classref-signal

**child_order_changed**\ (\ ) :ref:`🔗<class_Node_signal_child_order_changed>`

Được phát ra khi danh sách các node con thay đổi. Điều này xảy ra khi node con được thêm, di chuyển hoặc xóa.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_editor_description_changed:

.. rst-class:: classref-signal

**editor_description_changed**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_Node_signal_editor_description_changed>`

Được phát ra khi trường mô tả của node trong editor thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_editor_state_changed:

.. rst-class:: classref-signal

**editor_state_changed**\ (\ ) :ref:`🔗<class_Node_signal_editor_state_changed>`

Được phát ra khi một thuộc tính của node có liên quan đến editor thay đổi. Chỉ được phát ra trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_ready:

.. rst-class:: classref-signal

**ready**\ (\ ) :ref:`🔗<class_Node_signal_ready>`

Được phát ra khi node được xem là đã sẵn sàng, sau khi :ref:`_ready()<class_Node_private_method__ready>` được gọi.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_renamed:

.. rst-class:: classref-signal

**renamed**\ (\ ) :ref:`🔗<class_Node_signal_renamed>`

Được phát ra khi :ref:`name<class_Node_property_name>` của node thay đổi, nếu node đang ở bên trong cây.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_replacing_by:

.. rst-class:: classref-signal

**replacing_by**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_Node_signal_replacing_by>`

Được phát ra khi node này đang được thay thế bởi ``node``, xem :ref:`replace_by()<class_Node_method_replace_by>`.

Signal này được phát ra *sau* khi ``node`` đã được thêm làm child của node cha ban đầu, nhưng *trước* khi tất cả node con ban đầu được chuyển parent sang ``node``.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_tree_entered:

.. rst-class:: classref-signal

**tree_entered**\ (\ ) :ref:`🔗<class_Node_signal_tree_entered>`

Được phát ra khi node đi vào cây.

Signal này được phát ra *sau* thông báo :ref:`NOTIFICATION_ENTER_TREE<class_Node_constant_NOTIFICATION_ENTER_TREE>` liên quan.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_tree_exited:

.. rst-class:: classref-signal

**tree_exited**\ (\ ) :ref:`🔗<class_Node_signal_tree_exited>`

Được phát ra sau khi node rời khỏi cây và không còn hoạt động.

Signal này được phát ra *sau* thông báo :ref:`NOTIFICATION_EXIT_TREE<class_Node_constant_NOTIFICATION_EXIT_TREE>` liên quan.

.. rst-class:: classref-item-separator

----

.. _class_Node_signal_tree_exiting:

.. rst-class:: classref-signal

**tree_exiting**\ (\ ) :ref:`🔗<class_Node_signal_tree_exiting>`

Được phát ra khi node sắp rời khỏi cây. Node vẫn hợp lệ. Vì vậy, đây là nơi phù hợp để thực hiện việc de-initialization (hoặc "destructor", nếu bạn muốn gọi như vậy).

Signal này được phát ra *sau* :ref:`_exit_tree()<class_Node_private_method__exit_tree>` của node và *trước* :ref:`NOTIFICATION_EXIT_TREE<class_Node_constant_NOTIFICATION_EXIT_TREE>` liên quan.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_Node_ProcessMode:

.. rst-class:: classref-enumeration

enum **ProcessMode**: :ref:`🔗<enum_Node_ProcessMode>`

.. _class_Node_constant_PROCESS_MODE_INHERIT:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessMode<enum_Node_ProcessMode>` **PROCESS_MODE_INHERIT** = ``0``

Kế thừa :ref:`process_mode<class_Node_property_process_mode>` từ node cha của node. Đây là giá trị mặc định cho mọi node mới được tạo.

.. _class_Node_constant_PROCESS_MODE_PAUSABLE:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessMode<enum_Node_ProcessMode>` **PROCESS_MODE_PAUSABLE** = ``1``

Xử lý khi :ref:`SceneTree.paused<class_SceneTree_property_paused>` là ``false``. Đây là nghịch đảo của :ref:`PROCESS_MODE_WHEN_PAUSED<class_Node_constant_PROCESS_MODE_WHEN_PAUSED>` và là giá trị mặc định cho node gốc.

.. _class_Node_constant_PROCESS_MODE_WHEN_PAUSED:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessMode<enum_Node_ProcessMode>` **PROCESS_MODE_WHEN_PAUSED** = ``2``

Chỉ xử lý khi :ref:`SceneTree.paused<class_SceneTree_property_paused>` là ``true``. Đây là nghịch đảo của :ref:`PROCESS_MODE_PAUSABLE<class_Node_constant_PROCESS_MODE_PAUSABLE>`.

.. _class_Node_constant_PROCESS_MODE_ALWAYS:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessMode<enum_Node_ProcessMode>` **PROCESS_MODE_ALWAYS** = ``3``

Luôn xử lý. Tiếp tục xử lý, bỏ qua :ref:`SceneTree.paused<class_SceneTree_property_paused>`. Đây là nghịch đảo của :ref:`PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`.

.. _class_Node_constant_PROCESS_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessMode<enum_Node_ProcessMode>` **PROCESS_MODE_DISABLED** = ``4``

Không bao giờ xử lý. Vô hiệu hóa hoàn toàn việc xử lý, bỏ qua :ref:`SceneTree.paused<class_SceneTree_property_paused>`. Đây là nghịch đảo của :ref:`PROCESS_MODE_ALWAYS<class_Node_constant_PROCESS_MODE_ALWAYS>`.

.. rst-class:: classref-item-separator

----

.. _enum_Node_ProcessThreadGroup:

.. rst-class:: classref-enumeration

enum **ProcessThreadGroup**: :ref:`🔗<enum_Node_ProcessThreadGroup>`

.. _class_Node_constant_PROCESS_THREAD_GROUP_INHERIT:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>` **PROCESS_THREAD_GROUP_INHERIT** = ``0``

Xử lý node này dựa trên chế độ thread group của node cha đầu tiên (hoặc node ông bà) có chế độ thread group không phải inherit. Xem :ref:`process_thread_group<class_Node_property_process_thread_group>` để biết thêm thông tin.

.. _class_Node_constant_PROCESS_THREAD_GROUP_MAIN_THREAD:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>` **PROCESS_THREAD_GROUP_MAIN_THREAD** = ``1``

Xử lý node này (và các node con được đặt thành inherit) trên main thread. Xem :ref:`process_thread_group<class_Node_property_process_thread_group>` để biết thêm thông tin.

.. _class_Node_constant_PROCESS_THREAD_GROUP_SUB_THREAD:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>` **PROCESS_THREAD_GROUP_SUB_THREAD** = ``2``

Xử lý node này (và các node con được đặt thành inherit) trên sub-thread. Xem :ref:`process_thread_group<class_Node_property_process_thread_group>` để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _enum_Node_ProcessThreadMessages:

.. rst-class:: classref-enumeration

flags **ProcessThreadMessages**: :ref:`🔗<enum_Node_ProcessThreadMessages>`

.. _class_Node_constant_FLAG_PROCESS_THREAD_MESSAGES:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>` **FLAG_PROCESS_THREAD_MESSAGES** = ``1``

Cho phép node này xử lý các threaded message được tạo bằng :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>` ngay trước khi :ref:`_process()<class_Node_private_method__process>` được gọi.

.. _class_Node_constant_FLAG_PROCESS_THREAD_MESSAGES_PHYSICS:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>` **FLAG_PROCESS_THREAD_MESSAGES_PHYSICS** = ``2``

Cho phép node này xử lý các threaded message được tạo bằng :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>` ngay trước khi :ref:`_physics_process()<class_Node_private_method__physics_process>` được gọi.

.. _class_Node_constant_FLAG_PROCESS_THREAD_MESSAGES_ALL:

.. rst-class:: classref-enumeration-constant

:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>` **FLAG_PROCESS_THREAD_MESSAGES_ALL** = ``3``

Cho phép node này xử lý các threaded message được tạo bằng :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>` ngay trước khi :ref:`_process()<class_Node_private_method__process>` hoặc :ref:`_physics_process()<class_Node_private_method__physics_process>` được gọi.

.. rst-class:: classref-item-separator

----

.. _enum_Node_PhysicsInterpolationMode:

.. rst-class:: classref-enumeration

enum **PhysicsInterpolationMode**: :ref:`🔗<enum_Node_PhysicsInterpolationMode>`

.. _class_Node_constant_PHYSICS_INTERPOLATION_MODE_INHERIT:

.. rst-class:: classref-enumeration-constant

:ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` **PHYSICS_INTERPOLATION_MODE_INHERIT** = ``0``

Kế thừa :ref:`physics_interpolation_mode<class_Node_property_physics_interpolation_mode>` từ node cha. Đây là giá trị mặc định cho mọi node mới được tạo.

.. _class_Node_constant_PHYSICS_INTERPOLATION_MODE_ON:

.. rst-class:: classref-enumeration-constant

:ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` **PHYSICS_INTERPOLATION_MODE_ON** = ``1``

Bật physics interpolation cho node này và các node con được đặt thành :ref:`PHYSICS_INTERPOLATION_MODE_INHERIT<class_Node_constant_PHYSICS_INTERPOLATION_MODE_INHERIT>`. Đây là giá trị mặc định cho node gốc.

.. _class_Node_constant_PHYSICS_INTERPOLATION_MODE_OFF:

.. rst-class:: classref-enumeration-constant

:ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` **PHYSICS_INTERPOLATION_MODE_OFF** = ``2``

Tắt physics interpolation cho node này và các node con được đặt thành :ref:`PHYSICS_INTERPOLATION_MODE_INHERIT<class_Node_constant_PHYSICS_INTERPOLATION_MODE_INHERIT>`.

.. rst-class:: classref-item-separator

----

.. _enum_Node_DuplicateFlags:

.. rst-class:: classref-enumeration

enum **DuplicateFlags**: :ref:`🔗<enum_Node_DuplicateFlags>`

.. _class_Node_constant_DUPLICATE_SIGNALS:

.. rst-class:: classref-enumeration-constant

:ref:`DuplicateFlags<enum_Node_DuplicateFlags>` **DUPLICATE_SIGNALS** = ``1``

Nhân bản các kết nối signal của node được kết nối với flag :ref:`Object.CONNECT_PERSIST<class_Object_constant_CONNECT_PERSIST>`.

.. _class_Node_constant_DUPLICATE_GROUPS:

.. rst-class:: classref-enumeration-constant

:ref:`DuplicateFlags<enum_Node_DuplicateFlags>` **DUPLICATE_GROUPS** = ``2``

Nhân bản các group của node.

.. _class_Node_constant_DUPLICATE_SCRIPTS:

.. rst-class:: classref-enumeration-constant

:ref:`DuplicateFlags<enum_Node_DuplicateFlags>` **DUPLICATE_SCRIPTS** = ``4``

Nhân bản script của node (đồng thời ghi đè script của các node con đã nhân bản nếu kết hợp với :ref:`DUPLICATE_USE_INSTANTIATION<class_Node_constant_DUPLICATE_USE_INSTANTIATION>`).

.. _class_Node_constant_DUPLICATE_USE_INSTANTIATION:

.. rst-class:: classref-enumeration-constant

:ref:`DuplicateFlags<enum_Node_DuplicateFlags>` **DUPLICATE_USE_INSTANTIATION** = ``8``

Nhân bản bằng :ref:`PackedScene.instantiate()<class_PackedScene_method_instantiate>`. Nếu node bắt nguồn từ một scene được lưu trên ổ đĩa, sử dụng lại :ref:`PackedScene.instantiate()<class_PackedScene_method_instantiate>` làm cơ sở cho node đã nhân bản và các node con của nó.

.. _class_Node_constant_DUPLICATE_INTERNAL_STATE:

.. rst-class:: classref-enumeration-constant

:ref:`DuplicateFlags<enum_Node_DuplicateFlags>` **DUPLICATE_INTERNAL_STATE** = ``16``

Đồng thời nhân bản các biến không thể tuần tự hóa (tức là không có :ref:`@GlobalScope.PROPERTY_USAGE_STORAGE<class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>`).

.. _class_Node_constant_DUPLICATE_DEFAULT:

.. rst-class:: classref-enumeration-constant

:ref:`DuplicateFlags<enum_Node_DuplicateFlags>` **DUPLICATE_DEFAULT** = ``15``

Nhân bản bằng các flag mặc định. Hằng số này hữu ích khi thêm hoặc xóa một flag đơn lẻ.

::

    # Nhân bản các biến không được export.
    var dupe = duplicate(DUPLICATE_DEFAULT | DUPLICATE_INTERNAL_STATE)

.. rst-class:: classref-item-separator

----

.. _enum_Node_InternalMode:

.. rst-class:: classref-enumeration

enum **InternalMode**: :ref:`🔗<enum_Node_InternalMode>`

.. _class_Node_constant_INTERNAL_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`InternalMode<enum_Node_InternalMode>` **INTERNAL_MODE_DISABLED** = ``0``

Node sẽ không ở trạng thái internal.

.. _class_Node_constant_INTERNAL_MODE_FRONT:

.. rst-class:: classref-enumeration-constant

:ref:`InternalMode<enum_Node_InternalMode>` **INTERNAL_MODE_FRONT** = ``1``

Node sẽ được đặt ở đầu danh sách node con của node cha, trước mọi sibling không phải internal.

.. _class_Node_constant_INTERNAL_MODE_BACK:

.. rst-class:: classref-enumeration-constant

:ref:`InternalMode<enum_Node_InternalMode>` **INTERNAL_MODE_BACK** = ``2``

Node sẽ được đặt ở cuối danh sách node con của node cha, sau mọi sibling không phải internal.

.. rst-class:: classref-item-separator

----

.. _enum_Node_AutoTranslateMode:

.. rst-class:: classref-enumeration

enum **AutoTranslateMode**: :ref:`🔗<enum_Node_AutoTranslateMode>`

.. _class_Node_constant_AUTO_TRANSLATE_MODE_INHERIT:

.. rst-class:: classref-enumeration-constant

:ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **AUTO_TRANSLATE_MODE_INHERIT** = ``0``

Kế thừa :ref:`auto_translate_mode<class_Node_property_auto_translate_mode>` từ node cha. Đây là giá trị mặc định cho mọi node mới được tạo.

.. _class_Node_constant_AUTO_TRANSLATE_MODE_ALWAYS:

.. rst-class:: classref-enumeration-constant

:ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **AUTO_TRANSLATE_MODE_ALWAYS** = ``1``

Luôn tự động dịch. Đây là giá trị đối nghịch với :ref:`AUTO_TRANSLATE_MODE_DISABLED<class_Node_constant_AUTO_TRANSLATE_MODE_DISABLED>` và là giá trị mặc định cho node gốc.

.. _class_Node_constant_AUTO_TRANSLATE_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **AUTO_TRANSLATE_MODE_DISABLED** = ``2``

Không bao giờ tự động dịch. Đây là giá trị đối nghịch với :ref:`AUTO_TRANSLATE_MODE_ALWAYS<class_Node_constant_AUTO_TRANSLATE_MODE_ALWAYS>`.

Việc phân tích chuỗi để tạo translation template sẽ được bỏ qua đối với node này và các node con được đặt thành :ref:`AUTO_TRANSLATE_MODE_INHERIT<class_Node_constant_AUTO_TRANSLATE_MODE_INHERIT>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_Node_constant_NOTIFICATION_ENTER_TREE:

.. rst-class:: classref-constant

**NOTIFICATION_ENTER_TREE** = ``10`` :ref:`🔗<class_Node_constant_NOTIFICATION_ENTER_TREE>`

Thông báo được nhận khi node đi vào một :ref:`SceneTree<class_SceneTree>`. Xem :ref:`_enter_tree()<class_Node_private_method__enter_tree>`.

Thông báo này được nhận *trước* signal :ref:`tree_entered<class_Node_signal_tree_entered>` liên quan.

.. _class_Node_constant_NOTIFICATION_EXIT_TREE:

.. rst-class:: classref-constant

**NOTIFICATION_EXIT_TREE** = ``11`` :ref:`🔗<class_Node_constant_NOTIFICATION_EXIT_TREE>`

Thông báo được nhận khi node sắp rời khỏi một :ref:`SceneTree<class_SceneTree>`. Xem :ref:`_exit_tree()<class_Node_private_method__exit_tree>`.

Thông báo này được nhận *sau* signal :ref:`tree_exiting<class_Node_signal_tree_exiting>` liên quan.

Thông báo này được gửi theo thứ tự ngược lại.

.. _class_Node_constant_NOTIFICATION_MOVED_IN_PARENT:

.. rst-class:: classref-constant

**NOTIFICATION_MOVED_IN_PARENT** = ``12`` :ref:`🔗<class_Node_constant_NOTIFICATION_MOVED_IN_PARENT>`

**Đã lỗi thời:** Engine không còn gửi thông báo này. Thay vào đó, hãy dùng :ref:`NOTIFICATION_CHILD_ORDER_CHANGED<class_Node_constant_NOTIFICATION_CHILD_ORDER_CHANGED>`.



.. _class_Node_constant_NOTIFICATION_READY:

.. rst-class:: classref-constant

**NOTIFICATION_READY** = ``13`` :ref:`🔗<class_Node_constant_NOTIFICATION_READY>`

Thông báo được nhận khi node đã sẵn sàng. Xem :ref:`_ready()<class_Node_private_method__ready>`.

.. _class_Node_constant_NOTIFICATION_PAUSED:

.. rst-class:: classref-constant

**NOTIFICATION_PAUSED** = ``14`` :ref:`🔗<class_Node_constant_NOTIFICATION_PAUSED>`

Thông báo được nhận khi node bị tạm dừng. Xem :ref:`process_mode<class_Node_property_process_mode>`.

.. _class_Node_constant_NOTIFICATION_UNPAUSED:

.. rst-class:: classref-constant

**NOTIFICATION_UNPAUSED** = ``15`` :ref:`🔗<class_Node_constant_NOTIFICATION_UNPAUSED>`

Thông báo được nhận khi node tiếp tục hoạt động. Xem :ref:`process_mode<class_Node_property_process_mode>`.

.. _class_Node_constant_NOTIFICATION_PHYSICS_PROCESS:

.. rst-class:: classref-constant

**NOTIFICATION_PHYSICS_PROCESS** = ``16`` :ref:`🔗<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>`

Thông báo được nhận từ tree trong mỗi physics frame khi :ref:`is_physics_processing()<class_Node_method_is_physics_processing>` trả về ``true``. Xem :ref:`_physics_process()<class_Node_private_method__physics_process>`.

.. _class_Node_constant_NOTIFICATION_PROCESS:

.. rst-class:: classref-constant

**NOTIFICATION_PROCESS** = ``17`` :ref:`🔗<class_Node_constant_NOTIFICATION_PROCESS>`

Thông báo được nhận từ tree trong mỗi rendered frame khi :ref:`is_processing()<class_Node_method_is_processing>` trả về ``true``. Xem :ref:`_process()<class_Node_private_method__process>`.

.. _class_Node_constant_NOTIFICATION_PARENTED:

.. rst-class:: classref-constant

**NOTIFICATION_PARENTED** = ``18`` :ref:`🔗<class_Node_constant_NOTIFICATION_PARENTED>`

Thông báo được nhận khi node được đặt làm node con của một node khác (xem :ref:`add_child()<class_Node_method_add_child>` và :ref:`add_sibling()<class_Node_method_add_sibling>`).

\ **Lưu ý:** Điều này *không* có nghĩa là node đã đi vào :ref:`SceneTree<class_SceneTree>`.

.. _class_Node_constant_NOTIFICATION_UNPARENTED:

.. rst-class:: classref-constant

**NOTIFICATION_UNPARENTED** = ``19`` :ref:`🔗<class_Node_constant_NOTIFICATION_UNPARENTED>`

Thông báo được nhận khi node cha gọi :ref:`remove_child()<class_Node_method_remove_child>` trên node này.

\ **Lưu ý:** Điều này *không* có nghĩa là node đã rời khỏi :ref:`SceneTree<class_SceneTree>`.

.. _class_Node_constant_NOTIFICATION_SCENE_INSTANTIATED:

.. rst-class:: classref-constant

**NOTIFICATION_SCENE_INSTANTIATED** = ``20`` :ref:`🔗<class_Node_constant_NOTIFICATION_SCENE_INSTANTIATED>`

Thông báo chỉ được nhận bởi node gốc của scene vừa được instantiate, khi :ref:`PackedScene.instantiate()<class_PackedScene_method_instantiate>` hoàn tất.

.. _class_Node_constant_NOTIFICATION_DRAG_BEGIN:

.. rst-class:: classref-constant

**NOTIFICATION_DRAG_BEGIN** = ``21`` :ref:`🔗<class_Node_constant_NOTIFICATION_DRAG_BEGIN>`

Thông báo được nhận khi thao tác kéo bắt đầu. Tất cả node đều nhận thông báo này, không chỉ node đang được kéo.

Có thể được kích hoạt bằng cách kéo một :ref:`Control<class_Control>` cung cấp dữ liệu kéo (xem :ref:`Control._get_drag_data()<class_Control_private_method__get_drag_data>`) hoặc sử dụng :ref:`Control.force_drag()<class_Control_method_force_drag>`.

Sử dụng :ref:`Viewport.gui_get_drag_data()<class_Viewport_method_gui_get_drag_data>` để lấy dữ liệu đang được kéo.

.. _class_Node_constant_NOTIFICATION_DRAG_END:

.. rst-class:: classref-constant

**NOTIFICATION_DRAG_END** = ``22`` :ref:`🔗<class_Node_constant_NOTIFICATION_DRAG_END>`

Thông báo được nhận khi thao tác kéo kết thúc.

Sử dụng :ref:`Viewport.gui_is_drag_successful()<class_Viewport_method_gui_is_drag_successful>` để kiểm tra xem thao tác kéo có thành công hay không.

.. _class_Node_constant_NOTIFICATION_PATH_RENAMED:

.. rst-class:: classref-constant

**NOTIFICATION_PATH_RENAMED** = ``23`` :ref:`🔗<class_Node_constant_NOTIFICATION_PATH_RENAMED>`

Thông báo được nhận khi :ref:`name<class_Node_property_name>` của node hoặc :ref:`name<class_Node_property_name>` của một trong các ancestor của node bị thay đổi. Thông báo này *không* được nhận khi node bị xóa khỏi :ref:`SceneTree<class_SceneTree>`.

.. _class_Node_constant_NOTIFICATION_CHILD_ORDER_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_CHILD_ORDER_CHANGED** = ``24`` :ref:`🔗<class_Node_constant_NOTIFICATION_CHILD_ORDER_CHANGED>`

Thông báo được nhận khi danh sách node con thay đổi. Điều này xảy ra khi node con được thêm, di chuyển hoặc xóa.

.. _class_Node_constant_NOTIFICATION_INTERNAL_PROCESS:

.. rst-class:: classref-constant

**NOTIFICATION_INTERNAL_PROCESS** = ``25`` :ref:`🔗<class_Node_constant_NOTIFICATION_INTERNAL_PROCESS>`

Thông báo được nhận từ tree trong mỗi rendered frame khi :ref:`is_processing_internal()<class_Node_method_is_processing_internal>` trả về ``true``.

.. _class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS:

.. rst-class:: classref-constant

**NOTIFICATION_INTERNAL_PHYSICS_PROCESS** = ``26`` :ref:`🔗<class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS>`

Thông báo được nhận từ tree trong mỗi physics frame khi :ref:`is_physics_processing_internal()<class_Node_method_is_physics_processing_internal>` trả về ``true``.

.. _class_Node_constant_NOTIFICATION_POST_ENTER_TREE:

.. rst-class:: classref-constant

**NOTIFICATION_POST_ENTER_TREE** = ``27`` :ref:`🔗<class_Node_constant_NOTIFICATION_POST_ENTER_TREE>`

Thông báo được nhận khi node đi vào tree, ngay trước khi :ref:`NOTIFICATION_READY<class_Node_constant_NOTIFICATION_READY>` có thể được nhận. Không giống như thông báo sau, thông báo này được gửi mỗi lần node đi vào tree, không chỉ một lần.

.. _class_Node_constant_NOTIFICATION_DISABLED:

.. rst-class:: classref-constant

**NOTIFICATION_DISABLED** = ``28`` :ref:`🔗<class_Node_constant_NOTIFICATION_DISABLED>`

Thông báo được nhận khi node bị vô hiệu hóa. Xem :ref:`PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`.

.. _class_Node_constant_NOTIFICATION_ENABLED:

.. rst-class:: classref-constant

**NOTIFICATION_ENABLED** = ``29`` :ref:`🔗<class_Node_constant_NOTIFICATION_ENABLED>`

Thông báo được nhận khi node được bật lại sau khi bị vô hiệu hóa. Xem :ref:`PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`.

.. _class_Node_constant_NOTIFICATION_RESET_PHYSICS_INTERPOLATION:

.. rst-class:: classref-constant

**NOTIFICATION_RESET_PHYSICS_INTERPOLATION** = ``2001`` :ref:`🔗<class_Node_constant_NOTIFICATION_RESET_PHYSICS_INTERPOLATION>`

Thông báo được nhận khi :ref:`reset_physics_interpolation()<class_Node_method_reset_physics_interpolation>` được gọi trên node hoặc các ancestor của node.

.. _class_Node_constant_NOTIFICATION_EDITOR_PRE_SAVE:

.. rst-class:: classref-constant

**NOTIFICATION_EDITOR_PRE_SAVE** = ``9001`` :ref:`🔗<class_Node_constant_NOTIFICATION_EDITOR_PRE_SAVE>`

Thông báo được nhận ngay trước khi scene chứa node được lưu trong editor. Thông báo này chỉ được gửi trong Godot editor và sẽ không xảy ra trong các project đã export.

.. _class_Node_constant_NOTIFICATION_EDITOR_POST_SAVE:

.. rst-class:: classref-constant

**NOTIFICATION_EDITOR_POST_SAVE** = ``9002`` :ref:`🔗<class_Node_constant_NOTIFICATION_EDITOR_POST_SAVE>`

Thông báo được nhận ngay sau khi scene chứa node được lưu trong editor. Thông báo này chỉ được gửi trong Godot editor và sẽ không xảy ra trong các project đã export.

.. _class_Node_constant_NOTIFICATION_WM_MOUSE_ENTER:

.. rst-class:: classref-constant

**NOTIFICATION_WM_MOUSE_ENTER** = ``1002`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_MOUSE_ENTER>`

Thông báo được nhận khi chuột đi vào cửa sổ.

Được triển khai cho các cửa sổ nhúng và trên các nền tảng desktop và web.

.. _class_Node_constant_NOTIFICATION_WM_MOUSE_EXIT:

.. rst-class:: classref-constant

**NOTIFICATION_WM_MOUSE_EXIT** = ``1003`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_MOUSE_EXIT>`

Thông báo được nhận khi chuột rời khỏi cửa sổ.

Được triển khai cho các cửa sổ nhúng và trên các nền tảng desktop và web.

.. _class_Node_constant_NOTIFICATION_WM_WINDOW_FOCUS_IN:

.. rst-class:: classref-constant

**NOTIFICATION_WM_WINDOW_FOCUS_IN** = ``1004`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_WINDOW_FOCUS_IN>`

Thông báo được nhận từ OS khi ancestor :ref:`Window<class_Window>` của node được focus. Đây có thể là sự thay đổi focus giữa hai cửa sổ của cùng một engine instance, hoặc từ desktop OS hay ứng dụng bên thứ ba sang một cửa sổ của game (trong trường hợp đó, :ref:`NOTIFICATION_APPLICATION_FOCUS_IN<class_Node_constant_NOTIFICATION_APPLICATION_FOCUS_IN>` cũng được nhận).

Node :ref:`Window<class_Window>` nhận thông báo này khi được focus.

.. _class_Node_constant_NOTIFICATION_WM_WINDOW_FOCUS_OUT:

.. rst-class:: classref-constant

**NOTIFICATION_WM_WINDOW_FOCUS_OUT** = ``1005`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_WINDOW_FOCUS_OUT>`

Thông báo được nhận từ OS khi ancestor :ref:`Window<class_Window>` của node mất focus. Đây có thể là sự thay đổi focus giữa hai cửa sổ của cùng một engine instance, hoặc từ một cửa sổ của game sang desktop OS hay ứng dụng bên thứ ba (trong trường hợp đó, :ref:`NOTIFICATION_APPLICATION_FOCUS_OUT<class_Node_constant_NOTIFICATION_APPLICATION_FOCUS_OUT>` cũng được nhận).

Node :ref:`Window<class_Window>` nhận thông báo này khi mất focus.

.. _class_Node_constant_NOTIFICATION_WM_CLOSE_REQUEST:

.. rst-class:: classref-constant

**NOTIFICATION_WM_CLOSE_REQUEST** = ``1006`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_CLOSE_REQUEST>`

Thông báo được nhận từ OS khi có yêu cầu đóng được gửi (ví dụ: đóng cửa sổ bằng nút "Close" hoặc :kbd:`Alt + F4`).

Được triển khai trên các nền tảng desktop.

.. _class_Node_constant_NOTIFICATION_WM_GO_BACK_REQUEST:

.. rst-class:: classref-constant

**NOTIFICATION_WM_GO_BACK_REQUEST** = ``1007`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_GO_BACK_REQUEST>`

Thông báo được nhận từ OS khi có yêu cầu quay lại được gửi (ví dụ: nhấn nút "Back" trên Android).

Chỉ được triển khai trên Android.

.. _class_Node_constant_NOTIFICATION_WM_SIZE_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_WM_SIZE_CHANGED** = ``1008`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_SIZE_CHANGED>`

Thông báo được nhận khi cửa sổ được thay đổi kích thước.

\ **Lưu ý:** Chỉ node :ref:`Window<class_Window>` được thay đổi kích thước nhận thông báo này và thông báo không được truyền đến các node con.

.. _class_Node_constant_NOTIFICATION_WM_DPI_CHANGE:

.. rst-class:: classref-constant

**NOTIFICATION_WM_DPI_CHANGE** = ``1009`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_DPI_CHANGE>`

Thông báo được nhận từ OS khi tỷ lệ dots per inch (DPI) của màn hình thay đổi. Chỉ được triển khai trên macOS.

.. _class_Node_constant_NOTIFICATION_VP_MOUSE_ENTER:

.. rst-class:: classref-constant

**NOTIFICATION_VP_MOUSE_ENTER** = ``1010`` :ref:`🔗<class_Node_constant_NOTIFICATION_VP_MOUSE_ENTER>`

Thông báo được nhận khi con trỏ chuột đi vào vùng hiển thị của :ref:`Viewport<class_Viewport>`, không bị che khuất phía sau các :ref:`Control<class_Control>`\ s hoặc :ref:`Window<class_Window>`\ s khác, với điều kiện :ref:`Viewport.gui_disable_input<class_Viewport_property_gui_disable_input>` của nó là ``false``, bất kể hiện tại nó có được focus hay không.

.. _class_Node_constant_NOTIFICATION_VP_MOUSE_EXIT:

.. rst-class:: classref-constant

**NOTIFICATION_VP_MOUSE_EXIT** = ``1011`` :ref:`🔗<class_Node_constant_NOTIFICATION_VP_MOUSE_EXIT>`

Thông báo được nhận khi con trỏ chuột rời khỏi vùng hiển thị của :ref:`Viewport<class_Viewport>`, không bị che khuất phía sau các :ref:`Control<class_Control>`\ s hoặc :ref:`Window<class_Window>`\ s khác, với điều kiện :ref:`Viewport.gui_disable_input<class_Viewport_property_gui_disable_input>` của nó là ``false``, bất kể hiện tại nó có được focus hay không.

.. _class_Node_constant_NOTIFICATION_WM_POSITION_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_WM_POSITION_CHANGED** = ``1012`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_POSITION_CHANGED>`

Thông báo được nhận khi cửa sổ được di chuyển.

.. _class_Node_constant_NOTIFICATION_WM_OUTPUT_MAX_LINEAR_VALUE_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_WM_OUTPUT_MAX_LINEAR_VALUE_CHANGED** = ``1013`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_OUTPUT_MAX_LINEAR_VALUE_CHANGED>`

Thông báo được nhận khi giá trị tuyến tính tối đa của output do :ref:`Window.get_output_max_linear_value()<class_Window_method_get_output_max_linear_value>` trả về thay đổi.

Điều này xảy ra khi output HDR được bật hoặc tắt và khi bất kỳ giá trị độ sáng output HDR nào của cửa sổ thay đổi, chẳng hạn như khi người chơi điều chỉnh cài đặt độ sáng màn hình hoặc di chuyển cửa sổ sang màn hình khác.

.. _class_Node_constant_NOTIFICATION_OS_MEMORY_WARNING:

.. rst-class:: classref-constant

**NOTIFICATION_OS_MEMORY_WARNING** = ``2009`` :ref:`🔗<class_Node_constant_NOTIFICATION_OS_MEMORY_WARNING>`

Thông báo được nhận từ OS khi ứng dụng vượt quá lượng bộ nhớ được cấp phát.

Chỉ được triển khai trên iOS.

.. _class_Node_constant_NOTIFICATION_TRANSLATION_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_TRANSLATION_CHANGED** = ``2010`` :ref:`🔗<class_Node_constant_NOTIFICATION_TRANSLATION_CHANGED>`

Thông báo được nhận khi bản dịch có thể đã thay đổi. Có thể được kích hoạt khi người dùng thay đổi locale, thay đổi :ref:`auto_translate_mode<class_Node_property_auto_translate_mode>` hoặc khi node đi vào scene tree. Có thể dùng để phản hồi các thay đổi ngôn ngữ, chẳng hạn như thay đổi các chuỗi UI ngay lập tức. Hữu ích khi làm việc với tính năng hỗ trợ translation tích hợp sẵn, chẳng hạn như :ref:`Object.tr()<class_Object_method_tr>`.

\ **Lưu ý:** Thông báo này được nhận cùng với :ref:`NOTIFICATION_ENTER_TREE<class_Node_constant_NOTIFICATION_ENTER_TREE>`, vì vậy nếu bạn đang instantiate một scene, các node con sẽ chưa được khởi tạo. Bạn có thể dùng nó để thiết lập translation cho node này và các node con được tạo từ script; hoặc nếu muốn truy cập các node con được thêm trong editor, hãy bảo đảm node đã sẵn sàng bằng :ref:`is_node_ready()<class_Node_method_is_node_ready>`.

::

    func _notification(what):
        if what == NOTIFICATION_TRANSLATION_CHANGED:
            if not is_node_ready():
                await ready # Chờ tín hiệu ready.
            $Label.text = atr("%d Bananas") % banana_counter

.. _class_Node_constant_NOTIFICATION_WM_ABOUT:

.. rst-class:: classref-constant

**NOTIFICATION_WM_ABOUT** = ``2011`` :ref:`🔗<class_Node_constant_NOTIFICATION_WM_ABOUT>`

Thông báo được nhận từ OS khi có yêu cầu cung cấp thông tin "About".

Chỉ được triển khai trên macOS.

.. _class_Node_constant_NOTIFICATION_CRASH:

.. rst-class:: classref-constant

**NOTIFICATION_CRASH** = ``2012`` :ref:`🔗<class_Node_constant_NOTIFICATION_CRASH>`

Thông báo được nhận từ crash handler của Godot khi engine sắp gặp sự cố.

Được triển khai trên các nền tảng desktop nếu crash handler được bật.

.. _class_Node_constant_NOTIFICATION_OS_IME_UPDATE:

.. rst-class:: classref-constant

**NOTIFICATION_OS_IME_UPDATE** = ``2013`` :ref:`🔗<class_Node_constant_NOTIFICATION_OS_IME_UPDATE>`

Thông báo được nhận từ OS khi Input Method Engine được cập nhật (ví dụ: thay đổi vị trí con trỏ IME hoặc chuỗi composition).

Được triển khai trên các nền tảng desktop và web.

.. _class_Node_constant_NOTIFICATION_APPLICATION_RESUMED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_RESUMED** = ``2014`` :ref:`🔗<class_Node_constant_NOTIFICATION_APPLICATION_RESUMED>`

Thông báo được nhận từ OS khi ứng dụng được tiếp tục.

Cụ thể cho các nền tảng Android và iOS.

.. _class_Node_constant_NOTIFICATION_APPLICATION_PAUSED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_PAUSED** = ``2015`` :ref:`🔗<class_Node_constant_NOTIFICATION_APPLICATION_PAUSED>`

Thông báo được nhận từ OS khi ứng dụng bị tạm dừng.

Cụ thể cho các nền tảng Android và iOS.

\ **Lưu ý:** Trên iOS, bạn chỉ có khoảng 5 giây để hoàn tất tác vụ được bắt đầu bởi signal này. Nếu vượt quá khoảng thời gian đó, iOS sẽ buộc app đóng thay vì tạm dừng app.

.. _class_Node_constant_NOTIFICATION_APPLICATION_FOCUS_IN:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_FOCUS_IN** = ``2016`` :ref:`🔗<class_Node_constant_NOTIFICATION_APPLICATION_FOCUS_IN>`

Thông báo được nhận từ OS khi ứng dụng được focus, tức là khi focus chuyển từ desktop OS hoặc ứng dụng bên thứ ba sang bất kỳ cửa sổ nào đang mở của Godot instance.

Được triển khai trên các nền tảng desktop và mobile.

.. _class_Node_constant_NOTIFICATION_APPLICATION_FOCUS_OUT:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_FOCUS_OUT** = ``2017`` :ref:`🔗<class_Node_constant_NOTIFICATION_APPLICATION_FOCUS_OUT>`

Thông báo được nhận từ OS khi ứng dụng mất focus, tức là khi focus chuyển từ bất kỳ cửa sổ nào đang mở của Godot instance sang desktop OS hoặc ứng dụng bên thứ ba.

Được triển khai trên các nền tảng desktop và mobile.

.. _class_Node_constant_NOTIFICATION_TEXT_SERVER_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_TEXT_SERVER_CHANGED** = ``2018`` :ref:`🔗<class_Node_constant_NOTIFICATION_TEXT_SERVER_CHANGED>`

Thông báo được nhận khi :ref:`TextServer<class_TextServer>` thay đổi.

.. _class_Node_constant_NOTIFICATION_APPLICATION_PIP_MODE_ENTERED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_PIP_MODE_ENTERED** = ``2019`` :ref:`🔗<class_Node_constant_NOTIFICATION_APPLICATION_PIP_MODE_ENTERED>`

Thông báo được nhận khi ứng dụng chuyển sang chế độ picture-in-picture.

.. _class_Node_constant_NOTIFICATION_APPLICATION_PIP_MODE_EXITED:

.. rst-class:: classref-constant

**NOTIFICATION_APPLICATION_PIP_MODE_EXITED** = ``2020`` :ref:`🔗<class_Node_constant_NOTIFICATION_APPLICATION_PIP_MODE_EXITED>`

Thông báo được nhận khi ứng dụng thoát khỏi chế độ picture-in-picture.

.. _class_Node_constant_NOTIFICATION_ACCESSIBILITY_UPDATE:

.. rst-class:: classref-constant

**NOTIFICATION_ACCESSIBILITY_UPDATE** = ``3000`` :ref:`🔗<class_Node_constant_NOTIFICATION_ACCESSIBILITY_UPDATE>`

Thông báo được nhận khi cần cập nhật thông tin accessibility.

.. _class_Node_constant_NOTIFICATION_ACCESSIBILITY_INVALIDATE:

.. rst-class:: classref-constant

**NOTIFICATION_ACCESSIBILITY_INVALIDATE** = ``3001`` :ref:`🔗<class_Node_constant_NOTIFICATION_ACCESSIBILITY_INVALIDATE>`

Thông báo được nhận khi các phần tử accessibility bị invalidated. Tất cả phần tử accessibility của node sẽ tự động bị xóa sau khi nhận thông báo này, vì vậy cần loại bỏ mọi reference hiện có đến các phần tử đó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Node_property_auto_translate_mode:

.. rst-class:: classref-property

:ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **auto_translate_mode** = ``0`` :ref:`🔗<class_Node_property_auto_translate_mode>`

.. rst-class:: classref-property-setget

- |void| **set_auto_translate_mode**\ (\ value\: :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>`\ ) - :ref:`AutoTranslateMode<enum_Node_AutoTranslateMode>` **get_auto_translate_mode**\ (\ )

Xác định liệu văn bản có tự động thay đổi thành phiên bản đã dịch tùy theo locale hiện tại hay không (đối với các node như :ref:`Label<class_Label>`, :ref:`RichTextLabel<class_RichTextLabel>`, :ref:`Window<class_Window>`, v.v.). Đồng thời xác định liệu các chuỗi của node có được phân tích để tạo translation template hay không.

\ **Lưu ý:** Đối với root node, auto translate mode cũng có thể được thiết lập thông qua :ref:`ProjectSettings.internationalization/rendering/root_node_auto_translate<class_ProjectSettings_property_internationalization/rendering/root_node_auto_translate>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_editor_description:

.. rst-class:: classref-property

:ref:`String<class_String>` **editor_description** = ``""`` :ref:`🔗<class_Node_property_editor_description>`

.. rst-class:: classref-property-setget

- |void| **set_editor_description**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_editor_description**\ (\ )

Mô tả tùy chọn cho node. Mô tả này sẽ được hiển thị dưới dạng tooltip khi di chuột lên node trong dock Scene của editor.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_multiplayer:

.. rst-class:: classref-property

:ref:`MultiplayerAPI<class_MultiplayerAPI>` **multiplayer** :ref:`🔗<class_Node_property_multiplayer>`

.. rst-class:: classref-property-setget

- :ref:`MultiplayerAPI<class_MultiplayerAPI>` **get_multiplayer**\ (\ )

Instance :ref:`MultiplayerAPI<class_MultiplayerAPI>` được liên kết với node này. Xem :ref:`SceneTree.get_multiplayer()<class_SceneTree_method_get_multiplayer>`.

\ **Lưu ý:** Việc đổi tên node hoặc di chuyển node trong cây sẽ không di chuyển :ref:`MultiplayerAPI<class_MultiplayerAPI>` đến path mới; bạn sẽ phải cập nhật thủ công.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_name:

.. rst-class:: classref-property

:ref:`StringName<class_StringName>` **name** :ref:`🔗<class_Node_property_name>`

.. rst-class:: classref-property-setget

- |void| **set_name**\ (\ value\: :ref:`StringName<class_StringName>`\ ) - :ref:`StringName<class_StringName>` **get_name**\ (\ )

Tên của node. Tên này phải là duy nhất giữa các node cùng cấp (các node con khác của cùng một node cha). Khi được đặt thành tên của một node cùng cấp hiện có, node sẽ tự động được đổi tên.

\ **Lưu ý:** Khi thay đổi tên, các ký tự sau sẽ được thay thế bằng dấu gạch dưới: (``.`` ``:`` ``@`` ``/`` ``"`` ``%``). Đặc biệt, ký tự ``@`` được dành riêng cho các tên tự động tạo. Xem thêm :ref:`String.validate_node_name()<class_String_method_validate_node_name>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_owner:

.. rst-class:: classref-property

:ref:`Node<class_Node>` **owner** :ref:`🔗<class_Node_property_owner>`

.. rst-class:: classref-property-setget

- |void| **set_owner**\ (\ value\: :ref:`Node<class_Node>`\ ) - :ref:`Node<class_Node>` **get_owner**\ (\ )

Owner của node này. Owner phải là ancestor của node này. Khi đóng gói node owner trong một :ref:`PackedScene<class_PackedScene>`, tất cả các node mà nó sở hữu cũng được lưu cùng. Xem thêm :ref:`unique_name_in_owner<class_Node_property_unique_name_in_owner>`.

\ **Lưu ý:** Trong editor, các node không thuộc sở hữu của scene root thường không được hiển thị trong dock Scene và **sẽ không** được lưu. Để tránh điều này, hãy nhớ đặt owner sau khi gọi :ref:`add_child()<class_Node_method_add_child>`.

\ **Lưu ý:** Owner cần phải là scene root hiện tại. Xem `Instancing scenes <../tutorials/plugins/running_code_in_the_editor.html#instancing-scenes>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_physics_interpolation_mode:

.. rst-class:: classref-property

:ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` **physics_interpolation_mode** = ``0`` :ref:`🔗<class_Node_property_physics_interpolation_mode>`

.. rst-class:: classref-property-setget

- |void| **set_physics_interpolation_mode**\ (\ value\: :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>`\ ) - :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` **get_physics_interpolation_mode**\ (\ )

Chế độ nội suy physics được sử dụng cho node này. Chỉ có hiệu lực nếu :ref:`ProjectSettings.physics/common/physics_interpolation<class_ProjectSettings_property_physics/common/physics_interpolation>` hoặc :ref:`SceneTree.physics_interpolation<class_SceneTree_property_physics_interpolation>` là ``true``.

Theo mặc định, các node kế thừa chế độ nội suy physics từ node cha. Property này có thể bật hoặc tắt nội suy physics riêng cho từng node, bất kể chế độ nội suy physics của node cha.

\ **Lưu ý:** Một số loại node như :ref:`VehicleWheel3D<class_VehicleWheel3D>` mặc định tắt nội suy physics vì chúng dựa vào giải pháp tùy chỉnh riêng.

\ **Lưu ý:** Khi dịch chuyển node đến một vị trí xa, bạn nên tạm thời tắt nội suy bằng :ref:`reset_physics_interpolation()<class_Node_method_reset_physics_interpolation>` *sau khi* di chuyển node. Điều này tránh tạo ra vệt hình ảnh giữa vị trí cũ và mới.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_process_mode:

.. rst-class:: classref-property

:ref:`ProcessMode<enum_Node_ProcessMode>` **process_mode** = ``0`` :ref:`🔗<class_Node_property_process_mode>`

.. rst-class:: classref-property-setget

- |void| **set_process_mode**\ (\ value\: :ref:`ProcessMode<enum_Node_ProcessMode>`\ ) - :ref:`ProcessMode<enum_Node_ProcessMode>` **get_process_mode**\ (\ )

Hành vi xử lý của node. Để kiểm tra node có thể xử lý ở mode hiện tại hay không, hãy sử dụng :ref:`can_process()<class_Node_method_can_process>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_process_physics_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **process_physics_priority** = ``0`` :ref:`🔗<class_Node_property_process_physics_priority>`

.. rst-class:: classref-property-setget

- |void| **set_physics_process_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_physics_process_priority**\ (\ )

Tương tự như :ref:`process_priority<class_Node_property_process_priority>` nhưng dành cho :ref:`NOTIFICATION_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>`, :ref:`_physics_process()<class_Node_private_method__physics_process>` hoặc :ref:`NOTIFICATION_INTERNAL_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_process_priority:

.. rst-class:: classref-property

:ref:`int<class_int>` **process_priority** = ``0`` :ref:`🔗<class_Node_property_process_priority>`

.. rst-class:: classref-property-setget

- |void| **set_process_priority**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_process_priority**\ (\ )

Thứ tự thực thi các process callback của node (:ref:`_process()<class_Node_private_method__process>`, :ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>` và :ref:`NOTIFICATION_INTERNAL_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PROCESS>`). Các node có giá trị priority *thấp hơn* sẽ gọi process callback trước, bất kể thứ tự trong cây.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_process_thread_group:

.. rst-class:: classref-property

:ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>` **process_thread_group** = ``0`` :ref:`🔗<class_Node_property_process_thread_group>`

.. rst-class:: classref-property-setget

- |void| **set_process_thread_group**\ (\ value\: :ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>`\ ) - :ref:`ProcessThreadGroup<enum_Node_ProcessThreadGroup>` **get_process_thread_group**\ (\ )

Thiết lập process thread group cho node này (về cơ bản là xác định node nhận :ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>`, :ref:`NOTIFICATION_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>`, :ref:`_process()<class_Node_private_method__process>` hoặc :ref:`_physics_process()<class_Node_private_method__physics_process>` (và các phiên bản nội bộ) trên main thread hay trong sub-thread).

Theo mặc định, thread group là :ref:`PROCESS_THREAD_GROUP_INHERIT<class_Node_constant_PROCESS_THREAD_GROUP_INHERIT>`, nghĩa là node này thuộc cùng thread group với node cha. Các thread group có nghĩa là các node trong một thread group cụ thể sẽ được xử lý cùng nhau, tách biệt với các thread group khác (tùy thuộc vào :ref:`process_thread_group_order<class_Node_property_process_thread_group_order>`). Nếu giá trị được đặt thành :ref:`PROCESS_THREAD_GROUP_SUB_THREAD<class_Node_constant_PROCESS_THREAD_GROUP_SUB_THREAD>`, thread group này sẽ chạy trên một sub-thread (không phải main thread); ngược lại, nếu được đặt thành :ref:`PROCESS_THREAD_GROUP_MAIN_THREAD<class_Node_constant_PROCESS_THREAD_GROUP_MAIN_THREAD>`, nó sẽ được xử lý trên main thread. Nếu không có node cha hoặc ông được đặt thành giá trị khác inherit, node sẽ thuộc về *default thread group*. Group mặc định này sẽ được xử lý trên main thread và có thứ tự group là 0.

Trong quá trình xử lý trên sub-thread, việc truy cập hầu hết các function trong những node nằm ngoài thread group là bị cấm (và sẽ gây lỗi trong debug mode). Hãy sử dụng :ref:`Object.call_deferred()<class_Object_method_call_deferred>`, :ref:`call_thread_safe()<class_Node_method_call_thread_safe>`, :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>` và các thành phần tương tự để giao tiếp từ các thread group với main thread (hoặc với các thread group khác).

Để hiểu rõ hơn về process thread group, có thể hình dung rằng bất kỳ node nào được đặt thành giá trị khác :ref:`PROCESS_THREAD_GROUP_INHERIT<class_Node_constant_PROCESS_THREAD_GROUP_INHERIT>` sẽ bao gồm mọi node con (và node cháu) được đặt thành inherit vào process thread group của nó. Điều này có nghĩa là tất cả node trong group sẽ được xử lý cùng nhau, tại cùng thời điểm với node bao gồm chúng.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_process_thread_group_order:

.. rst-class:: classref-property

:ref:`int<class_int>` **process_thread_group_order** :ref:`🔗<class_Node_property_process_thread_group_order>`

.. rst-class:: classref-property-setget

- |void| **set_process_thread_group_order**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_process_thread_group_order**\ (\ )

Thay đổi thứ tự của process thread group. Các group có thứ tự nhỏ hơn sẽ được xử lý trước các group có thứ tự lớn hơn. Điều này hữu ích khi một số lượng lớn node được xử lý trong sub-thread, sau đó một group khác muốn thu thập kết quả của chúng trên main thread, chẳng hạn.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_process_thread_messages:

.. rst-class:: classref-property

|bitfield|\[:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>`\] **process_thread_messages** :ref:`🔗<class_Node_property_process_thread_messages>`

.. rst-class:: classref-property-setget

- |void| **set_process_thread_messages**\ (\ value\: |bitfield|\[:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>`\]\ ) - |bitfield|\[:ref:`ProcessThreadMessages<enum_Node_ProcessThreadMessages>`\] **get_process_thread_messages**\ (\ )

Thiết lập việc thread group hiện tại có xử lý message hay không (các lệnh gọi đến :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>` trên các thread), và liệu nó có muốn nhận chúng trong các process callback thông thường hay physics process callback.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_scene_file_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **scene_file_path** :ref:`🔗<class_Node_property_scene_file_path>`

.. rst-class:: classref-property-setget

- |void| **set_scene_file_path**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_scene_file_path**\ (\ )

File path của scene gốc, nếu node được instantiate từ một file :ref:`PackedScene<class_PackedScene>`. Chỉ các scene root node mới chứa giá trị này.

.. rst-class:: classref-item-separator

----

.. _class_Node_property_unique_name_in_owner:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **unique_name_in_owner** = ``false`` :ref:`🔗<class_Node_property_unique_name_in_owner>`

.. rst-class:: classref-property-setget

- |void| **set_unique_name_in_owner**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_unique_name_in_owner**\ (\ )

Nếu ``true``, node có thể được truy cập từ bất kỳ node nào dùng chung :ref:`owner<class_Node_property_owner>` hoặc từ chính :ref:`owner<class_Node_property_owner>`, bằng cú pháp ``%Name`` đặc biệt trong :ref:`get_node()<class_Node_method_get_node>`.

\ **Lưu ý:** Nếu một node khác có cùng :ref:`owner<class_Node_property_owner>` dùng chung :ref:`name<class_Node_property_name>` với node này, node kia sẽ không còn có thể được truy cập dưới dạng unique.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các method
----------------

.. _class_Node_private_method__enter_tree:

.. rst-class:: classref-method

|void| **_enter_tree**\ (\ ) |virtual| :ref:`🔗<class_Node_private_method__enter_tree>`

Được gọi khi node đi vào :ref:`SceneTree<class_SceneTree>` (ví dụ: khi instantiate, thay đổi scene hoặc sau khi gọi :ref:`add_child()<class_Node_method_add_child>` trong script). Nếu node có node con, callback :ref:`_enter_tree()<class_Node_private_method__enter_tree>` của nó sẽ được gọi trước, sau đó mới đến callback của các node con.

Tương ứng với notification :ref:`NOTIFICATION_ENTER_TREE<class_Node_constant_NOTIFICATION_ENTER_TREE>` trong :ref:`Object._notification()<class_Object_private_method__notification>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__exit_tree:

.. rst-class:: classref-method

|void| **_exit_tree**\ (\ ) |virtual| :ref:`🔗<class_Node_private_method__exit_tree>`

Được gọi khi node sắp rời khỏi :ref:`SceneTree<class_SceneTree>` (ví dụ: khi được giải phóng, thay đổi scene hoặc sau khi gọi :ref:`remove_child()<class_Node_method_remove_child>` trong script). Nếu node có node con, callback :ref:`_exit_tree()<class_Node_private_method__exit_tree>` của nó sẽ được gọi sau cùng, sau khi tất cả node con đã rời khỏi tree.

Tương ứng với notification :ref:`NOTIFICATION_EXIT_TREE<class_Node_constant_NOTIFICATION_EXIT_TREE>` trong :ref:`Object._notification()<class_Object_private_method__notification>` và signal :ref:`tree_exiting<class_Node_signal_tree_exiting>`. Để nhận thông báo khi node đã rời khỏi active tree, hãy kết nối với :ref:`tree_exited<class_Node_signal_tree_exited>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__get_accessibility_configuration_warnings:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_accessibility_configuration_warnings**\ (\ ) |virtual| |const| :ref:`🔗<class_Node_private_method__get_accessibility_configuration_warnings>`

Các phần tử trong mảng được trả về từ phương thức này sẽ được hiển thị dưới dạng cảnh báo trong Scene dock nếu script ghi đè phương thức này là script ``tool`` và các cảnh báo accessibility được bật trong phần cài đặt của editor.

Trả về một mảng rỗng sẽ không tạo ra cảnh báo nào.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__get_configuration_warnings:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_configuration_warnings**\ (\ ) |virtual| |const| :ref:`🔗<class_Node_private_method__get_configuration_warnings>`

Các phần tử trong mảng được trả về từ phương thức này sẽ được hiển thị dưới dạng cảnh báo trong Scene dock nếu script ghi đè phương thức này là script ``tool``.

Trả về một mảng rỗng sẽ không tạo ra cảnh báo nào.

Gọi :ref:`update_configuration_warnings()<class_Node_method_update_configuration_warnings>` khi cần cập nhật các cảnh báo cho node này.

::

    @export var energy = 0:
        set(value):
            energy = value
            update_configuration_warnings()

    func _get_configuration_warnings():
        if energy < 0:
            return ["Energy must be 0 or greater."]
        else:
            return []

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__get_focused_accessibility_element:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **_get_focused_accessibility_element**\ (\ ) |virtual| |const| :ref:`🔗<class_Node_private_method__get_focused_accessibility_element>`

Được gọi trong quá trình cập nhật thông tin accessibility để xác định sub-element hiện đang được focus; phương thức này phải trả về một sub-element RID hoặc giá trị được trả về bởi :ref:`get_accessibility_element()<class_Node_method_get_accessibility_element>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__input:

.. rst-class:: classref-method

|void| **_input**\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual| :ref:`🔗<class_Node_private_method__input>`

Được gọi khi có một input event. Input event sẽ lan truyền lên qua cây node cho đến khi một node xử lý nó.

Phương thức này chỉ được gọi nếu input processing được bật; việc này được thực hiện tự động khi phương thức này được ghi đè và có thể được chuyển đổi bằng :ref:`set_process_input()<class_Node_method_set_process_input>`.

Để xử lý input event và ngăn không cho nó tiếp tục lan truyền đến các node khác, có thể gọi :ref:`Viewport.set_input_as_handled()<class_Viewport_method_set_input_as_handled>`.

Đối với gameplay input, :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>` và :ref:`_unhandled_key_input()<class_Node_private_method__unhandled_key_input>` thường phù hợp hơn, vì chúng cho phép GUI intercept event trước.

\ **Lưu ý:** Phương thức này chỉ được gọi nếu node hiện diện trong scene tree (tức là không phải orphan).

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__physics_process:

.. rst-class:: classref-method

|void| **_physics_process**\ (\ delta\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_Node_private_method__physics_process>`

Được gọi một lần trong mỗi physics tick và cho phép các Node đồng bộ logic của chúng với các physics tick. ``delta`` là khoảng thời gian logic giữa các physics tick, tính bằng giây, và bằng :ref:`Engine.time_scale<class_Engine_property_time_scale>` / :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`.

Phương thức này chỉ được gọi nếu physics processing được bật cho Node này; việc này được thực hiện tự động khi phương thức này được ghi đè và có thể được chuyển đổi bằng :ref:`set_physics_process()<class_Node_method_set_physics_process>`.

Việc processing diễn ra theo thứ tự của :ref:`process_physics_priority<class_Node_property_process_physics_priority>`; các giá trị priority thấp hơn được gọi trước. Các Node có cùng priority được xử lý theo thứ tự trong tree, hoặc từ trên xuống dưới như hiển thị trong editor (còn gọi là pre-order traversal).

Tương ứng với notification :ref:`NOTIFICATION_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>` trong :ref:`Object._notification()<class_Object_private_method__notification>`.

\ **Lưu ý:** Phương thức này chỉ được gọi nếu node hiện diện trong scene tree (tức là không phải orphan).

\ **Lưu ý:** ``delta`` tích lũy có thể khác với số giây trong thế giới thực.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__process:

.. rst-class:: classref-method

|void| **_process**\ (\ delta\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_Node_private_method__process>`

Được gọi trong mỗi idle frame, trước khi rendering và sau khi các physics tick được xử lý. ``delta`` là khoảng thời gian giữa các frame, tính bằng giây.

Phương thức này chỉ được gọi nếu processing được bật cho Node này; việc này được thực hiện tự động khi phương thức này được ghi đè và có thể được chuyển đổi bằng :ref:`set_process()<class_Node_method_set_process>`.

Việc processing diễn ra theo thứ tự của :ref:`process_priority<class_Node_property_process_priority>`; các giá trị priority thấp hơn được gọi trước. Các Node có cùng priority được xử lý theo thứ tự trong tree, hoặc từ trên xuống dưới như hiển thị trong editor (còn gọi là pre-order traversal).

Tương ứng với notification :ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>` trong :ref:`Object._notification()<class_Object_private_method__notification>`.

\ **Lưu ý:** Phương thức này chỉ được gọi nếu node hiện diện trong scene tree (tức là không phải orphan).

\ **Lưu ý:** Khi engine gặp vấn đề về hiệu năng và frame rate giảm, ``delta`` sẽ tăng. Khi ``delta`` tăng, nó bị giới hạn ở mức tối đa :ref:`Engine.time_scale<class_Engine_property_time_scale>` \* :ref:`Engine.max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` / :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>`. Do đó, ``delta`` tích lũy có thể không thể hiện thời gian thực tế.

\ **Lưu ý:** Khi ``--fixed-fps`` được bật hoặc engine đang chạy ở Movie Maker mode (xem :ref:`MovieWriter<class_MovieWriter>`), process ``delta`` sẽ luôn giống nhau trong mọi frame, bất kể frame đó mất bao lâu để rendering.

\ **Lưu ý:** Frame delta có thể được post-process bởi :ref:`OS.delta_smoothing<class_OS_property_delta_smoothing>` nếu tùy chọn này được bật cho project.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__ready:

.. rst-class:: classref-method

|void| **_ready**\ (\ ) |virtual| :ref:`🔗<class_Node_private_method__ready>`

Được gọi khi node ở trạng thái "ready", tức là khi cả node và các node con của nó đã đi vào scene tree. Nếu node có node con, các callback :ref:`_ready()<class_Node_private_method__ready>` của chúng sẽ được kích hoạt trước, sau đó node cha mới nhận notification ready.

Tương ứng với notification :ref:`NOTIFICATION_READY<class_Node_constant_NOTIFICATION_READY>` trong :ref:`Object._notification()<class_Object_private_method__notification>`. Xem thêm annotation ``@onready`` dành cho các biến.

Thường được dùng để khởi tạo. Để khởi tạo sớm hơn nữa, có thể sử dụng :ref:`Object._init()<class_Object_private_method__init>`. Xem thêm :ref:`_enter_tree()<class_Node_private_method__enter_tree>`.

\ **Lưu ý:** Phương thức này có thể chỉ được gọi một lần cho mỗi node. Sau khi xóa một node khỏi scene tree rồi thêm lại, :ref:`_ready()<class_Node_private_method__ready>` sẽ **không** được gọi lần thứ hai. Có thể bỏ qua hạn chế này bằng cách yêu cầu gọi lại với :ref:`request_ready()<class_Node_method_request_ready>`, phương thức này có thể được gọi ở bất kỳ thời điểm nào trước khi thêm lại node.

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__shortcut_input:

.. rst-class:: classref-method

|void| **_shortcut_input**\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual| :ref:`🔗<class_Node_private_method__shortcut_input>`

Được gọi khi một :ref:`InputEventKey<class_InputEventKey>`, :ref:`InputEventShortcut<class_InputEventShortcut>` hoặc :ref:`InputEventJoypadButton<class_InputEventJoypadButton>` chưa được :ref:`_input()<class_Node_private_method__input>` hoặc bất kỳ GUI :ref:`Control<class_Control>` item nào xử lý. Phương thức này được gọi trước :ref:`_unhandled_key_input()<class_Node_private_method__unhandled_key_input>` và :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>`. Input event sẽ lan truyền lên qua cây node cho đến khi một node xử lý nó.

Phương thức này chỉ được gọi nếu shortcut processing được bật; việc này được thực hiện tự động khi phương thức này được ghi đè và có thể được chuyển đổi bằng :ref:`set_process_shortcut_input()<class_Node_method_set_process_shortcut_input>`.

Để xử lý input event và ngăn không cho nó tiếp tục lan truyền đến các node khác, có thể gọi :ref:`Viewport.set_input_as_handled()<class_Viewport_method_set_input_as_handled>`.

Phương thức này có thể được dùng để xử lý shortcut. Đối với các GUI event nói chung, hãy dùng :ref:`_input()<class_Node_private_method__input>` thay thế. Gameplay event thường nên được xử lý bằng :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>` hoặc :ref:`_unhandled_key_input()<class_Node_private_method__unhandled_key_input>`.

\ **Lưu ý:** Phương thức này chỉ được gọi nếu node hiện diện trong scene tree (tức là không phải orphan).

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__unhandled_input:

.. rst-class:: classref-method

|void| **_unhandled_input**\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual| :ref:`🔗<class_Node_private_method__unhandled_input>`

Được gọi khi một :ref:`InputEvent<class_InputEvent>` chưa được :ref:`_input()<class_Node_private_method__input>` hoặc bất kỳ GUI :ref:`Control<class_Control>` item nào xử lý. Phương thức này được gọi sau :ref:`_shortcut_input()<class_Node_private_method__shortcut_input>` và sau :ref:`_unhandled_key_input()<class_Node_private_method__unhandled_key_input>`. Input event sẽ lan truyền lên qua cây node cho đến khi một node xử lý nó.

Phương thức này chỉ được gọi nếu unhandled input processing được bật; việc này được thực hiện tự động khi phương thức này được ghi đè và có thể được chuyển đổi bằng :ref:`set_process_unhandled_input()<class_Node_method_set_process_unhandled_input>`.

Để xử lý input event và ngăn không cho nó tiếp tục lan truyền đến các node khác, có thể gọi :ref:`Viewport.set_input_as_handled()<class_Viewport_method_set_input_as_handled>`.

Đối với gameplay input, phương thức này thường phù hợp hơn :ref:`_input()<class_Node_private_method__input>`, vì GUI event cần có priority cao hơn. Đối với keyboard shortcut, hãy cân nhắc sử dụng :ref:`_shortcut_input()<class_Node_private_method__shortcut_input>` thay thế, vì nó được gọi trước phương thức này. Cuối cùng, để xử lý keyboard event, hãy cân nhắc sử dụng :ref:`_unhandled_key_input()<class_Node_private_method__unhandled_key_input>` vì lý do hiệu năng.

\ **Lưu ý:** Phương thức này chỉ được gọi nếu node hiện diện trong scene tree (tức là không phải orphan).

.. rst-class:: classref-item-separator

----

.. _class_Node_private_method__unhandled_key_input:

.. rst-class:: classref-method

|void| **_unhandled_key_input**\ (\ event\: :ref:`InputEvent<class_InputEvent>`\ ) |virtual| :ref:`🔗<class_Node_private_method__unhandled_key_input>`

Được gọi khi một :ref:`InputEventKey<class_InputEventKey>` chưa được :ref:`_input()<class_Node_private_method__input>` hoặc bất kỳ GUI :ref:`Control<class_Control>` item nào xử lý. Phương thức này được gọi sau :ref:`_shortcut_input()<class_Node_private_method__shortcut_input>` nhưng trước :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>`. Input event sẽ lan truyền lên qua cây node cho đến khi một node xử lý nó.

Phương thức này chỉ được gọi nếu unhandled key input processing được bật; việc này được thực hiện tự động khi phương thức này được ghi đè và có thể được chuyển đổi bằng :ref:`set_process_unhandled_key_input()<class_Node_method_set_process_unhandled_key_input>`.

Để xử lý input event và ngăn không cho nó tiếp tục lan truyền đến các node khác, có thể gọi :ref:`Viewport.set_input_as_handled()<class_Viewport_method_set_input_as_handled>`.

Phương thức này có thể được dùng để xử lý Unicode character input với các modifier :kbd:`Alt`, :kbd:`Alt + Ctrl` và :kbd:`Alt + Shift`, sau khi các shortcut đã được xử lý.

Đối với gameplay input, phương thức này và :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>` thường phù hợp hơn :ref:`_input()<class_Node_private_method__input>`, vì GUI event nên được xử lý trước. Phương thức này cũng có hiệu năng tốt hơn :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>`, vì các event không liên quan như :ref:`InputEventMouseMotion<class_InputEventMouseMotion>` sẽ được tự động lọc. Đối với shortcut, hãy cân nhắc sử dụng :ref:`_shortcut_input()<class_Node_private_method__shortcut_input>` thay thế.

\ **Lưu ý:** Phương thức này chỉ được gọi nếu node hiện diện trong scene tree (tức là không phải orphan).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_add_child:

.. rst-class:: classref-method

|void| **add_child**\ (\ node\: :ref:`Node<class_Node>`, force_readable_name\: :ref:`bool<class_bool>` = false, internal\: :ref:`InternalMode<enum_Node_InternalMode>` = 0\ ) :ref:`🔗<class_Node_method_add_child>`

Thêm một child ``node``. Các node có thể có bất kỳ số lượng node con nào, nhưng mỗi node con phải có một tên duy nhất. Các node con sẽ tự động bị xóa khi node cha bị xóa, vì vậy có thể xóa toàn bộ scene bằng cách xóa node trên cùng của nó.

Nếu ``force_readable_name`` là ``true``, thì khả năng dễ đọc của ``node`` được thêm vào sẽ được cải thiện. Nếu không được đặt tên, ``node`` sẽ được đổi tên thành kiểu của nó, và nếu nó dùng chung :ref:`name<class_Node_property_name>` với một node cùng cấp, một số sẽ được thêm vào hậu tố theo cách phù hợp hơn. Thao tác này rất chậm. Vì vậy, bạn nên để ``false`` thực hiện việc này; nó sẽ gán một tên tạm có chứa ``@`` trong cả hai trường hợp.

Nếu ``internal`` khác :ref:`INTERNAL_MODE_DISABLED<class_Node_constant_INTERNAL_MODE_DISABLED>`, node con sẽ được thêm dưới dạng internal node. Các node này bị các method như :ref:`get_children()<class_Node_method_get_children>` bỏ qua, trừ khi tham số ``include_internal`` của chúng là ``true``. Điều này cũng ngăn các node này bị nhân bản cùng với node cha. Mục đích là ẩn các internal node khỏi người dùng, để người dùng không vô tình xóa hoặc chỉnh sửa chúng. Được một số GUI node sử dụng, chẳng hạn như :ref:`ColorPicker<class_ColorPicker>`.

\ **Lưu ý:** Nếu ``node`` đã có node cha, method này sẽ thất bại. Trước tiên, hãy dùng :ref:`remove_child()<class_Node_method_remove_child>` để xóa ``node`` khỏi node cha hiện tại. Ví dụ:


.. tabs::

 .. code-tab:: gdscript

    var child_node = get_child(0)
    if child_node.get_parent():
        child_node.get_parent().remove_child(child_node)
    add_child(child_node)

 .. code-tab:: csharp

    Node childNode = GetChild(0);
    if (childNode.GetParent() != null)
    {
        childNode.GetParent().RemoveChild(childNode);
    }
    AddChild(childNode);



Nếu bạn cần thêm node con bên dưới một node cụ thể trong danh sách các node con, hãy dùng :ref:`add_sibling()<class_Node_method_add_sibling>` thay vì method này.

\ **Lưu ý:** Nếu muốn một node con được lưu vào :ref:`PackedScene<class_PackedScene>`, bạn phải thiết lập :ref:`owner<class_Node_property_owner>` ngoài việc gọi :ref:`add_child()<class_Node_method_add_child>`. Điều này thường liên quan đến :doc:`tool scripts <../tutorials/plugins/running_code_in_the_editor>` và :doc:`editor plugins <../tutorials/plugins/editor/index>`. Nếu gọi :ref:`add_child()<class_Node_method_add_child>` mà không thiết lập :ref:`owner<class_Node_property_owner>`, **Node** mới được thêm sẽ không hiển thị trong scene tree, dù vẫn hiển thị trong chế độ xem 2D/3D.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_add_sibling:

.. rst-class:: classref-method

|void| **add_sibling**\ (\ sibling\: :ref:`Node<class_Node>`, force_readable_name\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node_method_add_sibling>`

Thêm một node ``sibling`` vào node cha của node này và di chuyển sibling được thêm ngay bên dưới node này.

Nếu ``force_readable_name`` là ``true``, thì khả năng dễ đọc của ``sibling`` được thêm vào sẽ được cải thiện. Nếu không được đặt tên, ``sibling`` sẽ được đổi tên thành kiểu của nó, và nếu nó dùng chung :ref:`name<class_Node_property_name>` với một node cùng cấp, một số sẽ được thêm vào hậu tố theo cách phù hợp hơn. Thao tác này rất chậm. Vì vậy, bạn nên để ``false`` thực hiện việc này; nó sẽ gán một tên tạm có chứa ``@`` trong cả hai trường hợp.

Hãy dùng :ref:`add_child()<class_Node_method_add_child>` thay vì method này nếu bạn không cần thêm node con bên dưới một node cụ thể trong danh sách các node con.

\ **Note:** If this node is internal, the added sibling will be internal too (see :ref:`add_child()<class_Node_method_add_child>`'s ``internal`` parameter).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_add_to_group:

.. rst-class:: classref-method

|void| **add_to_group**\ (\ group\: :ref:`StringName<class_StringName>`, persistent\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node_method_add_to_group>`

Thêm node vào ``group``. Group có thể hữu ích để tổ chức một tập hợp con các node, chẳng hạn như ``"enemies"`` hoặc ``"collectables"``. Xem các ghi chú trong phần mô tả và các group method trong :ref:`SceneTree<class_SceneTree>`.

Nếu ``persistent`` là ``true``, group sẽ được lưu khi lưu bên trong :ref:`PackedScene<class_PackedScene>`. Tất cả group được tạo và hiển thị trong Groups dock đều là persistent.

\ **Lưu ý:** Để cải thiện hiệu suất, thứ tự tên group *không* được đảm bảo và có thể thay đổi giữa các lần chạy project. Vì vậy, không nên dựa vào thứ tự của group.

\ **Lưu ý:** Các group method của :ref:`SceneTree<class_SceneTree>` sẽ *không* hoạt động trên node này nếu node không nằm trong tree (xem :ref:`is_inside_tree()<class_Node_method_is_inside_tree>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_atr:

.. rst-class:: classref-method

:ref:`String<class_String>` **atr**\ (\ message\: :ref:`String<class_String>`, context\: :ref:`StringName<class_StringName>` = ""\ ) |const| :ref:`🔗<class_Node_method_atr>`

Dịch một ``message`` bằng các translation catalog được cấu hình trong Project Settings. Có thể chỉ định thêm ``context`` để hỗ trợ việc dịch. Lưu ý rằng hầu hết các :ref:`Control<class_Control>` node đều tự động dịch chuỗi của chúng, vì vậy method này chủ yếu hữu ích cho các chuỗi được định dạng hoặc văn bản tự vẽ.

Method này hoạt động giống :ref:`Object.tr()<class_Object_method_tr>`, đồng thời tôn trọng trạng thái :ref:`auto_translate_mode<class_Node_property_auto_translate_mode>`.

Nếu :ref:`Object.can_translate_messages()<class_Object_method_can_translate_messages>` là ``false``, hoặc không có bản dịch, method này trả về ``message`` mà không thay đổi. Xem :ref:`Object.set_message_translation()<class_Object_method_set_message_translation>`.

Để xem các ví dụ chi tiết, hãy xem :doc:`Internationalizing games <../tutorials/i18n/internationalizing_games>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_atr_n:

.. rst-class:: classref-method

:ref:`String<class_String>` **atr_n**\ (\ message\: :ref:`String<class_String>`, plural_message\: :ref:`StringName<class_StringName>`, n\: :ref:`int<class_int>`, context\: :ref:`StringName<class_StringName>` = ""\ ) |const| :ref:`🔗<class_Node_method_atr_n>`

Dịch một ``message`` hoặc ``plural_message`` bằng các translation catalog được cấu hình trong Project Settings. Có thể chỉ định thêm ``context`` để hỗ trợ việc dịch.

Method này hoạt động giống :ref:`Object.tr_n()<class_Object_method_tr_n>`, đồng thời tôn trọng trạng thái :ref:`auto_translate_mode<class_Node_property_auto_translate_mode>`.

Nếu :ref:`Object.can_translate_messages()<class_Object_method_can_translate_messages>` là ``false``, hoặc không có bản dịch, method này trả về ``message`` hoặc ``plural_message`` mà không thay đổi. Xem :ref:`Object.set_message_translation()<class_Object_method_set_message_translation>`.

``n`` là số lượng của chủ thể trong message. Nó được hệ thống dịch sử dụng để lấy dạng số nhiều chính xác cho ngôn ngữ hiện tại.

Để xem các ví dụ chi tiết, hãy xem :doc:`Localization using gettext <../tutorials/i18n/localization_using_gettext>`.

\ **Lưu ý:** Số âm và số :ref:`float<class_float>` có thể không được áp dụng chính xác cho một số chủ thể có thể đếm được. Bạn nên xử lý các trường hợp này bằng :ref:`atr()<class_Node_method_atr>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_call_deferred_thread_group:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **call_deferred_thread_group**\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Node_method_call_deferred_thread_group>`

Hàm này tương tự :ref:`Object.call_deferred()<class_Object_method_call_deferred>`, ngoại trừ việc lệnh gọi sẽ diễn ra khi node thread group được xử lý. Nếu node thread group được xử lý trong sub-thread, lệnh gọi sẽ được thực hiện trên thread đó, ngay trước khi :ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>` hoặc :ref:`NOTIFICATION_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>`, tức :ref:`_process()<class_Node_private_method__process>` hoặc :ref:`_physics_process()<class_Node_private_method__physics_process>` hay các phiên bản internal của chúng được gọi.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_call_thread_safe:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **call_thread_safe**\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Node_method_call_thread_safe>`

Hàm này đảm bảo việc gọi hàm sẽ thành công, bất kể được thực hiện từ một thread hay không. Nếu được gọi từ một thread không được phép gọi hàm, lệnh gọi sẽ trở thành deferred. Nếu không, lệnh gọi sẽ được thực hiện trực tiếp.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_can_auto_translate:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_auto_translate**\ (\ ) |const| :ref:`🔗<class_Node_method_can_auto_translate>`

Trả về ``true`` nếu node này có thể tự động dịch các message tùy thuộc vào locale hiện tại. Xem :ref:`auto_translate_mode<class_Node_property_auto_translate_mode>`, :ref:`atr()<class_Node_method_atr>` và :ref:`atr_n()<class_Node_method_atr_n>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_can_process:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_process**\ (\ ) |const| :ref:`🔗<class_Node_method_can_process>`

Trả về ``true`` nếu node có thể nhận các thông báo xử lý và input callback (:ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>`, :ref:`_input()<class_Node_private_method__input>`, v.v.) từ :ref:`SceneTree<class_SceneTree>` và :ref:`Viewport<class_Viewport>`. Giá trị trả về phụ thuộc vào :ref:`process_mode<class_Node_property_process_mode>`:

- Nếu được đặt thành :ref:`PROCESS_MODE_PAUSABLE<class_Node_constant_PROCESS_MODE_PAUSABLE>`, trả về ``true`` khi game đang được xử lý, tức là :ref:`SceneTree.paused<class_SceneTree_property_paused>` là ``false``;

- Nếu được đặt thành :ref:`PROCESS_MODE_WHEN_PAUSED<class_Node_constant_PROCESS_MODE_WHEN_PAUSED>`, trả về ``true`` khi game bị tạm dừng, tức là :ref:`SceneTree.paused<class_SceneTree_property_paused>` là ``true``;

- Nếu được đặt thành :ref:`PROCESS_MODE_ALWAYS<class_Node_constant_PROCESS_MODE_ALWAYS>`, luôn trả về ``true``;

- Nếu được đặt thành :ref:`PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, luôn trả về ``false``;

- Nếu được đặt thành :ref:`PROCESS_MODE_INHERIT<class_Node_constant_PROCESS_MODE_INHERIT>`, sử dụng :ref:`process_mode<class_Node_property_process_mode>` của node cha để xác định kết quả.

Nếu node không nằm trong tree, trả về ``false`` bất kể giá trị của :ref:`process_mode<class_Node_property_process_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_create_tween:

.. rst-class:: classref-method

:ref:`Tween<class_Tween>` **create_tween**\ (\ ) :ref:`🔗<class_Node_method_create_tween>`

Tạo một :ref:`Tween<class_Tween>` mới và bind nó vào node này.

Tương đương với việc thực hiện:


.. tabs::

 .. code-tab:: gdscript

    get_tree().create_tween().bind_node(self)

 .. code-tab:: csharp

    GetTree().CreateTween().BindNode(this);



Tween sẽ tự động bắt đầu ở process frame hoặc physics frame tiếp theo (tùy thuộc vào :ref:`TweenProcessMode<enum_Tween_TweenProcessMode>`). Xem :ref:`Tween.bind_node()<class_Tween_method_bind_node>` để biết thêm thông tin về các Tween được bind vào node.

\ **Lưu ý:** Method này vẫn có thể được sử dụng khi node không nằm trong :ref:`SceneTree<class_SceneTree>`. Nó có thể thất bại trong trường hợp hiếm gặp khi sử dụng :ref:`MainLoop<class_MainLoop>` tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_duplicate:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **duplicate**\ (\ flags\: :ref:`int<class_int>` = 15\ ) |const| :ref:`🔗<class_Node_method_duplicate>`

Nhân bản node, trả về một node mới với tất cả thuộc tính, signal, group và node con được sao chép đệ quy từ node ban đầu. Có thể điều chỉnh hành vi thông qua ``flags`` (xem :ref:`DuplicateFlags<enum_Node_DuplicateFlags>`). Các internal node không được nhân bản.

\ **Lưu ý:** Đối với các node có :ref:`Script<class_Script>` được gắn vào, nếu :ref:`Object._init()<class_Object_private_method__init>` được định nghĩa với các tham số bắt buộc, node được nhân bản sẽ không có :ref:`Script<class_Script>`.

\ **Lưu ý:** Theo mặc định, method này chỉ nhân bản các thuộc tính được đánh dấu để serialization (tức là sử dụng :ref:`@GlobalScope.PROPERTY_USAGE_STORAGE<class_@GlobalScope_constant_PROPERTY_USAGE_STORAGE>`, hoặc trong GDScript là :ref:`@GDScript.@export<class_@GDScript_annotation_@export>`). Nếu muốn nhân bản tất cả thuộc tính, hãy sử dụng :ref:`DUPLICATE_INTERNAL_STATE<class_Node_constant_DUPLICATE_INTERNAL_STATE>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_find_child:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **find_child**\ (\ pattern\: :ref:`String<class_String>`, recursive\: :ref:`bool<class_bool>` = true, owned\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Node_method_find_child>`

Tìm hậu duệ đầu tiên của node này có :ref:`name<class_Node_property_name>` khớp với ``pattern``, trả về ``null`` nếu không tìm thấy kết quả khớp. Việc khớp được thực hiện trên tên node, *không phải* đường dẫn của chúng, thông qua :ref:`String.match()<class_String_method_match>`. Do đó, việc khớp phân biệt chữ hoa chữ thường, ``"*"`` khớp với không hoặc nhiều ký tự, còn ``"?"`` khớp với bất kỳ ký tự đơn nào.

Nếu ``recursive`` là ``false``, chỉ các node con trực tiếp của node này được kiểm tra. Các node được kiểm tra theo thứ tự cây, vì vậy node con trực tiếp đầu tiên của node này được kiểm tra trước, sau đó đến các node con trực tiếp của chính nó, v.v., rồi mới chuyển sang node con trực tiếp thứ hai, và tiếp tục như vậy. Các node con nội bộ cũng được đưa vào tìm kiếm (xem tham số ``internal`` trong :ref:`add_child()<class_Node_method_add_child>`).

Nếu ``owned`` là ``true``, chỉ các hậu duệ có node :ref:`owner<class_Node_property_owner>` hợp lệ mới được kiểm tra.

\ **Lưu ý:** Phương thức này có thể rất chậm. Hãy cân nhắc lưu tham chiếu đến node được tìm thấy vào một biến. Ngoài ra, hãy sử dụng :ref:`get_node()<class_Node_method_get_node>` với các tên duy nhất (xem :ref:`unique_name_in_owner<class_Node_property_unique_name_in_owner>`).

\ **Lưu ý:** Để tìm tất cả node hậu duệ khớp với một mẫu hoặc một kiểu class, hãy xem :ref:`find_children()<class_Node_method_find_children>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_find_children:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] **find_children**\ (\ pattern\: :ref:`String<class_String>`, type\: :ref:`String<class_String>` = "", recursive\: :ref:`bool<class_bool>` = true, owned\: :ref:`bool<class_bool>` = true\ ) |const| :ref:`🔗<class_Node_method_find_children>`

Tìm tất cả hậu duệ của node này có tên khớp với ``pattern``, trả về một :ref:`Array<class_Array>` rỗng nếu không tìm thấy kết quả khớp. Việc khớp được thực hiện trên tên node, *không phải* đường dẫn của chúng, thông qua :ref:`String.match()<class_String_method_match>`. Do đó, việc khớp phân biệt chữ hoa chữ thường, ``"*"`` khớp với không hoặc nhiều ký tự, còn ``"?"`` khớp với bất kỳ ký tự đơn nào.

Nếu ``type`` không rỗng, chỉ các hậu duệ kế thừa từ ``type`` mới được đưa vào (xem :ref:`Object.is_class()<class_Object_method_is_class>`).

Nếu ``recursive`` là ``false``, chỉ các node con trực tiếp của node này được kiểm tra. Các node được kiểm tra theo thứ tự cây, vì vậy node con trực tiếp đầu tiên của node này được kiểm tra trước, sau đó đến các node con trực tiếp của chính nó, v.v., rồi mới chuyển sang node con trực tiếp thứ hai, và tiếp tục như vậy. Các node con nội bộ cũng được đưa vào tìm kiếm (xem tham số ``internal`` trong :ref:`add_child()<class_Node_method_add_child>`).

Nếu ``owned`` là ``true``, chỉ các hậu duệ có node :ref:`owner<class_Node_property_owner>` hợp lệ mới được kiểm tra.

\ **Lưu ý:** Phương thức này có thể rất chậm. Hãy cân nhắc lưu các tham chiếu đến những node được tìm thấy vào một biến.

\ **Lưu ý:** Để tìm một node hậu duệ duy nhất khớp với một mẫu, hãy xem :ref:`find_child()<class_Node_method_find_child>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_find_parent:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **find_parent**\ (\ pattern\: :ref:`String<class_String>`\ ) |const| :ref:`🔗<class_Node_method_find_parent>`

Tìm tổ tiên đầu tiên của node này có :ref:`name<class_Node_property_name>` khớp với ``pattern``, trả về ``null`` nếu không tìm thấy kết quả khớp. Việc khớp được thực hiện thông qua :ref:`String.match()<class_String_method_match>`. Do đó, việc khớp phân biệt chữ hoa chữ thường, ``"*"`` khớp với không hoặc nhiều ký tự, còn ``"?"`` khớp với bất kỳ ký tự đơn nào. Xem thêm :ref:`find_child()<class_Node_method_find_child>` và :ref:`find_children()<class_Node_method_find_children>`.

\ **Lưu ý:** Vì phương thức này di chuyển lên trên trong scene tree, nó có thể chậm khi các node lớn và lồng nhau sâu. Hãy cân nhắc lưu tham chiếu đến node được tìm thấy vào một biến. Ngoài ra, hãy sử dụng :ref:`get_node()<class_Node_method_get_node>` với các tên duy nhất (xem :ref:`unique_name_in_owner<class_Node_property_unique_name_in_owner>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_accessibility_element:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_accessibility_element**\ (\ ) |const| :ref:`🔗<class_Node_method_get_accessibility_element>`

Trả về RID của accessibility element chính.

\ **Lưu ý:** Phương thức này chỉ nên được gọi trong khi cập nhật thông tin accessibility (:ref:`NOTIFICATION_ACCESSIBILITY_UPDATE<class_Node_constant_NOTIFICATION_ACCESSIBILITY_UPDATE>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_child:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **get_child**\ (\ idx\: :ref:`int<class_int>`, include_internal\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Node_method_get_child>`

Lấy node con theo chỉ mục của nó. Mỗi node con có một chỉ mục tương đối với các node cùng cấp (xem :ref:`get_index()<class_Node_method_get_index>`). Node con đầu tiên có chỉ mục là 0. Bạn cũng có thể sử dụng các giá trị âm để bắt đầu từ cuối danh sách. Có thể dùng phương thức này kết hợp với :ref:`get_child_count()<class_Node_method_get_child_count>` để lặp qua các node con của node này. Nếu không có node con nào tại chỉ mục đã cho, phương thức này trả về ``null`` và phát sinh lỗi.

If ``include_internal`` is ``false``, internal children are ignored (see :ref:`add_child()<class_Node_method_add_child>`'s ``internal`` parameter).

::

    # Giả sử các node sau đây là các node con của node này, theo thứ tự:
    # First, Middle, Last.

    var a = get_child(0).name  # a là "First"
    var b = get_child(1).name  # b là "Middle"
    var b = get_child(2).name  # b là "Last"
    var c = get_child(-1).name # c là "Last"

\ **Lưu ý:** Để lấy một node theo :ref:`NodePath<class_NodePath>`, hãy sử dụng :ref:`get_node()<class_Node_method_get_node>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_child_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_child_count**\ (\ include_internal\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Node_method_get_child_count>`

Trả về số lượng node con của node này.

If ``include_internal`` is ``false``, internal children are not counted (see :ref:`add_child()<class_Node_method_add_child>`'s ``internal`` parameter).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_children:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node<class_Node>`\] **get_children**\ (\ include_internal\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Node_method_get_children>`

Trả về tất cả node con của node này bên trong một :ref:`Array<class_Array>`.

If ``include_internal`` is ``false``, excludes internal children from the returned array (see :ref:`add_child()<class_Node_method_add_child>`'s ``internal`` parameter).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_groups:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_groups**\ (\ ) |const| :ref:`🔗<class_Node_method_get_groups>`

Trả về một :ref:`Array<class_Array>` gồm tên các group mà node đã được thêm vào.

\ **Lưu ý:** Để cải thiện hiệu năng, thứ tự của tên group *không* được đảm bảo và có thể thay đổi giữa các lần chạy project. Do đó, không được phụ thuộc vào thứ tự group.

\ **Lưu ý:** Phương thức này cũng có thể trả về một số tên group bắt đầu bằng dấu gạch dưới (``_``). Đây là các group được engine sử dụng nội bộ. Để tránh xung đột, không sử dụng các group tùy chỉnh bắt đầu bằng dấu gạch dưới. Để loại trừ các group nội bộ, hãy xem đoạn code sau:


.. tabs::

 .. code-tab:: gdscript

    # Chỉ lưu các group không nội bộ của node (dưới dạng một array các StringNames).
    var non_internal_groups = []
    for group in get_groups():
        if not str(group).begins_with("_"):
            non_internal_groups.push_back(group)

 .. code-tab:: csharp

    // Chỉ lưu các group không nội bộ của node (dưới dạng một List các StringNames).
    List<string> nonInternalGroups = new List<string>();
    foreach (string group in GetGroups())
    {
        if (!group.BeginsWith("_"))
            nonInternalGroups.Add(group);
    }



.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_index**\ (\ include_internal\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Node_method_get_index>`

Trả về thứ tự của node này trong số các node cùng cấp. Chỉ mục của node đầu tiên là ``0``. Xem thêm :ref:`get_child()<class_Node_method_get_child>`.

If ``include_internal`` is ``false``, returns the index ignoring internal children. The first, non-internal child will have an index of ``0`` (see :ref:`add_child()<class_Node_method_add_child>`'s ``internal`` parameter).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_last_exclusive_window:

.. rst-class:: classref-method

:ref:`Window<class_Window>` **get_last_exclusive_window**\ (\ ) |const| :ref:`🔗<class_Node_method_get_last_exclusive_window>`

Trả về :ref:`Window<class_Window>` chứa node này, hoặc child độc quyền cuối cùng trong một chuỗi window bắt đầu từ window chứa node này.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_multiplayer_authority:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_multiplayer_authority**\ (\ ) |const| :ref:`🔗<class_Node_method_get_multiplayer_authority>`

Trả về peer ID của multiplayer authority của node này. Xem :ref:`set_multiplayer_authority()<class_Node_method_set_multiplayer_authority>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_node:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **get_node**\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const| :ref:`🔗<class_Node_method_get_node>`

Lấy một node. :ref:`NodePath<class_NodePath>` có thể là đường dẫn tương đối (từ node này) hoặc đường dẫn tuyệt đối (từ :ref:`SceneTree.root<class_SceneTree_property_root>`) đến một node. Nếu ``path`` không trỏ đến một node hợp lệ, phương thức sẽ phát sinh lỗi và trả về ``null``. Việc cố gắng truy cập các method trên giá trị trả về sẽ gây ra lỗi *"Attempt to call <method> on a null instance."*.

\ **Lưu ý:** Việc lấy node bằng đường dẫn tuyệt đối chỉ hoạt động khi node nằm trong scene tree (xem :ref:`is_inside_tree()<class_Node_method_is_inside_tree>`).

\ **Ví dụ:** Giả sử phương thức này được gọi từ node Character, bên trong cây sau:

.. code:: text

     ┖╴root
        ┠╴Character (you are here!)
        ┃  ┠╴Sword
        ┃  ┖╴Backpack
        ┃     ┖╴Dagger
        ┠╴MyGame
        ┖╴Swamp
           ┠╴Alligator
           ┠╴Mosquito
           ┖╴Goblin

Các lệnh gọi sau sẽ trả về một node hợp lệ:


.. tabs::

 .. code-tab:: gdscript

    get_node("Sword")
    get_node("Backpack/Dagger")
    get_node("../Swamp/Alligator")
    get_node("/root/MyGame")

 .. code-tab:: csharp

    GetNode("Sword");
    GetNode("Backpack/Dagger");
    GetNode("../Swamp/Alligator");
    GetNode("/root/MyGame");



.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_node_and_resource:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_node_and_resource**\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) :ref:`🔗<class_Node_method_get_node_and_resource>`

Lấy một node và resource lồng sâu nhất của nó như được chỉ định bởi subname của :ref:`NodePath<class_NodePath>`. Trả về một :ref:`Array<class_Array>` có kích thước ``3``, trong đó:

- Element ``0`` là **Node**, hoặc ``null`` nếu không tìm thấy;

- Element ``1`` là :ref:`Resource<class_Resource>` lồng sâu nhất cuối cùng của subname, hoặc ``null`` nếu không tìm thấy;

- Element ``2`` là :ref:`NodePath<class_NodePath>` còn lại, tham chiếu đến một property hiện có và không phải :ref:`Resource<class_Resource>` (xem :ref:`Object.get_indexed()<class_Object_method_get_indexed>`).

\ **Ví dụ:** Giả sử :ref:`Sprite2D.texture<class_Sprite2D_property_texture>` của node con đã được gán một :ref:`AtlasTexture<class_AtlasTexture>`:


.. tabs::

 .. code-tab:: gdscript

    var a = get_node_and_resource("Area2D/Sprite2D")
    print(a[0].name) # In ra Sprite2D
    print(a[1])      # In ra <null>
    print(a[2])      # In ra ^""

    var b = get_node_and_resource("Area2D/Sprite2D:texture:atlas")
    print(b[0].name)        # In ra Sprite2D
    print(b[1].get_class()) # In ra AtlasTexture
    print(b[2])             # In ra ^""

    var c = get_node_and_resource("Area2D/Sprite2D:texture:atlas:region")
    print(c[0].name)        # In ra Sprite2D
    print(c[1].get_class()) # In ra AtlasTexture
    print(c[2])             # In ra ^":region"

 .. code-tab:: csharp

    var a = GetNodeAndResource(NodePath("Area2D/Sprite2D"));
    GD.Print(a[0].Name); // In ra Sprite2D
    GD.Print(a[1]);      // In ra <null>
    GD.Print(a[2]);      // In ra ^"

    var b = GetNodeAndResource(NodePath("Area2D/Sprite2D:texture:atlas"));
    GD.Print(b[0].name);        // In ra Sprite2D
    GD.Print(b[1].get_class()); // In ra AtlasTexture
    GD.Print(b[2]);             // In ra ^""

    var c = GetNodeAndResource(NodePath("Area2D/Sprite2D:texture:atlas:region"));
    GD.Print(c[0].name);        // In ra Sprite2D
    GD.Print(c[1].get_class()); // In ra AtlasTexture
    GD.Print(c[2]);             // In ra ^":region"



.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_node_or_null:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **get_node_or_null**\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const| :ref:`🔗<class_Node_method_get_node_or_null>`

Lấy một node theo :ref:`NodePath<class_NodePath>`. Tương tự :ref:`get_node()<class_Node_method_get_node>`, nhưng không tạo lỗi nếu ``path`` không trỏ đến một node hợp lệ.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_node_rpc_config:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_node_rpc_config**\ (\ ) |const| :ref:`🔗<class_Node_method_get_node_rpc_config>`

Trả về một :ref:`Dictionary<class_Dictionary>` ánh xạ tên phương thức với cấu hình RPC được định nghĩa cho node này bằng :ref:`rpc_config()<class_Node_method_rpc_config>`.

\ **Lưu ý:** Phương thức này chỉ trả về cấu hình RPC được gán qua :ref:`rpc_config()<class_Node_method_rpc_config>`. Xem :ref:`Script.get_rpc_config()<class_Script_method_get_rpc_config>` để lấy các RPC được định nghĩa bởi :ref:`Script<class_Script>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_orphan_node_ids:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`int<class_int>`\] **get_orphan_node_ids**\ (\ ) |static| :ref:`🔗<class_Node_method_get_orphan_node_ids>`

Trả về ID đối tượng của tất cả node mồ côi (các node nằm ngoài :ref:`SceneTree<class_SceneTree>`). Dùng cho mục đích debug.

\ **Lưu ý:** :ref:`get_orphan_node_ids()<class_Node_method_get_orphan_node_ids>` chỉ hoạt động trong các bản build debug. Khi được gọi trong một project được export ở chế độ release, :ref:`get_orphan_node_ids()<class_Node_method_get_orphan_node_ids>` sẽ trả về một mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_parent:

.. rst-class:: classref-method

:ref:`Node<class_Node>` **get_parent**\ (\ ) |const| :ref:`🔗<class_Node_method_get_parent>`

Trả về node cha của node này, hoặc ``null`` nếu node không có node cha.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_path:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_path**\ (\ ) |const| :ref:`🔗<class_Node_method_get_path>`

Trả về path tuyệt đối của node, tương đối so với :ref:`SceneTree.root<class_SceneTree_property_root>`. Nếu node không nằm trong scene tree, phương thức này sẽ thất bại và trả về một :ref:`NodePath<class_NodePath>` rỗng.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_path_to:

.. rst-class:: classref-method

:ref:`NodePath<class_NodePath>` **get_path_to**\ (\ node\: :ref:`Node<class_Node>`, use_unique_path\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Node_method_get_path_to>`

Trả về :ref:`NodePath<class_NodePath>` tương đối từ node này đến ``node`` được chỉ định. Cả hai node phải nằm trong cùng một :ref:`SceneTree<class_SceneTree>` hoặc hệ thống phân cấp scene; nếu không, phương thức này sẽ thất bại và trả về một :ref:`NodePath<class_NodePath>` rỗng.

Nếu ``use_unique_path`` là ``true``, trả về path ngắn nhất có tính đến tên duy nhất của node này (xem :ref:`unique_name_in_owner<class_Node_property_unique_name_in_owner>`).

\ **Lưu ý:** Nếu bạn lấy một path tương đối bắt đầu từ một node duy nhất, path này có thể dài hơn path tương đối thông thường do được thêm tên của node duy nhất.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_physics_process_delta_time:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_physics_process_delta_time**\ (\ ) |const| :ref:`🔗<class_Node_method_get_physics_process_delta_time>`

Returns the time elapsed (in seconds) since the last physics callback. This value is identical to :ref:`_physics_process()<class_Node_private_method__physics_process>`'s ``delta`` parameter, and is often consistent at run-time, unless :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` is changed. See also :ref:`NOTIFICATION_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>`.

\ **Lưu ý:** Giá trị trả về sẽ lớn hơn dự kiến nếu chạy ở framerate thấp hơn :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` / :ref:`Engine.max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` FPS. Điều này nhằm tránh các tình huống "spiral of death", trong đó hiệu năng giảm mạnh do số lượng physics step trên mỗi frame liên tục tăng. Hành vi này ảnh hưởng đến cả :ref:`_process()<class_Node_private_method__process>` và :ref:`_physics_process()<class_Node_private_method__physics_process>`. Vì vậy, tránh sử dụng ``delta`` để đo thời gian theo số giây thực tế. Thay vào đó, hãy sử dụng các phương thức của singleton :ref:`Time<class_Time>` cho mục đích này, chẳng hạn như :ref:`Time.get_ticks_usec()<class_Time_method_get_ticks_usec>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_process_delta_time:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_process_delta_time**\ (\ ) |const| :ref:`🔗<class_Node_method_get_process_delta_time>`

Returns the time elapsed (in seconds) since the last process callback. This value is identical to :ref:`_process()<class_Node_private_method__process>`'s ``delta`` parameter, and may vary from frame to frame. See also :ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>`.

\ **Lưu ý:** Giá trị trả về sẽ lớn hơn dự kiến nếu chạy ở framerate thấp hơn :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` / :ref:`Engine.max_physics_steps_per_frame<class_Engine_property_max_physics_steps_per_frame>` FPS. Điều này nhằm tránh các tình huống "spiral of death", trong đó hiệu năng giảm mạnh do số lượng physics step trên mỗi frame liên tục tăng. Hành vi này ảnh hưởng đến cả :ref:`_process()<class_Node_private_method__process>` và :ref:`_physics_process()<class_Node_private_method__physics_process>`. Vì vậy, tránh sử dụng ``delta`` để đo thời gian theo số giây thực tế. Thay vào đó, hãy sử dụng các phương thức của singleton :ref:`Time<class_Time>` cho mục đích này, chẳng hạn như :ref:`Time.get_ticks_usec()<class_Time_method_get_ticks_usec>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_scene_instance_load_placeholder:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_scene_instance_load_placeholder**\ (\ ) |const| :ref:`🔗<class_Node_method_get_scene_instance_load_placeholder>`

Trả về ``true`` nếu node này là placeholder tải instance. Xem :ref:`InstancePlaceholder<class_InstancePlaceholder>` và :ref:`set_scene_instance_load_placeholder()<class_Node_method_set_scene_instance_load_placeholder>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_tree:

.. rst-class:: classref-method

:ref:`SceneTree<class_SceneTree>` **get_tree**\ (\ ) |const| :ref:`🔗<class_Node_method_get_tree>`

Trả về :ref:`SceneTree<class_SceneTree>` chứa node này. Nếu node này không nằm trong tree, sẽ tạo lỗi và trả về ``null``. Xem thêm :ref:`is_inside_tree()<class_Node_method_is_inside_tree>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_tree_string:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_tree_string**\ (\ ) :ref:`🔗<class_Node_method_get_tree_string>`

Trả về tree dưới dạng :ref:`String<class_String>`. Chủ yếu được dùng cho mục đích debug. Phiên bản này hiển thị path tương đối so với node hiện tại và phù hợp để sao chép/dán vào hàm :ref:`get_node()<class_Node_method_get_node>`. Nó cũng có thể được sử dụng trong UI/UX của game.

Ví dụ, có thể in ra:

.. code:: text

    TheGame
    TheGame/Menu
    TheGame/Menu/Label
    TheGame/Menu/Camera2D
    TheGame/SplashScreen
    TheGame/SplashScreen/Camera2D

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_tree_string_pretty:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_tree_string_pretty**\ (\ ) :ref:`🔗<class_Node_method_get_tree_string_pretty>`

Tương tự :ref:`get_tree_string()<class_Node_method_get_tree_string>`, phương thức này trả về tree dưới dạng :ref:`String<class_String>`. Phiên bản này hiển thị biểu diễn trực quan hơn, tương tự nội dung được hiển thị trong Scene Dock. Nó hữu ích khi kiểm tra các tree lớn hơn.

Ví dụ, có thể in ra:

.. code:: text

     ┖╴TheGame
        ┠╴Menu
        ┃  ┠╴Label
        ┃  ┖╴Camera2D
        ┖╴SplashScreen
           ┖╴Camera2D

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_viewport:

.. rst-class:: classref-method

:ref:`Viewport<class_Viewport>` **get_viewport**\ (\ ) |const| :ref:`🔗<class_Node_method_get_viewport>`

Trả về ancestor :ref:`Viewport<class_Viewport>` gần nhất của node nếu node nằm trong tree. Nếu không, trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_get_window:

.. rst-class:: classref-method

:ref:`Window<class_Window>` **get_window**\ (\ ) |const| :ref:`🔗<class_Node_method_get_window>`

Trả về :ref:`Window<class_Window>` chứa node này. Nếu node nằm trong cửa sổ chính, điều này tương đương với việc lấy node gốc (``get_tree().get_root()``).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_has_node:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_node**\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const| :ref:`🔗<class_Node_method_has_node>`

Trả về ``true`` nếu ``path`` trỏ đến một node hợp lệ. Xem thêm :ref:`get_node()<class_Node_method_get_node>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_has_node_and_resource:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_node_and_resource**\ (\ path\: :ref:`NodePath<class_NodePath>`\ ) |const| :ref:`🔗<class_Node_method_has_node_and_resource>`

Trả về ``true`` nếu ``path`` trỏ đến một node hợp lệ và các subname của node đó trỏ đến một :ref:`Resource<class_Resource>` hợp lệ, ví dụ ``Area2D/CollisionShape2D:shape``. Các property không thuộc kiểu :ref:`Resource<class_Resource>` (chẳng hạn như node hoặc các kiểu :ref:`Variant<class_Variant>` khác) sẽ không được xét đến. Xem thêm :ref:`get_node_and_resource()<class_Node_method_get_node_and_resource>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_ancestor_of:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_ancestor_of**\ (\ node\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Node_method_is_ancestor_of>`

Trả về ``true`` nếu ``node`` đã cho là child trực tiếp hoặc gián tiếp của node này.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_displayed_folded:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_displayed_folded**\ (\ ) |const| :ref:`🔗<class_Node_method_is_displayed_folded>`

Trả về ``true`` nếu node đang được fold (thu gọn) trong Scene dock. Phương thức này dành cho editor plugin và tool. Xem thêm :ref:`set_display_folded()<class_Node_method_set_display_folded>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_editable_instance:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_editable_instance**\ (\ node\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Node_method_is_editable_instance>`

Trả về ``true`` nếu ``node`` đã bật các child có thể chỉnh sửa đối với node này. Phương thức này dành cho editor plugin và tool. Xem thêm :ref:`set_editable_instance()<class_Node_method_set_editable_instance>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_greater_than:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_greater_than**\ (\ node\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Node_method_is_greater_than>`

Trả về ``true`` nếu ``node`` đã cho xuất hiện sau node này trong hệ thống phân cấp scene. Node xuất hiện sau thường được process sau cùng.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_in_group:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_in_group**\ (\ group\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Node_method_is_in_group>`

Trả về ``true`` nếu node này đã được thêm vào ``group`` đã cho. Xem :ref:`add_to_group()<class_Node_method_add_to_group>` và :ref:`remove_from_group()<class_Node_method_remove_from_group>`. Xem thêm các lưu ý trong phần mô tả và các phương thức group của :ref:`SceneTree<class_SceneTree>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_inside_tree:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_inside_tree**\ (\ ) |const| :ref:`🔗<class_Node_method_is_inside_tree>`

Trả về ``true`` nếu node này hiện đang nằm trong :ref:`SceneTree<class_SceneTree>`. Xem thêm :ref:`get_tree()<class_Node_method_get_tree>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_multiplayer_authority:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_multiplayer_authority**\ (\ ) |const| :ref:`🔗<class_Node_method_is_multiplayer_authority>`

Trả về ``true`` nếu hệ thống cục bộ là multiplayer authority của node này.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_node_ready:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_node_ready**\ (\ ) |const| :ref:`🔗<class_Node_method_is_node_ready>`

Trả về ``true`` nếu node đã sẵn sàng, tức là node đang nằm trong scene tree và tất cả child của node đã được khởi tạo.

\ :ref:`request_ready()<class_Node_method_request_ready>` đặt lại nó về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_part_of_edited_scene:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_part_of_edited_scene**\ (\ ) |const| :ref:`🔗<class_Node_method_is_part_of_edited_scene>`

Trả về ``true`` nếu node là một phần của scene hiện đang mở trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_physics_interpolated:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_physics_interpolated**\ (\ ) |const| :ref:`🔗<class_Node_method_is_physics_interpolated>`

Trả về ``true`` nếu nội suy physics được bật cho node này (xem :ref:`physics_interpolation_mode<class_Node_property_physics_interpolation_mode>`).

\ **Lưu ý:** Nội suy chỉ hoạt động nếu cả cờ này được đặt **và** nội suy physics được bật trong :ref:`SceneTree<class_SceneTree>`. Có thể kiểm tra điều này bằng :ref:`is_physics_interpolated_and_enabled()<class_Node_method_is_physics_interpolated_and_enabled>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_physics_interpolated_and_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_physics_interpolated_and_enabled**\ (\ ) |const| :ref:`🔗<class_Node_method_is_physics_interpolated_and_enabled>`

Trả về ``true`` nếu nội suy physics được bật (xem :ref:`physics_interpolation_mode<class_Node_property_physics_interpolation_mode>`) **và** được bật trong :ref:`SceneTree<class_SceneTree>`.

Đây là phiên bản tiện lợi của :ref:`is_physics_interpolated()<class_Node_method_is_physics_interpolated>`, đồng thời kiểm tra xem nội suy physics có được bật trên toàn cục hay không.

Xem :ref:`SceneTree.physics_interpolation<class_SceneTree_property_physics_interpolation>` và :ref:`ProjectSettings.physics/common/physics_interpolation<class_ProjectSettings_property_physics/common/physics_interpolation>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_physics_processing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_physics_processing**\ (\ ) |const| :ref:`🔗<class_Node_method_is_physics_processing>`

Trả về ``true`` nếu xử lý physics được bật (xem :ref:`set_physics_process()<class_Node_method_set_physics_process>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_physics_processing_internal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_physics_processing_internal**\ (\ ) |const| :ref:`🔗<class_Node_method_is_physics_processing_internal>`

Trả về ``true`` nếu xử lý physics nội bộ được bật (xem :ref:`set_physics_process_internal()<class_Node_method_set_physics_process_internal>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_processing:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_processing**\ (\ ) |const| :ref:`🔗<class_Node_method_is_processing>`

Trả về ``true`` nếu quá trình xử lý được bật (xem :ref:`set_process()<class_Node_method_set_process>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_processing_input:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_processing_input**\ (\ ) |const| :ref:`🔗<class_Node_method_is_processing_input>`

Trả về ``true`` nếu node đang xử lý input (xem :ref:`set_process_input()<class_Node_method_set_process_input>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_processing_internal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_processing_internal**\ (\ ) |const| :ref:`🔗<class_Node_method_is_processing_internal>`

Trả về ``true`` nếu xử lý nội bộ được bật (xem :ref:`set_process_internal()<class_Node_method_set_process_internal>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_processing_shortcut_input:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_processing_shortcut_input**\ (\ ) |const| :ref:`🔗<class_Node_method_is_processing_shortcut_input>`

Trả về ``true`` nếu node đang xử lý các shortcut (xem :ref:`set_process_shortcut_input()<class_Node_method_set_process_shortcut_input>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_processing_unhandled_input:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_processing_unhandled_input**\ (\ ) |const| :ref:`🔗<class_Node_method_is_processing_unhandled_input>`

Trả về ``true`` nếu node đang xử lý input chưa được xử lý (xem :ref:`set_process_unhandled_input()<class_Node_method_set_process_unhandled_input>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_is_processing_unhandled_key_input:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_processing_unhandled_key_input**\ (\ ) |const| :ref:`🔗<class_Node_method_is_processing_unhandled_key_input>`

Trả về ``true`` nếu node đang xử lý key input chưa được xử lý (xem :ref:`set_process_unhandled_key_input()<class_Node_method_set_process_unhandled_key_input>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_move_child:

.. rst-class:: classref-method

|void| **move_child**\ (\ child_node\: :ref:`Node<class_Node>`, to_index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Node_method_move_child>`

Di chuyển ``child_node`` đến index đã cho. Index của một node là thứ tự của node đó trong số các node cùng cấp. Nếu ``to_index`` là số âm, index được tính từ cuối danh sách. Xem thêm :ref:`get_child()<class_Node_method_get_child>` và :ref:`get_index()<class_Node_method_get_index>`.

\ **Lưu ý:** Thứ tự xử lý của một số callback của engine (:ref:`_ready()<class_Node_private_method__ready>`, :ref:`_process()<class_Node_private_method__process>`, v.v.) và các notification được gửi qua :ref:`propagate_notification()<class_Node_method_propagate_notification>` bị ảnh hưởng bởi thứ tự trong tree. Các node :ref:`CanvasItem<class_CanvasItem>` cũng được render theo thứ tự trong tree. Xem thêm :ref:`process_priority<class_Node_property_process_priority>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_notify_deferred_thread_group:

.. rst-class:: classref-method

|void| **notify_deferred_thread_group**\ (\ what\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Node_method_notify_deferred_thread_group>`

Tương tự :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>`, nhưng dành cho các notification.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_notify_thread_safe:

.. rst-class:: classref-method

|void| **notify_thread_safe**\ (\ what\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Node_method_notify_thread_safe>`

Tương tự :ref:`call_thread_safe()<class_Node_method_call_thread_safe>`, nhưng dành cho các notification.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_print_orphan_nodes:

.. rst-class:: classref-method

|void| **print_orphan_nodes**\ (\ ) |static| :ref:`🔗<class_Node_method_print_orphan_nodes>`

In tất cả các node mồ côi (các node nằm ngoài :ref:`SceneTree<class_SceneTree>`). Hữu ích khi debug.

\ **Lưu ý:** Phương thức này chỉ hoạt động trong các bản build debug. Nó không thực hiện gì trong project được export ở chế độ release.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_print_tree:

.. rst-class:: classref-method

|void| **print_tree**\ (\ ) :ref:`🔗<class_Node_method_print_tree>`

In node và các node con của nó ra console theo cách đệ quy. Node không cần phải nằm trong tree. Phương thức này xuất :ref:`NodePath<class_NodePath>`\ s tương đối với node này và phù hợp để sao chép/dán vào :ref:`get_node()<class_Node_method_get_node>`. Xem thêm :ref:`print_tree_pretty()<class_Node_method_print_tree_pretty>`.

Có thể in, ví dụ như:

.. code:: text

    .
    Menu
    Menu/Label
    Menu/Camera2D
    SplashScreen
    SplashScreen/Camera2D

.. rst-class:: classref-item-separator

----

.. _class_Node_method_print_tree_pretty:

.. rst-class:: classref-method

|void| **print_tree_pretty**\ (\ ) :ref:`🔗<class_Node_method_print_tree_pretty>`

In node và các node con của nó ra console theo cách đệ quy. Node không cần phải nằm trong tree. Tương tự :ref:`print_tree()<class_Node_method_print_tree>`, nhưng biểu diễn đồ họa có hình thức giống như nội dung hiển thị trong Scene dock của editor. Hữu ích khi kiểm tra các tree lớn hơn.

Có thể in, ví dụ như:

.. code:: text

     ┖╴TheGame
        ┠╴Menu
        ┃  ┠╴Label
        ┃  ┖╴Camera2D
        ┖╴SplashScreen
           ┖╴Camera2D

.. rst-class:: classref-item-separator

----

.. _class_Node_method_propagate_call:

.. rst-class:: classref-method

|void| **propagate_call**\ (\ method\: :ref:`StringName<class_StringName>`, args\: :ref:`Array<class_Array>` = [], parent_first\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node_method_propagate_call>`

Gọi tên ``method`` đã cho, truyền ``args`` làm các đối số, trên node này và tất cả các node con của nó theo cách đệ quy.

Nếu ``parent_first`` là ``true``, phương thức được gọi trên node này trước, sau đó trên tất cả các node con của nó. Nếu ``false``, các phương thức của node con được gọi trước.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_propagate_notification:

.. rst-class:: classref-method

|void| **propagate_notification**\ (\ what\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Node_method_propagate_notification>`

Gọi :ref:`Object.notification()<class_Object_method_notification>` với ``what`` trên node này và tất cả các node con của nó theo cách đệ quy.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_queue_accessibility_update:

.. rst-class:: classref-method

|void| **queue_accessibility_update**\ (\ ) :ref:`🔗<class_Node_method_queue_accessibility_update>`

Đưa một bản cập nhật thông tin accessibility vào hàng đợi cho node này.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_queue_free:

.. rst-class:: classref-method

|void| **queue_free**\ (\ ) :ref:`🔗<class_Node_method_queue_free>`

Đưa node này vào hàng đợi để xóa ở cuối frame hiện tại. Khi bị xóa, tất cả các node con của nó cũng bị xóa, đồng thời mọi tham chiếu đến node và các node con của nó đều trở nên không hợp lệ.

Không giống :ref:`Object.free()<class_Object_method_free>`, node không bị xóa ngay lập tức và vẫn có thể được truy cập trước khi bị xóa. Việc gọi :ref:`queue_free()<class_Node_method_queue_free>` nhiều lần cũng an toàn. Sử dụng :ref:`Object.is_queued_for_deletion()<class_Object_method_is_queued_for_deletion>` để kiểm tra xem node có bị xóa ở cuối frame hay không.

\ **Lưu ý:** Node chỉ được giải phóng sau khi tất cả các deferred call khác hoàn tất. Việc sử dụng phương thức này không phải lúc nào cũng giống với việc gọi :ref:`Object.free()<class_Object_method_free>` thông qua :ref:`Object.call_deferred()<class_Object_method_call_deferred>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_remove_child:

.. rst-class:: classref-method

|void| **remove_child**\ (\ node\: :ref:`Node<class_Node>`\ ) :ref:`🔗<class_Node_method_remove_child>`

Xóa một child ``node``. ``node``, cùng với các node con của nó, **không** bị xóa. Để xóa một node, xem :ref:`queue_free()<class_Node_method_queue_free>`.

\ **Lưu ý:** Khi node này nằm trong tree, phương thức này đặt :ref:`owner<class_Node_property_owner>` của ``node`` bị xóa (hoặc các node con của nó) thành ``null``, nếu :ref:`owner<class_Node_property_owner>` của chúng không còn là ancestor (xem :ref:`is_ancestor_of()<class_Node_method_is_ancestor_of>`).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_remove_from_group:

.. rst-class:: classref-method

|void| **remove_from_group**\ (\ group\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Node_method_remove_from_group>`

Xóa node khỏi ``group`` đã cho. Không làm gì nếu node không nằm trong ``group``. Xem thêm các lưu ý trong phần mô tả và các phương thức group của :ref:`SceneTree<class_SceneTree>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_reparent:

.. rst-class:: classref-method

|void| **reparent**\ (\ new_parent\: :ref:`Node<class_Node>`, keep_global_transform\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_Node_method_reparent>`

Thay đổi parent của **Node** này thành ``new_parent``. Node phải có parent từ trước. :ref:`owner<class_Node_property_owner>` của node được giữ nguyên nếu owner của nó vẫn có thể truy cập được từ vị trí mới (tức là node vẫn là hậu duệ của parent mới sau thao tác này).

Nếu ``keep_global_transform`` là ``true``, global transform của node sẽ được giữ nguyên nếu được hỗ trợ. :ref:`Node2D<class_Node2D>`, :ref:`Node3D<class_Node3D>` và :ref:`Control<class_Control>` hỗ trợ đối số này (nhưng :ref:`Control<class_Control>` chỉ giữ lại position).

\ **Cảnh báo:** Nếu :ref:`ProjectSettings.physics/common/physics_interpolation<class_ProjectSettings_property_physics/common/physics_interpolation>` được bật và việc reparent gây ra thay đổi lớn về global transform, object có thể trông như di chuyển từ vị trí cũ sang vị trí mới trong physics tick tiếp theo. Để tránh điều này, hãy gọi :ref:`reset_physics_interpolation()<class_Node_method_reset_physics_interpolation>` sau khi reparent.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_replace_by:

.. rst-class:: classref-method

|void| **replace_by**\ (\ node\: :ref:`Node<class_Node>`, keep_groups\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node_method_replace_by>`

Thay thế node này bằng ``node`` đã cho. Tất cả các node con của node này được chuyển sang ``node``.

Nếu ``keep_groups`` là ``true``, ``node`` được thêm vào cùng các group mà node bị thay thế đang thuộc về (xem :ref:`add_to_group()<class_Node_method_add_to_group>`).

\ **Cảnh báo:** Node bị thay thế được xóa khỏi tree, nhưng **không** bị xóa. Để tránh rò rỉ bộ nhớ, hãy lưu tham chiếu đến node trong một biến hoặc sử dụng :ref:`Object.free()<class_Object_method_free>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_request_ready:

.. rst-class:: classref-method

|void| **request_ready**\ (\ ) :ref:`🔗<class_Node_method_request_ready>`

Yêu cầu gọi :ref:`_ready()<class_Node_private_method__ready>` lại vào lần tiếp theo node đi vào tree. **Không** gọi :ref:`_ready()<class_Node_private_method__ready>` ngay lập tức.

\ **Lưu ý:** Phương thức này chỉ ảnh hưởng đến node hiện tại. Nếu các node con của node cũng cần yêu cầu ready, phải gọi phương thức này cho từng node con. Khi node và các node con của nó đi vào tree lần nữa, thứ tự của các callback :ref:`_ready()<class_Node_private_method__ready>` sẽ giống như bình thường.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_reset_physics_interpolation:

.. rst-class:: classref-method

|void| **reset_physics_interpolation**\ (\ ) :ref:`🔗<class_Node_method_reset_physics_interpolation>`

Khi physics interpolation đang hoạt động, việc di chuyển một node đến một transform hoàn toàn khác (chẳng hạn như đặt nó trong một level) có thể gây ra lỗi hiển thị rõ ràng khi đối tượng được render đang di chuyển từ vị trí cũ đến vị trí mới trong suốt physics tick.

Có thể ngăn lỗi hiển thị này bằng cách gọi method này; nó sẽ tạm thời vô hiệu hóa interpolation cho đến khi physics tick hoàn tất.

Node và tất cả các node con theo đệ quy sẽ nhận được notification :ref:`NOTIFICATION_RESET_PHYSICS_INTERPOLATION<class_Node_constant_NOTIFICATION_RESET_PHYSICS_INTERPOLATION>`.

\ **Lưu ý:** Nên gọi function này **sau khi** di chuyển node, thay vì trước đó.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_rpc:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **rpc**\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Node_method_rpc>`

Gửi một yêu cầu remote procedure call đến các peer trên network (và cục bộ) cho ``method`` đã cho, đồng thời gửi các đối số bổ sung đến method được gọi bởi RPC. Yêu cầu gọi này sẽ chỉ được các node có cùng :ref:`NodePath<class_NodePath>` nhận, bao gồm cả :ref:`name<class_Node_property_name>` hoàn toàn giống nhau. Hành vi phụ thuộc vào cấu hình RPC của ``method`` đã cho (xem :ref:`rpc_config()<class_Node_method_rpc_config>` và :ref:`@GDScript.@rpc<class_@GDScript_annotation_@rpc>`). Theo mặc định, các method không được exposed cho RPC.

Có thể trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu lời gọi thành công, :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu các đối số được truyền trong ``method`` không khớp, :ref:`@GlobalScope.ERR_UNCONFIGURED<class_@GlobalScope_constant_ERR_UNCONFIGURED>` nếu không thể lấy :ref:`multiplayer<class_Node_property_multiplayer>` của node (chẳng hạn khi node không nằm trong tree), :ref:`@GlobalScope.ERR_CONNECTION_ERROR<class_@GlobalScope_constant_ERR_CONNECTION_ERROR>` nếu không có connection của :ref:`multiplayer<class_Node_property_multiplayer>`.

\ **Lưu ý:** Bạn chỉ có thể sử dụng RPC an toàn trên các client sau khi nhận được signal :ref:`MultiplayerAPI.connected_to_server<class_MultiplayerAPI_signal_connected_to_server>` từ :ref:`MultiplayerAPI<class_MultiplayerAPI>`. Bạn cũng cần theo dõi trạng thái connection, bằng các signal :ref:`MultiplayerAPI<class_MultiplayerAPI>` như :ref:`MultiplayerAPI.server_disconnected<class_MultiplayerAPI_signal_server_disconnected>` hoặc bằng cách kiểm tra (``get_multiplayer().peer.get_connection_status() == CONNECTION_CONNECTED``).

.. rst-class:: classref-item-separator

----

.. _class_Node_method_rpc_config:

.. rst-class:: classref-method

|void| **rpc_config**\ (\ method\: :ref:`StringName<class_StringName>`, config\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Node_method_rpc_config>`

Thay đổi cấu hình RPC cho ``method`` đã cho. ``config`` phải là ``null`` để tắt tính năng (như mặc định), hoặc là một :ref:`Dictionary<class_Dictionary>` chứa các mục sau:

- ``rpc_mode``: xem :ref:`RPCMode<enum_MultiplayerAPI_RPCMode>`;

- ``transfer_mode``: xem :ref:`TransferMode<enum_MultiplayerPeer_TransferMode>`;

- ``call_local``: nếu ``true``, method cũng sẽ được gọi cục bộ;

- ``channel``: một :ref:`int<class_int>` đại diện cho channel dùng để gửi RPC.

\ **Lưu ý:** Trong GDScript, method này tương ứng với annotation :ref:`@GDScript.@rpc<class_@GDScript_annotation_@rpc>`, cùng với các tham số khác nhau được truyền vào (``@rpc(any)``, ``@rpc(authority)``...). Xem thêm tutorial :doc:`multiplayer cấp cao <../tutorials/networking/high_level_multiplayer>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_rpc_id:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **rpc_id**\ (\ peer_id\: :ref:`int<class_int>`, method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Node_method_rpc_id>`

Gửi một :ref:`rpc()<class_Node_method_rpc>` đến một peer cụ thể được xác định bởi ``peer_id`` (xem :ref:`MultiplayerPeer.set_target_peer()<class_MultiplayerPeer_method_set_target_peer>`).

Có thể trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu lời gọi thành công, :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu các đối số được truyền trong ``method`` không khớp, :ref:`@GlobalScope.ERR_UNCONFIGURED<class_@GlobalScope_constant_ERR_UNCONFIGURED>` nếu không thể lấy :ref:`multiplayer<class_Node_property_multiplayer>` của node (chẳng hạn khi node không nằm trong tree), :ref:`@GlobalScope.ERR_CONNECTION_ERROR<class_@GlobalScope_constant_ERR_CONNECTION_ERROR>` nếu không có connection của :ref:`multiplayer<class_Node_property_multiplayer>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_deferred_thread_group:

.. rst-class:: classref-method

|void| **set_deferred_thread_group**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Node_method_set_deferred_thread_group>`

Tương tự như :ref:`call_deferred_thread_group()<class_Node_method_call_deferred_thread_group>`, nhưng dùng để thiết lập các property.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_display_folded:

.. rst-class:: classref-method

|void| **set_display_folded**\ (\ fold\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_display_folded>`

Nếu được đặt thành ``true``, node sẽ hiển thị ở trạng thái thu gọn trong Scene dock. Do đó, tất cả node con của nó sẽ bị ẩn. Method này предназнач dành cho editor plugin và tool, nhưng cũng hoạt động trong các release build. Xem thêm :ref:`is_displayed_folded()<class_Node_method_is_displayed_folded>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_editable_instance:

.. rst-class:: classref-method

|void| **set_editable_instance**\ (\ node\: :ref:`Node<class_Node>`, is_editable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_editable_instance>`

Đặt thành ``true`` để cho phép tất cả node do ``node`` sở hữu được hiển thị và chỉnh sửa trong Scene dock, ngay cả khi :ref:`owner<class_Node_property_owner>` của chúng không phải là scene root. Method này предназнач dành cho editor plugin và tool, nhưng cũng hoạt động trong các release build. Xem thêm :ref:`is_editable_instance()<class_Node_method_is_editable_instance>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_multiplayer_authority:

.. rst-class:: classref-method

|void| **set_multiplayer_authority**\ (\ id\: :ref:`int<class_int>`, recursive\: :ref:`bool<class_bool>` = true\ ) :ref:`🔗<class_Node_method_set_multiplayer_authority>`

Đặt multiplayer authority của node thành peer có peer ``id`` đã cho. Multiplayer authority là peer có quyền kiểm soát node trên network. Mặc định là peer ID 1 (server). Hữu ích khi dùng cùng với :ref:`rpc_config()<class_Node_method_rpc_config>` và :ref:`MultiplayerAPI<class_MultiplayerAPI>`.

Nếu ``recursive`` là ``true``, peer đã cho sẽ được đặt đệ quy làm authority cho tất cả node con của node này.

\ **Cảnh báo:** Việc này **không** tự động replicate authority mới đến các peer khác. Nhà phát triển chịu trách nhiệm thực hiện việc đó. Bạn có thể replicate thông tin về authority mới bằng :ref:`MultiplayerSpawner.spawn_function<class_MultiplayerSpawner_property_spawn_function>`, một RPC hoặc một :ref:`MultiplayerSynchronizer<class_MultiplayerSynchronizer>`. Ngoài ra, authority của node cha **không** được truyền đến các node con mới được thêm.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_physics_process:

.. rst-class:: classref-method

|void| **set_physics_process**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_physics_process>`

Nếu được đặt thành ``true``, tính năng physics processing (fixed framerate) sẽ được bật. Khi một node đang được xử lý, node đó sẽ nhận một :ref:`NOTIFICATION_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_PHYSICS_PROCESS>` theo một khoảng thời gian cố định (thường là 60 FPS, xem :ref:`Engine.physics_ticks_per_second<class_Engine_property_physics_ticks_per_second>` để thay đổi) (và callback :ref:`_physics_process()<class_Node_private_method__physics_process>` sẽ được gọi nếu tồn tại).

\ **Lưu ý:** Nếu :ref:`_physics_process()<class_Node_private_method__physics_process>` bị override, tính năng này sẽ tự động được bật trước khi gọi :ref:`_ready()<class_Node_private_method__ready>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_physics_process_internal:

.. rst-class:: classref-method

|void| **set_physics_process_internal**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_physics_process_internal>`

Nếu được đặt thành ``true``, physics nội bộ cho node này sẽ được bật. Physics processing nội bộ diễn ra tách biệt với các lần gọi :ref:`_physics_process()<class_Node_private_method__physics_process>` thông thường và được một số node sử dụng nội bộ để đảm bảo hoạt động đúng ngay cả khi node bị tạm dừng hoặc physics processing bị tắt đối với scripting (:ref:`set_physics_process()<class_Node_method_set_physics_process>`).

\ **Cảnh báo:** Các node tích hợp sẵn phụ thuộc vào internal processing cho logic nội bộ của chúng. Việc tắt tính năng này không an toàn và có thể dẫn đến hành vi không mong muốn. Hãy sử dụng method này nếu bạn biết mình đang làm gì.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_process:

.. rst-class:: classref-method

|void| **set_process**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_process>`

Nếu được đặt thành ``true``, processing sẽ được bật. Khi một node đang được xử lý, node đó sẽ nhận một :ref:`NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>` trên mỗi frame được vẽ (và callback :ref:`_process()<class_Node_private_method__process>` sẽ được gọi nếu tồn tại).

\ **Lưu ý:** Nếu :ref:`_process()<class_Node_private_method__process>` bị override, tính năng này sẽ tự động được bật trước khi gọi :ref:`_ready()<class_Node_private_method__ready>`.

\ **Lưu ý:** Method này chỉ ảnh hưởng đến callback :ref:`_process()<class_Node_private_method__process>`, tức là không ảnh hưởng đến các callback khác như :ref:`_physics_process()<class_Node_private_method__physics_process>`. Nếu muốn tắt tất cả processing cho node, hãy đặt :ref:`process_mode<class_Node_property_process_mode>` thành :ref:`PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_process_input:

.. rst-class:: classref-method

|void| **set_process_input**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_process_input>`

Nếu được đặt thành ``true``, input processing sẽ được bật.

\ **Lưu ý:** Nếu :ref:`_input()<class_Node_private_method__input>` bị override, tính năng này sẽ tự động được bật trước khi gọi :ref:`_ready()<class_Node_private_method__ready>`. Input processing cũng đã được bật cho các GUI control, chẳng hạn như :ref:`Button<class_Button>` và :ref:`TextEdit<class_TextEdit>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_process_internal:

.. rst-class:: classref-method

|void| **set_process_internal**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_process_internal>`

Nếu được đặt thành ``true``, internal processing cho node này sẽ được bật. Internal processing diễn ra tách biệt với các lần gọi :ref:`_process()<class_Node_private_method__process>` thông thường và được một số node sử dụng nội bộ để đảm bảo hoạt động đúng ngay cả khi node bị tạm dừng hoặc processing bị tắt đối với scripting (:ref:`set_process()<class_Node_method_set_process>`).

\ **Cảnh báo:** Các node tích hợp sẵn phụ thuộc vào internal processing cho logic nội bộ của chúng. Việc tắt tính năng này không an toàn và có thể dẫn đến hành vi không mong muốn. Hãy sử dụng method này nếu bạn biết mình đang làm gì.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_process_shortcut_input:

.. rst-class:: classref-method

|void| **set_process_shortcut_input**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_process_shortcut_input>`

Nếu được đặt thành ``true``, shortcut processing cho node này sẽ được bật.

\ **Lưu ý:** Nếu :ref:`_shortcut_input()<class_Node_private_method__shortcut_input>` bị override, tính năng này sẽ tự động được bật trước khi gọi :ref:`_ready()<class_Node_private_method__ready>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_process_unhandled_input:

.. rst-class:: classref-method

|void| **set_process_unhandled_input**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_process_unhandled_input>`

Nếu được đặt thành ``true``, unhandled input processing sẽ được bật. Node sẽ nhận được tất cả input chưa được xử lý trước đó (thường bởi một :ref:`Control<class_Control>`).

\ **Lưu ý:** Nếu :ref:`_unhandled_input()<class_Node_private_method__unhandled_input>` bị override, tính năng này sẽ tự động được bật trước khi gọi :ref:`_ready()<class_Node_private_method__ready>`. Unhandled input processing cũng đã được bật cho các GUI control, chẳng hạn như :ref:`Button<class_Button>` và :ref:`TextEdit<class_TextEdit>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_process_unhandled_key_input:

.. rst-class:: classref-method

|void| **set_process_unhandled_key_input**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_process_unhandled_key_input>`

Nếu được đặt thành ``true``, unhandled key input processing sẽ được bật.

\ **Lưu ý:** Nếu :ref:`_unhandled_key_input()<class_Node_private_method__unhandled_key_input>` bị ghi đè, tùy chọn này sẽ tự động được bật trước khi :ref:`_ready()<class_Node_private_method__ready>` được gọi.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_scene_instance_load_placeholder:

.. rst-class:: classref-method

|void| **set_scene_instance_load_placeholder**\ (\ load_placeholder\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node_method_set_scene_instance_load_placeholder>`

Nếu được đặt thành ``true``, node sẽ trở thành một :ref:`InstancePlaceholder<class_InstancePlaceholder>` khi được đóng gói và khởi tạo từ một :ref:`PackedScene<class_PackedScene>`. Xem thêm :ref:`get_scene_instance_load_placeholder()<class_Node_method_get_scene_instance_load_placeholder>`.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_thread_safe:

.. rst-class:: classref-method

|void| **set_thread_safe**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Node_method_set_thread_safe>`

Tương tự như :ref:`call_thread_safe()<class_Node_method_call_thread_safe>`, nhưng dùng để thiết lập các thuộc tính.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_set_translation_domain_inherited:

.. rst-class:: classref-method

|void| **set_translation_domain_inherited**\ (\ ) :ref:`🔗<class_Node_method_set_translation_domain_inherited>`

Khiến node này kế thừa translation domain từ node cha. Nếu node này không có node cha, translation domain chính sẽ được sử dụng.

Đây là hành vi mặc định đối với tất cả các node. Việc gọi :ref:`Object.set_translation_domain()<class_Object_method_set_translation_domain>` sẽ vô hiệu hóa hành vi này.

.. rst-class:: classref-item-separator

----

.. _class_Node_method_update_configuration_warnings:

.. rst-class:: classref-method

|void| **update_configuration_warnings**\ (\ ) :ref:`🔗<class_Node_method_update_configuration_warnings>`

Làm mới các cảnh báo được hiển thị cho node này trong Scene dock. Sử dụng :ref:`_get_configuration_warnings()<class_Node_private_method__get_configuration_warnings>` để tùy chỉnh các thông báo cảnh báo cần hiển thị.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
