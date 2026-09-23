.. _doc_variable_rate_shading:

Shading với tốc độ thay đổi
===========================

Shading với tốc độ thay đổi là gì?
----------------------------------

Trong các engine kết xuất 3D hiện đại, shader phức tạp hơn nhiều so với trước đây. Sự xuất hiện của kết xuất dựa trên cơ sở vật lý, global illumination theo thời gian thực và các hiệu ứng trong không gian màn hình đã làm tăng số lượng shading *trên mỗi pixel* cần thực hiện để kết xuất từng khung hình. Ngoài ra, độ phân giải màn hình cũng đã tăng đáng kể, trong đó 1440p và 4K hiện là các độ phân giải mục tiêu phổ biến. Do đó, tổng chi phí shading khi kết xuất cảnh thường chiếm một phần đáng kể trong thời gian cần thiết để kết xuất mỗi khung hình.

Shading với tốc độ thay đổi (VRS) là một phương pháp giảm chi phí shading này bằng cách giảm độ phân giải của shading *trên mỗi pixel* (còn gọi là shading *fragment*), đồng thời giữ nguyên độ phân giải khi kết xuất hình học. Điều này có nghĩa là các cạnh hình học vẫn sắc nét như khi không sử dụng VRS. VRS có thể kết hợp với bất kỳ
:ref:`doc_3d_antialiasing` kỹ thuật nào (MSAA, FXAA, TAA, SSAA).

VRS cho phép chỉ định chất lượng shading theo từng khu vực, nhờ đó một số phần của viewport có thể nhận được shading chi tiết hơn các phần khác. Điều này đặc biệt hữu ích trong thực tế ảo (VR) để đạt được *kết xuất tập trung điểm nhìn*, trong đó trung tâm viewport có nhiều chi tiết hơn các cạnh.

Đây là một cảnh được kết xuất khi tắt rồi bật shading với tốc độ thay đổi, sử dụng density map được liên kết ở cuối trang này:

.. figure:: img/variable_rate_shading_textured_disabled.webp
   :align: center
   :alt: Shading với tốc độ thay đổi bị tắt trong cảnh có texture

   Shading với tốc độ thay đổi bị tắt trong cảnh có texture

.. figure:: img/variable_rate_shading_textured_enabled.webp
   :align: center
   :alt: Shading với tốc độ thay đổi được bật trong cảnh có texture (chất lượng thấp hơn nhưng hiệu năng cao hơn)

   Shading với tốc độ thay đổi được bật trong cảnh có texture (chất lượng thấp hơn nhưng hiệu năng cao hơn)

Khi sử dụng trong các cảnh có chi tiết tần số thấp (chẳng hạn như cảnh có phong cách cách điệu/low-poly), bạn có thể đạt được mức tăng hiệu năng tương tự nhưng giảm chất lượng hình ảnh ít hơn:

.. figure:: img/variable_rate_shading_untextured_disabled.webp
   :align: center
   :alt: Shading với tốc độ thay đổi bị tắt trong cảnh không có texture

   Shading với tốc độ thay đổi bị tắt trong cảnh không có texture

.. figure:: img/variable_rate_shading_untextured_enabled.webp
   :align: center
   :alt: Shading với tốc độ thay đổi được bật trong cảnh không có texture (chất lượng thấp hơn nhưng hiệu năng cao hơn)

   Shading với tốc độ thay đổi được bật trong cảnh không có texture (chất lượng thấp hơn nhưng hiệu năng cao hơn)

Hỗ trợ phần cứng
----------------

Shading với tốc độ thay đổi chỉ được hỗ trợ trên một số GPU nhất định:

**Desktop:**

- NVIDIA Turing và mới hơn (bao gồm dòng GTX 1600)
- AMD RDNA2 và mới hơn (cả GPU tích hợp lẫn GPU rời – bao gồm Steam Deck)
- Intel Arc Alchemist và mới hơn **(chỉ GPU rời)**

  - Đồ họa tích hợp Intel không hỗ trợ shading với tốc độ thay đổi.

**Mobile SoCs:**

- Snapdragon 888 và mới hơn
- MediaTek Dimensity 9000 và mới hơn
- ARM Mali-G615 và mới hơn

