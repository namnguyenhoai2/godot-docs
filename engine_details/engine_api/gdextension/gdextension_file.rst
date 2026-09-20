.. _doc_gdextension_file:

Tệp .gdextension
================

Giới thiệu
----------

Tệp ``.gdextension`` trong dự án của bạn chứa các chỉ dẫn về cách tải GDExtension. Các chỉ dẫn được phân tách thành những phần cụ thể. Trang này cung cấp cho bạn cái nhìn tổng quan nhanh về các tùy chọn khác nhau hiện có. Để tìm hiểu cách bắt đầu với C++ (godot-cpp), hãy xem :ref:`GDExtension C++ Example <doc_godot_cpp_getting_started>`.

Phần cấu hình
-------------

+-------------------------------+------------+------------------------------------------------------------------------------------------------------+
| Thuộc tính | Kiểu | Mô tả |
+++++++++++++++++++++++++++++
| **entry_symbol** | String | Tên của hàm entry để khởi tạo GDExtension. Hàm này phải được định nghĩa trong | | | | tệp ``register_types.cpp`` khi sử dụng godot-cpp. Việc thêm thuộc tính này là cần thiết để extension |
| | | hoạt động. |
++++++++++++++++++
| **compatibility_minimum** | String | Phiên bản tương thích tối thiểu. Điều này ngăn các phiên bản Godot cũ hơn tải những extension |
| | | phụ thuộc vào các tính năng từ những phiên bản Godot mới hơn. **Chỉ được hỗ trợ trong Godot 4.1 trở lên** |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **compatibility_maximum** | String | Phiên bản tương thích tối đa. Điều này ngăn các phiên bản Godot mới hơn tải extension. |
| | | **Chỉ được hỗ trợ trong Godot 4.3 trở lên** |
+++++++++++++++++++++++++++++++++++++++++++++++++++
| **reloadable** | Boolean | Tải lại extension sau khi biên dịch lại. Việc tải lại được hỗ trợ cho binding godot-cpp trong | | | | Godot 4.2 trở lên. Các binding ngôn ngữ khác có thể hỗ trợ hoặc không. Cờ này chủ yếu nên được |
| | | sử dụng để phát triển hoặc gỡ lỗi extension. |
++++++++++++++++++++++++++++++++++++++++++++++++++++
| **android_aar_plugin** | Boolean | GDExtension là một phần của :ref:`v2 Android plugin <doc_android_plugin>`. Khi xuất, cờ này | | | | sẽ cho trình biên tập biết rằng các thư viện chia sẻ native của GDExtension được xuất bởi các tệp nhị phân |
| | | AAR của plugin Android. |
+++++++++++++++++++++++++++++++

Phần thư viện
-------------

Trong phần này, bạn có thể thiết lập đường dẫn đến các tệp nhị phân đã biên dịch của thư viện GDExtension. Bằng cách chỉ định các cờ tính năng, bạn có thể lọc phiên bản nào sẽ được tải và xuất cùng trò chơi, tùy thuộc vào các cờ tính năng đang hoạt động. Mỗi cờ tính năng phải khớp với các cờ tính năng của Godot hoặc các cờ xuất tùy chỉnh của bạn để được tải trong trò chơi đã xuất. Ví dụ, ``macos.debug`` có nghĩa là nó sẽ được tải nếu Godot có cả cờ ``macos`` và ``debug`` đang hoạt động. Mỗi dòng trong phần này được đánh giá từ trên xuống dưới.

Dưới đây là một ví dụ về cách phần này có thể trông như thế nào:

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

