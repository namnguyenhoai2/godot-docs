.. _doc_configuring_an_ide_rider:

JetBrains Rider
===============

`JetBrains Rider <https://www.jetbrains.com/rider/>`_ là một IDE thương mại của `JetBrains <https://www.jetbrains.com/>`_ dành cho C++, C# và GDScript, sử dụng cùng hệ thống solution như Visual Studio.

.. note::

    Tài liệu này hướng dẫn đóng góp cho game engine, không hướng dẫn sử dụng JetBrains Rider làm trình soạn thảo C# hoặc GDScript. Để viết mã C# hoặc GDScript trong trình soạn thảo bên ngoài, hãy xem
    :ref:`hướng dẫn C# để cấu hình trình soạn thảo bên ngoài <doc_c_sharp_setup_external_editor>`.

Import project
--------------

.. tip:: Nếu bạn đã sử dụng Visual Studio làm IDE chính, bạn có thể sử dụng cùng tệp solution trong Rider. Rider và Visual Studio sử dụng cùng định dạng solution, vì vậy bạn có thể chuyển đổi giữa hai IDE mà không cần tạo lại tệp solution. Cần thay đổi các cấu hình debug khi chuyển từ IDE này sang IDE kia.

Nếu bạn bắt đầu từ đầu, hãy làm theo :ref:`hướng dẫn <doc_compiling_index>`, cụ thể là:

- Cài đặt tất cả dependency.
- Xác định lệnh scons để biên dịch cho một platform cụ thể.

Cung cấp cho scons các đối số bổ sung để yêu cầu tạo tệp solution:

- Thêm `vsproj=yes dev_build=yes` vào lệnh scons

Tham số ``vsproj`` cho biết bạn muốn tạo solution Visual Studio. Tham số ``dev_build`` đảm bảo các debug symbol được bao gồm, cho phép bạn chẳng hạn như thực hiện từng bước qua mã bằng breakpoint.

.. note:: Mỗi lần chạy SCons chỉ tạo tệp ``.generated.props`` cho một Solution Configuration. Hãy chạy SCons một lần cho mỗi target bạn dự định sử dụng:

          .. code-block:: shell

             scons vsproj=yes dev_build=yes target=editor
             scons vsproj=yes dev_build=yes target=template_debug
             scons vsproj=yes dev_build=yes target=template_release

- Mở ``godot.sln`` đã tạo trong Rider.

.. note:: Đảm bảo Solution configuration phù hợp được chọn trên thanh công cụ Rider. Cấu hình này ảnh hưởng đến việc phân giải SDK, phân tích mã, build, run, v.v.

Biên dịch và debug project
--------------------------
Rider có debugger tích hợp, có thể dùng để debug project Godot. Bạn có thể khởi chạy debugger bằng cách nhấn biểu tượng **Debug** ở đầu màn hình; cách này chỉ hoạt động với Project Manager. Nếu muốn debug editor, trước tiên bạn cần cấu hình debugger.

.. figure:: img/rider_run_debug.webp
   :align: center

- Nhấp vào tùy chọn **Godot > Edit Configurations** ở đầu màn hình.

.. figure:: img/rider_configurations.webp
   :align: center

- Đảm bảo các giá trị sau cho C++ Project Run Configuration:

    - Exe Path : ``$(LocalDebuggerCommand)``
    - Program Arguments: ``-e --path <path to the Godot project>``
    - Working Directory: ``$(LocalDebuggerWorkingDirectory)``
    - Before Launch có giá trị là "Build Project"

Thao tác này sẽ yêu cầu executable debug project được chỉ định mà không mở Project Manager. Sử dụng đường dẫn gốc đến thư mục project, không sử dụng đường dẫn tệp ``project.godot``.

.. figure:: img/rider_configurations_changed.webp
   :align: center

- Cuối cùng, nhấp vào "Apply" và "OK" để lưu các thay đổi.

- Khi bạn nhấn biểu tượng **Debug** ở đầu màn hình, JetBrains Rider sẽ khởi chạy editor Godot với debugger được đính kèm.

Ngoài ra, bạn có thể sử dụng **Run > Attach to Process** để đính kèm debugger vào một instance Godot đang chạy.

.. figure:: img/rider_attach_to_process.webp
   :align: center

- Bạn có thể tìm instance Godot bằng cách tìm kiếm ``godot.editor``, sau đó nhấp vào ``Attach with LLDB``

.. figure:: img/rider_attach_to_process_dialog.webp
   :align: center

|

Trình trực quan hóa debug
-------------------------
Trình trực quan hóa debug tùy chỉnh cách hiển thị các cấu trúc dữ liệu phức tạp trong quá trình debug. Các tệp "natvis" (viết tắt của "Native Visualization") tích hợp sẵn trong Godot sẽ được tự động sử dụng.

.. note:: Trên macOS và Linux, hỗ trợ natvis yêu cầu Rider 2026.2 trở lên.

Kiểm thử đơn vị
---------------
Tận dụng hỗ trợ :ref:`doctest <doc_unit_testing>` của Rider. Vui lòng tham khảo `hướng dẫn <https://github.com/JetBrains/godot-support/wiki/Godot-doctest-Unit-Tests>`_.

Profiling
---------
Vui lòng tham khảo `hướng dẫn profiling <https://github.com/JetBrains/godot-support/wiki/Profiling-Godot-engine-(native-code)-with-dotTrace-or-JetBrains-Rider>`_.

Vui lòng tham khảo `tài liệu JetBrains Rider <https://www.jetbrains.com/rider/documentation/>`_ để biết thông tin cụ thể về JetBrains IDE.

Các vấn đề đã biết
------------------
Debug bản build Windows MinGV - symbol không được tải. Đã báo cáo tại `RIDER-106816 <https://youtrack.jetbrains.com/issue/RIDER-106816/Upgrade-LLDB-to-actual-version>`_.

.. _`JetBrains Rider`: https://www.jetbrains.com/rider/
.. _`JetBrains`: https://www.jetbrains.com/
.. _`the instructions`: https://github.com/JetBrains/godot-support/wiki/Godot-doctest-Unit-Tests
.. _`the profiling instructions`: https://github.com/JetBrains/godot-support/wiki/Profiling-Godot-engine-(native-code)-with-dotTrace-or-JetBrains-Rider
.. _`JetBrains Rider documentation`: https://www.jetbrains.com/rider/documentation/
.. _`RIDER-106816`: https://youtrack.jetbrains.com/issue/RIDER-106816/Upgrade-LLDB-to-actual-version
