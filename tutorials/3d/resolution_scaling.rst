.. _doc_resolution_scaling:

Tỷ lệ độ phân giải
==================

.. Hình ảnh trên trang này được tạo bằng dự án dưới đây: .. https://github.com/Calinou/godot-antialiasing-comparison

Tại sao nên sử dụng tỷ lệ độ phân giải?
---------------------------------------

Với độ phức tạp kết xuất ngày càng tăng của các game hiện đại, việc kết xuất ở độ phân giải gốc không còn khả thi trong mọi trường hợp, đặc biệt là trên các GPU cấp thấp.

Tỷ lệ độ phân giải là một trong những cách trực tiếp nhất để tác động đến yêu cầu GPU của một scene. Trong các scene bị giới hạn bởi GPU (thay vì CPU), việc giảm tỷ lệ độ phân giải có thể cải thiện hiệu năng đáng kể. Tỷ lệ độ phân giải đặc biệt quan trọng trên GPU di động, nơi ngân sách hiệu năng và điện năng bị giới hạn.

Mặc dù tỷ lệ độ phân giải là một công cụ quan trọng, hãy nhớ rằng tỷ lệ độ phân giải không được thiết kế để thay thế cho việc giảm cài đặt đồ họa trên phần cứng cấp thấp. Hãy cân nhắc cung cấp cả tỷ lệ độ phân giải và cài đặt đồ họa trong các menu trong game.

.. seealso::

    Bạn có thể so sánh trực tiếp các chế độ và hệ số tỷ lệ độ phân giải bằng dự án demo `3D Antialiasing <https://github.com/godotengine/godot-demo-projects/tree/master/3d/antialiasing>`__.

.. note::

    Hiện tại, tỷ lệ độ phân giải chưa khả dụng cho kết xuất 2D, nhưng có thể mô phỏng bằng chế độ stretch ``viewport``. Xem :ref:`doc_multiple_resolutions` để biết thêm thông tin.

Các tùy chọn tỷ lệ độ phân giải
-------------------------------

Trong phần **Rendering > Scaling 3D** của Advanced Project Settings, bạn có thể tìm thấy một số tùy chọn cho tỷ lệ độ phân giải 3D:

Chế độ tỷ lệ
~~~~~~~~~~~~

- **Bilinear:** Bộ lọc bilinear tiêu chuẩn (mặc định). Chế độ này được dùng làm phương án dự phòng khi renderer hiện tại không hỗ trợ FSR 1.0 hoặc FSR 2.2. *Khả dụng trong tất cả renderer.* - **FSR 1.0:** `AMD FidelityFX Super Resolution 1.0 <https://gpuopen.com/fidelityfx-superresolution/>`__. Chậm hơn nhưng chất lượng cao hơn so với tỷ lệ bilinear. Trên các GPU rất chậm, chi phí của FSR1 có thể quá cao và không đáng để sử dụng thay cho tỷ lệ bilinear. *Chỉ khả dụng khi sử dụng renderer Forward+.* - **FSR 2.2:** AMD FidelityFX Super Resolution 2.2 (từ Godot 4.2). Chậm nhất nhưng chất lượng còn cao hơn so với FSR1 và tỷ lệ bilinear. Trên các GPU chậm, chi phí của FSR2 có thể quá cao và không đáng để sử dụng thay cho tỷ lệ bilinear hoặc FSR1. Để đạt hiệu năng tương đương FSR2 bằng FSR1, bạn cần sử dụng hệ số tỷ lệ độ phân giải thấp hơn. *Chỉ khả dụng khi sử dụng renderer Forward+.*

Dưới đây là các hình ảnh so sánh giữa độ phân giải gốc, tỷ lệ bilinear với tỷ lệ độ phân giải 50%, FSR1 và tỷ lệ FSR2 với tỷ lệ độ phân giải 50%:

.. image:: img/resolution_scaling_bilinear_0.5.png

.. image:: img/resolution_scaling_fsr1_0.5.png

