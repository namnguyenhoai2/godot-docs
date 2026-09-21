:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesAttractorSphere3D.xml.

.. _class_GPUParticlesAttractorSphere3D:

GPUParticlesAttractorSphere3D
=============================

**Kế thừa:** :ref:`GPUParticlesAttractor3D<class_GPUParticlesAttractor3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Attractor hình cầu dẹt có hình dạng spheroid, tác động đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Attractor hình cầu dẹt có hình dạng spheroid, tác động đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`. Có thể dùng để hút các particle về phía gốc của nó hoặc đẩy chúng ra xa gốc.

Particle attractor hoạt động theo thời gian thực và có thể được di chuyển, xoay và thay đổi scale trong khi gameplay diễn ra. Không giống các collision shape, attractor cũng hỗ trợ scale không đồng đều.

\ **Lưu ý:** Particle attractor chỉ tác động đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không tác động đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+--------------------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`radius<class_GPUParticlesAttractorSphere3D_property_radius>` | ``1.0`` |
   +---------------------------+--------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesAttractorSphere3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``1.0`` :ref:`🔗<class_GPUParticlesAttractorSphere3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của attractor hình cầu, tính theo đơn vị 3D.

\ **Lưu ý:** Có thể tạo các ellipse bị kéo giãn bằng cách sử dụng scale không đồng đều trên node **GPUParticlesAttractorSphere3D**.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
