.. _doc_creating_3d_particle_system:

Tạo hệ thống particle 3D
------------------------

.. figure:: img/particle_node_new.webp
   :align: right

   Required particle node properties

Để bắt đầu với particle, việc đầu tiên chúng ta cần làm là thêm một node ``GPUParticles3D`` vào scene. Trước khi có thể thực sự nhìn thấy bất kỳ particle nào, chúng ta phải thiết lập hai tham số trên node: ``Process Material`` và ít nhất một ``Draw Pass``.

Process material
~~~~~~~~~~~~~~~~

Để thêm process material vào node particle, hãy đi đến ``Process Material`` trong bảng inspector. Nhấp vào ô bên cạnh ``Process Material`` và chọn ``New ParticleProcessMaterial`` từ menu dropdown.

.. figure:: img/particle_new_process_material.webp
   :align: right

   Creating a process material

:ref:`class_ParticleProcessMaterial` is a special kind of material. We don't use it to draw any objects.
Chúng ta sử dụng nó để cập nhật dữ liệu và hành vi của particle trên GPU thay vì CPU, nhờ đó đạt được mức tăng hiệu năng rất lớn. Nhấp vào material vừa thêm sẽ hiển thị một danh sách dài các thuộc tính mà bạn có thể thiết lập để điều khiển hành vi của từng particle.

Draw pass
~~~~~~~~~

.. figure:: img/particle_first_draw_pass.webp
   :align: right

   At least one draw pass is required

Để render bất kỳ particle nào, cần xác định ít nhất một draw pass. Để thực hiện việc đó, hãy đi đến ``Draw Passes`` trong bảng inspector. Nhấp vào ô bên cạnh ``Pass 1`` và chọn ``New QuadMesh`` từ menu dropdown. Sau đó, nhấp vào mesh và đặt ``Size`` của nó thành 0.1 cho cả ``x`` và ``y``. Việc giảm kích thước của mesh giúp dễ phân biệt các mesh particle riêng lẻ hơn một chút ở giai đoạn này.

Bạn có thể sử dụng tối đa 4 draw pass cho mỗi hệ thống particle. Mỗi pass có thể render một mesh khác với material riêng biệt. Tất cả draw pass đều sử dụng dữ liệu được tính toán bởi process material. Đây là một phương pháp hiệu quả để tạo các hiệu ứng phức tạp: tính toán hành vi của particle một lần rồi cung cấp dữ liệu đó cho nhiều render pass.

.. figure:: img/particle_two_draw_passes.webp

   Using multiple draw passes: yellow rectangles (pass1) and blue spheres (pass 2)

Nếu đã làm theo các bước trên, hệ thống particle của bạn hiện sẽ phát particle theo kiểu giống như thác nước, khiến chúng di chuyển xuống dưới và biến mất sau vài giây. Đây là nền tảng cho mọi hiệu ứng particle. Hãy xem tài liệu về :ref:`particle <doc_3d_particles_properties>` và
:ref:`particle material <doc_process_material_properties>` properties to
tìm hiểu cách làm cho các hiệu ứng particle trở nên thú vị hơn.

.. figure:: img/particle_basic_system.webp

Chuyển đổi particle
~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_convert_cpu.webp
   :align: right

   Turning GPU into CPU particles

Bạn có thể chuyển đổi GPU particle thành CPU particle bất kỳ lúc nào bằng mục tương ứng trong menu viewport. Khi thực hiện việc này, hãy nhớ rằng không phải mọi tính năng của GPU particle đều khả dụng cho CPU particle, vì vậy hệ thống particle kết quả sẽ có diện mạo và hành vi khác với bản gốc.

Bạn cũng có thể chuyển đổi CPU particle thành GPU particle nếu không còn cần sử dụng CPU particle. Việc này cũng được thực hiện từ menu viewport.

Một số tính năng đáng chú ý nhất bị mất trong quá trình chuyển đổi bao gồm:

- multiple draw passes - turbulence - sub-emitters - trails - attractors - collision

Bạn cũng mất các thuộc tính sau:

- ``Amount Ratio`` - ``Interp to End`` - ``Damping as Friction`` - ``Emission Shape Offset`` - ``Emission Shape Scale`` - ``Inherit Velocity Ratio`` - ``Velocity Pivot`` - ``Directional Velocity`` - ``Radial Velocity`` - ``Velocity Limit`` - ``Scale Over Velocity``

Việc chuyển đổi GPU particle thành CPU particle có thể trở nên cần thiết khi bạn muốn phát hành game trên các thiết bị cũ không hỗ trợ các graphics API hiện đại.
