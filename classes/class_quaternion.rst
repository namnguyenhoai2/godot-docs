:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/Quaternion.xml.

.. _class_Quaternion:

Quaternion
==========

Một quaternion đơn vị được dùng để biểu diễn các phép xoay 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu **Quaternion** tích hợp sẵn :ref:`Variant<class_Variant>` là một cấu trúc dữ liệu 4D biểu diễn phép xoay dưới dạng `Hamilton convention quaternion <https://en.wikipedia.org/wiki/Quaternions_and_spatial_rotation>`__. So với kiểu :ref:`Basis<class_Basis>` có thể lưu cả phép xoay và tỷ lệ, quaternion *chỉ* có thể lưu phép xoay.

Một **Quaternion** được tạo thành từ 4 thành phần số thực dấu phẩy động: :ref:`w<class_Quaternion_property_w>`, :ref:`x<class_Quaternion_property_x>`, :ref:`y<class_Quaternion_property_y>` và :ref:`z<class_Quaternion_property_z>`. Các thành phần này rất nhỏ gọn trong bộ nhớ, và nhờ đó một số phép toán hiệu quả hơn, đồng thời ít có khả năng gây ra lỗi số dấu phẩy động hơn. Các phương thức như :ref:`get_angle()<class_Quaternion_method_get_angle>`, :ref:`get_axis()<class_Quaternion_method_get_axis>` và :ref:`slerp()<class_Quaternion_method_slerp>` nhanh hơn các phương thức tương ứng của :ref:`Basis<class_Basis>`.

Để có phần giới thiệu tuyệt vời về quaternion, hãy xem `this video by 3Blue1Brown <https://www.youtube.com/watch?v=d4EgbgTm0Bg>`__. Bạn không cần biết phần toán học phía sau quaternion, vì Godot cung cấp một số phương thức trợ giúp để xử lý việc đó cho bạn. Các phương thức này bao gồm :ref:`slerp()<class_Quaternion_method_slerp>` và :ref:`spherical_cubic_interpolate()<class_Quaternion_method_spherical_cubic_interpolate>`, cũng như toán tử ``*``.

\ **Lưu ý:** Quaternion phải được chuẩn hóa trước khi được dùng để xoay (xem :ref:`normalized()<class_Quaternion_method_normalized>`).

\ **Lưu ý:** Tương tự :ref:`Vector2<class_Vector2>` và :ref:`Vector3<class_Vector3>`, các thành phần của quaternion mặc định sử dụng độ chính xác 32-bit, không giống :ref:`float<class_float>` vốn luôn là 64-bit. Nếu cần độ chính xác kép, hãy biên dịch engine với tùy chọn ``precision=double``.

\ **Lưu ý:** Trong ngữ cảnh boolean, một quaternion sẽ được đánh giá là ``false`` nếu nó bằng :ref:`IDENTITY<class_Quaternion_constant_IDENTITY>`. Nếu không, quaternion sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `3Blue1Brown's video on Quaternions <https://www.youtube.com/watch?v=d4EgbgTm0Bg>`__

- `Online Quaternion Visualization <https://quaternions.online/>`__

- `Using 3D transforms <../tutorials/3d/using_transforms.html#interpolating-with-quaternions>`__

- `Third Person Shooter (TPS) Demo <https://godotengine.org/asset-library/asset/2710>`__

