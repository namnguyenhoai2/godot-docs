.. _doc_internal_rendering_architecture:

Kiến trúc kết xuất nội bộ
=========================

Trang này là phần tổng quan cấp cao về thiết kế trình kết xuất nội bộ của Godot 4. Nội dung này không áp dụng cho các phiên bản Godot trước đây.

Mục tiêu của trang này là ghi lại các quyết định thiết kế nhằm phù hợp nhất với `triết lý thiết kế của Godot <https://contributing.godotengine.org/en/latest/engine/guidelines/best_practices.html>`__, đồng thời cung cấp điểm khởi đầu cho những người đóng góp mới cho hệ thống kết xuất.

Nếu bạn có câu hỏi về nội bộ hệ thống kết xuất chưa được giải đáp ở đây, hãy đặt câu hỏi trong kênh ``#rendering`` của `Godot Contributors Chat <https://chat.godotengine.org/channel/rendering>`__.

.. note::

    Nếu bạn gặp khó khăn khi hiểu các khái niệm trên trang này, bạn nên xem qua một hướng dẫn OpenGL, chẳng hạn như `LearnOpenGL <https://learnopengl.com/>`__.

    Các API cấp thấp hiện đại (Vulkan/Direct3D 12/Metal) yêu cầu kiến thức trung gian về các API cấp cao hơn (OpenGL/Direct3D 11) để có thể sử dụng hiệu quả. May mắn là những người đóng góp hiếm khi cần làm việc trực tiếp với các API cấp thấp. Các trình kết xuất của Godot được xây dựng hoàn toàn trên OpenGL và RenderingDevice, đây là lớp trừu tượng của chúng tôi trên Vulkan/Direct3D 12/Metal.

.. _doc_internal_rendering_architecture_methods:

Các phương thức kết xuất
------------------------

Forward+
~~~~~~~~

Đây là trình kết xuất tiến sử dụng phương pháp *phân cụm* để chiếu sáng.

Phương pháp chiếu sáng phân cụm sử dụng compute shader để nhóm các nguồn sáng vào một lưới 3D được căn chỉnh theo frustum. Sau đó, tại thời điểm kết xuất, các pixel có thể tra cứu những nguồn sáng ảnh hưởng đến ô lưới chứa chúng và chỉ thực hiện tính toán ánh sáng cho những nguồn sáng có khả năng ảnh hưởng đến pixel đó.

Phương pháp này có thể tăng đáng kể hiệu năng kết xuất trên phần cứng máy tính để bàn, nhưng kém hiệu quả hơn đáng kể trên thiết bị di động.

Mobile
~~~~~~

Đây là trình kết xuất tiến sử dụng phương pháp chiếu sáng truyền thống một lượt. Về nội bộ, nó được gọi là **Forward Mobile**.

Được thiết kế cho các nền tảng di động, nhưng cũng có thể chạy trên các nền tảng máy tính để bàn. Phương thức kết xuất này được tối ưu để hoạt động tốt trên GPU di động. GPU di động có kiến trúc rất khác so với GPU máy tính để bàn do các giới hạn riêng về mức tiêu thụ pin, nhiệt và tổng băng thông khi đọc và ghi dữ liệu. Compute shader cũng được hỗ trợ rất hạn chế hoặc hoàn toàn không được hỗ trợ. Do đó, trình kết xuất di động chỉ sử dụng shader dựa trên raster (fragment/vertex).

Không giống GPU máy tính để bàn, GPU di động thực hiện *kết xuất dựa trên ô*. Thay vì kết xuất toàn bộ hình ảnh như một đơn vị duy nhất, hình ảnh được chia thành các ô nhỏ hơn, vừa với bộ nhớ trong nhanh hơn của GPU di động. Mỗi ô được kết xuất rồi ghi vào texture đích. Tất cả quá trình này diễn ra tự động trong trình điều khiển đồ họa.

Vấn đề là điều này tạo ra các nút thắt trong phương pháp truyền thống của chúng ta. Đối với kết xuất trên máy tính để bàn, chúng ta kết xuất toàn bộ hình học không trong suốt, sau đó xử lý nền, rồi đến hình học trong suốt và cuối cùng là hậu xử lý. Mỗi lượt sẽ cần đọc kết quả hiện tại vào bộ nhớ ô, thực hiện các thao tác rồi lại ghi kết quả ra. Sau đó, chúng ta phải chờ tất cả các ô hoàn tất trước khi chuyển sang lượt tiếp theo.

Thay đổi quan trọng đầu tiên trong trình kết xuất di động là trình kết xuất di động không sử dụng các định dạng texture RGBA16F mà trình kết xuất máy tính để bàn (Forward+) sử dụng. Thay vào đó, nó sử dụng định dạng texture R10G10B10A2 UNORM trừ khi
:ref:`rendering/viewport/hdr_2d<class_ProjectSettings_property_rendering/viewport/hdr_2d>`
cài đặt dự án được bật. Điều này giảm một nửa băng thông cần thiết và còn mang lại các cải thiện khác, vì phần cứng di động thường tối ưu hơn nữa cho các định dạng 32-bit. Đổi lại, theo mặc định, trình kết xuất di động có khả năng HDR hạn chế do độ chính xác và giá trị tối đa trong dữ liệu màu bị giảm.

Khi cài đặt dự án :ref:`rendering/viewport/hdr_2d <class_ProjectSettings_property_rendering/viewport/hdr_2d>` được bật, trình kết xuất di động sử dụng các trình kết xuất RGBA16F giống như Forward+. Điều này cho phép hỗ trợ HDR đầy đủ, nhưng cũng làm tăng mức sử dụng băng thông và có thể làm giảm hiệu năng trên GPU di động hoặc đồ họa tích hợp.

Thay đổi quan trọng thứ hai là sử dụng các sub-pass bất cứ khi nào có thể. Sub-pass cho phép chúng ta thực hiện các bước kết xuất từ đầu đến cuối theo từng ô, giúp tiết kiệm chi phí phát sinh do phải đọc và ghi các ô giữa mỗi lượt kết xuất. Khả năng sử dụng sub-pass bị giới hạn bởi việc không thể đọc các pixel lân cận, vì chúng ta bị giới hạn trong phạm vi một ô duy nhất.

Hạn chế này của subpass khiến chúng ta không thể triển khai hiệu quả các tính năng như glow và depth of field. Tương tự, nếu cần đọc từ texture màn hình hoặc texture độ sâu, chúng ta phải ghi toàn bộ kết quả kết xuất ra, hạn chế khả năng sử dụng sub-pass. Khi các tính năng như vậy được bật, sự kết hợp giữa sub-pass và lượt thông thường sẽ được sử dụng, và các tính năng này gây ra mức phạt hiệu năng đáng kể.

