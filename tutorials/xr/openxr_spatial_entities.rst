.. _doc_openxr_spatial_entities:

Các thực thể không gian OpenXR
==============================

Đối với mọi loại ứng dụng thực tế tăng cường, bạn cần truy cập thông tin về thế giới thực và có khả năng theo dõi các vị trí trong thế giới thực. API spatial entities của OpenXR được giới thiệu chính xác để phục vụ mục đích này.

API này có thiết kế rất mô-đun. Phần cốt lõi của API xác định cách các thực thể trong thế giới thực được cấu trúc, cách tìm thấy chúng cũng như cách thông tin về chúng được lưu trữ và truy cập.

Nhiều extension khác nhau được thêm vào bên trên để triển khai các hệ thống cụ thể như theo dõi marker, theo dõi mặt phẳng và anchor. Chúng được gọi là spatial capabilities.

Mỗi thực thể có thể được hệ thống xử lý được chia thành các component nhỏ hơn, nhờ đó dễ dàng mở rộng hệ thống và thêm các capability mới.

Các nhà cung cấp có khả năng triển khai và cung cấp thêm các capability cùng loại component có thể được sử dụng với core API. Trong Godot, những capability này có thể được triển khai trong các extension. Tuy nhiên, các triển khai này nằm ngoài phạm vi của tài liệu hướng dẫn này.

Cuối cùng, điều quan trọng cần lưu ý là hệ thống spatial entity sử dụng các hàm bất đồng bộ (asynchronous functions). Điều này có nghĩa là bạn có thể bắt đầu một quy trình, sau đó được thông báo khi quy trình hoàn tất.

Thiết lập
---------

Để sử dụng spatial entities, bạn cần bật các project settings liên quan. Bạn có thể tìm thấy chúng trong phần OpenXR:

.. image:: img/openxr_spatial_entities_project_settings.webp

.. list-table:: Spatial entity settings
   :header-rows: 1

   * - Cài đặt
     - Mô tả
   * - Đã bật
     - Bật phần cốt lõi của hệ thống spatial entities. Phải bật mục này để bất kỳ hệ thống spatial
       entities nào hoạt động.
   * - Bật spatial anchors
     - Bật capability spatial anchors, cho phép tạo và theo dõi spatial anchors.
   * - Bật persistent anchors
     - Bật khả năng duy trì spatial anchors. Điều này có nghĩa là vị trí của chúng được lưu trữ
       và có thể được truy xuất trong các session tiếp theo.
   * - Bật phát hiện anchor tích hợp sẵn
     - Bật logic phát hiện anchor tích hợp sẵn của chúng tôi; logic này sẽ tự động truy xuất các persistent anchors
       và điều chỉnh vị trí của các anchor khi việc tracking được cập nhật.
   * - Bật plane tracking
     - Bật capability plane tracking, cho phép phát hiện các bề mặt như sàn nhà, tường,
       trần nhà và bàn.
   * - Bật phát hiện plane tích hợp sẵn
     - Bật logic phát hiện plane tích hợp sẵn của chúng tôi; logic này sẽ tự động phản hồi khi dữ liệu plane mới
       trở nên khả dụng.
   * - Bật marker tracking
     - Bật capability marker tracking của chúng tôi, cho phép phát hiện các marker như mã QR,
       marker Aruco và April tags.
   * - Bật marker tracking tích hợp sẵn
     - Bật logic phát hiện marker tích hợp sẵn của chúng tôi; logic này sẽ tự động phản hồi khi các marker mới được
       tìm thấy hoặc khi các marker được di chuyển trong không gian của người chơi.

.. note::

    Lưu ý rằng nhiều thiết bị XR cũng yêu cầu thiết lập các permission flags. Bạn cần bật chúng trong phần export preset settings.

Việc bật các capability khác nhau sẽ kích hoạt các OpenXR API liên quan, nhưng cần thêm logic để tương tác với dữ liệu này. Đối với mỗi hệ thống cốt lõi, chúng tôi có logic tích hợp sẵn mà bạn có thể bật để thực hiện việc này thay mình.

Chúng ta sẽ thảo luận về hệ thống spatial entities với giả định rằng trước tiên logic tích hợp sẵn đã được bật. Sau đó, chúng ta sẽ xem xét các API nền tảng và cách bạn có thể tự triển khai chúng. Tuy nhiên, cần lưu ý rằng việc này thường là quá mức cần thiết và các API nền tảng chủ yếu được cung cấp để các plugin GDExtension triển khai thêm capability.

Tạo spatial manager
-------------------

Khi các spatial entities được phát hiện hoặc tạo, một
:ref:`OpenXRSpatialEntityTracker<class_OpenXRSpatialEntityTracker>`
object sẽ được khởi tạo và đăng ký với :ref:`XRServer<class_XRServer>`.

Mỗi loại spatial entity sẽ triển khai subclass riêng, vì vậy chúng ta có thể phản hồi khác nhau đối với từng loại entity.

Nói chung, chúng ta sẽ instance các subscene khác nhau cho từng loại entity. Vì các tracker object có thể được sử dụng với các node :ref:`XRAnchor3D<class_XRAnchor3D>`, những subscene này nên có một node như vậy làm root node.

Tất cả entity tracker sẽ cung cấp vị trí của chúng thông qua pose ``default``.

Chúng ta có thể tự động hóa việc tạo các subscene và thêm chúng vào scene tree bằng cách tạo một manager object. Vì tất cả vị trí đều là local so với node :ref:`XROrigin3D<class_XROrigin3D>`, chúng ta nên tạo manager dưới dạng node con của origin node.

Dưới đây là phần cơ bản của script triển khai logic manager của chúng ta:

.. code-block:: gdscript

    class_name SpatialEntitiesManager
    extends Node3D

    ## Phát tín hiệu khi một node spatial entity mới được thêm vào.
    signal added_spatial_entity(node: XRNode3D)

    ## Phát tín hiệu ngay trước khi một node spatial entity bị xóa.
    signal removed_spatial_entity(node: XRNode3D)

    ## Scene sẽ được instance cho các spatial anchor entity.
    @export var spatial_anchor_scene: PackedScene

    ## Scene sẽ được instance cho các spatial entity theo dõi plane.
    @export var plane_tracker_scene: PackedScene

    ## Scene sẽ được instance cho các spatial entity theo dõi marker.
    @export var marker_tracker_scene: PackedScene

    # Các tracker mà chúng ta quản lý node cho chúng.
    var _managed_nodes: Dictionary[XRTracker, XRAnchor3D]

    # Enter tree được gọi mỗi khi node của chúng ta được thêm vào scene.
    func _enter_tree():
        # Kết nối với các signal thông báo cho chúng ta về những thay đổi của tracker.
        XRServer.tracker_added.connect(_on_tracker_added)
        XRServer.tracker_updated.connect(_on_tracker_updated)
        XRServer.tracker_removed.connect(_on_tracker_removed)

        # Thiết lập các tracker hiện có.
        var trackers : Dictionary = XRServer.get_trackers(XRServer.TRACKER_ANCHOR)
        for tracker_name in trackers:
            var tracker: XRTracker = trackers[tracker_name]
            if tracker and tracker is OpenXRSpatialEntityTracker:
                _add_tracker(tracker)


    # Exit tree được gọi mỗi khi node của chúng ta bị xóa khỏi scene.
    func _exit_tree():
        # Dọn dẹp các signal của chúng ta.
        XRServer.tracker_added.disconnect(_on_tracker_added)
        XRServer.tracker_updated.disconnect(_on_tracker_updated)
        XRServer.tracker_removed.disconnect(_on_tracker_removed)

        # Dọn dẹp các tracker.
        for tracker in _managed_nodes:
            removed_spatial_entity.emit(_managed_nodes[tracker])
            remove_child(_managed_nodes[tracker])
            _managed_nodes[tracker].queue_free()

        _managed_nodes.clear()


    # Kiểm tra xem tracker này có nên được chúng ta quản lý hay không và thêm nó vào.
    func _add_tracker(tracker: OpenXRSpatialEntityTracker):
        var new_node: XRAnchor3D

        if _managed_nodes.has(tracker):
            # Đã được chúng ta quản lý!
            return

        if tracker is OpenXRAnchorTracker:
            # Note: Generally spatial anchors are controlled by the developer and
            # khó có khả năng được manager của chúng ta xử lý.
            # Nhưng để đầy đủ, chúng ta vẫn sẽ thêm nó vào.
            if spatial_anchor_scene:
                var new_scene = spatial_anchor_scene.instantiate()
                if new_scene is XRAnchor3D:
                    new_node = new_scene
                else:
                    push_error("Spatial anchor scene doesn't have an XRAnchor3D as a root node and can't be used!")
                    new_scene.free()
        elif tracker is OpenXRPlaneTracker:
            if plane_tracker_scene:
                var new_scene = plane_tracker_scene.instantiate()
                if new_scene is XRAnchor3D:
                    new_node = new_scene
                else:
                    push_error("Plane tracking scene doesn't have an XRAnchor3D as a root node and can't be used!")
                    new_scene.free()
        elif tracker is OpenXRMarkerTracker:
            if marker_tracker_scene:
                var new_scene = marker_tracker_scene.instantiate()
                if new_scene is XRAnchor3D:
                    new_node = new_scene
                else:
                    push_error("Marker tracking scene doesn't have an XRAnchor3D as a root node and can't be used!")
                    new_scene.free()
        else:
            # Loại spatial entity tracker mà chúng ta không hỗ trợ?
            push_warning("OpenXR Spatial Entities: Unsupported anchor tracker " + tracker.get_name() + " of type " + tracker.get_class())

        if not new_node:
            # Không có scene được xác định hoặc không thể instance? Vậy là xong!
            return

        # Thiết lập và thêm vào scene của chúng ta.
        new_node.tracker = tracker.name
        new_node.pose = "default"
        _managed_nodes[tracker] = new_node
        add_child(new_node)

        added_spatial_entity.emit(new_node)


    # Một tracker mới đã được thêm vào XRServer của chúng ta.
    func _on_tracker_added(tracker_name: StringName, type: int):
        if type == XRServer.TRACKER_ANCHOR:
            var tracker: XRTracker = XRServer.get_tracker(tracker_name)
            if tracker and tracker is OpenXRSpatialEntityTracker:
                _add_tracker(tracker)


    # Một tracker được XRServer quản lý đã thay đổi.
    func _on_tracker_updated(_tracker_name: StringName, _type: int):
        # Hiện tại chúng ta bỏ qua việc này vì không có thay đổi nào ở đây mà chúng ta cần phản hồi
        # và scene đã được instance có thể tự phản hồi nếu cần.
        pass


    # Một tracker đã bị xóa khỏi XRServer của chúng ta.
    func _on_tracker_removed(tracker_name: StringName, type: int):
        if type == XRServer.TRACKER_ANCHOR:
            var tracker: XRTracker = XRServer.get_tracker(tracker_name)
            if _managed_nodes.has(tracker):
                # Chúng ta phát tín hiệu này ngay trước khi xóa nó!
                removed_spatial_entity.emit(_managed_nodes[tracker])

                # Xóa node.
                remove_child(_managed_nodes[tracker])

                # Đưa node vào hàng đợi để giải phóng.
                _managed_nodes[tracker].queue_free()

                # Và xóa khỏi các node được chúng ta quản lý.
                _managed_nodes.erase(tracker)

