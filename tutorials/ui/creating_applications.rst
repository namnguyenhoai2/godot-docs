.. _doc_creating_applications:

Tạo ứng dụng
============

Godot tích hợp sẵn một hệ thống UI phong phú, và kích thước bản phân phối nhỏ giúp nó trở thành một lựa chọn phù hợp thay thế cho các framework như Electron hoặc Qt.

Trang này cung cấp các hướng dẫn về cách tạo ứng dụng không phải trò chơi bằng Godot, cũng như hướng dẫn thực hiện các tác vụ phổ biến để cải thiện khả năng tích hợp với máy tính để bàn.

.. note::

    Trước hết, Godot là một game engine. Điều này có nghĩa là việc tạo ứng dụng bằng Godot là sản phẩm phụ từ tập tính năng của nó, chứ không phải trọng tâm phát triển chính.

.. seealso::

    Hãy xem `Material Maker <https://github.com/RodZill4/material-maker>`__ và `Pixelorama <https://github.com/Orama-Interactive/Pixelorama>`__ để tham khảo các ứng dụng mã nguồn mở được tạo bằng Godot.

Thực hiện các tác vụ phổ biến
-----------------------------

Tạo nhiều cửa sổ
^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows, macOS và Linux (chỉ X11/XWayland, không hỗ trợ ở chế độ Wayland nguyên bản).*

Có thể tạo các cửa sổ bổ sung bằng cách sử dụng node :ref:`class_Window`. Các cửa sổ có thể được di chuyển, thay đổi kích thước, thu nhỏ và đóng độc lập với cửa sổ ứng dụng chính.

Tuy nhiên, nếu bạn đóng cửa sổ chính, tất cả các cửa sổ khác cũng sẽ bị đóng vì việc đóng cửa sổ chính sẽ kết thúc process. Bạn có thể tránh điều này bằng cách thu nhỏ cửa sổ chính, đặt thuộc tính :ref:`unfocusable <class_Window_property_unfocusable>` của nó thành ``true`` (để ẩn cửa sổ khỏi thanh tác vụ và trình chuyển đổi tác vụ), sau đó tạo ngay các node Window bổ sung khi khởi động. Trong trường hợp này, hãy nhớ cung cấp một cách khác để thoát ứng dụng, chẳng hạn như :ref:`biểu tượng khay hệ thống <doc_creating_applications_tray_icon>`.

Giới hạn kích thước cửa sổ
^^^^^^^^^^^^^^^^^^^^^^^^^^

Hầu hết ứng dụng chỉ có thể kết xuất chính xác từ một kích thước cửa sổ tối thiểu nhất định. Với các trường hợp sử dụng cụ thể hơn, bạn cũng có thể muốn buộc kích thước cửa sổ tối đa.

Có thể áp dụng giới hạn kích thước bằng cách sử dụng các thuộc tính :ref:`min_size <class_Window_property_min_size>` và :ref:`max_size <class_Window_property_max_size>` trên một node Window. Hãy nhớ nhân các giới hạn kích thước này theo scale factor của ứng dụng (xem :ref:`doc_creating_applications_scaling_to_hidpi_displays` để biết chi tiết).

.. tip::

    Xin nhắc lại, bạn có thể lấy node Window gốc để đặt các thuộc tính trên đó bằng cách sử dụng :ref:`get_window() <class_Node_method_get_window>` trên bất kỳ Node nào.

Sử dụng hộp thoại tệp nguyên bản
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows, macOS, Linux và Android.*

Theo mặc định, Godot sử dụng implementation :ref:`class_FileDialog` riêng cho các hộp thoại tệp. Tuy nhiên, bạn có thể sử dụng hộp thoại tệp nguyên bản của hệ điều hành. Người dùng thường ưu tiên cách này vì hộp thoại tệp nguyên bản tích hợp tốt hơn với môi trường desktop và mang lại trải nghiệm quen thuộc hơn.

Bạn có thể bật hộp thoại tệp nguyên bản bằng cách bật thuộc tính :ref:`use_native_dialog <class_FileDialog_property_use_native_dialog>` trên node FileDialog. Việc này phải được thực hiện trên từng node FileDialog được sử dụng trong project, vì không có thiết lập project nào để kiểm soát hành vi này trên toàn cục.

.. figure:: img/creating_applications_native_file_dialog.webp
   :align: center
   :alt: So sánh giữa FileDialog tiêu chuẩn (bên trái) và hộp thoại tệp nguyên bản (bên phải) trên macOS

   So sánh giữa FileDialog tiêu chuẩn (bên trái) và hộp thoại tệp nguyên bản (bên phải) trên macOS

.. note::

    Xem :ref:`mô tả thuộc tính <class_FileDialog_property_use_native_dialog>` để biết chi tiết về hỗ trợ nền tảng.

    Ngoài ra, trên macOS, hộp thoại tệp nguyên bản không được hỗ trợ khi tính năng nhúng game được bật trong editor. Để kiểm tra chức năng này khi chạy project, hãy đảm bảo bạn tắt tính năng nhúng game bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

.. _doc_creating_applications_tray_icon:

Tạo biểu tượng trong khay hệ thống
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows và macOS.*

Bạn có thể tạo một hoặc nhiều biểu tượng trong khay hệ thống (còn gọi là vùng thông báo) bằng cách sử dụng một node :ref:`class_StatusIndicator`. Ngoài tooltip, node này có thể được gán một node :ref:`class_PopupMenu` để hiển thị menu thả xuống khi nhấp vào biểu tượng.

StatusIndicator cũng có một signal :ref:`pressed <class_StatusIndicator_signal_pressed>` được phát khi biểu tượng được nhấp. Sử dụng signal này để thực hiện một hành động mà không hiển thị menu thả xuống, hoặc thực hiện các hành động khác nhau tùy thuộc vào nút chuột được nhấn.

