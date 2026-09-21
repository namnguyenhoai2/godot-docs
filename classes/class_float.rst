:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/float.xml.

.. _class_float:

float
=====

Một kiểu dựng sẵn dành cho các số dấu phẩy động.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu dựng sẵn **float** là một số dấu phẩy động độ chính xác kép 64 bit, tương đương với ``double`` trong C++. Kiểu này có 14 chữ số thập phân có độ chính xác đáng tin cậy. Giá trị lớn nhất của **float** xấp xỉ ``1.79769e308``, còn giá trị nhỏ nhất xấp xỉ ``-1.79769e308``.

Nhiều phương thức và thuộc tính trong engine thay vào đó sử dụng các số dấu phẩy động độ chính xác đơn 32 bit, tương đương với ``float`` trong C++, có 6 chữ số thập phân có độ chính xác đáng tin cậy. Đối với các cấu trúc dữ liệu như :ref:`Vector2<class_Vector2>` và :ref:`Vector3<class_Vector3>`, Godot mặc định sử dụng các số dấu phẩy động 32 bit, nhưng có thể thay đổi để sử dụng double 64 bit nếu Godot được biên dịch với tùy chọn ``precision=double``.

Các phép toán thực hiện bằng kiểu **float** không được đảm bảo là chính xác và thường tạo ra các sai số nhỏ. Thông thường, bạn nên sử dụng các phương thức :ref:`@GlobalScope.is_equal_approx()<class_@GlobalScope_method_is_equal_approx>` và :ref:`@GlobalScope.is_zero_approx()<class_@GlobalScope_method_is_zero_approx>` thay vì ``==`` để so sánh các giá trị **float** bằng nhau.

\ **Lưu ý:** Trong ngữ cảnh boolean, một **float** sẽ được đánh giá là ``false`` nếu nó chính xác bằng ``0.0``, và là ``true`` trong các trường hợp khác.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- `Wikipedia: Double-precision floating-point format <https://en.wikipedia.org/wiki/Double-precision_floating-point_format>`__

- `Wikipedia: Single-precision floating-point format <https://en.wikipedia.org/wiki/Single-precision_floating-point_format>`__

.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +---------------------------+---------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`float<class_float_constructor_float>`\ (\ )                                     |
   +---------------------------+---------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`float<class_float_constructor_float>`\ (\ from\: :ref:`float<class_float>`\ )   |
   +---------------------------+---------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`float<class_float_constructor_float>`\ (\ from\: :ref:`String<class_String>`\ ) |
   +---------------------------+---------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`float<class_float_constructor_float>`\ (\ from\: :ref:`bool<class_bool>`\ )     |
   +---------------------------+---------------------------------------------------------------------------------------+
   | :ref:`float<class_float>` | :ref:`float<class_float_constructor_float>`\ (\ from\: :ref:`int<class_int>`\ )       |
   +---------------------------+---------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các toán tử
-----------

