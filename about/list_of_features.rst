:allow_comments: False

.. _doc_list_of_features:

Danh sách tính năng
===================

Trang này nhằm liệt kê **tất cả** các tính năng hiện được Godot hỗ trợ.

.. note::

    Trang này liệt kê các tính năng được phiên bản ổn định hiện tại của Godot hỗ trợ. Một số tính năng trong đó không có trong `3.x release series <https://docs.godotengine.org/en/3.6/about/list_of_features.html>`__.

Nền tảng
--------

.. seealso::

    Xem :ref:`doc_system_requirements` để biết các yêu cầu về phiên bản phần cứng và phần mềm.

.. note::

    Để biết thông tin về hỗ trợ console, xem `trang web Godot <https://godotengine.org/consoles/>`_.

**Có thể chạy cả editor và các project đã export:**

- Windows (x86 và ARM, 64-bit và 32-bit). - macOS (x86 và ARM, chỉ 64-bit). - Linux (x86 và ARM, 64-bit và 32-bit).

   - Các binary được liên kết tĩnh và có thể chạy trên bất kỳ distribution nào nếu được biên dịch trên một base distribution đủ cũ. - Các binary chính thức được biên dịch bằng `Godot Engine buildroot <https://github.com/godotengine/buildroot>`__, cho phép binary hoạt động trên các Linux distribution phổ biến.

- Android (hỗ trợ editor đang ở trạng thái thử nghiệm). - :ref:`Web browsers <doc_using_the_web_editor>`. Đang thử nghiệm trong 4.0; thay vào đó, nên sử dụng Godot 3.x khi nhắm đến HTML5.

.. note::

    Linux hỗ trợ rv64 (RISC-V), ppc64 & ppc32 (PowerPC) và loongarch64. Tuy nhiên, bạn phải tự biên dịch editor cho nền tảng đó (cũng như các export template); hiện chưa cung cấp bản tải xuống chính thức. Có thể tìm hướng dẫn biên dịch RISC-V trên trang :ref:`doc_compiling_for_linuxbsd`.

**Chạy các project đã export:**

- iOS.

Godot hướng đến việc độc lập với nền tảng nhiều nhất có thể và có thể
:ref:`ported to new platforms <doc_custom_platform_ports>` with relative ease.

.. note::

    Các project viết bằng C# sử dụng Godot 4 hiện không thể export sang nền tảng web. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3. Hỗ trợ nền tảng Android và iOS có từ Godot 4.2, nhưng đang ở trạng thái thử nghiệm và :ref:`some limitations apply <doc_c_sharp_platforms>`.

Editor
------

**Tính năng:**

- Scene tree editor. - Built-in script editor. Cũng hỗ trợ chỉnh sửa các tệp văn bản và sử dụng custom syntax highlighter. - Hỗ trợ :ref:`external script editors <doc_external_editor>` như Visual Studio Code hoặc Vim. - GDScript :ref:`debugger <doc_debugger_panel>`.

   - Hỗ trợ debugging trong các thread.

- Visual profiler với thông tin thời gian CPU và GPU cho từng bước của rendering pipeline. - Các công cụ theo dõi hiệu năng, bao gồm
  :ref:`custom performance monitors <doc_custom_performance_monitors>`.
- Hỗ trợ :ref:`tracing profilers <doc_tracing_profilers>` như
  :ref:`doc_profiler_tracy` and :ref:`doc_profiler_perfetto` for deeper optimization tasks.
- Bất kỳ script nào cũng có thể được :ref:`run in the editor <doc_running_code_in_the_editor>` và cung cấp chức năng tùy chỉnh như các nút có thể nhấp trong inspector mà không cần tạo editor plugin. - Live script reloading. - Live scene editing.

   - Các thay đổi *sẽ* được phản ánh trong editor và *sẽ* được giữ lại sau khi đóng project đang chạy.

- Live camera replication (bị tắt theo mặc định).

   - Di chuyển camera trong editor và xem kết quả trong project đang chạy.

- Remote inspector.

   - Các thay đổi *sẽ không* được phản ánh trong editor và *sẽ không* được giữ lại sau khi đóng project đang chạy.

- Chạy đồng thời nhiều instance của project từ một instance editor duy nhất (hữu ích khi kiểm thử client/server). - Tùy chọn :ref:`game embedding <doc_game_embedding>` để chạy project trong một panel bên trong editor.

  - Chọn các node 2D và 3D trong viewport của project để kiểm tra chúng trong editor. - Di chuyển camera trong project bằng cách sử dụng các camera override 2D và 3D. - Hỗ trợ điều chỉnh time scale, tạm dừng và tiến từng frame. - Hỗ trợ tắt tiếng project.

- Công cụ thước để đo khoảng cách trong 2D và 3D. - Hỗ trợ vertex snapping trong 3D. - Hỗ trợ theo dõi lựa chọn khi lựa chọn di chuyển trong 3D bằng cách sử dụng Focus Selection hai lần. - Tài liệu tham khảo class offline tích hợp sẵn. - Sử dụng editor bằng hàng chục ngôn ngữ do cộng đồng đóng góp.

**Plugin:**

- Editor plugin có thể được tải xuống từ
  :ref:`Asset Store <doc_what_is_asset_store>` to extend editor functionality.
- :ref:`Create your own plugins <doc_making_plugins>` bằng GDScript để thêm tính năng mới hoặc tăng tốc workflow của bạn. - :ref:`Download projects from the Asset Store <doc_using_asset_store_editor>` trong Project Manager và import chúng trực tiếp.

Rendering
---------

Godot 4 bao gồm ba renderer:

- **Forward+**. Renderer tiên tiến nhất, chỉ phù hợp với các nền tảng desktop. Được sử dụng theo mặc định trên các nền tảng desktop. Renderer này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm rendering driver và sử dụng backend **RenderingDevice**. - **Mobile**. Có ít tính năng hơn nhưng render các scene đơn giản nhanh hơn. Phù hợp với các nền tảng mobile và desktop. Được sử dụng theo mặc định trên các nền tảng mobile. Renderer này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm rendering driver và sử dụng backend **RenderingDevice**. - **Compatibility**, đôi khi được gọi là **GL Compatibility**. Renderer ít tiên tiến nhất, phù hợp với các nền tảng desktop và mobile cấp thấp. Được sử dụng theo mặc định trên nền tảng web. Renderer này sử dụng **OpenGL** làm rendering driver.

