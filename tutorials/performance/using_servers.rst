.. _doc_using_servers:

Tối ưu hóa bằng Servers
=======================

Các engine như Godot mang lại sự dễ sử dụng cao hơn nhờ các cấu trúc và tính năng cấp cao. Hầu hết chúng được truy cập và sử dụng thông qua
:ref:`scene system <doc_scene_tree>`. Using nodes and resources simplifies
việc tổ chức project và quản lý asset trong các game phức tạp.

Có một số nhược điểm:

- Có thêm một lớp phức tạp. - Hiệu năng thấp hơn so với khi sử dụng trực tiếp các API đơn giản. - Không thể :ref:`use multiple threads <doc_using_multiple_threads>` để điều khiển chúng. - Cần nhiều bộ nhớ hơn.

Trong hầu hết trường hợp, đây thực sự không phải là vấn đề. Godot được tối ưu hóa tốt, và hầu hết các thao tác đều được xử lý bằng signals, nghĩa là không cần polling. Tuy vậy, đôi khi chúng ta muốn khai thác hiệu năng tốt hơn từ phần cứng khi đã cạn kiệt các hướng tối ưu hóa khác. Ví dụ, việc xử lý hàng chục nghìn instance cho một tác vụ cần được thực hiện ở mỗi frame có thể trở thành một nút thắt cổ chai.

Tình huống này khiến các programmer hối tiếc vì đã sử dụng game engine và ước gì họ có thể quay lại cách triển khai code game thủ công, cấp thấp hơn.

Tuy vậy, Godot được thiết kế để xử lý vấn đề này.

.. seealso::

    Bạn có thể xem cách sử dụng các server cấp thấp hoạt động trên thực tế bằng cách sử dụng `Bullet Shower demo project <https://github.com/godotengine/godot-demo-projects/tree/master/2d/bullet_shower>`__.

Servers
-------

Một trong những quyết định thiết kế thú vị nhất của Godot là toàn bộ hệ thống scene là *tùy chọn*. Mặc dù không thể loại bỏ khi compile, bạn có thể hoàn toàn bỏ qua nó.

Về cốt lõi, Godot sử dụng khái niệm Servers. Đây là các API cấp thấp để điều khiển rendering, physics, âm thanh, v.v. Hệ thống scene được xây dựng trên chúng và sử dụng trực tiếp chúng. Các server phổ biến nhất là:

* :ref:`class_RenderingServer`: Xử lý mọi thứ liên quan đến đồ họa. * :ref:`class_PhysicsServer3D`: Xử lý mọi thứ liên quan đến physics 3D. * :ref:`class_PhysicsServer2D`: Xử lý mọi thứ liên quan đến physics 2D. * :ref:`class_AudioServer`: Xử lý mọi thứ liên quan đến âm thanh.

Hãy khám phá các API của chúng, và bạn sẽ nhận ra rằng tất cả các hàm được cung cấp đều là những triển khai cấp thấp của mọi thứ Godot cho phép bạn thực hiện bằng nodes.

RIDs
----

Chìa khóa để sử dụng các server là hiểu các object Resource ID (:ref:`RID <class_RID>`). Đây là các handle không trong suốt đến phần triển khai của server. Chúng được cấp phát và giải phóng thủ công. Hầu hết mọi hàm trong các server đều yêu cầu RIDs để truy cập resource thực tế.

Hầu hết các node và resource của Godot đều chứa các RID từ server ở bên trong, và bạn có thể lấy chúng bằng nhiều hàm khác nhau. Trên thực tế, bất kỳ thứ gì kế thừa :ref:`Resource <class_Resource>` đều có thể được cast trực tiếp thành một RID. Tuy nhiên, không phải mọi resource đều chứa một RID: trong những trường hợp đó, RID sẽ rỗng. Khi đó, resource có thể được truyền cho các API của server dưới dạng một RID.

.. warning::

    Các resource được reference-count (xem :ref:`RefCounted <class_RefCounted>`), và các tham chiếu đến RID của resource *không* được tính khi xác định liệu resource có còn đang được sử dụng hay không. Hãy đảm bảo **giữ một tham chiếu** đến resource bên ngoài server. Nếu không, cả resource và RID của nó sẽ bị xóa.

Đối với các node, có nhiều hàm khả dụng:

- Đối với CanvasItem, phương thức :ref:`CanvasItem.get_canvas_item() <class_CanvasItem_method_get_canvas_item>` sẽ trả về RID của canvas item trong server. - Đối với CanvasLayer, phương thức :ref:`CanvasLayer.get_canvas() <class_CanvasLayer_method_get_canvas>` sẽ trả về RID của canvas trong server. - Đối với Viewport, phương thức :ref:`Viewport.get_viewport_rid() <class_Viewport_method_get_viewport_rid>` sẽ trả về RID của viewport trong server. - Đối với 2D, resource :ref:`class_World2D` (có thể lấy được trong các node :ref:`class_Viewport` và :ref:`CanvasItem <class_CanvasItem>`) chứa các hàm để lấy *RenderingServer Canvas* và *PhysicsServer2D Space*. Điều này cho phép tạo các object 2D trực tiếp bằng API của server và sử dụng chúng. - Đối với 3D, resource :ref:`class_World3D` (có thể lấy được trong các node :ref:`class_Viewport` và :ref:`class_Node3D`) chứa các hàm để lấy *RenderingServer Scenario* và *PhysicsServer Space*. Điều này cho phép tạo các object 3D trực tiếp bằng API của server và sử dụng chúng. - Class :ref:`class_VisualInstance3D` cho phép lấy *instance* và *instance base* của scenario lần lượt thông qua :ref:`VisualInstance3D.get_instance() <class_VisualInstance3D_method_get_instance>` và :ref:`VisualInstance3D.get_base() <class_VisualInstance3D_method_get_base>`.

Hãy thử khám phá các node và resource mà bạn quen thuộc, rồi tìm các hàm để lấy *RIDs* của server.

Không nên điều khiển RIDs từ những object đã có node liên kết. Thay vào đó, luôn nên sử dụng các hàm của server để tạo và điều khiển các object mới, cũng như tương tác với các object hiện có.

Tạo một sprite
--------------

Đây là ví dụ về cách tạo một sprite từ code và di chuyển nó bằng cách sử dụng
:ref:`class_CanvasItem` API.

.. note::

    Khi tạo các canvas item bằng RenderingServer, bạn nên reset physics interpolation ở frame đầu tiên bằng cách sử dụng
    :ref:`RenderingServer.canvas_item_reset_physics_interpolation() <class_RenderingServer_method_canvas_item_reset_physics_interpolation>`.
    Điều này đảm bảo sự đồng bộ chính xác giữa hệ thống rendering và physics.

    Nếu không thực hiện việc này, canvas item có thể trông như dịch chuyển tức thời vào vị trí khi scene được load, thay vì xuất hiện trực tiếp tại vị trí dự kiến.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node2D


    # RenderingServer yêu cầu phải giữ các tham chiếu.
    var texture


    func _ready():
        # Tạo một canvas item, là con của node này.
        var ci_rid = RenderingServer.canvas_item_create()
        # Đặt node này làm parent.
        RenderingServer.canvas_item_set_parent(ci_rid, get_canvas_item())
        # Vẽ một texture lên đó.
        # Hãy nhớ giữ tham chiếu này.
        texture = load("res://my_texture.png")
        # Thêm nó vào, căn giữa.
        RenderingServer.canvas_item_add_texture_rect(ci_rid, Rect2(-texture.get_size() / 2, texture.get_size()), texture)
        # Thêm item, xoay 45 độ và dịch chuyển.
        var xform = Transform2D().rotated(deg_to_rad(45)).translated(Vector2(20, 30))
        RenderingServer.canvas_item_set_transform(ci_rid, xform)
        # Reset physics interpolation cho item này.
        RenderingServer.canvas_item_reset_physics_interpolation(ci_rid)

 .. code-tab:: csharp

    public partial class MyNode2D : Node2D
    {
        // RenderingServer yêu cầu phải giữ các tham chiếu.
        private Texture2D _texture;

        public override void _Ready()
        {
            // Tạo một canvas item, là con của node này.
            Rid ciRid = RenderingServer.CanvasItemCreate();
            // Đặt node này làm parent.
            RenderingServer.CanvasItemSetParent(ciRid, GetCanvasItem());
            // Vẽ một texture lên đó.
            // Hãy nhớ giữ tham chiếu này.
            _texture = ResourceLoader.Load<Texture2D>("res://my_texture.png");
            // Thêm nó vào, căn giữa.
            RenderingServer.CanvasItemAddTextureRect(ciRid, new Rect2(-_texture.GetSize() / 2, _texture.GetSize()), _texture.GetRid());
            // Thêm item, xoay 45 độ và dịch chuyển.
            Transform2D xform = Transform2D.Identity.Rotated(Mathf.DegToRad(45)).Translated(new Vector2(20, 30));
            RenderingServer.CanvasItemSetTransform(ciRid, xform);
            // Reset physics interpolation cho item này.
            RenderingServer.CanvasItemResetPhysicsInterpolation(ciRid);
        }
    }

