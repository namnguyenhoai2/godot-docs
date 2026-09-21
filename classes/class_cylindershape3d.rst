:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CylinderShape3D.xml.

.. _class_CylinderShape3D:

CylinderShape3D
===============

**Kế thừa:** :ref:`Shape3D<class_Shape3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một hình trụ 3D được dùng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hình trụ 3D, предназначена để sử dụng trong vật lý. Thường được dùng để cung cấp một hình dạng cho :ref:`CollisionShape3D<class_CollisionShape3D>`.

\ **Lưu ý:** Có một số lỗi đã biết với các hình dạng va chạm hình trụ. Bạn nên sử dụng :ref:`CapsuleShape3D<class_CapsuleShape3D>` hoặc :ref:`BoxShape3D<class_BoxShape3D>` thay thế.

\ **Hiệu năng:** **CylinderShape3D** kiểm tra va chạm rất nhanh, nhưng chậm hơn :ref:`CapsuleShape3D<class_CapsuleShape3D>`, :ref:`BoxShape3D<class_BoxShape3D>` và :ref:`SphereShape3D<class_SphereShape3D>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

- `3D Physics Tests Demo <https://godotengine.org/asset-library/asset/2747>`__

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------+------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`height<class_CylinderShape3D_property_height>` | ``2.0`` |
   +---------------------------+------------------------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`radius<class_CylinderShape3D_property_radius>` | ``0.5`` |
   +---------------------------+------------------------------------------------------+---------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CylinderShape3D_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``2.0`` :ref:`🔗<class_CylinderShape3D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Chiều cao của hình trụ.

.. rst-class:: classref-item-separator

----

.. _class_CylinderShape3D_property_radius:

.. rst-class:: classref-property

:ref:`float<class_float>` **radius** = ``0.5`` :ref:`🔗<class_CylinderShape3D_property_radius>`

.. rst-class:: classref-property-setget

- |void| **set_radius**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_radius**\ (\ )

Bán kính của hình trụ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