Sau khi tạo biểu tượng khay, bạn cũng có thể muốn triển khai hành vi "thu nhỏ khi đóng". Điều này có nghĩa là khi người dùng cố đóng ứng dụng bằng nút X của window manager, ứng dụng sẽ được thu nhỏ vào khay thay vì đóng. Để thực hiện, hãy gắn script này vào một scene :ref:`Autoload <doc_singletons_autoload>` *scene* với StatusIndicator làm node gốc:

.. code-block::

    extends StatusIndicator

    # Tắt hành vi này khi chạy từ editor với tính năng nhúng game,
    # vì tính năng này không hoạt động tốt cùng nhau.
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
                        # Ẩn biểu tượng khay khi cửa sổ nhận focus,
                        # điều này có nghĩa là cửa sổ đã được khôi phục từ trạng thái thu nhỏ.
                        visible = false
                )
            pressed.connect(
                    func(_mouse_button, _position):
                        # Khôi phục ứng dụng khi nhấp vào biểu tượng khay.
                        get_window().mode = Window.MODE_WINDOWED
                )


    func _notification(what):
        if not tray_icon_supported:
            return

        match what:
            NOTIFICATION_WM_CLOSE_REQUEST:
                get_window().mode = Window.MODE_MINIMIZED
                # Hiển thị biểu tượng khay.
                visible = true


Xem :ref:`doc_handling_quit_requests` để biết chi tiết về cách ghi đè hành vi khi người dùng cố đóng ứng dụng. Điều này rất quan trọng khi người dùng có các thay đổi chưa được lưu, nhằm tránh mất dữ liệu.

.. note::

    Khi có nhiều node StatusIndicator, thứ tự của chúng trong khay hệ thống được xác định bởi thứ tự chúng được thêm vào scene tree.

Sử dụng menu toàn cục
^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên macOS.*

Trên macOS, ứng dụng có thể sử dụng thanh menu toàn cục của hệ thống thay vì hiển thị thanh menu bên trong cửa sổ ứng dụng. Trong Godot, tính năng này còn được gọi là *menu nguyên bản*.

.. figure:: img/creating_applications_native_menu.webp
   :align: center
   :alt: So sánh giữa MenuBar tiêu chuẩn (bên trái), MenuBar với popup nguyên bản (ở giữa) và menu nguyên bản (bên phải) trên macOS

   So sánh giữa MenuBar tiêu chuẩn (bên trái), MenuBar với popup nguyên bản (ở giữa) và menu nguyên bản (bên phải) trên macOS

Godot hỗ trợ tạo menu thông qua node :ref:`class_MenuBar`, node này hiển thị các node con :ref:`class_PopupMenu` dưới dạng menu. Bạn có thể bật hỗ trợ menu toàn cục trên một node MenuBar cụ thể bằng cách bật
Thuộc tính :ref:`prefer_global_menu <class_MenuBar_property_prefer_global_menu>` trong inspector. Trên macOS, thuộc tính này sẽ khiến node MenuBar biến mất và không chiếm không gian, đồng thời các menu của nó sẽ được hiển thị trên thanh menu toàn cục của hệ thống. Nếu tắt thuộc tính này, node MenuBar sẽ hiển thị các menu bên trong cửa sổ ứng dụng như bình thường, nhưng các popup native vẫn được sử dụng khi hệ điều hành hỗ trợ.

.. note::

    Menu ứng dụng (với tên dự án được in đậm), cùng với :menu:`Window` và
    các menu :menu:`Help` luôn hiện diện trên macOS. Bạn không nên thêm các menu này vào menu toàn cục theo cách thủ công.

    Trong Godot 4.6 trở lên, bạn có thể thêm các mục mới vào những menu này bằng cách thay đổi thuộc tính :ref:`system_menu_id <class_PopupMenu_property_system_menu_id>` trên node PopupMenu. Bạn có thể chọn giữa **Application Menu** (menu đầu tiên có tên ứng dụng được in đậm), **Window Menu**, **Help Menu** và **Dock** (hiển thị khi nhấp chuột phải vào biểu tượng trong Dock). Các mục menu tiêu chuẩn vốn đã có trong những menu đó sẽ được giữ lại:

    .. figure:: img/creating_applications_native_menu_window.webp
       :align: center
       :alt: Các tùy chọn tùy chỉnh được thêm vào menu Window của hệ thống trên macOS

       Các tùy chọn tùy chỉnh được thêm vào menu Window của hệ thống trên macOS

Một dự án có thể có nhiều node MenuBar. Nếu nhiều node MenuBar bật thuộc tính **Prefer Global Menu**, các tùy chọn menu sẽ được thêm tại chỉ mục được xác định bởi thuộc tính **Start Index** khi node MenuBar được thêm vào scene tree. Điều này cho phép đặt các menu theo ngữ cảnh ở cuối thanh menu, để các tùy chọn menu đầu tiên vẫn giữ nguyên vị trí khi thanh menu bổ sung được thêm vào hoặc xóa đi.

Đối với các trường hợp sử dụng nâng cao hơn, bạn cũng có thể sử dụng trực tiếp singleton :ref:`class_NativeMenu` mà không cần node MenuBar.

.. note::

    Tích hợp menu toàn cục không được hỗ trợ khi bật tính năng nhúng game trong editor. Để kiểm thử chức năng này khi chạy dự án, hãy đảm bảo bạn tắt tính năng nhúng game bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

Sử dụng client-side decorations
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên macOS.*

Nhiều ứng dụng hiện đại sử dụng *client-side decorations* (CSD) thay vì dựa vào window manager của hệ điều hành để vẽ thanh tiêu đề và viền cửa sổ (server-side decorations). Điều này cho phép tùy chỉnh giao diện linh hoạt hơn và tích hợp tốt hơn với UI của ứng dụng.

Hiện tại Godot chỉ hỗ trợ client-side decorations trên macOS. Bạn có thể sử dụng tính năng này bằng cách bật
cài đặt dự án :ref:`display/window/size/extend_to_title <class_ProjectSettings_property_display/window/size/extend_to_title>`.

