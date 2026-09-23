.. _doc_environment_and_post_processing:

Môi trường và hậu kỳ
====================

Godot 4 cung cấp một resource Environment được thiết kế lại, cùng với một hệ thống hậu kỳ mới có sẵn nhiều hiệu ứng ngay từ đầu.

.. note::

    Kể từ Godot 4, các thiết lập *hiệu năng/chất lượng* của Environment được xác định trong phần thiết lập project thay vì trong resource Environment. Điều này giúp việc điều chỉnh trên toàn cục dễ dàng hơn, vì bạn không còn phải tinh chỉnh từng resource Environment riêng lẻ để phù hợp với các cấu hình phần cứng khác nhau.

    Lưu ý rằng hầu hết các thiết lập hiệu năng/chất lượng của Environment chỉ hiển thị sau khi bật tùy chọn **Advanced** trong Project Settings.

Environment
-----------

Resource :ref:`class_Environment` lưu trữ mọi thông tin cần thiết để điều khiển môi trường render 2D và 3D. Thông tin này bao gồm bầu trời, ánh sáng môi trường, tone mapping, hiệu ứng và các điều chỉnh. Bản thân resource này không thực hiện gì, nhưng bạn có thể bật nó bằng cách sử dụng ở một trong các vị trí sau, theo thứ tự ưu tiên:

Node Camera3D (ưu tiên cao)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể đặt một Environment cho node Camera3D. Environment này sẽ được ưu tiên hơn mọi thiết lập khác.

.. image:: img/environment_camera.webp

Điều này chủ yếu hữu ích khi bạn muốn ghi đè một môi trường hiện có, nhưng nhìn chung, sử dụng tùy chọn bên dưới sẽ tốt hơn.

Node WorldEnvironment (ưu tiên trung bình, khuyến nghị)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có thể thêm node WorldEnvironment vào bất kỳ scene nào, nhưng mỗi scene tree đang hoạt động chỉ có thể tồn tại một node. Việc thêm nhiều hơn một node sẽ tạo ra cảnh báo.

.. image:: img/environment_world.webp

Mọi Environment được thêm vào đều có mức ưu tiên cao hơn Environment mặc định (được giải thích bên dưới). Điều này có nghĩa là bạn có thể ghi đè nó theo từng scene, khiến nó trở nên rất hữu ích.

Môi trường và mặt trời xem trước (ưu tiên thấp)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

    Kể từ Godot 4, hệ thống môi trường và mặt trời xem trước thay thế file ``default_env.tres`` từng được sử dụng trong các project Godot 3.

Nếu scene hiện tại không có node WorldEnvironment hoặc node DirectionalLight3D, editor sẽ hiển thị môi trường và mặt trời xem trước. Bạn có thể tắt tính năng này bằng các nút ở đầu 3D editor:

.. image:: img/environment_preview_sun_sky_toggle.webp

Nhấp vào ba dấu chấm dọc ở bên phải sẽ hiển thị một hộp thoại cho phép bạn tùy chỉnh diện mạo của môi trường xem trước:

.. image:: img/environment_preview_sun_sky_dialog.webp

**Mặt trời và bầu trời xem trước chỉ hiển thị trong editor, không hiển thị trong project đang chạy.** Sử dụng các nút ở cuối hộp thoại, bạn có thể thêm mặt trời và bầu trời xem trước vào scene dưới dạng các node.

.. tip::

    Nếu bạn giữ :kbd:`Shift` trong khi nhấp vào **Add Sun to Scene** hoặc **Add Environment to Scene** trong trình chỉnh sửa môi trường xem trước, thao tác này sẽ thêm cả mặt trời và môi trường xem trước vào scene hiện tại (như thể bạn đã nhấp riêng vào cả hai nút). Hãy sử dụng cách này để tăng tốc quá trình thiết lập và tạo prototype cho project.

Thuộc tính camera
-----------------

.. note::

    Trong Godot 4, thông tin về exposure và depth of field được tách khỏi resource Environment thành một resource CameraAttributes riêng biệt. Điều này giúp điều chỉnh các thuộc tính đó độc lập với các thiết lập Environment khác dễ dàng hơn.

Resource :ref:`class_CameraAttributes` lưu trữ thông tin về exposure và depth of field. Resource này cũng cho phép bật các điều chỉnh exposure tự động tùy theo độ sáng của scene.

Có hai loại resource CameraAttributes:

- **CameraAttributesPractical:** Các tính năng được thể hiện bằng những đơn vị tùy ý, dễ hình dung hơn trong hầu hết trường hợp sử dụng game.
- **CameraAttributesPhysical:** Các tính năng được thể hiện bằng đơn vị thực tế, tương tự như camera kỹ thuật số. Ví dụ, field of view được thiết lập bằng tiêu cự tính theo milimét thay vì một giá trị tính theo độ. Được khuyến nghị khi độ chính xác vật lý là quan trọng, chẳng hạn như trong render chân thực.

Cả hai loại resource CameraAttribute đều cho phép bạn sử dụng cùng các tính năng, nhưng chúng được cấu hình khác nhau. Nếu không biết nên chọn loại nào, hãy sử dụng **CameraAttributesPractical**.

.. note::

    Việc sử dụng một :ref:`class_CameraAttributesPhysical` trên node Camera3D sẽ khóa các điều chỉnh FOV và aspect trong Camera3D đó, vì field of view được điều chỉnh trong resource CameraAttributesPhysical. Nếu được sử dụng trong WorldEnvironment, CameraAttributesPhysical sẽ không ghi đè bất kỳ Camera3D nào trong scene.

Có thể thêm một resource CameraAttributes vào node Camera3D hoặc WorldEnvironment. Khi camera hiện tại đã được thiết lập CameraAttributes, nó sẽ *ghi đè* CameraAttributes được thiết lập trong WorldEnvironment (nếu có).

Trong hầu hết trường hợp, bạn nên thiết lập resource CameraAttributes trên node Camera3D thay vì WorldEnvironment. Không giống như WorldEnvironment, việc gán resource CameraAttributes cho node Camera3D sẽ ngăn depth of field hiển thị trong viewport 3D editor, trừ khi camera đang được xem trước.

Các tùy chọn Environment
------------------------

Phần sau đây mô tả chi tiết tất cả các tùy chọn môi trường và cách chúng được dự định sử dụng.

Background
~~~~~~~~~~

Phần Background chứa các thiết lập về cách tô nền (những phần trên màn hình mà các đối tượng không được vẽ). Nền không chỉ có tác dụng hiển thị hình ảnh hoặc màu sắc. Theo mặc định, nền còn ảnh hưởng đến cách các đối tượng chịu tác động của ánh sáng môi trường và ánh sáng phản xạ. Đây được gọi là image-based lighting (IBL).

Do đó, bầu trời nền có thể ảnh hưởng rất lớn đến diện mạo tổng thể của scene, ngay cả khi bầu trời không bao giờ hiển thị trực tiếp trên màn hình. Bạn nên ghi nhớ điều này khi tinh chỉnh ánh sáng trong scene.

.. image:: img/environment_background1.webp

Có một số chế độ nền:

- **Clear Color** sử dụng màu xóa mặc định được xác định trong phần thiết lập project. Nền sẽ có một màu cố định.
- **Custom Color** tương tự Clear Color, nhưng sử dụng giá trị màu tùy chỉnh.
- **Sky** cho phép bạn xác định material bầu trời nền (xem bên dưới). Theo mặc định, các đối tượng trong scene sẽ phản chiếu material bầu trời này và hấp thụ ánh sáng môi trường từ nó.
- **Canvas** hiển thị scene 2D làm nền cho scene 3D. Bạn có thể sử dụng tùy chọn này để làm cho các hiệu ứng môi trường hiển thị trên phần render 2D, chẳng hạn như
  :ref:`glow trong 2D <doc_environment_and_post_processing_using_glow_in_2d>`.
