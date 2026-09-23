.. _doc_3d_rendering_limitations:

Các giới hạn của rendering 3D
=============================

Giới thiệu
----------

Do tập trung vào hiệu năng, các rendering engine thời gian thực có nhiều giới hạn. Renderer của Godot cũng không ngoại lệ. Để làm việc hiệu quả với những giới hạn đó, bạn cần hiểu rõ chúng.

Giới hạn kích thước texture
---------------------------

Trên máy tính để bàn và máy tính xách tay, các texture lớn hơn 8192×8192 có thể không được hỗ trợ trên những thiết bị cũ. Bạn có thể kiểm tra các giới hạn của GPU mục tiêu trên `GPUinfo.org <https://www.gpuinfo.org/>`__.

GPU di động thường bị giới hạn ở texture 4096×4096. Ngoài ra, một số GPU di động không hỗ trợ lặp các texture có kích thước không phải lũy thừa của hai. Vì vậy, nếu muốn texture hiển thị chính xác trên mọi nền tảng, bạn nên tránh sử dụng texture lớn hơn 4096×4096 và sử dụng kích thước là lũy thừa của hai nếu texture cần được lặp.

Để giới hạn kích thước của một texture cụ thể có thể quá lớn để render, bạn có thể đặt tùy chọn import **Process > Size Limit** thành một giá trị lớn hơn ``0``. Điều này sẽ giảm kích thước của texture khi import (giữ nguyên tỷ lệ khung hình) mà không ảnh hưởng đến tệp nguồn.

.. _doc_3d_rendering_limitations_color_banding:

Dải màu
-------

Khi sử dụng các phương thức rendering Forward+ hoặc Mobile, engine 3D của Godot render nội bộ ở HDR. Tuy nhiên, đầu ra rendering thường được ghi vào một buffer có độ chính xác thấp hơn. Điều này có thể gây ra các dải màu nhìn thấy được, đặc biệt khi sử dụng material không có texture. Vì lý do hiệu năng, độ chính xác màu cũng thấp hơn khi sử dụng phương thức rendering Mobile so với Forward+.

Khi sử dụng phương thức rendering Compatibility, rendering HDR nội bộ không được sử dụng và độ chính xác màu là thấp nhất trong tất cả các phương thức rendering. Điều này cũng áp dụng cho rendering 2D, trong đó các dải màu có thể nhìn thấy khi sử dụng texture gradient mượt.

Có hai cách chính để giảm dải màu:

- Nếu sử dụng các phương thức rendering Forward+ hoặc Forward Mobile, hãy bật
  :ref:`Use Debanding <class_ProjectSettings_property_rendering/anti_aliasing/quality/use_debanding>` trong **Project Settings > Rendering > Anti Aliasing**. Tùy chọn này áp dụng một shader debanding toàn màn hình dưới dạng hiệu ứng hậu kỳ và có chi phí rất thấp.
- Ngoài ra, hãy bake một ít noise vào các texture. Cách này chủ yếu hiệu quả trong 2D, chẳng hạn như với các hiệu ứng vignette. Trong 3D, bạn cũng có thể sử dụng một `custom debanding shader <https://github.com/fractilegames/godot-gles2-debanding-material>`__ để áp dụng lên *materials*. Kỹ thuật này vẫn hoạt động ngay cả khi project của bạn được render với độ chính xác màu thấp, nghĩa là nó sẽ hoạt động khi sử dụng các phương thức rendering Mobile và Compatibility.

.. figure:: img/3d_rendering_limitations_banding.webp
   :align: center
   :alt: So sánh dải màu (đã tăng độ tương phản để dễ nhìn hơn)

   So sánh dải màu (đã tăng độ tương phản để dễ nhìn hơn)

.. seealso::

    Xem `Banding in Games: A Noisy Rant (PDF) <https://loopit.dk/banding_in_games.pdf>`__ để biết thêm chi tiết về dải màu và các cách khắc phục.

Độ chính xác của depth buffer
-----------------------------

Để sắp xếp các đối tượng trong không gian 3D, các rendering engine dựa vào một *depth buffer* (còn gọi là *Z-buffer*). Buffer này có độ chính xác hữu hạn: 32-bit trên các nền tảng desktop, 24-bit trên các nền tảng di động (vì lý do hiệu năng). Nếu hai đối tượng khác nhau rơi vào cùng một giá trị trong buffer, hiện tượng Z-fighting sẽ xảy ra. Hiện tượng này biểu hiện dưới dạng các texture nhấp nháy qua lại khi camera di chuyển hoặc xoay.

Để làm depth buffer chính xác hơn trên vùng được render, bạn nên *increase* thuộc tính **Near** của node Camera. Tuy nhiên, hãy cẩn thận: nếu đặt giá trị này quá cao, người chơi sẽ có thể nhìn xuyên qua các hình học ở gần. Bạn cũng nên *decrease* thuộc tính **Far** của node Camera xuống giá trị thấp nhất cho phép trong trường hợp sử dụng của mình, nhưng hãy nhớ rằng nó sẽ không ảnh hưởng đến độ chính xác nhiều bằng thuộc tính **Near**.

