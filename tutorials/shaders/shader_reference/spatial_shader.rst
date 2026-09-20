.. _doc_spatial_shader:

Shader không gian
=================

Shader không gian được dùng để đổ bóng cho các đối tượng 3D. Đây là loại shader phức tạp nhất mà Godot cung cấp. Shader không gian có khả năng cấu hình cao với nhiều chế độ kết xuất và tùy chọn kết xuất khác nhau (ví dụ: Subsurface Scattering, Transmission, Ambient Occlusion, Rim lighting, v.v.). Người dùng có thể tùy chọn viết các hàm xử lý vertex, fragment và light để tác động đến cách các đối tượng được vẽ.

Chế độ kết xuất
---------------

Để xem các ví dụ trực quan về những chế độ kết xuất này, hãy xem :ref:`Standard Material 3D and ORM Material 3D<doc_standard_material_3d>`.

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Render mode                   | Description                                                                                          |
+===============================+======================================================================================================+
| **blend_mix**                 | Mix blend mode (alpha is transparency), default.                                                     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **blend_add**                 | Additive blend mode.                                                                                 |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **blend_sub**                 | Subtractive blend mode.                                                                              |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **blend_mul**                 | Multiplicative blend mode.                                                                           |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **blend_premul_alpha**        | Premultiplied alpha blend mode (fully transparent = add, fully opaque = mix).                        |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_draw_opaque**         | Only draw depth for opaque geometry (not transparent).                                               |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_draw_always**         | Always draw depth (opaque and transparent).                                                          |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_draw_never**          | Never draw depth.                                                                                    |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_prepass_alpha**       | Do opaque depth pre-pass for transparent geometry.                                                   |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_test_disabled**       | Disable depth testing.                                                                               |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_test_default**        | Depth test will discard the pixel if it is behind other pixels.                                      |
|                               | In Forward+ only, the pixel is also discarded if it's at the exact same depth as another pixel.      |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **depth_test_inverted**       | Depth test will discard the pixel if it is in front of other pixels. Useful for stencil effects.     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **sss_mode_skin**             | Subsurface Scattering mode for skin (optimizes visuals for human skin, e.g. boosted red channel).    |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **cull_back**                 | Cull back-faces (default).                                                                           |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **cull_front**                | Cull front-faces.                                                                                    |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **cull_disabled**             | Culling disabled (double sided).                                                                     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **unshaded**                  | Result is just albedo. No lighting/shading happens in material, making it faster to render.          |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **wireframe**                 | Geometry draws using lines (useful for troubleshooting).                                             |
|                               | When using the Compatibility renderer, you must call                                                 |
|                               | ``RenderingServer.set_debug_generate_wireframes(true)`` *before* the mesh is loaded for wireframe    |
|                               | rendering to work. In the Compatibility renderer, backface culling is always disabled in wireframe   |
|                               | mode, while in the Forward+ and Mobile renderers, the cull mode is respected.                        |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **debug_shadow_splits**       | Directional shadows are drawn using different colors for each split (useful for troubleshooting).    |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **diffuse_burley**            | Burley (Disney PBS) for diffuse (default).                                                           |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **diffuse_lambert**           | Lambert shading for diffuse.                                                                         |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **diffuse_lambert_wrap**      | Lambert-wrap shading (roughness-dependent) for diffuse.                                              |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **diffuse_toon**              | Toon shading for diffuse.                                                                            |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **specular_schlick_ggx**      | Schlick-GGX for direct light specular lobes (default).                                               |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **specular_toon**             | Toon for direct light specular lobes.                                                                |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **specular_disabled**         | Disable direct light specular lobes. Doesn't affect reflected light (use ``SPECULAR = 0.0`` instead).|
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **skip_vertex_transform**     | ``VERTEX``, ``NORMAL``, ``TANGENT``, and ``BITANGENT``                                               |
|                               | need to be transformed manually in the ``vertex()`` function.                                        |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **world_vertex_coords**       | ``VERTEX``, ``NORMAL``, ``TANGENT``, and ``BITANGENT``                                               |
|                               | are modified in world space instead of model space.                                                  |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **ensure_correct_normals**    | Use when non-uniform scale is applied to mesh *(note: currently unimplemented)*.                     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **shadows_disabled**          | Disable computing shadows in shader. The shader will not receive shadows, but can still cast them.   |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **ambient_light_disabled**    | Disable contribution from ambient light and radiance map.                                            |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **shadow_to_opacity**         | Lighting modifies the alpha so shadowed areas are opaque and                                         |
|                               | non-shadowed areas are transparent. Useful for overlaying shadows onto                               |
|                               | a camera feed in AR.                                                                                 |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **vertex_lighting**           | Use vertex-based lighting instead of per-pixel lighting.                                             |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **particle_trails**           | Enables the trails when used on particle geometry.                                                   |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **alpha_to_coverage**         | Alpha antialiasing mode, see `here <https://github.com/godotengine/godot/pull/40364>`_ for more.     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **alpha_to_coverage_and_one** | Alpha antialiasing mode, see `here <https://github.com/godotengine/godot/pull/40364>`_ for more.     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **fog_disabled**              | Disable receiving depth-based or volumetric fog. Useful for ``blend_add`` materials like particles.  |
+-------------------------------+------------------------------------------------------------------------------------------------------+

