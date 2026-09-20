.. _doc_thread_safe_apis:

API an toàn luồng (thread-safe)
===============================

Luồng (thread)
--------------

Luồng được sử dụng để cân bằng năng lực xử lý giữa các CPU và lõi. Godot hỗ trợ đa luồng, nhưng không phải trong toàn bộ engine.

Dưới đây là danh sách các cách có thể sử dụng đa luồng trong những khu vực khác nhau của Godot.

Phạm vi global
--------------

Hầu hết các singleton :ref:`Global Scope<class_@GlobalScope>` đều thread-safe theo mặc định. Việc truy cập các servers từ các luồng được hỗ trợ. Tuy nhiên, để
:ref:`rendering <doc_thread_safe_apis_rendering>` and
:ref:`physics <doc_thread_safe_apis_physics>` servers,
thao tác thread-safe, trước tiên phải bật tùy chọn này trong project settings.

Điều này khiến các singleton trở nên lý tưởng cho những đoạn code tạo hàng chục nghìn instance trong các servers và điều khiển chúng từ các luồng. Tất nhiên, cách này cần thêm một chút code, vì nó được sử dụng trực tiếp chứ không nằm trong scene tree.

Scene tree
----------

Tương tác với scene tree đang hoạt động **không** thread-safe. Hãy đảm bảo sử dụng mutex khi gửi dữ liệu giữa các luồng. Nếu muốn gọi các function hoặc thiết lập các property từ một luồng, bạn có thể sử dụng
:ref:`call_deferred <class_Object_method_call_deferred>` or :ref:`set_deferred <class_Object_method_set_deferred>`:

.. tabs::
 .. code-tab:: gdscript

    # Không an toàn:
    node.add_child(child_node)
    # An toàn:
    node.add_child.call_deferred(child_node)

 .. code-tab:: csharp

    // Không an toàn:
    node.AddChild(childNode);
    // An toàn:
    node.CallDeferred(Node.MethodName.AddChild, childNode);

Tuy nhiên, việc tạo các scene chunk (các node được sắp xếp theo cấu trúc cây) bên ngoài tree đang hoạt động là hoàn toàn ổn. Bằng cách này, các phần của một scene có thể được xây dựng hoặc tạo instance trong một luồng, sau đó được thêm vào trong luồng chính:

.. tabs::
 .. code-tab:: gdscript

    var enemy_scene = load("res://enemy_scene.scn")
    var enemy = enemy_scene.instantiate()
    enemy.add_child(weapon) # Thiết lập một vũ khí.
    world.add_child.call_deferred(enemy)

 .. code-tab:: csharp

    PackedScene enemyScene = GD.Load<PackedScene>("res://EnemyScene.scn");
    Node enemy = enemyScene.Instantiate<Node>();
    enemy.AddChild(weapon);
    world.CallDeferred(Node.MethodName.AddChild, enemy);

Tuy vậy, cách này chỉ thực sự hữu ích nếu bạn có **một** luồng tải dữ liệu. Việc cố gắng tải hoặc tạo các scene chunk từ nhiều luồng có thể hoạt động, nhưng bạn có nguy cơ khiến các resource (chỉ được tải một lần trong Godot) bị nhiều luồng chỉnh sửa, dẫn đến hành vi không mong muốn hoặc crash.

Chỉ sử dụng nhiều hơn một luồng để tạo dữ liệu scene nếu bạn *thực sự* hiểu rõ mình đang làm gì và chắc chắn rằng một resource duy nhất không được sử dụng hoặc thiết lập trong nhiều luồng. Nếu không, cách an toàn hơn là sử dụng trực tiếp servers API (hoàn toàn thread-safe) và không chạm vào scene hoặc resource.

.. _doc_thread_safe_apis_rendering:

Rendering
---------

Việc tạo instance các node render bất kỳ thứ gì trong 2D hoặc 3D (chẳng hạn như :ref:`class_Sprite2D` hoặc :ref:`class_MeshInstance3D`) theo mặc định là *không* thread-safe. Để chạy rendering driver trên một luồng riêng, hãy đặt
:ref:`Rendering > Driver > Thread Model <class_ProjectSettings_property_rendering/driver/threads/thread_model>`
project setting thành **Separate**.

