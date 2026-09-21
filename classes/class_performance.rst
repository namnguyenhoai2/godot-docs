:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Performance.xml.

.. _class_Performance:

Hiệu năng
=========

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp dữ liệu liên quan đến hiệu năng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class này cung cấp quyền truy cập vào nhiều monitor khác nhau liên quan đến hiệu năng, chẳng hạn như mức sử dụng bộ nhớ, draw call và FPS. Đây chính là các giá trị được hiển thị trong tab **Monitor** thuộc bảng **Debugger** của editor. Bằng cách sử dụng phương thức :ref:`get_monitor()<class_Performance_method_get_monitor>` của class này, bạn có thể truy cập dữ liệu này từ code của mình.

Bạn có thể thêm monitor tùy chỉnh bằng phương thức :ref:`add_custom_monitor()<class_Performance_method_add_custom_monitor>`. Các monitor tùy chỉnh sẽ khả dụng trong tab **Monitor** thuộc bảng **Debugger** của editor, cùng với các monitor tích hợp sẵn.

\ **Lưu ý:** Một số monitor tích hợp sẵn chỉ khả dụng trong debug mode và sẽ luôn trả về ``0`` khi được sử dụng trong project được export ở release mode.

\ **Lưu ý:** Một số monitor tích hợp sẵn không được cập nhật theo thời gian thực vì lý do hiệu năng, nên có thể có độ trễ tối đa 1 giây giữa các thay đổi.