Spatial anchors
---------------

Spatial anchors cho phép chúng ta ánh xạ các vị trí trong thế giới thực vào thế giới ảo theo cách mà XR runtime sẽ tiếp tục theo dõi các vị trí này và điều chỉnh chúng khi cần. Nếu được hỗ trợ, các anchor có thể được duy trì, nghĩa là chúng sẽ được tạo lại ở đúng vị trí khi ứng dụng của bạn khởi động lại.

Bạn có thể hình dung các trường hợp sử dụng như: - đặt các cửa sổ ảo xung quanh không gian của bạn để chúng được tạo lại khi ứng dụng khởi động lại - đặt các object ảo trên bàn hoặc tường và tạo lại chúng

Spatial anchors được theo dõi bằng các object :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>` được đăng ký với XRServer.

Khi cần, vị trí của spatial anchor sẽ được tự động cập nhật; pose trên tracker liên quan sẽ được cập nhật và do đó node :ref:`XRAnchor3D<class_XRAnchor3D>` sẽ được định vị lại.

Khi một spatial anchor được duy trì, một Universally Unique Identifier (hay UUID) sẽ được gán cho anchor đó. Bạn cần lưu UUID này cùng với mọi thông tin cần thiết để tái tạo scene. Trong code mẫu dưới đây, chúng ta sẽ gọi đơn giản là ``set_scene_path`` và ``get_scene_path``, nhưng bạn sẽ cần tự cung cấp các triển khai cho những hàm này.

Để tạo một persistent anchor, bạn cần thực hiện theo một quy trình cụ thể: - Tạo spatial anchor - Chờ cho đến khi trạng thái tracking thay đổi thành ``ENTITY_TRACKING_STATE_TRACKING`` - Duy trì anchor - Lấy UUID và lưu lại

Khi tìm thấy một persistent anchor hiện có, một tracker mới sẽ được thêm vào và UUID đã được thiết lập sẵn. Sự khác biệt trong workflow này cho phép chúng ta phản hồi chính xác với các persistent anchor mới và hiện có.

.. note::

    Nếu bạn hủy trạng thái persistent của một anchor, UUID sẽ bị hủy nhưng anchor không tự động bị xóa. Bạn cần phản hồi khi việc hủy trạng thái persistent của anchor hoàn tất, sau đó dọn dẹp anchor. Ngoài ra, bạn sẽ nhận được lỗi nếu cố gắng hủy một anchor vẫn đang ở trạng thái persistent.

Để hoàn thiện hệ thống anchor, trước tiên chúng ta tạo một scene và đặt scene đó làm scene sẽ được instance cho các anchor trên spatial manager node.

Scene này nên có một node :ref:`XRAnchor3D<class_XRAnchor3D>` làm root nhưng không có gì khác. Chúng ta sẽ thêm một script vào đó để load một subscene chứa phần hiển thị thực tế của anchor, nhờ đó có thể tạo các anchor khác nhau trong scene. Chúng ta sẽ giả định mục đích là duy trì các anchor này và lưu path đến subscene dưới dạng metadata cho UUID của chúng.

.. code-block:: gdscript

    class_name OpenXRSpatialAnchor3D
    extends XRAnchor3D

    var anchor_tracker: OpenXRAnchorTracker
    var child_scene: Node
    var made_persistent: bool = false

    ## Trả về path của scene cho UUID của chúng ta.
    func get_scene_path(p_uuid: String) -> String:
        # Placeholder, hãy triển khai phần này.
        return ""


    ## Lưu path của scene cho UUID của chúng ta.
    func set_scene_path(p_uuid: String, p_scene_path: String):
        # Placeholder, hãy triển khai phần này.
        pass


    ## Xóa thông tin liên quan đến UUID của chúng ta.
    func remove_uuid(p_uuid: String):
        # Placeholder, hãy triển khai phần này.
        pass


    ## Thiết lập scene con cho anchor này; gọi hàm này khi tạo anchor mới.
    func set_child_scene(p_child_scene_path: String):
        var packed_scene: PackedScene = load(p_child_scene_path)
        if not packed_scene:
            return

        child_scene = packed_scene.instantiate()
        if not child_scene:
            return

        add_child(child_scene)


    # Được gọi khi trạng thái tracking của chúng ta thay đổi.
    func _on_spatial_tracking_state_changed(new_state) -> void:
        if new_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_TRACKING and not made_persistent:
            # Chỉ thử thực hiện việc này một lần.
            made_persistent = true

            # Cảnh báo này là tùy chọn nếu bạn không muốn phụ thuộc vào persistence.
            if not OpenXRSpatialAnchorCapability.is_spatial_persistence_supported():
                push_warning("Persistent spatial anchors are not supported on this device!")
                return

            # Lưu trạng thái này, thao tác này sẽ thông báo rằng UUID đã thay đổi trên anchor,
            # sau đó chúng ta có thể lưu đường dẫn scene mà chúng ta đã áp dụng cho
            # scene được theo dõi.
            OpenXRSpatialAnchorCapability.persist_anchor(anchor_tracker, RID(), Callable())


    func _on_uuid_changed() -> void:
        if anchor_tracker.uuid != "":
            made_persistent = true

            if child_scene:
                # Nếu đã có subscene, hãy lưu subscene đó cùng với UUID.
                set_scene_path(anchor_tracker.uuid, child_scene.scene_file_path)
            else:
                # Nếu chưa có, hãy tra UUID trong cache đã lưu.
                var scene_path: String = get_scene_path(anchor_tracker.uuid)
                if scene_path.is_empty():
                    # Hiển thị cảnh báo rằng chúng ta không có file scene được lưu cho UUID này.
                    push_warning("Unknown UUID given, can't determine child scene.")

                    # Tải một scene mặc định để ít nhất chúng ta có thể nhìn thấy thứ gì đó.
                    set_child_scene("res://unknown_anchor.tscn")
                    return

                set_child_scene(scene_path)


    func _ready():
        anchor_tracker = XRServer.get_tracker(tracker)
        if anchor_tracker:
            _on_uuid_changed()

            anchor_tracker.spatial_tracking_state_changed.connect(_on_spatial_tracking_state_changed)
            anchor_tracker.uuid_changed.connect(_on_uuid_changed)

Sau khi đã có anchor scene, chúng ta có thể thêm một vài function vào script spatial manager để tạo hoặc xóa anchor:

.. code-block:: gdscript

    ...

    ## Tạo một spatial anchor mới cùng với child scene tương ứng.
    ## Nếu persistent anchor được hỗ trợ, anchor này sẽ được tạo dưới dạng persistent node
    ## và chúng ta sẽ lưu đường dẫn child scene cùng với UUID của anchor để tái tạo trong tương lai.
    func create_spatial_anchor(p_transform: Transform3D, p_child_scene_path: String):
        # Chúng ta có hỗ trợ anchor không?
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            push_error("Spatial anchors are not supported on this device!")
            return

        # Điều chỉnh transform sang local space.
        var t: Transform3D = global_transform.inverse() * p_transform

        # Tạo anchor trên manager hiện tại.
        var new_anchor = OpenXRSpatialAnchorCapability.create_new_anchor(t, RID())
        if not new_anchor:
            push_error("Couldn't create an anchor for %s." % [ p_child_scene_path ])
            return

        # Việc tạo anchor mới sẽ thêm một XRAnchor vào scene
        # bởi manager của chúng ta. Vì vậy, chúng ta có thể tiếp tục với giả định rằng việc này đã xảy ra.

        var anchor_scene = get_tracked_scene(new_anchor)
        if not anchor_scene:
            push_error("Couldn't locate anchor scene for %s, has the manager been configured with an applicable anchor scene?" % [ new_anchor.name ])
            return
        if not anchor_scene is OpenXRSpatialAnchor3D:
            push_error("Anchor scene for %s is not an OpenXRSpatialAnchor3D scene, has the manager been configured with an applicable anchor scene?" % [ new_anchor.name ])
            return

        anchor_scene.set_child_scene(p_child_scene_path)


    ## Xóa spatial anchor này khỏi scene của chúng ta.
    ## Nếu spatial anchor là persistent, UUID tương ứng sẽ được xóa.
    func remove_spatial_anchor(p_anchor: XRAnchor3D):
        # Chúng ta có hỗ trợ anchor không?
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            push_error("Spatial anchors are not supported on this device!")
            return

        var tracker: XRTracker = XRServer.get_tracker(p_anchor.tracker)
        if tracker and tracker is OpenXRAnchorTracker:
            var anchor_tracker: OpenXRAnchorTracker = tracker
            if anchor_tracker.has_uuid() and OpenXRSpatialAnchorCapability.is_spatial_persistence_supported():
                # Nếu có UUID, trước tiên chúng ta nên hủy trạng thái persistent của anchor
                # rồi xóa nó trong callback của anchor.
                remove_uuid(anchor_tracker.uuid)
                OpenXRSpatialAnchorCapability.unpersist_anchor(anchor_tracker, RID(), _on_unpersist_complete)
            else:
                # Nếu không, chúng ta chỉ cần xóa nó.
                # Thao tác này sẽ xóa nó khỏi XRServer, từ đó kích hoạt việc dọn dẹp node của chúng ta.
                OpenXRSpatialAnchorCapability.remove_anchor(tracker)


    func _on_unpersist_complete(p_tracker: XRTracker):
        # Tracker của chúng ta giờ không còn persistent nữa, chúng ta có thể xóa nó.
        OpenXRSpatialAnchorCapability.remove_anchor(p_tracker)


    ## Lấy scene mà chúng ta đã thêm cho một tracker nhất định (nếu có).
    func get_tracked_scene(p_tracker: XRTracker) -> XRNode3D:
        for node in get_children():
            if node is XRNode3D and node.tracker == p_tracker.name:
                return node

        return null

.. note::

    Có vẻ như đoạn code trên đang thực hiện một chút phép thuật. Bất cứ khi nào một spatial anchor được tạo hoặc xóa trên anchor capability, đối tượng tracker liên quan sẽ được tạo hoặc hủy. Điều này khiến spatial manager thêm hoặc xóa child scene cho anchor này. Vì vậy, chúng ta có thể dựa vào điều đó ở đây.

Theo dõi mặt phẳng
------------------

Tính năng theo dõi mặt phẳng cho phép chúng ta phát hiện các bề mặt như tường, sàn, trần nhà và bàn ở gần người chơi. Dữ liệu này có thể đến từ quá trình chụp lại căn phòng do người dùng thực hiện vào bất kỳ thời điểm nào trước đó hoặc được các cảm biến quang học phát hiện trực tiếp. Plane tracking extension không phân biệt hai trường hợp này.

.. note::

    Một số XR runtime yêu cầu vendor extension để bật và/hoặc cấu hình quy trình này, nhưng dữ liệu sẽ được cung cấp thông qua extension này.

Đoạn code chúng ta đã viết ở trên cho spatial manager sẽ tự động phát hiện các plane mới. Tuy nhiên, chúng ta cần thiết lập một scene mới và gán scene đó cho spatial manager.

Node gốc của scene này phải là một node :ref:`XRAnchor3D<class_XRAnchor3D>`. Chúng ta sẽ thêm một node :ref:`StaticBody3D<class_StaticBody3D>` làm node con và thêm một
:ref:`CollisionShape3D<class_CollisionShape3D>` and :ref:`MeshInstance3D<class_MeshInstance3D>`
node làm các node con của static body.

.. image:: img/openxr_plane_anchor.webp

Static body và collision shape sẽ cho phép chúng ta làm cho plane có thể tương tác.

Mesh instance node cho phép chúng ta áp dụng material "hole punch" cho plane; khi kết hợp với passthrough, nó biến plane thành một visual occluder. Ngoài ra, chúng ta có thể gán một material trực quan hóa plane để debug.

Chúng ta cấu hình material này làm material ``material_override`` trên MeshInstance3D. Đối với material "hole punch", hãy tạo một :ref:`ShaderMaterial<class_ShaderMaterial>` và sử dụng đoạn code sau làm shader code:

.. code-block:: glsl

    shader_type spatial;
    render_mode unshaded, shadow_to_opacity;

    void fragment() {
        ALBEDO = vec3(0.0, 0.0, 0.0);
    }

Chúng ta cũng cần thêm một script vào scene để đảm bảo collision và mesh của chúng ta được áp dụng.

.. code-block:: gdscript

    extends XRAnchor3D

    var plane_tracker: OpenXRPlaneTracker

    func _update_mesh_and_collision():
        if plane_tracker:
            # Đặt static body bằng offset của chúng ta để cả collision
            # và mesh đều được định vị chính xác.
            $StaticBody3D.transform = plane_tracker.get_mesh_offset()

            # Thiết lập mesh để chúng ta có thể che khuất bề mặt.
            $StaticBody3D/MeshInstance3D.mesh = plane_tracker.get_mesh()

            # Và thiết lập shape để các vật thể có thể va chạm với bề mặt của chúng ta.
            $StaticBody3D/CollisionShape3D.shape = plane_tracker.get_shape()


    func _ready():
        plane_tracker = XRServer.get_tracker(tracker)
        if plane_tracker:
            _update_mesh_and_collision()

            plane_tracker.mesh_changed.connect(_update_mesh_and_collision)

Nếu được XR runtime hỗ trợ, bạn có thể truy vấn thêm metadata trên plane tracker object. Đáng chú ý là property ``plane_label``; nếu có, property này xác định loại bề mặt. Vui lòng tham khảo tài liệu về class :ref:`OpenXRPlaneTracker<class_OpenXRPlaneTracker>` để biết thêm thông tin.

Theo dõi marker
---------------

Marker tracking phát hiện các marker cụ thể trong thế giới thực. Đây thường là những hình ảnh được in, chẳng hạn như mã QR.

API cung cấp hỗ trợ cho 4 loại mã khác nhau: mã QR, mã Micro QR, mã Aruco và April tag; tuy nhiên, XR runtime không bắt buộc phải hỗ trợ tất cả các loại này.

Khi phát hiện được marker, các object :ref:`OpenXRMarkerTracker<class_OpenXRMarkerTracker>` sẽ được khởi tạo và đăng ký với XRServer.

Code spatial manager hiện có của chúng ta đã tự động phát hiện các marker này; tất cả những gì cần làm là tạo một scene có node :ref:`XRAnchor3D<class_XRAnchor3D>` ở gốc, lưu scene đó và gán nó cho spatial manager làm scene cần khởi tạo cho các marker.

Marker tracker phải được cấu hình đầy đủ khi được gán, vì vậy tất cả những gì cần thiết là một function ``_ready`` phản hồi dữ liệu marker. Dưới đây là template cho đoạn code bắt buộc:

.. code-block:: gdscript

    extends XRAnchor3D

    var marker_tracker: OpenXRMarkerTracker

    func _ready():
        marker_tracker = XRServer.get_tracker(tracker)
        if marker_tracker:
            match marker_tracker.marker_type:
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_QRCODE:
                    var data = marker_tracker.get_marker_data()
                    if data is String:
                        # Dữ liệu là một mã QR dạng chuỗi, thường là một URL.
                        pass
                    elif data is PackedByteArray:
                        # Dữ liệu ở dạng binary, có thể là bất kỳ thứ gì.
                        pass
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_MICRO_QRCODE:
                    var data = marker_tracker.get_marker_data()
                    if data is String:
                        # Dữ liệu là một mã QR dạng chuỗi, thường là một URL.
                        pass
                    elif data is PackedByteArray:
                        # Dữ liệu ở dạng binary, có thể là bất kỳ thứ gì.
                        pass
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_ARUCO:
                    # Sử dụng marker_tracker.marker_id để xác định marker.
                    pass
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_APRIL_TAG:
                    # Sử dụng marker_tracker.marker_id để xác định marker.
                    pass

Như chúng ta có thể thấy, QR Code cung cấp một block dữ liệu có thể là chuỗi hoặc mảng byte. Aruco và April tag cung cấp một ID được đọc từ mã.

Cách liên kết dữ liệu marker với scene cần được tải như thế nào là tùy thuộc vào trường hợp sử dụng của bạn. Một ví dụ là mã hóa tên của asset bạn muốn hiển thị vào mã QR.

Truy cập backend
----------------

Đối với hầu hết mục đích, core system cùng với mọi vendor extension sẽ là những gì mà phần lớn người dùng sử dụng theo cách được cung cấp.

Đối với những người triển khai vendor extension hoặc những người mà logic tích hợp sẵn không đáp ứng đủ nhu cầu, quyền truy cập backend được cung cấp thông qua một tập hợp các singleton object.

Các object này cũng có thể được dùng để truy vấn những capability nào được headset đang sử dụng hỗ trợ. Chúng ta đã thêm code kiểm tra các capability này trong spatial manager và spatial anchor ở các phần trên.

.. note::

    Hệ thống spatial entities sẽ đóng gói nhiều OpenXR entity vào các resource được trả về dưới dạng RID.

Spatial entity core
~~~~~~~~~~~~~~~~~~~

Chức năng spatial entity cốt lõi được cung cấp thông qua
:ref:`OpenXRSpatialEntityExtension<class_OpenXRSpatialEntityExtension>` singleton.

Logic cụ thể được cung cấp thông qua các capability, trong đó giới thiệu những component type chuyên biệt và cho phép truy cập các entity type cụ thể; tuy nhiên, tất cả đều sử dụng cùng một cơ chế để truy cập dữ liệu entity do hệ thống spatial entity quản lý.

Chúng ta sẽ bắt đầu bằng cách xem xét các component riêng lẻ tạo nên core system.

Spatial context
"""""""""""""""

Spatial context là object chính mà thông qua đó chúng ta truy vấn hệ thống spatial entities. Spatial context cho phép chúng ta cấu hình cách tương tác với một hoặc nhiều capability.

Bạn nên tạo một spatial context cho mỗi capability mà bạn muốn tương tác; trên thực tế, đây cũng là cách Godot thực hiện đối với logic tích hợp sẵn.

Chúng ta bắt đầu bằng cách thiết lập các capability configuration object cho những capability mà mình muốn truy cập. Mỗi capability sẽ bật các component được hỗ trợ cho capability đó. Các setting có thể quyết định component nào sẽ được bật. Chúng ta sẽ xem xét các configuration object này chi tiết hơn khi tìm hiểu từng capability được hỗ trợ.

Tạo một spatial context là một thao tác bất đồng bộ (asynchronous). Điều này có nghĩa là chúng ta yêu cầu XR runtime tạo một spatial context, rồi tại một thời điểm trong tương lai, XR runtime sẽ cung cấp kết quả cho chúng ta.

Script sau đây là phần khởi đầu của ví dụ và có thể được thêm dưới dạng một node vào scene của bạn. Script minh họa việc tạo một spatial context cho plane tracking và thiết lập quá trình khám phá entity.

.. code-block:: gdscript

    extends Node

    var spatial_context: RID

    func _set_up_spatial_context():
        # Đã thiết lập?
        if spatial_context:
            return

        # Không được hỗ trợ hoặc chúng ta chưa sẵn sàng?
        if not OpenXRSpatialPlaneTrackingCapability.is_supported():
            return

        # Ở đây chúng ta sẽ sử dụng plane tracking làm ví dụ; configuration object của chúng ta
        # ở đây không có cấu hình bổ sung nào. Nó chỉ cần tồn tại.
        var plane_capability : OpenXRSpatialCapabilityConfigurationPlaneTracking = OpenXRSpatialCapabilityConfigurationPlaneTracking.new()

        var future_result : OpenXRFutureResult = OpenXRSpatialEntityExtension.create_spatial_context([ plane_capability ])

        # Chờ hoàn tất thao tác async.
        await future_result.completed

        # Lấy kết quả.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với discovery signal.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện lần discovery ban đầu.
            _on_perform_discovery(spatial_context)


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Để đề phòng session của chúng ta chưa bắt đầu,
            # hãy gọi thao tác tạo spatial context khi bắt đầu.
            openxr_interface.session_begun.connect(_set_up_spatial_context)

            # Và trong trường hợp session đã hoạt động, hãy gọi nó ngay,
            # nó sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_spatial_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi discovery signal.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context; thao tác này sẽ dọn dẹp nó.
            OpenXRSpatialEntityExtension.free_spatial_context(spatial_context)
            spatial_context = RID()

        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            openxr_interface.session_begun.disconnect(_set_up_spatial_context)


    func _on_perform_discovery(p_spatial_context):
        # Xem phần tiếp theo.
        pass

Discovery snapshot
""""""""""""""""""

Sau khi spatial context được tạo, XR runtime sẽ bắt đầu quản lý các spatial entity theo cấu hình của những capability được chỉ định.

Để tìm các entity mới hoặc lấy thông tin về những entity hiện tại, chúng ta có thể tạo một discovery snapshot. Thao tác này sẽ yêu cầu XR runtime thu thập dữ liệu cụ thể liên quan đến tất cả spatial entity hiện đang được spatial context quản lý.

Hàm này là bất đồng bộ vì có thể cần chút thời gian để thu thập dữ liệu này và cung cấp kết quả. Nói chung, bạn sẽ muốn thực hiện một discovery snapshot khi tìm thấy các entity mới. OpenXR phát ra một sự kiện khi có các entity mới cần được xử lý, điều này khiến tín hiệu ``spatial_discovery_recommended`` được phát ra bởi
:ref:`OpenXRSpatialEntityExtension<class_OpenXRSpatialEntityExtension>` singleton.

Lưu ý trong đoạn mã ví dụ ở trên, chúng ta đã kết nối với tín hiệu này và gọi phương thức ``_on_perform_discovery`` trên node của mình. Hãy triển khai điều này:

.. code-block:: gdscript

    ...

    var discovery_result : OpenXRFutureResult

    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận được tín hiệu này cho tất cả spatial context, vì vậy hãy thoát nếu tín hiệu này không dành cho chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Nếu hiện tại chúng ta đang có một kết quả discovery đang diễn ra, hãy hủy nó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_PLANE_ALIGNMENT \
            ])

        # Chờ hoàn tất async.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả snapshot của chúng ta.
            _process_snapshot(snapshot)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot):
        # Xem phần bên dưới.
        pass


Lưu ý rằng khi gọi ``discover_spatial_entities``, chúng ta chỉ định một danh sách component. Discovery query sẽ tìm mọi entity được spatial context quản lý và có ít nhất một trong các component đã chỉ định.

Cập nhật snapshot
"""""""""""""""""

Thực hiện update snapshot cho phép chúng ta lấy thông tin đã cập nhật về các entity mà trước đó chúng ta đã tìm thấy bằng discovery snapshot. Hàm này là synchronous và chủ yếu dùng để lấy dữ liệu về trạng thái và vị trí, đồng thời có thể được chạy ở mỗi frame.

Nói chung, bạn chỉ thực hiện update snapshot khi có khả năng các entity thay đổi hoặc có một quy trình vòng đời. Một ví dụ điển hình là persistent anchor và marker. Hãy tham khảo tài liệu về một capability để xác định liệu việc này có cần thiết hay không.

Tuy nhiên, việc này không cần thiết đối với plane tracking. Dù vậy, để hoàn thiện ví dụ, dưới đây là ví dụ về update snapshot cho plane tracking nếu chúng ta cần:

.. code-block:: gdscript

    ...

    func _process(_delta):
        if not spatial_context:
            return

        if entities.is_empty():
            return

        var entity_rids: Array[RID]
        for entity_id in entities:
            entity_rids.push_back(entities[entity_id].entity)

        var snapshot : RID = OpenXRSpatialEntityExtension.update_spatial_entities(spatial_context, entity_rids, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_PLANE_ALIGNMENT \
            ])
        if snapshot:
            # Xử lý snapshot của chúng ta.
            _process_snapshot(snapshot)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)

Lưu ý rằng trong ví dụ này, chúng ta sử dụng cùng một hàm ``_process_snapshot`` để xử lý snapshot. Điều này hợp lý trong hầu hết tình huống. Tuy nhiên, nếu các component bạn chỉ định khi tạo snapshot khác nhau giữa discovery snapshot và update snapshot, bạn phải tính đến các component khác nhau đó.

Truy vấn snapshot
"""""""""""""""""

Sau khi có snapshot, chúng ta có thể chạy các query trên snapshot đó để lấy dữ liệu bên trong. Snapshot được đảm bảo không thay đổi cho đến khi bạn giải phóng nó.

Với mỗi component đã thêm vào snapshot, chúng ta có một data object tương ứng. Data object này có hai chức năng: thêm nó vào query sẽ đảm bảo chúng ta query đúng loại component đó, đồng thời đây cũng là object mà dữ liệu được query sẽ được nạp vào.

Có một data object đặc biệt luôn phải được thêm vào danh sách request ở vị trí đầu tiên, đó là :ref:`OpenXRSpatialQueryResultData<class_OpenXRSpatialQueryResultData>`. Object này sẽ chứa một entry cho mỗi entity được trả về, cùng với ID duy nhất và trạng thái hiện tại của entity.

Hoàn thiện logic discovery, chúng ta thêm những nội dung sau:

.. code-block:: gdscript

    ...

    var entities : Dictionary[int, OpenXRSpatialEntityTracker]

    func _process_snapshot(p_snapshot):
        # Luôn include dữ liệu kết quả query.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()

        # Thêm dữ liệu bounded 2D component.
        var bounded2d_list : OpenXRSpatialComponentBounded2DList = OpenXRSpatialComponentBounded2DList.new()

        # Và dữ liệu plane alignment component.
        var alignment_list : OpenXRSpatialComponentPlaneAlignmentList = OpenXRSpatialComponentPlaneAlignmentList.new()

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, [ query_result_data, bounded2d_list, alignment_list]):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # Trạng thái này chỉ xuất hiện khi thực hiện update snapshot
                    # và cho chúng ta biết entity này không còn được tracking.
                    # Do đó, chúng ta xóa nó khỏi dictionary, việc này sẽ khiến
                    # entity được dọn dẹp.
                    if entities.has(entity_id):
                        var entity_tracker : OpenXRSpatialEntityTracker = entities[entity_id]
                        entity_tracker.spatial_tracking_state = entity_state
                        XRServer.remove_tracker(entity_tracker)
                        entities.erase(entity_id)
                else:
                    var entity_tracker : OpenXRSpatialEntityTracker
                    var register_with_xr_server : bool = false
                    if entities.has(entity_id):
                        entity_tracker = entities[entity_id]
                    else:
                        entity_tracker = OpenXRSpatialEntityTracker.new()
                        entity_tracker.entity = OpenXRSpatialEntityExtension.make_spatial_entity(spatial_context, entity_id)
                        entities[entity_id] = entity_tracker
                        register_with_xr_server = true

                    # Sao chép trạng thái.
                    entity_tracker.spatial_tracking_state = entity_state

                    # Nếu đang tracking, chúng ta nên query các component còn lại.
                    if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_TRACKING:
                        var center_pose : Transform3D = bounded2d_list.get_center_pose(i)
                        entity_tracker.set_pose("default", center_pose, Vector3(), Vector3(), XRPose.XR_TRACKING_CONFIDENCE_HIGH)

                        # Trong ví dụ này, tôi sử dụng OpenXRSpatialEntityTracker, vốn không
                        # chứa thêm dữ liệu nào. Bạn nên mở rộng class này để lưu trữ phần
                        # trạng thái bổ sung được truy xuất. Đối với plane tracking, đó sẽ là OpenXRPlaneTracker
                        # và chúng ta có thể lưu trữ dữ liệu sau trong tracker:
                        var size : Vector2 = bounded2d_list.get_size(i)
                        var alignment = alignment_list.get_plane_alignment(i)
                    else:
                        entity_tracker.invalidate_pose("default")

                    # Chúng ta không đăng ký tracker cho đến sau khi thiết lập dữ liệu ban đầu.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

.. note::

    Trong ví dụ trên, chúng ta dựa vào ``ENTITY_TRACKING_STATE_STOPPED`` để dọn dẹp các spatial entity không còn được tracking. Tính năng này chỉ khả dụng với update snapshot.

    Đối với các capability chỉ dựa vào discovery snapshot, bạn có thể muốn thực hiện việc dọn dẹp dựa trên các entity không còn thuộc snapshot, thay vì dựa vào thay đổi trạng thái.

Spatial entity
""""""""""""""

Với các thông tin trên, giờ chúng ta đã biết cách query spatial entity và lấy thông tin về chúng, nhưng vẫn còn một số điều cần xem xét liên quan đến bản thân các entity.

Về lý thuyết, chúng ta lấy toàn bộ dữ liệu từ snapshot. Tuy nhiên, OpenXR có thêm một API cho phép chúng ta tạo spatial entity object từ entity ID. Khi object này tồn tại, XR runtime biết rằng chúng ta đang sử dụng entity này và entity đó sẽ không bị dọn dẹp sớm. Đây là điều kiện tiên quyết để thực hiện update query trên entity này.

Trong mã ví dụ, chúng ta thực hiện việc này bằng cách gọi ``OpenXRSpatialEntityExtension.make_spatial_entity``.

Một số spatial entity API sẽ tự động tạo object cho chúng ta. Trong trường hợp này, chúng ta cần gọi ``OpenXRSpatialEntityExtension.add_spatial_entity`` để đăng ký object đã tạo với implementation của mình.

Cả hai hàm đều trả về một RID mà chúng ta có thể sử dụng trong các hàm tiếp theo yêu cầu entity object.

Khi hoàn tất, chúng ta có thể gọi ``OpenXRSpatialEntityExtension.free_spatial_entity``.

Lưu ý rằng chúng ta không làm vậy trong mã ví dụ. Việc này được tự động xử lý khi
:ref:`OpenXRSpatialEntityTracker<class_OpenXRSpatialEntityTracker>` instance is destroyed.

Spatial anchor capability
~~~~~~~~~~~~~~~~~~~~~~~~~

Spatial anchor được quản lý bởi singleton object :ref:`OpenXRSpatialAnchorCapability<class_OpenXRSpatialAnchorCapability>` của chúng ta. Sau khi OpenXR session được tạo, bạn có thể gọi ``OpenXRSpatialAnchorCapability.is_spatial_anchor_supported`` để kiểm tra xem tính năng spatial anchor có được phần cứng của bạn hỗ trợ hay không.

Spatial anchor capability có một số điểm khác với những gì chúng ta đã trình bày ở trên.

Hệ thống spatial anchor cho phép chúng ta xác định, tracking, persist và chia sẻ một vị trí vật lý. Điểm khác biệt là chúng ta tạo và hủy anchor, do đó quản lý vòng đời của anchor.

Vì vậy, chúng ta chỉ sử dụng discovery system để phát hiện các anchor được tạo và persist trong những session trước, hoặc các anchor được chia sẻ với chúng ta.

.. note::

    Hiện tại, việc chia sẻ anchor chưa được hỗ trợ trong spatial entities specification.

Như đã trình bày trong ví dụ trước, chúng ta luôn bắt đầu bằng việc tạo spatial context, nhưng lần này sử dụng
:ref:`OpenXRSpatialCapabilityConfigurationAnchor<class_OpenXRSpatialCapabilityConfigurationAnchor>`
configuration object. Chúng ta sẽ trình bày ví dụ về đoạn mã này sau khi thảo luận về persistence scope. Trước tiên, hãy xem cách quản lý local anchor.

Việc tạo spatial anchor không khác với logic tích hợp sẵn mà chúng ta đã thảo luận. Điều quan trọng duy nhất là truyền spatial context của bạn làm tham số cho ``OpenXRSpatialAnchorCapability.create_new_anchor``.

Để persist một anchor, bạn cần chờ cho đến khi anchor đang tracking. Điều này có nghĩa là bạn phải thực hiện update query cho mọi anchor được tạo để có thể xử lý các thay đổi trạng thái.

Để bật khả năng persist anchor, bạn cũng phải thiết lập persistence scope. Trong phần core của OpenXR, hai loại persistence scope được hỗ trợ:

.. list-table:: Persistence scopes
   :header-rows: 1

   * - Enum
     - Mô tả
   * - PERSISTENCE_SCOPE_SYSTEM_MANAGED
     - Cung cấp cho application quyền truy cập chỉ đọc (tức là application không thể sửa đổi store này)
       đối với các spatial entity được system persist và quản lý.
       Application có thể sử dụng UUID trong persistence component của store này để đối chiếu
       các entity giữa các spatial context và những lần khởi động lại thiết bị.
   * - PERSISTENCE_SCOPE_LOCAL_ANCHORS
     - Các thao tác persistence và quyền truy cập dữ liệu chỉ giới hạn ở spatial anchor, trên cùng một thiết bị,
       đối với cùng một user và app (sử dụng `persist_anchor` và
       các hàm `unpersist_anchor`)

Chúng ta sẽ bắt đầu với một script mới để xử lý spatial anchor. Script này sẽ tương tự script được trình bày trước đó nhưng có một vài điểm khác biệt.

Điểm khác biệt đầu tiên là việc tạo persistence scope.

.. code-block:: gdscript

    extends Node

    var persistence_context : RID

    func _set_up_persistence_context():
        # Đã được thiết lập?
        if persistence_context:
            # Kiểm tra spatial context của chúng ta.
            _set_up_spatial_context()
            return

        # Không được hỗ trợ hoặc chúng ta chưa sẵn sàng? Hãy thoát.
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            return

        # Nếu không thể sử dụng persistence scope, chỉ cần tạo spatial context mà không có scope.
        if not OpenXRSpatialAnchorCapability.is_spatial_persistence_supported():
            _set_up_spatial_context()
            return

        var scope : int = 0
        if OpenXRSpatialAnchorCapability.is_persistence_scope_supported(OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_LOCAL_ANCHORS):
            scope = OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_LOCAL_ANCHORS
        elif OpenXRSpatialAnchorCapability.is_persistence_scope_supported(OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_SYSTEM_MANAGED):
            scope = OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_SYSTEM_MANAGED
        else:
            # Không có persistence scope đã biết, hãy báo cáo và thiết lập mà không có scope đó.
            push_error("No known persistence scope is supported.")
            _set_up_spatial_context()
            return

        # Tạo persistence scope của chúng ta.
        var future_result : OpenXRFutureResult = OpenXRSpatialAnchorCapability.create_persistence_context(scope)
        if not future:
            # Không thể tạo persistence scope? Hãy thiết lập mà không có scope đó.
            _set_up_spatial_context()
            return

        # Bây giờ chờ process của chúng ta hoàn tất.
        await future_result.completed

        # Lấy kết quả của chúng ta.
        persistence_context = future_result.get_result()
        if persistence_context:
            # Bây giờ thiết lập spatial context của chúng ta.
            _set_up_spatial_context()


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Để đề phòng session của chúng ta chưa bắt đầu,
            # hãy gọi việc tạo context khi bắt đầu, bắt đầu bằng persistence scope của chúng ta.
            openxr_interface.session_begun.connect(_set_up_persistence_context)

            # Và trong trường hợp nó đã hoạt động, hãy gọi nó ngay,
            # nó sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_persistence_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi discovery signal của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context của chúng ta; việc này sẽ dọn dẹp nó.
            OpenXRSpatialEntityExtension.free_spatial_context(spatial_context)
            spatial_context = RID()

        if persistence_context:
            # Giải phóng persistence context của chúng ta...
            OpenXRSpatialAnchorCapability.free_persistence_context(persistence_context)
            persistence_context = RID()

        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            openxr_interface.session_begun.disconnect(_set_up_persistence_context)

Sau khi đã tạo persistence scope, giờ chúng ta có thể tạo spatial context.

.. code-block:: gdscript

    ...

    var spatial_context: RID

    func _set_up_spatial_context():
        # Đã được thiết lập?
        if spatial_context:
            return

        # Không được hỗ trợ hoặc chúng ta chưa thiết lập xong.
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            return

        # Tạo anchor capability của chúng ta.
        var anchor_capability : OpenXRSpatialCapabilityConfigurationAnchor = OpenXRSpatialCapabilityConfigurationAnchor.new()

        # Và thiết lập persistence configuration object (nếu cần).
        var persistence_config : OpenXRSpatialContextPersistenceConfig
        if persistence_context:
            persistence_config = OpenXRSpatialContextPersistenceConfig.new()
            persistence_config.add_persistence_context(persistence_context)

        var future_result : OpenXRFutureResultg = OpenXRSpatialEntityExtension.create_spatial_context([ anchor_capability ], persistence_config)

        # Chờ hoàn tất async.
        await future_result.completed

        # Nhận kết quả của chúng ta.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với signal discovery của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện discovery ban đầu của chúng ta.
            _on_perform_discovery(spatial_context)


Việc tạo snapshot discovery cho các anchor của chúng ta gần như giống hệt những gì đã làm trước đây, tuy nhiên chỉ hợp lý khi tạo snapshot cho các anchor persistent. Chúng ta đã biết các anchor được tạo trong session, nên chỉ cần truy cập những anchor đến từ XR runtime.

Chúng ta cũng muốn thực hiện các truy vấn cập nhật định kỳ; ở đây chúng ta chỉ quan tâm đến state, vì vậy cần xử lý snapshot hơi khác một chút.

Hệ thống anchor cho phép chúng ta truy cập hai component:

.. list-table:: Anchor components
   :header-rows: 1

   * - Component
     - Data class
     - Mô tả
   * - COMPONENT_TYPE_ANCHOR
     - :ref:`OpenXRSpatialComponentAnchorList<class_OpenXRSpatialComponentAnchorList>`
     - Cung cấp pose (vị trí + hướng) của mỗi anchor
   * - COMPONENT_TYPE_PERSISTENCE
     - :ref:`OpenXRSpatialComponentPersistenceList<class_OpenXRSpatialComponentPersistenceList>`
     - Cung cấp persistence state và UUID của mỗi anchor

.. code-block:: gdscript

    ...

    var discovery_result : OpenXRFutureResult
    var entities : Dictionary[int, OpenXRAnchorTracker]

    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận signal này cho tất cả spatial context, vì vậy hãy thoát nếu đây không phải spatial context của chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Bỏ qua bước này nếu chúng ta không có persistence context.
        if not persistence_context:
            return

        # Nếu hiện đang có một discovery result đang hoạt động, hãy hủy nó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery của chúng ta.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_ANCHOR, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_PERSISTENCE \
            ])

        # Chờ async hoàn tất.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả snapshot của chúng ta.
            _process_snapshot(snapshot, true)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process(_delta):
        if not spatial_context:
            return

        if entities.is_empty():
            return

        var entity_rids: Array[RID]
        for entity_id in entities:
            entity_rids.push_back(entities[entity_id].entity)

        # Ở đây chúng ta chỉ cần anchor component.
        var snapshot : RID = OpenXRSpatialEntityExtension.update_spatial_entities(spatial_context, entity_rids, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_ANCHOR, \
            ])
        if snapshot:
            # Xử lý snapshot của chúng ta.
            _process_snapshot(snapshot)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot, p_get_uuids):
        pass


Cuối cùng, chúng ta có thể xử lý snapshot. Lưu ý rằng chúng ta sử dụng :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>` làm tracker class, vì class này đã tích hợp sẵn toàn bộ hỗ trợ cho anchor.

