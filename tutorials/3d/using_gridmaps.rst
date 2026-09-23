.. _doc_using_gridmaps:

Sử dụng GridMaps
================

Giới thiệu
----------

:ref:`Gridmaps <class_GridMap>` là công cụ để tạo các màn chơi game 3D, tương tự như cách :ref:`TileMap <doc_using_tilemaps>` hoạt động trong 2D. Bạn bắt đầu với một tập hợp được xác định trước gồm các mesh 3D (một
:ref:`class_MeshLibrary`) có thể được đặt trên một lưới, như thể bạn đang xây dựng một màn chơi với số lượng khối Lego không giới hạn.

Bạn cũng có thể thêm va chạm và điều hướng vào các mesh, giống như khi thêm chúng vào các tile của một tilemap.

Dự án mẫu
---------

Để tìm hiểu cách GridMaps hoạt động, trước tiên hãy tải xuống dự án mẫu: `gridmap_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/gridmap_starter.zip>`_.

Giải nén dự án này và thêm nó vào Project Manager bằng nút "Import". Có thể bạn sẽ nhận được một cửa sổ bật lên cho biết dự án cần được chuyển đổi sang phiên bản Godot mới hơn; hãy nhấp vào **Convert project.godot**.

Tạo MeshLibrary
---------------

Để bắt đầu, bạn cần một :ref:`class_MeshLibrary`, là một tập hợp các mesh riêng lẻ có thể được sử dụng trong gridmap. Mở scene "mesh_library_source.tscn" để xem ví dụ về cách thiết lập mesh library.

.. image:: img/gridmap_meshlibrary1.webp

Như bạn có thể thấy, scene này có một node :ref:`class_Node3D` làm node gốc và một số node con :ref:`class_MeshInstance3D`.

Nếu scene của bạn không cần physics thì bạn đã hoàn tất. Tuy nhiên, trong hầu hết trường hợp, bạn sẽ muốn gán các body va chạm cho các mesh.

Va chạm
-------

Bạn có thể gán thủ công một :ref:`class_StaticBody3D` và
:ref:`class_CollisionShape3D` cho mỗi mesh. Ngoài ra, bạn có thể sử dụng menu "Mesh" để tự động tạo body va chạm dựa trên dữ liệu mesh.

.. image:: img/gridmap_create_body.webp

Lưu ý rằng body va chạm "Convex" sẽ hoạt động tốt hơn đối với các mesh đơn giản. Với những hình dạng phức tạp hơn, hãy chọn "Create Trimesh Static Body". Khi mỗi mesh đã được gán physics body và collision shape, mesh library của bạn đã sẵn sàng để sử dụng.

.. image:: img/gridmap_mesh_scene.webp


Vật liệu
--------

Khi tạo mesh library, chỉ các vật liệu bên trong các mesh mới được sử dụng. Các vật liệu được thiết lập trên node sẽ bị bỏ qua.

NavigationMeshes
----------------

Giống như mọi mesh instance, các mục MeshLibrary có thể được gán một resource :ref:`class_NavigationMesh`, có thể được tạo thủ công hoặc bake như mô tả bên dưới.

Để tạo NavigationMesh từ scene export của MeshLibrary, hãy đặt một
:ref:`class_NavigationRegion3D` node con bên dưới MeshInstance3D chính cho mục GridMap. Thêm một resource NavigationMesh hợp lệ vào NavigationRegion3D, cùng một số node hình học nguồn bên dưới, rồi bake NavigationMesh.

.. note::

    Với các ô lưới nhỏ, thường cần giảm các thuộc tính NavigationMesh về bán kính agent và kích thước tối thiểu của region.

.. image:: img/meshlibrary_scene.png

Các node bên dưới NavigationRegion3D sẽ bị bỏ qua khi export scene MeshLibrary, vì vậy bạn có thể thêm các node khác làm hình học nguồn chỉ để bake navmesh.

