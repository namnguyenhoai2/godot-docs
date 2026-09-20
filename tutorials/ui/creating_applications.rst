.. _doc_creating_applications:

Tạo ứng dụng
============

Godot có một hệ thống UI tích hợp phong phú, và kích thước bản phân phối nhỏ có thể khiến nó trở thành một lựa chọn thay thế phù hợp cho các framework như Electron hoặc Qt.

Trang này cung cấp hướng dẫn tạo các ứng dụng không phải game bằng Godot, cũng như hướng dẫn thực hiện các tác vụ phổ biến để cải thiện khả năng tích hợp với desktop.

.. note::

    Godot trước hết và chủ yếu là một game engine. Điều này có nghĩa là việc tạo ứng dụng bằng Godot là sản phẩm phụ của tập tính năng, chứ không phải trọng tâm phát triển chính của nó.

.. seealso::

    Hãy xem `Material Maker <https://github.com/RodZill4/material-maker>`__ và `Pixelorama <https://github.com/Orama-Interactive/Pixelorama>`__ để tham khảo các ví dụ về ứng dụng mã nguồn mở được tạo bằng Godot.

Thực hiện các tác vụ phổ biến
-----------------------------

Tạo nhiều cửa sổ
^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows, macOS và Linux (chỉ X11/XWayland, không hỗ trợ native Wayland).*

Có thể tạo các cửa sổ bổ sung bằng node :ref:`class_Window`. Các cửa sổ có thể được di chuyển, thay đổi kích thước, thu nhỏ và đóng độc lập với cửa sổ ứng dụng chính.

Tuy nhiên, nếu bạn đóng cửa sổ chính, tất cả các cửa sổ khác cũng sẽ bị đóng vì việc đóng cửa sổ chính sẽ kết thúc process. Bạn có thể tránh điều này bằng cách thu nhỏ cửa sổ chính, đặt thuộc tính :ref:`unfocusable <class_Window_property_unfocusable>` của nó thành ``true`` (để ẩn cửa sổ khỏi taskbar và trình chuyển đổi cửa sổ), sau đó tạo các node Window bổ sung ngay khi khởi động. Trong trường hợp này, hãy nhớ cung cấp một cách khác để thoát ứng dụng, chẳng hạn như :ref:`tray icon <doc_creating_applications_tray_icon>`.

Giới hạn kích thước cửa sổ
^^^^^^^^^^^^^^^^^^^^^^^^^^

Hầu hết ứng dụng chỉ có thể render chính xác từ một kích thước cửa sổ tối thiểu nhất định. Với các trường hợp sử dụng cụ thể hơn, bạn cũng có thể muốn buộc kích thước cửa sổ tối đa.

Có thể áp dụng giới hạn kích thước bằng các thuộc tính :ref:`min_size <class_Window_property_min_size>` và :ref:`max_size <class_Window_property_max_size>` trên node Window. Hãy nhớ nhân các giới hạn kích thước này theo scale factor của ứng dụng (xem :ref:`doc_creating_applications_scaling_to_hidpi_displays` để biết chi tiết).

.. tip::

    Xin nhắc lại, bạn có thể lấy node Window gốc để thiết lập các thuộc tính trên đó bằng :ref:`get_window() <class_Node_method_get_window>` trên bất kỳ Node nào.

Sử dụng hộp thoại tệp native
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows, macOS, Linux và Android.*

Theo mặc định, Godot sử dụng implementation :ref:`class_FileDialog` của riêng mình cho các hộp thoại tệp. Tuy nhiên, bạn có thể sử dụng hộp thoại tệp native của hệ điều hành. Người dùng thường ưu tiên cách này vì các hộp thoại tệp native tích hợp tốt hơn với môi trường desktop và mang lại trải nghiệm quen thuộc hơn.

Bạn có thể chọn sử dụng hộp thoại tệp native bằng cách bật thuộc tính :ref:`use_native_dialog <class_FileDialog_property_use_native_dialog>` trên node FileDialog. Việc này phải được thực hiện trên từng node FileDialog được sử dụng trong project, vì không có thiết lập project nào để kiểm soát hành vi này trên toàn cục.

.. figure:: img/creating_applications_native_file_dialog.webp
   :align: center
   :alt: Comparison between standard FileDialog (left) and native file dialog (right) on macOS

   Comparison between standard FileDialog (left) and native file dialog (right) on macOS

.. note::

    Xem :ref:`property description <class_FileDialog_property_use_native_dialog>` để biết chi tiết về khả năng hỗ trợ trên các platform.

    Ngoài ra, trên macOS, hộp thoại tệp native không được hỗ trợ khi game embedding được bật trong editor. Để kiểm tra chức năng này khi chạy project, hãy đảm bảo bạn tắt game embedding bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

.. _doc_creating_applications_tray_icon:

Tạo icon trong system tray
^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows và macOS.*

Bạn có thể tạo một hoặc nhiều icon trong system tray (còn gọi là notification area) bằng node :ref:`class_StatusIndicator`. Ngoài tooltip, node này có thể được gán một node :ref:`class_PopupMenu`, để hiển thị dropdown khi nhấp vào icon.

StatusIndicator cũng có signal :ref:`pressed <class_StatusIndicator_signal_pressed>`, được phát khi icon được nhấp. Hãy sử dụng signal này để thực hiện một hành động mà không hiển thị dropdown, hoặc thực hiện các hành động khác nhau tùy thuộc vào nút chuột được nhấn.

Sau khi tạo tray icon, bạn cũng có thể muốn triển khai hành vi "thu nhỏ khi đóng". Điều này có nghĩa là khi người dùng cố đóng ứng dụng bằng nút X của window manager, ứng dụng sẽ được thu nhỏ vào tray thay vì đóng. Để thực hiện việc này, hãy gắn script sau vào một *scene* :ref:`Autoload <doc_singletons_autoload>` có StatusIndicator làm node gốc:

