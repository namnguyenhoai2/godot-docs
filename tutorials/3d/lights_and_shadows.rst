.. _doc_lights_and_shadows:

Ánh sáng và bóng đổ 3D
======================

Giới thiệu
----------

Các nguồn sáng phát ra ánh sáng, ánh sáng này kết hợp với vật liệu và tạo ra kết quả hiển thị. Ánh sáng trong một cảnh có thể đến từ một số loại nguồn:

- Từ chính vật liệu, dưới dạng màu phát xạ (dù không ảnh hưởng đến các đối tượng lân cận trừ khi đã được bake hoặc bật indirect lighting trong screen-space).
- Các light node: DirectionalLight3D, OmniLight3D, SpotLight3D và AreaLight3D.
- Ánh sáng môi trường trong :ref:`Environment <class_Environment>` hoặc
  :ref:`doc_reflection_probes`.
- Global illumination (:ref:`LightmapGI <doc_using_lightmap_gi>`,
  :ref:`VoxelGI <doc_using_voxel_gi>` hoặc :ref:`SDFGI <doc_using_sdfgi>`).

Màu phát xạ là một thuộc tính của vật liệu. Bạn có thể đọc thêm về thuộc tính này trong :ref:`doc_standard_material_3d` tutorial.

.. seealso::

    Bạn có thể so sánh cách hoạt động của nhiều loại ánh sáng khác nhau bằng `3D Lights and Shadows demo project <https://github.com/godotengine/godot-demo-projects/tree/master/3d/lights_and_shadows>`__.

Light node
----------

Có bốn loại light node: :ref:`class_DirectionalLight3D`,
:ref:`class_OmniLight3D`, :ref:`class_SpotLight3D` và :ref:`class_AreaLight3D`. Hãy xem các tham số chung của ánh sáng:

.. image:: img/light_params.png

Mỗi thuộc tính có một chức năng cụ thể:

- **Color:** Màu cơ bản của ánh sáng phát ra.
- **Energy:** Hệ số nhân năng lượng. Thuộc tính này hữu ích khi làm bão hòa ánh sáng hoặc làm việc với :ref:`doc_high_dynamic_range`.
- **Indirect Energy:** Hệ số nhân thứ cấp được dùng với ánh sáng gián tiếp (ánh sáng dội lại). Thuộc tính này hoạt động với :ref:`doc_using_lightmap_gi`, VoxelGI hoặc SDFGI.
- **Volumetric Fog Energy:** Hệ số nhân thứ cấp được dùng với sương mù thể tích. Thuộc tính này chỉ có tác dụng khi sương mù thể tích được bật.
- **Negative:** Ánh sáng trở thành phép trừ thay vì phép cộng. Đôi khi thuộc tính này hữu ích để bù thủ công cho một số góc tối.
- **Specular:** Ảnh hưởng đến cường độ của vùng specular trên các đối tượng chịu tác động của ánh sáng này. Khi bằng 0, ánh sáng này trở thành ánh sáng diffuse thuần túy.
- **Bake Mode:** Đặt chế độ bake cho ánh sáng. Xem :ref:`doc_using_lightmap_gi`.
- **Cull Mask:** Các đối tượng nằm trong những layer được chọn bên dưới sẽ chịu tác động của ánh sáng này. Lưu ý rằng các đối tượng bị vô hiệu hóa thông qua cull mask này vẫn đổ bóng. Nếu không muốn các đối tượng bị vô hiệu hóa đổ bóng, hãy điều chỉnh thuộc tính **Cast Shadow** trên GeometryInstance3D thành giá trị mong muốn.

.. seealso::

    Xem :ref:`doc_physical_light_and_camera_units` nếu bạn muốn sử dụng các đơn vị trong thế giới thực để cấu hình cường độ và nhiệt độ màu của ánh sáng.

Giới hạn số lượng ánh sáng
--------------------------

Khi sử dụng Forward+ renderer, Godot sử dụng phương pháp *clustering* cho lighting theo thời gian thực. Có thể thêm số lượng ánh sáng tùy ý (miễn là hiệu năng cho phép). Tuy nhiên, vẫn có giới hạn mặc định là 512 *clustered elements* có thể xuất hiện trong chế độ xem hiện tại của camera. Một clustered element có thể là omni light, spot light, area light, :ref:`decal <doc_using_decals>` hoặc một
:ref:`reflection probe <doc_reflection_probes>`.
Bạn có thể tăng giới hạn này bằng cách điều chỉnh :ref:`Max Clustered Elements <class_ProjectSettings_property_rendering/limits/cluster_builder/max_clustered_elements>` trong **Project Settings > Rendering > Limits > Cluster Builder**.

Khi sử dụng Mobile renderer, mỗi mesh resource bị giới hạn ở 8 OmniLights + 8 SpotLights. Ngoài ra, chế độ xem hiện tại của camera bị giới hạn ở 256 OmniLights + 256 SpotLights có thể được render. Hiện tại không thể thay đổi các giới hạn này.

