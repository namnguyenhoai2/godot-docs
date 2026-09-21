:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MeshInstance2D.xml.

.. _class_MeshInstance2D:

MeshInstance2D
==============

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Node dùng để hiển thị một :ref:`Mesh<class_Mesh>` trong 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Node dùng để hiển thị một :ref:`Mesh<class_Mesh>` trong 2D. Cách này có thể render nhanh hơn so với việc hiển thị một node :ref:`Sprite2D<class_Sprite2D>` có các vùng trong suốt lớn, đặc biệt khi node chiếm nhiều diện tích trên màn hình ở độ phân giải viewport cao. Nguyên nhân là việc sử dụng mesh được thiết kế vừa với các vùng đục của sprite sẽ giảm mức sử dụng GPU fill rate (đổi lại làm tăng mức sử dụng vertex processing).

Khi một :ref:`Mesh<class_Mesh>` cần được instantiate hơn hàng nghìn lần ở gần nhau, hãy cân nhắc sử dụng một :ref:`MultiMesh<class_MultiMesh>` trong một :ref:`MultiMeshInstance2D<class_MultiMeshInstance2D>` thay thế.

Có thể tạo **MeshInstance2D** từ một :ref:`Sprite2D<class_Sprite2D>` hiện có thông qua một công cụ trên thanh công cụ của editor. Chọn node :ref:`Sprite2D<class_Sprite2D>`, sau đó chọn **Sprite2D > Convert to MeshInstance2D** ở đầu viewport của 2D editor.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Mesh 2D <../tutorials/2d/2d_meshes>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+-------------------------------------------------------+
   | :ref:`Mesh<class_Mesh>`           | :ref:`mesh<class_MeshInstance2D_property_mesh>`       |
   +-----------------------------------+-------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`texture<class_MeshInstance2D_property_texture>` |
   +-----------------------------------+-------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signal
------

.. _class_MeshInstance2D_signal_texture_changed:

.. rst-class:: classref-signal

**texture_changed**\ (\ ) :ref:`🔗<class_MeshInstance2D_signal_texture_changed>`

Được phát ra khi :ref:`texture<class_MeshInstance2D_property_texture>` bị thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MeshInstance2D_property_mesh:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **mesh** :ref:`🔗<class_MeshInstance2D_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_mesh**\ (\ )

:ref:`Mesh<class_Mesh>` sẽ được **MeshInstance2D** vẽ.

.. rst-class:: classref-item-separator

----

.. _class_MeshInstance2D_property_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **texture** :ref:`🔗<class_MeshInstance2D_property_texture>`

.. rst-class:: classref-property-setget

- |void| **set_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_texture**\ (\ )

:ref:`Texture2D<class_Texture2D>` sẽ được sử dụng nếu dùng :ref:`CanvasItemMaterial<class_CanvasItemMaterial>` mặc định. Có thể truy cập dưới dạng ``TEXTURE`` trong CanvasItem shader.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
