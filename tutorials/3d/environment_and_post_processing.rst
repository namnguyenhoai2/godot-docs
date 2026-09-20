.. _doc_environment_and_post_processing:

Môi trường và hậu kỳ
====================

Godot 4 cung cấp một resource Environment được thiết kế lại, cùng với một hệ thống hậu kỳ mới có sẵn nhiều hiệu ứng ngay từ đầu.

.. note::

    Kể từ Godot 4, các thiết lập *hiệu năng/chất lượng* của Environment được định nghĩa trong phần thiết lập project thay vì trong resource Environment. Điều này giúp việc điều chỉnh toàn cục dễ dàng hơn, vì bạn không còn phải tinh chỉnh từng resource Environment riêng lẻ để phù hợp với nhiều cấu hình phần cứng khác nhau.

    Lưu ý rằng hầu hết các thiết lập hiệu năng/chất lượng của Environment chỉ hiển thị sau khi bật nút chuyển **Advanced** trong Project Settings.

Environment
-----------

Resource :ref:`class_Environment` lưu trữ mọi thông tin cần thiết để điều khiển môi trường render 2D và 3D. Các thông tin này bao gồm bầu trời, ánh sáng môi trường, tone mapping, hiệu ứng và các điều chỉnh. Bản thân nó không làm gì cả, nhưng bạn có thể bật nó bằng cách sử dụng ở một trong các vị trí sau, theo thứ tự ưu tiên:

Node Camera3D (ưu tiên cao)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể thiết lập Environment cho một node Camera3D. Environment này sẽ được ưu tiên hơn mọi thiết lập khác.

.. image:: img/environment_camera.webp

Điều này chủ yếu hữu ích khi bạn muốn ghi đè một môi trường hiện có, nhưng nhìn chung, sử dụng tùy chọn bên dưới sẽ tốt hơn.

Node WorldEnvironment (ưu tiên trung bình, khuyến nghị)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Node WorldEnvironment có thể được thêm vào bất kỳ scene nào, nhưng mỗi scene tree đang hoạt động chỉ có thể tồn tại một node. Việc thêm nhiều hơn một node sẽ tạo ra cảnh báo.

.. image:: img/environment_world.webp

Bất kỳ Environment nào được thêm vào cũng có độ ưu tiên cao hơn Environment mặc định (được giải thích bên dưới). Điều này có nghĩa là nó có thể được ghi đè theo từng scene, khiến nó khá hữu ích.

Môi trường và mặt trời xem trước (ưu tiên thấp)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Kể từ Godot 4, hệ thống môi trường và mặt trời xem trước thay thế file ``default_env.tres`` từng được sử dụng trong các project Godot 3.

Nếu không có node WorldEnvironment hoặc node DirectionalLight3D nào trong scene hiện tại, editor sẽ hiển thị môi trường và mặt trời xem trước. Bạn có thể tắt chúng bằng các nút ở phía trên editor 3D:

.. image:: img/environment_preview_sun_sky_toggle.webp

Khi nhấp vào 3 dấu chấm dọc ở bên phải, một hộp thoại sẽ hiển thị, cho phép bạn tùy chỉnh diện mạo của môi trường xem trước:

.. image:: img/environment_preview_sun_sky_dialog.webp

**Mặt trời và bầu trời xem trước chỉ hiển thị trong editor, không hiển thị trong project đang chạy.** Bằng cách sử dụng các nút ở cuối hộp thoại, bạn có thể thêm mặt trời và bầu trời xem trước vào scene dưới dạng các node.

.. tip::

    Nếu giữ :kbd:`Shift` trong khi nhấp vào **Add Sun to Scene** hoặc **Add Environment to Scene** trong trình chỉnh sửa môi trường xem trước, thao tác này sẽ thêm cả mặt trời và môi trường xem trước vào scene hiện tại (như thể bạn đã nhấp riêng từng nút). Sử dụng cách này để tăng tốc quá trình thiết lập và tạo prototype cho project.

Thuộc tính camera
-----------------

.. note::

    Trong Godot 4, thông tin về exposure và depth of field được tách khỏi resource Environment và chuyển sang một resource CameraAttributes riêng biệt. Điều này giúp điều chỉnh các thuộc tính đó độc lập với các thiết lập Environment khác dễ dàng hơn.

Resource :ref:`class_CameraAttributes` lưu trữ thông tin về exposure và depth of field. Nó cũng cho phép bật các điều chỉnh exposure tự động tùy theo độ sáng của scene.

Có hai loại resource CameraAttributes:

- **CameraAttributesPractical:** Các tính năng được thể hiện bằng những đơn vị tùy ý, dễ hình dung hơn trong hầu hết trường hợp sử dụng game. - **CameraAttributesPhysical:** Các tính năng được thể hiện bằng các đơn vị trong thế giới thực, tương tự như máy ảnh kỹ thuật số. Ví dụ, field of view được thiết lập bằng tiêu cự tính theo millimeter thay vì một giá trị tính theo độ. Được khuyến nghị khi độ chính xác vật lý là quan trọng, chẳng hạn như khi render photorealistic.

Cả hai loại resource CameraAttribute đều cho phép bạn sử dụng cùng các tính năng, nhưng chúng được cấu hình theo những cách khác nhau. Nếu không biết nên chọn loại nào, hãy sử dụng **CameraAttributesPractical**.

.. note::

    Việc sử dụng :ref:`class_CameraAttributesPhysical` trên node Camera3D sẽ khóa các điều chỉnh FOV và aspect trong Camera3D đó, vì field of view được điều chỉnh trong resource CameraAttributesPhysical. Nếu được sử dụng trong WorldEnvironment, CameraAttributesPhysical sẽ không ghi đè bất kỳ Camera3D nào trong scene.

Có thể thêm một resource CameraAttributes vào node Camera3D hoặc WorldEnvironment. Khi camera hiện tại có CameraAttributes được thiết lập, nó sẽ *ghi đè* CameraAttributes được thiết lập trong WorldEnvironment (nếu có).

Trong hầu hết trường hợp, nên thiết lập resource CameraAttributes trên node Camera3D thay vì WorldEnvironment. Không giống WorldEnvironment, việc gán resource CameraAttributes cho node Camera3D sẽ ngăn depth of field hiển thị trong viewport editor 3D, trừ khi camera đang được xem trước.

Các tùy chọn Environment
------------------------

Phần sau đây mô tả chi tiết tất cả các tùy chọn của Environment và cách chúng được dự định sử dụng.

Background
~~~~~~~~~~

Phần Background chứa các thiết lập về cách tô nền (những phần trên màn hình nơi các đối tượng không được vẽ). Background không chỉ có mục đích hiển thị hình ảnh hoặc màu sắc. Theo mặc định, nó còn ảnh hưởng đến cách các đối tượng chịu tác động của ánh sáng môi trường và ánh sáng phản xạ. Đây được gọi là image-based lighting (IBL).

Do đó, bầu trời nền có thể ảnh hưởng rất lớn đến diện mạo tổng thể của scene, ngay cả khi bầu trời không bao giờ hiển thị trực tiếp trên màn hình. Bạn nên lưu ý điều này khi tinh chỉnh ánh sáng trong scene.

.. image:: img/environment_background1.webp

Có một số chế độ background khả dụng:

- **Clear Color** sử dụng màu clear mặc định được định nghĩa trong phần thiết lập project. Background sẽ có một màu cố định. - **Custom Color** tương tự Clear Color, nhưng sử dụng giá trị màu tùy chỉnh. - **Sky** cho phép bạn định nghĩa material bầu trời nền (xem bên dưới). Theo mặc định, các đối tượng trong scene sẽ phản chiếu material bầu trời này và hấp thụ ánh sáng môi trường từ nó. - **Canvas** hiển thị scene 2D làm background cho scene 3D. Có thể sử dụng tùy chọn này để làm cho các hiệu ứng môi trường hiển thị trên render 2D, chẳng hạn như
  :ref:`glow in 2D <doc_environment_and_post_processing_using_glow_in_2d>`.
