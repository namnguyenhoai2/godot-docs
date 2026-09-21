:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Bộ tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CollisionPolygon2D.xml.

.. _class_CollisionPolygon2D:

CollisionPolygon2D
==================

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node cung cấp hình đa giác cho parent :ref:`CollisionObject2D<class_CollisionObject2D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node cung cấp hình đa giác cho parent :ref:`CollisionObject2D<class_CollisionObject2D>` và cho phép chỉnh sửa hình đó. Hình đa giác có thể lõm hoặc lồi. Hình này có thể tạo hình phát hiện cho một :ref:`Area2D<class_Area2D>`, biến một :ref:`PhysicsBody2D<class_PhysicsBody2D>` thành một đối tượng đặc, hoặc tạo hình rỗng cho một :ref:`StaticBody2D<class_StaticBody2D>`.

\ **Cảnh báo:** **CollisionPolygon2D** được scale không đồng đều có thể sẽ không hoạt động như mong đợi. Hãy đảm bảo scale của nó giống nhau trên tất cả các trục và thay vào đó điều chỉnh polygon của nó.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`BuildMode<enum_CollisionPolygon2D_BuildMode>` | :ref:`build_mode<class_CollisionPolygon2D_property_build_mode>`                                   | ``0``                    |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`disabled<class_CollisionPolygon2D_property_disabled>`                                       | ``false``                |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`one_way_collision<class_CollisionPolygon2D_property_one_way_collision>`                     | ``false``                |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`Vector2<class_Vector2>`                       | :ref:`one_way_collision_direction<class_CollisionPolygon2D_property_one_way_collision_direction>` | ``Vector2(0, 1)``        |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`one_way_collision_margin<class_CollisionPolygon2D_property_one_way_collision_margin>`       | ``1.0``                  |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`polygon<class_CollisionPolygon2D_property_polygon>`                                         | ``PackedVector2Array()`` |
   +-----------------------------------------------------+---------------------------------------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CollisionPolygon2D_BuildMode:

.. rst-class:: classref-enumeration

enum **BuildMode**: :ref:`🔗<enum_CollisionPolygon2D_BuildMode>`

.. _class_CollisionPolygon2D_constant_BUILD_SOLIDS:

.. rst-class:: classref-enumeration-constant

:ref:`BuildMode<enum_CollisionPolygon2D_BuildMode>` **BUILD_SOLIDS** = ``0``

Va chạm sẽ bao gồm polygon và vùng nằm bên trong nó. Ở chế độ này, node có tác dụng giống như nhiều node :ref:`ConvexPolygonShape2D<class_ConvexPolygonShape2D>`, mỗi node tương ứng với một hình lồi trong phép phân rã lồi của polygon (nhưng không chịu overhead của nhiều node).

.. _class_CollisionPolygon2D_constant_BUILD_SEGMENTS:

.. rst-class:: classref-enumeration-constant

:ref:`BuildMode<enum_CollisionPolygon2D_BuildMode>` **BUILD_SEGMENTS** = ``1``

Va chạm sẽ chỉ bao gồm các cạnh của polygon. Ở chế độ này, node có tác dụng giống như một :ref:`ConcavePolygonShape2D<class_ConcavePolygonShape2D>` duy nhất được tạo từ các đoạn, với giới hạn là mỗi đoạn (sau đoạn đầu tiên) bắt đầu tại nơi đoạn trước đó kết thúc, và đoạn cuối cùng kết thúc tại nơi đoạn đầu tiên bắt đầu (tạo thành một polygon khép kín nhưng rỗng).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CollisionPolygon2D_property_build_mode:

.. rst-class:: classref-property

:ref:`BuildMode<enum_CollisionPolygon2D_BuildMode>` **build_mode** = ``0`` :ref:`🔗<class_CollisionPolygon2D_property_build_mode>`

.. rst-class:: classref-property-setget

- |void| **set_build_mode**\ (\ value\: :ref:`BuildMode<enum_CollisionPolygon2D_BuildMode>`\ ) - :ref:`BuildMode<enum_CollisionPolygon2D_BuildMode>` **get_build_mode**\ (\ )

Chế độ tạo va chạm.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon2D_property_disabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disabled** = ``false`` :ref:`🔗<class_CollisionPolygon2D_property_disabled>`

.. rst-class:: classref-property-setget

- |void| **set_disabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_disabled**\ (\ )

Nếu ``true``, sẽ không phát hiện va chạm nào. Thuộc tính này nên được thay đổi bằng :ref:`Object.set_deferred()<class_Object_method_set_deferred>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon2D_property_one_way_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **one_way_collision** = ``false`` :ref:`🔗<class_CollisionPolygon2D_property_one_way_collision>`

.. rst-class:: classref-property-setget

- |void| **set_one_way_collision**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_one_way_collision_enabled**\ (\ )

Nếu ``true``, chỉ các cạnh hướng lên trên, tính theo rotation của **CollisionPolygon2D**, mới va chạm với các đối tượng khác.

\ **Lưu ý:** Thuộc tính này không có tác dụng nếu **CollisionPolygon2D** này là node con của một node :ref:`Area2D<class_Area2D>`.

\ **Lưu ý:** Có thể cấu hình hướng va chạm một chiều bằng cách thiết lập :ref:`one_way_collision_direction<class_CollisionPolygon2D_property_one_way_collision_direction>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon2D_property_one_way_collision_direction:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **one_way_collision_direction** = ``Vector2(0, 1)`` :ref:`🔗<class_CollisionPolygon2D_property_one_way_collision_direction>`

.. rst-class:: classref-property-setget

- |void| **set_one_way_collision_direction**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_one_way_collision_direction**\ (\ )

Hướng được sử dụng cho va chạm một chiều.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon2D_property_one_way_collision_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **one_way_collision_margin** = ``1.0`` :ref:`🔗<class_CollisionPolygon2D_property_one_way_collision_margin>`

.. rst-class:: classref-property-setget

- |void| **set_one_way_collision_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_one_way_collision_margin**\ (\ )

Margin được sử dụng cho va chạm một chiều (tính bằng pixel). Giá trị cao hơn sẽ làm hình dày hơn và hoạt động tốt hơn đối với các collider đi vào polygon với vận tốc cao.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon2D_property_polygon:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **polygon** = ``PackedVector2Array()`` :ref:`🔗<class_CollisionPolygon2D_property_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_polygon**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_polygon**\ (\ )

Danh sách các đỉnh của polygon. Mỗi điểm sẽ được nối với điểm tiếp theo, và điểm cuối cùng sẽ được nối với điểm đầu tiên.

\ **Lưu ý:** Các đỉnh được trả về nằm trong không gian tọa độ cục bộ của **CollisionPolygon2D** đã cho.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
