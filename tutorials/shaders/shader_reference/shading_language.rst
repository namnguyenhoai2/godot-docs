.. _doc_shading_language:

Ngôn ngữ shading
================

Giới thiệu
----------

Godot sử dụng một ngôn ngữ shading tương tự như GLSL ES 3.0. Hầu hết các kiểu dữ liệu và hàm đều được hỗ trợ, còn một số ít kiểu và hàm còn lại có thể sẽ được bổ sung theo thời gian.

Nếu bạn đã quen thuộc với GLSL, :ref:`Godot Shader Migration Guide<doc_converting_glsl_to_godot_shaders>` là một tài nguyên sẽ giúp bạn chuyển từ GLSL thông thường sang ngôn ngữ shading của Godot.

.. _doc_shading_language_data_types:

Kiểu dữ liệu
------------

Hầu hết các kiểu dữ liệu GLSL ES 3.0 đều được hỗ trợ:

+------------------------+---------------------------------------------------------------------------------+
| Type                   | Description                                                                     |
+========================+=================================================================================+
| **void**               | Void datatype, useful only for functions that return nothing.                   |
+------------------------+---------------------------------------------------------------------------------+
| **bool**               | Boolean datatype, can only contain ``true`` or ``false``.                       |
+------------------------+---------------------------------------------------------------------------------+
| **bvec2**              | Two-component vector of booleans.                                               |
+------------------------+---------------------------------------------------------------------------------+
| **bvec3**              | Three-component vector of booleans.                                             |
+------------------------+---------------------------------------------------------------------------------+
| **bvec4**              | Four-component vector of booleans.                                              |
+------------------------+---------------------------------------------------------------------------------+
| **int**                | 32 bit signed scalar integer.                                                   |
+------------------------+---------------------------------------------------------------------------------+
| **ivec2**              | Two-component vector of signed integers.                                        |
+------------------------+---------------------------------------------------------------------------------+
| **ivec3**              | Three-component vector of signed integers.                                      |
+------------------------+---------------------------------------------------------------------------------+
| **ivec4**              | Four-component vector of signed integers.                                       |
+------------------------+---------------------------------------------------------------------------------+
| **uint**               | Unsigned scalar integer; can't contain negative numbers.                        |
+------------------------+---------------------------------------------------------------------------------+
| **uvec2**              | Two-component vector of unsigned integers.                                      |
+------------------------+---------------------------------------------------------------------------------+
| **uvec3**              | Three-component vector of unsigned integers.                                    |
+------------------------+---------------------------------------------------------------------------------+
| **uvec4**              | Four-component vector of unsigned integers.                                     |
+------------------------+---------------------------------------------------------------------------------+
| **float**              | 32 bit floating-point scalar.                                                   |
+------------------------+---------------------------------------------------------------------------------+
| **vec2**               | Two-component vector of floating-point values.                                  |
+------------------------+---------------------------------------------------------------------------------+
| **vec3**               | Three-component vector of floating-point values.                                |
+------------------------+---------------------------------------------------------------------------------+
| **vec4**               | Four-component vector of floating-point values.                                 |
+------------------------+---------------------------------------------------------------------------------+
| **mat2**               | 2x2 matrix, in column major order.                                              |
+------------------------+---------------------------------------------------------------------------------+
| **mat3**               | 3x3 matrix, in column major order.                                              |
+------------------------+---------------------------------------------------------------------------------+
| **mat4**               | 4x4 matrix, in column major order.                                              |
+------------------------+---------------------------------------------------------------------------------+
| **sampler2D**          | Sampler type for binding 2D textures, which are read as float.                  |
+------------------------+---------------------------------------------------------------------------------+
| **isampler2D**         | Sampler type for binding 2D textures, which are read as signed integer.         |
+------------------------+---------------------------------------------------------------------------------+
| **usampler2D**         | Sampler type for binding 2D textures, which are read as unsigned integer.       |
+------------------------+---------------------------------------------------------------------------------+
| **sampler2DArray**     | Sampler type for binding 2D texture arrays, which are read as float.            |
+------------------------+---------------------------------------------------------------------------------+
| **isampler2DArray**    | Sampler type for binding 2D texture arrays, which are read as signed integer.   |
+------------------------+---------------------------------------------------------------------------------+
| **usampler2DArray**    | Sampler type for binding 2D texture arrays, which are read as unsigned integer. |
+------------------------+---------------------------------------------------------------------------------+
| **sampler3D**          | Sampler type for binding 3D textures, which are read as float.                  |
+------------------------+---------------------------------------------------------------------------------+
| **isampler3D**         | Sampler type for binding 3D textures, which are read as signed integer.         |
+------------------------+---------------------------------------------------------------------------------+
| **usampler3D**         | Sampler type for binding 3D textures, which are read as unsigned integer.       |
+------------------------+---------------------------------------------------------------------------------+
| **samplerCube**        | Sampler type for binding Cubemaps, which are read as float.                     |
+------------------------+---------------------------------------------------------------------------------+
| **samplerCubeArray**   | Sampler type for binding Cubemap arrays, which are read as float.               |
|                        | Only supported in Forward+ and Mobile, not Compatibility.                       |
+------------------------+---------------------------------------------------------------------------------+
| **samplerExternalOES** | External sampler type.                                                          |
|                        | Only supported in Compatibility/Android platform.                               |
+------------------------+---------------------------------------------------------------------------------+

Các kiểu này cũng có thể được đặt bên trong :ref:`arrays <doc_shading_language_arrays>` hoặc :ref:`structs <doc_shading_language_structs>`, vốn cũng có thể được sử dụng làm tham số hoặc giá trị trả về của hàm. Array có thể được sử dụng làm uniform, nhưng struct thì không.

.. warning::

    Các biến cục bộ không được khởi tạo bằng một giá trị mặc định như ``0.0``. Nếu bạn sử dụng một biến trước khi gán giá trị cho nó, biến đó sẽ chứa bất kỳ giá trị nào đã có sẵn tại vị trí bộ nhớ đó, và các lỗi hiển thị không thể dự đoán sẽ xuất hiện. Tuy nhiên, uniform và varying được khởi tạo bằng một giá trị mặc định.

Comment
~~~~~~~

Ngôn ngữ shading hỗ trợ cùng cú pháp comment được sử dụng trong C# và C++, dùng ``//`` cho comment một dòng và ``/* */`` cho comment nhiều dòng:

.. code-block:: glsl

    // Comment một dòng.
    int a = 2;  // Một comment một dòng khác.

    /*
    Multi-line comment.
    The comment ends when the ending delimiter is found
    (here, it's on the line below).
    */
    int b = 3;

