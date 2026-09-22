.. _doc_internal_rendering_architecture:

Kiến trúc rendering nội bộ
==========================

Trang này là tổng quan cấp cao về thiết kế renderer nội bộ của Godot 4. Nội dung này không áp dụng cho các phiên bản Godot trước đây.

Mục tiêu của trang này là ghi lại các quyết định thiết kế nhằm phù hợp nhất với `triết lý thiết kế của Godot <https://contributing.godotengine.org/en/latest/development/engine/best_practices.html>`__, đồng thời cung cấp điểm khởi đầu cho những người đóng góp mới cho rendering.

Nếu bạn có câu hỏi về phần nội bộ của rendering chưa được giải đáp tại đây, hãy thoải mái hỏi trong kênh ``#rendering`` của `Godot Contributors Chat <https://chat.godotengine.org/channel/rendering>`__.

.. note::

    Nếu bạn gặp khó khăn khi hiểu các khái niệm trên trang này, bạn nên xem qua một tutorial về OpenGL, chẳng hạn như `LearnOpenGL <https://learnopengl.com/>`__.

    Các API cấp thấp hiện đại (Vulkan/Direct3D 12/Metal) yêu cầu kiến thức trung gian về các API cấp cao hơn (OpenGL/Direct3D 11) để có thể được sử dụng hiệu quả. May mắn là những người đóng góp hiếm khi cần làm việc trực tiếp với các API cấp thấp. Các renderer của Godot được xây dựng hoàn toàn trên OpenGL và RenderingDevice, đây là lớp abstraction của chúng tôi trên Vulkan/Direct3D 12/Metal.

.. _doc_internal_rendering_architecture_methods:

Các phương thức rendering
-------------------------

Forward+
~~~~~~~~

Đây là một forward renderer sử dụng phương pháp chiếu sáng *clustered*.

Clustered lighting sử dụng compute shader để nhóm các nguồn sáng vào một lưới 3D được căn chỉnh theo frustum. Sau đó, tại thời điểm rendering, các pixel có thể tra cứu những nguồn sáng ảnh hưởng đến ô lưới chứa chúng và chỉ thực hiện tính toán ánh sáng cho những nguồn sáng có khả năng ảnh hưởng đến pixel đó.

Phương pháp này có thể tăng đáng kể hiệu năng rendering trên phần cứng desktop, nhưng kém hiệu quả hơn đáng kể trên mobile.

Mobile
~~~~~~

Đây là một forward renderer sử dụng phương pháp chiếu sáng single-pass truyền thống. Về mặt nội bộ, nó được gọi là **Forward Mobile**.

Được thiết kế cho các nền tảng mobile, nhưng cũng có thể chạy trên các nền tảng desktop. Phương thức rendering này được tối ưu để hoạt động tốt trên GPU mobile. GPU mobile có kiến trúc rất khác so với GPU desktop do những giới hạn riêng về mức sử dụng pin, nhiệt lượng và băng thông tổng thể khi đọc và ghi dữ liệu. Compute shader cũng có mức hỗ trợ rất hạn chế hoặc hoàn toàn không được hỗ trợ. Do đó, mobile renderer chỉ sử dụng các shader dựa trên raster (fragment/vertex).

Khác với GPU desktop, GPU mobile thực hiện *tile-based rendering*. Thay vì rendering toàn bộ hình ảnh như một đơn vị duy nhất, hình ảnh được chia thành các tile nhỏ hơn, vừa với bộ nhớ nội bộ nhanh hơn của GPU mobile. Mỗi tile được rendering rồi ghi ra destination texture. Tất cả quá trình này diễn ra tự động trong graphics driver.

Vấn đề là điều này tạo ra các điểm nghẽn trong phương pháp truyền thống của chúng ta. Đối với rendering trên desktop, chúng ta render toàn bộ geometry opaque, sau đó xử lý background, tiếp đến là geometry trong suốt, rồi post-processing. Mỗi pass sẽ cần đọc kết quả hiện tại vào tile memory, thực hiện các thao tác của mình rồi ghi kết quả ra lại. Sau đó, chúng ta phải chờ tất cả tile hoàn tất trước khi chuyển sang pass tiếp theo.

Thay đổi quan trọng đầu tiên trong mobile renderer là mobile renderer không sử dụng các texture format RGBA16F như desktop (Forward+) renderer. Thay vào đó, nó sử dụng texture format R10G10B10A2 UNORM, trừ khi
project setting :ref:`rendering/viewport/hdr_2d <class_ProjectSettings_property_rendering/viewport/hdr_2d>` được bật. Điều này giảm một nửa băng thông cần thiết và còn mang lại những cải thiện khác, vì phần cứng mobile thường tối ưu hơn nữa cho các format 32-bit. Đánh đổi là theo mặc định, mobile renderer có khả năng HDR hạn chế do độ chính xác và các giá trị tối đa trong dữ liệu màu bị giảm.

Khi project setting :ref:`rendering/viewport/hdr_2d <class_ProjectSettings_property_rendering/viewport/hdr_2d>` được bật, mobile renderer sử dụng các renderer RGBA16F giống như Forward+. Điều này cho phép hỗ trợ HDR đầy đủ, nhưng cũng làm tăng mức sử dụng băng thông và có thể làm giảm hiệu năng trên GPU mobile hoặc đồ họa tích hợp.

Thay đổi quan trọng thứ hai là sử dụng sub-pass bất cứ khi nào có thể. Sub-pass cho phép chúng ta thực hiện các bước rendering end-to-end trên từng tile, nhờ đó tiết kiệm overhead phát sinh do phải đọc từ và ghi vào các tile giữa mỗi rendering pass. Khả năng sử dụng sub-pass bị giới hạn bởi việc không thể đọc các pixel lân cận, vì chúng ta bị giới hạn trong phạm vi một tile duy nhất.

Hạn chế này của subpass khiến chúng ta không thể triển khai hiệu quả các tính năng như glow và depth of field. Tương tự, nếu cần đọc từ screen texture hoặc depth texture, chúng ta phải ghi toàn bộ kết quả rendering ra ngoài, làm hạn chế khả năng sử dụng sub-pass. Khi các tính năng như vậy được bật, sự kết hợp giữa sub-pass và pass thông thường sẽ được sử dụng, đồng thời các tính năng này gây ra mức phạt hiệu năng đáng kể.