.. seealso::

    Xem :ref:`doc_renderers` để biết so sánh chi tiết các phương pháp rendering.

Đồ họa 2D
---------

- Rendering sprite, polygon và line.

   - Các công cụ cấp cao để vẽ line và polygon như
     :ref:`class_Polygon2D` and :ref:`class_Line2D`, with support for texturing.

- :ref:`class_AnimatedSprite2D` làm helper để tạo sprite animated. - Các lớp parallax.

   - Hỗ trợ pseudo-3D, bao gồm xem trước trong editor.

- :ref:`2D lighting <doc_2d_lights_and_shadows>` với normal map và specular map.

   - Đèn 2D dạng point (omni/spot) và directional. - Shadow cứng hoặc mềm (có thể điều chỉnh theo từng đèn). - Custom shader có thể truy cập biểu diễn :abbr:`SDF (Signed Distance Field)` theo thời gian thực của scene 2D dựa trên các node :ref:`class_LightOccluder2D`, có thể được sử dụng để cải thiện hiệu ứng chiếu sáng 2D, bao gồm global illumination 2D.

- :ref:`Font rendering <doc_gui_using_fonts>` bằng bitmap, rasterization bằng FreeType hoặc multi-channel signed distance field (MSDF).

   - Bitmap font có thể được export bằng các công cụ như BMFont hoặc import từ hình ảnh (chỉ dành cho font fixed-width). - Dynamic font hỗ trợ font monochrome cũng như font màu (ví dụ: emoji). Các định dạng được hỗ trợ là TTF, OTF, WOFF1 và WOFF2. - Dynamic font hỗ trợ outline font tùy chọn với chiều rộng và màu có thể điều chỉnh. - Dynamic font hỗ trợ variable font và các tính năng OpenType, bao gồm ligature. - Dynamic font hỗ trợ bold và italic mô phỏng khi tệp font không có các style đó. - Dynamic font hỗ trợ oversampling để giữ cho font sắc nét ở độ phân giải cao hơn. - Dynamic font hỗ trợ định vị subpixel để làm font rõ nét hơn ở kích thước nhỏ. - Dynamic font hỗ trợ tối ưu hóa LCD subpixel để làm font thậm chí rõ nét hơn ở kích thước nhỏ. - Font signed distance field có thể được scale ở bất kỳ độ phân giải nào mà không cần rasterization lại. Việc sử dụng multi-channel giúp font SDF scale xuống các kích thước nhỏ tốt hơn so với font SDF monochrome.

- :ref:`Oversampling <doc_multiple_resolutions_font_and_image_oversampling>` cho hình ảnh SVG bằng cách sử dụng loại import :ref:`class_DPITexture`. Điều này cho phép đạt kết quả sắc nét hơn khi scale texture lên bằng cách rasterization lại hình ảnh nguồn SVG ở độ phân giải mới trong runtime.

  - Oversampling có thể tùy chọn tính đến scale :ref:`class_CanvasItem` riêng lẻ để rendering sắc nét hơn khi scale node.

- :ref:`particles <doc_particle_systems_2d>` dựa trên GPU với hỗ trợ
  :ref:`custom particle shaders <doc_particle_shader>`.
- Particle dựa trên CPU. - Tùy chọn :ref:`2D HDR rendering <doc_environment_and_post_processing_using_glow_in_2d>` để có khả năng glow tốt hơn. - Debanding tùy chọn để giảm artifact banding trong gradient. - :ref:`HDR output <doc_hdr_output>` trên các nền tảng và renderer được hỗ trợ.

Công cụ 2D
----------

- :ref:`TileMaps <doc_using_tilemaps>` để thiết kế level 2D dựa trên tile. - Camera 2D với tính năng smoothing và drag margin tích hợp sẵn. - Node Path2D để biểu diễn một path trong không gian 2D.

   - Có thể được vẽ trong editor hoặc tạo theo thủ tục. - Node PathFollow2D để khiến các node đi theo một Path2D.

- :ref:`2D geometry helper class <class_Geometry2D>`.

Vật lý 2D
---------

**Physics body:**

- Static body. - Animatable body (dành cho các object chỉ di chuyển bằng script hoặc animation, chẳng hạn như cửa và platform). - Rigid body. - Character body. - Joint. - Area để phát hiện các body đi vào hoặc rời khỏi nó. - :ref:`Physics interpolation <doc_physics_interpolation>`.

**Phát hiện va chạm:**

- Shape tích hợp sẵn: line, box, circle, capsule, world boundary (mặt phẳng vô hạn). - Polygon va chạm (có thể được vẽ thủ công hoặc tạo từ sprite trong editor).

Đồ họa 3D
---------

- Tính toán chiếu sáng nội bộ HDR tuyến tính. - Debanding tùy chọn để giảm artifact banding trong gradient. - :ref:`HDR output <doc_hdr_output>` trên các nền tảng và renderer được hỗ trợ. - Camera perspective, orthographic và frustum-offset. - Khi sử dụng renderer Forward+, depth prepass được dùng để cải thiện hiệu năng trong các scene phức tạp bằng cách giảm chi phí overdraw. - :ref:`doc_variable_rate_shading` trên các GPU được hỗ trợ trong Forward+ và Mobile.

**Rendering dựa trên vật lý (các tính năng material tích hợp sẵn):**

- Tuân theo model PBR của Disney. - Hỗ trợ các chế độ diffuse shading Burley, Lambert, Lambert Wrap (half-Lambert) và Toon. - Hỗ trợ các chế độ specular shading Schlick-GGX, Toon và Disabled. - Sử dụng workflow roughness-metallic với hỗ trợ cho texture ORM. - Sử dụng horizon specular occlusion (model Filament) để cải thiện hình thức của material. - Normal mapping. - Parallax/relief mapping với level of detail tự động dựa trên khoảng cách. - Detail mapping cho albedo map và normal map. - Subsurface scattering và transmittance. - Screen-space refraction với hỗ trợ cho roughness của material (tạo ra refraction mờ). - Proximity fade (soft particle) và distance fade. - Distance fade có thể sử dụng alpha blending hoặc dithering để tránh đi qua transparent pipeline. - Dithering có thể được xác định theo từng pixel hoặc từng object.

