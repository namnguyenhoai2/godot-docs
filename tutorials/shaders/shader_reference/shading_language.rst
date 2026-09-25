.. _doc_shading_language:

Ngôn ngữ shading
================

Giới thiệu
----------

Godot sử dụng ngôn ngữ shading tương tự GLSL ES 3.0. Hầu hết các kiểu dữ liệu và hàm đều được hỗ trợ, còn một số ít kiểu và hàm còn lại có thể sẽ được bổ sung theo thời gian.

Nếu đã quen thuộc với GLSL, :ref:`Godot Shader Migration Guide <doc_converting_glsl_to_godot_shaders>` là tài nguyên sẽ giúp bạn chuyển từ GLSL thông thường sang ngôn ngữ shading của Godot.

.. _doc_shading_language_data_types:

Kiểu dữ liệu
------------

Hầu hết các kiểu dữ liệu của GLSL ES 3.0 đều được hỗ trợ:

+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| Kiểu                   | Mô tả                                                                                                                                                   |
+========================+=========================================================================================================================================================+
| **void**               | Kiểu dữ liệu void, chỉ hữu ích cho các hàm không trả về giá trị.                                                                                        |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **bool**               | Kiểu dữ liệu Boolean, chỉ có thể chứa ``true`` hoặc ``false``.                                                                                          |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **bvec2**              | Vector gồm hai thành phần Boolean.                                                                                                                      |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **bvec3**              | Vector gồm ba thành phần Boolean.                                                                                                                       |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **bvec4**              | Vector gồm bốn thành phần Boolean.                                                                                                                      |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **int**                | Số nguyên vô hướng có dấu 32 bit.                                                                                                                       |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **ivec2**              | Vector gồm hai số nguyên có dấu.                                                                                                                        |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **ivec3**              | Vector gồm ba số nguyên có dấu.                                                                                                                         |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **ivec4**              | Vector gồm bốn số nguyên có dấu.                                                                                                                        |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **uint**               | Số nguyên vô hướng không dấu; không thể chứa số âm.                                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **uvec2**              | Vector gồm hai số nguyên không dấu.                                                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **uvec3**              | Vector gồm ba số nguyên không dấu.                                                                                                                      |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **uvec4**              | Vector gồm bốn số nguyên không dấu.                                                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **float**              | Số thực vô hướng dấu phẩy động 32 bit.                                                                                                                  |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **vec2**               | Vector gồm hai giá trị dấu phẩy động.                                                                                                                   |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **vec3**               | Vector gồm ba giá trị dấu phẩy động.                                                                                                                    |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **vec4**               | Vector gồm bốn giá trị dấu phẩy động.                                                                                                                   |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **mat2**               | Ma trận 2x2, theo thứ tự cột chính.                                                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **mat3**               | Ma trận 3x3, theo thứ tự cột chính.                                                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **mat4**               | Ma trận 4x4, theo thứ tự cột chính.                                                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**          | Kiểu sampler để liên kết các texture 2D, được đọc dưới dạng số thực.                                                                                    |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **isampler2D**         | Kiểu sampler để liên kết các texture 2D, được đọc dưới dạng số nguyên có dấu.                                                                           |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **usampler2D**         | Kiểu sampler để liên kết các texture 2D, được đọc dưới dạng số nguyên không dấu.                                                                        |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2DArray**     | Kiểu sampler để liên kết các mảng texture 2D, được đọc dưới dạng số thực.                                                                               |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **isampler2DArray**    | Kiểu sampler để liên kết các mảng texture 2D, được đọc dưới dạng số nguyên có dấu.                                                                      |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **usampler2DArray**    | Kiểu sampler để liên kết các mảng texture 2D, được đọc dưới dạng số nguyên không dấu.                                                                   |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler3D**          | Kiểu sampler để liên kết các texture 3D, được đọc dưới dạng số thực.                                                                                    |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **isampler3D**         | Kiểu sampler để liên kết các texture 3D, được đọc dưới dạng số nguyên có dấu.                                                                           |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **usampler3D**         | Kiểu sampler để liên kết các texture 3D, được đọc dưới dạng số nguyên không dấu.                                                                        |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **samplerCube**        | Kiểu sampler để liên kết các Cubemap, được đọc dưới dạng số thực.                                                                                       |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **samplerCubeArray**   | Kiểu sampler để liên kết các mảng Cubemap, được đọc dưới dạng số thực. Chỉ được hỗ trợ trong Forward+ và Mobile, không được hỗ trợ trong Compatibility. |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| **samplerExternalOES** | Kiểu sampler bên ngoài. Chỉ được hỗ trợ trên nền tảng Compatibility/Android.                                                                            |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+

Các kiểu này cũng có thể được đặt bên trong :ref:`arrays <doc_shading_language_arrays>` hoặc :ref:`structs <doc_shading_language_structs>`, vốn cũng có thể được dùng làm tham số hoặc giá trị trả về của hàm. Có thể sử dụng mảng làm uniform, nhưng không thể sử dụng struct.

.. warning::

    Các biến cục bộ không được khởi tạo bằng một giá trị mặc định như ``0.0``. Nếu sử dụng một biến trước khi gán giá trị cho nó, biến sẽ chứa giá trị đã có sẵn tại vị trí bộ nhớ đó, và các lỗi hiển thị không thể đoán trước sẽ xuất hiện. Tuy nhiên, uniform và varying được khởi tạo bằng một giá trị mặc định.

Chú thích
~~~~~~~~~

Ngôn ngữ shading hỗ trợ cú pháp chú thích giống như trong C# và C++, sử dụng ``//`` cho chú thích một dòng và ``/* */`` cho chú thích nhiều dòng:

.. code-block:: glsl

    // Chú thích một dòng.
    int a = 2;  // Một chú thích một dòng khác.

    /*
    Chú thích nhiều dòng.
    Chú thích kết thúc khi tìm thấy dấu phân cách kết thúc
    (ở đây, nó nằm trên dòng bên dưới).
    */
    int b = 3;