.. image:: img/resolution_scaling_fsr2_0.5.webp

Upscaling bằng FSR1 hoạt động tốt nhất khi kết hợp với một hình thức antialiasing khác. Trong trường hợp này, nên sử dụng temporal antialiasing (TAA) hoặc multisample antialiasing (MSAA), vì FXAA không bổ sung thông tin theo thời gian và khiến hình ảnh bị mờ hơn.

Mặt khác, FSR2 cung cấp temporal antialiasing riêng. Điều này có nghĩa là bạn không cần bật các phương pháp antialiasing khác để hình ảnh đầu ra trông mượt mà. Cài đặt project **Use TAA** sẽ bị bỏ qua khi FSR2 được sử dụng làm phương pháp tỷ lệ 3D, vì temporal antialiasing của FSR2 được ưu tiên.

Dưới đây là cùng phép so sánh đó, nhưng với 4× MSAA được bật trên tất cả hình ảnh:

.. image:: img/resolution_scaling_bilinear_msaa_4x_0.5.png

.. image:: img/resolution_scaling_fsr1_msaa_4x_0.5.png

.. image:: img/resolution_scaling_fsr2_msaa_4x_0.5.webp

Lưu ý rằng việc upscaling các cạnh của FSR1 trở nên thuyết phục hơn nhiều khi bật 4× MSAA. Tuy nhiên, FSR2 không hưởng lợi nhiều từ việc bật MSAA vì bản thân nó đã thực hiện temporal antialiasing.

Tỷ lệ kết xuất
~~~~~~~~~~~~~~

Cài đặt **Rendering > Scaling 3D > Scale** điều chỉnh tỷ lệ độ phân giải. ``1.0`` đại diện cho tỷ lệ độ phân giải đầy đủ, trong đó độ phân giải kết xuất 3D khớp với độ phân giải kết xuất 2D. Có thể sử dụng các tỷ lệ độ phân giải *thấp hơn* ``1.0`` để tăng tốc kết xuất, đổi lại hình ảnh cuối cùng sẽ mờ hơn và có nhiều aliasing hơn.

Có thể điều chỉnh tỷ lệ kết xuất tại runtime bằng cách thay đổi thuộc tính ``scaling_3d_scale`` trên một node :ref:`class_Viewport`.

Có thể sử dụng các tỷ lệ độ phân giải *cao hơn* ``1.0`` cho supersample antialiasing (SSAA). Cách này cung cấp antialiasing với chi phí hiệu năng *rất* cao và **không được khuyến nghị** cho hầu hết trường hợp sử dụng. Xem :ref:`doc_3d_antialiasing` để biết thêm thông tin.

Các bảng dưới đây liệt kê những độ phân giải màn hình phổ biến, độ phân giải kết xuất 3D tương ứng và số megapixel cần được kết xuất trong mỗi frame tùy theo tùy chọn tỷ lệ kết xuất. Các hàng được sắp xếp từ nhanh nhất đến chậm nhất trong mỗi bảng.

.. note::

    Tỷ lệ độ phân giải được xác định theo **từng trục**. Ví dụ, điều này có nghĩa là giảm một nửa hệ số tỷ lệ độ phân giải sẽ giảm số megapixel được kết xuất mỗi frame xuống 4 lần, không phải 2 lần. Vì vậy, các hệ số tỷ lệ độ phân giải rất thấp hoặc rất cao có thể tác động đến hiệu năng nhiều hơn dự kiến.

**1920×1080 (Full HD)**

+--------------------------+-------------------------+-------------------------------+
| Resolution scale factor  | 3D rendering resolution | Megapixels rendered per frame |
+==========================+=========================+===============================+
| ``0.50``                 | 960×540                 | 0.52 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.67``                 | 1286×723                | 0.93 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.75``                 | 1440×810                | 1.17 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.85``                 | 1632×918                | 1.50 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``1.00`` **(native)**    | **1920×1080**           | **2.07 MPix**                 |
+--------------------------+-------------------------+-------------------------------+
| ``1.33`` (supersampling) | 2553×1436               | 3.67 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``1.50`` (supersampling) | 2880×1620               | 4.67 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``2.00`` (supersampling) | 3840×2160               | 8.29 MPix                     |
+--------------------------+-------------------------+-------------------------------+

