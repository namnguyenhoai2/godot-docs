.. _doc_importing_3d_scenes_node_type_customization:

Tùy chỉnh loại node bằng hậu tố tên
===================================

Nhiều khi, khi chỉnh sửa một scene, có những tác vụ phổ biến cần được thực hiện sau khi export:

- Thêm tính năng phát hiện va chạm cho các đối tượng.
- Thiết lập các đối tượng làm navigation mesh.
- Xóa các node không được sử dụng trong game engine (chẳng hạn như các đèn cụ thể dùng để modeling).

Để đơn giản hóa quy trình này, Godot cung cấp một số hậu tố có thể thêm vào tên của các đối tượng trong phần mềm modeling 3D. Khi import, Godot sẽ phát hiện các hậu tố trong tên đối tượng và tự động thực hiện các hành động tương ứng.

.. warning::

    Tất cả các hậu tố được mô tả dưới đây đều có thể được sử dụng với ``-``, ``$`` và ``_``, đồng thời **case-insensitive**.

Không sử dụng
-------------

Nếu không muốn Godot thực hiện bất kỳ hành động nào được mô tả dưới đây, bạn có thể đặt tùy chọn import ``nodes/use_node_type_suffixes`` thành ``false``. Thao tác này sẽ vô hiệu hóa tất cả hậu tố loại node, giữ cho các node có cùng loại như được chỉ định trong tệp gốc. Tuy nhiên, hậu tố ``-noimp`` vẫn được áp dụng, cũng như các hậu tố không phải node như ``-vcol`` hoặc ``-loop``.

Ngoài ra, bạn có thể hoàn toàn không sử dụng tất cả hậu tố tên bằng cách đặt tùy chọn import ``nodes/use_name_suffixes`` thành ``false``. Thao tác này sẽ khiến mã import scene chung hoàn toàn không xét đến các hậu tố tên. Tuy nhiên, mã import dành riêng cho định dạng vẫn có thể xét đến các hậu tố tên, chẳng hạn như glTF importer kiểm tra hậu tố ``-loop``.

Việc vô hiệu hóa các tùy chọn này khiến các tệp được import trong editor giống các tệp gốc hơn và cũng giống hơn với việc import tệp tại runtime. Để có quy trình import hoạt động tại runtime, cho kết quả dễ dự đoán hơn và chỉ có hành vi được định nghĩa rõ ràng, hãy cân nhắc đặt các tùy chọn này thành ``false`` và sử dụng :ref:`class_GLTFDocumentExtension` thay thế.

Xóa node và animation (-noimp)
------------------------------

Các node và animation có hậu tố ``-noimp`` sẽ bị xóa tại thời điểm import, bất kể loại của chúng là gì. Chúng sẽ không xuất hiện trong scene đã import.

Điều này tương đương với việc bật **Skip Import** cho một node trong hộp thoại Advanced Import Settings.

Tạo va chạm (-col, -convcol, -colonly, -convcolonly)
----------------------------------------------------

Tùy chọn ``-col`` chỉ hoạt động với các đối tượng Mesh. Khi được phát hiện, một node va chạm tĩnh con sẽ được thêm vào, sử dụng cùng hình học với mesh. Thao tác này sẽ tạo một collision shape dạng triangle mesh, đây là tùy chọn chậm nhưng chính xác để phát hiện va chạm. Tùy chọn này thường là lựa chọn bạn cần cho hình học của level (nhưng cũng xem ``-colonly`` bên dưới).

Tùy chọn ``-convcol`` sẽ tạo một :ref:`class_ConvexPolygonShape3D` thay vì một :ref:`class_ConcavePolygonShape3D`. Không giống triangle mesh có thể lõm, một shape lồi chỉ có thể biểu diễn chính xác một shape không có góc lõm nào (kim tự tháp là shape lồi, còn một hộp rỗng là shape lõm). Vì vậy, các collision shape lồi nhìn chung không phù hợp với hình học của level. Khi biểu diễn các mesh đủ đơn giản, collision shape lồi có thể cho hiệu năng tốt hơn so với collision shape dạng triangle. Tùy chọn này lý tưởng cho các đối tượng đơn giản hoặc động, cần khả năng phát hiện va chạm tương đối chính xác.

Tuy nhiên, trong cả hai trường hợp, hình học trực quan có thể quá phức tạp hoặc không đủ mượt để dùng làm va chạm. Điều này có thể gây ra lỗi vật lý và khiến engine chậm đi một cách không cần thiết.

Để giải quyết vấn đề này, modifier ``-colonly`` được cung cấp. Modifier này sẽ xóa mesh khi import và thay vào đó tạo một collision :ref:`class_StaticBody3D`. Nhờ đó, mesh trực quan và va chạm thực tế được tách biệt.

