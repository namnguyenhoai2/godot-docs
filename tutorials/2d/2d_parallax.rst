.. _doc_2d_parallax:

Parallax 2D
===========

Giới thiệu
----------

Parallax là một hiệu ứng được dùng để mô phỏng chiều sâu bằng cách cho các texture chuyển động ở những tốc độ khác nhau so với camera. Godot cung cấp node :ref:`Parallax2D<class_parallax2d>` để tạo hiệu ứng này. Tuy nhiên, hiệu ứng này vẫn có thể dễ gây nhầm lẫn, vì vậy trang này cung cấp mô tả chuyên sâu về một số thuộc tính và cách khắc phục một số lỗi thường gặp.

.. note::

    Trang này trình bày cách sử dụng :ref:`Parallax2D<class_parallax2d>`, được khuyến nghị dùng thay cho :ref:`ParallaxLayer<class_parallaxlayer>` và
    :ref:`ParallaxBackground<class_parallaxbackground>` nodes.

Bắt đầu
-------

Node parallax hỗ trợ thêm các node kết xuất nội dung làm node con, vì vậy bạn có thể sử dụng một hoặc nhiều node để tạo thành mỗi lớp. Để bắt đầu, hãy đặt từng node hoặc các node bạn muốn cuộn độc lập làm node con của một parallax node riêng. Đảm bảo góc trên bên trái của các texture được sử dụng nằm tại giao điểm ``(0, 0)``, như trong hình bên dưới. Xem phần :ref:`positioning <doc_2d_parallax_positioning>` để biết tại sao điều này lại quan trọng.

.. image:: img/2d_parallax_size_viewport.webp

Cảnh bên trên sử dụng một texture đã chuẩn bị cho các đám mây ở xa hơn trong một :ref:`Sprite2D <class_sprite2d>`, nhưng bạn cũng có thể dễ dàng sử dụng nhiều node được bố trí cách nhau để tạo thành lớp này.

Tỷ lệ cuộn
----------

Nền tảng của hiệu ứng parallax là thuộc tính :ref:`scroll_scale <class_parallax2d_property_scroll_scale>`. Thuộc tính này hoạt động như một hệ số nhân tốc độ cuộn, cho phép các lớp di chuyển với tốc độ khác camera trên từng trục được thiết lập. Giá trị 1 khiến parallax node cuộn với cùng tốc độ như camera. Nếu muốn hình ảnh trông xa hơn khi cuộn, hãy dùng giá trị nhỏ hơn 1; giá trị 0 sẽ khiến hình ảnh dừng hoàn toàn. Nếu muốn một vật thể trông gần camera hơn, hãy dùng giá trị lớn hơn 1, khiến nó cuộn nhanh hơn.

Cảnh bên trên gồm năm lớp. Một số giá trị :ref:`scroll_scale <class_parallax2d_property_scroll_scale>` phù hợp có thể là:

- ``(0.7, 1)`` - Rừng - ``(0.5, 1)`` - Đồi - ``(0.3, 1)`` - Mây thấp - ``(0.2, 1)`` - Mây cao - ``(0.1, 1)`` - Bầu trời

Video bên dưới minh họa cách các giá trị này ảnh hưởng đến việc cuộn trong game:

.. video:: video/2d_parallax_scroll_scale.webm
   :alt: A scene with five layers scrolling at different speeds
   :autoplay:
   :loop:
   :muted:
   :align: default

Lặp vô hạn
----------

:ref:`Parallax2D<class_parallax2d>` provides a bonus effect that gives textures the illusion of repeating infinitely.
:ref:`repeat_size<class_parallax2d_property_repeat_size>` tells the node to snap its position forward or back when the
camera cuộn theo giá trị đã thiết lập. Hiệu ứng này đạt được bằng cách thêm một bản lặp duy nhất cho tất cả canvas item con, được dịch chuyển theo giá trị đó. Khi camera cuộn giữa hình ảnh và bản lặp của nó, hình ảnh sẽ vô hình chuyển về vị trí ban đầu, tạo cảm giác hình ảnh lặp vô tận.

.. image:: img/2d_parallax_scroll.gif

Vì đây là một hiệu ứng khá nhạy, người dùng chưa quen rất dễ mắc lỗi khi thiết lập. Hãy cùng xem xét "cách thức" và "lý do" của một số vấn đề phổ biến mà người dùng thường gặp.

