.. _doc_using_gridmaps:

Sử dụng GridMaps
================

Giới thiệu
----------

:ref:`Gridmaps <class_GridMap>` are a tool for creating 3D
các level của game, tương tự như cách :ref:`TileMap <doc_using_tilemaps>` hoạt động trong 2D. Bạn bắt đầu với một tập hợp mesh 3D được định nghĩa trước (một
:ref:`class_MeshLibrary`) that can be placed on a grid,
như thể bạn đang xây dựng một level với số lượng khối Lego không giới hạn.

Bạn cũng có thể thêm collision và navigation vào các mesh, giống như cách bạn thực hiện với các tile của tilemap.

Project mẫu
-----------

Để tìm hiểu cách GridMaps hoạt động, trước tiên hãy tải project mẫu: `gridmap_starter.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/gridmap_starter.zip>`_.

Giải nén project này và thêm nó vào Project Manager bằng nút "Import". Bạn có thể nhận được một popup cho biết project cần được chuyển đổi sang phiên bản Godot mới hơn; hãy nhấp vào **Convert project.godot**.

Tạo MeshLibrary
---------------

Để bắt đầu, bạn cần một :ref:`class_MeshLibrary`, đây là một tập hợp các mesh riêng lẻ có thể được sử dụng trong gridmap. Mở scene "mesh_library_source.tscn" để xem ví dụ về cách thiết lập mesh library.

.. image:: img/gridmap_meshlibrary1.webp

Như bạn có thể thấy, scene này có một node :ref:`class_Node3D` làm node gốc và một số node con :ref:`class_MeshInstance3D`.

Nếu scene của bạn không cần physics thì bạn đã hoàn tất. Tuy nhiên, trong hầu hết trường hợp, bạn sẽ muốn gán các collision body cho các mesh.

Collisions
----------

Bạn có thể gán thủ công một :ref:`class_StaticBody3D` và
:ref:`class_CollisionShape3D` to each mesh. Alternatively, you can use the "Mesh" menu
để tự động tạo collision body dựa trên dữ liệu mesh.

.. image:: img/gridmap_create_body.webp

Lưu ý rằng collision body "Convex" sẽ hoạt động tốt hơn đối với các mesh đơn giản. Với các hình dạng phức tạp hơn, hãy chọn "Create Trimesh Static Body". Sau khi mỗi mesh đã được gán một physics body và collision shape, mesh library của bạn đã sẵn sàng để sử dụng.

.. image:: img/gridmap_mesh_scene.webp


Materials
---------

Chỉ các material bên trong mesh được sử dụng khi tạo mesh library. Các material được thiết lập trên node sẽ bị bỏ qua.

NavigationMeshes
----------------

Giống như mọi mesh instance, các item của MeshLibrary có thể được gán một resource :ref:`class_NavigationMesh`, có thể được tạo thủ công hoặc bake như mô tả bên dưới.

Để tạo NavigationMesh từ thao tác export scene MeshLibrary, hãy đặt một
:ref:`class_NavigationRegion3D` child node below the main MeshInstance3D for the GridMap
item. Thêm một resource NavigationMesh hợp lệ vào NavigationRegion3D cùng với một số node source geometry bên dưới, rồi bake NavigationMesh.

.. note::

    Với các cell grid nhỏ, thường cần giảm các thuộc tính NavigationMesh dành cho agent radius và region minimum size.

.. image:: img/meshlibrary_scene.png

Các node bên dưới NavigationRegion3D sẽ bị bỏ qua khi export scene MeshLibrary, vì vậy có thể thêm các node bổ sung làm source geometry chỉ để bake navmesh.

.. warning::

    Cell size đã bake của NavigationMesh phải khớp với cell size của map NavigationServer để các navigation mesh của những cell grid khác nhau được hợp nhất chính xác.

Lightmaps
---------

Bạn có thể bake lightmap lên GridMap. Dữ liệu Lightmap UV2 sẽ được tái sử dụng từ các mesh nếu đã tồn tại. Nếu không có dữ liệu UV2, dữ liệu này sẽ được tự động tạo khi bake với lightmap texel size là 0.1 units. Để tạo dữ liệu UV2 với lightmap texel size khác, bạn có thể đặt global illumination mode trong Import dock thành **Static Lightmaps** và chỉ định texel size tại đó. Phải thay đổi tùy chọn này *trước* khi scene được chuyển đổi thành MeshLibrary, vì thay đổi sau đó sẽ không ảnh hưởng đến dữ liệu MeshLibrary hiện có.

Ngoài điểm đặc biệt này, quy trình bake lightmap cũng giống như đối với mọi scene 3D khác. Xem :ref:`doc_using_lightmap_gi` để biết thêm thông tin về việc bake lightmap.

Định dạng MeshLibrary
---------------------

Tóm lại các ràng buộc cụ thể của định dạng MeshLibrary: một scene MeshLibrary có Node3D làm node gốc và một số node con sẽ trở thành các item MeshLibrary. Mỗi node con của node gốc nên:

- Là một :ref:`class_MeshInstance3D`, sẽ trở thành item MeshLibrary. Chỉ mesh hiển thị này được export. - Có một material trong material slot của mesh, *không phải* trong các material slot của MeshInstance3D. - Có tối đa một node con :ref:`class_StaticBody3D`, dùng cho collision. StaticBody3D phải có một hoặc nhiều node con :ref:`class_CollisionShape3D`. - Có tối đa một node con :ref:`class_NavigationRegion3D`, dùng cho navigation. NavigationRegion3D có thể có một hoặc nhiều node con :ref:`class_MeshInstance3D` bổ sung, có thể được bake cho navigation nhưng sẽ không được export dưới dạng mesh hiển thị.