Trên các nền tảng máy tính để bàn, việc sử dụng sub-pass sẽ không ảnh hưởng đến hiệu năng. Tuy nhiên, phương thức kết xuất này vẫn có thể hoạt động tốt hơn Forward+ trong các cảnh đơn giản nhờ độ phức tạp thấp hơn và mức sử dụng băng thông thấp hơn. Điều này đặc biệt dễ nhận thấy trên GPU cấp thấp, đồ họa tích hợp hoặc trong các ứng dụng VR.

Do tập trung vào phần cứng cấp thấp, phương thức kết xuất này không cung cấp các tính năng kết xuất cao cấp như SDFGI và :ref:`doc_volumetric_fog`. Một số hiệu ứng hậu xử lý cũng không khả dụng.

.. _doc_internal_rendering_architecture_compatibility:

Compatibility
~~~~~~~~~~~~~

.. note::

    Đây là phương thức kết xuất duy nhất khả dụng khi sử dụng trình điều khiển OpenGL. Phương thức kết xuất này không khả dụng khi sử dụng Vulkan, Direct3D 12 hoặc Metal.

Đây là trình kết xuất tiến truyền thống (không phân cụm). Về nội bộ, nó được gọi là **GL Compatibility**. Nó dành cho các GPU cũ không hỗ trợ Vulkan, nhưng vẫn hoạt động rất hiệu quả trên phần cứng mới hơn. Cụ thể, nó được tối ưu cho các thiết bị di động cũ và cấp thấp. Tuy nhiên, nhiều tối ưu hóa được áp dụng tương tự, khiến đây cũng là lựa chọn phù hợp cho máy tính để bàn cũ và cấp thấp.

Giống như trình kết xuất Mobile, trình kết xuất Compatibility sử dụng texture R10G10B10A2 UNORM cho kết xuất 3D. Không giống trình kết xuất di động, màu được tonemap và lưu ở định dạng sRGB nên không hỗ trợ HDR. Điều này loại bỏ nhu cầu về một lượt tonemap và cho phép chúng ta sử dụng texture có số bit thấp hơn mà không tạo ra hiện tượng phân dải đáng kể.

Trình kết xuất Compatibility sử dụng phương pháp truyền thống một lượt, tiến, để vẽ các đối tượng có nguồn sáng, nhưng sử dụng phương pháp nhiều lượt để vẽ các nguồn sáng có bóng. Cụ thể, trong lượt đầu tiên, nó có thể vẽ nhiều nguồn sáng không có bóng và tối đa một DirectionalLight3D có bóng. Trong mỗi lượt tiếp theo, nó có thể vẽ tối đa một OmniLight3D, một SpotLight3D và một DirectionalLight3D có bóng. Các nguồn sáng có bóng sẽ ảnh hưởng đến cảnh khác với các nguồn sáng không có bóng, vì ánh sáng được trộn trong không gian sRGB thay vì không gian tuyến tính. Sự khác biệt này trong ánh sáng sẽ ảnh hưởng đến diện mạo của cảnh và cần được lưu ý khi thiết kế cảnh cho trình kết xuất Compatibility.

Do tập trung vào phần cứng cấp thấp, phương thức kết xuất này không cung cấp các tính năng kết xuất cao cấp (thậm chí còn ít hơn so với Mobile). Hầu hết các hiệu ứng hậu xử lý đều không khả dụng.

Tại sao không sử dụng kết xuất deferred?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kết xuất tiến nhìn chung mang lại sự cân bằng tốt hơn giữa hiệu năng và tính linh hoạt, đặc biệt khi sử dụng phương pháp chiếu sáng phân cụm. Mặc dù kết xuất deferred có thể nhanh hơn trong một số trường hợp, nó cũng kém linh hoạt hơn và yêu cầu sử dụng các thủ thuật để có thể dùng MSAA. Vì các trò chơi có phong cách nghệ thuật ít chân thực hơn có thể hưởng lợi nhiều từ MSAA, chúng tôi đã chọn kết xuất tiến cho Godot 4 (giống như Godot 3).

Tuy vậy, một số phần của trình kết xuất tiến *được* thực hiện theo phương pháp deferred để cho phép một số tối ưu hóa khi có thể. Điều này đặc biệt áp dụng cho VoxelGI và SDFGI.

Một trình kết xuất deferred phân cụm có thể được phát triển trong tương lai. Trình kết xuất này có thể được sử dụng trong các tình huống ưu tiên hiệu năng hơn tính linh hoạt.

Các trình điều khiển kết xuất
-----------------------------

Godot 4 hỗ trợ các API đồ họa sau:

Vulkan
~~~~~~

Đây là trình điều khiển chính trong Godot 4, với phần lớn trọng tâm phát triển hướng đến trình điều khiển này.

Vulkan 1.0 là nền tảng bắt buộc, với các tính năng Vulkan 1.1 và 1.2 tùy chọn được sử dụng khi khả dụng. `volk <https://github.com/zeux/volk>`__ được sử dụng làm trình nạp Vulkan, còn `Vulkan Memory Allocator <https://github.com/GPUOpen-LibrariesAndSDKs/VulkanMemoryAllocator>`__ được sử dụng để quản lý bộ nhớ.

Cả Forward+ và Mobile
:ref:`doc_internal_rendering_architecture_methods` are supported when using the
đều sử dụng trình điều khiển Vulkan.

**Tạo context Vulkan:**

- `drivers/vulkan/rendering_context_driver_vulkan.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/vulkan/rendering_context_driver_vulkan.cpp>`__

**Tạo context Direct3D 12:**

- `drivers/d3d12/rendering_context_driver_d3d12.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/d3d12/rendering_context_driver_d3d12.cpp>`__

Direct3D 12
~~~~~~~~~~~

Giống như Vulkan, trình điều khiển Direct3D 12 chỉ nhắm đến các nền tảng hiện đại. Nó được thiết kế để nhắm đến cả Windows và Xbox (trong khi Vulkan không thể được sử dụng trực tiếp trên Xbox).

Cả Forward+ và Mobile :ref:`doc_internal_rendering_architecture_methods` đều có thể được sử dụng với Direct3D 12.

:ref:`doc_internal_rendering_architecture_core_shaders` are shared with the
trình kết xuất Vulkan. Shader được chuyển đổi từ
:abbr:`SPIR-V (Standard Portable Intermediate Representation)` to
:abbr:`DXIL (DirectX Intermediate Language)` using
Mesa NIR (`thông tin thêm <https://godotengine.org/article/d3d12-adventures-in-shaderland/>`__).

