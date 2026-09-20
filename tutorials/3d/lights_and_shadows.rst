.. _doc_lights_and_shadows:

Đèn và bóng đổ 3D
=================

Giới thiệu
----------

Các nguồn sáng phát ra ánh sáng, ánh sáng này hòa trộn với vật liệu và tạo ra kết quả hiển thị. Ánh sáng có thể đến từ một số loại nguồn trong một cảnh:

- Từ chính vật liệu, dưới dạng màu phát xạ (tuy nhiên, nó không ảnh hưởng đến các đối tượng lân cận trừ khi tính năng chiếu sáng gián tiếp được bake hoặc trong screen-space được bật). - Các light node: DirectionalLight3D, OmniLight3D, SpotLight3D và AreaLight3D. - Ánh sáng môi trường trong :ref:`Environment <class_Environment>` hoặc
  :ref:`doc_reflection_probes`.
- Global illumination (:ref:`LightmapGI <doc_using_lightmap_gi>`,
  :ref:`VoxelGI <doc_using_voxel_gi>` or :ref:`SDFGI <doc_using_sdfgi>`).

Màu phát xạ là một thuộc tính của vật liệu. Bạn có thể đọc thêm về thuộc tính này trong tutorial :ref:`doc_standard_material_3d`.

.. seealso::

    Bạn có thể so sánh trực tiếp các loại đèn khác nhau bằng cách sử dụng `dự án demo Đèn và Bóng đổ 3D <https://github.com/godotengine/godot-demo-projects/tree/master/3d/lights_and_shadows>`__.

Light node
----------

Có bốn loại light node: :ref:`class_DirectionalLight3D`,
:ref:`class_OmniLight3D`, :ref:`class_SpotLight3D`, and :ref:`class_AreaLight3D`. Let's take a look at the common
các tham số của đèn:

.. image:: img/light_params.png

Mỗi thuộc tính có một chức năng cụ thể:

- **Color:** Màu cơ bản của ánh sáng phát ra. - **Energy:** Hệ số nhân năng lượng. Thuộc tính này hữu ích để làm bão hòa ánh sáng hoặc làm việc với :ref:`doc_high_dynamic_range`. - **Indirect Energy:** Hệ số nhân phụ được sử dụng với ánh sáng gián tiếp (ánh sáng phản xạ). Thuộc tính này hoạt động với :ref:`doc_using_lightmap_gi`, VoxelGI hoặc SDFGI. - **Volumetric Fog Energy:** Hệ số nhân phụ được sử dụng với sương mù thể tích. Thuộc tính này chỉ có tác dụng khi sương mù thể tích được bật. - **Negative:** Ánh sáng trở thành dạng trừ thay vì cộng. Đôi khi thuộc tính này hữu ích để bù thủ công cho một số góc tối. - **Specular:** Ảnh hưởng đến cường độ của vùng sáng specular trên các đối tượng chịu ảnh hưởng của đèn này. Khi bằng 0, đèn này trở thành đèn diffuse thuần túy. - **Bake Mode:** Thiết lập chế độ bake cho đèn. Xem :ref:`doc_using_lightmap_gi`. - **Cull Mask:** Các đối tượng nằm trong những layer được chọn bên dưới sẽ chịu ảnh hưởng của đèn này. Lưu ý rằng các đối tượng bị vô hiệu hóa qua cull mask này vẫn đổ bóng. Nếu không muốn các đối tượng bị vô hiệu hóa đổ bóng, hãy điều chỉnh thuộc tính **Cast Shadow** trên GeometryInstance3D thành giá trị mong muốn.

.. seealso::

    Xem :ref:`doc_physical_light_and_camera_units` nếu bạn muốn sử dụng các đơn vị trong thế giới thực để cấu hình cường độ và nhiệt độ màu của đèn.

Giới hạn số lượng đèn
---------------------

Khi sử dụng renderer Forward+, Godot dùng phương pháp *clustering* cho việc chiếu sáng theo thời gian thực. Bạn có thể thêm bao nhiêu đèn tùy ý (miễn là hiệu năng cho phép). Tuy nhiên, vẫn có giới hạn mặc định là 512 *clustered element* có thể hiện diện trong góc nhìn hiện tại của camera. Một clustered element có thể là omni light, spot light, area light, :ref:`decal <doc_using_decals>` hoặc một
:ref:`reflection probe <doc_reflection_probes>`. This limit can be increased by adjusting
:ref:`Max Clustered Elements<class_ProjectSettings_property_rendering/limits/cluster_builder/max_clustered_elements>`
trong **Project Settings > Rendering > Limits > Cluster Builder**.

Khi sử dụng renderer Mobile, có giới hạn 8 OmniLights + 8 SpotLights cho mỗi mesh resource. Ngoài ra còn có giới hạn 256 OmniLights + 256 SpotLights có thể được render trong góc nhìn hiện tại của camera. Hiện tại không thể thay đổi các giới hạn này.

