.. _doc_3d_antialiasing:

Khử răng cưa 3D
===============

.. Images on this page were generated using the project below
.. (except for `antialiasing_none_scaled.webp`):
.. https://github.com/Calinou/godot-antialiasing-comparison

.. seealso::

    Godot cũng hỗ trợ khử răng cưa trong kết xuất 2D. Nội dung này được trình bày trên
    Trang :ref:`doc_2d_antialiasing`.

Giới thiệu
----------

Do có độ phân giải hạn chế, các cảnh được kết xuất trong 3D có thể xuất hiện các hiện tượng răng cưa. Những hiện tượng này thường biểu hiện dưới dạng hiệu ứng "bậc thang" trên các cạnh bề mặt (răng cưa cạnh), cũng như hiện tượng nhấp nháy và/hoặc lấp lánh trên các bề mặt phản chiếu (răng cưa phản xạ).

Trong ví dụ dưới đây, bạn có thể nhận thấy các cạnh có vẻ ngoài dạng khối. Thảm thực vật cũng nhấp nháy rồi biến mất, còn các đường mảnh trên đầu hộp gần như đã biến mất:

.. figure:: img/antialiasing_none_scaled.webp
   :alt: Hình ảnh được phóng to 2× bằng bộ lọc láng giềng gần nhất để làm cho hiện tượng răng cưa dễ nhận thấy hơn.
   :align: center

   Hình ảnh được phóng to 2× bằng bộ lọc láng giềng gần nhất để làm cho hiện tượng răng cưa dễ nhận thấy hơn.

Để khắc phục vấn đề này, Godot cung cấp nhiều kỹ thuật khử răng cưa khác nhau. Các kỹ thuật này được trình bày chi tiết bên dưới.

.. seealso::

    Bạn có thể so sánh hoạt động của các thuật toán khử răng cưa bằng `dự án trình diễn Khử răng cưa 3D <https://github.com/godotengine/godot-demo-projects/tree/master/3d/antialiasing>`__.

Khử răng cưa đa mẫu (MSAA)
--------------------------

*Tính năng này có trong tất cả các renderer.*

Đây là kỹ thuật "truyền thống" để xử lý răng cưa. MSAA rất hiệu quả trên các cạnh hình học (đặc biệt ở các mức cao hơn). MSAA hoàn toàn không gây mờ.

MSAA có 3 mức: 2×, 4×, 8×. Các mức cao hơn khử răng cưa cạnh hiệu quả hơn, nhưng đòi hỏi tài nguyên cao hơn đáng kể. Trong các game có hình ảnh hiện đại, bạn nên dùng MSAA 2× hoặc 4×, vì MSAA 8× thường đòi hỏi quá nhiều tài nguyên.

Nhược điểm của MSAA là nó chỉ hoạt động trên các cạnh. Đó là vì MSAA tăng số lượng mẫu *coverage*, nhưng không tăng số lượng mẫu *color*. Tuy nhiên, vì số lượng mẫu màu không tăng, các fragment shader vẫn chỉ được chạy một lần cho mỗi pixel. Do đó, MSAA không làm giảm hiện tượng răng cưa trong suốt đối với các material sử dụng chế độ trong suốt **Alpha Scissor** (độ trong suốt 1 bit). MSAA cũng không hiệu quả với răng cưa phản xạ.

Để giảm răng cưa trên các material alpha scissor,
:ref:`khử răng cưa alpha <doc_standard_material_3d_alpha_antialiasing>` (còn gọi là *alpha to coverage*) có thể được bật trên các material cụ thể trong thuộc tính StandardMaterial3D hoặc ORMMaterial3D. Alpha to coverage có chi phí hiệu năng vừa phải, nhưng hiệu quả trong việc giảm răng cưa trên các material trong suốt mà không gây mờ.

Để làm cho răng cưa phản xạ khó nhận thấy hơn, hãy sử dụng `Screen-space roughness limiter <Screen-space roughness limiter_>`_, tính năng này được bật theo mặc định.

Có thể bật MSAA trong Project Settings bằng cách thay đổi giá trị của
thiết lập :ref:`Rendering > Anti Aliasing > Quality > MSAA 3D <class_ProjectSettings_property_rendering/anti_aliasing/quality/msaa_3d>`. Điều quan trọng là phải thay đổi giá trị của thiết lập **MSAA 3D**, không phải **MSAA 2D**, vì đây là hai thiết lập hoàn toàn riêng biệt.