.. code-block:: gdscript

    ...

    func _process_snapshot(p_snapshot, p_get_uuids):
        var result_data : Array

        # Luôn bao gồm dữ liệu query result của chúng ta.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()
        result_data.push_back(query_result_data)

        # Thêm dữ liệu anchor component của chúng ta.
        var anchor_list : OpenXRSpatialComponentAnchorList = OpenXRSpatialComponentAnchorList.new()
        result_data.push_back(anchor_list)

        # Và dữ liệu persistent component của chúng ta.
        var persistent_list : OpenXRSpatialComponentPersistenceList
        if p_get_uuids:
            # Chỉ thêm dữ liệu này khi cần.
            persistent_list = OpenXRSpatialComponentPersistenceList.new()
            result_data.push_back(persistent_list)

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, result_data):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # State này chỉ xuất hiện khi thực hiện update snapshot
                    # và cho biết entity này không còn được tracking.
                    # Do đó, chúng ta xóa nó khỏi dictionary, việc này sẽ khiến
                    # entity được dọn dẹp.
                    if entities.has(entity_id):
                        var entity_tracker : OpenXRAnchorTracker = entities[entity_id]
                        entity_tracker.spatial_tracking_state = entity_state
                        XRServer.remove_tracker(entity_tracker)
                        entities.erase(entity_id)
                else:
                    var entity_tracker : OpenXRAnchorTracker
                    var register_with_xr_server : bool = false
                    if entities.has(entity_id):
                        entity_tracker = entities[entity_id]
                    else:
                        entity_tracker = OpenXRAnchorTracker.new()
                        entity_tracker.entity = OpenXRSpatialEntityExtension.make_spatial_entity(spatial_context, entity_id)
                        entities[entity_id] = entity_tracker
                        register_with_xr_server = true

                    # Sao chép state.
                    entity_tracker.spatial_tracking_state = entity_state

                    # Nếu đang tracking, chúng ta cập nhật vị trí.
                    if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_TRACKING:
                        var anchor_transform = anchor_list.get_entity_pose(i)
                        entity_tracker.set_pose("default", anchor_transform, Vector3(), Vector3(), XRPose.XR_TRACKING_CONFIDENCE_HIGH)
                    else:
                        entity_tracker.invalidate_pose("default")

                    # Tuy nhiên, persistence data là một ngoại lệ lớn: nó có thể được cung cấp ngay cả khi chúng ta không tracking.
                    if p_get_uuids:
                        var persistent_state = persistent_list.get_persistent_state(i)
                        if persistent_state == 1:
                            entity_tracker.uuid = persistent_list.get_persistent_uuid(i)

                    # Chúng ta không register tracker cho đến sau khi đã thiết lập initial data.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

