:allow_comments: False

.. _doc_list_of_features:

Danh sách tính năng
===================

Trang này nhằm liệt kê **tất cả** các tính năng hiện được Godot hỗ trợ.

.. note::

    Trang này liệt kê các tính năng được phiên bản ổn định hiện tại của Godot hỗ trợ. Một số tính năng trong số này không khả dụng trong `3.x release series <https://docs.godotengine.org/en/3.6/about/list_of_features.html>`__.

Nền tảng
--------

.. seealso::

    Xem :ref:`doc_system_requirements` để biết các yêu cầu về phiên bản phần cứng và phần mềm.

.. note::

    Để biết thông tin về việc hỗ trợ console, hãy xem `Godot website <https://godotengine.org/consoles/>`_.

**Có thể chạy cả trình chỉnh sửa lẫn các dự án đã xuất:**

- Windows (x86 và ARM, 64-bit và 32-bit). - macOS (x86 và ARM, chỉ 64-bit). - Linux (x86 và ARM, 64-bit và 32-bit).

   - Các tệp nhị phân được liên kết tĩnh và có thể chạy trên mọi bản phân phối nếu được biên dịch trên một bản phân phối cơ sở đủ cũ. - Các tệp nhị phân chính thức được biên dịch bằng `Godot Engine buildroot <https://github.com/godotengine/buildroot>`__, cho phép các tệp nhị phân hoạt động trên những bản phân phối Linux phổ biến.

- Android (việc hỗ trợ trình chỉnh sửa đang ở giai đoạn thử nghiệm). - :ref:`Web browsers <doc_using_the_web_editor>`. Thử nghiệm trong 4.0; thay vào đó, nên sử dụng Godot 3.x khi nhắm đến HTML5.

.. note::

    Linux hỗ trợ rv64 (RISC-V), ppc64 & ppc32 (PowerPC) và loongarch64. Tuy nhiên, bạn phải tự biên dịch trình chỉnh sửa cho nền tảng đó (cũng như các mẫu xuất), hiện chưa có bản tải xuống chính thức. Có thể tìm thấy hướng dẫn biên dịch RISC-V trên trang :ref:`doc_compiling_for_linuxbsd`.

**Chạy các dự án đã xuất:**

- iOS.

Godot hướng đến việc độc lập với nền tảng hết mức có thể và có thể
:ref:`ported to new platforms <doc_custom_platform_ports>` with relative ease.

.. note::

    Các dự án được viết bằng C# sử dụng Godot 4 hiện không thể xuất sang nền tảng web. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3. Việc hỗ trợ nền tảng Android và iOS có từ Godot 4.2, nhưng đang ở giai đoạn thử nghiệm và :ref:`some limitations apply <doc_c_sharp_platforms>`.

Trình chỉnh sửa
---------------

**Tính năng:**

- Trình chỉnh sửa cây cảnh. - Trình chỉnh sửa tập lệnh tích hợp. Cũng hỗ trợ chỉnh sửa tệp văn bản và sử dụng trình tô sáng cú pháp tùy chỉnh. - Hỗ trợ :ref:`external script editors <doc_external_editor>` như Visual Studio Code hoặc Vim. - GDScript :ref:`debugger <doc_debugger_panel>`.

   - Hỗ trợ gỡ lỗi trong các luồng.

- Trình lập hồ sơ trực quan với chỉ báo thời gian CPU và GPU cho từng bước của quy trình kết xuất. - Các công cụ giám sát hiệu năng, bao gồm
  :ref:`custom performance monitors <doc_custom_performance_monitors>`.
- Hỗ trợ :ref:`tracing profilers <doc_tracing_profilers>` như
  :ref:`doc_profiler_tracy` and :ref:`doc_profiler_perfetto` for deeper optimization tasks.
- Bất kỳ tập lệnh nào cũng có thể được :ref:`run in the editor <doc_running_code_in_the_editor>` và cung cấp chức năng tùy chỉnh, chẳng hạn như các nút có thể nhấp trong trình kiểm tra, mà không cần tạo plugin cho trình chỉnh sửa. - Tải lại tập lệnh trực tiếp. - Chỉnh sửa cảnh trực tiếp.

   - Các thay đổi *sẽ* được phản ánh trong trình chỉnh sửa và *sẽ* được giữ lại sau khi đóng dự án đang chạy.

- Nhân bản camera trực tiếp (bị tắt theo mặc định).

   - Di chuyển camera trong trình chỉnh sửa và xem kết quả trong dự án đang chạy.

- Trình kiểm tra từ xa.

   - Các thay đổi *sẽ không* được phản ánh trong trình chỉnh sửa và *sẽ không* được giữ lại sau khi đóng dự án đang chạy.

- Chạy nhiều phiên bản dự án đồng thời từ một phiên bản trình chỉnh sửa duy nhất (hữu ích khi kiểm thử máy khách/máy chủ). - :ref:`game embedding <doc_game_embedding>` tùy chọn để chạy dự án trong một bảng bên trong trình chỉnh sửa.

  - Chọn các node 2D và 3D trong khung nhìn của dự án để kiểm tra chúng trong trình chỉnh sửa. - Di chuyển camera trong dự án bằng các chế độ ghi đè camera 2D và 3D. - Hỗ trợ điều chỉnh tỷ lệ thời gian, tạm dừng và tiến từng khung hình. - Hỗ trợ tắt tiếng dự án.

- Công cụ thước để đo khoảng cách trong 2D và 3D. - Hỗ trợ bắt dính đỉnh trong 3D. - Hỗ trợ theo dõi vùng chọn khi vùng này di chuyển trong 3D bằng cách sử dụng Focus Selection hai lần. - Tài liệu tham khảo lớp tích hợp, có thể sử dụng ngoại tuyến. - Sử dụng trình chỉnh sửa bằng hàng chục ngôn ngữ do cộng đồng đóng góp.

**Plugin:**

- Có thể tải plugin cho trình chỉnh sửa từ
  :ref:`Asset Store <doc_what_is_asset_store>` to extend editor functionality.
- :ref:`Create your own plugins <doc_making_plugins>` bằng GDScript để thêm tính năng mới hoặc tăng tốc quy trình làm việc. - :ref:`Download projects from the Asset Store <doc_using_asset_store_editor>` trong Project Manager và nhập chúng trực tiếp.

Kết xuất
--------

Godot 4 bao gồm ba trình kết xuất:

- **Forward+**. Trình kết xuất tiên tiến nhất, chỉ phù hợp với các nền tảng máy tính để bàn. Được sử dụng theo mặc định trên các nền tảng máy tính để bàn. Trình kết xuất này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm trình điều khiển kết xuất và sử dụng phần phụ trợ **RenderingDevice**. - **Mobile**. Có ít tính năng hơn nhưng kết xuất các cảnh đơn giản nhanh hơn. Phù hợp với các nền tảng di động và máy tính để bàn. Được sử dụng theo mặc định trên các nền tảng di động. Trình kết xuất này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm trình điều khiển kết xuất và sử dụng phần phụ trợ **RenderingDevice**. - **Compatibility**, đôi khi được gọi là **GL Compatibility**. Trình kết xuất ít tiên tiến nhất, phù hợp với các nền tảng máy tính để bàn và di động cấp thấp. Được sử dụng theo mặc định trên nền tảng web. Trình kết xuất này sử dụng **OpenGL** làm trình điều khiển kết xuất.

