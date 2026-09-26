.. _doc_webxr_intro:

WebXR
=====

WebXR là một tiêu chuẩn web cho phép cung cấp trải nghiệm XR trực tiếp từ trình duyệt web mà người dùng không cần cài đặt bất kỳ thứ gì. Godot có hỗ trợ WebXR tích hợp sẵn.

.. note::

    Vì sử dụng tính năng xuất HTML, WebXR yêu cầu dùng compatibility renderer. Hiện tại Godot yêu cầu hỗ trợ multiview để kết xuất stereo, nhưng tính năng này không có trên mọi thiết bị hỗ trợ WebXR.

Thiết lập
---------

Việc thiết lập WebXR hơi khác vì ứng dụng của bạn luôn khởi động dưới dạng một trang web thông thường, không phải XR. Do đó, chúng ta định nghĩa một UI 2D trên trang chính, trong đó có một nút chuyển sang XR.

Chúng ta cần đoạn mã sau để mọi thứ hoạt động:

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node3D

    @onready var start_xr_button: Button = $EnterWebXR

    # Giao diện WebXR của chúng ta.
    var xr_interface: WebXRInterface

    # Đang chạy truy vấn is_session_supported của WebXR
    var webxr_session_query: bool = false

    # Đặt giá trị này thành true nếu muốn có một phiên AR
    var require_ar: bool = false

    # Đặt giá trị này thành true nếu muốn có tính năng hand tracking
    var enable_hand_tracking: bool = false

    # Xử lý nút Enter VR trên trình duyệt WebXR
    func _on_enter_webxr_button_pressed() -> void:
        # Cấu hình giao diện WebXR
        xr_interface.session_mode = "immersive-ar" if require_ar else "immersive-vr"
        xr_interface.requested_reference_space_types = "local-floor, local"
        xr_interface.required_features = "local-floor"
        xr_interface.optional_features = ""

        # Thêm hand-tracking nếu cần
        if enable_hand_tracking:
            xr_interface.optional_features += ", hand-tracking"

        # Khởi tạo giao diện. Thao tác này sẽ kích hoạt _on_webxr_session_started
        # hoặc _on_webxr_session_failed
        if not xr_interface.initialize():
            OS.alert("Failed to initialize WebXR")


    # Được gọi khi chúng ta đã sẵn sàng
    func _ready() -> void:
        xr_interface = XRServer.find_interface("WebXR")
        if xr_interface:
            # Kết nối các signal của chúng ta
            xr_interface.session_supported.connect(_on_webxr_session_supported)
            xr_interface.session_started.connect(_on_webxr_session_started)
            xr_interface.session_ended.connect(_on_webxr_session_ended)
            xr_interface.session_failed.connect(_on_webxr_session_failed)

           	webxr_session_query = true
        	xr_interface.is_session_supported("immersive-ar" if require_ar else "immersive-vr")
        else:
            print("WebXR is not available")


    # Xử lý việc kiểm tra xem phiên WebXR có được hỗ trợ hay không
    func _on_webxr_session_supported(session_mode: String, supported: bool) -> void:
        # Bỏ qua nếu không chạy session-query
        if not webxr_session_query:
            return

        # Xóa cờ truy vấn
        webxr_session_query = false

        # Báo cáo nếu không được hỗ trợ
        if not supported:
            OS.alert("Your web browser doesn't support " + session_mode + ". Sorry!")
            return

        # WebXR được hỗ trợ - hiển thị canvas trên trình duyệt web để vào WebVR
        start_xr_button.visible = true


    # Được gọi khi phiên WebXR đã khởi động thành công
    func _on_webxr_session_started() -> void:
        # Ẩn canvas và chuyển viewport sang XR
        start_xr_button.visible = false

        get_viewport().transparent_bg = require_ar
        get_viewport().use_xr = true


    # Được gọi khi người dùng kết thúc phiên VR immersive
    func _on_webxr_session_ended() -> void:
        # Hiển thị canvas và chuyển viewport sang non-XR
        start_xr_button.visible = true

        get_viewport().transparent_bg = false
        get_viewport().use_xr = false


    # Được gọi khi phiên VR immersive không khởi động được
    func _on_webxr_session_failed(message: String) -> void:
        OS.alert("Unable to enter VR: " + message)
        start_xr_button.visible = true


