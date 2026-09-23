.. _doc_resolution_scaling:

Tỷ lệ độ phân giải
==================

.. Images on this page were generated using the project below:
.. https://github.com/Calinou/godot-antialiasing-comparison

Tại sao nên sử dụng tỷ lệ độ phân giải?
---------------------------------------

Với độ phức tạp kết xuất ngày càng tăng của các trò chơi hiện đại, việc kết xuất ở độ phân giải gốc không còn luôn khả thi, đặc biệt trên các GPU cấp thấp.

Tỷ lệ độ phân giải là một trong những cách trực tiếp nhất để tác động đến yêu cầu GPU của một cảnh. Trong những cảnh bị giới hạn bởi GPU (thay vì CPU), việc giảm tỷ lệ độ phân giải có thể cải thiện hiệu năng đáng kể. Tỷ lệ độ phân giải đặc biệt quan trọng trên GPU di động, nơi ngân sách hiệu năng và năng lượng bị giới hạn.

Mặc dù tỷ lệ độ phân giải là một công cụ quan trọng, hãy nhớ rằng tỷ lệ độ phân giải không nhằm thay thế cho việc giảm các thiết lập đồ họa trên phần cứng cấp thấp. Hãy cân nhắc cho phép người dùng điều chỉnh cả tỷ lệ độ phân giải và các thiết lập đồ họa trong menu trong trò chơi.

.. seealso::

    Bạn có thể so sánh các chế độ và hệ số tỷ lệ độ phân giải trong thực tế bằng `dự án demo Khử răng cưa 3D <https://github.com/godotengine/godot-demo-projects/tree/master/3d/antialiasing>`__.

.. note::

    Hiện tại, việc thay đổi tỷ lệ độ phân giải không khả dụng cho kết xuất 2D, nhưng bạn có thể mô phỏng bằng chế độ kéo giãn ``viewport``. Xem :ref:`doc_multiple_resolutions` để biết thêm thông tin.

Các tùy chọn tỷ lệ độ phân giải
-------------------------------

Trong phần **Rendering > Scaling 3D** của Project Settings nâng cao, bạn có thể tìm thấy một số tùy chọn tỷ lệ độ phân giải 3D:

Chế độ tỷ lệ
~~~~~~~~~~~~

- **Bilinear:** Bộ lọc bilinear tiêu chuẩn (mặc định). Bộ lọc này được sử dụng dự phòng khi renderer hiện tại không hỗ trợ FSR 1.0 hoặc FSR 2.2. *Có sẵn trong tất cả renderer.*
- **FSR 1.0:** `AMD FidelityFX Super Resolution 1.0 <https://gpuopen.com/fidelityfx-superresolution/>`__. Chậm hơn nhưng chất lượng cao hơn so với tỷ lệ bilinear. Trên các GPU rất chậm, chi phí của FSR1 có thể quá cao, khiến việc sử dụng nó không đáng so với tỷ lệ bilinear. *Chỉ khả dụng khi sử dụng Forward+ renderer.*
- **FSR 2.2:** AMD FidelityFX Super Resolution 2.2 (từ Godot 4.2). Chậm nhất nhưng chất lượng còn cao hơn so với FSR1 và tỷ lệ bilinear. Trên các GPU chậm, chi phí của FSR2 có thể quá cao, khiến việc sử dụng nó không đáng so với tỷ lệ bilinear hoặc FSR1. Để đạt hiệu năng tương đương với FSR2 bằng FSR1, bạn cần sử dụng hệ số tỷ lệ độ phân giải thấp hơn. *Chỉ khả dụng khi sử dụng Forward+ renderer.*

Dưới đây là các hình ảnh so sánh giữa độ phân giải gốc, tỷ lệ bilinear với tỷ lệ độ phân giải 50%, FSR1 và tỷ lệ FSR2 với tỷ lệ độ phân giải 50%:

.. image:: img/resolution_scaling_bilinear_0.5.png

.. image:: img/resolution_scaling_fsr1_0.5.png

.. image:: img/resolution_scaling_fsr2_0.5.webp

