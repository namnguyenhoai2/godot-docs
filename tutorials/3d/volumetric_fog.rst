.. _doc_volumetric_fog:

Sương mù thể tích và các thể tích sương mù
==========================================

.. note::

    Sương mù thể tích chỉ được hỗ trợ trong renderer Forward+, không được hỗ trợ trong renderer Mobile hoặc Compatibility.

Như được mô tả trong :ref:`doc_environment_and_post_processing`, Godot hỗ trợ nhiều hiệu ứng hình ảnh, bao gồm hai loại sương mù: sương mù truyền thống (không thể tích) và sương mù thể tích. Sương mù truyền thống ảnh hưởng đến toàn bộ scene cùng lúc và không thể tùy chỉnh bằng :ref:`doc_fog_shader`.

Có thể sử dụng sương mù thể tích cùng lúc với sương mù không thể tích nếu muốn.

Trên trang này, bạn sẽ học:

- Cách thiết lập sương mù thể tích trong Godot. - FogVolume là gì và chúng khác với sương mù thể tích "toàn cục" như thế nào.

.. seealso::

    Bạn có thể xem sương mù thể tích hoạt động như thế nào qua `dự án demo Volumetric Fog <https://github.com/godotengine/godot-demo-projects/tree/master/3d/volumetric_fog>`__.

Dưới đây là so sánh giữa sương mù truyền thống (không tương tác với ánh sáng) và sương mù thể tích, có thể tương tác với ánh sáng:

.. image:: img/volumetric_fog_comparison.png

Các thuộc tính của sương mù thể tích
------------------------------------

Sau khi bật sương mù thể tích trong resource Environment của node WorldEnvironment, bạn có thể chỉnh sửa các thuộc tính sau:

- **Density:** Mật độ *exponential* cơ sở của sương mù thể tích. Đặt giá trị này thành mật độ thấp nhất mà bạn muốn áp dụng trên toàn cục. Có thể sử dụng FogVolumes để cộng hoặc trừ mật độ này trong các khu vực cụ thể. Giá trị ``0.0`` sẽ tắt sương mù thể tích toàn cục nhưng vẫn cho phép FogVolumes hiển thị sương mù thể tích trong các khu vực cụ thể. Việc render sương mù có tính exponential giống như trong thực tế. - **Albedo:** Color của sương mù thể tích khi tương tác với ánh sáng. Sương và mù có albedo gần với màu trắng (``Color(1, 1, 1, 1)``), trong khi khói có albedo tối hơn. - **Emission:** Ánh sáng phát ra từ sương mù thể tích. Ngay cả khi có emission, sương mù thể tích sẽ không chiếu sáng lên các bề mặt khác. Emission hữu ích để thiết lập màu môi trường. Vì hiệu ứng sương mù thể tích chỉ sử dụng single-scattering, sương mù thường cần một chút emission để làm mềm các bóng đổ gắt. - **Emission Energy:** Độ sáng của ánh sáng phát ra từ sương mù thể tích. - **GI Inject:** Điều chỉnh cường độ của Global Illumination được sử dụng trong màu albedo của sương mù thể tích. Giá trị ``0.0`` có nghĩa là Global Illumination sẽ không ảnh hưởng đến sương mù thể tích. Điều này gây ra một chi phí hiệu năng nhỏ khi được đặt cao hơn ``0.0``. - **Anisotropy:** Hướng của ánh sáng tán xạ khi truyền qua sương mù thể tích. Giá trị gần ``1.0`` có nghĩa là gần như toàn bộ ánh sáng bị tán xạ về phía trước. Giá trị gần ``0.0`` có nghĩa là ánh sáng được tán xạ đồng đều theo mọi hướng. Giá trị gần ``-1.0`` có nghĩa là ánh sáng chủ yếu bị tán xạ về phía sau. Sương và mù tán xạ ánh sáng hơi hướng về phía trước, trong khi khói tán xạ ánh sáng đồng đều theo mọi hướng. - **Length:** Khoảng cách mà sương mù thể tích được tính toán. Tăng giá trị để tính sương mù trên phạm vi lớn hơn, giảm giá trị để có thêm chi tiết khi không cần phạm vi xa. Để có chất lượng sương mù tốt nhất, hãy giữ giá trị này thấp nhất có thể. - **Detail Spread:** Phân bố kích thước dọc theo chiều dài của bộ đệm froxel. Giá trị cao hơn sẽ nén các froxel lại gần camera hơn và đặt nhiều chi tiết hơn ở gần camera. - **Ambient Inject:** Điều chỉnh cường độ của ánh sáng môi trường được sử dụng trong sương mù thể tích. Giá trị ``0.0`` có nghĩa là ánh sáng môi trường sẽ không ảnh hưởng đến sương mù thể tích. Điều này gây ra một chi phí hiệu năng nhỏ khi được đặt cao hơn ``0.0``. - **Sky Affect:** Kiểm soát mức độ sương mù thể tích được vẽ lên bầu trời nền. Nếu đặt thành ``0.0``, sương mù thể tích sẽ hoàn toàn không ảnh hưởng đến việc render bầu trời (bao gồm cả FogVolumes).

