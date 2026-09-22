.. _doc_profiler_hotspot:

Hotspot
=======

.. seealso:: Vui lòng xem :ref:`hướng dẫn về sampling profiler <doc_sampling_profilers>` để biết thêm thông tin.

- Mở `Hotspot <https://github.com/KDAB/hotspot>`__. Nhấp vào **Record Data**:

.. image:: img/cpp_profiler_hotspot_welcome.png

- Trong cửa sổ tiếp theo, chỉ định đường dẫn đến tệp nhị phân Godot có chứa debug symbols.
- Chỉ định các đối số dòng lệnh để chạy một project cụ thể, có hoặc không có editor.
- Đường dẫn đến working directory có thể là bất kỳ đường dẫn nào nếu sử dụng đường dẫn tuyệt đối cho ``--path`` command line argument. Nếu không, đường dẫn này phải được thiết lập sao cho đường dẫn tương đối đến project hợp lệ.
- Đảm bảo đã chọn **Elevate Privileges** nếu bạn có quyền quản trị. Mặc dù không bắt buộc khi profiling Godot, tùy chọn này sẽ đảm bảo tất cả các event đều được ghi lại. Nếu không, một số event có thể bị thiếu trong bản ghi. Các thiết lập của bạn lúc này sẽ trông tương tự như sau:

.. image:: img/cpp_profiler_hotspot_record.png

- Nhấp vào **Start Recording** và thực hiện các thao tác bạn muốn profile trong editor/project.
- Thoát editor/project theo cách bình thường hoặc sử dụng nút **Stop Profiling** trong Hotspot để dừng profiling sớm. Dừng profiling sớm có thể giúp profile sạch hơn nếu bạn không quan tâm đến quy trình tắt của engine.
- Nhấp vào **View Results** và chờ tạo xong phần trực quan hóa profiling:

.. image:: img/cpp_profiler_hotspot_view_results.png

- Sử dụng các tab ở trên cùng để chuyển đổi giữa các chế độ xem khác nhau. Các chế độ xem này hiển thị cùng một dữ liệu nhưng theo những cách khác nhau. Tab **Flame Graph** là một cách hữu ích để nhanh chóng xem những function nào chiếm nhiều thời gian nhất. Do đó, đây là những function quan trọng nhất cần tối ưu, vì việc tối ưu chúng sẽ cải thiện hiệu năng nhiều nhất.
- Ở cuối tất cả các tab ngoại trừ **Summary**, bạn cũng sẽ thấy danh sách các CPU thread do engine khởi chạy cùng với mức sử dụng CPU của từng thread. Điều này cho phép bạn thấy những thread có thể trở thành bottleneck tại một thời điểm cụ thể.

.. image:: img/cpp_profiler_hotspot_flame_graph.png

.. note::

    Nếu không muốn quy trình khởi động được đưa vào profile, bạn cũng có thể attach Hotspot vào một process đang chạy bằng cách nhấp vào **Record Data**, sau đó đặt tùy chọn dropdown **Launch Application** thành **Attach To Process(es)**.

    Quy trình dựa trên việc attach vào process này tương tự quy trình được VerySleepy sử dụng.
