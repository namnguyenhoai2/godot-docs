:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/BoneMap.xml.

.. _class_BoneMap:

BoneMap
=======

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Mô tả ánh xạ tên xương để retargeting :ref:`Skeleton3D<class_Skeleton3D>` thành các tên chung được định nghĩa bởi một :ref:`SkeletonProfile<class_SkeletonProfile>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này chứa một dictionary sử dụng danh sách tên xương trong :ref:`SkeletonProfile<class_SkeletonProfile>` làm các tên khóa.

Bằng cách gán tên xương :ref:`Skeleton3D<class_Skeleton3D>` thực tế làm giá trị khóa, nó ánh xạ :ref:`Skeleton3D<class_Skeleton3D>` tới :ref:`SkeletonProfile<class_SkeletonProfile>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Retargeting 3D Skeletons <../tutorials/assets_pipeline/retargeting_3d_skeletons>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------+------------------------------------------------+
   | :ref:`SkeletonProfile<class_SkeletonProfile>` | :ref:`profile<class_BoneMap_property_profile>` |
   +-----------------------------------------------+------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`find_profile_bone_name<class_BoneMap_method_find_profile_bone_name>`\ (\ skeleton_bone_name\: :ref:`StringName<class_StringName>`\ ) |const|                                                  |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`StringName<class_StringName>` | :ref:`get_skeleton_bone_name<class_BoneMap_method_get_skeleton_bone_name>`\ (\ profile_bone_name\: :ref:`StringName<class_StringName>`\ ) |const|                                                   |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_skeleton_bone_name<class_BoneMap_method_set_skeleton_bone_name>`\ (\ profile_bone_name\: :ref:`StringName<class_StringName>`, skeleton_bone_name\: :ref:`StringName<class_StringName>`\ ) |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_BoneMap_signal_bone_map_updated:

.. rst-class:: classref-signal

**bone_map_updated**\ (\ ) :ref:`🔗<class_BoneMap_signal_bone_map_updated>`

Signal này được phát khi thay đổi giá trị khóa trong **BoneMap**. Signal này được dùng để xác thực ánh xạ và cập nhật trình chỉnh sửa **BoneMap**.

.. rst-class:: classref-item-separator

----

.. _class_BoneMap_signal_profile_updated:

.. rst-class:: classref-signal

**profile_updated**\ (\ ) :ref:`🔗<class_BoneMap_signal_profile_updated>`

Signal này được phát khi thay đổi giá trị trong profile hoặc thay đổi tham chiếu của profile. Signal này được dùng để cập nhật tên khóa trong **BoneMap** và vẽ lại trình chỉnh sửa **BoneMap**.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BoneMap_property_profile:

.. rst-class:: classref-property

:ref:`SkeletonProfile<class_SkeletonProfile>` **profile** :ref:`🔗<class_BoneMap_property_profile>`

.. rst-class:: classref-property-setget

- |void| **set_profile**\ (\ value\: :ref:`SkeletonProfile<class_SkeletonProfile>`\ ) - :ref:`SkeletonProfile<class_SkeletonProfile>` **get_profile**\ (\ )

Một :ref:`SkeletonProfile<class_SkeletonProfile>` của đích ánh xạ. Tên khóa trong **BoneMap** được đồng bộ hóa với nó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_BoneMap_method_find_profile_bone_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **find_profile_bone_name**\ (\ skeleton_bone_name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_BoneMap_method_find_profile_bone_name>`

Trả về một tên xương trong profile có ``skeleton_bone_name``. Nếu không tìm thấy, một :ref:`StringName<class_StringName>` rỗng sẽ được trả về.

Trong quá trình retargeting, tên xương được trả về là tên xương của skeleton đích.

.. rst-class:: classref-item-separator

----

.. _class_BoneMap_method_get_skeleton_bone_name:

.. rst-class:: classref-method

:ref:`StringName<class_StringName>` **get_skeleton_bone_name**\ (\ profile_bone_name\: :ref:`StringName<class_StringName>`\ ) |const| :ref:`🔗<class_BoneMap_method_get_skeleton_bone_name>`

Trả về tên xương của skeleton được ánh xạ tới ``profile_bone_name``.

Trong quá trình retargeting, tên xương được trả về là tên xương của skeleton nguồn.

.. rst-class:: classref-item-separator

----

.. _class_BoneMap_method_set_skeleton_bone_name:

.. rst-class:: classref-method

|void| **set_skeleton_bone_name**\ (\ profile_bone_name\: :ref:`StringName<class_StringName>`, skeleton_bone_name\: :ref:`StringName<class_StringName>`\ ) :ref:`🔗<class_BoneMap_method_set_skeleton_bone_name>`

Ánh xạ tên xương của skeleton tới ``profile_bone_name``.

Trong quá trình retargeting, tên xương được thiết lập là tên xương của skeleton nguồn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
