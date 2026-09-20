.. _doc_webxr_intro:

WebXR
=====

WebXR là một tiêu chuẩn web cho phép cung cấp các trải nghiệm XR trực tiếp từ trình duyệt web mà không cần người dùng cài đặt bất kỳ thứ gì. Godot có hỗ trợ WebXR tích hợp sẵn.

.. note::

    Vì sử dụng HTML export, WebXR yêu cầu dùng compatibility renderer. Hiện tại Godot yêu cầu hỗ trợ multiview để render stereo, nhưng tính năng này không có trên tất cả các thiết bị hỗ trợ WebXR.

Thiết lập
---------

Việc thiết lập WebXR có đôi chút khác biệt vì ứng dụng của bạn luôn bắt đầu dưới dạng một trang web thông thường, không phải XR. Do đó, chúng ta định nghĩa một UI 2D trên trang chính, trong đó có một nút chuyển sang XR.

Chúng ta sẽ cần đoạn mã sau để mọi thứ hoạt động:

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node3D

    @onready var start_xr_button: Button = $EnterWebXR

    # Interface WebXR của chúng ta.
    var xr_interface: WebXRInterface

    # Có đang chạy truy vấn is_session_supported của WebXR không
    var webxr_session_query: bool = false

    # Đặt thành true nếu chúng ta muốn có một AR session
    var require_ar: bool = false

    # Đặt thành true nếu chúng ta muốn có hand tracking
    var enable_hand_tracking: bool = false

    # Xử lý nút Enter VR trên trình duyệt WebXR
    func _on_enter_webxr_button_pressed() -> void:
        # Cấu hình interface WebXR
        xr_interface.session_mode = "immersive-ar" if require_ar else "immersive-vr"
        xr_interface.requested_reference_space_types = "local-floor, local"
        xr_interface.required_features = "local-floor"
        xr_interface.optional_features = ""

        # Thêm hand-tracking nếu cần
        if enable_hand_tracking:
            xr_interface.optional_features += ", hand-tracking"

        # Khởi tạo interface. Thao tác này sẽ kích hoạt либо _on_webxr_session_started
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


    # Xử lý việc kiểm tra session được hỗ trợ bởi WebXR
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


    # Được gọi khi WebXR session đã khởi động thành công
    func _on_webxr_session_started() -> void:
        # Ẩn canvas và chuyển viewport sang XR
        start_xr_button.visible = false

        get_viewport().transparent_bg = require_ar
        get_viewport().use_xr = true


    # Được gọi khi người dùng kết thúc immersive VR session
    func _on_webxr_session_ended() -> void:
        # Hiển thị canvas và chuyển viewport sang non-XR
        start_xr_button.visible = true

        get_viewport().transparent_bg = false
        get_viewport().use_xr = false


    # Được gọi khi immersive VR session không thể khởi động
    func _on_webxr_session_failed(message: String) -> void:
        OS.alert("Unable to enter VR: " + message)
        start_xr_button.visible = true


Đảm bảo signal ``button_pressed`` của nút "Enable WebXR" gọi phương thức ``_on_enter_webxr_button_pressed``.

.. note::

    Trong đoạn mã trên, chúng ta cố gắng sử dụng các reference space ``local-floor``. Các reference space này giả định gameplay trong đó chúng ta cần biết chiều cao của người chơi so với mặt sàn.

    Đối với các game trong đó người chơi ngồi bên trong một phương tiện, chẳng hạn như game mô phỏng bay hoặc đua xe, reference space ``local`` có thể phù hợp hơn.


Input của controller
--------------------

Hệ thống input trong WebXR hoạt động dựa trên một tập hợp input cố định, giúp che giấu phần cứng thực tế đang được sử dụng. Để cho phép code có thể chuyển đổi giữa một ứng dụng WebXR và OpenXR, các input này được ánh xạ tới các action trùng với action map mặc định được interface OpenXR của chúng ta sử dụng.

Có một số khác biệt nhỏ, chẳng hạn WebXR tách touchpad và thumbstick thành các input riêng biệt, thay vì thiết lập input primary và secondary trong action map OpenXR mặc định của chúng ta.

Các input cốt lõi có sẵn cho WebXR:


.. table::
   :widths: auto

   +-----------------------------+-----------+---------------------------------------------------------+
   |  Name                       | Type      | Description                                             |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  trigger_click              | Boolean   | ``true`` if the trigger is pressed                      |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  trigger                    | Float     | Trigger value between 0.0 and 1.0                       |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  grip_click                 | Boolean   | ``true`` if the grip button is pressed                  |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  grip                       | Float     | Grip value between 0.0 and 1.0                          |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  touchpad_click             | Boolean   | ``true`` if the touchpad is pressed                     |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  thumbstick_click           | Boolean   | ``true`` if the thumbstick is pressed                   |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  ax_button                  | Boolean   | ``true`` if the A or X button is pressed                |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  by_button                  | Boolean   | ``true`` if the B or Y button is pressed                |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  touchpad_x                 | Float     | Finger movement on the touchpad in the X direction      |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  touchpad_y                 | Float     | Finger movement on the touchpad in the Y direction      |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  touchpad                   | Vector2   | Touchpad input as a Vector2                             |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  thumbstick_x               | Float     | Thumbstick movement in the X direction                  |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  thumbstick_y               | Float     | Thumbstick movement in the Y direction                  |
   +-----------------------------+-----------+---------------------------------------------------------+
   |  thumbstick                 | Vector2   | Thumbstick input as a Vector2                           |
   +-----------------------------+-----------+---------------------------------------------------------+

WebXR cũng cung cấp các pose ``aim`` và ``grip``, lần lượt xác định một vị trí hướng về phía trước ở đầu controller và một vị trí trên grip của controller.
