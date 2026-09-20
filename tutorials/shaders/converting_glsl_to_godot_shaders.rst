.. _doc_converting_glsl_to_godot_shaders:

Chuyển đổi GLSL sang shader Godot
=================================

Tài liệu này giải thích những khác biệt giữa ngôn ngữ shading của Godot và GLSL, đồng thời đưa ra lời khuyên thực tế về cách chuyển các shader từ những nguồn khác, chẳng hạn như Shadertoy và The Book of Shaders, sang shader Godot.

Để biết thông tin chi tiết về ngôn ngữ shading của Godot, vui lòng tham khảo
:ref:`Shading Language <doc_shading_language>` reference.

GLSL
----

Godot sử dụng một ngôn ngữ shading dựa trên GLSL, với một vài tính năng cải thiện chất lượng sử dụng được bổ sung. Do đó, hầu hết các tính năng có trong GLSL đều có trong ngôn ngữ shading của Godot.

Các chương trình shader
~~~~~~~~~~~~~~~~~~~~~~~

Trong GLSL, mỗi shader sử dụng một chương trình riêng. Bạn có một chương trình cho vertex shader và một chương trình cho fragment shader. Trong Godot, bạn có một shader duy nhất chứa hàm ``vertex`` và/hoặc ``fragment``. Nếu bạn chỉ chọn viết một hàm, Godot sẽ cung cấp hàm còn lại.

Godot cho phép chia sẻ các biến uniform và hàm bằng cách định nghĩa fragment shader và vertex shader trong cùng một tệp. Trong GLSL, các chương trình vertex và fragment không thể chia sẻ biến, trừ khi sử dụng varying.

Các thuộc tính vertex
~~~~~~~~~~~~~~~~~~~~~

Trong GLSL, bạn có thể truyền thông tin theo từng vertex bằng các thuộc tính và linh hoạt truyền vào nhiều hoặc ít dữ liệu tùy ý. Trong Godot, bạn có một số lượng thuộc tính đầu vào cố định, bao gồm ``VERTEX`` (vị trí), ``COLOR``, ``UV``, ``UV2``, ``NORMAL``. Trang của mỗi shader trong phần tham chiếu shader của tài liệu đều có danh sách đầy đủ các thuộc tính vertex của shader đó.

gl_Position
~~~~~~~~~~~

``gl_Position`` nhận vị trí cuối cùng của một vertex được chỉ định trong vertex shader. Vị trí này do người dùng chỉ định trong clip space. Thông thường, trong GLSL, vị trí vertex trong model space được truyền vào bằng một thuộc tính vertex có tên ``position``, và bạn phải tự xử lý việc chuyển đổi từ model space sang clip space.

Trong Godot, ``VERTEX`` chỉ định vị trí vertex trong model space ở đầu hàm ``vertex``. Godot cũng xử lý việc chuyển đổi cuối cùng sang clip space sau khi hàm ``vertex`` do người dùng định nghĩa được chạy. Nếu muốn bỏ qua việc chuyển đổi từ model space sang view space, bạn có thể đặt ``render_mode`` thành ``skip_vertex_transform``. Nếu muốn bỏ qua mọi phép biến đổi, hãy đặt ``render_mode`` thành ``skip_vertex_transform`` và đặt ``PROJECTION_MATRIX`` thành ``mat4(1.0)`` để vô hiệu hóa phép biến đổi cuối cùng từ view space sang clip space.

Varying
~~~~~~~

Varying là một loại biến có thể được truyền từ vertex shader sang fragment shader. Trong GLSL hiện đại (3.0 trở lên), varying được định nghĩa bằng các từ khóa ``in`` và ``out``. Một biến truyền ra từ vertex shader được định nghĩa bằng ``out`` trong vertex shader và ``in`` bên trong fragment shader.

Main
~~~~

Trong GLSL, mỗi chương trình shader trông giống như một chương trình kiểu C độc lập. Vì vậy, điểm vào chính là ``main``. Nếu bạn sao chép một vertex shader, hãy đổi tên ``main`` thành ``vertex``; còn nếu bạn sao chép một fragment shader, hãy đổi tên ``main`` thành ``fragment``.

Macro
~~~~~

:ref:`Godot shader preprocessor<doc_shader_preprocessor>` hỗ trợ các macro sau:

* ``#define`` / ``#undef`` * ``#if``, ``#elif``, ``#else``, ``#endif``, ``defined()``, ``#ifdef``, ``#ifndef`` * ``#include`` (chỉ với các tệp ``.gdshaderinc`` và độ sâu tối đa là 25) * ``#pragma disable_preprocessor``, vô hiệu hóa tiền xử lý cho phần còn lại của tệp

Biến
~~~~

GLSL có nhiều biến dựng sẵn được hard-code. Những biến này không phải là uniform, vì vậy không thể chỉnh sửa chúng từ chương trình chính.

+---------------------+---------+------------------------+-----------------------------------------------------+
|Variable             |Type     |Equivalent              |Description                                          |
+=====================+=========+========================+=====================================================+
|gl_FragColor         |out vec4 |COLOR                   |Output color for each pixel.                         |
+---------------------+---------+------------------------+-----------------------------------------------------+
|gl_FragCoord         |vec4     |FRAGCOORD               |For full screen quads. For smaller quads, use UV.    |
+---------------------+---------+------------------------+-----------------------------------------------------+
|gl_Position          |vec4     |VERTEX                  |Position of Vertex, output from Vertex Shader.       |
+---------------------+---------+------------------------+-----------------------------------------------------+
|gl_PointSize         |float    |POINT_SIZE              |Size of Point primitive.                             |
+---------------------+---------+------------------------+-----------------------------------------------------+
|gl_PointCoord        |vec2     |POINT_COORD             |Position on point when drawing Point primitives.     |
+---------------------+---------+------------------------+-----------------------------------------------------+
|gl_FrontFacing       |bool     |FRONT_FACING            |True if front face of primitive.                     |
+---------------------+---------+------------------------+-----------------------------------------------------+

.. _glsl_coordinates:

Tọa độ
~~~~~~

``gl_FragCoord`` trong GLSL và ``FRAGCOORD`` trong ngôn ngữ shading của Godot sử dụng cùng một hệ tọa độ. Nếu sử dụng UV trong Godot, tọa độ y sẽ bị lật ngược.

Độ chính xác
~~~~~~~~~~~~

Trong GLSL, bạn có thể định nghĩa độ chính xác của một kiểu dữ liệu nhất định (float hoặc int) ở đầu shader bằng từ khóa ``precision``. Trong Godot, bạn có thể đặt độ chính xác cho từng biến tùy theo nhu cầu bằng cách đặt các qualifier độ chính xác ``lowp``, ``mediump`` và ``highp`` trước kiểu dữ liệu khi định nghĩa biến. Để biết thêm thông tin, hãy xem tài liệu tham chiếu :ref:`Shading Language <doc_shading_language>`.

Shadertoy
---------

`Shadertoy <https://www.shadertoy.com/results?query=&sort=popular&from=10&num=4>`_ là một website giúp dễ dàng viết fragment shader và tạo `pure magic <https://www.shadertoy.com/view/4tjGRh>`_.

Shadertoy không cung cấp cho người dùng toàn quyền kiểm soát shader. Nó xử lý tất cả đầu vào và uniform, đồng thời chỉ cho phép người dùng viết fragment shader.

Kiểu dữ liệu
~~~~~~~~~~~~

Shadertoy sử dụng đặc tả webgl, nên chạy một phiên bản GLSL hơi khác. Tuy nhiên, nó vẫn có các kiểu dữ liệu thông thường, bao gồm hằng số và macro.

mainImage
~~~~~~~~~

Điểm vào chính của shader Shadertoy là hàm ``mainImage``. ``mainImage`` có hai tham số, ``fragColor`` và ``fragCoord``, lần lượt tương ứng với ``COLOR`` và ``FRAGCOORD`` trong Godot. Các tham số này được Godot tự động xử lý, vì vậy bạn không cần tự thêm chúng làm tham số. Mọi nội dung trong hàm ``mainImage`` cần được sao chép vào hàm ``fragment`` khi chuyển sang Godot.

Biến
~~~~

Để việc viết fragment shader trở nên đơn giản và dễ dàng, Shadertoy tự xử lý việc truyền nhiều thông tin hữu ích từ chương trình chính vào fragment shader. Một số thông tin trong đó không có tương đương trong Godot vì Godot đã chọn không cung cấp chúng theo mặc định. Điều này không sao, vì Godot cho phép bạn tự tạo uniform. Đối với những biến có phần tương đương được liệt kê là "Provide with Uniform", người dùng chịu trách nhiệm tự tạo uniform đó. Phần mô tả sẽ gợi ý cho người đọc về dữ liệu có thể truyền vào để thay thế.