Ngoài ra, bạn có thể sử dụng comment tài liệu, được hiển thị trong inspector khi di chuột lên một tham số shader. Hiện tại, comment tài liệu chỉ được hỗ trợ khi đặt ngay phía trên khai báo ``uniform``. Các comment tài liệu này chỉ hỗ trợ cú pháp comment **nhiều dòng** (ngay cả khi được sử dụng trên một dòng) và phải dùng **hai** dấu hoa thị ở đầu (``/**``) thay vì chỉ một dấu (``/*``):

.. code-block:: glsl

    /**
     * Đây là một comment tài liệu.
     * Các dòng này sẽ xuất hiện trong inspector khi di chuột lên tham số shader
     * có tên "Something".
     * Bạn có thể sử dụng định dạng [b]BBCode[/b] [i]trong comment[/i].
     */
    uniform int something = 1;

    /** Đây là một comment tài liệu một dòng. */
    uniform float something_else = 1.0;

Các dấu hoa thị ở những dòng tiếp theo không bắt buộc, nhưng được khuyến nghị theo :ref:`doc_shaders_style_guide`. Các dấu hoa thị này sẽ được inspector tự động loại bỏ, nên chúng sẽ không xuất hiện trong tooltip.

Ép kiểu
~~~~~~~

Giống như GLSL ES 3.0, không cho phép ép kiểu ngầm định giữa các scalar và vector có cùng kích thước nhưng khác kiểu. Việc ép kiểu giữa các kiểu có kích thước khác nhau cũng không được phép. Việc chuyển đổi phải được thực hiện tường minh thông qua các constructor.

Ví dụ:

.. code-block:: glsl

    float a = 2; // không hợp lệ
    float a = 2.0; // hợp lệ
    float a = float(2); // hợp lệ

Các hằng số integer mặc định là signed, vì vậy luôn cần ép kiểu để chuyển đổi sang unsigned:

.. code-block:: glsl

    int a = 2; // hợp lệ
    uint a = 2; // không hợp lệ
    uint a = uint(2); // hợp lệ

Các thành phần
~~~~~~~~~~~~~~

Các thành phần scalar riêng lẻ của kiểu vector được truy cập thông qua các thành phần "x", "y", "z" và "w". Ngoài ra, việc sử dụng "r", "g", "b" và "a" cũng hoạt động và tương đương. Hãy sử dụng cách phù hợp nhất với nhu cầu của bạn.

Đối với matrix, hãy sử dụng cú pháp lập chỉ mục ``m[column][row]`` để truy cập từng scalar, hoặc ``m[column]`` để truy cập một vector theo chỉ mục cột. Ví dụ, để truy cập thành phần y của phép tịnh tiến từ một matrix biến đổi mat4 (cột thứ 4, dòng thứ 2), bạn sử dụng ``m[3][1]`` hoặc ``m[3].y``.

Khởi tạo
~~~~~~~~

Việc khởi tạo các kiểu vector luôn phải truyền vào:

.. code-block:: glsl

    // Số lượng scalar bắt buộc
    vec4 a = vec4(0.0, 1.0, 2.0, 3.0);
    // Các vector và/hoặc scalar bổ sung
    vec4 a = vec4(vec2(0.0, 1.0), vec2(2.0, 3.0));
    vec4 a = vec4(vec3(0.0, 1.0, 2.0), 3.0);
    // Một scalar duy nhất cho toàn bộ vector
    vec4 a = vec4(0.0);

Việc khởi tạo các kiểu matrix yêu cầu các vector có cùng số chiều với matrix, được diễn giải như các cột. Bạn cũng có thể tạo một matrix đường chéo bằng cú pháp ``matx(float)``. Theo đó, ``mat4(1.0)`` là một identity matrix.

.. code-block:: glsl

    mat2 m2 = mat2(vec2(1.0, 0.0), vec2(0.0, 1.0));
    mat3 m3 = mat3(vec3(1.0, 0.0, 0.0), vec3(0.0, 1.0, 0.0), vec3(0.0, 0.0, 1.0));
    mat4 identity = mat4(1.0);

Matrix cũng có thể được tạo từ một matrix có số chiều khác. Có hai quy tắc:

1. Nếu một matrix lớn hơn được tạo từ một matrix nhỏ hơn, các dòng và cột bổ sung sẽ được đặt thành những giá trị tương ứng trong một identity matrix. 1. Nếu một matrix nhỏ hơn được tạo từ một matrix lớn hơn, submatrix phía trên, bên trái của matrix lớn hơn sẽ được sử dụng.

.. code-block:: glsl

    mat3 basis = mat3(MODEL_MATRIX);
    mat4 m4 = mat4(basis);
    mat2 m2 = mat2(m4);

Swizzling
~~~~~~~~~

Có thể lấy bất kỳ tổ hợp nào của các thành phần theo bất kỳ thứ tự nào, miễn là kết quả là một kiểu vector khác (hoặc scalar). Điều này dễ minh họa hơn là giải thích:

.. code-block:: glsl

    vec4 a = vec4(0.0, 1.0, 2.0, 3.0);
    vec3 b = a.rgb; // Tạo một vec3 với các thành phần của vec4.
    vec3 b = a.ggg; // Cũng hợp lệ; tạo một vec3 và điền vào đó một thành phần duy nhất của vec4.
    vec3 b = a.bgr; // "b" sẽ là vec3(2.0, 1.0, 0.0).
    vec3 b = a.xyz; // rgba và xyzw cũng tương đương.
    vec3 b = a.stp; // Và stpq (dùng cho tọa độ texture).
    float c = b.w; // Không hợp lệ vì "w" không tồn tại trong vec3 b.
    vec3 c = b.xrt; // Không hợp lệ vì không được phép trộn các kiểu khác nhau.
    b.rrr = a.rgb; // Không hợp lệ vì phép gán có thành phần trùng lặp.
    b.bgr = a.rgb; // Phép gán hợp lệ. Thành phần "blue" của "b" sẽ là thành phần "red" của "a" và ngược lại.

Độ chính xác
~~~~~~~~~~~~

Có thể thêm các modifier độ chính xác vào kiểu dữ liệu; hãy sử dụng chúng cho uniform, biến, đối số và varying:

.. code-block:: glsl

    lowp vec4 a = vec4(0.0, 1.0, 2.0, 3.0); // độ chính xác thấp, thường là 8 bit cho mỗi thành phần được ánh xạ vào khoảng 0-1
    mediump vec4 a = vec4(0.0, 1.0, 2.0, 3.0); // độ chính xác trung bình, thường là 16 bit hoặc half float
    highp vec4 a = vec4(0.0, 1.0, 2.0, 3.0); // độ chính xác cao, sử dụng toàn bộ phạm vi float hoặc integer (mặc định 32 bit)


Sử dụng độ chính xác thấp hơn cho một số phép toán có thể tăng tốc các phép tính liên quan (đổi lại độ chính xác thấp hơn). Điều này hiếm khi cần thiết trong hàm vertex processor (nơi hầu hết thời gian cần độ chính xác đầy đủ), nhưng thường hữu ích trong fragment processor.

Một số kiến trúc (chủ yếu là mobile) có thể hưởng lợi đáng kể từ việc này, nhưng cũng có các nhược điểm như chi phí bổ sung do chuyển đổi giữa các mức độ chính xác. Hãy tham khảo tài liệu của kiến trúc đích để biết thêm thông tin. Trong nhiều trường hợp, driver mobile gây ra hành vi không nhất quán hoặc không mong đợi, và tốt nhất là tránh chỉ định độ chính xác trừ khi cần thiết.

.. _doc_shading_language_arrays:

Array
-----

Array là các container chứa nhiều biến có kiểu tương tự.

Array cục bộ
~~~~~~~~~~~~

Array cục bộ được khai báo trong các hàm. Chúng có thể sử dụng tất cả các kiểu dữ liệu được cho phép, ngoại trừ sampler. Khai báo array tuân theo cú pháp kiểu C: ``[const] + [precision] + typename + identifier + [array size]``.

.. code-block:: glsl

    void fragment() {
        float arr[3];
    }

Chúng có thể được khởi tạo ở phần đầu như sau:

.. code-block:: glsl

    float float_arr[3] = float[3] (1.0, 0.5, 0.0); // constructor thứ nhất

    int int_arr[3] = int[] (2, 1, 0); // constructor thứ hai

    vec2 vec2_arr[3] = { vec2(1.0, 1.0), vec2(0.5, 0.5), vec2(0.0, 0.0) }; // constructor thứ ba

    bool bool_arr[] = { true, true, false }; // constructor thứ tư - kích thước được tự động xác định từ số lượng phần tử

Bạn có thể khai báo nhiều array (ngay cả với các kích thước khác nhau) trong một biểu thức:

.. code-block:: glsl

    float a[3] = float[3] (1.0, 0.5, 0.0),
    b[2] = { 1.0, 0.5 },
    c[] = { 0.7 },
    d = 0.0,
    e[5];

Để truy cập một phần tử array, hãy sử dụng cú pháp lập chỉ mục:

.. code-block:: glsl

    float arr[3];

    arr[0] = 1.0; // setter

    COLOR.r = arr[0]; // getter

Array cũng có một hàm tích hợp sẵn ``.length()`` (không được nhầm lẫn với hàm tích hợp sẵn ``length()``). Hàm này không nhận tham số nào và sẽ trả về kích thước của array.

.. code-block:: glsl

    float arr[] = { 0.0, 1.0, 0.5, -1.0 };
    for (int i = 0; i < arr.length(); i++) {
        // ...
    }

.. note::

    Nếu bạn sử dụng một chỉ mục nhỏ hơn 0 hoặc lớn hơn kích thước array - shader sẽ bị crash và quá trình rendering bị dừng. Để ngăn điều này, hãy sử dụng các hàm ``length()``, ``if`` hoặc ``clamp()`` để đảm bảo chỉ mục nằm trong khoảng từ 0 đến độ dài của array. Luôn kiểm tra và thử nghiệm code của bạn cẩn thận. Nếu bạn truyền vào một biểu thức hằng hoặc một số, editor sẽ kiểm tra giới hạn của nó để ngăn lỗi crash này.

Array toàn cục
~~~~~~~~~~~~~~

Bạn có thể khai báo array trong phạm vi toàn cục dưới dạng ``const`` hoặc ``uniform``:

.. code-block:: glsl

    shader_type spatial;

    const lowp vec3 v[1] = lowp vec3[1] ( vec3(0, 0, 1) );
    uniform lowp vec3 w[1];

    void fragment() {
      ALBEDO = v[0] + w[0];
    }

.. note::

    Array toàn cục sử dụng cùng cú pháp với array cục bộ, ngoại trừ việc có thêm ``const`` hoặc ``uniform`` vào khai báo. Lưu ý rằng array uniform không thể có giá trị mặc định.

Hằng số
-------

Sử dụng từ khóa ``const`` trước khai báo biến để biến đó trở nên bất biến, nghĩa là không thể sửa đổi. Tất cả các kiểu cơ bản, ngoại trừ sampler, đều có thể được khai báo dưới dạng hằng số. Việc truy cập và sử dụng một giá trị hằng số nhanh hơn một chút so với uniform. Hằng số phải được khởi tạo ngay khi khai báo.

.. code-block:: glsl

    const vec2 a = vec2(0.0, 1.0);
    vec2 b;

    a = b; // không hợp lệ
    b = a; // hợp lệ

Hằng số không thể được sửa đổi và cũng không thể có hint, nhưng có thể khai báo nhiều hằng số (nếu chúng có cùng kiểu) trong một biểu thức duy nhất, ví dụ

.. code-block:: glsl

    const vec2 V1 = vec2(1, 1), V2 = vec2(2, 2);

Tương tự như biến, array cũng có thể được khai báo với ``const``.

.. code-block:: glsl

    const float arr[] = { 1.0, 0.5, 0.0 };

    arr[0] = 1.0; // không hợp lệ

    COLOR.r = arr[0]; // hợp lệ

Hằng số có thể được khai báo ở cả phạm vi toàn cục (bên ngoài mọi hàm) hoặc cục bộ (bên trong một hàm). Hằng số toàn cục hữu ích khi bạn muốn truy cập một giá trị trong toàn bộ shader mà không cần sửa đổi giá trị đó. Giống như uniform, hằng số toàn cục được dùng chung giữa tất cả các stage của shader, nhưng không thể được truy cập bên ngoài shader.

.. code-block:: glsl

    shader_type spatial;

    const float GOLDEN_RATIO = 1.618033988749894;

Các hằng số thuộc kiểu ``float`` phải được khởi tạo bằng ký hiệu ``.`` sau phần thập phân hoặc bằng cách sử dụng ký hiệu khoa học. Hậu tố ``f`` tùy chọn cũng được hỗ trợ.

.. code-block:: glsl

    float a = 1.0;
    float b = 1.0f; // giống nhau, sử dụng hậu tố để rõ ràng hơn
    float c = 1e-1; // cho kết quả 0.1 bằng cách sử dụng ký hiệu khoa học

Các hằng số thuộc kiểu ``uint`` (unsigned int) phải có hậu tố ``u`` để phân biệt với integer signed. Ngoài ra, có thể thực hiện việc này bằng cách sử dụng hàm chuyển đổi tích hợp sẵn ``uint(x)``.

.. code-block:: glsl

    uint a = 1u;
    uint b = uint(1);

.. _doc_shading_language_structs:

Struct
------

Struct là các kiểu hợp thành, có thể được sử dụng để trừu tượng hóa code shader tốt hơn. Bạn có thể khai báo chúng ở phạm vi global như sau:

.. code-block:: glsl

    struct PointLight {
        vec3 position;
        vec3 color;
        float intensity;
    };

Sau khi khai báo, bạn có thể khởi tạo và gán giá trị ban đầu cho chúng như sau:

.. code-block:: glsl

    void fragment()
    {
        PointLight light;
        light.position = vec3(0.0);
        light.color = vec3(1.0, 0.0, 0.0);
        light.intensity = 0.5;
    }

Hoặc sử dụng struct constructor cho cùng mục đích:

.. code-block:: glsl

    PointLight light = PointLight(vec3(0.0), vec3(1.0, 0.0, 0.0), 0.5);

Struct có thể chứa struct hoặc array khác; bạn cũng có thể khởi tạo chúng dưới dạng hằng số global:

.. code-block:: glsl

    shader_type spatial;

    ...

    struct Scene {
        PointLight lights[2];
    };

    const Scene scene = Scene(PointLight[2](PointLight(vec3(0.0, 0.0, 0.0), vec3(1.0, 0.0, 0.0), 1.0), PointLight(vec3(0.0, 0.0, 0.0), vec3(1.0, 0.0, 0.0), 1.0)));

    void fragment()
    {
        ALBEDO = scene.lights[0].color;
    }

Bạn cũng có thể truyền chúng vào các hàm:

.. code-block:: glsl

    shader_type canvas_item;

    ...

    Scene construct_scene(PointLight light1, PointLight light2) {
        return Scene({light1, light2});
    }

    void fragment()
    {
        COLOR.rgb = construct_scene(PointLight(vec3(0.0, 0.0, 0.0), vec3(1.0, 0.0, 0.0), 1.0), PointLight(vec3(0.0, 0.0, 0.0), vec3(1.0, 0.0, 1.0), 1.0)).lights[0].color;
    }

Các toán tử
-----------

Ngôn ngữ shading của Godot hỗ trợ cùng một tập toán tử như GLSL ES 3.0. Dưới đây là danh sách các toán tử theo thứ tự precedence:

.. table::
    :class: nowrap-col3

    +-------------+------------------------+------------------+
    | Precedence  | Class                  | Operator         |
    +-------------+------------------------+------------------+
    | 1 (highest) | parenthetical grouping | **()**           |
    +-------------+------------------------+------------------+
    | 2           | unary                  | **+, -, !, ~**   |
    +-------------+------------------------+------------------+
    | 3           | multiplicative         | **/, \*, %**     |
    +-------------+------------------------+------------------+
    | 4           | additive               | **+, -**         |
    +-------------+------------------------+------------------+
    | 5           | bit-wise shift         | **<<, >>**       |
    +-------------+------------------------+------------------+
    | 6           | relational             | **<, >, <=, >=** |
    +-------------+------------------------+------------------+
    | 7           | equality               | **==, !=**       |
    +-------------+------------------------+------------------+
    | 8           | bit-wise AND           | **&**            |
    +-------------+------------------------+------------------+
    | 9           | bit-wise exclusive OR  | **^**            |
    +-------------+------------------------+------------------+
    | 10          | bit-wise inclusive OR  | **|**            |
    +-------------+------------------------+------------------+
    | 11          | logical AND            | **&&**           |
    +-------------+------------------------+------------------+
    | 12 (lowest) | logical inclusive OR   | **||**           |
    +-------------+------------------------+------------------+

.. note::

    Hầu hết các toán tử nhận vector hoặc matrix (phép nhân, phép chia, v.v.) đều hoạt động theo từng component, nghĩa là hàm được áp dụng cho giá trị đầu tiên của mỗi vector, sau đó là giá trị thứ hai của mỗi vector, v.v. Một số ví dụ:

    .. table::
        :class: nowrap-col2 nowrap-col1
        :widths: auto

        +---------------------------------------+------------------------------------------------------+
        | Operation                             | Equivalent Scalar Operation                          |
        +=======================================+======================================================+
        | ``vec3(4, 5, 6) + 2``                 | ``vec3(4 + 2, 5 + 2, 6 + 2)``                        |
        +---------------------------------------+------------------------------------------------------+
        | ``vec2(3, 4) * vec2(10, 20)``         | ``vec2(3 * 10, 4 * 20)``                             |
        +---------------------------------------+------------------------------------------------------+
        | ``mat2(vec2(1, 2), vec2(3, 4)) + 10`` | ``mat2(vec2(1 + 10, 2 + 10), vec2(3 + 10, 4 + 10))`` |
        +---------------------------------------+------------------------------------------------------+

    `GLSL Language Specification <http://www.opengl.org/registry/doc/GLSLangSpec.4.30.6.pdf>`_ viết trong mục 5.10 Vector and Matrix Operations:

        Ngoại trừ một vài trường hợp, các phép toán được thực hiện theo từng component. Thông thường, khi một toán tử hoạt động trên một vector hoặc matrix, nó sẽ hoạt động độc lập trên từng component của vector hoặc matrix đó. [...] Các trường hợp ngoại lệ là matrix nhân với vector, vector nhân với matrix và matrix nhân với matrix. Những phép toán này không hoạt động theo từng component mà thực hiện phép nhân đại số tuyến tính phù hợp.

Điều khiển luồng
----------------

Ngôn ngữ Shading của Godot hỗ trợ các kiểu điều khiển luồng phổ biến nhất:

.. code-block:: glsl

    // `if`, `else if` và `else`.
    if (cond) {

    } else if (other_cond) {

    } else {

    }

    // Toán tử ba ngôi.
    // Đây là một biểu thức hoạt động giống như `if`/`else` và trả về giá trị.
    // Nếu `cond` được đánh giá là `true`, `result` sẽ là `9`.
    // Nếu không, `result` sẽ là `5`.
    int result = cond ? 9 : 5;

    // `switch`.
    switch (i) { // `i` phải là một biểu thức số nguyên có dấu.
        case -1:
            break;
        case 0:
            return; // `break` hoặc `return` để tránh chạy `case` tiếp theo.
        case 1: // Fallthrough (không có `break` hoặc `return`): sẽ chạy `case` tiếp theo.
        case 2:
            break;
        //...
        default: // Chỉ chạy nếu không có `case` nào ở trên khớp. Tùy chọn.
            break;
    }

    // Vòng lặp `for`. Phù hợp nhất khi số lượng phần tử cần lặp qua
    // đã được biết trước.
    for (int i = 0; i < 10; i++) {

    }

    // Vòng lặp `while`. Phù hợp nhất khi số lượng phần tử cần lặp qua
    // chưa được biết trước.
    while (cond) {

    }

    // `do while`. Tương tự `while`, nhưng luôn chạy ít nhất một lần ngay cả khi `cond`
    // không bao giờ được đánh giá là `true`.
    do {

    } while (cond);

Hãy nhớ rằng trên các GPU hiện đại, vòng lặp vô hạn có thể xảy ra và làm treo ứng dụng của bạn (bao gồm cả editor). Godot không thể bảo vệ bạn khỏi điều này, vì vậy hãy cẩn thận để không mắc phải sai lầm này!

Ngoài ra, khi so sánh các giá trị floating-point với một số, hãy đảm bảo so sánh chúng với một *range* thay vì một số chính xác.

Một phép so sánh như ``if (value == 0.3)`` có thể không được đánh giá là ``true``. Phép toán floating-point thường mang tính xấp xỉ và có thể không như mong đợi. Nó cũng có thể hoạt động khác nhau tùy thuộc vào phần cứng.

**Không** làm như vậy.

.. code-block:: glsl

    float value = 0.1 + 0.2;

    // Có thể không được đánh giá là `true`!
    if (value == 0.3) {
        // ...
    }

Thay vào đó, luôn thực hiện phép so sánh theo range với một giá trị epsilon. Số floating-point càng lớn (và càng kém chính xác), giá trị epsilon càng phải lớn.

.. code-block:: glsl

    const float EPSILON = 0.0001;
    if (value >= 0.3 - EPSILON && value <= 0.3 + EPSILON) {
        // ...
    }

Xem `floating-point-gui.de <https://floating-point-gui.de/>`__ để biết thêm thông tin.

Loại bỏ
-------

Các hàm fragment, light và custom (được gọi từ fragment hoặc light) có thể sử dụng từ khóa ``discard``. Nếu được sử dụng, fragment sẽ bị loại bỏ và không có gì được ghi.

Hãy lưu ý rằng ``discard`` có chi phí hiệu năng khi được sử dụng, vì nó sẽ khiến depth prepass không thể hoạt động hiệu quả trên mọi surface sử dụng shader. Ngoài ra, một pixel bị loại bỏ vẫn cần được render trong vertex shader, nghĩa là shader sử dụng ``discard`` trên tất cả pixel vẫn tốn nhiều chi phí render hơn so với việc ngay từ đầu không render bất kỳ object nào.

Các hàm
-------

Bạn có thể định nghĩa các hàm trong shader Godot. Chúng sử dụng cú pháp sau:

.. code-block:: glsl

    ret_type func_name(args) {
        return ret_type; // nếu trả về một giá trị
    }

    // một ví dụ cụ thể hơn:

    int sum2(int a, int b) {
        return a + b;
    }


Bạn chỉ có thể sử dụng các hàm đã được định nghĩa ở phía trên (cao hơn trong editor) hàm mà bạn đang gọi chúng từ đó. Việc định nghĩa lại một hàm đã được định nghĩa ở phía trên (hoặc tên của một hàm built-in) sẽ gây ra lỗi.

Các đối số của hàm có thể có những qualifier đặc biệt:

* **in**: Có nghĩa là đối số chỉ dùng để đọc (mặc định). * **out**: Có nghĩa là đối số chỉ dùng để ghi. * **inout**: Có nghĩa là đối số được truyền hoàn toàn qua reference. * **const**: Có nghĩa là đối số là một hằng số và không thể thay đổi; có thể kết hợp với qualifier **in**.

Ví dụ bên dưới:

.. code-block:: glsl

    void sum2(int a, int b, inout int result) {
        result = a + b;
    }

Function overloading được hỗ trợ. Bạn có thể định nghĩa nhiều hàm cùng tên nhưng có các đối số khác nhau. Lưu ý rằng `implicit casting <Casting_>`_ trong các lời gọi overloaded function không được phép, chẳng hạn như từ ``int`` đến ``float`` (``1`` đến ``1.0``).

.. code-block:: glsl

    vec3 get_color(int t) {
        return vec3(1, 0, 0); // Màu đỏ.
    }
    vec3 get_color(float t) {
        return vec3(0, 1, 0); // Màu xanh lá.
    }
    void fragment() {
        vec3 red = get_color(1);
        vec3 green = get_color(1.0);
    }

.. _doc_shading_language_varyings:

Varying
-------

Để gửi dữ liệu từ hàm xử lý vertex đến hàm xử lý fragment (hoặc light), ta sử dụng *varying*. Chúng được thiết lập cho mọi vertex của primitive trong *vertex processor*, và giá trị được nội suy cho mọi pixel trong *fragment processor*.

.. code-block:: glsl

    shader_type spatial;

    varying vec3 some_color;

    void vertex() {
        some_color = NORMAL; // Biến normal thành màu.
    }

    void fragment() {
        ALBEDO = some_color;
    }

    void light() {
        DIFFUSE_LIGHT = some_color * 100; // tùy chọn
    }

Varying cũng có thể là một array:

.. code-block:: glsl

    shader_type spatial;

    varying float var_arr[3];

    void vertex() {
        var_arr[0] = 1.0;
        var_arr[1] = 0.0;
    }

    void fragment() {
        ALBEDO = vec3(var_arr[0], var_arr[1], var_arr[2]); // màu đỏ
    }

Bạn cũng có thể gửi dữ liệu từ *fragment* đến *light processor* bằng từ khóa *varying*. Để làm vậy, bạn có thể gán giá trị cho nó trong *fragment*, sau đó sử dụng nó trong hàm *light*.

.. code-block:: glsl

    shader_type spatial;

    varying vec3 some_light;

    void fragment() {
        some_light = ALBEDO * 100.0; // Tạo ánh sáng phát sáng.
    }

    void light() {
        DIFFUSE_LIGHT = some_light;
    }

Lưu ý rằng varying không thể được gán trong các hàm custom hoặc một hàm *light processor*, chẳng hạn như:

.. code-block:: glsl

    shader_type spatial;

    varying float test;

    void foo() {
        test = 0.0; // Lỗi.
    }

    void vertex() {
        test = 0.0;
    }

    void light() {
        test = 0.0; // Cũng có lỗi.
    }

Giới hạn này được đưa ra để ngăn việc sử dụng không chính xác trước khi khởi tạo.

Interpolation qualifier
-----------------------

Một số giá trị được nội suy trong quá trình shading pipeline. Bạn có thể sửa đổi cách thực hiện các phép nội suy này bằng cách sử dụng *interpolation qualifier*.

.. code-block:: glsl

    shader_type spatial;

    varying flat vec3 our_color;

    void vertex() {
        our_color = COLOR.rgb;
    }

    void fragment() {
        ALBEDO = our_color;
    }

Có hai interpolation qualifier khả dụng:

+-------------------+---------------------------------------------------------------------------------+
| Qualifier         | Description                                                                     |
+===================+=================================================================================+
| **flat**          | The value is not interpolated.                                                  |
+-------------------+---------------------------------------------------------------------------------+
| **smooth**        | The value is interpolated in a perspective-correct fashion. This is the default.|
+-------------------+---------------------------------------------------------------------------------+

.. _doc_shading_language_uniforms:

Uniform
-------

Bạn có thể truyền giá trị vào shader bằng *uniform*, được định nghĩa ở phạm vi global của shader, bên ngoài các hàm. Khi shader được gán cho một material, các uniform sẽ xuất hiện dưới dạng các tham số có thể chỉnh sửa trong inspector của material. Không thể ghi vào uniform từ bên trong shader. Bất kỳ
:ref:`data type <doc_shading_language_data_types>` except for ``void`` can be a uniform.

.. code-block:: glsl

    shader_type spatial;

    uniform float some_value;

    uniform vec3 colors[3];

Bạn có thể thiết lập uniform trong editor ở inspector của material. Ngoài ra, bạn có thể thiết lập chúng :ref:`from code <doc_shading_language_setting_uniforms_from_code>`.

Uniform hint
~~~~~~~~~~~~

Godot cung cấp các uniform hint tùy chọn để giúp compiler hiểu uniform được dùng cho mục đích gì và editor nên cho phép người dùng chỉnh sửa nó như thế nào.

.. code-block:: glsl

    shader_type spatial;

    uniform vec4 color : source_color;
    uniform float amount : hint_range(0, 1);
    uniform vec4 other_color : source_color = vec4(1.0); // Giá trị mặc định được đặt sau hint.
    uniform sampler2D image : source_color;

Uniform cũng có thể được gán giá trị mặc định:

.. code-block:: glsl

    shader_type spatial;

    uniform vec4 some_vector = vec4(0.0);
    uniform vec4 some_color : source_color = vec4(1.0);

Lưu ý rằng khi thêm giá trị mặc định và hint, giá trị mặc định được đặt sau hint.

Dưới đây là danh sách đầy đủ các uniform hint:

+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| Type                 | Hint                                             | Description                                                                 |
+======================+==================================================+=============================================================================+
| **vec3, vec4**       | source_color                                     | Used as color.                                                              |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **int**              | hint_enum("String1", "String2")                  | Displays int input as a dropdown widget in the editor.                      |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **int, float**       | hint_range(min, max[, step])                     | Restricted to values in a range (with min/max/step).                        |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | source_color                                     | Used as albedo color.                                                       |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_normal                                      | Used as normalmap.                                                          |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_default_white                               | As value or albedo color, default to opaque white.                          |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_default_black                               | As value or albedo color, default to opaque black.                          |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_default_transparent                         | As value or albedo color, default to transparent black.                     |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_anisotropy                                  | As flowmap, default to right.                                               |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_roughness[_r, _g, _b, _a, _normal, _gray]   | Used for roughness limiter on import (attempts reducing specular aliasing). |
|                      |                                                  | ``_normal`` is a normal map that guides the roughness limiter,              |
|                      |                                                  | with roughness increasing in areas that have high-frequency detail.         |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | filter[_nearest, _linear][_mipmap][_anisotropic] | Enabled specified texture filtering.                                        |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | repeat[_enable, _disable]                        | Enabled texture repeating.                                                  |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_screen_texture                              | Texture is the screen texture.                                              |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_depth_texture                               | Texture is the depth texture.                                               |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+
| **sampler2D**        | hint_normal_roughness_texture                    | Texture is the normal roughness texture (only supported in Forward+).       |
+----------------------+--------------------------------------------------+-----------------------------------------------------------------------------+

Sử dụng ``hint_enum``
^^^^^^^^^^^^^^^^^^^^^

Bạn có thể truy cập các giá trị ``int`` dưới dạng widget dropdown có thể đọc bằng uniform ``hint_enum``:

.. code-block::

    uniform int noise_type : hint_enum("OpenSimplex2", "Cellular", "Perlin", "Value") = 0;

Bạn có thể gán các giá trị tường minh cho uniform ``hint_enum`` bằng cú pháp dấu hai chấm tương tự như trong GDScript:

.. code-block::

    uniform int character_speed: hint_enum("Slow:30", "Average:60", "Very Fast:200") = 60;

Giá trị sẽ được lưu dưới dạng số nguyên, tương ứng với chỉ mục của tùy chọn đã chọn (tức là ``0``, ``1`` hoặc ``2``) hoặc giá trị được gán bằng cú pháp dấu hai chấm (tức là ``30``, ``60`` hoặc ``200``). Khi thiết lập giá trị bằng ``set_shader_parameter()``, bạn phải sử dụng giá trị số nguyên, không phải tên ``String``.

Sử dụng ``source_color``
^^^^^^^^^^^^^^^^^^^^^^^^

Mọi texture chứa *sRGB color data* đều cần hint ``source_color`` để được sample chính xác. Điều này là do Godot render trong không gian màu tuyến tính, trong khi một số texture chứa dữ liệu màu sRGB. Nếu không sử dụng hint này, texture sẽ bị nhạt màu.

Texture albedo và color thường nên có hint ``source_color``. Texture normal, roughness, metallic và height thường không cần hint ``source_color``.

Bắt buộc phải sử dụng hint ``source_color`` trong các renderer Forward+ và Mobile, cũng như trong các shader ``canvas_item`` khi :ref:`HDR 2D<class_ProjectSettings_property_rendering/viewport/hdr_2d>` được bật. Hint ``source_color`` là tùy chọn đối với renderer Compatibility và các shader ``canvas_item`` nếu ``HDR 2D`` bị tắt. Tuy nhiên, bạn luôn nên sử dụng hint ``source_color``, vì nó vẫn hoạt động ngay cả khi bạn thay đổi renderer hoặc tắt ``HDR 2D``.

Nhóm uniform
~~~~~~~~~~~~

Để nhóm nhiều uniform vào một section trong inspector, bạn có thể sử dụng từ khóa ``group_uniform`` như sau:

.. code-block:: glsl

    group_uniforms MyGroup;
    uniform sampler2D test;

Bạn có thể đóng group bằng cách sử dụng:

.. code-block:: glsl

    group_uniforms;

Cú pháp này cũng hỗ trợ subgroup (không bắt buộc phải khai báo group cơ sở trước):

.. code-block:: glsl

    group_uniforms MyGroup.MySubgroup;

.. _doc_shading_language_global_uniforms:

Uniform global
~~~~~~~~~~~~~~

Đôi khi, bạn muốn sửa đổi một tham số trong nhiều shader khác nhau cùng lúc. Với uniform thông thường, việc này đòi hỏi rất nhiều công sức vì bạn phải theo dõi tất cả các shader này và đặt uniform cho từng shader. Global uniform cho phép bạn tạo và cập nhật các uniform khả dụng trong mọi shader, thuộc mọi loại shader (``canvas_item``, ``spatial``, ``particles``, ``sky`` và ``fog``).

Global uniform đặc biệt hữu ích cho các hiệu ứng môi trường ảnh hưởng đến nhiều đối tượng trong một cảnh, chẳng hạn như làm tán lá uốn cong khi người chơi ở gần hoặc làm các đối tượng chuyển động theo gió.

.. note:: *Global uniforms* are not the same as *global scope* for an individual
    shader. Trong khi uniform thông thường được định nghĩa bên ngoài các hàm shader và do đó nằm trong phạm vi toàn cục của shader, global uniform là toàn cục đối với mọi shader trong toàn bộ dự án (nhưng trong mỗi shader, chúng cũng nằm trong phạm vi toàn cục).

Để tạo global uniform, hãy mở **Project Settings**, sau đó chuyển đến tab **Shader Globals**. Chỉ định tên cho uniform (phân biệt chữ hoa chữ thường) và một kiểu, sau đó nhấp **Add** ở góc trên bên phải của hộp thoại. Sau đó, bạn có thể chỉnh sửa giá trị được gán cho uniform bằng cách nhấp vào giá trị trong danh sách các uniform:

.. figure:: img/shading_language_adding_global_uniforms.webp
   :align: center
   :alt: Adding a global uniform in the Shader Globals tab of the Project Settings

   Adding a global uniform in the Shader Globals tab of the Project Settings

Sau khi tạo global uniform, bạn có thể sử dụng nó trong shader như sau:

.. code-block:: glsl

    shader_type canvas_item;

    global uniform vec4 my_color;

    void fragment() {
        COLOR = my_color.rgb;
    }

Lưu ý rằng global uniform *phải* tồn tại trong Project Settings tại thời điểm shader được lưu, nếu không quá trình biên dịch sẽ thất bại. Mặc dù bạn có thể gán một giá trị mặc định bằng ``global uniform vec4 my_color = ...`` trong mã shader, giá trị này sẽ bị bỏ qua vì global uniform luôn phải được định nghĩa trong Project Settings.

Để thay đổi giá trị của một global uniform trong runtime, hãy sử dụng
:ref:`RenderingServer.global_shader_parameter_set <class_RenderingServer_method_global_shader_parameter_set>`
phương thức trong một script:

.. code-block:: gdscript

    RenderingServer.global_shader_parameter_set("my_color", Color(0.3, 0.6, 1.0))

Bạn có thể gán giá trị global uniform bao nhiêu lần tùy ý mà không ảnh hưởng đến hiệu năng, vì việc thiết lập dữ liệu không yêu cầu đồng bộ hóa giữa CPU và GPU.

Bạn cũng có thể thêm hoặc xóa global uniform trong runtime:

.. code-block:: gdscript

    RenderingServer.global_shader_parameter_add("my_color", RenderingServer.GLOBAL_VAR_TYPE_COLOR, Color(0.3, 0.6, 1.0))
    RenderingServer.global_shader_parameter_remove("my_color")

Việc thêm hoặc xóa global uniform trong runtime có chi phí hiệu năng, mặc dù tác động không đáng kể bằng việc lấy các giá trị global uniform từ một script (xem cảnh báo bên dưới).

.. warning::

    Mặc dù bạn *có thể* truy vấn giá trị của global uniform trong runtime từ một script bằng ``RenderingServer.global_shader_parameter_get("uniform_name")``, việc này gây ảnh hưởng lớn đến hiệu năng vì rendering thread cần đồng bộ hóa với calling thread.

    Do đó, không nên liên tục đọc các giá trị global shader uniform trong một script. Nếu cần đọc các giá trị trong một script sau khi đặt chúng, hãy cân nhắc tạo một :ref:`autoload <doc_singletons_autoload>` để lưu trữ các giá trị bạn cần truy vấn cùng thời điểm bạn đặt chúng làm global uniform.

.. _doc_shading_language_per_instance_uniforms:

Per-instance uniform
~~~~~~~~~~~~~~~~~~~~

.. note::

    Per-instance uniform khả dụng trong cả shader ``canvas_item`` (2D) và ``spatial`` (3D).

Đôi khi, bạn muốn sửa đổi một tham số trên từng node bằng material. Ví dụ, trong một khu rừng đầy cây, bạn muốn mỗi cây có một màu hơi khác nhau và có thể chỉnh sửa thủ công. Nếu không có per-instance uniform, bạn phải tạo một material duy nhất cho mỗi cây (mỗi material có một sắc độ hơi khác nhau). Điều này khiến việc quản lý material trở nên phức tạp hơn, đồng thời làm tăng chi phí hiệu năng vì cảnh cần nhiều material instance duy nhất hơn. Vertex color cũng có thể được sử dụng trong trường hợp này, nhưng chúng yêu cầu tạo các bản sao duy nhất của mesh cho từng màu khác nhau, việc này cũng làm tăng chi phí hiệu năng.

Per-instance uniform được đặt trên từng GeometryInstance3D, thay vì trên từng Material instance. Hãy lưu ý điều này khi làm việc với các mesh được gán nhiều material hoặc các thiết lập MultiMesh.

.. code-block:: glsl

    shader_type spatial;

    // Cung cấp gợi ý để chỉnh sửa dưới dạng màu. Bạn cũng có thể tùy chọn cung cấp một giá trị mặc định.
    // Nếu không cung cấp giá trị mặc định, giá trị mặc định của kiểu sẽ được sử dụng (ví dụ: màu đen đục đối với màu).
    instance uniform vec4 my_color : source_color = vec4(1.0, 0.5, 0.0, 1.0);

    void fragment() {
        ALBEDO = my_color.rgb;
    }

Sau khi lưu shader, bạn có thể thay đổi giá trị của per-instance uniform bằng inspector:

.. figure:: img/shading_language_per_instance_uniforms_inspector.webp
   :align: center
   :alt: Setting a per-instance uniform's value in the GeometryInstance3D section of the inspector

   Setting a per-instance uniform's value in the GeometryInstance3D section of the inspector

Giá trị per-instance uniform cũng có thể được đặt trong runtime bằng
:ref:`set_instance_shader_parameter <class_GeometryInstance3D_method_set_instance_shader_parameter>`
phương thức trên một node kế thừa từ :ref:`class_GeometryInstance3D`:

.. code-block:: gdscript

    $MeshInstance3D.set_instance_shader_parameter("my_color", Color(0.3, 0.6, 1.0))

Khi sử dụng per-instance uniform, có một số hạn chế bạn cần lưu ý:

- **Per-instance uniform không hỗ trợ texture hoặc array**, chỉ hỗ trợ các kiểu scalar và vector thông thường. Một cách khắc phục là truyền một texture array dưới dạng uniform thông thường, sau đó truyền chỉ số của texture cần vẽ bằng per-instance uniform.

.. note::

    Trong các phiên bản GLSL trước 4.0 (tức GLSL 3.3 trở xuống), bạn không thể lập chỉ mục trực tiếp texture array bằng per-instance uniform, vì sampler array chỉ có thể được lập chỉ mục bằng các biểu thức hằng số tại thời điểm biên dịch. Điều này ảnh hưởng đến các shader được biên dịch bằng Compatibility renderer.

    Nếu bị ảnh hưởng, hãy sử dụng câu lệnh ``switch`` để chọn texture:

   .. code-block:: glsl

      uniform sampler2D texture_array[2];
      instance uniform int texture_index;

      void fragment() {
          vec4 color;
          switch (texture_index) {
              case 0:
                  color = texture(texture_array[0], UV);
                  break;
              case 1:
                  color = texture(texture_array[1], UV);
                  break;
          }

          COLOR = color;
      }

- Giới hạn tối đa trên thực tế là 16 instance uniform cho mỗi shader. - Nếu mesh của bạn sử dụng nhiều material, các tham số của material đầu tiên của mesh được tìm thấy sẽ "thắng" các tham số tiếp theo, trừ khi chúng có cùng tên, chỉ số *và* kiểu. Trong trường hợp này, tất cả tham số đều được tác động chính xác. - Nếu gặp tình huống trên, bạn có thể tránh xung đột bằng cách chỉ định thủ công chỉ số (0-15) của instance uniform bằng gợi ý ``instance_index``:

.. code-block:: glsl

    instance uniform vec4 my_color : source_color, instance_index(5);

.. _doc_shading_language_setting_uniforms_from_code:

Đặt uniform từ code
~~~~~~~~~~~~~~~~~~~

Bạn có thể đặt uniform từ GDScript bằng
:ref:`set_shader_parameter() <class_ShaderMaterial_method_set_shader_parameter>`
phương thức:

.. code-block:: gdscript

  material.set_shader_parameter("some_value", some_value)

  material.set_shader_parameter("colors", [Vector3(1, 0, 0), Vector3(0, 1, 0), Vector3(0, 0, 1)])

.. note:: The first argument to ``set_shader_parameter()`` is the name of the uniform
          trong shader. Tên này phải khớp *chính xác* với tên của uniform trong shader, nếu không nó sẽ không được nhận diện.

GDScript sử dụng các kiểu biến khác với GLSL, vì vậy khi truyền biến từ GDScript vào shader, Godot sẽ tự động chuyển đổi kiểu. Dưới đây là bảng các kiểu tương ứng:

+------------------------+-------------------------+------------------------------------------------------------+
| GLSL type              | GDScript type           | Notes                                                      |
+========================+=========================+============================================================+
| **bool**               | **bool**                |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **bvec2**              | **int**                 | Bitwise packed int where bit 0 (LSB) corresponds to x.     |
|                        |                         |                                                            |
|                        |                         | For example, a bvec2 of (bx, by) could be created in       |
|                        |                         | the following way:                                         |
|                        |                         |                                                            |
|                        |                         | .. code-block:: gdscript                                   |
|                        |                         |                                                            |
|                        |                         |   bvec2_input: int = (int(bx)) | (int(by) << 1)            |
|                        |                         |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **bvec3**              | **int**                 | Bitwise packed int where bit 0 (LSB) corresponds to x.     |
+------------------------+-------------------------+------------------------------------------------------------+
| **bvec4**              | **int**                 | Bitwise packed int where bit 0 (LSB) corresponds to x.     |
+------------------------+-------------------------+------------------------------------------------------------+
| **int**                | **int**                 |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **ivec2**              | **Vector2i**            |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **ivec3**              | **Vector3i**            |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **ivec4**              | **Vector4i**            |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **uint**               | **int**                 |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **uvec2**              | **Vector2i**            |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **uvec3**              | **Vector3i**            |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **uvec4**              | **Vector4i**            |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **float**              | **float**               |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **vec2**               | **Vector2**             |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **vec3**               | **Vector3**, **Color**  | When Color is used, it will be interpreted as (r, g, b).   |
+------------------------+-------------------------+------------------------------------------------------------+
| **vec4**               | **Vector4**, **Color**, | When Color is used, it will be interpreted as (r, g, b, a).|
|                        | **Rect2**, **Plane**,   |                                                            |
|                        | **Quaternion**          | When Rect2 is used, it will be interpreted as              |
|                        |                         | (position.x, position.y, size.x, size.y).                  |
|                        |                         |                                                            |
|                        |                         | When Plane is used it will be interpreted as               |
|                        |                         | (normal.x, normal.y, normal.z, d).                         |
|                        |                         |                                                            |
|                        |                         |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **mat2**               | **Transform2D**         |                                                            |
|                        |                         |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **mat3**               | **Basis**               |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **mat4**               | **Projection**,         | When a Transform3D is used, the w Vector is set to the     |
|                        | **Transform3D**         | identity.                                                  |
+------------------------+-------------------------+------------------------------------------------------------+
| **sampler2D**          | **Texture2D**           |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **isampler2D**         | **Texture2D**           |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **usampler2D**         | **Texture2D**           |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **sampler2DArray**     | **Texture2DArray**      |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **isampler2DArray**    | **Texture2DArray**      |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **usampler2DArray**    | **Texture2DArray**      |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **sampler3D**          | **Texture3D**           |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **isampler3D**         | **Texture3D**           |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **usampler3D**         | **Texture3D**           |                                                            |
+------------------------+-------------------------+------------------------------------------------------------+
| **samplerCube**        | **Cubemap**             | See :ref:`doc_importing_images_changing_import_type` for   |
|                        |                         | instructions on importing cubemaps for use in Godot.       |
+------------------------+-------------------------+------------------------------------------------------------+
| **samplerCubeArray**   | **CubemapArray**        | Only supported in Forward+ and Mobile, not Compatibility.  |
+------------------------+-------------------------+------------------------------------------------------------+
| **samplerExternalOES** | **ExternalTexture**     | Only supported in Compatibility/Android platform.          |
+------------------------+-------------------------+------------------------------------------------------------+

.. note:: Be careful when setting shader uniforms from GDScript, since no error
          sẽ được phát sinh nếu kiểu không khớp. Shader của bạn sẽ chỉ thể hiện hành vi không xác định. Cụ thể, điều này bao gồm việc đặt GDScript int/float (64 bit) vào int/float (32 bit) của ngôn ngữ shader Godot. Điều này có thể dẫn đến hậu quả không mong muốn trong các trường hợp yêu cầu độ chính xác cao.

Giới hạn uniform
~~~~~~~~~~~~~~~~

Có giới hạn về tổng kích thước của các shader uniform mà bạn có thể sử dụng trong một shader. Trên hầu hết các nền tảng desktop, giới hạn này là ``65536`` byte hoặc 4096 uniform ``vec4``. Trên các nền tảng mobile, giới hạn thường là ``16384`` byte hoặc 1024 uniform ``vec4``. Các vector uniform nhỏ hơn một ``vec4``, chẳng hạn như ``vec2`` hoặc ``vec3``, sẽ được đệm đến kích thước của một ``vec4``. Các scalar uniform như ``int`` hoặc ``float`` không được đệm, còn ``bool`` được đệm đến kích thước của một ``int``.

Array được tính theo tổng kích thước nội dung của chúng. Nếu cần một uniform array lớn hơn giới hạn này, hãy cân nhắc đóng gói dữ liệu vào texture thay thế, vì *nội dung* của texture không được tính vào giới hạn này, chỉ kích thước của sampler uniform mới được tính.

Biến tích hợp sẵn
-----------------

Có rất nhiều biến tích hợp sẵn, chẳng hạn như ``UV``, ``COLOR`` và ``VERTEX``. Các biến khả dụng phụ thuộc vào loại shader (``spatial``, ``canvas_item``, ``particle``, v.v.) và hàm được sử dụng (``vertex``, ``fragment``, ``light``, ``start``, ``process``, ``sky`` hoặc ``fog``). Để xem danh sách các biến tích hợp sẵn khả dụng, vui lòng xem các trang tương ứng:

- :ref:`Spatial shaders <doc_spatial_shader>` - :ref:`Canvas item shaders <doc_canvas_item_shader>` - :ref:`Particle shaders <doc_particle_shader>` - :ref:`Sky shaders <doc_sky_shader>` - :ref:`Fog shaders <doc_fog_shader>`

Hàm tích hợp sẵn
----------------

Có rất nhiều hàm tích hợp sẵn được hỗ trợ, tuân theo GLSL ES 3.0. Xem trang :ref:`Built-in functions <doc_shader_functions>` để biết chi tiết.
