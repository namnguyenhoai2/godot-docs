:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/FlowContainer.xml.

.. _class_FlowContainer:

FlowContainer
=============

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`HFlowContainer<class_HFlowContainer>`, :ref:`VFlowContainer<class_VFlowContainer>`

Một container sắp xếp các control con theo chiều ngang hoặc dọc và ngắt dòng khi chúng chạm đến các biên.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một container sắp xếp các control con theo chiều ngang hoặc dọc và ngắt dòng khi chúng chạm đến các biên. Cách này tương tự như khi văn bản trong một cuốn sách tự động ngắt dòng vì không thể chứa thêm từ nào trên một dòng.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng Container <../tutorials/ui/gui_containers>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +------------------------------------------------------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>`                 | :ref:`alignment<class_FlowContainer_property_alignment>`                     | ``0``     |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` | :ref:`last_wrap_alignment<class_FlowContainer_property_last_wrap_alignment>` | ``0``     |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                | :ref:`reverse_fill<class_FlowContainer_property_reverse_fill>`               | ``false`` |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`                                                | :ref:`vertical<class_FlowContainer_property_vertical>`                       | ``false`` |
   +------------------------------------------------------------------------+------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`get_line_count<class_FlowContainer_method_get_line_count>`\ (\ ) |const| |
   +-----------------------+--------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các thuộc tính Theme
--------------------

.. table::
   :widths: auto

   +-----------------------+----------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`h_separation<class_FlowContainer_theme_constant_h_separation>` | ``4`` |
   +-----------------------+----------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`v_separation<class_FlowContainer_theme_constant_v_separation>` | ``4`` |
   +-----------------------+----------------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_FlowContainer_AlignmentMode:

.. rst-class:: classref-enumeration

enum **AlignmentMode**: :ref:`🔗<enum_FlowContainer_AlignmentMode>`

.. _class_FlowContainer_constant_ALIGNMENT_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>` **ALIGNMENT_BEGIN** = ``0``

Các control con sẽ được sắp xếp ở đầu container, tức là phía trên nếu orientation là dọc, phía trái nếu orientation là ngang (phía phải đối với layout RTL).

.. _class_FlowContainer_constant_ALIGNMENT_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>` **ALIGNMENT_CENTER** = ``1``

Các control con sẽ được căn giữa trong container.

.. _class_FlowContainer_constant_ALIGNMENT_END:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>` **ALIGNMENT_END** = ``2``

Các control con sẽ được sắp xếp ở cuối container, tức là phía dưới nếu orientation là dọc, phía phải nếu orientation là ngang (phía trái đối với layout RTL).

.. rst-class:: classref-item-separator

----

.. _enum_FlowContainer_LastWrapAlignmentMode:

.. rst-class:: classref-enumeration

enum **LastWrapAlignmentMode**: :ref:`🔗<enum_FlowContainer_LastWrapAlignmentMode>`

.. _class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_INHERIT:

.. rst-class:: classref-enumeration-constant

:ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` **LAST_WRAP_ALIGNMENT_INHERIT** = ``0``

Hàng hoặc cột cuối cùng chưa được lấp đầy hoàn toàn sẽ được ngắt dòng và căn chỉnh theo hàng hoặc cột trước đó, theo :ref:`alignment<class_FlowContainer_property_alignment>`.

.. _class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` **LAST_WRAP_ALIGNMENT_BEGIN** = ``1``

Hàng hoặc cột cuối cùng chưa được lấp đầy hoàn toàn sẽ được ngắt dòng và căn chỉnh theo đầu của hàng hoặc cột trước đó.

.. _class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` **LAST_WRAP_ALIGNMENT_CENTER** = ``2``

Hàng hoặc cột cuối cùng chưa được lấp đầy hoàn toàn sẽ được ngắt dòng và căn chỉnh theo giữa của hàng hoặc cột trước đó.

.. _class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_END:

.. rst-class:: classref-enumeration-constant

:ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` **LAST_WRAP_ALIGNMENT_END** = ``3``

