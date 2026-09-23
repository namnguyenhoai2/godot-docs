.. _doc_importing_images:

Nhập hình ảnh
=============

Các định dạng hình ảnh được hỗ trợ
----------------------------------

Godot có thể nhập các định dạng hình ảnh sau:

**Raster:**

- BMP (``.bmp``) - Hỗ trợ tất cả các định dạng pixel, nhưng không hỗ trợ nén :abbr:`RLE (Run-Length Encoding)`.

- DirectDraw Surface (``.dds``) - Nếu texture có mipmap, chúng sẽ được tải trực tiếp. Có thể sử dụng tính năng này để tạo hiệu ứng bằng mipmap tùy chỉnh.

- Khronos Texture (``.ktx``) - Việc giải mã được thực hiện bằng `libktx <https://github.com/KhronosGroup/KTX-Software>`__. Chỉ hỗ trợ hình ảnh 2D. Không hỗ trợ cubemap, mảng texture và bỏ padding.

- OpenEXR (``.exr``) - Hỗ trợ HDR (rất được khuyến nghị cho bầu trời panorama).

- Radiance HDR (``.hdr``) - Hỗ trợ HDR (rất được khuyến nghị cho bầu trời panorama).

- JPEG (``.jpg``, ``.jpeg``) - Không hỗ trợ độ trong suốt do giới hạn của định dạng.

- PNG (``.png``) - Độ chính xác bị giới hạn ở 8 bit trên mỗi kênh khi nhập (không hỗ trợ hình ảnh HDR).

- Truevision Targa (``.tga``)

- WebP (``.webp``) - Tệp WebP hỗ trợ độ trong suốt và có thể được nén có tổn hao hoặc không tổn hao. Độ chính xác bị giới hạn ở 8 bit trên mỗi kênh.

**Vector:**

- SVG (``.svg``)

  - Theo mặc định, SVG được rasterize tại thời điểm nhập.

  - SVG là định dạng hình ảnh duy nhất có thể được nhập dưới dạng DPITexture, cho phép rasterize tại runtime để khớp với hệ số oversampling hiện tại. Xem :ref:`doc_importing_images_changing_import_type` để biết chi tiết.

  - Godot sử dụng thư viện `ThorVG <https://www.thorvg.org/>`__ để render SVG. `Tính năng hỗ trợ SVG bị giới hạn <https://www.thorvg.org/about#:~:text=certain%20features%20remain%20unsupported%20within%20the%20current%20framework>`__; các vector phức tạp có thể không được render chính xác. :ref:`Văn bản phải được chuyển đổi thành path <doc_importing_images_svg_text>`; nếu không, văn bản sẽ không xuất hiện trong hình ảnh đã rasterize. Đối với các vector phức tạp, thường nên render chúng thành PNG bằng `Inkscape <https://inkscape.org/>`__. Bạn có thể tự động hóa việc này nhờ `giao diện dòng lệnh <https://wiki.inkscape.org/wiki/index.php/Using_the_Command_Line#Export_files>`__ của Inkscape.

  - Bạn có thể kiểm tra xem ThorVG có thể render chính xác một vector cụ thể hay không bằng `trình xem trên web <https://www.thorvg.org/viewer>`__ của thư viện.

.. note::

    Nếu bạn đã biên dịch trình chỉnh sửa Godot từ mã nguồn với một số module bị vô hiệu hóa, một số định dạng có thể không khả dụng.

Nhập texture
------------

Hành động mặc định trong Godot là nhập hình ảnh dưới dạng texture. Texture được lưu trong bộ nhớ video. Không thể truy cập trực tiếp dữ liệu pixel của chúng từ CPU nếu không chuyển đổi chúng trở lại thành một :ref:`class_Image` trong script. Đây là yếu tố giúp việc vẽ chúng đạt hiệu suất cao.

Có hơn một tá tùy chọn nhập mà bạn có thể điều chỉnh sau khi chọn một hình ảnh trong dock FileSystem:

.. figure:: img/importing_images_import_dock.webp
   :align: center
   :alt: Các tùy chọn nhập trong dock Import sau khi chọn một hình ảnh trong dock FileSystem

   Các tùy chọn nhập trong dock Import sau khi chọn một hình ảnh trong dock FileSystem. Một số tùy chọn chỉ hiển thị với một số chế độ nén nhất định.

.. _doc_importing_images_changing_import_type:

Thay đổi kiểu nhập
~~~~~~~~~~~~~~~~~~

Bạn có thể chọn các kiểu tài nguyên đã nhập khác trong dock Import:

- **BitMap:** texture đơn sắc 1 bit (dùng làm mặt nạ nhấp chuột trong
  :ref:`class_TextureButton` và :ref:`class_TouchScreenButton`). Không thể hiển thị trực tiếp kiểu tài nguyên này trên các node 2D hoặc 3D, nhưng có thể truy vấn các giá trị pixel từ script bằng :ref:`get_bit <class_BitMap_method_get_bit>`.