.. seealso::

    Xem :ref:`doc_renderers` để biết so sánh chi tiết giữa các phương pháp kết xuất.

Đồ họa 2D
---------

- Kết xuất sprite, đa giác và đường.

   - Các công cụ cấp cao để vẽ đường và đa giác như
     :ref:`class_Polygon2D` and :ref:`class_Line2D`, with support for texturing.

- AnimatedSprite2D làm trình trợ giúp để tạo sprite động. - Các lớp thị sai.

   - Hỗ trợ giả 3D, bao gồm cả bản xem trước trong trình chỉnh sửa.

- :ref:`2D lighting <doc_2d_lights_and_shadows>` với các bản đồ pháp tuyến và bản đồ phản chiếu.

   - Đèn 2D điểm (toàn hướng/tiêu điểm) và định hướng. - Bóng cứng hoặc mềm (có thể điều chỉnh theo từng đèn). - Shader tùy chỉnh có thể truy cập biểu diễn :abbr:`SDF (Signed Distance Field)` theo thời gian thực của cảnh 2D dựa trên các node :ref:`class_LightOccluder2D`, có thể được sử dụng để cải thiện hiệu ứng chiếu sáng 2D, bao gồm cả chiếu sáng toàn cục 2D.

- :ref:`Font rendering <doc_gui_using_fonts>` bằng bitmap, raster hóa bằng FreeType hoặc các trường khoảng cách có dấu đa kênh (MSDF).

   - Phông chữ bitmap có thể được xuất bằng các công cụ như BMFont hoặc nhập từ hình ảnh (chỉ dành cho phông chữ có chiều rộng cố định). - Phông chữ động hỗ trợ phông chữ đơn sắc cũng như phông chữ màu (ví dụ: emoji). Các định dạng được hỗ trợ là TTF, OTF, WOFF1 và WOFF2. - Phông chữ động hỗ trợ đường viền phông chữ tùy chọn với chiều rộng và màu sắc có thể điều chỉnh. - Phông chữ động hỗ trợ phông chữ biến thiên và các tính năng OpenType, bao gồm chữ ghép. - Phông chữ động hỗ trợ mô phỏng kiểu đậm và nghiêng khi tệp phông chữ không có các kiểu đó. - Phông chữ động hỗ trợ lấy mẫu vượt mức để giữ cho phông chữ sắc nét hơn ở độ phân giải cao hơn. - Phông chữ động hỗ trợ định vị dưới pixel để làm cho phông chữ rõ nét hơn ở kích thước nhỏ. - Phông chữ động hỗ trợ tối ưu hóa LCD dưới pixel để làm cho phông chữ thậm chí rõ nét hơn ở kích thước nhỏ. - Phông chữ trường khoảng cách có dấu có thể được thu phóng ở bất kỳ độ phân giải nào mà không cần raster hóa lại. Việc sử dụng đa kênh giúp phông chữ SDF thu nhỏ xuống các kích thước thấp hơn tốt hơn so với phông chữ SDF đơn sắc.

- :ref:`Oversampling <doc_multiple_resolutions_font_and_image_oversampling>` cho hình ảnh SVG bằng loại nhập :ref:`class_DPITexture`. Điều này cho phép đạt được kết quả sắc nét hơn khi phóng to kết cấu bằng cách raster hóa lại hình ảnh nguồn SVG thành độ phân giải mới trong thời gian chạy.

  - Lấy mẫu vượt mức tùy chọn có thể tính đến các tỷ lệ :ref:`class_CanvasItem` riêng lẻ để kết xuất rõ nét hơn khi thu phóng node.

- :ref:`particles <doc_particle_systems_2d>` dựa trên GPU với hỗ trợ cho
  :ref:`custom particle shaders <doc_particle_shader>`.
- Các hạt dựa trên CPU. - :ref:`2D HDR rendering <doc_environment_and_post_processing_using_glow_in_2d>` tùy chọn để có khả năng phát sáng tốt hơn. - Debanding tùy chọn để giảm các hiện tượng dải màu trong chuyển sắc. - :ref:`HDR output <doc_hdr_output>` trên các nền tảng và trình kết xuất được hỗ trợ.

Công cụ 2D
----------

- :ref:`TileMaps <doc_using_tilemaps>` để thiết kế màn chơi dựa trên ô 2D. - Camera 2D với tính năng làm mượt và lề kéo tích hợp. - Node Path2D để biểu diễn một đường dẫn trong không gian 2D.

   - Có thể được vẽ trong trình chỉnh sửa hoặc tạo theo thủ tục. - Node PathFollow2D để khiến các node đi theo một Path2D.

- :ref:`2D geometry helper class <class_Geometry2D>`.

Vật lý 2D
---------

**Vật thể vật lý:**

- Vật thể tĩnh. - Vật thể có thể hoạt ảnh (dành cho các đối tượng chỉ di chuyển bằng tập lệnh hoặc hoạt ảnh, chẳng hạn như cửa và nền tảng). - Vật thể rắn. - Vật thể nhân vật. - Khớp nối. - Các vùng để phát hiện vật thể đi vào hoặc rời khỏi vùng đó. - :ref:`Physics interpolation <doc_physics_interpolation>`.

**Phát hiện va chạm:**

- Các hình dạng tích hợp: đường, hộp, hình tròn, viên nang, ranh giới thế giới (mặt phẳng vô hạn). - Các đa giác va chạm (có thể được vẽ thủ công hoặc tạo từ một sprite trong trình chỉnh sửa).

Đồ họa 3D
---------

- Tính toán chiếu sáng HDR tuyến tính nội bộ. - Debanding tùy chọn để giảm các hiện tượng dải màu trong chuyển sắc. - :ref:`HDR output <doc_hdr_output>` trên các nền tảng và trình kết xuất được hỗ trợ. - Camera phối cảnh, trực giao và lệch frustum. - Khi sử dụng trình kết xuất Forward+, một bước tiền xử lý độ sâu được dùng để cải thiện hiệu năng trong các cảnh phức tạp bằng cách giảm chi phí overdraw. - :ref:`doc_variable_rate_shading` trên các GPU được hỗ trợ trong Forward+ và Mobile.

**Kết xuất dựa trên vật lý (các tính năng vật liệu tích hợp):**

