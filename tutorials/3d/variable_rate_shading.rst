.. _doc_variable_rate_shading:

Variable rate shading
=====================

Variable rate shading là gì?
----------------------------

Trong các engine kết xuất 3D hiện đại, shader phức tạp hơn rất nhiều so với trước đây. Sự ra đời của physically-based rendering, global illumination theo thời gian thực và các hiệu ứng screen-space đã làm tăng số lượng phép shading *per-pixel* cần thực hiện để kết xuất mỗi frame. Ngoài ra, độ phân giải màn hình cũng đã tăng đáng kể, với 1440p và 4K hiện là các độ phân giải mục tiêu phổ biến. Do đó, tổng chi phí shading trong quá trình kết xuất scene thường chiếm một phần đáng kể trong thời gian cần để kết xuất mỗi frame.

Variable rate shading (VRS) là một phương pháp giảm chi phí shading này bằng cách giảm độ phân giải của phép shading *per-pixel* (còn gọi là phép shading *fragment*), đồng thời giữ nguyên độ phân giải ban đầu cho việc kết xuất hình học. Điều này có nghĩa là các cạnh hình học vẫn sắc nét như khi không sử dụng VRS. VRS có thể được kết hợp với bất kỳ
:ref:`doc_3d_antialiasing` technique (MSAA, FXAA, TAA, SSAA).

VRS cho phép chỉ định chất lượng shading theo từng khu vực, nhờ đó một số phần của viewport có thể nhận được shading chi tiết hơn các phần khác. Điều này đặc biệt hữu ích trong thực tế ảo (VR) để tạo *foveated rendering*, trong đó phần trung tâm của viewport được thể hiện chi tiết hơn các cạnh.

Dưới đây là một scene được kết xuất khi tắt rồi bật rate shading, sử dụng density map được liên kết ở cuối trang này:

.. figure:: img/variable_rate_shading_textured_disabled.webp
   :align: center
   :alt: Variable rate shading disabled in textured scene

   Variable rate shading disabled in textured scene

.. figure:: img/variable_rate_shading_textured_enabled.webp
   :align: center
   :alt: Variable rate shading enabled in textured scene (lower quality, but higher performance)

   Variable rate shading enabled in textured scene (lower quality, but higher performance)

Khi được sử dụng trong các scene có chi tiết tần số thấp (chẳng hạn như các scene có phong cách stylized/low-poly), bạn có thể đạt được mức cải thiện hiệu năng tương tự nhưng với mức suy giảm chất lượng hình ảnh thấp hơn:

.. figure:: img/variable_rate_shading_untextured_disabled.webp
   :align: center
   :alt: Variable rate shading disabled in untextured scene

   Variable rate shading disabled in untextured scene

.. figure:: img/variable_rate_shading_untextured_enabled.webp
   :align: center
   :alt: Variable rate shading enabled in untextured scene (lower quality, but higher performance)

   Variable rate shading enabled in untextured scene (lower quality, but higher performance)

Hỗ trợ phần cứng
----------------

Variable rate shading chỉ được hỗ trợ trên một số GPU cụ thể:

**Máy tính để bàn:**

- NVIDIA Turing và mới hơn (bao gồm dòng GTX 1600) - AMD RDNA2 và mới hơn (cả GPU tích hợp và GPU rời – bao gồm Steam Deck) - Intel Arc Alchemist và mới hơn **(chỉ GPU rời)**

  - Đồ họa tích hợp Intel không hỗ trợ variable rate shading.

**Mobile SoC:**

- Snapdragon 888 và mới hơn - MediaTek Dimensity 9000 và mới hơn - ARM Mali-G615 và mới hơn

Tính đến tháng 1 năm 2023, GPU của Apple và Raspberry Pi không hỗ trợ variable rate shading.

Sử dụng variable rate shading trong Godot
-----------------------------------------