Ngoài ra, bạn có thể sử dụng các chú thích tài liệu, được hiển thị trong inspector khi di chuột qua một tham số shader. Hiện tại, chú thích tài liệu chỉ được hỗ trợ khi đặt ngay phía trên một khai báo ``uniform``. Các chú thích tài liệu này chỉ hỗ trợ cú pháp chú thích **multiline** (ngay cả khi được dùng trên một dòng) và phải sử dụng **hai** dấu sao (``/**``) ở đầu thay vì chỉ một dấu (``/*``):

.. code-block:: glsl

    /**
     * Đây là một chú thích tài liệu.
     * Các dòng này sẽ xuất hiện trong inspector khi di chuột qua tham số shader
     * có tên là "Something".
     * Bạn có thể sử dụng định dạng [b]BBCode[/b] [i]trong chú thích[/i].
     */
    uniform int something = 1;

    /** Đây là một chú thích tài liệu một dòng. */
    uniform float something_else = 1.0;

Các dấu sao trên những dòng tiếp theo không bắt buộc, nhưng được khuyến nghị theo :ref:`doc_shaders_style_guide`. Các dấu sao này sẽ được inspector tự động loại bỏ, vì vậy chúng sẽ không xuất hiện trong chú giải công cụ.

Ép kiểu
~~~~~~~

Giống như GLSL ES 3.0, không cho phép ép kiểu ngầm định giữa các scalar và vector có cùng kích thước nhưng khác kiểu. Cũng không cho phép ép kiểu giữa các kiểu có kích thước khác nhau. Phải thực hiện chuyển đổi một cách tường minh thông qua các constructor.

Ví dụ:

.. code-block:: glsl

    float a = 2; // không hợp lệ
    float a = 2.0; // hợp lệ
    float a = float(2); // hợp lệ

Các hằng số integer mặc định là có dấu, vì vậy luôn cần ép kiểu để chuyển đổi sang không dấu:

.. code-block:: glsl

    int a = 2; // hợp lệ
    uint a = 2; // không hợp lệ
    uint a = uint(2); // hợp lệ

Thành phần
~~~~~~~~~~

Có thể truy cập từng thành phần scalar của các kiểu vector thông qua các thành phần "x", "y", "z" và "w". Ngoài ra, sử dụng "r", "g", "b" và "a" cũng được và có ý nghĩa tương đương. Hãy sử dụng cách phù hợp nhất với nhu cầu của bạn.

Đối với ma trận, sử dụng cú pháp lập chỉ mục ``m[column][row]`` để truy cập từng scalar, hoặc ``m[column]`` để truy cập một vector theo chỉ mục cột. Ví dụ, để truy cập thành phần y của phép tịnh tiến từ ma trận biến đổi mat4 (cột thứ 4, dòng thứ 2), bạn sử dụng ``m[3][1]`` hoặc ``m[3].y``.

Khởi tạo
~~~~~~~~

Khi khởi tạo các kiểu vector, luôn phải truyền vào:

.. code-block:: glsl

    // Số lượng scalar cần thiết
    vec4 a = vec4(0.0, 1.0, 2.0, 3.0);
    // Các vector và/hoặc scalar bổ sung
    vec4 a = vec4(vec2(0.0, 1.0), vec2(2.0, 3.0));
    vec4 a = vec4(vec3(0.0, 1.0, 2.0), 3.0);
    // Một scalar duy nhất cho toàn bộ vector
    vec4 a = vec4(0.0);

Khi khởi tạo các kiểu ma trận, cần các vector có cùng số chiều với ma trận và được hiểu là các cột. Bạn cũng có thể tạo một ma trận đường chéo bằng cú pháp ``matx(float)``. Theo đó, ``mat4(1.0)`` là một ma trận đơn vị.

.. code-block:: glsl

    mat2 m2 = mat2(vec2(1.0, 0.0), vec2(0.0, 1.0));
    mat3 m3 = mat3(vec3(1.0, 0.0, 0.0), vec3(0.0, 1.0, 0.0), vec3(0.0, 0.0, 1.0));
    mat4 identity = mat4(1.0);

Ma trận cũng có thể được tạo từ một ma trận có số chiều khác. Có hai quy tắc:

1. Nếu tạo một ma trận lớn hơn từ một ma trận nhỏ hơn, các hàng bổ sung
và các cột được đặt thành những giá trị mà chúng sẽ có trong một ma trận đơn vị.
1. Nếu tạo một ma trận nhỏ hơn từ một ma trận lớn hơn, phần trên bên trái
ma trận con của ma trận lớn hơn được sử dụng.

.. code-block:: glsl

    mat3 basis = mat3(MODEL_MATRIX);
    mat4 m4 = mat4(basis);
    mat2 m2 = mat2(m4);

Swizzling
~~~~~~~~~

Có thể lấy bất kỳ tổ hợp thành phần nào theo bất kỳ thứ tự nào, miễn là kết quả là một kiểu vector khác (hoặc scalar). Cách này dễ minh họa hơn là giải thích:

.. code-block:: glsl

    vec4 a = vec4(0.0, 1.0, 2.0, 3.0);
    vec3 b = a.rgb; // Tạo một vec3 với các thành phần của vec4.
    vec3 b = a.ggg; // Cũng hợp lệ; tạo một vec3 và điền vào đó một thành phần duy nhất của vec4.
    vec3 b = a.bgr; // "b" sẽ là vec3(2.0, 1.0, 0.0).
    vec3 b = a.xyz; // rgba và xyzw cũng tương đương.
    vec3 b = a.stp; // Và stpq (dành cho tọa độ texture).
    float c = b.w; // Không hợp lệ vì "w" không có trong vec3 b.
    vec3 c = b.xrt; // Không hợp lệ, không được trộn lẫn các kiểu khác nhau.
    b.rrr = a.rgb; // Không hợp lệ, phép gán có trùng lặp.
    b.bgr = a.rgb; // Phép gán hợp lệ. Thành phần "blue" của "b" sẽ là thành phần "red" của "a" và ngược lại.

Precision
~~~~~~~~~

Có thể thêm các precision modifier vào kiểu dữ liệu; sử dụng chúng cho uniforms, biến, arguments và varyings:

.. code-block:: glsl

    lowp vec4 a = vec4(0.0, 1.0, 2.0, 3.0); // precision thấp, thường là 8 bit cho mỗi thành phần, ánh xạ vào khoảng 0-1
    mediump vec4 a = vec4(0.0, 1.0, 2.0, 3.0); // precision trung bình, thường là 16 bit hoặc half float
    highp vec4 a = vec4(0.0, 1.0, 2.0, 3.0); // precision cao, sử dụng toàn bộ phạm vi của float hoặc integer (mặc định 32 bit)


Sử dụng precision thấp hơn cho một số phép toán có thể tăng tốc phần tính toán liên quan (đổi lại độ chính xác thấp hơn). Điều này hiếm khi cần thiết trong hàm vertex processor (nơi thường cần precision đầy đủ), nhưng thường hữu ích trong fragment processor.

Một số kiến trúc (chủ yếu là thiết bị di động) có thể hưởng lợi đáng kể từ việc này, nhưng cũng có nhược điểm như chi phí bổ sung khi chuyển đổi giữa các mức precision. Hãy tham khảo tài liệu của kiến trúc đích để biết thêm thông tin. Trong nhiều trường hợp, driver trên thiết bị di động gây ra hành vi không nhất quán hoặc không mong đợi, vì vậy tốt nhất nên tránh chỉ định precision nếu không cần thiết.

.. _doc_shading_language_arrays:

Arrays
------

Arrays là các vùng chứa nhiều biến có kiểu tương tự nhau.

Local arrays
~~~~~~~~~~~~

Local arrays được khai báo trong các hàm. Chúng có thể sử dụng tất cả các kiểu dữ liệu được cho phép, ngoại trừ samplers. Khai báo array tuân theo cú pháp kiểu C: ``[const] + [precision] + typename + identifier + [array size]``.

.. code-block:: glsl

    void fragment() {
        float arr[3];
    }

Bạn có thể khởi tạo chúng ngay từ đầu như sau:

.. code-block:: glsl

    float float_arr[3] = float[3] (1.0, 0.5, 0.0); // constructor thứ nhất

    int int_arr[3] = int[] (2, 1, 0); // constructor thứ hai

    vec2 vec2_arr[3] = { vec2(1.0, 1.0), vec2(0.5, 0.5), vec2(0.0, 0.0) }; // constructor thứ ba

    bool bool_arr[] = { true, true, false }; // constructor thứ tư - kích thước được tự động xác định dựa trên số lượng phần tử

Bạn có thể khai báo nhiều array (ngay cả với kích thước khác nhau) trong một biểu thức:

.. code-block:: glsl

    float a[3] = float[3] (1.0, 0.5, 0.0),
    b[2] = { 1.0, 0.5 },
    c[] = { 0.7 },
    d = 0.0,
    e[5];

Để truy cập một phần tử array, hãy sử dụng cú pháp indexing:

.. code-block:: glsl

    float arr[3];

    arr[0] = 1.0; // setter

    COLOR.r = arr[0]; // getter

Arrays cũng có một hàm tích hợp ``.length()`` (không nên nhầm với hàm tích hợp ``length()``). Hàm này không nhận tham số và trả về kích thước của array.

.. code-block:: glsl

    float arr[] = { 0.0, 1.0, 0.5, -1.0 };
    for (int i = 0; i < arr.length(); i++) {
        // ...
    }

.. note::

    Nếu sử dụng một index nhỏ hơn 0 hoặc lớn hơn kích thước array, shader sẽ bị crash và dừng việc render. Để ngăn điều này, hãy sử dụng các hàm ``length()``, ``if`` hoặc ``clamp()`` để đảm bảo index nằm trong khoảng từ 0 đến độ dài của array. Luôn kiểm tra kỹ và test code của bạn. Nếu truyền một biểu thức hằng hoặc một số, editor sẽ kiểm tra giới hạn của nó để ngăn lỗi crash này.

Global arrays
~~~~~~~~~~~~~

Bạn có thể khai báo arrays trong global scope dưới dạng ``const`` hoặc ``uniform``:

.. code-block:: glsl

    shader_type spatial;

    const lowp vec3 v[1] = lowp vec3[1] ( vec3(0, 0, 1) );
    uniform lowp vec3 w[1];

    void fragment() {
      ALBEDO = v[0] + w[0];
    }

.. note::

    Global arrays sử dụng cùng cú pháp với local arrays, ngoại trừ việc thêm ``const`` hoặc ``uniform`` vào khai báo của chúng. Lưu ý rằng uniform arrays không thể có giá trị mặc định.

Constants
---------

Sử dụng keyword ``const`` trước khai báo biến để biến đó trở thành immutable, nghĩa là không thể bị thay đổi. Tất cả các kiểu cơ bản, ngoại trừ samplers, đều có thể được khai báo là constants. Việc truy cập và sử dụng một constant nhanh hơn một chút so với sử dụng uniform. Constants phải được khởi tạo ngay khi khai báo.

.. code-block:: glsl

    const vec2 a = vec2(0.0, 1.0);
    vec2 b;

    a = b; // không hợp lệ
    b = a; // hợp lệ

Constants không thể bị thay đổi và cũng không thể có hints, nhưng có thể khai báo nhiều constant (nếu chúng cùng kiểu) trong một biểu thức duy nhất, ví dụ

.. code-block:: glsl

    const vec2 V1 = vec2(1, 1), V2 = vec2(2, 2);

Tương tự như variables, arrays cũng có thể được khai báo với ``const``.

.. code-block:: glsl

    const float arr[] = { 1.0, 0.5, 0.0 };

    arr[0] = 1.0; // không hợp lệ

    COLOR.r = arr[0]; // hợp lệ

Constants có thể được khai báo ở global scope (bên ngoài mọi hàm) hoặc local scope (bên trong một hàm). Global constants hữu ích khi bạn muốn truy cập một giá trị trong toàn bộ shader và giá trị đó không cần bị thay đổi. Giống như uniforms, global constants được chia sẻ giữa tất cả shader stages, nhưng không thể truy cập từ bên ngoài shader.

.. code-block:: glsl

    shader_type spatial;

    const float GOLDEN_RATIO = 1.618033988749894;

Constants có kiểu ``float`` phải được khởi tạo bằng ký hiệu ``.`` sau phần thập phân hoặc bằng scientific notation. Hậu tố ``f`` tùy chọn cũng được hỗ trợ.

.. code-block:: glsl

    float a = 1.0;
    float b = 1.0f; // giống nhau, sử dụng hậu tố để dễ hiểu hơn
    float c = 1e-1; // cho giá trị 0.1 bằng cách sử dụng scientific notation

Constants có kiểu ``uint`` (unsigned int) phải có hậu tố ``u`` để phân biệt với các số nguyên có dấu. Ngoài ra, có thể thực hiện việc này bằng cách sử dụng hàm chuyển đổi tích hợp ``uint(x)``.

.. code-block:: glsl

    uint a = 1u;
    uint b = uint(1);

.. _doc_shading_language_structs:

Structs
-------

Structs là các kiểu compound có thể được sử dụng để trừu tượng hóa code shader tốt hơn. Bạn có thể khai báo chúng ở global scope như sau:

.. code-block:: glsl

    struct PointLight {
        vec3 position;
        vec3 color;
        float intensity;
    };

Sau khi khai báo, bạn có thể khởi tạo và gán giá trị cho chúng như sau:

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

Structs có thể chứa struct hoặc array khác; bạn cũng có thể khởi tạo chúng dưới dạng global constant:

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

Toán tử
-------

Ngôn ngữ shading của Godot hỗ trợ cùng tập toán tử như GLSL ES 3.0. Dưới đây là danh sách theo thứ tự độ ưu tiên:

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

    Hầu hết các toán tử chấp nhận vector hoặc ma trận (phép nhân, phép chia, v.v.) đều hoạt động theo từng thành phần, nghĩa là hàm được áp dụng cho giá trị đầu tiên của mỗi vector, sau đó đến giá trị thứ hai của mỗi vector, v.v. Một số ví dụ:

    .. table::
        :class: nowrap-col2 nowrap-col1
        :widths: auto

        +---------------------------------------+------------------------------------------------------+
        | Phép toán                             | Phép toán vô hướng tương đương                       |
        +=======================================+======================================================+
        | ``vec3(4, 5, 6) + 2``                 | ``vec3(4 + 2, 5 + 2, 6 + 2)``                        |
        +---------------------------------------+------------------------------------------------------+
        | ``vec2(3, 4) * vec2(10, 20)``         | ``vec2(3 * 10, 4 * 20)``                             |
        +---------------------------------------+------------------------------------------------------+
        | ``mat2(vec2(1, 2), vec2(3, 4)) + 10`` | ``mat2(vec2(1 + 10, 2 + 10), vec2(3 + 10, 4 + 10))`` |
        +---------------------------------------+------------------------------------------------------+

    `Đặc tả ngôn ngữ GLSL <http://www.opengl.org/registry/doc/GLSLangSpec.4.30.6.pdf>`_ nêu trong mục 5.10 Các phép toán vector và ma trận:

        Ngoại trừ một vài trường hợp, các phép toán được thực hiện theo từng thành phần. Thông thường, khi một toán tử hoạt động trên vector hoặc ma trận, nó sẽ hoạt động độc lập trên từng thành phần của vector hoặc ma trận theo cách thức từng thành phần. [...] Các ngoại lệ là ma trận nhân với vector, vector nhân với ma trận và ma trận nhân với ma trận. Những phép toán này không hoạt động theo từng thành phần mà thực hiện phép nhân đại số tuyến tính phù hợp.

Điều khiển luồng
----------------

Ngôn ngữ Shading của Godot hỗ trợ các loại điều khiển luồng phổ biến nhất:

.. code-block:: glsl

    // `if`, `else if` và `else`.
    if (cond) {

    } else if (other_cond) {

    } else {

    }

    // Toán tử ba ngôi.
    // Đây là một biểu thức hoạt động như `if`/`else` và trả về giá trị.
    // Nếu `cond` đánh giá thành `true`, `result` sẽ là `9`.
    // Nếu không, `result` sẽ là `5`.
    int result = cond ? 9 : 5;

    // `switch`.
    switch (i) { // `i` phải là một biểu thức số nguyên có dấu.
        case -1:
            break;
        case 0:
            return; // `break` hoặc `return` để tránh chạy `case` tiếp theo.
        case 1: // Chuyển tiếp (không có `break` hoặc `return`): sẽ chạy `case` tiếp theo.
        case 2:
            break;
        //...
        default: // Chỉ chạy nếu không có `case` nào ở trên khớp. Tùy chọn.
            break;
    }

    // Vòng lặp `for`. Tốt nhất nên dùng khi đã biết trước số phần tử cần lặp qua
    // .
    for (int i = 0; i < 10; i++) {

    }

    // Vòng lặp `while`. Tốt nhất nên dùng khi chưa biết trước số phần tử cần lặp qua
    // .
    while (cond) {

    }

    // `do while`. Tương tự `while`, nhưng luôn chạy ít nhất một lần ngay cả khi `cond`
    // không bao giờ đánh giá thành `true`.
    do {

    } while (cond);

Hãy nhớ rằng trên các GPU hiện đại, một vòng lặp vô hạn có thể xảy ra và làm ứng dụng của bạn bị treo (bao gồm cả trình chỉnh sửa). Godot không thể bảo vệ bạn khỏi điều này, vì vậy hãy cẩn thận để không mắc lỗi này!

Ngoài ra, khi so sánh các giá trị dấu phẩy động với một số, hãy đảm bảo so sánh chúng với một *khoảng* thay vì một số chính xác.

Một phép so sánh như ``if (value == 0.3)`` có thể không đánh giá thành ``true``. Phép toán dấu phẩy động thường mang tính xấp xỉ và có thể không như dự đoán. Nó cũng có thể hoạt động khác nhau tùy theo phần cứng.

**Đừng** làm như vậy.

.. code-block:: glsl

    float value = 0.1 + 0.2;

    // Có thể không đánh giá thành `true`!
    if (value == 0.3) {
        // ...
    }

Thay vào đó, luôn thực hiện phép so sánh khoảng bằng một giá trị epsilon. Số dấu phẩy động càng lớn (và càng kém chính xác) thì giá trị epsilon cần càng lớn.

.. code-block:: glsl

    const float EPSILON = 0.0001;
    if (value >= 0.3 - EPSILON && value <= 0.3 + EPSILON) {
        // ...
    }

Xem `floating-point-gui.de <https://floating-point-gui.de/>`__ để biết thêm thông tin.

Loại bỏ
-------

Các hàm fragment, light và hàm tùy chỉnh (được gọi từ fragment hoặc light) có thể sử dụng từ khóa ``discard``. Khi được sử dụng, fragment sẽ bị loại bỏ và không có gì được ghi.

Lưu ý rằng ``discard`` gây tốn hiệu năng khi được sử dụng, vì nó khiến depth prepass không thể hoạt động hiệu quả trên mọi bề mặt sử dụng shader. Ngoài ra, một pixel bị loại bỏ vẫn cần được render trong vertex shader, nghĩa là shader sử dụng ``discard`` trên tất cả pixel vẫn tốn nhiều chi phí render hơn so với việc ngay từ đầu không render đối tượng nào.

Hàm
---

Bạn có thể định nghĩa các hàm trong shader Godot. Chúng sử dụng cú pháp sau:

.. code-block:: glsl

    ret_type func_name(args) {
        return ret_type; // nếu trả về một giá trị
    }

    // một ví dụ cụ thể hơn:

    int sum2(int a, int b) {
        return a + b;
    }


Bạn chỉ có thể sử dụng các hàm đã được định nghĩa phía trên (ở vị trí cao hơn trong trình chỉnh sửa) hàm mà từ đó bạn gọi chúng. Việc định nghĩa lại một hàm đã được định nghĩa phía trên (hoặc tên của một hàm tích hợp sẵn) sẽ gây ra lỗi.

Các đối số của hàm có thể có các qualifier đặc biệt:

* **in**: Có nghĩa là đối số chỉ dùng để đọc (mặc định).
* **out**: Có nghĩa là đối số chỉ dùng để ghi.
* **inout**: Có nghĩa là đối số được truyền hoàn toàn qua tham chiếu.
* **const**: Có nghĩa là đối số là hằng số và không thể thay đổi, có thể kết hợp với qualifier **in**.

Ví dụ bên dưới:

.. code-block:: glsl

    void sum2(int a, int b, inout int result) {
        result = a + b;
    }

Có hỗ trợ overloading hàm. Bạn có thể định nghĩa nhiều hàm cùng tên nhưng có các đối số khác nhau. Lưu ý rằng `ép kiểu ngầm định <Casting_>`_ trong các lời gọi hàm overloaded không được phép, chẳng hạn như từ ``int`` sang ``float`` (``1`` sang ``1.0``).

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

Để gửi dữ liệu từ hàm xử lý vertex đến hàm xử lý fragment (hoặc light), người ta sử dụng *varyings*. Chúng được thiết lập cho mọi vertex nguyên thủy trong *bộ xử lý vertex*, và giá trị được nội suy cho mọi pixel trong *bộ xử lý fragment*.

.. code-block:: glsl

    shader_type spatial;

    varying vec3 some_color;

    void vertex() {
        some_color = NORMAL; // Đặt normal làm màu.
    }

    void fragment() {
        ALBEDO = some_color;
    }

    void light() {
        DIFFUSE_LIGHT = some_color * 100; // tùy chọn
    }

Varying cũng có thể là một mảng:

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

Bạn cũng có thể gửi dữ liệu từ *fragment* đến bộ xử lý *light* bằng từ khóa *varying*. Để làm vậy, bạn có thể gán giá trị cho nó trong *fragment* rồi sử dụng nó trong hàm *light*.

.. code-block:: glsl

    shader_type spatial;

    varying vec3 some_light;

    void fragment() {
        some_light = ALBEDO * 100.0; // Tạo ra ánh sáng lấp lánh.
    }

    void light() {
        DIFFUSE_LIGHT = some_light;
    }

Lưu ý rằng varying không thể được gán trong các hàm tùy chỉnh hoặc một hàm *light processor* như sau:

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
        test = 0.0; // Cũng lỗi.
    }

