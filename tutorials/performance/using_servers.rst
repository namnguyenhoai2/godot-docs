.. _doc_using_servers:

Tối ưu hóa bằng Servers
=======================

Các engine như Godot mang lại sự dễ sử dụng cao hơn nhờ những cấu trúc và tính năng cấp cao. Hầu hết chúng được truy cập và sử dụng thông qua
:ref:`scene system <doc_scene_tree>`. Việc sử dụng node và resource giúp đơn giản hóa việc tổ chức dự án và quản lý asset trong các game phức tạp.

Điều này có một số hạn chế:

- Có thêm một lớp phức tạp.
- Hiệu năng thấp hơn so với khi sử dụng trực tiếp các API đơn giản.
- Không thể :ref:`sử dụng nhiều thread <doc_using_multiple_threads>` để điều khiển chúng.
- Cần nhiều bộ nhớ hơn.

Trong hầu hết trường hợp, đây không thực sự là vấn đề. Godot được tối ưu hóa tốt và hầu hết các thao tác đều được xử lý bằng signal, nghĩa là không cần polling. Tuy vậy, đôi khi chúng ta muốn khai thác hiệu năng tốt hơn từ phần cứng sau khi đã thử hết các hướng tối ưu hóa khác. Ví dụ, việc xử lý hàng chục nghìn instance cho một tác vụ cần được thực hiện ở mỗi frame có thể trở thành nút thắt cổ chai.

Tình huống này khiến lập trình viên hối tiếc vì đã sử dụng game engine và ước rằng họ có thể quay lại cách triển khai mã game cấp thấp, được xây dựng thủ công hơn.

Tuy vậy, Godot được thiết kế để giải quyết vấn đề này.

.. seealso::

    Bạn có thể xem cách các server cấp thấp hoạt động trong thực tế qua `dự án demo Bullet Shower <https://github.com/godotengine/godot-demo-projects/tree/master/2d/bullet_shower>`__.

Servers
-------

Một trong những quyết định thiết kế thú vị nhất của Godot là toàn bộ scene system *không bắt buộc*. Mặc dù không thể loại bỏ nó khi biên dịch, bạn hoàn toàn có thể bỏ qua nó.

Về cốt lõi, Godot sử dụng khái niệm Servers. Đây là các API cấp thấp để điều khiển rendering, physics, sound, v.v. Scene system được xây dựng trên nền tảng này và sử dụng chúng trực tiếp. Các server phổ biến nhất gồm:

* :ref:`class_RenderingServer`: Xử lý mọi thứ liên quan đến đồ họa.
* :ref:`class_PhysicsServer3D`: Xử lý mọi thứ liên quan đến physics 3D.
* :ref:`class_PhysicsServer2D`: Xử lý mọi thứ liên quan đến physics 2D.
* :ref:`class_AudioServer`: Xử lý mọi thứ liên quan đến âm thanh.

Hãy khám phá các API của chúng, và bạn sẽ nhận ra rằng tất cả các hàm được cung cấp đều là những triển khai cấp thấp của mọi thứ Godot cho phép bạn thực hiện bằng node.

RIDs
----

Chìa khóa để sử dụng server là hiểu các đối tượng Resource ID (:ref:`RID <class_RID>`). Đây là các handle không trong suốt đến phần triển khai của server. Chúng được cấp phát và giải phóng thủ công. Hầu như mọi hàm trong server đều yêu cầu RID để truy cập resource thực tế.

Hầu hết node và resource của Godot đều chứa các RID từ server ở bên trong, và bạn có thể lấy chúng bằng nhiều hàm khác nhau. Trên thực tế, mọi thứ kế thừa :ref:`Resource <class_Resource>` đều có thể được ép kiểu trực tiếp thành RID. Tuy nhiên, không phải mọi resource đều chứa RID: trong những trường hợp đó, RID sẽ rỗng. Khi đó, resource có thể được truyền đến các API của server dưới dạng RID.

.. warning::

    Resource được đếm tham chiếu (xem :ref:`RefCounted <class_RefCounted>`), còn các tham chiếu đến RID của resource thì *không* được tính khi xác định resource có còn đang được sử dụng hay không. Hãy đảm bảo **giữ một tham chiếu** đến resource bên ngoài server. Nếu không, cả resource và RID của nó sẽ bị xóa.

