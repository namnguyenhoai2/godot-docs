:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/NavigationAgent2D.xml.

.. _class_NavigationAgent2D:

NavigationAgent2D
=================

**Thử nghiệm:** Class này có thể được thay đổi hoặc loại bỏ trong các phiên bản tương lai.

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một agent 2D dùng để tìm đường đến một vị trí đồng thời tránh các chướng ngại vật.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một agent 2D dùng để tìm đường đến một vị trí đồng thời tránh các chướng ngại vật tĩnh và động. Phép tính này có thể được node cha sử dụng để di chuyển nó linh hoạt dọc theo đường đi. Cần có dữ liệu navigation để hoạt động chính xác.

Các chướng ngại vật động được tránh bằng cơ chế tránh va chạm RVO. Việc tránh được tính toán trước physics, vì vậy thông tin tìm đường có thể được sử dụng an toàn trong bước physics.

\ **Lưu ý:** Sau khi thiết lập thuộc tính :ref:`target_position<class_NavigationAgent2D_property_target_position>`, phải sử dụng phương thức :ref:`get_next_path_position()<class_NavigationAgent2D_method_get_next_path_position>` một lần trong mỗi frame physics để cập nhật logic đường đi nội bộ của navigation agent. Vị trí vector mà phương thức này trả về nên được sử dụng làm vị trí di chuyển tiếp theo cho node cha của agent.

\ **Lưu ý:** Một số phương thức của class này, chẳng hạn như :ref:`get_next_path_position()<class_NavigationAgent2D_method_get_next_path_position>`, có thể kích hoạt phép tính đường đi mới. Việc gọi các phương thức này trong callback của bạn đối với signal của agent, chẳng hạn như :ref:`waypoint_reached<class_NavigationAgent2D_signal_waypoint_reached>`, có thể gây ra đệ quy vô hạn. Bạn nên gọi các phương thức này trong bước physics hoặc, nếu không, trì hoãn việc gọi chúng cho đến cuối frame (xem :ref:`Object.call_deferred()<class_Object_method_call_deferred>` hoặc :ref:`Object.CONNECT_DEFERRED<class_Object_constant_CONNECT_DEFERRED>`).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng NavigationAgents <../tutorials/navigation/navigation_using_navigationagents>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`avoidance_enabled<class_NavigationAgent2D_property_avoidance_enabled>`                       | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`avoidance_layers<class_NavigationAgent2D_property_avoidance_layers>`                         | ``1``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`avoidance_mask<class_NavigationAgent2D_property_avoidance_mask>`                             | ``1``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`avoidance_priority<class_NavigationAgent2D_property_avoidance_priority>`                     | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`debug_enabled<class_NavigationAgent2D_property_debug_enabled>`                               | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`                                                                      | :ref:`debug_path_custom_color<class_NavigationAgent2D_property_debug_path_custom_color>`           | ``Color(1, 1, 1, 1)`` |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`debug_path_custom_line_width<class_NavigationAgent2D_property_debug_path_custom_line_width>` | ``-1.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`debug_path_custom_point_size<class_NavigationAgent2D_property_debug_path_custom_point_size>` | ``4.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`debug_use_custom<class_NavigationAgent2D_property_debug_use_custom>`                         | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`max_neighbors<class_NavigationAgent2D_property_max_neighbors>`                               | ``10``                |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`max_speed<class_NavigationAgent2D_property_max_speed>`                                       | ``100.0``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`navigation_layers<class_NavigationAgent2D_property_navigation_layers>`                       | ``1``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`neighbor_distance<class_NavigationAgent2D_property_neighbor_distance>`                       | ``500.0``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_desired_distance<class_NavigationAgent2D_property_path_desired_distance>`               | ``20.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_max_distance<class_NavigationAgent2D_property_path_max_distance>`                       | ``100.0``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\] | :ref:`path_metadata_flags<class_NavigationAgent2D_property_path_metadata_flags>`                   | ``7``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>`             | :ref:`path_postprocessing<class_NavigationAgent2D_property_path_postprocessing>`                   | ``0``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_length<class_NavigationAgent2D_property_path_return_max_length>`             | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_return_max_radius<class_NavigationAgent2D_property_path_return_max_radius>`             | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`path_search_max_distance<class_NavigationAgent2D_property_path_search_max_distance>`         | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`int<class_int>`                                                                          | :ref:`path_search_max_polygons<class_NavigationAgent2D_property_path_search_max_polygons>`         | ``4096``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>`         | :ref:`pathfinding_algorithm<class_NavigationAgent2D_property_pathfinding_algorithm>`               | ``0``                 |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`radius<class_NavigationAgent2D_property_radius>`                                             | ``10.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`simplify_epsilon<class_NavigationAgent2D_property_simplify_epsilon>`                         | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`                                                                        | :ref:`simplify_path<class_NavigationAgent2D_property_simplify_path>`                               | ``false``             |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`target_desired_distance<class_NavigationAgent2D_property_target_desired_distance>`           | ``10.0``              |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector2<class_Vector2>`                                                                  | :ref:`target_position<class_NavigationAgent2D_property_target_position>`                           | ``Vector2(0, 0)``     |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`time_horizon_agents<class_NavigationAgent2D_property_time_horizon_agents>`                   | ``1.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`                                                                      | :ref:`time_horizon_obstacles<class_NavigationAgent2D_property_time_horizon_obstacles>`             | ``0.0``               |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector2<class_Vector2>`                                                                  | :ref:`velocity<class_NavigationAgent2D_property_velocity>`                                         | ``Vector2(0, 0)``     |
   +------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                             | :ref:`distance_to_target<class_NavigationAgent2D_method_distance_to_target>`\ (\ ) |const|                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`get_avoidance_layer_value<class_NavigationAgent2D_method_get_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`get_avoidance_mask_value<class_NavigationAgent2D_method_get_avoidance_mask_value>`\ (\ mask_number\: :ref:`int<class_int>`\ ) |const|                               |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`                   | :ref:`get_current_navigation_path<class_NavigationAgent2D_method_get_current_navigation_path>`\ (\ ) |const|                                                              |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                                 | :ref:`get_current_navigation_path_index<class_NavigationAgent2D_method_get_current_navigation_path_index>`\ (\ ) |const|                                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`NavigationPathQueryResult2D<class_NavigationPathQueryResult2D>` | :ref:`get_current_navigation_result<class_NavigationAgent2D_method_get_current_navigation_result>`\ (\ ) |const|                                                          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                         | :ref:`get_final_position<class_NavigationAgent2D_method_get_final_position>`\ (\ )                                                                                        |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`get_navigation_layer_value<class_NavigationAgent2D_method_get_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                                 | :ref:`get_navigation_map<class_NavigationAgent2D_method_get_navigation_map>`\ (\ ) |const|                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                         | :ref:`get_next_path_position<class_NavigationAgent2D_method_get_next_path_position>`\ (\ )                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                                             | :ref:`get_path_length<class_NavigationAgent2D_method_get_path_length>`\ (\ ) |const|                                                                                      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                                                 | :ref:`get_rid<class_NavigationAgent2D_method_get_rid>`\ (\ ) |const|                                                                                                      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`is_navigation_finished<class_NavigationAgent2D_method_is_navigation_finished>`\ (\ )                                                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`is_target_reachable<class_NavigationAgent2D_method_is_target_reachable>`\ (\ )                                                                                      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`is_target_reached<class_NavigationAgent2D_method_is_target_reached>`\ (\ ) |const|                                                                                  |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_avoidance_layer_value<class_NavigationAgent2D_method_set_avoidance_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )   |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_avoidance_mask_value<class_NavigationAgent2D_method_set_avoidance_mask_value>`\ (\ mask_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_navigation_layer_value<class_NavigationAgent2D_method_set_navigation_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_navigation_map<class_NavigationAgent2D_method_set_navigation_map>`\ (\ navigation_map\: :ref:`RID<class_RID>`\ )                                                |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                                | :ref:`set_velocity_forced<class_NavigationAgent2D_method_set_velocity_forced>`\ (\ velocity\: :ref:`Vector2<class_Vector2>`\ )                                            |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_NavigationAgent2D_signal_link_reached:

.. rst-class:: classref-signal

**link_reached**\ (\ details\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_NavigationAgent2D_signal_link_reached>`

Thông báo rằng agent đã đến một navigation link. Được phát khi agent di chuyển đến trong phạm vi :ref:`path_desired_distance<class_NavigationAgent2D_property_path_desired_distance>` so với vị trí tiếp theo trên đường đi, khi vị trí đó là một navigation link.

Dictionary details có thể chứa các key sau tùy thuộc vào giá trị của :ref:`path_metadata_flags<class_NavigationAgent2D_property_path_metadata_flags>`:

- ``position``: Vị trí bắt đầu của link đã đến.

- ``type``: Luôn là :ref:`NavigationPathQueryResult2D.PATH_SEGMENT_TYPE_LINK<class_NavigationPathQueryResult2D_constant_PATH_SEGMENT_TYPE_LINK>`.

- ``rid``: :ref:`RID<class_RID>` của link.

- ``owner``: Object quản lý link (thường là :ref:`NavigationLink2D<class_NavigationLink2D>`).

- ``link_entry_position``: Nếu ``owner`` khả dụng và owner là một :ref:`NavigationLink2D<class_NavigationLink2D>`, nó sẽ chứa vị trí global của điểm trên link mà agent đang đi vào.

- ``link_exit_position``: Nếu ``owner`` khả dụng và owner là một :ref:`NavigationLink2D<class_NavigationLink2D>`, nó sẽ chứa vị trí global của điểm trên link mà agent đang đi ra.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_signal_navigation_finished:

.. rst-class:: classref-signal

**navigation_finished**\ (\ ) :ref:`🔗<class_NavigationAgent2D_signal_navigation_finished>`

Thông báo rằng navigation của agent đã hoàn tất. Nếu target có thể tiếp cận, navigation kết thúc khi target được đến. Nếu target không thể tiếp cận, navigation kết thúc khi waypoint cuối cùng của đường đi được đến. Signal này chỉ được phát một lần cho mỗi đường đi đã tải.

Signal này sẽ được phát ngay sau :ref:`target_reached<class_NavigationAgent2D_signal_target_reached>` khi target có thể tiếp cận.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_signal_path_changed:

.. rst-class:: classref-signal

**path_changed**\ (\ ) :ref:`🔗<class_NavigationAgent2D_signal_path_changed>`

Được phát khi agent phải cập nhật đường đi đã tải:

- vì đường đi trước đó trống.

- vì navigation map đã thay đổi.

- vì agent bị đẩy ra xa segment hiện tại của đường đi hơn :ref:`path_max_distance<class_NavigationAgent2D_property_path_max_distance>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_signal_target_reached:

.. rst-class:: classref-signal

**target_reached**\ (\ ) :ref:`🔗<class_NavigationAgent2D_signal_target_reached>`

Thông báo rằng agent đã đến target, tức là agent đã di chuyển đến trong phạm vi :ref:`target_desired_distance<class_NavigationAgent2D_property_target_desired_distance>` so với :ref:`target_position<class_NavigationAgent2D_property_target_position>`. Signal này chỉ được phát một lần cho mỗi đường đi đã tải.

Signal này sẽ được phát ngay trước :ref:`navigation_finished<class_NavigationAgent2D_signal_navigation_finished>` khi target có thể tiếp cận.

Không phải lúc nào cũng có thể đến target, nhưng luôn phải có thể đến vị trí cuối cùng. Xem :ref:`get_final_position()<class_NavigationAgent2D_method_get_final_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_signal_velocity_computed:

.. rst-class:: classref-signal

**velocity_computed**\ (\ safe_velocity\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_NavigationAgent2D_signal_velocity_computed>`

Thông báo khi velocity tránh va chạm được tính toán. Được phát trong mỗi lần cập nhật miễn là :ref:`avoidance_enabled<class_NavigationAgent2D_property_avoidance_enabled>` là ``true`` và agent có navigation map.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_signal_waypoint_reached:

.. rst-class:: classref-signal

**waypoint_reached**\ (\ details\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_NavigationAgent2D_signal_waypoint_reached>`

Thông báo rằng agent đã đến một waypoint. Được phát khi agent di chuyển đến trong phạm vi :ref:`path_desired_distance<class_NavigationAgent2D_property_path_desired_distance>` so với vị trí tiếp theo trên đường đi.

Dictionary details có thể chứa các key sau tùy thuộc vào giá trị của :ref:`path_metadata_flags<class_NavigationAgent2D_property_path_metadata_flags>`:

- ``position``: Vị trí của waypoint đã đến.

- ``type``: Loại navigation primitive (region hoặc link) chứa waypoint này.

- ``rid``: :ref:`RID<class_RID>` của navigation primitive chứa waypoint (region hoặc link).

- ``owner``: Object quản lý navigation primitive chứa waypoint (region hoặc link).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NavigationAgent2D_property_avoidance_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **avoidance_enabled** = ``false`` :ref:`🔗<class_NavigationAgent2D_property_avoidance_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_avoidance_enabled**\ (\ )

Nếu ``true``, agent sẽ được đăng ký callback tránh RVO trên :ref:`NavigationServer2D<class_NavigationServer2D>`. Khi sử dụng :ref:`velocity<class_NavigationAgent2D_property_velocity>` và quá trình xử lý hoàn tất, một Vector2 ``safe_velocity`` sẽ được nhận với kết nối signal tới :ref:`velocity_computed<class_NavigationAgent2D_signal_velocity_computed>`. Việc xử lý tránh với nhiều agent đã đăng ký có chi phí hiệu năng đáng kể và chỉ nên được bật trên những agent hiện đang cần nó.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_avoidance_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **avoidance_layers** = ``1`` :ref:`🔗<class_NavigationAgent2D_property_avoidance_layers>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_avoidance_layers**\ (\ )

Một bitfield xác định các avoidance layer cho NavigationAgent này. Các agent khác có bit tương ứng trên :ref:`avoidance_mask<class_NavigationAgent2D_property_avoidance_mask>` sẽ tránh agent này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_avoidance_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **avoidance_mask** = ``1`` :ref:`🔗<class_NavigationAgent2D_property_avoidance_mask>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_avoidance_mask**\ (\ )

Một bitfield xác định những avoidance agent và chướng ngại vật khác mà NavigationAgent này sẽ tránh khi một bit khớp với ít nhất một trong các :ref:`avoidance_layers<class_NavigationAgent2D_property_avoidance_layers>` của chúng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_avoidance_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **avoidance_priority** = ``1.0`` :ref:`🔗<class_NavigationAgent2D_property_avoidance_priority>`

.. rst-class:: classref-property-setget

- |void| **set_avoidance_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_avoidance_priority**\ (\ )

Agent không điều chỉnh velocity cho các agent khác khớp với :ref:`avoidance_mask<class_NavigationAgent2D_property_avoidance_mask>` nhưng có :ref:`avoidance_priority<class_NavigationAgent2D_property_avoidance_priority>` thấp hơn. Do đó, các agent khác có priority thấp hơn sẽ điều chỉnh velocity của chúng nhiều hơn để tránh va chạm với agent này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_debug_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **debug_enabled** = ``false`` :ref:`🔗<class_NavigationAgent2D_property_debug_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_debug_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_debug_enabled**\ (\ )

Nếu ``true``, hiển thị hình ảnh debug cho agent này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_debug_path_custom_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **debug_path_custom_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_NavigationAgent2D_property_debug_path_custom_color>`

.. rst-class:: classref-property-setget

- |void| **set_debug_path_custom_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_debug_path_custom_color**\ (\ )

Nếu :ref:`debug_use_custom<class_NavigationAgent2D_property_debug_use_custom>` là ``true``, sử dụng màu này cho agent thay vì màu global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_debug_path_custom_line_width:

.. rst-class:: classref-property

:ref:`float<class_float>` **debug_path_custom_line_width** = ``-1.0`` :ref:`🔗<class_NavigationAgent2D_property_debug_path_custom_line_width>`

.. rst-class:: classref-property-setget

- |void| **set_debug_path_custom_line_width**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_debug_path_custom_line_width**\ (\ )

Nếu :ref:`debug_use_custom<class_NavigationAgent2D_property_debug_use_custom>` là ``true``, sử dụng độ rộng đường này để render các đường đi cho agent thay vì độ rộng global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_debug_path_custom_point_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **debug_path_custom_point_size** = ``4.0`` :ref:`🔗<class_NavigationAgent2D_property_debug_path_custom_point_size>`

.. rst-class:: classref-property-setget

- |void| **set_debug_path_custom_point_size**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_debug_path_custom_point_size**\ (\ )

Nếu :ref:`debug_use_custom<class_NavigationAgent2D_property_debug_use_custom>` là ``true``, sử dụng kích thước point đã rasterize này để render các point của đường đi cho agent thay vì kích thước point global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_debug_use_custom:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **debug_use_custom** = ``false`` :ref:`🔗<class_NavigationAgent2D_property_debug_use_custom>`

.. rst-class:: classref-property-setget

- |void| **set_debug_use_custom**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_debug_use_custom**\ (\ )

Nếu ``true``, sử dụng :ref:`debug_path_custom_color<class_NavigationAgent2D_property_debug_path_custom_color>` đã xác định cho agent này thay vì màu global.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_max_neighbors:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_neighbors** = ``10`` :ref:`🔗<class_NavigationAgent2D_property_max_neighbors>`

.. rst-class:: classref-property-setget

- |void| **set_max_neighbors**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_neighbors**\ (\ )

Số lượng neighbor tối đa mà agent sẽ xem xét.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_max_speed:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_speed** = ``100.0`` :ref:`🔗<class_NavigationAgent2D_property_max_speed>`

.. rst-class:: classref-property-setget

- |void| **set_max_speed**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_speed**\ (\ )

Tốc độ tối đa mà agent có thể di chuyển.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_navigation_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **navigation_layers** = ``1`` :ref:`🔗<class_NavigationAgent2D_property_navigation_layers>`

.. rst-class:: classref-property-setget

- |void| **set_navigation_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_navigation_layers**\ (\ )

Một bitfield xác định các lớp điều hướng của các vùng điều hướng mà agent này sẽ sử dụng để tính toán đường đi. Việc thay đổi thuộc tính này trong runtime sẽ xóa đường điều hướng hiện tại và tạo một đường mới theo các lớp điều hướng mới.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_neighbor_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **neighbor_distance** = ``500.0`` :ref:`🔗<class_NavigationAgent2D_property_neighbor_distance>`

.. rst-class:: classref-property-setget

- |void| **set_neighbor_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_neighbor_distance**\ (\ )

Khoảng cách dùng để tìm kiếm các agent khác.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_desired_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_desired_distance** = ``20.0`` :ref:`🔗<class_NavigationAgent2D_property_path_desired_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_desired_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_desired_distance**\ (\ )

Ngưỡng khoảng cách trước khi một điểm trên đường đi được xem là đã đến. Điều này cho phép agent không cần phải chạm chính xác vào một điểm trên đường đi mà chỉ cần đến khu vực nói chung của điểm đó. Nếu giá trị này quá cao, NavigationAgent sẽ bỏ qua các điểm trên đường đi, điều này có thể khiến nó rời khỏi navigation mesh. Nếu giá trị này quá thấp, NavigationAgent sẽ bị mắc kẹt trong vòng lặp repath vì liên tục vượt quá khoảng cách đến điểm tiếp theo trong mỗi lần cập nhật physics frame.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_max_distance** = ``100.0`` :ref:`🔗<class_NavigationAgent2D_property_path_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_max_distance**\ (\ )

Khoảng cách tối đa mà agent được phép lệch khỏi đường đi lý tưởng đến vị trí cuối. Điều này có thể xảy ra do việc cố gắng tránh va chạm. Khi vượt quá khoảng cách tối đa, đường đi lý tưởng sẽ được tính toán lại.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_metadata_flags:

.. rst-class:: classref-property

|bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\] **path_metadata_flags** = ``7`` :ref:`🔗<class_NavigationAgent2D_property_path_metadata_flags>`

.. rst-class:: classref-property-setget

- |void| **set_path_metadata_flags**\ (\ value\: |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\]\ ) - |bitfield|\[:ref:`PathMetadataFlags<enum_NavigationPathQueryParameters2D_PathMetadataFlags>`\] **get_path_metadata_flags**\ (\ )

