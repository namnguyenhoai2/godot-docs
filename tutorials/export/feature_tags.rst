.. _doc_feature_tags:

Thẻ tính năng
=============

Giới thiệu
----------

Godot có một hệ thống đặc biệt để gắn thẻ cho tính khả dụng của các tính năng. Mỗi *tính năng* được biểu diễn dưới dạng một chuỗi, có thể đề cập đến nhiều mục sau:

* Tên nền tảng. * Kiến trúc nền tảng (64-bit hoặc 32-bit, x86 hoặc ARM). * Loại nền tảng (desktop, mobile, Web). * Các thuật toán nén texture được nền tảng hỗ trợ. * Việc một bản build là ``debug`` hay ``release`` (``debug`` bao gồm editor). * Việc project đang chạy từ editor hay một binary "standalone". * Còn nhiều mục khác.

Có thể truy vấn các thẻ tính năng trong runtime từ API singleton bằng cách gọi:

.. tabs::
 .. code-tab:: gdscript

    OS.has_feature(name)

 .. code-tab:: csharp

    OS.HasFeature(name);

Các thẻ tính năng của OS được GDExtension sử dụng để xác định những library nào cần load. Ví dụ, một library dành cho ``linux.debug.editor.x86_64`` sẽ chỉ được load trên bản debug editor cho Linux x86_64.

Các tính năng mặc định
----------------------

Sau đây là danh sách hầu hết các thẻ tính năng trong Godot. Hãy lưu ý rằng chúng **phân biệt chữ hoa chữ thường**:

+----------------------+-----------------------------------------------------------------------------------------+
| **Feature tag**      | **Description**                                                                         |
+======================+=========================================================================================+
| **android**          | Running on Android (but not within a Web browser)                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **bsd**              | Running on \*BSD (but not within a Web browser)                                         |
+----------------------+-----------------------------------------------------------------------------------------+
| **linux**            | Running on Linux (but not within a Web browser)                                         |
+----------------------+-----------------------------------------------------------------------------------------+
| **macos**            | Running on macOS (but not within a Web browser)                                         |
+----------------------+-----------------------------------------------------------------------------------------+
| **ios**              | Running on iOS (but not within a Web browser)                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **visionos**         | Running on visionOS (but not within a Web browser)                                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **windows**          | Running on Windows                                                                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **linuxbsd**         | Running on Linux or \*BSD                                                               |
+----------------------+-----------------------------------------------------------------------------------------+
| **debug**            | Running on a debug build (including the editor)                                         |
+----------------------+-----------------------------------------------------------------------------------------+
| **release**          | Running on a release build                                                              |
+----------------------+-----------------------------------------------------------------------------------------+
| **editor**           | Running on an editor build                                                              |
+----------------------+-----------------------------------------------------------------------------------------+
| **editor_hint**      | Running on an editor build, and inside the editor                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **editor_runtime**   | Running on an editor build, and running the project                                     |
+----------------------+-----------------------------------------------------------------------------------------+
| **template**         | Running on a non-editor (export template) build                                         |
+----------------------+-----------------------------------------------------------------------------------------+
| **double**           | Running on a double-precision build                                                     |
+----------------------+-----------------------------------------------------------------------------------------+
| **single**           | Running on a single-precision build                                                     |
+----------------------+-----------------------------------------------------------------------------------------+
| **64**               | Running on a 64-bit build (any architecture)                                            |
+----------------------+-----------------------------------------------------------------------------------------+
| **32**               | Running on a 32-bit build (any architecture)                                            |
+----------------------+-----------------------------------------------------------------------------------------+
| **x86_64**           | Running on a 64-bit x86 build                                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **x86_32**           | Running on a 32-bit x86 build                                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **x86**              | Running on an x86 build (any bitness)                                                   |
+----------------------+-----------------------------------------------------------------------------------------+
| **arm64**            | Running on a 64-bit ARM build                                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **arm32**            | Running on a 32-bit ARM build                                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **arm**              | Running on an ARM build (any bitness)                                                   |
+----------------------+-----------------------------------------------------------------------------------------+
| **rv64**             | Running on a 64-bit RISC-V build                                                        |
+----------------------+-----------------------------------------------------------------------------------------+
| **riscv**            | Running on a RISC-V build (any bitness)                                                 |
+----------------------+-----------------------------------------------------------------------------------------+
| **ppc64**            | Running on a 64-bit PowerPC build                                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **ppc32**            | Running on a 32-bit PowerPC build                                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **ppc**              | Running on a PowerPC build (any bitness)                                                |
+----------------------+-----------------------------------------------------------------------------------------+
| **wasm64**           | Running on a 64-bit WebAssembly build (not yet possible)                                |
+----------------------+-----------------------------------------------------------------------------------------+
| **wasm32**           | Running on a 32-bit WebAssembly build                                                   |
+----------------------+-----------------------------------------------------------------------------------------+
| **wasm**             | Running on a WebAssembly build (any bitness)                                            |
+----------------------+-----------------------------------------------------------------------------------------+
| **mobile**           | Host OS is a mobile platform                                                            |
+----------------------+-----------------------------------------------------------------------------------------+
| **pc**               | Host OS is a PC platform (desktop/laptop)                                               |
+----------------------+-----------------------------------------------------------------------------------------+
| **web**              | Host OS is a Web browser                                                                |
+----------------------+-----------------------------------------------------------------------------------------+
| **nothreads**        | Running without threading support                                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **threads**          | Running with threading support                                                          |
+----------------------+-----------------------------------------------------------------------------------------+
| **web_android**      | Host OS is a Web browser running on Android                                             |
+----------------------+-----------------------------------------------------------------------------------------+
| **web_ios**          | Host OS is a Web browser running on iOS                                                 |
+----------------------+-----------------------------------------------------------------------------------------+
| **web_linuxbsd**     | Host OS is a Web browser running on Linux or \*BSD                                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **web_macos**        | Host OS is a Web browser running on macOS                                               |
+----------------------+-----------------------------------------------------------------------------------------+
| **web_windows**      | Host OS is a Web browser running on Windows                                             |
+----------------------+-----------------------------------------------------------------------------------------+
| **etc**              | Textures using ETC1 compression are supported                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **etc2**             | Textures using ETC2 compression are supported                                           |
+----------------------+-----------------------------------------------------------------------------------------+
| **s3tc**             | Textures using S3TC (DXT/BC) compression are supported                                  |
+----------------------+-----------------------------------------------------------------------------------------+
| **movie**            | :ref:`Movie Maker mode <doc_creating_movies>` is active                                 |
+----------------------+-----------------------------------------------------------------------------------------+
| **shader_baker**     | Project was exported with :ref:`shader baking <doc_pipeline_compilations_shader_baker>` |
|                      | enabled (only applies to the exported project, not when running in the editor)          |
+----------------------+-----------------------------------------------------------------------------------------+
| **dedicated_server** | Project was exported as a :ref:`dedicated server <doc_exporting_for_dedicated_servers>` |
|                      | (only applies to the exported project, not when running in the editor)                  |
+----------------------+-----------------------------------------------------------------------------------------+

.. warning::

    Ngoại trừ các thẻ tính năng về texture compression, ``web_<platform>`` và ``movie``, các thẻ tính năng mặc định là **bất biến**. Điều này có nghĩa là chúng *sẽ không* thay đổi tùy theo các điều kiện runtime. Ví dụ, ``OS.has_feature("mobile")`` sẽ trả về ``false`` khi chạy một project được export sang Web trên thiết bị di động.

    Để kiểm tra xem một project được export sang Web có đang chạy trên thiết bị di động hay không, hãy sử dụng ``OS.has_feature("web_android") or OS.has_feature("web_ios")``.

Tính năng tùy chỉnh
-------------------