- **Keep** không vẽ bầu trời mà giữ lại nội dung đã có ở các frame trước. Điều này cải thiện hiệu năng trong các scene hoàn toàn ở trong nhà, nhưng sẽ tạo ra lỗi hình ảnh kiểu "hall of mirrors" nếu bầu trời hiển thị vào bất kỳ thời điểm nào.
- **Camera Feed** hiển thị một :ref:`class_CameraFeed` từ camera vật lý làm nền, hữu ích cho các game AR trên thiết bị di động.

Vật liệu bầu trời
~~~~~~~~~~~~~~~~~

Khi sử dụng chế độ nền **Sky** (hoặc khi chế độ ánh sáng môi trường/phản chiếu được đặt thành **Sky**), một subresource Sky sẽ có sẵn để chỉnh sửa trong resource Environment. Việc chỉnh sửa subresource này cho phép bạn tạo một resource SkyMaterial bên trong Sky.

Có 3 vật liệu bầu trời tích hợp để lựa chọn:

- **PanoramaSkyMaterial:** Sử dụng hình ảnh bầu trời panorama 360 độ (khuyến nghị tỷ lệ khung hình 2:1). Để tận dụng dải tương phản động cao, hình ảnh panorama phải ở định dạng tương thích với HDR như ``.hdr`` hoặc ``.exr`` thay vì định dạng dải tương phản động tiêu chuẩn như ``.png`` hoặc ``.jpg``.
- **ProceduralSkyMaterial:** Sử dụng bầu trời được tạo bằng quy trình với các màu mặt đất, mặt trời, bầu trời và đường chân trời có thể điều chỉnh. Đây là loại bầu trời được sử dụng trong phần xem trước của editor. Vị trí của mặt trời được tự động suy ra từ 4 node DirectionalLight3D đầu tiên xuất hiện trong scene. Có thể có tối đa 4 mặt trời tại một thời điểm.
- **PhysicalSkyMaterial:** Sử dụng bầu trời được tạo bằng quy trình dựa trên vật lý với các tham số tán xạ có thể điều chỉnh. Vị trí của mặt trời được tự động suy ra từ node DirectionalLight3D đầu tiên xuất hiện trong scene. PhysicalSkyMaterial tốn nhiều chi phí render hơn một chút so với ProceduralSkyMaterial. Có thể có tối đa 1 mặt trời tại một thời điểm.

Hình ảnh bầu trời panorama đôi khi được gọi là HDRI (High Dynamic Range Images). Bạn có thể tìm thấy các HDRI được cấp phép miễn phí trên `Poly Haven <https://polyhaven.com/hdris>`__.

.. note::

    Texture HDR PanoramaSkyMaterial có các vùng rất sáng (chẳng hạn như ảnh chụp thực tế có thể nhìn thấy mặt trời) có thể tạo ra các đốm lấp lánh rõ ràng trên phản xạ môi trường và phản xạ specular. Nguyên nhân là do mức phơi sáng cực đại của texture quá cao.

    Để khắc phục, hãy chọn texture panorama trong dock FileSystem, chuyển đến dock Import, bật **HDR Clamp Exposure** rồi nhấp vào **Reimport**.

Nếu cần một vật liệu bầu trời tùy chỉnh (ví dụ: cho mây được tạo bằng quy trình), bạn có thể tạo một :ref:`sky shader <doc_sky_shader>` tùy chỉnh.

Ánh sáng môi trường
~~~~~~~~~~~~~~~~~~~

Ánh sáng môi trường (theo định nghĩa ở đây) là một loại ánh sáng tác động lên mọi phần hình học với cùng cường độ. Đây là ánh sáng toàn cục và độc lập với các nguồn sáng có thể được thêm vào scene. Ánh sáng môi trường là một trong hai thành phần của image-based lighting. Không giống ánh sáng phản xạ, ánh sáng môi trường không thay đổi tùy theo vị trí và góc nhìn của camera.

Có một số loại ánh sáng môi trường để lựa chọn:

- **Background:** Lấy ánh sáng môi trường từ nền, chẳng hạn như bầu trời, màu tùy chỉnh hoặc màu xóa (mặc định). Cường độ ánh sáng môi trường sẽ thay đổi tùy theo nội dung của hình ảnh bầu trời, nhờ đó ánh sáng môi trường có thể trông hấp dẫn hơn về mặt thị giác. Phải đặt bầu trời làm nền thì chế độ này mới hiển thị.
- **Disabled:** Không sử dụng ánh sáng môi trường. Hữu ích cho các scene hoàn toàn trong nhà.
- **Color:** Sử dụng một màu cố định cho ánh sáng môi trường, bỏ qua bầu trời nền. Cường độ ánh sáng môi trường sẽ giống nhau ở mọi phía, khiến ánh sáng của scene có thể trông phẳng hơn. Hữu ích cho các scene trong nhà, nơi bóng đen hoàn toàn có thể quá tối, hoặc để tối đa hóa hiệu suất trên các thiết bị cấp thấp.
- **Sky:** Lấy ánh sáng môi trường từ một bầu trời được chỉ định, ngay cả khi nền được đặt thành chế độ khác với **Sky**. Nếu chế độ nền đã là **Sky**, chế độ này hoạt động giống hệt **Background**.

Khi chế độ ánh sáng môi trường được đặt thành Sky hoặc Background (và nền được đặt thành Sky), bạn có thể pha trộn giữa màu môi trường và bầu trời bằng thuộc tính **Sky Contribution**. Theo mặc định, giá trị này được đặt thành ``1.0``, nghĩa là chỉ bầu trời môi trường được sử dụng. Màu môi trường sẽ bị bỏ qua trừ khi **Sky Contribution** được giảm xuống dưới ``1.0``.

Sau đây là so sánh ảnh hưởng của các loại ánh sáng môi trường khác nhau lên một scene:

.. image:: img/environment_ambient2.webp

Cuối cùng, có một thiết lập **Energy**, đây là một hệ số nhân. Thiết lập này hữu ích khi làm việc với HDR.

Nhìn chung, bạn chỉ nên dựa vào riêng ánh sáng môi trường cho các scene đơn giản hoặc các không gian ngoài trời rộng lớn. Bạn cũng có thể làm vậy để tăng hiệu suất. Ánh sáng môi trường render nhanh, nhưng không cung cấp chất lượng ánh sáng tốt nhất. Tốt hơn là tạo ánh sáng môi trường từ :ref:`ReflectionProbe <doc_reflection_probes>`,
:ref:`VoxelGI <doc_using_voxel_gi>` hoặc :ref:`SDFGI <doc_using_sdfgi>`, vì các phương pháp này mô phỏng chính xác hơn cách ánh sáng gián tiếp lan truyền. Dưới đây là so sánh về chất lượng giữa việc sử dụng màu môi trường phẳng và VoxelGI:

.. image:: img/environment_ambient_comparison.webp

Sử dụng một trong các phương pháp được mô tả ở trên sẽ thay thế ánh sáng môi trường cố định bằng ánh sáng môi trường từ các probe.

Ánh sáng phản xạ
~~~~~~~~~~~~~~~~

Ánh sáng phản xạ (còn gọi là ánh sáng specular) là thành phần còn lại trong hai thành phần của image-based lighting.

Ánh sáng phản xạ có thể được đặt thành một trong 3 chế độ:

- **Background:** Phản xạ từ nền, chẳng hạn như bầu trời, màu tùy chỉnh hoặc màu xóa (mặc định).
- **Disabled:** Không phản xạ bất kỳ ánh sáng nào từ môi trường. Hữu ích cho các scene hoàn toàn trong nhà hoặc để tối đa hóa hiệu suất trên các thiết bị cấp thấp.
- **Sky:** Phản xạ từ bầu trời nền, ngay cả khi nền được đặt thành chế độ khác với **Sky**. Nếu chế độ nền đã là **Sky**, chế độ này hoạt động giống hệt **Background**.

