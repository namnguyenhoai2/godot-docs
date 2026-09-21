:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRHand.xml.

.. _class_OpenXRHand:

OpenXRHand
==========

**Đã lỗi thời:** Thay vào đó, hãy sử dụng :ref:`XRHandModifier3D<class_XRHandModifier3D>`.

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node hỗ trợ tracking bàn tay và ngón tay trong OpenXR.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này bật chức năng tracking bàn tay của OpenXR. Node này phải là node con của một node :ref:`XROrigin3D<class_XROrigin3D>`; việc tracking sẽ cập nhật vị trí của node đến vị trí khớp Palm của bàn tay được tracking của người chơi (tâm của xương bàn ngón giữa). Node này cũng cập nhật skeleton của mô hình bàn tay hoặc avatar đã được skinning phù hợp.

Nếu skeleton là một bàn tay (một trong các xương bàn tay là node gốc của skeleton), thì skeleton sẽ được đặt tương đối so với vị trí lòng bàn tay, còn mesh bàn tay và skeleton phải là các node con của node OpenXRHand.

Nếu các xương bàn tay là một phần của skeleton hoàn chỉnh, thì gốc của bàn tay sẽ giữ nguyên vị trí, với giả định rằng IK được sử dụng để định vị bàn tay và cánh tay.

Theo mặc định, các xương bàn tay của skeleton được định vị lại để khớp với kích thước của bàn tay được tracking. Để giữ nguyên kích thước xương theo mô hình, hãy thay đổi :ref:`bone_update<class_OpenXRHand_property_bone_update>` để chỉ áp dụng rotation.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------------------+------------------+
   | :ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>`   | :ref:`bone_update<class_OpenXRHand_property_bone_update>`     | ``0``            |
   +-------------------------------------------------+---------------------------------------------------------------+------------------+
   | :ref:`Hands<enum_OpenXRHand_Hands>`             | :ref:`hand<class_OpenXRHand_property_hand>`                   | ``0``            |
   +-------------------------------------------------+---------------------------------------------------------------+------------------+
   | :ref:`NodePath<class_NodePath>`                 | :ref:`hand_skeleton<class_OpenXRHand_property_hand_skeleton>` | ``NodePath("")`` |
   +-------------------------------------------------+---------------------------------------------------------------+------------------+
   | :ref:`MotionRange<enum_OpenXRHand_MotionRange>` | :ref:`motion_range<class_OpenXRHand_property_motion_range>`   | ``0``            |
   +-------------------------------------------------+---------------------------------------------------------------+------------------+
   | :ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>` | :ref:`skeleton_rig<class_OpenXRHand_property_skeleton_rig>`   | ``0``            |
   +-------------------------------------------------+---------------------------------------------------------------+------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OpenXRHand_Hands:

.. rst-class:: classref-enumeration

enum **Hands**: :ref:`🔗<enum_OpenXRHand_Hands>`

.. _class_OpenXRHand_constant_HAND_LEFT:

.. rst-class:: classref-enumeration-constant

:ref:`Hands<enum_OpenXRHand_Hands>` **HAND_LEFT** = ``0``

Tracking bàn tay trái của người chơi.

.. _class_OpenXRHand_constant_HAND_RIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`Hands<enum_OpenXRHand_Hands>` **HAND_RIGHT** = ``1``

Tracking bàn tay phải của người chơi.

.. _class_OpenXRHand_constant_HAND_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Hands<enum_OpenXRHand_Hands>` **HAND_MAX** = ``2``

Số bàn tay được hỗ trợ tối đa.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRHand_MotionRange:

.. rst-class:: classref-enumeration

enum **MotionRange**: :ref:`🔗<enum_OpenXRHand_MotionRange>`

.. _class_OpenXRHand_constant_MOTION_RANGE_UNOBSTRUCTED:

.. rst-class:: classref-enumeration-constant

:ref:`MotionRange<enum_OpenXRHand_MotionRange>` **MOTION_RANGE_UNOBSTRUCTED** = ``0``

Khi người chơi nắm lại, skeleton bàn tay sẽ tạo thành nắm đấm hoàn chỉnh.

.. _class_OpenXRHand_constant_MOTION_RANGE_CONFORM_TO_CONTROLLER:

.. rst-class:: classref-enumeration-constant

:ref:`MotionRange<enum_OpenXRHand_MotionRange>` **MOTION_RANGE_CONFORM_TO_CONTROLLER** = ``1``

Khi người chơi nắm lại, skeleton bàn tay sẽ khớp với controller mà người chơi đang cầm.

.. _class_OpenXRHand_constant_MOTION_RANGE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`MotionRange<enum_OpenXRHand_MotionRange>` **MOTION_RANGE_MAX** = ``2``

Số phạm vi chuyển động được hỗ trợ tối đa.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRHand_SkeletonRig:

.. rst-class:: classref-enumeration

enum **SkeletonRig**: :ref:`🔗<enum_OpenXRHand_SkeletonRig>`

.. _class_OpenXRHand_constant_SKELETON_RIG_OPENXR:

.. rst-class:: classref-enumeration-constant

:ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>` **SKELETON_RIG_OPENXR** = ``0``

