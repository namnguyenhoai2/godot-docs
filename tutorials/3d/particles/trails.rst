.. _doc_3d_particles_trails:

Vệt hạt 3D
----------

.. note::

     Vệt hạt chỉ được hỗ trợ trong các renderer Forward+ và Mobile, không được hỗ trợ trong Compatibility.

.. figure:: img/particle_trails.webp
   :alt: Particle trails

.. figure:: img/particle_trail_params.webp
   :alt: Particle trail params
   :align: right

   Setting up particle trails

Godot cung cấp một số loại vệt mà bạn có thể thêm vào particle system. Trước khi có thể làm việc với vệt, bạn cần thiết lập một vài tham số trước. Tạo một particle system mới và gán một process material :ref:`as described before <doc_creating_3d_particle_system>`. Trong nhóm ``Trails`` của particle system, đánh dấu vào ô bên cạnh ``Enabled`` và tăng thời lượng phát bằng cách đặt ``Lifetime`` thành một giá trị như ``0.8``. Trong process material, đặt ``Direction`` thành ``(X=0,Y=1.0,Z=0)`` và ``Initial Velocity`` thành ``10.0`` cho cả ``Min`` và ``Max``.

Điều duy nhất còn thiếu là một mesh cho draw pass. Loại mesh bạn đặt ở đây sẽ quyết định loại vệt hạt mà bạn tạo ra.

Vệt dải
~~~~~~~

.. figure:: img/particle_ribbon_mesh.webp
   :alt: Particle ribbon
   :align: right

   Important ribbon mesh parameters

Loại vệt hạt đơn giản nhất là vệt dải. Điều hướng đến phần ``Draw Passes`` và chọn ``New RibbonTrailMesh`` từ các tùy chọn của ``Pass 1``. Một
:ref:`RibbonTrailMesh <class_RibbonTrailMesh>` is a simple quad that is divided into
các phần, sau đó được kéo dài và lặp lại dọc theo những phần đó.

Gán một :ref:`Standard Material <doc_standard_material_3d>` mới cho thuộc tính ``Material`` và bật ``Use Particle Trails`` trong nhóm thuộc tính ``Transform``. Giờ đây các hạt sẽ được phát ra thành các vệt.

Bạn có hai tùy chọn cho tham số ``Shape`` của ribbon mesh. ``Cross`` tạo ra hai quad vuông góc với nhau, khiến vệt hạt có dạng ba chiều hơn một chút. Điều này chỉ thực sự có ý nghĩa nếu bạn không vẽ các vệt ở chế độ ``Particle Billboard``, đồng thời giúp ích khi quan sát các hạt từ nhiều góc khác nhau. Tùy chọn ``Flat`` giới hạn mesh ở một quad duy nhất và hoạt động tốt nhất với các billboard particles.

Tham số ``Size`` điều khiển độ rộng của vệt. Sử dụng nó để làm cho vệt rộng hơn hoặc hẹp hơn.

``Sections``, ``Section Length`` và ``Section Segments`` phối hợp với nhau để điều khiển độ mượt của vệt hạt. Khi một vệt hạt không di chuyển theo đường thẳng, vệt sẽ trông mượt hơn khi uốn cong và xoáy nếu có nhiều phần hơn. ``Section Length`` điều khiển độ dài của mỗi phần. Nhân giá trị này với số phần để biết tổng độ dài của vệt.

.. figure:: img/particle_ribbon_sections.webp
   :alt: Particle ribbon sections

   3 sections, 1m section length (left) vs. 12 sections, 0.25m section length (right). Notice how the total length of the trails stays the same.

Tham số ``Section Segments`` tiếp tục chia mỗi phần thành các đoạn nhỏ hơn. Tuy nhiên, nó không ảnh hưởng đến độ mượt của các phần trong vệt. Thay vào đó, nó điều khiển độ mượt của hình dạng tổng thể của vệt hạt. Thuộc tính ``Curve`` xác định hình dạng này. Nhấp vào ô bên cạnh ``Curve`` rồi gán hoặc tạo một curve mới. Vệt sẽ có hình dạng giống hệt curve, với giá trị của curve tại ``0.0`` ở đầu vệt và giá trị của curve tại ``1.0`` ở đuôi vệt.