Có thêm hai thuộc tính trong phần **Temporal Reprojection**:

- **Temporal Reprojection > Enabled:** Bật temporal reprojection trong sương mù thể tích. Temporal reprojection trộn sương mù thể tích của frame hiện tại với sương mù thể tích của frame trước để làm mượt các cạnh răng cưa. Chi phí hiệu năng là tối thiểu, tuy nhiên điều này khiến các FogVolume và Light3D đang di chuyển bị "bóng ma" và để lại vệt phía sau. Khi bật temporal reprojection, hãy cố gắng tránh di chuyển FogVolume hoặc Light3D quá nhanh. Các hiệu ứng chiếu sáng động tồn tại trong thời gian ngắn nên đặt **Volumetric Fog Energy** thành ``0.0`` để tránh bóng ma. - **Temporal Reprojection > Amount:** Mức độ trộn frame trước với frame hiện tại. Giá trị cao hơn tạo ra sương mù thể tích mượt hơn, nhưng khiến hiện tượng "bóng ma" nghiêm trọng hơn nhiều. Giá trị thấp hơn làm giảm bóng ma nhưng có thể khiến hiện tượng jitter theo thời gian giữa các frame trở nên nhìn thấy được.

.. note::

    Không giống sương mù không thể tích, sương mù thể tích có phạm vi *hữu hạn*. Điều này có nghĩa là sương mù thể tích không thể bao phủ hoàn toàn một thế giới lớn, vì cuối cùng nó sẽ ngừng được render ở khoảng cách xa.

    Nếu bạn muốn ẩn các khu vực xa khỏi người chơi, nên bật cả sương mù không thể tích và sương mù thể tích cùng lúc, rồi điều chỉnh mật độ của chúng cho phù hợp.

Tương tác của ánh sáng với sương mù thể tích
--------------------------------------------

Để mô phỏng hành vi tán xạ ánh sáng của sương mù trong thực tế, mọi loại ánh sáng sẽ tương tác với sương mù thể tích. Có thể điều chỉnh mức độ ảnh hưởng của từng ánh sáng đến sương mù thể tích bằng thuộc tính **Volumetric Fog Energy** trên mỗi ánh sáng. Việc bật bóng đổ trên một ánh sáng cũng sẽ làm cho các bóng đổ đó hiển thị trên sương mù thể tích.

Nếu không muốn ánh sáng tương tác với sương mù vì lý do nghệ thuật, bạn có thể tắt tính năng này trên toàn cục bằng cách đặt **Volumetric Fog > Albedo** thành màu đen thuần trong resource Environment. Bạn cũng có thể tắt tương tác của ánh sáng với sương mù cho từng ánh sáng cụ thể bằng cách đặt **Volumetric Fog Energy** của ánh sáng đó thành ``0``. Việc này cũng cải thiện hiệu năng một chút bằng cách loại trừ ánh sáng khỏi các phép tính sương mù thể tích.

Sử dụng sương mù thể tích như một giải pháp chiếu sáng thể tích
---------------------------------------------------------------

