.. _doc_shader_preprocessor:

Bộ tiền xử lý shader
====================

Tại sao sử dụng bộ tiền xử lý shader?
-------------------------------------

Trong các ngôn ngữ lập trình, một *bộ tiền xử lý* cho phép thay đổi mã trước khi trình biên dịch đọc mã đó. Không giống trình biên dịch, bộ tiền xử lý không quan tâm cú pháp của mã đã được tiền xử lý có hợp lệ hay không. Bộ tiền xử lý luôn thực hiện những gì các *chỉ thị* yêu cầu. Chỉ thị là một câu lệnh bắt đầu bằng ký hiệu dấu thăng (``#``). Đây không phải là một *từ khóa* của ngôn ngữ shader (chẳng hạn như ``if`` hoặc ``for``), mà là một loại token đặc biệt trong ngôn ngữ.

Để tránh lặp lại và cải thiện khả năng tái sử dụng mã, bạn có thể sử dụng bộ tiền xử lý shader trong các shader dựa trên văn bản. Cú pháp tương tự cú pháp mà hầu hết các trình biên dịch shader GLSL hỗ trợ (vốn tương tự bộ tiền xử lý C/C++).

.. note::

    Bộ tiền xử lý shader không khả dụng trong :ref:`visual shaders <doc_visual_shaders>`. Nếu cần thêm các câu lệnh tiền xử lý vào visual shader, bạn có thể chuyển nó thành shader dựa trên văn bản bằng tùy chọn **Convert to Shader** trong menu thả xuống tài nguyên của inspector VisualShader. Thao tác chuyển đổi này chỉ thực hiện được theo một chiều; không thể chuyển shader văn bản ngược lại thành visual shader.

Chỉ thị
-------

Cú pháp chung
~~~~~~~~~~~~~

- Các chỉ thị tiền xử lý không sử dụng dấu ngoặc vuông (``{}``), nhưng có thể sử dụng dấu ngoặc đơn. - Các chỉ thị tiền xử lý **không bao giờ** kết thúc bằng dấu chấm phẩy (ngoại trừ ``#define``, trong đó dấu chấm phẩy được cho phép nhưng có thể gây nguy hiểm). - Các chỉ thị tiền xử lý có thể trải dài trên nhiều dòng bằng cách kết thúc mỗi dòng bằng dấu gạch chéo ngược (``\``). Dòng ngắt đầu tiên *không* có dấu gạch chéo ngược sẽ kết thúc câu lệnh tiền xử lý.

#define
~~~~~~~

**Cú pháp:** ``#define <identifier> [replacement_code]``.

Định nghĩa identifier sau chỉ thị đó dưới dạng macro và thay thế mọi lần xuất hiện tiếp theo của identifier này bằng mã thay thế được cung cấp trong shader. Việc thay thế được thực hiện theo đơn vị "từ hoàn chỉnh", nghĩa là không thay thế nếu chuỗi đó là một phần của chuỗi khác (không có khoảng trắng hoặc toán tử phân tách).

Các định nghĩa có mã thay thế cũng có thể có một hoặc nhiều *đối số*, sau đó có thể truyền các đối số này khi tham chiếu đến define (tương tự một lời gọi hàm).

Nếu mã thay thế không được định nghĩa, identifier chỉ có thể được sử dụng với các chỉ thị ``#ifdef`` hoặc ``#ifndef``.

Nếu ký hiệu *nối* (``##``) xuất hiện trong mã thay thế, ký hiệu này sẽ bị xóa khi chèn macro, cùng với mọi khoảng trắng xung quanh nó, đồng thời nối các từ và đối số xung quanh thành một token mới.

.. code-block:: glsl

    uniform sampler2D material0;

    #define SAMPLE(N) vec4 tex##N = texture(material##N, UV)

    void fragment() {
        SAMPLE(0);
        ALBEDO = tex0.rgb;
    }

So với các hằng số (``const CONSTANT = value;``), ``#define`` có thể được sử dụng ở bất kỳ đâu trong shader (bao gồm cả trong các gợi ý uniform). ``#define`` cũng có thể được sử dụng để chèn mã shader tùy ý vào bất kỳ vị trí nào, trong khi các hằng số không thể làm điều đó.

.. code-block:: glsl

    shader_type spatial;

    // Lưu ý rằng dòng này không có dấu chấm phẩy ở cuối, vì văn bản thay thế
    // không nên tự chèn dấu chấm phẩy.
    // Nếu chỉ thị kết thúc bằng dấu chấm phẩy, dấu chấm phẩy sẽ được chèn vào mọi lần sử dụng
    // chỉ thị đó, ngay cả khi điều này gây ra lỗi cú pháp.
    #define USE_MY_COLOR
    #define MY_COLOR vec3(1, 0, 0)

    // Thay thế có đối số.
    // Tất cả đối số đều bắt buộc (không thể cung cấp giá trị mặc định).
    #define BRIGHTEN_COLOR(r, g, b) vec3(r + 0.5, g + 0.5, b + 0.5)

    // Thay thế nhiều dòng bằng dấu gạch chéo ngược để tiếp tục dòng:
    #define SAMPLE(param1, param2, param3, param4) long_function_call( \
            param1, \
            param2, \
            param3, \
            param4 \
    )

    void fragment() {
    #ifdef USE_MY_COLOR
        ALBEDO = MY_COLOR;
    #endif
    }


Định nghĩa một ``#define`` cho một identifier đã được định nghĩa sẽ gây ra lỗi. Để tránh điều này, hãy sử dụng ``#undef <identifier>``.

#undef
~~~~~~

**Cú pháp:** ``#undef identifier``

Có thể sử dụng chỉ thị ``#undef`` để hủy một chỉ thị ``#define`` đã được định nghĩa trước đó:

.. code-block:: glsl

    #define MY_COLOR vec3(1, 0, 0)

    vec3 get_red_color() {
        return MY_COLOR;
    }

    #undef MY_COLOR
    #define MY_COLOR vec3(0, 1, 0)

    vec3 get_green_color() {
        return MY_COLOR;
    }

    // Giống như trong hầu hết các bộ tiền xử lý, việc hủy một define chưa từng được định nghĩa trước đó là hợp lệ
    // (và sẽ không in ra cảnh báo hay lỗi nào).
    #undef THIS_DOES_NOT_EXIST

Nếu không có ``#undef`` trong ví dụ trên, sẽ xảy ra lỗi định nghĩa lại macro.

#if
~~~

**Cú pháp:** ``#if <condition>``

Chỉ thị ``#if`` kiểm tra ``condition`` được truyền vào. Nếu kết quả đánh giá là giá trị khác không, khối mã sẽ được đưa vào; nếu không, khối mã sẽ bị bỏ qua.

Để được đánh giá chính xác, điều kiện phải là một biểu thức cho kết quả là một giá trị dấu phẩy động, số nguyên hoặc boolean đơn giản. Có thể có nhiều khối điều kiện được nối bằng các toán tử ``&&`` (AND) hoặc ``||`` (OR). Khối này có thể được tiếp nối bằng khối ``#else``, nhưng **phải** kết thúc bằng chỉ thị ``#endif``.

.. code-block:: glsl

    #define VAR 3
    #define USE_LIGHT 0 // Đánh giá thành `false`.
    #define USE_COLOR 1 // Đánh giá thành `true`.

    #if VAR == 3 && (USE_LIGHT || USE_COLOR)
    // Điều kiện là `true`. Đưa phần này vào shader cuối cùng.
    #endif

Bằng *hàm tiền xử lý* ``defined()``, bạn có thể kiểm tra xem identifier được truyền vào có được định nghĩa bởi một ``#define`` đặt phía trên chỉ thị đó hay không. Điều này hữu ích khi tạo nhiều phiên bản shader trong cùng một tệp. Khối này có thể được tiếp nối bằng khối ``#else``, nhưng phải kết thúc bằng chỉ thị ``#endif``.

Kết quả của hàm ``defined()`` có thể được phủ định bằng cách sử dụng ký hiệu ``!`` (NOT boolean) ở phía trước hàm. Có thể dùng cách này để kiểm tra xem một define *chưa* được thiết lập hay không.

.. code-block:: glsl

    #define USE_LIGHT
    #define USE_COLOR

    // Cú pháp chính xác:
    #if defined(USE_LIGHT) || defined(USE_COLOR) || !defined(USE_REFRACTION)
    // Điều kiện là `true`. Đưa phần này vào shader cuối cùng.
    #endif

Hãy cẩn thận: ``defined()`` chỉ được bao bọc một identifier duy nhất bên trong dấu ngoặc đơn, không bao giờ được bao bọc nhiều hơn:

.. code-block:: glsl

    // Cú pháp không chính xác (dấu ngoặc đơn không được đặt đúng vị trí):
    #if defined(USE_LIGHT || USE_COLOR || !USE_REFRACTION)
    // Điều này sẽ gây ra lỗi hoặc khiến mã không hoạt động như mong đợi.
    #endif

.. tip::

    Trong shader editor, các nhánh tiền xử lý đánh giá thành ``false`` (và do đó bị loại khỏi shader được biên dịch cuối cùng) sẽ hiển thị màu xám. Điều này không áp dụng cho các câu lệnh ``if`` runtime.

**Bộ tiền xử lý #if so với câu lệnh if: Lưu ý về hiệu năng**

:ref:`shading language <doc_shading_language>` hỗ trợ các câu lệnh ``if`` runtime:

.. code-block:: glsl

    uniform bool USE_LIGHT = true;

    if (USE_LIGHT) {
        // Phần này được đưa vào shader đã biên dịch và luôn được chạy.
    } else {
        // Phần này được đưa vào shader đã biên dịch nhưng không bao giờ được chạy.
    }

Nếu uniform không bao giờ thay đổi, cách này hoạt động giống hệt cách sử dụng câu lệnh tiền xử lý ``#if`` sau đây:

.. code-block:: glsl

    #define USE_LIGHT

    #if defined(USE_LIGHT)
    // Phần này được đưa vào shader đã biên dịch và luôn được chạy.
    #else
    // Phần này *không* được đưa vào shader đã biên dịch (và do đó không bao giờ được chạy).
    #endif

Tuy nhiên, biến thể ``#if`` có thể nhanh hơn trong một số trường hợp. Nguyên nhân là tất cả các nhánh runtime trong shader vẫn được biên dịch và các biến bên trong những nhánh đó vẫn có thể chiếm dung lượng thanh ghi, ngay cả khi trên thực tế chúng không bao giờ được chạy.

Các GPU hiện đại `quite effective <https://medium.com/@jasonbooth_86226/branching-on-a-gpu-18bfc83694f2>`__ rất tốt trong việc thực hiện phân nhánh "tĩnh". Phân nhánh "tĩnh" là các câu lệnh ``if`` trong đó *tất cả* pixel/vertex đều cho cùng một kết quả trong một lần gọi shader nhất định. Tuy nhiên, lượng lớn :abbr:`VGPRs (Vector General-Purpose Register)` (có thể do có quá nhiều nhánh) vẫn có thể làm chậm đáng kể quá trình thực thi shader.

#elif
~~~~~

Chỉ thị ``#elif`` là viết tắt của "else if" và kiểm tra điều kiện được truyền vào nếu ``#if`` ở trên đánh giá thành ``false``. ``#elif`` chỉ có thể được sử dụng bên trong một khối ``#if``. Có thể sử dụng nhiều câu lệnh ``#elif`` sau một câu lệnh ``#if``.

.. code-block:: glsl

    #define VAR 2

    #if VAR == 0
    // Không được đưa vào.
    #elif VAR == 1
    // Không được đưa vào.
    #elif VAR == 2
    // Điều kiện là `true`. Đưa phần này vào shader cuối cùng.
    #else
    // Không được đưa vào.
    #endif

Giống như ``#if``, có thể sử dụng hàm tiền xử lý ``defined()``:

.. code-block:: glsl

    #define SHADOW_QUALITY_MEDIUM

    #if defined(SHADOW_QUALITY_HIGH)
    // Chất lượng bóng cao.
    #elif defined(SHADOW_QUALITY_MEDIUM)
    // Chất lượng bóng trung bình.
    #else
    // Chất lượng bóng thấp.
    #endif

#ifdef
~~~~~~

**Cú pháp:** ``#ifdef <identifier>``

Đây là cách viết tắt của ``#if defined(...)``. Kiểm tra xem identifier được truyền vào có được định nghĩa bởi ``#define`` được đặt phía trên directive đó hay không. Điều này hữu ích khi tạo nhiều phiên bản shader trong cùng một tệp. Có thể tiếp nối bằng một block ``#else``, nhưng phải kết thúc bằng directive ``#endif``.

.. code-block:: glsl

    #define USE_LIGHT

    #ifdef USE_LIGHT
    // USE_LIGHT đã được định nghĩa. Đưa phần này vào shader cuối cùng.
    #endif

Bộ xử lý *không* hỗ trợ ``#elifdef`` như một cách viết tắt cho ``#elif defined(...)``. Thay vào đó, hãy sử dụng chuỗi ``#ifdef`` và ``#else`` sau đây khi cần nhiều hơn hai nhánh:

.. code-block:: glsl

    #define SHADOW_QUALITY_MEDIUM

    #ifdef SHADOW_QUALITY_HIGH
    // Chất lượng bóng cao.
    #else
    #ifdef SHADOW_QUALITY_MEDIUM
    // Chất lượng bóng trung bình.
    #else
    // Chất lượng bóng thấp.
    #endif // Kết thúc nhánh của `SHADOW_QUALITY_MEDIUM`.
    #endif // Kết thúc nhánh của `SHADOW_QUALITY_HIGH`.

#ifndef
~~~~~~~

**Cú pháp:** ``#ifndef <identifier>``

Đây là cách viết tắt của ``#if !defined(...)``. Tương tự ``#ifdef``, nhưng kiểm tra xem identifier được truyền vào **không** được định nghĩa bởi ``#define`` trước directive đó hay không.

Đây chính xác là điều ngược lại với ``#ifdef``; nó sẽ luôn khớp trong những tình huống mà ``#ifdef`` sẽ không bao giờ khớp, và ngược lại.

.. code-block:: glsl

    #define USE_LIGHT

    #ifndef USE_LIGHT
    // Đánh giá thành `false`. Phần này sẽ không được đưa vào shader cuối cùng.
    #endif

    #ifndef USE_COLOR
    // Đánh giá thành `true`. Phần này sẽ được đưa vào shader cuối cùng.
    #endif

#else
~~~~~

**Cú pháp:** ``#else``

Định nghĩa block tùy chọn được đưa vào khi directive ``#if``, ``#elif``, ``#ifdef`` hoặc ``#ifndef`` được định nghĩa trước đó đánh giá thành false.

.. code-block:: glsl

    shader_type spatial;

    #define MY_COLOR vec3(1.0, 0, 0)

    void fragment() {
    #ifdef MY_COLOR
        ALBEDO = MY_COLOR;
    #else
        ALBEDO = vec3(0, 0, 1.0);
    #endif
    }

#endif
~~~~~~

**Cú pháp:** ``#endif``

Được dùng làm terminator cho các directive ``#if``, ``#ifdef``, ``#ifndef`` hoặc directive ``#else`` tiếp theo.

#error
~~~~~~

**Cú pháp:** ``#error <message>``

Directive ``#error`` buộc preprocessor phát ra một lỗi cùng thông báo tùy chọn. Ví dụ, directive này hữu ích khi được dùng trong block ``#if`` để áp dụng giới hạn nghiêm ngặt cho giá trị đã định nghĩa.

.. code-block:: glsl

    #define MAX_LOD 3
    #define LOD 4

    #if LOD > MAX_LOD
    #error LOD exceeds MAX_LOD
    #endif

#include
~~~~~~~~

**Cú pháp:** ``#include "path"``

Directive ``#include`` đưa *toàn bộ* nội dung của tệp shader include vào một shader. ``"path"`` có thể là đường dẫn ``res://`` tuyệt đối hoặc đường dẫn tương đối so với tệp shader hiện tại. Chỉ các shader được lưu vào tệp ``.gdshader`` hoặc ``.gdshaderinc`` mới được phép sử dụng đường dẫn tương đối, trong khi đường dẫn tuyệt đối có thể được dùng trong các shader được tích hợp vào tệp scene/resource.

Bạn có thể tạo shader include mới bằng tùy chọn menu **File > Create Shader Include** của shader editor, hoặc bằng cách tạo một resource :ref:`ShaderInclude<class_ShaderInclude>` mới trong dock FileSystem.

Shader include có thể được đưa vào từ bất kỳ shader hoặc shader include nào khác, tại bất kỳ vị trí nào trong tệp.

Khi đưa shader include vào global scope của shader, bạn nên thực hiện việc này sau statement ``shader_type`` ban đầu.

Bạn cũng có thể đưa shader include vào bên trong phần thân của một function. Lưu ý rằng shader editor có thể sẽ báo lỗi đối với code trong shader include, vì code đó có thể không hợp lệ khi nằm ngoài context mà nó được viết cho. Bạn có thể chọn bỏ qua các lỗi này (shader vẫn sẽ compile bình thường), hoặc bọc include trong một block ``#ifdef`` để kiểm tra một define từ shader của bạn.

``#include`` hữu ích khi tạo các thư viện helper function (hoặc macro) và giảm việc lặp code. Khi sử dụng ``#include``, hãy cẩn thận với các xung đột tên, vì không cho phép định nghĩa lại function hoặc macro.

``#include`` chịu một số hạn chế:

- Chỉ các shader include resource (có phần mở rộng ``.gdshaderinc``) mới có thể được include. Các tệp ``.gdshader`` không thể được shader khác include, nhưng một tệp ``.gdshaderinc`` có thể include các tệp ``.gdshaderinc`` khác. - Không cho phép **cyclic dependency** và sẽ dẫn đến lỗi. - Để tránh đệ quy vô hạn, độ sâu include được giới hạn ở 25 bước.

Tệp shader include ví dụ:

.. code-block:: glsl

    // fancy_color.gdshaderinc

    // Mặc dù về mặt kỹ thuật được phép, các tệp include thường không có khai báo `shader_type`.

    vec3 get_fancy_color() {
        return vec3(0.3, 0.6, 0.9);
    }

Shader cơ sở ví dụ (sử dụng tệp include mà chúng ta đã tạo ở trên):

.. code-block:: glsl

    // material.gdshader

    shader_type spatial;

    #include "res://fancy_color.gdshaderinc"

    void fragment() {
        // Không có lỗi, vì chúng ta đã include định nghĩa cho `get_fancy_color()` thông qua shader include.
        COLOR = get_fancy_color();
    }

#pragma
~~~~~~~

**Cú pháp:** ``#pragma value``

Directive ``#pragma`` cung cấp thông tin bổ sung cho preprocessor hoặc compiler.

Hiện tại, directive này chỉ có thể nhận một giá trị: ``disable_preprocessor``. Nếu không cần preprocessor, hãy sử dụng directive đó để tăng tốc quá trình compile shader bằng cách loại bỏ bước preprocessor.

.. code-block:: glsl

    #pragma disable_preprocessor

    #if USE_LIGHT
    // Điều này gây ra lỗi compile shader, vì `#if USE_LIGHT` và `#endif`
    // được giữ nguyên như trong code shader cuối cùng.
    #endif

Các define tích hợp sẵn
-----------------------

Renderer hiện tại
~~~~~~~~~~~~~~~~~

Kể từ Godot 4.4, bạn có thể kiểm tra renderer hiện đang được sử dụng bằng các define tích hợp sẵn ``CURRENT_RENDERER``, ``RENDERER_COMPATIBILITY``, ``RENDERER_MOBILE`` và ``RENDERER_FORWARD_PLUS``:

- ``CURRENT_RENDERER`` được đặt thành ``0``, ``1`` hoặc ``2`` tùy thuộc vào renderer hiện tại. - ``RENDERER_COMPATIBILITY`` luôn là ``0``. - ``RENDERER_MOBILE`` luôn là ``1``. - ``RENDERER_FORWARD_PLUS`` luôn là ``2``.

Ví dụ, shader này đặt ``ALBEDO`` thành một màu khác nhau trong mỗi renderer:

.. code-block:: glsl

    shader_type spatial;

    void fragment() {
    #if CURRENT_RENDERER == RENDERER_COMPATIBILITY
        ALBEDO = vec3(0.0, 0.0, 1.0);
    #elif CURRENT_RENDERER == RENDERER_MOBILE
        ALBEDO = vec3(1.0, 0.0, 0.0);
    #else // CURRENT_RENDERER == RENDERER_FORWARD_PLUS
        ALBEDO = vec3(0.0, 1.0, 0.0);
    #endif
    }
