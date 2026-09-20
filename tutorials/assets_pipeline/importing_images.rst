.. _doc_importing_images:

Nhập hình ảnh
=============

Các định dạng hình ảnh được hỗ trợ
----------------------------------

Godot có thể nhập các định dạng hình ảnh sau:

**Raster:**

- BMP (``.bmp``) - Tất cả các định dạng pixel đều được hỗ trợ, nhưng không hỗ trợ tính năng nén :abbr:`RLE (Run-Length Encoding)`.

- DirectDraw Surface (``.dds``) - Nếu texture có mipmap, chúng sẽ được tải trực tiếp. Có thể dùng tính năng này để tạo hiệu ứng bằng mipmap tùy chỉnh.

- Khronos Texture (``.ktx``) - Việc giải mã được thực hiện bằng `libktx <https://github.com/KhronosGroup/KTX-Software>`__. Chỉ hỗ trợ hình ảnh 2D. Không hỗ trợ cubemap, mảng texture và bỏ padding.

- OpenEXR (``.exr``) - Hỗ trợ HDR (rất khuyến nghị dùng cho bầu trời panorama).

- Radiance HDR (``.hdr``) - Hỗ trợ HDR (rất khuyến nghị dùng cho bầu trời panorama).

- JPEG (``.jpg``, ``.jpeg``) - Không hỗ trợ độ trong suốt do giới hạn của định dạng.

- PNG (``.png``) - Độ chính xác bị giới hạn ở 8 bit trên mỗi kênh khi nhập (không hỗ trợ hình ảnh HDR).

- Truevision Targa (``.tga``)

- WebP (``.webp``) - Các tệp WebP hỗ trợ độ trong suốt và có thể được nén lossy hoặc lossless. Độ chính xác bị giới hạn ở 8 bit trên mỗi kênh.

**Vector:**

- SVG (``.svg``)

  - Theo mặc định, SVG được rasterize tại thời điểm nhập.

  - SVG là định dạng hình ảnh duy nhất có thể được nhập dưới dạng DPITexture, cho phép rasterize tại runtime để khớp với hệ số oversampling hiện tại. Xem :ref:`doc_importing_images_changing_import_type` để biết chi tiết.

  - Godot sử dụng thư viện `ThorVG <https://www.thorvg.org/>`__ để render SVG. `SVG feature support is limited <https://www.thorvg.org/about#:~:text=certain%20features%20remain%20unsupported%20within%20the%20current%20framework>`__; các vector phức tạp có thể không được render chính xác. :ref:`Text must be converted to paths <doc_importing_images_svg_text>`; nếu không, nó sẽ không xuất hiện trong hình ảnh đã rasterize. Đối với các vector phức tạp, render chúng thành PNG bằng `Inkscape <https://inkscape.org/>`__ thường là giải pháp tốt hơn. Việc này có thể được tự động hóa nhờ `command-line interface <https://wiki.inkscape.org/wiki/index.php/Using_the_Command_Line#Export_files>`__ của nó.

  - Bạn có thể kiểm tra xem ThorVG có thể render chính xác một vector cụ thể hay không bằng `web-based viewer <https://www.thorvg.org/viewer>`__ của nó.

.. note::

    Nếu bạn đã biên dịch trình chỉnh sửa Godot từ mã nguồn với một số module cụ thể bị vô hiệu hóa, một số định dạng có thể không khả dụng.

Nhập texture
------------

Hành động mặc định trong Godot là nhập hình ảnh dưới dạng texture. Texture được lưu trong bộ nhớ video. Không thể truy cập trực tiếp dữ liệu pixel từ CPU nếu không chuyển chúng trở lại thành một :ref:`class_Image` trong script. Đây là yếu tố giúp việc vẽ texture đạt hiệu suất cao.

Có hơn một chục tùy chọn nhập có thể điều chỉnh sau khi chọn một hình ảnh trong dock FileSystem:

.. figure:: img/importing_images_import_dock.webp
   :align: center
   :alt: Import options in the Import dock after selecting an image in the FileSystem dock

   Import options in the Import dock after selecting an image in the FileSystem dock.
   Some of these options are only visible with certain compression modes.

.. _doc_importing_images_changing_import_type:

Thay đổi kiểu nhập
~~~~~~~~~~~~~~~~~~

Có thể chọn các kiểu resource được nhập khác trong dock Import:

- **BitMap:** texture đơn sắc 1 bit (dự kiến được dùng làm mặt nạ nhấp chuột trong
  :ref:`class_TextureButton` and :ref:`class_TouchScreenButton`). This resource
  kiểu này không thể được hiển thị trực tiếp trên các node 2D hoặc 3D, nhưng có thể truy vấn các giá trị pixel từ script bằng :ref:`get_bit <class_BitMap_method_get_bit>`. - **Cubemap:** Nhập texture dưới dạng cubemap 6 mặt, với phép nội suy giữa các mặt của cubemap (cubemap liền mạch), có thể được lấy mẫu trong các shader tùy chỉnh. - **CubemapArray:** Nhập texture dưới dạng một tập hợp các cubemap 6 mặt, có thể được lấy mẫu trong các shader tùy chỉnh. Kiểu resource này chỉ có thể được hiển thị khi sử dụng renderer Forward+ hoặc Mobile, không phải renderer Compatibility. - **DPITexture:** Chỉ khả dụng cho hình ảnh SVG. Tương tự Texture2D, nhưng có thể được rasterize lại ở các tỷ lệ khác nhau trong editor và runtime mà không cần nhập lại. Xem :ref:`doc_multiple_resolutions_font_and_image_oversampling` để biết chi tiết. - **Font Data (Monospace Image Font):** Nhập hình ảnh dưới dạng bitmap font trong đó tất cả ký tự có cùng chiều rộng. Xem :ref:`doc_gui_using_fonts`. - **Image:** Nhập hình ảnh nguyên trạng. Kiểu resource này không thể được hiển thị trực tiếp trên các node 2D hoặc 3D, nhưng có thể truy vấn các giá trị pixel từ script bằng :ref:`get_pixel<class_Image_method_get_pixel>`. - **Texture2D:** Nhập hình ảnh dưới dạng texture 2 chiều, phù hợp để hiển thị trên các bề mặt 2D và 3D. Đây là chế độ nhập mặc định. - **Texture2DArray:** Nhập hình ảnh dưới dạng một tập hợp các texture 2 chiều. Texture2DArray tương tự texture 3 chiều, nhưng không có phép nội suy giữa các layer. Các shader 2D và 3D tích hợp sẵn không thể hiển thị mảng texture, vì vậy bạn phải tạo shader tùy chỉnh trong :ref:`2D <doc_canvas_item_shader>` hoặc :ref:`3D <doc_spatial_shader>` để hiển thị texture từ một mảng texture. - **Texture3D:** Nhập hình ảnh dưới dạng texture 3 chiều. Đây *không phải* là texture 2D được áp dụng lên một bề mặt 3D. Texture3D tương tự mảng texture, nhưng có phép nội suy giữa các layer. Texture3D thường được dùng cho
  :ref:`class_FogMaterial` density maps in :ref:`volumetric fog
  <doc_volumetric_fog>`, các trường vector :ref:`particle attractor <doc_3d_particles_attractors>`, :ref:`class_Environment` 3D LUT để hiệu chỉnh màu và các shader tùy chỉnh. - **TextureAtlas:** Nhập hình ảnh dưới dạng *atlas* gồm nhiều texture khác nhau. Có thể dùng để giảm mức sử dụng bộ nhớ cho các sprite 2D động. Chỉ được hỗ trợ trong 2D do các shader 3D tích hợp sẵn chưa hỗ trợ.

Đối với **Cubemap**, thứ tự hình ảnh dự kiến là X+, X-, Y+, Y-, Z+, Z- (trong hệ tọa độ của Godot, vì vậy Y+ là "lên trên" và Z- là "hướng về phía trước"). Dưới đây là các template bạn có thể dùng cho hình ảnh cubemap (nhấp chuột phải > **Save Link As…**):

- :download:`2×3 cubemap template (default layout option) <img/cubemap_template_2x3.webp>` - :download:`3×2 cubemap template <img/cubemap_template_3x2.webp>` - :download:`1×6 cubemap template <img/cubemap_template_1x6.webp>` - :download:`6×1 cubemap template <img/cubemap_template_6x1.webp>`

Detect 3D
~~~~~~~~~

Các tùy chọn nhập mặc định (không có mipmap và nén **Lossless**) phù hợp với 2D, nhưng không lý tưởng cho hầu hết dự án 3D. **Detect 3D** giúp Godot nhận biết khi texture được sử dụng trong một cảnh 3D (chẳng hạn như texture trong một
:ref:`class_BaseMaterial3D`). If this happens, several import options are
được thay đổi để các cờ texture phù hợp hơn với 3D. Mipmap được bật và chế độ nén được đổi thành **VRAM Compressed** trừ khi
:ref:`doc_importing_images_detect_3d_compress_to` is changed. The texture is
cũng được tự động nhập lại.

Một thông báo được in trong panel Output khi phát hiện texture được sử dụng trong 3D.

Nếu bạn gặp vấn đề về chất lượng khi phát hiện texture được sử dụng trong 3D (ví dụ: texture pixel art), hãy thay đổi
:ref:`doc_importing_images_detect_3d_compress_to` option before using the
texture trong 3D hoặc đổi :ref:`doc_importing_images_compress_mode` thành **Lossless** sau khi sử dụng texture trong 3D. Cách này tốt hơn việc tắt **Detect 3D**, vì việc tạo mipmap vẫn được bật để ngăn texture bị nhiễu hạt khi ở xa.