Khả năng plane tracking
~~~~~~~~~~~~~~~~~~~~~~~

Plane tracking được xử lý bởi
:ref:`OpenXRSpatialPlaneTrackingCapability<class_OpenXRSpatialPlaneTrackingCapability>`
singleton class.

Sau khi OpenXR session được tạo, bạn có thể gọi ``OpenXRSpatialPlaneTrackingCapability.is_supported`` để kiểm tra xem tính năng plane tracking có được hỗ trợ trên phần cứng của bạn hay không.

Mặc dù phần lớn code cho plane tracking đã được cung cấp ở trên, chúng ta sẽ trình bày implementation đầy đủ bên dưới vì có một vài điều chỉnh nhỏ. Ở đây không cần cập nhật snapshot; chúng ta chỉ thực hiện discovery snapshot và triển khai hàm process.

Plane tracking cho phép truy cập hai component bắt buộc được hỗ trợ và ba component tùy chọn.

.. list-table:: Plane tracking components
   :header-rows: 1

   * - Component
     - Data class
     - Mô tả
   * - COMPONENT_TYPE_BOUNDED_2D
     - :ref:`OpenXRSpatialComponentBounded2DList<class_OpenXRSpatialComponentBounded2DList>`
     - Cung cấp center pose và bounding rectangle của mỗi plane.
   * - COMPONENT_TYPE_PLANE_ALIGNMENT
     - :ref:`OpenXRSpatialComponentPlaneAlignmentList<class_OpenXRSpatialComponentPlaneAlignmentList>`
     - Cung cấp alignment của mỗi plane
   * - COMPONENT_TYPE_MESH_2D
     - :ref:`OpenXRSpatialComponentMesh2DList<class_OpenXRSpatialComponentMesh2DList>`
     - Cung cấp mesh 2D tạo hình cho mỗi plane
   * - COMPONENT_TYPE_POLYGON_2D
     - :ref:`OpenXRSpatialComponentPolygon2DList<class_OpenXRSpatialComponentPolygon2DList>`
     - Cung cấp polygon 2D tạo hình cho mỗi plane
   * - COMPONENT_TYPE_PLANE_SEMANTIC_LABEL
     - :ref:`OpenXRSpatialComponentPlaneSemanticLabelList<class_OpenXRSpatialComponentPlaneSemanticLabelList>`
     - Cung cấp type identification của mỗi plane