Canvas Item API trong server cho phép bạn thêm các draw primitive vào đó. Sau khi được thêm, chúng không thể được sửa đổi. Item cần được xóa và các primitive phải được thêm lại. Điều này không áp dụng cho việc thiết lập transform, vốn có thể được thực hiện bao nhiêu lần tùy ý.

Các primitive được xóa như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    RenderingServer.canvas_item_clear(ci_rid)

 .. code-tab:: csharp

    RenderingServer.CanvasItemClear(ciRid);


Khởi tạo một Mesh vào không gian 3D
-----------------------------------

Các API 3D khác với API 2D, vì vậy phải sử dụng API khởi tạo.

.. tabs::
 .. code-tab:: gdscript GDScript

    extends Node3D


    # RenderingServer yêu cầu phải giữ các tham chiếu.
    var mesh


    func _ready():
        # Tạo một visual instance (cho 3D).
        var instance = RenderingServer.instance_create()
        # Đặt scenario từ world. Điều này đảm bảo nó
        # xuất hiện cùng các object như scene.
        var scenario = get_world_3d().scenario
        RenderingServer.instance_set_scenario(instance, scenario)
        # Thêm một mesh vào đó.
        # Hãy nhớ giữ tham chiếu này.
        mesh = load("res://my_mesh.obj")
        RenderingServer.instance_set_base(instance, mesh)
        # Di chuyển mesh.
        var xform = Transform3D(Basis(), Vector3(2, 3, 0))
        RenderingServer.instance_set_transform(instance, xform)

 .. code-tab:: csharp

    public partial class MyNode3D : Node3D
    {
        // RenderingServer yêu cầu phải giữ các tham chiếu.
        private Mesh _mesh;

        public override void _Ready()
        {
            // Tạo một visual instance (cho 3D).
            Rid instance = RenderingServer.InstanceCreate();
            // Đặt scenario từ world. Điều này đảm bảo nó
            // xuất hiện cùng các object như scene.
            Rid scenario = GetWorld3D().Scenario;
            RenderingServer.InstanceSetScenario(instance, scenario);
            // Thêm một mesh vào đó.
            // Hãy nhớ giữ tham chiếu này.
            _mesh = ResourceLoader.Load<Mesh>("res://my_mesh.obj");
            RenderingServer.InstanceSetBase(instance, _mesh.GetRid());
            // Di chuyển mesh.
            Transform3D xform = new Transform3D(Basis.Identity, new Vector3(2, 3, 0));
            RenderingServer.InstanceSetTransform(instance, xform);
        }
    }

Tạo một RigidBody 2D và di chuyển sprite bằng nó
------------------------------------------------

Đoạn này tạo một :ref:`class_RigidBody2D` bằng API :ref:`class_PhysicsServer2D`, và di chuyển một :ref:`class_CanvasItem` khi body di chuyển.

