:article_outdated: Đúng

.. _doc_csg_tools:

Các mức độ tạo nguyên mẫu với CSG
=================================

CSG là viết tắt của **Constructive Solid Geometry**, một công cụ dùng để kết hợp các hình dạng cơ bản hoặc mesh tùy chỉnh nhằm tạo ra những hình dạng phức tạp hơn. Trong phần mềm tạo mô hình 3D, CSG chủ yếu được biết đến với tên gọi "Boolean Operators".

Tạo nguyên mẫu cho level là một trong những cách sử dụng chính của CSG trong Godot. Kỹ thuật này cho phép người dùng tạo các hình dạng phổ biến nhất bằng cách kết hợp các primitive. Có thể tạo môi trường bên trong bằng cách sử dụng các primitive đảo ngược.

.. note:: Các node CSG trong Godot chủ yếu được dùng để tạo nguyên mẫu. Không có hỗ trợ tích hợp cho UV mapping hoặc chỉnh sửa polygon 3D (mặc dù có thể sử dụng polygon 2D được extrude với node CSGPolygon3D).

          Nếu bạn đang tìm một công cụ thiết kế level dễ sử dụng cho dự án, bạn có thể muốn dùng `FuncGodot <https://github.com/func-godot/func_godot_plugin>`__ hoặc `Cyclops Level Builder <https://github.com/blackears/cyclopsLevelBuilder>`__ thay thế.

.. video:: video/csg_tools.webm
   :alt: CSG being used to subtract a torus shape from a box
   :autoplay:
   :loop:
   :muted:
   :align: default

.. seealso::

    Bạn có thể xem cách sử dụng các node CSG để xây dựng nhiều hình dạng khác nhau (chẳng hạn như cầu thang hoặc đường đi) trong `Constructive Solid Geometry demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/csg>`__.

Giới thiệu về các node CSG
--------------------------

Cũng như các tính năng khác của Godot, CSG được hỗ trợ dưới dạng các node. Đây là các node CSG:

- :ref:`CSGBox3D <class_CSGBox3D>`
- :ref:`CSGCylinder3D <class_CSGCylinder3D>` (cũng hỗ trợ hình nón)
- :ref:`CSGSphere3D <class_CSGSphere3D>`
- :ref:`CSGTorus3D <class_CSGTorus3D>`
- :ref:`CSGPolygon3D <class_CSGPolygon3D>`
- :ref:`CSGMesh3D <class_CSGMesh3D>`
- :ref:`CSGCombiner3D <class_CSGCombiner3D>`

.. image:: img/csg_nodes.png

.. image:: img/csg_mesh.png

Các tính năng của công cụ CSG
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mỗi node CSG hỗ trợ 3 loại phép toán boolean:

- **Union:** Hình học của cả hai primitive được hợp nhất, phần hình học giao nhau bị loại bỏ.
- **Intersection:** Chỉ phần hình học giao nhau được giữ lại, phần còn lại bị loại bỏ.
- **Subtraction:** Hình dạng thứ hai được trừ khỏi hình dạng thứ nhất, để lại một phần lõm có hình dạng của nó.

.. image:: img/csg_operation_menu.png

.. image:: img/csg_operation.png

CSGPolygon
~~~~~~~~~~

Node :ref:`CSGPolygon3D <class_CSGPolygon3D>` extrude một Polygon được vẽ trong không gian 2D (theo tọa độ X, Y) theo các cách sau:

- **Depth:** Extrude về phía sau một khoảng đã cho.
- **Spin:** Extrude đồng thời xoay quanh gốc của nó.
- **Path:** Extrude dọc theo một node Path. Thao tác này thường được gọi là lofting.

.. image:: img/csg_poly_mode.png

.. image:: img/csg_poly.png

.. note:: Chế độ **Path** phải được cung cấp một node :ref:`Path3D <class_Path3D>` để hoạt động. Trong node Path, hãy vẽ đường dẫn; polygon trong CSGPolygon3D sẽ extrude dọc theo đường dẫn đã cho.


Mesh tùy chỉnh
~~~~~~~~~~~~~~

Có thể sử dụng mesh tùy chỉnh cho :ref:`CSGMesh3D <class_CSGMesh3D>` miễn là mesh đó *manifold*. Mesh có thể được tạo trong phần mềm khác rồi import vào Godot. Có hỗ trợ nhiều material.

Để được sử dụng làm mesh CSG, một mesh cần:

- khép kín
- có mỗi cạnh chỉ nối với đúng hai mặt
- có thể tích