+---------------------+---------+------------------------+-----------------------------------------------------+
|Variable             |Type     |Equivalent              |Description                                          |
+=====================+=========+========================+=====================================================+
|fragColor            |out vec4 |COLOR                   |Output color for each pixel.                         |
+---------------------+---------+------------------------+-----------------------------------------------------+
|fragCoord            |vec2     |FRAGCOORD.xy            |For full screen quads. For smaller quads, use UV.    |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iResolution          |vec3     |1.0 / SCREEN_PIXEL_SIZE |Can also pass in manually.                           |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iTime                |float    |TIME                    |Time since shader started.                           |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iTimeDelta           |float    |Provide with Uniform    |Time to render previous frame.                       |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iFrame               |float    |Provide with Uniform    |Frame number.                                        |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iChannelTime[4]      |float    |Provide with Uniform    |Time since that particular texture started.          |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iMouse               |vec4     |Provide with Uniform    |Mouse position in pixel coordinates.                 |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iDate                |vec4     |Provide with Uniform    |Current date, expressed in seconds.                  |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iChannelResolution[4]|vec3     |1.0 / TEXTURE_PIXEL_SIZE|Resolution of particular texture.                    |
+---------------------+---------+------------------------+-----------------------------------------------------+
|iChanneli            |Sampler2D|TEXTURE                 |Godot provides only one built-in; user can make more.|
+---------------------+---------+------------------------+-----------------------------------------------------+

Tọa độ
~~~~~~

``fragCoord`` hoạt động giống ``gl_FragCoord`` trong :ref:`GLSL <glsl_coordinates>` và ``FRAGCOORD`` trong Godot.


The Book of Shaders
-------------------

Tương tự như Shadertoy, `The Book of Shaders <https://thebookofshaders.com>`_ cung cấp quyền truy cập vào một fragment shader trong trình duyệt web để người dùng có thể tương tác. Người dùng chỉ được viết mã fragment shader với một danh sách uniform được truyền vào cố định và không thể thêm uniform bổ sung.

Để được trợ giúp thêm về việc chuyển shader sang các framework nói chung, The Book of Shaders cung cấp một `page <https://thebookofshaders.com/04>`_ về cách chạy shader trong nhiều framework khác nhau.

Kiểu dữ liệu
~~~~~~~~~~~~

The Book of Shaders sử dụng đặc tả webgl, nên chạy một phiên bản GLSL hơi khác. Tuy nhiên, nó vẫn có các kiểu dữ liệu thông thường, bao gồm hằng số và macro.

Main
~~~~

Điểm vào của fragment shader trong The Book of Shaders là ``main``, giống như trong GLSL. Mọi nội dung được viết trong hàm ``main`` của The Book of Shaders cần được sao chép vào hàm ``fragment`` của Godot.

Biến
~~~~

The Book of Shaders gần với GLSL thuần túy hơn Shadertoy. Nó cũng triển khai ít uniform hơn Shadertoy.

+---------------------+---------+------------------------+-----------------------------------------------------+
|Variable             |Type     |Equivalent              |Description                                          |
+=====================+=========+========================+=====================================================+
|gl_FragColor         |out vec4 |COLOR                   |Output color for each pixel.                         |
+---------------------+---------+------------------------+-----------------------------------------------------+
|gl_FragCoord         |vec4     |FRAGCOORD               |For full screen quads. For smaller quads, use UV.    |
+---------------------+---------+------------------------+-----------------------------------------------------+
|u_resolution         |vec2     |1.0 / SCREEN_PIXEL_SIZE |Can also pass in manually.                           |
+---------------------+---------+------------------------+-----------------------------------------------------+
|u_time               |float    |TIME                    |Time since shader started.                           |
+---------------------+---------+------------------------+-----------------------------------------------------+
|u_mouse              |vec2     |Provide with Uniform    |Mouse position in pixel coordinates.                 |
+---------------------+---------+------------------------+-----------------------------------------------------+

Tọa độ
~~~~~~

The Book of Shaders sử dụng cùng hệ tọa độ với
:ref:`GLSL <glsl_coordinates>`.