Khi sử dụng renderer Compatibility, tối đa 8 OmniLights + 8 SpotLights có thể được render cho mỗi mesh resource. Có thể tăng giới hạn này trong Project Settings nâng cao bằng cách điều chỉnh
:ref:`Max Renderable Elements<class_ProjectSettings_property_rendering/limits/opengl/max_renderable_elements>`
và/hoặc :ref:`Max Lights per Object<class_ProjectSettings_property_rendering/limits/opengl/max_lights_per_object>` trong **Rendering > Limits > OpenGL**, nhưng phải đánh đổi bằng hiệu năng và thời gian biên dịch shader lâu hơn. Bạn cũng có thể giảm giới hạn để rút ngắn thời gian biên dịch shader và cải thiện đôi chút hiệu năng.

Với tất cả các phương thức rendering, tối đa 8 DirectionalLights có thể hiển thị cùng lúc. Tuy nhiên, mỗi DirectionalLight bổ sung có bật bóng đổ sẽ làm giảm độ phân giải bóng đổ hiệu dụng của từng DirectionalLight. Điều này là do directional shadow atlas được dùng chung giữa tất cả các đèn.

Nếu vượt quá giới hạn rendering, các đèn sẽ bắt đầu liên tục xuất hiện rồi biến mất trong khi camera di chuyển, gây mất tập trung. Bật **Distance Fade** trên các light node có thể giúp giảm vấn đề này đồng thời cải thiện hiệu năng. Chia mesh thành các phần nhỏ hơn cũng có thể hữu ích, đặc biệt đối với hình học của level (điều này cũng cải thiện hiệu quả culling).

Nếu cần render nhiều đèn hơn khả năng của một renderer nhất định, hãy cân nhắc sử dụng :ref:`baked lightmaps <doc_using_lightmap_gi>` với bake mode của đèn được đặt thành **Static**. Điều này cho phép bake hoàn toàn các đèn, đồng thời giúp render chúng nhanh hơn nhiều. Bạn cũng có thể sử dụng vật liệu phát sáng với bất kỳ
:ref:`global illumination <doc_introduction_to_global_illumination>` technique
nào để thay thế cho các light node phát sáng trên một khu vực lớn.

Shadow mapping
--------------

Đèn có thể tùy chọn đổ bóng. Điều này giúp chúng chân thực hơn (ánh sáng không chiếu tới các khu vực bị che khuất), nhưng có thể làm tăng chi phí hiệu năng. Có một danh sách các tham số bóng đổ chung, mỗi tham số cũng có một chức năng cụ thể:

- **Enabled:** Chọn để bật shadow mapping cho đèn này. - **Opacity:** Các khu vực bị che khuất sẽ tối đi theo hệ số opacity này. Theo mặc định, bóng đổ hoàn toàn không trong suốt, nhưng có thể thay đổi để làm bóng đổ trong mờ đối với một đèn cụ thể. - **Bias:** Khi tham số này quá thấp, hiện tượng tự đổ bóng sẽ xảy ra. Khi quá cao, bóng đổ sẽ tách khỏi đối tượng đổ bóng. Hãy điều chỉnh đến giá trị phù hợp nhất với bạn. - **Normal Bias:** Khi tham số này quá thấp, hiện tượng tự đổ bóng sẽ xảy ra. Khi quá cao, bóng đổ có vẻ bị lệch khỏi đối tượng đổ bóng. Hãy điều chỉnh đến giá trị phù hợp nhất với bạn. - **Transmittance Bias:** Khi tham số này quá thấp, hiện tượng tự đổ bóng sẽ xảy ra trên các vật liệu đã bật transmittance. Khi quá cao, bóng đổ sẽ không tác động nhất quán lên các vật liệu đã bật transmittance. Hãy điều chỉnh đến giá trị phù hợp nhất với bạn. - **Reverse Cull Face:** Một số cảnh hoạt động tốt hơn khi shadow mapping được render với việc culling mặt bị đảo ngược. - **Blur:** Nhân bán kính làm mờ bóng đổ của đèn này. Thuộc tính này hoạt động với cả shadow mapping truyền thống và contact-hardening shadow (các đèn có **Angular Distance** hoặc **Size** lớn hơn ``0.0``). Giá trị cao hơn tạo ra bóng đổ mềm hơn, đồng thời có vẻ ổn định hơn theo thời gian đối với các đối tượng chuyển động. Nhược điểm của việc tăng độ mờ bóng đổ là làm cho mẫu nhiễu dùng để lọc trở nên dễ nhận thấy hơn. Xem thêm :ref:`doc_lights_and_shadows_shadow_filter_mode`. - **Caster Mask:** Chỉ các đối tượng trong những layer này mới đổ bóng. Lưu ý rằng mask này không ảnh hưởng đến việc bóng đổ được chiếu *lên* những đối tượng nào.

.. image:: img/lights_and_shadows_blur.webp

Điều chỉnh bias của bóng đổ
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dưới đây là hình ảnh minh họa việc điều chỉnh bias. Các giá trị mặc định phù hợp với hầu hết trường hợp, nhưng nhìn chung còn phụ thuộc vào kích thước và độ phức tạp của hình học.

Nếu **Shadow Bias** hoặc **Shadow Normal Bias** được đặt quá thấp đối với một đèn nhất định, bóng đổ sẽ bị "lem" lên các đối tượng. Điều này khiến vẻ ngoài vốn có của ánh sáng bị tối đi và được gọi là *shadow acne*:

.. image:: img/lights_and_shadows_acne.webp

Ngược lại, nếu **Shadow Bias** hoặc **Shadow Normal Bias** được đặt quá cao đối với một đèn nhất định, bóng đổ có thể trông như bị tách khỏi đối tượng. Hiện tượng này được gọi là *peter-panning*:

.. image:: img/lights_and_shadows_peter_panning.webp

Nhìn chung, nên tăng **Shadow Normal Bias** thay vì tăng **Shadow Bias**. Tăng **Shadow Normal Bias** không gây ra hiện tượng peter-panning nhiều như tăng **Shadow Bias**, nhưng vẫn có thể xử lý hiệu quả hầu hết vấn đề shadow acne. Nhược điểm của việc tăng **Shadow Normal Bias** là có thể khiến bóng đổ trông mỏng hơn trên một số đối tượng.

Mọi vấn đề liên quan đến bias đều có thể được khắc phục bằng cách
:ref:`increasing the shadow map resolution <doc_lights_and_shadows_balancing_performance_and_quality>`,
nhưng phải đánh đổi bằng hiệu năng giảm.

.. note::

    Việc điều chỉnh các thiết lập shadow mapping là một nghệ thuật – không có thiết lập "phù hợp cho mọi trường hợp". Để đạt được hình ảnh tốt nhất, bạn có thể cần sử dụng các giá trị shadow bias khác nhau cho từng đèn.

**Lưu ý về thay đổi giao diện**: Khi bật bóng đổ trên một đèn, hãy lưu ý rằng giao diện của đèn có thể thay đổi so với khi được render không có bóng đổ trong renderer Compatibility. Do những hạn chế của các thiết bị di động cũ, bóng đổ được triển khai bằng phương pháp rendering nhiều pass, vì vậy các đèn có bóng đổ được render trong không gian sRGB thay vì không gian tuyến tính. Thay đổi không gian rendering này đôi khi có thể làm thay đổi đáng kể giao diện của đèn. Để đạt được giao diện tương tự như đèn không có bóng đổ, bạn có thể cần điều chỉnh thiết lập energy của đèn.

.. _doc_lights_and_shadows_directional_light:

Directional light
-----------------

Đây là loại đèn phổ biến nhất và đại diện cho một nguồn sáng ở rất xa (chẳng hạn như mặt trời). Đây cũng là loại đèn có chi phí tính toán thấp nhất và nên được sử dụng bất cứ khi nào có thể (mặc dù shadow-map của nó không phải loại có chi phí tính toán thấp nhất, nhưng sẽ nói thêm về điều đó sau).

Directional light mô phỏng vô số tia sáng song song bao phủ toàn bộ cảnh. Directional light node được biểu diễn bằng một mũi tên lớn cho biết hướng của các tia sáng. Tuy nhiên, vị trí của node hoàn toàn không ảnh hưởng đến việc chiếu sáng và có thể nằm ở bất kỳ đâu.

.. image:: img/light_directional.png

Mọi mặt có mặt trước bị các tia sáng chiếu vào đều được chiếu sáng, trong khi các mặt còn lại vẫn tối. Không giống hầu hết các loại đèn khác, directional light không có các tham số riêng.

Directional light cũng cung cấp thuộc tính **Angular Distance**, xác định kích thước góc của đèn theo độ. Tăng giá trị này cao hơn ``0.0`` sẽ làm bóng đổ mềm hơn khi khoảng cách từ đối tượng đổ bóng tăng, đồng thời ảnh hưởng đến diện mạo của mặt trời trong các vật liệu bầu trời procedural. Đây được gọi là bóng đổ *contact-hardening* (còn gọi là PCSS).

Để tham khảo, khoảng cách góc của Mặt Trời khi nhìn từ Trái Đất xấp xỉ ``0.5``. Loại bóng đổ này tốn nhiều tài nguyên, vì vậy hãy xem các khuyến nghị trong :ref:`doc_lights_and_shadows_pcss_recommendations` nếu đặt giá trị này cao hơn ``0.0`` trên các đèn đã bật bóng đổ.

Directional shadow mapping
~~~~~~~~~~~~~~~~~~~~~~~~~~

Để tính shadow map, cảnh được render (chỉ độ sâu) từ một góc nhìn trực giao bao quát toàn bộ cảnh (hoặc tối đa đến khoảng cách lớn nhất). Tuy nhiên, cách tiếp cận này có một vấn đề: các đối tượng ở gần camera hơn sẽ nhận shadow có độ phân giải thấp, khiến chúng có thể trông bị vỡ hình.

Để khắc phục điều này, một kỹ thuật có tên *Parallel Split Shadow Maps* (PSSM) được sử dụng. Kỹ thuật này chia view frustum thành 2 hoặc 4 vùng. Mỗi vùng có shadow map riêng. Nhờ đó, các vùng nhỏ ở gần người xem có thể có cùng độ phân giải shadow như một vùng rất lớn ở xa. Khi shadow được bật cho DirectionalLight3D, chế độ shadow mặc định là PSSM với 4 vùng chia. Trong các trường hợp một đối tượng đủ lớn để xuất hiện trong cả bốn vùng chia, số lần draw call sẽ tăng. Cụ thể, đối tượng đó sẽ được render tổng cộng năm lần: một lần cho mỗi trong bốn vùng shadow và một lần cho lần render cảnh cuối cùng. Điều này có thể ảnh hưởng đến hiệu năng; việc hiểu hành vi này rất quan trọng để tối ưu hóa cảnh và quản lý kỳ vọng về hiệu năng.