.. warning::

    Kích thước ô đã bake của NavigationMesh phải khớp với kích thước ô bản đồ của NavigationServer để các navigation mesh của những ô lưới khác nhau được hợp nhất chính xác.

Lightmap
--------

Bạn có thể bake lightmap lên GridMap. Dữ liệu UV2 của lightmap sẽ được dùng lại từ các mesh nếu đã có sẵn. Nếu chưa có dữ liệu UV2, dữ liệu này sẽ được tự động tạo khi bake với kích thước texel lightmap là 0.1 đơn vị. Để tạo dữ liệu UV2 với kích thước texel lightmap khác, bạn có thể đặt chế độ global illumination trong dock Import thành **Static Lightmaps** và chỉ định kích thước texel ở đó. Tùy chọn này phải được thay đổi *trước* khi scene được chuyển đổi thành MeshLibrary, vì thay đổi sau đó sẽ không ảnh hưởng đến dữ liệu MeshLibrary hiện có.

Ngoài điểm đặc biệt này, quy trình bake lightmap cũng giống như với mọi scene 3D khác. Xem :ref:`doc_using_lightmap_gi` để biết thêm thông tin về việc bake lightmap.

Định dạng MeshLibrary
---------------------

Tóm lại các ràng buộc cụ thể của định dạng MeshLibrary: một scene MeshLibrary có Node3D làm node gốc và một số node con sẽ trở thành các mục MeshLibrary. Mỗi node con của node gốc cần:

- Là một :ref:`class_MeshInstance3D`, node này sẽ trở thành mục MeshLibrary. Chỉ mesh trực quan này được export.
- Có một vật liệu trong slot vật liệu của mesh, *không phải* trong các slot vật liệu của MeshInstance3D.
- Có tối đa một node con :ref:`class_StaticBody3D` để xử lý va chạm. StaticBody3D phải có một hoặc nhiều node con :ref:`class_CollisionShape3D`.
- Có tối đa một node con :ref:`class_NavigationRegion3D` để xử lý điều hướng. NavigationRegion3D có thể có thêm một hoặc nhiều node con :ref:`class_MeshInstance3D`, các node này có thể được bake để điều hướng nhưng sẽ không được export dưới dạng mesh trực quan.

Chỉ định dạng cụ thể này được nhận dạng. Các loại node khác được đặt làm node con sẽ không được nhận dạng và export. GridMap không phải là một hệ thống đa dụng để đặt *nodes* trên một lưới, mà là một hệ thống cụ thể, được tối ưu hóa để đặt *meshes* có va chạm và điều hướng.

Export MeshLibrary
------------------

Để export library, hãy nhấp vào **Scene > Export As... > MeshLibrary...**, rồi lưu nó dưới dạng resource.

.. image:: img/gridmap_export.webp

Bạn có thể tìm thấy một MeshLibrary đã được export trong dự án có tên ``MeshLibrary.tres``.

Sử dụng GridMap
---------------

Tạo một scene mới và thêm một node GridMap. Thêm mesh library bằng cách kéo file resource từ dock FileSystem rồi thả vào thuộc tính **Mesh Library** trong Inspector.

.. image:: img/gridmap_mesh_library_inspector.webp

Các thuộc tính trong Inspector
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Thiết lập **Physics Material** cho phép bạn ghi đè physics material cho mọi mesh trong NavigationMesh.

Trong mục **Cells**, thuộc tính **Size** nên được đặt bằng kích thước của các mesh. Bạn có thể giữ nguyên giá trị mặc định cho bản demo. Bỏ chọn thuộc tính **Center Y**.

Các tùy chọn **Collision** cho phép bạn thiết lập collision layer, collision mask và priority cho toàn bộ lưới. Để biết thêm thông tin về cách chúng hoạt động, hãy xem
:ref:`doc_physics_index` section.

