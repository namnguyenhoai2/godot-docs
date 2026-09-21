:github_url: hide

.. meta::
	:keywords: batch

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/MultiMesh.xml.

.. _class_MultiMesh:

MultiMesh
=========

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Cung cấp khả năng vẽ một mesh nhiều lần với hiệu năng cao bằng cách sử dụng GPU instancing.

.. rst-class:: classref-introduction-group

Mô tả
-----

MultiMesh cung cấp khả năng instancing mesh ở cấp thấp. Việc vẽ hàng nghìn node :ref:`MeshInstance3D<class_MeshInstance3D>` có thể chậm, vì mỗi đối tượng được gửi đến GPU rồi vẽ riêng lẻ.

MultiMesh nhanh hơn nhiều vì có thể vẽ hàng nghìn instance chỉ bằng một draw call, giúp giảm overhead của API.

Điểm bất lợi là nếu các instance ở quá xa nhau, hiệu năng có thể bị giảm vì mọi instance đơn lẻ luôn được render (chúng được lập chỉ mục không gian như một đối tượng duy nhất, cho toàn bộ object).

Vì các instance có thể có bất kỳ hành vi nào, AABB dùng cho visibility phải do người dùng cung cấp.

\ **Lưu ý:** Một MultiMesh là một đối tượng duy nhất, do đó vẫn áp dụng giới hạn số lượng light tối đa trên mỗi đối tượng. Điều này có nghĩa là một khi số light tối đa đã được một hoặc nhiều instance sử dụng, các instance còn lại của MultiMesh sẽ **không** nhận được bất kỳ ánh sáng nào.

