:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Curve3D.xml.

.. _class_Curve3D:

Curve3D
=======

**Kế thừa:** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Mô tả một đường cong Bézier trong không gian 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này mô tả một đường cong Bézier trong không gian 3D. Lớp này chủ yếu được dùng để tạo hình dạng cho :ref:`Path3D<class_Path3D>`, nhưng cũng có thể được lấy mẫu thủ công cho các mục đích khác.

Lớp này lưu một bộ nhớ đệm gồm các điểm được tính toán trước dọc theo đường cong để tăng tốc các phép tính tiếp theo.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`bake_interval<class_Curve3D_property_bake_interval>`                   | ``0.2``              |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`       | :ref:`closed<class_Curve3D_property_closed>`                                 | ``false``            |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`int<class_int>`         | :ref:`point_count<class_Curve3D_property_point_count>`                       | ``0``                |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`point_{index}/in<class_Curve3D_property_point_{index}/in>`             | ``Vector3(0, 0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`point_{index}/out<class_Curve3D_property_point_{index}/out>`           | ``Vector3(0, 0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`point_{index}/position<class_Curve3D_property_point_{index}/position>` | ``Vector3(0, 0, 0)`` |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`float<class_float>`     | :ref:`point_{index}/tilt<class_Curve3D_property_point_{index}/tilt>`         | ``0.0``              |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+
   | :ref:`bool<class_bool>`       | :ref:`up_vector_enabled<class_Curve3D_property_up_vector_enabled>`           | ``true``             |
   +-------------------------------+------------------------------------------------------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`add_point<class_Curve3D_method_add_point>`\ (\ position\: :ref:`Vector3<class_Vector3>`, in\: :ref:`Vector3<class_Vector3>` = Vector3(0, 0, 0), out\: :ref:`Vector3<class_Vector3>` = Vector3(0, 0, 0), index\: :ref:`int<class_int>` = -1\ ) |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`clear_points<class_Curve3D_method_clear_points>`\ (\ )                                                                                                                                                                                        |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_baked_length<class_Curve3D_method_get_baked_length>`\ (\ ) |const|                                                                                                                                                                        |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_baked_points<class_Curve3D_method_get_baked_points>`\ (\ ) |const|                                                                                                                                                                        |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedFloat32Array<class_PackedFloat32Array>` | :ref:`get_baked_tilts<class_Curve3D_method_get_baked_tilts>`\ (\ ) |const|                                                                                                                                                                          |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`get_baked_up_vectors<class_Curve3D_method_get_baked_up_vectors>`\ (\ ) |const|                                                                                                                                                                |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_closest_offset<class_Curve3D_method_get_closest_offset>`\ (\ to_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                          |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`get_closest_point<class_Curve3D_method_get_closest_point>`\ (\ to_point\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                            |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`get_point_in<class_Curve3D_method_get_point_in>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                   |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`get_point_out<class_Curve3D_method_get_point_out>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                                 |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`get_point_position<class_Curve3D_method_get_point_position>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                       |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`                           | :ref:`get_point_tilt<class_Curve3D_method_get_point_tilt>`\ (\ idx\: :ref:`int<class_int>`\ ) |const|                                                                                                                                               |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`remove_point<class_Curve3D_method_remove_point>`\ (\ idx\: :ref:`int<class_int>`\ )                                                                                                                                                           |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`sample<class_Curve3D_method_sample>`\ (\ idx\: :ref:`int<class_int>`, t\: :ref:`float<class_float>`\ ) |const|                                                                                                                                |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`sample_baked<class_Curve3D_method_sample_baked>`\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false\ ) |const|                                                                                             |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`sample_baked_up_vector<class_Curve3D_method_sample_baked_up_vector>`\ (\ offset\: :ref:`float<class_float>`, apply_tilt\: :ref:`bool<class_bool>` = false\ ) |const|                                                                          |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Transform3D<class_Transform3D>`               | :ref:`sample_baked_with_rotation<class_Curve3D_method_sample_baked_with_rotation>`\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false, apply_tilt\: :ref:`bool<class_bool>` = false\ ) |const|                   |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`                       | :ref:`samplef<class_Curve3D_method_samplef>`\ (\ fofs\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                        |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_in<class_Curve3D_method_set_point_in>`\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ )                                                                                                                 |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_out<class_Curve3D_method_set_point_out>`\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ )                                                                                                               |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_position<class_Curve3D_method_set_point_position>`\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ )                                                                                                     |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                              | :ref:`set_point_tilt<class_Curve3D_method_set_point_tilt>`\ (\ idx\: :ref:`int<class_int>`, tilt\: :ref:`float<class_float>`\ )                                                                                                                     |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`tessellate<class_Curve3D_method_tessellate>`\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_degrees\: :ref:`float<class_float>` = 4\ ) |const|                                                                                         |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedVector3Array<class_PackedVector3Array>` | :ref:`tessellate_even_length<class_Curve3D_method_tessellate_even_length>`\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_length\: :ref:`float<class_float>` = 0.2\ ) |const|                                                                |
   +-----------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Curve3D_property_bake_interval:

.. rst-class:: classref-property

:ref:`float<class_float>` **bake_interval** = ``0.2`` :ref:`🔗<class_Curve3D_property_bake_interval>`

.. rst-class:: classref-property-setget

- |void| **set_bake_interval**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bake_interval**\ (\ )

Khoảng cách tính bằng mét giữa hai điểm liền kề trong bộ nhớ đệm. Việc thay đổi giá trị này buộc bộ nhớ đệm phải được tính toán lại vào lần tiếp theo hàm :ref:`get_baked_points()<class_Curve3D_method_get_baked_points>` hoặc :ref:`get_baked_length()<class_Curve3D_method_get_baked_length>` được gọi. Khoảng cách càng nhỏ thì số điểm trong bộ nhớ đệm càng nhiều và càng tiêu tốn nhiều bộ nhớ, vì vậy hãy sử dụng cẩn thận.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_closed:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **closed** = ``false`` :ref:`🔗<class_Curve3D_property_closed>`

.. rst-class:: classref-property-setget

- |void| **set_closed**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_closed**\ (\ )

Nếu ``true``, và đường cong có nhiều hơn 2 điểm điều khiển, điểm cuối và điểm đầu sẽ được nối thành một vòng lặp.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_point_count:

.. rst-class:: classref-property

:ref:`int<class_int>` **point_count** = ``0`` :ref:`🔗<class_Curve3D_property_point_count>`

.. rst-class:: classref-property-setget

- |void| **set_point_count**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_point_count**\ (\ )

Số điểm mô tả đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_point_{index}/in:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **point_{index}/in** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_Curve3D_property_point_{index}/in>`

