.. _doc_gdextension_file:

Tệp .gdextension
================

Giới thiệu
----------

Tệp ``.gdextension`` trong dự án của bạn chứa các hướng dẫn về cách tải GDExtension. Các hướng dẫn được chia thành những phần cụ thể. Trang này cung cấp cho bạn phần tổng quan nhanh về các tùy chọn khác nhau hiện có. Để tìm hiểu cách bắt đầu với C++ (godot-cpp), hãy xem :ref:`GDExtension C++ Example <doc_godot_cpp_getting_started>`.

Phần Configuration
------------------

+-------------------------------+------------+------------------------------------------------------------------------------------------------------+
| Property                      | Type       | Description                                                                                          |
+===============================+============+======================================================================================================+
| **entry_symbol**              | String     | Name of the entry function for initializing the GDExtension. This function should be defined in      |
|                               |            | the ``register_types.cpp`` file when using godot-cpp. Adding this is necessary for the extension to  |
|                               |            | work.                                                                                                |
+-------------------------------+------------+------------------------------------------------------------------------------------------------------+
| **compatibility_minimum**     | String     | Minimum compatible version. This prevents older versions of Godot from loading extensions that       |
|                               |            | depend on features from newer versions of Godot. **Only supported in Godot 4.1 or later**            |
+-------------------------------+------------+------------------------------------------------------------------------------------------------------+
| **compatibility_maximum**     | String     | Maximum compatible version. This prevents newer versions of Godot from loading the extension.        |
|                               |            | **Only supported in Godot 4.3 or later**                                                             |
+-------------------------------+------------+------------------------------------------------------------------------------------------------------+
| **reloadable**                | Boolean    | Reloads the extension upon recompilation. Reloading is supported for the godot-cpp binding in        |
|                               |            | Godot 4.2 or later. Other language bindings may or may not support it as well. This flag should be   |
|                               |            | mainly used for developing or debugging an extension.                                                |
+-------------------------------+------------+------------------------------------------------------------------------------------------------------+
| **android_aar_plugin**        | Boolean    | The GDExtension is part of a :ref:`v2 Android plugin <doc_android_plugin>`. During export this flag  |
|                               |            | will indicate to the editor that the GDExtension native shared libraries are exported by the Android |
|                               |            | plugin AAR binaries.                                                                                 |
+-------------------------------+------------+------------------------------------------------------------------------------------------------------+

Phần Libraries
--------------

Trong phần này, bạn có thể đặt các đường dẫn đến binary đã biên dịch của các thư viện GDExtension. Bằng cách chỉ định các feature flag, bạn có thể lọc phiên bản nào sẽ được tải và xuất cùng game, tùy thuộc vào các feature flag đang được kích hoạt. Mọi feature flag phải khớp với feature flag của Godot hoặc các cờ xuất tùy chỉnh của bạn để được tải trong game đã xuất. Ví dụ, ``macos.debug`` có nghĩa là nó sẽ được tải nếu Godot đang kích hoạt cả cờ ``macos`` và ``debug``. Mỗi dòng trong phần này được đánh giá từ trên xuống dưới.

Dưới đây là ví dụ về cách phần này có thể được viết:

.. code-block:: none

    ; A comment line starts with a semicolon. This line is ignored by the engine.
    [libraries]

    macos.debug = "./bin/libgdexample.macos.template_debug.dylib" ; Inline comments are also allowed.
    macos.release = "./bin/libgdexample.macos.template_release.dylib"
    windows.debug.x86_32 = "./bin/libgdexample.windows.template_debug.x86_32.dll"
    windows.release.x86_32 = "./bin/libgdexample.windows.template_release.x86_32.dll"
    windows.debug.x86_64 = "./bin/libgdexample.windows.template_debug.x86_64.dll"
    windows.release.x86_64 = "./bin/libgdexample.windows.template_release.x86_64.dll"
    linux.debug.x86_64 = "./bin/libgdexample.linux.template_debug.x86_64.so"
    linux.release.x86_64 = "./bin/libgdexample.linux.template_release.x86_64.so"
    linux.debug.arm64 = "./bin/libgdexample.linux.template_debug.arm64.so"
    linux.release.arm64 = "./bin/libgdexample.linux.template_release.arm64.so"
    linux.debug.rv64 = "./bin/libgdexample.linux.template_debug.rv64.so"
    linux.release.rv64 = "./bin/libgdexample.linux.template_release.rv64.so"