Kích thước không phù hợp
~~~~~~~~~~~~~~~~~~~~~~~~

Hiệu ứng lặp vô hạn dễ xử lý nhất khi bạn có một hình ảnh được thiết kế để lặp liền mạch và có kích thước bằng hoặc lớn hơn viewport **trước khi** thiết lập :ref:`repeat_size<class_parallax2d_property_repeat_size>`. Nếu không thể tìm được asset được thiết kế cho tác vụ này, bạn vẫn có thể thực hiện một số việc khác để chuẩn bị hình ảnh tốt hơn về mặt kích thước.

Dưới đây là một ví dụ về texture quá nhỏ so với viewport:

.. image:: img/2d_parallax_size_bad.webp

Ta có thể thấy kích thước viewport là 500x300, nhưng texture có kích thước 288x208. Nếu ta thiết lập
:ref:`repeat_size<class_parallax2d_property_repeat_size>` to the size of our image, the infinite repeat effect doesn't
cuộn đúng cách vì texture ban đầu không bao phủ viewport. Nếu ta thiết lập
:ref:`repeat_size<class_parallax2d_property_repeat_size>` to the size of the viewport, we have a large gap. What can we
thì sao?

Thu nhỏ viewport
^^^^^^^^^^^^^^^^

Cách đơn giản nhất là đặt viewport có kích thước bằng hoặc nhỏ hơn texture. Trong **Project Settings > Display > Window**, hãy thay đổi
:ref:`Viewport Width<class_ProjectSettings_property_display/window/size/viewport_width>`
và các thiết lập :ref:`Viewport Height<class_ProjectSettings_property_display/window/size/viewport_height>` để khớp với nền của bạn.

.. image:: img/2d_parallax_size_viewport.webp

Thu phóng Parallax2D
^^^^^^^^^^^^^^^^^^^^

Nếu bạn không hướng đến phong cách chính xác đến từng pixel hoặc không ngại hình ảnh hơi mờ, bạn có thể chọn phóng to texture để vừa với màn hình. Hãy thiết lập :ref:`scale<class_node2d_property_scale>` của :ref:`Parallax2D<class_parallax2d>`, và tất cả texture con sẽ được phóng to theo.

Thu phóng các node con
^^^^^^^^^^^^^^^^^^^^^^

Tương tự như việc thu phóng :ref:`Parallax2D<class_parallax2d>`, bạn có thể thu phóng các node :ref:`Sprite2D<class_sprite2d>` để chúng đủ lớn nhằm bao phủ màn hình. Hãy lưu ý rằng một số thiết lập như
:ref:`Parallax2D.repeat_size<class_parallax2d_property_repeat_size>` and
:ref:`Sprite2D.region_rect<class_sprite2d_property_region_rect>` do not take scaling into account, so it's necessary to
hãy điều chỉnh các giá trị này dựa trên tỷ lệ.

.. image:: img/2d_parallax_size_scale.webp

Lặp các texture
^^^^^^^^^^^^^^^

Bạn cũng có thể chuẩn bị các node con từ sớm để có một khởi đầu thuận lợi. Nếu bạn có một
:ref:`Sprite2D<class_sprite2d>` you'd like to repeat, but is too small, you can do the following to repeat it:

- đặt :ref:`texture_repeat<class_canvasitem_property_texture_repeat>` thành :ref:`CanvasItem.TEXTURE_REPEAT_ENABLED<class_canvasitem_constant_TEXTURE_REPEAT_ENABLED>` - đặt :ref:`region_enabled<class_sprite2d_property_region_enabled>` thành ``true`` - đặt :ref:`region_rect<class_sprite2d_property_region_rect>` thành bội số của kích thước texture, đủ lớn để bao phủ viewport.

Bên dưới, bạn có thể thấy việc lặp hình ảnh hai lần khiến nó đủ lớn để bao phủ màn hình.

.. image:: img/2d_parallax_size_repeat.webp

.. _doc_2d_parallax_positioning:

Vị trí không phù hợp
~~~~~~~~~~~~~~~~~~~~

Người dùng thường vô tình đặt tất cả texture của mình căn giữa tại giao điểm ``(0,0)``:

.. image:: img/2d_parallax_single_centered.webp

Điều này gây ra vấn đề với hiệu ứng lặp vô hạn và nên tránh. "Canvas lặp vô hạn" bắt đầu tại ``(0,0)`` và mở rộng xuống dưới, sang phải theo kích thước của giá trị :ref:`repeat_size<class_parallax2d_property_repeat_size>`.

.. image:: img/2d_parallax_single_expand.webp

Nếu các texture được căn giữa tại giao điểm ``(0,0)``, canvas lặp vô hạn chỉ được phủ một phần, nên nó cũng chỉ lặp một phần.

Tăng ``repeat_times`` có khắc phục được vấn đề này không?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Về mặt kỹ thuật, việc tăng :ref:`repeat_times<class_parallax2d_property_repeat_times>` *có thể* hiệu quả trong một số trường hợp, nhưng đây là giải pháp dùng vũ lực và không giải quyết đúng vấn đề mà thuộc tính này được thiết kế để xử lý (chúng ta sẽ tìm hiểu thêm về điều này sau). Cách khắc phục tốt hơn là hiểu cách hiệu ứng lặp hoạt động và thiết lập các texture parallax phù hợp ngay từ đầu.

Trước tiên, hãy kiểm tra xem có texture nào tràn sang các phần âm của canvas hay không. Đảm bảo các texture được sử dụng trong parallax node nằm gọn bên trong "canvas lặp vô hạn" bắt đầu tại ``(0,0)``. Như vậy, nếu
:ref:`Parallax2D.repeat_size<class_parallax2d_property_repeat_size>` is set correctly, it should look something like
điều này, với một vòng lặp duy nhất của hình ảnh có kích thước bằng hoặc lớn hơn viewport:

.. image:: img/2d_parallax_repeat_good_norect.webp

Hãy hình dung cách hình ảnh cuộn ngang qua màn hình: ban đầu nó hiển thị phần nằm trong hình chữ nhật màu đỏ (được xác định bởi :ref:`repeat_size<class_parallax2d_property_repeat_size>`), và khi đến phần nằm trong hình chữ nhật màu vàng, nó nhanh chóng đưa hình ảnh về phía trước để tạo ảo giác cuộn vô tận.

.. image:: img/2d_parallax_repeat_good.webp

Nếu bạn đặt hình ảnh lệch khỏi "canvas lặp vô hạn", khi camera đến hình chữ nhật màu vàng, một nửa hình ảnh sẽ bị cắt trước khi nó nhảy về phía trước như trong hình bên dưới:

.. image:: img/2d_parallax_repeat_bad.webp

Độ lệch cuộn
------------

Nếu các texture parallax của bạn đã hoạt động chính xác, nhưng bạn muốn chúng bắt đầu từ một vị trí khác,
:ref:`Parallax2D<class_parallax2d>` comes with a :ref:`scroll_offset<class_parallax2d_property_scroll_offset>` property
được dùng để dịch chuyển vị trí bắt đầu của canvas lặp vô hạn. Ví dụ, nếu hình ảnh của bạn có kích thước 288x208, đặt :ref:`scroll_offset<class_parallax2d_property_scroll_offset>` thành ``(-144,0)`` hoặc ``(144,0)`` cho phép hình ảnh bắt đầu từ giữa ảnh.

Số lần lặp
----------

Lý tưởng nhất là sau khi làm theo hướng dẫn này, các texture parallax của bạn đủ lớn để bao phủ màn hình ngay cả khi thu nhỏ. Cho đến lúc này, ta có một texture 288x208 vừa khít bên trong viewport 288x208. Tuy nhiên, vấn đề xảy ra khi ta thu nhỏ bằng cách đặt :ref:`Camera2D.zoom<class_camera2d_property_zoom>` thành ``(0.5, 0.5)``:

.. image:: img/2d_parallax_zoom_single.webp

Mặc dù mọi thứ được thiết lập chính xác cho viewport ở mức thu phóng mặc định, việc thu nhỏ khiến texture nhỏ hơn viewport, làm hỏng hiệu ứng lặp vô hạn. Đây là lúc
:ref:`repeat_times<class_parallax2d_property_repeat_times>` can help out. Setting a value of ``3`` (one extra
lặp phía sau và phía trước), giờ đây nó đủ lớn để đáp ứng hiệu ứng lặp vô hạn.