Tùy chọn nhập
-------------

.. seealso::

    Kể từ Godot 4.0, chế độ lọc và lặp texture được thiết lập trong các thuộc tính CanvasItem ở chế độ 2D (với một thiết lập project làm mặc định), và trong một
    :ref:`per-material configuration in 3D <doc_standard_material_3d_sampling>`.
    Trong các shader tùy chỉnh, chế độ lọc và lặp được thay đổi trên uniform ``sampler2D`` bằng các hint được mô tả trong tài liệu :ref:`doc_shading_language`.

.. _doc_importing_images_compress_mode:

Compress > Mode
~~~~~~~~~~~~~~~

Hình ảnh là một trong những asset lớn nhất trong game. Để xử lý chúng hiệu quả, cần nén chúng. Godot cung cấp một số phương pháp nén, tùy thuộc vào trường hợp sử dụng.

- **Lossless:** Đây là chế độ nén mặc định và phổ biến nhất cho asset 2D. Nó hiển thị asset mà không tạo ra bất kỳ artifact nào, đồng thời mức nén trên đĩa khá tốt. Tuy nhiên, nó sẽ sử dụng nhiều bộ nhớ video hơn đáng kể so với VRAM Compression. Đây cũng là thiết lập được khuyến nghị cho pixel art. - **Lossy:** Đây là lựa chọn phù hợp cho các asset 2D lớn. Nó tạo ra một số artifact, nhưng ít hơn VRAM compression, và kích thước tệp thấp hơn vài lần so với Lossless hoặc VRAM Uncompressed. Chế độ này không làm giảm mức sử dụng bộ nhớ video; mức sử dụng giống với Lossless hoặc VRAM Uncompressed. - **VRAM Compressed:** Đây là chế độ nén mặc định và phổ biến nhất cho asset 3D. Kích thước trên đĩa được giảm xuống và mức sử dụng bộ nhớ video cũng giảm đáng kể (thường từ 4 đến 6 lần). Nên tránh dùng chế độ này cho 2D vì nó tạo ra các artifact dễ nhận thấy, đặc biệt với texture có độ phân giải thấp. - **VRAM Uncompressed:** Chỉ hữu ích cho các định dạng không thể nén, chẳng hạn như hình ảnh dấu phẩy động thô. - **Basis Universal:** Chế độ nén VRAM thay thế này mã hóa texture thành một định dạng có thể được chuyển mã sang hầu hết các định dạng nén GPU tại thời điểm tải. Cách này tạo ra các tệp rất nhỏ có sử dụng tính năng nén VRAM, nhưng đánh đổi bằng chất lượng thấp hơn so với VRAM Compressed và thời gian nén chậm. Mức sử dụng VRAM thường giống với VRAM Compressed. Basis Universal không hỗ trợ các định dạng hình ảnh dấu phẩy động (engine sẽ tự động chuyển về VRAM Compressed).

.. note::

    Ngay cả trong 3D, các texture "pixel art" cũng nên tắt tính năng nén VRAM vì nó sẽ ảnh hưởng tiêu cực đến hình thức của texture mà không cải thiện đáng kể hiệu suất do độ phân giải thấp.

Trong bảng này, mỗi trong 5 tùy chọn được mô tả cùng với ưu điểm và nhược điểm của chúng (|good| = tốt nhất, |bad| = kém nhất):

+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+
| Compress mode    | Lossless                      | Lossy                | VRAM Compressed                                      | VRAM Uncompressed      | Basis Universal                      |
+==================+===============================+======================+======================================================+========================+======================================+
| **Description**  | Stored as Lossless WebP / PNG | Stored as Lossy WebP | Stored as S3TC, BPTC or ETC2 depending on platform   | Stored as raw pixels   | Transcoded to VRAM Compressed format |
+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+
| **Size on disk** | |regular| Small               | |good| Very small    | |regular| Small                                      | |bad| Large            | |good| Very small                    |
+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+
| **Memory usage** | |bad| Large                   | |bad| Large          | |good| Small                                         | |bad| Large            | |good| Small                         |
+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+
| **Performance**  | |regular| Normal              | |regular| Normal     | |good| Fast                                          | |regular| Normal       | |good| Fast                          |
+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+
| **Quality loss** | |good| None                   | |regular| Slight     | |bad| Moderate                                       | |good| None            | |bad| Moderate                       |
+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+
| **Load time**    | |bad| Slow                    | |bad| Slow           | |good| Fast                                          | |regular| Normal       | |regular| Normal                     |
+------------------+-------------------------------+----------------------+------------------------------------------------------+------------------------+--------------------------------------+

