:allow_comments: False

Gỡ lỗi
======

Phần này chứa các trang hướng dẫn nếu bạn đang xem mã nguồn engine để tìm một vấn đề tiềm ẩn hoặc một khả năng tối ưu hóa.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-cpp-debug-profiling

   using_sanitizers
   macos_debug
   vulkan/index

Gỡ lỗi trình chỉnh sửa
----------------------

Khi làm việc trên trình chỉnh sửa Godot, hãy nhớ rằng theo mặc định, tệp thực thi sẽ khởi động ở chế độ Project Manager. Việc mở một dự án từ Project Manager sẽ tạo một tiến trình mới, khiến phiên gỡ lỗi dừng lại. Để tránh điều đó, bạn nên khởi chạy trực tiếp vào dự án bằng các tùy chọn khởi chạy ``-e`` và ``--path``.

Ví dụ, khi sử dụng trực tiếp ``gdb``, bạn có thể thực hiện như sau:

.. code-block:: none

    gdb godot
    > run -e --path ~/myproject

Bạn cũng có thể chạy trực tiếp trình chỉnh sửa từ thư mục dự án của mình. Trong trường hợp đó, chỉ cần tùy chọn ``-e``.

.. code-block:: none

    cd ~/myproject
    gdb godot
    > run -e

Bạn có thể tìm hiểu thêm về các tùy chọn khởi chạy này và những tham số dòng lệnh khác trong :ref:`command line tutorial <doc_command_line_tutorial>`.

Nếu bạn đang sử dụng trình chỉnh sửa mã hoặc IDE để gỡ lỗi Godot, hãy xem
:ref:`configuration guides <doc_configuring_an_ide>`, which cover the setup
quy trình xây dựng và gỡ lỗi bằng trình chỉnh sửa cụ thể của bạn.
