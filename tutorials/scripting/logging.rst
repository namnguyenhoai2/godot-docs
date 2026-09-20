.. _doc_logging:

Ghi nhật ký
===========

Godot cung cấp một số cách để tổ chức và thu thập các thông báo nhật ký.

In thông báo
------------

.. seealso::

    Xem :ref:`doc_output_panel_printing_messages` để biết hướng dẫn về cách in thông báo. Kết quả được in thường giống hệt kết quả được ghi vào nhật ký.

    Khi chạy một project từ editor, editor sẽ hiển thị văn bản được ghi vào nhật ký trong :ref:`doc_output_panel`.

Cài đặt project
---------------

Có một số cài đặt project để kiểm soát hành vi ghi nhật ký trong Godot:

- **Application > Run > Disable stdout:** Tắt hoàn toàn việc ghi nhật ký vào standard output. Điều này cũng ảnh hưởng đến dữ liệu mà các logger tùy chỉnh nhận được. Có thể kiểm soát tùy chọn này trong runtime bằng cách đặt :ref:`Engine.print_to_stdout <class_Engine_property_print_to_stdout>`. - **Application > Run > Disable stderr:** Tắt hoàn toàn việc ghi nhật ký vào standard error. Điều này cũng ảnh hưởng đến dữ liệu mà các logger tùy chỉnh nhận được. Có thể kiểm soát tùy chọn này trong runtime bằng cách đặt :ref:`Engine.print_error_messages <class_Engine_property_print_error_messages>`. - **Debug > Settings > stdout > Verbose stdout:** Bật ghi nhật ký chi tiết vào standard output. Kết quả in từ :ref:`print_verbose() <class_@GlobalScope_method_print_verbose>` chỉ hiển thị khi chế độ verbose được bật. - **Debug > Settings > stdout > Print FPS:** In số khung hình trên giây sau mỗi giây, cũng như trạng thái V-Sync khi khởi động (vì V-Sync có thể thực sự giới hạn framerate tối đa). - **Debug > Settings > stdout > Print GPU Profile:** In báo cáo về mức sử dụng GPU sau mỗi giây, sử dụng cùng nguồn dữ liệu với :ref:`doc_debugger_panel_visual_profiler`.

Một số cài đặt project này cũng có thể được ghi đè bằng cách sử dụng
:ref:`command line arguments <doc_command_line_tutorial>` such as ``--quiet``,
``--verbose`` và ``--print-fps``.

Tính năng ghi nhật ký vào file của engine cũng có thể được cấu hình, như mô tả trong phần bên dưới.

Ghi nhật ký vào file tích hợp sẵn
---------------------------------

Theo mặc định, Godot ghi các file nhật ký vào ``user://logs/godot.log`` trên các nền tảng desktop. Bạn có thể thay đổi vị trí này bằng cách sửa cài đặt project ``debug/file_logging/log_path``. Các file nhật ký được xoay vòng để giữ lại những file cũ cho việc kiểm tra. Mỗi session tạo một file nhật ký mới; file cũ được đổi tên để chứa ngày mà nó được xoay vòng. Theo mặc định, tối đa 5 file nhật ký được giữ lại; con số này có thể điều chỉnh bằng cài đặt project ``debug/file_logging/max_log_files``.

Bạn cũng có thể tắt hoàn toàn việc ghi nhật ký vào file bằng cài đặt project ``debug/file_logging/enable_file_logging``.

Khi project bị crash, nhật ký crash được ghi vào cùng file với file nhật ký. Nhật ký crash chỉ chứa backtrace có thể sử dụng nếu binary đã chạy có debugging symbols, hoặc nếu có thể tìm thấy file debug symbols khớp với binary. Các binary chính thức không cung cấp debugging symbols, vì vậy cần có custom build để tính năng này hoạt động. Xem
:ref:`Debugging symbols <doc_introduction_to_the_buildsystem_debugging_symbols>`
để biết hướng dẫn biên dịch binary với debugging symbols được bật.

