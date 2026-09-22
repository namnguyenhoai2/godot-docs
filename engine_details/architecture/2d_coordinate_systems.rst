.. _doc_2d_coordinate_systems:

Hệ tọa độ 2D và phép biến đổi 2D
================================

Giới thiệu
----------

Đây là phần tổng quan chi tiết về các hệ tọa độ 2D và phép biến đổi 2D tích hợp sẵn. Các khái niệm cơ bản được trình bày trong :ref:`doc_viewport_and_canvas_transforms`.

:ref:`Transform2D <class_Transform2D>` là các ma trận chuyển đổi tọa độ từ hệ tọa độ này sang hệ tọa độ khác. Để sử dụng chúng, bạn nên biết những hệ tọa độ nào có sẵn trong Godot. Để hiểu sâu hơn, tutorial :ref:`doc_matrices_and_transforms` cung cấp thông tin chi tiết về chức năng bên dưới.

Hệ tọa độ 2D của Godot
----------------------

Hình minh họa sau đây cung cấp tổng quan về các hệ tọa độ 2D của Godot và các node-transform, transform-function cũng như các function liên quan đến hệ tọa độ hiện có. Bên trái là màn hình OS Window Manager, bên phải là :ref:`CanvasItems <class_CanvasItem>`. Vì lý do đơn giản, hình minh họa này không bao gồm :ref:`SubViewport <class_SubViewport>`,
:ref:`SubViewportContainer <class_SubViewportContainer>`, :ref:`ParallaxLayer<class_ParallaxLayer>` và :ref:`ParallaxBackground<class_ParallaxBackground>`, tất cả đều ảnh hưởng đến các phép biến đổi.

