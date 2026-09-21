:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesCollisionHeightField3D.xml.

.. _class_GPUParticlesCollisionHeightField3D:

GPUParticlesCollisionHeightField3D
==================================

**Kế thừa:** :ref:`GPUParticlesCollision3D<class_GPUParticlesCollision3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một collision shape 3D dạng heightmap theo thời gian thực, tác động đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một collision shape 3D dạng heightmap theo thời gian thực, tác động đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

Các shape dạng heightmap cho phép biểu diễn hiệu quả collision cho các đối tượng lồi và lõm với một "mặt sàn" duy nhất (chẳng hạn như địa hình). Cách này kém linh hoạt hơn :ref:`GPUParticlesCollisionSDF3D<class_GPUParticlesCollisionSDF3D>`, nhưng không yêu cầu bước baking.

\ **GPUParticlesCollisionHeightField3D** cũng có thể được tạo lại theo thời gian thực khi node này được di chuyển, khi camera di chuyển hoặc thậm chí liên tục. Điều này khiến **GPUParticlesCollisionHeightField3D** trở thành lựa chọn phù hợp cho các hiệu ứng thời tiết như mưa và tuyết, cũng như các game có hình học thay đổi linh động. Tuy nhiên, class này bị giới hạn vì heightmap không thể biểu diễn các phần nhô ra (ví dụ: trong nhà hoặc hang động).

\ **Lưu ý:** :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` phải được ``true`` trên process material của :ref:`GPUParticles3D<class_GPUParticles3D>` để collision hoạt động.

\ **Lưu ý:** Collision của particle chỉ tác động đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không tác động đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`                                               | :ref:`follow_camera_enabled<class_GPUParticlesCollisionHeightField3D_property_follow_camera_enabled>` | ``false``            |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                                 | :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>`           | ``1048575``          |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` | :ref:`resolution<class_GPUParticlesCollisionHeightField3D_property_resolution>`                       | ``2``                |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                                         | :ref:`size<class_GPUParticlesCollisionHeightField3D_property_size>`                                   | ``Vector3(2, 2, 2)`` |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------+
   | :ref:`UpdateMode<enum_GPUParticlesCollisionHeightField3D_UpdateMode>` | :ref:`update_mode<class_GPUParticlesCollisionHeightField3D_property_update_mode>`                     | ``0``                |
   +-----------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_heightfield_mask_value<class_GPUParticlesCollisionHeightField3D_method_get_heightfield_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_heightfield_mask_value<class_GPUParticlesCollisionHeightField3D_method_set_heightfield_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_GPUParticlesCollisionHeightField3D_Resolution:

.. rst-class:: classref-enumeration

enum **Resolution**: :ref:`🔗<enum_GPUParticlesCollisionHeightField3D_Resolution>`

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_256:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_256** = ``0``

Tạo heightmap 256×256. Dành cho các scene quy mô nhỏ hoặc các scene lớn hơn không có particle ở xa.

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_512:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_512** = ``1``

Tạo heightmap 512×512. Dành cho các scene quy mô trung bình hoặc các scene lớn hơn không có particle ở xa.

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_1024:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_1024** = ``2``

Tạo heightmap 1024×1024. Dành cho các scene lớn có particle ở xa.

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_2048:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_2048** = ``3``

Tạo heightmap 2048×2048. Dành cho các scene rất lớn có particle ở xa.

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_4096:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_4096** = ``4``

Tạo heightmap 4096×4096. Dành cho các scene khổng lồ có particle ở xa.

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_8192:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_8192** = ``5``

Tạo heightmap 8192×8192. Dành cho các scene cực kỳ khổng lồ có particle ở xa.

.. _class_GPUParticlesCollisionHeightField3D_constant_RESOLUTION_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **RESOLUTION_MAX** = ``6``

Biểu thị kích thước của enum :ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>`.

.. rst-class:: classref-item-separator

----

.. _enum_GPUParticlesCollisionHeightField3D_UpdateMode:

.. rst-class:: classref-enumeration

enum **UpdateMode**: :ref:`🔗<enum_GPUParticlesCollisionHeightField3D_UpdateMode>`

.. _class_GPUParticlesCollisionHeightField3D_constant_UPDATE_MODE_WHEN_MOVED:

.. rst-class:: classref-enumeration-constant

:ref:`UpdateMode<enum_GPUParticlesCollisionHeightField3D_UpdateMode>` **UPDATE_MODE_WHEN_MOVED** = ``0``

Chỉ cập nhật heightmap khi node **GPUParticlesCollisionHeightField3D** được di chuyển hoặc khi camera di chuyển nếu :ref:`follow_camera_enabled<class_GPUParticlesCollisionHeightField3D_property_follow_camera_enabled>` là ``true``. Có thể buộc cập nhật bằng cách di chuyển nhẹ **GPUParticlesCollisionHeightField3D** theo bất kỳ hướng nào hoặc gọi :ref:`RenderingServer.particles_collision_height_field_update()<class_RenderingServer_method_particles_collision_height_field_update>`.

.. _class_GPUParticlesCollisionHeightField3D_constant_UPDATE_MODE_ALWAYS:

.. rst-class:: classref-enumeration-constant

:ref:`UpdateMode<enum_GPUParticlesCollisionHeightField3D_UpdateMode>` **UPDATE_MODE_ALWAYS** = ``1``

