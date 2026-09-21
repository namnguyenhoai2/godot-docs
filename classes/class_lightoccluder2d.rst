:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/LightOccluder2D.xml.

.. _class_LightOccluder2D:

LightOccluder2D
===============

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Che khuất ánh sáng do một Light2D phát ra, tạo bóng.

.. rst-class:: classref-introduction-group

Mô tả
-----

Che khuất ánh sáng do một Light2D phát ra, tạo bóng. LightOccluder2D phải được cung cấp một :ref:`OccluderPolygon2D<class_OccluderPolygon2D>` để có thể tính toán bóng.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Đèn và bóng 2D <../tutorials/2d/2d_lights_and_shadows>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`OccluderPolygon2D<class_OccluderPolygon2D>` | :ref:`occluder<class_LightOccluder2D_property_occluder>`                       |          |
   +---------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`                             | :ref:`occluder_light_mask<class_LightOccluder2D_property_occluder_light_mask>` | ``1``    |
   +---------------------------------------------------+--------------------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`                           | :ref:`sdf_collision<class_LightOccluder2D_property_sdf_collision>`             | ``true`` |
   +---------------------------------------------------+--------------------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_LightOccluder2D_property_occluder:

.. rst-class:: classref-property

:ref:`OccluderPolygon2D<class_OccluderPolygon2D>` **occluder** :ref:`🔗<class_LightOccluder2D_property_occluder>`

.. rst-class:: classref-property-setget

- |void| **set_occluder_polygon**\ (\ value\: :ref:`OccluderPolygon2D<class_OccluderPolygon2D>`\ ) - :ref:`OccluderPolygon2D<class_OccluderPolygon2D>` **get_occluder_polygon**\ (\ )

:ref:`OccluderPolygon2D<class_OccluderPolygon2D>` được dùng để tính toán bóng.

.. rst-class:: classref-item-separator

----

.. _class_LightOccluder2D_property_occluder_light_mask:

.. rst-class:: classref-property

:ref:`int<class_int>` **occluder_light_mask** = ``1`` :ref:`🔗<class_LightOccluder2D_property_occluder_light_mask>`

.. rst-class:: classref-property-setget

- |void| **set_occluder_light_mask**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_occluder_light_mask**\ (\ )

Mặt nạ ánh sáng của occluder thuộc LightOccluder2D. LightOccluder2D sẽ chỉ tạo bóng từ (các) Light2D có (các) mặt nạ ánh sáng giống nhau.

.. rst-class:: classref-item-separator

----

.. _class_LightOccluder2D_property_sdf_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **sdf_collision** = ``true`` :ref:`🔗<class_LightOccluder2D_property_sdf_collision>`

.. rst-class:: classref-property-setget

- |void| **set_as_sdf_collision**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_set_as_sdf_collision**\ (\ )

Nếu được bật, occluder sẽ là một phần của signed distance field được tạo theo thời gian thực và có thể được sử dụng trong các shader tùy chỉnh.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
