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

Abstract base class for 2D physics objects. **CollisionObject2D** can hold any number of :ref:`Shape2D<class_Shape2D>`\ s for collision. Each shape must be assigned to a *shape owner*. Shape owners are not nodes and do not appear in the editor, but are accessible through code using the ``shape_owner_*`` methods.

\ **Lưu ý:** Chỉ hỗ trợ va chạm giữa các đối tượng trong cùng một canvas (:ref:`Viewport<class_Viewport>` canvas hoặc :ref:`CanvasLayer<class_CanvasLayer>`). Hành vi của va chạm giữa các đối tượng trong những canvas khác nhau là không xác định.

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

Được phát ra khi xảy ra input event. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Xem :ref:`_input_event()<class_CollisionObject2D_private_method__input_event>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_entered:

.. rst-class:: classref-signal

**mouse_entered**\ (\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_entered>`

Được phát ra khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không khiến signal này được phát ra.

\ **Lưu ý:** Do thiếu tính năng phát hiện va chạm liên tục, signal này có thể không được phát ra theo thứ tự dự kiến nếu chuột di chuyển đủ nhanh và vùng của **CollisionObject2D** nhỏ. Signal này cũng có thể không được phát ra nếu một **CollisionObject2D** khác đang chồng lấp lên **CollisionObject2D** đang được đề cập.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_exited:

.. rst-class:: classref-signal