.. |bad| image:: img/bad.png

.. |good| image:: img/good.png

.. |regular| image:: img/regular.png

Mức sử dụng bộ nhớ ước tính cho một texture RGBA8 đơn với mipmap được bật:

+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+
| Texture size  | Lossless            | Lossy               | VRAM Compressed     | VRAM Uncompressed   | Basis Universal     |
+===============+=====================+=====================+=====================+=====================+=====================+
| **128×128**   | |good| 85 KiB       | |good| 85 KiB       | |good| 21 KiB       | |good| 85 KiB       | |good| 21 KiB       |
+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+
| **256×256**   | |good| 341 KiB      | |good| 341 KiB      | |good| 85 KiB       | |good| 341 KiB      | |good| 85 KiB       |
+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+
| **512×512**   | |good| 1.33 MiB     | |good| 1.33 MiB     | |good| 341 KiB      | |good| 1.33 MiB     | |good| 341 KiB      |
+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+
| **1024×1024** | |regular| 5.33 MiB  | |regular| 5.33 MiB  | |good| 1.33 MiB     | |regular| 5.33 MiB  | |good| 1.33 MiB     |
+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+
| **2048×2048** | |bad| 21.33 MiB     | |bad| 21.33 MiB     | |regular| 5.33 MiB  | |bad| 21.33 MiB     | |regular| 5.33 MiB  |
+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+
| **4096×4096** | |bad| 85.33 MiB     | |bad| 85.33 MiB     | |bad| 21.33 MiB     | |bad| 85.33 MiB     | |bad| 21.33 MiB     |
+---------------+---------------------+---------------------+---------------------+---------------------+---------------------+

.. note::

    Trong bảng trên, mức sử dụng bộ nhớ sẽ giảm 25% đối với hình ảnh không có kênh alpha (RGB8). Mức sử dụng bộ nhớ sẽ tiếp tục giảm 25% đối với hình ảnh đã tắt mipmap.

Lưu ý rằng ở các độ phân giải lớn hơn, tác động của việc nén VRAM lớn hơn nhiều. Với tỷ lệ nén 4:1 (6:1 đối với texture không trong suốt với S3TC), nén VRAM thực tế cho phép texture lớn gấp đôi trên mỗi trục, trong khi vẫn sử dụng cùng lượng bộ nhớ trên GPU.

Nén VRAM cũng làm giảm băng thông bộ nhớ cần thiết để lấy mẫu texture, nhờ đó có thể tăng tốc quá trình render trong các trường hợp bị giới hạn bởi băng thông bộ nhớ (thường gặp trên đồ họa tích hợp và thiết bị di động). Kết hợp lại, các yếu tố này khiến nén VRAM trở thành yếu tố bắt buộc đối với game 3D sử dụng texture độ phân giải cao.

Bạn có thể xem trước texture chiếm bao nhiêu bộ nhớ bằng cách nhấp đúp vào texture trong dock FileSystem, sau đó xem trong Inspector:

.. figure:: img/importing_images_inspector_preview.webp
   :align: center
   :alt: Previewing a texture in the Inspector

   Previewing a texture in the Inspector. Credit: `Red Brick 03 - Poly Haven <https://polyhaven.com/a/red_brick_03>`__

Compress > High Quality
~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Nén texture VRAM chất lượng cao chỉ được hỗ trợ trong các renderer Forward+ và Mobile.

    Khi sử dụng renderer Compatibility, tùy chọn này luôn được xem là bị tắt.

Nếu được bật, sử dụng nén BPTC trên các nền tảng desktop và nén :abbr:`ASTC (Adaptive Scalable Texture Compression)` trên các nền tảng mobile. Khi sử dụng BPTC, BC7 được dùng cho texture SDR và BC6H được dùng cho texture HDR.

Nếu bị tắt (mặc định), sử dụng nén S3TC nhanh hơn nhưng chất lượng thấp hơn trên các nền tảng desktop và ETC2 trên các nền tảng mobile/web. Khi sử dụng S3TC, DXT1 (BC1) được dùng cho texture không trong suốt, còn DXT5 (BC3) được dùng cho texture trong suốt hoặc texture normal map (:abbr:`RGTC (Red-Green Texture Compression)`).

BPTC và ASTC hỗ trợ nén VRAM cho texture HDR, nhưng S3TC và ETC2 thì không (xem **HDR Compression** bên dưới).

Compress > HDR Compression
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Tùy chọn này chỉ có tác dụng với các texture được import dưới dạng HDR trong Godot (các tệp ``.hdr`` và ``.exr``).

