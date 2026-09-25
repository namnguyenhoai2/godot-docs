.. _doc_thread_safe_apis:

API an toàn khi sử dụng với luồng
=================================

Luồng
-----

Luồng được sử dụng để phân bổ sức mạnh xử lý trên các CPU và lõi. Godot hỗ trợ đa luồng, nhưng không phải trong toàn bộ engine.

Dưới đây là danh sách các cách sử dụng đa luồng trong những khu vực khác nhau của Godot.

Phạm vi toàn cục
----------------

Hầu hết singleton :ref:`Global Scope <class_@GlobalScope>` đều an toàn với luồng theo mặc định. Việc truy cập các server từ luồng được hỗ trợ. Tuy nhiên, đối với
server :ref:`rendering <doc_thread_safe_apis_rendering>` và
server :ref:`physics <doc_thread_safe_apis_physics>`, trước tiên phải bật thao tác an toàn với luồng trong phần cài đặt dự án.

Điều này khiến các singleton trở nên lý tưởng cho mã tạo hàng chục nghìn instance trong các server và điều khiển chúng từ các luồng. Tất nhiên, cách này yêu cầu viết thêm một chút mã, vì nó được sử dụng trực tiếp chứ không nằm trong scene tree.

Scene tree
----------

Tương tác với scene tree đang hoạt động **not** an toàn với luồng. Hãy đảm bảo sử dụng mutex khi gửi dữ liệu giữa các luồng. Nếu muốn gọi các hàm hoặc đặt thuộc tính từ một luồng, bạn có thể sử dụng
:ref:`call_deferred <class_Object_method_call_deferred>` hoặc :ref:`set_deferred <class_Object_method_set_deferred>`:

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

Tuy nhiên, việc tạo các phần scene (các node được sắp xếp theo cấu trúc cây) bên ngoài tree đang hoạt động là an toàn. Bằng cách này, các phần của scene có thể được xây dựng hoặc tạo instance trong một luồng, sau đó được thêm vào trong luồng chính:

.. tabs::
 .. code-tab:: gdscript

    var enemy_scene = load("res://enemy_scene.scn")
    var enemy = enemy_scene.instantiate()
    enemy.add_child(weapon) # Đặt một vũ khí.
    world.add_child.call_deferred(enemy)

 .. code-tab:: csharp

    PackedScene enemyScene = GD.Load<PackedScene>("res://EnemyScene.scn");
    Node enemy = enemyScene.Instantiate<Node>();
    enemy.AddChild(weapon);
    world.CallDeferred(Node.MethodName.AddChild, enemy);

Tuy vậy, cách này chỉ thực sự hữu ích nếu bạn có **one** luồng tải dữ liệu. Việc cố gắng tải hoặc tạo các phần scene từ nhiều luồng có thể hoạt động, nhưng bạn có nguy cơ khiến các resource (chỉ được tải một lần trong Godot) bị nhiều luồng chỉnh sửa, dẫn đến hành vi không mong muốn hoặc crash.

Chỉ sử dụng nhiều hơn một luồng để tạo dữ liệu scene nếu bạn *really* biết rõ mình đang làm gì và chắc chắn rằng một resource duy nhất không được sử dụng hoặc thiết lập trong nhiều luồng. Nếu không, cách an toàn hơn là sử dụng trực tiếp API của các server (hoàn toàn an toàn với luồng) và không tác động đến scene hoặc resource.

.. _doc_thread_safe_apis_rendering:

Rendering
---------

Việc tạo instance các node render bất kỳ nội dung nào trong 2D hoặc 3D (chẳng hạn như :ref:`class_Sprite2D` hoặc :ref:`class_MeshInstance3D`) *not* an toàn với luồng theo mặc định. Để chạy rendering driver trên một luồng riêng, hãy đặt
cài đặt dự án :ref:`Rendering > Driver > Thread Model <class_ProjectSettings_property_rendering/driver/threads/thread_model>` thành **Separate**.

Lưu ý rằng thread model **Separate** có một số lỗi đã được biết, nên có thể không sử dụng được trong mọi trường hợp.