- `Advanced Quaternion Visualization <https://iwatake2222.github.io/rotation_master/rotation_master.html>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`w<class_Quaternion_property_w>` | ``1.0`` |
   +---------------------------+---------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`x<class_Quaternion_property_x>` | ``0.0`` |
   +---------------------------+---------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`y<class_Quaternion_property_y>` | ``0.0`` |
   +---------------------------+---------------------------------------+---------+
   | :ref:`float<class_float>` | :ref:`z<class_Quaternion_property_z>` | ``0.0`` |
   +---------------------------+---------------------------------------+---------+

.. rst-class:: classref-reftable-group

Hàm khởi tạo
------------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`Quaternion<class_Quaternion_constructor_Quaternion>`\ (\ )                                                                                                                             |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`Quaternion<class_Quaternion_constructor_Quaternion>`\ (\ from\: :ref:`Quaternion<class_Quaternion>`\ )                                                                                 |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`Quaternion<class_Quaternion_constructor_Quaternion>`\ (\ arc_from\: :ref:`Vector3<class_Vector3>`, arc_to\: :ref:`Vector3<class_Vector3>`\ )                                           |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`Quaternion<class_Quaternion_constructor_Quaternion>`\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )                                                    |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`Quaternion<class_Quaternion_constructor_Quaternion>`\ (\ from\: :ref:`Basis<class_Basis>`\ )                                                                                           |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`Quaternion<class_Quaternion_constructor_Quaternion>`\ (\ x\: :ref:`float<class_float>`, y\: :ref:`float<class_float>`, z\: :ref:`float<class_float>`, w\: :ref:`float<class_float>`\ ) |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`angle_to<class_Quaternion_method_angle_to>`\ (\ to\: :ref:`Quaternion<class_Quaternion>`\ ) |const|                                                                                                                                                                                                                                                                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`dot<class_Quaternion_method_dot>`\ (\ with\: :ref:`Quaternion<class_Quaternion>`\ ) |const|                                                                                                                                                                                                                                                                                                         |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`exp<class_Quaternion_method_exp>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                                     |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`from_euler<class_Quaternion_method_from_euler>`\ (\ euler\: :ref:`Vector3<class_Vector3>`\ ) |static|                                                                                                                                                                                                                                                                                               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`get_angle<class_Quaternion_method_get_angle>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                         |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`get_axis<class_Quaternion_method_get_axis>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`get_euler<class_Quaternion_method_get_euler>`\ (\ order\: :ref:`int<class_int>` = 2\ ) |const|                                                                                                                                                                                                                                                                                                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`inverse<class_Quaternion_method_inverse>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                             |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_equal_approx<class_Quaternion_method_is_equal_approx>`\ (\ to\: :ref:`Quaternion<class_Quaternion>`\ ) |const|                                                                                                                                                                                                                                                                                   |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_finite<class_Quaternion_method_is_finite>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                         |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_normalized<class_Quaternion_method_is_normalized>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`length<class_Quaternion_method_length>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`length_squared<class_Quaternion_method_length_squared>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`log<class_Quaternion_method_log>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                                     |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`normalized<class_Quaternion_method_normalized>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`slerp<class_Quaternion_method_slerp>`\ (\ to\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                                                                                                                                   |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`slerpni<class_Quaternion_method_slerpni>`\ (\ to\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`\ ) |const|                                                                                                                                                                                                                                                               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`spherical_cubic_interpolate<class_Quaternion_method_spherical_cubic_interpolate>`\ (\ b\: :ref:`Quaternion<class_Quaternion>`, pre_a\: :ref:`Quaternion<class_Quaternion>`, post_b\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`\ ) |const|                                                                                                                             |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`spherical_cubic_interpolate_in_time<class_Quaternion_method_spherical_cubic_interpolate_in_time>`\ (\ b\: :ref:`Quaternion<class_Quaternion>`, pre_a\: :ref:`Quaternion<class_Quaternion>`, post_b\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`, b_t\: :ref:`float<class_float>`, pre_a_t\: :ref:`float<class_float>`, post_b_t\: :ref:`float<class_float>`\ ) |const| |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator !=<class_Quaternion_operator_neq_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator *<class_Quaternion_operator_mul_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ )  |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`operator *<class_Quaternion_operator_mul_Vector3>`\ (\ right\: :ref:`Vector3<class_Vector3>`\ )           |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator *<class_Quaternion_operator_mul_float>`\ (\ right\: :ref:`float<class_float>`\ )                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator *<class_Quaternion_operator_mul_int>`\ (\ right\: :ref:`int<class_int>`\ )                       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator +<class_Quaternion_operator_sum_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ )  |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator -<class_Quaternion_operator_dif_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ )  |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator /<class_Quaternion_operator_div_float>`\ (\ right\: :ref:`float<class_float>`\ )                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator /<class_Quaternion_operator_div_int>`\ (\ right\: :ref:`int<class_int>`\ )                       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ==<class_Quaternion_operator_eq_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ )  |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator []<class_Quaternion_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator unary+<class_Quaternion_operator_unplus>`\ (\ )                                                  |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator unary-<class_Quaternion_operator_unminus>`\ (\ )                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_Quaternion_constant_IDENTITY:

.. rst-class:: classref-constant

**IDENTITY** = ``Quaternion(0, 0, 0, 1)`` :ref:`🔗<class_Quaternion_constant_IDENTITY>`

Quaternion đơn vị, biểu diễn việc không xoay. Nó có cùng phép xoay với :ref:`Basis.IDENTITY<class_Basis_constant_IDENTITY>`.

Nếu một :ref:`Vector3<class_Vector3>` được xoay (nhân) với quaternion này, nó sẽ không thay đổi.

\ **Lưu ý:** Trong GDScript, hằng số này tương đương với việc tạo một :ref:`Quaternion<class_Quaternion_constructor_Quaternion>` mà không có đối số. Hằng số này có thể được dùng để làm cho mã của bạn rõ ràng hơn và nhất quán với C#.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Quaternion_property_w:

.. rst-class:: classref-property

:ref:`float<class_float>` **w** = ``1.0`` :ref:`🔗<class_Quaternion_property_w>`

Thành phần W của quaternion. Đây là phần "thực".

\ **Lưu ý:** Thông thường không nên thao tác trực tiếp với các thành phần của quaternion.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_property_x:

.. rst-class:: classref-property

:ref:`float<class_float>` **x** = ``0.0`` :ref:`🔗<class_Quaternion_property_x>`

Thành phần X của quaternion. Đây là giá trị trên trục ``i`` "ảo".

\ **Lưu ý:** Thông thường không nên thao tác trực tiếp với các thành phần của quaternion.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_property_y:

.. rst-class:: classref-property

:ref:`float<class_float>` **y** = ``0.0`` :ref:`🔗<class_Quaternion_property_y>`

Thành phần Y của quaternion. Đây là giá trị trên trục ``j`` "ảo".

\ **Lưu ý:** Thông thường không nên thao tác trực tiếp với các thành phần của quaternion.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_property_z:

.. rst-class:: classref-property

:ref:`float<class_float>` **z** = ``0.0`` :ref:`🔗<class_Quaternion_property_z>`

Thành phần Z của quaternion. Đây là giá trị trên trục ``k`` "ảo".

\ **Lưu ý:** Thông thường không nên thao tác trực tiếp với các thành phần của quaternion.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_Quaternion_constructor_Quaternion:

.. rst-class:: classref-constructor

:ref:`Quaternion<class_Quaternion>` **Quaternion**\ (\ ) :ref:`🔗<class_Quaternion_constructor_Quaternion>`

Tạo một **Quaternion** giống hệt :ref:`IDENTITY<class_Quaternion_constant_IDENTITY>`.

\ **Lưu ý:** Trong C#, hàm này tạo một **Quaternion** với tất cả các thành phần được đặt thành ``0.0``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Quaternion<class_Quaternion>` **Quaternion**\ (\ from\: :ref:`Quaternion<class_Quaternion>`\ )

Tạo một **Quaternion** dưới dạng bản sao của **Quaternion** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Quaternion<class_Quaternion>` **Quaternion**\ (\ arc_from\: :ref:`Vector3<class_Vector3>`, arc_to\: :ref:`Vector3<class_Vector3>`\ )

Tạo một **Quaternion** biểu diễn cung ngắn nhất giữa ``arc_from`` và ``arc_to``. Có thể hình dung chúng là hai điểm giao với bề mặt của một hình cầu có bán kính ``1.0``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Quaternion<class_Quaternion>` **Quaternion**\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )

Tạo một **Quaternion** biểu diễn phép xoay quanh ``axis`` theo ``angle`` đã cho, tính bằng radian. Trục phải là một vector đã chuẩn hóa.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Quaternion<class_Quaternion>` **Quaternion**\ (\ from\: :ref:`Basis<class_Basis>`\ )

Tạo một **Quaternion** từ :ref:`Basis<class_Basis>` xoay đã cho.

Hàm khởi tạo này nhanh hơn :ref:`Basis.get_rotation_quaternion()<class_Basis_method_get_rotation_quaternion>`, nhưng basis đã cho phải được *orthonormalize* (xem :ref:`Basis.orthonormalized()<class_Basis_method_orthonormalized>`). Nếu không, hàm khởi tạo sẽ thất bại và trả về :ref:`IDENTITY<class_Quaternion_constant_IDENTITY>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Quaternion<class_Quaternion>` **Quaternion**\ (\ x\: :ref:`float<class_float>`, y\: :ref:`float<class_float>`, z\: :ref:`float<class_float>`, w\: :ref:`float<class_float>`\ )

Tạo một **Quaternion** được xác định bởi các giá trị đã cho.

\ **Lưu ý:** Chỉ quaternion đã chuẩn hóa mới biểu diễn phép xoay; nếu các giá trị này chưa được chuẩn hóa, **Quaternion** mới sẽ không phải là một phép xoay hợp lệ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Quaternion_method_angle_to:

.. rst-class:: classref-method

:ref:`float<class_float>` **angle_to**\ (\ to\: :ref:`Quaternion<class_Quaternion>`\ ) |const| :ref:`🔗<class_Quaternion_method_angle_to>`

Trả về góc giữa quaternion này và ``to``. Đây là độ lớn của góc mà bạn cần xoay để đi từ quaternion này đến quaternion kia.

\ **Lưu ý:** Độ lớn của lỗi số dấu phẩy động đối với phương thức này cao bất thường, vì vậy các phương thức như ``is_zero_approx`` sẽ không hoạt động đáng tin cậy.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_dot:

.. rst-class:: classref-method

:ref:`float<class_float>` **dot**\ (\ with\: :ref:`Quaternion<class_Quaternion>`\ ) |const| :ref:`🔗<class_Quaternion_method_dot>`

Trả về tích vô hướng giữa quaternion này và ``with``.

Điều này tương đương với ``(quat.x * with.x) + (quat.y * with.y) + (quat.z * with.z) + (quat.w * with.w)``.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_exp:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **exp**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_exp>`

Trả về hàm mũ của quaternion này. Trục xoay của kết quả là trục xoay đã chuẩn hóa của quaternion này, còn góc của kết quả là độ dài phần vector của quaternion này.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_from_euler:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **from_euler**\ (\ euler\: :ref:`Vector3<class_Vector3>`\ ) |static| :ref:`🔗<class_Quaternion_method_from_euler>`

Tạo một **Quaternion** mới từ :ref:`Vector3<class_Vector3>` đã cho gồm `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__, tính bằng radian. Trong Godot, các góc Euler luôn sử dụng thứ tự nội tại. Phương thức này luôn sử dụng quy ước YXZ nội tại (:ref:`@GlobalScope.EULER_ORDER_YXZ<class_@GlobalScope_constant_EULER_ORDER_YXZ>`).

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_get_angle:

.. rst-class:: classref-method

:ref:`float<class_float>` **get_angle**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_get_angle>`

Trả về góc của phép xoay được biểu diễn bởi quaternion này.

\ **Lưu ý:** Quaternion phải được chuẩn hóa.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_get_axis:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_axis**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_get_axis>`

Trả về trục xoay của phép xoay được biểu diễn bởi quaternion này.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_get_euler:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_euler**\ (\ order\: :ref:`int<class_int>` = 2\ ) |const| :ref:`🔗<class_Quaternion_method_get_euler>`

Trả về phép xoay của quaternion này dưới dạng :ref:`Vector3<class_Vector3>` gồm `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__, tính bằng radian.

Thứ tự của từng phép xoay liên tiếp có thể được thay đổi bằng ``order`` (xem các hằng số :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>`). Trong Godot, các góc Euler luôn sử dụng thứ tự nội tại. Theo mặc định, quy ước YXZ nội tại được sử dụng (:ref:`@GlobalScope.EULER_ORDER_YXZ<class_@GlobalScope_constant_EULER_ORDER_YXZ>`): vì chúng ta đang phân rã, Z cục bộ (roll) được tính trước, sau đó đến X cục bộ (pitch), và cuối cùng là Y cục bộ (yaw). Khi sử dụng phương thức ngược lại :ref:`from_euler()<class_Quaternion_method_from_euler>` để kết hợp một phép xoay, thứ tự này bị đảo ngược.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_inverse:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **inverse**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_inverse>`

Trả về phiên bản nghịch đảo của quaternion này, đảo dấu mọi thành phần ngoại trừ :ref:`w<class_Quaternion_property_w>`.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_is_equal_approx:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_equal_approx**\ (\ to\: :ref:`Quaternion<class_Quaternion>`\ ) |const| :ref:`🔗<class_Quaternion_method_is_equal_approx>`

Trả về ``true`` nếu quaternion này và ``to`` xấp xỉ bằng nhau, bằng cách gọi :ref:`@GlobalScope.is_equal_approx()<class_@GlobalScope_method_is_equal_approx>` trên từng thành phần.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_is_finite:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_finite**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_is_finite>`

Trả về ``true`` nếu quaternion này là hữu hạn, bằng cách gọi :ref:`@GlobalScope.is_finite()<class_@GlobalScope_method_is_finite>` trên từng thành phần.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_is_normalized:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_normalized**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_is_normalized>`

Trả về ``true`` nếu quaternion này đã được chuẩn hóa. Xem thêm :ref:`normalized()<class_Quaternion_method_normalized>`.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_length:

.. rst-class:: classref-method

:ref:`float<class_float>` **length**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_length>`

Trả về độ dài của quaternion này, còn được gọi là độ lớn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_length_squared:

.. rst-class:: classref-method

:ref:`float<class_float>` **length_squared**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_length_squared>`

Trả về bình phương độ dài của quaternion này.

\ **Lưu ý:** Phương thức này nhanh hơn :ref:`length()<class_Quaternion_method_length>`, vì vậy hãy ưu tiên sử dụng nó nếu bạn chỉ cần so sánh độ dài của các quaternion.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_log:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **log**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_log>`

Trả về logarithm của quaternion này. Nhân trục xoay của quaternion này với góc xoay của nó, rồi lưu kết quả vào phần vector của quaternion được trả về (:ref:`x<class_Quaternion_property_x>`, :ref:`y<class_Quaternion_property_y>` và :ref:`z<class_Quaternion_property_z>`). Phần thực (:ref:`w<class_Quaternion_property_w>`) của quaternion được trả về luôn là ``0.0``.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_normalized:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **normalized**\ (\ ) |const| :ref:`🔗<class_Quaternion_method_normalized>`

Trả về một bản sao của quaternion này, được chuẩn hóa để độ dài của nó là ``1.0``. Xem thêm :ref:`is_normalized()<class_Quaternion_method_is_normalized>`.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_slerp:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **slerp**\ (\ to\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Quaternion_method_slerp>`

Thực hiện phép nội suy tuyến tính cầu với quaternion ``to``, sử dụng ``weight`` và trả về kết quả. Cả quaternion này và ``to`` đều phải được chuẩn hóa.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_slerpni:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **slerpni**\ (\ to\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Quaternion_method_slerpni>`

Thực hiện phép nội suy tuyến tính cầu với quaternion ``to``, sử dụng ``weight`` và trả về kết quả. Không giống :ref:`slerp()<class_Quaternion_method_slerp>`, phương thức này không kiểm tra xem đường đi của phép xoay có nhỏ hơn 90 độ hay không. Cả quaternion này và ``to`` đều phải được chuẩn hóa.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_spherical_cubic_interpolate:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **spherical_cubic_interpolate**\ (\ b\: :ref:`Quaternion<class_Quaternion>`, pre_a\: :ref:`Quaternion<class_Quaternion>`, post_b\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Quaternion_method_spherical_cubic_interpolate>`

Thực hiện phép nội suy cubic cầu giữa các quaternion ``pre_a``, vector này, ``b`` và ``post_b`` theo lượng ``weight`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_method_spherical_cubic_interpolate_in_time:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **spherical_cubic_interpolate_in_time**\ (\ b\: :ref:`Quaternion<class_Quaternion>`, pre_a\: :ref:`Quaternion<class_Quaternion>`, post_b\: :ref:`Quaternion<class_Quaternion>`, weight\: :ref:`float<class_float>`, b_t\: :ref:`float<class_float>`, pre_a_t\: :ref:`float<class_float>`, post_b_t\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Quaternion_method_spherical_cubic_interpolate_in_time>`

Thực hiện phép nội suy cubic cầu giữa các quaternion ``pre_a``, vector này, ``b`` và ``post_b`` theo lượng ``weight`` đã cho.

Phương thức này có thể thực hiện phép nội suy mượt hơn :ref:`spherical_cubic_interpolate()<class_Quaternion_method_spherical_cubic_interpolate>` nhờ các giá trị thời gian.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_Quaternion_operator_neq_Quaternion:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_Quaternion_operator_neq_Quaternion>`

Trả về ``true`` nếu các thành phần của hai quaternion không hoàn toàn bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác của số dấu phẩy động, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_Quaternion_method_is_equal_approx>` thay thế vì nó đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_mul_Quaternion:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator ***\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_Quaternion_operator_mul_Quaternion>`

Kết hợp (nhân) hai quaternion. Phép này xoay quaternion ``right`` (con) bằng quaternion này (cha).

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_mul_Vector3:

.. rst-class:: classref-operator

:ref:`Vector3<class_Vector3>` **operator ***\ (\ right\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Quaternion_operator_mul_Vector3>`

Xoay (nhân) vector ``right`` bằng quaternion này, trả về một :ref:`Vector3<class_Vector3>`.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_mul_float:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator ***\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Quaternion_operator_mul_float>`

Nhân từng thành phần của **Quaternion** với giá trị :ref:`float<class_float>` ở bên phải.

Phép toán này không có ý nghĩa khi sử dụng riêng lẻ, nhưng có thể được dùng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_mul_int:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator ***\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Quaternion_operator_mul_int>`

Nhân từng thành phần của **Quaternion** với giá trị :ref:`int<class_int>` ở bên phải.

Phép toán này không có ý nghĩa khi sử dụng riêng lẻ, nhưng có thể được dùng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_sum_Quaternion:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator +**\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_Quaternion_operator_sum_Quaternion>`

Cộng từng thành phần của **Quaternion** bên trái với **Quaternion** bên phải.

Phép toán này không có ý nghĩa khi sử dụng riêng lẻ, nhưng có thể được dùng như một phần của biểu thức lớn hơn, chẳng hạn như để xấp xỉ một phép xoay trung gian giữa hai phép xoay gần nhau.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_dif_Quaternion:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator -**\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_Quaternion_operator_dif_Quaternion>`

Trừ từng thành phần của **Quaternion** bên trái cho **Quaternion** bên phải.

Phép toán này không có ý nghĩa khi sử dụng riêng lẻ, nhưng có thể được dùng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_div_float:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator /**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Quaternion_operator_div_float>`

Chia từng thành phần của **Quaternion** cho giá trị :ref:`float<class_float>` ở bên phải.

Phép toán này không có ý nghĩa khi sử dụng riêng lẻ, nhưng có thể được dùng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_div_int:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator /**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Quaternion_operator_div_int>`

Chia từng thành phần của **Quaternion** cho giá trị :ref:`int<class_int>` ở bên phải.

Phép toán này không có ý nghĩa khi sử dụng riêng lẻ, nhưng có thể được dùng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_eq_Quaternion:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_Quaternion_operator_eq_Quaternion>`

Trả về ``true`` nếu các thành phần của hai quaternion hoàn toàn bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác của số dấu phẩy động, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_Quaternion_method_is_equal_approx>` thay thế vì nó đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_idx_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Quaternion_operator_idx_int>`

Truy cập từng thành phần của quaternion này bằng chỉ mục của chúng.

Chỉ mục ``0`` tương ứng với :ref:`x<class_Quaternion_property_x>`, chỉ mục ``1`` tương ứng với :ref:`y<class_Quaternion_property_y>`, chỉ mục ``2`` tương ứng với :ref:`z<class_Quaternion_property_z>`, và chỉ mục ``3`` tương ứng với :ref:`w<class_Quaternion_property_w>`.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_unplus:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator unary+**\ (\ ) :ref:`🔗<class_Quaternion_operator_unplus>`

Trả về cùng một giá trị như khi ``+`` không tồn tại. Unary ``+`` không thực hiện thao tác gì, nhưng đôi khi có thể giúp code của bạn dễ đọc hơn.

.. rst-class:: classref-item-separator

----

.. _class_Quaternion_operator_unminus:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator unary-**\ (\ ) :ref:`🔗<class_Quaternion_operator_unminus>`

Trả về giá trị âm của **Quaternion**. Điều này tương đương với việc nhân tất cả các thành phần với ``-1``. Phép toán này cho kết quả là một quaternion biểu diễn cùng một phép xoay.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