Đối với node, có nhiều hàm khả dụng:

- Đối với CanvasItem, phương thức :ref:`CanvasItem.get_canvas_item() <class_CanvasItem_method_get_canvas_item>` sẽ trả về RID của canvas item trong server.
- Đối với CanvasLayer, phương thức :ref:`CanvasLayer.get_canvas() <class_CanvasLayer_method_get_canvas>` sẽ trả về RID của canvas trong server.
- Đối với Viewport, phương thức :ref:`Viewport.get_viewport_rid() <class_Viewport_method_get_viewport_rid>` sẽ trả về RID của viewport trong server.
- Đối với 2D, resource :ref:`class_World2D` (có thể lấy được trong các node :ref:`class_Viewport` và :ref:`CanvasItem <class_CanvasItem>`) chứa các hàm để lấy *RenderingServer Canvas* và *PhysicsServer2D Space*. Điều này cho phép tạo trực tiếp các đối tượng 2D bằng API của server và sử dụng chúng.
- Đối với 3D, resource :ref:`class_World3D` (có thể lấy được trong các node :ref:`class_Viewport` và :ref:`class_Node3D`) chứa các hàm để lấy *RenderingServer Scenario* và *PhysicsServer Space*. Điều này cho phép tạo trực tiếp các đối tượng 3D bằng API của server và sử dụng chúng.
- Lớp :ref:`class_VisualInstance3D` cho phép lấy *instance* và *instance base* của scenario lần lượt thông qua :ref:`VisualInstance3D.get_instance() <class_VisualInstance3D_method_get_instance>` và :ref:`VisualInstance3D.get_base() <class_VisualInstance3D_method_get_base>`.

Hãy thử khám phá các node và resource mà bạn quen thuộc, rồi tìm các hàm để lấy *RID* của server.

Không nên điều khiển RID từ các đối tượng đã có node liên kết. Thay vào đó, luôn sử dụng các hàm của server để tạo và điều khiển những đối tượng mới cũng như tương tác với các đối tượng hiện có.

Tạo một sprite
--------------

Đây là ví dụ về cách tạo một sprite từ code và di chuyển nó bằng
API :ref:`class_CanvasItem` cấp thấp.

.. note::

    Khi tạo canvas item bằng RenderingServer, bạn nên đặt lại nội suy physics ở frame đầu tiên bằng
    :ref:`RenderingServer.canvas_item_reset_physics_interpolation() <class_RenderingServer_method_canvas_item_reset_physics_interpolation>`. Điều này đảm bảo sự đồng bộ chính xác giữa hệ thống rendering và physics.

    Nếu không thực hiện việc này, canvas item có thể trông như dịch chuyển tức thời vào vị trí khi scene được tải, thay vì xuất hiện trực tiếp tại vị trí dự kiến.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D


    # RenderingServer yêu cầu các tham chiếu được duy trì.
    var texture


    func _ready():
        # Tạo một canvas item, là node con của node này.
        var ci_rid = RenderingServer.canvas_item_create()
        # Đặt node này làm node cha.
        RenderingServer.canvas_item_set_parent(ci_rid, get_canvas_item())
        # Vẽ một texture lên đó.
        # Nhớ duy trì tham chiếu này.
        texture = load("res://my_texture.png")
        # Thêm nó vào, căn giữa.
        RenderingServer.canvas_item_add_texture_rect(ci_rid, Rect2(-texture.get_size() / 2, texture.get_size()), texture)
        # Thêm item, xoay 45 độ và dịch chuyển.
        var xform = Transform2D().rotated(deg_to_rad(45)).translated(Vector2(20, 30))
        RenderingServer.canvas_item_set_transform(ci_rid, xform)
        # Đặt lại nội suy physics cho item này.
        RenderingServer.canvas_item_reset_physics_interpolation(ci_rid)

 .. code-tab:: csharp

    public partial class MyNode2D : Node2D
    {
        // RenderingServer yêu cầu các tham chiếu được duy trì.
        private Texture2D _texture;

        public override void _Ready()
        {
            // Tạo một canvas item, là node con của node này.
            Rid ciRid = RenderingServer.CanvasItemCreate();
            // Đặt node này làm node cha.
            RenderingServer.CanvasItemSetParent(ciRid, GetCanvasItem());
            // Vẽ một texture lên đó.
            // Nhớ giữ lại tham chiếu này.
            _texture = ResourceLoader.Load<Texture2D>("res://my_texture.png");
            // Thêm nó vào chính giữa.
            RenderingServer.CanvasItemAddTextureRect(ciRid, new Rect2(-_texture.GetSize() / 2, _texture.GetSize()), _texture.GetRid());
            // Thêm đối tượng, xoay 45 độ và dịch chuyển.
            Transform2D xform = Transform2D.Identity.Rotated(Mathf.DegToRad(45)).Translated(new Vector2(20, 30));
            RenderingServer.CanvasItemSetTransform(ciRid, xform);
            // Đặt lại nội suy vật lý cho đối tượng này.
            RenderingServer.CanvasItemResetPhysicsInterpolation(ciRid);
        }
    }

