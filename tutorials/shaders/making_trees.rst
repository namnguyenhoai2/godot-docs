.. _doc_making_trees:

Tạo cây
=======

Đây là hướng dẫn ngắn về cách tự tạo cây và các loại thảm thực vật khác từ đầu.

Mục tiêu không phải tập trung vào các kỹ thuật dựng hình (có rất nhiều hướng dẫn về chủ đề này), mà là cách làm cho chúng trông đẹp trong Godot.

.. image:: img/tree_sway.gif

Bắt đầu với một cái cây
-----------------------

Tôi lấy cái cây này từ SketchFab:

.. image:: img/tree_base.png

https://sketchfab.com/models/ea5e6ed7f9d6445ba69589d503e8cebf

và mở nó trong Blender.

Tô bằng vertex color
--------------------

Điều đầu tiên bạn có thể muốn làm là dùng vertex color để tô mức độ cây sẽ đung đưa khi có gió. Chỉ cần sử dụng công cụ tô vertex color trong chương trình dựng hình 3D yêu thích của bạn và tô tương tự như sau:

.. image:: img/tree_vertex_paint.png

Điều này hơi cường điệu, nhưng ý tưởng là màu sắc biểu thị mức độ gió ảnh hưởng đến từng phần của cây. Thang đo này thể hiện điều đó rõ hơn:

.. image:: img/tree_gradient.png

Viết custom shader cho lá
-------------------------

Đây là một ví dụ về shader cho lá:

.. code-block:: glsl

    shader_type spatial;
    render_mode depth_prepass_alpha, cull_disabled, world_vertex_coords;

Đây là một spatial shader. Không có front/back culling (vì vậy có thể nhìn thấy lá từ cả hai phía), và alpha prepass được sử dụng, nhờ đó có ít artifact về độ sâu hơn do dùng transparency (đồng thời lá có thể đổ bóng). Cuối cùng, đối với hiệu ứng đung đưa, nên dùng tọa độ world, để cây có thể được nhân bản, di chuyển, v.v. mà vẫn hoạt động đồng bộ với các cây khác.

.. code-block:: glsl

    uniform sampler2D texture_albedo : source_color;
    uniform vec4 transmission : source_color;

Ở đây, texture được đọc cùng với một transmission color, dùng để thêm hiệu ứng chiếu sáng từ phía sau cho lá, mô phỏng subsurface scattering.


.. code-block:: glsl

    uniform float sway_speed = 1.0;
    uniform float sway_strength = 0.05;
    uniform float sway_phase_len = 8.0;

    void vertex() {
        float strength = COLOR.r * sway_strength;
        VERTEX.x += sin(VERTEX.x * sway_phase_len * 1.123 + TIME * sway_speed) * strength;
        VERTEX.y += sin(VERTEX.y * sway_phase_len + TIME * sway_speed * 1.12412) * strength;
        VERTEX.z += sin(VERTEX.z * sway_phase_len * 0.9123 + TIME * sway_speed * 1.3123) * strength;
    }

Đây là code tạo hiệu ứng đung đưa của lá. Nó khá cơ bản (chỉ dùng một sóng sine nhân với thời gian và vị trí trên trục, nhưng hoạt động tốt). Lưu ý rằng strength được nhân với color. Mỗi trục sử dụng một hệ số nhân nhỏ khác nhau, gần 1.0, để các trục không xuất hiện đồng bộ.


Cuối cùng, tất cả những gì còn lại là fragment shader:

.. code-block:: glsl

    void fragment() {
        vec4 albedo_tex = texture(texture_albedo, UV);
        ALBEDO = albedo_tex.rgb;
        ALPHA = albedo_tex.a;
        METALLIC = 0.0;
        ROUGHNESS = 1.0;
        SSS_TRANSMITTANCE_COLOR = transmission.rgba;
    }

Và về cơ bản là xong.

Shader cho thân cây cũng tương tự, ngoại trừ việc nó không ghi vào kênh alpha (do đó không cần alpha prepass) và không cần transmission để hoạt động. Cả hai shader đều có thể được cải thiện bằng cách thêm normal mapping, AO và các map khác.

Cải thiện shader
----------------

Bạn có thể đọc thêm nhiều tài liệu về cách thực hiện việc này. Giờ bạn đã biết những điều cơ bản, nên đọc chương trong GPU Gems3 về cách Crysis thực hiện việc này (chủ yếu tập trung vào code tạo hiệu ứng đung đưa, vì nhiều kỹ thuật khác được trình bày ở đó đã lỗi thời):

https://developer.nvidia.com/gpugems/GPUGems3/gpugems3_ch16.html
