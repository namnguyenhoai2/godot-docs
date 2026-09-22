:allow_comments: False

.. _doc_list_of_features:

Danh sách tính năng
===================

Trang này nhằm liệt kê **tất cả** các tính năng hiện được Godot hỗ trợ.

.. note::

    Trang này liệt kê các tính năng được phiên bản ổn định hiện tại hỗ trợ
    Godot. Một số tính năng này không có trong
    `nhánh phát hành 3.x <https://docs.godotengine.org/en/3.6/about/list_of_features.html>`__.

Nền tảng
--------

.. seealso::

    Xem :ref:`doc_system_requirements` để biết các yêu cầu về phiên bản phần cứng và phần mềm.

.. note::

    Để biết thông tin về việc hỗ trợ console, hãy xem `trang web Godot <https://godotengine.org/consoles/>`_.

**Có thể chạy cả editor và các project đã export:**

- Windows (x86 và ARM, 64-bit và 32-bit).
- macOS (x86 và ARM, chỉ 64-bit).
- Linux (x86 và ARM, 64-bit và 32-bit).

   - Các binary được liên kết tĩnh và có thể chạy trên mọi distribution nếu được biên dịch trên một distribution nền đủ cũ.
   - Các binary chính thức được biên dịch bằng `Godot Engine buildroot <https://github.com/godotengine/buildroot>`__, cho phép tạo ra các binary hoạt động trên những distribution Linux phổ biến.

- Android (editor đang được hỗ trợ thử nghiệm).
- :ref:`Trình duyệt web <doc_using_the_web_editor>`. Đang thử nghiệm trong 4.0; thay vào đó, khi nhắm đến HTML5, bạn nên sử dụng Godot 3.x.

.. note::

    Linux hỗ trợ rv64 (RISC-V), ppc64 và ppc32 (PowerPC), cũng như loongarch64. Tuy nhiên, bạn phải tự biên dịch editor cho nền tảng đó (cũng như các export template); hiện chưa có bản tải xuống chính thức. Có thể tìm thấy hướng dẫn biên dịch RISC-V trên trang :ref:`doc_compiling_for_linuxbsd`.

**Chạy các project đã export:**

- iOS.

Godot hướng đến việc độc lập với nền tảng nhiều nhất có thể và có thể được
:ref:`port sang các nền tảng mới <doc_custom_platform_ports>` tương đối dễ dàng.

.. note::

    Các project được viết bằng C# sử dụng Godot 4 hiện không thể export sang nền tảng web. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3. Hỗ trợ nền tảng Android và iOS có từ Godot 4.2, nhưng đang ở trạng thái thử nghiệm và :ref:`có một số hạn chế <doc_c_sharp_platforms>`.

Editor
------

**Tính năng:**

- Trình chỉnh sửa scene tree.
- Trình chỉnh sửa script tích hợp sẵn. Đồng thời hỗ trợ chỉnh sửa các tệp văn bản và sử dụng syntax highlighter tùy chỉnh.
- Hỗ trợ :ref:`external script editor <doc_external_editor>` như Visual Studio Code hoặc Vim.
- :ref:`debugger <doc_debugger_panel>` GDScript.

   - Hỗ trợ debug trong các thread.

- Visual profiler hiển thị thời gian CPU và GPU cho từng bước của rendering pipeline.
- Các công cụ theo dõi hiệu năng, bao gồm
  :ref:`custom performance monitor <doc_custom_performance_monitors>`.
- Hỗ trợ :ref:`tracing profiler <doc_tracing_profilers>` như
  :ref:`doc_profiler_tracy` và :ref:`doc_profiler_perfetto` cho các tác vụ tối ưu hóa chuyên sâu hơn.
- Mọi script đều có thể được :ref:`chạy trong editor <doc_running_code_in_the_editor>` và cung cấp các chức năng tùy chỉnh như các nút có thể nhấp trong inspector mà không cần tạo editor plugin.
- Tải lại script trực tiếp.
- Chỉnh sửa scene trực tiếp.

   - Các thay đổi *sẽ* được phản ánh trong editor và *sẽ* được giữ lại sau khi đóng project đang chạy.

- Đồng bộ camera trực tiếp (mặc định bị tắt).

   - Di chuyển camera trong editor và xem kết quả trong project đang chạy.

- Remote inspector.

   - Các thay đổi *sẽ không* được phản ánh trong editor và *sẽ không* được giữ lại sau khi đóng project đang chạy.

- Chạy đồng thời nhiều instance project từ một instance editor duy nhất (hữu ích khi kiểm thử client/server).
- Tùy chọn :ref:`nhúng game <doc_game_embedding>` để chạy project trong một panel bên trong editor.

  - Chọn các node 2D và 3D trong viewport của project để kiểm tra chúng trong editor.
  - Di chuyển camera trong project bằng các tùy chọn ghi đè camera 2D và 3D.
  - Hỗ trợ điều chỉnh time scale, tạm dừng và tiến từng frame.
  - Hỗ trợ tắt tiếng project.

- Công cụ thước để đo khoảng cách trong 2D và 3D.
- Hỗ trợ bắt dính vertex trong 3D.
- Hỗ trợ theo dõi lựa chọn khi nó di chuyển trong 3D bằng cách sử dụng Focus Selection hai lần.
- Tài liệu tham khảo class ngoại tuyến tích hợp sẵn.
- Sử dụng editor bằng hàng chục ngôn ngữ do cộng đồng đóng góp.

**Plugin:**

- Có thể tải editor plugin từ
  :ref:`Asset Store <doc_what_is_asset_store>` để mở rộng chức năng của editor.
- :ref:`Tạo plugin của riêng bạn <doc_making_plugins>` bằng GDScript để thêm tính năng mới hoặc tăng tốc quy trình làm việc.
- :ref:`Tải project từ Asset Store <doc_using_asset_store_editor>` trong Project Manager và import trực tiếp.

Rendering
---------

Godot 4 bao gồm ba renderer:

- **Forward+**. Renderer tiên tiến nhất, chỉ phù hợp với các nền tảng desktop. Được sử dụng mặc định trên các nền tảng desktop. Renderer này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm rendering driver và sử dụng backend **RenderingDevice**.
- **Mobile**. Có ít tính năng hơn nhưng render các scene đơn giản nhanh hơn. Phù hợp với các nền tảng mobile và desktop. Được sử dụng mặc định trên các nền tảng mobile. Renderer này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm rendering driver và sử dụng backend **RenderingDevice**.
- **Compatibility**, đôi khi được gọi là **GL Compatibility**. Renderer ít tiên tiến nhất, phù hợp với các nền tảng desktop và mobile cấp thấp. Được sử dụng mặc định trên nền tảng web. Renderer này sử dụng **OpenGL** làm rendering driver.