**Chiếu sáng theo thời gian thực:**

- :ref:`Directional lights <doc_lights_and_shadows_directional_light>` (mặt trời/mặt trăng). - :ref:`Omnidirectional lights <doc_lights_and_shadows_omni_light>`. - :ref:`Spot lights <doc_lights_and_shadows_spot_light>` với góc hình nón và độ suy giảm có thể điều chỉnh. - :ref:`Rectangular area lights <doc_lights_and_shadows_area_light>` với texture tùy chọn để xác định hình dạng và màu sắc. - Có thể điều chỉnh năng lượng của ánh sáng specular, ánh sáng gián tiếp và sương mù thể tích cho từng đèn. - Có thể điều chỉnh "kích thước" ánh sáng cho đèn omni hình cầu và đèn spot dạng đĩa (đồng thời làm bóng mờ hơn với vùng nửa tối thay đổi). - Hệ thống làm mờ theo khoảng cách tùy chọn để làm mờ các đèn ở xa và bóng của chúng, giúp cải thiện hiệu năng. - Khi sử dụng renderer Forward+ (mặc định trên máy tính), các đèn được render bằng các tối ưu hóa forward theo cụm để giảm chi phí riêng lẻ. Clustered rendering cũng loại bỏ mọi giới hạn về số lượng đèn có thể sử dụng trên một mesh. - Khi sử dụng renderer Mobile, mỗi mesh resource có thể hiển thị tối đa 8 đèn omni, 8 đèn spot và 8 đèn area. Có thể sử dụng baked lighting để vượt qua giới hạn này nếu cần.

**Shadow mapping:**

- *DirectionalLight3D:* Orthogonal (nhanh nhất), PSSM 2-split và 4-split. Hỗ trợ hòa trộn giữa các split. - *OmniLight3D:* Dual paraboloid (nhanh) hoặc cubemap (chậm hơn nhưng chính xác hơn). Hỗ trợ texture projector có màu dưới dạng panorama. - *SpotLight3D:* Texture đơn. Hỗ trợ texture projector có màu. - *AreaLight3D:* Texture đơn với biến dạng dual paraboloid để xấp xỉ hình dạng ánh sáng. - Độ lệch pháp tuyến của bóng và shadow pancaking để giảm lượng shadow acne và peter-panning hiển thị. - Độ mờ bóng dựa trên kích thước đèn và khoảng cách từ bề mặt mà bóng được chiếu, tương tự :abbr:`PCSS (Percentage Closer Soft Shadows)`. Được hỗ trợ cho mọi loại đèn. - Có thể điều chỉnh độ mờ bóng cho từng đèn.

**Global illumination with indirect lighting:**

- :ref:`Baked lightmaps <doc_using_lightmap_gi>` (nhanh nhưng không thể cập nhật trong runtime).

   - Hỗ trợ bake chỉ ánh sáng gián tiếp hoặc cả ánh sáng trực tiếp và gián tiếp. Có thể điều chỉnh chế độ bake cho từng đèn để hỗ trợ các thiết lập bake ánh sáng kết hợp. - Hỗ trợ chiếu sáng các đối tượng động bằng probe tự động và probe được đặt thủ công. - Tùy chọn hỗ trợ chiếu sáng định hướng dựa trên spherical harmonics. - Tùy chọn hỗ trợ bake shadowmask cho các bóng định hướng tĩnh ở xa. - Tùy chọn supersampling khi bake để cải thiện chất lượng và giảm hiện tượng rò rỉ ánh sáng, đổi lại thời gian bake và mức sử dụng bộ nhớ trong quá trình bake sẽ tăng. - Lightmap được bake trên GPU bằng compute shader (nhanh hơn nhiều so với lightmapping trên CPU). Chỉ có thể thực hiện bake từ editor, không phải trong các project đã export. - Hỗ trợ :ref:`denoising <doc_using_lightmap_gi_denoising>` dựa trên GPU với JNLM ngay khi cài đặt, hoặc khử nhiễu chất lượng cao hơn dựa trên CPU/GPU với OIDN (yêu cầu tải OIDN riêng). - Lightmap được render bằng bộ lọc bicubic để giảm các lỗi khi scale.

- :ref:`Voxel-based GI probes <doc_using_voxel_gi>`. Hỗ trợ cả light động *và* occluder động, đồng thời hỗ trợ reflection. Yêu cầu một bước bake nhanh, có thể thực hiện trong editor hoặc runtime (bao gồm cả từ project đã export). - :ref:`Signed-distance field GI <doc_using_sdfgi>` được thiết kế cho các thế giới mở lớn. Hỗ trợ light động nhưng không hỗ trợ occluder động. Hỗ trợ reflection. Không yêu cầu bake. - :ref:`Screen-space indirect lighting (SSIL) <doc_environment_and_post_processing_ssil>` ở độ phân giải một nửa hoặc đầy đủ. Hoàn toàn real-time và hỗ trợ mọi loại nguồn sáng phát xạ (bao gồm decal). - VoxelGI và SDFGI sử dụng một deferred pass để cho phép render GI ở độ phân giải một nửa nhằm cải thiện hiệu năng (đồng thời vẫn hỗ trợ MSAA hoạt động bình thường).

**Reflections:**

- Reflection dựa trên voxel (khi sử dụng GI probe) và reflection dựa trên SDF (khi sử dụng signed distance field GI). Reflection dựa trên voxel hiển thị trên các bề mặt trong suốt, trong khi reflection dựa trên SDF thô cũng hiển thị trên các bề mặt trong suốt. - Reflection bake nhanh hoặc reflection real-time chậm bằng ReflectionProbe. Có thể tùy chọn bật hiệu chỉnh hộp parallax. - Reflection trong screen-space với hỗ trợ roughness của material. - Có thể kết hợp các kỹ thuật reflection để đạt độ chính xác hoặc khả năng mở rộng cao hơn. - Khi sử dụng renderer Forward+ (mặc định trên máy tính), các reflection probe được render bằng các tối ưu hóa forward theo cụm để giảm chi phí riêng lẻ. Clustered rendering cũng loại bỏ mọi giới hạn về số lượng reflection probe có thể sử dụng trên một mesh. - Khi sử dụng renderer Mobile, mỗi mesh resource có thể hiển thị tối đa 8 reflection probe. Khi sử dụng renderer Compatibility, mỗi mesh resource có thể hiển thị tối đa 2 reflection probe.

