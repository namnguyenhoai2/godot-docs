:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicalBoneSimulator3D.xml.

.. _class_PhysicalBoneSimulator3D:

PhysicalBoneSimulator3D
=======================

**Kế thừa:** :ref:`SkeletonModifier3D<class_SkeletonModifier3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node có thể làm node cha của :ref:`PhysicalBone3D<class_PhysicalBone3D>` và có thể áp dụng kết quả mô phỏng cho :ref:`Skeleton3D<class_Skeleton3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node có thể làm node cha của :ref:`PhysicalBone3D<class_PhysicalBone3D>` và có thể áp dụng kết quả mô phỏng cho :ref:`Skeleton3D<class_Skeleton3D>`.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`is_simulating_physics<class_PhysicalBoneSimulator3D_method_is_simulating_physics>`\ (\ ) |const|                                                                                            |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`physical_bones_add_collision_exception<class_PhysicalBoneSimulator3D_method_physical_bones_add_collision_exception>`\ (\ exception\: :ref:`RID<class_RID>`\ )                               |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`physical_bones_remove_collision_exception<class_PhysicalBoneSimulator3D_method_physical_bones_remove_collision_exception>`\ (\ exception\: :ref:`RID<class_RID>`\ )                         |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`physical_bones_start_simulation<class_PhysicalBoneSimulator3D_method_physical_bones_start_simulation>`\ (\ bones\: :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] = []\ ) |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`physical_bones_stop_simulation<class_PhysicalBoneSimulator3D_method_physical_bones_stop_simulation>`\ (\ )                                                                                  |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_PhysicalBoneSimulator3D_method_is_simulating_physics:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_simulating_physics**\ (\ ) |const| :ref:`🔗<class_PhysicalBoneSimulator3D_method_is_simulating_physics>`

Trả về một giá trị boolean cho biết **PhysicalBoneSimulator3D** có đang chạy và mô phỏng hay không.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBoneSimulator3D_method_physical_bones_add_collision_exception:

.. rst-class:: classref-method

|void| **physical_bones_add_collision_exception**\ (\ exception\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_PhysicalBoneSimulator3D_method_physical_bones_add_collision_exception>`

Thêm một ngoại lệ va chạm cho xương vật lý.

Hoạt động giống hệt node :ref:`RigidBody3D<class_RigidBody3D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBoneSimulator3D_method_physical_bones_remove_collision_exception:

.. rst-class:: classref-method

|void| **physical_bones_remove_collision_exception**\ (\ exception\: :ref:`RID<class_RID>`\ ) :ref:`🔗<class_PhysicalBoneSimulator3D_method_physical_bones_remove_collision_exception>`

Xóa một ngoại lệ va chạm khỏi xương vật lý.

Hoạt động giống hệt node :ref:`RigidBody3D<class_RigidBody3D>`.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBoneSimulator3D_method_physical_bones_start_simulation:

.. rst-class:: classref-method

|void| **physical_bones_start_simulation**\ (\ bones\: :ref:`Array<class_Array>`\[:ref:`StringName<class_StringName>`\] = []\ ) :ref:`🔗<class_PhysicalBoneSimulator3D_method_physical_bones_start_simulation>`

Yêu cầu các node :ref:`PhysicalBone3D<class_PhysicalBone3D>` trong Skeleton bắt đầu mô phỏng và phản ứng với thế giới vật lý.

Có thể tùy chọn truyền vào một danh sách tên xương, cho phép chỉ mô phỏng các xương được truyền vào.

.. rst-class:: classref-item-separator

----

.. _class_PhysicalBoneSimulator3D_method_physical_bones_stop_simulation:

.. rst-class:: classref-method

|void| **physical_bones_stop_simulation**\ (\ ) :ref:`🔗<class_PhysicalBoneSimulator3D_method_physical_bones_stop_simulation>`

Yêu cầu các node :ref:`PhysicalBone3D<class_PhysicalBone3D>` trong Skeleton dừng mô phỏng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
