.. _doc_3d_antialiasing:

Khử răng cưa 3D
===============

.. Hình ảnh trên trang này được tạo bằng project bên dưới .. (ngoại trừ `antialiasing_none_scaled.webp`): .. https://github.com/Calinou/godot-antialiasing-comparison

.. seealso::

    Godot cũng hỗ trợ khử răng cưa trong kết xuất 2D. Nội dung này được trình bày trong
    :ref:`doc_2d_antialiasing` page.

Giới thiệu
----------

Do có độ phân giải hạn chế, các scene được kết xuất trong 3D có thể xuất hiện các hiện tượng aliasing. Những hiện tượng này thường biểu hiện dưới dạng hiệu ứng "bậc thang" trên các cạnh bề mặt (edge aliasing), cùng hiện tượng nhấp nháy và/hoặc lấp lánh trên các bề mặt phản chiếu (specular aliasing).

Trong ví dụ bên dưới, bạn có thể nhận thấy các cạnh có vẻ ngoài dạng khối. Thảm thực vật cũng nhấp nháy rồi biến mất, còn các đường mảnh trên nóc hộp gần như biến mất:

.. figure:: img/antialiasing_none_scaled.webp
   :alt: Image is scaled by 2× with nearest-neighbor filtering to make aliasing more noticeable.
   :align: center

   Image is scaled by 2× with nearest-neighbor filtering to make aliasing more noticeable.

Để khắc phục điều này, Godot cung cấp nhiều kỹ thuật khử răng cưa khác nhau. Các kỹ thuật này được trình bày chi tiết bên dưới.

.. seealso::

    Bạn có thể so sánh hoạt động của các thuật toán khử răng cưa bằng `3D Antialiasing demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/antialiasing>`__.

Khử răng cưa đa mẫu (MSAA)
--------------------------

*Tính năng này có trong tất cả renderer.*

Đây là cách "truyền thống" để xử lý aliasing. MSAA rất hiệu quả với các cạnh hình học (đặc biệt ở các mức cao hơn). MSAA hoàn toàn không làm hình ảnh bị mờ.

MSAA có 3 mức: 2×, 4×, 8×. Các mức cao hơn khử răng cưa trên cạnh hiệu quả hơn, nhưng đòi hỏi nhiều tài nguyên hơn đáng kể. Trong các game có hình ảnh hiện đại, bạn nên dùng 2× hoặc 4× MSAA, vì 8× MSAA thường đòi hỏi quá nhiều tài nguyên.

Nhược điểm của MSAA là nó chỉ hoạt động trên các cạnh. Đó là vì MSAA tăng số lượng mẫu *coverage*, nhưng không tăng số lượng mẫu *color*. Tuy nhiên, vì số lượng mẫu màu không tăng, các fragment shader vẫn chỉ chạy một lần cho mỗi pixel. Do đó, MSAA không giảm được aliasing trong suốt đối với các material sử dụng chế độ trong suốt **Alpha Scissor** (độ trong suốt 1-bit). MSAA cũng không hiệu quả với specular aliasing.

Để giảm aliasing trên các material alpha scissor,
:ref:`alpha antialiasing <doc_standard_material_3d_alpha_antialiasing>`
(còn gọi là *alpha to coverage*) có thể được bật trên các material cụ thể trong các thuộc tính của StandardMaterial3D hoặc ORMMaterial3D. Alpha to coverage có chi phí hiệu năng vừa phải, nhưng hiệu quả trong việc giảm aliasing trên các material trong suốt mà không làm hình ảnh bị mờ.

Để làm cho specular aliasing khó nhận thấy hơn, hãy sử dụng `Bộ giới hạn roughness trong không gian màn hình`_, tính năng được bật theo mặc định.

Có thể bật MSAA trong Project Settings bằng cách thay đổi giá trị của
:ref:`Rendering > Anti Aliasing > Quality > MSAA 3D<class_ProjectSettings_property_rendering/anti_aliasing/quality/msaa_3d>`
setting. Điều quan trọng là phải thay đổi giá trị của setting **MSAA 3D**, không phải **MSAA 2D**, vì đây là hai setting hoàn toàn riêng biệt.

So sánh giữa không khử răng cưa (bên trái) và các mức MSAA khác nhau (bên phải). Lưu ý rằng khử răng cưa alpha không được sử dụng ở đây:

.. image:: img/antialiasing_msaa_2x.webp