.. figure:: img/creating_applications_client_side_decoration.webp
   :align: center
   :alt: So sánh giữa decorations cửa sổ tiêu chuẩn (trên) và client-side decorations (dưới) trên macOS

   So sánh giữa decorations cửa sổ tiêu chuẩn (trên) và client-side decorations (dưới) trên macOS

Sau khi bật client-side decorations, viền cửa sổ sẽ không còn hiển thị, còn các nút thu nhỏ/phóng to/đóng sẽ hiển thị dưới dạng lớp phủ trên ứng dụng. Bạn cần đảm bảo ứng dụng chừa đủ khoảng cách ở phía trên để các nút hiển thị thoải mái, đồng thời hiển thị tiêu đề cửa sổ bằng node Label hoặc thành phần tương tự.

Để điều chỉnh UI có điều kiện theo việc client-side decorations có được bật hay không, hãy sử dụng :ref:`DisplayServer.has_feature <class_DisplayServer_method_has_feature>` và đồng thời kiểm tra giá trị hiện tại của
:ref:`Window.extend_to_title <class_Window_property_extend_to_title>` (đây là giá trị mà cài đặt dự án thay đổi):

.. code-block::

    func _ready():
        if DisplayServer.has_feature(FEATURE_EXTEND_TO_TITLE) and get_window().extend_to_title:
            # Điều chỉnh UI cho client-side decorations (node MarginContainer có thể hữu ích ở đây).
            # Đồng thời đặt tiêu đề cửa sổ để hiển thị
            # theo tiêu đề cửa sổ native.
            $WindowTitle.visible = true
            $WindowTitle.text = get_window().title
            if OS.is_debug_build():
                $WindowTitle.text += " (DEBUG)"

Để định vị chính xác tiêu đề cửa sổ, hãy cân nhắc sử dụng
:ref:`DisplayServer.window_get_safe_title_margins() <class_DisplayServer_method_window_get_safe_title_margins>` trả về một Vector3, trong đó ``x`` là lề trái, ``y`` là lề phải (sẽ tăng khi hệ thống sử dụng kiểu chữ từ phải sang trái), còn ``z`` là chiều cao. Ngoài ra, bạn có thể gọi
:ref:`DisplayServer.window_set_window_buttons_offset() <class_DisplayServer_method_window_set_window_buttons_offset>` để điều chỉnh vị trí của các nút đóng/thu nhỏ/phóng to (thường là để căn giữa chúng theo chiều dọc).

.. figure:: img/creating_applications_client_side_decoration_margins.webp
    :align: center
    :alt: Lề tiêu đề an toàn khi sử dụng client-side decorations trên macOS

    Lề tiêu đề an toàn khi sử dụng client-side decorations trên macOS

.. note::

    Trên macOS, client-side decorations không được hỗ trợ khi bật tính năng nhúng game trong editor. Để kiểm thử chức năng này khi chạy dự án, hãy đảm bảo bạn tắt tính năng nhúng game bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

Hiển thị trạng thái tiến trình trên taskbar/Dock
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

*Tính năng này chỉ được hỗ trợ trên Windows và macOS.*

Ứng dụng có thể báo cáo trạng thái tiến trình cho hệ điều hành, trạng thái này có thể được hiển thị trên taskbar hoặc biểu tượng Dock. Trạng thái này bao gồm một trạng thái (đang hoạt động, tạm dừng, lỗi) và phần trăm hoàn thành. Bạn có thể dùng tính năng này để hiển thị tiến trình khi người dùng không tập trung vào ứng dụng.

.. figure:: img/creating_applications_progress_reporting.webp
    :align: center
    :alt: Báo cáo tiến trình trong Dock trên macOS

    Báo cáo tiến trình trong Dock trên macOS

Điều này thường được thực hiện bằng cách đồng bộ tiến trình của node :ref:`class_ProgressBar` với tiến trình được báo cáo cho hệ điều hành:

.. code-block::

    func set_progress(value, indeterminate = false):
        $ProgressBar.value = value
        $ProgressBar.indeterminate = indeterminate

        if $ProgressBar.indeterminate:
            get_window().set_taskbar_progress_state(DisplayServer.PROGRESS_STATE_INDETERMINATE)
        else:
            get_window().set_taskbar_progress_state(DisplayServer.PROGRESS_STATE_NORMAL)

        # Giá trị tiến trình trên taskbar phải nằm giữa `0.0` và `1.0`
        # (các giá trị nằm ngoài phạm vi này sẽ bị giới hạn vào phạm vi).
        # ProgressBar cung cấp thuộc tính `ratio` biểu thị tiến trình hiện tại của nó
        # dưới dạng một giá trị nằm giữa `0.0` và `1.0`.
        get_window().set_taskbar_progress_value($ProgressBar.ratio)

Có một số trạng thái tiến trình: không có tiến trình (ẩn thanh tiến trình), không xác định, bình thường, tạm dừng, lỗi. Hãy xem tài liệu tham chiếu lớp để biết chi tiết.

Bạn cũng có thể sử dụng
:ref:`Window.request_attention() <class_Window_method_request_attention>` để làm cửa sổ nhấp nháy trên taskbar (hoặc nảy lên trong Dock trên macOS). Ví dụ, có thể dùng cách này để thu hút sự chú ý của người dùng sau khi hoàn tất một thao tác dài.

.. note::

    Tính năng báo cáo tiến trình không được hỗ trợ khi bật game embedding trong editor. Để kiểm tra chức năng này khi chạy project, hãy đảm bảo bạn tắt game embedding bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn
    :menu:`Embed Game on Next Play`.

Gửi thông báo trên desktop
^^^^^^^^^^^^^^^^^^^^^^^^^^

Hiện tại Godot chưa hỗ trợ native việc gửi thông báo trên desktop.

Tuy nhiên, trên macOS và Linux, bạn có thể lần lượt sử dụng các tiện ích dòng lệnh ``osascript`` và ``notify-send`` để gửi thông báo trên desktop:

.. code-block::

    func send_notification(title, message):
        var app_name = ProjectSettings.get_setting("application/config/name")
        if app_name.is_empty():
            app_name = "Unnamed Project"

        if OS.has_feature("macos") and not OS.is_sandboxed():
            # Lưu ý rằng cách này sẽ không hoạt động nếu project được export ở chế độ sandbox
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

Đáng tiếc là trên Windows không có giải pháp tương đương được cung cấp sẵn.

Ghi nhớ vị trí và kích thước cửa sổ giữa các phiên
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Godot không có hỗ trợ tích hợp sẵn cho việc ghi nhớ vị trí và kích thước cửa sổ giữa các phiên, nhưng bạn có thể tự triển khai bằng một script. Một ví dụ cơ bản hỗ trợ thiết lập nhiều màn hình sẽ là một
:ref:`Autoload <doc_singletons_autoload>` với script sau:

.. code-block::

    extends Node

    # Sử dụng một file cấu hình riêng cho trạng thái cửa sổ.
    # Bằng cách này, các file cấu hình khác của ứng dụng sẽ được giữ
    # nguyên và có thể đưa vào version control mà không tạo ra các diff không cần thiết
    # được tạo ra.
    const CONFIG_WINDOW_PATH = "user://window.ini"

    var config_file = ConfigFile.new()


    func _enter_tree():
        config_file.load(CONFIG_WINDOW_PATH)

        # Không khôi phục trạng thái cửa sổ trước đó nếu chạy từ editor
        # khi đã bật game embedding.
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
        # Lưu trạng thái cửa sổ hiện tại khi ứng dụng được thoát bình thường.
        # Trong tình huống thực tế, bạn cũng nên lưu thông tin này
        # định kỳ (ví dụ: bằng một node Timer), để trạng thái cửa sổ có thể được
        # khôi phục sau sự cố hoặc khi bị kết thúc từ bên ngoài.
        config_file.set_value("main", "screen", get_window().current_screen)
        config_file.set_value("main", "mode", get_window().mode)
        config_file.set_value("main", "position", get_window().position)
        config_file.set_value("main", "size", get_window().size)
        config_file.save(CONFIG_WINDOW_PATH)

.. note::

    Ví dụ trên chỉ theo dõi vị trí của cửa sổ chính. Trong các ứng dụng tạo nhiều cửa sổ, bạn sẽ cần lưu và tải riêng vị trí và kích thước của từng cửa sổ.

Ẩn cửa sổ trong khi hiển thị splash screen
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Đối với một số ứng dụng, bạn có thể muốn ẩn splash screen để thay vào đó vẽ splash screen tùy chỉnh có thanh tiến trình (hoặc hoàn toàn không hiển thị splash screen nếu ứng dụng khởi động nhanh).

Godot không có hỗ trợ native cho việc ẩn cửa sổ trong khi hiển thị splash screen, nhưng bạn có thể thực hiện điều này bằng cách sử dụng một cửa sổ trong suốt rất nhỏ trong project settings, sau đó thay đổi kích thước cửa sổ và tắt transparency khi scene chính được tải.

Để thực hiện việc này, hãy cấu hình project settings như sau:

- :ref:`application/boot_splash/bg_color <class_ProjectSettings_property_application/boot_splash/bg_color>` đặt thành màu đen trong suốt (RGBA: 0, 0, 0, 0).
- :ref:`application/boot_splash/show_image <class_ProjectSettings_property_application/boot_splash/show_image>` tắt.
- :ref:`display/window/size/borderless <class_ProjectSettings_property_display/window/size/borderless>` bật.
- :ref:`display/window/size/no_focus <class_ProjectSettings_property_display/window/size/no_focus>` bật.
- :ref:`display/window/size/window_width_override <class_ProjectSettings_property_display/window/size/window_width_override>` đặt thành ``1``.
- :ref:`display/window/size/window_height_override <class_ProjectSettings_property_display/window/size/window_height_override>` đặt thành ``1``.
- :ref:`display/window/per_pixel_transparency/allowed <class_ProjectSettings_property_display/window/per_pixel_transparency/allowed>` bật.
- :ref:`display/window/size/transparent <class_ProjectSettings_property_display/window/size/transparent>` bật.
- :ref:`rendering/viewport/transparent_background <class_ProjectSettings_property_rendering/viewport/transparent_background>` bật.

Có thể sử dụng script này làm một :ref:`Autoload <doc_singletons_autoload>` để khôi phục các thiết lập ban đầu sau khi hiển thị xong splash screen:

.. code-block::

    extends Node


    func _enter_tree():
        # Chờ một frame được render trước khi khôi phục các thuộc tính của cửa sổ.
        # Nếu không, các thuộc tính sẽ được khôi phục quá sớm và viền cửa sổ
        # sẽ xuất hiện xung quanh cửa sổ trong suốt.
        await get_tree().process_frame

        get_viewport().transparent_bg = false
        get_window().transparent = false
        get_window().borderless = false
        get_window().size = Vector2i(1152, 648)

Hiển thị ứng dụng dưới dạng overlay
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bạn có thể hiển thị cửa sổ ứng dụng dưới dạng overlay luôn nằm trên các cửa sổ khác. Điều này hữu ích cho các ứng dụng như widget hoặc trình giám sát hệ thống.

Để thực hiện việc này, hãy bật **tất cả** các thiết lập project sau:

- :ref:`display/window/size/borderless <class_ProjectSettings_property_display/window/size/borderless>`
- :ref:`display/window/per_pixel_transparency/allowed <class_ProjectSettings_property_display/window/per_pixel_transparency/allowed>`
- :ref:`display/window/size/transparent <class_ProjectSettings_property_display/window/size/transparent>`
- :ref:`rendering/viewport/transparent_background <class_ProjectSettings_property_rendering/viewport/transparent_background>`
- :ref:`display/window/size/always_on_top <class_ProjectSettings_property_display/window/size/always_on_top>`
- :ref:`display/window/size/no_focus <class_ProjectSettings_property_display/window/size/no_focus>`

  - Điều này ngăn lớp phủ nhận đầu vào từ bàn phím, đồng thời ẩn lớp phủ khỏi thanh tác vụ và trình chuyển đổi tác vụ. Lớp phủ vẫn có thể nhận đầu vào từ chuột (xem bên dưới).

