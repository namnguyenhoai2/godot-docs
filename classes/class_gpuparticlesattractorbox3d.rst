:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesAttractorBox3D.xml.

.. _class_GPUParticlesAttractorBox3D:

GPUParticlesAttractorBox3D
==========================

**Kế thừa:** :ref:`GPUParticlesAttractor3D<class_GPUParticlesAttractor3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một attractor hình hộp tạo ảnh hưởng đến các particle từ các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một attractor hình hộp tạo ảnh hưởng đến các particle từ các node :ref:`GPUParticles3D<class_GPUParticles3D>`. Có thể dùng để hút các particle về phía gốc của nó hoặc đẩy chúng ra xa gốc.

Particle attractor hoạt động theo thời gian thực và có thể được di chuyển, xoay và thay đổi tỷ lệ trong quá trình chơi. Không giống như các collision shape, attractor cũng hỗ trợ thay đổi tỷ lệ không đồng đều.

\ **Lưu ý:** Particle attractor chỉ ảnh hưởng đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không ảnh hưởng đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`size<class_GPUParticlesAttractorBox3D_property_size>` | ``Vector3(2, 2, 2)`` |
   +-------------------------------+-------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesAttractorBox3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_GPUParticlesAttractorBox3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của attractor box theo đơn vị 3D.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
