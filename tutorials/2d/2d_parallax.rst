.. _doc_2d_parallax:

Parallax 2D
===========

Giới thiệu
----------

Parallax là hiệu ứng được dùng để mô phỏng chiều sâu bằng cách cho các texture di chuyển với tốc độ khác nhau tương đối so với camera. Godot cung cấp node :ref:`Parallax2D<class_parallax2d>` để tạo hiệu ứng này. Tuy vậy, bạn vẫn có thể dễ mắc lỗi, vì thế trang này cung cấp mô tả chuyên sâu về một số thuộc tính và cách khắc phục một số lỗi thường gặp.

.. note::

    Trang này hướng dẫn cách sử dụng :ref:`Parallax2D<class_parallax2d>`, được khuyến nghị dùng thay cho :ref:`ParallaxLayer<class_parallaxlayer>` và
    các node :ref:`ParallaxBackground<class_parallaxbackground>`.

Bắt đầu
-------

Node parallax hỗ trợ thêm các node dùng để render nội dung dưới dạng node con, vì vậy bạn có thể sử dụng một hoặc nhiều node để tạo thành mỗi layer. Để bắt đầu, hãy đặt từng node hoặc nhóm node mà bạn muốn cuộn độc lập làm node con của node parallax riêng. Đảm bảo góc trên bên trái của các texture được sử dụng nằm tại giao điểm ``(0, 0)``, như trong hình bên dưới. Xem phần :ref:`định vị <doc_2d_parallax_positioning>` để biết tại sao điều này quan trọng.

.. image:: img/2d_parallax_size_viewport.webp

Scene ở trên sử dụng một texture đã chuẩn bị cho những đám mây ở phía trên trong một :ref:`Sprite2D <class_sprite2d>`, nhưng bạn cũng có thể dễ dàng sử dụng nhiều node được giãn cách để tạo thành layer.

Tỷ lệ cuộn
----------

Nền tảng của hiệu ứng parallax là thuộc tính :ref:`scroll_scale <class_parallax2d_property_scroll_scale>`. Thuộc tính này hoạt động như một hệ số nhân tốc độ cuộn, cho phép các layer di chuyển với tốc độ khác camera trên từng trục được thiết lập. Giá trị 1 khiến node parallax cuộn với cùng tốc độ với camera. Nếu muốn hình ảnh trông xa hơn khi cuộn, hãy dùng giá trị nhỏ hơn 1, trong đó 0 sẽ khiến hình ảnh dừng hoàn toàn. Nếu muốn một đối tượng trông gần camera hơn, hãy dùng giá trị lớn hơn 1 để đối tượng cuộn nhanh hơn.

Scene ở trên gồm năm layer. Một số giá trị :ref:`scroll_scale <class_parallax2d_property_scroll_scale>` phù hợp có thể là:

- ``(0.7, 1)`` - Rừng
- ``(0.5, 1)`` - Đồi
- ``(0.3, 1)`` - Mây phía dưới
- ``(0.2, 1)`` - Mây phía trên
- ``(0.1, 1)`` - Bầu trời

Video bên dưới minh họa cách các giá trị này ảnh hưởng đến việc cuộn trong game:

.. video:: video/2d_parallax_scroll_scale.webm
   :alt: A scene with five layers scrolling at different speeds
   :autoplay:
   :loop:
   :muted:
   :align: default

Lặp vô hạn
----------

:ref:`Parallax2D<class_parallax2d>` cung cấp một hiệu ứng bổ sung, tạo ảo giác rằng các texture được lặp vô hạn.
:ref:`repeat_size<class_parallax2d_property_repeat_size>` yêu cầu node nhảy vị trí về phía trước hoặc phía sau khi camera cuộn một khoảng bằng giá trị đã thiết lập. Hiệu ứng này được tạo ra bằng cách thêm một bản lặp duy nhất cho tất cả canvas item con, được offset theo giá trị đó. Khi camera cuộn giữa hình ảnh và bản lặp của nó, vị trí sẽ âm thầm nhảy về sau, tạo cảm giác hình ảnh đang lặp.

.. image:: img/2d_parallax_scroll.gif

Vì đây là một hiệu ứng nhạy cảm, người dùng chưa quen rất dễ mắc lỗi khi thiết lập. Hãy cùng xem xét "cách thức" và "lý do" của một số vấn đề thường gặp.

