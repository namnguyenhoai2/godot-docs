:github_url: hide

.. meta::
	:keywords: ragdoll

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicalBone3D.xml.

.. _class_PhysicalBone3D:

PhysicalBone3D
==============

**Kế thừa:** :ref:`PhysicsBody3D<class_PhysicsBody3D>` **<** :ref:`CollisionObject3D<class_CollisionObject3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một physics body được dùng để khiến các bone trong :ref:`Skeleton3D<class_Skeleton3D>` phản ứng với physics.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node **PhysicalBone3D** là một physics body có thể được dùng để khiến các bone trong :ref:`Skeleton3D<class_Skeleton3D>` phản ứng với physics.

\ **Lưu ý:** Để phát hiện các physical bone bằng raycast, thuộc tính :ref:`SkeletonModifier3D.active<class_SkeletonModifier3D_property_active>` của :ref:`PhysicalBoneSimulator3D<class_PhysicalBoneSimulator3D>` cha phải là ``true`` và bone của :ref:`Skeleton3D<class_Skeleton3D>` phải được gán đúng cho **PhysicalBone3D**; điều này có nghĩa là :ref:`get_bone_id()<class_PhysicalBone3D_method_get_bone_id>` phải trả về một id hợp lệ (``>= 0``).

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Hệ thống Ragdoll <../tutorials/physics/ragdoll_system>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`angular_damp<class_PhysicalBone3D_property_angular_damp>`           | ``0.0``                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`DampMode<enum_PhysicalBone3D_DampMode>`   | :ref:`angular_damp_mode<class_PhysicalBone3D_property_angular_damp_mode>` | ``0``                                               |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`angular_velocity<class_PhysicalBone3D_property_angular_velocity>`   | ``Vector3(0, 0, 0)``                                |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`           | :ref:`body_offset<class_PhysicalBone3D_property_body_offset>`             | ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`bounce<class_PhysicalBone3D_property_bounce>`                       | ``0.0``                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`can_sleep<class_PhysicalBone3D_property_can_sleep>`                 | ``true``                                            |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`custom_integrator<class_PhysicalBone3D_property_custom_integrator>` | ``false``                                           |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`friction<class_PhysicalBone3D_property_friction>`                   | ``1.0``                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`gravity_scale<class_PhysicalBone3D_property_gravity_scale>`         | ``1.0``                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`           | :ref:`joint_offset<class_PhysicalBone3D_property_joint_offset>`           | ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`joint_rotation<class_PhysicalBone3D_property_joint_rotation>`       | ``Vector3(0, 0, 0)``                                |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`JointType<enum_PhysicalBone3D_JointType>` | :ref:`joint_type<class_PhysicalBone3D_property_joint_type>`               | ``0``                                               |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`linear_damp<class_PhysicalBone3D_property_linear_damp>`             | ``0.0``                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`DampMode<enum_PhysicalBone3D_DampMode>`   | :ref:`linear_damp_mode<class_PhysicalBone3D_property_linear_damp_mode>`   | ``0``                                               |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                   | :ref:`linear_velocity<class_PhysicalBone3D_property_linear_velocity>`     | ``Vector3(0, 0, 0)``                                |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+
   | :ref:`float<class_float>`                       | :ref:`mass<class_PhysicalBone3D_property_mass>`                           | ``1.0``                                             |
   +-------------------------------------------------+---------------------------------------------------------------------------+-----------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`_integrate_forces<class_PhysicalBone3D_private_method__integrate_forces>`\ (\ state\: :ref:`PhysicsDirectBodyState3D<class_PhysicsDirectBodyState3D>`\ ) |virtual|    |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`apply_central_impulse<class_PhysicalBone3D_method_apply_central_impulse>`\ (\ impulse\: :ref:`Vector3<class_Vector3>`\ )                                              |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`apply_impulse<class_PhysicalBone3D_method_apply_impulse>`\ (\ impulse\: :ref:`Vector3<class_Vector3>`, position\: :ref:`Vector3<class_Vector3>` = Vector3(0, 0, 0)\ ) |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`   | :ref:`get_bone_id<class_PhysicalBone3D_method_get_bone_id>`\ (\ ) |const|                                                                                                   |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_simulate_physics<class_PhysicalBone3D_method_get_simulate_physics>`\ (\ )                                                                                         |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_simulating_physics<class_PhysicalBone3D_method_is_simulating_physics>`\ (\ )                                                                                       |
   +-------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_PhysicalBone3D_DampMode:

.. rst-class:: classref-enumeration

enum **DampMode**: :ref:`🔗<enum_PhysicalBone3D_DampMode>`

.. _class_PhysicalBone3D_constant_DAMP_MODE_COMBINE:

.. rst-class:: classref-enumeration-constant

:ref:`DampMode<enum_PhysicalBone3D_DampMode>` **DAMP_MODE_COMBINE** = ``0``

Ở chế độ này, giá trị damping của body được cộng vào mọi giá trị được đặt trong các area hoặc giá trị mặc định.

.. _class_PhysicalBone3D_constant_DAMP_MODE_REPLACE:

.. rst-class:: classref-enumeration-constant

:ref:`DampMode<enum_PhysicalBone3D_DampMode>` **DAMP_MODE_REPLACE** = ``1``

Ở chế độ này, giá trị damping của body thay thế mọi giá trị được đặt trong các area hoặc giá trị mặc định.

.. rst-class:: classref-item-separator

----

.. _enum_PhysicalBone3D_JointType:

.. rst-class:: classref-enumeration

enum **JointType**: :ref:`🔗<enum_PhysicalBone3D_JointType>`

.. _class_PhysicalBone3D_constant_JOINT_TYPE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`JointType<enum_PhysicalBone3D_JointType>` **JOINT_TYPE_NONE** = ``0``

Không áp dụng joint nào cho PhysicsBone3D.

.. _class_PhysicalBone3D_constant_JOINT_TYPE_PIN:

.. rst-class:: classref-enumeration-constant

:ref:`JointType<enum_PhysicalBone3D_JointType>` **JOINT_TYPE_PIN** = ``1``

Một pin joint được áp dụng cho PhysicsBone3D.

.. _class_PhysicalBone3D_constant_JOINT_TYPE_CONE:

.. rst-class:: classref-enumeration-constant

:ref:`JointType<enum_PhysicalBone3D_JointType>` **JOINT_TYPE_CONE** = ``2``

Một cone joint được áp dụng cho PhysicsBone3D.

.. _class_PhysicalBone3D_constant_JOINT_TYPE_HINGE:

.. rst-class:: classref-enumeration-constant

:ref:`JointType<enum_PhysicalBone3D_JointType>` **JOINT_TYPE_HINGE** = ``3``

Một hinge joint được áp dụng cho PhysicsBone3D.

.. _class_PhysicalBone3D_constant_JOINT_TYPE_SLIDER:

.. rst-class:: classref-enumeration-constant

:ref:`JointType<enum_PhysicalBone3D_JointType>` **JOINT_TYPE_SLIDER** = ``4``

Một slider joint được áp dụng cho PhysicsBone3D.

.. _class_PhysicalBone3D_constant_JOINT_TYPE_6DOF:

.. rst-class:: classref-enumeration-constant

:ref:`JointType<enum_PhysicalBone3D_JointType>` **JOINT_TYPE_6DOF** = ``5``

Một joint có 6 bậc tự do được áp dụng cho PhysicsBone3D.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicalBone3D_property_angular_damp:

.. rst-class:: classref-property

:ref:`float<class_float>` **angular_damp** = ``0.0`` :ref:`🔗<class_PhysicalBone3D_property_angular_damp>`

.. rst-class:: classref-property-setget

- |void| **set_angular_damp**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_angular_damp**\ (\ )

Giảm tốc chuyển động xoay của body. Theo mặc định, body sẽ sử dụng thiết lập project :ref:`ProjectSettings.physics/3d/default_angular_damp<class_ProjectSettings_property_physics/3d/default_angular_damp>` hoặc bất kỳ giá trị ghi đè nào được đặt bởi một :ref:`Area3D<class_Area3D>` mà body đang ở trong đó. Tùy thuộc vào :ref:`angular_damp_mode<class_PhysicalBone3D_property_angular_damp_mode>`, bạn có thể đặt :ref:`angular_damp<class_PhysicalBone3D_property_angular_damp>` để được cộng vào hoặc thay thế giá trị damping của body.

