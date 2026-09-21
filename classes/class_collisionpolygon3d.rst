:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CollisionPolygon3D.xml.

.. _class_CollisionPolygon3D:

CollisionPolygon3D
==================

**Kế thừa:** :ref:`Node3D<class_Node3D>` **<** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node cung cấp hình dạng đa giác được làm dày (một lăng trụ) cho parent :ref:`CollisionObject3D<class_CollisionObject3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node cung cấp hình dạng đa giác được làm dày (một lăng trụ) cho parent :ref:`CollisionObject3D<class_CollisionObject3D>` và cho phép chỉnh sửa hình dạng đó. Đa giác có thể lõm hoặc lồi. Điều này có thể cung cấp một hình dạng phát hiện cho :ref:`Area3D<class_Area3D>` hoặc biến :ref:`PhysicsBody3D<class_PhysicsBody3D>` thành một vật thể rắn.

\ **Cảnh báo:** :ref:`CollisionShape3D<class_CollisionShape3D>` được scale không đồng nhất có thể sẽ không hoạt động như mong đợi. Hãy đảm bảo scale của nó giống nhau trên tất cả các trục và thay vào đó điều chỉnh shape resource của nó.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+
   | :ref:`Color<class_Color>`                           | :ref:`debug_color<class_CollisionPolygon3D_property_debug_color>` | ``Color(0, 0, 0, 0)``    |
   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`debug_fill<class_CollisionPolygon3D_property_debug_fill>`   | ``true``                 |
   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`depth<class_CollisionPolygon3D_property_depth>`             | ``1.0``                  |
   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+
   | :ref:`bool<class_bool>`                             | :ref:`disabled<class_CollisionPolygon3D_property_disabled>`       | ``false``                |
   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+
   | :ref:`float<class_float>`                           | :ref:`margin<class_CollisionPolygon3D_property_margin>`           | ``0.04``                 |
   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`polygon<class_CollisionPolygon3D_property_polygon>`         | ``PackedVector2Array()`` |
   +-----------------------------------------------------+-------------------------------------------------------------------+--------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CollisionPolygon3D_property_debug_color:

.. rst-class:: classref-property

:ref:`Color<class_Color>` **debug_color** = ``Color(0, 0, 0, 0)`` :ref:`🔗<class_CollisionPolygon3D_property_debug_color>`

.. rst-class:: classref-property-setget

- |void| **set_debug_color**\ (\ value\: :ref:`Color<class_Color>`\ ) - :ref:`Color<class_Color>` **get_debug_color**\ (\ )

Màu collision shape được hiển thị trong editor hoặc trong project đang chạy nếu **Debug > Visible Collision Shapes** được chọn ở đầu editor.

\ **Lưu ý:** Giá trị mặc định là :ref:`ProjectSettings.debug/shapes/collision/shape_color<class_ProjectSettings_property_debug/shapes/collision/shape_color>`. Giá trị ``Color(0, 0, 0, 0)`` được ghi lại ở đây chỉ là placeholder, không phải màu debug mặc định thực tế.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon3D_property_debug_fill:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **debug_fill** = ``true`` :ref:`🔗<class_CollisionPolygon3D_property_debug_fill>`

.. rst-class:: classref-property-setget

- |void| **set_enable_debug_fill**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_enable_debug_fill**\ (\ )

Nếu ``true``, khi hình dạng được hiển thị, nó sẽ hiển thị một màu tô đặc bên cạnh wireframe.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon3D_property_depth:

.. rst-class:: classref-property

:ref:`float<class_float>` **depth** = ``1.0`` :ref:`🔗<class_CollisionPolygon3D_property_depth>`

.. rst-class:: classref-property-setget

- |void| **set_depth**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_depth**\ (\ )

Độ dài mà collision được tạo ra mở rộng theo cả hai hướng vuông góc với đa giác 2D của nó.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon3D_property_disabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **disabled** = ``false`` :ref:`🔗<class_CollisionPolygon3D_property_disabled>`

.. rst-class:: classref-property-setget

- |void| **set_disabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_disabled**\ (\ )

Nếu ``true``, sẽ không tạo ra collision nào. Nên thay đổi thuộc tính này bằng :ref:`Object.set_deferred()<class_Object_method_set_deferred>`.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon3D_property_margin:

.. rst-class:: classref-property

:ref:`float<class_float>` **margin** = ``0.04`` :ref:`🔗<class_CollisionPolygon3D_property_margin>`

.. rst-class:: classref-property-setget

- |void| **set_margin**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_margin**\ (\ )

Collision margin cho :ref:`Shape3D<class_Shape3D>` được tạo ra. Xem :ref:`Shape3D.margin<class_Shape3D_property_margin>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_CollisionPolygon3D_property_polygon:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **polygon** = ``PackedVector2Array()`` :ref:`🔗<class_CollisionPolygon3D_property_polygon>`

.. rst-class:: classref-property-setget

- |void| **set_polygon**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_polygon**\ (\ )

Mảng các đỉnh xác định đa giác 2D trong mặt phẳng XY cục bộ.

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
