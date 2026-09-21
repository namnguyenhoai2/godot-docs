:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Object.xml.

.. _class_Object:

Object
======

**Được kế thừa bởi:** :ref:`AccessibilityServer<class_AccessibilityServer>`, :ref:`AudioServer<class_AudioServer>`, :ref:`CameraServer<class_CameraServer>`, :ref:`ClassDB<class_ClassDB>`, :ref:`DisplayServer<class_DisplayServer>`, :ref:`EditorFileSystemDirectory<class_EditorFileSystemDirectory>`, :ref:`EditorInterface<class_EditorInterface>`, :ref:`EditorPaths<class_EditorPaths>`, :ref:`EditorSelection<class_EditorSelection>`, :ref:`EditorUndoRedoManager<class_EditorUndoRedoManager>`, :ref:`EditorVCSInterface<class_EditorVCSInterface>`, :ref:`Engine<class_Engine>`, :ref:`EngineDebugger<class_EngineDebugger>`, :ref:`FramebufferCacheRD<class_FramebufferCacheRD>`, :ref:`GDExtensionManager<class_GDExtensionManager>`, :ref:`Geometry2D<class_Geometry2D>`, :ref:`Geometry3D<class_Geometry3D>`, :ref:`GodotInstance<class_GodotInstance>`, :ref:`Input<class_Input>`, :ref:`InputMap<class_InputMap>`, :ref:`IP<class_IP>`, :ref:`JavaClassWrapper<class_JavaClassWrapper>`, :ref:`JavaScriptBridge<class_JavaScriptBridge>`, :ref:`JNISingleton<class_JNISingleton>`, :ref:`JSONRPC<class_JSONRPC>`, :ref:`MainLoop<class_MainLoop>`, :ref:`Marshalls<class_Marshalls>`, :ref:`MovieWriter<class_MovieWriter>`, :ref:`NativeMenu<class_NativeMenu>`, :ref:`NavigationMeshGenerator<class_NavigationMeshGenerator>`, :ref:`NavigationServer2D<class_NavigationServer2D>`, :ref:`NavigationServer2DManager<class_NavigationServer2DManager>`, :ref:`NavigationServer3D<class_NavigationServer3D>`, :ref:`NavigationServer3DManager<class_NavigationServer3DManager>`, :ref:`Node<class_Node>`, :ref:`OpenXRExtensionWrapper<class_OpenXRExtensionWrapper>`, :ref:`OpenXRInteractionProfileMetadata<class_OpenXRInteractionProfileMetadata>`, :ref:`OS<class_OS>`, :ref:`Performance<class_Performance>`, :ref:`PhysicsDirectBodyState2D<class_PhysicsDirectBodyState2D>`, :ref:`PhysicsDirectBodyState3D<class_PhysicsDirectBodyState3D>`, :ref:`PhysicsDirectSpaceState2D<class_PhysicsDirectSpaceState2D>`, :ref:`PhysicsDirectSpaceState3D<class_PhysicsDirectSpaceState3D>`, :ref:`PhysicsServer2D<class_PhysicsServer2D>`, :ref:`PhysicsServer2DManager<class_PhysicsServer2DManager>`, :ref:`PhysicsServer3D<class_PhysicsServer3D>`, :ref:`PhysicsServer3DManager<class_PhysicsServer3DManager>`, :ref:`PhysicsServer3DRenderingServerHandler<class_PhysicsServer3DRenderingServerHandler>`, :ref:`ProjectSettings<class_ProjectSettings>`, :ref:`RefCounted<class_RefCounted>`, :ref:`RenderData<class_RenderData>`, :ref:`RenderingDevice<class_RenderingDevice>`, :ref:`RenderingServer<class_RenderingServer>`, :ref:`RenderSceneData<class_RenderSceneData>`, :ref:`ResourceLoader<class_ResourceLoader>`, :ref:`ResourceSaver<class_ResourceSaver>`, :ref:`ResourceUID<class_ResourceUID>`, :ref:`ScriptLanguage<class_ScriptLanguage>`, :ref:`ShaderIncludeDB<class_ShaderIncludeDB>`, :ref:`TextServerManager<class_TextServerManager>`, :ref:`ThemeDB<class_ThemeDB>`, :ref:`TileData<class_TileData>`, :ref:`Time<class_Time>`, :ref:`TranslationServer<class_TranslationServer>`, :ref:`TreeItem<class_TreeItem>`, :ref:`UndoRedo<class_UndoRedo>`, :ref:`UniformSetCacheRD<class_UniformSetCacheRD>`, :ref:`WorkerThreadPool<class_WorkerThreadPool>`, :ref:`XRServer<class_XRServer>`, :ref:`XRVRS<class_XRVRS>`

Lớp cơ sở cho tất cả các lớp khác trong engine.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một kiểu :ref:`Variant<class_Variant>` nâng cao. Tất cả các lớp trong engine đều kế thừa từ Object. Mỗi lớp có thể định nghĩa các thuộc tính, phương thức hoặc signal mới, và các thành phần này sẽ khả dụng cho tất cả các lớp kế thừa. Ví dụ, một instance :ref:`Sprite2D<class_Sprite2D>` có thể gọi :ref:`Node.add_child()<class_Node_method_add_child>` vì nó kế thừa từ :ref:`Node<class_Node>`.

Bạn có thể tạo các instance mới bằng cách sử dụng ``Object.new()`` trong GDScript hoặc ``new GodotObject`` trong C#.

Để xóa một instance Object, hãy gọi :ref:`free()<class_Object_method_free>`. Điều này cần thiết đối với hầu hết các lớp kế thừa Object, vì chúng không tự quản lý bộ nhớ và nếu không sẽ gây rò rỉ bộ nhớ khi không còn được sử dụng. Có một số lớp thực hiện quản lý bộ nhớ. Ví dụ, :ref:`RefCounted<class_RefCounted>` (và :ref:`Resource<class_Resource>` theo đó) sẽ tự xóa khi không còn được tham chiếu, còn :ref:`Node<class_Node>` sẽ xóa các lớp con của nó khi được giải phóng.

Các Object có thể được gắn một :ref:`Script<class_Script>`. Sau khi :ref:`Script<class_Script>` được khởi tạo, nó thực chất hoạt động như một phần mở rộng của lớp cơ sở, cho phép định nghĩa và kế thừa các thuộc tính, phương thức và signal mới.

Bên trong một :ref:`Script<class_Script>`, :ref:`_get_property_list()<class_Object_private_method__get_property_list>` có thể được ghi đè để tùy chỉnh các thuộc tính theo nhiều cách. Nhờ đó, chúng có thể khả dụng trong editor, hiển thị dưới dạng danh sách tùy chọn, được chia thành các nhóm, lưu trên đĩa, v.v. Các ngôn ngữ scripting cung cấp những cách dễ dàng hơn để tùy chỉnh thuộc tính, chẳng hạn như annotation :ref:`@GDScript.@export<class_@GDScript_annotation_@export>`.

Godot rất dynamic. Script của một Object, và do đó cả các thuộc tính, phương thức và signal của nó, có thể được thay đổi trong lúc chạy (run-time). Vì vậy, đôi khi có thể xảy ra trường hợp, chẳng hạn, một thuộc tính mà một phương thức yêu cầu lại không tồn tại. Để ngăn lỗi run-time, hãy xem các phương thức như :ref:`set()<class_Object_method_set>`, :ref:`get()<class_Object_method_get>`, :ref:`call()<class_Object_method_call>`, :ref:`has_method()<class_Object_method_has_method>`, :ref:`has_signal()<class_Object_method_has_signal>`, v.v. Lưu ý rằng các phương thức này **chậm hơn rất nhiều** so với tham chiếu trực tiếp.

Trong GDScript, bạn cũng có thể kiểm tra xem tên của một thuộc tính, phương thức hoặc signal đã cho có tồn tại trong một Object bằng toán tử ``in`` hay không:

::

    var node = Node.new()
    print("name" in node)         # In ra true
    print("get_parent" in node)   # In ra true
    print("tree_entered" in node) # In ra true
    print("unknown" in node)      # In ra false

Notifications là các hằng số :ref:`int<class_int>` thường được các Object gửi và nhận. Ví dụ, trong mỗi frame được render, :ref:`SceneTree<class_SceneTree>` thông báo cho các node bên trong tree bằng một :ref:`Node.NOTIFICATION_PROCESS<class_Node_constant_NOTIFICATION_PROCESS>`. Các node nhận thông báo này và có thể gọi :ref:`Node._process()<class_Node_private_method__process>` để cập nhật. Để sử dụng notifications, hãy xem :ref:`notification()<class_Object_method_notification>` và :ref:`_notification()<class_Object_private_method__notification>`.

Cuối cùng, mọi Object cũng có thể chứa metadata (dữ liệu về dữ liệu). :ref:`set_meta()<class_Object_method_set_meta>` có thể hữu ích để lưu trữ thông tin mà bản thân Object không phụ thuộc vào. Để giữ cho code gọn gàng, không nên lạm dụng metadata.

\ **Lưu ý:** Không giống như các tham chiếu đến một :ref:`RefCounted<class_RefCounted>`, các tham chiếu đến một Object được lưu trong biến có thể trở nên không hợp lệ mà không được đặt thành ``null``. Để kiểm tra xem một Object đã bị xóa hay chưa, *không* so sánh nó với ``null``. Thay vào đó, hãy sử dụng :ref:`@GlobalScope.is_instance_valid()<class_@GlobalScope_method_is_instance_valid>`. Bạn cũng nên kế thừa từ :ref:`RefCounted<class_RefCounted>` đối với các lớp lưu trữ dữ liệu thay vì **Object**.

\ **Lưu ý:** ``script`` không được expose như hầu hết các thuộc tính. Để đặt hoặc lấy :ref:`Script<class_Script>` của một Object trong code, lần lượt sử dụng :ref:`set_script()<class_Object_method_set_script>` và :ref:`get_script()<class_Object_method_get_script>`.