Xem :ref:`ProjectSettings.physics/3d/default_angular_damp<class_ProjectSettings_property_physics/3d/default_angular_damp>` để biết thêm chi tiết về damping.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_angular_damp_mode:

.. rst-class:: classref-property

:ref:`DampMode<enum_PhysicalBone3D_DampMode>` **angular_damp_mode** = ``0`` :ref:`🔗<class_PhysicalBone3D_property_angular_damp_mode>`

.. rst-class:: classref-property-setget

- |void| **set_angular_damp_mode**\ (\ value\: :ref:`DampMode<enum_PhysicalBone3D_DampMode>`\ ) - :ref:`DampMode<enum_PhysicalBone3D_DampMode>` **get_angular_damp_mode**\ (\ )

Xác định cách áp dụng :ref:`angular_damp<class_PhysicalBone3D_property_angular_damp>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_angular_velocity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **angular_velocity** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_PhysicalBone3D_property_angular_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_angular_velocity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_angular_velocity**\ (\ )

Vận tốc xoay của PhysicalBone3D tính theo *radian* trên giây.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_body_offset:

.. rst-class:: classref-property

:ref:`Transform3D<class_Transform3D>` **body_offset** = ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` :ref:`🔗<class_PhysicalBone3D_property_body_offset>`

.. rst-class:: classref-property-setget

- |void| **set_body_offset**\ (\ value\: :ref:`Transform3D<class_Transform3D>`\ ) - :ref:`Transform3D<class_Transform3D>` **get_body_offset**\ (\ )

Đặt transform của body.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_bounce:

.. rst-class:: classref-property

:ref:`float<class_float>` **bounce** = ``0.0`` :ref:`🔗<class_PhysicalBone3D_property_bounce>`

.. rst-class:: classref-property-setget

- |void| **set_bounce**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bounce**\ (\ )

Độ nảy của body. Các giá trị nằm trong khoảng từ ``0`` (không nảy) đến ``1`` (độ nảy tối đa).

\ **Lưu ý:** Ngay cả khi :ref:`bounce<class_PhysicalBone3D_property_bounce>` được đặt thành ``1.0``, một phần năng lượng vẫn sẽ mất dần theo thời gian do damping tuyến tính và damping góc. Để một **PhysicalBone3D** bảo toàn toàn bộ năng lượng theo thời gian, hãy đặt :ref:`bounce<class_PhysicalBone3D_property_bounce>` thành ``1.0``, :ref:`linear_damp_mode<class_PhysicalBone3D_property_linear_damp_mode>` thành :ref:`DAMP_MODE_REPLACE<class_PhysicalBone3D_constant_DAMP_MODE_REPLACE>`, :ref:`linear_damp<class_PhysicalBone3D_property_linear_damp>` thành ``0.0``, :ref:`angular_damp_mode<class_PhysicalBone3D_property_angular_damp_mode>` thành :ref:`DAMP_MODE_REPLACE<class_PhysicalBone3D_constant_DAMP_MODE_REPLACE>`, và :ref:`angular_damp<class_PhysicalBone3D_property_angular_damp>` thành ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_can_sleep:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **can_sleep** = ``true`` :ref:`🔗<class_PhysicalBone3D_property_can_sleep>`

.. rst-class:: classref-property-setget

- |void| **set_can_sleep**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_able_to_sleep**\ (\ )

Nếu ``true``, body sẽ bị vô hiệu hóa khi không có chuyển động, nên nó sẽ không tham gia mô phỏng cho đến khi được đánh thức bởi một lực bên ngoài.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_custom_integrator:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **custom_integrator** = ``false`` :ref:`🔗<class_PhysicalBone3D_property_custom_integrator>`

.. rst-class:: classref-property-setget

- |void| **set_use_custom_integrator**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_custom_integrator**\ (\ )

Nếu ``true``, việc tích hợp lực tiêu chuẩn (chẳng hạn như gravity hoặc damping) sẽ bị vô hiệu hóa đối với body này. Ngoài phản hồi va chạm, body sẽ chỉ di chuyển theo như được xác định bởi phương thức :ref:`_integrate_forces()<class_PhysicalBone3D_private_method__integrate_forces>`, nếu phương thức ảo đó được override.