Hình minh họa dựa trên cây node có dạng sau: ``Root Window (embed Windows)`` ⇒ ``Window (don't embed Windows)`` ⇒ ``CanvasLayer`` ⇒ ``CanvasItem`` ⇒ ``CanvasItem`` ⇒ ``CanvasItem``. Có thể có những tổ hợp phức tạp hơn, chẳng hạn như Window và SubViewport lồng sâu, tuy nhiên ví dụ này nhằm cung cấp tổng quan về phương pháp nói chung.

.. image:: img/transforms_overview.webp
    :target: ../../_images/transforms_overview.webp

Nhấp vào hình minh họa để phóng to.

- **Tọa độ Item**
    Đây là hệ tọa độ cục bộ của một :ref:`CanvasItem <class_CanvasItem>`.

- **Tọa độ Item cha**
    Đây là hệ tọa độ cục bộ của *CanvasItem* của node cha. Khi định vị các *CanvasItems* trong *Canvas*, chúng thường kế thừa các phép biến đổi của *CanvasItems* cha. Một ngoại lệ là
    :ref:`CanvasItems.top_level <class_CanvasItem_property_top_level>`.

- **Tọa độ Canvas**
    Như đã đề cập trong tutorial trước :ref:`doc_canvas_layers`, có hai loại canvas (*Viewport* canvas và *CanvasLayer* canvas), và cả hai đều có hệ tọa độ canvas. Chúng còn được gọi là tọa độ thế giới. Một *Viewport* có thể chứa nhiều *Canvases* với các hệ tọa độ khác nhau.

- **Tọa độ Viewport**
    Đây là hệ tọa độ của :ref:`Viewport <class_Viewport>`.

- **Tọa độ Camera**
    Hệ tọa độ này chỉ được sử dụng nội bộ cho các chức năng như phép chiếu tia của camera 3D.

- **Tọa độ Embedder / Tọa độ màn hình**
    Mỗi *Viewport* (*Window* hoặc *SubViewport*) trong scene tree được nhúng vào một node khác hoặc vào OS Window Manager. Gốc của hệ tọa độ này trùng với góc trên bên trái của *Window* hoặc *SubViewport*, còn tỷ lệ của nó là tỷ lệ của embedder hoặc OS Window Manager.

    Nếu embedder là OS Window Manager, chúng cũng được gọi là Tọa độ màn hình.

- **Tọa độ Embedder tuyệt đối / Tọa độ màn hình tuyệt đối**
    Gốc của hệ tọa độ này là góc trên bên trái của node nhúng hoặc màn hình OS Window Manager. Tỷ lệ của nó là tỷ lệ của embedder hoặc OS Window Manager.

    Nếu embedder là OS Window Manager, chúng cũng được gọi là Tọa độ màn hình tuyệt đối.


Các phép biến đổi của node
--------------------------

Mỗi node được đề cập đều có một hoặc nhiều phép biến đổi liên kết với nó, và sự kết hợp của các node này suy ra các phép biến đổi giữa những hệ tọa độ khác nhau. Ngoại trừ một vài trường hợp, các phép biến đổi là :ref:`Transform2D <class_Transform2D>`, và danh sách sau đây trình bày chi tiết cũng như tác động của từng phép biến đổi.

- **Phép biến đổi CanvasItem**
    *CanvasItems* là các node *Control* hoặc node *Node2D*.

    Đối với các node *Control*, phép biến đổi này bao gồm một :ref:`position <class_Control_property_position>` so với gốc của node cha, cùng với một :ref:`scale <class_Control_property_scale>` và
    :ref:`rotation <class_Control_property_rotation>` quanh một
    :ref:`điểm pivot <class_Control_property_pivot_offset>`.

    Đối với các node *Node2D*, :ref:`transform <class_Node2D_property_transform>` bao gồm
    :ref:`position <class_Node2D_property_position>`, :ref:`rotation <class_Node2D_property_rotation>`,
    :ref:`scale <class_Node2D_property_scale>` và :ref:`skew <class_Node2D_property_skew>`.

    Phép biến đổi ảnh hưởng đến chính item đó và thường cả các *CanvasItems* con; trong trường hợp là một *SubViewportContainer*, nó ảnh hưởng đến *SubViewport* được chứa bên trong.

- **Phép biến đổi CanvasLayer**
    *CanvasLayer's* :ref:`transform <class_CanvasLayer_property_transform>` ảnh hưởng đến tất cả *CanvasItems* bên trong *CanvasLayer*. Nó không ảnh hưởng đến các *CanvasLayers* hoặc *Windows* khác trong *Viewport* của nó.

- **Phép biến đổi CanvasLayer follow viewport**
    *follow viewport transform* là một phép biến đổi được tự động tính toán, dựa trên *Viewport's* :ref:`canvas transform <class_Viewport_property_canvas_transform>` và *CanvasLayer's* :ref:`follow viewport scale <class_CanvasLayer_property_follow_viewport_scale>`, đồng thời có thể được sử dụng, nếu :ref:`enabled <class_CanvasLayer_property_follow_viewport_enabled>`, để tạo hiệu ứng pseudo-3D. Nó ảnh hưởng đến cùng các node con như *CanvasLayer transform*.

- **Phép biến đổi canvas của Viewport**
    :ref:`canvas transform <class_Viewport_property_canvas_transform>` ảnh hưởng đến tất cả *CanvasItems* trong canvas mặc định của *Viewport's*. Nó cũng ảnh hưởng đến *CanvasLayers* đã bật follow viewport transform. *Viewport's* đang hoạt động :ref:`Camera2D <class_Camera2D>` hoạt động bằng cách thay đổi phép biến đổi này. Nó không ảnh hưởng đến các *Windows* được nhúng trong *Viewport's* này.

- **Phép biến đổi canvas toàn cục của Viewport**
    *Viewports* cũng có :ref:`global canvas transform <class_Viewport_property_global_canvas_transform>`. Đây là phép biến đổi chính, ảnh hưởng đến tất cả các phép biến đổi riêng lẻ của *Canvas Layer* và *Window* được nhúng. Phép biến đổi này chủ yếu được sử dụng trong CanvasItem Editor của Godot.

- **Biến đổi stretch của Viewport**
    Cuối cùng, *Viewports* có một *stretch transform*, được sử dụng khi thay đổi kích thước hoặc kéo giãn viewport. Transform này được sử dụng cho :ref:`Windows <class_Window>` như mô tả trong
    :ref:`doc_multiple_resolutions`, nhưng cũng có thể được đặt thủ công trên *SubViewports* bằng cách sử dụng
    :ref:`size <class_SubViewport_property_size>` và
    :ref:`size_2d_override <class_SubViewport_property_size_2d_override>`. Các giá trị của nó
    :ref:`translation <class_Transform2D_method_get_origin>`,
    :ref:`rotation <class_Transform2D_method_get_rotation>` và
    :ref:`skew <class_Transform2D_method_get_skew>` là các giá trị mặc định và nó chỉ có thể có :ref:`scale <class_Transform2D_method_get_scale>` khác mặc định.

- **Biến đổi Window**
    Để scale và định vị nội dung của *Window* như mô tả trong
    :ref:`doc_multiple_resolutions`, mỗi :ref:`Window <class_Window>` chứa một *window transform*. Ví dụ, nó chịu trách nhiệm tạo ra các dải màu đen ở hai bên của *Window* để *Viewport* được hiển thị với tỷ lệ khung hình cố định.

- **Vị trí Window**
    Mỗi *Window* cũng có một :ref:`position <class_Window_property_position>` để mô tả vị trí của nó bên trong trình nhúng. Trình nhúng có thể là một *Viewport* khác hoặc OS Window Manager.

- **Biến đổi shrink của SubViewportContainer**
    :ref:`stretch <class_SubViewportContainer_property_stretch>` cùng với
    :ref:`stretch_shrink <class_SubViewportContainer_property_stretch_shrink>` xác định cho một *SubViewportContainer* xem và theo hệ số nguyên nào *SubViewport* được chứa bên trong cần được scale so với kích thước của container.