\ **Lưu ý:** Trong ngữ cảnh boolean, một **Object** sẽ được đánh giá là ``false`` nếu nó bằng ``null`` hoặc đã được giải phóng. Nếu không, một **Object** sẽ luôn được đánh giá là ``true``. Xem thêm :ref:`@GlobalScope.is_instance_valid()<class_@GlobalScope_method_is_instance_valid>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Giới thiệu về lớp Object <../engine_details/architecture/object_class>`

- :doc:`Khi nào và làm thế nào để tránh sử dụng node cho mọi thứ <../tutorials/best_practices/node_alternatives>`

- :doc:`Notifications của Object <../tutorials/best_practices/godot_notifications>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`_get<class_Object_private_method__get>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |virtual|                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`_get_property_list<class_Object_private_method__get_property_list>`\ (\ ) |virtual|                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_init<class_Object_private_method__init>`\ (\ ) |virtual|                                                                                                                                                                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`_iter_get<class_Object_private_method__iter_get>`\ (\ iter\: :ref:`Variant<class_Variant>`\ ) |virtual|                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_iter_init<class_Object_private_method__iter_init>`\ (\ iter\: :ref:`Array<class_Array>`\ ) |virtual|                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_iter_next<class_Object_private_method__iter_next>`\ (\ iter\: :ref:`Array<class_Array>`\ ) |virtual|                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_notification<class_Object_private_method__notification>`\ (\ what\: :ref:`int<class_int>`\ ) |virtual|                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_property_can_revert<class_Object_private_method__property_can_revert>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |virtual|                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`_property_get_revert<class_Object_private_method__property_get_revert>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |virtual|                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`_set<class_Object_private_method__set>`\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) |virtual|                                                                                     |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`_to_string<class_Object_private_method__to_string>`\ (\ ) |virtual|                                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`_validate_property<class_Object_private_method__validate_property>`\ (\ property\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual|                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_user_signal<class_Object_method_add_user_signal>`\ (\ signal\: :ref:`String<class_String>`, arguments\: :ref:`Array<class_Array>` = []\ )                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`call<class_Object_method_call>`\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`call_deferred<class_Object_method_call_deferred>`\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`callv<class_Object_method_callv>`\ (\ method\: :ref:`StringName<class_StringName>`, arg_array\: :ref:`Array<class_Array>`\ )                                                                                                       |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`can_translate_messages<class_Object_method_can_translate_messages>`\ (\ ) |const|                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`cancel_free<class_Object_method_cancel_free>`\ (\ )                                                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`connect<class_Object_method_connect>`\ (\ signal\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`, flags\: :ref:`int<class_int>` = 0\ )                                                           |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`disconnect<class_Object_method_disconnect>`\ (\ signal\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`\ )                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`                            | :ref:`emit_signal<class_Object_method_emit_signal>`\ (\ signal\: :ref:`StringName<class_StringName>`, ...\ ) |vararg|                                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`free<class_Object_method_free>`\ (\ )                                                                                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get<class_Object_method_get>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`get_class<class_Object_method_get_class>`\ (\ ) |const|                                                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_incoming_connections<class_Object_method_get_incoming_connections>`\ (\ ) |const|                                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get_indexed<class_Object_method_get_indexed>`\ (\ property_path\: :ref:`NodePath<class_NodePath>`\ ) |const|                                                                                                                       |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_instance_id<class_Object_method_get_instance_id>`\ (\ ) |const|                                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get_meta<class_Object_method_get_meta>`\ (\ name\: :ref:`StringName<class_StringName>`, default\: :ref:`Variant<class_Variant>` = null\ ) |const|                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] | :ref:`get_meta_list<class_Object_method_get_meta_list>`\ (\ ) |const|                                                                                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_method_argument_count<class_Object_method_get_method_argument_count>`\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_method_list<class_Object_method_get_method_list>`\ (\ ) |const|                                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_property_list<class_Object_method_get_property_list>`\ (\ ) |const|                                                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get_script<class_Object_method_get_script>`\ (\ ) |const|                                                                                                                                                                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_signal_connection_list<class_Object_method_get_signal_connection_list>`\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_signal_list<class_Object_method_get_signal_list>`\ (\ ) |const|                                                                                                                                                                |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>`                              | :ref:`get_translation_domain<class_Object_method_get_translation_domain>`\ (\ ) |const|                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_connections<class_Object_method_has_connections>`\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_meta<class_Object_method_has_meta>`\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_method<class_Object_method_has_method>`\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_signal<class_Object_method_has_signal>`\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_user_signal<class_Object_method_has_user_signal>`\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_blocking_signals<class_Object_method_is_blocking_signals>`\ (\ ) |const|                                                                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_class<class_Object_method_is_class>`\ (\ class\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                                                 |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_connected<class_Object_method_is_connected>`\ (\ signal\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`\ ) |const|                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`is_queued_for_deletion<class_Object_method_is_queued_for_deletion>`\ (\ ) |const|                                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`notification<class_Object_method_notification>`\ (\ what\: :ref:`int<class_int>`, reversed\: :ref:`bool<class_bool>` = false\ )                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`notify_property_list_changed<class_Object_method_notify_property_list_changed>`\ (\ )                                                                                                                                              |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`property_can_revert<class_Object_method_property_can_revert>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`property_get_revert<class_Object_method_property_get_revert>`\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const|                                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_meta<class_Object_method_remove_meta>`\ (\ name\: :ref:`StringName<class_StringName>`\ )                                                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_user_signal<class_Object_method_remove_user_signal>`\ (\ signal\: :ref:`StringName<class_StringName>`\ )                                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set<class_Object_method_set>`\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                         |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_block_signals<class_Object_method_set_block_signals>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                                  |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_deferred<class_Object_method_set_deferred>`\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                       |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_indexed<class_Object_method_set_indexed>`\ (\ property_path\: :ref:`NodePath<class_NodePath>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                        |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_message_translation<class_Object_method_set_message_translation>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_meta<class_Object_method_set_meta>`\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ )                                                                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_script<class_Object_method_set_script>`\ (\ script\: :ref:`Variant<class_Variant>`\ )                                                                                                                                          |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`set_translation_domain<class_Object_method_set_translation_domain>`\ (\ domain\: :ref:`StringName<class_StringName>`\ )                                                                                                            |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`to_string<class_Object_method_to_string>`\ (\ )                                                                                                                                                                                    |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`tr<class_Object_method_tr>`\ (\ message\: :ref:`StringName<class_StringName>`, context\: :ref:`StringName<class_StringName>` = &""\ ) |const|                                                                                      |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`tr_n<class_Object_method_tr_n>`\ (\ message\: :ref:`StringName<class_StringName>`, plural_message\: :ref:`StringName<class_StringName>`, n\: :ref:`int<class_int>`, context\: :ref:`StringName<class_StringName>` = &""\ ) |const| |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_Object_signal_property_list_changed:

.. rst-class:: classref-signal

**property_list_changed**\ (\ ) :ref:`🔗<class_Object_signal_property_list_changed>`

Được phát ra khi :ref:`notify_property_list_changed()<class_Object_method_notify_property_list_changed>` được gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_signal_script_changed:

.. rst-class:: classref-signal

**script_changed**\ (\ ) :ref:`🔗<class_Object_signal_script_changed>`

Được phát ra khi script của Object bị thay đổi.

\ **Lưu ý:** Khi signal này được phát ra, script mới vẫn chưa được khởi tạo. Nếu cần truy cập script mới, hãy defer các connection đến signal này bằng :ref:`CONNECT_DEFERRED<class_Object_constant_CONNECT_DEFERRED>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_Object_ConnectFlags:

.. rst-class:: classref-enumeration

flags **ConnectFlags**: :ref:`🔗<enum_Object_ConnectFlags>`

.. _class_Object_constant_CONNECT_DEFERRED:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectFlags<enum_Object_ConnectFlags>` **CONNECT_DEFERRED** = ``1``

Các connection deferred sẽ kích hoạt :ref:`Callable<class_Callable>`\ s của chúng khi engine rảnh (ở cuối frame), thay vì ngay lập tức.

.. _class_Object_constant_CONNECT_PERSIST:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectFlags<enum_Object_ConnectFlags>` **CONNECT_PERSIST** = ``2``

Các connection persistent được lưu khi Object được serialize (chẳng hạn khi sử dụng :ref:`PackedScene.pack()<class_PackedScene_method_pack>`). Trong editor, các connection được tạo thông qua Signals dock luôn là persistent.

\ **Lưu ý:** Không thể tạo connection persistent đến các hàm lambda (tức là khi code của hàm được nhúng trong lệnh gọi :ref:`connect()<class_Object_method_connect>`).

.. _class_Object_constant_CONNECT_ONE_SHOT:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectFlags<enum_Object_ConnectFlags>` **CONNECT_ONE_SHOT** = ``4``

Các connection one-shot sẽ tự ngắt kết nối sau khi được phát ra.

.. _class_Object_constant_CONNECT_REFERENCE_COUNTED:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectFlags<enum_Object_ConnectFlags>` **CONNECT_REFERENCE_COUNTED** = ``8``

Các connection reference-counted có thể được gán cho cùng một :ref:`Callable<class_Callable>` nhiều lần. Mỗi lần ngắt kết nối sẽ giảm bộ đếm nội bộ. Signal chỉ ngắt kết nối hoàn toàn khi bộ đếm đạt 0.

.. _class_Object_constant_CONNECT_APPEND_SOURCE_OBJECT:

.. rst-class:: classref-enumeration-constant

:ref:`ConnectFlags<enum_Object_ConnectFlags>` **CONNECT_APPEND_SOURCE_OBJECT** = ``16``

Khi signal được phát ra, Object nguồn sẽ tự động được thêm vào sau các đối số ban đầu của signal, bất kể các unbind của :ref:`Callable<class_Callable>` được kết nối, vì chúng chỉ ảnh hưởng đến các đối số ban đầu của signal (xem :ref:`Callable.unbind()<class_Callable_method_unbind>`, :ref:`Callable.get_unbound_arguments_count()<class_Callable_method_get_unbound_arguments_count>`).

::

    extends Object

    signal test_signal

    func test():
        print(self) # In ra, ví dụ: <Object#35332818393>
        test_signal.connect(prints.unbind(1), CONNECT_APPEND_SOURCE_OBJECT)
        test_signal.emit("emit_arg_1", "emit_arg_2") # In ra emit_arg_1 <Object#35332818393>

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_Object_constant_NOTIFICATION_POSTINITIALIZE:

.. rst-class:: classref-constant

**NOTIFICATION_POSTINITIALIZE** = ``0`` :ref:`🔗<class_Object_constant_NOTIFICATION_POSTINITIALIZE>`

Notification được nhận khi Object được khởi tạo, trước khi script của nó được gắn vào. Được sử dụng nội bộ.

.. _class_Object_constant_NOTIFICATION_PREDELETE:

.. rst-class:: classref-constant

**NOTIFICATION_PREDELETE** = ``1`` :ref:`🔗<class_Object_constant_NOTIFICATION_PREDELETE>`

Notification được nhận khi Object sắp bị xóa. Có thể được sử dụng giống như destructor trong các ngôn ngữ lập trình hướng đối tượng.

Notification này được gửi theo thứ tự ngược.

.. _class_Object_constant_NOTIFICATION_EXTENSION_RELOADED:

.. rst-class:: classref-constant

**NOTIFICATION_EXTENSION_RELOADED** = ``2`` :ref:`🔗<class_Object_constant_NOTIFICATION_EXTENSION_RELOADED>`

Notification được nhận khi Object hoàn tất hot reloading. Notification này chỉ được gửi cho các lớp extension và các lớp dẫn xuất.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_Object_private_method__get:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_get**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |virtual| :ref:`🔗<class_Object_private_method__get>`

Ghi đè phương thức này để tùy chỉnh hành vi của :ref:`get()<class_Object_method_get>`. Phương thức này phải trả về giá trị của ``property`` đã cho hoặc ``null`` nếu ``property`` nên được xử lý theo cách thông thường.

Kết hợp với :ref:`_set()<class_Object_private_method__set>` và :ref:`_get_property_list()<class_Object_private_method__get_property_list>`, phương thức này cho phép định nghĩa các thuộc tính tùy chỉnh, đặc biệt hữu ích cho các editor plugin.

\ **Lưu ý:** Phương thức này không được gọi khi lấy các thuộc tính tích hợp của một Object, bao gồm cả các thuộc tính được định nghĩa bằng :ref:`@GDScript.@export<class_@GDScript_annotation_@export>`.


.. tabs::

 .. code-tab:: gdscript

    func _get(property):
        if property == "fake_property":
            print("Getting my property!")
            return 4
        return null

    func _get_property_list():
        return [
            { "name": "fake_property", "type": TYPE_INT }
        ]

 .. code-tab:: csharp

    public override Variant _Get(StringName property)
    {
        if (property == "FakeProperty")
        {
            GD.Print("Getting my property!");
            return 4;
        }
        return default;
    }

    public override Godot.Collections.Array<Godot.Collections.Dictionary> _GetPropertyList()
    {
        return
        [
            new Godot.Collections.Dictionary()
            {
                { "name", "FakeProperty" },
                { "type", (int)Variant.Type.Int },
            },
        ];
    }



\ **Lưu ý:** Không giống các virtual method khác, phương thức này được tự động gọi cho mọi script ghi đè nó. Điều này có nghĩa là không được gọi implementation của lớp cơ sở thông qua ``super`` trong GDScript hoặc các tương đương của nó trong những ngôn ngữ khác. Lớp con thấp nhất sẽ được gọi trước, sau đó các lệnh gọi tiếp tục đi lên trong hệ thống phân cấp lớp. Chuỗi lệnh gọi sẽ dừng ở lớp đầu tiên trả về một giá trị không phải ``null``.

\ **Cảnh báo:** Phương thức này phải :doc:`an toàn luồng <../tutorials/performance/thread_safe_apis>` nếu được ghi đè. Nếu không, engine có thể gặp sự cố khi cố gắng lưu một resource chứa đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__get_property_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **_get_property_list**\ (\ ) |virtual| :ref:`🔗<class_Object_private_method__get_property_list>`

Ghi đè phương thức này để cung cấp danh sách tùy chỉnh các property bổ sung cần được engine xử lý.

Phải trả về một danh sách property dưới dạng :ref:`Array<class_Array>` gồm các dictionary. Kết quả được thêm vào array của :ref:`get_property_list()<class_Object_method_get_property_list>`, và phải được định dạng theo cùng cách. Mỗi :ref:`Dictionary<class_Dictionary>` ít nhất phải chứa các mục ``name`` và ``type``.

Bạn có thể sử dụng :ref:`_property_can_revert()<class_Object_private_method__property_can_revert>` và :ref:`_property_get_revert()<class_Object_private_method__property_get_revert>` để tùy chỉnh các giá trị mặc định của những property được thêm bởi phương thức này.

Ví dụ dưới đây hiển thị danh sách các số được viết bằng chữ, từ ``ZERO`` đến ``FIVE``, với ``number_count`` điều khiển kích thước của danh sách:


.. tabs::

 .. code-tab:: gdscript

    @tool
    extends Node

    @export var number_count = 3:
        set(nc):
            number_count = nc
            numbers.resize(number_count)
            notify_property_list_changed()

    var numbers = PackedInt32Array([0, 0, 0])

    func _get_property_list():
        var properties: Array[Dictionary] = []

        for i in range(number_count):
            properties.append({
                "name": "number_%d" % i,
                "type": TYPE_INT,
                "hint": PROPERTY_HINT_ENUM,
                "hint_string": "ZERO,ONE,TWO,THREE,FOUR,FIVE",
            })

        return properties

    func _get(property):
        if property.begins_with("number_"):
            var index = property.get_slice("_", 1).to_int()
            return numbers[index]
        return null

    func _set(property, value):
        if property.begins_with("number_"):
            var index = property.get_slice("_", 1).to_int()
            numbers[index] = value
            return true
        return false

 .. code-tab:: csharp

    [Tool]
    public partial class MyNode : Node
    {
        private int _numberCount;

        [Export]
        public int NumberCount
        {
            get => _numberCount;
            set
            {
                _numberCount = value;
                _numbers.Resize(_numberCount);
                NotifyPropertyListChanged();
            }
        }

        private Godot.Collections.Array<int> _numbers = [];

        public override Godot.Collections.Array<Godot.Collections.Dictionary> _GetPropertyList()
        {
            Godot.Collections.Array<Godot.Collections.Dictionary> properties = [];

            for (int i = 0; i < _numberCount; i++)
            {
                properties.Add(new Godot.Collections.Dictionary()
                {
                    { "name", $"number_{i}" },
                    { "type", (int)Variant.Type.Int },
                    { "hint", (int)PropertyHint.Enum },
                    { "hint_string", "Zero,One,Two,Three,Four,Five" },
                });
            }

            return properties;
        }

        public override Variant _Get(StringName property)
        {
            string propertyName = property.ToString();
            if (propertyName.StartsWith("number_"))
            {
                int index = int.Parse(propertyName.Substring("number_".Length));
                return _numbers[index];
            }
            return default;
        }

        public override bool _Set(StringName property, Variant value)
        {
            string propertyName = property.ToString();
            if (propertyName.StartsWith("number_"))
            {
                int index = int.Parse(propertyName.Substring("number_".Length));
                _numbers[index] = value.As<int>();
                return true;
            }
            return false;
        }
    }



\ **Lưu ý:** Phương thức này dành cho các mục đích nâng cao. Đối với hầu hết trường hợp sử dụng thông thường, các ngôn ngữ scripting cung cấp những cách dễ dàng hơn để xử lý property. Xem :ref:`@GDScript.@export<class_@GDScript_annotation_@export>`, :ref:`@GDScript.@export_enum<class_@GDScript_annotation_@export_enum>`, :ref:`@GDScript.@export_group<class_@GDScript_annotation_@export_group>`, v.v. Nếu muốn tùy chỉnh các property được export, hãy sử dụng :ref:`_validate_property()<class_Object_private_method__validate_property>`.

\ **Lưu ý:** Nếu script của đối tượng không phải là :ref:`@GDScript.@tool<class_@GDScript_annotation_@tool>`, phương thức này sẽ không được gọi trong editor.

\ **Lưu ý:** Không giống các virtual method khác, phương thức này được tự động gọi cho mọi script ghi đè nó. Điều này có nghĩa là không được gọi implementation cơ sở thông qua ``super`` trong GDScript hoặc các cách tương đương trong những ngôn ngữ khác. Sub-class thấp nhất sẽ được gọi trước, sau đó các lệnh gọi sẽ đi lên trong cây phân cấp class.

\ **Cảnh báo:** Phương thức này phải :doc:`an toàn luồng <../tutorials/performance/thread_safe_apis>` nếu được ghi đè. Nếu không, engine có thể gặp sự cố khi cố gắng lưu một resource chứa đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__init:

.. rst-class:: classref-method

|void| **_init**\ (\ ) |virtual| :ref:`🔗<class_Object_private_method__init>`

Được gọi khi script của đối tượng được khởi tạo, thường là sau khi đối tượng được khởi tạo trong bộ nhớ (thông qua ``Object.new()`` trong GDScript hoặc ``new GodotObject`` trong C#). Phương thức này cũng có thể được định nghĩa để nhận các tham số. Phương thức này tương tự constructor trong hầu hết ngôn ngữ lập trình.

\ **Lưu ý:** Nếu :ref:`_init()<class_Object_private_method__init>` được định nghĩa với các tham số *bắt buộc*, Object có script chỉ có thể được tạo trực tiếp. Nếu sử dụng bất kỳ cách nào khác (chẳng hạn như :ref:`PackedScene.instantiate()<class_PackedScene_method_instantiate>` hoặc :ref:`Node.duplicate()<class_Node_method_duplicate>`), quá trình khởi tạo script sẽ thất bại.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__iter_get:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_iter_get**\ (\ iter\: :ref:`Variant<class_Variant>`\ ) |virtual| :ref:`🔗<class_Object_private_method__iter_get>`

Trả về giá trị iterable hiện tại. ``iter`` lưu trạng thái lặp, nhưng không giống :ref:`_iter_init()<class_Object_private_method__iter_init>` và :ref:`_iter_next()<class_Object_private_method__iter_next>`, trạng thái này được cho là chỉ đọc, vì vậy không có wrapper :ref:`Array<class_Array>`.

\ **Mẹo:** Trong GDScript, bạn có thể sử dụng một subtype của :ref:`Variant<class_Variant>` làm kiểu trả về cho :ref:`_iter_get()<class_Object_private_method__iter_get>`. Kiểu được chỉ định sẽ được dùng để thiết lập kiểu của biến iterator trong các vòng lặp ``for``, giúp tăng tính an toàn kiểu.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__iter_init:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_iter_init**\ (\ iter\: :ref:`Array<class_Array>`\ ) |virtual| :ref:`🔗<class_Object_private_method__iter_init>`

Khởi tạo iterator. ``iter`` lưu trạng thái lặp. Vì GDScript không hỗ trợ truyền đối số bằng tham chiếu, một array một phần tử được dùng làm wrapper. Trả về ``true`` khi iterator chưa đi đến cuối.

::

    class MyRange:
        var _from
        var _to

        func _init(from, to):
            assert(from <= to)
            _from = from
            _to = to

        func _iter_init(iter):
            iter[0] = _from
            return iter[0] < _to

        func _iter_next(iter):
            iter[0] += 1
            return iter[0] < _to

        func _iter_get(iter):
            return iter

    func _ready():
        var my_range = MyRange.new(2, 5)
        for x in my_range:
            print(x) # In ra 2, 3, 4.

\ **Lưu ý:** Tránh lưu trạng thái iterator trong member variable, thay vào đó hãy sử dụng tham số ``iter``. Nếu không, bạn sẽ không thể tái sử dụng cùng một iterator instance trong các vòng lặp lồng nhau.

Xem thêm `online docs <../tutorials/scripting/gdscript/gdscript_advanced.html#custom-iterators>`__.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__iter_next:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_iter_next**\ (\ iter\: :ref:`Array<class_Array>`\ ) |virtual| :ref:`🔗<class_Object_private_method__iter_next>`

Di chuyển iterator đến lần lặp tiếp theo. ``iter`` lưu trạng thái lặp. Vì GDScript không hỗ trợ truyền đối số bằng tham chiếu, một array một phần tử được dùng làm wrapper. Trả về ``true`` khi iterator chưa đi đến cuối.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__notification:

.. rst-class:: classref-method

|void| **_notification**\ (\ what\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_Object_private_method__notification>`

Được gọi khi đối tượng nhận một notification, có thể được xác định trong ``what`` bằng cách so sánh nó với một hằng số. Xem thêm :ref:`notification()<class_Object_method_notification>`.


.. tabs::

 .. code-tab:: gdscript

    func _notification(what):
        if what == NOTIFICATION_PREDELETE:
            print("Goodbye!")

 .. code-tab:: csharp

    public override void _Notification(int what)
    {
        if (what == NotificationPredelete)
        {
            GD.Print("Goodbye!");
        }
    }



\ **Lưu ý:** **Object** cơ sở định nghĩa một vài notification (:ref:`NOTIFICATION_POSTINITIALIZE<class_Object_constant_NOTIFICATION_POSTINITIALIZE>` và :ref:`NOTIFICATION_PREDELETE<class_Object_constant_NOTIFICATION_PREDELETE>`). Các class kế thừa như :ref:`Node<class_Node>` định nghĩa nhiều notification hơn, và chúng cũng được phương thức này nhận.

\ **Lưu ý:** Không giống các virtual method khác, phương thức này được tự động gọi cho mọi script ghi đè nó. Điều này có nghĩa là không được gọi implementation cơ sở thông qua ``super`` trong GDScript hoặc các cách tương đương trong những ngôn ngữ khác. Thứ tự gọi phụ thuộc vào đối số ``reversed`` của :ref:`notification()<class_Object_method_notification>` và thay đổi tùy theo từng notification. Hầu hết notification được gửi theo thứ tự tiến (tức là class Object trước, class dẫn xuất sâu nhất sau cùng).

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__property_can_revert:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_property_can_revert**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |virtual| :ref:`🔗<class_Object_private_method__property_can_revert>`

Ghi đè phương thức này để tùy chỉnh hành vi revert của ``property`` đã cho. Phải trả về ``true`` nếu ``property`` có giá trị mặc định tùy chỉnh và có thể revert trong Inspector dock. Sử dụng :ref:`_property_get_revert()<class_Object_private_method__property_get_revert>` để chỉ định giá trị mặc định của ``property``.

\ **Lưu ý:** Phương thức này phải trả về nhất quán, bất kể giá trị hiện tại của ``property``.

\ **Lưu ý:** Không giống các virtual method khác, phương thức này được tự động gọi cho mọi script ghi đè nó. Điều này có nghĩa là không được gọi implementation cơ sở thông qua ``super`` trong GDScript hoặc các cách tương đương trong những ngôn ngữ khác. Sub-class thấp nhất sẽ được gọi trước, sau đó các lệnh gọi sẽ đi lên trong cây phân cấp class. Chuỗi gọi sẽ dừng ở class đầu tiên trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__property_get_revert:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **_property_get_revert**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |virtual| :ref:`🔗<class_Object_private_method__property_get_revert>`

Ghi đè phương thức này để tùy chỉnh hành vi revert của ``property`` đã cho. Phải trả về giá trị mặc định của ``property``. Nếu giá trị mặc định khác với giá trị hiện tại của ``property``, một biểu tượng revert sẽ được hiển thị trong Inspector dock.

\ **Lưu ý:** :ref:`_property_can_revert()<class_Object_private_method__property_can_revert>` cũng phải được ghi đè thì phương thức này mới được gọi.

\ **Lưu ý:** Không giống các virtual method khác, phương thức này được tự động gọi cho mọi script ghi đè nó. Điều này có nghĩa là không được gọi implementation cơ sở thông qua ``super`` trong GDScript hoặc các cách tương đương trong những ngôn ngữ khác. Sub-class thấp nhất sẽ được gọi trước, sau đó các lệnh gọi sẽ đi lên trong cây phân cấp class. Chuỗi gọi sẽ dừng ở class đầu tiên trả về giá trị không phải ``null``.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__set:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_set**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) |virtual| :ref:`🔗<class_Object_private_method__set>`

Ghi đè phương thức này để tùy chỉnh hành vi của :ref:`set()<class_Object_method_set>`. Phải đặt ``property`` thành ``value`` và trả về ``true``, hoặc ``false`` nếu ``property`` nên được xử lý theo cách thông thường. Cách *chính xác* để đặt ``property`` phụ thuộc vào implementation của phương thức này.

Kết hợp với :ref:`_get()<class_Object_private_method__get>` và :ref:`_get_property_list()<class_Object_private_method__get_property_list>`, phương thức này cho phép định nghĩa các property tùy chỉnh, đặc biệt hữu ích cho các editor plugin.

\ **Lưu ý:** Phương thức này không được gọi khi đặt các property tích hợp sẵn của một đối tượng, bao gồm các property được định nghĩa bằng :ref:`@GDScript.@export<class_@GDScript_annotation_@export>`.


.. tabs::

 .. code-tab:: gdscript

    var internal_data = {}

    func _set(property, value):
        if property == "fake_property":
            # Lưu giá trị vào fake property.
            internal_data["fake_property"] = value
            return true
        return false

    func _get_property_list():
        return [
            { "name": "fake_property", "type": TYPE_INT }
        ]

 .. code-tab:: csharp

    private Godot.Collections.Dictionary _internalData = new Godot.Collections.Dictionary();

    public override bool _Set(StringName property, Variant value)
    {
        if (property == "FakeProperty")
        {
            // Lưu giá trị vào fake property.
            _internalData["FakeProperty"] = value;
            return true;
        }

        return false;
    }

    public override Godot.Collections.Array<Godot.Collections.Dictionary> _GetPropertyList()
    {
        return
        [
            new Godot.Collections.Dictionary()
            {
                { "name", "FakeProperty" },
                { "type", (int)Variant.Type.Int },
            },
        ];
    }



\ **Lưu ý:** Không giống các virtual method khác, phương thức này được tự động gọi cho mọi script ghi đè nó. Điều này có nghĩa là không được gọi implementation cơ sở thông qua ``super`` trong GDScript hoặc các cách tương đương trong những ngôn ngữ khác. Sub-class thấp nhất sẽ được gọi trước, sau đó các lệnh gọi sẽ đi lên trong cây phân cấp class. Chuỗi gọi sẽ dừng ở class đầu tiên trả về ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__to_string:

.. rst-class:: classref-method

:ref:`String<class_String>` **_to_string**\ (\ ) |virtual| :ref:`🔗<class_Object_private_method__to_string>`

Ghi đè phương thức này để tùy chỉnh giá trị trả về của :ref:`to_string()<class_Object_method_to_string>`, và do đó tùy chỉnh biểu diễn của đối tượng dưới dạng :ref:`String<class_String>`.

::

    func _to_string():
        return "Welcome to Godot 4!"

    func _init():
        print(self)       # In ra "Welcome to Godot 4!"
        var a = str(self) # a là "Welcome to Godot 4!"

.. rst-class:: classref-item-separator

----

.. _class_Object_private_method__validate_property:

.. rst-class:: classref-method

|void| **_validate_property**\ (\ property\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| :ref:`🔗<class_Object_private_method__validate_property>`

Ghi đè phương thức này để tùy chỉnh các property hiện có. Mọi thông tin property đều đi qua phương thức này, ngoại trừ các property được thêm bằng :ref:`_get_property_list()<class_Object_private_method__get_property_list>`. Nội dung dictionary giống như trong :ref:`_get_property_list()<class_Object_private_method__get_property_list>`.


.. tabs::

 .. code-tab:: gdscript

    @tool
    extends Node

    @export var is_number_editable: bool:
        set(value):
            is_number_editable = value
            notify_property_list_changed()
    @export var number: int

    func _validate_property(property: Dictionary):
        if property.name == "number" and not is_number_editable:
            property.usage |= PROPERTY_USAGE_READ_ONLY

 .. code-tab:: csharp

    [Tool]
    public partial class MyNode : Node
    {
        private bool _isNumberEditable;

        [Export]
        public bool IsNumberEditable
        {
            get => _isNumberEditable;
            set
            {
                _isNumberEditable = value;
                NotifyPropertyListChanged();
            }
        }

        [Export]
        public int Number { get; set; }

        public override void _ValidateProperty(Godot.Collections.Dictionary property)
        {
            if (property["name"].AsStringName() == PropertyName.Number && !IsNumberEditable)
            {
                var usage = property["usage"].As<PropertyUsageFlags>() | PropertyUsageFlags.ReadOnly;
                property["usage"] = (int)usage;
            }
        }
    }



.. rst-class:: classref-item-separator

----

.. _class_Object_method_add_user_signal:

.. rst-class:: classref-method

|void| **add_user_signal**\ (\ signal\: :ref:`String<class_String>`, arguments\: :ref:`Array<class_Array>` = []\ ) :ref:`🔗<class_Object_method_add_user_signal>`

Thêm một signal do người dùng định nghĩa có tên ``signal``. Có thể thêm các đối số tùy chọn cho signal dưới dạng một :ref:`Array<class_Array>` gồm các dictionary, mỗi dictionary định nghĩa một ``name`` :ref:`String<class_String>` và một ``type`` :ref:`int<class_int>` (xem :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`). Xem thêm :ref:`has_user_signal()<class_Object_method_has_user_signal>` và :ref:`remove_user_signal()<class_Object_method_remove_user_signal>`.


.. tabs::

 .. code-tab:: gdscript

    add_user_signal("hurt", [
        { "name": "damage", "type": TYPE_INT },
        { "name": "source", "type": TYPE_OBJECT }
    ])

 .. code-tab:: csharp

    AddUserSignal("Hurt",
    [
        new Godot.Collections.Dictionary()
        {
            { "name", "damage" },
            { "type", (int)Variant.Type.Int },
        },
        new Godot.Collections.Dictionary()
        {
            { "name", "source" },
            { "type", (int)Variant.Type.Object },
        },
    ]);



.. rst-class:: classref-item-separator

----

.. _class_Object_method_call:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **call**\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Object_method_call>`

Gọi ``method`` trên object và trả về kết quả. Method này hỗ trợ số lượng đối số thay đổi, vì vậy có thể truyền các tham số dưới dạng danh sách phân tách bằng dấu phẩy.


.. tabs::

 .. code-tab:: gdscript

    var node = Node3D.new()
    node.call("rotate", Vector3(1.0, 0.0, 0.0), 1.571)

 .. code-tab:: csharp

    var node = new Node3D();
    node.Call(Node3D.MethodName.Rotate, new Vector3(1f, 0f, 0f), 1.571f);



\ **Lưu ý:** Trong C#, ``method`` phải ở dạng snake_case khi tham chiếu đến các method dựng sẵn của Godot. Nên sử dụng các tên được cung cấp trong class ``MethodName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_call_deferred:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **call_deferred**\ (\ method\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Object_method_call_deferred>`

Gọi ``method`` trên object trong thời gian idle. Luôn trả về ``null``, **không phải** kết quả của method.

Thời gian idle chủ yếu diễn ra vào cuối các frame process và physics. Trong thời gian này, các deferred call sẽ được thực thi cho đến khi không còn call nào, nghĩa là bạn có thể defer các call từ những deferred call khác và chúng vẫn sẽ được thực thi trong chu kỳ idle hiện tại. Điều này có nghĩa là bạn không nên gọi một method theo cách deferred từ chính nó (hoặc từ một method được nó gọi), vì sẽ gây đệ quy vô hạn giống như khi bạn gọi trực tiếp method đó.

Method này hỗ trợ số lượng đối số thay đổi, vì vậy có thể truyền các tham số dưới dạng danh sách phân tách bằng dấu phẩy.


.. tabs::

 .. code-tab:: gdscript

    var node = Node3D.new()
    node.call_deferred("rotate", Vector3(1.0, 0.0, 0.0), 1.571)

 .. code-tab:: csharp

    var node = new Node3D();
    node.CallDeferred(Node3D.MethodName.Rotate, new Vector3(1f, 0f, 0f), 1.571f);



Đối với các method được defer từ cùng một thread, thứ tự thực thi trong thời gian idle giống hệt thứ tự mà ``call_deferred`` được gọi.

Xem thêm :ref:`Callable.call_deferred()<class_Callable_method_call_deferred>`.

\ **Lưu ý:** Trong C#, ``method`` phải ở dạng snake_case khi tham chiếu đến các method dựng sẵn của Godot. Nên sử dụng các tên được cung cấp trong class ``MethodName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

\ **Lưu ý:** Nếu bạn muốn trì hoãn lời gọi function một frame, hãy tham khảo các signal :ref:`SceneTree.process_frame<class_SceneTree_signal_process_frame>` và :ref:`SceneTree.physics_frame<class_SceneTree_signal_physics_frame>`.

::

    var node = Node3D.new()
    # Tạo một Callable và bind các đối số vào lời gọi rotate() của node.
    var callable = node.rotate.bind(Vector3(1.0, 0.0, 0.0), 1.571)
    # Kết nối callable với signal process_frame để nó được gọi trong frame process tiếp theo.
    # CONNECT_ONE_SHOT đảm bảo nó chỉ được gọi một lần thay vì trong mọi frame.
    get_tree().process_frame.connect(callable, CONNECT_ONE_SHOT)

.. rst-class:: classref-item-separator

----

.. _class_Object_method_callv:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **callv**\ (\ method\: :ref:`StringName<class_StringName>`, arg_array\: :ref:`Array<class_Array>`\ ) :ref:`🔗<class_Object_method_callv>`

Gọi ``method`` trên object và trả về kết quả. Không giống :ref:`call()<class_Object_method_call>`, method này yêu cầu tất cả tham số phải nằm trong ``arg_array``.


.. tabs::

 .. code-tab:: gdscript

    var node = Node3D.new()
    node.callv("rotate", [Vector3(1.0, 0.0, 0.0), 1.571])

 .. code-tab:: csharp

    var node = new Node3D();
    node.Callv(Node3D.MethodName.Rotate, [new Vector3(1f, 0f, 0f), 1.571f]);



\ **Lưu ý:** Trong C#, ``method`` phải ở dạng snake_case khi tham chiếu đến các method dựng sẵn của Godot. Nên sử dụng các tên được cung cấp trong class ``MethodName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_can_translate_messages:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **can_translate_messages**\ (\ ) |const| :ref:`🔗<class_Object_method_can_translate_messages>`

Trả về ``true`` nếu object được phép dịch các message bằng :ref:`tr()<class_Object_method_tr>` và :ref:`tr_n()<class_Object_method_tr_n>`. Xem thêm :ref:`set_message_translation()<class_Object_method_set_message_translation>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_cancel_free:

.. rst-class:: classref-method

|void| **cancel_free**\ (\ ) :ref:`🔗<class_Object_method_cancel_free>`

Nếu method này được gọi trong :ref:`NOTIFICATION_PREDELETE<class_Object_constant_NOTIFICATION_PREDELETE>`, object này sẽ từ chối bị giải phóng và vẫn được cấp phát. Đây chủ yếu là một function nội bộ dùng để xử lý lỗi, nhằm ngăn người dùng giải phóng các object khi chúng không được phép bị giải phóng.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_connect:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **connect**\ (\ signal\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`, flags\: :ref:`int<class_int>` = 0\ ) :ref:`🔗<class_Object_method_connect>`

