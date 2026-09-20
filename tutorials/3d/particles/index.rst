:allow_comments: False

.. _doc_3d_particles:

Hệ thống particle (3D)
======================

Phần này của tutorial trình bày về các hệ thống particle (3D) được tăng tốc bằng GPU. Hầu hết những nội dung được thảo luận ở đây cũng áp dụng cho particle CPU.

.. rubric:: Introduction
   :heading-level: 2

Bạn có thể sử dụng hệ thống particle để mô phỏng các hiệu ứng vật lý phức tạp như lửa, tia lửa, khói, hiệu ứng ma thuật và nhiều hiệu ứng khác. Chúng đặc biệt phù hợp để tạo ra hành vi năng động, tự nhiên và thêm "sức sống" vào các scene của bạn.

Ý tưởng là một particle được phát ra theo một khoảng thời gian cố định và có lifetime cố định. Trong suốt lifetime của nó, mọi particle sẽ có cùng hành vi cơ bản. Điều khiến mỗi particle khác biệt với những particle khác và tạo ra vẻ tự nhiên là tính ngẫu nhiên mà bạn có thể thêm vào hầu hết các tham số và hành vi của nó.

Mỗi hệ thống particle bạn tạo trong Godot gồm hai phần chính: particle và emitter.

.. rubric:: Particles
   :heading-level: 3

Particle là phần hiển thị của một hệ thống particle. Đó là những gì bạn nhìn thấy trên màn hình khi một hệ thống particle đang hoạt động: những hạt bụi nhỏ li ti, ngọn lửa, những quả cầu phát sáng của một hiệu ứng ma thuật. Một hệ thống có thể có từ vài trăm đến hàng chục nghìn particle. Bạn có thể ngẫu nhiên hóa kích thước, tốc độ và hướng chuyển động của particle, đồng thời thay đổi màu của nó trong suốt lifetime. Khi nghĩ về một ngọn lửa, bạn có thể hình dung tất cả những đốm than nhỏ bay ra từ đó như các particle riêng lẻ.

.. rubric:: Emitters
   :heading-level: 3

Emitter là thành phần tạo ra các particle. Emitter thường không hiển thị, nhưng có thể có một hình dạng. Hình dạng đó kiểm soát vị trí và cách các particle được spawn, chẳng hạn chúng sẽ lấp đầy một căn phòng như bụi hay bắn ra từ một điểm duy nhất như đài phun nước. Quay lại ví dụ về ngọn lửa, emitter sẽ là phần nhiệt ở trung tâm ngọn lửa, tạo ra các đốm than và ngọn lửa.

.. rubric:: Node overview
   :heading-level: 3

.. figure:: img/particle_nodes.webp
   :alt: A list of nodes related to 3D particles
   :align: right

   All 3D particle nodes available in Godot

Có hai loại hệ thống particle 3D trong Godot: :ref:`class_GPUParticles3D`, được xử lý trên GPU, và :ref:`class_CPUParticles3D`, được xử lý trên CPU.

Hệ thống particle CPU kém linh hoạt hơn so với phiên bản GPU tương ứng, nhưng hoạt động trên nhiều loại hardware hơn và hỗ trợ tốt hơn cho các thiết bị cũ cũng như điện thoại di động. Vì được xử lý trên CPU nên chúng không có hiệu năng tốt bằng hệ thống particle GPU và không thể render nhiều particle riêng lẻ như vậy. Ngoài ra, hiện tại chúng chưa có đầy đủ các tùy chọn điều khiển mà particle GPU cung cấp.

Hệ thống particle GPU chạy trên GPU và có thể render hàng trăm nghìn particle trên hardware hiện đại. Bạn có thể viết các particle shader tùy chỉnh cho chúng, nhờ đó chúng rất linh hoạt. Bạn cũng có thể khiến chúng tương tác với môi trường bằng cách sử dụng các node attractor và collision.

Có ba node particle attractor: :ref:`class_GPUParticlesAttractorBox3D`, :ref:`class_GPUParticlesAttractorSphere3D` và :ref:`class_GPUParticlesAttractorVectorField3D`. Một node attractor tác dụng một lực lên tất cả particle trong phạm vi ảnh hưởng của nó, kéo chúng lại gần hoặc đẩy chúng ra xa dựa trên hướng của lực đó.

Có một số node particle collision. :ref:`class_GPUParticlesCollisionBox3D` và
:ref:`class_GPUParticlesCollisionSphere3D` are the simple ones. You can use them to create basic
các hình dạng như box, floor hoặc wall mà particle va chạm vào. Hai node còn lại cung cấp hành vi collision phức tạp hơn. :ref:`class_GPUParticlesCollisionSDF3D` hữu ích khi bạn muốn các scene trong nhà va chạm với particle mà không phải tự tạo tất cả collider box và sphere riêng lẻ. Nếu muốn particle va chạm với các scene ngoài trời lớn, bạn sẽ sử dụng
:ref:`class_GPUParticlesCollisionHeightField3D` node. It creates a heightmap of your world and the
các object trong đó và dùng chúng cho các collision particle quy mô lớn.


.. rubric:: Basic usage
   :heading-level: 2

.. toctree::
   :maxdepth: 1
   :name: toc-particles-basic

   creating_a_3d_particle_system
   properties
   process_material_properties

.. rubric:: Advanced topics
   :heading-level: 2

.. toctree::
   :maxdepth: 1
   :name: toc-particles-advanced

   subemitters
   trails
   turbulence
   attractors
   collision
   complex_shapes