**2560×1440 (QHD)**

+--------------------------+-------------------------+-------------------------------+
| Resolution scale factor  | 3D rendering resolution | Megapixels rendered per frame |
+==========================+=========================+===============================+
| ``0.50``                 | 1280×720                | 0.92 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.67``                 | 1715×964                | 1.65 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.75``                 | 1920×1080               | 2.07 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.85``                 | 2176×1224               | 2.66 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``1.00`` **(native)**    | **2560×1440**           | **3.69 MPix**                 |
+--------------------------+-------------------------+-------------------------------+
| ``1.33`` (supersampling) | 3404×1915               | 6.52 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``1.50`` (supersampling) | 3840×2160               | 8.29 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``2.00`` (supersampling) | 5120×2880               | 14.75 MPix                    |
+--------------------------+-------------------------+-------------------------------+

**3840×2160 (Ultra HD "4K")**

+--------------------------+-------------------------+-------------------------------+
| Resolution scale factor  | 3D rendering resolution | Megapixels rendered per frame |
+==========================+=========================+===============================+
| ``0.50``                 | 1920×1080               | 2.07 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.67``                 | 2572×1447               | 3.72 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.75``                 | 2880×1620               | 4.67 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``0.85``                 | 3264×1836               | 5.99 MPix                     |
+--------------------------+-------------------------+-------------------------------+
| ``1.00`` **(native)**    | **3840×2160**           | **8.29 MPix**                 |
+--------------------------+-------------------------+-------------------------------+
| ``1.33`` (supersampling) | 5107×2872               | 14.67 MPix                    |
+--------------------------+-------------------------+-------------------------------+
| ``1.50`` (supersampling) | 5760×3240               | 18.66 MPix                    |
+--------------------------+-------------------------+-------------------------------+
| ``2.00`` (supersampling) | 7680×4320               | 33.18 MPix                    |
+--------------------------+-------------------------+-------------------------------+

Độ sắc nét FSR
~~~~~~~~~~~~~~

*Chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.*

Khi sử dụng chế độ tỷ lệ FSR1 hoặc FSR2, có thể điều khiển độ sắc nét bằng cài đặt project nâng cao **Rendering > Scaling 3D > FSR Sharpness**.

Cường độ được đảo ngược so với hầu hết các thanh trượt độ sắc nét khác: các giá trị *thấp hơn* sẽ tạo ra hình ảnh cuối cùng sắc nét hơn, trong khi các giá trị *cao hơn* sẽ *giảm* tác động của bộ lọc làm sắc nét. ``0.0`` là mức sắc nét nhất, còn ``2.0`` là mức ít sắc nét nhất. Giá trị mặc định ``0.2`` tạo sự cân bằng giữa việc giữ lại độ sắc nét của hình ảnh gốc và tránh aliasing bổ sung do làm sắc nét quá mức.

.. note::

    Nếu muốn sử dụng tính năng làm sắc nét khi kết xuất ở độ phân giải gốc, hiện tại Godot không cho phép sử dụng độc lập thành phần làm sắc nét của FSR1 (RCAS) với thành phần upscaling (EASU).

    Để khắc phục tạm thời, bạn có thể đặt tỷ lệ kết xuất 3D thành ``0.99``, đặt chế độ tỷ lệ thành **FSR 1.0**, sau đó điều chỉnh độ sắc nét FSR theo nhu cầu. Cách này cho phép sử dụng FSR1 trong khi kết xuất ở độ phân giải gần với độ phân giải gốc.

    Ngoài ra, bạn có thể đặt chế độ tỷ lệ thành **FSR 2.2** với tỷ lệ kết xuất 3D được đặt thành ``1.0`` nếu GPU còn đủ headroom. Cách này cũng cung cấp temporal antialiasing chất lượng cao. Cài đặt **FSR Sharpness** vẫn hoạt động trong trường hợp này.