.. image:: img/antialiasing_msaa_4x.webp

.. image:: img/antialiasing_msaa_8x.webp

.. _doc_3d_antialiasing_taa:

Khử răng cưa theo thời gian (TAA)
---------------------------------

*Tính năng này chỉ có trong Forward+ renderer, không có trong Mobile hoặc Compatibility renderer.*

Khử răng cưa theo thời gian hoạt động bằng cách *hội tụ* kết quả của các frame đã kết xuất trước đó thành một frame duy nhất có chất lượng cao. Đây là một quá trình liên tục, trong đó vị trí của tất cả vertex trong scene được làm jitter ở mỗi frame. Việc làm jitter này nhằm thu nhận chi tiết dưới pixel và thường không thể nhận thấy, ngoại trừ trong những trường hợp cực đoan.

Kỹ thuật này thường được sử dụng trong các game hiện đại, vì nó cung cấp hình thức khử răng cưa hiệu quả nhất đối với specular aliasing và các hiện tượng khác do shader gây ra. TAA cũng hỗ trợ đầy đủ khử răng cưa trong suốt.

TAA tạo ra một lượng mờ nhỏ khi được bật trong các scene tĩnh, nhưng hiệu ứng mờ này sẽ rõ hơn khi camera di chuyển. Một nhược điểm khác của TAA là nó có thể tạo ra các hiện tượng *ghosting* phía sau những vật thể đang chuyển động. Kết xuất ở framerate cao hơn sẽ giúp TAA hội tụ nhanh hơn, từ đó làm các hiện tượng ghosting này ít thấy hơn.

Có thể bật khử răng cưa theo thời gian trong Project Settings bằng cách thay đổi giá trị của
:ref:`Rendering > Anti Aliasing > Quality > TAA<class_ProjectSettings_property_rendering/anti_aliasing/quality/use_taa>`
setting.

So sánh giữa không khử răng cưa (bên trái) và TAA (bên phải):

.. image:: img/antialiasing_taa.webp

.. _doc_3d_antialiasing_fsr2:

AMD FidelityFX Super Resolution 2.2 (FSR2)
------------------------------------------

*Tính năng này chỉ có trong Forward+ renderer, không có trong Mobile hoặc Compatibility renderer.*

Kể từ Godot 4.2, Godot đã tích hợp sẵn hỗ trợ cho `AMD FidelityFX Super Resolution <https://www.amd.com/en/products/graphics/technologies/fidelityfx/super-resolution.html>`__ 2.2. Đây là một :ref:`upscaling method <doc_resolution_scaling>` tương thích với tất cả GPU gần đây của mọi nhà sản xuất. FSR2 thường được thiết kế để cải thiện hiệu năng bằng cách giảm độ phân giải kết xuất 3D nội bộ, sau đó upscale lên độ phân giải đầu ra.

Tuy nhiên, không giống FSR1, FSR2 cũng cung cấp khử răng cưa theo thời gian. Điều này có nghĩa là FSR2 có thể được sử dụng ở độ phân giải gốc để khử răng cưa chất lượng cao, với độ phân giải đầu vào bằng độ phân giải đầu ra. Trong trường hợp này, việc bật FSR2 thực tế sẽ *làm giảm* hiệu năng, nhưng sẽ cải thiện đáng kể chất lượng kết xuất.

Sử dụng FSR2 ở độ phân giải gốc đòi hỏi nhiều tài nguyên hơn so với sử dụng TAA ở độ phân giải gốc, vì vậy chỉ nên dùng khi GPU của bạn còn nhiều headroom. Mặt tích cực là FSR2 cung cấp khả năng khử răng cưa tốt hơn và ít làm mờ hơn so với TAA, đặc biệt khi chuyển động.

So sánh giữa không khử răng cưa (bên trái) và FSR2 ở độ phân giải gốc (bên phải):

.. image:: img/antialiasing_fsr2_native.webp

..  note::

    Theo mặc định, project setting **FSR Sharpness** được đặt thành ``0.2`` (giá trị cao hơn sẽ cho kết quả sharpening ít hơn). Để so sánh, sharpening của FSR đã được tắt bằng cách đặt thành ``2.0`` trong ảnh chụp màn hình bên trên.

.. _doc_3d_antialiasing_fxaa:

Khử răng cưa xấp xỉ nhanh (FXAA)
--------------------------------

*Tính năng này chỉ có trong Forward+ và Mobile renderer, không có trong Compatibility renderer.*

