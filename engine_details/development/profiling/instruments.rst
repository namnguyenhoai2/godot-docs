.. _doc_profiler_instruments:

Instruments
===========

.. seealso:: Please see the :ref:`sampling profiler instructions <doc_sampling_profilers>`
             và :ref:`tracing profiler instructions <doc_tracing_profilers>` để biết thêm thông tin.

- Mở `Xcode <https://developer.apple.com/xcode/>`__. Chọn **Open Developer Tool** - **Instruments** từ menu ứng dụng **Xcode**: - Nhấp đúp vào **Time Profiler** trong cửa sổ **Instruments**:

.. image:: img/cpp_profiler_xcode_menu.png

- Trong cửa sổ Time Profiler, nhấp vào menu **Target**, chọn **Choose target...** rồi chỉ định đường dẫn đến tệp nhị phân Godot, các đối số dòng lệnh và các biến môi trường trong cửa sổ tiếp theo.

.. image:: img/cpp_profiler_time_profiler.png

- Bạn cũng có thể đính kèm Time Profiler vào một tiến trình đang chạy bằng cách chọn tiến trình đó từ menu **Target**.

- Nhấp vào nút **Start an immediate mode recording** để bắt đầu lập hồ sơ hiệu năng.

.. image:: img/cpp_profiler_time_profiler_record.png

- Thực hiện các thao tác bạn muốn lập hồ sơ hiệu năng trong trình chỉnh sửa hoặc dự án. Khi hoàn tất, nhấp vào nút **Stop**.

- Chờ kết quả xuất hiện. - Ở cuối cửa sổ, bạn sẽ thấy cây lời gọi cho tất cả các luồng CPU đã khởi chạy và phần tổng quan **Heaviest Stack Trace**. - Chọn **Hide system libraries** trong menu **Call Tree** (ở cuối cửa sổ) để loại bỏ các mô-đun bên ngoài. - Bạn có thể sử dụng dòng thời gian ở đầu cửa sổ để hiển thị thông tin chi tiết cho khoảng thời gian cụ thể.

.. image:: img/cpp_profiler_time_profiler_result.png
