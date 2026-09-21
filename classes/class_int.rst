:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/int.xml.

.. _class_int:

int
===

Một kiểu dựng sẵn dành cho số nguyên.

.. rst-class:: classref-introduction-group

Mô tả
-----

Kiểu số nguyên có dấu 64-bit. Điều này có nghĩa là nó có thể nhận các giá trị từ ``-2^63`` đến ``2^63 - 1``, tức là từ ``-9223372036854775808`` đến ``9223372036854775807``. Khi vượt quá các giới hạn này, nó sẽ quay vòng.

\ **int**\ có thể được tự động chuyển đổi thành :ref:`float<class_float>`\ khi cần, chẳng hạn như khi truyền chúng làm đối số cho các hàm. :ref:`float<class_float>` sẽ gần với số nguyên ban đầu nhất có thể.

Tương tự, :ref:`float<class_float>`\ có thể được tự động chuyển đổi thành **int**\ . Thao tác này sẽ cắt ngắn :ref:`float<class_float>`, loại bỏ mọi phần sau dấu phẩy động.

\ **Lưu ý:** Trong ngữ cảnh boolean, một **int** sẽ được đánh giá là ``false`` nếu nó bằng ``0``, và là ``true`` trong các trường hợp khác.


.. tabs::

 .. code-tab:: gdscript

    var x: int = 1 # x là 1
    x = 4.2 # x là 4, vì 4.2 bị cắt ngắn
    var max_int = 9223372036854775807 # Giá trị lớn nhất mà một int có thể lưu trữ
    max_int += 1 # max_int hiện là -9223372036854775808, vì nó đã quay vòng

 .. code-tab:: csharp

    int x = 1; // x là 1
    x = (int)4.2; // x là 4, vì 4.2 bị cắt ngắn
    // Bên dưới, chúng ta sử dụng long vì int của GDScript là 64-bit, còn int của C# là 32-bit.
    long maxLong = 9223372036854775807; // Giá trị lớn nhất mà một long có thể lưu trữ
    maxLong++; // maxLong hiện là -9223372036854775808, vì nó đã quay vòng.

    // Ngoài ra, có thể sử dụng kiểu int 32-bit của C#, vốn có giá trị lớn nhất nhỏ hơn.
    int maxInt = 2147483647; // Giá trị lớn nhất mà một int có thể lưu trữ
    maxInt++; // maxInt hiện là -2147483648, vì nó đã quay vòng



Bạn có thể sử dụng literal ``0b`` cho biểu diễn nhị phân, literal ``0x`` cho biểu diễn thập lục phân, và ký hiệu ``_`` để phân tách các số dài nhằm cải thiện khả năng đọc.


.. tabs::

 .. code-tab:: gdscript

    var x = 0b1001 # x là 9
    var y = 0xF5 # y là 245
    var z = 10_000_000 # z là 10000000

 .. code-tab:: csharp

    int x = 0b1001; // x là 9
    int y = 0xF5; // y là 245
    int z = 10_000_000; // z là 10000000



.. rst-class:: classref-reftable-group

Các hàm khởi tạo
----------------

.. table::
   :widths: auto

   +-----------------------+---------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`int<class_int_constructor_int>`\ (\ )                                     |
   +-----------------------+---------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`int<class_int_constructor_int>`\ (\ from\: :ref:`int<class_int>`\ )       |
   +-----------------------+---------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`int<class_int_constructor_int>`\ (\ from\: :ref:`String<class_String>`\ ) |
   +-----------------------+---------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`int<class_int_constructor_int>`\ (\ from\: :ref:`bool<class_bool>`\ )     |
   +-----------------------+---------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`int<class_int_constructor_int>`\ (\ from\: :ref:`float<class_float>`\ )   |
   +-----------------------+---------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các toán tử
-----------