Đường dẫn có thể là tương đối hoặc tuyệt đối (bắt đầu bằng ``res://``). Khuyến nghị sử dụng đường dẫn tương đối vì chúng cho phép extension tiếp tục hoạt động nếu được cài đặt vào một thư mục khác với thư mục được chỉ định trong đường dẫn.

Các mục được đối chiếu theo thứ tự, vì vậy nếu hai tập thẻ tính năng có thể khớp với cùng một hệ thống, hãy đảm bảo đặt các mục cụ thể hơn trước:

.. code-block:: none

    [libraries]

    linux.release.editor.x86_64 = "./bin/libgdexample.linux.template_release.x86_64.so"
    linux.release.x86_64 = "./bin/libgdexample.linux.noeditor.template_release.x86_64.so"

Dưới đây là danh sách một số tùy chọn tích hợp sẵn hiện có (xem :ref:`feature tags <doc_feature_tags>` để biết thêm):

Hệ thống đang chạy
~~~~~~~~~~~~~~~~~~

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Cờ | Mô tả |
++++++++++++++
| **windows** | Hệ điều hành Windows |
++++++++++++++++++++++++++++++++++++++
| **macos** | Hệ điều hành Mac |
++++++++++++++++++++++++++++++++
| **linux** | Hệ điều hành Linux |
++++++++++++++++++++++++++++++++++
| **bsd** | Hệ điều hành BSD |
++++++++++++++++++++++++++++++
| **linuxbsd** | Hệ điều hành Linux hoặc BSD |
++++++++++++++++++++++++++++++++++++++++++++++
| **android** | Hệ điều hành Android |
++++++++++++++++++++++++++++++++++++++
| **ios** | Hệ điều hành iOS |
++++++++++++++++++++++++++++++
| **web** | Trình duyệt web |
+++++++++++++++++++++++++++++

Bản dựng
~~~~~~~~

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Cờ | Mô tả |
++++++++++++++
| **debug** | Bản dựng có các tính năng gỡ lỗi (các bản dựng trình biên tập luôn có các tính năng gỡ lỗi) |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **release** | Bản dựng được tối ưu hóa không có các tính năng gỡ lỗi |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **editor** | Bản dựng trình biên tập |
++++++++++++++++++++++++++++++++++++++++

Kiến trúc
~~~~~~~~~

+-------------------------------+------------------------------------------------------------------------------------------------------+
| Cờ | Mô tả |
++++++++++++++
| **double** | Bản dựng độ chính xác kép |
++++++++++++++++++++++++++++++++++++++++++
| **single** | Bản dựng độ chính xác đơn |
++++++++++++++++++++++++++++++++++++++++++
| **x86_64** | Bản dựng x86 64-bit |
++++++++++++++++++++++++++++++++++++
| **arm64** | Bản dựng ARM 64-bit |
+++++++++++++++++++++++++++++++++++
| **rv64** | Bản dựng RISC-V 64-bit |
+++++++++++++++++++++++++++++++++++++
| **riscv** | Bản dựng RISC-V (bất kỳ số bit nào) |
+++++++++++++++++++++++++++++++++++++++++++++++++++
| **wasm32** | Bản dựng WebAssembly 32-bit |
++++++++++++++++++++++++++++++++++++++++++++

Phần biểu tượng
---------------

Theo mặc định, Godot sử dụng biểu tượng Node trong dock scene cho các node GDExtension. Có thể đặt biểu tượng tùy chỉnh bằng cách tham chiếu đến tên và đường dẫn tài nguyên của một tệp SVG.

Ví dụ:

.. code-block:: none

    [icons]

    GDExample = "res://icons/gd_example.svg"

Đường dẫn phải trỏ đến một hình ảnh SVG có kích thước 16×16 pixel, với hai tùy chọn được bật trên hình ảnh trong dock Import:

- **Editor > Scale with Editor Scale**. - **Editor > Convert Colors with Editor Theme**.

Việc bật cả hai tùy chọn đảm bảo biểu tượng hoạt động gần giống nhất có thể với các biểu tượng trình biên tập có sẵn. Đọc hướng dẫn về :ref:`creating icons <doc_editor_icons>` để biết thêm thông tin.

Phần phụ thuộc
--------------

Trong phần này, bạn thiết lập đường dẫn đến các phần phụ thuộc của GDExtension. Đường dẫn này được sử dụng nội bộ để xuất các phần phụ thuộc khi xuất tệp thực thi trò chơi. Bạn có thể thiết lập phần phụ thuộc nào được tải tùy thuộc vào các cờ tính năng của tệp thực thi đã xuất. Ngoài ra, bạn có thể thiết lập một thư mục con tùy chọn để di chuyển các phần phụ thuộc vào đó. Nếu không cung cấp đường dẫn, Godot sẽ di chuyển các thư viện vào cùng thư mục với tệp thực thi trò chơi.

.. warning::

    Trên macOS, các thư viện chia sẻ cần nằm trong một thư mục có tên là ``Frameworks`` với cấu trúc thư mục như sau: ``Game.app/Contents/Frameworks``.

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
