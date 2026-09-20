.. _doc_renderers:

Tổng quan về các renderer
=========================

.. seealso::

    Trang này cung cấp tổng quan về các renderer của Godot, tập trung vào sự khác biệt giữa các tính năng rendering của chúng. Để biết thêm chi tiết kỹ thuật về các renderer, hãy xem :ref:`doc_internal_rendering_architecture`.

Giới thiệu
----------

Godot 4 bao gồm ba renderer:

- **Forward+**. Renderer tiên tiến nhất, chỉ phù hợp với các nền tảng desktop. Được sử dụng mặc định trên các nền tảng desktop. Renderer này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm rendering driver và sử dụng backend **RenderingDevice**. - **Mobile**. Có ít tính năng hơn nhưng rendering các scene đơn giản nhanh hơn. Phù hợp với các nền tảng mobile và desktop. Được sử dụng mặc định trên các nền tảng mobile. Renderer này sử dụng **Vulkan**, **Direct3D 12** hoặc **Metal** làm rendering driver và sử dụng backend **RenderingDevice**. - **Compatibility**, đôi khi được gọi là **GL Compatibility**. Renderer kém tiên tiến nhất, phù hợp với các nền tảng desktop và mobile cấp thấp. Được sử dụng mặc định trên nền tảng web. Renderer này sử dụng **OpenGL** làm rendering driver.

Renderer, rendering driver và RenderingDevice
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. figure:: img/renderers_rendering_layers.webp
  :alt: Diagram of rendering layers. The Compatibility renderer runs on the OpenGL
    driver. The Forward+ and Mobile renderers run on RenderingDevice, which can use
    Vulkan, Direct3D 12, or Metal as a rendering driver.
  :align: center

  Godot's rendering abstraction layers.

*Renderer*, hay *rendering method*, xác định những tính năng khả dụng. Hầu hết thời gian, đây là điều duy nhất bạn cần quan tâm. Các renderer của Godot là **Forward+**, **Mobile** và **Compatibility**.

*Rendering driver* cho GPU biết cần làm gì bằng cách sử dụng một graphics API. Godot có thể sử dụng các rendering driver **OpenGL**, **Vulkan**, **Direct3D 12** và **Metal**. Không phải GPU nào cũng hỗ trợ mọi rendering driver, vì vậy không phải GPU nào cũng hỗ trợ tất cả renderer. Vulkan, Direct3D 12 và Metal là các graphics API hiện đại, cấp thấp và yêu cầu phần cứng mới hơn. OpenGL là một graphics API cũ hơn, chạy được trên hầu hết phần cứng.

RenderingDevice là một *rendering backend*, tức lớp trừu tượng nằm giữa renderer và rendering driver. Nó được sử dụng bởi các renderer Forward+ và Mobile, và các renderer này đôi khi được gọi là "RenderingDevice-based renderers".

Chọn renderer
-------------

Việc chọn renderer là một câu hỏi phức tạp và phụ thuộc vào phần cứng của bạn cũng như những nền tảng mà bạn đang phát triển cho. Để bắt đầu:

Chọn **Forward+** nếu:

    - Bạn đang phát triển cho desktop. - Bạn có phần cứng tương đối mới hỗ trợ Vulkan, Direct3D 12 hoặc Metal. - Bạn đang phát triển một game 3D. - Bạn muốn sử dụng các tính năng rendering tiên tiến nhất.

Chọn **Mobile** nếu:

    - Bạn đang phát triển cho các thiết bị mobile đời mới, desktop XR, XR độc lập hoặc desktop. - Bạn có phần cứng tương đối mới hỗ trợ Vulkan, Direct3D 12 hoặc Metal. - Bạn đang phát triển một game 3D. - Bạn muốn sử dụng các tính năng rendering tiên tiến, trong phạm vi các giới hạn của phần cứng mobile.

Chọn **Compatibility** nếu:

    - Bạn đang phát triển cho các thiết bị mobile đời cũ hoặc thiết bị desktop đời cũ. Renderer Compatibility hỗ trợ phạm vi phần cứng rộng nhất. - Bạn đang phát triển cho web. Trong trường hợp này, Compatibility là lựa chọn duy nhất. - Bạn có phần cứng cũ không hỗ trợ Vulkan. Trong trường hợp này, Compatibility là lựa chọn duy nhất. - Bạn đang phát triển một game 2D hoặc một game 3D không cần các tính năng rendering tiên tiến. - Bạn muốn có hiệu năng tốt nhất có thể trên mọi thiết bị và không cần các tính năng rendering tiên tiến.