Canvas Item API trên server cho phép bạn thêm các primitive vẽ vào đó. Sau khi được thêm, chúng không thể sửa đổi. Cần xóa Item rồi thêm lại các primitive. Điều này không áp dụng cho việc đặt transform, thao tác có thể thực hiện bao nhiêu lần tùy ý.

Có thể xóa các primitive như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    RenderingServer.canvas_item_clear(ci_rid)

 .. code-tab:: csharp

    RenderingServer.CanvasItemClear(ciRid);


Khởi tạo Mesh trong không gian 3D
---------------------------------

Các API 3D khác với các API 2D, vì vậy phải sử dụng API khởi tạo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node3D


    # RenderingServer yêu cầu phải giữ lại các tham chiếu.
    var mesh


    func _ready():
        # Tạo một visual instance (cho 3D).
        var instance = RenderingServer.instance_create()
        # Đặt scenario từ world. Điều này đảm bảo nó
        # xuất hiện cùng các đối tượng như scene.
        var scenario = get_world_3d().scenario
        RenderingServer.instance_set_scenario(instance, scenario)
        # Thêm một mesh vào đó.
        # Nhớ giữ lại tham chiếu này.
        mesh = load("res://my_mesh.obj")
        RenderingServer.instance_set_base(instance, mesh)
        # Di chuyển mesh.
        var xform = Transform3D(Basis(), Vector3(2, 3, 0))
        RenderingServer.instance_set_transform(instance, xform)

 .. code-tab:: csharp

    public partial class MyNode3D : Node3D
    {
        // RenderingServer yêu cầu phải giữ lại các tham chiếu.
        private Mesh _mesh;

        public override void _Ready()
        {
            // Tạo một visual instance (cho 3D).
            Rid instance = RenderingServer.InstanceCreate();
            // Đặt scenario từ world. Điều này đảm bảo nó
            // xuất hiện cùng các đối tượng như scene.
            Rid scenario = GetWorld3D().Scenario;
            RenderingServer.InstanceSetScenario(instance, scenario);
            // Thêm một mesh vào đó.
            // Nhớ giữ lại tham chiếu này.
            _mesh = ResourceLoader.Load<Mesh>("res://my_mesh.obj");
            RenderingServer.InstanceSetBase(instance, _mesh.GetRid());
            // Di chuyển mesh.
            Transform3D xform = new Transform3D(Basis.Identity, new Vector3(2, 3, 0));
            RenderingServer.InstanceSetTransform(instance, xform);
        }
    }

Tạo một RigidBody 2D và di chuyển sprite bằng nó
------------------------------------------------

Thao tác này tạo một :ref:`class_RigidBody2D` bằng API :ref:`class_PhysicsServer2D`, và di chuyển một :ref:`class_CanvasItem` khi body di chuyển.