**Trình điều khiển này vẫn đang ở giai đoạn thử nghiệm và chỉ khả dụng trong Godot 4.3 trở lên.** Mặc dù Direct3D 12 cho phép hỗ trợ các tính năng độc quyền của Direct3D trên Windows 11, chẳng hạn như tối ưu hóa cửa sổ và Auto HDR, Vulkan vẫn được khuyến nghị cho hầu hết các dự án. Xem `pull request đã giới thiệu hỗ trợ Direct3D 12 <https://github.com/godotengine/godot/pull/70315>`__ để biết thêm thông tin.

Metal
~~~~~

Godot cung cấp trình điều khiển Metal gốc hoạt động trên mọi phần cứng Apple Silicon (macOS ARM). So với việc sử dụng lớp chuyển đổi MoltenVK, cách này nhanh hơn đáng kể, đặc biệt trong các tình huống bị giới hạn bởi CPU.

Cả :ref:`doc_internal_rendering_architecture_methods` Forward+ và Mobile đều có thể được sử dụng với Metal.

:ref:`doc_internal_rendering_architecture_core_shaders` are shared with the
Trình kết xuất Vulkan. Shader được chuyển đổi từ GLSL sang :abbr:`MSL (Metal Shading Language)` bằng SPIRV-Cross.

Godot cũng hỗ trợ kết xuất Metal thông qua `MoltenVK <https://github.com/KhronosGroup/MoltenVK>`__, được sử dụng làm phương án dự phòng khi không có hỗ trợ Metal gốc (ví dụ: trên macOS x86).

Kể từ Godot 4.7, Metal 4 sẽ được sử dụng khi được hỗ trợ. Mọi phần cứng Apple Silicon đều hỗ trợ Metal 4, nhưng phải chạy macOS 26 trở lên hoặc iOS 26 trở lên. Metal 3 sẽ tự động được sử dụng làm phương án dự phòng trên các phiên bản macOS và iOS cũ hơn. Xem `pull request giới thiệu hỗ trợ Metal 4 <https://github.com/godotengine/godot/pull/114484>`__ để biết thêm thông tin.

OpenGL
~~~~~~

Trình điều khiển này sử dụng OpenGL ES 3.0 và nhắm đến các thiết bị cũ cũng như cấp thấp không hỗ trợ Vulkan. OpenGL 3.3 Core Profile được sử dụng trên các nền tảng máy tính để bàn nhằm chạy trình điều khiển này, vì hầu hết trình điều khiển đồ họa trên máy tính để bàn không hỗ trợ OpenGL ES. WebGL 2.0 được sử dụng cho các bản xuất web.

Có thể sử dụng trực tiếp OpenGL ES 3.0 trên các nền tảng máy tính để bàn bằng cách truyền đối số dòng lệnh ``--rendering-driver opengl3_es``, mặc dù cách này chỉ hoạt động trên các trình điều khiển đồ họa có hỗ trợ OpenGL ES gốc (chẳng hạn như Mesa).

Chỉ phương thức kết xuất :ref:`doc_internal_rendering_architecture_compatibility` mới có thể được sử dụng với trình điều khiển OpenGL.

:ref:`doc_internal_rendering_architecture_core_shaders` are entirely different
từ trình kết xuất Vulkan.

Nhiều tính năng nâng cao không được hỗ trợ với trình điều khiển này, vì ưu tiên hàng đầu của nó là nhắm đến các thiết bị cấp thấp.

Tóm tắt các trình điều khiển/phương thức kết xuất
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiện có thể sử dụng các tổ hợp API kết xuất + phương thức kết xuất sau:

- Vulkan + Forward+ (tùy chọn thông qua MoltenVK trên macOS và iOS) - Vulkan + Mobile (tùy chọn thông qua MoltenVK trên macOS và iOS) - Direct3D 12 + Forward+ - Direct3D 12 + Mobile - Metal + Forward+ - Metal + Mobile - OpenGL + Compatibility (tùy chọn thông qua ANGLE trên Windows và macOS)

Mỗi tổ hợp có những giới hạn và đặc tính hiệu năng riêng. Nếu có thể, hãy đảm bảo kiểm tra các thay đổi của bạn trên tất cả phương thức kết xuất trước khi mở một pull request.

Lớp trừu tượng RenderingDevice
------------------------------

.. note::

    Trình điều khiển OpenGL không sử dụng lớp trừu tượng RenderingDevice.

Để giúp quản lý độ phức tạp của các API đồ họa cấp thấp hiện đại dễ dàng hơn, Godot sử dụng lớp trừu tượng riêng có tên là RenderingDevice.

Điều này có nghĩa là khi viết mã cho các phương thức kết xuất hiện đại, bạn không thực sự sử dụng trực tiếp các API Vulkan, Direct3D 12 hoặc Metal. Mặc dù vẫn ở cấp thấp hơn một API như OpenGL, điều này giúp làm việc trên trình kết xuất dễ dàng hơn, vì RenderingDevice sẽ trừu tượng hóa nhiều khác biệt riêng của từng API cho bạn. RenderingDevice cung cấp mức độ trừu tượng tương tự như WebGPU.

**Triển khai RenderingDevice cho Vulkan:**

- `drivers/vulkan/rendering_device_driver_vulkan.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/vulkan/rendering_device_driver_vulkan.cpp>`__

**Triển khai RenderingDevice cho Direct3D 12:**

- `drivers/d3d12/rendering_device_driver_d3d12.cpp <https://github.com/godotengine/godot/blob/4.6/drivers/d3d12/rendering_device_driver_d3d12.cpp>`__

**Triển khai RenderingDevice cho Metal:**

- `drivers/metal/rendering_device_driver_metal.cpp <https://github.com/godotengine/godot/blob/master/drivers/metal/rendering_device_driver_metal.cpp>`__ - Metal 4 - `drivers/metal/rendering_device_driver_metal3.cpp <https://github.com/godotengine/godot/blob/master/drivers/metal/rendering_device_driver_metal3.cpp>`__ - Metal 3

Kiến trúc các lớp kết xuất cốt lõi
----------------------------------

Sơ đồ này thể hiện cấu trúc của các lớp kết xuất trong Godot, bao gồm cả lớp trừu tượng RenderingDevice:

.. image:: img/rendering_architecture_diagram.webp

`Xem kích thước đầy đủ <https://raw.githubusercontent.com/godotengine/godot-docs/master/engine_details/architecture/img/rendering_architecture_diagram.webp>`__

