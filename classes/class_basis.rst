:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/Basis.xml.

.. _class_Basis:

Basis
=====

Một ma trận 3×3 dùng để biểu diễn phép xoay và tỷ lệ 3D.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu tích hợp **Basis** :ref:`Variant<class_Variant>` là một `matrix <https://en.wikipedia.org/wiki/Matrix_(mathematics)>`__ 3×3 dùng để biểu diễn phép xoay, tỷ lệ và biến dạng (shear) 3D. Nó thường được sử dụng bên trong một :ref:`Transform3D<class_Transform3D>`.

Một **Basis** được cấu thành từ 3 vector trục, mỗi vector biểu diễn một cột của ma trận: :ref:`x<class_Basis_property_x>`, :ref:`y<class_Basis_property_y>` và :ref:`z<class_Basis_property_z>`. Độ dài của mỗi trục (:ref:`Vector3.length()<class_Vector3_method_length>`) ảnh hưởng đến tỷ lệ của basis, còn hướng của tất cả các trục ảnh hưởng đến phép xoay. Thông thường, các trục này vuông góc với nhau. Tuy nhiên, khi bạn xoay riêng lẻ bất kỳ trục nào, basis sẽ bị biến dạng. Việc áp dụng một basis bị biến dạng cho mô hình 3D sẽ khiến mô hình trông méo mó.

Một **Basis** là:

- **Orthogonal** nếu các trục của nó vuông góc với nhau.

- **Normalized** nếu độ dài của mọi trục là ``1.0``.

- **Uniform** nếu tất cả các trục có cùng độ dài (xem :ref:`get_scale()<class_Basis_method_get_scale>`).

- **Orthonormal** nếu vừa orthogonal vừa normalized, cho phép nó chỉ biểu diễn các phép xoay (xem :ref:`orthonormalized()<class_Basis_method_orthonormalized>`).

- **Conformal** nếu vừa orthogonal vừa uniform, đảm bảo nó không bị biến dạng.

Để xem phần giới thiệu tổng quan, hãy xem tutorial :doc:`Matrices and transforms <../tutorials/math/matrices_and_transforms>`.

\ **Lưu ý:** Godot sử dụng `right-handed coordinate system <https://en.wikipedia.org/wiki/Right-hand_rule>`__, một tiêu chuẩn phổ biến. Đối với hướng, quy ước cho các kiểu tích hợp như :ref:`Camera3D<class_Camera3D>` là -Z hướng về phía trước (+X là bên phải, +Y là hướng lên và +Z là phía sau). Các đối tượng khác có thể sử dụng quy ước hướng khác. Để biết thêm thông tin, hãy xem tutorial `3D asset direction conventions <../tutorials/assets_pipeline/importing_3d_scenes/model_export_considerations.html#d-asset-direction-conventions>`__.

\ **Lưu ý:** Các ma trận basis được cung cấp theo thứ tự `column-major <https://www.mindcontrol.org/~hplus/graphics/matrix-layout.html>`__, giống với OpenGL. Tuy nhiên, chúng được lưu trữ nội bộ theo thứ tự hàng (row-major), giống với DirectX.

\ **Lưu ý:** Trong ngữ cảnh boolean, một basis sẽ được đánh giá là ``false`` nếu nó bằng :ref:`IDENTITY<class_Basis_constant_IDENTITY>`. Nếu không, basis sẽ luôn được đánh giá là ``true``.

.. note::

	Có những khác biệt đáng chú ý khi sử dụng API này với C#. Xem :ref:`doc_c_sharp_differences` để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Math documentation index <../tutorials/math/index>`

- :doc:`Matrices and transforms <../tutorials/math/matrices_and_transforms>`

- :doc:`Using 3D transforms <../tutorials/3d/using_transforms>`

- `Matrix Transform Demo <https://godotengine.org/asset-library/asset/2787>`__

- `3D Platformer Demo <https://godotengine.org/asset-library/asset/2748>`__

- `3D Voxel Demo <https://godotengine.org/asset-library/asset/2755>`__

- `2.5D Game Demo <https://godotengine.org/asset-library/asset/2783>`__

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------+----------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`x<class_Basis_property_x>` | ``Vector3(1, 0, 0)`` |
   +-------------------------------+----------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`y<class_Basis_property_y>` | ``Vector3(0, 1, 0)`` |
   +-------------------------------+----------------------------------+----------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`z<class_Basis_property_z>` | ``Vector3(0, 0, 1)`` |
   +-------------------------------+----------------------------------+----------------------+

.. rst-class:: classref-reftable-group

