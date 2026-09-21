:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Path2D.xml.

.. _class_Path2D:

Path2D
======

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Chứa một đường dẫn :ref:`Curve2D<class_Curve2D>` để các node :ref:`PathFollow2D<class_PathFollow2D>` đi theo.

.. rst-class:: classref-introduction-group

Mô tả
-----

Có thể có các node con :ref:`PathFollow2D<class_PathFollow2D>` di chuyển dọc theo :ref:`Curve2D<class_Curve2D>`. Xem :ref:`PathFollow2D<class_PathFollow2D>` để biết thêm thông tin về cách sử dụng.

\ **Lưu ý:** Đường dẫn được xem là tương đối so với các node được di chuyển (các node con của :ref:`PathFollow2D<class_PathFollow2D>`). Vì vậy, đường cong thường nên bắt đầu bằng một vector không (``(0, 0)``).

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------+
   | :ref:`Curve2D<class_Curve2D>` | :ref:`curve<class_Path2D_property_curve>` |
   +-------------------------------+-------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Path2D_property_curve:

.. rst-class:: classref-property

:ref:`Curve2D<class_Curve2D>` **curve** :ref:`🔗<class_Path2D_property_curve>`

.. rst-class:: classref-property-setget

- |void| **set_curve**\ (\ value\: :ref:`Curve2D<class_Curve2D>`\ ) - :ref:`Curve2D<class_Curve2D>` **get_curve**\ (\ )

Một :ref:`Curve2D<class_Curve2D>` mô tả đường dẫn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