Tonemap
~~~~~~~

Tonemap chọn thuật toán tonemapping sẽ được áp dụng cho scene từ danh sách các thuật toán tiêu chuẩn được sử dụng trong ngành công nghiệp phim và game. Các chế độ tonemapping khác **Linear** được dùng để làm cho các vùng sáng và tối đồng đều hơn, đồng thời tránh hiện tượng cắt ngưỡng ở các vùng sáng mạnh. Mỗi thuật toán có đặc điểm hiệu suất khác nhau cần được cân nhắc khi chọn tonemapper.

Các tùy chọn tone mapping là:

- **Mode:** Chế độ tonemapping sẽ sử dụng.

  - **Linear:** Không thay đổi dữ liệu màu, tạo ra đường cong tonemapping tuyến tính, đường cong này cắt ngưỡng các giá trị sáng một cách thiếu tự nhiên, khiến ánh sáng mạnh trông bị cháy sáng. Đây là tonemapper đơn giản và nhanh nhất.
  - **Reinhard:** Một đường cong tonemapping đơn giản làm giảm dần các giá trị sáng để ngăn cắt ngưỡng. Kết quả là hình ảnh có thể trông nhạt và ít tương phản. Chậm hơn Linear. Khi **White** giữ giá trị mặc định là ``1.0``, Reinhard tạo ra hình ảnh giống hệt Linear.
  - **Filmic:** Sử dụng đường cong tonemapping giống phim để ngăn cắt ngưỡng các giá trị sáng và cung cấp độ tương phản tốt hơn Reinhard. Chậm hơn Reinhard một chút.
  - **ACES:** Sử dụng đường cong tonemapping giống phim với độ tương phản cao và giảm bão hòa các giá trị sáng để tạo vẻ ngoài chân thực hơn. Chậm hơn Filmic một chút.
  - **AgX:** Sử dụng đường cong tonemapping mang phong cách phim và giảm độ bão hòa của các giá trị sáng để tạo diện mạo chân thực hơn. Duy trì sắc độ của màu sắc khi chúng trở nên sáng hơn tốt hơn các tonemapper khác. Đây là tùy chọn tonemapping chậm nhất.

- **Exposure:** Điều chỉnh độ sáng của các giá trị trước khi chúng được cung cấp cho tonemapper. Các giá trị **Exposure** cao hơn sẽ tạo ra hình ảnh sáng hơn. Các giá trị được cung cấp cho tonemapper cũng sẽ được nhân với ``2.0`` và ``1.8`` lần lượt đối với **Filmic** và **ACES** để tạo ra độ sáng cảm nhận tương tự như Linear.

- **White:** Giá trị tham chiếu màu trắng cho tonemapping, cho biết vị trí của màu trắng sáng trên thang giá trị được cung cấp cho tonemapper. Đối với ánh sáng chân thực, các giá trị được khuyến nghị nằm trong khoảng từ ``6.0`` đến ``8.0``. Các giá trị cao hơn tạo ra vùng sáng ít bị cháy hơn, nhưng có thể khiến cảnh trông kém tương phản hơn. **White** không khả dụng khi sử dụng **Linear**. Nếu bạn sử dụng AgX, mobile renderer và HDR 2D bị tắt, giá trị được đặt tại đây sẽ bị bỏ qua và giá trị ``2.0`` sẽ được sử dụng thay thế.

- **AGX Contrast:** Chỉ khả dụng khi sử dụng AgX. Tăng giá trị này sẽ làm các giá trị tối tối hơn và các giá trị sáng sáng hơn. Tùy chọn này tạo ra kết quả tốt hơn tùy chọn contrast trong phần adjustment mà không làm tăng chi phí hiệu năng.

Hiệu ứng xử lý trung gian và hậu kỳ
-----------------------------------

Tài nguyên Environment hỗ trợ nhiều hiệu ứng xử lý trung gian và hậu kỳ phổ biến.

.. note::

    Các hiệu ứng trong không gian màn hình như :abbr:`SSR (Screen-Space Reflections)`,
    :abbr:`SSAO (Screen-Space Ambient Occlusion)`,
    :abbr:`SSIL (Screen-Space Indirect Lighting)` và glow không hoạt động trên hình học nằm ngoài tầm nhìn của camera hoặc bị che khuất bởi hình học đục khác. Hãy cân nhắc điều này khi tinh chỉnh các thiết lập của chúng để tránh những thay đổi gây mất tập trung trong quá trình chơi.

Screen-Space Reflections (SSR)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng Forward+ renderer, không khả dụng với Mobile hoặc Compatibility.*

Mặc dù Godot hỗ trợ một số nguồn dữ liệu phản chiếu như
:ref:`doc_reflection_probes`, chúng có thể không cung cấp đủ chi tiết cho mọi tình huống. Các trường hợp phản chiếu trong không gian màn hình phù hợp nhất là khi các đối tượng tiếp xúc với nhau (đối tượng nằm trên sàn, trên bàn, nổi trên mặt nước, v.v.).

.. image:: img/environment_ssr.webp

Ngoài việc cung cấp nhiều chi tiết hơn, phản chiếu trong không gian màn hình còn hoạt động theo thời gian thực (trong khi các loại phản chiếu khác thường được tính toán trước). Bạn có thể sử dụng tính năng này để khiến nhân vật, ô tô, v.v. phản chiếu trên các bề mặt xung quanh khi di chuyển.

Có thể sử dụng phản chiếu trong không gian màn hình đồng thời với các nguồn phản chiếu khác để tận dụng phản chiếu chi tiết khi có thể, đồng thời có phương án dự phòng khi không thể sử dụng phản chiếu trong không gian màn hình (ví dụ: để phản chiếu các đối tượng ngoài màn hình).

Có một số tham số do người dùng điều khiển để tinh chỉnh kỹ thuật này tốt hơn:

- **Max Steps:** Xác định độ dài tối đa của phản chiếu. Giá trị này càng lớn thì chi phí tính toán càng cao.
- **Fade In:** Cho phép điều chỉnh đường cong fade-in, hữu ích để làm vùng tiếp xúc mềm hơn.
- **Fade Out:** Cho phép điều chỉnh đường cong fade-out, để giới hạn bước mờ dần một cách mềm mại.
- **Depth Tolerance:** Có thể được sử dụng để cho phép các tia trong không gian màn hình đi xuyên ra phía sau đối tượng. Khi xác định liệu có thể đi ra phía sau đối tượng hay không, các tia sẽ coi mỗi đối tượng như thể nó có độ sâu này. Giá trị cao hơn sẽ khiến phản chiếu trong không gian màn hình xuất hiện ít "breakup" hơn, nhưng phải đánh đổi bằng việc một số đối tượng tạo ra phản chiếu không chính xác về mặt vật lý.

Ngoài ra, bạn có thể điều chỉnh chất lượng của SSR trong phần cài đặt dự án bằng cách bật tắt **Rendering > Environment > Screen Space Reflection > Half Size**. Theo mặc định, phản chiếu trong không gian màn hình được kết xuất ở một nửa độ phân giải vì lý do hiệu năng. Tắt thiết lập này sẽ khiến hiệu ứng được kết xuất ở độ phân giải đầy đủ, cải thiện chất lượng nhưng làm tăng mức sử dụng GPU.

.. note::

    Hãy lưu ý rằng phản chiếu trong không gian màn hình chỉ hoạt động với hình học đục. Các vật liệu trong suốt sẽ không được phản chiếu vì chúng không ghi vào depth buffer. Điều này cũng áp dụng cho các shader sử dụng uniform ``hint_screen_texture`` hoặc ``hint_depth_texture``.

