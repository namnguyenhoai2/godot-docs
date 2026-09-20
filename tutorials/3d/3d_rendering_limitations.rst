.. _doc_3d_rendering_limitations:

Các hạn chế của việc render 3D
==============================

Giới thiệu
----------

Do tập trung vào hiệu năng, các rendering engine thời gian thực có nhiều hạn chế. Renderer của Godot cũng không ngoại lệ. Để làm việc hiệu quả với những hạn chế này, bạn cần hiểu rõ chúng.

Giới hạn kích thước texture
---------------------------

Trên máy tính để bàn và laptop, các texture lớn hơn 8192×8192 có thể không được hỗ trợ trên những thiết bị cũ. Bạn có thể kiểm tra các hạn chế của GPU mục tiêu trên `GPUinfo.org <https://www.gpuinfo.org/>`__.

GPU di động thường bị giới hạn ở texture 4096×4096. Ngoài ra, một số GPU di động không hỗ trợ lặp các texture có kích thước không phải lũy thừa của hai. Do đó, nếu muốn texture hiển thị chính xác trên mọi nền tảng, bạn nên tránh sử dụng texture lớn hơn 4096×4096 và sử dụng kích thước là lũy thừa của hai nếu texture cần được lặp.

Để giới hạn kích thước của một texture cụ thể có thể quá lớn để render, bạn có thể đặt tùy chọn import **Process > Size Limit** thành một giá trị lớn hơn ``0``. Thao tác này sẽ giảm kích thước của texture khi import (giữ nguyên tỷ lệ khung hình) mà không ảnh hưởng đến tệp nguồn.

.. _doc_3d_rendering_limitations_color_banding:

Hiện tượng banding màu
----------------------

Khi sử dụng phương thức rendering Forward+ hoặc Mobile, engine 3D của Godot render nội bộ ở HDR. Tuy nhiên, đầu ra rendering thường được ghi vào một buffer có độ chính xác thấp hơn. Điều này có thể gây ra hiện tượng banding thấy rõ, đặc biệt khi sử dụng các material không có texture. Vì lý do hiệu năng, độ chính xác màu cũng thấp hơn khi sử dụng phương thức rendering Mobile so với Forward+.

Khi sử dụng phương thức rendering Compatibility, rendering HDR nội bộ không được sử dụng và độ chính xác màu là thấp nhất trong tất cả các phương thức rendering. Điều này cũng áp dụng cho rendering 2D, trong đó hiện tượng banding có thể nhìn thấy khi sử dụng các texture gradient mượt.

Có hai cách chính để giảm hiện tượng banding:

- Nếu sử dụng phương thức rendering Forward+ hoặc Forward Mobile, hãy bật
  :ref:`Use Debanding<class_ProjectSettings_property_rendering/anti_aliasing/quality/use_debanding>`
  trong **Project Settings > Rendering > Anti Aliasing**. Thao tác này áp dụng một debanding shader toàn màn hình dưới dạng hiệu ứng post-processing và có chi phí rất thấp. - Ngoài ra, hãy bake một ít noise vào texture. Cách này chủ yếu hiệu quả trong 2D, chẳng hạn như đối với các hiệu ứng vignette. Trong 3D, bạn cũng có thể sử dụng `custom debanding shader <https://github.com/fractilegames/godot-gles2-debanding-material>`__ để áp dụng lên *material*. Kỹ thuật này vẫn hoạt động ngay cả khi project được render với độ chính xác màu thấp, nghĩa là nó sẽ hoạt động khi sử dụng phương thức rendering Mobile và Compatibility.

.. figure:: img/3d_rendering_limitations_banding.webp
   :align: center
   :alt: Color banding comparison (contrast increased for more visibility)

   Color banding comparison (contrast increased for more visibility)

.. seealso::

    Xem `Banding in Games: A Noisy Rant (PDF) <https://loopit.dk/banding_in_games.pdf>`__ để biết thêm chi tiết về banding và các cách khắc phục.

Độ chính xác của depth buffer
-----------------------------

Để sắp xếp các object trong không gian 3D, các rendering engine dựa vào một *depth buffer* (còn gọi là *Z-buffer*). Buffer này có độ chính xác hữu hạn: 32-bit trên các nền tảng desktop và 24-bit trên các nền tảng di động (vì lý do hiệu năng). Nếu hai object khác nhau có cùng giá trị trong buffer, hiện tượng Z-fighting sẽ xảy ra. Hiện tượng này biểu hiện dưới dạng các texture nhấp nháy qua lại khi camera di chuyển hoặc xoay.

Để làm cho depth buffer chính xác hơn trên vùng được render, bạn nên *tăng* thuộc tính **Near** của node Camera. Tuy nhiên, hãy cẩn thận: nếu đặt giá trị quá cao, người chơi sẽ có thể nhìn xuyên qua hình học ở gần. Bạn cũng nên *giảm* thuộc tính **Far** của Camera xuống giá trị thấp nhất cho phép đối với trường hợp sử dụng của mình, nhưng cần lưu ý rằng thuộc tính này không ảnh hưởng đến độ chính xác nhiều bằng thuộc tính **Near**.

