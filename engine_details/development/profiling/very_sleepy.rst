.. _doc_profiler_very_sleepy:

VerySleepy
==========

.. seealso:: Please see the :ref:`sampling profiler instructions <doc_sampling_profilers>` for more information.

- Trước tiên, hãy khởi động trình chỉnh sửa Godot hoặc dự án của bạn. Nếu khởi động Project Manager, hãy đảm bảo bạn chỉnh sửa hoặc chạy một dự án trước. Nếu không, profiler sẽ không theo dõi tiến trình con vì Project Manager sẽ tạo một tiến trình con cho mỗi dự án được chỉnh sửa hoặc chạy. - Mở `VerySleepy <https://github.com/VerySleepy/verysleepy>`__ và chọn tệp thực thi Godot trong danh sách các tiến trình ở bên trái:

.. image:: img/cpp_profiler_verysleepy_select_process.png

- Nhấp vào nút **Profile All** ở bên phải để bắt đầu lập hồ sơ. - Thực hiện các thao tác bạn muốn lập hồ sơ trong trình chỉnh sửa hoặc dự án. Khi hoàn tất, hãy nhấp vào **Stop** (*không phải* **Abort**). - Chờ cửa sổ kết quả xuất hiện. - Khi cửa sổ kết quả xuất hiện, hãy lọc chế độ xem để loại bỏ các mô-đun bên ngoài (chẳng hạn như trình điều khiển đồ họa). Bạn có thể lọc theo mô-đun bằng cách tìm một dòng có **Module** khớp với tên tệp thực thi Godot, nhấp chuột phải vào dòng đó rồi chọn **Filter Module to <Godot executable name>** trong menu thả xuống xuất hiện. - Cửa sổ kết quả của bạn lúc này sẽ trông tương tự như sau:

.. image:: img/cpp_profiler_verysleepy_results_filtered.png
