.. _doc_volumetric_fog:

Sương mù thể tích và các thể tích sương mù
==========================================

.. note::

    Sương mù thể tích chỉ được hỗ trợ trong renderer Forward+, không được hỗ trợ trong renderer Mobile hoặc Compatibility.

Như đã mô tả trong :ref:`doc_environment_and_post_processing`, Godot hỗ trợ nhiều hiệu ứng hình ảnh, bao gồm hai loại sương mù: sương mù truyền thống (không thể tích) và sương mù thể tích. Sương mù truyền thống ảnh hưởng đến toàn bộ cảnh cùng lúc và không thể được tùy chỉnh bằng :ref:`doc_fog_shader`.

Nếu muốn, có thể sử dụng sương mù thể tích đồng thời với sương mù không thể tích.

Trong trang này, bạn sẽ học:

- Cách thiết lập sương mù thể tích trong Godot.
- Fog volumes là gì và chúng khác với sương mù thể tích "toàn cục" như thế nào.

.. seealso::

    Bạn có thể xem cách sương mù thể tích hoạt động trong thực tế bằng dự án demo `Volumetric Fog <https://github.com/godotengine/godot-demo-projects/tree/master/3d/volumetric_fog>`__.

Sau đây là so sánh giữa sương mù truyền thống (không tương tác với ánh sáng) và sương mù thể tích, có thể tương tác với ánh sáng:

.. image:: img/volumetric_fog_comparison.png

Các thuộc tính của sương mù thể tích
------------------------------------

Sau khi bật sương mù thể tích trong resource Environment của node WorldEnvironment, bạn có thể chỉnh sửa các thuộc tính sau:

- **Density:** Mật độ *exponential* cơ sở của sương mù thể tích. Đặt giá trị này thành mật độ thấp nhất bạn muốn áp dụng trên toàn cục. Có thể sử dụng FogVolumes để cộng hoặc trừ mật độ này tại các khu vực cụ thể. Giá trị ``0.0`` sẽ tắt sương mù thể tích toàn cục, đồng thời cho phép FogVolumes hiển thị sương mù thể tích tại các khu vực cụ thể. Việc render sương mù mang tính exponential như trong thực tế.
- **Albedo:** Màu của sương mù thể tích khi tương tác với ánh sáng. Sương và sương mù có albedo gần với màu trắng (``Color(1, 1, 1, 1)``), trong khi khói có albedo tối hơn.
- **Emission:** Ánh sáng phát ra từ sương mù thể tích. Ngay cả khi có emission, sương mù thể tích cũng không chiếu sáng lên các bề mặt khác. Emission hữu ích để thiết lập màu môi trường. Vì hiệu ứng sương mù thể tích chỉ sử dụng single-scattering, sương mù thường cần một chút emission để làm mềm các bóng đổ gắt.
- **Emission Energy:** Độ sáng của ánh sáng phát ra từ sương mù thể tích.
- **GI Inject:** Tỷ lệ cường độ Global Illumination được sử dụng trong màu albedo của sương mù thể tích. Giá trị ``0.0`` có nghĩa là Global Illumination sẽ không ảnh hưởng đến sương mù thể tích. Khi được đặt cao hơn ``0.0``, thuộc tính này gây ra một chi phí hiệu năng nhỏ.
- **Anisotropy:** Hướng của ánh sáng tán xạ khi đi qua sương mù thể tích. Giá trị gần ``1.0`` có nghĩa là gần như toàn bộ ánh sáng được tán xạ về phía trước. Giá trị gần ``0.0`` có nghĩa là ánh sáng được tán xạ đồng đều theo mọi hướng. Giá trị gần ``-1.0`` có nghĩa là ánh sáng chủ yếu được tán xạ về phía sau. Sương mù và sương tán xạ ánh sáng hơi hướng về phía trước, trong khi khói tán xạ ánh sáng đồng đều theo mọi hướng.
- **Length:** Khoảng cách mà sương mù thể tích được tính toán. Tăng giá trị này để tính sương mù trong phạm vi lớn hơn; giảm giá trị để tăng chi tiết khi không cần phạm vi xa. Để đạt chất lượng sương mù tốt nhất, hãy giữ giá trị này ở mức thấp nhất có thể.
- **Detail Spread:** Phân bố kích thước dọc theo chiều dài của bộ đệm froxel. Giá trị cao hơn sẽ nén các froxel lại gần camera hơn và đặt nhiều chi tiết hơn ở gần camera.
- **Ambient Inject:** Tỷ lệ cường độ ánh sáng môi trường được sử dụng trong sương mù thể tích. Giá trị ``0.0`` có nghĩa là ánh sáng môi trường sẽ không ảnh hưởng đến sương mù thể tích. Khi được đặt cao hơn ``0.0``, thuộc tính này gây ra một chi phí hiệu năng nhỏ.
- **Sky Affect:** Kiểm soát mức độ sương mù thể tích được vẽ lên bầu trời nền. Nếu đặt thành ``0.0``, sương mù thể tích sẽ hoàn toàn không ảnh hưởng đến việc render bầu trời (bao gồm cả FogVolumes).