.. _doc_internal_rendering_architecture_core_shaders:

Shader cốt lõi
--------------

Mặc dù shader trong các dự án Godot được viết bằng một
:ref:`custom language inspired by GLSL <doc_shading_language>`, core shaders are
được viết trực tiếp bằng GLSL.

Các shader cốt lõi này được nhúng vào trình chỉnh sửa và các tệp nhị phân mẫu xuất tại thời điểm biên dịch. Để xem bất kỳ thay đổi nào bạn đã thực hiện đối với các shader GLSL đó, bạn cần biên dịch lại trình chỉnh sửa hoặc tệp nhị phân mẫu xuất.

Một số tính năng vật liệu như lập bản đồ chiều cao, khúc xạ và làm mờ theo khoảng cách không thuộc các shader cốt lõi, mà được thực hiện trong BaseMaterial3D mặc định bằng ngôn ngữ shader Godot thay thế (không phải GLSL). Việc này được thực hiện bằng cách tạo mã shader theo thủ tục, tùy thuộc vào các tính năng được bật trong vật liệu.

Theo quy ước, các tệp shader có ``_inc`` trong tên sẽ được đưa vào các tệp GLSL khác để tái sử dụng mã tốt hơn. Tiền xử lý GLSL tiêu chuẩn được sử dụng để thực hiện việc này.

.. warning::

    Các shader vật liệu cốt lõi sẽ được mọi vật liệu trong cảnh sử dụng – cả BaseMaterial3D mặc định lẫn shader tùy chỉnh. Do đó, các shader này phải được giữ đơn giản nhất có thể để tránh vấn đề về hiệu năng và đảm bảo quá trình biên dịch shader không trở nên quá chậm.

    Nếu bạn sử dụng rẽ nhánh ``if`` trong shader, hiệu năng có thể giảm khi
    :abbr:`VGPR (Vector General-Purpose Register)` usage will increase in the
    shader. Điều này xảy ra ngay cả khi tất cả pixel đều cho kết quả ``true`` hoặc ``false`` trong một khung hình nhất định.

    Nếu bạn sử dụng rẽ nhánh tiền xử lý ``#if``, số lượng phiên bản shader cần thiết trong cảnh sẽ tăng lên. Trong trường hợp xấu nhất, việc thêm một ``#define`` boolean duy nhất có thể *gấp đôi* số phiên bản shader có thể cần được biên dịch trong một cảnh nhất định. Trong một số trường hợp, các hằng số chuyên biệt hóa Vulkan có thể được sử dụng như một giải pháp thay thế nhanh hơn (nhưng hạn chế hơn).

    Điều này có nghĩa là việc thêm các tính năng vật liệu tích hợp mới vào Godot có rào cản rất cao, cả trong các shader cốt lõi lẫn BaseMaterial3D. Mặc dù BaseMaterial3D có thể sử dụng tính năng tạo mã động để chỉ đưa mã shader vào khi tính năng được bật, việc này vẫn đòi hỏi tạo thêm các phiên bản shader khi những tính năng này được sử dụng trong một dự án. Điều này có thể khiến hiện tượng giật do biên dịch shader dễ nhận thấy hơn trong các cảnh 3D phức tạp.

    Xem các bài viết trên blog `The Shader Permutation Problem <https://therealmjp.github.io/posts/shader-permutations-part1/>`__ và `Branching on a GPU <https://medium.com/@jasonbooth_86226/branching-on-a-gpu-18bfc83694f2>`__ để biết thêm thông tin.

**Shader vật liệu GLSL cốt lõi:**

- Forward+: `servers/rendering/renderer_rd/shaders/forward_clustered/scene_forward_clustered.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/forward_clustered/scene_forward_clustered.glsl>`__ - Mobile: `servers/rendering/renderer_rd/shaders/forward_mobile/scene_forward_mobile.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/forward_mobile/scene_forward_mobile.glsl>`__ - Compatibility: `drivers/gles3/shaders/scene.glsl <https://github.com/godotengine/godot/blob/4.6/drivers/gles3/shaders/scene.glsl>`__

**Tạo shader vật liệu:**

- `scene/resources/material.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/material.cpp>`__

**Các shader GLSL khác cho các phương thức kết xuất Forward+ và Mobile:**

- `servers/rendering/renderer_rd/shaders/ <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/>`__ - `modules/lightmapper_rd/ <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd>`__

**Các shader GLSL khác cho phương thức kết xuất Compatibility:**

- `drivers/gles3/shaders/ <https://github.com/godotengine/godot/blob/4.6/drivers/gles3/shaders/>`__

Tách biệt kết xuất 2D và 3D
---------------------------

.. note::

    Nội dung sau chỉ áp dụng cho các phương thức kết xuất Forward+ và Mobile, không áp dụng cho Compatibility. Có thể sử dụng nhiều Viewport để mô phỏng điều này khi sử dụng trình kết xuất Compatibility hoặc để thực hiện điều chỉnh tỷ lệ độ phân giải 2D.

2D và 3D được kết xuất vào các bộ đệm riêng biệt, vì kết xuất 2D trong Godot được thực hiện trong không gian sRGB :abbr:`LDR (Low Dynamic Range)`, trong khi kết xuất 3D sử dụng
:abbr:`HDR (High Dynamic Range)` linear space.

Định dạng màu được sử dụng cho kết xuất 2D là RGB8 (RGBA8 nếu thuộc tính **Transparent** trên Viewport được bật). Kết xuất 3D sử dụng bộ đệm độ sâu số nguyên chuẩn hóa không dấu 24 bit hoặc số dấu phẩy động có dấu 32 bit nếu phần cứng không hỗ trợ bộ đệm độ sâu 24 bit. Kết xuất 2D không sử dụng bộ đệm độ sâu.

Việc điều chỉnh tỷ lệ độ phân giải 3D được thực hiện khác nhau tùy thuộc vào việc sử dụng điều chỉnh tỷ lệ song tuyến tính hay FSR 1.0. Khi sử dụng điều chỉnh tỷ lệ song tuyến tính, không có shader nâng tỷ lệ đặc biệt nào được chạy. Thay vào đó, kết cấu của viewport được kéo giãn và hiển thị bằng bộ lấy mẫu tuyến tính (khiến quá trình lọc diễn ra trực tiếp trên phần cứng). Điều này cho phép tối đa hóa hiệu năng của việc điều chỉnh tỷ lệ 3D song tuyến tính.

Hàm ``configure()`` trong RenderSceneBuffersRD phân bổ lại các bộ đệm 2D/3D khi độ phân giải hoặc tỷ lệ điều chỉnh thay đổi.

