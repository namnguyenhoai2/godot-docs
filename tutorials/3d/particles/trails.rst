.. _doc_3d_particles_trails:

Dải vệt hạt 3D
--------------

.. note::

     Dải vệt hạt chỉ được hỗ trợ trong các renderer Forward+ và Mobile, không được hỗ trợ trong Compatibility.

.. figure:: img/particle_trails.webp
   :alt: Dải vệt hạt

.. figure:: img/particle_trail_params.webp
   :alt: Tham số dải vệt hạt
   :align: right

   Thiết lập dải vệt hạt

Godot cung cấp một số loại dải vệt mà bạn có thể thêm vào hệ thống hạt. Trước khi có thể làm việc với dải vệt, trước tiên bạn cần thiết lập một vài tham số. Tạo một hệ thống hạt mới và gán một process material :ref:`như đã mô tả trước đó <doc_creating_3d_particle_system>`. Trong nhóm ``Trails`` của hệ thống hạt, chọn hộp bên cạnh ``Enabled`` và tăng thời lượng phát bằng cách đặt ``Lifetime`` thành một giá trị như ``0.8``. Trong process material, đặt ``Direction`` thành ``(X=0,Y=1.0,Z=0)`` và ``Initial Velocity`` thành ``10.0`` cho cả ``Min`` và ``Max``.

Điều duy nhất còn thiếu là một mesh cho draw pass. Loại mesh bạn đặt ở đây sẽ quyết định loại dải vệt hạt mà bạn nhận được.

Dải vệt dạng dải băng
~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/particle_ribbon_mesh.webp
   :alt: Dải băng hạt
   :align: right

   Các tham số mesh dải băng quan trọng

Loại dải vệt hạt đơn giản nhất là dải vệt dạng dải băng. Chuyển đến phần ``Draw Passes`` và chọn ``New RibbonTrailMesh`` từ các tùy chọn cho ``Pass 1``. Một
:ref:`RibbonTrailMesh <class_RibbonTrailMesh>` là một quad đơn giản được chia thành các section, sau đó kéo giãn và lặp lại dọc theo các section đó.

Gán một :ref:`Standard Material <doc_standard_material_3d>` mới cho thuộc tính ``Material`` và bật ``Use Particle Trails`` trong nhóm thuộc tính ``Transform``. Các hạt lúc này sẽ được phát ra thành các dải vệt.

Bạn có hai tùy chọn cho tham số mesh dải băng ``Shape``. ``Cross`` tạo ra hai quad vuông góc, khiến dải vệt hạt có dạng ba chiều hơn một chút. Điều này thực sự chỉ có ý nghĩa nếu bạn không vẽ các dải vệt ở chế độ ``Particle Billboard`` và hữu ích khi quan sát các hạt từ nhiều góc khác nhau. Tùy chọn ``Flat`` giới hạn mesh ở một quad duy nhất và hoạt động tốt nhất với các hạt billboard.

Tham số ``Size`` kiểm soát chiều rộng của dải vệt. Sử dụng tham số này để làm dải vệt rộng hơn hoặc hẹp hơn.

``Sections``, ``Section Length`` và ``Section Segments`` phối hợp với nhau để kiểm soát độ mượt của dải vệt hạt. Khi dải vệt hạt không di chuyển theo đường thẳng, nó càng có nhiều section thì càng trông mượt hơn khi uốn cong và xoắn. ``Section Length`` kiểm soát độ dài của mỗi section. Nhân giá trị này với số section để biết tổng độ dài của dải vệt.

.. figure:: img/particle_ribbon_sections.webp
   :alt: Các section của dải băng hạt

   3 section, độ dài section 1m (bên trái) so với 12 section, độ dài section 0.25m (bên phải). Lưu ý rằng tổng độ dài của các dải vệt vẫn giữ nguyên.

Tham số ``Section Segments`` tiếp tục chia mỗi section thành các segment. Tuy nhiên, nó không ảnh hưởng đến độ mượt của các section trong dải vệt. Thay vào đó, nó kiểm soát độ mượt của hình dạng tổng thể của dải vệt hạt. Thuộc tính ``Curve`` xác định hình dạng này. Nhấp vào hộp bên cạnh ``Curve`` và gán hoặc tạo một curve mới. Dải vệt sẽ có hình dạng giống curve, với giá trị của curve tại ``0.0`` ở đầu dải vệt và giá trị của curve tại ``1.0`` ở cuối dải vệt.

.. figure:: img/particle_ribbon_curve.webp
   :alt: Các curve của dải băng hạt

   Các dải vệt hạt được tạo hình bằng những curve khác nhau. Các dải vệt di chuyển từ trái sang phải.

