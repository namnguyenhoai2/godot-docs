:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/HScrollBar.xml.

.. _class_HScrollBar:

HScrollBar
==========

**Kế thừa:** :ref:`ScrollBar<class_ScrollBar>` **<** :ref:`Range<class_Range>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một thanh cuộn ngang đi từ trái (min) sang phải (max).

.. rst-class:: classref-introduction-group

Mô tả
-----

Một thanh cuộn ngang, thường được dùng để điều hướng qua nội dung mở rộng vượt quá chiều rộng hiển thị của một control. Đây là một control dựa trên :ref:`Range<class_Range>` và đi từ trái (min) sang phải (max).

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------+-----------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`padding_bottom<class_HScrollBar_theme_constant_padding_bottom>` | ``0`` |
   +-----------------------+-----------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`padding_top<class_HScrollBar_theme_constant_padding_top>`       | ``0`` |
   +-----------------------+-----------------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_HScrollBar_theme_constant_padding_bottom:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **padding_bottom** = ``0`` :ref:`🔗<class_HScrollBar_theme_constant_padding_bottom>`

Khoảng đệm giữa phần tử :ref:`ScrollBar.scroll<class_ScrollBar_theme_style_scroll>` ở dưới cùng và :ref:`ScrollBar.grabber<class_ScrollBar_theme_style_grabber>`.

\ **Lưu ý:** Để áp dụng khoảng đệm ngang, hãy thay đổi lề nội dung trái/phải của :ref:`ScrollBar.scroll<class_ScrollBar_theme_style_scroll>`.

.. rst-class:: classref-item-separator

----

.. _class_HScrollBar_theme_constant_padding_top:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **padding_top** = ``0`` :ref:`🔗<class_HScrollBar_theme_constant_padding_top>`

Khoảng đệm giữa phần tử :ref:`ScrollBar.scroll<class_ScrollBar_theme_style_scroll>` ở trên cùng và :ref:`ScrollBar.grabber<class_ScrollBar_theme_style_grabber>`.

\ **Lưu ý:** Để áp dụng khoảng đệm ngang, hãy thay đổi lề nội dung trái/phải của :ref:`ScrollBar.scroll<class_ScrollBar_theme_style_scroll>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
