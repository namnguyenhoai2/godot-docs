:github_url: hide

.. meta::
	:keywords: padding

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MarginContainer.xml.

.. _class_MarginContainer:

MarginContainer
===============

**Kế thừa:** :ref:`Container<class_Container>` **<** :ref:`Control<class_Control>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`EditorDock<class_EditorDock>`

Một container giữ khoảng đệm xung quanh các control con.

.. rst-class:: classref-introduction-group

Mô tả
-----

**MarginContainer** thêm một khoảng đệm có thể điều chỉnh ở mỗi cạnh của các control con. Các khoảng đệm được thêm xung quanh tất cả các node con, không phải xung quanh từng node riêng lẻ. Để điều khiển các khoảng đệm của **MarginContainer**, hãy sử dụng các thuộc tính theme ``margin_*`` được liệt kê bên dưới.

\ **Lưu ý:** Kích thước khoảng đệm là các thuộc tính ghi đè của theme, không phải các thuộc tính thông thường. Đây là ví dụ về cách thay đổi chúng trong code:


.. tabs::

 .. code-tab:: gdscript

    # Mẫu code này giả định rằng script hiện tại đang kế thừa MarginContainer.
    var margin_value = 100
    add_theme_constant_override("margin_top", margin_value)
    add_theme_constant_override("margin_left", margin_value)
    add_theme_constant_override("margin_bottom", margin_value)
    add_theme_constant_override("margin_right", margin_value)

 .. code-tab:: csharp

    // Mẫu code này giả định rằng script hiện tại đang kế thừa MarginContainer.
    int marginValue = 100;
    AddThemeConstantOverride("margin_top", marginValue);
    AddThemeConstantOverride("margin_left", marginValue);
    AddThemeConstantOverride("margin_bottom", marginValue);
    AddThemeConstantOverride("margin_right", marginValue);



.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Sử dụng Container <../tutorials/ui/gui_containers>`

.. rst-class:: classref-reftable-group

Thuộc tính Theme
----------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`margin_bottom<class_MarginContainer_theme_constant_margin_bottom>` | ``0`` |
   +-----------------------+--------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`margin_left<class_MarginContainer_theme_constant_margin_left>`     | ``0`` |
   +-----------------------+--------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`margin_right<class_MarginContainer_theme_constant_margin_right>`   | ``0`` |
   +-----------------------+--------------------------------------------------------------------------+-------+
   | :ref:`int<class_int>` | :ref:`margin_top<class_MarginContainer_theme_constant_margin_top>`       | ``0`` |
   +-----------------------+--------------------------------------------------------------------------+-------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính Theme
----------------------

.. _class_MarginContainer_theme_constant_margin_bottom:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **margin_bottom** = ``0`` :ref:`🔗<class_MarginContainer_theme_constant_margin_bottom>`

Dịch các node con trực tiếp vào phía trong container một khoảng bằng số pixel này, tính từ phía dưới.

.. rst-class:: classref-item-separator

----

.. _class_MarginContainer_theme_constant_margin_left:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **margin_left** = ``0`` :ref:`🔗<class_MarginContainer_theme_constant_margin_left>`

Dịch các node con trực tiếp vào phía trong container một khoảng bằng số pixel này, tính từ bên trái.

.. rst-class:: classref-item-separator

----

.. _class_MarginContainer_theme_constant_margin_right:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **margin_right** = ``0`` :ref:`🔗<class_MarginContainer_theme_constant_margin_right>`

Dịch các node con trực tiếp vào phía trong container một khoảng bằng số pixel này, tính từ bên phải.

.. rst-class:: classref-item-separator

----

.. _class_MarginContainer_theme_constant_margin_top:

.. rst-class:: classref-themeproperty

:ref:`int<class_int>` **margin_top** = ``0`` :ref:`🔗<class_MarginContainer_theme_constant_margin_top>`

Dịch các node con trực tiếp vào phía trong container một khoảng bằng số pixel này, tính từ phía trên.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
