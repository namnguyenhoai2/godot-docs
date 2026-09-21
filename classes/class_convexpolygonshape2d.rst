:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ConvexPolygonShape2D.xml.

.. _class_ConvexPolygonShape2D:

ConvexPolygonShape2D
====================

**Kế thừa:** :ref:`Shape2D<class_Shape2D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một hình đa giác lồi 2D được dùng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hình đa giác lồi 2D, được thiết kế để sử dụng trong vật lý. Được sử dụng nội bộ trong :ref:`CollisionPolygon2D<class_CollisionPolygon2D>` khi nó ở chế độ :ref:`CollisionPolygon2D.BUILD_SOLIDS<class_CollisionPolygon2D_constant_BUILD_SOLIDS>`.

\ **ConvexPolygonShape2D** là hình *đặc*, nghĩa là nó phát hiện các va chạm từ những đối tượng nằm hoàn toàn bên trong nó, không giống :ref:`ConcavePolygonShape2D<class_ConcavePolygonShape2D>` vốn rỗng. Điều này khiến nó phù hợp hơn cho cả việc phát hiện và xử lý vật lý.

\ **Phân rã lồi:** Một đa giác lõm có thể được chia thành nhiều đa giác lồi. Điều này cho phép các physics body động có va chạm lõm phức tạp (đổi lại hiệu năng) và có thể thực hiện bằng cách sử dụng nhiều node **ConvexPolygonShape2D** hoặc sử dụng node :ref:`CollisionPolygon2D<class_CollisionPolygon2D>` ở chế độ :ref:`CollisionPolygon2D.BUILD_SOLIDS<class_CollisionPolygon2D_constant_BUILD_SOLIDS>`. Để tạo một đa giác va chạm từ sprite, hãy chọn node :ref:`Sprite2D<class_Sprite2D>`, đi đến menu **Sprite2D** xuất hiện phía trên viewport và chọn **Create Polygon2D Sibling**.

\ **Hiệu năng:** **ConvexPolygonShape2D** kiểm tra va chạm nhanh hơn so với :ref:`ConcavePolygonShape2D<class_ConcavePolygonShape2D>`, nhưng chậm hơn các hình va chạm nguyên thủy như :ref:`CircleShape2D<class_CircleShape2D>` và :ref:`RectangleShape2D<class_RectangleShape2D>`. Nhìn chung, chỉ nên sử dụng nó cho các đối tượng kích thước trung bình mà hình dạng va chạm không thể được biểu diễn chính xác bằng các hình nguyên thủy.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------+--------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>` | :ref:`points<class_ConvexPolygonShape2D_property_points>` | ``PackedVector2Array()`` |
   +-----------------------------------------------------+-----------------------------------------------------------+--------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void| | :ref:`set_point_cloud<class_ConvexPolygonShape2D_method_set_point_cloud>`\ (\ point_cloud\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) |
   +--------+----------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConvexPolygonShape2D_property_points:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **points** = ``PackedVector2Array()`` :ref:`🔗<class_ConvexPolygonShape2D_property_points>`

.. rst-class:: classref-property-setget

- |void| **set_points**\ (\ value\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) - :ref:`PackedVector2Array<class_PackedVector2Array>` **get_points**\ (\ )

Danh sách các đỉnh của đa giác tạo thành một bao lồi. Có thể được sắp xếp theo chiều kim đồng hồ hoặc ngược chiều kim đồng hồ.

\ **Cảnh báo:** Chỉ đặt thuộc tính này thành danh sách các điểm thực sự tạo thành một bao lồi. Sử dụng :ref:`set_point_cloud()<class_ConvexPolygonShape2D_method_set_point_cloud>` để tạo bao lồi của một tập hợp điểm bất kỳ.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi trên đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ConvexPolygonShape2D_method_set_point_cloud:

.. rst-class:: classref-method

|void| **set_point_cloud**\ (\ point_cloud\: :ref:`PackedVector2Array<class_PackedVector2Array>`\ ) :ref:`🔗<class_ConvexPolygonShape2D_method_set_point_cloud>`

Dựa trên tập hợp các điểm được cung cấp, phương thức này gán thuộc tính :ref:`points<class_ConvexPolygonShape2D_property_points>` bằng thuật toán bao lồi, loại bỏ tất cả các điểm không cần thiết. Xem :ref:`Geometry2D.convex_hull()<class_Geometry2D_method_convex_hull>` để biết chi tiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