Việc đặt thuộc tính này sẽ gọi phương thức :ref:`PhysicsServer3D.body_set_omit_force_integration()<class_PhysicsServer3D_method_body_set_omit_force_integration>` ở bên trong.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_friction:

.. rst-class:: classref-property

:ref:`float<class_float>` **friction** = ``1.0`` :ref:`🔗<class_PhysicalBone3D_property_friction>`

.. rst-class:: classref-property-setget

- |void| **set_friction**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_friction**\ (\ )

Độ ma sát của body, từ ``0`` (không ma sát) đến ``1`` (ma sát tối đa).

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_gravity_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **gravity_scale** = ``1.0`` :ref:`🔗<class_PhysicalBone3D_property_gravity_scale>`

.. rst-class:: classref-property-setget

- |void| **set_gravity_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gravity_scale**\ (\ )

Giá trị này được nhân với :ref:`ProjectSettings.physics/3d/default_gravity<class_ProjectSettings_property_physics/3d/default_gravity>` để tạo ra gravity cho body này. Ví dụ, giá trị ``1.0`` sẽ áp dụng gravity bình thường, ``2.0`` sẽ áp dụng gravity gấp đôi, còn ``0.5`` sẽ áp dụng gravity bằng một nửa cho body này.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_joint_offset:

.. rst-class:: classref-property

:ref:`Transform3D<class_Transform3D>` **joint_offset** = ``Transform3D(1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0)`` :ref:`🔗<class_PhysicalBone3D_property_joint_offset>`

.. rst-class:: classref-property-setget

- |void| **set_joint_offset**\ (\ value\: :ref:`Transform3D<class_Transform3D>`\ ) - :ref:`Transform3D<class_Transform3D>` **get_joint_offset**\ (\ )

Đặt transform của joint.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_joint_rotation:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **joint_rotation** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_PhysicalBone3D_property_joint_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_joint_rotation**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_joint_rotation**\ (\ )

Đặt rotation của joint theo radian.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_joint_type:

.. rst-class:: classref-property

:ref:`JointType<enum_PhysicalBone3D_JointType>` **joint_type** = ``0`` :ref:`🔗<class_PhysicalBone3D_property_joint_type>`

.. rst-class:: classref-property-setget

- |void| **set_joint_type**\ (\ value\: :ref:`JointType<enum_PhysicalBone3D_JointType>`\ ) - :ref:`JointType<enum_PhysicalBone3D_JointType>` **get_joint_type**\ (\ )

Đặt loại joint.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_linear_damp:

.. rst-class:: classref-property

:ref:`float<class_float>` **linear_damp** = ``0.0`` :ref:`🔗<class_PhysicalBone3D_property_linear_damp>`

.. rst-class:: classref-property-setget

- |void| **set_linear_damp**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_linear_damp**\ (\ )

Giảm tốc chuyển động của body. Theo mặc định, body sẽ sử dụng :ref:`ProjectSettings.physics/3d/default_linear_damp<class_ProjectSettings_property_physics/3d/default_linear_damp>` hoặc bất kỳ giá trị ghi đè nào được đặt bởi một :ref:`Area3D<class_Area3D>` mà body đang ở trong đó. Tùy thuộc vào :ref:`linear_damp_mode<class_PhysicalBone3D_property_linear_damp_mode>`, :ref:`linear_damp<class_PhysicalBone3D_property_linear_damp>` có thể được cộng vào hoặc thay thế giá trị damping của body.

Xem :ref:`ProjectSettings.physics/3d/default_linear_damp<class_ProjectSettings_property_physics/3d/default_linear_damp>` để biết thêm chi tiết về damping.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_linear_damp_mode:

.. rst-class:: classref-property

:ref:`DampMode<enum_PhysicalBone3D_DampMode>` **linear_damp_mode** = ``0`` :ref:`🔗<class_PhysicalBone3D_property_linear_damp_mode>`

.. rst-class:: classref-property-setget

- |void| **set_linear_damp_mode**\ (\ value\: :ref:`DampMode<enum_PhysicalBone3D_DampMode>`\ ) - :ref:`DampMode<enum_PhysicalBone3D_DampMode>` **get_linear_damp_mode**\ (\ )

