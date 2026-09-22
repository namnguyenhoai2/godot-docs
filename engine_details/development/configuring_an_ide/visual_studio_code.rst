.. _doc_configuring_an_ide_vscode:

Visual Studio Code
==================

.. note::

    Tài liệu này dành cho việc đóng góp cho game engine, không phải để sử dụng Visual Studio Code làm trình soạn thảo C# hoặc GDScript. Để viết mã C# hoặc GDScript trong trình soạn thảo bên ngoài, hãy xem
    :ref:`hướng dẫn C# để cấu hình trình soạn thảo bên ngoài <doc_c_sharp_setup_external_editor>` hoặc
    :ref:`hướng dẫn GDScript về cách sử dụng trình soạn thảo văn bản bên ngoài <doc_external_editor>`.

`Visual Studio Code <https://code.visualstudio.com>`_ là trình soạn thảo mã đa nền tảng miễn phí do `Microsoft <https://microsoft.com>`_ phát triển (không nên nhầm lẫn với :ref:`doc_configuring_an_ide_vs`).

Importing the project
---------------------

- Hãy đảm bảo đã cài đặt tiện ích C/C++. Bạn có thể tìm thấy hướng dẫn trong `tài liệu chính thức <https://code.visualstudio.com/docs/languages/cpp>`_. Ngoài ra, có thể sử dụng `clangd <https://open-vsx.org/extension/llvm-vs-code-extensions/vscode-clangd>`_.
- Khi sử dụng tiện ích clangd, hãy chạy ``scons compiledb=yes``.
- Từ màn hình chính của Visual Studio Code, mở thư mục gốc Godot bằng **File > Open Folder...**.
- Nhấn :kbd:`Ctrl + Shift + P` để mở cửa sổ dòng lệnh và nhập *Configure Task*.

.. figure:: img/vscode_configure_task.png
   :align: center

- Chọn tùy chọn **Create tasks.json file from template**.

.. figure:: img/vscode_create_tasksjson.png
   :align: center

- Sau đó chọn **Others**.

.. figure:: img/vscode_create_tasksjson_others.png
   :align: center

- Nếu không có tùy chọn **Create tasks.json file from template**, hãy xóa tệp đó nếu nó đã tồn tại trong thư mục của bạn hoặc tự tạo tệp ``.vscode/tasks.json``. Xem `Tasks in Visual Studio Code <https://code.visualstudio.com/docs/editor/tasks#_custom-tasks>`_ để biết thêm chi tiết về các task.

- Trong tệp ``tasks.json``, tìm mảng ``"tasks"`` và thêm một phần mới vào đó:

  .. code-block:: js
    :caption: .vscode/tasks.json

    {
      "label": "build",
      "group": "build",
      "type": "shell",
      "command": "scons",
      "args": [
        // bật để debug với breakpoint
        "dev_build=yes",
      ],
      "problemMatcher": "$msCompile"
    }

.. figure:: img/vscode_3_tasks.json.png
   :figclass: figure-w480
   :align: center

   Ví dụ về ``tasks.json`` đã được điền đầy đủ.

Các đối số có thể khác nhau tùy theo thiết lập và nhu cầu của bạn. Xem
:ref:`doc_introduction_to_the_buildsystem` để biết danh sách đầy đủ các đối số.

Debugging the project
---------------------

Để chạy và debug project, bạn cần tạo một cấu hình mới trong tệp ``launch.json``.

- Nhấn :kbd:`Ctrl + Shift + D` để mở bảng Run.
- Nếu thiếu tệp ``launch.json``, bạn sẽ được nhắc tạo tệp mới.

.. figure:: img/vscode_1_create_launch.json.png
   :align: center

- Chọn **C++ (GDB/LLDB)**. Tại đây có thể có một tùy chọn dành riêng cho nền tảng khác. Nếu chọn tùy chọn đó, hãy điều chỉnh ví dụ cấu hình được cung cấp cho phù hợp.
- Trong tệp ``launch.json``, tìm mảng ``"configurations"`` và thêm một phần mới vào đó:

.. tabs::
  .. code-tab:: js LinuxBSD

    {
      "name": "Launch Project",
      "type": "lldb",
      "request": "launch",
      // Change to godot.linuxbsd.editor.dev.x86_64.llvm for llvm-based builds.
      "program": "${workspaceFolder}/bin/godot.linuxbsd.editor.dev.x86_64",
      // Change the arguments below for the project you want to test with.
      // To run the project instead of editing it, remove the "--editor" argument.
      "args": [ "--editor", "--path", "path-to-your-godot-project-folder" ],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "preLaunchTask": "build"
    }
  .. code-tab:: js LinuxBSD_gdb

    {
      "name": "Launch Project",
      "type": "cppdbg",
      "request": "launch",
      // Change to godot.linuxbsd.editor.dev.x86_64.llvm for llvm-based builds.
      "program": "${workspaceFolder}/bin/godot.linuxbsd.editor.dev.x86_64",
      // Change the arguments below for the project you want to test with.
      // To run the project instead of editing it, remove the "--editor" argument.
      "args": [ "--editor", "--path", "path-to-your-godot-project-folder" ],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "setupCommands":
      [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        },
        {
            "description": "Load custom pretty-printers for Godot types.",
            "text": "source ${workspaceRoot}/misc/utility/godot_gdb_pretty_print.py"
        }
      ],
      "preLaunchTask": "build"
    }

  .. code-tab:: js Windows

    {
      "name": "Launch Project",
      "type": "cppvsdbg",
      "request": "launch",
      "program": "${workspaceFolder}/bin/godot.windows.editor.dev.x86_64.exe",
      // Change the arguments below for the project you want to test with.
      // To run the project instead of editing it, remove the "--editor" argument.
      "args": [ "--editor", "--path", "path-to-your-godot-project-folder" ],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "console": "internalConsole",
      "visualizerFile": "${workspaceFolder}/platform/windows/godot.natvis",
      "preLaunchTask": "build"
    }

  .. code-tab:: js macOS_x86_64

    {
      "name": "Launch Project",
      "type": "lldb",
      "request": "launch",
      "program": "${workspaceFolder}/bin/godot.macos.editor.x86_64",
      // Change the arguments below for the project you want to test with.
      // To run the project instead of editing it, remove the "--editor" argument.
      "args": ["--editor", "--path", "path-to-your-godot-project-folder"],
      "cwd": "${workspaceFolder}",
      "preLaunchTask": "build"
    }

  .. code-tab:: js macOS_arm64

    {
      "name": "Launch Project",
      "type": "lldb",
      "request": "launch",
      "program": "${workspaceFolder}/bin/godot.macos.editor.arm64",
      // Change the arguments below for the project you want to test with.
      // To run the project instead of editing it, remove the "--editor" argument.
      "args": ["--editor", "--path", "path-to-your-godot-project-folder"],
      "cwd": "${workspaceFolder}",
      "preLaunchTask": "build"
    }

.. figure:: img/vscode_2_launch.json.png
   :figclass: figure-w480
   :align: center

   Ví dụ về ``launch.json`` đã được điền đầy đủ.


.. note::

    Do các vấn đề hiệu năng xảy ra không thường xuyên, bạn nên sử dụng LLDB thay cho GDB trên các hệ thống dựa trên Unix. Hãy đảm bảo đã cài đặt tiện ích `CodeLLDB extension <https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb>`_ cho các cấu hình sử dụng `lldb`.

    Nếu gặp vấn đề với lldb, bạn có thể cân nhắc sử dụng gdb (xem cấu hình LinuxBSD_gdb).

    Lưu ý rằng lldb có thể hoạt động tốt hơn với các bản build dựa trên LLVM. Xem :ref:`doc_compiling_for_linuxbsd` để biết thêm thông tin.

Tên trong ``program`` phụ thuộc vào cấu hình build của bạn, chẳng hạn như ``godot.linuxbsd.editor.dev.x86_64`` cho nền tảng LinuxBSD 64-bit với ``target=editor`` và ``dev_build=yes``.

Configuring IntelliSense
------------------------

Đối với tiện ích C/C++:

Để khắc phục các lỗi include có thể gặp phải, bạn cần cấu hình một số thiết lập trong tệp ``c_cpp_properties.json``.

- Trước tiên, hãy đảm bảo build project vì cần tạo một số tệp.

- Chỉnh sửa tệp C/C++ Configuration bằng giao diện người dùng hoặc bằng văn bản:

.. figure:: img/vscode_edit_configurations.webp
   :align: center

- Thêm đường dẫn include cho nền tảng của bạn, ví dụ: ``${workspaceFolder}/platform/windows``.

- Thêm các define cho editor ``TOOLS_ENABLED``, các bản build debug ``DEBUG_ENABLED`` và các bản test ``TESTS_ENABLED``.

- Hãy đảm bảo đường dẫn compiler được cấu hình chính xác đến compiler bạn đang sử dụng. Xem :ref:`doc_introduction_to_the_buildsystem` để biết thêm thông tin về nền tảng của bạn.

- Tệp ``c_cpp_properties.json`` trên Windows sẽ có dạng tương tự như sau:

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

  - Có thể thêm đối số này vào build task trong ``tasks.json`` vì cần chạy nó mỗi khi tệp được thêm hoặc di chuyển.

Linting class reference XML files
---------------------------------

Để lint các tệp XML tham chiếu class, hãy cài đặt `vscode-xml extension <https://marketplace.visualstudio.com/items?itemName=redhat.vscode-xml>`__.

Displaying documentation on hover
---------------------------------

Bằng cách cài đặt `Godot Hover Docs extension <https://marketplace.visualstudio.com/items?itemName=RedMser.godot-hover-docs>`__, bạn có thể hiển thị tài liệu tham chiếu class khi di chuột qua các symbol trong tệp nguồn hoặc tệp header C++. Thông tin được lấy từ các tệp XML cục bộ nên có thể hoạt động ngoại tuyến.

.. note::

    Tính năng này chỉ có tác dụng với các symbol được ghi tài liệu trong XML tham chiếu class, tức là những symbol được exposed cho scripting API. Các symbol nội bộ của engine sẽ không hiển thị tài liệu khi di chuột qua, trừ khi chúng có comment ngay phía trên phần khai báo.

Troubleshooting
---------------

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.

.. _`Visual Studio Code`: https://code.visualstudio.com
.. _`Microsoft`: https://microsoft.com
.. _`official documentation`: https://code.visualstudio.com/docs/languages/cpp
.. _`clangd`: https://open-vsx.org/extension/llvm-vs-code-extensions/vscode-clangd
.. _`Tasks in Visual Studio Code`: https://code.visualstudio.com/docs/editor/tasks#_custom-tasks
.. _`CodeLLDB extension`: https://marketplace.visualstudio.com/items?itemName=vadimcn.vscode-lldb