Bạn có thể thêm các tính năng tùy chỉnh vào một bản build; hãy sử dụng trường tương ứng trong *export preset* được dùng để tạo bản build đó:

.. image:: img/feature_tags1.webp

.. note::

    Các thẻ tính năng tùy chỉnh chỉ được sử dụng khi chạy project đã export (bao gồm cả khi sử dụng :ref:`doc_one-click_deploy`). Chúng **không được sử dụng** khi chạy project từ editor, ngay cả khi export preset được đánh dấu là **Runnable** cho nền tảng hiện tại của bạn có khai báo các thẻ tính năng tùy chỉnh.

    Các thẻ tính năng tùy chỉnh cũng không được sử dụng trong các script :ref:`class_EditorExportPlugin`. Thay vào đó, các thẻ tính năng trong :ref:`class_EditorExportPlugin` sẽ phản ánh thiết bị mà editor hiện đang chạy trên đó.

Ghi đè các thiết lập của project
--------------------------------

Có thể sử dụng các tính năng để ghi đè những giá trị cấu hình cụ thể trong *Project Settings*. Điều này cho phép bạn tùy chỉnh tốt hơn bất kỳ cấu hình nào khi thực hiện một bản build.

Trong ví dụ sau, một icon khác được thêm vào cho bản build demo của game (được tùy chỉnh trong một export preset đặc biệt; đến lượt mình, preset này chỉ bao gồm các level demo).

.. figure:: img/feature_tags2.webp
    :alt: The Project Settings panel

    The desired configuration is selected, which effectively copies its properties to the panel above (1). The "demo_build" feature tag is selected (2). The configuration is added to the project settings (3).

Sau khi ghi đè, một trường mới được thêm vào cho cấu hình cụ thể này.

.. image:: img/feature_tags3.webp

.. note::

    Khi sử dụng
    :ref:`project settings "override.cfg" functionality <class_ProjectSettings>`
    (không liên quan đến các thẻ tính năng), hãy nhớ rằng các thẻ tính năng vẫn được áp dụng. Do đó, hãy nhớ *đồng thời* ghi đè thiết lập bằng các thẻ tính năng mong muốn nếu bạn muốn chúng ghi đè các thiết lập cơ sở của project trên mọi nền tảng và cấu hình.

Các ghi đè mặc định
-------------------

Đã có rất nhiều thiết lập đi kèm với các ghi đè theo mặc định; bạn có thể tìm thấy chúng trong nhiều phần của project settings.

.. image:: img/feature_tags4.webp

Tính đến các thẻ tính năng khi đọc các thiết lập của project
------------------------------------------------------------

Theo mặc định, các thẻ tính năng **không** được tính đến khi đọc các thiết lập của project bằng những cách tiếp cận thông thường (:ref:`ProjectSettings.get_setting<class_ProjectSettings_method_get_setting>` hoặc :ref:`ProjectSettings.get <class_Object_private_method__get>`). Thay vào đó, bạn phải sử dụng :ref:`ProjectSettings.get_setting_with_override <class_ProjectSettings_method_get_setting>`.

Ví dụ, với các thiết lập project sau:

::

    [section]

    subsection/example = "Release"
    subsection/example.debug = "Debug"

Việc sử dụng ``ProjectSettings.get_setting("section/subsection/example")`` sẽ trả về ``"Release"`` bất kể hiện đang chạy bản debug hay không. Mặt khác, ``ProjectSettings.get_setting_with_override("section/subsection/example")`` sẽ tuân theo các thẻ tính năng và trả về ``"Debug"`` nếu đang sử dụng bản debug.

Tùy chỉnh bản build
-------------------

Các thẻ tính năng cũng có thể được sử dụng để tùy chỉnh quy trình build bằng cách viết một **ExportPlugin** tùy chỉnh. Chúng cũng được sử dụng để chỉ định shared library nào được load và export trong **GDExtension**.
