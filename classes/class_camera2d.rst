:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Camera2D.xml.

.. _class_Camera2D:

Camera2D
========

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node camera cho các scene 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node camera cho các scene 2D. Nó buộc màn hình (layer hiện tại) cuộn theo node này. Điều này giúp việc lập trình các scene có thể cuộn dễ dàng (và nhanh hơn) so với việc thay đổi thủ công vị trí của các node dựa trên :ref:`CanvasItem<class_CanvasItem>`.

Các camera tự đăng ký với node :ref:`Viewport<class_Viewport>` gần nhất (khi đi ngược lên cây). Mỗi viewport chỉ có thể có một camera hoạt động. Nếu không có viewport nào khi đi ngược lên cây, camera sẽ đăng ký với viewport toàn cục.

Node này được thiết kế như một helper đơn giản để nhanh chóng bắt đầu, nhưng có thể cần thêm chức năng để thay đổi cách camera hoạt động. Để tạo node camera tùy chỉnh của riêng bạn, hãy kế thừa nó từ :ref:`Node2D<class_Node2D>` và thay đổi transform của canvas bằng cách thiết lập :ref:`Viewport.canvas_transform<class_Viewport_property_canvas_transform>` trong :ref:`Viewport<class_Viewport>` (bạn có thể lấy :ref:`Viewport<class_Viewport>` hiện tại bằng cách sử dụng :ref:`Node.get_viewport()<class_Node_method_get_viewport>`).

Lưu ý rằng :ref:`Node2D.global_position<class_Node2D_property_global_position>` của node **Camera2D** không biểu diễn vị trí thực tế của màn hình, vị trí này có thể khác do smoothing hoặc các giới hạn được áp dụng. Bạn có thể sử dụng :ref:`get_screen_center_position()<class_Camera2D_method_get_screen_center_position>` để lấy vị trí thực. Tương tự, :ref:`Node2D.global_rotation<class_Node2D_property_global_rotation>` của node có thể khác do smoothing xoay được áp dụng. Bạn có thể sử dụng :ref:`get_screen_rotation()<class_Camera2D_method_get_screen_rotation>` để lấy góc xoay hiện tại của màn hình.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `2D Platformer Demo <https://godotengine.org/asset-library/asset/2727>`__

