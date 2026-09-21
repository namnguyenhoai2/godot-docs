:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGSphere3D.xml.

.. _class_CSGSphere3D:

CSGSphere3D
===========

**Kế thừa:** :ref:`CSGPrimitive3D<class_CSGPrimitive3D>` **<** :ref:`CSGShape3D<class_CSGShape3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một hình cầu CSG.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này cho phép bạn tạo một hình cầu để sử dụng với hệ thống CSG.

\ **Lưu ý:** Các node CSG được dùng để dựng nguyên mẫu level. Việc tạo các node CSG có chi phí CPU đáng kể so với việc tạo một :ref:`MeshInstance3D<class_MeshInstance3D>` với một :ref:`PrimitiveMesh<class_PrimitiveMesh>`. Việc di chuyển một node CSG bên trong một node CSG khác cũng có chi phí CPU đáng kể, vì vậy nên tránh thực hiện việc này trong quá trình chơi.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Tạo nguyên mẫu level bằng CSG <../tutorials/3d/csg_tools>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+--------------------------------------------------------------------+----------+
   | :ref:`Material<class_Material>` | :ref:`material<class_CSGSphere3D_property_material>`               |          |
   +---------------------------------+--------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`           | :ref:`radial_segments<class_CSGSphere3D_property_radial_segments>` | ``12``   |
   +---------------------------------+--------------------------------------------------------------------+----------+
   | :ref:`float<class_float>`       | :ref:`radius<class_CSGSphere3D_property_radius>`                   | ``0.5``  |
   +---------------------------------+--------------------------------------------------------------------+----------+
   | :ref:`int<class_int>`           | :ref:`rings<class_CSGSphere3D_property_rings>`                     | ``6``    |
   +---------------------------------+--------------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`         | :ref:`smooth_faces<class_CSGSphere3D_property_smooth_faces>`       | ``true`` |
   +---------------------------------+--------------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CSGSphere3D_property_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material** :ref:`🔗<class_CSGSphere3D_property_material>`

.. rst-class:: classref-property-setget

- |void| **set_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material**\ (\ )

Material được sử dụng để render hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_CSGSphere3D_property_radial_segments:

.. rst-class:: classref-property

:ref:`int<class_int>` **radial_segments** = ``12`` :ref:`🔗<class_CSGSphere3D_property_radial_segments>`

.. rst-class:: classref-property-setget

- |void| **set_radial_segments**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_radial_segments**\ (\ )

Số lượng lát cắt dọc của hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_CSGSphere3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.5`` :ref:`🔗<class_CSGSphere3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_CSGSphere3D_property_rings:

.. rst-class:: classref-property

:ref:`int<class_int>` **rings** = ``6`` :ref:`🔗<class_CSGSphere3D_property_rings>`

.. rst-class:: classref-property-setget

- |void| **set_rings**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_rings**\ (\ )

Số lượng lát cắt ngang của hình cầu.

.. rst-class:: classref-item-separator

----

.. _class_CSGSphere3D_property_smooth_faces:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **smooth_faces** = ``true`` :ref:`🔗<class_CSGSphere3D_property_smooth_faces>`

.. rst-class:: classref-property-setget

- |void| **set_smooth_faces**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_smooth_faces**\ (\ )

Nếu ``true``, các pháp tuyến của hình cầu được thiết lập để tạo hiệu ứng mượt, khiến hình cầu trông bo tròn. Nếu ``false``, hình cầu sẽ có vẻ ngoài được tô bóng phẳng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