.. note::

    Cả renderer Forward+ và Mobile đều hỗ trợ variable rate shading. VRS có thể được sử dụng ở cả chế độ hiển thị pancake (không phải XR) và XR.

    Renderer Compatibility **không** hỗ trợ variable rate shading. Đối với XR, bạn có thể sử dụng :ref:`foveation level <doc_openxr_settings_foveation_level>` làm phương án thay thế.

Trong Project Settings nâng cao, phần **Rendering > VRS** cung cấp các thiết lập để điều khiển variable rate shading trên root viewport:

- **Mode:** Điều khiển chế độ variable rate shading. **Disabled** tắt variable rate shading. **Texture** sử dụng texture được tạo thủ công để thiết lập mật độ shading (xem thuộc tính bên dưới). **XR** tự động tạo texture phù hợp cho foveated rendering trong thực tế ảo/thực tế tăng cường. - **Texture:** Texture dùng để điều khiển mật độ shading trên root viewport. Chỉ được sử dụng khi **Mode** là **Texture**.

Đối với các viewport tùy chỉnh, chế độ và texture VRS phải được thiết lập thủ công cho
:ref:`class_Viewport` node.

.. note::

    Trên phần cứng không được hỗ trợ, sẽ không có khác biệt về hình ảnh khi bật variable rate shading. Bạn có thể kiểm tra phần cứng có hỗ trợ variable rate shading hay không bằng cách chạy editor hoặc project với ``--verbose``
    :ref:`command line argument <doc_command_line_tutorial>`.

Tạo density map VRS
~~~~~~~~~~~~~~~~~~~

Nếu sử dụng chế độ VRS **Texture**, bạn *phải* thiết lập một texture để dùng làm density map. Nếu không, sẽ không thấy hiệu ứng nào.

Bạn có thể tự tạo density map VRS bằng trình chỉnh sửa hình ảnh hoặc tạo nó bằng một phương pháp khác (ví dụ: trên CPU bằng class Image hoặc trên GPU bằng shader). Tuy nhiên, hãy lưu ý đến ảnh hưởng hiệu năng khi tạo ảnh VRS một cách động. Nếu chọn tạo động, hãy đảm bảo quá trình tạo ảnh VRS đủ nhanh để không làm mất đi lợi ích hiệu năng do VRS mang lại.

Texture phải tuân theo các quy tắc sau:

- Texture *phải* sử dụng định dạng nén không mất dữ liệu để màu sắc có thể được đối chiếu chính xác. - Các mật độ VRS sau đây được ánh xạ với nhiều màu khác nhau, trong đó màu sáng hơn biểu thị mức độ chính xác của shading thấp hơn:

+----------------------+--------------------------------+---------------------------------+
| Density              | Color                          | Comment                         |
+======================+================================+=================================+
| 1×1 (highest detail) | ``rgb(0, 0, 0) - #000000``     |                                 |
+----------------------+--------------------------------+---------------------------------+
| 1×2                  | ``rgb(0, 85, 0) - #005500``    |                                 |
+----------------------+--------------------------------+---------------------------------+
| 2×1                  | ``rgb(85, 0, 0) - #550000``    |                                 |
+----------------------+--------------------------------+---------------------------------+
| 2×2                  | ``rgb(85, 85, 0) - #555500``   |                                 |
+----------------------+--------------------------------+---------------------------------+
| 2×4                  | ``rgb(85, 170, 0) - #55aa00``  |                                 |
+----------------------+--------------------------------+---------------------------------+
| 4×2                  | ``rgb(170, 85, 0) - #aa5500``  |                                 |
+----------------------+--------------------------------+---------------------------------+
| 4×4                  | ``rgb(170, 170, 0) - #aaaa00`` |                                 |
+----------------------+--------------------------------+---------------------------------+
| 4×8                  | ``rgb(170, 255, 0) - #aaff00`` | Not supported on most hardware. |
+----------------------+--------------------------------+---------------------------------+
| 8×4                  | ``rgb(255, 170, 0) - #ffaa00`` | Not supported on most hardware. |
+----------------------+--------------------------------+---------------------------------+
| 8×8 (lowest detail)  | ``rgb(255, 255, 0) - #ffff00`` | Not supported on most hardware. |
+----------------------+--------------------------------+---------------------------------+

