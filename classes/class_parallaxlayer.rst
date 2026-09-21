:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ParallaxLayer.xml.

.. _class_ParallaxLayer:

ParallaxLayer
=============

**Đã lỗi thời:** Thay vào đó, hãy sử dụng node :ref:`Parallax2D<class_Parallax2D>`.

**Kế thừa:** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một layer cuộn parallax được sử dụng cùng với :ref:`ParallaxBackground<class_ParallaxBackground>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một ParallaxLayer phải là node con của một node :ref:`ParallaxBackground<class_ParallaxBackground>`. Mỗi ParallaxLayer có thể được thiết lập để di chuyển với tốc độ khác nhau tương đối so với chuyển động của camera hoặc giá trị :ref:`ParallaxBackground.scroll_offset<class_ParallaxBackground_property_scroll_offset>`.

Các node con của node này sẽ chịu ảnh hưởng của scroll offset của nó.

\ **Lưu ý:** Mọi thay đổi đối với position và scale của node này sau khi node đi vào scene sẽ bị bỏ qua.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`motion_mirroring<class_ParallaxLayer_property_motion_mirroring>` | ``Vector2(0, 0)``                                                             |
   +---------------------------------------------------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`motion_offset<class_ParallaxLayer_property_motion_offset>`       | ``Vector2(0, 0)``                                                             |
   +---------------------------------------------------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`                                       | :ref:`motion_scale<class_ParallaxLayer_property_motion_scale>`         | ``Vector2(1, 1)``                                                             |
   +---------------------------------------------------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+
   | :ref:`PhysicsInterpolationMode<enum_Node_PhysicsInterpolationMode>` | physics_interpolation_mode                                             | ``2`` (overrides :ref:`Node<class_Node_property_physics_interpolation_mode>`) |
   +---------------------------------------------------------------------+------------------------------------------------------------------------+-------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ParallaxLayer_property_motion_mirroring:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **motion_mirroring** = ``Vector2(0, 0)`` :ref:`🔗<class_ParallaxLayer_property_motion_mirroring>`

.. rst-class:: classref-property-setget

- |void| **set_mirroring**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_mirroring**\ (\ )

Khoảng lặp, tính theo pixel, mà tại đó **ParallaxLayer** được vẽ lặp lại. Hữu ích khi tạo background cuộn vô hạn. Nếu một trục được đặt thành ``0``, **ParallaxLayer** sẽ chỉ được vẽ một lần theo hướng đó.

\ **Lưu ý:** Nếu bạn muốn phần lặp khớp chính xác đến từng pixel với một :ref:`Texture2D<class_Texture2D>` được hiển thị bởi node con, bạn nên tính đến mọi scale được áp dụng cho texture khi xác định khoảng lặp này. Ví dụ, nếu bạn sử dụng một :ref:`Sprite2D<class_Sprite2D>` con được scale thành ``0.5`` để hiển thị texture 600x600 và muốn sprite này được lặp liên tục theo chiều ngang, bạn nên đặt giá trị mirroring thành ``Vector2(300, 0)``.

\ **Lưu ý:** Nếu độ dài của trục viewport lớn hơn hai lần kích thước trục được lặp, nó sẽ không lặp vô hạn, vì parallax layer chỉ vẽ 2 instance của layer tại bất kỳ thời điểm nào. Cửa sổ hiển thị được tính từ position của :ref:`ParallaxBackground<class_ParallaxBackground>` cha, không phải position của chính layer. Vì vậy, nếu sử dụng mirroring, **không được** thay đổi position của **ParallaxLayer** tương đối so với node cha. Thay vào đó, nếu cần điều chỉnh position của background, hãy thiết lập thuộc tính :ref:`CanvasLayer.offset<class_CanvasLayer_property_offset>` trong :ref:`ParallaxBackground<class_ParallaxBackground>` cha.

\ **Lưu ý:** Mặc dù có tên như vậy, layer sẽ không được mirror mà chỉ được lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxLayer_property_motion_offset:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **motion_offset** = ``Vector2(0, 0)`` :ref:`🔗<class_ParallaxLayer_property_motion_offset>`

.. rst-class:: classref-property-setget

- |void| **set_motion_offset**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_motion_offset**\ (\ )

Offset của ParallaxLayer tương đối so với :ref:`ParallaxBackground.scroll_offset<class_ParallaxBackground_property_scroll_offset>` của ParallaxBackground cha.

.. rst-class:: classref-item-separator

----

.. _class_ParallaxLayer_property_motion_scale:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **motion_scale** = ``Vector2(1, 1)`` :ref:`🔗<class_ParallaxLayer_property_motion_scale>`

.. rst-class:: classref-property-setget

- |void| **set_motion_scale**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_motion_scale**\ (\ )

Nhân chuyển động của ParallaxLayer. Nếu một trục được đặt thành ``0``, layer sẽ không cuộn.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
