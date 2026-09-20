:article_outdated: True

.. _doc_csg_tools:

Tạo nguyên mẫu level bằng CSG
=============================

CSG là viết tắt của **Constructive Solid Geometry**, một công cụ để kết hợp các hình cơ bản hoặc mesh tùy chỉnh nhằm tạo ra các hình phức tạp hơn. Trong phần mềm modeling 3D, CSG thường được biết đến với tên gọi "Boolean Operators".

Tạo nguyên mẫu level là một trong những cách sử dụng chính của CSG trong Godot. Kỹ thuật này cho phép người dùng tạo các hình dạng phổ biến nhất bằng cách kết hợp các primitive. Có thể tạo môi trường nội thất bằng cách sử dụng các primitive đảo ngược.

.. note:: The CSG nodes in Godot are mainly intended for prototyping. There is
          không có hỗ trợ tích hợp cho UV mapping hoặc chỉnh sửa các polygon 3D (mặc dù có thể sử dụng polygon 2D được extrude với node CSGPolygon3D).

          Nếu bạn đang tìm một công cụ thiết kế level dễ sử dụng cho dự án, bạn có thể muốn sử dụng `FuncGodot <https://github.com/func-godot/func_godot_plugin>`__ hoặc `Cyclops Level Builder <https://github.com/blackears/cyclopsLevelBuilder>`__ thay thế.

.. video:: video/csg_tools.webm
   :alt: CSG being used to subtract a torus shape from a box
   :autoplay:
   :loop:
   :muted:
   :align: default

.. seealso::

    Bạn có thể xem cách sử dụng các node CSG để xây dựng nhiều hình dạng khác nhau (chẳng hạn như cầu thang hoặc đường đi) bằng `Constructive Solid Geometry demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/csg>`__.

Giới thiệu về các node CSG
--------------------------

Giống như các tính năng khác của Godot, CSG được hỗ trợ dưới dạng các node. Đây là các node CSG:

- :ref:`CSGBox3D <class_CSGBox3D>` - :ref:`CSGCylinder3D <class_CSGCylinder3D>` (cũng hỗ trợ cone) - :ref:`CSGSphere3D <class_CSGSphere3D>` - :ref:`CSGTorus3D <class_CSGTorus3D>` - :ref:`CSGPolygon3D <class_CSGPolygon3D>` - :ref:`CSGMesh3D <class_CSGMesh3D>` - :ref:`CSGCombiner3D <class_CSGCombiner3D>`

.. image:: img/csg_nodes.png

.. image:: img/csg_mesh.png

Các tính năng của công cụ CSG
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mỗi node CSG hỗ trợ 3 loại phép toán boolean:

- **Union:** Hình học của cả hai primitive được hợp nhất, phần hình học giao nhau bị loại bỏ. - **Intersection:** Chỉ phần hình học giao nhau được giữ lại, phần còn lại bị loại bỏ. - **Subtraction:** Hình thứ hai bị trừ khỏi hình thứ nhất, để lại một phần lõm có hình dạng của nó.

.. image:: img/csg_operation_menu.png

.. image:: img/csg_operation.png

CSGPolygon
~~~~~~~~~~

Node :ref:`CSGPolygon3D <class_CSGPolygon3D>` extrude một Polygon được vẽ trong không gian 2D (theo tọa độ X, Y) theo các cách sau:

- **Depth:** Extrude về phía sau một khoảng xác định. - **Spin:** Extrude đồng thời xoay quanh gốc của nó. - **Path:** Extrude dọc theo một node Path. Phép toán này thường được gọi là lofting.

.. image:: img/csg_poly_mode.png

.. image:: img/csg_poly.png

.. note:: The **Path** mode must be provided with a :ref:`Path3D <class_Path3D>`
          node để hoạt động. Trong node Path, hãy vẽ path; polygon trong CSGPolygon3D sẽ được extrude dọc theo path đã cho.


Mesh tùy chỉnh
~~~~~~~~~~~~~~

Có thể sử dụng mesh tùy chỉnh cho :ref:`CSGMesh3D <class_CSGMesh3D>` miễn là mesh đó là *manifold*. Mesh có thể được modeling trong phần mềm khác rồi import vào Godot. Có hỗ trợ nhiều material.

Để một mesh có thể được sử dụng làm mesh CSG, mesh đó phải:

- khép kín - mỗi edge chỉ kết nối với đúng hai face - có volume