::

    extends StatusIndicator

    # Tắt hành vi này khi chạy từ editor với game embedding,
    # vì nó không hoạt động tốt cùng nhau.
    var tray_icon_supported = (
            DisplayServer.has_feature(DisplayServer.FEATURE_STATUS_INDICATOR)
            and not Engine.is_embedded_in_editor()
        )


    func _ready():
        visible = false

        if tray_icon_supported:
            get_tree().auto_accept_quit = false
            get_window().focus_entered.connect(
                    func():
                        # Ẩn tray icon khi cửa sổ nhận focus,
                        # nghĩa là cửa sổ đã được khôi phục từ trạng thái thu nhỏ.
                        visible = false
                )
            pressed.connect(
                    func(_mouse_button, _position):
                        # Khôi phục ứng dụng khi tray icon được nhấp.
                        get_window().mode = Window.MODE_WINDOWED
                )


    func _notification(what):
        if not tray_icon_supported:
            return

        match what:
            NOTIFICATION_WM_CLOSE_REQUEST:
                get_window().mode = Window.MODE_MINIMIZED
                # Hiển thị tray icon.
                visible = true


Xem :ref:`doc_handling_quit_requests` để biết chi tiết về cách ghi đè hành vi khi người dùng cố đóng ứng dụng. Việc xử lý trường hợp này rất quan trọng khi người dùng có các thay đổi chưa được lưu, nhằm tránh mất dữ liệu.

.. note::

    Khi có nhiều node StatusIndicator, thứ tự của chúng trong system tray được xác định bởi thứ tự chúng được thêm vào scene tree.

Sử dụng global menu
^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên macOS.*

Trên macOS, ứng dụng có thể sử dụng global menu bar của hệ thống thay vì hiển thị menu bar bên trong cửa sổ ứng dụng. Trong Godot, tính năng này còn được gọi là *native menu*.

.. figure:: img/creating_applications_native_menu.webp
   :align: center
   :alt: Comparison between standard MenuBar (left), MenuBar with native popups (middle), and native menu (right) on macOS

   Comparison between standard MenuBar (left), MenuBar with native popups (middle), and native menu (right) on macOS

Godot hỗ trợ tạo menu thông qua node :ref:`class_MenuBar`, node này hiển thị các node con :ref:`class_PopupMenu` dưới dạng menu. Bạn có thể bật hỗ trợ global menu trên một MenuBar cụ thể bằng cách bật thuộc tính của nó
:ref:`prefer_global_menu <class_MenuBar_property_prefer_global_menu>` property
trong inspector. Trên macOS, thao tác này sẽ khiến node MenuBar biến mất và không chiếm không gian, đồng thời các menu của nó sẽ được hiển thị trong global menu bar của hệ thống. Nếu thuộc tính này bị tắt, node MenuBar sẽ hiển thị các menu bên trong cửa sổ ứng dụng như bình thường, nhưng native popup vẫn được sử dụng khi hệ điều hành hỗ trợ.

.. note::

    App menu (với tên project được in đậm), cũng như :menu:`Window` và
    :menu:`Help` menus are always present on macOS. You should not add these
    vào global menu theo cách thủ công.

    Trong Godot 4.6 trở lên, bạn có thể thêm các mục mới vào những menu này bằng cách thay đổi thuộc tính :ref:`system_menu_id <class_PopupMenu_property_system_menu_id>` trên node PopupMenu. Bạn có thể chọn giữa **Application Menu** (menu đầu tiên có tên ứng dụng được in đậm), **Window Menu**, **Help Menu** và **Dock** (hiển thị khi nhấp chuột phải vào icon trong Dock). Các mục menu tiêu chuẩn vốn đã có trong những menu đó sẽ được giữ lại:

    .. figure:: img/creating_applications_native_menu_window.webp
       :align: center
       :alt: Custom options added to the system Window menu on macOS

       Custom options added to the system Window menu on macOS

Một project có thể có nhiều node MenuBar. Nếu nhiều node MenuBar bật thuộc tính **Prefer Global Menu**, các tùy chọn menu sẽ được thêm tại index được xác định bởi thuộc tính **Start Index** khi node MenuBar được thêm vào scene tree. Điều này cho phép đặt các menu theo ngữ cảnh ở cuối menu bar, để các tùy chọn menu đầu tiên vẫn giữ nguyên vị trí khi menu bar bổ sung được thêm vào hoặc xóa đi.

Đối với các trường hợp sử dụng nâng cao hơn, bạn cũng có thể sử dụng trực tiếp singleton :ref:`class_NativeMenu` mà không cần dùng node MenuBar.

.. note::

    Tích hợp global menu không được hỗ trợ khi game embedding được bật trong editor. Để kiểm tra chức năng này khi chạy project, hãy đảm bảo bạn tắt game embedding bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

Sử dụng client-side decorations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên macOS.*

Nhiều ứng dụng hiện đại sử dụng *client-side decorations* (CSD) thay vì dựa vào window manager của hệ điều hành để vẽ title bar và viền cửa sổ (server-side decorations). Điều này cho phép tùy chỉnh giao diện nhiều hơn và tích hợp tốt hơn với UI của ứng dụng.

Hiện tại, Godot chỉ hỗ trợ client-side decorations trên macOS. Bạn có thể sử dụng tính năng này bằng cách bật
:ref:`display/window/size/extend_to_title <class_ProjectSettings_property_display/window/size/extend_to_title>`
project setting.

.. figure:: img/creating_applications_client_side_decoration.webp
   :align: center
   :alt: Comparison between standard window decorations (top) and client-side decorations (bottom) on macOS

   Comparison between standard window decorations (top) and client-side decorations (bottom) on macOS