Kết nối một ``signal`` theo tên với một ``callable``. Cũng có thể thêm ``flags`` tùy chọn để cấu hình hành vi của kết nối (xem các hằng số :ref:`ConnectFlags<enum_Object_ConnectFlags>`).

Một signal chỉ có thể được kết nối một lần với cùng một :ref:`Callable<class_Callable>`. Nếu signal đã được kết nối, method này trả về :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` và tạo ra lỗi, trừ khi signal được kết nối với :ref:`CONNECT_REFERENCE_COUNTED<class_Object_constant_CONNECT_REFERENCE_COUNTED>`. Để ngăn điều này, trước tiên hãy dùng :ref:`is_connected()<class_Object_method_is_connected>` để kiểm tra các kết nối hiện có.

\ **Lưu ý:** Nếu object của ``callable`` được giải phóng, kết nối sẽ bị mất.

\ **Lưu ý:** Trong GDScript, nhìn chung nên kết nối các signal bằng :ref:`Signal.connect()<class_Signal_method_connect>` thay thế.

\ **Lưu ý:** Method này và tất cả các method liên quan đến signal khác đều thread-safe.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_disconnect:

.. rst-class:: classref-method

|void| **disconnect**\ (\ signal\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_Object_method_disconnect>`

Ngắt kết nối một ``signal`` theo tên khỏi một ``callable`` được chỉ định. Nếu kết nối không tồn tại, method sẽ tạo ra lỗi. Dùng :ref:`is_connected()<class_Object_method_is_connected>` để đảm bảo kết nối tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_emit_signal:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **emit_signal**\ (\ signal\: :ref:`StringName<class_StringName>`, ...\ ) |vararg| :ref:`🔗<class_Object_method_emit_signal>`