- **Cubemap:** Nhập texture dưới dạng cubemap 6 mặt, có nội suy giữa các mặt của cubemap (cubemap liền mạch), có thể được lấy mẫu trong các shader tùy chỉnh.
- **CubemapArray:** Nhập texture dưới dạng một tập hợp các cubemap 6 mặt, có thể được lấy mẫu trong các shader tùy chỉnh. Kiểu tài nguyên này chỉ có thể hiển thị khi sử dụng renderer Forward+ hoặc Mobile, không phải renderer Compatibility.
- **DPITexture:** Chỉ khả dụng cho hình ảnh SVG. Tương tự Texture2D, nhưng có thể được rasterize lại ở các tỷ lệ khác nhau trong trình chỉnh sửa và tại runtime mà không cần nhập lại. Xem :ref:`doc_multiple_resolutions_font_and_image_oversampling` để biết chi tiết.
- **Font Data (Monospace Image Font):** Nhập hình ảnh dưới dạng bitmap font trong đó tất cả ký tự có cùng chiều rộng. Xem :ref:`doc_gui_using_fonts`.
- **Image:** Nhập hình ảnh nguyên trạng. Không thể hiển thị trực tiếp kiểu tài nguyên này trên các node 2D hoặc 3D, nhưng có thể truy vấn các giá trị pixel từ script bằng :ref:`get_pixel<class_Image_method_get_pixel>`.
- **Texture2D:** Nhập hình ảnh dưới dạng texture 2 chiều, phù hợp để hiển thị trên các bề mặt 2D và 3D. Đây là chế độ nhập mặc định.
- **Texture2DArray:** Nhập hình ảnh dưới dạng một tập hợp các texture 2 chiều. Texture2DArray tương tự texture 3 chiều, nhưng không có nội suy giữa các lớp. Shader 2D và 3D tích hợp sẵn không thể hiển thị mảng texture, vì vậy bạn phải tạo shader tùy chỉnh trong :ref:`2D <doc_canvas_item_shader>` hoặc :ref:`3D <doc_spatial_shader>` để hiển thị texture từ một mảng texture.
- **Texture3D:** Nhập hình ảnh dưới dạng texture 3 chiều. Đây *không phải* là texture 2D được áp dụng lên bề mặt 3D. Texture3D tương tự mảng texture, nhưng có nội suy giữa các lớp. Texture3D thường được sử dụng cho
  :ref:`class_FogMaterial` các bản đồ mật độ trong :ref:`sương thể tích <doc_volumetric_fog>`, các trường vector của :ref:`bộ thu hút hạt <doc_3d_particles_attractors>`, :ref:`class_Environment` hiệu chỉnh màu 3D LUT và các shader tùy chỉnh.
- **TextureAtlas:** Nhập hình ảnh dưới dạng một *atlas* gồm nhiều texture khác nhau. Có thể sử dụng để giảm mức sử dụng bộ nhớ cho các sprite 2D động. Chỉ được hỗ trợ trong 2D do shader 3D tích hợp sẵn chưa hỗ trợ.

Đối với **Cubemap**, thứ tự hình ảnh dự kiến là X+, X-, Y+, Y-, Z+, Z- (theo hệ tọa độ của Godot, nên Y+ là "lên" và Z- là "tiến về phía trước"). Dưới đây là các mẫu bạn có thể sử dụng cho hình ảnh cubemap (nhấp chuột phải > **Save Link As…**):

- :download:`Mẫu cubemap 2×3 (tùy chọn bố cục mặc định) <img/cubemap_template_2x3.webp>`
- :download:`Mẫu cubemap 3×2 <img/cubemap_template_3x2.webp>`
- :download:`Mẫu cubemap 1×6 <img/cubemap_template_1x6.webp>`
- :download:`Mẫu cubemap 6×1 <img/cubemap_template_6x1.webp>`

Phát hiện 3D
~~~~~~~~~~~~

Các tùy chọn nhập mặc định (không có mipmap và compression **Lossless**) phù hợp với 2D nhưng không lý tưởng cho hầu hết dự án 3D. **Detect 3D** giúp Godot nhận biết khi texture được sử dụng trong một cảnh 3D (chẳng hạn như texture trong một
:ref:`class_BaseMaterial3D`). Khi xảy ra điều này, một số tùy chọn nhập sẽ được thay đổi để các texture flags phù hợp hơn với 3D. Mipmap được bật và chế độ compression được đổi thành **VRAM Compressed** trừ khi
:ref:`doc_importing_images_detect_3d_compress_to` được thay đổi. Texture cũng được tự động reimport.

Một thông báo sẽ được in ra bảng Output khi phát hiện texture được sử dụng trong 3D.

