.. _doc_3d_particles_attractors:

Bộ hút hạt 3D
-------------

.. figure:: img/particle_attractor.webp
   :alt: Particle attractors

Bộ hút hạt là các node áp dụng một lực lên tất cả hạt trong phạm vi ảnh hưởng của chúng. Chúng kéo các hạt lại gần hoặc đẩy chúng ra xa dựa trên hướng của lực đó. Có ba loại bộ hút: :ref:`class_GPUParticlesAttractorBox3D`, :ref:`class_GPUParticlesAttractorSphere3D` và :ref:`class_GPUParticlesAttractorVectorField3D`. Bạn có thể khởi tạo chúng khi runtime và thay đổi các thuộc tính của chúng từ gameplay code; thậm chí bạn còn có thể animate và kết hợp chúng để tạo ra các hiệu ứng hút phức tạp.

.. CẬP NHẬT: Chưa được triển khai. Khi bộ hút hạt được triển khai cho hệ thống hạt 2D .., hãy xóa ghi chú này và xóa comment này.

.. note::

   Bộ hút hạt hiện chưa được triển khai cho hệ thống hạt 2D.

Điều đầu tiên bạn phải làm nếu muốn sử dụng bộ hút là bật thuộc tính ``Attractor Interaction`` trên ParticleProcessMaterial. Hãy thực hiện việc này cho mọi hệ thống hạt cần phản ứng với bộ hút. Giống như hầu hết các thuộc tính trong Godot, bạn cũng có thể thay đổi thuộc tính này trong runtime.

Các thuộc tính phổ biến
~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_common.webp
   :alt: Common particle attractor properties
   :align: right

   Common attractor properties

Có một số thuộc tính mà bạn có thể tìm thấy trên tất cả bộ hút. Chúng nằm trong phần ``GPUParticlesAttractor3D`` trong inspector.

``Strength`` kiểm soát độ mạnh của lực hút. Giá trị dương kéo các hạt lại gần tâm của bộ hút, trong khi giá trị âm đẩy chúng ra xa.

``Attenuation`` kiểm soát mức suy giảm cường độ trong vùng ảnh hưởng của bộ hút. Mỗi bộ hút hạt đều có một ranh giới. Cường độ của nó yếu nhất tại biên của ranh giới này và mạnh nhất tại tâm. Các hạt nằm ngoài ranh giới hoàn toàn không bị bộ hút ảnh hưởng. Đường cong attenuation kiểm soát cách cường độ suy yếu theo khoảng cách đó. Một đường thẳng có nghĩa là cường độ tỉ lệ với khoảng cách: nếu một hạt nằm giữa ranh giới và tâm, cường độ của bộ hút sẽ bằng một nửa so với tại tâm. Các hình dạng đường cong khác nhau sẽ thay đổi tốc độ các hạt tăng tốc về phía bộ hút.

.. figure:: img/particle_attractor_curve.webp
   :alt: Different attractor attenuation curves

   Strength increase variations: constantly over the distance to the attractor (left), fast
   at the boundary border and slowly at the center (middle), slowly at the boundary and
   fast at the center (right).

Thuộc tính ``Directionality`` thay đổi hướng mà các hạt bị kéo về. Ở giá trị ``0.0``, không có tính định hướng, nghĩa là các hạt bị kéo về phía tâm của bộ hút. Ở ``1.0``, bộ hút hoàn toàn có tính định hướng, nghĩa là các hạt sẽ bị kéo dọc theo trục ``-Z`` cục bộ của bộ hút. Bạn có thể thay đổi hướng toàn cục bằng cách xoay bộ hút. Nếu ``Strength`` là số âm, các hạt thay vào đó sẽ bị kéo dọc theo trục ``+Z``.

.. figure:: img/particle_attractor_direction.webp
   :alt: Different attractor directionality values

   No directionality (left) vs. full directionality (right). Notice how the particles move along
   the attractor's local Z-axis.

Thuộc tính ``Cull Mask`` kiểm soát những hệ thống hạt nào bị bộ hút ảnh hưởng, dựa trên :ref:`visibility layers <class_VisualInstance3D>` của từng hệ thống. Một hệ thống hạt chỉ bị bộ hút ảnh hưởng nếu ít nhất một trong các visibility layer của hệ thống được bật trong cull mask của bộ hút.

Bộ hút hình hộp
~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_box_entry.webp
   :alt: Particle attractor box
   :align: right

   Box attractor in the node list

Bộ hút hình hộp có vùng ảnh hưởng dạng hộp. Bạn kiểm soát kích thước của chúng bằng thuộc tính ``Extents``. Box extents luôn đo bằng một nửa độ dài các cạnh của bounds, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp có vùng ảnh hưởng rộng 2 mét theo mỗi cạnh.

Để tạo một bộ hút hình hộp, hãy thêm một child node mới vào scene và chọn ``GPUParticlesAttractorBox3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của hộp hoặc gắn nó vào một node đang di chuyển để tạo ra các hiệu ứng linh động hơn.

