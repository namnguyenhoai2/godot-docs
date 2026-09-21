:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CircleShape2D.xml.

.. _class_CircleShape2D:

CircleShape2D
=============

**Kế thừa:** :ref:`Shape2D<class_Shape2D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một hình tròn 2D được dùng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hình tròn 2D, được thiết kế để sử dụng trong vật lý. Thường được dùng để cung cấp hình dạng cho một :ref:`CollisionShape2D<class_CollisionShape2D>`.

\ **Hiệu năng:** **CircleShape2D** nhanh khi kiểm tra va chạm. Nó nhanh hơn :ref:`RectangleShape2D<class_RectangleShape2D>` và :ref:`CapsuleShape2D<class_CapsuleShape2D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+----------------------------------------------------+----------+
   | :ref:`float<class_float>` | :ref:`radius<class_CircleShape2D_property_radius>` | ``10.0`` |
   +---------------------------+----------------------------------------------------+----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CircleShape2D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``10.0`` :ref:`🔗<class_CircleShape2D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của hình tròn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