Vị trí của điểm điều khiển dẫn đến đỉnh tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_point_{index}/out:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **point_{index}/out** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_Curve3D_property_point_{index}/out>`

Vị trí của điểm điều khiển dẫn ra khỏi đỉnh tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_point_{index}/position:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **point_{index}/position** = ``Vector3(0, 0, 0)`` :ref:`🔗<class_Curve3D_property_point_{index}/position>`

Vị trí của đỉnh tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_point_{index}/tilt:

.. rst-class:: classref-property

:ref:`float<class_float>` **point_{index}/tilt** = ``0.0`` :ref:`🔗<class_Curve3D_property_point_{index}/tilt>`

Góc nghiêng tính bằng radian của điểm tại ``index``.

\ **Lưu ý:** ``index`` là một giá trị trong phạm vi ``0 .. point_count - 1``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_property_up_vector_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **up_vector_enabled** = ``true`` :ref:`🔗<class_Curve3D_property_up_vector_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_up_vector_enabled**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_up_vector_enabled**\ (\ )

Nếu ``true``, đường cong sẽ tạo bộ nhớ đệm cho các vector hướng lên được dùng để định hướng. Tính năng này được sử dụng khi :ref:`PathFollow3D.rotation_mode<class_PathFollow3D_property_rotation_mode>` được đặt thành :ref:`PathFollow3D.ROTATION_ORIENTED<class_PathFollow3D_constant_ROTATION_ORIENTED>`. Việc thay đổi giá trị này buộc bộ nhớ đệm phải được tính toán lại.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Curve3D_method_add_point:

.. rst-class:: classref-method

|void| **add_point**\ (\ position\: :ref:`Vector3<class_Vector3>`, in\: :ref:`Vector3<class_Vector3>` = Vector3(0, 0, 0), out\: :ref:`Vector3<class_Vector3>` = Vector3(0, 0, 0), index\: :ref:`int<class_int>` = -1\ ) :ref:`🔗<class_Curve3D_method_add_point>`

Thêm một điểm với ``position`` được chỉ định, tương đối với vị trí riêng của đường cong, cùng các điểm điều khiển ``in`` và ``out``. Nối điểm mới vào cuối danh sách điểm.

Nếu ``index`` được cung cấp, điểm mới sẽ được chèn trước điểm hiện có được xác định bằng chỉ mục ``index``. Mọi điểm hiện có bắt đầu từ ``index`` sẽ được dịch xuống dưới trong danh sách điểm. Chỉ mục phải lớn hơn hoặc bằng ``0`` và không được vượt quá số điểm hiện có trong đường. Xem :ref:`point_count<class_Curve3D_property_point_count>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_clear_points:

.. rst-class:: classref-method

|void| **clear_points**\ (\ ) :ref:`🔗<class_Curve3D_method_clear_points>`

Xóa tất cả các điểm khỏi đường cong.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_baked_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_baked_length**\ (\ ) |const| :ref:`🔗<class_Curve3D_method_get_baked_length>`

Trả về tổng độ dài của đường cong, dựa trên các điểm được lưu trong bộ nhớ đệm. Với mật độ đủ cao (xem :ref:`bake_interval<class_Curve3D_property_bake_interval>`), kết quả sẽ đủ gần đúng.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_baked_points:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_baked_points**\ (\ ) |const| :ref:`🔗<class_Curve3D_method_get_baked_points>`

Trả về bộ nhớ đệm các điểm dưới dạng :ref:`PackedVector3Array<class_PackedVector3Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_baked_tilts:

.. rst-class:: classref-method

:ref:`PackedFloat32Array<class_PackedFloat32Array>` **get_baked_tilts**\ (\ ) |const| :ref:`🔗<class_Curve3D_method_get_baked_tilts>`

Trả về bộ nhớ đệm các góc nghiêng dưới dạng :ref:`PackedFloat32Array<class_PackedFloat32Array>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_baked_up_vectors:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **get_baked_up_vectors**\ (\ ) |const| :ref:`🔗<class_Curve3D_method_get_baked_up_vectors>`

Trả về bộ nhớ đệm các vector hướng lên dưới dạng :ref:`PackedVector3Array<class_PackedVector3Array>`.

Nếu :ref:`up_vector_enabled<class_Curve3D_property_up_vector_enabled>` là ``false``, bộ nhớ đệm sẽ trống.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_closest_offset:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_closest_offset**\ (\ to_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Curve3D_method_get_closest_offset>`

Trả về offset gần nhất với ``to_point``. Offset này được dùng trong :ref:`sample_baked()<class_Curve3D_method_sample_baked>` hoặc :ref:`sample_baked_up_vector()<class_Curve3D_method_sample_baked_up_vector>`.

