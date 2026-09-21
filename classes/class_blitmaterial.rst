:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/BlitMaterial.xml.

.. _class_BlitMaterial:

BlitMaterial
============

**Kế thừa:** :ref:`Material<class_Material>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một material xử lý các lời gọi blit đến một DrawableTexture.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một tài nguyên material có thể được DrawableTextures sử dụng khi xử lý các lời gọi blit để vẽ.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------+-----------------------------------------------------------+-------+
   | :ref:`BlendMode<enum_BlitMaterial_BlendMode>` | :ref:`blend_mode<class_BlitMaterial_property_blend_mode>` | ``0`` |
   +-----------------------------------------------+-----------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_BlitMaterial_BlendMode:

.. rst-class:: classref-enumeration

enum **BlendMode**: :ref:`🔗<enum_BlitMaterial_BlendMode>`

.. _class_BlitMaterial_constant_BLEND_MODE_MIX:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_BlitMaterial_BlendMode>` **BLEND_MODE_MIX** = ``0``

Chế độ blending hòa trộn. Màu sắc được giả định là độc lập với giá trị alpha (độ mờ).

.. _class_BlitMaterial_constant_BLEND_MODE_ADD:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_BlitMaterial_BlendMode>` **BLEND_MODE_ADD** = ``1``

Chế độ blending cộng.

.. _class_BlitMaterial_constant_BLEND_MODE_SUB:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_BlitMaterial_BlendMode>` **BLEND_MODE_SUB** = ``2``

Chế độ blending trừ.

.. _class_BlitMaterial_constant_BLEND_MODE_MUL:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_BlitMaterial_BlendMode>` **BLEND_MODE_MUL** = ``3``

Chế độ blending nhân.

.. _class_BlitMaterial_constant_BLEND_MODE_DISABLED:

.. rst-class:: classref-enumeration-constant

:ref:`BlendMode<enum_BlitMaterial_BlendMode>` **BLEND_MODE_DISABLED** = ``4``

Không có chế độ blending, sao chép màu trực tiếp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BlitMaterial_property_blend_mode:

.. rst-class:: classref-property

:ref:`BlendMode<enum_BlitMaterial_BlendMode>` **blend_mode** = ``0`` :ref:`🔗<class_BlitMaterial_property_blend_mode>`

.. rst-class:: classref-property-setget

- |void| **set_blend_mode**\ (\ value\: :ref:`BlendMode<enum_BlitMaterial_BlendMode>`\ ) - :ref:`BlendMode<enum_BlitMaterial_BlendMode>` **get_blend_mode**\ (\ )

Cách texture vừa được blit được hòa trộn với DrawableTexture ban đầu.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