- Tuân theo mô hình PBR của Disney. - Hỗ trợ các chế độ đổ bóng khuếch tán Burley, Lambert, Lambert Wrap (half-Lambert) và Toon. - Hỗ trợ các chế độ đổ bóng phản chiếu Schlick-GGX, Toon và Disabled. - Sử dụng quy trình roughness-metallic với hỗ trợ cho kết cấu ORM. - Sử dụng hiện tượng che khuất phản chiếu theo đường chân trời (mô hình Filament) để cải thiện diện mạo vật liệu. - Lập bản đồ pháp tuyến. - Lập bản đồ thị sai/địa hình với mức độ chi tiết tự động dựa trên khoảng cách. - Lập bản đồ chi tiết cho các bản đồ albedo và pháp tuyến. - Tán xạ dưới bề mặt và độ truyền qua. - Khúc xạ trong không gian màn hình với hỗ trợ cho độ roughness của vật liệu (tạo ra khúc xạ mờ). - Làm mờ theo độ gần (hạt mềm) và làm mờ theo khoảng cách. - Làm mờ theo khoảng cách có thể sử dụng trộn alpha hoặc dithering để tránh đi qua quy trình trong suốt. - Dithering có thể được xác định theo từng pixel hoặc từng đối tượng.

**Chiếu sáng theo thời gian thực:**

- :ref:`Directional lights <doc_lights_and_shadows_directional_light>` (mặt trời/mặt trăng). - :ref:`Omnidirectional lights <doc_lights_and_shadows_omni_light>`. - :ref:`Spot lights <doc_lights_and_shadows_spot_light>` với góc hình nón và độ suy giảm có thể điều chỉnh. - :ref:`Rectangular area lights <doc_lights_and_shadows_area_light>` với kết cấu tùy chọn để xác định hình dạng và màu sắc. - Có thể điều chỉnh năng lượng của ánh sáng phản chiếu, ánh sáng gián tiếp và sương mù thể tích cho từng nguồn sáng. - Có thể điều chỉnh "kích thước" ánh sáng cho đèn omni hình cầu và đèn spot dạng đĩa (đồng thời làm bóng mờ hơn với vùng nửa tối thay đổi). - Hệ thống làm mờ theo khoảng cách tùy chọn để làm mờ các nguồn sáng ở xa và bóng của chúng, giúp cải thiện hiệu năng. - Khi sử dụng trình kết xuất Forward+ (mặc định trên máy tính), các nguồn sáng được kết xuất bằng các tối ưu hóa forward theo cụm để giảm chi phí riêng lẻ. Kết xuất theo cụm cũng loại bỏ mọi giới hạn về số lượng nguồn sáng có thể sử dụng trên một mesh. - Khi sử dụng trình kết xuất Mobile, mỗi tài nguyên mesh có thể hiển thị tối đa 8 đèn omni, 8 đèn spot và 8 đèn area. Có thể sử dụng ánh sáng được bake để vượt qua giới hạn này nếu cần.

**Lập bản đồ bóng:**

- *DirectionalLight3D:* Trực giao (nhanh nhất), PSSM 2 phần và 4 phần. Hỗ trợ pha trộn giữa các phần. - *OmniLight3D:* Paraboloid kép (nhanh) hoặc cubemap (chậm hơn nhưng chính xác hơn). Hỗ trợ các kết cấu projector có màu ở dạng panorama. - *SpotLight3D:* Một kết cấu. Hỗ trợ các kết cấu projector có màu. - *AreaLight3D:* Một kết cấu với biến dạng paraboloid kép để xấp xỉ hình dạng của ánh sáng. - Độ lệch pháp tuyến của bóng và kỹ thuật làm phẳng bóng để giảm hiện tượng bóng bị lỗi dạng acne và peter-panning có thể nhìn thấy. - Độ mờ bóng tương tự :abbr:`PCSS (Percentage Closer Soft Shadows)`, dựa trên kích thước ánh sáng và khoảng cách từ bề mặt đổ bóng. Được hỗ trợ cho mọi loại ánh sáng. - Có thể điều chỉnh độ mờ bóng cho từng nguồn sáng.

**Chiếu sáng toàn cục với ánh sáng gián tiếp:**

- :ref:`Baked lightmaps <doc_using_lightmap_gi>` (nhanh, nhưng không thể cập nhật trong thời gian chạy).

   - Hỗ trợ bake chỉ ánh sáng gián tiếp hoặc bake cả ánh sáng trực tiếp và gián tiếp. Có thể điều chỉnh chế độ bake cho từng nguồn sáng để cho phép thiết lập bake ánh sáng lai. - Hỗ trợ chiếu sáng các đối tượng động bằng probe tự động và probe được đặt thủ công. - Tùy chọn hỗ trợ chiếu sáng định hướng dựa trên các hài cầu. - Tùy chọn hỗ trợ bake shadowmask cho bóng định hướng tĩnh ở xa. - Tùy chọn supersampling trong thời gian bake để cải thiện chất lượng và giảm hiện tượng rò rỉ ánh sáng, nhưng phải đánh đổi bằng thời gian bake lâu hơn và mức sử dụng bộ nhớ cao hơn trong quá trình bake. - Lightmap được bake trên GPU bằng compute shader (nhanh hơn nhiều so với lightmap trên CPU). Chỉ có thể thực hiện bake từ trình chỉnh sửa, không phải trong các dự án đã export. - Hỗ trợ :ref:`denoising <doc_using_lightmap_gi_denoising>` trên GPU với JNLM ngay khi cài đặt, hoặc khử nhiễu chất lượng cao hơn trên CPU/GPU bằng OIDN (yêu cầu tải OIDN riêng). - Lightmap được kết xuất bằng bộ lọc bicubic để giảm các hiện tượng biến dạng do thay đổi tỷ lệ.

- :ref:`Voxel-based GI probes <doc_using_voxel_gi>`. Hỗ trợ *cả* nguồn sáng động *và* vật cản động, đồng thời hỗ trợ phản chiếu. Yêu cầu một bước bake nhanh có thể thực hiện trong trình chỉnh sửa hoặc trong thời gian chạy (kể cả từ một dự án đã export). - :ref:`Signed-distance field GI <doc_using_sdfgi>` được thiết kế cho các thế giới mở rộng lớn. Hỗ trợ nguồn sáng động nhưng không hỗ trợ vật cản động. Hỗ trợ phản chiếu. Không yêu cầu bake. - :ref:`Screen-space indirect lighting (SSIL) <doc_environment_and_post_processing_ssil>` ở độ phân giải một nửa hoặc đầy đủ. Hoàn toàn theo thời gian thực và hỗ trợ mọi loại nguồn sáng phát xạ (bao gồm decal). - VoxelGI và SDFGI sử dụng một lượt chuyển tiếp deferred để cho phép kết xuất GI ở độ phân giải một nửa nhằm cải thiện hiệu năng (đồng thời vẫn hỗ trợ MSAA hoạt động).

**Phản chiếu:**

