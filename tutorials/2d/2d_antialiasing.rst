.. _doc_2d_antialiasing:

Khử răng cưa 2D
===============

.. Hình ảnh trên trang này được tạo bằng dự án bên dưới .. (ngoại trừ `antialiasing_none_scaled.webp`): .. https://github.com/Calinou/godot-antialiasing-comparison

.. seealso::

    Godot cũng hỗ trợ khử răng cưa trong kết xuất 3D. Nội dung này được trình bày trên
    :ref:`doc_3d_antialiasing` page.

Giới thiệu
----------

Do có độ phân giải hạn chế, các cảnh được kết xuất trong 2D có thể xuất hiện các hiện tượng răng cưa. Những hiện tượng này thường biểu hiện dưới dạng hiệu ứng "bậc thang" trên các cạnh hình học và dễ nhận thấy nhất khi sử dụng các node như :ref:`class_Line2D`,
:ref:`class_Polygon2D` or :ref:`class_TextureProgressBar`. :ref:`doc_custom_drawing_in_2d`
cũng có thể xuất hiện hiện tượng răng cưa đối với những phương thức không hỗ trợ khử răng cưa.

Trong ví dụ dưới đây, bạn có thể nhận thấy các cạnh có vẻ ngoài dạng khối:

.. figure:: img/antialiasing_none_scaled.webp
   :alt: Image is scaled by 2× with nearest-neighbor filtering to make aliasing more noticeable.
   :align: center

   Image is scaled by 2× with nearest-neighbor filtering to make aliasing more noticeable.

Để khắc phục điều này, Godot hỗ trợ một số phương pháp bật khử răng cưa khi kết xuất 2D.

Thuộc tính khử răng cưa trong Line2D và tính năng vẽ tùy chỉnh
--------------------------------------------------------------

Đây là phương pháp được khuyến nghị vì trong hầu hết trường hợp, tác động đến hiệu suất thấp hơn.

Line2D có thuộc tính **Antialiased** mà bạn có thể bật trong trình kiểm tra. Ngoài ra, một số phương thức cho :ref:`doc_custom_drawing_in_2d` hỗ trợ tham số ``antialiased`` tùy chọn, có thể đặt thành ``true`` khi gọi hàm.

Các phương thức này không yêu cầu bật MSAA, nhờ đó chi phí hiệu suất *cơ bản* thấp. Nói cách khác, sẽ không có chi phí phát sinh cố định nếu tại một thời điểm nào đó bạn không vẽ hình học được khử răng cưa.

Nhược điểm của các phương pháp khử răng cưa này là chúng hoạt động bằng cách tạo thêm hình học. Nếu bạn tạo hình học 2D phức tạp và cập nhật hình học đó trong mỗi khung hình, đây có thể trở thành điểm nghẽn. Ngoài ra, Polygon2D, TextureProgressBar và một số phương thức vẽ tùy chỉnh không có thuộc tính khử răng cưa. Đối với các node này, thay vào đó bạn có thể sử dụng khử răng cưa đa mẫu 2D.

Khử răng cưa đa mẫu (MSAA)
--------------------------

*Tính năng này chỉ khả dụng trong các trình kết xuất Forward+ và Mobile, không khả dụng trong trình kết xuất Compatibility.*

Trước khi bật MSAA trong 2D, điều quan trọng là phải hiểu MSAA sẽ tác động lên những gì. MSAA trong 2D có các giới hạn tương tự như trong 3D. Mặc dù không gây ra hiện tượng mờ, phạm vi áp dụng của nó bị giới hạn. Các ứng dụng chính của MSAA 2D là:

- Các cạnh hình học, chẳng hạn như khi vẽ đường và đa giác. - Các cạnh sprite *chỉ đối với những pixel chạm vào một trong các cạnh của texture*. Điều này hoạt động với cả bộ lọc tuyến tính và bộ lọc láng giềng gần nhất. Các cạnh sprite được tạo bằng độ trong suốt trên hình ảnh không bị MSAA ảnh hưởng.

Nhược điểm của MSAA là nó chỉ hoạt động trên các cạnh. Điều này là do MSAA tăng số lượng mẫu *coverage*, nhưng không tăng số lượng mẫu *color*. Tuy nhiên, vì số lượng mẫu màu không tăng nên các trình đổ bóng phân mảnh vẫn chỉ được chạy một lần cho mỗi pixel. Do đó, MSAA sẽ **không ảnh hưởng** đến các loại răng cưa sau đây theo bất kỳ cách nào:

- Răng cưa *bên trong* các texture được lọc bằng bộ lọc láng giềng gần nhất (pixel art). - Răng cưa do shader 2D tùy chỉnh gây ra. - Răng cưa phản chiếu khi sử dụng Light2D. - Răng cưa trong quá trình kết xuất phông chữ.

Có thể bật MSAA trong Project Settings bằng cách thay đổi giá trị của
:ref:`Rendering > Anti Aliasing > Quality > MSAA 2D<class_ProjectSettings_property_rendering/anti_aliasing/quality/msaa_2d>`
cài đặt. Điều quan trọng là phải thay đổi giá trị của cài đặt **MSAA 2D**, không phải **MSAA 3D**, vì đây là hai cài đặt hoàn toàn riêng biệt.

So sánh giữa không khử răng cưa (bên trái) và các mức MSAA khác nhau (bên phải). Góc trên bên trái chứa một node Line2D, góc trên bên phải chứa 2 node TextureProgressBar. Phần dưới chứa 8 sprite pixel art, trong đó 4 sprite chạm vào các cạnh (nền màu xanh lá) và 4 sprite không chạm vào các cạnh (logo Godot):

.. image:: img/antialiasing_msaa_2x.webp

.. image:: img/antialiasing_msaa_4x.webp

.. image:: img/antialiasing_msaa_8x.webp
