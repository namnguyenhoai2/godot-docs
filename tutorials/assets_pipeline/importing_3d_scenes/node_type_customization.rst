.. _doc_importing_3d_scenes_node_type_customization:

Tùy chỉnh loại node bằng hậu tố tên
===================================

Nhiều khi, khi chỉnh sửa một scene, có những tác vụ phổ biến cần thực hiện sau khi export:

- Thêm tính năng phát hiện va chạm cho các object. - Đặt các object làm navigation mesh. - Xóa các node không được sử dụng trong game engine (chẳng hạn như các đèn cụ thể được dùng để modeling).

Để đơn giản hóa workflow này, Godot cung cấp một số hậu tố có thể thêm vào tên của các object trong phần mềm 3D modeling của bạn. Khi được import, Godot sẽ phát hiện các hậu tố trong tên object và tự động thực hiện các hành động tương ứng.

.. warning::

    Tất cả các hậu tố được mô tả bên dưới có thể được sử dụng với ``-``, ``Tất cả các hậu tố được mô tả bên dưới có thể được sử dụng với ``-``, ` và ``_``, đồng thời **không phân biệt chữ hoa chữ thường**.

Không sử dụng
-------------

Nếu không muốn Godot thực hiện bất kỳ hành động nào được mô tả bên dưới, bạn có thể đặt tùy chọn import ``nodes/use_node_type_suffixes`` thành ``false``. Điều này sẽ vô hiệu hóa tất cả hậu tố loại node, khiến các node giữ nguyên loại như được chỉ định trong file gốc. Tuy nhiên, hậu tố ``-noimp`` vẫn sẽ được áp dụng, cũng như các hậu tố không phải node như ``-vcol`` hoặc ``-loop``.

Ngoài ra, bạn có thể hoàn toàn không sử dụng tất cả hậu tố tên bằng cách đặt tùy chọn import ``nodes/use_name_suffixes`` thành ``false``. Điều này sẽ ngăn hoàn toàn mã import scene tổng quát kiểm tra các hậu tố tên. Tuy nhiên, mã import dành riêng cho từng định dạng vẫn có thể kiểm tra các hậu tố tên, chẳng hạn như glTF importer kiểm tra hậu tố ``-loop``.

Việc tắt các tùy chọn này khiến các file được editor import giống với file gốc hơn và giống với việc import file tại runtime hơn. Để có workflow import hoạt động tại runtime, cho kết quả dễ dự đoán hơn và chỉ có hành vi được định nghĩa rõ ràng, hãy cân nhắc đặt các tùy chọn này thành ``false`` và sử dụng :ref:`class_GLTFDocumentExtension` thay thế.

Xóa node và animation (-noimp)
------------------------------

Các node và animation có hậu tố ``-noimp`` sẽ bị xóa trong quá trình import, bất kể chúng thuộc loại nào. Chúng sẽ không xuất hiện trong scene đã import.

Điều này tương đương với việc bật **Skip Import** cho một node trong hộp thoại Advanced Import Settings.

Tạo collision (-col, -convcol, -colonly, -convcolonly)
------------------------------------------------------

Tùy chọn ``-col`` chỉ hoạt động với các Mesh object. Nếu được phát hiện, một static collision node con sẽ được thêm vào, sử dụng cùng geometry với mesh. Thao tác này sẽ tạo một triangle mesh collision shape, đây là tùy chọn chậm nhưng chính xác để phát hiện va chạm. Đây thường là tùy chọn bạn muốn dùng cho geometry của level (nhưng cũng xem ``-colonly`` bên dưới).

Tùy chọn ``-convcol`` sẽ tạo một :ref:`class_ConvexPolygonShape3D` thay vì một :ref:`class_ConcavePolygonShape3D`. Không giống triangle mesh, vốn có thể lõm, convex shape chỉ có thể biểu diễn chính xác một shape không có góc lõm nào (kim tự tháp là convex, nhưng hộp rỗng là lõm). Vì vậy, convex collision shape thường không phù hợp với geometry của level. Khi biểu diễn các mesh đủ đơn giản, convex collision shape có thể cho hiệu năng tốt hơn so với triangle collision shape. Tùy chọn này phù hợp với các object đơn giản hoặc động, cần khả năng phát hiện va chạm tương đối chính xác.

Tuy nhiên, trong cả hai trường hợp, geometry hiển thị có thể quá phức tạp hoặc không đủ mượt để dùng cho collision. Điều này có thể gây ra lỗi physics và làm engine chậm đi một cách không cần thiết.

Để giải quyết vấn đề này, modifier ``-colonly`` được cung cấp. Modifier này sẽ xóa mesh khi import và thay vào đó tạo một collision :ref:`class_StaticBody3D`. Điều này giúp tách mesh hiển thị và collision thực tế.

Tùy chọn ``-convcolonly`` hoạt động tương tự, nhưng sẽ tạo một
:ref:`class_ConvexPolygonShape3D` instead using convex decomposition.

Với các file Collada, tùy chọn ``-colonly`` cũng có thể được sử dụng với các empty object của Blender. Khi import, tùy chọn này sẽ tạo một :ref:`class_StaticBody3D` với một collision node làm node con. Collision node sẽ có một trong số các shape được định nghĩa sẵn, tùy thuộc vào draw type của empty trong Blender:

.. figure:: img/importing_3d_scenes_blender_empty_draw_types.webp
   :align: center
   :alt: Choosing a draw type for an Empty on creation in Blender

   Choosing a draw type for an Empty on creation in Blender

- Single arrow sẽ tạo một :ref:`class_SeparationRayShape3D`. - Cube sẽ tạo một :ref:`class_BoxShape3D`. - Image sẽ tạo một :ref:`class_WorldBoundaryShape3D`. - Sphere (và các loại khác không được liệt kê) sẽ tạo một :ref:`class_SphereShape3D`.

Khi có thể, **hãy cố gắng sử dụng một vài primitive collision shape** thay vì triangle mesh hoặc convex shape. Primitive shape thường có hiệu năng và độ tin cậy tốt nhất.

.. note::

    Để dễ nhìn hơn trong editor của Blender, bạn có thể bật tùy chọn "X-Ray" trên các collision empty và đặt màu riêng biệt cho chúng bằng cách thay đổi **Edit > Preferences > Themes > 3D Viewport > Empty**.

    Nếu sử dụng Blender 2.79 hoặc cũ hơn, hãy thực hiện theo các bước sau: **User Preferences > Themes > 3D View > Empty**.

.. seealso::

    Xem :ref:`doc_collision_shapes_3d` để có cái nhìn tổng quan đầy đủ về các collision shape.

Tạo Occluder (-occ, -occonly)
-----------------------------

Nếu một mesh được import với hậu tố ``-occ``, một node :ref:`class_occluder3D` sẽ được tạo dựa trên geometry của mesh; node này không thay thế mesh. Một mesh node có hậu tố ``-occonly`` sẽ được chuyển đổi thành một
:ref:`class_occluder3D` on import.

Tạo navigation (-navmesh)
-------------------------

Một mesh node có hậu tố ``-navmesh`` sẽ được chuyển đổi thành navigation mesh. Mesh object gốc sẽ bị xóa trong quá trình import.

Tạo VehicleBody (-vehicle)
--------------------------

Một mesh node có hậu tố ``-vehicle`` sẽ được import làm node con của một
:ref:`class_VehicleBody3D` node.

Tạo VehicleWheel (-wheel)
-------------------------

Một mesh node có hậu tố ``-wheel`` sẽ được import làm node con của một
:ref:`class_VehicleWheel3D` node.

Rigid Body (-rigid)
-------------------

Một mesh node có hậu tố ``-rigid`` sẽ được import dưới dạng một :ref:`class_RigidBody3D`.

Vòng lặp animation (-loop, -cycle)
----------------------------------

Các animation clip trong file 3D nguồn bắt đầu hoặc kết thúc bằng token ``loop`` hoặc ``cycle`` sẽ được import dưới dạng một Godot :ref:`class_Animation` với cờ loop được bật. **Không giống các hậu tố khác được mô tả ở trên, hậu tố này không yêu cầu dấu gạch nối.**

Trong Blender, thao tác này yêu cầu sử dụng NLA Editor và đặt tên Action với tiền tố hoặc hậu tố ``loop`` hoặc ``cycle``.

Alpha của material (-alpha)
---------------------------

Một material có hậu tố ``-alpha`` sẽ được import với
:ref:`TRANSPARENCY_ALPHA<class_BaseMaterial3D_constant_TRANSPARENCY_ALPHA>` transparency mode.

Màu vertex của material (-vcol)
-------------------------------

Một material có hậu tố ``-vcol`` sẽ được import với
:ref:`FLAG_ALBEDO_FROM_VERTEX_COLOR<class_BaseMaterial3D_constant_FLAG_ALBEDO_FROM_VERTEX_COLOR>` and
:ref:`FLAG_SRGB_VERTEX_COLOR<class_BaseMaterial3D_constant_FLAG_SRGB_VERTEX_COLOR>` flags set.
