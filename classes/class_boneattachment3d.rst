:github_url: hide

.. meta::
	:keywords: tag

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/BoneAttachment3D.xml.

.. _class_BoneAttachment3D:

BoneAttachment3D
================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node tự động sao chép hoặc ghi đè transform 3D của một xương trong :ref:`Skeleton3D<class_Skeleton3D>` cha.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này chọn một xương trong :ref:`Skeleton3D<class_Skeleton3D>` và gắn vào xương đó. Điều này có nghĩa là node **BoneAttachment3D** sẽ tự động sao chép hoặc ghi đè transform 3D của xương đã chọn.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                               | :ref:`bone_idx<class_BoneAttachment3D_property_bone_idx>`                           | ``-1``                                                                        |
   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                         | :ref:`bone_name<class_BoneAttachment3D_property_bone_name>`                         | ``""``                                                                        |
   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`NodePath<class_NodePath>`                                     | :ref:`external_skeleton<class_BoneAttachment3D_property_external_skeleton>`         |                                                                               |
   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`override_pose<class_BoneAttachment3D_property_override_pose>`                 | ``false``                                                                     |
   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` | physics_interpolation_mode                                                          | ``2`` (overrides :ref:`Node<class_Node_property_physics_interpolation_mode>`) |
   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`use_external_skeleton<class_BoneAttachment3D_property_use_external_skeleton>` | ``false``                                                                     |
   +---------------------------------------------------------------------+-------------------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------+
   | :ref:`Skeleton3D<class_Skeleton3D>` | :ref:`get_skeleton<class_BoneAttachment3D_method_get_skeleton>`\ (\ )             |
   +-------------------------------------+-----------------------------------------------------------------------------------+
   | |void|                              | :ref:`on_skeleton_update<class_BoneAttachment3D_method_on_skeleton_update>`\ (\ ) |
   +-------------------------------------+-----------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BoneAttachment3D_property_bone_idx:

.. rst-class:: classref-property

:ref:`int<class_int>` **bone_idx** = ``-1`` :ref:`🔗<class_BoneAttachment3D_property_bone_idx>`

.. rst-class:: classref-property-setget

- |void| **set_bone_idx**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bone_idx**\ (\ )

Chỉ mục của xương được gắn.

.. rst-class:: classref-item-separator

----

.. _class_BoneAttachment3D_property_bone_name:

.. rst-class:: classref-property

:ref:`String<class_String>` **bone_name** = ``""`` :ref:`🔗<class_BoneAttachment3D_property_bone_name>`

.. rst-class:: classref-property-setget

- |void| **set_bone_name**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_bone_name**\ (\ )

Tên của xương được gắn.

.. rst-class:: classref-item-separator

----

.. _class_BoneAttachment3D_property_external_skeleton:

.. rst-class:: classref-property

:ref:`NodePath<class_NodePath>` **external_skeleton** :ref:`🔗<class_BoneAttachment3D_property_external_skeleton>`

.. rst-class:: classref-property-setget

- |void| **set_external_skeleton**\ (\ value\: :ref:`NodePath<class_NodePath>`\ ) - :ref:`NodePath<class_NodePath>` **get_external_skeleton**\ (\ )

:ref:`NodePath<class_NodePath>` trỏ đến node :ref:`Skeleton3D<class_Skeleton3D>` bên ngoài.

.. rst-class:: classref-item-separator

----

.. _class_BoneAttachment3D_property_override_pose:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **override_pose** = ``false`` :ref:`🔗<class_BoneAttachment3D_property_override_pose>`

.. rst-class:: classref-property-setget

- |void| **set_override_pose**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_override_pose**\ (\ )

Xác định liệu node **BoneAttachment3D** có ghi đè pose của xương mà nó được gắn vào hay không. Khi được đặt thành ``true``, node **BoneAttachment3D** có thể thay đổi pose của xương. Khi được đặt thành ``false``, **BoneAttachment3D** sẽ luôn được đặt theo transform của xương.

\ **Lưu ý:** Việc ghi đè này được thực hiện gián đoạn trong quy trình cập nhật skeleton bằng signal do thiết kế cũ. Nó có thể gây ra hành vi không mong muốn khi được sử dụng đồng thời với :ref:`SkeletonModifier3D<class_SkeletonModifier3D>`.

.. rst-class:: classref-item-separator

----

.. _class_BoneAttachment3D_property_use_external_skeleton:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_external_skeleton** = ``false`` :ref:`🔗<class_BoneAttachment3D_property_use_external_skeleton>`

.. rst-class:: classref-property-setget

- |void| **set_use_external_skeleton**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_use_external_skeleton**\ (\ )

Xác định liệu node **BoneAttachment3D** có sử dụng node :ref:`Skeleton3D<class_Skeleton3D>` bên ngoài thay vì cố gắng sử dụng node cha của nó làm :ref:`Skeleton3D<class_Skeleton3D>` hay không. Khi được đặt thành ``true``, node **BoneAttachment3D** sẽ sử dụng node :ref:`Skeleton3D<class_Skeleton3D>` bên ngoài được đặt trong :ref:`external_skeleton<class_BoneAttachment3D_property_external_skeleton>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_BoneAttachment3D_method_get_skeleton:

.. rst-class:: classref-method

:ref:`Skeleton3D<class_Skeleton3D>` **get_skeleton**\ (\ ) :ref:`🔗<class_BoneAttachment3D_method_get_skeleton>`

Trả về node :ref:`Skeleton3D<class_Skeleton3D>` cha hoặc bên ngoài nếu node đó tồn tại; nếu không, trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_BoneAttachment3D_method_on_skeleton_update:

.. rst-class:: classref-method

|void| **on_skeleton_update**\ (\ ) :ref:`🔗<class_BoneAttachment3D_method_on_skeleton_update>`

Một hàm được tự động gọi khi :ref:`Skeleton3D<class_Skeleton3D>` được cập nhật. Đây là nơi node **BoneAttachment3D** cập nhật vị trí của nó để được liên kết chính xác khi *không* được đặt để ghi đè pose của xương.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