\ **Lưu ý:** Monitor tùy chỉnh không hỗ trợ giá trị âm. Các giá trị âm được giới hạn về 0.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_custom_monitor<class_Performance_method_add_custom_monitor>`\ (\ id\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`, arguments\: :ref:`Array<class_Array>` = [], type\: :ref:`MonitorType<enum_Performance_MonitorType>` = 0\ ) |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                                    | :ref:`get_custom_monitor<class_Performance_method_get_custom_monitor>`\ (\ id\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                      |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] | :ref:`get_custom_monitor_names<class_Performance_method_get_custom_monitor_names>`\ (\ )                                                                                                                                                                                    |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`                  | :ref:`get_custom_monitor_types<class_Performance_method_get_custom_monitor_types>`\ (\ )                                                                                                                                                                                    |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                        | :ref:`get_monitor<class_Performance_method_get_monitor>`\ (\ monitor\: :ref:`Monitor<enum_Performance_Monitor>`\ ) |const|                                                                                                                                                  |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_monitor_modification_time<class_Performance_method_get_monitor_modification_time>`\ (\ )                                                                                                                                                                          |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                          | :ref:`has_custom_monitor<class_Performance_method_has_custom_monitor>`\ (\ id\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                      |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_custom_monitor<class_Performance_method_remove_custom_monitor>`\ (\ id\: :ref:`StringName<class_StringName>`\ )                                                                                                                                                |
   +------------------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_Performance_Monitor:

.. rst-class:: classref-enumeration

enum **Monitor**: :ref:`🔗<enum_Performance_Monitor>`

.. _class_Performance_constant_TIME_FPS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **TIME_FPS** = ``0``

Số frame được render trong giây vừa qua. Chỉ số này chỉ được cập nhật một lần mỗi giây, ngay cả khi được truy vấn thường xuyên hơn. *Cao hơn là tốt hơn.*

.. _class_Performance_constant_TIME_PROCESS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **TIME_PROCESS** = ``1``

Thời gian cần để hoàn tất một frame, tính bằng giây. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_TIME_PHYSICS_PROCESS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **TIME_PHYSICS_PROCESS** = ``2``

Thời gian cần để hoàn tất một frame physics, tính bằng giây. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_TIME_NAVIGATION_PROCESS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **TIME_NAVIGATION_PROCESS** = ``3``

Thời gian cần để hoàn tất một bước navigation, tính bằng giây. Thời gian này bao gồm cả việc cập nhật navigation map và tính toán tránh va chạm của agent. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_MEMORY_STATIC:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **MEMORY_STATIC** = ``4``

Bộ nhớ static hiện đang được sử dụng, tính bằng byte. Không khả dụng trong các bản build release. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_MEMORY_STATIC_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **MEMORY_STATIC_MAX** = ``5``

Bộ nhớ static khả dụng. Không khả dụng trong các bản build release. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_MEMORY_MESSAGE_BUFFER_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **MEMORY_MESSAGE_BUFFER_MAX** = ``6``

Lượng bộ nhớ lớn nhất mà buffer của message queue đã sử dụng, tính bằng byte. Message queue được sử dụng cho các lần gọi hàm deferred và notification. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_OBJECT_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **OBJECT_COUNT** = ``7``

Số object hiện đang được khởi tạo (bao gồm cả node). *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_OBJECT_RESOURCE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **OBJECT_RESOURCE_COUNT** = ``8``

Số resource hiện đang được sử dụng. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_OBJECT_NODE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **OBJECT_NODE_COUNT** = ``9``

Số node hiện đang được khởi tạo trong scene tree. Số này cũng bao gồm root node. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_OBJECT_ORPHAN_NODE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **OBJECT_ORPHAN_NODE_COUNT** = ``10``

Số orphan node, tức là các node không có node thuộc scene tree làm parent. *Thấp hơn là tốt hơn.*\

\ **Lưu ý:** Chỉ khả dụng trong debug mode và sẽ luôn trả về ``0`` khi được sử dụng trong project được export ở release mode.

.. _class_Performance_constant_RENDER_TOTAL_OBJECTS_IN_FRAME:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **RENDER_TOTAL_OBJECTS_IN_FRAME** = ``11``

Tổng số object trong frame được render gần nhất. Chỉ số này không bao gồm các object bị cull (bằng cách ẩn node, frustum culling hoặc occlusion culling). *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_RENDER_TOTAL_PRIMITIVES_IN_FRAME:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **RENDER_TOTAL_PRIMITIVES_IN_FRAME** = ``12``

Tổng số vertex hoặc index được render trong frame được render gần nhất. Chỉ số này không bao gồm primitive từ các object bị cull (bằng cách ẩn node, frustum culling hoặc occlusion culling). Do depth prepass và shadow pass, số primitive luôn cao hơn số vertex thực tế trong scene (thường gấp đôi hoặc gấp ba số vertex ban đầu). *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_RENDER_TOTAL_DRAW_CALLS_IN_FRAME:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **RENDER_TOTAL_DRAW_CALLS_IN_FRAME** = ``13``

Tổng số draw call được thực hiện trong frame được render gần nhất. Chỉ số này không bao gồm các object bị cull (bằng cách ẩn node, frustum culling hoặc occlusion culling), vì chúng không tạo ra draw call. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_RENDER_VIDEO_MEM_USED:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **RENDER_VIDEO_MEM_USED** = ``14``

Lượng video memory được sử dụng (tổng memory của texture và vertex, tính bằng byte). Vì chỉ số này cũng bao gồm các allocation linh tinh, giá trị này luôn lớn hơn tổng của :ref:`RENDER_TEXTURE_MEM_USED<class_Performance_constant_RENDER_TEXTURE_MEM_USED>` và :ref:`RENDER_BUFFER_MEM_USED<class_Performance_constant_RENDER_BUFFER_MEM_USED>`. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_RENDER_TEXTURE_MEM_USED:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **RENDER_TEXTURE_MEM_USED** = ``15``

Lượng texture memory được sử dụng (tính bằng byte). *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_RENDER_BUFFER_MEM_USED:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **RENDER_BUFFER_MEM_USED** = ``16``

Lượng render buffer memory được sử dụng (tính bằng byte). *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_PHYSICS_2D_ACTIVE_OBJECTS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PHYSICS_2D_ACTIVE_OBJECTS** = ``17``

Số node :ref:`RigidBody2D<class_RigidBody2D>` đang hoạt động trong game. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_PHYSICS_2D_COLLISION_PAIRS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PHYSICS_2D_COLLISION_PAIRS** = ``18``

Số cặp collision trong 2D physics engine. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_PHYSICS_2D_ISLAND_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PHYSICS_2D_ISLAND_COUNT** = ``19``

Số island trong 2D physics engine. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_PHYSICS_3D_ACTIVE_OBJECTS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PHYSICS_3D_ACTIVE_OBJECTS** = ``20``

Số node :ref:`RigidBody3D<class_RigidBody3D>` và :ref:`VehicleBody3D<class_VehicleBody3D>` đang hoạt động trong game. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_PHYSICS_3D_COLLISION_PAIRS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PHYSICS_3D_COLLISION_PAIRS** = ``21``

Số cặp collision trong 3D physics engine. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_PHYSICS_3D_ISLAND_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PHYSICS_3D_ISLAND_COUNT** = ``22``

Số island trong 3D physics engine. *Thấp hơn là tốt hơn.*

.. _class_Performance_constant_AUDIO_OUTPUT_LATENCY:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **AUDIO_OUTPUT_LATENCY** = ``23``

Độ trễ output của :ref:`AudioServer<class_AudioServer>`. Tương đương với việc gọi :ref:`AudioServer.get_output_latency()<class_AudioServer_method_get_output_latency>`, không nên gọi hàm này ở mỗi frame.

.. _class_Performance_constant_NAVIGATION_ACTIVE_MAPS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_ACTIVE_MAPS** = ``24``

Số navigation map đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`. Số này cũng bao gồm các navigation map mặc định rỗng được tạo bởi các instance :ref:`World2D<class_World2D>` và :ref:`World3D<class_World3D>`.

.. _class_Performance_constant_NAVIGATION_REGION_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_REGION_COUNT** = ``25``

Số navigation region đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_AGENT_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_AGENT_COUNT** = ``26``

Số navigation agent đang hoạt động và xử lý việc tránh va chạm trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_LINK_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_LINK_COUNT** = ``27``

Số navigation link đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_POLYGON_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_POLYGON_COUNT** = ``28``

Số polygon của navigation mesh trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_EDGE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_EDGE_COUNT** = ``29``

Số edge của polygon navigation mesh trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_EDGE_MERGE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_EDGE_MERGE_COUNT** = ``30``

Số edge của polygon navigation mesh đã được merge do edge key bị trùng trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_EDGE_CONNECTION_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_EDGE_CONNECTION_COUNT** = ``31``

Số edge của polygon được xem là đã kết nối dựa trên khoảng cách giữa các edge trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_EDGE_FREE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_EDGE_FREE_COUNT** = ``32``

Số edge của polygon navigation mesh không thể được merge trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`. Các edge này vẫn có thể được kết nối dựa trên khoảng cách giữa các edge hoặc bằng link.

.. _class_Performance_constant_NAVIGATION_OBSTACLE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_OBSTACLE_COUNT** = ``33``

Số navigation obstacle đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_PIPELINE_COMPILATIONS_CANVAS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PIPELINE_COMPILATIONS_CANVAS** = ``34``

Số lần compile pipeline được kích hoạt bởi 2D canvas renderer.

.. _class_Performance_constant_PIPELINE_COMPILATIONS_MESH:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PIPELINE_COMPILATIONS_MESH** = ``35``

Số lần compile pipeline được kích hoạt khi load mesh. Các lần compile này sẽ khiến thời gian load lâu hơn vào lần đầu người dùng chạy game và pipeline được yêu cầu.

.. _class_Performance_constant_PIPELINE_COMPILATIONS_SURFACE:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PIPELINE_COMPILATIONS_SURFACE** = ``36``

Số lần compile pipeline được kích hoạt khi xây dựng surface cache trước khi render scene. Các lần compile này sẽ gây hiện tượng giật khi load scene lần đầu người dùng chạy game và pipeline được yêu cầu.

.. _class_Performance_constant_PIPELINE_COMPILATIONS_DRAW:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PIPELINE_COMPILATIONS_DRAW** = ``37``

Số lần biên dịch pipeline được kích hoạt trong khi vẽ cảnh. Những lần biên dịch này sẽ xuất hiện dưới dạng hiện tượng giật hình trong gameplay khi người dùng chạy trò chơi lần đầu và pipeline được yêu cầu.

.. _class_Performance_constant_PIPELINE_COMPILATIONS_SPECIALIZATION:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **PIPELINE_COMPILATIONS_SPECIALIZATION** = ``38``

Số lần biên dịch pipeline được kích hoạt để tối ưu hóa cảnh hiện tại. Những lần biên dịch này được thực hiện trong nền và hoàn toàn không gây ra hiện tượng giật hình.

.. _class_Performance_constant_NAVIGATION_2D_ACTIVE_MAPS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_ACTIVE_MAPS** = ``39``

Số bản đồ navigation đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>`. Số này cũng bao gồm các bản đồ navigation mặc định trống được tạo bởi các instance :ref:`World2D<class_World2D>`.

.. _class_Performance_constant_NAVIGATION_2D_REGION_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_REGION_COUNT** = ``40``

Số region navigation đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_AGENT_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_AGENT_COUNT** = ``41``

Số agent navigation đang hoạt động và xử lý avoidance trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_LINK_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_LINK_COUNT** = ``42``

Số link navigation đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_POLYGON_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_POLYGON_COUNT** = ``43``

Số polygon của navigation mesh trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_EDGE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_EDGE_COUNT** = ``44``

Số edge của polygon navigation mesh trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_EDGE_MERGE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_EDGE_MERGE_COUNT** = ``45``

Số edge của polygon navigation mesh được hợp nhất do các edge key trùng nhau trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_EDGE_CONNECTION_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_EDGE_CONNECTION_COUNT** = ``46``

Số edge polygon được xem là kết nối với nhau do độ gần của edge :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_2D_EDGE_FREE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_EDGE_FREE_COUNT** = ``47``

Số edge của polygon navigation mesh không thể được hợp nhất trong :ref:`NavigationServer2D<class_NavigationServer2D>`. Các edge này vẫn có thể được kết nối nhờ độ gần của edge hoặc bằng các link.

.. _class_Performance_constant_NAVIGATION_2D_OBSTACLE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_2D_OBSTACLE_COUNT** = ``48``

Số obstacle navigation đang hoạt động trong :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. _class_Performance_constant_NAVIGATION_3D_ACTIVE_MAPS:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_ACTIVE_MAPS** = ``49``

Số bản đồ navigation đang hoạt động trong :ref:`NavigationServer3D<class_NavigationServer3D>`. Số này cũng bao gồm các bản đồ navigation mặc định trống được tạo bởi các instance :ref:`World3D<class_World3D>`.

.. _class_Performance_constant_NAVIGATION_3D_REGION_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_REGION_COUNT** = ``50``

Số region navigation đang hoạt động trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_AGENT_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_AGENT_COUNT** = ``51``

Số agent navigation đang hoạt động và xử lý avoidance trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_LINK_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_LINK_COUNT** = ``52``

Số link navigation đang hoạt động trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_POLYGON_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_POLYGON_COUNT** = ``53``

Số polygon của navigation mesh trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_EDGE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_EDGE_COUNT** = ``54``

Số edge của polygon navigation mesh trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_EDGE_MERGE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_EDGE_MERGE_COUNT** = ``55``

Số edge của polygon navigation mesh được hợp nhất do các edge key trùng nhau trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_EDGE_CONNECTION_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_EDGE_CONNECTION_COUNT** = ``56``

Số edge polygon được xem là kết nối với nhau do độ gần của edge :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_NAVIGATION_3D_EDGE_FREE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_EDGE_FREE_COUNT** = ``57``

Số edge của polygon navigation mesh không thể được hợp nhất trong :ref:`NavigationServer3D<class_NavigationServer3D>`. Các edge này vẫn có thể được kết nối nhờ độ gần của edge hoặc bằng các link.

.. _class_Performance_constant_NAVIGATION_3D_OBSTACLE_COUNT:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **NAVIGATION_3D_OBSTACLE_COUNT** = ``58``

Số obstacle navigation đang hoạt động trong :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. _class_Performance_constant_MONITOR_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Monitor<enum_Performance_Monitor>` **MONITOR_MAX** = ``59``

Biểu thị kích thước của enum :ref:`Monitor<enum_Performance_Monitor>`.

.. rst-class:: classref-item-separator

----

.. _enum_Performance_MonitorType:

.. rst-class:: classref-enumeration

enum **MonitorType**: :ref:`🔗<enum_Performance_MonitorType>`

.. _class_Performance_constant_MONITOR_TYPE_QUANTITY:

.. rst-class:: classref-enumeration-constant

:ref:`MonitorType<enum_Performance_MonitorType>` **MONITOR_TYPE_QUANTITY** = ``0``

Đầu ra của monitor được định dạng dưới dạng giá trị số nguyên.

.. _class_Performance_constant_MONITOR_TYPE_MEMORY:

.. rst-class:: classref-enumeration-constant

:ref:`MonitorType<enum_Performance_MonitorType>` **MONITOR_TYPE_MEMORY** = ``1``

Đầu ra của monitor được định dạng dưới dạng bộ nhớ máy tính. Các giá trị được gửi phải biểu thị một số byte.

.. _class_Performance_constant_MONITOR_TYPE_TIME:

.. rst-class:: classref-enumeration-constant

:ref:`MonitorType<enum_Performance_MonitorType>` **MONITOR_TYPE_TIME** = ``2``

Đầu ra của monitor được định dạng dưới dạng thời gian tính bằng mili giây. Các giá trị được gửi phải biểu thị thời gian tính bằng giây (không phải mili giây).

.. _class_Performance_constant_MONITOR_TYPE_PERCENTAGE:

.. rst-class:: classref-enumeration-constant

:ref:`MonitorType<enum_Performance_MonitorType>` **MONITOR_TYPE_PERCENTAGE** = ``3``

Đầu ra của monitor được định dạng dưới dạng phần trăm. Các giá trị được gửi phải biểu thị giá trị phân số thay vì phần trăm trực tiếp, ví dụ ``0.5`` cho ``50.00%``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Performance_method_add_custom_monitor:

.. rst-class:: classref-method

|void| **add_custom_monitor**\ (\ id\: :ref:`StringName<class_StringName>`, callable\: :ref:`Callable<class_Callable>`, arguments\: :ref:`Array<class_Array>` = [], type\: :ref:`MonitorType<enum_Performance_MonitorType>` = 0\ ) :ref:`🔗<class_Performance_method_add_custom_monitor>`

Thêm một monitor tùy chỉnh với tên ``id``. Bạn có thể chỉ định category của monitor bằng cách sử dụng dấu gạch chéo phân cách trong ``id`` (ví dụ: ``"Game/NumberOfNPCs"``). Nếu có nhiều hơn một dấu gạch chéo phân cách, category mặc định sẽ được sử dụng. Category mặc định là ``"Custom"``. In lỗi nếu ``id`` đã tồn tại.


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        var monitor_value = Callable(self, "get_monitor_value")

        # Thêm monitor có tên "MyName" vào category "MyCategory".
        Performance.add_custom_monitor("MyCategory/MyMonitor", monitor_value)

        # Thêm monitor có tên "MyName" vào category "Custom".
        # Note: "MyCategory/MyMonitor" and "MyMonitor" have same name but different IDs, so the code is valid.
        Performance.add_custom_monitor("MyMonitor", monitor_value)

        # Thêm monitor có tên "MyName" vào category "Custom".
        # Note: "MyMonitor" and "Custom/MyMonitor" have same name and same category but different IDs, so the code is valid.
        Performance.add_custom_monitor("Custom/MyMonitor", monitor_value)

        # Thêm monitor có tên "MyCategoryOne/MyCategoryTwo/MyMonitor" vào category "Custom".
        Performance.add_custom_monitor("MyCategoryOne/MyCategoryTwo/MyMonitor", monitor_value)

    func get_monitor_value():
        return randi() % 25

 .. code-tab:: csharp

    public override void _Ready()
    {
        var monitorValue = new Callable(this, MethodName.GetMonitorValue);

        // Thêm monitor có tên "MyName" vào category "MyCategory".
        Performance.AddCustomMonitor("MyCategory/MyMonitor", monitorValue);
        // Thêm monitor có tên "MyName" vào category "Custom".
        // Note: "MyCategory/MyMonitor" and "MyMonitor" have same name but different ids so the code is valid.
        Performance.AddCustomMonitor("MyMonitor", monitorValue);

        // Thêm monitor có tên "MyName" vào category "Custom".
        // Note: "MyMonitor" and "Custom/MyMonitor" have same name and same category but different ids so the code is valid.
        Performance.AddCustomMonitor("Custom/MyMonitor", monitorValue);

        // Thêm monitor có tên "MyCategoryOne/MyCategoryTwo/MyMonitor" vào category "Custom".
        Performance.AddCustomMonitor("MyCategoryOne/MyCategoryTwo/MyMonitor", monitorValue);
    }

    public int GetMonitorValue()
    {
        return GD.Randi() % 25;
    }



Trình debugger gọi callable để lấy giá trị của monitor tùy chỉnh. Callable phải trả về một số nguyên hoặc số dấu phẩy động bằng 0 hoặc dương.

Các callable được gọi với các đối số được cung cấp trong mảng arguments.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_get_custom_monitor:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **get_custom_monitor**\ (\ id\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Performance_method_get_custom_monitor>`

Trả về giá trị của monitor tùy chỉnh có ``id`` được chỉ định. Callable được gọi để lấy giá trị của monitor tùy chỉnh. Xem thêm :ref:`has_custom_monitor()<class_Performance_method_has_custom_monitor>`. In lỗi nếu ``id`` được chỉ định không tồn tại.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_get_custom_monitor_names:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] **get_custom_monitor_names**\ (\ ) :ref:`🔗<class_Performance_method_get_custom_monitor_names>`

