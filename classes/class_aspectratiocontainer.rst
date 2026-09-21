:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/AspectRatioContainer.xml.

.. _class_AspectRatioContainer:

AspectRatioContainer
====================

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một container giữ nguyên tỷ lệ của các control con.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một loại container sắp xếp các control con theo cách tự động giữ nguyên tỷ lệ của chúng khi container được thay đổi kích thước. Hữu ích khi container có kích thước động và các node con cần điều chỉnh kích thước tương ứng mà không làm mất tỷ lệ khung hình.

.. rst-class:: classref-introduction-group

Tutorials
---------

- :doc:`Using Containers <../tutorials/ui/gui_containers>`

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +---------------------------------------------------------------+---------------------------------------------------------------------------------------+---------+
   | :ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` | :ref:`alignment_horizontal<class_AspectRatioContainer_property_alignment_horizontal>` | ``1``   |
   +---------------------------------------------------------------+---------------------------------------------------------------------------------------+---------+
   | :ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` | :ref:`alignment_vertical<class_AspectRatioContainer_property_alignment_vertical>`     | ``1``   |
   +---------------------------------------------------------------+---------------------------------------------------------------------------------------+---------+
   | :ref:`float<class_float>`                                     | :ref:`ratio<class_AspectRatioContainer_property_ratio>`                               | ``1.0`` |
   +---------------------------------------------------------------+---------------------------------------------------------------------------------------+---------+
   | :ref:`StretchMode<enum_AspectRatioContainer_StretchMode>`     | :ref:`stretch_mode<class_AspectRatioContainer_property_stretch_mode>`                 | ``2``   |
   +---------------------------------------------------------------+---------------------------------------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumerations
------------

.. _enum_AspectRatioContainer_StretchMode:

.. rst-class:: classref-enumeration

enum **StretchMode**: :ref:`🔗<enum_AspectRatioContainer_StretchMode>`

.. _class_AspectRatioContainer_constant_STRETCH_WIDTH_CONTROLS_HEIGHT:

.. rst-class:: classref-enumeration-constant

:ref:`StretchMode<enum_AspectRatioContainer_StretchMode>` **STRETCH_WIDTH_CONTROLS_HEIGHT** = ``0``

Chiều cao của các control con được tự động điều chỉnh dựa trên chiều rộng của container.

.. _class_AspectRatioContainer_constant_STRETCH_HEIGHT_CONTROLS_WIDTH:

.. rst-class:: classref-enumeration-constant

:ref:`StretchMode<enum_AspectRatioContainer_StretchMode>` **STRETCH_HEIGHT_CONTROLS_WIDTH** = ``1``

Chiều rộng của các control con được tự động điều chỉnh dựa trên chiều cao của container.

.. _class_AspectRatioContainer_constant_STRETCH_FIT:

.. rst-class:: classref-enumeration-constant

:ref:`StretchMode<enum_AspectRatioContainer_StretchMode>` **STRETCH_FIT** = ``2``

Hình chữ nhật bao quanh các control con được tự động điều chỉnh để vừa bên trong container trong khi vẫn giữ nguyên tỷ lệ khung hình.

.. _class_AspectRatioContainer_constant_STRETCH_COVER:

.. rst-class:: classref-enumeration-constant

:ref:`StretchMode<enum_AspectRatioContainer_StretchMode>` **STRETCH_COVER** = ``3``

Chiều rộng và chiều cao của các control con được tự động điều chỉnh để hình chữ nhật bao quanh chúng phủ toàn bộ khu vực của container trong khi vẫn giữ nguyên tỷ lệ khung hình.

Khi hình chữ nhật bao quanh các control con vượt quá kích thước của container và :ref:`Control.clip_contents<class_Control_property_clip_contents>` được bật, tùy chọn này cho phép chỉ hiển thị khu vực của container bị giới hạn bởi chính hình chữ nhật bao quanh nó.

.. rst-class:: classref-item-separator

----

.. _enum_AspectRatioContainer_AlignmentMode:

.. rst-class:: classref-enumeration

enum **AlignmentMode**: :ref:`🔗<enum_AspectRatioContainer_AlignmentMode>`

.. _class_AspectRatioContainer_constant_ALIGNMENT_BEGIN:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **ALIGNMENT_BEGIN** = ``0``

Căn các control con theo phần đầu (bên trái hoặc phía trên) của container.

.. _class_AspectRatioContainer_constant_ALIGNMENT_CENTER:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **ALIGNMENT_CENTER** = ``1``

Căn các control con theo giữa container.

.. _class_AspectRatioContainer_constant_ALIGNMENT_END:

.. rst-class:: classref-enumeration-constant

:ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **ALIGNMENT_END** = ``2``

Căn các control con theo phần cuối (bên phải hoặc phía dưới) của container.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_AspectRatioContainer_property_alignment_horizontal:

.. rst-class:: classref-property

:ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **alignment_horizontal** = ``1`` :ref:`🔗<class_AspectRatioContainer_property_alignment_horizontal>`

.. rst-class:: classref-property-setget

- |void| **set_alignment_horizontal**\ (\ value\: :ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>`\ ) - :ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **get_alignment_horizontal**\ (\ )

Chỉ định vị trí tương đối theo chiều ngang của các control con.

.. rst-class:: classref-item-separator

----

.. _class_AspectRatioContainer_property_alignment_vertical:

.. rst-class:: classref-property

:ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **alignment_vertical** = ``1`` :ref:`🔗<class_AspectRatioContainer_property_alignment_vertical>`

.. rst-class:: classref-property-setget

- |void| **set_alignment_vertical**\ (\ value\: :ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>`\ ) - :ref:`AlignmentMode<enum_AspectRatioContainer_AlignmentMode>` **get_alignment_vertical**\ (\ )

Chỉ định vị trí tương đối theo chiều dọc của các control con.

.. rst-class:: classref-item-separator

----

.. _class_AspectRatioContainer_property_ratio:

.. rst-class:: classref-property

:ref:`float<class_float>` **ratio** = ``1.0`` :ref:`🔗<class_AspectRatioContainer_property_ratio>`

.. rst-class:: classref-property-setget

- |void| **set_ratio**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_ratio**\ (\ )

Tỷ lệ khung hình được áp dụng cho các control con. Đây là chiều rộng chia cho chiều cao. Tỷ lệ phụ thuộc vào :ref:`stretch_mode<class_AspectRatioContainer_property_stretch_mode>`.

.. rst-class:: classref-item-separator

----

.. _class_AspectRatioContainer_property_stretch_mode:

.. rst-class:: classref-property

:ref:`StretchMode<enum_AspectRatioContainer_StretchMode>` **stretch_mode** = ``2`` :ref:`🔗<class_AspectRatioContainer_property_stretch_mode>`

.. rst-class:: classref-property-setget

- |void| **set_stretch_mode**\ (\ value\: :ref:`StretchMode<enum_AspectRatioContainer_StretchMode>`\ ) - :ref:`StretchMode<enum_AspectRatioContainer_StretchMode>` **get_stretch_mode**\ (\ )

Chế độ stretch được sử dụng để căn chỉnh các control con.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