Constructor
-----------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>` | :ref:`Basis<class_Basis_constructor_Basis>`\ (\ )                                                                                                                         |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>` | :ref:`Basis<class_Basis_constructor_Basis>`\ (\ from\: :ref:`Basis<class_Basis>`\ )                                                                                       |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>` | :ref:`Basis<class_Basis_constructor_Basis>`\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )                                                |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>` | :ref:`Basis<class_Basis_constructor_Basis>`\ (\ from\: :ref:`Quaternion<class_Quaternion>`\ )                                                                             |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>` | :ref:`Basis<class_Basis_constructor_Basis>`\ (\ x_axis\: :ref:`Vector3<class_Vector3>`, y_axis\: :ref:`Vector3<class_Vector3>`, z_axis\: :ref:`Vector3<class_Vector3>`\ ) |
   +---------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`determinant<class_Basis_method_determinant>`\ (\ ) |const|                                                                                                                                                  |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`from_euler<class_Basis_method_from_euler>`\ (\ euler\: :ref:`Vector3<class_Vector3>`, order\: :ref:`int<class_int>` = 2\ ) |static|                                                                         |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`from_scale<class_Basis_method_from_scale>`\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) |static|                                                                                                            |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`get_euler<class_Basis_method_get_euler>`\ (\ order\: :ref:`int<class_int>` = 2\ ) |const|                                                                                                                   |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`get_rotation_quaternion<class_Basis_method_get_rotation_quaternion>`\ (\ ) |const|                                                                                                                          |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`get_scale<class_Basis_method_get_scale>`\ (\ ) |const|                                                                                                                                                      |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`inverse<class_Basis_method_inverse>`\ (\ ) |const|                                                                                                                                                          |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_conformal<class_Basis_method_is_conformal>`\ (\ ) |const|                                                                                                                                                |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_equal_approx<class_Basis_method_is_equal_approx>`\ (\ b\: :ref:`Basis<class_Basis>`\ ) |const|                                                                                                           |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_finite<class_Basis_method_is_finite>`\ (\ ) |const|                                                                                                                                                      |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`is_orthonormal<class_Basis_method_is_orthonormal>`\ (\ ) |const|                                                                                                                                            |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`looking_at<class_Basis_method_looking_at>`\ (\ target\: :ref:`Vector3<class_Vector3>`, up\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0), use_model_front\: :ref:`bool<class_bool>` = false\ ) |static| |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`orthonormalized<class_Basis_method_orthonormalized>`\ (\ ) |const|                                                                                                                                          |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`rotated<class_Basis_method_rotated>`\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ ) |const|                                                                                 |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`scaled<class_Basis_method_scaled>`\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                     |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`scaled_local<class_Basis_method_scaled_local>`\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                         |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`slerp<class_Basis_method_slerp>`\ (\ to\: :ref:`Basis<class_Basis>`, weight\: :ref:`float<class_float>`\ ) |const|                                                                                          |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`tdotx<class_Basis_method_tdotx>`\ (\ with\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                        |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`tdoty<class_Basis_method_tdoty>`\ (\ with\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                        |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`tdotz<class_Basis_method_tdotz>`\ (\ with\: :ref:`Vector3<class_Vector3>`\ ) |const|                                                                                                                        |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`           | :ref:`transposed<class_Basis_method_transposed>`\ (\ ) |const|                                                                                                                                                    |
   +-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Toán tử
-------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator !=<class_Basis_operator_neq_Basis>`\ (\ right\: :ref:`Basis<class_Basis>`\ )      |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`     | :ref:`operator *<class_Basis_operator_mul_Basis>`\ (\ right\: :ref:`Basis<class_Basis>`\ )       |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`operator *<class_Basis_operator_mul_Vector3>`\ (\ right\: :ref:`Vector3<class_Vector3>`\ ) |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`     | :ref:`operator *<class_Basis_operator_mul_float>`\ (\ right\: :ref:`float<class_float>`\ )       |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`     | :ref:`operator *<class_Basis_operator_mul_int>`\ (\ right\: :ref:`int<class_int>`\ )             |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`     | :ref:`operator /<class_Basis_operator_div_float>`\ (\ right\: :ref:`float<class_float>`\ )       |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Basis<class_Basis>`     | :ref:`operator /<class_Basis_operator_div_int>`\ (\ right\: :ref:`int<class_int>`\ )             |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | :ref:`operator ==<class_Basis_operator_eq_Basis>`\ (\ right\: :ref:`Basis<class_Basis>`\ )       |
   +-------------------------------+--------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>` | :ref:`operator []<class_Basis_operator_idx_int>`\ (\ index\: :ref:`int<class_int>`\ )            |
   +-------------------------------+--------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Hằng số
-------

.. _class_Basis_constant_IDENTITY:

.. rst-class:: classref-constant

**IDENTITY** = ``Basis(1, 0, 0, 0, 1, 0, 0, 0, 1)`` :ref:`🔗<class_Basis_constant_IDENTITY>`

**Basis** đơn vị. Đây là một basis orthonormal không có phép xoay, không có biến dạng và có tỷ lệ là :ref:`Vector3.ONE<class_Vector3_constant_ONE>`. Điều này cũng có nghĩa là:

- :ref:`x<class_Basis_property_x>` hướng sang phải (:ref:`Vector3.RIGHT<class_Vector3_constant_RIGHT>`);

- :ref:`y<class_Basis_property_y>` hướng lên (:ref:`Vector3.UP<class_Vector3_constant_UP>`);

- :ref:`z<class_Basis_property_z>` hướng ra sau (:ref:`Vector3.BACK<class_Vector3_constant_BACK>`).

::

    var basis = Basis.IDENTITY
    print("| X | Y | Z")
    print("| %.f | %.f | %.f" % [basis.x.x, basis.y.x, basis.z.x])
    print("| %.f | %.f | %.f" % [basis.x.y, basis.y.y, basis.z.y])
    print("| %.f | %.f | %.f" % [basis.x.z, basis.y.z, basis.z.z])
    # In ra:
    # | X | Y | Z
    # | 1 | 0 | 0
    # | 0 | 1 | 0
    # | 0 | 0 | 1

Nếu một :ref:`Vector3<class_Vector3>` hoặc một **Basis** khác được biến đổi (nhân) với hằng số này, sẽ không có phép biến đổi nào xảy ra.

\ **Lưu ý:** Trong GDScript, hằng số này tương đương với việc tạo một :ref:`Basis<class_Basis_constructor_Basis>` không có đối số. Nó có thể được dùng để làm cho mã của bạn rõ ràng hơn và nhất quán với C#.

.. _class_Basis_constant_FLIP_X:

.. rst-class:: classref-constant

**FLIP_X** = ``Basis(-1, 0, 0, 0, 1, 0, 0, 0, 1)`` :ref:`🔗<class_Basis_constant_FLIP_X>`

Khi bất kỳ basis nào được nhân với :ref:`FLIP_X<class_Basis_constant_FLIP_X>`, nó sẽ đổi dấu tất cả các thành phần của trục :ref:`x<class_Basis_property_x>` (cột X).

Khi :ref:`FLIP_X<class_Basis_constant_FLIP_X>` được nhân với bất kỳ basis nào, nó sẽ đổi dấu thành phần :ref:`Vector3.x<class_Vector3_property_x>` của tất cả các trục (hàng X).

.. _class_Basis_constant_FLIP_Y:

.. rst-class:: classref-constant

**FLIP_Y** = ``Basis(1, 0, 0, 0, -1, 0, 0, 0, 1)`` :ref:`🔗<class_Basis_constant_FLIP_Y>`

Khi bất kỳ basis nào được nhân với :ref:`FLIP_Y<class_Basis_constant_FLIP_Y>`, nó sẽ đổi dấu tất cả các thành phần của trục :ref:`y<class_Basis_property_y>` (cột Y).

Khi :ref:`FLIP_Y<class_Basis_constant_FLIP_Y>` được nhân với bất kỳ basis nào, nó sẽ đổi dấu thành phần :ref:`Vector3.y<class_Vector3_property_y>` của tất cả các trục (hàng Y).

.. _class_Basis_constant_FLIP_Z:

.. rst-class:: classref-constant

**FLIP_Z** = ``Basis(1, 0, 0, 0, 1, 0, 0, 0, -1)`` :ref:`🔗<class_Basis_constant_FLIP_Z>`

Khi bất kỳ basis nào được nhân với :ref:`FLIP_Z<class_Basis_constant_FLIP_Z>`, nó sẽ đổi dấu tất cả các thành phần của trục :ref:`z<class_Basis_property_z>` (cột Z).

Khi :ref:`FLIP_Z<class_Basis_constant_FLIP_Z>` được nhân với bất kỳ basis nào, nó sẽ đổi dấu thành phần :ref:`Vector3.z<class_Vector3_property_z>` của tất cả các trục (hàng Z).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_Basis_property_x:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **x** = ``Vector3(1, 0, 0)`` :ref:`🔗<class_Basis_property_x>`

Trục X của basis và cột ``0`` của ma trận.

Trên basis đơn vị, vector này hướng sang phải (:ref:`Vector3.RIGHT<class_Vector3_constant_RIGHT>`).

.. rst-class:: classref-item-separator

----

.. _class_Basis_property_y:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **y** = ``Vector3(0, 1, 0)`` :ref:`🔗<class_Basis_property_y>`

Trục Y của basis và cột ``1`` của ma trận.

Trên basis đơn vị, vector này hướng lên (:ref:`Vector3.UP<class_Vector3_constant_UP>`).

.. rst-class:: classref-item-separator

----

.. _class_Basis_property_z:

.. rst-class:: classref-property

:ref:`Vector3<class_Vector3>` **z** = ``Vector3(0, 0, 1)`` :ref:`🔗<class_Basis_property_z>`

Trục Z của basis và cột ``2`` của ma trận.

Trên basis đơn vị, vector này hướng ra sau (:ref:`Vector3.BACK<class_Vector3_constant_BACK>`).

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả constructor
-----------------

.. _class_Basis_constructor_Basis:

.. rst-class:: classref-constructor

:ref:`Basis<class_Basis>` **Basis**\ (\ ) :ref:`🔗<class_Basis_constructor_Basis>`

Tạo một **Basis** giống hệt :ref:`IDENTITY<class_Basis_constant_IDENTITY>`.

\ **Lưu ý:** Trong C#, lệnh này tạo một **Basis** với tất cả các thành phần được đặt thành :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Basis<class_Basis>` **Basis**\ (\ from\: :ref:`Basis<class_Basis>`\ )

Tạo một **Basis** là bản sao của **Basis** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Basis<class_Basis>` **Basis**\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ )

Tạo một **Basis** chỉ biểu diễn phép xoay, xoay quanh ``axis`` theo ``angle`` đã cho, tính bằng radian. Trục phải là một vector normalized.

\ **Lưu ý:** Điều này tương đương với việc sử dụng :ref:`rotated()<class_Basis_method_rotated>` trên basis :ref:`IDENTITY<class_Basis_constant_IDENTITY>`. Khi có nhiều hơn một góc, hãy cân nhắc sử dụng :ref:`from_euler()<class_Basis_method_from_euler>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Basis<class_Basis>` **Basis**\ (\ from\: :ref:`Quaternion<class_Quaternion>`\ )

Tạo một **Basis** chỉ biểu diễn phép xoay từ :ref:`Quaternion<class_Quaternion>` đã cho.

\ **Lưu ý:** Quaternion *chỉ* lưu phép xoay, không lưu tỷ lệ. Vì vậy, việc chuyển đổi từ **Basis** sang :ref:`Quaternion<class_Quaternion>` không phải lúc nào cũng có thể đảo ngược.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`Basis<class_Basis>` **Basis**\ (\ x_axis\: :ref:`Vector3<class_Vector3>`, y_axis\: :ref:`Vector3<class_Vector3>`, z_axis\: :ref:`Vector3<class_Vector3>`\ )

Tạo một **Basis** từ 3 vector trục. Đây là các cột của ma trận basis.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_Basis_method_determinant:

.. rst-class:: classref-method

:ref:`float<class_float>` **determinant**\ (\ ) |const| :ref:`🔗<class_Basis_method_determinant>`

Trả về `determinant <https://en.wikipedia.org/wiki/Determinant>`__ của ma trận basis này. Trong toán nâng cao, số này có thể được dùng để xác định một số thuộc tính:

- Nếu định thức chính xác bằng ``0.0``, basis không khả nghịch (xem :ref:`inverse()<class_Basis_method_inverse>`).

- Nếu định thức là một số âm, basis biểu diễn một tỷ lệ âm.

\ **Lưu ý:** Nếu tỷ lệ của basis giống nhau trên mọi trục, định thức luôn bằng tỷ lệ đó lũy thừa 3.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_from_euler:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **from_euler**\ (\ euler\: :ref:`Vector3<class_Vector3>`, order\: :ref:`int<class_int>` = 2\ ) |static| :ref:`🔗<class_Basis_method_from_euler>`

Tạo một **Basis** mới chỉ biểu diễn phép xoay từ :ref:`Vector3<class_Vector3>` đã cho của `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__, tính bằng radian.

- :ref:`Vector3.x<class_Vector3_property_x>` phải chứa góc quanh trục :ref:`x<class_Basis_property_x>` (pitch);

- :ref:`Vector3.y<class_Vector3_property_y>` phải chứa góc quanh trục :ref:`y<class_Basis_property_y>` (yaw);

- :ref:`Vector3.z<class_Vector3_property_z>` phải chứa góc quanh trục :ref:`z<class_Basis_property_z>` (roll).


.. tabs::

 .. code-tab:: gdscript

    # Tạo một Basis có trục z hướng xuống.
    var my_basis = Basis.from_euler(Vector3(TAU / 4, 0, 0))

    print(my_basis.z) # In ra (0.0, -1.0, 0.0)

 .. code-tab:: csharp

    // Tạo một Basis có trục z hướng xuống.
    var myBasis = Basis.FromEuler(new Vector3(Mathf.Tau / 4.0f, 0.0f, 0.0f));

    GD.Print(myBasis.Z); // In ra (0, -1, 0)



Có thể thay đổi thứ tự của từng phép xoay liên tiếp bằng ``order`` (xem các hằng số :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>`). Trong Godot, các góc Euler luôn sử dụng thứ tự nội tại (intrinsic order). Theo mặc định, quy ước YXZ nội tại được sử dụng (:ref:`@GlobalScope.EULER_ORDER_YXZ<class_@GlobalScope_constant_EULER_ORDER_YXZ>`): basis trước tiên xoay quanh trục Y cục bộ (yaw), sau đó là X cục bộ (pitch) và cuối cùng là Z cục bộ (roll). Khi sử dụng phương thức ngược lại :ref:`get_euler()<class_Basis_method_get_euler>` để phân rã một phép xoay, thứ tự này sẽ bị đảo ngược.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_from_scale:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **from_scale**\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) |static| :ref:`🔗<class_Basis_method_from_scale>`