Tỷ lệ nâng độ phân giải FSR1 hoạt động tốt nhất khi kết hợp với một dạng khử răng cưa khác. Trong trường hợp này, nên sử dụng khử răng cưa tạm thời (TAA) hoặc khử răng cưa đa mẫu (MSAA), vì FXAA không bổ sung thông tin tạm thời và làm hình ảnh bị mờ hơn.

Mặt khác, FSR2 cung cấp khử răng cưa tạm thời riêng. Điều này có nghĩa là bạn không cần bật các phương pháp khử răng cưa khác để hình ảnh đầu ra trông mượt mà. Thiết lập project **Use TAA** sẽ bị bỏ qua khi FSR2 được sử dụng làm phương pháp tỷ lệ 3D, vì khử răng cưa tạm thời của FSR2 được ưu tiên.

Đây là cùng một phép so sánh, nhưng với 4× MSAA được bật trên tất cả hình ảnh:

.. image:: img/resolution_scaling_bilinear_msaa_4x_0.5.png

.. image:: img/resolution_scaling_fsr1_msaa_4x_0.5.png

.. image:: img/resolution_scaling_fsr2_msaa_4x_0.5.webp

Hãy chú ý cách việc nâng độ phân giải các cạnh của FSR1 trở nên thuyết phục hơn nhiều sau khi bật 4× MSAA. Tuy nhiên, FSR2 không được hưởng lợi nhiều từ việc bật MSAA vì bản thân nó đã thực hiện khử răng cưa tạm thời.

Tỷ lệ kết xuất
~~~~~~~~~~~~~~

Thiết lập **Rendering > Scaling 3D > Scale** điều chỉnh tỷ lệ độ phân giải. ``1.0`` biểu thị tỷ lệ độ phân giải đầy đủ, trong đó độ phân giải kết xuất 3D khớp với độ phân giải kết xuất 2D. Có thể sử dụng các tỷ lệ độ phân giải *thấp hơn* ``1.0`` để tăng tốc kết xuất, đổi lại hình ảnh cuối cùng sẽ mờ hơn và có nhiều răng cưa hơn.

Có thể điều chỉnh tỷ lệ kết xuất trong runtime bằng cách thay đổi thuộc tính ``scaling_3d_scale`` trên một node :ref:`class_Viewport`.

Có thể sử dụng các tỷ lệ độ phân giải *cao hơn* ``1.0`` để khử răng cưa bằng supersampling (SSAA). Cách này cung cấp khả năng khử răng cưa với chi phí hiệu năng *rất* cao và **không được khuyến nghị** cho hầu hết trường hợp sử dụng. Xem :ref:`doc_3d_antialiasing` để biết thêm thông tin.

Các bảng bên dưới liệt kê những độ phân giải màn hình phổ biến, độ phân giải kết xuất 3D tương ứng và số megapixel cần được kết xuất trong mỗi frame tùy theo tùy chọn tỷ lệ kết xuất. Các hàng trong mỗi bảng được sắp xếp từ nhanh nhất đến chậm nhất.

.. note::

    Tỷ lệ độ phân giải được xác định theo cơ sở **trên từng trục**. Ví dụ, điều này có nghĩa là giảm một nửa hệ số tỷ lệ độ phân giải sẽ giảm số megapixel được kết xuất mỗi frame theo hệ số 4, không phải 2. Vì vậy, các hệ số tỷ lệ độ phân giải rất thấp hoặc rất cao có thể tác động đến hiệu năng nhiều hơn dự kiến.

**1920×1080 (Full HD)**

+--------------------------+--------------------------+-----------------------------------+
| Hệ số tỷ lệ độ phân giải | Độ phân giải kết xuất 3D | Megapixel được kết xuất mỗi frame |
+==========================+==========================+===================================+
| ``0.50``                 | 960×540                  | 0.52 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.67``                 | 1286×723                 | 0.93 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.75``                 | 1440×810                 | 1.17 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.85``                 | 1632×918                 | 1.50 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``1.00`` **(gốc)**       | **1920×1080**            | **2.07 MPix**                     |
+--------------------------+--------------------------+-----------------------------------+
| ``1.33`` (siêu lấy mẫu)  | 2553×1436                | 3.67 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``1.50`` (siêu lấy mẫu)  | 2880×1620                | 4.67 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``2.00`` (siêu lấy mẫu)  | 3840×2160                | 8.29 MPix                         |
+--------------------------+--------------------------+-----------------------------------+

