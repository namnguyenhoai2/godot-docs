:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Parallax2D.xml.

.. _class_Parallax2D:

Parallax2D
==========

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node dùng để tạo background cuộn parallax.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một **Parallax2D** được dùng để tạo hiệu ứng parallax. Nó có thể di chuyển với tốc độ khác so với chuyển động của camera bằng :ref:`scroll_scale<class_Parallax2D_property_scroll_scale>`. Điều này tạo ra ảo giác về chiều sâu trong game 2D. Nếu muốn cuộn thủ công, có thể bỏ qua vị trí :ref:`Camera2D<class_Camera2D>` bằng :ref:`ignore_camera_scroll<class_Parallax2D_property_ignore_camera_scroll>`.

\ **Lưu ý:** Mọi thay đổi đối với vị trí của node này sau khi nó đi vào scene tree sẽ bị ghi đè nếu :ref:`ignore_camera_scroll<class_Parallax2D_property_ignore_camera_scroll>` là ``false`` hoặc :ref:`screen_offset<class_Parallax2D_property_screen_offset>` bị sửa đổi.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`2D Parallax <../tutorials/2d/2d_parallax>`

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`autoscroll<class_Parallax2D_property_autoscroll>`                     | ``Vector2(0, 0)``                                                             |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`follow_viewport<class_Parallax2D_property_follow_viewport>`           | ``true``                                                                      |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                                             | :ref:`ignore_camera_scroll<class_Parallax2D_property_ignore_camera_scroll>` | ``false``                                                                     |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`limit_begin<class_Parallax2D_property_limit_begin>`                   | ``Vector2(-10000000, -10000000)``                                             |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`limit_end<class_Parallax2D_property_limit_end>`                       | ``Vector2(10000000, 10000000)``                                               |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` | physics_interpolation_mode                                                  | ``2`` (overrides :ref:`Node<class_Node_property_physics_interpolation_mode>`) |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`repeat_size<class_Parallax2D_property_repeat_size>`                   | ``Vector2(0, 0)``                                                             |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                               | :ref:`repeat_times<class_Parallax2D_property_repeat_times>`                 | ``1``                                                                         |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`screen_offset<class_Parallax2D_property_screen_offset>`               | ``Vector2(0, 0)``                                                             |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`scroll_offset<class_Parallax2D_property_scroll_offset>`               | ``Vector2(0, 0)``                                                             |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`scroll_scale<class_Parallax2D_property_scroll_scale>`                 | ``Vector2(1, 1)``                                                             |
   +---------------------------------------------------------------------+-----------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Parallax2D_property_autoscroll:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **autoscroll** = ``Vector2(0, 0)`` :ref:`🔗<class_Parallax2D_property_autoscroll>`

.. rst-class:: classref-property-setget

- |void| **set_autoscroll**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_autoscroll**\ (\ )

Tốc độ mà offset tự động cuộn, tính bằng pixel mỗi giây.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_follow_viewport:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **follow_viewport** = ``true`` :ref:`🔗<class_Parallax2D_property_follow_viewport>`

.. rst-class:: classref-property-setget

- |void| **set_follow_viewport**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_follow_viewport**\ (\ )

Nếu ``true``, **Parallax2D** sẽ được offset theo vị trí của camera hiện tại. Nếu **Parallax2D** nằm trong một :ref:`CanvasLayer<class_CanvasLayer>` riêng biệt với camera hiện tại, có thể cần đặt giá trị này khớp với :ref:`CanvasLayer.follow_viewport_enabled<class_CanvasLayer_property_follow_viewport_enabled>`.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_ignore_camera_scroll:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **ignore_camera_scroll** = ``false`` :ref:`🔗<class_Parallax2D_property_ignore_camera_scroll>`

.. rst-class:: classref-property-setget

- |void| **set_ignore_camera_scroll**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_ignore_camera_scroll**\ (\ )

Nếu ``true``, vị trí của **Parallax2D** không bị ảnh hưởng bởi vị trí của camera.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_limit_begin:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **limit_begin** = ``Vector2(-10000000, -10000000)`` :ref:`🔗<class_Parallax2D_property_limit_begin>`

.. rst-class:: classref-property-setget

- |void| **set_limit_begin**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_limit_begin**\ (\ )

Giới hạn trên-trái để bắt đầu cuộn. Nếu camera nằm ngoài giới hạn này, **Parallax2D** sẽ dừng cuộn. Để hoạt động, giá trị này phải nhỏ hơn :ref:`limit_end<class_Parallax2D_property_limit_end>` trừ đi kích thước viewport.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_limit_end:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **limit_end** = ``Vector2(10000000, 10000000)`` :ref:`🔗<class_Parallax2D_property_limit_end>`

.. rst-class:: classref-property-setget

- |void| **set_limit_end**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_limit_end**\ (\ )

Giới hạn dưới-phải để kết thúc cuộn. Nếu camera nằm ngoài giới hạn này, **Parallax2D** sẽ dừng cuộn. Để hoạt động, giá trị này phải lớn hơn :ref:`limit_begin<class_Parallax2D_property_limit_begin>` cộng với kích thước viewport.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_repeat_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **repeat_size** = ``Vector2(0, 0)`` :ref:`🔗<class_Parallax2D_property_repeat_size>`

.. rst-class:: classref-property-setget

- |void| **set_repeat_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_repeat_size**\ (\ )

Lặp lại :ref:`Texture2D<class_Texture2D>` của từng node con của node này và offset chúng theo giá trị này. Khi cuộn, vị trí của node sẽ lặp lại, tạo ảo giác về một background cuộn vô hạn nếu các giá trị lớn hơn kích thước màn hình. Nếu một trục được đặt thành ``0``, :ref:`Texture2D<class_Texture2D>` sẽ không được lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_repeat_times:

.. rst-class:: classref-property

:ref:`int<class_int>` **repeat_times** = ``1`` :ref:`🔗<class_Parallax2D_property_repeat_times>`

.. rst-class:: classref-property-setget

- |void| **set_repeat_times**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_repeat_times**\ (\ )

Ghi đè số lần texture được lặp lại. Mỗi bản sao của texture được trải đều từ bản gốc theo :ref:`repeat_size<class_Parallax2D_property_repeat_size>`. Hữu ích khi thu nhỏ camera.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_screen_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **screen_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Parallax2D_property_screen_offset>`