Khi sử dụng Compatibility renderer, mỗi mesh resource có thể render tối đa 8 OmniLights + 8 SpotLights. Có thể tăng giới hạn này trong Project Settings nâng cao bằng cách điều chỉnh
:ref:`Max Renderable Elements <class_ProjectSettings_property_rendering/limits/opengl/max_renderable_elements>` và/hoặc :ref:`Max Lights per Object <class_ProjectSettings_property_rendering/limits/opengl/max_lights_per_object>` trong **Rendering > Limits > OpenGL**, với cái giá phải trả là hiệu năng giảm và thời gian biên dịch shader lâu hơn. Bạn cũng có thể giảm giới hạn để rút ngắn thời gian biên dịch shader và cải thiện đôi chút hiệu năng.

Với tất cả phương thức render, có thể hiển thị tối đa 8 DirectionalLights cùng lúc. Tuy nhiên, mỗi DirectionalLight bổ sung có bật bóng đổ sẽ làm giảm độ phân giải bóng hiệu dụng của từng DirectionalLight. Điều này là do directional shadow atlas được dùng chung giữa tất cả ánh sáng.

Nếu vượt quá giới hạn render, các ánh sáng sẽ bắt đầu xuất hiện rồi biến mất khi camera di chuyển, gây mất tập trung. Bật **Distance Fade** trên các light node có thể giúp giảm vấn đề này đồng thời cải thiện hiệu năng. Chia mesh thành các phần nhỏ hơn cũng có thể hữu ích, đặc biệt đối với geometry của level (đồng thời cải thiện hiệu quả culling).

Nếu cần render nhiều ánh sáng hơn mức renderer cho phép, hãy cân nhắc sử dụng :ref:`baked lightmaps <doc_using_lightmap_gi>` với bake mode của ánh sáng được đặt thành **Static**. Điều này cho phép bake hoàn toàn các ánh sáng, đồng thời giúp render chúng nhanh hơn nhiều. Bạn cũng có thể sử dụng vật liệu phát xạ với bất kỳ kỹ thuật
:ref:`global illumination <doc_introduction_to_global_illumination>` nào để thay thế các light node phát sáng trên một khu vực rộng.

Shadow mapping
--------------

Ánh sáng có thể tùy chọn đổ bóng. Điều này giúp chúng trông chân thực hơn (ánh sáng không chiếu tới các khu vực bị che khuất), nhưng có thể gây tốn hiệu năng hơn. Có một danh sách các tham số bóng đổ chung, mỗi tham số cũng có một chức năng cụ thể:

- **Enabled:** Chọn để bật shadow mapping cho ánh sáng này.
- **Opacity:** Các khu vực bị che khuất sẽ tối đi theo hệ số opacity này. Theo mặc định, bóng đổ hoàn toàn opaque, nhưng có thể thay đổi để làm bóng đổ trong mờ đối với một ánh sáng nhất định.
- **Bias:** Khi tham số này quá thấp, hiện tượng tự đổ bóng sẽ xảy ra. Khi quá cao, bóng sẽ tách khỏi các đối tượng tạo bóng. Hãy điều chỉnh đến giá trị phù hợp nhất với bạn.
- **Normal Bias:** Khi tham số này quá thấp, hiện tượng tự đổ bóng sẽ xảy ra. Khi quá cao, bóng có vẻ lệch khỏi các đối tượng tạo bóng. Hãy điều chỉnh đến giá trị phù hợp nhất với bạn.
- **Transmittance Bias:** Khi tham số này quá thấp, hiện tượng tự đổ bóng sẽ xảy ra trên các vật liệu đã bật transmittance. Khi quá cao, bóng sẽ không tác động nhất quán lên các vật liệu đã bật transmittance. Hãy điều chỉnh đến giá trị phù hợp nhất với bạn.
- **Reverse Cull Face:** Một số cảnh hoạt động tốt hơn khi shadow mapping được render với thao tác culling mặt bị đảo ngược.
- **Blur:** Nhân bán kính làm mờ bóng đổ của đèn này. Tùy chọn này hoạt động với cả shadow mapping truyền thống và contact-hardening shadows (các đèn có **Angular Distance** hoặc **Size** lớn hơn ``0.0``). Giá trị cao hơn tạo ra bóng mềm hơn, đồng thời bóng cũng có vẻ ổn định hơn theo thời gian đối với các vật thể chuyển động. Nhược điểm của việc tăng độ mờ bóng là hoa văn nhiễu dùng để lọc sẽ dễ nhận thấy hơn. Xem thêm :ref:`doc_lights_and_shadows_shadow_filter_mode`.
- **Caster Mask:** Chỉ các vật thể thuộc những layer này mới đổ bóng. Lưu ý rằng mask này không ảnh hưởng đến việc bóng được đổ *lên* những vật thể nào.

.. image:: img/lights_and_shadows_blur.webp

Điều chỉnh shadow bias
~~~~~~~~~~~~~~~~~~~~~~

Dưới đây là hình ảnh minh họa việc điều chỉnh bias. Các giá trị mặc định phù hợp với hầu hết trường hợp, nhưng nhìn chung còn tùy thuộc vào kích thước và độ phức tạp của hình học.

Nếu **Shadow Bias** hoặc **Shadow Normal Bias** được đặt quá thấp đối với một đèn nhất định, bóng sẽ bị "lem" lên các vật thể. Điều này khiến diện mạo dự kiến của đèn bị tối đi và được gọi là *shadow acne*:

.. image:: img/lights_and_shadows_acne.webp

