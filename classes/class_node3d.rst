:github_url: hide

.. meta::
	:keywords: spatial

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Node3D.xml.

.. _class_Node3D:

Node3D
======

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AudioListener3D<class_AudioListener3D>`, :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>`, :ref:`BoneAttachment3D<class_BoneAttachment3D>`, :ref:`Camera3D<class_Camera3D>`, :ref:`CollisionObject3D<class_CollisionObject3D>`, :ref:`CollisionPolygon3D<class_CollisionPolygon3D>`, :ref:`CollisionShape3D<class_CollisionShape3D>`, :ref:`GridMap<class_GridMap>`, :ref:`ImporterMeshInstance3D<class_ImporterMeshInstance3D>`, :ref:`Joint3D<class_Joint3D>`, :ref:`LightmapProbe<class_LightmapProbe>`, :ref:`Marker3D<class_Marker3D>`, :ref:`NavigationLink3D<class_NavigationLink3D>`, :ref:`NavigationObstacle3D<class_NavigationObstacle3D>`, :ref:`NavigationRegion3D<class_NavigationRegion3D>`, :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>`, :ref:`OpenXRHand<class_OpenXRHand>`, :ref:`OpenXRRenderModel<class_OpenXRRenderModel>`, :ref:`OpenXRRenderModelManager<class_OpenXRRenderModelManager>`, :ref:`Path3D<class_Path3D>`, :ref:`PathFollow3D<class_PathFollow3D>`, :ref:`RayCast3D<class_RayCast3D>`, :ref:`RemoteTransform3D<class_RemoteTransform3D>`, :ref:`ShapeCast3D<class_ShapeCast3D>`, :ref:`Skeleton3D<class_Skeleton3D>`, :ref:`SkeletonModifier3D<class_SkeletonModifier3D>`, :ref:`SpringArm3D<class_SpringArm3D>`, :ref:`SpringBoneCollision3D<class_SpringBoneCollision3D>`, :ref:`VehicleWheel3D<class_VehicleWheel3D>`, :ref:`VisualInstance3D<class_VisualInstance3D>`, :ref:`XRFaceModifier3D<class_XRFaceModifier3D>`, :ref:`XRNode3D<class_XRNode3D>`, :ref:`XROrigin3D<class_XROrigin3D>`

Đối tượng cơ sở trong không gian 3D, được tất cả các node 3D kế thừa.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node **Node3D** là biểu diễn cơ sở của một node trong không gian 3D. Tất cả các node 3D khác đều kế thừa từ class này.

Các phép biến đổi affine (translation, rotation, scale) được tính trong hệ tọa độ tương đối với node cha, trừ khi :ref:`top_level<class_Node3D_property_top_level>` của **Node3D** là ``true``. Trong hệ tọa độ này, các phép biến đổi affine tương ứng với các phép biến đổi affine trực tiếp trên :ref:`transform<class_Node3D_property_transform>` của **Node3D**. Thuật ngữ *parent space* chỉ hệ tọa độ này. Hệ tọa độ gắn với chính **Node3D** được gọi là hệ tọa độ cục bộ của đối tượng, hay *local space*.

\ **Lưu ý:** Trừ khi được chỉ định khác, tất cả các phương thức cần tham số góc phải nhận góc theo *radian*. Để chuyển độ sang radian, hãy sử dụng :ref:`@GlobalScope.deg_to_rad()<class_@GlobalScope_method_deg_to_rad>`.

\ **Lưu ý:** Trong Godot 3 và các phiên bản cũ hơn, **Node3D** có tên là *Spatial*.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Giới thiệu về 3D <../tutorials/3d/introduction_to_3d>`

