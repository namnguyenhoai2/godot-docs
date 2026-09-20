.. _doc_pipeline_compilations:

Giảm hiện tượng giật hình do biên dịch shader (pipeline)
========================================================

.. warning::

    Trang này chỉ áp dụng cho renderer Forward+ và Mobile, không áp dụng cho Compatibility. Ubershader và pipeline precompilation dựa vào các chức năng chỉ có trong những graphics API cấp thấp hiện đại (Vulkan, Direct3D 12, Metal). Renderer Compatibility sử dụng OpenGL 3.3, OpenGL ES 3.0 hoặc WebGL 2.0 tùy theo nền tảng. Những phiên bản này thiếu chức năng để triển khai ubershader và pipeline precompilation một cách hiệu quả.

    Để tránh hiện tượng giật shader trong Compatibility, bạn cần sử dụng phương pháp cũ là preload material, shader và particle bằng cách hiển thị chúng trong view frustum ít nhất một frame khi level đang được load.

Biên dịch pipeline, còn thường được gọi là biên dịch shader, là một thao tác tốn tài nguyên mà engine cần thực hiện để có thể vẽ bất kỳ loại nội dung nào bằng GPU.

.. figure:: img/pipeline_compilations_shader_compilation_diagram.webp
   :align: center
   :alt: Flowchart showing the entire compilation process for a shader: VisualShader and Standard Material to Godot Shading Language to GLSL to Intermediate Format (SPIR-V) to Pipeline. Shader Compilation is the GLSL to Intermediate Format step. Pipeline Compilation is the Intermediate Format to Pipeline step.

   Shaders and materials in Godot go through several steps before they can be run
   by the GPU.

Nói chính xác hơn, *biên dịch shader* bao gồm việc chuyển đổi mã GLSL do Godot tạo ra thành một định dạng trung gian có thể được chia sẻ giữa các hệ thống (chẳng hạn như SPIR-V khi sử dụng Vulkan). Tuy nhiên, GPU không thể sử dụng trực tiếp định dạng này.

*Biên dịch pipeline* là bước mà driver GPU chuyển đổi định dạng shader trung gian (kết quả của quá trình biên dịch shader) thành thứ mà GPU thực sự có thể sử dụng để render. Driver thường lưu một cache các pipeline ở đâu đó trong hệ thống để tránh lặp lại quá trình này mỗi khi game được chạy. Cache này thường bị xóa khi driver được cập nhật.

Pipeline chứa nhiều thông tin hơn chỉ riêng mã shader, nghĩa là với mỗi shader, có thể có hàng chục pipeline hoặc nhiều hơn! Điều này khiến engine khó biên dịch chúng trước, vì quá trình này vừa rất chậm vừa chiếm nhiều bộ nhớ. Ngoài ra, bước này chỉ có thể được thực hiện trên hệ thống của người dùng và rất khó chia sẻ kết quả giữa những người dùng, trừ khi họ có chính xác cùng phần cứng và phiên bản driver.

Trước Godot 4.4, không có giải pháp nào cho việc biên dịch pipeline ngoài việc tạo chúng khi một object xuất hiện bên trong vùng nhìn của camera, dẫn đến hiện tượng *shader stutter* hoặc hitch nổi tiếng, chỉ xảy ra trong lần chơi đầu tiên. **Với Godot 4.4, các cơ chế mới đã được giới thiệu để giảm hiện tượng giật do biên dịch pipeline.**

- **Ubershader**: Godot sử dụng specialization constant, một tính năng cho phép driver tối ưu mã của pipeline dựa trên một tập hợp tham số như ánh sáng, chất lượng bóng đổ, v.v. Specialization constant được sử dụng để tối ưu shader bằng cách giới hạn các tính năng không cần thiết. Việc thay đổi một specialization constant yêu cầu biên dịch lại pipeline. Ubershader là một phiên bản đặc biệt của shader, có khả năng thay đổi các constant này trong khi render, nghĩa là Godot có thể biên dịch trước chỉ một pipeline và biên dịch các phiên bản được tối ưu hơn ở background trong khi chơi game. Điều này làm giảm đáng kể số lượng pipeline cần được tạo. - **Pipeline precompilation**: Bằng cách sử dụng ubershader, engine có thể biên dịch trước pipeline tại nhiều thời điểm, chẳng hạn như khi mesh được load hoặc khi node được thêm vào scene. Vì là một phần của quá trình load resource, pipeline thậm chí có thể được biên dịch trước trong nhiều background thread nếu có thể, trong màn hình loading hoặc ngay cả khi đang chơi game.