Thông tin bổ sung cần trả về cùng với đường điều hướng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_postprocessing:

.. rst-class:: classref-property

:ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **path_postprocessing** = ``0`` :ref:`🔗<class_NavigationAgent2D_property_path_postprocessing>`

.. rst-class:: classref-property-setget

- |void| **set_path_postprocessing**\ (\ value\: :ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>`\ ) - :ref:`PathPostProcessing<enum_NavigationPathQueryParameters2D_PathPostProcessing>` **get_path_postprocessing**\ (\ )

Quá trình hậu xử lý đường đi được áp dụng cho corridor đường đi thô do :ref:`pathfinding_algorithm<class_NavigationAgent2D_property_pathfinding_algorithm>` tìm thấy.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_return_max_length:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_length** = ``0.0`` :ref:`🔗<class_NavigationAgent2D_property_path_return_max_length>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_length**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_length**\ (\ )

Độ dài tối đa được phép của đường đi trả về, tính theo đơn vị thế giới. Đường đi sẽ bị cắt khi vượt quá độ dài này.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_return_max_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_return_max_radius** = ``0.0`` :ref:`🔗<class_NavigationAgent2D_property_path_return_max_radius>`

.. rst-class:: classref-property-setget

- |void| **set_path_return_max_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_return_max_radius**\ (\ )

Bán kính tối đa được phép, tính theo đơn vị thế giới, mà đường đi trả về có thể cách điểm bắt đầu của đường đi. Đường đi sẽ bị cắt khi vượt quá bán kính này. So với :ref:`path_return_max_length<class_NavigationAgent2D_property_path_return_max_length>`, thuộc tính này cho phép agent đi xa hơn chừng đó nếu cần đi vòng qua một góc.

\ **Lưu ý:** Thao tác này sẽ thực hiện việc cắt theo hình cầu, chỉ xét các điểm thực tế trên đường đi của navigation mesh, trong đó vị trí đầu tiên của đường đi là tâm hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_search_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **path_search_max_distance** = ``0.0`` :ref:`🔗<class_NavigationAgent2D_property_path_search_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_path_search_max_distance**\ (\ )

Khoảng cách tối đa mà một polygon được tìm kiếm có thể cách polygon bắt đầu trước khi pathfinding hủy việc tìm đường đến polygon vị trí đích (có thể không thể đi tới hoặc ở rất xa). Trong trường hợp này, pathfinding sẽ đặt lại và xây dựng đường đi từ polygon bắt đầu đến polygon được tìm thấy là gần vị trí đích nhất cho đến thời điểm đó. Giá trị ``0`` hoặc nhỏ hơn được xem là không giới hạn. Khi không giới hạn, pathfinding sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí đích hoặc đã dùng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_path_search_max_polygons:

.. rst-class:: classref-property

:ref:`int<class_int>` **path_search_max_polygons** = ``4096`` :ref:`🔗<class_NavigationAgent2D_property_path_search_max_polygons>`

.. rst-class:: classref-property-setget

- |void| **set_path_search_max_polygons**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_path_search_max_polygons**\ (\ )

Số lượng polygon tối đa được tìm kiếm trước khi pathfinding hủy việc tìm đường đến polygon vị trí đích (có thể không thể đi tới hoặc ở rất xa). Trong trường hợp này, pathfinding sẽ đặt lại và xây dựng đường đi từ polygon bắt đầu đến polygon được tìm thấy là gần vị trí đích nhất cho đến thời điểm đó. Giá trị ``0`` hoặc nhỏ hơn được xem là không giới hạn. Khi không giới hạn, pathfinding sẽ tìm kiếm tất cả polygon được kết nối với polygon bắt đầu cho đến khi tìm thấy polygon vị trí đích hoặc đã dùng hết mọi tùy chọn tìm kiếm polygon hiện có.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_pathfinding_algorithm:

.. rst-class:: classref-property

:ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>` **pathfinding_algorithm** = ``0`` :ref:`🔗<class_NavigationAgent2D_property_pathfinding_algorithm>`

.. rst-class:: classref-property-setget

- |void| **set_pathfinding_algorithm**\ (\ value\: :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>`\ ) - :ref:`PathfindingAlgorithm<enum_NavigationPathQueryParameters2D_PathfindingAlgorithm>` **get_pathfinding_algorithm**\ (\ )

Thuật toán pathfinding được sử dụng trong truy vấn đường đi.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``10.0`` :ref:`🔗<class_NavigationAgent2D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của avoidance agent. Đây là "thân" của avoidance agent, không phải bán kính bắt đầu của thao tác tránh (được điều khiển bởi :ref:`neighbor_distance<class_NavigationAgent2D_property_neighbor_distance>`).

Không ảnh hưởng đến pathfinding thông thường. Để thay đổi bán kính pathfinding của actor, hãy bake các resource :ref:`NavigationPolygon<class_NavigationPolygon>` với thuộc tính :ref:`NavigationPolygon.agent_radius<class_NavigationPolygon_property_agent_radius>` khác và sử dụng các navigation map khác nhau cho từng kích thước actor.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_simplify_epsilon:

.. rst-class:: classref-property

:ref:`float<class_float>` **simplify_epsilon** = ``0.0`` :ref:`🔗<class_NavigationAgent2D_property_simplify_epsilon>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_epsilon**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_simplify_epsilon**\ (\ )

Mức độ đơn giản hóa đường đi, tính theo đơn vị thế giới.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_simplify_path:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **simplify_path** = ``false`` :ref:`🔗<class_NavigationAgent2D_property_simplify_path>`

.. rst-class:: classref-property-setget

- |void| **set_simplify_path**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_simplify_path**\ (\ )

Nếu ``true``, một phiên bản đơn giản hóa của đường đi sẽ được trả về, trong đó các điểm đường đi ít quan trọng hơn đã bị loại bỏ. Mức độ đơn giản hóa được điều khiển bởi :ref:`simplify_epsilon<class_NavigationAgent2D_property_simplify_epsilon>`. Việc đơn giản hóa sử dụng một biến thể của thuật toán Ramer-Douglas-Peucker để giảm số điểm của đường cong.

Đơn giản hóa đường đi có thể giúp giảm thiểu nhiều vấn đề khi bám theo đường đi, vốn có thể phát sinh với một số loại agent và hành vi của script. Ví dụ: agent "steering" hoặc cơ chế tránh trong "open fields".

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_target_desired_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **target_desired_distance** = ``10.0`` :ref:`🔗<class_NavigationAgent2D_property_target_desired_distance>`

.. rst-class:: classref-property-setget

- |void| **set_target_desired_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_target_desired_distance**\ (\ )

Ngưỡng khoảng cách trước khi mục tiêu được xem là đã đến. Khi đến mục tiêu, :ref:`target_reached<class_NavigationAgent2D_signal_target_reached>` được phát ra và navigation kết thúc (xem :ref:`is_navigation_finished()<class_NavigationAgent2D_method_is_navigation_finished>` và :ref:`navigation_finished<class_NavigationAgent2D_signal_navigation_finished>`).

Bạn có thể khiến navigation kết thúc sớm bằng cách đặt thuộc tính này thành giá trị lớn hơn :ref:`path_desired_distance<class_NavigationAgent2D_property_path_desired_distance>` (navigation sẽ kết thúc trước khi đến waypoint cuối cùng).

Bạn cũng có thể khiến navigation kết thúc ở vị trí gần mục tiêu hơn từng vị trí riêng lẻ trên đường đi bằng cách đặt thuộc tính này thành giá trị nhỏ hơn :ref:`path_desired_distance<class_NavigationAgent2D_property_path_desired_distance>` (navigation sẽ không kết thúc ngay khi đến waypoint cuối cùng). Tuy nhiên, nếu giá trị được đặt quá thấp, agent sẽ bị mắc kẹt trong vòng lặp repath vì liên tục vượt quá khoảng cách đến mục tiêu trong mỗi lần cập nhật physics frame.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_target_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **target_position** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationAgent2D_property_target_position>`

.. rst-class:: classref-property-setget

- |void| **set_target_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_target_position**\ (\ )

Nếu được thiết lập, một đường navigation mới từ vị trí hiện tại của agent đến :ref:`target_position<class_NavigationAgent2D_property_target_position>` sẽ được yêu cầu từ NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_time_horizon_agents:

.. rst-class:: classref-property

:ref:`float<class_float>` **time_horizon_agents** = ``1.0`` :ref:`🔗<class_NavigationAgent2D_property_time_horizon_agents>`

.. rst-class:: classref-property-setget

- |void| **set_time_horizon_agents**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_time_horizon_agents**\ (\ )

Khoảng thời gian tối thiểu mà trong đó vận tốc của agent này, được tính bằng thuật toán tránh va chạm, an toàn đối với các agent khác. Giá trị càng lớn, agent sẽ phản hồi các agent khác càng sớm, nhưng càng ít tự do trong việc chọn vận tốc. Giá trị quá cao sẽ làm chuyển động của các agent chậm đi đáng kể. Phải là số dương.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_time_horizon_obstacles:

.. rst-class:: classref-property

:ref:`float<class_float>` **time_horizon_obstacles** = ``0.0`` :ref:`🔗<class_NavigationAgent2D_property_time_horizon_obstacles>`

.. rst-class:: classref-property-setget

- |void| **set_time_horizon_obstacles**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_time_horizon_obstacles**\ (\ )

Khoảng thời gian tối thiểu mà trong đó vận tốc của agent này, được tính bằng thuật toán tránh va chạm, an toàn đối với các chướng ngại vật tránh tĩnh. Giá trị càng lớn, agent sẽ phản hồi các chướng ngại vật tránh tĩnh càng sớm, nhưng càng ít tự do trong việc chọn vận tốc. Giá trị quá cao sẽ làm chuyển động của các agent chậm đi đáng kể. Phải là số dương.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_property_velocity:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **velocity** = ``Vector2(0, 0)`` :ref:`🔗<class_NavigationAgent2D_property_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_velocity**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_velocity**\ (\ )

Đặt vận tốc mong muốn mới cho agent. Mô phỏng tránh va chạm sẽ cố gắng đáp ứng vận tốc này nếu có thể, nhưng sẽ điều chỉnh nó để tránh va chạm với các agent và chướng ngại vật khác. Khi một agent được dịch chuyển tức thời đến vị trí mới, hãy sử dụng :ref:`set_velocity_forced()<class_NavigationAgent2D_method_set_velocity_forced>` để đặt lại vận tốc mô phỏng nội bộ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_NavigationAgent2D_method_distance_to_target:

.. rst-class:: classref-method

:ref:`float<class_float>` **distance_to_target**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_distance_to_target>`

Trả về khoảng cách đến vị trí đích, sử dụng vị trí toàn cục của agent. Người dùng phải đặt :ref:`target_position<class_NavigationAgent2D_property_target_position>` để giá trị này chính xác.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_avoidance_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_avoidance_layer_value>`

Trả về liệu layer được chỉ định của bitmask :ref:`avoidance_layers<class_NavigationAgent2D_property_avoidance_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_avoidance_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_avoidance_mask_value**\ (\ mask_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_avoidance_mask_value>`

Trả về liệu mask được chỉ định của bitmask :ref:`avoidance_mask<class_NavigationAgent2D_property_avoidance_mask>` có được bật hay không, với ``mask_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_current_navigation_path:

.. rst-class:: classref-method

:ref:`PackedVector2Array<class_PackedVector2Array>` **get_current_navigation_path**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_current_navigation_path>`

Trả về path hiện tại của agent này từ đầu đến cuối trong tọa độ toàn cục. Path chỉ được cập nhật khi vị trí đích thay đổi hoặc agent yêu cầu tính lại path. Mảng path không предназнач định để dùng cho việc di chuyển trực tiếp theo path, vì agent có logic path nội bộ riêng và logic này sẽ bị hỏng nếu mảng path bị thay đổi thủ công. Hãy sử dụng :ref:`get_next_path_position()<class_NavigationAgent2D_method_get_next_path_position>` một lần trong mỗi physics frame để nhận điểm path tiếp theo cho chuyển động của agent, vì hàm này cũng cập nhật logic path nội bộ.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_current_navigation_path_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_current_navigation_path_index**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_current_navigation_path_index>`

Trả về index mà agent hiện đang ở trong :ref:`PackedVector2Array<class_PackedVector2Array>` của path điều hướng.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_current_navigation_result:

.. rst-class:: classref-method

:ref:`NavigationPathQueryResult2D<class_NavigationPathQueryResult2D>` **get_current_navigation_result**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_current_navigation_result>`

Trả về kết quả truy vấn path của path mà agent hiện đang đi theo.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_final_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_final_position**\ (\ ) :ref:`🔗<class_NavigationAgent2D_method_get_final_position>`

Trả về vị trí cuối cùng có thể đến được của path điều hướng hiện tại trong tọa độ toàn cục. Vị trí này có thể thay đổi nếu agent cần cập nhật path điều hướng, khiến agent phát signal :ref:`path_changed<class_NavigationAgent2D_signal_path_changed>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_navigation_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_navigation_layer_value>`

Trả về liệu layer được chỉ định của bitmask :ref:`navigation_layers<class_NavigationAgent2D_property_navigation_layers>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_navigation_map:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_navigation_map**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_navigation_map>`

Trả về :ref:`RID<class_RID>` của navigation map dành cho node NavigationAgent này. Hàm này luôn trả về map được đặt trên node NavigationAgent, không phải map của agent trừu tượng trên NavigationServer. Nếu map của agent được thay đổi trực tiếp bằng API NavigationServer, node NavigationAgent sẽ không biết về thay đổi map đó. Hãy sử dụng :ref:`set_navigation_map()<class_NavigationAgent2D_method_set_navigation_map>` để thay đổi navigation map cho NavigationAgent và đồng thời cập nhật agent trên NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_next_path_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_next_path_position**\ (\ ) :ref:`🔗<class_NavigationAgent2D_method_get_next_path_position>`

Trả về vị trí tiếp theo trong tọa độ toàn cục mà agent có thể di chuyển đến, đồng thời đảm bảo không có đối tượng tĩnh nào cản đường. Nếu agent không có path điều hướng, hàm sẽ trả về vị trí của parent của agent. Cần sử dụng hàm này một lần trong mỗi physics frame để cập nhật logic path nội bộ của NavigationAgent.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_path_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_path_length**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_path_length>`

Trả về độ dài của path hiện đang được tính toán. Giá trị trả về là ``0.0`` nếu path vẫn đang được tính toán hoặc chưa có yêu cầu tính toán nào.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của agent này trên :ref:`NavigationServer2D<class_NavigationServer2D>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_is_navigation_finished:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_navigation_finished**\ (\ ) :ref:`🔗<class_NavigationAgent2D_method_is_navigation_finished>`

Trả về ``true`` nếu navigation của agent đã hoàn tất. Nếu đích có thể đến được, navigation kết thúc khi đến đích. Nếu đích không thể đến được, navigation kết thúc khi đến waypoint cuối cùng của path.

\ **Lưu ý:** Khi ``true``, nên ưu tiên dừng gọi các hàm cập nhật như :ref:`get_next_path_position()<class_NavigationAgent2D_method_get_next_path_position>`. Điều này tránh làm agent đang đứng bị rung do gọi các bản cập nhật path lặp đi lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_is_target_reachable:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_target_reachable**\ (\ ) :ref:`🔗<class_NavigationAgent2D_method_is_target_reachable>`

Trả về ``true`` nếu :ref:`get_final_position()<class_NavigationAgent2D_method_get_final_position>` nằm trong :ref:`target_desired_distance<class_NavigationAgent2D_property_target_desired_distance>` của :ref:`target_position<class_NavigationAgent2D_property_target_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_is_target_reached:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_target_reached**\ (\ ) |const| :ref:`🔗<class_NavigationAgent2D_method_is_target_reached>`

Trả về ``true`` nếu agent đã đến đích, tức là agent đã di chuyển vào trong phạm vi :ref:`target_desired_distance<class_NavigationAgent2D_property_target_desired_distance>` của :ref:`target_position<class_NavigationAgent2D_property_target_position>`. Có thể không phải lúc nào cũng đến được đích, nhưng luôn phải đến được vị trí cuối cùng. Xem :ref:`get_final_position()<class_NavigationAgent2D_method_get_final_position>`.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_set_avoidance_layer_value:

.. rst-class:: classref-method

|void| **set_avoidance_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationAgent2D_method_set_avoidance_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`avoidance_layers<class_NavigationAgent2D_property_avoidance_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_set_avoidance_mask_value:

.. rst-class:: classref-method

|void| **set_avoidance_mask_value**\ (\ mask_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationAgent2D_method_set_avoidance_mask_value>`

Dựa trên ``value``, bật hoặc tắt mask được chỉ định trong bitmask :ref:`avoidance_mask<class_NavigationAgent2D_property_avoidance_mask>`, với ``mask_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_set_navigation_layer_value:

.. rst-class:: classref-method

|void| **set_navigation_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_NavigationAgent2D_method_set_navigation_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong bitmask :ref:`navigation_layers<class_NavigationAgent2D_property_navigation_layers>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_set_navigation_map:

.. rst-class:: classref-method

|void| **set_navigation_map**\ (\ navigation_map\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_NavigationAgent2D_method_set_navigation_map>`

Đặt :ref:`RID<class_RID>` của navigation map mà node NavigationAgent này nên sử dụng, đồng thời cập nhật ``agent`` trên NavigationServer.

.. rst-class:: classref-item-separator

----

.. _class_NavigationAgent2D_method_set_velocity_forced:

.. rst-class:: classref-method

|void| **set_velocity_forced**\ (\ velocity\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_NavigationAgent2D_method_set_velocity_forced>`

Thay thế vận tốc nội bộ trong mô phỏng tránh va chạm bằng ``velocity``. Khi agent được dịch chuyển tức thời đến vị trí mới, nên sử dụng hàm này trong cùng frame. Nếu được gọi thường xuyên, hàm này có thể khiến các agent bị mắc kẹt.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