Tính đến tháng 1 năm 2023, GPU Apple và Raspberry Pi không hỗ trợ shading với tốc độ thay đổi.

Sử dụng shading với tốc độ thay đổi trong Godot
-----------------------------------------------

.. note::

    Cả renderer Forward+ và Mobile đều hỗ trợ shading với tốc độ thay đổi. VRS có thể được sử dụng trong cả chế độ hiển thị pancake (không phải XR) và XR.

    Renderer Compatibility **không** hỗ trợ shading với tốc độ thay đổi. Với XR, bạn có thể sử dụng :ref:`foveation level <doc_openxr_settings_foveation_level>` làm phương án thay thế.

Trong phần Project Settings nâng cao, mục **Rendering > VRS** cung cấp các thiết lập để điều khiển shading với tốc độ thay đổi trên viewport gốc:

- **Mode:** Điều khiển chế độ shading với tốc độ thay đổi. **Disabled** tắt shading với tốc độ thay đổi. **Texture** sử dụng texture được tạo thủ công để thiết lập mật độ shading (xem thuộc tính bên dưới). **XR** tự động tạo texture phù hợp cho kết xuất tập trung điểm nhìn trong thực tế ảo/thực tế tăng cường.
- **Texture:** Texture dùng để điều khiển mật độ shading trên viewport gốc. Chỉ được sử dụng nếu **Mode** là **Texture**.

Đối với các viewport tùy chỉnh, phải thiết lập thủ công chế độ và texture VRS cho
:ref:`class_Viewport` node.

.. note::

    Trên phần cứng không được hỗ trợ, việc bật shading với tốc độ thay đổi sẽ không tạo ra khác biệt về hình ảnh. Bạn có thể kiểm tra phần cứng có hỗ trợ shading với tốc độ thay đổi hay không bằng cách chạy editor hoặc project với ``--verbose``
    :ref:`đối số dòng lệnh <doc_command_line_tutorial>`.

Tạo density map VRS
~~~~~~~~~~~~~~~~~~~

Nếu sử dụng chế độ VRS **Texture**, bạn *phải* thiết lập một texture để dùng làm density map. Nếu không, sẽ không thấy hiệu ứng nào.

Bạn có thể tự tạo density map VRS thủ công bằng trình chỉnh sửa ảnh hoặc tạo nó bằng một phương pháp khác (ví dụ: trên CPU bằng lớp Image hoặc trên GPU bằng shader). Tuy nhiên, hãy lưu ý đến ảnh hưởng về hiệu năng khi tạo ảnh VRS động. Nếu chọn cách tạo động, hãy đảm bảo quá trình tạo ảnh VRS đủ nhanh để mức tăng hiệu năng từ VRS không bị triệt tiêu.

Texture phải tuân theo các quy tắc sau:

- Texture *phải* sử dụng định dạng nén không mất dữ liệu để các màu có thể được đối chiếu chính xác.
- Các mật độ VRS sau đây được ánh xạ với nhiều màu khác nhau, trong đó màu sáng hơn biểu thị mức độ chính xác của shading thấp hơn:

+-----------------------------+--------------------------------+-------------------------------------------+
| Mật độ                      | Màu                            | Chú thích                                 |
+=============================+================================+===========================================+
| 1×1 (chi tiết cao nhất)     | ``rgb(0, 0, 0) - #000000``     |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 1×2                         | ``rgb(0, 85, 0) - #005500``    |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 2×1                         | ``rgb(85, 0, 0) - #550000``    |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 2×2                         | ``rgb(85, 85, 0) - #555500``   |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 2×4                         | ``rgb(85, 170, 0) - #55aa00``  |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 4×2                         | ``rgb(170, 85, 0) - #aa5500``  |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 4×4                         | ``rgb(170, 170, 0) - #aaaa00`` |                                           |
+-----------------------------+--------------------------------+-------------------------------------------+
| 4×8                         | ``rgb(170, 255, 0) - #aaff00`` | Không được hầu hết phần cứng hỗ trợ.      |
+-----------------------------+--------------------------------+-------------------------------------------+
| 8×4                         | ``rgb(255, 170, 0) - #ffaa00`` | Không được hỗ trợ trên hầu hết phần cứng. |
+-----------------------------+--------------------------------+-------------------------------------------+
| 8×8 (độ chi tiết thấp nhất) | ``rgb(255, 255, 0) - #ffff00`` | Không được hỗ trợ trên hầu hết phần cứng. |
+-----------------------------+--------------------------------+-------------------------------------------+

