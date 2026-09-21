:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/BoxContainer.xml.

.. _class_BoxContainer:

BoxContainer
============

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`HBoxContainer<class_HBoxContainer>`, :ref:`VBoxContainer<class_VBoxContainer>`

Một container sắp xếp các control con theo chiều ngang hoặc chiều dọc.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một container sắp xếp các control con theo chiều ngang hoặc chiều dọc, tự động sắp xếp lại chúng khi kích thước tối thiểu của chúng thay đổi.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Using Containers <../tutorials/ui/gui_containers>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------------------------+---------------------------------------------------------+-----------+
   | :ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>` | :ref:`alignment<class_BoxContainer_property_alignment>` | ``0``     |
   +-------------------------------------------------------+---------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                               | :ref:`vertical<class_BoxContainer_property_vertical>`   | ``false`` |
   +-------------------------------------------------------+---------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------------------------------------+
   | :ref:`Control<class_Control>` | :ref:`add_spacer<class_BoxContainer_method_add_spacer>`\ (\ begin\: :ref:`bool<class_bool>`\ ) |
   +-------------------------------+------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------+-----------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`separation<class_BoxContainer_theme_constant_separation>` | ``4`` |
   +-----------------------+-----------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_BoxContainer_AlignmentMode:

.. rst-class:: classref-enumeration

enum **AlignmentMode**: :ref:`🔗<enum_BoxContainer_AlignmentMode>`

.. _class_BoxContainer_constant_ALIGNMENT_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>` **ALIGNMENT_BEGIN** = ``0``

Các control con sẽ được sắp xếp ở đầu container, tức là phía trên nếu orientation là chiều dọc, phía trái nếu orientation là chiều ngang (phía phải đối với bố cục RTL).

.. _class_BoxContainer_constant_ALIGNMENT_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>` **ALIGNMENT_CENTER** = ``1``

Các control con sẽ được căn giữa trong container.

.. _class_BoxContainer_constant_ALIGNMENT_END:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>` **ALIGNMENT_END** = ``2``

Các control con sẽ được sắp xếp ở cuối container, tức là phía dưới nếu orientation là chiều dọc, phía phải nếu orientation là chiều ngang (phía trái đối với bố cục RTL).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BoxContainer_property_alignment:

.. rst-class:: classref-property

:ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>` **alignment** = ``0`` :ref:`🔗<class_BoxContainer_property_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_alignment**\ (\ value\: :ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>`\ ) - :ref:`AlignmentMode<enum_BoxContainer_AlignmentMode>` **get_alignment**\ (\ )

Căn chỉnh các phần tử con của container (phải là một trong :ref:`ALIGNMENT_BEGIN<class_BoxContainer_constant_ALIGNMENT_BEGIN>`, :ref:`ALIGNMENT_CENTER<class_BoxContainer_constant_ALIGNMENT_CENTER>` hoặc :ref:`ALIGNMENT_END<class_BoxContainer_constant_ALIGNMENT_END>`).

.. rst-class:: classref-item-separator

----

.. _class_BoxContainer_property_vertical:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **vertical** = ``false`` :ref:`🔗<class_BoxContainer_property_vertical>`

.. rst-class:: classref-property-setget

- |void| **set_vertical**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_vertical**\ (\ )

Nếu ``true``, **BoxContainer** sẽ sắp xếp các phần tử con theo chiều dọc thay vì chiều ngang.

Không thể thay đổi khi sử dụng :ref:`HBoxContainer<class_HBoxContainer>` và :ref:`VBoxContainer<class_VBoxContainer>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_BoxContainer_method_add_spacer:

.. rst-class:: classref-method

:ref:`Control<class_Control>` **add_spacer**\ (\ begin\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_BoxContainer_method_add_spacer>`

Thêm một node :ref:`Control<class_Control>` vào box làm khoảng đệm. Nếu ``begin`` là ``true``, node :ref:`Control<class_Control>` sẽ được chèn phía trước tất cả các phần tử con khác.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_BoxContainer_theme_constant_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **separation** = ``4`` :ref:`🔗<class_BoxContainer_theme_constant_separation>`

Khoảng cách giữa các phần tử của **BoxContainer**, tính bằng pixel.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