Nếu bạn gặp vấn đề về chất lượng khi phát hiện texture được sử dụng trong 3D (ví dụ: texture pixel art), hãy thay đổi
:ref:`doc_importing_images_detect_3d_compress_to` trước khi sử dụng texture trong 3D, hoặc đổi :ref:`doc_importing_images_compress_mode` thành **Lossless** sau khi sử dụng texture trong 3D. Cách này tốt hơn việc tắt **Detect 3D**, vì việc tạo mipmap vẫn được bật để ngăn texture bị hạt ở khoảng cách xa.

Tùy chọn nhập
-------------

.. seealso::

    Kể từ Godot 4.0, các chế độ lọc texture và lặp được thiết lập trong các thuộc tính CanvasItem ở 2D (với một project setting đóng vai trò mặc định), và trong một
    :ref:`cấu hình theo từng material trong 3D <doc_standard_material_3d_sampling>`. Trong custom shader, chế độ lọc và lặp được thay đổi trên uniform ``sampler2D`` bằng các hint được mô tả trong tài liệu :ref:`doc_shading_language`.

.. _doc_importing_images_compress_mode:

Compress > Mode
~~~~~~~~~~~~~~~

Hình ảnh là một trong những asset lớn nhất trong game. Để xử lý chúng hiệu quả, cần compression. Godot cung cấp một số phương pháp compression, tùy thuộc vào trường hợp sử dụng.

- **Lossless:** Đây là chế độ compression mặc định và phổ biến nhất cho asset 2D. Chế độ này hiển thị asset mà không có bất kỳ artifact nào, đồng thời compression trên ổ đĩa ở mức khá tốt. Tuy nhiên, nó sẽ sử dụng nhiều video memory hơn đáng kể so với VRAM Compression. Đây cũng là thiết lập được khuyến nghị cho pixel art.
- **Lossy:** Đây là lựa chọn phù hợp cho các asset 2D lớn. Chế độ này có một số artifact, nhưng ít hơn VRAM compression, còn kích thước file thấp hơn nhiều lần so với Lossless hoặc VRAM Uncompressed. Chế độ này không làm giảm mức sử dụng video memory; mức sử dụng giống với Lossless hoặc VRAM Uncompressed.
- **VRAM Compressed:** Đây là chế độ compression mặc định và phổ biến nhất cho asset 3D. Kích thước trên ổ đĩa được giảm, đồng thời mức sử dụng video memory cũng giảm đáng kể (thường từ 4 đến 6 lần). Nên tránh sử dụng chế độ này cho 2D vì nó tạo ra các artifact dễ nhận thấy, đặc biệt với texture có độ phân giải thấp.
- **VRAM Uncompressed:** Chỉ hữu ích cho các định dạng không thể được compressed, chẳng hạn như hình ảnh floating-point thô.
- **Basis Universal:** Chế độ compression VRAM thay thế này mã hóa texture sang một định dạng có thể được chuyển đổi sang hầu hết các định dạng GPU-compressed khi tải. Cách này tạo ra các file rất nhỏ, tận dụng compression VRAM, nhưng phải đánh đổi bằng chất lượng thấp hơn so với VRAM Compressed và thời gian compression chậm hơn. Mức sử dụng VRAM thường giống với VRAM Compressed. Basis Universal không hỗ trợ các định dạng hình ảnh floating-point (engine sẽ tự động chuyển về VRAM Compressed ở bên trong).

.. note::

    Ngay cả trong 3D, texture "pixel art" cũng nên tắt VRAM compression vì nó sẽ ảnh hưởng tiêu cực đến hình thức hiển thị mà không cải thiện đáng kể hiệu năng do độ phân giải thấp.

Trong bảng này, mỗi tùy chọn trong 5 tùy chọn được mô tả cùng với ưu điểm và nhược điểm của chúng (|good| = tốt nhất, |bad| = kém nhất):

+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+
| Compress mode             | Lossless                               | Lossy                         | VRAM Compressed                                                | VRAM Uncompressed            | Basis Universal                                |
+===========================+========================================+===============================+================================================================+==============================+================================================+
| **Mô tả**                 | Được lưu dưới dạng Lossless WebP / PNG | Được lưu dưới dạng Lossy WebP | Được lưu dưới dạng S3TC, BPTC hoặc ETC2 tùy thuộc vào nền tảng | Được lưu dưới dạng pixel thô | Được chuyển đổi sang định dạng VRAM Compressed |
+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+
| **Kích thước trên ổ đĩa** | |regular| Nhỏ                          | |good| Rất nhỏ                | |regular| Nhỏ                                                  | |bad| Lớn                    | |good| Rất nhỏ                                 |
+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+
| **Mức sử dụng bộ nhớ**    | |bad| Lớn                              | |bad| Lớn                     | |good| Nhỏ                                                     | |bad| Lớn                    | |good| Nhỏ                                     |
+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+
| **Hiệu năng**             | |regular| Bình thường                  | |regular| Bình thường         | |good| Nhanh                                                   | |regular| Bình thường        | |good| Nhanh                                   |
+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+
| **Mức giảm chất lượng**   | |good| Không                           | |regular| Nhẹ                 | |bad| Vừa phải                                                 | |good| Không                 | |bad| Vừa phải                                 |
+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+
| **Thời gian tải**         | |bad| Chậm                             | |bad| Chậm                    | |good| Nhanh                                                   | |regular| Bình thường        | |regular| Bình thường                          |
+---------------------------+----------------------------------------+-------------------------------+----------------------------------------------------------------+------------------------------+------------------------------------------------+

