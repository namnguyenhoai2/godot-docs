.. _doc_sky_shader:

Sky shader
==========

Sky shader là một loại shader đặc biệt được dùng để vẽ nền bầu trời và cập nhật các radiance cubemap được dùng cho image-based lighting (IBL). Sky shader chỉ có một hàm xử lý duy nhất, hàm ``sky()``.

Có ba nơi sky shader được sử dụng.

* Đầu tiên, sky shader được dùng để vẽ bầu trời khi bạn chọn sử dụng Sky làm nền trong scene. * Thứ hai, sky shader được dùng để cập nhật radiance cubemap khi sử dụng Sky cho màu môi trường hoặc hiệu ứng phản chiếu. * Thứ ba, sky shader được dùng để vẽ các subpass có độ phân giải thấp hơn, có thể được sử dụng trong background pass hoặc cubemap pass có độ phân giải cao.

Tổng cộng, điều này có nghĩa là sky shader có thể chạy tối đa sáu lần trong mỗi frame. Tuy nhiên, trên thực tế con số này sẽ ít hơn nhiều vì radiance cubemap không cần được cập nhật ở mỗi frame và không phải tất cả subpass đều được sử dụng. Bạn có thể thay đổi hành vi của shader dựa trên nơi nó được gọi bằng cách kiểm tra các giá trị boolean ``AT_*_PASS``. Ví dụ:

.. code-block:: glsl

    shader_type sky;

    void sky() {
        if (AT_CUBEMAP_PASS) {
            // Đặt radiance cubemap thành một sắc xanh lam đẹp mắt thay vì thực hiện
            // các phép tính bầu trời tốn kém
            COLOR = vec3(0.2, 0.6, 1.0);
        } else {
            // Thực hiện các phép tính bầu trời tốn kém chỉ cho bầu trời nền
            COLOR = get_sky_color(EYEDIR);
        }
    }


Khi sử dụng sky shader để vẽ nền, shader sẽ được gọi cho tất cả fragment không bị che khuất trên màn hình. Tuy nhiên, đối với các subpass của nền, shader sẽ được gọi cho từng pixel của subpass.

Khi sử dụng sky shader để cập nhật radiance cubemap, sky shader sẽ được gọi cho từng pixel trong cubemap. Mặt khác, shader chỉ được gọi khi radiance cubemap cần được cập nhật. Radiance cubemap cần được cập nhật khi bất kỳ tham số nào của shader được cập nhật. Ví dụ: nếu ``TIME`` được sử dụng trong shader, radiance cubemap sẽ được cập nhật ở mỗi frame. Danh sách thay đổi sau đây sẽ buộc radiance cubemap phải cập nhật:

* ``TIME`` được sử dụng. * ``POSITION`` được sử dụng và vị trí camera thay đổi. * Nếu bất kỳ thuộc tính ``LIGHTX_*`` nào được sử dụng và bất kỳ
  :ref:`DirectionalLight3D <class_DirectionalLight3D>` changes.
* uniform nào được thay đổi trong shader. * Nếu kích thước màn hình thay đổi và một trong hai subpass được sử dụng.

Hãy tránh cập nhật radiance cubemap một cách không cần thiết. Nếu bạn cần cập nhật radiance cubemap ở mỗi frame, hãy đảm bảo rằng
:ref:`Sky process mode <class_Sky_property_process_mode>` is set to
:ref:`PROCESS_MODE_REALTIME <class_Sky_constant_PROCESS_MODE_REALTIME>`.

Lưu ý rằng :ref:`process mode <class_Sky_property_process_mode>` chỉ ảnh hưởng đến việc render radiance cubemap. Bầu trời hiển thị luôn được render bằng cách gọi fragment shader cho từng pixel. Với các fragment shader phức tạp, điều này có thể gây ra overhead render lớn. Nếu bầu trời là tĩnh (các điều kiện được liệt kê ở trên được đáp ứng) hoặc thay đổi chậm, không cần chạy toàn bộ fragment shader ở mỗi frame. Có thể tránh điều này bằng cách render toàn bộ bầu trời vào radiance cubemap, rồi đọc từ cubemap này khi render bầu trời hiển thị. Với một bầu trời hoàn toàn tĩnh, điều này có nghĩa là bầu trời chỉ cần được render một lần.

Đoạn code sau render toàn bộ bầu trời vào radiance cubemap và đọc từ cubemap đó để hiển thị bầu trời nhìn thấy:

.. code-block:: glsl

    shader_type sky;

    void sky() {
        if (AT_CUBEMAP_PASS) {
            vec3 dir = EYEDIR;

            vec4 col = vec4(0.0);

            // Tính toán màu phức tạp

            COLOR = col.xyz;
            ALPHA = 1.0;
        } else {
            COLOR = texture(RADIANCE, EYEDIR).rgb;
        }
    }

Theo cách này, các phép tính phức tạp chỉ diễn ra trong cubemap pass, vốn có thể được tối ưu bằng cách đặt :ref:`process mode <class_Sky_property_process_mode>` và :ref:`radiance size <class_Sky_property_radiance_size>` của sky để đạt được sự cân bằng mong muốn giữa hiệu năng và độ trung thực hình ảnh.

Chế độ render
-------------

Subpass cho phép bạn thực hiện các phép tính tốn kém hơn ở độ phân giải thấp hơn để tăng tốc shader. Ví dụ: đoạn code sau render mây ở độ phân giải thấp hơn phần còn lại của bầu trời:

