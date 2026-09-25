.. _doc_logging:

Ghi nhật ký
===========

Godot cung cấp một số cách để tổ chức và thu thập thông báo nhật ký.

In thông báo
------------

.. seealso::

    Xem :ref:`doc_output_panel_printing_messages` để biết hướng dẫn in thông báo. Nội dung được in nhìn chung giống hệt nội dung được ghi vào nhật ký.

    Khi chạy một project từ editor, editor sẽ hiển thị văn bản được ghi vào nhật ký trong :ref:`doc_output_panel`.

Cài đặt project
---------------

Có một số cài đặt project để kiểm soát hoạt động ghi nhật ký trong Godot:

- **Application > Run > Disable stdout:** Tắt hoàn toàn việc ghi nhật ký vào đầu ra tiêu chuẩn. Điều này cũng ảnh hưởng đến nội dung mà các custom logger nhận được. Bạn có thể kiểm soát tùy chọn này trong runtime bằng cách thiết lập :ref:`Engine.print_to_stdout <class_Engine_property_print_to_stdout>`.
- **Application > Run > Disable stderr:** Tắt hoàn toàn việc ghi nhật ký vào lỗi tiêu chuẩn. Điều này cũng ảnh hưởng đến nội dung mà các custom logger nhận được. Bạn có thể kiểm soát tùy chọn này trong runtime bằng cách thiết lập :ref:`Engine.print_error_messages <class_Engine_property_print_error_messages>`.
- **Debug > Settings > stdout > Verbose stdout:** Bật ghi nhật ký chi tiết vào đầu ra tiêu chuẩn. Nội dung được in từ :ref:`print_verbose() <class_@GlobalScope_method_print_verbose>` chỉ hiển thị khi chế độ chi tiết được bật.
- **Debug > Settings > stdout > Print FPS:** In số khung hình mỗi giây sau mỗi giây, cũng như trạng thái V-Sync khi khởi động (vì V-Sync có thể giới hạn hiệu quả framerate tối đa).
- **Debug > Settings > stdout > Print GPU Profile:** In báo cáo về mức sử dụng GPU sau mỗi giây, sử dụng cùng nguồn dữ liệu với :ref:`doc_debugger_panel_visual_profiler`.

Một số cài đặt project này cũng có thể được ghi đè bằng
:ref:`đối số dòng lệnh <doc_command_line_tutorial>` như ``--quiet``, ``--verbose`` và ``--print-fps``.

Chức năng ghi nhật ký vào tệp của engine cũng có thể được cấu hình, như mô tả trong phần bên dưới.

Ghi nhật ký vào tệp tích hợp sẵn
--------------------------------

Theo mặc định, Godot ghi các tệp nhật ký vào ``user://logs/godot.log`` trên các nền tảng desktop. Bạn có thể thay đổi vị trí này bằng cách chỉnh sửa cài đặt project ``debug/file_logging/log_path``. Các tệp nhật ký được xoay vòng để giữ lại những tệp cũ cho việc kiểm tra. Mỗi session tạo một tệp nhật ký mới; tệp cũ được đổi tên để chứa ngày mà nó được xoay vòng. Theo mặc định, tối đa 5 tệp nhật ký được giữ lại; bạn có thể điều chỉnh số lượng này bằng cài đặt project ``debug/file_logging/max_log_files``.

Bạn cũng có thể tắt hoàn toàn việc ghi nhật ký vào tệp bằng cài đặt project ``debug/file_logging/enable_file_logging``.

Khi project gặp sự cố, nhật ký sự cố được ghi vào cùng tệp với tệp nhật ký. Nhật ký sự cố chỉ chứa backtrace có thể sử dụng được nếu binary đã chạy có debugging symbols, hoặc nếu binary có thể tìm thấy tệp debug symbols khớp với nó. Các binary chính thức không cung cấp debugging symbols, vì vậy cần có custom build để tính năng này hoạt động. Xem
:ref:`Debugging symbols <doc_introduction_to_the_buildsystem_debugging_symbols>` để biết hướng dẫn biên dịch binary với debugging symbols được bật.

