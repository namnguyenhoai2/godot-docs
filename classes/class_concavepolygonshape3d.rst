:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ConcavePolygonShape3D.xml.

.. _class_ConcavePolygonShape3D:

ConcavePolygonShape3D
=====================

**Kế thừa:** :ref:`Shape3D<class_Shape3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một trimesh shape 3D được dùng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một trimesh shape 3D, được thiết kế để sử dụng trong vật lý. Thường được dùng để cung cấp một shape cho :ref:`CollisionShape3D<class_CollisionShape3D>`.

Là một tập hợp các tam giác liên kết với nhau, **ConcavePolygonShape3D** là shape 3D đơn lẻ có khả năng cấu hình tự do nhất. Nó có thể được dùng để tạo các khối đa diện thuộc bất kỳ dạng nào, hoặc thậm chí các shape không bao kín một thể tích. Tuy nhiên, **ConcavePolygonShape3D** vẫn *rỗng* ngay cả khi các tam giác liên kết với nhau bao kín một thể tích, điều này thường khiến nó không phù hợp cho vật lý hoặc phát hiện.

\ **Note:** When used for collision, **ConcavePolygonShape3D** is intended to work with static :ref:`CollisionShape3D<class_CollisionShape3D>` nodes like :ref:`StaticBody3D<class_StaticBody3D>` and will likely not behave well for :ref:`CharacterBody3D<class_CharacterBody3D>`\ s or :ref:`RigidBody3D<class_RigidBody3D>`\ s in a mode other than Static.

\ **Cảnh báo:** Các physics body nhỏ có khả năng đi xuyên qua shape này khi di chuyển nhanh. Điều này xảy ra vì trong một frame, physics body có thể ở "bên ngoài" shape, còn trong frame tiếp theo lại có thể ở "bên trong" shape. **ConcavePolygonShape3D** là shape rỗng, vì vậy nó sẽ không phát hiện va chạm.

\ **Performance:** Due to its complexity, **ConcavePolygonShape3D** is the slowest 3D collision shape to check collisions against. Its use should generally be limited to level geometry. For convex geometry, :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>` should be used. For dynamic physics bodies that need concave collision, several :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>`\ s can be used to represent its collision by using convex decomposition; see :ref:`ConvexPolygonShape3D<class_ConvexPolygonShape3D>`'s documentation for instructions.

.. rst-class:: classref-introduction-group

Tutorial
--------

- `3D Physics Tests Demo <https://godotengine.org/asset-library/asset/2747>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------+------------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`backface_collision<class_ConcavePolygonShape3D_property_backface_collision>` | ``false`` |
   +-------------------------+------------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_faces<class_ConcavePolygonShape3D_method_get_faces>`\ (\ ) |const|                                                      |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_faces<class_ConcavePolygonShape3D_method_set_faces>`\ (\ faces\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConcavePolygonShape3D_property_backface_collision:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **backface_collision** = ``false`` :ref:`🔗<class_ConcavePolygonShape3D_property_backface_collision>`

.. rst-class:: classref-property-setget

- |void| **set_backface_collision_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_backface_collision_enabled**\ (\ )

Nếu được đặt thành ``true``, va chạm sẽ xảy ra ở cả hai phía của các mặt concave shape. Nếu không, va chạm chỉ xảy ra dọc theo các pháp tuyến của mặt.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ConcavePolygonShape3D_method_get_faces:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_faces**\ (\ ) |const| :ref:`🔗<class_ConcavePolygonShape3D_method_get_faces>`

Trả về các mặt của trimesh shape dưới dạng một mảng các đỉnh. Mảng này (có độ dài chia hết cho ba) được chia tự nhiên thành các bộ ba; mỗi bộ ba đỉnh xác định một tam giác.

.. rst-class:: classref-item-separator

----

.. _class_ConcavePolygonShape3D_method_set_faces:

.. rst-class:: classref-method

|void| **set_faces**\ (\ faces\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) :ref:`🔗<class_ConcavePolygonShape3D_method_set_faces>`

Thiết lập các mặt của trimesh shape từ một mảng các đỉnh. Mảng ``faces`` phải được tạo thành từ các bộ ba sao cho mỗi bộ ba đỉnh xác định một tam giác.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