Trên các nền tảng desktop, việc sử dụng sub-pass sẽ không ảnh hưởng đến hiệu năng. Tuy nhiên, phương thức rendering này vẫn có thể hoạt động tốt hơn Forward+ trong các scene đơn giản nhờ độ phức tạp thấp hơn và mức sử dụng băng thông thấp hơn. Điều này đặc biệt dễ nhận thấy trên các GPU cấp thấp, đồ họa tích hợp hoặc trong các ứng dụng VR.

Do tập trung vào phần cứng cấp thấp, phương thức rendering này không cung cấp các tính năng rendering cao cấp như SDFGI và :ref:`doc_volumetric_fog`. Một số hiệu ứng post-processing cũng không khả dụng.

.. _doc_internal_rendering_architecture_compatibility:

Compatibility
~~~~~~~~~~~~~

.. note::

    Đây là phương thức rendering duy nhất khả dụng khi sử dụng OpenGL driver. Phương thức rendering này không khả dụng khi sử dụng Vulkan, Direct3D 12 hoặc Metal.

Đây là một forward renderer truyền thống (không clustered). Về mặt nội bộ, nó được gọi là **GL Compatibility**. Phương thức này dành cho các GPU cũ không hỗ trợ Vulkan, nhưng vẫn hoạt động rất hiệu quả trên phần cứng mới hơn. Cụ thể, nó được tối ưu cho các thiết bị mobile cũ và cấp thấp hơn. Tuy nhiên, nhiều tối ưu hóa cũng áp dụng được cho desktop, khiến đây trở thành lựa chọn phù hợp cho các hệ thống desktop cũ và cấp thấp hơn.

Giống như Mobile renderer, Compatibility renderer sử dụng texture R10G10B10A2 UNORM cho rendering 3D. Khác với mobile renderer, màu sắc được tonemap và lưu ở format sRGB nên không hỗ trợ HDR. Điều này loại bỏ nhu cầu sử dụng một tonemapping pass và cho phép chúng ta dùng texture có số bit thấp hơn mà không bị banding đáng kể.

Compatibility renderer sử dụng phương pháp forward single-pass truyền thống để vẽ các object có nguồn sáng, nhưng sử dụng phương pháp multi-pass để vẽ các nguồn sáng có shadow. Cụ thể, trong pass đầu tiên, nó có thể vẽ nhiều nguồn sáng không có shadow và tối đa một DirectionalLight3D có shadow. Trong mỗi pass tiếp theo, nó có thể vẽ tối đa một OmniLight3D, một SpotLight3D và một DirectionalLight3D có shadow. Các nguồn sáng có shadow sẽ ảnh hưởng đến scene khác với các nguồn sáng không có shadow, vì ánh sáng được blend trong không gian sRGB thay vì không gian tuyến tính. Sự khác biệt về ánh sáng này sẽ ảnh hưởng đến diện mạo của scene và cần được lưu ý khi thiết kế scene cho Compatibility renderer.

Do tập trung vào phần cứng cấp thấp, phương thức rendering này không cung cấp các tính năng rendering cao cấp (thậm chí còn ít hơn so với Mobile). Hầu hết hiệu ứng post-processing đều không khả dụng.

Tại sao không sử dụng deferred rendering?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Forward rendering nhìn chung mang lại sự đánh đổi tốt hơn giữa hiệu năng và tính linh hoạt, đặc biệt khi sử dụng phương pháp clustered cho việc chiếu sáng. Mặc dù deferred rendering có thể nhanh hơn trong một số trường hợp, nó cũng kém linh hoạt hơn và yêu cầu sử dụng các thủ thuật để có thể dùng MSAA. Vì các game có phong cách nghệ thuật ít chân thực hơn có thể hưởng lợi nhiều từ MSAA, chúng tôi đã chọn forward rendering cho Godot 4 (giống như Godot 3).

Tuy vậy, một số phần của forward renderer *được* thực hiện theo cách deferred để cho phép áp dụng một số tối ưu hóa khi có thể. Điều này đặc biệt áp dụng cho VoxelGI và SDFGI.

Trong tương lai, có thể sẽ phát triển một clustered deferred renderer. Renderer này có thể được sử dụng trong những tình huống ưu tiên hiệu năng hơn tính linh hoạt.

Các rendering driver
--------------------

Godot 4 hỗ trợ các graphics API sau:

Vulkan
~~~~~~

Đây là driver chính trong Godot 4, với phần lớn trọng tâm phát triển được dành cho driver này.

Vulkan 1.0 là yêu cầu cơ bản, còn các tính năng Vulkan 1.1 và 1.2 tùy chọn sẽ được sử dụng khi khả dụng. `volk <https://github.com/zeux/volk>`__ được sử dụng làm Vulkan loader, còn `Vulkan Memory Allocator <https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator>`__ được sử dụng để quản lý bộ nhớ.

Forward+ và Mobile
:ref:`doc_internal_rendering_architecture_methods` đều được hỗ trợ khi sử dụng Vulkan driver.

**Tạo Vulkan context:**

- `drivers/vulkan/rendering_context_driver_vulkan.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/vulkan/rendering_context_driver_vulkan.cpp>`__

**Tạo Direct3D 12 context:**

- `drivers/d3d12/rendering_context_driver_d3d12.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/d3d12/rendering_context_driver_d3d12.cpp>`__

Direct3D 12
~~~~~~~~~~~

Giống như Vulkan, Direct3D 12 driver chỉ nhắm đến các nền tảng hiện đại. Driver này được thiết kế để nhắm đến cả Windows và Xbox (trong khi Vulkan không thể được sử dụng trực tiếp trên Xbox).

Cả Forward+ và Mobile :ref:`doc_internal_rendering_architecture_methods` đều có thể được sử dụng với Direct3D 12.