**Decals:**

- :ref:`Supports albedo <doc_using_decals>`, emissive, :abbr:`ORM (Occlusion Roughness Metallic)` và normal mapping. - Các kênh texture được phủ mượt lên trên material bên dưới, hỗ trợ decal chỉ có normal/ORM. - Hỗ trợ fade theo normal để làm mờ decal tùy thuộc vào góc tới của nó. - Không phụ thuộc vào việc tạo mesh trong runtime. Điều này có nghĩa là decal có thể được sử dụng trên các mesh skinned phức tạp mà không bị phạt hiệu năng, ngay cả khi decal di chuyển ở mỗi frame. - Hỗ trợ lọc texture nearest, bilinear, trilinear hoặc anisotropic (được cấu hình trên toàn cục). - Hệ thống làm mờ theo khoảng cách tùy chọn để làm mờ các decal ở xa, giúp cải thiện hiệu năng. - Khi sử dụng renderer Forward+ (mặc định trên máy tính), các decal được render bằng các tối ưu hóa forward theo cụm để giảm chi phí riêng lẻ. Clustered rendering cũng loại bỏ mọi giới hạn về số lượng decal có thể sử dụng trên một mesh. - Khi sử dụng renderer Mobile, mỗi mesh resource có thể hiển thị tối đa 8 decal.

**Sky:**

- Sky panorama (sử dụng HDRI). - Sky procedural và sky dựa trên vật lý (Physically-based sky) phản hồi với các DirectionalLight trong scene. - Hỗ trợ :ref:`custom sky shaders <doc_sky_shader>`, có thể được animate. - Bản đồ radiance được sử dụng cho ánh sáng ambient và specular có thể được cập nhật theo thời gian thực tùy thuộc vào các thiết lập chất lượng đã chọn.

**Fog:**

- Sương mù độ sâu theo hàm mũ. - Sương mù độ cao theo hàm mũ. - Hỗ trợ tự động xác định màu sương mù dựa trên màu sky (aerial perspective). - Hỗ trợ tán xạ ánh sáng mặt trời trong sương mù. - Hỗ trợ kiểm soát mức độ ảnh hưởng của việc render sương mù lên sky, với các tùy chọn điều khiển riêng cho sương mù truyền thống và sương mù thể tích. - Hỗ trợ để các material cụ thể bỏ qua sương mù.

**Volumetric fog:**

- :ref:`volumetric fog <doc_volumetric_fog>` toàn cục phản hồi với ánh sáng và bóng. - Sương mù thể tích có thể tính đến ánh sáng gián tiếp khi sử dụng VoxelGI hoặc SDFGI. - Các node fog volume có thể được đặt để thêm sương mù vào những khu vực cụ thể (hoặc loại bỏ sương mù khỏi những khu vực cụ thể). Các hình dạng được hỗ trợ gồm box, ellipse, cone, cylinder và density map dựa trên texture 3D. - Mỗi fog volume có thể có shader tùy chỉnh riêng. - Có thể sử dụng cùng với sương mù truyền thống.

**Particles:**

- Particle dựa trên GPU với hỗ trợ subemitter (2D + 3D), trail (2D + 3D), attractor (chỉ 3D) và collision (2D + 3D).

  - Các hình dạng attractor của particle 3D được hỗ trợ: box, sphere và vector field 3D. - Các hình dạng collision của particle 3D được hỗ trợ: box, sphere, signed distance field đã bake và heightmap theo thời gian thực (phù hợp với hiệu ứng thời tiết trong thế giới mở). - Collision của particle 2D được xử lý bằng signed distance field được tạo theo thời gian thực dựa trên các node :ref:`class_LightOccluder2D` trong scene. - Trail có thể sử dụng mesh ribbon trail và tube trail tích hợp sẵn, hoặc mesh tùy chỉnh có skeleton. - Hỗ trợ shader particle tùy chỉnh với emission thủ công.

- Particle dựa trên CPU.

**Post-processing:**

- Tonemapping (Linear, Reinhard, Filmic, ACES, AgX). - Tự động điều chỉnh exposure dựa trên độ sáng của viewport (và ghi đè exposure thủ công). - Depth of field gần và xa với mô phỏng bokeh có thể điều chỉnh (box, hexagon, circle). - Ambient occlusion trong screen-space (SSAO) ở độ phân giải một nửa hoặc đầy đủ. - Glow/bloom với tùy chọn upscale bicubic và một số blend mode: Screen, Soft Light, Add, Replace, Mix. - Glow có thể sử dụng texture dirt map có màu, hoạt động như hiệu ứng bụi trên ống kính. - Glow có thể được :ref:`used as a screen-space blur effect <doc_environment_and_post_processing_using_glow_to_blur_the_screen>`. - Hiệu chỉnh màu bằng ramp một chiều hoặc texture LUT 3D. - Bộ giới hạn roughness để giảm ảnh hưởng của hiện tượng aliasing specular. - Điều chỉnh độ sáng, độ tương phản và độ bão hòa.

**Texture filtering:**

- Lọc nearest, bilinear, trilinear hoặc anisotropic. - Các tùy chọn lọc được xác định theo từng lần sử dụng, không phải theo từng texture.

**Texture VRAM compression:**

- BPTC (để nén chất lượng cao nhắm đến các nền tảng máy tính). - ASTC (để nén chất lượng cao nhắm đến các nền tảng di động). - ETC2 (để nén nhanh nhắm đến các nền tảng di động). - S3TC (để nén nhanh nhắm đến các nền tảng máy tính). - Basis Universal (chậm nhưng chỉ yêu cầu một lần encoding cho mọi nền tảng).

**Antialiasing:**