- **Keep** không vẽ bất kỳ bầu trời nào, thay vào đó giữ lại nội dung đã có ở các frame trước. Điều này cải thiện hiệu năng trong các scene hoàn toàn trong nhà, nhưng tạo ra lỗi hình ảnh "hall of mirrors" nếu bầu trời hiển thị vào bất kỳ thời điểm nào. - **Camera Feed** hiển thị một :ref:`class_CameraFeed` từ camera vật lý làm background, hữu ích cho các game AR trên thiết bị di động.

Material bầu trời
~~~~~~~~~~~~~~~~~

Khi sử dụng chế độ background **Sky** (hoặc khi chế độ ánh sáng môi trường/phản xạ được đặt thành **Sky**), một subresource Sky sẽ khả dụng để chỉnh sửa trong resource Environment. Việc chỉnh sửa subresource này cho phép bạn tạo một resource SkyMaterial bên trong Sky.

Có 3 material bầu trời tích hợp sẵn để lựa chọn:

- **PanoramaSkyMaterial:** Sử dụng hình ảnh bầu trời panorama 360 độ (khuyến nghị tỷ lệ khung hình 2:1). Để tận dụng dải tương phản động cao, hình ảnh panorama phải ở định dạng tương thích với HDR như ``.hdr`` hoặc ``.exr``, thay vì định dạng dải tương phản động tiêu chuẩn như ``.png`` hoặc ``.jpg``. - **ProceduralSkyMaterial:** Sử dụng bầu trời được tạo theo quy trình với các màu ground, sun, sky và horizon có thể điều chỉnh. Đây là loại bầu trời được sử dụng trong phần xem trước của editor. Vị trí của mặt trời được tự động suy ra từ 4 node DirectionalLight3D đầu tiên có trong scene. Có thể có tối đa 4 mặt trời tại một thời điểm. - **PhysicalSkyMaterial:** Sử dụng bầu trời được tạo theo quy trình dựa trên vật lý với các tham số tán xạ có thể điều chỉnh. Vị trí của mặt trời được tự động suy ra từ node DirectionalLight3D đầu tiên có trong scene. PhysicalSkyMaterial tốn nhiều chi phí render hơn một chút so với ProceduralSkyMaterial. Có thể có tối đa 1 mặt trời tại một thời điểm.

Hình ảnh bầu trời panorama đôi khi được gọi là HDRI (High Dynamic Range Images). Bạn có thể tìm thấy các HDRI được cấp phép miễn phí trên `Poly Haven <https://polyhaven.com/hdris>`__.

.. note::

    Texture HDR PanoramaSkyMaterial có các điểm quá sáng (chẳng hạn như ảnh chụp thực tế có mặt trời hiển thị) có thể tạo ra những đốm sáng lấp lánh rõ rệt trên các phản xạ môi trường và phản xạ specular. Nguyên nhân là do exposure cực đại của texture quá cao.

    Để khắc phục, hãy chọn texture panorama trong dock FileSystem, chuyển đến dock Import, bật **HDR Clamp Exposure**, sau đó nhấp vào **Reimport**.

Nếu cần một material bầu trời tùy chỉnh (ví dụ: cho mây được tạo theo quy trình), bạn có thể tạo một :ref:`sky shader <doc_sky_shader>` tùy chỉnh.

Ánh sáng môi trường
~~~~~~~~~~~~~~~~~~~

Ánh sáng môi trường (như được định nghĩa ở đây) là một loại ánh sáng tác động lên mọi hình học với cùng cường độ. Đây là ánh sáng toàn cục và độc lập với các nguồn sáng có thể được thêm vào scene. Ánh sáng môi trường là một trong hai thành phần của image-based lighting. Không giống ánh sáng phản xạ, ánh sáng môi trường không thay đổi tùy theo vị trí và góc nhìn của camera.

Có một số loại ánh sáng môi trường để lựa chọn:

- **Bối cảnh:** Lấy ánh sáng môi trường từ bối cảnh, chẳng hạn như bầu trời, màu tùy chỉnh hoặc màu trong suốt (mặc định). Cường độ ánh sáng môi trường sẽ thay đổi tùy theo nội dung của hình ảnh bầu trời, từ đó có thể tạo ra ánh sáng môi trường đẹp mắt hơn. Phải đặt bầu trời làm bối cảnh thì chế độ này mới hiển thị. - **Tắt:** Không sử dụng ánh sáng môi trường. Hữu ích cho các cảnh hoàn toàn trong nhà. - **Màu:** Sử dụng một màu cố định cho ánh sáng môi trường, bỏ qua bầu trời của bối cảnh. Cường độ ánh sáng môi trường sẽ giống nhau ở mọi phía, khiến ánh sáng của cảnh có thể trông phẳng hơn. Hữu ích cho các cảnh trong nhà, nơi bóng đen hoàn toàn có thể quá tối, hoặc để tối đa hóa hiệu năng trên các thiết bị cấp thấp. - **Bầu trời:** Lấy ánh sáng môi trường từ một bầu trời được chỉ định, ngay cả khi bối cảnh được đặt ở chế độ khác **Sky**. Nếu chế độ bối cảnh đã là **Sky**, chế độ này hoạt động giống hệt **Background**.

Khi chế độ ánh sáng môi trường được đặt thành Sky hoặc Background (và bối cảnh được đặt thành Sky), bạn có thể pha trộn giữa màu môi trường và bầu trời bằng thuộc tính **Sky Contribution**. Giá trị này mặc định được đặt thành ``1.0``, nghĩa là chỉ sử dụng bầu trời môi trường. Màu môi trường sẽ bị bỏ qua trừ khi **Sky Contribution** được giảm xuống dưới ``1.0``.

Dưới đây là so sánh về cách các loại ánh sáng môi trường khác nhau ảnh hưởng đến một cảnh:

.. image:: img/environment_ambient2.webp

Cuối cùng, có một thiết lập **Energy** đóng vai trò là một hệ số nhân. Thiết lập này hữu ích khi làm việc với HDR.

Nhìn chung, bạn chỉ nên dựa vào riêng ánh sáng môi trường cho các cảnh đơn giản hoặc ngoại cảnh lớn. Bạn cũng có thể làm vậy để tăng hiệu năng. Ánh sáng môi trường được render nhanh, nhưng không cung cấp chất lượng chiếu sáng tốt nhất. Tốt hơn là tạo ánh sáng môi trường từ :ref:`ReflectionProbe <doc_reflection_probes>`,
:ref:`VoxelGI <doc_using_voxel_gi>` or :ref:`SDFGI <doc_using_sdfgi>`, as these
sẽ mô phỏng chính xác hơn cách ánh sáng gián tiếp lan truyền. Dưới đây là so sánh về chất lượng giữa việc sử dụng một màu môi trường phẳng và VoxelGI:

.. image:: img/environment_ambient_comparison.webp

Sử dụng một trong các phương pháp được mô tả ở trên sẽ thay thế ánh sáng môi trường cố định bằng ánh sáng môi trường từ các probe.

Ánh sáng phản xạ
~~~~~~~~~~~~~~~~

Ánh sáng phản xạ (còn gọi là ánh sáng specular) là một trong hai thành phần của image-based lighting.

Ánh sáng phản xạ có thể được đặt ở một trong 3 chế độ:

- **Bối cảnh:** Phản xạ từ bối cảnh, chẳng hạn như bầu trời, màu tùy chỉnh hoặc màu trong suốt (mặc định). - **Tắt:** Không phản xạ bất kỳ ánh sáng nào từ môi trường. Hữu ích cho các cảnh hoàn toàn trong nhà hoặc để tối đa hóa hiệu năng trên các thiết bị cấp thấp. - **Bầu trời:** Phản xạ từ bầu trời của bối cảnh, ngay cả khi bối cảnh được đặt ở chế độ khác **Sky**. Nếu chế độ bối cảnh đã là **Sky**, chế độ này hoạt động giống hệt **Background**.

Tonemap
~~~~~~~

Tonemap chọn thuật toán tonemapping sẽ được áp dụng cho cảnh từ danh sách các thuật toán tiêu chuẩn được sử dụng trong ngành điện ảnh và game. Các chế độ tonemapping khác **Linear** được dùng để làm cho các vùng sáng và tối đồng đều hơn, đồng thời tránh hiện tượng clipping ở các vùng sáng mạnh. Mỗi thuật toán có đặc điểm hiệu năng khác nhau cần được cân nhắc khi chọn tonemapper.

Các tùy chọn tone mapping là:

- **Mode:** Chế độ tonemapping sẽ sử dụng.

  - **Linear:** Không sửa đổi dữ liệu màu, tạo ra một đường cong tonemapping tuyến tính làm clipping các giá trị sáng một cách không tự nhiên, khiến ánh sáng mạnh trông bị cháy sáng. Tonemapper đơn giản và nhanh nhất. - **Reinhard:** Một đường cong tonemapping đơn giản làm giảm dần các giá trị sáng để tránh clipping. Điều này tạo ra hình ảnh có thể trông xỉn màu và tương phản thấp. Chậm hơn Linear. Khi **White** giữ giá trị mặc định là ``1.0``, Reinhard tạo ra hình ảnh giống hệt Linear. - **Filmic:** Sử dụng đường cong tonemapping giống phim để tránh clipping các giá trị sáng và cung cấp độ tương phản tốt hơn Reinhard. Chậm hơn Reinhard một chút. - **ACES:** Sử dụng đường cong tonemapping giống phim có độ tương phản cao và giảm độ bão hòa của các giá trị sáng để tạo vẻ chân thực hơn. Chậm hơn Filmic một chút. - **AgX:** Sử dụng đường cong tonemapping giống phim và giảm độ bão hòa của các giá trị sáng để tạo vẻ chân thực hơn. Duy trì sắc độ của màu sắc khi chúng trở nên sáng hơn tốt hơn các tonemapper khác. Đây là tùy chọn tonemapping chậm nhất.

- **Exposure:** Điều chỉnh độ sáng của các giá trị trước khi chúng được cung cấp cho tonemapper. Giá trị **Exposure** cao hơn sẽ tạo ra hình ảnh sáng hơn. Các giá trị cung cấp cho tonemapper cũng sẽ được nhân với ``2.0`` và ``1.8`` tương ứng cho **Filmic** và **ACES** để tạo ra độ sáng cảm nhận tương tự như Linear.

- **White:** Giá trị tham chiếu màu trắng cho tonemapping, cho biết vị trí của màu trắng sáng trên thang giá trị được cung cấp cho tonemapper. Đối với ánh sáng chân thực, các giá trị được khuyến nghị nằm trong khoảng từ ``6.0`` đến ``8.0``. Giá trị cao hơn tạo ra các vùng sáng ít bị cháy hơn, nhưng có thể khiến cảnh trông ít tương phản hơn. **White** không khả dụng khi sử dụng **Linear**. Nếu bạn đang sử dụng AgX, mobile renderer và HDR 2D bị tắt, giá trị được đặt ở đây sẽ bị bỏ qua và thay vào đó sẽ sử dụng giá trị ``2.0``.

- **AGX Contrast:** Chỉ khả dụng khi sử dụng AgX. Tăng giá trị này sẽ làm các giá trị tối tối hơn và các giá trị sáng sáng hơn. Nó tạo ra kết quả tốt hơn tùy chọn contrast trong phần điều chỉnh mà không làm tăng chi phí hiệu năng.

Các hiệu ứng mid-processing và post-processing
----------------------------------------------

Tài nguyên Environment hỗ trợ nhiều hiệu ứng mid-processing và post-processing phổ biến.

.. note::

    Các hiệu ứng screen-space như :abbr:`SSR (Screen-Space Reflections)`,
    :abbr:`SSAO (Screen-Space Ambient Occlusion)`,
    :abbr:`SSIL (Screen-Space Indirect Lighting)` and glow do not operate on
    hình học nằm bên ngoài tầm nhìn của camera hoặc bị che khuất bởi hình học mờ đục khác. Hãy cân nhắc điều này khi tinh chỉnh các thiết lập của chúng để tránh những thay đổi gây mất tập trung trong quá trình chơi.