Ngoài ra, bạn nên tránh:

- volume âm - self-intersection - các face bên trong

Godot sử dụng thư viện `manifold <https://github.com/elalish/manifold>`__ để triển khai mesh CSG. Định nghĩa kỹ thuật của "manifold" được Godot sử dụng như sau, được điều chỉnh từ `definition of "manifold" <https://github.com/elalish/manifold/wiki/Manifold-Library#manifoldness-definition>`__ của thư viện đó:

  Mỗi edge của mọi triangle phải chứa cùng hai vertex (theo index) như chính xác một edge khác của triangle, đồng thời vertex bắt đầu và kết thúc phải đổi vị trí cho nhau giữa hai edge này. Các vertex của triangle phải xuất hiện theo thứ tự clockwise khi nhìn từ bên ngoài mesh manifold của Godot Engine.

.. image:: img/csg_custom_mesh.png

Làm cho mesh hiện có trở thành manifold bằng Blender
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. CẬP NHẬT: Phần này phụ thuộc vào một Blender addon cụ thể. Nếu addon này không còn được hỗ trợ, .. chúng ta có thể xóa phần này.

Nếu bạn có một mesh hiện có chưa phải là manifold, bạn có thể làm cho nó trở thành manifold bằng Blender.

Trong Blender, hãy cài đặt và bật addon `3D Print Toolbox <https://extensions.blender.org/add-ons/print3d-toolbox/>`_.

Chọn mesh bạn muốn làm cho trở thành manifold. Mở sidebar bằng cách nhấp vào mũi tên:

.. image:: img/csg_manifold_step_1.webp

Trong tab **3D Print**, bên dưới **Clean Up**, hãy nhấp vào nút **Make Manifold**:

.. image:: img/csg_manifold_step_2.webp

Mesh giờ đây sẽ là manifold và có thể được sử dụng làm mesh tùy chỉnh.

CSGCombiner3D
~~~~~~~~~~~~~

Node :ref:`CSGCombiner3D <class_CSGCombiner3D>` là một shape rỗng được dùng để tổ chức. Node này chỉ kết hợp các node con.

Thứ tự xử lý
~~~~~~~~~~~~

Mỗi node CSG trước tiên sẽ xử lý các node con và phép toán của chúng: union, intersection hoặc subtraction, theo thứ tự trong cây, rồi lần lượt áp dụng chúng vào chính nó.

.. note:: In the interest of performance, make sure CSG geometry remains
          tương đối đơn giản, vì các mesh phức tạp có thể mất một lúc để xử lý. Nếu cộng các object với nhau (chẳng hạn như object bàn và phòng), hãy tạo chúng dưới dạng các cây CSG riêng biệt. Việc ép quá nhiều object vào một cây cuối cùng sẽ bắt đầu ảnh hưởng đến hiệu năng. Chỉ sử dụng các phép toán nhị phân khi thực sự cần.

Tạo nguyên mẫu một level
------------------------

Chúng ta sẽ tạo nguyên mẫu một căn phòng để thực hành sử dụng các công cụ CSG.

.. tip:: Working in **Orthogonal** projection gives a better view when combining
         các shape CSG.

Level của chúng ta sẽ chứa các object sau:

- một căn phòng, - một chiếc giường, - một chiếc đèn, - một chiếc bàn, - một kệ sách.

Tạo một scene với node Node3D làm node gốc.

.. tip:: The default lighting of the environment doesn't provide clear shading
         ở một số góc nhìn. Thay đổi chế độ hiển thị bằng **Display Overdraw** trong menu viewport 3D, hoặc thêm một node DirectionalLight để giúp bạn nhìn rõ hơn.

.. image:: img/csg_overdraw.png

Tạo một CSGBox3D và đặt tên là ``room``, bật **Invert Faces** rồi thay đổi kích thước theo căn phòng của bạn.

.. image:: img/csg_room.png

.. image:: img/csg_room_invert.png

Tiếp theo, tạo một CSGCombiner3D và đặt tên là ``desk``.

Một chiếc bàn có một mặt bàn và 4 chân:

- Tạo 1 node con CSGBox3D ở chế độ **Union** cho mặt bàn và điều chỉnh kích thước. - Tạo 4 node con CSGBox3D ở chế độ **Union** cho các chân bàn và điều chỉnh kích thước.

Điều chỉnh vị trí của chúng để trông giống một chiếc bàn.

.. image:: img/csg_desk.png