Bắt đầu từ Godot 4.4, Godot sẽ phát hiện những pipeline cần thiết và biên dịch trước chúng trong thời gian load. Hệ thống phát hiện này phần lớn là tự động, nhưng dựa vào việc RenderingServer nhìn thấy bằng chứng về tất cả shader, mesh hoặc tính năng rendering trong thời gian load. Ví dụ, nếu bạn load một mesh và shader trong khi game đang chạy, pipeline cho tổ hợp mesh/shader đó sẽ chỉ được biên dịch sau khi mesh/shader được load. Tương tự, những thao tác như bật MSAA hoặc instance một node VoxelGI trong khi game đang chạy sẽ kích hoạt việc biên dịch lại pipeline.

Các monitor pipeline precompilation
-----------------------------------

.. CẬP NHẬT: Các phiên bản tương lai được đề cập.

Biên dịch pipeline trước là cơ chế chính mà Godot sử dụng để giảm hiện tượng giật shader, nhưng đây không phải là giải pháp hoàn hảo. Nhận biết những tình huống có thể dẫn đến hiện tượng giật pipeline sẽ rất hữu ích, và các giải pháp khắc phục khá đơn giản so với những phiên bản trước. Những giải pháp này có thể sẽ ít cần thiết hơn theo thời gian khi các phiên bản Godot tương lai triển khai thêm nhiều kỹ thuật phát hiện.

Godot debugger cung cấp các monitor để theo dõi số lượng pipeline được game tạo ra và bước đã kích hoạt quá trình biên dịch chúng. Bạn có thể theo dõi các monitor này khi game chạy để xác định các nguồn có thể gây giật shader mà không cần xóa driver cache mỗi lần muốn kiểm thử. Việc các giá trị này tăng đột ngột bên ngoài màn hình loading có thể xuất hiện dưới dạng hitch trong quá trình chơi, vào lần đầu tiên ai đó chơi game trên hệ thống của họ. **Bạn nên xem các monitor này để xác định những nguồn có thể gây giật cho người chơi**, vì bạn có thể không tự trải nghiệm được chúng nếu không xóa driver cache hoặc kiểm thử trên một hệ thống yếu hơn.

.. figure:: img/pipeline_compilations_monitors.webp
   :align: center
   :alt: Screenshot of the Godot pipeline compilations monitor

   Pipeline compilations of one of the demo projects.

.. note:: We can see the pipelines compiled during gameplay and
          xác minh những bước nào có thể gây giật. Lưu ý rằng các giá trị này chỉ tăng và không bao giờ giảm, vì các pipeline đã bị xóa không được những monitor này theo dõi, đồng thời pipeline có thể bị xóa và tạo lại trong quá trình chơi.

- **Canvas**: Được biên dịch khi vẽ một node 2D. Hiện tại engine chưa có tính năng precompilation cho các phần tử 2D, nên hiện tượng giật sẽ xuất hiện khi node 2D được vẽ lần đầu. - **Mesh**: Được biên dịch trong quá trình load một mesh 3D và xác định những pipeline nào có thể được biên dịch trước dựa trên các thuộc tính của mesh. Việc này có thể gây giật nếu mesh được load trong khi chơi, nhưng có thể giảm thiểu bằng cách load mesh bằng background thread. **Các modifier thuộc về node như material override không thể được biên dịch ở bước này**. - **Surface**: Được biên dịch khi một frame sắp được vẽ và các object 3D lần đầu được instance trong scene tree. Việc này cũng có thể bao gồm quá trình biên dịch cho các node thậm chí không hiển thị trong scene tree. Hiện tượng giật sẽ chỉ xảy ra ở frame đầu tiên node được thêm vào scene, nên sẽ không gây giật rõ rệt nếu diễn ra ngay sau màn hình loading. - **Draw**: Được biên dịch theo yêu cầu khi cần vẽ một object 3D và ubershader chưa được biên dịch trước. Engine không thể biên dịch trước pipeline này vì gặp một trường hợp chưa được xử lý hoặc một thay đổi đã được thực hiện trong mã của engine. Gây giật trong quá trình chơi. Điều này giống hệt các phiên bản Godot trước 4.4. Nếu bạn thấy có quá trình biên dịch ở đây, vui lòng `let the developers know <https://github.com/godotengine/godot/issues>`__ vì điều này không bao giờ được xảy ra với hệ thống Ubershader. Hãy nhớ đính kèm một project tái hiện tối thiểu khi thực hiện việc đó. - **Specialization**: Được biên dịch ở background trong quá trình chơi để tối ưu framerate. Không thể gây giật, nhưng có thể làm giảm framerate nếu có nhiều quá trình diễn ra trong mỗi frame.

