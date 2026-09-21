:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ConvexPolygonShape3D.xml.

.. _class_ConvexPolygonShape3D:

ConvexPolygonShape3D
====================

**Kế thừa:** :ref:`Shape3D<class_Shape3D>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một hình đa diện lồi 3D dùng cho va chạm vật lý.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một hình đa diện lồi 3D, được thiết kế để sử dụng trong vật lý. Thường được dùng để cung cấp hình dạng cho một :ref:`CollisionShape3D<class_CollisionShape3D>`.

\ **ConvexPolygonShape3D** là hình *đặc*, nghĩa là nó phát hiện các va chạm từ những đối tượng nằm hoàn toàn bên trong nó, không giống :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>` vốn rỗng. Điều này khiến nó phù hợp hơn cho cả việc phát hiện va chạm và mô phỏng vật lý.

\ **Phân rã lồi:** Một hình đa diện lõm có thể được tách thành nhiều hình đa diện lồi. Điều này cho phép các physics body động có va chạm lõm phức tạp (đánh đổi bằng hiệu năng) và có thể thực hiện bằng cách sử dụng nhiều node **ConvexPolygonShape3D**. Để tạo phân rã lồi từ một mesh, hãy chọn node :ref:`MeshInstance3D<class_MeshInstance3D>`, đi đến menu **Mesh** xuất hiện phía trên viewport, rồi chọn **Create Multiple Convex Collision Siblings**. Ngoài ra, có thể gọi :ref:`MeshInstance3D.create_multiple_convex_collisions()<class_MeshInstance3D_method_create_multiple_convex_collisions>` trong một script để thực hiện việc phân rã này lúc runtime.

\ **Hiệu năng:** **ConvexPolygonShape3D** kiểm tra va chạm nhanh hơn so với :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>`, nhưng chậm hơn các collision shape nguyên thủy như :ref:`SphereShape3D<class_SphereShape3D>` và :ref:`BoxShape3D<class_BoxShape3D>`. Nhìn chung, chỉ nên sử dụng nó cho các đối tượng kích thước trung bình không thể biểu diễn chính xác va chạm bằng các shape nguyên thủy.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3D Physics Tests Demo <https://godotengine.org/asset-library/asset/2747>`__

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------+--------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`points<class_ConvexPolygonShape3D_property_points>` | ``PackedVector3Array()`` |
   +-----------------------------------------------------+-----------------------------------------------------------+--------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ConvexPolygonShape3D_property_points:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **points** = ``PackedVector3Array()`` :ref:`🔗<class_ConvexPolygonShape3D_property_points>`

.. rst-class:: classref-property-setget

- |void| **set_points**\ (\ value\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) - :ref:`PackedVector3Array<class_PackedVector3Array>` **get_points**\ (\ )

Danh sách các điểm 3D tạo thành hình đa giác lồi.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với nó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
