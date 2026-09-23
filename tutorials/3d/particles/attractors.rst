.. _doc_3d_particles_attractors:

Bộ thu hút hạt 3D
-----------------

.. figure:: img/particle_attractor.webp
   :alt: Bộ thu hút hạt

Bộ thu hút hạt là các node áp dụng một lực lên tất cả các hạt trong phạm vi ảnh hưởng của chúng. Chúng kéo các hạt lại gần hoặc đẩy chúng ra xa dựa trên hướng của lực đó. Có ba loại bộ thu hút: :ref:`class_GPUParticlesAttractorBox3D`, :ref:`class_GPUParticlesAttractorSphere3D` và :ref:`class_GPUParticlesAttractorVectorField3D`. Bạn có thể khởi tạo chúng trong runtime và thay đổi các thuộc tính của chúng từ mã gameplay; thậm chí bạn có thể animate và kết hợp chúng để tạo ra các hiệu ứng thu hút phức tạp.

.. UPDATE: Not implemented. When particle attractors are implemented for 2D
.. particle systems, remove this note and remove this comment.

.. note::

   Bộ thu hút hạt hiện chưa được triển khai cho các hệ thống hạt 2D.

Điều đầu tiên bạn phải làm nếu muốn sử dụng bộ thu hút là bật thuộc tính ``Attractor Interaction`` trên ParticleProcessMaterial. Hãy thực hiện việc này cho mọi hệ thống hạt cần phản ứng với bộ thu hút. Giống như hầu hết các thuộc tính trong Godot, bạn cũng có thể thay đổi thuộc tính này trong runtime.

Các thuộc tính chung
~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_common.webp
   :alt: Các thuộc tính chung của bộ thu hút hạt
   :align: right

   Các thuộc tính chung của bộ thu hút

Có một số thuộc tính mà bạn có thể tìm thấy trên tất cả các bộ thu hút. Chúng nằm trong phần ``GPUParticlesAttractor3D`` của inspector.

``Strength`` kiểm soát độ mạnh của lực thu hút. Giá trị dương kéo các hạt lại gần tâm của bộ thu hút, còn giá trị âm đẩy chúng ra xa.

``Attenuation`` kiểm soát mức suy giảm cường độ trong vùng ảnh hưởng của bộ thu hút. Mọi bộ thu hút hạt đều có một ranh giới. Cường độ của nó yếu nhất ở rìa ranh giới này và mạnh nhất tại tâm. Các hạt nằm ngoài ranh giới hoàn toàn không bị bộ thu hút tác động. Đường cong suy giảm kiểm soát cách cường độ yếu đi theo khoảng cách đó. Một đường thẳng có nghĩa là cường độ tỉ lệ với khoảng cách: nếu một hạt nằm giữa ranh giới và tâm, cường độ thu hút sẽ bằng một nửa so với tại tâm. Các hình dạng đường cong khác nhau sẽ thay đổi tốc độ các hạt tăng tốc về phía bộ thu hút.

.. figure:: img/particle_attractor_curve.webp
   :alt: Các đường cong suy giảm khác nhau của bộ thu hút

   Các biến thể về mức tăng cường độ: tăng đều theo khoảng cách đến bộ thu hút (trái), tăng nhanh ở rìa ranh giới và chậm ở tâm (giữa), tăng chậm ở ranh giới và nhanh ở tâm (phải).

Thuộc tính ``Directionality`` thay đổi hướng mà các hạt bị kéo về. Ở giá trị ``0.0``, không có tính định hướng, nghĩa là các hạt bị kéo về tâm của bộ thu hút. Ở ``1.0``, bộ thu hút có tính định hướng hoàn toàn, nghĩa là các hạt sẽ bị kéo dọc theo trục ``-Z`` cục bộ của bộ thu hút. Bạn có thể thay đổi hướng toàn cục bằng cách xoay bộ thu hút. Nếu ``Strength`` là số âm, các hạt sẽ bị kéo dọc theo trục ``+Z``.

.. figure:: img/particle_attractor_direction.webp
   :alt: Các giá trị định hướng khác nhau của bộ thu hút

   Không định hướng (trái) so với định hướng hoàn toàn (phải). Hãy chú ý cách các hạt di chuyển dọc theo trục Z cục bộ của bộ thu hút.

Thuộc tính ``Cull Mask`` kiểm soát những hệ thống hạt nào bị bộ thu hút tác động dựa trên :ref:`visibility layers <class_VisualInstance3D>` của từng hệ thống. Một hệ thống hạt chỉ bị bộ thu hút tác động nếu ít nhất một visibility layer của hệ thống được bật trong cull mask của bộ thu hút.

Bộ thu hút dạng hộp
~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_box_entry.webp
   :alt: Bộ thu hút hạt dạng hộp
   :align: right

   Bộ thu hút dạng hộp trong danh sách node

Bộ thu hút dạng hộp có vùng ảnh hưởng hình hộp. Bạn điều khiển kích thước của chúng bằng thuộc tính ``Extents``. Kích thước mở rộng của hộp luôn đo bằng một nửa độ dài các cạnh của giới hạn, vì vậy giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp có vùng ảnh hưởng rộng 2 mét ở mỗi phía.

Để tạo một bộ thu hút dạng hộp, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesAttractorBox3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của hộp hoặc gắn nó vào một node đang di chuyển để tạo ra các hiệu ứng linh hoạt hơn.