Có thêm hai thuộc tính trong phần **Temporal Reprojection**:

- **Temporal Reprojection > Enabled:** Bật temporal reprojection trong sương mù thể tích. Temporal reprojection trộn sương mù thể tích của khung hình hiện tại với sương mù thể tích của khung hình trước để làm mượt các cạnh răng cưa. Chi phí hiệu năng là tối thiểu, tuy nhiên tính năng này khiến các FogVolumes và Light3Ds đang di chuyển bị "bóng ma" và để lại vệt phía sau. Khi bật temporal reprojection, hãy cố gắng tránh di chuyển FogVolumes hoặc Light3Ds quá nhanh. Các hiệu ứng chiếu sáng động có thời gian tồn tại ngắn nên đặt **Volumetric Fog Energy** thành ``0.0`` để tránh bóng ma.
- **Temporal Reprojection > Amount:** Mức độ trộn khung hình trước với khung hình hiện tại. Giá trị cao hơn tạo ra sương mù thể tích mượt hơn, nhưng khiến hiện tượng "bóng ma" nghiêm trọng hơn nhiều. Giá trị thấp hơn làm giảm bóng ma, nhưng có thể khiến hiện tượng jitter theo thời gian giữa các khung hình trở nên visible.

.. note::

    Không giống sương mù không thể tích, sương mù thể tích có phạm vi *hữu hạn*. Điều này có nghĩa là sương mù thể tích không thể bao phủ hoàn toàn một thế giới rộng lớn, vì cuối cùng nó sẽ không còn được render ở khoảng cách xa.

    Nếu muốn che khuất các khu vực ở xa khỏi người chơi, bạn nên bật đồng thời cả sương mù không thể tích và sương mù thể tích, rồi điều chỉnh mật độ của chúng cho phù hợp.

Tương tác của ánh sáng với sương mù thể tích
--------------------------------------------

Để mô phỏng hành vi tán xạ ánh sáng của sương mù trong thực tế, mọi loại ánh sáng đều tương tác với sương mù thể tích. Có thể điều chỉnh mức độ mỗi ánh sáng ảnh hưởng đến sương mù thể tích bằng thuộc tính **Volumetric Fog Energy** trên từng ánh sáng. Bật bóng đổ trên một ánh sáng cũng khiến các bóng đổ đó hiển thị trên sương mù thể tích.

Nếu không muốn ánh sáng tương tác với sương mù vì lý do nghệ thuật, bạn có thể tắt tính năng này trên toàn cục bằng cách đặt **Volumetric Fog > Albedo** thành màu đen hoàn toàn trong resource Environment. Bạn cũng có thể tắt tương tác của ánh sáng với sương mù đối với từng ánh sáng cụ thể bằng cách đặt **Volumetric Fog Energy** của ánh sáng đó thành ``0``. Làm vậy cũng cải thiện hiệu năng đôi chút vì loại ánh sáng đó sẽ bị loại khỏi các phép tính sương mù thể tích.

Sử dụng sương mù thể tích như một giải pháp chiếu sáng thể tích
---------------------------------------------------------------

