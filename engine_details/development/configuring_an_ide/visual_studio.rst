.. _doc_configuring_an_ide_vs:

Visual Studio
=============

`Visual Studio Community <https://visualstudio.microsoft.com>`__ là một IDE chỉ dành cho Windows do `Microsoft <https://microsoft.com>`_ phát triển, miễn phí cho mục đích sử dụng cá nhân hoặc sử dụng phi thương mại trong các tổ chức. IDE này có nhiều tính năng hữu ích, chẳng hạn như chế độ xem bộ nhớ, chế độ xem hiệu suất, quản lý mã nguồn và nhiều tính năng khác.

.. note::

    Tài liệu này dành cho việc đóng góp cho game engine, không phải sử dụng Visual Studio làm trình soạn thảo C#. Để viết mã C# trong một trình soạn thảo bên ngoài, hãy xem
    :ref:`the C# guide to configure an external editor <doc_c_sharp_setup_external_editor>`.

Nhập dự án
----------

Visual Studio yêu cầu một tệp solution để làm việc với một dự án. Mặc dù Godot không đi kèm tệp solution, bạn có thể tạo tệp này bằng SCons.

- Đi đến thư mục gốc của Godot và mở cửa sổ Command Prompt hoặc PowerShell. - | Chạy ``scons platform=windows vsproj=yes dev_build=yes`` để tạo solution cùng với các ký hiệu gỡ lỗi. | Tham số ``vsproj`` báo hiệu rằng bạn muốn tạo solution Visual Studio. | Tham số ``dev_build`` đảm bảo các ký hiệu gỡ lỗi được đưa vào, cho phép bạn, chẳng hạn, thực thi từng bước mã bằng các điểm ngắt. - Bây giờ bạn có thể mở dự án bằng cách nhấp đúp vào ``godot.sln`` trong thư mục gốc của dự án hoặc sử dụng tùy chọn **Open a project or solution** trong Visual Studio. - Sử dụng menu trên cùng **Build** để build dự án.

.. warning:: Visual Studio must be configured with the C++ package. It can be selected
             trong trình cài đặt:

             .. figure:: img/vs_1_install_cpp_package.png
                :align: center

Gỡ lỗi dự án
------------

Visual Studio có một trình gỡ lỗi mạnh mẽ. Trình gỡ lỗi này cho phép người dùng kiểm tra mã nguồn của Godot, dừng tại các điểm cụ thể trong mã, kiểm tra ngữ cảnh thực thi hiện tại và thực hiện các thay đổi trực tiếp đối với mã nguồn.

Bạn có thể khởi chạy dự án với trình gỡ lỗi được đính kèm bằng tùy chọn **Debug > Start Debugging** trong menu trên cùng. Tuy nhiên, trừ khi bạn muốn gỡ lỗi riêng Project Manager, trước tiên bạn cần cấu hình các tùy chọn gỡ lỗi. Nguyên nhân là khi Godot Project Manager mở một dự án, tiến trình ban đầu sẽ bị kết thúc và trình gỡ lỗi bị tách khỏi tiến trình đó.

- Để cấu hình các tùy chọn khởi chạy dùng với trình gỡ lỗi, hãy chọn **Project > Properties** từ menu trên cùng:

.. figure:: img/vs_2_project_properties.png
   :align: center

- Mở phần **Debugging** và trong **Command Arguments**, thêm hai đối số mới: cờ ``-e`` sẽ mở trình soạn thảo thay vì Project Manager, còn đối số ``--path`` yêu cầu tệp thực thi mở dự án được chỉ định (phải được cung cấp dưới dạng đường dẫn *tuyệt đối* đến thư mục gốc của dự án, không phải tệp ``project.godot``; nếu đường dẫn chứa khoảng trắng, hãy nhớ đặt đường dẫn trong dấu ngoặc kép).

.. figure:: img/vs_3_debug_command_line.webp
   :align: center

Để tìm hiểu thêm về các đối số dòng lệnh, hãy tham khảo
:ref:`command line tutorial <doc_command_line_tutorial>`.

Ngay cả khi bạn khởi động dự án mà không đính kèm trình gỡ lỗi, bạn vẫn có thể kết nối trình gỡ lỗi với tiến trình đang chạy bằng menu **Debug > Attach to Process...**.

Để kiểm tra mọi thứ đang hoạt động, hãy đặt một điểm ngắt trong ``main.cpp`` và nhấn :kbd:`F5` để bắt đầu gỡ lỗi.

.. figure:: img/vs_4_debugging_main.png
   :align: center

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.