Mặc dù không chính xác về mặt vật lý, bạn có thể tinh chỉnh các thiết lập của sương mù thể tích để sử dụng nó như một giải pháp *chiếu sáng* thể tích. Điều này có nghĩa là các phần không được chiếu sáng của môi trường sẽ không còn bị sương mù làm tối, nhưng ánh sáng vẫn có thể làm sương mù sáng hơn ở các khu vực cụ thể.

Bạn có thể thực hiện điều này bằng cách đặt mật độ sương mù thể tích thành giá trị thấp nhất được phép *lớn hơn không* (``0.0001``), sau đó tăng thuộc tính **Volumetric Fog Energy** trên các ánh sáng lên các giá trị cao hơn nhiều so với mặc định để bù lại. Các giá trị từ ``200.0`` đến ``5000.0`` thường hoạt động tốt cho mục đích này.

.. image:: img/volumetric_fog_lighting.png

Cân bằng hiệu năng và chất lượng
--------------------------------

Có một số project settings giúp điều chỉnh hiệu năng và chất lượng của sương mù thể tích:

- **Rendering > Environment > Volumetric Fog > Volume Size:** Kích thước cơ sở được sử dụng để xác định kích thước của bộ đệm froxel trên trục X và trục Y của camera. Kích thước cuối cùng được điều chỉnh theo aspect ratio của màn hình, vì vậy các giá trị thực tế có thể khác với giá trị được đặt. Đặt kích thước lớn hơn để có sương mù chi tiết hơn, hoặc đặt kích thước nhỏ hơn để có hiệu năng tốt hơn. - **Rendering > Environment > Volumetric Fog > Volume Depth:** Số lượng lát cắt được sử dụng dọc theo chiều sâu của bộ đệm froxel cho sương mù thể tích. Số lượng thấp hơn sẽ hiệu quả hơn, nhưng có thể khiến các artifact xuất hiện khi camera di chuyển. - **Rendering > Environment > Volumetric Fog > Use Filter:** Bật tính năng lọc hiệu ứng sương mù thể tích trước khi tích hợp. Tính năng này làm mờ sương mù đáng kể, giúp giảm các chi tiết nhỏ nhưng cũng làm mượt các cạnh gắt và artifact aliasing. Hãy tắt tính năng này khi cần nhiều chi tiết hơn.

.. note::

    Sương mù thể tích có thể gây ra hiện tượng banding trên viewport, đặc biệt ở các mức mật độ cao hơn. Xem :ref:`doc_3d_rendering_limitations_color_banding` để biết hướng dẫn giảm banding.

Sử dụng fog volume cho sương mù thể tích cục bộ
-----------------------------------------------

Đôi khi, bạn muốn giới hạn sương mù trong các khu vực cụ thể. Ngược lại, bạn có thể muốn có sương mù thể tích toàn cục, nhưng loại trừ sương mù khỏi một số khu vực nhất định. Có thể thực hiện cả hai cách bằng các node FogVolume.

Dưới đây là hướng dẫn bắt đầu nhanh để sử dụng FogVolume:

- Hãy đảm bảo **Volumetric Fog** được bật trong các thuộc tính Environment. Nếu không muốn có sương mù thể tích toàn cục, hãy đặt **Density** của nó thành ``0.0``. - Tạo một node FogVolume. - Gán một FogMaterial mới cho thuộc tính **Material** của node FogVolume. - Trong FogMaterial, đặt **Density** thành giá trị dương để tăng mật độ bên trong FogVolume, hoặc giá trị âm để trừ mật độ khỏi sương mù thể tích toàn cục. - Cấu hình phạm vi và hình dạng của FogVolume theo nhu cầu.

.. note::

    Các fog volume mỏng có thể nhấp nháy khi camera di chuyển hoặc xoay. Có thể giảm hiện tượng này bằng cách tăng project setting **Rendering > Environment > Volumetric Fog > Volume Depth** (đánh đổi bằng hiệu năng) hoặc giảm **Length** trong các thuộc tính sương mù thể tích của Environment (không ảnh hưởng đến hiệu năng, nhưng làm giảm phạm vi sương mù). Ngoài ra, có thể làm FogVolume dày hơn và sử dụng mật độ thấp hơn trong **Material**.