:ref:`doc_internal_rendering_architecture_core_shaders` được dùng chung với Vulkan renderer. Shader được chuyển đổi từ
:abbr:`SPIR-V (Standard Portable Intermediate Representation)` sang
:abbr:`DXIL (DirectX Intermediate Language)` bằng Mesa NIR (`thông tin thêm <https://godotengine.org/article/d3d12-adventures-in-shaderland/>`__).

**Driver này vẫn đang trong giai đoạn thử nghiệm và chỉ khả dụng trong Godot 4.3 trở lên.** Mặc dù Direct3D 12 cho phép hỗ trợ các tính năng độc quyền của Direct3D trên Windows 11, chẳng hạn như tối ưu hóa cửa sổ và Auto HDR, Vulkan vẫn được khuyến nghị cho hầu hết các dự án. Xem `pull request giới thiệu hỗ trợ Direct3D 12 <https://github.com/godotengine/godot/pull/70315>`__ để biết thêm thông tin.

Metal
~~~~~

Godot cung cấp một Metal driver native hoạt động trên mọi phần cứng Apple Silicon (macOS ARM). So với việc sử dụng lớp chuyển đổi MoltenVK, driver này nhanh hơn đáng kể, đặc biệt trong các tình huống bị giới hạn bởi CPU.

Cả Forward+ và Mobile :ref:`doc_internal_rendering_architecture_methods` đều có thể được sử dụng với Metal.

:ref:`doc_internal_rendering_architecture_core_shaders` được dùng chung với Vulkan renderer. Shader được chuyển đổi từ GLSL sang :abbr:`MSL (Metal Shading Language)` bằng SPIRV-Cross.

Godot cũng hỗ trợ rendering bằng Metal thông qua `MoltenVK <https://github.com/KhronosGroup/MoltenVK>`__, được sử dụng làm phương án dự phòng khi không có hỗ trợ Metal native (ví dụ: trên macOS x86).

Kể từ Godot 4.7, Metal 4 được sử dụng khi được hỗ trợ. Mọi phần cứng Apple Silicon đều hỗ trợ Metal 4, nhưng phải chạy macOS 26 trở lên hoặc iOS 26 trở lên. Metal 3 sẽ tự động được sử dụng làm phương án dự phòng trên các phiên bản macOS và iOS cũ hơn. Xem `pull request giới thiệu hỗ trợ Metal 4 <https://github.com/godotengine/godot/pull/114484>`__ để biết thêm thông tin.

OpenGL
~~~~~~

Driver này sử dụng OpenGL ES 3.0 và nhắm đến các thiết bị đời cũ và cấp thấp không hỗ trợ Vulkan. OpenGL 3.3 Core Profile được sử dụng trên các nền tảng desktop để chạy driver này, vì phần lớn graphics driver trên desktop không hỗ trợ OpenGL ES. WebGL 2.0 được sử dụng cho các bản export web.

Có thể sử dụng trực tiếp OpenGL ES 3.0 trên các nền tảng desktop bằng cách truyền đối số dòng lệnh ``--rendering-driver opengl3_es``, tuy nhiên cách này chỉ hoạt động trên các graphics driver có hỗ trợ OpenGL ES native (chẳng hạn như Mesa).

Chỉ có rendering method :ref:`doc_internal_rendering_architecture_compatibility` mới có thể được sử dụng với OpenGL driver.

:ref:`doc_internal_rendering_architecture_core_shaders` hoàn toàn khác với Vulkan renderer.

Driver này không hỗ trợ nhiều tính năng nâng cao, vì trước hết nó nhắm đến các thiết bị cấp thấp.

Tóm tắt các rendering driver/method
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiện có thể sử dụng các tổ hợp rendering API + rendering method sau:

- Vulkan + Forward+ (tùy chọn thông qua MoltenVK trên macOS và iOS)
- Vulkan + Mobile (tùy chọn thông qua MoltenVK trên macOS và iOS)
- Direct3D 12 + Forward+
- Direct3D 12 + Mobile
- Metal + Forward+
- Metal + Mobile
- OpenGL + Compatibility (tùy chọn thông qua ANGLE trên Windows và macOS)

Mỗi tổ hợp đều có những hạn chế và đặc tính hiệu năng riêng. Nếu có thể, hãy kiểm tra các thay đổi của bạn trên tất cả rendering method trước khi mở pull request.

Kiến trúc abstraction của RenderingDevice
-----------------------------------------

.. note::

    OpenGL driver không sử dụng abstraction của RenderingDevice.

Để giúp quản lý độ phức tạp của các graphics API cấp thấp hiện đại, Godot sử dụng abstraction riêng có tên là RenderingDevice.

Điều này có nghĩa là khi viết code cho các rendering method hiện đại, bạn không thực sự sử dụng trực tiếp các API Vulkan, Direct3D 12 hoặc Metal. Mặc dù vẫn ở mức thấp hơn một API như OpenGL, cách này giúp làm việc với renderer dễ dàng hơn, vì RenderingDevice sẽ trừu tượng hóa nhiều điểm khác biệt đặc thù của API cho bạn. RenderingDevice cung cấp mức độ abstraction tương tự WebGPU.

**Triển khai Vulkan RenderingDevice:**

- `drivers/vulkan/rendering_device_driver_vulkan.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/vulkan/rendering_device_driver_vulkan.cpp>`__

**Triển khai Direct3D 12 RenderingDevice:**

- `drivers/d3d12/rendering_device_driver_d3d12.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/d3d12/rendering_device_driver_d3d12.cpp>`__

**Triển khai Metal RenderingDevice:**

- `drivers/metal/rendering_device_driver_metal.cpp <https://github.com/godotengine/godot/blob/master/drivers/metal/rendering_device_driver_metal.cpp>`__ - Metal 4
- `drivers/metal/rendering_device_driver_metal3.cpp <https://github.com/godotengine/godot/blob/master/drivers/metal/rendering_device_driver_metal3.cpp>`__ - Metal 3

Kiến trúc các lớp rendering cốt lõi
-----------------------------------

Sơ đồ này thể hiện cấu trúc của các lớp rendering trong Godot, bao gồm cả lớp trừu tượng RenderingDevice:

.. image:: img/rendering_architecture_diagram.webp

`Xem ở kích thước đầy đủ <https://raw.githubusercontent.com/godotengine/godot-docs/master/engine_details/architecture/img/rendering_architecture_diagram.webp>`__

.. _doc_internal_rendering_architecture_core_shaders:

Core shaders
------------

Mặc dù shader trong các dự án Godot được viết bằng
:ref:`ngôn ngữ tùy chỉnh lấy cảm hứng từ GLSL <doc_shading_language>`, core shader được viết trực tiếp bằng GLSL.

Các core shader này được nhúng vào editor và các binary export template trong thời gian biên dịch. Để xem bất kỳ thay đổi nào bạn đã thực hiện đối với các shader GLSL đó, bạn cần biên dịch lại editor hoặc binary export template.

Một số tính năng material như height mapping, refraction và proximity fade không thuộc core shader mà được thực hiện trong BaseMaterial3D mặc định bằng ngôn ngữ shader của Godot (thay vì GLSL). Điều này được thực hiện bằng cách tạo mã shader cần thiết theo thủ tục, tùy thuộc vào các tính năng được bật trong material.

Theo quy ước, các tệp shader có ``_inc`` trong tên sẽ được đưa vào các tệp GLSL khác để tái sử dụng mã tốt hơn. Việc này sử dụng tiền xử lý GLSL tiêu chuẩn.

.. warning::

    Core material shader sẽ được mọi material trong scene sử dụng – cả với BaseMaterial3D mặc định lẫn custom shader. Do đó, các shader này phải được giữ đơn giản nhất có thể để tránh vấn đề về hiệu năng và bảo đảm quá trình biên dịch shader không trở nên quá chậm.

    Nếu bạn sử dụng ``if`` branching trong shader, hiệu năng có thể giảm vì
    :abbr:`VGPR (việc sử dụng Vector General-Purpose Register)` sẽ tăng trong shader. Điều này xảy ra ngay cả khi tất cả pixel đều cho kết quả ``true`` hoặc ``false`` trong một frame nhất định.

    Nếu bạn sử dụng ``#if`` branching của preprocessor, số phiên bản shader cần thiết trong scene sẽ tăng. Trong trường hợp xấu nhất, việc thêm một ``#define`` boolean duy nhất có thể *tăng gấp đôi* số phiên bản shader có thể cần được biên dịch trong một scene nhất định. Trong một số trường hợp, specialization constant của Vulkan có thể được sử dụng như một giải pháp thay thế nhanh hơn (nhưng hạn chế hơn).

    Điều này có nghĩa là việc thêm các tính năng material tích hợp mới vào Godot có rào cản rất lớn, cả trong core shader lẫn BaseMaterial3D. Mặc dù BaseMaterial3D có thể sử dụng việc tạo mã động để chỉ đưa mã shader vào khi tính năng được bật, việc đó vẫn yêu cầu tạo thêm các phiên bản shader khi những tính năng này được sử dụng trong một dự án. Điều này có thể khiến hiện tượng giật do biên dịch shader dễ nhận thấy hơn trong các scene 3D phức tạp.

    Xem các bài viết blog `The Shader Permutation Problem <https://therealmjp.github.io/posts/shader-permutations-part1/>`__ và `Branching on a GPU <https://medium.com/@jasonbooth_86226/branching-on-a-gpu-18bfc83694f2>`__ để biết thêm thông tin.

**Core GLSL material shader:**

- Forward+: `servers/rendering/renderer_rd/shaders/forward_clustered/scene_forward_clustered.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/forward_clustered/scene_forward_clustered.glsl>`__
- Mobile: `servers/rendering/renderer_rd/shaders/forward_mobile/scene_forward_mobile.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/forward_mobile/scene_forward_mobile.glsl>`__
- Compatibility: `drivers/gles3/shaders/scene.glsl <https://github.com/godotengine/godot/blob/4.6/drivers/gles3/shaders/scene.glsl>`__

**Tạo material shader:**

- `scene/resources/material.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/material.cpp>`__

**Các GLSL shader khác cho phương thức rendering Forward+ và Mobile:**

- `servers/rendering/renderer_rd/shaders/ <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/>`__
- `modules/lightmapper_rd/ <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd>`__

**Các GLSL shader khác cho phương thức rendering Compatibility:**

- `drivers/gles3/shaders/ <https://github.com/godotengine/godot/blob/4.6/drivers/gles3/shaders/>`__

Phân tách rendering 2D và 3D
----------------------------

.. note::

    Nội dung sau chỉ áp dụng cho các phương thức rendering Forward+ và Mobile, không áp dụng cho Compatibility. Có thể sử dụng nhiều Viewport để mô phỏng điều này khi sử dụng Compatibility renderer, hoặc để thực hiện scaling độ phân giải 2D.

2D và 3D được render vào các buffer riêng biệt, vì rendering 2D trong Godot được thực hiện trong không gian sRGB :abbr:`LDR (Low Dynamic Range)`, còn rendering 3D sử dụng
không gian tuyến tính :abbr:`HDR (High Dynamic Range)`.

Định dạng màu được sử dụng cho rendering 2D là RGB8 (RGBA8 nếu thuộc tính **Transparent** trên Viewport được bật). Rendering 3D sử dụng depth buffer số nguyên chưa chuẩn hóa không dấu 24-bit, hoặc số dấu phẩy động có dấu 32-bit nếu phần cứng không hỗ trợ depth buffer 24-bit. Rendering 2D không sử dụng depth buffer.

Scaling độ phân giải 3D được thực hiện khác nhau tùy thuộc vào việc sử dụng scaling bilinear hay FSR 1.0. Khi sử dụng scaling bilinear, không có shader upscale đặc biệt nào được chạy. Thay vào đó, texture của viewport được kéo giãn và hiển thị bằng linear sampler (khiến việc lọc diễn ra trực tiếp trên phần cứng). Điều này cho phép tối đa hóa hiệu năng của scaling 3D bilinear.

``configure()`` function trong RenderSceneBuffersRD sẽ cấp phát lại các buffer 2D/3D khi độ phân giải hoặc scaling thay đổi.

