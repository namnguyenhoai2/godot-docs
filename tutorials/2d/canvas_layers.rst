.. _doc_canvas_layers:

Các lớp Canvas
==============

Các mục Viewport và Canvas
--------------------------

:ref:`CanvasItem <class_CanvasItem>` is the base for all 2D nodes, be it regular
Các node 2D, chẳng hạn như :ref:`Node2D <class_Node2D>`, hoặc :ref:`Control <class_Control>`. Cả hai đều kế thừa từ :ref:`CanvasItem <class_CanvasItem>`. Bạn có thể sắp xếp các mục canvas thành các cây. Mỗi mục sẽ kế thừa phép biến đổi của mục cha: khi mục cha di chuyển, các mục con của nó cũng di chuyển theo.

Các node CanvasItem và những node kế thừa từ chúng là các node con trực tiếp hoặc gián tiếp của một
:ref:`Viewport <class_Viewport>`, that displays them.

Thuộc tính của Viewport
:ref:`Viewport.canvas_transform <class_Viewport_property_canvas_transform>`,
cho phép áp dụng một phép biến đổi :ref:`Transform2D <class_Transform2D>` tùy chỉnh cho hệ phân cấp CanvasItem mà nó chứa. Các node như
:ref:`Camera2D <class_Camera2D>` work by changing that transform.

Để tạo ra các hiệu ứng như cuộn, việc thao tác với thuộc tính canvas transform sẽ hiệu quả hơn so với việc di chuyển mục canvas gốc và toàn bộ cảnh cùng với nó.

Tuy nhiên, thông thường chúng ta không muốn *mọi thứ* trong trò chơi hoặc ứng dụng chịu tác động của phép biến đổi canvas. Ví dụ:

-  **Nền Parallax**: Nền di chuyển chậm hơn phần còn lại của màn chơi. - **UI**: Hãy nghĩ đến một giao diện người dùng (UI) hoặc màn hình hiển thị thông tin (HUD) được chồng lên khung nhìn của chúng ta về thế giới trò chơi. Chúng ta muốn bộ đếm mạng, bảng điểm và các thành phần khác giữ nguyên vị trí trên màn hình ngay cả khi khung nhìn của chúng ta về thế giới trò chơi thay đổi. - **Chuyển cảnh**: Chúng ta có thể muốn các hiệu ứng hình ảnh được dùng cho chuyển cảnh (mờ dần, hòa trộn) vẫn ở một vị trí cố định trên màn hình.

Làm thế nào để giải quyết các vấn đề này trong một cây cảnh duy nhất?

CanvasLayers
------------

Câu trả lời là :ref:`CanvasLayer <class_CanvasLayer>`, một node bổ sung một lớp kết xuất 2D riêng cho tất cả các node con và node cháu của nó. Theo mặc định, các node con của Viewport sẽ được vẽ ở lớp "0", trong khi CanvasLayer sẽ được vẽ ở bất kỳ lớp số nào. Các lớp có số lớn hơn sẽ được vẽ phía trên các lớp có số nhỏ hơn. CanvasLayer cũng có phép biến đổi riêng và không phụ thuộc vào phép biến đổi của các lớp khác. Điều này cho phép UI được cố định trong không gian màn hình trong khi khung nhìn của chúng ta về thế giới trò chơi thay đổi.

Một ví dụ là tạo nền parallax. Có thể thực hiện việc này bằng một CanvasLayer ở lớp "-1". Màn hình hiển thị điểm số, bộ đếm mạng và nút tạm dừng cũng có thể được tạo ở lớp "1".

Dưới đây là sơ đồ minh họa:

.. image:: img/canvaslayers.png

CanvasLayer độc lập với thứ tự trong cây và chỉ phụ thuộc vào số lớp, vì vậy chúng có thể được khởi tạo khi cần.

.. note::   CanvasLayers aren't necessary to control the drawing order of nodes.
            Cách tiêu chuẩn để đảm bảo một node được vẽ đúng 'phía trước' hoặc 'phía sau' các node khác là điều chỉnh thứ tự của các node trong bảng scene. Trái với trực giác, các node ở trên cùng trong bảng scene được vẽ *phía sau* các node bên dưới trong viewport. Các node 2D cũng có thuộc tính :ref:`CanvasItem.z_index <class_CanvasItem_property_z_index>` để kiểm soát thứ tự vẽ của chúng.
