:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CollisionShape2D.xml.

.. _class_CollisionShape2D:

CollisionShape2D
================

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node cung cấp :ref:`Shape2D<class_Shape2D>` cho node cha :ref:`CollisionObject2D<class_CollisionObject2D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node cung cấp :ref:`Shape2D<class_Shape2D>` cho node cha :ref:`CollisionObject2D<class_CollisionObject2D>` và cho phép chỉnh sửa nó. Điều này có thể cung cấp một hình dạng phát hiện cho :ref:`Area2D<class_Area2D>` hoặc biến :ref:`PhysicsBody2D<class_PhysicsBody2D>` thành một vật thể rắn.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Physics introduction <../tutorials/physics/physics_introduction>`

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

- `2D Pong Demo <https://godotengine.org/asset-library/asset/2728>`__

- `2D Kinematic Character Demo <https://godotengine.org/asset-library/asset/2719>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Color<class_Color>`     | :ref:`debug_color<class_CollisionShape2D_property_debug_color>`                                 | ``Color(0, 0, 0, 0)`` |
   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`       | :ref:`disabled<class_CollisionShape2D_property_disabled>`                                       | ``false``             |
   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`bool<class_bool>`       | :ref:`one_way_collision<class_CollisionShape2D_property_one_way_collision>`                     | ``false``             |
   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`one_way_collision_direction<class_CollisionShape2D_property_one_way_collision_direction>` | ``Vector2(0, 1)``     |
   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`float<class_float>`     | :ref:`one_way_collision_margin<class_CollisionShape2D_property_one_way_collision_margin>`       | ``1.0``               |
   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+
   | :ref:`Shape2D<class_Shape2D>` | :ref:`shape<class_CollisionShape2D_property_shape>`                                             |                       |
   +-------------------------------+-------------------------------------------------------------------------------------------------+-----------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CollisionShape2D_property_debug_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **debug_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_CollisionShape2D_property_debug_color>`

.. rst-class:: classref-property-setget

- |void| **set_debug_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_debug_color**\ (\ )

Màu hình dạng va chạm được hiển thị trong editor hoặc trong project đang chạy nếu **Debug > Visible Collision Shapes** được chọn ở đầu editor.

\ **Lưu ý:** Giá trị mặc định là :ref:`ProjectSettings.debug/shapes/collision/shape_color<class_ProjectSettings_property_debug/shapes/collision/shape_color>`. Giá trị ``Color(0, 0, 0, 0)`` được ghi lại ở đây chỉ là placeholder, không phải màu debug mặc định thực tế.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape2D_property_disabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disabled** = ``false`` :ref:`🔗<class_CollisionShape2D_property_disabled>`

.. rst-class:: classref-property-setget

- |void| **set_disabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_disabled**\ (\ )

Hình dạng va chạm bị vô hiệu hóa không có tác động nào trong thế giới. Nên thay đổi thuộc tính này bằng :ref:`Object.set_deferred()<class_Object_method_set_deferred>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape2D_property_one_way_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **one_way_collision** = ``false`` :ref:`🔗<class_CollisionShape2D_property_one_way_collision>`

.. rst-class:: classref-property-setget

- |void| **set_one_way_collision**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_one_way_collision_enabled**\ (\ )

Thiết lập xem hình dạng va chạm này chỉ nên phát hiện va chạm ở một phía (trên hoặc dưới) hay không.

\ **Lưu ý:** Thuộc tính này không có tác dụng nếu **CollisionShape2D** này là node con của node :ref:`Area2D<class_Area2D>`.

\ **Lưu ý:** Có thể cấu hình hướng va chạm một chiều bằng cách thiết lập :ref:`one_way_collision_direction<class_CollisionShape2D_property_one_way_collision_direction>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape2D_property_one_way_collision_direction:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **one_way_collision_direction** = ``Vector2(0, 1)`` :ref:`🔗<class_CollisionShape2D_property_one_way_collision_direction>`

.. rst-class:: classref-property-setget

- |void| **set_one_way_collision_direction**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_one_way_collision_direction**\ (\ )

Hướng được sử dụng cho va chạm một chiều.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape2D_property_one_way_collision_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **one_way_collision_margin** = ``1.0`` :ref:`🔗<class_CollisionShape2D_property_one_way_collision_margin>`

.. rst-class:: classref-property-setget

- |void| **set_one_way_collision_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_one_way_collision_margin**\ (\ )

Khoảng đệm được sử dụng cho va chạm một chiều (tính bằng pixel). Giá trị cao hơn sẽ làm hình dạng dày hơn và hoạt động tốt hơn đối với các collider đi vào hình dạng với vận tốc cao.

.. rst-class:: classref-item-separator

----

.. _class_CollisionShape2D_property_shape:

.. rst-class:: classref-property

:ref:`Shape2D<class_Shape2D>` **shape** :ref:`🔗<class_CollisionShape2D_property_shape>`

.. rst-class:: classref-property-setget

- |void| **set_shape**\ (\ value\: :ref:`Shape2D<class_Shape2D>`\ ) - :ref:`Shape2D<class_Shape2D>` **get_shape**\ (\ )

Hình dạng thực tế do hình dạng va chạm này sở hữu.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
