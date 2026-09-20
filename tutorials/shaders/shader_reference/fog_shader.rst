.. _doc_fog_shader:

Shader sương mù
===============

Shader sương mù được dùng để xác định cách sương mù được thêm vào (hoặc loại bỏ khỏi) một cảnh trong một khu vực nhất định. Shader sương mù luôn được sử dụng cùng với
:ref:`FogVolumes <class_FogVolume>` and volumetric fog. Fog shaders only have
một hàm xử lý, hàm ``fog()``.

Độ phân giải của shader sương mù phụ thuộc vào độ phân giải của lưới froxel của sương mù thể tích. Theo đó, mức độ chi tiết mà một shader sương mù có thể thêm vào phụ thuộc vào khoảng cách từ :ref:`FogVolume <class_FogVolume>` đến camera.

Shader sương mù là một dạng đặc biệt của compute shader, được gọi một lần cho mỗi froxel bị chạm bởi một bounding box căn chỉnh theo trục của đối tượng liên kết
:ref:`FogVolume <class_FogVolume>`. This means that froxels that just barely
các :ref:`FogVolume <class_FogVolume>` nhất định chạm tới vẫn sẽ được sử dụng.

Built-in
--------

Các giá trị được đánh dấu là ``in`` chỉ được đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết phải chứa các giá trị hợp lý. Sampler không thể được ghi nên không được đánh dấu.

Built-in toàn cục
-----------------

Built-in toàn cục có sẵn ở mọi nơi, bao gồm cả trong các hàm tùy chỉnh.

+-----------------------------------+-------------------------------------------------------------------------------------------------+
| Built-in                          | Description                                                                                     |
+===================================+=================================================================================================+
| in float **TIME**                 | Global time since the engine has started, in seconds. It repeats after every ``3,600``          |
|                                   | seconds (which can be changed with the                                                          |
|                                   | :ref:`rollover<class_ProjectSettings_property_rendering/limits/time/time_rollover_secs>`        |
|                                   | setting). It's affected by                                                                      |
|                                   | :ref:`time_scale<class_Engine_property_time_scale>` but not by pausing. If you need a           |
|                                   | ``TIME`` variable that is not affected by time scale, add your own                              |
|                                   | :ref:`global shader uniform<doc_shading_language_global_uniforms>` and update it each           |
|                                   | frame.                                                                                          |
+-----------------------------------+-------------------------------------------------------------------------------------------------+
| in float **PI**                   | A ``PI`` constant (``3.141592``).                                                               |
|                                   | The ratio of a circle's circumference to its diameter and the number of radians in a half turn. |
+-----------------------------------+-------------------------------------------------------------------------------------------------+
| in float **TAU**                  | A ``TAU`` constant (``6.283185``).                                                              |
|                                   | Equivalent to ``PI * 2`` and the number of radians in a full turn.                              |
+-----------------------------------+-------------------------------------------------------------------------------------------------+
| in float **E**                    | An ``E`` constant (``2.718281``).                                                               |
|                                   | Euler's number, the base of the natural logarithm.                                              |
+-----------------------------------+-------------------------------------------------------------------------------------------------+

Built-in của sương mù
---------------------

Tất cả các giá trị đầu ra của các volume sương mù chồng lên nhau. Điều này cho phép
:ref:`FogVolumes <class_FogVolume>` to be rendered efficiently as they can all
được vẽ cùng một lúc.

+-------------------------------+-------------------------------------------------------------------------------------------------+
| Built-in                      | Description                                                                                     |
+===============================+=================================================================================================+
| in vec3 **WORLD_POSITION**    | Position of current froxel cell in world space.                                                 |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| in vec3 **OBJECT_POSITION**   | Position of the center of the current :ref:`FogVolume <class_FogVolume>` in world space.        |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| in vec3 **UVW**               | 3-dimensional UV, used to map a 3D texture to the current :ref:`FogVolume <class_FogVolume>`.   |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| in vec3 **SIZE**              | Size of the current :ref:`FogVolume <class_FogVolume>` when its                                 |
|                               | :ref:`shape<class_FogVolume_property_shape>` has a size.                                        |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| in vec3 **SDF**               | Signed distance field to the surface of the :ref:`FogVolume <class_FogVolume>`. Negative if     |
|                               | inside volume, positive otherwise.                                                              |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| out vec3 **ALBEDO**           | Output base color value, interacts with light to produce final color. Only written to fog       |
|                               | volume if used.                                                                                 |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| out float **DENSITY**         | Output density value. Can be negative to allow subtracting one volume from another. Density     |
|                               | must be used for fog shader to write anything at all.                                           |
+-------------------------------+-------------------------------------------------------------------------------------------------+
| out vec3 **EMISSION**         | Output emission color value, added to color during light pass to produce final color. Only      |
|                               | written to fog volume if used.                                                                  |
+-------------------------------+-------------------------------------------------------------------------------------------------+