.. _doc_resolution_scaling_mipmap_bias:

Mipmap bias
~~~~~~~~~~~

*Chỉ khả dụng trong renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Godot tự động sử dụng texture mipmap bias âm khi tỷ lệ độ phân giải 3D được đặt thấp hơn ``1.0``. Điều này giúp bảo toàn chi tiết texture tốt hơn, nhưng khiến các texture nhiều chi tiết có vẻ nhiễu.

Texture LOD bias hiện ảnh hưởng đến cả kết xuất 2D và 3D theo cùng một cách. Tuy nhiên, hãy lưu ý rằng nó chỉ có tác dụng với các texture đã bật mipmap. Texture được sử dụng trong 2D không bật mipmap theo mặc định, nghĩa là chỉ kết xuất 3D bị ảnh hưởng, trừ khi bạn bật mipmap cho texture 2D trong Import dock.

Công thức dùng để xác định texture mipmap bias là: ``log2f(min(scaling_3d_scale, 1.0)) + custom_texture_mipmap_bias``

Để bù cho độ mờ do một số phương pháp antialiasing gây ra, Godot cũng thêm offset ``-0.25`` khi FXAA được bật và offset ``-0.5`` khi TAA được bật. Nếu cả hai được bật cùng lúc, offset ``-0.75`` sẽ được sử dụng. Offset mipmap bias này được áp dụng *trước* offset tỷ lệ độ phân giải, nên nó không thay đổi theo tỷ lệ độ phân giải.

Có thể thay đổi thủ công texture LOD bias bằng cách điều chỉnh cài đặt project nâng cao **Rendering > Textures > Default Filters > Texture Mipmap Bias**. Bạn cũng có thể thay đổi nó tại runtime trên :ref:`Viewports <class_Viewport>` bằng cách điều chỉnh thuộc tính ``texture_mipmap_bias``.

.. warning::

    Việc điều chỉnh mipmap LOD bias thủ công có thể hữu ích trong một số trường hợp, nhưng cần thực hiện cẩn thận để tránh hình ảnh cuối cùng bị nhiễu khi chuyển động.

    Mipmap LOD bias *âm* cũng có thể làm giảm hiệu năng do các mip có độ phân giải cao hơn phải được sample từ xa hơn. Các giá trị được khuyến nghị cho offset thủ công nằm trong khoảng từ ``-0.5`` đến ``0.0``.

    Mipmap LOD bias *dương* sẽ khiến texture có mipmap mờ hơn mức dự kiến. Điều này có thể cải thiện hiệu năng đôi chút, nhưng nếu không thì không được khuyến nghị, vì sự suy giảm chất lượng hình ảnh thường không đáng với mức tăng hiệu năng đạt được.

Ví dụ dưới đây cho thấy một trường hợp cực đoan, với mipmap LOD bias bằng ``-1.0`` và anisotropic filtering bị tắt để làm cho sự khác biệt dễ nhận thấy hơn:

.. image:: img/resolution_scaling_texture_mipmap_bias_comparison.png

Khắc phục sự cố
---------------

Hiệu năng không tăng nhiều khi giảm tỷ lệ độ phân giải
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu hiệu năng không tăng nhiều khi giảm tỷ lệ độ phân giải xuống một giá trị như ``0.5``, có khả năng bottleneck hiệu năng nằm ở nơi khác trong scene. Ví dụ, scene của bạn có thể có quá nhiều draw call, dẫn đến bottleneck CPU. Tương tự, bạn có thể đã bật quá nhiều hiệu ứng đồ họa khiến GPU không xử lý được (chẳng hạn như SDFGI, SSAO hoặc SSR).

Xem các tutorial :ref:`doc_performance` để biết thêm thông tin.
