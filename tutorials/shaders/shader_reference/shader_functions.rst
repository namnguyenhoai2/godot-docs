.. _doc_shader_functions:

Các hàm shader tích hợp sẵn
===========================

Godot hỗ trợ một số lượng lớn các hàm shader tích hợp sẵn, gần như tuân theo đặc tả GLSL ES 3.0.

.. note::
    Các bí danh kiểu (type alias) sau đây chỉ được sử dụng trong tài liệu để giảm việc khai báo hàm lặp lại. Mỗi bí danh có thể tham chiếu đến một trong nhiều kiểu thực tế.

    +-----------------+-------------------------------------------------------+-----------------------------+
    | bí danh         | các kiểu thực tế                                      | bí danh trong tài liệu GLSL |
    +=================+=======================================================+=============================+
    | vec_type        | float, vec2, vec3, hoặc vec4                          | genType                     |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | vec_int_type    | int, ivec2, ivec3, hoặc ivec4                         | genIType                    |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | vec_uint_type   | uint, uvec2, uvec3, hoặc uvec4                        | genUType                    |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | vec_bool_type   | bool, bvec2, bvec3, hoặc bvec4                        | genBType                    |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | mat_type        | mat2, mat3, hoặc mat4                                 | mat                         |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | gvec4_type      | vec4, ivec4, hoặc uvec4                               | gvec4                       |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | gsampler2D      | sampler2D, isampler2D, hoặc uSampler2D                | gsampler2D                  |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | gsampler2DArray | sampler2DArray, isampler2DArray, hoặc uSampler2DArray | gsampler2DArray             |
    +-----------------+-------------------------------------------------------+-----------------------------+
    | gsampler3D      | sampler3D, isampler3D, hoặc uSampler3D                | gsampler3D                  |
    +-----------------+-------------------------------------------------------+-----------------------------+

    Nếu bất kỳ kiểu nào trong số này được chỉ định cho nhiều tham số, tất cả chúng phải cùng một kiểu trừ khi có ghi chú khác.

.. _shading_componentwise:

.. note::
    Nhiều hàm nhận một hoặc nhiều vector hoặc ma trận sẽ thực hiện hàm được mô tả trên từng thành phần của vector/ma trận. Một số ví dụ:

    .. table::
        :class: nowrap-col2 nowrap-col1
        :widths: auto

        +---------------------------------------+-------------------------------------------+
        | Phép toán                             | Phép toán vô hướng tương đương            |
        +=======================================+===========================================+
        | ``sqrt(vec2(4, 64))``                 | ``vec2(sqrt(4), sqrt(64))``               |
        +---------------------------------------+-------------------------------------------+
        | ``min(vec2(3, 4), 1)``                | ``vec2(min(3, 1), min(4, 1))``            |
        +---------------------------------------+-------------------------------------------+
        | ``min(vec3(1, 2, 3),vec3(5, 1, 3))``  | ``vec3(min(1, 5), min(2, 1), min(3, 3))`` |
        +---------------------------------------+-------------------------------------------+
        | ``pow(vec3(3, 8, 5 ), 2)``            | ``vec3(pow(3, 2), pow(8, 2), pow(5, 2))`` |
        +---------------------------------------+-------------------------------------------+
        | ``pow(vec3(3, 8, 5), vec3(1, 2, 4))`` | ``vec3(pow(3, 1), pow(8, 2), pow(5, 4))`` |
        +---------------------------------------+-------------------------------------------+

    `Đặc tả Ngôn ngữ GLSL <http://www.opengl.org/registry/doc/GLSLangSpec.4.30.6.pdf>`_ nêu trong mục 5.10 Phép toán Vector và Ma trận:

        Với một vài ngoại lệ, các phép toán được thực hiện theo từng thành phần. Thông thường, khi một toán tử tác động lên một vector hoặc ma trận, nó sẽ tác động độc lập lên từng thành phần của vector hoặc ma trận theo cách thức từng thành phần. [...] Các ngoại lệ là ma trận nhân với vector, vector nhân với ma trận và ma trận nhân với ma trận. Các phép toán này không được thực hiện theo từng thành phần, mà thực hiện phép nhân đại số tuyến tính chính xác.

Các mô tả hàm này được điều chỉnh và sửa đổi từ `tài liệu OpenGL chính thức <https://registry.khronos.org/OpenGL-Refpages/gl4/>`__, ban đầu do Khronos Group phát hành theo `Open Publication License <https://opencontent.org/openpub>`__. Mỗi mô tả hàm liên kết đến tài liệu OpenGL chính thức tương ứng. Lịch sử sửa đổi của trang này có thể được xem trên `GitHub <https://github.com/godotengine/godot-docs/blob/master/tutorials/shaders/shader_reference/shader_functions.rst>`__.

.. rst-class:: classref-section-separator

----



.. rst-class:: classref-reftable-group

Các hàm lượng giác
------------------

.. table::
    :class: nowrap-col2
    :widths: auto

    +-----------------+-----------------------------------------------------------------+-----------------------------+
    |    Return Type  |                          Function                               | Description / Return value  |
    +=================+=================================================================+=============================+
    | |vec_type|      | :ref:`radians<shader_func_radians>`\ (\ |vec_type| degrees)     | Convert degrees to radians. |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`degrees<shader_func_degrees>`\ (\ |vec_type| radians)     | Convert radians to degrees. |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`sin<shader_func_sin>`\ (\ |vec_type| x)                   | Sine.                       |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`cos<shader_func_cos>`\ (\ |vec_type| x)                   | Cosine.                     |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`tan<shader_func_tan>`\ (\ |vec_type| x)                   | Tangent.                    |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`asin<shader_func_asin>`\ (\ |vec_type| x)                 | Arc sine.                   |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`acos<shader_func_acos>`\ (\ |vec_type| x)                 | Arc cosine.                 |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | | |vec_type|    | | :ref:`atan<shader_func_atan>`\ (\ |vec_type| y_over_x)        | Arc tangent.                |
    | | |vec_type|    | | :ref:`atan<shader_func_atan2>`\ (\ |vec_type| y, |vec_type| x)|                             |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`sinh<shader_func_sinh>`\ (\ |vec_type| x)                 | Hyperbolic sine.            |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`cosh<shader_func_cosh>`\ (\ |vec_type| x)                 | Hyperbolic cosine.          |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`tanh<shader_func_tanh>`\ (\ |vec_type| x)                 | Hyperbolic tangent.         |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`asinh<shader_func_asinh>`\ (\ |vec_type| x)               | Arc hyperbolic sine.        |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`acosh<shader_func_acosh>`\ (\ |vec_type| x)               | Arc hyperbolic cosine.      |
    +-----------------+-----------------------------------------------------------------+-----------------------------+
    | |vec_type|      | :ref:`atanh<shader_func_atanh>`\ (\ |vec_type| x)               | Arc hyperbolic tangent.     |
    +-----------------+-----------------------------------------------------------------+-----------------------------+


.. rst-class:: classref-descriptions-group

Mô tả các hàm lượng giác
~~~~~~~~~~~~~~~~~~~~~~~~

.. _shader_func_radians:

.. rst-class:: classref-method

|vec_type| **radians**\ (\ |vec_type| degrees) :ref:`🔗<shader_func_radians>`

    |componentwise|

    Chuyển đổi một đại lượng được chỉ định theo độ sang radian, theo công thức ``degrees * (PI / 180)``.

    :param degrees:Đại lượng, tính theo độ, cần được chuyển đổi sang radian.

    :return:Đầu vào ``degrees`` được chuyển đổi sang radian.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/radians.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_degrees:

.. rst-class:: classref-method

|vec_type| **degrees**\ (\ |vec_type| radians) :ref:`🔗<shader_func_degrees>`

    |componentwise|

    Chuyển đổi một đại lượng được chỉ định theo radian sang độ, theo công thức ``radians * (180 / PI)``

    :param radians:Đại lượng, tính theo radian, cần được chuyển đổi sang độ.

    :return:Đầu vào ``radians`` được chuyển đổi sang độ.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/degrees.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_sin:

.. rst-class:: classref-method

|vec_type| **sin**\ (\ |vec_type| angle) :ref:`🔗<shader_func_sin>`

    |componentwise|

    Trả về sin lượng giác của ``angle``.

    :param angle:Đại lượng, tính theo radian, cần trả về sin.

    :return:Sin của ``angle``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sin.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_cos:

.. rst-class:: classref-method

|vec_type| **cos**\ (\ |vec_type| angle) :ref:`🔗<shader_func_cos>`

    |componentwise|

    Trả về cosin lượng giác của ``angle``.

    :param angle:Đại lượng, tính theo radian, cần trả về cosin.

    :return:Cosin của ``angle``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/cos.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_tan:

.. rst-class:: classref-method

|vec_type| **tan**\ (\ |vec_type| angle) :ref:`🔗<shader_func_tan>`

    |componentwise|

    Trả về tang lượng giác của ``angle``.

    :param angle:Giá trị, tính bằng radian, cần trả về tiếp tuyến.

    :return:Tiếp tuyến của ``angle``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/tan.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_asin:

.. rst-class:: classref-method

|vec_type| **asin**\ (\ |vec_type| x) :ref:`🔗<shader_func_asin>`

    |componentwise|

    Sin cung, hay sin nghịch đảo. Tính góc có sin bằng ``x`` và nằm trong khoảng ``[-PI/2, PI/2]``. Kết quả không xác định nếu ``x < -1`` hoặc ``x > 1``.

    :param x:Giá trị cần trả về sin cung.
    :return:Góc có sin lượng giác bằng ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/asin.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_acos:

.. rst-class:: classref-method

|vec_type| **acos**\ (\ |vec_type| x) :ref:`🔗<shader_func_acos>`

    |componentwise|

    Cos cung, hay cos nghịch đảo. Tính góc có cos bằng ``x`` và nằm trong khoảng ``[0, PI]``.

    Kết quả không xác định nếu ``x < -1`` hoặc ``x > 1``.

    :param x:Giá trị cần trả về cos cung.

    :return:Góc có cos lượng giác bằng ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/acos.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_atan:

.. rst-class:: classref-method

|vec_type| **atan**\ (\ |vec_type| y_over_x) :ref:`🔗<shader_func_atan>`

    |componentwise|

    Tính tan cung với giá trị tiếp tuyến là ``y/x``.

    .. Note::
        Do sự mơ hồ về dấu, hàm không thể xác định chắc chắn góc nằm ở góc phần tư nào chỉ dựa trên giá trị tiếp tuyến. Nếu cần biết góc phần tư, hãy sử dụng :ref:`atan(vec_type y, vec_type x) <shader_func_atan2>`.

    :param y_over_x:Phân số cần trả về tan cung.

    :return:Tan cung lượng giác của ``y_over_x`` và nằm trong khoảng ``[-PI/2, PI/2]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/atan.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_atan2:

.. rst-class:: classref-method

|vec_type| **atan**\ (\ |vec_type| y, |vec_type| x) :ref:`🔗<shader_func_atan2>`

    |componentwise|

    Tính tan cung với tử số và mẫu số. Dấu của ``y`` và ``x`` được dùng để xác định góc nằm ở góc phần tư nào. Kết quả không xác định nếu ``x == 0``.

    Tương đương với :ref:`atan2() <class_@GlobalScope_method_atan2>` trong GDScript.

    :param y:Tử số của phân số cần trả về tan cung.

    :param x:Mẫu số của phân số cần trả về tan cung.

    :return:Tan cung lượng giác của ``y/x`` và nằm trong khoảng ``[-PI, PI]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/atan.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_sinh:

.. rst-class:: classref-method

|vec_type| **sinh**\ (\ |vec_type| x) :ref:`🔗<shader_func_sinh>`

    |componentwise|

    Tính sin hyperbolic bằng ``(e^x - e^-x)/2``.

    :param x:Giá trị cần trả về sin hyperbolic.

    :return:Sin hyperbolic của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sinh.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_cosh:

.. rst-class:: classref-method

|vec_type| **cosh**\ (\ |vec_type| x) :ref:`🔗<shader_func_cosh>`

    |componentwise|

    Tính cos hyperbolic bằng ``(e^x + e^-x)/2``.

    :param x:Giá trị cần trả về cos hyperbolic.

    :return:Cos hyperbolic của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/cosh.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_tanh:

.. rst-class:: classref-method

|vec_type| **tanh**\ (\ |vec_type| x) :ref:`🔗<shader_func_tanh>`

    |componentwise|

    Tính tan hyperbolic bằng ``sinh(x)/cosh(x)``.

    :param x:Giá trị cần trả về tan hyperbolic.

    :return:Tan hyperbolic của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/tanh.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_asinh:

.. rst-class:: classref-method

|vec_type| **asinh**\ (\ |vec_type| x) :ref:`🔗<shader_func_asinh>`

    |componentwise|

    Tính sin hyperbolic cung của ``x``, hay nghịch đảo của ``sinh``.

    :param x:Giá trị cần trả về sin hyperbolic cung.

    :return:Sin hyperbolic cung của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/asinh.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_acosh:

.. rst-class:: classref-method

|vec_type| **acosh**\ (\ |vec_type| x) :ref:`🔗<shader_func_acosh>`

    |componentwise|

    Tính cos hyperbolic cung của ``x``, hay nghịch đảo không âm của ``cosh``. Kết quả không xác định nếu ``x < 1``.

    :param x:Giá trị cần trả về cos hyperbolic cung.

    :return:Cos hyperbolic cung của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/acosh.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_atanh:

.. rst-class:: classref-method

|vec_type| **atanh**\ (\ |vec_type| x) :ref:`🔗<shader_func_atanh>`

    |componentwise|

    Tính tan hyperbolic cung của ``x``, hay nghịch đảo của ``tanh``. Kết quả không xác định nếu ``abs(x) > 1``.

    :param x:Giá trị cần trả về tan hyperbolic cung.

    :return:Tan hyperbolic cung của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/atanh.xhtml


.. rst-class:: classref-section-separator

----








.. rst-class:: classref-reftable-group

Các hàm mũ và toán học
----------------------

