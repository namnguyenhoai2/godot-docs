:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/MeshTexture.xml.

.. _class_MeshTexture:

MeshTexture
===========

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture đơn giản sử dụng một mesh để tự vẽ.

.. rst-class:: classref-introduction-group

Mô tả
-----

Texture đơn giản sử dụng một mesh để tự vẽ. Nó bị giới hạn vì không thể thay đổi các flags và không hỗ trợ vẽ theo vùng.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Texture2D<class_Texture2D>` | :ref:`base_texture<class_MeshTexture_property_base_texture>` |                                                                                        |
   +-----------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`     | :ref:`image_size<class_MeshTexture_property_image_size>`     | ``Vector2(0, 0)``                                                                      |
   +-----------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Mesh<class_Mesh>`           | :ref:`mesh<class_MeshTexture_property_mesh>`                 |                                                                                        |
   +-----------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`           | resource_local_to_scene                                      | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-----------------------------------+--------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MeshTexture_property_base_texture:

.. rst-class:: classref-property

:ref:`Texture2D<class_Texture2D>` **base_texture** :ref:`🔗<class_MeshTexture_property_base_texture>`

.. rst-class:: classref-property-setget

- |void| **set_base_texture**\ (\ value\: :ref:`Texture2D<class_Texture2D>`\ ) - :ref:`Texture2D<class_Texture2D>` **get_base_texture**\ (\ )

Thiết lập texture cơ sở mà Mesh sẽ sử dụng để vẽ.

.. rst-class:: classref-item-separator

----

.. _class_MeshTexture_property_image_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **image_size** = ``Vector2(0, 0)`` :ref:`🔗<class_MeshTexture_property_image_size>`

.. rst-class:: classref-property-setget

- |void| **set_image_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_image_size**\ (\ )

Thiết lập kích thước của hình ảnh, cần thiết để tham chiếu.

.. rst-class:: classref-item-separator

----

.. _class_MeshTexture_property_mesh:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **mesh** :ref:`🔗<class_MeshTexture_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_mesh**\ (\ )

Thiết lập mesh được sử dụng để vẽ. Mesh đó phải sử dụng các đỉnh 2D.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