Ngược lại, nếu **Shadow Bias** hoặc **Shadow Normal Bias** được đặt quá cao đối với một đèn nhất định, bóng có thể trông như bị tách khỏi vật thể. Hiện tượng này được gọi là *peter-panning*:

.. image:: img/lights_and_shadows_peter_panning.webp

Nhìn chung, nên tăng **Shadow Normal Bias** thay vì tăng **Shadow Bias**. Việc tăng **Shadow Normal Bias** không gây ra hiện tượng peter-panning nhiều như khi tăng **Shadow Bias**, nhưng vẫn có thể giải quyết hiệu quả hầu hết vấn đề shadow acne. Nhược điểm của việc tăng **Shadow Normal Bias** là có thể khiến bóng trông mỏng hơn đối với một số vật thể.

Mọi vấn đề liên quan đến bias đều có thể được khắc phục bằng cách
:ref:`tăng độ phân giải của shadow map <doc_lights_and_shadows_balancing_performance_and_quality>`, nhưng sẽ làm giảm hiệu năng.

.. note::

    Điều chỉnh các thiết lập shadow mapping là cả một nghệ thuật – không có thiết lập nào phù hợp với mọi trường hợp. Để đạt được hình ảnh đẹp nhất, bạn có thể cần sử dụng các giá trị shadow bias khác nhau cho từng đèn.

**Lưu ý về thay đổi diện mạo**: Khi bật bóng cho một đèn, hãy lưu ý rằng diện mạo của đèn có thể thay đổi so với khi được render không có bóng trong compatibility renderer. Do những hạn chế của các thiết bị di động cũ, bóng được triển khai bằng phương pháp render nhiều pass, vì vậy các đèn có bóng được render trong không gian sRGB thay vì không gian tuyến tính. Thay đổi không gian render này đôi khi có thể làm thay đổi đáng kể diện mạo của đèn. Để đạt được diện mạo tương tự như đèn không có bóng, bạn có thể cần điều chỉnh thiết lập energy của đèn.

.. _doc_lights_and_shadows_directional_light:

Đèn định hướng
--------------

Đây là loại đèn phổ biến nhất, đại diện cho một nguồn sáng ở rất xa (chẳng hạn như mặt trời). Đây cũng là loại đèn có chi phí tính toán thấp nhất và nên được sử dụng bất cứ khi nào có thể (mặc dù shadow map của nó không phải loại có chi phí tính toán thấp nhất, nhưng sẽ nói thêm về điều đó sau).

Directional light mô phỏng vô số tia sáng song song bao phủ toàn bộ cảnh. Node directional light được biểu diễn bằng một mũi tên lớn chỉ hướng của các tia sáng. Tuy nhiên, vị trí của node hoàn toàn không ảnh hưởng đến việc chiếu sáng và có thể ở bất kỳ đâu.

.. image:: img/light_directional.png

Mọi mặt có mặt trước bị các tia sáng chiếu vào đều được chiếu sáng, còn các mặt khác vẫn tối. Không giống hầu hết các loại đèn khác, directional light không có tham số cụ thể.

Directional light cũng cung cấp thuộc tính **Angular Distance**, xác định kích thước góc của đèn theo độ. Tăng giá trị này lên trên ``0.0`` sẽ làm bóng mềm hơn ở khoảng cách xa hơn so với vật thể đổ bóng, đồng thời cũng ảnh hưởng đến diện mạo của mặt trời trong các vật liệu bầu trời procedural. Đây được gọi là bóng *contact-hardening* (còn gọi là PCSS).

Để tham khảo, khoảng cách góc của Mặt trời khi nhìn từ Trái đất xấp xỉ ``0.5``. Loại bóng này tốn nhiều tài nguyên, vì vậy hãy xem các khuyến nghị trong :ref:`doc_lights_and_shadows_pcss_recommendations` nếu đặt giá trị này cao hơn ``0.0`` trên các đèn đã bật bóng.

Shadow mapping cho directional light
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để tính shadow map, cảnh được render (chỉ có depth) từ góc nhìn trực giao bao phủ toàn bộ cảnh (hoặc đến khoảng cách tối đa). Tuy nhiên, cách tiếp cận này có một vấn đề: các vật thể gần camera hơn sẽ nhận bóng có độ phân giải thấp, khiến bóng có thể trông như các khối vuông.

Để khắc phục điều này, một kỹ thuật có tên *Parallel Split Shadow Maps* (PSSM) được sử dụng. Kỹ thuật này chia view frustum thành 2 hoặc 4 vùng. Mỗi vùng có shadow map riêng. Nhờ đó, các vùng nhỏ gần người xem có thể có cùng độ phân giải bóng như một vùng lớn ở xa. Khi bật bóng cho DirectionalLight3D, chế độ bóng mặc định là PSSM với 4 vùng chia. Trong trường hợp một vật thể đủ lớn để xuất hiện trong cả bốn vùng chia, số draw call sẽ tăng. Cụ thể, vật thể đó sẽ được render tổng cộng năm lần: một lần cho mỗi trong bốn vùng bóng chia và một lần cho bước render cảnh cuối cùng. Điều này có thể ảnh hưởng đến hiệu năng; việc hiểu hành vi này rất quan trọng để tối ưu hóa cảnh và quản lý kỳ vọng về hiệu năng.

.. image:: img/lights_and_shadows_pssm_explained.webp

