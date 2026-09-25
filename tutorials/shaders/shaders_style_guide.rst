.. _doc_shaders_style_guide:

Hướng dẫn về phong cách viết shader
===================================

Hướng dẫn phong cách này liệt kê các quy ước để viết shader thanh thoát. Mục tiêu là khuyến khích viết mã sạch, dễ đọc và thúc đẩy tính nhất quán giữa các dự án, cuộc thảo luận và hướng dẫn. Hy vọng rằng tài liệu này cũng hỗ trợ việc phát triển các công cụ tự động định dạng.

Vì ngôn ngữ shader của Godot khá gần với các ngôn ngữ kiểu C và GLSL, hướng dẫn này được lấy cảm hứng từ cách định dạng GLSL của chính Godot. Bạn có thể xem các ví dụ về tệp GLSL trong mã nguồn của Godot `tại đây <https://github.com/godotengine/godot/blob/master/drivers/gles3/shaders/>`__.

Hướng dẫn phong cách không phải là những bộ quy tắc cứng nhắc. Đôi khi, bạn có thể không áp dụng được một số hướng dẫn dưới đây. Khi đó, hãy vận dụng phán đoán tốt nhất của mình và hỏi ý kiến các nhà phát triển khác.

Nhìn chung, việc giữ cho mã nhất quán trong các dự án và trong nhóm của bạn quan trọng hơn việc tuân thủ hướng dẫn này một cách tuyệt đối.

.. note:: Trình chỉnh sửa shader tích hợp sẵn của Godot mặc định đã sử dụng nhiều quy ước trong số này. Hãy để nó hỗ trợ bạn.

Dưới đây là một ví dụ shader hoàn chỉnh dựa trên các hướng dẫn này:

.. code-block:: glsl

    shader_type canvas_item;
    // Shader trong không gian màn hình để điều chỉnh độ sáng, độ tương phản của một cảnh 2D
    // và độ bão hòa. Lấy từ
    // https://github.com/godotengine/godot-demo-projects/blob/master/2d/screen_space_shaders/shaders/BCS.gdshader

    uniform sampler2D screen_texture : hint_screen_texture, filter_linear_mipmap;
    uniform float brightness = 0.8;
    uniform float contrast = 1.5;
    uniform float saturation = 1.8;

    void fragment() {
        vec3 c = textureLod(screen_texture, SCREEN_UV, 0.0).rgb;

        c.rgb = mix(vec3(0.0), c.rgb, brightness);
        c.rgb = mix(vec3(0.5), c.rgb, contrast);
        c.rgb = mix(vec3(dot(vec3(1.0), c.rgb) * 0.33333), c.rgb, saturation);

        COLOR.rgb = c;
    }

Định dạng
---------

Mã hóa và ký tự đặc biệt
~~~~~~~~~~~~~~~~~~~~~~~~

* Sử dụng ký tự xuống dòng (**LF**) để ngắt dòng, không sử dụng CRLF hoặc CR. *(mặc định của trình chỉnh sửa)*
* Sử dụng một ký tự xuống dòng ở cuối mỗi tệp. *(mặc định của trình chỉnh sửa)*
* Sử dụng mã hóa **UTF-8** không có `dấu thứ tự byte <https://en.wikipedia.org/wiki/Byte_order_mark>`_. *(mặc định của trình chỉnh sửa)*
* Sử dụng **Tab** thay vì dấu cách để thụt lề. *(mặc định của trình chỉnh sửa)*

Thụt lề
~~~~~~~

Mỗi cấp thụt lề phải lớn hơn một tab so với khối chứa nó.

**Đúng**:

.. code-block:: glsl

    void fragment() {
        COLOR = vec3(1.0, 1.0, 1.0);
    }

**Sai**:

.. code-block:: glsl

    void fragment() {
            COLOR = vec3(1.0, 1.0, 1.0);
    }

Sử dụng 2 cấp thụt lề để phân biệt các dòng tiếp nối với các khối mã thông thường.