.. table::
    :class: nowrap-col2
    :widths: auto

    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    |    Return Type      | Function                                                                                           | Description / Return value                                      |
    +=====================+====================================================================================================+=================================================================+
    | |vec_type|          | :ref:`pow<shader_func_pow>`\ (\ |vec_type| x, |vec_type| y)                                        | Power (undefined if ``x < 0`` or if ``x == 0`` and ``y <= 0``). |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`exp<shader_func_exp>`\ (\ |vec_type| x)                                                      | Base-e exponential.                                             |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`exp2<shader_func_exp2>`\ (\ |vec_type| x)                                                    | Base-2 exponential.                                             |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`log<shader_func_log>`\ (\ |vec_type| x)                                                      | Natural (base-e) logarithm.                                     |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`log2<shader_func_log2>`\ (\ |vec_type| x)                                                    | Base-2 logarithm.                                               |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`sqrt<shader_func_sqrt>`\ (\ |vec_type| x)                                                    | Square root.                                                    |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`inversesqrt<shader_func_inversesqrt>`\ (\ |vec_type| x)                                      | Inverse square root.                                            |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`abs<shader_func_abs>`\ (\ |vec_type| x)                                                    | Absolute value (returns positive value if negative).            |
    | | |vec_int_type|    | | :ref:`abs<shader_func_abs>`\ (\ |vec_int_type| x)                                                |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`sign<shader_func_sign>`\ (\ |vec_type| x)                                                    | Returns ``1.0`` if positive, ``-1.0`` if negative,              |
    |                     |                                                                                                    | ``0.0`` otherwise.                                              |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_int_type|      | :ref:`sign<shader_func_sign>`\ (\ |vec_int_type| x)                                                | Returns ``1`` if positive, ``-1`` if negative,                  |
    |                     |                                                                                                    | ``0`` otherwise.                                                |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`floor<shader_func_floor>`\ (\ |vec_type| x)                                                  | Rounds to the integer below.                                    |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`round<shader_func_round>`\ (\ |vec_type| x)                                                  | Rounds to the nearest integer.                                  |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`roundEven<shader_func_roundEven>`\ (\ |vec_type| x)                                          | Rounds to the nearest even integer.                             |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`trunc<shader_func_trunc>`\ (\ |vec_type| x)                                                  | Truncation.                                                     |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`ceil<shader_func_ceil>`\ (\ |vec_type| x)                                                    | Rounds to the integer above.                                    |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`fract<shader_func_fract>`\ (\ |vec_type| x)                                                  | Fractional (returns ``x - floor(x)``).                          |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`mod<shader_func_mod>`\ (\ |vec_type| x, |vec_type| y)                                      | Modulo (division remainder).                                    |
    | | |vec_type|        | | :ref:`mod<shader_func_mod>`\ (\ |vec_type| x, float y)                                           |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`modf<shader_func_modf>`\ (\ |vec_type| x, out |vec_type| i)                                  | Fractional of ``x``, with ``i`` as integer part.                |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`min<shader_func_min>`\ (\ |vec_type| a, |vec_type| b)                                      | Lowest value between ``a`` and ``b``.                           |
    | | |vec_type|        | | :ref:`min<shader_func_min>`\ (\ |vec_type| a, float b)                                           |                                                                 |
    | | |vec_int_type|    | | :ref:`min<shader_func_min>`\ (\ |vec_int_type| a, |vec_int_type| b)                              |                                                                 |
    | | |vec_int_type|    | | :ref:`min<shader_func_min>`\ (\ |vec_int_type| a, int b)                                         |                                                                 |
    | | |vec_uint_type|   | | :ref:`min<shader_func_min>`\ (\ |vec_uint_type| a, |vec_uint_type| b)                            |                                                                 |
    | | |vec_uint_type|   | | :ref:`min<shader_func_min>`\ (\ |vec_uint_type| a, uint b)                                       |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`max<shader_func_max>`\ (\ |vec_type| a, |vec_type| b)                                      | Highest value between ``a`` and ``b``.                          |
    | | |vec_type|        | | :ref:`max<shader_func_max>`\ (\ |vec_type| a, float b)                                           |                                                                 |
    | | |vec_int_type|    | | :ref:`max<shader_func_max>`\ (\ |vec_int_type| a, |vec_int_type| b)                              |                                                                 |
    | | |vec_int_type|    | | :ref:`max<shader_func_max>`\ (\ |vec_int_type| a, int b)                                         |                                                                 |
    | | |vec_uint_type|   | | :ref:`max<shader_func_max>`\ (\ |vec_uint_type| a, |vec_uint_type| b)                            |                                                                 |
    | | |vec_uint_type|   | | :ref:`max<shader_func_max>`\ (\ |vec_uint_type| a, uint b)                                       |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`clamp<shader_func_clamp>`\ (\ |vec_type| x, |vec_type| min, |vec_type| max)                | Clamps ``x`` between ``min`` and ``max`` (inclusive).           |
    | | |vec_type|        | | :ref:`clamp<shader_func_clamp>`\ (\ |vec_type| x, float min, float max)                          |                                                                 |
    | | |vec_int_type|    | | :ref:`clamp<shader_func_clamp>`\ (\ |vec_int_type| x, |vec_int_type| min, |vec_int_type| max)    |                                                                 |
    | | |vec_int_type|    | | :ref:`clamp<shader_func_clamp>`\ (\ |vec_int_type| x, int min, int max)                          |                                                                 |
    | | |vec_uint_type|   | | :ref:`clamp<shader_func_clamp>`\ (\ |vec_uint_type| x, |vec_uint_type| min, |vec_uint_type| max) |                                                                 |
    | | |vec_uint_type|   | | :ref:`clamp<shader_func_clamp>`\ (\ |vec_uint_type| x, uint min, uint max)                       |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`mix<shader_func_mix>`\ (\ |vec_type| a, |vec_type| b, |vec_type| c)                        | Linear interpolate between ``a`` and ``b`` by ``c``.            |
    | | |vec_type|        | | :ref:`mix<shader_func_mix>`\ (\ |vec_type| a, |vec_type| b, float c)                             |                                                                 |
    | | |vec_type|        | | :ref:`mix<shader_func_mix>`\ (\ |vec_type| a, |vec_type| b, |vec_bool_type| c)                   |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`fma<shader_func_fma>`\ (\ |vec_type| a, |vec_type| b, |vec_type| c)                          | Fused multiply-add operation: ``(a * b + c)``                   |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`step<shader_func_step>`\ (\ |vec_type| a, |vec_type| b)                                    | ``b < a ? 0.0 : 1.0``                                           |
    | | |vec_type|        | | :ref:`step<shader_func_step>`\ (\ float a, |vec_type| b)                                         |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | | |vec_type|        | | :ref:`smoothstep<shader_func_smoothstep>`\ (\ |vec_type| a, |vec_type| b, |vec_type| c)          | Hermite interpolate between ``a`` and ``b`` by ``c``.           |
    | | |vec_type|        | | :ref:`smoothstep<shader_func_smoothstep>`\ (\ float a, float b, |vec_type| c)                    |                                                                 |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_bool_type|     | :ref:`isnan<shader_func_isnan>`\ (\ |vec_type| x)                                                  | Returns ``true`` if scalar or vector component is ``NaN``.      |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_bool_type|     | :ref:`isinf<shader_func_isinf>`\ (\ |vec_type| x)                                                  | Returns ``true`` if scalar or vector component is ``INF``.      |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_int_type|      | :ref:`floatBitsToInt<shader_func_floatBitsToInt>`\ (\ |vec_type| x)                                | ``float`` to ``int`` bit copying, no conversion.                |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_uint_type|     | :ref:`floatBitsToUint<shader_func_floatBitsToUint>`\ (\ |vec_type| x)                              | ``float`` to ``uint`` bit copying, no conversion.               |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`intBitsToFloat<shader_func_intBitsToFloat>`\ (\ |vec_int_type| x)                            | ``int`` to ``float`` bit copying, no conversion.                |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+
    | |vec_type|          | :ref:`uintBitsToFloat<shader_func_uintBitsToFloat>`\ (\ |vec_uint_type| x)                         | ``uint`` to ``float`` bit copying, no conversion.               |
    +---------------------+----------------------------------------------------------------------------------------------------+-----------------------------------------------------------------+


.. rst-class:: classref-descriptions-group

Mô tả các hàm mũ và toán học
~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. _shader_func_pow:

.. rst-class:: classref-method

|vec_type| **pow**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_pow>`

    |componentwise|

    Nâng ``x`` lên lũy thừa ``y``.

    Kết quả không xác định nếu ``x < 0`` hoặc nếu ``x == 0`` và ``y <= 0``.

    :param x:Giá trị được nâng lên lũy thừa ``y``.

    :param y:Lũy thừa mà ``x`` sẽ được nâng lên.

    :return:Giá trị của ``x`` được nâng lên lũy thừa ``y``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/pow.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_exp:

.. rst-class:: classref-method

|vec_type| **exp**\ (\ |vec_type| x) :ref:`🔗<shader_func_exp>`

    |componentwise|

    Nâng ``e`` lên lũy thừa ``x``, hay phép lũy thừa tự nhiên.

    Tương đương với ``pow(e, x)``.

    :param x:Giá trị cần lũy thừa hóa.

    :return:Phép lũy thừa tự nhiên của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/exp.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_exp2:

.. rst-class:: classref-method

|vec_type| **exp2**\ (\ |vec_type| x) :ref:`🔗<shader_func_exp2>`

    |componentwise|

    Nâng ``2`` lên lũy thừa ``x``.

    Tương đương với ``pow(2.0, x)``.


    :param x:Giá trị của lũy thừa mà ``2`` sẽ được nâng lên.

    :return:``2`` được nâng lên lũy thừa ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/exp2.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_log:

.. rst-class:: classref-method

|vec_type| **log**\ (\ |vec_type| x) :ref:`🔗<shader_func_log>`

    |componentwise|

    Trả về logarit tự nhiên của ``x``, tức là giá trị ``y`` thỏa mãn ``x == pow(e, y)``. Kết quả không xác định nếu ``x <= 0``.

    :param x:Giá trị cần lấy logarit tự nhiên.

    :return:Logarit tự nhiên của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/log.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_log2:

.. rst-class:: classref-method

|vec_type| **log2**\ (\ |vec_type| x) :ref:`🔗<shader_func_log2>`

    |componentwise|

    Trả về logarit cơ số 2 của ``x``, tức là giá trị ``y`` thỏa mãn ``x == pow(2, y)``. Kết quả không xác định nếu ``x <= 0``.

    :param x:Giá trị cần lấy logarit cơ số 2.

    :return:Logarit cơ số 2 của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/log2.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_sqrt:

.. rst-class:: classref-method

|vec_type| **sqrt**\ (\ |vec_type| x) :ref:`🔗<shader_func_sqrt>`

    |componentwise|

    Trả về căn bậc hai của ``x``. Kết quả không xác định nếu ``x < 0``.

    :param x:Giá trị cần lấy căn bậc hai.

    :return:Căn bậc hai của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sqrt.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_inversesqrt:

.. rst-class:: classref-method

|vec_type| **inversesqrt**\ (\ |vec_type| x) :ref:`🔗<shader_func_inversesqrt>`

    |componentwise|

    Trả về nghịch đảo của căn bậc hai của ``x``, hoặc ``1.0 / sqrt(x)``. Kết quả không xác định nếu ``x <= 0``.

    :param x:Giá trị cần lấy nghịch đảo căn bậc hai.

    :return:Nghịch đảo của căn bậc hai của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/inversesqrt.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_abs:

.. rst-class:: classref-method

|vec_type| **abs**\ (\ |vec_type| x) :ref:`🔗<shader_func_abs>`

.. rst-class:: classref-method

|vec_int_type| **abs**\ (\ |vec_int_type| x) :ref:`🔗<shader_func_abs>`

    |componentwise|

    Trả về giá trị tuyệt đối của ``x``. Trả về ``x`` nếu ``x`` dương, nếu không thì trả về ``-1 * x``.

    :param x:Giá trị cần trả về giá trị tuyệt đối.

    :return:Giá trị tuyệt đối của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/abs.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_sign:

.. rst-class:: classref-method

|vec_type| **sign**\ (\ |vec_type| x) :ref:`🔗<shader_func_sign>`

.. rst-class:: classref-method

|vec_int_type| **sign**\ (\ |vec_int_type| x) :ref:`🔗<shader_func_sign>`

    |componentwise|

    Trả về ``-1`` nếu ``x < 0``, ``0`` nếu ``x == 0``, và ``1`` nếu ``x > 0``.

    :param x:Giá trị cần lấy dấu.

    :return:Dấu của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/sign.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_floor:

.. rst-class:: classref-method

|vec_type| **floor**\ (\ |vec_type| x) :ref:`🔗<shader_func_floor>`

    |componentwise|

    Trả về một giá trị bằng số nguyên gần nhất nhỏ hơn hoặc bằng ``x``.

    :param x:Giá trị cần làm tròn xuống.

    :return:Số nguyên gần nhất nhỏ hơn hoặc bằng ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/floor.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_round:

.. rst-class:: classref-method

|vec_type| **round**\ (\ |vec_type| x) :ref:`🔗<shader_func_round>`

    |componentwise|

    Làm tròn ``x`` đến số nguyên gần nhất.

    .. note::
        Việc làm tròn các giá trị có phần thập phân là ``0.5`` phụ thuộc vào cách triển khai. Điều này bao gồm khả năng ``round(x)`` trả về cùng giá trị với ``roundEven(x)`` cho mọi giá trị của ``x``.

    :param x:Giá trị cần làm tròn.

    :return:Giá trị đã làm tròn.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/round.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_roundEven:

.. rst-class:: classref-method

|vec_type| **roundEven**\ (\ |vec_type| x) :ref:`🔗<shader_func_roundEven>`

    |componentwise|

    Làm tròn ``x`` đến số nguyên gần nhất. Một giá trị có phần thập phân là ``0.5`` sẽ luôn được làm tròn về số nguyên chẵn gần nhất. Ví dụ, cả ``3.5`` và ``4.5`` đều được làm tròn thành ``4.0``.

    :param x:Giá trị cần làm tròn.

    :return:Giá trị đã làm tròn.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/roundEven.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_trunc:

.. rst-class:: classref-method

|vec_type| **trunc**\ (\ |vec_type| x) :ref:`🔗<shader_func_trunc>`

    |componentwise|

    Cắt bỏ phần thập phân của ``x``. Trả về một giá trị bằng số nguyên gần nhất với ``x`` có giá trị tuyệt đối không lớn hơn giá trị tuyệt đối của ``x``.

    :param x:Giá trị cần đánh giá.

    :return:Giá trị sau khi cắt bỏ phần thập phân.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/trunc.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_ceil:

.. rst-class:: classref-method

|vec_type| **ceil**\ (\ |vec_type| x) :ref:`🔗<shader_func_ceil>`

    |componentwise|

    Trả về một giá trị bằng số nguyên gần nhất lớn hơn hoặc bằng ``x``.

    :param x:Giá trị cần đánh giá.

    :return:Giá trị làm tròn lên.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/ceil.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_fract:

.. rst-class:: classref-method

|vec_type| **fract**\ (\ |vec_type| x) :ref:`🔗<shader_func_fract>`

    |componentwise|

    Trả về phần thập phân của ``x``.

    Giá trị này được tính là ``x - floor(x)``.

    :param x:Giá trị cần đánh giá.

    :return:Phần thập phân của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fract.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_mod:

.. rst-class:: classref-method

|vec_type| **mod**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_mod>`

.. rst-class:: classref-method

|vec_type| **mod**\ (\ |vec_type| x, float y) :ref:`🔗<shader_func_mod>`

    |componentwise|

    Trả về giá trị của ``x modulo y``. Giá trị này đôi khi còn được gọi là phần dư.

    Giá trị này được tính là ``x - y * floor(x/y)``.

    :param x:Giá trị cần đánh giá.

    :return:Giá trị của ``x modulo y``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mod.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_modf:

.. rst-class:: classref-method

|vec_type| **modf**\ (\ |vec_type| x, out |vec_type| i) :ref:`🔗<shader_func_modf>`

    |componentwise|

    Tách giá trị dấu phẩy động ``x`` thành phần nguyên và phần thập phân.

    Phần thập phân của số được hàm trả về. Phần nguyên (dưới dạng giá trị dấu phẩy động) được trả về trong tham số đầu ra ``i``.

    :param x:Giá trị cần tách.

    :param out i:Biến nhận phần nguyên của ``x``.

    :return:Phần thập phân của số.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/modf.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_min:

.. rst-class:: classref-method

|vec_type| **min**\ (\ |vec_type| a, |vec_type| b) :ref:`🔗<shader_func_min>`

.. rst-class:: classref-method

|vec_type| **min**\ (\ |vec_type| a, float b) :ref:`🔗<shader_func_min>`

.. rst-class:: classref-method

|vec_int_type| **min**\ (\ |vec_int_type| a, |vec_int_type| b) :ref:`🔗<shader_func_min>`

.. rst-class:: classref-method

|vec_int_type| **min**\ (\ |vec_int_type| a, int b) :ref:`🔗<shader_func_min>`

.. rst-class:: classref-method

|vec_uint_type| **min**\ (\ |vec_uint_type| a, |vec_uint_type| b) :ref:`🔗<shader_func_min>`