Sau khi bật client-side decorations, viền cửa sổ sẽ không còn hiển thị, đồng thời các nút thu nhỏ/phóng to/đóng sẽ hiển thị dưới dạng overlay trên ứng dụng. Bạn cần đảm bảo ứng dụng có đủ khoảng trống ở phía trên để các nút hiển thị thoải mái, đồng thời hiển thị tiêu đề cửa sổ bằng node Label hoặc node tương tự.

Để điều chỉnh UI theo điều kiện dựa trên việc client-side decorations có được bật hay không, hãy sử dụng :ref:`DisplayServer.has_feature <class_DisplayServer_method_has_feature>` và cũng kiểm tra giá trị hiện tại của
:ref:`Window.extend_to_title <class_Window_property_extend_to_title>`
(đây là giá trị mà project setting thay đổi):

::

    func _ready():
        if DisplayServer.has_feature(FEATURE_EXTEND_TO_TITLE) and get_window().extend_to_title:
            # Điều chỉnh UI cho client-side decorations (ở đây có thể dùng một node MarginContainer
            #  hữu ích). Đồng thời đặt tiêu đề cửa sổ sẽ được hiển thị
            # theo tiêu đề cửa sổ native.
            $WindowTitle.visible = true
            $WindowTitle.text = get_window().title
            if OS.is_debug_build():
                $WindowTitle.text += " (DEBUG)"

Để định vị chính xác tiêu đề cửa sổ, hãy cân nhắc sử dụng
:ref:`DisplayServer.window_get_safe_title_margins() <class_DisplayServer_method_window_get_safe_title_margins>`
trả về một Vector3 trong đó ``x`` là lề trái, ``y`` là lề phải (sẽ tăng khi hệ thống sử dụng kiểu chữ từ phải sang trái), còn ``z`` là chiều cao. Ngoài ra, bạn có thể gọi
:ref:`DisplayServer.window_set_window_buttons_offset() <class_DisplayServer_method_window_set_window_buttons_offset>`
để điều chỉnh vị trí của các nút đóng/thu nhỏ/phóng to (thường là để căn giữa chúng theo chiều dọc).

.. figure:: img/creating_applications_client_side_decoration_margins.webp
    :align: center
    :alt: Safe title margins when using client-side decorations on macOS

    Safe title margins when using client-side decorations on macOS

.. note::

    Trên macOS, client-side decorations không được hỗ trợ khi game embedding được bật trong editor. Để kiểm tra chức năng này khi chạy project, hãy đảm bảo bạn tắt game embedding bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

Hiển thị trạng thái tiến trình trên taskbar/Dock
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows và macOS.*

Ứng dụng có thể báo cáo trạng thái tiến trình cho hệ điều hành, trạng thái này có thể được hiển thị trên thanh tác vụ hoặc biểu tượng Dock. Trạng thái này gồm một trạng thái (đang hoạt động, tạm dừng, lỗi) và phần trăm hoàn thành. Có thể dùng tính năng này để hiển thị tiến trình khi người dùng không tập trung vào ứng dụng.

.. figure:: img/creating_applications_progress_reporting.webp
    :align: center
    :alt: Progress reporting in the Dock on macOS

    Progress reporting in the Dock on macOS

Điều này thường được thực hiện bằng cách đồng bộ tiến trình của node :ref:`class_ProgressBar` với tiến trình được báo cáo cho hệ điều hành:

::

    func set_progress(value, indeterminate = false):
        $ProgressBar.value = value
        $ProgressBar.indeterminate = indeterminate

        if $ProgressBar.indeterminate:
            get_window().set_taskbar_progress_state(DisplayServer.PROGRESS_STATE_INDETERMINATE)
        else:
            get_window().set_taskbar_progress_state(DisplayServer.PROGRESS_STATE_NORMAL)

        # Giá trị tiến trình trên thanh tác vụ phải nằm trong khoảng từ `0.0` đến `1.0`
        # (các giá trị nằm ngoài khoảng này sẽ bị giới hạn).
        # ProgressBar cung cấp thuộc tính `ratio`, biểu thị tiến trình hiện tại của nó
        # dưới dạng một giá trị từ `0.0` đến `1.0`.
        get_window().set_taskbar_progress_value($ProgressBar.ratio)

Có một số trạng thái tiến trình: không có tiến trình (ẩn thanh tiến trình), không xác định, bình thường, tạm dừng, lỗi. Hãy xem tài liệu tham chiếu lớp để biết chi tiết.

Bạn cũng có thể sử dụng
:ref:`Window.request_attention() <class_Window_method_request_attention>`
để làm cửa sổ nhấp nháy trên thanh tác vụ (hoặc nảy lên trong Dock trên macOS). Ví dụ, có thể dùng tính năng này để thu hút sự chú ý của người dùng sau khi hoàn tất một thao tác dài.

.. note::

    Không hỗ trợ báo cáo tiến trình khi bật game embedding trong editor. Để kiểm thử chức năng này khi chạy project, hãy đảm bảo bạn tắt game embedding bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

Gửi thông báo trên desktop
^^^^^^^^^^^^^^^^^^^^^^^^^^

Hiện tại Godot không hỗ trợ native cho việc gửi thông báo trên desktop.

Tuy nhiên, trên macOS và Linux, bạn có thể lần lượt sử dụng các tiện ích dòng lệnh ``osascript`` và ``notify-send`` để gửi thông báo trên desktop:

::

    func send_notification(title, message):
        var app_name = ProjectSettings.get_setting("application/config/name")
        if app_name.is_empty():
            app_name = "Unnamed Project"

        if OS.has_feature("macos") and not OS.is_sandboxed():
            # Note that this will not work if the project is exported in sandbox mode
            # (ví dụ: cho Mac App Store).
            OS.execute("osascript", [
                    "-e",
                    'display notification \\"%s\\" with title \\"%s\\" subtitle \\"%s\\"' % [
                        message,
                        app_name,
                        title,
                    ]
                ])
        elif OS.has_feature("linuxbsd"):
            OS.execute("notify-send", ["--app-name", app_name, title, message])

    func _ready():
        send_notification("Success", "Operation completed successfully.")