.. seealso::

    Xem :ref:`doc_renderers` để biết phần so sánh chi tiết giữa các phương pháp rendering.

Đồ họa 2D
---------

- Rendering sprite, polygon và đường thẳng.

   - Các công cụ cấp cao để vẽ đường thẳng và polygon như
     :ref:`class_Polygon2D` và :ref:`class_Line2D`, với hỗ trợ texturing.

- :ref:`class_AnimatedSprite2D` làm công cụ hỗ trợ tạo sprite động.
- Các lớp parallax.

   - Hỗ trợ pseudo-3D, bao gồm xem trước trong editor.

- :ref:`Chiếu sáng 2D <doc_2d_lights_and_shadows>` với normal map và specular map.

   - Đèn 2D dạng điểm (omni/spot) và định hướng.
   - Bóng cứng hoặc mềm (có thể điều chỉnh riêng cho từng đèn).
   - Các shader tùy chỉnh có thể truy cập biểu diễn :abbr:`SDF (Signed Distance Field)` theo thời gian thực của cảnh 2D, dựa trên các node :ref:`class_LightOccluder2D`, có thể dùng để cải thiện hiệu ứng chiếu sáng 2D, bao gồm global illumination 2D.

- :ref:`Rendering font <doc_gui_using_fonts>` bằng bitmap, rasterization sử dụng FreeType hoặc signed distance field đa kênh (MSDF).

   - Có thể export font bitmap bằng các công cụ như BMFont hoặc import từ hình ảnh (chỉ dành cho font có độ rộng cố định).
   - Font động hỗ trợ font đơn sắc cũng như font màu (ví dụ: emoji). Các định dạng được hỗ trợ là TTF, OTF, WOFF1 và WOFF2.
   - Font động hỗ trợ outline font tùy chọn với độ rộng và màu sắc có thể điều chỉnh.
   - Font động hỗ trợ variable font và các tính năng OpenType, bao gồm ligature.
   - Font động hỗ trợ mô phỏng chữ đậm và chữ nghiêng khi file font không có các kiểu này.
   - Font động hỗ trợ oversampling để giữ cho font sắc nét hơn ở độ phân giải cao.
   - Font động hỗ trợ định vị subpixel để làm font rõ nét hơn ở kích thước nhỏ.
   - Font động hỗ trợ tối ưu hóa subpixel LCD để làm font rõ nét hơn nữa ở kích thước nhỏ.
   - Font signed distance field có thể được scale ở mọi độ phân giải mà không cần rasterization lại. Việc sử dụng đa kênh giúp font SDF scale xuống các kích thước nhỏ tốt hơn so với font SDF đơn sắc.

- :ref:`Oversampling <doc_multiple_resolutions_font_and_image_oversampling>` cho hình ảnh SVG bằng :ref:`class_DPITexture` import type. Điều này cho kết quả sắc nét hơn khi scale texture lên bằng cách rasterization lại hình ảnh nguồn SVG thành độ phân giải mới trong lúc runtime.

  - Oversampling có thể tùy chọn tính đến các :ref:`class_CanvasItem` scale riêng lẻ để rendering sắc nét hơn khi scale node.

- :ref:`particle <doc_particle_systems_2d>` dựa trên GPU với hỗ trợ
  :ref:`shader particle tùy chỉnh <doc_particle_shader>`.
- Particle dựa trên CPU.
- Tùy chọn :ref:`rendering HDR 2D <doc_environment_and_post_processing_using_glow_in_2d>` để cải thiện khả năng tạo glow.
- Tùy chọn debanding để giảm hiện tượng banding trong gradient.
- :ref:`Đầu ra HDR <doc_hdr_output>` trên các platform và renderer được hỗ trợ.

Công cụ 2D
----------

- :ref:`TileMap <doc_using_tilemaps>` để thiết kế level 2D dựa trên tile.
- Camera 2D với tính năng smoothing và drag margin tích hợp sẵn.
- Node Path2D để biểu diễn một đường dẫn trong không gian 2D.

   - Có thể vẽ trong editor hoặc tạo bằng phương pháp procedural.
   - Node PathFollow2D để khiến các node đi theo một Path2D.

- :ref:`class hỗ trợ hình học 2D <class_Geometry2D>`.

Vật lý 2D
---------

**Physics body:**

- Body tĩnh.
- Body có thể animation (dành cho các đối tượng chỉ di chuyển bằng script hoặc animation, chẳng hạn như cửa và platform).
- Rigid body.
- Character body.
- Joint.
- Area để phát hiện các body đi vào hoặc rời khỏi area đó.
- :ref:`Nội suy vật lý <doc_physics_interpolation>`.

**Phát hiện va chạm:**

- Các shape tích hợp sẵn: đường thẳng, hình hộp, hình tròn, capsule, biên thế giới (mặt phẳng vô hạn).
- Polygon va chạm (có thể vẽ thủ công hoặc tạo từ sprite trong editor).

Đồ họa 3D
---------

- Tính toán chiếu sáng nội bộ HDR tuyến tính.
- Tùy chọn debanding để giảm hiện tượng banding trong gradient.
- :ref:`Đầu ra HDR <doc_hdr_output>` trên các platform và renderer được hỗ trợ.
- Camera phối cảnh, trực giao và có frustum offset.
- Khi sử dụng renderer Forward+, depth prepass được dùng để cải thiện hiệu năng trong các cảnh phức tạp bằng cách giảm chi phí overdraw.
- :ref:`doc_variable_rate_shading` trên các GPU được hỗ trợ trong Forward+ và Mobile.

**Rendering dựa trên vật lý (các tính năng material tích hợp sẵn):**

- Tuân theo model PBR của Disney.
- Hỗ trợ các chế độ diffuse shading Burley, Lambert, Lambert Wrap (half-Lambert) và Toon.
- Hỗ trợ các chế độ specular shading Schlick-GGX, Toon và Disabled.
- Sử dụng quy trình roughness-metallic với hỗ trợ texture ORM.
- Sử dụng horizon specular occlusion (model Filament) để cải thiện diện mạo material.
- Normal mapping.
- Parallax/relief mapping với level of detail tự động dựa trên khoảng cách.
- Detail mapping cho albedo map và normal map.
- Subsurface scattering và transmittance.
- Refraction trong screen-space với hỗ trợ roughness của material (tạo ra refraction mờ).
- Fade theo độ gần (particle mềm) và fade theo khoảng cách.
- Fade theo khoảng cách có thể sử dụng alpha blending hoặc dithering để tránh đi qua transparent pipeline.
- Dithering có thể được xác định theo từng pixel hoặc từng object.