Nhờ vậy, bóng trở nên chi tiết hơn:

.. image:: img/lights_and_shadows_directional_mode.webp

Để kiểm soát PSSM, một số tham số được cung cấp:

.. image:: img/lights_and_shadows_directional_shadow_params.webp

Khoảng cách của mỗi vùng chia được kiểm soát tương đối so với camera far (hoặc shadow **Max Distance** nếu lớn hơn ``0.0``). ``0.0`` là vị trí mắt và ``1.0`` là nơi bóng kết thúc tại một khoảng cách nhất định. Các vùng chia nằm ở giữa. Các giá trị mặc định nhìn chung hoạt động tốt, nhưng thường điều chỉnh vùng chia đầu tiên một chút để tăng chi tiết cho các vật thể ở gần (chẳng hạn như nhân vật trong game góc nhìn người thứ ba).

Luôn nhớ đặt shadow **Max Distance** phù hợp với nhu cầu của cảnh. Khoảng cách tối đa thấp hơn sẽ tạo ra bóng đẹp hơn và hiệu năng tốt hơn, vì sẽ có ít vật thể cần được đưa vào quá trình render bóng hơn. Bạn cũng có thể điều chỉnh **Fade Start** để kiểm soát mức độ mạnh của hiệu ứng bóng mờ dần theo khoảng cách. Đối với các cảnh mà **Max Distance** bao phủ hoàn toàn cảnh tại mọi vị trí của camera, bạn có thể tăng **Fade Start** lên ``1.0`` để ngăn bóng mờ dần theo khoảng cách. Không nên làm vậy trong các cảnh mà **Max Distance** không bao phủ hoàn toàn cảnh, vì bóng sẽ có vẻ đột ngột bị cắt ở xa.

Đôi khi, sự chuyển tiếp giữa một vùng chia và vùng tiếp theo có thể trông không đẹp. Để khắc phục, có thể bật tùy chọn **Blend Splits**, đánh đổi chi tiết và hiệu năng để có sự chuyển tiếp mượt mà hơn:

.. image:: img/blend_splits.png

Có thể sử dụng tham số **Shadow > Normal Bias** để khắc phục các trường hợp đặc biệt về tự đổ bóng khi vật thể vuông góc với ánh sáng. Nhược điểm duy nhất là nó khiến bóng mỏng hơn một chút. Trong hầu hết trường hợp, hãy cân nhắc tăng **Shadow > Normal Bias** trước khi tăng **Shadow > Bias**.

Cuối cùng, **Pancake Size** là một thuộc tính có thể điều chỉnh để khắc phục tình trạng thiếu bóng khi sử dụng các vật thể lớn với mesh chưa được chia nhỏ. Chỉ thay đổi giá trị này nếu bạn nhận thấy bóng bị thiếu mà nguyên nhân không liên quan đến các vấn đề về shadow bias.

.. _doc_lights_and_shadows_omni_light:

Đèn omni
--------

Đèn omni là một nguồn sáng điểm phát ánh sáng hình cầu theo mọi hướng trong phạm vi bán kính nhất định.

.. image:: img/light_omni.png

Trong thực tế, độ suy giảm ánh sáng là một hàm nghịch đảo, nghĩa là đèn omni không có bán kính. Đây là một vấn đề vì việc tính toán nhiều đèn omni sẽ trở nên tốn tài nguyên.

Để giải quyết vấn đề này, tham số **Range** được thêm vào cùng với một hàm suy giảm.

.. image:: img/light_omni_params.png

Hai tham số này cho phép điều chỉnh cách hiệu ứng hoạt động về mặt hình ảnh để tìm ra kết quả đẹp mắt.

.. image:: img/light_attenuation.png

Tham số **Size** cũng có trong OmniLight3D. Việc tăng giá trị này sẽ làm ánh sáng mờ dần chậm hơn và bóng đổ trở nên mờ hơn khi ở xa vật thể đổ bóng. Có thể dùng tham số này để phần nào mô phỏng đèn vùng. Đây được gọi là bóng đổ *contact-hardening* (còn gọi là PCSS). Loại bóng đổ này tốn nhiều tài nguyên, vì vậy hãy xem các khuyến nghị trong
:ref:`doc_lights_and_shadows_pcss_recommendations` nếu đặt giá trị này cao hơn ``0.0`` trên các đèn bật bóng đổ.

.. image:: img/lights_and_shadows_pcss.webp

Ánh xạ bóng đổ của đèn omni
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Ánh xạ bóng đổ của đèn omni tương đối đơn giản. Vấn đề chính cần cân nhắc là thuật toán được dùng để kết xuất bóng đổ.

Bóng đổ của đèn omni có thể được kết xuất bằng **Dual Paraboloid** hoặc ánh xạ **Cube**. **Dual Paraboloid** kết xuất nhanh, nhưng có thể gây biến dạng, còn **Cube** chính xác hơn nhưng chậm hơn. Mặc định là **Cube**, nhưng hãy cân nhắc đổi thành **Dual Paraboloid** cho các đèn mà sự khác biệt về hình ảnh không đáng kể.

.. image:: img/lights_and_shadows_dual_parabolid_vs_cubemap.webp