Nếu chỉ cần độ chính xác cao khi người chơi có thể nhìn xa, bạn có thể thay đổi giá trị này một cách động dựa trên các điều kiện trong game. Chẳng hạn, nếu người chơi bước vào máy bay, thuộc tính **Near** có thể được tăng tạm thời để tránh Z-fighting ở khoảng cách xa. Sau đó, có thể giảm giá trị này khi người chơi rời khỏi máy bay.

Tùy thuộc vào scene và điều kiện quan sát, bạn cũng có thể di chuyển các đối tượng bị Z-fighting ra xa nhau hơn mà người chơi vẫn không nhận thấy sự khác biệt.

.. figure:: img/3d_rendering_limitations_z_fighting.webp
   :align: center
   :alt: So sánh Z-fighting (trước và sau khi tinh chỉnh scene bằng cách dịch Label3D ra xa sàn)

   So sánh Z-fighting (trước và sau khi tinh chỉnh scene bằng cách dịch Label3D ra xa sàn)

.. _doc_3d_rendering_limitations_transparency_sorting:

Sắp xếp độ trong suốt
---------------------

Trong Godot, các material trong suốt được vẽ sau các material không trong suốt. Các đối tượng trong suốt được sắp xếp từ phía sau ra phía trước trước khi vẽ, dựa trên vị trí của Node3D chứ không phải vị trí của vertex trong không gian thế giới. Vì vậy, các đối tượng chồng lấp thường có thể bị sắp xếp sai thứ tự. Để sửa các đối tượng được sắp xếp không đúng, hãy điều chỉnh
thuộc tính :ref:`Render Priority <class_Material_property_render_priority>` của material hoặc
:ref:`Sorting Offset <class_VisualInstance3D_property_sorting_offset>` của node. Render Priority sẽ buộc các material cụ thể xuất hiện phía trước hoặc phía sau các material trong suốt khác, còn Sorting Offset sẽ di chuyển đối tượng về phía trước hoặc phía sau nhằm mục đích sắp xếp. Tuy vậy, ngay cả những tùy chọn này cũng không phải lúc nào cũng đủ.

Các đối tượng trong suốt không được render vào buffer normal-roughness vì chúng được vẽ sau hình học không trong suốt. Do đó, các tính năng phụ thuộc vào buffer normal-roughness sẽ không ảnh hưởng đến các material trong suốt.

Một số rendering engine có các kỹ thuật *order-independent transparency* để giảm vấn đề này, nhưng chúng gây tốn kém cho GPU. Hiện tại Godot chưa cung cấp tính năng này. Vẫn có một số cách để tránh vấn đề này:

- Chỉ làm cho material trong suốt khi thực sự cần. Nếu material chỉ có một phần nhỏ trong suốt, hãy cân nhắc tách phần đó thành một material riêng. Điều này cho phép phần không trong suốt đổ bóng và cũng cải thiện hiệu năng.

- Nếu texture của bạn chủ yếu gồm các vùng hoàn toàn không trong suốt và hoàn toàn trong suốt, bạn có thể sử dụng alpha testing thay cho alpha blending. Chế độ trong suốt này render nhanh hơn và không gặp các vấn đề về độ trong suốt. Trong StandardMaterial3D, hãy bật **Transparency > Transparency** thành **Alpha Scissor**, và điều chỉnh **Transparency > Alpha Scissor Threshold** tương ứng nếu cần. Lưu ý rằng MSAA sẽ không khử răng cưa các cạnh của texture trừ khi alpha antialiasing được bật trong các thuộc tính của material. Tuy nhiên, FXAA, TAA và supersampling vẫn có thể khử răng cưa các cạnh của texture bất kể alpha antialiasing có được bật trên material hay không.

- Nếu cần render các vùng bán trong suốt của texture, alpha scissor không phù hợp. Thay vào đó, đôi khi có thể đặt thuộc tính **Transparency > Transparency** của StandardMaterial3D thành **Depth Pre-Pass** (đánh đổi bằng hiệu năng). Bạn cũng có thể thử chế độ **Alpha Hash**.

- Nếu muốn một material mờ dần theo khoảng cách, hãy sử dụng chế độ distance fade **Pixel Dither** hoặc **Object Dither** của StandardMaterial3D thay cho **Pixel Alpha**. Điều này sẽ làm material trở nên không trong suốt, đồng thời tăng tốc quá trình rendering.

.. figure:: img/3d_rendering_limitations_transparency_sorting.webp
   :align: center
   :alt: So sánh việc sắp xếp độ trong suốt (vật liệu alpha-blended ở bên trái, vật liệu alpha scissor ở bên phải)

   So sánh việc sắp xếp độ trong suốt (vật liệu alpha-blended ở bên trái, vật liệu alpha scissor ở bên phải)
