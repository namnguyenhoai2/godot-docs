.. _doc_profiler_very_sleepy:

VerySleepy
==========

.. seealso:: Vui lòng xem :ref:`hướng dẫn về sampling profiler <doc_sampling_profilers>` để biết thêm thông tin.

- Trước tiên, hãy khởi động trình biên tập Godot hoặc project của bạn. Nếu bạn khởi động Project Manager, hãy đảm bảo trước tiên chỉnh sửa hoặc chạy một project. Nếu không, profiler sẽ không theo dõi tiến trình con, vì Project Manager sẽ tạo một tiến trình con cho mỗi project được chỉnh sửa hoặc chạy.
- Mở `VerySleepy <https://github.com/VerySleepy/verysleepy>`__ và chọn tệp thực thi Godot trong danh sách các tiến trình ở bên trái:

.. image:: img/cpp_profiler_verysleepy_select_process.png

- Nhấp vào nút **Profile All** ở bên phải để bắt đầu profiling.
- Thực hiện các thao tác bạn muốn profile trong trình biên tập hoặc project. Khi hoàn tất, hãy nhấp vào **Stop** (*not* Abort).
- Chờ cửa sổ kết quả xuất hiện.
- Sau khi cửa sổ kết quả xuất hiện, hãy lọc chế độ xem để loại bỏ các module bên ngoài (chẳng hạn như driver đồ họa). Bạn có thể lọc theo module bằng cách tìm một dòng có **Module** khớp với tên tệp thực thi Godot, nhấp chuột phải vào dòng đó rồi chọn **Filter Module to <Godot executable name>** trong menu thả xuống xuất hiện.
- Cửa sổ kết quả của bạn lúc này sẽ trông tương tự như sau:

.. image:: img/cpp_profiler_verysleepy_results_filtered.png