Hãy nhớ rằng mỗi game đều có những đặc điểm riêng và đây chỉ là điểm khởi đầu. Ví dụ, bạn có thể chọn sử dụng renderer Compatibility dù đang có GPU mới nhất, để hỗ trợ phạm vi phần cứng rộng nhất. Hoặc bạn có thể muốn sử dụng renderer Forward+ cho một game 2D, để dùng các tính năng tiên tiến như compute shader.

Chuyển đổi giữa các renderer
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trong editor, bạn luôn có thể chuyển đổi giữa các renderer bằng cách nhấp vào tên renderer ở góc trên bên phải của editor.

Việc chuyển đổi giữa các renderer có thể yêu cầu một số điều chỉnh thủ công đối với scene, lighting và environment, vì mỗi renderer đều khác nhau. Nhìn chung, việc chuyển đổi giữa các renderer Mobile và Forward+ sẽ yêu cầu ít điều chỉnh hơn so với việc chuyển đổi giữa renderer Compatibility và renderer Forward+ hoặc Mobile.

Kể từ Godot 4.4, khi sử dụng Forward+ hoặc Mobile, nếu Vulkan không được hỗ trợ, engine sẽ chuyển sang Direct3D 12 và ngược lại. Nếu rendering driver dự phòng được thử cũng không được hỗ trợ, engine sẽ chuyển sang Compatibility khi backend RenderingDevice không được hỗ trợ. Điều này cho phép project vẫn chạy được, nhưng giao diện có thể khác với hình thức dự kiến do renderer bị giới hạn hơn. Bạn có thể tắt hành vi này trong project settings bằng cách bỏ chọn
:ref:`Rendering > Rendering Device > Fallback to OpenGL 3<class_ProjectSettings_property_rendering/rendering_device/fallback_to_opengl3>`.

So sánh tính năng
-----------------

Đây không phải là danh sách đầy đủ các tính năng của từng renderer. Nếu một tính năng không được liệt kê ở đây, tính năng đó khả dụng trên tất cả renderer, mặc dù có thể nhanh hơn nhiều trên một số renderer. Để xem danh sách *tất cả* tính năng trong Godot, hãy xem :ref:`doc_list_of_features`.

Phần cứng có hỗ trợ RenderingDevice là phần cứng có thể chạy Vulkan, Direct3D 12 hoặc Metal.

So sánh tổng quan
~~~~~~~~~~~~~~~~~

.. Lưu ý rằng các bảng này sử dụng emoji, vốn không có độ rộng cố định trong hầu hết editor. .. Các bảng trông có vẻ bị lỗi định dạng nhưng thực ra không phải vậy. Khi thực hiện thay đổi, hãy kiểm tra các dòng .. lân cận để được hướng dẫn.