Screen-Space Reflections (SSR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng Forward+, không khả dụng trên Mobile hoặc Compatibility.*

Mặc dù Godot hỗ trợ một số nguồn dữ liệu phản xạ như
:ref:`doc_reflection_probes`, they may not provide enough detail for all
tình huống. Phản xạ screen-space phù hợp nhất trong các trường hợp các đối tượng tiếp xúc với nhau (đối tượng nằm trên sàn, trên bàn, nổi trên mặt nước, v.v.).

.. image:: img/environment_ssr.webp

Ngoài việc cung cấp nhiều chi tiết hơn, phản xạ screen-space còn hoạt động theo thời gian thực (trong khi các loại phản xạ khác thường được tính toán trước). Bạn có thể dùng tính năng này để khiến nhân vật, ô tô, v.v. phản chiếu trên các bề mặt xung quanh khi di chuyển.

Có thể sử dụng phản xạ screen-space đồng thời với các nguồn phản xạ khác để tận dụng phản xạ chi tiết khi có thể, đồng thời có phương án dự phòng khi không thể sử dụng phản xạ screen-space (ví dụ: để phản xạ các đối tượng nằm ngoài màn hình).

Có một số tham số do người dùng điều khiển để tinh chỉnh kỹ thuật này tốt hơn:

- **Max Steps:** Xác định độ dài tối đa của phản xạ. Số này càng lớn thì chi phí tính toán càng cao. - **Fade In:** Cho phép điều chỉnh đường cong fade-in, hữu ích để làm vùng tiếp xúc mềm hơn. - **Fade Out:** Cho phép điều chỉnh đường cong fade-out để giới hạn bước mờ dần một cách mềm mại. - **Depth Tolerance:** Có thể dùng để cho phép các tia screen-space đi xuyên phía sau đối tượng. Khi xác định liệu có thể đi xuyên phía sau đối tượng hay không, các tia sẽ coi mỗi đối tượng như thể nó có độ sâu này. Giá trị cao hơn sẽ khiến phản xạ screen-space xuất hiện ít hiện tượng "breakup" hơn, nhưng phải đánh đổi bằng việc một số đối tượng tạo ra các phản xạ không đúng về mặt vật lý.

Ngoài ra, bạn có thể điều chỉnh chất lượng SSR trong project settings bằng cách bật/tắt **Rendering > Environment > Screen Space Reflection > Half Size**. Theo mặc định, phản xạ screen-space được render ở một nửa độ phân giải vì lý do hiệu năng. Tắt thiết lập này sẽ khiến hiệu ứng được render ở độ phân giải đầy đủ, cải thiện chất lượng nhưng làm tăng mức sử dụng GPU.

.. note::

    Hãy lưu ý rằng phản xạ screen-space chỉ hoạt động với hình học mờ đục. Vật liệu trong suốt sẽ không được phản xạ vì chúng không ghi vào depth buffer. Điều này cũng áp dụng cho các shader sử dụng uniform ``hint_screen_texture`` hoặc ``hint_depth_texture``.

Screen-Space Ambient Occlusion (SSAO)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng các renderer Forward+ và Compatibility, không khả dụng trên Mobile.*

Như đã đề cập trong phần **Ambient**, các khu vực không nhận được ánh sáng từ các light node (do nằm ngoài bán kính hoặc bị che bởi bóng) sẽ được chiếu sáng bằng ánh sáng môi trường. Godot có thể mô phỏng điều này bằng VoxelGI, ReflectionProbe, Sky hoặc một màu môi trường cố định. Tuy nhiên, vấn đề là tất cả các phương pháp được đề cập trước đó đều hoạt động nhiều hơn ở quy mô lớn (các vùng lớn) thay vì ở cấp độ hình học nhỏ hơn.

Màu môi trường cố định và Sky giống nhau ở mọi nơi, trong khi GI và Reflection probe có nhiều chi tiết cục bộ hơn, nhưng chưa đủ để mô phỏng các tình huống ánh sáng không thể lấp đầy bên trong các đặc điểm rỗng hoặc lõm.

Điều này có thể được mô phỏng bằng Screen Space Ambient Occlusion. Như bạn có thể thấy trong hình bên dưới, mục đích của nó là đảm bảo các khu vực lõm tối hơn, mô phỏng một lối hẹp hơn để ánh sáng đi vào:

.. image:: img/environment_ssao.webp

Một sai lầm phổ biến là bật hiệu ứng này, bật một đèn rồi không thể nhận thấy tác dụng của nó. Đó là vì :abbr:`SSAO (Screen-Space Ambient Occlusion)` chỉ tác động lên ánh sáng *môi trường*. Nó không ảnh hưởng đến ánh sáng trực tiếp.

Đó là lý do trong hình trên, hiệu ứng ít nhận thấy hơn dưới ánh sáng trực tiếp (ở bên trái). Nếu bạn muốn buộc
:abbr:`SSAO (Screen-Space Ambient Occlusion)` to work with direct light too,
sử dụng tham số **Light Affect**. Mặc dù điều này không đúng về mặt vật lý, một số họa sĩ thích cách nó hiển thị.

:abbr:`SSAO (Screen-Space Ambient Occlusion)` looks best when combined with a
nguồn sáng gián tiếp thực sự, chẳng hạn như VoxelGI:

.. image:: img/environment_ssao2.webp

Có thể tinh chỉnh :abbr:`SSAO (Screen-Space Ambient Occlusion)` bằng một số tham số:

.. image:: img/environment_ssao_parameters.webp

- **Radius:** Khoảng cách mà tại đó các đối tượng có thể che khuất lẫn nhau khi tính toán ambient occlusion trong không gian màn hình (screen-space ambient occlusion). Giá trị cao hơn sẽ tạo ra hiện tượng che khuất trên khoảng cách lớn hơn, nhưng phải đánh đổi bằng hiệu năng và chất lượng. - **Intensity:** Cường độ chính của ambient occlusion trong không gian màn hình. Hoạt động như một hệ số nhân cho hiệu ứng ambient occlusion trong không gian màn hình. Giá trị cao hơn tạo ra hiện tượng che khuất tối hơn. Vì :abbr:`SSAO (Screen-Space Ambient Occlusion)` là một hiệu ứng trong không gian màn hình, bạn nên giữ giá trị này ở mức thận trọng.
  :abbr:`SSAO (Screen-Space Ambient Occlusion)` that is too strong can be
  gây mất tập trung trong khi chơi. - **Power:** Mức phân bố của hiện tượng che khuất. Giá trị cao hơn tạo ra hiện tượng che khuất tối hơn, tương tự như **Intensity**, nhưng có độ suy giảm rõ hơn. - **Detail:** Thiết lập cường độ của mức độ chi tiết bổ sung cho hiệu ứng ambient occlusion trong không gian màn hình. Giá trị cao làm cho lớp chi tiết nổi bật hơn, nhưng có thể góp phần gây aliasing trong hình ảnh cuối cùng. - **Horizon:** Ngưỡng để xác định một điểm nhất định trên bề mặt có bị che khuất hay không, được biểu diễn dưới dạng một góc tính từ đường chân trời và ánh xạ vào phạm vi 0.0-1.0. Giá trị 1.0 sẽ không tạo ra hiện tượng che khuất. - **Sharpness:** Mức độ mà hiệu ứng ambient occlusion trong không gian màn hình được phép làm mờ qua các cạnh của đối tượng. Đặt quá cao sẽ gây aliasing xung quanh các cạnh của đối tượng. Đặt quá thấp sẽ khiến các cạnh của đối tượng trông bị mờ. - **Light Affect:** Cường độ ambient occlusion trong không gian màn hình dưới ánh sáng trực tiếp. Trong đời thực, ambient occlusion chỉ áp dụng cho ánh sáng gián tiếp, nghĩa là không thể thấy tác động của nó dưới ánh sáng trực tiếp. Các giá trị lớn hơn 0 sẽ làm cho hiệu ứng :abbr:`SSAO (Screen-Space Ambient Occlusion)` hiển thị dưới ánh sáng trực tiếp. Các giá trị lớn hơn ``0.0`` không chính xác về mặt vật lý, nhưng một số họa sĩ thích hiệu ứng này. - **AO Channel Affect** Cường độ ambient occlusion trong không gian màn hình trên các vật liệu đã xác định texture AO. Các giá trị lớn hơn ``0.0`` sẽ làm cho hiệu ứng SSAO hiển thị trong các vùng bị làm tối bởi texture AO.

Ngoài ra, bạn có thể điều chỉnh chất lượng của SSAO trong phần **Rendering > Environment > SSAO** của project settings:

- **Quality:** Thiết lập chất lượng của hiệu ứng ambient occlusion trong không gian màn hình. Giá trị cao hơn sẽ lấy nhiều mẫu hơn, từ đó cho chất lượng tốt hơn, nhưng phải đánh đổi bằng hiệu năng. Đặt giá trị này thành Ultra sẽ sử dụng thiết lập **Adaptive Target** (xem bên dưới). - **Half Size:** Nếu ``true``, ambient occlusion trong không gian màn hình sẽ được kết xuất ở một nửa kích thước, sau đó được nâng kích thước trước khi thêm vào scene. Cách này nhanh hơn đáng kể nhưng có thể bỏ sót các chi tiết nhỏ. Nếu ``false``, ambient occlusion trong không gian màn hình sẽ được kết xuất ở kích thước đầy đủ. - **Adaptive Target:** Mục tiêu chất lượng được sử dụng khi **Quality** được đặt thành **Ultra**. Giá trị ``0.0`` cho chất lượng và tốc độ tương tự Medium, trong khi giá trị ``1.0`` cho chất lượng cao hơn nhiều so với mọi thiết lập khác, nhưng phải đánh đổi bằng hiệu năng. - **Blur Passes:** Số lần blur được sử dụng khi tính toán ambient occlusion trong không gian màn hình. Số lần cao hơn sẽ tạo ra hình ảnh mượt hơn, nhưng tính toán chậm hơn và có ít chi tiết tần số cao hơn. - **Fadeout From:** Khoảng cách mà tại đó hiệu ứng ambient occlusion trong không gian màn hình bắt đầu mờ dần. Sử dụng tùy chọn này để ẩn ambient occlusion ở khoảng cách xa. - **Fadeout To:** Khoảng cách mà tại đó ambient occlusion trong không gian màn hình mờ hoàn toàn. Sử dụng tùy chọn này để ẩn ambient occlusion ở khoảng cách xa.

.. note::

    Kể từ Godot 4.6, một phiên bản đơn giản hóa của SSAO đã có trong Compatibility renderer. Cách triển khai này có hình thức khác, nhưng sẽ cho hiệu năng tốt hơn đáng kể trên các thiết bị cấp thấp so với SSAO trong Forward+.

    Khi sử dụng Compatibility renderer, chỉ có thể điều chỉnh các tham số **Radius** và **Intensity**.

.. _doc_environment_and_post_processing_ssil:

Chiếu sáng gián tiếp trong không gian màn hình (Screen-Space Indirect Lighting — SSIL)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng Forward+ renderer, không khả dụng trên Mobile hoặc Compatibility.*

:abbr:`SSIL (Screen-Space Indirect Lighting)` provides indirect lighting for
các chi tiết nhỏ hoặc hình học động mà các kỹ thuật global illumination khác không thể bao phủ. Điều này áp dụng cho ánh sáng khuếch tán dội lại, cũng như các vật liệu phát sáng. Khi :abbr:`SSIL (Screen-Space Indirect Lighting)` được bật riêng, hiệu ứng có thể không dễ nhận thấy, và đó là chủ đích.

Thay vào đó, :abbr:`SSIL (Screen-Space Indirect Lighting)` được dùng như một *bổ trợ* cho các kỹ thuật global illumination khác như VoxelGI, SDFGI và LightmapGI. :abbr:`SSIL (Screen-Space Indirect Lighting)` cũng cung cấp một hiệu ứng ambient occlusion tinh tế, tương tự SSAO nhưng ít chi tiết hơn.

Tính năng này chỉ cung cấp ánh sáng gián tiếp. Đây không phải là một giải pháp global illumination đầy đủ. Điều này khiến nó khác với global illumination trong không gian màn hình (screen-space global illumination — SSGI) do các 3D engine khác cung cấp. :abbr:`SSIL (Screen-Space Indirect Lighting)` có thể kết hợp với :abbr:`SSR (Screen-Space Reflections)` và/hoặc
:abbr:`SSAO (Screen-Space Ambient Occlusion)` for greater visual quality
(đánh đổi bằng hiệu năng).

Có thể tinh chỉnh :abbr:`SSIL (Screen-Space Indirect Lighting)` bằng một số tham số:

- **Radius:** Khoảng cách mà ánh sáng dội lại có thể truyền đi khi sử dụng hiệu ứng chiếu sáng gián tiếp trong không gian màn hình. Giá trị lớn hơn sẽ khiến ánh sáng dội xa hơn trong scene, nhưng có thể gây ra các artifact do lấy mẫu không đủ, trông giống như những tia dài bao quanh nguồn sáng. - **Intensity:** Hệ số nhân độ sáng cho hiệu ứng chiếu sáng gián tiếp trong không gian màn hình. Giá trị cao hơn sẽ tạo ra ánh sáng sáng hơn. - **Sharpness:** Mức độ mà hiệu ứng chiếu sáng gián tiếp trong không gian màn hình được phép làm mờ qua các cạnh của đối tượng. Đặt quá cao sẽ gây aliasing xung quanh các cạnh của đối tượng. Đặt quá thấp sẽ khiến các cạnh của đối tượng trông bị mờ. - **Normal Rejection:** Mức độ loại bỏ normal được sử dụng khi tính toán chiếu sáng gián tiếp trong không gian màn hình. Normal rejection sử dụng normal của một điểm mẫu nhất định để loại bỏ các mẫu hướng ra xa pixel hiện tại. Normal rejection là cần thiết để tránh rò rỉ ánh sáng khi chỉ một phía của đối tượng được chiếu sáng. Tuy nhiên, có thể tắt normal rejection nếu muốn có rò rỉ ánh sáng, chẳng hạn khi scene chủ yếu chứa các đối tượng phát sáng phát ra ánh sáng từ những mặt không thể nhìn thấy từ camera.

Ngoài ra, bạn có thể điều chỉnh chất lượng của SSIL trong phần **Rendering > Environment > SSIL** của project settings:

- **Quality:** Thiết lập chất lượng của hiệu ứng chiếu sáng gián tiếp trong không gian màn hình. Giá trị cao hơn sẽ lấy nhiều mẫu hơn, từ đó cho chất lượng tốt hơn, nhưng phải đánh đổi bằng hiệu năng. Đặt giá trị này thành Ultra sẽ sử dụng thiết lập **Adaptive Target** (xem bên dưới). - **Half Size:** Nếu ``true``, chiếu sáng gián tiếp trong không gian màn hình sẽ được kết xuất ở một nửa kích thước, sau đó được nâng kích thước trước khi thêm vào scene. Cách này nhanh hơn đáng kể nhưng có thể bỏ sót các chi tiết nhỏ. Nếu ``false``, chiếu sáng gián tiếp trong không gian màn hình sẽ được kết xuất ở kích thước đầy đủ. - **Adaptive Target:** Mục tiêu chất lượng được sử dụng khi **Quality** được đặt thành **Ultra**. Giá trị ``0.0`` cho chất lượng và tốc độ tương tự Medium, trong khi giá trị ``1.0`` cho chất lượng cao hơn nhiều so với mọi thiết lập khác, nhưng phải đánh đổi bằng hiệu năng. Khi sử dụng adaptive target, chi phí hiệu năng tăng theo độ phức tạp của scene. - **Blur Passes:** Số lần blur được sử dụng khi tính toán chiếu sáng gián tiếp trong không gian màn hình. Số lần cao hơn sẽ tạo ra hình ảnh mượt hơn, nhưng tính toán chậm hơn và có ít chi tiết tần số cao hơn. - **Fadeout From:** Khoảng cách mà tại đó hiệu ứng chiếu sáng gián tiếp trong không gian màn hình bắt đầu mờ dần. Sử dụng tùy chọn này để ẩn chiếu sáng gián tiếp trong không gian màn hình ở khoảng cách xa. - **Fadeout To:** Khoảng cách mà tại đó chiếu sáng gián tiếp trong không gian màn hình mờ hoàn toàn. Sử dụng tùy chọn này để ẩn chiếu sáng gián tiếp trong không gian màn hình ở khoảng cách xa.

.. image:: img/environment_ssil.webp

Global Illumination bằng Signed Distance Field (SDFGI)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng Forward+ renderer, không khả dụng trên Mobile hoặc Compatibility.*

Global illumination bằng signed distance field (SDFGI) là một dạng global illumination theo thời gian thực. Đây không phải là hiệu ứng trong không gian màn hình, nghĩa là nó có thể cung cấp global illumination cho các phần tử ngoài màn hình (không giống :abbr:`SSIL (Screen-Space Indirect Lighting)`).

.. seealso::

    Xem :ref:`doc_using_sdfgi` để biết hướng dẫn thiết lập kỹ thuật global illumination này.

.. image:: img/environment_sdfgi.webp

.. _doc_environment_and_post_processing_glow:

Glow
~~~~

.. note::

    Khi sử dụng Compatibility rendering method, glow dùng một cách triển khai khác, trong đó một số thuộc tính không khả dụng và bị ẩn khỏi inspector: **Levels**, **Normalized**, **Strength**, **Blend Mode**, **Mix**, **Map** và **Map Strength**.

    Cách triển khai này được tối ưu để chạy trên các thiết bị cấp thấp và vì vậy kém linh hoạt hơn.

Trong nhiếp ảnh và điện ảnh, khi lượng ánh sáng vượt quá *luminance* (độ sáng) tối đa mà phương tiện hỗ trợ, ánh sáng thường lan ra ngoài về phía các vùng tối hơn của hình ảnh. Điều này được mô phỏng trong Godot bằng hiệu ứng **Glow**.

.. image:: img/environment_glow1.webp

Theo mặc định, ngay cả khi hiệu ứng được bật, nó vẫn yếu hoặc không hiển thị. Một trong hai điều kiện sau phải xảy ra để hiệu ứng thực sự hiển thị:

- 1) Ánh sáng trong một pixel vượt qua **HDR Threshold** (trong đó 0 nghĩa là mọi ánh sáng đều vượt qua ngưỡng, còn 1.0 là ánh sáng vượt quá giá trị **White** của tonemapper). Thông thường, giá trị này được kỳ vọng là 1.0, nhưng có thể giảm xuống để cho phép nhiều ánh sáng lan ra hơn. Ngoài ra còn có tham số **HDR Scale**, cho phép điều chỉnh tỷ lệ (làm sáng hơn hoặc tối hơn) lượng ánh sáng vượt qua ngưỡng.