Kích thước không phù hợp
~~~~~~~~~~~~~~~~~~~~~~~~

Hiệu ứng lặp vô hạn dễ sử dụng nhất khi bạn có một hình ảnh được thiết kế để lặp liền mạch và có kích thước bằng hoặc lớn hơn viewport **trước khi** thiết lập :ref:`repeat_size<class_parallax2d_property_repeat_size>`. Nếu không thể có được asset được thiết kế cho tác vụ này, bạn vẫn có thể làm một số việc khác để chuẩn bị hình ảnh tốt hơn về mặt kích thước.

Dưới đây là ví dụ về một texture quá nhỏ so với viewport:

.. image:: img/2d_parallax_size_bad.webp

Ta có thể thấy kích thước viewport là 500x300 nhưng texture có kích thước 288x208. Nếu đặt
:ref:`repeat_size<class_parallax2d_property_repeat_size>` bằng kích thước hình ảnh, hiệu ứng lặp vô hạn sẽ không cuộn đúng cách vì texture gốc không phủ kín viewport. Nếu đặt
:ref:`repeat_size<class_parallax2d_property_repeat_size>` bằng kích thước viewport, ta sẽ có một khoảng trống lớn. Ta có thể làm gì?

Thu nhỏ viewport
^^^^^^^^^^^^^^^^

Cách đơn giản nhất là đặt viewport có kích thước bằng hoặc nhỏ hơn texture. Trong **Project Settings > Display > Window**, thay đổi các thiết lập
:ref:`Viewport Width <class_ProjectSettings_property_display/window/size/viewport_width>` và :ref:`Viewport Height <class_ProjectSettings_property_display/window/size/viewport_height>` để khớp với nền của bạn.

.. image:: img/2d_parallax_size_viewport.webp

Scale Parallax2D
^^^^^^^^^^^^^^^^

Nếu bạn không hướng đến phong cách pixel-perfect hoặc không ngại hình ảnh hơi mờ, bạn có thể scale texture lớn hơn để vừa với màn hình. Đặt :ref:`scale<class_node2d_property_scale>` của :ref:`Parallax2D<class_parallax2d>`, và tất cả texture con sẽ được scale theo.

Scale các node con
^^^^^^^^^^^^^^^^^^

Tương tự như việc scale :ref:`Parallax2D<class_parallax2d>`, bạn có thể scale các node :ref:`Sprite2D<class_sprite2d>` đủ lớn để phủ kín màn hình. Hãy nhớ rằng một số thiết lập như
:ref:`Parallax2D.repeat_size<class_parallax2d_property_repeat_size>` và
:ref:`Sprite2D.region_rect<class_sprite2d_property_region_rect>` không tính đến việc scale, vì vậy cần điều chỉnh các giá trị này dựa trên tỷ lệ scale.

.. image:: img/2d_parallax_size_scale.webp

Lặp các texture
^^^^^^^^^^^^^^^

Bạn cũng có thể chuẩn bị các node con ngay từ đầu để có được kết quả tốt. Nếu có một
:ref:`Sprite2D<class_sprite2d>` muốn lặp nhưng quá nhỏ, bạn có thể thực hiện các bước sau để lặp nó:

- đặt :ref:`texture_repeat<class_canvasitem_property_texture_repeat>` thành :ref:`CanvasItem.TEXTURE_REPEAT_ENABLED<class_canvasitem_constant_TEXTURE_REPEAT_ENABLED>`
- đặt :ref:`region_enabled<class_sprite2d_property_region_enabled>` thành ``true``
- đặt :ref:`region_rect<class_sprite2d_property_region_rect>` thành một bội số của kích thước texture, đủ lớn để phủ kín viewport.

Bên dưới, bạn có thể thấy rằng việc lặp hình ảnh hai lần khiến nó đủ lớn để phủ kín màn hình.

.. image:: img/2d_parallax_size_repeat.webp

.. _doc_2d_parallax_positioning:

Vị trí không phù hợp
~~~~~~~~~~~~~~~~~~~~

Người dùng thường vô tình đặt tất cả texture nằm chính giữa tại ``(0,0)``:

.. image:: img/2d_parallax_single_centered.webp