Nếu được đặt thành **Disabled**, không bao giờ sử dụng nén VRAM cho texture HDR, bất kể chúng không trong suốt hay trong suốt. Thay vào đó, texture được chuyển đổi thành RGBE9995 (9-bit cho mỗi kênh + số mũ 5-bit = 32 bit trên mỗi pixel) để giảm mức sử dụng bộ nhớ so với định dạng ảnh half-float hoặc single-precision float.

Nếu được đặt thành **Opaque Only** (mặc định), chỉ sử dụng nén VRAM cho texture HDR không trong suốt. Điều này là do một hạn chế của các định dạng HDR, vì không có định dạng HDR được nén VRAM nào đồng thời hỗ trợ độ trong suốt.

Nếu được đặt thành **Always**, sẽ buộc sử dụng nén VRAM ngay cả với texture HDR có kênh alpha. Để thực hiện việc này, kênh alpha sẽ bị loại bỏ khi import.

Compress > Normal Map
~~~~~~~~~~~~~~~~~~~~~

Khi sử dụng texture làm normal map, chỉ cần các kênh đỏ và xanh lá. Vì các thuật toán nén texture thông thường tạo ra các artifact không đẹp khi dùng cho normal map, định dạng nén :abbr:`RGTC (Red-Green Texture Compression)` là lựa chọn phù hợp nhất cho dữ liệu này. Buộc tùy chọn này thành **Enable** sẽ khiến Godot import ảnh dưới dạng được nén bằng :abbr:`RGTC (Red-Green Texture Compression)`. Theo mặc định, tùy chọn này được đặt thành **Detect**. Điều đó có nghĩa là nếu texture được phát hiện đang được dùng làm normal map, nó sẽ được chuyển thành **Enable** và tự động reimport.

Lưu ý rằng việc nén :abbr:`RGTC (Red-Green Texture Compression)` ảnh hưởng đến ảnh normal map kết quả. Bạn sẽ phải điều chỉnh các custom shader sử dụng kênh xanh dương của normal map để tính đến điều này. Các shader material tích hợp sẵn đã bỏ qua kênh xanh dương trong normal map (bất kể nội dung thực tế của normal map).

Trong ví dụ bên dưới, normal map với nén :abbr:`RGTC (Red-Green Texture Compression)` có thể giữ lại chi tiết tốt hơn nhiều, đồng thời sử dụng cùng lượng bộ nhớ như một texture RGBA được nén VRAM tiêu chuẩn:

.. figure:: img/importing_images_normal_map_rgtc.webp
   :align: center
   :alt: Normal map with standard VRAM compression (left) and with RGTC VRAM compression (right)

   Normal map with standard VRAM compression (left) and with RGTC VRAM compression (right)

.. note::

  Godot yêu cầu normal map sử dụng các tọa độ X+, Y+ và Z+, được gọi là normal map kiểu OpenGL. Nếu bạn đã import một material được tạo để sử dụng với engine khác, nó có thể là kiểu DirectX. Trong trường hợp này, normal map cần được chuyển đổi bằng cách bật tùy chọn import **Normal Map Invert Y**.

  Có thể tìm thêm thông tin về normal map (bao gồm bảng thứ tự tọa độ cho các engine phổ biến) `here <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details>`__.

Compress > Channel Pack
~~~~~~~~~~~~~~~~~~~~~~~

Nếu được đặt thành **sRGB Friendly** (mặc định), ngăn không cho sử dụng định dạng màu RG vì định dạng này không hỗ trợ màu sRGB.

Nếu được đặt thành **Optimized**, cho phép sử dụng định dạng màu RG nếu texture không sử dụng kênh xanh dương.

Tùy chọn thứ ba **Normal Map (RG Channels)** *chỉ* khả dụng trong các texture dạng layer (:ref:`class_Cubemap`, :ref:`class_CubemapArray`, :ref:`class_Texture2DArray` và :ref:`class_Texture3D`). Tùy chọn này buộc tất cả layer của texture được import bằng định dạng màu RG, chỉ giữ lại các kênh đỏ và xanh lá. Nén :abbr:`RGTC (Red-Green Texture Compression)` có thể giữ lại chi tiết tốt hơn nhiều, đồng thời sử dụng cùng lượng bộ nhớ như một texture RGBA được nén VRAM tiêu chuẩn. Tùy chọn này chỉ có tác dụng với texture sử dụng chế độ nén **VRAM Compressed** hoặc **Basis Universal**.

.. _doc_importing_images_mipmaps:

Mipmaps > Generate
~~~~~~~~~~~~~~~~~~

Nếu được bật, các phiên bản nhỏ hơn của texture sẽ được tạo khi import. Ví dụ, texture 64×64 sẽ tạo 6 mipmap (32×32, 16×16, 8×8, 4×4, 2×2, 1×1). Điều này mang lại một số lợi ích:

- Texture sẽ không bị nhiễu hạt khi ở xa (trong 3D), hoặc khi được thu nhỏ do zoom camera hoặc scale của CanvasItem (trong 2D). - Hiệu năng sẽ được cải thiện nếu texture được hiển thị ở xa, vì việc lấy mẫu các phiên bản nhỏ hơn của texture gốc nhanh hơn và cần ít băng thông bộ nhớ hơn.

Nhược điểm của mipmap là chúng làm tăng mức sử dụng bộ nhớ khoảng 33%.

Bạn nên bật mipmap trong 3D. Tuy nhiên, trong 2D, chỉ nên bật tùy chọn này nếu dự án của bạn thực sự hưởng lợi rõ rệt từ việc bật mipmap. Nếu camera không bao giờ zoom out đáng kể, việc bật mipmap sẽ không mang lại lợi ích nhưng sẽ làm tăng mức sử dụng bộ nhớ.

Mipmaps > Limit
~~~~~~~~~~~~~~~

.. UPDATE: Chưa được triển khai. Khi Mipmaps > Limit được triển khai, hãy xóa cảnh báo .. này và xóa comment này.

.. warning::

    **Mipmaps > Limit** hiện chưa được triển khai và không có tác dụng khi thay đổi.

Nếu được đặt thành giá trị lớn hơn ``-1``, giới hạn số lượng mipmap tối đa có thể được tạo. Có thể giảm giá trị này nếu bạn không muốn texture trở nên có độ phân giải quá thấp ở khoảng cách cực xa, đổi lại sẽ có một chút nhiễu hạt.

Roughness > Mode
~~~~~~~~~~~~~~~~

Kênh màu được xem là roughness map trong texture này. Chỉ có tác dụng nếu **Roughness > Src Normal** không trống.

Roughness > Src Normal
~~~~~~~~~~~~~~~~~~~~~~

Đường dẫn đến texture được xem là normal map để lọc roughness khi import. Việc chỉ định texture này có thể giúp giảm nhẹ hiện tượng specular aliasing trong 3D.

Lọc roughness khi import chỉ được sử dụng trong quá trình render 3D, không phải 2D.

Process > Fix Alpha Border
~~~~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này đặt các pixel có cùng màu với vùng xung quanh vào phần chuyển tiếp từ vùng trong suốt sang vùng không trong suốt. Đối với texture được hiển thị bằng bilinear filtering, điều này giúp giảm hiệu ứng đường viền khi export ảnh từ image editor.

.. image:: img/fixedborder.png

Bạn nên để tùy chọn này bật (như mặc định), trừ khi nó gây ra sự cố với một ảnh cụ thể.

Process > Premult Alpha
~~~~~~~~~~~~~~~~~~~~~~~

Một cách thay thế cho việc sửa các đường viền bị tối bằng **Fix Alpha Border** là sử dụng alpha premultiplied. Bằng cách bật tùy chọn này, texture sẽ được chuyển đổi sang định dạng đó. Texture alpha premultiplied yêu cầu các material cụ thể để được hiển thị chính xác:

- Trong 2D, cần tạo một :ref:`class_CanvasItemMaterial` và cấu hình để sử dụng chế độ blend **Premultiplied Alpha** trên các CanvasItem sử dụng texture này. Trong :ref:`custom canvas item shaders <doc_canvas_item_shader>`, nên sử dụng ``render_mode blend_premul_alpha;``. - Trong 3D, cần tạo một :ref:`class_BaseMaterial3D` và cấu hình để sử dụng chế độ blend **Premult Alpha** trên các material sử dụng texture này. Trong :ref:`custom spatial shaders <doc_spatial_shader>`, nên sử dụng ``render_mode blend_premul_alpha;``.

Process > Normal Map Invert Y
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot yêu cầu normal map sử dụng các tọa độ X+, Y+ và Z+, được gọi là normal map kiểu OpenGL. Nếu bạn đã import một material được tạo để sử dụng với engine khác, nó có thể là kiểu DirectX. Trong trường hợp này, normal map cần được chuyển đổi bằng cách bật tùy chọn import **Normal Map Invert Y**.

Có thể tìm thêm thông tin về normal map (bao gồm bảng thứ tự tọa độ cho các engine phổ biến) `here <http://wiki.polycount.com/wiki/Normal_Map_Technical_Details>`__.

Process > HDR as sRGB
~~~~~~~~~~~~~~~~~~~~~

Một số ảnh HDR bạn tìm thấy trên mạng có thể bị lỗi và chứa dữ liệu màu sRGB (thay vì dữ liệu màu tuyến tính). Bạn không nên sử dụng những tệp đó. Nếu nhất thiết phải dùng, việc bật tùy chọn này sẽ khiến chúng hiển thị chính xác.

