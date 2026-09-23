:allow_comments: False

.. _doc_3d_particles:

Hệ thống hạt (3D)
=================

Phần này của hướng dẫn đề cập đến các hệ thống hạt (3D) được tăng tốc bằng GPU. Hầu hết nội dung được thảo luận ở đây cũng áp dụng cho các hạt CPU.

.. rubric:: Giới thiệu
   :heading-level: 2

Bạn có thể sử dụng hệ thống hạt để mô phỏng các hiệu ứng vật lý phức tạp như lửa, tia lửa, khói, hiệu ứng ma thuật và nhiều hiệu ứng khác. Chúng đặc biệt phù hợp để tạo hành vi linh động, tự nhiên và thêm "sức sống" cho các cảnh của bạn.

Ý tưởng là một hạt được phát ra theo một khoảng thời gian cố định và có vòng đời cố định. Trong suốt vòng đời, mọi hạt đều có cùng hành vi cơ bản. Điều làm cho mỗi hạt khác với các hạt khác và tạo nên vẻ tự nhiên là tính ngẫu nhiên mà bạn có thể thêm vào hầu hết các tham số và hành vi của hạt.

Mọi hệ thống hạt bạn tạo trong Godot đều gồm hai phần chính: các hạt và các emitter.

.. rubric:: Các hạt
   :heading-level: 3

Hạt là phần hiển thị của một hệ thống hạt. Đó là những gì bạn nhìn thấy trên màn hình khi một hệ thống hạt đang hoạt động: những hạt bụi nhỏ li ti, ngọn lửa, những quả cầu phát sáng của một hiệu ứng ma thuật. Một hệ thống có thể có từ vài trăm đến hàng chục nghìn hạt. Bạn có thể ngẫu nhiên hóa kích thước, tốc độ và hướng chuyển động của hạt, đồng thời thay đổi màu của hạt trong suốt vòng đời. Khi nghĩ về một đám cháy, bạn có thể hình dung tất cả những hạt than nhỏ bay ra từ đó như các hạt riêng lẻ.

.. rubric:: Emitter
   :heading-level: 3

Emitter là thành phần tạo ra các hạt. Emitter thường không hiển thị, nhưng có thể có hình dạng. Hình dạng đó kiểm soát vị trí và cách các hạt được sinh ra, chẳng hạn như việc chúng lấp đầy một căn phòng giống bụi hay bắn ra từ một điểm duy nhất giống đài phun nước. Quay lại ví dụ về đám cháy, emitter sẽ là phần nhiệt ở trung tâm ngọn lửa tạo ra các hạt than và ngọn lửa.

.. rubric:: Tổng quan về node
   :heading-level: 3

.. figure:: img/particle_nodes.webp
   :alt: Danh sách các node liên quan đến hạt 3D
   :align: right

   Tất cả các node hạt 3D có sẵn trong Godot

Có hai loại hệ thống hạt 3D trong Godot: :ref:`class_GPUParticles3D`, được xử lý trên GPU, và :ref:`class_CPUParticles3D`, được xử lý trên CPU.

Hệ thống hạt CPU kém linh hoạt hơn hệ thống tương ứng trên GPU, nhưng hoạt động trên nhiều loại phần cứng hơn và hỗ trợ tốt hơn cho các thiết bị cũ cũng như điện thoại di động. Vì được xử lý trên CPU, chúng không có hiệu năng tốt bằng hệ thống hạt GPU và không thể render nhiều hạt riêng lẻ như vậy. Ngoài ra, hiện tại chúng không có đầy đủ các tùy chọn kiểm soát mà hạt GPU cung cấp.

Hệ thống hạt GPU chạy trên GPU và có thể render hàng trăm nghìn hạt trên phần cứng hiện đại. Bạn có thể viết shader hạt tùy chỉnh cho chúng, nhờ đó chúng rất linh hoạt. Bạn cũng có thể khiến chúng tương tác với môi trường bằng cách sử dụng các node attractor và collision.

Có ba node attractor hạt: :ref:`class_GPUParticlesAttractorBox3D`, :ref:`class_GPUParticlesAttractorSphere3D` và :ref:`class_GPUParticlesAttractorVectorField3D`. Node attractor tác dụng một lực lên tất cả các hạt trong phạm vi ảnh hưởng, kéo chúng lại gần hoặc đẩy chúng ra xa dựa trên hướng của lực đó.

Có một số node collision hạt. :ref:`class_GPUParticlesCollisionBox3D` và
:ref:`class_GPUParticlesCollisionSphere3D` là những node đơn giản. Bạn có thể sử dụng chúng để tạo các hình dạng cơ bản như hộp, sàn hoặc tường để các hạt va chạm. Hai node còn lại cung cấp hành vi va chạm phức tạp hơn. :ref:`class_GPUParticlesCollisionSDF3D` hữu ích khi bạn muốn các cảnh trong nhà va chạm với hạt mà không phải tự tạo từng collider hình hộp và hình cầu. Nếu muốn các hạt va chạm với những cảnh ngoài trời quy mô lớn, bạn sẽ sử dụng node
:ref:`class_GPUParticlesCollisionHeightField3D`. Node này tạo một heightmap của thế giới và các đối tượng trong đó, rồi sử dụng heightmap này để xử lý va chạm hạt trên quy mô lớn.


.. rubric:: Cách sử dụng cơ bản
   :heading-level: 2

.. toctree::
   :maxdepth: 1
   :name: toc-particles-basic

   creating_a_3d_particle_system
   properties
   process_material_properties

.. rubric:: Chủ đề nâng cao
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