Giới hạn này được đưa ra để ngăn việc sử dụng không chính xác trước khi khởi tạo.

Bộ định tính nội suy
--------------------

Một số giá trị được nội suy trong pipeline đổ bóng. Bạn có thể thay đổi cách thực hiện các phép nội suy này bằng cách sử dụng *bộ định tính nội suy*.

.. code-block:: glsl

    shader_type spatial;

    varying flat vec3 our_color;

    void vertex() {
        our_color = COLOR.rgb;
    }

    void fragment() {
        ALBEDO = our_color;
    }

Có hai bộ định tính nội suy khả dụng:

+--------------+-----------------------------------------------------------------------+
| Bộ định tính | Mô tả                                                                 |
+==============+=======================================================================+
| **flat**     | Giá trị không được nội suy.                                           |
+--------------+-----------------------------------------------------------------------+
| **smooth**   | Giá trị được nội suy theo cách hiệu chỉnh phối cảnh. Đây là mặc định. |
+--------------+-----------------------------------------------------------------------+

.. _doc_shading_language_uniforms:

Uniform
-------

Có thể truyền giá trị vào shader bằng *uniform*, được định nghĩa trong phạm vi global của shader, bên ngoài các hàm. Khi shader được gán cho một material, các uniform sẽ xuất hiện dưới dạng các tham số có thể chỉnh sửa trong inspector của material. Không thể ghi vào uniform từ bên trong shader. Bất kỳ
:ref:`kiểu dữ liệu <doc_shading_language_data_types>` nào, ngoại trừ ``void``, đều có thể là một uniform.