So sánh giữa không khử răng cưa (bên trái) và các mức MSAA khác nhau (bên phải). Lưu ý rằng khử răng cưa alpha không được sử dụng ở đây:

.. image:: img/antialiasing_msaa_2x.webp

.. image:: img/antialiasing_msaa_4x.webp

.. image:: img/antialiasing_msaa_8x.webp

.. _doc_3d_antialiasing_taa:

Khử răng cưa theo thời gian (TAA)
---------------------------------

*Tính năng này chỉ có trong renderer Forward+, không có trong renderer Mobile hoặc Compatibility.*

Khử răng cưa theo thời gian hoạt động bằng cách *hội tụ* kết quả của các khung hình đã kết xuất trước đó thành một khung hình duy nhất có chất lượng cao. Đây là một quá trình liên tục, hoạt động bằng cách làm lệch vị trí của tất cả các đỉnh trong cảnh ở mỗi khung hình. Việc làm lệch này nhằm thu nhận chi tiết dưới pixel và sẽ không thể nhận thấy, ngoại trừ trong những tình huống cực đoan.

Kỹ thuật này thường được sử dụng trong các game hiện đại vì cung cấp hình thức khử răng cưa hiệu quả nhất để chống lại răng cưa phản xạ và các hiện tượng khác do shader gây ra. TAA cũng hỗ trợ đầy đủ khử răng cưa trong suốt.

TAA tạo ra một lượng mờ nhỏ khi được bật trong các cảnh tĩnh, nhưng hiệu ứng mờ này trở nên rõ rệt hơn khi camera di chuyển. Một nhược điểm khác của TAA là nó có thể tạo ra các hiện tượng *bóng ma* phía sau các vật thể đang di chuyển. Kết xuất ở framerate cao hơn sẽ cho phép TAA hội tụ nhanh hơn, nhờ đó làm cho các hiện tượng bóng ma này khó nhận thấy hơn.

Có thể bật khử răng cưa theo thời gian trong Project Settings bằng cách thay đổi giá trị của
thiết lập :ref:`Rendering > Anti Aliasing > Quality > TAA <class_ProjectSettings_property_rendering/anti_aliasing/quality/use_taa>`.

So sánh giữa không khử răng cưa (bên trái) và TAA (bên phải):

.. image:: img/antialiasing_taa.webp

.. _doc_3d_antialiasing_fsr2:

AMD FidelityFX Super Resolution 2.2 (FSR2)
------------------------------------------

*Tính năng này chỉ có trong renderer Forward+, không có trong renderer Mobile hoặc Compatibility.*

Kể từ Godot 4.2, Godot đã tích hợp hỗ trợ `AMD FidelityFX Super Resolution <https://www.amd.com/en/products/graphics/technologies/fidelityfx/super-resolution.html>`__ 2.2. Đây là một :ref:`phương pháp nâng độ phân giải <doc_resolution_scaling>` tương thích với tất cả GPU gần đây của mọi nhà cung cấp. FSR2 thường được thiết kế để cải thiện hiệu năng bằng cách giảm độ phân giải kết xuất 3D nội bộ, sau đó nâng lên độ phân giải đầu ra.

Tuy nhiên, không giống FSR1, FSR2 cũng cung cấp khử răng cưa theo thời gian. Điều này có nghĩa là FSR2 có thể được sử dụng ở độ phân giải gốc để khử răng cưa chất lượng cao, trong đó độ phân giải đầu vào bằng độ phân giải đầu ra. Trong trường hợp này, bật FSR2 thực sự sẽ *làm giảm* hiệu năng, nhưng sẽ cải thiện đáng kể chất lượng kết xuất.

Sử dụng FSR2 ở độ phân giải gốc đòi hỏi nhiều tài nguyên hơn so với sử dụng TAA ở độ phân giải gốc, vì vậy chỉ nên dùng khi GPU của bạn còn nhiều tài nguyên dự phòng. Mặt tích cực là FSR2 cung cấp độ bao phủ khử răng cưa tốt hơn với ít hiện tượng mờ hơn so với TAA, đặc biệt khi chuyển động.

So sánh giữa không khử răng cưa (bên trái) và FSR2 ở độ phân giải gốc (bên phải):

.. image:: img/antialiasing_fsr2_native.webp

..  note::

    Theo mặc định, thiết lập dự án **FSR Sharpness** được đặt thành ``0.2`` (các giá trị cao hơn sẽ cho mức làm sắc nét thấp hơn). Để so sánh, tính năng làm sắc nét của FSR đã được tắt bằng cách đặt thành ``2.0`` trong ảnh chụp màn hình ở trên.

