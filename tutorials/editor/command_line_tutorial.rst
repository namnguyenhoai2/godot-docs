.. _doc_command_line_tutorial:

Hướng dẫn về dòng lệnh
======================

.. highlight:: shell

Một số developer thích sử dụng dòng lệnh thường xuyên. Godot được thiết kế để thân thiện với họ, vì vậy dưới đây là các bước để làm việc hoàn toàn từ dòng lệnh. Vì engine hầu như không phụ thuộc vào thư viện bên ngoài, thời gian khởi tạo khá nhanh, nên phù hợp với workflow này.

.. note::

    Trên Windows và Linux, bạn có thể chạy một binary Godot trong terminal bằng cách chỉ định path tương đối hoặc tuyệt đối của nó.

    Trên macOS, quy trình này khác do Godot nằm trong một bundle ``.app`` (là một *folder*, không phải file). Để chạy một binary Godot từ terminal trên macOS, bạn phải ``cd`` đến folder chứa application bundle của Godot, sau đó chạy ``Godot.app/Contents/MacOS/Godot`` kèm theo bất kỳ command line argument nào. Nếu bạn đã đổi tên application bundle từ ``Godot`` thành tên khác, hãy nhớ chỉnh sửa command này cho phù hợp.

Tham chiếu dòng lệnh
--------------------

.. |release| image:: img/template_release.svg
.. |debug| image:: img/template_debug.svg
.. |extended| image:: img/template_extended.svg
.. |editor| image:: img/editor.svg

**Chú giải**

- |release| Có trong editor build, debug export template và release export template. - |debug| Chỉ có trong editor build và debug export template. - |extended| Chỉ có trong editor build và export template được biên dịch với ``disable_path_overrides=false``. - |editor| Chỉ có trong editor build.

Lưu ý rằng các command line argument không xác định hoàn toàn không có tác dụng. Engine sẽ **không** cảnh báo bạn khi sử dụng một command line argument không tồn tại trong một build type nhất định.

**Tùy chọn chung**

+----------------------------+-------------------------------------------------------------------------------+
| Command                    | Description                                                                   |
+----------------------------+-------------------------------------------------------------------------------+
| ``-h``, ``--help``         | |release| Display the list of command line options.                           |
+----------------------------+-------------------------------------------------------------------------------+
| ``--version``              | |release| Display the version string.                                         |
+----------------------------+-------------------------------------------------------------------------------+
| ``-v``, ``--verbose``      | |release| Use verbose stdout mode.                                            |
+----------------------------+-------------------------------------------------------------------------------+
| ``-q``, ``--quiet``        | |release| Quiet mode, silences stdout messages. Errors are still displayed.   |
+----------------------------+-------------------------------------------------------------------------------+
| ``--no-header``            | |release| Do not print engine version and rendering method header on startup. |
+----------------------------+-------------------------------------------------------------------------------+

**Tùy chọn chạy**

