:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CompositorEffect.xml.

.. _class_CompositorEffect:

CompositorEffect
================

**Thử nghiệm:** Cách triển khai có thể thay đổi khi ngày càng nhiều thành phần nội bộ của rendering được công khai theo thời gian.

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Resource này cho phép tạo một rendering effect tùy chỉnh.

.. rst-class:: classref-introduction-group

Mô tả
-----

This resource defines a custom rendering effect that can be applied to :ref:`Viewport<class_Viewport>`\ s through the viewports' :ref:`Environment<class_Environment>`. You can implement a callback that is called during rendering at a given stage of the rendering pipeline and allows you to insert additional passes. Note that this callback happens on the rendering thread. CompositorEffect is an abstract base class and must be extended to implement specific rendering logic.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`The Compositor <../tutorials/rendering/compositor>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`access_resolved_color<class_CompositorEffect_property_access_resolved_color>`     |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`access_resolved_depth<class_CompositorEffect_property_access_resolved_depth>`     |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` | :ref:`effect_callback_type<class_CompositorEffect_property_effect_callback_type>`       |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`enabled<class_CompositorEffect_property_enabled>`                                 |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`needs_motion_vectors<class_CompositorEffect_property_needs_motion_vectors>`       |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`needs_normal_roughness<class_CompositorEffect_property_needs_normal_roughness>`   |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`needs_separate_specular<class_CompositorEffect_property_needs_separate_specular>` |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`_render_callback<class_CompositorEffect_private_method__render_callback>`\ (\ effect_callback_type\: :ref:`int<class_int>`, render_data\: :ref:`RenderData<class_RenderData>`\ ) |virtual| |
   +--------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_CompositorEffect_EffectCallbackType:

.. rst-class:: classref-enumeration

enum **EffectCallbackType**: :ref:`🔗<enum_CompositorEffect_EffectCallbackType>`

.. _class_CompositorEffect_constant_EFFECT_CALLBACK_TYPE_PRE_OPAQUE:

.. rst-class:: classref-enumeration-constant

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **EFFECT_CALLBACK_TYPE_PRE_OPAQUE** = ``0``

Callback được gọi trước opaque rendering pass của chúng ta, nhưng sau depth prepass (nếu có).

.. _class_CompositorEffect_constant_EFFECT_CALLBACK_TYPE_POST_OPAQUE:

.. rst-class:: classref-enumeration-constant

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **EFFECT_CALLBACK_TYPE_POST_OPAQUE** = ``1``

Callback được gọi sau opaque rendering pass của chúng ta, nhưng trước khi sky được render.

.. _class_CompositorEffect_constant_EFFECT_CALLBACK_TYPE_POST_SKY:

.. rst-class:: classref-enumeration-constant

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **EFFECT_CALLBACK_TYPE_POST_SKY** = ``2``

Callback được gọi sau khi sky được render, nhưng trước khi các back buffer của chúng ta được tạo (và nếu được bật, trước subsurface scattering và/hoặc screen space reflections).

.. _class_CompositorEffect_constant_EFFECT_CALLBACK_TYPE_PRE_TRANSPARENT:

.. rst-class:: classref-enumeration-constant

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **EFFECT_CALLBACK_TYPE_PRE_TRANSPARENT** = ``3``

Callback được gọi trước transparent rendering pass của chúng ta, nhưng sau khi sky được render và chúng ta đã tạo các back buffer.

.. _class_CompositorEffect_constant_EFFECT_CALLBACK_TYPE_POST_TRANSPARENT:

.. rst-class:: classref-enumeration-constant

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **EFFECT_CALLBACK_TYPE_POST_TRANSPARENT** = ``4``

Callback được gọi sau transparent rendering pass của chúng ta, nhưng trước mọi post-processing effect tích hợp sẵn và trước khi xuất ra render target của chúng ta.

.. _class_CompositorEffect_constant_EFFECT_CALLBACK_TYPE_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **EFFECT_CALLBACK_TYPE_MAX** = ``5``

Đại diện cho kích thước của enum :ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CompositorEffect_property_access_resolved_color:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **access_resolved_color** :ref:`🔗<class_CompositorEffect_property_access_resolved_color>`

.. rst-class:: classref-property-setget

- |void| **set_access_resolved_color**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_access_resolved_color**\ (\ )

Nếu ``true`` và MSAA được bật, thao tác này sẽ kích hoạt việc resolve color buffer trước khi effect được chạy.

\ **Lưu ý:** Trong :ref:`_render_callback()<class_CompositorEffect_private_method__render_callback>`, để truy cập resolved buffer, hãy sử dụng:

::

    var render_scene_buffers = render_data.get_render_scene_buffers()
    var color_buffer = render_scene_buffers.get_texture("render_buffers", "color")

.. rst-class:: classref-item-separator

----

.. _class_CompositorEffect_property_access_resolved_depth:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **access_resolved_depth** :ref:`🔗<class_CompositorEffect_property_access_resolved_depth>`

.. rst-class:: classref-property-setget

- |void| **set_access_resolved_depth**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_access_resolved_depth**\ (\ )

Nếu ``true`` và MSAA được bật, thao tác này sẽ kích hoạt việc resolve depth buffer trước khi effect được chạy.