.. rst-class:: classref-property-setget

- |void| **set_screen_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_screen_offset**\ (\ )

Offset được dùng để cuộn **Parallax2D** này. Giá trị này được tự động cập nhật trừ khi :ref:`ignore_camera_scroll<class_Parallax2D_property_ignore_camera_scroll>` là ``true``.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_scroll_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_Parallax2D_property_scroll_offset>`

.. rst-class:: classref-property-setget

- |void| **set_scroll_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scroll_offset**\ (\ )

Offset của **Parallax2D**. Tương tự :ref:`screen_offset<class_Parallax2D_property_screen_offset>` và :ref:`Node2D.position<class_Node2D_property_position>`, nhưng sẽ không bị ghi đè.

\ **Lưu ý:** Các giá trị sẽ lặp lại nếu :ref:`repeat_size<class_Parallax2D_property_repeat_size>` được đặt cao hơn ``0``.

.. rst-class:: classref-item-separator

----

.. _class_Parallax2D_property_scroll_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_scale** = ``Vector2(1, 1)`` :ref:`🔗<class_Parallax2D_property_scroll_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scroll_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scroll_scale**\ (\ )

Hệ số nhân cho offset cuối cùng của **Parallax2D**. Có thể dùng để mô phỏng khoảng cách đến camera.

Ví dụ, giá trị ``1`` sẽ cuộn với cùng tốc độ như camera. Giá trị lớn hơn ``1`` sẽ cuộn nhanh hơn, khiến các đối tượng có vẻ gần hơn. Giá trị nhỏ hơn ``1`` sẽ cuộn chậm hơn, khiến các đối tượng có vẻ xa hơn, còn giá trị ``0`` sẽ dừng hoàn toàn các đối tượng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