.. code-block:: glsl

    shader_type spatial;

    uniform float some_value;

    uniform vec3 colors[3];

Bạn có thể đặt uniform trong editor, tại inspector của material. Ngoài ra, bạn có thể đặt chúng :ref:`từ code <doc_shading_language_setting_uniforms_from_code>`.

Gợi ý cho uniform
~~~~~~~~~~~~~~~~~

Godot cung cấp các gợi ý uniform tùy chọn để compiler hiểu uniform được sử dụng vào việc gì và editor nên cho phép người dùng chỉnh sửa nó như thế nào.

.. code-block:: glsl

    shader_type spatial;

    uniform vec4 color : source_color;
    uniform float amount : hint_range(0, 1);
    uniform vec4 other_color : source_color = vec4(1.0); // Giá trị mặc định đặt sau gợi ý.
    uniform sampler2D image : source_color;

Uniform cũng có thể được gán các giá trị mặc định:

.. code-block:: glsl

    shader_type spatial;

    uniform vec4 some_vector = vec4(0.0);
    uniform vec4 some_color : source_color = vec4(1.0);

Lưu ý rằng khi thêm giá trị mặc định và một gợi ý, giá trị mặc định đặt sau gợi ý.

Danh sách đầy đủ các gợi ý uniform:

+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Kiểu           | Gợi ý                                            | Mô tả                                                                                                                                                                                                                          |
+================+==================================================+================================================================================================================================================================================================================================+
| **vec3, vec4** | source_color                                     | Được sử dụng làm màu.                                                                                                                                                                                                          |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **int**        | hint_enum("String1", "String2")                  | Hiển thị đầu vào int dưới dạng tiện ích dropdown trong editor.                                                                                                                                                                 |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **int, float** | hint_range(min, max[, step])                     | Bị giới hạn trong các giá trị thuộc một khoảng (với min/max/step).                                                                                                                                                             |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | source_color                                     | Được sử dụng làm màu albedo.                                                                                                                                                                                                   |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_normal                                      | Được sử dụng làm normalmap.                                                                                                                                                                                                    |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_default_white                               | Dùng làm giá trị hoặc màu albedo, mặc định là màu trắng đục.                                                                                                                                                                   |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_default_black                               | Dùng làm giá trị hoặc màu albedo, mặc định là màu đen đục.                                                                                                                                                                     |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_default_transparent                         | Dùng làm giá trị hoặc màu albedo, mặc định là màu đen trong suốt.                                                                                                                                                              |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_anisotropy                                  | Dùng làm flowmap, mặc định hướng sang phải.                                                                                                                                                                                    |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_roughness[_r, _g, _b, _a, _normal, _gray]   | Được dùng cho bộ giới hạn roughness khi import (cố gắng giảm hiện tượng aliasing của specular). ``_normal`` là một normal map hướng dẫn bộ giới hạn roughness, trong đó roughness tăng ở những khu vực có chi tiết tần số cao. |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | filter[_nearest, _linear][_mipmap][_anisotropic] | Bật tính năng lọc texture được chỉ định.                                                                                                                                                                                       |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | repeat[_enable, _disable]                        | Bật tính năng lặp texture.                                                                                                                                                                                                     |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_screen_texture                              | Texture là screen texture.                                                                                                                                                                                                     |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_depth_texture                               | Texture là depth texture.                                                                                                                                                                                                      |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **sampler2D**  | hint_normal_roughness_texture                    | Texture là normal roughness texture (chỉ được hỗ trợ trong Forward+).                                                                                                                                                          |
+----------------+--------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Sử dụng ``hint_enum``
^^^^^^^^^^^^^^^^^^^^^

