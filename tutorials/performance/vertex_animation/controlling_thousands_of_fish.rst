:article_outdated: True

.. _doc_controlling_thousands_of_fish:

Điều khiển hàng nghìn con cá bằng Particles
===========================================

Vấn đề với :ref:`MeshInstance3D <class_MeshInstance3D>` là việc cập nhật mảng transform của chúng rất tốn kém. Nó rất phù hợp để đặt nhiều đối tượng tĩnh xung quanh scene. Nhưng việc di chuyển các đối tượng quanh scene vẫn rất khó.

Để khiến mỗi instance di chuyển theo một cách thú vị, chúng ta sẽ sử dụng một
:ref:`GPUParticles3D <class_GPUParticles3D>` node. Particles take advantage of GPU acceleration
bằng cách tính toán và thiết lập thông tin trên từng instance trong một :ref:`Shader <class_Shader>`.

Trước tiên, hãy tạo một node Particles. Sau đó, trong "Draw Passes", đặt "Draw Pass 1" của Particle thành
:ref:`Mesh <class_Mesh>`. Then under "Process Material" create a new
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

Một điểm đặc biệt của particle shader là một số biến tích hợp được lưu lại giữa các frame. ``TRANSFORM``, ``COLOR`` và ``CUSTOM`` đều có thể được truy cập trong shader của mesh, cũng như trong particle shader vào lần chạy tiếp theo.

Tiếp theo, hãy thiết lập hàm ``start()``. Particle shader chứa một hàm ``start()`` và một hàm ``process()``.

Code trong hàm ``start()`` chỉ chạy khi particle system khởi động. Code trong hàm ``process()`` sẽ luôn chạy.

Chúng ta cần tạo 4 số ngẫu nhiên: 3 số để tạo một vị trí ngẫu nhiên và 1 số cho độ lệch ngẫu nhiên của chu kỳ bơi.

Trước tiên, hãy tạo 4 seed bên trong hàm ``start()`` bằng hàm ``hash()`` được cung cấp ở trên:

.. code-block:: glsl

  uint alt_seed1 = hash(NUMBER + uint(1) + RANDOM_SEED);
  uint alt_seed2 = hash(NUMBER + uint(27) + RANDOM_SEED);
  uint alt_seed3 = hash(NUMBER + uint(43) + RANDOM_SEED);
  uint alt_seed4 = hash(NUMBER + uint(111) + RANDOM_SEED);

Sau đó, dùng các seed đó để tạo số ngẫu nhiên bằng ``rand_from_seed``:

.. code-block:: glsl

  CUSTOM.x = rand_from_seed(alt_seed1);
  vec3 position = vec3(rand_from_seed(alt_seed2) * 2.0 - 1.0,
                       rand_from_seed(alt_seed3) * 2.0 - 1.0,
                       rand_from_seed(alt_seed4) * 2.0 - 1.0);

Cuối cùng, gán ``position`` cho ``TRANSFORM[3].xyz``, là phần của transform chứa thông tin vị trí.

.. code-block:: glsl

  TRANSFORM[3].xyz = position * 20.0;

Hãy nhớ rằng toàn bộ code cho đến thời điểm này đều nằm bên trong hàm ``start()``.

Vertex shader cho mesh của bạn có thể giữ nguyên hoàn toàn như trong tutorial trước.

Bây giờ bạn có thể di chuyển từng con cá riêng lẻ trong mỗi frame, bằng cách cộng trực tiếp vào ``TRANSFORM`` hoặc ghi vào ``VELOCITY``.

Hãy biến đổi những con cá bằng cách thiết lập ``VELOCITY`` của chúng trong hàm ``start()``.

.. code-block:: glsl

  VELOCITY.z = 10.0;

Đây là cách cơ bản nhất để thiết lập ``VELOCITY``: mọi particle (hoặc cá) sẽ có cùng vận tốc.

Chỉ cần thiết lập ``VELOCITY``, bạn có thể khiến cá bơi theo bất kỳ cách nào mình muốn. Ví dụ, hãy thử đoạn code dưới đây.

.. code-block:: glsl

  VELOCITY.z = cos(TIME + CUSTOM.x * 6.28) * 4.0 + 6.0;

Điều này sẽ tạo cho mỗi con cá một tốc độ riêng trong khoảng từ ``2`` đến ``10``.

Bạn cũng có thể cho phép mỗi con cá thay đổi vận tốc theo thời gian nếu thiết lập vận tốc trong hàm ``process()``.

Nếu bạn đã sử dụng ``CUSTOM.y`` trong tutorial trước, bạn cũng có thể thiết lập tốc độ của animation bơi dựa trên ``VELOCITY``. Chỉ cần sử dụng ``CUSTOM.y``.

.. code-block:: glsl

  CUSTOM.y = VELOCITY.z * 0.1;

Đoạn code này sẽ tạo ra hành vi sau:

.. image:: img/scene.gif

Bằng cách sử dụng ParticleProcessMaterial, bạn có thể khiến hành vi của cá đơn giản hoặc phức tạp tùy ý. Trong tutorial này, chúng ta chỉ thiết lập Velocity, nhưng trong các Shader của riêng mình, bạn cũng có thể thiết lập ``COLOR``, rotation, scale (thông qua ``TRANSFORM``). Vui lòng tham khảo :ref:`Particles Shader Reference <doc_particle_shader>` để biết thêm thông tin về particle shader.
