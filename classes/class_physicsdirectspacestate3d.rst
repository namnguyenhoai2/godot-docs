:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PhysicsDirectSpaceState3D.xml.

.. _class_PhysicsDirectSpaceState3D:

PhysicsDirectSpaceState3D
=========================

**Kế thừa:** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`PhysicsDirectSpaceState3DExtension<class_PhysicsDirectSpaceState3DExtension>`

Cung cấp quyền truy cập trực tiếp vào một physics space trong :ref:`PhysicsServer3D<class_PhysicsServer3D>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp quyền truy cập trực tiếp vào một physics space trong :ref:`PhysicsServer3D<class_PhysicsServer3D>`. Lớp này chủ yếu được dùng để thực hiện truy vấn đối với các đối tượng và area nằm trong một space nhất định.

\ **Lưu ý:** Không nên khởi tạo trực tiếp class này. Hãy sử dụng :ref:`World3D.direct_space_state<class_World3D_property_direct_space_state>` để lấy trạng thái physics space 3D của world.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Giới thiệu về physics <../tutorials/physics/physics_introduction>`

- :doc:`Ray-casting <../tutorials/physics/ray-casting>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>`              | :ref:`cast_motion<class_PhysicsDirectSpaceState3D_method_cast_motion>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`\ )                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Vector3<class_Vector3>`\]       | :ref:`collide_shape<class_PhysicsDirectSpaceState3D_method_collide_shape>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, max_results\: :ref:`int<class_int>` = 32\ )     |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`get_rest_info<class_PhysicsDirectSpaceState3D_method_get_rest_info>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`\ )                                               |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`intersect_point<class_PhysicsDirectSpaceState3D_method_intersect_point>`\ (\ parameters\: :ref:`PhysicsPointQueryParameters3D<class_PhysicsPointQueryParameters3D>`, max_results\: :ref:`int<class_int>` = 32\ ) |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`                              | :ref:`intersect_ray<class_PhysicsDirectSpaceState3D_method_intersect_ray>`\ (\ parameters\: :ref:`PhysicsRayQueryParameters3D<class_PhysicsRayQueryParameters3D>`\ )                                                   |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`intersect_shape<class_PhysicsDirectSpaceState3D_method_intersect_shape>`\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, max_results\: :ref:`int<class_int>` = 32\ ) |
   +------------------------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_PhysicsDirectSpaceState3D_method_cast_motion:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **cast_motion**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`\ ) :ref:`🔗<class_PhysicsDirectSpaceState3D_method_cast_motion>`

Kiểm tra xem một :ref:`Shape3D<class_Shape3D>` có thể di chuyển bao xa mà không va chạm. Tất cả các tham số cho truy vấn, bao gồm shape và chuyển động, được cung cấp thông qua một đối tượng :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`.

Trả về một mảng chứa tỷ lệ an toàn và không an toàn (từ 0 đến 1) của chuyển động. Tỷ lệ an toàn là phần tối đa của chuyển động có thể thực hiện mà không xảy ra va chạm. Tỷ lệ không an toàn là phần tối thiểu của khoảng cách phải di chuyển để xảy ra va chạm. Nếu không phát hiện va chạm, kết quả trả về sẽ là ``[1.0, 1.0]``.

\ **Lưu ý:** Mọi :ref:`Shape3D<class_Shape3D>`\ s mà shape đã va chạm, chẳng hạn như đang ở bên trong, sẽ bị bỏ qua. Hãy sử dụng :ref:`collide_shape()<class_PhysicsDirectSpaceState3D_method_collide_shape>` để xác định các :ref:`Shape3D<class_Shape3D>`\ s mà shape đã va chạm.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState3D_method_collide_shape:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Vector3<class_Vector3>`\] **collide_shape**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, max_results\: :ref:`int<class_int>` = 32\ ) :ref:`🔗<class_PhysicsDirectSpaceState3D_method_collide_shape>`

Kiểm tra các giao điểm của một shape, được cung cấp thông qua một đối tượng :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, với space. Mảng kết quả chứa danh sách các điểm nơi shape giao với một shape khác. Tương tự như :ref:`intersect_shape()<class_PhysicsDirectSpaceState3D_method_intersect_shape>`, số lượng kết quả trả về có thể được giới hạn để tiết kiệm thời gian xử lý.

Các điểm trả về là một danh sách các cặp điểm tiếp xúc. Với mỗi cặp, điểm thứ nhất nằm trong shape được truyền vào đối tượng :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, còn điểm thứ hai nằm trong shape bị va chạm trong physics space.