Dù không chính xác về mặt vật lý, bạn có thể điều chỉnh các thiết lập của sương mù thể tích để hoạt động như một giải pháp *chiếu sáng* thể tích. Điều này có nghĩa là các phần không được chiếu sáng của môi trường sẽ không còn bị sương mù làm tối, nhưng ánh sáng vẫn có thể khiến sương mù sáng hơn tại các khu vực cụ thể.

Bạn có thể thực hiện điều này bằng cách đặt mật độ sương mù thể tích thành giá trị nhỏ nhất được phép *lớn hơn 0* (``0.0001``), sau đó tăng thuộc tính **Volumetric Fog Energy** trên các ánh sáng lên những giá trị cao hơn nhiều so với mặc định để bù lại. Các giá trị từ ``200.0`` đến ``5000.0`` thường cho kết quả tốt trong trường hợp này.

.. image:: img/volumetric_fog_lighting.png

Cân bằng giữa hiệu năng và chất lượng
-------------------------------------

Có một số cài đặt dự án cho phép điều chỉnh hiệu năng và chất lượng của volumetric fog:

- **Rendering > Environment > Volumetric Fog > Volume Size:** Kích thước cơ sở được dùng để xác định kích thước của bộ đệm froxel trên trục X và trục Y của camera. Kích thước cuối cùng được điều chỉnh theo tỷ lệ khung hình của màn hình, vì vậy các giá trị thực tế có thể khác với giá trị đã thiết lập. Đặt kích thước lớn hơn để có sương mù chi tiết hơn, hoặc đặt kích thước nhỏ hơn để cải thiện hiệu năng.
- **Rendering > Environment > Volumetric Fog > Volume Depth:** Số lượng lát được sử dụng dọc theo chiều sâu của bộ đệm froxel cho volumetric fog. Số lượng thấp hơn sẽ hiệu quả hơn, nhưng có thể khiến các hiện tượng bất thường xuất hiện khi camera di chuyển.
- **Rendering > Environment > Volumetric Fog > Use Filter:** Bật tính năng lọc hiệu ứng volumetric fog trước khi tích hợp. Tính năng này làm mờ sương mù đáng kể, giúp giảm các chi tiết nhỏ, đồng thời làm mượt các cạnh gắt và hiện tượng răng cưa. Tắt tùy chọn này khi cần nhiều chi tiết hơn.

.. note::

    Volumetric fog có thể khiến hiện tượng phân dải xuất hiện trong viewport, đặc biệt ở các mức mật độ cao. Xem :ref:`doc_3d_rendering_limitations_color_banding` để biết hướng dẫn giảm hiện tượng phân dải.

Sử dụng fog volume cho volumetric fog cục bộ
--------------------------------------------

Đôi khi, bạn muốn giới hạn sương mù trong các khu vực cụ thể. Ngược lại, bạn có thể muốn sử dụng volumetric fog toàn cục nhưng loại trừ sương mù khỏi một số khu vực nhất định. Cả hai cách tiếp cận đều có thể thực hiện bằng các node FogVolume.

Dưới đây là hướng dẫn nhanh để sử dụng FogVolume:

- Hãy đảm bảo **Volumetric Fog** được bật trong các thuộc tính Environment. Nếu không muốn sử dụng volumetric fog toàn cục, hãy đặt **Density** của nó thành ``0.0``.
- Tạo một node FogVolume.
- Gán một FogMaterial mới cho thuộc tính **Material** của node FogVolume.
- Trong FogMaterial, đặt **Density** thành một giá trị dương để tăng mật độ bên trong FogVolume, hoặc một giá trị âm để trừ mật độ khỏi volumetric fog toàn cục.
- Định cấu hình phạm vi và hình dạng của FogVolume theo nhu cầu.

.. note::

    Các fog volume mỏng có thể bị nhấp nháy khi camera di chuyển hoặc xoay. Có thể giảm hiện tượng này bằng cách tăng cài đặt dự án **Rendering > Environment > Volumetric Fog > Volume Depth** (đổi lại là hiệu năng giảm) hoặc giảm **Length** trong các thuộc tính volumetric fog của Environment (không ảnh hưởng đến hiệu năng, nhưng làm giảm phạm vi sương mù). Ngoài ra, có thể làm FogVolume dày hơn và sử dụng mật độ thấp hơn trong **Material**.

