:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsDirectSpaceState2D.xml.

.. _class_PhysicsDirectSpaceState2D:

PhysicsDirectSpaceState2D
=========================

**Kế thừa:** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`PhysicsDirectSpaceState2DExtension<class_PhysicsDirectSpaceState2DExtension>`

Cung cấp quyền truy cập trực tiếp vào một physics space trong :ref:`PhysicsServer2D<class_PhysicsServer2D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp quyền truy cập trực tiếp vào một physics space trong :ref:`PhysicsServer2D<class_PhysicsServer2D>`. Lớp này chủ yếu được dùng để thực hiện các truy vấn đối với những object và area nằm trong một space nhất định.

\ **Lưu ý:** Không nên khởi tạo trực tiếp class này. Hãy sử dụng :ref:`World2D.direct_space_state<class_World2D_property_direct_space_state>` để lấy trạng thái physics space 2D của world.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Giới thiệu về physics <../tutorials/physics/physics_introduction>`

- :doc:`Ray-casting <../tutorials/physics/ray-casting>`

.. rst-class:: classref-reftable-group

Các method
----------

.. table::
   :widths: auto

   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>`              | :ref:`cast_motion<class_PhysicsDirectSpaceState2D_method_cast_motion>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`\ )                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector2<class_Vector2>`\]       | :ref:`collide_shape<class_PhysicsDirectSpaceState2D_method_collide_shape>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, max_results\: :ref:`int<class_int>` = 32\ )     |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`get_rest_info<class_PhysicsDirectSpaceState2D_method_get_rest_info>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`\ )                                               |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`intersect_point<class_PhysicsDirectSpaceState2D_method_intersect_point>`\ (\ parameters\: :ref:`PhysicsPointQueryParameters2D<class_PhysicsPointQueryParameters2D>`, max_results\: :ref:`int<class_int>` = 32\ ) |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`intersect_ray<class_PhysicsDirectSpaceState2D_method_intersect_ray>`\ (\ parameters\: :ref:`PhysicsRayQueryParameters2D<class_PhysicsRayQueryParameters2D>`\ )                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`intersect_shape<class_PhysicsDirectSpaceState2D_method_intersect_shape>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, max_results\: :ref:`int<class_int>` = 32\ ) |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả method
------------

.. _class_PhysicsDirectSpaceState2D_method_cast_motion:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **cast_motion**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`\ ) :ref:`🔗<class_PhysicsDirectSpaceState2D_method_cast_motion>`

Kiểm tra khoảng cách mà một :ref:`Shape2D<class_Shape2D>` có thể di chuyển mà không va chạm. Tất cả parameters cho truy vấn, bao gồm shape và motion, được cung cấp thông qua một object :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`.

Trả về một array chứa tỷ lệ an toàn và không an toàn (trong khoảng từ 0 đến 1) của motion. Tỷ lệ an toàn là phần motion tối đa có thể thực hiện mà không xảy ra va chạm. Tỷ lệ không an toàn là phần khoảng cách tối thiểu phải di chuyển để xảy ra va chạm. Nếu không phát hiện va chạm, kết quả trả về sẽ là ``[1.0, 1.0]``.

\ **Lưu ý:** Mọi :ref:`Shape2D<class_Shape2D>`\ s mà shape đang va chạm, chẳng hạn như đang ở bên trong, sẽ bị bỏ qua. Hãy sử dụng :ref:`collide_shape()<class_PhysicsDirectSpaceState2D_method_collide_shape>` để xác định các :ref:`Shape2D<class_Shape2D>`\ s mà shape đang va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState2D_method_collide_shape:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector2<class_Vector2>`\] **collide_shape**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, max_results\: :ref:`int<class_int>` = 32\ ) :ref:`🔗<class_PhysicsDirectSpaceState2D_method_collide_shape>`

Kiểm tra các giao điểm của một shape, được cung cấp thông qua object :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, với space. Array kết quả chứa danh sách các điểm tại đó shape giao với một shape khác. Tương tự :ref:`intersect_shape()<class_PhysicsDirectSpaceState2D_method_intersect_shape>`, có thể giới hạn số lượng kết quả trả về để tiết kiệm thời gian xử lý.

Các điểm được trả về là danh sách các cặp điểm tiếp xúc. Với mỗi cặp, điểm thứ nhất nằm trong shape được truyền vào object :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, còn điểm thứ hai nằm trong shape bị va chạm từ physics space.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState2D_method_get_rest_info:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_rest_info**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`\ ) :ref:`🔗<class_PhysicsDirectSpaceState2D_method_get_rest_info>`

