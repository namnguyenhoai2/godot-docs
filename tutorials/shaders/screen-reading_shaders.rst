.. _doc_screen-reading_shaders:

Shader đọc màn hình
===================

Giới thiệu
----------

Thông thường, người ta muốn tạo một shader đọc từ chính màn hình mà nó đang ghi. Các API 3D như OpenGL hoặc DirectX khiến việc này trở nên rất khó khăn do những hạn chế của phần cứng bên trong. GPU có mức độ xử lý song song cực kỳ cao, nên việc đọc và ghi gây ra đủ loại vấn đề về cache và tính nhất quán. Vì vậy, ngay cả phần cứng hiện đại nhất cũng không hỗ trợ việc này đúng cách.

Giải pháp thay thế là sao chép toàn bộ hoặc một phần màn hình vào back-buffer, sau đó đọc từ đó trong khi vẽ. Godot cung cấp một số công cụ giúp quá trình này trở nên dễ dàng.

Texture màn hình
----------------

Godot :ref:`doc_shading_language` có một texture đặc biệt để truy cập nội dung màn hình đã được kết xuất. Texture này được sử dụng bằng cách chỉ định một hint khi khai báo uniform ``sampler2D``: ``hint_screen_texture``. Có thể sử dụng varying dựng sẵn đặc biệt ``SCREEN_UV`` để lấy UV tương ứng với màn hình của fragment hiện tại. Do đó, canvas_item fragment shader này tạo ra một đối tượng vô hình, vì nó chỉ hiển thị những gì nằm phía sau:

.. code-block:: glsl

    shader_type canvas_item;

    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    void fragment() {
        COLOR = textureLod(screen_texture, SCREEN_UV, 0.0);
    }

``textureLod`` được sử dụng ở đây vì chúng ta chỉ muốn đọc từ mipmap dưới cùng. Nếu muốn đọc một phiên bản đã làm mờ của texture, bạn có thể tăng đối số thứ ba của ``textureLod`` và thay đổi hint ``filter_nearest`` thành ``filter_nearest_mipmap`` (hoặc bất kỳ filter nào khác đã bật mipmap). Nếu sử dụng filter có mipmap, Godot sẽ tự động tính toán texture đã làm mờ cho bạn.

.. warning::

    Nếu chế độ filter không được thay đổi thành một chế độ filter có chứa ``mipmap`` trong tên, ``textureLod`` với tham số LOD lớn hơn ``0.0`` sẽ có hình thức giống với tham số LOD ``0.0``.

Ví dụ về texture màn hình
-------------------------

Texture màn hình có thể được sử dụng cho nhiều mục đích. Có một bản demo đặc biệt về *Shader không gian màn hình*, bạn có thể tải xuống để xem và tìm hiểu. Một ví dụ là shader đơn giản để điều chỉnh độ sáng, độ tương phản và độ bão hòa:

.. code-block:: glsl

    shader_type canvas_item;

    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    uniform float brightness = 1.0;
    uniform float contrast = 1.0;
    uniform float saturation = 1.0;

    void fragment() {
        vec3 c = textureLod(screen_texture, SCREEN_UV, 0.0).rgb;

        c.rgb = mix(vec3(0.0), c.rgb, brightness);
        c.rgb = mix(vec3(0.5), c.rgb, contrast);
        c.rgb = mix(vec3(dot(vec3(1.0), c.rgb) * 0.33333), c.rgb, saturation);

        COLOR.rgb = c;
    }

Cơ chế bên trong
----------------

Mặc dù có vẻ kỳ diệu, nhưng thực ra không phải vậy. Trong 2D, khi ``hint_screen_texture`` được phát hiện lần đầu trong một node sắp được vẽ, Godot sẽ sao chép toàn màn hình vào back-buffer. Các node tiếp theo sử dụng nó trong shader sẽ không được sao chép màn hình riêng, vì việc này kém hiệu quả. Trong 3D, màn hình được sao chép sau bước kết xuất hình học opaque nhưng trước bước kết xuất hình học transparent, vì vậy các đối tượng transparent sẽ không được thu vào texture màn hình.

Do đó, trong 2D, nếu các shader sử dụng ``hint_screen_texture`` chồng lên nhau, shader thứ hai sẽ không sử dụng kết quả của shader thứ nhất, dẫn đến hình ảnh không như mong đợi:

.. image:: img/texscreen_demo1.png

Trong hình ảnh trên, hình cầu thứ hai (phía trên bên phải) sử dụng cùng nguồn cho texture màn hình với hình cầu thứ nhất ở bên dưới, nên hình cầu thứ nhất "biến mất" hoặc không hiển thị.

Trong 2D, có thể khắc phục điều này bằng node :ref:`BackBufferCopy <class_BackBufferCopy>`, được khởi tạo giữa hai hình cầu. BackBufferCopy có thể hoạt động bằng cách chỉ định một vùng màn hình hoặc toàn bộ màn hình:

.. image:: img/texscreen_bbc.png

Khi sao chép back-buffer đúng cách, hai hình cầu sẽ hòa trộn chính xác:

.. image:: img/texscreen_demo2.png

