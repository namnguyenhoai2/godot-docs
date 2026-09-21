:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Path3D.xml.

.. _class_Path3D:

Path3D
======

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Chứa một đường dẫn :ref:`Curve3D<class_Curve3D>` để các node :ref:`PathFollow3D<class_PathFollow3D>` đi theo.

.. rst-class:: classref-introduction-group

Mô tả
-----

Có thể có các node con :ref:`PathFollow3D<class_PathFollow3D>` di chuyển dọc theo :ref:`Curve3D<class_Curve3D>`. Xem :ref:`PathFollow3D<class_PathFollow3D>` để biết thêm thông tin về cách sử dụng.

Lưu ý rằng đường dẫn được xem là tương đối so với các node được di chuyển (các node con của :ref:`PathFollow3D<class_PathFollow3D>`). Vì vậy, đường cong thường nên bắt đầu bằng một vector không ``(0, 0, 0)``.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------------------------------------+-----------------------+
   | :ref:`Curve3D<class_Curve3D>` | :ref:`curve<class_Path3D_property_curve>`                           |                       |
   +-------------------------------+---------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`debug_custom_color<class_Path3D_property_debug_custom_color>` | ``Color(0, 0, 0, 1)`` |
   +-------------------------------+---------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_Path3D_signal_curve_changed:

.. rst-class:: classref-signal

**curve_changed**\ (\ ) :ref:`🔗<class_Path3D_signal_curve_changed>`

Được phát ra khi :ref:`curve<class_Path3D_property_curve>` thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_Path3D_signal_debug_color_changed:

.. rst-class:: classref-signal

**debug_color_changed**\ (\ ) :ref:`🔗<class_Path3D_signal_debug_color_changed>`

Được phát ra khi :ref:`debug_custom_color<class_Path3D_property_debug_custom_color>` thay đổi.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Path3D_property_curve:

.. rst-class:: classref-property

:ref:`Curve3D<class_Curve3D>` **curve** :ref:`🔗<class_Path3D_property_curve>`

.. rst-class:: classref-property-setget

- |void| **set_curve**\ (\ value\: :ref:`Curve3D<class_Curve3D>`\ ) - :ref:`Curve3D<class_Curve3D>` **get_curve**\ (\ )

Một :ref:`Curve3D<class_Curve3D>` mô tả đường dẫn.

.. rst-class:: classref-item-separator

----

.. _class_Path3D_property_debug_custom_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **debug_custom_color** = ``Color(0, 0, 0, 1)`` :ref:`🔗<class_Path3D_property_debug_custom_color>`

.. rst-class:: classref-property-setget

- |void| **set_debug_custom_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_debug_custom_color**\ (\ )

Màu tùy chỉnh được dùng để vẽ đường dẫn trong editor. Nếu được đặt thành :ref:`Color.BLACK<class_Color_constant_BLACK>` (như mặc định), màu được thiết lập trong :ref:`ProjectSettings.debug/shapes/paths/geometry_color<class_ProjectSettings_property_debug/shapes/paths/geometry_color>` sẽ được sử dụng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