.. image:: img/environment_glow_threshold.webp

- 2) Thuộc tính **Bloom** có giá trị lớn hơn ``0.0``. Khi giá trị này tăng, toàn bộ màn hình sẽ được gửi đến bộ xử lý glow với cường độ cao hơn.

.. image:: img/environment_glow_bloom.webp

Cả hai đều sẽ khiến ánh sáng bắt đầu tràn ra khỏi những vùng sáng hơn.

Khi hiệu ứng phát sáng đã hiển thị, bạn có thể điều khiển hiệu ứng này bằng một vài tham số bổ sung:

- **Intensity** là tỷ lệ tổng thể của hiệu ứng; bạn có thể tăng hoặc giảm cường độ (``0.0`` sẽ loại bỏ hiệu ứng). - **Strength** xác định mức độ mạnh khi xử lý kernel của bộ lọc gaussian. Giá trị lớn hơn khiến bộ lọc bão hòa và mở rộng ra ngoài. Nhìn chung, bạn không cần thay đổi giá trị này, vì có thể điều chỉnh kích thước hiệu quả hơn bằng **Levels**.

Bạn cũng có thể thay đổi **Blend Mode** của hiệu ứng:

- **Additive** là chế độ mạnh nhất vì nó chỉ thêm hiệu ứng phát sáng lên hình ảnh mà không thực hiện blending. Nhìn chung, chế độ này quá mạnh để sử dụng, nhưng có thể trông đẹp khi dùng với **Bloom** có cường độ thấp (tạo ra hiệu ứng giống như trong mơ). - **Screen** đảm bảo hiệu ứng phát sáng không bao giờ làm sáng hơn chính nó và hoạt động tốt trong hầu hết trường hợp. - **Softlight** là chế độ mặc định và yếu nhất, chỉ tạo ra sự thay đổi màu sắc nhẹ xung quanh các vật thể. Chế độ này hoạt động tốt nhất trong các cảnh tối. - **Replace** có thể được dùng để
  :ref:`blur the whole screen <doc_environment_and_post_processing_using_glow_to_blur_the_screen>`
  hoặc debug hiệu ứng. Chế độ này chỉ hiển thị hiệu ứng phát sáng mà không hiển thị hình ảnh bên dưới. - **Mix** trộn hiệu ứng phát sáng với hình ảnh chính. Bạn có thể dùng chế độ này để kiểm soát nghệ thuật tốt hơn. Hệ số trộn được điều khiển bằng thuộc tính **Mix**, xuất hiện phía trên blend mode (chỉ khi blend mode được đặt thành Mix). Giá trị hệ số trộn cao sẽ khiến hình ảnh có vẻ tối hơn, trừ khi **Bloom** được tăng lên.