.. image:: img/lights_and_shadows_pssm_explained.webp

Nhờ vậy, shadow trở nên chi tiết hơn:

.. image:: img/lights_and_shadows_directional_mode.webp

Để điều khiển PSSM, một số tham số được cung cấp:

.. image:: img/lights_and_shadows_directional_shadow_params.webp

Khoảng cách của mỗi vùng chia được điều khiển tương đối so với camera far (hoặc **Max Distance** của shadow nếu lớn hơn ``0.0``). ``0.0`` là vị trí mắt và ``1.0`` là nơi shadow kết thúc tại một khoảng cách nhất định. Các vùng chia nằm ở giữa. Các giá trị mặc định nhìn chung hoạt động tốt, nhưng việc tinh chỉnh vùng chia đầu tiên đôi chút là cách thường dùng để cung cấp nhiều chi tiết hơn cho các đối tượng ở gần (chẳng hạn như nhân vật trong game góc nhìn người thứ ba).

Luôn nhớ đặt **Max Distance** của shadow phù hợp với nhu cầu của cảnh. Khoảng cách tối đa thấp hơn sẽ tạo ra shadow đẹp hơn và hiệu năng tốt hơn, vì sẽ có ít đối tượng cần được đưa vào quá trình render shadow hơn. Bạn cũng có thể điều chỉnh **Fade Start** để kiểm soát mức độ shadow mờ dần theo khoảng cách. Đối với các cảnh mà **Max Distance** bao phủ hoàn toàn cảnh tại mọi vị trí của camera, bạn có thể tăng **Fade Start** lên ``1.0`` để ngăn shadow mờ dần theo khoảng cách. Không nên làm vậy trong các cảnh mà **Max Distance** không bao phủ hoàn toàn cảnh, vì shadow sẽ có vẻ bị cắt đột ngột ở một khoảng cách nào đó.

Đôi khi, sự chuyển tiếp giữa một vùng chia và vùng tiếp theo có thể trông không đẹp. Để khắc phục điều này, có thể bật tùy chọn **Blend Splits**, đánh đổi chi tiết và hiệu năng để có sự chuyển tiếp mượt mà hơn:

.. image:: img/blend_splits.png

Có thể sử dụng tham số **Shadow > Normal Bias** để khắc phục các trường hợp đặc biệt về self-shadowing khi các đối tượng vuông góc với nguồn sáng. Nhược điểm duy nhất là shadow sẽ mỏng hơn một chút. Trong hầu hết trường hợp, hãy cân nhắc tăng **Shadow > Normal Bias** trước khi tăng **Shadow > Bias**.

Cuối cùng, **Pancake Size** là một thuộc tính có thể được điều chỉnh để khắc phục shadow bị thiếu khi sử dụng các đối tượng lớn với mesh chưa được chia nhỏ. Chỉ thay đổi giá trị này nếu bạn nhận thấy shadow bị thiếu mà nguyên nhân không liên quan đến các vấn đề về shadow bias.

.. _doc_lights_and_shadows_omni_light:

Đèn Omni
--------

Đèn Omni là một nguồn sáng dạng điểm, phát ánh sáng hình cầu theo mọi hướng trong phạm vi bán kính cho trước.

.. image:: img/light_omni.png

Trong thực tế, độ suy giảm ánh sáng là một hàm nghịch đảo, nghĩa là đèn Omni không có bán kính. Đây là một vấn đề vì việc tính toán nhiều đèn Omni sẽ trở nên tốn tài nguyên.

Để giải quyết vấn đề này, tham số **Range** được giới thiệu cùng với một hàm suy giảm.

.. image:: img/light_omni_params.png

Hai tham số này cho phép tinh chỉnh cách hiệu ứng hoạt động về mặt hình ảnh để đạt được kết quả thẩm mỹ mong muốn.

.. image:: img/light_attenuation.png

Một tham số **Size** cũng có trong OmniLight3D. Việc tăng giá trị này sẽ khiến ánh sáng mờ dần chậm hơn và shadow trở nên mờ hơn khi ở xa vật thể đổ shadow. Có thể sử dụng tham số này để phần nào mô phỏng đèn vùng. Loại shadow này được gọi là shadow *contact-hardening* (còn được gọi là PCSS). Loại shadow này tốn nhiều tài nguyên, vì vậy hãy xem các khuyến nghị trong
:ref:`doc_lights_and_shadows_pcss_recommendations` if setting this value above
``0.0`` trên các đèn đã bật shadow.

.. image:: img/lights_and_shadows_pcss.webp

Ánh xạ shadow của đèn Omni
~~~~~~~~~~~~~~~~~~~~~~~~~~

Ánh xạ shadow của đèn Omni tương đối đơn giản. Vấn đề chính cần cân nhắc là thuật toán được sử dụng để render nó.