+---------------------+--------------------------+--------------------------+--------------------------+
| Feature             | Compatibility            | Mobile                   | Forward+                 |
+=====================+==========================+==========================+==========================+
| **Required**        | Older or low-end.        | Newer or high-end.       | Newer or high-end.       |
| **hardware**        |                          | Requires Vulkan, Direct3D| Requires Vulkan, Direct3D|
|                     |                          | 12, or Metal support.    | 12, or Metal support.    |
+---------------------+--------------------------+--------------------------+--------------------------+
| Runs on new hardware| ✔️ Yes.                  | ✔️ Yes.                  | ✔️ Yes.                  |
+---------------------+--------------------------+--------------------------+--------------------------+
| Runs on old and     | ✔️ Yes.                  | ✔️ Yes, but slower than  | ✔️ Yes, but slowest of   |
| low-end hardware    |                          | Compatibility.           | all renderers.           |
+---------------------+--------------------------+--------------------------+--------------------------+
| Runs on hardware    | ✔️ Yes.                  | ❌ No.                   | ❌ No.                   |
| without             |                          |                          |                          |
| RenderingDevice     |                          |                          |                          |
| support             |                          |                          |                          |
+---------------------+--------------------------+--------------------------+--------------------------+
| **Target platforms**| Mobile, low-end desktop, | Mobile, desktop.         | Desktop.                 |
|                     | web.                     |                          |                          |
|                     |                          |                          |                          |
+---------------------+--------------------------+--------------------------+--------------------------+
| Desktop             | ✔️ Yes.                  | ✔️ Yes.                  | ✔️ Yes.                  |
+---------------------+--------------------------+--------------------------+--------------------------+
| Mobile              | ✔️ Yes (low-end).        | ✔️ Yes (high-end).       | ⚠️ Supported, but poorly |
|                     |                          |                          | optimized. Use Mobile or |
|                     |                          |                          | Compatibility instead.   |
+---------------------+--------------------------+--------------------------+--------------------------+
| XR                  | ⚠️ Supported, but not    | ✔️ Yes. Recommended for  | ⚠️ Supported, but poorly |
|                     | recommended. Use Mobile  | desktop and standalone   | optimized. Use Mobile or |
|                     | instead.                 | headsets.                | Compatibility instead.   |
+---------------------+--------------------------+--------------------------+--------------------------+
| Web                 | ✔️ Yes.                  | ❌ No.                   | ❌ No.                   |
+---------------------+--------------------------+--------------------------+--------------------------+
| 2D Games            | ✔️ Yes.                  | ✔️ Yes, but              | ✔️ Yes, but              |
|                     |                          | Compatibility is usually | Compatibility is usually |
|                     |                          | good enough for 2D.      | good enough for 2D.      |
+---------------------+--------------------------+--------------------------+--------------------------+
| 3D Games            | ✔️ Yes.                  | ✔️ Yes.                  | ✔️ Yes.                  |
+---------------------+--------------------------+--------------------------+--------------------------+
| **Feature set**     | 2D and core 3D features. | Most rendering features. | All rendering features.  |
+---------------------+--------------------------+--------------------------+--------------------------+
| 2D rendering        | ✔️ Yes.                  | ✔️ Yes.                  | ✔️ Yes.                  |
| features            |                          |                          |                          |
+---------------------+--------------------------+--------------------------+--------------------------+
| Core 3D rendering   | ✔️ Yes.                  | ✔️ Yes.                  | ✔️ Yes.                  |
| features            |                          |                          |                          |
+---------------------+--------------------------+--------------------------+--------------------------+
| Advanced            | ❌ No.                   | ⚠️ Yes, limited by       | ✔️ Yes. All rendering    |
| rendering features  |                          | mobile hardware.         | features are supported.  |
+---------------------+--------------------------+--------------------------+--------------------------+
| New features        | ⚠️ Some new rendering    | ✔️ Most new rendering    | ✔️ All new features are  |
|                     | features are added to    | features are added to    | added to Forward+. As the|
|                     | Compatibility. Features  | Mobile. Mobile usually   | focus of new development,|
|                     | are added after Mobile   | gets new features as     | Forward+ gets features   |
|                     | and Forward+.            | Forward+ does.           | first.                   |
+---------------------+--------------------------+--------------------------+--------------------------+
| Rendering cost      | Low base cost, but       | Medium base cost, and    | Highest base cost, and   |
|                     | high scaling cost.       | medium scaling cost.     | low scaling cost.        |
+---------------------+--------------------------+--------------------------+--------------------------+
| Rendering driver    | OpenGL.                  | Vulkan, Direct3D 12, or  | Vulkan, Direct3D 12, or  |
|                     |                          | Metal.                   | Metal.                   |
+---------------------+--------------------------+--------------------------+--------------------------+

Đèn và bóng
~~~~~~~~~~~

Xem :ref:`doc_lights_and_shadows` để biết thêm thông tin.

+-------------------------+--------------------------+--------------------------+--------------------------+
| Feature                 | Compatibility            | Mobile                   | Forward+                 |
+=========================+==========================+==========================+==========================+
| Lighting approach       | Forward single-pass.     | Forward single-pass.     | Clustered forward.       |
|                         | Lights with shadows use  |                          |                          |
|                         | a multi-pass approach and|                          |                          |
|                         | less accurate blending.  |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Maximum                 | 8 per mesh. Can be       | 8 per mesh, 256 per view.| 512 per cluster. Can be  |
| OmniLights              | increased.               |                          | increased.               |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Maximum                 | 8 per mesh. Can be       | 8 per mesh, 256 per view.| 512 per cluster. Can be  |
| SpotLights              | increased.               |                          | increased.               |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Maximum                 | 8                        | 8                        | 8                        |
| DirectionalLights       |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| PCSS for                | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| OmniLight and SpotLight |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| PCSS for                | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
| DirectionalLight        |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Light projector         | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| textures                |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+

Global Illumination
~~~~~~~~~~~~~~~~~~~

Xem :ref:`doc_introduction_to_global_illumination` để biết thêm thông tin.

