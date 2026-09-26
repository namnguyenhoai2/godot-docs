.. _doc_a_better_xr_start_script:

Tập lệnh khởi động XR tốt hơn
=============================

Trong :ref:`doc_setting_up_xr`, chúng ta đã giới thiệu một tập lệnh khởi động để khởi tạo thiết lập, được dùng làm tập lệnh trên node chính của chúng ta. Tập lệnh này thực hiện các bước tối thiểu cần thiết cho bất kỳ interface nào.

Khi sử dụng OpenXR, chúng ta nên thực hiện một số cải tiến ở đây. Vì vậy, chúng ta đã tạo một tập lệnh khởi động chi tiết hơn. Bạn sẽ thấy tập lệnh này được sử dụng trong các dự án demo của chúng ta.

Ngoài ra, nếu bạn đang sử dụng XR Tools (xem :ref:`doc_introducing_xr_tools`), trong đó có một phiên bản của tập lệnh này được cập nhật với một số tính năng liên quan đến XR tools.

Dưới đây, chúng ta sẽ trình bày chi tiết tập lệnh được sử dụng trong các bản demo và giải thích những phần được bổ sung.

Các signal cho tập lệnh của chúng ta
------------------------------------

Chúng ta thêm 3 signal vào tập lệnh để game có thể bổ sung logic:

- ``focus_lost`` được phát ra khi người chơi tháo headset hoặc khi người chơi vào hệ thống menu của headset.
- ``focus_gained`` được phát ra khi người chơi đeo lại headset hoặc thoát khỏi hệ thống menu và quay lại game.
- ``pose_recentered`` được phát ra khi headset yêu cầu đặt lại vị trí của người chơi.

Game của chúng ta nên phản hồi tương ứng với các signal này.