.. CẬP NHẬT: Tính năng đã lên kế hoạch. Khi hỗ trợ điều chỉnh tỷ lệ độ phân giải động, .. hãy cập nhật đoạn này.

Điều chỉnh tỷ lệ độ phân giải động hiện chưa được hỗ trợ, nhưng đã được lên kế hoạch cho một bản phát hành Godot trong tương lai.

**Mã C++ cấu hình bộ đệm kết xuất 2D và 3D:**

- `servers/rendering/renderer_rd/storage_rd/render_scene_buffers_rd.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/storage_rd/render_scene_buffers_rd.cpp>`__

**FSR 1.0:**

- `servers/rendering/renderer_rd/effects/fsr.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/fsr.cpp>`__ - `thirdparty/amd-fsr/ <https://github.com/godotengine/godot/tree/master/thirdparty/amd-fsr>`__

Các kỹ thuật kết xuất 2D
------------------------

Kết xuất ánh sáng 2D được thực hiện trong một lượt duy nhất để mang lại hiệu năng tốt hơn khi có số lượng lớn đèn.

Tất cả các phương thức kết xuất đều có tính năng gộp lô 2D để cải thiện hiệu năng, đặc biệt dễ nhận thấy khi có nhiều văn bản trên màn hình.

MSAA có thể được bật trong 2D để cung cấp tính khử răng cưa "tự động" cho đường thẳng và đa giác, nhưng FXAA không ảnh hưởng đến kết xuất 2D vì nó được tính toán trước khi quá trình kết xuất 2D bắt đầu. Các phương thức vẽ 2D của Godot, chẳng hạn như node Line2D hoặc một số phương thức ``draw_*()`` của CanvasItem, cung cấp cách khử răng cưa riêng dựa trên các dải tam giác và màu đỉnh, không yêu cầu MSAA để hoạt động.

Một trường khoảng cách có dấu 2D biểu diễn các node LightOccluder2D trong khung nhìn sẽ được tự động tạo nếu shader người dùng yêu cầu. Trường này có thể được dùng cho nhiều hiệu ứng khác nhau trong các shader tùy chỉnh, chẳng hạn như chiếu sáng toàn cục 2D. Nó cũng được dùng để tính toán va chạm của hạt trong 2D.

**Shader GLSL tạo SDF 2D:**

- `servers/rendering/renderer_rd/shaders/canvas_sdf.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/canvas_sdf.glsl>`__

Kỹ thuật kết xuất 3D
--------------------

Z đảo ngược
~~~~~~~~~~~

Tất cả renderer của Godot đều sử dụng Z đảo ngược. Điều này có nghĩa là bộ đệm độ sâu bị đảo ngược, trong đó ``1.0`` biểu thị mặt phẳng gần và ``0.0`` biểu thị mặt phẳng xa. Điều này cho phép có `độ chính xác tốt hơn <https://developer.nvidia.com/content/depth-precision-visualized>`__, đặc biệt ở khoảng cách xa.

Batching và instancing
~~~~~~~~~~~~~~~~~~~~~~

Trong renderer Forward+, instancing của Vulkan được sử dụng để nhóm việc kết xuất các đối tượng đục hoặc được kiểm tra alpha giống hệt nhau nhằm cải thiện hiệu năng. (Các đối tượng pha trộn alpha không bao giờ được instance.) Cách này không nhanh bằng việc hợp nhất mesh tĩnh, nhưng vẫn cho phép loại bỏ từng instance riêng lẻ.

Kết xuất ánh sáng, decal và probe phản xạ
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

  Kết xuất decal hiện chưa khả dụng trong renderer Compatibility.

Renderer Forward+ sử dụng chiếu sáng theo cụm. Điều này cho phép sử dụng bao nhiêu đèn tùy ý; hiệu năng phần lớn phụ thuộc vào độ phủ màn hình. Các đèn không có bóng có thể gần như không tốn chi phí nếu chúng không chiếm nhiều không gian trên màn hình.

Tất cả phương thức kết xuất cũng hỗ trợ kết xuất tối đa 8 đèn định hướng cùng lúc (mặc dù chất lượng bóng sẽ thấp hơn khi có nhiều hơn một đèn bật bóng).

Renderer Mobile sử dụng phương pháp chiếu sáng một lượt, với giới hạn 8 OmniLight + 8 SpotLight tác động lên mỗi *resource* Mesh (cùng giới hạn 256 OmniLight + 256 SpotLight trong khung nhìn của camera). Các giới hạn này được hardcode và không thể điều chỉnh trong cài đặt dự án.

Renderer Compatibility sử dụng phương pháp chiếu sáng lai giữa một lượt và nhiều lượt. Các đèn không có bóng được kết xuất trong một lượt. Các đèn có bóng được kết xuất qua nhiều lượt. Điều này cần thiết vì lý do hiệu năng trên thiết bị di động. Do đó, hiệu năng không mở rộng tốt khi có nhiều đèn đổ bóng. Khuyến nghị tại một thời điểm chỉ nên có một số ít đèn có bóng trong frustum của camera, đồng thời các đèn đó nên được bố trí cách xa nhau để mỗi đối tượng chỉ bị tác động bởi 1 hoặc 2 đèn có bóng tại một thời điểm. Có thể điều chỉnh số lượng đèn tối đa nhìn thấy cùng lúc trong cài đặt dự án.

.. CẬP NHẬT: Tính năng đã lên kế hoạch. Khi việc kết xuất bóng tĩnh và động được .. tách riêng, hãy cập nhật đoạn này.

Trong cả 3 phương thức, các đèn không có bóng rẻ hơn nhiều so với các đèn có bóng. Để cải thiện hiệu năng, đèn chỉ được cập nhật khi bản thân đèn bị sửa đổi hoặc khi các đối tượng trong bán kính của nó bị sửa đổi. Hiện tại Godot chưa tách việc kết xuất bóng tĩnh khỏi kết xuất bóng động, nhưng điều này đã được lên kế hoạch cho một bản phát hành trong tương lai.

Clustering cũng được sử dụng cho probe phản xạ và kết xuất decal trong renderer Forward+.

Đèn vùng sử dụng kỹ thuật `Linearly Transformed Cosines <https://eheitzresearch.wordpress.com/757-2/>`__.

Lập bản đồ bóng
~~~~~~~~~~~~~~~

Cả phương thức Forward+ và Mobile đều sử dụng
:abbr:`PCF (Percentage Closer Filtering)` to filter shadow maps and create a
penumbra mềm. Thay vì sử dụng một mẫu PCF cố định, các phương thức này sử dụng mẫu đĩa vogel, cho phép thay đổi số lượng mẫu và thay đổi chất lượng một cách mượt mà.