Các thuộc tính của FogVolume
----------------------------

- **Extents:** Kích thước của FogVolume khi **Shape** là **Ellipsoid**, **Cone**, **Cylinder** hoặc **Box**. Nếu **Shape** là **Cone** hoặc **Cylinder**, hình nón/hình trụ sẽ được điều chỉnh để vừa bên trong các extents. Không hỗ trợ scale không đồng nhất các hình nón/hình trụ thông qua thuộc tính **Extents**, nhưng bạn có thể scale node FogVolume thay thế. - **Shape:** Hình dạng của FogVolume. Có thể đặt thành **Ellipsoid**, **Cone**, **Cylinder**, **Box** hoặc **World** (hoạt động như sương mù thể tích toàn cục). - **Material:** Material được FogVolume sử dụng. Có thể là FogMaterial dựng sẵn hoặc ShaderMaterial tùy chỉnh (:ref:`doc_fog_shader`).

Sau khi chọn **New FogMaterial** trong thuộc tính **Material**, bạn có thể điều chỉnh các thuộc tính sau trong FogMaterial:

- **Density:** Độ đặc của FogVolume. Các đối tượng đặc hơn sẽ mờ đục hơn, nhưng có thể gặp hiện tượng lấy mẫu thiếu, tạo ra các lỗi hình ảnh trông như các sọc. Có thể dùng các giá trị âm để trừ sương khỏi những FogVolume khác hoặc sương thể tích toàn cục. - **Albedo:** Color tán xạ đơn của FogVolume. Về mặt nội bộ, thành viên albedo được chuyển đổi thành tán xạ đơn, sau đó được hòa trộn cộng với các FogVolume khác và **Albedo** của sương thể tích toàn cục. - **Emission:** Color của ánh sáng do FogVolume phát ra. Ánh sáng phát ra sẽ không chiếu sáng hoặc tạo bóng lên các đối tượng khác, nhưng có thể hữu ích để điều chỉnh Color của FogVolume độc lập với các nguồn sáng. - **Height Falloff:** Tốc độ giảm độ đặc của sương dựa trên độ cao khi độ cao tăng trong không gian thế giới. Falloff cao sẽ tạo ra sự chuyển tiếp gắt, còn Falloff thấp sẽ tạo ra sự chuyển tiếp mượt hơn. Giá trị ``0.0`` tạo ra sương có độ đặc đồng đều. Ngưỡng độ cao được xác định bởi độ cao của FogVolume liên kết. - **Edge Fade:** Độ cứng của các cạnh FogVolume. Giá trị cao hơn sẽ tạo ra các cạnh mềm hơn, còn giá trị thấp hơn sẽ tạo ra các cạnh cứng hơn. - **Density Texture:** Texture 3D được dùng để điều chỉnh độ đặc của thành viên density trong FogVolume. Bạn có thể dùng thuộc tính này để tạo biến thiên độ đặc của sương bên trong FogVolume theo bất kỳ mẫu tĩnh nào. Đối với các hiệu ứng hoạt ảnh, hãy cân nhắc sử dụng một shader tùy chỉnh
  :ref:`fog shader <doc_fog_shader>`.
  Bạn có thể import bất kỳ hình ảnh nào dưới dạng texture 3D bằng cách
  :ref:`changing its import type in the Import dock <doc_importing_images_changing_import_type>`.

Sử dụng texture độ đặc nhiễu 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.1, có một resource NoiseTexture3D có thể được dùng để tạo nhiễu 3D theo quy trình. Resource này rất phù hợp với các texture độ đặc của FogMaterial, từ đó có thể tạo ra các hiệu ứng sương chi tiết hơn:

.. figure:: img/volumetric_fog_fog_material_density_texture.webp
   :alt: FogMaterial comparison (without and with density texture)

   Screenshot taken with **Volume Size** project setting set to 192 to make
   high-frequency detail more visible in the fog.

Để thực hiện việc này, hãy chọn thuộc tính **Density Texture** rồi chọn **New NoiseTexture3D**. Chỉnh sửa NoiseTexture3D bằng cách nhấp vào nó, sau đó nhấp vào **Noise** ở cuối các thuộc tính của NoiseTexture3D và chọn **New FastNoiseLite**. Điều chỉnh chiều rộng, chiều cao và độ sâu của texture nhiễu theo kích thước FogVolume của bạn.

