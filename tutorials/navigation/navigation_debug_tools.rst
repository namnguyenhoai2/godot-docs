.. _doc_navigation_debug_tools:

Công cụ debug navigation
========================

.. note::

    Các công cụ, thuộc tính và hàm debug chỉ khả dụng trong các bản build debug của Godot. Không sử dụng bất kỳ thành phần nào trong số đó trong code sẽ thuộc về bản build release.

Bật debug navigation
--------------------

Các hình ảnh trực quan debug navigation được bật mặc định trong editor. Để trực quan hóa navigation mesh và các kết nối cả khi runtime, hãy bật tùy chọn **Visible Navigation** trong menu **Debug** của editor.

.. image:: img/navigation_debug_toggle.png

Trong các bản build debug của Godot, debug navigation cũng có thể được bật hoặc tắt thông qua các singleton NavigationServer từ script.

.. tabs::
 .. code-tab:: gdscript GDScript

    NavigationServer2D.set_debug_enabled(false)
    NavigationServer3D.set_debug_enabled(true)

 .. code-tab:: csharp

    NavigationServer2D.SetDebugEnabled(false);
    NavigationServer3D.SetDebugEnabled(true);

Các hình ảnh trực quan debug hiện dựa trên các Node trong SceneTree. Nếu chỉ sử dụng các API :ref:`NavigationServer2D<class_NavigationServer2D>` hoặc :ref:`NavigationServer3D<class_NavigationServer3D>` thì các thay đổi sẽ không được phản ánh bởi các công cụ debug navigation.

Cài đặt debug navigation
------------------------

Có thể thay đổi giao diện của debug navigation trong ProjectSettings tại ``debug/shapes/navigation``. Một số tính năng debug cũng có thể được bật hoặc tắt tùy ý, nhưng có thể yêu cầu khởi động lại scene để có hiệu lực.

.. image:: img/nav_debug_settings.png

Các polygon navigation mesh debug
---------------------------------

Nếu ``enable_edge_lines`` được bật, các cạnh của polygon navigation mesh sẽ được làm nổi bật. Nếu ``enable_edge_lines_xray`` cũng được bật, các cạnh của navigation mesh sẽ hiển thị xuyên qua hình học.

Nếu ``enable_geometry_face_random_color`` được bật, màu của mỗi mặt navigation mesh sẽ được trộn với một màu ngẫu nhiên, sau đó màu này tiếp tục được trộn với màu được chỉ định trong ``geometry_face_color``.

.. image:: img/nav_debug_xray_edge_lines.png

Các kết nối cạnh debug
----------------------

Khi hai navigation mesh được kết nối trong phạm vi khoảng cách ``edge_connection_margin``, kết nối đó sẽ được phủ lớp hiển thị. Màu của lớp phủ được điều khiển bởi ``edge_connection_color``. Có thể làm cho các kết nối hiển thị xuyên qua hình học bằng ``enable_edge_connections_xray``.

.. image:: img/nav_edge_connection2d.gif

.. image:: img/nav_edge_connection3d.gif

.. note::

    Các kết nối cạnh chỉ hiển thị khi NavigationServer đang hoạt động.

Hiệu năng debug
---------------

Để đo hiệu năng của NavigationServer, có một monitor chuyên dụng nằm trong Editor Debugger tại *Debugger->Monitors->Navigation Process*.

.. image:: img/navigation_debug_performance1.webp

Navigation Process hiển thị thời gian NavigationServer dành cho việc cập nhật các thành phần nội bộ trong frame cập nhật này, tính bằng mili giây. Navigation Process hoạt động tương tự Process trong việc render frame hình ảnh và Physics Process trong việc xử lý va chạm và các cập nhật cố định.

Navigation Process tính tất cả các cập nhật đối với **navigation maps**, **navigation regions** và **navigation agents**, cũng như toàn bộ **avoidance calculations** cho frame cập nhật.

.. note::

    Navigation Process KHÔNG bao gồm hiệu năng pathfinding, vì pathfinding hoạt động độc lập trên dữ liệu navigation map với quá trình cập nhật của server.

Nhìn chung, Navigation Process nên được giữ ở mức thấp và ổn định nhất có thể để đảm bảo hiệu năng runtime, nhằm tránh các vấn đề về frame rate. Lưu ý rằng vì quá trình cập nhật của NavigationServer diễn ra ở giữa quá trình cập nhật physics, việc Navigation Process tăng lên sẽ tự động làm Physics Process tăng cùng một lượng.

Navigation cũng cung cấp các thống kê chi tiết hơn về các đối tượng liên quan đến navigation hiện tại và cấu tạo của navigation map trên NavigationServer.

.. image:: img/navigation_debug_performance2.webp

Không thể đánh giá các thống kê navigation được hiển thị ở đây là tốt hay xấu đối với hiệu năng, vì điều này hoàn toàn phụ thuộc vào dự án và những gì được xem là hợp lý hoặc quá mức nghiêm trọng.

Các thống kê navigation giúp xác định những nút thắt hiệu năng ít rõ ràng hơn, vì nguồn gây ra vấn đề có thể không phải lúc nào cũng có biểu diễn trực quan. Ví dụ: các vấn đề về hiệu năng pathfinding do navigation mesh quá chi tiết với hàng nghìn cạnh / polygon, hoặc các vấn đề do navigation procedural hoạt động không đúng.
