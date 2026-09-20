.. _doc_canvas_item_shader:

Shader CanvasItem
=================

Shader CanvasItem được dùng để vẽ tất cả các phần tử 2D trong Godot. Chúng bao gồm tất cả các node kế thừa từ CanvasItems và tất cả các phần tử GUI.

Shader CanvasItem chứa ít biến built-in và chức năng hơn
:ref:`Spatial shaders<doc_spatial_shader>`, but they maintain the same basic structure
với các hàm xử lý vertex, fragment và light.

Chế độ kết xuất
---------------

+---------------------------------+----------------------------------------------------------------------+
| Render mode                     | Description                                                          |
+=================================+======================================================================+
| **blend_mix**                   | Mix blend mode (alpha is transparency), default.                     |
+---------------------------------+----------------------------------------------------------------------+
| **blend_add**                   | Additive blend mode.                                                 |
+---------------------------------+----------------------------------------------------------------------+
| **blend_sub**                   | Subtractive blend mode.                                              |
+---------------------------------+----------------------------------------------------------------------+
| **blend_mul**                   | Multiplicative blend mode.                                           |
+---------------------------------+----------------------------------------------------------------------+
| **blend_premul_alpha**          | Pre-multiplied alpha blend mode.                                     |
+---------------------------------+----------------------------------------------------------------------+
| **blend_disabled**              | Disable blending, values (including alpha) are written as-is.        |
+---------------------------------+----------------------------------------------------------------------+
| **unshaded**                    | Result is just albedo. No lighting/shading happens in material.      |
+---------------------------------+----------------------------------------------------------------------+
| **light_only**                  | Only draw in the light pass.                                         |
+---------------------------------+----------------------------------------------------------------------+
| **skip_vertex_transform**       | ``VERTEX`` needs to be transformed manually in the ``vertex()``      |
|                                 | function.                                                            |
+---------------------------------+----------------------------------------------------------------------+
| **world_vertex_coords**         | ``VERTEX`` is modified in world coordinates instead of local.        |
+---------------------------------+----------------------------------------------------------------------+

Built-in
--------

Các giá trị được đánh dấu là ``in`` chỉ có thể đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết chứa các giá trị hợp lý. Các giá trị được đánh dấu là ``inout`` cung cấp một giá trị mặc định hợp lý và có thể được ghi tùy chọn. Không thể ghi vào sampler nên chúng không được đánh dấu.

Không phải tất cả built-in đều khả dụng trong mọi hàm xử lý. Để truy cập một built-in của vertex từ hàm ``fragment()``, bạn có thể sử dụng một :ref:`varying <doc_shading_language_varyings>`. Điều tương tự cũng áp dụng khi truy cập các built-in của fragment từ hàm ``light()``.

Built-in toàn cục
-----------------

Built-in toàn cục khả dụng ở mọi nơi, bao gồm cả các hàm tùy chỉnh.

