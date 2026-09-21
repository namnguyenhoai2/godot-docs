:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesCollision3D.xml.

.. _class_GPUParticlesCollision3D:

GPUParticlesCollision3D
=======================

**Kế thừa:** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`GPUParticlesCollisionBox3D<class_GPUParticlesCollisionBox3D>`, :ref:`GPUParticlesCollisionHeightField3D<class_GPUParticlesCollisionHeightField3D>`, :ref:`GPUParticlesCollisionSDF3D<class_GPUParticlesCollisionSDF3D>`, :ref:`GPUParticlesCollisionSphere3D<class_GPUParticlesCollisionSphere3D>`

Lớp cơ sở trừu tượng cho các hình dạng va chạm hạt 3D tác động đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các hình dạng va chạm hạt có thể được dùng để khiến các hạt dừng lại hoặc bật nảy khi va vào chúng.

Các hình dạng va chạm hạt hoạt động theo thời gian thực và có thể được di chuyển, xoay, thay đổi tỷ lệ trong khi chơi. Không giống attractor, các hình dạng va chạm không hỗ trợ thay đổi tỷ lệ không đồng đều.

Có thể tạm thời vô hiệu hóa các hình dạng va chạm hạt bằng cách ẩn chúng.

\ **Lưu ý:** :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` phải là :ref:`ParticleProcessMaterial.COLLISION_RIGID<class_ParticleProcessMaterial_constant_COLLISION_RIGID>` hoặc :ref:`ParticleProcessMaterial.COLLISION_HIDE_ON_CONTACT<class_ParticleProcessMaterial_constant_COLLISION_HIDE_ON_CONTACT>` trên process material của :ref:`GPUParticles3D<class_GPUParticles3D>` để va chạm hoạt động.

\ **Lưu ý:** Va chạm hạt chỉ tác động đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không tác động đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

\ **Lưu ý:** Các hạt bị collider đang di chuyển đẩy đi sẽ không được nội suy, điều này có thể gây ra hiện tượng giật hình dễ nhận thấy. Có thể giảm hiện tượng này bằng cách đặt :ref:`GPUParticles3D.fixed_fps<class_GPUParticles3D_property_fixed_fps>` thành ``0`` hoặc một giá trị khớp hoặc cao hơn framerate mục tiêu.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------+----------------+
   | :ref:`int<class_int>` | :ref:`cull_mask<class_GPUParticlesCollision3D_property_cull_mask>` | ``4294967295`` |
   +-----------------------+--------------------------------------------------------------------+----------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesCollision3D_property_cull_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **cull_mask** = ``4294967295`` :ref:`🔗<class_GPUParticlesCollision3D_property_cull_mask>`

.. rst-class:: classref-property-setget

- |void| **set_cull_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_cull_mask**\ (\ )

Các layer kết xuất hạt (:ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>`) sẽ chịu tác động của hình dạng va chạm. Theo mặc định, tất cả các hạt có :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` được đặt thành :ref:`ParticleProcessMaterial.COLLISION_RIGID<class_ParticleProcessMaterial_constant_COLLISION_RIGID>` hoặc :ref:`ParticleProcessMaterial.COLLISION_HIDE_ON_CONTACT<class_ParticleProcessMaterial_constant_COLLISION_HIDE_ON_CONTACT>` sẽ chịu tác động của hình dạng va chạm.

Sau khi cấu hình các node hạt tương ứng, có thể bỏ chọn các layer cụ thể để ngăn một số hạt nhất định chịu tác động của collider. Ví dụ, bạn có thể dùng cách này nếu đang sử dụng một collider như một phần của hiệu ứng phép thuật nhưng không muốn collider tác động đến các hạt thời tiết không liên quan ở cùng vị trí.

Bạn cũng có thể vô hiệu hóa va chạm hạt trên từng process material bằng cách đặt :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` trên node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
