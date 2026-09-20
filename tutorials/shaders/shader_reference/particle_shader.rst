.. _doc_particle_shader:

Particle shader
===============

Particle shader là một loại shader đặc biệt chạy trước khi đối tượng được vẽ. Chúng được dùng để tính toán các thuộc tính của material như màu sắc, vị trí và góc xoay. Chúng có thể được vẽ bằng bất kỳ material thông thường nào cho CanvasItem hoặc Spatial, tùy thuộc vào việc chúng là 2D hay 3D.

Particle shader có tính đặc thù vì chúng không được dùng để vẽ chính đối tượng; chúng được dùng để tính toán các thuộc tính của particle, sau đó được sử dụng bởi một
:ref:`CanvasItem<doc_canvas_item_shader>` or :ref:`Spatial<doc_spatial_shader>`
shader. Chúng chứa hai hàm processor: ``start()`` và ``process()``.

Không giống các loại shader khác, particle shader giữ lại dữ liệu được xuất ra ở frame trước đó. Vì vậy, particle shader có thể được dùng cho các hiệu ứng phức tạp diễn ra trong nhiều frame.

.. note::

    Particle shader chỉ khả dụng với các node particle dựa trên GPU (:ref:`class_GPUParticles2D` và :ref:`class_GPUParticles3D`).

    Các node particle dựa trên CPU (:ref:`class_CPUParticles2D` và
    :ref:`class_CPUParticles3D`) are *rendered* on the GPU (which means they can
    sử dụng shader CanvasItem hoặc Spatial tùy chỉnh), nhưng chuyển động của chúng được *mô phỏng* trên CPU.

Render mode
-----------

+--------------------------+-------------------------------------------+
| Render mode              | Description                               |
+==========================+===========================================+
| **keep_data**            | Do not clear previous data on restart.    |
+--------------------------+-------------------------------------------+
| **disable_force**        | Disable attractor force.                  |
+--------------------------+-------------------------------------------+
| **disable_velocity**     | Ignore ``VELOCITY`` value.                |
+--------------------------+-------------------------------------------+
| **collision_use_scale**  | Scale the particle's size for collisions. |
+--------------------------+-------------------------------------------+

Built-in
--------

Các giá trị được đánh dấu là ``in`` chỉ được đọc. Các giá trị được đánh dấu là ``out`` có thể được ghi tùy chọn và không nhất thiết chứa các giá trị hợp lệ. Các giá trị được đánh dấu là ``inout`` cung cấp một giá trị mặc định hợp lệ và có thể được ghi tùy chọn. Sampler không thể được ghi nên không được đánh dấu.

Global built-in
---------------

Global built-in khả dụng ở mọi nơi, bao gồm cả các hàm tùy chỉnh.

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
| in float **E**    | An ``E`` constant (``2.718281``). Euler's number, the base of the natural logarithm.            |
+-------------------+-------------------------------------------------------------------------------------------------+

Built-in của Start và Process
-----------------------------

Các thuộc tính này có thể được truy cập từ cả hai hàm ``start()`` và ``process()``.

+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| Function                           | Description                                                                                                                             |
+====================================+=========================================================================================================================================+
| in float **LIFETIME**              | Particle lifetime.                                                                                                                      |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in float **DELTA**                 | Delta process time.                                                                                                                     |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **NUMBER**                 | Unique number since emission start.                                                                                                     |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **INDEX**                  | Particle index (from total particles).                                                                                                  |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in mat4 **EMISSION_TRANSFORM**     | Emitter transform (used for non-local systems).                                                                                         |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **RANDOM_SEED**            | Random seed used as base for random.                                                                                                    |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| inout bool **ACTIVE**              | ``true`` when the particle is active, can be set to ``false``.                                                                          |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| inout vec4 **COLOR**               | Particle color, can be written to and accessed in the mesh's vertex function.                                                           |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| inout vec3 **VELOCITY**            | Particle velocity, can be modified.                                                                                                     |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| inout mat4 **TRANSFORM**           | Particle transform.                                                                                                                     |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| inout vec4 **CUSTOM**              | Custom particle data. Accessible from the mesh's shader as ``INSTANCE_CUSTOM``.                                                         |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| inout float **MASS**               | Particle mass, intended to be used with attractors. ``1.0`` by default.                                                                 |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in vec4 **USERDATAX**              | Vector that enables the integration of supplementary user-defined data into the particle process shader.                                |
|                                    | ``USERDATAX`` are six built-ins identified by number, ``X`` can be numbers between 1 and 6, for example ``USERDATA3``.                  |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **FLAG_EMIT_POSITION**     | A flag for the last argument of the ``emit_subparticle()`` function to assign a position to a new particle's transform.                 |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **FLAG_EMIT_ROT_SCALE**    | A flag for the last argument of the ``emit_subparticle()`` function to assign a rotation and scale to a new particle's transform.       |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **FLAG_EMIT_VELOCITY**     | A flag for the last argument of the ``emit_subparticle()`` function to assign a velocity to a new particle.                             |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **FLAG_EMIT_COLOR**        | A flag for the last argument of the ``emit_subparticle()`` function to assign a color to a new particle.                                |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **FLAG_EMIT_CUSTOM**       | A flag for the last argument of the ``emit_subparticle()`` function to assign a custom data vector to a new particle.                   |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in vec3 **EMITTER_VELOCITY**       | Velocity of the :ref:`Particles2D<class_GPUParticles2D>` (:ref:`3D<class_GPUParticles3D>`) node.                                        |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in float **INTERPOLATE_TO_END**    | Value of the :ref:`interp_to_end<class_GPUParticles2D_property_interp_to_end>`                                                          |
|                                    | (:ref:`3D<class_GPUParticles3D_property_interp_to_end>`) property of the Particles node.                                                |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+
| in uint **AMOUNT_RATIO**           | Value of the :ref:`amount_ratio<class_GPUParticles2D_property_amount_ratio>`                                                            |
|                                    | (:ref:`3D<class_GPUParticles3D_property_amount_ratio>`) property of the Particles node.                                                 |
+------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------+