Điều này gây ra vấn đề với hiệu ứng lặp vô hạn và nên tránh. "Canvas lặp vô hạn" bắt đầu tại ``(0,0)`` và mở rộng xuống dưới và sang phải theo kích thước của giá trị :ref:`repeat_size<class_parallax2d_property_repeat_size>`.

.. image:: img/2d_parallax_single_expand.webp

Nếu các texture được căn giữa tại giao điểm ``(0,0)``, canvas lặp vô hạn chỉ được phủ một phần, vì vậy nó cũng chỉ được lặp một phần.

Tăng ``repeat_times`` có khắc phục được vấn đề này không?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Về mặt kỹ thuật, việc tăng :ref:`repeat_times<class_parallax2d_property_repeat_times>` *có thể* hoạt động trong một số trường hợp, nhưng đây là giải pháp brute force và không giải quyết đúng vấn đề mà nó được thiết kế để xử lý (chúng ta sẽ xem xét điều này sau). Cách khắc phục tốt hơn là hiểu cách hiệu ứng lặp hoạt động và thiết lập các texture parallax phù hợp ngay từ đầu.

Trước tiên, hãy kiểm tra xem có texture nào tràn sang các phần âm của canvas hay không. Đảm bảo các texture được sử dụng trong node parallax nằm gọn bên trong "canvas lặp vô hạn" bắt đầu tại ``(0,0)``. Như vậy, nếu
:ref:`Parallax2D.repeat_size<class_parallax2d_property_repeat_size>` được thiết lập chính xác, kết quả sẽ trông tương tự như sau, với một vòng lặp duy nhất của hình ảnh có kích thước bằng hoặc lớn hơn viewport:

.. image:: img/2d_parallax_repeat_good_norect.webp

Nếu hình dung cách hình ảnh cuộn trên màn hình, trước tiên nó hiển thị phần nằm trong hình chữ nhật màu đỏ (được xác định bởi :ref:`repeat_size<class_parallax2d_property_repeat_size>`), và khi chạm đến phần nằm trong hình chữ nhật màu vàng, nó nhanh chóng đưa hình ảnh tiến lên để tạo ảo giác cuộn vô hạn.

.. image:: img/2d_parallax_repeat_good.webp

Nếu bạn đặt hình ảnh lệch khỏi "canvas lặp vô hạn", khi camera chạm đến hình chữ nhật màu vàng, một nửa hình ảnh sẽ bị cắt trước khi nhảy tiến lên như trong hình bên dưới:

.. image:: img/2d_parallax_repeat_bad.webp

Độ lệch cuộn
------------

Nếu các texture parallax của bạn đã hoạt động chính xác, nhưng bạn muốn nó bắt đầu từ một vị trí khác,
:ref:`Parallax2D<class_parallax2d>` có thuộc tính :ref:`scroll_offset<class_parallax2d_property_scroll_offset>` dùng để điều chỉnh vị trí bắt đầu của canvas lặp vô hạn. Ví dụ, nếu hình ảnh của bạn có kích thước 288x208, đặt :ref:`scroll_offset<class_parallax2d_property_scroll_offset>` thành ``(-144,0)`` hoặc ``(144,0)`` sẽ cho phép nó bắt đầu từ giữa hình ảnh.

Số lần lặp
----------

Lý tưởng nhất là khi làm theo hướng dẫn này, các texture parallax của bạn đủ lớn để phủ kín màn hình ngay cả khi thu nhỏ. Cho đến lúc này, chúng ta có một texture 288x208 vừa khít bên trong viewport 288x208. Tuy nhiên, vấn đề xảy ra khi chúng ta thu nhỏ bằng cách đặt :ref:`Camera2D.zoom<class_camera2d_property_zoom>` thành ``(0.5, 0.5)``:

.. image:: img/2d_parallax_zoom_single.webp

Mặc dù mọi thứ đã được thiết lập chính xác cho viewport ở mức zoom mặc định, việc thu nhỏ khiến nó nhỏ hơn viewport, làm hỏng hiệu ứng lặp vô hạn. Đây là lúc
:ref:`repeat_times<class_parallax2d_property_repeat_times>` phát huy tác dụng. Khi đặt giá trị ``3`` (thêm một lần lặp ở phía sau và phía trước), nó giờ đã đủ lớn để đáp ứng hiệu ứng lặp vô hạn.