Hãy nhớ định vị và thay đổi kích thước cửa sổ bằng các script, vì người dùng thường không thể di chuyển cửa sổ không có viền.

Để cho phép đầu vào từ chuột truyền đến ứng dụng nền, hãy đặt thuộc tính :ref:`mouse_passthrough <class_Window_property_mouse_passthrough>` thành ``true`` trên Window đang được hiển thị dưới dạng lớp phủ. Bạn cũng có thể xác định một đa giác trong
:ref:`mouse_passthrough_polygon <class_Window_property_mouse_passthrough_polygon>`, để một số khu vực nhất định vẫn có thể chặn đầu vào từ chuột trên lớp phủ.

Ngoài ra, bạn có thể muốn đặt
thuộc tính :ref:`exclude_from_capture <class_Window_property_exclude_from_capture>` thành ``true`` để ngăn lớp phủ xuất hiện trong ảnh chụp màn hình hoặc bản ghi. Gợi ý này chỉ được triển khai trên Windows và macOS, đồng thời chỉ dựa trên nỗ lực tốt nhất, vì vậy không nên sử dụng nó như một biện pháp bảo mật tuyệt đối hoặc DRM.

.. note::

    Không hỗ trợ hiển thị dưới dạng lớp phủ khi bật tính năng nhúng game trong trình chỉnh sửa. Để kiểm tra chức năng này khi chạy project, hãy đảm bảo bạn tắt tính năng nhúng game bằng cách chuyển sang màn hình :menu:`Game`, nhấp vào biểu tượng ngoài cùng bên phải trên thanh ở phía trên và bỏ chọn :menu:`Embed Game on Next Play`.

    Ngoài ra, hãy lưu ý rằng không thể hiển thị lớp phủ bên trên một ứng dụng khác nếu ứng dụng đó sử dụng chế độ toàn màn hình độc quyền. Thay vào đó, phải sử dụng chế độ toàn màn hình không viền để lớp phủ hiển thị được.

    Ngoài ra còn có `các vấn đề đã biết <https://github.com/godotengine/godot/issues/76167>`__ với việc hiển thị cửa sổ trong suốt trên Windows khi sử dụng thiết lập GPU lai (chẳng hạn như NVIDIA Optimus). Việc chuyển renderer có thể giúp khắc phục vấn đề này.

    Trên Linux với X11, tính trong suốt sẽ không hoạt động nếu người dùng đã tắt tính năng compositing trong cài đặt của trình quản lý cửa sổ.

.. _doc_creating_applications_scaling_to_hidpi_displays:

Điều chỉnh tỷ lệ cho màn hình hiDPI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các màn hình hiện đại có mật độ điểm ảnh rất khác nhau, điều này có nghĩa là thường cần một hệ số tỷ lệ khác để đảm bảo các phần tử UI dễ đọc. Hệ số tỷ lệ cũng có thể được cung cấp dưới dạng tùy chỉnh thủ công cho người dùng, để ứng dụng vẫn dễ sử dụng.

Tính năng hỗ trợ nhiều độ phân giải của Godot rất phù hợp để điều chỉnh tỷ lệ ứng dụng khi được cấu hình đúng cách. Hãy làm theo hướng dẫn trong
:ref:`phần ứng dụng không phải game của tài liệu Multiple resolutions <doc_multiple_resolutions_non_game_application>`.

.. note::

    Hiện tại, Godot chỉ hỗ trợ đọc hệ số tỷ lệ màn hình từ cài đặt hệ điều hành trên macOS, Android và Linux (chỉ Wayland). Trên Linux (X11) và Windows, bạn cần cung cấp tùy chọn điều chỉnh tỷ lệ thủ công để người dùng điều chỉnh tỷ lệ UI theo nhu cầu.

Tích hợp trình đọc màn hình
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Trình đọc màn hình cho phép người khiếm thị sử dụng ứng dụng bằng cách đọc các phần tử UI và cung cấp các điều khiển điều hướng. Màn hình chữ Braille là một phương pháp khác cũng dựa vào thông tin trợ năng để hoạt động chính xác.

Godot tự động bật hỗ trợ trình đọc màn hình nếu phát hiện trình đọc màn hình đang chạy. Bạn có thể cấu hình tính năng này trong Project Settings bằng :ref:`accessibility/general/accessibility_support <class_ProjectSettings_property_accessibility/general/accessibility_support>` để tắt trong những tình huống không mong muốn sử dụng. Tính năng này cũng có thể được buộc bật, rất hữu ích khi sử dụng các công cụ gỡ lỗi trợ năng mà Godot không nhận diện là trình đọc màn hình.

Godot sử dụng thư viện `AccessKit <https://accesskit.dev/>`__ để tích hợp trình đọc màn hình.

.. tip::

    Vì hỗ trợ trình đọc màn hình sử dụng chính ứng dụng trình đọc màn hình để phát âm thanh (thay vì project Godot), tính năng này vẫn hoạt động ngay cả khi driver âm thanh được đặt thành ``Dummy`` trong cài đặt project như mô tả bên dưới.

Bạn nên kiểm thử ứng dụng với các trình đọc màn hình phổ biến trên những nền tảng mục tiêu để đảm bảo trải nghiệm tốt cho người dùng khiếm thị. Ví dụ gồm `NVDA <https://www.nvaccess.org/download/>`__ trên Windows, `VoiceOver <https://www.apple.com/accessibility/features/?vision>`__ trên macOS và `Orca <https://help.gnome.org/orca/>`__ trên Linux.