Ngoài ra, bạn nên tránh:

- thể tích âm
- tự giao nhau
- các mặt bên trong

Godot sử dụng thư viện `manifold <https://github.com/elalish/manifold>`__ để triển khai mesh CSG. Định nghĩa kỹ thuật về "manifold" được Godot sử dụng như sau, được chuyển thể từ `definition of "manifold" <https://github.com/elalish/manifold/wiki/Manifold-Library#manifoldness-definition>`__ của thư viện đó:

  Mỗi cạnh của mỗi tam giác phải chứa cùng hai đỉnh (theo index) với đúng một cạnh tam giác khác, đồng thời đỉnh đầu và đỉnh cuối phải đổi chỗ cho nhau giữa hai cạnh này. Các đỉnh của tam giác phải xuất hiện theo thứ tự clockwise khi nhìn từ bên ngoài mesh manifold của Godot Engine.

.. image:: img/csg_custom_mesh.png

Biến một mesh hiện có thành manifold bằng Blender
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. UPDATE: This relies on a specific Blender addon. If it becomes unsupported,
.. we can remove this section.

Nếu bạn có một mesh hiện có chưa phải là manifold, bạn có thể dùng Blender để biến nó thành manifold.

Trong Blender, hãy cài đặt và bật addon `3D Print Toolbox <https://extensions.blender.org/add-ons/print3d-toolbox/>`_.

Chọn mesh bạn muốn biến thành manifold. Mở thanh bên bằng cách nhấp vào mũi tên:

.. image:: img/csg_manifold_step_1.webp

Trong tab **3D Print**, bên dưới **Clean Up**, hãy nhấp vào nút **Make Manifold**:

.. image:: img/csg_manifold_step_2.webp

Mesh giờ đây sẽ là manifold và có thể được sử dụng làm mesh tùy chỉnh.

CSGCombiner3D
~~~~~~~~~~~~~

Node :ref:`CSGCombiner3D <class_CSGCombiner3D>` là một hình dạng rỗng dùng để tổ chức. Node này chỉ kết hợp các node con.

Thứ tự xử lý
~~~~~~~~~~~~

Mỗi node CSG trước tiên sẽ xử lý các node con và các phép toán của chúng: union, intersection hoặc subtraction, theo thứ tự trong cây, rồi lần lượt áp dụng chúng lên chính nó.

.. note:: Để đảm bảo hiệu năng, hãy giữ hình học CSG tương đối đơn giản, vì các mesh phức tạp có thể mất khá nhiều thời gian để xử lý. Nếu kết hợp các đối tượng với nhau (chẳng hạn như đối tượng cái bàn và căn phòng), hãy tạo chúng thành các cây CSG riêng biệt. Việc ép quá nhiều đối tượng vào cùng một cây cuối cùng sẽ bắt đầu ảnh hưởng đến hiệu năng. Chỉ sử dụng các phép toán nhị phân khi thực sự cần.

Tạo nguyên mẫu cho một level
----------------------------

Chúng ta sẽ tạo nguyên mẫu cho một căn phòng để thực hành sử dụng các công cụ CSG.

.. tip:: Làm việc trong phép chiếu **Orthogonal** sẽ cho góc nhìn tốt hơn khi kết hợp các hình dạng CSG.

Level của chúng ta sẽ chứa các đối tượng sau:

- một căn phòng,
- một chiếc giường,
- một chiếc đèn,
- một chiếc bàn,
- một giá sách.

Tạo một scene với một node Node3D làm node gốc.

.. tip:: Ánh sáng mặc định của môi trường không cung cấp shading rõ ràng ở một số góc. Thay đổi chế độ hiển thị bằng **Display Overdraw** trong menu viewport 3D, hoặc thêm một node DirectionalLight để giúp bạn nhìn rõ hơn.

.. image:: img/csg_overdraw.png

Tạo một CSGBox3D và đặt tên là ``room``, bật **Invert Faces** rồi thay đổi kích thước căn phòng.

.. image:: img/csg_room.png

.. image:: img/csg_room_invert.png

Tiếp theo, tạo một CSGCombiner3D và đặt tên là ``desk``.

Một chiếc bàn có một mặt bàn và 4 chân:

- Tạo 1 node con CSGBox3D ở chế độ **Union** cho bề mặt và điều chỉnh kích thước.
- Tạo 4 node con CSGBox3D ở chế độ **Union** cho các chân và điều chỉnh kích thước.

Điều chỉnh vị trí của chúng để trông giống một chiếc bàn.

.. image:: img/csg_desk.png