+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Command                                  | Description                                                                                                                                                  |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--``, ``++``                           | |release| Separator for user-provided arguments. Following arguments are not used by the engine, but can be read from ``OS.get_cmdline_user_args()``.        |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``-e``, ``--editor``                     | |editor| Start the editor instead of running the scene.                                                                                                      |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``-p``, ``--project-manager``            | |editor| Start the Project Manager, even if a project is auto-detected.                                                                                      |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--recovery-mode``                      | |editor| Start the editor in recovery mode, which disables features that can typically cause startup crashes, such as tool scripts, editor plugins, and      |
|                                          | GDExtension addons.                                                                                                                                          |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--debug-server <uri>``                 | |editor| Start the editor debug server (``<protocol>://<host/IP>[:<port>]``, e.g. ``tcp://127.0.0.1:6007``)                                                  |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--dap-port <port>``                    | |editor| Use the specified port for the GDScript Debug Adapter Protocol. Recommended port range ``[1024, 49151]``.                                           |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--lsp-port <port>``                    | |editor| Use the specified port for the GDScript Language Server Protocol. Recommended port range ``[1024, 49151]``.                                         |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--quit``                               | |release| Quit after the first iteration.                                                                                                                    |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--quit-after``                         | |release| Quit after the given number of iterations. Set to 0 to disable.                                                                                    |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``-l``, ``--language <locale>``          | |release| Use a specific locale. ``<locale>`` follows the format ``language_Script_COUNTRY_VARIANT`` where language is a 2 or 3-letter language code in      |
|                                          | lowercase and the rest is optional. See :ref:`doc_locales` for more details.                                                                                 |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--path <directory>``                   | |extended| Path to a project (``<directory>`` must contain a "project.godot" file).                                                                          |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--scene <path>``                       | |extended| Path or UID of a scene in the project that should be started.                                                                                     |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--main-pack <file>``                   | |extended| Path to a pack (.pck) file to load.                                                                                                               |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--render-thread <mode>``               | |release| Render thread mode ("unsafe", "safe", "separate"). See :ref:`Thread Model <class_ProjectSettings_property_rendering/driver/threads/thread_model>`  |
|                                          | for more details.                                                                                                                                            |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--remote-fs <address>``                | |release| Remote filesystem (``<host/IP>[:<port>]`` address).                                                                                                |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--remote-fs-password <password>``      | |release| Password for remote filesystem.                                                                                                                    |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--audio-driver <driver>``              | |release| Audio driver. Use ``--help`` first to display the list of available drivers.                                                                       |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--display-driver <driver>``            | |release| Display driver (and rendering driver). Use ``--help`` first to display the list of available drivers.                                              |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--audio-output-latency <ms>``          | |release| Override audio output latency in milliseconds (default is 15 ms). Lower values make sound playback more reactive but increase CPU usage, and may   |
|                                          | result in audio cracking if the CPU can't keep up.                                                                                                           |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--rendering-method <renderer>``        | |release| Renderer name. Valid values are ``forward_plus``, ``mobile``, and ``gl_compatibility``. Requires driver support.                                   |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--rendering-driver <driver>``          | |release| Rendering driver (depends on display driver). Use ``--help`` first to display the list of available drivers.                                       |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--gpu-index <device_index>``           | |release| Use a specific GPU (only available on the Forward+/Mobile renderers; run with ``--verbose`` to get available device list).                         |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--text-driver <driver>``               | |release| Text driver (Fonts, BiDi, shaping).                                                                                                                |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--tablet-driver <driver>``             | |release| Pen tablet input driver.                                                                                                                           |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--headless``                           | |release| Enable headless mode (``--display-driver headless --audio-driver Dummy``). Useful for servers and with ``--script``.                               |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--log-file``                           | |release| Write output/error log to the specified path instead of the default location defined by the project. ``<file>`` path should be absolute or         |
|                                          | relative to the project directory.                                                                                                                           |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--write-movie <file>``                 | |release| Run the engine in a way that a movie is written (usually with .avi or .png extension).                                                             |
|                                          | ``--fixed-fps`` is forced when enabled, but can be used to change movie FPS.                                                                                 |
|                                          | ``--disable-vsync`` can speed up movie writing but makes interaction more difficult.                                                                         |
|                                          | ``--quit-after`` can be used to specify the number of frames to write.                                                                                       |
+------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Tùy chọn hiển thị**

+------------------------------------+----------------------------------------------------------------------------+
| Command                            | Description                                                                |
+------------------------------------+----------------------------------------------------------------------------+
| ``-f``, ``--fullscreen``           | |release| Request fullscreen mode.                                         |
+------------------------------------+----------------------------------------------------------------------------+
| ``-m``, ``--maximized``            | |release| Request a maximized window.                                      |
+------------------------------------+----------------------------------------------------------------------------+
| ``-w``, ``--windowed``             | |release| Request windowed mode.                                           |
+------------------------------------+----------------------------------------------------------------------------+
| ``-t``, ``--always-on-top``        | |release| Request an always-on-top window.                                 |
+------------------------------------+----------------------------------------------------------------------------+
| ``--resolution <W>x<H>``           | |release| Request window resolution.                                       |
+------------------------------------+----------------------------------------------------------------------------+
| ``--position <X>,<Y>``             | |release| Request window position.                                         |
+------------------------------------+----------------------------------------------------------------------------+
| ``--screen <N>``                   | |release| Request window screen.                                           |
+------------------------------------+----------------------------------------------------------------------------+
| ``--single-window``                | |release| Use a single window (no separate subwindows).                    |
+------------------------------------+----------------------------------------------------------------------------+
| ``--xr-mode <mode>``               | |release| Select XR mode ("default", "off", "on").                         |
+------------------------------------+----------------------------------------------------------------------------+
| ``--wid <window_id>``              | |release| Request parented to window.                                      |
+------------------------------------+----------------------------------------------------------------------------+
| ``--accessibility <mode>``         | |release| Select accessibility mode ["auto" (when screen reader is running,|
|                                    | default), "always", "disabled"].                                           |
+------------------------------------+----------------------------------------------------------------------------+

**Tùy chọn debug**

+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| Command                        | Description                                                                                                     |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``-d``, ``--debug``            | |release| Debug (local stdout debugger).                                                                        |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``-b``, ``--breakpoints``      | |release| Breakpoint list as source::line comma-separated pairs, no spaces (use ``%20`` instead).               |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--ignore-error-breaks``      | |release| If debugger is connected, prevents sending error breakpoints.                                         |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--profiling``                | |release| Enable profiling in the script debugger.                                                              |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--gpu-profile``              | |release| Show a GPU profile of the tasks that took the most time during frame rendering.                       |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--gpu-validation``           | |release| Enable graphics API :ref:`validation layers <doc_vulkan_validation_layers>` for debugging.            |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--gpu-abort``                | |debug| Abort on GPU errors (usually validation layer errors), may help see the problem if your system freezes. |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--generate-spirv-debug-info``| |debug| Generate SPIR-V debug information. This allows source-level shader debugging with RenderDoc.            |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--extra-gpu-memory-tracking``| |debug| Enables additional memory tracking (see class reference for                                             |
|                                | `RenderingDevice.get_driver_and_device_memory_report()` and linked methods). Currently only implemented for     |
|                                | Vulkan. Enabling this feature may cause crashes on some systems due to buggy drivers or bugs in the Vulkan      |
|                                | Loader. See https://github.com/godotengine/godot/issues/95967                                                   |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--accurate-breadcrumbs``     | |debug| Force barriers between breadcrumbs. Useful for narrowing down a command causing GPU resets. Currently   |
|                                | only implemented for Vulkan.                                                                                    |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--remote-debug <uri>``       | |release| Remote debug (``<protocol>://<host/IP>[:<port>]``, e.g. ``tcp://127.0.0.1:6007``).                    |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--single-threaded-scene``    | |release| Scene tree runs in single-threaded mode. Sub-thread groups are disabled and run on the main thread.   |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--debug-collisions``         | |debug| Show collision shapes when running the scene.                                                           |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--debug-paths``              | |debug| Show path lines when running the scene.                                                                 |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--debug-navigation``         | |debug| Show navigation polygons when running the scene.                                                        |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--debug-avoidance``          | |debug| Show navigation avoidance debug visuals when running the scene.                                         |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--debug-stringnames``        | |debug| Print all StringName allocations to stdout when the engine quits.                                       |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--debug-canvas-item-redraw`` | |debug| Display a rectangle each time a canvas item requests a redraw (useful to troubleshoot low processor     |
|                                | mode).                                                                                                          |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--max-fps <fps>``            | |release| Set a maximum number of frames per second rendered (can be used to limit power usage). A value of 0   |
|                                | results in unlimited framerate.                                                                                 |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--frame-delay <ms>``         | |release| Simulate high CPU load (delay each frame by <ms> milliseconds). Do not use as a FPS limiter; use      |
|                                | ``--max-fps`` instead.                                                                                          |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--time-scale <scale>``       | |release| Force time scale (higher values are faster, 1.0 is normal speed).                                     |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--disable-vsync``            | |release| Forces disabling of vertical synchronization, even if enabled in the project settings.                |
|                                | Does not override driver-level V-Sync enforcement.                                                              |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--disable-render-loop``      | |release| Disable render loop so rendering only occurs when called explicitly from script.                      |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--disable-crash-handler``    | |release| Disable crash handler when supported by the platform code.                                            |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--fixed-fps <fps>``          | |release| Force a fixed number of frames per second. This setting disables real-time synchronization.           |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--delta-smoothing <enable>`` | |release| Enable or disable frame delta smoothing ("enable", "disable").                                        |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--print-fps``                | |release| Print the frames per second to the stdout.                                                            |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+
| ``--editor-pseudolocalization``| |editor| Enable pseudolocalization for the editor and the project manager.                                      |
+--------------------------------+-----------------------------------------------------------------------------------------------------------------+

**Công cụ độc lập**

+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| Command                                                          | Description                                                                                                                                             |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``-s``, ``--script <script>``                                    | |extended| Run a script. ``<script>`` must be a resource path relative to the project (``myscript.gd`` will be interpreted as ``res://my_script.gd``)   |
|                                                                  | or an absolute filesystem path (for example, on Windows: ``C:/tmp/my_script.gd``).                                                                      |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--main-loop <main_loop_name>``                                 | |extended| Run a MainLoop specified by its global class name.                                                                                           |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--check-only``                                                 | |extended| Only parse for errors and quit (use with ``--script``).                                                                                      |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--import``                                                     | |editor| Starts the editor, waits for any resources to be imported, and then quits. Implies ``--editor`` and ``--quit``.                                |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--export-release <preset> <path>``                             | |editor| Export the project in release mode using the given preset and output path. The preset name should match one defined in "export_presets.cfg".   |
|                                                                  | ``<path>`` should be absolute or relative to the project directory, and include the filename for the binary (e.g. "builds/game.exe"). The target        |
|                                                                  | directory must exist.                                                                                                                                   |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--export-debug <preset> <path>``                               | |editor| Like ``--export-release``, but use debug template. Implies ``--import``.                                                                       |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--export-pack <preset> <path>``                                | |editor| Like ``--export-release``, but only export the game pack for the given preset. The ``<path>`` extension determines whether it will be in PCK   |
|                                                                  | or ZIP format. Implies ``--import``.                                                                                                                    |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--export-patch <preset> <path>``                               | |editor| Export pack with changed files only. See ``--export-pack`` description for other considerations.                                               |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--patches <paths>``                                            | |editor| List of patches to use with ``--export-patch``. The list is comma-separated.                                                                   |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--install-android-build-template``                             | |editor| Install the Android build template. Used in conjunction with ``--export-release`` or ``--export-debug``.                                       |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--convert-3to4 [<max_file_kb>] [<max_line_size>]``             | |editor| Convert project from Godot 3.x to Godot 4.x.                                                                                                   |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--validate-conversion-3to4 [<max_file_kb>] [<max_line_size>]`` | |editor| Show what elements will be renamed when converting project from Godot 3.x to Godot 4.x.                                                        |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--doctool [<path>]``                                           | |editor| Dump the engine API reference to the given ``<path>`` in XML format, merging if existing files are found.                                      |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--no-docbase``                                                 | |editor| Disallow dumping the base types (used with ``--doctool``).                                                                                     |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--gdextension-docs``                                           | |editor| Rather than dumping the engine API, generate API reference from all the GDExtensions loaded in the current project (used with                  |
|                                                                  | ``--doctool``).                                                                                                                                         |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--gdscript-docs <path>``                                       | |editor| Rather than dumping the engine API, generate API reference from the inline documentation in the GDScript files found in ``<path>``             |
|                                                                  | (used with ``--doctool``).                                                                                                                              |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--build-solutions``                                            | |editor| Build the scripting solutions (e.g. for C# projects). Implies ``--editor`` and requires a valid project to edit.                               |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--dump-gdextension-interface``                                 | |editor| Generate GDExtension header file "gdextension_interface.h" in the current folder. This file is the base file required to implement             |
|                                                                  | a GDExtension.                                                                                                                                          |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--dump-gdextension-interface-json``                            | |editor| Generate a JSON dump of the GDExtension interface named "gdextension_interface.json" in the current folder.                                    |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--dump-extension-api``                                         | |editor| Generate JSON dump of the Godot API for GDExtension bindings named "extension_api.json" in the current folder.                                 |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--dump-extension-api-with-docs``                               | |editor| Generate JSON dump of the Godot API like the previous option, but including documentation.                                                     |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--validate-extension-api <path>``                              | |editor| Validate an extension API file dumped (with the option above) from a previous version of the engine to ensure API compatibility.               |
|                                                                  | If incompatibilities or errors are detected, the return code will be non-zero.                                                                          |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--benchmark``                                                  | |editor| Benchmark the run time and print it to console.                                                                                                |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
| ``--benchmark-file <path>``                                      | |editor| Benchmark the run time and save it to a given file in JSON format. The path should be absolute.                                                |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+
|``--test [--help]``                                               | |editor| Run :ref:`unit tests <doc_unit_testing>` (requires compiling the engine with ``tests=yes``). Use ``--test --help`` for more information.       |
+------------------------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------+


Path
----

Bạn nên đặt binary editor Godot vào biến môi trường ``PATH``, để có thể dễ dàng thực thi từ bất kỳ vị trí nào bằng cách nhập ``godot``. Trên Linux, bạn có thể thực hiện việc này bằng cách đặt binary Godot vào ``/usr/local/bin`` và đảm bảo tên của nó là ``godot`` (phân biệt chữ hoa chữ thường).

Để dễ dàng thực hiện việc này trên Windows hoặc macOS, bạn có thể cài đặt Godot bằng `Scoop <https://scoop.sh>`__ (trên Windows) hoặc `Homebrew <https://brew.sh>`__ (trên macOS). Thao tác này sẽ tự động cung cấp bản sao Godot đã cài đặt trong ``PATH``:

.. tabs::

 .. code-tab:: sh Windows

    # Thêm bucket "Extras"
    scoop bucket add extras

    # Editor tiêu chuẩn:
    scoop install godot

    # Editor có hỗ trợ C# (sẽ có sẵn dưới dạng `godot-mono` trong `PATH`):
    scoop install godot-mono

 .. code-tab:: sh macOS

    # Editor tiêu chuẩn:
    brew install godot

    # Editor có hỗ trợ C# (sẽ có sẵn dưới dạng `godot-mono` trong `PATH`):
    brew install godot-mono

Thiết lập path của project
--------------------------

Tùy thuộc vào vị trí của binary Godot và current working directory, bạn có thể cần thiết lập path đến project để bất kỳ command nào sau đây hoạt động chính xác.

Khi chạy editor, bạn có thể thực hiện việc này bằng cách cung cấp path đến file ``project.godot`` của project dưới dạng argument đầu tiên, như sau:

::

    godot path_to_your_project/project.godot [other] [commands] [and] [args]

Đối với tất cả command, bạn có thể thực hiện việc này bằng cách sử dụng argument ``--path``:

::

    godot --path path_to_your_project [other] [commands] [and] [args]

Ví dụ, command đầy đủ để export game (như giải thích bên dưới) có thể trông như sau:

::

    godot --headless --path path_to_your_project --export-release my_export_preset_name game.exe

Khi bắt đầu từ một subdirectory của project, hãy sử dụng argument ``--upwards`` để Godot tự động tìm file ``project.godot`` bằng cách tìm kiếm đệ quy trong các directory cha.

Ví dụ, việc chạy một scene (như giải thích bên dưới) nằm trong một subdirectory có thể trông như sau khi current working directory của bạn ở cùng path:

::

    godot --upwards nested_scene.tscn


..

Tạo project
-----------


Bạn có thể tạo project từ dòng lệnh bằng cách điều hướng shell đến vị trí mong muốn và tạo file ``project.godot``.


::

    mkdir newgame
    cd newgame
    touch project.godot


Bây giờ có thể mở project bằng Godot.


Chạy editor
-----------

Chạy editor được thực hiện bằng cách thực thi Godot với flag ``-e``. Việc này phải được thực hiện từ trong directory của project hoặc bằng cách thiết lập path của project như đã giải thích ở trên; nếu không, command sẽ bị bỏ qua và Project Manager sẽ xuất hiện.

::

    godot -e

Khi truyền vào path đầy đủ đến file ``project.godot``, có thể bỏ qua flag ``-e``.

Nếu một scene đã được tạo và lưu, bạn có thể chỉnh sửa scene đó sau này bằng cách chạy cùng đoạn code với scene đó làm argument.

::

    godot -e scene.tscn

Xóa scene
---------

Godot thân thiện với filesystem của bạn và sẽ không tạo thêm các file metadata. Sử dụng ``rm`` để xóa một file scene. Hãy đảm bảo không có gì tham chiếu đến scene đó. Nếu không, một lỗi sẽ được đưa ra khi mở project.

::

    rm scene.tscn

Chạy game
---------

Để chạy game, hãy thực thi Godot trong directory của project hoặc với path của project như đã giải thích ở trên.

::

    godot

Lưu ý rằng việc truyền file ``project.godot`` sẽ luôn chạy editor thay vì chạy game.

Khi cần kiểm thử một scene cụ thể, hãy truyền scene đó vào dòng lệnh.

::

    godot scene.tscn

Debug
-----

Việc bắt lỗi trong dòng lệnh có thể khó khăn vì chúng cuộn qua rất nhanh. Để giải quyết việc này, một command line debugger được cung cấp bằng cách thêm ``-d``. Nó hoạt động khi chạy cả game lẫn một scene đơn.

::

    godot -d

::

    godot -d scene.tscn

.. _doc_command_line_tutorial_exporting:

Export
------

Việc export project từ dòng lệnh cũng được hỗ trợ. Điều này đặc biệt hữu ích cho các thiết lập continuous integration.

.. note::

    Việc sử dụng command line argument ``--headless`` là **bắt buộc** trên các platform không có quyền truy cập GPU (chẳng hạn như continuous integration). Trên các platform có quyền truy cập GPU, ``--headless`` ngăn không cho một cửa sổ xuất hiện trong khi project đang được export.

::

    # `godot` phải là binary editor Godot, không phải export template.
    # Ngoài ra, export template phải được cài đặt cho editor
    # (hoặc phải định nghĩa một custom export template hợp lệ trong export preset).
    godot --headless --export-release "Linux/X11" /var/builds/project
    godot --headless --export-release Android /var/builds/project.apk

Tên preset phải khớp với tên của một export preset được định nghĩa trong file ``export_presets.cfg`` của project. Nếu tên preset chứa khoảng trắng hoặc ký tự đặc biệt (chẳng hạn như "Windows Desktop"), tên đó phải được đặt trong dấu ngoặc kép.

Để export phiên bản debug của game, hãy sử dụng switch ``--export-debug`` thay cho ``--export-release``. Các tham số và cách sử dụng của chúng giống nhau.

Để chỉ export một file PCK, hãy sử dụng tùy chọn ``--export-pack`` theo sau là tên preset và output path có phần mở rộng file, thay cho ``--export-release`` hoặc ``--export-debug``. Phần mở rộng của output path xác định format của package, entweder PCK hoặc ZIP.

.. warning::

    Khi chỉ định một path tương đối làm path cho ``--export-release``, ``--export-debug`` hoặc ``--export-pack``, path sẽ tương đối với directory chứa file ``project.godot``, **không phải** tương đối với current working directory.

Chạy script
-----------

Có thể chạy một script ``.gd`` từ dòng lệnh. Tính năng này đặc biệt hữu ích trong các project lớn, ví dụ như để batch conversion asset hoặc import/export tùy chỉnh.

Script phải kế thừa từ ``SceneTree`` hoặc ``MainLoop``.

Dưới đây là một ví dụ ``sayhello.gd``, cho thấy cách hoạt động của nó:

.. code-block:: python

    #!/usr/bin/env -S godot -s
    extends SceneTree

    func _init():
        print("Hello!")
        quit()

Và cách chạy nó:

::

    # In "Hello!" ra standard output.
    godot -s sayhello.gd

Nếu không tồn tại ``project.godot`` tại path, path hiện tại được giả định là current working directory (trừ khi ``--path`` được chỉ định).

Script path sẽ được diễn giải là một resource path tương đối với project, ở đây là ``res://sayhello.gd``. Bạn cũng có thể sử dụng một filesystem path tuyệt đối, điều này hữu ích nếu script nằm bên ngoài directory của project.

Dòng đầu tiên của ``sayhello.gd`` ở trên thường được gọi là *shebang*. Nếu binary Godot nằm trong ``PATH`` của bạn dưới dạng ``godot``, nó cho phép bạn chạy script như sau trên các bản phân phối Linux hiện đại cũng như macOS:

::

    # Đánh dấu script là executable.
    chmod +x sayhello.gd
    # In "Hello!" ra standard output.
    ./sayhello.gd

Nếu cách trên không hoạt động trong phiên bản Linux hoặc macOS hiện tại của bạn, bạn luôn có thể để shebang chạy Godot trực tiếp từ vị trí của nó như sau:

::

    #!/usr/bin/godot -s