.. UPDATE: Planned feature. When dynamic resolution scaling is supported,
.. update this paragraph.

Dynamic resolution scaling hiện chưa được hỗ trợ, nhưng đã được lên kế hoạch cho một bản phát hành Godot trong tương lai.

**Mã C++ cấu hình buffer rendering 2D và 3D:**

- `servers/rendering/renderer_rd/storage_rd/render_scene_buffers_rd.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/storage_rd/render_scene_buffers_rd.cpp>`__

**FSR 1.0:**

- `servers/rendering/renderer_rd/effects/fsr.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/fsr.cpp>`__
- `thirdparty/amd-fsr/ <https://github.com/godotengine/godot/tree/master/thirdparty/amd-fsr>`__

Các kỹ thuật rendering 2D
-------------------------

Rendering ánh sáng 2D được thực hiện trong một pass duy nhất để đạt hiệu năng tốt hơn với số lượng lớn đèn.

Tất cả các phương thức rendering đều có batching 2D để cải thiện hiệu năng, đặc biệt dễ nhận thấy khi có nhiều văn bản trên màn hình.

Có thể bật MSAA trong 2D để cung cấp khả năng khử răng cưa "tự động" cho đường thẳng và đa giác, nhưng FXAA không ảnh hưởng đến rendering 2D vì nó được tính toán trước khi rendering 2D bắt đầu. Các phương thức vẽ 2D của Godot như node Line2D hoặc một số ``draw_*()`` methods của CanvasItem cung cấp cách khử răng cưa riêng dựa trên triangle strip và vertex color, không yêu cầu MSAA để hoạt động.

Một signed distance field 2D đại diện cho các node LightOccluder2D trong viewport sẽ tự động được tạo nếu user shader yêu cầu. Field này có thể được sử dụng cho nhiều hiệu ứng khác nhau trong custom shader, chẳng hạn như global illumination 2D. Nó cũng được sử dụng để tính toán va chạm của particle trong 2D.

**GLSL shader tạo 2D SDF:**

- `servers/rendering/renderer_rd/shaders/canvas_sdf.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/canvas_sdf.glsl>`__

Các kỹ thuật rendering 3D
-------------------------

Reverse Z
~~~~~~~~~

Tất cả renderer của Godot đều sử dụng reverse Z. Điều này có nghĩa là depth buffer bị đảo ngược, trong đó ``1.0`` biểu thị mặt phẳng gần và ``0.0`` biểu thị mặt phẳng xa. Điều này cho phép `độ chính xác tốt hơn <https://developer.nvidia.com/content/depth-precision-visualized>`__, đặc biệt là ở khoảng cách xa.

Batching và instancing
~~~~~~~~~~~~~~~~~~~~~~

Trong renderer Forward+, Vulkan instancing được sử dụng để nhóm việc rendering các đối tượng opaque hoặc alpha-tested giống hệt nhau nhằm cải thiện hiệu năng. (Các đối tượng alpha-blended không bao giờ được instancing.) Cách này không nhanh bằng việc hợp nhất static mesh, nhưng vẫn cho phép culling từng instance riêng lẻ.

Rendering light, decal và reflection probe
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

  Hiện tại, renderer Compatibility không hỗ trợ rendering decal.

Renderer Forward+ sử dụng clustered lighting. Điều này cho phép bạn sử dụng bao nhiêu light tùy ý; hiệu năng phần lớn phụ thuộc vào phần diện tích màn hình bị che phủ. Các light không có shadow có thể gần như không tốn chi phí nếu chúng không chiếm nhiều không gian trên màn hình.

Tất cả phương thức rendering cũng hỗ trợ rendering đồng thời tối đa 8 directional light (dù chất lượng shadow sẽ thấp hơn khi có nhiều hơn một light bật shadow).

Renderer Mobile sử dụng phương pháp lighting một pass, với giới hạn 8 OmniLights + 8 SpotLights ảnh hưởng đến mỗi Mesh *tài nguyên* (cộng thêm giới hạn 256 OmniLights + 256 SpotLights trong vùng nhìn của camera). Các giới hạn này được hardcode và không thể điều chỉnh trong project settings.

Renderer Compatibility sử dụng phương pháp lighting lai giữa một pass và nhiều pass. Các light không có shadow được rendering trong một pass. Các light có shadow được rendering qua nhiều pass. Điều này cần thiết vì lý do hiệu năng trên các thiết bị di động. Do đó, hiệu năng không mở rộng tốt khi có nhiều light tạo shadow. Bạn nên chỉ có một vài light có shadow trong camera frustum tại một thời điểm, đồng thời bố trí các light đó cách xa nhau để mỗi object chỉ bị tác động bởi 1 hoặc 2 light có shadow tại một thời điểm. Có thể điều chỉnh số lượng light tối đa hiển thị cùng lúc trong project settings.

.. UPDATE: Planned feature. When static and dynamic shadow rendering are
.. separated, update this paragraph.

Trong cả 3 phương thức, light không có shadow rẻ hơn nhiều so với light có shadow. Để cải thiện hiệu năng, light chỉ được cập nhật khi light bị thay đổi hoặc khi các object trong bán kính của nó bị thay đổi. Hiện tại Godot không tách rendering static shadow khỏi rendering dynamic shadow, nhưng tính năng này đã được lên kế hoạch cho một bản phát hành trong tương lai.

Clustering cũng được sử dụng cho reflection probe và rendering decal trong renderer Forward+.

Area light sử dụng kỹ thuật `Linearly Transformed Cosines <https://eheitzresearch.wordpress.com/757-2/>`__.

Shadow mapping
~~~~~~~~~~~~~~

Cả phương thức Forward+ và Mobile đều sử dụng
:abbr:`PCF (Percentage Closer Filtering)` để lọc shadow map và tạo penumbra mềm. Thay vì sử dụng một mẫu PCF cố định, các phương thức này sử dụng mẫu vogel disk, cho phép thay đổi số lượng sample và thay đổi chất lượng một cách mượt mà.