.. figure:: img/particle_ribbon_curve.webp
   :alt: Particle ribbon curves

   Particle trails shaped by different curves. The trails move from left to right.

Tùy thuộc vào độ phức tạp của curve, hình dạng của vệt hạt sẽ không trông thật mượt khi số phần thấp. Đây là lúc thuộc tính ``Section Segments`` phát huy tác dụng. Tăng số đoạn của mỗi phần sẽ thêm nhiều vertex hơn vào các cạnh của vệt, để vệt có thể bám sát curve hơn.

.. figure:: img/particle_ribbon_segments.webp
   :alt: Particle ribbon segments

   Particle trail shape smoothness: 1 segment per section (top), 12 segments per section (bottom)

Vệt ống
~~~~~~~

Vệt ống có nhiều thuộc tính chung với vệt dải. Điểm khác biệt lớn là vệt ống phát ra các mesh hình trụ thay vì quad.

.. figure:: img/particle_tube.webp
   :alt: Particle tube trails

   Tube trails emit cylindrical particles

Để tạo vệt ống, điều hướng đến phần ``Draw Passes`` và chọn ``New TubeTrailMesh`` từ các tùy chọn của ``Pass 1``. Một :ref:`TubeTrailMesh <class_TubeTrailMesh>` là một hình trụ được chia thành các phần, sau đó được kéo dài và lặp lại dọc theo những phần đó. Gán một :ref:`Standard Material <doc_standard_material_3d>` mới cho thuộc tính ``Material`` và bật ``Use Particle Trails`` trong nhóm thuộc tính ``Transform``. Giờ đây các hạt sẽ được phát ra thành những vệt hình trụ dài.

.. figure:: img/particle_tube_mesh.webp
   :alt: Particle tube
   :align: right

   Important tube mesh parameters

Các thuộc tính ``Radius`` và ``Radial Steps`` đối với vệt ống tương đương với ``Size`` đối với vệt dải. ``Radius`` xác định bán kính của ống và làm tăng hoặc giảm kích thước tổng thể của nó. ``Radial Steps`` điều khiển số cạnh quanh chu vi của ống. Giá trị cao hơn sẽ tăng độ phân giải của phần nắp ống.

``Sections`` và ``Section Length`` hoạt động giống nhau đối với vệt ống và vệt dải. Chúng điều khiển độ mượt của vệt ống khi nó uốn cong và xoắn thay vì di chuyển theo đường thẳng. Tăng số phần sẽ giúp vệt trông mượt hơn. Thay đổi thuộc tính ``Section Length`` để thay đổi độ dài của mỗi phần, đồng thời thay đổi tổng độ dài của vệt. ``Section Rings`` là phiên bản tương đương dành cho ống của thuộc tính ``Section Segments`` đối với dải. Nó chia nhỏ các phần và thêm hình học vào ống để khớp tốt hơn với hình dạng tùy chỉnh được xác định trong thuộc tính ``Curve``.

Bạn có thể tạo hình cho vệt ống bằng curve, giống như với vệt dải. Nhấp vào ô bên cạnh thuộc tính ``Curve`` rồi gán hoặc tạo một curve mới. Vệt sẽ có hình dạng giống curve, với giá trị của curve tại ``0.0`` ở đầu vệt và giá trị của curve tại ``1.0`` ở đuôi vệt.

.. figure:: img/particle_tube_curve.webp
   :alt: Particle tubes

   Particle tube trails with a custom curve shape: 4 radial steps, 3 sections, 1 section ring (left),
   12 radial steps, 9 sections, 3 section rings (right)

Một thuộc tính quan trọng mà bạn có thể muốn thiết lập là ``Transform Align`` trong nhóm ``Drawing`` của particle system. Nếu giữ nguyên, các ống sẽ không bảo toàn thể tích; chúng bị dẹt ra khi di chuyển vì trục Y của chúng luôn hướng lên ngay cả khi chúng đổi hướng. Điều này có thể gây ra nhiều lỗi hiển thị. Thay vào đó, hãy đặt thuộc tính thành ``Y to Velocity``, khi đó mỗi vệt hạt sẽ giữ cho trục Y của nó thẳng hàng với hướng chuyển động.

.. figure:: img/particle_tube_align.webp
   :alt: Particle tubes aligned

   Particle tube trails without alignment (left) and with Y-axis aligned to velocity (right)