.. |bad| image:: img/bad.png

.. |good| image:: img/good.png

.. |regular| image:: img/regular.png

Mức sử dụng bộ nhớ ước tính cho một texture RGBA8 đơn có bật mipmap:

+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+
| Kích thước texture | Lossless           | Lossy              | VRAM Compressed    | VRAM Uncompressed  | Basis Universal    |
+====================+====================+====================+====================+====================+====================+
| **128×128**        | |good| 85 KiB      | |good| 85 KiB      | |good| 21 KiB      | |good| 85 KiB      | |good| 21 KiB      |
+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+
| **256×256**        | |good| 341 KiB     | |good| 341 KiB     | |good| 85 KiB      | |good| 341 KiB     | |good| 85 KiB      |
+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+
| **512×512**        | |good| 1.33 MiB    | |good| 1.33 MiB    | |good| 341 KiB     | |good| 1.33 MiB    | |good| 341 KiB     |
+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+
| **1024×1024**      | |regular| 5.33 MiB | |regular| 5.33 MiB | |good| 1.33 MiB    | |regular| 5.33 MiB | |good| 1.33 MiB    |
+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+
| **2048×2048**      | |bad| 21.33 MiB    | |bad| 21.33 MiB    | |regular| 5.33 MiB | |bad| 21.33 MiB    | |regular| 5.33 MiB |
+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+
| **4096×4096**      | |bad| 85.33 MiB    | |bad| 85.33 MiB    | |bad| 21.33 MiB    | |bad| 85.33 MiB    | |bad| 21.33 MiB    |
+--------------------+--------------------+--------------------+--------------------+--------------------+--------------------+

.. note::

    Trong bảng trên, mức sử dụng bộ nhớ sẽ giảm 25% đối với các hình ảnh không có kênh alpha (RGB8). Mức sử dụng bộ nhớ sẽ tiếp tục giảm 25% đối với các hình ảnh đã tắt mipmap.

Lưu ý rằng ở các độ phân giải lớn hơn, tác động của việc nén VRAM lớn hơn nhiều. Với tỷ lệ nén 4:1 (6:1 đối với texture mờ đục sử dụng S3TC), việc nén VRAM cho phép một texture có kích thước lớn gấp đôi trên mỗi trục mà vẫn sử dụng cùng một lượng bộ nhớ trên GPU.

Việc nén VRAM cũng làm giảm băng thông bộ nhớ cần thiết để lấy mẫu texture, nhờ đó có thể tăng tốc quá trình kết xuất trong các trường hợp bị giới hạn băng thông bộ nhớ (thường gặp trên đồ họa tích hợp và thiết bị di động). Kết hợp lại, các yếu tố này khiến việc nén VRAM trở thành yêu cầu thiết yếu đối với các game 3D sử dụng texture độ phân giải cao.

Bạn có thể xem trước texture chiếm bao nhiêu bộ nhớ bằng cách nhấp đúp vào texture trong dock FileSystem, sau đó xem Inspector:

.. figure:: img/importing_images_inspector_preview.webp
   :align: center
   :alt: Xem trước texture trong Inspector

   Xem trước texture trong Inspector. Tín dụng: `Red Brick 03 - Poly Haven <https://polyhaven.com/a/red_brick_03>`__

Nén > Chất lượng cao
~~~~~~~~~~~~~~~~~~~~

.. note::

    Chỉ các renderer Forward+ và Mobile mới hỗ trợ nén texture VRAM chất lượng cao.

    Khi sử dụng renderer Compatibility, tùy chọn này luôn được xem là đã tắt.

Nếu được bật, sử dụng tính năng nén BPTC trên các nền tảng máy tính và tính năng nén :abbr:`ASTC (Adaptive Scalable Texture Compression)` trên các nền tảng di động. Khi sử dụng BPTC, BC7 được dùng cho texture SDR và BC6H được dùng cho texture HDR.

Nếu bị tắt (mặc định), sử dụng tính năng nén S3TC nhanh hơn nhưng chất lượng thấp hơn trên các nền tảng máy tính, và ETC2 trên các nền tảng di động/web. Khi sử dụng S3TC, DXT1 (BC1) được dùng cho texture không trong suốt và DXT5 (BC3) được dùng cho texture trong suốt hoặc texture normal map (:abbr:`RGTC (Red-Green Texture Compression)`).

BPTC và ASTC hỗ trợ nén VRAM cho texture HDR, nhưng S3TC và ETC2 thì không (xem **HDR Compression** bên dưới).

