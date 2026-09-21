:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesAttractor3D.xml.

.. _class_GPUParticlesAttractor3D:

GPUParticlesAttractor3D
=======================

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`GPUParticlesAttractorBox3D<class_GPUParticlesAttractorBox3D>`, :ref:`GPUParticlesAttractorSphere3D<class_GPUParticlesAttractorSphere3D>`, :ref:`GPUParticlesAttractorVectorField3D<class_GPUParticlesAttractorVectorField3D>`

Lớp cơ sở trừu tượng cho các particle attractor 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Particle attractor có thể được dùng để hút các particle về phía gốc của attractor hoặc đẩy chúng ra xa gốc của attractor.

Particle attractor hoạt động theo thời gian thực và có thể được di chuyển, xoay, cũng như thay đổi tỷ lệ trong khi gameplay diễn ra. Không giống collision shape, attractor cũng hỗ trợ thay đổi tỷ lệ không đồng đều.

Có thể tạm thời vô hiệu hóa attractor bằng cách ẩn chúng hoặc đặt :ref:`strength<class_GPUParticlesAttractor3D_property_strength>` thành ``0.0``.

\ **Lưu ý:** Particle attractor chỉ ảnh hưởng đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không ảnh hưởng đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`attenuation<class_GPUParticlesAttractor3D_property_attenuation>`       | ``1.0``        |
   +---------------------------+------------------------------------------------------------------------------+----------------+
   | :ref:`int<class_int>`     | :ref:`cull_mask<class_GPUParticlesAttractor3D_property_cull_mask>`           | ``4294967295`` |
   +---------------------------+------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`directionality<class_GPUParticlesAttractor3D_property_directionality>` | ``0.0``        |
   +---------------------------+------------------------------------------------------------------------------+----------------+
   | :ref:`float<class_float>` | :ref:`strength<class_GPUParticlesAttractor3D_property_strength>`             | ``1.0``        |
   +---------------------------+------------------------------------------------------------------------------+----------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesAttractor3D_property_attenuation:

.. rst-class:: classref-property

:ref:`float<class_float>` **attenuation** = ``1.0`` :ref:`🔗<class_GPUParticlesAttractor3D_property_attenuation>`

.. rst-class:: classref-property-setget

- |void| **set_attenuation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_attenuation**\ (\ )

Độ suy giảm của particle attractor. Giá trị càng cao thì lực đẩy các particle khi chúng đến gần gốc của attractor càng từ từ. Giá trị bằng không hoặc âm sẽ khiến các particle bị đẩy đi rất nhanh ngay khi chạm vào các cạnh của attractor.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesAttractor3D_property_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **cull_mask** = ``4294967295`` :ref:`🔗<class_GPUParticlesAttractor3D_property_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_cull_mask**\ (\ )

Các lớp particle rendering (:ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>`) sẽ chịu ảnh hưởng của attractor. Theo mặc định, tất cả particle đều chịu ảnh hưởng của attractor.

Sau khi cấu hình các particle node tương ứng, bạn có thể bỏ chọn các lớp cụ thể để ngăn một số particle nhất định chịu ảnh hưởng của attractor. Ví dụ, cách này có thể được sử dụng khi bạn dùng attractor như một phần của hiệu ứng phép thuật nhưng không muốn attractor ảnh hưởng đến các particle thời tiết không liên quan ở cùng vị trí.

Cũng có thể vô hiệu hóa particle attraction trên cơ sở từng process material bằng cách đặt :ref:`ParticleProcessMaterial.attractor_interaction_enabled<class_ParticleProcessMaterial_property_attractor_interaction_enabled>` trên node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesAttractor3D_property_directionality:

.. rst-class:: classref-property

:ref:`float<class_float>` **directionality** = ``0.0`` :ref:`🔗<class_GPUParticlesAttractor3D_property_directionality>`

.. rst-class:: classref-property-setget

- |void| **set_directionality**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_directionality**\ (\ )

Điều chỉnh mức độ định hướng của attractor. Ở ``0.0``, attractor hoàn toàn không có tính định hướng: nó sẽ hút các particle về phía tâm. Ở ``1.0``, attractor có tính định hướng hoàn toàn: các particle sẽ luôn bị đẩy về phía -Z cục bộ (hoặc +Z nếu :ref:`strength<class_GPUParticlesAttractor3D_property_strength>` là số âm).

\ **Lưu ý:** Nếu :ref:`directionality<class_GPUParticlesAttractor3D_property_directionality>` lớn hơn ``0.0``, hướng đẩy các particle có thể được thay đổi bằng cách xoay node **GPUParticlesAttractor3D**.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesAttractor3D_property_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **strength** = ``1.0`` :ref:`🔗<class_GPUParticlesAttractor3D_property_strength>`

.. rst-class:: classref-property-setget

- |void| **set_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_strength**\ (\ )

Điều chỉnh độ mạnh của attractor. Nếu :ref:`strength<class_GPUParticlesAttractor3D_property_strength>` là số âm, các particle sẽ bị đẩy theo hướng ngược lại. Các particle sẽ bị đẩy *ra xa* gốc của attractor nếu :ref:`directionality<class_GPUParticlesAttractor3D_property_directionality>` là ``0.0``, hoặc về phía +Z cục bộ nếu :ref:`directionality<class_GPUParticlesAttractor3D_property_directionality>` lớn hơn ``0.0``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
