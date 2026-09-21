:github_url: hide

.. meta::
	:keywords: ragdoll

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicalBone2D.xml.

.. _class_PhysicalBone2D:

PhysicalBone2D
==============

**Kế thừa:** :ref:`RigidBody2D<class_RigidBody2D>` **<** :ref:`PhysicsBody2D<class_PhysicsBody2D>` **<** :ref:`CollisionObject2D<class_CollisionObject2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node bắt nguồn từ :ref:`RigidBody2D<class_RigidBody2D>`, được dùng để khiến :ref:`Bone2D<class_Bone2D>`\ s trong một :ref:`Skeleton2D<class_Skeleton2D>` phản ứng với physics.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node **PhysicalBone2D** là một node dựa trên :ref:`RigidBody2D<class_RigidBody2D>`, có thể được dùng để khiến :ref:`Bone2D<class_Bone2D>`\ s trong một :ref:`Skeleton2D<class_Skeleton2D>` phản ứng với physics.

\ **Lưu ý:** Để khiến :ref:`Bone2D<class_Bone2D>`\ s hiển thị chuyển động theo node **PhysicalBone2D**, hãy sử dụng một phép sửa đổi :ref:`SkeletonModification2DPhysicalBones<class_SkeletonModification2DPhysicalBones>` trên node cha :ref:`Skeleton2D<class_Skeleton2D>`.

\ **Lưu ý:** Node **PhysicalBone2D** không tự động tạo một node :ref:`Joint2D<class_Joint2D>` để giữ các node **PhysicalBone2D** cùng nhau. Bạn phải tự tạo chúng. Trong hầu hết trường hợp, bạn nên sử dụng một node :ref:`PinJoint2D<class_PinJoint2D>`. Node **PhysicalBone2D** sẽ tự động cấu hình node :ref:`Joint2D<class_Joint2D>` sau khi node này được thêm làm node con.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+-----------------------------------------------------------------------------------------------+------------------+
   | :ref:`bool<class_bool>`         | :ref:`auto_configure_joint<class_PhysicalBone2D_property_auto_configure_joint>`               | ``true``         |
   +---------------------------------+-----------------------------------------------------------------------------------------------+------------------+
   | :ref:`int<class_int>`           | :ref:`bone2d_index<class_PhysicalBone2D_property_bone2d_index>`                               | ``-1``           |
   +---------------------------------+-----------------------------------------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>` | :ref:`bone2d_nodepath<class_PhysicalBone2D_property_bone2d_nodepath>`                         | ``NodePath("")`` |
   +---------------------------------+-----------------------------------------------------------------------------------------------+------------------+
   | :ref:`bool<class_bool>`         | :ref:`follow_bone_when_simulating<class_PhysicalBone2D_property_follow_bone_when_simulating>` | ``false``        |
   +---------------------------------+-----------------------------------------------------------------------------------------------+------------------+
   | :ref:`bool<class_bool>`         | :ref:`simulate_physics<class_PhysicalBone2D_property_simulate_physics>`                       | ``false``        |
   +---------------------------------+-----------------------------------------------------------------------------------------------+------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`Joint2D<class_Joint2D>` | :ref:`get_joint<class_PhysicalBone2D_method_get_joint>`\ (\ ) |const|                         |
   +-------------------------------+-----------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`is_simulating_physics<class_PhysicalBone2D_method_is_simulating_physics>`\ (\ ) |const| |
   +-------------------------------+-----------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PhysicalBone2D_property_auto_configure_joint:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **auto_configure_joint** = ``true`` :ref:`🔗<class_PhysicalBone2D_property_auto_configure_joint>`

.. rst-class:: classref-property-setget

- |void| **set_auto_configure_joint**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_auto_configure_joint**\ (\ )

Nếu ``true``, **PhysicalBone2D** sẽ tự động cấu hình node con :ref:`Joint2D<class_Joint2D>` đầu tiên. Việc cấu hình tự động chỉ giới hạn ở thiết lập các thuộc tính của node và định vị :ref:`Joint2D<class_Joint2D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone2D_property_bone2d_index:

.. rst-class:: classref-property

:ref:`int<class_int>` **bone2d_index** = ``-1`` :ref:`🔗<class_PhysicalBone2D_property_bone2d_index>`

.. rst-class:: classref-property-setget

- |void| **set_bone2d_index**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bone2d_index**\ (\ )

Chỉ mục của :ref:`Bone2D<class_Bone2D>` mà **PhysicalBone2D** này sẽ mô phỏng.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone2D_property_bone2d_nodepath:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **bone2d_nodepath** = ``NodePath("")`` :ref:`🔗<class_PhysicalBone2D_property_bone2d_nodepath>`

.. rst-class:: classref-property-setget

- |void| **set_bone2d_nodepath**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_bone2d_nodepath**\ (\ )

:ref:`NodePath<class_NodePath>` đến :ref:`Bone2D<class_Bone2D>` mà **PhysicalBone2D** này sẽ mô phỏng.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone2D_property_follow_bone_when_simulating:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **follow_bone_when_simulating** = ``false`` :ref:`🔗<class_PhysicalBone2D_property_follow_bone_when_simulating>`

.. rst-class:: classref-property-setget

- |void| **set_follow_bone_when_simulating**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_follow_bone_when_simulating**\ (\ )

Nếu ``true``, **PhysicalBone2D** sẽ giữ transform của bone mà nó liên kết trong khi mô phỏng physics.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone2D_property_simulate_physics:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **simulate_physics** = ``false`` :ref:`🔗<class_PhysicalBone2D_property_simulate_physics>`

.. rst-class:: classref-property-setget

- |void| **set_simulate_physics**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_simulate_physics**\ (\ )

Nếu ``true``, **PhysicalBone2D** sẽ bắt đầu mô phỏng bằng physics. Nếu ``false``, node **PhysicalBone2D** sẽ theo transform của node :ref:`Bone2D<class_Bone2D>`.

\ **Lưu ý:** Để khiến :ref:`Bone2D<class_Bone2D>`\ s hiển thị chuyển động theo **PhysicalBone2D**, hãy sử dụng một phép sửa đổi :ref:`SkeletonModification2DPhysicalBones<class_SkeletonModification2DPhysicalBones>` trên node :ref:`Skeleton2D<class_Skeleton2D>` cùng với các node :ref:`Bone2D<class_Bone2D>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicalBone2D_method_get_joint:

.. rst-class:: classref-method

:ref:`Joint2D<class_Joint2D>` **get_joint**\ (\ ) |const| :ref:`🔗<class_PhysicalBone2D_method_get_joint>`

Trả về node con :ref:`Joint2D<class_Joint2D>` đầu tiên, nếu tồn tại. Đây chủ yếu là một hàm hỗ trợ giúp dễ lấy :ref:`Joint2D<class_Joint2D>` mà **PhysicalBone2D** đang tự động cấu hình.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBone2D_method_is_simulating_physics:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_simulating_physics**\ (\ ) |const| :ref:`🔗<class_PhysicalBone2D_method_is_simulating_physics>`

Trả về một boolean cho biết liệu **PhysicalBone2D** có đang chạy và mô phỏng bằng engine physics 2D của Godot hay không. Khi ``true``, node PhysicalBone2D đang sử dụng physics.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