Đáng tiếc là Windows không có tính năng tương đương được cung cấp sẵn.

Ghi nhớ vị trí và kích thước cửa sổ qua các phiên
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Godot không có hỗ trợ tích hợp sẵn để ghi nhớ vị trí và kích thước cửa sổ qua các phiên, nhưng bạn có thể tự triển khai bằng script. Một ví dụ cơ bản hỗ trợ thiết lập nhiều màn hình sẽ là một
:ref:`Autoload <doc_singletons_autoload>` with this script:

::

    extends Node

    # Sử dụng một tệp cấu hình riêng cho trạng thái cửa sổ.
    # Bằng cách này, các tệp cấu hình khác của ứng dụng sẽ không bị
    # đụng đến và có thể được đưa vào version control mà không tạo ra các diff không cần thiết
    # .
    const CONFIG_WINDOW_PATH = "user://window.ini"

    var config_file = ConfigFile.new()


    func _enter_tree():
        config_file.load(CONFIG_WINDOW_PATH)

        # Không khôi phục trạng thái cửa sổ trước đó nếu chạy từ editor
        # khi game embedding đang được bật.
        if not Engine.is_embedded_in_editor():
            var window_screen = config_file.get_value("main", "screen", -1)
            if window_screen is int:
                get_window().current_screen = window_screen

            var window_mode = config_file.get_value("main", "mode", -1)
            if window_mode is Window.Mode:
                get_window().mode = window_mode

            var window_position = config_file.get_value("main", "position", -1)
            if window_position is Vector2i:
                get_window().position = window_position

            var window_size = config_file.get_value("main", "size", -1)
            if window_size is Vector2i:
                get_window().size = window_size


    func _exit_tree():
        # Lưu trạng thái cửa sổ hiện tại khi ứng dụng thoát bình thường.
        # Trong thực tế, bạn cũng nên lưu thông tin này
        # định kỳ (ví dụ: bằng một node Timer), để trạng thái cửa sổ có thể được
        # khôi phục sau khi xảy ra sự cố hoặc khi bị kết thúc từ bên ngoài.
        config_file.set_value("main", "screen", get_window().current_screen)
        config_file.set_value("main", "mode", get_window().mode)
        config_file.set_value("main", "position", get_window().position)
        config_file.set_value("main", "size", get_window().size)
        config_file.save(CONFIG_WINDOW_PATH)

.. note::

    Ví dụ trên chỉ theo dõi vị trí của cửa sổ chính. Trong các ứng dụng tạo nhiều cửa sổ, bạn sẽ cần lưu và tải riêng vị trí và kích thước của từng cửa sổ.

Ẩn cửa sổ trong màn hình splash
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Đối với một số ứng dụng, bạn có thể muốn ẩn splash screen để thay vào đó tự vẽ splash screen tùy chỉnh có thanh tiến trình (hoặc thậm chí không dùng splash screen nếu ứng dụng khởi động nhanh).

Godot không hỗ trợ native cho việc ẩn cửa sổ trong splash screen, nhưng bạn có thể thực hiện điều này bằng cách sử dụng một cửa sổ trong suốt rất nhỏ trong project settings, sau đó thay đổi kích thước cửa sổ và tắt transparency khi scene chính được tải.

Để thực hiện việc này, cần cấu hình project settings như sau:

- :ref:`application/boot_splash/bg_color <class_ProjectSettings_property_application/boot_splash/bg_color>` được đặt thành màu đen trong suốt (RGBA: 0, 0, 0, 0). - Tắt :ref:`application/boot_splash/show_image <class_ProjectSettings_property_application/boot_splash/show_image>`. - Bật :ref:`display/window/size/borderless <class_ProjectSettings_property_display/window/size/borderless>`. - Bật :ref:`display/window/size/no_focus <class_ProjectSettings_property_display/window/size/no_focus>`. - :ref:`display/window/size/window_width_override <class_ProjectSettings_property_display/window/size/window_width_override>` được đặt thành ``1``. - :ref:`display/window/size/window_height_override <class_ProjectSettings_property_display/window/size/window_height_override>` được đặt thành ``1``. - Bật :ref:`display/window/per_pixel_transparency/allowed <class_ProjectSettings_property_display/window/per_pixel_transparency/allowed>`. - Bật :ref:`display/window/size/transparent <class_ProjectSettings_property_display/window/size/transparent>`. - Bật :ref:`rendering/viewport/transparent_background <class_ProjectSettings_property_rendering/viewport/transparent_background>`.

Có thể sử dụng script này làm một :ref:`Autoload <doc_singletons_autoload>` để khôi phục các thiết lập ban đầu sau khi splash screen hiển thị xong:

::

    extends Node


    func _enter_tree():
        # Chờ một frame được render trước khi khôi phục các thuộc tính cửa sổ.
        # Nếu không, các thuộc tính sẽ được khôi phục quá sớm và viền cửa sổ
        # sẽ xuất hiện quanh một cửa sổ trong suốt.
        await get_tree().process_frame

        get_viewport().transparent_bg = false
        get_window().transparent = false
        get_window().borderless = false
        get_window().size = Vector2i(1152, 648)

Hiển thị ứng dụng dưới dạng overlay
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bạn có thể hiển thị cửa sổ ứng dụng dưới dạng overlay luôn nằm trên các cửa sổ khác. Tính năng này hữu ích cho các ứng dụng như widget hoặc trình giám sát hệ thống.

Để thực hiện việc này, hãy bật **tất cả** các project settings sau:

- :ref:`display/window/size/borderless <class_ProjectSettings_property_display/window/size/borderless>` - :ref:`display/window/per_pixel_transparency/allowed <class_ProjectSettings_property_display/window/per_pixel_transparency/allowed>` - :ref:`display/window/size/transparent <class_ProjectSettings_property_display/window/size/transparent>` - :ref:`rendering/viewport/transparent_background <class_ProjectSettings_property_rendering/viewport/transparent_background>` - :ref:`display/window/size/always_on_top <class_ProjectSettings_property_display/window/size/always_on_top>` - :ref:`display/window/size/no_focus <class_ProjectSettings_property_display/window/size/no_focus>`

  - Điều này ngăn overlay nhận dữ liệu nhập từ bàn phím, đồng thời ẩn overlay khỏi thanh tác vụ và trình chuyển đổi tác vụ. Overlay vẫn có thể nhận dữ liệu nhập từ chuột (xem bên dưới).

Hãy nhớ định vị và thay đổi kích thước cửa sổ bằng script, vì người dùng thường không thể di chuyển cửa sổ không có viền.

Để cho phép dữ liệu nhập từ chuột đi xuyên qua đến ứng dụng nền, hãy đặt thuộc tính :ref:`mouse_passthrough <class_Window_property_mouse_passthrough>` thành ``true`` trên Window được vẽ dưới dạng overlay. Bạn cũng có thể định nghĩa một polygon trong
:ref:`mouse_passthrough_polygon <class_Window_property_mouse_passthrough_polygon>`,
để một số khu vực nhất định vẫn có thể chặn dữ liệu nhập từ chuột trên overlay.

Ngoài ra, bạn có thể muốn đặt
:ref:`exclude_from_capture <class_Window_property_exclude_from_capture>`
thuộc tính thành ``true`` để ngăn overlay xuất hiện trong ảnh chụp màn hình hoặc bản ghi. Hint này chỉ được triển khai trên Windows và macOS, đồng thời hoạt động theo nguyên tắc nỗ lực tối đa, vì vậy không nên dùng nó làm biện pháp bảo mật tuyệt đối hoặc DRM.

.. note::

    Không hỗ trợ hiển thị dưới dạng overlay khi bật game embedding trong editor. Để kiểm thử chức năng này khi chạy project, hãy đảm bảo bạn tắt game embedding bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn :menu:`Embed Game on Next Play`.

    Ngoài ra, hãy lưu ý rằng overlay không thể hiển thị bên trên một ứng dụng khác nếu ứng dụng đó sử dụng chế độ toàn màn hình độc quyền. Thay vào đó, phải sử dụng chế độ toàn màn hình không viền để overlay hiển thị được.

    Ngoài ra còn có `known issues <https://github.com/godotengine/godot/issues/76167>`__ liên quan đến việc hiển thị cửa sổ trong suốt trên Windows với thiết lập GPU lai (chẳng hạn như NVIDIA Optimus). Việc chuyển renderer có thể giúp giải quyết sự cố.

    Trên Linux với X11, transparency sẽ không hoạt động nếu người dùng đã tắt compositing trong thiết lập của window manager.

.. _doc_creating_applications_scaling_to_hidpi_displays:

Tỷ lệ theo các màn hình hiDPI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các màn hình hiện đại khác nhau đáng kể về mật độ pixel, do đó thường cần một hệ số tỷ lệ khác để đảm bảo các phần tử UI dễ đọc. Hệ số tỷ lệ cũng có thể được cung cấp dưới dạng điều chỉnh thủ công cho người dùng, để ứng dụng vẫn thuận tiện khi sử dụng.

Hỗ trợ nhiều độ phân giải của Godot rất phù hợp để thay đổi tỷ lệ của ứng dụng khi được cấu hình đúng cách. Hãy làm theo hướng dẫn trong
:ref:`non-game application section of the Multiple resolutions documentation <doc_multiple_resolutions_non_game_application>`.

.. note::

    Hiện tại Godot chỉ hỗ trợ đọc hệ số tỷ lệ màn hình từ thiết lập của OS trên macOS, Android và Linux (chỉ Wayland). Trên Linux (X11) và Windows, bạn sẽ cần cung cấp tùy chọn thay đổi tỷ lệ thủ công để người dùng điều chỉnh tỷ lệ UI theo nhu cầu.

Tích hợp trình đọc màn hình
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Trình đọc màn hình cho phép người khiếm thị sử dụng ứng dụng bằng cách đọc các phần tử UI và cung cấp các điều khiển điều hướng. Màn hình chữ nổi Braille là một phương pháp khác cũng dựa vào thông tin accessibility để hoạt động đúng cách.

Godot tự động bật hỗ trợ trình đọc màn hình nếu phát hiện một trình đọc màn hình đang chạy. Bạn có thể cấu hình tính năng này trong Project Settings bằng :ref:`accessibility/general/accessibility_support <class_ProjectSettings_property_accessibility/general/accessibility_support>` để tắt trong những trường hợp không mong muốn. Tính năng này cũng có thể được buộc bật, điều này hữu ích khi sử dụng các công cụ debug accessibility mà Godot không nhận diện là trình đọc màn hình.

Godot sử dụng thư viện `AccessKit <https://accesskit.dev/>`__ để tích hợp trình đọc màn hình.

.. tip::

    Vì hỗ trợ trình đọc màn hình sử dụng chính ứng dụng trình đọc màn hình để phát âm thanh (thay vì project Godot), nên tính năng này vẫn hoạt động ngay cả khi audio driver được đặt thành ``Dummy`` trong project settings như mô tả bên dưới.

Bạn nên kiểm thử ứng dụng với các trình đọc màn hình phổ biến trên những nền tảng mục tiêu để đảm bảo trải nghiệm tốt cho người dùng khiếm thị. Ví dụ gồm `NVDA <https://www.nvaccess.org/download/>`__ trên Windows, `VoiceOver <https://www.apple.com/accessibility/features/?vision>`__ trên macOS và `Orca <https://help.gnome.org/orca/>`__ trên Linux.

