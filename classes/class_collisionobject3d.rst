:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CollisionObject3D.xml.

.. _class_CollisionObject3D:

CollisionObject3D
=================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`Area3D<class_Area3D>`, :ref:`PhysicsBody3D<class_PhysicsBody3D>`

Lớp cơ sở trừu tượng cho các đối tượng vật lý 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Abstract base class for 3D physics objects. **CollisionObject3D** can hold any number of :ref:`Shape3D<class_Shape3D>`\ s for collision. Each shape must be assigned to a *shape owner*. Shape owners are not nodes and do not appear in the editor, but are accessible through code using the ``shape_owner_*`` methods.

\ **Cảnh báo:** Với scale không đồng nhất, node này có thể sẽ không hoạt động như mong đợi. Bạn nên giữ scale giống nhau trên tất cả các trục và thay đổi shape va chạm của nó thay thế.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                  | :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>`             | ``1``     |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                                  | :ref:`collision_mask<class_CollisionObject3D_property_collision_mask>`               | ``1``     |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                              | :ref:`collision_priority<class_CollisionObject3D_property_collision_priority>`       | ``1.0``   |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`DisableMode<enum_CollisionObject3D_DisableMode>` | :ref:`disable_mode<class_CollisionObject3D_property_disable_mode>`                   | ``0``     |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                | :ref:`input_capture_on_drag<class_CollisionObject3D_property_input_capture_on_drag>` | ``false`` |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                | :ref:`input_ray_pickable<class_CollisionObject3D_property_input_ray_pickable>`       | ``true``  |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_input_event<class_CollisionObject3D_private_method__input_event>`\ (\ camera\: :ref:`Camera3D<class_Camera3D>`, event\: :ref:`InputEvent<class_InputEvent>`, event_position\: :ref:`Vector3<class_Vector3>`, normal\: :ref:`Vector3<class_Vector3>`, shape_idx\: :ref:`int<class_int>`\ ) |virtual| |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_mouse_enter<class_CollisionObject3D_private_method__mouse_enter>`\ (\ ) |virtual|                                                                                                                                                                                                                   |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`_mouse_exit<class_CollisionObject3D_private_method__mouse_exit>`\ (\ ) |virtual|                                                                                                                                                                                                                     |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`create_shape_owner<class_CollisionObject3D_method_create_shape_owner>`\ (\ owner\: :ref:`Object<class_Object>`\ )                                                                                                                                                                                    |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`get_collision_layer_value<class_CollisionObject3D_method_get_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                             |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`get_collision_mask_value<class_CollisionObject3D_method_get_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                               |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                           | :ref:`get_rid<class_CollisionObject3D_method_get_rid>`\ (\ ) |const|                                                                                                                                                                                                                                       |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>` | :ref:`get_shape_owners<class_CollisionObject3D_method_get_shape_owners>`\ (\ )                                                                                                                                                                                                                             |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_shape_owner_disabled<class_CollisionObject3D_method_is_shape_owner_disabled>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                     |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`remove_shape_owner<class_CollisionObject3D_method_remove_shape_owner>`\ (\ owner_id\: :ref:`int<class_int>`\ )                                                                                                                                                                                       |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_collision_layer_value<class_CollisionObject3D_method_set_collision_layer_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                                                                                                                                    |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`set_collision_mask_value<class_CollisionObject3D_method_set_collision_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ )                                                                                                                                      |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`shape_find_owner<class_CollisionObject3D_method_shape_find_owner>`\ (\ shape_index\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                                |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_add_shape<class_CollisionObject3D_method_shape_owner_add_shape>`\ (\ owner_id\: :ref:`int<class_int>`, shape\: :ref:`Shape3D<class_Shape3D>`\ )                                                                                                                                          |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_clear_shapes<class_CollisionObject3D_method_shape_owner_clear_shapes>`\ (\ owner_id\: :ref:`int<class_int>`\ )                                                                                                                                                                           |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Object<class_Object>`                     | :ref:`shape_owner_get_owner<class_CollisionObject3D_method_shape_owner_get_owner>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                         |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Shape3D<class_Shape3D>`                   | :ref:`shape_owner_get_shape<class_CollisionObject3D_method_shape_owner_get_shape>`\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                       |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`shape_owner_get_shape_count<class_CollisionObject3D_method_shape_owner_get_shape_count>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                             |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                           | :ref:`shape_owner_get_shape_index<class_CollisionObject3D_method_shape_owner_get_shape_index>`\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                           |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`           | :ref:`shape_owner_get_transform<class_CollisionObject3D_method_shape_owner_get_transform>`\ (\ owner_id\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                                 |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_remove_shape<class_CollisionObject3D_method_shape_owner_remove_shape>`\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ )                                                                                                                                         |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_disabled<class_CollisionObject3D_method_shape_owner_set_disabled>`\ (\ owner_id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>`\ )                                                                                                                                       |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`shape_owner_set_transform<class_CollisionObject3D_method_shape_owner_set_transform>`\ (\ owner_id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ )                                                                                                                      |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_CollisionObject3D_signal_input_event:

.. rst-class:: classref-signal

**input_event**\ (\ camera\: :ref:`Node<class_Node>`, event\: :ref:`InputEvent<class_InputEvent>`, event_position\: :ref:`Vector3<class_Vector3>`, normal\: :ref:`Vector3<class_Vector3>`, shape_idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject3D_signal_input_event>`

Được phát ra khi đối tượng nhận được một :ref:`InputEvent<class_InputEvent>` chưa được xử lý. ``event_position`` là vị trí trong world space của con trỏ chuột trên bề mặt của shape có chỉ mục ``shape_idx`` và ``normal`` là vector pháp tuyến của bề mặt tại điểm đó.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_signal_mouse_entered:

.. rst-class:: classref-signal

**mouse_entered**\ (\ ) :ref:`🔗<class_CollisionObject3D_signal_mouse_entered>`

Được phát ra khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này. Yêu cầu :ref:`input_ray_pickable<class_CollisionObject3D_property_input_ray_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` được thiết lập.

\ **Lưu ý:** Do thiếu cơ chế phát hiện va chạm liên tục, signal này có thể không được phát ra theo thứ tự mong đợi nếu chuột di chuyển đủ nhanh và vùng của **CollisionObject3D** nhỏ. Signal này cũng có thể không được phát ra nếu một **CollisionObject3D** khác đang chồng lấn lên **CollisionObject3D** đang xét.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_signal_mouse_exited:

.. rst-class:: classref-signal

**mouse_exited**\ (\ ) :ref:`🔗<class_CollisionObject3D_signal_mouse_exited>`

Được phát ra khi con trỏ chuột rời khỏi tất cả các shape của đối tượng này. Yêu cầu :ref:`input_ray_pickable<class_CollisionObject3D_property_input_ray_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` được thiết lập.

\ **Lưu ý:** Do thiếu cơ chế phát hiện va chạm liên tục, signal này có thể không được phát ra theo thứ tự mong đợi nếu chuột di chuyển đủ nhanh và vùng của **CollisionObject3D** nhỏ. Signal này cũng có thể không được phát ra nếu một **CollisionObject3D** khác đang chồng lấn lên **CollisionObject3D** đang xét.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CollisionObject3D_DisableMode:

.. rst-class:: classref-enumeration

enum **DisableMode**: :ref:`🔗<enum_CollisionObject3D_DisableMode>`

.. _class_CollisionObject3D_constant_DISABLE_MODE_REMOVE:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject3D_DisableMode>` **DISABLE_MODE_REMOVE** = ``0``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, xóa khỏi mô phỏng vật lý để dừng mọi tương tác vật lý với **CollisionObject3D** này.

Tự động thêm lại vào mô phỏng vật lý khi :ref:`Node<class_Node>` được xử lý lần nữa.

.. _class_CollisionObject3D_constant_DISABLE_MODE_MAKE_STATIC:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject3D_DisableMode>` **DISABLE_MODE_MAKE_STATIC** = ``1``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, chuyển body thành static. Không ảnh hưởng đến :ref:`Area3D<class_Area3D>`. :ref:`PhysicsBody3D<class_PhysicsBody3D>` không thể bị tác động bởi lực hoặc các body khác khi ở trạng thái static.

Tự động đặt :ref:`PhysicsBody3D<class_PhysicsBody3D>` về mode ban đầu khi :ref:`Node<class_Node>` được xử lý lần nữa.

.. _class_CollisionObject3D_constant_DISABLE_MODE_KEEP_ACTIVE:

.. rst-class:: classref-enumeration-constant

:ref:`DisableMode<enum_CollisionObject3D_DisableMode>` **DISABLE_MODE_KEEP_ACTIVE** = ``2``

Khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`, không tác động đến mô phỏng vật lý.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CollisionObject3D_property_collision_layer:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_layer** = ``1`` :ref:`🔗<class_CollisionObject3D_property_collision_layer>`

.. rst-class:: classref-property-setget

- |void| **set_collision_layer**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_layer**\ (\ )

Các layer vật lý mà CollisionObject3D này **nằm trong**. Các đối tượng va chạm có thể tồn tại trong một hoặc nhiều layer trong số 32 layer khác nhau. Xem thêm :ref:`collision_mask<class_CollisionObject3D_property_collision_mask>`.

\ **Lưu ý:** Đối tượng A chỉ có thể phát hiện tiếp xúc với đối tượng B nếu đối tượng B nằm trong bất kỳ layer nào mà đối tượng A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_property_collision_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **collision_mask** = ``1`` :ref:`🔗<class_CollisionObject3D_property_collision_mask>`

.. rst-class:: classref-property-setget

- |void| **set_collision_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_collision_mask**\ (\ )

Các layer vật lý mà CollisionObject3D này **quét**. Các đối tượng va chạm có thể quét một hoặc nhiều layer trong số 32 layer khác nhau. Xem thêm :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>`.

\ **Lưu ý:** Đối tượng A chỉ có thể phát hiện tiếp xúc với đối tượng B nếu đối tượng B nằm trong bất kỳ layer nào mà đối tượng A quét. Xem `Collision layers and masks <../tutorials/physics/physics_introduction.html#collision-layers-and-masks>`__ trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_property_collision_priority:

.. rst-class:: classref-property

:ref:`float<class_float>` **collision_priority** = ``1.0`` :ref:`🔗<class_CollisionObject3D_property_collision_priority>`

.. rst-class:: classref-property-setget

- |void| **set_collision_priority**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_collision_priority**\ (\ )

Mức ưu tiên được sử dụng để giải quyết va chạm khi xảy ra xuyên lấn. Mức ưu tiên càng cao thì độ xuyên vào đối tượng càng thấp. Ví dụ, điều này có thể được sử dụng để ngăn người chơi xuyên qua ranh giới của một level.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_property_disable_mode:

.. rst-class:: classref-property

:ref:`DisableMode<enum_CollisionObject3D_DisableMode>` **disable_mode** = ``0`` :ref:`🔗<class_CollisionObject3D_property_disable_mode>`

.. rst-class:: classref-property-setget

- |void| **set_disable_mode**\ (\ value\: :ref:`DisableMode<enum_CollisionObject3D_DisableMode>`\ ) - :ref:`DisableMode<enum_CollisionObject3D_DisableMode>` **get_disable_mode**\ (\ )

Xác định hành vi trong vật lý khi :ref:`Node.process_mode<class_Node_property_process_mode>` được đặt thành :ref:`Node.PROCESS_MODE_DISABLED<class_Node_constant_PROCESS_MODE_DISABLED>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_property_input_capture_on_drag:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **input_capture_on_drag** = ``false`` :ref:`🔗<class_CollisionObject3D_property_input_capture_on_drag>`

.. rst-class:: classref-property-setget

- |void| **set_capture_input_on_drag**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_capture_input_on_drag**\ (\ )

Nếu ``true``, **CollisionObject3D** sẽ tiếp tục nhận các input event khi chuột được kéo qua các shape của nó.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_property_input_ray_pickable:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **input_ray_pickable** = ``true`` :ref:`🔗<class_CollisionObject3D_property_input_ray_pickable>`

.. rst-class:: classref-property-setget

- |void| **set_ray_pickable**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_ray_pickable**\ (\ )

Nếu ``true``, đối tượng này có thể được chọn. Một đối tượng có thể được chọn có thể phát hiện con trỏ chuột đi vào/rời khỏi, và nếu chuột ở bên trong nó thì báo cáo các input event. Yêu cầu ít nhất một bit :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` được thiết lập.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CollisionObject3D_private_method__input_event:

.. rst-class:: classref-method

|void| **_input_event**\ (\ camera\: :ref:`Camera3D<class_Camera3D>`, event\: :ref:`InputEvent<class_InputEvent>`, event_position\: :ref:`Vector3<class_Vector3>`, normal\: :ref:`Vector3<class_Vector3>`, shape_idx\: :ref:`int<class_int>`\ ) |virtual| :ref:`🔗<class_CollisionObject3D_private_method__input_event>`

Receives unhandled :ref:`InputEvent<class_InputEvent>`\ s. ``event_position`` is the location in world space of the mouse pointer on the surface of the shape with index ``shape_idx`` and ``normal`` is the normal vector of the surface at that point. Connect to the :ref:`input_event<class_CollisionObject3D_signal_input_event>` signal to easily pick up these events.

\ **Lưu ý:** :ref:`_input_event()<class_CollisionObject3D_private_method__input_event>` yêu cầu :ref:`input_ray_pickable<class_CollisionObject3D_property_input_ray_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` được thiết lập.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_private_method__mouse_enter:

.. rst-class:: classref-method

|void| **_mouse_enter**\ (\ ) |virtual| :ref:`🔗<class_CollisionObject3D_private_method__mouse_enter>`

Được gọi khi con trỏ chuột đi vào bất kỳ shape nào của đối tượng này. Yêu cầu :ref:`input_ray_pickable<class_CollisionObject3D_property_input_ray_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` được thiết lập. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject3D** sẽ không khiến hàm này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_private_method__mouse_exit:

.. rst-class:: classref-method

|void| **_mouse_exit**\ (\ ) |virtual| :ref:`🔗<class_CollisionObject3D_private_method__mouse_exit>`

Được gọi khi con trỏ chuột rời khỏi tất cả các shape của đối tượng này. Yêu cầu :ref:`input_ray_pickable<class_CollisionObject3D_property_input_ray_pickable>` là ``true`` và ít nhất một bit :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` được thiết lập. Lưu ý rằng việc di chuyển giữa các shape khác nhau trong cùng một **CollisionObject3D** sẽ không khiến hàm này được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_create_shape_owner:

.. rst-class:: classref-method

:ref:`int<class_int>` **create_shape_owner**\ (\ owner\: :ref:`Object<class_Object>`\ ) :ref:`🔗<class_CollisionObject3D_method_create_shape_owner>`

Tạo một shape owner mới cho đối tượng đã cho. Trả về ``owner_id`` của owner mới để tham chiếu sau này.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_get_collision_layer_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_get_collision_layer_value>`

Trả về liệu layer được chỉ định của :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_get_collision_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_get_collision_mask_value>`

Trả về liệu layer được chỉ định của :ref:`collision_mask<class_CollisionObject3D_property_collision_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_get_rid:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_rid**\ (\ ) |const| :ref:`🔗<class_CollisionObject3D_method_get_rid>`

Trả về :ref:`RID<class_RID>` của đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_get_shape_owners:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_shape_owners**\ (\ ) :ref:`🔗<class_CollisionObject3D_method_get_shape_owners>`

Trả về một :ref:`Array<class_Array>` gồm các mã định danh ``owner_id``. Bạn có thể sử dụng các id này trong những phương thức khác nhận ``owner_id`` làm đối số.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_is_shape_owner_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_shape_owner_disabled**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_is_shape_owner_disabled>`

Nếu ``true``, shape owner và các shape của nó sẽ bị vô hiệu hóa.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_remove_shape_owner:

.. rst-class:: classref-method

|void| **remove_shape_owner**\ (\ owner_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject3D_method_remove_shape_owner>`

Xóa shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_set_collision_layer_value:

.. rst-class:: classref-method

|void| **set_collision_layer_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject3D_method_set_collision_layer_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_layer<class_CollisionObject3D_property_collision_layer>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_set_collision_mask_value:

.. rst-class:: classref-method

|void| **set_collision_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject3D_method_set_collision_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`collision_mask<class_CollisionObject3D_property_collision_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_find_owner:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_find_owner**\ (\ shape_index\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_shape_find_owner>`

Trả về ``owner_id`` của shape đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_add_shape:

.. rst-class:: classref-method

|void| **shape_owner_add_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape\: :ref:`Shape3D<class_Shape3D>`\ ) :ref:`🔗<class_CollisionObject3D_method_shape_owner_add_shape>`

Thêm một :ref:`Shape3D<class_Shape3D>` vào shape owner.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_clear_shapes:

.. rst-class:: classref-method

|void| **shape_owner_clear_shapes**\ (\ owner_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject3D_method_shape_owner_clear_shapes>`

Xóa tất cả shape khỏi shape owner.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_get_owner:

.. rst-class:: classref-method

:ref:`Object<class_Object>` **shape_owner_get_owner**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_shape_owner_get_owner>`

Trả về đối tượng cha của shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_get_shape:

.. rst-class:: classref-method

:ref:`Shape3D<class_Shape3D>` **shape_owner_get_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_shape_owner_get_shape>`

Trả về :ref:`Shape3D<class_Shape3D>` có ID đã cho từ shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_get_shape_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_owner_get_shape_count**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_shape_owner_get_shape_count>`

Trả về số lượng shape mà shape owner đã cho chứa.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_get_shape_index:

.. rst-class:: classref-method

:ref:`int<class_int>` **shape_owner_get_shape_index**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_shape_owner_get_shape_index>`

Trả về chỉ mục con của :ref:`Shape3D<class_Shape3D>` có ID đã cho từ shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_get_transform:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **shape_owner_get_transform**\ (\ owner_id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_CollisionObject3D_method_shape_owner_get_transform>`

Trả về :ref:`Transform3D<class_Transform3D>` của shape owner.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_remove_shape:

.. rst-class:: classref-method

|void| **shape_owner_remove_shape**\ (\ owner_id\: :ref:`int<class_int>`, shape_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CollisionObject3D_method_shape_owner_remove_shape>`

Xóa một shape khỏi shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_set_disabled:

.. rst-class:: classref-method

|void| **shape_owner_set_disabled**\ (\ owner_id\: :ref:`int<class_int>`, disabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_CollisionObject3D_method_shape_owner_set_disabled>`

Nếu ``true``, vô hiệu hóa shape owner đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CollisionObject3D_method_shape_owner_set_transform:

.. rst-class:: classref-method

|void| **shape_owner_set_transform**\ (\ owner_id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_CollisionObject3D_method_shape_owner_set_transform>`

Thiết lập :ref:`Transform3D<class_Transform3D>` của shape owner đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