Omni Shadow có thể được render dưới dạng ánh xạ **Dual Paraboloid** hoặc **Cube**. **Dual Paraboloid** render nhanh, nhưng có thể gây biến dạng, trong khi **Cube** chính xác hơn nhưng chậm hơn. Mặc định là **Cube**, nhưng hãy cân nhắc chuyển sang **Dual Paraboloid** đối với những đèn mà việc thay đổi này không tạo ra khác biệt đáng kể về hình ảnh.

.. image:: img/lights_and_shadows_dual_parabolid_vs_cubemap.webp

Nếu các đối tượng được render chủ yếu có hình dạng bất quy tắc và đã được chia nhỏ, Dual Paraboloid thường là đủ. Trong mọi trường hợp, vì các shadow này được lưu vào shadow atlas (sẽ nói thêm ở cuối), hiệu năng có thể không thay đổi đối với hầu hết các cảnh.

Các đèn Omni đã bật shadow có thể sử dụng projector. Texture của projector sẽ *nhân* màu của đèn với màu tại một điểm nhất định trên texture. Do đó, đèn thường sẽ trông tối hơn sau khi được gán texture projector; bạn có thể tăng **Energy** để bù lại.

Texture projector của đèn Omni yêu cầu một kiểu ánh xạ panorama 360° đặc biệt, tương tự như texture :ref:`class_PanoramaSkyMaterial`.

Với texture projector bên dưới, kết quả thu được như sau:

.. image:: img/lights_and_shadows_omni_projector_example.webp

.. image:: img/lights_and_shadows_omni_projector.webp

.. tip::

    Nếu bạn đã có projector Omni dưới dạng ảnh cubemap, bạn có thể sử dụng `công cụ chuyển đổi trên web này <https://danilw.github.io/GLSL-howto/cubemap_to_panorama_js/cubemap_to_panorama.html>`__ để chuyển đổi chúng thành một ảnh panorama duy nhất.

.. _doc_lights_and_shadows_spot_light:

Đèn Spot
--------

Đèn Spot tương tự đèn Omni, ngoại trừ việc chúng chỉ phát ánh sáng vào một hình nón (hay "cutoff"). Chúng hữu ích để mô phỏng đèn pin, đèn xe, đèn phản chiếu, đèn sân khấu, v.v. Loại đèn này cũng bị suy giảm theo hướng ngược lại với hướng mà nó chiếu tới.

Đèn Spot dùng chung **Range**, **Attenuation** và **Size** với OmniLight3D, đồng thời bổ sung thêm hai tham số:

- **Angle:** Góc khẩu độ của đèn. - **Angle Attenuation:** Độ suy giảm của hình nón, giúp làm mềm các đường biên của hình nón.

Ánh xạ shadow của đèn Spot
~~~~~~~~~~~~~~~~~~~~~~~~~~

Đèn Spot có cùng các tham số ánh xạ shadow như đèn Omni. Việc render shadow map của đèn Spot nhanh hơn đáng kể so với đèn Omni, vì chỉ cần render một texture shadow (thay vì render 6 mặt, hoặc 2 mặt trong chế độ dual paraboloid).

Các đèn Spot đã bật shadow có thể sử dụng projector. Texture của projector sẽ *nhân* màu của đèn với màu tại một điểm nhất định trên texture. Do đó, đèn thường sẽ trông tối hơn sau khi được gán texture projector; bạn có thể tăng **Energy** để bù lại.

Không giống projector của đèn Omni, texture projector của đèn Spot không cần tuân theo định dạng đặc biệt để hiển thị chính xác. Nó sẽ được ánh xạ theo cách tương tự như một
:ref:`decal <doc_using_decals>`.

Với texture projector bên dưới, kết quả thu được như sau:

.. image:: img/lights_and_shadows_spot_projector_example.webp

.. image:: img/lights_and_shadows_spot_projector.webp

.. note::

    Đèn Spot có góc rộng sẽ có shadow chất lượng thấp hơn đèn Spot có góc hẹp, vì shadow map được trải trên một bề mặt lớn hơn. Ở các góc rộng hơn 89 độ, shadow của đèn Spot sẽ hoàn toàn ngừng hoạt động. Nếu cần shadow cho các đèn có góc rộng hơn, hãy sử dụng đèn Omni thay thế.

.. _doc_lights_and_shadows_area_light:

Đèn vùng
--------

Đôi khi, bạn muốn ánh sáng phát ra từ một vùng lớn thay vì một điểm duy nhất. Đèn vùng hữu ích để mô phỏng ánh sáng mềm, khuếch tán, chẳng hạn như ánh sáng phát ra từ cửa sổ hoặc bảng quảng cáo được chiếu sáng.

Godot cung cấp node :ref:`class_AreaLight3D` cho mục đích này; node này phát ánh sáng từ một vùng hình chữ nhật. Node này chỉ phát ánh sáng và không có biểu diễn trực quan nào khác trong cảnh. Các ảnh chụp màn hình bên dưới sử dụng node :ref:`class_Sprite3D` làm node con của đèn vùng để phục vụ mục đích trực quan hóa.