Phát ``signal`` được chỉ định theo tên. Signal đó phải tồn tại, vì vậy nó phải là signal dựng sẵn của class này hoặc một trong các class kế thừa, hoặc là signal do người dùng định nghĩa (xem :ref:`add_user_signal()<class_Object_method_add_user_signal>`). Method này hỗ trợ số lượng đối số thay đổi, vì vậy có thể truyền các tham số dưới dạng danh sách phân tách bằng dấu phẩy.

Trả về :ref:`@GlobalScope.ERR_UNAVAILABLE<class_@GlobalScope_constant_ERR_UNAVAILABLE>` nếu ``signal`` không tồn tại hoặc các tham số không hợp lệ.


.. tabs::

 .. code-tab:: gdscript

    emit_signal("hit", "sword", 100)
    emit_signal("game_over")

 .. code-tab:: csharp

    EmitSignal(SignalName.Hit, "sword", 100);
    EmitSignal(SignalName.GameOver);



\ **Lưu ý:** Trong C#, ``signal`` phải ở dạng snake_case khi tham chiếu đến các signal dựng sẵn của Godot. Nên sử dụng các tên được cung cấp trong class ``SignalName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_free:

.. rst-class:: classref-method

|void| **free**\ (\ ) :ref:`🔗<class_Object_method_free>`

