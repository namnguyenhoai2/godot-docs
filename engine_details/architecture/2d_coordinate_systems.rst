.. _doc_2d_coordinate_systems:

Hệ tọa độ 2D và phép biến đổi 2D
================================

Giới thiệu
----------

Đây là phần tổng quan chi tiết về các hệ tọa độ 2D và phép biến đổi 2D có sẵn được tích hợp sẵn. Các khái niệm cơ bản được trình bày trong :ref:`doc_viewport_and_canvas_transforms`.

:ref:`Transform2D <class_Transform2D>` are matrices that convert coordinates from one coordinate
hệ thống này sang hệ thống khác. Để sử dụng chúng, bạn nên biết những hệ tọa độ nào có sẵn trong Godot. Để hiểu sâu hơn, hướng dẫn :ref:`doc_matrices_and_transforms` cung cấp thông tin chi tiết về chức năng nền tảng.

Hệ tọa độ 2D của Godot
----------------------

Hình minh họa sau đây cung cấp cái nhìn tổng quan về các hệ tọa độ 2D của Godot cũng như các phép biến đổi node, hàm biến đổi và hàm liên quan đến hệ tọa độ hiện có. Bên trái là màn hình của OS Window Manager, bên phải là :ref:`CanvasItems <class_CanvasItem>`. Vì lý do đơn giản, hình minh họa này không bao gồm :ref:`SubViewport <class_SubViewport>`,
:ref:`SubViewportContainer <class_SubViewportContainer>`, :ref:`ParallaxLayer<class_ParallaxLayer>`
và :ref:`ParallaxBackground<class_ParallaxBackground>`, tất cả đều ảnh hưởng đến các phép biến đổi.