Ví dụ: texture mật độ VRS này cung cấp mật độ shading cao nhất ở giữa viewport và mật độ shading thấp nhất ở các góc:

.. figure:: img/variable_rate_shading_texture_example.webp
   :align: center
   :alt: Texture bản đồ mật độ VRS mẫu, mô phỏng foveated rendering

   Texture bản đồ mật độ VRS mẫu, mô phỏng foveated rendering

Texture mật độ VRS không có yêu cầu nào về kích thước hoặc tỷ lệ khung hình. Tuy nhiên, việc sử dụng bản đồ mật độ VRS lớn hơn độ phân giải viewport chia cho *kích thước tile* của GPU không mang lại lợi ích. Kích thước tile là yếu tố quyết định vùng pixel nhỏ nhất mà mật độ shading có thể được thay đổi riêng biệt với các tile khác. Trên hầu hết GPU, kích thước tile này là 8×8 pixel. Bạn có thể xem kích thước tile bằng cách chạy Godot với đối số dòng lệnh ``--verbose``, vì kích thước này được in trong thông tin gỡ lỗi VRS.

Do đó, bạn nên sử dụng độ phân giải tương đối thấp như 256×256 (hình vuông) hoặc 480×270 (16:9). Tùy vào trường hợp sử dụng, texture hình vuông có thể phù hợp hơn texture khớp với tỷ lệ khung hình viewport phổ biến nhất trong dự án của bạn (chẳng hạn như 16:9).

.. tip::

    Khi sử dụng variable rate shading, bạn có thể sử dụng một
    :ref:`độ lệch LOD mipmap âm của texture <doc_resolution_scaling_mipmap_bias>` để giảm độ mờ ở các vùng có shading rate thấp hơn.

    Lưu ý rằng độ lệch LOD của texture được đặt trên toàn cục, vì vậy điều này cũng ảnh hưởng đến các vùng viewport có shading rate đầy đủ. Không sử dụng giá trị quá thấp, nếu không texture sẽ bị nhiễu hạt.

So sánh hiệu năng
~~~~~~~~~~~~~~~~~

Để hình dung VRS có thể cải thiện hiệu năng về mặt lý thuyết đến mức nào, dưới đây là so sánh hiệu năng với scene mẫu có texture được hiển thị ở đầu trang này. Ví dụ về bản đồ mật độ VRS trên trang này được sử dụng.

Kết quả được ghi nhận trên GeForce RTX 4090 với driver NVIDIA 525.60.11.

+---------------------+----------+----------+-------------------------+
| Độ phân giải        | Tắt VRS  | Bật VRS  | Mức cải thiện hiệu năng |
+=====================+==========+==========+=========================+
| 1920×1080 (Full HD) | 2832 FPS | 3136 FPS | +10.7%                  |
+---------------------+----------+----------+-------------------------+
| 2560×1440 (QHD)     | 2008 FPS | 2256 FPS | +12.3%                  |
+---------------------+----------+----------+-------------------------+
| 3840×2160 (4K)      | 1236 FPS | 1436 FPS | +16.2%                  |
+---------------------+----------+----------+-------------------------+
| 7680×4320 (8K)      | 384 FPS  | 473 FPS  | +23.1%                  |
+---------------------+----------+----------+-------------------------+

Xét về mức cải thiện hiệu năng, variable rate shading mang lại nhiều lợi ích hơn ở các độ phân giải mục tiêu cao hơn. Sự suy giảm chất lượng hình ảnh cũng khó nhận thấy hơn ở độ phân giải cao.

.. note::

    Đối với các game không dùng VR, có lẽ bạn sẽ phải sử dụng texture VRS ít mạnh hơn so với texture được dùng trong ví dụ này. Do đó, mức tăng hiệu năng thực tế sẽ thấp hơn.