- Phản chiếu dựa trên voxel (khi sử dụng probe GI) và phản chiếu dựa trên SDF (khi sử dụng GI trường khoảng cách có dấu). Phản chiếu dựa trên voxel hiển thị trên các bề mặt trong suốt, trong khi phản chiếu dựa trên SDF thô cũng hiển thị trên các bề mặt trong suốt. - Phản chiếu được bake nhanh hoặc phản chiếu theo thời gian thực chậm bằng ReflectionProbe. Có thể tùy chọn bật hiệu chỉnh hộp parallax. - Phản chiếu trong không gian màn hình với hỗ trợ độ nhám của vật liệu. - Có thể kết hợp các kỹ thuật phản chiếu để đạt độ chính xác hoặc khả năng mở rộng cao hơn. - Khi sử dụng trình kết xuất Forward+ (mặc định trên máy tính), các probe phản chiếu được kết xuất bằng các tối ưu hóa forward theo cụm để giảm chi phí riêng lẻ. Kết xuất theo cụm cũng loại bỏ mọi giới hạn về số lượng probe phản chiếu có thể sử dụng trên một mesh. - Khi sử dụng trình kết xuất Mobile, mỗi tài nguyên mesh có thể hiển thị tối đa 8 probe phản chiếu. Khi sử dụng trình kết xuất Compatibility, mỗi tài nguyên mesh có thể hiển thị tối đa 2 probe phản chiếu.

**Decal:**

- :ref:`Supports albedo <doc_using_decals>`, phát xạ, :abbr:`ORM (Occlusion Roughness Metallic)` và lập bản đồ pháp tuyến. - Các kênh kết cấu được phủ mượt lên trên vật liệu bên dưới, hỗ trợ decal chỉ có pháp tuyến/ORM. - Hỗ trợ làm mờ pháp tuyến để làm mờ decal tùy theo góc tới của nó. - Không phụ thuộc vào việc tạo mesh trong thời gian chạy. Điều này nghĩa là decal có thể được sử dụng trên các mesh có skin phức tạp mà không bị phạt hiệu năng, ngay cả khi decal di chuyển ở mỗi khung hình. - Hỗ trợ lọc kết cấu nearest, bilinear, trilinear hoặc anisotropic (được cấu hình trên toàn cục). - Hệ thống làm mờ theo khoảng cách tùy chọn để làm mờ các decal ở xa, giúp cải thiện hiệu năng. - Khi sử dụng trình kết xuất Forward+ (mặc định trên máy tính), decal được kết xuất bằng các tối ưu hóa forward theo cụm để giảm chi phí riêng lẻ. Kết xuất theo cụm cũng loại bỏ mọi giới hạn về số lượng decal có thể sử dụng trên một mesh. - Khi sử dụng trình kết xuất Mobile, mỗi tài nguyên mesh có thể hiển thị tối đa 8 decal.

**Bầu trời:**

- Bầu trời panorama (sử dụng HDRI). - Bầu trời thủ tục và bầu trời dựa trên vật lý phản hồi theo các DirectionalLight trong cảnh. - Hỗ trợ :ref:`custom sky shaders <doc_sky_shader>`, có thể được tạo hoạt ảnh. - Bản đồ bức xạ được sử dụng cho ánh sáng môi trường và ánh sáng phản chiếu có thể được cập nhật theo thời gian thực tùy thuộc vào các thiết lập chất lượng đã chọn.

**Sương mù:**

- Sương mù độ sâu hàm mũ. - Sương mù độ cao hàm mũ. - Hỗ trợ tự động chọn màu sương mù tùy theo màu bầu trời (phối cảnh khí quyển). - Hỗ trợ tán xạ ánh sáng mặt trời trong sương mù. - Hỗ trợ kiểm soát mức độ ảnh hưởng của việc kết xuất sương mù lên bầu trời, với các điều khiển riêng cho sương mù truyền thống và sương mù thể tích. - Hỗ trợ để các vật liệu cụ thể bỏ qua sương mù.

**Sương mù thể tích:**

- :ref:`volumetric fog <doc_volumetric_fog>` toàn cục phản ứng với nguồn sáng và bóng. - Sương mù thể tích có thể tính đến ánh sáng gián tiếp khi sử dụng VoxelGI hoặc SDFGI. - Các node thể tích sương mù có thể được đặt để thêm sương mù vào các khu vực cụ thể (hoặc loại bỏ sương mù khỏi các khu vực cụ thể). Các hình dạng được hỗ trợ gồm hộp, elip, hình nón, hình trụ và bản đồ mật độ dựa trên kết cấu 3D. - Mỗi thể tích sương mù có thể có shader tùy chỉnh riêng. - Có thể sử dụng cùng với sương mù truyền thống.

**Hạt:**

- Hạt dựa trên GPU với hỗ trợ cho subemitter (2D + 3D), vệt (2D + 3D), attractor (chỉ 3D) và va chạm (2D + 3D).

  - Các hình dạng attractor hạt 3D được hỗ trợ: hộp, hình cầu và trường vector 3D. - Các hình dạng va chạm hạt 3D được hỗ trợ: hộp, hình cầu, trường khoảng cách có dấu được bake và heightmap theo thời gian thực (phù hợp với hiệu ứng thời tiết trong thế giới mở). - Va chạm hạt 2D được xử lý bằng trường khoảng cách có dấu được tạo theo thời gian thực dựa trên các node :ref:`class_LightOccluder2D` trong cảnh. - Vệt có thể sử dụng mesh vệt ruy-băng và mesh vệt ống tích hợp sẵn, hoặc mesh tùy chỉnh có skeleton. - Hỗ trợ shader hạt tùy chỉnh với phát sinh thủ công.

- Hạt dựa trên CPU.

**Hậu kỳ:**

- Ánh xạ tông màu (Linear, Reinhard, Filmic, ACES, AgX). - Tự động điều chỉnh phơi sáng dựa trên độ sáng của viewport (và ghi đè phơi sáng thủ công). - Độ sâu trường ảnh gần và xa với mô phỏng bokeh có thể điều chỉnh (hộp, lục giác, hình tròn). - Che khuất môi trường trong không gian màn hình (SSAO) ở độ phân giải một nửa hoặc đầy đủ. - Glow/bloom với tùy chọn nâng tỷ lệ bicubic và một số chế độ hòa trộn: Screen, Soft Light, Add, Replace, Mix. - Glow có thể sử dụng kết cấu bản đồ bụi bẩn có màu, tạo hiệu ứng bụi bẩn trên ống kính. - Glow có thể được :ref:`used as a screen-space blur effect <doc_environment_and_post_processing_using_glow_to_blur_the_screen>`. - Hiệu chỉnh màu bằng ramp một chiều hoặc kết cấu LUT 3D. - Bộ giới hạn độ nhám để giảm ảnh hưởng của aliasing ánh sáng phản chiếu. - Điều chỉnh độ sáng, độ tương phản và độ bão hòa.

**Lọc kết cấu:**

- Lọc nearest, bilinear, trilinear hoặc anisotropic. - Các tùy chọn lọc được xác định theo từng lần sử dụng, không phải theo từng kết cấu.

**Nén VRAM kết cấu:**

- BPTC (cho nén chất lượng cao nhắm đến các nền tảng máy tính). - ASTC (cho nén chất lượng cao nhắm đến các nền tảng di động). - ETC2 (cho nén nhanh nhắm đến các nền tảng di động). - S3TC (cho nén nhanh nhắm đến các nền tảng máy tính). - Basis Universal (chậm, nhưng chỉ yêu cầu một lần mã hóa cho mọi nền tảng).