.. tabs::
 .. code-tab:: gdscript GDScript

    # PhysicsServer2D yêu cầu phải giữ các tham chiếu.
    var body
    var shape


    func _body_moved(state, index):
        # Đã tạo canvas item của riêng bạn; sử dụng nó ở đây.
        # `ci_rid` từ ví dụ sprite ở trên cần được chuyển vào một
        # biến thành viên (thay vì nằm trong `_ready()`) để có thể được tham chiếu ở đây.
        RenderingServer.canvas_item_set_transform(ci_rid, state.transform)


    func _ready():
        # Tạo body.
        body = PhysicsServer2D.body_create()
        PhysicsServer2D.body_set_mode(body, PhysicsServer2D.BODY_MODE_RIGID)
        # Thêm một shape.
        shape = PhysicsServer2D.rectangle_shape_create()
        # Thiết lập kích thước của hình chữ nhật.
        PhysicsServer2D.shape_set_data(shape, Vector2(10, 10))
        # Hãy đảm bảo giữ tham chiếu đến shape!
        PhysicsServer2D.body_add_shape(body, shape)
        # Thiết lập space để nó va chạm trong cùng space với scene hiện tại.
        PhysicsServer2D.body_set_space(body, get_world_2d().space)
        # Di chuyển vị trí ban đầu.
        PhysicsServer2D.body_set_state(body, PhysicsServer2D.BODY_STATE_TRANSFORM, Transform2D(0, Vector2(10, 20)))
        # Thêm callback transform khi body di chuyển
        # Tham số cuối cùng là tùy chọn, có thể được dùng làm index
        # nếu bạn có nhiều body và một callback duy nhất.
        PhysicsServer2D.body_set_force_integration_callback(body, self, "_body_moved", 0)

        # Cũng tạo một sprite bằng RenderingServer ở đây.
        # Xem phần bên trên về cách tạo một sprite.
        # ...

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode2D : Node2D
    {
        private Rid _canvasItem;

        private void BodyMoved(PhysicsDirectBodyState2D state, int index)
        {
            // Đã tạo canvas item của riêng bạn; sử dụng nó ở đây.
            // `ciRid` từ ví dụ sprite ở trên cần được chuyển vào một
            // biến thành viên (thay vì nằm trong `_Ready()`) để có thể được tham chiếu ở đây.
            RenderingServer.CanvasItemSetTransform(_canvasItem, state.Transform);
        }

        public override void _Ready()
        {
            // Tạo body.
            var body = PhysicsServer2D.BodyCreate();
            PhysicsServer2D.BodySetMode(body, PhysicsServer2D.BodyMode.Rigid);
            // Thêm một shape.
            var shape = PhysicsServer2D.RectangleShapeCreate();
            // Thiết lập kích thước của hình chữ nhật.
            PhysicsServer2D.ShapeSetData(shape, new Vector2(10, 10));
            // Hãy đảm bảo giữ tham chiếu đến shape!
            PhysicsServer2D.BodyAddShape(body, shape);
            // Thiết lập space để nó va chạm trong cùng space với scene hiện tại.
            PhysicsServer2D.BodySetSpace(body, GetWorld2D().Space);
            // Di chuyển vị trí ban đầu.
            PhysicsServer2D.BodySetState(body, PhysicsServer2D.BodyState.Transform, new Transform2D(0, new Vector2(10, 20)));
            // Thêm callback transform khi body di chuyển
            // Tham số cuối cùng là tùy chọn, có thể được dùng làm index
            // nếu bạn có nhiều body và một callback duy nhất.
            PhysicsServer2D.BodySetForceIntegrationCallback(body, new Callable(this, MethodName.BodyMoved), 0);

            // Cũng tạo một sprite bằng RenderingServer ở đây.
            // Xem phần bên trên về cách tạo một sprite.
            // ...
        }
    }

Phiên bản 3D sẽ rất tương tự, vì các physics server 2D và 3D giống hệt nhau (lần lượt sử dụng :ref:`class_RigidBody3D` và :ref:`class_PhysicsServer3D`).

Lấy dữ liệu từ các server
-------------------------

Hãy **không bao giờ** yêu cầu bất kỳ thông tin nào từ :ref:`class_RenderingServer`,
:ref:`class_PhysicsServer2D`, or :ref:`class_PhysicsServer3D` by calling
các function trừ khi bạn biết mình đang làm gì. Những server này thường chạy bất đồng bộ (asynchronously) để đạt hiệu năng tốt hơn, và việc gọi bất kỳ function nào trả về một giá trị sẽ làm chúng bị đình trệ, buộc chúng phải xử lý mọi thứ đang chờ cho đến khi function thực sự được gọi. Điều này sẽ làm giảm hiệu năng nghiêm trọng nếu bạn gọi chúng ở mỗi frame (và sẽ không dễ nhận ra nguyên nhân).

Vì lý do này, hầu hết API trên những server như vậy được thiết kế để thậm chí không thể yêu cầu trả về thông tin, cho đến khi đó là dữ liệu thực tế có thể được lưu lại.
