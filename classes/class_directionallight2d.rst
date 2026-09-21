:github_url: hide

.. meta::
	:keywords: sun

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/DirectionalLight2D.xml.

.. _class_DirectionalLight2D:

DirectionalLight2D
==================

**Kế thừa:** :ref:`Light2D<class_Light2D>` **<** :ref:`Node2D<class_Node2D>` **<** :ref:`CanvasItem<class_CanvasItem>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Đèn 2D định hướng từ xa.

.. rst-class:: classref-introduction-group

Mô tả
-----

Đèn định hướng là một loại node :ref:`Light2D<class_Light2D>` mô phỏng vô số tia song song bao phủ toàn bộ scene. Nó được dùng cho các đèn có cường độ mạnh và nằm rất xa scene (ví dụ: để mô phỏng ánh sáng mặt trời hoặc ánh trăng).

Ánh sáng được phát ra theo hướng +Y của global basis của node. Với một đèn chưa xoay, điều này có nghĩa là ánh sáng được phát ra theo hướng xuống dưới. Vị trí của node bị bỏ qua; chỉ basis được dùng để xác định hướng của ánh sáng.

\ **Lưu ý:** **DirectionalLight2D** không hỗ trợ light cull masks (nhưng hỗ trợ shadow cull masks). Nó sẽ luôn chiếu sáng các node 2D, bất kể :ref:`CanvasItem.light_mask<class_CanvasItem_property_light_mask>` của node 2D là gì.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Đèn và bóng 2D <../tutorials/2d/2d_lights_and_shadows>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`height<class_DirectionalLight2D_property_height>`             | ``0.0``     |
   +---------------------------+---------------------------------------------------------------------+-------------+
   | :ref:`float<class_float>` | :ref:`max_distance<class_DirectionalLight2D_property_max_distance>` | ``10000.0`` |
   +---------------------------+---------------------------------------------------------------------+-------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_DirectionalLight2D_property_height:

.. rst-class:: classref-property

:ref:`float<class_float>` **height** = ``0.0`` :ref:`🔗<class_DirectionalLight2D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_height**\ (\ )

Độ cao của đèn. Được dùng với 2D normal mapping. Có giá trị từ 0 (song song với mặt phẳng) đến 1 (vuông góc với mặt phẳng).

.. rst-class:: classref-item-separator

----

.. _class_DirectionalLight2D_property_max_distance:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_distance** = ``10000.0`` :ref:`🔗<class_DirectionalLight2D_property_max_distance>`

.. rst-class:: classref-property-setget

- |void| **set_max_distance**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_distance**\ (\ )

Khoảng cách tối đa tính từ tâm camera mà các đối tượng có thể ở trước khi bóng của chúng bị loại bỏ (tính bằng pixel). Giảm giá trị này có thể ngăn các đối tượng nằm ngoài camera tạo bóng (đồng thời cải thiện hiệu năng). :ref:`Camera2D.zoom<class_Camera2D_property_zoom>` không được tính đến bởi :ref:`max_distance<class_DirectionalLight2D_property_max_distance>`, nghĩa là ở các giá trị zoom cao hơn, bóng sẽ có vẻ mờ dần sớm hơn khi zoom vào một điểm nhất định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