Chế độ stencil
--------------

.. note::

    Tính năng hỗ trợ stencil đang ở trạng thái thử nghiệm, hãy tự chịu rủi ro khi sử dụng. Chúng tôi sẽ cố gắng không phá vỡ khả năng tương thích nhiều nhất có thể, nhưng nếu phát hiện các lỗi nghiêm trọng trong API, API có thể thay đổi ở phiên bản minor tiếp theo.

Các thao tác stencil là một tập hợp các thao tác cho phép ghi vào một buffer hiệu quả theo cách được tăng tốc bằng phần cứng. Tính năng này thường được dùng để che vào hoặc che ra các phần của scene.

Một số cách sử dụng phổ biến nhất là:

- Outlines: Che mesh bên trong đang được tạo outline để tránh xuất hiện outline bên trong. - X-Ray: Hiển thị một mesh phía sau các đối tượng khác. - Portals: Vẽ hình học vốn thường là "không thể" (phi Euclid) bằng cách che các đối tượng.

.. note::

    Bạn chỉ có thể đọc từ stencil buffer trong transparent pass. Mọi nỗ lực đọc trong opaque pass sẽ thất bại, vì hành vi này hiện chưa được hỗ trợ.

    Lưu ý rằng đối với các hiệu ứng compositor, stencil buffer của renderer chính không thể được sao chép vào một texture tùy chỉnh.

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Stencil mode                  | Description                                                                                          |
+===============================+======================================================================================================+
| **read**                      | Read from the stencil buffer.                                                                        |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **write**                     | Write reference value to the stencil buffer.                                                         |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **write_if_depth_fail**       | Write reference value to the stencil buffer if the depth test fails.                                 |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_always**            | Always pass stencil test.                                                                            |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_equal**             | Pass stencil test if the reference value is equal to the stencil buffer value.                       |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_not_equal**         | Pass stencil test if the reference value is not equal to the stencil buffer value.                   |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_less**              | Pass stencil test if the reference value is less than the stencil buffer value.                      |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_less_or_equal**     | Pass stencil test if the reference value is less than or equal to the stencil buffer value.          |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_greater**           | Pass stencil test if the reference value is greater than the stencil buffer value.                   |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **compare_greater_or_equal**  | Pass stencil test if the reference value is greater than or equal to the stencil buffer value.       |
+-------------------------------+------------------------------------------------------------------------------------------------------+

Built-in
--------

Các giá trị được đánh dấu là ``in`` chỉ có thể đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết chứa các giá trị hợp lý. Các giá trị được đánh dấu là ``inout`` cung cấp một giá trị mặc định hợp lý và có thể được ghi tùy chọn. Không thể ghi vào sampler nên chúng không được đánh dấu.

Không phải tất cả built-in đều khả dụng trong mọi hàm xử lý. Để truy cập một vertex built-in từ hàm ``fragment()``, bạn có thể sử dụng một :ref:`varying <doc_shading_language_varyings>`. Điều tương tự cũng áp dụng khi truy cập fragment built-in từ hàm ``light()``.

Built-in toàn cục
-----------------

Built-in toàn cục khả dụng ở mọi nơi, bao gồm cả các hàm tùy chỉnh.

