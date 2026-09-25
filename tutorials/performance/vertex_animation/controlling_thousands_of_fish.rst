:article_outdated: Đúng

.. _doc_controlling_thousands_of_fish:

Điều khiển hàng nghìn con cá bằng Particles
===========================================

Vấn đề với :ref:`MeshInstance3D <class_MeshInstance3D>` là chi phí cập nhật mảng transform của chúng rất cao. Nó rất phù hợp để đặt nhiều đối tượng tĩnh xung quanh cảnh. Tuy nhiên, việc di chuyển các đối tượng xung quanh cảnh vẫn rất khó.

Để làm cho mỗi instance di chuyển theo một cách thú vị, chúng ta sẽ sử dụng một
node :ref:`GPUParticles3D <class_GPUParticles3D>`. Particles tận dụng khả năng tăng tốc GPU bằng cách tính toán và thiết lập thông tin cho từng instance trong một :ref:`Shader <class_Shader>`.

Trước tiên, hãy tạo một node Particles. Sau đó, trong "Draw Passes", đặt "Draw Pass 1" của Particle thành
:ref:`Mesh <class_Mesh>` của bạn. Tiếp theo, trong "Process Material", hãy tạo một
:ref:`ShaderMaterial <class_ShaderMaterial>`.

Đặt ``shader_type`` thành ``particles``.

.. code-block:: glsl

  shader_type particles

Sau đó, thêm hai hàm sau:

.. code-block:: glsl

  float rand_from_seed(in uint seed) {
    int k;
    int s = int(seed);
    if (s == 0)
      s = 305420679;
    k = s / 127773;
    s = 16807 * (s - k * 127773) - 2836 * k;
    if (s < 0)
      s += 2147483647;
    seed = uint(s);
    return float(seed % uint(65536)) / 65535.0;
  }

  uint hash(uint x) {
    x = ((x >> uint(16)) ^ x) * uint(73244475);
    x = ((x >> uint(16)) ^ x) * uint(73244475);
    x = (x >> uint(16)) ^ x;
    return x;
  }

Các hàm này đến từ :ref:`ParticleProcessMaterial <class_ParticleProcessMaterial>` mặc định. Chúng được dùng để tạo một số ngẫu nhiên từ ``RANDOM_SEED`` của mỗi particle.

Một điểm đặc biệt của particle shader là một số biến tích hợp được lưu lại qua các frame. ``TRANSFORM``, ``COLOR`` và ``CUSTOM`` đều có thể được truy cập trong shader của mesh, cũng như trong particle shader ở lần chạy tiếp theo.

Tiếp theo, hãy thiết lập hàm ``start()``. Particle shader chứa một hàm ``start()`` và một hàm ``process()``.

Mã trong hàm ``start()`` chỉ chạy khi hệ thống particle khởi động. Mã trong hàm ``process()`` sẽ luôn chạy.

Chúng ta cần tạo 4 số ngẫu nhiên: 3 số để tạo một vị trí ngẫu nhiên và 1 số cho độ lệch ngẫu nhiên của chu kỳ bơi.

Trước tiên, hãy tạo 4 seed bên trong hàm ``start()`` bằng hàm ``hash()`` được cung cấp ở trên:

.. code-block:: glsl

  uint alt_seed1 = hash(NUMBER + uint(1) + RANDOM_SEED);
  uint alt_seed2 = hash(NUMBER + uint(27) + RANDOM_SEED);
  uint alt_seed3 = hash(NUMBER + uint(43) + RANDOM_SEED);
  uint alt_seed4 = hash(NUMBER + uint(111) + RANDOM_SEED);

Sau đó, dùng các seed đó để tạo các số ngẫu nhiên bằng ``rand_from_seed``:

.. code-block:: glsl

  CUSTOM.x = rand_from_seed(alt_seed1);
  vec3 position = vec3(rand_from_seed(alt_seed2) * 2.0 - 1.0,
                       rand_from_seed(alt_seed3) * 2.0 - 1.0,
                       rand_from_seed(alt_seed4) * 2.0 - 1.0);

Cuối cùng, gán ``position`` cho ``TRANSFORM[3].xyz``, là phần của transform chứa thông tin vị trí.

.. code-block:: glsl

  TRANSFORM[3].xyz = position * 20.0;

Hãy nhớ rằng toàn bộ mã cho đến lúc này đều nằm bên trong hàm ``start()``.

Vertex shader cho mesh của bạn có thể giữ nguyên hoàn toàn như trong tutorial trước.

Bây giờ bạn có thể di chuyển từng con cá riêng lẻ trong mỗi frame, bằng cách cộng trực tiếp vào ``TRANSFORM`` hoặc ghi vào ``VELOCITY``.

Hãy biến đổi các con cá bằng cách thiết lập ``VELOCITY`` của chúng trong hàm ``start()``.

.. code-block:: glsl

  VELOCITY.z = 10.0;

Đây là cách cơ bản nhất để thiết lập ``VELOCITY``; mọi particle (hoặc cá) sẽ có cùng vận tốc.

Chỉ bằng cách thiết lập ``VELOCITY``, bạn có thể khiến cá bơi theo bất kỳ cách nào mình muốn. Ví dụ, hãy thử đoạn mã dưới đây.

.. code-block:: glsl

  VELOCITY.z = cos(TIME + CUSTOM.x * 6.28) * 4.0 + 6.0;

Điều này sẽ tạo cho mỗi con cá một tốc độ riêng trong khoảng từ ``2`` đến ``10``.

Bạn cũng có thể cho phép mỗi con cá thay đổi vận tốc theo thời gian nếu thiết lập vận tốc trong hàm ``process()``.

Nếu bạn đã sử dụng ``CUSTOM.y`` trong tutorial trước, bạn cũng có thể thiết lập tốc độ của animation bơi dựa trên ``VELOCITY``. Chỉ cần sử dụng ``CUSTOM.y``.

.. code-block:: glsl

  CUSTOM.y = VELOCITY.z * 0.1;

Đoạn mã này sẽ tạo ra hành vi sau:

.. image:: img/scene.gif

Bằng cách sử dụng ParticleProcessMaterial, bạn có thể làm cho hành vi của cá đơn giản hoặc phức tạp tùy ý. Trong tutorial này, chúng ta chỉ thiết lập Velocity, nhưng trong Shaders của riêng mình, bạn cũng có thể thiết lập ``COLOR``, rotation và scale (thông qua ``TRANSFORM``). Vui lòng tham khảo :ref:`Particles Shader Reference <doc_particle_shader>` để biết thêm thông tin về particle shader.
