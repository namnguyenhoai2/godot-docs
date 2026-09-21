:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationAgent3D.xml.

.. _class_NavigationAgent3D:

NavigationAgent3D
=================

**Thử nghiệm:** Lớp này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một agent 3D dùng để tìm đường đến một vị trí trong khi tránh chướng ngại vật.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một agent 3D dùng để tìm đường đến một vị trí trong khi tránh các chướng ngại vật tĩnh và động. Phép tính này có thể được node cha sử dụng để di chuyển node đó theo đường đi một cách động. Cần có dữ liệu navigation để hoạt động chính xác.

Các chướng ngại vật động được tránh bằng cơ chế tránh va chạm RVO. Việc tránh được tính toán trước bước vật lý, vì vậy thông tin tìm đường có thể được sử dụng an toàn trong bước vật lý.

\ **Lưu ý:** Sau khi thiết lập thuộc tính :ref:`target_position<class_NavigationAgent3D_property_target_position>`, phải sử dụng phương thức :ref:`get_next_path_position()<class_NavigationAgent3D_method_get_next_path_position>` một lần trong mỗi frame vật lý để cập nhật logic đường đi nội bộ của navigation agent. Vị trí vector mà phương thức này trả về nên được sử dụng làm vị trí di chuyển tiếp theo cho node cha của agent.