.. note::

    Các file nhật ký cho các câu lệnh :ref:`print() <class_@GlobalScope_method_print>` được cập nhật khi standard output được engine *flush*. Standard output chỉ được flush sau mỗi lần in trong các bản build debug. Trong các project được export ở chế độ release, standard output chỉ được flush khi project thoát hoặc bị crash để cải thiện hiệu năng, đặc biệt nếu project thường xuyên in văn bản vào standard output.

    Mặt khác, stream standard error (được sử dụng bởi :ref:`printerr() <class_@GlobalScope_method_printerr>`,
    :ref:`push_error() <class_@GlobalScope_method_push_error>`, and
    :ref:`push_warning() <class_@GlobalScope_method_push_warning>`) is always
    được flush sau mỗi lần in, ngay cả trong các project được export ở chế độ release.

    Đối với một số trường hợp sử dụng như dedicated server, bạn có thể muốn các bản build release luôn flush stdout khi in, để các dịch vụ ghi nhật ký như journald có thể thu thập nhật ký trong khi process đang chạy. Bạn có thể thực hiện việc này bằng cách bật ``application/run/flush_stdout_on_print`` trong Project Settings.

Backtrace của script
--------------------

Kể từ Godot 4.5, khi code GDScript gặp lỗi, nó sẽ ghi lại một backtrace trỏ đến nguồn gốc của lỗi, đồng thời chứa call stack dẫn đến lỗi đó. Hành vi này luôn được bật khi chạy trong editor hoặc khi project được export ở chế độ debug.

Trong các project được export ở chế độ release, backtrace mặc định bị tắt vì lý do hiệu năng. Bạn có thể bật chúng bằng cách chọn **Debug > Settings > GDScript > Always Track Call Stacks** trong Project Settings. Nếu bạn sử dụng một hệ thống logging tùy chỉnh để báo cáo exception đến một dịch vụ từ xa, bạn nên bật tùy chọn này để các lỗi được báo cáo có thêm thông tin hữu ích cho việc xử lý.

Backtrace của crash
-------------------

.. warning::

    Backtrace của crash chỉ hữu ích nếu chúng được ghi lại trong một bản build có chứa :ref:`debugging symbols <doc_introduction_to_the_buildsystem_debugging_symbols>`. Các binary Godot chính thức không chứa debugging symbols, vì vậy bạn phải biên dịch một editor tùy chỉnh hoặc binary export template để có backtrace crash hữu ích.

Khi project bị crash, backtrace của crash được in vào stream standard error. Đây là dạng kết quả có thể thấy trong một bản build có debug symbols:

.. code-block:: none

    ================================================================
    handle_crash: Program crashed with signal 4
    Engine version: Godot Engine v4.5.beta.custom_build (6c9aa4c7d3b9b91cd50714c40eeb234874df7075)
    Dumping the backtrace. Please include this when reporting the bug to the project developer.
    [1] /lib64/libc.so.6(+0x1a070) [0x7f6e5e277070] (??:0)
    [2] godot() [0x4da3358] (/path/to/godot/core/core_bind.cpp:336 (discriminator 2))
    [3] godot() [0xdf5f2f] (/path/to/godot/modules/gdscript/gdscript.h:591)
    [4] godot() [0xbffd46] (/path/to/godot/modules/gdscript/gdscript.cpp:2065 (discriminator 1))
    [5] godot() [0x30f2ea4] (/path/to/godot/core/variant/variant.h:870)
    [6] godot() [0x550d4e1] (/path/to/godot/core/object/object.cpp:933)
    [7] godot() [0x30d996a] (/path/to/godot/scene/main/node.cpp:318 (discriminator 1))
    [8] godot() [0x3131a7f] (/path/to/godot/core/templates/hash_map.h:465)
    [9] godot() [0x424589] (/path/to/godot/platform/linuxbsd/os_linuxbsd.cpp:970)
    [10] /lib64/libc.so.6(+0x3575) [0x7f6e5e260575] (??:0)
    [11] /lib64/libc.so.6(__libc_start_main+0x88) [0x7f6e5e260628] (??:0)
    [12] godot() [0x464df5] (??:?)
    -- END OF C++ BACKTRACE --
    ================================================================
    GDScript backtrace (most recent call first):
        [0] _ready (res://test.gd:5)
    -- END OF GDSCRIPT BACKTRACE --
    ================================================================

Mặt khác, nếu không có debug symbols, kết quả sẽ có dạng như sau:

.. code-block:: none

    ================================================================
    handle_crash: Program crashed with signal 4
    Engine version: Godot Engine v4.5.beta.custom_build (6c9aa4c7d3b9b91cd50714c40eeb234874df7075)
    Dumping the backtrace. Please include this when reporting the bug to the project developer.
    [1] /lib64/libc.so.6(+0x1a070) [0x7fdfaf666070] (??:0)
    [2] godot() [0x4da3358] (??:0)
    [3] godot() [0xdf5f2f] (??:0)
    [4] godot() [0xbffd46] (??:0)
    [5] godot() [0x30f2ea4] (??:0)
    [6] godot() [0x550d4e1] (??:0)
    [7] godot() [0x30d996a] (??:0)
    [8] godot() [0x3131a7f] (??:0)
    [9] godot() [0x424589] (??:0)
    [10] /lib64/libc.so.6(+0x3575) [0x7fdfaf64f575] (??:0)
    [11] /lib64/libc.so.6(__libc_start_main+0x88) [0x7fdfaf64f628] (??:0)
    [12] godot() [0x464df5] (??:0)
    -- END OF C++ BACKTRACE --
    ================================================================
    GDScript backtrace (most recent call first):
        [0] _ready (res://test.gd:5)
    -- END OF GDSCRIPT BACKTRACE --
    ================================================================

Backtrace này cũng được ghi vào file của session hiện tại, nhưng **không** hiển thị trong bảng Output của editor. Vì hệ thống scripting của engine không còn chạy khi engine bị crash, nên không thể truy cập backtrace này từ scripting trong cùng session. Tuy nhiên, bạn vẫn có thể đọc backtrace của crash trong session tiếp theo bằng cách tải các file nhật ký và tìm chuỗi backtrace của crash (``Program crashed with signal``) bằng :ref:`class_FileAccess`. Điều này cho phép bạn truy cập thông tin backtrace ngay cả sau khi crash, miễn là người dùng khởi động lại project và tính năng ghi nhật ký vào file được bật:

.. code-block:: gdscript

    # Bạn có thể biến script này thành một autoload để nó chạy khi project khởi động.
    extends Node

    func _ready() -> void:
      var log_dir: String = String(ProjectSettings.get_setting("debug/file_logging/log_path")).get_base_dir()
      # Lấy file nhật ký cuối cùng theo thứ tự alphabet.
      # Vì timestamp được đưa vào tên file, file đó luôn phải là file gần đây nhất
      # đã được xoay vòng. File nhật ký không có timestamp là file của session hiện tại,
      # vì vậy chúng ta không muốn đọc file đó.
      var last_log_file: String = log_dir.path_join(DirAccess.get_files_at(log_dir)[-1])
      var last_long_contents: String = FileAccess.get_file_as_string(last_log_file)

      var crash_begin_idx: int = last_long_contents.find("Program crashed with signal")
      if crash_begin_idx != -1:
          print("The previous session has crashed with the following backtrace:\n")
          print(last_long_contents.substr(crash_begin_idx))

Bạn có thể tùy chỉnh thông báo xuất hiện ở đầu backtrace bằng cài đặt project **Debug > Settings > Crash Handler > Message**. Có thể sử dụng thông báo này để cung cấp URL hoặc địa chỉ email mà người dùng có thể dùng để báo cáo sự cố.

Tạo logger tùy chỉnh
--------------------

Kể từ Godot 4.5, bạn có thể tạo logger tùy chỉnh. Tính năng logging tùy chỉnh này có thể được sử dụng cho nhiều mục đích:

- Hiển thị console trong game với cùng các thông báo mà engine in ra mà không yêu cầu sửa đổi các script khác. - Báo cáo các lỗi được in từ máy của người chơi đến một server từ xa. Điều này có thể giúp developer sửa lỗi dễ dàng hơn khi game đã phát hành hoặc trong quá trình playtest. - Tích hợp một bản export dedicated server với các nền tảng monitoring.

Có thể đăng ký một logger tùy chỉnh bằng cách tạo một class kế thừa từ :ref:`class_logger`, sau đó truyền một instance của class này vào :ref:`OS.add_logger <class_OS_method_add_logger>` trong method :ref:`_init() <class_Object_private_method__init>` của một script. Một nơi phù hợp để thực hiện việc này là một :ref:`autoload <doc_singletons_autoload>`.

Class phải định nghĩa hai method: :ref:`_log_message() <class_Logger_private_method__log_message>` và :ref:`_log_error() <class_Logger_private_method__log_error>`.

Sau đây là một ví dụ tối thiểu nhưng hoạt động được về logger tùy chỉnh, với script được thêm dưới dạng autoload:

.. code-block:: gdscript

    extends Node

    class CustomLogger extends Logger:
        # Note that this method is not called for messages that use
        # `push_error()` và `push_warning()`, mặc dù chúng được in vào stderr.
        func _log_message(message: String, error: bool) -> void:
            # Thực hiện một thao tác nào đó với `message`.
            # `error` là `true` đối với các thông báo được in vào stream standard error (stderr) bằng `print_error()`.
            # Note that this method will be called from threads other than the main thread, possibly at the same
            # thời điểm, vì vậy bạn sẽ cần có một cơ chế thread-safety nào đó, chẳng hạn như một Mutex.
            pass

        func _log_error(
                function: String,
                file: String,
                line: int,
                code: String,
                rationale: String,
                editor_notify: bool,
                error_type: int,
                script_backtraces: Array[ScriptBacktrace]
        ) -> void:
            # Thực hiện một thao tác nào đó với lỗi. Văn bản lỗi nằm trong `rationale`.
            # Xem tài liệu tham chiếu về class Logger để biết chi tiết về các tham số khác.
            # Note that this method will be called from threads other than the main thread, possibly at the same
            # thời điểm, vì vậy bạn sẽ cần có một cơ chế thread-safety nào đó, chẳng hạn như một Mutex.
            pass

    # Sử dụng `_init()` để khởi tạo logger sớm nhất có thể, nhằm đảm bảo các thông báo
    # được in sớm cũng được ghi nhận. Tuy nhiên, ngay cả khi sử dụng `_init()`, các thông báo khởi tạo của
    # chính engine vẫn không thể truy cập được.
    func _init() -> void:
        OS.add_logger(CustomLogger.new())

Lưu ý rằng để tránh đệ quy vô hạn, bạn không thể sử dụng một cách hiệu quả
:ref:`print() <class_@GlobalScope_method_print>` and its related methods in
``_log_message()``. Bạn cũng không thể sử dụng một cách hiệu quả
:ref:`push_error() <class_@GlobalScope_method_push_error>`
hoặc :ref:`push_warning() <class_@GlobalScope_method_push_warning>` trong ``_log_error()``. Việc cố gắng làm vậy sẽ in một thông báo vào cùng stream với thông báo ban đầu. Thông báo này không khả dụng trong logger tùy chỉnh, nhờ đó ngăn đệ quy vô hạn xảy ra:

.. code-block:: none

    While attempting to print a message, another message was printed:
    ...

    While attempting to print an error, another error was printed:
    ...

.. seealso::

    Bạn có thể tìm thấy một ví dụ về console trong game được xây dựng bằng logger tùy chỉnh trong `Custom Logging demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/custom_logging>`__.