.. warning::

    Bật **HDR as sRGB** trên các ảnh HDR được định dạng đúng sẽ khiến ảnh kết quả quá tối, vì vậy hãy để tùy chọn này tắt nếu không chắc chắn.

Process > HDR Clamp Exposure
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Một số ảnh panorama HDR bạn tìm thấy trên mạng có thể chứa các pixel cực kỳ sáng do được chụp từ nguồn thực tế mà không thực hiện clipping.

Mặc dù các ảnh panorama HDR này chính xác với thực tế, điều này có thể khiến radiance map do Godot tạo ra chứa các điểm lấp lánh khi được dùng làm background sky. Hiện tượng này có thể thấy trong các phản chiếu của material (thậm chí trong những trường hợp đặc biệt, trên cả material rough). Bật **HDR Clamp Exposure** có thể giải quyết vấn đề này bằng công thức clamp thông minh, không tạo ra clipping *nhìn thấy được* – glow vẫn tiếp tục hoạt động khi nhìn vào background sky.

Process > Size Limit
~~~~~~~~~~~~~~~~~~~~

Nếu được đặt thành giá trị lớn hơn ``0``, kích thước texture sẽ bị giới hạn khi import ở mức nhỏ hơn hoặc bằng giá trị được chỉ định tại đây. Đối với texture không vuông, giới hạn kích thước áp dụng cho chiều dài hơn, còn chiều ngắn hơn được scale để giữ nguyên tỷ lệ khung hình. Việc thay đổi kích thước được thực hiện bằng nội suy cubic.

Có thể dùng tùy chọn này để giảm mức sử dụng bộ nhớ mà không ảnh hưởng đến ảnh nguồn, hoặc tránh các sự cố khi texture không hiển thị trên các nền tảng mobile/web (vì những nền tảng này thường không thể hiển thị texture lớn hơn 4096×4096).

.. _doc_importing_images_detect_3d_compress_to:

Detect 3D > Compress To
~~~~~~~~~~~~~~~~~~~~~~~

Tùy chọn này thay đổi tùy chọn :ref:`doc_importing_images_compress_mode` được sử dụng khi texture được phát hiện là đang được dùng trong 3D.

Việc thay đổi tùy chọn import này chỉ có hiệu lực nếu texture được phát hiện là đang được sử dụng trong 3D. Việc chuyển tùy chọn này thành **Disabled** rồi reimport sẽ không thay đổi chế độ nén hiện có trên texture (nếu texture được phát hiện là đang được sử dụng trong 3D), nhưng chọn **VRAM Compressed** hoặc **Basis Universal** thì có.

SVG > Scale
~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng cho hình ảnh SVG.*

Scale mà SVG sẽ được render, trong đó ``1.0`` là kích thước thiết kế ban đầu. Giá trị cao hơn sẽ tạo ra hình ảnh lớn hơn. Lưu ý rằng không giống như font oversampling, tùy chọn này ảnh hưởng đến kích thước vật lý mà SVG được render trong 2D. Xem thêm **Editor > Scale With Editor Scale** bên dưới.

.. _doc_importing_images_editor_import_options:

Editor > Scale With Editor Scale
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng cho hình ảnh SVG.*

Nếu là true, scale hình ảnh đã import để khớp với hệ số scale hiển thị của editor. Bạn nên bật tùy chọn này cho icon của editor plugin và icon của custom class, nhưng nên để tắt trong các trường hợp khác.

Editor > Convert Colors With Editor Theme
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tùy chọn này chỉ khả dụng cho hình ảnh SVG.*

Nếu được chọn, tùy chọn này sẽ chuyển đổi màu của hình ảnh đã import để khớp với bảng màu icon và font của editor. Điều này giả định rằng hình ảnh sử dụng chính xác cùng màu với
:ref:`Godot's own color palette for editor icons <doc_editor_icons>`, with the
file nguồn được thiết kế cho theme editor tối. Bạn nên bật tùy chọn này cho icon của editor plugin và icon của custom class, nhưng nên để tắt trong các trường hợp khác.

.. _doc_importing_images_svg_text:

Import hình ảnh SVG có văn bản
------------------------------

Do thư viện SVG được sử dụng trong Godot không hỗ trợ rasterize văn bản có trong hình ảnh SVG, trước tiên bạn phải chuyển văn bản thành path. Nếu không, văn bản sẽ không xuất hiện trong hình ảnh đã rasterize.

Có hai cách để thực hiện việc này theo phương thức không phá hủy (non-destructive), nhờ đó bạn vẫn có thể tiếp tục chỉnh sửa văn bản gốc sau này:

- Chọn đối tượng văn bản trong Inkscape, sau đó duplicate đối tượng tại đúng vị trí bằng cách nhấn
  :kbd:`Ctrl + D` and use **Path > Object to Path**. Hide the original text
  đối tượng sau đó bằng dock **Layers and Objects**. - Sử dụng command line của Inkscape để export một SVG từ một file SVG khác với văn bản đã được chuyển thành path:

::

    inkscape --export-text-to-path --export-filename svg_with_text_converted_to_path.svg svg_with_text.svg

Các phương pháp hay nhất
------------------------

Hỗ trợ kích thước texture độ phân giải cao trong 2D mà không có artifact
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để hỗ trợ :ref:`multiple resolutions <doc_multiple_resolutions>` với hình ảnh sắc nét ở độ phân giải cao, bạn cần sử dụng hình ảnh nguồn độ phân giải cao (phù hợp với độ phân giải cao nhất mà bạn muốn hỗ trợ mà không bị mờ; trong các game desktop hiện đại, độ phân giải này thường là 4K).

Có 2 cách để thực hiện:

- Sử dụng độ phân giải cơ sở cao trong project settings (chẳng hạn 4K), sau đó sử dụng texture ở scale gốc. Đây là cách dễ hơn. - Sử dụng độ phân giải cơ sở thấp trong project settings (chẳng hạn 1080p), sau đó downscale texture khi sử dụng. Cách này thường khó hơn và có thể khiến nhiều phép tính trong script trở nên tẻ nhạt, vì vậy cách được mô tả ở trên được khuyến nghị hơn.

Sau khi thực hiện việc này, bạn có thể nhận thấy texture trở nên nhiễu hạt ở các độ phân giải viewport thấp hơn. Để khắc phục, hãy bật **Mipmaps** trên các texture được sử dụng trong 2D tại dock Import. Việc này sẽ làm tăng mức sử dụng bộ nhớ.

Việc bật mipmap cũng có thể khiến texture trông mờ hơn, nhưng bạn có thể làm texture sắc nét hơn (đánh đổi bằng một phần nhiễu hạt) bằng cách đặt **Rendering > Textures > Default Filters > Texture Mipmap Bias** thành một giá trị âm.

Sử dụng kích thước texture phù hợp trong 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù không có khuyến nghị "một kích thước phù hợp cho mọi trường hợp", dưới đây là một số khuyến nghị chung khi chọn kích thước texture trong 3D:

- Kích thước của texture nên được điều chỉnh để có mật độ texel nhất quán so với các object xung quanh. Mặc dù không thể đảm bảo hoàn toàn khi chỉ sử dụng kích thước texture lũy thừa của hai, thông thường vẫn có thể duy trì chi tiết texture khá nhất quán trong toàn bộ một cảnh 3D. - Object càng nhỏ trên màn hình thì texture của nó càng nên nhỏ. Ví dụ, một cái cây chỉ xuất hiện ở hậu cảnh không cần độ phân giải texture cao như các object khác mà người chơi có thể đi đến gần. - Khuyến nghị sử dụng kích thước texture lũy thừa của hai, nhưng đây không phải là yêu cầu bắt buộc. Texture không nhất thiết phải vuông – các kích thước như 1024×512 vẫn được chấp nhận. - Việc sử dụng kích thước texture lớn có hiệu quả giảm dần, dù làm tăng mức sử dụng bộ nhớ và thời gian tải. Hầu hết game 3D hiện đại không sử dụng phong cách pixel art thường dùng texture 2048×2048 ở mức trung bình, cùng với 1024×1024 và 512×512 cho các texture phủ những bề mặt nhỏ hơn. - Khi làm việc với các vật liệu dựa trên đặc tính vật lý trong 3D, bạn có thể giảm mức sử dụng bộ nhớ và kích thước file mà không ảnh hưởng quá nhiều đến chất lượng bằng cách sử dụng độ phân giải thấp hơn cho một số texture map nhất định. Cách này đặc biệt hiệu quả với các texture chỉ có chi tiết tần số thấp (chẳng hạn normal map cho texture tuyết).

Nếu bạn có quyền kiểm soát cách tạo các model 3D, những mẹo sau cũng đáng để tìm hiểu:

- Khi làm việc với các model 3D phần lớn có tính đối xứng, bạn có thể sử dụng UV được mirror để tăng gấp đôi mật độ texel hiệu dụng. Tuy nhiên, cách này có thể trông không tự nhiên khi được sử dụng trên khuôn mặt người. - Khi làm việc với các model 3D sử dụng phong cách low-poly và màu đơn sắc, bạn có thể dùng vertex color thay cho texture để thể hiện màu sắc trên các bề mặt của model.

.. seealso::

    Có thể load và save hình ảnh tại runtime bằng cách sử dụng
    :ref:`runtime file loading and saving <doc_runtime_file_loading_and_saving_images>`,
    bao gồm cả từ một project đã export.
