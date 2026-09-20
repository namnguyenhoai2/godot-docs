.. _doc_using_cpp_profilers:

Sử dụng trình phân tích hiệu năng C++
=====================================

Để tối ưu hóa hiệu năng của Godot, trước tiên bạn cần biết nên tối ưu phần nào. Trình phân tích hiệu năng là công cụ hữu ích cho mục đích này.

.. note::

    Trong trình chỉnh sửa có :ref:`built-in GDScript profiler <doc_the_profiler>`, nhưng việc sử dụng trình phân tích hiệu năng C++ có thể hữu ích trong những trường hợp trình phân tích GDScript không đủ chính xác hoặc thiếu thông tin do lỗi trong trình phân tích.

Có hai loại trình phân tích hiệu năng chính: trình phân tích lấy mẫu và trình phân tích truy vết.

Trình phân tích lấy mẫu định kỳ ngắt chương trình đang chạy và lấy một "mẫu", ghi lại những hàm đang chạy. Dựa trên thông tin này, trình phân tích ước tính những hàm mà chương trình đã dành nhiều thời gian nhất để thực thi.

Trình phân tích truy vết hoạt động bằng cách ghi lại các sự kiện cụ thể của ứng dụng (chẳng hạn như thời điểm bắt đầu và kết thúc của một khung hình), tạo ra một nhật ký gọi là "trace". Trình phân tích có thể sử dụng trace để tạo biểu đồ hiển thị dòng thời gian cấp cao chính xác về những gì đã xảy ra. Tuy nhiên, mọi mã không được chèn mã đo lường một cách rõ ràng sẽ không xuất hiện trên dòng thời gian của trình phân tích truy vết!

Godot hỗ trợ cả trình phân tích lấy mẫu và trình phân tích truy vết, đồng thời đã tích hợp sẵn mã ghi nhật ký cho các sự kiện Godot phổ biến để sử dụng với trình phân tích truy vết!

Các vấn đề khác nhau có thể dễ gỡ lỗi hơn bằng một loại trình phân tích này so với loại kia, nhưng rất khó đưa ra một bộ quy tắc về việc nên sử dụng loại nào. Hãy thử cả hai và xem bạn có thể học được gì từ chúng!

.. _doc_sampling_profilers:

Trình phân tích lấy mẫu
-----------------------

Chúng tôi khuyến nghị các trình phân tích lấy mẫu sau:

- :ref:`VerySleepy <doc_profiler_very_sleepy>` (chỉ dành cho Windows) - :ref:`Hotspot <doc_profiler_hotspot>` (chỉ dành cho Linux) - :ref:`Instruments <doc_profiler_instruments>` (chỉ dành cho Apple)

Những trình phân tích này có thể không phải là các tùy chọn mạnh mẽ hoặc linh hoạt nhất, nhưng khả năng hoạt động độc lập và tập tính năng hạn chế thường khiến chúng dễ sử dụng hơn.

Thiết lập Godot
~~~~~~~~~~~~~~~

Để nhận được thông tin phân tích hiệu năng hữu ích, **bắt buộc** phải sử dụng bản dựng Godot có chứa ký hiệu gỡ lỗi. Các tệp nhị phân chính thức không chứa ký hiệu gỡ lỗi, vì chúng sẽ làm kích thước tải xuống tăng đáng kể.

Để có dữ liệu phân tích hiệu năng phù hợp nhất với môi trường phát hành (nhưng vẫn có ký hiệu gỡ lỗi), bạn nên biên dịch các tệp nhị phân với các tùy chọn SCons ``production=yes debug_symbols=yes``.

Có thể chạy trình phân tích hiệu năng trên các bản dựng được tối ưu hóa ít hơn (ví dụ: ``target=template_debug`` không có LTO), nhưng kết quả đương nhiên sẽ ít phản ánh các điều kiện thực tế hơn.

.. warning::

    *Không* được tước bỏ ký hiệu gỡ lỗi khỏi các tệp nhị phân bằng lệnh ``strip`` sau khi biên dịch chúng. Nếu không, bạn sẽ không còn nhận được thông tin phân tích hiệu năng hữu ích khi chạy trình phân tích.

Đo thời gian khởi động/tắt máy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn đang tìm cách tối ưu hiệu năng khởi động/tắt máy của Godot, bạn có thể yêu cầu trình phân tích sử dụng tùy chọn dòng lệnh ``--quit`` trên tệp nhị phân Godot. Tùy chọn này sẽ thoát Godot ngay sau khi quá trình khởi động hoàn tất. Tùy chọn ``--quit`` hoạt động với ``--editor``, ``--project-manager`` và ``--path <path to project directory>`` (tùy chọn này chạy trực tiếp một dự án).

.. seealso::

    Xem :ref:`doc_command_line_tutorial` để biết thêm các đối số dòng lệnh được Godot hỗ trợ.

.. _doc_tracing_profilers:

Trình phân tích truy vết
------------------------

Hiện tại Godot hỗ trợ ba trình phân tích truy vết:

- :ref:`Tracy <doc_profiler_tracy>` - :ref:`Perfetto <doc_profiler_perfetto>` - :ref:`Instruments <doc_profiler_instruments>` (chỉ dành cho Apple)

.. note::

    Perfetto là hệ thống truy vết mặc định cho Android, vì vậy các mẫu xuất dựng sẵn có tích hợp và bật Perfetto được cung cấp tại `GitHub Releases page <https://github.com/godotengine/godot-builds/releases>`__.

Để sử dụng một trong hai trình phân tích này, bạn sẽ cần biên dịch engine từ mã nguồn. Nếu trước đây bạn chưa từng làm việc này, vui lòng đọc
:ref:`these docs <doc_compiling_index>` for the platform you want to profile on.
Bạn sẽ cần thực hiện các bước tương tự ở đây, nhưng với một số đối số bổ sung cho ``scons``.

Tất cả trình phân tích hiệu năng được khuyến nghị
-------------------------------------------------

.. toctree::
   :maxdepth: 1
   :name: toc-devel-using-cpp-profilers

   hotspot
   instruments
   perfetto
   tracy
   very_sleepy
