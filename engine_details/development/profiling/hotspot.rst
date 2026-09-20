.. _doc_profiler_hotspot:

Hotspot
=======

.. seealso:: Please see the :ref:`sampling profiler instructions <doc_sampling_profilers>` for more information.

- Mở `Hotspot <https://github.com/KDAB/hotspot>`__. Nhấp **Record Data**:

.. image:: img/cpp_profiler_hotspot_welcome.png

- Trong cửa sổ tiếp theo, chỉ định đường dẫn đến tệp nhị phân Godot có chứa ký hiệu gỡ lỗi. - Chỉ định các đối số dòng lệnh để chạy một dự án cụ thể, có hoặc không có trình chỉnh sửa. - Đường dẫn đến thư mục làm việc có thể là bất kỳ đường dẫn nào nếu sử dụng đường dẫn tuyệt đối cho đối số dòng lệnh ``--path``. Nếu không, đường dẫn này phải được thiết lập để đường dẫn tương đối đến dự án hợp lệ. - Hãy đảm bảo **Elevate Privileges** được chọn nếu bạn có quyền quản trị. Mặc dù không thiết yếu để lập hồ sơ Godot, tùy chọn này sẽ đảm bảo tất cả sự kiện đều được ghi lại. Nếu không, một số sự kiện có thể bị thiếu trong dữ liệu thu thập. Lúc này, các thiết lập của bạn sẽ trông tương tự như sau:

.. image:: img/cpp_profiler_hotspot_record.png

- Nhấp **Start Recording** và thực hiện các thao tác bạn muốn lập hồ sơ trong trình chỉnh sửa/dự án. - Thoát trình chỉnh sửa/dự án theo cách thông thường hoặc sử dụng nút **Stop Profiling** trong Hotspot để dừng lập hồ sơ sớm. Việc dừng lập hồ sơ sớm có thể tạo ra các hồ sơ rõ ràng hơn nếu bạn không quan tâm đến quy trình tắt máy của engine. - Nhấp **View Results** và đợi phần trực quan hóa dữ liệu lập hồ sơ được tạo:

.. image:: img/cpp_profiler_hotspot_view_results.png

- Sử dụng các thẻ ở trên cùng để chuyển đổi giữa những chế độ xem khác nhau. Các chế độ xem này hiển thị cùng một dữ liệu nhưng theo những cách khác nhau. Thẻ **Flame Graph** là một cách hữu ích để nhanh chóng xem những hàm nào chiếm nhiều thời gian nhất. Do đó, đây là những hàm quan trọng nhất cần tối ưu, vì việc tối ưu chúng sẽ cải thiện hiệu suất nhiều nhất. - Ở cuối tất cả các thẻ, ngoại trừ **Summary**, bạn cũng sẽ thấy danh sách các luồng CPU do engine khởi chạy cùng với mức sử dụng CPU của từng luồng. Điều này cho phép bạn nhận biết những luồng có thể trở thành nút thắt cổ chai tại một thời điểm nhất định.

.. image:: img/cpp_profiler_hotspot_flame_graph.png

.. note::

    Nếu không muốn quy trình khởi động được đưa vào hồ sơ, bạn cũng có thể gắn Hotspot vào một tiến trình đang chạy bằng cách nhấp **Record Data**, sau đó đặt tùy chọn trong danh sách thả xuống **Launch Application** thành **Attach To Process(es)**.

    Quy trình dựa trên việc gắn vào tiến trình này tương tự như quy trình được VerySleepy sử dụng.