Kiểm tra các giao điểm của một shape, được cung cấp thông qua object :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, với space. Nếu nó va chạm với nhiều hơn một shape, shape ở gần nhất sẽ được chọn. Object được trả về là một dictionary chứa các field sau:

\ ``collider_id``: ID của object đang va chạm.

\ ``linear_velocity``: :ref:`Vector2<class_Vector2>` vận tốc của object đang va chạm. Nếu object là một :ref:`Area2D<class_Area2D>`, kết quả là ``(0, 0)``.

\ ``normal``: Normal va chạm của shape được truy vấn tại điểm giao nhau, hướng ra xa object giao nhau.

\ ``point``: Điểm giao nhau.

\ ``rid``: :ref:`RID<class_RID>` của object giao nhau.

\ ``shape``: Chỉ mục shape của shape đang va chạm.

Nếu shape không giao với bất kỳ thứ gì, một dictionary rỗng sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState2D_method_intersect_point:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **intersect_point**\ (\ parameters\: :ref:`PhysicsPointQueryParameters2D<class_PhysicsPointQueryParameters2D>`, max_results\: :ref:`int<class_int>` = 32\ ) :ref:`🔗<class_PhysicsDirectSpaceState2D_method_intersect_point>`

Kiểm tra xem một điểm có nằm bên trong bất kỳ solid shape nào hay không. Vị trí và các parameters khác được định nghĩa thông qua :ref:`PhysicsPointQueryParameters2D<class_PhysicsPointQueryParameters2D>`. Các shape mà điểm nằm bên trong được trả về trong một array chứa các dictionary với những field sau:

\ ``collider``: Object đang va chạm.

\ ``collider_id``: ID của object đang va chạm.

\ ``rid``: :ref:`RID<class_RID>` của object giao nhau.

\ ``shape``: Chỉ mục shape của shape đang va chạm.

Có thể giới hạn số lượng giao điểm bằng parameter ``max_results`` để giảm thời gian xử lý.

\ **Lưu ý:** :ref:`ConcavePolygonShape2D<class_ConcavePolygonShape2D>`\ s và :ref:`CollisionPolygon2D<class_CollisionPolygon2D>`\ s trong ``Segments`` build mode không phải là solid shape. Vì vậy, chúng sẽ không được phát hiện.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState2D_method_intersect_ray:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **intersect_ray**\ (\ parameters\: :ref:`PhysicsRayQueryParameters2D<class_PhysicsRayQueryParameters2D>`\ ) :ref:`🔗<class_PhysicsDirectSpaceState2D_method_intersect_ray>`

Kiểm tra giao của một ray trong một space nhất định. Vị trí của ray và các parameters khác được định nghĩa thông qua :ref:`PhysicsRayQueryParameters2D<class_PhysicsRayQueryParameters2D>`. Object được trả về là một dictionary với các field sau:

\ ``collider``: Object đang va chạm.

\ ``collider_id``: ID của object đang va chạm.

\ ``normal``: Normal bề mặt của object tại điểm giao nhau, hoặc ``Vector2(0, 0)`` nếu ray bắt đầu bên trong shape và :ref:`PhysicsRayQueryParameters2D.hit_from_inside<class_PhysicsRayQueryParameters2D_property_hit_from_inside>` là ``true``.

\ ``position``: Điểm giao nhau.

\ ``rid``: :ref:`RID<class_RID>` của object giao nhau.

\ ``shape``: Chỉ mục shape của shape đang va chạm.

Nếu ray không giao với bất kỳ thứ gì, một dictionary rỗng sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState2D_method_intersect_shape:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **intersect_shape**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, max_results\: :ref:`int<class_int>` = 32\ ) :ref:`🔗<class_PhysicsDirectSpaceState2D_method_intersect_shape>`

Kiểm tra các giao điểm của một shape, được cung cấp thông qua object :ref:`PhysicsShapeQueryParameters2D<class_PhysicsShapeQueryParameters2D>`, với space. Các shape được giao sẽ được trả về trong một array chứa các dictionary với những field sau:

\ ``collider``: Object đang va chạm.

\ ``collider_id``: ID của object đang va chạm.

\ ``rid``: :ref:`RID<class_RID>` của object giao nhau.

\ ``shape``: Chỉ mục shape của shape đang va chạm.

Có thể giới hạn số lượng giao điểm bằng parameter ``max_results`` để giảm thời gian xử lý.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