- Temporal :ref:`antialiasing <doc_3d_antialiasing>` (TAA). - AMD FidelityFX Super Resolution 2.2 :ref:`antialiasing <doc_3d_antialiasing>` (FSR2), có thể được sử dụng ở độ phân giải gốc như một dạng antialiasing theo thời gian chất lượng cao. - Multi-sample antialiasing (MSAA), cho cả :ref:`doc_2d_antialiasing` và :ref:`doc_3d_antialiasing`. - Fast approximate antialiasing (FXAA). - Super-sample antialiasing (SSAA) sử dụng scaling 3D bilinear và scale độ phân giải 3D lớn hơn 1.0. - Antialiasing alpha, alpha to coverage của MSAA và alpha hashing theo từng material.

**Resolution scaling:**

- Hỗ trợ :ref:`rendering 3D at a lower resolution <doc_resolution_scaling>` trong khi vẫn giữ việc render 2D ở scale gốc. Tính năng này có thể được sử dụng để cải thiện hiệu năng trên các hệ thống cấp thấp hoặc cải thiện hình ảnh trên các hệ thống cấp cao. - Resolution scaling sử dụng lọc nearest-neighbor, lọc bilinear, AMD FidelityFX Super Resolution 1.0 (FSR1) hoặc AMD FidelityFX Super Resolution 2.2.1 (FSR2). - Độ lệch LOD mipmap của texture được tự động điều chỉnh để cải thiện chất lượng ở các scale độ phân giải thấp hơn. Độ lệch này cũng có thể được sửa đổi bằng một offset thủ công.

Hầu hết các hiệu ứng được liệt kê ở trên có thể được điều chỉnh để đạt hiệu suất tốt hơn hoặc cải thiện chất lượng hơn nữa. Điều này có thể hữu ích khi
:ref:`using Godot for offline rendering <doc_creating_movies>`.

Công cụ 3D
----------

- Mesh tích hợp sẵn: hình lập phương, hình trụ/hình nón, hình cầu (bán cầu), lăng trụ, mặt phẳng, hình tứ giác, hình xuyến, dải, ống. - :ref:`GridMaps <doc_using_gridmaps>` cho thiết kế màn chơi 3D dựa trên ô. - :ref:`Constructive solid geometry <doc_csg_tools>` (dùng cho việc tạo nguyên mẫu). - Công cụ cho :ref:`procedural geometry generation <doc_procedural_geometry>`. - Node Path3D để biểu diễn một đường dẫn trong không gian 3D.

   - Có thể được vẽ trong editor hoặc tạo theo quy trình. - Node PathFollow3D để khiến các node đi theo một Path3D.

- :ref:`3D geometry helper class <class_Geometry3D>`. - Hỗ trợ xuất scene hiện tại dưới dạng tệp glTF 2.0, cả từ editor lẫn tại runtime từ một project đã export.

Vật lý 3D
---------

**Các physics body:**

- Body tĩnh. - Body có thể animate (dành cho các đối tượng chỉ chuyển động bằng script hoặc animation, chẳng hạn như cửa và bệ). - Body rigid. - Body character. - Body phương tiện (dành cho vật lý arcade, không phải mô phỏng). - Joint. - :ref:`Soft bodies <doc_soft_body>`. - :ref:`Ragdolls <doc_ragdoll_system>`. - Area để phát hiện các body đi vào hoặc rời khỏi nó. - :ref:`Physics interpolation <doc_physics_interpolation>`.

**Phát hiện va chạm:**

- Shape tích hợp sẵn: hình hộp chữ nhật, hình cầu, capsule, hình trụ, biên thế giới (mặt phẳng vô hạn). - Tạo shape va chạm dạng tam giác cho mọi mesh từ editor. - Tạo một hoặc nhiều shape va chạm lồi cho mọi mesh từ editor.

Shader
------

- *2D:* Shader vertex, fragment và light tùy chỉnh. - *3D:* Shader vertex, fragment, light, sky và fog tùy chỉnh. - Shader tùy chỉnh có thể tạo và sửa đổi texture theo quy trình trong thời gian thực bằng cách sử dụng
  :ref:`class_DrawableTexture2D`.
- Shader dựa trên văn bản sử dụng :ref:`shader language inspired by GLSL <doc_shading_language>`. - GitHub cung cấp syntax highlighting bằng cách sử dụng ``gdshader`` làm tên ngôn ngữ trong một khối mã Markdown. - Trình chỉnh sửa visual shader.

   - Hỗ trợ :ref:`visual shader plugins <doc_visual_shader_plugins>`.

Scripting
---------

**Tổng quát:**

- Mẫu thiết kế hướng đối tượng với các script mở rộng node. - Signal và group để giao tiếp giữa các script. - Hỗ trợ :ref:`cross-language scripting <doc_cross_language_scripting>`. - Nhiều kiểu dữ liệu đại số tuyến tính 2D, 3D và 4D như vector và transform.

:ref:`GDScript: <doc_gdscript>`

- :ref:`High-level interpreted language <doc_gdscript_reference>` với
  :ref:`optional static typing <doc_gdscript_static_typing>`.
- Cú pháp lấy cảm hứng từ Python. Tuy nhiên, GDScript **không** dựa trên Python. - GitHub cung cấp syntax highlighting bằng cách sử dụng ``gdscript`` làm tên ngôn ngữ trong một khối mã Markdown. - :ref:`Use threads <doc_using_multiple_threads>` để thực hiện các tác vụ bất đồng bộ hoặc tận dụng nhiều lõi bộ xử lý.

:ref:`C#: <doc_c_sharp>`

- Được đóng gói trong một binary riêng để giảm kích thước tệp và số lượng dependency. - Hỗ trợ .NET 8 trở lên.

   - Hỗ trợ đầy đủ cú pháp và tính năng của C# 12.0.

- Hỗ trợ Windows, Linux và macOS. Kể từ Godot 4.2, hỗ trợ thử nghiệm cho Android và iOS cũng đã có.

   - Trên nền tảng iOS, chỉ một số kiến trúc được hỗ trợ: ``arm64``. - Nền tảng web hiện chưa được hỗ trợ. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3.

- Khuyến nghị sử dụng editor bên ngoài để tận dụng các chức năng IDE.

**GDExtension (C, C++, Rust, D, ...):**