Các thuộc tính của FogVolume
----------------------------

- **Extents:** Kích thước của FogVolume khi **Shape** là **Ellipsoid**, **Cone**, **Cylinder** hoặc **Box**. Nếu **Shape** là **Cone** hoặc **Cylinder**, hình nón/hình trụ sẽ được điều chỉnh để vừa với phạm vi. Không hỗ trợ co giãn không đồng nhất các hình nón/hình trụ thông qua thuộc tính **Extents**, nhưng bạn có thể co giãn node FogVolume.
- **Shape:** Hình dạng của FogVolume. Có thể đặt thành **Ellipsoid**, **Cone**, **Cylinder**, **Box** hoặc **World** (hoạt động như volumetric fog toàn cục).
- **Material:** Material được FogVolume sử dụng. Có thể là FogMaterial tích hợp sẵn hoặc ShaderMaterial tùy chỉnh (:ref:`doc_fog_shader`).

Sau khi chọn **New FogMaterial** trong thuộc tính **Material**, bạn có thể điều chỉnh các thuộc tính sau trong FogMaterial:

- **Density:** Mật độ của FogVolume. Các đối tượng đặc hơn sẽ đục hơn, nhưng có thể gặp các hiện tượng bất thường do lấy mẫu không đủ, trông giống như các sọc. Có thể sử dụng các giá trị âm để trừ sương mù khỏi các FogVolume khác hoặc volumetric fog toàn cục.
- **Albedo:** Color tán xạ đơn của FogVolume. Về bên trong, albedo của member được chuyển đổi thành tán xạ đơn, sau đó được hòa trộn cộng với các FogVolume khác và **Albedo** của volumetric fog toàn cục.
- **Emission:** Color của ánh sáng do FogVolume phát ra. Ánh sáng phát ra sẽ không chiếu sáng hoặc tạo bóng lên các đối tượng khác, nhưng có thể hữu ích để điều chỉnh Color của FogVolume độc lập với các nguồn sáng.
- **Height Falloff:** Tốc độ giảm mật độ của sương mù dựa trên độ cao khi độ cao tăng trong không gian thế giới. Falloff cao sẽ tạo ra sự chuyển tiếp gắt, trong khi falloff thấp sẽ tạo ra sự chuyển tiếp mượt hơn. Giá trị ``0.0`` tạo ra sương mù có mật độ đồng nhất. Ngưỡng độ cao được xác định bởi độ cao của FogVolume liên kết.
- **Edge Fade:** Độ cứng của các cạnh FogVolume. Giá trị cao hơn sẽ tạo ra các cạnh mềm hơn, trong khi giá trị thấp hơn sẽ tạo ra các cạnh cứng hơn.
- **Density Texture:** Texture 3D được dùng để điều chỉnh mật độ của FogVolume. Có thể dùng texture này để biến đổi mật độ sương mù bên trong FogVolume theo bất kỳ mẫu tĩnh nào. Đối với các hiệu ứng động, hãy cân nhắc sử dụng một
  :ref:`shader sương mù <doc_fog_shader>`. Bạn có thể import bất kỳ hình ảnh nào dưới dạng texture 3D bằng cách
  :ref:`thay đổi kiểu import của hình ảnh đó trong Import dock <doc_importing_images_changing_import_type>`.

Sử dụng texture mật độ nhiễu 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kể từ Godot 4.1, có một resource NoiseTexture3D có thể được dùng để tạo nhiễu 3D theo thủ tục. Resource này rất phù hợp với texture mật độ của FogMaterial, giúp tạo ra các hiệu ứng sương mù chi tiết hơn:

.. figure:: img/volumetric_fog_fog_material_density_texture.webp
   :alt: So sánh FogMaterial (không có và có texture mật độ)

   Ảnh chụp màn hình được thực hiện với cài đặt dự án **Volume Size** được đặt thành 192 để các chi tiết tần số cao hiển thị rõ hơn trong sương mù.

Để thực hiện việc này, hãy chọn thuộc tính **Density Texture** và chọn **New NoiseTexture3D**. Chỉnh sửa NoiseTexture3D này bằng cách nhấp vào nó, sau đó nhấp vào **Noise** ở cuối các thuộc tính NoiseTexture3D và chọn **New FastNoiseLite**. Điều chỉnh chiều rộng, chiều cao và chiều sâu của texture nhiễu theo kích thước fog volume của bạn.

