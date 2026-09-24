.. _doc_navigation_different_actor_area_access:

Hỗ trợ quyền truy cập các khu vực khác nhau theo tác nhân
=========================================================

.. image:: img/nav_actor_doors.png

Một ví dụ điển hình về quyền truy cập các khu vực khác nhau trong gameplay là những cánh cửa kết nối các phòng có navigation mesh khác nhau và không phải lúc nào cũng cho phép mọi tác nhân đi qua.

Thêm một NavigationRegion tại vị trí cánh cửa. Thêm một navigation mesh phù hợp có kích thước bằng cánh cửa và có thể kết nối với các navigation mesh xung quanh. Để kiểm soát quyền truy cập, hãy bật / tắt các bit của navigation layer để những truy vấn đường đi sử dụng cùng các bit của navigation layer có thể tìm được đường đi qua navigation mesh của "cánh cửa".

Bitmask có thể hoạt động như một tập hợp các chìa khóa hoặc khả năng của cửa, và chỉ những tác nhân có ít nhất một lớp bit tương ứng và được bật trong truy vấn tìm đường mới tìm được đường đi qua vùng này. Xem :ref:`doc_navigation_advanced_using_navigationlayers` để biết thêm thông tin về cách làm việc với navigation layer và bitmask.

.. image:: img/nav_actor_doorbitmask.png

Toàn bộ vùng "cánh cửa" cũng có thể được bật / tắt khi cần, nhưng nếu bị tắt thì sẽ chặn quyền truy cập đối với mọi truy vấn đường đi.

Khi có thể, hãy ưu tiên sử dụng navigation layer trong các truy vấn đường đi, vì việc bật hoặc tắt navigation layer trên một vùng sẽ kích hoạt quá trình tính toán lại tốn kém các kết nối của navigation map.

.. warning::

    Việc thay đổi navigation layer chỉ ảnh hưởng đến các truy vấn đường đi mới, chứ không tự động cập nhật các đường đi hiện có.