Nén > Nén HDR
~~~~~~~~~~~~~

.. note::

    Tùy chọn này chỉ có tác dụng với các texture được import dưới dạng format HDR trong Godot (các tệp ``.hdr`` và ``.exr``).

Nếu được đặt thành **Disabled**, không bao giờ sử dụng tính năng nén VRAM cho texture HDR, bất kể chúng không trong suốt hay trong suốt. Thay vào đó, texture được chuyển đổi thành RGBE9995 (9 bit mỗi kênh + số mũ 5 bit = 32 bit mỗi pixel) để giảm mức sử dụng bộ nhớ so với format ảnh half-float hoặc floating-point độ chính xác đơn.

Nếu được đặt thành **Opaque Only** (mặc định), chỉ sử dụng tính năng nén VRAM cho texture HDR không trong suốt. Điều này là do một hạn chế của các format HDR, vì không có format HDR được nén VRAM nào đồng thời hỗ trợ độ trong suốt.

Nếu được đặt thành **Always**, sẽ buộc sử dụng tính năng nén VRAM ngay cả với texture HDR có kênh alpha. Để thực hiện việc này, kênh alpha sẽ bị loại bỏ khi import.

Nén > Normal Map
~~~~~~~~~~~~~~~~

Khi sử dụng texture làm normal map, chỉ cần các kênh đỏ và xanh lá. Vì các thuật toán nén texture thông thường tạo ra các hiện tượng không đẹp trong normal map, format nén :abbr:`RGTC (Red-Green Texture Compression)` là lựa chọn phù hợp nhất cho dữ liệu này. Buộc tùy chọn này thành **Enable** sẽ khiến Godot import ảnh dưới dạng được nén bằng :abbr:`RGTC (Red-Green Texture Compression)`. Theo mặc định, tùy chọn này được đặt thành **Detect**. Điều này có nghĩa là nếu texture được phát hiện đang được sử dụng làm normal map, nó sẽ được chuyển thành **Enable** và tự động reimport.

Lưu ý rằng tính năng nén :abbr:`RGTC (Red-Green Texture Compression)` ảnh hưởng đến ảnh normal map kết quả. Bạn sẽ phải điều chỉnh các shader tùy chỉnh sử dụng kênh xanh dương của normal map để tính đến điều này. Các shader material tích hợp sẵn đã bỏ qua kênh xanh dương trong normal map (bất kể nội dung thực tế của normal map).

Trong ví dụ bên dưới, normal map được nén bằng :abbr:`RGTC (Red-Green Texture Compression)` có thể giữ lại chi tiết tốt hơn nhiều, đồng thời sử dụng cùng lượng bộ nhớ như texture RGBA được nén VRAM tiêu chuẩn:

.. figure:: img/importing_images_normal_map_rgtc.webp
   :align: center
   :alt: Normal map với tính năng nén VRAM tiêu chuẩn (bên trái) và với tính năng nén VRAM RGTC (bên phải)

   Normal map với tính năng nén VRAM tiêu chuẩn (bên trái) và với tính năng nén VRAM RGTC (bên phải)

.. note::

  Godot yêu cầu normal map sử dụng các tọa độ X+, Y+ và Z+, được gọi là normal map kiểu OpenGL. Nếu bạn đã import một material được tạo để sử dụng với engine khác, material đó có thể thuộc kiểu DirectX. Trong trường hợp này, normal map cần được chuyển đổi bằng cách bật tùy chọn import **Normal Map Invert Y**.

  Có thể tìm thấy thêm thông tin về normal map (bao gồm bảng thứ tự tọa độ cho các engine phổ biến) `tại đây <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details>`__.

Nén > Đóng gói kênh
~~~~~~~~~~~~~~~~~~~

Nếu được đặt thành **sRGB Friendly** (mặc định), ngăn không cho sử dụng format màu RG vì format này không hỗ trợ màu sRGB.

Nếu được đặt thành **Optimized**, cho phép sử dụng format màu RG nếu texture không sử dụng kênh xanh dương.

Tùy chọn thứ ba **Normal Map (RG Channels)** *chỉ* khả dụng trong các texture nhiều lớp (:ref:`class_Cubemap`, :ref:`class_CubemapArray`, :ref:`class_Texture2DArray` và :ref:`class_Texture3D`). Tùy chọn này buộc tất cả các layer của texture được import bằng format màu RG, chỉ giữ lại các kênh đỏ và xanh lá. Tính năng nén :abbr:`RGTC (Red-Green Texture Compression)` có thể giữ lại chi tiết tốt hơn nhiều, đồng thời sử dụng cùng lượng bộ nhớ như texture RGBA được nén VRAM tiêu chuẩn. Tùy chọn này chỉ có tác dụng với các texture sử dụng chế độ nén **VRAM Compressed** hoặc **Basis Universal**.

.. _doc_importing_images_mipmaps:

Mipmaps > Tạo
~~~~~~~~~~~~~