Lưu ý rằng mô hình luồng **Separate** có một số bug đã biết, vì vậy có thể không sử dụng được trong mọi trường hợp.

.. warning::

    Bạn nên tránh gọi các function liên quan đến tương tác trực tiếp với GPU trên các luồng khác, chẳng hạn như tạo texture mới hoặc chỉnh sửa và lấy dữ liệu hình ảnh. Những thao tác này có thể gây ra các lần đình trệ hiệu năng vì chúng yêu cầu đồng bộ hóa với :ref:`RenderingServer<class_RenderingServer>`, do dữ liệu cần được truyền đến hoặc cập nhật trên GPU.

.. _doc_thread_safe_apis_physics:

Vật lý
------

Mô phỏng vật lý theo mặc định là *không* thread-safe. Để chạy các physics servers trên các luồng riêng (khiến chúng thread-safe), hãy bật các project settings sau:

- **PhysicsServer2D:** :ref:`Physics > 2D > Run on Separate Thread <class_ProjectSettings_property_physics/2d/run_on_separate_thread>`. - **PhysicsServer3D:** :ref:`Physics > 3D > Run on Separate Thread <class_ProjectSettings_property_physics/3d/run_on_separate_thread>`.

Navigation
----------

:ref:`NavigationServer2D<class_NavigationServer2D>` and :ref:`NavigationServer3D<class_NavigationServer3D>` are both thread-safe and thread-friendly.

Các function truy vấn liên quan đến navigation có thể được gọi bởi các luồng và chạy song song thực sự.

Theo mặc định, một số lượng luồng thận trọng được hỗ trợ chạy song song thực sự trên các navigation map trước khi những luồng bổ sung phải chờ quyền truy cập dữ liệu map tại một semaphore. Để tăng số lượng luồng có thể chạy đồng thời trên dữ liệu map, hãy đặt :ref:`Navigation > Pathfinding > Max Threads <class_ProjectSettings_property_navigation/pathfinding/max_threads>`.

Các resource liên quan đến navigation server như NavigationSourceGeometryData, NavigationMesh và NavigationPolygon đều thread-safe nhưng không nhất thiết thân thiện với luồng (thread-friendly). Chúng sử dụng các read-write lock nội bộ để đảm bảo thread-safety, vì vậy việc chỉnh sửa cùng một resource (ví dụ: một navmesh lớn duy nhất) trên nhiều luồng cùng lúc có thể gây tắc nghẽn luồng.

Các helper class liên quan đến navigation như :ref:`AStar2D<class_AStar2D>`, :ref:`AStar3D<class_AStar3D>` và :ref:`AStarGrid2D<class_AStarGrid2D>` **không** thread-safe. Chúng có thể được sử dụng với các luồng ở mức độ hạn chế, nhưng việc sử dụng từ hai luồng trở lên trên cùng một đối tượng AStar sẽ gây hỏng dữ liệu. Ví dụ, sử dụng một luồng background riêng cho mỗi đối tượng AStar để thêm các điểm hoặc thực hiện truy vấn sẽ hoạt động, nhưng hai luồng sử dụng cùng một đối tượng AStar sẽ làm hỏng dữ liệu của nhau.

Mảng và dictionary trong GDScript
---------------------------------

Trong GDScript, việc đọc và ghi các phần tử từ nhiều luồng là ổn, nhưng mọi thao tác làm thay đổi kích thước container (resize, thêm hoặc xóa phần tử) đều yêu cầu khóa một :ref:`mutex <doc_using_multiple_threads_mutexes>`.

Resource
--------

Việc chỉnh sửa một resource duy nhất từ nhiều luồng không được hỗ trợ. Tuy nhiên, việc xử lý các reference trên nhiều luồng *được* hỗ trợ. Do đó, việc tải resource trên một luồng cũng được hỗ trợ. Các scene, texture, mesh, v.v. có thể được tải và thao tác trên một luồng, sau đó được thêm vào scene đang hoạt động trên luồng chính. Hạn chế ở đây là như đã mô tả ở trên: cần cẩn thận để không tải cùng một resource từ nhiều luồng cùng lúc. Vì vậy, cách dễ nhất là sử dụng **một** luồng để tải và chỉnh sửa resource, sau đó sử dụng luồng chính để thêm chúng.
