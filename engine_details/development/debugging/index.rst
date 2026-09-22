:allow_comments: False

Gỡ lỗi
======

Phần này chứa các trang hướng dẫn khi bạn đang xem xét mã nguồn của engine để tìm nguyên nhân sự cố hoặc khả năng tối ưu hóa.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-cpp-debug-profiling

   using_sanitizers
   macos_debug
   vulkan/index

Gỡ lỗi editor
-------------

Khi làm việc với Godot editor, hãy nhớ rằng theo mặc định, tệp thực thi sẽ khởi động ở chế độ Project Manager. Việc mở một project từ Project Manager sẽ tạo một tiến trình mới, khiến phiên gỡ lỗi dừng lại. Để tránh điều đó, bạn nên khởi chạy trực tiếp vào project bằng các tùy chọn khởi chạy ``-e`` và ``--path``.

Ví dụ, sử dụng trực tiếp ``gdb``, bạn có thể thực hiện như sau:

.. code-block:: none

    gdb godot
    > run -e --path ~/myproject

Bạn cũng có thể chạy editor trực tiếp từ thư mục của project. Trong trường hợp đó, chỉ cần tùy chọn ``-e``.

.. code-block:: none

    cd ~/myproject
    gdb godot
    > run -e

Bạn có thể tìm hiểu thêm về các tùy chọn khởi chạy này và những đối số dòng lệnh khác trong :ref:`hướng dẫn dòng lệnh <doc_command_line_tutorial>`.

Nếu bạn đang sử dụng trình soạn thảo mã hoặc IDE để gỡ lỗi Godot, hãy xem
:ref:`hướng dẫn cấu hình <doc_configuring_an_ide>`, trong đó trình bày quy trình thiết lập để build và gỡ lỗi bằng trình soạn thảo cụ thể của bạn.