**mouse_exited**\ (\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_exited>`

Được phát ra khi con trỏ chuột rời khỏi tất cả các shape của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không khiến signal này được phát ra.

\ **Lưu ý:** Do thiếu tính năng phát hiện va chạm liên tục, signal này có thể không được phát ra theo thứ tự dự kiến nếu chuột di chuyển đủ nhanh và vùng của **CollisionObject2D** nhỏ. Signal này cũng có thể không được phát ra nếu một **CollisionObject2D** khác đang chồng lấp lên **CollisionObject2D** đang được đề cập.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_shape_entered:

.. rst-class:: classref-signal

**mouse_shape_entered**\ (\ shape_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_shape_entered>`

Được phát ra khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này hoặc di chuyển từ shape này sang shape khác. ``shape_idx`` là chỉ mục con của :ref:`Shape2D<class_Shape2D>` mới được đi vào. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_signal_mouse_shape_exited:

.. rst-class:: classref-signal

**mouse_shape_exited**\ (\ shape_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_signal_mouse_shape_exited>`

Được phát ra khi con trỏ chuột rời khỏi bất kỳ shape nào của đối tượng này. ``shape_idx`` là chỉ mục con của :ref:`Shape2D<class_Shape2D>` đã rời khỏi. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

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

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, loại bỏ khỏi physics simulation để dừng mọi tương tác vật lý với **CollisionObject2D** này.

Tự động thêm lại vào physics simulation khi :ref:`Node<class_Node>` được xử lý lần nữa.

.. _class_CollisionObject2D_constant_DISABLE_MODE_MAKE_STATIC:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **DISABLE_MODE_MAKE_STATIC** = ``1``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, đặt body thành static. Không ảnh hưởng đến :ref:`Area2D<class_Area2D>`. :ref:`PhysicsBody2D<class_PhysicsBody2D>` không thể bị tác động bởi lực hoặc các body khác khi đang static.

Tự động đặt :ref:`PhysicsBody2D<class_PhysicsBody2D>` trở lại mode ban đầu khi :ref:`Node<class_Node>` được xử lý lần nữa.

.. _class_CollisionObject2D_constant_DISABLE_MODE_KEEP_ACTIVE:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject2D_DisableMode>` **DISABLE_MODE_KEEP_ACTIVE** = ``2``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, không ảnh hưởng đến physics simulation.

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

Các physics layer mà CollisionObject2D này thuộc về. Các collision object có thể tồn tại trong một hoặc nhiều trong số 32 layer khác nhau. Xem thêm :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>`.

\ **Lưu ý:** Object A chỉ có thể phát hiện tiếp xúc với object B nếu object B nằm trong một trong các layer mà object A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``1`` :ref:`🔗<class_CollisionObject2D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các physics layer mà CollisionObject2D này quét. Các collision object có thể quét một hoặc nhiều trong số 32 layer khác nhau. Xem thêm :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>`.

\ **Lưu ý:** Object A chỉ có thể phát hiện tiếp xúc với object B nếu object B nằm trong một trong các layer mà object A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_property_collision_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_priority** = ``1.0`` :ref:`🔗<class_CollisionObject2D_property_collision_priority>`

.. rst-class:: classref-property-setget

- |void| **set_collision_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_priority**\ (\ )

Priority được sử dụng để giải quyết va chạm khi xảy ra penetration. Priority càng cao thì mức penetration vào đối tượng càng thấp. Ví dụ, có thể dùng thuộc tính này để ngăn player phá vỡ các ranh giới của một level.

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

Nếu ``true``, đối tượng này có thể được chọn. Một đối tượng có thể được chọn có thể phát hiện con trỏ chuột đi vào/rời khỏi và báo cáo các input event khi chuột ở bên trong nó. Yêu cầu có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CollisionObject2D_private_method__input_event:

.. rst-class:: classref-method

|void| **_input_event**\ (\ viewport\: :ref:`Viewport<class_Viewport>`, event\: :ref:`InputEvent<class_InputEvent>`, shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__input_event>`

Accepts unhandled :ref:`InputEvent<class_InputEvent>`\ s. ``shape_idx`` is the child index of the clicked :ref:`Shape2D<class_Shape2D>`. Connect to :ref:`input_event<class_CollisionObject2D_signal_input_event>` to easily pick up these events.

\ **Lưu ý:** :ref:`_input_event()<class_CollisionObject2D_private_method__input_event>` yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_enter:

.. rst-class:: classref-method

|void| **_mouse_enter**\ (\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_enter>`

Được gọi khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không khiến function này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_exit:

.. rst-class:: classref-method

|void| **_mouse_exit**\ (\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_exit>`

Được gọi khi con trỏ chuột rời khỏi tất cả các shape của đối tượng này. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject2D** sẽ không khiến function này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_shape_enter:

.. rst-class:: classref-method

|void| **_mouse_shape_enter**\ (\ shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_shape_enter>`

Được gọi khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này hoặc di chuyển từ shape này sang shape khác. ``shape_idx`` là chỉ mục con của :ref:`Shape2D<class_Shape2D>` mới được đi vào. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật để function được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_private_method__mouse_shape_exit:

.. rst-class:: classref-method

|void| **_mouse_shape_exit**\ (\ shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject2D_private_method__mouse_shape_exit>`

Được gọi khi con trỏ chuột rời khỏi bất kỳ shape nào của đối tượng này. ``shape_idx`` là chỉ mục con của :ref:`Shape2D<class_Shape2D>` đã rời khỏi. Yêu cầu :ref:`input_pickable<class_CollisionObject2D_property_input_pickable>` là ``true`` và có ít nhất một bit :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` được bật để function được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_create_shape_owner:

.. rst-class:: classref-method

:ref:`int<class_int>` **create_shape_owner**\ (\ owner\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_CollisionObject2D_method_create_shape_owner>`

Tạo một shape owner mới cho object đã cho. Trả về ``owner_id`` của owner mới để tham chiếu trong tương lai.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_collision_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_collision_layer_value>`

Trả về layer được chỉ định của :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_collision_mask_value>`

Trả về layer được chỉ định của :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của object.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_shape_owner_one_way_collision_direction:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **get_shape_owner_one_way_collision_direction**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_shape_owner_one_way_collision_direction>`

Trả về ``one_way_collision_direction`` của shape owner được xác định bởi ``owner_id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_shape_owner_one_way_collision_margin:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_shape_owner_one_way_collision_margin**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_get_shape_owner_one_way_collision_margin>`

Trả về ``one_way_collision_margin`` của shape owner được xác định bởi ``owner_id`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_get_shape_owners:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_shape_owners**\ (\ ) :ref:`🔗<class_CollisionObject2D_method_get_shape_owners>`

Trả về một :ref:`Array<class_Array>` gồm các identifier của ``owner_id``. Bạn có thể sử dụng các id này trong những phương thức khác nhận ``owner_id`` làm đối số.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_is_shape_owner_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_shape_owner_disabled**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_is_shape_owner_disabled>`

Nếu ``true``, shape owner và các shape của nó sẽ bị vô hiệu hóa.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_is_shape_owner_one_way_collision_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_shape_owner_one_way_collision_enabled**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_is_shape_owner_one_way_collision_enabled>`

Trả về ``true`` nếu các va chạm đối với shape owner bắt nguồn từ **CollisionObject2D** này sẽ không được báo cáo là đã va chạm với **CollisionObject2D**\ s.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_remove_shape_owner:

.. rst-class:: classref-method

|void| **remove_shape_owner**\ (\ owner_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_method_remove_shape_owner>`

Xóa shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_set_collision_layer_value:

.. rst-class:: classref-method

|void| **set_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_set_collision_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_layer<class_CollisionObject2D_property_collision_layer>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_set_collision_mask_value:

.. rst-class:: classref-method

|void| **set_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_set_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_mask<class_CollisionObject2D_property_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_find_owner:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_find_owner**\ (\ shape_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_find_owner>`

Trả về ``owner_id`` của shape đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_add_shape:

.. rst-class:: classref-method

|void| **shape_owner_add_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape\: :ref:`Shape2D<class_Shape2D>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_add_shape>`

Thêm một :ref:`Shape2D<class_Shape2D>` vào shape owner.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_clear_shapes:

.. rst-class:: classref-method

|void| **shape_owner_clear_shapes**\ (\ owner_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_clear_shapes>`

Xóa tất cả shape khỏi shape owner.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_owner:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **shape_owner_get_owner**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_owner>`

Trả về đối tượng cha của shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_shape:

.. rst-class:: classref-method

:ref:`Shape2D<class_Shape2D>` **shape_owner_get_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_shape>`

Trả về :ref:`Shape2D<class_Shape2D>` có ID đã cho từ shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_owner_get_shape_count**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_shape_count>`

Trả về số lượng shape mà shape owner đã cho chứa.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_shape_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_owner_get_shape_index**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_shape_index>`

Trả về chỉ mục con của :ref:`Shape2D<class_Shape2D>` có ID đã cho từ shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_get_transform:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **shape_owner_get_transform**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject2D_method_shape_owner_get_transform>`

Trả về :ref:`Transform2D<class_Transform2D>` của shape owner.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_remove_shape:

.. rst-class:: classref-method

|void| **shape_owner_remove_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_remove_shape>`

Xóa một shape khỏi shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_disabled:

.. rst-class:: classref-method

|void| **shape_owner_set_disabled**\ (\ owner_id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_disabled>`

Nếu ``true``, vô hiệu hóa shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_one_way_collision:

.. rst-class:: classref-method

|void| **shape_owner_set_one_way_collision**\ (\ owner_id\: :ref:`int<class_int>`, enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_one_way_collision>`

Nếu ``enable`` là ``true``, các va chạm đối với shape owner bắt nguồn từ **CollisionObject2D** này sẽ không được báo cáo là đã va chạm với **CollisionObject2D**\ s.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_one_way_collision_direction:

.. rst-class:: classref-method

|void| **shape_owner_set_one_way_collision_direction**\ (\ owner_id\: :ref:`int<class_int>`, direction\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_one_way_collision_direction>`

Đặt ``one_way_collision_direction`` của shape owner được xác định bởi ``owner_id`` đã cho thành ``direction``.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_one_way_collision_margin:

.. rst-class:: classref-method

|void| **shape_owner_set_one_way_collision_margin**\ (\ owner_id\: :ref:`int<class_int>`, margin\: :ref:`float<class_float>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_one_way_collision_margin>`

Đặt ``one_way_collision_margin`` của shape owner được xác định bởi ``owner_id`` đã cho thành ``margin`` pixel.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject2D_method_shape_owner_set_transform:

.. rst-class:: classref-method

|void| **shape_owner_set_transform**\ (\ owner_id\: :ref:`int<class_int>`, transform\: :ref:`Transform2D<class_Transform2D>`\ ) :ref:`🔗<class_CollisionObject2D_method_shape_owner_set_transform>`

Đặt :ref:`Transform2D<class_Transform2D>` của shape owner đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