Chỉ định dạng cụ thể này được nhận diện. Các loại node khác được đặt làm node con sẽ không được nhận diện và export. GridMap không phải là một hệ thống đa dụng để đặt *node* trên grid, mà là một hệ thống chuyên biệt, được tối ưu hóa để đặt *mesh* cùng collision và navigation.

Export MeshLibrary
------------------

Để export library, hãy nhấp vào **Scene > Export As... > MeshLibrary...** và lưu nó dưới dạng resource.

.. image:: img/gridmap_export.webp

Bạn có thể tìm thấy một MeshLibrary đã được export trong project có tên ``MeshLibrary.tres``.

Sử dụng GridMap
---------------

Tạo một scene mới và thêm node GridMap. Thêm mesh library bằng cách kéo file resource từ FileSystem dock rồi thả vào thuộc tính **Mesh Library** trong Inspector.

.. image:: img/gridmap_mesh_library_inspector.webp

Các thuộc tính Inspector
~~~~~~~~~~~~~~~~~~~~~~~~

Thiết lập **Physics Material** cho phép bạn ghi đè physics material cho mọi mesh trong NavigationMesh.

Trong **Cells**, thuộc tính **Size** nên được đặt bằng kích thước của các mesh. Bạn có thể giữ giá trị mặc định cho bản demo. Bỏ chọn thuộc tính **Center Y**.

Các tùy chọn **Collision** cho phép bạn đặt collision layer, collision mask và priority cho toàn bộ grid. Để biết thêm thông tin về cách chúng hoạt động, hãy xem
:ref:`doc_physics_index` section.

Trong **Navigation** có tùy chọn "Bake Navigation". Nếu được bật, tùy chọn này sẽ tạo một navigation region cho mỗi cell sử dụng item mesh library có navigation mesh.

Nếu nhấp vào chính MeshLibrary trong inspector, bạn có thể điều chỉnh các thiết lập cho từng mesh, chẳng hạn như navigation mesh, navigation layers hoặc việc mesh có đổ bóng hay không.

.. image:: img/gridmap_mesh_library_settings.webp

Panel GridMap
~~~~~~~~~~~~~

Ở cuối editor là panel GridMap, panel này sẽ tự động mở khi bạn thêm node GridMap.

.. image:: img/gridmap_panel.webp

Từ trái sang phải trên toolbar:

- **Transform**: Thêm một gizmo vào scene, cho phép bạn thay đổi vị trí tương đối và rotation của gridmap trong scene. - **Selection**: Khi đang bật, bạn có thể chọn một vùng trong viewport; nhấp và kéo để chọn nhiều hơn một ô trên grid. - **Erase**: Khi đang bật, nhấp vào viewport để xóa mesh. - **Paint**: Khi đang bật, nhấp vào viewport để thêm mesh hiện đang được chọn trong panel GridMap vào scene. - **Pick**: Khi đang bật, nhấp vào một mesh gridmap trong viewport sẽ chọn mesh đó trong panel GridMap. - **Fill**: Tô đầy vùng đã chọn trong viewport bằng mesh đang được chọn trong panel GridMap bên dưới. - **Move**: Di chuyển mesh hoặc các mesh hiện đang được chọn trong viewport. - **Duplicate**: Tạo một bản sao của mesh hoặc các mesh đang được chọn trong GridMap. - **Delete**: Tương tự erase nhưng áp dụng cho toàn bộ vùng đã chọn. - **Cursor Rotate X**: Khi công cụ paint được chọn, thao tác này sẽ xoay mesh sẽ được vẽ theo trục X. Thao tác này cũng xoay các vùng đã chọn nếu chúng đang được di chuyển. - **Cursor Rotate Y**: Khi công cụ paint được chọn, thao tác này sẽ xoay mesh sẽ được vẽ theo trục Y. Thao tác này cũng xoay các vùng đã chọn nếu chúng đang được di chuyển. - **Cursor Rotate Z**: Khi công cụ paint được chọn, thao tác này sẽ xoay mesh sẽ được vẽ theo trục Z. Thao tác này cũng xoay các vùng đã chọn nếu chúng đang được di chuyển. - **Change Grid Floor**: Điều chỉnh floor hiện đang được thao tác. Có thể thay đổi bằng các mũi tên, nhập giá trị vào trường hoặc :kbd:`Ctrl + Mouse wheel`. - **Filter Meshes**: Dùng để tìm kiếm một mesh cụ thể trong panel bên dưới. - **Zoom**: Điều khiển mức zoom của các mesh trong panel bên dưới. - **Layout toggles**: Hai nút này chuyển đổi giữa các layout khác nhau cho các mesh trong panel bên dưới. - **Tools dropdown**: Nút này mở một menu dropdown với thêm một số tùy chọn.

.. image:: img/gridmap_dropdown.webp

Nhấp vào **Settings** trong dropdown đó sẽ mở ra một cửa sổ cho phép bạn thay đổi **Pick Distance**, tức khoảng cách tối đa mà tại đó các tile có thể được đặt trên GridMap, tính tương đối so với vị trí camera (theo mét).

Sử dụng GridMap trong code
--------------------------

Xem :ref:`class_GridMap` để biết chi tiết về các method và member variable của node.