Tùy thuộc vào độ phức tạp của curve, hình dạng dải vệt hạt sẽ không trông thật mượt khi số section thấp. Đây là lúc thuộc tính ``Section Segments`` phát huy tác dụng. Tăng số lượng segment trong mỗi section sẽ thêm nhiều vertex vào các cạnh của dải vệt để dải vệt có thể bám sát curve hơn.

.. figure:: img/particle_ribbon_segments.webp
   :alt: Các segment của dải băng hạt

   Độ mượt của hình dạng dải vệt hạt: 1 segment mỗi section (trên), 12 segment mỗi section (dưới)

Dải vệt dạng ống
~~~~~~~~~~~~~~~~

Dải vệt dạng ống có nhiều thuộc tính giống với dải vệt dạng dải băng. Điểm khác biệt lớn giữa chúng là dải vệt dạng ống phát ra các mesh hình trụ thay vì quad.

.. figure:: img/particle_tube.webp
   :alt: Dải vệt ống hạt

   Dải vệt dạng ống phát ra các hạt hình trụ

Để tạo dải vệt dạng ống, chuyển đến phần ``Draw Passes`` và chọn ``New TubeTrailMesh`` từ các tùy chọn cho ``Pass 1``. Một :ref:`TubeTrailMesh <class_TubeTrailMesh>` là một hình trụ được chia thành các section, sau đó kéo giãn và lặp lại dọc theo các section đó. Gán một :ref:`Standard Material <doc_standard_material_3d>` mới cho thuộc tính ``Material`` và bật ``Use Particle Trails`` trong nhóm thuộc tính ``Transform``. Các hạt lúc này sẽ được phát ra thành những dải vệt dài, hình trụ.

.. figure:: img/particle_tube_mesh.webp
   :alt: Ống hạt
   :align: right

   Các tham số mesh ống quan trọng

Các thuộc tính ``Radius`` và ``Radial Steps`` đối với dải vệt dạng ống cũng tương đương với ``Size`` đối với dải vệt dạng dải băng. ``Radius`` xác định bán kính của ống và tăng hoặc giảm kích thước tổng thể của nó. ``Radial Steps`` kiểm soát số cạnh xung quanh chu vi của ống. Giá trị cao hơn sẽ tăng độ phân giải của nắp ống.

``Sections`` và ``Section Length`` hoạt động giống nhau đối với dải vệt dạng ống và dải vệt dạng dải băng. Chúng kiểm soát độ mượt của dải vệt dạng ống khi nó uốn cong và xoắn thay vì di chuyển theo đường thẳng. Tăng số section sẽ khiến nó trông mượt hơn. Thay đổi thuộc tính ``Section Length`` để thay đổi độ dài của mỗi section và qua đó thay đổi tổng độ dài của dải vệt. ``Section Rings`` là phiên bản tương đương cho ống của thuộc tính ``Section Segments`` đối với dải băng. Nó chia nhỏ các section và thêm hình học vào ống để khớp tốt hơn với hình dạng tùy chỉnh được xác định trong thuộc tính ``Curve``.

Bạn có thể tạo hình cho dải vệt dạng ống bằng curve, giống như với dải vệt dạng dải băng. Nhấp vào hộp bên cạnh thuộc tính ``Curve`` và gán hoặc tạo một curve mới. Dải vệt sẽ có hình dạng giống curve, với giá trị của curve tại ``0.0`` ở đầu dải vệt và giá trị của curve tại ``1.0`` ở cuối dải vệt.

.. figure:: img/particle_tube_curve.webp
   :alt: Các ống hạt

   Các dải vệt dạng ống hạt với hình dạng curve tùy chỉnh: 4 radial step, 3 section, 1 section ring (bên trái), 12 radial step, 9 section, 3 section ring (bên phải)

Một thuộc tính quan trọng bạn có thể muốn thiết lập là ``Transform Align`` trong nhóm ``Drawing`` của hệ thống hạt. Nếu giữ nguyên, các ống sẽ không bảo toàn thể tích; chúng sẽ bị dẹt khi di chuyển vì trục Y của chúng luôn hướng lên ngay cả khi đổi hướng. Điều này có thể gây ra nhiều lỗi hiển thị. Thay vào đó, đặt thuộc tính thành ``Y to Velocity`` để mỗi dải vệt hạt giữ cho trục Y của nó thẳng hàng với hướng chuyển động.

.. figure:: img/particle_tube_align.webp
   :alt: Các ống hạt được căn chỉnh

   Các dải vệt dạng ống hạt không được căn chỉnh (bên trái) và có trục Y được căn chỉnh theo vận tốc (bên phải)
