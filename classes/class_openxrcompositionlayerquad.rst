:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/openxr/doc_classes/OpenXRCompositionLayerQuad.xml.

.. _class_OpenXRCompositionLayerQuad:

OpenXRCompositionLayerQuad
==========================

**Thử nghiệm:** Class này có thể được thay đổi hoặc xóa trong các phiên bản tương lai.

**Kế thừa:** :ref:`OpenXRCompositionLayer<class_OpenXRCompositionLayer>` **<** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một composition layer của OpenXR được kết xuất dưới dạng một quad.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một composition layer của OpenXR cho phép kết xuất một :ref:`SubViewport<class_SubViewport>` trên một quad.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`quad_size<class_OpenXRCompositionLayerQuad_property_quad_size>` | ``Vector2(1, 1)`` |
   +-------------------------------+-----------------------------------------------------------------------+-------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_OpenXRCompositionLayerQuad_property_quad_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **quad_size** = ``Vector2(1, 1)`` :ref:`🔗<class_OpenXRCompositionLayerQuad_property_quad_size>`

.. rst-class:: classref-property-setget

- |void| **set_quad_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_quad_size**\ (\ )

Kích thước của quad.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