Trả về tên của các monitor tùy chỉnh đang hoạt động trong một :ref:`Array<class_Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_get_custom_monitor_types:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_custom_monitor_types**\ (\ ) :ref:`🔗<class_Performance_method_get_custom_monitor_types>`

Trả về các giá trị :ref:`MonitorType<enum_Performance_MonitorType>` của những monitor tùy chỉnh đang hoạt động trong một :ref:`Array<class_Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_get_monitor:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_monitor**\ (\ monitor\: :ref:`Monitor<enum_Performance_Monitor>`\ ) |const| :ref:`🔗<class_Performance_method_get_monitor>`

Trả về giá trị của một trong các monitor tích hợp hiện có. Bạn nên cung cấp một trong các hằng số :ref:`Monitor<enum_Performance_Monitor>` làm đối số, như sau:


.. tabs::

 .. code-tab:: gdscript

    print(Performance.get_monitor(Performance.TIME_FPS)) # In FPS ra console.

 .. code-tab:: csharp

    GD.Print(Performance.GetMonitor(Performance.Monitor.TimeFps)); // In FPS ra console.



Xem :ref:`get_custom_monitor()<class_Performance_method_get_custom_monitor>` để truy vấn giá trị của các performance monitor tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_get_monitor_modification_time:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_monitor_modification_time**\ (\ ) :ref:`🔗<class_Performance_method_get_monitor_modification_time>`

Trả về tick cuối cùng tại đó monitor tùy chỉnh được thêm/xóa (tính bằng micro giây kể từ khi engine khởi động). Giá trị này được đặt thành :ref:`Time.get_ticks_usec()<class_Time_method_get_ticks_usec>` khi monitor được cập nhật.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_has_custom_monitor:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_custom_monitor**\ (\ id\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Performance_method_has_custom_monitor>`

Trả về ``true`` nếu monitor tùy chỉnh có ``id`` đã cho tồn tại, ngược lại trả về ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Performance_method_remove_custom_monitor:

.. rst-class:: classref-method

|void| **remove_custom_monitor**\ (\ id\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_Performance_method_remove_custom_monitor>`

Xóa monitor tùy chỉnh có ``id`` đã cho. In lỗi nếu ``id`` đã không còn tồn tại.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