Tùy chọn ``-convcolonly`` hoạt động tương tự, nhưng sẽ tạo một
:ref:`class_ConvexPolygonShape3D` thay vào đó bằng cách sử dụng convex decomposition.

Với các tệp Collada, tùy chọn ``-colonly`` cũng có thể được sử dụng với các empty object của Blender. Khi import, tùy chọn này sẽ tạo một :ref:`class_StaticBody3D` với một node va chạm làm node con. Node va chạm sẽ có một trong số các shape được định nghĩa sẵn, tùy thuộc vào kiểu hiển thị empty của Blender:

.. figure:: img/importing_3d_scenes_blender_empty_draw_types.webp
   :align: center
   :alt: Chọn kiểu hiển thị cho một Empty khi tạo trong Blender

   Chọn kiểu hiển thị cho một Empty khi tạo trong Blender

- Single arrow sẽ tạo một :ref:`class_SeparationRayShape3D`.
- Cube sẽ tạo một :ref:`class_BoxShape3D`.
- Image sẽ tạo một :ref:`class_WorldBoundaryShape3D`.
- Sphere (và các kiểu khác không được liệt kê) sẽ tạo một :ref:`class_SphereShape3D`.

Khi có thể, **try to use a few primitive collision shapes** thay vì triangle mesh hoặc shape lồi. Các shape nguyên thủy thường có hiệu năng và độ tin cậy tốt nhất.

.. note::

    Để dễ quan sát hơn trong editor của Blender, bạn có thể bật tùy chọn "X-Ray" trên các collision empty và đặt màu riêng biệt cho chúng bằng cách thay đổi **Edit > Preferences > Themes > 3D Viewport > Empty**.

    Nếu sử dụng Blender 2.79 hoặc cũ hơn, thay vào đó hãy làm theo các bước sau: **User Preferences > Themes > 3D View > Empty**.

.. seealso::

    Xem :ref:`doc_collision_shapes_3d` để có cái nhìn tổng quan đầy đủ về các collision shape.

Tạo Occluder (-occ, -occonly)
-----------------------------

Nếu một mesh được import với hậu tố ``-occ``, một node :ref:`class_occluder3D` sẽ được tạo dựa trên hình học của mesh; node này không thay thế mesh. Một node mesh có hậu tố ``-occonly`` sẽ được chuyển đổi thành một
:ref:`class_occluder3D` khi import.

Tạo navigation (-navmesh)
-------------------------

Một node mesh có hậu tố ``-navmesh`` sẽ được chuyển đổi thành navigation mesh. Đối tượng Mesh gốc sẽ bị xóa tại thời điểm import.

Tạo VehicleBody (-vehicle)
--------------------------

Một node mesh có hậu tố ``-vehicle`` sẽ được import làm node con của một
:ref:`class_VehicleBody3D` node.

Tạo VehicleWheel (-wheel)
-------------------------

Một node mesh có hậu tố ``-wheel`` sẽ được import làm node con của một
:ref:`class_VehicleWheel3D` nút.

Thân cứng (-rigid)
------------------

Một nút mesh có hậu tố ``-rigid`` sẽ được nhập dưới dạng :ref:`class_RigidBody3D`.

Vòng lặp animation (-loop, -cycle)
----------------------------------

Các clip animation trong tệp 3D nguồn bắt đầu hoặc kết thúc bằng token ``loop`` hoặc ``cycle`` sẽ được nhập dưới dạng :ref:`class_Animation` của Godot với cờ loop được bật. **Không giống các hậu tố khác được mô tả ở trên, hậu tố này không yêu cầu dấu gạch nối.**

Trong Blender, việc này yêu cầu sử dụng NLA Editor và đặt tên Action với tiền tố hoặc hậu tố ``loop`` hoặc ``cycle``.

Alpha của material (-alpha)
---------------------------

Material có hậu tố ``-alpha`` sẽ được nhập với chế độ
transparency :ref:`TRANSPARENCY_ALPHA<class_BaseMaterial3D_constant_TRANSPARENCY_ALPHA>`.

Màu vertex của material (-vcol)
-------------------------------

Material có hậu tố ``-vcol`` sẽ được nhập với
các cờ :ref:`FLAG_ALBEDO_FROM_VERTEX_COLOR<class_BaseMaterial3D_constant_FLAG_ALBEDO_FROM_VERTEX_COLOR>` và
:ref:`FLAG_SRGB_VERTEX_COLOR<class_BaseMaterial3D_constant_FLAG_SRGB_VERTEX_COLOR>` được bật.