Hình minh họa dựa trên cây node có dạng sau: ``Root Window (embed Windows)`` ⇒ ``Window (don't embed Windows)`` ⇒ ``CanvasLayer`` ⇒ ``CanvasItem`` ⇒ ``CanvasItem`` ⇒ ``CanvasItem``. Có thể có những kết hợp phức tạp hơn, chẳng hạn như Window và SubViewport lồng nhau nhiều cấp, tuy nhiên ví dụ này nhằm cung cấp cái nhìn tổng quan về phương pháp nói chung.

.. image:: img/transforms_overview.webp
    :target: ../../_images/transforms_overview.webp

Nhấp vào hình minh họa để phóng to.

- **Tọa độ của item** Đây là hệ tọa độ cục bộ của một :ref:`CanvasItem <class_CanvasItem>`.

- **Tọa độ của item cha** Đây là hệ tọa độ cục bộ của *CanvasItem* cha. Khi định vị *CanvasItems* trong *Canvas*, chúng thường kế thừa các phép biến đổi của *CanvasItems* cha. Một ngoại lệ là
    :ref:`CanvasItems.top_level <class_CanvasItem_property_top_level>`.

- **Tọa độ Canvas** Như đã đề cập trong hướng dẫn trước :ref:`doc_canvas_layers`, có hai loại canvas (*Viewport* canvas và *CanvasLayer* canvas), và cả hai đều có một hệ tọa độ canvas. Các tọa độ này còn được gọi là tọa độ thế giới. Một *Viewport* có thể chứa nhiều *Canvas* với các hệ tọa độ khác nhau.

- **Tọa độ Viewport** Đây là hệ tọa độ của :ref:`Viewport <class_Viewport>`.

- **Tọa độ Camera** Hệ tọa độ này chỉ được sử dụng nội bộ cho các chức năng như phép chiếu tia từ camera 3D.

- **Tọa độ Embedder / Tọa độ màn hình** Mỗi *Viewport* (*Window* hoặc *SubViewport*) trong cây cảnh được nhúng vào một node khác hoặc vào OS Window Manager. Gốc của hệ tọa độ này trùng với góc trên bên trái của *Window* hoặc *SubViewport*, còn tỷ lệ của nó là tỷ lệ của embedder hoặc OS Window Manager.

    Nếu embedder là OS Window Manager thì chúng cũng được gọi là Tọa độ màn hình.

- **Tọa độ Embedder tuyệt đối / Tọa độ màn hình tuyệt đối** Gốc của hệ tọa độ này là góc trên bên trái của node nhúng hoặc màn hình của OS Window Manager. Tỷ lệ của nó là tỷ lệ của embedder hoặc OS Window Manager.

    Nếu embedder là OS Window Manager thì chúng cũng được gọi là Tọa độ màn hình tuyệt đối.


Các phép biến đổi của node
--------------------------

Mỗi node được đề cập đều có một hoặc nhiều phép biến đổi liên kết với nó, và sự kết hợp của các node này xác định các phép biến đổi giữa những hệ tọa độ khác nhau. Ngoại trừ một vài trường hợp, các phép biến đổi là :ref:`Transform2D <class_Transform2D>`, và danh sách sau đây trình bày chi tiết cũng như tác động của từng phép biến đổi.

- **Phép biến đổi CanvasItem** *CanvasItems* có thể là các node *Control* hoặc *Node2D*.

    Đối với các node *Control*, phép biến đổi này bao gồm một :ref:`position <class_Control_property_position>` tương đối so với gốc của node cha và một :ref:`scale <class_Control_property_scale>` và
    :ref:`rotation <class_Control_property_rotation>` around a
    :ref:`pivot point <class_Control_property_pivot_offset>`.

    Đối với các node *Node2D*, :ref:`transform <class_Node2D_property_transform>` bao gồm
    :ref:`position <class_Node2D_property_position>`, :ref:`rotation <class_Node2D_property_rotation>`,
    :ref:`scale <class_Node2D_property_scale>` and :ref:`skew <class_Node2D_property_skew>`.

    Phép biến đổi này tác động lên chính item đó và thường cũng tác động lên các *CanvasItems* con; trong trường hợp của một *SubViewportContainer*, nó tác động lên *SubViewport* được chứa bên trong.

- **Phép biến đổi CanvasLayer** :ref:`transform <class_CanvasLayer_property_transform>` của *CanvasLayer* tác động lên tất cả *CanvasItems* bên trong *CanvasLayer*. Nó không tác động lên các *CanvasLayers* khác hoặc *Windows* trong *Viewport* của nó.

- **Phép biến đổi CanvasLayer theo viewport** *Phép biến đổi theo viewport* là một phép biến đổi được tự động tính toán, dựa trên :ref:`canvas transform <class_Viewport_property_canvas_transform>` của *Viewport* và :ref:`follow viewport scale <class_CanvasLayer_property_follow_viewport_scale>` của *CanvasLayer*, và có thể được sử dụng nếu :ref:`enabled <class_CanvasLayer_property_follow_viewport_enabled>` để tạo hiệu ứng giả 3D. Nó tác động lên cùng các node con như *phép biến đổi CanvasLayer*.

- **Phép biến đổi canvas của Viewport** :ref:`canvas transform <class_Viewport_property_canvas_transform>` tác động lên tất cả *CanvasItems* trong canvas mặc định của *Viewport*. Nó cũng tác động lên các *CanvasLayers* đã bật phép biến đổi theo viewport. :ref:`Camera2D <class_Camera2D>` đang hoạt động của *Viewport* hoạt động bằng cách thay đổi phép biến đổi này. Nó không tác động lên các *Windows* được nhúng trong *Viewport* này.

- **Phép biến đổi canvas toàn cục của Viewport** *Viewports* cũng có :ref:`global canvas transform <class_Viewport_property_global_canvas_transform>`. Đây là phép biến đổi chính và tác động lên tất cả các phép biến đổi riêng lẻ của *Canvas Layer* và *Window* được nhúng. Phép biến đổi này chủ yếu được sử dụng trong Trình chỉnh sửa CanvasItem của Godot.

- **Phép biến đổi co giãn Viewport** Cuối cùng, *Viewports* có một *phép biến đổi co giãn*, được sử dụng khi thay đổi kích thước hoặc co giãn viewport. Phép biến đổi này được sử dụng cho :ref:`Windows <class_Window>` như mô tả trong
    :ref:`doc_multiple_resolutions`, but can also be manually set on *SubViewports* by means of
    :ref:`size <class_SubViewport_property_size>` and
    :ref:`size_2d_override <class_SubViewport_property_size_2d_override>`. Its
    :ref:`translation <class_Transform2D_method_get_origin>`,
    :ref:`rotation <class_Transform2D_method_get_rotation>` and
    :ref:`skew <class_Transform2D_method_get_skew>` are the default values and it can only have
    :ref:`scale <class_Transform2D_method_get_scale>` không mặc định.

- **Phép biến đổi Window** Để co giãn và định vị nội dung của *Window* như mô tả trong
    :ref:`doc_multiple_resolutions`, each :ref:`Window <class_Window>` contains a
    *phép biến đổi window*. Ví dụ, nó chịu trách nhiệm tạo các dải màu đen ở hai bên *Window* để *Viewport* được hiển thị với tỷ lệ khung hình cố định.

- **Vị trí Window** Mỗi *Window* cũng có một :ref:`position <class_Window_property_position>` để mô tả vị trí của nó bên trong embedder. Embedder có thể là một *Viewport* khác hoặc OS Window Manager.

- **Phép biến đổi thu nhỏ SubViewportContainer**
    :ref:`stretch <class_SubViewportContainer_property_stretch>` together with
    :ref:`stretch_shrink <class_SubViewportContainer_property_stretch_shrink>` declare for a
    *SubViewportContainer* có nên thu nhỏ *SubViewport* được chứa hay không và nếu có thì theo hệ số nguyên nào so với kích thước của container.