Godot cũng hỗ trợ bóng mềm gần điểm ảnh (PCSS) để kết xuất penumbra của bóng chân thực hơn. Bóng PCSS bị giới hạn ở renderer Forward+ vì chúng đòi hỏi quá nhiều tài nguyên để có thể sử dụng trong renderer Mobile. PCSS cũng sử dụng kernel có hình dạng đĩa vogel.

Ngoài ra, cả hai kỹ thuật lập bản đồ bóng đều xoay kernel theo từng pixel để giúp làm mềm các hiện tượng giả do lấy mẫu thiếu.

Renderer Compatibility hỗ trợ lập bản đồ bóng cho các đèn DirectionalLight3D, OmniLight3D và SpotLight3D.

Khử răng cưa tạm thời
~~~~~~~~~~~~~~~~~~~~~

.. note::

    Chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.

Godot sử dụng một triển khai TAA tùy chỉnh dựa trên triển khai TAA cũ từ `Spartan Engine <https://github.com/PanosK92/SpartanEngine>`__.

Khử răng cưa tạm thời yêu cầu vector chuyển động để hoạt động. Nếu vector chuyển động không được tạo chính xác, hiện tượng bóng mờ sẽ xảy ra khi camera hoặc các đối tượng di chuyển.

Vector chuyển động được tạo trên GPU trong shader vật liệu chính. Việc này được thực hiện bằng cách chạy shader đỉnh tương ứng với khung hình đã kết xuất trước đó (với phép biến đổi camera trước đó) ngoài shader đỉnh của khung hình hiện tại, sau đó lưu chênh lệch giữa chúng vào một bộ đệm màu.

Ngoài ra, có thể sử dụng FSR 2.2 làm giải pháp nâng cấp độ phân giải, đồng thời cung cấp thuật toán khử răng cưa tạm thời riêng. FSR 2.2 được triển khai trên lớp trừu tượng RenderingDevice thay vì sử dụng trực tiếp mã tham chiếu của AMD.

**Tổng hợp TAA:**

- `servers/rendering/renderer_rd/shaders/effects/taa_resolve.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/taa_resolve.glsl>`__

**FSR 2.2:**

- `servers/rendering/renderer_rd/effects/fsr2.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/fsr2.cpp>`__ - `servers/rendering/renderer_rd/shaders/effects/fsr2/ <https://github.com/godotengine/godot/tree/master/servers/rendering/renderer_rd/shaders/effects/fsr2>`__ - `thirdparty/amd-fsr2/ <https://github.com/godotengine/godot/tree/master/thirdparty/amd-fsr2>`__

Chiếu sáng toàn cục
~~~~~~~~~~~~~~~~~~~

.. note::

    VoxelGI và SDFGI chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.

    Việc *bake* LightmapGI chỉ khả dụng trong renderer Forward+ và Mobile, đồng thời chỉ có thể được thực hiện trong editor (không phải trong project đã export). Renderer Compatibility hỗ trợ *kết xuất* LightmapGI.

Godot hỗ trợ GI dựa trên voxel (VoxelGI), GI bằng trường khoảng cách có dấu (SDFGI) và bake cũng như kết xuất lightmap (LightmapGI). Có thể sử dụng đồng thời các kỹ thuật này nếu muốn.

Việc bake lightmap diễn ra trên GPU bằng compute shader Vulkan. Lightmapper dựa trên GPU được triển khai trong lớp LightmapperRD, lớp này kế thừa từ lớp Lightmapper. Điều này cho phép triển khai thêm các lightmapper, mở đường cho việc chuyển lightmapper dựa trên CPU hiện có trong Godot 3.x trong tương lai. Nhờ đó, có thể bake lightmap khi sử dụng renderer Compatibility.

**Mã C++ GI cốt lõi:**

- `servers/rendering/renderer_rd/environment/gi.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/environment/gi.cpp>`__ - `scene/3d/voxel_gi.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/voxel_gi.cpp>`__ - node VoxelGI - `editor/scene/3d/voxel_gi_editor_plugin.cpp <https://github.com/godotengine/godot/blob/4.6/editor/scene/3d/voxel_gi_editor_plugin.cpp>`__ - Giao diện editor cho node VoxelGI

**Shader GLSL GI cốt lõi:**

- `servers/rendering/renderer_rd/shaders/environment/voxel_gi.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/voxel_gi.glsl>`__ - `servers/rendering/renderer_rd/shaders/environment/voxel_gi_debug.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/voxel_gi_debug.glsl>`__ - chế độ vẽ gỡ lỗi VoxelGI - `servers/rendering/renderer_rd/shaders/environment/sdfgi_debug.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_debug.glsl>`__ - chế độ vẽ gỡ lỗi Cascades SDFGI - `servers/rendering/renderer_rd/shaders/environment/sdfgi_debug_probes.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_debug_probes.glsl>`__ - chế độ vẽ gỡ lỗi Probes SDFGI - `servers/rendering/renderer_rd/shaders/environment/sdfgi_integrate.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_integrate.glsl>`__ - `servers/rendering/renderer_rd/shaders/environment/sdfgi_preprocess.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_preprocess.glsl>`__ - `servers/rendering/renderer_rd/shaders/environment/sdfgi_direct_light.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/sdfgi_direct_light.glsl>`__

**Mã C++ Lightmapper:**

- `scene/3d/lightmap_gi.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/lightmap_gi.cpp>`__ - node LightmapGI - `editor/scene/3d/lightmap_gi_editor_plugin.cpp <https://github.com/godotengine/godot/blob/4.6/editor/scene/3d/lightmap_gi_editor_plugin.cpp>`__ - Giao diện editor cho node LightmapGI - `scene/3d/lightmapper.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/lightmapper.cpp>`__ - Lớp trừu tượng - `modules/lightmapper_rd/lightmapper_rd.cpp <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lightmapper_rd.cpp>`__ - triển khai lightmapper dựa trên GPU

**Shader GLSL Lightmapper:**

- `modules/lightmapper_rd/lm_raster.glsl <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lm_raster.glsl>`__ - `modules/lightmapper_rd/lm_compute.glsl <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lm_compute.glsl>`__ - `modules/lightmapper_rd/lm_blendseams.glsl <https://github.com/godotengine/godot/blob/4.6/modules/lightmapper_rd/lm_blendseams.glsl>`__

Độ sâu trường ảnh
~~~~~~~~~~~~~~~~~

