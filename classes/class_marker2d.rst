:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Marker2D.xml.

.. _class_Marker2D:

Marker2D
========

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Gợi ý vị trí 2D chung để chỉnh sửa.

.. rst-class:: classref-introduction-group

Mô tả
-----

Gợi ý vị trí 2D chung để chỉnh sửa. Nó giống như một :ref:`Node2D<class_Node2D>` đơn giản, nhưng luôn hiển thị dưới dạng dấu thập trong trình chỉnh sửa 2D. Bạn có thể đặt kích thước hiển thị của dấu thập bằng gizmo trong trình chỉnh sửa 2D khi node được chọn.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+-------------------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`gizmo_extents<class_Marker2D_property_gizmo_extents>` | ``10.0`` |
   +---------------------------+-------------------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Marker2D_property_gizmo_extents:

.. rst-class:: classref-property

:ref:`float<class_float>` **gizmo_extents** = ``10.0`` :ref:`🔗<class_Marker2D_property_gizmo_extents>`

.. rst-class:: classref-property-setget

- |void| **set_gizmo_extents**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_gizmo_extents**\ (\ )

Kích thước của dấu thập gizmo xuất hiện trong trình chỉnh sửa.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