Nếu chỉ cần độ chính xác cao khi người chơi có thể nhìn thấy khoảng cách xa, bạn có thể thay đổi giá trị này động dựa trên điều kiện trong game. Ví dụ, nếu người chơi bước vào một chiếc máy bay, thuộc tính **Near** có thể được tạm thời tăng lên để tránh Z-fighting ở khoảng cách xa. Sau đó, thuộc tính này có thể được giảm xuống khi người chơi rời khỏi máy bay.

Tùy thuộc vào scene và điều kiện quan sát, bạn cũng có thể di chuyển các object bị Z-fighting ra xa nhau hơn mà không khiến người chơi nhận thấy sự khác biệt.

.. figure:: img/3d_rendering_limitations_z_fighting.webp
   :align: center
   :alt: Z-fighting comparison (before and after tweaking the scene by offsetting the Label3D away from the floor)

   Z-fighting comparison (before and after tweaking the scene by offsetting the Label3D away from the floor)

.. _doc_3d_rendering_limitations_transparency_sorting:

Sắp xếp độ trong suốt
---------------------

Trong Godot, các material trong suốt được vẽ sau các material không trong suốt. Các object trong suốt được sắp xếp từ sau ra trước trước khi được vẽ, dựa trên vị trí của Node3D chứ không phải vị trí của vertex trong không gian world. Vì vậy, các object chồng lấp thường có thể bị sắp xếp sai thứ tự. Để sửa các object được sắp xếp không đúng, hãy điều chỉnh
:ref:`Render Priority <class_Material_property_render_priority>`
của material hoặc
:ref:`Sorting Offset <class_VisualInstance3D_property_sorting_offset>`.
Render Priority sẽ buộc các material cụ thể xuất hiện phía trước hoặc phía sau các material trong suốt khác, trong khi Sorting Offset sẽ di chuyển object về phía trước hoặc phía sau nhằm mục đích sắp xếp. Tuy vậy, những tùy chọn này không phải lúc nào cũng đủ.

Các object trong suốt không được render vào normal-roughness buffer, vì chúng được vẽ sau hình học không trong suốt. Do đó, các tính năng dựa vào normal-roughness buffer sẽ không ảnh hưởng đến các material trong suốt.

Một số rendering engine có các kỹ thuật *order-independent transparency* để giảm vấn đề này, nhưng chúng tiêu tốn nhiều tài nguyên GPU. Hiện tại Godot không cung cấp tính năng này. Vẫn có một số cách để tránh vấn đề này:

- Chỉ làm cho material trong suốt khi bạn thực sự cần. Nếu một material chỉ có một phần nhỏ trong suốt, hãy cân nhắc tách phần đó thành một material riêng. Điều này cho phép phần không trong suốt đổ bóng và cũng cải thiện hiệu năng.

- Nếu texture của bạn chủ yếu có các vùng hoàn toàn không trong suốt và hoàn toàn trong suốt, bạn có thể sử dụng alpha testing thay cho alpha blending. Chế độ trong suốt này render nhanh hơn và không gặp các vấn đề về độ trong suốt. Trong StandardMaterial3D, hãy bật **Transparency > Transparency** thành **Alpha Scissor**, và điều chỉnh **Transparency > Alpha Scissor Threshold** cho phù hợp nếu cần. Lưu ý rằng MSAA sẽ không khử răng cưa các cạnh của texture trừ khi alpha antialiasing được bật trong các thuộc tính của material. Tuy nhiên, FXAA, TAA và supersampling vẫn có thể khử răng cưa các cạnh của texture bất kể alpha antialiasing có được bật trên material hay không.

- Nếu cần render các vùng bán trong suốt của texture, alpha scissor không phù hợp. Thay vào đó, đôi khi việc đặt thuộc tính **Transparency > Transparency** của StandardMaterial3D thành **Depth Pre-Pass** có thể hoạt động (đổi lại là chi phí hiệu năng). Bạn cũng có thể thử chế độ **Alpha Hash**.

- Nếu muốn material mờ dần theo khoảng cách, hãy sử dụng chế độ distance fade **Pixel Dither** hoặc **Object Dither** của StandardMaterial3D thay cho **Pixel Alpha**. Điều này sẽ làm material trở nên không trong suốt, đồng thời tăng tốc độ rendering.

.. figure:: img/3d_rendering_limitations_transparency_sorting.webp
   :align: center
   :alt: Transparency sorting comparison (alpha-blended materials on the left, alpha scissor materials on the right)

   Transparency sorting comparison (alpha-blended materials on the left, alpha scissor materials on the right)