Một skeleton tuân thủ OpenXR.

.. _class_OpenXRHand_constant_SKELETON_RIG_HUMANOID:

.. rst-class:: classref-enumeration-constant

:ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>` **SKELETON_RIG_HUMANOID** = ``1``

Một skeleton tuân thủ :ref:`SkeletonProfileHumanoid<class_SkeletonProfileHumanoid>`.

.. _class_OpenXRHand_constant_SKELETON_RIG_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>` **SKELETON_RIG_MAX** = ``2``

Số bàn tay được hỗ trợ tối đa.

.. rst-class:: classref-item-separator

----

.. _enum_OpenXRHand_BoneUpdate:

.. rst-class:: classref-enumeration

enum **BoneUpdate**: :ref:`🔗<enum_OpenXRHand_BoneUpdate>`

.. _class_OpenXRHand_constant_BONE_UPDATE_FULL:

.. rst-class:: classref-enumeration-constant

:ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>` **BONE_UPDATE_FULL** = ``0``

Các xương của skeleton được cập nhật hoàn toàn (cả vị trí và rotation) để khớp với các xương được tracking.

.. _class_OpenXRHand_constant_BONE_UPDATE_ROTATION_ONLY:

.. rst-class:: classref-enumeration-constant

:ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>` **BONE_UPDATE_ROTATION_ONLY** = ``1``

Các xương của skeleton chỉ được xoay để căn chỉnh với các xương được tracking, giữ nguyên độ dài xương.

.. _class_OpenXRHand_constant_BONE_UPDATE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>` **BONE_UPDATE_MAX** = ``2``

Chế độ cập nhật xương được hỗ trợ tối đa.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRHand_property_bone_update:

.. rst-class:: classref-property

:ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>` **bone_update** = ``0`` :ref:`🔗<class_OpenXRHand_property_bone_update>`

.. rst-class:: classref-property-setget

- |void| **set_bone_update**\ (\ value\: :ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>`\ ) - :ref:`BoneUpdate<enum_OpenXRHand_BoneUpdate>` **get_bone_update**\ (\ )

Chỉ định loại cập nhật cần thực hiện trên xương.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRHand_property_hand:

.. rst-class:: classref-property

:ref:`Hands<enum_OpenXRHand_Hands>` **hand** = ``0`` :ref:`🔗<class_OpenXRHand_property_hand>`

.. rst-class:: classref-property-setget

- |void| **set_hand**\ (\ value\: :ref:`Hands<enum_OpenXRHand_Hands>`\ ) - :ref:`Hands<enum_OpenXRHand_Hands>` **get_hand**\ (\ )

Chỉ định node này tracking bàn tay trái hay phải của người chơi.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRHand_property_hand_skeleton:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **hand_skeleton** = ``NodePath("")`` :ref:`🔗<class_OpenXRHand_property_hand_skeleton>`

.. rst-class:: classref-property-setget

- |void| **set_hand_skeleton**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_hand_skeleton**\ (\ )

Đặt một node :ref:`Skeleton3D<class_Skeleton3D>` để cập nhật các vị trí pose.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRHand_property_motion_range:

.. rst-class:: classref-property

:ref:`MotionRange<enum_OpenXRHand_MotionRange>` **motion_range** = ``0`` :ref:`🔗<class_OpenXRHand_property_motion_range>`

.. rst-class:: classref-property-setget

- |void| **set_motion_range**\ (\ value\: :ref:`MotionRange<enum_OpenXRHand_MotionRange>`\ ) - :ref:`MotionRange<enum_OpenXRHand_MotionRange>` **get_motion_range**\ (\ )

Đặt phạm vi chuyển động (nếu được hỗ trợ) để giới hạn chuyển động của bàn tay.

.. rst-class:: classref-item-separator

----

.. _class_OpenXRHand_property_skeleton_rig:

.. rst-class:: classref-property

:ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>` **skeleton_rig** = ``0`` :ref:`🔗<class_OpenXRHand_property_skeleton_rig>`

.. rst-class:: classref-property-setget

- |void| **set_skeleton_rig**\ (\ value\: :ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>`\ ) - :ref:`SkeletonRig<enum_OpenXRHand_SkeletonRig>` **get_skeleton_rig**\ (\ )

Đặt loại skeleton rig mà :ref:`hand_skeleton<class_OpenXRHand_property_hand_skeleton>` tuân thủ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