.. figure:: img/particle_attractor_box.webp
   :alt: Bộ thu hút dạng hộp chia tách trường hạt

   Một bộ thu hút dạng hộp có giá trị cường độ âm sẽ chia tách một trường hạt khi di chuyển qua trường đó.

Bộ thu hút dạng cầu
~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_sphere_entry.webp
   :alt: Bộ thu hút hạt dạng cầu
   :align: right

   Bộ thu hút dạng cầu trong danh sách node

Bộ thu hút dạng cầu có vùng ảnh hưởng hình cầu. Bạn điều khiển kích thước của chúng bằng thuộc tính ``Radius``. Mặc dù bộ thu hút dạng hộp không nhất thiết phải là hình lập phương hoàn hảo, bộ thu hút dạng cầu sẽ luôn là hình cầu: bạn không thể thiết lập chiều rộng độc lập với chiều cao. Nếu muốn sử dụng bộ thu hút dạng cầu cho các hình dạng kéo dài, bạn phải thay đổi ``Scale`` của nó trong phần ``Node3D`` của bộ thu hút.

Để tạo một bộ thu hút dạng cầu, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesAttractorSphere3D`` từ danh sách các node khả dụng. Bạn có thể animate vị trí của hình cầu hoặc gắn nó vào một node đang di chuyển để tạo ra các hiệu ứng linh hoạt hơn.

.. figure:: img/particle_attractor_sphere.webp
   :alt: Bộ thu hút dạng cầu chia tách trường hạt

   Một bộ thu hút dạng cầu có giá trị cường độ âm sẽ chia tách một trường hạt khi di chuyển qua trường đó.

Bộ thu hút trường vector
~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_attractor_vector_entry.webp
   :alt: Trường vector của bộ thu hút hạt
   :align: right

   Bộ thu hút trường vector trong danh sách node

Trường vector là một vùng 3D chứa các vector được bố trí trên một lưới. Mật độ lưới kiểm soát số lượng vector và khoảng cách giữa chúng. Mỗi vector trong một trường vector chỉ theo một hướng cụ thể. Hướng này có thể hoàn toàn ngẫu nhiên hoặc được căn chỉnh theo cách tạo thành các mẫu và đường đi riêng biệt.

Khi các hạt tương tác với một trường vector, hướng di chuyển của chúng thay đổi để khớp với vector gần nhất trong trường. Khi một hạt di chuyển đến gần vector tiếp theo trong trường, nó sẽ đổi hướng để khớp với hướng của vector đó. Tốc độ của hạt phụ thuộc vào độ dài của vector.

Giống như bộ thu hút dạng hộp, bộ thu hút trường vector có vùng ảnh hưởng hình hộp. Bạn điều khiển kích thước của chúng bằng thuộc tính ``Extents``, trong đó giá trị ``(X=1.0,Y=1.0,Z=1.0)`` sẽ tạo ra một hộp có vùng ảnh hưởng rộng 2 mét ở mỗi phía. Thuộc tính ``Texture`` nhận một :ref:`3D texture <class_Texture3D>` trong đó mỗi pixel đại diện cho một vector, với màu của pixel được diễn giải thành hướng và kích thước của vector.

.. note::

   Khi một texture được sử dụng làm trường vector, có hai loại chuyển đổi mà bạn cần lưu ý:

   1. Tọa độ texture ánh xạ tới các giới hạn của bộ thu hút. Hình ảnh bên dưới cho biết phần nào của texture tương ứng với phần nào của thể tích trường vector. Ví dụ, nửa dưới của texture tác động đến nửa trên của bộ thu hút trường vector vì ``+Y`` hướng xuống trong không gian UV của texture nhưng hướng lên trong không gian thế giới của Godot.
   2. Các giá trị màu của pixel ánh xạ tới các vector hướng trong không gian. Hình ảnh bên dưới cung cấp tổng quan về việc này. Vì các hạt có thể di chuyển theo hai hướng trên mỗi trục, nửa dưới của dải màu biểu thị các giá trị hướng âm, còn nửa trên biểu thị các giá trị hướng dương. Vì vậy, một pixel màu vàng ``(R=1,G=1,B=0)`` ánh xạ tới vector ``(X=1,Y=1,Z=-1)``, trong khi màu xám trung tính ``(R=0.5,G=0.5,B=0.5)`` sẽ không tạo ra chuyển động nào.

   .. figure:: img/particle_attractor_vector_mapping.webp
      :alt: Ánh xạ từ texture sang trường vector

Để tạo một vector field attractor, hãy thêm một node con mới vào scene rồi chọn ``GPUParticlesAttractorVectorField3D`` từ danh sách các node hiện có. Bạn có thể animate vị trí của attractor hoặc gắn nó vào một node đang chuyển động để tạo ra các hiệu ứng linh hoạt hơn.

.. tip::

   Nếu không có công cụ bên ngoài để tạo texture vector field, bạn có thể sử dụng NoiseTexture3D với Color Ramp được gắn làm texture vector field. Có thể sửa đổi Color Ramp để điều chỉnh mức độ ảnh hưởng của vector field lên từng tọa độ.

.. figure:: img/particle_attractor_vector.webp
   :alt: Vector field attractor trong một trường hạt

   Hai hệ thống hạt chịu ảnh hưởng của cùng một vector field attractor. :download:`Nhấp vào đây để tải xuống texture 3D <img/particle_vector_field_16x16x16.bmp>`.