Xóa object khỏi bộ nhớ. Các tham chiếu đã tồn tại đến object sẽ trở nên không hợp lệ, và mọi nỗ lực truy cập chúng sẽ dẫn đến lỗi runtime. Việc kiểm tra các tham chiếu bằng :ref:`@GlobalScope.is_instance_valid()<class_@GlobalScope_method_is_instance_valid>` sẽ trả về ``false``. Điều này tương đương với function ``memdelete`` trong GDExtension C++.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_get>`

Trả về giá trị :ref:`Variant<class_Variant>` của ``property`` đã cho. Nếu ``property`` không tồn tại, method này trả về ``null``.


.. tabs::

 .. code-tab:: gdscript

    var node = Node2D.new()
    node.rotation = 1.5
    var a = node.get("rotation") # a là 1.5

 .. code-tab:: csharp

    var node = new Node2D();
    node.Rotation = 1.5f;
    var a = node.Get(Node2D.PropertyName.Rotation); // a là 1.5



\ **Lưu ý:** Trong C#, ``property`` phải ở dạng snake_case khi tham chiếu đến các property dựng sẵn của Godot. Nên sử dụng các tên được cung cấp trong class ``PropertyName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_class:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_class**\ (\ ) |const| :ref:`🔗<class_Object_method_get_class>`

Trả về tên class dựng sẵn của object dưới dạng :ref:`String<class_String>`. Xem thêm :ref:`is_class()<class_Object_method_is_class>`.

\ **Lưu ý:** Method này bỏ qua các khai báo ``class_name``. Nếu script của object này đã định nghĩa ``class_name``, tên class cơ sở, dựng sẵn sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_incoming_connections:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_incoming_connections**\ (\ ) |const| :ref:`🔗<class_Object_method_get_incoming_connections>`

Trả về một :ref:`Array<class_Array>` gồm các kết nối signal nhận được bởi object này. Mỗi kết nối được biểu diễn dưới dạng một :ref:`Dictionary<class_Dictionary>` chứa ba mục:

- ``signal`` là một tham chiếu đến :ref:`Signal<class_Signal>`; 

- ``callable`` là một tham chiếu đến :ref:`Callable<class_Callable>`; 

- ``flags`` là một tổ hợp của :ref:`ConnectFlags<enum_Object_ConnectFlags>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_indexed:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_indexed**\ (\ property_path\: :ref:`NodePath<class_NodePath>`\ ) |const| :ref:`🔗<class_Object_method_get_indexed>`