.. code-block:: glsl

    shader_type sky;
    render_mode use_half_res_pass;

    void sky() {
        if (AT_HALF_RES_PASS) {
            // Chạy phép tính mây cho 1/4 số pixel
            vec4 color = generate_clouds(EYEDIR);
            COLOR = color.rgb;
            ALPHA = color.a;
        } else {
            // Ở pass có độ phân giải đầy đủ, trộn bầu trời và mây với nhau
            vec3 color = generate_sky(EYEDIR);
            COLOR = color + HALF_RES_COLOR.rgb * HALF_RES_COLOR.a;
        }
    }

+--------------------------+-----------------------------------------------------------------------+
| Render mode              | Description                                                           |
+==========================+=======================================================================+
| **use_half_res_pass**    | Allows the shader to write to and access the half resolution pass.    |
+--------------------------+-----------------------------------------------------------------------+
| **use_quarter_res_pass** | Allows the shader to write to and access the quarter resolution pass. |
+--------------------------+-----------------------------------------------------------------------+
| **disable_fog**          | If used, fog will not affect the sky.                                 |
+--------------------------+-----------------------------------------------------------------------+

Built-in
--------

Các giá trị được đánh dấu là ``in`` chỉ được đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi vào tùy chọn và không nhất thiết chứa các giá trị hợp lý. Không thể ghi vào sampler nên chúng không được đánh dấu.

Global built-in
---------------

Global built-in khả dụng ở mọi nơi, bao gồm cả trong các hàm tùy chỉnh.

Có 4 ánh sáng ``LIGHTX``, được truy cập dưới dạng ``LIGHT0``, ``LIGHT1``, ``LIGHT2`` và ``LIGHT3``.


+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| Built-in                        | Description                                                                                                              |
+=================================+==========================================================================================================================+
| in float **TIME**               | Global time since the engine has started, in seconds. It repeats after every ``3,600``                                   |
|                                 | seconds (which can be changed with the                                                                                   |
|                                 | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>`                                 |
|                                 | setting). It's affected by :ref:`time_scale<class_Engine_property_time_scale>` but not by pausing. If you need a         |
|                                 | ``TIME`` variable that is not affected by time scale, add your own                                                       |
|                                 | :ref:`global shader uniform<doc_shading_language_global_uniforms>` and update it each                                    |
|                                 | frame.                                                                                                                   |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in vec3 **POSITION**            | Camera position, in world space.                                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| samplerCube **RADIANCE**        | Radiance cubemap. Can only be read from during the background pass. Check ``!AT_CUBEMAP_PASS`` before using.             |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in bool **AT_HALF_RES_PASS**    | ``true`` when rendering to the half resolution pass.                                                                     |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in bool **AT_QUARTER_RES_PASS** | ``true`` when rendering to the quarter resolution pass.                                                                  |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in bool **AT_CUBEMAP_PASS**     | ``true`` when rendering to the radiance cubemap.                                                                         |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in bool **LIGHTX_ENABLED**      | ``true`` if ``LIGHTX`` is visible and in the scene. If ``false``, other light properties may be garbage.                 |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in float **LIGHTX_ENERGY**      | Energy multiplier for ``LIGHTX``.                                                                                        |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in vec3 **LIGHTX_DIRECTION**    | Direction that ``LIGHTX`` is facing.                                                                                     |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in vec3 **LIGHTX_COLOR**        | Color of ``LIGHTX``.                                                                                                     |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in float **LIGHTX_SIZE**        | Angular diameter of ``LIGHTX`` in the sky. Expressed in radians. For reference, the sun from earth is about .0087 radians|
|                                 | (0.5 degrees).                                                                                                           |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in float **PI**                 | A ``PI`` constant (``3.141592``).                                                                                        |
|                                 | The ratio of a circle's circumference to its diameter and the number of radians in a half turn.                          |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in float **TAU**                | A ``TAU`` constant (``6.283185``).                                                                                       |
|                                 | Equivalent to ``PI * 2`` and the number of radians in a full turn.                                                       |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+
| in float **E**                  | An ``E`` constant (``2.718281``).                                                                                        |
|                                 | Euler's number, the base of the natural logarithm.                                                                       |
+---------------------------------+--------------------------------------------------------------------------------------------------------------------------+

Sky built-in
------------

+-------------------------------+-----------------------------------------------------------------------------------------------------+
| Built-in                      | Description                                                                                         |
+===============================+=====================================================================================================+
| in vec3 **EYEDIR**            | Normalized direction of the current pixel. Use this as your basic direction for procedural effects. |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| in vec2 **SCREEN_UV**         | Screen UV coordinate for the current pixel. Used to map a texture to the full screen.               |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| in vec2 **SKY_COORDS**        | Sphere UV. Used to map a panorama texture to the sky.                                               |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| in vec4 **HALF_RES_COLOR**    | Color value of the corresponding pixel from the half resolution pass. Uses linear filter.           |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| in vec4 **QUARTER_RES_COLOR** | Color value of the corresponding pixel from the quarter resolution pass. Uses linear filter.        |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| out vec3 **COLOR**            | Output color.                                                                                       |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| out float **ALPHA**           | Output alpha value, can only be used in subpasses.                                                  |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
| out vec4 **FOG**              |                                                                                                     |
+-------------------------------+-----------------------------------------------------------------------------------------------------+
