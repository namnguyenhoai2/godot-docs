:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Occluder3D.xml.

.. _class_Occluder3D:

Occluder3D
==========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ArrayOccluder3D<class_ArrayOccluder3D>`, :ref:`BoxOccluder3D<class_BoxOccluder3D>`, :ref:`PolygonOccluder3D<class_PolygonOccluder3D>`, :ref:`QuadOccluder3D<class_QuadOccluder3D>`, :ref:`SphereOccluder3D<class_SphereOccluder3D>`

Tài nguyên hình dạng occluder để sử dụng cho occlusion culling trong :ref:`OccluderInstance3D<class_OccluderInstance3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**Occluder3D** lưu trữ một hình dạng occluder có thể được engine sử dụng trong hệ thống occlusion culling.

Xem tài liệu của :ref:`OccluderInstance3D<class_OccluderInstance3D>` để biết hướng dẫn thiết lập occlusion culling.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Occlusion culling <../tutorials/3d/occlusion_culling>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`     | :ref:`get_indices<class_Occluder3D_method_get_indices>`\ (\ ) |const|   |
   +-----------------------------------------------------+-------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_vertices<class_Occluder3D_method_get_vertices>`\ (\ ) |const| |
   +-----------------------------------------------------+-------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Occluder3D_method_get_indices:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **get_indices**\ (\ ) |const| :ref:`🔗<class_Occluder3D_method_get_indices>`

Trả về các chỉ số đỉnh của hình dạng occluder.

.. rst-class:: classref-item-separator

----

.. _class_Occluder3D_method_get_vertices:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_vertices**\ (\ ) |const| :ref:`🔗<class_Occluder3D_method_get_vertices>`

Trả về các vị trí đỉnh của hình dạng occluder.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