Các tính năng pipeline precompilation
-------------------------------------

Godot cung cấp nhiều tính năng rendering không nhất thiết được mọi game sử dụng. Đáng tiếc là pipeline precompilation không thể biết trước một tính năng cụ thể có được project sử dụng hay không. Một số tính năng chỉ có thể được phát hiện khi người dùng thêm một node vào scene hoặc bật một thiết lập cụ thể trong project hay environment. Hệ thống pipeline precompilation sẽ theo dõi những tính năng này khi chúng được gặp lần đầu và bật precompilation cho chúng đối với mọi mesh hoặc surface được tạo sau đó.

Nếu game của bạn sử dụng những tính năng này, **hãy đảm bảo có một scene sử dụng chúng càng sớm càng tốt** trước khi load phần lớn asset. Scene này có thể rất đơn giản và vẫn hoàn thành nhiệm vụ, miễn là nó sử dụng các tính năng mà game dự định dùng. Nếu cần, scene thậm chí có thể được render ngoài màn hình trong ít nhất một frame, chẳng hạn bằng cách che nó bằng một node :ref:`class_ColorRect` hoặc sử dụng một :ref:`class_SubViewport` nằm bên ngoài phạm vi của cửa sổ.

Bạn cũng nên lưu ý rằng việc thay đổi bất kỳ tính năng nào trong số này trong quá trình chơi sẽ gây ra hiện tượng giật ngay lập tức. Nếu cần, hãy chỉ thay đổi các tính năng này từ các màn hình cấu hình và chèn màn hình loading cùng thông báo khi áp dụng các thay đổi.

- **MSAA Level**: Được bật khi cấp độ 3D MSAA được thay đổi trong cài đặt dự án. Đáng tiếc là việc sử dụng các cấp độ MSAA khác nhau trên các viewport khác nhau sẽ dẫn đến hiện tượng giật, vì engine chỉ theo dõi một cấp độ tại một thời điểm để thực hiện biên dịch trước. - **Reflection Probes**: Được bật khi một node ReflectionProbe được đặt trong scene. - **Separate Specular**: Được bật khi sử dụng các hiệu ứng như tán xạ dưới bề mặt hoặc hiệu ứng compositor dựa vào việc lấy mẫu độ specular trực tiếp từ màn hình. - **Motion Vectors**: Được bật khi sử dụng các hiệu ứng như TAA, FSR2 hoặc hiệu ứng compositor yêu cầu motion vector (chẳng hạn như motion blur). - **Normal and Roughness**: Được bật khi sử dụng SDFGI, VoxelGI, phản xạ không gian màn hình, SSAO, SSIL hoặc sử dụng ``normal_roughness_buffer`` trong shader tùy chỉnh hoặc :ref:`class_CompositorEffect`. - **Lightmaps**: Được bật khi một node LightmapGI được đặt trong scene và một node sử dụng lightmap đã bake. - **VoxelGI**: Được bật khi một node VoxelGI được đặt trong scene. - **SDFGI**: Được bật khi WorldEnvironment bật SDFGI. - **Multiview**: Được bật cho các dự án XR. - **16/32-bit Shadows**: Được bật khi cấu hình độ chính xác độ sâu của shadowmap được thay đổi trong cài đặt dự án. - **Omni Shadow Dual Paraboloid**: Được bật khi một đèn omni tạo bóng và sử dụng chế độ dual paraboloid. - **Omni Shadow Cubemap**: Được bật khi một đèn omni tạo bóng và sử dụng chế độ cubemap (đây là chế độ mặc định).

Nếu bạn nhận thấy hiện tượng giật trong khi chơi game và các màn hình giám sát báo số lượt biên dịch tăng đột ngột trong bước **Surface**, rất có thể một tính năng đã chưa được bật từ trước. Đảm bảo hiệu ứng này được bật trong khi tải game có thể sẽ giảm thiểu vấn đề.

Khởi tạo pipeline trước
-----------------------

Một nguồn gây giật phổ biến trong game là việc một số hiệu ứng chỉ được khởi tạo trong scene do các tương tác chỉ xảy ra trong khi chơi game. Ví dụ, bạn có một hiệu ứng particle chỉ được thêm vào scene thông qua một script khi người chơi thực hiện một hành động. Ngay cả khi scene đã được preload, engine có thể không thể biên dịch trước các pipeline cho đến khi hiệu ứng được thêm vào scene ít nhất một lần.