**Đúng**:

.. code-block:: glsl

    vec2 st = vec2(
            atan(NORMAL.x, NORMAL.z),
            acos(NORMAL.y));

**Sai**:

.. code-block:: glsl

    vec2 st = vec2(
        atan(NORMAL.x, NORMAL.z),
        acos(NORMAL.y));


Ngắt dòng và dòng trống
~~~~~~~~~~~~~~~~~~~~~~~

Đối với quy tắc thụt lề chung, hãy tuân theo `"Phong cách 1TBS" <https://en.wikipedia.org/wiki/Indentation_style#Variant:_1TBS_(OTBS)>`_, trong đó khuyến nghị đặt dấu ngoặc nhọn đi kèm câu lệnh điều khiển trên cùng một dòng. Luôn sử dụng dấu ngoặc nhọn cho các câu lệnh, ngay cả khi chúng chỉ chiếm một dòng. Điều này giúp việc tái cấu trúc dễ dàng hơn và tránh sai sót khi thêm nhiều dòng vào một câu lệnh ``if`` hoặc tương tự.

**Đúng**:

.. code-block:: glsl

    void fragment() {
        if (true) {
            // ...
        }
    }

**Sai**:

.. code-block:: glsl

    void fragment()
    {
        if (true)
            // ...
    }

Dòng trống
~~~~~~~~~~

Đặt một (và chỉ một) dòng trống trước và sau mỗi định nghĩa hàm:

.. code-block:: glsl

    void do_something() {
        // ...
    }

    void fragment() {
        // ...
    }

Sử dụng một (và chỉ một) dòng trống bên trong hàm để phân tách các phần logic.

Độ dài dòng
~~~~~~~~~~~

Giữ mỗi dòng mã dưới 100 ký tự.

Nếu có thể, hãy cố gắng giữ các dòng dưới 80 ký tự. Điều này giúp đọc mã trên các màn hình nhỏ và khi mở hai shader cạnh nhau trong một trình soạn thảo văn bản bên ngoài. Ví dụ, khi xem một bản sửa đổi khác biệt.

Mỗi dòng một câu lệnh
~~~~~~~~~~~~~~~~~~~~~

Không bao giờ kết hợp nhiều câu lệnh trên cùng một dòng.

**Đúng**:

.. code-block:: glsl

    void fragment() {
        ALBEDO = vec3(1.0);
        EMISSION = vec3(1.0);
    }

**Sai**:

.. code-block:: glsl

    void fragment() {
        ALBEDO = vec3(1.0); EMISSION = vec3(1.0);
    }

Ngoại lệ duy nhất cho quy tắc này là toán tử ba ngôi:

.. code-block:: glsl

   void fragment() {
        bool should_be_white = true;
        ALBEDO = should_be_white ? vec3(1.0) : vec3(0.0);
    }

Khoảng cách trong chú thích
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Chú thích thông thường nên bắt đầu bằng một dấu cách, nhưng mã được chú thích thì không. Điều này giúp phân biệt chú thích văn bản với mã bị vô hiệu hóa.

**Đúng**:

.. code-block:: glsl

    // Đây là một chú thích.
    //return;

**Sai**:

.. code-block:: glsl

    //Đây là một chú thích.
    // return;

Không sử dụng cú pháp chú thích nhiều dòng nếu chú thích của bạn có thể vừa trên một dòng:

.. code-block:: glsl

    /* Đây là một chú thích khác. */

.. note::

   Trong trình chỉnh sửa shader, để biến mã đã chọn thành chú thích (hoặc bỏ chú thích), hãy nhấn :kbd:`Ctrl + K`. Tính năng này thêm hoặc xóa ``//`` ở đầu các dòng đã chọn.

Chú thích tài liệu
~~~~~~~~~~~~~~~~~~

