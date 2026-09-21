:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/modules/csg/doc_classes/CSGTorus3D.xml.

.. _class_CSGTorus3D:

CSGTorus3D
==========

**Kế thừa:** :ref:`CSGPrimitive3D<class_CSGPrimitive3D>` **<** :ref:`CSGShape3D<class_CSGShape3D>` **<** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một hình xuyến CSG.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node này cho phép bạn tạo một hình xuyến để sử dụng với hệ thống CSG.

\ **Lưu ý:** Các node CSG được dùng cho việc tạo nguyên mẫu level. Việc tạo node CSG có chi phí CPU đáng kể so với việc tạo một :ref:`MeshInstance3D<class_MeshInstance3D>` với một :ref:`PrimitiveMesh<class_PrimitiveMesh>`. Việc di chuyển một node CSG bên trong một node CSG khác cũng có chi phí CPU đáng kể, vì vậy nên tránh thực hiện việc này trong quá trình gameplay.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tạo nguyên mẫu level bằng CSG <../tutorials/3d/csg_tools>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+-------------------------------------------------------------+----------+
   | :ref:`float<class_float>`       | :ref:`inner_radius<class_CSGTorus3D_property_inner_radius>` | ``0.5``  |
   +---------------------------------+-------------------------------------------------------------+----------+
   | :ref:`Material<class_Material>` | :ref:`material<class_CSGTorus3D_property_material>`         |          |
   +---------------------------------+-------------------------------------------------------------+----------+
   | :ref:`float<class_float>`       | :ref:`outer_radius<class_CSGTorus3D_property_outer_radius>` | ``1.0``  |
   +---------------------------------+-------------------------------------------------------------+----------+
   | :ref:`int<class_int>`           | :ref:`ring_sides<class_CSGTorus3D_property_ring_sides>`     | ``6``    |
   +---------------------------------+-------------------------------------------------------------+----------+
   | :ref:`int<class_int>`           | :ref:`sides<class_CSGTorus3D_property_sides>`               | ``8``    |
   +---------------------------------+-------------------------------------------------------------+----------+
   | :ref:`bool<class_bool>`         | :ref:`smooth_faces<class_CSGTorus3D_property_smooth_faces>` | ``true`` |
   +---------------------------------+-------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CSGTorus3D_property_inner_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **inner_radius** = ``0.5`` :ref:`🔗<class_CSGTorus3D_property_inner_radius>`

.. rst-class:: classref-property-setget

- |void| **set_inner_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_inner_radius**\ (\ )

Bán kính trong của hình xuyến.

.. rst-class:: classref-item-separator

----

.. _class_CSGTorus3D_property_material:

.. rst-class:: classref-property

:ref:`Material<class_Material>` **material** :ref:`🔗<class_CSGTorus3D_property_material>`

.. rst-class:: classref-property-setget

- |void| **set_material**\ (\ value\: :ref:`Material<class_Material>`\ ) - :ref:`Material<class_Material>` **get_material**\ (\ )

Material được dùng để render hình xuyến.

.. rst-class:: classref-item-separator

----

.. _class_CSGTorus3D_property_outer_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **outer_radius** = ``1.0`` :ref:`🔗<class_CSGTorus3D_property_outer_radius>`

.. rst-class:: classref-property-setget

- |void| **set_outer_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_outer_radius**\ (\ )

Bán kính ngoài của hình xuyến.

.. rst-class:: classref-item-separator

----

.. _class_CSGTorus3D_property_ring_sides:

.. rst-class:: classref-property

:ref:`int<class_int>` **ring_sides** = ``6`` :ref:`🔗<class_CSGTorus3D_property_ring_sides>`

.. rst-class:: classref-property-setget

- |void| **set_ring_sides**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_ring_sides**\ (\ )

Số cạnh tạo nên mỗi vòng của hình xuyến.

.. rst-class:: classref-item-separator

----

.. _class_CSGTorus3D_property_sides:

.. rst-class:: classref-property

:ref:`int<class_int>` **sides** = ``8`` :ref:`🔗<class_CSGTorus3D_property_sides>`

.. rst-class:: classref-property-setget

- |void| **set_sides**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_sides**\ (\ )

Số lát tạo nên hình xuyến.

.. rst-class:: classref-item-separator

----

.. _class_CSGTorus3D_property_smooth_faces:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **smooth_faces** = ``true`` :ref:`🔗<class_CSGTorus3D_property_smooth_faces>`

.. rst-class:: classref-property-setget

- |void| **set_smooth_faces**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_smooth_faces**\ (\ )

Nếu ``true`` các normal của hình xuyến được thiết lập để tạo hiệu ứng mượt, khiến hình xuyến trông bo tròn. Nếu ``false`` hình xuyến sẽ có diện mạo đổ bóng phẳng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