Tạo một **Basis** mới chỉ biểu diễn tỷ lệ, không có phép xoay hoặc biến dạng, từ vector ``scale`` đã cho.


.. tabs::

 .. code-tab:: gdscript

    var my_basis = Basis.from_scale(Vector3(2, 4, 8))

    print(my_basis.x) # In ra (2.0, 0.0, 0.0)
    print(my_basis.y) # In ra (0.0, 4.0, 0.0)
    print(my_basis.z) # In ra (0.0, 0.0, 8.0)

 .. code-tab:: csharp

    var myBasis = Basis.FromScale(new Vector3(2.0f, 4.0f, 8.0f));

    GD.Print(myBasis.X); // In ra (2, 0, 0)
    GD.Print(myBasis.Y); // In ra (0, 4, 0)
    GD.Print(myBasis.Z); // In ra (0, 0, 8)



\ **Lưu ý:** Trong đại số tuyến tính, ma trận của basis này còn được gọi là `diagonal matrix <https://en.wikipedia.org/wiki/Diagonal_matrix>`__.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_get_euler:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_euler**\ (\ order\: :ref:`int<class_int>` = 2\ ) |const| :ref:`🔗<class_Basis_method_get_euler>`

Trả về phép xoay của basis này dưới dạng :ref:`Vector3<class_Vector3>` của `Euler angles <https://en.wikipedia.org/wiki/Euler_angles>`__, tính bằng radian. Đối với giá trị trả về:

- :ref:`Vector3.x<class_Vector3_property_x>` chứa góc quanh trục :ref:`x<class_Basis_property_x>` (pitch);

- :ref:`Vector3.y<class_Vector3_property_y>` chứa góc quanh trục :ref:`y<class_Basis_property_y>` (yaw);

- :ref:`Vector3.z<class_Vector3_property_z>` chứa góc quanh trục :ref:`z<class_Basis_property_z>` (roll).

Có thể thay đổi thứ tự của từng phép xoay liên tiếp bằng ``order`` (xem các hằng số :ref:`EulerOrder<enum_@GlobalScope_EulerOrder>`). Trong Godot, các góc Euler luôn sử dụng thứ tự nội tại. Theo mặc định, quy ước YXZ nội tại được sử dụng (:ref:`@GlobalScope.EULER_ORDER_YXZ<class_@GlobalScope_constant_EULER_ORDER_YXZ>`): vì chúng ta đang phân rã, Z cục bộ (roll) được tính trước, sau đó là X cục bộ (pitch) và cuối cùng là Y cục bộ (yaw). Khi sử dụng phương thức ngược lại :ref:`from_euler()<class_Basis_method_from_euler>` để hợp thành một phép xoay, thứ tự này sẽ bị đảo ngược.

\ **Lưu ý:** Để phương thức này trả về chính xác, basis cần phải là *orthonormal* (xem :ref:`orthonormalized()<class_Basis_method_orthonormalized>`).