Để hỗ trợ trình đọc màn hình đạt mức khả dụng tốt, cần thực hiện một lượng công việc đáng kể. Bạn cần định nghĩa các nhãn accessibility bằng các thuộc tính :ref:`Control.accessibility_name <class_Control_property_accessibility_name>` và :ref:`Control.accessibility_description <class_Control_property_accessibility_description>`, đồng thời đảm bảo UI có thứ tự logic khi được trình đọc màn hình đọc.

.. seealso::

    Xem thêm :ref:`doc_text_to_speech` để biết chức năng chuyển văn bản thành giọng nói (text-to-speech) tách biệt với trình đọc màn hình.

Project settings được khuyến nghị
---------------------------------

Tích hợp desktop
^^^^^^^^^^^^^^^^

Để ứng dụng tích hợp tốt hơn với môi trường desktop, bạn có thể đặt các project settings như sau:

- Bật :ref:`application/config/use_custom_user_dir <class_ProjectSettings_property_application/config/use_custom_user_dir>` và đặt :ref:`application/config/custom_user_dir_name <class_ProjectSettings_property_application/config/custom_user_dir_name>` thành tên phù hợp cho ứng dụng của bạn. Điều này đảm bảo các thiết lập và tệp của người dùng được lưu trong một thư mục riêng thay vì
  :ref:`default Godot folder <doc_data_paths_accessing_persistent_user_data>`.
  Theo quy ước, bạn nên sử dụng chữ thường cho Windows (ví dụ: ``Application Name``) và kebab-case (ví dụ: ``application-name``) trên macOS và Linux.

- Cấu hình các biểu tượng native phù hợp với hướng dẫn thiết kế của hệ điều hành bằng :ref:`application/config/windows_native_icon <class_ProjectSettings_property_application/config/windows_native_icon>` (ở định dạng ICO) và
  :ref:`application/config/macos_native_icon <class_ProjectSettings_property_application/config/macos_native_icon>`
  (ở định dạng ICNS). Theo mặc định, Godot sẽ tự động tạo các biểu tượng native dựa trên biểu tượng của project, nhưng cách này không phải lúc nào cũng tối ưu.

  - Trên Windows, việc sử dụng tệp ICO được thiết kế thủ công cho phép bạn dùng các biểu tượng khác nhau ở những độ phân giải khác nhau. Bạn có thể dùng cách này để tạo thiết kế đặc biệt ở độ phân giải thấp nhằm cải thiện khả năng đọc.

  - macOS có `app icon guidelines <https://developer.apple.com/design/human-interface-guidelines/app-icons/>`__ khác biệt đáng kể so với các nền tảng khác. Việc sử dụng thiết kế biểu tượng native phù hợp sẽ giúp ứng dụng hòa hợp hơn với môi trường desktop của nó.

- Tắt
  :ref:`display/window/subwindows/embed_subwindows <class_ProjectSettings_property_display/window/subwindows/embed_subwindows>`,
  để các cửa sổ bổ sung sử dụng giao diện của hệ điều hành và được xem là các cửa sổ native của hệ điều hành.

Hiệu năng
^^^^^^^^^

Dưới đây là một số cài đặt project bạn có thể sử dụng để giảm mức sử dụng CPU, GPU và bộ nhớ:

- Sử dụng renderer Compatibility nếu bạn không cần các tính năng chỉ có trong Forward+ hoặc Mobile. Renderer Compatibility có yêu cầu phần cứng thấp hơn và thường khởi chạy nhanh hơn, nên đây là lựa chọn phù hợp hơn cho các ứng dụng. Việc tạo các cửa sổ mới cũng nhanh hơn với renderer này.

- Bật :ref:`application/run/low_processor_mode <class_ProjectSettings_property_application/run/low_processor_mode>` để giảm mức sử dụng CPU và GPU. Khi đó, project chỉ render một frame nếu có thứ gì đó trên màn hình thay đổi.

  - Lưu ý rằng trong một số trường hợp, project phải redraw liên tục (ví dụ: khi một animation hoặc shader sử dụng ``TIME`` đang hiển thị). Nếu diễn ra trong thời gian dài, việc này sẽ tiêu thụ nhiều điện năng, làm giảm thời lượng pin và tăng tiếng ồn của quạt. Để khắc phục sự cố project redraw liên tục, bạn có thể bật :menu:`Debug > Debug Canvas Item Redraws` ở đầu editor, sau đó chạy project. Các khu vực được redraw sẽ được tô đỏ trong một giây. Bạn có thể điều chỉnh màu và thời lượng đánh dấu bằng các cài đặt project :ref:`debug/canvas_items/debug_redraw_time <class_ProjectSettings_property_debug/canvas_items/debug_redraw_time>` và :ref:`debug/canvas_items/debug_redraw_color <class_ProjectSettings_property_debug/canvas_items/debug_redraw_color>`.

  - Tốc độ khung hình tối đa mà ứng dụng có thể render được xác định bởi
    :ref:`application/run/low_processor_mode_sleep_usec <class_ProjectSettings_property_application/run/low_processor_mode_sleep_usec>`.
    Giá trị này được biểu thị bằng microsecond trên mỗi frame, vì vậy có thể lấy FPS tối đa bằng công thức ``1000000.0 / sleep_usec``. Theo mặc định, giá trị này được đặt thành ``6900``, tương ứng với tối đa khoảng 145 FPS. Bạn có thể tăng giá trị này để tiếp tục giảm mức sử dụng CPU và GPU, nhưng trải nghiệm sẽ kém mượt hơn.

