:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/GridContainer.xml.

.. _class_GridContainer:

GridContainer
=============

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một container sắp xếp các control con theo bố cục lưới.

.. rst-class:: classref-introduction-group

Mô tả
-----

**GridContainer** sắp xếp các control con theo bố cục lưới. Số lượng cột được chỉ định bởi thuộc tính :ref:`columns<class_GridContainer_property_columns>`, trong khi số lượng hàng phụ thuộc vào số hàng cần thiết cho các control con. Số lượng hàng và cột được giữ nguyên với mọi kích thước của container.

\ **Lưu ý:** **GridContainer** chỉ hoạt động với các node con kế thừa từ :ref:`Control<class_Control>`. Nó sẽ không sắp xếp lại các node con kế thừa từ :ref:`Node2D<class_Node2D>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng Container <../tutorials/ui/gui_containers>`

- `Operating System Testing Demo <https://godotengine.org/asset-library/asset/2789>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------+------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`columns<class_GridContainer_property_columns>` | ``1`` |
   +-----------------------+------------------------------------------------------+-------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------+----------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`h_separation<class_GridContainer_theme_constant_h_separation>` | ``4`` |
   +-----------------------+----------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`v_separation<class_GridContainer_theme_constant_v_separation>` | ``4`` |
   +-----------------------+----------------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_GridContainer_property_columns:

.. rst-class:: classref-property

:ref:`int<class_int>` **columns** = ``1`` :ref:`🔗<class_GridContainer_property_columns>`

.. rst-class:: classref-property-setget

- |void| **set_columns**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_columns**\ (\ )

Số lượng cột trong **GridContainer**. Nếu được thay đổi, **GridContainer** sẽ sắp xếp lại các node con kế thừa từ Control để phù hợp với bố cục mới.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_GridContainer_theme_constant_h_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **h_separation** = ``4`` :ref:`🔗<class_GridContainer_theme_constant_h_separation>`

Khoảng cách theo chiều ngang giữa các node con.

.. rst-class:: classref-item-separator

----

.. _class_GridContainer_theme_constant_v_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **v_separation** = ``4`` :ref:`🔗<class_GridContainer_theme_constant_v_separation>`

Khoảng cách theo chiều dọc giữa các node con.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
