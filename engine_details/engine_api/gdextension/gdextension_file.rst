.. _doc_gdextension_file:

Tệp .gdextension
================

Giới thiệu
----------

Tệp ``.gdextension`` trong dự án của bạn chứa các chỉ thị về cách tải GDExtension. Các chỉ thị được chia thành những phần cụ thể. Trang này cung cấp cho bạn cái nhìn tổng quan nhanh về các tùy chọn khác nhau hiện có. Để tìm hiểu cách bắt đầu với C++ (godot-cpp), hãy xem :ref:`GDExtension C++ Example <doc_godot_cpp_getting_started>`.

Phần cấu hình
-------------

+---------------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Thuộc tính                | Kiểu    | Mô tả                                                                                                                                                                                                                                           |
+===========================+=========+=================================================================================================================================================================================================================================================+
| **entry_symbol**          | String  | Tên của hàm entry dùng để khởi tạo GDExtension. Khi sử dụng godot-cpp, hàm này phải được định nghĩa trong tệp ``register_types.cpp``. Việc thêm hàm này là cần thiết để extension hoạt động.                                                    |
+---------------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **compatibility_minimum** | String  | Phiên bản tương thích tối thiểu. Điều này ngăn các phiên bản Godot cũ hơn tải những extension phụ thuộc vào các tính năng của phiên bản Godot mới hơn. **Chỉ được hỗ trợ trong Godot 4.1 trở lên**                                              |
+---------------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **compatibility_maximum** | String  | Phiên bản tương thích tối đa. Điều này ngăn các phiên bản Godot mới hơn tải extension. **Chỉ được hỗ trợ trong Godot 4.3 trở lên**                                                                                                              |
+---------------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **reloadable**            | Boolean | Tải lại extension sau khi biên dịch lại. Tính năng tải lại được hỗ trợ cho binding godot-cpp trong Godot 4.2 trở lên. Các language binding khác có thể hỗ trợ hoặc không. Cờ này chủ yếu nên được sử dụng khi phát triển hoặc gỡ lỗi extension. |
+---------------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **android_aar_plugin**    | Boolean | GDExtension là một phần của :ref:`v2 Android plugin <doc_android_plugin>`. Trong quá trình export, cờ này sẽ cho editor biết rằng các thư viện native dùng chung của GDExtension được export bởi các tệp nhị phân AAR của Android plugin.       |
+---------------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Phần thư viện
-------------

Trong phần này, bạn có thể đặt đường dẫn đến các tệp nhị phân đã biên dịch của thư viện GDExtension. Bằng cách chỉ định các feature flag, bạn có thể lọc phiên bản nào sẽ được tải và export cùng game, tùy thuộc vào các feature flag đang hoạt động. Mỗi feature flag phải khớp với feature flag của Godot hoặc cờ export tùy chỉnh của bạn thì mới được tải trong game đã export. Ví dụ ``macos.debug`` có nghĩa là nó sẽ được tải nếu Godot kích hoạt cả cờ ``macos`` và ``debug``. Mỗi dòng trong phần này được đánh giá từ trên xuống dưới.

Dưới đây là một ví dụ về cách phần này có thể được viết:

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