- `2D Isometric Demo <https://godotengine.org/asset-library/asset/2718>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`AnchorMode<enum_Camera2D_AnchorMode>`                           | :ref:`anchor_mode<class_Camera2D_property_anchor_mode>`                               | ``1``             |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`Node<class_Node>`                                               | :ref:`custom_viewport<class_Camera2D_property_custom_viewport>`                       |                   |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`drag_bottom_margin<class_Camera2D_property_drag_bottom_margin>`                 | ``0.2``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`drag_horizontal_enabled<class_Camera2D_property_drag_horizontal_enabled>`       | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`drag_horizontal_offset<class_Camera2D_property_drag_horizontal_offset>`         | ``0.0``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`drag_left_margin<class_Camera2D_property_drag_left_margin>`                     | ``0.2``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`drag_right_margin<class_Camera2D_property_drag_right_margin>`                   | ``0.2``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`drag_top_margin<class_Camera2D_property_drag_top_margin>`                       | ``0.2``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`drag_vertical_enabled<class_Camera2D_property_drag_vertical_enabled>`           | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`drag_vertical_offset<class_Camera2D_property_drag_vertical_offset>`             | ``0.0``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`editor_draw_drag_margin<class_Camera2D_property_editor_draw_drag_margin>`       | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`editor_draw_limits<class_Camera2D_property_editor_draw_limits>`                 | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`editor_draw_screen<class_Camera2D_property_editor_draw_screen>`                 | ``true``          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`enabled<class_Camera2D_property_enabled>`                                       | ``true``          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`ignore_rotation<class_Camera2D_property_ignore_rotation>`                       | ``true``          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                                 | :ref:`limit_bottom<class_Camera2D_property_limit_bottom>`                             | ``10000000``      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`limit_enabled<class_Camera2D_property_limit_enabled>`                           | ``true``          |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                                 | :ref:`limit_left<class_Camera2D_property_limit_left>`                                 | ``-10000000``     |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                                 | :ref:`limit_right<class_Camera2D_property_limit_right>`                               | ``10000000``      |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`limit_smoothed<class_Camera2D_property_limit_smoothed>`                         | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`int<class_int>`                                                 | :ref:`limit_top<class_Camera2D_property_limit_top>`                                   | ``-10000000``     |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                                         | :ref:`offset<class_Camera2D_property_offset>`                                         | ``Vector2(0, 0)`` |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`position_smoothing_enabled<class_Camera2D_property_position_smoothing_enabled>` | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`position_smoothing_speed<class_Camera2D_property_position_smoothing_speed>`     | ``5.0``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`Camera2DProcessCallback<enum_Camera2D_Camera2DProcessCallback>` | :ref:`process_callback<class_Camera2D_property_process_callback>`                     | ``1``             |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`rotation_smoothing_enabled<class_Camera2D_property_rotation_smoothing_enabled>` | ``false``         |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`                                             | :ref:`rotation_smoothing_speed<class_Camera2D_property_rotation_smoothing_speed>`     | ``5.0``           |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`                                         | :ref:`zoom<class_Camera2D_property_zoom>`                                             | ``Vector2(1, 1)`` |
   +-----------------------------------------------------------------------+---------------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`align<class_Camera2D_method_align>`\ (\ )                                                                                                            |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`force_update_scroll<class_Camera2D_method_force_update_scroll>`\ (\ )                                                                                |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_drag_margin<class_Camera2D_method_get_drag_margin>`\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                                  |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | :ref:`get_limit<class_Camera2D_method_get_limit>`\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|                                              |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_screen_center_position<class_Camera2D_method_get_screen_center_position>`\ (\ ) |const|                                                          |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`     | :ref:`get_screen_rotation<class_Camera2D_method_get_screen_rotation>`\ (\ ) |const|                                                                        |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`get_target_position<class_Camera2D_method_get_target_position>`\ (\ ) |const|                                                                        |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_current<class_Camera2D_method_is_current>`\ (\ ) |const|                                                                                          |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`make_current<class_Camera2D_method_make_current>`\ (\ )                                                                                              |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`reset_smoothing<class_Camera2D_method_reset_smoothing>`\ (\ )                                                                                        |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_drag_margin<class_Camera2D_method_set_drag_margin>`\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, drag_margin\: :ref:`float<class_float>`\ ) |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                        | :ref:`set_limit<class_Camera2D_method_set_limit>`\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, limit\: :ref:`int<class_int>`\ )                       |
   +-------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_Camera2D_AnchorMode:

.. rst-class:: classref-enumeration

enum **AnchorMode**: :ref:`🔗<enum_Camera2D_AnchorMode>`

.. _class_Camera2D_constant_ANCHOR_MODE_FIXED_TOP_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`AnchorMode<enum_Camera2D_AnchorMode>` **ANCHOR_MODE_FIXED_TOP_LEFT** = ``0``

Vị trí của camera được cố định sao cho góc trên bên trái luôn ở gốc tọa độ.

.. _class_Camera2D_constant_ANCHOR_MODE_DRAG_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`AnchorMode<enum_Camera2D_AnchorMode>` **ANCHOR_MODE_DRAG_CENTER** = ``1``

Vị trí của camera tính đến các offset dọc/ngang và kích thước màn hình.

.. rst-class:: classref-item-separator

----

.. _enum_Camera2D_Camera2DProcessCallback:

.. rst-class:: classref-enumeration

enum **Camera2DProcessCallback**: :ref:`🔗<enum_Camera2D_Camera2DProcessCallback>`

.. _class_Camera2D_constant_CAMERA2D_PROCESS_PHYSICS:

.. rst-class:: classref-enumeration-constant

:ref:`Camera2DProcessCallback<enum_Camera2D_Camera2DProcessCallback>` **CAMERA2D_PROCESS_PHYSICS** = ``0``

Camera được cập nhật trong các frame vật lý (xem :ref:`Node.NOTIFICATION_INTERNAL_PHYSICS_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PHYSICS_PROCESS>`).

.. _class_Camera2D_constant_CAMERA2D_PROCESS_IDLE:

.. rst-class:: classref-enumeration-constant