Ví dụ, texture mật độ VRS này cung cấp mật độ shading cao nhất ở trung tâm viewport và mật độ shading thấp nhất ở các góc:

.. figure:: img/variable_rate_shading_texture_example.webp
   :align: center
   :alt: Example VRS density map texture, simulating foveated rendering

   Example VRS density map texture, simulating foveated rendering

Không có yêu cầu nào về kích thước hoặc tỷ lệ khung hình đối với texture mật độ VRS. Tuy nhiên, sử dụng density map VRS lớn hơn độ phân giải viewport chia cho *tile size* của GPU không mang lại lợi ích nào. Tile size là yếu tố xác định vùng pixel nhỏ nhất mà tại đó mật độ shading có thể được thay đổi độc lập với các tile khác. Trên hầu hết GPU, tile size là 8×8 pixel. Bạn có thể xem tile size bằng cách chạy Godot với đối số dòng lệnh ``--verbose``, vì giá trị này được in trong thông tin gỡ lỗi VRS.

Do đó, nên sử dụng độ phân giải tương đối thấp như 256×256 (hình vuông) hoặc 480×270 (16:9). Tùy theo trường hợp sử dụng, texture hình vuông có thể phù hợp hơn so với texture khớp với tỷ lệ khung hình viewport phổ biến nhất trong project của bạn (chẳng hạn như 16:9).

.. tip::

    Khi sử dụng variable rate shading, bạn có thể dùng một giá trị âm
    :ref:`texture mipmap LOD bias <doc_resolution_scaling_mipmap_bias>`
    để giảm độ mờ ở các khu vực có shading rate thấp hơn.

    Lưu ý rằng texture LOD bias được thiết lập trên toàn cục, vì vậy điều này cũng ảnh hưởng đến các khu vực của viewport có shading rate đầy đủ. Không sử dụng các giá trị quá thấp, nếu không texture sẽ có vẻ nhiễu hạt.

So sánh hiệu năng
~~~~~~~~~~~~~~~~~

Để hình dung VRS có thể cải thiện hiệu năng về mặt lý thuyết đến mức nào, dưới đây là phần so sánh hiệu năng với scene ví dụ có texture được hiển thị ở đầu trang này. Ví dụ VRS density map xuất hiện trên trang này được sử dụng.

Kết quả được ghi nhận trên GeForce RTX 4090 với driver NVIDIA 525.60.11.

+---------------------+--------------+-------------+-------------------------+
| Resolution          | VRS disabled | VRS enabled | Performance improvement |
+=====================+==============+=============+=========================+
| 1920×1080 (Full HD) | 2832 FPS     | 3136 FPS    | +10.7%                  |
+---------------------+--------------+-------------+-------------------------+
| 2560×1440 (QHD)     | 2008 FPS     | 2256 FPS    | +12.3%                  |
+---------------------+--------------+-------------+-------------------------+
| 3840×2160 (4K)      | 1236 FPS     | 1436 FPS    | +16.2%                  |
+---------------------+--------------+-------------+-------------------------+
| 7680×4320 (8K)      | 384 FPS      | 473 FPS     | +23.1%                  |
+---------------------+--------------+-------------+-------------------------+

Về mức cải thiện hiệu năng, variable rate shading mang lại nhiều lợi ích hơn ở các độ phân giải mục tiêu cao hơn. Sự suy giảm chất lượng hình ảnh cũng ít dễ nhận thấy hơn ở độ phân giải cao.

.. note::

    Đối với các game không dùng VR, có lẽ bạn sẽ phải sử dụng texture VRS ít mạnh tay hơn texture được dùng trong ví dụ này. Do đó, mức cải thiện hiệu năng thực tế sẽ thấp hơn.
