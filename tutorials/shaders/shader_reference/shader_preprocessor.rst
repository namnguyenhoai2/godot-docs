.. _doc_shader_preprocessor:

Bộ tiền xử lý shader
====================

Tại sao nên sử dụng bộ tiền xử lý shader?
-----------------------------------------

Trong các ngôn ngữ lập trình, *bộ tiền xử lý* cho phép thay đổi mã trước khi trình biên dịch đọc mã đó. Không giống trình biên dịch, bộ tiền xử lý không quan tâm cú pháp của mã đã tiền xử lý có hợp lệ hay không. Bộ tiền xử lý luôn thực hiện những gì các *chỉ thị* yêu cầu. Chỉ thị là một câu lệnh bắt đầu bằng ký hiệu thăng (``#``). Đây không phải là *từ khóa* của ngôn ngữ shader (chẳng hạn như ``if`` hoặc ``for``), mà là một loại token đặc biệt trong ngôn ngữ.

Để tránh lặp lại và cải thiện khả năng tái sử dụng mã, bạn có thể sử dụng bộ tiền xử lý shader trong các shader dựa trên văn bản. Cú pháp tương tự như cú pháp mà hầu hết trình biên dịch shader GLSL hỗ trợ (và bản thân cú pháp đó cũng tương tự bộ tiền xử lý C/C++).

.. note::

    Bộ tiền xử lý shader không khả dụng trong :ref:`shader trực quan <doc_visual_shaders>`. Nếu cần thêm các câu lệnh tiền xử lý vào shader trực quan, bạn có thể chuyển nó thành shader dựa trên văn bản bằng tùy chọn **Convert to Shader** trong danh sách thả xuống tài nguyên của trình kiểm tra VisualShader. Đây là thao tác chuyển đổi một chiều; shader văn bản không thể được chuyển đổi ngược thành shader trực quan.

Các chỉ thị
-----------

Cú pháp chung
~~~~~~~~~~~~~

- Các chỉ thị tiền xử lý không sử dụng dấu ngoặc vuông (``{}``), nhưng có thể sử dụng dấu ngoặc đơn.
- Các chỉ thị tiền xử lý **không bao giờ** kết thúc bằng dấu chấm phẩy (ngoại trừ ``#define``, nơi dấu chấm phẩy được phép nhưng có thể gây nguy hiểm).
- Các chỉ thị tiền xử lý có thể trải dài trên nhiều dòng bằng cách kết thúc mỗi dòng bằng dấu gạch chéo ngược (``\``). Dấu ngắt dòng đầu tiên *không* có dấu gạch chéo ngược sẽ kết thúc câu lệnh tiền xử lý.

#define
~~~~~~~

**Cú pháp:** ``#define <identifier> [replacement_code]``.

Định nghĩa identifier sau chỉ thị đó thành một macro và thay thế mọi lần xuất hiện tiếp theo của identifier bằng mã thay thế được cung cấp trong shader. Việc thay thế được thực hiện theo cơ chế "toàn bộ từ", nghĩa là không thay thế nếu chuỗi đó là một phần của chuỗi khác (không có khoảng trắng hoặc toán tử phân cách).

Các định nghĩa có mã thay thế cũng có thể có một hoặc nhiều *đối số*, sau đó các đối số này có thể được truyền khi tham chiếu đến define (tương tự như lời gọi hàm).

Nếu mã thay thế không được định nghĩa, identifier chỉ có thể được sử dụng với các chỉ thị ``#ifdef`` hoặc ``#ifndef``.

Nếu ký hiệu *nối* (``##``) xuất hiện trong mã thay thế, ký hiệu đó sẽ bị xóa khi chèn macro, cùng với mọi khoảng trắng xung quanh, đồng thời nối các từ và đối số xung quanh thành một token mới.

.. code-block:: glsl

    uniform sampler2D material0;

    #define SAMPLE(N) vec4 tex##N = texture(material##N, UV)

    void fragment() {
        SAMPLE(0);
        ALBEDO = tex0.rgb;
    }

So với các hằng số (``const CONSTANT = value;``), ``#define`` có thể được sử dụng ở bất kỳ đâu trong shader (bao gồm cả trong các gợi ý uniform). ``#define`` cũng có thể được sử dụng để chèn mã shader tùy ý tại bất kỳ vị trí nào, còn hằng số thì không thể.

.. code-block:: glsl

    shader_type spatial;

    // Lưu ý không có dấu chấm phẩy ở cuối dòng, vì văn bản thay thế
    // không nên tự chèn dấu chấm phẩy.
    // Nếu chỉ thị kết thúc bằng dấu chấm phẩy, dấu chấm phẩy sẽ được chèn trong mọi lần sử dụng
    // chỉ thị đó, ngay cả khi điều này gây ra lỗi cú pháp.
    #define USE_MY_COLOR
    #define MY_COLOR vec3(1, 0, 0)

    // Thay thế với các đối số.
    // Tất cả các đối số đều bắt buộc (không thể cung cấp giá trị mặc định).
    #define BRIGHTEN_COLOR(r, g, b) vec3(r + 0.5, g + 0.5, b + 0.5)

    // Thay thế nhiều dòng bằng dấu gạch chéo ngược để tiếp tục:
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

Chỉ thị ``#undef`` có thể được sử dụng để hủy một chỉ thị ``#define`` đã được định nghĩa trước đó:

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

    // Giống như trong hầu hết bộ tiền xử lý, việc hủy định nghĩa một define chưa từng được định nghĩa trước đó là được phép
    // (và sẽ không in ra bất kỳ cảnh báo hay lỗi nào).
    #undef THIS_DOES_NOT_EXIST

Nếu không có ``#undef`` trong ví dụ trên, sẽ xảy ra lỗi định nghĩa lại macro.

#if
~~~

**Cú pháp:** ``#if <condition>``

Chỉ thị ``#if`` kiểm tra ``condition`` được truyền vào. Nếu kết quả là một giá trị khác 0, khối mã sẽ được đưa vào; nếu không, khối mã sẽ bị bỏ qua.

Để được đánh giá chính xác, điều kiện phải là một biểu thức cho kết quả số thực, số nguyên hoặc boolean đơn giản. Có thể có nhiều khối điều kiện được nối bằng các toán tử ``&&`` (AND) hoặc ``||`` (OR). Khối này có thể được tiếp nối bởi một khối ``#else``, nhưng **phải** kết thúc bằng chỉ thị ``#endif``.

.. code-block:: glsl

    #define VAR 3
    #define USE_LIGHT 0 // Cho kết quả `false`.
    #define USE_COLOR 1 // Cho kết quả `true`.

    #if VAR == 3 && (USE_LIGHT || USE_COLOR)
    // Điều kiện là `true`. Đưa phần này vào shader cuối cùng.
    #endif

Bằng cách sử dụng ``defined()`` *hàm tiền xử lý*, bạn có thể kiểm tra xem identifier được truyền vào có được định nghĩa bởi một ``#define`` đặt phía trên chỉ thị đó hay không. Điều này hữu ích khi tạo nhiều phiên bản shader trong cùng một tệp. Khối này có thể được tiếp nối bởi một khối ``#else``, nhưng phải kết thúc bằng chỉ thị ``#endif``.

Kết quả của hàm ``defined()`` có thể được phủ định bằng cách sử dụng ký hiệu ``!`` (NOT boolean) ở phía trước hàm. Cách này có thể được dùng để kiểm tra xem một define có *không* được thiết lập hay không.

.. code-block:: glsl

    #define USE_LIGHT
    #define USE_COLOR

    // Cú pháp đúng:
    #if defined(USE_LIGHT) || defined(USE_COLOR) || !defined(USE_REFRACTION)
    // Điều kiện là `true`. Đưa phần này vào shader cuối cùng.
    #endif

Hãy cẩn thận, vì ``defined()`` chỉ được bao quanh một identifier duy nhất trong dấu ngoặc đơn, không bao giờ được bao quanh nhiều identifier:

.. code-block:: glsl

    // Cú pháp không đúng (dấu ngoặc đơn không được đặt ở vị trí thích hợp):
    #if defined(USE_LIGHT || USE_COLOR || !USE_REFRACTION)
    // Điều này sẽ gây ra lỗi hoặc hoạt động không như mong đợi.
    #endif

.. tip::

    Trong trình chỉnh sửa shader, các nhánh tiền xử lý cho kết quả ``false`` (và do đó bị loại khỏi shader được biên dịch cuối cùng) sẽ hiển thị màu xám. Điều này không áp dụng cho các câu lệnh ``if`` trong runtime.

**Bộ tiền xử lý #if so với câu lệnh if: Lưu ý về hiệu năng**

:ref:`Ngôn ngữ shading <doc_shading_language>` hỗ trợ các câu lệnh ``if`` trong runtime:

.. code-block:: glsl

    uniform bool USE_LIGHT = true;

    if (USE_LIGHT) {
        // Phần này được đưa vào shader đã biên dịch và luôn được chạy.
    } else {
        // Phần này được đưa vào shader đã biên dịch nhưng không bao giờ được chạy.
    }

Nếu uniform không bao giờ thay đổi, hành vi này giống hệt cách sử dụng câu lệnh tiền xử lý ``#if`` sau đây:

.. code-block:: glsl

    #define USE_LIGHT

    #if defined(USE_LIGHT)
    // Phần này được đưa vào shader đã biên dịch và luôn được chạy.
    #else
    // Phần này *không* được đưa vào shader đã biên dịch (và do đó không bao giờ được chạy).
    #endif

Tuy nhiên, biến thể ``#if`` có thể nhanh hơn trong một số tình huống nhất định. Điều này là do tất cả các nhánh runtime trong shader vẫn được biên dịch và các biến bên trong những nhánh đó vẫn có thể chiếm không gian thanh ghi, ngay cả khi chúng không bao giờ thực sự được chạy.

GPU hiện đại `thực hiện rất hiệu quả <https://medium.com/@jasonbooth_86226/branching-on-a-gpu-18bfc83694f2>`__ việc rẽ nhánh "tĩnh". Rẽ nhánh "tĩnh" đề cập đến các câu lệnh ``if`` trong đó *tất cả* pixel/vertex đều cho cùng một kết quả trong một lần shader được gọi cụ thể. Tuy nhiên, lượng :abbr:`VGPRs (Vector General-Purpose Register)` lớn (có thể do có quá nhiều nhánh) vẫn có thể làm chậm đáng kể quá trình thực thi shader.

#elif
~~~~~

Chỉ thị ``#elif`` là viết tắt của "else if" và kiểm tra điều kiện được truyền vào nếu ``#if`` bên trên đánh giá thành ``false``. ``#elif`` chỉ có thể được sử dụng bên trong một khối ``#if``. Có thể sử dụng nhiều câu lệnh ``#elif`` sau một câu lệnh ``#if``.

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

Tương tự như ``#if``, có thể sử dụng hàm tiền xử lý ``defined()``:

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

Đây là cách viết tắt của ``#if defined(...)``. Kiểm tra xem mã định danh được truyền vào có được định nghĩa bởi ``#define`` đặt phía trên chỉ thị đó hay không. Điều này hữu ích khi tạo nhiều phiên bản shader trong cùng một tệp. Nó có thể được tiếp nối bằng một khối ``#else``, nhưng phải kết thúc bằng chỉ thị ``#endif``.

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
    #endif // Đây là phần kết thúc nhánh của `SHADOW_QUALITY_MEDIUM`.
    #endif // Đây là phần kết thúc nhánh của `SHADOW_QUALITY_HIGH`.

#ifndef
~~~~~~~

**Cú pháp:** ``#ifndef <identifier>``

Đây là cách viết tắt của ``#if !defined(...)``. Tương tự như ``#ifdef``, nhưng kiểm tra xem mã định danh được truyền vào có **không** được định nghĩa bởi ``#define`` trước chỉ thị đó hay không.

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

Định nghĩa khối tùy chọn được đưa vào khi chỉ thị ``#if``, ``#elif``, ``#ifdef`` hoặc ``#ifndef`` được định nghĩa trước đó đánh giá thành false.

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

Được dùng làm phần kết thúc cho các chỉ thị ``#if``, ``#ifdef``, ``#ifndef`` hoặc các chỉ thị ``#else`` tiếp theo.

#error
~~~~~~

**Cú pháp:** ``#error <message>``

Chỉ thị ``#error`` buộc bộ tiền xử lý phát ra lỗi kèm thông báo tùy chọn. Ví dụ, chỉ thị này hữu ích khi được sử dụng trong khối ``#if`` để áp đặt giới hạn nghiêm ngặt cho giá trị được định nghĩa.

.. code-block:: glsl

    #define MAX_LOD 3
    #define LOD 4

    #if LOD > MAX_LOD
    #error LOD exceeds MAX_LOD
    #endif

#include
~~~~~~~~

**Cú pháp:** ``#include "path"``

Chỉ thị ``#include`` đưa *toàn bộ* nội dung của tệp shader include vào một shader. ``"path"`` có thể là đường dẫn ``res://`` tuyệt đối hoặc tương đối so với tệp shader hiện tại. Đường dẫn tương đối chỉ được phép dùng trong các shader được lưu vào tệp ``.gdshader`` hoặc ``.gdshaderinc``, còn đường dẫn tuyệt đối có thể được dùng trong các shader được tích hợp vào tệp scene/resource.

Bạn có thể tạo shader include mới bằng tùy chọn menu **File > Create Shader Include** của trình chỉnh sửa shader, hoặc bằng cách tạo một resource :ref:`ShaderInclude<class_ShaderInclude>` mới trong dock FileSystem.

Shader include có thể được đưa vào từ bất kỳ shader nào hoặc shader include khác, tại bất kỳ vị trí nào trong tệp.

Khi đưa shader include vào phạm vi toàn cục của shader, bạn nên thực hiện việc này sau câu lệnh ``shader_type`` ban đầu.

Bạn cũng có thể đưa shader include vào bên trong phần thân của một hàm. Lưu ý rằng trình chỉnh sửa shader có thể sẽ báo lỗi đối với mã của shader include, vì mã đó có thể không hợp lệ bên ngoài ngữ cảnh mà nó được viết cho. Bạn có thể bỏ qua các lỗi này (shader vẫn sẽ biên dịch bình thường), hoặc bọc include trong một khối ``#ifdef`` để kiểm tra một define từ shader của bạn.

``#include`` hữu ích khi tạo các thư viện hàm trợ giúp (hoặc macro) và giảm việc lặp lại mã. Khi sử dụng ``#include``, hãy cẩn thận với việc trùng tên, vì không cho phép định nghĩa lại các hàm hoặc macro.

``#include`` có một số hạn chế:

- Chỉ có thể đưa vào các resource shader include (kết thúc bằng ``.gdshaderinc``). Không thể đưa các tệp ``.gdshader`` vào một shader khác, nhưng một tệp ``.gdshaderinc`` có thể đưa các tệp ``.gdshaderinc`` khác vào.
- Các dependency vòng **không được phép** và sẽ gây ra lỗi.
- Để tránh đệ quy vô hạn, độ sâu include được giới hạn ở 25 bước.

Tệp include shader mẫu:

.. code-block:: glsl

    // fancy_color.gdshaderinc

    // Mặc dù về mặt kỹ thuật được phép, các tệp include thường không có khai báo `shader_type`.

    vec3 get_fancy_color() {
        return vec3(0.3, 0.6, 0.9);
    }

Shader cơ sở mẫu (sử dụng tệp include chúng ta đã tạo ở trên):

.. code-block:: glsl

    // material.gdshader

    shader_type spatial;

    #include "res://fancy_color.gdshaderinc"

    void fragment() {
        // Không có lỗi vì chúng ta đã include định nghĩa cho `get_fancy_color()` thông qua shader include.
        COLOR = get_fancy_color();
    }

#pragma
~~~~~~~

**Cú pháp:** ``#pragma value``

Directive ``#pragma`` cung cấp thông tin bổ sung cho preprocessor hoặc compiler.

Hiện tại, directive này chỉ có thể có một giá trị: ``disable_preprocessor``. Nếu không cần preprocessor, hãy sử dụng directive đó để tăng tốc quá trình biên dịch shader bằng cách bỏ qua bước preprocessor.

.. code-block:: glsl

    #pragma disable_preprocessor

    #if USE_LIGHT
    // Điều này gây ra lỗi biên dịch shader vì `#if USE_LIGHT` và `#endif`
    // được đưa nguyên trạng vào mã shader cuối cùng.
    #endif

Các define tích hợp sẵn
-----------------------

Renderer hiện tại
~~~~~~~~~~~~~~~~~

Kể từ Godot 4.4, bạn có thể kiểm tra renderer hiện đang được sử dụng bằng các define tích hợp sẵn ``CURRENT_RENDERER``, ``RENDERER_COMPATIBILITY``, ``RENDERER_MOBILE`` và ``RENDERER_FORWARD_PLUS``:

- ``CURRENT_RENDERER`` được đặt thành ``0``, ``1`` hoặc ``2`` tùy thuộc vào renderer hiện tại.
- ``RENDERER_COMPATIBILITY`` luôn là ``0``.
- ``RENDERER_MOBILE`` luôn là ``1``.
- ``RENDERER_FORWARD_PLUS`` luôn là ``2``.

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