**2560×1440 (QHD)**

+--------------------------+--------------------------+-----------------------------------+
| Hệ số tỷ lệ độ phân giải | Độ phân giải kết xuất 3D | Megapixel được kết xuất mỗi frame |
+==========================+==========================+===================================+
| ``0.50``                 | 1280×720                 | 0.92 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.67``                 | 1715×964                 | 1.65 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.75``                 | 1920×1080                | 2.07 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.85``                 | 2176×1224                | 2.66 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``1.00`` **(gốc)**       | **2560×1440**            | **3.69 MPix**                     |
+--------------------------+--------------------------+-----------------------------------+
| ``1.33`` (siêu lấy mẫu)  | 3404×1915                | 6.52 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``1.50`` (siêu lấy mẫu)  | 3840×2160                | 8.29 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``2.00`` (siêu lấy mẫu)  | 5120×2880                | 14.75 MPix                        |
+--------------------------+--------------------------+-----------------------------------+

**3840×2160 (Ultra HD "4K")**

+--------------------------+--------------------------+-----------------------------------+
| Hệ số tỷ lệ độ phân giải | Độ phân giải kết xuất 3D | Megapixel được kết xuất mỗi frame |
+==========================+==========================+===================================+
| ``0.50``                 | 1920×1080                | 2.07 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.67``                 | 2572×1447                | 3.72 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.75``                 | 2880×1620                | 4.67 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``0.85``                 | 3264×1836                | 5.99 MPix                         |
+--------------------------+--------------------------+-----------------------------------+
| ``1.00`` **(gốc)**       | **3840×2160**            | **8.29 MPix**                     |
+--------------------------+--------------------------+-----------------------------------+
| ``1.33`` (siêu lấy mẫu)  | 5107×2872                | 14.67 MPix                        |
+--------------------------+--------------------------+-----------------------------------+
| ``1.50`` (siêu lấy mẫu)  | 5760×3240                | 18.66 MPix                        |
+--------------------------+--------------------------+-----------------------------------+
| ``2.00`` (siêu lấy mẫu)  | 7680×4320                | 33.18 MPix                        |
+--------------------------+--------------------------+-----------------------------------+

Độ sắc nét FSR
~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng trong trình kết xuất Forward+, không khả dụng trong trình kết xuất Mobile hoặc Compatibility.*

Khi sử dụng chế độ масштаб FSR1 hoặc FSR2, bạn có thể điều khiển độ sắc nét bằng thiết lập dự án nâng cao **Rendering > Scaling 3D > FSR Sharpness**.

Cường độ được đảo ngược so với hầu hết các thanh trượt độ sắc nét khác: các giá trị *thấp hơn* sẽ tạo ra hình ảnh cuối sắc nét hơn, trong khi các giá trị *cao hơn* sẽ *giảm* tác động của bộ lọc tăng độ sắc nét. ``0.0`` là mức sắc nét nhất, còn ``2.0`` là mức ít sắc nét nhất. Giá trị mặc định ``0.2`` tạo sự cân bằng giữa việc giữ lại độ sắc nét của hình ảnh gốc và tránh hiện tượng răng cưa bổ sung do tăng độ sắc nét quá mức.

.. note::

    Nếu muốn sử dụng tính năng tăng độ sắc nét khi kết xuất ở độ phân giải gốc, hiện tại Godot không cho phép sử dụng riêng thành phần tăng độ sắc nét của FSR1 (RCAS) khỏi thành phần nâng cấp (EASU).

    Để khắc phục, bạn có thể đặt tỷ lệ kết xuất 3D thành ``0.99``, đặt chế độ scaling thành **FSR 1.0**, rồi điều chỉnh độ sắc nét FSR theo nhu cầu. Cách này cho phép sử dụng FSR1 trong khi kết xuất ở độ phân giải gần với độ phân giải gốc.

    Ngoài ra, bạn có thể đặt chế độ scaling thành **FSR 2.2**, với tỷ lệ kết xuất 3D được đặt thành ``1.0`` nếu GPU còn đủ công suất. Cách này cũng cung cấp tính năng khử răng cưa theo thời gian chất lượng cao. Thiết lập **FSR Sharpness** vẫn hoạt động trong trường hợp này.

