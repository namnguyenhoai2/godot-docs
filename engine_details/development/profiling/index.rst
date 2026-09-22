.. _doc_using_cpp_profilers:

Sử dụng profiler C++
====================

Để tối ưu hiệu năng của Godot, trước tiên bạn cần biết nên tối ưu điều gì. Profiler là công cụ hữu ích cho mục đích này.

.. note::

    Trong editor có :ref:`profiler GDScript tích hợp sẵn <doc_the_profiler>`, nhưng sử dụng profiler C++ có thể hữu ích trong những trường hợp profiler GDScript chưa đủ chính xác hoặc thiếu thông tin do lỗi trong profiler.

Có hai loại profiler chính: profiler lấy mẫu và profiler tracing.

Profiler lấy mẫu định kỳ ngắt chương trình đang chạy và lấy một "mẫu", ghi lại các hàm đang chạy. Dựa trên thông tin này, profiler ước tính những hàm mà chương trình đã dành nhiều thời gian nhất để thực thi.

Profiler tracing hoạt động bằng cách ghi lại các sự kiện đặc thù của ứng dụng (chẳng hạn như thời điểm bắt đầu và kết thúc của một frame), tạo ra một nhật ký gọi là "trace". Profiler có thể sử dụng trace để tạo biểu đồ hiển thị dòng thời gian cấp cao chính xác về những gì đã xảy ra. Tuy nhiên, mọi mã không được instrument rõ ràng sẽ không xuất hiện trên dòng thời gian của profiler tracing!

Godot hỗ trợ cả profiler lấy mẫu và profiler tracing, đồng thời đã bao gồm mã logging cho các sự kiện Godot phổ biến để sử dụng với profiler tracing!

Việc debug các vấn đề khác nhau có thể dễ dàng hơn với một loại profiler này so với loại kia, nhưng rất khó đưa ra một bộ quy tắc về việc nên sử dụng loại nào. Hãy thử cả hai và xem bạn có thể tìm hiểu được gì từ chúng!

.. _doc_sampling_profilers:

Profiler lấy mẫu
----------------

Chúng tôi khuyến nghị các profiler lấy mẫu sau:

- :ref:`VerySleepy <doc_profiler_very_sleepy>` (chỉ dành cho Windows)
- :ref:`Hotspot <doc_profiler_hotspot>` (chỉ dành cho Linux)
- :ref:`Instruments <doc_profiler_instruments>` (chỉ dành cho Apple)

Những profiler này có thể không phải là các lựa chọn mạnh mẽ hoặc linh hoạt nhất, nhưng việc hoạt động độc lập cùng tập tính năng giới hạn thường giúp chúng dễ sử dụng hơn.

Thiết lập Godot
~~~~~~~~~~~~~~~

Để nhận được thông tin profiling hữu ích, **bắt buộc phải** sử dụng bản build Godot có chứa debugging symbols. Các binary chính thức không chứa debugging symbols vì chúng sẽ làm kích thước tải xuống lớn hơn đáng kể.

Để có dữ liệu profiling phù hợp nhất với môi trường production (nhưng vẫn có debugging symbols), bạn nên biên dịch binary với các tùy chọn ``production=yes debug_symbols=yes`` SCons.

Bạn có thể chạy profiler trên các bản build được tối ưu hóa ít hơn (ví dụ: ``target=template_debug`` không có LTO), nhưng kết quả đương nhiên sẽ ít phản ánh điều kiện thực tế hơn.

.. warning::

    *Không được* loại bỏ debugging symbols khỏi các binary bằng lệnh ``strip`` sau khi biên dịch binary. Nếu không, bạn sẽ không còn nhận được thông tin profiling hữu ích khi chạy profiler.

Đo thời gian khởi động/tắt
~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn đang tìm cách tối ưu hiệu năng khởi động/tắt của Godot, bạn có thể yêu cầu profiler sử dụng tùy chọn dòng lệnh ``--quit`` trên binary Godot. Tùy chọn này sẽ thoát Godot ngay sau khi quá trình khởi động hoàn tất. Tùy chọn ``--quit`` hoạt động với ``--editor``, ``--project-manager`` và ``--path <path to project directory>`` (chạy trực tiếp một project).

.. seealso::

    Xem :ref:`doc_command_line_tutorial` để biết thêm các đối số dòng lệnh được Godot hỗ trợ.

.. _doc_tracing_profilers:

Profiler tracing
----------------

Hiện tại Godot hỗ trợ ba profiler tracing:

- :ref:`Tracy <doc_profiler_tracy>`
- :ref:`Perfetto <doc_profiler_perfetto>`
- :ref:`Instruments <doc_profiler_instruments>` (chỉ dành cho Apple)

.. note::

    Perfetto là hệ thống tracing mặc định cho Android, vì vậy các export template dựng sẵn có tích hợp và bật Perfetto được cung cấp trên `trang GitHub Releases <https://github.com/godotengine/godot-builds/releases>`__.

Để sử dụng một trong hai profiler này, bạn cần build engine từ source. Nếu trước đây bạn chưa từng làm việc này, vui lòng đọc
:ref:`tài liệu này <doc_compiling_index>` dành cho nền tảng mà bạn muốn profiling. Bạn sẽ cần thực hiện các bước tương tự tại đây, nhưng thêm một số đối số cho ``scons``.

Tất cả profiler được khuyến nghị
--------------------------------

.. toctree::
   :maxdepth: 1
   :name: toc-devel-using-cpp-profilers

   hotspot
   instruments
   perfetto
   tracy
   very_sleepy