.. image:: img/2d_parallax_zoom_repeat_times.webp

Nếu các texture này được dùng để lặp theo chiều dọc, ta sẽ chỉ định giá trị ``y`` cho
:ref:`repeat_size<class_parallax2d_property_repeat_size>`. The
:ref:`repeat_times<class_parallax2d_property_repeat_times>` would automatically add a repeat above and below as well.
Đây chỉ là parallax theo chiều ngang, nên một khoảng trống sẽ xuất hiện phía trên và bên dưới hình ảnh. Làm thế nào để giải quyết vấn đề này? Ta cần sáng tạo! Trong ví dụ này, ta kéo giãn bầu trời lên cao hơn và sprite cỏ xuống thấp hơn. Các texture giờ đây hỗ trợ mức thu phóng bình thường và mức thu phóng xuống còn một nửa kích thước.

.. image:: img/2d_parallax_zoom_repeat_adjusted.webp

Màn hình chia đôi
-----------------

Hầu hết hướng dẫn tạo game màn hình chia đôi trong Godot bắt đầu bằng việc viết một script nhỏ để gán :ref:`Viewport.world_2d<class_viewport_property_world_2d>` của SubViewport thứ nhất cho SubViewport thứ hai, để chúng dùng chung nội dung hiển thị. Người dùng thường đặt câu hỏi về cách chia sẻ hiệu ứng parallax giữa cả hai màn hình.

Hiệu ứng parallax giả lập phối cảnh bằng cách di chuyển vị trí của các texture khác nhau theo mối quan hệ với camera. Điều này hiển nhiên gây vấn đề nếu bạn có nhiều camera, vì texture không thể ở hai nơi cùng lúc!

Điều này vẫn có thể thực hiện bằng cách sao chép các parallax node vào SubViewport thứ hai (hoặc thứ ba, thứ tư)
:ref:`SubViewport<class_subviewport>`. Here's how a setup looks for a two player game:

.. image:: img/2d_parallax_splitscreen.webp

Tất nhiên, lúc này cả hai nền đều hiển thị trong cả hai SubViewport. Điều ta muốn là mỗi parallax chỉ hiển thị trong viewport tương ứng của nó. Ta có thể thực hiện như sau:

- Giữ tất cả parallax node ở giá trị :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` mặc định là 1. - Đặt :ref:`canvas_cull_mask<class_viewport_property_canvas_cull_mask>` của SubViewport thứ nhất chỉ bao gồm các layer 1 và 2. - Làm tương tự cho SubViewport thứ hai nhưng sử dụng các layer 1 và 3. - Cho các parallax node trong SubViewport thứ nhất một node cha chung và đặt :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` của nó thành 2. - Làm tương tự cho các parallax node trong SubViewport thứ hai, nhưng sử dụng layer 3.

Cách này hoạt động như thế nào? Nếu một canvas item có :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` không khớp với :ref:`canvas_cull_mask<class_viewport_property_canvas_cull_mask>` của SubViewport, nó sẽ ẩn tất cả node con, ngay cả khi các node con đó khớp. Ta tận dụng điều này để cho phép các SubViewport ngừng kết xuất những parallax node có node cha không chứa :ref:`visibility_layer<class_canvasitem_property_visibility_layer>` được hỗ trợ.

Xem trước trong trình chỉnh sửa
-------------------------------

Trước phiên bản 4.3, khuyến nghị là đặt mỗi layer vào một
:ref:`ParallaxBackground<class_parallaxbackground>`, enable the
:ref:`follow_viewport_enabled<class_canvaslayer_property_follow_viewport_enabled>` property, and scale the individual
layer riêng. Phương pháp này vốn luôn khó thiết lập chính xác, nhưng vẫn có thể thực hiện bằng cách sử dụng một
:ref:`CanvasLayer<class_canvaslayer>` instead of a :ref:`ParallaxBackground<class_parallaxbackground>`.

.. note::
    Một khuyến nghị khác là `KoBeWi's "Parallax2D Preview" addon <https://github.com/KoBeWi/Godot-Parallax2D-Preview>`_. Addon này cung cấp một số chế độ xem trước khác nhau và rất tiện dụng!
