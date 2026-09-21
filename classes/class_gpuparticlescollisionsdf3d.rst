:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/GPUParticlesCollisionSDF3D.xml.

.. _class_GPUParticlesCollisionSDF3D:

GPUParticlesCollisionSDF3D
==========================

**Kế thừa:** :ref:`GPUParticlesCollision3D<class_GPUParticlesCollision3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một hình dạng va chạm hạt 3D sử dụng trường khoảng cách có dấu đã bake, ảnh hưởng đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hình dạng va chạm hạt 3D sử dụng trường khoảng cách có dấu đã bake, ảnh hưởng đến các node :ref:`GPUParticles3D<class_GPUParticles3D>`.

Các trường khoảng cách có dấu (SDF) cho phép biểu diễn hiệu quả các hình dạng va chạm gần đúng cho các đối tượng lồi và lõm với mọi hình dạng. Cách này linh hoạt hơn :ref:`GPUParticlesCollisionHeightField3D<class_GPUParticlesCollisionHeightField3D>`, nhưng yêu cầu một bước baking.

\ **Baking:** Có thể bake texture trường khoảng cách có dấu bằng cách chọn node **GPUParticlesCollisionSDF3D** trong editor, sau đó nhấp vào **Bake SDF** ở phía trên viewport 3D. Mọi :ref:`MeshInstance3D<class_MeshInstance3D>`\ *hiển thị* bên trong :ref:`size<class_GPUParticlesCollisionSDF3D_property_size>` sẽ được tính đến khi baking, bất kể :ref:`GeometryInstance3D.gi_mode<class_GeometryInstance3D_property_gi_mode>` của chúng.

\ **Lưu ý:** Chỉ có thể bake :ref:`texture<class_GPUParticlesCollisionSDF3D_property_texture>` của **GPUParticlesCollisionSDF3D** trong editor, vì không có phương thức bake nào được cung cấp để sử dụng trong các project đã export. Tuy nhiên, vẫn có thể tải :ref:`Texture3D<class_Texture3D>`\ đã bake sẵn vào thuộc tính :ref:`texture<class_GPUParticlesCollisionSDF3D_property_texture>` của nó trong project đã export.

\ **Lưu ý:** :ref:`ParticleProcessMaterial.collision_mode<class_ParticleProcessMaterial_property_collision_mode>` phải là :ref:`ParticleProcessMaterial.COLLISION_RIGID<class_ParticleProcessMaterial_constant_COLLISION_RIGID>` hoặc :ref:`ParticleProcessMaterial.COLLISION_HIDE_ON_CONTACT<class_ParticleProcessMaterial_constant_COLLISION_HIDE_ON_CONTACT>` trên process material của :ref:`GPUParticles3D<class_GPUParticles3D>` để va chạm hoạt động.

\ **Lưu ý:** Va chạm hạt chỉ ảnh hưởng đến :ref:`GPUParticles3D<class_GPUParticles3D>`, không ảnh hưởng đến :ref:`CPUParticles3D<class_CPUParticles3D>`.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------------------+-------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`                                         | :ref:`bake_mask<class_GPUParticlesCollisionSDF3D_property_bake_mask>`   | ``4294967295``       |
   +---------------------------------------------------------------+-------------------------------------------------------------------------+----------------------+
   | :ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` | :ref:`resolution<class_GPUParticlesCollisionSDF3D_property_resolution>` | ``2``                |
   +---------------------------------------------------------------+-------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>`                                 | :ref:`size<class_GPUParticlesCollisionSDF3D_property_size>`             | ``Vector3(2, 2, 2)`` |
   +---------------------------------------------------------------+-------------------------------------------------------------------------+----------------------+
   | :ref:`Texture3D<class_Texture3D>`                             | :ref:`texture<class_GPUParticlesCollisionSDF3D_property_texture>`       |                      |
   +---------------------------------------------------------------+-------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`                                     | :ref:`thickness<class_GPUParticlesCollisionSDF3D_property_thickness>`   | ``1.0``              |
   +---------------------------------------------------------------+-------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_bake_mask_value<class_GPUParticlesCollisionSDF3D_method_get_bake_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`\ ) |const|                          |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_bake_mask_value<class_GPUParticlesCollisionSDF3D_method_set_bake_mask_value>`\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) |
   +-------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_GPUParticlesCollisionSDF3D_Resolution:

.. rst-class:: classref-enumeration

enum **Resolution**: :ref:`🔗<enum_GPUParticlesCollisionSDF3D_Resolution>`

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_16:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_16** = ``0``

Bake trường khoảng cách có dấu 16×16×16. Đây là tùy chọn nhanh nhất nhưng cũng kém chính xác nhất.

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_32:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_32** = ``1``

Bake trường khoảng cách có dấu 32×32×32.

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_64:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_64** = ``2``

Bake trường khoảng cách có dấu 64×64×64.

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_128:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_128** = ``3``

Bake trường khoảng cách có dấu 128×128×128.

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_256:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_256** = ``4``

Bake trường khoảng cách có dấu 256×256×256.

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_512:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_512** = ``5``

Bake trường khoảng cách có dấu 512×512×512. Đây là tùy chọn chậm nhất nhưng cũng chính xác nhất.

.. _class_GPUParticlesCollisionSDF3D_constant_RESOLUTION_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **RESOLUTION_MAX** = ``6``

Biểu thị kích thước của enum :ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GPUParticlesCollisionSDF3D_property_bake_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **bake_mask** = ``4294967295`` :ref:`🔗<class_GPUParticlesCollisionSDF3D_property_bake_mask>`

.. rst-class:: classref-property-setget

- |void| **set_bake_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_bake_mask**\ (\ )

Các layer hình ảnh cần tính đến khi baking SDF va chạm hạt. Chỉ những :ref:`MeshInstance3D<class_MeshInstance3D>`\ có :ref:`VisualInstance3D.layers<class_VisualInstance3D_property_layers>` khớp với :ref:`bake_mask<class_GPUParticlesCollisionSDF3D_property_bake_mask>` này mới được đưa vào SDF va chạm hạt được tạo. Theo mặc định, tất cả đối tượng đều được tính đến khi baking SDF va chạm hạt.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionSDF3D_property_resolution:

.. rst-class:: classref-property

:ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **resolution** = ``2`` :ref:`🔗<class_GPUParticlesCollisionSDF3D_property_resolution>`

.. rst-class:: classref-property-setget

- |void| **set_resolution**\ (\ value\: :ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>`\ ) - :ref:`Resolution<enum_GPUParticlesCollisionSDF3D_Resolution>` **get_resolution**\ (\ )