Đường dẫn có thể là tương đối hoặc tuyệt đối (bắt đầu bằng ``res://``). Đường dẫn tương đối được khuyến nghị vì cho phép extension tiếp tục hoạt động nếu được cài đặt vào thư mục khác với thư mục được chỉ định trong đường dẫn.

Các mục được đối chiếu theo thứ tự, vì vậy nếu hai tập thẻ tính năng có thể khớp với cùng một hệ thống, hãy đặt các mục cụ thể hơn lên trước:

.. code-block:: none

    [libraries]

    linux.release.editor.x86_64 = "./bin/libgdexample.linux.template_release.x86_64.so"
    linux.release.x86_64 = "./bin/libgdexample.linux.noeditor.template_release.x86_64.so"

Dưới đây là danh sách một số tùy chọn tích hợp có sẵn (để xem thêm, hãy xem :ref:`feature tags <doc_feature_tags>`):

Hệ thống đang chạy
~~~~~~~~~~~~~~~~~~

+--------------+-----------------------------+
| Cờ           | Mô tả                       |
+==============+=============================+
| **windows**  | Hệ điều hành Windows        |
+--------------+-----------------------------+
| **macos**    | Hệ điều hành Mac            |
+--------------+-----------------------------+
| **linux**    | Hệ điều hành Linux          |
+--------------+-----------------------------+
| **bsd**      | Hệ điều hành BSD            |
+--------------+-----------------------------+
| **linuxbsd** | Hệ điều hành Linux hoặc BSD |
+--------------+-----------------------------+
| **android**  | Hệ điều hành Android        |
+--------------+-----------------------------+
| **ios**      | Hệ điều hành iOS            |
+--------------+-----------------------------+
| **web**      | Trình duyệt web             |
+--------------+-----------------------------+

Bản build
~~~~~~~~~

+-------------+-------------------------------------------------------------------------------------+
| Cờ          | Mô tả                                                                               |
+=============+=====================================================================================+
| **debug**   | Bản build có các tính năng debug (các bản build Editor luôn có các tính năng debug) |
+-------------+-------------------------------------------------------------------------------------+
| **release** | Bản build được tối ưu hóa không có các tính năng debug                              |
+-------------+-------------------------------------------------------------------------------------+
| **editor**  | Bản build Editor                                                                    |
+-------------+-------------------------------------------------------------------------------------+

Kiến trúc
~~~~~~~~~

+------------+------------------------------------+
| Cờ         | Mô tả                              |
+============+====================================+
| **double** | bản build độ chính xác kép         |
+------------+------------------------------------+
| **single** | bản build độ chính xác đơn         |
+------------+------------------------------------+
| **x86_64** | bản build x86 64-bit               |
+------------+------------------------------------+
| **arm64**  | bản build ARM 64-bit               |
+------------+------------------------------------+
| **rv64**   | bản build RISC-V 64-bit            |
+------------+------------------------------------+
| **riscv**  | bản build RISC-V (mọi độ rộng bit) |
+------------+------------------------------------+
| **wasm32** | bản build WebAssembly 32-bit       |
+------------+------------------------------------+

Phần biểu tượng
---------------

Theo mặc định, Godot sử dụng biểu tượng Node trong scene dock cho các node GDExtension. Có thể đặt biểu tượng tùy chỉnh bằng cách tham chiếu đến tên và đường dẫn tài nguyên của một tệp SVG.

Ví dụ:

.. code-block:: none

    [icons]

    GDExample = "res://icons/gd_example.svg"

Đường dẫn phải trỏ đến một hình ảnh SVG kích thước 16×16 pixel, với hai tùy chọn được bật cho hình ảnh trong Import dock:

- **Editor > Scale with Editor Scale**.
- **Editor > Convert Colors with Editor Theme**.

Bật cả hai tùy chọn đảm bảo biểu tượng hoạt động giống các biểu tượng có sẵn của trình chỉnh sửa nhất có thể. Đọc hướng dẫn về :ref:`tạo biểu tượng <doc_editor_icons>` để biết thêm thông tin.

Phần dependency
---------------

Trong phần này, bạn đặt đường dẫn của các dependency GDExtension. Các đường dẫn này được dùng nội bộ để xuất dependency khi xuất tệp thực thi game. Bạn có thể đặt dependency nào được tải dựa trên các feature flag của tệp thực thi đã xuất. Ngoài ra, bạn có thể đặt một thư mục con tùy chọn để chuyển các dependency vào đó. Nếu không cung cấp đường dẫn, Godot sẽ chuyển các thư viện vào cùng thư mục với tệp thực thi game.

.. warning::

    Trên macOS, các thư viện dùng chung cần nằm trong một thư mục có tên là ``Frameworks`` với cấu trúc thư mục như sau: ``Game.app/Contents/Frameworks``.

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
