:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CanvasLayer.xml.

.. _class_CanvasLayer:

CanvasLayer
===========

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ParallaxBackground<class_ParallaxBackground>`

Một node được dùng để render độc lập các đối tượng trong một scene 2D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các node bắt nguồn từ :ref:`CanvasItem<class_CanvasItem>` là các node con trực tiếp hoặc gián tiếp của **CanvasLayer** sẽ được vẽ trong layer đó. Layer là một chỉ mục dạng số xác định thứ tự vẽ. Scene 2D mặc định được render với chỉ mục ``0``, vì vậy **CanvasLayer** có chỉ mục ``-1`` sẽ được vẽ bên dưới, còn **CanvasLayer** có chỉ mục ``1`` sẽ được vẽ bên trên. Thứ tự này vẫn được giữ nguyên bất kể :ref:`CanvasItem.z_index<class_CanvasItem_property_z_index>` của các node trong mỗi layer.

\ Các **CanvasLayer** có thể được ẩn và cũng có thể tùy chọn bám theo viewport. Điều này khiến chúng hữu ích cho các HUD như lớp phủ thanh máu (trên các layer ``1`` trở lên) hoặc background (trên các layer ``-1`` trở xuống).

\ **Lưu ý:** Các :ref:`Window<class_Window>` được nhúng được đặt trên layer ``1024``. Các :ref:`CanvasItem<class_CanvasItem>` trên layer ``1025`` trở lên sẽ xuất hiện phía trước các cửa sổ được nhúng.

\ **Lưu ý:** Mỗi **CanvasLayer** được vẽ trên một :ref:`Viewport<class_Viewport>` cụ thể và không thể được dùng chung giữa nhiều :ref:`Viewport<class_Viewport>`, xem :ref:`custom_viewport<class_CanvasLayer_property_custom_viewport>`. Khi sử dụng nhiều :ref:`Viewport<class_Viewport>`, chẳng hạn trong một game chia đôi màn hình, bạn cần tạo một **CanvasLayer** riêng cho mỗi :ref:`Viewport<class_Viewport>` mà bạn muốn nó được vẽ trên đó.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Viewport và các phép biến đổi canvas <../tutorials/2d/2d_transforms>`

- :doc:`Các canvas layer <../tutorials/2d/canvas_layers>`

- `2D Dodge The Creeps Demo <https://godotengine.org/asset-library/asset/2712>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Node<class_Node>`               | :ref:`custom_viewport<class_CanvasLayer_property_custom_viewport>`                 |                                   |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`follow_viewport_enabled<class_CanvasLayer_property_follow_viewport_enabled>` | ``false``                         |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`             | :ref:`follow_viewport_scale<class_CanvasLayer_property_follow_viewport_scale>`     | ``1.0``                           |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`int<class_int>`                 | :ref:`layer<class_CanvasLayer_property_layer>`                                     | ``1``                             |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`offset<class_CanvasLayer_property_offset>`                                   | ``Vector2(0, 0)``                 |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`float<class_float>`             | :ref:`rotation<class_CanvasLayer_property_rotation>`                               | ``0.0``                           |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Vector2<class_Vector2>`         | :ref:`scale<class_CanvasLayer_property_scale>`                                     | ``Vector2(1, 1)``                 |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`transform<class_CanvasLayer_property_transform>`                             | ``Transform2D(1, 0, 0, 1, 0, 0)`` |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`visible<class_CanvasLayer_property_visible>`                                 | ``true``                          |
   +---------------------------------------+------------------------------------------------------------------------------------+-----------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>`                 | :ref:`get_canvas<class_CanvasLayer_method_get_canvas>`\ (\ ) |const|                   |
   +---------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`get_final_transform<class_CanvasLayer_method_get_final_transform>`\ (\ ) |const| |
   +---------------------------------------+----------------------------------------------------------------------------------------+
   | |void|                                | :ref:`hide<class_CanvasLayer_method_hide>`\ (\ )                                       |
   +---------------------------------------+----------------------------------------------------------------------------------------+
   | |void|                                | :ref:`show<class_CanvasLayer_method_show>`\ (\ )                                       |
   +---------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Tín hiệu
--------

.. _class_CanvasLayer_signal_visibility_changed:

.. rst-class:: classref-signal

**visibility_changed**\ (\ ) :ref:`🔗<class_CanvasLayer_signal_visibility_changed>`

Được phát khi khả năng hiển thị của layer thay đổi. Xem :ref:`visible<class_CanvasLayer_property_visible>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CanvasLayer_property_custom_viewport:

.. rst-class:: classref-property

:ref:`Node<class_Node>` **custom_viewport** :ref:`🔗<class_CanvasLayer_property_custom_viewport>`

.. rst-class:: classref-property-setget

- |void| **set_custom_viewport**\ (\ value\: :ref:`Node<class_Node>`\ ) - :ref:`Node<class_Node>` **get_custom_viewport**\ (\ )