- `All 3D Demos <https://github.com/godotengine/godot-demo-projects/tree/master/3d>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Basis<class_Basis>`                             | :ref:`basis<class_Node3D_property_basis>`                                     |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Basis<class_Basis>`                             | :ref:`global_basis<class_Node3D_property_global_basis>`                       |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`global_position<class_Node3D_property_global_position>`                 |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`global_rotation<class_Node3D_property_global_rotation>`                 |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`global_rotation_degrees<class_Node3D_property_global_rotation_degrees>` |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`                 | :ref:`global_transform<class_Node3D_property_global_transform>`               |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`position<class_Node3D_property_position>`                               | ``Vector3(0, 0, 0)``                                |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>`                   | :ref:`quaternion<class_Node3D_property_quaternion>`                           |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`rotation<class_Node3D_property_rotation>`                               | ``Vector3(0, 0, 0)``                                |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`rotation_degrees<class_Node3D_property_rotation_degrees>`               |                                                     |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`RotationEditMode<enum_Node3D_RotationEditMode>` | :ref:`rotation_edit_mode<class_Node3D_property_rotation_edit_mode>`           | ``0``                                               |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>`       | :ref:`rotation_order<class_Node3D_property_rotation_order>`                   | ``2``                                               |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                         | :ref:`scale<class_Node3D_property_scale>`                                     | ``Vector3(1, 1, 1)``                                |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`top_level<class_Node3D_property_top_level>`                             | ``false``                                           |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`                 | :ref:`transform<class_Node3D_property_transform>`                             | ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                       | :ref:`visibility_parent<class_Node3D_property_visibility_parent>`             | ``NodePath("")``                                    |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                               | :ref:`visible<class_Node3D_property_visible>`                                 | ``true``                                            |
   +-------------------------------------------------------+-------------------------------------------------------------------------------+-----------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`add_gizmo<class_Node3D_method_add_gizmo>`\ (\ gizmo\: :ref:`Node3DGizmo<class_Node3DGizmo>`\ )                                                                                                                                                                      |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`clear_gizmos<class_Node3D_method_clear_gizmos>`\ (\ )                                                                                                                                                                                                               |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`clear_subgizmo_selection<class_Node3D_method_clear_subgizmo_selection>`\ (\ )                                                                                                                                                                                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`force_update_transform<class_Node3D_method_force_update_transform>`\ (\ )                                                                                                                                                                                           |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Node3DGizmo<class_Node3DGizmo>`\] | :ref:`get_gizmos<class_Node3D_method_get_gizmos>`\ (\ ) |const|                                                                                                                                                                                                           |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`                              | :ref:`get_global_transform_interpolated<class_Node3D_method_get_global_transform_interpolated>`\ (\ )                                                                                                                                                                     |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Node3D<class_Node3D>`                                        | :ref:`get_parent_node_3d<class_Node3D_method_get_parent_node_3d>`\ (\ ) |const|                                                                                                                                                                                           |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`World3D<class_World3D>`                                      | :ref:`get_world_3d<class_Node3D_method_get_world_3d>`\ (\ ) |const|                                                                                                                                                                                                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`global_rotate<class_Node3D_method_global_rotate>`\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )                                                                                                                                    |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`global_scale<class_Node3D_method_global_scale>`\ (\ scale\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                                                                        |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`global_translate<class_Node3D_method_global_translate>`\ (\ offset\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                                                               |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`hide<class_Node3D_method_hide>`\ (\ )                                                                                                                                                                                                                               |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                            | :ref:`is_local_transform_notification_enabled<class_Node3D_method_is_local_transform_notification_enabled>`\ (\ ) |const|                                                                                                                                                 |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                            | :ref:`is_scale_disabled<class_Node3D_method_is_scale_disabled>`\ (\ ) |const|                                                                                                                                                                                             |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                            | :ref:`is_transform_notification_enabled<class_Node3D_method_is_transform_notification_enabled>`\ (\ ) |const|                                                                                                                                                             |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                            | :ref:`is_visible_in_tree<class_Node3D_method_is_visible_in_tree>`\ (\ ) |const|                                                                                                                                                                                           |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`look_at<class_Node3D_method_look_at>`\ (\ target\: :ref:`Vector3<class_Vector3>`, up\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0), use_model_front\: :ref:`bool<class_bool>` = false\ )                                                                       |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`look_at_from_position<class_Node3D_method_look_at_from_position>`\ (\ position\: :ref:`Vector3<class_Vector3>`, target\: :ref:`Vector3<class_Vector3>`, up\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0), use_model_front\: :ref:`bool<class_bool>` = false\ ) |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`orthonormalize<class_Node3D_method_orthonormalize>`\ (\ )                                                                                                                                                                                                           |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`rotate<class_Node3D_method_rotate>`\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )                                                                                                                                                  |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`rotate_object_local<class_Node3D_method_rotate_object_local>`\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )                                                                                                                        |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`rotate_x<class_Node3D_method_rotate_x>`\ (\ angle\: :ref:`float<class_float>`\ )                                                                                                                                                                                    |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`rotate_y<class_Node3D_method_rotate_y>`\ (\ angle\: :ref:`float<class_float>`\ )                                                                                                                                                                                    |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`rotate_z<class_Node3D_method_rotate_z>`\ (\ angle\: :ref:`float<class_float>`\ )                                                                                                                                                                                    |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`scale_object_local<class_Node3D_method_scale_object_local>`\ (\ scale\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                                                            |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`set_disable_scale<class_Node3D_method_set_disable_scale>`\ (\ disable\: :ref:`bool<class_bool>`\ )                                                                                                                                                                  |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`set_identity<class_Node3D_method_set_identity>`\ (\ )                                                                                                                                                                                                               |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`set_ignore_transform_notification<class_Node3D_method_set_ignore_transform_notification>`\ (\ enabled\: :ref:`bool<class_bool>`\ )                                                                                                                                  |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`set_notify_local_transform<class_Node3D_method_set_notify_local_transform>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                                                 |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`set_notify_transform<class_Node3D_method_set_notify_transform>`\ (\ enable\: :ref:`bool<class_bool>`\ )                                                                                                                                                             |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`set_subgizmo_selection<class_Node3D_method_set_subgizmo_selection>`\ (\ gizmo\: :ref:`Node3DGizmo<class_Node3DGizmo>`, id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ )                                                             |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`show<class_Node3D_method_show>`\ (\ )                                                                                                                                                                                                                               |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                      | :ref:`to_global<class_Node3D_method_to_global>`\ (\ local_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                                                                |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                                      | :ref:`to_local<class_Node3D_method_to_local>`\ (\ global_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                                                                 |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`translate<class_Node3D_method_translate>`\ (\ offset\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                                                                             |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`translate_object_local<class_Node3D_method_translate_object_local>`\ (\ offset\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                                                   |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                             | :ref:`update_gizmos<class_Node3D_method_update_gizmos>`\ (\ )                                                                                                                                                                                                             |
   +--------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_Node3D_signal_visibility_changed:

.. rst-class:: classref-signal

**visibility_changed**\ (\ ) :ref:`🔗<class_Node3D_signal_visibility_changed>`

Được phát ra khi khả năng hiển thị của node này thay đổi (xem :ref:`visible<class_Node3D_property_visible>` và :ref:`is_visible_in_tree()<class_Node3D_method_is_visible_in_tree>`).

Signal này được phát ra *sau* notification :ref:`NOTIFICATION_VISIBILITY_CHANGED<class_Node3D_constant_NOTIFICATION_VISIBILITY_CHANGED>` liên quan.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_Node3D_RotationEditMode:

.. rst-class:: classref-enumeration

enum **RotationEditMode**: :ref:`🔗<enum_Node3D_RotationEditMode>`

.. _class_Node3D_constant_ROTATION_EDIT_MODE_EULER:

.. rst-class:: classref-enumeration-constant

:ref:`RotationEditMode<enum_Node3D_RotationEditMode>` **ROTATION_EDIT_MODE_EULER** = ``0``

Rotation được chỉnh sửa bằng :ref:`Vector3<class_Vector3>` trong `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__. Trong Godot, các góc Euler luôn sử dụng thứ tự nội tại, nghĩa là rotation diễn ra quanh các trục cục bộ của đối tượng.

.. _class_Node3D_constant_ROTATION_EDIT_MODE_QUATERNION:

.. rst-class:: classref-enumeration-constant

:ref:`RotationEditMode<enum_Node3D_RotationEditMode>` **ROTATION_EDIT_MODE_QUATERNION** = ``1``

Rotation được chỉnh sửa bằng :ref:`Quaternion<class_Quaternion>`. Quaternion tránh được :doc:`gimbal lock <../tutorials/3d/using_transforms>` và không cần chọn thứ tự rotation, nhưng kém trực quan hơn. Rotation bằng quaternion hầu như giống với rotor trong đại số hình học 3D, ngoại trừ việc các số được đặt tên khác nhau.

.. _class_Node3D_constant_ROTATION_EDIT_MODE_BASIS:

.. rst-class:: classref-enumeration-constant

:ref:`RotationEditMode<enum_Node3D_RotationEditMode>` **ROTATION_EDIT_MODE_BASIS** = ``2``

Rotation được chỉnh sửa bằng :ref:`Basis<class_Basis>`. Ở chế độ này, các trục của :ref:`basis<class_Node3D_property_basis>` thô có thể được tự do sửa đổi, nhưng thuộc tính :ref:`scale<class_Node3D_property_scale>` không khả dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_Node3D_constant_NOTIFICATION_TRANSFORM_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_TRANSFORM_CHANGED** = ``2000`` :ref:`🔗<class_Node3D_constant_NOTIFICATION_TRANSFORM_CHANGED>`

Notification được nhận khi :ref:`global_transform<class_Node3D_property_global_transform>` của node này thay đổi, nếu :ref:`is_transform_notification_enabled()<class_Node3D_method_is_transform_notification_enabled>` là ``true``. Xem thêm :ref:`set_notify_transform()<class_Node3D_method_set_notify_transform>`.

\ **Lưu ý:** Hầu hết các node 3D như :ref:`VisualInstance3D<class_VisualInstance3D>` hoặc :ref:`CollisionObject3D<class_CollisionObject3D>` đều tự động bật tính năng này để hoạt động chính xác.

\ **Lưu ý:** Trong editor, các node sẽ truyền notification này đến các node con nếu có gizmo được gắn vào (xem :ref:`add_gizmo()<class_Node3D_method_add_gizmo>`).

.. _class_Node3D_constant_NOTIFICATION_ENTER_WORLD:

.. rst-class:: classref-constant

**NOTIFICATION_ENTER_WORLD** = ``41`` :ref:`🔗<class_Node3D_constant_NOTIFICATION_ENTER_WORLD>`

Notification được nhận khi node này được đăng ký vào một :ref:`World3D<class_World3D>` mới (xem :ref:`get_world_3d()<class_Node3D_method_get_world_3d>`).

.. _class_Node3D_constant_NOTIFICATION_EXIT_WORLD:

.. rst-class:: classref-constant

**NOTIFICATION_EXIT_WORLD** = ``42`` :ref:`🔗<class_Node3D_constant_NOTIFICATION_EXIT_WORLD>`

Notification được nhận khi node này được hủy đăng ký khỏi :ref:`World3D<class_World3D>` hiện tại (xem :ref:`get_world_3d()<class_Node3D_method_get_world_3d>`).

Notification này được gửi theo thứ tự ngược.

.. _class_Node3D_constant_NOTIFICATION_VISIBILITY_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_VISIBILITY_CHANGED** = ``43`` :ref:`🔗<class_Node3D_constant_NOTIFICATION_VISIBILITY_CHANGED>`

Notification được nhận khi khả năng hiển thị của node này thay đổi (xem :ref:`visible<class_Node3D_property_visible>` và :ref:`is_visible_in_tree()<class_Node3D_method_is_visible_in_tree>`).

Notification này được nhận *trước* signal :ref:`visibility_changed<class_Node3D_signal_visibility_changed>` liên quan.

.. _class_Node3D_constant_NOTIFICATION_LOCAL_TRANSFORM_CHANGED:

.. rst-class:: classref-constant

**NOTIFICATION_LOCAL_TRANSFORM_CHANGED** = ``44`` :ref:`🔗<class_Node3D_constant_NOTIFICATION_LOCAL_TRANSFORM_CHANGED>`

Notification được nhận khi :ref:`transform<class_Node3D_property_transform>` của node này thay đổi, nếu :ref:`is_local_transform_notification_enabled()<class_Node3D_method_is_local_transform_notification_enabled>` là ``true``. Notification này không được nhận khi :ref:`transform<class_Node3D_property_transform>` của **Node3D** cha thay đổi. Xem thêm :ref:`set_notify_local_transform()<class_Node3D_method_set_notify_local_transform>`.

\ **Lưu ý:** Một số node 3D như :ref:`CSGShape3D<class_CSGShape3D>` hoặc :ref:`CollisionShape3D<class_CollisionShape3D>` tự động bật tính năng này để hoạt động chính xác.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Node3D_property_basis:

.. rst-class:: classref-property

:ref:`Basis<class_Basis>` **basis** :ref:`🔗<class_Node3D_property_basis>`

.. rst-class:: classref-property-setget

- |void| **set_basis**\ (\ value\: :ref:`Basis<class_Basis>`\ ) - :ref:`Basis<class_Basis>` **get_basis**\ (\ )

Basis của thuộc tính :ref:`transform<class_Node3D_property_transform>`. Biểu diễn rotation, scale và shear của node này trong parent space (tương đối với node cha).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_global_basis:

.. rst-class:: classref-property

:ref:`Basis<class_Basis>` **global_basis** :ref:`🔗<class_Node3D_property_global_basis>`

.. rst-class:: classref-property-setget

- |void| **set_global_basis**\ (\ value\: :ref:`Basis<class_Basis>`\ ) - :ref:`Basis<class_Basis>` **get_global_basis**\ (\ )

Basis của thuộc tính :ref:`global_transform<class_Node3D_property_global_transform>`. Biểu diễn rotation, scale và shear của node này trong global space (tương đối với world).

\ **Lưu ý:** Nếu node không nằm trong tree, việc lấy thuộc tính này sẽ thất bại và trả về :ref:`Basis.IDENTITY<class_Basis_constant_IDENTITY>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_global_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **global_position** :ref:`🔗<class_Node3D_property_global_position>`

.. rst-class:: classref-property-setget

- |void| **set_global_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_global_position**\ (\ )

Global position (translation) of this node in global space (relative to the world). This is equivalent to the :ref:`global_transform<class_Node3D_property_global_transform>`'s :ref:`Transform3D.origin<class_Transform3D_property_origin>`.

\ **Lưu ý:** Nếu node không nằm trong tree, việc lấy thuộc tính này sẽ thất bại và trả về :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_global_rotation:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **global_rotation** :ref:`🔗<class_Node3D_property_global_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_global_rotation**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_global_rotation**\ (\ )

Global rotation của node này dưới dạng `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__, theo radian và trong global space (tương đối với world). Giá trị này được lấy từ rotation của :ref:`global_basis<class_Node3D_property_global_basis>`.

- :ref:`Vector3.x<class_Vector3_property_x>` là góc quanh trục X global (pitch);

- :ref:`Vector3.y<class_Vector3_property_y>` là góc quanh trục Y global (yaw);

- :ref:`Vector3.z<class_Vector3_property_z>` là góc quanh trục Z global (roll).

\ **Lưu ý:** Không giống :ref:`rotation<class_Node3D_property_rotation>`, thuộc tính này luôn tuân theo quy ước YXZ (:ref:`@GlobalScope.EULER_ORDER_YXZ<class_@GlobalScope_constant_EULER_ORDER_YXZ>`).

\ **Lưu ý:** Nếu node không nằm trong tree, việc lấy thuộc tính này sẽ thất bại và trả về :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_global_rotation_degrees:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **global_rotation_degrees** :ref:`🔗<class_Node3D_property_global_rotation_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_global_rotation_degrees**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_global_rotation_degrees**\ (\ )

:ref:`global_rotation<class_Node3D_property_global_rotation>` của node này, theo độ thay vì radian.

\ **Lưu ý:** Nếu node không nằm trong tree, việc lấy thuộc tính này sẽ thất bại và trả về :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_global_transform:

.. rst-class:: classref-property

:ref:`Transform3D<class_Transform3D>` **global_transform** :ref:`🔗<class_Node3D_property_global_transform>`

.. rst-class:: classref-property-setget

- |void| **set_global_transform**\ (\ value\: :ref:`Transform3D<class_Transform3D>`\ ) - :ref:`Transform3D<class_Transform3D>` **get_global_transform**\ (\ )

Phép biến đổi của node này trong global space (tương đối với world). Chứa và biểu diễn :ref:`global_position<class_Node3D_property_global_position>`, :ref:`global_rotation<class_Node3D_property_global_rotation>` và scale global của node này.

\ **Lưu ý:** Nếu node không nằm trong tree, việc lấy thuộc tính này sẽ thất bại và trả về :ref:`Transform3D.IDENTITY<class_Transform3D_constant_IDENTITY>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_Node3D_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_position**\ (\ )

Position (translation) of this node in parent space (relative to the parent node). This is equivalent to the :ref:`transform<class_Node3D_property_transform>`'s :ref:`Transform3D.origin<class_Transform3D_property_origin>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_quaternion:

.. rst-class:: classref-property

:ref:`Quaternion<class_Quaternion>` **quaternion** :ref:`🔗<class_Node3D_property_quaternion>`

.. rst-class:: classref-property-setget

- |void| **set_quaternion**\ (\ value\: :ref:`Quaternion<class_Quaternion>`\ ) - :ref:`Quaternion<class_Quaternion>` **get_quaternion**\ (\ )

Rotation của node này được biểu diễn dưới dạng :ref:`Quaternion<class_Quaternion>` trong parent space (tương đối với node cha). Giá trị này được lấy từ rotation của :ref:`basis<class_Node3D_property_basis>`.

\ **Lưu ý:** Quaternion phù hợp hơn nhiều cho phép toán 3D nhưng kém trực quan hơn. Việc thiết lập thuộc tính này có thể hữu ích cho interpolation (xem :ref:`Quaternion.slerp()<class_Quaternion_method_slerp>`).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_rotation:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **rotation** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_Node3D_property_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_rotation**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_rotation**\ (\ )

Rotation của node này dưới dạng `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__, tính bằng radian và trong parent space (so với node cha). Giá trị này được lấy từ rotation của :ref:`basis<class_Node3D_property_basis>`.

- :ref:`Vector3.x<class_Vector3_property_x>` là góc quanh trục X cục bộ (pitch);

- :ref:`Vector3.y<class_Vector3_property_y>` là góc quanh trục Y cục bộ (yaw);

- :ref:`Vector3.z<class_Vector3_property_z>` là góc quanh trục Z cục bộ (roll).

Thứ tự của mỗi rotation liên tiếp có thể được thay đổi bằng :ref:`rotation_order<class_Node3D_property_rotation_order>` (xem các hằng số :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>`). Trong Godot, các góc Euler luôn sử dụng thứ tự intrinsic. Theo mặc định, quy ước intrinsic YXZ được sử dụng (:ref:`@GlobalScope.EULER_ORDER_YXZ<class_@GlobalScope_constant_EULER_ORDER_YXZ>`).

