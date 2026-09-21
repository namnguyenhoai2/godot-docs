:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CanvasTexture.xml.

.. _class_CanvasTexture:

CanvasTexture
=============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture với các normal map và specular map tùy chọn để sử dụng trong kết xuất 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CanvasTexture** là một lựa chọn thay thế cho :ref:`ImageTexture<class_ImageTexture>` trong kết xuất 2D. Nó cho phép sử dụng normal map và specular map trong bất kỳ node nào kế thừa từ :ref:`CanvasItem<class_CanvasItem>`. **CanvasTexture** cũng cho phép ghi đè filter và repeat mode của texture một cách độc lập với các thuộc tính của node (hoặc thiết lập của project).

\ **Lưu ý:** Không thể sử dụng **CanvasTexture** trong 3D. Nó sẽ không hiển thị chính xác khi được áp dụng cho bất kỳ :ref:`VisualInstance3D<class_VisualInstance3D>` nào, chẳng hạn như :ref:`Sprite3D<class_Sprite3D>` hoặc :ref:`Decal<class_Decal>`. Đối với vật liệu dựa trên cơ sở vật lý trong 3D, hãy sử dụng :ref:`BaseMaterial3D<class_BaseMaterial3D>` thay thế.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`2D Lights and Shadows <../tutorials/2d/2d_lights_and_shadows>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`                   | :ref:`diffuse_texture<class_CanvasTexture_property_diffuse_texture>`       |                                                                                        |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`                   | :ref:`normal_texture<class_CanvasTexture_property_normal_texture>`         |                                                                                        |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                             | resource_local_to_scene                                                    | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`                           | :ref:`specular_color<class_CanvasTexture_property_specular_color>`         | ``Color(1, 1, 1, 1)``                                                                  |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`specular_shininess<class_CanvasTexture_property_specular_shininess>` | ``1.0``                                                                                |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>`                   | :ref:`specular_texture<class_CanvasTexture_property_specular_texture>`     |                                                                                        |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`TextureFilter<enum_CanvasItem_TextureFilter>` | :ref:`texture_filter<class_CanvasTexture_property_texture_filter>`         | ``0``                                                                                  |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`TextureRepeat<enum_CanvasItem_TextureRepeat>` | :ref:`texture_repeat<class_CanvasTexture_property_texture_repeat>`         | ``0``                                                                                  |
   +-----------------------------------------------------+----------------------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CanvasTexture_property_diffuse_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **diffuse_texture** :ref:`🔗<class_CanvasTexture_property_diffuse_texture>`

.. rst-class:: classref-property-setget

- |void| **set_diffuse_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_diffuse_texture**\ (\ )

Texture diffuse (màu sắc) cần sử dụng. Đây là texture chính mà bạn muốn thiết lập trong hầu hết các trường hợp.

.. rst-class:: classref-item-separator

----

.. _class_CanvasTexture_property_normal_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **normal_texture** :ref:`🔗<class_CanvasTexture_property_normal_texture>`

.. rst-class:: classref-property-setget

- |void| **set_normal_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_normal_texture**\ (\ )

The normal map texture to use. Only has a visible effect if :ref:`Light2D<class_Light2D>`\ s are affecting this **CanvasTexture**.

\ **Lưu ý:** Godot yêu cầu normal map sử dụng các tọa độ X+, Y+ và Z+. Xem `this page <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details#Common_Swizzle_Coordinates>`__ để so sánh các tọa độ normal map được các engine phổ biến yêu cầu.

.. rst-class:: classref-item-separator

----

.. _class_CanvasTexture_property_specular_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **specular_color** = ``Color(1, 1, 1, 1)`` :ref:`🔗<class_CanvasTexture_property_specular_color>`

.. rst-class:: classref-property-setget

- |void| **set_specular_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_specular_color**\ (\ )

The multiplier for specular reflection colors. The :ref:`Light2D<class_Light2D>`'s color is also taken into account when determining the reflection color. Only has a visible effect if :ref:`Light2D<class_Light2D>`\ s are affecting this **CanvasTexture**.

.. rst-class:: classref-item-separator

----

.. _class_CanvasTexture_property_specular_shininess:

.. rst-class:: classref-property

:ref:`float<class_float>` **specular_shininess** = ``1.0`` :ref:`🔗<class_CanvasTexture_property_specular_shininess>`

.. rst-class:: classref-property-setget

- |void| **set_specular_shininess**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_specular_shininess**\ (\ )

The specular exponent for :ref:`Light2D<class_Light2D>` specular reflections. Higher values result in a more glossy/"wet" look, with reflections becoming more localized and less visible overall. The default value of ``1.0`` disables specular reflections entirely. Only has a visible effect if :ref:`Light2D<class_Light2D>`\ s are affecting this **CanvasTexture**.

.. rst-class:: classref-item-separator

----

.. _class_CanvasTexture_property_specular_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **specular_texture** :ref:`🔗<class_CanvasTexture_property_specular_texture>`

.. rst-class:: classref-property-setget

- |void| **set_specular_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_specular_texture**\ (\ )

The specular map to use for :ref:`Light2D<class_Light2D>` specular reflections. This should be a grayscale or colored texture, with brighter areas resulting in a higher :ref:`specular_shininess<class_CanvasTexture_property_specular_shininess>` value. Using a colored :ref:`specular_texture<class_CanvasTexture_property_specular_texture>` allows controlling specular shininess on a per-channel basis. Only has a visible effect if :ref:`Light2D<class_Light2D>`\ s are affecting this **CanvasTexture**.

.. rst-class:: classref-item-separator

----

.. _class_CanvasTexture_property_texture_filter:

.. rst-class:: classref-property

:ref:`TextureFilter<enum_CanvasItem_TextureFilter>` **texture_filter** = ``0`` :ref:`🔗<class_CanvasTexture_property_texture_filter>`

.. rst-class:: classref-property-setget

- |void| **set_texture_filter**\ (\ value\: :ref:`TextureFilter<enum_CanvasItem_TextureFilter>`\ ) - :ref:`TextureFilter<enum_CanvasItem_TextureFilter>` **get_texture_filter**\ (\ )

Chế độ texture filtering cần sử dụng khi vẽ **CanvasTexture** này.

.. rst-class:: classref-item-separator

----

.. _class_CanvasTexture_property_texture_repeat:

.. rst-class:: classref-property

:ref:`TextureRepeat<enum_CanvasItem_TextureRepeat>` **texture_repeat** = ``0`` :ref:`🔗<class_CanvasTexture_property_texture_repeat>`

.. rst-class:: classref-property-setget

- |void| **set_texture_repeat**\ (\ value\: :ref:`TextureRepeat<enum_CanvasItem_TextureRepeat>`\ ) - :ref:`TextureRepeat<enum_CanvasItem_TextureRepeat>` **get_texture_repeat**\ (\ )

Chế độ texture repeat cần sử dụng khi vẽ **CanvasTexture** này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