**Khử răng cưa:**

- :ref:`antialiasing <doc_3d_antialiasing>` theo thời gian (TAA). - :ref:`antialiasing <doc_3d_antialiasing>` AMD FidelityFX Super Resolution 2.2 (FSR2), có thể được sử dụng ở độ phân giải gốc như một dạng khử răng cưa theo thời gian chất lượng cao. - Khử răng cưa đa mẫu (MSAA), cho cả :ref:`doc_2d_antialiasing` và :ref:`doc_3d_antialiasing`. - Khử răng cưa xấp xỉ nhanh (FXAA). - Khử răng cưa siêu mẫu (SSAA) bằng cách chia tỷ lệ 3D bilinear và tỷ lệ độ phân giải 3D lớn hơn 1.0. - Khử răng cưa alpha, alpha MSAA theo độ bao phủ và băm alpha theo từng vật liệu.

**Chia tỷ lệ độ phân giải:**

- Hỗ trợ :ref:`rendering 3D at a lower resolution <doc_resolution_scaling>` trong khi vẫn giữ kết xuất 2D ở tỷ lệ ban đầu. Có thể sử dụng tính năng này để cải thiện hiệu năng trên các hệ thống cấp thấp hoặc cải thiện hình ảnh trên các hệ thống cấp cao. - Chia tỷ lệ độ phân giải sử dụng lọc nearest-neighbor, lọc bilinear, AMD FidelityFX Super Resolution 1.0 (FSR1) hoặc AMD FidelityFX Super Resolution 2.2.1 (FSR2). - Bias LOD mipmap của kết cấu được tự động điều chỉnh để cải thiện chất lượng ở các tỷ lệ độ phân giải thấp hơn. Bias này cũng có thể được sửa đổi bằng một độ lệch thủ công.

Hầu hết các hiệu ứng được liệt kê ở trên đều có thể được điều chỉnh để cải thiện hiệu năng hoặc nâng cao hơn nữa chất lượng. Điều này có thể hữu ích khi
:ref:`using Godot for offline rendering <doc_creating_movies>`.

Công cụ 3D
----------

- Lưới dựng sẵn: hình lập phương, hình trụ/hình nón, hình cầu (bán cầu), lăng trụ, mặt phẳng, tứ giác, hình xuyến, dải, ống. - :ref:`GridMaps <doc_using_gridmaps>` cho thiết kế màn chơi 3D dạng ô. - :ref:`Constructive solid geometry <doc_csg_tools>` (dành cho việc tạo nguyên mẫu). - Công cụ cho :ref:`procedural geometry generation <doc_procedural_geometry>`. - Nút Path3D để biểu diễn một đường đi trong không gian 3D.

   - Có thể được vẽ trong trình chỉnh sửa hoặc tạo theo thủ tục. - Nút PathFollow3D để khiến các nút đi theo một Path3D.

- :ref:`3D geometry helper class <class_Geometry3D>`. - Hỗ trợ xuất cảnh hiện tại thành tệp glTF 2.0, cả từ trình chỉnh sửa lẫn trong thời gian chạy từ một dự án đã xuất.

Vật lý 3D
---------

**Thân vật lý:**

- Thân tĩnh. - Thân có thể hoạt ảnh (dành cho các đối tượng chỉ chuyển động bằng tập lệnh hoặc hoạt ảnh, chẳng hạn như cửa và bệ). - Thân cứng. - Thân nhân vật. - Thân phương tiện (dành cho vật lý kiểu arcade, không phải mô phỏng). - Khớp nối. - :ref:`Soft bodies <doc_soft_body>`. - :ref:`Ragdolls <doc_ragdoll_system>`. - Vùng để phát hiện các thân đi vào hoặc rời khỏi vùng đó. - :ref:`Physics interpolation <doc_physics_interpolation>`.

**Phát hiện va chạm:**

- Các hình dạng dựng sẵn: hình hộp, hình cầu, hình con nhộng, hình trụ, ranh giới thế giới (mặt phẳng vô hạn). - Tạo các hình dạng va chạm tam giác cho mọi lưới từ trình chỉnh sửa. - Tạo một hoặc nhiều hình dạng va chạm lồi cho mọi lưới từ trình chỉnh sửa.

Shader
------

- *2D:* Shader đỉnh, mảnh và ánh sáng tùy chỉnh. - *3D:* Shader đỉnh, mảnh, ánh sáng, bầu trời và sương mù tùy chỉnh. - Shader tùy chỉnh có thể tạo và sửa đổi kết cấu theo thủ tục trong thời gian thực bằng cách sử dụng
  :ref:`class_DrawableTexture2D`.
- Shader dạng văn bản sử dụng :ref:`shader language inspired by GLSL <doc_shading_language>`. - Tô sáng cú pháp được cung cấp trên GitHub bằng cách sử dụng ``gdshader`` làm tên ngôn ngữ trong khối mã Markdown. - Trình chỉnh sửa shader trực quan.

   - Hỗ trợ :ref:`visual shader plugins <doc_visual_shader_plugins>`.

Lập trình bằng tập lệnh
-----------------------

**Tổng quát:**

- Mẫu thiết kế hướng đối tượng với các tập lệnh mở rộng các nút. - Tín hiệu và nhóm để giao tiếp giữa các tập lệnh. - Hỗ trợ :ref:`cross-language scripting <doc_cross_language_scripting>`. - Nhiều kiểu dữ liệu đại số tuyến tính 2D, 3D và 4D như vectơ và phép biến đổi.

:ref:`GDScript: <doc_gdscript>`

- :ref:`High-level interpreted language <doc_gdscript_reference>` với
  :ref:`optional static typing <doc_gdscript_static_typing>`.
- Cú pháp lấy cảm hứng từ Python. Tuy nhiên, GDScript **không** dựa trên Python. - Tô sáng cú pháp được cung cấp trên GitHub bằng cách sử dụng ``gdscript`` làm tên ngôn ngữ trong khối mã Markdown. - :ref:`Use threads <doc_using_multiple_threads>` để thực hiện các tác vụ bất đồng bộ hoặc sử dụng nhiều lõi xử lý.

:ref:`C#: <doc_c_sharp>`

- Được đóng gói trong một tệp nhị phân riêng để giảm kích thước tệp và số lượng phần phụ thuộc. - Hỗ trợ .NET 8 trở lên.

   - Hỗ trợ đầy đủ cú pháp và tính năng của C# 12.0.

- Hỗ trợ Windows, Linux và macOS. Kể từ Godot 4.2, hỗ trợ thử nghiệm cho Android và iOS cũng khả dụng.

   - Trên nền tảng iOS, chỉ một số kiến trúc được hỗ trợ: ``arm64``. - Nền tảng web hiện chưa được hỗ trợ. Để sử dụng C# trên nền tảng đó, hãy cân nhắc dùng Godot 3.

