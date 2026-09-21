:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesCollisionSphere3D.xml.

.. _class_GPUParticlesCollisionSphere3D:

GPUParticlesCollisionSphere3D
=============================

**Kế thừa:** :ref:`GPUParticlesCollision3D<class_GPUParticlesCollision3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một collision shape hình cầu 3D ảnh hưởng đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một collision shape hình cầu 3D ảnh hưởng đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

Các collision shape của particle hoạt động theo thời gian thực và có thể được di chuyển, xoay và scale trong khi gameplay diễn ra. Không giống attractor, collision shape *không* hỗ trợ scaling không đồng đều.

\ **Lưu ý:** :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` phải là :ref:`ParticleProcessMaterial.COLLISION_RIGID<class_ParticleProcessMaterial_constant_COLLISION_RIGID>` hoặc :ref:`ParticleProcessMaterial.COLLISION_HIDE_ON_CONTACT<class_ParticleProcessMaterial_constant_COLLISION_HIDE_ON_CONTACT>` trong process material của :ref:`GPUParticles3D<class_GPUParticles3D>` thì collision mới hoạt động.

\ **Lưu ý:** Collision của particle chỉ ảnh hưởng đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không ảnh hưởng đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`radius<class_GPUParticlesCollisionSphere3D_property_radius>` | ``1.0`` |
   +---------------------------+--------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesCollisionSphere3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``1.0`` :ref:`🔗<class_GPUParticlesCollisionSphere3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của collision sphere theo đơn vị 3D.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
