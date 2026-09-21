:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesAttractorVectorField3D.xml.

.. _class_GPUParticlesAttractorVectorField3D:

GPUParticlesAttractorVectorField3D
==================================

**Kế thừa:** :ref:`GPUParticlesAttractor3D<class_GPUParticlesAttractor3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một bộ hút hình hộp với các hướng và cường độ thay đổi được xác định bên trong, có tác động đến các hạt từ các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một bộ hút hình hộp với các hướng và cường độ thay đổi được xác định bên trong, có tác động đến các hạt từ các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

Không giống :ref:`GPUParticlesAttractorBox3D<class_GPUParticlesAttractorBox3D>`, **GPUParticlesAttractorVectorField3D** sử dụng một :ref:`texture<class_GPUParticlesAttractorVectorField3D_property_texture>` để tác động đến cường độ hút bên trong hộp. Điều này có thể được dùng để tạo ra các tình huống hút phức tạp, trong đó các hạt di chuyển theo những hướng khác nhau tùy thuộc vào vị trí của chúng. Tính năng này hữu ích cho các hiệu ứng thời tiết như bão cát.

Các bộ hút hạt hoạt động theo thời gian thực và có thể được di chuyển, xoay và thay đổi tỉ lệ trong khi chơi. Không giống các hình dạng va chạm, bộ hút cũng hỗ trợ scaling không đồng đều.

\ **Lưu ý:** Các bộ hút hạt chỉ tác động đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không tác động đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+---------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`     | :ref:`size<class_GPUParticlesAttractorVectorField3D_property_size>`       | ``Vector3(2, 2, 2)`` |
   +-----------------------------------+---------------------------------------------------------------------------+----------------------+
   | :ref:`Texture3D<class_Texture3D>` | :ref:`texture<class_GPUParticlesAttractorVectorField3D_property_texture>` |                      |
   +-----------------------------------+---------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesAttractorVectorField3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_GPUParticlesAttractorVectorField3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của hộp vector field theo đơn vị 3D.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesAttractorVectorField3D_property_texture:

.. rst-class:: classref-property

:ref:`Texture3D<class_Texture3D>` **texture** :ref:`🔗<class_GPUParticlesAttractorVectorField3D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture3D<class_Texture3D>`\ ) - :ref:`Texture3D<class_Texture3D>` **get_texture**\ (\ )

Texture 3D sẽ được sử dụng. Các giá trị được nội suy tuyến tính giữa những pixel của texture.

\ **Lưu ý:** Để có hiệu suất tốt hơn, resolution của texture 3D nên phản ánh :ref:`size<class_GPUParticlesAttractorVectorField3D_property_size>` của bộ hút. Vì lực hút hạt thường là dữ liệu có tần số thấp, texture có thể được giữ ở resolution thấp, chẳng hạn như 64×64×64.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