.. warning::

    Bạn nên tránh gọi các hàm liên quan đến việc tương tác trực tiếp với GPU trên các luồng khác, chẳng hạn như tạo texture mới hoặc sửa đổi và lấy dữ liệu hình ảnh. Các thao tác này có thể gây ra hiện tượng đình trệ hiệu năng vì chúng yêu cầu đồng bộ hóa với :ref:`RenderingServer<class_RenderingServer>`, do dữ liệu cần được truyền đến hoặc cập nhật trên GPU.

.. _doc_thread_safe_apis_physics:

Physics
-------

Mô phỏng physics *not* an toàn với luồng theo mặc định. Để chạy các physics server trên các luồng riêng (khiến chúng an toàn với luồng), hãy bật các cài đặt dự án sau:

- **PhysicsServer2D:** :ref:`Physics > 2D > Run on Separate Thread <class_ProjectSettings_property_physics/2d/run_on_separate_thread>`.
- **PhysicsServer3D:** :ref:`Physics > 3D > Run on Separate Thread <class_ProjectSettings_property_physics/3d/run_on_separate_thread>`.

Navigation
----------

:ref:`NavigationServer2D<class_NavigationServer2D>` và :ref:`NavigationServer3D<class_NavigationServer3D>` đều an toàn với luồng và phù hợp với đa luồng.

Các hàm truy vấn liên quan đến navigation có thể được gọi bởi các luồng và chạy song song thực sự.

Theo mặc định, một số lượng luồng thận trọng được hỗ trợ chạy song song thực sự trên các navigation map trước khi các luồng bổ sung phải chờ quyền truy cập dữ liệu map tại một semaphore. Để tăng số lượng luồng có thể chạy đồng thời trên dữ liệu map, hãy đặt :ref:`Navigation > Pathfinding > Max Threads <class_ProjectSettings_property_navigation/pathfinding/max_threads>`.

Các resource liên quan đến navigation server như NavigationSourceGeometryData, NavigationMesh và NavigationPolygon đều an toàn với luồng nhưng không nhất thiết phù hợp với đa luồng. Chúng sử dụng các khóa đọc-ghi nội bộ để đảm bảo an toàn với luồng, vì vậy việc chỉnh sửa cùng một resource (ví dụ: một navmesh lớn duy nhất) trên nhiều luồng cùng lúc có thể gây tắc nghẽn luồng.

Các lớp helper liên quan đến navigation như :ref:`AStar2D<class_AStar2D>`, :ref:`AStar3D<class_AStar3D>` và :ref:`AStarGrid2D<class_AStarGrid2D>` **not** an toàn với luồng. Chúng có thể được sử dụng với các luồng trong một giới hạn nhất định, nhưng việc sử dụng từ hai luồng trở lên trên cùng một đối tượng AStar sẽ gây hỏng dữ liệu. Ví dụ, sử dụng một luồng nền riêng cho mỗi đối tượng AStar để thêm các điểm hoặc thực hiện truy vấn là được, nhưng hai luồng sử dụng cùng một đối tượng AStar sẽ làm hỏng dữ liệu của nhau.

Mảng và dictionary trong GDScript
---------------------------------

Trong GDScript, việc đọc và ghi các phần tử từ nhiều luồng là được, nhưng mọi thao tác làm thay đổi kích thước container (đổi kích thước, thêm hoặc xóa phần tử) đều yêu cầu khóa một :ref:`mutex <doc_using_multiple_threads_mutexes>`.

Resource
--------

Không hỗ trợ sửa đổi một resource duy nhất từ nhiều luồng. Tuy nhiên, việc xử lý các tham chiếu trên nhiều luồng *is* được hỗ trợ. Do đó, việc tải resource trên một luồng cũng được hỗ trợ. Scene, texture, mesh, v.v. có thể được tải và thao tác trên một luồng, sau đó được thêm vào scene đang hoạt động trên luồng chính. Hạn chế ở đây như đã mô tả bên trên: cần cẩn thận không tải cùng một resource từ nhiều luồng cùng lúc. Vì vậy, cách dễ nhất là sử dụng **one** luồng để tải và sửa đổi resource, sau đó sử dụng luồng chính để thêm chúng.