Nếu các đối tượng được kết xuất chủ yếu có hình dạng bất quy tắc và được chia nhỏ, Dual Paraboloid thường là đủ. Trong mọi trường hợp, vì các bóng đổ này được lưu vào shadow atlas (sẽ nói thêm ở cuối), hiệu năng trong hầu hết các cảnh có thể không khác biệt.

Đèn omni đã bật bóng đổ có thể sử dụng projector. Texture projector sẽ *multiply* màu của đèn với màu tại một điểm nhất định trên texture. Do đó, đèn thường sẽ trông tối hơn sau khi được gán texture projector; bạn có thể tăng **Energy** để bù lại.

Texture projector của đèn omni yêu cầu ánh xạ panorama 360° đặc biệt, tương tự như texture :ref:`class_PanoramaSkyMaterial`.

Với texture projector bên dưới, kết quả thu được như sau:

.. image:: img/lights_and_shadows_omni_projector_example.webp

.. image:: img/lights_and_shadows_omni_projector.webp

.. tip::

    Nếu bạn đã có projector omni ở dạng ảnh cubemap, bạn có thể dùng `công cụ chuyển đổi trên web này <https://danilw.github.io/GLSL-howto/cubemap_to_panorama_js/cubemap_to_panorama.html>`__ để chuyển đổi chúng thành một ảnh panorama duy nhất.

.. _doc_lights_and_shadows_spot_light:

Đèn spot
--------

Đèn spot tương tự đèn omni, nhưng chỉ phát ánh sáng trong một hình nón (hay "góc cắt"). Chúng hữu ích để mô phỏng đèn pin, đèn xe, đèn phản xạ, đèn chiếu điểm, v.v. Loại đèn này cũng suy giảm theo hướng ngược với hướng mà nó chiếu.

Đèn spot dùng chung các tham số **Range**, **Attenuation** và **Size** với OmniLight3D, đồng thời bổ sung hai tham số:

- **Angle:** Góc khẩu độ của đèn.
- **Angle Attenuation:** Độ suy giảm hình nón, giúp làm mềm các viền của hình nón.

Ánh xạ bóng đổ của đèn spot
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Đèn spot có cùng các tham số ánh xạ bóng đổ như đèn omni. Việc kết xuất shadow map của đèn spot nhanh hơn đáng kể so với đèn omni, vì chỉ cần kết xuất một texture bóng đổ (thay vì kết xuất 6 mặt, hoặc 2 mặt ở chế độ dual paraboloid).

Đèn spot đã bật bóng đổ có thể sử dụng projector. Texture projector sẽ *multiply* màu của đèn với màu tại một điểm nhất định trên texture. Do đó, đèn thường sẽ trông tối hơn sau khi được gán texture projector; bạn có thể tăng **Energy** để bù lại.

Không giống projector của đèn omni, texture projector của đèn spot không cần tuân theo định dạng đặc biệt để hiển thị chính xác. Nó sẽ được ánh xạ theo cách tương tự như một
:ref:`decal <doc_using_decals>`.

Với texture projector bên dưới, kết quả thu được như sau:

.. image:: img/lights_and_shadows_spot_projector_example.webp

.. image:: img/lights_and_shadows_spot_projector.webp

.. note::

    Đèn spot có góc rộng sẽ có bóng đổ chất lượng thấp hơn đèn spot có góc hẹp, vì shadow map được trải trên một bề mặt lớn hơn. Ở các góc rộng hơn 89 độ, bóng đổ của đèn spot sẽ ngừng hoạt động hoàn toàn. Nếu cần bóng đổ cho các đèn có góc rộng hơn, hãy dùng đèn omni thay thế.

.. _doc_lights_and_shadows_area_light:

Đèn vùng
--------

Đôi khi, bạn muốn ánh sáng phát ra từ một vùng lớn thay vì một điểm duy nhất. Đèn vùng hữu ích để mô phỏng ánh sáng mềm, khuếch tán, chẳng hạn như ánh sáng phát ra từ cửa sổ hoặc biển quảng cáo được chiếu sáng.

Godot cung cấp node :ref:`class_AreaLight3D` cho mục đích này; node phát ánh sáng từ một vùng hình chữ nhật. Node này chỉ phát ánh sáng và không có biểu diễn trực quan nào khác trong cảnh. Các ảnh chụp màn hình bên dưới sử dụng node :ref:`class_Sprite3D` làm node con của đèn vùng để phục vụ mục đích trực quan hóa.

.. warning::

    Đây là loại đèn tốn nhiều tài nguyên nhất khi kết xuất theo thời gian thực. Nên sử dụng tiết chế, đặc biệt khi bật bóng đổ. Chỉ nên dùng chúng cho các cảnh điện ảnh hoặc khi nhắm đến các thiết bị cao cấp.

    Trong Forward+, ngay khi một đèn vùng hiển thị trong viewing frustum, nó sẽ làm phát sinh thêm chi phí hiệu năng trên **tất cả** đối tượng được kết xuất trong cảnh, kể cả những đối tượng không bị đèn vùng chiếu tới. Sự đánh đổi này cho phép kết xuất nhiều đèn vùng hơn (clustered lighting).

    Trong Mobile và Compatibility, chỉ những đối tượng được đèn vùng chiếu tới mới phát sinh thêm chi phí hiệu năng.

