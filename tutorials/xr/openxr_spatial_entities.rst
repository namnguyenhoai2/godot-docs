.. _doc_openxr_spatial_entities:

Các thực thể không gian của OpenXR
==================================

Đối với mọi loại ứng dụng thực tế tăng cường, bạn cần truy cập thông tin về thế giới thực và có khả năng theo dõi các vị trí trong thế giới thực. API thực thể không gian của OpenXR được giới thiệu chính xác nhằm mục đích này.

API này có thiết kế rất mô-đun. Phần lõi của API xác định cách các thực thể trong thế giới thực được cấu trúc, cách tìm thấy chúng cũng như cách thông tin về chúng được lưu trữ và truy cập.

Nhiều extension khác nhau được bổ sung bên trên để triển khai các hệ thống cụ thể như theo dõi marker, theo dõi mặt phẳng và anchor. Chúng được gọi là các spatial capability.

Mỗi thực thể có thể được hệ thống xử lý đều được chia thành các component nhỏ hơn, giúp dễ dàng mở rộng hệ thống và bổ sung các capability mới.

Các nhà cung cấp có thể triển khai và cung cấp thêm các capability và component type có thể được sử dụng với core API. Trong Godot, những thành phần này có thể được triển khai trong các extension. Tuy nhiên, những triển khai này nằm ngoài phạm vi của tài liệu hướng dẫn này.

Cuối cùng, điều quan trọng cần lưu ý là hệ thống thực thể không gian sử dụng các hàm bất đồng bộ (asynchronous function). Điều này có nghĩa là bạn có thể bắt đầu một quy trình rồi nhận được thông báo khi quy trình đó hoàn tất sau đó.

Thiết lập
---------

Để sử dụng các thực thể không gian, bạn cần bật các project settings liên quan. Bạn có thể tìm thấy chúng trong phần OpenXR:

.. image:: img/openxr_spatial_entities_project_settings.webp

.. list-table:: Cài đặt thực thể không gian
   :header-rows: 1

   * - Setting
     - Description
   * - Enabled
     - Bật phần lõi của hệ thống thực thể không gian. Tùy chọn này phải được bật để bất kỳ hệ thống thực thể không gian nào hoạt động.
   * - Enable spatial anchors
     - Bật spatial capability cho phép tạo và theo dõi các spatial anchor.
   * - Enable persistent anchors
     - Bật khả năng duy trì các spatial anchor. Điều này có nghĩa là vị trí của chúng được lưu trữ và có thể được truy xuất trong các session tiếp theo.
   * - Enable built-in anchor detection
     - Bật logic phát hiện anchor tích hợp sẵn của chúng tôi. Logic này sẽ tự động truy xuất các persistent anchor và điều chỉnh vị trí của anchor khi thông tin theo dõi được cập nhật.
   * - Enable plane tracking
     - Bật spatial capability theo dõi mặt phẳng, cho phép phát hiện các bề mặt như sàn, tường, trần nhà và bàn.
   * - Enable built-in plane detection
     - Bật logic phát hiện mặt phẳng tích hợp sẵn của chúng tôi. Logic này sẽ tự động phản hồi khi dữ liệu mặt phẳng mới khả dụng.
   * - Enable marker tracking
     - Bật capability theo dõi marker, cho phép phát hiện các marker như mã QR, marker Aruco và April tag.
   * - Enable built-in marker tracking
     - Bật logic phát hiện marker tích hợp sẵn của chúng tôi. Logic này sẽ tự động phản hồi khi tìm thấy marker mới hoặc khi marker được di chuyển trong không gian của người chơi.

.. note::

    Lưu ý rằng nhiều thiết bị XR cũng yêu cầu thiết lập các cờ quyền. Bạn cần bật những cờ này trong cài đặt export preset.

Việc bật các capability khác nhau sẽ kích hoạt các OpenXR API liên quan, nhưng cần thêm logic để tương tác với dữ liệu này. Đối với mỗi hệ thống lõi, chúng tôi có logic tích hợp sẵn mà bạn có thể bật để thực hiện việc này.

Chúng ta sẽ thảo luận về hệ thống thực thể không gian với giả định rằng trước tiên logic tích hợp sẵn đã được bật. Sau đó, chúng ta sẽ xem xét các API nền tảng và cách bạn có thể tự triển khai chúng. Tuy nhiên, cần lưu ý rằng việc này thường là quá mức cần thiết và các API nền tảng chủ yếu được cung cấp để các plugin GDExtension triển khai thêm capability.

Tạo spatial manager
-------------------

Khi các thực thể không gian được phát hiện hoặc tạo, một
:ref:`OpenXRSpatialEntityTracker<class_OpenXRSpatialEntityTracker>` object được khởi tạo và đăng ký với :ref:`XRServer<class_XRServer>`.

Mỗi loại thực thể không gian sẽ triển khai subclass riêng, vì vậy chúng ta có thể phản hồi khác nhau với từng loại thực thể.

Nói chung, chúng ta sẽ instance các subscene khác nhau cho từng loại thực thể. Vì các tracker object có thể được sử dụng với các node :ref:`XRAnchor3D<class_XRAnchor3D>`, những subscene này nên có một node như vậy làm root node.

Tất cả entity tracker sẽ cung cấp vị trí của chúng thông qua pose ``default``.

Chúng ta có thể tự động tạo các subscene này và thêm chúng vào scene tree bằng cách tạo một manager object. Vì tất cả vị trí đều là local so với node :ref:`XROrigin3D<class_XROrigin3D>`, chúng ta nên tạo manager dưới dạng child node của origin node.

Dưới đây là phần cơ bản của script triển khai logic manager:

.. code-block:: gdscript

    class_name SpatialEntitiesManager
    extends Node3D

    ## Phát tín hiệu khi một node thực thể không gian mới được thêm vào.
    signal added_spatial_entity(node: XRNode3D)

    ## Phát tín hiệu khi một node thực thể không gian sắp bị xóa.
    signal removed_spatial_entity(node: XRNode3D)

    ## Scene sẽ được instance cho các thực thể spatial anchor.
    @export var spatial_anchor_scene: PackedScene

    ## Scene sẽ được instance cho các thực thể không gian theo dõi mặt phẳng.
    @export var plane_tracker_scene: PackedScene

    ## Scene sẽ được instance cho các thực thể không gian theo dõi marker.
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
        # Dọn dẹp các signal.
        XRServer.tracker_added.disconnect(_on_tracker_added)
        XRServer.tracker_updated.disconnect(_on_tracker_updated)
        XRServer.tracker_removed.disconnect(_on_tracker_removed)

        # Dọn dẹp các tracker.
        for tracker in _managed_nodes:
            removed_spatial_entity.emit(_managed_nodes[tracker])
            remove_child(_managed_nodes[tracker])
            _managed_nodes[tracker].queue_free()

        _managed_nodes.clear()


    # Kiểm tra xem tracker này có nên được chúng ta quản lý hay không và thêm nó.
    func _add_tracker(tracker: OpenXRSpatialEntityTracker):
        var new_node: XRAnchor3D

        if _managed_nodes.has(tracker):
            # Đã được chúng ta quản lý rồi!
            return

        if tracker is OpenXRAnchorTracker:
            # Lưu ý: Nói chung, spatial anchor do nhà phát triển kiểm soát và
            # khó có khả năng được manager của chúng ta xử lý.
            # Nhưng để đầy đủ, chúng ta sẽ thêm nó vào.
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
            # Không hỗ trợ loại spatial entity tracker nào?
            push_warning("OpenXR Spatial Entities: Unsupported anchor tracker " + tracker.get_name() + " of type " + tracker.get_class())

        if not new_node:
            # Không có scene nào được định nghĩa hoặc có thể khởi tạo? Xong rồi!
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
        # và scene được khởi tạo có thể tự phản hồi việc này nếu cần.
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

