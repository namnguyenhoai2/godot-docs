.. _doc_shaders_style_guide:

Hướng dẫn về style của shader
=============================

Hướng dẫn về style này liệt kê các quy ước để viết shader thanh thoát. Mục tiêu là khuyến khích viết code sạch, dễ đọc và thúc đẩy tính nhất quán giữa các dự án, cuộc thảo luận và tutorial. Hy vọng tài liệu này cũng hỗ trợ việc phát triển các công cụ tự động format.

Vì ngôn ngữ shader của Godot gần với các ngôn ngữ kiểu C và GLSL, hướng dẫn này được lấy cảm hứng từ cách format GLSL của chính Godot. Bạn có thể xem các ví dụ về file GLSL trong mã nguồn của Godot `here <https://github.com/godotengine/godot/blob/master/drivers/gles3/shaders/>`__.

Style guide không nhằm trở thành những bộ luật cứng nhắc. Đôi khi, bạn có thể không áp dụng được một số hướng dẫn dưới đây. Khi đó, hãy sử dụng phán đoán tốt nhất của mình và hỏi các developer khác để có thêm góc nhìn.

Nhìn chung, việc giữ code nhất quán trong các dự án và trong nhóm của bạn quan trọng hơn việc tuân thủ hướng dẫn này một cách tuyệt đối.

.. note:: Godot's built-in shader editor uses a lot of these conventions
          theo mặc định. Hãy để nó hỗ trợ bạn.

Sau đây là một ví dụ shader hoàn chỉnh dựa trên các hướng dẫn này:

.. code-block:: glsl

    shader_type canvas_item;
    // Shader trong screen space để điều chỉnh độ sáng, độ tương phản của một scene 2D
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

Format
------

Encoding và ký tự đặc biệt
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Sử dụng ký tự line feed (**LF**) để ngắt dòng, không dùng CRLF hoặc CR. *(mặc định của editor)* * Sử dụng một ký tự line feed ở cuối mỗi file. *(mặc định của editor)* * Sử dụng encoding **UTF-8** không có `byte order mark <https://en.wikipedia.org/wiki/Byte_order_mark>`_. *(mặc định của editor)* * Sử dụng **Tab** thay vì space để thụt lề. *(mặc định của editor)*

Thụt lề
~~~~~~~

Mỗi cấp thụt lề phải nhiều hơn block chứa nó một tab.

**Tốt**:

.. code-block:: glsl

    void fragment() {
        COLOR = vec3(1.0, 1.0, 1.0);
    }

**Xấu**:

.. code-block:: glsl

    void fragment() {
            COLOR = vec3(1.0, 1.0, 1.0);
    }

Sử dụng 2 cấp thụt lề để phân biệt các dòng tiếp nối với các block code thông thường.

**Tốt**:

.. code-block:: glsl

    vec2 st = vec2(
            atan(NORMAL.x, NORMAL.z),
            acos(NORMAL.y));

**Xấu**:

.. code-block:: glsl

    vec2 st = vec2(
        atan(NORMAL.x, NORMAL.z),
        acos(NORMAL.y));


Ngắt dòng và dòng trống
~~~~~~~~~~~~~~~~~~~~~~~

Đối với quy tắc thụt lề chung, hãy làm theo `the "1TBS Style" <https://en.wikipedia.org/wiki/Indentation_style#Variant:_1TBS_(OTBS)>`_, trong đó khuyến nghị đặt dấu ngoặc nhọn đi kèm với một câu lệnh điều khiển trên cùng dòng. Luôn sử dụng dấu ngoặc nhọn cho các câu lệnh, ngay cả khi chúng chỉ trải dài một dòng. Điều này giúp chúng dễ refactor hơn và tránh sai sót khi thêm nhiều dòng vào một câu lệnh ``if`` hoặc tương tự.

**Tốt**:

.. code-block:: glsl

    void fragment() {
        if (true) {
            // ...
        }
    }

**Xấu**:

.. code-block:: glsl

    void fragment()
    {
        if (true)
            // ...
    }

Dòng trống
~~~~~~~~~~

Bao quanh các định nghĩa hàm bằng một (và chỉ một) dòng trống:

.. code-block:: glsl

    void do_something() {
        // ...
    }

    void fragment() {
        // ...
    }

Sử dụng một (và chỉ một) dòng trống bên trong các hàm để phân tách những phần logic.