Trong mục **Navigation** có tùy chọn "Bake Navigation". Nếu được bật, tùy chọn này sẽ tạo một navigation region cho mỗi ô sử dụng một mục mesh library có navigation mesh.

Nếu nhấp vào chính MeshLibrary trong Inspector, bạn có thể điều chỉnh các thiết lập cho từng mesh, chẳng hạn như navigation mesh, navigation layers hoặc việc mesh có đổ bóng hay không.

.. image:: img/gridmap_mesh_library_settings.webp

Bảng GridMap
~~~~~~~~~~~~

Ở cuối editor là bảng điều khiển GridMap, bảng này lẽ ra đã tự động mở khi bạn thêm node GridMap.

.. image:: img/gridmap_panel.webp

Từ trái sang phải trên toolbar:

- **Transform**: Thêm một gizmo vào scene, cho phép bạn thay đổi vị trí tương đối và góc xoay của gridmap trong scene.
- **Selection**: Khi đang hoạt động, bạn có thể chọn một khu vực trong viewport, nhấp và kéo để chọn nhiều hơn một ô trên lưới.
- **Erase**: Khi đang hoạt động, nhấp vào viewport để xóa các mesh.
- **Paint**: Khi đang hoạt động, nhấp vào viewport để thêm mesh hiện được chọn trong bảng điều khiển GridMap vào scene.
- **Pick**: Khi đang hoạt động, nhấp vào một mesh của gridmap trong viewport sẽ chọn mesh đó trong bảng điều khiển GridMap.
- **Fill**: Lấp đầy khu vực đã chọn trong viewport bằng mesh đang được chọn trong bảng điều khiển GridMap ở phía dưới.
- **Move**: Di chuyển mesh hoặc các mesh hiện đang được chọn trong viewport.
- **Duplicate**: Tạo một bản sao của mesh hoặc các mesh đang được chọn trong GridMap.
- **Delete**: Tương tự erase, nhưng áp dụng cho toàn bộ khu vực đã chọn.
- **Cursor Rotate X**: Khi công cụ paint được chọn, tùy chọn này sẽ xoay mesh được vẽ quanh trục X. Tùy chọn này cũng xoay các khu vực đã chọn nếu chúng đang được di chuyển.
- **Cursor Rotate Y**: Khi công cụ paint được chọn, tùy chọn này sẽ xoay mesh được vẽ quanh trục Y. Tùy chọn này cũng xoay các khu vực đã chọn nếu chúng đang được di chuyển.
- **Cursor Rotate Z**: Khi công cụ paint được chọn, tùy chọn này sẽ xoay mesh được vẽ quanh trục Z. Tùy chọn này cũng xoay các khu vực đã chọn nếu chúng đang được di chuyển.
- **Change Grid Floor**: Điều chỉnh tầng hiện đang được thao tác. Có thể thay đổi bằng các mũi tên, nhập giá trị vào trường hoặc :kbd:`Ctrl + Mouse wheel`.
- **Filter Meshes**: Dùng để tìm kiếm một mesh cụ thể trong bảng điều khiển phía dưới.
- **Zoom**: Điều khiển mức thu phóng của các mesh trong bảng điều khiển phía dưới.
- **Layout toggles**: Hai nút này chuyển đổi giữa các bố cục khác nhau cho các mesh trong bảng điều khiển phía dưới.
- **Tools dropdown**: Nút này mở một menu thả xuống với một vài tùy chọn bổ sung.

.. image:: img/gridmap_dropdown.webp

Nhấp vào **Settings** trong menu thả xuống đó sẽ mở một cửa sổ cho phép bạn thay đổi **Pick Distance**, là khoảng cách tối đa mà tại đó các tile có thể được đặt trên một GridMap, tính tương đối so với vị trí camera (tính bằng mét).

Sử dụng GridMap trong code
--------------------------

Xem :ref:`class_GridMap` để biết chi tiết về các method và biến thành viên của node.

.. _`gridmap_starter.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/gridmap_starter.zip
