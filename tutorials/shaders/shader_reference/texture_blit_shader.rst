.. _doc_texture_blit_shader:

Shader blit texture
===================

Shader blit texture được sử dụng để xác định hành vi của các lệnh gọi blit trên một
:ref:`DrawableTexture2D <doc_drawable_textures>`.

Shader blit texture chỉ có một hàm xử lý là hàm ``blit()``, hàm này chạy cho mọi pixel của texture nguồn nằm trong hình chữ nhật được truyền cho ``blit_rect()``.

.. seealso::

    Xem :ref:`doc_drawable_textures` để biết thêm thông tin về cách sử dụng shader blit texture như một phần của DrawableTexture.

Chế độ render
-------------

+---------------------------------+-------------------------------------------------------------------------+
| Render mode                     | Description                                                             |
+=================================+=========================================================================+
| **blend_disabled**              | Disable blending, values (including alpha) are written as-is. Default.  |
+---------------------------------+-------------------------------------------------------------------------+
| **blend_mix**                   | Mix blend mode (alpha is transparency).                                 |
+---------------------------------+-------------------------------------------------------------------------+
| **blend_add**                   | Additive blend mode.                                                    |
+---------------------------------+-------------------------------------------------------------------------+
| **blend_sub**                   | Subtractive blend mode.                                                 |
+---------------------------------+-------------------------------------------------------------------------+
| **blend_mul**                   | Multiplicative blend mode.                                              |
+---------------------------------+-------------------------------------------------------------------------+

.. note::

    Không có chế độ trộn alpha premultiplied dành cho shader blit texture.

Các built-in
------------

Các giá trị được đánh dấu là ``in`` chỉ có thể đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết chứa các giá trị hợp lý. Các giá trị được đánh dấu là ``inout`` cung cấp một giá trị mặc định hợp lý và có thể được ghi tùy chọn. Sampler không thể được ghi nên không được đánh dấu.

Các built-in toàn cục
---------------------

Các built-in toàn cục có sẵn ở mọi nơi, bao gồm cả các hàm tùy chỉnh.

+-------------------+------------------------------------------------------------------------------------------+
| Built-in          | Description                                                                              |
+===================+==========================================================================================+
| in float **TIME** | Global time since the engine has started, in seconds. It repeats after every ``3,600``   |
|                   | seconds (which can be changed with the                                                   |
|                   | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>` |
|                   | setting). It's affected by                                                               |
|                   | :ref:`time_scale<class_Engine_property_time_scale>` but not by pausing. If you need a    |
|                   | ``TIME`` variable that is not affected by time scale, add your own                       |
|                   | :ref:`global shader uniform<doc_shading_language_global_uniforms>` and update it each    |
|                   | frame.                                                                                   |
+-------------------+------------------------------------------------------------------------------------------+
| in float **PI**   | A ``PI`` constant (``3.141592``).                                                        |
|                   | The ratio of a circle's circumference to its diameter and the number of radians in a     |
|                   | half turn.                                                                               |
+-------------------+------------------------------------------------------------------------------------------+
| in float **TAU**  | A ``TAU`` constant (``6.283185``).                                                       |
|                   | An equivalent of ``PI * 2`` and amount of radians in full turn.                          |
+-------------------+------------------------------------------------------------------------------------------+
| in float **E**    | An ``E`` constant (``2.718281``).                                                        |
|                   | Euler's number and a base of the natural logarithm.                                      |
+-------------------+------------------------------------------------------------------------------------------+


Các built-in của blit
---------------------

Texture nguồn
~~~~~~~~~~~~~

Shader blit texture có tối đa 4 texture nguồn được liên kết làm đầu vào. Có thể truy cập các texture này bằng một ``sampler2D`` sử dụng ``hint_blit_source0``, ``hint_blit_source1``, ``hint_blit_source2`` và ``hint_blit_source3``.

+---------------------------------------------+---------------------------------------------------------------+
| Built-in                                    | Description                                                   |
+=============================================+===============================================================+
| in vec4 **FRAGCOORD**                       | Coordinate of pixel center. In screen space. ``xy`` specifies |
|                                             | position in viewport. Upper-left of the viewport is the       |
|                                             | origin, ``(0.0, 0.0)``.                                       |
+---------------------------------------------+---------------------------------------------------------------+
| in vec2 **UV**                              | UV from the ``vertex()`` function.                            |
|                                             | This is set to sample all of a source texture.                |
+---------------------------------------------+---------------------------------------------------------------+
| in vec4 **MODULATE**                        | ``MODULATE`` color passed in by RenderingServer API.          |
+---------------------------------------------+---------------------------------------------------------------+
| out vec4 **COLOR0**                         | Output color to blended with the DrawableTexture target.      |
|                                             | Initialized to ``(0.0, 0.0, 0.0, 0.0)``.                      |
+---------------------------------------------+---------------------------------------------------------------+
| out vec4 **COLOR1**                         | Output color to blended with an extra DrawableTexture target. |
|                                             | Initialized to ``(0.0, 0.0, 0.0, 0.0)``.                      |
+---------------------------------------------+---------------------------------------------------------------+
| out vec4 **COLOR2**                         | Output color to blended with an extra DrawableTexture target. |
|                                             | Initialized to ``(0.0, 0.0, 0.0, 0.0)``.                      |
+---------------------------------------------+---------------------------------------------------------------+
| out vec4 **COLOR3**                         | Output color to blended with an extra DrawableTexture target. |
|                                             | Initialized to ``(0.0, 0.0, 0.0, 0.0)``.                      |
+---------------------------------------------+---------------------------------------------------------------+