Đèn vùng cũng có thể đổ bóng, với vùng nửa tối biến đổi được mô phỏng mặc định bằng
:ref:`PCSS <doc_lights_and_shadows_pcss_recommendations>`. Kích thước vùng nửa tối này có thể được điều khiển bằng thuộc tính **Size** của Light3D. Hiệu ứng này có thể khá tốn tài nguyên, vì vậy có thể tắt bằng cách đặt **Size** thành ``0.0``.

.. note::

    Bóng đổ của đèn vùng có thể trông không chính xác nếu đối tượng đổ bóng không có đủ phân khu và ở rất gần đèn vùng. Đây cũng là hạn chế của chế độ bóng đổ Dual Paraboloid trên đèn omni.

.. image:: img/lights_and_shadows_area_example.webp

.. note::

    Vì đèn vùng khó mô phỏng trong trình kết xuất raster theo thời gian thực, chúng có một số hạn chế.

    Đối với các nguồn sáng nhỏ, bạn có thể sẽ nhận được kết quả tốt hơn khi dùng đèn điểm. Bóng đổ từ đèn vùng chỉ là các phép xấp xỉ thô, vì chúng được tính như thể là đèn điểm và có thể bị biến dạng ở các cạnh. Để có kết quả tốt hơn, hãy đảm bảo các mesh trong phạm vi của đèn được chia đủ nhỏ.

    Đèn vùng bị rò rỉ ánh sáng ở mặt sau của hình học nằm gần phía trước chúng khi nhìn theo góc tiếp tuyến, vì vậy hãy cẩn thận khi đặt chúng.

    Cuối cùng, không phải mọi đặc tính vật liệu đều được hỗ trợ đầy đủ; đèn vùng thực tế chỉ bị giới hạn ở việc đổ bóng khuếch tán Lambertian và bóng phản chiếu GGX, trong khi vật liệu bất đẳng hướng sẽ hiển thị như vật liệu đẳng hướng. Đổ bóng theo vertex cũng chưa được triển khai cho đèn vùng.

Đèn vùng phát sáng trong một vùng hình chữ nhật được xác định bởi thuộc tính **Area > Size** (không nên nhầm với thuộc tính **Size** chung của Light3D). Để có kết quả chính xác về mặt vật lý, bạn nên thay đổi kích thước vùng này cho khớp với kích thước của nguồn sáng thực tế mà bạn đang mô phỏng. Ví dụ, nếu bạn mô phỏng một ống neon dài 1 mét và rộng 10 cm, hãy đặt kích thước vùng thành ``(1, 0.1)`` rồi điều chỉnh năng lượng cho phù hợp.

Theo mặc định, năng lượng của đèn được chuẩn hóa: vùng càng lớn thì đèn càng yếu. Điều này cho phép bạn thay đổi kích thước vùng mà không cần điều chỉnh năng lượng để bù lại, rất hữu ích cho animation. Bạn có thể tắt hành vi này bằng cách bỏ chọn **Area > Normalize Energy** nếu muốn năng lượng độc lập với kích thước vùng.

Vùng hình chữ nhật có thể tùy chọn sử dụng texture. Điều này có thể được dùng hiệu quả để biến hình dạng của đèn thành bất kỳ hình dạng 2D nào hoặc nhuộm đèn bằng các màu khác nhau. Kênh alpha của texture được xem là màu đen (không có ánh sáng đi qua). Texture của đèn vùng sẽ hiển thị trong các phản xạ tùy theo độ nhám của bề mặt. Hành vi này khác với các projector omni/spot, vì texture không được chiếu trực tiếp lên toàn bộ ánh sáng khuếch tán.

Khi sử dụng các texture trong suốt hoặc có màu đen ở gần các cạnh, bạn có thể muốn chừa một khoảng cách vài pixel để đảm bảo texture được làm mờ mượt mà.

.. image:: img/lights_and_shadows_area_texture.webp

.. note::

    Việc thay đổi texture của đèn vùng trong runtime có thể tốn kém, đặc biệt nếu texture lớn.

    Để giảm ảnh hưởng đến hiệu năng khi chuyển texture trong runtime, hãy đảm bảo mỗi chiều của texture vùng либо là bội số của 128 pixel hoặc là lũy thừa của hai. Điều này loại bỏ nhu cầu thực hiện một bước scale, vốn làm chậm quá trình thay đổi texture. Texture không nhất thiết phải có dạng hình vuông để đạt hiệu quả tối ưu. Các kích thước texture tối ưu gồm 32×64, 128×128 và 256×384.

    Texture cho đèn vùng không được hỗ trợ trong Compatibility renderer.

.. _doc_lights_and_shadows_shadow_atlas:

Atlas bóng đổ
-------------

Không giống đèn Directional, vốn có texture bóng đổ riêng, đèn omni, spot và vùng được gán vào các slot của shadow atlas. Atlas này có thể được cấu hình trong Project Settings nâng cao (**Rendering > Lights And Shadows > Positional Shadow**).

Độ phân giải áp dụng cho toàn bộ shadow atlas. Atlas này được chia thành bốn góc phần tư:

.. image:: img/lights_and_shadows_shadow_quadrants.webp

Mỗi góc phần tư có thể được chia nhỏ để phân bổ bất kỳ số lượng shadow map nào; cách chia mặc định như sau:

.. image:: img/lights_and_shadows_shadow_quadrants2.webp