.. rst-class:: classref-method

|vec_uint_type| **min**\ (\ |vec_uint_type| a, uint b) :ref:`🔗<shader_func_min>`

    |componentwise|

    Trả về giá trị nhỏ nhất trong hai giá trị ``a`` và ``b``.

    Trả về ``b`` nếu ``b < a``, nếu không thì trả về ``a``.

    :param a:Giá trị đầu tiên cần so sánh.

    :param b:Giá trị thứ hai cần so sánh.

    :return:Giá trị nhỏ nhất.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/min.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_max:

.. rst-class:: classref-method

|vec_type| **max**\ (\ |vec_type| a, |vec_type| b) :ref:`🔗<shader_func_max>`

.. rst-class:: classref-method

|vec_type| **max**\ (\ |vec_type| a, float b) :ref:`🔗<shader_func_max>`

.. rst-class:: classref-method

|vec_uint_type| **max**\ (\ |vec_uint_type| a, |vec_uint_type| b) :ref:`🔗<shader_func_max>`

.. rst-class:: classref-method

|vec_uint_type| **max**\ (\ |vec_uint_type| a, uint b) :ref:`🔗<shader_func_max>`

.. rst-class:: classref-method

|vec_int_type| **max**\ (\ |vec_int_type| a, |vec_int_type| b) :ref:`🔗<shader_func_max>`

.. rst-class:: classref-method

|vec_int_type| **max**\ (\ |vec_int_type| a, int b) :ref:`🔗<shader_func_max>`

    |componentwise|

    Trả về giá trị lớn nhất trong hai giá trị ``a`` và ``b``.

    Trả về ``b`` nếu ``b > a``, nếu không thì trả về ``a``.

    :param a:Giá trị đầu tiên cần so sánh.

    :param b:Giá trị thứ hai cần so sánh.

    :return:Giá trị lớn nhất.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/max.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_clamp:

.. rst-class:: classref-method

|vec_type| **clamp**\ (\ |vec_type| x, |vec_type| minVal, |vec_type| maxVal) :ref:`🔗<shader_func_clamp>`

.. rst-class:: classref-method

|vec_type| **clamp**\ (\ |vec_type| x, float minVal, float maxVal) :ref:`🔗<shader_func_clamp>`

.. rst-class:: classref-method

|vec_int_type| **clamp**\ (\ |vec_int_type| x, |vec_int_type| minVal, |vec_int_type| maxVal) :ref:`🔗<shader_func_clamp>`

.. rst-class:: classref-method

|vec_int_type| **clamp**\ (\ |vec_int_type| x, int minVal, int maxVal) :ref:`🔗<shader_func_clamp>`

.. rst-class:: classref-method

|vec_uint_type| **clamp**\ (\ |vec_uint_type| x, |vec_uint_type| minVal, |vec_uint_type| maxVal) :ref:`🔗<shader_func_clamp>`

.. rst-class:: classref-method

|vec_uint_type| **clamp**\ (\ |vec_uint_type| x, uint minVal, uint maxVal) :ref:`🔗<shader_func_clamp>`

    |componentwise|

    Trả về giá trị của ``x`` bị giới hạn trong khoảng từ ``minVal`` đến ``maxVal``.

    Giá trị trả về được tính là ``min(max(x, minVal), maxVal)``.

    :param x:Giá trị cần giới hạn.

    :param minVal:Đầu dưới của khoảng dùng để giới hạn ``x``.

    :param maxVal:Đầu trên của khoảng dùng để giới hạn ``x``.

    :return:Giá trị đã được giới hạn.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/clamp.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_mix:

.. rst-class:: classref-method

|vec_type| **mix**\ (\ |vec_type| a, |vec_type| b, |vec_type| c) :ref:`🔗<shader_func_mix>`

.. rst-class:: classref-method

|vec_type| **mix**\ (\ |vec_type| a, |vec_type| b, float c) :ref:`🔗<shader_func_mix>`

    |componentwise|

    Thực hiện nội suy tuyến tính giữa ``a`` và ``b``, sử dụng ``c`` để xác định trọng số giữa chúng.

    Được tính là ``a * (1 - c) + b * c``.

    Tương đương với :ref:`lerp() <class_@GlobalScope_method_lerp>` trong GDScript.

    :param a:Điểm bắt đầu của khoảng cần nội suy.

    :param b:Điểm kết thúc của khoảng cần nội suy.

    :param c:Giá trị dùng để nội suy giữa ``a`` và ``b``.

    :return:Giá trị đã nội suy.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mix.xhtml

.. rst-class:: classref-item-separator

----


.. rst-class:: classref-method

|vec_type| **mix**\ (\ |vec_type| a, |vec_type| b, |vec_bool_type| c) :ref:`🔗<shader_func_mix>`

    Chọn giá trị ``a`` hoặc giá trị ``b`` dựa trên giá trị của ``c``. Đối với một thành phần của ``c`` có giá trị false, thành phần tương ứng của ``a`` được trả về. Đối với một thành phần của ``c`` có giá trị true, thành phần tương ứng của ``b`` được trả về. Các thành phần của ``a`` và ``b`` không được chọn có thể là các giá trị dấu phẩy động không hợp lệ và sẽ không ảnh hưởng đến kết quả.

    Nếu ``a``, ``b`` và ``c`` là các kiểu vector, phép toán được thực hiện :ref:`theo từng thành phần <shading_componentwise>`. Ví dụ, ``mix(vec2(42, 314), vec2(9.8, 6e23), bvec2(true, false)))`` sẽ trả về ``vec2(9.8, 314)``.

    :param a:Giá trị được trả về khi ``c`` là false.

    :param b:Giá trị được trả về khi ``c`` là true.

    :param c:Giá trị được dùng để chọn giữa ``a`` và ``b``.

    :return:Giá trị đã nội suy.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/mix.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_fma:

.. rst-class:: classref-method

|vec_type| **fma**\ (\ |vec_type| a, |vec_type| b, |vec_type| c) :ref:`🔗<shader_func_fma>`

    |componentwise|

    Thực hiện phép toán fused multiply-add nếu có thể, trả về ``a * b + c``. Trong các trường hợp sử dụng mà giá trị trả về cuối cùng được một biến khai báo là precise sử dụng:

     - ``fma()`` được xem là một phép toán đơn, trong khi biểu thức ``a * b + c`` được một biến khai báo là precise sử dụng được xem là hai phép toán.

     - Độ chính xác của ``fma()`` có thể khác với độ chính xác của biểu thức ``a * b + c``.

     - ``fma()`` sẽ được tính với cùng độ chính xác như bất kỳ ``fma()`` nào khác được một biến precise sử dụng, cho kết quả bất biến với cùng các giá trị đầu vào của a, b và c.

    Nếu không có việc sử dụng bởi precise, sẽ không có ràng buộc đặc biệt nào về số lượng phép toán hoặc sự khác biệt về độ chính xác giữa ``fma()`` và biểu thức ``a * b + c``.

    :param a:Giá trị đầu tiên được nhân.

    :param b:Giá trị thứ hai được nhân.

    :param c:Giá trị được cộng vào kết quả.

    :return:Giá trị của ``a * b + c``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fma.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_step:

.. rst-class:: classref-method

|vec_type| **step**\ (\ |vec_type| a, |vec_type| b) :ref:`🔗<shader_func_step>`

.. rst-class:: classref-method

|vec_type| **step**\ (\ float a, |vec_type| b) :ref:`🔗<shader_func_step>`

    |componentwise|

    Tạo một hàm step bằng cách so sánh b với a.

    Tương đương với ``if (b < a) { return 0.0; } else { return 1.0; }``. Đối với phần tử i của giá trị trả về, 0.0 được trả về nếu b[i] < a[i], và 1.0 được trả về trong các trường hợp khác.

    :param a:Vị trí của cạnh của hàm step.

    :param b:Giá trị được dùng để tạo hàm step.

    :return:``0.0`` hoặc ``1.0``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/step.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_smoothstep:

.. rst-class:: classref-method

|vec_type| **smoothstep**\ (\ |vec_type| a, |vec_type| b, |vec_type| c) :ref:`🔗<shader_func_smoothstep>`

.. rst-class:: classref-method

|vec_type| **smoothstep**\ (\ float a, float b, |vec_type| c) :ref:`🔗<shader_func_smoothstep>`

    |componentwise|

    Thực hiện phép nội suy Hermite mượt giữa ``0`` và ``1`` khi a < c < b. Điều này hữu ích trong các trường hợp cần một hàm ngưỡng có chuyển tiếp mượt.

    Smoothstep tương đương với:

    ::

        vec_type t;
        t = clamp((c - a) / (b - a), 0.0, 1.0);
        return t * t * (3.0 - 2.0 * t);

    Kết quả không được xác định nếu ``a >= b``.

    :param a:Giá trị của cạnh dưới của hàm Hermite.

    :param b:Giá trị của cạnh trên của hàm Hermite.

    :param c:Giá trị nguồn dùng cho phép nội suy.

    :return:Giá trị đã nội suy.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/smoothstep.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_isnan:

.. rst-class:: classref-method

|vec_bool_type| **isnan**\ (\ |vec_type| x) :ref:`🔗<shader_func_isnan>`

    |componentwise|

    Đối với mỗi phần tử i của kết quả, trả về ``true`` nếu x[i] là NaN dấu phẩy động dương hoặc âm (Not a Number), và false trong các trường hợp khác.

    :param x:Giá trị cần kiểm tra NaN.

    :return:``true`` hoặc ``false``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/isnan.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_isinf:

.. rst-class:: classref-method

|vec_bool_type| **isinf**\ (\ |vec_type| x) :ref:`🔗<shader_func_isinf>`

    |componentwise|

    Đối với mỗi phần tử i của kết quả, trả về ``true`` nếu x[i] là vô cực dấu phẩy động dương hoặc âm, và false trong các trường hợp khác.

    :param x:Giá trị cần kiểm tra vô cực.

    :return:``true`` hoặc ``false``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/isinf.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_floatBitsToInt:

.. rst-class:: classref-method

|vec_int_type| **floatBitsToInt**\ (\ |vec_type| x) :ref:`🔗<shader_func_floatBitsToInt>`

    |componentwise|

    Trả về phần mã hóa của các tham số dấu phẩy động dưới dạng ``int``.

    Biểu diễn cấp bit dấu phẩy động được bảo toàn.

    :param x:Giá trị có phần mã hóa dấu phẩy động cần được trả về.

    :return:Phần mã hóa dấu phẩy động của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/floatBitsToInt.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_floatBitsToUint:

.. rst-class:: classref-method

|vec_uint_type| **floatBitsToUint**\ (\ |vec_type| x) :ref:`🔗<shader_func_floatBitsToUint>`

    |componentwise|

    Trả về phần mã hóa của các tham số dấu phẩy động dưới dạng ``uint``.

    Biểu diễn cấp bit dấu phẩy động được bảo toàn.

    :param x:Giá trị có phần mã hóa dấu phẩy động cần được trả về.

    :return:Phần mã hóa dấu phẩy động của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/floatBitsToInt.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_intBitsToFloat:

.. rst-class:: classref-method

|vec_type| **intBitsToFloat**\ (\ |vec_int_type| x) :ref:`🔗<shader_func_intBitsToFloat>`

    |componentwise|

    Chuyển đổi một phần mã hóa bit thành giá trị dấu phẩy động. Ngược lại với `floatBitsToInt<shader_func_floatBitsToInt>`

    Nếu phần mã hóa của một ``NaN`` được truyền vào ``x``, nó sẽ không phát tín hiệu và giá trị kết quả sẽ không được xác định.

    Nếu phần mã hóa của một vô cực dấu phẩy động được truyền vào tham số ``x``, giá trị dấu phẩy động kết quả là vô cực dấu phẩy động tương ứng (dương hoặc âm).

    :param x:Phần mã hóa bit cần được trả về dưới dạng giá trị dấu phẩy động.

    :return:Một giá trị dấu phẩy động.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/intBitsToFloat.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_uintBitsToFloat:

.. rst-class:: classref-method

|vec_type| **uintBitsToFloat**\ (\ |vec_uint_type| x) :ref:`🔗<shader_func_uintBitsToFloat>`

    |componentwise|

    Chuyển đổi một phần mã hóa bit thành giá trị dấu phẩy động. Ngược lại với `floatBitsToUint<shader_func_floatBitsToUint>`

    Nếu phần mã hóa của một ``NaN`` được truyền vào ``x``, nó sẽ không phát tín hiệu và giá trị kết quả sẽ không được xác định.

    Nếu phần mã hóa của một vô cực dấu phẩy động được truyền vào tham số ``x``, giá trị dấu phẩy động kết quả là vô cực dấu phẩy động tương ứng (dương hoặc âm).

    :param x:Phần mã hóa bit cần được trả về dưới dạng giá trị dấu phẩy động.

    :return:Một giá trị dấu phẩy động.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/intBitsToFloat.xhtml


.. rst-class:: classref-section-separator

----



















.. rst-class:: classref-reftable-group

Các hàm hình học
----------------

.. table::
    :class: nowrap-col2
    :widths: auto

    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | float      | :ref:`length <shader_func_length>`\ (\ |vec_type| x)                                          | Độ dài vector.                                                       |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | float      | :ref:`distance <shader_func_distance>`\ (\ |vec_type| a, |vec_type| b)                        | Khoảng cách giữa các vector, tức là ``length(a - b)``.               |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | float      | :ref:`dot <shader_func_dot>`\ (\ |vec_type| a, |vec_type| b)                                  | Tích vô hướng.                                                       |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | vec3       | :ref:`cross <shader_func_cross>`\ (\ vec3 a, vec3 b)                                          | Tích có hướng.                                                       |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | |vec_type| | :ref:`normalize <shader_func_normalize>`\ (\ |vec_type| x)                                    | Chuẩn hóa về độ dài đơn vị.                                          |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | vec3       | :ref:`reflect <shader_func_reflect>`\ (\ vec3 I, vec3 N)                                      | Phản xạ.                                                             |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | vec3       | :ref:`refract <shader_func_refract>`\ (\ vec3 I, vec3 N, float eta)                           | Khúc xạ.                                                             |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | |vec_type| | :ref:`faceforward <shader_func_faceforward>`\ (\ |vec_type| N, |vec_type| I, |vec_type| Nref) | Nếu ``dot(Nref, I) < 0``, trả về ``N``; nếu không thì trả về ``-N``. |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | |mat_type| | :ref:`matrixCompMult <shader_func_matrixCompMult>`\ (\ |mat_type| x, |mat_type| y)            | Phép nhân từng thành phần của ma trận.                               |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | |mat_type| | :ref:`outerProduct <shader_func_outerProduct>`\ (\ |vec_type| column, |vec_type| row)         | Tích ngoài của ma trận.                                              |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | |mat_type| | :ref:`transpose <shader_func_transpose>`\ (\ |mat_type| m)                                    | Ma trận chuyển vị.                                                   |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | float      | :ref:`determinant <shader_func_determinant>`\ (\ |mat_type| m)                                | Định thức ma trận.                                                   |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+
    | |mat_type| | :ref:`inverse <shader_func_inverse>`\ (\ |mat_type| m)                                        | Ma trận nghịch đảo.                                                  |
    +------------+-----------------------------------------------------------------------------------------------+----------------------------------------------------------------------+


.. rst-class:: classref-descriptions-group

Mô tả các hàm hình học
~~~~~~~~~~~~~~~~~~~~~~


.. _shader_func_length:

.. rst-class:: classref-method

