:github_url: hide

.. meta::
	:keywords: batch

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MultiMeshInstance2D.xml.

.. _class_MultiMeshInstance2D:

MultiMeshInstance2D
===================

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node tạo một instance của :ref:`MultiMesh<class_MultiMesh>` trong 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

**MultiMeshInstance2D** là một node chuyên dụng để tạo instance của resource :ref:`MultiMesh<class_MultiMesh>` trong 2D. Cách này có thể render nhanh hơn so với việc hiển thị nhiều node :ref:`Sprite2D<class_Sprite2D>` có các vùng trong suốt lớn, đặc biệt nếu các node chiếm nhiều không gian trên màn hình ở độ phân giải viewport cao. Điều này là do việc sử dụng một mesh được thiết kế vừa với các vùng không trong suốt của sprite sẽ giảm mức sử dụng GPU fill rate (đổi lại làm tăng mức sử dụng vertex processing).

Cách sử dụng giống như :ref:`MultiMeshInstance3D<class_MultiMeshInstance3D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+----------------------------------------------------------------+
   | :ref:`MultiMesh<class_MultiMesh>` | :ref:`multimesh<class_MultiMeshInstance2D_property_multimesh>` |
   +-----------------------------------+----------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture<class_MultiMeshInstance2D_property_texture>`     |
   +-----------------------------------+----------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_MultiMeshInstance2D_signal_texture_changed:

.. rst-class:: classref-signal

**texture_changed**\ (\ ) :ref:`🔗<class_MultiMeshInstance2D_signal_texture_changed>`

Được phát ra khi :ref:`texture<class_MultiMeshInstance2D_property_texture>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiMeshInstance2D_property_multimesh:

.. rst-class:: classref-property

:ref:`MultiMesh<class_MultiMesh>` **multimesh** :ref:`🔗<class_MultiMeshInstance2D_property_multimesh>`

.. rst-class:: classref-property-setget

- |void| **set_multimesh**\ (\ value\: :ref:`MultiMesh<class_MultiMesh>`\ ) - :ref:`MultiMesh<class_MultiMesh>` **get_multimesh**\ (\ )

:ref:`MultiMesh<class_MultiMesh>` sẽ được vẽ bởi **MultiMeshInstance2D**.

.. rst-class:: classref-item-separator

----

.. _class_MultiMeshInstance2D_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_MultiMeshInstance2D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

:ref:`Texture2D<class_Texture2D>` sẽ được sử dụng khi dùng :ref:`CanvasItemMaterial<class_CanvasItemMaterial>` mặc định. Có thể truy cập dưới dạng ``TEXTURE`` trong CanvasItem shader.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