May mắn là từ Godot 4.4 trở lên, bạn có thể biên dịch trước các pipeline này miễn là scene được khởi tạo ít nhất một lần trong scene, ngay cả khi nó hoàn toàn không hiển thị hoặc nằm ngoài góc nhìn của camera.

.. figure:: img/pipeline_compilations_hidden_node.webp
   :align: center
   :alt: Screenshot of an example of a hidden Node for an effect

   Hidden bullet node attached to the player in one of the demo projects. This
   helps the engine precompile the effect's pipelines ahead of time.

Nếu bạn biết có hiệu ứng nào được thêm động vào scene trong khi chơi game và nhận thấy số lượt biên dịch tăng đột ngột trên màn hình giám sát khi các hiệu ứng này xuất hiện, một cách khắc phục tạm thời là gắn một phiên bản ẩn của hiệu ứng ở một vị trí chắc chắn sẽ xuất hiện.

Ví dụ, nếu nhân vật người chơi có thể gây ra một vụ nổ, bạn có thể gắn hiệu ứng đó làm node con của người chơi dưới dạng một node không hiển thị. Hãy đảm bảo tắt script được gắn vào node ẩn hoặc ẩn mọi node khác có thể gây ra vấn đề. Bạn có thể thực hiện việc này bằng cách bật **Editable Children** trên node.

.. _doc_pipeline_compilations_shader_baker:

Shader baker
------------

Kể từ Godot 4.5, bạn có thể chọn bake shader khi export để cải thiện thời gian khởi động ban đầu. Điều này thường không giải quyết các hiện tượng giật hiện có, nhưng sẽ giảm thời gian tải game trong lần đầu tiên. Điều này đặc biệt đúng khi sử dụng Direct3D 12 hoặc Metal, vốn có thời gian biên dịch shader ban đầu chậm hơn đáng kể so với Vulkan do cần thực hiện bước chuyển đổi. Các shader của Godot sử dụng GLSL và SPIR-V, nhưng Direct3D 12 và Metal sử dụng các định dạng khác.

.. note::

    Shader baker chỉ có thể bake mã nguồn thành định dạng trung gian (SPIR-V cho Vulkan, DXIL cho Direct3D 12, MIL cho Metal). Nó không thể bake định dạng trung gian thành pipeline cuối cùng, vì việc này phụ thuộc vào driver GPU và phần cứng.

    Shader baker không thay thế cho việc biên dịch trước pipeline, mà được thiết kế để bổ trợ cho việc này.

Khi được bật, shader baker sẽ đóng gói mã shader đã biên dịch vào PCK, nhờ đó hoàn toàn bỏ qua bước biên dịch shader. Nhược điểm là quá trình export sẽ mất thêm một chút thời gian. Tệp PCK sẽ lớn hơn vài megabyte.

Shader baker mặc định bị tắt, nhưng bạn có thể bật nó trong từng export preset của hộp thoại Export bằng cách đánh dấu tùy chọn export :ui:`Shader Baker > Enabled`.

Lưu ý rằng shader baking chỉ có thể export shader cho các driver được nền tảng mà editor hiện đang chạy hỗ trợ:

- Editor chạy trên Windows có thể export shader cho Vulkan và Direct3D 12. - Editor chạy trên macOS có thể export shader cho Vulkan và Metal. - Editor chạy trên Linux chỉ có thể export shader cho Vulkan. - Editor chạy trên Android chỉ có thể export shader cho Vulkan.

Shader baker chỉ export các shader khớp với cài đặt dự án ``rendering/rendering_device/driver`` cho nền tảng đích.

.. note::

    Shader baker chỉ được hỗ trợ cho các renderer Forward+ và Mobile. Nó sẽ không có tác dụng nếu dự án sử dụng renderer Compatibility hoặc đối với những người dùng sử dụng Compatibility fallback vì phần cứng của họ không hỗ trợ renderer Forward+ hoặc Mobile.

    Điều này cũng có nghĩa là shader baker không được hỗ trợ trên nền tảng web, vì nền tảng web chỉ hỗ trợ renderer Compatibility.

    Ngoài ra, shader baker không được hỗ trợ khi export dự án bằng ``--headless`` :ref:`command line argument <doc_command_line_tutorial>`, vì Godot không thể truy cập GPU khi chạy ở chế độ headless.