\ **Lưu ý:** Các góc Euler trực quan hơn nhiều nhưng không phù hợp với toán học 3D. Vì vậy, hãy cân nhắc sử dụng phương thức :ref:`get_rotation_quaternion()<class_Basis_method_get_rotation_quaternion>` thay thế, phương thức này trả về một :ref:`Quaternion<class_Quaternion>`.

\ **Lưu ý:** Trong dock Inspector, phép quay của một basis thường được hiển thị dưới dạng các góc Euler (theo độ), tương tự như thuộc tính :ref:`Node3D.rotation<class_Node3D_property_rotation>`.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_get_rotation_quaternion:

.. rst-class:: classref-method

:ref:`Quaternion<class_Quaternion>` **get_rotation_quaternion**\ (\ ) |const| :ref:`🔗<class_Basis_method_get_rotation_quaternion>`

Trả về phép quay của basis này dưới dạng một :ref:`Quaternion<class_Quaternion>`.

\ **Lưu ý:** Quaternion phù hợp với toán học 3D hơn nhiều nhưng kém trực quan hơn. Đối với giao diện người dùng, hãy cân nhắc sử dụng phương thức :ref:`get_euler()<class_Basis_method_get_euler>`, phương thức này trả về các góc Euler.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_get_scale:

.. rst-class:: classref-method

:ref:`Vector3<class_Vector3>` **get_scale**\ (\ ) |const| :ref:`🔗<class_Basis_method_get_scale>`

Trả về độ dài của mỗi trục của basis này dưới dạng một :ref:`Vector3<class_Vector3>`. Nếu basis không bị shear, giá trị này là hệ số scale. Giá trị này không bị ảnh hưởng bởi phép quay.


.. tabs::

 .. code-tab:: gdscript

    var my_basis = Basis(
        Vector3(2, 0, 0),
        Vector3(0, 4, 0),
        Vector3(0, 0, 8)
    )
    # Xoay Basis theo bất kỳ cách nào cũng giữ nguyên scale của nó.
    my_basis = my_basis.rotated(Vector3.UP, TAU / 2)
    my_basis = my_basis.rotated(Vector3.RIGHT, TAU / 4)

    print(my_basis.get_scale()) # In ra (2.0, 4.0, 8.0)

 .. code-tab:: csharp

    var myBasis = new Basis(
        Vector3(2.0f, 0.0f, 0.0f),
        Vector3(0.0f, 4.0f, 0.0f),
        Vector3(0.0f, 0.0f, 8.0f)
    );
    // Xoay Basis theo bất kỳ cách nào cũng giữ nguyên scale của nó.
    myBasis = myBasis.Rotated(Vector3.Up, Mathf.Tau / 2.0f);
    myBasis = myBasis.Rotated(Vector3.Right, Mathf.Tau / 4.0f);

    GD.Print(myBasis.Scale); // In ra (2, 4, 8)



\ **Lưu ý:** Nếu giá trị được trả về bởi :ref:`determinant()<class_Basis_method_determinant>` là số âm, scale cũng là số âm.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_inverse:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **inverse**\ (\ ) |const| :ref:`🔗<class_Basis_method_inverse>`

Trả về `inverse of this basis's matrix <https://en.wikipedia.org/wiki/Invertible_matrix>`__.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_is_conformal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_conformal**\ (\ ) |const| :ref:`🔗<class_Basis_method_is_conformal>`

Trả về ``true`` nếu basis này là conformal. Một basis conformal vừa *orthogonal* (các trục vuông góc với nhau) vừa *uniform* (các trục có cùng độ dài). Phương thức này đặc biệt hữu ích trong các phép tính vật lý.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_is_equal_approx:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_equal_approx**\ (\ b\: :ref:`Basis<class_Basis>`\ ) |const| :ref:`🔗<class_Basis_method_is_equal_approx>`

