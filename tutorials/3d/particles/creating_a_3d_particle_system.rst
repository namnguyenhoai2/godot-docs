.. _doc_creating_3d_particle_system:

Tạo hệ thống hạt 3D
-------------------

.. figure:: img/particle_node_new.webp
   :align: right

   Các thuộc tính bắt buộc của node hạt

Để bắt đầu sử dụng hạt, việc đầu tiên chúng ta cần làm là thêm một node ``GPUParticles3D`` vào scene. Trước khi thực sự có thể nhìn thấy hạt, chúng ta phải thiết lập hai tham số trên node: ``Process Material`` và ít nhất một ``Draw Pass``.

Vật liệu xử lý
~~~~~~~~~~~~~~

Để thêm vật liệu xử lý vào node hạt, hãy đi đến ``Process Material`` trong bảng inspector. Nhấp vào ô bên cạnh ``Process Material`` và chọn ``New ParticleProcessMaterial`` từ menu thả xuống.

.. figure:: img/particle_new_process_material.webp
   :align: right

   Tạo vật liệu xử lý

:ref:`class_ParticleProcessMaterial` là một loại vật liệu đặc biệt. Chúng ta không dùng nó để vẽ bất kỳ đối tượng nào. Thay vào đó, chúng ta dùng nó để cập nhật dữ liệu và hành vi của hạt trên GPU thay vì CPU, nhờ đó hiệu năng được cải thiện đáng kể. Nhấp vào vật liệu vừa thêm sẽ hiển thị một danh sách dài các thuộc tính mà bạn có thể thiết lập để điều khiển hành vi của từng hạt.

Các lượt vẽ
~~~~~~~~~~~

.. figure:: img/particle_first_draw_pass.webp
   :align: right

   Cần ít nhất một lượt vẽ

Để render bất kỳ hạt nào, cần xác định ít nhất một lượt vẽ. Để thực hiện việc đó, hãy đi đến ``Draw Passes`` trong bảng inspector. Nhấp vào ô bên cạnh ``Pass 1`` và chọn ``New QuadMesh`` từ menu thả xuống. Sau đó, nhấp vào mesh và đặt ``Size`` của nó thành 0.1 cho cả ``x`` và ``y``. Việc giảm kích thước của mesh giúp phân biệt các mesh hạt riêng lẻ dễ hơn một chút ở giai đoạn này.

Bạn có thể sử dụng tối đa 4 lượt vẽ cho mỗi hệ thống hạt. Mỗi lượt có thể render một mesh khác với material riêng. Tất cả các lượt vẽ đều sử dụng dữ liệu được tính toán bởi vật liệu xử lý, đây là một phương pháp hiệu quả để tạo các hiệu ứng phức tạp: Tính toán hành vi của hạt một lần rồi cung cấp dữ liệu đó cho nhiều lượt render.

.. figure:: img/particle_two_draw_passes.webp

   Sử dụng nhiều lượt vẽ: các hình chữ nhật màu vàng (lượt 1) và các hình cầu màu xanh dương (lượt 2)

Nếu đã làm theo các bước trên, hệ thống hạt của bạn lúc này sẽ phát ra các hạt theo kiểu giống như thác nước, khiến chúng di chuyển xuống dưới và biến mất sau vài giây. Đây là nền tảng cho mọi hiệu ứng hạt. Hãy xem tài liệu về :ref:`particle <doc_3d_particles_properties>` và
các thuộc tính của :ref:`particle material <doc_process_material_properties>` để tìm hiểu cách làm cho hiệu ứng hạt thú vị hơn.

.. figure:: img/particle_basic_system.webp

Chuyển đổi hạt
~~~~~~~~~~~~~~

.. figure:: img/particle_convert_cpu.webp
   :align: right

   Chuyển hạt GPU thành hạt CPU

Bạn có thể chuyển đổi hạt GPU thành hạt CPU bất kỳ lúc nào bằng mục tương ứng trong menu viewport. Khi thực hiện việc này, hãy lưu ý rằng không phải mọi tính năng của hạt GPU đều có sẵn cho hạt CPU, vì vậy hệ thống hạt kết quả sẽ có hình thức và hành vi khác với hệ thống ban đầu.

Bạn cũng có thể chuyển đổi hạt CPU thành hạt GPU nếu không còn cần sử dụng hạt CPU. Việc này cũng được thực hiện từ menu viewport.

Một số tính năng đáng chú ý nhất bị mất trong quá trình chuyển đổi gồm có:

- nhiều lượt vẽ
- turbulence
- sub-emitters
- trails
- attractors
- collision

Bạn cũng sẽ mất các thuộc tính sau:

- ``Amount Ratio``
- ``Interp to End``
- ``Damping as Friction``
- ``Emission Shape Offset``
- ``Emission Shape Scale``
- ``Inherit Velocity Ratio``
- ``Velocity Pivot``
- ``Directional Velocity``
- ``Radial Velocity``
- ``Velocity Limit``
- ``Scale Over Velocity``

Việc chuyển đổi hạt GPU thành hạt CPU có thể trở nên cần thiết khi bạn muốn phát hành game trên các thiết bị cũ không hỗ trợ các graphics API hiện đại.