- Khi cần, hãy liên kết với các thư viện native để đạt hiệu suất cao hơn và tích hợp với bên thứ ba.

   - Để lập trình logic game, GDScript hoặc C# được khuyến nghị nếu hiệu suất của chúng phù hợp.

- Các binding GDExtension chính thức cho `C <https://github.com/godotengine/godot-headers>`__ và `C++ <https://github.com/godotengine/godot-cpp>`__.

   - Sử dụng bất kỳ build system và tính năng ngôn ngữ nào bạn muốn.

- Các binding GDExtension cho `D <https://github.com/godot-dlang/godot-dlang>`__, `Swift <https://github.com/migueldeicaza/SwiftGodot>`__ và `Rust <https://github.com/godot-rust/gdextension>`__ đang được cộng đồng tích cực phát triển. (Một số binding trong đó có thể đang ở trạng thái thử nghiệm và chưa sẵn sàng cho môi trường production).

Âm thanh
--------

**Tính năng:**

- Đầu ra mono, stereo, 5.1 và 7.1. - Phát lại không định vị và có định vị trong 2D và 3D.

   - Hiệu ứng Doppler tùy chọn trong 2D và 3D.

- Hỗ trợ :ref:`audio buses <doc_audio_buses>` có thể định tuyến lại và các hiệu ứng với hàng chục hiệu ứng được tích hợp sẵn. - Hỗ trợ polyphony (phát nhiều âm thanh từ một node :ref:`class_AudioStreamPlayer`). - Hỗ trợ âm lượng và cao độ ngẫu nhiên. - Hỗ trợ điều chỉnh cao độ theo thời gian thực. - Hỗ trợ chọn sample tuần tự/ngẫu nhiên, bao gồm ngăn lặp lại khi chọn sample ngẫu nhiên. - Các node :ref:`class_AudioListener2D` và :ref:`class_AudioListener3D` để lắng nghe từ một vị trí khác với camera. - Hỗ trợ :ref:`procedural audio generation <class_AudioStreamGenerator>`. - Đầu vào âm thanh để ghi âm microphone. - :ref:`Text to speech <doc_text_to_speech>` bằng các engine TTS do nền tảng cung cấp. - Đầu vào MIDI.

   - Hiện chưa hỗ trợ đầu ra MIDI.

**API được sử dụng:**

- *Windows:* WASAPI. - *macOS:* CoreAudio. - *Linux:* PulseAudio hoặc ALSA.

Import
------

- Hỗ trợ :ref:`custom import plugins <doc_import_plugins>`.

**Định dạng:**

- *Hình ảnh:* Xem :ref:`doc_importing_images`. - *Âm thanh:*

   - WAV với tính năng nén :abbr:`QOA (Quite OK Audio)` hoặc IMA-ADPCM tùy chọn. - Ogg Vorbis. - MP3.