\ **Lưu ý:** Trong :ref:`_render_callback()<class_CompositorEffect_private_method__render_callback>`, để truy cập resolved buffer, hãy sử dụng:

::

    var render_scene_buffers = render_data.get_render_scene_buffers()
    var depth_buffer = render_scene_buffers.get_texture("render_buffers", "depth")

.. rst-class:: classref-item-separator

----

.. _class_CompositorEffect_property_effect_callback_type:

.. rst-class:: classref-property

:ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **effect_callback_type** :ref:`🔗<class_CompositorEffect_property_effect_callback_type>`

.. rst-class:: classref-property-setget

- |void| **set_effect_callback_type**\ (\ value\: :ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>`\ ) - :ref:`EffectCallbackType<enum_CompositorEffect_EffectCallbackType>` **get_effect_callback_type**\ (\ )

Loại effect được triển khai sẽ xác định giai đoạn rendering mà callback được gọi.

.. rst-class:: classref-item-separator

----

.. _class_CompositorEffect_property_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **enabled** :ref:`🔗<class_CompositorEffect_property_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_enabled**\ (\ )

Nếu ``true``, rendering effect này sẽ được áp dụng cho mọi viewport mà nó được thêm vào.

.. rst-class:: classref-item-separator

----

.. _class_CompositorEffect_property_needs_motion_vectors:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **needs_motion_vectors** :ref:`🔗<class_CompositorEffect_property_needs_motion_vectors>`

.. rst-class:: classref-property-setget

- |void| **set_needs_motion_vectors**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_needs_motion_vectors**\ (\ )

Nếu ``true``, thao tác này sẽ kích hoạt việc tính toán motion vectors trong opaque render state.

\ **Lưu ý:** Trong :ref:`_render_callback()<class_CompositorEffect_private_method__render_callback>`, để truy cập motion vector buffer, hãy sử dụng:

::

    var render_scene_buffers = render_data.get_render_scene_buffers()
    var motion_buffer = render_scene_buffers.get_velocity_texture()

.. rst-class:: classref-item-separator

----

.. _class_CompositorEffect_property_needs_normal_roughness:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **needs_normal_roughness** :ref:`🔗<class_CompositorEffect_property_needs_normal_roughness>`

.. rst-class:: classref-property-setget

- |void| **set_needs_normal_roughness**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_needs_normal_roughness**\ (\ )

Nếu ``true``, thao tác này sẽ kích hoạt việc xuất dữ liệu normal và roughness trong depth pre-pass, chỉ áp dụng cho Forward+ renderer.

\ **Lưu ý:** Trong :ref:`_render_callback()<class_CompositorEffect_private_method__render_callback>`, để truy cập roughness buffer, hãy sử dụng:

::

    var render_scene_buffers = render_data.get_render_scene_buffers()
    var roughness_buffer = render_scene_buffers.get_texture("forward_clustered", "normal_roughness")

Raw normal và roughness buffer được lưu trữ ở một định dạng được tối ưu hóa, khác với định dạng có trong Spatial shader. Khi lấy mẫu buffer, phải áp dụng một hàm chuyển đổi. Hãy sử dụng hàm này, được sao chép từ `here <https://github.com/godotengine/godot/blob/da5f39889f155658cef7f7ec3cc1abb94e17d815/servers/rendering/renderer_rd/shaders/forward_clustered/scene_forward_clustered_inc.glsl#L334-L341>`__:

::

    vec4 normal_roughness_compatibility(vec4 p_normal_roughness) {
        float roughness = p_normal_roughness.w;
        if (roughness > 0.5) {
            roughness = 1.0 - roughness;
        }
        roughness /= (127.0 / 255.0);
        return vec4(normalize(p_normal_roughness.xyz * 2.0 - 1.0) * 0.5 + 0.5, roughness);
    }

.. rst-class:: classref-item-separator

----

.. _class_CompositorEffect_property_needs_separate_specular:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **needs_separate_specular** :ref:`🔗<class_CompositorEffect_property_needs_separate_specular>`

.. rst-class:: classref-property-setget

- |void| **set_needs_separate_specular**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_needs_separate_specular**\ (\ )

Nếu ``true``, thao tác này sẽ kích hoạt việc render dữ liệu specular vào một buffer riêng và kết hợp dữ liệu đó sau khi các effect đã được áp dụng, chỉ áp dụng cho Forward+ renderer.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CompositorEffect_private_method__render_callback:

.. rst-class:: classref-method

|void| **_render_callback**\ (\ effect_callback_type\: :ref:`int<class_int>`, render_data\: :ref:`RenderData<class_RenderData>`\ ) |virtual| :ref:`🔗<class_CompositorEffect_private_method__render_callback>`

Triển khai hàm này bằng mã rendering tùy chỉnh của bạn. ``effect_callback_type`` phải luôn khớp với effect callback type bạn đã chỉ định trong :ref:`effect_callback_type<class_CompositorEffect_property_effect_callback_type>`. ``render_data`` cung cấp quyền truy cập vào rendering state; nó chỉ hợp lệ trong quá trình rendering và không nên được lưu trữ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