.. warning::

    Đây là loại đèn tốn nhiều tài nguyên nhất khi render theo thời gian thực. Nên sử dụng hạn chế, đặc biệt khi đã bật shadow. Hãy cân nhắc chỉ sử dụng chúng cho các đoạn phim hoặc khi nhắm đến các thiết bị cao cấp.

    Trong Forward+, ngay khi một đèn vùng hiển thị trong view frustum, nó sẽ gây thêm chi phí hiệu năng cho **tất cả** đối tượng được render trong cảnh, kể cả những đối tượng không được đèn vùng chiếu tới. Sự đánh đổi này cho phép render số lượng đèn vùng lớn hơn (clustered lighting).

    Trong Mobile và Compatibility, chỉ các đối tượng được đèn vùng chiếu tới mới phải chịu thêm chi phí hiệu năng.

Đèn vùng cũng có thể đổ shadow, với penumbra thay đổi được mô phỏng bằng
:ref:`PCSS <doc_lights_and_shadows_pcss_recommendations>` by default. The size
Có thể điều khiển mức độ của penumbra này bằng thuộc tính **Size** của Light3D. Hiệu ứng này có thể khá tốn tài nguyên, vì vậy có thể tắt bằng cách đặt **Size** thành ``0.0``.

.. note::

    Shadow do đèn vùng tạo ra có thể trông không chính xác nếu đối tượng đổ shadow không có đủ subdivisions và ở quá gần đèn vùng. Đây cũng là giới hạn của chế độ shadow Dual Paraboloid trên đèn Omni.

.. image:: img/lights_and_shadows_area_example.webp

.. note::

    Vì đèn vùng khó mô phỏng trong một renderer rasterized theo thời gian thực, chúng đi kèm với một số giới hạn.

    Đối với các nguồn sáng nhỏ, bạn có thể sẽ đạt kết quả tốt hơn khi sử dụng đèn điểm. Shadow từ đèn vùng chỉ là các phép xấp xỉ thô, vì chúng được tính như thể là đèn điểm và có thể trông bị biến dạng ở các cạnh. Để có kết quả tốt hơn, hãy đảm bảo các mesh trong phạm vi của đèn được chia nhỏ đầy đủ.

    Đèn vùng dễ gây ra hiện tượng ánh sáng lọt ở mặt sau của hình học nằm ngay phía trước chúng tại các góc chiếu sượt, vì vậy hãy cẩn thận khi bố trí chúng.

    Cuối cùng, không phải tất cả các đặc tính của vật liệu đều được hỗ trợ đầy đủ; area light thực tế chỉ bị giới hạn ở shading diffuse Lambertian và specular GGX, trong khi vật liệu anisotropic sẽ hiển thị như thể là isotropic. Vertex shading cũng chưa được triển khai cho area light.

Area light phát sáng trong một vùng hình chữ nhật được xác định bởi thuộc tính **Area > Size** (không nên nhầm với thuộc tính **Size** chung của Light3D). Để có kết quả chính xác về mặt vật lý, bạn nên thay đổi kích thước vùng này để khớp với kích thước của nguồn sáng thực tế mà bạn đang mô phỏng. Ví dụ: nếu bạn đang mô phỏng một ống neon dài 1 mét và rộng 10 centimet, hãy đặt kích thước vùng thành ``(1, 0.1)`` và điều chỉnh energy tương ứng.

Theo mặc định, energy của light được normalize: vùng càng lớn thì light càng yếu. Điều này cho phép bạn thay đổi kích thước vùng mà không cần điều chỉnh energy để bù lại, rất hữu ích cho animation. Bạn có thể tắt hành vi này bằng cách bỏ chọn **Area > Normalize Energy** nếu muốn energy độc lập với kích thước vùng.

Vùng hình chữ nhật có thể tùy chọn sử dụng texture. Điều này có thể được dùng hiệu quả để thay đổi hình dạng của light thành bất kỳ hình dạng 2D nào hoặc nhuộm nó bằng các màu khác nhau. Kênh alpha của texture được xử lý như màu đen (không có ánh sáng đi qua). Texture của area light sẽ hiển thị trong reflection tùy theo roughness của bề mặt. Hành vi này khác với projector omni/spot, vì nó không chiếu texture trực tiếp lên toàn bộ diffuse lighting.

Khi sử dụng texture trong suốt hoặc có màu đen ở các cạnh, bạn có thể muốn chừa một khoảng trống vài pixel để đảm bảo texture được làm mờ mượt mà.

.. image:: img/lights_and_shadows_area_texture.webp

.. note::

    Việc thay đổi texture của area light tại runtime có thể tốn nhiều tài nguyên, đặc biệt nếu texture lớn.

    Để giảm tác động đến hiệu năng khi chuyển texture tại runtime, hãy đảm bảo mỗi chiều của texture area hoặc là bội số của 128 pixel, hoặc là lũy thừa của hai. Điều này loại bỏ nhu cầu thực hiện scaling pass, vốn làm chậm quá trình thay đổi texture. Texture không nhất thiết phải là hình vuông để đạt hiệu năng tối ưu. Các ví dụ về kích thước texture tối ưu gồm 32×64, 128×128 và 256×384.

    Texture area light không được hỗ trợ trong Compatibility renderer.

.. _doc_lights_and_shadows_shadow_atlas:

Shadow atlas
------------

Không giống Directional light, vốn có texture shadow riêng, omni, spot và area light được gán vào các slot của shadow atlas. Atlas này có thể được cấu hình trong Project Settings nâng cao (**Rendering > Lights And Shadows > Positional Shadow**).

Độ phân giải áp dụng cho toàn bộ shadow atlas. Atlas này được chia thành bốn quadrant:

.. image:: img/lights_and_shadows_shadow_quadrants.webp

Mỗi quadrant có thể được chia nhỏ để phân bổ số lượng shadow map bất kỳ; cách chia mặc định như sau:

.. image:: img/lights_and_shadows_shadow_quadrants2.webp

Shadow atlas phân bổ không gian như sau:

- Kích thước shadow map lớn nhất (khi không sử dụng subdivision) đại diện cho một light có kích thước bằng màn hình (hoặc lớn hơn). - Subdivision (các map nhỏ hơn) đại diện cho shadow của những light ở xa góc nhìn hơn và nhỏ hơn theo tỷ lệ.

Mỗi frame, quy trình sau được thực hiện cho tất cả light:

1. Kiểm tra xem light có nằm trong slot đúng kích thước hay không. Nếu không, render lại light và chuyển nó sang slot lớn hơn/nhỏ hơn. 2. Kiểm tra xem có object nào ảnh hưởng đến shadow map đã thay đổi hay không. Nếu có, render lại light. 3. Nếu không có điều nào ở trên xảy ra, không làm gì cả và giữ nguyên shadow.

Nếu các slot trong một quadrant đã đầy, light sẽ được đẩy về các slot nhỏ hơn, tùy thuộc vào kích thước và khoảng cách. Nếu tất cả slot trong mọi quadrant đều đầy, một số light sẽ không thể render shadow ngay cả khi chúng đã bật shadow.

Chiến lược phân bổ shadow mặc định cho phép render tối đa 88 light với shadow được bật trong camera frustum (4 + 4 + 16 + 64):

1. Quadrant đầu tiên và chi tiết nhất có thể lưu trữ 4 shadow. 2. Quadrant thứ hai có thể lưu trữ 4 shadow khác. 3. Quadrant thứ ba có thể lưu trữ 16 shadow, với ít chi tiết hơn. 4. Quadrant thứ tư và ít chi tiết nhất có thể lưu trữ 64 shadow, với thậm chí ít chi tiết hơn.

Sử dụng số lượng shadow cao hơn cho mỗi quadrant cho phép hỗ trợ tổng số light lớn hơn với shadow được bật, đồng thời cải thiện hiệu năng (vì shadow sẽ được render ở độ phân giải thấp hơn cho mỗi light). Tuy nhiên, việc tăng số lượng shadow cho mỗi quadrant phải đánh đổi bằng chất lượng shadow thấp hơn.

Trong một số trường hợp, bạn có thể muốn sử dụng một chiến lược phân bổ khác. Ví dụ: trong một game top-down, nơi tất cả light có kích thước gần như nhau, bạn có thể muốn đặt tất cả quadrant sử dụng cùng một subdivision để mọi light có shadow với mức chất lượng tương tự.

.. _doc_lights_and_shadows_balancing_performance_and_quality:

Cân bằng hiệu năng và chất lượng
--------------------------------

Việc render shadow là một chủ đề quan trọng đối với hiệu năng 3D rendering. Điều quan trọng là đưa ra lựa chọn phù hợp ở đây để tránh tạo ra các bottleneck.

Có thể thay đổi các thiết lập chất lượng directional shadow tại runtime bằng cách gọi các method :ref:`class_RenderingServer` tương ứng.

Có thể thay đổi các thiết lập chất lượng positional (omni/spot/area) shadow tại runtime trên root :ref:`class_Viewport`.

Kích thước shadow map
~~~~~~~~~~~~~~~~~~~~~

Độ phân giải shadow cao tạo ra shadow sắc nét hơn, nhưng phải trả giá đáng kể về hiệu năng. Cũng cần lưu ý rằng *shadow sắc nét hơn không phải lúc nào cũng chân thực hơn*. Trong hầu hết trường hợp, nên giữ giá trị mặc định là ``4096`` hoặc giảm xuống ``2048`` đối với GPU cấp thấp.

Nếu positional shadow trở nên quá mờ sau khi giảm kích thước shadow map, bạn có thể khắc phục bằng cách điều chỉnh
:ref:`shadow atlas <doc_lights_and_shadows_shadow_atlas>` quadrants to contain
ít shadow hơn. Điều này cho phép render mỗi shadow ở độ phân giải cao hơn.

.. _doc_lights_and_shadows_shadow_filter_mode:

Chế độ lọc shadow
~~~~~~~~~~~~~~~~~

Tại đây có thể chọn một số thiết lập chất lượng shadow map. Mặc định **Soft Low** là sự cân bằng tốt giữa hiệu năng và chất lượng cho các scene có texture chi tiết, vì độ chi tiết của texture sẽ giúp làm cho pattern dithering ít dễ nhận thấy hơn.