.. note::

    Chỉ khả dụng trong renderer Forward+ và Mobile, không khả dụng trong renderer Compatibility.

Renderer Forward+ và Mobile sử dụng các phương pháp khác nhau để kết xuất DOF, với kết quả hình ảnh khác nhau. Việc này nhằm phù hợp nhất với đặc tính hiệu năng của phần cứng mục tiêu. Trong Forward+, DOF được thực hiện bằng compute shader. Trong Mobile, DOF được thực hiện bằng fragment shader (raster).

Có các hình dạng bokeh hình hộp, lục giác và tròn (từ nhanh nhất đến chậm nhất). Có thể tùy chọn làm rung độ sâu trường ảnh ở mỗi khung hình để cải thiện hình ảnh khi bật khử răng cưa tạm thời.

**Mã C++ độ sâu trường ảnh:**

- `servers/rendering/renderer_rd/effects/bokeh_dof.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/bokeh_dof.cpp>`__

**Shader GLSL độ sâu trường ảnh (compute - dùng cho Forward+):**

- `servers/rendering/renderer_rd/shaders/effects/bokeh_dof.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/bokeh_dof.glsl>`__

**Shader GLSL độ sâu trường ảnh (raster - dùng cho Mobile):**

- `servers/rendering/renderer_rd/shaders/effects/bokeh_dof_raster.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/bokeh_dof_raster.glsl>`__

Các hiệu ứng trong không gian màn hình (SSAO, SSIL, SSR, SSS)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Chỉ khả dụng trong renderer Forward+, không khả dụng trong renderer Mobile hoặc Compatibility.

Trình kết xuất Forward+ hỗ trợ ambient occlusion trong không gian màn hình, ánh sáng gián tiếp trong không gian màn hình, phản xạ trong không gian màn hình và tán xạ dưới bề mặt.

SSAO sử dụng một triển khai bắt nguồn từ `ASSAO <https://www.intel.com/content/www/us/en/developer/articles/technical/adaptive-screen-space-ambient-occlusion.html>`__ của Intel (được chuyển đổi sang Vulkan). SSIL bắt nguồn từ SSAO để cung cấp ánh sáng gián tiếp hiệu năng cao.

Khi cả SSAO và SSIL được bật, một số phần của SSAO và SSIL được dùng chung để giảm tác động đến hiệu năng.

Theo mặc định, SSAO, SSIL và SSR được thực hiện ở độ phân giải bằng một nửa để cải thiện hiệu năng.

SSR sử dụng bộ đệm Hi-Z để cải thiện hiệu năng. Bộ đệm Hi-Z này được tạo từ bộ đệm độ sâu trong compute shader. Xem `pull request that overhauled SSR <https://github.com/godotengine/godot/pull/111210>`__ để biết thêm thông tin.

**Mã C++ của các hiệu ứng trong không gian màn hình:**

- `servers/rendering/renderer_rd/effects/ss_effects.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/effects/ss_effects.cpp>`__

**GLSL shader của ambient occlusion trong không gian màn hình:**

- `servers/rendering/renderer_rd/shaders/effects/ssao.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/ssao_blur.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao_blur.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/ssao_interleave.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao_interleave.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/ssao_importance_map.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssao_importance_map.glsl>`__

**GLSL shader của ánh sáng gián tiếp trong không gian màn hình:**

- `servers/rendering/renderer_rd/shaders/effects/ssil.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/ssil_blur.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil_blur.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/ssil_interleave.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil_interleave.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/ssil_importance_map.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/ssil_importance_map.glsl>`__

**GLSL shader của phản xạ trong không gian màn hình:**

- `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_filter.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_filter.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_resolve.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_resolve.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_hiz.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_hiz.glsl>`__ - `servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_downsample.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/screen_space_reflection_downsample.glsl>`__

**GLSL của tán xạ dưới bề mặt:**

- `servers/rendering/renderer_rd/shaders/effects/subsurface_scattering.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/effects/subsurface_scattering.glsl>`__

Kết xuất bầu trời
~~~~~~~~~~~~~~~~~

.. seealso::

    :ref:`doc_sky_shader`

Godot hỗ trợ sử dụng shader để kết xuất nền bầu trời. Bản đồ bức xạ (được dùng để cung cấp ánh sáng môi trường và phản xạ cho các vật liệu PBR) được tự động cập nhật dựa trên sky shader.

Các tài nguyên SkyMaterial như ProceduralSkyMaterial, PhysicalSkyMaterial và PanoramaSkyMaterial tạo một shader tích hợp sẵn để kết xuất bầu trời. Điều này tương tự như những gì BaseMaterial3D cung cấp cho các vật liệu cảnh 3D.

Có thể tìm thấy phần triển khai kỹ thuật chi tiết trong bài viết `Custom sky shaders in Godot 4.0 <https://godotengine.org/article/custom-sky-shaders-godot-4-0>`__.

**Mã C++ của kết xuất bầu trời:**

- `servers/rendering/renderer_rd/environment/sky.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/environment/sky.cpp>`__ - Kết xuất bầu trời - `scene/resources/sky.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/sky.cpp>`__ - Tài nguyên bầu trời (không nên nhầm với việc kết xuất bầu trời) - `scene/resources/3d/sky_material.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/3d/sky_material.cpp>`__ Các tài nguyên SkyMaterial (được sử dụng trong tài nguyên Sky)

**GLSL shader của kết xuất bầu trời:**

Sương mù thể tích
~~~~~~~~~~~~~~~~~

.. note::

    Chỉ khả dụng trong trình kết xuất Forward+, không khả dụng trong trình kết xuất Mobile hoặc Compatibility.

.. seealso::

    :ref:`doc_fog_shader`

Godot hỗ trợ phương pháp voxel căn chỉnh theo frustum (froxel) để kết xuất sương mù thể tích. Không giống như bộ lọc hậu kỳ, phương pháp này có mục đích sử dụng tổng quát hơn vì có thể hoạt động với mọi loại ánh sáng. Sương mù cũng có thể sử dụng shader cho hành vi tùy chỉnh, cho phép tạo hiệu ứng chuyển động cho sương mù hoặc sử dụng texture 3D để biểu diễn mật độ.

Tài nguyên FogMaterial tạo một shader tích hợp sẵn cho các node FogVolume. Điều này tương tự như những gì BaseMaterial3D cung cấp cho các vật liệu cảnh 3D.

Có thể tìm thấy phần giải thích kỹ thuật chi tiết trong bài viết `Fog Volumes arrive in Godot 4.0 <https://godotengine.org/article/fog-volumes-arrive-in-godot-4>`__.