float **length**\ (\ |vec_type| x) :ref:`🔗<shader_func_length>`

    Trả về độ dài của vector, tức là ``sqrt(x[0] * x[0] + x[1] * x[1] + ... + x[n] * x[n])``

    :param x:Vector

    :return:Độ dài của vector.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/length.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_distance:

.. rst-class:: classref-method

float **distance**\ (\ |vec_type| a, |vec_type| b) :ref:`🔗<shader_func_distance>`

    Trả về khoảng cách giữa hai điểm ``a`` và ``b``, tức là ``length(b - a);``

    :param a:Điểm thứ nhất.

    :param b:Điểm thứ hai.

    :return:Khoảng cách vô hướng giữa các điểm

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/distance.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_dot:

.. rst-class:: classref-method

float **dot**\ (\ |vec_type| a, |vec_type| b) :ref:`🔗<shader_func_dot>`

    Trả về tích vô hướng của hai vector, ``a`` và ``b``, tức là ``a.x * b.x + a.y * b.y + ...``

    :param a:Vector thứ nhất.

    :param b:Vector thứ hai.

    :return:Tích vô hướng.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/dot.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_cross:

.. rst-class:: classref-method

vec3 **cross**\ (\ vec3 a, vec3 b) :ref:`🔗<shader_func_cross>`

    Trả về tích có hướng của hai vector, tức là:

    .. code-block:: glsl

        vec3( a.y * b.z - b.y * a.z,
              a.z * b.x - b.z * a.x,
              a.x * b.y - b.x * a.y)

    :param a:Vector thứ nhất.

    :param b:Vector thứ hai.

    :return:Tích có hướng của ``a`` và ``b``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/cross.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_normalize:

.. rst-class:: classref-method

|vec_type| **normalize**\ (\ |vec_type| x) :ref:`🔗<shader_func_normalize>`

    Trả về một vector có cùng hướng với ``x`` nhưng có độ dài ``1.0``.

    :param x:Vector cần chuẩn hóa.

    :return:Vector đã chuẩn hóa.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/normalize.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_reflect:

.. rst-class:: classref-method

vec3 **reflect**\ (\ vec3 I, vec3 N) :ref:`🔗<shader_func_reflect>`

    Tính hướng phản xạ của một vector tới.

    Với vector tới ``I`` và pháp tuyến bề mặt ``N`` đã cho, reflect trả về hướng phản xạ được tính bằng ``I - 2.0 * dot(N, I) * N``.

    .. Note::
        ``N`` phải được chuẩn hóa để đạt được kết quả mong muốn.

    :param I:Vector tới.

    :param N:Vector pháp tuyến.

    :return:Vector phản xạ.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/reflect.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_refract:

.. rst-class:: classref-method

vec3 **refract**\ (\ vec3 I, vec3 N, float eta) :ref:`🔗<shader_func_refract>`

    Tính hướng khúc xạ cho một vector tới.

    Với một vector tới ``I``, pháp tuyến bề mặt ``N`` và tỷ số chiết suất ``eta``, refract trả về vector khúc xạ ``R``.

    ``R`` được tính như sau:

    .. code-block:: glsl

        k = 1.0 - eta * eta * (1.0 - dot(N, I) * dot(N, I));
        if (k < 0.0)
            R = genType(0.0);       // hoặc genDType(0.0)
        else
            R = eta * I - (eta * dot(N, I) + sqrt(k)) * N;

    .. Note::
        Các tham số đầu vào I và N phải được chuẩn hóa để đạt được kết quả mong muốn.

    :param I:Vector tới.

    :param N:Vector pháp tuyến.

    :param eta:Tỷ số chiết suất.

    :return:Vector khúc xạ.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/refract.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_faceforward:

.. rst-class:: classref-method

|vec_type| **faceforward**\ (\ |vec_type| N, |vec_type| I, |vec_type| Nref) :ref:`🔗<shader_func_faceforward>`

    Trả về một vector hướng cùng hướng với một vector khác.

    Định hướng một vector để hướng ra xa bề mặt theo định nghĩa của pháp tuyến bề mặt. Nếu ``dot(Nref, I) < 0`` faceforward trả về ``N``, nếu không, hàm trả về ``-N``.

    :param N:Vector cần định hướng.

    :param I:Vector tới.

    :param Nref:Vector tham chiếu.

    :return:Vector đã định hướng.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/faceforward.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_matrixCompMult:

.. rst-class:: classref-method

|mat_type| **matrixCompMult**\ (\ |mat_type| x, |mat_type| y) :ref:`🔗<shader_func_matrixCompMult>`

    Thực hiện phép nhân :ref:`theo từng thành phần <shading_componentwise>` của hai ma trận.

    Thực hiện phép nhân hai ma trận theo từng thành phần, tạo ra một ma trận kết quả trong đó mỗi thành phần, ``result[i][j]``, được tính là tích vô hướng của ``x[i][j]`` và ``y[i][j]``.

    :param x:Toán hạng ma trận thứ nhất.

    :param y:Toán hạng ma trận thứ hai.

    :return:Ma trận kết quả.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/matrixCompMult.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_outerProduct:

.. rst-class:: classref-method

|mat_type| **outerProduct**\ (\ |vec_type| column, |vec_type| row) :ref:`🔗<shader_func_outerProduct>`

    Tính tích ngoài của một cặp vector.

    Thực hiện phép nhân ma trận đại số tuyến tính ``column * row``, tạo ra một ma trận có số hàng bằng số thành phần trong ``column`` và số cột bằng số thành phần trong ``row``.

    :param column:Vector cột dùng cho phép nhân.

    :param row:Vector hàng dùng cho phép nhân.

    :return:Ma trận tích ngoài.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/outerProduct.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_transpose:

.. rst-class:: classref-method

|mat_type| **transpose**\ (\ |mat_type| m) :ref:`🔗<shader_func_transpose>`

    Tính ma trận chuyển vị.

    :param m:Ma trận cần chuyển vị.

    :return:Một ma trận mới là ma trận chuyển vị của ma trận đầu vào ``m``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/transpose.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_determinant:

.. rst-class:: classref-method

float **determinant**\ (\ |mat_type| m) :ref:`🔗<shader_func_determinant>`

    Tính định thức của một ma trận.

    :param m:Ma trận.

    :return:Định thức của ma trận đầu vào ``m``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/determinant.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_inverse:

.. rst-class:: classref-method

|mat_type| **inverse**\ (\ |mat_type| m) :ref:`🔗<shader_func_inverse>`

    Tính ma trận nghịch đảo.

    Các giá trị trong ma trận trả về không được xác định nếu ``m`` là ma trận suy biến hoặc điều kiện kém (gần suy biến).

    :param m:Ma trận cần lấy nghịch đảo.

    :return:Một ma trận mới là ma trận nghịch đảo của ma trận đầu vào ``m``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/inverse.xhtml

.. rst-class:: classref-section-separator

----













.. rst-class:: classref-reftable-group

Các hàm so sánh
---------------

.. table::
    :class: nowrap-col2
    :widths: auto

    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`lessThan <shader_func_lessThan>`\ (\ |vec_type| x, |vec_type| y)                  | So sánh vector Bool trên các vector int/uint/float với <.                   |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`greaterThan <shader_func_greaterThan>`\ (\ |vec_type| x, |vec_type| y)            | So sánh vector Bool trên các vector int/uint/float với >.                   |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`lessThanEqual <shader_func_lessThanEqual>`\ (\ |vec_type| x, |vec_type| y)        | So sánh vector Bool trên các vector int/uint/float với <=.                  |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`greaterThanEqual <shader_func_greaterThanEqual>`\ (\  |vec_type| x, |vec_type| y) | So sánh vector Bool trên các vector int/uint/float với >=.                  |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`equal <shader_func_equal>`\ (\ |vec_type| x, |vec_type| y)                        | So sánh vector Bool trên các vector int/uint/float với ==.                  |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`notEqual <shader_func_notEqual>`\ (\ |vec_type| x, |vec_type| y)                  | So sánh vector Bool trên các vector int/uint/float với !=.                  |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | bool            | :ref:`any <shader_func_any>`\ (\ |vec_bool_type| x)                                     | ``true`` nếu bất kỳ thành phần nào là ``true``, ngược lại là ``false``.     |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | bool            | :ref:`all <shader_func_all>`\ (\ |vec_bool_type| x)                                     | ``true`` nếu tất cả các thành phần đều là ``true``, ngược lại là ``false``. |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+
    | |vec_bool_type| | :ref:`not <shader_func_not>`\ (\ |vec_bool_type| x)                                     | Đảo ngược vector boolean.                                                   |
    +-----------------+-----------------------------------------------------------------------------------------+-----------------------------------------------------------------------------+


.. rst-class:: classref-descriptions-group

Mô tả các hàm so sánh
~~~~~~~~~~~~~~~~~~~~~


.. _shader_func_lessThan:

.. rst-class:: classref-method

|vec_bool_type| **lessThan**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_lessThan>`

    Thực hiện phép so sánh nhỏ hơn :ref:`theo từng thành phần <shading_componentwise>` giữa hai vector.

    :param x:Vector đầu tiên cần so sánh.

    :param y:Vector thứ hai cần so sánh.

    :return:Một vector boolean trong đó mỗi phần tử ``i`` được tính là ``x[i] < y[i]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/lessThan.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_greaterThan:

.. rst-class:: classref-method

|vec_bool_type| **greaterThan**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_greaterThan>`

    Thực hiện phép so sánh lớn hơn :ref:`theo từng thành phần <shading_componentwise>` giữa hai vector.

    :param x:Vector đầu tiên cần so sánh.

    :param y:Vector thứ hai cần so sánh.

    :return:Một vector boolean trong đó mỗi phần tử ``i`` được tính là ``x[i] > y[i]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/greaterThan.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_lessThanEqual:

.. rst-class:: classref-method

|vec_bool_type| **lessThanEqual**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_lessThanEqual>`

    Thực hiện phép so sánh nhỏ hơn hoặc bằng :ref:`theo từng thành phần <shading_componentwise>` giữa hai vector.

    :param x:Vector đầu tiên cần so sánh.

    :param y:Vector thứ hai cần so sánh.

    :return:Một vector boolean trong đó mỗi phần tử ``i`` được tính là ``x[i] <= y[i]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/lessThanEqual.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_greaterThanEqual:

.. rst-class:: classref-method

|vec_bool_type| **greaterThanEqual**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_greaterThanEqual>`

    Thực hiện phép so sánh lớn hơn hoặc bằng :ref:`theo từng thành phần <shading_componentwise>` giữa hai vector.

    :param x:Vector đầu tiên cần so sánh.

    :param y:Vector thứ hai cần so sánh.

    :return:Một vector boolean trong đó mỗi phần tử ``i`` được tính là ``x[i] >= y[i]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/greaterThanEqual.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_equal:

.. rst-class:: classref-method

