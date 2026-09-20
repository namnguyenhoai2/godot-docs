.. _doc_configuring_an_ide_vscode:

Visual Studio Code
==================

.. note::

    Tài liệu này dành cho việc đóng góp cho game engine, không phải sử dụng Visual Studio Code làm trình chỉnh sửa C# hoặc GDScript. Để viết mã C# hoặc GDScript trong một trình chỉnh sửa bên ngoài, hãy xem
    :ref:`the C# guide to configure an external editor <doc_c_sharp_setup_external_editor>` or
    :ref:`the GDScript guide to using an external text editor <doc_external_editor>`.

`Visual Studio Code <https://code.visualstudio.com>`_ là một trình chỉnh sửa mã nguồn miễn phí, đa nền tảng do `Microsoft <https://microsoft.com>`_ phát triển (không nên nhầm lẫn với :ref:`doc_configuring_an_ide_vs`).

Nhập dự án
----------

- Hãy đảm bảo tiện ích mở rộng C/C++ đã được cài đặt. Bạn có thể tìm thấy hướng dẫn trong `tài liệu chính thức <https://code.visualstudio.com/docs/languages/cpp>`_. Ngoài ra, bạn có thể sử dụng `clangd <https://open-vsx.org/extension/llvm-vs-code-extensions/vscode-clangd>`_. - Khi sử dụng tiện ích mở rộng clangd, hãy chạy ``scons compiledb=yes``. - Từ màn hình chính của Visual Studio Code, mở thư mục gốc của Godot bằng **File > Open Folder...**. - Nhấn :kbd:`Ctrl + Shift + P` để mở cửa sổ dấu nhắc lệnh và nhập *Configure Task*.

.. figure:: img/vscode_configure_task.png
   :align: center

- Chọn tùy chọn **Create tasks.json file from template**.

.. figure:: img/vscode_create_tasksjson.png
   :align: center

- Sau đó chọn **Others**.

.. figure:: img/vscode_create_tasksjson_others.png
   :align: center

- Nếu không có tùy chọn **Create tasks.json file from template**, hãy xóa tệp đó nếu nó đã tồn tại trong thư mục của bạn hoặc tự tạo tệp ``.vscode/tasks.json``. Xem `Tasks in Visual Studio Code <https://code.visualstudio.com/docs/editor/tasks#_custom-tasks>`_ để biết thêm chi tiết về các tác vụ.

- Trong tệp ``tasks.json``, tìm mảng ``"tasks"`` và thêm một phần mới vào đó:

  .. code-block:: js
    :caption: .vscode/tasks.json

    {
      "label": "build",
      "group": "build",
      "type": "shell",
      "command": "scons",
      "args": [
        // enable for debugging with breakpoints
        "dev_build=yes",
      ],
      "problemMatcher": "$msCompile"
    }

.. figure:: img/vscode_3_tasks.json.png
   :figclass: figure-w480
   :align: center

   An example of a filled out ``tasks.json``.

Các đối số có thể khác nhau tùy theo thiết lập và nhu cầu của bạn. Xem
:ref:`doc_introduction_to_the_buildsystem` for a full list of arguments.

Gỡ lỗi dự án
------------

Để chạy và gỡ lỗi dự án, bạn cần tạo một cấu hình mới trong tệp ``launch.json``.

- Nhấn :kbd:`Ctrl + Shift + D` để mở bảng Run. - Nếu thiếu tệp ``launch.json``, bạn sẽ được nhắc tạo một tệp mới.

.. figure:: img/vscode_1_create_launch.json.png
   :align: center

- Chọn **C++ (GDB/LLDB)**. Có thể ở đây sẽ có một tùy chọn dành riêng cho nền tảng khác. Nếu chọn tùy chọn đó, hãy điều chỉnh ví dụ cấu hình được cung cấp cho phù hợp. - Trong tệp ``launch.json``, tìm mảng ``"configurations"`` và thêm một phần mới vào đó:

.. tabs::
  .. code-tab:: js LinuxBSD

    { "name": "Launch Project", "type": "lldb", "request": "launch", // Change to godot.linuxbsd.editor.dev.x86_64.llvm for llvm-based builds. "program": "${workspaceFolder}/bin/godot.linuxbsd.editor.dev.x86_64", // Change the arguments below for the project you want to test with. // To run the project instead of editing it, remove the "--editor" argument. "args": [ "--editor", "--path", "path-to-your-godot-project-folder" ], "stopAtEntry": false, "cwd": "${workspaceFolder}", "environment": [], "externalConsole": false, "preLaunchTask": "build" }
  .. code-tab:: js LinuxBSD_gdb

    { "name": "Launch Project", "type": "cppdbg", "request": "launch", // Change to godot.linuxbsd.editor.dev.x86_64.llvm for llvm-based builds. "program": "${workspaceFolder}/bin/godot.linuxbsd.editor.dev.x86_64", // Change the arguments below for the project you want to test with. // To run the project instead of editing it, remove the "--editor" argument. "args": [ "--editor", "--path", "path-to-your-godot-project-folder" ], "stopAtEntry": false, "cwd": "${workspaceFolder}", "environment": [], "externalConsole": false, "setupCommands": [ { "description": "Enable pretty-printing for gdb", "text": "-enable-pretty-printing", "ignoreFailures": true }, { "description": "Load custom pretty-printers for Godot types.", "text": "source ${workspaceRoot}/misc/utility/godot_gdb_pretty_print.py" } ], "preLaunchTask": "build" }

  .. code-tab:: js Windows

    { "name": "Launch Project", "type": "cppvsdbg", "request": "launch", "program": "${workspaceFolder}/bin/godot.windows.editor.dev.x86_64.exe", // Change the arguments below for the project you want to test with. // To run the project instead of editing it, remove the "--editor" argument. "args": [ "--editor", "--path", "path-to-your-godot-project-folder" ], "stopAtEntry": false, "cwd": "${workspaceFolder}", "environment": [], "console": "internalConsole", "visualizerFile": "${workspaceFolder}/platform/windows/godot.natvis", "preLaunchTask": "build" }

  .. code-tab:: js macOS_x86_64

    { "name": "Launch Project", "type": "lldb", "request": "launch", "program": "${workspaceFolder}/bin/godot.macos.editor.x86_64", // Change the arguments below for the project you want to test with. // To run the project instead of editing it, remove the "--editor" argument. "args": ["--editor", "--path", "path-to-your-godot-project-folder"], "cwd": "${workspaceFolder}", "preLaunchTask": "build" }

  .. code-tab:: js macOS_arm64

    { "name": "Launch Project", "type": "lldb", "request": "launch", "program": "${workspaceFolder}/bin/godot.macos.editor.arm64", // Change the arguments below for the project you want to test with. // To run the project instead of editing it, remove the "--editor" argument. "args": ["--editor", "--path", "path-to-your-godot-project-folder"], "cwd": "${workspaceFolder}", "preLaunchTask": "build" }

.. figure:: img/vscode_2_launch.json.png
   :figclass: figure-w480
   :align: center

   An example of a filled out ``launch.json``.


.. note::

    Do các vấn đề hiệu năng xảy ra không thường xuyên, nên sử dụng LLDB thay cho GDB trên các hệ thống dựa trên Unix. Hãy đảm bảo `CodeLLDB extension <https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb>`_ đã được cài đặt cho các cấu hình sử dụng `lldb`.

    Nếu gặp sự cố với lldb, bạn có thể cân nhắc sử dụng gdb (xem cấu hình LinuxBSD_gdb).

    Lưu ý rằng lldb có thể hoạt động tốt hơn với các bản dựng dựa trên LLVM. Xem :ref:`doc_compiling_for_linuxbsd` để biết thêm thông tin.

Tên trong ``program`` phụ thuộc vào cấu hình bản dựng của bạn, ví dụ ``godot.linuxbsd.editor.dev.x86_64`` dành cho nền tảng LinuxBSD 64 bit với ``target=editor`` và ``dev_build=yes``.

Cấu hình IntelliSense
---------------------

Đối với tiện ích mở rộng C/C++:

Để khắc phục các lỗi include có thể gặp phải, bạn cần cấu hình một số thiết lập trong tệp ``c_cpp_properties.json``.

- Trước tiên, hãy đảm bảo đã xây dựng dự án vì một số tệp cần được tạo.

- Chỉnh sửa tệp C/C++ Configuration bằng giao diện người dùng hoặc bằng văn bản:

.. figure:: img/vscode_edit_configurations.webp
   :align: center

- Thêm đường dẫn include cho nền tảng của bạn, ví dụ ``${workspaceFolder}/platform/windows``.

- Thêm các define cho editor ``TOOLS_ENABLED``, các bản dựng debug ``DEBUG_ENABLED`` và các bài kiểm thử ``TESTS_ENABLED``.

- Hãy đảm bảo đường dẫn trình biên dịch được cấu hình chính xác cho trình biên dịch bạn đang sử dụng. Xem :ref:`doc_introduction_to_the_buildsystem` để biết thêm thông tin về nền tảng của bạn.

- Tệp ``c_cpp_properties.json`` sẽ có dạng tương tự như sau đối với Windows:

  .. code-block:: js
    :caption: .vscode/c_cpp_properties.json

    {
      "configurations": [
        {
          "name": "Win32",
          "includePath": [
            "${workspaceFolder}/**",
            "${workspaceFolder}/platform/windows"
          ],
          "defines": [
            "_DEBUG",
            "UNICODE",
            "_UNICODE",
            "TOOLS_ENABLED",
            "DEBUG_ENABLED",
            "TESTS_ENABLED"
          ],
          "windowsSdkVersion": "10.0.22621.0",
          "compilerPath": "C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.39.33519/bin/Hostx64/x64/cl.exe",
          "cStandard": "c17",
          "cppStandard": "c++17",
          "intelliSenseMode": "windows-msvc-x64"
        }
      ],
      "version": 4
    }

- Ngoài ra, bạn có thể sử dụng đối số scons ``compiledb=yes`` và đặt thiết lập compile commands ``compileCommands`` thành ``compile_commands.json``, nằm trong phần nâng cao của giao diện C/C++ Configuration.

  - Bạn có thể thêm đối số này vào tác vụ build trong ``tasks.json`` vì tác vụ này sẽ cần được chạy mỗi khi tệp được thêm hoặc di chuyển.

Lint các tệp XML tham chiếu lớp
-------------------------------

Để lint các tệp XML tham chiếu lớp, hãy cài đặt `vscode-xml extension <https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml>`__.

Hiển thị tài liệu khi di chuột
------------------------------

Bằng cách cài đặt `Godot Hover Docs extension <https://marketplace.visualstudio.com/items?itemName=RedMser.godot-hover-docs>`__, bạn có thể hiển thị tài liệu tham chiếu lớp khi di chuột lên các ký hiệu trong tệp mã nguồn hoặc tệp tiêu đề C++. Thông tin được lấy từ các tệp XML cục bộ nên có thể hoạt động ngoại tuyến.

.. note::

    Tính năng này chỉ có hiệu lực với các ký hiệu được ghi lại trong XML tham chiếu lớp, tức là những ký hiệu được cung cấp cho API lập trình. Các ký hiệu nội bộ của engine sẽ không hiển thị tài liệu khi di chuột, trừ khi chúng có chú thích ngay phía trên khai báo.

Khắc phục sự cố
---------------

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.