Trả về ``true`` nếu basis này và ``b`` gần bằng nhau, bằng cách gọi :ref:`@GlobalScope.is_equal_approx()<class_@GlobalScope_method_is_equal_approx>` trên tất cả các thành phần vector.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_is_finite:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_finite**\ (\ ) |const| :ref:`🔗<class_Basis_method_is_finite>`

Trả về ``true`` nếu basis này là hữu hạn, bằng cách gọi :ref:`@GlobalScope.is_finite()<class_@GlobalScope_method_is_finite>` trên tất cả các thành phần vector.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_is_orthonormal:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_orthonormal**\ (\ ) |const| :ref:`🔗<class_Basis_method_is_orthonormal>`

Trả về ``true`` nếu basis này là orthonormal. Một basis orthonormal vừa *orthogonal* (các trục vuông góc với nhau) vừa *normalized* (độ dài của mỗi trục là ``1.0``). Phương thức này đặc biệt hữu ích trong các phép tính vật lý.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_looking_at:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **looking_at**\ (\ target\: :ref:`Vector3<class_Vector3>`, up\: :ref:`Vector3<class_Vector3>` = Vector3(0, 1, 0), use_model_front\: :ref:`bool<class_bool>` = false\ ) |static| :ref:`🔗<class_Basis_method_looking_at>`

Tạo một **Basis** mới với phép quay sao cho trục forward (-Z) hướng về vị trí ``target``.

Theo mặc định, trục -Z (forward của camera) được xem là forward (ngụ ý +X là right). Nếu ``use_model_front`` là ``true``, trục +Z (front của asset) được xem là forward (ngụ ý +X là left) và hướng về vị trí ``target``.

Trục up (+Y) hướng gần nhất có thể về vector ``up`` trong khi vẫn vuông góc với trục forward. Basis được trả về là orthonormalized (xem :ref:`orthonormalized()<class_Basis_method_orthonormalized>`).

``target`` và ``up`` không được là :ref:`Vector3.ZERO<class_Vector3_constant_ZERO>`, đồng thời không nên colinear để tránh việc xoay ngoài ý muốn quanh trục Z cục bộ.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_orthonormalized:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **orthonormalized**\ (\ ) |const| :ref:`🔗<class_Basis_method_orthonormalized>`

Trả về phiên bản orthonormalized của basis này. Một basis orthonormal vừa *orthogonal* (các trục vuông góc với nhau) vừa *normalized* (các trục có độ dài ``1.0``), điều này cũng có nghĩa là nó chỉ có thể biểu diễn một phép quay.

Việc gọi phương thức này thường hữu ích để tránh lỗi làm tròn trên một basis đang xoay:


.. tabs::

 .. code-tab:: gdscript

    # Xoay Node3D này mỗi frame.
    func _process(delta):
        basis = basis.rotated(Vector3.UP, TAU * delta)
        basis = basis.rotated(Vector3.RIGHT, TAU * delta)
        basis = basis.orthonormalized()

 .. code-tab:: csharp

    // Xoay Node3D này mỗi frame.
    public override void _Process(double delta)
    {
        Basis = Basis.Rotated(Vector3.Up, Mathf.Tau * (float)delta)
                .Rotated(Vector3.Right, Mathf.Tau * (float)delta)
                .Orthonormalized();
    }



.. rst-class:: classref-item-separator

----