.. table::
   :widths: auto

   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator !=<class_int_operator_neq_float>`\ (\ right\: :ref:`float<class_float>`\ )               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator !=<class_int_operator_neq_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator %<class_int_operator_mod_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator &<class_int_operator_bwand_int>`\ (\ right\: :ref:`int<class_int>`\ )                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Color<class_Color>`           | :ref:`operator *<class_int_operator_mul_Color>`\ (\ right\: :ref:`Color<class_Color>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Quaternion<class_Quaternion>` | :ref:`operator *<class_int_operator_mul_Quaternion>`\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>`       | :ref:`operator *<class_int_operator_mul_Vector2>`\ (\ right\: :ref:`Vector2<class_Vector2>`\ )          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Vector2i<class_Vector2i>`     | :ref:`operator *<class_int_operator_mul_Vector2i>`\ (\ right\: :ref:`Vector2i<class_Vector2i>`\ )       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3<class_Vector3>`       | :ref:`operator *<class_int_operator_mul_Vector3>`\ (\ right\: :ref:`Vector3<class_Vector3>`\ )          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Vector3i<class_Vector3i>`     | :ref:`operator *<class_int_operator_mul_Vector3i>`\ (\ right\: :ref:`Vector3i<class_Vector3i>`\ )       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Vector4<class_Vector4>`       | :ref:`operator *<class_int_operator_mul_Vector4>`\ (\ right\: :ref:`Vector4<class_Vector4>`\ )          |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`Vector4i<class_Vector4i>`     | :ref:`operator *<class_int_operator_mul_Vector4i>`\ (\ right\: :ref:`Vector4i<class_Vector4i>`\ )       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator *<class_int_operator_mul_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator *<class_int_operator_mul_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator **<class_int_operator_pow_float>`\ (\ right\: :ref:`float<class_float>`\ )               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator **<class_int_operator_pow_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator +<class_int_operator_sum_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator +<class_int_operator_sum_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator -<class_int_operator_dif_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator -<class_int_operator_dif_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`           | :ref:`operator /<class_int_operator_div_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator /<class_int_operator_div_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<<class_int_operator_lt_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<<class_int_operator_lt_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator \<\<<class_int_operator_bwsl_int>`\ (\ right\: :ref:`int<class_int>`\ )                  |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<=<class_int_operator_lte_float>`\ (\ right\: :ref:`float<class_float>`\ )              |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator \<=<class_int_operator_lte_int>`\ (\ right\: :ref:`int<class_int>`\ )                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ==<class_int_operator_eq_float>`\ (\ right\: :ref:`float<class_float>`\ )                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ==<class_int_operator_eq_int>`\ (\ right\: :ref:`int<class_int>`\ )                      |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ><class_int_operator_gt_float>`\ (\ right\: :ref:`float<class_float>`\ )                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator ><class_int_operator_gt_int>`\ (\ right\: :ref:`int<class_int>`\ )                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator >=<class_int_operator_gte_float>`\ (\ right\: :ref:`float<class_float>`\ )               |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`             | :ref:`operator >=<class_int_operator_gte_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator >><class_int_operator_bwsr_int>`\ (\ right\: :ref:`int<class_int>`\ )                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator ^<class_int_operator_bwxor_int>`\ (\ right\: :ref:`int<class_int>`\ )                    |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator unary+<class_int_operator_unplus>`\ (\ )                                                 |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator unary-<class_int_operator_unminus>`\ (\ )                                                |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator |<class_int_operator_bwor_int>`\ (\ right\: :ref:`int<class_int>`\ )                     |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`               | :ref:`operator ~<class_int_operator_bwnot>`\ (\ )                                                       |
   +-------------------------------------+---------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả hàm khởi tạo
------------------

.. _class_int_constructor_int:

.. rst-class:: classref-constructor

:ref:`int<class_int>` **int**\ (\ ) :ref:`🔗<class_int_constructor_int>`

Tạo một **int** có giá trị ``0``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`int<class_int>` **int**\ (\ from\: :ref:`int<class_int>`\ )

Tạo một **int** là bản sao của **int** đã cho.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`int<class_int>` **int**\ (\ from\: :ref:`String<class_String>`\ )

Tạo một **int** mới từ một :ref:`String<class_String>`, tuân theo các quy tắc giống như :ref:`String.to_int()<class_String_method_to_int>`.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`int<class_int>` **int**\ (\ from\: :ref:`bool<class_bool>`\ )

Tạo một **int** mới từ một :ref:`bool<class_bool>`. ``true`` được chuyển đổi thành ``1`` và ``false`` được chuyển đổi thành ``0``.

.. rst-class:: classref-item-separator

----

.. rst-class:: classref-constructor

:ref:`int<class_int>` **int**\ (\ from\: :ref:`float<class_float>`\ )

Tạo một **int** mới từ một :ref:`float<class_float>`. Thao tác này sẽ cắt ngắn :ref:`float<class_float>`, loại bỏ mọi phần sau dấu phẩy động.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả toán tử
-------------

.. _class_int_operator_neq_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_neq_float>`

Trả về ``true`` nếu **int** không tương đương với :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_neq_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator !=**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_neq_int>`

Trả về ``true`` nếu các **int**\ không bằng nhau.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mod_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator %**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_mod_int>`

Trả về phần dư sau khi chia hai **int**\ . Sử dụng phép chia cắt ngắn, trong đó trả về số âm nếu số bị chia là số âm. Nếu không muốn như vậy, hãy cân nhắc sử dụng :ref:`@GlobalScope.posmod()<class_@GlobalScope_method_posmod>`.

::

    print(6 % 2) # In ra 0
    print(11 % 4) # In ra 3
    print(-5 % 3) # In ra -2

.. rst-class:: classref-item-separator