Node :ref:`Viewport<class_Viewport>` tùy chỉnh được gán cho **CanvasLayer**. Nếu là ``null``, thay vào đó sẽ sử dụng viewport mặc định.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_follow_viewport_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **follow_viewport_enabled** = ``false`` :ref:`🔗<class_CanvasLayer_property_follow_viewport_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_follow_viewport**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_following_viewport**\ (\ )

Khi được bật, **CanvasLayer** duy trì vị trí của nó trong không gian thế giới. Khi bị tắt, **CanvasLayer** giữ nguyên tại một vị trí cố định trên màn hình.

Kết hợp với :ref:`follow_viewport_scale<class_CanvasLayer_property_follow_viewport_scale>`, tính năng này có thể được dùng để tạo hiệu ứng pseudo-3D.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_follow_viewport_scale:

.. rst-class:: classref-property

:ref:`float<class_float>` **follow_viewport_scale** = ``1.0`` :ref:`🔗<class_CanvasLayer_property_follow_viewport_scale>`

.. rst-class:: classref-property-setget

- |void| **set_follow_viewport_scale**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_follow_viewport_scale**\ (\ )

Scale layer khi sử dụng :ref:`follow_viewport_enabled<class_CanvasLayer_property_follow_viewport_enabled>`. Các layer di chuyển vào foreground nên có scale tăng dần, trong khi các layer di chuyển vào background nên có scale giảm dần.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_layer:

.. rst-class:: classref-property

:ref:`int<class_int>` **layer** = ``1`` :ref:`🔗<class_CanvasLayer_property_layer>`

.. rst-class:: classref-property-setget

- |void| **set_layer**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_layer**\ (\ )

Chỉ mục layer cho thứ tự vẽ. Các giá trị thấp hơn được vẽ phía sau các giá trị cao hơn.

\ **Lưu ý:** Nếu nhiều CanvasLayer có cùng chỉ mục layer, các node con :ref:`CanvasItem<class_CanvasItem>` của một CanvasLayer sẽ được vẽ phía sau các node con :ref:`CanvasItem<class_CanvasItem>` của CanvasLayer còn lại. CanvasLayer nào được vẽ phía trước là không xác định.

\ **Lưu ý:** Chỉ mục layer phải nằm giữa :ref:`RenderingServer.CANVAS_LAYER_MIN<class_RenderingServer_constant_CANVAS_LAYER_MIN>` và :ref:`RenderingServer.CANVAS_LAYER_MAX<class_RenderingServer_constant_CANVAS_LAYER_MAX>` (bao gồm cả hai). Mọi giá trị khác sẽ quay vòng.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **offset** = ``Vector2(0, 0)`` :ref:`🔗<class_CanvasLayer_property_offset>`

.. rst-class:: classref-property-setget

- |void| **set_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_offset**\ (\ )

Offset cơ sở của layer.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_rotation:

.. rst-class:: classref-property

:ref:`float<class_float>` **rotation** = ``0.0`` :ref:`🔗<class_CanvasLayer_property_rotation>`

.. rst-class:: classref-property-setget

- |void| **set_rotation**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_rotation**\ (\ )

Rotation của layer tính bằng radian.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **scale** = ``Vector2(1, 1)`` :ref:`🔗<class_CanvasLayer_property_scale>`

.. rst-class:: classref-property-setget

- |void| **set_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_scale**\ (\ )

Scale của layer.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **transform** = ``Transform2D(1, 0, 0, 1, 0, 0)`` :ref:`🔗<class_CanvasLayer_property_transform>`

.. rst-class:: classref-property-setget

- |void| **set_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_transform**\ (\ )

Transform của layer.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_property_visible:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **visible** = ``true`` :ref:`🔗<class_CanvasLayer_property_visible>`

.. rst-class:: classref-property-setget

- |void| **set_visible**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_visible**\ (\ )

Nếu ``false``, mọi :ref:`CanvasItem<class_CanvasItem>` bên dưới **CanvasLayer** này sẽ bị ẩn.

Không giống :ref:`CanvasItem.visible<class_CanvasItem_property_visible>`, khả năng hiển thị của **CanvasLayer** không được truyền đến các layer bên dưới.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CanvasLayer_method_get_canvas:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_canvas**\ (\ ) |const| :ref:`🔗<class_CanvasLayer_method_get_canvas>`

Trả về RID của canvas được layer này sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_method_get_final_transform:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **get_final_transform**\ (\ ) |const| :ref:`🔗<class_CanvasLayer_method_get_final_transform>`

Trả về transform từ hệ tọa độ của **CanvasLayer** đến hệ tọa độ của :ref:`Viewport<class_Viewport>`.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_method_hide:

.. rst-class:: classref-method

|void| **hide**\ (\ ) :ref:`🔗<class_CanvasLayer_method_hide>`

Ẩn mọi :ref:`CanvasItem<class_CanvasItem>` bên dưới **CanvasLayer** này. Tương đương với việc đặt :ref:`visible<class_CanvasLayer_property_visible>` thành ``false``.

.. rst-class:: classref-item-separator

----

.. _class_CanvasLayer_method_show:

.. rst-class:: classref-method

|void| **show**\ (\ ) :ref:`🔗<class_CanvasLayer_method_show>`

Hiển thị mọi :ref:`CanvasItem<class_CanvasItem>` bên dưới **CanvasLayer** này. Tương đương với việc đặt :ref:`visible<class_CanvasLayer_property_visible>` thành ``true``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