+-------------------+-------------------------------------------------------------------------------------------------+
| Built-in          | Description                                                                                     |
+===================+=================================================================================================+
| in float **TIME** | Global time since the engine has started, in seconds. It repeats after every ``3,600``          |
|                   | seconds (which can be changed with the                                                          |
|                   | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>`        |
|                   | setting). It's affected by                                                                      |
|                   | :ref:`time_scale<class_Engine_property_time_scale>` but not by pausing. If you need a           |
|                   | ``TIME`` variable that is not affected by time scale, add your own                              |
|                   | :ref:`global shader uniform<doc_shading_language_global_uniforms>` and update it each           |
|                   | frame.                                                                                          |
+-------------------+-------------------------------------------------------------------------------------------------+
| in float **PI**   | A ``PI`` constant (``3.141592``).                                                               |
|                   | The ratio of a circle's circumference to its diameter and the number of radians in a half turn. |
+-------------------+-------------------------------------------------------------------------------------------------+
| in float **TAU**  | A ``TAU`` constant (``6.283185``).                                                              |
|                   | Equivalent to ``PI * 2`` and the number of radians in a full turn.                              |
+-------------------+-------------------------------------------------------------------------------------------------+
| in float **E**    | An ``E`` constant (``2.718281``).                                                               |
|                   | Euler's number, the base of the natural logarithm.                                              |
+-------------------+-------------------------------------------------------------------------------------------------+

Built-in của vertex
-------------------

Dữ liệu vertex (``VERTEX``) được cung cấp trong không gian cục bộ (tọa độ pixel, tương đối so với gốc của Node2D). Nếu không được ghi, các giá trị này sẽ không bị thay đổi và được truyền tiếp như ban đầu.

Người dùng có thể tắt phép biến đổi built-in từ model sang world (việc biến đổi từ world sang screen và projection vẫn sẽ diễn ra sau đó) và tự thực hiện bằng đoạn code sau:

.. code-block:: glsl

    shader_type canvas_item;
    render_mode skip_vertex_transform;

    void vertex() {

        VERTEX = (MODEL_MATRIX * vec4(VERTEX, 0.0, 1.0)).xy;
    }

Các built-in khác, chẳng hạn như ``UV`` và ``COLOR``, cũng được truyền tiếp đến hàm ``fragment()`` nếu không bị thay đổi.

Đối với instancing, biến ``INSTANCE_CUSTOM`` chứa dữ liệu tùy chỉnh của instance. Khi sử dụng particle, thông tin này thường là:

* **x**: Góc xoay tính bằng radian. * **y**: Pha trong suốt vòng đời (``0.0`` đến ``1.0``). * **z**: Khung hình animation.

+--------------------------------+----------------------------------------------------------------+
| Built-in                       | Description                                                    |
+================================+================================================================+
| in mat4 **MODEL_MATRIX**       | Local space to world space transform. World space              |
|                                | is the coordinates you normally use in the editor.             |
+--------------------------------+----------------------------------------------------------------+
| in mat4 **CANVAS_MATRIX**      | World space to canvas space transform. In canvas               |
|                                | space the origin is the upper-left corner of the               |
|                                | screen and coordinates range from ``(0.0, 0.0)``               |
|                                | to viewport size.                                              |
+--------------------------------+----------------------------------------------------------------+
| in mat4 **SCREEN_MATRIX**      | Canvas space to clip space transform. In clip space            |
|                                | coordinates range from ``(-1.0, -1.0)`` to                     |
|                                | ``(1.0, 1.0).``                                                |
+--------------------------------+----------------------------------------------------------------+
| in int **INSTANCE_ID**         | Instance ID for instancing.                                    |
+--------------------------------+----------------------------------------------------------------+
| in vec4 **INSTANCE_CUSTOM**    | Instance custom data.                                          |
+--------------------------------+----------------------------------------------------------------+
| in bool **AT_LIGHT_PASS**      | Always ``false``.                                              |
+--------------------------------+----------------------------------------------------------------+
| in vec2 **TEXTURE_PIXEL_SIZE** | Normalized pixel size of the default 2D texture.               |
|                                | For a Sprite2D with a texture of size 64×32 pixels,            |
|                                | ``TEXTURE_PIXEL_SIZE`` = ``vec2(1.0 / 64.0, 1.0 / 32.0)``.     |
+--------------------------------+----------------------------------------------------------------+
| inout vec2 **VERTEX**          | Vertex position, in local space.                               |
+--------------------------------+----------------------------------------------------------------+
| in int **VERTEX_ID**           | The index of the current vertex in the vertex                  |
|                                | buffer.                                                        |
+--------------------------------+----------------------------------------------------------------+
| inout vec2 **UV**              | Normalized texture coordinates. Range from ``0.0``             |
|                                | to ``1.0``.                                                    |
+--------------------------------+----------------------------------------------------------------+
| inout vec4 **COLOR**           | Color from vertex primitive multiplied by the CanvasItem's     |
|                                | :ref:`modulate<class_CanvasItem_property_modulate>`            |
|                                | multiplied by CanvasItem's                                     |
|                                | :ref:`self_modulate<class_CanvasItem_property_self_modulate>`. |
+--------------------------------+----------------------------------------------------------------+
| inout float **POINT_SIZE**     | Point size for point drawing.                                  |
+--------------------------------+----------------------------------------------------------------+
| in vec4 **CUSTOM0**            | Custom value from vertex primitive.                            |
+--------------------------------+----------------------------------------------------------------+
| in vec4 **CUSTOM1**            | Custom value from vertex primitive.                            |
+--------------------------------+----------------------------------------------------------------+



Built-in của fragment
---------------------

COLOR và TEXTURE
~~~~~~~~~~~~~~~~

Biến built-in ``COLOR`` được dùng cho một vài mục đích:

  - Trong hàm ``vertex()``, ``COLOR`` chứa màu từ primitive của vertex được nhân với
    :ref:`modulate<class_CanvasItem_property_modulate>` multiplied by the
    :ref:`self_modulate<class_CanvasItem_property_self_modulate>` của CanvasItem. - Trong hàm ``fragment()``, giá trị đầu vào ``COLOR`` là cùng giá trị đó được nhân với màu từ ``TEXTURE`` mặc định (nếu có). - Trong hàm ``fragment()``, ``COLOR`` cũng là đầu ra cuối cùng.

Một số node (ví dụ: :ref:`Sprite2D <class_Sprite2D>`) hiển thị texture theo mặc định, chẳng hạn như :ref:`texture <class_Sprite2D_property_texture>`. Khi sử dụng hàm ``fragment()`` tùy chỉnh, bạn có một số tùy chọn về cách lấy mẫu texture này.

Để chỉ đọc nội dung của texture mặc định, bỏ qua ``COLOR`` của vertex:

.. code-block:: glsl

  void fragment() {
    COLOR = texture(TEXTURE, UV);
  }

Để đọc nội dung của texture mặc định được nhân với ``COLOR`` của vertex:

.. code-block:: glsl

  void fragment() {
    // Tương đương với một hàm fragment() rỗng, vì COLOR cũng là biến đầu ra.
    COLOR = COLOR;
  }

Để chỉ đọc ``COLOR`` của vertex trong ``fragment()``, bỏ qua texture chính, bạn phải truyền ``COLOR`` dưới dạng varying, sau đó đọc nó trong ``fragment()``:

.. code-block:: glsl

  varying vec4 vertex_color;
  void vertex() {
    vertex_color = COLOR;
  }
  void fragment() {
    COLOR = vertex_color;
  }

NORMAL
~~~~~~

Tương tự, nếu một normal map được sử dụng trong :ref:`CanvasTexture <class_CanvasTexture>`, Godot sẽ dùng nó theo mặc định và gán giá trị của nó cho biến built-in ``NORMAL``. Nếu bạn đang sử dụng một normal map dành cho 3D, nó sẽ hiển thị bị đảo ngược. Để sử dụng nó trong shader, bạn phải gán nó cho thuộc tính ``NORMAL_MAP``. Godot sẽ xử lý việc chuyển đổi để sử dụng trong 2D và ghi đè ``NORMAL``.

.. code-block:: glsl

  NORMAL_MAP = texture(NORMAL_TEXTURE, UV).rgb;

+---------------------------------------------+---------------------------------------------------------------+
| Built-in                                    | Description                                                   |
+=============================================+===============================================================+
| in vec4 **FRAGCOORD**                       | Coordinate of pixel center. In screen space. ``xy`` specifies |
|                                             | position in viewport. Upper-left of the viewport is the       |
|                                             | origin, ``(0.0, 0.0)``. Bottom-right of the viewport is       |
|                                             | ``(1.0, 1.0)``.                                               |
+---------------------------------------------+---------------------------------------------------------------+
| in vec2 **SCREEN_PIXEL_SIZE**               | Size of individual pixels. Equal to the inverse of resolution.|
+---------------------------------------------+---------------------------------------------------------------+
| in vec4 **REGION_RECT**                     | Visible area of the sprite region in format                   |
|                                             | ``(x, y, width, height)``. Varies according to                |
|                                             | Sprite2D's ``region_enabled`` property. Values are            |
|                                             | normalized; for example, a 600×400 region on a 1000×800       |
|                                             | texture with a 100×100 offset would be                        |
|                                             | ``vec4(0.1, 0.125, 0.6, 0.5)``. Values may exceed the 0.0 to  |
|                                             | 1.0 range if the X/Y offset is negative, or if the size       |
|                                             | exceeds the texture's size.                                   |
+---------------------------------------------+---------------------------------------------------------------+
| in vec2 **POINT_COORD**                     | Coordinate for drawing points in the 0.0 to 1.0 range.        |
+---------------------------------------------+---------------------------------------------------------------+
| sampler2D **TEXTURE**                       | Default 2D texture.                                           |
+---------------------------------------------+---------------------------------------------------------------+
| in vec2 **TEXTURE_PIXEL_SIZE**              | Normalized pixel size of the default 2D texture.              |
|                                             | For a Sprite2D with a texture of size 64×32 pixels,           |
|                                             | ``TEXTURE_PIXEL_SIZE`` = ``vec2(1.0 / 64.0, 1.0 / 32.0)``.    |
+---------------------------------------------+---------------------------------------------------------------+
| in bool **AT_LIGHT_PASS**                   | Always ``false``.                                             |
+---------------------------------------------+---------------------------------------------------------------+
| sampler2D **SPECULAR_SHININESS_TEXTURE**    | Specular shininess texture of this object.                    |
+---------------------------------------------+---------------------------------------------------------------+
| in vec4 **SPECULAR_SHININESS**              | Specular shininess color, as sampled from the texture.        |
+---------------------------------------------+---------------------------------------------------------------+
| in vec2 **UV**                              | UV from the ``vertex()`` function.                            |
|                                             | For a Sprite2D with region enabled, this will sample the      |
|                                             | entire texture. Use ``REGION_RECT`` instead to sample only    |
|                                             | the region defined in the Sprite2D's properties.              |
+---------------------------------------------+---------------------------------------------------------------+
| in vec2 **SCREEN_UV**                       | Screen UV coordinate for the current pixel.                   |
+---------------------------------------------+---------------------------------------------------------------+
| sampler2D **SCREEN_TEXTURE**                | Removed in Godot 4. Use a ``sampler2D`` with                  |
|                                             | ``hint_screen_texture`` instead.                              |
+---------------------------------------------+---------------------------------------------------------------+
| inout vec3 **NORMAL**                       | Normal read from ``NORMAL_TEXTURE``. Writable.                |
+---------------------------------------------+---------------------------------------------------------------+
| sampler2D **NORMAL_TEXTURE**                | Default 2D normal texture.                                    |
+---------------------------------------------+---------------------------------------------------------------+
| out vec3 **NORMAL_MAP**                     | Configures normal maps meant for 3D for use in 2D. If used,   |
|                                             | overrides ``NORMAL``.                                         |
+---------------------------------------------+---------------------------------------------------------------+
| out float **NORMAL_MAP_DEPTH**              | Normal map depth for scaling.                                 |
+---------------------------------------------+---------------------------------------------------------------+
| inout vec2 **VERTEX**                       | Pixel position in screen space.                               |
+---------------------------------------------+---------------------------------------------------------------+
| inout vec2 **SHADOW_VERTEX**                | Same as ``VERTEX`` but can be written to alter shadows.       |
+---------------------------------------------+---------------------------------------------------------------+
| inout vec3 **LIGHT_VERTEX**                 | Same as ``VERTEX`` but can be written to alter lighting.      |
|                                             | Z component represents height.                                |
+---------------------------------------------+---------------------------------------------------------------+
| inout vec4 **COLOR**                        | ``COLOR`` from the ``vertex()`` function multiplied by the    |
|                                             | ``TEXTURE`` color. Also output color value.                   |
+---------------------------------------------+---------------------------------------------------------------+

Built-in của light
------------------

Các hàm xử lý light hoạt động khác trong Godot 4.x so với Godot 3.x. Trong Godot 4.x, toàn bộ việc chiếu sáng được thực hiện trong lượt vẽ thông thường. Nói cách khác, Godot không còn vẽ lại đối tượng cho từng light nữa.

Sử dụng chế độ kết xuất ``unshaded`` nếu bạn không muốn hàm ``light()`` chạy. Sử dụng chế độ kết xuất ``light_only`` nếu bạn chỉ muốn thấy tác động của ánh sáng lên một đối tượng; điều này hữu ích khi bạn chỉ muốn đối tượng hiển thị tại những nơi nó được ánh sáng phủ lên.

Nếu bạn định nghĩa một hàm ``light()``, hàm đó sẽ thay thế hàm light built-in, ngay cả khi hàm light của bạn rỗng.

Dưới đây là một ví dụ về light shader có tính đến normal map của CanvasItem:

.. code-block:: glsl

  void light() {
    float cNdotL = max(0.0, dot(NORMAL, LIGHT_DIRECTION));
    LIGHT = vec4(LIGHT_COLOR.rgb * COLOR.rgb * LIGHT_ENERGY * cNdotL, LIGHT_COLOR.a);
  }

+----------------------------------+------------------------------------------------------------------------------+
| Built-in                         | Description                                                                  |
+==================================+==============================================================================+
| in vec4 **FRAGCOORD**            | Coordinate of pixel center. In screen space. ``xy`` specifies                |
|                                  | position in viewport. Upper-left of the viewport is the origin,              |
|                                  | ``(0.0, 0.0)``. Bottom-right of the viewport is ``(1.0, 1.0)``.              |
+----------------------------------+------------------------------------------------------------------------------+
| in vec3 **NORMAL**               | Input normal.                                                                |
+----------------------------------+------------------------------------------------------------------------------+
| in vec4 **COLOR**                | Input color. This is the output of the ``fragment()`` function.              |
+----------------------------------+------------------------------------------------------------------------------+
| in vec2 **UV**                   | UV from the ``vertex()`` function, equivalent to the UV in the               |
|                                  | ``fragment()`` function.                                                     |
+----------------------------------+------------------------------------------------------------------------------+
| sampler2D **TEXTURE**            | Current texture in use for the CanvasItem.                                   |
+----------------------------------+------------------------------------------------------------------------------+
| in vec2 **TEXTURE_PIXEL_SIZE**   | Normalized pixel size of ``TEXTURE``.                                        |
|                                  | For a Sprite2D with a ``TEXTURE`` of size 64×32 pixels,                      |
|                                  | ``TEXTURE_PIXEL_SIZE`` = ``vec2(1.0 / 64.0, 1.0 / 32.0)``.                   |
+----------------------------------+------------------------------------------------------------------------------+
| in vec2 **SCREEN_UV**            | Screen UV coordinate for the current pixel.                                  |
+----------------------------------+------------------------------------------------------------------------------+
| in vec2 **POINT_COORD**          | UV for Point Sprite.                                                         |
+----------------------------------+------------------------------------------------------------------------------+
| in vec4 **LIGHT_COLOR**          | :ref:`Color<class_Light2D_property_color>` of the :ref:`class_Light2D`.      |
|                                  | If the light is a :ref:`class_PointLight2D`, multiplied by the light's       |
|                                  | :ref:`texture<class_PointLight2D_property_texture>`.                         |
+----------------------------------+------------------------------------------------------------------------------+
| in float **LIGHT_ENERGY**        | :ref:`Energy multiplier<class_Light2D_property_energy>` of the               |
|                                  | :ref:`class_Light2D`.                                                        |
+----------------------------------+------------------------------------------------------------------------------+
| in vec3 **LIGHT_POSITION**       | Position of the :ref:`class_Light2D` in screen space. If using a             |
|                                  | :ref:`class_DirectionalLight2D` this is always ``(0.0, 0.0, 0.0)``.          |
+----------------------------------+------------------------------------------------------------------------------+
| in vec3 **LIGHT_DIRECTION**      | Direction of the :ref:`class_Light2D` in screen space.                       |
+----------------------------------+------------------------------------------------------------------------------+
| in bool **LIGHT_IS_DIRECTIONAL** | ``true`` if this pass is a :ref:`class_DirectionalLight2D`.                  |
+----------------------------------+------------------------------------------------------------------------------+
| in vec3 **LIGHT_VERTEX**         | Pixel position, in screen space as modified in the ``fragment()`` function.  |
+----------------------------------+------------------------------------------------------------------------------+
| inout vec4 **LIGHT**             | Output color for this :ref:`class_Light2D`.                                  |
+----------------------------------+------------------------------------------------------------------------------+
| in vec4 **SPECULAR_SHININESS**   | Specular shininess, as set in the object's texture.                          |
+----------------------------------+------------------------------------------------------------------------------+
| out vec4 **SHADOW_MODULATE**     | Multiply shadows cast at this point by this color.                           |
+----------------------------------+------------------------------------------------------------------------------+

Các hàm SDF
-----------

Có một số hàm bổ sung được triển khai để lấy mẫu texture Signed Distance Field được tự động tạo. Các hàm này khả dụng trong các hàm ``fragment()`` và ``light()`` của shader CanvasItem. Các hàm tùy chỉnh cũng có thể sử dụng chúng miễn là được gọi từ các hàm được hỗ trợ.

Signed Distance Field được tạo từ các node :ref:`class_LightOccluder2D` có trong scene với thuộc tính **SDF Collision** được bật (đây là thiết lập mặc định). Xem tài liệu :ref:`2D lights and shadows <doc_2d_lights_and_shadows_setting_up_shadows>` để biết thêm thông tin.

+-----------------------------------------------+-------------------------------------------+
| Function                                      | Description                               |
+===============================================+===========================================+
| float **texture_sdf** (vec2 sdf_pos)          | Performs an SDF texture lookup.           |
+-----------------------------------------------+-------------------------------------------+
| vec2 **texture_sdf_normal** (vec2 sdf_pos)    | Calculates a normal from the SDF texture. |
+-----------------------------------------------+-------------------------------------------+
| vec2 **sdf_to_screen_uv** (vec2 sdf_pos)      | Converts an SDF to screen UV.             |
+-----------------------------------------------+-------------------------------------------+
| vec2 **screen_uv_to_sdf** (vec2 uv)           | Converts screen UV to an SDF.             |
+-----------------------------------------------+-------------------------------------------+