Độ phân giải baking được sử dụng cho :ref:`texture<class_GPUParticlesCollisionSDF3D_property_texture>` của trường khoảng cách có dấu. Phải bake lại texture để các thay đổi đối với thuộc tính :ref:`resolution<class_GPUParticlesCollisionSDF3D_property_resolution>` có hiệu lực. Độ phân giải cao hơn có chi phí hiệu năng lớn hơn và mất nhiều thời gian baking hơn. Độ phân giải cao hơn cũng tạo ra texture đã bake lớn hơn, dẫn đến nhu cầu VRAM và dung lượng lưu trữ tăng lên. Để cải thiện hiệu năng và giảm thời gian baking, hãy sử dụng độ phân giải thấp nhất có thể cho đối tượng mà bạn đang biểu diễn va chạm.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionSDF3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(2, 2, 2)`` :ref:`🔗<class_GPUParticlesCollisionSDF3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Kích thước của SDF va chạm theo đơn vị 3D. Để cải thiện chất lượng SDF, nên đặt :ref:`size<class_GPUParticlesCollisionSDF3D_property_size>` nhỏ nhất có thể nhưng vẫn bao phủ các phần của scene mà bạn cần.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionSDF3D_property_texture:

.. rst-class:: classref-property

:ref:`Texture3D<class_Texture3D>` **texture** :ref:`🔗<class_GPUParticlesCollisionSDF3D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture3D<class_Texture3D>`\ ) - :ref:`Texture3D<class_Texture3D>` **get_texture**\ (\ )

Texture 3D biểu diễn trường khoảng cách có dấu.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionSDF3D_property_thickness:

.. rst-class:: classref-property

:ref:`float<class_float>` **thickness** = ``1.0`` :ref:`🔗<class_GPUParticlesCollisionSDF3D_property_thickness>`

.. rst-class:: classref-property-setget

- |void| **set_thickness**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_thickness**\ (\ )

Độ dày của hình dạng va chạm. Không giống các collider hạt khác, **GPUParticlesCollisionSDF3D** thực sự rỗng ở bên trong. Có thể tăng :ref:`thickness<class_GPUParticlesCollisionSDF3D_property_thickness>` để ngăn các hạt xuyên qua hình dạng va chạm ở tốc độ cao hoặc khi **GPUParticlesCollisionSDF3D** được di chuyển.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_GPUParticlesCollisionSDF3D_method_get_bake_mask_value:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_bake_mask_value**\ (\ layer_number\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_GPUParticlesCollisionSDF3D_method_get_bake_mask_value>`

Trả về việc layer được chỉ định của :ref:`bake_mask<class_GPUParticlesCollisionSDF3D_property_bake_mask>` có được bật hay không, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. rst-class:: classref-item-separator

----

.. _class_GPUParticlesCollisionSDF3D_method_set_bake_mask_value:

.. rst-class:: classref-method

|void| **set_bake_mask_value**\ (\ layer_number\: :ref:`int<class_int>`, value\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_GPUParticlesCollisionSDF3D_method_set_bake_mask_value>`

Dựa trên ``value``, bật hoặc tắt layer được chỉ định trong :ref:`bake_mask<class_GPUParticlesCollisionSDF3D_property_bake_mask>`, với ``layer_number`` nằm trong khoảng từ 1 đến 32.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