.. _doc_resolution_scaling_mipmap_bias:

Độ lệch Mipmap
~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng trong trình kết xuất Forward+ và Mobile, không khả dụng trong trình kết xuất Compatibility.*

Godot tự động sử dụng độ lệch mipmap âm cho texture khi tỷ lệ độ phân giải 3D được đặt thấp hơn ``1.0``. Điều này giúp giữ lại chi tiết của texture tốt hơn, đổi lại các texture có nhiều chi tiết sẽ có vẻ nhiễu hạt.

Độ lệch LOD của texture hiện ảnh hưởng đến cả kết xuất 2D và 3D theo cùng một cách. Tuy nhiên, hãy lưu ý rằng nó chỉ có tác dụng với các texture đã bật mipmap. Texture được sử dụng trong 2D không bật mipmap theo mặc định, nghĩa là chỉ kết xuất 3D bị ảnh hưởng, trừ khi bạn đã bật mipmap cho texture 2D trong dock Import.

Công thức dùng để xác định độ lệch mipmap của texture là: ``log2f(min(scaling_3d_scale, 1.0)) + custom_texture_mipmap_bias``

Để bù lại hiện tượng mờ do một số phương pháp khử răng cưa gây ra, Godot cũng thêm độ lệch ``-0.25`` khi FXAA được bật và độ lệch ``-0.5`` khi TAA được bật. Nếu cả hai được bật cùng lúc, độ lệch ``-0.75`` sẽ được sử dụng. Độ lệch mipmap này được áp dụng *trước* độ lệch do scaling độ phân giải, vì vậy nó không thay đổi theo tỷ lệ độ phân giải.

Có thể thay đổi thủ công độ lệch LOD của texture bằng cách điều chỉnh thiết lập dự án nâng cao **Rendering > Textures > Default Filters > Texture Mipmap Bias**. Bạn cũng có thể thay đổi nó trong runtime trên :ref:`Viewports <class_Viewport>` bằng cách điều chỉnh thuộc tính ``texture_mipmap_bias``.

.. warning::

    Việc điều chỉnh thủ công độ lệch LOD của mipmap có thể hữu ích trong một số trường hợp, nhưng cần thực hiện cẩn thận để tránh khiến hình ảnh cuối bị nhiễu hạt khi chuyển động.

    Độ lệch LOD mipmap *âm* cũng có thể làm giảm hiệu năng do phải lấy mẫu các mip có độ phân giải cao hơn ở khoảng cách xa hơn. Giá trị khuyến nghị cho một offset thủ công nằm trong khoảng từ ``-0.5`` đến ``0.0``.

    Độ lệch LOD mipmap *dương* sẽ khiến các texture được mipmap trông mờ hơn mức mong muốn. Điều này có thể cải thiện hiệu năng đôi chút, nhưng nhìn chung không được khuyến nghị vì mức suy giảm chất lượng hình ảnh thường không đáng để đổi lấy phần hiệu năng tăng thêm.

Ví dụ dưới đây cho thấy một trường hợp cực đoan, với độ lệch LOD mipmap là ``-1.0`` và anisotropic filtering bị vô hiệu hóa để sự khác biệt dễ nhận thấy hơn:

.. image:: img/resolution_scaling_texture_mipmap_bias_comparison.png

Khắc phục sự cố
---------------

Hiệu năng không tăng nhiều khi giảm tỷ lệ độ phân giải
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu hiệu năng không tăng nhiều khi giảm tỷ lệ độ phân giải xuống một giá trị như ``0.5``, có thể nút thắt hiệu năng nằm ở nơi khác trong scene của bạn. Ví dụ, scene của bạn có thể có quá nhiều draw call, dẫn đến nút thắt CPU. Tương tự, có thể bạn đã bật quá nhiều hiệu ứng đồ họa khiến GPU không thể xử lý (chẳng hạn như SDFGI, SSAO hoặc SSR).

Xem các hướng dẫn :ref:`doc_performance` để biết thêm thông tin.
