:github_url: hide

.. meta::
	:keywords: omni, spot

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PointLight2D.xml.

.. _class_PointLight2D:

PointLight2D
============

**Kế thừa:** :ref:`Light2D<class_Light2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Nguồn sáng 2D theo vị trí.

.. rst-class:: classref-introduction-group

Mô tả
-----

Phát ánh sáng trong môi trường 2D. Hình dạng của nguồn sáng này được xác định bởi một texture (thường là grayscale).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Đèn và bóng 2D <../tutorials/2d/2d_lights_and_shadows>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+-----------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`         | :ref:`height<class_PointLight2D_property_height>`               | ``0.0``           |
   +-----------------------------------+-----------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`     | :ref:`offset<class_PointLight2D_property_offset>`               | ``Vector2(0, 0)`` |
   +-----------------------------------+-----------------------------------------------------------------+-------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture<class_PointLight2D_property_texture>`             |                   |
   +-----------------------------------+-----------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`         | :ref:`texture_scale<class_PointLight2D_property_texture_scale>` | ``1.0``           |
   +-----------------------------------+-----------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PointLight2D_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``0.0`` :ref:`🔗<class_PointLight2D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Chiều cao của nguồn sáng. Được sử dụng với normal mapping 2D. Đơn vị được tính bằng pixel; ví dụ: nếu chiều cao là 100, nguồn sáng sẽ chiếu sáng một đối tượng cách 100 pixel ở góc 45° so với mặt phẳng.

.. rst-class:: classref-item-separator

----

.. _class_PointLight2D_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_PointLight2D_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_texture_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_texture_offset**\ (\ )

Độ lệch của :ref:`texture<class_PointLight2D_property_texture>` của nguồn sáng.

.. rst-class:: classref-item-separator

----

.. _class_PointLight2D_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_PointLight2D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

:ref:`Texture2D<class_Texture2D>` được sử dụng cho diện mạo của nguồn sáng.

.. rst-class:: classref-item-separator

----

.. _class_PointLight2D_property_texture_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **texture_scale** = ``1.0`` :ref:`🔗<class_PointLight2D_property_texture_scale>`

.. rst-class:: classref-property-setget

- |void| **set_texture_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_texture_scale**\ (\ )

Hệ số scale của :ref:`texture<class_PointLight2D_property_texture>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