\ **Lưu ý:** Blend Shapes sẽ bị bỏ qua nếu được sử dụng trong một MultiMesh.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Sử dụng MultiMeshInstance <../tutorials/3d/using_multi_mesh_instance>`

- :doc:`Tối ưu hóa bằng MultiMeshes <../tutorials/performance/using_multimesh>`

- :doc:`Tạo hoạt ảnh cho hàng nghìn con cá bằng MultiMeshInstance <../tutorials/performance/vertex_animation/animating_thousands_of_fish>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>`                            | :ref:`buffer<class_MultiMesh_property_buffer>`                                               | ``PackedFloat32Array()``   |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>`                                | :ref:`color_array<class_MultiMesh_property_color_array>`                                     |                            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`AABB<class_AABB>`                                                        | :ref:`custom_aabb<class_MultiMesh_property_custom_aabb>`                                     | ``AABB(0, 0, 0, 0, 0, 0)`` |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedColorArray<class_PackedColorArray>`                                | :ref:`custom_data_array<class_MultiMesh_property_custom_data_array>`                         |                            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`int<class_int>`                                                          | :ref:`instance_count<class_MultiMesh_property_instance_count>`                               | ``0``                      |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`Mesh<class_Mesh>`                                                        | :ref:`mesh<class_MultiMesh_property_mesh>`                                                   |                            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PhysicsInterpolationQuality<enum_MultiMesh_PhysicsInterpolationQuality>` | :ref:`physics_interpolation_quality<class_MultiMesh_property_physics_interpolation_quality>` | ``0``                      |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedVector2Array<class_PackedVector2Array>`                            | :ref:`transform_2d_array<class_MultiMesh_property_transform_2d_array>`                       |                            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>`                            | :ref:`transform_array<class_MultiMesh_property_transform_array>`                             |                            |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`TransformFormat<enum_MultiMesh_TransformFormat>`                         | :ref:`transform_format<class_MultiMesh_property_transform_format>`                           | ``0``                      |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`use_colors<class_MultiMesh_property_use_colors>`                                       | ``false``                  |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`bool<class_bool>`                                                        | :ref:`use_custom_data<class_MultiMesh_property_use_custom_data>`                             | ``false``                  |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+
   | :ref:`int<class_int>`                                                          | :ref:`visible_instance_count<class_MultiMesh_property_visible_instance_count>`               | ``-1``                     |
   +--------------------------------------------------------------------------------+----------------------------------------------------------------------------------------------+----------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`AABB<class_AABB>`               | :ref:`get_aabb<class_MultiMesh_method_get_aabb>`\ (\ ) |const|                                                                                                                                                             |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`             | :ref:`get_instance_color<class_MultiMesh_method_get_instance_color>`\ (\ instance\: :ref:`int<class_int>`\ ) |const|                                                                                                       |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`             | :ref:`get_instance_custom_data<class_MultiMesh_method_get_instance_custom_data>`\ (\ instance\: :ref:`int<class_int>`\ ) |const|                                                                                           |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>` | :ref:`get_instance_transform<class_MultiMesh_method_get_instance_transform>`\ (\ instance\: :ref:`int<class_int>`\ ) |const|                                                                                               |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`get_instance_transform_2d<class_MultiMesh_method_get_instance_transform_2d>`\ (\ instance\: :ref:`int<class_int>`\ ) |const|                                                                                         |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`reset_instance_physics_interpolation<class_MultiMesh_method_reset_instance_physics_interpolation>`\ (\ instance\: :ref:`int<class_int>`\ )                                                                           |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`reset_instances_physics_interpolation<class_MultiMesh_method_reset_instances_physics_interpolation>`\ (\ )                                                                                                           |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_buffer_interpolated<class_MultiMesh_method_set_buffer_interpolated>`\ (\ buffer_curr\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`, buffer_prev\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_instance_color<class_MultiMesh_method_set_instance_color>`\ (\ instance\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ )                                                                            |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_instance_custom_data<class_MultiMesh_method_set_instance_custom_data>`\ (\ instance\: :ref:`int<class_int>`, custom_data\: :ref:`Color<class_Color>`\ )                                                          |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_instance_transform<class_MultiMesh_method_set_instance_transform>`\ (\ instance\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ )                                                    |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_instance_transform_2d<class_MultiMesh_method_set_instance_transform_2d>`\ (\ instance\: :ref:`int<class_int>`, transform\: :ref:`Transform2D<class_Transform2D>`\ )                                              |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_MultiMesh_TransformFormat:

.. rst-class:: classref-enumeration

enum **TransformFormat**: :ref:`🔗<enum_MultiMesh_TransformFormat>`

.. _class_MultiMesh_constant_TRANSFORM_2D:

.. rst-class:: classref-enumeration-constant

:ref:`TransformFormat<enum_MultiMesh_TransformFormat>` **TRANSFORM_2D** = ``0``

Sử dụng giá trị này khi dùng các transform 2D.

.. _class_MultiMesh_constant_TRANSFORM_3D:

.. rst-class:: classref-enumeration-constant

:ref:`TransformFormat<enum_MultiMesh_TransformFormat>` **TRANSFORM_3D** = ``1``

Sử dụng giá trị này khi dùng các transform 3D.

.. rst-class:: classref-item-separator

----

.. _enum_MultiMesh_PhysicsInterpolationQuality:

.. rst-class:: classref-enumeration

enum **PhysicsInterpolationQuality**: :ref:`🔗<enum_MultiMesh_PhysicsInterpolationQuality>`

.. _class_MultiMesh_constant_INTERP_QUALITY_FAST:

.. rst-class:: classref-enumeration-constant

:ref:`PhysicsInterpolationQuality<enum_MultiMesh_PhysicsInterpolationQuality>` **INTERP_QUALITY_FAST** = ``0``

Luôn nội suy bằng cách lerp Basis, điều này có thể tạo ra các hiện tượng biến dạng trong một số tình huống.

.. _class_MultiMesh_constant_INTERP_QUALITY_HIGH:

.. rst-class:: classref-enumeration-constant

:ref:`PhysicsInterpolationQuality<enum_MultiMesh_PhysicsInterpolationQuality>` **INTERP_QUALITY_HIGH** = ``1``

Cố gắng nội suy bằng cách slerp Basis (nội suy tuyến tính hình cầu) khi có thể; nếu không, chuyển sang lerp.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_MultiMesh_property_buffer:

.. rst-class:: classref-property

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **buffer** = ``PackedFloat32Array()`` :ref:`🔗<class_MultiMesh_property_buffer>`

.. rst-class:: classref-property-setget

- |void| **set_buffer**\ (\ value\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) - :ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_buffer**\ (\ )

.. container:: contribute

	Hiện chưa có mô tả cho thuộc tính này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedFloat32Array<class_PackedFloat32Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_color_array:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **color_array** :ref:`🔗<class_MultiMesh_property_color_array>`

**Đã lỗi thời:** Việc truy cập thuộc tính này rất chậm. Thay vào đó, hãy sử dụng :ref:`set_instance_color()<class_MultiMesh_method_set_instance_color>` và :ref:`get_instance_color()<class_MultiMesh_method_get_instance_color>`.

Mảng chứa từng :ref:`Color<class_Color>` được tất cả instance của mesh này sử dụng.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_custom_aabb:

.. rst-class:: classref-property

:ref:`AABB<class_AABB>` **custom_aabb** = ``AABB(0, 0, 0, 0, 0, 0)`` :ref:`🔗<class_MultiMesh_property_custom_aabb>`

.. rst-class:: classref-property-setget

- |void| **set_custom_aabb**\ (\ value\: :ref:`AABB<class_AABB>`\ ) - :ref:`AABB<class_AABB>` **get_custom_aabb**\ (\ )

AABB tùy chỉnh cho resource MultiMesh này. Việc đặt thủ công sẽ ngăn việc tính toán lại AABB tốn kém trong runtime.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_custom_data_array:

.. rst-class:: classref-property

:ref:`PackedColorArray<class_PackedColorArray>` **custom_data_array** :ref:`🔗<class_MultiMesh_property_custom_data_array>`

**Đã lỗi thời:** Việc truy cập thuộc tính này rất chậm. Thay vào đó, hãy sử dụng :ref:`set_instance_custom_data()<class_MultiMesh_method_set_instance_custom_data>` và :ref:`get_instance_custom_data()<class_MultiMesh_method_get_instance_custom_data>`.

Mảng chứa từng giá trị dữ liệu tùy chỉnh được tất cả instance của mesh này sử dụng, dưới dạng một :ref:`PackedColorArray<class_PackedColorArray>`.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedColorArray<class_PackedColorArray>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_instance_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **instance_count** = ``0`` :ref:`🔗<class_MultiMesh_property_instance_count>`

.. rst-class:: classref-property-setget

- |void| **set_instance_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_instance_count**\ (\ )

Số lượng instance sẽ được vẽ. Thao tác này xóa và thay đổi kích thước các buffer. Việc đặt data format hoặc flags sau đó sẽ không có tác dụng.

Theo mặc định, tất cả instance đều được vẽ, nhưng bạn có thể giới hạn số lượng này bằng :ref:`visible_instance_count<class_MultiMesh_property_visible_instance_count>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_mesh:

.. rst-class:: classref-property

:ref:`Mesh<class_Mesh>` **mesh** :ref:`🔗<class_MultiMesh_property_mesh>`

.. rst-class:: classref-property-setget

- |void| **set_mesh**\ (\ value\: :ref:`Mesh<class_Mesh>`\ ) - :ref:`Mesh<class_Mesh>` **get_mesh**\ (\ )

Resource :ref:`Mesh<class_Mesh>` sẽ được instancing.

Hình thức của từng instance có thể được thay đổi bằng :ref:`set_instance_color()<class_MultiMesh_method_set_instance_color>` và :ref:`set_instance_custom_data()<class_MultiMesh_method_set_instance_custom_data>`.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_physics_interpolation_quality:

.. rst-class:: classref-property

:ref:`PhysicsInterpolationQuality<enum_MultiMesh_PhysicsInterpolationQuality>` **physics_interpolation_quality** = ``0`` :ref:`🔗<class_MultiMesh_property_physics_interpolation_quality>`

.. rst-class:: classref-property-setget

- |void| **set_physics_interpolation_quality**\ (\ value\: :ref:`PhysicsInterpolationQuality<enum_MultiMesh_PhysicsInterpolationQuality>`\ ) - :ref:`PhysicsInterpolationQuality<enum_MultiMesh_PhysicsInterpolationQuality>` **get_physics_interpolation_quality**\ (\ )

Chọn sử dụng phương pháp interpolation ưu tiên tốc độ hay chất lượng.

Khi sử dụng physics tick rate thấp (thường dưới 20) hoặc tốc độ xoay của object cao, bạn có thể nhận được kết quả tốt hơn với thiết lập chất lượng cao.

\ **Lưu ý:** Chất lượng nhanh không đồng nghĩa với chất lượng thấp. Ngoại trừ các trường hợp đặc biệt nêu trên, chất lượng phải tương đương với chất lượng cao.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_transform_2d_array:

.. rst-class:: classref-property

:ref:`PackedVector2Array<class_PackedVector2Array>` **transform_2d_array** :ref:`🔗<class_MultiMesh_property_transform_2d_array>`

**Đã lỗi thời:** Việc truy cập thuộc tính này rất chậm. Thay vào đó, hãy sử dụng :ref:`set_instance_transform_2d()<class_MultiMesh_method_set_instance_transform_2d>` và :ref:`get_instance_transform_2d()<class_MultiMesh_method_get_instance_transform_2d>`.

Mảng chứa từng giá trị :ref:`Transform2D<class_Transform2D>` được tất cả instance của mesh này sử dụng, dưới dạng một :ref:`PackedVector2Array<class_PackedVector2Array>`. Mỗi transform được chia thành 3 giá trị :ref:`Vector2<class_Vector2>` tương ứng với ``x``, ``y`` và ``origin`` của các transform.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector2Array<class_PackedVector2Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_transform_array:

.. rst-class:: classref-property

:ref:`PackedVector3Array<class_PackedVector3Array>` **transform_array** :ref:`🔗<class_MultiMesh_property_transform_array>`

**Đã lỗi thời:** Việc truy cập thuộc tính này rất chậm. Thay vào đó, hãy sử dụng :ref:`set_instance_transform()<class_MultiMesh_method_set_instance_transform>` và :ref:`get_instance_transform()<class_MultiMesh_method_get_instance_transform>`.

Mảng chứa từng giá trị :ref:`Transform3D<class_Transform3D>` được tất cả instance của mesh này sử dụng, dưới dạng một :ref:`PackedVector3Array<class_PackedVector3Array>`. Mỗi transform được chia thành 4 giá trị :ref:`Vector3<class_Vector3>` tương ứng với ``x``, ``y``, ``z`` và ``origin`` của các transform.

**Lưu ý:** Mảng được trả về là một bản *sao chép* và mọi thay đổi đối với mảng đó sẽ không cập nhật giá trị thuộc tính ban đầu. Xem :ref:`PackedVector3Array<class_PackedVector3Array>` để biết thêm chi tiết.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_transform_format:

.. rst-class:: classref-property

:ref:`TransformFormat<enum_MultiMesh_TransformFormat>` **transform_format** = ``0`` :ref:`🔗<class_MultiMesh_property_transform_format>`

.. rst-class:: classref-property-setget

- |void| **set_transform_format**\ (\ value\: :ref:`TransformFormat<enum_MultiMesh_TransformFormat>`\ ) - :ref:`TransformFormat<enum_MultiMesh_TransformFormat>` **get_transform_format**\ (\ )

Định dạng của transform dùng để transform mesh, có thể là 2D hoặc 3D.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_use_colors:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_colors** = ``false`` :ref:`🔗<class_MultiMesh_property_use_colors>`

.. rst-class:: classref-property-setget

- |void| **set_use_colors**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_colors**\ (\ )

Nếu ``true``, **MultiMesh** sẽ sử dụng dữ liệu màu (xem :ref:`set_instance_color()<class_MultiMesh_method_set_instance_color>`). Chỉ có thể đặt khi :ref:`instance_count<class_MultiMesh_property_instance_count>` là ``0`` hoặc nhỏ hơn. Điều này có nghĩa là bạn cần gọi method này trước khi đặt instance count, hoặc tạm thời đặt lại thành ``0``.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_use_custom_data:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_custom_data** = ``false`` :ref:`🔗<class_MultiMesh_property_use_custom_data>`

.. rst-class:: classref-property-setget

- |void| **set_use_custom_data**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_custom_data**\ (\ )

Nếu ``true``, **MultiMesh** sẽ sử dụng dữ liệu tùy chỉnh (xem :ref:`set_instance_custom_data()<class_MultiMesh_method_set_instance_custom_data>`). Chỉ có thể đặt khi :ref:`instance_count<class_MultiMesh_property_instance_count>` là ``0`` hoặc nhỏ hơn. Điều này có nghĩa là bạn cần gọi method này trước khi đặt instance count, hoặc tạm thời đặt lại thành ``0``.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_property_visible_instance_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **visible_instance_count** = ``-1`` :ref:`🔗<class_MultiMesh_property_visible_instance_count>`

.. rst-class:: classref-property-setget

- |void| **set_visible_instance_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_visible_instance_count**\ (\ )

Giới hạn số lượng instance được vẽ; -1 sẽ vẽ tất cả instance. Việc thay đổi giá trị này không làm thay đổi kích thước các buffer.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_MultiMesh_method_get_aabb:

.. rst-class:: classref-method

:ref:`AABB<class_AABB>` **get_aabb**\ (\ ) |const| :ref:`🔗<class_MultiMesh_method_get_aabb>`

Trả về hộp giới hạn trục song song dùng cho visibility trong local space.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_get_instance_color:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_instance_color**\ (\ instance\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MultiMesh_method_get_instance_color>`

Lấy multiplier màu của một instance cụ thể.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_get_instance_custom_data:

.. rst-class:: classref-method

:ref:`Color<class_Color>` **get_instance_custom_data**\ (\ instance\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MultiMesh_method_get_instance_custom_data>`

Trả về dữ liệu tùy chỉnh đã được thiết lập cho một instance cụ thể.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_get_instance_transform:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **get_instance_transform**\ (\ instance\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MultiMesh_method_get_instance_transform>`

Trả về :ref:`Transform3D<class_Transform3D>` của một instance cụ thể.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_get_instance_transform_2d:

.. rst-class:: classref-method

:ref:`Transform2D<class_Transform2D>` **get_instance_transform_2d**\ (\ instance\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_MultiMesh_method_get_instance_transform_2d>`

Trả về :ref:`Transform2D<class_Transform2D>` của một instance cụ thể.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_reset_instance_physics_interpolation:

.. rst-class:: classref-method

|void| **reset_instance_physics_interpolation**\ (\ instance\: :ref:`int<class_int>`\ ) :ref:`🔗<class_MultiMesh_method_reset_instance_physics_interpolation>`

Khi sử dụng *physics interpolation*, hàm này cho phép bạn ngăn việc nội suy một instance trong tick vật lý hiện tại.

Điều này cho phép bạn di chuyển các instance ngay lập tức và thường nên được sử dụng khi đặt một instance lần đầu, chẳng hạn như một viên đạn, để ngăn lỗi hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_reset_instances_physics_interpolation:

.. rst-class:: classref-method

|void| **reset_instances_physics_interpolation**\ (\ ) :ref:`🔗<class_MultiMesh_method_reset_instances_physics_interpolation>`

Khi sử dụng *physics interpolation*, hàm này cho phép bạn ngăn việc nội suy cho tất cả instance trong tick vật lý hiện tại.

Điều này cho phép bạn di chuyển tất cả instance ngay lập tức và thường nên được sử dụng khi đặt các instance lần đầu để ngăn lỗi hiển thị.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_set_buffer_interpolated:

.. rst-class:: classref-method

|void| **set_buffer_interpolated**\ (\ buffer_curr\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`, buffer_prev\: :ref:`PackedFloat32Array<class_PackedFloat32Array>`\ ) :ref:`🔗<class_MultiMesh_method_set_buffer_interpolated>`

Một phương án thay thế cho việc thiết lập thuộc tính :ref:`buffer<class_MultiMesh_property_buffer>`, có thể được sử dụng với *physics interpolation*. Phương thức này nhận hai mảng và có thể thiết lập dữ liệu cho tick hiện tại và tick trước đó trong một lần gọi. Renderer sẽ tự động nội suy dữ liệu ở mỗi frame.

Điều này hữu ích trong các trường hợp thứ tự của các instance có thể thay đổi từ tick vật lý này sang tick vật lý khác, chẳng hạn như các hệ thống particle.

Khi thứ tự của các instance nhất quán, vẫn có thể sử dụng phương án đơn giản hơn là thiết lập :ref:`buffer<class_MultiMesh_property_buffer>` cùng với interpolation.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_set_instance_color:

.. rst-class:: classref-method

|void| **set_instance_color**\ (\ instance\: :ref:`int<class_int>`, color\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_MultiMesh_method_set_instance_color>`

Thiết lập màu của một instance cụ thể bằng cách *nhân* với màu vertex hiện có của mesh. Điều này cho phép tạo sắc màu khác nhau cho từng instance.

\ **Lưu ý:** Mỗi thành phần được lưu trữ bằng 32 bit trong các phương thức rendering Forward+ và Mobile, nhưng được đóng gói thành 16 bit trong phương thức rendering Compatibility.

Để màu có hiệu lực, hãy đảm bảo :ref:`use_colors<class_MultiMesh_property_use_colors>` là ``true`` trên **MultiMesh** và :ref:`BaseMaterial3D.vertex_color_use_as_albedo<class_BaseMaterial3D_property_vertex_color_use_as_albedo>` là ``true`` trên material. Nếu bạn định thiết lập một màu tuyệt đối thay vì tạo sắc màu, hãy đảm bảo màu albedo của material được đặt thành màu trắng thuần (``Color(1, 1, 1)``).

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_set_instance_custom_data:

.. rst-class:: classref-method

|void| **set_instance_custom_data**\ (\ instance\: :ref:`int<class_int>`, custom_data\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_MultiMesh_method_set_instance_custom_data>`

Thiết lập dữ liệu tùy chỉnh cho một instance cụ thể. ``custom_data`` chỉ là một kiểu :ref:`Color<class_Color>` dùng để chứa 4 số dấu phẩy động.

\ **Lưu ý:** Mỗi số được lưu trữ bằng 32 bit trong các phương thức rendering Forward+ và Mobile, nhưng được đóng gói thành 16 bit trong phương thức rendering Compatibility.

Để dữ liệu tùy chỉnh được sử dụng, hãy đảm bảo :ref:`use_custom_data<class_MultiMesh_property_use_custom_data>` là ``true``.

Dữ liệu instance tùy chỉnh này phải được truy cập thủ công trong custom shader bằng ``INSTANCE_CUSTOM``.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_set_instance_transform:

.. rst-class:: classref-method

|void| **set_instance_transform**\ (\ instance\: :ref:`int<class_int>`, transform\: :ref:`Transform3D<class_Transform3D>`\ ) :ref:`🔗<class_MultiMesh_method_set_instance_transform>`

Thiết lập :ref:`Transform3D<class_Transform3D>` cho một instance cụ thể.

.. rst-class:: classref-item-separator

----

.. _class_MultiMesh_method_set_instance_transform_2d:

.. rst-class:: classref-method

|void| **set_instance_transform_2d**\ (\ instance\: :ref:`int<class_int>`, transform\: :ref:`Transform2D<class_Transform2D>`\ ) :ref:`🔗<class_MultiMesh_method_set_instance_transform_2d>`

Thiết lập :ref:`Transform2D<class_Transform2D>` cho một instance cụ thể.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
