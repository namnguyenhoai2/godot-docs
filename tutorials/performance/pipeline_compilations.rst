.. _doc_pipeline_compilations:

Giảm hiện tượng giật hình do biên dịch shader (pipeline)
========================================================

.. warning::

    Trang này chỉ áp dụng cho các renderer Forward+ và Mobile, không áp dụng cho Compatibility. Ubershader và pipeline precompilation phụ thuộc vào các chức năng chỉ có trong những graphics API cấp thấp hiện đại (Vulkan, Direct3D 12, Metal). Renderer Compatibility sử dụng OpenGL 3.3, OpenGL ES 3.0 hoặc WebGL 2.0 tùy theo nền tảng. Các phiên bản này thiếu chức năng cần thiết để triển khai hiệu quả ubershader và pipeline precompilation.

    Để tránh hiện tượng giật shader trong Compatibility, bạn cần sử dụng phương pháp cũ là preload material, shader và particle bằng cách hiển thị chúng trong ít nhất một frame bên trong view frustum khi level đang được tải.

Biên dịch pipeline, còn thường được gọi là biên dịch shader, là một thao tác tốn nhiều tài nguyên mà engine cần thực hiện để GPU có thể vẽ bất kỳ loại nội dung nào.

.. figure:: img/pipeline_compilations_shader_compilation_diagram.webp
   :align: center
   :alt: Sơ đồ thể hiện toàn bộ quy trình biên dịch shader: VisualShader và Standard Material đến Godot Shading Language, rồi đến GLSL, Intermediate Format (SPIR-V), và cuối cùng là Pipeline. Shader Compilation là bước từ GLSL đến Intermediate Format. Pipeline Compilation là bước từ Intermediate Format đến Pipeline.

   Shader và material trong Godot phải trải qua một số bước trước khi có thể được GPU chạy.

Nói chính xác hơn, *biên dịch shader* bao gồm việc chuyển đổi mã GLSL mà Godot tạo ra thành một định dạng trung gian có thể được chia sẻ giữa các hệ thống (chẳng hạn như SPIR-V khi sử dụng Vulkan). Tuy nhiên, GPU không thể sử dụng trực tiếp định dạng này.

*Biên dịch pipeline* là bước mà driver GPU chuyển đổi định dạng shader trung gian (kết quả của quá trình biên dịch shader) thành thứ mà GPU thực sự có thể sử dụng để render. Driver thường lưu một cache các pipeline ở đâu đó trong hệ thống để tránh lặp lại quy trình này mỗi lần game được chạy. Cache này thường bị xóa khi driver được cập nhật.

Pipeline chứa nhiều thông tin hơn chỉ riêng mã shader, nghĩa là mỗi shader có thể có hàng chục pipeline hoặc nhiều hơn! Điều này khiến engine khó biên dịch chúng trước, vừa vì quá trình này sẽ rất chậm, vừa vì nó sẽ chiếm nhiều bộ nhớ. Ngoài ra, bước này chỉ có thể được thực hiện trên hệ thống của người dùng và rất khó chia sẻ kết quả giữa những người dùng, trừ khi họ có phần cứng và phiên bản driver hoàn toàn giống nhau.

Trước Godot 4.4, không có giải pháp nào cho việc biên dịch pipeline ngoài việc tạo chúng khi một đối tượng xuất hiện trong vùng nhìn của camera, dẫn đến *hiện tượng giật shader* hoặc khựng hình tai tiếng chỉ xảy ra trong lần chơi đầu tiên. **Với Godot 4.4, các cơ chế mới đã được giới thiệu để giảm hiện tượng giật do biên dịch pipeline.**

- **Ubershader**: Godot sử dụng specialization constant, một tính năng cho phép driver tối ưu mã của pipeline dựa trên một tập tham số như ánh sáng, chất lượng bóng, v.v. Specialization constant được dùng để tối ưu shader bằng cách loại bỏ các tính năng không cần thiết. Việc thay đổi một specialization constant yêu cầu biên dịch lại pipeline. Ubershader là một phiên bản đặc biệt của shader, có khả năng thay đổi các constant này trong khi render, nghĩa là Godot chỉ cần precompile trước một pipeline và biên dịch các phiên bản được tối ưu hơn ở background trong khi chơi game. Điều này làm giảm đáng kể số lượng pipeline cần được tạo.
- **Pipeline precompilation**: Bằng cách sử dụng ubershader, engine có thể precompile pipeline trước tại nhiều thời điểm, chẳng hạn như khi mesh được tải hoặc khi node được thêm vào scene. Vì là một phần của quá trình tải resource, pipeline thậm chí có thể được precompile trên nhiều background thread nếu có thể trong màn hình loading hoặc ngay cả khi đang chơi game.

