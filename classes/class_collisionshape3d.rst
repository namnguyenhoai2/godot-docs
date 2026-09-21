:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CollisionShape3D.xml.

.. _class_CollisionShape3D:

CollisionShape3D
================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node cung cấp :ref:`Shape3D<class_Shape3D>` cho parent :ref:`CollisionObject3D<class_CollisionObject3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node cung cấp :ref:`Shape3D<class_Shape3D>` cho parent :ref:`CollisionObject3D<class_CollisionObject3D>` và cho phép chỉnh sửa nó. Điều này có thể cung cấp một detection shape cho :ref:`Area3D<class_Area3D>` hoặc biến :ref:`PhysicsBody3D<class_PhysicsBody3D>` thành một đối tượng rắn.

\ **Cảnh báo:** **CollisionShape3D** được scale không đồng đều có thể sẽ không hoạt động như mong đợi. Hãy đảm bảo scale của nó giống nhau trên tất cả các trục và thay vào đó điều chỉnh resource :ref:`shape<class_CollisionShape3D_property_shape>` của nó.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Physics introduction <../tutorials/physics/physics_introduction>`

- `3D Kinematic Character Demo <https://godotengine.org/asset-library/asset/2739>`__

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

.. rst-class:: classref-reftable-group

Properties
----------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`debug_color<class_CollisionShape3D_property_debug_color>` | ``Color(0, 0, 0, 0)`` |
   +-------------------------------+-----------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`       | :ref:`debug_fill<class_CollisionShape3D_property_debug_fill>`   | ``true``              |
   +-------------------------------+-----------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`       | :ref:`disabled<class_CollisionShape3D_property_disabled>`       | ``false``             |
   +-------------------------------+-----------------------------------------------------------------+-----------------------+
   | :ref:`Shape3D<class_Shape3D>` | :ref:`shape<class_CollisionShape3D_property_shape>`             |                       |
   +-------------------------------+-----------------------------------------------------------------+-----------------------+

.. rst-class:: classref-reftable-group

Methods
-------

.. table::
   :widths: auto

   +--------+---------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`make_convex_from_siblings<class_CollisionShape3D_method_make_convex_from_siblings>`\ (\ )                           |
   +--------+---------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`resource_changed<class_CollisionShape3D_method_resource_changed>`\ (\ resource\: :ref:`Resource<class_Resource>`\ ) |
   +--------+---------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CollisionShape3D_property_debug_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **debug_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_CollisionShape3D_property_debug_color>`

.. rst-class:: classref-property-setget

- |void| **set_debug_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_debug_color**\ (\ )

Màu của collision shape được hiển thị trong editor hoặc trong project đang chạy nếu **Debug > Visible Collision Shapes** được đánh dấu ở phía trên editor.

\ **Lưu ý:** Giá trị mặc định là :ref:`ProjectSettings.debug/shapes/collision/shape_color<class_ProjectSettings_property_debug/shapes/collision/shape_color>`. Giá trị ``Color(0, 0, 0, 0)`` được ghi lại ở đây chỉ là placeholder, không phải màu debug mặc định thực tế.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape3D_property_debug_fill:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **debug_fill** = ``true`` :ref:`🔗<class_CollisionShape3D_property_debug_fill>`

.. rst-class:: classref-property-setget

- |void| **set_enable_debug_fill**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_enable_debug_fill**\ (\ )

Nếu ``true``, khi shape được hiển thị, nó sẽ hiển thị màu tô đặc bên cạnh wireframe của nó.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape3D_property_disabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disabled** = ``false`` :ref:`🔗<class_CollisionShape3D_property_disabled>`

.. rst-class:: classref-property-setget

- |void| **set_disabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_disabled**\ (\ )

Collision shape bị vô hiệu hóa sẽ không có tác dụng trong world. Nên thay đổi thuộc tính này bằng :ref:`Object.set_deferred()<class_Object_method_set_deferred>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape3D_property_shape:

.. rst-class:: classref-property

:ref:`Shape3D<class_Shape3D>` **shape** :ref:`🔗<class_CollisionShape3D_property_shape>`

.. rst-class:: classref-property-setget

- |void| **set_shape**\ (\ value\: :ref:`Shape3D<class_Shape3D>`\ ) - :ref:`Shape3D<class_Shape3D>` **get_shape**\ (\ )

Shape thực tế thuộc về collision shape này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CollisionShape3D_method_make_convex_from_siblings:

.. rst-class:: classref-method

|void| **make_convex_from_siblings**\ (\ ) :ref:`🔗<class_CollisionShape3D_method_make_convex_from_siblings>`

Đặt shape của collision shape thành phần tổng hợp hình học của tất cả các sibling :ref:`MeshInstance3D<class_MeshInstance3D>` đã được chuyển thành convex.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape3D_method_resource_changed:

.. rst-class:: classref-method

|void| **resource_changed**\ (\ resource\: :ref:`Resource<class_Resource>`\ ) :ref:`🔗<class_CollisionShape3D_method_resource_changed>`

**Không dùng nữa:** Thay vào đó, hãy sử dụng :ref:`Resource.changed<class_Resource_signal_changed>`.

Phương thức này không thực hiện thao tác nào.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
