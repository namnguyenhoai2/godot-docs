.. _doc_navigation_different_actor_area_access:

Hỗ trợ quyền truy cập các khu vực khác nhau của actor
=====================================================

.. image:: img/nav_actor_doors.png

Một ví dụ điển hình về quyền truy cập các khu vực khác nhau trong gameplay là những cánh cửa kết nối các phòng có navigation mesh khác nhau và không phải lúc nào cũng cho phép tất cả actor đi qua.

Thêm một NavigationRegion tại vị trí cánh cửa. Thêm một navigation mesh phù hợp có kích thước bằng cánh cửa và có thể kết nối với các navigation mesh xung quanh. Để kiểm soát quyền truy cập, hãy bật / tắt các bit của navigation layer để những path query sử dụng cùng các bit của navigation layer có thể tìm thấy đường đi qua navigation mesh của "cánh cửa".

Bitmask có thể hoạt động như một tập hợp các chìa khóa hoặc khả năng của cánh cửa, và chỉ những actor có ít nhất một bit layer khớp và được bật trong pathfinding query của chúng mới tìm thấy đường đi qua region này. Xem :ref:`doc_navigation_advanced_using_navigationlayers` để biết thêm thông tin về cách làm việc với navigation layer và bitmask.

.. image:: img/nav_actor_doorbitmask.png

Toàn bộ region của "cánh cửa" cũng có thể được bật / tắt nếu cần, nhưng nếu bị tắt thì sẽ chặn quyền truy cập đối với mọi path query.

Bất cứ khi nào có thể, hãy ưu tiên làm việc với navigation layer trong path query, vì việc bật hoặc tắt navigation layer trên một region sẽ kích hoạt quá trình tính toán lại tốn kém đối với các kết nối của navigation map.

.. warning::

    Việc thay đổi navigation layer chỉ ảnh hưởng đến các path query mới, không tự động cập nhật những path hiện có.
