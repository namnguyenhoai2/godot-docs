:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CanvasItemMaterial.xml.

.. _class_CanvasItemMaterial:

CanvasItemMaterial
==================

**Kế thừa:** :ref:`Material<class_Material>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

A material for :ref:`CanvasItem<class_CanvasItem>`\ s.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CanvasItemMaterial**\ s cung cấp phương thức để sửa đổi các texture liên kết với một CanvasItem. Chúng chuyên dùng để mô tả các hành vi blend và chiếu sáng cho texture. Sử dụng một :ref:`ShaderMaterial<class_ShaderMaterial>` để tùy chỉnh đầy đủ hơn cách material tương tác với một :ref:`CanvasItem<class_CanvasItem>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
   | :ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` | :ref:`blend_mode<class_CanvasItemMaterial_property_blend_mode>`                           | ``0``     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
   | :ref:`LightMode<enum_CanvasItemMaterial_LightMode>` | :ref:`light_mode<class_CanvasItemMaterial_property_light_mode>`                           | ``0``     |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                               | :ref:`particles_anim_h_frames<class_CanvasItemMaterial_property_particles_anim_h_frames>` |           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                             | :ref:`particles_anim_loop<class_CanvasItemMaterial_property_particles_anim_loop>`         |           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`                               | :ref:`particles_anim_v_frames<class_CanvasItemMaterial_property_particles_anim_v_frames>` |           |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                             | :ref:`particles_animation<class_CanvasItemMaterial_property_particles_animation>`         | ``false`` |
   +-----------------------------------------------------+-------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_CanvasItemMaterial_BlendMode:

.. rst-class:: classref-enumeration

enum **BlendMode**: :ref:`🔗<enum_CanvasItemMaterial_BlendMode>`

.. _class_CanvasItemMaterial_constant_BLEND_MODE_MIX:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **BLEND_MODE_MIX** = ``0``

Chế độ blend Mix. Các màu được giả định là độc lập với giá trị alpha (độ trong suốt).

.. _class_CanvasItemMaterial_constant_BLEND_MODE_ADD:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **BLEND_MODE_ADD** = ``1``

Chế độ blend Additive.

.. _class_CanvasItemMaterial_constant_BLEND_MODE_SUB:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **BLEND_MODE_SUB** = ``2``

Chế độ blend Subtractive.

.. _class_CanvasItemMaterial_constant_BLEND_MODE_MUL:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **BLEND_MODE_MUL** = ``3``

Chế độ blend Multiplicative.

.. _class_CanvasItemMaterial_constant_BLEND_MODE_PREMULT_ALPHA:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **BLEND_MODE_PREMULT_ALPHA** = ``4``

Chế độ blend Mix. Các màu được giả định đã được nhân trước với giá trị alpha (độ trong suốt).

.. rst-class:: classref-item-separator

----

.. _enum_CanvasItemMaterial_LightMode:

.. rst-class:: classref-enumeration

enum **LightMode**: :ref:`🔗<enum_CanvasItemMaterial_LightMode>`

.. _class_CanvasItemMaterial_constant_LIGHT_MODE_NORMAL:

.. rst-class:: classref-enumeration-constant

:ref:`LightMode<enum_CanvasItemMaterial_LightMode>` **LIGHT_MODE_NORMAL** = ``0``

Render material bằng cả các thuộc tính material nhạy sáng và không nhạy sáng.

.. _class_CanvasItemMaterial_constant_LIGHT_MODE_UNSHADED:

.. rst-class:: classref-enumeration-constant

:ref:`LightMode<enum_CanvasItemMaterial_LightMode>` **LIGHT_MODE_UNSHADED** = ``1``

Render material như thể không có ánh sáng.

.. _class_CanvasItemMaterial_constant_LIGHT_MODE_LIGHT_ONLY:

.. rst-class:: classref-enumeration-constant

:ref:`LightMode<enum_CanvasItemMaterial_LightMode>` **LIGHT_MODE_LIGHT_ONLY** = ``2``

Render material như thể chỉ có ánh sáng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CanvasItemMaterial_property_blend_mode:

.. rst-class:: classref-property

:ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **blend_mode** = ``0`` :ref:`🔗<class_CanvasItemMaterial_property_blend_mode>`

