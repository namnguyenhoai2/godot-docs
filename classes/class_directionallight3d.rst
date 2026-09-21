:github_url: hide

.. meta::
	:keywords: sun

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/DirectionalLight3D.xml.

.. _class_DirectionalLight3D:

DirectionalLight3D
==================

**Kế thừa:** :ref:`Light3D<class_Light3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Đèn định hướng từ xa, chẳng hạn như ánh sáng Mặt Trời.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đèn định hướng là một loại node :ref:`Light3D<class_Light3D>` mô phỏng vô số tia sáng song song bao phủ toàn bộ scene. Nó được dùng cho các đèn có cường độ mạnh nằm cách xa scene để mô phỏng ánh sáng mặt trời hoặc ánh trăng.

Ánh sáng được phát ra theo hướng -Z trong basis toàn cục của node. Đối với một đèn chưa xoay, điều này có nghĩa là ánh sáng được phát ra về phía trước, chiếu sáng mặt trước của một mô hình 3D (xem :ref:`Vector3.FORWARD<class_Vector3_constant_FORWARD>` và :ref:`Vector3.MODEL_FRONT<class_Vector3_constant_MODEL_FRONT>`). Vị trí của node bị bỏ qua; chỉ basis được sử dụng để xác định hướng ánh sáng.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D lights and shadows <../tutorials/3d/lights_and_shadows.html#directional-light>`__

- :doc:`Giả lập global illumination <../tutorials/3d/global_illumination/faking_global_illumination>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                               | :ref:`directional_shadow_blend_splits<class_DirectionalLight3D_property_directional_shadow_blend_splits>` | ``false`` |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`directional_shadow_fade_start<class_DirectionalLight3D_property_directional_shadow_fade_start>`     | ``0.8``   |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>` | ``100.0`` |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>` | :ref:`directional_shadow_mode<class_DirectionalLight3D_property_directional_shadow_mode>`                 | ``2``     |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`directional_shadow_pancake_size<class_DirectionalLight3D_property_directional_shadow_pancake_size>` | ``20.0``  |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`directional_shadow_split_1<class_DirectionalLight3D_property_directional_shadow_split_1>`           | ``0.1``   |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`directional_shadow_split_2<class_DirectionalLight3D_property_directional_shadow_split_2>`           | ``0.2``   |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`                             | :ref:`directional_shadow_split_3<class_DirectionalLight3D_property_directional_shadow_split_3>`           | ``0.5``   |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+
   | :ref:`SkyMode<enum_DirectionalLight3D_SkyMode>`       | :ref:`sky_mode<class_DirectionalLight3D_property_sky_mode>`                                               | ``0``     |
   +-------------------------------------------------------+-----------------------------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_DirectionalLight3D_ShadowMode:

.. rst-class:: classref-enumeration

enum **ShadowMode**: :ref:`🔗<enum_DirectionalLight3D_ShadowMode>`

.. _class_DirectionalLight3D_constant_SHADOW_ORTHOGONAL:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>` **SHADOW_ORTHOGONAL** = ``0``

Render shadow map của toàn bộ scene từ góc nhìn trực giao. Đây là chế độ directional shadow nhanh nhất. Có thể khiến bóng của các vật thể ở gần bị mờ hơn.

.. _class_DirectionalLight3D_constant_SHADOW_PARALLEL_2_SPLITS:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>` **SHADOW_PARALLEL_2_SPLITS** = ``1``

Chia view frustum thành 2 vùng, mỗi vùng có shadow map riêng. Chế độ shadow này là sự thỏa hiệp giữa :ref:`SHADOW_ORTHOGONAL<class_DirectionalLight3D_constant_SHADOW_ORTHOGONAL>` và :ref:`SHADOW_PARALLEL_4_SPLITS<class_DirectionalLight3D_constant_SHADOW_PARALLEL_4_SPLITS>` về hiệu năng.

.. _class_DirectionalLight3D_constant_SHADOW_PARALLEL_4_SPLITS:

.. rst-class:: classref-enumeration-constant

:ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>` **SHADOW_PARALLEL_4_SPLITS** = ``2``

Chia view frustum thành 4 vùng, mỗi vùng có shadow map riêng. Đây là chế độ directional shadow chậm nhất.

.. rst-class:: classref-item-separator

----

.. _enum_DirectionalLight3D_SkyMode:

.. rst-class:: classref-enumeration

enum **SkyMode**: :ref:`🔗<enum_DirectionalLight3D_SkyMode>`

.. _class_DirectionalLight3D_constant_SKY_MODE_LIGHT_AND_SKY:

.. rst-class:: classref-enumeration-constant

:ref:`SkyMode<enum_DirectionalLight3D_SkyMode>` **SKY_MODE_LIGHT_AND_SKY** = ``0``

Khiến ánh sáng hiển thị trong cả lighting của scene và việc render sky.

.. _class_DirectionalLight3D_constant_SKY_MODE_LIGHT_ONLY:

.. rst-class:: classref-enumeration-constant

:ref:`SkyMode<enum_DirectionalLight3D_SkyMode>` **SKY_MODE_LIGHT_ONLY** = ``1``

Khiến ánh sáng chỉ hiển thị trong lighting của scene (bao gồm direct lighting và global illumination). Khi sử dụng chế độ này, ánh sáng sẽ không hiển thị từ các sky shader.

.. _class_DirectionalLight3D_constant_SKY_MODE_SKY_ONLY:

.. rst-class:: classref-enumeration-constant

:ref:`SkyMode<enum_DirectionalLight3D_SkyMode>` **SKY_MODE_SKY_ONLY** = ``2``

Khiến ánh sáng chỉ hiển thị với các sky shader. Khi sử dụng chế độ này, ánh sáng sẽ không chiếu sáng vào scene (dù thông qua direct lighting hay global illumination), nhưng có thể được truy cập thông qua các sky shader. Chế độ này có thể hữu ích, chẳng hạn khi bạn muốn điều khiển các hiệu ứng sky mà không chiếu sáng scene (ví dụ trong một chu kỳ ban đêm).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_DirectionalLight3D_property_directional_shadow_blend_splits:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **directional_shadow_blend_splits** = ``false`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_blend_splits>`

.. rst-class:: classref-property-setget

- |void| **set_blend_splits**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_blend_splits_enabled**\ (\ )

Nếu ``true``, độ chi tiết của bóng sẽ bị giảm để đổi lấy các chuyển tiếp mượt hơn giữa các vùng chia. Bật blend splitting cho shadow cũng gây tốn hiệu năng ở mức vừa phải. Điều này bị bỏ qua khi :ref:`directional_shadow_mode<class_DirectionalLight3D_property_directional_shadow_mode>` là :ref:`SHADOW_ORTHOGONAL<class_DirectionalLight3D_constant_SHADOW_ORTHOGONAL>`.

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_fade_start:

.. rst-class:: classref-property

:ref:`float<class_float>` **directional_shadow_fade_start** = ``0.8`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_fade_start>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Tỷ lệ của :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>` tại đó bóng bắt đầu mờ dần. Tại :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>`, bóng sẽ biến mất. Giá trị mặc định là sự cân bằng giữa việc mờ dần mượt mà và khả năng hiển thị bóng ở xa. Nếu camera di chuyển nhanh và :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>` thấp, hãy cân nhắc giảm :ref:`directional_shadow_fade_start<class_DirectionalLight3D_property_directional_shadow_fade_start>` xuống dưới ``0.8`` để làm cho các chuyển tiếp của bóng ít замет hơn. Mặt khác, nếu bạn đã điều chỉnh :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>` để bao phủ toàn bộ scene, bạn có thể đặt :ref:`directional_shadow_fade_start<class_DirectionalLight3D_property_directional_shadow_fade_start>` thành ``1.0`` để ngăn bóng mờ dần ở khoảng cách xa (thay vào đó, bóng sẽ bị cắt đột ngột).

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **directional_shadow_max_distance** = ``100.0`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Khoảng cách tối đa của các vùng chia bóng. Tăng giá trị này sẽ khiến directional shadow hiển thị từ xa hơn, đổi lại là độ chi tiết tổng thể của bóng và hiệu năng thấp hơn (vì cần đưa nhiều vật thể hơn vào quá trình render directional shadow).

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_mode:

.. rst-class:: classref-property

:ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>` **directional_shadow_mode** = ``2`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_mode>`