Xác định cách áp dụng :ref:`linear_damp<class_PhysicalBone3D_property_linear_damp>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_linear_velocity:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **linear_velocity** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_PhysicalBone3D_property_linear_velocity>`

.. rst-class:: classref-property-setget

- |void| **set_linear_velocity**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_linear_velocity**\ (\ )

Vận tốc tuyến tính của body tính theo đơn vị trên giây. Có thể sử dụng không thường xuyên, nhưng **đừng đặt giá trị này ở mỗi frame**, vì physics có thể chạy trong một thread khác và chạy với độ chi tiết khác. Hãy sử dụng :ref:`_integrate_forces()<class_PhysicalBone3D_private_method__integrate_forces>` làm process loop để kiểm soát chính xác trạng thái của body.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_property_mass:

.. rst-class:: classref-property

:ref:`float<class_float>` **mass** = ``1.0`` :ref:`🔗<class_PhysicalBone3D_property_mass>`

.. rst-class:: classref-property-setget

- |void| **set_mass**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_mass**\ (\ )

Khối lượng của body.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicalBone3D_private_method__integrate_forces:

.. rst-class:: classref-method

|void| **_integrate_forces**\ (\ state\: :ref:`PhysicsDirectBodyState3D<class_PhysicsDirectBodyState3D>`\ ) |virtual| :ref:`🔗<class_PhysicalBone3D_private_method__integrate_forces>`

Được gọi trong quá trình xử lý physics, cho phép bạn đọc và sửa đổi an toàn trạng thái mô phỏng của object. Theo mặc định, phương thức này được gọi trước khi tích hợp lực tiêu chuẩn, nhưng thuộc tính :ref:`custom_integrator<class_PhysicalBone3D_property_custom_integrator>` cho phép bạn vô hiệu hóa việc tích hợp lực tiêu chuẩn và thực hiện tích hợp lực hoàn toàn tùy chỉnh cho một body.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_method_apply_central_impulse:

.. rst-class:: classref-method

|void| **apply_central_impulse**\ (\ impulse\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_PhysicalBone3D_method_apply_central_impulse>`

Áp dụng một impulse theo hướng mà không ảnh hưởng đến chuyển động quay.

Impulse độc lập với thời gian! Việc áp dụng impulse trong mỗi frame sẽ tạo ra một lực phụ thuộc vào framerate. Vì lý do này, chỉ nên sử dụng nó khi mô phỏng các va chạm xảy ra một lần (nếu không, hãy sử dụng các hàm "_integrate_forces").

Điều này tương đương với việc sử dụng :ref:`apply_impulse()<class_PhysicalBone3D_method_apply_impulse>` tại tâm khối lượng của body.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_method_apply_impulse:

.. rst-class:: classref-method

|void| **apply_impulse**\ (\ impulse\: :ref:`Vector3<class_Vector3>`, position\: :ref:`Vector3<class_Vector3>` = Vector3(0, 0, 0)\ ) :ref:`🔗<class_PhysicalBone3D_method_apply_impulse>`

Áp dụng một impulse tại vị trí cho PhysicsBone3D.

Impulse độc lập với thời gian! Việc áp dụng impulse trong mỗi frame sẽ tạo ra một lực phụ thuộc vào framerate. Vì lý do này, chỉ nên sử dụng nó khi mô phỏng các va chạm xảy ra một lần (nếu không, hãy sử dụng các hàm "_integrate_forces").

\ ``position`` là độ lệch từ gốc tọa độ của PhysicsBone3D trong hệ tọa độ toàn cục.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_method_get_bone_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_bone_id**\ (\ ) |const| :ref:`🔗<class_PhysicalBone3D_method_get_bone_id>`

Trả về mã định danh duy nhất của PhysicsBone3D.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_method_get_simulate_physics:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_simulate_physics**\ (\ ) :ref:`🔗<class_PhysicalBone3D_method_get_simulate_physics>`

Trả về ``true`` nếu PhysicsBone3D được phép mô phỏng vật lý.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone3D_method_is_simulating_physics:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_simulating_physics**\ (\ ) :ref:`🔗<class_PhysicalBone3D_method_is_simulating_physics>`

Trả về ``true`` nếu PhysicsBone3D hiện đang mô phỏng vật lý.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