Nếu được bật, các phiên bản nhỏ hơn của texture sẽ được tạo khi import. Ví dụ, một texture 64×64 sẽ tạo ra 6 mipmap (32×32, 16×16, 8×8, 4×4, 2×2, 1×1). Điều này mang lại một số lợi ích:

- Texture sẽ không bị nhiễu hạt khi ở xa (trong 3D), hoặc khi bị thu nhỏ do camera zoom hoặc scale của CanvasItem (trong 2D).
- Hiệu suất sẽ được cải thiện nếu texture được hiển thị ở xa, vì việc lấy mẫu các phiên bản nhỏ hơn của texture gốc nhanh hơn và yêu cầu ít băng thông bộ nhớ hơn.

Nhược điểm của mipmap là chúng làm tăng mức sử dụng bộ nhớ khoảng 33%.

Bạn nên bật mipmap trong 3D. Tuy nhiên, trong 2D, chỉ nên bật tùy chọn này nếu dự án của bạn thực sự hưởng lợi rõ rệt từ việc bật mipmap. Nếu camera không bao giờ zoom out đáng kể, việc bật mipmap sẽ không mang lại lợi ích nhưng lại làm tăng mức sử dụng bộ nhớ.

Mipmaps > Giới hạn
~~~~~~~~~~~~~~~~~~

.. UPDATE: Not implemented. When Mipmaps > Limit is implemented, remove this
.. warning and remove this comment.

.. warning::

    **Mipmaps > Limit** hiện chưa được triển khai và không có tác dụng khi thay đổi.

Nếu được đặt thành giá trị lớn hơn ``-1``, giới hạn số mipmap tối đa có thể được tạo. Bạn có thể giảm giá trị này nếu không muốn texture trở nên có độ phân giải quá thấp ở khoảng cách rất xa, đổi lại sẽ có một chút nhiễu hạt.

Roughness > Chế độ
~~~~~~~~~~~~~~~~~~

Kênh màu được xem là roughness map trong texture này. Chỉ có hiệu lực nếu **Roughness > Src Normal** không trống.

Roughness > Normal nguồn
~~~~~~~~~~~~~~~~~~~~~~~~

Đường dẫn đến texture được xem là normal map để lọc roughness khi import. Việc chỉ định texture này có thể giúp giảm nhẹ hiện tượng aliasing specular trong 3D.

Tính năng lọc roughness khi import chỉ được sử dụng trong rendering 3D, không dùng trong 2D.

Xử lý > Sửa viền Alpha
~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này đặt các pixel có cùng màu xung quanh vào vùng chuyển tiếp từ trong suốt sang không trong suốt. Đối với texture được hiển thị bằng bilinear filtering, điều này giúp giảm hiệu ứng đường viền khi export ảnh từ trình chỉnh sửa ảnh.

.. image:: img/fixedborder.png

Bạn nên để tùy chọn này được bật (như mặc định), trừ khi tùy chọn này gây ra sự cố với một hình ảnh cụ thể.

Process > Premult Alpha
~~~~~~~~~~~~~~~~~~~~~~~

Một giải pháp thay thế cho việc khắc phục các đường viền bị tối bằng **Fix Alpha Border** là sử dụng alpha premultiplied. Khi bật tùy chọn này, texture sẽ được chuyển đổi sang định dạng này. Texture alpha premultiplied cần các material cụ thể để được hiển thị chính xác:

- Trong 2D, cần tạo một :ref:`class_CanvasItemMaterial` và cấu hình để sử dụng chế độ hòa trộn **Premultiplied Alpha** trên các CanvasItems sử dụng texture này. Trong :ref:`custom canvas item shaders <doc_canvas_item_shader>`, nên sử dụng ``render_mode blend_premul_alpha;``.
- Trong 3D, cần tạo một :ref:`class_BaseMaterial3D` và cấu hình để sử dụng chế độ hòa trộn **Premult Alpha** trên các material sử dụng texture này. Trong :ref:`custom spatial shaders <doc_spatial_shader>`, nên sử dụng ``render_mode blend_premul_alpha;``.

Process > Normal Map Invert Y
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot yêu cầu normal map sử dụng các tọa độ X+, Y+ và Z+, được gọi là normal map kiểu OpenGL. Nếu bạn đã import một material được tạo để sử dụng với engine khác, material đó có thể là kiểu DirectX. Trong trường hợp này, normal map cần được chuyển đổi bằng cách bật tùy chọn import **Normal Map Invert Y**.

Bạn có thể tìm thêm thông tin về normal map (bao gồm bảng thứ tự tọa độ cho các engine phổ biến) `tại đây <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details>`__.

Process > HDR as sRGB
~~~~~~~~~~~~~~~~~~~~~

Một số hình ảnh HDR bạn có thể tìm thấy trên mạng có thể bị lỗi và chứa dữ liệu màu sRGB (thay vì dữ liệu màu tuyến tính). Bạn không nên sử dụng các tệp đó. Nếu bắt buộc phải sử dụng, việc bật tùy chọn này sẽ khiến chúng hiển thị chính xác.