Bạn có thể truy cập các giá trị ``int`` dưới dạng widget dropdown dễ đọc bằng uniform ``hint_enum``:

.. code-block::

    uniform int noise_type : hint_enum("OpenSimplex2", "Cellular", "Perlin", "Value") = 0;

Bạn có thể gán các giá trị cụ thể cho uniform ``hint_enum`` bằng cú pháp dấu hai chấm tương tự như trong GDScript:

.. code-block::

    uniform int character_speed: hint_enum("Slow:30", "Average:60", "Very Fast:200") = 60;

Giá trị sẽ được lưu dưới dạng số nguyên, tương ứng với chỉ mục của tùy chọn được chọn (tức là ``0``, ``1`` hoặc ``2``) hoặc giá trị được gán bằng cú pháp dấu hai chấm (tức là ``30``, ``60`` hoặc ``200``). Khi đặt giá trị bằng ``set_shader_parameter()``, bạn phải sử dụng giá trị số nguyên, không phải tên ``String``.

Sử dụng ``source_color``
^^^^^^^^^^^^^^^^^^^^^^^^

Bất kỳ texture nào chứa dữ liệu màu *sRGB color data* đều cần hint ``source_color`` để được sample chính xác. Điều này là do Godot render trong không gian màu tuyến tính, trong khi một số texture chứa dữ liệu màu sRGB. Nếu không sử dụng hint này, texture sẽ bị nhạt màu.

