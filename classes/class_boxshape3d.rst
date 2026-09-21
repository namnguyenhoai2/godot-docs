:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/BoxShape3D.xml.

.. _class_BoxShape3D:

BoxShape3D
==========

**Kế thừa:** :ref:`Shape3D<class_Shape3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một hình hộp 3D được sử dụng để xử lý va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hình hộp 3D, предназнач предназнач? intended for use in physics. Usually used to provide a shape for a :ref:`CollisionShape3D<class_CollisionShape3D>`.

\ **Hiệu năng:** **BoxShape3D** kiểm tra va chạm rất nhanh. Nó nhanh hơn :ref:`CapsuleShape3D<class_CapsuleShape3D>` và :ref:`CylinderShape3D<class_CylinderShape3D>`, nhưng chậm hơn :ref:`SphereShape3D<class_SphereShape3D>`.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D Physics Tests Demo <https://godotengine.org/asset-library/asset/2747>`__

- `3D Kinematic Character Demo <https://godotengine.org/asset-library/asset/2739>`__

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+---------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`size<class_BoxShape3D_property_size>` | ``Vector3(1, 1, 1)`` |
   +-------------------------------+---------------------------------------------+----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_BoxShape3D_property_size:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **size** = ``Vector3(1, 1, 1)`` :ref:`🔗<class_BoxShape3D_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector3<class_Vector3>`\ ) - :ref:`Vector3<class_Vector3>` **get_size**\ (\ )

Chiều rộng, chiều cao và chiều sâu của hình hộp.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