Hàng hoặc cột cuối cùng chưa được lấp đầy hoàn toàn sẽ được ngắt dòng và căn chỉnh theo cuối của hàng hoặc cột trước đó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_FlowContainer_property_alignment:

.. rst-class:: classref-property

:ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>` **alignment** = ``0`` :ref:`🔗<class_FlowContainer_property_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_alignment**\ (\ value\: :ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>`\ ) - :ref:`AlignmentMode<enum_FlowContainer_AlignmentMode>` **get_alignment**\ (\ )

Alignment của các control con trong container (phải là một trong :ref:`ALIGNMENT_BEGIN<class_FlowContainer_constant_ALIGNMENT_BEGIN>`, :ref:`ALIGNMENT_CENTER<class_FlowContainer_constant_ALIGNMENT_CENTER>` hoặc :ref:`ALIGNMENT_END<class_FlowContainer_constant_ALIGNMENT_END>`).

.. rst-class:: classref-item-separator

----

.. _class_FlowContainer_property_last_wrap_alignment:

.. rst-class:: classref-property

:ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` **last_wrap_alignment** = ``0`` :ref:`🔗<class_FlowContainer_property_last_wrap_alignment>`

.. rst-class:: classref-property-setget

- |void| **set_last_wrap_alignment**\ (\ value\: :ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>`\ ) - :ref:`LastWrapAlignmentMode<enum_FlowContainer_LastWrapAlignmentMode>` **get_last_wrap_alignment**\ (\ )

Cách xử lý ngắt dòng của hàng hoặc cột cuối cùng chưa được lấp đầy hoàn toàn (phải là một trong :ref:`LAST_WRAP_ALIGNMENT_INHERIT<class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_INHERIT>`, :ref:`LAST_WRAP_ALIGNMENT_BEGIN<class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_BEGIN>`, :ref:`LAST_WRAP_ALIGNMENT_CENTER<class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_CENTER>` hoặc :ref:`LAST_WRAP_ALIGNMENT_END<class_FlowContainer_constant_LAST_WRAP_ALIGNMENT_END>`).

.. rst-class:: classref-item-separator

----

.. _class_FlowContainer_property_reverse_fill:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **reverse_fill** = ``false`` :ref:`🔗<class_FlowContainer_property_reverse_fill>`

.. rst-class:: classref-property-setget

- |void| **set_reverse_fill**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_reverse_fill**\ (\ )

Nếu là ``true``, đảo ngược hướng lấp đầy. Các **FlowContainer**\ ngang sẽ lấp đầy các hàng từ dưới lên trên, còn **FlowContainer**\ dọc sẽ lấp đầy các cột từ phải sang trái.

Khi sử dụng **FlowContainer** dọc với :ref:`Control.layout_direction<class_Control_property_layout_direction>` từ phải sang trái, các cột sẽ được lấp đầy từ trái sang phải.

.. rst-class:: classref-item-separator

----

.. _class_FlowContainer_property_vertical:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **vertical** = ``false`` :ref:`🔗<class_FlowContainer_property_vertical>`

.. rst-class:: classref-property-setget

- |void| **set_vertical**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_vertical**\ (\ )

Nếu là ``true``, **FlowContainer** sẽ sắp xếp các control con theo chiều dọc thay vì chiều ngang.

Không thể thay đổi khi sử dụng :ref:`HFlowContainer<class_HFlowContainer>` và :ref:`VFlowContainer<class_VFlowContainer>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_FlowContainer_method_get_line_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_line_count**\ (\ ) |const| :ref:`🔗<class_FlowContainer_method_get_line_count>`

Trả về số dòng hiện tại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_FlowContainer_theme_constant_h_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **h_separation** = ``4`` :ref:`🔗<class_FlowContainer_theme_constant_h_separation>`

Khoảng cách theo chiều ngang giữa các node con.

.. rst-class:: classref-item-separator

----

.. _class_FlowContainer_theme_constant_v_separation:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **v_separation** = ``4`` :ref:`🔗<class_FlowContainer_theme_constant_v_separation>`

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