Để thay đổi kích thước và hình dạng của hiệu ứng phát sáng, Godot cung cấp **Levels**. Các level nhỏ tạo ra ánh sáng mạnh xuất hiện xung quanh vật thể, trong khi các level lớn tạo ra ánh sáng mờ bao phủ toàn bộ màn hình:

.. image:: img/environment_glow_layers.webp

Tuy nhiên, điểm mạnh thực sự của hệ thống này là khả năng kết hợp các level để tạo ra những mẫu phát sáng thú vị hơn:

.. image:: img/environment_glow_layers2.webp

Cuối cùng, bạn có thể điều khiển hiệu ứng phát sáng bằng *glow map*, một texture xác định độ sáng của hiệu ứng trên từng phần của màn hình. Texture này có thể được tô màu tùy chọn để nhuộm hiệu ứng phát sáng theo màu của glow map. Texture được kéo giãn để vừa với viewport, vì vậy bạn nên sử dụng tỷ lệ khung hình phù hợp với tỷ lệ khung hình thường dùng nhất của viewport (chẳng hạn như 16:9) để tránh hiện tượng méo rõ rệt.

Có 2 trường hợp sử dụng chính cho texture glow map:

- Tạo hiệu ứng "lens dirt" bằng texture có mẫu bụi. - Làm cho hiệu ứng phát sáng yếu hơn ở những phần cụ thể của màn hình bằng texture gradient.

.. image:: img/environment_glow_map.webp

Theo mặc định, glow sử dụng bộ lọc scaling bicubic trên các nền tảng desktop và bộ lọc scaling bilinear trên các nền tảng mobile. Bộ lọc scaling bicubic cho chất lượng cao hơn với hình ảnh ít bị vỡ khối hơn, nhưng làm tăng chi phí hiệu năng trên GPU, mức tăng này có thể đáng kể đối với graphics tích hợp. Bạn có thể điều khiển scale mode bằng project setting **Rendering > Environment > Glow > Upscale Mode**. Setting này chỉ có hiệu lực khi sử dụng renderer Forward+ hoặc Mobile, vì Compatibility sử dụng một implementation glow khác.

.. image:: img/environment_and_post_processing_glow_scale_mode.webp

.. _doc_environment_and_post_processing_using_glow_in_2d:

Sử dụng glow trong 2D
~~~~~~~~~~~~~~~~~~~~~

Có 2 cách sử dụng glow trong 2D:

- Kể từ Godot 4.2, bạn có thể bật HDR cho việc rendering 2D khi sử dụng phương thức rendering Forward+ và Mobile. Việc này làm tăng chi phí hiệu năng, nhưng cho phép có dynamic range lớn hơn. Tính năng này cũng cho phép bạn kiểm soát vật thể nào phát sáng bằng các thuộc tính **Modulate** hoặc **Self Modulate** riêng của chúng (sử dụng thanh trượt Intensity trong color picker). Bật HDR cũng có thể giảm hiện tượng banding trong đầu ra rendering 2D.

  - Để bật HDR trong 2D, hãy mở Project Settings và bật
    :ref:`Rendering > Viewport > HDR 2D<class_ProjectSettings_property_rendering/viewport/hdr_2d>`
    sau đó khởi động lại editor.

- Nếu muốn tối đa hóa hiệu năng, bạn có thể để HDR tắt khi rendering 2D. Tuy nhiên, bạn sẽ ít kiểm soát hơn đối với những vật thể phát sáng.

  - Bật glow, đặt background mode của environment thành **Canvas**, sau đó giảm **Glow HDR Threshold** để các pixel không quá sáng vẫn phát sáng. Để ngăn các thành phần UI phát sáng, hãy đặt chúng làm các node con của một
    :ref:`class_CanvasLayer` node. You can control which layers are affected by
    node glow bằng thuộc tính **Background > Canvas Max Layer** của resource Environment.

.. figure:: img/environment_and_post_processing_glow_in_2d.webp
   :align: center
   :alt: Example of using glow in a 2D scene

   Example of using glow in a 2D scene. HDR 2D is enabled, while coins and the
   bullet have their **Modulate** property increased to overbright values using the
   Intensity slider in the color picker.

