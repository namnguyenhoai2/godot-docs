:github_url: hide

.. meta::
	:keywords: batch

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/MultiMeshInstance3D.xml.

.. _class_MultiMeshInstance3D:

MultiMeshInstance3D
===================

**Kế thừa:** :ref:`GeometryInstance3D<class_GeometryInstance3D>` **<** :ref:`VisualInstance3D<class_VisualInstance3D>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node tạo instance của một :ref:`MultiMesh<class_MultiMesh>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

**MultiMeshInstance3D** là một node chuyên dụng để tạo instance của :ref:`GeometryInstance3D<class_GeometryInstance3D>`\ s dựa trên một resource :ref:`MultiMesh<class_MultiMesh>`.

Điều này hữu ích để tối ưu hóa việc render số lượng lớn instance của một mesh nhất định (ví dụ như cây trong rừng hoặc các ngọn cỏ).

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng MultiMeshInstance <../tutorials/3d/using_multi_mesh_instance>`

- :doc:`Tối ưu hóa bằng MultiMesh <../tutorials/performance/using_multimesh>`

- :doc:`Tạo hoạt ảnh cho hàng nghìn con cá bằng MultiMeshInstance <../tutorials/performance/vertex_animation/animating_thousands_of_fish>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+----------------------------------------------------------------+
   | :ref:`MultiMesh<class_MultiMesh>` | :ref:`multimesh<class_MultiMeshInstance3D_property_multimesh>` |
   +-----------------------------------+----------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiMeshInstance3D_property_multimesh:

.. rst-class:: classref-property

:ref:`MultiMesh<class_MultiMesh>` **multimesh** :ref:`🔗<class_MultiMeshInstance3D_property_multimesh>`

.. rst-class:: classref-property-setget

- |void| **set_multimesh**\ (\ value\: :ref:`MultiMesh<class_MultiMesh>`\ ) - :ref:`MultiMesh<class_MultiMesh>` **get_multimesh**\ (\ )

Resource :ref:`MultiMesh<class_MultiMesh>` sẽ được sử dụng và chia sẻ giữa tất cả các instance của **MultiMeshInstance3D**.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
