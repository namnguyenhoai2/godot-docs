.. _doc_configuring_an_ide_rider:

JetBrains Rider
===============

`JetBrains Rider <https://www.jetbrains.com/rider/>`_ là một IDE thương mại `JetBrains <https://www.jetbrains.com/>`_ dành cho C++, C# và GDScript, sử dụng cùng hệ thống solution như Visual Studio.

.. note::

    Tài liệu này dành cho việc đóng góp cho game engine, không dành cho việc sử dụng JetBrains Rider làm trình chỉnh sửa C# hoặc GDScript. Để viết mã C# hoặc GDScript trong một trình chỉnh sửa bên ngoài, hãy xem
    :ref:`the C# guide to configure an external editor <doc_c_sharp_setup_external_editor>`.

Nhập project
------------

.. tip:: If you already use Visual Studio as your main IDE, you can use the same solution file in Rider.
         Rider và Visual Studio sử dụng cùng định dạng solution, vì vậy bạn có thể chuyển đổi giữa hai IDE mà không cần xây dựng lại tệp solution. Cần thay đổi các cấu hình gỡ lỗi khi chuyển từ IDE này sang IDE khác.

Nếu bạn bắt đầu từ đầu, vui lòng làm theo :ref:`instructions<doc_compiling_index>`, cụ thể là:

- Cài đặt tất cả các dependency. - Xác định lệnh scons để biên dịch cho một nền tảng cụ thể.

Cung cấp cho scons các tham số bổ sung để yêu cầu tạo tệp solution:

- Thêm `vsproj=yes dev_build=yes` vào lệnh scons

Tham số ``vsproj`` cho biết bạn muốn tạo solution Visual Studio. Tham số ``dev_build`` đảm bảo các ký hiệu gỡ lỗi được đưa vào, cho phép bạn, chẳng hạn, đi qua từng dòng mã bằng các breakpoint.

.. note:: Each SCons run only generates the ``.generated.props`` file for a single
          Cấu hình Solution. Vui lòng chạy SCons một lần cho mỗi target bạn định sử dụng:

          .. code-block:: shell

             scons vsproj=yes dev_build=yes target=editor
             scons vsproj=yes dev_build=yes target=template_debug
             scons vsproj=yes dev_build=yes target=template_release

- Mở ``godot.sln`` đã tạo trong Rider.

.. note:: Ensure that the appropriate Solution configuration is selected on the
          Thanh công cụ Rider. Thanh công cụ này ảnh hưởng đến việc phân giải SDK, phân tích mã, build, chạy, v.v.

Biên dịch và gỡ lỗi project
---------------------------
Rider tích hợp sẵn trình gỡ lỗi có thể được sử dụng để gỡ lỗi project Godot. Bạn có thể khởi chạy trình gỡ lỗi bằng cách nhấn biểu tượng **Debug** ở đầu màn hình; tính năng này chỉ hoạt động với Project Manager. Nếu muốn gỡ lỗi editor, trước tiên bạn cần cấu hình trình gỡ lỗi.

.. figure:: img/rider_run_debug.webp
   :align: center

- Nhấp vào tùy chọn **Godot > Edit Configurations** ở đầu màn hình.

.. figure:: img/rider_configurations.webp
   :align: center

- Đảm bảo các giá trị sau cho C++ Project Run Configuration:

    - Exe Path : ``$(LocalDebuggerCommand)`` - Program Arguments: ``-e --path <path to the Godot project>`` - Working Directory: ``$(LocalDebuggerWorkingDirectory)`` - Before Launch có giá trị là "Build Project"

Điều này sẽ yêu cầu tệp thực thi gỡ lỗi project được chỉ định mà không mở Project Manager. Sử dụng đường dẫn gốc đến thư mục project, không phải đường dẫn tệp ``project.godot``.

.. figure:: img/rider_configurations_changed.webp
   :align: center

- Cuối cùng, nhấp vào "Apply" và "OK" để lưu các thay đổi.

- Khi nhấn biểu tượng **Debug** ở đầu màn hình, JetBrains Rider sẽ khởi chạy editor Godot với trình gỡ lỗi được đính kèm.

Ngoài ra, bạn có thể sử dụng **Run > Attach to Process** để đính kèm trình gỡ lỗi vào một phiên bản Godot đang chạy.

.. figure:: img/rider_attach_to_process.webp
   :align: center

- Bạn có thể tìm phiên bản Godot bằng cách tìm kiếm ``godot.editor`` rồi nhấp vào ``Attach with LLDB``

.. figure:: img/rider_attach_to_process_dialog.webp
   :align: center

|

Trình trực quan hóa gỡ lỗi
--------------------------
Trình trực quan hóa gỡ lỗi tùy chỉnh cách hiển thị các cấu trúc dữ liệu phức tạp trong khi gỡ lỗi. Các tệp "natvis" (viết tắt của "Native Visualization") được tích hợp trong Godot sẽ tự động được sử dụng.

.. note:: On macOS and Linux, natvis support requires Rider 2026.2 or later.

Kiểm thử đơn vị
---------------
Tận dụng hỗ trợ :ref:`doctest<doc_unit_testing>` của Rider. Vui lòng tham khảo `hướng dẫn <https://github.com/JetBrains/godot-support/wiki/Godot-doctest-Unit-Tests>`_.

Lập hồ sơ hiệu năng
-------------------
Vui lòng tham khảo `hướng dẫn lập hồ sơ hiệu năng <https://github.com/JetBrains/godot-support/wiki/Profiling-Godot-engine-(native-code)-with-dotTrace-or-JetBrains-Rider>`_.

Vui lòng tham khảo `tài liệu JetBrains Rider <https://www.jetbrains.com/rider/documentation/>`_ để biết thông tin cụ thể về IDE JetBrains.

Các vấn đề đã biết
------------------
Gỡ lỗi bản build MinGW trên Windows - các ký hiệu chưa được tải. Đã báo cáo tại `RIDER-106816 <https://youtrack.jetbrains.com/issue/RIDER-106816/Upgrade-LLDB-to-actual-version>`_.
