.. _doc_screen-reading_shaders:

Shader đọc màn hình
===================

Giới thiệu
----------

Thông thường, người ta muốn tạo một shader đọc từ chính màn hình mà nó đang ghi vào. Các API 3D như OpenGL hoặc DirectX khiến việc này trở nên rất khó khăn do những giới hạn phần cứng nội tại. GPU có tính song song cực cao, vì vậy việc đọc và ghi gây ra đủ loại vấn đề về cache và tính nhất quán. Do đó, ngay cả phần cứng hiện đại nhất cũng không hỗ trợ việc này một cách đúng đắn.

Cách xử lý là tạo một bản sao của màn hình, hoặc một phần màn hình, vào back-buffer rồi đọc từ đó trong khi vẽ. Godot cung cấp một số công cụ giúp quá trình này trở nên dễ dàng.

Screen texture
--------------

Godot :ref:`doc_shading_language` có một texture đặc biệt để truy cập nội dung màn hình đã được render. Bạn sử dụng nó bằng cách chỉ định một hint khi khai báo uniform ``sampler2D``: ``hint_screen_texture``. Có thể sử dụng varying dựng sẵn đặc biệt ``SCREEN_UV`` để lấy UV tương đối so với màn hình cho fragment hiện tại. Do đó, canvas_item fragment shader này tạo ra một đối tượng vô hình, vì nó chỉ hiển thị những gì nằm phía sau:

.. code-block:: glsl

    shader_type canvas_item;

    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    void fragment() {
        COLOR = textureLod(screen_texture, SCREEN_UV, 0.0);
    }

``textureLod`` được sử dụng ở đây vì chúng ta chỉ muốn đọc từ mipmap dưới cùng. Nếu muốn đọc từ một phiên bản làm mờ của texture, bạn có thể tăng đối số thứ ba lên ``textureLod`` và đổi hint ``filter_nearest`` thành ``filter_nearest_mipmap`` (hoặc bất kỳ filter nào khác có bật mipmap). Khi sử dụng filter có mipmap, Godot sẽ tự động tính toán texture đã làm mờ cho bạn.

.. warning::

    Nếu filter mode không được đổi thành một filter mode có chứa ``mipmap`` trong tên, ``textureLod`` với tham số LOD lớn hơn ``0.0`` sẽ có hình thức giống với tham số LOD ``0.0``.

Ví dụ về screen texture
-----------------------

Screen texture có thể được sử dụng cho nhiều mục đích. Có một bản demo đặc biệt về *Screen Space Shaders*, bạn có thể tải xuống để xem và học hỏi. Một ví dụ là shader đơn giản để điều chỉnh độ sáng, độ tương phản và độ bão hòa:

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

Mặc dù có vẻ kỳ diệu, nhưng thực ra không phải vậy. Trong 2D, khi ``hint_screen_texture`` được tìm thấy lần đầu tiên trong một node sắp được vẽ, Godot sẽ sao chép toàn màn hình vào back-buffer. Các node tiếp theo sử dụng nó trong shader sẽ không được sao chép màn hình riêng, vì việc này trở nên không hiệu quả. Trong 3D, màn hình được sao chép sau opaque geometry pass nhưng trước transparent geometry pass, vì vậy các đối tượng trong suốt sẽ không được ghi lại trong screen texture.

Do đó, trong 2D, nếu các shader sử dụng ``hint_screen_texture`` chồng lên nhau, shader thứ hai sẽ không sử dụng kết quả của shader thứ nhất, dẫn đến hình ảnh không như mong đợi:

.. image:: img/texscreen_demo1.png

Trong hình trên, hình cầu thứ hai (phía trên bên phải) đang sử dụng cùng nguồn screen texture với hình cầu thứ nhất ở bên dưới, vì vậy hình cầu thứ nhất "biến mất" hoặc không hiển thị.

Trong 2D, vấn đề này có thể được khắc phục thông qua node :ref:`BackBufferCopy <class_BackBufferCopy>`, được tạo instance giữa hai hình cầu. BackBufferCopy có thể hoạt động bằng cách chỉ định một vùng màn hình hoặc toàn bộ màn hình:

.. image:: img/texscreen_bbc.png

Khi sao chép back-buffer đúng cách, hai hình cầu sẽ hòa trộn chính xác:

.. image:: img/texscreen_demo2.png

.. warning::

    Trong 3D, các material sử dụng ``hint_screen_texture`` được xem là trong suốt và bản thân chúng sẽ không xuất hiện trong screen texture kết quả của các material khác. Nếu dự định tạo instance cho một scene sử dụng material có ``hint_screen_texture``, bạn sẽ cần sử dụng một node BackBufferCopy.

