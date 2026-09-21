:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/FogMaterial.xml.

.. _class_FogMaterial:

FogMaterial
===========

**Kế thừa:** :ref:`Material<class_Material>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một material điều khiển cách fog thể tích được render, dùng để gán cho một :ref:`FogVolume<class_FogVolume>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một resource :ref:`Material<class_Material>` có thể được :ref:`FogVolume<class_FogVolume>`\ s sử dụng để vẽ các hiệu ứng thể tích.

Nếu cần các hiệu ứng nâng cao hơn, hãy sử dụng một :doc:`fog shader <../tutorials/shaders/shader_reference/fog_shader>` tùy chỉnh.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`         | :ref:`albedo<class_FogMaterial_property_albedo>`                   | ``Color(1, 1, 1, 1)`` |
   +-----------------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`density<class_FogMaterial_property_density>`                 | ``1.0``               |
   +-----------------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`Texture3D<class_Texture3D>` | :ref:`density_texture<class_FogMaterial_property_density_texture>` |                       |
   +-----------------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`edge_fade<class_FogMaterial_property_edge_fade>`             | ``0.1``               |
   +-----------------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`         | :ref:`emission<class_FogMaterial_property_emission>`               | ``Color(0, 0, 0, 1)`` |
   +-----------------------------------+--------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`         | :ref:`height_falloff<class_FogMaterial_property_height_falloff>`   | ``0.0``               |
   +-----------------------------------+--------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FogMaterial_property_albedo:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **albedo** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_FogMaterial_property_albedo>`

.. rst-class:: classref-property-setget

- |void| **set_albedo**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_albedo**\ (\ )

:ref:`Color<class_Color>` single-scattering của :ref:`FogVolume<class_FogVolume>`. Về bên trong, :ref:`albedo<class_FogMaterial_property_albedo>` được chuyển đổi thành single-scattering, sau đó được blend cộng với các :ref:`FogVolume<class_FogVolume>`\ s khác và :ref:`Environment.volumetric_fog_albedo<class_Environment_property_volumetric_fog_albedo>`.

.. rst-class:: classref-item-separator

----

.. _class_FogMaterial_property_density:

.. rst-class:: classref-property

:ref:`float<class_float>` **density** = ``1.0`` :ref:`🔗<class_FogMaterial_property_density>`

.. rst-class:: classref-property-setget

- |void| **set_density**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_density**\ (\ )

Mật độ của :ref:`FogVolume<class_FogVolume>`. Các object đặc hơn sẽ đục hơn, nhưng có thể gặp các artifact do lấy mẫu thiếu, trông giống như các sọc. Có thể dùng các giá trị âm để trừ fog khỏi các :ref:`FogVolume<class_FogVolume>`\ s khác hoặc fog thể tích toàn cục.

\ **Lưu ý:** Do độ chính xác bị giới hạn, các giá trị :ref:`density<class_FogMaterial_property_density>` nằm giữa ``-0.001`` và ``0.001`` (không bao gồm hai giá trị này) sẽ hoạt động như ``0.0``. Điều này không áp dụng cho :ref:`Environment.volumetric_fog_density<class_Environment_property_volumetric_fog_density>`.

.. rst-class:: classref-item-separator

----

.. _class_FogMaterial_property_density_texture:

.. rst-class:: classref-property

:ref:`Texture3D<class_Texture3D>` **density_texture** :ref:`🔗<class_FogMaterial_property_density_texture>`

.. rst-class:: classref-property-setget

- |void| **set_density_texture**\ (\ value\: :ref:`Texture3D<class_Texture3D>`\ ) - :ref:`Texture3D<class_Texture3D>` **get_density_texture**\ (\ )

Texture 3D được sử dụng để điều chỉnh :ref:`density<class_FogMaterial_property_density>` của :ref:`FogVolume<class_FogVolume>`. Có thể dùng texture này để thay đổi mật độ fog trong :ref:`FogVolume<class_FogVolume>` bằng bất kỳ mẫu tĩnh nào. Đối với các hiệu ứng được animate, hãy cân nhắc sử dụng một :doc:`fog shader <../tutorials/shaders/shader_reference/fog_shader>` tùy chỉnh.

.. rst-class:: classref-item-separator

----

.. _class_FogMaterial_property_edge_fade:

.. rst-class:: classref-property

:ref:`float<class_float>` **edge_fade** = ``0.1`` :ref:`🔗<class_FogMaterial_property_edge_fade>`

.. rst-class:: classref-property-setget

- |void| **set_edge_fade**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_edge_fade**\ (\ )

Độ cứng của các cạnh của :ref:`FogVolume<class_FogVolume>`. Giá trị cao hơn sẽ tạo ra các cạnh mềm hơn, trong khi giá trị thấp hơn sẽ tạo ra các cạnh cứng hơn.

.. rst-class:: classref-item-separator

----

.. _class_FogMaterial_property_emission:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **emission** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_FogMaterial_property_emission>`

.. rst-class:: classref-property-setget

- |void| **set_emission**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_emission**\ (\ )

:ref:`Color<class_Color>` của ánh sáng phát ra từ :ref:`FogVolume<class_FogVolume>`. Ánh sáng phát ra sẽ không chiếu sáng hoặc tạo bóng lên các object khác, nhưng có thể hữu ích để điều chỉnh :ref:`Color<class_Color>` của :ref:`FogVolume<class_FogVolume>` độc lập với các nguồn sáng.

.. rst-class:: classref-item-separator

----

.. _class_FogMaterial_property_height_falloff:

.. rst-class:: classref-property

:ref:`float<class_float>` **height_falloff** = ``0.0`` :ref:`🔗<class_FogMaterial_property_height_falloff>`

.. rst-class:: classref-property-setget

- |void| **set_height_falloff**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height_falloff**\ (\ )

Tốc độ giảm mật độ của fog dựa trên độ cao khi độ cao tăng trong world space. Falloff cao sẽ tạo ra sự chuyển tiếp sắc nét, trong khi falloff thấp sẽ tạo ra sự chuyển tiếp mượt mà hơn. Giá trị ``0.0`` tạo ra fog có mật độ đồng đều. Ngưỡng độ cao được xác định bởi độ cao của :ref:`FogVolume<class_FogVolume>` liên kết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