.. _doc_3d_antialiasing_fxaa:

Khử răng cưa xấp xỉ nhanh (FXAA)
--------------------------------

*Tính năng này chỉ có trong renderer Forward+ và Mobile, không có trong renderer Compatibility.*

Khử răng cưa xấp xỉ nhanh là một giải pháp khử răng cưa hậu kỳ. Kỹ thuật này chạy nhanh hơn bất kỳ kỹ thuật khử răng cưa nào khác và cũng hỗ trợ khử răng cưa trong suốt. Tuy nhiên, vì không có thông tin theo thời gian, nó không xử lý được nhiều đối với răng cưa phản xạ.

Kỹ thuật này đôi khi vẫn được sử dụng trong các game dành cho thiết bị di động. Tuy nhiên, trên các nền tảng máy tính để bàn, FXAA nhìn chung đã không còn phổ biến và được thay thế bởi temporal antialiasing, vốn hiệu quả hơn nhiều trong việc xử lý hiện tượng răng cưa specular. Dù vậy, việc cung cấp FXAA như một tùy chọn trong game vẫn có thể hữu ích cho người chơi sử dụng GPU cấp thấp.

FXAA tạo ra mức độ mờ vừa phải khi được bật (mờ hơn TAA khi hình ảnh đứng yên, nhưng ít mờ hơn TAA khi camera đang di chuyển).

Có thể bật FXAA trong Project Settings bằng cách thay đổi giá trị của thiết lập
:ref:`Rendering > Anti Aliasing > Quality > Screen Space AA <class_ProjectSettings_property_rendering/anti_aliasing/quality/screen_space_aa>` thành ``FXAA``.

So sánh giữa không dùng antialiasing (bên trái) và FXAA (bên phải):

.. image:: img/antialiasing_fxaa.webp

Sub-pixel Morphological Antialiasing (SMAA 1x)
----------------------------------------------

*Tính năng này chỉ khả dụng trong các renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Sub-pixel Morphological Antialiasing là một giải pháp antialiasing hậu kỳ. Tốc độ xử lý của nó chậm hơn FXAA một chút, nhưng tạo ra ít độ mờ hơn. Điều này đặc biệt hữu ích khi độ phân giải màn hình là 1080p trở xuống. Giống như FXAA, SMAA 1x không có thông tin theo thời gian và do đó không xử lý được nhiều hiện tượng răng cưa specular.

Hãy sử dụng SMAA 1x nếu bạn không đủ khả năng dùng MSAA nhưng thấy FXAA quá mờ.

Kết hợp nó với TAA hoặc thậm chí FSR2 để tối đa hóa antialiasing, với chi phí GPU cao hơn và độ mờ tăng thêm. Điều này có lợi nhất trong các cảnh chuyển động nhanh hoặc ngay sau khi camera cắt cảnh, đặc biệt ở FPS thấp.

Có thể bật SMAA 1x trong Project Settings bằng cách thay đổi giá trị của thiết lập
:ref:`Rendering > Anti Aliasing > Quality > Screen Space AA <class_ProjectSettings_property_rendering/anti_aliasing/quality/screen_space_aa>` thành ``SMAA``.

So sánh giữa không dùng antialiasing (bên trái) và SMAA 1x (bên phải):

.. image:: img/antialiasing_smaa.webp

Supersample antialiasing (SSAA)
-------------------------------

*Tính năng này khả dụng trong tất cả các renderer.*

Supersampling cung cấp chất lượng antialiasing cao nhất có thể, nhưng cũng tốn kém nhất. Nó hoạt động bằng cách đổ bóng cho mỗi pixel trong cảnh nhiều lần. Nhờ đó, SSAA có thể khử răng cưa cho các cạnh, độ trong suốt *và* hiện tượng răng cưa specular cùng lúc mà không tạo ra các lỗi bóng ma tiềm ẩn.

Nhược điểm của SSAA là chi phí *cực kỳ* cao. Chi phí này thường khiến SSAA khó được sử dụng cho game, nhưng supersampling vẫn có thể hữu ích cho :ref:`offline rendering <doc_creating_movies>`.