.. rst-class:: classref-property-setget

- |void| **set_shadow_mode**\ (\ value\: :ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>`\ ) - :ref:`ShadowMode<enum_DirectionalLight3D_ShadowMode>` **get_shadow_mode**\ (\ )

Thuật toán render bóng của đèn.

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_pancake_size:

.. rst-class:: classref-property

:ref:`float<class_float>` **directional_shadow_pancake_size** = ``20.0`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_pancake_size>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Đặt kích thước của directional shadow pancake. Pancake dịch điểm bắt đầu của camera frustum của bóng để cung cấp độ phân giải độ sâu hiệu dụng cao hơn cho bóng. Tuy nhiên, kích thước pancake lớn có thể gây ra lỗi hiển thị trong bóng của các vật thể lớn nằm gần mép frustum. Giảm kích thước pancake có thể giúp khắc phục. Đặt kích thước thành ``0`` sẽ tắt hiệu ứng pancaking.

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_split_1:

.. rst-class:: classref-property

:ref:`float<class_float>` **directional_shadow_split_1** = ``0.1`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_split_1>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Khoảng cách từ camera đến vùng chia bóng 1. Tính tương đối so với :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>`. Chỉ được sử dụng khi :ref:`directional_shadow_mode<class_DirectionalLight3D_property_directional_shadow_mode>` là :ref:`SHADOW_PARALLEL_2_SPLITS<class_DirectionalLight3D_constant_SHADOW_PARALLEL_2_SPLITS>` hoặc :ref:`SHADOW_PARALLEL_4_SPLITS<class_DirectionalLight3D_constant_SHADOW_PARALLEL_4_SPLITS>`.

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_split_2:

.. rst-class:: classref-property

:ref:`float<class_float>` **directional_shadow_split_2** = ``0.2`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_split_2>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Khoảng cách từ vùng chia bóng 1 đến vùng chia 2. Tính tương đối so với :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>`. Chỉ được sử dụng khi :ref:`directional_shadow_mode<class_DirectionalLight3D_property_directional_shadow_mode>` là :ref:`SHADOW_PARALLEL_4_SPLITS<class_DirectionalLight3D_constant_SHADOW_PARALLEL_4_SPLITS>`.

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_directional_shadow_split_3:

.. rst-class:: classref-property

:ref:`float<class_float>` **directional_shadow_split_3** = ``0.5`` :ref:`🔗<class_DirectionalLight3D_property_directional_shadow_split_3>`

.. rst-class:: classref-property-setget

- |void| **set_param**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_param**\ (\ )

Khoảng cách từ vùng chia bóng 2 đến vùng chia 3. Tính tương đối so với :ref:`directional_shadow_max_distance<class_DirectionalLight3D_property_directional_shadow_max_distance>`. Chỉ được sử dụng khi :ref:`directional_shadow_mode<class_DirectionalLight3D_property_directional_shadow_mode>` là :ref:`SHADOW_PARALLEL_4_SPLITS<class_DirectionalLight3D_constant_SHADOW_PARALLEL_4_SPLITS>`.

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight3D_property_sky_mode:

.. rst-class:: classref-property

:ref:`SkyMode<enum_DirectionalLight3D_SkyMode>` **sky_mode** = ``0`` :ref:`🔗<class_DirectionalLight3D_property_sky_mode>`

.. rst-class:: classref-property-setget

- |void| **set_sky_mode**\ (\ value\: :ref:`SkyMode<enum_DirectionalLight3D_SkyMode>`\ ) - :ref:`SkyMode<enum_DirectionalLight3D_SkyMode>` **get_sky_mode**\ (\ )

**DirectionalLight3D** này có hiển thị trong sky, trong scene, hay cả trong sky và scene hay không.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