Để hỗ trợ trình đọc màn hình đạt mức khả dụng tốt, cần thực hiện rất nhiều công việc. Bạn cần xác định các nhãn trợ năng bằng cách sử dụng các thuộc tính :ref:`Control.accessibility_name <class_Control_property_accessibility_name>` và :ref:`Control.accessibility_description <class_Control_property_accessibility_description>`, đồng thời đảm bảo UI được sắp xếp theo thứ tự logic khi được trình đọc màn hình đọc.

.. seealso::

    Xem thêm :ref:`doc_text_to_speech` về chức năng chuyển văn bản thành giọng nói, hoạt động độc lập với trình đọc màn hình.

Cài đặt project được khuyến nghị
--------------------------------

Tích hợp với desktop
^^^^^^^^^^^^^^^^^^^^

Để ứng dụng tích hợp tốt hơn với môi trường desktop, bạn có thể đặt các cài đặt project như sau:

- Bật :ref:`application/config/use_custom_user_dir <class_ProjectSettings_property_application/config/use_custom_user_dir>` và đặt :ref:`application/config/custom_user_dir_name <class_ProjectSettings_property_application/config/custom_user_dir_name>` thành một tên phù hợp cho ứng dụng. Điều này đảm bảo các cài đặt và tệp của người dùng được lưu trong một thư mục riêng thay vì
  :ref:`default Godot folder <doc_data_paths_accessing_persistent_user_data>`. Theo quy ước, nên sử dụng kiểu chữ thông thường trên Windows (ví dụ: ``Application Name``) và kebab-case (ví dụ: ``application-name``) trên macOS và Linux.

- Cấu hình các biểu tượng native phù hợp với hướng dẫn thiết kế của hệ điều hành bằng :ref:`application/config/windows_native_icon <class_ProjectSettings_property_application/config/windows_native_icon>` (định dạng ICO) và
  :ref:`application/config/macos_native_icon <class_ProjectSettings_property_application/config/macos_native_icon>` (định dạng ICNS). Theo mặc định, Godot sẽ tự động tạo biểu tượng native dựa trên biểu tượng project, nhưng cách này không phải lúc nào cũng tối ưu.

  - Trên Windows, việc sử dụng tệp ICO được thiết kế thủ công cho phép bạn dùng các biểu tượng khác nhau cho những độ phân giải khác nhau. Bạn có thể dùng cách này để tạo thiết kế riêng ở các độ phân giải thấp hơn nhằm cải thiện khả năng đọc.

  - macOS có `hướng dẫn về biểu tượng ứng dụng <https://developer.apple.com/design/human-interface-guidelines/app-icons/>`__ khác biệt đáng kể so với các nền tảng khác. Sử dụng thiết kế biểu tượng native riêng phù hợp sẽ giúp ứng dụng hòa hợp hơn với môi trường desktop.

- Tắt
  :ref:`display/window/subwindows/embed_subwindows <class_ProjectSettings_property_display/window/subwindows/embed_subwindows>`, để các cửa sổ bổ sung sử dụng giao diện của hệ điều hành và được xem như các cửa sổ native của hệ điều hành.

Hiệu năng
^^^^^^^^^

Dưới đây là một số cài đặt project bạn có thể sử dụng để giảm mức sử dụng CPU, GPU và bộ nhớ:

- Sử dụng trình kết xuất Compatibility nếu bạn không cần các tính năng chỉ có trong Forward+ hoặc Mobile. Trình kết xuất Compatibility có yêu cầu phần cứng thấp hơn và thường khởi chạy nhanh hơn, nên đây là lựa chọn tốt hơn cho các ứng dụng. Việc tạo cửa sổ mới cũng nhanh hơn với trình kết xuất này.

- Bật :ref:`application/run/low_processor_mode <class_ProjectSettings_property_application/run/low_processor_mode>` để giảm mức sử dụng CPU và GPU. Khi đó, dự án chỉ kết xuất một khung hình nếu có nội dung trên màn hình thay đổi.

  - Lưu ý rằng trong một số trường hợp, dự án phải vẽ lại liên tục (ví dụ: nếu một animation hoặc shader sử dụng ``TIME`` đang hiển thị). Việc này sẽ tiêu thụ nhiều điện năng nếu kéo dài, dẫn đến thời lượng pin ngắn hơn và quạt phát ra nhiều tiếng ồn hơn. Để khắc phục sự cố dự án vẽ lại liên tục, bạn có thể bật :menu:`Debug > Debug Canvas Item Redraws` ở đầu trình chỉnh sửa, sau đó chạy dự án. Các vùng được vẽ lại sẽ được tô sáng màu đỏ trong một giây. Có thể điều chỉnh màu và thời lượng tô sáng bằng các thiết lập dự án :ref:`debug/canvas_items/debug_redraw_time <class_ProjectSettings_property_debug/canvas_items/debug_redraw_time>` và :ref:`debug/canvas_items/debug_redraw_color <class_ProjectSettings_property_debug/canvas_items/debug_redraw_color>`.

  - Tốc độ khung hình tối đa mà ứng dụng có thể kết xuất được xác định bởi
    :ref:`application/run/low_processor_mode_sleep_usec <class_ProjectSettings_property_application/run/low_processor_mode_sleep_usec>`. Giá trị này được biểu thị bằng microsecond trên mỗi khung hình, vì vậy có thể tính FPS tối đa bằng công thức ``1000000.0 / sleep_usec``. Theo mặc định, giá trị này được đặt là ``6900``, tương ứng với tối đa khoảng 145 FPS. Bạn có thể tăng giá trị này để giảm thêm mức sử dụng CPU và GPU, nhưng trải nghiệm sẽ kém mượt mà hơn.

- Tắt :ref:`display/window/energy_saving/keep_screen_on <class_ProjectSettings_property_display/window/energy_saving/keep_screen_on>` để màn hình có thể tắt theo các thiết lập nguồn của hệ điều hành khi ứng dụng không hoạt động. Hành vi này thường không mong muốn trong game (ví dụ: khi xem các đoạn cutscene), nhưng đối với ứng dụng, chúng ta muốn màn hình tắt để tiết kiệm điện khi người dùng không chủ động sử dụng ứng dụng.