\ **Lưu ý:** Thuộc tính này được chỉnh sửa theo độ trong inspector. Nếu bạn muốn sử dụng độ trong script, hãy dùng :ref:`rotation_degrees<class_Node3D_property_rotation_degrees>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_rotation_degrees:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **rotation_degrees** :ref:`🔗<class_Node3D_property_rotation_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_degrees**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_rotation_degrees**\ (\ )

:ref:`rotation<class_Node3D_property_rotation>` của node này, tính bằng độ thay vì radian.

\ **Lưu ý:** Đây **không phải** là thuộc tính có trong Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_rotation_edit_mode:

.. rst-class:: classref-property

:ref:`RotationEditMode<enum_Node3D_RotationEditMode>` **rotation_edit_mode** = ``0`` :ref:`🔗<class_Node3D_property_rotation_edit_mode>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_edit_mode**\ (\ value\: :ref:`RotationEditMode<enum_Node3D_RotationEditMode>`\ ) - :ref:`RotationEditMode<enum_Node3D_RotationEditMode>` **get_rotation_edit_mode**\ (\ )

Cách rotation và scale của node này được hiển thị trong Inspector dock.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_rotation_order:

.. rst-class:: classref-property

:ref:`EulerOrder<enum_@GlobalScope_EulerOrder>` **rotation_order** = ``2`` :ref:`🔗<class_Node3D_property_rotation_order>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_order**\ (\ value\: :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>`\ ) - :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>` **get_rotation_order**\ (\ )

Thứ tự rotation của các trục của thuộc tính :ref:`rotation<class_Node3D_property_rotation>`. Trong Godot, các góc Euler luôn sử dụng thứ tự intrinsic, nghĩa là hướng cuối cùng được tính bằng cách xoay quanh các trục cục bộ theo thứ tự này.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_scale:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **scale** = ``Vector3(1, 1, 1)`` :ref:`🔗<class_Node3D_property_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scale**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_scale**\ (\ )

Scale của node này trong local space (so với chính node này). Giá trị này được lấy từ scale của :ref:`basis<class_Node3D_property_basis>`.

\ **Lưu ý:** Một số loại node 3D không bị ảnh hưởng bởi thuộc tính này. Các loại này bao gồm :ref:`Light3D<class_Light3D>`, :ref:`Camera3D<class_Camera3D>`, :ref:`AudioStreamPlayer3D<class_AudioStreamPlayer3D>` và các loại khác.

\ **Cảnh báo:** Các component của scale phải hoặc đều dương hoặc đều âm, và **không** được chính xác bằng ``0.0``. Nếu không, sẽ không thể lấy scale từ :ref:`basis<class_Node3D_property_basis>`. Điều này có thể khiến scale dự định bị mất khi tải lại từ đĩa, cũng như gây ra các hành vi không ổn định khác.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_top_level:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **top_level** = ``false`` :ref:`🔗<class_Node3D_property_top_level>`

.. rst-class:: classref-property-setget

- |void| **set_as_top_level**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_set_as_top_level**\ (\ )

Nếu ``true``, node sẽ không kế thừa các phép biến đổi từ node cha. Do đó, các phép biến đổi của node sẽ chỉ nằm trong global space, đồng nghĩa với việc :ref:`global_transform<class_Node3D_property_global_transform>` và :ref:`transform<class_Node3D_property_transform>` sẽ giống hệt nhau.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_transform:

.. rst-class:: classref-property

:ref:`Transform3D<class_Transform3D>` **transform** = ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` :ref:`🔗<class_Node3D_property_transform>`

.. rst-class:: classref-property-setget

- |void| **set_transform**\ (\ value\: :ref:`Transform3D<class_Transform3D>`\ ) - :ref:`Transform3D<class_Transform3D>` **get_transform**\ (\ )

Phép biến đổi cục bộ của node này, trong parent space (so với node cha). Chứa và biểu diễn :ref:`position<class_Node3D_property_position>`, :ref:`rotation<class_Node3D_property_rotation>` và :ref:`scale<class_Node3D_property_scale>` của node này.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_visibility_parent:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **visibility_parent** = ``NodePath("")`` :ref:`🔗<class_Node3D_property_visibility_parent>`

.. rst-class:: classref-property-setget

- |void| **set_visibility_parent**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_visibility_parent**\ (\ )

Đường dẫn đến visibility range parent của node này và các node con của nó. Visibility parent phải là một :ref:`GeometryInstance3D<class_GeometryInstance3D>`.

Mọi visual instance chỉ hiển thị khi visibility parent (và tất cả visibility ancestor của nó) bị ẩn do ở gần camera hơn :ref:`GeometryInstance3D.visibility_range_begin<class_GeometryInstance3D_property_visibility_range_begin>` của chính nó. Các node bị ẩn thông qua thuộc tính :ref:`visible<class_Node3D_property_visible>` về cơ bản sẽ bị loại khỏi cây phụ thuộc visibility, vì vậy các instance phụ thuộc sẽ không tính đến node bị ẩn hoặc các node con của nó.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_property_visible:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **visible** = ``true`` :ref:`🔗<class_Node3D_property_visible>`

.. rst-class:: classref-property-setget

- |void| **set_visible**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_visible**\ (\ )

Nếu ``true``, node này có thể hiển thị. Node chỉ được render khi tất cả ancestor của nó cũng đang hiển thị. Điều đó có nghĩa là :ref:`is_visible_in_tree()<class_Node3D_method_is_visible_in_tree>` phải trả về ``true``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_Node3D_method_add_gizmo:

.. rst-class:: classref-method

|void| **add_gizmo**\ (\ gizmo\: :ref:`Node3DGizmo<class_Node3DGizmo>`\ ) :ref:`🔗<class_Node3D_method_add_gizmo>`

Gắn ``gizmo`` đã cho vào node này. Chỉ hoạt động trong editor.

\ **Lưu ý:** ``gizmo`` phải là một :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`. Kiểu đối số là :ref:`Node3DGizmo<class_Node3DGizmo>` để tránh phụ thuộc vào các editor class trong **Node3D**.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_clear_gizmos:

.. rst-class:: classref-method

|void| **clear_gizmos**\ (\ ) :ref:`🔗<class_Node3D_method_clear_gizmos>`

Xóa tất cả object :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` được gắn vào node này. Chỉ hoạt động trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_clear_subgizmo_selection:

.. rst-class:: classref-method

|void| **clear_subgizmo_selection**\ (\ ) :ref:`🔗<class_Node3D_method_clear_subgizmo_selection>`

Bỏ chọn tất cả subgizmo của node này. Hữu ích khi gọi lúc subgizmo đang được chọn có thể không còn tồn tại sau khi một thuộc tính thay đổi. Chỉ hoạt động trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_force_update_transform:

.. rst-class:: classref-method

|void| **force_update_transform**\ (\ ) :ref:`🔗<class_Node3D_method_force_update_transform>`

Buộc :ref:`global_transform<class_Node3D_property_global_transform>` của node cập nhật bằng cách gửi :ref:`NOTIFICATION_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_TRANSFORM_CHANGED>`. Sẽ thất bại nếu node không nằm trong tree.

\ **Lưu ý:** Vì lý do hiệu năng, các thay đổi transform thường được tích lũy và áp dụng *một lần* vào cuối frame. Bản cập nhật cũng lan truyền qua các node con **Node3D**. Do đó, chỉ sử dụng method này khi bạn cần transform mới nhất (chẳng hạn trong các phép toán physics).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_get_gizmos:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Node3DGizmo<class_Node3DGizmo>`\] **get_gizmos**\ (\ ) |const| :ref:`🔗<class_Node3D_method_get_gizmos>`

Trả về tất cả object :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` được gắn vào node này. Chỉ hoạt động trong editor.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_get_global_transform_interpolated:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **get_global_transform_interpolated**\ (\ ) :ref:`🔗<class_Node3D_method_get_global_transform_interpolated>`

Khi sử dụng physics interpolation, sẽ có những trường hợp bạn muốn biết transform đã nội suy (đang hiển thị) của một node thay vì transform tiêu chuẩn (có thể chỉ chính xác đến physics tick gần nhất).

Điều này đặc biệt quan trọng đối với các thao tác dựa trên frame diễn ra trong :ref:`Node._process()<class_Node_private_method__process>`, thay vì :ref:`Node._physics_process()<class_Node_private_method__physics_process>`. Ví dụ gồm việc :ref:`Camera3D<class_Camera3D>`\ s tập trung vào một node hoặc tìm vị trí để bắn laser trong một frame thay vì physics tick.

\ **Lưu ý:** Lần đầu được gọi, function này tạo một interpolation pump trên **Node3D**, có thể phản hồi các lần reset physics interpolation. Nếu gặp vấn đề về hiện tượng "streaking" khi ban đầu bám theo một **Node3D**, hãy đảm bảo gọi :ref:`get_global_transform_interpolated()<class_Node3D_method_get_global_transform_interpolated>` ít nhất một lần *trước khi* reset physics interpolation của **Node3D**.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_get_parent_node_3d:

.. rst-class:: classref-method

:ref:`Node3D<class_Node3D>` **get_parent_node_3d**\ (\ ) |const| :ref:`🔗<class_Node3D_method_get_parent_node_3d>`

Trả về **Node3D** cha trực tiếp ảnh hưởng đến :ref:`global_transform<class_Node3D_property_global_transform>` của node này. Trả về ``null`` nếu không tồn tại node cha, node cha không phải là **Node3D**, hoặc :ref:`top_level<class_Node3D_property_top_level>` là ``true``.

\ **Lưu ý:** Method này không phải lúc nào cũng tương đương với :ref:`Node.get_parent()<class_Node_method_get_parent>`, vốn không tính đến :ref:`top_level<class_Node3D_property_top_level>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_get_world_3d:

.. rst-class:: classref-method

:ref:`World3D<class_World3D>` **get_world_3d**\ (\ ) |const| :ref:`🔗<class_Node3D_method_get_world_3d>`

Trả về :ref:`World3D<class_World3D>` mà node này đã đăng ký.

Thông thường, đây là world được viewport của node này sử dụng (xem :ref:`Node.get_viewport()<class_Node_method_get_viewport>` và :ref:`Viewport.find_world_3d()<class_Viewport_method_find_world_3d>`).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_global_rotate:

.. rst-class:: classref-method

|void| **global_rotate**\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node3D_method_global_rotate>`

Xoay :ref:`global_basis<class_Node3D_property_global_basis>` của node này quanh ``axis`` toàn cục theo ``angle`` đã cho, tính bằng radian. Thao tác này được tính trong global space (so với world) và giữ nguyên :ref:`global_position<class_Node3D_property_global_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_global_scale:

.. rst-class:: classref-method

|void| **global_scale**\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Node3D_method_global_scale>`

Scale :ref:`global_basis<class_Node3D_property_global_basis>` của node này theo hệ số ``scale`` đã cho. Thao tác này được tính trong global space (so với world) và giữ nguyên :ref:`global_position<class_Node3D_property_global_position>`.

\ **Lưu ý:** Không được nhầm method này với thuộc tính :ref:`scale<class_Node3D_property_scale>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_global_translate:

.. rst-class:: classref-method

|void| **global_translate**\ (\ offset\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Node3D_method_global_translate>`

Cộng translation ``offset`` đã cho vào :ref:`global_position<class_Node3D_property_global_position>` của node trong global space (so với world).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_hide:

.. rst-class:: classref-method

|void| **hide**\ (\ ) :ref:`🔗<class_Node3D_method_hide>`

Ngăn node này được render. Tương đương với việc đặt :ref:`visible<class_Node3D_property_visible>` thành ``false``. Đây là điều ngược lại với :ref:`show()<class_Node3D_method_show>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_is_local_transform_notification_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_local_transform_notification_enabled**\ (\ ) |const| :ref:`🔗<class_Node3D_method_is_local_transform_notification_enabled>`

Trả về ``true`` nếu node nhận được :ref:`NOTIFICATION_LOCAL_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_LOCAL_TRANSFORM_CHANGED>` mỗi khi :ref:`transform<class_Node3D_property_transform>` thay đổi. Tùy chọn này được bật bằng :ref:`set_notify_local_transform()<class_Node3D_method_set_notify_local_transform>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_is_scale_disabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_scale_disabled**\ (\ ) |const| :ref:`🔗<class_Node3D_method_is_scale_disabled>`

Trả về ``true`` nếu :ref:`global_transform<class_Node3D_property_global_transform>` của node này được tự động chuẩn hóa trực giao. Điều này khiến node không bị biến dạng, như thể scale toàn cục của nó được đặt thành :ref:`Vector3.ONE<class_Vector3_constant_ONE>` (hoặc giá trị đối của nó). Xem thêm :ref:`set_disable_scale()<class_Node3D_method_set_disable_scale>` và :ref:`orthonormalize()<class_Node3D_method_orthonormalize>`.

\ **Lưu ý:** :ref:`transform<class_Node3D_property_transform>` không bị ảnh hưởng bởi thiết lập này.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_is_transform_notification_enabled:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_transform_notification_enabled**\ (\ ) |const| :ref:`🔗<class_Node3D_method_is_transform_notification_enabled>`

Trả về ``true`` nếu node nhận được :ref:`NOTIFICATION_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_TRANSFORM_CHANGED>` mỗi khi :ref:`global_transform<class_Node3D_property_global_transform>` thay đổi. Tùy chọn này được bật bằng :ref:`set_notify_transform()<class_Node3D_method_set_notify_transform>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_is_visible_in_tree:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_visible_in_tree**\ (\ ) |const| :ref:`🔗<class_Node3D_method_is_visible_in_tree>`

Trả về ``true`` nếu node này nằm trong scene tree và thuộc tính :ref:`visible<class_Node3D_property_visible>` là ``true`` đối với node này cùng tất cả tổ tiên **Node3D** của nó *theo thứ tự*. Tổ tiên thuộc bất kỳ kiểu nào khác (chẳng hạn như :ref:`Node<class_Node>` hoặc :ref:`Node2D<class_Node2D>`) sẽ phá vỡ chuỗi này. Xem thêm :ref:`Node.get_parent()<class_Node_method_get_parent>`.

\ **Lưu ý:** Phương thức này không thể tính đến :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>`, vì vậy ngay cả khi phương thức này trả về ``true``, node vẫn có thể không được render.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_look_at:

.. rst-class:: classref-method

|void| **look_at**\ (\ target\: :ref:`Vector3<class_Vector3>`, up\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0), use_model_front\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node3D_method_look_at>`

Xoay node sao cho trục tiến cục bộ (-Z, :ref:`Vector3.FORWARD<class_Vector3_constant_FORWARD>`) hướng về vị trí ``target``. Thao tác này được tính trong không gian toàn cục (tương đối với world).

Trục lên cục bộ (+Y) hướng gần nhất có thể về vector ``up`` trong khi vẫn vuông góc với trục tiến cục bộ. Transform kết quả là trực giao và scale được giữ nguyên. Scale không đồng nhất có thể không hoạt động chính xác.

Vị trí ``target`` không thể trùng với vị trí của node, vector ``up`` không thể là :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`. Ngoài ra, hướng từ vị trí của node đến vị trí ``target`` không thể song song với vector ``up``, để tránh việc xoay ngoài ý muốn quanh trục Z cục bộ.

Nếu ``use_model_front`` là ``true``, trục +Z (mặt trước của asset) được xem là hướng tiến (ngụ ý +X là bên trái) và hướng về vị trí ``target``. Theo mặc định, trục -Z (hướng tiến của camera) được xem là hướng tiến (ngụ ý +X là bên phải).

\ **Lưu ý:** Phương thức này thất bại nếu node không nằm trong scene tree. Nếu cần, hãy sử dụng :ref:`look_at_from_position()<class_Node3D_method_look_at_from_position>` thay thế.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_look_at_from_position:

.. rst-class:: classref-method

|void| **look_at_from_position**\ (\ position\: :ref:`Vector3<class_Vector3>`, target\: :ref:`Vector3<class_Vector3>`, up\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0), use_model_front\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node3D_method_look_at_from_position>`

Di chuyển node đến ``position`` được chỉ định, sau đó xoay node để hướng về vị trí ``target``, tương tự như :ref:`look_at()<class_Node3D_method_look_at>`. Thao tác này được tính trong không gian toàn cục (tương đối với world).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_orthonormalize:

.. rst-class:: classref-method

|void| **orthonormalize**\ (\ ) :ref:`🔗<class_Node3D_method_orthonormalize>`

Chuẩn hóa trực giao :ref:`basis<class_Node3D_property_basis>` của node này. Phương thức này đặt :ref:`scale<class_Node3D_property_scale>` của node này thành :ref:`Vector3.ONE<class_Vector3_constant_ONE>` (hoặc giá trị đối của nó), nhưng giữ nguyên :ref:`position<class_Node3D_property_position>` và :ref:`rotation<class_Node3D_property_rotation>`. Xem thêm :ref:`Transform3D.orthonormalized()<class_Transform3D_method_orthonormalized>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_rotate:

.. rst-class:: classref-method

|void| **rotate**\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node3D_method_rotate>`

Xoay :ref:`basis<class_Node3D_property_basis>` của node này quanh ``axis`` theo ``angle`` đã cho, tính bằng radian. Thao tác này được tính trong không gian của parent (tương đối với parent) và giữ nguyên :ref:`position<class_Node3D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_rotate_object_local:

.. rst-class:: classref-method

|void| **rotate_object_local**\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node3D_method_rotate_object_local>`

Xoay :ref:`basis<class_Node3D_property_basis>` của node này quanh ``axis`` theo ``angle`` đã cho, tính bằng radian. Thao tác này được tính trong không gian cục bộ (tương đối với node này) và giữ nguyên :ref:`position<class_Node3D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_rotate_x:

.. rst-class:: classref-method

|void| **rotate_x**\ (\ angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node3D_method_rotate_x>`

Xoay :ref:`basis<class_Node3D_property_basis>` của node này quanh trục X theo ``angle`` đã cho, tính bằng radian. Thao tác này được tính trong không gian của parent (tương đối với parent) và giữ nguyên :ref:`position<class_Node3D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_rotate_y:

.. rst-class:: classref-method

|void| **rotate_y**\ (\ angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node3D_method_rotate_y>`

Xoay :ref:`basis<class_Node3D_property_basis>` của node này quanh trục Y theo ``angle`` đã cho, tính bằng radian. Thao tác này được tính trong không gian của parent (tương đối với parent) và giữ nguyên :ref:`position<class_Node3D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_rotate_z:

.. rst-class:: classref-method

|void| **rotate_z**\ (\ angle\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node3D_method_rotate_z>`

Xoay :ref:`basis<class_Node3D_property_basis>` của node này quanh trục Z theo ``angle`` đã cho, tính bằng radian. Thao tác này được tính trong không gian của parent (tương đối với parent) và giữ nguyên :ref:`position<class_Node3D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_scale_object_local:

.. rst-class:: classref-method

|void| **scale_object_local**\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Node3D_method_scale_object_local>`

Scale :ref:`basis<class_Node3D_property_basis>` của node này theo hệ số ``scale`` đã cho. Thao tác này được tính trong không gian cục bộ (tương đối với node này) và giữ nguyên :ref:`position<class_Node3D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_set_disable_scale:

.. rst-class:: classref-method

|void| **set_disable_scale**\ (\ disable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node3D_method_set_disable_scale>`

Nếu ``true``, :ref:`global_transform<class_Node3D_property_global_transform>` của node này sẽ được tự động chuẩn hóa trực giao. Điều này khiến node không bị biến dạng, như thể scale toàn cục của nó được đặt thành :ref:`Vector3.ONE<class_Vector3_constant_ONE>` (hoặc giá trị đối của nó). Xem thêm :ref:`is_scale_disabled()<class_Node3D_method_is_scale_disabled>` và :ref:`orthonormalize()<class_Node3D_method_orthonormalize>`.

\ **Lưu ý:** :ref:`transform<class_Node3D_property_transform>` không bị ảnh hưởng bởi thiết lập này.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_set_identity:

.. rst-class:: classref-method

|void| **set_identity**\ (\ ) :ref:`🔗<class_Node3D_method_set_identity>`

Đặt :ref:`transform<class_Node3D_property_transform>` của node này thành :ref:`Transform3D.IDENTITY<class_Transform3D_constant_IDENTITY>`, thao tác này đặt lại mọi phép biến đổi trong không gian của parent (:ref:`position<class_Node3D_property_position>`, :ref:`rotation<class_Node3D_property_rotation>` và :ref:`scale<class_Node3D_property_scale>`).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_set_ignore_transform_notification:

.. rst-class:: classref-method

|void| **set_ignore_transform_notification**\ (\ enabled\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node3D_method_set_ignore_transform_notification>`

Nếu ``true``, node sẽ không nhận :ref:`NOTIFICATION_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_TRANSFORM_CHANGED>` hoặc :ref:`NOTIFICATION_LOCAL_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_LOCAL_TRANSFORM_CHANGED>`.

Có thể hữu ích khi gọi phương thức này trong lúc xử lý các notification này để ngăn đệ quy vô hạn.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_set_notify_local_transform:

.. rst-class:: classref-method

|void| **set_notify_local_transform**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node3D_method_set_notify_local_transform>`

Nếu ``true``, node sẽ nhận :ref:`NOTIFICATION_LOCAL_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_LOCAL_TRANSFORM_CHANGED>` mỗi khi :ref:`transform<class_Node3D_property_transform>` thay đổi.

\ **Lưu ý:** Một số node 3D như :ref:`CSGShape3D<class_CSGShape3D>` hoặc :ref:`CollisionShape3D<class_CollisionShape3D>` tự động bật tùy chọn này để hoạt động chính xác.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_set_notify_transform:

.. rst-class:: classref-method

|void| **set_notify_transform**\ (\ enable\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_Node3D_method_set_notify_transform>`

Nếu ``true``, node sẽ nhận :ref:`NOTIFICATION_TRANSFORM_CHANGED<class_Node3D_constant_NOTIFICATION_TRANSFORM_CHANGED>` mỗi khi :ref:`global_transform<class_Node3D_property_global_transform>` thay đổi.

\ **Lưu ý:** Hầu hết node 3D như :ref:`VisualInstance3D<class_VisualInstance3D>` hoặc :ref:`CollisionObject3D<class_CollisionObject3D>` tự động bật tùy chọn này để hoạt động chính xác.

\ **Lưu ý:** Trong editor, các node sẽ truyền notification này đến các node con nếu một gizmo được gắn vào (xem :ref:`add_gizmo()<class_Node3D_method_add_gizmo>`).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_set_subgizmo_selection:

.. rst-class:: classref-method

|void| **set_subgizmo_selection**\ (\ gizmo\: :ref:`Node3DGizmo<class_Node3DGizmo>`, id\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_Node3D_method_set_subgizmo_selection>`

Chọn subgizmo của ``gizmo`` với ``id`` đã cho và đặt transform của nó. Chỉ hoạt động trong editor.

\ **Lưu ý:** Đối tượng gizmo thường sẽ là một instance của :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>`, nhưng kiểu đối số được giữ ở dạng tổng quát để tránh tạo dependency vào các class của editor trong **Node3D**.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_show:

.. rst-class:: classref-method

|void| **show**\ (\ ) :ref:`🔗<class_Node3D_method_show>`

Cho phép render node này. Tương đương với việc đặt :ref:`visible<class_Node3D_property_visible>` thành ``true``. Đây là thao tác ngược với :ref:`hide()<class_Node3D_method_hide>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_to_global:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **to_global**\ (\ local_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Node3D_method_to_global>`

Trả về ``local_point`` được chuyển đổi từ không gian cục bộ của node này sang không gian toàn cục. Đây là thao tác ngược với :ref:`to_local()<class_Node3D_method_to_local>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_to_local:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **to_local**\ (\ global_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Node3D_method_to_local>`

Trả về ``global_point`` được chuyển đổi từ không gian toàn cục sang không gian cục bộ của node này. Đây là thao tác ngược với :ref:`to_global()<class_Node3D_method_to_global>`.

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_translate:

.. rst-class:: classref-method

|void| **translate**\ (\ offset\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Node3D_method_translate>`

Cộng translation ``offset`` đã cho vào vị trí của node, trong không gian cục bộ (tương đối với node này).

\ **Lưu ý:** Thay vào đó, nên sử dụng :ref:`translate_object_local()<class_Node3D_method_translate_object_local>`, vì phương thức này có thể bị thay đổi trong bản phát hành tương lai.

\ **Lưu ý:** Mặc dù theo quy ước đặt tên, thao tác này **không** được tính trong không gian cha vì lý do tương thích. Để dịch chuyển trong không gian cha, hãy thêm ``offset`` vào :ref:`position<class_Node3D_property_position>` (``node_3d.position += offset``).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_translate_object_local:

.. rst-class:: classref-method

|void| **translate_object_local**\ (\ offset\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Node3D_method_translate_object_local>`

Thêm phép dịch chuyển ``offset`` đã cho vào vị trí của node, trong không gian cục bộ (tương đối so với node này).

.. rst-class:: classref-item-separator

----

.. _class_Node3D_method_update_gizmos:

.. rst-class:: classref-method

|void| **update_gizmos**\ (\ ) :ref:`🔗<class_Node3D_method_update_gizmos>`

Cập nhật tất cả các đối tượng :ref:`EditorNode3DGizmo<class_EditorNode3DGizmo>` được gắn vào node này. Chỉ hoạt động trong editor.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