- Khuyến nghị sử dụng trình chỉnh sửa bên ngoài để tận dụng các chức năng của IDE.

**GDExtension (C, C++, Rust, D, ...):**

- Khi cần, hãy liên kết với các thư viện gốc để đạt hiệu năng cao hơn và tích hợp với bên thứ ba.

   - Để lập trình logic trò chơi, nên sử dụng GDScript hoặc C# nếu hiệu năng của chúng phù hợp.

- Các liên kết GDExtension chính thức cho `C <https://github.com/godotengine/godot-headers>`__ và `C++ <https://github.com/godotengine/godot-cpp>`__.

   - Sử dụng bất kỳ hệ thống xây dựng và tính năng ngôn ngữ nào bạn muốn.

- Các liên kết GDExtension cho `D <https://github.com/godot-dlang/godot-dlang>`__, `Swift <https://github.com/migueldeicaza/SwiftGodot>`__ và `Rust <https://github.com/godot-rust/gdextension>`__ đang được cộng đồng tích cực phát triển. (Một số liên kết trong số này có thể đang ở trạng thái thử nghiệm và chưa sẵn sàng cho môi trường sản xuất).

Âm thanh
--------

**Tính năng:**

- Đầu ra mono, stereo, 5.1 và 7.1. - Phát lại có định vị và không định vị trong 2D và 3D.

   - Hiệu ứng Doppler tùy chọn trong 2D và 3D.

- Hỗ trợ :ref:`audio buses <doc_audio_buses>` có thể định tuyến lại và các hiệu ứng với hàng chục hiệu ứng được tích hợp. - Hỗ trợ đa âm (phát nhiều âm thanh từ một nút :ref:`class_AudioStreamPlayer`). - Hỗ trợ âm lượng và cao độ ngẫu nhiên. - Hỗ trợ thay đổi cao độ trong thời gian thực. - Hỗ trợ chọn mẫu tuần tự/ngẫu nhiên, bao gồm ngăn lặp lại khi chọn mẫu ngẫu nhiên. - Các nút :ref:`class_AudioListener2D` và :ref:`class_AudioListener3D` để lắng nghe từ một vị trí khác với camera. - Hỗ trợ :ref:`procedural audio generation <class_AudioStreamGenerator>`. - Đầu vào âm thanh để ghi âm từ micrô. - :ref:`Text to speech <doc_text_to_speech>` bằng các công cụ TTS do nền tảng cung cấp. - Đầu vào MIDI.

   - Hiện chưa hỗ trợ đầu ra MIDI.

**Các API được sử dụng:**

- *Windows:* WASAPI. - *macOS:* CoreAudio. - *Linux:* PulseAudio hoặc ALSA.

Nhập
----

- Hỗ trợ :ref:`custom import plugins <doc_import_plugins>`.

**Định dạng:**

- *Hình ảnh:* Xem :ref:`doc_importing_images`. - *Âm thanh:*

   - WAV với tính năng nén :abbr:`QOA (Quite OK Audio)` hoặc IMA-ADPCM tùy chọn. - Ogg Vorbis. - MP3.

- *Cảnh 3D:* Xem :ref:`doc_importing_3d_scenes`.

   - glTF 2.0 *(khuyến nghị)*. - ``.blend`` (bằng cách gọi minh bạch chức năng xuất glTF của Blender). - FBX (bằng cách gọi minh bạch `FBX2glTF <https://github.com/godotengine/FBX2glTF>`__). - Collada (.dae). - Wavefront OBJ (chỉ dành cho cảnh tĩnh, có thể được tải trực tiếp dưới dạng lưới hoặc nhập dưới dạng cảnh 3D).

- Hỗ trợ tải các cảnh glTF 2.0 trong thời gian chạy, bao gồm từ một dự án đã xuất. - Các lưới 3D sử dụng `Mikktspace <http://www.mikktspace.com/>`__ để tạo các tiếp tuyến khi nhập, đảm bảo tính nhất quán với các ứng dụng 3D khác như Blender.

Đầu vào
-------

- :ref:`Input mapping system <doc_input_examples>` bằng các sự kiện đầu vào được mã hóa cứng hoặc các hành động đầu vào có thể ánh xạ lại.

   - Các giá trị trục có thể được ánh xạ tới hai hành động khác nhau với vùng chết có thể cấu hình. - Sử dụng cùng một mã để hỗ trợ cả bàn phím và tay cầm chơi game.

- Đầu vào từ bàn phím.

   - Các phím có thể được ánh xạ ở chế độ "physical" để không phụ thuộc vào bố cục bàn phím.

- Đầu vào từ chuột.

   - Con trỏ chuột có thể hiển thị, ẩn, được bắt giữ hoặc giới hạn trong cửa sổ. - Có thể thay đổi hình dạng con trỏ chuột thành hình ảnh tùy chỉnh hoặc một trong các con trỏ hệ thống. - Khi bị bắt giữ, đầu vào thô được sử dụng trên Windows và Linux để bỏ qua cài đặt tăng tốc chuột của hệ điều hành.

- :ref:`Gamepad input <doc_controllers_gamepads_joysticks>` (tối đa 8 tay cầm đồng thời).

  - Hỗ trợ :ref:`changing the LED color <doc_controller_features_led_color>` trên các tay cầm được hỗ trợ. - Hỗ trợ :ref:`reading motion sensors <doc_controller_features_motion_sensors>` trên các tay cầm được hỗ trợ (dùng để triển khai ngắm bằng con quay hồi chuyển).

- Đầu vào từ bút/máy tính bảng với hỗ trợ áp lực và độ nghiêng.

Điều hướng
----------

- Thuật toán A* trong :ref:`2D <class_AStar2D>` và :ref:`3D <class_AStar3D>`. - Lưới điều hướng với khả năng tránh chướng ngại vật động trong
  :ref:`2D <doc_navigation_overview_2d>` and :ref:`3D <doc_navigation_overview_3d>`.
- Tạo lưới điều hướng từ trình chỉnh sửa hoặc trong thời gian chạy (bao gồm từ một dự án đã xuất).

Mạng
----

- Mạng TCP cấp thấp sử dụng :ref:`class_StreamPeer` và :ref:`class_TCPServer`. - Mạng UDP cấp thấp sử dụng :ref:`class_PacketPeer` và :ref:`class_UDPServer`. - Các yêu cầu HTTP cấp thấp sử dụng :ref:`class_HTTPClient`. - Các yêu cầu HTTP cấp cao sử dụng :ref:`class_HTTPRequest`.

   - Hỗ trợ HTTPS ngay khi cài đặt bằng các chứng chỉ đi kèm.

- API :ref:`High-level multiplayer <doc_high_level_multiplayer>` sử dụng UDP và ENet.

   - Tự động sao chép bằng các lệnh gọi thủ tục từ xa (RPC). - Hỗ trợ truyền không đáng tin cậy, đáng tin cậy và theo thứ tự.