.. note::

    Các tệp nhật ký cho các câu lệnh :ref:`print() <class_@GlobalScope_method_print>` được cập nhật khi đầu ra tiêu chuẩn được engine *xả*. Đầu ra tiêu chuẩn chỉ được xả sau mỗi lần print trong các bản build debug. Trong các project được export ở chế độ release, đầu ra tiêu chuẩn chỉ được xả khi project thoát hoặc gặp sự cố để cải thiện hiệu năng, đặc biệt nếu project thường xuyên in văn bản ra đầu ra tiêu chuẩn.

    Mặt khác, luồng lỗi tiêu chuẩn (được sử dụng bởi :ref:`printerr() <class_@GlobalScope_method_printerr>`,
    :ref:`push_error() <class_@GlobalScope_method_push_error>`, và
    :ref:`push_warning() <class_@GlobalScope_method_push_warning>`) luôn được xả sau mỗi lần print, kể cả trong các project được export ở chế độ release.

    Đối với một số trường hợp sử dụng như dedicated server, việc để các bản build release luôn xả stdout khi print có thể sẽ phù hợp hơn, ताकि các dịch vụ ghi nhật ký như journald có thể thu thập nhật ký trong khi process đang chạy. Bạn có thể thực hiện việc này bằng cách bật ``application/run/flush_stdout_on_print`` trong Project Settings.

Backtrace của script
--------------------

Kể từ Godot 4.5, khi mã GDScript gặp lỗi, nó sẽ ghi một backtrace trỏ đến nguồn gốc của lỗi, đồng thời chứa call stack dẫn đến lỗi đó. Hành vi này luôn được bật khi chạy trong editor hoặc khi project được export ở chế độ debug.

Trong các project được export ở chế độ release, backtrace bị tắt theo mặc định vì lý do hiệu năng. Bạn có thể bật chúng bằng cách chọn **Debug > Settings > GDScript > Always Track Call Stacks** trong Project Settings. Nếu bạn sử dụng custom logging system để báo cáo exception cho một remote service, bạn nên bật tùy chọn này để các lỗi được báo cáo có nhiều thông tin hữu ích hơn.

Backtrace khi gặp sự cố
-----------------------

.. warning::

    Backtrace khi gặp sự cố chỉ hữu ích nếu chúng được ghi lại trong một bản build có chứa :ref:`debugging symbols <doc_introduction_to_the_buildsystem_debugging_symbols>`. Các binary Godot chính thức không chứa debugging symbols, vì vậy bạn phải biên dịch một editor custom hoặc binary export template để có backtrace khi gặp sự cố hữu ích.

Khi project gặp sự cố, backtrace sự cố được in vào luồng lỗi tiêu chuẩn. Trong một bản build có debug symbols, nội dung này có thể trông như sau:

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

Mặt khác, nếu không có debug symbols, nội dung sẽ trông như sau:

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

Backtrace này cũng được ghi vào tệp của session hiện tại, nhưng **không** hiển thị trong bảng Output của editor. Vì hệ thống scripting của engine không còn chạy khi engine gặp sự cố, bạn không thể truy cập backtrace từ scripting trong cùng session. Tuy nhiên, bạn vẫn có thể đọc backtrace sự cố trong session tiếp theo bằng cách tải các tệp nhật ký và tìm chuỗi backtrace sự cố (``Program crashed with signal``) bằng :ref:`class_FileAccess`. Điều này cho phép bạn truy cập thông tin backtrace ngay cả sau khi xảy ra sự cố, miễn là người dùng khởi động lại project và tính năng ghi nhật ký vào tệp được bật:

.. code-block:: gdscript

    # Có thể biến script này thành autoload để nó chạy khi project khởi động.
    extends Node

    func _ready() -> void:
      var log_dir: String = String(ProjectSettings.get_setting("debug/file_logging/log_path")).get_base_dir()
      # Lấy tệp nhật ký cuối cùng theo thứ tự bảng chữ cái.
      # Vì timestamp được đặt trong tên tệp nên đây luôn phải là tệp gần đây nhất
      # đã được xoay vòng. Tệp nhật ký không có timestamp là tệp của session hiện tại,
      # vì vậy chúng ta không muốn đọc tệp đó.
      var last_log_file: String = log_dir.path_join(DirAccess.get_files_at(log_dir)[-1])
      var last_long_contents: String = FileAccess.get_file_as_string(last_log_file)

      var crash_begin_idx: int = last_long_contents.find("Program crashed with signal")
      if crash_begin_idx != -1:
          print("The previous session has crashed with the following backtrace:\n")
          print(last_long_contents.substr(crash_begin_idx))

