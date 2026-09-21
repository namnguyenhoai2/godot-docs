:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/MeshConvexDecompositionSettings.xml.

.. _class_MeshConvexDecompositionSettings:

MeshConvexDecompositionSettings
===============================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Các tham số được sử dụng với thao tác phân rã lồi :ref:`Mesh<class_Mesh>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Các tham số được sử dụng với thao tác phân rã lồi :ref:`Mesh<class_Mesh>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`bool<class_bool>`                                | :ref:`convex_hull_approximation<class_MeshConvexDecompositionSettings_property_convex_hull_approximation>`               | ``true``   |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`int<class_int>`                                  | :ref:`convex_hull_downsampling<class_MeshConvexDecompositionSettings_property_convex_hull_downsampling>`                 | ``4``      |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                              | :ref:`max_concavity<class_MeshConvexDecompositionSettings_property_max_concavity>`                                       | ``1.0``    |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`int<class_int>`                                  | :ref:`max_convex_hulls<class_MeshConvexDecompositionSettings_property_max_convex_hulls>`                                 | ``1``      |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`int<class_int>`                                  | :ref:`max_num_vertices_per_convex_hull<class_MeshConvexDecompositionSettings_property_max_num_vertices_per_convex_hull>` | ``32``     |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                              | :ref:`min_volume_per_convex_hull<class_MeshConvexDecompositionSettings_property_min_volume_per_convex_hull>`             | ``0.0001`` |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`Mode<enum_MeshConvexDecompositionSettings_Mode>` | :ref:`mode<class_MeshConvexDecompositionSettings_property_mode>`                                                         | ``0``      |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`bool<class_bool>`                                | :ref:`normalize_mesh<class_MeshConvexDecompositionSettings_property_normalize_mesh>`                                     | ``false``  |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`int<class_int>`                                  | :ref:`plane_downsampling<class_MeshConvexDecompositionSettings_property_plane_downsampling>`                             | ``4``      |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`bool<class_bool>`                                | :ref:`project_hull_vertices<class_MeshConvexDecompositionSettings_property_project_hull_vertices>`                       | ``true``   |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`int<class_int>`                                  | :ref:`resolution<class_MeshConvexDecompositionSettings_property_resolution>`                                             | ``10000``  |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                              | :ref:`revolution_axes_clipping_bias<class_MeshConvexDecompositionSettings_property_revolution_axes_clipping_bias>`       | ``0.05``   |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+
   | :ref:`float<class_float>`                              | :ref:`symmetry_planes_clipping_bias<class_MeshConvexDecompositionSettings_property_symmetry_planes_clipping_bias>`       | ``0.05``   |
   +--------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------+------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_MeshConvexDecompositionSettings_Mode:

.. rst-class:: classref-enumeration

enum **Mode**: :ref:`🔗<enum_MeshConvexDecompositionSettings_Mode>`