Sử dụng định dạng sau cho chú thích tài liệu phía trên các uniform, với **hai** dấu hoa thị ở đầu (``/**``) và các dấu hoa thị tiếp theo trên mỗi dòng:

.. code-block:: glsl

    /**
     * Đây là một chú thích tài liệu.
     * Các dòng này sẽ xuất hiện trong trình thanh tra khi di chuột qua tham số shader
     * có tên "Something".
     * Bạn có thể sử dụng định dạng [b]BBCode[/b] [i]trong chú thích[/i].
     */
    uniform int something = 1;

Các chú thích này sẽ xuất hiện khi di chuột qua một thuộc tính trong trình thanh tra. Nếu không muốn chú thích hiển thị trong trình thanh tra, hãy sử dụng cú pháp chú thích tiêu chuẩn thay thế (``// ...`` hoặc ``/* ... */`` chỉ có một dấu hoa thị ở đầu).

Khoảng trắng
~~~~~~~~~~~~

Luôn sử dụng một dấu cách quanh các toán tử và sau dấu phẩy. Ngoài ra, tránh các dấu cách thừa trong lời gọi hàm.

**Đúng**:

.. code-block:: glsl

    COLOR.r = 5.0;
    COLOR.r = COLOR.g + 0.1;
    COLOR.b = some_function(1.0, 2.0);

**Sai**:

.. code-block:: glsl

    COLOR.r=5.0;
    COLOR.r = COLOR.g+0.1;
    COLOR.b = some_function (1.0,2.0);

Không sử dụng dấu cách để căn chỉnh biểu thức theo chiều dọc:

.. code-block:: glsl

    ALBEDO.r   = 1.0;
    EMISSION.r = 1.0;

Số thực
~~~~~~~

Luôn chỉ định ít nhất một chữ số cho cả phần nguyên và phần thập phân. Điều này giúp dễ phân biệt số dấu phẩy động với số nguyên, cũng như phân biệt các số lớn hơn 1 với các số nhỏ hơn 1.

**Tốt**:

.. code-block:: glsl

    void fragment() {
        ALBEDO.rgb = vec3(5.0, 0.1, 0.2);
    }

**Không tốt**:

.. code-block:: glsl

    void fragment() {
        ALBEDO.rgb = vec3(5., .1, .2);
    }

Truy cập các thành phần của vector
----------------------------------

Sử dụng ``r``, ``g``, ``b`` và ``a`` khi truy cập các thành phần của vector nếu vector đó chứa màu. Nếu vector chứa bất kỳ thứ gì khác ngoài màu, hãy sử dụng ``x``, ``y``, ``z`` và ``w``. Điều này giúp người đọc code của bạn hiểu rõ hơn dữ liệu bên dưới biểu diễn điều gì.

**Tốt**:

.. code-block:: glsl

    COLOR.rgb = vec3(5.0, 0.1, 0.2);

**Không tốt**:

.. code-block:: glsl

    COLOR.xyz = vec3(5.0, 0.1, 0.2);

Quy ước đặt tên
---------------

Các quy ước đặt tên này tuân theo phong cách của Godot Engine. Việc vi phạm các quy ước này sẽ khiến code của bạn xung đột với các quy ước đặt tên tích hợp sẵn, dẫn đến code không nhất quán.

Hàm và biến
~~~~~~~~~~~

Sử dụng snake\_case để đặt tên cho hàm và biến:

.. code-block:: glsl

   void some_function() {
        float some_variable = 0.5;
   }

Hằng số
~~~~~~~

Viết hằng số bằng CONSTANT\_CASE, tức là viết toàn bộ bằng chữ in hoa và dùng dấu gạch dưới (\_) để phân tách các từ:

.. code-block:: glsl

    const float GOLDEN_RATIO = 1.618;

Chỉ thị tiền xử lý
~~~~~~~~~~~~~~~~~~

Các chỉ thị :ref:`doc_shader_preprocessor` nên được viết theo CONSTANT_CASE. Chỉ thị phải được viết mà không có bất kỳ mức thụt lề nào ở phía trước, ngay cả khi nằm bên trong một hàm.

Để duy trì luồng thụt lề tự nhiên khi lỗi shader được in ra console, **không** nên thêm mức thụt lề bổ sung bên trong các khối ``#if``, ``#ifdef`` hoặc ``#ifndef``:

**Tốt**:

.. code-block:: glsl

    #define HEIGHTMAP_ENABLED

    void fragment() {
        vec2 position = vec2(1.0, 2.0);

    #ifdef HEIGHTMAP_ENABLED
        sample_heightmap(position);
    #endif
    }

**Không tốt**:

.. code-block:: glsl

    #define heightmap_enabled

    void fragment() {
        vec2 position = vec2(1.0, 2.0);

        #ifdef heightmap_enabled
            sample_heightmap(position);
        #endif
    }

Tự động áp dụng định dạng
-------------------------

Để tự động định dạng các tệp shader, bạn có thể sử dụng `clang-format <https://clang.llvm.org/docs/ClangFormat.html>`__ trên một hoặc nhiều tệp ``.gdshader``, vì cú pháp đủ gần với một ngôn ngữ kiểu C.

Tuy nhiên, style mặc định trong clang-format không tuân theo hướng dẫn style này, vì vậy bạn cần lưu tệp này dưới tên ``.clang-format`` trong thư mục gốc của project:

.. code-block:: yaml

    BasedOnStyle: LLVM
    AlignAfterOpenBracket: DontAlign
    AlignOperands: DontAlign
    AlignTrailingComments:
      Kind: Never
      OverEmptyLines: 0
    AllowAllParametersOfDeclarationOnNextLine: false
    AllowShortFunctionsOnASingleLine: Inline
    BreakConstructorInitializers: AfterColon
    ColumnLimit: 0
    ContinuationIndentWidth: 8
    IndentCaseLabels: true
    IndentWidth: 4
    InsertBraces: true
    KeepEmptyLinesAtTheStartOfBlocks: false
    RemoveSemicolon: true
    SpacesInLineCommentPrefix:
      Minimum: 0 # Chúng tôi muốn số lượng comment tối thiểu là 1, nhưng cho phép 0 đối với code bị vô hiệu hóa.
      Maximum: -1
    TabWidth: 4
    UseTab: Always

Khi đang ở thư mục gốc của project, bạn có thể gọi ``clang-format -i path/to/shader.gdshader`` trong terminal để định dạng một tệp shader, hoặc ``clang-format -i path/to/folder/*.gdshader`` để định dạng tất cả shader trong một thư mục.

Thứ tự code
-----------

Chúng tôi đề xuất tổ chức code shader như sau:

.. code-block:: glsl

    01. shader type declaration
    02. render mode declaration
    03. // docstring

    04. uniforms
    05. constants
    06. varyings

    07. other functions
    08. vertex() function
    09. fragment() function
    10. light() function

Chúng tôi đã tối ưu thứ tự này để giúp dễ đọc code từ trên xuống dưới, giúp các developer lần đầu đọc code hiểu cách code hoạt động và tránh các lỗi liên quan đến thứ tự khai báo biến.

Thứ tự code này tuân theo hai nguyên tắc chung:

1. Metadata và thuộc tính trước, tiếp theo là các method.
2. "Public" đứng trước "private". Trong ngữ cảnh của ngôn ngữ shader, "public" chỉ những gì người dùng có thể dễ dàng điều chỉnh (uniform).

Biến cục bộ
~~~~~~~~~~~

Khai báo biến cục bộ gần với lần sử dụng đầu tiên của chúng nhất có thể. Điều này giúp dễ theo dõi code hơn mà không phải cuộn quá nhiều để tìm nơi biến được khai báo.

.. _`byte order mark`: https://en.wikipedia.org/wiki/Byte_order_mark
.. _`the "1TBS Style"`: https://en.wikipedia.org/wiki/Indentation_style#Variant:_1TBS_(OTBS)