\ **Lưu ý:** Phương thức này không tính đến thuộc tính ``motion`` của đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState3D_method_get_rest_info:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_rest_info**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`\ ) :ref:`🔗<class_PhysicsDirectSpaceState3D_method_get_rest_info>`

Kiểm tra các giao điểm của một shape, được cung cấp thông qua một đối tượng :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, với space. Nếu nó va chạm với nhiều shape, shape gần nhất sẽ được chọn. Đối tượng trả về là một dictionary chứa các trường sau:

\ ``collider_id``: ID của đối tượng bị va chạm.

\ ``linear_velocity``: :ref:`Vector3<class_Vector3>` vận tốc của đối tượng bị va chạm. Nếu đối tượng là một :ref:`Area3D<class_Area3D>`, kết quả sẽ là ``(0, 0, 0)``.

\ ``normal``: Pháp tuyến va chạm của shape truy vấn tại điểm giao, hướng ra xa đối tượng giao nhau.

\ ``point``: Điểm giao.

\ ``rid``: :ref:`RID<class_RID>` của đối tượng giao nhau.

\ ``shape``: Chỉ số shape của shape bị va chạm.

Nếu shape không giao với bất kỳ thứ gì, một dictionary rỗng sẽ được trả về.

\ **Lưu ý:** Phương thức này không tính đến thuộc tính ``motion`` của đối tượng.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState3D_method_intersect_point:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **intersect_point**\ (\ parameters\: :ref:`PhysicsPointQueryParameters3D<class_PhysicsPointQueryParameters3D>`, max_results\: :ref:`int<class_int>` = 32\ ) :ref:`🔗<class_PhysicsDirectSpaceState3D_method_intersect_point>`

Kiểm tra xem một điểm có nằm bên trong shape đặc nào hay không. Vị trí và các tham số khác được định nghĩa thông qua :ref:`PhysicsPointQueryParameters3D<class_PhysicsPointQueryParameters3D>`. Các shape mà điểm nằm bên trong được trả về trong một mảng chứa các dictionary với những trường sau:

\ ``collider``: Đối tượng bị va chạm.

\ ``collider_id``: ID của đối tượng bị va chạm.

\ ``rid``: :ref:`RID<class_RID>` của đối tượng giao nhau.

\ ``shape``: Chỉ số shape của shape bị va chạm.

Có thể giới hạn số lượng giao điểm bằng tham số ``max_results`` để giảm thời gian xử lý.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState3D_method_intersect_ray:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **intersect_ray**\ (\ parameters\: :ref:`PhysicsRayQueryParameters3D<class_PhysicsRayQueryParameters3D>`\ ) :ref:`🔗<class_PhysicsDirectSpaceState3D_method_intersect_ray>`

Thực hiện giao cắt một ray trong space nhất định. Vị trí của ray và các tham số khác được định nghĩa thông qua :ref:`PhysicsRayQueryParameters3D<class_PhysicsRayQueryParameters3D>`. Đối tượng trả về là một dictionary có các trường sau:

\ ``collider``: Đối tượng bị va chạm.

\ ``collider_id``: ID của đối tượng bị va chạm.

\ ``normal``: Pháp tuyến bề mặt của đối tượng tại điểm giao, hoặc ``Vector3(0, 0, 0)`` nếu ray bắt đầu bên trong shape và :ref:`PhysicsRayQueryParameters3D.hit_from_inside<class_PhysicsRayQueryParameters3D_property_hit_from_inside>` là ``true``.

\ ``position``: Điểm giao.

\ ``face_index``: Chỉ số face tại điểm giao.

\ **Lưu ý:** Chỉ trả về một số hợp lệ nếu shape được giao cắt là một :ref:`ConcavePolygonShape3D<class_ConcavePolygonShape3D>`. Nếu không, ``-1`` sẽ được trả về.

\ ``rid``: :ref:`RID<class_RID>` của đối tượng giao nhau.

\ ``shape``: Chỉ số shape của shape bị va chạm.

Nếu ray không giao với bất kỳ thứ gì, một dictionary rỗng sẽ được trả về.

.. rst-class:: classref-item-separator

----

.. _class_PhysicsDirectSpaceState3D_method_intersect_shape:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **intersect_shape**\ (\ parameters\: :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, max_results\: :ref:`int<class_int>` = 32\ ) :ref:`🔗<class_PhysicsDirectSpaceState3D_method_intersect_shape>`

Kiểm tra các giao điểm của một shape, được cung cấp thông qua một đối tượng :ref:`PhysicsShapeQueryParameters3D<class_PhysicsShapeQueryParameters3D>`, với space. Các shape được giao cắt sẽ được trả về trong một mảng chứa các dictionary với những trường sau:

\ ``collider``: Đối tượng bị va chạm.

\ ``collider_id``: ID của đối tượng bị va chạm.

\ ``rid``: :ref:`RID<class_RID>` của đối tượng giao nhau.

\ ``shape``: Chỉ số shape của shape bị va chạm.

Có thể giới hạn số lượng giao điểm bằng tham số ``max_results`` để giảm thời gian xử lý.

\ **Lưu ý:** Phương thức này không tính đến thuộc tính ``motion`` của đối tượng.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