Configuration object cho plane tracking đã bật tất cả component được hỗ trợ, nhưng chúng ta sẽ cần truy vấn nó, nên sẽ lưu instance vào một member variable. Chúng ta có thể sử dụng tracker object :ref:`OpenXRPlaneTracker<class_OpenXRPlaneTracker>` để lưu component data.

.. code-block:: gdscript

    extends Node

    var plane_capability : OpenXRSpatialCapabilityConfigurationPlaneTracking
    var spatial_context: RID
    var discovery_result : OpenXRFutureResult
    var entities : Dictionary[int, OpenXRPlaneTracker]

    func _set_up_spatial_context():
        # Đã được thiết lập?
        if spatial_context:
            return

        # Không được hỗ trợ hoặc chúng ta chưa sẵn sàng?
        if not OpenXRSpatialPlaneTrackingCapability.is_supported():
            return

        # Ở đây chúng ta sẽ dùng plane tracking làm ví dụ; configuration object của chúng ta
        # không có configuration bổ sung nào. Nó chỉ cần tồn tại.
        plane_capability = OpenXRSpatialCapabilityConfigurationPlaneTracking.new()

        var future_result : OpenXRFutureResult = OpenXRSpatialEntityExtension.create_spatial_context([ plane_capability ])

        # Chờ async hoàn tất.
        await future_result.completed

        # Nhận kết quả của chúng ta.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với signal discovery của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện discovery ban đầu của chúng ta.
            _on_perform_discovery(spatial_context)


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Đề phòng session của chúng ta chưa bắt đầu,
            # hãy gọi thao tác tạo spatial context khi bắt đầu.
            openxr_interface.session_begun.connect(_set_up_spatial_context)

            # Và nếu nó đã hoạt động, hãy gọi ngay,
            # nó sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_spatial_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi signal discovery của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context của chúng ta; thao tác này sẽ dọn dẹp nó.
            OpenXRSpatialEntityExtension.free_spatial_context(spatial_context)
            spatial_context = RID()

        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            openxr_interface.session_begun.disconnect(_set_up_spatial_context)


    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận signal này cho tất cả spatial context, vì vậy hãy thoát nếu đây không phải spatial context của chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Nếu hiện đang có một discovery result đang hoạt động, hãy hủy nó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery của chúng ta.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, \
                plane_capability.get_enabled_components())

        # Chờ async hoàn tất.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả snapshot của chúng ta.
            _process_snapshot(snapshot)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot):
        var result_data : Array

        # Tạo một bản sao của các entity mà chúng ta hiện đã tìm thấy.
        var org_entities : PackedInt64Array
        for entity_id in entities:
            org_entities.push_back(entity_id)

        # Luôn bao gồm dữ liệu query result của chúng ta.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()
        result_data.push_back(query_result_data)

        # Thêm dữ liệu bounded 2D component của chúng ta.
        var bounded2d_list : OpenXRSpatialComponentBounded2DList = OpenXRSpatialComponentBounded2DList.new()
        result_data.push_back(bounded2d_list)

        # Và dữ liệu plane alignment component của chúng ta.
        var alignment_list : OpenXRSpatialComponentPlaneAlignmentList = OpenXRSpatialComponentPlaneAlignmentList.new()
        result_data.push_back(alignment_list)

        # Chúng ta cần Mesh2D hoặc Polygon2D, không cần cả hai.
        var mesh2d_list : OpenXRSpatialComponentMesh2DList
        var polygon2d_list : OpenXRSpatialComponentPolygon2DList
        if plane_capability.get_supports_mesh_2d():
            mesh2d_list = OpenXRSpatialComponentMesh2DList.new()
            result_data.push_back(mesh2d_list)
        elif plane_capability.get_supports_polygons():
            polygon2d_list = OpenXRSpatialComponentPolygon2DList.new()
            result_data.push_back(polygon2d_list)

        # Và thêm semantic label nếu được hỗ trợ.
        var label_list : OpenXRSpatialComponentPlaneSemanticLabelList
        if plane_capability.get_supports_labels():
            label_list = OpenXRSpatialComponentPlaneSemanticLabelList.new()
            result_data.push_back(label_list)

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, result_data):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                # Xóa entity khỏi danh sách ban đầu của chúng ta.
                if org_entities.has(entity_id):
                    org_entities.erase(entity_id)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # Chúng ta không thực hiện update snapshot, nên sẽ không nhận được state này,
                    # nhưng để đảm bảo tương thích trong tương lai:
                    if entities.has(entity_id):
                        var entity_tracker : OpenXRPlaneTracker = entities[entity_id]
                        entity_tracker.spatial_tracking_state = entity_state
                        XRServer.remove_tracker(entity_tracker)
                        entities.erase(entity_id)
                else:
                    var entity_tracker : OpenXRPlaneTracker
                    var register_with_xr_server : bool = false
                    if entities.has(entity_id):
                        entity_tracker = entities[entity_id]
                    else:
                        entity_tracker = OpenXRPlaneTracker.new()
                        entity_tracker.entity = OpenXRSpatialEntityExtension.make_spatial_entity(spatial_context, entity_id)
                        entities[entity_id] = entity_tracker
                        register_with_xr_server = true

                    # Sao chép state.
                    entity_tracker.spatial_tracking_state = entity_state

                    # Nếu đang tracking, chúng ta nên truy vấn các component còn lại.
                    if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_TRACKING:
                        var center_pose : Transform3D = bounded2d_list.get_center_pose(i)
                        entity_tracker.set_pose("default", center_pose, Vector3(), Vector3(), XRPose.XR_TRACKING_CONFIDENCE_HIGH)

                        entity_tracker.bounds_size = bounded2d_list.get_size(i)
                        entity_tracker.plane_alignment = alignment_list.get_plane_alignment(i)

                        if mesh2d_list:
                            entity_tracker.set_mesh_data( \
                                    mesh2d_list.get_transform(i), \
                                    mesh2d_list.get_vertices(p_snapshot, i), \
                                    mesh2d_list.get_indices(p_snapshot, i))
                        elif polygon2d_list:
                            # Logic trong tracker sẽ chuyển polygon thành mesh.
                            entity_tracker.set_mesh_data( \
                                    polygon2d_list.get_transform(i), \
                                    polygon2d_list.get_vertices(p_snapshot, i))
                        else:
                            entity_tracker.clear_mesh_data()

                        if label_list:
                            entity_tracker.plane_label = label_list.get_plane_semantic_label(i)
                    else:
                        entity_tracker.invalidate_pose("default")

                    # Chúng ta không register tracker cho đến sau khi đã thiết lập initial data.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

        # Chúng ta có thể xóa mọi entity còn lại.
        for entity_id in org_entities:
            var entity_tracker : OpenXRPlaneTracker = entities[entity_id]
            entity_tracker.spatial_tracking_state = OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED
            XRServer.remove_tracker(entity_tracker)
            entities.erase(entity_id)