Để cải thiện hiệu năng, bạn nên sử dụng kích thước texture nhỏ (64×64×64 hoặc thấp hơn), vì khó nhận thấy các chi tiết tần số cao trong FogVolume. Nếu muốn thể hiện các biến thiên mật độ chi tiết hơn, bạn sẽ cần tăng **Rendering > Environment > Volumetric Fog > Volume Size** trong cài đặt dự án, việc này sẽ ảnh hưởng đến hiệu năng.

.. note::

    **Color Ramp** của NoiseTexture3D ảnh hưởng đến các texture mật độ của FogMaterial, nhưng vì chỉ có kênh đỏ của texture được lấy mẫu nên chỉ kênh đỏ của color ramp ảnh hưởng đến mật độ thu được.

    Tuy nhiên, sử dụng color ramp sẽ *không* nhuộm màu thể tích sương theo texture. Bạn cần sử dụng custom shader đọc một Texture3D để đạt được điều này.

Shader FogVolume tùy chỉnh
--------------------------

Trang này chỉ đề cập đến các thiết lập tích hợp sẵn do FogMaterial cung cấp. Nếu cần tùy chỉnh hành vi của sương trong một node FogVolume, chẳng hạn như tạo sương động, bạn có thể tùy chỉnh diện mạo của các node FogVolume bằng :ref:`doc_fog_shader`.

Giả lập sương thể tích bằng quad
--------------------------------

Trong một số trường hợp, sử dụng QuadMesh được cấu hình đặc biệt có thể phù hợp hơn để thay thế cho sương thể tích:

- Quad hoạt động với mọi phương thức kết xuất, bao gồm Mobile và Compatibility.
- Quad không yêu cầu temporal reprojection để hiển thị mượt mà, nên phù hợp với các hiệu ứng động di chuyển nhanh như laser. Chúng cũng có thể biểu diễn các chi tiết nhỏ mà sương thể tích không thể thực hiện hiệu quả.
- Quad thường có chi phí hiệu năng thấp hơn sương thể tích.

Tuy nhiên, phương pháp này cũng có một vài nhược điểm:

- Hiệu ứng sương có độ giảm dần kém chân thực hơn, đặc biệt nếu camera đi vào trong sương.
- Có thể xảy ra vấn đề sắp xếp transparency khi các sprite chồng lên nhau.
- Hiệu năng không nhất thiết tốt hơn sương thể tích nếu có nhiều sprite ở gần camera.

Để tạo một sprite sương dựa trên QuadMesh:

1. Tạo một node MeshInstance3D với resource QuadMesh trong thuộc tính **Mesh**. Đặt kích thước theo mong muốn.
2. Tạo một StandardMaterial3D mới trong thuộc tính **Material** của mesh.
3. Trong StandardMaterial3D, đặt **Shading > Shading Mode** thành **Unshaded**, đặt **Billboard > Mode** thành **Enabled**, bật **Proximity Fade** và đặt **Distance Fade** thành **Pixel Alpha**.
4. Đặt **Albedo > Texture** thành texture bên dưới (nhấp chuột phải và chọn **Save as…**):

   .. image:: img/volumetric_fog_quad_mesh_texture.webp

5. *Sau khi* đặt texture albedo, đi đến dock Import, chọn texture rồi thay đổi chế độ nén thành **Lossless** để cải thiện chất lượng.

Màu của sương được đặt bằng thuộc tính **Albedo > Color**; mật độ của nó được đặt bằng kênh alpha của màu. Để đạt kết quả tốt nhất, bạn sẽ phải điều chỉnh **Proximity Fade > Distance** và **Distance Fade > Max Distance** tùy theo kích thước QuadMesh.

Bạn có thể để tính năng billboarding bị tắt nếu đặt quad sao cho tất cả các góc của nó nằm trong hình học đặc. Điều này có thể hữu ích khi tạo sương cho các mặt phẳng lớn mà camera không thể đi vào, chẳng hạn như các hố không đáy.