Shadow atlas phân bổ không gian như sau:

- Kích thước shadow map lớn nhất (khi không sử dụng subdivision) biểu thị một đèn có kích thước bằng màn hình (hoặc lớn hơn).
- Các subdivision (map nhỏ hơn) biểu thị bóng đổ của những đèn ở xa tầm nhìn hơn và có kích thước tương ứng nhỏ hơn.

Ở mỗi frame, quy trình sau được thực hiện cho tất cả đèn:

1. Kiểm tra xem đèn có nằm trong slot có kích thước phù hợp hay không. Nếu không, render lại đèn và chuyển đèn vào slot lớn hơn/nhỏ hơn.
2. Kiểm tra xem có đối tượng nào ảnh hưởng đến shadow map đã thay đổi hay không. Nếu có, render lại đèn.
3. Nếu không điều nào ở trên xảy ra thì không làm gì cả và giữ nguyên bóng đổ.

Nếu các slot trong một góc phần tư đã đầy, các đèn sẽ được đẩy về những slot nhỏ hơn, tùy theo kích thước và khoảng cách. Nếu tất cả slot trong mọi góc phần tư đều đầy, một số đèn sẽ không thể render bóng đổ ngay cả khi đã bật bóng đổ cho chúng.

Chiến lược phân bổ bóng đổ mặc định cho phép render tối đa 88 đèn có bật bóng đổ trong camera frustum (4 + 4 + 16 + 64):

1. Góc phần tư đầu tiên và có độ chi tiết cao nhất có thể lưu trữ 4 bóng đổ.
2. Góc phần tư thứ hai có thể lưu trữ thêm 4 bóng đổ.
3. Góc phần tư thứ ba có thể lưu trữ 16 bóng đổ với độ chi tiết thấp hơn.
4. Góc phần tư thứ tư và có độ chi tiết thấp nhất có thể lưu trữ 64 bóng đổ với độ chi tiết thậm chí còn thấp hơn.

Sử dụng số lượng bóng đổ trên mỗi góc phần tư lớn hơn cho phép hỗ trợ tổng số đèn có bật bóng đổ nhiều hơn, đồng thời cải thiện hiệu năng (vì bóng đổ của mỗi đèn sẽ được render ở độ phân giải thấp hơn). Tuy nhiên, việc tăng số lượng bóng đổ trên mỗi góc phần tư sẽ phải đánh đổi bằng chất lượng bóng đổ thấp hơn.

Trong một số trường hợp, bạn có thể muốn sử dụng một chiến lược phân bổ khác. Ví dụ, trong một game nhìn từ trên xuống, nơi tất cả đèn có kích thước gần như nhau, bạn có thể đặt tất cả góc phần tư có cùng subdivision để mọi đèn có bóng đổ với mức chất lượng tương tự.

.. _doc_lights_and_shadows_balancing_performance_and_quality:

Cân bằng hiệu năng và chất lượng
--------------------------------

Việc render bóng đổ là một chủ đề quan trọng đối với hiệu năng rendering 3D. Điều quan trọng là đưa ra lựa chọn phù hợp để tránh tạo ra các điểm nghẽn.

Có thể thay đổi các thiết lập chất lượng bóng đổ Directional trong runtime bằng cách gọi các :ref:`class_RenderingServer` thích hợp.

Có thể thay đổi các thiết lập chất lượng bóng đổ theo vị trí (omni/spot/area) trong runtime trên :ref:`class_Viewport` gốc.

Kích thước shadow map
~~~~~~~~~~~~~~~~~~~~~

Độ phân giải bóng đổ cao tạo ra bóng sắc nét hơn, nhưng phải trả giá đáng kể về hiệu năng. Cũng cần lưu ý rằng *bóng sắc nét hơn không phải lúc nào cũng chân thực hơn*. Trong hầu hết trường hợp, nên giữ giá trị mặc định là ``4096`` hoặc giảm xuống ``2048`` đối với GPU cấp thấp.

Nếu bóng đổ theo vị trí trở nên quá mờ sau khi giảm kích thước shadow map, bạn có thể khắc phục bằng cách điều chỉnh
các góc phần tư của :ref:`shadow atlas <doc_lights_and_shadows_shadow_atlas>` để chứa ít bóng đổ hơn. Điều này cho phép render mỗi bóng đổ ở độ phân giải cao hơn.

.. _doc_lights_and_shadows_shadow_filter_mode:

Chế độ lọc bóng đổ
~~~~~~~~~~~~~~~~~~

Tại đây có thể chọn một số thiết lập chất lượng shadow map. Tùy chọn mặc định **Soft Low** là sự cân bằng tốt giữa hiệu năng và chất lượng đối với các scene có texture chi tiết, vì độ chi tiết của texture sẽ giúp làm cho mẫu dithering ít dễ nhận thấy hơn.

Tuy nhiên, trong các project có texture ít chi tiết hơn, mẫu dithering của bóng đổ có thể dễ nhìn thấy hơn. Để ẩn mẫu này, bạn có thể bật
:ref:`doc_3d_antialiasing_taa`, :ref:`doc_3d_antialiasing_fsr2`,
:ref:`doc_3d_antialiasing_fxaa`, hoặc tăng chất lượng bộ lọc bóng đổ lên **Soft Medium** hoặc cao hơn.