Godot cũng hỗ trợ percentage-closer soft shadow (PCSS) để rendering penumbra của shadow chân thực hơn. Shadow PCSS chỉ được giới hạn ở renderer Forward+ vì chúng đòi hỏi quá nhiều tài nguyên để có thể sử dụng trong renderer Mobile. PCSS cũng sử dụng kernel có hình dạng vogel disk.

Ngoài ra, cả hai kỹ thuật shadow mapping đều xoay kernel theo từng pixel để giúp làm mềm các artifact do lấy mẫu thiếu.

Renderer Compatibility hỗ trợ shadow mapping cho các light DirectionalLight3D, OmniLight3D và SpotLight3D.

Temporal antialiasing
~~~~~~~~~~~~~~~~~~~~~

.. note::

    Chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.

Godot sử dụng một triển khai TAA tùy chỉnh dựa trên triển khai TAA cũ của `Spartan Engine <https://github.com/PanosK92/SpartanEngine>`__.

Temporal antialiasing yêu cầu motion vector để hoạt động. Nếu motion vector không được tạo chính xác, hiện tượng ghosting sẽ xảy ra khi camera hoặc các object di chuyển.

Motion vector được tạo trên GPU trong main material shader. Việc này được thực hiện bằng cách chạy vertex shader tương ứng với frame đã rendering trước đó (với phép biến đổi camera trước đó) cùng với vertex shader của frame hiện tại, sau đó lưu phần chênh lệch giữa chúng vào color buffer.

Ngoài ra, có thể sử dụng FSR 2.2 làm giải pháp upscaling, đồng thời cung cấp thuật toán temporal antialiasing riêng. FSR 2.2 được triển khai trên lớp trừu tượng RenderingDevice thay vì sử dụng trực tiếp mã tham chiếu của AMD.

**TAA resolve:**

- `servers/rendering/renderer_rd/shaders/effects/taa_resolve.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/taa_resolve.glsl>`__

**FSR 2.2:**

- `servers/rendering/renderer_rd/effects/fsr2.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/fsr2.cpp>`__
- `servers/rendering/renderer_rd/shaders/effects/fsr2/ <https://github.com/godotengine/godot/tree/master/servers/rendering/renderer_rd/shaders/effects/fsr2>`__
- `thirdparty/amd-fsr2/ <https://github.com/godotengine/godot/tree/master/thirdparty/amd-fsr2>`__

Global illumination
~~~~~~~~~~~~~~~~~~~

.. note::

    VoxelGI và SDFGI chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.

    *Việc baking* LightmapGI chỉ khả dụng trong renderer Forward+ và Mobile, đồng thời chỉ có thể được thực hiện trong editor (không phải trong project đã export). *Việc rendering* LightmapGI được renderer Compatibility hỗ trợ.

Godot hỗ trợ GI dựa trên voxel (VoxelGI), GI dựa trên signed distance field (SDFGI) và baking cũng như rendering lightmap (LightmapGI). Có thể sử dụng đồng thời các kỹ thuật này nếu muốn.

Việc baking lightmap diễn ra trên GPU bằng compute shader Vulkan. Lightmapper dựa trên GPU được triển khai trong class LightmapperRD, kế thừa từ class Lightmapper. Điều này cho phép triển khai thêm các lightmapper, mở đường cho việc port lightmapper dựa trên CPU hiện có trong Godot 3.x trong tương lai. Nhờ đó, có thể baking lightmap khi sử dụng renderer Compatibility.

**Mã C++ GI cốt lõi:**

- `servers/rendering/renderer_rd/environment/gi.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/environment/gi.cpp>`__
- `scene/3d/voxel_gi.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/voxel_gi.cpp>`__ - node VoxelGI
- `editor/scene/3d/voxel_gi_editor_plugin.cpp <https://github.com/godotengine/godot/blob/4.6/editor/scene/3d/voxel_gi_editor_plugin.cpp>`__ - UI editor cho node VoxelGI

**Các shader GLSL GI cốt lõi:**

- `servers/rendering/renderer_rd/shaders/environment/voxel_gi.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/voxel_gi.glsl>`__
- `servers/rendering/renderer_rd/shaders/environment/voxel_gi_debug.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/voxel_gi_debug.glsl>`__ - chế độ vẽ gỡ lỗi VoxelGI
- `servers/rendering/renderer_rd/shaders/environment/sdfgi_debug.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_debug.glsl>`__ - chế độ vẽ gỡ lỗi Cascades của SDFGI
- `servers/rendering/renderer_rd/shaders/environment/sdfgi_debug_probes.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_debug_probes.glsl>`__ - chế độ vẽ gỡ lỗi Probes của SDFGI
- `servers/rendering/renderer_rd/shaders/environment/sdfgi_integrate.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_integrate.glsl>`__
- `servers/rendering/renderer_rd/shaders/environment/sdfgi_preprocess.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_preprocess.glsl>`__
- `servers/rendering/renderer_rd/shaders/environment/sdfgi_direct_light.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_direct_light.glsl>`__

**Mã C++ của Lightmapper:**

- `scene/3d/lightmap_gi.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/lightmap_gi.cpp>`__ - node LightmapGI
- `editor/scene/3d/lightmap_gi_editor_plugin.cpp <https://github.com/godotengine/godot/blob/4.6/editor/scene/3d/lightmap_gi_editor_plugin.cpp>`__ - UI editor cho node LightmapGI
- `scene/3d/lightmapper.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/lightmapper.cpp>`__ - Lớp trừu tượng
- `modules/lightmapper_rd/lightmapper_rd.cpp <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lightmapper_rd.cpp>`__ - triển khai lightmapper dựa trên GPU

**Các shader GLSL của Lightmapper:**

- `modules/lightmapper_rd/lm_raster.glsl <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lm_raster.glsl>`__
- `modules/lightmapper_rd/lm_compute.glsl <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lm_compute.glsl>`__
- `modules/lightmapper_rd/lm_blendseams.glsl <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lm_blendseams.glsl>`__

Độ sâu trường ảnh
~~~~~~~~~~~~~~~~~

.. note::

    Chỉ có trong các renderer Forward+ và Mobile, không có trong renderer Compatibility.