Khả năng marker tracking
~~~~~~~~~~~~~~~~~~~~~~~~

Marker tracking được xử lý bởi
:ref:`OpenXRSpatialMarkerTrackingCapability<class_OpenXRSpatialMarkerTrackingCapability>`
singleton class.

Marker tracking hoạt động tương tự plane tracking, tuy nhiên lúc này chúng ta tracking các entity cụ thể trong thế giới thực dựa trên một đoạn code được in trên một vật thể, chẳng hạn như một tờ giấy.

Có nhiều tùy chọn marker tracking khác nhau. OpenXR hỗ trợ sẵn 4 tùy chọn; bảng sau cung cấp thêm thông tin và tên function dùng để kiểm tra xem headset của bạn có hỗ trợ một tùy chọn cụ thể hay không:

.. list-table:: Marker tracking options
   :header-rows: 1

   * - Tùy chọn
     - Kiểm tra hỗ trợ
     - Configuration object
   * - April tag
     - ``april_tag_is_supported``
     - :ref:`OpenXRSpatialCapabilityConfigurationAprilTag<class_OpenXRSpatialCapabilityConfigurationAprilTag>`
   * - Aruco
     - ``aruco_is_supported``
     - :ref:`OpenXRSpatialCapabilityConfigurationAruco<class_OpenXRSpatialCapabilityConfigurationAruco>`
   * - QR code
     - ``qrcode_is_supported``
     - :ref:`OpenXRSpatialCapabilityConfigurationQrCode<class_OpenXRSpatialCapabilityConfigurationQrCode>`
   * - Micro QR code
     - ``micro_qrcode_is_supported``
     - :ref:`OpenXRSpatialCapabilityConfigurationMicroQrCode<class_OpenXRSpatialCapabilityConfigurationMicroQrCode>`