**Chiếu sáng theo thời gian thực:**

- :ref:`Đèn định hướng <doc_lights_and_shadows_directional_light>` (mặt trời/mặt trăng).
- :ref:`Đèn đa hướng <doc_lights_and_shadows_omni_light>`.
- :ref:`Đèn spotlight <doc_lights_and_shadows_spot_light>` với góc hình nón và độ suy giảm có thể điều chỉnh.
- :ref:`Đèn vùng hình chữ nhật <doc_lights_and_shadows_area_light>` với texture tùy chọn để xác định hình dạng và màu sắc.
- Có thể điều chỉnh năng lượng của ánh sáng phản xạ, ánh sáng gián tiếp và sương mù thể tích cho từng đèn.
- Có thể điều chỉnh "kích thước" đèn cho đèn omni hình cầu và đèn spotlight dạng đĩa (đồng thời làm bóng đổ mờ hơn với vùng nửa tối biến thiên).
- Hệ thống làm mờ theo khoảng cách tùy chọn để làm mờ các đèn ở xa và bóng đổ của chúng, giúp cải thiện hiệu năng.
- Khi sử dụng renderer Forward+ (mặc định trên máy tính), các đèn được render với các tối ưu hóa clustered forward để giảm chi phí riêng lẻ. Clustered rendering cũng loại bỏ mọi giới hạn về số lượng đèn có thể sử dụng trên một mesh.
- Khi sử dụng renderer Mobile, tối đa 8 đèn omni, 8 đèn spotlight và 8 đèn vùng có thể được hiển thị trên mỗi tài nguyên mesh. Có thể sử dụng baked lighting để vượt qua giới hạn này nếu cần.

**Lập bản đồ bóng đổ:**

- *DirectionalLight3D:* Trực giao (nhanh nhất), PSSM chia 2 phần và chia 4 phần. Hỗ trợ chuyển tiếp giữa các phần.
- *OmniLight3D:* Paraboloid kép (nhanh) hoặc cubemap (chậm hơn nhưng chính xác hơn). Hỗ trợ texture máy chiếu có màu dưới dạng panorama.
- *SpotLight3D:* Texture đơn. Hỗ trợ texture máy chiếu có màu.
- *AreaLight3D:* Texture đơn với biến dạng paraboloid kép để xấp xỉ hình dạng của đèn.
- Độ lệch chuẩn của pháp tuyến bóng đổ và kỹ thuật shadow pancaking để giảm hiện tượng bóng đổ bị lốm đốm và bóng đổ bị tách khỏi vật thể.
- Độ mờ bóng đổ tương tự :abbr:`PCSS (Percentage Closer Soft Shadows)` dựa trên kích thước đèn và khoảng cách từ bề mặt mà bóng đổ lên. Được hỗ trợ cho tất cả loại đèn.
- Có thể điều chỉnh độ mờ bóng đổ cho từng đèn.

**Global illumination với ánh sáng gián tiếp:**

- :ref:`Lightmap baked <doc_using_lightmap_gi>` (nhanh nhưng không thể cập nhật trong runtime).

   - Hỗ trợ bake chỉ ánh sáng gián tiếp hoặc bake cả ánh sáng trực tiếp và gián tiếp. Có thể điều chỉnh chế độ bake cho từng đèn để cho phép thiết lập bake ánh sáng lai.
   - Hỗ trợ chiếu sáng các đối tượng động bằng probe tự động và probe được đặt thủ công.
   - Tùy chọn hỗ trợ chiếu sáng định hướng dựa trên spherical harmonics.
   - Tùy chọn hỗ trợ bake shadowmask cho bóng đổ định hướng tĩnh ở xa.
   - Tùy chọn supersampling tại thời điểm bake để cải thiện chất lượng và giảm hiện tượng rò rỉ ánh sáng, với cái giá là thời gian bake lâu hơn và mức sử dụng bộ nhớ cao hơn trong quá trình bake.
   - Lightmap được bake trên GPU bằng compute shader (nhanh hơn nhiều so với lightmap trên CPU). Chỉ có thể thực hiện bake từ editor, không phải trong các project đã export.
   - Hỗ trợ :ref:`khử nhiễu <doc_using_lightmap_gi_denoising>` dựa trên GPU với JNLM ngay khi cài đặt, hoặc khử nhiễu dựa trên CPU/GPU có chất lượng cao hơn với OIDN (cần tải OIDN riêng).
   - Lightmap được render bằng bộ lọc bicubic để giảm các sai lệch do scaling.

- :ref:`Probe GI dựa trên voxel <doc_using_voxel_gi>`. Hỗ trợ đèn động *và* vật cản động, đồng thời hỗ trợ phản xạ. Cần một bước bake nhanh có thể thực hiện trong editor hoặc tại runtime (bao gồm cả từ project đã export).
- :ref:`GI bằng trường khoảng cách có dấu <doc_using_sdfgi>` được thiết kế cho các thế giới mở rộng lớn. Hỗ trợ đèn động nhưng không hỗ trợ vật cản động. Hỗ trợ phản xạ. Không cần bake.
- :ref:`Chiếu sáng gián tiếp trong không gian màn hình (SSIL) <doc_environment_and_post_processing_ssil>` ở độ phân giải một nửa hoặc đầy đủ. Hoàn toàn theo thời gian thực và hỗ trợ mọi loại nguồn sáng phát xạ (bao gồm decal).
- VoxelGI và SDFGI sử dụng một deferred pass để cho phép render GI ở độ phân giải một nửa nhằm cải thiện hiệu năng (đồng thời vẫn hỗ trợ MSAA đầy đủ chức năng).

**Phản xạ:**

- Phản xạ dựa trên voxel (khi sử dụng probe GI) và phản xạ dựa trên SDF (khi sử dụng GI bằng trường khoảng cách có dấu). Phản xạ dựa trên voxel hiển thị trên các bề mặt trong suốt, trong khi phản xạ dựa trên SDF thô cũng hiển thị trên các bề mặt trong suốt.
- Phản xạ baked nhanh hoặc phản xạ theo thời gian thực chậm bằng ReflectionProbe. Tùy chọn có thể bật hiệu chỉnh hộp parallax.
- Phản xạ trong không gian màn hình với hỗ trợ roughness của material.
- Có thể kết hợp các kỹ thuật phản xạ để đạt độ chính xác hoặc khả năng mở rộng cao hơn.
- Khi sử dụng renderer Forward+ (mặc định trên máy tính), các probe phản xạ được render với các tối ưu hóa clustered forward để giảm chi phí riêng lẻ. Clustered rendering cũng loại bỏ mọi giới hạn về số lượng probe phản xạ có thể sử dụng trên một mesh.
- Khi sử dụng renderer Mobile, tối đa 8 probe phản xạ có thể được hiển thị trên mỗi mesh
  resource. Khi sử dụng renderer Compatibility, tối đa 2 probe phản xạ có thể
  được hiển thị trên mỗi tài nguyên mesh.