.. figure:: img/particle_attractor_box.webp
   :alt: Box attractor parts particle field

   A box attractor with a negative strength value parts a particle field as it moves through it.

Bộ hút hình cầu
~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_sphere_entry.webp
   :alt: Particle attractor sphere
   :align: right

   Sphere attractor in the node list

Bộ hút hình cầu có vùng ảnh hưởng dạng hình cầu. Bạn kiểm soát kích thước của chúng bằng thuộc tính ``Radius``. Mặc dù bộ hút hình hộp không nhất thiết phải là các hình lập phương hoàn hảo, bộ hút hình cầu sẽ luôn là hình cầu: Bạn không thể thiết lập chiều rộng độc lập với chiều cao. Nếu muốn sử dụng bộ hút hình cầu cho các hình dạng thuôn dài, bạn phải thay đổi ``Scale`` của nó trong phần ``Node3D`` của bộ hút.

Để tạo một bộ hút hình cầu, hãy thêm một child node mới vào scene và chọn ``GPUParticlesAttractorSphere3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của hình cầu hoặc gắn nó vào một node đang di chuyển để tạo ra các hiệu ứng linh động hơn.

.. figure:: img/particle_attractor_sphere.webp
   :alt: Sphere attractor parts particle field

   A sphere attractor with a negative strength value parts a particle field as it moves through it.

Bộ hút trường vector
~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_vector_entry.webp
   :alt: Particle attractor vector field
   :align: right

   Vector field attractor in the node list

Trường vector là một vùng 3D chứa các vector được sắp xếp trên một grid. Mật độ grid kiểm soát số lượng vector và khoảng cách giữa chúng. Mỗi vector trong một trường vector trỏ theo một hướng cụ thể. Hướng này có thể hoàn toàn ngẫu nhiên hoặc được căn chỉnh theo cách tạo thành các pattern và đường đi riêng biệt.

Khi các hạt tương tác với một trường vector, hướng chuyển động của chúng thay đổi để khớp với vector gần nhất trong trường. Khi một hạt di chuyển đến gần vector tiếp theo trong trường, nó sẽ thay đổi hướng để khớp với hướng của vector đó. Tốc độ của hạt phụ thuộc vào độ dài của vector.

Giống như bộ hút hình hộp, bộ hút trường vector có vùng ảnh hưởng dạng hộp. Bạn kiểm soát kích thước của chúng bằng thuộc tính ``Extents``, trong đó giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp có vùng ảnh hưởng rộng 2 mét theo mỗi cạnh. Thuộc tính ``Texture`` nhận một :ref:`3D texture <class_Texture3D>`, trong đó mỗi pixel đại diện cho một vector với màu của pixel được diễn giải thành hướng và kích thước của vector.

.. note::

   Khi một texture được sử dụng làm trường vector, có hai kiểu chuyển đổi mà bạn cần nắm rõ:

   1. Tọa độ texture ánh xạ tới bounds của bộ hút. Hình ảnh bên dưới cho biết phần nào của texture tương ứng với phần nào của volume trường vector. Ví dụ, nửa dưới của texture ảnh hưởng đến nửa trên của bộ hút trường vector vì ``+Y`` hướng xuống trong không gian UV của texture nhưng hướng lên trong không gian thế giới của Godot. 2. Các giá trị màu của pixel ánh xạ tới các vector hướng trong không gian. Hình ảnh bên dưới cung cấp một cái nhìn tổng quan. Vì các hạt có thể di chuyển theo hai hướng trên mỗi trục, nửa dưới của dải màu biểu thị các giá trị hướng âm, trong khi nửa trên biểu thị các giá trị hướng dương. Vì vậy, một pixel màu vàng ``(R=1,G=1,B=0)`` ánh xạ tới vector ``(X=1,Y=1,Z=-1)``, trong khi màu xám trung tính ``(R=0.5,G=0.5,B=0.5)`` dẫn đến việc hoàn toàn không có chuyển động.

   .. figure:: img/particle_attractor_vector_mapping.webp
      :alt: Mapping from texture to vector field

Để tạo một bộ hút trường vector, hãy thêm một child node mới vào scene và chọn ``GPUParticlesAttractorVectorField3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của bộ hút hoặc gắn nó vào một node đang di chuyển để tạo ra các hiệu ứng linh động hơn.

.. tip::

   Nếu không có các công cụ bên ngoài để tạo texture trường vector, bạn có thể sử dụng NoiseTexture3D với một Color Ramp được gắn vào làm texture trường vector. Có thể chỉnh sửa Color Ramp để điều chỉnh mức độ ảnh hưởng của trường vector lên từng tọa độ.

.. figure:: img/particle_attractor_vector.webp
   :alt: Vector field attractor in a field of particles

   Two particle systems are affected by the same vector field attractor. :download:`Click here to download the 3D texture <img/particle_vector_field_16x16x16.bmp>`.