Mỗi tùy chọn có configuration object riêng mà bạn có thể sử dụng khi tạo spatial entity.

QR code cho phép encode một string, sau đó được XR runtime decode và có thể truy cập khi tìm thấy marker. Với April tag và Aruco marker, binary data được encode; bạn cũng có thể truy cập dữ liệu này khi tìm thấy marker, tuy nhiên cần cấu hình detection với decoding format chính xác.

Ví dụ, chúng ta sẽ tạo một spatial context để tìm QR code và Aruco marker.

.. code-block:: gdscript

    extends Node

    var qrcode_config : OpenXRSpatialCapabilityConfigurationQrCode
    var aruco_config : OpenXRSpatialCapabilityConfigurationAruco
    var spatial_context: RID

    func _set_up_spatial_context():
        # Đã được thiết lập?
        if spatial_context:
            return

        var configurations : Array

        # Thêm QR code configuration của chúng ta.
        if not OpenXRSpatialMarkerTrackingCapability.qrcode_is_supported():
            qrcode_config = OpenXRSpatialCapabilityConfigurationQrCode.new()
            configurations.push_back(qrcode_config)

        # Thêm Aruco marker configuration của chúng ta.
        if not OpenXRSpatialMarkerTrackingCapability.aruco_is_supported():
            aruco_config = OpenXRSpatialCapabilityConfigurationAruco.new()
            aruco_config.aruco_dict = OpenXRSpatialCapabilityConfigurationAruco.ARUCO_DICT_7X7_1000
            configurations.push_back(aruco_config)

        # Không được hỗ trợ?
        if configurations.is_empty():
            return

        var future_result : OpenXRFutureResult = OpenXRSpatialEntityExtension.create_spatial_context(configurations)

        # Chờ async hoàn tất.
        await future_result.completed

        # Nhận kết quả của chúng ta.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với signal discovery của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện discovery ban đầu của chúng ta.
            _on_perform_discovery(spatial_context)


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Đề phòng session của chúng ta chưa bắt đầu,
            # hãy gọi thao tác tạo spatial context khi bắt đầu.
            openxr_interface.session_begun.connect(_set_up_spatial_context)

            # Và nếu nó đã hoạt động, hãy gọi ngay,
            # nó sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_spatial_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi signal discovery của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context của chúng ta; thao tác này sẽ dọn dẹp nó.
            OpenXRSpatialEntityExtension.free_spatial_context(spatial_context)
            spatial_context = RID()

        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            openxr_interface.session_begun.disconnect(_set_up_spatial_context)