**Decal:**

- :ref:`Hỗ trợ albedo <doc_using_decals>`, emissive, :abbr:`ORM (Occlusion Roughness Metallic)`, và normal mapping.
- Các kênh texture được phủ mượt lên trên material bên dưới, với hỗ trợ decal chỉ có normal/ORM.
- Hỗ trợ làm mờ normal để làm mờ decal tùy theo góc tới của nó.
- Không phụ thuộc vào việc tạo mesh tại runtime. Điều này có nghĩa là decal có thể được sử dụng trên các mesh skinned phức tạp mà không bị phạt hiệu năng, ngay cả khi decal di chuyển ở mỗi frame.
- Hỗ trợ lọc texture nearest, bilinear, trilinear hoặc anisotropic (được cấu hình trên toàn cục).
- Hệ thống làm mờ theo khoảng cách tùy chọn để làm mờ các decal ở xa, giúp cải thiện hiệu năng.
- Khi sử dụng renderer Forward+ (mặc định trên máy tính), các decal được render với các tối ưu hóa clustered forward để giảm chi phí riêng lẻ. Clustered rendering cũng loại bỏ mọi giới hạn về số lượng decal có thể sử dụng trên một mesh.
- Khi sử dụng renderer Mobile, tối đa 8 decal có thể được hiển thị trên mỗi tài nguyên mesh.

**Bầu trời:**

- Bầu trời panorama (sử dụng HDRI).
- Sky dạng procedural và sky dựa trên vật lý phản hồi theo các DirectionalLights trong cảnh.
- Hỗ trợ :ref:`custom sky shaders <doc_sky_shader>`, có thể được animation.
- Bản đồ radiance được dùng cho ánh sáng ambient và specular có thể được cập nhật theo thời gian thực tùy thuộc vào các thiết lập chất lượng đã chọn.

**Fog:**

- Fog độ sâu theo hàm mũ.
- Fog độ cao theo hàm mũ.
- Hỗ trợ tự động xác định màu fog dựa trên màu sky (aerial perspective).
- Hỗ trợ tán xạ ánh nắng trong fog.
- Hỗ trợ kiểm soát mức độ ảnh hưởng của việc render fog lên sky, với các tùy chọn điều khiển riêng cho fog truyền thống và fog thể tích.
- Hỗ trợ để các material cụ thể bỏ qua fog.

**Volumetric fog:**

- :ref:`volumetric fog <doc_volumetric_fog>` toàn cục phản ứng với ánh sáng và bóng đổ.
- Volumetric fog có thể tính đến ánh sáng gián tiếp khi sử dụng VoxelGI hoặc SDFGI.
- Các node fog volume có thể được đặt vào để thêm fog cho những khu vực cụ thể (hoặc loại bỏ fog khỏi những khu vực cụ thể). Các hình dạng được hỗ trợ gồm box, ellipse, cone, cylinder và density map dựa trên texture 3D.
- Mỗi fog volume có thể có shader tùy chỉnh riêng.
- Có thể được sử dụng cùng với fog truyền thống.

**Particles:**

- Particles dựa trên GPU với hỗ trợ cho subemitters (2D + 3D), trails (2D + 3D), attractors (chỉ 3D) và collision (2D + 3D).

  - Các hình dạng attractor cho particle 3D được hỗ trợ: box, sphere và vector field 3D.
  - Các hình dạng collision cho particle 3D được hỗ trợ: box, sphere, signed distance field đã bake và heightmap theo thời gian thực (phù hợp với hiệu ứng thời tiết trong open world).
  - Collision của particle 2D được xử lý bằng signed distance field được tạo theo thời gian thực dựa trên các node :ref:`class_LightOccluder2D` trong cảnh.
  - Trails có thể sử dụng các mesh ribbon trail và tube trail tích hợp sẵn, hoặc các mesh tùy chỉnh có skeleton.
  - Hỗ trợ custom particle shaders với emission thủ công.

- Particles dựa trên CPU.

**Post-processing:**

- Tonemapping (Linear, Reinhard, Filmic, ACES, AgX).
- Tự động điều chỉnh exposure dựa trên độ sáng của viewport (và ghi đè exposure thủ công).
- Depth of field gần và xa với mô phỏng bokeh có thể điều chỉnh (box, hexagon, circle).
- Screen-space ambient occlusion (SSAO) ở độ phân giải một nửa hoặc đầy đủ.
- Glow/bloom với tùy chọn upscaling bicubic và nhiều blend mode: Screen, Soft Light, Add, Replace, Mix.
- Glow có thể sử dụng texture dirt map có màu, hoạt động như hiệu ứng lens dirt.
- Glow có thể được :ref:`dùng như hiệu ứng làm mờ trong screen-space <doc_environment_and_post_processing_using_glow_to_blur_the_screen>`.
- Hiệu chỉnh màu bằng ramp một chiều hoặc texture 3D LUT.
- Bộ giới hạn roughness để giảm ảnh hưởng của specular aliasing.
- Điều chỉnh độ sáng, độ tương phản và độ bão hòa.

**Texture filtering:**

- Filtering nearest, bilinear, trilinear hoặc anisotropic.
- Các tùy chọn filtering được xác định theo từng lần sử dụng, không phải theo từng texture.

**Texture VRAM compression:**

- BPTC (dùng để compression chất lượng cao, nhắm đến các nền tảng desktop).
- ASTC (dùng để compression chất lượng cao, nhắm đến các nền tảng mobile).
- ETC2 (dùng để compression nhanh, nhắm đến các nền tảng mobile).
- S3TC (dùng để compression nhanh, nhắm đến các nền tảng desktop).
- Basis Universal (chậm, nhưng chỉ yêu cầu một lần encoding cho mọi nền tảng).

**Antialiasing:**