Bạn có thể tùy chỉnh thông báo xuất hiện ở đầu backtrace bằng cài đặt project **Debug > Settings > Crash Handler > Message**. Bạn có thể dùng tùy chọn này để trỏ đến một URL hoặc địa chỉ email nơi người dùng có thể báo cáo sự cố.

Tạo custom logger
-----------------

Kể từ Godot 4.5, bạn có thể tạo custom logger. Chức năng ghi nhật ký tùy chỉnh này có thể được sử dụng cho nhiều mục đích:

- Hiển thị một console trong game với cùng các thông báo mà engine in ra, mà không cần sửa đổi các script khác.
- Báo cáo các lỗi được in từ máy của người chơi lên một máy chủ từ xa. Điều này có thể giúp các nhà phát triển sửa lỗi dễ dàng hơn khi trò chơi đã được phát hành hoặc trong quá trình playtest.
- Tích hợp bản export dedicated server với các nền tảng monitoring.

Có thể đăng ký custom logger bằng cách tạo một class kế thừa từ :ref:`class_logger`, sau đó truyền một instance của class này vào :ref:`OS.add_logger <class_OS_method_add_logger>` trong phương thức :ref:`_init() <class_Object_private_method__init>` của một script. Một vị trí phù hợp để thực hiện việc này là một :ref:`autoload <doc_singletons_autoload>`.

Class phải định nghĩa hai phương thức: :ref:`_log_message() <class_Logger_private_method__log_message>` và :ref:`_log_error() <class_Logger_private_method__log_error>`.

Sau đây là một ví dụ tối thiểu có thể hoạt động về custom logger, với script được thêm dưới dạng autoload:

.. code-block:: gdscript

    extends Node

    class CustomLogger extends Logger:
        # Lưu ý rằng phương thức này không được gọi cho các thông báo sử dụng
        # `push_error()` và `push_warning()`, dù chúng được in ra stderr.
        func _log_message(message: String, error: bool) -> void:
            # Thực hiện một thao tác với `message`.
            # `error` là `true` cho các thông báo được in ra standard error stream (stderr) bằng `print_error()`.
            # Lưu ý rằng phương thức này sẽ được gọi từ các thread khác với main thread, có thể xảy ra đồng thời
            # vì vậy bạn cần đảm bảo thread-safety cho phương thức này, chẳng hạn bằng Mutex.
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
            # Thực hiện một thao tác với lỗi. Nội dung lỗi nằm trong `rationale`.
            # Xem phần tham chiếu lớp Logger để biết chi tiết về các tham số khác.
            # Lưu ý rằng phương thức này sẽ được gọi từ các thread khác với main thread, có thể xảy ra đồng thời
            # vì vậy bạn cần đảm bảo thread-safety cho phương thức này, chẳng hạn bằng Mutex.
            pass

    # Sử dụng `_init()` để khởi tạo logger sớm nhất có thể, nhờ đó các thông báo
    # được in ra sớm sẽ được ghi nhận. Tuy nhiên, ngay cả khi sử dụng `_init()`, các thông báo khởi tạo
    # của engine vẫn không thể truy cập được.
    func _init() -> void:
        OS.add_logger(CustomLogger.new())

Lưu ý rằng để tránh đệ quy vô hạn, bạn không thể thực sự sử dụng
:ref:`print() <class_@GlobalScope_method_print>` và các phương thức liên quan của nó trong ``_log_message()``. Bạn cũng không thể thực sự sử dụng
:ref:`push_error() <class_@GlobalScope_method_push_error>` hoặc :ref:`push_warning() <class_@GlobalScope_method_push_warning>` trong ``_log_error()``. Việc cố gắng làm vậy sẽ in một thông báo vào cùng stream với thông báo ban đầu. Thông báo này không khả dụng trong custom logger, nhờ đó ngăn đệ quy vô hạn xảy ra:

.. code-block:: none

    While attempting to print a message, another message was printed:
    ...

    While attempting to print an error, another error was printed:
    ...

.. seealso::

    Bạn có thể tìm thấy một ví dụ về console trong game được xây dựng bằng custom logger trong dự án demo `Custom Logging demo project <https://github.com/godotengine/godot-demo-projects/tree/master/misc/custom_logging>`__.
