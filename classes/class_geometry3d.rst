:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Geometry3D.xml.

.. _class_Geometry3D:

Geometry3D
==========

**Kế thừa:** :ref:`Object<class_Object>`

Cung cấp các phương thức cho một số phép toán hình học 3D phổ biến.

.. rst-class:: classref-introduction-group

Mô tả
-----

Cung cấp một tập hợp các hàm hỗ trợ để tạo hình dạng hình học, tính toán giao điểm giữa các hình dạng và xử lý nhiều phép toán hình học khác trong không gian 3D.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] | :ref:`build_box_planes<class_Geometry3D_method_build_box_planes>`\ (\ extents\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                                                                 |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] | :ref:`build_capsule_planes<class_Geometry3D_method_build_capsule_planes>`\ (\ radius\: :ref:`float<class_float>`, height\: :ref:`float<class_float>`, sides\: :ref:`int<class_int>`, lats\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>` = 2\ )                  |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] | :ref:`build_cylinder_planes<class_Geometry3D_method_build_cylinder_planes>`\ (\ radius\: :ref:`float<class_float>`, height\: :ref:`float<class_float>`, sides\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>` = 2\ )                                              |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`    | :ref:`clip_polygon<class_Geometry3D_method_clip_polygon>`\ (\ points\: :ref:`PackedVector3Array<class_PackedVector3Array>`, plane\: :ref:`Plane<class_Plane>`\ )                                                                                                                 |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`    | :ref:`compute_convex_mesh_points<class_Geometry3D_method_compute_convex_mesh_points>`\ (\ planes\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ )                                                                                                                     |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`get_closest_point_to_segment<class_Geometry3D_method_get_closest_point_to_segment>`\ (\ point\: :ref:`Vector3<class_Vector3>`, s1\: :ref:`Vector3<class_Vector3>`, s2\: :ref:`Vector3<class_Vector3>`\ )                                                                   |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`get_closest_point_to_segment_uncapped<class_Geometry3D_method_get_closest_point_to_segment_uncapped>`\ (\ point\: :ref:`Vector3<class_Vector3>`, s1\: :ref:`Vector3<class_Vector3>`, s2\: :ref:`Vector3<class_Vector3>`\ )                                                 |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`    | :ref:`get_closest_points_between_segments<class_Geometry3D_method_get_closest_points_between_segments>`\ (\ p1\: :ref:`Vector3<class_Vector3>`, p2\: :ref:`Vector3<class_Vector3>`, q1\: :ref:`Vector3<class_Vector3>`, q2\: :ref:`Vector3<class_Vector3>`\ )                    |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                          | :ref:`get_triangle_barycentric_coords<class_Geometry3D_method_get_triangle_barycentric_coords>`\ (\ point\: :ref:`Vector3<class_Vector3>`, a\: :ref:`Vector3<class_Vector3>`, b\: :ref:`Vector3<class_Vector3>`, c\: :ref:`Vector3<class_Vector3>`\ )                            |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                          | :ref:`ray_intersects_triangle<class_Geometry3D_method_ray_intersects_triangle>`\ (\ from\: :ref:`Vector3<class_Vector3>`, dir\: :ref:`Vector3<class_Vector3>`, a\: :ref:`Vector3<class_Vector3>`, b\: :ref:`Vector3<class_Vector3>`, c\: :ref:`Vector3<class_Vector3>`\ )        |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`    | :ref:`segment_intersects_convex<class_Geometry3D_method_segment_intersects_convex>`\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, planes\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ )                                             |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`    | :ref:`segment_intersects_cylinder<class_Geometry3D_method_segment_intersects_cylinder>`\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, height\: :ref:`float<class_float>`, radius\: :ref:`float<class_float>`\ )                                  |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`    | :ref:`segment_intersects_sphere<class_Geometry3D_method_segment_intersects_sphere>`\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, sphere_position\: :ref:`Vector3<class_Vector3>`, sphere_radius\: :ref:`float<class_float>`\ )                  |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                          | :ref:`segment_intersects_triangle<class_Geometry3D_method_segment_intersects_triangle>`\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, a\: :ref:`Vector3<class_Vector3>`, b\: :ref:`Vector3<class_Vector3>`, c\: :ref:`Vector3<class_Vector3>`\ ) |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedInt32Array<class_PackedInt32Array>`        | :ref:`tetrahedralize_delaunay<class_Geometry3D_method_tetrahedralize_delaunay>`\ (\ points\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ )                                                                                                                              |
   +--------------------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Geometry3D_method_build_box_planes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] **build_box_planes**\ (\ extents\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_build_box_planes>`