Cập nhật heightmap ở mỗi frame. Việc này gây ảnh hưởng đáng kể đến hiệu năng. Chỉ nên sử dụng chế độ cập nhật này khi hình học mà particle có thể collision cùng thay đổi đáng kể trong quá trình chơi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesCollisionHeightField3D_property_follow_camera_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **follow_camera_enabled** = ``false`` :ref:`🔗<class_GPUParticlesCollisionHeightField3D_property_follow_camera_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_follow_camera_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_follow_camera_enabled**\ (\ )

Nếu ``true``, **GPUParticlesCollisionHeightField3D** sẽ theo camera hiện tại trong global space. **GPUParticlesCollisionHeightField3D** không cần là node con của node :ref:`Camera3D<class_Camera3D>` để tính năng này hoạt động.

Việc theo camera gây ảnh hưởng đến hiệu năng vì buộc heightmap phải cập nhật mỗi khi camera di chuyển. Hãy cân nhắc giảm :ref:`resolution<class_GPUParticlesCollisionHeightField3D_property_resolution>` để cải thiện hiệu năng nếu :ref:`follow_camera_enabled<class_GPUParticlesCollisionHeightField3D_property_follow_camera_enabled>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionHeightField3D_property_heightfield_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **heightfield_mask** = ``1048575`` :ref:`🔗<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>`

.. rst-class:: classref-property-setget

- |void| **set_heightfield_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_heightfield_mask**\ (\ )

Các visual layer cần được xét khi cập nhật heightmap. Chỉ các :ref:`MeshInstance3D<class_MeshInstance3D>`\ s có :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>` khớp với :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>` này mới được đưa vào bản cập nhật collision của heightmap. Theo mặc định, cả 20 layer hiển thị với người dùng đều được xét khi cập nhật collision của heightmap.

\ **Lưu ý:** Vì :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>` cho phép lưu trữ tổng cộng 32 layer, có thêm 12 layer chỉ được engine sử dụng nội bộ và không hiển thị trong editor. Việc thiết lập :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>` bằng script cho phép bạn bật hoặc tắt các layer dành riêng đó, điều này có thể hữu ích cho các editor plugin.

Để điều chỉnh :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>` dễ dàng hơn bằng script, hãy sử dụng :ref:`get_heightfield_mask_value()<class_GPUParticlesCollisionHeightField3D_method_get_heightfield_mask_value>` và :ref:`set_heightfield_mask_value()<class_GPUParticlesCollisionHeightField3D_method_set_heightfield_mask_value>`.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionHeightField3D_property_resolution:

.. rst-class:: classref-property

:ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **resolution** = ``2`` :ref:`🔗<class_GPUParticlesCollisionHeightField3D_property_resolution>`

.. rst-class:: classref-property-setget

- |void| **set_resolution**\ (\ value\: :ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>`\ ) - :ref:`Resolution<enum_GPUParticlesCollisionHeightField3D_Resolution>` **get_resolution**\ (\ )

Resolution cao hơn có thể biểu diễn các chi tiết nhỏ chính xác hơn trong các scene lớn, đổi lại hiệu năng sẽ thấp hơn. Nếu :ref:`update_mode<class_GPUParticlesCollisionHeightField3D_property_update_mode>` là :ref:`UPDATE_MODE_ALWAYS<class_GPUParticlesCollisionHeightField3D_constant_UPDATE_MODE_ALWAYS>`, hãy cân nhắc sử dụng resolution thấp nhất có thể.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionHeightField3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_GPUParticlesCollisionHeightField3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của collision heightmap theo đơn vị 3D. Để cải thiện chất lượng heightmap, :ref:`size<class_GPUParticlesCollisionHeightField3D_property_size>` nên được đặt nhỏ nhất có thể nhưng vẫn bao phủ các phần scene cần thiết.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionHeightField3D_property_update_mode:

.. rst-class:: classref-property

:ref:`UpdateMode<enum_GPUParticlesCollisionHeightField3D_UpdateMode>` **update_mode** = ``0`` :ref:`🔗<class_GPUParticlesCollisionHeightField3D_property_update_mode>`

.. rst-class:: classref-property-setget

- |void| **set_update_mode**\ (\ value\: :ref:`UpdateMode<enum_GPUParticlesCollisionHeightField3D_UpdateMode>`\ ) - :ref:`UpdateMode<enum_GPUParticlesCollisionHeightField3D_UpdateMode>` **get_update_mode**\ (\ )

Chính sách cập nhật được sử dụng cho heightmap đã tạo.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GPUParticlesCollisionHeightField3D_method_get_heightfield_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_heightfield_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GPUParticlesCollisionHeightField3D_method_get_heightfield_mask_value>`

Trả về ``true`` nếu layer được chỉ định của :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>` được bật, với ``layer_number`` nằm trong khoảng từ ``1`` đến ``20``, bao gồm cả hai giá trị.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionHeightField3D_method_set_heightfield_mask_value:

.. rst-class:: classref-method

|void| **set_heightfield_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_GPUParticlesCollisionHeightField3D_method_set_heightfield_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`heightfield_mask<class_GPUParticlesCollisionHeightField3D_property_heightfield_mask>`, với ``layer_number`` nằm trong khoảng từ ``1`` đến ``20``, bao gồm cả hai giá trị.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