.. note:: Các node CSG bên trong một CSGCombiner3D chỉ xử lý phép toán của chúng trong combiner đó. Vì vậy, CSGCombiner3D được dùng để tổ chức các node CSG.

Tạo một CSGCombiner3D và đặt tên là ``bed``.

Chiếc giường của chúng ta gồm 3 phần: giường, nệm và gối. Tạo một CSGBox3D và điều chỉnh kích thước của nó cho phần giường. Tạo một CSGBox3D khác và điều chỉnh kích thước của nó cho phần nệm.

.. image:: img/csg_bed_mat.png

Chúng ta sẽ tạo một CSGCombiner3D khác có tên ``pillow`` làm node con của ``bed``. Cây scene sẽ trông như sau:

.. image:: img/csg_bed_tree.png

Chúng ta sẽ kết hợp 3 node CSGSphere3D ở chế độ **Union** để tạo thành một chiếc gối. Scale trục Y của các hình cầu và bật **Smooth Faces**.

.. image:: img/csg_pillow_smooth.png

Chọn node ``pillow`` và chuyển chế độ sang **Subtraction**; các hình cầu đã kết hợp sẽ khoét một lỗ trên nệm.

.. image:: img/csg_pillow_hole.png

Hãy thử chuyển node ``pillow`` làm node con của node gốc ``Node3D``; cái lỗ sẽ biến mất.

.. note:: Điều này minh họa ảnh hưởng của thứ tự xử lý CSG. Vì node gốc không phải là node CSG, các node CSGCombiner3D là điểm kết thúc của các phép toán; điều này cho thấy cách dùng CSGCombiner3D để tổ chức scene CSG.

Hoàn tác thao tác chuyển node con sau khi quan sát ảnh hưởng. Chiếc giường bạn đã dựng sẽ trông như sau:

.. image:: img/csg_bed.png

Tạo một CSGCombiner3D và đặt tên là ``lamp``.

Một chiếc đèn gồm 3 phần: đế, thân và chụp đèn. Tạo một CSGCylinder3D, bật tùy chọn **Cone** và dùng nó làm đế. Tạo một CSGCylinder3D khác và điều chỉnh kích thước để dùng nó làm thân đèn.

.. image:: img/csg_lamp_pole_stand.png

Chúng ta sẽ dùng một CSGPolygon3D cho chụp đèn. Dùng chế độ **Spin** cho CSGPolygon3D và vẽ một `trapezoid <https://en.wikipedia.org/wiki/Trapezoid>`_ khi đang ở **Front View** (bàn phím số 1); hình dạng này sẽ đùn quanh gốc tọa độ và tạo thành chụp đèn.

.. image:: img/csg_lamp_spin.png

.. image:: img/csg_lamp_polygon.png

.. image:: img/csg_lamp_extrude.png

Điều chỉnh vị trí của 3 phần để chúng trông giống một chiếc đèn.

.. image:: img/csg_lamp.png

Tạo một CSGCombiner3D và đặt tên là ``bookshelf``.

Chúng ta sẽ dùng 3 node CSGBox3D cho giá sách. Tạo một CSGBox3D và điều chỉnh kích thước của nó; đây sẽ là kích thước của giá sách.

.. image:: img/csg_shelf_big.png

Nhân bản CSGBox3D, thu nhỏ kích thước trên mỗi trục và chuyển chế độ sang **Subtraction**.

.. image:: img/csg_shelf_subtract.png

.. image:: img/csg_shelf_subtract_menu.png

Bạn gần như đã dựng xong một chiếc kệ. Tạo thêm một CSGBox3D để chia kệ thành hai tầng.

.. image:: img/csg_shelf.png

Đặt đồ nội thất trong phòng theo ý muốn; scene của bạn sẽ trông như sau:

.. image:: img/csg_room_result.png

Bạn đã dựng thành công prototype cho một level phòng bằng các công cụ CSG trong Godot. Công cụ CSG có thể được dùng để thiết kế mọi loại level, chẳng hạn như mê cung hoặc thành phố; hãy khám phá các giới hạn của chúng khi thiết kế game.

Sử dụng texture prototype
-------------------------

:ref:`doc_standard_material_3d` của Godot hỗ trợ *triplanar mapping*, có thể được dùng để tự động áp dụng texture lên các đối tượng bất kỳ mà không gây biến dạng. Điều này rất hữu ích khi dùng CSG vì Godot hiện chưa hỗ trợ chỉnh sửa UV map trên các node CSG. Triplanar mapping tương đối chậm, nên thường chỉ được dùng cho các bề mặt hữu cơ như địa hình. Tuy nhiên, khi làm prototype, bạn có thể dùng nó để nhanh chóng áp dụng texture cho các level dựa trên CSG.