\ ``to_point`` phải nằm trong không gian cục bộ của đường cong này.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_closest_point:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_closest_point**\ (\ to_point\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Curve3D_method_get_closest_point>`

Trả về điểm gần ``to_point`` nhất trên các đoạn đã tạo bộ nhớ đệm (trong không gian cục bộ của đường cong).

\ ``to_point`` phải nằm trong không gian cục bộ của đường cong này.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_point_in:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_point_in**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve3D_method_get_point_in>`

Trả về vị trí của điểm điều khiển dẫn đến đỉnh ``idx``. Vị trí trả về tương đối với đỉnh ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``(0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_point_out:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_point_out**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve3D_method_get_point_out>`

Trả về vị trí của điểm điều khiển dẫn ra khỏi đỉnh ``idx``. Vị trí trả về tương đối với đỉnh ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``(0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_point_position:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_point_position**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve3D_method_get_point_position>`

Trả về vị trí của đỉnh ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``(0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_get_point_tilt:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_point_tilt**\ (\ idx\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_Curve3D_method_get_point_tilt>`

Trả về góc nghiêng tính bằng radian của điểm ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console và trả về ``0``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_remove_point:

.. rst-class:: classref-method

|void| **remove_point**\ (\ idx\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Curve3D_method_remove_point>`

Xóa điểm ``idx`` khỏi đường cong. Gửi lỗi đến console nếu ``idx`` nằm ngoài phạm vi.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_sample:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **sample**\ (\ idx\: :ref:`int<class_int>`, t\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Curve3D_method_sample>`

Trả về vị trí giữa đỉnh ``idx`` và đỉnh ``idx + 1``, trong đó ``t`` xác định điểm là đỉnh đầu tiên (``t = 0.0``), đỉnh cuối cùng (``t = 1.0``) hay nằm ở giữa. Các giá trị của ``t`` nằm ngoài phạm vi (``0.0 >= t <=1``) sẽ cho kết quả bất thường nhưng có thể dự đoán được.

Nếu ``idx`` nằm ngoài phạm vi, giá trị này sẽ bị giới hạn về đỉnh đầu tiên hoặc cuối cùng, còn ``t`` sẽ bị bỏ qua. Nếu đường cong không có điểm nào, hàm sẽ gửi lỗi đến console và trả về ``(0, 0, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_sample_baked:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **sample_baked**\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Curve3D_method_sample_baked>`

Trả về một điểm trên đường cong tại vị trí ``offset``, trong đó ``offset`` được đo bằng khoảng cách theo đơn vị 3D dọc theo đường cong. Để thực hiện việc này, hàm tìm hai điểm được lưu trong bộ nhớ đệm mà ``offset`` nằm giữa, sau đó nội suy các giá trị. Phép nội suy này là cubic nếu ``cubic`` được đặt thành ``true``, hoặc linear nếu được đặt thành ``false``.

Phép nội suy cubic thường bám theo đường cong tốt hơn, nhưng linear nhanh hơn (và thường đủ chính xác).

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_sample_baked_up_vector:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **sample_baked_up_vector**\ (\ offset\: :ref:`float<class_float>`, apply_tilt\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Curve3D_method_sample_baked_up_vector>`

Trả về một vector hướng lên trên đường cong tại vị trí ``offset``, trong đó ``offset`` được đo bằng khoảng cách theo đơn vị 3D dọc theo đường cong. Để thực hiện việc này, hàm tìm hai vector hướng lên được lưu trong bộ nhớ đệm mà ``offset`` nằm giữa, sau đó nội suy các giá trị. Nếu ``apply_tilt`` là ``true``, một góc nghiêng đã nội suy sẽ được áp dụng cho vector hướng lên đã nội suy.

Nếu đường cong không có vector hướng lên, hàm sẽ gửi lỗi đến console và trả về ``(0, 1, 0)``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_sample_baked_with_rotation:

.. rst-class:: classref-method

:ref:`Transform3D<class_Transform3D>` **sample_baked_with_rotation**\ (\ offset\: :ref:`float<class_float>` = 0.0, cubic\: :ref:`bool<class_bool>` = false, apply_tilt\: :ref:`bool<class_bool>` = false\ ) |const| :ref:`🔗<class_Curve3D_method_sample_baked_with_rotation>`

Trả về một :ref:`Transform3D<class_Transform3D>` với ``origin`` là vị trí điểm, ``basis.x`` là vector ngang, ``basis.y`` là vector hướng lên và ``basis.z`` là vector hướng về phía trước. Khi độ dài đường cong bằng 0, không có cách hợp lý nào để tính phép xoay; tất cả các vector đều được căn chỉnh theo các trục của không gian toàn cục. Xem thêm :ref:`sample_baked()<class_Curve3D_method_sample_baked>`.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_samplef:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **samplef**\ (\ fofs\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Curve3D_method_samplef>`

Trả về vị trí tại đỉnh ``fofs``. Hàm gọi :ref:`sample()<class_Curve3D_method_sample>` bằng cách sử dụng phần nguyên của ``fofs`` làm ``idx`` và phần thập phân của nó làm ``t``.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_set_point_in:

.. rst-class:: classref-method

|void| **set_point_in**\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Curve3D_method_set_point_in>`

Đặt vị trí của điểm điều khiển dẫn đến đỉnh ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console. Vị trí này tương đối với đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_set_point_out:

.. rst-class:: classref-method

|void| **set_point_out**\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Curve3D_method_set_point_out>`

Đặt vị trí của điểm điều khiển dẫn ra khỏi đỉnh ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console. Vị trí này tương đối với đỉnh.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_set_point_position:

.. rst-class:: classref-method

|void| **set_point_position**\ (\ idx\: :ref:`int<class_int>`, position\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Curve3D_method_set_point_position>`

Đặt vị trí cho đỉnh ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_set_point_tilt:

.. rst-class:: classref-method

|void| **set_point_tilt**\ (\ idx\: :ref:`int<class_int>`, tilt\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Curve3D_method_set_point_tilt>`

Đặt góc nghiêng tính bằng radian cho điểm ``idx``. Nếu chỉ mục nằm ngoài phạm vi, hàm sẽ gửi lỗi đến console.

Độ nghiêng điều khiển góc xoay của một đối tượng di chuyển dọc theo đường đi quanh trục hướng tới. Trong trường hợp một đường cong điều khiển :ref:`PathFollow3D<class_PathFollow3D>`, độ nghiêng này là một độ lệch so với độ nghiêng tự nhiên mà :ref:`PathFollow3D<class_PathFollow3D>` tính toán.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_tessellate:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **tessellate**\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_degrees\: :ref:`float<class_float>` = 4\ ) |const| :ref:`🔗<class_Curve3D_method_tessellate>`

Trả về danh sách các điểm dọc theo đường cong, với mật độ điểm được điều khiển theo độ cong. Điều đó có nghĩa là các phần cong hơn sẽ có nhiều điểm hơn các phần thẳng hơn.

Phép xấp xỉ này tạo các đoạn thẳng giữa từng cặp điểm, sau đó chia nhỏ các đoạn đó cho đến khi hình dạng thu được đủ tương đồng.

\ ``max_stages`` kiểm soát số lần chia nhỏ mà một đoạn đường cong có thể trải qua trước khi được xem là đủ gần đúng. Mỗi lần chia nhỏ sẽ tách đoạn thành hai nửa, vì vậy 5 giai đoạn mặc định có thể tương đương với tối đa 32 lần chia nhỏ cho mỗi đoạn đường cong. Hãy tăng giá trị này một cách thận trọng!

\ ``tolerance_degrees`` kiểm soát số độ mà điểm giữa của một đoạn có thể lệch so với đường cong thực trước khi đoạn đó phải được chia nhỏ.

.. rst-class:: classref-item-separator

----

.. _class_Curve3D_method_tessellate_even_length:

.. rst-class:: classref-method

:ref:`PackedVector3Array<class_PackedVector3Array>` **tessellate_even_length**\ (\ max_stages\: :ref:`int<class_int>` = 5, tolerance_length\: :ref:`float<class_float>` = 0.2\ ) |const| :ref:`🔗<class_Curve3D_method_tessellate_even_length>`

Trả về danh sách các điểm dọc theo đường cong, với mật độ gần như đồng đều. ``max_stages`` kiểm soát số lần chia nhỏ mà một đoạn đường cong có thể trải qua trước khi được xem là đủ gần đúng. Mỗi lần chia nhỏ sẽ tách đoạn thành hai nửa, vì vậy 5 giai đoạn mặc định có thể tương đương với tối đa 32 lần chia nhỏ cho mỗi đoạn đường cong. Hãy tăng giá trị này một cách thận trọng!

\ ``tolerance_length`` kiểm soát khoảng cách tối đa giữa hai điểm lân cận trước khi đoạn đó phải được chia nhỏ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