.. warning::

    Việc bật **HDR as sRGB** trên các hình ảnh HDR được định dạng đúng sẽ khiến hình ảnh kết quả trông quá tối, vì vậy hãy để tùy chọn này tắt nếu không chắc chắn.

Process > HDR Clamp Exposure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một số hình ảnh panorama HDR bạn có thể tìm thấy trên mạng có thể chứa các pixel cực kỳ sáng, do được chụp từ nguồn thực tế mà không có bất kỳ thao tác clipping nào.

Mặc dù các hình ảnh panorama HDR này phản ánh chính xác thực tế, điều này có thể khiến radiance map do Godot tạo ra chứa các đốm sáng khi được dùng làm bầu trời nền. Hiện tượng này có thể thấy trong các phản chiếu của material (thậm chí trên các material thô trong những trường hợp cực đoan). Bật **HDR Clamp Exposure** có thể khắc phục vấn đề này bằng một công thức giới hạn thông minh, không tạo ra hiện tượng clipping *visible* – glow vẫn tiếp tục hoạt động khi nhìn vào bầu trời nền.

Process > Size Limit
~~~~~~~~~~~~~~~~~~~~

Nếu được đặt thành một giá trị lớn hơn ``0``, kích thước của texture sẽ bị giới hạn khi import ở một giá trị nhỏ hơn hoặc bằng giá trị được chỉ định tại đây. Với texture không vuông, giới hạn kích thước ảnh hưởng đến chiều dài hơn, còn chiều ngắn hơn sẽ được điều chỉnh theo tỷ lệ để giữ nguyên tỷ lệ khung hình. Việc thay đổi kích thước được thực hiện bằng phép nội suy cubic.

Có thể dùng tùy chọn này để giảm mức sử dụng bộ nhớ mà không ảnh hưởng đến các hình ảnh nguồn, hoặc tránh các sự cố khiến texture không hiển thị trên nền tảng mobile/web (vì các nền tảng này thường không thể hiển thị texture lớn hơn 4096×4096).

.. _doc_importing_images_detect_3d_compress_to:

Detect 3D > Compress To
~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này thay đổi tùy chọn :ref:`doc_importing_images_compress_mode` được sử dụng khi phát hiện texture đang được dùng trong 3D.

Việc thay đổi tùy chọn import này chỉ có hiệu lực nếu phát hiện texture đang được dùng trong 3D. Thay đổi tùy chọn này thành **Disabled** rồi import lại sẽ không thay đổi chế độ nén hiện có trên texture (nếu texture được phát hiện là đang được dùng trong 3D), nhưng chọn **VRAM Compressed** hoặc **Basis Universal** thì sẽ thay đổi.

SVG > Scale
~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng cho hình ảnh SVG.*

Tỷ lệ mà SVG sẽ được render, trong đó ``1.0`` là kích thước thiết kế ban đầu. Giá trị cao hơn sẽ tạo ra hình ảnh lớn hơn. Lưu ý rằng không giống như oversampling của font, tùy chọn này ảnh hưởng đến kích thước vật lý mà SVG được render trong 2D. Xem thêm **Editor > Scale With Editor Scale** bên dưới.

.. _doc_importing_images_editor_import_options:

Editor > Scale With Editor Scale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng cho hình ảnh SVG.*

Nếu là true, hình ảnh đã import sẽ được điều chỉnh tỷ lệ để khớp với hệ số tỷ lệ hiển thị của editor. Nên bật tùy chọn này cho các biểu tượng của editor plugin và biểu tượng custom class, nhưng nên để tắt trong các trường hợp khác.

Editor > Convert Colors With Editor Theme
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng cho hình ảnh SVG.*

Nếu được chọn, tùy chọn này sẽ chuyển đổi màu của hình ảnh đã import để khớp với bảng màu biểu tượng và font của editor. Điều này giả định rằng hình ảnh sử dụng chính xác các màu giống như
:ref:`bảng màu riêng của Godot dành cho các biểu tượng của editor <doc_editor_icons>`, với tệp nguồn được thiết kế cho theme tối của editor. Nên bật tùy chọn này cho các biểu tượng của editor plugin và biểu tượng custom class, nhưng nên để tắt trong các trường hợp khác.

.. _doc_importing_images_svg_text:

Importing SVG images with text
------------------------------

Vì thư viện SVG được Godot sử dụng không hỗ trợ rasterize văn bản có trong hình ảnh SVG, văn bản phải được chuyển đổi thành path trước. Nếu không, văn bản sẽ không xuất hiện trong hình ảnh đã rasterize.

Có hai cách để thực hiện việc này theo phương thức không phá hủy, nhờ đó bạn vẫn có thể tiếp tục chỉnh sửa văn bản gốc sau này:

- Chọn đối tượng văn bản trong Inkscape, sau đó nhân bản tại chỗ bằng cách nhấn
  :kbd:`Ctrl + D` và sử dụng **Path > Object to Path**. Sau đó ẩn đối tượng văn bản gốc bằng dock **Layers and Objects**.
- Sử dụng dòng lệnh Inkscape để export một SVG từ một tệp SVG khác, trong đó văn bản được chuyển đổi thành path:

::

    inkscape --export-text-to-path --export-filename svg_with_text_converted_to_path.svg svg_with_text.svg

Best practices
--------------

Supporting high-resolution texture sizes in 2D without artifacts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để hỗ trợ :ref:`multiple resolutions <doc_multiple_resolutions>` với hình ảnh sắc nét ở độ phân giải cao, bạn sẽ cần sử dụng các hình ảnh nguồn có độ phân giải cao (phù hợp với độ phân giải cao nhất mà bạn muốn hỗ trợ mà không bị mờ, thường là 4K trong các game desktop hiện đại).

Có 2 cách để thực hiện:

- Sử dụng độ phân giải cơ sở cao trong cài đặt project (chẳng hạn như 4K), sau đó sử dụng texture ở tỷ lệ gốc. Đây là cách dễ hơn.
- Sử dụng độ phân giải cơ sở thấp trong cài đặt dự án (chẳng hạn 1080p), sau đó giảm kích thước texture khi sử dụng chúng. Cách này thường khó hơn và có thể khiến nhiều phép tính trong script trở nên tẻ nhạt, vì vậy nên sử dụng phương pháp được mô tả ở trên.

Sau khi thực hiện việc này, bạn có thể nhận thấy texture trở nên nhiễu hạt ở độ phân giải viewport thấp hơn. Để khắc phục, hãy bật **Mipmaps** cho các texture được sử dụng trong 2D tại dock Import. Điều này sẽ làm tăng mức sử dụng bộ nhớ.

Việc bật mipmap cũng có thể khiến texture trông mờ hơn, nhưng bạn có thể làm texture sắc nét hơn (đổi lại sẽ có một chút nhiễu hạt) bằng cách đặt **Rendering > Textures > Default Filters > Texture Mipmap Bias** thành một giá trị âm.

Sử dụng kích thước texture phù hợp trong 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù không có khuyến nghị "phù hợp với mọi trường hợp", dưới đây là một số khuyến nghị chung để lựa chọn kích thước texture trong 3D:

- Nên điều chỉnh kích thước texture để có mật độ texel nhất quán so với các đối tượng xung quanh. Mặc dù không thể đảm bảo hoàn hảo khi chỉ sử dụng các kích thước texture lũy thừa của hai, thông thường vẫn có thể duy trì chi tiết texture khá nhất quán trong toàn bộ cảnh 3D.
- Đối tượng xuất hiện càng nhỏ trên màn hình thì texture của nó càng nên nhỏ. Ví dụ, một cái cây chỉ xuất hiện ở hậu cảnh không cần độ phân giải texture cao như các đối tượng khác mà người chơi có thể đến gần.
- Khuyến nghị sử dụng các kích thước texture lũy thừa của hai, nhưng đây không phải là yêu cầu bắt buộc. Texture không nhất thiết phải có dạng hình vuông – các kích thước như 1024×512 đều được chấp nhận.
- Việc sử dụng texture có kích thước lớn mang lại lợi ích giảm dần, dù mức sử dụng bộ nhớ và thời gian tải tăng lên. Hầu hết các game 3D hiện đại không sử dụng phong cách pixel art thường dùng texture 2048×2048, cùng với 1024×1024 và 512×512 cho các texture trải trên những bề mặt nhỏ hơn.
- Khi làm việc với các material dựa trên tính chất vật lý trong 3D, bạn có thể giảm mức sử dụng bộ nhớ và kích thước tệp mà không ảnh hưởng quá nhiều đến chất lượng bằng cách sử dụng độ phân giải thấp hơn cho một số texture map nhất định. Cách này đặc biệt hiệu quả với các texture chỉ có chi tiết tần số thấp (chẳng hạn như normal map cho texture tuyết).

Nếu bạn có quyền kiểm soát cách tạo các model 3D, những mẹo sau đây cũng đáng để tìm hiểu:

- Khi làm việc với các model 3D chủ yếu có tính đối xứng, bạn có thể sử dụng UV đối xứng để tăng gấp đôi mật độ texel hiệu dụng. Tuy nhiên, cách này có thể trông không tự nhiên khi sử dụng trên khuôn mặt người.
- Khi làm việc với các model 3D theo phong cách low-poly và có màu đơn sắc, bạn có thể sử dụng màu vertex thay cho texture để biểu thị màu sắc trên các bề mặt của model.

.. seealso::

    Hình ảnh có thể được tải và lưu trong runtime bằng
    :ref:`runtime file loading and saving <doc_runtime_file_loading_and_saving_images>`, kể cả từ một dự án đã export.
