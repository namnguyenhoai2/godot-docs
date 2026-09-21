:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Node2D.xml.

.. _class_Node2D:

Node2D
======

**Kế thừa:** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`AnimatedSprite2D<class_AnimatedSprite2D>`, :ref:`AudioListener2D<class_AudioListener2D>`, :ref:`AudioStreamPlayer2D<class_AudioStreamPlayer2D>`, :ref:`BackBufferCopy<class_BackBufferCopy>`, :ref:`Bone2D<class_Bone2D>`, :ref:`Camera2D<class_Camera2D>`, :ref:`CanvasGroup<class_CanvasGroup>`, :ref:`CanvasModulate<class_CanvasModulate>`, :ref:`CollisionObject2D<class_CollisionObject2D>`, :ref:`CollisionPolygon2D<class_CollisionPolygon2D>`, :ref:`CollisionShape2D<class_CollisionShape2D>`, :ref:`CPUParticles2D<class_CPUParticles2D>`, :ref:`GPUParticles2D<class_GPUParticles2D>`, :ref:`Joint2D<class_Joint2D>`, :ref:`Light2D<class_Light2D>`, :ref:`LightOccluder2D<class_LightOccluder2D>`, :ref:`Line2D<class_Line2D>`, :ref:`Marker2D<class_Marker2D>`, :ref:`MeshInstance2D<class_MeshInstance2D>`, :ref:`MultiMeshInstance2D<class_MultiMeshInstance2D>`, :ref:`NavigationLink2D<class_NavigationLink2D>`, :ref:`NavigationObstacle2D<class_NavigationObstacle2D>`, :ref:`NavigationRegion2D<class_NavigationRegion2D>`, :ref:`Parallax2D<class_Parallax2D>`, :ref:`ParallaxLayer<class_ParallaxLayer>`, :ref:`Path2D<class_Path2D>`, :ref:`PathFollow2D<class_PathFollow2D>`, :ref:`Polygon2D<class_Polygon2D>`, :ref:`RayCast2D<class_RayCast2D>`, :ref:`RemoteTransform2D<class_RemoteTransform2D>`, :ref:`ShapeCast2D<class_ShapeCast2D>`, :ref:`Skeleton2D<class_Skeleton2D>`, :ref:`Sprite2D<class_Sprite2D>`, :ref:`TileMap<class_TileMap>`, :ref:`TileMapLayer<class_TileMapLayer>`, :ref:`TouchScreenButton<class_TouchScreenButton>`, :ref:`VisibleOnScreenNotifier2D<class_VisibleOnScreenNotifier2D>`

Một game object 2D, được tất cả các node liên quan đến 2D kế thừa. Có position, rotation, scale và skew.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một game object 2D có transform (position, rotation và scale). Tất cả node 2D, bao gồm các physics object và sprite, đều kế thừa từ Node2D. Sử dụng Node2D làm node cha để di chuyển, scale và rotate các node con trong một project 2D. Node này cũng cho phép kiểm soát thứ tự render của node.

\ **Lưu ý:** Vì cả **Node2D** và :ref:`Control<class_Control>` đều kế thừa từ :ref:`CanvasItem<class_CanvasItem>`, chúng chia sẻ một số khái niệm của class, chẳng hạn như các thuộc tính :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` và :ref:`CanvasItem.visible<class_CanvasItem_property_visible>`.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Vẽ tùy chỉnh trong 2D <../tutorials/2d/custom_drawing_in_2d>`