.. table::
   :widths: auto

   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator !=<class_float_operator_neq_float>`\ (\ right\: :ref:`float<class_float>`\ )               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator !=<class_float_operator_neq_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`           | :ref:`operator *<class_float_operator_mul_Color>`\ (\ right\: :ref:`Color<class_Color>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator *<class_float_operator_mul_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`       | :ref:`operator *<class_float_operator_mul_Vector2>`\ (\ right\: :ref:`Vector2<class_Vector2>`\ )          |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`       | :ref:`operator *<class_float_operator_mul_Vector2i>`\ (\ right\: :ref:`Vector2i<class_Vector2i>`\ )       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`operator *<class_float_operator_mul_Vector3>`\ (\ right\: :ref:`Vector3<class_Vector3>`\ )          |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`operator *<class_float_operator_mul_Vector3i>`\ (\ right\: :ref:`Vector3i<class_Vector3i>`\ )       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Vector4<class_Vector4>`       | :ref:`operator *<class_float_operator_mul_Vector4>`\ (\ right\: :ref:`Vector4<class_Vector4>`\ )          |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`Vector4<class_Vector4>`       | :ref:`operator *<class_float_operator_mul_Vector4i>`\ (\ right\: :ref:`Vector4i<class_Vector4i>`\ )       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator *<class_float_operator_mul_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator *<class_float_operator_mul_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator **<class_float_operator_pow_float>`\ (\ right\: :ref:`float<class_float>`\ )               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator **<class_float_operator_pow_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator +<class_float_operator_sum_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator +<class_float_operator_sum_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator -<class_float_operator_dif_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator -<class_float_operator_dif_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator /<class_float_operator_div_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator /<class_float_operator_div_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<<class_float_operator_lt_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<<class_float_operator_lt_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<=<class_float_operator_lte_float>`\ (\ right\: :ref:`float<class_float>`\ )              |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<=<class_float_operator_lte_int>`\ (\ right\: :ref:`int<class_int>`\ )                    |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ==<class_float_operator_eq_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ==<class_float_operator_eq_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ><class_float_operator_gt_float>`\ (\ right\: :ref:`float<class_float>`\ )                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ><class_float_operator_gt_int>`\ (\ right\: :ref:`int<class_int>`\ )                       |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator >=<class_float_operator_gte_float>`\ (\ right\: :ref:`float<class_float>`\ )               |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator >=<class_float_operator_gte_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator unary+<class_float_operator_unplus>`\ (\ )                                                 |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator unary-<class_float_operator_unminus>`\ (\ )                                                |
   +-------------------------------------+-----------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các hàm khởi tạo
----------------------

.. _class_float_constructor_float:

.. rst-class:: classref-constructor

:ref:`float<class_float>` **float**\ (\ ) :ref:`🔗<class_float_constructor_float>`

Tạo một **float** được khởi tạo mặc định với giá trị ``0.0``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`float<class_float>` **float**\ (\ from\: :ref:`float<class_float>`\ )

Tạo một **float** dưới dạng bản sao của **float** được cung cấp.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`float<class_float>` **float**\ (\ from\: :ref:`String<class_String>`\ )

Chuyển đổi một :ref:`String<class_String>` thành **float**, theo cùng quy tắc như :ref:`String.to_float()<class_String_method_to_float>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`float<class_float>` **float**\ (\ from\: :ref:`bool<class_bool>`\ )

Ép kiểu một giá trị :ref:`bool<class_bool>` thành giá trị dấu phẩy động; ``float(true)`` sẽ bằng 1.0 và ``float(false)`` sẽ bằng 0.0.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`float<class_float>` **float**\ (\ from\: :ref:`int<class_int>`\ )

Ép kiểu một giá trị :ref:`int<class_int>` thành giá trị dấu phẩy động; ``float(1)`` sẽ bằng ``1.0``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các toán tử
-----------------

.. _class_float_operator_neq_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_neq_float>`

Trả về ``true`` nếu hai float khác nhau.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả của toán tử này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_neq_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_neq_int>`

Trả về ``true`` nếu số nguyên có giá trị khác với float.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Color:

.. rst-class:: classref-operator

:ref:`Color<class_Color>` **operator ***\ (\ right\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_float_operator_mul_Color>`

Nhân từng thành phần của :ref:`Color<class_Color>`, bao gồm cả alpha, với **float** được cung cấp.

::

    print(1.5 * Color(0.5, 0.5, 0.5)) # In ra (0.75, 0.75, 0.75, 1.5)

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Quaternion:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator ***\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_float_operator_mul_Quaternion>`

Nhân từng thành phần của :ref:`Quaternion<class_Quaternion>` với **float** được cung cấp. Bản thân phép toán này không có ý nghĩa, nhưng có thể được sử dụng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Vector2:

.. rst-class:: classref-operator

:ref:`Vector2<class_Vector2>` **operator ***\ (\ right\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_float_operator_mul_Vector2>`

Nhân từng thành phần của :ref:`Vector2<class_Vector2>` với **float** được cung cấp.

::

    print(2.5 * Vector2(1, 3)) # In ra (2.5, 7.5)

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Vector2i:

.. rst-class:: classref-operator

:ref:`Vector2<class_Vector2>` **operator ***\ (\ right\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_float_operator_mul_Vector2i>`

Nhân từng thành phần của :ref:`Vector2i<class_Vector2i>` với **float** được cung cấp. Trả về một :ref:`Vector2<class_Vector2>`.

::

    print(0.9 * Vector2i(10, 15)) # In ra (9.0, 13.5)

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Vector3:

.. rst-class:: classref-operator

:ref:`Vector3<class_Vector3>` **operator ***\ (\ right\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_float_operator_mul_Vector3>`

Nhân từng thành phần của :ref:`Vector3<class_Vector3>` với **float** được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Vector3i:

.. rst-class:: classref-operator

:ref:`Vector3<class_Vector3>` **operator ***\ (\ right\: :ref:`Vector3i<class_Vector3i>`\ ) :ref:`🔗<class_float_operator_mul_Vector3i>`

Nhân từng thành phần của :ref:`Vector3i<class_Vector3i>` với **float** được cung cấp. Trả về một :ref:`Vector3<class_Vector3>`.

::

    print(0.9 * Vector3i(10, 15, 20)) # In ra (9.0, 13.5, 18.0)

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Vector4:

.. rst-class:: classref-operator

:ref:`Vector4<class_Vector4>` **operator ***\ (\ right\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_float_operator_mul_Vector4>`

Nhân từng thành phần của :ref:`Vector4<class_Vector4>` với **float** được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_Vector4i:

.. rst-class:: classref-operator

:ref:`Vector4<class_Vector4>` **operator ***\ (\ right\: :ref:`Vector4i<class_Vector4i>`\ ) :ref:`🔗<class_float_operator_mul_Vector4i>`

Nhân từng thành phần của :ref:`Vector4i<class_Vector4i>` với **float** được cung cấp. Trả về một :ref:`Vector4<class_Vector4>`.

::

    print(0.9 * Vector4i(10, 15, 20, -10)) # In ra (9.0, 13.5, 18.0, -9.0)

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator ***\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_mul_float>`

Nhân hai **float**\.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_mul_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator ***\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_mul_int>`

Nhân một **float** với một :ref:`int<class_int>`. Kết quả là một **float**.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_pow_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator ****\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_pow_float>`

Lũy thừa một **float** với số mũ là một **float**.

::

    print(39.0625**0.25) # 2.5

.. rst-class:: classref-item-separator

----

.. _class_float_operator_pow_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator ****\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_pow_int>`

Lũy thừa một **float** với số mũ là một :ref:`int<class_int>`. Kết quả là một **float**.

::

    print(0.9**3) # 0.729

.. rst-class:: classref-item-separator

----

.. _class_float_operator_sum_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator +**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_sum_float>`

Cộng hai float.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_sum_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator +**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_sum_int>`

Cộng một **float** với một :ref:`int<class_int>`. Kết quả là một **float**.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_dif_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator -**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_dif_float>`

Trừ một float khỏi một float.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_dif_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator -**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_dif_int>`

Trừ một :ref:`int<class_int>` khỏi một **float**. Kết quả là một **float**.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_div_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator /**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_div_float>`

Chia hai float.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_div_int:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator /**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_div_int>`

Chia một **float** cho một :ref:`int<class_int>`. Kết quả là một **float**.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_lt_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_lt_float>`

Trả về ``true`` nếu float bên trái nhỏ hơn float bên phải.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả của toán tử này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_lt_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_lt_int>`

Trả về ``true`` nếu **float** này nhỏ hơn :ref:`int<class_int>` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_lte_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <=**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_lte_float>`

Trả về ``true`` nếu float bên trái nhỏ hơn hoặc bằng float bên phải.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả của toán tử này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_lte_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <=**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_lte_int>`

Trả về ``true`` nếu **float** này nhỏ hơn hoặc bằng :ref:`int<class_int>` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_eq_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_eq_float>`

Trả về ``true`` nếu hai float hoàn toàn bằng nhau.

\ **Lưu ý:** Do lỗi độ chính xác của số dấu phẩy động, hãy cân nhắc sử dụng :ref:`@GlobalScope.is_equal_approx()<class_@GlobalScope_method_is_equal_approx>` hoặc :ref:`@GlobalScope.is_zero_approx()<class_@GlobalScope_method_is_zero_approx>` thay thế vì chúng đáng tin cậy hơn.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống các số khác. Do đó, kết quả của toán tử này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_eq_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_eq_int>`

Trả về ``true`` nếu **float** và :ref:`int<class_int>` được cung cấp bằng nhau.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_gt_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_gt_float>`

Trả về ``true`` nếu số thực bên trái lớn hơn số thực bên phải.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống như các số khác. Do đó, kết quả từ toán tử này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_gt_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_gt_int>`

Trả về ``true`` nếu **float** này lớn hơn :ref:`int<class_int>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_gte_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >=**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_float_operator_gte_float>`

Trả về ``true`` nếu số thực bên trái lớn hơn hoặc bằng số thực bên phải.

\ **Lưu ý:** :ref:`@GDScript.NAN<class_@GDScript_constant_NAN>` không hoạt động giống như các số khác. Do đó, kết quả từ toán tử này có thể không chính xác nếu có NaN.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_gte_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >=**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_float_operator_gte_int>`

Trả về ``true`` nếu **float** này lớn hơn hoặc bằng :ref:`int<class_int>` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_unplus:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator unary+**\ (\ ) :ref:`🔗<class_float_operator_unplus>`

Trả về cùng giá trị như khi không có ``+``. Unary ``+`` không thực hiện thao tác gì, nhưng đôi khi có thể giúp code của bạn dễ đọc hơn.

.. rst-class:: classref-item-separator

----

.. _class_float_operator_unminus:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator unary-**\ (\ ) :ref:`🔗<class_float_operator_unminus>`

Trả về giá trị âm của **float**. Nếu số dương, chuyển số đó thành số âm. Nếu số âm, chuyển số đó thành số dương. Với số thực, số 0 có thể là số dương hoặc số âm.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