- :ref:`antialiasing <doc_3d_antialiasing>` theo thời gian (TAA).
- :ref:`antialiasing <doc_3d_antialiasing>` AMD FidelityFX Super Resolution 2.2 (FSR2), có thể được sử dụng ở độ phân giải gốc như một dạng antialiasing theo thời gian chất lượng cao.
- Multi-sample antialiasing (MSAA), cho cả :ref:`doc_2d_antialiasing` và :ref:`doc_3d_antialiasing`.
- Fast approximate antialiasing (FXAA).
- Super-sample antialiasing (SSAA) sử dụng scaling 3D bilinear và scale độ phân giải 3D lớn hơn 1.0.
- Antialiasing alpha, alpha to coverage của MSAA và alpha hashing theo từng material.

**Resolution scaling:**

- Hỗ trợ :ref:`render 3D ở độ phân giải thấp hơn <doc_resolution_scaling>` trong khi vẫn giữ rendering 2D ở scale ban đầu. Có thể sử dụng tính năng này để cải thiện hiệu năng trên các hệ thống cấp thấp hoặc cải thiện hình ảnh trên các hệ thống cao cấp.
- Resolution scaling sử dụng filtering nearest-neighbor, filtering bilinear, AMD FidelityFX Super Resolution 1.0 (FSR1) hoặc AMD FidelityFX Super Resolution 2.2.1 (FSR2).
- LOD bias của texture mipmap được tự động điều chỉnh để cải thiện chất lượng ở các scale độ phân giải thấp hơn. Bias này cũng có thể được thay đổi bằng offset thủ công.

Hầu hết các hiệu ứng được liệt kê ở trên có thể được điều chỉnh để đạt hiệu năng tốt hơn hoặc cải thiện thêm chất lượng. Điều này có thể hữu ích khi
:ref:`sử dụng Godot để render offline <doc_creating_movies>`.

Công cụ 3D
----------

- Mesh tích hợp sẵn: cube, cylinder/cone, (hemi)sphere, prism, plane, quad, torus, ribbon, tube.
- :ref:`GridMaps <doc_using_gridmaps>` để thiết kế level 3D dựa trên tile.
- :ref:`Constructive solid geometry <doc_csg_tools>` (dùng cho prototyping).
- Các công cụ để :ref:`tạo geometry procedural <doc_procedural_geometry>`.
- Node Path3D để biểu diễn một path trong không gian 3D.

   - Có thể được vẽ trong editor hoặc tạo bằng procedural.
   - Node PathFollow3D để khiến các node đi theo một Path3D.

- :ref:`Lớp trợ giúp hình học 3D <class_Geometry3D>`.
- Hỗ trợ xuất scene hiện tại dưới dạng tệp glTF 2.0, cả từ editor lẫn trong runtime từ project đã xuất.

Vật lý 3D
---------

**Các body vật lý:**

- Các body tĩnh.
- Các body có thể hoạt ảnh (dành cho các đối tượng chỉ di chuyển bằng script hoặc animation, chẳng hạn như cửa và platform).
- Các rigid body.
- Các character body.
- Các vehicle body (dành cho vật lý kiểu arcade, không dành cho mô phỏng).
- Các joint.
- :ref:`Các soft body <doc_soft_body>`.
- :ref:`Ragdoll <doc_ragdoll_system>`.
- Các area để phát hiện body đi vào hoặc rời khỏi chúng.
- :ref:`Nội suy vật lý <doc_physics_interpolation>`.

**Phát hiện va chạm:**

- Các shape tích hợp: hình hộp, hình cầu, capsule, hình trụ, ranh giới thế giới (mặt phẳng vô hạn).
- Tạo các shape va chạm tam giác cho mọi mesh từ editor.
- Tạo một hoặc nhiều shape va chạm lồi cho mọi mesh từ editor.

Shader
------

- *2D:* Shader vertex, fragment và light tùy chỉnh.
- *3D:* Shader vertex, fragment, light, sky và fog tùy chỉnh.
- Shader tùy chỉnh có thể tạo và sửa đổi texture theo thủ tục trong thời gian thực bằng
  :ref:`class_DrawableTexture2D`.
- Shader dựa trên văn bản sử dụng :ref:`ngôn ngữ shader lấy cảm hứng từ GLSL <doc_shading_language>`.
- GitHub cung cấp tính năng tô sáng cú pháp bằng cách sử dụng ``gdshader`` làm tên ngôn ngữ trong một khối mã Markdown.
- Trình chỉnh sửa shader trực quan.

   - Hỗ trợ :ref:`plugin shader trực quan <doc_visual_shader_plugins>`.

Scripting
---------

**Tổng quan:**

- Mẫu thiết kế hướng đối tượng với các script mở rộng node.
- Signal và group để giao tiếp giữa các script.
- Hỗ trợ :ref:`scripting đa ngôn ngữ <doc_cross_language_scripting>`.
- Nhiều kiểu dữ liệu đại số tuyến tính 2D, 3D và 4D như vector và transform.

:ref:`GDScript: <doc_gdscript>`

- :ref:`Ngôn ngữ thông dịch cấp cao <doc_gdscript_reference>` với
  :ref:`kiểu tĩnh tùy chọn <doc_gdscript_static_typing>`.
- Cú pháp lấy cảm hứng từ Python. Tuy nhiên, GDScript **không** dựa trên Python.
- GitHub cung cấp tính năng tô sáng cú pháp bằng cách sử dụng ``gdscript`` làm tên ngôn ngữ trong một khối mã Markdown.
- :ref:`Sử dụng thread <doc_using_multiple_threads>` để thực hiện các tác vụ bất đồng bộ hoặc tận dụng nhiều lõi xử lý.

:ref:`C#: <doc_c_sharp>`

- Được đóng gói trong một binary riêng để giảm kích thước tệp và dependency.
- Hỗ trợ .NET 8 trở lên.

   - Hỗ trợ đầy đủ cú pháp và tính năng của C# 12.0.

- Hỗ trợ Windows, Linux và macOS. Kể từ Godot 4.2, Android và iOS cũng được hỗ trợ thử nghiệm.

   - Trên nền tảng iOS, chỉ một số architecture được hỗ trợ: ``arm64``.
   - Nền tảng web hiện chưa được hỗ trợ. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3.

- Nên sử dụng editor bên ngoài để tận dụng các chức năng IDE.

**GDExtension (C, C++, Rust, D, ...):**

- Khi cần, hãy liên kết với các thư viện native để đạt hiệu năng cao hơn và tích hợp với bên thứ ba.

   - Để viết game logic, nên dùng GDScript hoặc C# nếu hiệu năng của chúng phù hợp.