Screen-Space Ambient Occlusion (SSAO)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng Forward+ và Compatibility renderers, không khả dụng với Mobile.*

Như đã đề cập trong phần **Ambient**, các khu vực không nhận được ánh sáng từ các light node (do nằm ngoài bán kính hoặc bị che bóng) sẽ được chiếu sáng bằng ánh sáng môi trường. Godot có thể mô phỏng điều này bằng VoxelGI, ReflectionProbe, Sky hoặc một màu môi trường cố định. Tuy nhiên, vấn đề là tất cả các phương pháp được đề cập trước đó hoạt động ở quy mô lớn hơn (các vùng lớn) thay vì ở cấp độ hình học nhỏ hơn.

Màu môi trường cố định và Sky giống nhau ở mọi nơi, trong khi GI và Reflection probe có nhiều chi tiết cục bộ hơn, nhưng vẫn chưa đủ để mô phỏng các tình huống ánh sáng không thể lấp đầy bên trong những đặc điểm rỗng hoặc lõm.

Có thể mô phỏng điều này bằng Screen Space Ambient Occlusion. Như bạn có thể thấy trong hình bên dưới, mục đích của nó là đảm bảo các khu vực lõm tối hơn, mô phỏng đường đi hẹp hơn để ánh sáng đi vào:

.. image:: img/environment_ssao.webp

Một lỗi thường gặp là bật hiệu ứng này, bật một light và không nhận thấy tác dụng của nó. Đó là vì :abbr:`SSAO (Screen-Space Ambient Occlusion)` chỉ tác động lên ánh sáng *ambient*. Nó không ảnh hưởng đến ánh sáng trực tiếp.

Đó là lý do trong hình phía trên, hiệu ứng ít nhận thấy hơn bên dưới ánh sáng trực tiếp (ở bên trái). Nếu bạn muốn buộc
:abbr:`SSAO (Screen-Space Ambient Occlusion)` cũng hoạt động với ánh sáng trực tiếp, hãy sử dụng tham số **Light Affect**. Mặc dù điều này không chính xác về mặt vật lý, một số họa sĩ thích diện mạo mà nó tạo ra.

:abbr:`SSAO (Screen-Space Ambient Occlusion)` cho kết quả tốt nhất khi kết hợp với một nguồn ánh sáng gián tiếp thực sự, chẳng hạn như VoxelGI:

.. image:: img/environment_ssao2.webp

Có thể tinh chỉnh :abbr:`SSAO (Screen-Space Ambient Occlusion)` bằng một số tham số:

.. image:: img/environment_ssao_parameters.webp

- **Radius:** Khoảng cách mà các đối tượng có thể che khuất lẫn nhau khi tính toán ambient occlusion trong không gian màn hình. Giá trị cao hơn sẽ tạo ra hiện tượng che khuất trên khoảng cách lớn hơn, nhưng phải đánh đổi bằng hiệu năng và chất lượng.
- **Intensity:** Cường độ ambient occlusion trong không gian màn hình chính. Hoạt động như một hệ số nhân cho hiệu ứng ambient occlusion trong không gian màn hình. Giá trị cao hơn tạo ra vùng occlusion tối hơn. Vì :abbr:`SSAO (Screen-Space Ambient Occlusion)` là một hiệu ứng trong không gian màn hình, bạn nên sử dụng giá trị này một cách thận trọng.
  :abbr:`SSAO (Screen-Space Ambient Occlusion)` quá mạnh có thể gây mất tập trung trong khi chơi game.
- **Power:** Phân bố của vùng occlusion. Giá trị cao hơn tạo ra vùng occlusion tối hơn, tương tự như **Intensity**, nhưng có độ suy giảm gắt hơn.
- **Detail:** Thiết lập cường độ của mức chi tiết bổ sung cho hiệu ứng ambient occlusion trong không gian màn hình. Giá trị cao làm cho lượt xử lý chi tiết nổi bật hơn, nhưng có thể góp phần gây aliasing trong hình ảnh cuối cùng.
- **Horizon:** Ngưỡng xác định một điểm nhất định trên bề mặt có bị che khuất hay không, được biểu diễn dưới dạng góc tính từ đường chân trời và ánh xạ vào phạm vi 0.0-1.0. Giá trị 1.0 sẽ không tạo ra occlusion.
- **Sharpness:** Mức độ hiệu ứng ambient occlusion trong không gian màn hình được phép làm mờ qua các cạnh của vật thể. Đặt giá trị quá cao sẽ gây aliasing quanh các cạnh của vật thể. Đặt giá trị quá thấp sẽ khiến các cạnh vật thể trông mờ.
- **Light Affect:** Cường độ ambient occlusion trong không gian màn hình dưới ánh sáng trực tiếp. Trong thực tế, ambient occlusion chỉ áp dụng cho ánh sáng gián tiếp, nghĩa là không thể thấy hiệu ứng của nó dưới ánh sáng trực tiếp. Các giá trị lớn hơn 0 sẽ khiến hiệu ứng :abbr:`SSAO (Screen-Space Ambient Occlusion)` hiển thị dưới ánh sáng trực tiếp. Các giá trị trên ``0.0`` không chính xác về mặt vật lý, nhưng một số artist thích hiệu ứng này.
- **AO Channel Affect** Cường độ ambient occlusion trong không gian màn hình trên các material có texture AO được xác định. Các giá trị lớn hơn ``0.0`` sẽ khiến hiệu ứng SSAO hiển thị ở những khu vực bị làm tối bởi texture AO.

Ngoài ra, bạn có thể điều chỉnh chất lượng SSAO trong phần **Rendering > Environment > SSAO** của project settings:

- **Quality:** Thiết lập chất lượng của hiệu ứng ambient occlusion trong không gian màn hình. Giá trị cao hơn sẽ lấy nhiều sample hơn, nhờ đó cho chất lượng tốt hơn nhưng làm giảm hiệu năng. Đặt thành Ultra sẽ sử dụng thiết lập **Adaptive Target** (xem bên dưới).
- **Half Size:** Nếu ``true``, ambient occlusion trong không gian màn hình sẽ được render ở kích thước một nửa, sau đó upscale trước khi được thêm vào scene. Cách này nhanh hơn đáng kể nhưng có thể bỏ sót các chi tiết nhỏ. Nếu ``false``, ambient occlusion trong không gian màn hình sẽ được render ở kích thước đầy đủ.
- **Adaptive Target:** Mục tiêu chất lượng được sử dụng khi **Quality** được đặt thành **Ultra**. Giá trị ``0.0`` cho chất lượng và tốc độ tương tự Medium, trong khi giá trị ``1.0`` cho chất lượng cao hơn nhiều so với mọi thiết lập khác nhưng làm giảm hiệu năng.
- **Blur Passes:** Số lượt làm mờ được sử dụng khi tính toán ambient occlusion trong không gian màn hình. Số lượng cao hơn sẽ tạo ra hình ảnh mượt hơn, nhưng tính toán chậm hơn và có ít chi tiết tần số cao hơn.
- **Fadeout From:** Khoảng cách mà tại đó hiệu ứng ambient occlusion trong không gian màn hình bắt đầu mờ dần. Sử dụng tùy chọn này để ẩn ambient occlusion ở khoảng cách xa.
- **Fadeout To:** Khoảng cách mà tại đó ambient occlusion trong không gian màn hình biến mất hoàn toàn. Sử dụng tùy chọn này để ẩn ambient occlusion ở khoảng cách xa.

.. note::

    Kể từ Godot 4.6, một phiên bản đơn giản hóa của SSAO có trong Compatibility renderer. Cách triển khai này cho hình ảnh khác biệt, nhưng sẽ có hiệu năng tốt hơn đáng kể trên các thiết bị cấp thấp so với SSAO trong Forward+.

    Khi sử dụng Compatibility renderer, chỉ có thể điều chỉnh các tham số **Radius** và **Intensity**.