- *Scene 3D:* Xem :ref:`doc_importing_3d_scenes`.

   - glTF 2.0 *(khuyến nghị)*. - ``.blend`` (bằng cách gọi minh bạch chức năng export glTF của Blender). - FBX (bằng cách gọi minh bạch `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__). - Collada (.dae). - Wavefront OBJ (chỉ scene tĩnh, có thể được tải trực tiếp dưới dạng mesh hoặc import dưới dạng scene 3D).

- Hỗ trợ tải scene glTF 2.0 tại runtime, bao gồm từ một project đã export. - Mesh 3D sử dụng `Mikktspace <http://www.mikktspace.com/>`__ để tạo tangent khi import, đảm bảo tính nhất quán với các ứng dụng 3D khác như Blender.

Input
-----

- :ref:`Input mapping system <doc_input_examples>` bằng các input event được hardcode hoặc các input action có thể remap.

   - Các giá trị trục có thể được ánh xạ tới hai action khác nhau với deadzone có thể cấu hình. - Sử dụng cùng một đoạn code để hỗ trợ cả keyboard và gamepad.

- Đầu vào từ keyboard.

   - Các phím có thể được ánh xạ ở chế độ "physical" để không phụ thuộc vào bố cục keyboard.

- Đầu vào từ mouse.

   - Con trỏ mouse có thể hiển thị, ẩn, bị capture hoặc bị giới hạn trong cửa sổ. - Có thể thay đổi giao diện con trỏ mouse thành hình ảnh tùy chỉnh hoặc một trong các con trỏ hệ thống. - Khi bị capture, input thô được sử dụng trên Windows và Linux để bỏ qua các thiết lập tăng tốc mouse của hệ điều hành.

- :ref:`Gamepad input <doc_controllers_gamepads_joysticks>` (tối đa 8 controller đồng thời).

  - Hỗ trợ :ref:`changing the LED color <doc_controller_features_led_color>` trên các controller được hỗ trợ. - Hỗ trợ :ref:`reading motion sensors <doc_controller_features_motion_sensors>` trên các controller được hỗ trợ (dùng để triển khai ngắm bằng gyro).

- Đầu vào từ bút/tablet với hỗ trợ áp lực và độ nghiêng.

Navigation
----------

- Thuật toán A* trong :ref:`2D <class_AStar2D>` và :ref:`3D <class_AStar3D>`. - Navigation mesh với khả năng tránh chướng ngại vật động trong
  :ref:`2D <doc_navigation_overview_2d>` and :ref:`3D <doc_navigation_overview_3d>`.
- Tạo navigation mesh từ editor hoặc tại runtime (bao gồm từ một project đã export).

Networking
----------

- Networking TCP cấp thấp bằng :ref:`class_StreamPeer` và :ref:`class_TCPServer`. - Networking UDP cấp thấp bằng :ref:`class_PacketPeer` và :ref:`class_UDPServer`. - HTTP request cấp thấp bằng :ref:`class_HTTPClient`. - HTTP request cấp cao bằng :ref:`class_HTTPRequest`.

   - Hỗ trợ HTTPS ngay khi cài đặt bằng các certificate đi kèm.

- API :ref:`High-level multiplayer <doc_high_level_multiplayer>` sử dụng UDP và ENet.

   - Replication tự động bằng remote procedure call (RPC). - Hỗ trợ truyền không tin cậy, tin cậy và có thứ tự.

- :ref:`WebSocket <doc_websocket>` client và server, khả dụng trên mọi nền tảng. - :ref:`WebRTC <doc_webrtc>` client và server, khả dụng trên mọi nền tảng. - Hỗ trợ :ref:`UPnP <class_UPNP>` để tránh yêu cầu forward port khi host server phía sau NAT.

Quốc tế hóa
-----------

- Hỗ trợ đầy đủ Unicode, bao gồm emoji. - Hỗ trợ tải system font trên Windows, macOS và Linux.

  - Theo mặc định, system font được sử dụng làm fallback để hiển thị các ký tự không được hỗ trợ. Điều này cho phép hiển thị đúng văn bản đa ngôn ngữ mà không cần đóng gói các tệp font lớn cùng project.

- Lưu các chuỗi bản địa hóa bằng :ref:`CSV <doc_internationalizing_games>` hoặc :ref:`gettext <doc_localization_using_gettext>`.

  - Hỗ trợ tạo tệp gettext POT và PO từ editor.

- Tự động sử dụng các chuỗi đã bản địa hóa trong project của bạn ở các phần tử GUI hoặc bằng cách sử dụng hàm ``tr()``. - Hỗ trợ pluralization và ngữ cảnh dịch. - Hỗ trợ :ref:`bidirectional typesetting <doc_internationalizing_games_bidi>`, shaping văn bản và các dạng bản địa hóa OpenType. - Tự động phản chiếu UI cho các locale từ phải sang trái. - Hỗ trợ :ref:`pseudolocalization <doc_pseudolocalization>` để kiểm tra mức độ thân thiện với i18n của project.

Quản lý cửa sổ và tích hợp hệ điều hành
---------------------------------------

- Tạo nhiều cửa sổ độc lập trong một process duy nhất. - Di chuyển, thay đổi kích thước, thu nhỏ và phóng to các cửa sổ do project tạo ra. - Thay đổi tiêu đề và icon của cửa sổ. - Tạo các cửa sổ trong suốt để sử dụng làm overlay, với hỗ trợ cho phép chuột đi xuyên qua dựa trên polygon. - Yêu cầu chú ý (sẽ khiến thanh tiêu đề nhấp nháy trên hầu hết các nền tảng). - Chế độ fullscreen (không viền và độc quyền). - Cửa sổ không viền (fullscreen hoặc không fullscreen). - Giữ một cửa sổ luôn ở trên cùng. - Khiến một cửa sổ bỏ qua focus (hữu ích cho overlay). - Khai báo một cửa sổ là popup (ẩn khỏi trình chuyển đổi tác vụ) hoặc exclusive (ngăn tương tác với các cửa sổ khác trong cùng process). - Hỗ trợ hộp thoại tệp native trên Windows, macOS, Linux và Android. - Hỗ trợ icon khay hệ thống trên Windows và macOS. - Tích hợp menu toàn cục trên macOS. - Client-side decorations trên macOS. - Thực thi các lệnh theo cách blocking hoặc non-blocking (bao gồm chạy nhiều instance của cùng một project). - Mở đường dẫn tệp và URL bằng trình xử lý protocol mặc định hoặc tùy chỉnh (nếu đã được đăng ký trên hệ thống). - Phân tích các đối số dòng lệnh tùy chỉnh. - Hỗ trợ screen reader trên Windows, macOS và Linux. - Bất kỳ binary Godot nào (editor hoặc project đã export) đều có thể được
  :ref:`used as a headless server <doc_exporting_for_dedicated_servers>`
  bằng cách khởi động với đối số dòng lệnh ``--headless``. Điều này cho phép chạy engine mà không cần GPU hoặc display server.

.. seealso::

    Xem :ref:`doc_creating_applications` để biết chi tiết về cách sử dụng các tính năng này.

Mobile
------

- :ref:`Virtual joystick <class_VirtualJoystick>` và :ref:`buttons <class_TouchScreenButton>` cho đầu vào cảm ứng. - Mua hàng trong ứng dụng trên :ref:`Android <doc_android_in_app_purchases>` và `iOS <https://github.com/godot-sdk-integrations/godot-storekit2>`_. - Hỗ trợ quảng cáo bằng các module bên thứ ba. - Hỗ trợ chế độ picture-in-picture trên Android.

.. _doc_xr_support:

Hỗ trợ XR (AR và VR)
--------------------

- Hỗ trợ headset desktop bằng :ref:`OpenXR <doc_setting_up_xr>`. Nếu một headset hoạt động với SteamVR thì nó sẽ hoạt động với Godot.

   - Godot cũng hỗ trợ Quest qua Link, AndroidXR Direct Preview và Pico Connect.

- Hỗ trợ :ref:`Android-based headsets <doc_deploying_to_android>` bằng OpenXR. Bao gồm hỗ trợ cho các headset độc lập sau:

   - Meta Quest 1/2/3 và Pro - Pico 4/4 Ultra - Magic Leap 2 - Lynx R1 - HTC Vive Focus Vision - Headset Android XR

- Hỗ trợ Steam Frame độc lập chạy trên nền Linux bằng OpenXR.

- Hỗ trợ hạn chế cho headset Apple visionOS.

  - Hiện tại chỉ hỗ trợ export một ứng dụng để sử dụng trên một mặt phẳng trong headset. Không hỗ trợ các trải nghiệm immersive.

- Các thiết bị khác được hỗ trợ thông qua cấu trúc plugin XR. - Có nhiều toolkit nâng cao triển khai các tính năng phổ biến cần thiết cho ứng dụng XR.

Hệ thống GUI
------------

GUI của Godot được xây dựng bằng các node Control giống với các node được dùng để tạo game trong Godot. UI của editor có thể dễ dàng được mở rộng theo nhiều cách bằng các add-on.

**Nodes:**

- Buttons. - Checkboxes, check buttons, radio buttons. - Nhập văn bản bằng :ref:`class_LineEdit` (một dòng), :ref:`class_TextEdit` (nhiều dòng) và :ref:`class_CodeEdit` (hỗ trợ syntax highlighting, số dòng và nhiều tính năng khác). - Menu dropdown bằng :ref:`class_PopupMenu` và :ref:`class_OptionButton`, với hỗ trợ thanh tìm kiếm tùy chọn. - Thanh cuộn. - Nhãn. - RichTextLabel cho :ref:`text formatted using BBCode <doc_bbcode_in_richtextlabel>`, với hỗ trợ các hiệu ứng tùy chỉnh dạng animation. - Cây (cũng có thể dùng để biểu diễn bảng). - Bộ chọn màu với các chế độ RGB, HSV và OKHSL, cũng như các bảng màu tùy chỉnh. - Các Control có thể được xoay và scale. - Hỗ trợ kéo và thả.

**Sizing:**

- Anchor để giữ các phần tử GUI ở một góc, cạnh cụ thể hoặc ở giữa. - Container để tự động bố trí các phần tử GUI theo những quy tắc nhất định.

   - Layout :ref:`Stack <class_BoxContainer>`. - Layout :ref:`Grid <class_GridContainer>`. - Layout :ref:`Flow <class_FlowContainer>` (tương tự văn bản tự động xuống dòng). - Layout :ref:`Margin <class_MarginContainer>`, :ref:`centered <class_CenterContainer>` và :ref:`aspect ratio <class_AspectRatioContainer>`. - Layout :ref:`Draggable splitter <class_SplitContainer>`. - Layout :ref:`Foldable section <class_FoldableContainer>`.

- Scale đến :ref:`multiple resolutions <doc_multiple_resolutions>` bằng các chế độ stretch ``canvas_items`` hoặc ``viewport``. - Hỗ trợ mọi tỷ lệ khung hình bằng anchor và stretch aspect ``expand``.

**Theming:**

- Trình chỉnh sửa theme tích hợp sẵn.

   - Tạo theme dựa trên các thiết lập theme hiện tại của editor.

- Theming vector dạng procedural bằng :ref:`class_StyleBoxFlat`.

   - Hỗ trợ các góc bo/vát, drop shadow, độ rộng từng border và antialiasing.

- Theming dựa trên texture bằng :ref:`class_StyleBoxTexture`.

Kích thước distribution nhỏ của Godot có thể khiến nó trở thành một lựa chọn phù hợp thay thế cho các framework như Electron hoặc Qt.

Animation
---------

- Kinematics trực tiếp và inverse kinematics. - Hỗ trợ animation cho mọi property với interpolation có thể tùy chỉnh. - Hỗ trợ gọi các method trong animation track. - Hỗ trợ phát âm thanh trong animation track. - Hỗ trợ đường cong Bézier trong animation.

Định dạng tệp
-------------

- Scene và resource có thể được lưu ở định dạng :ref:`text-based <doc_tscn_file_format>` hoặc binary.

   - Định dạng dựa trên văn bản dễ đọc đối với con người và thân thiện hơn với version control. - Định dạng binary lưu/tải nhanh hơn đối với scene/resource lớn.

- Đọc và ghi tệp văn bản hoặc binary bằng :ref:`class_FileAccess`.

   - Có thể tùy chọn nén hoặc mã hóa.

- Đọc và ghi tệp :ref:`class_JSON`. - Đọc và ghi tệp cấu hình kiểu INI bằng :ref:`class_ConfigFile`.

   - Có thể (de)serialize mọi datatype của Godot, bao gồm Vector2/3, Color, ...

- Đọc tệp XML bằng :ref:`class_XMLParser`. - :ref:`Load and save images, audio/video, fonts and ZIP archives <doc_runtime_loading_and_saving>` trong một project đã export mà không cần đi qua hệ thống import của Godot. - Đóng gói dữ liệu game vào tệp PCK (định dạng tùy chỉnh được tối ưu để seek nhanh), vào archive ZIP hoặc trực tiếp vào executable để phân phối dưới dạng một tệp duy nhất. - :ref:`Export additional PCK files<doc_exporting_pcks>` có thể được engine đọc để hỗ trợ mod và DLC.

Khác
----

- :ref:`Video playback <doc_playing_videos>` với hỗ trợ Ogg Theora tích hợp sẵn. - :ref:`Movie Maker mode <doc_creating_movies>` để ghi video từ một project đang chạy với âm thanh được đồng bộ và nhịp khung hình hoàn hảo. - :ref:`Low-level access to servers <doc_using_servers>`, cho phép bỏ qua overhead của scene tree khi cần. - :ref:`Command line interface <doc_command_line_tutorial>` cho automation.

   - Export và deploy project bằng các nền tảng continuous integration. - `Shell completion scripts <https://github.com/godotengine/godot/tree/master/misc/dist/shell>`__ có sẵn cho Bash, zsh và fish. - In văn bản có màu ra standard output trên mọi nền tảng bằng
     :ref:`print_rich <class_@GlobalScope_method_print_rich>`.

- Editor có thể
  :ref:`detect features used in a project and create a compilation profile <doc_engine_compilation_configuration_editor>`,
  có thể được dùng để tạo các binary export template nhỏ hơn bằng cách tắt các tính năng không cần thiết. - Hỗ trợ :ref:`C++ modules <doc_custom_modules_in_cpp>` được liên kết tĩnh vào binary của engine.

  - Hầu hết module tích hợp sẵn có thể được tắt tại thời điểm compile để giảm kích thước binary trong các bản build tùy chỉnh. Xem :ref:`doc_optimizing_for_size` để biết chi tiết.

- Engine và editor được viết bằng C++17.

   - Có thể được :ref:`compiled <doc_introduction_to_the_buildsystem>` bằng GCC, Clang và MSVC. MinGW cũng được hỗ trợ. - Thân thiện với các packager. Trong hầu hết trường hợp, có thể sử dụng các system library thay cho những thư viện do Godot cung cấp. Hệ thống build không tải xuống bất cứ thứ gì. Các bản build có thể được tái lập hoàn toàn.

- Được cấp phép theo giấy phép MIT có tính cho phép.

   - Quy trình phát triển mở với `hoan nghênh đóng góp <https://contributing.godotengine.org/en/latest/index.html>`__.

.. seealso::

    `Repository đề xuất của Godot <https://github.com/godotengine/godot-proposals>`__ liệt kê các tính năng đã được cộng đồng yêu cầu và có thể được triển khai trong các bản phát hành Godot tương lai.
