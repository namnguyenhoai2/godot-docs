.. _doc_canvas_layers:

Các layer Canvas
================

Viewport và CanvasItem
----------------------

:ref:`CanvasItem <class_CanvasItem>` là nền tảng cho tất cả node 2D, dù là các node 2D thông thường như :ref:`Node2D <class_Node2D>` hay :ref:`Control <class_Control>`. Cả hai đều kế thừa từ :ref:`CanvasItem <class_CanvasItem>`. Bạn có thể sắp xếp các CanvasItem trong các cây. Mỗi item sẽ kế thừa transform của node cha: khi node cha di chuyển, các node con cũng di chuyển theo.

Các node CanvasItem và những node kế thừa từ chúng là các node con trực tiếp hoặc gián tiếp của một
:ref:`Viewport <class_Viewport>`, node này sẽ hiển thị chúng.

Thuộc tính
:ref:`Viewport.canvas_transform <class_Viewport_property_canvas_transform>` của Viewport cho phép áp dụng một transform :ref:`Transform2D <class_Transform2D>` tùy chỉnh cho hệ thống phân cấp CanvasItem mà nó chứa. Các node như
:ref:`Camera2D <class_Camera2D>` hoạt động bằng cách thay đổi transform đó.

Để tạo các hiệu ứng như cuộn, việc thao tác với thuộc tính canvas transform sẽ hiệu quả hơn so với việc di chuyển CanvasItem gốc và toàn bộ scene cùng với nó.

Tuy nhiên, thông thường chúng ta không muốn *mọi thứ* trong game hoặc ứng dụng chịu tác động của canvas transform. Ví dụ:

-  **Parallax Backgrounds**: Các background di chuyển chậm hơn phần còn lại của stage.
-  **UI**: Hãy hình dung một giao diện người dùng (UI) hoặc màn hình hiển thị thông tin (HUD) được chồng lên khung nhìn của chúng ta về thế giới game. Chúng ta muốn bộ đếm mạng, màn hình điểm số và các phần tử khác giữ nguyên vị trí trên màn hình ngay cả khi khung nhìn về thế giới game thay đổi.
-  **Transitions**: Chúng ta có thể muốn các hiệu ứng hình ảnh dùng cho transitions (fade, blend) vẫn ở một vị trí cố định trên màn hình.

Làm thế nào để giải quyết những vấn đề này trong một scene tree duy nhất?

CanvasLayers
------------

Câu trả lời là :ref:`CanvasLayer <class_CanvasLayer>`, một node thêm một layer rendering 2D riêng cho tất cả node con và node cháu của nó. Các node con của Viewport mặc định sẽ được vẽ ở layer "0", còn CanvasLayer sẽ được vẽ ở bất kỳ layer số nào. Các layer có số lớn hơn sẽ được vẽ phía trên các layer có số nhỏ hơn. CanvasLayer cũng có transform riêng và không phụ thuộc vào transform của các layer khác. Điều này cho phép UI được cố định trong screen-space trong khi khung nhìn của chúng ta về thế giới game thay đổi.

Một ví dụ là tạo background parallax. Có thể thực hiện việc này bằng một CanvasLayer ở layer "-1". Màn hình chứa điểm số, bộ đếm mạng và nút tạm dừng cũng có thể được tạo ở layer "1".

Đây là sơ đồ minh họa:

.. image:: img/canvaslayers.png

CanvasLayer độc lập với thứ tự trong cây và chỉ phụ thuộc vào số layer của chúng, vì vậy chúng có thể được khởi tạo khi cần.

.. note::   CanvasLayer không cần thiết để kiểm soát thứ tự vẽ của các node. Cách tiêu chuẩn để đảm bảo một node được vẽ chính xác 'phía trước' hoặc 'phía sau' các node khác là điều chỉnh thứ tự của các node trong scene panel. Trái với trực giác, các node ở trên cùng trong scene panel được vẽ *phía sau* các node thấp hơn trong viewport. Các node 2D cũng có thuộc tính :ref:`CanvasItem.z_index <class_CanvasItem_property_z_index>` để kiểm soát thứ tự vẽ của chúng.