.. note:: In order to use the ``COLOR`` variable in a StandardMaterial3D, set ``vertex_color_use_as_albedo``
          đến ``true``. Trong một ShaderMaterial, hãy truy cập nó bằng biến ``COLOR``.

Built-in của Start
------------------

+---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Built-in                        | Description                                                                                                                                                                           |
+=================================+=======================================================================================================================================================================================+
| in bool **RESTART_POSITION**    | ``true`` if particle is restarted, or emitted without a custom position (i.e. this particle was created by ``emit_subparticle()`` without the ``FLAG_EMIT_POSITION`` flag).           |
+---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **RESTART_ROT_SCALE**   | ``true`` if particle is restarted, or emitted without a custom rotation or scale (i.e. this particle was created by ``emit_subparticle()`` without the ``FLAG_EMIT_ROT_SCALE`` flag). |
+---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **RESTART_VELOCITY**    | ``true`` if particle is restarted, or emitted without a custom velocity (i.e. this particle was created by ``emit_subparticle()`` without the ``FLAG_EMIT_VELOCITY`` flag).           |
+---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **RESTART_COLOR**       | ``true`` if particle is restarted, or emitted without a custom color (i.e. this particle was created by ``emit_subparticle()`` without the ``FLAG_EMIT_COLOR`` flag).                 |
+---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| in bool **RESTART_CUSTOM**      | ``true`` if particle is restarted, or emitted without a custom property (i.e. this particle was created by ``emit_subparticle()`` without the ``FLAG_EMIT_CUSTOM`` flag).             |
+---------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Built-in của Process
--------------------

+------------------------------------+---------------------------------------------------------------------------------------------------------+
| Built-in                           | Description                                                                                             |
+====================================+=========================================================================================================+
| in bool **RESTART**                | ``true`` if the current process frame is the first for the particle.                                    |
+------------------------------------+---------------------------------------------------------------------------------------------------------+
| in bool **COLLIDED**               | ``true`` when the particle has collided with a particle collider.                                       |
+------------------------------------+---------------------------------------------------------------------------------------------------------+
| in vec3 **COLLISION_NORMAL**       | A normal of the last collision. If there is no collision detected it is equal to ``(0.0, 0.0, 0.0)``.   |
+------------------------------------+---------------------------------------------------------------------------------------------------------+
| in float **COLLISION_DEPTH**       | A length of the normal of the last collision. If there is no collision detected it is equal to ``0.0``. |
+------------------------------------+---------------------------------------------------------------------------------------------------------+
| in vec3 **ATTRACTOR_FORCE**        | A combined force of the attractors at the moment on that particle.                                      |
+------------------------------------+---------------------------------------------------------------------------------------------------------+

Hàm Process
-----------

``emit_subparticle()`` hiện là hàm tùy chỉnh duy nhất được particle shader hỗ trợ. Hàm này cho phép người dùng thêm một particle mới với các tham số được chỉ định từ một sub-emitter. Particle mới được tạo sẽ chỉ sử dụng các thuộc tính khớp với tham số ``flags``. Ví dụ: đoạn mã sau sẽ phát ra một particle với vị trí, vận tốc và màu được chỉ định, nhưng không chỉ định góc xoay, tỉ lệ và giá trị tùy chỉnh:

.. code-block:: glsl

    mat4 custom_transform = mat4(1.0);
    custom_transform[3].xyz = vec3(10.5, 0.0, 4.0);
    emit_subparticle(custom_transform, vec3(1.0, 0.5, 1.0), vec4(1.0, 0.0, 0.0, 1.0), vec4(1.0), FLAG_EMIT_POSITION | FLAG_EMIT_VELOCITY | FLAG_EMIT_COLOR);

+--------------------------------------------------------------------------------------------+--------------------------------------+
| Function                                                                                   | Description                          |
+============================================================================================+======================================+
| bool **emit_subparticle** (mat4 xform, vec3 velocity, vec4 color, vec4 custom, uint flags) | Emits a particle from a sub-emitter. |
+--------------------------------------------------------------------------------------------+--------------------------------------+