Khử răng cưa xấp xỉ nhanh là một giải pháp khử răng cưa hậu kỳ. Nó chạy nhanh hơn bất kỳ kỹ thuật khử răng cưa nào khác và cũng hỗ trợ khử răng cưa trong suốt. Tuy nhiên, vì không có thông tin theo thời gian, nó không xử lý được nhiều specular aliasing.

Kỹ thuật này đôi khi vẫn được sử dụng trong các game mobile. Tuy nhiên, trên các nền tảng desktop, FXAA nhìn chung đã không còn phổ biến và được thay thế bằng khử răng cưa theo thời gian, vốn hiệu quả hơn nhiều đối với specular aliasing. Dù vậy, việc cung cấp FXAA như một tùy chọn trong game vẫn có thể hữu ích cho những người chơi sử dụng GPU cấp thấp.

FXAA tạo ra một lượng mờ vừa phải khi được bật (nhiều hơn TAA trong cảnh tĩnh, nhưng ít hơn TAA khi camera di chuyển).

Có thể bật FXAA trong Project Settings bằng cách thay đổi giá trị của
:ref:`Rendering > Anti Aliasing > Quality > Screen Space AA<class_ProjectSettings_property_rendering/anti_aliasing/quality/screen_space_aa>`
setting thành ``FXAA``.

So sánh giữa không khử răng cưa (bên trái) và FXAA (bên phải):

.. image:: img/antialiasing_fxaa.webp

Khử răng cưa hình thái dưới pixel (SMAA 1x)
-------------------------------------------

*Tính năng này chỉ có trong Forward+ và Mobile renderer, không có trong Compatibility renderer.*

Khử răng cưa hình thái dưới pixel là một giải pháp khử răng cưa hậu kỳ. Nó chạy chậm hơn FXAA một chút, nhưng tạo ra ít hiện tượng mờ hơn. Điều này rất hữu ích khi độ phân giải màn hình là 1080p hoặc thấp hơn. Giống như FXAA, SMAA 1x không có thông tin theo thời gian và do đó không xử lý được nhiều specular aliasing.

Hãy sử dụng SMAA 1x nếu bạn không đủ khả năng dùng MSAA nhưng thấy FXAA quá mờ.

Kết hợp nó với TAA, hoặc thậm chí FSR2, để tối đa hóa khả năng khử răng cưa với chi phí GPU cao hơn và một phần độ mờ bổ sung. Điều này có lợi nhất trong các scene chuyển động nhanh hoặc ngay sau khi cắt camera, đặc biệt ở FPS thấp.

Có thể bật SMAA 1x trong Project Settings bằng cách thay đổi giá trị của
:ref:`Rendering > Anti Aliasing > Quality > Screen Space AA<class_ProjectSettings_property_rendering/anti_aliasing/quality/screen_space_aa>`
setting thành ``SMAA``.

So sánh giữa không khử răng cưa (bên trái) và SMAA 1x (bên phải):

.. image:: img/antialiasing_smaa.webp

Khử răng cưa bằng lấy mẫu siêu cấp (SSAA)
-----------------------------------------

*Tính năng này có trong tất cả renderer.*

Supersampling cung cấp chất lượng khử răng cưa cao nhất có thể, nhưng cũng đắt nhất. Nó hoạt động bằng cách shading mỗi pixel trong scene nhiều lần. Nhờ đó, SSAA có thể đồng thời khử răng cưa cho cạnh, độ trong suốt *và* specular aliasing mà không tạo ra các hiện tượng ghosting tiềm ẩn.

Nhược điểm của SSAA là chi phí *cực kỳ* cao. Chi phí này thường khiến SSAA khó sử dụng cho game, nhưng supersampling vẫn có thể hữu ích cho :ref:`offline rendering <doc_creating_movies>`.

Khử răng cưa bằng lấy mẫu siêu cấp được thực hiện bằng cách tăng
:ref:`Rendering > Scaling 3D > Scale<class_ProjectSettings_property_rendering/scaling_3d/scale>`
advanced project setting lên trên ``1.0`` đồng thời đảm bảo
:ref:`Rendering > Scaling 3D > Mode<class_ProjectSettings_property_rendering/scaling_3d/mode>`
được đặt thành ``Bilinear`` (mặc định). Vì hệ số scale được xác định theo từng trục, hệ số scale ``1.5`` sẽ tạo ra SSAA 2.25×, còn hệ số scale ``2.0`` sẽ tạo ra SSAA 4×. Vì Godot sử dụng bilinear filtering của phần cứng để thực hiện downsampling, kết quả sẽ sắc nét hơn ở các hệ số scale là số nguyên (cụ thể là ``2.0``).