|vec_bool_type| **equal**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_equal>`

    Thực hiện phép so sánh bằng :ref:`theo từng thành phần <shading_componentwise>` giữa hai vector.

    :param x:Vector đầu tiên cần so sánh.

    :param y:Vector thứ hai cần so sánh.

    :return:Một vector boolean trong đó mỗi phần tử ``i`` được tính là ``x[i] == y[i]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/equal.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_notEqual:

.. rst-class:: classref-method

|vec_bool_type| **notEqual**\ (\ |vec_type| x, |vec_type| y) :ref:`🔗<shader_func_notEqual>`

    Thực hiện phép so sánh khác :ref:`theo từng thành phần <shading_componentwise>` giữa hai vector.

    :param x:Vector đầu tiên dùng để so sánh.

    :param y:Vector thứ hai dùng để so sánh.

    :return:Một vector boolean trong đó mỗi phần tử ``i`` được tính là ``x[i] != y[i]``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/notEqual.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_any:

.. rst-class:: classref-method

bool **any**\ (\ |vec_bool_type| x) :ref:`🔗<shader_func_any>`

    Trả về ``true`` nếu bất kỳ phần tử nào của vector boolean là ``true``, ngược lại là ``false``.

    Tương đương về chức năng với:

    ::

        bool any(bvec x) {     // bvec can be bvec2, bvec3 or bvec4
            bool result = false;
            int i;
            for (i = 0; i < x.length(); ++i) {
                result |= x[i];
            }
            return result;
        }

    :param x:Vector cần được kiểm tra giá trị đúng.

    :return:``true`` nếu bất kỳ phần tử nào của ``x`` là ``true`` và ``false`` nếu không.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/any.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_all:

.. rst-class:: classref-method

bool **all**\ (\ |vec_bool_type| x) :ref:`🔗<shader_func_all>`

    Trả về ``true`` nếu tất cả phần tử của vector boolean đều là ``true``, ngược lại là ``false``.

    Tương đương về chức năng với:

    ::

        bool all(bvec x)       // bvec can be bvec2, bvec3 or bvec4
        {
            bool result = true;
            int i;
            for (i = 0; i < x.length(); ++i)
            {
                result &= x[i];
            }
            return result;
        }

    :param x:Vector cần được kiểm tra giá trị đúng.

    :return:``true`` nếu tất cả phần tử của ``x`` đều là ``true`` và ``false`` nếu không.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/all.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_not:

.. rst-class:: classref-method

|vec_bool_type| **not**\ (\ |vec_bool_type| x) :ref:`🔗<shader_func_not>`

    Đảo ngược logic một vector boolean.

    :param x:Vector cần được đảo ngược.

    :return:Một vector boolean mới trong đó mỗi phần tử i được tính là !x[i].

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/not.xhtml


.. rst-class:: classref-section-separator

----










.. rst-class:: classref-reftable-group

Các hàm texture
---------------

.. table::
    :class: nowrap-col2
    :widths: auto

    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | ivec2          | | :ref:`textureSize<shader_func_textureSize>`\ (\ |gsampler2D| s, int lod)                              | Get the size of a texture.                                          |
    | | ivec2          | | :ref:`textureSize<shader_func_textureSize>`\ (\ samplerCube s, int lod)                               |                                                                     |
    | | ivec2          | | :ref:`textureSize<shader_func_textureSize>`\ (\ samplerCubeArray s, int lod)                          | For performance reasons, this function should be avoided as it      |
    | | ivec3          | | :ref:`textureSize<shader_func_textureSize>`\ (\ |gsampler2DArray| s, int lod)                         | always performs a full texture read. When possible, you should pass |
    | | ivec3          | | :ref:`textureSize<shader_func_textureSize>`\ (\ |gsampler3D| s, int lod)                              | the texture size as a uniform instead.                              |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | vec2           | | :ref:`textureQueryLod<shader_func_textureQueryLod>`\ (\ |gsampler2D| s, vec2 p)                       | Compute the level-of-detail that would be used to sample from a     |
    | | vec3           | | :ref:`textureQueryLod<shader_func_textureQueryLod>`\ (\ |gsampler2DArray| s, vec2 p)                  | texture.                                                            |
    | | vec2           | | :ref:`textureQueryLod<shader_func_textureQueryLod>`\ (\ |gsampler3D| s, vec3 p)                       |                                                                     |
    | | vec2           | | :ref:`textureQueryLod<shader_func_textureQueryLod>`\ (\ samplerCube s, vec3 p)                        |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | int            | | :ref:`textureQueryLevels<shader_func_textureQueryLevels>`\ (\ |gsampler2D| s)                         | Get the number of accessible mipmap levels of a texture.            |
    | | int            | | :ref:`textureQueryLevels<shader_func_textureQueryLevels>`\ (\ |gsampler2DArray| s)                    |                                                                     |
    | | int            | | :ref:`textureQueryLevels<shader_func_textureQueryLevels>`\ (\ |gsampler3D| s)                         |                                                                     |
    | | int            | | :ref:`textureQueryLevels<shader_func_textureQueryLevels>`\ (\ samplerCube s)                          |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`texture<shader_func_texture>`\ (\ |gsampler2D| s, vec2 p [, float bias] )                       | Performs a texture read.                                            |
    | | |gvec4_type|   | | :ref:`texture<shader_func_texture>`\ (\ |gsampler2DArray| s, vec3 p [, float bias] )                  |                                                                     |
    | | |gvec4_type|   | | :ref:`texture<shader_func_texture>`\ (\ |gsampler3D| s, vec3 p [, float bias] )                       |                                                                     |
    | | vec4           | | :ref:`texture<shader_func_texture>`\ (\ samplerCube s, vec3 p [, float bias] )                        |                                                                     |
    | | vec4           | | :ref:`texture<shader_func_texture>`\ (\ samplerCubeArray s, vec4 p [, float bias] )                   |                                                                     |
    | | vec4           | | :ref:`texture<shader_func_texture>`\ (\ samplerExternalOES s, vec2 p [, float bias] )                 |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`textureProj<shader_func_textureProj>`\ (\ |gsampler2D| s, vec3 p [, float bias] )               | Performs a texture read with projection.                            |
    | | |gvec4_type|   | | :ref:`textureProj<shader_func_textureProj>`\ (\ |gsampler2D| s, vec4 p [, float bias] )               |                                                                     |
    | | |gvec4_type|   | | :ref:`textureProj<shader_func_textureProj>`\ (\ |gsampler3D| s, vec4 p [, float bias] )               |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`textureLod<shader_func_textureLod>`\ (\ |gsampler2D| s, vec2 p, float lod)                      | Performs a texture read at custom mipmap.                           |
    | | |gvec4_type|   | | :ref:`textureLod<shader_func_textureLod>`\ (\ |gsampler2DArray| s, vec3 p, float lod)                 |                                                                     |
    | | |gvec4_type|   | | :ref:`textureLod<shader_func_textureLod>`\ (\ |gsampler3D| s, vec3 p, float lod)                      |                                                                     |
    | | vec4           | | :ref:`textureLod<shader_func_textureLod>`\ (\ samplerCube s, vec3 p, float lod)                       |                                                                     |
    | | vec4           | | :ref:`textureLod<shader_func_textureLod>`\ (\ samplerCubeArray s, vec4 p, float lod)                  |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`textureProjLod<shader_func_textureProjLod>`\ (\ |gsampler2D| s, vec3 p, float lod)              | Performs a texture read with projection/LOD.                        |
    | | |gvec4_type|   | | :ref:`textureProjLod<shader_func_textureProjLod>`\ (\ |gsampler2D| s, vec4 p, float lod)              |                                                                     |
    | | |gvec4_type|   | | :ref:`textureProjLod<shader_func_textureProjLod>`\ (\ |gsampler3D| s, vec4 p, float lod)              |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`textureGrad<shader_func_textureGrad>`\ (\ |gsampler2D| s, vec2 p, vec2 dPdx, vec2 dPdy)         | Performs a texture read with explicit gradients.                    |
    | | |gvec4_type|   | | :ref:`textureGrad<shader_func_textureGrad>`\ (\ |gsampler2DArray| s, vec3 p, vec2 dPdx, vec2 dPdy)    |                                                                     |
    | | |gvec4_type|   | | :ref:`textureGrad<shader_func_textureGrad>`\ (\ |gsampler3D| s, vec3 p, vec2 dPdx, vec2 dPdy)         |                                                                     |
    | | vec4           | | :ref:`textureGrad<shader_func_textureGrad>`\ (\ samplerCube s, vec3 p, vec3 dPdx, vec3 dPdy)          |                                                                     |
    | | vec4           | | :ref:`textureGrad<shader_func_textureGrad>`\ (\ samplerCubeArray s, vec3 p, vec3 dPdx, vec3 dPdy)     |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`textureProjGrad<shader_func_textureProjGrad>`\ (\ |gsampler2D| s, vec3 p, vec2 dPdx, vec2 dPdy) | Performs a texture read with projection/LOD and with explicit       |
    | | |gvec4_type|   | | :ref:`textureProjGrad<shader_func_textureProjGrad>`\ (\ |gsampler2D| s, vec4 p, vec2 dPdx, vec2 dPdy) |                                                                     |
    | | |gvec4_type|   | | :ref:`textureProjGrad<shader_func_textureProjGrad>`\ (\ |gsampler3D| s, vec4 p, vec3 dPdx, vec3 dPdy) |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`texelFetch<shader_func_texelFetch>`\ (\ |gsampler2D| s, ivec2 p, int lod)                       | Fetches a single texel using integer coordinates.                   |
    | | |gvec4_type|   | | :ref:`texelFetch<shader_func_texelFetch>`\ (\ |gsampler2DArray| s, ivec3 p, int lod)                  |                                                                     |
    | | |gvec4_type|   | | :ref:`texelFetch<shader_func_texelFetch>`\ (\ |gsampler3D| s, ivec3 p, int lod)                       |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |gvec4_type|   | | :ref:`textureGather<shader_func_textureGather>`\ (\ |gsampler2D| s, vec2 p [, int comps] )            | Gathers four texels from a texture.                                 |
    | | |gvec4_type|   | | :ref:`textureGather<shader_func_textureGather>`\ (\ |gsampler2DArray| s, vec3 p [, int comps] )       |                                                                     |
    | | vec4           | | :ref:`textureGather<shader_func_textureGather>`\ (\ samplerCube s, vec3 p [, int comps] )             |                                                                     |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`dFdx<shader_func_dFdx>`\ (\ |vec_type| p)                                                         | Derivative with respect to ``x`` window coordinate,                 |
    |                  |                                                                                                         | automatic granularity.                                              |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`dFdxCoarse<shader_func_dFdxCoarse>`\ (\ |vec_type| p)                                             | Derivative with respect to ``x`` window coordinate,                 |
    |                  |                                                                                                         | course granularity.                                                 |
    |                  |                                                                                                         |                                                                     |
    |                  |                                                                                                         | Not available when using the Compatibility renderer.                |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`dFdxFine<shader_func_dFdxFine>`\ (\ |vec_type| p)                                                 | Derivative with respect to ``x`` window coordinate,                 |
    |                  |                                                                                                         | fine granularity.                                                   |
    |                  |                                                                                                         |                                                                     |
    |                  |                                                                                                         | Not available when using the Compatibility renderer.                |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`dFdy<shader_func_dFdy>`\ (\ |vec_type| p)                                                         | Derivative with respect to ``y`` window coordinate,                 |
    |                  |                                                                                                         | automatic granularity.                                              |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`dFdyCoarse<shader_func_dFdyCoarse>`\ (\ |vec_type| p)                                             | Derivative with respect to ``y`` window coordinate,                 |
    |                  |                                                                                                         | course granularity.                                                 |
    |                  |                                                                                                         |                                                                     |
    |                  |                                                                                                         | Not available when using the Compatibility renderer.                |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`dFdyFine<shader_func_dFdyFine>`\ (\ |vec_type| p)                                                 | Derivative with respect to ``y`` window coordinate,                 |
    |                  |                                                                                                         | fine granularity.                                                   |
    |                  |                                                                                                         |                                                                     |
    |                  |                                                                                                         | Not available when using the Compatibility renderer.                |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`fwidth<shader_func_fwidth>`\ (\ |vec_type| p)                                                     | Sum of absolute derivative in ``x`` and ``y``.                      |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`fwidthCoarse<shader_func_fwidthCoarse>`\ (\ |vec_type| p)                                         | Sum of absolute derivative in ``x`` and ``y``.                      |
    |                  |                                                                                                         |                                                                     |
    |                  |                                                                                                         | Not available when using the Compatibility renderer.                |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|       | :ref:`fwidthFine<shader_func_fwidthFine>`\ (\ |vec_type| p)                                             | Sum of absolute derivative in ``x`` and ``y``.                      |
    |                  |                                                                                                         |                                                                     |
    |                  |                                                                                                         | Not available when using the Compatibility renderer.                |
    +------------------+---------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+


.. rst-class:: classref-descriptions-group

Mô tả các hàm texture
~~~~~~~~~~~~~~~~~~~~~

.. _shader_func_textureSize:

.. rst-class:: classref-method

ivec2 **textureSize**\ (\ |gsampler2D| s, int lod) :ref:`🔗<shader_func_textureSize>`

.. rst-class:: classref-method

ivec2 **textureSize**\ (\ samplerCube s, int lod) :ref:`🔗<shader_func_textureSize>`

.. rst-class:: classref-method

ivec2 **textureSize**\ (\ samplerCubeArray s, int lod) :ref:`🔗<shader_func_textureSize>`

.. rst-class:: classref-method

ivec3 **textureSize**\ (\ |gsampler2DArray| s, int lod) :ref:`🔗<shader_func_textureSize>`

.. rst-class:: classref-method

ivec3 **textureSize**\ (\ |gsampler3D| s, int lod) :ref:`🔗<shader_func_textureSize>`

    Lấy kích thước của một level của texture.

    Trả về kích thước của level ``lod`` (nếu có) của texture được liên kết với sampler.

    Các thành phần trong giá trị trả về lần lượt được điền bằng chiều rộng, chiều cao và độ sâu của texture. Đối với các dạng mảng, thành phần cuối cùng của giá trị trả về là số layer trong mảng texture.

    :param s:Sampler mà texture cần lấy kích thước được liên kết với.

    :param lod:Level của texture cần lấy kích thước.

    :return:Kích thước của level ``lod`` (nếu có) của texture được liên kết với sampler.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureSize.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureQueryLod:

.. rst-class:: classref-method

vec2 **textureQueryLod**\ (\ |gsampler2D| s, vec2 p) :ref:`🔗<shader_func_textureQueryLod>`

.. rst-class:: classref-method

vec2 **textureQueryLod**\ (\ |gsampler2DArray| s, vec2 p) :ref:`🔗<shader_func_textureQueryLod>`

.. rst-class:: classref-method

vec2 **textureQueryLod**\ (\ |gsampler3D| s, vec3 p) :ref:`🔗<shader_func_textureQueryLod>`

.. rst-class:: classref-method

vec2 **textureQueryLod**\ (\ samplerCube s, vec3 p) :ref:`🔗<shader_func_textureQueryLod>`

    .. note:: Chỉ khả dụng trong fragment shader.

    Tính level-of-detail sẽ được dùng để lấy mẫu từ một texture.

    Mipmap array sẽ được truy cập được trả về trong thành phần x của giá trị trả về. Level-of-detail được tính toán so với base level được trả về trong thành phần y của giá trị trả về.

    Nếu được gọi trên một texture chưa hoàn chỉnh, kết quả của thao tác là không xác định.

    :param s:Sampler mà texture cần truy vấn level-of-detail được liên kết với.

    :param p:Tọa độ texture tại đó level-of-detail sẽ được truy vấn.

    :return:Xem mô tả.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureQueryLod.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureQueryLevels:

.. rst-class:: classref-method

int **textureQueryLevels**\ (\ |gsampler2D| s) :ref:`🔗<shader_func_textureQueryLevels>`

.. rst-class:: classref-method

int **textureQueryLevels**\ (\ |gsampler2DArray| s) :ref:`🔗<shader_func_textureQueryLevels>`

.. rst-class:: classref-method

int **textureQueryLevels**\ (\ |gsampler3D| s) :ref:`🔗<shader_func_textureQueryLevels>`

.. rst-class:: classref-method

int **textureQueryLevels**\ (\ samplerCube s) :ref:`🔗<shader_func_textureQueryLevels>`

    Tính số level mipmap có thể truy cập của một texture.

    Nếu được gọi trên một texture chưa hoàn chỉnh hoặc không có texture nào được liên kết với sampler, ``0`` sẽ được trả về.

    :param s:Sampler mà texture có số lượng mức mipmap cần truy vấn được liên kết với.

    :return:Số mức mipmap có thể truy cập trong texture, hoặc ``0``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureQueryLevels.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_texture:

.. rst-class:: classref-method

|gvec4_type| **texture**\ (\ |gsampler2D| s, vec2 p [, float bias] ) :ref:`🔗<shader_func_texture>`

.. rst-class:: classref-method

|gvec4_type| **texture**\ (\ |gsampler2DArray| s, vec3 p [, float bias] ) :ref:`🔗<shader_func_texture>`

.. rst-class:: classref-method

|gvec4_type| **texture**\ (\ |gsampler3D| s, vec3 p [, float bias] ) :ref:`🔗<shader_func_texture>`

.. rst-class:: classref-method

vec4 **texture**\ (\ samplerCube s, vec3 p [, float bias] ) :ref:`🔗<shader_func_texture>`

.. rst-class:: classref-method

vec4 **texture**\ (\ samplerCubeArray s, vec4 p [, float bias] ) :ref:`🔗<shader_func_texture>`

.. rst-class:: classref-method

vec4 **texture**\ (\ samplerExternalOES s, vec2 p [, float bias] ) :ref:`🔗<shader_func_texture>`

    Truy xuất các texel từ một texture.

    Lấy mẫu các texel từ texture được liên kết với ``s`` tại tọa độ texture ``p``. Một bias tùy chọn, được chỉ định trong ``bias``, được đưa vào phép tính level-of-detail dùng để chọn (các) mipmap lấy mẫu.

    Đối với các dạng shadow, component cuối cùng của ``p`` được dùng làm Dsub và layer của mảng được chỉ định trong component áp chót của ``p``. (Component thứ hai của ``p`` không được sử dụng cho các phép tra cứu shadow 1D.)

    Đối với các biến thể không phải shadow, layer của mảng được lấy từ component cuối cùng của P.

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param bias:Bias tùy chọn được áp dụng trong quá trình tính level-of-detail.

    :return:Một texel.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/texture.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureProj:

.. rst-class:: classref-method

|gvec4_type| **textureProj**\ (\ |gsampler2D| s, vec3 p [, float bias] ) :ref:`🔗<shader_func_textureProj>`

.. rst-class:: classref-method

|gvec4_type| **textureProj**\ (\ |gsampler2D| s, vec4 p [, float bias] ) :ref:`🔗<shader_func_textureProj>`

.. rst-class:: classref-method

|gvec4_type| **textureProj**\ (\ |gsampler3D| s, vec4 p [, float bias] ) :ref:`🔗<shader_func_textureProj>`

    Thực hiện phép tra cứu texture có phép chiếu.

    Các tọa độ texture lấy từ ``p``, không bao gồm component cuối cùng của ``p``, được chia cho component cuối cùng của ``p``. Component thứ 3 thu được của ``p`` trong các dạng shadow được dùng làm Dref. Sau khi tính các giá trị này, phép tra cứu texture tiếp tục như trong texture.

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param bias:Bias tùy chọn được áp dụng trong quá trình tính level-of-detail.

    :return:Một texel.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureProj.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureLod:

.. rst-class:: classref-method

|gvec4_type| **textureLod**\ (\ |gsampler2D| s, vec2 p, float lod) :ref:`🔗<shader_func_textureLod>`

.. rst-class:: classref-method

|gvec4_type| **textureLod**\ (\ |gsampler2DArray| s, vec3 p, float lod) :ref:`🔗<shader_func_textureLod>`

.. rst-class:: classref-method

|gvec4_type| **textureLod**\ (\ |gsampler3D| s, vec3 p, float lod) :ref:`🔗<shader_func_textureLod>`

.. rst-class:: classref-method

vec4 **textureLod**\ (\ samplerCube s, vec3 p, float lod) :ref:`🔗<shader_func_textureLod>`

.. rst-class:: classref-method

vec4 **textureLod**\ (\ samplerCubeArray s, vec4 p, float lod) :ref:`🔗<shader_func_textureLod>`

    Thực hiện phép tra cứu texture tại tọa độ ``p`` từ texture được liên kết với sampler, với level-of-detail tường minh như được chỉ định trong ``lod``. ``lod`` chỉ định λbase và thiết lập các đạo hàm riêng như sau:

    ::

        δu/δx=0, δv/δx=0, δw/δx=0
        δu/δy=0, δv/δy=0, δw/δy=0

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param lod:Level-of-detail tường minh.

    :return:Một texel.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureLod.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureProjLod:

.. rst-class:: classref-method

|gvec4_type| **textureProjLod**\ (\ |gsampler2D| s, vec3 p, float lod) :ref:`🔗<shader_func_textureProjLod>`

.. rst-class:: classref-method

|gvec4_type| **textureProjLod**\ (\ |gsampler2D| s, vec4 p, float lod) :ref:`🔗<shader_func_textureProjLod>`

.. rst-class:: classref-method

|gvec4_type| **textureProjLod**\ (\ |gsampler3D| s, vec4 p, float lod) :ref:`🔗<shader_func_textureProjLod>`

    Thực hiện phép tra cứu texture có phép chiếu từ một level-of-detail được chỉ định tường minh.

    Các tọa độ texture lấy từ P, không bao gồm component cuối cùng của ``p``, được chia cho component cuối cùng của ``p``. Component thứ 3 thu được của ``p`` trong các dạng shadow được dùng làm Dref. Sau khi tính các giá trị này, phép tra cứu texture tiếp tục như trong `textureLod<shader_func_textureLod>`, với ``lod`` được dùng để chỉ định level-of-detail mà texture sẽ được lấy mẫu từ đó.

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param lod:Level-of-detail tường minh mà từ đó các texel được truy xuất.

    :return:một texel

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureProjLod.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureGrad:

.. rst-class:: classref-method

|gvec4_type| **textureGrad**\ (\ |gsampler2D| s, vec2 p, vec2 dPdx, vec2 dPdy) :ref:`🔗<shader_func_textureGrad>`

.. rst-class:: classref-method

|gvec4_type| **textureGrad**\ (\ |gsampler2DArray| s, vec3 p, vec2 dPdx, vec2 dPdy) :ref:`🔗<shader_func_textureGrad>`

.. rst-class:: classref-method

|gvec4_type| **textureGrad**\ (\ |gsampler3D| s, vec3 p, vec2 dPdx, vec2 dPdy) :ref:`🔗<shader_func_textureGrad>`

.. rst-class:: classref-method

vec4 **textureGrad**\ (\ samplerCube s, vec3 p, vec3 dPdx, vec3 dPdy) :ref:`🔗<shader_func_textureGrad>`

.. rst-class:: classref-method

vec4 **textureGrad**\ (\ samplerCubeArray s, vec3 p, vec3 dPdx, vec3 dPdy) :ref:`🔗<shader_func_textureGrad>`

    Thực hiện phép tra cứu texture tại tọa độ ``p`` từ texture được liên kết với sampler, với các gradient tọa độ texture tường minh như được chỉ định trong ``dPdx`` và ``dPdy``. Thiết lập:
     - ``δs/δx=δp/δx`` cho texture 1D, nếu không thì ``δp.s/δx``
     - ``δs/δy=δp/δy`` cho texture 1D, nếu không thì ``δp.s/δy``
     - ``δt/δx=0.0`` cho texture 1D, nếu không thì ``δp.t/δx``
     - ``δt/δy=0.0`` cho texture 1D, nếu không thì ``δp.t/δy``
     - ``δr/δx=0.0`` cho texture 1D hoặc 2D, nếu không thì ``δp.p/δx``
     - ``δr/δy=0.0`` cho texture 1D hoặc 2D, nếu không thì ``δp.p/δy``

    Đối với phiên bản cube, các đạo hàm riêng của ``p`` được giả định là nằm trong hệ tọa độ được sử dụng trước khi các tọa độ texture được chiếu lên mặt cube thích hợp.

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param dPdx:Đạo hàm riêng của P theo window x.

    :param dPdy:Đạo hàm riêng của P theo window y.

    :return:Một texel.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureGrad.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureProjGrad:

.. rst-class:: classref-method

|gvec4_type| **textureProjGrad**\ (\ |gsampler2D| s, vec3 p, vec2 dPdx, vec2 dPdy) :ref:`🔗<shader_func_textureProjGrad>`

.. rst-class:: classref-method

|gvec4_type| **textureProjGrad**\ (\ |gsampler2D| s, vec4 p, vec2 dPdx, vec2 dPdy) :ref:`🔗<shader_func_textureProjGrad>`

.. rst-class:: classref-method

|gvec4_type| **textureProjGrad**\ (\ |gsampler3D| s, vec4 p, vec3 dPdx, vec3 dPdy) :ref:`🔗<shader_func_textureProjGrad>`

    Thực hiện phép tra cứu texture có phép chiếu và các gradient tường minh.

    Các tọa độ texture lấy từ ``p``, không bao gồm component cuối cùng của ``p``, được chia cho component cuối cùng của ``p``. Sau khi tính các giá trị này, phép tra cứu texture tiếp tục như trong `textureGrad<shader_func_textureGrad>`, truyền ``dPdx`` và ``dPdy`` làm các gradient.

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param dPdx:Đạo hàm riêng của ``p`` theo window x.

    :param dPdy:Đạo hàm riêng của ``p`` theo window y.

    :return:Một texel.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureProjGrad.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_texelFetch:

.. rst-class:: classref-method

|gvec4_type| **texelFetch**\ (\ |gsampler2D| s, ivec2 p, int lod) :ref:`🔗<shader_func_texelFetch>`

.. rst-class:: classref-method

|gvec4_type| **texelFetch**\ (\ |gsampler2DArray| s, ivec3 p, int lod) :ref:`🔗<shader_func_texelFetch>`

.. rst-class:: classref-method

|gvec4_type| **texelFetch**\ (\ |gsampler3D| s, ivec3 p, int lod) :ref:`🔗<shader_func_texelFetch>`

    Thực hiện tra cứu một texel duy nhất từ tọa độ texture ``p`` trong texture được liên kết với sampler.

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param lod:Chỉ định level-of-detail trong texture mà từ đó texel sẽ được truy xuất.

    :return:Một texel.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/texelFetch.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_textureGather:

.. rst-class:: classref-method

|gvec4_type| **textureGather**\ (\ |gsampler2D| s, vec2 p [, int comps] ) :ref:`🔗<shader_func_textureGather>`

.. rst-class:: classref-method

|gvec4_type| **textureGather**\ (\ |gsampler2DArray| s, vec3 p [, int comps] ) :ref:`🔗<shader_func_textureGather>`

.. rst-class:: classref-method

vec4 **textureGather**\ (\ samplerCube s, vec3 p [, int comps] ) :ref:`🔗<shader_func_textureGather>`

    Tập hợp bốn texel từ một texture.

    Trả về giá trị:

    ::

        vec4(Sample_i0_j1(p, base).comps,
             Sample_i1_j1(p, base).comps,
             Sample_i1_j0(p, base).comps,
             Sample_i0_j0(p, base).comps);

    :param s:Sampler mà texture cần truy xuất texel được liên kết với.

    :param p:Các tọa độ texture tại đó texture sẽ được lấy mẫu.

    :param comps:*optional* thành phần của texture nguồn (0 -> x, 1 -> y, 2 -> z, 3 -> w) sẽ được dùng để tạo vector kết quả. Bằng không nếu không được chỉ định.

    :return:Texel đã lấy.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/textureGather.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_dFdx:

.. rst-class:: classref-method

|vec_type| **dFdx**\ (\ |vec_type| p) :ref:`🔗<shader_func_dFdx>`

    .. note:: Chỉ khả dụng trong fragment shader.

    Trả về đạo hàm riêng của ``p`` theo tọa độ x của cửa sổ bằng cách lấy sai phân cục bộ.

    Trả về :ref:`dFdxCoarse <shader_func_dFdxCoarse>` hoặc :ref:`dFdxFine <shader_func_dfdxFine>`. Việc triển khai có thể chọn phép tính nào để thực hiện dựa trên các yếu tố như hiệu năng hoặc giá trị của gợi ý ``GL_FRAGMENT_SHADER_DERIVATIVE_HINT`` của API.


    .. warning::
        Các biểu thức ngụ ý đạo hàm bậc cao hơn như ``dFdx(dFdx(n))`` có kết quả không xác định, cũng như các đạo hàm có bậc hỗn hợp như ``dFdx(dFdy(n))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

        .. note:: Giả định rằng biểu thức ``p`` là liên tục, do đó các biểu thức được đánh giá thông qua luồng điều khiển không đồng nhất có thể không xác định.

    :return:Đạo hàm riêng của ``p``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/dFdx.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_dFdxCoarse:

.. rst-class:: classref-method

|vec_type| **dFdxCoarse**\ (\ |vec_type| p) :ref:`🔗<shader_func_dFdxCoarse>`

    .. note::
        Chỉ khả dụng trong fragment shader. Không khả dụng khi sử dụng Compatibility renderer.

    Trả về đạo hàm riêng của ``p`` theo tọa độ x của cửa sổ.

    Tính các đạo hàm bằng cách lấy sai phân cục bộ dựa trên giá trị của ``p`` tại các fragment lân cận của fragment hiện tại, và có thể, nhưng không nhất thiết, bao gồm giá trị của fragment hiện tại. Nghĩa là, trong một vùng cho trước, việc triển khai có thể tính các đạo hàm tại ít vị trí duy nhất hơn số vị trí được phép đối với hàm :ref:`dFdxFine <shader_func_dFdxFine>` tương ứng.

    .. warning::
        Các biểu thức ngụ ý đạo hàm bậc cao hơn như ``dFdx(dFdx(n))`` có kết quả không xác định, cũng như các đạo hàm có bậc hỗn hợp như ``dFdx(dFdy(n))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

        .. note:: Giả định rằng biểu thức ``p`` là liên tục, do đó các biểu thức được đánh giá thông qua luồng điều khiển không đồng nhất có thể không xác định.

    :return:Đạo hàm riêng của ``p``.

    https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_dFdxFine:

.. rst-class:: classref-method

|vec_type| **dFdxFine**\ (\ |vec_type| p) :ref:`🔗<shader_func_dFdxFine>`

    .. note::
        Chỉ khả dụng trong fragment shader. Không khả dụng khi sử dụng Compatibility renderer.

    Trả về đạo hàm riêng của ``p`` theo tọa độ x của cửa sổ.

    Tính các đạo hàm bằng cách lấy sai phân cục bộ dựa trên giá trị của ``p`` tại fragment hiện tại và (các) fragment lân cận trực tiếp của nó.

    .. warning::
        Các biểu thức ngụ ý đạo hàm bậc cao hơn như ``dFdx(dFdx(n))`` có kết quả không xác định, cũng như các đạo hàm có bậc hỗn hợp như ``dFdx(dFdy(n))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

        .. note:: Giả định rằng biểu thức ``p`` là liên tục, do đó các biểu thức được đánh giá thông qua luồng điều khiển không đồng nhất có thể không xác định.

    :return:Đạo hàm riêng của ``p``.

    https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_dFdy:

.. rst-class:: classref-method

|vec_type| **dFdy**\ (\ |vec_type| p) :ref:`🔗<shader_func_dFdy>`

    .. note:: Chỉ khả dụng trong fragment shader.

    Trả về đạo hàm riêng của ``p`` theo tọa độ y của cửa sổ bằng cách lấy sai phân cục bộ.

    Trả về :ref:`dFdyCoarse <shader_func_dFdyCoarse>` hoặc :ref:`dFdyFine <shader_func_dfdyFine>`. Việc triển khai có thể chọn phép tính nào để thực hiện dựa trên các yếu tố như hiệu năng hoặc giá trị của gợi ý ``GL_FRAGMENT_SHADER_DERIVATIVE_HINT`` của API.

    .. warning::
        Các biểu thức ngụ ý đạo hàm bậc cao hơn như ``dFdx(dFdx(n))`` có kết quả không xác định, cũng như các đạo hàm có bậc hỗn hợp như ``dFdx(dFdy(n))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

        .. note:: Giả định rằng biểu thức ``p`` là liên tục, do đó các biểu thức được đánh giá thông qua luồng điều khiển không đồng nhất có thể không xác định.

    :return:Đạo hàm riêng của ``p``.

    https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_dFdyCoarse:

.. rst-class:: classref-method

|vec_type| **dFdyCoarse**\ (\ |vec_type| p) :ref:`🔗<shader_func_dFdyCoarse>`

    .. note::
        Chỉ khả dụng trong fragment shader. Không khả dụng khi sử dụng Compatibility renderer.

    Trả về đạo hàm riêng của ``p`` theo tọa độ y của cửa sổ.

    Tính các đạo hàm bằng cách lấy sai phân cục bộ dựa trên giá trị của ``p`` tại các fragment lân cận của fragment hiện tại, và có thể, nhưng không nhất thiết, bao gồm giá trị của fragment hiện tại. Nghĩa là, trong một vùng cho trước, việc triển khai có thể tính các đạo hàm tại ít vị trí duy nhất hơn số vị trí được phép đối với các hàm dFdyFine và dFdyFine tương ứng.

    .. warning:: Các biểu thức ngụ ý đạo hàm bậc cao hơn như ``dFdx(dFdx(n))`` có kết quả không xác định, cũng như các đạo hàm có bậc hỗn hợp như ``dFdx(dFdy(n))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

        .. note:: Giả định rằng biểu thức ``p`` là liên tục, do đó các biểu thức được đánh giá thông qua luồng điều khiển không đồng nhất có thể không xác định.

    :return:Đạo hàm riêng của ``p``.

    https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_dFdyFine:

.. rst-class:: classref-method

|vec_type| **dFdyFine**\ (\ |vec_type| p) :ref:`🔗<shader_func_dFdyFine>`

    .. note::
        Chỉ khả dụng trong fragment shader. Không khả dụng khi sử dụng Compatibility renderer.

    Trả về đạo hàm riêng của ``p`` theo tọa độ y của cửa sổ.

    Tính các đạo hàm bằng cách lấy sai phân cục bộ dựa trên giá trị của ``p`` tại fragment hiện tại và (các) fragment lân cận trực tiếp của nó.

    .. warning:: Các biểu thức ngụ ý đạo hàm bậc cao hơn như ``dFdx(dFdx(n))`` có kết quả không xác định, cũng như các đạo hàm có bậc hỗn hợp như ``dFdx(dFdy(n))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

        .. note:: Giả định rằng biểu thức ``p`` là liên tục, do đó các biểu thức được đánh giá thông qua luồng điều khiển không đồng nhất có thể không xác định.

    :return:Đạo hàm riêng của ``p``.

    https://registry.khronos.org/OpenGL-Refpages/gl4/html/dFdx.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_fwidth:

.. rst-class:: classref-method

|vec_type| **fwidth**\ (\ |vec_type| p) :ref:`🔗<shader_func_fwidth>`

    Trả về tổng các giá trị tuyệt đối của các đạo hàm theo x và y.

    Sử dụng sai phân cục bộ cho đối số đầu vào ``p``.

    Tương đương với ``abs(dFdx(p)) + abs(dFdy(p))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

    :return:Đạo hàm riêng.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fwidth.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_fwidthCoarse:

.. rst-class:: classref-method

|vec_type| **fwidthCoarse**\ (\ |vec_type| p) :ref:`🔗<shader_func_fwidthCoarse>`

    .. note::
        Chỉ khả dụng trong fragment shader. Không khả dụng khi sử dụng Compatibility renderer.

    Trả về tổng các giá trị tuyệt đối của các đạo hàm theo x và y.

    Sử dụng phép sai phân cục bộ cho đối số đầu vào p.

    Tương đương với ``abs(dFdxCoarse(p)) + abs(dFdyCoarse(p))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

    :return:Đạo hàm riêng.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/fwidth.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_fwidthFine:

.. rst-class:: classref-method

|vec_type| **fwidthFine**\ (\ |vec_type| p) :ref:`🔗<shader_func_fwidthFine>`

    .. note::
        Chỉ khả dụng trong fragment shader. Không khả dụng khi sử dụng Compatibility renderer.

    Trả về tổng các giá trị tuyệt đối của các đạo hàm theo x và y.

    Sử dụng phép sai phân cục bộ cho đối số đầu vào p.

    Tương đương với ``abs(dFdxFine(p)) + abs(dFdyFine(p))``.

    :param p:Biểu thức cần lấy đạo hàm riêng.

    :return:Đạo hàm riêng.

    https://registry.khronos.org/OpenGL-Refpages/gl4/html/fwidth.xhtml


.. rst-class:: classref-section-separator

----













.. rst-class:: classref-reftable-group

Các hàm đóng gói và giải đóng gói
---------------------------------

Các hàm này chuyển đổi các số dấu phẩy động thành các số nguyên có nhiều kích thước khác nhau, sau đó đóng gói các số nguyên đó vào một số nguyên không dấu 32 bit duy nhất. Các hàm 'unpack' thực hiện thao tác ngược lại, trả về các số dấu phẩy động ban đầu.

.. table::
    :class: nowrap-col2
    :widths: auto

    +------------+------------------------------------------------------------------------+--------------------------------------------------------------+
    | | uint     | | :ref:`packHalf2x16<shader_func_packHalf2x16>`\ (\ vec2 v)            | Convert two 32-bit floats to 16 bit floats and pack them.    |
    | | vec2     | | :ref:`unpackHalf2x16<shader_func_unpackHalf2x16>`\ (\ uint v)        |                                                              |
    +------------+------------------------------------------------------------------------+--------------------------------------------------------------+
    | | uint     | | :ref:`packUnorm2x16<shader_func_packUnorm2x16>`\ (\ vec2 v)          | Convert two normalized (range 0..1) 32-bit floats            |
    | | vec2     | | :ref:`unpackUnorm2x16<shader_func_unpackUnorm2x16>`\ (\ uint v)      | to 16-bit unsigned ints and pack them.                       |
    +------------+------------------------------------------------------------------------+--------------------------------------------------------------+
    | | uint     | | :ref:`packSnorm2x16<shader_func_packSnorm2x16>`\ (\ vec2 v)          | Convert two signed normalized (range -1..1) 32-bit floats    |
    | | vec2     | | :ref:`unpackSnorm2x16<shader_func_unpackSnorm2x16>`\ (\ uint v)      | to 16-bit signed ints and pack them.                         |
    +------------+------------------------------------------------------------------------+--------------------------------------------------------------+
    | | uint     | | :ref:`packUnorm4x8<shader_func_packUnorm4x8>`\ (\ vec4 v)            | Convert four normalized (range 0..1) 32-bit floats           |
    | | vec4     | | :ref:`unpackUnorm4x8<shader_func_unpackUnorm4x8>`\ (\ uint v)        | into 8-bit unsigned ints and pack them.                      |
    +------------+------------------------------------------------------------------------+--------------------------------------------------------------+
    | | uint     | | :ref:`packSnorm4x8<shader_func_packSnorm4x8>`\ (\ vec4 v)            | Convert four signed normalized (range -1..1) 32-bit floats   |
    | | vec4     | | :ref:`unpackSnorm4x8<shader_func_unpackSnorm4x8>`\ (\ uint v)        | into 8-bit signed ints and pack them.                        |
    +------------+------------------------------------------------------------------------+--------------------------------------------------------------+

.. rst-class:: classref-descriptions-group

Mô tả các hàm đóng gói và giải đóng gói
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _shader_func_packHalf2x16:

.. rst-class:: classref-method

uint **packHalf2x16**\ (\ vec2 v) :ref:`🔗<shader_func_packHalf2x16>`

    Chuyển đổi hai giá trị dấu phẩy động 32 bit thành các giá trị dấu phẩy động 16 bit và đóng gói chúng vào một số nguyên 32 bit duy nhất.

    Trả về một số nguyên không dấu thu được bằng cách chuyển đổi các thành phần của một vector dấu phẩy động hai thành phần sang biểu diễn dấu phẩy động 16 bit được nêu trong OpenGL Specification, sau đó đóng gói hai số nguyên 16 bit này vào một số nguyên không dấu 32 bit. Thành phần vector thứ nhất chỉ định 16 bit ít quan trọng nhất của kết quả; thành phần thứ hai chỉ định 16 bit quan trọng nhất.

    :param v:Một vector gồm hai giá trị dấu phẩy động 32 bit cần được chuyển đổi sang biểu diễn 16 bit và đóng gói vào kết quả.

    :return:Giá trị đã đóng gói.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packHalf2x16.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_unpackHalf2x16:

.. rst-class:: classref-method

vec2 **unpackHalf2x16**\ (\ uint v) :ref:`🔗<shader_func_unpackHalf2x16>`

    Phép đảo của :ref:`packHalf2x16 <shader_func_packHalf2x16>`.

    Giải đóng gói một số nguyên 32 bit thành hai giá trị dấu phẩy động 16 bit, chuyển đổi chúng thành các giá trị dấu phẩy động 32 bit và đưa chúng vào một vector. Thành phần thứ nhất của vector được lấy từ 16 bit ít quan trọng nhất của ``v``; thành phần thứ hai được lấy từ 16 bit quan trọng nhất của ``v``.

    :param v:Một số nguyên không dấu 32 bit duy nhất chứa 2 giá trị dấu phẩy động 16 bit đã đóng gói.

    :return:Hai giá trị dấu phẩy động đã giải đóng gói.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackHalf2x16.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_packUnorm2x16:

.. rst-class:: classref-method

uint **packUnorm2x16**\ (\ vec2 v) :ref:`🔗<shader_func_packUnorm2x16>`

    Đóng gói các giá trị dấu phẩy động vào một số nguyên không dấu.

    Chuyển đổi từng thành phần của giá trị dấu phẩy động đã chuẩn hóa v thành các giá trị số nguyên 16 bit, sau đó đóng gói các kết quả vào một số nguyên không dấu 32 bit.

    Phép chuyển đổi thành phần c của ``v`` sang dạng dấu phẩy tĩnh được thực hiện như sau:

    ::

        round(clamp(c, 0.0, 1.0) * 65535.0)

    Thành phần thứ nhất của vector sẽ được ghi vào các bit ít quan trọng nhất của đầu ra; thành phần cuối cùng sẽ được ghi vào các bit quan trọng nhất.


    :param v:Một vector các giá trị cần được đóng gói vào một số nguyên không dấu.

    :return:Số nguyên không dấu 32 bit chứa mã hóa đã đóng gói của vector.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_unpackUnorm2x16:

.. rst-class:: classref-method

vec2 **unpackUnorm2x16**\ (\ uint v) :ref:`🔗<shader_func_unpackUnorm2x16>`

    Giải đóng gói các giá trị dấu phẩy động từ một số nguyên không dấu.

    Giải đóng gói các số nguyên không dấu 32 bit đơn thành một cặp số nguyên không dấu 16 bit. Sau đó, mỗi thành phần được chuyển đổi thành một giá trị dấu phẩy động đã chuẩn hóa để tạo ra vector hai thành phần được trả về.

    Phép chuyển đổi giá trị dấu phẩy tĩnh f đã giải đóng gói sang dấu phẩy động được thực hiện như sau:

        f / 65535.0

    Thành phần thứ nhất của vector được trả về sẽ được trích xuất từ các bit ít quan trọng nhất của đầu vào; thành phần cuối cùng sẽ được trích xuất từ các bit quan trọng nhất.

    :param v:Một số nguyên không dấu chứa các giá trị dấu phẩy động đã đóng gói.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_packSnorm2x16:

.. rst-class:: classref-method

uint **packSnorm2x16**\ (\ vec2 v) :ref:`🔗<shader_func_packSnorm2x16>`

    Đóng gói các giá trị dấu phẩy động vào một số nguyên không dấu.

    Chuyển đổi từng thành phần của giá trị dấu phẩy động đã chuẩn hóa ``v`` thành các giá trị số nguyên 16 bit, sau đó đóng gói các kết quả vào một số nguyên không dấu 32 bit.

    Phép chuyển đổi thành phần c của ``v`` sang dạng dấu phẩy tĩnh được thực hiện như sau:

    ::

        round(clamp(c, -1.0, 1.0) * 32767.0)

    Thành phần thứ nhất của vector sẽ được ghi vào các bit ít quan trọng nhất của đầu ra; thành phần cuối cùng sẽ được ghi vào các bit quan trọng nhất.

    :param v:Một vector các giá trị cần được đóng gói vào một số nguyên không dấu.

    :return:Số nguyên không dấu 32 bit chứa mã hóa đã đóng gói của vector.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_unpackSnorm2x16:

.. rst-class:: classref-method

vec2 **unpackSnorm2x16**\ (\ uint v) :ref:`🔗<shader_func_unpackSnorm2x16>`

    Giải đóng gói các giá trị dấu phẩy động từ một số nguyên không dấu.

    Giải đóng gói các số nguyên không dấu 32 bit đơn thành một cặp số nguyên có dấu 16 bit. Sau đó, mỗi thành phần được chuyển đổi thành một giá trị dấu phẩy động đã chuẩn hóa để tạo ra vector hai thành phần được trả về.

    Phép chuyển đổi giá trị dấu phẩy tĩnh f đã giải đóng gói sang dấu phẩy động được thực hiện như sau:

        clamp(f / 32727.0, -1.0, 1.0)

    Thành phần thứ nhất của vector được trả về sẽ được trích xuất từ các bit ít quan trọng nhất của đầu vào; thành phần cuối cùng sẽ được trích xuất từ các bit quan trọng nhất.

    :param v:Một số nguyên không dấu chứa các giá trị dấu phẩy động đã đóng gói.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_packUnorm4x8:

.. rst-class:: classref-method

uint **packUnorm4x8**\ (\ vec4 v) :ref:`🔗<shader_func_packUnorm4x8>`

    Đóng gói các giá trị dấu phẩy động vào một số nguyên không dấu.

    Chuyển đổi từng thành phần của giá trị dấu phẩy động đã chuẩn hóa ``v`` thành các giá trị số nguyên 16 bit, sau đó đóng gói các kết quả vào một số nguyên không dấu 32 bit.

    Phép chuyển đổi thành phần c của ``v`` sang dạng dấu phẩy tĩnh được thực hiện như sau:

    ::

        round(clamp(c, 0.0, 1.0) * 255.0)

    Thành phần thứ nhất của vector sẽ được ghi vào các bit ít quan trọng nhất của đầu ra; thành phần cuối cùng sẽ được ghi vào các bit quan trọng nhất.


    :param v:Một vector các giá trị cần được đóng gói vào một số nguyên không dấu.

    :return:Số nguyên không dấu 32 bit chứa mã hóa đã đóng gói của vector.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_unpackUnorm4x8:

.. rst-class:: classref-method

vec4 **unpackUnorm4x8**\ (\ uint v) :ref:`🔗<shader_func_unpackUnorm4x8>`

    Giải đóng gói các giá trị dấu phẩy động từ một số nguyên không dấu.

    Giải nén các số nguyên không dấu 32-bit đơn lẻ thành bốn số nguyên không dấu 8-bit. Sau đó, mỗi thành phần được chuyển đổi thành giá trị dấu phẩy động chuẩn hóa để tạo ra vector bốn thành phần được trả về.

    Phép chuyển đổi giá trị dấu phẩy tĩnh f đã giải đóng gói sang dấu phẩy động được thực hiện như sau:

        f / 255.0

    Thành phần thứ nhất của vector được trả về sẽ được trích xuất từ các bit ít quan trọng nhất của đầu vào; thành phần cuối cùng sẽ được trích xuất từ các bit quan trọng nhất.

    :param v:Một số nguyên không dấu chứa các giá trị dấu phẩy động đã đóng gói.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_packSnorm4x8:

.. rst-class:: classref-method

uint **packSnorm4x8**\ (\ vec4 v) :ref:`🔗<shader_func_packSnorm4x8>`

    Đóng gói các giá trị dấu phẩy động vào một số nguyên không dấu.

    Chuyển đổi từng thành phần của giá trị dấu phẩy động đã chuẩn hóa ``v`` thành các giá trị số nguyên 16 bit, sau đó đóng gói các kết quả vào một số nguyên không dấu 32 bit.

    Phép chuyển đổi thành phần c của ``v`` sang dạng dấu phẩy tĩnh được thực hiện như sau:

    ::

        round(clamp(c, -1.0, 1.0) * 127.0)

    Thành phần thứ nhất của vector sẽ được ghi vào các bit ít quan trọng nhất của đầu ra; thành phần cuối cùng sẽ được ghi vào các bit quan trọng nhất.


    :param v:Một vector các giá trị cần được đóng gói vào một số nguyên không dấu.

    :return:Số nguyên không dấu 32 bit chứa mã hóa đã đóng gói của vector.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/packUnorm.xhtml

.. rst-class:: classref-item-separator

----




.. _shader_func_unpackSnorm4x8:

.. rst-class:: classref-method

vec4 **unpackSnorm4x8**\ (\ uint v) :ref:`🔗<shader_func_unpackSnorm4x8>`

    Giải đóng gói các giá trị dấu phẩy động từ một số nguyên không dấu.

    Giải nén các số nguyên không dấu 32-bit đơn lẻ thành bốn số nguyên có dấu 8-bit. Sau đó, mỗi thành phần được chuyển đổi thành giá trị dấu phẩy động chuẩn hóa để tạo ra vector bốn thành phần được trả về.

    Phép chuyển đổi giá trị dấu phẩy tĩnh f đã giải đóng gói sang dấu phẩy động được thực hiện như sau:

        clamp(f / 127.0, -1.0, 1.0)

    Thành phần thứ nhất của vector được trả về sẽ được trích xuất từ các bit ít quan trọng nhất của đầu vào; thành phần cuối cùng sẽ được trích xuất từ các bit quan trọng nhất.

    :param v:Một số nguyên không dấu chứa các giá trị dấu phẩy động đã đóng gói.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/unpackUnorm.xhtml


.. rst-class:: classref-section-separator

----














.. rst-class:: classref-reftable-group

Các hàm thao tác bit
--------------------

.. table::
    :class: nowrap-col2
    :widths: auto

    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |vec_int_type|  | | :ref:`bitfieldExtract<shader_func_bitfieldExtract>`\ (\ |vec_int_type| value, int offset, int bits)                                       | Extracts a range of bits from an integer.                           |
    | | |vec_uint_type| | | :ref:`bitfieldExtract<shader_func_bitfieldExtract>`\ (\ |vec_uint_type| value, int offset, int bits)                                      |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |vec_int_type|  | | :ref:`bitfieldInsert<shader_func_bitfieldInsert>`\ (\ |vec_int_type| base, |vec_int_type| insert, int offset, int bits)                   | Insert a range of bits into an integer.                             |
    | | |vec_uint_type| | | :ref:`bitfieldInsert<shader_func_bitfieldInsert>`\ (\ |vec_uint_type| base, |vec_uint_type| insert, int offset, int bits)                 |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |vec_int_type|  | | :ref:`bitfieldReverse<shader_func_bitfieldReverse>`\ (\ |vec_int_type| value)                                                             | Reverse the order of bits in an integer.                            |
    | | |vec_uint_type| | | :ref:`bitfieldReverse<shader_func_bitfieldReverse>`\ (\ |vec_uint_type| value)                                                            |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |vec_int_type|  | | :ref:`bitCount<shader_func_bitCount>`\ (\ |vec_int_type| value)                                                                           | Counts the number of 1 bits in an integer.                          |
    | | |vec_uint_type| | | :ref:`bitCount<shader_func_bitCount>`\ (\ |vec_uint_type| value)                                                                          |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |vec_int_type|  | | :ref:`findLSB<shader_func_findLSB>`\ (\ |vec_int_type| value)                                                                             | Find the index of the least significant bit set to 1 in an integer. |
    | | |vec_uint_type| | | :ref:`findLSB<shader_func_findLSB>`\ (\ |vec_uint_type| value)                                                                            |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |vec_int_type|  | | :ref:`findMSB<shader_func_findMSB>`\ (\ |vec_int_type| value)                                                                             | Find the index of the most significant bit set to 1 in an integer.  |
    | | |vec_uint_type| | | :ref:`findMSB<shader_func_findMSB>`\ (\ |vec_uint_type| value)                                                                            |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | | |void|          | | :ref:`imulExtended<shader_func_imulExtended>`\ (\ |vec_int_type| x, |vec_int_type| y, out |vec_int_type| msb, out |vec_int_type| lsb)     | Multiplies two 32-bit numbers and produce a 64-bit result.          |
    | | |void|          | | :ref:`umulExtended<shader_func_umulExtended>`\ (\ |vec_uint_type| x, |vec_uint_type| y, out |vec_uint_type| msb, out |vec_uint_type| lsb) |                                                                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_uint_type|   | :ref:`uaddCarry<shader_func_uaddCarry>`\ (\ |vec_uint_type| x, |vec_uint_type| y, out |vec_uint_type| carry)                                | Adds two unsigned integers and generates carry.                     |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_uint_type|   | :ref:`usubBorrow<shader_func_usubBorrow>`\ (\ |vec_uint_type| x, |vec_uint_type| y, out |vec_uint_type| borrow)                             | Subtracts two unsigned integers and generates borrow.               |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|        | :ref:`ldexp<shader_func_ldexp>`\ (\ |vec_type| x, out |vec_int_type| exp)                                                                   | Assemble a floating-point number from a value and exponent.         |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+
    | |vec_type|        | :ref:`frexp<shader_func_frexp>`\ (\ |vec_type| x, out |vec_int_type| exp)                                                                   | Splits a floating-point number (``x``) into significand integral    |
    |                   |                                                                                                                                             | components                                                          |
    +-------------------+---------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------+


.. rst-class:: classref-descriptions-group

Mô tả các hàm thao tác bit
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. _shader_func_bitfieldExtract:

.. rst-class:: classref-method

|vec_int_type| **bitfieldExtract**\ (\ |vec_int_type| value, int offset, int bits) :ref:`🔗<shader_func_bitfieldExtract>`

    Trích xuất một tập hợp con các bit của ``value`` và trả về tập hợp đó trong các bit ít quan trọng nhất của kết quả. Phạm vi các bit được trích xuất là ``[offset, offset + bits - 1]``.

    Các bit quan trọng nhất của kết quả sẽ được đặt thành zero.

    .. note::
        Nếu bits bằng zero, kết quả sẽ là zero.

    .. warning::
        Kết quả sẽ không xác định nếu:

        - offset hoặc bits là số âm.
        - nếu tổng của offset và bits lớn hơn số bit được dùng để lưu toán hạng.

    :param value:Số nguyên mà từ đó các bit được trích xuất.

    :param offset:Chỉ số của bit đầu tiên cần trích xuất.

    :param bits:Số bit cần trích xuất.

    :return:Số nguyên chứa các bit được yêu cầu.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldExtract.xhtml

.. rst-class:: classref-item-separator

----


.. rst-class:: classref-method

|vec_uint_type| **bitfieldExtract**\ (\ |vec_uint_type| value, int offset, int bits) :ref:`🔗<shader_func_bitfieldExtract>`

    |componentwise|

    Trích xuất một tập hợp con các bit của ``value`` và trả về tập hợp đó trong các bit ít quan trọng nhất của kết quả. Phạm vi các bit được trích xuất là ``[offset, offset + bits - 1]``.

    Các bit quan trọng nhất sẽ được đặt thành giá trị của ``offset + base - 1`` (tức là được sign extend đến độ rộng của kiểu trả về).

    .. note::
        Nếu bits bằng zero, kết quả sẽ là zero.

    .. warning::
        Kết quả sẽ không xác định nếu:

        - offset hoặc bits là số âm.
        - nếu tổng của offset và bits lớn hơn số bit được dùng để lưu toán hạng.

    :param value:Số nguyên mà từ đó các bit được trích xuất.

    :param offset:Chỉ số của bit đầu tiên cần trích xuất.

    :param bits:Số bit cần trích xuất.

    :return:Số nguyên chứa các bit được yêu cầu.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldExtract.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_bitfieldInsert:

.. rst-class:: classref-method

|vec_uint_type| **bitfieldExtract**\ (\ |vec_uint_type| value, int offset, int bits) :ref:`🔗<shader_func_bitfieldInsert>`

.. rst-class:: classref-method

|vec_uint_type| **bitfieldInsert**\ (\ |vec_uint_type| base, |vec_uint_type| insert, int offset, int bits) :ref:`🔗<shader_func_bitfieldInsert>`

    |componentwise|

    Chèn ``bits`` bit ít quan trọng nhất của ``insert`` vào ``base`` tại offset ``offset``.

    Giá trị được trả về sẽ có các bit [offset, offset + bits + 1] được lấy từ [0, bits - 1] của ``insert``, còn tất cả các bit khác được lấy trực tiếp từ các bit tương ứng của base.

    .. note:: Nếu bits bằng zero, kết quả sẽ là giá trị ban đầu của base.

    .. warning::
        Kết quả sẽ không xác định nếu:

        - offset hoặc bits là số âm.
        - nếu tổng của offset và bits lớn hơn số bit được dùng để lưu toán hạng.

    :param base:Số nguyên mà ``insert`` được chèn vào.

    :param insert:Giá trị của các bit cần chèn.

    :param offset:Chỉ số của bit đầu tiên cần chèn.

    :param bits:Số bit cần chèn.

    :return:``base`` với các bit đã chèn.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldInsert.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_bitfieldReverse:

.. rst-class:: classref-method

|vec_int_type| **bitfieldReverse**\ (\ |vec_int_type| value) :ref:`🔗<shader_func_bitfieldReverse>`

.. rst-class:: classref-method

|vec_uint_type| **bitfieldReverse**\ (\ |vec_uint_type| value) :ref:`🔗<shader_func_bitfieldReverse>`

    |componentwise|

    Đảo ngược thứ tự các bit trong một số nguyên.

    Bit có số ``n`` sẽ được lấy từ bit ``(bits - 1) - n`` của ``value``, trong đó bits là tổng số bit được dùng để biểu diễn ``value``.

    :param value:Giá trị có các bit cần đảo ngược.

    :return:``value`` nhưng với các bit đã được đảo ngược.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitfieldReverse.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_bitCount:

.. rst-class:: classref-method

|vec_int_type| **bitCount**\ (\ |vec_int_type| value) :ref:`🔗<shader_func_bitCount>`

.. rst-class:: classref-method

|vec_uint_type| **bitCount**\ (\ |vec_uint_type| value) :ref:`🔗<shader_func_bitCount>`

    |componentwise|

    Đếm số bit 1 trong một số nguyên.

    :param value:Giá trị có các bit cần đếm.

    :return:Số bit được đặt thành 1 trong biểu diễn nhị phân của ``value``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/bitCount.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_findLSB:

.. rst-class:: classref-method

|vec_int_type| **findLSB**\ (\ |vec_int_type| value) :ref:`🔗<shader_func_findLSB>`

.. rst-class:: classref-method

|vec_uint_type| **findLSB**\ (\ |vec_uint_type| value) :ref:`🔗<shader_func_findLSB>`

    |componentwise|

    Tìm chỉ số của bit ít quan trọng nhất được đặt thành ``1``.

    .. note:: Nếu ``value`` bằng không, ``-1`` sẽ được trả về.

    :param value:Giá trị có các bit cần quét.

    :return:Số bit của bit ít quan trọng nhất được đặt thành 1 trong biểu diễn nhị phân của value.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/findLSB.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_findMSB:

.. rst-class:: classref-method

|vec_int_type| **findMSB**\ (\ |vec_int_type| value) :ref:`🔗<shader_func_findMSB>`

.. rst-class:: classref-method

|vec_uint_type| **findMSB**\ (\ |vec_uint_type| value) :ref:`🔗<shader_func_findMSB>`

    |componentwise|

    Tìm chỉ số của bit quan trọng nhất được đặt thành 1.

    .. note::
        Đối với các kiểu số nguyên có dấu, bit dấu được kiểm tra trước, sau đó:
         - Đối với số nguyên dương, kết quả sẽ là số bit của bit quan trọng nhất được đặt thành 1.
         - Đối với số nguyên âm, kết quả sẽ là số bit của bit quan trọng nhất được đặt thành 0.

    .. note:: Đối với giá trị bằng không hoặc âm 1, -1 sẽ được trả về.

    :param value:Giá trị có các bit cần quét.

    :return:Số bit của bit quan trọng nhất được đặt thành 1 trong biểu diễn nhị phân của value.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/findMSB.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_imulExtended:

.. rst-class:: classref-method

|void| **imulExtended**\ (\ |vec_int_type| x, |vec_int_type| y, out |vec_int_type| msb, out |vec_int_type| lsb) :ref:`🔗<shader_func_imulExtended>`

    |componentwise|

    Thực hiện phép nhân có dấu 32 bit với 32 bit để tạo ra kết quả 64 bit.

    32 bit ít quan trọng nhất của tích này được trả về trong ``lsb`` và 32 bit quan trọng nhất được trả về trong ``msb``.

    :param x:Thừa số thứ nhất.

    :param y:Thừa số thứ hai.

    :param msb:Biến nhận word quan trọng nhất của tích.

    :param lsb:Biến nhận word ít quan trọng nhất của tích.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/umulExtended.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_umulExtended:

.. rst-class:: classref-method

|void| **umulExtended**\ (\ |vec_uint_type| x, |vec_uint_type| y, out |vec_uint_type| msb, out |vec_uint_type| lsb) :ref:`🔗<shader_func_umulExtended>`

    |componentwise|

    Thực hiện phép nhân không dấu 32 bit với 32 bit để tạo ra kết quả 64 bit.

    32 bit ít quan trọng nhất của tích này được trả về trong ``lsb`` và 32 bit quan trọng nhất được trả về trong ``msb``.

    :param x:Thừa số thứ nhất.

    :param y:Thừa số thứ hai.

    :param msb:Biến nhận word quan trọng nhất của tích.

    :param lsb:Biến nhận word ít quan trọng nhất của tích.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/umulExtended.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_uaddCarry:

.. rst-class:: classref-method

|vec_uint_type| **uaddCarry**\ (\ |vec_uint_type| x, |vec_uint_type| y, out |vec_uint_type| carry) :ref:`🔗<shader_func_uaddCarry>`

    |componentwise|

    Cộng các số nguyên không dấu và tạo carry.

    cộng hai biến số nguyên không dấu 32 bit (scalar hoặc vector) và tạo ra một kết quả số nguyên không dấu 32 bit cùng với một đầu ra carry. Giá trị carry là .

    :param x:Toán hạng thứ nhất.

    :param y:Toán hạng thứ hai.

    :param carry:0 nếu tổng nhỏ hơn 2\ :sup:`32`, nếu không thì là 1.

    :return:
        ``(x + y) % 2^32``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/uaddCarry.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_usubBorrow:

.. rst-class:: classref-method

|vec_uint_type| **usubBorrow**\ (\ |vec_uint_type| x, |vec_uint_type| y, out |vec_uint_type| borrow) :ref:`🔗<shader_func_usubBorrow>`

    |componentwise|

    Trừ các số nguyên không dấu và tạo borrow.

    :param x:Toán hạng thứ nhất.

    :param y:Toán hạng thứ hai.

    :param borrow:``0`` nếu ``x >= y``, nếu không thì ``1``.

    :return:Hiệu của ``x`` và ``y`` nếu không âm, hoặc 2\ :sup:`32` cộng với hiệu đó trong trường hợp ngược lại.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/usubBorrow.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_ldexp:

.. rst-class:: classref-method

|vec_type| **ldexp**\ (\ |vec_type| x, out |vec_int_type| exp) :ref:`🔗<shader_func_ldexp>`

    |componentwise|

    Tạo một số dấu phẩy động từ một giá trị và số mũ.

    .. warning::
        Nếu tích này quá lớn để biểu diễn trong kiểu dấu phẩy động, kết quả là không xác định.

    :param x:Giá trị được dùng làm nguồn của significand.

    :param exp:Giá trị được dùng làm nguồn của số mũ.

    :return:
        ``x * 2^exp``

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/ldexp.xhtml

.. rst-class:: classref-item-separator

----


.. _shader_func_frexp:

.. rst-class:: classref-method

|vec_type| **frexp**\ (\ |vec_type| x, out |vec_int_type| exp) :ref:`🔗<shader_func_frexp>`

    |componentwise|

    Trích xuất ``x`` thành một significand dấu phẩy động trong phạm vi ``[0.5, 1.0)`` và một số mũ nguyên của hai, sao cho:

    ::

        x = significand * 2 ^ exponent

    Đối với giá trị dấu phẩy động bằng không, significand và số mũ đều bằng không.

    .. warning:: Đối với giá trị dấu phẩy động là vô cực hoặc NaN dấu phẩy động, kết quả là không xác định.

    :param x:Giá trị từ đó significand và số mũ sẽ được trích xuất.

    :param exp:Biến dùng để chứa số mũ của ``x``.

    :return:Significand của ``x``.

    https://www.khronos.org/registry/OpenGL-Refpages/gl4/html/frexp.xhtml


.. rst-class:: classref-section-separator

----




.. |void| replace:: :abbr:`void (Không có giá trị trả về.)`
.. |vec_type| replace:: :abbr:`vec_type (Một trong các kiểu: float, vec2, vec3, vec4)`
.. |vec_int_type| replace:: :abbr:`vec_int_type (Một trong các kiểu: int, ivec2, ivec3, ivec4)`
.. |vec_uint_type| replace:: :abbr:`vec_uint_type (Một trong các kiểu: uint, uvec2, uvec3, uvec4)`
.. |vec_bool_type| replace:: :abbr:`vec_bool_type (Một trong các kiểu: bool, bvec2, bvec3, bvec4)`
.. |gsampler2D| replace:: :abbr:`gsampler2D (Một trong các kiểu: sampler2D, isampler2D, uSampler2D)`
.. |gsampler2DArray| replace:: :abbr:`gsampler2DArray (Một trong các kiểu: sampler2DArray, isampler2DArray, uSampler2DArray)`
.. |gsampler3D| replace:: :abbr:`gsampler3D (Một trong các kiểu: sampler3D, isampler3D, uSampler3D)`
.. |mat_type| replace:: :abbr:`mat_type (Một trong các kiểu: mat2, mat3, mat4)`
.. |gvec4_type| replace:: :abbr:`gvec4_type (Một trong các kiểu: vec4, ivec4, uvec4)`
.. |componentwise| replace:: :ref:`Hàm theo từng thành phần <shading_componentwise>`.

.. _`GLSL Language Specification`: http://www.opengl.org/registry/doc/GLSLangSpec.4.30.6.pdf