.. image:: img/2d_parallax_zoom_repeat_times.webp

Nếu các texture này được dùng để lặp theo chiều dọc, chúng ta sẽ chỉ định giá trị ``y`` cho
:ref:`repeat_size<class_parallax2d_property_repeat_size>`.
:ref:`repeat_times<class_parallax2d_property_repeat_times>` cũng sẽ tự động thêm một lần lặp ở phía trên và phía dưới. Đây chỉ là parallax theo chiều ngang, nên nó để lại một vùng trống phía trên và phía dưới hình ảnh. Chúng ta giải quyết việc này thế nào? Hãy sáng tạo! Trong ví dụ này, chúng ta kéo giãn bầu trời cao hơn và sprite cỏ thấp hơn. Các texture giờ hỗ trợ mức zoom bình thường cũng như thu nhỏ xuống một nửa kích thước.

.. image:: img/2d_parallax_zoom_repeat_adjusted.webp

Màn hình chia đôi
-----------------

Hầu hết hướng dẫn tạo game màn hình chia đôi trong Godot đều bắt đầu bằng việc viết một script nhỏ để gán :ref:`Viewport.world_2d<class_viewport_property_world_2d>` của SubViewport thứ nhất cho SubViewport thứ hai, để chúng có cùng phần hiển thị. Người dùng thường đặt câu hỏi về cách chia sẻ hiệu ứng parallax giữa cả hai màn hình.

Hiệu ứng parallax giả lập phối cảnh bằng cách di chuyển vị trí của các texture khác nhau theo mối quan hệ với camera. Điều này rõ ràng gây vấn đề nếu bạn có nhiều camera, vì các texture của bạn không thể ở hai nơi cùng lúc!

Điều này vẫn có thể thực hiện được bằng cách sao chép các node parallax vào
:ref:`SubViewport<class_subviewport>` thứ hai (hoặc thứ ba hoặc thứ tư). Đây là một cấu hình cho game hai người chơi:

.. image:: img/2d_parallax_splitscreen.webp

Tất nhiên, giờ cả hai background đều hiển thị trong cả hai SubViewport. Điều chúng ta muốn là mỗi parallax chỉ hiển thị trong viewport tương ứng. Chúng ta có thể thực hiện việc này như sau:

- Giữ tất cả node parallax ở :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` mặc định là 1.
- Đặt :ref:`canvas_cull_mask<class_viewport_property_canvas_cull_mask>` của SubViewport thứ nhất chỉ sử dụng layer 1 và 2.
- Làm tương tự cho SubViewport thứ hai, nhưng sử dụng layer 1 và 3.
- Đặt các node parallax trong SubViewport thứ nhất dưới cùng một parent và đặt :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` của parent đó thành 2.
- Làm tương tự cho các node parallax của SubViewport thứ hai, nhưng sử dụng layer 3.

Cách này hoạt động thế nào? Nếu một canvas item có :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` không khớp với :ref:`canvas_cull_mask<class_viewport_property_canvas_cull_mask>` của SubViewport, nó sẽ ẩn tất cả các node con, ngay cả khi các node con đó có khớp. Chúng ta tận dụng điều này để SubViewport ngừng render các node parallax có parent không có :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` được hỗ trợ.

Xem trước trong editor
----------------------

Trước phiên bản 4.3, khuyến nghị là đặt mỗi layer vào một
:ref:`ParallaxBackground<class_parallaxbackground>` riêng, bật thuộc tính
:ref:`follow_viewport_enabled<class_canvaslayer_property_follow_viewport_enabled>`, rồi scale từng layer. Phương pháp này vốn luôn khó thiết lập cho đúng, nhưng vẫn có thể thực hiện bằng cách sử dụng một
:ref:`CanvasLayer<class_canvaslayer>` thay cho :ref:`ParallaxBackground<class_parallaxbackground>`.

.. note::
    Một khuyến nghị khác là `addon "Parallax2D Preview" của KoBeWi <https://github.com/KoBeWi/Godot-Parallax2D-Preview>`_. Addon này cung cấp một vài chế độ xem trước khác nhau và rất tiện dụng!

.. _`KoBeWi's "Parallax2D Preview" addon`: https://github.com/KoBeWi/Godot-Parallax2D-Preview