:ref:`Camera2DProcessCallback<enum_Camera2D_Camera2DProcessCallback>` **CAMERA2D_PROCESS_IDLE** = ``1``

Camera được cập nhật trong các frame xử lý (xem :ref:`Node.NOTIFICATION_INTERNAL_PROCESS<class_Node_constant_NOTIFICATION_INTERNAL_PROCESS>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Camera2D_property_anchor_mode:

.. rst-class:: classref-property

:ref:`AnchorMode<enum_Camera2D_AnchorMode>` **anchor_mode** = ``1`` :ref:`🔗<class_Camera2D_property_anchor_mode>`

.. rst-class:: classref-property-setget

- |void| **set_anchor_mode**\ (\ value\: :ref:`AnchorMode<enum_Camera2D_AnchorMode>`\ ) - :ref:`AnchorMode<enum_Camera2D_AnchorMode>` **get_anchor_mode**\ (\ )

Điểm neo của Camera2D.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_custom_viewport:

.. rst-class:: classref-property

:ref:`Node<class_Node>` **custom_viewport** :ref:`🔗<class_Camera2D_property_custom_viewport>`

.. rst-class:: classref-property-setget

- |void| **set_custom_viewport**\ (\ value\: :ref:`Node<class_Node>`\ ) - :ref:`Node<class_Node>` **get_custom_viewport**\ (\ )

Node :ref:`Viewport<class_Viewport>` tùy chỉnh được gắn vào **Camera2D**. Nếu ``null`` hoặc không phải là :ref:`Viewport<class_Viewport>`, thay vào đó sẽ sử dụng viewport mặc định.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_bottom_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **drag_bottom_margin** = ``0.2`` :ref:`🔗<class_Camera2D_property_drag_bottom_margin>`

.. rst-class:: classref-property-setget

- |void| **set_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, drag_margin\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Lề dưới cần thiết để kéo camera. Giá trị ``1`` khiến camera chỉ di chuyển khi chạm đến cạnh dưới của màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_horizontal_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **drag_horizontal_enabled** = ``false`` :ref:`🔗<class_Camera2D_property_drag_horizontal_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_drag_horizontal_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_drag_horizontal_enabled**\ (\ )

Nếu ``true``, camera chỉ di chuyển khi chạm đến các lề kéo ngang (trái và phải). Nếu ``false``, camera di chuyển theo chiều ngang bất kể các lề.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_horizontal_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **drag_horizontal_offset** = ``0.0`` :ref:`🔗<class_Camera2D_property_drag_horizontal_offset>`

.. rst-class:: classref-property-setget

- |void| **set_drag_horizontal_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drag_horizontal_offset**\ (\ )

Offset kéo ngang tương đối của camera giữa lề kéo bên phải (``-1``) và bên trái (``1``).

\ **Lưu ý:** Dùng để thiết lập offset kéo ngang ban đầu; xác định offset hiện tại; hoặc buộc đặt offset hiện tại. Giá trị này không tự động được cập nhật khi :ref:`drag_horizontal_enabled<class_Camera2D_property_drag_horizontal_enabled>` là ``true`` hoặc khi các lề kéo thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_left_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **drag_left_margin** = ``0.2`` :ref:`🔗<class_Camera2D_property_drag_left_margin>`

.. rst-class:: classref-property-setget

- |void| **set_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, drag_margin\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Lề trái cần thiết để kéo camera. Giá trị ``1`` khiến camera chỉ di chuyển khi chạm đến cạnh trái của màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_right_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **drag_right_margin** = ``0.2`` :ref:`🔗<class_Camera2D_property_drag_right_margin>`

.. rst-class:: classref-property-setget

- |void| **set_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, drag_margin\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Lề phải cần thiết để kéo camera. Giá trị ``1`` khiến camera chỉ di chuyển khi chạm đến cạnh phải của màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_top_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **drag_top_margin** = ``0.2`` :ref:`🔗<class_Camera2D_property_drag_top_margin>`

.. rst-class:: classref-property-setget

- |void| **set_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, drag_margin\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Lề trên cần thiết để kéo camera. Giá trị ``1`` khiến camera chỉ di chuyển khi chạm đến cạnh trên của màn hình.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_vertical_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **drag_vertical_enabled** = ``false`` :ref:`🔗<class_Camera2D_property_drag_vertical_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_drag_vertical_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_drag_vertical_enabled**\ (\ )

Nếu ``true``, camera chỉ di chuyển khi chạm đến các lề kéo dọc (trên và dưới). Nếu ``false``, camera di chuyển theo chiều dọc bất kể các lề kéo.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_drag_vertical_offset:

.. rst-class:: classref-property

:ref:`float<class_float>` **drag_vertical_offset** = ``0.0`` :ref:`🔗<class_Camera2D_property_drag_vertical_offset>`

.. rst-class:: classref-property-setget

- |void| **set_drag_vertical_offset**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_drag_vertical_offset**\ (\ )

Offset kéo dọc tương đối của camera giữa lề kéo bên dưới (``-1``) và bên trên (``1``).

\ **Lưu ý:** Dùng để thiết lập offset kéo dọc ban đầu; xác định offset hiện tại; hoặc buộc đặt offset hiện tại. Giá trị này không tự động được cập nhật khi :ref:`drag_vertical_enabled<class_Camera2D_property_drag_vertical_enabled>` là ``true`` hoặc khi các lề kéo thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_editor_draw_drag_margin:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editor_draw_drag_margin** = ``false`` :ref:`🔗<class_Camera2D_property_editor_draw_drag_margin>`

.. rst-class:: classref-property-setget

- |void| **set_margin_drawing_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_margin_drawing_enabled**\ (\ )

Nếu ``true``, vẽ hình chữ nhật lề kéo của camera trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_editor_draw_limits:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editor_draw_limits** = ``false`` :ref:`🔗<class_Camera2D_property_editor_draw_limits>`

.. rst-class:: classref-property-setget

- |void| **set_limit_drawing_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_limit_drawing_enabled**\ (\ )

Nếu ``true``, vẽ hình chữ nhật giới hạn của camera trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_editor_draw_screen:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **editor_draw_screen** = ``true`` :ref:`🔗<class_Camera2D_property_editor_draw_screen>`

.. rst-class:: classref-property-setget

- |void| **set_screen_drawing_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_screen_drawing_enabled**\ (\ )

Nếu ``true``, vẽ hình chữ nhật màn hình của camera trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** = ``true`` :ref:`🔗<class_Camera2D_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_enabled**\ (\ )

Kiểm soát việc camera có thể hoạt động hay không. Nếu ``true``, **Camera2D** sẽ trở thành camera chính khi đi vào scene tree và hiện không có camera nào hoạt động (xem :ref:`Viewport.get_camera_2d()<class_Viewport_method_get_camera_2d>`).

Khi camera hiện đang hoạt động và :ref:`enabled<class_Camera2D_property_enabled>` được đặt thành ``false``, **Camera2D** tiếp theo được bật trong scene tree sẽ trở thành camera hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_ignore_rotation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ignore_rotation** = ``true`` :ref:`🔗<class_Camera2D_property_ignore_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_ignore_rotation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_ignoring_rotation**\ (\ )

Nếu ``true``, chế độ xem được render của camera không bị ảnh hưởng bởi :ref:`Node2D.rotation<class_Node2D_property_rotation>` và :ref:`Node2D.global_rotation<class_Node2D_property_global_rotation>` của nó.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_limit_bottom:

.. rst-class:: classref-property

:ref:`int<class_int>` **limit_bottom** = ``10000000`` :ref:`🔗<class_Camera2D_property_limit_bottom>`

.. rst-class:: classref-property-setget

- |void| **set_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, limit\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Giới hạn cuộn dưới theo pixel. Camera sẽ dừng di chuyển khi đạt giá trị này, nhưng :ref:`offset<class_Camera2D_property_offset>` có thể đẩy chế độ xem vượt qua giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_limit_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **limit_enabled** = ``true`` :ref:`🔗<class_Camera2D_property_limit_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_limit_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_limit_enabled**\ (\ )

Nếu ``true``, các giới hạn sẽ được bật. Việc tắt tùy chọn này cho phép camera lấy nét ở bất kỳ đâu; khi đó bốn thuộc tính ``limit_*`` sẽ không hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_limit_left:

.. rst-class:: classref-property

:ref:`int<class_int>` **limit_left** = ``-10000000`` :ref:`🔗<class_Camera2D_property_limit_left>`

.. rst-class:: classref-property-setget

- |void| **set_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, limit\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Giới hạn cuộn trái theo pixel. Camera sẽ dừng di chuyển khi đạt giá trị này, nhưng :ref:`offset<class_Camera2D_property_offset>` có thể đẩy chế độ xem vượt qua giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_limit_right:

.. rst-class:: classref-property

:ref:`int<class_int>` **limit_right** = ``10000000`` :ref:`🔗<class_Camera2D_property_limit_right>`

.. rst-class:: classref-property-setget

- |void| **set_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, limit\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Giới hạn cuộn phải theo pixel. Camera sẽ dừng di chuyển khi đạt giá trị này, nhưng :ref:`offset<class_Camera2D_property_offset>` có thể đẩy chế độ xem vượt qua giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_limit_smoothed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **limit_smoothed** = ``false`` :ref:`🔗<class_Camera2D_property_limit_smoothed>`

.. rst-class:: classref-property-setget

- |void| **set_limit_smoothing_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_limit_smoothing_enabled**\ (\ )

Nếu ``true``, camera sẽ dừng mượt mà khi chạm đến các giới hạn.

Thuộc tính này không có tác dụng nếu :ref:`position_smoothing_enabled<class_Camera2D_property_position_smoothing_enabled>` là ``false``.

\ **Lưu ý:** Để cập nhật ngay lập tức vị trí của camera nằm trong các giới hạn mà không làm mượt, ngay cả khi cài đặt này được bật, hãy gọi :ref:`reset_smoothing()<class_Camera2D_method_reset_smoothing>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_limit_top:

.. rst-class:: classref-property

:ref:`int<class_int>` **limit_top** = ``-10000000`` :ref:`🔗<class_Camera2D_property_limit_top>`

.. rst-class:: classref-property-setget

- |void| **set_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, limit\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const|

Giới hạn cuộn phía trên tính bằng pixel. Camera sẽ dừng di chuyển khi đạt đến giá trị này, nhưng :ref:`offset<class_Camera2D_property_offset>` có thể đẩy khung nhìn vượt quá giới hạn.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Camera2D_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Độ lệch tương đối của camera. Hữu ích khi quan sát xung quanh hoặc tạo animation rung camera. Camera bị lệch có thể vượt qua các giới hạn được xác định trong :ref:`limit_top<class_Camera2D_property_limit_top>`, :ref:`limit_bottom<class_Camera2D_property_limit_bottom>`, :ref:`limit_left<class_Camera2D_property_limit_left>` và :ref:`limit_right<class_Camera2D_property_limit_right>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_position_smoothing_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **position_smoothing_enabled** = ``false`` :ref:`🔗<class_Camera2D_property_position_smoothing_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_position_smoothing_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_position_smoothing_enabled**\ (\ )

Nếu ``true``, khung nhìn của camera sẽ di chuyển mượt về phía vị trí đích tại :ref:`position_smoothing_speed<class_Camera2D_property_position_smoothing_speed>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_position_smoothing_speed:

.. rst-class:: classref-property

:ref:`float<class_float>` **position_smoothing_speed** = ``5.0`` :ref:`🔗<class_Camera2D_property_position_smoothing_speed>`

.. rst-class:: classref-property-setget

- |void| **set_position_smoothing_speed**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_position_smoothing_speed**\ (\ )

Tốc độ tính bằng pixel mỗi giây của hiệu ứng làm mượt camera khi :ref:`position_smoothing_enabled<class_Camera2D_property_position_smoothing_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_process_callback:

.. rst-class:: classref-property

:ref:`Camera2DProcessCallback<enum_Camera2D_Camera2DProcessCallback>` **process_callback** = ``1`` :ref:`🔗<class_Camera2D_property_process_callback>`

.. rst-class:: classref-property-setget

- |void| **set_process_callback**\ (\ value\: :ref:`Camera2DProcessCallback<enum_Camera2D_Camera2DProcessCallback>`\ ) - :ref:`Camera2DProcessCallback<enum_Camera2D_Camera2DProcessCallback>` **get_process_callback**\ (\ )

Process callback của camera.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_rotation_smoothing_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **rotation_smoothing_enabled** = ``false`` :ref:`🔗<class_Camera2D_property_rotation_smoothing_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_smoothing_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_rotation_smoothing_enabled**\ (\ )

Nếu ``true``, khung nhìn của camera sẽ xoay mượt, thông qua tính năng làm mượt tiệm cận, để căn chỉnh với góc xoay đích tại :ref:`rotation_smoothing_speed<class_Camera2D_property_rotation_smoothing_speed>`.

\ **Lưu ý:** Thuộc tính này không có tác dụng nếu :ref:`ignore_rotation<class_Camera2D_property_ignore_rotation>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_rotation_smoothing_speed:

.. rst-class:: classref-property

:ref:`float<class_float>` **rotation_smoothing_speed** = ``5.0`` :ref:`🔗<class_Camera2D_property_rotation_smoothing_speed>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_smoothing_speed**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rotation_smoothing_speed**\ (\ )

Tốc độ góc tiệm cận của hiệu ứng làm mượt góc xoay camera khi :ref:`rotation_smoothing_enabled<class_Camera2D_property_rotation_smoothing_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_property_zoom:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **zoom** = ``Vector2(1, 1)`` :ref:`🔗<class_Camera2D_property_zoom>`

.. rst-class:: classref-property-setget

- |void| **set_zoom**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_zoom**\ (\ )

Mức zoom của camera. Giá trị cao hơn sẽ phóng to hơn. Ví dụ, mức zoom ``Vector2(2.0, 2.0)`` sẽ phóng to gấp đôi trên mỗi trục (khung nhìn bao phủ một vùng nhỏ hơn bốn lần). Ngược lại, mức zoom ``Vector2(0.5, 0.5)`` sẽ thu nhỏ đi một nửa trên mỗi trục (khung nhìn bao phủ một vùng lớn hơn bốn lần). Nhìn chung, các thành phần X và Y luôn nên được đặt cùng một giá trị, trừ khi bạn muốn kéo giãn khung nhìn của camera.

\ **Lưu ý:** :ref:`FontFile.oversampling<class_FontFile_property_oversampling>` *không* tính đến mức zoom của **Camera2D**. Điều này có nghĩa là việc phóng to/thu nhỏ sẽ khiến bitmap font và dynamic font được rasterize (không phải MSDF) trông bị mờ hoặc vỡ hạt, trừ khi font là một phần của :ref:`CanvasLayer<class_CanvasLayer>` khiến nó bỏ qua mức zoom của camera. Để đảm bảo văn bản vẫn sắc nét bất kể mức zoom, bạn có thể bật tính năng render font MSDF bằng cách bật :ref:`ProjectSettings.gui/theme/default_font_multichannel_signed_distance_field<class_ProjectSettings_property_gui/theme/default_font_multichannel_signed_distance_field>` (chỉ áp dụng cho font mặc định của project), hoặc bật **Multichannel Signed Distance Field** trong các tùy chọn import của DynamicFont đối với font tùy chỉnh. Đối với system font, có thể bật :ref:`SystemFont.multichannel_signed_distance_field<class_SystemFont_property_multichannel_signed_distance_field>` trong inspector.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_Camera2D_method_align:

.. rst-class:: classref-method

|void| **align**\ (\ ) :ref:`🔗<class_Camera2D_method_align>`

Căn chỉnh camera theo node được theo dõi.

\ **Lưu ý:** Không cần gọi :ref:`force_update_scroll()<class_Camera2D_method_force_update_scroll>` sau phương thức này.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_force_update_scroll:

.. rst-class:: classref-method

|void| **force_update_scroll**\ (\ ) :ref:`🔗<class_Camera2D_method_force_update_scroll>`

Buộc camera cập nhật thao tác cuộn ngay lập tức.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_get_drag_margin:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_Camera2D_method_get_drag_margin>`

Trả về margin của :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Xem thêm :ref:`drag_bottom_margin<class_Camera2D_property_drag_bottom_margin>`, :ref:`drag_top_margin<class_Camera2D_property_drag_top_margin>`, :ref:`drag_left_margin<class_Camera2D_property_drag_left_margin>` và :ref:`drag_right_margin<class_Camera2D_property_drag_right_margin>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_get_limit:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`\ ) |const| :ref:`🔗<class_Camera2D_method_get_limit>`