Supersample antialiasing được thực hiện bằng cách tăng thiết lập project nâng cao
:ref:`Rendering > Scaling 3D > Scale <class_ProjectSettings_property_rendering/scaling_3d/scale>` lên trên ``1.0`` đồng thời đảm bảo rằng
:ref:`Rendering > Scaling 3D > Mode <class_ProjectSettings_property_rendering/scaling_3d/mode>` được đặt thành ``Bilinear`` (giá trị mặc định). Vì hệ số scale được xác định theo từng trục, hệ số scale ``1.5`` sẽ tạo ra SSAA 2.25×, còn hệ số scale ``2.0`` sẽ tạo ra SSAA 4×. Vì Godot sử dụng bộ lọc song tuyến tính của phần cứng để thực hiện downsampling, kết quả sẽ sắc nét hơn với các hệ số scale là số nguyên (cụ thể là ``2.0``).

So sánh giữa không dùng antialiasing (bên trái) và các mức SSAA khác nhau (bên phải):

.. image:: img/antialiasing_ssaa_2.25x.webp

.. image:: img/antialiasing_ssaa_4x.webp

.. warning::

    Supersampling cũng yêu cầu nhiều video RAM, vì nó cần render ở độ phân giải đích rồi *downscale* xuống kích thước cửa sổ. Ví dụ, hiển thị một project ở độ phân giải 3840×2160 (độ phân giải 4K) với SSAA 4× sẽ yêu cầu render cảnh ở độ phân giải 7680×4320 (độ phân giải 8K), tức là nhiều hơn 4 lần số pixel.

    Nếu bạn sử dụng kích thước cửa sổ lớn như 4K, việc tăng scale độ phân giải vượt quá một giá trị nhất định có thể gây chậm nghiêm trọng (hoặc thậm chí crash) do hết VRAM.

.. _`Screen-space roughness limiter`:

Screen-space roughness limiter
------------------------------

*Tính năng này chỉ khả dụng trong các renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.*

Đây không phải là phương pháp khử răng cưa cho cạnh, mà là một cách giảm hiện tượng răng cưa specular trong 3D.

Screen-space roughness limiter hoạt động hiệu quả nhất trên hình học có nhiều chi tiết. Mặc dù nó có tác động đến chính việc render roughness map, ảnh hưởng tại đó khá hạn chế.

Screen-space roughness limiter được bật theo mặc định và không yêu cầu thiết lập thủ công. Nó chỉ ảnh hưởng nhỏ đến hiệu năng, vì vậy hãy cân nhắc tắt tính năng này nếu project của bạn không bị ảnh hưởng nhiều bởi hiện tượng răng cưa specular. Bạn có thể tắt tính năng này bằng thiết lập project **Rendering > Quality > Screen Space Filters > Screen Space Roughness Limiter**.

Texture roughness limiter khi import
------------------------------------

Giống như screen-space roughness limiter, đây không phải là phương pháp khử răng cưa cho cạnh, mà là một cách giảm hiện tượng răng cưa specular trong 3D.

Roughness limiting khi import hoạt động bằng cách chỉ định một normal map để sử dụng làm hướng dẫn giới hạn roughness. Bạn thực hiện việc này bằng cách chọn roughness map trong dock FileSystem, sau đó chuyển đến dock Import và đặt **Roughness > Mode** thành kênh màu nơi roughness map được lưu trữ (thường là **Green**), rồi đặt đường dẫn đến normal map của material. Hãy nhớ nhấp vào **Reimport** ở cuối dock Import sau khi đặt đường dẫn đến normal map.

Vì quá trình xử lý này chỉ diễn ra khi import nên hoàn toàn không ảnh hưởng đến hiệu năng. Tuy nhiên, tác động về mặt hình ảnh của nó khá hạn chế. Việc giới hạn roughness khi import chỉ giúp giảm hiện tượng răng cưa specular trong texture, không giúp giảm hiện tượng răng cưa xuất hiện trên các cạnh hình học của những mesh nhiều chi tiết.

Tôi nên sử dụng kỹ thuật antialiasing nào?
------------------------------------------

**Không có kỹ thuật antialiasing nào phù hợp với mọi trường hợp.** Vì antialiasing thường gây tải nặng cho GPU hoặc có thể tạo ra độ mờ không mong muốn, bạn nên thêm một thiết lập cho phép người chơi tắt antialiasing.

