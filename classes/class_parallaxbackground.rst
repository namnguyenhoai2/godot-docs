:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ParallaxBackground.xml.

.. _class_ParallaxBackground:

ParallaxBackground
==================

**Đã lỗi thời:** Thay vào đó, hãy sử dụng node :ref:`Parallax2D<class_Parallax2D>`.

**Kế thừa:** :ref:`CanvasLayer<class_CanvasLayer>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node được dùng để tạo background cuộn parallax.

.. rst-class:: classref-introduction-group

Mô tả
-----

ParallaxBackground sử dụng một hoặc nhiều node con :ref:`ParallaxLayer<class_ParallaxLayer>` để tạo hiệu ứng parallax. Mỗi :ref:`ParallaxLayer<class_ParallaxLayer>` có thể di chuyển với tốc độ khác nhau bằng cách sử dụng :ref:`ParallaxLayer.motion_offset<class_ParallaxLayer_property_motion_offset>`. Điều này tạo ra ảo giác về chiều sâu trong game 2D. Nếu không được sử dụng cùng với một :ref:`Camera2D<class_Camera2D>`, bạn phải tự tính toán :ref:`scroll_offset<class_ParallaxBackground_property_scroll_offset>`.

\ **Lưu ý:** Mỗi **ParallaxBackground** được vẽ trên một :ref:`Viewport<class_Viewport>` cụ thể và không thể được dùng chung giữa nhiều :ref:`Viewport<class_Viewport>`\ s, xem :ref:`CanvasLayer.custom_viewport<class_CanvasLayer_property_custom_viewport>`. Khi sử dụng nhiều :ref:`Viewport<class_Viewport>`\ s, chẳng hạn trong game có màn hình chia đôi, bạn cần tạo một **ParallaxBackground** riêng cho mỗi :ref:`Viewport<class_Viewport>` mà bạn muốn nó được vẽ trên đó.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`int<class_int>`         | layer                                                                                         | ``-100`` (overrides :ref:`CanvasLayer<class_CanvasLayer_property_layer>`) |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`scroll_base_offset<class_ParallaxBackground_property_scroll_base_offset>`               | ``Vector2(0, 0)``                                                         |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`scroll_base_scale<class_ParallaxBackground_property_scroll_base_scale>`                 | ``Vector2(1, 1)``                                                         |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`scroll_ignore_camera_zoom<class_ParallaxBackground_property_scroll_ignore_camera_zoom>` | ``false``                                                                 |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`scroll_limit_begin<class_ParallaxBackground_property_scroll_limit_begin>`               | ``Vector2(0, 0)``                                                         |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`scroll_limit_end<class_ParallaxBackground_property_scroll_limit_end>`                   | ``Vector2(0, 0)``                                                         |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`scroll_offset<class_ParallaxBackground_property_scroll_offset>`                         | ``Vector2(0, 0)``                                                         |
   +-------------------------------+-----------------------------------------------------------------------------------------------+---------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ParallaxBackground_property_scroll_base_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_base_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_ParallaxBackground_property_scroll_base_offset>`

.. rst-class:: classref-property-setget

- |void| **set_scroll_base_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scroll_base_offset**\ (\ )

Độ lệch vị trí cơ sở cho tất cả các node con :ref:`ParallaxLayer<class_ParallaxLayer>`.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxBackground_property_scroll_base_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_base_scale** = ``Vector2(1, 1)`` :ref:`🔗<class_ParallaxBackground_property_scroll_base_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scroll_base_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scroll_base_scale**\ (\ )

Tỷ lệ chuyển động cơ sở cho tất cả các node con :ref:`ParallaxLayer<class_ParallaxLayer>`.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxBackground_property_scroll_ignore_camera_zoom:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **scroll_ignore_camera_zoom** = ``false`` :ref:`🔗<class_ParallaxBackground_property_scroll_ignore_camera_zoom>`

.. rst-class:: classref-property-setget

- |void| **set_ignore_camera_zoom**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_ignore_camera_zoom**\ (\ )

Nếu ``true``, các phần tử trong node con :ref:`ParallaxLayer<class_ParallaxLayer>` sẽ không bị ảnh hưởng bởi mức zoom của camera.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxBackground_property_scroll_limit_begin:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_limit_begin** = ``Vector2(0, 0)`` :ref:`🔗<class_ParallaxBackground_property_scroll_limit_begin>`

.. rst-class:: classref-property-setget

- |void| **set_limit_begin**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_limit_begin**\ (\ )

Giới hạn góc trên bên trái để bắt đầu cuộn. Nếu camera nằm ngoài giới hạn này, background sẽ dừng cuộn. Phải nhỏ hơn :ref:`scroll_limit_end<class_ParallaxBackground_property_scroll_limit_end>` thì mới hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxBackground_property_scroll_limit_end:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_limit_end** = ``Vector2(0, 0)`` :ref:`🔗<class_ParallaxBackground_property_scroll_limit_end>`

.. rst-class:: classref-property-setget

- |void| **set_limit_end**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_limit_end**\ (\ )

Giới hạn góc dưới bên phải để kết thúc cuộn. Nếu camera nằm ngoài giới hạn này, background sẽ dừng cuộn. Phải lớn hơn :ref:`scroll_limit_begin<class_ParallaxBackground_property_scroll_limit_begin>` thì mới hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxBackground_property_scroll_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scroll_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_ParallaxBackground_property_scroll_offset>`

.. rst-class:: classref-property-setget

- |void| **set_scroll_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scroll_offset**\ (\ )

Giá trị cuộn của ParallaxBackground. Được tự động tính toán khi sử dụng một :ref:`Camera2D<class_Camera2D>`, nhưng có thể được dùng để quản lý việc cuộn thủ công khi không có camera.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
