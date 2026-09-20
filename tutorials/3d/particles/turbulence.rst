.. _doc_3d_particles_turbulence:

Turbulence của particle
-----------------------

.. figure:: img/particle_turbulence.webp
   :alt: Particle turbulence

Turbulence sử dụng noise texture để thêm biến thể và các pattern thú vị vào chuyển động của particle. Nó có thể được kết hợp với :ref:`particle attractors <doc_3d_particles_attractors>` và
:ref:`collision <doc_3d_particles_collision>` nodes to create even more complex looking behavior.

.. figure:: img/particle_turbulence_properties.webp
   :alt: Turbulence properties
   :align: right

   Particle turbulence properties

Có hai việc bạn phải làm trước khi turbulence có bất kỳ tác động nào lên một hệ thống particle. Trước tiên, bạn phải thêm chuyển động cho hệ thống particle. Turbulence thay đổi hướng và tốc độ chuyển động của particle, nhưng không tự tạo ra chuyển động. Chỉ cần cung cấp cho hệ thống particle một chút trọng lực là đủ, nhưng bạn cũng có thể tạo một số attractor nếu muốn các particle đi theo một đường chuyển động phức tạp hơn. Thứ hai, bạn cần :ref:`enable turbulence in the particle process material <doc_process_material_properties_turbulence>`. Sau khi được bật, bạn có thể truy cập tất cả các thuộc tính của turbulence.

.. warning::

    Turbulence sử dụng noise 3D, vốn có chi phí hiệu năng cao trên GPU. Tối đa chỉ nên bật turbulence trên một vài hệ thống particle đang hiển thị trên màn hình. Không khuyến nghị sử dụng turbulence khi nhắm đến các nền tảng mobile/web.

Các thuộc tính noise
~~~~~~~~~~~~~~~~~~~~

Nền tảng của turbulence trong particle là một pattern noise. Có một số thuộc tính cho phép bạn điều chỉnh các thuộc tính khác nhau của pattern này.

Thuộc tính ``Noise Strength`` điều khiển độ tương phản của pattern, yếu tố ảnh hưởng đến độ sắc nét tổng thể của turbulence. Giá trị thấp hơn tạo ra một pattern mềm hơn, trong đó các đường chuyển động riêng lẻ không bị tách biệt quá rõ khỏi nhau. Đặt giá trị này cao hơn để pattern rõ rệt hơn.

.. figure:: img/particle_turbulence_strength.webp
   :alt: Turbulence noise strength

   At a value of 1 (left), the noise strength produces softer turbulence patterns than at 20 (right)

Thuộc tính ``Noise Scale`` điều khiển tần số của pattern. Về cơ bản, nó thay đổi tỷ lệ UV của noise texture; giá trị nhỏ hơn tạo ra chi tiết mịn hơn, nhưng các pattern lặp lại sẽ trở nên dễ nhận thấy hơn. Giá trị lớn hơn tạo ra pattern turbulence yếu hơn về tổng thể, nhưng hệ thống particle có thể bao phủ một khu vực lớn hơn trước khi hiện tượng lặp lại bắt đầu trở thành vấn đề.

.. figure:: img/particle_turbulence_scale.webp
   :alt: Turbulence noise scale

   Turbulence noise scale produces finer details at a value of 1.5 (left) than at 6 (right)

Thuộc tính ``Noise Speed`` nhận một vector và điều khiển tốc độ cũng như hướng panning của noise. Điều này cho phép bạn di chuyển pattern noise theo thời gian, thêm một lớp biến thiên chuyển động khác cho hệ thống particle.

.. warning::

   Đừng nhầm tốc độ chuyển động của particle với tốc độ panning của noise! Đây là hai khái niệm khác nhau. Chuyển động của particle được xác định bởi một số thuộc tính, bao gồm noise của turbulence. Thuộc tính ``Noise Speed`` di chuyển chính pattern, từ đó thay đổi vị trí mà noise tác động lên các particle.

Ở giá trị ``(X=0,Y=0,Z=0)``, pattern noise hoàn toàn không di chuyển. Ảnh hưởng lên chuyển động của particle vẫn giữ nguyên tại mỗi điểm nhất định. Thay vào đó, đặt tốc độ thành ``(X=1,Y=0,Z=0)``, pattern noise sẽ di chuyển dọc theo trục X.

.. figure:: img/particle_turbulence_speed.webp
   :alt: Turbulence noise speed

   Different noise speed values. Left\: (X=0,Y=0,Z=0), middle\: (X=0.5,Y=0.5,Z=0.5), right\: (X=0,Y=-2,Z=0).

Thuộc tính ``Noise Speed Random`` thêm một chút tính ngẫu nhiên vào tốc độ panning của noise. Điều này giúp phá vỡ các pattern dễ nhìn thấy, đặc biệt là ở tốc độ panning cao, khi hiện tượng lặp lại trở nên dễ nhận thấy hơn.

Các thuộc tính ảnh hưởng
~~~~~~~~~~~~~~~~~~~~~~~~

Các thuộc tính ảnh hưởng xác định mức độ mỗi particle bị turbulence tác động. Sử dụng ``Influence Min`` để đặt giá trị tối thiểu và ``Influence Max`` để đặt giá trị tối đa. Khi một particle xuất hiện, mức ảnh hưởng sẽ được chọn ngẫu nhiên trong phạm vi này. Bạn cũng có thể thiết lập một curve bằng thuộc tính ``Influence Over Life`` để điều chỉnh giá trị đó trong suốt vòng đời của mỗi particle. Ba thuộc tính này kết hợp với nhau sẽ kiểm soát cường độ tác động của turbulence lên hệ thống particle :ref:`as described before <doc_process_material_properties>`.

Vì các thuộc tính này ảnh hưởng đến tác động tổng thể của turbulence lên một hệ thống particle, cả hướng và tốc độ chuyển động đều thay đổi khi bạn đặt các giá trị khác nhau. Tác động mạnh hơn khiến particle di chuyển nhanh hơn, đồng thời tất cả particle sẽ đi theo các đường hẹp hơn.

.. figure:: img/particle_turbulence_influence.webp
   :alt: Turbulence influence

   Notice how the particle paths are more narrow and less spread out at high influence values (right)

Các thuộc tính dịch chuyển
~~~~~~~~~~~~~~~~~~~~~~~~~~

Displacement thay đổi vị trí bắt đầu của particle. Sử dụng ``Initial Displacement Min`` để đặt giới hạn dưới và ``Initial Displacement Max`` để đặt giới hạn trên. Khi một particle xuất hiện, mức displacement sẽ được chọn ngẫu nhiên trong phạm vi này và nhân với một hướng ngẫu nhiên.

Displacement rất hữu ích để phá vỡ các hình dạng đều đặn hoặc tạo ra các hình dạng phức tạp từ những hình dạng đơn giản hơn. Điểm khác biệt duy nhất giữa các hệ thống particle trong ảnh chụp màn hình bên dưới là giá trị được gán cho các thuộc tính displacement.

.. figure:: img/particle_turbulence_displacement.webp
   :alt: Turbulence displacement

   No displacement (left), displacement value of 5 (middle), displacement range [-20, 20] (right)