- Đặt :ref:`audio/driver/driver <class_ProjectSettings_property_audio/driver/driver>` thành ``Dummy`` *(case-sensitive)* nếu ứng dụng của bạn không cần đầu ra hoặc đầu vào âm thanh. Việc này ngăn máy chủ âm thanh khởi động, nhờ đó tiết kiệm một phần tài nguyên CPU và bộ nhớ. Việc này cũng ngăn ứng dụng xuất hiện trong danh sách các ứng dụng đang phát âm thanh của bộ trộn âm thanh trong hệ điều hành. Trên macOS, việc này còn đảm bảo ứng dụng không ngăn thiết bị chuyển sang chế độ ngủ.

- Đặt :ref:`physics/2d/physics_engine <class_ProjectSettings_property_physics/2d/physics_engine>` và :ref:`physics/3d/physics_engine <class_ProjectSettings_property_physics/3d/physics_engine>` thành ``Dummy`` nếu ứng dụng của bạn không cần mô phỏng vật lý (bao gồm cả việc chọn đối tượng). Việc này ngăn các máy chủ vật lý khởi động, nhờ đó tiết kiệm tài nguyên CPU và bộ nhớ. Việc này cũng cho phép
  :ref:`engine compilation configuration editor <doc_engine_compilation_configuration_editor>` tự động phát hiện rằng dự án không sử dụng vật lý.

- Hãy cân nhắc đặt :ref:`display/window/vsync/vsync_mode <class_ProjectSettings_property_display/window/vsync/vsync_mode>` thành **Disabled** để giảm độ trễ đầu vào. Điều này đặc biệt hữu ích cho các dự án nhạy cảm với độ trễ, chẳng hạn như ứng dụng vẽ. Việc này có thể làm tăng mức tiêu thụ điện năng và gây hiện tượng xé hình, vì vậy bạn nên cung cấp tùy chọn để người dùng bật hoặc tắt V-Sync theo nhu cầu.

Hãy tham khảo `Material Maker <https://github.com/RodZill4/material-maker>`__ và `Pixelorama <https://github.com/Orama-Interactive/Pixelorama>`__ để xem các ví dụ về ứng dụng mã nguồn mở được tạo bằng Godot.

Mobile
^^^^^^

Khi thiết kế ứng dụng cho các nền tảng di động, bạn có thể bật một số thiết lập để cải thiện khả năng sử dụng:

**Android:**

- Bật :ref:`input_devices/pointing/android/enable_long_press_as_right_click <class_ProjectSettings_property_input_devices/pointing/android/enable_long_press_as_right_click>` để cho phép người dùng thực hiện thao tác nhấp chuột phải bằng cử chỉ nhấn giữ.

- Bật :ref:`input_devices/pointing/android/enable_pan_and_scale_gestures <class_ProjectSettings_property_input_devices/pointing/android/enable_pan_and_scale_gestures>` để cho phép người dùng di chuyển và thu phóng bằng cử chỉ chạm. Thao tác này sẽ mô phỏng
  :ref:`class_InputEventPanGesture` và :ref:`class_InputEventMagnifyGesture` các sự kiện, có thể được xử lý trong mã của dự án và thường được phát ra bởi bàn di chuột của laptop.

- Tắt :menu:`Screen > Immersive Mode` trong preset export Android để hiển thị thanh trạng thái và thanh điều hướng của hệ thống khi ứng dụng đang hoạt động. Ngoài ra, hãy bật :menu:`Screen > Edge to Edge` để làm cho thanh trạng thái và các biểu tượng điều hướng trở nên trong mờ, đồng thời vẽ chúng lên trên ứng dụng. Nếu làm vậy, hãy đảm bảo ứng dụng chừa đủ không gian cho thanh trạng thái và các biểu tượng điều hướng. Bạn có thể sử dụng
  :ref:`DisplayServer.get_display_safe_area <class_DisplayServer_method_get_display_safe_area>` và :ref:`DisplayServer.get_display_cutouts <class_DisplayServer_method_get_display_cutouts>` để truy vấn vùng mà ứng dụng có thể vẽ một cách an toàn.

**iOS:**

- Tắt :ref:`display/window/ios/hide_home_indicator <class_ProjectSettings_property_display/window/ios/hide_home_indicator>` để hiển thị chỉ báo màn hình chính bên trên ứng dụng.

- Tắt :ref:`display/window/ios/hide_status_bar <class_ProjectSettings_property_display/window/ios/hide_status_bar>` để giữ thanh trạng thái hiển thị khi ứng dụng đang hoạt động.

- Tắt :ref:`display/window/ios/suppress_ui_gesture <class_ProjectSettings_property_display/window/ios/suppress_ui_gesture>` để cho phép các cử chỉ UI hoạt động ngay lập tức mà không yêu cầu thực hiện chúng hai lần.

Thêm unit test
--------------

Trong một ứng dụng, việc có một thiết lập `unit testing <https://en.wikipedia.org/wiki/Unit_testing>`__ thường có giá trị hơn so với trong một game. Thiết lập này có thể được dùng để tự động phát hiện các hồi quy, việc thường dễ thực hiện hơn trong bối cảnh ứng dụng, nơi logic có thể được tách biệt rõ ràng.

GDScript không có framework unit testing tích hợp, nhưng cộng đồng đã duy trì một số plugin unit testing:

- `Gut <https://github.com/bitwes/Gut>`__
- `GdUnit4 <https://github.com/godot-gdunit-labs/gdUnit4>`__ (cũng hỗ trợ C#)

Với C# và GDExtension (C++, Rust, v.v.), bạn có thể sử dụng các framework testing tiêu chuẩn như NUnit hoặc `doctest <https://github.com/doctest/doctest>`__.

Tối ưu hóa kích thước bản phân phối
-----------------------------------

Vì các ứng dụng không phải game thường tránh sử dụng những phần lớn của engine, chẳng hạn như chức năng âm thanh hoặc 3D, bạn có thể biên dịch một export template được tối ưu hóa để giảm kích thước tệp. Việc này cũng cải thiện thời gian khởi động, đặc biệt trên nền tảng web, nơi kích thước tệp nhị phân liên quan trực tiếp đến tốc độ khởi tạo.

Mức giảm kích thước thường đáng kể (so với kích thước dự án), vì ứng dụng chứa ít asset lớn hơn so với game. Xem :ref:`doc_optimizing_for_size` để biết thêm thông tin về cách thực hiện việc này.

Tạo bản phân phối một tệp thực thi duy nhất
-------------------------------------------

Theo mặc định, Godot tạo một tệp PCK chứa dữ liệu dự án bên cạnh tệp thực thi. Điều này có nghĩa là nếu tệp thực thi được di chuyển mà không đồng thời di chuyển tệp PCK, ứng dụng sẽ không chạy. Đây không phải là lựa chọn lý tưởng cho các ứng dụng, vốn ngày càng được phân phối dưới dạng một tệp thực thi duy nhất.

Để làm cho ứng dụng hoàn toàn độc lập trong một tệp thực thi duy nhất, bạn có thể bật **Embed PCK** trong các tùy chọn preset export. Việc này sẽ nhúng dữ liệu PCK vào trong tệp thực thi, nhờ đó có thể di chuyển ứng dụng mà không làm ứng dụng bị lỗi. Điều này cũng cho phép chạy ứng dụng trực tiếp từ một kho lưu trữ ZIP mà không cần giải nén trước.

.. note::

    PCK embedding có giới hạn về kích thước tùy thuộc vào nền tảng. Các ứng dụng rất lớn (vài GB) có thể không sử dụng được tính năng này trên tất cả nền tảng. Hãy xem tài liệu export dành cho nền tảng đích để biết thêm chi tiết.

Tạo ứng dụng portable
---------------------

Một ứng dụng được gọi là *portable* khi có thể chạy mà không cần cài đặt và cấu hình của ứng dụng hoàn toàn tự chứa trong thư mục mà ứng dụng được giải nén vào. Điều này cho phép đặt các tệp ứng dụng trên ổ USB hoặc thiết bị tương tự và chạy ứng dụng trên các máy khác nhau mà không cần thực hiện quy trình cài đặt.

:ref:`self-contained mode <doc_data_paths_self_contained_mode>` của chính trình chỉnh sửa Godot hiện không thể được sử dụng trong các project. Tuy nhiên, bạn vẫn có thể chọn lưu các tệp cấu hình của riêng mình vào thư mục chứa executable như sau:

.. code-block::

    var config_path = OS.get_executable_path().get_base_dir().path_join("config.ini")
    # Sau đó dùng `config_path` để lưu/tải các tệp cấu hình bằng ConfigFile hoặc công cụ tương tự.

Bạn có thể muốn để chế độ portable là tùy chọn vì chế độ này không phải lúc nào cũng được mong muốn. Thông thường, việc này được thực hiện bằng cách phát hiện sự hiện diện của một tệp cụ thể trong thư mục của executable (ví dụ: một tệp có tên ``portable.txt``) và chỉ sử dụng thư mục của executable để lưu cấu hình nếu tệp đó hiện diện.

.. warning::

    Hãy nhớ rằng cách này chỉ hoạt động nếu ứng dụng được giải nén vào một vị trí có quyền ghi. Nếu executable được chạy từ một vị trí chỉ đọc, chẳng hạn như ``C:\Program Files`` trên Windows, sẽ xảy ra lỗi quyền truy cập.

Tạo trình cài đặt
-----------------

Trong khi game thường được cài đặt thông qua các launcher như Steam hoặc được tải xuống dưới dạng ZIP, các ứng dụng thường được phân phối dưới dạng trình cài đặt để tích hợp tốt hơn với desktop. Trình cài đặt có thể thực hiện các thao tác như thêm shortcut vào Start Menu hoặc desktop, thiết lập liên kết tệp và nhiều thao tác khác. Trình cài đặt cũng có thể được chạy tự động thông qua command line, nhờ đó phù hợp hơn với môi trường doanh nghiệp.

Godot không có hỗ trợ tích hợp để tạo trình cài đặt cho các project đã export. Tuy nhiên, bạn vẫn có thể tạo trình cài đặt của riêng mình bằng các công cụ bên thứ ba.

Sau đây là danh sách chưa đầy đủ các công cụ có thể dùng để tạo trình cài đặt:

- **Windows:** `Inno Setup <https://jrsoftware.org/isinfo.php>`__, `NSIS <https://nsis.sourceforge.io/Main_Page>`__

  - Nếu có chứng chỉ code signing, hãy nhớ ký *cả* trình cài đặt và executable của project. Để thực hiện việc này,
    :ref:`ký executable của project đã export <doc_exporting_for_windows_code_signing>`, tạo trình cài đặt chứa project đã export, sau đó ký thủ công trình cài đặt vừa tạo.

- **macOS:** `create-dmg <https://github.com/create-dmg/create-dmg>`__

- **Linux:** `Flatpak <https://docs.flatpak.org/en/latest/first-build.html>`__

  - Có một `Godot BaseApp <https://github.com/flathub/org.godotengine.Godot.BaseApp>`__ có thể được dùng làm cơ sở để tạo các gói Flatpak cho các project Godot. Xem `the Pixelorama Flatpak <https://github.com/flathub/com.orama_interactive.Pixelorama>`__ để biết một ví dụ về Flatpak sử dụng BaseApp này.

Tài nguyên
----------

Các trang này đề cập đến những tác vụ thường được thực hiện trong các ứng dụng không phải game:

- :ref:`doc_runtime_loading_and_saving`
- :ref:`doc_http_request_class`
- :ref:`class_ConfigFile` (dùng để lưu tùy chọn của người dùng)