Lấy property của object được lập chỉ mục bởi ``property_path`` đã cho. Đường dẫn phải là một :ref:`NodePath<class_NodePath>` tương đối với object hiện tại và có thể sử dụng ký tự hai chấm (``:``) để truy cập các property lồng nhau.

\ **Ví dụ:** ``"position:x"`` hoặc ``"material:next_pass:blend_mode"``.


.. tabs::

 .. code-tab:: gdscript

    var node = Node2D.new()
    node.position = Vector2(5, -10)
    var a = node.get_indexed("position")   # a là Vector2(5, -10)
    var b = node.get_indexed("position:y") # b là -10

 .. code-tab:: csharp

    var node = new Node2D();
    node.Position = new Vector2(5, -10);
    var a = node.GetIndexed("position");   // a là Vector2(5, -10)
    var b = node.GetIndexed("position:y"); // b là -10



\ **Lưu ý:** Trong C#, ``property_path`` phải ở dạng snake_case khi tham chiếu đến các property dựng sẵn của Godot. Nên sử dụng các tên được cung cấp trong class ``PropertyName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

\ **Lưu ý:** Method này không hỗ trợ các đường dẫn thực tế đến node trong :ref:`SceneTree<class_SceneTree>`, mà chỉ hỗ trợ các đường dẫn đến sub-property. Trong ngữ cảnh node, hãy sử dụng :ref:`Node.get_node_and_resource()<class_Node_method_get_node_and_resource>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_instance_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_instance_id**\ (\ ) |const| :ref:`🔗<class_Object_method_get_instance_id>`

Trả về ID instance duy nhất của object. Có thể lưu ID này trong :ref:`EncodedObjectAsID<class_EncodedObjectAsID>` và dùng nó để truy xuất instance object này bằng :ref:`@GlobalScope.instance_from_id()<class_@GlobalScope_method_instance_from_id>`.

\ **Lưu ý:** ID này chỉ hữu ích trong session hiện tại. Nó sẽ không tương ứng với một object tương tự nếu ID được gửi qua network hoặc được tải từ file vào thời điểm sau.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_meta:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_meta**\ (\ name\: :ref:`StringName<class_StringName>`, default\: :ref:`Variant<class_Variant>` = null\ ) |const| :ref:`🔗<class_Object_method_get_meta>`

Trả về giá trị metadata của đối tượng cho mục nhập ``name``. Nếu mục nhập không tồn tại, trả về ``default``. Nếu ``default`` là ``null``, một lỗi cũng được tạo ra.

\ **Lưu ý:** Tên của metadata phải là một identifier hợp lệ theo phương thức :ref:`StringName.is_valid_identifier()<class_StringName_method_is_valid_identifier>`.

\ **Lưu ý:** Metadata có tên bắt đầu bằng dấu gạch dưới (``_``) được xem là chỉ dành cho editor. Metadata chỉ dành cho editor không được hiển thị trong Inspector và không nên được chỉnh sửa, mặc dù vẫn có thể được tìm thấy bằng phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_meta_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_meta_list**\ (\ ) |const| :ref:`🔗<class_Object_method_get_meta_list>`

Trả về tên các mục metadata của đối tượng dưới dạng một :ref:`Array<class_Array>` gồm các :ref:`StringName<class_StringName>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_method_argument_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_method_argument_count**\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_get_method_argument_count>`

Trả về số lượng đối số của ``method`` đã cho theo tên.

\ **Lưu ý:** Trong C#, ``method`` phải ở dạng snake_case khi tham chiếu đến các phương thức Godot tích hợp sẵn. Nên sử dụng các tên được cung cấp trong class ``MethodName`` để tránh phải cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_method_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_method_list**\ (\ ) |const| :ref:`🔗<class_Object_method_get_method_list>`

Trả về các phương thức của đối tượng này cùng signature của chúng dưới dạng một :ref:`Array<class_Array>` gồm các dictionary. Mỗi :ref:`Dictionary<class_Dictionary>` chứa các mục sau:

- ``name`` là tên của phương thức, dưới dạng một :ref:`String<class_String>`;

- ``args`` là một :ref:`Array<class_Array>` gồm các dictionary đại diện cho các đối số;

- ``default_args`` là các đối số mặc định dưới dạng một :ref:`Array<class_Array>` gồm các variant;

- ``flags`` là một tổ hợp của :ref:`MethodFlags<enum_@GlobalScope_MethodFlags>`;

- ``id`` là identifier nội bộ của phương thức :ref:`int<class_int>`;

- ``return`` là giá trị được trả về, dưới dạng một :ref:`Dictionary<class_Dictionary>`;

\ **Lưu ý:** Các dictionary của ``args`` và ``return`` được định dạng giống hệt kết quả của :ref:`get_property_list()<class_Object_method_get_property_list>`, mặc dù không phải tất cả các mục đều được sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_property_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_property_list**\ (\ ) |const| :ref:`🔗<class_Object_method_get_property_list>`

Trả về danh sách property của đối tượng dưới dạng một :ref:`Array<class_Array>` gồm các dictionary. Mỗi :ref:`Dictionary<class_Dictionary>` chứa các mục sau:

- ``name`` là tên của property, dưới dạng một :ref:`String<class_String>`;

- ``class_name`` là một :ref:`StringName<class_StringName>` rỗng, trừ khi property là :ref:`@GlobalScope.TYPE_OBJECT<class_@GlobalScope_constant_TYPE_OBJECT>` và kế thừa từ một class;

- ``type`` là kiểu của property, dưới dạng một :ref:`int<class_int>` (xem :ref:`Variant.Type<enum_@GlobalScope_Variant.Type>`);

- ``hint`` là *cách* property được dự định chỉnh sửa (xem :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>`);

- ``hint_string`` phụ thuộc vào hint (xem :ref:`PropertyHint<enum_@GlobalScope_PropertyHint>`);

- ``usage`` là một tổ hợp của :ref:`PropertyUsageFlags<enum_@GlobalScope_PropertyUsageFlags>`.

\ **Lưu ý:** Trong GDScript, tất cả class member đều được xử lý như property. Trong C# và GDExtension, có thể cần đánh dấu rõ ràng class member là Godot property bằng decorator hoặc attribute.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_script:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_script**\ (\ ) |const| :ref:`🔗<class_Object_method_get_script>`

Trả về instance :ref:`Script<class_Script>` của đối tượng, hoặc ``null`` nếu không có script nào được gắn vào.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_signal_connection_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_signal_connection_list**\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_get_signal_connection_list>`

Trả về một :ref:`Array<class_Array>` gồm các connection cho tên ``signal`` đã cho. Mỗi connection được biểu diễn dưới dạng một :ref:`Dictionary<class_Dictionary>` chứa ba mục:

- ``signal`` là tham chiếu đến :ref:`Signal<class_Signal>`;

- ``callable`` là tham chiếu đến :ref:`Callable<class_Callable>` được kết nối;

- ``flags`` là một tổ hợp của :ref:`ConnectFlags<enum_Object_ConnectFlags>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_signal_list:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_signal_list**\ (\ ) |const| :ref:`🔗<class_Object_method_get_signal_list>`

