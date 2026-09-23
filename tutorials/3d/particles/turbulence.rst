.. _doc_3d_particles_turbulence:

Nhiễu loạn hạt
--------------

.. figure:: img/particle_turbulence.webp
   :alt: Nhiễu loạn hạt

Nhiễu loạn sử dụng texture nhiễu để thêm biến thiên và các mẫu thú vị vào chuyển động của hạt. Nó có thể được kết hợp với :ref:`particle attractors <doc_3d_particles_attractors>` và
các node :ref:`collision <doc_3d_particles_collision>` để tạo ra hành vi có vẻ phức tạp hơn nữa.

.. figure:: img/particle_turbulence_properties.webp
   :alt: Các thuộc tính nhiễu loạn
   :align: right

   Các thuộc tính nhiễu loạn hạt

Có hai việc bạn phải làm trước khi nhiễu loạn có bất kỳ tác động nào lên một hệ thống hạt. Trước tiên, bạn phải thêm chuyển động cho hệ thống hạt. Nhiễu loạn thay đổi hướng và tốc độ chuyển động của hạt, nhưng không tự tạo ra chuyển động. Chỉ cần cung cấp cho hệ thống hạt một chút trọng lực là đủ, nhưng bạn cũng có thể tạo một số attractor nếu muốn các hạt đi theo một đường chuyển động phức tạp hơn. Thứ hai, bạn cần :ref:`bật nhiễu loạn trong particle process material <doc_process_material_properties_turbulence>`. Sau khi được bật, bạn có thể truy cập tất cả các thuộc tính nhiễu loạn.

.. warning::

    Nhiễu loạn sử dụng nhiễu 3D, vốn có chi phí hiệu năng cao trên GPU. Tối đa chỉ nên bật nhiễu loạn cho một vài hệ thống hạt trên màn hình. Không nên sử dụng nhiễu loạn khi nhắm đến các nền tảng mobile/web.

Các thuộc tính nhiễu
~~~~~~~~~~~~~~~~~~~~

Nền tảng của nhiễu loạn hạt là một mẫu nhiễu. Có một số thuộc tính cho phép bạn điều chỉnh các thuộc tính khác nhau của mẫu này.

Thuộc tính ``Noise Strength`` điều khiển độ tương phản của mẫu, yếu tố ảnh hưởng đến độ sắc nét tổng thể của nhiễu loạn. Giá trị thấp hơn tạo ra một mẫu mềm hơn, trong đó các đường chuyển động riêng lẻ không được phân tách rõ ràng khỏi nhau. Đặt giá trị này cao hơn để làm cho mẫu rõ rệt hơn.

.. figure:: img/particle_turbulence_strength.webp
   :alt: Độ mạnh nhiễu loạn của nhiễu

   Ở giá trị 1 (bên trái), độ mạnh của nhiễu tạo ra các mẫu nhiễu loạn mềm hơn so với giá trị 20 (bên phải)

Thuộc tính ``Noise Scale`` điều khiển tần số của mẫu. Về cơ bản, nó thay đổi tỷ lệ UV của texture nhiễu, trong đó giá trị nhỏ hơn tạo ra chi tiết mịn hơn, nhưng các mẫu lặp lại sẽ dễ nhận thấy hơn. Giá trị lớn hơn tạo ra mẫu nhiễu loạn yếu hơn về tổng thể, nhưng hệ thống hạt có thể bao phủ một khu vực lớn hơn trước khi việc lặp lại trở thành vấn đề.

.. figure:: img/particle_turbulence_scale.webp
   :alt: Tỷ lệ nhiễu loạn của nhiễu

   Tỷ lệ nhiễu loạn của nhiễu tạo ra chi tiết mịn hơn ở giá trị 1.5 (bên trái) so với giá trị 6 (bên phải)

Thuộc tính ``Noise Speed`` nhận một vector và điều khiển tốc độ cũng như hướng pan của nhiễu. Điều này cho phép bạn di chuyển mẫu nhiễu theo thời gian, tạo thêm một lớp biến thiên chuyển động cho hệ thống hạt.