- `All 2D Demos <https://github.com/godotengine/godot-demo-projects/tree/master/2d>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`global_position<class_Node2D_property_global_position>`                 |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`             | :ref:`global_rotation<class_Node2D_property_global_rotation>`                 |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`             | :ref:`global_rotation_degrees<class_Node2D_property_global_rotation_degrees>` |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`global_scale<class_Node2D_property_global_scale>`                       |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`             | :ref:`global_skew<class_Node2D_property_global_skew>`                         |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`global_transform<class_Node2D_property_global_transform>`               |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`position<class_Node2D_property_position>`                               | ``Vector2(0, 0)`` |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`             | :ref:`rotation<class_Node2D_property_rotation>`                               | ``0.0``           |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`             | :ref:`rotation_degrees<class_Node2D_property_rotation_degrees>`               |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`scale<class_Node2D_property_scale>`                                     | ``Vector2(1, 1)`` |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`float<class_float>`             | :ref:`skew<class_Node2D_property_skew>`                                       | ``0.0``           |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`transform<class_Node2D_property_transform>`                             |                   |
   +---------------------------------------+-------------------------------------------------------------------------------+-------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`apply_scale<class_Node2D_method_apply_scale>`\ (\ ratio\: :ref:`Vector2<class_Vector2>`\ )                                              |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`             | :ref:`get_angle_to<class_Node2D_method_get_angle_to>`\ (\ point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                    |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`get_relative_transform_to_parent<class_Node2D_method_get_relative_transform_to_parent>`\ (\ parent\: :ref:`Node<class_Node>`\ ) |const| |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`global_translate<class_Node2D_method_global_translate>`\ (\ offset\: :ref:`Vector2<class_Vector2>`\ )                                   |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`look_at<class_Node2D_method_look_at>`\ (\ point\: :ref:`Vector2<class_Vector2>`\ )                                                      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`move_local_x<class_Node2D_method_move_local_x>`\ (\ delta\: :ref:`float<class_float>`, scaled\: :ref:`bool<class_bool>` = false\ )      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`move_local_y<class_Node2D_method_move_local_y>`\ (\ delta\: :ref:`float<class_float>`, scaled\: :ref:`bool<class_bool>` = false\ )      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`rotate<class_Node2D_method_rotate>`\ (\ radians\: :ref:`float<class_float>`\ )                                                          |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`to_global<class_Node2D_method_to_global>`\ (\ local_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                    |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`to_local<class_Node2D_method_to_local>`\ (\ global_point\: :ref:`Vector2<class_Vector2>`\ ) |const|                                     |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`translate<class_Node2D_method_translate>`\ (\ offset\: :ref:`Vector2<class_Vector2>`\ )                                                 |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Node2D_property_global_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **global_position** :ref:`🔗<class_Node2D_property_global_position>`

.. rst-class:: classref-property-setget

- |void| **set_global_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_global_position**\ (\ )

Vị trí toàn cục. Xem thêm :ref:`position<class_Node2D_property_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_global_rotation:

.. rst-class:: classref-property

:ref:`float<class_float>` **global_rotation** :ref:`🔗<class_Node2D_property_global_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_global_rotation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_global_rotation**\ (\ )

Rotation toàn cục tính bằng radian. Xem thêm :ref:`rotation<class_Node2D_property_rotation>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_global_rotation_degrees:

.. rst-class:: classref-property

:ref:`float<class_float>` **global_rotation_degrees** :ref:`🔗<class_Node2D_property_global_rotation_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_global_rotation_degrees**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_global_rotation_degrees**\ (\ )

Thuộc tính hỗ trợ để truy cập :ref:`global_rotation<class_Node2D_property_global_rotation>` theo độ thay vì radian. Xem thêm :ref:`rotation_degrees<class_Node2D_property_rotation_degrees>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_global_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **global_scale** :ref:`🔗<class_Node2D_property_global_scale>`

.. rst-class:: classref-property-setget

- |void| **set_global_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_global_scale**\ (\ )

Scale toàn cục. Xem thêm :ref:`scale<class_Node2D_property_scale>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_global_skew:

.. rst-class:: classref-property

:ref:`float<class_float>` **global_skew** :ref:`🔗<class_Node2D_property_global_skew>`

.. rst-class:: classref-property-setget

- |void| **set_global_skew**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_global_skew**\ (\ )

Skew toàn cục tính bằng radian. Xem thêm :ref:`skew<class_Node2D_property_skew>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_global_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **global_transform** :ref:`🔗<class_Node2D_property_global_transform>`