Độ dài dòng
~~~~~~~~~~~

Giữ mỗi dòng code dưới 100 ký tự.

Nếu có thể, hãy cố gắng giữ các dòng dưới 80 ký tự. Điều này giúp đọc code trên màn hình nhỏ và khi mở hai shader cạnh nhau trong một text editor bên ngoài. Ví dụ, khi xem một revision khác biệt.

Một câu lệnh trên mỗi dòng
~~~~~~~~~~~~~~~~~~~~~~~~~~

Không bao giờ gộp nhiều câu lệnh trên cùng một dòng.

**Tốt**:

.. code-block:: glsl

    void fragment() {
        ALBEDO = vec3(1.0);
        EMISSION = vec3(1.0);
    }

**Xấu**:

.. code-block:: glsl

    void fragment() {
        ALBEDO = vec3(1.0); EMISSION = vec3(1.0);
    }

Ngoại lệ duy nhất của quy tắc này là toán tử ternary:

.. code-block:: glsl

   void fragment() {
        bool should_be_white = true;
        ALBEDO = should_be_white ? vec3(1.0) : vec3(0.0);
    }

Khoảng cách trong comment
~~~~~~~~~~~~~~~~~~~~~~~~~

Các comment thông thường nên bắt đầu bằng một khoảng trắng, nhưng code được comment out thì không. Điều này giúp phân biệt comment dạng văn bản với code bị vô hiệu hóa.

**Tốt**:

.. code-block:: glsl

    // Đây là một comment.
    //return;

**Xấu**:

.. code-block:: glsl

    //Đây là một comment.
    // return;

Không sử dụng cú pháp comment nhiều dòng nếu comment của bạn có thể vừa trên một dòng:

.. code-block:: glsl

    /* Đây là một comment khác. */

.. note::

   Trong shader editor, để biến phần code được chọn thành comment (hoặc bỏ comment), hãy nhấn :kbd:`Ctrl + K`. Tính năng này thêm hoặc xóa ``//`` ở đầu các dòng được chọn.

Comment tài liệu
~~~~~~~~~~~~~~~~

