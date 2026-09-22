.. _doc_configuring_an_ide_vs:

Visual Studio
=============

`Visual Studio Community <https://visualstudio.microsoft.com>`__ là một IDE chỉ dành cho Windows do `Microsoft <https://microsoft.com>`_ phát triển, miễn phí cho cá nhân hoặc mục đích phi thương mại trong các tổ chức. IDE này có nhiều tính năng hữu ích như chế độ xem bộ nhớ, chế độ xem hiệu năng, source control và nhiều tính năng khác.

.. note::

    Tài liệu này dành cho việc đóng góp cho game engine, không phải hướng dẫn sử dụng Visual Studio làm trình soạn thảo C#. Để viết mã C# trong một trình soạn thảo bên ngoài, hãy xem
    :ref:`hướng dẫn C# để cấu hình trình soạn thảo bên ngoài <doc_c_sharp_setup_external_editor>`.

Nhập project
------------

Visual Studio yêu cầu một solution file để làm việc với một project. Godot không đi kèm solution file, nhưng bạn có thể tạo file này bằng SCons.

- Đi đến thư mục gốc của Godot và mở cửa sổ Command Prompt hoặc PowerShell.
- | Chạy ``scons platform=windows vsproj=yes dev_build=yes`` để tạo solution kèm debug symbols.
  | Tham số ``vsproj`` cho biết bạn muốn tạo solution của Visual Studio.
  | Tham số ``dev_build`` đảm bảo debug symbols được đưa vào, cho phép bạn chẳng hạn như chạy từng bước qua mã bằng breakpoint.
- Bây giờ bạn có thể mở project bằng cách nhấp đúp vào ``godot.sln`` trong thư mục gốc của project hoặc sử dụng tùy chọn **Open a project or solution** trong Visual Studio.
- Sử dụng menu trên cùng **Build** để build project.

.. warning:: Visual Studio phải được cấu hình với gói C++. Bạn có thể chọn gói này trong trình cài đặt:

             .. figure:: img/vs_1_install_cpp_package.png
                :align: center

Gỡ lỗi project
--------------

Visual Studio có một debugger mạnh mẽ. Công cụ này cho phép người dùng xem xét mã nguồn của Godot, dừng tại các điểm cụ thể trong mã, kiểm tra ngữ cảnh thực thi hiện tại và thực hiện các thay đổi trực tiếp đối với codebase.

Bạn có thể khởi chạy project với debugger được đính kèm bằng tùy chọn **Debug > Start Debugging** từ menu trên cùng. Tuy nhiên, trừ khi bạn muốn gỡ lỗi riêng Project Manager, trước tiên bạn cần cấu hình các tùy chọn gỡ lỗi. Nguyên nhân là khi Godot Project Manager mở một project, process ban đầu sẽ bị kết thúc và debugger bị tách ra.

- Để cấu hình các tùy chọn khởi chạy dùng với debugger, hãy sử dụng **Project > Properties** từ menu trên cùng:

.. figure:: img/vs_2_project_properties.png
   :align: center

- Mở phần **Debugging** và trong **Command Arguments**, thêm hai đối số mới: cờ ``-e`` sẽ mở editor thay vì Project Manager, còn đối số ``--path`` yêu cầu executable mở project được chỉ định (phải cung cấp dưới dạng đường dẫn *absolute* đến thư mục gốc của project, không phải tệp ``project.godot``; nếu đường dẫn chứa khoảng trắng, hãy nhớ đặt nó trong dấu ngoặc kép).

.. figure:: img/vs_3_debug_command_line.webp
   :align: center

Để tìm hiểu thêm về các đối số dòng lệnh, hãy tham khảo
:ref:`hướng dẫn về dòng lệnh <doc_command_line_tutorial>`.

Ngay cả khi bạn khởi động project mà không đính kèm debugger, bạn vẫn có thể kết nối debugger với process đang chạy bằng menu **Debug > Attach to Process...**.

Để kiểm tra mọi thứ có hoạt động hay không, hãy đặt một breakpoint trong ``main.cpp`` và nhấn :kbd:`F5` để bắt đầu gỡ lỗi.

.. figure:: img/vs_4_debugging_main.png
   :align: center

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.

.. _`Microsoft`: https://microsoft.com