So sánh giữa không khử răng cưa (bên trái) và các mức SSAA khác nhau (bên phải):

.. image:: img/antialiasing_ssaa_2.25x.webp

.. image:: img/antialiasing_ssaa_4x.webp

.. warning::

    Supersampling cũng đòi hỏi nhiều video RAM, vì nó cần kết xuất ở độ phân giải đích rồi *downscale* xuống kích thước cửa sổ. Ví dụ, hiển thị một project ở 3840×2160 (độ phân giải 4K) với SSAA 4× sẽ yêu cầu kết xuất scene ở 7680×4320 (độ phân giải 8K), tức là có số pixel gấp 4 lần.

    Nếu bạn đang sử dụng kích thước cửa sổ lớn như 4K, việc tăng resolution scale vượt quá một giá trị nhất định có thể gây chậm nghiêm trọng (hoặc thậm chí crash) do hết VRAM.

Bộ giới hạn roughness trong không gian màn hình
-----------------------------------------------

*Tính năng này chỉ khả dụng trong các renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Đây không phải là một phương pháp khử răng cưa cạnh, mà là một cách giảm hiện tượng răng cưa specular trong 3D.

Bộ giới hạn roughness trong không gian màn hình hoạt động tốt nhất trên hình học có nhiều chi tiết. Mặc dù nó có tác động đến bản thân việc render roughness map, ảnh hưởng của nó trong trường hợp này khá hạn chế.

Bộ giới hạn roughness trong không gian màn hình được bật theo mặc định; không cần thiết lập thủ công. Nó ảnh hưởng một chút đến hiệu năng, vì vậy hãy cân nhắc tắt nó nếu dự án của bạn không bị ảnh hưởng nhiều bởi hiện tượng răng cưa specular. Bạn có thể tắt tính năng này bằng thiết lập dự án **Rendering > Quality > Screen Space Filters > Screen Space Roughness Limiter**.

Bộ giới hạn roughness của texture khi import
--------------------------------------------

Tương tự bộ giới hạn roughness trong không gian màn hình, đây không phải là một phương pháp khử răng cưa cạnh, mà là một cách giảm hiện tượng răng cưa specular trong 3D.

Việc giới hạn roughness khi import hoạt động bằng cách chỉ định một normal map để dùng làm hướng dẫn giới hạn roughness. Để thực hiện việc này, hãy chọn roughness map trong dock FileSystem, sau đó chuyển đến dock Import và đặt **Roughness > Mode** thành kênh màu mà roughness map được lưu trong đó (thường là **Green**), rồi đặt đường dẫn đến normal map của material. Hãy nhớ nhấp vào **Reimport** ở cuối dock Import sau khi đặt đường dẫn đến normal map.

Vì quá trình xử lý này hoàn toàn diễn ra khi import, nó không gây ra bất kỳ chi phí hiệu năng nào. Tuy nhiên, tác động về mặt hình ảnh của nó khá hạn chế. Việc giới hạn roughness khi import chỉ giúp giảm hiện tượng răng cưa specular bên trong texture, không giúp giảm hiện tượng răng cưa xảy ra trên các cạnh hình học của những mesh có nhiều chi tiết.

Tôi nên sử dụng kỹ thuật khử răng cưa nào?
------------------------------------------

**Không có kỹ thuật khử răng cưa nào phù hợp với mọi trường hợp.** Vì khử răng cưa thường đòi hỏi nhiều tài nguyên GPU hoặc có thể gây ra hiện tượng mờ không mong muốn, bạn nên thêm một thiết lập cho phép người chơi tắt khử răng cưa.

Đối với các dự án có định hướng nghệ thuật photorealistic, TAA nhìn chung là lựa chọn phù hợp nhất. Mặc dù TAA có thể tạo ra các lỗi ghosting, không có kỹ thuật nào khác xử lý hiện tượng răng cưa specular tốt như TAA. Bộ giới hạn roughness trong không gian màn hình có thể hỗ trợ đôi chút, nhưng nhìn chung kém hiệu quả hơn nhiều trong việc chống răng cưa specular. Nếu còn dư năng lực GPU, bạn có thể sử dụng FSR2 ở độ phân giải gốc để có hình thức khử răng cưa temporal đẹp hơn so với TAA tiêu chuẩn.