.. note:: Nếu cần một số texture để làm prototype, Kenney đã tạo một `bộ texture prototype được cấp phép CC0 <https://kenney.nl/assets/prototype-textures>`__.

Có hai cách để áp dụng material cho một node CSG:

- Áp dụng nó cho một node CSGCombiner3D dưới dạng material override (**Geometry > Material Override** trong Inspector). Cách này sẽ tự động ảnh hưởng đến các node con, nhưng khiến bạn không thể thay đổi material trên từng node con riêng lẻ.
- Áp dụng material cho từng node riêng lẻ (**Material** trong Inspector). Theo cách này, mỗi node CSG có thể có giao diện riêng. Các node CSG thực hiện phép trừ sẽ áp dụng material của chúng cho các node mà chúng đang "đào" vào.

Để áp dụng triplanar mapping cho một node CSG, hãy chọn node đó, đi đến Inspector, nhấp vào dòng chữ **[empty]** bên cạnh **Material Override** (hoặc **Material** đối với các node CSG riêng lẻ). Chọn **New StandardMaterial3D**. Nhấp vào biểu tượng của material vừa tạo để chỉnh sửa. Mở phần **Albedo** và nạp texture vào thuộc tính **Texture**. Tiếp theo, mở phần **Uv1** và chọn **Triplanar**. Bạn có thể thay đổi offset và scale của texture trên từng trục bằng cách điều chỉnh các thuộc tính **Scale** và **Offset** ngay phía trên. Giá trị trong thuộc tính **Scale** càng cao thì texture sẽ lặp lại càng thường xuyên.

.. tip:: Bạn có thể sao chép một StandardMaterial3D để sử dụng lại trên các node CSG. Để làm vậy, nhấp vào mũi tên thả xuống bên cạnh thuộc tính material trong Inspector và chọn **Copy**. Để dán, chọn node mà bạn muốn áp dụng material, nhấp vào mũi tên thả xuống bên cạnh thuộc tính material của node đó rồi chọn **Paste**.

.. _doc_csg_tools_converting_to_mesh_instance_3d:

Chuyển đổi sang MeshInstance3D
------------------------------

Kể từ Godot 4.4, bạn có thể chuyển đổi một node CSG và các node con của nó thành một node :ref:`class_MeshInstance3D`.

Điều này mang lại một số lợi ích:

- Bake lightmap, vì UV2 có thể được tạo trên một MeshInstance3D.
- Bake occlusion culling, vì quy trình bake occlusion culling chỉ tính đến MeshInstance3D.
- Thời gian tải nhanh hơn, vì mesh CSG không còn cần được dựng lại khi scene tải.
- Hiệu suất tốt hơn khi cập nhật transform của node nếu sử dụng mesh bên trong một node CSG khác.

Để chuyển đổi một node CSG thành node MeshInstance3D, hãy chọn node đó, sau đó chọn **CSG > Bake Mesh Instance** trên thanh công cụ. Node MeshInstance3D sẽ được tạo dưới dạng node cùng cấp. Lưu ý rằng node CSG được dùng để bake **không** tự động bị ẩn, vì vậy hãy nhớ ẩn nó để tránh hình học của nó chồng lấn với MeshInstance3D mới được tạo.

Bạn cũng có thể tạo collision shape dạng trimesh bằng **CSG > Bake Collision Shape**. Node :ref:`class_CollisionShape3D` được tạo phải là node con của một node :ref:`class_StaticBody3D` hoặc :ref:`class_AnimatableBody3D` thì mới có hiệu lực.

.. tip::

    Hãy nhớ giữ lại node CSG ban đầu trong cây cảnh để bạn có thể thay đổi hình học sau này nếu cần. Để thay đổi hình học, hãy xóa node MeshInstance3D và hiển thị lại node CSG gốc.

Xuất dưới dạng glTF
-------------------

Việc phác thảo một level bằng CSG rồi xuất dưới dạng mô hình 3D để nhập vào phần mềm modeling 3D có thể rất hữu ích. Bạn có thể thực hiện việc này bằng cách chọn **Scene > Export As... > glTF 2.0 Scene**.

.. image:: img/export_as_gltf.webp

.. _`3D Print Toolbox`: https://extensions.blender.org/add-ons/print3d-toolbox/
.. _`trapezoid`: https://en.wikipedia.org/wiki/Trapezoid