----

.. _class_int_operator_bwand_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator &**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_bwand_int>`

Thực hiện phép toán ``AND`` theo bit.

::

    print(0b1100 & 0b1010) # In ra 8 (nhị phân 1000)

Điều này hữu ích để lấy các cờ nhị phân từ một biến.

::

    var flags = 0b101
    # Kiểm tra xem bit thứ nhất hoặc thứ hai có được bật hay không.
    if flags & 0b011:
        do_stuff() # Dòng này sẽ được thực thi.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Color:

.. rst-class:: classref-operator

:ref:`Color<class_Color>` **operator ***\ (\ right\: :ref:`Color<class_Color>`\ ) :ref:`🔗<class_int_operator_mul_Color>`

Nhân từng thành phần của :ref:`Color<class_Color>` với **int**.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Quaternion:

.. rst-class:: classref-operator

:ref:`Quaternion<class_Quaternion>` **operator ***\ (\ right\: :ref:`Quaternion<class_Quaternion>`\ ) :ref:`🔗<class_int_operator_mul_Quaternion>`

Nhân từng thành phần của :ref:`Quaternion<class_Quaternion>` với **int**. Bản thân thao tác này không có ý nghĩa, nhưng có thể được sử dụng như một phần của biểu thức lớn hơn.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Vector2:

.. rst-class:: classref-operator

:ref:`Vector2<class_Vector2>` **operator ***\ (\ right\: :ref:`Vector2<class_Vector2>`\ ) :ref:`🔗<class_int_operator_mul_Vector2>`

Nhân từng thành phần của :ref:`Vector2<class_Vector2>` với **int**.

::

    print(2 * Vector2(1, 4)) # In ra (2, 8)

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Vector2i:

.. rst-class:: classref-operator

:ref:`Vector2i<class_Vector2i>` **operator ***\ (\ right\: :ref:`Vector2i<class_Vector2i>`\ ) :ref:`🔗<class_int_operator_mul_Vector2i>`

Nhân từng thành phần của :ref:`Vector2i<class_Vector2i>` với **int**.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Vector3:

.. rst-class:: classref-operator

:ref:`Vector3<class_Vector3>` **operator ***\ (\ right\: :ref:`Vector3<class_Vector3>`\ ) :ref:`🔗<class_int_operator_mul_Vector3>`

Nhân từng thành phần của :ref:`Vector3<class_Vector3>` với **int**.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Vector3i:

.. rst-class:: classref-operator

:ref:`Vector3i<class_Vector3i>` **operator ***\ (\ right\: :ref:`Vector3i<class_Vector3i>`\ ) :ref:`🔗<class_int_operator_mul_Vector3i>`

Nhân từng thành phần của :ref:`Vector3i<class_Vector3i>` với **int**.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Vector4:

.. rst-class:: classref-operator

:ref:`Vector4<class_Vector4>` **operator ***\ (\ right\: :ref:`Vector4<class_Vector4>`\ ) :ref:`🔗<class_int_operator_mul_Vector4>`

Nhân từng thành phần của :ref:`Vector4<class_Vector4>` với **int**.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_Vector4i:

.. rst-class:: classref-operator

:ref:`Vector4i<class_Vector4i>` **operator ***\ (\ right\: :ref:`Vector4i<class_Vector4i>`\ ) :ref:`🔗<class_int_operator_mul_Vector4i>`

Nhân từng thành phần của :ref:`Vector4i<class_Vector4i>` với **int**.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator ***\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_mul_float>`

Nhân :ref:`float<class_float>` với **int**. Kết quả là một :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_mul_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator ***\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_mul_int>`

Nhân hai **int**\ .

.. rst-class:: classref-item-separator

----

.. _class_int_operator_pow_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator ****\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_pow_float>`

Nâng một **int** lên lũy thừa của :ref:`float<class_float>`. Kết quả là một :ref:`float<class_float>`.

::

    print(2 ** 0.5) # In ra 1.4142135623731

.. rst-class:: classref-item-separator

----

.. _class_int_operator_pow_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator ****\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_pow_int>`

Nâng **int** bên trái lên lũy thừa của **int** bên phải.

::

    print(3 ** 4) # In ra 81

.. rst-class:: classref-item-separator

----

.. _class_int_operator_sum_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator +**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_sum_float>`

Cộng **int** với :ref:`float<class_float>`. Kết quả là một :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_sum_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator +**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_sum_int>`

Cộng hai **int**\ .

.. rst-class:: classref-item-separator

----

.. _class_int_operator_dif_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator -**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_dif_float>`

Trừ :ref:`float<class_float>` khỏi **int**. Kết quả là một :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_dif_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator -**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_dif_int>`

Trừ hai **int**\ cho nhau.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_div_float:

.. rst-class:: classref-operator

:ref:`float<class_float>` **operator /**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_div_float>`