Đối với các dự án có ít bề mặt phản chiếu (chẳng hạn như artstyle cartoon), MSAA có thể hoạt động tốt. MSAA cũng là một lựa chọn phù hợp nếu việc tránh hiện tượng mờ và các lỗi temporal là quan trọng, chẳng hạn trong các game cạnh tranh.

Khi nhắm đến các nền tảng cấp thấp như thiết bị mobile hoặc đồ họa tích hợp, FXAA thường là lựa chọn khả thi duy nhất. 2× MSAA có thể sử dụng được trong một số trường hợp, nhưng các mức MSAA cao hơn khó có thể chạy mượt trên GPU mobile.

Godot cho phép sử dụng đồng thời nhiều kỹ thuật khử răng cưa. Điều này thường không cần thiết, nhưng có thể mang lại hình ảnh đẹp hơn trên các GPU cao cấp hoặc cho
:ref:`non-real-time rendering <doc_creating_movies>`. For example, to make
các cạnh chuyển động trông đẹp hơn khi bật TAA, bạn cũng có thể bật MSAA đồng thời.

So sánh khử răng cưa
~~~~~~~~~~~~~~~~~~~~

.. Lưu ý rằng bảng này sử dụng emoji, vốn không có chiều rộng cố định trong hầu hết các trình soạn thảo. .. Bảng trông có vẻ bị sai định dạng nhưng thực ra không phải vậy. Khi thực hiện thay đổi, hãy xem các .. dòng lân cận để biết hướng dẫn.

+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Feature                  | MSAA                     | TAA                      | FSR2                     | FXAA                     | SMAA 1x                  | SSAA                     | SSRL                     |
+==========================+==========================+==========================+==========================+==========================+==========================+==========================+==========================+
| Edge antialiasing        | 🟢 Yes                   | 🟢 Yes                   | 🟢 Yes                   | 🟢 Yes                   |  🟢 Yes                  | 🟢 Yes                   | 🔴 No                    |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Specular antialiasing    | 🟡 Some                  | 🟢 Yes                   | 🟢 Yes                   | 🟡 Some                  |  🟡 Some                 | 🟢 Yes                   | 🟢 Yes                   |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Transparency antialiasing| 🟡 Some [1]_             | 🟢 Yes [2]_              | 🟢 Yes [2]_              | 🟢 Yes                   |  🟢 Yes                  | 🟢 Yes                   | 🔴 No                    |
|                          |                          |                          |                          |                          |                          |                          |                          |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Added blur               | 🟢 None                  | 🟡 Some                  | 🟡 Some                  | 🟡 Some                  |  🟢 Low                  | 🟡 Some [3]_             | 🟢 None                  |
|                          |                          |                          |                          |                          |                          |                          |                          |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Ghosting artifacts       | 🟢 None                  | 🔴 Yes                   | 🔴 Yes                   | 🟢 None                  |  🟢 None                 | 🟢 None                  | 🟢 None                  |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Performance cost         | 🟡 Medium                | 🟡 Medium                | 🔴 High                  | 🟢 Very Low              |  🟢 Low                  | 🔴 Very High             | 🟢 Low                   |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Forward+                 | ✔️ Yes                   | ✔️ Yes                   | ✔️ Yes                   | ✔️ Yes                   |  ✔️ Yes                  | ✔️ Yes                   | ✔️ Yes                   |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Mobile                   | ✔️ Yes                   | ❌ No                    | ❌ No                    | ✔️ Yes                   |  ✔️ Yes                  | ✔️ Yes                   | ✔️ Yes                   |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+
| Compatibility            | ✔️ Yes                   | ❌ No                    | ❌ No                    | ❌ No                    |  ❌ No                   | ✔️ Yes                   | ❌ No                    |
+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+--------------------------+


.. [1] MSAA không hoạt động tốt với các material có Alpha Scissor (độ trong suốt 1 bit). Có thể khắc phục điều này bằng cách bật ``alpha antialiasing`` trên material.
.. [2] Khử răng cưa độ trong suốt bằng TAA/FSR2 đạt hiệu quả cao nhất khi sử dụng Alpha Scissor.
.. [3] SSAA có một chút hiện tượng mờ do downscaling song tuyến tính. Có thể khắc phục điều này bằng cách sử dụng hệ số scaling nguyên là ``2.0``.