- Các binding GDExtension chính thức cho `C <https://github.com/godotengine/godot-headers>`__ và `C++ <https://github.com/godotengine/godot-cpp>`__.

   - Sử dụng bất kỳ build system và tính năng ngôn ngữ nào bạn muốn.

- Các binding GDExtension cho `D <https://github.com/godot-dlang/godot-dlang>`__, `Swift <https://github.com/migueldeicaza/SwiftGodot>`__ và `Rust <https://github.com/godot-rust/gdextension>`__ đang được cộng đồng tích cực phát triển. (Một số binding trong đó có thể đang thử nghiệm và chưa sẵn sàng cho production).

Âm thanh
--------

**Tính năng:**

- Đầu ra mono, stereo, 5.1 và 7.1.
- Phát âm thanh không định vị và có định vị trong 2D và 3D.

   - Hiệu ứng Doppler tùy chọn trong 2D và 3D.

- Hỗ trợ :ref:`bus âm thanh <doc_audio_buses>` có thể định tuyến lại và các effect, bao gồm hàng chục effect.
- Hỗ trợ polyphony (phát nhiều âm thanh từ một :ref:`class_AudioStreamPlayer` node).
- Hỗ trợ volume và pitch ngẫu nhiên.
- Hỗ trợ điều chỉnh pitch theo thời gian thực.
- Hỗ trợ chọn sample tuần tự/ngẫu nhiên, bao gồm ngăn lặp lại khi chọn sample ngẫu nhiên.
- :ref:`class_AudioListener2D` và :ref:`class_AudioListener3D` node để lắng nghe từ một vị trí khác với camera.
- Hỗ trợ :ref:`tạo âm thanh theo thủ tục <class_AudioStreamGenerator>`.
- Đầu vào âm thanh để ghi âm từ microphone.
- :ref:`Chuyển văn bản thành giọng nói <doc_text_to_speech>` bằng các engine TTS do nền tảng cung cấp.
- Đầu vào MIDI.

   - Hiện chưa hỗ trợ đầu ra MIDI.

**API được sử dụng:**

- *Windows:* WASAPI.
- *macOS:* CoreAudio.
- *Linux:* PulseAudio hoặc ALSA.

Import
------

- Hỗ trợ :ref:`plugin import tùy chỉnh <doc_import_plugins>`.

**Định dạng:**

- *Hình ảnh:* Xem :ref:`doc_importing_images`.
- *Âm thanh:*

   - WAV với tùy chọn nén :abbr:`QOA (Quite OK Audio)` hoặc IMA-ADPCM.
   - Ogg Vorbis.
   - MP3.