.. note:: CSG nodes inside a CSGCombiner3D will only process their operation
          bên trong combiner. Vì vậy, CSGCombiner3D được dùng để tổ chức các node CSG.

Tạo một CSGCombiner3D và đặt tên là ``bed``.

Chiếc giường của chúng ta gồm 3 phần: khung giường, nệm và gối. Tạo một CSGBox3D và điều chỉnh kích thước cho khung giường. Tạo một CSGBox3D khác và điều chỉnh kích thước cho nệm.

.. image:: img/csg_bed_mat.png

Chúng ta sẽ tạo một CSGCombiner3D khác có tên ``pillow`` làm node con của ``bed``. Cây scene sẽ trông như sau:

.. image:: img/csg_bed_tree.png

Chúng ta sẽ kết hợp 3 node CSGSphere3D ở chế độ **Union** để tạo thành một chiếc gối. Scale trục Y của các sphere và bật **Smooth Faces**.

.. image:: img/csg_pillow_smooth.png

Chọn node ``pillow`` và chuyển chế độ sang **Subtraction**; các sphere đã kết hợp sẽ cắt một lỗ vào nệm.

.. image:: img/csg_pillow_hole.png

Hãy thử re-parent node ``pillow`` vào node gốc ``Node3D``; cái lỗ sẽ biến mất.

.. note:: This is to illustrate the effect of CSG processing order.
          Vì node gốc không phải là node CSG, các node CSGCombiner3D là điểm kết thúc của các phép toán; điều này cho thấy cách sử dụng CSGCombiner3D để tổ chức scene CSG.

Undo thao tác re-parent sau khi quan sát hiệu ứng. Chiếc giường bạn đã xây dựng sẽ trông như sau:

.. image:: img/csg_bed.png

Tạo một CSGCombiner3D và đặt tên là ``lamp``.

Một chiếc đèn gồm 3 phần: chân đế, thân và chụp đèn. Tạo một CSGCylinder3D, bật tùy chọn **Cone** và dùng nó làm chân đế. Tạo một CSGCylinder3D khác và điều chỉnh kích thước để dùng làm thân đèn.

.. image:: img/csg_lamp_pole_stand.png

Chúng ta sẽ sử dụng một CSGPolygon3D cho chụp đèn. Sử dụng chế độ **Spin** cho CSGPolygon3D và vẽ một `trapezoid <https://en.wikipedia.org/wiki/Trapezoid>`_ trong khi ở **Front View** (bàn phím số 1); shape này sẽ extrude quanh gốc và tạo thành chụp đèn.

.. image:: img/csg_lamp_spin.png

.. image:: img/csg_lamp_polygon.png

.. image:: img/csg_lamp_extrude.png

Điều chỉnh vị trí của 3 phần để chúng trông giống một chiếc đèn.

.. image:: img/csg_lamp.png

Tạo một CSGCombiner3D và đặt tên là ``bookshelf``.

Chúng ta sẽ sử dụng 3 node CSGBox3D cho kệ sách. Tạo một CSGBox3D và điều chỉnh kích thước; đây sẽ là kích thước của kệ sách.

.. image:: img/csg_shelf_big.png

Nhân bản CSGBox3D, thu nhỏ kích thước trên mỗi trục và chuyển chế độ sang **Subtraction**.

.. image:: img/csg_shelf_subtract.png

.. image:: img/csg_shelf_subtract_menu.png

Bạn gần như đã xây dựng xong một chiếc kệ. Tạo thêm một CSGBox3D để chia kệ thành hai tầng.

.. image:: img/csg_shelf.png

Đặt đồ nội thất vào căn phòng theo ý muốn; scene của bạn sẽ trông như sau:

.. image:: img/csg_room_result.png

Bạn đã tạo nguyên mẫu thành công một level phòng bằng các công cụ CSG trong Godot. Có thể sử dụng công cụ CSG để thiết kế mọi loại level, chẳng hạn như mê cung hoặc thành phố; hãy khám phá các giới hạn của nó khi thiết kế game.

Sử dụng texture nguyên mẫu
--------------------------

:ref:`doc_standard_material_3d` của Godot hỗ trợ *triplanar mapping*, có thể được sử dụng để tự động áp dụng texture lên các object tùy ý mà không gây biến dạng. Điều này rất hữu ích khi sử dụng CSG, vì Godot hiện chưa hỗ trợ chỉnh sửa UV map trên các node CSG. Triplanar mapping tương đối chậm, nên thông thường việc sử dụng nó bị giới hạn ở các bề mặt hữu cơ như địa hình. Tuy vậy, khi tạo nguyên mẫu, bạn có thể dùng nó để nhanh chóng áp dụng texture cho các level dựa trên CSG.