Bắt đầu từ Godot 4.4, Godot sẽ phát hiện những pipeline cần thiết và precompile chúng tại thời điểm load. Hệ thống phát hiện này phần lớn là tự động, nhưng phụ thuộc vào việc RenderingServer nhìn thấy bằng chứng về tất cả shader, mesh hoặc tính năng render tại thời điểm load. Ví dụ, nếu bạn load một mesh và shader trong khi game đang chạy, pipeline cho tổ hợp mesh/shader đó sẽ không được biên dịch cho đến khi mesh/shader được load. Tương tự, những việc như bật MSAA hoặc tạo instance của một node VoxelGI trong khi game đang chạy sẽ kích hoạt việc biên dịch lại pipeline.

Các monitor pipeline precompilation
-----------------------------------

.. UPDATE: Future versions mentioned.

Biên dịch pipeline trước là cơ chế chính mà Godot sử dụng để giảm hiện tượng giật shader, nhưng đây không phải là giải pháp hoàn hảo. Nhận biết những tình huống có thể dẫn đến giật pipeline sẽ rất hữu ích, và các cách khắc phục cũng khá đơn giản so với những phiên bản trước. Những cách khắc phục này có thể sẽ ngày càng ít cần thiết hơn trong các phiên bản Godot tương lai khi có thêm nhiều kỹ thuật phát hiện được triển khai.

Godot debugger cung cấp các monitor để theo dõi số lượng pipeline được game tạo ra và bước đã kích hoạt quá trình biên dịch chúng. Bạn có thể theo dõi các monitor này khi game chạy để xác định những nguồn có thể gây giật shader mà không cần xóa cache của driver mỗi lần muốn kiểm thử. Việc các giá trị này tăng đột ngột bên ngoài màn hình loading có thể xuất hiện dưới dạng khựng hình trong quá trình chơi, lần đầu một người chơi game trên hệ thống của họ. **Bạn nên xem các monitor này để xác định những nguồn có thể gây giật cho người chơi**, vì bạn có thể không tự trải nghiệm được chúng nếu không xóa cache của driver hoặc kiểm thử trên một hệ thống yếu hơn.

.. figure:: img/pipeline_compilations_monitors.webp
   :align: center
   :alt: Ảnh chụp màn hình monitor pipeline compilations của Godot

   Pipeline compilations của một trong các dự án demo.

.. note:: Chúng ta có thể thấy các pipeline được biên dịch trong khi chơi game và xác minh những bước nào có thể gây giật. Lưu ý rằng các giá trị này chỉ tăng và không bao giờ giảm, vì những pipeline đã bị xóa không được các monitor này theo dõi, đồng thời pipeline có thể bị xóa và tạo lại trong khi chơi game.

- **Canvas**: Được biên dịch khi vẽ một node 2D. Hiện tại engine chưa có chức năng precompile cho các phần tử 2D, vì vậy hiện tượng giật sẽ xuất hiện khi node 2D được vẽ lần đầu.
- **Mesh**: Được biên dịch trong quá trình load mesh 3D và xác định những pipeline nào có thể được precompile từ các thuộc tính của mesh. Những pipeline này có thể gây giật nếu mesh được load trong khi chơi game, nhưng có thể giảm thiểu hiện tượng này nếu mesh được load bằng background thread. **Các modifier thuộc về những node như material override không thể được biên dịch ở bước này**.
- **Surface**: Được biên dịch khi một frame sắp được vẽ và các đối tượng 3D lần đầu được tạo instance trong scene tree. Việc này cũng có thể bao gồm biên dịch cho những node thậm chí không hiển thị trong scene tree. Hiện tượng giật chỉ xảy ra ở frame đầu tiên khi node được thêm vào scene, nên sẽ không gây giật rõ rệt nếu xảy ra ngay sau màn hình loading.
- **Draw**: Được biên dịch theo yêu cầu khi cần vẽ một đối tượng 3D và ubershader chưa được biên dịch trước. Engine không thể biên dịch trước pipeline này do gặp một trường hợp chưa được xử lý hoặc do có thay đổi trong mã nguồn của engine. Điều này gây ra hiện tượng giật hình trong khi chơi. Đây là hành vi giống hệt các phiên bản Godot trước 4.4. Nếu bạn thấy có lượt biên dịch ở đây, vui lòng `cho các nhà phát triển biết <https://github.com/godotengine/godot/issues>`__ vì điều này không bao giờ được xảy ra với hệ thống Ubershader. Khi thực hiện, hãy nhớ đính kèm một dự án tái hiện tối giản.
- **Specialization**: Được biên dịch trong nền khi đang chơi để tối ưu tốc độ khung hình. Không gây giật hình, nhưng có thể làm giảm tốc độ khung hình nếu có nhiều lượt biên dịch diễn ra trong mỗi khung hình.