Trả về danh sách các signal hiện có dưới dạng một :ref:`Array<class_Array>` gồm các dictionary.

\ **Lưu ý:** Do cách triển khai, mỗi :ref:`Dictionary<class_Dictionary>` được định dạng rất giống với các giá trị được trả về bởi :ref:`get_method_list()<class_Object_method_get_method_list>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_get_translation_domain:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_translation_domain**\ (\ ) |const| :ref:`🔗<class_Object_method_get_translation_domain>`

Trả về tên của translation domain được :ref:`tr()<class_Object_method_tr>` và :ref:`tr_n()<class_Object_method_tr_n>` sử dụng. Xem thêm :ref:`TranslationServer<class_TranslationServer>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_has_connections:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_connections**\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_has_connections>`

Trả về ``true`` nếu tồn tại bất kỳ connection nào trên tên ``signal`` đã cho.

\ **Lưu ý:** Trong C#, ``signal`` phải ở dạng snake_case khi tham chiếu đến các phương thức Godot tích hợp sẵn. Nên sử dụng các tên được cung cấp trong class ``SignalName`` để tránh phải cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_has_meta:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_meta**\ (\ name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_has_meta>`

Trả về ``true`` nếu tìm thấy một mục metadata với ``name`` đã cho. Xem thêm :ref:`get_meta()<class_Object_method_get_meta>`, :ref:`set_meta()<class_Object_method_set_meta>` và :ref:`remove_meta()<class_Object_method_remove_meta>`.

\ **Lưu ý:** Tên của metadata phải là một identifier hợp lệ theo phương thức :ref:`StringName.is_valid_identifier()<class_StringName_method_is_valid_identifier>`.