.. warning::

   Đừng nhầm lẫn tốc độ chuyển động của hạt với tốc độ pan của nhiễu! Đây là hai yếu tố khác nhau. Chuyển động của hạt được xác định bởi một số thuộc tính, bao gồm cả nhiễu loạn. Thuộc tính ``Noise Speed`` di chuyển chính mẫu nhiễu, từ đó thay đổi vị trí mà nhiễu tác động lên các hạt.

Ở giá trị ``(X=0,Y=0,Z=0)``, mẫu nhiễu hoàn toàn không di chuyển. Ảnh hưởng lên chuyển động của hạt vẫn giữ nguyên tại mọi điểm đã cho. Thay vào đó, đặt tốc độ thành ``(X=1,Y=0,Z=0)``, và mẫu nhiễu sẽ di chuyển dọc theo trục X.

.. figure:: img/particle_turbulence_speed.webp
   :alt: Tốc độ nhiễu loạn của nhiễu

   Các giá trị tốc độ nhiễu khác nhau. Bên trái\: (X=0,Y=0,Z=0), ở giữa\: (X=0.5,Y=0.5,Z=0.5), bên phải\: (X=0,Y=-2,Z=0).

Thuộc tính ``Noise Speed Random`` thêm một mức ngẫu nhiên vào tốc độ pan của nhiễu. Điều này giúp phá vỡ các mẫu dễ nhìn thấy, đặc biệt là ở tốc độ pan cao, khi sự lặp lại dễ nhận thấy hơn.

Các thuộc tính ảnh hưởng
~~~~~~~~~~~~~~~~~~~~~~~~

Các thuộc tính ảnh hưởng xác định mức độ mỗi hạt bị tác động bởi nhiễu loạn. Sử dụng ``Influence Min`` để đặt giá trị tối thiểu và ``Influence Max`` để đặt giá trị tối đa. Khi một hạt xuất hiện, ảnh hưởng được chọn ngẫu nhiên trong phạm vi này. Bạn cũng có thể thiết lập một đường cong bằng thuộc tính ``Influence Over Life`` để điều chỉnh giá trị đó trong suốt vòng đời của mỗi hạt. Ba thuộc tính này cùng nhau điều khiển cường độ tác động của nhiễu loạn lên hệ thống hạt :ref:`như đã mô tả ở trên <doc_process_material_properties>`.

Vì các thuộc tính này ảnh hưởng đến tác động tổng thể của nhiễu loạn lên một hệ thống hạt, cả hướng và tốc độ chuyển động đều thay đổi khi bạn đặt các giá trị khác nhau. Ảnh hưởng mạnh hơn khiến hạt di chuyển nhanh hơn và do đó tất cả các hạt đi theo những đường hẹp hơn.

.. figure:: img/particle_turbulence_influence.webp
   :alt: Ảnh hưởng của nhiễu loạn

   Hãy chú ý rằng các đường đi của hạt hẹp hơn và ít phân tán hơn ở các giá trị ảnh hưởng cao (bên phải)

Các thuộc tính dịch chuyển
~~~~~~~~~~~~~~~~~~~~~~~~~~

Dịch chuyển thay đổi vị trí bắt đầu của một hạt. Sử dụng ``Initial Displacement Min`` để đặt giới hạn dưới và ``Initial Displacement Max`` để đặt giới hạn trên. Khi một hạt xuất hiện, mức dịch chuyển được chọn ngẫu nhiên trong phạm vi này và nhân với một hướng ngẫu nhiên.

Dịch chuyển rất hữu ích để phá vỡ các hình dạng đều đặn hoặc tạo ra các hình dạng phức tạp từ những hình dạng đơn giản hơn. Điểm khác biệt duy nhất giữa các hệ thống hạt trong ảnh chụp màn hình bên dưới là giá trị được cung cấp cho các thuộc tính dịch chuyển.

.. figure:: img/particle_turbulence_displacement.webp
   :alt: Dịch chuyển nhiễu loạn

   Không dịch chuyển (bên trái), giá trị dịch chuyển là 5 (ở giữa), phạm vi dịch chuyển [-20, 20] (bên phải)