.. note:: If you need some textures for prototyping, Kenney made a
          `set of CC0-licensed prototype textures <https://kenney.nl/assets/prototype-textures>`__.

Có hai cách để áp dụng material cho một node CSG:

- Áp dụng material cho node CSGCombiner3D dưới dạng material override (**Geometry > Material Override** trong Inspector). Cách này sẽ tự động ảnh hưởng đến các node con, nhưng khiến bạn không thể thay đổi material trên từng node con. - Áp dụng material cho từng node riêng lẻ (**Material** trong Inspector). Theo cách này, mỗi node CSG có thể có diện mạo riêng. Các node CSG dạng subtractive sẽ áp dụng material của chúng lên các node mà chúng đang "đào" vào.

Để áp dụng triplanar mapping cho một node CSG, hãy chọn node đó, đi đến Inspector, nhấp vào văn bản **[empty]** bên cạnh **Material Override** (hoặc **Material** đối với các node CSG riêng lẻ). Chọn **New StandardMaterial3D**. Nhấp vào biểu tượng của material vừa tạo để chỉnh sửa. Mở rộng phần **Albedo** và tải một texture vào thuộc tính **Texture**. Tiếp theo, mở rộng phần **Uv1** và đánh dấu **Triplanar**. Bạn có thể thay đổi offset và scale của texture trên từng trục bằng cách điều chỉnh các thuộc tính **Scale** và **Offset** ngay phía trên. Giá trị trong thuộc tính **Scale** càng cao thì texture sẽ lặp lại càng thường xuyên.

.. tip:: You can copy a StandardMaterial3D to reuse it across CSG nodes. To do so,
         Nhấp vào mũi tên dropdown bên cạnh một thuộc tính material trong Inspector và chọn **Copy**. Để dán, hãy chọn node mà bạn muốn áp dụng material, nhấp vào mũi tên dropdown bên cạnh thuộc tính material của node đó rồi chọn **Paste**.

.. _doc_csg_tools_converting_to_mesh_instance_3d:

Chuyển đổi thành MeshInstance3D
-------------------------------

Kể từ Godot 4.4, bạn có thể chuyển đổi một node CSG và các node con của nó thành một node :ref:`class_MeshInstance3D`.

Điều này mang lại một số lợi ích:

- Bake lightmap, vì UV2 có thể được tạo trên một MeshInstance3D. - Bake occlusion culling, vì quy trình bake occlusion culling chỉ tính đến MeshInstance3D. - Thời gian tải nhanh hơn, vì mesh CSG không còn cần được dựng lại khi scene tải. - Hiệu năng tốt hơn khi cập nhật transform của node nếu sử dụng mesh bên trong một node CSG khác.

Để chuyển đổi một node CSG thành node MeshInstance3D, hãy chọn node đó, sau đó chọn **CSG > Bake Mesh Instance** trên thanh công cụ. Node MeshInstance3D sẽ được tạo dưới dạng sibling. Lưu ý rằng node CSG được dùng để bake sẽ **không** tự động bị ẩn, vì vậy hãy nhớ ẩn node đó để ngăn hình học của nó chồng lên MeshInstance3D mới được tạo.

Bạn cũng có thể tạo một collision shape dạng trimesh bằng **CSG > Bake Collision Shape**. Node :ref:`class_CollisionShape3D` được tạo phải là node con của node :ref:`class_StaticBody3D` hoặc :ref:`class_AnimatableBody3D` thì mới có hiệu lực.

.. tip::

    Hãy nhớ giữ node CSG ban đầu trong scene tree để sau này bạn có thể thực hiện các thay đổi đối với hình học nếu cần. Để thay đổi hình học, hãy xóa node MeshInstance3D và hiển thị lại node CSG gốc.

Xuất dưới dạng glTF
-------------------

Việc dựng khối một level bằng CSG rồi xuất nó dưới dạng mô hình 3D để nhập vào phần mềm modeling 3D có thể rất hữu ích. Bạn có thể thực hiện việc này bằng cách chọn **Scene > Export As... > glTF 2.0 Scene**.

.. image:: img/export_as_gltf.webp