+-------------------------+--------------------------+--------------------------+--------------------------+
| Feature                 | Compatibility            | Mobile                   | Forward+                 |
+=========================+==========================+==========================+==========================+
| ReflectionProbe         | ✔️ Supported, 2 per      | ✔️ Supported, 8 per      | ✔️ Supported, unlimited. |
|                         | mesh.                    | mesh.                    |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| LightmapGI              | ⚠️ Rendering of baked    | ✔️ Supported.            | ✔️ Supported.            |
|                         | lightmaps is supported.  |                          |                          |
|                         | Baking requires hardware |                          |                          |
|                         | with RenderingDevice     |                          |                          |
|                         | support.                 |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| VoxelGI                 | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
|                         |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Screen-Space            | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
| Indirect Lighting (SSIL)|                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Signed Distance Field   | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
| Global Illumination     |                          |                          |                          |
| (SDFGI)                 |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+

Environment và hậu kỳ
~~~~~~~~~~~~~~~~~~~~~

Xem :ref:`doc_environment_and_post_processing` để biết thêm thông tin.

+-------------------------+--------------------------+--------------------------+--------------------------+
| Feature                 | Compatibility            | Mobile                   | Forward+                 |
+=========================+==========================+==========================+==========================+
| Fog (Depth and Height)  | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Volumetric Fog          | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Tonemapping             | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Screen-Space Reflections| ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Screen-Space Ambient    | ✔️ Supported.            | ❌ Not supported.        | ✔️ Supported.            |
| Occlusion (SSAO)        |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Screen-Space            | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
| Indirect Lighting (SSIL)|                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Signed Distance Field   | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
| Global Illumination     |                          |                          |                          |
| (SDFGI)                 |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Glow                    | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Adjustments             | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Custom post-processing  | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
| with fullscreen quad    |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Custom post-processing  | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| with CompositorEffects  |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+

Khử răng cưa
~~~~~~~~~~~~

Xem :ref:`doc_3d_antialiasing` để biết thêm thông tin.

+-------------------+--------------------------+--------------------------+--------------------------+
| Feature           | Compatibility            | Mobile                   | Forward+                 |
+===================+==========================+==========================+==========================+
| MSAA 3D           | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| MSAA 2D           | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| TAA               | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| FSR2              | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| FXAA              | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| SMAA              | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| SSAA              | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------+--------------------------+--------------------------+--------------------------+
| Screen-space      | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| roughness limiter |                          |                          |                          |
+-------------------+--------------------------+--------------------------+--------------------------+

Các tính năng của StandardMaterial
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Xem :ref:`doc_standard_material_3d` để biết thêm thông tin.

+-------------------------+--------------------------+--------------------------+--------------------------+
| Feature                 | Compatibility            | Mobile                   | Forward+                 |
+=========================+==========================+==========================+==========================+
| Sub-surface scattering  | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
|                         |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+

Các tính năng của shader
~~~~~~~~~~~~~~~~~~~~~~~~

Xem :ref:`doc_shading_reference` để biết thêm thông tin.

+-------------------------+--------------------------+--------------------------+--------------------------+
| Feature                 | Compatibility            | Mobile                   | Forward+                 |
+=========================+==========================+==========================+==========================+
| Screen texture          | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Depth texture           | ✔️ Supported.            | ✔️ Supported.            | ✔️ Supported.            |
|                         |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Normal/Roughness buffer | ❌ Not supported.        | ❌ Not supported.        | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Compute shaders         | ❌ Not supported.        | ⚠️ Supported, but comes  | ✔️ Supported.            |
|                         |                          | with a performance       |                          |
|                         |                          | penalty on older devices.|                          |
+-------------------------+--------------------------+--------------------------+--------------------------+

Các tính năng khác
~~~~~~~~~~~~~~~~~~

+-------------------------+--------------------------+--------------------------+--------------------------+
| Feature                 | Compatibility            | Mobile                   | Forward+                 |
+=========================+==========================+==========================+==========================+
| Color precision         | RGBA8. Low dynamic range,| RGB10A2. Medium dynamic  | RGBA16F. High dynamic    |
|                         | medium precision.        | range, low precision.    | range, good precision.   |
|                         |                          | RGBA16F if HDR 2D is     |                          |
|                         |                          | enabled.                 |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Depth precision         | 24-bit without reverse Z.| 24-bit with reverse Z.   | 32-bit with reverse Z.   |
|                         | Medium precision.        | Medium precision.        | Good precision.          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Debanding               | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
|                         |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Variable rate           | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| shading                 |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Decals                  | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Particle trails         | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Particle SDF collision  | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Depth of field blur     | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| Adaptive and Mailbox    | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| VSync modes             |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
| 2D HDR Viewport         | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| HDR output              | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
+-------------------------+--------------------------+--------------------------+--------------------------+
| RenderingDevice         | ❌ Not supported.        | ✔️ Supported.            | ✔️ Supported.            |
| access                  |                          |                          |                          |
+-------------------------+--------------------------+--------------------------+--------------------------+