- Tắt :ref:`display/window/energy_saving/keep_screen_on <class_ProjectSettings_property_display/window/energy_saving/keep_screen_on>` để màn hình có thể tắt theo cài đặt nguồn của hệ điều hành khi ứng dụng ở trạng thái idle. Hành vi này thường không được mong muốn trong game (ví dụ: khi xem các đoạn cutscene), nhưng với ứng dụng, chúng ta muốn màn hình tắt để tiết kiệm điện khi người dùng không chủ động sử dụng ứng dụng.

- Đặt :ref:`audio/driver/driver <class_ProjectSettings_property_audio/driver/driver>` thành ``Dummy`` *(phân biệt chữ hoa chữ thường)* nếu ứng dụng của bạn không yêu cầu đầu ra hoặc đầu vào âm thanh. Điều này ngăn audio server khởi động, giúp tiết kiệm một phần tài nguyên CPU và bộ nhớ. Đồng thời, ứng dụng sẽ không xuất hiện trong danh sách các ứng dụng đang phát âm thanh của audio mixer trong hệ điều hành. Trên macOS, điều này cũng đảm bảo ứng dụng không ngăn thiết bị chuyển sang chế độ ngủ.

- Đặt :ref:`physics/2d/physics_engine <class_ProjectSettings_property_physics/2d/physics_engine>` và :ref:`physics/3d/physics_engine <class_ProjectSettings_property_physics/3d/physics_engine>` thành ``Dummy`` nếu ứng dụng của bạn không yêu cầu mô phỏng vật lý (bao gồm cả việc chọn đối tượng). Điều này ngăn các physics server khởi động, giúp tiết kiệm tài nguyên CPU và bộ nhớ. Cách này cũng cho phép
  :ref:`engine compilation configuration editor <doc_engine_compilation_configuration_editor>`
  tự động phát hiện rằng project không sử dụng vật lý.

- Hãy cân nhắc đặt :ref:`display/window/vsync/vsync_mode <class_ProjectSettings_property_display/window/vsync/vsync_mode>` thành **Disabled** để giảm input lag. Điều này đặc biệt hữu ích trong các project nhạy cảm với độ trễ, chẳng hạn như ứng dụng vẽ. Việc này có thể làm tăng mức tiêu thụ điện năng và gây xé hình, vì vậy bạn nên cung cấp tùy chọn để người dùng bật hoặc tắt V-Sync khi cần.

Hãy xem `Material Maker <https://github.com/RodZill4/material-maker>`__ và `Pixelorama <https://github.com/Orama-Interactive/Pixelorama>`__ để tham khảo các ví dụ về ứng dụng mã nguồn mở được tạo bằng Godot.

Mobile
^^^^^^

Khi thiết kế ứng dụng cho các nền tảng mobile, bạn có thể bật một số cài đặt để cải thiện khả năng sử dụng:

**Android:**

- Bật :ref:`input_devices/pointing/android/enable_long_press_as_right_click <class_ProjectSettings_property_input_devices/pointing/android/enable_long_press_as_right_click>` để cho phép người dùng thực hiện các thao tác nhấp chuột phải bằng cử chỉ nhấn giữ.

- Bật :ref:`input_devices/pointing/android/enable_pan_and_scale_gestures <class_ProjectSettings_property_input_devices/pointing/android/enable_pan_and_scale_gestures>` để cho phép người dùng di chuyển và phóng to, thu nhỏ bằng các cử chỉ chạm. Tùy chọn này sẽ mô phỏng
  :ref:`class_InputEventPanGesture` and :ref:`class_InputEventMagnifyGesture`
  các event, có thể được xử lý trong code của project và thường được phát ra bởi trackpad của laptop.

- Tắt :menu:`Screen > Immersive Mode` trong export preset Android để hiển thị status bar và navigation bar của hệ thống khi ứng dụng đang hoạt động. Ngoài ra, bật :menu:`Screen > Edge to Edge` để làm cho status bar và các biểu tượng điều hướng trong suốt, đồng thời vẽ chúng phía trên ứng dụng. Nếu làm vậy, hãy đảm bảo ứng dụng chừa đủ không gian cho status bar và các biểu tượng điều hướng. Bạn có thể sử dụng
  :ref:`DisplayServer.get_display_safe_area <class_DisplayServer_method_get_display_safe_area>`
  và :ref:`DisplayServer.get_display_cutouts <class_DisplayServer_method_get_display_cutouts>` để truy vấn khu vực mà ứng dụng có thể vẽ một cách an toàn.

**iOS:**

- Tắt :ref:`display/window/ios/hide_home_indicator <class_ProjectSettings_property_display/window/ios/hide_home_indicator>` để hiển thị home indicator phía trên ứng dụng.

- Tắt :ref:`display/window/ios/hide_status_bar <class_ProjectSettings_property_display/window/ios/hide_status_bar>` để giữ status bar hiển thị khi ứng dụng đang hoạt động.

- Tắt :ref:`display/window/ios/suppress_ui_gesture <class_ProjectSettings_property_display/window/ios/suppress_ui_gesture>` để cho phép các cử chỉ UI hoạt động ngay lập tức mà không yêu cầu thực hiện hai lần.

Thêm unit test
--------------

Trong một ứng dụng, việc có một thiết lập `unit testing <https://en.wikipedia.org/wiki/Unit_testing>`__ thường mang lại nhiều giá trị hơn so với game. Thiết lập này có thể được dùng để tự động phát hiện regression, điều thường dễ thực hiện hơn trong bối cảnh ứng dụng, nơi logic có thể được tách riêng một cách rõ ràng.

GDScript không có framework unit testing tích hợp, nhưng cộng đồng đã duy trì một số plugin unit testing:

- `Gut <https://github.com/bitwes/Gut>`__ - `GdUnit4 <https://github.com/godot-gdunit-labs/gdUnit4>`__ (cũng hỗ trợ C#)

Với C# và GDExtension (C++, Rust, v.v.), bạn có thể sử dụng các framework testing tiêu chuẩn như NUnit hoặc `doctest <https://github.com/doctest/doctest>`__.

Tối ưu kích thước bản phân phối
-------------------------------

Vì các ứng dụng không phải game thường không sử dụng những phần lớn của engine, chẳng hạn như chức năng âm thanh hoặc 3D, bạn có thể compile một export template được tối ưu để giảm kích thước tệp. Điều này cũng cải thiện thời gian khởi động, đặc biệt trên nền tảng web, nơi kích thước binary liên quan trực tiếp đến tốc độ khởi tạo.

Mức giảm kích thước thường đáng kể (so với kích thước của project), vì ứng dụng chứa ít asset lớn hơn so với game. Xem :ref:`doc_optimizing_for_size` để biết thêm thông tin về cách thực hiện.

Tạo bản phân phối dạng một executable duy nhất
----------------------------------------------

Theo mặc định, Godot tạo một tệp PCK chứa dữ liệu project bên cạnh executable. Điều này có nghĩa là nếu executable được di chuyển mà không đồng thời di chuyển tệp PCK, ứng dụng sẽ không chạy. Đây không phải là cách lý tưởng cho các ứng dụng, vốn ngày càng được phân phối dưới dạng một tệp executable duy nhất.

Để làm cho ứng dụng hoàn toàn tự chứa trong một executable duy nhất, bạn có thể bật **Embed PCK** trong các tùy chọn export preset. Tùy chọn này sẽ nhúng dữ liệu PCK vào executable, nhờ đó bạn có thể di chuyển ứng dụng mà không làm ứng dụng bị lỗi. Điều này cũng cho phép chạy ứng dụng trực tiếp từ một kho lưu trữ ZIP mà không cần giải nén trước.

.. note::

    Việc nhúng PCK có giới hạn kích thước tùy theo nền tảng. Các ứng dụng rất lớn (vài GB) có thể không sử dụng được tính năng này trên mọi nền tảng. Hãy xem tài liệu export dành cho nền tảng mục tiêu để biết thêm chi tiết.

Tạo ứng dụng portable
---------------------

Một ứng dụng được gọi là *portable* khi có thể chạy mà không cần cài đặt và khi cấu hình của ứng dụng hoàn toàn tự chứa trong thư mục mà ứng dụng được giải nén vào. Điều này cho phép đặt các tệp ứng dụng trên USB hoặc thiết bị tương tự, rồi chạy ứng dụng trên nhiều máy khác nhau mà không cần trải qua quy trình cài đặt.

The Godot editor's own :ref:`self-contained mode <doc_data_paths_self_contained_mode>` currently can't be used within projects. However, you can still choose to save your own configuration files to the folder containing the executable as follows:

::

    var config_path = OS.get_executable_path().get_base_dir().path_join("config.ini")
    # Sau đó, sử dụng `config_path` để lưu/tải các tệp cấu hình bằng ConfigFile hoặc công cụ tương tự.

Bạn có thể muốn cho phép bật hoặc tắt portable mode vì tùy chọn này không phải lúc nào cũng được mong muốn. Thông thường, bạn sẽ phát hiện sự hiện diện của một tệp cụ thể trong thư mục của executable (ví dụ: tệp có tên ``portable.txt``), và chỉ sử dụng thư mục của executable để lưu cấu hình nếu tệp đó tồn tại.

.. warning::

    Hãy nhớ rằng cách này chỉ hoạt động nếu ứng dụng được giải nén vào một vị trí có thể ghi. Nếu executable được chạy từ một vị trí chỉ đọc, chẳng hạn như ``C:\Program Files`` trên Windows, sẽ xảy ra lỗi quyền truy cập.

Tạo installer
-------------

Trong khi game thường được cài đặt thông qua các launcher như Steam hoặc được tải xuống dưới dạng ZIP, ứng dụng thường được phân phối dưới dạng installer để tích hợp tốt hơn với desktop. Installer có thể thực hiện các thao tác như thêm shortcut vào Start Menu hoặc desktop, thiết lập liên kết tệp và nhiều thao tác khác. Installer cũng có thể được chạy tự động thông qua command line, khiến chúng phù hợp hơn với môi trường doanh nghiệp.

Godot không tích hợp sẵn tính năng tạo installer cho các project đã export. Tuy nhiên, bạn vẫn có thể tạo installer của riêng mình bằng các công cụ của bên thứ ba.

Dưới đây là danh sách chưa đầy đủ các công cụ có thể dùng để tạo trình cài đặt:

- **Windows:** `Inno Setup <https://jrsoftware.org/isinfo.php>`__, `NSIS <https://nsis.sourceforge.io/Main_Page>`__

  - Nếu bạn có chứng chỉ ký mã (code signing certificate), hãy nhớ ký *cả* trình cài đặt và tệp thực thi của project. Để thực hiện việc này,
    :ref:`sign the exported project executable <doc_exporting_for_windows_code_signing>`,
    hãy tạo trình cài đặt chứa project đã export, sau đó ký thủ công trình cài đặt mà bạn vừa tạo.

- **macOS:** `create-dmg <https://github.com/create-dmg/create-dmg>`__

- **Linux:** `Flatpak <https://docs.flatpak.org/en/latest/first-build.html>`__

  - Có một `Godot BaseApp <https://github.com/flathub/org.godotengine.Godot.BaseApp>`__ có thể dùng làm cơ sở để tạo các gói Flatpak cho project Godot. Xem `the Pixelorama Flatpak <https://github.com/flathub/com.orama_interactive.Pixelorama>`__ để biết ví dụ về một Flatpak sử dụng BaseApp này.

Tài nguyên
----------

Các trang này đề cập đến những tác vụ thường được thực hiện trong các ứng dụng không phải game:

- :ref:`doc_runtime_loading_and_saving` - :ref:`doc_http_request_class` - :ref:`class_ConfigFile` (dùng để lưu tùy chọn của người dùng)
