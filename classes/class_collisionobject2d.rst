:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CollisionObject2D.xml.

.. _class_CollisionObject2D:

CollisionObject2D
=================

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`Area2D<class_Area2D>`, :ref:`PhysicsBody2D<class_PhysicsBody2D>`

Lớp cơ sở trừu tượng cho các đối tượng vật lý 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở trừu tượng cho các đối tượng vật lý 2D. **CollisionObject2D** có thể chứa bất kỳ số lượng :ref:`Shape2D<class_Shape2D>`\ s nào để xử lý va chạm. Mỗi shape phải được gán cho một *shape owner*. Shape owner không phải là node và không xuất hiện trong editor, nhưng có thể được truy cập thông qua code bằng các phương thức ``shape_owner_*``.

\ **Lưu ý:** Chỉ hỗ trợ các va chạm giữa những đối tượng nằm trong cùng một canvas (:ref:`Viewport<class_Viewport>` canvas hoặc :ref:`CanvasLayer<class_CanvasLayer>`). Hành vi của các va chạm giữa những đối tượng trong các canvas khác nhau là không xác định.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`                                  | :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>`       | ``1``    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`                                  | :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>`         | ``1``    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`                              | :ref:`collision_priority<class_CollisionObject2D_property_collision_priority>` | ``1.0``  |
   +--------------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`DisableMode<enum_CollisionObject2D_DisableMode>` | :ref:`disable_mode<class_CollisionObject2D_property_disable_mode>`             | ``0``    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`                                | :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>`         | ``true`` |
   +--------------------------------------------------------+--------------------------------------------------------------------------------+----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_input_event<class_CollisionObject2D_private_method__input_event>`\ (\ viewport\: :ref:`Viewport<class_Viewport>`, event\: :ref:`InputEvent<class_InputEvent>`, shape_idx\: :ref:`int<class_int>`\ ) |virtual| |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_mouse_enter<class_CollisionObject2D_private_method__mouse_enter>`\ (\ ) |virtual|                                                                                                                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_mouse_exit<class_CollisionObject2D_private_method__mouse_exit>`\ (\ ) |virtual|                                                                                                                               |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_mouse_shape_enter<class_CollisionObject2D_private_method__mouse_shape_enter>`\ (\ shape_idx\: :ref:`int<class_int>`\ ) |virtual|                                                                              |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_mouse_shape_exit<class_CollisionObject2D_private_method__mouse_shape_exit>`\ (\ shape_idx\: :ref:`int<class_int>`\ ) |virtual|                                                                                |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`create_shape_owner<class_CollisionObject2D_method_create_shape_owner>`\ (\ owner\: :ref:`Object<class_Object>`\ )                                                                                              |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`get_collision_layer_value<class_CollisionObject2D_method_get_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                                       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`get_collision_mask_value<class_CollisionObject2D_method_get_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                                         |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                           | :ref:`get_rid<class_CollisionObject2D_method_get_rid>`\ (\ ) |const|                                                                                                                                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                   | :ref:`get_shape_owner_one_way_collision_direction<class_CollisionObject2D_method_get_shape_owner_one_way_collision_direction>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`get_shape_owner_one_way_collision_margin<class_CollisionObject2D_method_get_shape_owner_one_way_collision_margin>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`get_shape_owners<class_CollisionObject2D_method_get_shape_owners>`\ (\ )                                                                                                                                       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_shape_owner_disabled<class_CollisionObject2D_method_is_shape_owner_disabled>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                               |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_shape_owner_one_way_collision_enabled<class_CollisionObject2D_method_is_shape_owner_one_way_collision_enabled>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                             |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`remove_shape_owner<class_CollisionObject2D_method_remove_shape_owner>`\ (\ owner_id\: :ref:`int<class_int>`\ )                                                                                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_collision_layer_value<class_CollisionObject2D_method_set_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                                              |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_collision_mask_value<class_CollisionObject2D_method_set_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                                                |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`shape_find_owner<class_CollisionObject2D_method_shape_find_owner>`\ (\ shape_index\: :ref:`int<class_int>`\ ) |const|                                                                                          |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_add_shape<class_CollisionObject2D_method_shape_owner_add_shape>`\ (\ owner_id\: :ref:`int<class_int>`, shape\: :ref:`Shape2D<class_Shape2D>`\ )                                                    |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_clear_shapes<class_CollisionObject2D_method_shape_owner_clear_shapes>`\ (\ owner_id\: :ref:`int<class_int>`\ )                                                                                     |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`                     | :ref:`shape_owner_get_owner<class_CollisionObject2D_method_shape_owner_get_owner>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                                   |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Shape2D<class_Shape2D>`                   | :ref:`shape_owner_get_shape<class_CollisionObject2D_method_shape_owner_get_shape>`\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const|                                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`shape_owner_get_shape_count<class_CollisionObject2D_method_shape_owner_get_shape_count>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                       |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`shape_owner_get_shape_index<class_CollisionObject2D_method_shape_owner_get_shape_index>`\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const|                                     |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform2D<class_Transform2D>`           | :ref:`shape_owner_get_transform<class_CollisionObject2D_method_shape_owner_get_transform>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                           |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_remove_shape<class_CollisionObject2D_method_shape_owner_remove_shape>`\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ )                                                   |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_disabled<class_CollisionObject2D_method_shape_owner_set_disabled>`\ (\ owner_id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>`\ )                                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_one_way_collision<class_CollisionObject2D_method_shape_owner_set_one_way_collision>`\ (\ owner_id\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ )                                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_one_way_collision_direction<class_CollisionObject2D_method_shape_owner_set_one_way_collision_direction>`\ (\ owner_id\: :ref:`int<class_int>`, direction\: :ref:`Vector2<class_Vector2>`\ )    |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_one_way_collision_margin<class_CollisionObject2D_method_shape_owner_set_one_way_collision_margin>`\ (\ owner_id\: :ref:`int<class_int>`, margin\: :ref:`float<class_float>`\ )                 |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_transform<class_CollisionObject2D_method_shape_owner_set_transform>`\ (\ owner_id\: :ref:`int<class_int>`, transform\: :ref:`Transform2D<class_Transform2D>`\ )                                |
   +-------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_CollisionObject2D_signal_input_event:

.. rst-class:: classref-signal

**input_event**\ (\ viewport\: :ref:`Node<class_Node>`, event\: :ref:`InputEvent<class_InputEvent>`, shape_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_signal_input_event>`

Được phát ra khi xảy ra một input event chưa được xử lý. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Xem :ref:`_input_event()<class_CollisionObject2D_private_method__input_event>` để biết chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_entered:

.. rst-class:: classref-signal

**mouse_entered**\ (\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_entered>`

Được phát ra khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không làm signal này được phát ra.

\ **Lưu ý:** Do thiếu cơ chế continuous collision detection, signal này có thể không được phát ra theo thứ tự dự kiến nếu chuột di chuyển đủ nhanh và vùng của **CollisionObject2D** nhỏ. Signal này cũng có thể không được phát ra nếu một **CollisionObject2D** khác đang chồng lấn lên **CollisionObject2D** được đề cập.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_exited:

.. rst-class:: classref-signal

**mouse_exited**\ (\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_exited>`

Được phát ra khi con trỏ chuột rời khỏi tất cả các shape của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không làm signal này được phát ra.

\ **Lưu ý:** Do thiếu cơ chế continuous collision detection, signal này có thể không được phát ra theo thứ tự dự kiến nếu chuột di chuyển đủ nhanh và vùng của **CollisionObject2D** nhỏ. Signal này cũng có thể không được phát ra nếu một **CollisionObject2D** khác đang chồng lấn lên **CollisionObject2D** được đề cập.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_shape_entered:

.. rst-class:: classref-signal

**mouse_shape_entered**\ (\ shape_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_shape_entered>`

Được phát ra khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này hoặc di chuyển từ shape này sang shape khác. ``shape_idx`` là chỉ số child của :ref:`Shape2D<class_Shape2D>` vừa đi vào. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_shape_exited:

.. rst-class:: classref-signal

**mouse_shape_exited**\ (\ shape_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_shape_exited>`

Được phát ra khi con trỏ chuột rời khỏi bất kỳ shape nào của đối tượng này. ``shape_idx`` là chỉ số child của :ref:`Shape2D<class_Shape2D>` vừa rời khỏi. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CollisionObject2D_DisableMode:

.. rst-class:: classref-enumeration

enum **DisableMode**: :ref:`🔗<enum_CollisionObject2D_DisableMode>`

.. _class_CollisionObject2D_constant_DISABLE_MODE_REMOVE:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **DISABLE_MODE_REMOVE** = ``0``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, loại khỏi physics simulation để dừng mọi tương tác vật lý với **CollisionObject2D** này.

Tự động được thêm lại vào physics simulation khi :ref:`Node<class_Node>` được xử lý lại.

.. _class_CollisionObject2D_constant_DISABLE_MODE_MAKE_STATIC:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **DISABLE_MODE_MAKE_STATIC** = ``1``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, chuyển body thành static. Không ảnh hưởng đến :ref:`Area2D<class_Area2D>`. :ref:`PhysicsBody2D<class_PhysicsBody2D>` không thể bị tác động bởi lực hoặc các body khác khi ở trạng thái static.

Tự động đặt :ref:`PhysicsBody2D<class_PhysicsBody2D>` trở lại mode ban đầu khi :ref:`Node<class_Node>` được xử lý lại.

.. _class_CollisionObject2D_constant_DISABLE_MODE_KEEP_ACTIVE:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **DISABLE_MODE_KEEP_ACTIVE** = ``2``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, không tác động đến physics simulation.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CollisionObject2D_property_collision_layer:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_layer** = ``1`` :ref:`🔗<class_CollisionObject2D_property_collision_layer>`

.. rst-class:: classref-property-setget

- |void| **set_collision_layer**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_layer**\ (\ )

Các physics layer mà CollisionObject2D này thuộc về. Các collision object có thể tồn tại trong một hoặc nhiều layer trong số 32 layer khác nhau. Xem thêm :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>`. Để thay đổi giá trị này dễ dàng hơn từ một script, xem :ref:`set_collision_layer_value()<class_CollisionObject2D_method_set_collision_layer_value>`.

\ **Lưu ý:** Object A chỉ có thể phát hiện tiếp xúc với object B nếu object B nằm trong bất kỳ layer nào mà object A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``1`` :ref:`🔗<class_CollisionObject2D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà CollisionObject2D này quét. Các collision object có thể quét một hoặc nhiều layer trong số 32 layer khác nhau. Xem thêm :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>`. Để thay đổi giá trị này dễ dàng hơn từ một script, xem :ref:`set_collision_mask_value()<class_CollisionObject2D_method_set_collision_mask_value>`.

\ **Lưu ý:** Object A chỉ có thể phát hiện tiếp xúc với object B nếu object B nằm trong bất kỳ layer nào mà object A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_property_collision_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_priority** = ``1.0`` :ref:`🔗<class_CollisionObject2D_property_collision_priority>`

.. rst-class:: classref-property-setget

- |void| **set_collision_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_priority**\ (\ )

Độ ưu tiên được sử dụng để giải quyết va chạm khi xảy ra hiện tượng xuyên lấn. Độ ưu tiên càng cao thì mức độ xuyên vào object càng thấp. Ví dụ, có thể dùng thuộc tính này để ngăn player phá vỡ ranh giới của một level.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_property_disable_mode:

.. rst-class:: classref-property

:ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **disable_mode** = ``0`` :ref:`🔗<class_CollisionObject2D_property_disable_mode>`

.. rst-class:: classref-property-setget

- |void| **set_disable_mode**\ (\ value\: :ref:`DisableMode<enum_CollisionObject2D_DisableMode>`\ ) - :ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **get_disable_mode**\ (\ )

Xác định hành vi trong physics khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_property_input_pickable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **input_pickable** = ``true`` :ref:`🔗<class_CollisionObject2D_property_input_pickable>`

.. rst-class:: classref-property-setget

- |void| **set_pickable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_pickable**\ (\ )

Nếu ``true``, object này có thể được chọn. Một object có thể được chọn có thể phát hiện con trỏ chuột đi vào/rời khỏi nó và báo cáo các input event nếu chuột đang ở bên trong nó. Yêu cầu ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CollisionObject2D_private_method__input_event:

.. rst-class:: classref-method

|void| **_input_event**\ (\ viewport\: :ref:`Viewport<class_Viewport>`, event\: :ref:`InputEvent<class_InputEvent>`, shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__input_event>`

Phát hiện các mouse và touch :ref:`InputEvent<class_InputEvent>`\ s chưa được xử lý thông qua ``event`` khi chúng xảy ra trong lúc con trỏ đang ở trên object. Không phát hiện gesture event. ``viewport`` là :ref:`Viewport<class_Viewport>` nơi event bắt nguồn (để phát hiện các viewport khác viewport chính, cần đặt :ref:`Viewport.physics_object_picking<class_Viewport_property_physics_object_picking>` thành ``true``). ``shape_idx`` là chỉ số của shape được phát hiện từ :ref:`PhysicsServer2D<class_PhysicsServer2D>`.

Xem thêm :ref:`Node._unhandled_input()<class_Node_private_method__unhandled_input>`, :ref:`shape_find_owner()<class_CollisionObject2D_method_shape_find_owner>` và :ref:`shape_owner_get_owner()<class_CollisionObject2D_method_shape_owner_get_owner>`.

\ **Lưu ý:** Các event :ref:`InputEventScreenDrag<class_InputEventScreenDrag>` được kích hoạt nếu sự kiện kéo bắt đầu khi con trỏ đang ở trên object hoặc khi object nằm trên đường đi của sự kiện kéo.

\ **Lưu ý:** :ref:`_input_event()<class_CollisionObject2D_private_method__input_event>` yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_enter:

.. rst-class:: classref-method

|void| **_mouse_enter**\ (\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_enter>`

Được gọi khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không khiến hàm này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_exit:

.. rst-class:: classref-method

|void| **_mouse_exit**\ (\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_exit>`

Được gọi khi con trỏ chuột rời khỏi tất cả các shape của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không khiến hàm này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_shape_enter:

.. rst-class:: classref-method

|void| **_mouse_shape_enter**\ (\ shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_shape_enter>`

Được gọi khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này hoặc di chuyển từ shape này sang shape khác. ``shape_idx`` là chỉ số child của :ref:`Shape2D<class_Shape2D>` vừa đi vào. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật để được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_shape_exit:

.. rst-class:: classref-method

|void| **_mouse_shape_exit**\ (\ shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_shape_exit>`

Được gọi khi con trỏ chuột rời khỏi bất kỳ hình dạng nào của đối tượng này. ``shape_idx`` là chỉ mục con của :ref:`Shape2D<class_Shape2D>` đã rời khỏi. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` để được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_create_shape_owner:

.. rst-class:: classref-method

:ref:`int<class_int>` **create_shape_owner**\ (\ owner\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_CollisionObject2D_method_create_shape_owner>`

Tạo một chủ sở hữu hình dạng mới cho đối tượng được cung cấp. Trả về ``owner_id`` của chủ sở hữu mới để tham chiếu trong tương lai.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_collision_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_collision_layer_value>`

Trả về liệu lớp được chỉ định của :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32. Điều này giúp đơn giản hóa việc chỉnh sửa lớp va chạm của **CollisionObject2D** này so với việc gán trực tiếp thuộc tính :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_collision_mask_value>`

Trả về liệu lớp được chỉ định của :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32. Điều này giúp đơn giản hóa việc chỉnh sửa mặt nạ va chạm của **CollisionObject2D** này so với việc gán trực tiếp thuộc tính :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_shape_owner_one_way_collision_direction:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_shape_owner_one_way_collision_direction**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_shape_owner_one_way_collision_direction>`

Trả về ``one_way_collision_direction`` của chủ sở hữu hình dạng được xác định bởi ``owner_id`` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_shape_owner_one_way_collision_margin:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_shape_owner_one_way_collision_margin**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_shape_owner_one_way_collision_margin>`

Trả về ``one_way_collision_margin`` của chủ sở hữu hình dạng được xác định bởi ``owner_id`` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_shape_owners:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_shape_owners**\ (\ ) :ref:`🔗<class_CollisionObject2D_method_get_shape_owners>`

Trả về một :ref:`Array<class_Array>` gồm các mã định danh ``owner_id``. Bạn có thể sử dụng các mã này trong những phương thức khác nhận ``owner_id`` làm đối số.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_is_shape_owner_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_shape_owner_disabled**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_is_shape_owner_disabled>`

Nếu ``true``, chủ sở hữu hình dạng và các hình dạng của nó sẽ bị tắt.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_is_shape_owner_one_way_collision_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_shape_owner_one_way_collision_enabled**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_is_shape_owner_one_way_collision_enabled>`

Trả về ``true`` nếu các va chạm đối với chủ sở hữu hình dạng bắt nguồn từ **CollisionObject2D** này sẽ không được báo cáo là đã va chạm với **CollisionObject2D**\ s.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_remove_shape_owner:

.. rst-class:: classref-method

|void| **remove_shape_owner**\ (\ owner_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_method_remove_shape_owner>`

Xóa chủ sở hữu hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_set_collision_layer_value:

.. rst-class:: classref-method

|void| **set_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_set_collision_layer_value>`

Dựa trên ``value``, bật hoặc tắt lớp được chỉ định trong :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_set_collision_mask_value:

.. rst-class:: classref-method

|void| **set_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_set_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt lớp được chỉ định trong :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_find_owner:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_find_owner**\ (\ shape_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_find_owner>`

Trả về ``owner_id`` của hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_add_shape:

.. rst-class:: classref-method

|void| **shape_owner_add_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape\: :ref:`Shape2D<class_Shape2D>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_add_shape>`

Thêm một :ref:`Shape2D<class_Shape2D>` vào chủ sở hữu hình dạng.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_clear_shapes:

.. rst-class:: classref-method

|void| **shape_owner_clear_shapes**\ (\ owner_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_clear_shapes>`

Xóa tất cả hình dạng khỏi chủ sở hữu hình dạng.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_owner:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **shape_owner_get_owner**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_owner>`

Trả về đối tượng cha của chủ sở hữu hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_shape:

.. rst-class:: classref-method

:ref:`Shape2D<class_Shape2D>` **shape_owner_get_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_shape>`

Trả về :ref:`Shape2D<class_Shape2D>` có ID được cung cấp từ chủ sở hữu hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_owner_get_shape_count**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_shape_count>`

Trả về số lượng hình dạng mà chủ sở hữu hình dạng được cung cấp chứa.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_shape_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_owner_get_shape_index**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_shape_index>`

Trả về chỉ mục con của :ref:`Shape2D<class_Shape2D>` có ID được cung cấp từ chủ sở hữu hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_transform:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **shape_owner_get_transform**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_transform>`

Trả về :ref:`Transform2D<class_Transform2D>` của chủ sở hữu hình dạng.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_remove_shape:

.. rst-class:: classref-method

|void| **shape_owner_remove_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_remove_shape>`

Xóa một hình dạng khỏi chủ sở hữu hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_disabled:

.. rst-class:: classref-method

|void| **shape_owner_set_disabled**\ (\ owner_id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_disabled>`

Nếu ``true``, tắt chủ sở hữu hình dạng được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_one_way_collision:

.. rst-class:: classref-method

|void| **shape_owner_set_one_way_collision**\ (\ owner_id\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_one_way_collision>`

Nếu ``enable`` là ``true``, các va chạm đối với chủ sở hữu hình dạng bắt nguồn từ **CollisionObject2D** này sẽ không được báo cáo là đã va chạm với **CollisionObject2D**\ s.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_one_way_collision_direction:

.. rst-class:: classref-method

|void| **shape_owner_set_one_way_collision_direction**\ (\ owner_id\: :ref:`int<class_int>`, direction\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_one_way_collision_direction>`

Đặt ``one_way_collision_direction`` của chủ sở hữu hình dạng được xác định bởi ``owner_id`` được cung cấp thành ``direction``.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_one_way_collision_margin:

.. rst-class:: classref-method

|void| **shape_owner_set_one_way_collision_margin**\ (\ owner_id\: :ref:`int<class_int>`, margin\: :ref:`float<class_float>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_one_way_collision_margin>`

Đặt ``one_way_collision_margin`` của chủ sở hữu hình dạng được xác định bởi ``owner_id`` được cung cấp thành ``margin`` pixel.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_transform:

.. rst-class:: classref-method

|void| **shape_owner_set_transform**\ (\ owner_id\: :ref:`int<class_int>`, transform\: :ref:`Transform2D<class_Transform2D>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_transform>`

Đặt :ref:`Transform2D<class_Transform2D>` của chủ sở hữu hình dạng được cung cấp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