Tuy nhiên, trong các project có texture ít chi tiết hơn, pattern dithering của shadow có thể dễ nhận thấy hơn. Để ẩn pattern này, bạn có thể bật
:ref:`doc_3d_antialiasing_taa`, :ref:`doc_3d_antialiasing_fsr2`,
:ref:`doc_3d_antialiasing_fxaa`, or increase the shadow filter quality to
**Soft Medium** hoặc cao hơn.

Thiết lập **Soft Very Low** sẽ tự động giảm độ blur của shadow để khiến các artifact do số lượng sample thấp ít dễ nhận thấy hơn. Ngược lại, các thiết lập **Soft High** và **Soft Ultra** sẽ tự động tăng độ blur của shadow để tận dụng tốt hơn số lượng sample tăng thêm.

.. image:: img/lights_and_shadows_filter_quality.webp

16-bit so với 32-bit
~~~~~~~~~~~~~~~~~~~~

Theo mặc định, Godot sử dụng depth texture 16-bit để render shadow map. Đây là lựa chọn được khuyến nghị trong hầu hết trường hợp vì có hiệu năng tốt hơn mà không tạo ra khác biệt đáng kể về chất lượng.

Nếu **16 Bits** bị tắt, depth texture 32-bit sẽ được sử dụng thay thế. Điều này có thể làm giảm artifact trong các scene lớn và các light lớn đã bật shadow. Tuy nhiên, khác biệt thường gần như không thể nhận thấy, trong khi chi phí hiệu năng có thể đáng kể.

Fade khoảng cách light/shadow
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OmniLight3D, SpotLight3D và AreaLight3D cung cấp một số thuộc tính để ẩn các light ở xa. Điều này có thể cải thiện đáng kể hiệu năng trong các scene lớn có hàng chục light trở lên.

- **Enabled:** Kiểm soát việc distance fade (một dạng :abbr:`LOD (Level of Detail)`) có được bật hay không. Light sẽ fade out trong khoảng **Begin + Length**, sau đó sẽ bị culling và hoàn toàn không được gửi đến shader. Sử dụng tùy chọn này để giảm số lượng light đang hoạt động trong scene và nhờ đó cải thiện hiệu năng. - **Begin:** Khoảng cách từ camera tại đó light bắt đầu fade out (tính theo đơn vị 3D). - **Shadow:** Khoảng cách từ camera tại đó shadow bắt đầu fade out (tính theo đơn vị 3D). Có thể dùng tùy chọn này để fade out shadow sớm hơn light, từ đó cải thiện hiệu năng hơn nữa. Chỉ khả dụng nếu shadow được bật cho light. - **Length:** Khoảng cách mà light và shadow fade out (tính theo đơn vị 3D). Light sẽ dần trở nên trong suốt hơn trong khoảng cách này và hoàn toàn biến mất ở cuối khoảng cách. Giá trị cao hơn tạo ra quá trình fade-out mượt mà hơn, phù hợp hơn khi camera di chuyển nhanh.

.. _doc_lights_and_shadows_pcss_recommendations:

Khuyến nghị về PCSS
~~~~~~~~~~~~~~~~~~~

Percentage-closer soft shadow (PCSS) tạo ra diện mạo shadow mapping chân thực hơn, với kích thước penumbra thay đổi tùy theo khoảng cách giữa vật thể đổ shadow và bề mặt nhận shadow. Điều này có chi phí hiệu năng cao, đặc biệt đối với directional light.

Để tránh các vấn đề về hiệu năng, bạn nên:

- Chỉ sử dụng một số ít light có bật PCSS shadow tại một thời điểm. Hiệu ứng này thường dễ nhận thấy nhất trên các light lớn và sáng. Các nguồn sáng phụ mờ hơn thường không hưởng lợi nhiều từ việc sử dụng PCSS shadow. - Cung cấp một thiết lập cho phép người dùng tắt PCSS shadow. Đối với directional light, có thể thực hiện việc này bằng cách đặt thuộc tính ``light_angular_distance`` của DirectionalLight3D thành ``0.0`` trong một script. Đối với positional light, có thể thực hiện việc này bằng cách đặt thuộc tính ``light_size`` của OmniLight3D hoặc SpotLight3D thành ``0.0`` trong một script.

Chế độ lọc projector
~~~~~~~~~~~~~~~~~~~~

Cách projector được render cũng ảnh hưởng đến hiệu suất. Thiết lập dự án nâng cao **Rendering > Textures > Light Projectors > Filter** cho phép bạn kiểm soát cách lọc texture của projector. **Nearest/Linear** không sử dụng mipmap, nhờ đó render nhanh hơn. Tuy nhiên, projector sẽ trông bị nhiễu hạt khi ở xa. **Nearest/Linear Mipmaps** sẽ trông mượt hơn khi ở xa, nhưng projector sẽ bị mờ khi nhìn từ các góc xiên. Có thể khắc phục điều này bằng cách sử dụng **Nearest/Linear Mipmaps Anisotropic**, đây là chế độ có chất lượng cao nhất nhưng cũng tốn tài nguyên nhất.

Nếu project của bạn có phong cách pixel art, hãy cân nhắc đặt bộ lọc thành một trong các giá trị **Nearest** để projector sử dụng phép lọc nearest-neighbor. Nếu không, hãy dùng **Linear**.