.. tabs::
 .. code-tab:: gdscript GDScript

    # PhysicsServer2D yêu cầu phải giữ lại các tham chiếu.
    var body
    var shape


    func _body_moved(state, index):
        # Đã tạo canvas item riêng; sử dụng nó ở đây.
        # `ci_rid` từ ví dụ về sprite ở trên cần được chuyển vào một
        # biến thành viên (thay vì nằm trong `_ready()`) để có thể tham chiếu tại đây.
        RenderingServer.canvas_item_set_transform(ci_rid, state.transform)


    func _ready():
        # Tạo body.
        body = PhysicsServer2D.body_create()
        PhysicsServer2D.body_set_mode(body, PhysicsServer2D.BODY_MODE_RIGID)
        # Thêm một shape.
        shape = PhysicsServer2D.rectangle_shape_create()
        # Đặt kích thước phần mở rộng của hình chữ nhật.
        PhysicsServer2D.shape_set_data(shape, Vector2(10, 10))
        # Hãy nhớ giữ lại tham chiếu đến shape!
        PhysicsServer2D.body_add_shape(body, shape)
        # Đặt space để nó va chạm trong cùng space với scene hiện tại.
        PhysicsServer2D.body_set_space(body, get_world_2d().space)
        # Di chuyển vị trí ban đầu.
        PhysicsServer2D.body_set_state(body, PhysicsServer2D.BODY_STATE_TRANSFORM, Transform2D(0, Vector2(10, 20)))
        # Thêm callback transform khi body di chuyển
        # Tham số cuối cùng là tùy chọn, có thể dùng làm chỉ mục
        # nếu bạn có nhiều body và một callback duy nhất.
        PhysicsServer2D.body_set_force_integration_callback(body, self, "_body_moved", 0)

        # Cũng tạo một sprite bằng RenderingServer tại đây.
        # Xem phần ở trên về cách tạo sprite.
        # ...

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private Rid _canvasItem;

        private void BodyMoved(PhysicsDirectBodyState2D state, int index)
        {
            // Đã tạo canvas item riêng; sử dụng nó ở đây.
            // `ciRid` từ ví dụ về sprite ở trên cần được chuyển vào một
            // biến thành viên (thay vì nằm trong `_Ready()`) để có thể tham chiếu tại đây.
            RenderingServer.CanvasItemSetTransform(_canvasItem, state.Transform);
        }

        public override void _Ready()
        {
            // Tạo body.
            var body = PhysicsServer2D.BodyCreate();
            PhysicsServer2D.BodySetMode(body, PhysicsServer2D.BodyMode.Rigid);
            // Thêm một shape.
            var shape = PhysicsServer2D.RectangleShapeCreate();
            // Đặt kích thước phần mở rộng của hình chữ nhật.
            PhysicsServer2D.ShapeSetData(shape, new Vector2(10, 10));
            // Hãy nhớ giữ lại tham chiếu đến shape!
            PhysicsServer2D.BodyAddShape(body, shape);
            // Đặt space để nó va chạm trong cùng space với scene hiện tại.
            PhysicsServer2D.BodySetSpace(body, GetWorld2D().Space);
            // Di chuyển vị trí ban đầu.
            PhysicsServer2D.BodySetState(body, PhysicsServer2D.BodyState.Transform, new Transform2D(0, new Vector2(10, 20)));
            // Thêm callback transform khi body di chuyển
            // Tham số cuối cùng là tùy chọn, có thể dùng làm chỉ mục
            // nếu bạn có nhiều body và chỉ một callback.
            PhysicsServer2D.BodySetForceIntegrationCallback(body, new Callable(this, MethodName.BodyMoved), 0);

            // Cũng tạo một sprite bằng RenderingServer tại đây.
            // Xem phần bên trên về cách tạo sprite.
            // ...
        }
    }

Phiên bản 3D sẽ rất tương tự, vì các physics server 2D và 3D là giống hệt nhau (lần lượt sử dụng :ref:`class_RigidBody3D` và :ref:`class_PhysicsServer3D`).

Lấy dữ liệu từ các server
-------------------------

Hãy cố **không bao giờ** yêu cầu bất kỳ thông tin nào từ :ref:`class_RenderingServer`,
:ref:`class_PhysicsServer2D`, hoặc :ref:`class_PhysicsServer3D` bằng cách gọi các hàm, trừ khi bạn biết mình đang làm gì. Các server này thường chạy bất đồng bộ (asynchronously) để tăng hiệu suất, và việc gọi bất kỳ hàm nào trả về một giá trị sẽ làm chúng tạm dừng, buộc chúng xử lý mọi thứ đang chờ cho đến khi hàm thực sự được gọi. Điều này sẽ làm giảm hiệu suất nghiêm trọng nếu bạn gọi chúng ở mỗi frame (và sẽ không rõ lý do tại sao).

Vì vậy, hầu hết API trong các server như vậy được thiết kế để thậm chí không thể yêu cầu thông tin trả về, cho đến khi đó là dữ liệu thực tế có thể được lưu.