- Máy khách và máy chủ :ref:`WebSocket <doc_websocket>`, khả dụng trên mọi nền tảng. - Máy khách và máy chủ :ref:`WebRTC <doc_webrtc>`, khả dụng trên mọi nền tảng. - Hỗ trợ :ref:`UPnP <class_UPNP>` để không cần chuyển tiếp cổng khi lưu trữ máy chủ phía sau NAT.

Quốc tế hóa
-----------

- Hỗ trợ đầy đủ Unicode, bao gồm emoji. - Hỗ trợ tải phông chữ hệ thống trên Windows, macOS và Linux.

  - Theo mặc định, phông chữ hệ thống được sử dụng làm phương án dự phòng để hiển thị các ký tự không được hỗ trợ. Điều này cho phép hiển thị chính xác văn bản đa ngôn ngữ mà không cần đóng gói các tệp phông chữ lớn cùng dự án.

- Lưu trữ các chuỗi bản địa hóa bằng :ref:`CSV <doc_internationalizing_games>` hoặc :ref:`gettext <doc_localization_using_gettext>`.

  - Hỗ trợ tạo các tệp gettext POT và PO từ trình chỉnh sửa.

- Tự động sử dụng các chuỗi đã bản địa hóa trong dự án của bạn trong các phần tử GUI hoặc bằng cách sử dụng hàm ``tr()``. - Hỗ trợ số nhiều và ngữ cảnh dịch. - Hỗ trợ :ref:`bidirectional typesetting <doc_internationalizing_games_bidi>`, định hình văn bản và các dạng bản địa hóa OpenType. - Tự động phản chiếu giao diện người dùng cho các ngôn ngữ viết từ phải sang trái. - Hỗ trợ :ref:`pseudolocalization <doc_pseudolocalization>` để kiểm tra mức độ thân thiện với i18n của dự án.

Quản lý cửa sổ và tích hợp hệ điều hành
---------------------------------------

- Tạo nhiều cửa sổ độc lập trong một tiến trình duy nhất. - Di chuyển, thay đổi kích thước, thu nhỏ và phóng to các cửa sổ do dự án tạo ra. - Thay đổi tiêu đề và biểu tượng cửa sổ. - Tạo các cửa sổ trong suốt để sử dụng làm lớp phủ, với hỗ trợ cho phép chuột đi xuyên qua dựa trên đa giác. - Yêu cầu chú ý (sẽ khiến thanh tiêu đề nhấp nháy trên hầu hết các nền tảng). - Chế độ toàn màn hình.

   - Theo mặc định, sử dụng chế độ toàn màn hình không viền trên Windows để chuyển đổi alt-tab nhanh, nhưng có thể tùy chọn sử dụng chế độ toàn màn hình độc quyền để giảm độ trễ đầu vào.

- Cửa sổ không viền (toàn màn hình hoặc không toàn màn hình). - Giữ một cửa sổ luôn ở trên cùng. - Khiến một cửa sổ bỏ qua trạng thái lấy nét (hữu ích cho lớp phủ). - Khai báo một cửa sổ là cửa sổ bật lên (ẩn khỏi trình chuyển đổi tác vụ) hoặc độc quyền (ngăn tương tác với các cửa sổ khác trong cùng một tiến trình). - Hỗ trợ hộp thoại tệp gốc trên Windows, macOS, Linux và Android. - Hỗ trợ biểu tượng khay hệ thống trên Windows và macOS. - Tích hợp menu toàn cục trên macOS. - Trang trí phía máy khách trên macOS. - Thực thi lệnh theo cách chặn hoặc không chặn (bao gồm chạy nhiều thực thể của cùng một dự án). - Mở đường dẫn tệp và URL bằng trình xử lý giao thức mặc định hoặc tùy chỉnh (nếu đã được đăng ký trên hệ thống). - Phân tích các đối số dòng lệnh tùy chỉnh. - Hỗ trợ trình đọc màn hình trên Windows, macOS và Linux. - Bất kỳ tệp nhị phân Godot nào (trình chỉnh sửa hoặc dự án đã xuất) đều có thể
  :ref:`used as a headless server <doc_exporting_for_dedicated_servers>`
  bằng cách khởi động với đối số dòng lệnh ``--headless``. Điều này cho phép chạy engine mà không cần GPU hoặc máy chủ hiển thị.

.. seealso::

    Xem :ref:`doc_creating_applications` để biết chi tiết về cách sử dụng các tính năng này.

Di động
-------

- :ref:`Virtual joystick <class_VirtualJoystick>` và :ref:`buttons <class_TouchScreenButton>` cho đầu vào cảm ứng. - Mua hàng trong ứng dụng trên :ref:`Android <doc_android_in_app_purchases>` và `iOS <https://github.com/godot-sdk-integrations/godot-storekit2>`_. - Hỗ trợ quảng cáo bằng các mô-đun của bên thứ ba. - Hỗ trợ chế độ hình trong hình trên Android.

.. _doc_xr_support:

Hỗ trợ XR (AR và VR)
--------------------

- Hỗ trợ tai nghe thực tế ảo dành cho máy tính để bàn bằng :ref:`OpenXR <doc_setting_up_xr>`. Nếu một tai nghe hoạt động với SteamVR, nó sẽ hoạt động với Godot.

   - Godot cũng hỗ trợ Quest qua Link, AndroidXR Direct Preview và Pico Connect.

- Hỗ trợ :ref:`Android-based headsets <doc_deploying_to_android>` bằng OpenXR. Bao gồm hỗ trợ cho các tai nghe độc lập sau:

   - Meta Quest 1/2/3 và Pro - Pico 4/4 Ultra - Magic Leap 2 - Lynx R1 - HTC Vive Focus Vision - Tai nghe Android XR

- Hỗ trợ Steam Frame độc lập dựa trên Linux bằng OpenXR.

- Hỗ trợ hạn chế cho tai nghe visionOS của Apple.

  - Hiện tại, chỉ hỗ trợ xuất một ứng dụng để sử dụng trên một mặt phẳng phẳng bên trong tai nghe. Không hỗ trợ các trải nghiệm nhập vai.

- Các thiết bị khác được hỗ trợ thông qua cấu trúc plugin XR. - Có nhiều bộ công cụ nâng cao triển khai các tính năng phổ biến cần thiết cho ứng dụng XR.

Hệ thống GUI
------------

GUI của Godot được xây dựng bằng chính các nút Control được sử dụng để tạo trò chơi trong Godot. Có thể dễ dàng mở rộng giao diện người dùng của trình chỉnh sửa theo nhiều cách bằng các tiện ích bổ sung.

**Các nút:**

