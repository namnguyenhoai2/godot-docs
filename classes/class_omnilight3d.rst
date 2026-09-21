:github_url: hide

.. meta::
	:keywords: point

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/OmniLight3D.xml.

.. _class_OmniLight3D:

OmniLight3D
===========

**Kế thừa:** :ref:`Light3D<class_Light3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Ánh sáng đa hướng, chẳng hạn như bóng đèn hoặc nến.

.. rst-class:: classref-introduction-group

Mô tả
-----

Ánh sáng đa hướng là một loại :ref:`Light3D<class_Light3D>` phát ra ánh sáng theo mọi hướng. Ánh sáng bị suy giảm theo khoảng cách và có thể cấu hình mức suy giảm này bằng cách thay đổi các tham số năng lượng, bán kính và độ suy giảm.

\ **Lưu ý:** Khi sử dụng phương thức kết xuất Mobile, mỗi mesh resource chỉ có thể hiển thị 8 omni light. Việc cố gắng hiển thị hơn 8 omni light trên một mesh resource sẽ khiến các omni light liên tục nhấp nháy khi camera di chuyển. Khi sử dụng phương thức kết xuất Compatibility, theo mặc định mỗi mesh resource chỉ có thể hiển thị 8 omni light, nhưng có thể tăng giới hạn này bằng cách điều chỉnh :ref:`ProjectSettings.rendering/limits/opengl/max_lights_per_object<class_ProjectSettings_property_rendering/limits/opengl/max_lights_per_object>`.

\ **Lưu ý:** Khi sử dụng phương thức kết xuất Mobile hoặc Compatibility, omni light sẽ chỉ tác động chính xác đến các mesh có visibility AABB giao với AABB của light. Nếu sử dụng shader để biến dạng mesh theo cách khiến mesh nằm ngoài AABB của nó, phải tăng :ref:`GeometryInstance3D.extra_cull_margin<class_GeometryInstance3D_property_extra_cull_margin>` trên mesh. Nếu không, light có thể không hiển thị trên mesh.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D lights and shadows <../tutorials/3d/lights_and_shadows.html#omni-light>`__

- :doc:`Giả lập global illumination <../tutorials/3d/global_illumination/faking_global_illumination>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +------------------------------------------------+----------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                      | light_specular                                                       | ``0.5`` (overrides :ref:`Light3D<class_Light3D_property_light_specular>`)     |
   +------------------------------------------------+----------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                      | :ref:`omni_attenuation<class_OmniLight3D_property_omni_attenuation>` | ``1.0``                                                                       |
   +------------------------------------------------+----------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                      | :ref:`omni_range<class_OmniLight3D_property_omni_range>`             | ``5.0``                                                                       |
   +------------------------------------------------+----------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`ShadowMode<enum_OmniLight3D_ShadowMode>` | :ref:`omni_shadow_mode<class_OmniLight3D_property_omni_shadow_mode>` | ``1``                                                                         |
   +------------------------------------------------+----------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                      | shadow_normal_bias                                                   | ``1.0`` (overrides :ref:`Light3D<class_Light3D_property_shadow_normal_bias>`) |
   +------------------------------------------------+----------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_OmniLight3D_ShadowMode:

.. rst-class:: classref-enumeration

enum **ShadowMode**: :ref:`🔗<enum_OmniLight3D_ShadowMode>`

.. _class_OmniLight3D_constant_SHADOW_DUAL_PARABOLOID:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowMode<enum_OmniLight3D_ShadowMode>` **SHADOW_DUAL_PARABOLOID** = ``0``

Bóng được kết xuất vào texture dual-paraboloid. Nhanh hơn :ref:`SHADOW_CUBE<class_OmniLight3D_constant_SHADOW_CUBE>`, nhưng chất lượng thấp hơn.

.. _class_OmniLight3D_constant_SHADOW_CUBE:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowMode<enum_OmniLight3D_ShadowMode>` **SHADOW_CUBE** = ``1``

Bóng được kết xuất vào cubemap. Chậm hơn :ref:`SHADOW_DUAL_PARABOLOID<class_OmniLight3D_constant_SHADOW_DUAL_PARABOLOID>`, nhưng chất lượng cao hơn.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OmniLight3D_property_omni_attenuation:

.. rst-class:: classref-property

:ref:`float<class_float>` **omni_attenuation** = ``1.0`` :ref:`🔗<class_OmniLight3D_property_omni_attenuation>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Điều khiển hàm suy giảm theo khoảng cách cho omnilight.

Giá trị ``0.0`` sẽ duy trì độ sáng không đổi trong phần lớn phạm vi, nhưng làm ánh sáng suy giảm một cách mượt mà ở rìa phạm vi. Sử dụng giá trị ``2.0`` cho ánh sáng chính xác về mặt vật lý, vì giá trị này tạo ra mức suy giảm theo đúng quy luật nghịch đảo bình phương.

\ **Lưu ý:** Việc đặt độ suy giảm thành ``2.0`` hoặc cao hơn có thể khiến các vật thể ở xa chỉ nhận được lượng ánh sáng tối thiểu, ngay cả khi vẫn nằm trong phạm vi. Ví dụ, với phạm vi ``4096``, một vật thể ở cách ``100`` đơn vị sẽ bị suy giảm theo hệ số ``0.0001``. Với độ sáng mặc định là ``1``, ánh sáng sẽ không thể nhìn thấy ở khoảng cách đó.

\ **Lưu ý:** Việc sử dụng giá trị âm hoặc giá trị cao hơn ``10.0`` có thể dẫn đến kết quả không mong muốn.

.. rst-class:: classref-item-separator

----

.. _class_OmniLight3D_property_omni_range:

.. rst-class:: classref-property

:ref:`float<class_float>` **omni_range** = ``5.0`` :ref:`🔗<class_OmniLight3D_property_omni_range>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Bán kính của light. Lưu ý rằng vùng được chiếu sáng trên thực tế có thể trông nhỏ hơn tùy thuộc vào :ref:`omni_attenuation<class_OmniLight3D_property_omni_attenuation>` đang được sử dụng. Bất kể :ref:`omni_attenuation<class_OmniLight3D_property_omni_attenuation>` đang được sử dụng là gì, light sẽ không bao giờ chiếu tới bất kỳ thứ gì nằm ngoài bán kính này.

\ **Lưu ý:** :ref:`omni_range<class_OmniLight3D_property_omni_range>` không bị ảnh hưởng bởi :ref:`Node3D.scale<class_Node3D_property_scale>` (scale của light hoặc scale của parent của nó).

.. rst-class:: classref-item-separator

----

.. _class_OmniLight3D_property_omni_shadow_mode:

.. rst-class:: classref-property

:ref:`ShadowMode<enum_OmniLight3D_ShadowMode>` **omni_shadow_mode** = ``1`` :ref:`🔗<class_OmniLight3D_property_omni_shadow_mode>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_mode**\ (\ value\: :ref:`ShadowMode<enum_OmniLight3D_ShadowMode>`\ ) - :ref:`ShadowMode<enum_OmniLight3D_ShadowMode>` **get_shadow_mode**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Vui lòng giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
