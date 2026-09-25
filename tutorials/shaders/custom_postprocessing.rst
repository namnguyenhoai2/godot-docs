.. _doc_custom_postprocessing:

Hậu xử lý tùy chỉnh
===================

Giới thiệu
----------

Godot cung cấp sẵn nhiều hiệu ứng hậu xử lý, bao gồm Bloom, DOF và SSAO, được mô tả trong :ref:`doc_environment_and_post_processing`. Tuy nhiên, một số trường hợp sử dụng nâng cao có thể yêu cầu các hiệu ứng tùy chỉnh. Bài viết này giải thích cách tự viết các hiệu ứng tùy chỉnh.

Cách dễ nhất để triển khai shader hậu xử lý tùy chỉnh là sử dụng khả năng tích hợp sẵn của Godot để đọc từ screen texture. Nếu bạn chưa quen với việc này, trước tiên bạn nên đọc
:ref:`Hướng dẫn về Screen Reading Shaders <doc_screen-reading_shaders>`.

Hậu xử lý một lượt
------------------

Hiệu ứng hậu xử lý là các shader được áp dụng cho một khung hình sau khi Godot kết xuất khung hình đó. Để áp dụng shader cho một khung hình, hãy tạo một :ref:`CanvasLayer <class_CanvasLayer>`, rồi cung cấp cho nó một :ref:`ColorRect <class_ColorRect>`. Gán một :ref:`ShaderMaterial <class_ShaderMaterial>` mới cho ``ColorRect`` vừa tạo, rồi đặt anchor preset của ``ColorRect`` thành Full Rect:

.. figure:: img/custom_postprocessing_anchors_preset_full_rect.webp
   :align: center
   :alt: Đặt anchor preset thành Full Rect trên node ColorRect

   Đặt anchor preset thành Full Rect trên node ColorRect

Cây scene của bạn sẽ có dạng tương tự như sau:

.. image:: img/post_tree1.png

.. note::

   Một phương pháp khác hiệu quả hơn là sử dụng :ref:`BackBufferCopy <class_BackBufferCopy>` để sao chép một vùng trên màn hình vào buffer và truy cập vùng đó trong shader script thông qua ``sampler2D`` bằng ``hint_screen_texture``.

.. note::

    Tại thời điểm viết bài, Godot chưa hỗ trợ kết xuất đồng thời vào nhiều buffer. Shader hậu xử lý của bạn sẽ không thể truy cập các render pass và buffer khác không được Godot cung cấp (chẳng hạn như depth hoặc normal/roughness). Bạn chỉ có thể truy cập khung hình đã kết xuất và các buffer được Godot cung cấp dưới dạng sampler.

Trong ví dụ này, chúng ta sẽ sử dụng :ref:`Sprite <class_Sprite2D>` này của một con cừu.

.. image:: img/post_example1.png

Gán một :ref:`Shader <class_Shader>` mới cho ``ColorRect``'s ``ShaderMaterial``. Bạn có thể truy cập texture và UV của khung hình bằng ``sampler2D`` sử dụng ``hint_screen_texture`` và các uniform tích hợp sẵn ``SCREEN_UV``.

Sao chép đoạn mã sau vào shader của bạn. Đoạn mã dưới đây là shader pixelization dạng hex do `arlez80 <https://bitbucket.org/arlez80/hex-mosaic/src/master/>`_ viết,

.. code-block:: glsl

    shader_type canvas_item;

    uniform vec2 size = vec2(32.0, 28.0);
    // Nếu bạn định đọc từ mipmap với các giá trị LOD của `textureLod()` lớn hơn `0.0`,
    // hãy dùng `filter_nearest_mipmap` thay thế. Shader này không yêu cầu nó.
    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    void fragment() {
            vec2 norm_size = size * SCREEN_PIXEL_SIZE;
            bool less_than_half = mod(SCREEN_UV.y / 2.0, norm_size.y) / norm_size.y < 0.5;
            vec2 uv = SCREEN_UV + vec2(norm_size.x * 0.5 * float(less_than_half), 0.0);
            vec2 center_uv = floor(uv / norm_size) * norm_size;
            vec2 norm_uv = mod(uv, norm_size) / norm_size;
            center_uv += mix(vec2(0.0, 0.0),
                             mix(mix(vec2(norm_size.x, -norm_size.y),
                                     vec2(0.0, -norm_size.y),
                                     float(norm_uv.x < 0.5)),
                                 mix(vec2(0.0, -norm_size.y),
                                     vec2(-norm_size.x, -norm_size.y),
                                     float(norm_uv.x < 0.5)),
                                 float(less_than_half)),
                             float(norm_uv.y < 0.3333333) * float(norm_uv.y / 0.3333333 < (abs(norm_uv.x - 0.5) * 2.0)));

            COLOR = textureLod(screen_texture, center_uv, 0.0);
    }

