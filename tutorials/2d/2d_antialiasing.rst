.. _doc_2d_antialiasing:

Khử răng cưa 2D
===============

.. Images on this page were generated using the project below
.. (except for `antialiasing_none_scaled.webp`):
.. https://github.com/Calinou/godot-antialiasing-comparison

.. seealso::

    Godot cũng hỗ trợ khử răng cưa trong kết xuất 3D. Nội dung này được trình bày trên
    :ref:`doc_3d_antialiasing` trang.

Giới thiệu
----------

Do có độ phân giải hạn chế, các cảnh được kết xuất trong 2D có thể xuất hiện hiện tượng răng cưa. Những hiện tượng này thường biểu hiện dưới dạng hiệu ứng "bậc thang" trên các cạnh hình học và dễ nhận thấy nhất khi sử dụng các node như :ref:`class_Line2D`,
:ref:`class_Polygon2D` hoặc :ref:`class_TextureProgressBar`. :ref:`doc_custom_drawing_in_2d` cũng có thể xuất hiện hiện tượng răng cưa đối với các phương thức không hỗ trợ khử răng cưa.

Trong ví dụ bên dưới, bạn có thể nhận thấy các cạnh có vẻ ngoài dạng khối:

.. figure:: img/antialiasing_none_scaled.webp
   :alt: Hình ảnh được phóng to 2× bằng bộ lọc điểm gần nhất để làm hiện tượng răng cưa dễ nhận thấy hơn.
   :align: center

   Hình ảnh được phóng to 2× bằng bộ lọc điểm gần nhất để làm hiện tượng răng cưa dễ nhận thấy hơn.

Để khắc phục vấn đề này, Godot hỗ trợ một số phương pháp bật khử răng cưa khi kết xuất 2D.

Thuộc tính khử răng cưa trong Line2D và chế độ vẽ tùy chỉnh
-----------------------------------------------------------

Đây là phương pháp được khuyến nghị vì trong hầu hết trường hợp, nó ảnh hưởng ít hơn đến hiệu năng.

Line2D có thuộc tính **Antialiased** mà bạn có thể bật trong inspector. Ngoài ra, một số phương thức của :ref:`doc_custom_drawing_in_2d` hỗ trợ tham số ``antialiased`` tùy chọn, có thể được đặt thành ``true`` khi gọi hàm.

Các phương thức này không yêu cầu bật MSAA, nên chi phí hiệu năng *baseline* của chúng thấp. Nói cách khác, sẽ không có chi phí phát sinh cố định nếu tại một thời điểm nào đó bạn không vẽ hình học có khử răng cưa.

Nhược điểm của các phương thức khử răng cưa này là chúng hoạt động bằng cách tạo thêm hình học. Nếu bạn tạo hình học 2D phức tạp được cập nhật mỗi khung hình, đây có thể là một điểm nghẽn. Ngoài ra, Polygon2D, TextureProgressBar và một số phương thức vẽ tùy chỉnh không có thuộc tính khử răng cưa. Đối với các node này, bạn có thể sử dụng khử răng cưa đa mẫu 2D thay thế.

Khử răng cưa đa mẫu (MSAA)
--------------------------

*Tính năng này chỉ khả dụng trong các renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Trước khi bật MSAA trong 2D, điều quan trọng là phải hiểu MSAA sẽ tác động lên những gì. MSAA trong 2D có các hạn chế tương tự như trong 3D. Mặc dù không gây ra hiện tượng mờ, phạm vi áp dụng của nó bị giới hạn. Các ứng dụng chính của MSAA 2D là:

- Các cạnh hình học, chẳng hạn như khi vẽ đường và đa giác.
- Các cạnh sprite *chỉ đối với các pixel chạm vào một trong các cạnh của texture*. Điều này hoạt động với cả bộ lọc tuyến tính và bộ lọc điểm gần nhất. Các cạnh sprite được tạo bằng độ trong suốt trên hình ảnh không bị MSAA tác động.

Nhược điểm của MSAA là nó chỉ hoạt động trên các cạnh. Điều này là do MSAA làm tăng số lượng mẫu *coverage*, nhưng không làm tăng số lượng mẫu *color*. Tuy nhiên, vì số lượng mẫu màu không tăng, các fragment shader vẫn chỉ được chạy một lần cho mỗi pixel. Do đó, MSAA sẽ **not affect** các loại răng cưa sau theo bất kỳ cách nào:

- Răng cưa *within* các texture được lọc bằng bộ lọc điểm gần nhất (pixel art).
- Răng cưa do các shader 2D tùy chỉnh gây ra.
- Răng cưa đặc trưng khi sử dụng Light2D.
- Răng cưa trong quá trình kết xuất font.

Có thể bật MSAA trong Project Settings bằng cách thay đổi giá trị của thiết lập
:ref:`Rendering > Anti Aliasing > Quality > MSAA 2D <class_ProjectSettings_property_rendering/anti_aliasing/quality/msaa_2d>`. Điều quan trọng là thay đổi giá trị của thiết lập **MSAA 2D** chứ không phải **MSAA 3D**, vì đây là hai thiết lập hoàn toàn riêng biệt.

So sánh giữa không khử răng cưa (bên trái) và các mức MSAA khác nhau (bên phải). Góc trên bên trái chứa một node Line2D, góc trên bên phải chứa 2 node TextureProgressBar. Phần dưới chứa 8 sprite pixel art, trong đó 4 sprite chạm vào các cạnh (nền màu xanh lá) và 4 sprite không chạm vào các cạnh (logo Godot):

.. image:: img/antialiasing_msaa_2x.webp

.. image:: img/antialiasing_msaa_4x.webp

.. image:: img/antialiasing_msaa_8x.webp