Để cải thiện hiệu năng, bạn nên dùng kích thước texture nhỏ (64×64×64 hoặc thấp hơn), vì rất khó nhận thấy chi tiết tần số cao trong FogVolume. Nếu muốn thể hiện các biến thiên độ đặc chi tiết hơn, bạn sẽ cần tăng **Rendering > Environment > Volumetric Fog > Volume Size** trong phần cài đặt project, điều này sẽ làm giảm hiệu năng.

.. note::

    **Color Ramp** của NoiseTexture3D ảnh hưởng đến các texture độ đặc của FogMaterial, nhưng vì chỉ lấy mẫu kênh đỏ của texture nên chỉ kênh đỏ của color ramp mới ảnh hưởng đến độ đặc kết quả.

    Tuy nhiên, sử dụng color ramp sẽ *không* tô màu volume sương theo texture. Bạn sẽ cần dùng một shader tùy chỉnh đọc Texture3D để thực hiện việc này.

Shader FogVolume tùy chỉnh
--------------------------

Trang này chỉ đề cập đến các cài đặt tích hợp sẵn do FogMaterial cung cấp. Nếu cần tùy chỉnh hành vi của sương bên trong một node FogVolume (chẳng hạn như tạo sương động), bạn có thể tùy chỉnh hình thức của các node FogVolume bằng :ref:`doc_fog_shader`.

Giả lập sương thể tích bằng quad
--------------------------------

Trong một số trường hợp, sử dụng QuadMesh được cấu hình đặc biệt có thể phù hợp hơn so với sương thể tích:

- Quad hoạt động với mọi phương thức render, bao gồm Mobile và Compatibility. - Quad không cần temporal reprojection để hiển thị mượt mà, nên phù hợp với các hiệu ứng động chuyển động nhanh như laser. Chúng cũng có thể thể hiện các chi tiết nhỏ mà sương thể tích không thể xử lý hiệu quả. - Quad nhìn chung có chi phí hiệu năng thấp hơn sương thể tích.

Tuy nhiên, phương pháp này cũng có một số nhược điểm:

- Hiệu ứng sương có falloff kém chân thực hơn, đặc biệt là khi camera đi vào sương. - Có thể xảy ra vấn đề sắp xếp độ trong suốt khi các sprite chồng lên nhau. - Hiệu năng không nhất thiết tốt hơn sương thể tích nếu có nhiều sprite ở gần camera.

Để tạo một sprite sương dựa trên QuadMesh:

1. Tạo một node MeshInstance3D với resource QuadMesh trong thuộc tính **Mesh**. Đặt kích thước theo mong muốn. 2. Tạo một StandardMaterial3D mới trong thuộc tính **Material** của mesh. 3. Trong StandardMaterial3D, đặt **Shading > Shading Mode** thành **Unshaded**, **Billboard > Mode** thành **Enabled**, bật **Proximity Fade** và đặt **Distance Fade** thành **Pixel Alpha**. 4. Đặt **Albedo > Texture** thành texture bên dưới (nhấp chuột phải và chọn **Save as…**):

   .. image:: img/volumetric_fog_quad_mesh_texture.webp

5. *Sau khi* đặt texture albedo, đi đến dock Import, chọn texture rồi thay đổi chế độ nén thành **Lossless** để cải thiện chất lượng.

Màu của sương được đặt bằng thuộc tính **Albedo > Color**; độ đặc của sương được đặt bằng kênh alpha của màu. Để có kết quả tốt nhất, bạn sẽ phải điều chỉnh **Proximity Fade > Distance** và **Distance Fade > Max Distance** tùy theo kích thước QuadMesh.

Bạn có thể giữ tắt billboarding nếu đặt quad sao cho tất cả các góc của nó đều nằm trong hình học đặc. Điều này có thể hữu ích khi tạo sương cho các mặt phẳng lớn mà camera không thể đi vào, chẳng hạn như các hố không đáy.