Spatial anchors cho phép chúng ta ánh xạ các vị trí trong thế giới thực vào thế giới ảo theo cách mà XR runtime sẽ theo dõi các vị trí này và điều chỉnh chúng khi cần. Nếu được hỗ trợ, anchors có thể được lưu giữ lâu dài (persistent), nghĩa là các anchors sẽ được tạo lại đúng vị trí khi ứng dụng của bạn khởi động lại.

Bạn có thể hình dung các trường hợp sử dụng như:
- đặt các cửa sổ ảo xung quanh không gian của bạn để chúng được tạo lại khi ứng dụng khởi động lại
- đặt các vật thể ảo trên bàn hoặc trên tường của bạn và tạo lại chúng

Spatial anchors được theo dõi bằng các đối tượng :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>` được đăng ký với XRServer.

Khi cần, vị trí của spatial anchor sẽ được tự động cập nhật; pose trên tracker liên quan sẽ được cập nhật và do đó node :ref:`XRAnchor3D<class_XRAnchor3D>` sẽ được định vị lại.

Khi một spatial anchor được lưu giữ lâu dài, một Universally Unique Identifier (hay UUID) sẽ được gán cho anchor đó. Bạn sẽ cần lưu thông tin này cùng với mọi thông tin cần thiết để dựng lại scene. Trong mã ví dụ bên dưới, chúng ta sẽ gọi đơn giản ``set_scene_path`` và ``get_scene_path``, nhưng bạn sẽ cần tự triển khai các hàm này.

Để tạo một anchor được lưu giữ lâu dài, bạn cần thực hiện theo một quy trình cụ thể:
- Tạo spatial anchor
- Chờ cho đến khi trạng thái tracking thay đổi thành ``ENTITY_TRACKING_STATE_TRACKING``
- Lưu giữ anchor lâu dài
- Lấy UUID và lưu lại

Khi tìm thấy một anchor lâu dài hiện có, một tracker mới sẽ được thêm vào với UUID đã được thiết lập sẵn. Chính sự khác biệt trong quy trình này cho phép chúng ta phản hồi chính xác với các persistent anchor mới và hiện có.

.. note::

    Nếu bạn hủy trạng thái persistent của một anchor, UUID sẽ bị hủy nhưng anchor không tự động bị xóa. Bạn sẽ cần phản hồi khi quá trình hủy trạng thái persistent của anchor hoàn tất rồi dọn dẹp nó. Ngoài ra, bạn sẽ nhận được lỗi nếu cố hủy một anchor vẫn đang ở trạng thái persistent.

Để hoàn thiện hệ thống anchor, trước tiên chúng ta tạo một scene và đặt scene đó làm scene sẽ được khởi tạo cho các anchor trên node spatial manager của chúng ta.

Scene này phải có một node :ref:`XRAnchor3D<class_XRAnchor3D>` làm root và không có gì khác. Chúng ta sẽ thêm một script vào đó để tải một subscene chứa phần hiển thị thực tế của anchor, nhờ vậy chúng ta có thể tạo các anchor khác nhau trong scene của mình. Chúng ta sẽ giả định mục đích là làm cho các anchor này ở trạng thái persistent và lưu đường dẫn đến subscene này làm metadata cho UUID của chúng ta.

.. code-block:: gdscript

    class_name OpenXRSpatialAnchor3D
    extends XRAnchor3D

    var anchor_tracker: OpenXRAnchorTracker
    var child_scene: Node
    var made_persistent: bool = false

    ## Trả về đường dẫn scene cho UUID của chúng ta.
    func get_scene_path(p_uuid: String) -> String:
        # Placeholder, hãy triển khai phần này.
        return ""


    ## Lưu đường dẫn scene cho UUID của chúng ta.
    func set_scene_path(p_uuid: String, p_scene_path: String):
        # Placeholder, hãy triển khai phần này.
        pass


    ## Xóa thông tin liên quan đến UUID của chúng ta.
    func remove_uuid(p_uuid: String):
        # Placeholder, hãy triển khai phần này.
        pass


    ## Đặt scene con cho anchor này, gọi hàm này khi tạo một anchor mới.
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

            # Làm cho nó persistent; việc này sẽ thông báo rằng UUID trên anchor đã thay đổi,
            # sau đó chúng ta có thể lưu đường dẫn scene mà chúng ta đã áp dụng cho
            # scene đang được tracking.
            OpenXRSpatialAnchorCapability.persist_anchor(anchor_tracker, RID(), Callable())


    func _on_uuid_changed() -> void:
        if anchor_tracker.uuid != "":
            made_persistent = true

            if child_scene:
                # Nếu đã có subscene, hãy lưu subscene đó cùng với UUID.
                set_scene_path(anchor_tracker.uuid, child_scene.scene_file_path)
            else:
                # Nếu chưa có, hãy tra UUID trong bộ nhớ đệm đã lưu của chúng ta.
                var scene_path: String = get_scene_path(anchor_tracker.uuid)
                if scene_path.is_empty():
                    # Đưa ra cảnh báo rằng chúng ta không có tệp scene được lưu cho UUID này.
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

Sau khi đã có anchor scene, chúng ta có thể thêm một vài hàm vào script spatial manager để tạo hoặc xóa anchors:

.. code-block:: gdscript

    ...

    ## Tạo một spatial anchor mới cùng với scene con tương ứng.
    ## Nếu persistent anchors được hỗ trợ, node này sẽ được tạo dưới dạng persistent
    ## và chúng ta sẽ lưu đường dẫn scene con cùng với UUID của anchor để tạo lại về sau.
    func create_spatial_anchor(p_transform: Transform3D, p_child_scene_path: String):
        # Chúng ta có hỗ trợ anchor không?
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            push_error("Spatial anchors are not supported on this device!")
            return

        # Điều chỉnh transform của chúng ta về không gian cục bộ.
        var t: Transform3D = global_transform.inverse() * p_transform

        # Tạo anchor trên manager hiện tại của chúng ta.
        var new_anchor = OpenXRSpatialAnchorCapability.create_new_anchor(t, RID())
        if not new_anchor:
            push_error("Couldn't create an anchor for %s." % [ p_child_scene_path ])
            return

        # Việc tạo anchor mới sẽ dẫn đến một XRAnchor được thêm vào scene
        # bởi manager của chúng ta. Vì vậy, chúng ta có thể tiếp tục giả định rằng việc này đã xảy ra.

        var anchor_scene = get_tracked_scene(new_anchor)
        if not anchor_scene:
            push_error("Couldn't locate anchor scene for %s, has the manager been configured with an applicable anchor scene?" % [ new_anchor.name ])
            return
        if not anchor_scene is OpenXRSpatialAnchor3D:
            push_error("Anchor scene for %s is not an OpenXRSpatialAnchor3D scene, has the manager been configured with an applicable anchor scene?" % [ new_anchor.name ])
            return

        anchor_scene.set_child_scene(p_child_scene_path)


    ## Xóa spatial anchor này khỏi scene của chúng ta.
    ## Nếu spatial anchor là persistent, UUID liên kết sẽ được xóa.
    func remove_spatial_anchor(p_anchor: XRAnchor3D):
        # Chúng ta có hỗ trợ anchor không?
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            push_error("Spatial anchors are not supported on this device!")
            return

        var tracker: XRTracker = XRServer.get_tracker(p_anchor.tracker)
        if tracker and tracker is OpenXRAnchorTracker:
            var anchor_tracker: OpenXRAnchorTracker = tracker
            if anchor_tracker.has_uuid() and OpenXRSpatialAnchorCapability.is_spatial_persistence_supported():
                # Nếu có UUID, trước tiên chúng ta nên đặt anchor thành không persistent
                # sau đó xóa nó trong callback của anchor.
                remove_uuid(anchor_tracker.uuid)
                OpenXRSpatialAnchorCapability.unpersist_anchor(anchor_tracker, RID(), _on_unpersist_complete)
            else:
                # Nếu không, chúng ta chỉ cần xóa nó.
                # Thao tác này sẽ xóa nó khỏi XRServer, từ đó kích hoạt việc dọn dẹp node của chúng ta.
                OpenXRSpatialAnchorCapability.remove_anchor(tracker)


    func _on_unpersist_complete(p_tracker: XRTracker):
        # Tracker của chúng ta hiện không còn persistent nữa, chúng ta có thể xóa nó.
        OpenXRSpatialAnchorCapability.remove_anchor(p_tracker)


    ## Lấy scene đã được thêm cho một tracker nhất định (nếu có).
    func get_tracked_scene(p_tracker: XRTracker) -> XRNode3D:
        for node in get_children():
            if node is XRNode3D and node.tracker == p_tracker.name:
                return node

        return null

.. note::

    Có vẻ như có một chút phép màu đang diễn ra trong đoạn code trên. Bất cứ khi nào một spatial anchor được tạo hoặc xóa trên anchor capability của chúng ta, tracker object liên quan sẽ được tạo hoặc hủy. Điều này khiến spatial manager thêm hoặc xóa child scene cho anchor này. Vì vậy, ở đây chúng ta có thể dựa vào cơ chế đó.

Theo dõi mặt phẳng
------------------

Theo dõi mặt phẳng cho phép chúng ta phát hiện các bề mặt như tường, sàn, trần nhà và bàn ở xung quanh người chơi. Dữ liệu này có thể đến từ việc người dùng quét phòng vào bất kỳ thời điểm nào trước đó, hoặc được các cảm biến quang học phát hiện theo thời gian thực. Extension theo dõi mặt phẳng không phân biệt hai trường hợp này.

.. note::

    Một số XR runtime yêu cầu các vendor extension để bật và/hoặc cấu hình quy trình này, nhưng dữ liệu sẽ được cung cấp thông qua extension này.

Đoạn code chúng ta đã viết ở trên cho spatial manager sẽ tự động phát hiện các mặt phẳng mới. Tuy nhiên, chúng ta cần thiết lập một scene mới và gán scene đó cho spatial manager.

Node gốc của scene này phải là một :ref:`XRAnchor3D<class_XRAnchor3D>` node. Chúng ta sẽ thêm một :ref:`StaticBody3D<class_StaticBody3D>` node làm node con và thêm một
:ref:`CollisionShape3D<class_CollisionShape3D>` và :ref:`MeshInstance3D<class_MeshInstance3D>` node làm các node con của static body.

.. image:: img/openxr_plane_anchor.webp

Static body và collision shape sẽ cho phép chúng ta làm cho mặt phẳng có thể tương tác.

Mesh instance node cho phép chúng ta áp dụng vật liệu "hole punch" cho mặt phẳng; khi kết hợp với passthrough, nó biến mặt phẳng thành một visual occluder. Ngoài ra, chúng ta có thể gán một vật liệu dùng để hiển thị mặt phẳng nhằm debug.

Chúng ta cấu hình vật liệu này làm vật liệu ``material_override`` trên MeshInstance3D. Đối với vật liệu "hole punch", hãy tạo một :ref:`ShaderMaterial<class_ShaderMaterial>` và sử dụng đoạn code sau làm shader code:

.. code-block:: glsl

    shader_type spatial;
    render_mode unshaded, shadow_to_opacity;

    void fragment() {
        ALBEDO = vec3(0.0, 0.0, 0.0);
    }

Chúng ta cũng cần thêm một script vào scene để đảm bảo collision và mesh được áp dụng.

.. code-block:: gdscript

    extends XRAnchor3D

    var plane_tracker: OpenXRPlaneTracker

    func _update_mesh_and_collision():
        if plane_tracker:
            # Đặt static body bằng offset của chúng ta để cả collision
            # và mesh đều được định vị chính xác.
            $StaticBody3D.transform = plane_tracker.get_mesh_offset()

            # Đặt mesh để chúng ta có thể che khuất bề mặt.
            $StaticBody3D/MeshInstance3D.mesh = plane_tracker.get_mesh()

            # Và đặt shape để các đối tượng có thể va chạm với bề mặt của chúng ta.
            $StaticBody3D/CollisionShape3D.shape = plane_tracker.get_shape()


    func _ready():
        plane_tracker = XRServer.get_tracker(tracker)
        if plane_tracker:
            _update_mesh_and_collision()

            plane_tracker.mesh_changed.connect(_update_mesh_and_collision)

Nếu XR runtime hỗ trợ, bạn có thể truy vấn thêm metadata trên plane tracker object. Đáng chú ý là thuộc tính ``plane_label``; nếu có, thuộc tính này xác định loại bề mặt. Vui lòng tham khảo tài liệu class :ref:`OpenXRPlaneTracker<class_OpenXRPlaneTracker>` để biết thêm thông tin.

Theo dõi marker
---------------

Theo dõi marker phát hiện các marker cụ thể trong thế giới thực. Đây thường là các hình ảnh được in, chẳng hạn như mã QR.

API cung cấp hỗ trợ cho 4 loại mã khác nhau: mã QR, mã Micro QR, mã Aruco và April tag; tuy nhiên, XR runtime không bắt buộc phải hỗ trợ tất cả.

Khi phát hiện marker, các object :ref:`OpenXRMarkerTracker<class_OpenXRMarkerTracker>` được khởi tạo và đăng ký với XRServer.

Code spatial manager hiện có của chúng ta đã tự động phát hiện các marker này; tất cả những gì cần làm là tạo một scene có node :ref:`XRAnchor3D<class_XRAnchor3D>` ở gốc, lưu scene đó, rồi gán nó cho spatial manager làm scene cần khởi tạo cho các marker.

Marker tracker sẽ được cấu hình đầy đủ khi được gán, vì vậy tất cả những gì cần thiết là một hàm ``_ready`` phản hồi dữ liệu marker. Dưới đây là template cho đoạn code bắt buộc:

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
                        # Dữ liệu là mã QR ở dạng string, thường là một URL.
                        pass
                    elif data is PackedByteArray:
                        # Dữ liệu là binary, có thể là bất kỳ thứ gì.
                        pass
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_MICRO_QRCODE:
                    var data = marker_tracker.get_marker_data()
                    if data is String:
                        # Dữ liệu là mã QR ở dạng string, thường là một URL.
                        pass
                    elif data is PackedByteArray:
                        # Dữ liệu là binary, có thể là bất kỳ thứ gì.
                        pass
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_ARUCO:
                    # Sử dụng marker_tracker.marker_id để xác định marker.
                    pass
                OpenXRSpatialComponentMarkerList.MARKER_TYPE_APRIL_TAG:
                    # Sử dụng marker_tracker.marker_id để xác định marker.
                    pass

Như chúng ta có thể thấy, QR Code cung cấp một data block ở dạng string hoặc byte array. Aruco và April tag cung cấp một ID được đọc từ mã.

Cách liên kết tốt nhất dữ liệu marker với scene cần tải phụ thuộc vào use case của bạn. Ví dụ, bạn có thể mã hóa tên asset muốn hiển thị vào mã QR.

Truy cập backend
----------------

Trong hầu hết trường hợp, core system cùng với mọi vendor extension sẽ là những gì mà phần lớn người dùng sử dụng ở trạng thái được cung cấp.

Đối với những người triển khai vendor extension, hoặc những người mà logic tích hợp sẵn không đáp ứng đủ nhu cầu, quyền truy cập backend được cung cấp thông qua một tập hợp các singleton object.

Các object này cũng có thể được dùng để truy vấn những capability nào được headset đang sử dụng hỗ trợ. Ở các phần trên, chúng ta đã thêm code kiểm tra các capability này trong spatial manager và spatial anchor code.

.. note::

    Hệ thống spatial entities sẽ đóng gói nhiều OpenXR entity vào các resource được trả về dưới dạng RID.

Lõi thực thể không gian
~~~~~~~~~~~~~~~~~~~~~~~

Chức năng cốt lõi của thực thể không gian được cung cấp thông qua
:ref:`OpenXRSpatialEntityExtension<class_OpenXRSpatialEntityExtension>` singleton.

Logic cụ thể được cung cấp thông qua các capability, trong đó giới thiệu những kiểu component chuyên biệt và cho phép truy cập các kiểu thực thể cụ thể; tuy nhiên, tất cả đều sử dụng cùng một cơ chế để truy cập dữ liệu thực thể do hệ thống thực thể không gian quản lý.

Trước tiên, chúng ta sẽ xem xét từng component tạo nên hệ thống cốt lõi.

Spatial context
"""""""""""""""

Spatial context là đối tượng chính dùng để truy vấn hệ thống thực thể không gian. Spatial context cho phép chúng ta cấu hình cách tương tác với một hoặc nhiều capability.

Bạn nên tạo một spatial context cho mỗi capability mà bạn muốn tương tác; thực tế, đây cũng là cách Godot triển khai logic tích hợp sẵn.

Trước tiên, chúng ta thiết lập các đối tượng cấu hình capability cho những capability muốn truy cập. Mỗi capability sẽ bật các component được hỗ trợ cho capability đó. Các thiết lập có thể xác định những component nào sẽ được bật. Chúng ta sẽ xem xét chi tiết hơn các đối tượng cấu hình này khi tìm hiểu từng capability được hỗ trợ.

Việc tạo spatial context là một tác vụ bất đồng bộ (asynchronous). Điều này có nghĩa là chúng ta yêu cầu XR runtime tạo một spatial context, rồi tại một thời điểm sau đó, XR runtime sẽ cung cấp kết quả cho chúng ta.

Script sau đây là phần bắt đầu của ví dụ và có thể được thêm dưới dạng một node vào scene của bạn. Script này minh họa cách tạo một spatial context để theo dõi mặt phẳng và thiết lập cơ chế khám phá thực thể.

.. code-block:: gdscript

    extends Node

    var spatial_context: RID

    func _set_up_spatial_context():
        # Đã thiết lập xong?
        if spatial_context:
            return

        # Không được hỗ trợ hoặc chúng ta chưa sẵn sàng?
        if not OpenXRSpatialPlaneTrackingCapability.is_supported():
            return

        # Ở đây, chúng ta sẽ dùng tính năng theo dõi mặt phẳng làm ví dụ; đối tượng cấu hình của chúng ta
        # ở đây không có cấu hình bổ sung nào. Nó chỉ cần tồn tại.
        var plane_capability : OpenXRSpatialCapabilityConfigurationPlaneTracking = OpenXRSpatialCapabilityConfigurationPlaneTracking.new()

        var future_result : OpenXRFutureResult = OpenXRSpatialEntityExtension.create_spatial_context([ plane_capability ])

        # Chờ hoàn tất thao tác bất đồng bộ.
        await future_result.completed

        # Nhận kết quả.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với signal khám phá.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện lần khám phá ban đầu.
            _on_perform_discovery(spatial_context)


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Đề phòng trường hợp session của chúng ta chưa bắt đầu,
            # gọi hàm tạo spatial context khi bắt đầu.
            openxr_interface.session_begun.connect(_set_up_spatial_context)

            # Và nếu nó đã đang chạy, hãy gọi ngay hàm này,
            # hàm sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_spatial_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi signal khám phá.
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

Ảnh chụp khám phá
"""""""""""""""""

Sau khi spatial context được tạo, XR runtime sẽ bắt đầu quản lý các thực thể không gian theo cấu hình của những capability đã chỉ định.

Để tìm các thực thể mới hoặc lấy thông tin về những thực thể hiện tại, chúng ta có thể tạo một ảnh chụp khám phá. Thao tác này yêu cầu XR runtime thu thập dữ liệu cụ thể liên quan đến tất cả thực thể không gian hiện đang được spatial context quản lý.

Hàm này là bất đồng bộ vì việc thu thập dữ liệu và cung cấp kết quả có thể mất một khoảng thời gian. Nói chung, bạn sẽ muốn thực hiện ảnh chụp khám phá khi phát hiện các thực thể mới. OpenXR phát một event khi có các thực thể mới cần được xử lý; điều này khiến signal ``spatial_discovery_recommended`` được phát bởi
:ref:`OpenXRSpatialEntityExtension<class_OpenXRSpatialEntityExtension>` singleton.

Lưu ý trong đoạn code ví dụ ở trên, chúng ta đã kết nối với signal này và gọi phương thức ``_on_perform_discovery`` trên node của mình. Hãy triển khai phương thức này:

.. code-block:: gdscript

    ...

    var discovery_result : OpenXRFutureResult

    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận được signal này cho tất cả spatial context, nên hãy thoát nếu signal không dành cho context này.
        if p_spatial_context != spatial_context:
            return

        # Nếu hiện đang có một kết quả khám phá đang thực hiện, hãy hủy kết quả đó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện khám phá.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_PLANE_ALIGNMENT \
            ])

        # Chờ hoàn tất thao tác bất đồng bộ.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả ảnh chụp.
            _process_snapshot(snapshot)

            # Và dọn dẹp ảnh chụp.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot):
        # Xem phần bên dưới.
        pass


Lưu ý rằng khi gọi ``discover_spatial_entities``, chúng ta chỉ định một danh sách component. Truy vấn khám phá sẽ tìm mọi thực thể do spatial context quản lý và có ít nhất một trong các component đã chỉ định.

Ảnh chụp cập nhật
"""""""""""""""""

Thực hiện ảnh chụp cập nhật cho phép chúng ta lấy thông tin đã cập nhật về những thực thể trước đó đã được tìm thấy bằng ảnh chụp khám phá. Hàm này là đồng bộ (synchronous), chủ yếu dùng để lấy dữ liệu trạng thái và vị trí, đồng thời có thể được chạy ở mỗi frame.

Nói chung, bạn chỉ thực hiện ảnh chụp cập nhật khi các thực thể có khả năng thay đổi hoặc có quy trình vòng đời. Một ví dụ điển hình là các anchor và marker liên tục. Hãy tham khảo tài liệu về capability để xác định xem có cần thao tác này hay không.

Tuy nhiên, theo dõi mặt phẳng không cần thao tác này. Để hoàn tất ví dụ, sau đây là ví dụ về ảnh chụp cập nhật cho tính năng theo dõi mặt phẳng nếu chúng ta cần:

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
            # Xử lý ảnh chụp.
            _process_snapshot(snapshot)

            # Và dọn dẹp ảnh chụp.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)

Lưu ý rằng trong ví dụ này, chúng ta sử dụng cùng một hàm ``_process_snapshot`` để xử lý ảnh chụp. Cách này phù hợp trong hầu hết trường hợp. Tuy nhiên, nếu các component bạn chỉ định khi tạo ảnh chụp khác nhau giữa ảnh chụp khám phá và ảnh chụp cập nhật, bạn phải tính đến sự khác biệt giữa các component đó.

Truy vấn ảnh chụp
"""""""""""""""""

Sau khi có ảnh chụp, chúng ta có thể chạy các truy vấn trên ảnh chụp đó để lấy dữ liệu bên trong. Ảnh chụp được đảm bảo không thay đổi cho đến khi bạn giải phóng nó.

Với mỗi component chúng ta thêm vào snapshot, chúng ta có một đối tượng dữ liệu đi kèm. Đối tượng dữ liệu này có hai chức năng: thêm nó vào query sẽ đảm bảo chúng ta query loại component đó, đồng thời đây là đối tượng mà dữ liệu được query sẽ được nạp vào.

Có một đối tượng dữ liệu đặc biệt luôn phải được thêm vào danh sách request ở vị trí đầu tiên, đó là :ref:`OpenXRSpatialQueryResultData<class_OpenXRSpatialQueryResultData>`. Đối tượng này sẽ chứa một mục cho mỗi entity được trả về, cùng với ID duy nhất và trạng thái hiện tại của entity.

Hoàn thiện logic discovery, chúng ta thêm các phần sau:

.. code-block:: gdscript

    ...

    var entities : Dictionary[int, OpenXRSpatialEntityTracker]

    func _process_snapshot(p_snapshot):
        # Luôn bao gồm dữ liệu kết quả query.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()

        # Thêm dữ liệu component 2D có giới hạn.
        var bounded2d_list : OpenXRSpatialComponentBounded2DList = OpenXRSpatialComponentBounded2DList.new()

        # Và dữ liệu component căn chỉnh theo mặt phẳng.
        var alignment_list : OpenXRSpatialComponentPlaneAlignmentList = OpenXRSpatialComponentPlaneAlignmentList.new()

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, [ query_result_data, bounded2d_list, alignment_list]):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # Trạng thái này chỉ xuất hiện khi thực hiện update snapshot
                    # và cho biết entity này không còn được theo dõi.
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

                    # Nếu đang theo dõi, chúng ta nên query các component còn lại.
                    if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_TRACKING:
                        var center_pose : Transform3D = bounded2d_list.get_center_pose(i)
                        entity_tracker.set_pose("default", center_pose, Vector3(), Vector3(), XRPose.XR_TRACKING_CONFIDENCE_HIGH)

                        # Trong ví dụ này, tôi sử dụng OpenXRSpatialEntityTracker, vốn không
                        # chứa thêm dữ liệu nào. Bạn nên mở rộng class này để lưu trữ trạng thái
                        # bổ sung đã truy xuất. Đối với việc theo dõi mặt phẳng, đó sẽ là OpenXRPlaneTracker
                        # và chúng ta có thể lưu trữ dữ liệu sau trong tracker:
                        var size : Vector2 = bounded2d_list.get_size(i)
                        var alignment = alignment_list.get_plane_alignment(i)
                    else:
                        entity_tracker.invalidate_pose("default")

                    # Chúng ta không đăng ký tracker cho đến khi đã thiết lập dữ liệu ban đầu.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

.. note::

    Trong ví dụ trên, chúng ta dựa vào ``ENTITY_TRACKING_STATE_STOPPED`` để dọn dẹp các spatial entity không còn được theo dõi. Tính năng này chỉ khả dụng với update snapshot.

    Đối với các capability chỉ dựa vào discovery snapshot, bạn có thể muốn thực hiện dọn dẹp dựa trên các entity không còn thuộc snapshot, thay vì dựa vào thay đổi trạng thái.

Spatial entities
""""""""""""""""

Với những thông tin trên, giờ chúng ta đã biết cách query các spatial entity và lấy thông tin về chúng, nhưng vẫn còn một số điều cần xem xét liên quan đến chính các entity này.

Về lý thuyết, chúng ta lấy toàn bộ dữ liệu từ snapshot, tuy nhiên OpenXR có thêm một API cho phép chúng ta tạo đối tượng spatial entity từ entity ID. Khi đối tượng này còn tồn tại, XR runtime biết rằng chúng ta đang sử dụng entity này và entity sẽ không bị dọn dẹp sớm. Đây là điều kiện tiên quyết để thực hiện update query trên entity này.

Trong code ví dụ, chúng ta thực hiện việc này bằng cách gọi ``OpenXRSpatialEntityExtension.make_spatial_entity``.

Một số spatial entity API sẽ tự động tạo đối tượng cho chúng ta. Trong trường hợp này, chúng ta cần gọi ``OpenXRSpatialEntityExtension.add_spatial_entity`` để đăng ký đối tượng đã tạo với implementation của mình.

Cả hai function đều trả về một RID mà chúng ta có thể sử dụng trong các function tiếp theo yêu cầu đối tượng entity của mình.

Khi hoàn tất, chúng ta có thể gọi ``OpenXRSpatialEntityExtension.free_spatial_entity``.

Lưu ý rằng chúng ta không làm vậy trong code ví dụ. Việc này được tự động xử lý khi
instance :ref:`OpenXRSpatialEntityTracker<class_OpenXRSpatialEntityTracker>` bị hủy.

Spatial anchor capability
~~~~~~~~~~~~~~~~~~~~~~~~~

Spatial anchor được quản lý bởi singleton object :ref:`OpenXRSpatialAnchorCapability<class_OpenXRSpatialAnchorCapability>` của chúng ta. Sau khi OpenXR session được tạo, bạn có thể gọi ``OpenXRSpatialAnchorCapability.is_spatial_anchor_supported`` để kiểm tra xem tính năng spatial anchor có được phần cứng của bạn hỗ trợ hay không.

Spatial anchor capability có một vài điểm khác với những gì chúng ta đã trình bày ở trên.

Hệ thống spatial anchor cho phép chúng ta xác định, theo dõi, lưu giữ và chia sẻ một vị trí vật lý. Điểm khác biệt là chúng ta tạo và hủy anchor, vì vậy chúng ta quản lý vòng đời của nó.

Do đó, chúng ta chỉ sử dụng hệ thống discovery để phát hiện các anchor được tạo và lưu giữ trong những session trước, hoặc các anchor được chia sẻ với chúng ta.

.. note::

    Hiện tại, đặc tả spatial entities chưa hỗ trợ việc chia sẻ anchor.

Như đã trình bày trong ví dụ trước, chúng ta luôn bắt đầu bằng việc tạo một spatial context, nhưng giờ sẽ sử dụng
đối tượng cấu hình :ref:`OpenXRSpatialCapabilityConfigurationAnchor<class_OpenXRSpatialCapabilityConfigurationAnchor>`. Chúng ta sẽ trình bày ví dụ code này sau khi thảo luận về persistence scope. Trước tiên, hãy xem cách quản lý các anchor cục bộ.

Việc tạo spatial anchor không khác với logic tích hợp mà chúng ta đã thảo luận. Điều quan trọng duy nhất là truyền spatial context của riêng bạn làm tham số cho ``OpenXRSpatialAnchorCapability.create_new_anchor``.

Để lưu giữ một anchor, bạn phải đợi cho đến khi anchor ở trạng thái tracking; điều này có nghĩa là bạn phải thực hiện update query cho mọi anchor được tạo để có thể xử lý các thay đổi trạng thái.

Để bật khả năng lưu giữ anchor, bạn cũng phải thiết lập một persistence scope. Trong core của OpenXR, có hai loại persistence scope được hỗ trợ:

.. list-table:: Persistence scopes
   :header-rows: 1

   * - Enum
     - Mô tả
   * - PERSISTENCE_SCOPE_SYSTEM_MANAGED
     - Cung cấp cho ứng dụng quyền truy cập chỉ đọc (tức là ứng dụng không thể sửa đổi store này) vào các spatial entity được hệ thống lưu giữ và quản lý. Ứng dụng có thể sử dụng UUID trong persistence component của store này để đối chiếu các entity giữa các spatial context và những lần khởi động lại thiết bị.
   * - PERSISTENCE_SCOPE_LOCAL_ANCHORS
     - Các thao tác persistence và quyền truy cập dữ liệu chỉ giới hạn ở các spatial anchor trên cùng thiết bị, dành cho cùng một người dùng và ứng dụng (sử dụng các function `persist_anchor` và `unpersist_anchor`)

Chúng ta sẽ bắt đầu với một script mới để xử lý các spatial anchor. Script này sẽ tương tự script đã trình bày trước đó, nhưng có một vài điểm khác biệt.

Điểm khác biệt đầu tiên là việc tạo persistence scope.

.. code-block:: gdscript

    extends Node

    var persistence_context : RID

    func _set_up_persistence_context():
        # Đã thiết lập xong?
        if persistence_context:
            # Kiểm tra spatial context của chúng ta.
            _set_up_spatial_context()
            return

        # Không được hỗ trợ hoặc chúng ta chưa sẵn sàng? Chỉ cần thoát.
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            return

        # Nếu không thể sử dụng persistence scope, chỉ cần tạo spatial context mà không có nó.
        if not OpenXRSpatialAnchorCapability.is_spatial_persistence_supported():
            _set_up_spatial_context()
            return

        var scope : int = 0
        if OpenXRSpatialAnchorCapability.is_persistence_scope_supported(OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_LOCAL_ANCHORS):
            scope = OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_LOCAL_ANCHORS
        elif OpenXRSpatialAnchorCapability.is_persistence_scope_supported(OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_SYSTEM_MANAGED):
            scope = OpenXRSpatialAnchorCapability.PERSISTENCE_SCOPE_SYSTEM_MANAGED
        else:
            # Không có persistence scope đã biết, hãy báo cáo và thiết lập mà không có nó.
            push_error("No known persistence scope is supported.")
            _set_up_spatial_context()
            return

        # Tạo persistence scope của chúng ta.
        var future_result : OpenXRFutureResult = OpenXRSpatialAnchorCapability.create_persistence_context(scope)
        if not future:
            # Không thể tạo persistence scope? Chỉ cần thiết lập mà không có nó.
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
            # Đề phòng session của chúng ta chưa bắt đầu,
            # gọi hàm tạo context khi bắt đầu, trước tiên sử dụng persistence scope của chúng ta.
            openxr_interface.session_begun.connect(_set_up_persistence_context)

            # Và nếu nó đã hoạt động, hãy gọi ngay,
            # hàm sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_persistence_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi discovery signal của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context của chúng ta để dọn dẹp nó.
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
        # Đã thiết lập xong?
        if spatial_context:
            return

        # Không được hỗ trợ hoặc chúng ta chưa thiết lập xong.
        if not OpenXRSpatialAnchorCapability.is_spatial_anchor_supported():
            return

        # Tạo anchor capability của chúng ta.
        var anchor_capability : OpenXRSpatialCapabilityConfigurationAnchor = OpenXRSpatialCapabilityConfigurationAnchor.new()

        # Và thiết lập persistence configuration object của chúng ta (nếu cần).
        var persistence_config : OpenXRSpatialContextPersistenceConfig
        if persistence_context:
            persistence_config = OpenXRSpatialContextPersistenceConfig.new()
            persistence_config.add_persistence_context(persistence_context)

        var future_result : OpenXRFutureResultg = OpenXRSpatialEntityExtension.create_spatial_context([ anchor_capability ], persistence_config)

        # Chờ async completion.
        await future_result.completed

        # Lấy kết quả của chúng ta.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với discovery signal của chúng ta.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện discovery ban đầu của chúng ta.
            _on_perform_discovery(spatial_context)


Việc tạo discovery snapshot cho các anchor của chúng ta gần như giống với những gì chúng ta đã làm trước đây, tuy nhiên chỉ hợp lý khi tạo snapshot cho các anchor persistent. Chúng ta đã biết các anchor được tạo trong session của mình, chúng ta chỉ muốn truy cập những anchor đến từ XR runtime.

Chúng ta cũng muốn thực hiện các truy vấn cập nhật thường xuyên; ở đây chúng ta chỉ quan tâm đến state, vì vậy cần xử lý snapshot của mình hơi khác một chút.

Anchor system cung cấp cho chúng ta quyền truy cập vào hai component:

.. list-table:: Các anchor component
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
        # Chúng ta nhận signal này cho mọi spatial context, vì vậy hãy thoát nếu signal này không dành cho chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Bỏ qua bước này nếu chúng ta không có persistence context.
        if not persistence_context:
            return

        # Nếu hiện đang có discovery result đang chạy, hãy hủy nó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery của chúng ta.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_ANCHOR, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_PERSISTENCE \
            ])

        # Chờ async completion.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý snapshot result của chúng ta.
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


Cuối cùng, chúng ta có thể xử lý snapshot của mình. Lưu ý rằng chúng ta sử dụng :ref:`OpenXRAnchorTracker<class_OpenXRAnchorTracker>` làm tracker class vì class này đã tích hợp sẵn toàn bộ hỗ trợ cho anchor.

.. code-block:: gdscript

    ...

    func _process_snapshot(p_snapshot, p_get_uuids):
        var result_data : Array

        # Luôn thêm query result data của chúng ta.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()
        result_data.push_back(query_result_data)

        # Thêm anchor component data của chúng ta.
        var anchor_list : OpenXRSpatialComponentAnchorList = OpenXRSpatialComponentAnchorList.new()
        result_data.push_back(anchor_list)

        # Và persistent component data của chúng ta.
        var persistent_list : OpenXRSpatialComponentPersistenceList
        if p_get_uuids:
            # Chỉ thêm mục này khi cần.
            persistent_list = OpenXRSpatialComponentPersistenceList.new()
            result_data.push_back(persistent_list)

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, result_data):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # State này chỉ xuất hiện khi thực hiện update snapshot
                    # và cho biết entity này không còn được tracking.
                    # Do đó, chúng ta xóa entity này khỏi dictionary, việc này sẽ khiến
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

                    # Tuy nhiên, dữ liệu persistence là một ngoại lệ lớn; dữ liệu này có thể được cung cấp ngay cả khi chúng ta không theo dõi.
                    if p_get_uuids:
                        var persistent_state = persistent_list.get_persistent_state(i)
                        if persistent_state == 1:
                            entity_tracker.uuid = persistent_list.get_persistent_uuid(i)

                    # Chúng ta chỉ đăng ký tracker sau khi đã thiết lập dữ liệu ban đầu.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

Khả năng theo dõi mặt phẳng
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Việc theo dõi mặt phẳng được xử lý bởi
:ref:`OpenXRSpatialPlaneTrackingCapability<class_OpenXRSpatialPlaneTrackingCapability>` singleton class.

Sau khi OpenXR session được tạo, bạn có thể gọi ``OpenXRSpatialPlaneTrackingCapability.is_supported`` để kiểm tra xem tính năng theo dõi mặt phẳng có được phần cứng của bạn hỗ trợ hay không.

Ở trên, chúng ta đã cung cấp phần lớn mã cho việc theo dõi mặt phẳng, nhưng bên dưới sẽ trình bày toàn bộ phần triển khai vì phần này có một vài điều chỉnh nhỏ. Ở đây không cần cập nhật snapshot; chúng ta chỉ thực hiện snapshot discovery và triển khai hàm process.

Tính năng theo dõi mặt phẳng cung cấp quyền truy cập vào hai component chắc chắn được hỗ trợ và ba component tùy chọn.

.. list-table:: Các component theo dõi mặt phẳng
   :header-rows: 1

   * - Component
     - Data class
     - Mô tả
   * - COMPONENT_TYPE_BOUNDED_2D
     - :ref:`OpenXRSpatialComponentBounded2DList<class_OpenXRSpatialComponentBounded2DList>`
     - Cung cấp pose ở tâm và hình chữ nhật bao quanh cho mỗi mặt phẳng.
   * - COMPONENT_TYPE_PLANE_ALIGNMENT
     - :ref:`OpenXRSpatialComponentPlaneAlignmentList<class_OpenXRSpatialComponentPlaneAlignmentList>`
     - Cung cấp thông tin căn chỉnh của mỗi mặt phẳng
   * - COMPONENT_TYPE_MESH_2D
     - :ref:`OpenXRSpatialComponentMesh2DList<class_OpenXRSpatialComponentMesh2DList>`
     - Cung cấp mesh 2D định hình mỗi mặt phẳng
   * - COMPONENT_TYPE_POLYGON_2D
     - :ref:`OpenXRSpatialComponentPolygon2DList<class_OpenXRSpatialComponentPolygon2DList>`
     - Cung cấp polygon 2D định hình mỗi mặt phẳng
   * - COMPONENT_TYPE_PLANE_SEMANTIC_LABEL
     - :ref:`OpenXRSpatialComponentPlaneSemanticLabelList<class_OpenXRSpatialComponentPlaneSemanticLabelList>`
     - Cung cấp thông tin nhận dạng loại của mỗi mặt phẳng

Đối tượng cấu hình theo dõi mặt phẳng của chúng ta đã bật tất cả component được hỗ trợ, nhưng chúng ta cần truy vấn đối tượng này nên sẽ lưu instance vào một member variable. Chúng ta có thể sử dụng tracker :ref:`OpenXRPlaneTracker<class_OpenXRPlaneTracker>` để lưu dữ liệu component.

.. code-block:: gdscript

    extends Node

    var plane_capability : OpenXRSpatialCapabilityConfigurationPlaneTracking
    var spatial_context: RID
    var discovery_result : OpenXRFutureResult
    var entities : Dictionary[int, OpenXRPlaneTracker]

    func _set_up_spatial_context():
        # Đã thiết lập rồi?
        if spatial_context:
            return

        # Không được hỗ trợ hoặc chúng ta chưa sẵn sàng?
        if not OpenXRSpatialPlaneTrackingCapability.is_supported():
            return

        # Ở đây chúng ta sẽ dùng tính năng theo dõi mặt phẳng làm ví dụ; đối tượng cấu hình của chúng ta
        # ở đây không có cấu hình bổ sung nào. Nó chỉ cần tồn tại.
        plane_capability = OpenXRSpatialCapabilityConfigurationPlaneTracking.new()

        var future_result : OpenXRFutureResult = OpenXRSpatialEntityExtension.create_spatial_context([ plane_capability ])

        # Chờ hoàn tất async.
        await future_result.completed

        # Lấy kết quả.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với signal discovery.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện discovery ban đầu.
            _on_perform_discovery(spatial_context)


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Để đề phòng session chưa bắt đầu,
            # gọi hàm tạo spatial context khi bắt đầu.
            openxr_interface.session_begun.connect(_set_up_spatial_context)

            # Và nếu nó đã hoạt động, hãy gọi hàm ngay,
            # hàm sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_spatial_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi signal discovery.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context; thao tác này sẽ dọn dẹp nó.
            OpenXRSpatialEntityExtension.free_spatial_context(spatial_context)
            spatial_context = RID()

        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            openxr_interface.session_begun.disconnect(_set_up_spatial_context)


    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận signal này cho tất cả spatial context, nên hãy thoát nếu đây không phải context của chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Nếu hiện đang có kết quả discovery đang thực hiện, hãy hủy kết quả đó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, \
                plane_capability.get_enabled_components())

        # Chờ hoàn tất async.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả snapshot.
            _process_snapshot(snapshot)

            # Và dọn dẹp snapshot.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot):
        var result_data : Array

        # Tạo một bản sao các entity hiện đã tìm thấy.
        var org_entities : PackedInt64Array
        for entity_id in entities:
            org_entities.push_back(entity_id)

        # Luôn đưa dữ liệu kết quả query vào.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()
        result_data.push_back(query_result_data)

        # Thêm dữ liệu component bounded 2D.
        var bounded2d_list : OpenXRSpatialComponentBounded2DList = OpenXRSpatialComponentBounded2DList.new()
        result_data.push_back(bounded2d_list)

        # Và dữ liệu component plane alignment.
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

        # Và thêm các semantic label nếu được hỗ trợ.
        var label_list : OpenXRSpatialComponentPlaneSemanticLabelList
        if plane_capability.get_supports_labels():
            label_list = OpenXRSpatialComponentPlaneSemanticLabelList.new()
            result_data.push_back(label_list)

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, result_data):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                # Xóa entity khỏi danh sách ban đầu.
                if org_entities.has(entity_id):
                    org_entities.erase(entity_id)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # Chúng ta không thực hiện update snapshot nên không nên nhận được trường hợp này,
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

                    # Nếu đang tracking, chúng ta nên query các component còn lại.
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

                    # Chúng ta chỉ đăng ký tracker sau khi đã thiết lập dữ liệu ban đầu.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

        # Chúng ta có thể xóa mọi entity còn lại.
        for entity_id in org_entities:
            var entity_tracker : OpenXRPlaneTracker = entities[entity_id]
            entity_tracker.spatial_tracking_state = OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED
            XRServer.remove_tracker(entity_tracker)
            entities.erase(entity_id)


Khả năng theo dõi marker
~~~~~~~~~~~~~~~~~~~~~~~~

Việc theo dõi marker được xử lý bởi
:ref:`OpenXRSpatialMarkerTrackingCapability<class_OpenXRSpatialMarkerTrackingCapability>` singleton class.

Việc theo dõi marker tương tự như theo dõi mặt phẳng, tuy nhiên giờ đây chúng ta theo dõi các thực thể cụ thể trong thế giới thực dựa trên một đoạn mã được in trên một vật thể, chẳng hạn như một tờ giấy.

Có nhiều tùy chọn theo dõi marker khác nhau. OpenXR hỗ trợ sẵn 4 tùy chọn, bảng sau cung cấp thêm thông tin và tên hàm dùng để kiểm tra xem headset của bạn có hỗ trợ một tùy chọn nhất định hay không:

.. list-table:: Các tùy chọn theo dõi marker
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
   * - Mã QR
     - ``qrcode_is_supported``
     - :ref:`OpenXRSpatialCapabilityConfigurationQrCode<class_OpenXRSpatialCapabilityConfigurationQrCode>`
   * - Mã Micro QR
     - ``micro_qrcode_is_supported``
     - :ref:`OpenXRSpatialCapabilityConfigurationMicroQrCode<class_OpenXRSpatialCapabilityConfigurationMicroQrCode>`

Mỗi tùy chọn có configuration object riêng mà bạn có thể sử dụng khi tạo một thực thể không gian.

Mã QR cho phép bạn mã hóa một chuỗi, chuỗi này được XR runtime giải mã và có thể truy cập khi tìm thấy marker. Với April tag và marker Aruco, dữ liệu nhị phân được mã hóa và bạn cũng có thể truy cập dữ liệu này khi tìm thấy marker, tuy nhiên bạn cần cấu hình việc phát hiện bằng đúng định dạng giải mã.

Ví dụ, chúng ta sẽ tạo một spatial context để tìm mã QR và marker Aruco.

.. code-block:: gdscript

    extends Node

    var qrcode_config : OpenXRSpatialCapabilityConfigurationQrCode
    var aruco_config : OpenXRSpatialCapabilityConfigurationAruco
    var spatial_context: RID

    func _set_up_spatial_context():
        # Đã thiết lập sẵn?
        if spatial_context:
            return

        var configurations : Array

        # Thêm cấu hình mã QR.
        if not OpenXRSpatialMarkerTrackingCapability.qrcode_is_supported():
            qrcode_config = OpenXRSpatialCapabilityConfigurationQrCode.new()
            configurations.push_back(qrcode_config)

        # Thêm cấu hình marker Aruco.
        if not OpenXRSpatialMarkerTrackingCapability.aruco_is_supported():
            aruco_config = OpenXRSpatialCapabilityConfigurationAruco.new()
            aruco_config.aruco_dict = OpenXRSpatialCapabilityConfigurationAruco.ARUCO_DICT_7X7_1000
            configurations.push_back(aruco_config)

        # Không có gì được hỗ trợ?
        if configurations.is_empty():
            return

        var future_result : OpenXRFutureResult = OpenXRSpatialEntityExtension.create_spatial_context(configurations)

        # Chờ hoàn tất async.
        await future_result.completed

        # Lấy kết quả.
        spatial_context = future_result.get_spatial_context()
        if spatial_context:
            # Kết nối với signal discovery.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.connect(_on_perform_discovery)

            # Thực hiện lần discovery đầu tiên.
            _on_perform_discovery(spatial_context)


    func _enter_tree():
        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            # Đề phòng session của chúng ta chưa bắt đầu,
            # hãy gọi hàm tạo spatial context khi bắt đầu.
            openxr_interface.session_begun.connect(_set_up_spatial_context)

            # Và nếu nó đã đang chạy, hãy gọi hàm ngay, khi đó
            # hàm sẽ thoát nếu chúng ta gọi quá sớm.
            _set_up_spatial_context()


    func _exit_tree():
        if spatial_context:
            # Ngắt kết nối khỏi signal discovery.
            OpenXRSpatialEntityExtension.spatial_discovery_recommended.disconnect(_on_perform_discovery)

            # Giải phóng spatial context; thao tác này sẽ dọn dẹp nó.
            OpenXRSpatialEntityExtension.free_spatial_context(spatial_context)
            spatial_context = RID()

        var openxr_interface : OpenXRInterface = XRServer.find_interface("OpenXR")
        if openxr_interface and openxr_interface.is_initialized():
            openxr_interface.session_begun.disconnect(_set_up_spatial_context)


Mỗi marker, bất kể loại nào, sẽ gồm hai thành phần:

.. list-table:: Các thành phần theo dõi marker
   :header-rows: 1

   * - Thành phần
     - Data class
     - Mô tả
   * - COMPONENT_TYPE_MARKER
     - :ref:`OpenXRSpatialComponentMarkerList<class_OpenXRSpatialComponentMarkerList>`
     - Cung cấp loại, ID (Aruco và April Tag) và/hoặc dữ liệu (QR Code) của từng marker.
   * - COMPONENT_TYPE_BOUNDED_2D
     - :ref:`OpenXRSpatialComponentBounded2DList<class_OpenXRSpatialComponentBounded2DList>`
     - Cung cấp pose trung tâm và hình chữ nhật giới hạn của từng mặt phẳng.

Chúng ta thêm phần triển khai discovery:

.. code-block:: gdscript

    ...

    var discovery_result : OpenXRFutureResult
    var entities : Dictionary[int, OpenXRMarkerTracker]

    func _on_perform_discovery(p_spatial_context):
        # Chúng ta nhận được signal này cho tất cả spatial context, vì vậy hãy thoát nếu đây không phải context của chúng ta.
        if p_spatial_context != spatial_context:
            return

        # Nếu hiện đang có kết quả discovery đang diễn ra, hãy hủy kết quả đó.
        if discovery_result:
            discovery_result.cancel_discovery()

        # Thực hiện discovery.
        discovery_result = OpenXRSpatialEntityExtension.discover_spatial_entities(spatial_context, [\
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_MARKER, \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D \
            ])

        # Chờ hoàn tất async.
        await discovery_result.completed

        var snapshot : RID = discovery_result.get_spatial_snapshot()
        if snapshot:
            # Xử lý kết quả snapshot.
            _process_snapshot(snapshot, true)

            # Và dọn dẹp snapshot.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)


    func _process_snapshot(p_snapshot, bool p_is_discovery):
        var result_data : Array

        # Tạo bản sao các thực thể hiện đã tìm thấy.
        var org_entities : PackedInt64Array
        if p_is_discovery:
            # Chỉ khi discovery, chúng ta mới kiểm tra xem có thực thể chưa được theo dõi cần dọn dẹp hay không.
            for entity_id in entities:
                org_entities.push_back(entity_id)

        # Luôn đưa dữ liệu kết quả query vào.
        var query_result_data : OpenXRSpatialQueryResultData = OpenXRSpatialQueryResultData.new()
        result_data.push_back(query_result_data)

        # Và dữ liệu của thành phần marker.
        var marker_list : OpenXRSpatialComponentMarkerList
        if p_is_discovery:
            # Chỉ khi discovery, chúng ta mới kiểm tra dữ liệu marker
            marker_list = OpenXRSpatialComponentMarkerList.new()
            result_data.push_back(marker_list)

        # Thêm dữ liệu thành phần bounded 2D.
        var bounded2d_list : OpenXRSpatialComponentBounded2DList = OpenXRSpatialComponentBounded2DList.new()
        result_data.push_back(bounded2d_list)

        if OpenXRSpatialEntityExtension.query_snapshot(p_snapshot, result_data):
            for i in query_result_data.get_entity_id_size():
                var entity_id = query_result_data.get_entity_id(i)
                var entity_state = query_result_data.get_entity_state(i)

                # Xóa thực thể khỏi danh sách ban đầu.
                if org_entities.has(entity_id):
                    org_entities.erase(entity_id)

                if entity_state == OpenXRSpatialEntityTracker.ENTITY_TRACKING_STATE_STOPPED:
                    # Chúng ta chỉ nhận được thực thể này khi thực hiện update,
                    # và khi đó chúng ta sẽ xóa marker.
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

                    # Nếu đang theo dõi, chúng ta nên query các thành phần còn lại.
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

                    # Chúng ta không đăng ký tracker cho đến khi đã thiết lập dữ liệu ban đầu.
                    if register_with_xr_server:
                        XRServer.add_tracker(entity_tracker)

        if p_is_discovery:
            # Các thực thể còn lại, chúng ta có thể xóa.
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

        # Ở đây chúng ta chỉ cần thành phần anchor.
        var snapshot : RID = OpenXRSpatialEntityExtension.update_spatial_entities(spatial_context, entity_rids, [ \
                OpenXRSpatialEntityExtension.COMPONENT_TYPE_BOUNDED_2D, \
            ])
        if snapshot:
            # Xử lý snapshot của chúng tôi.
            _process_snapshot(snapshot, false)

            # Và dọn dẹp snapshot.
            OpenXRSpatialEntityExtension.free_spatial_snapshot(snapshot)