.. warning::

    Renderer 2D render trong không gian màu tuyến tính nếu
    :ref:`Rendering > Viewport > HDR 2D<class_ProjectSettings_property_rendering/viewport/hdr_2d>`
    project setting được bật, vì vậy cũng phải sử dụng hint ``source_color`` cho các uniform sampler được dùng làm đầu vào màu trong các shader ``canvas_item``. Nếu không làm vậy, texture sẽ bị nhạt màu.

    Nếu HDR 2D bị tắt, ``source_color`` vẫn hoạt động chính xác trong các shader ``canvas_item``, vì vậy bạn nên sử dụng nó khi phù hợp trong mọi trường hợp.

    Việc sử dụng không gian màu tuyến tính cũng có nghĩa là alpha blending sẽ thay đổi. Các sprite có giá trị opacity thấp nhìn chung sẽ hiển thị rõ hơn, và việc render font sẽ trông đậm hơn do các pixel có opacity thấp từ quá trình antialiasing của font trở nên dễ thấy hơn. Điều này cũng ảnh hưởng đến rendering của chính editor.

.. _doc_environment_and_post_processing_using_glow_to_blur_the_screen:

Sử dụng glow để làm mờ màn hình
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể sử dụng glow để làm mờ toàn bộ viewport, rất hữu ích khi làm mờ background lúc menu đang mở. Chỉ rendering 3D bị ảnh hưởng, trừ khi background mode của environment được đặt thành **Canvas**. Để ngăn các thành phần UI bị làm mờ khi sử dụng background mode Canvas, hãy đặt chúng làm các node con của một node :ref:`class_CanvasLayer`. Bạn có thể kiểm soát những layer nào bị ảnh hưởng bởi hiệu ứng làm mờ này bằng thuộc tính **Background > Canvas Max Layer** của resource Environment.

Để sử dụng glow như một giải pháp làm mờ:

- Bật **Normalized** và điều chỉnh các level theo mong muốn. Việc tăng các chỉ số level cao hơn sẽ tạo ra hình ảnh mờ hơn. Bạn nên để một glow level duy nhất ở ``1.0`` và để tất cả các glow level khác ở ``0.0``, nhưng đây không phải yêu cầu bắt buộc. Lưu ý rằng hình ảnh cuối cùng sẽ thay đổi tùy theo độ phân giải viewport. - Đặt **Intensity** thành ``1.0`` và **Bloom** thành ``1.0``. - Đặt blend mode thành **Replace** và **HDR Luminance Cap** thành ``1.0``.

.. figure:: img/environment_and_post_processing_glow_blur.webp
   :align: center
   :alt: Example of using glow to blur the 2D rendering in the menu's background

   Example of using glow to blur the 2D rendering in the menu's background

Sương mù
~~~~~~~~

.. note::

    Phần này chỉ đề cập đến sương mù không thể tích. Bạn có thể sử dụng đồng thời sương mù không thể tích và :ref:`doc_volumetric_fog`.

Sương mù, giống như trong đời thực, khiến các vật thể ở xa dần biến mất vào một màu đồng nhất. Có hai loại sương mù trong Godot:

- **Depth Fog:** Loại này được áp dụng dựa trên khoảng cách từ camera. - **Height Fog:** Loại này được áp dụng cho mọi vật thể nằm dưới (hoặc trên) một độ cao nhất định, bất kể khoảng cách từ camera.

.. image:: img/environment_fog_depth_height.webp

Bạn có thể điều chỉnh các curve của cả hai loại sương mù này, khiến quá trình chuyển tiếp sắc nét hơn hoặc mềm hơn.

Có thể điều chỉnh hai thuộc tính để làm hiệu ứng sương mù thú vị hơn:

Thuộc tính đầu tiên là **Sun Scatter**, sử dụng màu và năng lượng của DirectionalLight3D trong scene hiện tại. Khi nhìn về phía directional light (thường là mặt trời), sương mù sẽ được nhuộm theo màu của ánh sáng để mô phỏng ánh nắng xuyên qua sương mù.

Thuộc tính thứ hai là **Aerial Perspective**, nhuộm màu sương mù theo màu bầu trời để hòa trộn bầu trời với background tốt hơn. Giá trị cao hơn sẽ tạo ra mức nhuộm màu mạnh hơn, trong đó ``1.0`` thay thế hoàn toàn màu sương mù thông thường bằng aerial perspective. Tính năng này có thể được dùng trong các level thế giới mở rộng lớn để tạo cảm nhận chiều sâu tốt hơn hoặc tránh sự gián đoạn màu sắc giữa màu bầu trời và màu sương mù.

Nếu cả **Sun Scatter** và **Aerial Perspective** đều lớn hơn ``0.0``, hiệu ứng tán xạ ánh sáng mặt trời sẽ được áp dụng bên trên aerial perspective.

.. note::

    Sương mù có thể khiến banding xuất hiện trên viewport, đặc biệt ở các mức density cao hơn. Xem :ref:`doc_3d_rendering_limitations_color_banding` để biết hướng dẫn giảm banding.

Sương mù thể tích
~~~~~~~~~~~~~~~~~

Sương mù thể tích tạo ra hiệu ứng sương mù chân thực cho scene, trong đó màu sương mù bị ảnh hưởng bởi các nguồn sáng xuyên qua sương mù.

.. seealso::

  Xem :ref:`doc_volumetric_fog` để biết tài liệu về cách thiết lập sương mù thể tích.

Điều chỉnh
~~~~~~~~~~

Ở cuối quá trình xử lý, Godot cung cấp khả năng thực hiện một số điều chỉnh hình ảnh tiêu chuẩn.

.. image:: img/environment_adjustments.webp

**Điều chỉnh BCS cơ bản**

Điều chỉnh đầu tiên là khả năng thay đổi các thuộc tính **Brightness**, **Contrast** và **Saturation** thông thường:

.. image:: img/environment_adjustments_bcs.webp

**Hiệu chỉnh màu bằng gradient 1D**

Điều chỉnh thứ hai là cung cấp một gradient hiệu chỉnh màu. Bạn có thể thực hiện việc này bằng cách gán một resource GradientTexture1D cho thuộc tính **Color Correction**, hoặc tải một texture chứa gradient ngang. Phần ngoài cùng bên trái của gradient biểu thị màu đen trong hình ảnh nguồn, còn phần ngoài cùng bên phải của gradient biểu thị màu trắng trong hình ảnh nguồn.

Một gradient tuyến tính từ đen đến trắng như gradient sau sẽ không tạo ra hiệu ứng:

.. image:: img/environment_adjustments_default_gradient.webp

Tuy nhiên, việc tạo các gradient tùy chỉnh sẽ cho phép ánh xạ mỗi channel sang một màu khác:

.. image:: img/environment_adjustments_custom_gradient.webp

**Hiệu chỉnh màu bằng 3D LUT**

Bạn cũng có thể sử dụng look-up texture (LUT) 3D để hiệu chỉnh màu. Đây là một texture đặc biệt dùng để sửa đổi từng channel màu riêng biệt (đỏ, xanh lá, xanh dương). Hình ảnh này có thể có độ phân giải bất kỳ, nhưng vì hiệu chỉnh màu là dữ liệu tần số thấp nên bạn nên sử dụng độ phân giải thấp để đảm bảo hiệu năng. Độ phân giải của texture LUT thường là 17×17×17, 33×33×33, 51×51×51 hoặc 65×65×65 (kích thước lẻ cho phép nội suy tốt hơn).

Để tính năng này hoạt động, import mode của look-up texture phải được đặt thành Texture3D trong Import dock (thay vì được import dưới dạng Texture2D thông thường):

.. image:: img/environment_adjustments_3d_lut_import.webp

Hãy đảm bảo bạn cũng cấu hình số lát cắt ngang và dọc cần nhập. Nếu không làm vậy, texture LUT sẽ không tác động chính xác đến viewport khi được sử dụng. Bạn có thể xem trước cách texture 3D được nhập bằng cách nhấp đúp vào texture đó trong dock FileSystem, sau đó đi đến inspector để lật qua các lớp của texture.

Bạn có thể sử dụng template LUT 33×33×33 trung tính này làm cơ sở (nhấp chuột phải và chọn **Save as…**):