.. tabs::
  .. code-tab:: gdscript GDScript

    extends Node3D

    signal focus_lost
    signal focus_gained
    signal pose_recentered

    ...

  .. code-tab:: csharp

    using Godot;

    public partial class MyNode3D : Node3D
    {
        [Signal]
        public delegate void FocusLostEventHandler();

        [Signal]
        public delegate void FocusGainedEventHandler();

        [Signal]
        public delegate void PoseRecenteredEventHandler();

    ...


Các biến cho tập lệnh của chúng ta
----------------------------------

Chúng ta cũng thêm một vài biến mới vào tập lệnh:

- ``maximum_refresh_rate`` sẽ điều khiển refresh rate của headset nếu headset hỗ trợ tính năng này.
- ``xr_interface`` lưu tham chiếu đến XR interface của chúng ta; biến này đã tồn tại, nhưng giờ chúng ta khai báo kiểu cho nó để có toàn quyền truy cập vào API :ref:`XRInterface <class_xrinterface>`.
- ``xr_is_focussed`` sẽ được đặt thành true bất cứ khi nào game của chúng ta có focus.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    @export var maximum_refresh_rate : int = 90

    var xr_interface : OpenXRInterface
    var xr_is_focussed = false

    ...

  .. code-tab:: csharp

    ...

        [Export]
        public int MaximumRefreshRate { get; set; } = 90;

        private OpenXRInterface _xrInterface;

        private bool _xrIsFocused;

    ...

Hàm ready được cập nhật
-----------------------

Chúng ta thêm một vài phần vào hàm ready.

Nếu đang sử dụng mobile renderer hoặc forward+ renderer, chúng ta đặt ``vrs_mode`` của viewport thành ``VRS_XR``. Trên các nền tảng hỗ trợ tính năng này, thao tác đó sẽ bật foveated rendering.

Nếu đang sử dụng compatibility renderer, chúng ta kiểm tra xem các thiết lập foveated rendering của OpenXR đã được cấu hình chưa; nếu chưa, chúng ta xuất một cảnh báo. Xem :ref:`OpenXR Settings <doc_openxr_settings>` để biết thêm chi tiết.

Chúng ta kết nối một số signal sẽ được phát ra bởi :ref:`XRInterface <class_xrinterface>`. Chúng ta sẽ trình bày chi tiết hơn về các signal này khi triển khai chúng.

Chúng ta cũng thoát ứng dụng nếu không thể khởi tạo OpenXR thành công. Giờ đây, đây có thể là một lựa chọn. Nếu bạn đang tạo game mixed mode, hãy thiết lập chế độ VR của game khi thành công và thiết lập chế độ non-VR của game khi thất bại. Tuy nhiên, khi chạy một ứng dụng chỉ dành cho VR trên headset độc lập, thoát khi thất bại sẽ tốt hơn là để hệ thống bị treo.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    # Được gọi khi node lần đầu tiên đi vào scene tree.
    func _ready():
        xr_interface = XRServer.find_interface("OpenXR")
        if xr_interface and xr_interface.is_initialized():
            print("OpenXR instantiated successfully.")
            var vp : Viewport = get_viewport()

            # Bật XR trên viewport của chúng ta
            vp.use_xr = true

            # Đảm bảo v-sync được tắt, vì v-sync do OpenXR xử lý
            DisplayServer.window_set_vsync_mode(DisplayServer.VSYNC_DISABLED)

            # Bật VRS
            if RenderingServer.get_rendering_device():
                vp.vrs_mode = Viewport.VRS_XR
            elif int(ProjectSettings.get_setting("xr/openxr/foveation_level")) == 0:
                push_warning("OpenXR: Recommend setting Foveation level to High in Project Settings")

            # Kết nối các sự kiện OpenXR
            xr_interface.session_begun.connect(_on_openxr_session_begun)
            xr_interface.session_visible.connect(_on_openxr_visible_state)
            xr_interface.session_focussed.connect(_on_openxr_focused_state)
            xr_interface.session_stopping.connect(_on_openxr_stopping)
            xr_interface.pose_recentered.connect(_on_openxr_pose_recentered)
        else:
            # Không thể khởi động OpenXR.
            print("OpenXR not instantiated!")
            get_tree().quit()

    ...

  .. code-tab:: csharp

    ...

        /// <summary>
        /// Được gọi khi node lần đầu tiên đi vào scene tree.
        /// </summary>
        public override void _Ready()
        {
            _xrInterface = (OpenXRInterface)XRServer.FindInterface("OpenXR");
            if (_xrInterface != null && _xrInterface.IsInitialized())
            {
                GD.Print("OpenXR instantiated successfully.");
                var vp = GetViewport();

                // Bật XR trên viewport của chúng ta
                vp.UseXR = true;

                // Đảm bảo v-sync được tắt, vì v-sync do OpenXR xử lý
                DisplayServer.WindowSetVsyncMode(DisplayServer.VSyncMode.Disabled);

                // Bật VRS
                if (RenderingServer.GetRenderingDevice() != null)
                {
                    vp.VrsMode = Viewport.VrsModeEnum.XR;
                }
                else if ((int)ProjectSettings.GetSetting("xr/openxr/foveation_level") == 0)
                {
                    GD.PushWarning("OpenXR: Recommend setting Foveation level to High in Project Settings");
                }

                // Kết nối các sự kiện OpenXR
                _xrInterface.SessionBegun += OnOpenXRSessionBegun;
                _xrInterface.SessionVisible += OnOpenXRVisibleState;
                _xrInterface.SessionFocussed += OnOpenXRFocusedState;
                _xrInterface.SessionStopping += OnOpenXRStopping;
                _xrInterface.PoseRecentered += OnOpenXRPoseRecentered;
            }
            else
            {
                // Không thể khởi động OpenXR.
                GD.Print("OpenXR not instantiated!");
                GetTree().Quit();
            }
        }

    ...


Khi session bắt đầu
-------------------

Signal này được OpenXR phát ra khi session của chúng ta được thiết lập. Điều đó có nghĩa là headset đã hoàn tất việc thiết lập mọi thứ và sẵn sàng bắt đầu nhận nội dung từ chúng ta. Chỉ vào thời điểm này, nhiều thông tin khác nhau mới khả dụng đầy đủ.

Điều chính chúng ta thực hiện ở đây là kiểm tra refresh rate của headset. Chúng ta cũng kiểm tra các refresh rate khả dụng do XR runtime báo cáo để xác định xem có muốn đặt headset ở refresh rate cao hơn hay không.

Cuối cùng, chúng ta đồng bộ update rate của physics với update rate của headset. Theo mặc định, Godot chạy ở update rate của physics là 60 lần mỗi giây, trong khi headset chạy ở mức tối thiểu 72 và với các headset hiện đại thường lên đến 144 frame mỗi giây. Không đồng bộ update rate của physics sẽ gây giật hình vì các frame được render mà các đối tượng không di chuyển.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    # Xử lý khi session OpenXR sẵn sàng
    func _on_openxr_session_begun() -> void:
        # Lấy refresh rate được báo cáo
        var current_refresh_rate = xr_interface.get_display_refresh_rate()
        if current_refresh_rate > 0:
            print("OpenXR: Refresh rate reported as ", str(current_refresh_rate))
        else:
            print("OpenXR: No refresh rate given by XR runtime")

        # Kiểm tra xem có refresh rate tốt hơn khả dụng không
        var new_rate = current_refresh_rate
        var available_rates : Array = xr_interface.get_available_display_refresh_rates()
        if available_rates.size() == 0:
            print("OpenXR: Target does not support refresh rate extension")
        elif available_rates.size() == 1:
            # Chỉ có một lựa chọn, nên sử dụng lựa chọn đó
            new_rate = available_rates[0]
        else:
            for rate in available_rates:
                if rate > new_rate and rate <= maximum_refresh_rate:
                    new_rate = rate

        # Chúng ta có tìm thấy rate tốt hơn không?
        if current_refresh_rate != new_rate:
            print("OpenXR: Setting refresh rate to ", str(new_rate))
            xr_interface.set_display_refresh_rate(new_rate)
            current_refresh_rate = new_rate

        # Giờ hãy đồng bộ rate của physics
        Engine.physics_ticks_per_second = current_refresh_rate

    ...

  .. code-tab:: csharp

    ...

        /// <summary>
        /// Xử lý khi session OpenXR sẵn sàng
        /// </summary>
        private void OnOpenXRSessionBegun()
        {
            // Lấy refresh rate được báo cáo
            var currentRefreshRate = _xrInterface.DisplayRefreshRate;
            GD.Print(currentRefreshRate > 0.0F
                ? $"OpenXR: Refresh rate reported as {currentRefreshRate}"
                : "OpenXR: No refresh rate given by XR runtime");

            // Kiểm tra xem có refresh rate tốt hơn khả dụng không
            var newRate = currentRefreshRate;
            var availableRates = _xrInterface.GetAvailableDisplayRefreshRates();
            if (availableRates.Count == 0)
            {
                GD.Print("OpenXR: Target does not support refresh rate extension");
            }
            else if (availableRates.Count == 1)
            {
                // Chỉ có một lựa chọn, nên sử dụng lựa chọn đó
                newRate = (float)availableRates[0];
            }
            else
            {
                GD.Print("OpenXR: Available refresh rates: ", availableRates);
                foreach (float rate in availableRates)
                {
                    if (rate > newRate && rate <= MaximumRefreshRate)
                    {
                        newRate = rate;
                    }
                }
            }

            // Chúng ta có tìm thấy rate tốt hơn không?
            if (currentRefreshRate != newRate)
            {
                GD.Print($"OpenXR: Setting refresh rate to {newRate}");
                _xrInterface.DisplayRefreshRate = newRate;
                currentRefreshRate = newRate;
            }

            // Giờ hãy đồng bộ rate của physics
            Engine.PhysicsTicksPerSecond = (int)currentRefreshRate;
        }

    ...

Về trạng thái hiển thị
----------------------

Tín hiệu này được OpenXR phát ra khi game của chúng ta trở nên hiển thị nhưng không được focus. Đây là một mô tả hơi kỳ lạ trong OpenXR, nhưng về cơ bản có nghĩa là game của chúng ta vừa khởi động và sắp chuyển sang trạng thái được focus, người dùng đã mở menu hệ thống hoặc vừa tháo headset.

Khi nhận tín hiệu này, chúng ta sẽ cập nhật trạng thái focus, đổi process mode của node thành disabled để tạm dừng việc xử lý trên node này và các node con, đồng thời phát tín hiệu ``focus_lost`` của chúng ta.

Nếu bạn đã thêm script này vào root node, điều đó có nghĩa là game của bạn sẽ tự động tạm dừng khi cần. Nếu chưa, bạn có thể kết nối một method với tín hiệu để thực hiện các thay đổi bổ sung.

.. note::

  Khi game của bạn đang ở trạng thái hiển thị vì người dùng đã mở menu hệ thống, Godot vẫn tiếp tục render các frame và tính năng theo dõi đầu vẫn hoạt động, để game của bạn tiếp tục hiển thị ở chế độ nền. Tuy nhiên, tính năng theo dõi controller và bàn tay sẽ bị tắt cho đến khi người dùng thoát khỏi menu hệ thống.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    # Xử lý trạng thái hiển thị của OpenXR
    func _on_openxr_visible_state() -> void:
        # Chúng ta luôn đi qua trạng thái này khi khởi động,
        # nhưng lần thứ hai nhận được trạng thái này có nghĩa là người chơi đã tháo headset
        if xr_is_focussed:
            print("OpenXR lost focus")

            xr_is_focussed = false

            # tạm dừng game của chúng ta
            get_tree().paused = true

            emit_signal("focus_lost")

    ...

  .. code-tab:: csharp

    ...

        /// <summary>
        /// Xử lý trạng thái hiển thị của OpenXR
        /// </summary>
        private void OnOpenXRVisibleState()
        {
            // Chúng ta luôn đi qua trạng thái này khi khởi động,
            // nhưng lần thứ hai nhận được trạng thái này có nghĩa là người chơi đã tháo headset
            if (_xrIsFocused)
            {
                GD.Print("OpenXR lost focus");

                _xrIsFocused = false;

                // Tạm dừng game của chúng ta
                GetTree().Paused = true;

                EmitSignal(SignalName.FocusLost);
            }
        }

    ...

Về trạng thái được focus
------------------------

Tín hiệu này được OpenXR phát ra khi game của chúng ta nhận được focus. Điều này xảy ra khi quá trình khởi động hoàn tất, nhưng cũng có thể xảy ra khi người dùng thoát khỏi menu hệ thống hoặc đeo headset trở lại.

Cũng lưu ý rằng khi game khởi động trong lúc người dùng không đeo headset, game sẽ duy trì ở trạng thái 'visible' cho đến khi người dùng đeo headset.

.. warning::

  Vì vậy, điều quan trọng là phải giữ game ở trạng thái tạm dừng khi đang trong chế độ hiển thị. Nếu không, game sẽ tiếp tục chạy trong khi người dùng không tương tác với game. Ngoài ra, khi game trở lại chế độ được focus, tính năng theo dõi controller và bàn tay sẽ đột ngột được bật lại, điều này có thể gây ra hậu quả nghiêm trọng cho game nếu bạn không xử lý phù hợp. Hãy nhớ kiểm thử hành vi này trong game của bạn!

Trong khi xử lý tín hiệu, chúng ta sẽ cập nhật trạng thái focus, bỏ tạm dừng node và phát tín hiệu ``focus_gained`` của mình.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    # Xử lý trạng thái được focus của OpenXR
    func _on_openxr_focused_state() -> void:
        print("OpenXR gained focus")
        xr_is_focussed = true

        # bỏ tạm dừng game của chúng ta
        get_tree().paused = false

        emit_signal("focus_gained")

    ...

  .. code-tab:: csharp

    ...

        /// <summary>
        /// Xử lý trạng thái được focus của OpenXR
        /// </summary>
        private void OnOpenXRFocusedState()
        {
            GD.Print("OpenXR gained focus");
            _xrIsFocused = true;

            // Bỏ tạm dừng game của chúng ta
            GetTree().Paused = false;

            EmitSignal(SignalName.FocusGained);
        }

    ...

Về trạng thái đang dừng
-----------------------

Tín hiệu này được OpenXR phát ra khi chúng ta chuyển sang trạng thái dừng. Có một số khác biệt giữa các nền tảng khi điều này xảy ra. Trên một số nền tảng, tín hiệu này chỉ được phát ra khi game đang đóng. Nhưng trên các nền tảng khác, tín hiệu này cũng được phát ra mỗi khi người chơi tháo headset.

Hiện tại, method này chỉ là một placeholder.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    # Xử lý trạng thái đang dừng của OpenXR
    func _on_openxr_stopping() -> void:
        # Session của chúng ta đang được dừng.
        print("OpenXR is stopping")

    ...

  .. code-tab:: csharp

    ...

        /// <summary>
        /// Xử lý trạng thái đang dừng của OpenXR
        /// </summary>
        private void OnOpenXRStopping()
        {
            // Session của chúng ta đang được dừng.
            GD.Print("OpenXR is stopping");
        }

    ...


Về việc căn giữa lại pose
-------------------------

Tín hiệu này được OpenXR phát ra khi người dùng yêu cầu căn giữa lại góc nhìn. Về cơ bản, tín hiệu này cho game của bạn biết rằng người dùng hiện đang hướng mặt về phía trước và bạn nên định hướng lại người chơi để họ hướng về phía trước trong thế giới ảo.

Vì việc này phụ thuộc vào game của bạn, game cần phản hồi tương ứng.

Ở đây, tất cả những gì chúng ta làm là phát tín hiệu ``pose_recentered``. Bạn có thể kết nối với tín hiệu này và triển khai code căn giữa lại thực tế. Thông thường, chỉ cần gọi :ref:`center_on_hmd() <class_XRServer_method_center_on_hmd>` là đủ.

.. tabs::
  .. code-tab:: gdscript GDScript

    ...

    # Xử lý tín hiệu căn giữa lại pose của OpenXR
    func _on_openxr_pose_recentered() -> void:
        # Người dùng đã căn giữa lại góc nhìn, chúng ta phải phản hồi bằng cách căn giữa lại góc nhìn.
        # Điều này phụ thuộc vào phần triển khai của game.
        emit_signal("pose_recentered")

  .. code-tab:: csharp

    ...

        /// <summary>
        /// Xử lý tín hiệu căn giữa lại pose của OpenXR
        /// </summary>
        private void OnOpenXRPoseRecentered()
        {
            // Người dùng đã căn giữa lại góc nhìn, chúng ta phải phản hồi bằng cách căn giữa lại góc nhìn.
            // Điều này phụ thuộc vào phần triển khai của game.
            EmitSignal(SignalName.PoseRecentered);
        }
    }

Vậy là script của chúng ta đã hoàn tất. Script được viết để có thể tái sử dụng trong nhiều project. Chỉ cần thêm nó làm script cho node chính của bạn (và mở rộng nếu cần) hoặc thêm nó vào một node con dành riêng cho script này.