Con cừu sẽ có dạng tương tự như sau:

.. image:: img/post_example2.png

Hậu xử lý nhiều lượt
--------------------

Một số hiệu ứng hậu xử lý như làm mờ tiêu tốn nhiều tài nguyên. Bạn có thể làm cho chúng chạy nhanh hơn đáng kể nếu chia chúng thành nhiều lượt. Trong material multipass, mỗi lượt lấy kết quả từ lượt trước làm đầu vào rồi xử lý kết quả đó.

Để tạo shader hậu xử lý nhiều lượt, bạn xếp chồng các node ``CanvasLayer`` và ``ColorRect``. Trong ví dụ trên, bạn sử dụng một đối tượng ``CanvasLayer`` để kết xuất shader bằng khung hình trên layer bên dưới. Ngoài cấu trúc node, các bước thực hiện cũng giống như với shader hậu xử lý một lượt.

Cây scene của bạn sẽ có dạng tương tự như sau:

.. image:: img/post_tree2.png

Ví dụ, bạn có thể viết hiệu ứng làm mờ Gaussian toàn màn hình bằng cách gắn các đoạn mã sau vào từng node ``ColorRect``. Thứ tự áp dụng shader phụ thuộc vào vị trí của ``CanvasLayer`` trong cây scene; vị trí cao hơn nghĩa là được áp dụng sớm hơn. Với shader làm mờ này, thứ tự không quan trọng.

.. code-block:: glsl

    shader_type canvas_item;

    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    // Làm mờ màn hình theo hướng X.
    void fragment() {
        vec3 col = texture(screen_texture, SCREEN_UV).xyz * 0.16;
        col += texture(screen_texture, SCREEN_UV + vec2(SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.15;
        col += texture(screen_texture, SCREEN_UV + vec2(-SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.15;
        col += texture(screen_texture, SCREEN_UV + vec2(2.0 * SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.12;
        col += texture(screen_texture, SCREEN_UV + vec2(2.0 * -SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.12;
        col += texture(screen_texture, SCREEN_UV + vec2(3.0 * SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.09;
        col += texture(screen_texture, SCREEN_UV + vec2(3.0 * -SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.09;
        col += texture(screen_texture, SCREEN_UV + vec2(4.0 * SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.05;
        col += texture(screen_texture, SCREEN_UV + vec2(4.0 * -SCREEN_PIXEL_SIZE.x, 0.0)).xyz * 0.05;
        COLOR.xyz = col;
    }

.. code-block:: glsl

    shader_type canvas_item;

    uniform sampler2D screen_texture : hint_screen_texture, repeat_disable, filter_nearest;

    // Làm mờ màn hình theo hướng Y.
    void fragment() {
        vec3 col = texture(screen_texture, SCREEN_UV).xyz * 0.16;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, SCREEN_PIXEL_SIZE.y)).xyz * 0.15;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, -SCREEN_PIXEL_SIZE.y)).xyz * 0.15;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, 2.0 * SCREEN_PIXEL_SIZE.y)).xyz * 0.12;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, 2.0 * -SCREEN_PIXEL_SIZE.y)).xyz * 0.12;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, 3.0 * SCREEN_PIXEL_SIZE.y)).xyz * 0.09;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, 3.0 * -SCREEN_PIXEL_SIZE.y)).xyz * 0.09;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, 4.0 * SCREEN_PIXEL_SIZE.y)).xyz * 0.05;
        col += texture(screen_texture, SCREEN_UV + vec2(0.0, 4.0 * -SCREEN_PIXEL_SIZE.y)).xyz * 0.05;
        COLOR.xyz = col;
    }

Với đoạn mã trên, bạn sẽ có hiệu ứng làm mờ toàn màn hình như bên dưới.

.. image:: img/post_example3.png

.. _`arlez80`: https://bitbucket.org/arlez80/hex-mosaic/src/master/