Các tính năng biên dịch trước pipeline
--------------------------------------

Godot cung cấp nhiều tính năng kết xuất không nhất thiết được mọi game sử dụng. Đáng tiếc là việc biên dịch trước pipeline không thể biết trước một tính năng cụ thể có được dự án sử dụng hay không. Một số tính năng chỉ có thể được phát hiện khi người dùng thêm một node vào scene hoặc bật một tùy chọn cụ thể trong dự án hay môi trường. Hệ thống biên dịch trước pipeline sẽ theo dõi các tính năng này khi chúng được gặp lần đầu và bật việc biên dịch trước cho mọi mesh hoặc surface được tạo sau đó.

Nếu game của bạn sử dụng các tính năng này, **hãy đảm bảo có một scene sử dụng chúng từ sớm nhất có thể** trước khi tải phần lớn asset. Scene này có thể rất đơn giản và sẽ hoạt động miễn là nó sử dụng các tính năng mà game dự định sử dụng. Nếu cần, scene thậm chí có thể được kết xuất ngoài màn hình trong ít nhất một khung hình, chẳng hạn bằng cách phủ nó bằng một :ref:`class_ColorRect` node hoặc sử dụng một :ref:`class_SubViewport` nằm ngoài giới hạn cửa sổ.

Bạn cũng nên lưu ý rằng việc thay đổi bất kỳ tính năng nào trong số này khi đang chơi sẽ gây ra hiện tượng giật hình ngay lập tức. Chỉ thay đổi các tính năng này từ màn hình cấu hình khi cần thiết, đồng thời chèn màn hình tải và thông báo khi áp dụng các thay đổi.

- **MSAA Level**: Được bật khi mức 3D MSAA được thay đổi trong cài đặt dự án. Đáng tiếc là việc sử dụng các mức MSAA khác nhau trên các viewport khác nhau sẽ gây giật hình, vì engine chỉ theo dõi một mức tại một thời điểm để thực hiện biên dịch trước.
- **Reflection Probes**: Được bật khi một node ReflectionProbe được đặt vào scene.
- **Separate Specular**: Được bật khi sử dụng các hiệu ứng như tán xạ dưới bề mặt hoặc hiệu ứng compositor dựa trên việc lấy mẫu trực tiếp độ specular từ màn hình.
- **Motion Vectors**: Được bật khi sử dụng các hiệu ứng như TAA, FSR2 hoặc hiệu ứng compositor yêu cầu motion vector (chẳng hạn như motion blur).
- **Normal and Roughness**: Được bật khi sử dụng SDFGI, VoxelGI, phản xạ không gian màn hình, SSAO, SSIL hoặc sử dụng ``normal_roughness_buffer`` trong custom shader hay :ref:`class_CompositorEffect`.
- **Lightmaps**: Được bật khi một node LightmapGI được đặt vào scene và một node sử dụng lightmap đã bake.
- **VoxelGI**: Được bật khi một node VoxelGI được đặt vào scene.
- **SDFGI**: Được bật khi WorldEnvironment bật SDFGI.
- **Multiview**: Được bật cho các dự án XR.
- **16/32-bit Shadows**: Được bật khi cấu hình độ chính xác độ sâu của shadowmap được thay đổi trong cài đặt dự án.
- **Omni Shadow Dual Paraboloid**: Được bật khi đèn omni đổ bóng và sử dụng chế độ dual paraboloid.
- **Omni Shadow Cubemap**: Được bật khi đèn omni đổ bóng và sử dụng chế độ cubemap (đây là chế độ mặc định).

Nếu bạn thấy hiện tượng giật hình trong khi chơi và các trình theo dõi báo cáo số lượt biên dịch tăng đột ngột trong bước **Surface**, rất có thể một tính năng đã chưa được bật trước đó. Đảm bảo hiệu ứng này được bật trong khi tải game có thể sẽ giảm thiểu vấn đề.

Khởi tạo instance khi biên dịch trước pipeline
----------------------------------------------

Một nguyên nhân phổ biến gây giật hình trong game là một số hiệu ứng chỉ được khởi tạo instance trong scene do những tương tác chỉ xảy ra khi đang chơi. Ví dụ: một hiệu ứng particle chỉ được thêm vào scene thông qua script khi người chơi thực hiện một hành động. Ngay cả khi scene đã được preload, engine vẫn có thể không biên dịch trước được các pipeline cho đến khi hiệu ứng được thêm vào scene ít nhất một lần.