- *Cảnh 3D:* Xem :ref:`doc_importing_3d_scenes`.

   - glTF 2.0 *(khuyến nghị)*.
   - ``.blend`` (bằng cách gọi ẩn chức năng xuất glTF của Blender).
   - FBX (bằng cách gọi ẩn `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__).
   - Collada (.dae).
   - Wavefront OBJ (chỉ dành cho cảnh tĩnh, có thể được tải trực tiếp dưới dạng mesh hoặc được nhập dưới dạng cảnh 3D).

- Hỗ trợ tải cảnh glTF 2.0 tại runtime, bao gồm cả từ project đã xuất.
- Mesh 3D sử dụng `Mikktspace <http://www.mikktspace.com/>`__ để tạo tangent khi import, bảo đảm tính nhất quán với các ứng dụng 3D khác như Blender.

Đầu vào
-------

- :ref:`Hệ thống ánh xạ đầu vào <doc_input_examples>` sử dụng các sự kiện đầu vào được hardcode hoặc các input action có thể ánh xạ lại.

   - Các giá trị trục có thể được ánh xạ tới hai action khác nhau với deadzone có thể cấu hình.
   - Sử dụng cùng một đoạn code để hỗ trợ cả bàn phím và gamepad.

- Đầu vào từ bàn phím.

   - Các phím có thể được ánh xạ ở chế độ "physical" để không phụ thuộc vào bố cục bàn phím.

- Đầu vào từ chuột.

   - Con trỏ chuột có thể hiển thị, ẩn, bị bắt hoặc bị giới hạn trong cửa sổ.
   - Có thể thay đổi giao diện con trỏ chuột thành hình ảnh tùy chỉnh hoặc một trong các con trỏ hệ thống.
   - Khi bị bắt, đầu vào thô được sử dụng trên Windows và Linux để bỏ qua các thiết lập tăng tốc chuột của hệ điều hành.

- :ref:`Đầu vào từ gamepad <doc_controllers_gamepads_joysticks>` (tối đa 8 bộ điều khiển đồng thời).

  - Hỗ trợ :ref:`thay đổi màu LED <doc_controller_features_led_color>` trên các bộ điều khiển được hỗ trợ.
  - Hỗ trợ :ref:`đọc cảm biến chuyển động <doc_controller_features_motion_sensors>` trên các bộ điều khiển được hỗ trợ (dùng để triển khai ngắm bằng gyro).

- Đầu vào từ bút/tablet với hỗ trợ áp lực và độ nghiêng.

Điều hướng
----------

- Thuật toán A* trong :ref:`2D <class_AStar2D>` và :ref:`3D <class_AStar3D>`.
- Mesh điều hướng với tính năng tránh chướng ngại vật động trong
  :ref:`2D <doc_navigation_overview_2d>` và :ref:`3D <doc_navigation_overview_3d>`.
- Tạo mesh điều hướng từ editor hoặc tại runtime (bao gồm cả từ project đã xuất).

Networking
----------

- Networking TCP cấp thấp sử dụng :ref:`class_StreamPeer` và :ref:`class_TCPServer`.
- Networking UDP cấp thấp sử dụng :ref:`class_PacketPeer` và :ref:`class_UDPServer`.
- Yêu cầu HTTP cấp thấp sử dụng :ref:`class_HTTPClient`.
- Yêu cầu HTTP cấp cao sử dụng :ref:`class_HTTPRequest`.

   - Hỗ trợ HTTPS ngay khi cài đặt bằng cách sử dụng các certificate đi kèm.

- API :ref:`multiplayer cấp cao <doc_high_level_multiplayer>` sử dụng UDP và ENet.

   - Tự động replication bằng remote procedure call (RPC).
   - Hỗ trợ truyền không tin cậy, tin cậy và có thứ tự.

- Client và server :ref:`WebSocket <doc_websocket>`, khả dụng trên mọi nền tảng.
- Client và server :ref:`WebRTC <doc_webrtc>`, khả dụng trên mọi nền tảng.
- Hỗ trợ :ref:`UPnP <class_UPNP>` để bỏ qua yêu cầu chuyển tiếp port khi host server phía sau NAT.

Quốc tế hóa
-----------

- Hỗ trợ đầy đủ Unicode, bao gồm emoji.
- Hỗ trợ tải system font trên Windows, macOS và Linux.

  - Theo mặc định, system font được sử dụng làm phương án dự phòng để hiển thị các ký tự không được hỗ trợ
    characters. Điều này cho phép hiển thị chính xác văn bản đa ngôn ngữ mà không
    phải đóng gói các tệp font lớn cùng với project.

- Lưu trữ chuỗi bản địa hóa bằng :ref:`CSV <doc_internationalizing_games>` hoặc :ref:`gettext <doc_localization_using_gettext>`.

  - Hỗ trợ tạo tệp gettext POT và PO từ editor.

- Tự động sử dụng các chuỗi đã bản địa hóa trong project ở các phần tử GUI hoặc bằng cách sử dụng hàm ``tr()``.
- Hỗ trợ số nhiều hóa và ngữ cảnh dịch.
- Hỗ trợ :ref:`dàn chữ hai chiều <doc_internationalizing_games_bidi>`, định hình văn bản và các dạng bản địa hóa OpenType.
- Tự động phản chiếu UI cho các locale từ phải sang trái.
- Hỗ trợ :ref:`pseudolocalization <doc_pseudolocalization>` để kiểm tra mức độ thân thiện với i18n của project.

Quản lý cửa sổ và tích hợp hệ điều hành
---------------------------------------

- Tạo nhiều cửa sổ độc lập trong một process.
- Di chuyển, thay đổi kích thước, thu nhỏ và phóng to các cửa sổ do project tạo ra.
- Thay đổi tiêu đề và biểu tượng cửa sổ.
- Tạo các cửa sổ trong suốt để dùng làm lớp phủ, với hỗ trợ cho phép chuột đi qua dựa trên polygon.
- Yêu cầu chú ý (sẽ khiến thanh tiêu đề nhấp nháy trên hầu hết nền tảng).
- Chế độ toàn màn hình (không viền và độc quyền).
- Cửa sổ không viền (toàn màn hình hoặc không toàn màn hình).
- Giữ cửa sổ luôn ở trên cùng.
- Khiến cửa sổ bỏ qua focus (hữu ích cho lớp phủ).
- Khai báo cửa sổ là popup (ẩn khỏi trình chuyển tác vụ) hoặc exclusive (ngăn tương tác với các cửa sổ khác trong cùng process).
- Hỗ trợ hộp thoại tệp native trên Windows, macOS, Linux và Android.
- Hỗ trợ biểu tượng khay hệ thống trên Windows và macOS.
- Tích hợp menu toàn cục trên macOS.
- Trang trí phía client trên macOS.
- Thực thi các lệnh theo cách blocking hoặc non-blocking (bao gồm chạy nhiều instance của cùng một project).
- Mở đường dẫn tệp và URL bằng trình xử lý giao thức mặc định hoặc tùy chỉnh (nếu đã được đăng ký trên hệ thống).
- Phân tích các đối số dòng lệnh tùy chỉnh.
- Hỗ trợ trình đọc màn hình trên Windows, macOS và Linux.
- Bất kỳ binary Godot nào (editor hoặc project đã export) đều có thể được
  :ref:`sử dụng làm server headless <doc_exporting_for_dedicated_servers>` bằng cách khởi động với đối số dòng lệnh ``--headless``. Điều này cho phép chạy engine mà không cần GPU hoặc display server.

.. seealso::

    Xem :ref:`doc_creating_applications` để biết chi tiết về cách sử dụng các tính năng này.

Thiết bị di động
----------------

- :ref:`Joystick ảo <class_VirtualJoystick>` và :ref:`buttons <class_TouchScreenButton>` cho thao tác nhập cảm ứng.
- Mua hàng trong ứng dụng trên :ref:`Android <doc_android_in_app_purchases>` và `iOS <https://github.com/godot-sdk-integrations/godot-storekit2>`_.
- Hỗ trợ quảng cáo bằng các module bên thứ ba.
- Hỗ trợ chế độ picture-in-picture trên Android.

.. _doc_xr_support:

Hỗ trợ XR (AR và VR)
--------------------

- Hỗ trợ headset máy tính để bàn sử dụng :ref:`OpenXR <doc_setting_up_xr>`. Nếu một headset hoạt động với SteamVR thì headset đó cũng sẽ hoạt động với Godot.

   - Godot cũng hỗ trợ Quest qua Link, AndroidXR Direct Preview và Pico Connect.

- Hỗ trợ :ref:`headset dựa trên Android <doc_deploying_to_android>` sử dụng OpenXR. Bao gồm hỗ trợ cho các headset độc lập sau:

   - Meta Quest 1/2/3 và Pro
   - Pico 4/4 Ultra
   - Magic Leap 2
   - Lynx R1
   - HTC Vive Focus Vision
   - Headset Android XR

- Hỗ trợ Steam Frame độc lập dựa trên Linux sử dụng OpenXR.

- Hỗ trợ hạn chế cho headset Apple visionOS.

  - Hiện tại, chỉ hỗ trợ export một ứng dụng để sử dụng trên một mặt phẳng trong headset. Không hỗ trợ trải nghiệm nhập vai.

- Các thiết bị khác được hỗ trợ thông qua cấu trúc plugin XR.
- Có nhiều bộ công cụ nâng cao triển khai các tính năng phổ biến cần thiết cho ứng dụng XR.

Hệ thống GUI
------------

GUI của Godot được xây dựng bằng các node Control giống với những node được sử dụng để tạo game trong Godot. Có thể dễ dàng mở rộng UI của editor theo nhiều cách bằng các add-on.

**Các node:**

- Các nút.
- Checkbox, check button, radio button.
- Nhập văn bản bằng :ref:`class_LineEdit` (một dòng), :ref:`class_TextEdit` (nhiều dòng) và :ref:`class_CodeEdit` (hỗ trợ syntax highlighting, số dòng và nhiều tính năng khác).
- Menu thả xuống bằng :ref:`class_PopupMenu` và :ref:`class_OptionButton`, có hỗ trợ thanh tìm kiếm tùy chọn.
- Thanh cuộn.
- Nhãn.
- RichTextLabel để :ref:`định dạng văn bản bằng BBCode <doc_bbcode_in_richtextlabel>`, có hỗ trợ các hiệu ứng tùy chỉnh động.
- Cây (cũng có thể được sử dụng để biểu diễn bảng).
- Bộ chọn màu với các chế độ RGB, HSV và OKHSL, cùng các bảng màu tùy chỉnh.
- Có thể xoay và thay đổi tỷ lệ các Control.
- Hỗ trợ kéo và thả.

**Kích thước:**

- Anchor để giữ các phần tử GUI tại một góc, cạnh cụ thể hoặc ở giữa.
- Container để tự động sắp xếp các phần tử GUI theo những quy tắc nhất định.

   - :ref:`Stack <class_BoxContainer>` bố cục.
   - :ref:`Grid <class_GridContainer>` bố cục.
   - :ref:`Flow <class_FlowContainer>` bố cục (tương tự như văn bản tự động xuống dòng).
   - :ref:`Margin <class_MarginContainer>`, :ref:`centered <class_CenterContainer>` và :ref:`bố cục theo tỷ lệ khung hình <class_AspectRatioContainer>`.
   - :ref:`Bố cục splitter có thể kéo <class_SplitContainer>`.
   - :ref:`Bố cục phần có thể thu gọn <class_FoldableContainer>`.

- Chia tỷ lệ đến :ref:`nhiều độ phân giải <doc_multiple_resolutions>` bằng các chế độ stretch ``canvas_items`` hoặc ``viewport``.
- Hỗ trợ mọi tỷ lệ khung hình bằng anchor và ``expand`` stretch aspect.

**Chủ đề:**

- Trình chỉnh sửa chủ đề tích hợp sẵn.

   - Tạo chủ đề dựa trên các thiết lập chủ đề hiện tại của editor.

- Tạo chủ đề vector theo thủ tục bằng :ref:`class_StyleBoxFlat`.

   - Hỗ trợ các góc bo/vát, đổ bóng, độ rộng từng cạnh và antialiasing.

- Tạo chủ đề dựa trên texture bằng :ref:`class_StyleBoxTexture`.

Kích thước phân phối nhỏ của Godot có thể khiến nó trở thành lựa chọn thay thế phù hợp cho các framework như Electron hoặc Qt.

Animation
---------

- Động học thuận và động học nghịch.
- Hỗ trợ tạo animation cho bất kỳ thuộc tính nào với nội suy có thể tùy chỉnh.
- Hỗ trợ gọi các method trong track animation.
- Hỗ trợ phát âm thanh trong track animation.
- Hỗ trợ đường cong Bézier trong animation.

Định dạng tệp
-------------

- Scene và resource có thể được lưu ở định dạng :ref:`dựa trên văn bản <doc_tscn_file_format>` hoặc binary.

   - Định dạng dựa trên văn bản có thể đọc được đối với con người và thân thiện hơn với việc quản lý phiên bản.
   - Định dạng binary lưu/tải scene/resource lớn nhanh hơn.

- Đọc và ghi tệp văn bản hoặc tệp nhị phân bằng :ref:`class_FileAccess`.

   - Có thể tùy chọn nén hoặc mã hóa.

- Đọc và ghi tệp :ref:`class_JSON`.
- Đọc và ghi tệp cấu hình kiểu INI bằng :ref:`class_ConfigFile`.

   - Có thể (de)serialize mọi kiểu dữ liệu Godot, bao gồm Vector2/3, Color, ...

- Đọc tệp XML bằng :ref:`class_XMLParser`.
- :ref:`Tải và lưu hình ảnh, âm thanh/video, phông chữ và kho lưu trữ ZIP <doc_runtime_loading_and_saving>` trong project đã export mà không cần đi qua hệ thống import của Godot.
- Đóng gói dữ liệu game vào tệp PCK (định dạng tùy chỉnh được tối ưu để tìm kiếm nhanh), vào kho lưu trữ ZIP hoặc trực tiếp vào tệp thực thi để phân phối dưới dạng một tệp duy nhất.
- :ref:`Export các tệp PCK bổ sung <doc_exporting_pcks>` để engine có thể đọc chúng nhằm hỗ trợ mod và DLC.

Linh tinh
---------

- :ref:`Phát video <doc_playing_videos>` với hỗ trợ tích hợp cho Ogg Theora.
- :ref:`Chế độ Movie Maker <doc_creating_movies>` để ghi video từ một project đang chạy với âm thanh được đồng bộ và nhịp khung hình hoàn hảo.
- :ref:`Truy cập cấp thấp vào các server <doc_using_servers>`, cho phép bỏ qua overhead của scene tree khi cần.
- :ref:`Giao diện dòng lệnh <doc_command_line_tutorial>` để tự động hóa.

   - Export và deploy project bằng các nền tảng continuous integration.
   - `Các script shell completion <https://github.com/godotengine/godot/tree/master/misc/dist/shell>`__ có sẵn cho Bash, zsh và fish.
   - In văn bản có màu ra standard output trên tất cả các nền tảng bằng cách sử dụng
     :ref:`print_rich <class_@GlobalScope_method_print_rich>`.

- Editor có thể
  :ref:`phát hiện các tính năng được sử dụng trong project và tạo một compilation profile <doc_engine_compilation_configuration_editor>`, có thể dùng để tạo các binary export template nhỏ hơn với những tính năng không cần thiết bị vô hiệu hóa.
- Hỗ trợ các :ref:`module C++ <doc_custom_modules_in_cpp>` được liên kết tĩnh vào binary của engine.

  - Hầu hết module tích hợp có thể được vô hiệu hóa tại thời điểm compile để giảm kích thước binary trong các bản build tùy chỉnh. Xem :ref:`doc_optimizing_for_size` để biết chi tiết.

- Engine và editor được viết bằng C++17.

   - Có thể được :ref:`compile <doc_introduction_to_the_buildsystem>` bằng GCC, Clang và MSVC. MinGW cũng được hỗ trợ.
   - Thân thiện với các packager. Trong hầu hết trường hợp, có thể sử dụng các thư viện hệ thống thay cho những thư viện do Godot cung cấp. Hệ thống build không tải xuống bất kỳ thứ gì. Các bản build có thể được tái tạo hoàn toàn.

- Được cấp phép theo giấy phép MIT mang tính cởi mở.

   - Quy trình phát triển mở với `hoan nghênh đóng góp <https://contributing.godotengine.org/en/latest/index.html>`__.

.. seealso::

    `Repository đề xuất Godot <https://github.com/godotengine/godot-proposals>`__ liệt kê các tính năng được cộng đồng yêu cầu và có thể được triển khai trong các bản phát hành Godot tương lai.

.. _`Godot website`: https://godotengine.org/consoles/
.. _`iOS`: https://github.com/godot-sdk-integrations/godot-storekit2