Thiết lập **Soft Very Low** sẽ tự động giảm độ mờ của bóng đổ để làm cho các artifact do số lượng sample thấp ít dễ nhận thấy hơn. Ngược lại, các thiết lập **Soft High** và **Soft Ultra** sẽ tự động tăng độ mờ của bóng đổ để tận dụng tốt hơn số lượng sample tăng lên.

.. image:: img/lights_and_shadows_filter_quality.webp

16-bit so với 32-bit
~~~~~~~~~~~~~~~~~~~~

Theo mặc định, Godot sử dụng depth texture 16-bit để kết xuất shadow map. Đây là lựa chọn được khuyến nghị trong hầu hết trường hợp vì cho hiệu năng tốt hơn mà không tạo ra khác biệt đáng kể về chất lượng.

Nếu **16 Bits** bị tắt, depth texture 32-bit sẽ được sử dụng thay thế. Điều này có thể làm giảm hiện tượng artifact trong các cảnh lớn và với các nguồn sáng lớn đã bật bóng. Tuy nhiên, khác biệt thường rất khó nhận thấy, trong khi chi phí hiệu năng có thể tăng đáng kể.

Độ mờ theo khoảng cách của ánh sáng/bóng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OmniLight3D, SpotLight3D và AreaLight3D cung cấp một số thuộc tính để ẩn các nguồn sáng ở xa. Điều này có thể cải thiện đáng kể hiệu năng trong các cảnh lớn có hàng chục nguồn sáng trở lên.

- **Enabled:** Kiểm soát việc bật distance fade (một dạng :abbr:`LOD (Level of Detail)`). Nguồn sáng sẽ mờ dần trong khoảng **Begin + Length**, sau đó bị loại bỏ và hoàn toàn không được gửi đến shader. Sử dụng tùy chọn này để giảm số lượng nguồn sáng đang hoạt động trong cảnh, từ đó cải thiện hiệu năng.
- **Begin:** Khoảng cách tính từ camera tại đó nguồn sáng bắt đầu mờ dần (theo đơn vị 3D).
- **Shadow:** Khoảng cách tính từ camera tại đó bóng bắt đầu mờ dần (theo đơn vị 3D). Có thể sử dụng tùy chọn này để làm bóng mờ sớm hơn nguồn sáng, giúp cải thiện hiệu năng hơn nữa. Chỉ khả dụng khi nguồn sáng đã bật bóng.
- **Length:** Khoảng cách mà trong đó nguồn sáng và bóng mờ dần (theo đơn vị 3D). Nguồn sáng sẽ dần trở nên trong suốt hơn trong khoảng cách này và hoàn toàn biến mất ở cuối khoảng. Giá trị cao hơn tạo ra quá trình chuyển tiếp mờ dần mượt hơn, phù hợp hơn khi camera di chuyển nhanh.

.. _doc_lights_and_shadows_pcss_recommendations:

Khuyến nghị về PCSS
~~~~~~~~~~~~~~~~~~~

Percentage-closer soft shadows (PCSS) tạo ra hình ảnh shadow mapping chân thực hơn, với kích thước vùng nửa tối thay đổi tùy theo khoảng cách giữa vật thể đổ bóng và bề mặt nhận bóng. Tuy nhiên, tính năng này có chi phí hiệu năng cao, đặc biệt đối với các nguồn sáng định hướng.

Để tránh các vấn đề về hiệu năng, bạn nên:

- Chỉ bật bóng PCSS cho một số ít nguồn sáng tại một thời điểm. Hiệu ứng này thường dễ nhận thấy nhất ở các nguồn sáng lớn và sáng. Các nguồn sáng phụ mờ hơn thường không hưởng lợi nhiều từ việc sử dụng bóng PCSS.
- Cung cấp một tùy chọn để người dùng tắt bóng PCSS. Đối với nguồn sáng định hướng, có thể thực hiện việc này bằng cách đặt thuộc tính ``light_angular_distance`` của DirectionalLight3D thành ``0.0`` trong script. Đối với nguồn sáng theo vị trí, có thể thực hiện việc này bằng cách đặt thuộc tính ``light_size`` của OmniLight3D hoặc SpotLight3D thành ``0.0`` trong script.

Chế độ lọc projector
~~~~~~~~~~~~~~~~~~~~

Cách projector được kết xuất cũng ảnh hưởng đến hiệu năng. Cài đặt dự án nâng cao **Rendering > Textures > Light Projectors > Filter** cho phép bạn kiểm soát cách lọc texture của projector. **Nearest/Linear** không sử dụng mipmap, nên kết xuất nhanh hơn. Tuy nhiên, projector sẽ có vẻ nhiễu ở khoảng cách xa. **Nearest/Linear Mipmaps** trông mượt hơn ở khoảng cách xa, nhưng projector sẽ bị mờ khi nhìn từ các góc xiên. Có thể khắc phục điều này bằng cách sử dụng **Nearest/Linear Mipmaps Anisotropic**, đây là chế độ có chất lượng cao nhất nhưng cũng tốn kém nhất.

Nếu dự án của bạn có phong cách pixel art, hãy cân nhắc đặt bộ lọc thành một trong các giá trị **Nearest** để projector sử dụng bộ lọc nearest-neighbor. Nếu không, hãy sử dụng **Linear**.