.. _class_MeshConvexDecompositionSettings_constant_CONVEX_DECOMPOSITION_MODE_VOXEL:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_MeshConvexDecompositionSettings_Mode>` **CONVEX_DECOMPOSITION_MODE_VOXEL** = ``0``

Hằng số cho phép phân rã lồi xấp xỉ dựa trên voxel.

.. _class_MeshConvexDecompositionSettings_constant_CONVEX_DECOMPOSITION_MODE_TETRAHEDRON:

.. rst-class:: classref-enumeration-constant

:ref:`Mode<enum_MeshConvexDecompositionSettings_Mode>` **CONVEX_DECOMPOSITION_MODE_TETRAHEDRON** = ``1``

Hằng số cho phép phân rã lồi xấp xỉ dựa trên tứ diện.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MeshConvexDecompositionSettings_property_convex_hull_approximation:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **convex_hull_approximation** = ``true`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_convex_hull_approximation>`

.. rst-class:: classref-property-setget

- |void| **set_convex_hull_approximation**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_convex_hull_approximation**\ (\ )

Nếu ``true``, sử dụng phép xấp xỉ để tính các convex hull.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_convex_hull_downsampling:

.. rst-class:: classref-property

:ref:`int<class_int>` **convex_hull_downsampling** = ``4`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_convex_hull_downsampling>`

.. rst-class:: classref-property-setget

- |void| **set_convex_hull_downsampling**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_convex_hull_downsampling**\ (\ )

Kiểm soát độ chính xác của quy trình tạo convex hull trong giai đoạn lựa chọn mặt phẳng cắt. Phạm vi từ ``1`` đến ``16``.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_max_concavity:

.. rst-class:: classref-property

:ref:`float<class_float>` **max_concavity** = ``1.0`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_max_concavity>`

.. rst-class:: classref-property-setget

- |void| **set_max_concavity**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_max_concavity**\ (\ )

Độ lõm tối đa. Phạm vi từ ``0.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_max_convex_hulls:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_convex_hulls** = ``1`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_max_convex_hulls>`

.. rst-class:: classref-property-setget

- |void| **set_max_convex_hulls**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_convex_hulls**\ (\ )

Số lượng convex hull tối đa được tạo ra từ thao tác hợp nhất.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_max_num_vertices_per_convex_hull:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_num_vertices_per_convex_hull** = ``32`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_max_num_vertices_per_convex_hull>`

.. rst-class:: classref-property-setget

- |void| **set_max_num_vertices_per_convex_hull**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_num_vertices_per_convex_hull**\ (\ )

Kiểm soát số lượng tam giác tối đa trên mỗi convex hull. Phạm vi từ ``4`` đến ``1024``.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_min_volume_per_convex_hull:

.. rst-class:: classref-property

:ref:`float<class_float>` **min_volume_per_convex_hull** = ``0.0001`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_min_volume_per_convex_hull>`

.. rst-class:: classref-property-setget

- |void| **set_min_volume_per_convex_hull**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_min_volume_per_convex_hull**\ (\ )

Kiểm soát việc lấy mẫu thích ứng của các convex hull được tạo. Phạm vi từ ``0.0`` đến ``0.01``.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_mode:

.. rst-class:: classref-property

:ref:`Mode<enum_MeshConvexDecompositionSettings_Mode>` **mode** = ``0`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_mode>`

.. rst-class:: classref-property-setget

- |void| **set_mode**\ (\ value\: :ref:`Mode<enum_MeshConvexDecompositionSettings_Mode>`\ ) - :ref:`Mode<enum_MeshConvexDecompositionSettings_Mode>` **get_mode**\ (\ )

Chế độ phân rã lồi xấp xỉ.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_normalize_mesh:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **normalize_mesh** = ``false`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_normalize_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_normalize_mesh**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_normalize_mesh**\ (\ )

Nếu ``true``, chuẩn hóa mesh trước khi áp dụng phép phân rã lồi.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_plane_downsampling:

.. rst-class:: classref-property

:ref:`int<class_int>` **plane_downsampling** = ``4`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_plane_downsampling>`

.. rst-class:: classref-property-setget

- |void| **set_plane_downsampling**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_plane_downsampling**\ (\ )

Kiểm soát độ chi tiết của quá trình tìm kiếm mặt phẳng cắt "tốt nhất". Phạm vi từ ``1`` đến ``16``.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_project_hull_vertices:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **project_hull_vertices** = ``true`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_project_hull_vertices>`

.. rst-class:: classref-property-setget

- |void| **set_project_hull_vertices**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_project_hull_vertices**\ (\ )

Nếu ``true``, chiếu các đỉnh convex hull đầu ra lên mesh nguồn ban đầu để tăng độ chính xác dấu phẩy động của kết quả.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_resolution:

.. rst-class:: classref-property

:ref:`int<class_int>` **resolution** = ``10000`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_resolution>`

.. rst-class:: classref-property-setget

- |void| **set_resolution**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_resolution**\ (\ )

Số voxel tối đa được tạo trong giai đoạn voxelization.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_revolution_axes_clipping_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **revolution_axes_clipping_bias** = ``0.05`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_revolution_axes_clipping_bias>`

.. rst-class:: classref-property-setget

- |void| **set_revolution_axes_clipping_bias**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_revolution_axes_clipping_bias**\ (\ )

Kiểm soát độ thiên lệch về việc cắt dọc theo các trục cách mạng. Phạm vi từ ``0.0`` đến ``1.0``.

.. rst-class:: classref-item-separator

----

.. _class_MeshConvexDecompositionSettings_property_symmetry_planes_clipping_bias:

.. rst-class:: classref-property

:ref:`float<class_float>` **symmetry_planes_clipping_bias** = ``0.05`` :ref:`🔗<class_MeshConvexDecompositionSettings_property_symmetry_planes_clipping_bias>`

.. rst-class:: classref-property-setget

- |void| **set_symmetry_planes_clipping_bias**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_symmetry_planes_clipping_bias**\ (\ )

Kiểm soát độ thiên lệch về việc cắt dọc theo các mặt phẳng đối xứng. Phạm vi từ ``0.0`` đến ``1.0``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