Trả về một mảng gồm 6 :ref:`Plane<class_Plane>`\ s mô tả các mặt của một hình hộp có tâm nằm tại gốc tọa độ. Kích thước hình hộp được xác định bởi ``extents``, đại diện cho một đỉnh (dương) của hình hộp (tức là một nửa kích thước thực tế của nó).

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_build_capsule_planes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] **build_capsule_planes**\ (\ radius\: :ref:`float<class_float>`, height\: :ref:`float<class_float>`, sides\: :ref:`int<class_int>`, lats\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>` = 2\ ) :ref:`🔗<class_Geometry3D_method_build_capsule_planes>`

Trả về một mảng gồm :ref:`Plane<class_Plane>`\ s bao quanh gần sát một capsule đa diện có tâm nằm tại gốc tọa độ, bán kính ``radius`` và chiều cao ``height``. Tham số ``sides`` xác định số lượng plane sẽ được tạo cho phần bên của capsule, trong khi ``lats`` cho biết số bước theo vĩ độ ở đáy và đỉnh capsule. Tham số ``axis`` mô tả trục mà capsule được định hướng theo (0 cho X, 1 cho Y, 2 cho Z).

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_build_cylinder_planes:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\] **build_cylinder_planes**\ (\ radius\: :ref:`float<class_float>`, height\: :ref:`float<class_float>`, sides\: :ref:`int<class_int>`, axis\: :ref:`Axis<enum_Vector3_Axis>` = 2\ ) :ref:`🔗<class_Geometry3D_method_build_cylinder_planes>`

Trả về một mảng gồm :ref:`Plane<class_Plane>`\ s bao quanh gần sát một hình trụ đa diện có tâm nằm tại gốc tọa độ, bán kính ``radius`` và chiều cao ``height``. Tham số ``sides`` xác định số lượng plane sẽ được tạo cho phần tròn của hình trụ. Tham số ``axis`` mô tả trục mà hình trụ được định hướng theo (0 cho X, 1 cho Y, 2 cho Z).

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_clip_polygon:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **clip_polygon**\ (\ points\: :ref:`PackedVector3Array<class_PackedVector3Array>`, plane\: :ref:`Plane<class_Plane>`\ ) :ref:`🔗<class_Geometry3D_method_clip_polygon>`

Cắt polygon được xác định bởi các điểm trong ``points`` theo ``plane`` và trả về các điểm của polygon sau khi cắt.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_compute_convex_mesh_points:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **compute_convex_mesh_points**\ (\ planes\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ ) :ref:`🔗<class_Geometry3D_method_compute_convex_mesh_points>`

Tính toán và trả về tất cả các điểm đỉnh của một hình dạng lồi được xác định bởi một mảng ``planes``.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_get_closest_point_to_segment:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_closest_point_to_segment**\ (\ point\: :ref:`Vector3<class_Vector3>`, s1\: :ref:`Vector3<class_Vector3>`, s2\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_get_closest_point_to_segment>`

Trả về điểm 3D trên đoạn 3D (``s1``, ``s2``) gần ``point`` nhất. Điểm được trả về luôn nằm bên trong đoạn đã chỉ định.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_get_closest_point_to_segment_uncapped:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_closest_point_to_segment_uncapped**\ (\ point\: :ref:`Vector3<class_Vector3>`, s1\: :ref:`Vector3<class_Vector3>`, s2\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_get_closest_point_to_segment_uncapped>`

Trả về điểm 3D trên đường thẳng 3D được xác định bởi (``s1``, ``s2``) gần ``point`` nhất. Điểm được trả về có thể nằm bên trong đoạn (``s1``, ``s2``) hoặc bên ngoài đoạn, tức là ở đâu đó trên đường thẳng kéo dài từ đoạn này.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_get_closest_points_between_segments:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_closest_points_between_segments**\ (\ p1\: :ref:`Vector3<class_Vector3>`, p2\: :ref:`Vector3<class_Vector3>`, q1\: :ref:`Vector3<class_Vector3>`, q2\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_get_closest_points_between_segments>`

Cho hai đoạn 3D (``p1``, ``p2``) và (``q1``, ``q2``), tìm hai điểm trên hai đoạn gần nhau nhất. Trả về một :ref:`PackedVector3Array<class_PackedVector3Array>` chứa điểm này trên (``p1``, ``p2``) cũng như điểm tương ứng trên (``q1``, ``q2``).

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_get_triangle_barycentric_coords:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_triangle_barycentric_coords**\ (\ point\: :ref:`Vector3<class_Vector3>`, a\: :ref:`Vector3<class_Vector3>`, b\: :ref:`Vector3<class_Vector3>`, c\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_get_triangle_barycentric_coords>`

Trả về một :ref:`Vector3<class_Vector3>` chứa các trọng số dựa trên mức độ gần của một vị trí 3D (``point``) với các đỉnh khác nhau của một tam giác (``a``, ``b`` và ``c``). Điều này hữu ích khi nội suy giữa dữ liệu của các đỉnh khác nhau trong một tam giác. Một trường hợp sử dụng là dùng cách này để xoay mượt trên một mesh thay vì chỉ dựa vào các pháp tuyến của mặt.

\ `Here is a more detailed explanation of barycentric coordinates. <https://en.wikipedia.org/wiki/Barycentric_coordinate_system>`__

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_ray_intersects_triangle:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **ray_intersects_triangle**\ (\ from\: :ref:`Vector3<class_Vector3>`, dir\: :ref:`Vector3<class_Vector3>`, a\: :ref:`Vector3<class_Vector3>`, b\: :ref:`Vector3<class_Vector3>`, c\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_ray_intersects_triangle>`

Kiểm tra xem tia 3D bắt đầu tại ``from`` và có hướng ``dir`` có giao với tam giác được xác định bởi ``a``, ``b`` và ``c`` hay không. Nếu có, trả về điểm giao dưới dạng :ref:`Vector3<class_Vector3>`. Nếu không xảy ra giao điểm, trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_segment_intersects_convex:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **segment_intersects_convex**\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, planes\: :ref:`Array<class_Array>`\[:ref:`Plane<class_Plane>`\]\ ) :ref:`🔗<class_Geometry3D_method_segment_intersects_convex>`

Cho một convex hull được xác định thông qua các :ref:`Plane<class_Plane>`\ s trong mảng ``planes``, kiểm tra xem đoạn (``from``, ``to``) có giao với hull đó hay không. Nếu tìm thấy giao điểm, trả về một :ref:`PackedVector3Array<class_PackedVector3Array>` chứa điểm giao và pháp tuyến của hull. Nếu không, trả về một mảng rỗng.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_segment_intersects_cylinder:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **segment_intersects_cylinder**\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, height\: :ref:`float<class_float>`, radius\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Geometry3D_method_segment_intersects_cylinder>`

Kiểm tra xem đoạn (``from``, ``to``) có giao với hình trụ có chiều cao ``height``, tâm nằm tại gốc tọa độ và bán kính ``radius`` hay không. Nếu không, trả về một :ref:`PackedVector3Array<class_PackedVector3Array>` rỗng. Nếu xảy ra giao điểm, mảng được trả về chứa điểm giao và pháp tuyến của hình trụ tại điểm giao.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_segment_intersects_sphere:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **segment_intersects_sphere**\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, sphere_position\: :ref:`Vector3<class_Vector3>`, sphere_radius\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Geometry3D_method_segment_intersects_sphere>`

Kiểm tra xem đoạn (``from``, ``to``) có giao với hình cầu nằm tại ``sphere_position`` và có bán kính ``sphere_radius`` hay không. Nếu không, trả về một :ref:`PackedVector3Array<class_PackedVector3Array>` rỗng. Nếu có, trả về một :ref:`PackedVector3Array<class_PackedVector3Array>` chứa điểm giao và pháp tuyến của hình cầu tại điểm giao.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_segment_intersects_triangle:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **segment_intersects_triangle**\ (\ from\: :ref:`Vector3<class_Vector3>`, to\: :ref:`Vector3<class_Vector3>`, a\: :ref:`Vector3<class_Vector3>`, b\: :ref:`Vector3<class_Vector3>`, c\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Geometry3D_method_segment_intersects_triangle>`

Kiểm tra xem đoạn (``from``, ``to``) có giao với tam giác ``a``, ``b``, ``c`` hay không. Nếu có, trả về điểm giao dưới dạng :ref:`Vector3<class_Vector3>`. Nếu không xảy ra giao điểm, trả về ``null``.

.. rst-class:: classref-item-separator

----

.. _class_Geometry3D_method_tetrahedralize_delaunay:

.. rst-class:: classref-method

:ref:`PackedInt32Array<class_PackedInt32Array>` **tetrahedralize_delaunay**\ (\ points\: :ref:`PackedVector3Array<class_PackedVector3Array>`\ ) :ref:`🔗<class_Geometry3D_method_tetrahedralize_delaunay>`

Tetrahedralize thể tích được xác định bởi một tập rời rạc các ``points`` trong không gian 3D, đảm bảo không có điểm nào nằm bên trong mặt cầu ngoại tiếp của bất kỳ tứ diện nào được tạo ra. Phương thức trả về một :ref:`PackedInt32Array<class_PackedInt32Array>`, trong đó mỗi tứ diện gồm bốn chỉ số điểm liên tiếp trỏ vào mảng ``points`` (tạo thành một mảng có ``n * 4`` phần tử, trong đó ``n`` là số tứ diện được tìm thấy). Nếu quá trình tetrahedralize không thành công, một :ref:`PackedInt32Array<class_PackedInt32Array>` rỗng sẽ được trả về.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