.. rst-class:: classref-property-setget

- |void| **set_blend_mode**\ (\ value\: :ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>`\ ) - :ref:`BlendMode<enum_CanvasItemMaterial_BlendMode>` **get_blend_mode**\ (\ )

Cách áp dụng việc render của material lên các texture bên dưới.

.. rst-class:: classref-item-separator

----

.. _class_CanvasItemMaterial_property_light_mode:

.. rst-class:: classref-property

:ref:`LightMode<enum_CanvasItemMaterial_LightMode>` **light_mode** = ``0`` :ref:`🔗<class_CanvasItemMaterial_property_light_mode>`

.. rst-class:: classref-property-setget

- |void| **set_light_mode**\ (\ value\: :ref:`LightMode<enum_CanvasItemMaterial_LightMode>`\ ) - :ref:`LightMode<enum_CanvasItemMaterial_LightMode>` **get_light_mode**\ (\ )

Cách material phản ứng với ánh sáng.

.. rst-class:: classref-item-separator

----

.. _class_CanvasItemMaterial_property_particles_anim_h_frames:

.. rst-class:: classref-property

:ref:`int<class_int>` **particles_anim_h_frames** :ref:`🔗<class_CanvasItemMaterial_property_particles_anim_h_frames>`

.. rst-class:: classref-property-setget

- |void| **set_particles_anim_h_frames**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_particles_anim_h_frames**\ (\ )

Số cột trong spritesheet được gán làm :ref:`Texture2D<class_Texture2D>` cho một :ref:`GPUParticles2D<class_GPUParticles2D>` hoặc :ref:`CPUParticles2D<class_CPUParticles2D>`.

\ **Lưu ý:** Thuộc tính này chỉ được sử dụng và hiển thị trong editor nếu :ref:`particles_animation<class_CanvasItemMaterial_property_particles_animation>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CanvasItemMaterial_property_particles_anim_loop:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **particles_anim_loop** :ref:`🔗<class_CanvasItemMaterial_property_particles_anim_loop>`

.. rst-class:: classref-property-setget

- |void| **set_particles_anim_loop**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_particles_anim_loop**\ (\ )

Nếu ``true``, animation của particle sẽ lặp lại.

\ **Lưu ý:** Thuộc tính này chỉ được sử dụng và hiển thị trong editor nếu :ref:`particles_animation<class_CanvasItemMaterial_property_particles_animation>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CanvasItemMaterial_property_particles_anim_v_frames:

.. rst-class:: classref-property

:ref:`int<class_int>` **particles_anim_v_frames** :ref:`🔗<class_CanvasItemMaterial_property_particles_anim_v_frames>`

.. rst-class:: classref-property-setget

- |void| **set_particles_anim_v_frames**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_particles_anim_v_frames**\ (\ )

Số hàng trong spritesheet được gán làm :ref:`Texture2D<class_Texture2D>` cho một :ref:`GPUParticles2D<class_GPUParticles2D>` hoặc :ref:`CPUParticles2D<class_CPUParticles2D>`.

\ **Lưu ý:** Thuộc tính này chỉ được sử dụng và hiển thị trong editor nếu :ref:`particles_animation<class_CanvasItemMaterial_property_particles_animation>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_CanvasItemMaterial_property_particles_animation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **particles_animation** = ``false`` :ref:`🔗<class_CanvasItemMaterial_property_particles_animation>`

.. rst-class:: classref-property-setget

- |void| **set_particles_animation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_particles_animation**\ (\ )

Nếu ``true``, bật các tính năng animation dựa trên spritesheet khi được gán cho các node :ref:`GPUParticles2D<class_GPUParticles2D>` và :ref:`CPUParticles2D<class_CPUParticles2D>`. :ref:`ParticleProcessMaterial.anim_speed_max<class_ParticleProcessMaterial_property_anim_speed_max>` hoặc :ref:`CPUParticles2D.anim_speed_max<class_CPUParticles2D_property_anim_speed_max>` cũng phải được đặt thành một giá trị dương để animation phát.

Thuộc tính này (và các thuộc tính ``particles_anim_*`` khác phụ thuộc vào nó) không có tác dụng trên các loại node khác.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