Mỗi marker, bất kể type nào, sẽ gồm hai component:

.. list-table:: Marker tracking components
   :header-rows: 1

   * - Component
     - Data class
     - Mô tả
   * - COMPONENT_TYPE_MARKER
     - :ref:`OpenXRSpatialComponentMarkerList<class_OpenXRSpatialComponentMarkerList>`
     - Cung cấp type, ID (Aruco và April Tag) và/hoặc data (QR Code) của mỗi marker.
   * - COMPONENT_TYPE_BOUNDED_2D
     - :ref:`OpenXRSpatialComponentBounded2DList<class_OpenXRSpatialComponentBounded2DList>`
     - Cung cấp center pose và bounding rectangle của mỗi plane.

Chúng ta thêm implementation cho discovery:

.. code-block:: gdscript

    ...

    var discovery_result : OpenXRFutureResult
    var entities : Dictionary[int, OpenXRMarkerTracker]

    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận signal này cho tất cả spatial context, vì vậy hãy thoát nếu đây không phải spatial context của chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Nếu hiện đang có một discovery result đang hoạt động, hãy hủy nó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery của chúng ta.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, [\
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_MARKER, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D \
            ])

        # Chờ tác vụ bất đồng bộ hoàn tất.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả snapshot của chúng ta.
            _process_snapshot(snapshot, true)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot, bool p_is_discovery):
        var result_data : Array

        # Tạo một bản sao của các thực thể mà hiện tại chúng ta đã tìm thấy.
        var org_entities : PackedInt64Array
        if p_is_discovery:
            # Chỉ trong discovery, chúng ta mới kiểm tra xem có thực thể chưa được theo dõi nào cần dọn dẹp hay không.
            for entity_id in entities:
                org_entities.push_back(entity_id)

        # Luôn bao gồm dữ liệu kết quả truy vấn của chúng ta.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()
        result_data.push_back(query_result_data)

        # Và dữ liệu marker component của chúng ta.
        var marker_list : OpenXRSpatialComponentMarkerList
        if p_is_discovery:
            # Chỉ trong discovery, chúng ta mới kiểm tra dữ liệu marker của mình
            marker_list = OpenXRSpatialComponentMarkerList.new()
            result_data.push_back(marker_list)

        # Thêm dữ liệu bounded 2D component của chúng ta.
        var bounded2d_list : OpenXRSpatialComponentBounded2DList = OpenXRSpatialComponentBounded2DList.new()
        result_data.push_back(bounded2d_list)

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, result_data):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                # Xóa thực thể khỏi danh sách ban đầu của chúng ta.
                if org_entities.has(entity_id):
                    org_entities.erase(entity_id)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # Chúng ta chỉ nhận được điều này khi thực hiện một bản cập nhật,
                    # và trong trường hợp đó, chúng ta sẽ xóa marker của mình.
                    if entities.has(entity_id):
                        var entity_tracker : OpenXRMarkerTracker = entities[entity_id]
                        entity_tracker.spatial_tracking_state = entity_state
                        XRServer.remove_tracker(entity_tracker)
                        entities.erase(entity_id)
                else:
                    var entity_tracker : OpenXRMarkerTracker
                    var register_with_xr_server : bool = false
                    if entities.has(entity_id):
                        entity_tracker = entities[entity_id]
                    else:
                        entity_tracker = OpenXRMarkerTracker.new()
                        entity_tracker.entity = OpenXRSpatialEntityExtension.make_spatial_entity(spatial_context, entity_id)
                        entities[entity_id] = entity_tracker
                        register_with_xr_server = true

                    # Sao chép state.
                    entity_tracker.spatial_tracking_state = entity_state

                    # Nếu đang theo dõi, chúng ta nên truy vấn các component còn lại.
                    if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_TRACKING:
                        var center_pose : Transform3D = bounded2d_list.get_center_pose(i)
                        entity_tracker.set_pose("default", center_pose, Vector3(), Vector3(), XRPose.XR_TRACKING_CONFIDENCE_HIGH)

                        entity_tracker.bounds_size = bounded2d_list.get_size(i)

                        if p_is_discovery:
                            entity_tracker.marker_type = marker_list.get_marker_type(i)
                            entity_tracker.marker_id = marker_list.get_marker_id(i)
                            entity_tracker.marker_data = marker_list.get_marker_data(p_snapshot, i)
                    else:
                        entity_tracker.invalidate_pose("default")

                    # Chúng ta không đăng ký tracker cho đến khi thiết lập dữ liệu ban đầu.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

        if p_is_discovery:
            # Chúng ta có thể xóa mọi thực thể còn sót lại.
            for entity_id in org_entities:
                var entity_tracker : OpenXRMarkerTracker = entities[entity_id]
                entity_tracker.spatial_tracking_state = OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED
                XRServer.remove_tracker(entity_tracker)
                entities.erase(entity_id)

Và chúng ta thêm chức năng update:

.. code-block:: gdscript

    ...


    func _process(_delta):
        if not spatial_context:
            return

        if entities.is_empty():
            return

        var entity_rids: Array[RID]
        for entity_id in entities:
            entity_rids.push_back(entities[entity_id].entity)

        # Ở đây, chúng ta chỉ cần anchor component.
        var snapshot : RID = OpenXRSpatialEntityExtension.update_spatial_entities(spatial_context, entity_rids, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D, \
            ])
        if snapshot:
            # Xử lý snapshot của chúng ta.
            _process_snapshot(snapshot, false)

            # Và dọn dẹp snapshot của chúng ta.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)