\ **Lưu ý:** Metadata có tên bắt đầu bằng dấu gạch dưới (``_``) được xem là chỉ dành cho editor. Metadata chỉ dành cho editor không được hiển thị trong Inspector và không nên được chỉnh sửa, mặc dù vẫn có thể được tìm thấy bằng phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_has_method:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_method**\ (\ method\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_has_method>`

Trả về ``true`` nếu tên ``method`` đã cho tồn tại trong đối tượng.

\ **Lưu ý:** Trong C#, ``method`` phải ở dạng snake_case khi tham chiếu đến các phương thức Godot tích hợp sẵn. Nên sử dụng các tên được cung cấp trong class ``MethodName`` để tránh phải cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_has_signal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_signal**\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_has_signal>`

Trả về ``true`` nếu tên ``signal`` đã cho tồn tại trong đối tượng.

\ **Lưu ý:** Trong C#, ``signal`` phải ở dạng snake_case khi tham chiếu đến các signal Godot tích hợp sẵn. Nên sử dụng các tên được cung cấp trong class ``SignalName`` để tránh phải cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_has_user_signal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_user_signal**\ (\ signal\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_has_user_signal>`

Trả về ``true`` nếu tên ``signal`` của signal do người dùng định nghĩa đã cho tồn tại. Chỉ các signal được thêm bằng :ref:`add_user_signal()<class_Object_method_add_user_signal>` mới được bao gồm. Xem thêm :ref:`remove_user_signal()<class_Object_method_remove_user_signal>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_is_blocking_signals:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_blocking_signals**\ (\ ) |const| :ref:`🔗<class_Object_method_is_blocking_signals>`

Trả về ``true`` nếu đối tượng đang chặn không cho các signal của nó được phát. Xem :ref:`set_block_signals()<class_Object_method_set_block_signals>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_is_class:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_class**\ (\ class\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_is_class>`

Trả về ``true`` nếu đối tượng kế thừa từ ``class`` đã cho. Xem thêm :ref:`get_class()<class_Object_method_get_class>`.


.. tabs::

 .. code-tab:: gdscript

    var sprite2d = Sprite2D.new()
    sprite2d.is_class("Sprite2D") # Trả về true
    sprite2d.is_class("Node")     # Trả về true
    sprite2d.is_class("Node3D")   # Trả về false

 .. code-tab:: csharp

    var sprite2D = new Sprite2D();
    sprite2D.IsClass("Sprite2D"); // Trả về true
    sprite2D.IsClass("Node");     // Trả về true
    sprite2D.IsClass("Node3D");   // Trả về false



\ **Lưu ý:** Phương thức này bỏ qua các khai báo ``class_name`` trong script của đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_is_connected:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_connected**\ (\ signal\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`\ ) |const| :ref:`🔗<class_Object_method_is_connected>`

Trả về ``true`` nếu tồn tại connection giữa tên ``signal`` đã cho và ``callable``.

\ **Lưu ý:** Trong C#, ``signal`` phải ở dạng snake_case khi tham chiếu đến các signal Godot tích hợp sẵn. Nên sử dụng các tên được cung cấp trong class ``SignalName`` để tránh phải cấp phát một :ref:`StringName<class_StringName>` mới trong mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_is_queued_for_deletion:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_queued_for_deletion**\ (\ ) |const| :ref:`🔗<class_Object_method_is_queued_for_deletion>`

Trả về ``true`` nếu phương thức :ref:`Node.queue_free()<class_Node_method_queue_free>` hoặc :ref:`SceneTree.queue_delete()<class_SceneTree_method_queue_delete>` đã được gọi cho đối tượng.

\ **Lưu ý:** Phương thức này không trả về ``true`` trên các node con của node mà :ref:`Node.queue_free()<class_Node_method_queue_free>` đã được gọi, mặc dù chúng sẽ được giải phóng cùng với node cha.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_notification:

.. rst-class:: classref-method

|void| **notification**\ (\ what\: :ref:`int<class_int>`, reversed\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Object_method_notification>`

Gửi notification ``what`` đã cho đến tất cả class được đối tượng kế thừa, kích hoạt các lần gọi đến :ref:`_notification()<class_Object_private_method__notification>`, bắt đầu từ ancestor cao nhất (class **Object**) và đi xuống script của đối tượng.

Nếu ``reversed`` là ``true``, thứ tự gọi sẽ bị đảo ngược.


.. tabs::

 .. code-tab:: gdscript

    var player = Node2D.new()
    player.set_script(load("res://player.gd"))

    player.notification(NOTIFICATION_ENTER_TREE)
    # Thứ tự gọi là Object -> Node -> Node2D -> player.gd.

    player.notification(NOTIFICATION_ENTER_TREE, true)
    # Thứ tự gọi là player.gd -> Node2D -> Node -> Object.

 .. code-tab:: csharp

    var player = new Node2D();
    player.SetScript(GD.Load("res://player.gd"));

    player.Notification(NotificationEnterTree);
    // Thứ tự gọi là GodotObject -> Node -> Node2D -> player.gd.

    player.Notification(NotificationEnterTree, true);
    // Thứ tự gọi là player.gd -> Node2D -> Node -> GodotObject.



.. rst-class:: classref-item-separator

----

.. _class_Object_method_notify_property_list_changed:

.. rst-class:: classref-method

|void| **notify_property_list_changed**\ (\ ) :ref:`🔗<class_Object_method_notify_property_list_changed>`

Phát tín hiệu :ref:`property_list_changed<class_Object_signal_property_list_changed>`. Tín hiệu này chủ yếu được dùng để làm mới editor, nhờ đó Inspector và các editor plugin được cập nhật chính xác.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_property_can_revert:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **property_can_revert**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_property_can_revert>`

Trả về ``true`` nếu ``property`` đã cho có giá trị mặc định tùy chỉnh. Sử dụng :ref:`property_get_revert()<class_Object_method_property_get_revert>` để lấy giá trị mặc định của ``property``.

\ **Lưu ý:** Phương thức này được Inspector dock sử dụng để hiển thị biểu tượng hoàn tác. Đối tượng phải triển khai :ref:`_property_can_revert()<class_Object_private_method__property_can_revert>` để tùy chỉnh giá trị mặc định. Nếu :ref:`_property_can_revert()<class_Object_private_method__property_can_revert>` chưa được triển khai, phương thức này trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_property_get_revert:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **property_get_revert**\ (\ property\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_Object_method_property_get_revert>`

Trả về giá trị mặc định tùy chỉnh của ``property`` đã cho. Sử dụng :ref:`property_can_revert()<class_Object_method_property_can_revert>` để kiểm tra xem ``property`` có giá trị mặc định tùy chỉnh hay không.

\ **Lưu ý:** Phương thức này được Inspector dock sử dụng để hiển thị biểu tượng hoàn tác. Đối tượng phải triển khai :ref:`_property_get_revert()<class_Object_private_method__property_get_revert>` để tùy chỉnh giá trị mặc định. Nếu :ref:`_property_get_revert()<class_Object_private_method__property_get_revert>` chưa được triển khai, phương thức này trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_remove_meta:

.. rst-class:: classref-method

|void| **remove_meta**\ (\ name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Object_method_remove_meta>`

Xóa mục ``name`` đã cho khỏi metadata của đối tượng. Xem thêm :ref:`has_meta()<class_Object_method_has_meta>`, :ref:`get_meta()<class_Object_method_get_meta>` và :ref:`set_meta()<class_Object_method_set_meta>`.

\ **Lưu ý:** Tên của metadata phải là một identifier hợp lệ theo phương thức :ref:`StringName.is_valid_identifier()<class_StringName_method_is_valid_identifier>`.

\ **Lưu ý:** Metadata có tên bắt đầu bằng dấu gạch dưới (``_``) được xem là chỉ dành cho editor. Metadata chỉ dành cho editor không được hiển thị trong Inspector và không nên được chỉnh sửa, mặc dù vẫn có thể được tìm thấy bằng phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_remove_user_signal:

.. rst-class:: classref-method

|void| **remove_user_signal**\ (\ signal\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Object_method_remove_user_signal>`

Xóa user signal ``signal`` đã cho khỏi đối tượng. Xem thêm :ref:`add_user_signal()<class_Object_method_add_user_signal>` và :ref:`has_user_signal()<class_Object_method_has_user_signal>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set:

.. rst-class:: classref-method

|void| **set**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Object_method_set>`

Gán ``value`` cho ``property`` đã cho. Nếu property không tồn tại hoặc kiểu của ``value`` đã cho không khớp, sẽ không có gì xảy ra.


.. tabs::

 .. code-tab:: gdscript

    var node = Node2D.new()
    node.set("global_scale", Vector2(8, 2.5))
    print(node.global_scale) # In ra (8.0, 2.5)

 .. code-tab:: csharp

    var node = new Node2D();
    node.Set(Node2D.PropertyName.GlobalScale, new Vector2(8, 2.5f));
    GD.Print(node.GlobalScale); // In ra (8, 2.5)



\ **Lưu ý:** Trong C#, ``property`` phải ở dạng snake_case khi tham chiếu đến các Godot property dựng sẵn. Nên sử dụng các tên được cung cấp trong class ``PropertyName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới ở mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_block_signals:

.. rst-class:: classref-method

|void| **set_block_signals**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Object_method_set_block_signals>`

Nếu được đặt thành ``true``, đối tượng sẽ không thể phát tín hiệu. Do đó, :ref:`emit_signal()<class_Object_method_emit_signal>` và các kết nối tín hiệu sẽ không hoạt động cho đến khi được đặt thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_deferred:

.. rst-class:: classref-method

|void| **set_deferred**\ (\ property\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Object_method_set_deferred>`

Gán ``value`` cho ``property`` đã cho vào cuối frame hiện tại. Điều này tương đương với việc gọi :ref:`set()<class_Object_method_set>` thông qua :ref:`call_deferred()<class_Object_method_call_deferred>`.


.. tabs::

 .. code-tab:: gdscript

    var node = Node2D.new()
    add_child(node)

    node.rotation = 1.5
    node.set_deferred("rotation", 3.0)
    print(node.rotation) # In ra 1.5

    await get_tree().process_frame
    print(node.rotation) # In ra 3.0

 .. code-tab:: csharp

    var node = new Node2D();
    node.Rotation = 1.5f;
    node.SetDeferred(Node2D.PropertyName.Rotation, 3f);
    GD.Print(node.Rotation); // In ra 1.5

    await ToSignal(GetTree(), SceneTree.SignalName.ProcessFrame);
    GD.Print(node.Rotation); // In ra 3.0



\ **Lưu ý:** Trong C#, ``property`` phải ở dạng snake_case khi tham chiếu đến các Godot property dựng sẵn. Nên sử dụng các tên được cung cấp trong class ``PropertyName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới ở mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_indexed:

.. rst-class:: classref-method

|void| **set_indexed**\ (\ property_path\: :ref:`NodePath<class_NodePath>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Object_method_set_indexed>`

Gán một ``value`` mới cho property được xác định bằng ``property_path``. Đường dẫn phải là một :ref:`NodePath<class_NodePath>` tương đối so với đối tượng này và có thể sử dụng ký tự hai chấm (``:``) để truy cập các property lồng nhau.


.. tabs::

 .. code-tab:: gdscript

    var node = Node2D.new()
    node.set_indexed("position", Vector2(42, 0))
    node.set_indexed("position:y", -10)
    print(node.position) # In ra (42.0, -10.0)

 .. code-tab:: csharp

    var node = new Node2D();
    node.SetIndexed("position", new Vector2(42, 0));
    node.SetIndexed("position:y", -10);
    GD.Print(node.Position); // In ra (42, -10)



\ **Lưu ý:** Trong C#, ``property_path`` phải ở dạng snake_case khi tham chiếu đến các Godot property dựng sẵn. Nên sử dụng các tên được cung cấp trong class ``PropertyName`` để tránh cấp phát một :ref:`StringName<class_StringName>` mới ở mỗi lần gọi.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_message_translation:

.. rst-class:: classref-method

|void| **set_message_translation**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Object_method_set_message_translation>`

Nếu được đặt thành ``true``, cho phép đối tượng dịch các thông báo bằng :ref:`tr()<class_Object_method_tr>` và :ref:`tr_n()<class_Object_method_tr_n>`. Được bật theo mặc định. Xem thêm :ref:`can_translate_messages()<class_Object_method_can_translate_messages>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_meta:

.. rst-class:: classref-method

|void| **set_meta**\ (\ name\: :ref:`StringName<class_StringName>`, value\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Object_method_set_meta>`

Thêm hoặc thay đổi mục ``name`` bên trong metadata của đối tượng. ``value`` của metadata có thể là bất kỳ :ref:`Variant<class_Variant>` nào, mặc dù một số kiểu không thể được serialize chính xác.

Nếu ``value`` là ``null``, mục đó sẽ bị xóa. Đây là cách tương đương với việc sử dụng :ref:`remove_meta()<class_Object_method_remove_meta>`. Xem thêm :ref:`has_meta()<class_Object_method_has_meta>` và :ref:`get_meta()<class_Object_method_get_meta>`.

\ **Lưu ý:** Tên của metadata phải là một identifier hợp lệ theo phương thức :ref:`StringName.is_valid_identifier()<class_StringName_method_is_valid_identifier>`.

\ **Lưu ý:** Metadata có tên bắt đầu bằng dấu gạch dưới (``_``) được xem là chỉ dành cho editor. Metadata chỉ dành cho editor không được hiển thị trong Inspector và không nên được chỉnh sửa, mặc dù vẫn có thể được tìm thấy bằng phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_script:

.. rst-class:: classref-method

|void| **set_script**\ (\ script\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_Object_method_set_script>`

Gắn ``script`` vào đối tượng và khởi tạo nó. Do đó, :ref:`_init()<class_Object_private_method__init>` của script được gọi. Một :ref:`Script<class_Script>` được dùng để mở rộng chức năng của đối tượng.

Nếu đã có script, instance của script đó sẽ bị tách ra, đồng thời các giá trị property và state của nó sẽ bị mất. Các giá trị property dựng sẵn vẫn được giữ lại.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_set_translation_domain:

.. rst-class:: classref-method

|void| **set_translation_domain**\ (\ domain\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Object_method_set_translation_domain>`

Đặt tên của translation domain được :ref:`tr()<class_Object_method_tr>` và :ref:`tr_n()<class_Object_method_tr_n>` sử dụng. Xem thêm :ref:`TranslationServer<class_TranslationServer>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_to_string:

.. rst-class:: classref-method

:ref:`String<class_String>` **to_string**\ (\ ) :ref:`🔗<class_Object_method_to_string>`

Trả về một :ref:`String<class_String>` đại diện cho đối tượng. Mặc định là ``"<ClassName#RID>"``. Ghi đè :ref:`_to_string()<class_Object_private_method__to_string>` để tùy chỉnh biểu diễn chuỗi của đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_tr:

.. rst-class:: classref-method

:ref:`String<class_String>` **tr**\ (\ message\: :ref:`StringName<class_StringName>`, context\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Object_method_tr>`

Dịch một ``message`` bằng các translation catalog được cấu hình trong Project Settings. Có thể chỉ định thêm ``context`` để hỗ trợ quá trình dịch. Lưu ý rằng hầu hết các node :ref:`Control<class_Control>` đều tự động dịch chuỗi của chúng, vì vậy phương thức này chủ yếu hữu ích cho các chuỗi được format hoặc văn bản được vẽ tùy chỉnh.

Nếu :ref:`can_translate_messages()<class_Object_method_can_translate_messages>` là ``false`` hoặc không có bản dịch khả dụng, phương thức này trả về ``message`` mà không thay đổi. Xem :ref:`set_message_translation()<class_Object_method_set_message_translation>`.

Để xem các ví dụ chi tiết, hãy xem :doc:`Internationalizing games <../tutorials/i18n/internationalizing_games>`.

\ **Lưu ý:** Không thể sử dụng phương thức này nếu không có một instance **Object**, vì phương thức này yêu cầu phương thức :ref:`can_translate_messages()<class_Object_method_can_translate_messages>`. Để dịch chuỗi trong static context, hãy sử dụng :ref:`TranslationServer.translate()<class_TranslationServer_method_translate>`.

.. rst-class:: classref-item-separator

----

.. _class_Object_method_tr_n:

.. rst-class:: classref-method

:ref:`String<class_String>` **tr_n**\ (\ message\: :ref:`StringName<class_StringName>`, plural_message\: :ref:`StringName<class_StringName>`, n\: :ref:`int<class_int>`, context\: :ref:`StringName<class_StringName>` = &""\ ) |const| :ref:`🔗<class_Object_method_tr_n>`

Dịch một ``message`` hoặc ``plural_message`` bằng các translation catalog được cấu hình trong Project Settings. Có thể chỉ định thêm ``context`` để hỗ trợ quá trình dịch.

Nếu :ref:`can_translate_messages()<class_Object_method_can_translate_messages>` là ``false`` hoặc không có bản dịch khả dụng, phương thức này trả về ``message`` hoặc ``plural_message`` mà không thay đổi. Xem :ref:`set_message_translation()<class_Object_method_set_message_translation>`.

``n`` là số lượng hoặc con số của đối tượng được đề cập trong thông báo. Nó được hệ thống dịch sử dụng để lấy dạng số nhiều chính xác cho ngôn ngữ hiện tại.

Để xem các ví dụ chi tiết, hãy xem :doc:`Localization using gettext <../tutorials/i18n/localization_using_gettext>`.

\ **Lưu ý:** Số âm và số :ref:`float<class_float>` có thể không được áp dụng chính xác cho một số đối tượng có thể đếm được. Bạn nên xử lý các trường hợp này bằng :ref:`tr()<class_Object_method_tr>`.

\ **Lưu ý:** Không thể sử dụng phương thức này nếu không có một instance **Object**, vì phương thức này yêu cầu phương thức :ref:`can_translate_messages()<class_Object_method_can_translate_messages>`. Để dịch chuỗi trong static context, hãy sử dụng :ref:`TranslationServer.translate_plural()<class_TranslationServer_method_translate_plural>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
