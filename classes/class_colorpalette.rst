:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ColorPalette.xml.

.. _class_ColorPalette:

ColorPalette
============

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một resource class dùng để quản lý bảng màu, có thể được tải và lưu bằng :ref:`ColorPicker<class_ColorPicker>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Resource **ColorPalette** được thiết kế để lưu trữ và quản lý một tập hợp màu. Resource này hữu ích trong các trường hợp cần một tập hợp màu được định sẵn, chẳng hạn như tạo theme, thiết kế user interface hoặc quản lý game asset. Control tích hợp sẵn :ref:`ColorPicker<class_ColorPicker>` cũng có thể sử dụng **ColorPalette** mà không cần thêm code.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------------------------+---------------------------------------------------+------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>` | :ref:`colors<class_ColorPalette_property_colors>` | ``PackedColorArray()`` |
   +-------------------------------------------------+---------------------------------------------------+------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ColorPalette_property_colors:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **colors** = ``PackedColorArray()`` :ref:`🔗<class_ColorPalette_property_colors>`

.. rst-class:: classref-property-setget

- |void| **set_colors**\ (\ value\: :ref:`PackedColorArray<class_PackedColorArray>`\ ) - :ref:`PackedColorArray<class_PackedColorArray>` **get_colors**\ (\ )

Một :ref:`PackedColorArray<class_PackedColorArray>` chứa các màu trong bảng màu.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng này sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