.. rst-class:: classref-property-setget

- |void| **set_global_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_global_transform**\ (\ )

:ref:`Transform2D<class_Transform2D>` toàn cục. Xem thêm :ref:`transform<class_Node2D_property_transform>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_position:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **position** = ``Vector2(0, 0)`` :ref:`🔗<class_Node2D_property_position>`

.. rst-class:: classref-property-setget

- |void| **set_position**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_position**\ (\ )

Position, tương đối so với node cha. Xem thêm :ref:`global_position<class_Node2D_property_global_position>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_rotation:

.. rst-class:: classref-property

:ref:`float<class_float>` **rotation** = ``0.0`` :ref:`🔗<class_Node2D_property_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_rotation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rotation**\ (\ )

Rotation tính bằng radian, tương đối so với node cha. Xem thêm :ref:`global_rotation<class_Node2D_property_global_rotation>`.

\ **Lưu ý:** Thuộc tính này được chỉnh sửa trong inspector theo độ. Nếu muốn sử dụng độ trong script, hãy dùng :ref:`rotation_degrees<class_Node2D_property_rotation_degrees>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_rotation_degrees:

.. rst-class:: classref-property

:ref:`float<class_float>` **rotation_degrees** :ref:`🔗<class_Node2D_property_rotation_degrees>`

.. rst-class:: classref-property-setget

- |void| **set_rotation_degrees**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rotation_degrees**\ (\ )

Thuộc tính hỗ trợ để truy cập :ref:`rotation<class_Node2D_property_rotation>` theo độ thay vì radian. Xem thêm :ref:`global_rotation_degrees<class_Node2D_property_global_rotation_degrees>`.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scale** = ``Vector2(1, 1)`` :ref:`🔗<class_Node2D_property_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scale**\ (\ )

Scale của node, tương đối so với node cha. Giá trị không scale: ``(1, 1)``. Xem thêm :ref:`global_scale<class_Node2D_property_global_scale>`.

\ **Lưu ý:** Scale X âm trong 2D không thể phân rã từ ma trận biến đổi. Do cách scale được biểu diễn bằng các ma trận biến đổi trong Godot, scale âm trên trục X sẽ được thay đổi thành scale âm trên trục Y và rotation 180 độ khi được phân rã.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_skew:

.. rst-class:: classref-property

:ref:`float<class_float>` **skew** = ``0.0`` :ref:`🔗<class_Node2D_property_skew>`

.. rst-class:: classref-property-setget

- |void| **set_skew**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_skew**\ (\ )

Nếu được đặt thành giá trị khác 0, node sẽ bị nghiêng theo một hướng nào đó. Có thể dùng thuộc tính này cho các hiệu ứng pseudo-3D. Xem thêm :ref:`global_skew<class_Node2D_property_global_skew>`.

\ **Lưu ý:** Skew chỉ được thực hiện trên trục X và *giữa* rotation và scaling.

\ **Lưu ý:** Thuộc tính này được chỉnh sửa trong inspector theo độ. Nếu muốn sử dụng độ trong script, hãy dùng ``skew = deg_to_rad(value_in_degrees)``.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_property_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **transform** :ref:`🔗<class_Node2D_property_transform>`

.. rst-class:: classref-property-setget

- |void| **set_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_transform**\ (\ )

:ref:`Transform2D<class_Transform2D>` của node, tương đối so với node cha. Xem thêm :ref:`global_transform<class_Node2D_property_global_transform>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Node2D_method_apply_scale:

.. rst-class:: classref-method