Đối với các project có định hướng nghệ thuật photorealistic, TAA thường là lựa chọn phù hợp nhất. Mặc dù TAA có thể tạo ra các lỗi bóng ma, không có kỹ thuật nào khác xử lý hiện tượng răng cưa specular tốt như TAA. Screen-space roughness limiter có thể hỗ trợ đôi chút, nhưng nhìn chung kém hiệu quả hơn nhiều trong việc xử lý hiện tượng răng cưa specular. Nếu GPU của bạn còn dư công suất, bạn có thể sử dụng FSR2 ở độ phân giải gốc để có temporal antialiasing cho hình ảnh đẹp hơn so với TAA tiêu chuẩn.

Đối với các project có ít bề mặt phản chiếu (chẳng hạn như phong cách nghệ thuật cartoon), MSAA có thể hoạt động hiệu quả. MSAA cũng là lựa chọn tốt nếu việc tránh độ mờ và các lỗi theo thời gian là quan trọng, chẳng hạn trong các game cạnh tranh.

Khi nhắm đến các nền tảng cấp thấp như thiết bị di động hoặc đồ họa tích hợp, FXAA thường là lựa chọn khả thi duy nhất. 2× MSAA có thể sử dụng được trong một số trường hợp, nhưng các mức MSAA cao hơn khó có thể chạy mượt mà trên GPU di động.

Godot cho phép sử dụng đồng thời nhiều kỹ thuật khử răng cưa. Điều này thường không cần thiết, nhưng có thể mang lại hình ảnh đẹp hơn trên các GPU cao cấp hoặc đối với
:ref:`kết xuất không theo thời gian thực <doc_creating_movies>`. Ví dụ: để các cạnh chuyển động trông đẹp hơn khi bật TAA, bạn cũng có thể bật MSAA cùng lúc.

So sánh các kỹ thuật khử răng cưa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. Note that this table uses emojis, which are not monospaced in most editors.
.. The table looks malformed but is not. When making changes, check the nearby
.. lines for guidance.

+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Tính năng               | MSAA             | TAA           | FSR2        | FXAA        | SMAA 1x     | SSAA             | SSRL        |
+=========================+==================+===============+=============+=============+=============+==================+=============+
| Khử răng cưa cạnh       | 🟢 Có            | 🟢 Có         | 🟢 Có       | 🟢 Có       | 🟢 Có       | 🟢 Có            | 🔴 Không    |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Khử răng cưa phản chiếu | 🟡 Một phần      | 🟢 Có         | 🟢 Có       | 🟡 Một phần | 🟡 Một phần | 🟢 Có            | 🟢 Có       |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Khử răng cưa trong suốt | 🟡 Một phần [1]_ | 🟢 Có [2]_    | 🟢 Có [2]_  | 🟢 Có       | 🟢 Có       | 🟢 Có            | 🔴 Không    |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Độ mờ thêm vào          | 🟢 Không có      | 🟡 Một phần   | 🟡 Một phần | 🟡 Một phần | 🟢 Thấp     | 🟡 Một phần [3]_ | 🟢 Không có |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Hiện tượng bóng mờ      | 🟢 Không có      | 🔴 Có         | 🔴 Có       | 🟢 Không có | 🟢 Không có | 🟢 Không có      | 🟢 Không có |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Chi phí hiệu năng       | 🟡 Trung bình    | 🟡 Trung bình | 🔴 Cao      | 🟢 Rất thấp | 🟢 Thấp     | 🔴 Rất cao       | 🟢 Thấp     |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Forward+                | ✔️ Có            | ✔️ Có         | ✔️ Có       | ✔️ Có       | ✔️ Có       | ✔️ Có            | ✔️ Có       |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Di động                 | ✔️ Có            | ❌ Không      | ❌ Không    | ✔️ Có       | ✔️ Có       | ✔️ Có            | ✔️ Có       |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+
| Tính tương thích        | ✔️ Có            | ❌ Không      | ❌ Không    | ❌ Không    | ❌ Không    | ✔️ Có            | ❌ Không    |
+-------------------------+------------------+---------------+-------------+-------------+-------------+------------------+-------------+


.. [1] MSAA không hoạt động tốt với các vật liệu sử dụng Alpha Scissor (độ trong suốt 1 bit). Có thể khắc phục điều này bằng cách bật ``alpha antialiasing`` trên vật liệu.
.. [2] Khử răng cưa cho độ trong suốt bằng TAA/FSR2 đạt hiệu quả cao nhất khi sử dụng Alpha Scissor.
.. [3] SSAA gây ra một chút mờ do quá trình giảm tỷ lệ song tuyến tính. Có thể khắc phục điều này bằng cách sử dụng hệ số tỷ lệ nguyên là ``2.0``.