May mắn là từ Godot 4.4 trở lên, bạn có thể biên dịch trước các pipeline này miễn là scene được khởi tạo instance ít nhất một lần trong scene, ngay cả khi nó hoàn toàn vô hình hoặc nằm ngoài tầm nhìn của camera.

.. figure:: img/pipeline_compilations_hidden_node.webp
   :align: center
   :alt: Ảnh chụp màn hình ví dụ về một Node ẩn cho một hiệu ứng

   Node đạn ẩn được gắn vào người chơi trong một trong các dự án demo. Điều này giúp engine biên dịch trước các pipeline của hiệu ứng.

Nếu bạn biết có hiệu ứng nào được thêm động vào scene trong khi chơi và thấy số lượt biên dịch tăng đột ngột trên trình theo dõi khi các hiệu ứng này xuất hiện, một giải pháp tạm thời là gắn một phiên bản ẩn của hiệu ứng vào một vị trí chắc chắn sẽ xuất hiện.

Ví dụ, nếu nhân vật người chơi có thể gây ra một vụ nổ, bạn có thể gắn hiệu ứng này làm node con của người chơi dưới dạng một node vô hình. Hãy đảm bảo tắt script được gắn vào node ẩn hoặc ẩn mọi node khác có thể gây ra vấn đề. Bạn có thể thực hiện việc này bằng cách bật **Editable Children** trên node.

.. _doc_pipeline_compilations_shader_baker:

Shader baker
------------

Từ Godot 4.5, bạn có thể chọn bake shader khi export để cải thiện thời gian khởi động ban đầu. Điều này nhìn chung sẽ không giải quyết các hiện tượng giật hình hiện có, nhưng sẽ giảm thời gian cần để tải game lần đầu. Điều này đặc biệt đúng khi sử dụng Direct3D 12 hoặc Metal, vốn có thời gian biên dịch shader ban đầu chậm hơn đáng kể so với Vulkan do bước chuyển đổi cần thiết. Shader của Godot sử dụng GLSL và SPIR-V, còn Direct3D 12 và Metal sử dụng các định dạng khác.

.. note::

    Shader baker chỉ có thể bake mã nguồn thành định dạng trung gian (SPIR-V cho Vulkan, DXIL cho Direct3D 12, MIL cho Metal). Nó không thể bake định dạng trung gian thành pipeline cuối cùng, vì việc này phụ thuộc vào driver GPU và phần cứng.

    Shader baker không thay thế cho việc biên dịch trước pipeline, mà nhằm bổ trợ cho tính năng này.

Khi được bật, shader baker sẽ đóng gói mã shader đã biên dịch vào PCK, nhờ đó hoàn toàn bỏ qua bước biên dịch shader. Nhược điểm là quá trình export sẽ mất nhiều thời gian hơn một chút. Tệp PCK sẽ lớn hơn vài megabyte.

Shader baker bị tắt theo mặc định, nhưng bạn có thể bật tính năng này trong từng export preset trong hộp thoại Export bằng cách đánh dấu tùy chọn export :ui:`Shader Baker > Enabled`.

Lưu ý rằng việc bake shader chỉ có thể xuất shader cho các driver được nền tảng mà editor hiện đang chạy hỗ trợ:

- Editor chạy trên Windows có thể xuất shader cho Vulkan và Direct3D 12.
- Editor chạy trên macOS có thể xuất shader cho Vulkan và Metal.
- Editor chạy trên Linux chỉ có thể xuất shader cho Vulkan.
- Editor chạy trên Android chỉ có thể xuất shader cho Vulkan.

Công cụ bake shader chỉ xuất các shader khớp với thiết lập project ``rendering/rendering_device/driver`` cho nền tảng đích.

.. note::

    Công cụ bake shader chỉ được hỗ trợ cho các renderer Forward+ và Mobile. Công cụ này sẽ không có tác dụng nếu project sử dụng renderer Compatibility hoặc đối với những người dùng sử dụng cơ chế dự phòng Compatibility vì phần cứng của họ không hỗ trợ renderer Forward+ hoặc Mobile.

    Điều này cũng có nghĩa là công cụ bake shader không được hỗ trợ trên nền tảng web, vì nền tảng web chỉ hỗ trợ renderer Compatibility.

    Ngoài ra, công cụ bake shader không được hỗ trợ khi xuất project bằng ``--headless`` :ref:`đối số dòng lệnh <doc_command_line_tutorial>`, vì Godot không thể truy cập GPU khi chạy ở chế độ headless.