.. warning::

    Trong 3D, các material sử dụng ``hint_screen_texture`` được xem là transparent và bản thân chúng sẽ không xuất hiện trong texture màn hình kết quả của các material khác. Nếu dự định khởi tạo một scene sử dụng material có ``hint_screen_texture``, bạn sẽ cần sử dụng một node BackBufferCopy.

Trong 3D, có ít khả năng linh hoạt hơn để giải quyết vấn đề cụ thể này vì texture màn hình chỉ được thu một lần. Hãy cẩn thận khi sử dụng texture màn hình trong 3D, vì nó sẽ không thu các đối tượng transparent và có thể thu một số đối tượng opaque nằm phía trước đối tượng sử dụng texture màn hình.

Bạn có thể tái tạo logic back-buffer trong 3D bằng cách tạo một :ref:`Viewport <class_Viewport>` với camera ở cùng vị trí với đối tượng, sau đó sử dụng
texture của :ref:`Viewport <class_Viewport>` thay cho texture màn hình.

Logic back-buffer
-----------------

Để rõ ràng hơn, sau đây là cách logic sao chép back-buffer hoạt động trong 2D ở Godot:

-  Nếu một node sử dụng ``hint_screen_texture``, toàn bộ màn hình sẽ được sao chép vào back buffer trước khi node đó được vẽ. Việc này chỉ xảy ra lần đầu; các node tiếp theo sẽ không kích hoạt nó.
-  Nếu một node BackBufferCopy đã được xử lý trước tình huống nêu ở mục trên (ngay cả khi ``hint_screen_texture`` không được sử dụng), hành vi được mô tả ở mục trên sẽ không xảy ra. Nói cách khác, việc tự động sao chép toàn bộ màn hình chỉ xảy ra nếu ``hint_screen_texture`` được sử dụng lần đầu trong một node và trước đó không tìm thấy node BackBufferCopy nào (không bị vô hiệu hóa) theo thứ tự trong cây.
-  BackBufferCopy có thể sao chép toàn bộ màn hình hoặc một vùng. Nếu chỉ đặt sao chép một vùng (không phải toàn bộ màn hình) và shader của bạn sử dụng các pixel không nằm trong vùng được sao chép, kết quả của lần đọc đó là không xác định (nhiều khả năng là dữ liệu rác từ các frame trước). Nói cách khác, có thể sử dụng BackBufferCopy để sao chép một vùng của màn hình, sau đó đọc texture màn hình từ một vùng khác. Hãy tránh hành vi này!


Texture độ sâu
--------------

Đối với shader 3D, bạn cũng có thể truy cập depth buffer của màn hình. Để làm việc này, sử dụng hint ``hint_depth_texture``. Texture này không tuyến tính; cần chuyển đổi nó bằng inverse projection matrix.

Đoạn mã sau lấy vị trí 3D bên dưới pixel đang được vẽ:

.. code-block:: glsl

    uniform sampler2D depth_texture : hint_depth_texture, repeat_disable, filter_nearest;

    void fragment() {
        float depth = textureLod(depth_texture, SCREEN_UV, 0.0).r;
        vec4 upos = INV_PROJECTION_MATRIX * vec4(SCREEN_UV * 2.0 - 1.0, depth, 1.0);
        vec3 pixel_position = upos.xyz / upos.w;
    }

Texture normal-roughness
------------------------

.. note::

    Texture normal-roughness chỉ được hỗ trợ trong phương thức kết xuất Forward+, không được hỗ trợ trong Mobile hoặc Compatibility.

Tương tự, texture normal-roughness có thể được sử dụng để đọc normal và roughness của các đối tượng được kết xuất trong depth prepass. Normal được lưu trong các kênh ``.xyz`` (ánh xạ vào phạm vi 0-1), còn roughness được lưu trong kênh ``.w``.

.. code-block:: glsl

    uniform sampler2D normal_roughness_texture : hint_normal_roughness_texture, repeat_disable, filter_nearest;

    void fragment() {
        float screen_roughness = texture(normal_roughness_texture, SCREEN_UV).w;
        vec3 screen_normal = texture(normal_roughness_texture, SCREEN_UV).xyz;
        screen_normal = screen_normal * 2.0 - 1.0;

Định nghĩa lại texture màn hình
-------------------------------

Các hint texture màn hình (``hint_screen_texture``, ``hint_depth_texture`` và ``hint_normal_roughness_texture``) có thể được sử dụng với nhiều uniform. Ví dụ, bạn có thể muốn đọc texture nhiều lần với cờ repeat hoặc cờ filter khác nhau.

Ví dụ sau đây cho thấy một shader đọc normal trong không gian màn hình bằng linear filtering, nhưng đọc roughness trong không gian màn hình bằng nearest neighbor filtering.

.. code-block:: glsl

    uniform sampler2D normal_roughness_texture : hint_normal_roughness_texture, repeat_disable, filter_nearest;
    uniform sampler2D normal_roughness_texture2 : hint_normal_roughness_texture, repeat_enable, filter_linear;

    void fragment() {
        float screen_roughness = texture(normal_roughness_texture, SCREEN_UV).w;
        vec3 screen_normal = texture(normal_roughness_texture2, SCREEN_UV).xyz;
        screen_normal = screen_normal * 2.0 - 1.0;