.. _doc_environment_and_post_processing_ssil:

Screen-Space Indirect Lighting (SSIL)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng Forward+ renderer, không khả dụng trong Mobile hoặc Compatibility.*

:abbr:`SSIL (Screen-Space Indirect Lighting)` cung cấp ánh sáng gián tiếp cho các chi tiết nhỏ hoặc hình học động mà các kỹ thuật global illumination khác không thể bao phủ. Điều này áp dụng cho ánh sáng diffuse dội lại, cũng như các material phát sáng. Khi bật riêng :abbr:`SSIL (Screen-Space Indirect Lighting)`, hiệu ứng có thể không quá dễ nhận thấy, và đó là chủ ý.

Thay vào đó, :abbr:`SSIL (Screen-Space Indirect Lighting)` được thiết kế để sử dụng như một *complement* cho các kỹ thuật global illumination khác như VoxelGI, SDFGI và LightmapGI. :abbr:`SSIL (Screen-Space Indirect Lighting)` cũng cung cấp hiệu ứng ambient occlusion tinh tế, tương tự SSAO nhưng ít chi tiết hơn.

Tính năng này chỉ cung cấp ánh sáng gián tiếp. Đây không phải là một giải pháp global illumination hoàn chỉnh. Điều này khiến nó khác với screen-space global illumination (SSGI) do các 3D engine khác cung cấp. :abbr:`SSIL (Screen-Space Indirect Lighting)` có thể kết hợp với :abbr:`SSR (Screen-Space Reflections)` và/hoặc
:abbr:`SSAO (Screen-Space Ambient Occlusion)` để có chất lượng hình ảnh cao hơn (đánh đổi bằng hiệu năng).

Bạn có thể tinh chỉnh :abbr:`SSIL (Screen-Space Indirect Lighting)` bằng một số tham số:

- **Radius:** Khoảng cách mà ánh sáng dội lại có thể truyền đi khi sử dụng hiệu ứng ánh sáng gián tiếp trong không gian màn hình. Giá trị lớn hơn sẽ khiến ánh sáng dội đi xa hơn trong scene, nhưng có thể tạo ra các artifact do lấy mẫu thiếu, trông giống như những tia dài bao quanh nguồn sáng.
- **Intensity:** Hệ số nhân độ sáng cho hiệu ứng ánh sáng gián tiếp trong không gian màn hình. Giá trị cao hơn sẽ tạo ra ánh sáng sáng hơn.
- **Sharpness:** Mức độ hiệu ứng ánh sáng gián tiếp trong không gian màn hình được phép làm mờ qua các cạnh của vật thể. Đặt giá trị quá cao sẽ gây aliasing quanh các cạnh của vật thể. Đặt giá trị quá thấp sẽ khiến các cạnh vật thể trông mờ.
- **Normal Rejection:** Mức độ loại bỏ normal được sử dụng khi tính toán ánh sáng gián tiếp trong không gian màn hình. Normal rejection sử dụng normal của một điểm sample nhất định để loại bỏ các sample hướng ra xa pixel hiện tại. Normal rejection là cần thiết để tránh hiện tượng ánh sáng lọt qua khi chỉ một mặt của vật thể được chiếu sáng. Tuy nhiên, có thể tắt normal rejection nếu muốn ánh sáng lọt qua, chẳng hạn khi scene chủ yếu chứa các vật thể phát sáng phát ra ánh sáng từ những mặt không thể nhìn thấy từ camera.

Ngoài ra, bạn có thể điều chỉnh chất lượng của SSIL trong phần **Rendering > Environment > SSIL** của cài đặt dự án:

- **Quality:** Đặt chất lượng của hiệu ứng chiếu sáng gián tiếp trong không gian màn hình. Giá trị cao hơn sẽ lấy nhiều mẫu hơn, nhờ đó cho chất lượng tốt hơn nhưng làm giảm hiệu năng. Đặt giá trị này thành Ultra sẽ sử dụng cài đặt **Adaptive Target** (xem bên dưới).
- **Half Size:** Nếu ``true``, chiếu sáng gián tiếp trong không gian màn hình sẽ được kết xuất ở một nửa kích thước, sau đó được nâng cấp trước khi thêm vào cảnh. Cách này nhanh hơn đáng kể nhưng có thể bỏ sót các chi tiết nhỏ. Nếu ``false``, chiếu sáng gián tiếp trong không gian màn hình sẽ được kết xuất ở kích thước đầy đủ.
- **Adaptive Target:** Mục tiêu chất lượng được sử dụng khi **Quality** được đặt thành **Ultra**. Giá trị ``0.0`` cho chất lượng và tốc độ tương tự Medium, trong khi giá trị ``1.0`` cho chất lượng cao hơn nhiều so với mọi cài đặt khác nhưng làm giảm hiệu năng. Khi sử dụng mục tiêu thích ứng, chi phí hiệu năng sẽ tăng theo độ phức tạp của cảnh.
- **Blur Passes:** Số lần làm mờ được sử dụng khi tính toán chiếu sáng gián tiếp trong không gian màn hình. Số lần cao hơn sẽ tạo ra hình ảnh mượt hơn, nhưng cần nhiều thời gian tính toán hơn và có ít chi tiết tần số cao hơn.
- **Fadeout From:** Khoảng cách mà tại đó hiệu ứng chiếu sáng gián tiếp trong không gian màn hình bắt đầu mờ dần. Sử dụng tùy chọn này để ẩn chiếu sáng gián tiếp trong không gian màn hình từ xa.
- **Fadeout To:** Khoảng cách mà tại đó chiếu sáng gián tiếp trong không gian màn hình mờ hoàn toàn. Sử dụng tùy chọn này để ẩn chiếu sáng gián tiếp trong không gian màn hình từ xa.

.. image:: img/environment_ssil.webp

Chiếu sáng toàn cục bằng Trường Khoảng cách có dấu (SDFGI)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng trình kết xuất Forward+, không khả dụng với Mobile hoặc Compatibility.*

Chiếu sáng toàn cục bằng trường khoảng cách có dấu (SDFGI) là một dạng chiếu sáng toàn cục theo thời gian thực. Đây không phải là hiệu ứng trong không gian màn hình, nghĩa là nó có thể cung cấp chiếu sáng toàn cục cho các phần tử nằm ngoài màn hình (không giống như :abbr:`SSIL (Screen-Space Indirect Lighting)`).

.. seealso::

    Xem :ref:`doc_using_sdfgi` để biết hướng dẫn thiết lập kỹ thuật chiếu sáng toàn cục này.

.. image:: img/environment_sdfgi.webp

.. _doc_environment_and_post_processing_glow:

Glow
~~~~

.. note::

    Khi sử dụng phương thức kết xuất Compatibility, Glow sử dụng một cách triển khai khác, trong đó một số thuộc tính không khả dụng và bị ẩn khỏi inspector: **Levels**, **Normalized**, **Strength**, **Blend Mode**, **Mix**, **Map** và **Map Strength**.

    Cách triển khai này được tối ưu để chạy trên các thiết bị cấp thấp nên kém linh hoạt hơn.

Trong nhiếp ảnh và điện ảnh, khi lượng ánh sáng vượt quá *độ chói* (độ sáng) tối đa mà phương tiện hỗ trợ, ánh sáng thường lan ra các vùng tối hơn của hình ảnh. Trong Godot, hiệu ứng này được mô phỏng bằng hiệu ứng **Glow**.

.. image:: img/environment_glow1.webp

Theo mặc định, ngay cả khi hiệu ứng được bật, hiệu ứng vẫn yếu hoặc không thể nhìn thấy. Một trong hai điều kiện sau phải xảy ra để hiệu ứng thực sự hiển thị:

- 1) Ánh sáng trong một pixel vượt quá **HDR Threshold** (trong đó 0 nghĩa là mọi ánh sáng đều vượt quá ngưỡng, còn 1.0 là ánh sáng vượt quá giá trị **White** của tonemapper). Thông thường, giá trị này được đặt ở 1.0, nhưng có thể giảm xuống để cho phép nhiều ánh sáng lan ra hơn. Ngoài ra còn có tham số **HDR Scale**, cho phép điều chỉnh tỷ lệ (làm sáng hơn hoặc tối hơn) phần ánh sáng vượt ngưỡng.

.. image:: img/environment_glow_threshold.webp

- 2) Thuộc tính **Bloom** có giá trị lớn hơn ``0.0``. Khi giá trị này tăng, toàn bộ màn hình sẽ được gửi đến bộ xử lý glow với cường độ cao hơn.

.. image:: img/environment_glow_bloom.webp

Cả hai trường hợp đều khiến ánh sáng bắt đầu lan ra từ các vùng sáng hơn.

Sau khi Glow hiển thị, bạn có thể điều khiển hiệu ứng bằng một số tham số bổ sung:

- **Intensity** là tỷ lệ tổng thể của hiệu ứng; bạn có thể làm hiệu ứng mạnh hơn hoặc yếu hơn (``0.0`` sẽ loại bỏ hiệu ứng).
- **Strength** là cường độ xử lý của kernel bộ lọc gaussian. Giá trị lớn hơn khiến bộ lọc bão hòa và mở rộng ra ngoài. Nhìn chung, không cần thay đổi giá trị này, vì bạn có thể điều chỉnh kích thước hiệu quả hơn bằng **Levels**.

Bạn cũng có thể thay đổi **Blend Mode** của hiệu ứng:

- **Additive** là chế độ mạnh nhất, vì nó chỉ thêm hiệu ứng glow lên hình ảnh mà không thực hiện pha trộn. Nhìn chung, chế độ này quá mạnh để sử dụng, nhưng có thể trông đẹp khi kết hợp với **Bloom** cường độ thấp (tạo hiệu ứng như trong mơ).
- **Screen** đảm bảo Glow không bao giờ làm sáng hơn chính nó và hoạt động tốt như một chế độ đa dụng.
- **Softlight** là chế độ mặc định và yếu nhất, chỉ tạo ra sự biến đổi màu sắc nhẹ quanh các vật thể. Chế độ này hoạt động tốt nhất trong các cảnh tối.
- **Replace** có thể được sử dụng để
  :ref:`làm mờ toàn bộ màn hình <doc_environment_and_post_processing_using_glow_to_blur_the_screen>` hoặc gỡ lỗi hiệu ứng. Chế độ này chỉ hiển thị hiệu ứng glow mà không hiển thị hình ảnh bên dưới.
- **Mix** trộn hiệu ứng glow với hình ảnh chính. Bạn có thể sử dụng chế độ này để kiểm soát nghệ thuật tốt hơn. Hệ số trộn được điều khiển bởi thuộc tính **Mix**, xuất hiện phía trên blend mode (chỉ khi blend mode được đặt thành Mix). Các giá trị hệ số trộn cao sẽ khiến hình ảnh có vẻ tối hơn, trừ khi tăng **Bloom**.

Để thay đổi kích thước và hình dạng của hiệu ứng glow, Godot cung cấp **Levels**. Các level nhỏ tạo ra glow mạnh xuất hiện quanh vật thể, trong khi các level lớn tạo ra glow mờ bao phủ toàn bộ màn hình:

.. image:: img/environment_glow_layers.webp

Tuy nhiên, điểm mạnh thực sự của hệ thống này là kết hợp các level để tạo ra những kiểu glow thú vị hơn:

.. image:: img/environment_glow_layers2.webp

Cuối cùng, bạn có thể điều khiển hiệu ứng glow bằng *bản đồ glow*, một texture xác định độ sáng của glow trên từng phần màn hình. Texture này có thể được tô màu tùy chọn để nhuộm hiệu ứng glow theo màu của bản đồ glow. Texture được kéo giãn để vừa với viewport, vì vậy bạn nên sử dụng tỷ lệ khung hình khớp với tỷ lệ khung hình thường dùng nhất của viewport (chẳng hạn 16:9) để tránh biến dạng rõ rệt.

Có 2 trường hợp sử dụng chính cho texture bản đồ glow:

- Tạo hiệu ứng "bụi trên ống kính" bằng texture có họa tiết bụi.
- Làm cho glow yếu hơn ở các phần cụ thể của màn hình bằng texture chuyển sắc.

.. image:: img/environment_glow_map.webp

Theo mặc định, glow sử dụng bộ lọc scaling bicubic trên các nền tảng desktop và bộ lọc scaling bilinear trên các nền tảng mobile. Bộ lọc scaling bicubic cho chất lượng cao hơn với hình ảnh ít bị vỡ khối hơn, nhưng phải trả giá về hiệu năng GPU, điều này có thể đáng kể trên card đồ họa tích hợp. Chế độ scale có thể được kiểm soát bằng thiết lập project **Rendering > Environment > Glow > Upscale Mode**. Thiết lập này chỉ có hiệu lực khi sử dụng renderer Forward+ hoặc Mobile, vì Compatibility sử dụng một cách triển khai glow khác.

.. image:: img/environment_and_post_processing_glow_scale_mode.webp

.. _doc_environment_and_post_processing_using_glow_in_2d:

Sử dụng glow trong 2D
~~~~~~~~~~~~~~~~~~~~~

Có 2 cách sử dụng glow trong 2D:

- Kể từ Godot 4.2, bạn có thể bật HDR cho việc render 2D khi sử dụng các phương thức render Forward+ và Mobile. Điều này làm giảm hiệu năng, nhưng cho phép dải dynamic lớn hơn. Nó cũng cho phép bạn kiểm soát các đối tượng phát glow bằng các thuộc tính **Modulate** hoặc **Self Modulate** riêng của chúng (sử dụng thanh trượt Intensity trong color picker). Việc bật HDR cũng có thể giảm banding trong đầu ra render 2D.

  - Để bật HDR trong 2D, hãy mở Project Settings, bật
    :ref:`Rendering > Viewport > HDR 2D <class_ProjectSettings_property_rendering/viewport/hdr_2d>` rồi khởi động lại editor.

- Nếu muốn tối đa hóa hiệu năng, bạn có thể để HDR bị tắt khi render 2D. Tuy nhiên, bạn sẽ ít kiểm soát hơn đối với các đối tượng phát glow.

  - Bật glow, đặt chế độ nền của environment thành **Canvas** rồi giảm **Glow HDR Threshold** để các pixel không quá sáng vẫn phát glow. Để ngăn các phần tử UI phát glow, hãy đặt chúng làm con của một
    :ref:`class_CanvasLayer` node. Bạn có thể kiểm soát các layer bị glow tác động bằng thuộc tính **Background > Canvas Max Layer** của resource Environment.

.. figure:: img/environment_and_post_processing_glow_in_2d.webp
   :align: center
   :alt: Ví dụ sử dụng glow trong một scene 2D

   Ví dụ sử dụng glow trong một scene 2D. HDR 2D được bật, trong khi các đồng xu và viên đạn có thuộc tính **Modulate** được tăng lên các giá trị quá sáng bằng thanh trượt Intensity trong color picker.