\ **Lưu ý:** Một số phương thức của lớp này, chẳng hạn như :ref:`get_next_path_position()<class_NavigationAgent3D_method_get_next_path_position>`, có thể kích hoạt phép tính đường đi mới. Việc gọi các phương thức này trong callback của bạn đối với signal của agent, chẳng hạn như :ref:`waypoint_reached<class_NavigationAgent3D_signal_waypoint_reached>`, có thể gây đệ quy vô hạn. Bạn nên gọi các phương thức này trong bước vật lý hoặc, nếu không, trì hoãn việc gọi chúng đến cuối frame (xem :ref:`Object.call_deferred()<class_Object_method_call_deferred>` hoặc :ref:`Object.CONNECT_DEFERRED<class_Object_constant_CONNECT_DEFERRED>`).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationAgents <../tutorials/navigation/navigation_using_navigationagents>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`avoidance_enabled<class_NavigationAgent3D_property_avoidance_enabled>`                       | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`avoidance_layers<class_NavigationAgent3D_property_avoidance_layers>`                         | ``1``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`avoidance_mask<class_NavigationAgent3D_property_avoidance_mask>`                             | ``1``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`avoidance_priority<class_NavigationAgent3D_property_avoidance_priority>`                     | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`debug_enabled<class_NavigationAgent3D_property_debug_enabled>`                               | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`                                                                      | :ref:`debug_path_custom_color<class_NavigationAgent3D_property_debug_path_custom_color>`           | ``Color(1, 1, 1, 1)`` |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`debug_path_custom_point_size<class_NavigationAgent3D_property_debug_path_custom_point_size>` | ``4.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`debug_use_custom<class_NavigationAgent3D_property_debug_use_custom>`                         | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`height<class_NavigationAgent3D_property_height>`                                             | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`keep_y_velocity<class_NavigationAgent3D_property_keep_y_velocity>`                           | ``true``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`max_neighbors<class_NavigationAgent3D_property_max_neighbors>`                               | ``10``                |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`max_speed<class_NavigationAgent3D_property_max_speed>`                                       | ``10.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`navigation_layers<class_NavigationAgent3D_property_navigation_layers>`                       | ``1``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`neighbor_distance<class_NavigationAgent3D_property_neighbor_distance>`                       | ``50.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_desired_distance<class_NavigationAgent3D_property_path_desired_distance>`               | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_height_offset<class_NavigationAgent3D_property_path_height_offset>`                     | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_max_distance<class_NavigationAgent3D_property_path_max_distance>`                       | ``5.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\] | :ref:`path_metadata_flags<class_NavigationAgent3D_property_path_metadata_flags>`                   | ``7``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>`             | :ref:`path_postprocessing<class_NavigationAgent3D_property_path_postprocessing>`                   | ``0``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_length<class_NavigationAgent3D_property_path_return_max_length>`             | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_radius<class_NavigationAgent3D_property_path_return_max_radius>`             | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_search_max_distance<class_NavigationAgent3D_property_path_search_max_distance>`         | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`path_search_max_polygons<class_NavigationAgent3D_property_path_search_max_polygons>`         | ``4096``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>`         | :ref:`pathfinding_algorithm<class_NavigationAgent3D_property_pathfinding_algorithm>`               | ``0``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`radius<class_NavigationAgent3D_property_radius>`                                             | ``0.5``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`simplify_epsilon<class_NavigationAgent3D_property_simplify_epsilon>`                         | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`simplify_path<class_NavigationAgent3D_property_simplify_path>`                               | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`target_desired_distance<class_NavigationAgent3D_property_target_desired_distance>`           | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector3<class_Vector3>`                                                                  | :ref:`target_position<class_NavigationAgent3D_property_target_position>`                           | ``Vector3(0, 0, 0)``  |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`time_horizon_agents<class_NavigationAgent3D_property_time_horizon_agents>`                   | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`time_horizon_obstacles<class_NavigationAgent3D_property_time_horizon_obstacles>`             | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`use_3d_avoidance<class_NavigationAgent3D_property_use_3d_avoidance>`                         | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector3<class_Vector3>`                                                                  | :ref:`velocity<class_NavigationAgent3D_property_velocity>`                                         | ``Vector3(0, 0, 0)``  |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                             | :ref:`distance_to_target<class_NavigationAgent3D_method_distance_to_target>`\ (\ ) |const|                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`get_avoidance_layer_value<class_NavigationAgent3D_method_get_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`get_avoidance_mask_value<class_NavigationAgent3D_method_get_avoidance_mask_value>`\ (\ mask_number\: :ref:`int<class_int>`\ ) |const|                               |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`                   | :ref:`get_current_navigation_path<class_NavigationAgent3D_method_get_current_navigation_path>`\ (\ ) |const|                                                              |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                 | :ref:`get_current_navigation_path_index<class_NavigationAgent3D_method_get_current_navigation_path_index>`\ (\ ) |const|                                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NavigationPathQueryResult3D<class_NavigationPathQueryResult3D>` | :ref:`get_current_navigation_result<class_NavigationAgent3D_method_get_current_navigation_result>`\ (\ ) |const|                                                          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                         | :ref:`get_final_position<class_NavigationAgent3D_method_get_final_position>`\ (\ )                                                                                        |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`get_navigation_layer_value<class_NavigationAgent3D_method_get_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                                 | :ref:`get_navigation_map<class_NavigationAgent3D_method_get_navigation_map>`\ (\ ) |const|                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                         | :ref:`get_next_path_position<class_NavigationAgent3D_method_get_next_path_position>`\ (\ )                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                             | :ref:`get_path_length<class_NavigationAgent3D_method_get_path_length>`\ (\ ) |const|                                                                                      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                                 | :ref:`get_rid<class_NavigationAgent3D_method_get_rid>`\ (\ ) |const|                                                                                                      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`is_navigation_finished<class_NavigationAgent3D_method_is_navigation_finished>`\ (\ )                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`is_target_reachable<class_NavigationAgent3D_method_is_target_reachable>`\ (\ )                                                                                      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`is_target_reached<class_NavigationAgent3D_method_is_target_reached>`\ (\ ) |const|                                                                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_avoidance_layer_value<class_NavigationAgent3D_method_set_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )   |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_avoidance_mask_value<class_NavigationAgent3D_method_set_avoidance_mask_value>`\ (\ mask_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_navigation_layer_value<class_NavigationAgent3D_method_set_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_navigation_map<class_NavigationAgent3D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_velocity_forced<class_NavigationAgent3D_method_set_velocity_forced>`\ (\ velocity\: :ref:`Vector3<class_Vector3>`\ )                                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_NavigationAgent3D_signal_link_reached:

.. rst-class:: classref-signal

**link_reached**\ (\ details\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_NavigationAgent3D_signal_link_reached>`

Phát signal khi agent đến một navigation link. Được phát khi agent di chuyển đến trong phạm vi :ref:`path_desired_distance<class_NavigationAgent3D_property_path_desired_distance>` so với vị trí tiếp theo trên đường đi, nếu vị trí đó là một navigation link.

Dictionary details có thể chứa các key sau, tùy thuộc vào giá trị của :ref:`path_metadata_flags<class_NavigationAgent3D_property_path_metadata_flags>`:

- ``position``: Vị trí bắt đầu của link đã đến.

- ``type``: Luôn là :ref:`NavigationPathQueryResult3D.PATH_SEGMENT_TYPE_LINK<class_NavigationPathQueryResult3D_constant_PATH_SEGMENT_TYPE_LINK>`.

- ``rid``: :ref:`RID<class_RID>` của link.

- ``owner``: Đối tượng quản lý link (thường là :ref:`NavigationLink3D<class_NavigationLink3D>`).

- ``link_entry_position``: Nếu ``owner`` khả dụng và owner là một :ref:`NavigationLink3D<class_NavigationLink3D>`, giá trị này sẽ chứa vị trí global của điểm trên link mà agent đang đi vào.

- ``link_exit_position``: Nếu ``owner`` khả dụng và owner là một :ref:`NavigationLink3D<class_NavigationLink3D>`, giá trị này sẽ chứa vị trí global của điểm trên link mà agent đang đi ra.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_signal_navigation_finished:

.. rst-class:: classref-signal

**navigation_finished**\ (\ ) :ref:`🔗<class_NavigationAgent3D_signal_navigation_finished>`

Phát signal khi navigation của agent hoàn tất. Nếu target có thể đến được, navigation kết thúc khi đến target. Nếu target không thể đến được, navigation kết thúc khi đến waypoint cuối cùng của đường đi. Signal này chỉ được phát một lần cho mỗi đường đi đã tải.

Signal này sẽ được phát ngay sau :ref:`target_reached<class_NavigationAgent3D_signal_target_reached>` khi target có thể đến được.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_signal_path_changed:

.. rst-class:: classref-signal

**path_changed**\ (\ ) :ref:`🔗<class_NavigationAgent3D_signal_path_changed>`

Được phát khi agent phải cập nhật đường đi đã tải:

- vì đường đi trước đó đang trống.

- vì navigation map đã thay đổi.

- vì agent đã bị đẩy ra xa segment hiện tại của đường đi hơn :ref:`path_max_distance<class_NavigationAgent3D_property_path_max_distance>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_signal_target_reached:

.. rst-class:: classref-signal

**target_reached**\ (\ ) :ref:`🔗<class_NavigationAgent3D_signal_target_reached>`

Phát signal khi agent đến target, tức là agent di chuyển đến trong phạm vi :ref:`target_desired_distance<class_NavigationAgent3D_property_target_desired_distance>` so với :ref:`target_position<class_NavigationAgent3D_property_target_position>`. Signal này chỉ được phát một lần cho mỗi đường đi đã tải.

Signal này sẽ được phát ngay trước :ref:`navigation_finished<class_NavigationAgent3D_signal_navigation_finished>` khi target có thể đến được.

Không phải lúc nào cũng có thể đến target, nhưng luôn phải có thể đến vị trí cuối cùng. Xem :ref:`get_final_position()<class_NavigationAgent3D_method_get_final_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_signal_velocity_computed:

.. rst-class:: classref-signal

**velocity_computed**\ (\ safe_velocity\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_NavigationAgent3D_signal_velocity_computed>`

Thông báo khi velocity tránh va chạm được tính toán. Được phát sau mỗi lần cập nhật miễn là :ref:`avoidance_enabled<class_NavigationAgent3D_property_avoidance_enabled>` là ``true`` và agent có navigation map.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_signal_waypoint_reached:

.. rst-class:: classref-signal

**waypoint_reached**\ (\ details\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_NavigationAgent3D_signal_waypoint_reached>`

Phát signal khi agent đến một waypoint. Được phát khi agent di chuyển đến trong phạm vi :ref:`path_desired_distance<class_NavigationAgent3D_property_path_desired_distance>` so với vị trí tiếp theo trên đường đi.

Dictionary details có thể chứa các key sau, tùy thuộc vào giá trị của :ref:`path_metadata_flags<class_NavigationAgent3D_property_path_metadata_flags>`:

- ``position``: Vị trí của waypoint đã đến.

- ``type``: Loại navigation primitive (region hoặc link) chứa waypoint này.

- ``rid``: :ref:`RID<class_RID>` của navigation primitive chứa waypoint (region hoặc link).

- ``owner``: Đối tượng quản lý navigation primitive chứa waypoint (region hoặc link).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationAgent3D_property_avoidance_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **avoidance_enabled** = ``false`` :ref:`🔗<class_NavigationAgent3D_property_avoidance_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_avoidance_enabled**\ (\ )

Nếu ``true``, agent được đăng ký callback tránh RVO trên :ref:`NavigationServer3D<class_NavigationServer3D>`. Khi thiết lập :ref:`velocity<class_NavigationAgent3D_property_velocity>` và quá trình xử lý hoàn tất, một Vector3 ``safe_velocity`` sẽ được nhận thông qua kết nối signal đến :ref:`velocity_computed<class_NavigationAgent3D_signal_velocity_computed>`. Việc xử lý tránh với nhiều agent đã đăng ký có chi phí hiệu năng đáng kể và chỉ nên được bật trên các agent hiện đang cần tính năng này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_avoidance_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **avoidance_layers** = ``1`` :ref:`🔗<class_NavigationAgent3D_property_avoidance_layers>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_avoidance_layers**\ (\ )

Một bitfield xác định các lớp tránh cho NavigationAgent này. Các agent khác có bit tương ứng trên :ref:`avoidance_mask<class_NavigationAgent3D_property_avoidance_mask>` sẽ tránh agent này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_avoidance_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **avoidance_mask** = ``1`` :ref:`🔗<class_NavigationAgent3D_property_avoidance_mask>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_avoidance_mask**\ (\ )

Một bitfield xác định các agent tránh và chướng ngại vật khác mà NavigationAgent này sẽ tránh khi một bit khớp với ít nhất một bit trong :ref:`avoidance_layers<class_NavigationAgent3D_property_avoidance_layers>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_avoidance_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **avoidance_priority** = ``1.0`` :ref:`🔗<class_NavigationAgent3D_property_avoidance_priority>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_avoidance_priority**\ (\ )

Agent không điều chỉnh velocity để tránh các agent khác khớp với :ref:`avoidance_mask<class_NavigationAgent3D_property_avoidance_mask>` nhưng có :ref:`avoidance_priority<class_NavigationAgent3D_property_avoidance_priority>` thấp hơn. Do đó, các agent khác có priority thấp hơn sẽ phải điều chỉnh velocity nhiều hơn để tránh va chạm với agent này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_debug_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **debug_enabled** = ``false`` :ref:`🔗<class_NavigationAgent3D_property_debug_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_debug_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_debug_enabled**\ (\ )

Nếu ``true``, hiển thị các hình ảnh debug cho agent này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_debug_path_custom_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **debug_path_custom_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_NavigationAgent3D_property_debug_path_custom_color>`

.. rst-class:: classref-property-setget

- |void| **set_debug_path_custom_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_debug_path_custom_color**\ (\ )

Nếu :ref:`debug_use_custom<class_NavigationAgent3D_property_debug_use_custom>` là ``true``, sử dụng màu này cho agent thay vì màu global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_debug_path_custom_point_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **debug_path_custom_point_size** = ``4.0`` :ref:`🔗<class_NavigationAgent3D_property_debug_path_custom_point_size>`

.. rst-class:: classref-property-setget

- |void| **set_debug_path_custom_point_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_debug_path_custom_point_size**\ (\ )

Nếu :ref:`debug_use_custom<class_NavigationAgent3D_property_debug_use_custom>` là ``true``, sử dụng kích thước điểm đã rasterize này để kết xuất các điểm đường đi cho agent thay vì kích thước điểm global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_debug_use_custom:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **debug_use_custom** = ``false`` :ref:`🔗<class_NavigationAgent3D_property_debug_use_custom>`

.. rst-class:: classref-property-setget

- |void| **set_debug_use_custom**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_debug_use_custom**\ (\ )

Nếu ``true``, sử dụng :ref:`debug_path_custom_color<class_NavigationAgent3D_property_debug_path_custom_color>` đã xác định cho agent này thay vì màu global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``1.0`` :ref:`🔗<class_NavigationAgent3D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Chiều cao của avoidance agent. Trong avoidance 2D, các agent sẽ bỏ qua những agent hoặc chướng ngại vật khác nằm cao hơn hoặc thấp hơn vị trí hiện tại + height của chúng. Không có tác dụng trong avoidance 3D, vốn chỉ sử dụng các sphere bán kính.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_keep_y_velocity:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **keep_y_velocity** = ``true`` :ref:`🔗<class_NavigationAgent3D_property_keep_y_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_keep_y_velocity**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_keep_y_velocity**\ (\ )

Nếu ``true``, và agent sử dụng tránh va chạm 2D, nó sẽ ghi nhớ vận tốc theo trục y đã thiết lập và áp dụng lại vận tốc đó sau bước tránh. Mặc dù tránh va chạm 2D không có trục y và mô phỏng trên một mặt phẳng, thiết lập này có thể giúp giảm hiện tượng clipping rõ ràng nhất trên hình học 3D không bằng phẳng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_max_neighbors:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_neighbors** = ``10`` :ref:`🔗<class_NavigationAgent3D_property_max_neighbors>`

.. rst-class:: classref-property-setget

- |void| **set_max_neighbors**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_neighbors**\ (\ )

Số lượng neighbor tối đa mà agent sẽ xem xét.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_max_speed:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_speed** = ``10.0`` :ref:`🔗<class_NavigationAgent3D_property_max_speed>`

.. rst-class:: classref-property-setget

- |void| **set_max_speed**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_speed**\ (\ )

Tốc độ tối đa mà một agent có thể di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationAgent3D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Một bitfield xác định các navigation layer của navigation region mà agent này sẽ sử dụng để tính toán path. Việc thay đổi thuộc tính này trong runtime sẽ xóa navigation path hiện tại và tạo một path mới theo các navigation layer mới.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_neighbor_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **neighbor_distance** = ``50.0`` :ref:`🔗<class_NavigationAgent3D_property_neighbor_distance>`

.. rst-class:: classref-property-setget

- |void| **set_neighbor_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_neighbor_distance**\ (\ )

Khoảng cách dùng để tìm kiếm các agent khác.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_desired_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_desired_distance** = ``1.0`` :ref:`🔗<class_NavigationAgent3D_property_path_desired_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_desired_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_desired_distance**\ (\ )

Ngưỡng khoảng cách trước khi một điểm trên path được xem là đã đến. Điều này cho phép agent không cần phải chạm chính xác vào một điểm trên path mà chỉ cần đến khu vực chung quanh điểm đó. Nếu giá trị này được đặt quá cao, NavigationAgent sẽ bỏ qua các điểm trên path, điều này có thể khiến nó rời khỏi navigation mesh. Nếu giá trị này được đặt quá thấp, NavigationAgent sẽ bị kẹt trong vòng lặp repath vì nó sẽ liên tục đi quá khoảng cách đến điểm tiếp theo trong mỗi lần cập nhật physics frame.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_height_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_height_offset** = ``0.0`` :ref:`🔗<class_NavigationAgent3D_property_path_height_offset>`

.. rst-class:: classref-property-setget

- |void| **set_path_height_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_height_offset**\ (\ )

Độ lệch chiều cao được trừ khỏi giá trị trục y của mọi vị trí vector trên path của NavigationAgent này. Độ lệch chiều cao của NavigationAgent không thay đổi hoặc ảnh hưởng đến navigation mesh hay kết quả truy vấn pathfinding. Cần có thêm các navigation map sử dụng những region có navigation mesh được developer bake với các giá trị radius hoặc height phù hợp của agent để hỗ trợ các agent có kích thước khác nhau.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_max_distance** = ``5.0`` :ref:`🔗<class_NavigationAgent3D_property_path_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_max_distance**\ (\ )

Khoảng cách tối đa mà agent được phép cách xa path lý tưởng đến vị trí cuối. Điều này có thể xảy ra do cố gắng tránh va chạm. Khi vượt quá khoảng cách tối đa, path lý tưởng sẽ được tính toán lại.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_metadata_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\] **path_metadata_flags** = ``7`` :ref:`🔗<class_NavigationAgent3D_property_path_metadata_flags>`

.. rst-class:: classref-property-setget

- |void| **set_path_metadata_flags**\ (\ value\: |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\]\ ) - |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters3D_PathMetadataFlags>`\] **get_path_metadata_flags**\ (\ )

Thông tin bổ sung được trả về cùng navigation path.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_postprocessing:

.. rst-class:: classref-property

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **path_postprocessing** = ``0`` :ref:`🔗<class_NavigationAgent3D_property_path_postprocessing>`

.. rst-class:: classref-property-setget

- |void| **set_path_postprocessing**\ (\ value\: :ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>`\ ) - :ref:`PathPostProcessing<enum_NavigationPathQueryParameters3D_PathPostProcessing>` **get_path_postprocessing**\ (\ )

Hoạt động hậu xử lý path được áp dụng cho hành lang path thô do :ref:`pathfinding_algorithm<class_NavigationAgent3D_property_pathfinding_algorithm>` tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_return_max_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_length** = ``0.0`` :ref:`🔗<class_NavigationAgent3D_property_path_return_max_length>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_length**\ (\ )

Độ dài tối đa được phép của path trả về theo đơn vị world. Path sẽ bị cắt khi vượt quá độ dài này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_return_max_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_radius** = ``0.0`` :ref:`🔗<class_NavigationAgent3D_property_path_return_max_radius>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_radius**\ (\ )

Bán kính tối đa được phép theo đơn vị world mà path trả về có thể cách xa điểm bắt đầu của path. Path sẽ bị cắt khi vượt quá bán kính này. So với :ref:`path_return_max_length<class_NavigationAgent3D_property_path_return_max_length>`, thuộc tính này cho phép agent đi xa hơn tương ứng, nếu cần đi vòng qua một góc.

\ **Lưu ý:** Thao tác này sẽ thực hiện sphere clip và chỉ xét các điểm thực tế trên navigation mesh path, trong đó vị trí đầu tiên trên path là tâm của sphere.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_search_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_search_max_distance** = ``0.0`` :ref:`🔗<class_NavigationAgent3D_property_path_search_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_search_max_distance**\ (\ )

Khoảng cách tối đa mà một polygon được tìm kiếm có thể cách xa polygon bắt đầu trước khi pathfinding hủy việc tìm path đến polygon vị trí mục tiêu (có thể không thể đến được hoặc ở rất xa). Trong trường hợp này, pathfinding sẽ đặt lại và xây dựng path từ polygon bắt đầu đến polygon được tìm thấy là gần vị trí mục tiêu nhất cho đến thời điểm đó. Giá trị ``0`` hoặc thấp hơn được tính là không giới hạn. Khi không giới hạn, pathfinding sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí mục tiêu hoặc đã dùng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_path_search_max_polygons:

.. rst-class:: classref-property

:ref:`int<class_int>` **path_search_max_polygons** = ``4096`` :ref:`🔗<class_NavigationAgent3D_property_path_search_max_polygons>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_polygons**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_path_search_max_polygons**\ (\ )

Số lượng polygon tối đa được tìm kiếm trước khi pathfinding hủy việc tìm path đến polygon vị trí mục tiêu (có thể không thể đến được hoặc ở rất xa). Trong trường hợp này, pathfinding sẽ đặt lại và xây dựng path từ polygon bắt đầu đến polygon được tìm thấy là gần vị trí mục tiêu nhất cho đến thời điểm đó. Giá trị ``0`` hoặc thấp hơn được tính là không giới hạn. Khi không giới hạn, pathfinding sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí mục tiêu hoặc đã dùng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_pathfinding_algorithm:

.. rst-class:: classref-property

:ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>` **pathfinding_algorithm** = ``0`` :ref:`🔗<class_NavigationAgent3D_property_pathfinding_algorithm>`

.. rst-class:: classref-property-setget

- |void| **set_pathfinding_algorithm**\ (\ value\: :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>`\ ) - :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters3D_PathfindingAlgorithm>` **get_pathfinding_algorithm**\ (\ )

Thuật toán pathfinding được sử dụng trong truy vấn path.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.5`` :ref:`🔗<class_NavigationAgent3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của avoidance agent. Đây là "body" của avoidance agent, không phải bán kính bắt đầu của thao tác tránh (được điều khiển bởi :ref:`neighbor_distance<class_NavigationAgent3D_property_neighbor_distance>`).

Không ảnh hưởng đến pathfinding thông thường. Để thay đổi bán kính pathfinding của actor, hãy bake các resource :ref:`NavigationMesh<class_NavigationMesh>` với property :ref:`NavigationMesh.agent_radius<class_NavigationMesh_property_agent_radius>` khác và sử dụng các navigation map khác nhau cho từng kích thước actor.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_simplify_epsilon:

.. rst-class:: classref-property

:ref:`float<class_float>` **simplify_epsilon** = ``0.0`` :ref:`🔗<class_NavigationAgent3D_property_simplify_epsilon>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_epsilon**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_simplify_epsilon**\ (\ )

Mức độ đơn giản hóa path theo đơn vị world.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_simplify_path:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **simplify_path** = ``false`` :ref:`🔗<class_NavigationAgent3D_property_simplify_path>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_path**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_simplify_path**\ (\ )

Nếu ``true``, một phiên bản đơn giản hóa của path sẽ được trả về sau khi loại bỏ các điểm path không quan trọng. Mức độ đơn giản hóa được điều khiển bởi :ref:`simplify_epsilon<class_NavigationAgent3D_property_simplify_epsilon>`. Việc đơn giản hóa sử dụng một biến thể của thuật toán Ramer-Douglas-Peucker để giảm số lượng điểm của đường cong.

Đơn giản hóa path có thể giúp giảm thiểu nhiều vấn đề khi đi theo path có thể phát sinh với một số loại agent và hành vi script nhất định. Ví dụ: agent "steering" hoặc tránh va chạm trong "open fields".

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_target_desired_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **target_desired_distance** = ``1.0`` :ref:`🔗<class_NavigationAgent3D_property_target_desired_distance>`

.. rst-class:: classref-property-setget

- |void| **set_target_desired_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_target_desired_distance**\ (\ )

Ngưỡng khoảng cách trước khi mục tiêu được xem là đã đạt tới. Khi đạt tới mục tiêu, :ref:`target_reached<class_NavigationAgent3D_signal_target_reached>` được phát ra và quá trình điều hướng kết thúc (xem :ref:`is_navigation_finished()<class_NavigationAgent3D_method_is_navigation_finished>` và :ref:`navigation_finished<class_NavigationAgent3D_signal_navigation_finished>`).

Bạn có thể khiến quá trình điều hướng kết thúc sớm bằng cách đặt thuộc tính này thành một giá trị lớn hơn :ref:`path_desired_distance<class_NavigationAgent3D_property_path_desired_distance>` (quá trình điều hướng sẽ kết thúc trước khi đạt tới waypoint cuối cùng).

Bạn cũng có thể khiến quá trình điều hướng kết thúc ở vị trí gần mục tiêu hơn từng vị trí riêng lẻ trên đường đi bằng cách đặt thuộc tính này thành một giá trị nhỏ hơn :ref:`path_desired_distance<class_NavigationAgent3D_property_path_desired_distance>` (quá trình điều hướng sẽ không kết thúc ngay khi đạt tới waypoint cuối cùng). Tuy nhiên, nếu giá trị được đặt quá thấp, agent sẽ bị mắc kẹt trong vòng lặp repath vì nó sẽ liên tục vượt quá khoảng cách tới mục tiêu ở mỗi lần cập nhật physics frame.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_target_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **target_position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_NavigationAgent3D_property_target_position>`

.. rst-class:: classref-property-setget

- |void| **set_target_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_target_position**\ (\ )

Nếu được thiết lập, một đường đi điều hướng mới từ vị trí hiện tại của agent đến :ref:`target_position<class_NavigationAgent3D_property_target_position>` sẽ được yêu cầu từ NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_time_horizon_agents:

.. rst-class:: classref-property

:ref:`float<class_float>` **time_horizon_agents** = ``1.0`` :ref:`🔗<class_NavigationAgent3D_property_time_horizon_agents>`

.. rst-class:: classref-property-setget

- |void| **set_time_horizon_agents**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_time_horizon_agents**\ (\ )

Khoảng thời gian tối thiểu mà trong đó vận tốc của agent, được tính bằng thuật toán tránh va chạm, an toàn đối với các agent khác. Giá trị càng lớn, agent càng sớm phản ứng với các agent khác, nhưng càng ít tự do trong việc chọn vận tốc. Giá trị quá cao sẽ làm chuyển động của các agent chậm đi đáng kể. Phải là số dương.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_time_horizon_obstacles:

.. rst-class:: classref-property

:ref:`float<class_float>` **time_horizon_obstacles** = ``0.0`` :ref:`🔗<class_NavigationAgent3D_property_time_horizon_obstacles>`

.. rst-class:: classref-property-setget

- |void| **set_time_horizon_obstacles**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_time_horizon_obstacles**\ (\ )

Khoảng thời gian tối thiểu mà trong đó vận tốc của agent, được tính bằng thuật toán tránh va chạm, an toàn đối với các chướng ngại vật tránh tĩnh. Giá trị càng lớn, agent càng sớm phản ứng với các chướng ngại vật tránh tĩnh, nhưng càng ít tự do trong việc chọn vận tốc. Giá trị quá cao sẽ làm chuyển động của các agent chậm đi đáng kể. Phải là số dương.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_use_3d_avoidance:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_3d_avoidance** = ``false`` :ref:`🔗<class_NavigationAgent3D_property_use_3d_avoidance>`

.. rst-class:: classref-property-setget

- |void| **set_use_3d_avoidance**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_3d_avoidance**\ (\ )

Nếu ``true``, agent sẽ tính vận tốc tránh theo 3D đa hướng, ví dụ như trong các game diễn ra trên không, dưới nước hoặc ngoài không gian. Các agent sử dụng tránh 3D chỉ tránh các agent khác cũng sử dụng tránh 3D và phản ứng với các chướng ngại vật tránh dựa trên bán kính. Chúng bỏ qua mọi chướng ngại vật dựa trên đỉnh.

Nếu ``false``, agent sẽ tính vận tốc tránh theo 2D dọc theo các trục x và z, bỏ qua trục y. Các agent sử dụng tránh 2D chỉ tránh các agent khác cũng sử dụng tránh 2D và phản ứng với các chướng ngại vật tránh dựa trên bán kính hoặc dựa trên đỉnh. Các agent khác sử dụng tránh 2D nằm bên dưới hoặc bên trên vị trí hiện tại của chúng, bao gồm cả :ref:`height<class_NavigationAgent3D_property_height>`, sẽ bị bỏ qua.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_property_velocity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **velocity** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_NavigationAgent3D_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_velocity**\ (\ )

Đặt vận tốc mong muốn mới cho agent. Mô phỏng tránh va chạm sẽ cố gắng thực hiện vận tốc này nếu có thể, nhưng sẽ điều chỉnh nó để tránh va chạm với các agent và chướng ngại vật khác. Khi một agent được dịch chuyển tức thời đến vị trí mới, hãy sử dụng :ref:`set_velocity_forced()<class_NavigationAgent3D_method_set_velocity_forced>` để đặt lại vận tốc mô phỏng nội bộ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationAgent3D_method_distance_to_target:

.. rst-class:: classref-method

:ref:`float<class_float>` **distance_to_target**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_distance_to_target>`

Trả về khoảng cách đến vị trí mục tiêu, sử dụng vị trí global của agent. Người dùng phải thiết lập :ref:`target_position<class_NavigationAgent3D_property_target_position>` để kết quả này chính xác.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_avoidance_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_avoidance_layer_value>`

Trả về việc layer được chỉ định của bitmask :ref:`avoidance_layers<class_NavigationAgent3D_property_avoidance_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_avoidance_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_avoidance_mask_value**\ (\ mask_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_avoidance_mask_value>`

Trả về việc mask được chỉ định của bitmask :ref:`avoidance_mask<class_NavigationAgent3D_property_avoidance_mask>` có được bật hay không, với ``mask_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_current_navigation_path:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_current_navigation_path**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_current_navigation_path>`

Trả về đường đi hiện tại của agent này từ đầu đến cuối trong tọa độ global. Đường đi chỉ được cập nhật khi vị trí mục tiêu thay đổi hoặc agent yêu cầu repath. Mảng đường đi không được thiết kế để dùng cho việc di chuyển trực tiếp theo đường đi, vì agent có logic đường đi nội bộ riêng và logic này sẽ bị hỏng nếu bạn thay đổi mảng đường đi theo cách thủ công. Hãy sử dụng :ref:`get_next_path_position()<class_NavigationAgent3D_method_get_next_path_position>` theo từng physics frame để nhận điểm tiếp theo trên đường đi cho chuyển động của agent, vì hàm này cũng cập nhật logic đường đi nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_current_navigation_path_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_current_navigation_path_index**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_current_navigation_path_index>`

Trả về index mà agent hiện đang ở trong :ref:`PackedVector3Array<class_PackedVector3Array>` của đường đi điều hướng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_current_navigation_result:

.. rst-class:: classref-method

:ref:`NavigationPathQueryResult3D<class_NavigationPathQueryResult3D>` **get_current_navigation_result**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_current_navigation_result>`

Trả về kết quả truy vấn đường đi của đường đi mà agent hiện đang theo.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_final_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_final_position**\ (\ ) :ref:`🔗<class_NavigationAgent3D_method_get_final_position>`

Trả về vị trí cuối cùng có thể đến được của đường đi điều hướng hiện tại trong tọa độ global. Vị trí này có thể thay đổi nếu agent cần cập nhật đường đi điều hướng, khiến agent phát ra signal :ref:`path_changed<class_NavigationAgent3D_signal_path_changed>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_navigation_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_navigation_layer_value>`

Trả về việc layer được chỉ định của bitmask :ref:`navigation_layers<class_NavigationAgent3D_property_navigation_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_navigation_map>`

Trả về :ref:`RID<class_RID>` của navigation map cho node NavigationAgent này. Hàm này luôn trả về map được thiết lập trên node NavigationAgent, không phải map của agent trừu tượng trên NavigationServer. Nếu map của agent được thay đổi trực tiếp bằng NavigationServer API, node NavigationAgent sẽ không biết về thay đổi map đó. Hãy sử dụng :ref:`set_navigation_map()<class_NavigationAgent3D_method_set_navigation_map>` để thay đổi navigation map cho NavigationAgent và đồng thời cập nhật agent trên NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_next_path_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_next_path_position**\ (\ ) :ref:`🔗<class_NavigationAgent3D_method_get_next_path_position>`

Trả về vị trí tiếp theo trong tọa độ global có thể di chuyển tới, đồng thời đảm bảo không có đối tượng tĩnh nào cản đường. Nếu agent không có đường đi điều hướng, hàm sẽ trả về vị trí của parent của agent. Việc sử dụng hàm này theo từng physics frame là bắt buộc để cập nhật logic đường đi nội bộ của NavigationAgent.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_path_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_path_length**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_path_length>`

Trả về độ dài của đường đi hiện đang được tính. Giá trị trả về là ``0.0`` nếu đường đi vẫn đang được tính hoặc chưa có yêu cầu tính toán nào được gửi.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của agent này trên :ref:`NavigationServer3D<class_NavigationServer3D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_is_navigation_finished:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_navigation_finished**\ (\ ) :ref:`🔗<class_NavigationAgent3D_method_is_navigation_finished>`

Trả về ``true`` nếu quá trình điều hướng của agent đã hoàn tất. Nếu có thể đến được mục tiêu, quá trình điều hướng kết thúc khi đạt tới mục tiêu. Nếu không thể đến được mục tiêu, quá trình điều hướng kết thúc khi đạt tới waypoint cuối cùng của đường đi.

\ **Lưu ý:** Trong khi ``true``, nên ưu tiên dừng gọi các hàm cập nhật như :ref:`get_next_path_position()<class_NavigationAgent3D_method_get_next_path_position>`. Điều này tránh làm agent đang đứng bị rung do gọi các lần cập nhật đường đi lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_is_target_reachable:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_target_reachable**\ (\ ) :ref:`🔗<class_NavigationAgent3D_method_is_target_reachable>`

Trả về ``true`` nếu :ref:`get_final_position()<class_NavigationAgent3D_method_get_final_position>` nằm trong :ref:`target_desired_distance<class_NavigationAgent3D_property_target_desired_distance>` của :ref:`target_position<class_NavigationAgent3D_property_target_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_is_target_reached:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_target_reached**\ (\ ) |const| :ref:`🔗<class_NavigationAgent3D_method_is_target_reached>`

Trả về ``true`` nếu agent đã đạt tới mục tiêu, tức là agent đã di chuyển vào phạm vi :ref:`target_desired_distance<class_NavigationAgent3D_property_target_desired_distance>` của :ref:`target_position<class_NavigationAgent3D_property_target_position>`. Không phải lúc nào cũng có thể đạt tới mục tiêu, nhưng luôn phải có thể đạt tới vị trí cuối cùng. Xem :ref:`get_final_position()<class_NavigationAgent3D_method_get_final_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_set_avoidance_layer_value:

.. rst-class:: classref-method

|void| **set_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationAgent3D_method_set_avoidance_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`avoidance_layers<class_NavigationAgent3D_property_avoidance_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_set_avoidance_mask_value:

.. rst-class:: classref-method

|void| **set_avoidance_mask_value**\(\ mask_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationAgent3D_method_set_avoidance_mask_value>`

Dựa trên ``value``, bật hoặc tắt mask được chỉ định trong bitmask :ref:`avoidance_mask<class_NavigationAgent3D_property_avoidance_mask>`, với ``mask_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_set_navigation_layer_value:

.. rst-class:: classref-method

|void| **set_navigation_layer_value**\(\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationAgent3D_method_set_navigation_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationAgent3D_property_navigation_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\(\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationAgent3D_method_set_navigation_map>`

Thiết lập :ref:`RID<class_RID>` của navigation map mà node NavigationAgent này nên sử dụng, đồng thời cập nhật ``agent`` trên NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent3D_method_set_velocity_forced:

.. rst-class:: classref-method

|void| **set_velocity_forced**\(\ velocity\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_NavigationAgent3D_method_set_velocity_forced>`

Thay thế velocity nội bộ trong mô phỏng collision avoidance bằng ``velocity``. Khi agent được dịch chuyển tức thời đến một vị trí mới, nên sử dụng hàm này trong cùng frame. Nếu được gọi thường xuyên, hàm này có thể khiến các agent bị kẹt.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