Các renderer Forward+ và Mobile sử dụng những cách tiếp cận khác nhau để render DOF, tạo ra các kết quả hình ảnh khác nhau. Điều này nhằm phù hợp nhất với đặc tính hiệu năng của phần cứng đích. Trong Forward+, DOF được thực hiện bằng compute shader. Trong Mobile, DOF được thực hiện bằng fragment shader (raster).

Có các hình dạng bokeh hình hộp, hình lục giác và hình tròn (từ nhanh nhất đến chậm nhất). Có thể tùy chọn jitter độ sâu trường ảnh ở mỗi frame để cải thiện hình ảnh khi bật temporal antialiasing.

**Mã C++ của độ sâu trường ảnh:**

- `servers/rendering/renderer_rd/effects/bokeh_dof.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/bokeh_dof.cpp>`__

**Shader GLSL cho độ sâu trường ảnh (compute - dùng cho Forward+):**

- `servers/rendering/renderer_rd/shaders/effects/bokeh_dof.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/bokeh_dof.glsl>`__

**Shader GLSL cho độ sâu trường ảnh (raster - dùng cho Mobile):**

- `servers/rendering/renderer_rd/shaders/effects/bokeh_dof_raster.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/bokeh_dof_raster.glsl>`__

Các hiệu ứng trong không gian màn hình (SSAO, SSIL, SSR, SSS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Chỉ có trong renderer Forward+, không có trong các renderer Mobile hoặc Compatibility.

Renderer Forward+ hỗ trợ ambient occlusion trong không gian màn hình, lighting gián tiếp trong không gian màn hình, reflections trong không gian màn hình và subsurface scattering.

SSAO sử dụng một triển khai bắt nguồn từ `ASSAO <https://www.intel.com/content/www/us/en/developer/articles/technical/adaptive-screen-space-ambient-occlusion.html>`__ của Intel (được chuyển đổi sang Vulkan). SSIL được phát triển từ SSAO để cung cấp lighting gián tiếp hiệu năng cao.

Khi bật cả SSAO và SSIL, một số phần của SSAO và SSIL được dùng chung để giảm tác động đến hiệu năng.

Theo mặc định, SSAO, SSIL và SSR được thực hiện ở độ phân giải một nửa để cải thiện hiệu năng.

SSR sử dụng buffer Hi-Z để cải thiện hiệu năng. Buffer Hi-Z này được tạo từ depth buffer trong compute shader. Xem `pull request đã cải tiến SSR <https://github.com/godotengine/godot/pull/111210>`__ để biết thêm thông tin.

**Mã C++ của các hiệu ứng trong không gian màn hình:**

- `servers/rendering/renderer_rd/effects/ss_effects.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/ss_effects.cpp>`__

**Shader GLSL cho ambient occlusion trong không gian màn hình:**

- `servers/rendering/renderer_rd/shaders/effects/ssao.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/ssao_blur.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao_blur.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/ssao_interleave.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao_interleave.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/ssao_importance_map.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao_importance_map.glsl>`__

**Shader GLSL cho lighting gián tiếp trong không gian màn hình:**

- `servers/rendering/renderer_rd/shaders/effects/ssil.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/ssil_blur.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil_blur.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/ssil_interleave.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil_interleave.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/ssil_importance_map.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil_importance_map.glsl>`__

**Shader GLSL cho reflections trong không gian màn hình:**

- `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_filter.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_filter.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_resolve.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_resolve.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_hiz.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_hiz.glsl>`__
- `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_downsample.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_downsample.glsl>`__

**Subsurface scattering GLSL:**

- `servers/rendering/renderer_rd/shaders/effects/subsurface_scattering.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/subsurface_scattering.glsl>`__

Kết xuất bầu trời
~~~~~~~~~~~~~~~~~

.. seealso::

    :ref:`doc_sky_shader`

Godot hỗ trợ sử dụng shader để kết xuất nền bầu trời. Bản đồ bức xạ (được dùng để cung cấp ánh sáng môi trường và phản chiếu cho các vật liệu PBR) sẽ tự động được cập nhật dựa trên sky shader.

Các resource SkyMaterial như ProceduralSkyMaterial, PhysicalSkyMaterial và PanoramaSkyMaterial tạo ra một shader dựng sẵn để kết xuất bầu trời. Cách này tương tự những gì BaseMaterial3D cung cấp cho các vật liệu scene 3D.

Bạn có thể tìm thấy phần triển khai kỹ thuật chi tiết trong bài viết `Custom sky shaders in Godot 4.0 <https://godotengine.org/article/custom-sky-shaders-godot-4-0>`__.

**Mã C++ kết xuất bầu trời:**

- `servers/rendering/renderer_rd/environment/sky.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/environment/sky.cpp>`__ - Kết xuất bầu trời
- `scene/resources/sky.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/sky.cpp>`__ - Resource bầu trời (không nên nhầm với việc kết xuất bầu trời)
- `scene/resources/3d/sky_material.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/3d/sky_material.cpp>`__ Các resource SkyMaterial (được sử dụng trong resource Sky)

**Shader GLSL kết xuất bầu trời:**

Sương mù thể tích
~~~~~~~~~~~~~~~~~

.. note::

    Chỉ khả dụng trong Forward+, không khả dụng trong các renderer Mobile hoặc Compatibility.

.. seealso::

    :ref:`doc_fog_shader`

Godot hỗ trợ phương pháp voxel (froxel) căn chỉnh theo frustum để kết xuất sương mù thể tích. Không giống như một bộ lọc hậu kỳ, phương pháp này có mục đích sử dụng tổng quát hơn vì có thể hoạt động với mọi loại ánh sáng. Sương mù cũng có thể sử dụng shader để tạo hành vi tùy chỉnh, cho phép tạo hiệu ứng chuyển động cho sương mù hoặc sử dụng texture 3D để biểu diễn mật độ.

Resource FogMaterial tạo ra một shader dựng sẵn cho các node FogVolume. Cách này tương tự những gì BaseMaterial3D cung cấp cho các vật liệu scene 3D.

Bạn có thể tìm thấy phần giải thích kỹ thuật chi tiết trong bài viết `Fog Volumes arrive in Godot 4.0 <https://godotengine.org/article/fog-volumes-arrive-in-godot-4>`__.

**Mã C++ sương mù thể tích:**

- `servers/rendering/renderer_rd/environment/fog.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/environment/fog.cpp>`__ - Sương mù thể tích tổng quát
- `scene/3d/fog_volume.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/fog_volume.cpp>`__ - Node FogVolume
- `scene/resources/3d/fog_material.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/3d/fog_material.cpp>`__ - Resource FogMaterial (được FogVolume sử dụng)

**Các shader GLSL sương mù thể tích:**

- `servers/rendering/renderer_rd/shaders/environment/volumetric_fog.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/volumetric_fog.glsl>`__
- `servers/rendering/renderer_rd/shaders/environment/volumetric_fog_process.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/volumetric_fog_process.glsl>`__

Culling vật thể che khuất
~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù các GPU hiện đại có thể xử lý việc vẽ rất nhiều tam giác, số lượng draw call trong các scene phức tạp vẫn có thể trở thành nút thắt cổ chai (ngay cả với Vulkan, Direct3D 12 và Metal).

Godot 4 hỗ trợ culling vật thể che khuất để giảm overdraw (khi depth prepass bị tắt) và giảm vertex throughput. Việc này được thực hiện bằng cách rasterize một buffer độ phân giải thấp trên CPU thông qua `Embree <https://github.com/embree/embree>`__. Độ phân giải của buffer phụ thuộc vào số luồng CPU trên hệ thống, vì quá trình này được thực hiện song song. Buffer này bao gồm các hình dạng vật thể che khuất được bake trong editor hoặc tạo trong runtime. Buffer culling vật thể che khuất được jitter một lượng nhỏ ở mỗi frame để giúp giảm các hiện tượng giả do lấy mẫu thiếu, vốn có thể dẫn đến kết quả dương tính giả (các đối tượng bị che khuất dù không nên bị che khuất).

Vì các vật thể che khuất phức tạp có thể gây nhiều tải cho CPU, các vật thể che khuất được bake có thể được tự động đơn giản hóa khi tạo trong editor.

Culling vật thể che khuất của Godot hiện chưa hỗ trợ các vật thể che khuất động, nhưng các node OccluderInstance3D vẫn có thể bật/tắt khả năng hiển thị hoặc được di chuyển. Tuy nhiên, việc cập nhật các vật thể che khuất phức tạp theo cách này sẽ chậm. Do đó, tốt nhất chỉ cập nhật vật thể che khuất trong runtime đối với các hình dạng đơn giản như quad hoặc cuboid.

Phương pháp dựa trên CPU này có một số ưu điểm so với các giải pháp khác, chẳng hạn như portal và room hoặc giải pháp culling dựa trên GPU:

- Không cần thiết lập thủ công (nhưng có thể tinh chỉnh thủ công để đạt hiệu năng tốt nhất).
- Không có độ trễ frame, vốn gây vấn đề trong các cutscene khi camera chuyển cảnh hoặc khi camera di chuyển nhanh ra phía sau một bức tường.
- Hoạt động giống nhau trên mọi rendering driver và phương thức, không có hành vi khó đoán tùy thuộc vào driver hoặc phần cứng GPU.

Culling vật thể che khuất được thực hiện bằng cách đăng ký các mesh vật thể che khuất, thông qua các *node* OccluderInstance3D (bản thân chúng sử dụng các *resource* Occluder3D). Sau đó, RenderingServer thực hiện culling vật thể che khuất bằng cách gọi Embree trong RendererSceneOcclusionCull.

**Mã C++ culling vật thể che khuất:**

- `scene/3d/occluder_instance_3d.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/occluder_instance_3d.cpp>`__
- `servers/rendering/renderer_scene_occlusion_cull.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_scene_occlusion_cull.cpp>`__

Phạm vi hiển thị (LOD)
~~~~~~~~~~~~~~~~~~~~~~

Godot hỗ trợ hierarchical level of detail (HLOD) được tạo thủ công, với khoảng cách do người dùng chỉ định trong inspector.

Trong RenderingSceneCull, các hàm ``_scene_cull()`` và ``_render_scene()`` là nơi phần lớn quá trình xác định LOD diễn ra. Mỗi viewport có thể kết xuất cùng một mesh với các LOD khác nhau (để hiển thị split screen chính xác).

**Mã C++ phạm vi hiển thị:**

- `servers/rendering/renderer_scene_cull.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_scene_cull.cpp>`__

LOD mesh tự động
~~~~~~~~~~~~~~~~

Class ImporterMesh được sử dụng cho quy trình import mesh 3D trong editor. Hàm ``generate_lods()`` của class này xử lý việc tạo mesh bằng thư viện `meshoptimizer <https://meshoptimizer.org/>`__.

Việc tạo mesh LOD cũng đồng thời tạo các shadow mesh. Đây là những mesh có các vertex được weld bất kể smoothing và material. Tính năng này được dùng để cải thiện hiệu năng kết xuất bóng bằng cách giảm vertex throughput cần thiết để kết xuất bóng.

Hàm ``_render_scene()`` của class RenderingSceneCull xác định mesh LOD nào sẽ được sử dụng khi kết xuất. Mỗi viewport có thể kết xuất cùng một mesh với các LOD khác nhau (để hiển thị split screen chính xác).

LOD mesh được tự động chọn dựa trên metric độ bao phủ màn hình. Metric này tính đến các thay đổi về độ phân giải và FOV của camera mà không cần người dùng can thiệp. Có thể điều chỉnh multiplier của ngưỡng trong project settings.

Để cải thiện hiệu năng, việc kết xuất bóng đổ và kết xuất reflection probe cũng tự chọn các ngưỡng LOD của mesh riêng (có thể khác với việc kết xuất cảnh chính).

**Mã C++ tạo LOD của mesh khi import:**

- `scene/resources/3d/importer_mesh.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/3d/importer_mesh.cpp>`__

**Mã C++ xác định LOD của mesh:**

- `servers/rendering/renderer_scene_cull.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_scene_cull.cpp>`__