.. image:: img/environment_adjustments_3d_lut_template.webp

Với template LUT ở trên, sau khi thay đổi chế độ nhập thành **Texture3D**, hãy đặt số lát cắt **Horizontal** thành ``33`` trong dock Import, sau đó nhấp vào **Reimport**. Nếu bạn tải LUT này vào thuộc tính **Color Correction**, hiện tại bạn sẽ không thấy bất kỳ khác biệt nào vì texture này được thiết kế làm điểm khởi đầu trung tính.

Bạn có thể chỉnh sửa template LUT này trong trình chỉnh sửa ảnh để tạo ra một sắc thái khác cho hình ảnh. Một quy trình phổ biến là đặt ảnh LUT cạnh ảnh chụp màn hình viewport 3D của dự án, sau đó sử dụng trình chỉnh sửa ảnh để chỉnh sửa đồng thời cả ảnh LUT và ảnh chụp màn hình. Sau đó, LUT có thể được lưu lại và áp dụng vào game engine để thực hiện cùng một phép hiệu chỉnh màu theo thời gian thực.

Ví dụ, việc chỉnh sửa template LUT trong trình chỉnh sửa ảnh để tạo cho nó vẻ ngoài "sepia" sẽ cho ra hình ảnh ở bên phải:

.. image:: img/environment_adjustments_3d_lut_comparison.webp

.. note::

    Các điều chỉnh và hiệu chỉnh màu được áp dụng *sau* tonemapping. Điều này có nghĩa là các thuộc tính tonemapping được định nghĩa ở trên vẫn có tác dụng khi bật các điều chỉnh.

Các tùy chọn thuộc tính camera
------------------------------

Godot có hai loại thuộc tính camera: physical và practical. Khi sử dụng CameraAttributesPhysical thay vì CameraAttributesPractical, độ sâu trường ảnh được tự động tính toán từ khoảng cách lấy nét, tiêu cự và khẩu độ của các thuộc tính camera. Ngoài ra, các tùy chọn Frustum cũng khả dụng.

Depth of Field / Far Blur
~~~~~~~~~~~~~~~~~~~~~~~~~

Hiệu ứng này mô phỏng khoảng cách lấy nét trên camera. Nó làm mờ các vật thể nằm phía sau một phạm vi nhất định. Hiệu ứng có **Distance** ban đầu cùng một vùng **Transition** (tính theo đơn vị trong thế giới):

.. image:: img/environment_dof_far.webp

Tham số **Amount** kiểm soát mức độ làm mờ. Với độ mờ lớn hơn, có thể cần điều chỉnh chất lượng depth of field trong phần cài đặt dự án nâng cao để tránh hiện tượng lỗi hình ảnh.

Depth of Field / Near Blur
~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiệu ứng này mô phỏng khoảng cách lấy nét trên camera. Nó làm mờ các vật thể ở gần camera (hoạt động theo hướng ngược với far blur). Hiệu ứng có **Distance** ban đầu cùng một vùng **Transition** (tính theo đơn vị trong thế giới):

.. image:: img/environment_dof_near.webp

Tham số **Amount** kiểm soát mức độ làm mờ. Với độ mờ lớn hơn, có thể cần điều chỉnh chất lượng depth of field trong phần cài đặt dự án nâng cao để tránh hiện tượng lỗi hình ảnh.

Thông thường, người ta sử dụng cả hai hiệu ứng làm mờ cùng nhau để tập trung sự chú ý của người xem vào một vật thể nhất định hoặc tạo ra hiệu ứng `"tilt shift" effect <https://en.wikipedia.org/wiki/Miniature_faking>`__.

.. image:: img/environment_mixed_blur.webp

Exposure
~~~~~~~~

Giá trị này nhân với độ sáng tổng thể của cảnh mà camera nhìn thấy. Giá trị cao hơn sẽ tạo ra cảnh sáng hơn về mặt hình ảnh.

Auto Exposure
~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng renderer Forward+, không khả dụng với Mobile hoặc Compatibility.*

Mặc dù trong hầu hết trường hợp, ánh sáng và texture được nghệ sĩ kiểm soát rất nhiều, Godot vẫn hỗ trợ cơ chế high dynamic range cơ bản với cơ chế auto exposure. Cơ chế này thường được dùng để tăng tính chân thực khi kết hợp các khu vực trong nhà có ánh sáng yếu với các khu vực ngoài trời sáng. Auto exposure mô phỏng camera (hoặc mắt người) trong nỗ lực thích ứng giữa các vị trí sáng và tối, cũng như mức độ ánh sáng khác nhau của chúng.

.. note::

    Auto exposure cần đánh giá độ sáng của cảnh trong mỗi frame, dẫn đến chi phí hiệu năng ở mức vừa phải. Vì vậy, bạn nên tắt Auto Exposure nếu nó không tạo ra nhiều khác biệt trong cảnh của mình.

.. image:: img/environment_hdr_autoexp.webp

Cách đơn giản nhất để sử dụng auto exposure là đảm bảo đèn ngoài trời (hoặc các đèn mạnh khác) có energy lớn hơn 1.0. Việc này được thực hiện bằng cách điều chỉnh multiplier **Energy** của chúng (ngay trên Light). Để duy trì tính nhất quán, **Sky** thường cũng cần sử dụng multiplier energy để khớp với directional light. Thông thường, các giá trị từ 3.0 đến 6.0 là đủ để mô phỏng điều kiện trong nhà và ngoài trời.

Bằng cách kết hợp Auto Exposure với hậu kỳ :ref:`doc_environment_and_post_processing_glow`, các pixel vượt quá **White** của tonemap sẽ tràn vào glow buffer, tạo ra hiệu ứng bloom đặc trưng trong nhiếp ảnh.

.. image:: img/environment_hdr_bloom.webp

Các giá trị do người dùng kiểm soát trong phần Auto Exposure đi kèm các giá trị mặc định hợp lý, nhưng bạn vẫn có thể điều chỉnh chúng:

.. image:: img/environment_hdr.webp

- **Scale:** Giá trị dùng để scale ánh sáng. Giá trị cao hơn tạo ra hình ảnh sáng hơn, còn giá trị thấp hơn tạo ra hình ảnh tối hơn. - **Min Sensitivity / Min Exposure Value:** Độ chói tối thiểu mà auto exposure sẽ hướng đến khi điều chỉnh (tính theo ISO khi sử dụng CameraAttributesPractical hoặc theo EV100 khi sử dụng CameraAttributesPhysical). Độ chói là giá trị trung bình của ánh sáng trên tất cả pixel của màn hình. - **Max Sensitivity / Max Exposure Value:** Độ chói tối đa mà auto exposure sẽ hướng đến khi điều chỉnh (tính theo ISO khi sử dụng CameraAttributesPractical hoặc theo EV100 khi sử dụng CameraAttributesPhysical). - **Speed:** Tốc độ tự điều chỉnh của độ chói. Giá trị càng cao thì việc hiệu chỉnh độ chói càng nhanh. Các giá trị cao có thể phù hợp hơn với các game có nhịp độ nhanh, nhưng có thể gây mất tập trung trong một số trường hợp.

Khi sử dụng CameraAttributesPractical, exposure được thiết lập bằng *sensitivity* được định nghĩa theo ISO thay vì một giá trị exposure theo EV100. Các giá trị ISO phổ biến nằm trong khoảng từ 50 đến 3200, trong đó giá trị cao hơn tạo ra exposure cuối cùng cao hơn. Trong đời thực, nhiếp ảnh ban ngày thường sử dụng các giá trị ISO từ 100 đến 800.

.. seealso::

    Xem :ref:`doc_physical_light_and_camera_units` nếu bạn muốn sử dụng các đơn vị thực tế để cấu hình exposure, field of view và depth of field của camera.