.. warning::

    Renderer 2D render trong không gian màu tuyến tính nếu
    thiết lập project :ref:`Rendering > Viewport > HDR 2D <class_ProjectSettings_property_rendering/viewport/hdr_2d>` được bật, vì vậy cũng phải sử dụng hint ``source_color`` cho các uniform sampler được dùng làm đầu vào màu trong các shader ``canvas_item``. Nếu không làm vậy, texture sẽ trông bị nhạt màu.

    Nếu HDR 2D bị tắt, ``source_color`` vẫn hoạt động chính xác trong các shader ``canvas_item``, vì vậy bạn nên sử dụng nó khi phù hợp trong mọi trường hợp.

    Việc sử dụng không gian màu tuyến tính cũng có nghĩa là alpha blending sẽ thay đổi. Các sprite có giá trị opacity thấp nhìn chung sẽ hiển thị rõ hơn, và việc render font sẽ trông đậm hơn do các pixel có opacity thấp từ quá trình antialiasing của font trở nên rõ hơn. Điều này cũng ảnh hưởng đến việc render của chính editor.

.. _doc_environment_and_post_processing_using_glow_to_blur_the_screen:

Sử dụng glow để làm mờ màn hình
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Glow có thể được dùng để làm mờ toàn bộ viewport, rất hữu ích khi làm mờ nền lúc một menu đang mở. Chỉ việc render 3D bị ảnh hưởng, trừ khi chế độ nền của environment được đặt thành **Canvas**. Để ngăn các phần tử UI bị làm mờ khi sử dụng chế độ nền Canvas, hãy đặt chúng làm con của một node :ref:`class_CanvasLayer`. Bạn có thể kiểm soát các layer bị hiệu ứng làm mờ này tác động bằng thuộc tính **Background > Canvas Max Layer** của resource Environment.

Để sử dụng glow như một giải pháp làm mờ:

- Bật **Normalized** và điều chỉnh các level theo ý muốn. Tăng các chỉ số level cao hơn sẽ tạo ra hình ảnh mờ hơn. Bạn nên để một level glow duy nhất ở ``1.0`` và giữ tất cả các level glow khác ở ``0.0``, nhưng đây không phải yêu cầu bắt buộc. Lưu ý rằng hình thức cuối cùng sẽ thay đổi tùy theo độ phân giải viewport.
- Đặt **Intensity** thành ``1.0`` và **Bloom** thành ``1.0``.
- Đặt blend mode thành **Replace** và **HDR Luminance Cap** thành ``1.0``.

.. figure:: img/environment_and_post_processing_glow_blur.webp
   :align: center
   :alt: Ví dụ sử dụng glow để làm mờ phần render 2D trong nền của menu

   Ví dụ sử dụng glow để làm mờ phần render 2D trong nền của menu

Fog
~~~

.. note::

    Phần này chỉ đề cập đến fog không thể tích. Có thể sử dụng đồng thời cả fog không thể tích và :ref:`doc_volumetric_fog`.

Fog, giống như trong đời thực, khiến các đối tượng ở xa dần biến mất vào một màu đồng nhất. Godot có hai loại fog:

- **Depth Fog:** Loại này được áp dụng dựa trên khoảng cách từ camera.
- **Height Fog:** Loại này được áp dụng cho mọi đối tượng bên dưới (hoặc bên trên) một độ cao nhất định, bất kể khoảng cách từ camera.

.. image:: img/environment_fog_depth_height.webp

Cả hai loại fog này đều có thể được tinh chỉnh các đường cong, khiến quá trình chuyển tiếp sắc nét hơn hoặc mềm hơn.

Có thể tinh chỉnh hai thuộc tính để làm hiệu ứng fog thú vị hơn:

Thuộc tính đầu tiên là **Sun Scatter**, sử dụng màu và năng lượng của DirectionalLight3D trong scene hiện tại. Khi nhìn về phía directional light (thường là mặt trời), fog sẽ được nhuộm màu theo màu của ánh sáng để mô phỏng ánh nắng đi qua fog.

Thuộc tính thứ hai là **Aerial Perspective**, nhuộm màu fog theo màu bầu trời để hòa trộn bầu trời với nền tốt hơn. Các giá trị cao hơn sẽ tạo ra mức nhuộm màu mạnh hơn, trong đó ``1.0`` thay thế hoàn toàn màu fog thông thường bằng aerial perspective. Điều này có thể được sử dụng trong các level open world lớn để tạo cảm nhận chiều sâu tốt hơn, hoặc để tránh sự gián đoạn màu giữa màu bầu trời và màu fog.

Nếu cả **Sun Scatter** và **Aerial Perspective** đều lớn hơn ``0.0``, hiệu ứng tán xạ ánh nắng sẽ được áp dụng chồng lên aerial perspective.

.. note::

    Fog có thể khiến banding xuất hiện trên viewport, đặc biệt ở các mức density cao hơn. Xem :ref:`doc_3d_rendering_limitations_color_banding` để biết hướng dẫn giảm banding.

Volumetric Fog
~~~~~~~~~~~~~~

Volumetric fog tạo hiệu ứng fog chân thực cho scene, trong đó màu fog chịu ảnh hưởng của các ánh sáng xuyên qua fog.

.. seealso::

  Xem :ref:`doc_volumetric_fog` để biết tài liệu về cách thiết lập volumetric fog.

Điều chỉnh
~~~~~~~~~~

Khi kết thúc quá trình xử lý, Godot cho phép thực hiện một số điều chỉnh hình ảnh tiêu chuẩn.

.. image:: img/environment_adjustments.webp

**Điều chỉnh BCS cơ bản**

Điều chỉnh đầu tiên là khả năng thay đổi các thuộc tính điển hình **Brightness**, **Contrast** và **Saturation**:

.. image:: img/environment_adjustments_bcs.webp

**Hiệu chỉnh màu bằng gradient 1D**

Điều chỉnh thứ hai là cung cấp một gradient hiệu chỉnh màu. Có thể thực hiện việc này bằng cách gán tài nguyên GradientTexture1D cho thuộc tính **Color Correction**, hoặc bằng cách tải một texture chứa gradient ngang. Phần ngoài cùng bên trái của gradient đại diện cho màu đen trong ảnh nguồn, còn phần ngoài cùng bên phải của gradient đại diện cho màu trắng trong ảnh nguồn.

Một gradient tuyến tính từ đen đến trắng như sau sẽ không tạo ra hiệu ứng nào:

.. image:: img/environment_adjustments_default_gradient.webp

Tuy nhiên, việc tạo các gradient tùy chỉnh sẽ cho phép ánh xạ mỗi kênh sang một màu khác nhau:

.. image:: img/environment_adjustments_custom_gradient.webp

**Hiệu chỉnh màu bằng LUT 3D**

Cũng có thể sử dụng texture tra cứu (LUT) 3D để hiệu chỉnh màu. Đây là một texture đặc biệt được dùng để sửa đổi riêng từng kênh màu (đỏ, xanh lá, xanh dương). Ảnh này có thể có độ phân giải bất kỳ, nhưng vì dữ liệu hiệu chỉnh màu có tần số thấp nên nên dùng độ phân giải thấp để đảm bảo hiệu năng. Độ phân giải của texture LUT thường là 17×17×17, 33×33×33, 51×51×51 hoặc 65×65×65 (kích thước lẻ cho phép nội suy tốt hơn).

Để hoạt động, chế độ import của texture tra cứu phải được đặt thành Texture3D trong dock Import (thay vì được import dưới dạng Texture2D thông thường):

.. image:: img/environment_adjustments_3d_lut_import.webp

Ngoài ra, hãy nhớ cấu hình số lát ngang và dọc cần import. Nếu không thực hiện việc này, texture LUT sẽ không tác động chính xác đến viewport khi được sử dụng. Bạn có thể xem trước cách texture 3D được import bằng cách nhấp đúp vào texture đó trong dock FileSystem, sau đó chuyển đến inspector để lật qua các lớp của texture.

Bạn có thể dùng mẫu LUT trung tính 33×33×33 này làm cơ sở (nhấp chuột phải và chọn **Save as…**):

.. image:: img/environment_adjustments_3d_lut_template.webp