.. _class_Basis_method_rotated:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **rotated**\ (\ axis\: :ref:`Vector3<class_Vector3>`, angle\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Basis_method_rotated>`

Trả về một bản sao của basis này được xoay quanh ``axis`` đã cho theo ``angle`` đã cho (tính bằng radian).

``axis`` phải là một vector normalized (xem :ref:`Vector3.normalized()<class_Vector3_method_normalized>`). Nếu ``angle`` là số dương, basis sẽ được xoay ngược chiều kim đồng hồ quanh trục đó.


.. tabs::

 .. code-tab:: gdscript

    var my_basis = Basis.IDENTITY
    var angle = TAU / 2

    my_basis = my_basis.rotated(Vector3.UP, angle)    # Xoay quanh trục up (yaw).
    my_basis = my_basis.rotated(Vector3.RIGHT, angle) # Xoay quanh trục right (pitch).
    my_basis = my_basis.rotated(Vector3.BACK, angle)  # Xoay quanh trục back (roll).

 .. code-tab:: csharp

    var myBasis = Basis.Identity;
    var angle = Mathf.Tau / 2.0f;

    myBasis = myBasis.Rotated(Vector3.Up, angle);    // Xoay quanh trục up (yaw).
    myBasis = myBasis.Rotated(Vector3.Right, angle); // Xoay quanh trục right (pitch).
    myBasis = myBasis.Rotated(Vector3.Back, angle);  // Xoay quanh trục back (roll).



.. rst-class:: classref-item-separator

----

.. _class_Basis_method_scaled:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **scaled**\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Basis_method_scaled>`

Trả về basis này với các thành phần của mỗi trục được scale theo các thành phần của ``scale`` đã cho.

Các hàng của ma trận basis được nhân với các thành phần của ``scale``. Đây là phép scale global (tương đối với parent).


.. tabs::

 .. code-tab:: gdscript

    var my_basis = Basis(
        Vector3(1, 1, 1),
        Vector3(2, 2, 2),
        Vector3(3, 3, 3)
    )
    my_basis = my_basis.scaled(Vector3(0, 2, -2))

    print(my_basis.x) # In ra (0.0, 2.0, -2.0)
    print(my_basis.y) # In ra (0.0, 4.0, -4.0)
    print(my_basis.z) # In ra (0.0, 6.0, -6.0)

 .. code-tab:: csharp

    var myBasis = new Basis(
        new Vector3(1.0f, 1.0f, 1.0f),
        new Vector3(2.0f, 2.0f, 2.0f),
        new Vector3(3.0f, 3.0f, 3.0f)
    );
    myBasis = myBasis.Scaled(new Vector3(0.0f, 2.0f, -2.0f));

    GD.Print(myBasis.X); // In ra (0, 2, -2)
    GD.Print(myBasis.Y); // In ra (0, 4, -4)
    GD.Print(myBasis.Z); // In ra (0, 6, -6)



.. rst-class:: classref-item-separator

----

.. _class_Basis_method_scaled_local:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **scaled_local**\ (\ scale\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Basis_method_scaled_local>`

Trả về basis này với mỗi trục được scale theo thành phần tương ứng trong ``scale`` đã cho.

Các cột của ma trận basis được nhân với các thành phần của ``scale``. Đây là phép scale local (tương đối với self).


.. tabs::

 .. code-tab:: gdscript

    var my_basis = Basis(
        Vector3(1, 1, 1),
        Vector3(2, 2, 2),
        Vector3(3, 3, 3)
    )
    my_basis = my_basis.scaled_local(Vector3(0, 2, -2))

    print(my_basis.x) # In ra (0.0, 0.0, 0.0)
    print(my_basis.y) # In ra (4.0, 4.0, 4.0)
    print(my_basis.z) # In ra (-6.0, -6.0, -6.0)

 .. code-tab:: csharp

    var myBasis = new Basis(
        new Vector3(1.0f, 1.0f, 1.0f),
        new Vector3(2.0f, 2.0f, 2.0f),
        new Vector3(3.0f, 3.0f, 3.0f)
    );
    myBasis = myBasis.ScaledLocal(new Vector3(0.0f, 2.0f, -2.0f));

    GD.Print(myBasis.X); // In ra (0, 0, 0)
    GD.Print(myBasis.Y); // In ra (4, 4, 4)
    GD.Print(myBasis.Z); // In ra (-6, -6, -6)



.. rst-class:: classref-item-separator

----

.. _class_Basis_method_slerp:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **slerp**\ (\ to\: :ref:`Basis<class_Basis>`, weight\: :ref:`float<class_float>`\ ) |const| :ref:`🔗<class_Basis_method_slerp>`

Thực hiện phép nội suy tuyến tính cầu với basis ``to``, sử dụng một ``weight``. Cả basis này và ``to`` đều nên biểu diễn một phép quay.

\ **Ví dụ:** Xoay mượt một :ref:`Node3D<class_Node3D>` đến basis đích theo thời gian, với một :ref:`Tween<class_Tween>`:

::

    var start_basis = Basis.IDENTITY
    var target_basis = Basis.IDENTITY.rotated(Vector3.UP, TAU / 2)

    func _ready():
        create_tween().tween_method(interpolate, 0.0, 1.0, 5.0).set_trans(Tween.TRANS_EXPO)

    func interpolate(weight):
        basis = start_basis.slerp(target_basis, weight)

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_tdotx:

.. rst-class:: classref-method

:ref:`float<class_float>` **tdotx**\ (\ with\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Basis_method_tdotx>`

Trả về tích vô hướng chuyển vị giữa ``with`` và trục :ref:`x<class_Basis_property_x>` (xem :ref:`transposed()<class_Basis_method_transposed>`).

Điều này tương đương với ``basis.x.dot(vector)``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_tdoty:

.. rst-class:: classref-method

:ref:`float<class_float>` **tdoty**\ (\ with\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Basis_method_tdoty>`

Trả về tích vô hướng chuyển vị giữa ``with`` và trục :ref:`y<class_Basis_property_y>` (xem :ref:`transposed()<class_Basis_method_transposed>`).

Điều này tương đương với ``basis.y.dot(vector)``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_tdotz:

.. rst-class:: classref-method

:ref:`float<class_float>` **tdotz**\ (\ with\: :ref:`Vector3<class_Vector3>`\ ) |const| :ref:`🔗<class_Basis_method_tdotz>`

Trả về tích vô hướng chuyển vị giữa ``with`` và trục :ref:`z<class_Basis_property_z>` (xem :ref:`transposed()<class_Basis_method_transposed>`).

Điều này tương đương với ``basis.z.dot(vector)``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_method_transposed:

.. rst-class:: classref-method

:ref:`Basis<class_Basis>` **transposed**\ (\ ) |const| :ref:`🔗<class_Basis_method_transposed>`

Trả về phiên bản chuyển vị của basis này. Thao tác này biến các cột của ma trận basis thành các hàng, và các hàng thành các cột.


.. tabs::

 .. code-tab:: gdscript

    var my_basis = Basis(
        Vector3(1, 2, 3),
        Vector3(4, 5, 6),
        Vector3(7, 8, 9)
    )
    my_basis = my_basis.transposed()

    print(my_basis.x) # In ra (1.0, 4.0, 7.0)
    print(my_basis.y) # In ra (2.0, 5.0, 8.0)
    print(my_basis.z) # In ra (3.0, 6.0, 9.0)

 .. code-tab:: csharp

    var myBasis = new Basis(
        new Vector3(1.0f, 2.0f, 3.0f),
        new Vector3(4.0f, 5.0f, 6.0f),
        new Vector3(7.0f, 8.0f, 9.0f)
    );
    myBasis = myBasis.Transposed();

    GD.Print(myBasis.X); // In ra (1, 4, 7)
    GD.Print(myBasis.Y); // In ra (2, 5, 8)
    GD.Print(myBasis.Z); // In ra (3, 6, 9)



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các toán tử
-----------------

.. _class_Basis_operator_neq_Basis:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`Basis<class_Basis>`\ ) :ref:`🔗<class_Basis_operator_neq_Basis>`

Trả về ``true`` nếu các thành phần của cả hai ma trận **Basis** không bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác số thực dấu phẩy động, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_Basis_method_is_equal_approx>` thay thế vì cách này đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_mul_Basis:

.. rst-class:: classref-operator

:ref:`Basis<class_Basis>` **operator ***\ (\ right\: :ref:`Basis<class_Basis>`\ ) :ref:`🔗<class_Basis_operator_mul_Basis>`

Biến đổi (nhân) basis ``right`` bằng basis này.

This is the operation performed between parent and child :ref:`Node3D<class_Node3D>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_mul_Vector3:

.. rst-class:: classref-operator

:ref:`Vector3<class_Vector3>` **operator ***\ (\ right\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_Basis_operator_mul_Vector3>`

Biến đổi (nhân) vector ``right`` bằng basis này, trả về một :ref:`Vector3<class_Vector3>`.


.. tabs::

 .. code-tab:: gdscript

    # Basis hoán đổi các trục X/Z và nhân đôi scale.
    var my_basis = Basis(Vector3(0, 2, 0), Vector3(2, 0, 0), Vector3(0, 0, 2))
    print(my_basis * Vector3(1, 2, 3)) # In ra (4.0, 2.0, 6.0)

 .. code-tab:: csharp

    // Basis hoán đổi các trục X/Z và nhân đôi scale.
    var myBasis = new Basis(new Vector3(0, 2, 0), new Vector3(2, 0, 0), new Vector3(0, 0, 2));
    GD.Print(myBasis * new Vector3(1, 2, 3)); // In ra (4, 2, 6)



.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_mul_float:

.. rst-class:: classref-operator

:ref:`Basis<class_Basis>` **operator ***\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Basis_operator_mul_float>`

Nhân tất cả các thành phần của **Basis** với :ref:`float<class_float>` đã cho. Thao tác này ảnh hưởng đồng đều đến scale của basis, thay đổi kích thước cả 3 trục theo giá trị ``right``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_mul_int:

.. rst-class:: classref-operator

:ref:`Basis<class_Basis>` **operator ***\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Basis_operator_mul_int>`

Nhân tất cả các thành phần của **Basis** với :ref:`int<class_int>` đã cho. Thao tác này ảnh hưởng đồng đều đến scale của basis, thay đổi kích thước cả 3 trục theo giá trị ``right``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_div_float:

.. rst-class:: classref-operator

:ref:`Basis<class_Basis>` **operator /**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_Basis_operator_div_float>`

Chia tất cả các thành phần của **Basis** cho :ref:`float<class_float>` đã cho. Thao tác này ảnh hưởng đồng đều đến scale của basis, thay đổi kích thước cả 3 trục theo giá trị ``right``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_div_int:

.. rst-class:: classref-operator

:ref:`Basis<class_Basis>` **operator /**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Basis_operator_div_int>`

Chia tất cả các thành phần của **Basis** cho :ref:`int<class_int>` đã cho. Thao tác này ảnh hưởng đồng đều đến scale của basis, thay đổi kích thước cả 3 trục theo giá trị ``right``.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_eq_Basis:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`Basis<class_Basis>`\ ) :ref:`🔗<class_Basis_operator_eq_Basis>`

Trả về ``true`` nếu các thành phần của cả hai ma trận **Basis** hoàn toàn bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác số thực dấu phẩy động, hãy cân nhắc sử dụng :ref:`is_equal_approx()<class_Basis_method_is_equal_approx>` thay thế vì cách này đáng tin cậy hơn.

.. rst-class:: classref-item-separator

----

.. _class_Basis_operator_idx_int:

.. rst-class:: classref-operator

:ref:`Vector3<class_Vector3>` **operator []**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_Basis_operator_idx_int>`

Truy cập từng trục (cột) của basis này theo chỉ mục. Chỉ mục ``0`` giống với :ref:`x<class_Basis_property_x>`, chỉ mục ``1`` giống với :ref:`y<class_Basis_property_y>`, và chỉ mục ``2`` giống với :ref:`z<class_Basis_property_z>`.

\ **Lưu ý:** Trong C++, toán tử này truy cập các hàng của ma trận basis, *không phải* các cột. Để có cùng hành vi như các ngôn ngữ scripting, hãy sử dụng các phương thức ``set_column`` và ``get_column``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