Trả về giới hạn camera cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Xem thêm :ref:`limit_bottom<class_Camera2D_property_limit_bottom>`, :ref:`limit_top<class_Camera2D_property_limit_top>`, :ref:`limit_left<class_Camera2D_property_limit_left>` và :ref:`limit_right<class_Camera2D_property_limit_right>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_get_screen_center_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_screen_center_position**\ (\ ) |const| :ref:`🔗<class_Camera2D_method_get_screen_center_position>`

Trả về tâm màn hình theo góc nhìn của camera này, trong tọa độ global.

\ **Lưu ý:** Vị trí đích chính xác của camera có thể khác. Xem :ref:`get_target_position()<class_Camera2D_method_get_target_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_get_screen_rotation:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_screen_rotation**\ (\ ) |const| :ref:`🔗<class_Camera2D_method_get_screen_rotation>`

Trả về góc xoay màn hình hiện tại theo góc nhìn của camera này.

\ **Lưu ý:** Góc xoay màn hình có thể khác với :ref:`Node2D.global_rotation<class_Node2D_property_global_rotation>` nếu camera đang xoay mượt do :ref:`rotation_smoothing_enabled<class_Camera2D_property_rotation_smoothing_enabled>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_get_target_position:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_target_position**\ (\ ) |const| :ref:`🔗<class_Camera2D_method_get_target_position>`

Trả về vị trí đích của camera này, trong tọa độ global.

\ **Lưu ý:** Giá trị được trả về không giống :ref:`Node2D.global_position<class_Node2D_property_global_position>`, vì nó chịu ảnh hưởng của các thuộc tính kéo. Nó cũng không giống vị trí hiện tại nếu :ref:`position_smoothing_enabled<class_Camera2D_property_position_smoothing_enabled>` là ``true`` (xem :ref:`get_screen_center_position()<class_Camera2D_method_get_screen_center_position>`).

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_is_current:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_current**\ (\ ) |const| :ref:`🔗<class_Camera2D_method_is_current>`

Trả về ``true`` nếu **Camera2D** này là camera đang hoạt động (xem :ref:`Viewport.get_camera_2d()<class_Viewport_method_get_camera_2d>`).

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_make_current:

.. rst-class:: classref-method

|void| **make_current**\ (\ ) :ref:`🔗<class_Camera2D_method_make_current>`

Buộc **Camera2D** này trở thành camera đang hoạt động hiện tại. :ref:`enabled<class_Camera2D_property_enabled>` phải là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_reset_smoothing:

.. rst-class:: classref-method

|void| **reset_smoothing**\ (\ ) :ref:`🔗<class_Camera2D_method_reset_smoothing>`

Đặt ngay lập tức vị trí của camera về đích làm mượt hiện tại.

Phương thức này không có tác dụng nếu :ref:`position_smoothing_enabled<class_Camera2D_property_position_smoothing_enabled>` là ``false``.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_set_drag_margin:

.. rst-class:: classref-method

|void| **set_drag_margin**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, drag_margin\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Camera2D_method_set_drag_margin>`

Đặt margin của :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Xem thêm :ref:`drag_bottom_margin<class_Camera2D_property_drag_bottom_margin>`, :ref:`drag_top_margin<class_Camera2D_property_drag_top_margin>`, :ref:`drag_left_margin<class_Camera2D_property_drag_left_margin>` và :ref:`drag_right_margin<class_Camera2D_property_drag_right_margin>`.

.. rst-class:: classref-item-separator

----

.. _class_Camera2D_method_set_limit:

.. rst-class:: classref-method

|void| **set_limit**\ (\ margin\: :ref:`Side<enum_@GlobalScope_Side>`, limit\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Camera2D_method_set_limit>`

Đặt giới hạn camera cho :ref:`Side<enum_@GlobalScope_Side>` được chỉ định. Xem thêm :ref:`limit_bottom<class_Camera2D_property_limit_bottom>`, :ref:`limit_top<class_Camera2D_property_limit_top>`, :ref:`limit_left<class_Camera2D_property_limit_left>` và :ref:`limit_right<class_Camera2D_property_limit_right>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