**Mã C++ của sương mù thể tích:**

- `servers/rendering/renderer_rd/environment/fog.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/environment/fog.cpp>`__ - Sương mù thể tích tổng quát - `scene/3d/fog_volume.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/fog_volume.cpp>`__ - node FogVolume - `scene/resources/3d/fog_material.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/3d/fog_material.cpp>`__ - tài nguyên FogMaterial (được FogVolume sử dụng)

**Các GLSL shader của sương mù thể tích:**

- `servers/rendering/renderer_rd/shaders/environment/volumetric_fog.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/volumetric_fog.glsl>`__ - `servers/rendering/renderer_rd/shaders/environment/volumetric_fog_process.glsl <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_rd/shaders/environment/volumetric_fog_process.glsl>`__

Culling che khuất
~~~~~~~~~~~~~~~~~

Mặc dù các GPU hiện đại có thể xử lý việc vẽ rất nhiều tam giác, số lượng draw call trong các cảnh phức tạp vẫn có thể là nút thắt cổ chai (ngay cả khi sử dụng Vulkan, Direct3D 12 và Metal).

Godot 4 hỗ trợ culling che khuất để giảm việc vẽ dư (khi tắt bước tiền xử lý độ sâu) và giảm thông lượng vertex. Việc này được thực hiện bằng cách rasterize một bộ đệm độ phân giải thấp trên CPU sử dụng `Embree <https://github.com/embree/embree>`__. Độ phân giải của bộ đệm phụ thuộc vào số luồng CPU trên hệ thống, vì quá trình này được thực hiện song song. Bộ đệm này bao gồm các hình dạng vật cản đã được bake trong trình chỉnh sửa hoặc được tạo trong thời gian chạy. Bộ đệm culling che khuất được làm rung một lượng nhỏ sau mỗi khung hình để giúp giảm các lỗi lấy mẫu thiếu, vốn có thể dẫn đến kết quả dương tính giả (các đối tượng bị che khuất dù không nên bị che khuất).

Vì các vật cản phức tạp có thể gây nhiều tải cho CPU, các vật cản đã bake có thể được tự động đơn giản hóa khi được tạo trong trình chỉnh sửa.

Culling che khuất của Godot hiện chưa hỗ trợ các vật cản động, nhưng các node OccluderInstance3D vẫn có thể bật/tắt khả năng hiển thị hoặc được di chuyển. Tuy nhiên, việc cập nhật các vật cản phức tạp theo cách này sẽ chậm. Do đó, tốt nhất chỉ nên cập nhật vật cản trong thời gian chạy đối với các hình dạng vật cản đơn giản như quad hoặc hình hộp.

Phương pháp dựa trên CPU này có một số ưu điểm so với các giải pháp khác, chẳng hạn như portal và phòng hoặc giải pháp culling dựa trên GPU:

- Không yêu cầu thiết lập thủ công (nhưng có thể tinh chỉnh thủ công để đạt hiệu năng tốt nhất). - Không có độ trễ khung hình, vốn là vấn đề trong các đoạn cắt cảnh khi chuyển camera hoặc khi camera di chuyển nhanh ra phía sau một bức tường. - Hoạt động giống nhau trên mọi trình điều khiển và phương thức kết xuất, không có hành vi không thể dự đoán tùy thuộc vào trình điều khiển hoặc phần cứng GPU.

Culling che khuất được thực hiện bằng cách đăng ký các mesh vật cản, thông qua các *node* OccluderInstance3D (bản thân chúng sử dụng các *resource* Occluder3D). Sau đó, RenderingServer thực hiện culling che khuất bằng cách gọi Embree trong RendererSceneOcclusionCull.

**Mã C++ của culling che khuất:**

- `scene/3d/occluder_instance_3d.cpp <https://github.com/godotengine/godot/blob/4.6/scene/3d/occluder_instance_3d.cpp>`__ - `servers/rendering/renderer_scene_occlusion_cull.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_scene_occlusion_cull.cpp>`__

Phạm vi hiển thị (LOD)
~~~~~~~~~~~~~~~~~~~~~~

Godot hỗ trợ cấp độ chi tiết phân cấp (HLOD) do người dùng tự biên soạn, với khoảng cách được người dùng chỉ định trong inspector.

Trong RenderingSceneCull, các hàm ``_scene_cull()`` và ``_render_scene()`` là nơi phần lớn quá trình xác định LOD diễn ra. Mỗi viewport có thể kết xuất cùng một mesh với các LOD khác nhau (để hiển thị chia đôi màn hình chính xác).

**Mã C++ của phạm vi hiển thị:**

- `servers/rendering/renderer_scene_cull.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_scene_cull.cpp>`__

LOD mesh tự động
~~~~~~~~~~~~~~~~

Lớp ImporterMesh được sử dụng cho quy trình nhập mesh 3D trong trình chỉnh sửa. Hàm ``generate_lods()`` của lớp này xử lý việc tạo bằng thư viện `meshoptimizer <https://meshoptimizer.org/>`__.

Việc tạo mesh LOD cũng đồng thời tạo các mesh bóng đổ. Đây là những mesh có các vertex được hàn lại bất kể việc làm mượt và vật liệu. Việc này được sử dụng để cải thiện hiệu năng kết xuất bóng đổ bằng cách giảm thông lượng vertex cần thiết để kết xuất bóng.

Hàm ``_render_scene()`` của lớp RenderingSceneCull xác định LOD mesh nào sẽ được sử dụng khi kết xuất. Mỗi viewport có thể kết xuất cùng một mesh với các LOD khác nhau (để hiển thị chia đôi màn hình chính xác).

LOD mesh được tự động chọn dựa trên chỉ số độ phủ màn hình. Chỉ số này tính đến các thay đổi về độ phân giải và FOV của camera mà không cần người dùng can thiệp. Hệ số ngưỡng có thể được điều chỉnh trong phần cài đặt dự án.

Để cải thiện hiệu năng, kết xuất bóng đổ và kết xuất probe phản xạ cũng chọn các ngưỡng LOD mesh riêng (có thể khác với ngưỡng của kết xuất cảnh chính).

**Mã C++ tạo mesh LOD khi nhập:**

- `scene/resources/3d/importer_mesh.cpp <https://github.com/godotengine/godot/blob/4.6/scene/resources/3d/importer_mesh.cpp>`__

**Mã C++ xác định mesh LOD:**

- `servers/rendering/renderer_scene_cull.cpp <https://github.com/godotengine/godot/blob/4.6/servers/rendering/renderer_scene_cull.cpp>`__
