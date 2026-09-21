:github_url: hide

.. ĐỪNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ConcavePolygonShape2D.xml.

.. _class_ConcavePolygonShape2D:

ConcavePolygonShape2D
=====================

**Kế thừa:** :ref:`Shape2D<class_Shape2D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một shape polyline 2D được dùng cho việc collision trong physics.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một shape polyline 2D, предназнач cho việc sử dụng trong physics. Được dùng nội bộ trong :ref:`CollisionPolygon2D<class_CollisionPolygon2D>` khi nó ở chế độ :ref:`CollisionPolygon2D.BUILD_SEGMENTS<class_CollisionPolygon2D_constant_BUILD_SEGMENTS>`.

Là một tập hợp các đoạn thẳng được nối với nhau, **ConcavePolygonShape2D** là shape 2D đơn lẻ có khả năng cấu hình tự do nhất. Nó có thể được dùng để tạo các polygon với bất kỳ hình dạng nào, hoặc thậm chí các shape không bao kín một vùng. Tuy nhiên, **ConcavePolygonShape2D** là *rỗng* ngay cả khi các đoạn thẳng được nối với nhau có bao kín một vùng, nên thường không phù hợp cho physics hoặc detection.

\ **Note:** When used for collision, **ConcavePolygonShape2D** is intended to work with static :ref:`CollisionShape2D<class_CollisionShape2D>` nodes like :ref:`StaticBody2D<class_StaticBody2D>` and will likely not behave well for :ref:`CharacterBody2D<class_CharacterBody2D>`\ s or :ref:`RigidBody2D<class_RigidBody2D>`\ s in a mode other than Static.

\ **Cảnh báo:** Các physics body nhỏ có khả năng xuyên qua shape này khi di chuyển nhanh. Điều này xảy ra vì trong một frame, physics body có thể ở "bên ngoài" shape, còn trong frame tiếp theo nó có thể ở "bên trong" shape. **ConcavePolygonShape2D** là rỗng, nên sẽ không phát hiện collision.

\ **Performance:** Due to its complexity, **ConcavePolygonShape2D** is the slowest 2D collision shape to check collisions against. Its use should generally be limited to level geometry. If the polyline is closed, :ref:`CollisionPolygon2D<class_CollisionPolygon2D>`'s :ref:`CollisionPolygon2D.BUILD_SOLIDS<class_CollisionPolygon2D_constant_BUILD_SOLIDS>` mode can be used, which decomposes the polygon into convex ones; see :ref:`ConvexPolygonShape2D<class_ConvexPolygonShape2D>`'s documentation for instructions.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+----------------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`segments<class_ConcavePolygonShape2D_property_segments>` | ``PackedVector2Array()`` |
   +-----------------------------------------------------+----------------------------------------------------------------+--------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConcavePolygonShape2D_property_segments:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **segments** = ``PackedVector2Array()`` :ref:`🔗<class_ConcavePolygonShape2D_property_segments>`

.. rst-class:: classref-property-setget

- |void| **set_segments**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_segments**\ (\ )

Mảng các điểm tạo thành các đoạn thẳng của **ConcavePolygonShape2D**. Mảng này (có độ dài chia hết cho hai) được chia tự nhiên thành các cặp (mỗi cặp tương ứng với một đoạn); mỗi cặp gồm điểm bắt đầu và điểm kết thúc của một đoạn.

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