- Nút. - Hộp kiểm, nút kiểm, nút radio. - Nhập văn bản bằng :ref:`class_LineEdit` (một dòng), :ref:`class_TextEdit` (nhiều dòng) và :ref:`class_CodeEdit` (hỗ trợ tô sáng cú pháp, số dòng và nhiều tính năng khác). - Menu thả xuống bằng :ref:`class_PopupMenu` và :ref:`class_OptionButton`, có hỗ trợ thanh tìm kiếm tùy chọn. - Thanh cuộn. - Nhãn. - RichTextLabel cho :ref:`text formatted using BBCode <doc_bbcode_in_richtextlabel>`, có hỗ trợ các hiệu ứng tùy chỉnh động. - Cây (cũng có thể được dùng để biểu diễn bảng). - Bộ chọn màu với các chế độ RGB, HSV và OKHSL, cùng các bảng màu tùy chỉnh. - Có thể xoay và thay đổi tỷ lệ các Control. - Hỗ trợ kéo và thả.

**Kích thước:**

- Neo để giữ các phần tử GUI ở một góc, cạnh cụ thể hoặc ở giữa. - Container để tự động đặt các phần tử GUI theo những quy tắc nhất định.

   - Bố cục :ref:`Stack <class_BoxContainer>`. - Bố cục :ref:`Grid <class_GridContainer>`. - Bố cục :ref:`Flow <class_FlowContainer>` (tương tự như văn bản tự động xuống dòng). - Bố cục :ref:`Margin <class_MarginContainer>`, :ref:`centered <class_CenterContainer>` và :ref:`aspect ratio <class_AspectRatioContainer>`. - Bố cục :ref:`Draggable splitter <class_SplitContainer>`. - Bố cục :ref:`Foldable section <class_FoldableContainer>`.

- Thu phóng thành :ref:`multiple resolutions <doc_multiple_resolutions>` bằng các chế độ co giãn ``canvas_items`` hoặc ``viewport``. - Hỗ trợ mọi tỷ lệ khung hình bằng các neo và khía cạnh co giãn ``expand``.

**Chủ đề:**

- Trình chỉnh sửa chủ đề tích hợp sẵn.

   - Tạo một chủ đề dựa trên các thiết lập chủ đề hiện tại của trình chỉnh sửa.

- Tạo chủ đề vector theo thủ tục bằng :ref:`class_StyleBoxFlat`.

   - Hỗ trợ các góc bo/vát, bóng đổ, độ rộng từng viền và khử răng cưa.

- Tạo chủ đề dựa trên kết cấu bằng :ref:`class_StyleBoxTexture`.

Kích thước phân phối nhỏ của Godot khiến nó trở thành một lựa chọn phù hợp thay cho các framework như Electron hoặc Qt.

Hoạt ảnh
--------

- Động học thuận và động học nghịch. - Hỗ trợ tạo hoạt ảnh cho mọi thuộc tính với nội suy có thể tùy chỉnh. - Hỗ trợ gọi các phương thức trong các track hoạt ảnh. - Hỗ trợ phát âm thanh trong các track hoạt ảnh. - Hỗ trợ các đường cong Bézier trong hoạt ảnh.

Định dạng tệp
-------------

- Các cảnh và tài nguyên có thể được lưu ở định dạng :ref:`text-based <doc_tscn_file_format>` hoặc định dạng nhị phân.

   - Các định dạng dựa trên văn bản có thể đọc được đối với con người và thân thiện hơn với việc kiểm soát phiên bản. - Định dạng nhị phân lưu/tải nhanh hơn đối với các cảnh/tài nguyên lớn.

- Đọc và ghi tệp văn bản hoặc tệp nhị phân bằng :ref:`class_FileAccess`.

   - Có thể được nén hoặc mã hóa tùy chọn.

- Đọc và ghi tệp :ref:`class_JSON`. - Đọc và ghi các tệp cấu hình kiểu INI bằng :ref:`class_ConfigFile`.

   - Có thể tuần tự hóa (giải tuần tự hóa) mọi kiểu dữ liệu Godot, bao gồm Vector2/3, Color, ...

- Đọc tệp XML bằng :ref:`class_XMLParser`. - :ref:`Load and save images, audio/video, fonts and ZIP archives <doc_runtime_loading_and_saving>` trong một dự án đã xuất mà không cần đi qua hệ thống nhập của Godot. - Đóng gói dữ liệu trò chơi vào tệp PCK (định dạng tùy chỉnh được tối ưu hóa để tìm kiếm nhanh), vào kho lưu trữ ZIP hoặc trực tiếp vào tệp thực thi để phân phối dưới dạng một tệp duy nhất. - :ref:`Export additional PCK files<doc_exporting_pcks>` có thể được engine đọc để hỗ trợ mod và DLC.

Khác
----

- :ref:`Video playback <doc_playing_videos>` với hỗ trợ Ogg Theora tích hợp sẵn. - :ref:`Movie Maker mode <doc_creating_movies>` để ghi video từ một dự án đang chạy với âm thanh được đồng bộ hóa và tốc độ khung hình hoàn hảo. - :ref:`Low-level access to servers <doc_using_servers>`, cho phép bỏ qua phần chi phí của cây cảnh khi cần. - :ref:`Command line interface <doc_command_line_tutorial>` cho tự động hóa.

   - Xuất và triển khai dự án bằng các nền tảng tích hợp liên tục. - `Các tập lệnh hoàn thành Shell <https://github.com/godotengine/godot/tree/master/misc/dist/shell>`__ có sẵn cho Bash, zsh và fish. - In văn bản có màu ra đầu ra tiêu chuẩn trên tất cả các nền tảng bằng
     :ref:`print_rich <class_@GlobalScope_method_print_rich>`.

- Trình chỉnh sửa có thể
  :ref:`detect features used in a project and create a compilation profile <doc_engine_compilation_configuration_editor>`,
  cho phép tạo các tệp nhị phân mẫu xuất nhỏ hơn bằng cách tắt các tính năng không cần thiết. - Hỗ trợ :ref:`C++ modules <doc_custom_modules_in_cpp>` được liên kết tĩnh vào tệp nhị phân của engine.

  - Hầu hết các mô-đun tích hợp sẵn có thể được vô hiệu hóa tại thời điểm biên dịch để giảm kích thước tệp nhị phân trong các bản dựng tùy chỉnh. Xem :ref:`doc_optimizing_for_size` để biết chi tiết.

- Engine và trình chỉnh sửa được viết bằng C++17.

   - Có thể được :ref:`compiled <doc_introduction_to_the_buildsystem>` bằng GCC, Clang và MSVC. MinGW cũng được hỗ trợ. - Thân thiện với các nhà đóng gói. Trong hầu hết trường hợp, có thể sử dụng các thư viện hệ thống thay cho những thư viện do Godot cung cấp. Hệ thống xây dựng không tải xuống bất kỳ thứ gì. Các bản dựng có thể được tái tạo hoàn toàn.

- Được cấp phép theo giấy phép MIT cho phép sử dụng rộng rãi.

   - Quy trình phát triển mở với `hoan nghênh đóng góp <https://contributing.godotengine.org/en/latest/organization/how_to_contribute.html>`__.

.. seealso::

    `Kho lưu trữ đề xuất Godot <https://github.com/godotengine/godot-proposals>`__ liệt kê các tính năng đã được cộng đồng yêu cầu và có thể được triển khai trong các bản phát hành Godot trong tương lai.