+-----------------------------+-----------------------------------------------------------------------------------------------------+
| Built-in                    | Description                                                                                         |
+=============================+=====================================================================================================+
| in float **TIME**           | Global time since the engine has started, in seconds. It repeats after every ``3,600``              |
|                             | seconds (which can be changed with the                                                              |
|                             | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>`            |
|                             | setting). It's affected by :ref:`time_scale<class_Engine_property_time_scale>` but not by pausing.  |
|                             | If you need a ``TIME`` variable that is not affected by time scale, add your own                    |
|                             | :ref:`global shader uniform<doc_shading_language_global_uniforms>` and update it each               |
|                             | frame.                                                                                              |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in float **PI**             | A ``PI`` constant (``3.141592``).                                                                   |
|                             | The ratio of a circle's circumference to its diameter and the number of radians in a half turn.     |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in float **TAU**            | A ``TAU`` constant (``6.283185``).                                                                  |
|                             | Equivalent to ``PI * 2`` and the number of radians in a full turn.                                  |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in float **E**              | An ``E`` constant (``2.718281``). Euler's number, the base of the natural logarithm.                |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in bool **OUTPUT_IS_SRGB**  | ``true`` when output is in sRGB color space (this is ``true`` in the Compatibility                  |
|                             | renderer, ``false`` in Forward+ and Mobile).                                                        |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in float **CLIP_SPACE_FAR** | Clip space far ``z`` value.                                                                         |
|                             | In the Forward+ or Mobile renderers, it's ``0.0``.                                                  |
|                             | In the Compatibility renderer, it's ``-1.0``.                                                       |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in bool **IS_MULTIVIEW**    | ``true`` when output is stereoscopic (XR), ``false`` when output is monoscopic.                     |
+-----------------------------+-----------------------------------------------------------------------------------------------------+
| in bool **IN_SHADOW_PASS**  | ``true`` when the shader is being rendered in a shadow mapping pass, ``false`` otherwise.           |
|                             | This can be used to render objects differently in shadow maps compared to their regular rendering.  |
+-----------------------------+-----------------------------------------------------------------------------------------------------+

Vertex built-in
---------------

Dữ liệu vertex (``VERTEX``, ``NORMAL``, ``TANGENT`` và ``BITANGENT``) được cung cấp trong model space (còn gọi là local space). Nếu không được ghi, các giá trị này sẽ không bị thay đổi mà được truyền tiếp như ban đầu, sau đó được chuyển đổi sang view space để sử dụng trong ``fragment()``.

Bạn có thể tùy chọn cung cấp chúng trong world space bằng cách sử dụng chế độ kết xuất ``world_vertex_coords``.

Người dùng có thể tắt phép biến đổi modelview tích hợp (phép chiếu vẫn sẽ diễn ra sau đó) và thực hiện thủ công bằng đoạn code sau:

.. code-block:: glsl

    shader_type spatial;
    render_mode skip_vertex_transform;

    void vertex() {
        VERTEX = (MODELVIEW_MATRIX * vec4(VERTEX, 1.0)).xyz;
        NORMAL = normalize((MODELVIEW_MATRIX * vec4(NORMAL, 0.0)).xyz);
        BINORMAL = normalize((MODELVIEW_MATRIX * vec4(BINORMAL, 0.0)).xyz);
        TANGENT = normalize((MODELVIEW_MATRIX * vec4(TANGENT, 0.0)).xyz);
    }

Các built-in khác, chẳng hạn như ``UV``, ``UV2`` và ``COLOR``, cũng được truyền tiếp đến hàm ``fragment()`` nếu không bị sửa đổi.

Người dùng có thể ghi đè các phép biến đổi modelview và projection bằng built-in ``POSITION``. Nếu ``POSITION`` được ghi ở bất kỳ đâu trong shader, nó sẽ luôn được sử dụng, vì vậy người dùng có trách nhiệm đảm bảo rằng nó luôn có một giá trị chấp nhận được. Khi ``POSITION`` được sử dụng, giá trị từ ``VERTEX`` sẽ bị bỏ qua và phép chiếu sẽ không diễn ra. Tuy nhiên, giá trị được truyền đến fragment shader vẫn đến từ ``VERTEX``.

Đối với instancing, biến ``INSTANCE_CUSTOM`` chứa dữ liệu tùy chỉnh của instance. Khi sử dụng particle, thông tin này thường là:

* **x**: Góc xoay tính bằng radian. * **y**: Pha trong suốt vòng đời (``0.0`` đến ``1.0``). * **z**: Khung hình animation.

Điều này cho phép bạn dễ dàng điều chỉnh shader cho một hệ thống particle sử dụng material particle mặc định. Khi viết shader particle tùy chỉnh, bạn có thể sử dụng giá trị này theo ý muốn.

+----------------------------------------+--------------------------------------------------------+
| Built-in                               | Description                                            |
+========================================+========================================================+
| in vec2 **VIEWPORT_SIZE**              | Size of viewport (in pixels).                          |
+----------------------------------------+--------------------------------------------------------+
| in mat4 **VIEW_MATRIX**                | World space to view space transform.                   |
+----------------------------------------+--------------------------------------------------------+
| in mat4 **INV_VIEW_MATRIX**            | View space to world space transform.                   |
+----------------------------------------+--------------------------------------------------------+
| in mat4 **MAIN_CAM_INV_VIEW_MATRIX**   | View space to world space transform of the camera used |
|                                        | to draw the current viewport.                          |
+----------------------------------------+--------------------------------------------------------+
| in mat4 **INV_PROJECTION_MATRIX**      | Clip space to view space transform.                    |
+----------------------------------------+--------------------------------------------------------+
| in vec3 **NODE_POSITION_WORLD**        | Node position, in world space.                         |
+----------------------------------------+--------------------------------------------------------+
| in vec3 **NODE_POSITION_VIEW**         | Node position, in view space.                          |
+----------------------------------------+--------------------------------------------------------+
| in vec3 **CAMERA_POSITION_WORLD**      | Camera position, in world space. Represents the        |
|                                        | midpoint of the two eyes when in multiview/stereo      |
|                                        | rendering.                                             |
+----------------------------------------+--------------------------------------------------------+
| in vec3 **CAMERA_DIRECTION_WORLD**     | Camera direction, in world space.                      |
+----------------------------------------+--------------------------------------------------------+
| in uint **CAMERA_VISIBLE_LAYERS**      | Cull layers of the camera rendering the current pass.  |
+----------------------------------------+--------------------------------------------------------+
| in int **INSTANCE_ID**                 | Instance ID for instancing.                            |
+----------------------------------------+--------------------------------------------------------+
| in vec4 **INSTANCE_CUSTOM**            | Instance custom data (for particles, mostly).          |
+----------------------------------------+--------------------------------------------------------+
| in int **VIEW_INDEX**                  | The view that we are rendering.                        |
|                                        | ``VIEW_MONO_LEFT`` (``0``) for Mono (not multiview) or |
|                                        | left eye, ``VIEW_RIGHT`` (``1``) for right eye.        |
+----------------------------------------+--------------------------------------------------------+
| in int **VIEW_MONO_LEFT**              | Constant for Mono or left eye, always ``0``.           |
+----------------------------------------+--------------------------------------------------------+
| in int **VIEW_RIGHT**                  | Constant for right eye, always ``1``.                  |
+----------------------------------------+--------------------------------------------------------+
| in vec3 **EYE_OFFSET**                 | Position offset for the eye being rendered, in view    |
|                                        | space. Only applicable for multiview rendering.        |
+----------------------------------------+--------------------------------------------------------+
| inout vec3 **VERTEX**                  | Position of the vertex, in model space.                |
|                                        | In world space if ``world_vertex_coords`` is used.     |
+----------------------------------------+--------------------------------------------------------+
| in int **VERTEX_ID**                   | The index of the current vertex in the vertex buffer.  |
+----------------------------------------+--------------------------------------------------------+
| inout vec3 **NORMAL**                  | Normal in model space.                                 |
|                                        | In world space if ``world_vertex_coords`` is used.     |
+----------------------------------------+--------------------------------------------------------+
| inout vec3 **TANGENT**                 | Tangent in model space.                                |
|                                        | In world space if ``world_vertex_coords`` is used.     |
+----------------------------------------+--------------------------------------------------------+
| inout vec3 **BINORMAL**                | Binormal in model space.                               |
|                                        | In world space if ``world_vertex_coords`` is used.     |
+----------------------------------------+--------------------------------------------------------+
| out vec4 **POSITION**                  | If written to on any branch, overrides final vertex    |
|                                        | position in clip space.                                |
+----------------------------------------+--------------------------------------------------------+
| inout vec2 **UV**                      | UV main channel.                                       |
+----------------------------------------+--------------------------------------------------------+
| inout vec2 **UV2**                     | UV secondary channel.                                  |
+----------------------------------------+--------------------------------------------------------+
| inout vec4 **COLOR**                   | Color from vertices. Limited to values between ``0.0`` |
|                                        | and ``1.0`` for each channel and 8 bits per channel    |
|                                        | precision (256 possible levels). Alpha channel is      |
|                                        | supported. Values outside the allowed range are        |
|                                        | clamped, and values may be rounded due to precision    |
|                                        | limitations. Use ``CUSTOM0``-``CUSTOM3`` to pass data  |
|                                        | with more precision if needed.                         |
+----------------------------------------+--------------------------------------------------------+
| out float **ROUGHNESS**                | Roughness for vertex lighting.                         |
+----------------------------------------+--------------------------------------------------------+
| inout float **POINT_SIZE**             | Point size for point rendering.                        |
+----------------------------------------+--------------------------------------------------------+
| inout mat4 **MODELVIEW_MATRIX**        | Model/local space to view space transform              |
|                                        | (use if possible).                                     |
+----------------------------------------+--------------------------------------------------------+
| inout mat3 **MODELVIEW_NORMAL_MATRIX** |                                                        |
+----------------------------------------+--------------------------------------------------------+
| in mat4 **MODEL_MATRIX**               | Model/local space to world space transform.            |
+----------------------------------------+--------------------------------------------------------+
| in mat3 **MODEL_NORMAL_MATRIX**        |                                                        |
+----------------------------------------+--------------------------------------------------------+
| inout mat4 **PROJECTION_MATRIX**       | View space to clip space transform.                    |
+----------------------------------------+--------------------------------------------------------+
| in uvec4 **BONE_INDICES**              |                                                        |
+----------------------------------------+--------------------------------------------------------+
| in vec4 **BONE_WEIGHTS**               |                                                        |
+----------------------------------------+--------------------------------------------------------+
| in vec4 **CUSTOM0**                    | Custom value from vertex primitive. When using extra   |
|                                        | UVs, ``xy`` is UV3 and ``zw`` is UV4.                  |
+----------------------------------------+--------------------------------------------------------+
| in vec4 **CUSTOM1**                    | Custom value from vertex primitive. When using extra   |
|                                        | UVs, ``xy`` is UV5 and ``zw`` is UV6.                  |
+----------------------------------------+--------------------------------------------------------+
| in vec4 **CUSTOM2**                    | Custom value from vertex primitive. When using extra   |
|                                        | UVs, ``xy`` is UV7 and ``zw`` is UV8.                  |
+----------------------------------------+--------------------------------------------------------+
| in vec4 **CUSTOM3**                    | Custom value from vertex primitive.                    |
+----------------------------------------+--------------------------------------------------------+
| out float **Z_CLIP_SCALE**             | If written to on any branch, scales the vertex towards |
|                                        | the camera to avoid clipping into things like walls.   |
|                                        | Lighting and shadows will continue to work correctly   |
|                                        | when this is written to, but screen-space effects like |
|                                        | SSAO and SSR may break with lower scales. Try to keep  |
|                                        | this value as close to ``1.0`` as possible.            |
+----------------------------------------+--------------------------------------------------------+

.. note::

    ``MODELVIEW_MATRIX`` kết hợp cả ``MODEL_MATRIX`` và ``VIEW_MATRIX``, phù hợp hơn khi có thể phát sinh vấn đề về số dấu phẩy động. Ví dụ, nếu đối tượng ở rất xa gốc tọa độ của world, bạn có thể gặp vấn đề về số dấu phẩy động khi sử dụng ``MODEL_MATRIX`` và ``VIEW_MATRIX`` tách biệt.

.. note::

    ``INV_VIEW_MATRIX`` là ma trận được dùng để kết xuất đối tượng trong pass đó, không giống ``MAIN_CAM_INV_VIEW_MATRIX``, là ma trận của camera trong scene. Trong shadow pass, view của ``INV_VIEW_MATRIX`` dựa trên camera nằm tại vị trí của light.

Fragment built-in
-----------------

Cách sử dụng mặc định của hàm xử lý fragment trong Godot là thiết lập các thuộc tính material của đối tượng và để renderer tích hợp xử lý việc đổ bóng cuối cùng. Tuy nhiên, bạn không bắt buộc phải sử dụng tất cả các thuộc tính này; nếu không ghi vào chúng, Godot sẽ tối ưu hóa bằng cách loại bỏ chức năng tương ứng.

+----------------------------------------+--------------------------------------------------------------------------------------------------+
| Built-in                               | Description                                                                                      |
+========================================+==================================================================================================+
| in vec2 **VIEWPORT_SIZE**              | Size of viewport (in pixels).                                                                    |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec4 **FRAGCOORD**                  | Coordinate of pixel center in screen space. ``xy`` specifies position in window. Upper-left of   |
|                                        | the viewport is the origin, ``(0.0, 0.0)``. Bottom-right of the viewport is ``(1.0, 1.0)``.      |
|                                        | ``z`` specifies fragment depth. It is also used as the output value for the fragment depth       |
|                                        | unless ``DEPTH`` is written to.                                                                  |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in bool **FRONT_FACING**               | ``true`` if current face is front facing, ``false`` otherwise.                                   |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **VIEW**                       | Normalized vector from fragment position to camera (in view space). This is the same for both    |
|                                        | perspective and orthogonal cameras.                                                              |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec2 **UV**                         | UV that comes from the ``vertex()`` function.                                                    |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec2 **UV2**                        | UV2 that comes from the ``vertex()`` function.                                                   |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec4 **COLOR**                      | COLOR that comes from the ``vertex()`` function.                                                 |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec2 **POINT_COORD**                | Point coordinate for drawing points with ``POINT_SIZE``.                                         |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in mat4 **MODEL_MATRIX**               | Model/local space to world space transform.                                                      |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in mat3 **MODEL_NORMAL_MATRIX**        | Model/local space to world space transform for normals. This is the same as ``MODEL_MATRIX``     |
|                                        | by default unless the object is scaled non-uniformly, in which case this is set to               |
|                                        | ``transpose(inverse(mat3(MODEL_MATRIX)))``.                                                      |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in mat4 **VIEW_MATRIX**                | World space to view space transform.                                                             |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in mat4 **INV_VIEW_MATRIX**            | View space to world space transform.                                                             |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in mat4 **PROJECTION_MATRIX**          | View space to clip space transform.                                                              |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in mat4 **INV_PROJECTION_MATRIX**      | Clip space to view space transform.                                                              |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **NODE_POSITION_WORLD**        | Node position, in world space.                                                                   |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **NODE_POSITION_VIEW**         | Node position, in view space.                                                                    |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **CAMERA_POSITION_WORLD**      | Camera position, in world space. Represents the midpoint of the two eyes when in                 |
|                                        | multiview/stereo rendering.                                                                      |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **CAMERA_DIRECTION_WORLD**     | Camera direction, in world space.                                                                |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in uint **CAMERA_VISIBLE_LAYERS**      | Cull layers of the camera rendering the current pass.                                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **VERTEX**                     | Position of the fragment (pixel), in view space. It is the ``VERTEX`` value from ``vertex()``    |
|                                        | interpolated between the face's vertices and transformed into view space.                        |
|                                        | If ``skip_vertex_transform`` is enabled, it may not be in view space.                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| inout vec3 **LIGHT_VERTEX**            | A writable version of ``VERTEX`` that can be used to alter light and shadows. Writing to this    |
|                                        | will not change the position of the fragment.                                                    |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in int **VIEW_INDEX**                  | The view that we are rendering. Used to distinguish between views in multiview/stereo rendering. |
|                                        | ``VIEW_MONO_LEFT`` (``0``) for Mono (not multiview) or                                           |
|                                        | left eye, ``VIEW_RIGHT`` (``1``) for right eye.                                                  |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in int **VIEW_MONO_LEFT**              | Constant for Mono or left eye, always ``0``.                                                     |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in int **VIEW_RIGHT**                  | Constant for right eye, always ``1``.                                                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec3 **EYE_OFFSET**                 | Position offset for the eye being rendered, in view space. Only applicable for multiview         |
|                                        | rendering.                                                                                       |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| sampler2D **SCREEN_TEXTURE**           | Removed in Godot 4. Use a ``sampler2D`` with ``hint_screen_texture`` instead.                    |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| in vec2 **SCREEN_UV**                  | Screen UV coordinate for the current pixel.                                                      |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| sampler2D **DEPTH_TEXTURE**            | Removed in Godot 4. Use a ``sampler2D`` with ``hint_depth_texture`` instead.                     |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **DEPTH**                    | Custom depth value (range ``[0.0, 1.0]``). If ``DEPTH`` is written to in any shader branch,      |
|                                        | then you are responsible for setting ``DEPTH`` for **all** other branches.                       |
|                                        | Otherwise, the graphics API will leave them uninitialized.                                       |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| inout vec3 **NORMAL**                  | Normal that comes from the ``vertex()`` function, in view space.                                 |
|                                        | If ``skip_vertex_transform`` is enabled, it may not be in view space.                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| inout vec3 **TANGENT**                 | Tangent that comes from the ``vertex()`` function, in view space.                                |
|                                        | If ``skip_vertex_transform`` is enabled, it may not be in view space.                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| inout vec3 **BINORMAL**                | Binormal that comes from the ``vertex()`` function, in view space.                               |
|                                        | If ``skip_vertex_transform`` is enabled, it may not be in view space.                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec3 **NORMAL_MAP**                | Set normal here in tangent space if reading normal from a texture instead of ``NORMAL``.         |
|                                        | The blue channel is ignored, as it's reconstructed in the engine instead.                        |
|                                        | This allows normal maps with :abbr:`RGTC (Red-Green Texture Compression)` compression to work.   |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **NORMAL_MAP_DEPTH**         | Depth from ``NORMAL_MAP``. Defaults to ``1.0``.                                                  |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec3 **BENT_NORMAL_MAP**           | Set bent normal map here in tangent space to enable                                              |
|                                        | :ref:`bent normals <doc_standard_material_3d_bent_normal_map>`.                                  |
|                                        | This is used to improve specular occlusion, and requires a specially authored bent normal map.   |
|                                        | The blue channel is ignored, as it's reconstructed in the engine instead. This allows            |
|                                        | bent normal maps with :abbr:`RGTC (Red-Green Texture Compression)` compression to work.          |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec3 **ALBEDO**                    | Albedo (default white). Base color.                                                              |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **ALPHA**                    | Alpha (range ``[0.0, 1.0]``). If read from or written to, the material will go to the            |
|                                        | transparent pipeline.                                                                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **ALPHA_SCISSOR_THRESHOLD**  | If written to on any branch, values below a certain amount of alpha are discarded.               |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **ALPHA_HASH_SCALE**         | Alpha hash scale when using the alpha hash transparency mode. Defaults to ``1.0``.               |
|                                        | Higher values result in more visible pixels in the dithering pattern.                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **ALPHA_ANTIALIASING_EDGE**  | The threshold below which alpha to coverage antialiasing should be used. Defaults to ``0.0``.    |
|                                        | Requires the ``alpha_to_coverage`` render mode. Should be set to a value lower than              |
|                                        | ``ALPHA_SCISSOR_THRESHOLD`` to be effective.                                                     |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec2 **ALPHA_TEXTURE_COORDINATE**  | The texture coordinate to use for alpha-to-coverge antialiasing. Requires the                    |
|                                        | ``alpha_to_coverage`` render mode. Typically set to ``UV * vec2(albedo_texture_size)`` where     |
|                                        | ``albedo_texture_size`` is the size of the albedo texture in pixels.                             |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **PREMUL_ALPHA_FACTOR**      | Premultiplied alpha factor. Only effective if ``render_mode blend_premul_alpha;`` is used.       |
|                                        | This should be written to when using a *shaded* material with premultiplied alpha blending for   |
|                                        | interaction with lighting. This is not required for unshaded materials.                          |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **METALLIC**                 | Metallic (range ``[0.0, 1.0]``).                                                                 |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **SPECULAR**                 | Specular (not physically accurate to change). Defaults to ``0.5``. ``0.0`` disables reflections. |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **ROUGHNESS**                | Roughness (range ``[0.0, 1.0]``).                                                                |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **RIM**                      | Rim (range ``[0.0, 1.0]``). If used, Godot calculates rim lighting.                              |
|                                        | Rim size depends on ``ROUGHNESS``.                                                               |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **RIM_TINT**                 | Rim Tint, range from ``0.0`` (white) to ``1.0`` (albedo). If used, Godot calculates rim lighting.|
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **CLEARCOAT**                | Small specular blob added on top of the existing one. If used, Godot calculates clearcoat.       |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **CLEARCOAT_ROUGHNESS**      | The roughness of the clearcoat. If used, Godot calculates clearcoat.                             |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **ANISOTROPY**               | For distorting the specular blob according to tangent space.                                     |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec2 **ANISOTROPY_FLOW**           | Distortion direction, use with flowmaps.                                                         |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **SSS_STRENGTH**             | Strength of subsurface scattering. If used, subsurface scattering will be applied to the object. |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec4 **SSS_TRANSMITTANCE_COLOR**   | Color of subsurface scattering transmittance. If used, subsurface scattering transmittance       |
|                                        | will be applied to the object.                                                                   |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **SSS_TRANSMITTANCE_DEPTH**  | Depth of subsurface scattering transmittance. Higher values allow the effect to reach deeper     |
|                                        | into the object.                                                                                 |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **SSS_TRANSMITTANCE_BOOST**  | Boosts the subsurface scattering transmittance if set above ``0.0``. This makes the effect       |
|                                        | show up even on directly lit surfaces                                                            |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| inout vec3 **BACKLIGHT**               | Color of backlighting (works like direct light, but it's received even if the normal             |
|                                        | is slightly facing away from the light). If used, backlighting will be applied to the object.    |
|                                        | Can be used as a cheaper approximation of subsurface scattering.                                 |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **AO**                       | Strength of ambient occlusion. For use with pre-baked AO.                                        |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out float **AO_LIGHT_AFFECT**          | How much ambient occlusion affects direct light (range ``[0.0, 1.0]``, default ``0.0``).         |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec3 **EMISSION**                  | Emission color (can go over ``(1.0, 1.0, 1.0)`` for HDR).                                        |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec4 **FOG**                       | If written to on any branch, blends final pixel color with ``FOG.rgb`` based on ``FOG.a``.       |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec4 **RADIANCE**                  | If written to on any branch, blends environment map radiance with ``RADIANCE.rgb`` based on      |
|                                        | ``RADIANCE.a``.                                                                                  |
+----------------------------------------+--------------------------------------------------------------------------------------------------+
| out vec4 **IRRADIANCE**                | If written to on any branch, blends environment map irradiance with ``IRRADIANCE.rgb`` based on  |
|                                        | ``IRRADIANCE.a``.                                                                                |
+----------------------------------------+--------------------------------------------------------------------------------------------------+

.. note::

    Các shader đi qua transparent pipeline khi ghi vào ``ALPHA`` có thể gặp vấn đề về sắp xếp độ trong suốt. Đọc
    :ref:`transparency sorting section in the 3D rendering limitations page <doc_3d_rendering_limitations_transparency_sorting>`
    để biết thêm thông tin và các cách tránh vấn đề này.

Light built-in
--------------

Việc viết các hàm xử lý light là hoàn toàn tùy chọn. Bạn có thể bỏ qua hàm ``light()`` bằng cách sử dụng chế độ kết xuất ``unshaded``. Nếu không viết hàm light, Godot sẽ sử dụng các thuộc tính material được ghi trong hàm ``fragment()`` để tính toán ánh sáng cho bạn (tùy thuộc vào chế độ kết xuất).

Hàm ``light()`` được gọi cho mỗi light trong mỗi pixel. Hàm được gọi bên trong một vòng lặp cho từng loại light.

Dưới đây là ví dụ về một hàm ``light()`` tùy chỉnh sử dụng mô hình chiếu sáng Lambertian:

.. code-block:: glsl

    void light() {
        if (LIGHT_IS_AREA) {
            // Đổ bóng GGX của area light.
            DIFFUSE_LIGHT += LIGHT_AREA_DIFFUSE_MULTIPLIER * ATTENUATION * LIGHT_COLOR;
            SPECULAR_LIGHT += LIGHT_AREA_SPECULAR_MULTIPLIER * ATTENUATION * LIGHT_COLOR * SPECULAR_AMOUNT;
        } else {
            // Được sử dụng cho tất cả các loại light khác (directional, omni, spot).
            DIFFUSE_LIGHT += clamp(dot(NORMAL, LIGHT), 0.0, 1.0) * ATTENUATION * LIGHT_COLOR / PI;
        }
    }

Nếu muốn các light cộng dồn với nhau, hãy thêm phần đóng góp của light vào ``DIFFUSE_LIGHT`` bằng ``+=``, thay vì ghi đè lên nó.

.. warning::

    Hàm ``light()`` sẽ không được chạy nếu chế độ kết xuất ``vertex_lighting`` được bật hoặc nếu
    :ref:`Rendering > Quality > Shading > Force Vertex Shading<class_ProjectSettings_property_rendering/shading/overrides/force_vertex_shading>`
    được bật trong Project Settings. (Theo mặc định, tùy chọn này được bật trên các nền tảng mobile.)

+-----------------------------------+------------------------------------------------------------------------+
| Built-in                          | Description                                                            |
+===================================+========================================================================+
| in vec2 **VIEWPORT_SIZE**         | Size of viewport (in pixels).                                          |
+-----------------------------------+------------------------------------------------------------------------+
| in vec4 **FRAGCOORD**             | Coordinate of pixel center in screen space. ``xy`` specifies position  |
|                                   | in window. Upper-left of the viewport is the origin, ``(0.0, 0.0)``.   |
|                                   | Bottom-right of the viewport is ``(1.0, 1.0)``.                        |
|                                   | ``z`` specifies fragment depth. It is also used as the output value    |
|                                   | for the fragment depth unless ``DEPTH`` is written to.                 |
+-----------------------------------+------------------------------------------------------------------------+
| in mat4 **MODEL_MATRIX**          | Model/local space to world space transform.                            |
+-----------------------------------+------------------------------------------------------------------------+
| in mat4 **INV_VIEW_MATRIX**       | View space to world space transform.                                   |
+-----------------------------------+------------------------------------------------------------------------+
| in mat4 **VIEW_MATRIX**           | World space to view space transform.                                   |
+-----------------------------------+------------------------------------------------------------------------+
| in mat4 **PROJECTION_MATRIX**     | View space to clip space transform.                                    |
+-----------------------------------+------------------------------------------------------------------------+
| in mat4 **INV_PROJECTION_MATRIX** | Clip space to view space transform.                                    |
+-----------------------------------+------------------------------------------------------------------------+
| in vec3 **NORMAL**                | Normal vector, in view space.                                          |
+-----------------------------------+------------------------------------------------------------------------+
| in vec2 **SCREEN_UV**             | Screen UV coordinate for the current pixel.                            |
+-----------------------------------+------------------------------------------------------------------------+
| in vec2 **UV**                    | UV that comes from the ``vertex()`` function.                          |
+-----------------------------------+------------------------------------------------------------------------+
| in vec2 **UV2**                   | UV2 that comes from the ``vertex()`` function.                         |
+-----------------------------------+------------------------------------------------------------------------+
| in vec3 **VIEW**                  | View vector, in view space.                                            |
+-----------------------------------+------------------------------------------------------------------------+
| in vec3 **LIGHT**                 | Light vector, in view space.                                           |
+-----------------------------------+------------------------------------------------------------------------+
| in vec3 **LIGHT_COLOR**           | :ref:`Light color<class_Light3D_property_light_color>` multiplied by   |
|                                   | :ref:`light energy<class_Light3D_property_light_energy>` multiplied by |
|                                   | ``PI``. The ``PI`` multiplication is present because                   |
|                                   | physically-based lighting models include a division by ``PI``.         |
+-----------------------------------+------------------------------------------------------------------------+
| in float **SPECULAR_AMOUNT**      | For :ref:`class_OmniLight3D` and :ref:`class_SpotLight3D`,             |
|                                   | ``2.0`` multiplied by                                                  |
|                                   | :ref:`light_specular<class_Light3D_property_light_specular>`.          |
|                                   | For :ref:`class_DirectionalLight3D`, ``1.0``.                          |
+-----------------------------------+------------------------------------------------------------------------+
| in bool **LIGHT_IS_DIRECTIONAL**  | ``true`` if this pass is a :ref:`class_DirectionalLight3D`.            |
+-----------------------------------+------------------------------------------------------------------------+
| in float **ATTENUATION**          | Attenuation based on distance or shadow.                               |
+-----------------------------------+------------------------------------------------------------------------+
| in vec3 **ALBEDO**                | Base albedo.                                                           |
+-----------------------------------+------------------------------------------------------------------------+
| in vec3 **BACKLIGHT**             |                                                                        |
+-----------------------------------+------------------------------------------------------------------------+
| in float **METALLIC**             | Metallic.                                                              |
+-----------------------------------+------------------------------------------------------------------------+
| in float **ROUGHNESS**            | Roughness.                                                             |
+-----------------------------------+------------------------------------------------------------------------+
| out vec3 **DIFFUSE_LIGHT**        | Diffuse light result.                                                  |
+-----------------------------------+------------------------------------------------------------------------+
| out vec3 **SPECULAR_LIGHT**       | Specular light result.                                                 |
+-----------------------------------+------------------------------------------------------------------------+
| out float **ALPHA**               | Alpha (range ``[0.0, 1.0]``). If written to on any branch, the         |
|                                   | material will go through the transparent pipeline.                     |
+-----------------------------------+------------------------------------------------------------------------+

.. note::

    Các shader đi qua transparent pipeline khi ghi vào ``ALPHA`` có thể gặp vấn đề về sắp xếp độ trong suốt. Đọc
    :ref:`transparency sorting section in the 3D rendering limitations page <doc_3d_rendering_limitations_transparency_sorting>`
    để biết thêm thông tin và các cách tránh vấn đề này.

    Material trong suốt cũng không thể đổ bóng hoặc xuất hiện trong các uniform ``hint_screen_texture`` và ``hint_depth_texture``. Điều này khiến các material đó không xuất hiện trong phản xạ hoặc khúc xạ trong screen space.
    :ref:`SDFGI <doc_using_sdfgi>` sharp reflections are not visible on transparent
    material (chỉ có thể thấy các phản xạ thô trên material trong suốt).