Trong 3D, có ít linh hoạt hơn để giải quyết vấn đề cụ thể này vì screen texture chỉ được ghi lại một lần. Hãy cẩn thận khi sử dụng screen texture trong 3D, vì nó sẽ không ghi lại các đối tượng trong suốt và có thể ghi lại một số đối tượng opaque nằm phía trước đối tượng sử dụng screen texture.

Bạn có thể mô phỏng logic back-buffer trong 3D bằng cách tạo một :ref:`Viewport <class_Viewport>` với camera ở cùng vị trí với đối tượng của bạn, rồi sử dụng
:ref:`Viewport's <class_Viewport>` texture instead of the screen texture.

Logic back-buffer
-----------------

Để làm rõ hơn, sau đây là cách logic sao chép backbuffer hoạt động trong 2D của Godot:

-  Nếu một node sử dụng ``hint_screen_texture``, toàn bộ màn hình sẽ được sao chép vào back buffer trước khi node đó được vẽ. Việc này chỉ xảy ra lần đầu; các node tiếp theo sẽ không kích hoạt nó. - Nếu một node BackBufferCopy đã được xử lý trước trường hợp nêu ở điểm trên (ngay cả khi không sử dụng ``hint_screen_texture``), hành vi được mô tả ở điểm trên sẽ không xảy ra. Nói cách khác, việc tự động sao chép toàn bộ màn hình chỉ xảy ra nếu ``hint_screen_texture`` được sử dụng lần đầu trong một node và trước đó không tìm thấy node BackBufferCopy nào (không bị vô hiệu hóa) theo thứ tự trong cây. - BackBufferCopy có thể sao chép toàn bộ màn hình hoặc một vùng. Nếu chỉ đặt sao chép một vùng (không phải toàn bộ màn hình) và shader của bạn sử dụng các pixel không nằm trong vùng được sao chép, kết quả của thao tác đọc đó là không xác định (nhiều khả năng là dữ liệu rác từ các frame trước). Nói cách khác, bạn có thể sử dụng BackBufferCopy để sao chép ngược một vùng của màn hình rồi đọc screen texture từ một vùng khác. Hãy tránh hành vi này!


Depth texture
-------------

Đối với shader 3D, bạn cũng có thể truy cập depth buffer của màn hình. Để làm việc này, sử dụng hint ``hint_depth_texture``. Texture này không tuyến tính; nó phải được chuyển đổi bằng inverse projection matrix.

Đoạn code sau lấy vị trí 3D bên dưới pixel đang được vẽ:

.. code-block:: glsl

    uniform sampler2D depth_texture : hint_depth_texture, repeat_disable, filter_nearest;

    void fragment() {
        float depth = textureLod(depth_texture, SCREEN_UV, 0.0).r;
        vec4 upos = INV_PROJECTION_MATRIX * vec4(SCREEN_UV * 2.0 - 1.0, depth, 1.0);
        vec3 pixel_position = upos.xyz / upos.w;
    }

Normal-roughness texture
------------------------

.. note::

    Normal-roughness texture chỉ được hỗ trợ trong phương thức render Forward+, không được hỗ trợ trong Mobile hoặc Compatibility.

Tương tự, normal-roughness texture có thể được sử dụng để đọc normal và roughness của các đối tượng được render trong depth prepass. Normal được lưu trong các channel ``.xyz`` (được ánh xạ vào phạm vi 0-1), còn roughness được lưu trong channel ``.w``.

.. code-block:: glsl

    uniform sampler2D normal_roughness_texture : hint_normal_roughness_texture, repeat_disable, filter_nearest;

    void fragment() {
        float screen_roughness = texture(normal_roughness_texture, SCREEN_UV).w;
        vec3 screen_normal = texture(normal_roughness_texture, SCREEN_UV).xyz;
        screen_normal = screen_normal * 2.0 - 1.0;

Định nghĩa lại screen texture
-----------------------------

Các hint của screen texture (``hint_screen_texture``, ``hint_depth_texture`` và ``hint_normal_roughness_texture``) có thể được sử dụng với nhiều uniform. Ví dụ, bạn có thể muốn đọc texture nhiều lần với cờ repeat hoặc cờ filter khác nhau.

Ví dụ sau đây cho thấy một shader đọc normal trong screen space bằng linear filtering, nhưng đọc roughness trong screen space bằng nearest neighbor filtering.

.. code-block:: glsl

    uniform sampler2D normal_roughness_texture : hint_normal_roughness_texture, repeat_disable, filter_nearest;
    uniform sampler2D normal_roughness_texture2 : hint_normal_roughness_texture, repeat_enable, filter_linear;

    void fragment() {
        float screen_roughness = texture(normal_roughness_texture, SCREEN_UV).w;
        vec3 screen_normal = texture(normal_roughness_texture2, SCREEN_UV).xyz;
        screen_normal = screen_normal * 2.0 - 1.0;