Đảm bảo signal ``button_pressed`` của nút "Enable WebXR" gọi phương thức ``_on_enter_webxr_button_pressed``.

.. note::

    Trong đoạn mã trên, chúng ta cố gắng sử dụng các reference space ``local-floor``. Reference space này giả định lối chơi trong đó chúng ta cần biết độ cao của người chơi so với sàn.

    Đối với các game trong đó người chơi ngồi trong một phương tiện, chẳng hạn như game mô phỏng bay hoặc game đua xe, reference space ``local`` có thể phù hợp hơn.


Đầu vào bộ điều khiển
---------------------

Hệ thống input trong WebXR hoạt động với một tập input cố định, che giấu phần cứng thực tế đang được sử dụng. Để cho phép mã có thể dùng được giữa ứng dụng WebXR và OpenXR, các input này được ánh xạ tới những action trùng với action map mặc định mà interface OpenXR của chúng ta sử dụng.

Có một số khác biệt nhỏ, chẳng hạn như WebXR tách touchpad và thumbstick thành các input riêng, thay vì thiết lập input primary và secondary trong action map OpenXR mặc định của chúng ta.

Các input cốt lõi có sẵn cho WebXR:


.. table::
   :widths: auto

   +------------------+---------+-----------------------------------------------------+
   | Tên              | Kiểu    | Mô tả                                               |
   +------------------+---------+-----------------------------------------------------+
   | trigger_click    | Boolean | ``true`` nếu trigger được nhấn                      |
   +------------------+---------+-----------------------------------------------------+
   | trigger          | Float   | Giá trị trigger từ 0.0 đến 1.0                      |
   +------------------+---------+-----------------------------------------------------+
   | grip_click       | Boolean | ``true`` nếu nút grip được nhấn                     |
   +------------------+---------+-----------------------------------------------------+
   | grip             | Float   | Giá trị grip từ 0.0 đến 1.0                         |
   +------------------+---------+-----------------------------------------------------+
   | touchpad_click   | Boolean | ``true`` nếu touchpad được nhấn                     |
   +------------------+---------+-----------------------------------------------------+
   | thumbstick_click | Boolean | ``true`` nếu thumbstick được nhấn                   |
   +------------------+---------+-----------------------------------------------------+
   | ax_button        | Boolean | ``true`` nếu nút A hoặc X được nhấn                 |
   +------------------+---------+-----------------------------------------------------+
   | by_button        | Boolean | ``true`` nếu nhấn nút B hoặc Y                      |
   +------------------+---------+-----------------------------------------------------+
   | touchpad_x       | Float   | Chuyển động của ngón tay trên touchpad theo hướng X |
   +------------------+---------+-----------------------------------------------------+
   | touchpad_y       | Float   | Chuyển động của ngón tay trên touchpad theo hướng Y |
   +------------------+---------+-----------------------------------------------------+
   | touchpad         | Vector2 | Dữ liệu đầu vào của touchpad dưới dạng Vector2      |
   +------------------+---------+-----------------------------------------------------+
   | thumbstick_x     | Float   | Chuyển động của thumbstick theo hướng X             |
   +------------------+---------+-----------------------------------------------------+
   | thumbstick_y     | Float   | Chuyển động của thumbstick theo hướng Y             |
   +------------------+---------+-----------------------------------------------------+
   | thumbstick       | Vector2 | Dữ liệu đầu vào của thumbstick dưới dạng Vector2    |
   +------------------+---------+-----------------------------------------------------+

WebXR cũng cung cấp các pose ``aim`` và ``grip``, lần lượt xác định một vị trí hướng về phía trước ở đầu controller và một vị trí trên tay cầm của controller.
