.. _doc_navigation_debug_tools:

Công cụ gỡ lỗi điều hướng
=========================

.. note::

    Các công cụ, thuộc tính và hàm gỡ lỗi chỉ khả dụng trong các bản build debug của Godot. Không sử dụng bất kỳ thành phần nào trong số đó trong mã sẽ thuộc về bản build phát hành.

Bật gỡ lỗi điều hướng
---------------------

Các hình ảnh trực quan hóa gỡ lỗi điều hướng được bật theo mặc định trong editor. Để cũng trực quan hóa navigation mesh và các kết nối khi chạy runtime, hãy bật tùy chọn **Visible Navigation** trong menu **Debug** của editor.

.. image:: img/navigation_debug_toggle.png

Trong các bản build debug của Godot, bạn cũng có thể bật hoặc tắt gỡ lỗi điều hướng thông qua các singleton NavigationServer từ script.

.. tabs::
 .. code-tab:: gdscript GDScript

    NavigationServer2D.set_debug_enabled(false)
    NavigationServer3D.set_debug_enabled(true)

 .. code-tab:: csharp

    NavigationServer2D.SetDebugEnabled(false);
    NavigationServer3D.SetDebugEnabled(true);

Các hình ảnh trực quan hóa gỡ lỗi hiện dựa trên các Node trong SceneTree. Nếu chỉ sử dụng các API :ref:`NavigationServer2D<class_NavigationServer2D>` hoặc :ref:`NavigationServer3D<class_NavigationServer3D>` thì các thay đổi sẽ không được phản ánh trong các công cụ gỡ lỗi điều hướng.

Cài đặt gỡ lỗi điều hướng
-------------------------

Có thể thay đổi giao diện gỡ lỗi điều hướng trong ProjectSettings tại ``debug/shapes/navigation``. Một số tính năng gỡ lỗi cũng có thể được bật hoặc tắt tùy ý, nhưng có thể yêu cầu khởi động lại scene để có hiệu lực.

.. image:: img/nav_debug_settings.png

Các polygon navigation mesh khi gỡ lỗi
--------------------------------------

Nếu bật ``enable_edge_lines``, các cạnh của polygon navigation mesh sẽ được làm nổi bật. Nếu cũng bật ``enable_edge_lines_xray``, các cạnh của navigation mesh sẽ hiển thị xuyên qua hình học.

Nếu bật ``enable_geometry_face_random_color``, màu của mỗi mặt navigation mesh sẽ được pha trộn với một màu ngẫu nhiên, màu này lại được pha trộn với màu được chỉ định trong ``geometry_face_color``.

.. image:: img/nav_debug_xray_edge_lines.png

Các kết nối cạnh khi gỡ lỗi
---------------------------

Khi hai navigation mesh được kết nối trong phạm vi khoảng cách ``edge_connection_margin``, kết nối sẽ được phủ lớp hiển thị. Màu của lớp phủ được điều khiển bởi ``edge_connection_color``. Có thể làm cho các kết nối hiển thị xuyên qua hình học bằng ``enable_edge_connections_xray``.

.. image:: img/nav_edge_connection2d.gif

.. image:: img/nav_edge_connection3d.gif

.. note::

    Các kết nối cạnh chỉ hiển thị khi NavigationServer đang hoạt động.

Hiệu năng khi gỡ lỗi
--------------------

Để đo hiệu năng của NavigationServer, có một monitor chuyên dụng nằm trong Editor Debugger tại *Debugger->Monitors->Navigation Process*.

.. image:: img/navigation_debug_performance1.webp

Navigation Process cho biết thời gian NavigationServer dành để cập nhật các thành phần nội bộ trong frame cập nhật này, tính bằng mili giây. Navigation Process hoạt động tương tự Process đối với việc render frame hình ảnh và Physics Process đối với các cập nhật va chạm và cập nhật cố định.

Navigation Process tính cả mọi cập nhật đối với **navigation maps**, **navigation regions** và **navigation agents**, cũng như tất cả **avoidance calculations** cho frame cập nhật.

.. note::

    Navigation Process KHÔNG bao gồm hiệu năng tìm đường, vì việc tìm đường hoạt động độc lập trên dữ liệu navigation map với quá trình cập nhật của server.

Nhìn chung, Navigation Process nên được giữ ở mức thấp và ổn định nhất có thể để bảo đảm hiệu năng runtime và tránh các vấn đề về tốc độ khung hình. Lưu ý rằng vì quá trình cập nhật của NavigationServer diễn ra ở giữa quá trình cập nhật vật lý, việc Navigation Process tăng sẽ tự động làm Physics Process tăng cùng một lượng.

Navigation cũng cung cấp các thống kê chi tiết hơn về những đối tượng liên quan đến navigation hiện tại và cấu trúc của navigation map trên NavigationServer.

.. image:: img/navigation_debug_performance2.webp

Không thể đánh giá các thống kê navigation hiển thị ở đây là tốt hay xấu đối với hiệu năng, vì điều đó hoàn toàn phụ thuộc vào dự án và những gì được xem là hợp lý hoặc quá mức nghiêm trọng.

Các thống kê navigation giúp xác định những điểm nghẽn hiệu năng ít rõ ràng hơn, vì nguồn gây ra chúng có thể không phải lúc nào cũng có biểu diễn trực quan. Ví dụ: các vấn đề về hiệu năng tìm đường do navigation mesh quá chi tiết với hàng nghìn cạnh / polygon, hoặc các vấn đề do navigation procedural hoạt động không đúng.