Sử dụng format sau cho các comment tài liệu bên trên uniform, với **hai** dấu hoa thị ở đầu (``/**``) và các dấu hoa thị tiếp theo trên mỗi dòng:

.. code-block:: glsl

    /**
     * Đây là một comment tài liệu.
     * Các dòng này sẽ xuất hiện trong inspector khi di chuột lên tham số shader
     * có tên là "Something".
     * Bạn có thể sử dụng [b]BBCode[/b] [i]formatting[/i] trong comment.
     */
    uniform int something = 1;

Các comment này sẽ xuất hiện khi di chuột lên một property trong inspector. Nếu không muốn comment hiển thị trong inspector, hãy sử dụng cú pháp comment tiêu chuẩn thay thế (``// ...`` hoặc ``/* ... */`` với chỉ một dấu hoa thị ở đầu).

Khoảng trắng
~~~~~~~~~~~~

Luôn sử dụng một khoảng trắng xung quanh các toán tử và sau dấu phẩy. Ngoài ra, tránh các khoảng trắng thừa trong lời gọi hàm.

**Tốt**:

.. code-block:: glsl

    COLOR.r = 5.0;
    COLOR.r = COLOR.g + 0.1;
    COLOR.b = some_function(1.0, 2.0);

**Xấu**:

.. code-block:: glsl

    COLOR.r=5.0;
    COLOR.r = COLOR.g+0.1;
    COLOR.b = some_function (1.0,2.0);

Không sử dụng khoảng trắng để căn chỉnh các biểu thức theo chiều dọc:

.. code-block:: glsl

    ALBEDO.r   = 1.0;
    EMISSION.r = 1.0;

Số thực dấu phẩy động
~~~~~~~~~~~~~~~~~~~~~

Luôn chỉ định ít nhất một chữ số cho cả phần nguyên và phần thập phân. Điều này giúp phân biệt số thực dấu phẩy động với số nguyên dễ hơn, đồng thời phân biệt các số lớn hơn 1 với các số nhỏ hơn 1.

**Tốt**:

.. code-block:: glsl

    void fragment() {
        ALBEDO.rgb = vec3(5.0, 0.1, 0.2);
    }

**Xấu**:

.. code-block:: glsl

    void fragment() {
        ALBEDO.rgb = vec3(5., .1, .2);
    }

Truy cập các member của vector
------------------------------

Sử dụng ``r``, ``g``, ``b`` và ``a`` khi truy cập các member của vector nếu vector đó chứa màu. Nếu vector chứa bất kỳ thứ gì khác ngoài màu, hãy sử dụng ``x``, ``y``, ``z`` và ``w``. Điều này giúp người đọc code hiểu rõ hơn dữ liệu bên dưới biểu diễn điều gì.

**Tốt**:

.. code-block:: glsl

    COLOR.rgb = vec3(5.0, 0.1, 0.2);

**Xấu**:

.. code-block:: glsl

    COLOR.xyz = vec3(5.0, 0.1, 0.2);

Quy ước đặt tên
---------------

Các quy ước đặt tên này tuân theo style của Godot Engine. Việc phá vỡ các quy ước này sẽ khiến code của bạn xung đột với quy ước đặt tên tích hợp sẵn, dẫn đến code không nhất quán.

Hàm và biến
~~~~~~~~~~~

Sử dụng snake\_case để đặt tên cho hàm và biến:

.. code-block:: glsl

   void some_function() {
        float some_variable = 0.5;
   }

Hằng số
~~~~~~~

Viết hằng số bằng CONSTANT\_CASE, tức là viết toàn bộ bằng chữ hoa và sử dụng dấu gạch dưới (\_) để phân tách các từ:

.. code-block:: glsl

    const float GOLDEN_RATIO = 1.618;

Các chỉ thị tiền xử lý
~~~~~~~~~~~~~~~~~~~~~~

:ref:`doc_shader_preprocessor` directives should be written in CONSTANT_CASE.
Các chỉ thị phải được viết mà không có bất kỳ thụt lề nào ở phía trước, ngay cả khi nằm bên trong một hàm.

Để giữ luồng thụt lề tự nhiên khi lỗi shader được in ra console, **không** được thêm thụt lề bổ sung bên trong các block ``#if``, ``#ifdef`` hoặc ``#ifndef``:

**Tốt**:

.. code-block:: glsl

    #define HEIGHTMAP_ENABLED

    void fragment() {
        vec2 position = vec2(1.0, 2.0);

    #ifdef HEIGHTMAP_ENABLED
        sample_heightmap(position);
    #endif
    }

**Xấu**:

.. code-block:: glsl

    #define heightmap_enabled

    void fragment() {
        vec2 position = vec2(1.0, 2.0);

        #ifdef heightmap_enabled
            sample_heightmap(position);
        #endif
    }

Áp dụng format tự động
----------------------

Để tự động format các file shader, bạn có thể sử dụng `clang-format <https://clang.llvm.org/docs/ClangFormat.html>`__ trên một hoặc nhiều file ``.gdshader``, vì cú pháp đủ gần với một ngôn ngữ kiểu C.

Tuy nhiên, style mặc định trong clang-format không tuân theo style guide này, nên bạn cần lưu file này dưới tên ``.clang-format`` trong thư mục gốc của dự án:

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
      Minimum: 0 # Chúng ta muốn giá trị tối thiểu là 1 cho comment, nhưng cho phép giá trị 0 đối với code bị vô hiệu hóa.
      Maximum: -1
    TabWidth: 4
    UseTab: Always

Khi đang ở thư mục gốc của dự án, bạn có thể gọi ``clang-format -i path/to/shader.gdshader`` trong terminal để format một file shader, hoặc ``clang-format -i path/to/folder/*.gdshader`` để format tất cả shader trong một thư mục.

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

Chúng tôi đã tối ưu thứ tự này để code dễ đọc từ trên xuống dưới, giúp các developer lần đầu đọc code hiểu cách hoạt động của nó và tránh các lỗi liên quan đến thứ tự khai báo biến.

Thứ tự code này tuân theo hai quy tắc kinh nghiệm:

1. Trước tiên là metadata và property, tiếp theo là các method. 2. "Public" đứng trước "private". Trong ngữ cảnh của ngôn ngữ shader, "public" đề cập đến những gì người dùng có thể dễ dàng điều chỉnh (uniform).

Biến cục bộ
~~~~~~~~~~~

Khai báo biến cục bộ gần vị trí sử dụng đầu tiên của chúng nhất có thể. Điều này giúp theo dõi code dễ hơn mà không phải cuộn quá nhiều để tìm nơi biến được khai báo.
