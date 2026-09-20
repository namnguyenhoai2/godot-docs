.. _doc_godot_cpp_build_system:

Hệ thống build chính: Làm việc với SCons
========================================

.. seealso:: This page documents how to compile godot-cpp. If you're looking to compile Godot instead, see
             :ref:`doc_introduction_to_the_buildsystem`.

`godot-cpp <https://github.com/godotengine/godot-cpp>`__ sử dụng `SCons <https://scons.org>`__ làm hệ thống build chính. Nó được mô phỏng theo :ref:`Godot's build system <doc_compiling_index>`, và một số lệnh có sẵn ở đó cũng có trong các dự án godot-cpp.

Bắt đầu
-------

Để build một dự án godot-cpp, thông thường bạn chỉ cần cài đặt `SCons <https://scons.org>`__, rồi chạy nó trong thư mục dự án:

    scons

Bạn có thể muốn tìm hiểu về các tùy chọn có sẵn:

    scons --help

Để build lại dự án một cách sạch sẽ, hãy thêm ``--clean`` vào lệnh build của bạn:

    scons --clean

Bạn có thể tìm thêm thông tin về các đối số SCons phổ biến và các mẫu build trong `SCons User Guide <https://scons.org/doc/latest/HTML/scons-user/index.html>`__. Các dự án godot-cpp riêng lẻ có thể bổ sung thêm lệnh, vì vậy hãy tham khảo tài liệu cụ thể của chúng để biết thêm thông tin.

Cấu hình IDE
------------

Hầu hết IDE có thể sử dụng tệp ``compile_commands.json`` để hiểu một dự án C++. Bạn có thể tạo tệp này bằng godot-cpp với lệnh sau:

.. code-block:: shell

   # Tạo compile_commands.json trong khi biên dịch.
   scons compiledb=yes

   # Tạo compile_commands.json mà không biên dịch.
   scons compiledb=yes compile_commands.json

Để biết thêm thông tin, vui lòng xem :ref:`IDE configuration guides <doc_configuring_an_ide>`. Mặc dù được viết cho những người đóng góp cho Godot engine, phần lớn nội dung cũng áp dụng cho các dự án godot-cpp.

Nạp GDExtension của bạn vào Godot
---------------------------------

Godot nạp các GDExtension bằng cách tìm các tệp :ref:`.gdextension <doc_gdextension_file>` trong thư mục dự án. Các tệp ``.gdextension`` được dùng để chọn và nạp một binary tương thích với máy tính / hệ điều hành hiện tại.

`godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__, cũng như
:ref:`Getting Started section <doc_godot_cpp_getting_started>`, provide example ``.gdextension`` files for GDExtensions
có khả năng tương thích rộng rãi với nhiều hệ thống khác nhau.

Build cho nhiều nền tảng
------------------------

GDExtension được kỳ vọng sẽ chạy trên nhiều hệ thống khác nhau, mỗi hệ thống có binary và cấu hình build riêng. Nếu dự định phát hành GDExtension, chúng tôi khuyến nghị bạn cung cấp binary cho tất cả các cấu hình được đề cập trong `godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__ `.gdextension file <https://github.com/godotengine/godot-cpp-template/blob/main/demo/bin/example.gdextension>`__.

Có hai cách phổ biến để thực hiện build đa nền tảng:

- Công cụ build đa nền tảng - Continuous Integration (CI)

`godot-cpp-template <https://github.com/godotengine/godot-cpp-template>`__ chứa một `example setup <https://github.com/godotengine/godot-cpp-template/tree/main/.github/workflows>`__ cho quy trình CI dựa trên GitHub.

Sử dụng tệp API tùy chỉnh
-------------------------

Mỗi branch của godot-cpp đều đi kèm một tệp API (``extension_api.json``) phù hợp với phiên bản Godot tương ứng (ví dụ: branch ``4.3`` đi kèm tệp API tương thích với Godot phiên bản ``4.3`` trở lên).

Tuy nhiên, bạn có thể muốn sử dụng một ``extension_api.json`` tùy chỉnh, chẳng hạn như:

* Nếu bạn muốn sử dụng các API mới nhất từ Godot ``master``. * Nếu bạn :ref:`build Godot yourself <doc_compiling_index>` với các tùy chọn khác với các bản build chính thức (ví dụ: ``disable_3d=yes`` hoặc ``precision=double``). * Nếu bạn muốn sử dụng các API được cung cấp bởi các module tùy chỉnh.

Để sử dụng tệp API tùy chỉnh, trước tiên bạn phải tạo tệp này từ executable Godot phù hợp:

.. code-block:: shell

    godot --dump-extension-api

Tệp ``extension_api.json`` được tạo sẽ nằm trong thư mục của executable. Để sử dụng tệp này, bạn có thể thêm ``custom_api_file`` vào lệnh build của mình:

.. code-block:: shell

    scons platform=<platform> custom_api_file=<PATH_TO_FILE>

Ngoài ra, bạn có thể đặt tệp này làm tệp API mặc định cho dự án bằng cách thêm dòng sau vào tệp SConstruct:

.. code-block:: python

    localEnv["custom_api_file"] = "extension_api.json"