Với mẫu LUT ở trên, sau khi đổi chế độ import thành **Texture3D**, hãy đặt số lát **Horizontal** thành ``33`` trong dock Import, sau đó nhấp **Reimport**. Nếu tải LUT này vào thuộc tính **Color Correction**, hiện tại bạn sẽ không thấy sự khác biệt nào vì texture này được thiết kế làm điểm khởi đầu trung tính.

Có thể sửa đổi mẫu LUT này trong trình chỉnh sửa ảnh để tạo cho ảnh một sắc thái khác. Một quy trình phổ biến là đặt ảnh LUT cạnh ảnh chụp màn hình viewport 3D của dự án, sau đó dùng trình chỉnh sửa ảnh để sửa đổi đồng thời cả ảnh LUT và ảnh chụp màn hình. Sau đó có thể lưu LUT và áp dụng vào game engine để thực hiện cùng một hiệu chỉnh màu theo thời gian thực.

Ví dụ, sửa đổi mẫu LUT trong trình chỉnh sửa ảnh để tạo cho nó vẻ ngoài "sepia" sẽ cho ra ảnh ở bên phải:

.. image:: img/environment_adjustments_3d_lut_comparison.webp

.. note::

    Các điều chỉnh và hiệu chỉnh màu được áp dụng *sau* quá trình tonemapping. Điều này có nghĩa là các thuộc tính tonemapping được xác định ở trên vẫn có tác dụng khi bật các điều chỉnh.

Tùy chọn thuộc tính camera
--------------------------

Godot có hai loại thuộc tính camera: physical và practical. Khi sử dụng CameraAttributesPhysical thay cho CameraAttributesPractical, độ sâu trường ảnh được tự động tính toán từ khoảng cách lấy nét, tiêu cự và khẩu độ của các thuộc tính camera. Ngoài ra, còn có các tùy chọn Frustum.

Độ sâu trường ảnh / Làm mờ xa
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiệu ứng này mô phỏng khoảng cách lấy nét trên camera. Hiệu ứng làm mờ các vật thể nằm phía sau một phạm vi nhất định. Hiệu ứng có **Distance** ban đầu cùng một vùng **Transition** (tính theo đơn vị trong thế giới):

.. image:: img/environment_dof_far.webp

Tham số **Amount** kiểm soát mức độ làm mờ. Để có độ mờ lớn hơn, có thể cần điều chỉnh chất lượng độ sâu trường ảnh trong phần cài đặt dự án nâng cao nhằm tránh hiện tượng lỗi.

Độ sâu trường ảnh / Làm mờ gần
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Hiệu ứng này mô phỏng khoảng cách lấy nét trên camera. Hiệu ứng làm mờ các vật thể ở gần camera (tác động theo hướng ngược với làm mờ xa). Hiệu ứng có **Distance** ban đầu cùng một vùng **Transition** (tính theo đơn vị trong thế giới):

.. image:: img/environment_dof_near.webp

Tham số **Amount** kiểm soát mức độ làm mờ. Để có độ mờ lớn hơn, có thể cần điều chỉnh chất lượng độ sâu trường ảnh trong phần cài đặt dự án nâng cao nhằm tránh hiện tượng lỗi.

Thông thường, người ta sử dụng cả hai hiệu ứng làm mờ cùng nhau để tập trung sự chú ý của người xem vào một vật thể nhất định hoặc tạo ra hiệu ứng còn gọi là `"tilt shift" <https://en.wikipedia.org/wiki/Miniature_faking>`__.

.. image:: img/environment_mixed_blur.webp

Phơi sáng
~~~~~~~~~

Tùy chọn này nhân độ sáng tổng thể của cảnh nhìn thấy từ camera. Giá trị cao hơn tạo ra cảnh sáng hơn về mặt thị giác.

Phơi sáng tự động
~~~~~~~~~~~~~~~~~

*Tính năng này chỉ khả dụng khi sử dụng renderer Forward+, không khả dụng với Mobile hoặc Compatibility.*

Mặc dù trong hầu hết trường hợp, ánh sáng và texture được nghệ sĩ kiểm soát chặt chẽ, Godot vẫn hỗ trợ một triển khai high dynamic range cơ bản với cơ chế phơi sáng tự động. Cơ chế này thường được dùng để tăng tính chân thực khi kết hợp các khu vực trong nhà có ánh sáng yếu với các khu vực ngoài trời sáng. Phơi sáng tự động mô phỏng camera (hoặc mắt người) nhằm thích ứng giữa các vị trí sáng và tối cũng như cường độ ánh sáng khác nhau của chúng.

.. note::

    Phơi sáng tự động cần đánh giá độ sáng của cảnh ở mỗi frame, gây ra một mức chi phí hiệu năng vừa phải. Vì vậy, bạn nên tắt Auto Exposure nếu nó không tạo ra nhiều khác biệt trong cảnh của mình.

.. image:: img/environment_hdr_autoexp.webp

Cách đơn giản nhất để sử dụng phơi sáng tự động là đảm bảo các đèn ngoài trời (hoặc các đèn mạnh khác) có energy lớn hơn 1.0. Việc này được thực hiện bằng cách điều chỉnh hệ số nhân **Energy** của chúng (trên chính Light). Để nhất quán, **Sky** thường cũng cần sử dụng hệ số nhân energy nhằm khớp với directional light. Thông thường, các giá trị từ 3.0 đến 6.0 là đủ để mô phỏng điều kiện trong nhà-ngoài trời.

Bằng cách kết hợp Auto Exposure với :ref:`doc_environment_and_post_processing_glow` post-processing, các pixel vượt quá **White** của tonemap sẽ tràn vào glow buffer, tạo ra hiệu ứng bloom đặc trưng trong nhiếp ảnh.

.. image:: img/environment_hdr_bloom.webp

Các giá trị do người dùng kiểm soát trong phần Auto Exposure có giá trị mặc định hợp lý, nhưng bạn vẫn có thể điều chỉnh chúng:

.. image:: img/environment_hdr.webp

- **Scale:** Giá trị dùng để điều chỉnh tỷ lệ ánh sáng. Giá trị cao hơn tạo ra ảnh sáng hơn, còn giá trị thấp hơn tạo ra ảnh tối hơn.
- **Min Sensitivity / Min Exposure Value:** Độ chói tối thiểu mà phơi sáng tự động sẽ cố gắng điều chỉnh đến (tính theo ISO khi sử dụng CameraAttributesPractical hoặc theo EV100 khi sử dụng CameraAttributesPhysical). Độ chói là giá trị trung bình của ánh sáng trên tất cả pixel của màn hình.
- **Max Sensitivity / Max Exposure Value:** Độ chói tối đa mà phơi sáng tự động sẽ cố gắng điều chỉnh đến (tính theo ISO khi sử dụng CameraAttributesPractical hoặc theo EV100 khi sử dụng CameraAttributesPhysical).
- **Speed:** Tốc độ tự điều chỉnh của độ chói. Giá trị càng cao thì quá trình điều chỉnh độ chói diễn ra càng nhanh. Các giá trị cao có thể phù hợp hơn với những game có nhịp độ nhanh, nhưng có thể gây mất tập trung trong một số tình huống.

Khi sử dụng CameraAttributesPractical, độ phơi sáng được thiết lập bằng *sensitivity* tính theo ISO thay vì giá trị phơi sáng theo EV100. Các giá trị ISO điển hình nằm trong khoảng từ 50 đến 3200, trong đó giá trị cao hơn tạo ra độ phơi sáng cuối cùng cao hơn. Trong thực tế, nhiếp ảnh ban ngày thường sử dụng giá trị ISO từ 100 đến 800.

.. seealso::

    Xem :ref:`doc_physical_light_and_camera_units` nếu bạn muốn sử dụng các đơn vị trong thế giới thực để cấu hình độ phơi sáng, trường nhìn và độ sâu trường ảnh của camera.