Các đường dẫn có thể là tương đối hoặc tuyệt đối (bắt đầu bằng ``res://``). Khuyến nghị sử dụng đường dẫn tương đối, vì chúng cho phép extension tiếp tục hoạt động nếu được cài đặt vào một thư mục khác với thư mục được chỉ định trong đường dẫn.

Các mục được đối chiếu theo thứ tự, vì vậy nếu hai tập feature tag có thể khớp với cùng một hệ thống, hãy đặt các mục cụ thể hơn trước:

.. code-block:: none

    [libraries]

    linux.release.editor.x86_64 = "./bin/libgdexample.linux.template_release.x86_64.so"
    linux.release.x86_64 = "./bin/libgdexample.linux.noeditor.template_release.x86_64.so"

Dưới đây là danh sách một số tùy chọn tích hợp có sẵn (để xem thêm, hãy truy cập :ref:`feature tags <doc_feature_tags>`):

Hệ thống đang chạy
~~~~~~~~~~~~~~~~~~

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Flag                          | Description                                                                                          |
+===============================+======================================================================================================+
| **windows**                   | Windows operating system                                                                             |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **macos**                     | Mac operating system                                                                                 |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **linux**                     | Linux operating system                                                                               |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **bsd**                       | BSD operating system                                                                                 |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **linuxbsd**                  | Linux or BSD operating system                                                                        |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **android**                   | Android operating system                                                                             |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **ios**                       | iOS operating system                                                                                 |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **web**                       | Web browser                                                                                          |
+-------------------------------+------------------------------------------------------------------------------------------------------+

Bản build
~~~~~~~~~

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Flag                          | Description                                                                                          |
+===============================+======================================================================================================+
| **debug**                     | Build with debugging features (editor builds always have debugging features)                         |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **release**                   | Optimized build without debugging features                                                           |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **editor**                    | Editor build                                                                                         |
+-------------------------------+------------------------------------------------------------------------------------------------------+

Kiến trúc
~~~~~~~~~

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Flag                          | Description                                                                                          |
+===============================+======================================================================================================+
| **double**                    | double-precision build                                                                               |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **single**                    | single-precision build                                                                               |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **x86_64**                    | 64-bit x86 build                                                                                     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **arm64**                     | 64-bit ARM build                                                                                     |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **rv64**                      | 64-bit RISC-V build                                                                                  |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **riscv**                     | RISC-V build (any bitness)                                                                           |
+-------------------------------+------------------------------------------------------------------------------------------------------+
| **wasm32**                    | 32-bit WebAssembly build                                                                             |
+-------------------------------+------------------------------------------------------------------------------------------------------+

Phần Icons
----------

Theo mặc định, Godot sử dụng biểu tượng Node trong scene dock cho các node GDExtension. Bạn có thể đặt biểu tượng tùy chỉnh bằng cách tham chiếu đến tên và đường dẫn tài nguyên của tệp SVG.

Ví dụ:

.. code-block:: none

    [icons]

    GDExample = "res://icons/gd_example.svg"

Đường dẫn phải trỏ đến một hình ảnh SVG có kích thước 16×16 pixel, với hai tùy chọn được bật cho hình ảnh trong Import dock:

- **Editor > Scale with Editor Scale**. - **Editor > Convert Colors with Editor Theme**.

Việc bật cả hai tùy chọn đảm bảo biểu tượng hoạt động gần giống nhất có thể với các biểu tượng có sẵn trong editor. Đọc hướng dẫn về :ref:`creating icons <doc_editor_icons>` để biết thêm thông tin.

Phần Dependencies
-----------------

Trong phần này, bạn đặt các đường dẫn đến dependencies của GDExtension. Các đường dẫn này được sử dụng nội bộ để xuất dependencies khi xuất executable của game. Bạn có thể đặt dependency nào được tải tùy thuộc vào các feature flag của executable đã xuất. Ngoài ra, bạn có thể đặt một thư mục con tùy chọn để chuyển dependencies vào đó. Nếu không cung cấp đường dẫn, Godot sẽ chuyển các thư viện vào cùng thư mục với executable của game.

.. warning::

    Trên macOS, các shared library cần nằm trong một thư mục có tên ``Frameworks`` với cấu trúc thư mục như sau: ``Game.app/Contents/Frameworks``.

.. code-block:: none

    [dependencies]

    macos.debug = {
        "res://bin/libdependency.macos.template_debug.framework" : "Contents/Frameworks"
    }
    macos.release = {
        "res://bin/libdependency.macos.template_release.framework" : "Contents/Frameworks"
    }
    windows.debug = {
        "res://bin/libdependency.windows.template_debug.x86_64.dll" : "",
        "res://bin/libdependency.windows.template_debug.x86_32.dll" : ""
    }
    windows.release = {
        "res://bin/libdependency.windows.template_release.x86_64.dll" : "",
        "res://bin/libdependency.windows.template_release.x86_32.dll" : ""
    }
    linux.debug = {
        "res://bin/libdependency.linux.template_debug.x86_64.so" : "",
        "res://bin/libdependency.linux.template_debug.arm64.so" : "",
        "res://bin/libdependency.linux.template_debug.rv64.so" : ""
    }
    linux.release = {
        "res://bin/libdependency.linux.template_release.x86_64.so" : "",
        "res://bin/libdependency.linux.template_release.arm64.so" : "",
        "res://bin/libdependency.linux.template_release.rv64.so" : ""
    }