|void| **apply_scale**\ (\ ratio\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Node2D_method_apply_scale>`

Nhân scale hiện tại với vector ``ratio``.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_get_angle_to:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_angle_to**\ (\ point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Node2D_method_get_angle_to>`

Trả về góc giữa node và ``point`` theo radian. Xem thêm :ref:`look_at()<class_Node2D_method_look_at>`.

\ `Illustration of the returned angle. <https://raw.githubusercontent.com/godotengine/godot-docs/master/img/node2d_get_angle_to.png>`__

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_get_relative_transform_to_parent:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **get_relative_transform_to_parent**\ (\ parent\: :ref:`Node<class_Node>`\ ) |const| :ref:`🔗<class_Node2D_method_get_relative_transform_to_parent>`

Trả về :ref:`Transform2D<class_Transform2D>` tương đối so với node cha của node này.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_global_translate:

.. rst-class:: classref-method

|void| **global_translate**\ (\ offset\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Node2D_method_global_translate>`

Cộng vector ``offset`` vào position toàn cục của node.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_look_at:

.. rst-class:: classref-method

|void| **look_at**\ (\ point\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Node2D_method_look_at>`

Xoay node để trục +X cục bộ hướng về ``point``, được kỳ vọng sử dụng tọa độ toàn cục. Phương thức này là sự kết hợp của cả :ref:`rotate()<class_Node2D_method_rotate>` và :ref:`get_angle_to()<class_Node2D_method_get_angle_to>`.

\ ``point`` không được trùng với position của node, nếu không node sẽ luôn hướng sang phải.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_move_local_x:

.. rst-class:: classref-method

|void| **move_local_x**\ (\ delta\: :ref:`float<class_float>`, scaled\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node2D_method_move_local_x>`

Áp dụng phép tịnh tiến cục bộ trên trục X của node với độ lớn được chỉ định trong ``delta``. Nếu ``scaled`` là ``false``, chuẩn hóa chuyển động để nó xảy ra độc lập với :ref:`scale<class_Node2D_property_scale>` của node.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_move_local_y:

.. rst-class:: classref-method

|void| **move_local_y**\ (\ delta\: :ref:`float<class_float>`, scaled\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_Node2D_method_move_local_y>`

Áp dụng phép tịnh tiến cục bộ trên trục Y của node với độ lớn được chỉ định trong ``delta``. Nếu ``scaled`` là ``false``, chuẩn hóa chuyển động để nó xảy ra độc lập với :ref:`scale<class_Node2D_property_scale>` của node.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_rotate:

.. rst-class:: classref-method

|void| **rotate**\ (\ radians\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Node2D_method_rotate>`

Áp dụng rotation cho node theo radian, bắt đầu từ rotation hiện tại. Tương đương với ``rotation += radians``.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_to_global:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **to_global**\ (\ local_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Node2D_method_to_global>`

Biến đổi position cục bộ được cung cấp thành position trong không gian tọa độ toàn cục. Đầu vào được kỳ vọng là tọa độ cục bộ tương đối so với **Node2D** mà phương thức được gọi trên đó. Ví dụ: Áp dụng phương thức này cho position của các node con sẽ biến đổi chính xác position của chúng sang không gian tọa độ toàn cục, nhưng áp dụng cho position của chính node đó sẽ cho kết quả không chính xác, vì nó sẽ kết hợp phép biến đổi của node vào position toàn cục của node.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_to_local:

.. rst-class:: classref-method

:ref:`Vector2<class_Vector2>` **to_local**\ (\ global_point\: :ref:`Vector2<class_Vector2>`\ ) |const| :ref:`🔗<class_Node2D_method_to_local>`

Chuyển đổi vị trí global được cung cấp thành một vị trí trong hệ tọa độ local. Kết quả sẽ là vị trí local tương đối với **Node2D** mà hàm được gọi trên đó. Ví dụ: hàm này phù hợp để xác định vị trí của các node con, nhưng không phù hợp để xác định vị trí của chính nó tương đối với node cha.

.. rst-class:: classref-item-separator

----

.. _class_Node2D_method_translate:

.. rst-class:: classref-method

|void| **translate**\ (\ offset\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_Node2D_method_translate>`

Dịch node theo ``offset`` đã cho trong tọa độ local. Tương đương với ``position += offset``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