Albedo và color texture thường nên có hint ``source_color``. Normal, roughness, metallic và height texture thường không cần hint ``source_color``.

Bắt buộc sử dụng hint ``source_color`` trong các renderer Forward+ và Mobile, cũng như trong các shader ``canvas_item`` khi :ref:`HDR 2D <class_ProjectSettings_property_rendering/viewport/hdr_2d>` được bật. Hint ``source_color`` là tùy chọn đối với renderer Compatibility và các shader ``canvas_item`` nếu ``HDR 2D`` bị tắt. Tuy nhiên, bạn nên luôn sử dụng hint ``source_color``, vì nó vẫn hoạt động ngay cả khi bạn thay đổi renderer hoặc tắt ``HDR 2D``.

Các nhóm uniform
~~~~~~~~~~~~~~~~

Để nhóm nhiều uniform trong một mục của inspector, bạn có thể sử dụng keyword ``group_uniform`` như sau:

.. code-block:: glsl

    group_uniforms MyGroup;
    uniform sampler2D test;

Bạn có thể đóng nhóm bằng cách sử dụng:

.. code-block:: glsl

    group_uniforms;

Cú pháp cũng hỗ trợ các nhóm con (không bắt buộc phải khai báo nhóm cơ sở trước):

.. code-block:: glsl

    group_uniforms MyGroup.MySubgroup;