Chia **int** cho :ref:`float<class_float>`. Kết quả là một :ref:`float<class_float>`.

::

    print(10 / 3.0) # In ra 3.33333333333333

.. rst-class:: classref-item-separator

----

.. _class_int_operator_div_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator /**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_div_int>`

Chia hai **int**\ . Kết quả là một **int**. Thao tác này sẽ cắt ngắn :ref:`float<class_float>`, loại bỏ mọi phần sau dấu phẩy động.

::

    print(6 / 2) # In ra 3
    print(5 / 3) # In ra 1

.. rst-class:: classref-item-separator

----

.. _class_int_operator_lt_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_lt_float>`

Trả về ``true`` nếu **int** nhỏ hơn :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_lt_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_lt_int>`

Trả về ``true`` nếu **int** bên trái nhỏ hơn **int** bên phải.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_bwsl_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator <<**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_bwsl_int>`

Thực hiện phép dịch trái theo bit. Về cơ bản, thao tác này tương đương với việc nhân với một lũy thừa của 2.

::

    print(0b1010 << 1) # In ra 20 (nhị phân 10100)
    print(0b1010 << 3) # In ra 80 (nhị phân 1010000)

.. rst-class:: classref-item-separator

----

.. _class_int_operator_lte_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <=**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_lte_float>`

Trả về ``true`` nếu **int** nhỏ hơn hoặc bằng :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_lte_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator <=**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_lte_int>`

Trả về ``true`` nếu **int** bên trái nhỏ hơn hoặc bằng **int** bên phải.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_eq_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_eq_float>`

Trả về ``true`` nếu **int** bằng :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_eq_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator ==**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_eq_int>`

Trả về ``true`` nếu hai **int**\ s bằng nhau.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_gt_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_gt_float>`

Trả về ``true`` nếu **int** lớn hơn :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_gt_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_gt_int>`

Trả về ``true`` nếu **int** bên trái lớn hơn **int** bên phải.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_gte_float:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >=**\ (\ right\: :ref:`float<class_float>`\ ) :ref:`🔗<class_int_operator_gte_float>`

Trả về ``true`` nếu **int** lớn hơn hoặc bằng :ref:`float<class_float>`.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_gte_int:

.. rst-class:: classref-operator

:ref:`bool<class_bool>` **operator >=**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_gte_int>`

Trả về ``true`` nếu **int** bên trái lớn hơn hoặc bằng **int** bên phải.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_bwsr_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator >>**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_bwsr_int>`

Thực hiện phép dịch bit sang phải. Về cơ bản, phép này tương đương với việc chia cho một lũy thừa của 2.

::

    print(0b1010 >> 1) # In ra 5 (nhị phân 101)
    print(0b1010 >> 2) # In ra 2 (nhị phân 10)

.. rst-class:: classref-item-separator

----

.. _class_int_operator_bwxor_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator ^**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_bwxor_int>`

Thực hiện phép toán ``XOR`` theo bit.

::

    print(0b1100 ^ 0b1010) # In ra 6 (nhị phân 110)

.. rst-class:: classref-item-separator

----

.. _class_int_operator_unplus:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator unary+**\ (\ ) :ref:`🔗<class_int_operator_unplus>`

Trả về cùng giá trị như khi không có ``+``. Unary ``+`` không thực hiện thao tác gì, nhưng đôi khi có thể giúp mã của bạn dễ đọc hơn.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_unminus:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator unary-**\ (\ ) :ref:`🔗<class_int_operator_unminus>`

Trả về giá trị phủ định của **int**. Nếu dương, biến số đó thành số âm. Nếu âm, biến số đó thành số dương. Nếu bằng 0, không thực hiện thao tác gì.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_bwor_int:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator |**\ (\ right\: :ref:`int<class_int>`\ ) :ref:`🔗<class_int_operator_bwor_int>`

Thực hiện phép toán ``OR`` theo bit.

::

    print(0b1100 | 0b1010) # In ra 14 (nhị phân 1110)

Phép này hữu ích khi lưu trữ các cờ nhị phân trong một biến.

::

    var flags = 0
    flags |= 0b101 # Bật bit thứ nhất và thứ ba.

.. rst-class:: classref-item-separator

----

.. _class_int_operator_bwnot:

.. rst-class:: classref-operator

:ref:`int<class_int>` **operator ~**\ (\ ) :ref:`🔗<class_int_operator_bwnot>`

Thực hiện phép toán ``NOT`` theo bit trên **int**. Do `2's complement <https://en.wikipedia.org/wiki/Two%27s_complement>`__, phép này về cơ bản tương đương với ``-(int + 1)``.

::

    print(~4) # In ra -5
    print(~(-7)) # In ra 6

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