.. _doc_shading_language_global_uniforms:

Global uniform
~~~~~~~~~~~~~~

Đôi khi, bạn muốn sửa đổi một tham số trong nhiều shader khác nhau cùng lúc. Với uniform thông thường, việc này đòi hỏi nhiều công sức vì bạn phải theo dõi tất cả các shader này và đặt uniform cho từng shader. Global uniform cho phép bạn tạo và cập nhật các uniform có sẵn trong mọi shader, thuộc mọi loại shader (``canvas_item``, ``spatial``, ``particles``, ``sky`` và ``fog``).

Global uniform đặc biệt hữu ích cho các hiệu ứng môi trường ảnh hưởng đến nhiều đối tượng trong một cảnh, chẳng hạn như làm tán lá uốn cong khi người chơi ở gần hoặc làm các đối tượng chuyển động theo gió.

.. note:: *Global uniform* không giống với *global scope* của một shader riêng lẻ. Mặc dù uniform thông thường được định nghĩa bên ngoài các hàm shader và do đó thuộc global scope của shader, global uniform có phạm vi toàn cục đối với mọi shader trong toàn bộ project (nhưng trong mỗi shader, chúng cũng nằm trong global scope).

Để tạo một global uniform, mở **Project Settings** rồi chuyển đến tab **Shader Globals**. Chỉ định tên cho uniform (phân biệt chữ hoa chữ thường) và một kiểu, sau đó nhấp vào **Add** ở góc trên bên phải của hộp thoại. Sau đó, bạn có thể chỉnh sửa giá trị được gán cho uniform bằng cách nhấp vào giá trị trong danh sách uniform:

.. figure:: img/shading_language_adding_global_uniforms.webp
   :align: center
   :alt: Thêm global uniform trong tab Shader Globals của Project Settings

   Thêm global uniform trong tab Shader Globals của Project Settings

Sau khi tạo global uniform, bạn có thể sử dụng nó trong shader như sau:

.. code-block:: glsl

    shader_type canvas_item;

    global uniform vec4 my_color;

    void fragment() {
        COLOR = my_color.rgb;
    }

Lưu ý rằng global uniform *must* tồn tại trong Project Settings tại thời điểm shader được lưu, nếu không quá trình biên dịch sẽ thất bại. Mặc dù bạn có thể gán giá trị mặc định bằng ``global uniform vec4 my_color = ...`` trong mã shader, giá trị này sẽ bị bỏ qua vì global uniform luôn phải được định nghĩa trong Project Settings.

Để thay đổi giá trị của một global uniform trong runtime, hãy sử dụng
phương thức :ref:`RenderingServer.global_shader_parameter_set <class_RenderingServer_method_global_shader_parameter_set>` trong một script:

.. code-block:: gdscript

    RenderingServer.global_shader_parameter_set("my_color", Color(0.3, 0.6, 1.0))

Bạn có thể gán các giá trị global uniform bao nhiêu lần tùy ý mà không ảnh hưởng đến hiệu năng, vì việc đặt dữ liệu không yêu cầu đồng bộ hóa giữa CPU và GPU.

Bạn cũng có thể thêm hoặc xóa global uniform trong runtime:

.. code-block:: gdscript

    RenderingServer.global_shader_parameter_add("my_color", RenderingServer.GLOBAL_VAR_TYPE_COLOR, Color(0.3, 0.6, 1.0))
    RenderingServer.global_shader_parameter_remove("my_color")

Việc thêm hoặc xóa global uniform trong runtime có chi phí hiệu năng, mặc dù không đáng kể bằng việc lấy các giá trị global uniform từ một script (xem cảnh báo bên dưới).

.. warning::

    Mặc dù bạn *can* truy vấn giá trị của global uniform trong runtime bằng script thông qua ``RenderingServer.global_shader_parameter_get("uniform_name")``, thao tác này gây ảnh hưởng lớn đến hiệu năng vì rendering thread cần đồng bộ với calling thread.

    Do đó, không nên liên tục đọc các giá trị global shader uniform trong một script. Nếu cần đọc các giá trị trong script sau khi thiết lập chúng, hãy cân nhắc tạo một :ref:`autoload <doc_singletons_autoload>` để lưu trữ các giá trị cần truy vấn đồng thời với lúc thiết lập chúng làm global uniform.

.. _doc_shading_language_per_instance_uniforms:

Uniform theo từng instance
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Uniform theo từng instance khả dụng trong cả shader ``canvas_item`` (2D) và ``spatial`` (3D).

Đôi khi, bạn muốn sửa đổi một tham số trên từng node bằng material. Ví dụ, trong một khu rừng đầy cây, bạn muốn mỗi cây có một màu hơi khác nhau và có thể chỉnh sửa thủ công. Nếu không có uniform theo từng instance, bạn phải tạo một material riêng cho mỗi cây (mỗi material có sắc độ hơi khác nhau). Điều này khiến việc quản lý material phức tạp hơn, đồng thời làm giảm hiệu năng vì scene cần nhiều material instance riêng biệt hơn. Bạn cũng có thể dùng màu vertex trong trường hợp này, nhưng sẽ phải tạo các bản sao riêng của mesh cho từng màu khác nhau, việc này cũng làm giảm hiệu năng.

Uniform theo từng instance được thiết lập trên từng GeometryInstance3D thay vì trên từng Material instance. Hãy lưu ý điều này khi làm việc với các mesh được gán nhiều material hoặc các thiết lập MultiMesh.

.. code-block:: glsl

    shader_type spatial;

    // Cung cấp gợi ý để chỉnh sửa dưới dạng màu. Có thể cung cấp thêm giá trị mặc định.
    // Nếu không cung cấp giá trị mặc định, giá trị mặc định của kiểu sẽ được sử dụng (ví dụ: màu đen đục đối với màu).
    instance uniform vec4 my_color : source_color = vec4(1.0, 0.5, 0.0, 1.0);

    void fragment() {
        ALBEDO = my_color.rgb;
    }

Sau khi lưu shader, bạn có thể thay đổi giá trị của uniform theo từng instance bằng inspector:

.. figure:: img/shading_language_per_instance_uniforms_inspector.webp
   :align: center
   :alt: Thiết lập giá trị uniform theo từng instance trong phần GeometryInstance3D của inspector

   Thiết lập giá trị uniform theo từng instance trong phần GeometryInstance3D của inspector

Bạn cũng có thể thiết lập các giá trị uniform theo từng instance trong runtime bằng
phương thức :ref:`set_instance_shader_parameter <class_GeometryInstance3D_method_set_instance_shader_parameter>` trên một node kế thừa từ :ref:`class_GeometryInstance3D`:

.. code-block:: gdscript

    $MeshInstance3D.set_instance_shader_parameter("my_color", Color(0.3, 0.6, 1.0))

Khi sử dụng uniform theo từng instance, bạn cần lưu ý một số hạn chế sau:

- **Uniform theo từng instance không hỗ trợ texture hoặc array**, mà chỉ hỗ trợ các kiểu scalar và vector thông thường. Một cách khắc phục là truyền một texture array dưới dạng uniform thông thường, sau đó truyền chỉ số của texture cần vẽ bằng uniform theo từng instance.

.. note::

    Trong các phiên bản GLSL trước 4.0 (tức GLSL 3.3 trở xuống), bạn không thể lập chỉ mục trực tiếp vào texture array bằng uniform theo từng instance, vì sampler array chỉ có thể được lập chỉ mục bằng các biểu thức hằng số tại thời điểm biên dịch. Điều này ảnh hưởng đến các shader được biên dịch bằng Compatibility renderer.

    Nếu bị ảnh hưởng, hãy dùng câu lệnh ``switch`` để chọn texture:

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

- Giới hạn tối đa thực tế là 16 uniform theo từng instance cho mỗi shader.
- Nếu mesh của bạn sử dụng nhiều material, các tham số của material đầu tiên được tìm thấy sẽ "chiếm ưu thế" so với các material tiếp theo, trừ khi chúng có cùng tên, chỉ số *and* kiểu. Trong trường hợp này, tất cả tham số đều bị ảnh hưởng chính xác.
- Nếu gặp tình huống trên, bạn có thể tránh xung đột bằng cách chỉ định thủ công chỉ số (0-15) của uniform theo từng instance bằng gợi ý ``instance_index``:

.. code-block:: glsl

    instance uniform vec4 my_color : source_color, instance_index(5);

.. _doc_shading_language_setting_uniforms_from_code:

Thiết lập uniform từ code
~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể thiết lập uniform từ GDScript bằng
phương thức :ref:`set_shader_parameter() <class_ShaderMaterial_method_set_shader_parameter>`:

.. code-block:: gdscript

  material.set_shader_parameter("some_value", some_value)

  material.set_shader_parameter("colors", [Vector3(1, 0, 0), Vector3(0, 1, 0), Vector3(0, 0, 1)])

.. note:: Đối số đầu tiên của ``set_shader_parameter()`` là tên của uniform trong shader. Tên này phải khớp *chính xác* với tên của uniform trong shader, nếu không nó sẽ không được nhận diện.

GDScript sử dụng các kiểu biến khác với GLSL, vì vậy khi truyền biến từ GDScript sang shader, Godot sẽ tự động chuyển đổi kiểu. Bảng dưới đây liệt kê các kiểu tương ứng:

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

.. note:: Hãy cẩn thận khi thiết lập shader uniform từ GDScript, vì sẽ không có lỗi nào được phát sinh nếu kiểu không khớp. Shader của bạn chỉ thể hiện hành vi không xác định. Cụ thể, điều này bao gồm việc thiết lập int/float (64 bit) của GDScript vào int/float (32 bit) của ngôn ngữ shader Godot. Điều này có thể dẫn đến các kết quả không mong muốn trong những trường hợp cần độ chính xác cao.

Giới hạn uniform
~~~~~~~~~~~~~~~~

Có giới hạn về tổng kích thước của các shader uniform mà bạn có thể sử dụng trong một shader. Trên hầu hết nền tảng desktop, giới hạn này là ``65536`` byte, tương đương 4096 uniform ``vec4``. Trên nền tảng di động, giới hạn thường là ``16384`` byte, tương đương 1024 uniform ``vec4``. Các vector uniform nhỏ hơn một ``vec4``, chẳng hạn như ``vec2`` hoặc ``vec3``, được đệm lên kích thước của một ``vec4``. Các scalar uniform như ``int`` hoặc ``float`` không được đệm, còn ``bool`` được đệm lên kích thước của một ``int``.

Array được tính theo tổng kích thước của nội dung bên trong. Nếu cần một uniform array lớn hơn giới hạn này, hãy cân nhắc đóng gói dữ liệu vào một texture, vì *nội dung* của texture không được tính vào giới hạn này, chỉ kích thước của sampler uniform mới được tính.

Biến tích hợp sẵn
-----------------

Có rất nhiều biến tích hợp sẵn, chẳng hạn như ``UV``, ``COLOR`` và ``VERTEX``. Các biến khả dụng phụ thuộc vào loại shader (``spatial``, ``canvas_item``, ``particle``, v.v.) và hàm được sử dụng (``vertex``, ``fragment``, ``light``, ``start``, ``process``, ``sky`` hoặc ``fog``). Để xem danh sách các biến tích hợp sẵn khả dụng, hãy tham khảo các trang tương ứng:

- :ref:`Shader không gian <doc_spatial_shader>`
- :ref:`Shader canvas item <doc_canvas_item_shader>`
- :ref:`Shader particle <doc_particle_shader>`
- :ref:`Shader sky <doc_sky_shader>`
- :ref:`Shader fog <doc_fog_shader>`

Hàm tích hợp sẵn
----------------

Có rất nhiều hàm tích hợp sẵn được hỗ trợ, tuân theo GLSL ES 3.0. Xem trang :ref:`Built-in functions <doc_shader_functions>` để biết chi tiết.

.. _`GLSL Language Specification`: http://www.opengl.org/registry/doc/GLSLangSpec.4.30.6.pdf
.. _`implicit casting`: Casting_
