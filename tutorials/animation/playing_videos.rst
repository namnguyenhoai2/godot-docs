.. _doc_playing_videos:

Phát video
==========

Godot hỗ trợ phát video bằng node :ref:`class_VideoStreamPlayer`.

Các định dạng phát được hỗ trợ
------------------------------

Định dạng duy nhất được hỗ trợ trong core là **Ogg Theora** (không nên nhầm với âm thanh Ogg Vorbis), cùng với các track âm thanh Ogg Vorbis tùy chọn. Các extension có thể bổ sung hỗ trợ cho những định dạng khác.

H.264 và H.265 không thể được hỗ trợ trong core Godot vì cả hai đều bị ràng buộc bởi các bằng sáng chế phần mềm. AV1 không yêu cầu phí bản quyền, nhưng vẫn mất nhiều thời gian để giải mã trên CPU và hỗ trợ giải mã bằng phần cứng hiện chưa sẵn có trên tất cả GPU đang được sử dụng.

WebM từng được hỗ trợ trong core ở Godot 3.x, nhưng đã bị loại bỏ trong 4.0 vì có quá nhiều lỗi và khó bảo trì.

.. note::

    Bạn có thể bắt gặp các video có phần mở rộng ``.ogg`` hoặc ``.ogx``, đây là các phần mở rộng chung cho dữ liệu bên trong một container Ogg.

    Đổi tên các phần mở rộng tệp này thành ``.ogv`` *có thể* cho phép nhập video vào Godot. Tuy nhiên, không phải mọi tệp có phần mở rộng ``.ogg`` hoặc ``.ogx`` đều là video - một số tệp có thể chỉ chứa âm thanh.

Thiết lập VideoStreamPlayer
---------------------------

1. Tạo một node VideoStreamPlayer bằng hộp thoại Create New Node.
2. Chọn node VideoStreamPlayer trong scene tree dock, đi đến inspector và tải một tệp ``.ogv`` vào thuộc tính Stream.

   - Nếu video của bạn chưa ở định dạng Ogg Theora, hãy chuyển đến
     :ref:`doc_playing_videos_recommended_theora_encoding_settings`.

3. Nếu muốn video phát ngay khi scene được tải, hãy chọn **Autoplay** trong inspector. Nếu không, để **Autoplay** bị tắt và gọi ``play()`` trên node VideoStreamPlayer trong script để bắt đầu phát khi muốn.

Xử lý việc thay đổi kích thước và các tỷ lệ khung hình khác nhau
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, VideoStreamPlayer sẽ tự động được thay đổi kích thước để khớp với độ phân giải của video. Bạn có thể khiến nó tuân theo cách :ref:`class_Control` định kích thước thông thường bằng cách bật **Expand** trên node VideoStreamPlayer.

Để điều chỉnh cách node VideoStreamPlayer thay đổi kích thước tùy theo kích thước cửa sổ, hãy điều chỉnh các anchor bằng menu **Layout** ở đầu viewport của trình chỉnh sửa 2D. Tuy nhiên, thiết lập này có thể không đủ mạnh để xử lý mọi trường hợp sử dụng, chẳng hạn như phát video toàn màn hình mà không làm biến dạng video (thay vào đó để lại khoảng trống ở các cạnh). Để kiểm soát tốt hơn, bạn có thể sử dụng một
node :ref:`class_AspectRatioContainer`, được thiết kế để xử lý loại trường hợp sử dụng này:

Thêm một node AspectRatioContainer. Đảm bảo node này không phải là node con của bất kỳ node container nào khác. Chọn node AspectRatioContainer, sau đó đặt **Layout** của nó ở đầu trình chỉnh sửa 2D thành **Full Rect**. Đặt **Ratio** trong node AspectRatioContainer để khớp với tỷ lệ khung hình của video. Bạn có thể sử dụng các công thức toán học trong inspector để hỗ trợ. Hãy nhớ đặt một trong các toán hạng là số thực. Nếu không, kết quả phép chia sẽ luôn là số nguyên.

.. figure:: img/playing_videos_aspect_ratio_container.png
   :figclass: figure-w480
   :align: center
   :alt: Thuộc tính Ratio của AspectRatioContainer đang được chỉnh sửa trong inspector của trình chỉnh sửa

   Giá trị này sẽ được tính thành (xấp xỉ) 1.777778


Sau khi cấu hình AspectRatioContainer, hãy chuyển node VideoStreamPlayer thành node con của node AspectRatioContainer. Đảm bảo **Expand** được bật trên VideoStreamPlayer. Video của bạn giờ sẽ tự động co giãn để vừa toàn bộ màn hình mà không bị biến dạng.

.. seealso::

    Xem :ref:`doc_multiple_resolutions` để biết thêm mẹo hỗ trợ nhiều tỷ lệ khung hình trong dự án của bạn.

Hiển thị video trên bề mặt 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bằng cách sử dụng node VideoStreamPlayer làm node con của node :ref:`class_SubViewport`, bạn có thể hiển thị bất kỳ node 2D nào trên bề mặt 3D. Ví dụ, cách này có thể được dùng để hiển thị billboard động khi hoạt ảnh theo từng khung hình sẽ yêu cầu quá nhiều bộ nhớ.

Bạn có thể thực hiện việc này theo các bước sau:

1. Tạo một node :ref:`class_SubViewport`. Đặt kích thước của nó khớp với kích thước video tính bằng pixel.
2. Tạo một node VideoStreamPlayer *làm node con của node SubViewport* và chỉ định đường dẫn video cho nó. Đảm bảo **Expand** bị tắt, và bật **Autoplay** nếu cần.
3. Tạo một node MeshInstance3D với tài nguyên PlaneMesh hoặc QuadMesh trong thuộc tính Mesh của nó. Thay đổi kích thước mesh để khớp với tỷ lệ khung hình của video (nếu không, video sẽ bị biến dạng).
4. Tạo một tài nguyên StandardMaterial3D mới trong thuộc tính **Material Override** ở phần GeometryInstance3D.
5. Bật **Local To Scene** trong phần Resource của StandardMaterial3D (ở dưới cùng). Điều này *bắt buộc* trước khi bạn có thể sử dụng ViewportTexture trong thuộc tính Albedo Texture của nó.
6. Trong StandardMaterial3D, đặt thuộc tính **Albedo > Texture** thành **New ViewportTexture**. Chỉnh sửa tài nguyên mới bằng cách nhấp vào nó, sau đó chỉ định đường dẫn đến node SubViewport trong thuộc tính **Viewport Path**.
7. Bật **Albedo Texture Force sRGB** trong StandardMaterial3D để ngăn màu sắc bị nhạt đi.
8. Nếu billboard được cho là sẽ tự phát sáng, hãy đặt **Shading Mode** thành **Unshaded** để cải thiện hiệu năng kết xuất.

Xem :ref:`doc_viewports` và `GUI in 3D demo <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/gui_in_3d>`__ để biết thêm thông tin về cách thiết lập này.

Lặp video
~~~~~~~~~

Để lặp video, bạn có thể bật thuộc tính **Loop**. Thuộc tính này sẽ khởi động lại video một cách liền mạch khi video phát đến cuối.

Lưu ý rằng việc đặt thiết lập dự án **Video Delay Compensation** thành một giá trị khác không có thể khiến vòng lặp của bạn không còn liền mạch, vì quá trình đồng bộ hóa âm thanh và video diễn ra ở đầu mỗi vòng lặp, gây ra việc bỏ lỡ một số khung hình. Đặt **Video Delay Compensation** trong thiết lập dự án thành **0** để tránh các vấn đề rớt khung hình.

Điều kiện giải mã video và độ phân giải được khuyến nghị
--------------------------------------------------------

Việc giải mã video được thực hiện trên CPU, vì GPU không có khả năng tăng tốc phần cứng để giải mã video Ogg Theora. CPU máy tính để bàn hiện đại có thể giải mã video Ogg Theora ở 1440p @ 60 FPS hoặc cao hơn, nhưng CPU di động cấp thấp có thể sẽ gặp khó khăn với video độ phân giải cao.

Để đảm bảo video được giải mã mượt mà trên nhiều loại phần cứng:

- Khi phát triển game cho nền tảng máy tính để bàn, bạn nên mã hóa ở độ phân giải tối đa 1080p (tốt nhất là 30 FPS). Hầu hết mọi người vẫn đang sử dụng màn hình có độ phân giải 1080p hoặc thấp hơn, vì vậy việc mã hóa video ở độ phân giải cao hơn có thể không đáng với kích thước tệp và yêu cầu CPU tăng lên.
- Khi phát triển game cho nền tảng di động hoặc web, bạn nên mã hóa ở độ phân giải tối đa 720p (tốt nhất là 30 FPS hoặc thậm chí thấp hơn). Khác biệt về hình ảnh giữa video 720p và 1080p trên thiết bị di động thường không quá rõ rệt.

Các giới hạn phát lại
---------------------

Việc triển khai phát lại video hiện tại trong Godot có một số giới hạn:

- Không hỗ trợ stream video từ URL.
- Chỉ hỗ trợ đầu ra âm thanh mono và stereo. Video có 4, 5.1 và 7.1 kênh âm thanh vẫn được hỗ trợ, nhưng sẽ được down-mix xuống stereo.

.. _doc_playing_videos_recommended_theora_encoding_settings:

Thiết lập mã hóa Theora được khuyến nghị
----------------------------------------

Một lời khuyên là **tránh phụ thuộc vào các trình xuất Ogg Theora tích hợp sẵn** (trong hầu hết trường hợp). Có 2 lý do khiến bạn nên ưu tiên sử dụng chương trình bên ngoài để mã hóa video:

- Một số chương trình như Blender có thể render sang Ogg Theora. Tuy nhiên, các preset chất lượng mặc định thường rất thấp theo tiêu chuẩn hiện nay. Bạn có thể tăng các tùy chọn chất lượng trong phần mềm đang sử dụng, nhưng có thể nhận thấy chất lượng đầu ra vẫn chưa lý tưởng (dù kích thước tệp đã tăng). Điều này thường có nghĩa là phần mềm chỉ hỗ trợ mã hóa với bitrate không đổi (CBR), thay vì bitrate biến đổi (VBR). Trong hầu hết trường hợp, nên ưu tiên mã hóa VBR vì nó mang lại tỷ lệ chất lượng trên kích thước tệp tốt hơn.
- Một số chương trình khác hoàn toàn không thể render sang Ogg Theora.

Trong trường hợp này, bạn có thể **render video sang một định dạng trung gian có chất lượng cao** (chẳng hạn video H.264 có bitrate cao), sau đó mã hóa lại sang Ogg Theora. Lý tưởng nhất là sử dụng định dạng không mất dữ liệu hoặc không nén làm định dạng trung gian để tối đa hóa chất lượng của video Ogg Theora đầu ra, nhưng cách này có thể yêu cầu rất nhiều dung lượng đĩa.

`FFmpeg <https://ffmpeg.org/>`__ (CLI) là một công cụ mã nguồn mở phổ biến cho mục đích này. FFmpeg có đường cong học tập khá dốc, nhưng đây là một công cụ mạnh mẽ.

Sau đây là các lệnh FFmpeg mẫu để chuyển đổi video MP4 sang Ogg Theora. Vì FFmpeg hỗ trợ rất nhiều định dạng đầu vào, bạn có thể sử dụng các lệnh dưới đây với hầu hết mọi định dạng video đầu vào (AVI, MOV, WebM, …).

.. note::

   Hãy đảm bảo bản FFmpeg của bạn được biên dịch với hỗ trợ libtheora và libvorbis. Bạn có thể kiểm tra bằng cách chạy ``ffmpeg`` mà không có đối số nào, sau đó tìm dòng ``configuration:`` trong đầu ra của lệnh.

.. warning::

   Các bản phát hành FFmpeg chính thức hiện tại có một số lỗi trong bộ ghép kênh Ogg/Theora. Bạn nên sử dụng một trong các bản build tĩnh hằng ngày mới nhất hoặc build từ nhánh master của họ để nhận các bản sửa lỗi mới nhất.

   Trên Windows, hãy đảm bảo sử dụng các bản build 32-bit của FFmpeg. Các bản build 64-bit của Windows có những vấn đề đã biết với việc mã hóa Theora, dẫn đến hiện tượng nhiễu trong tệp đầu ra.

Cân bằng chất lượng và kích thước tệp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mức **chất lượng video** (``-q:v``) phải nằm trong khoảng từ ``1`` đến ``10``. Chất lượng ``6`` là một sự cân bằng tốt giữa chất lượng và kích thước tệp. Nếu mã hóa ở độ phân giải cao (chẳng hạn 1440p hoặc 4K), có lẽ bạn sẽ muốn giảm ``-q:v`` xuống ``5`` để giữ kích thước tệp ở mức hợp lý. Vì mật độ điểm ảnh cao hơn trên video 1440p hoặc 4K, các preset chất lượng thấp hơn ở độ phân giải cao sẽ cho hình ảnh đẹp tương đương hoặc tốt hơn so với video độ phân giải thấp.

Mức **chất lượng âm thanh** (``-q:a``) phải nằm trong khoảng từ ``-1`` đến ``10``. Chất lượng ``6`` mang lại sự cân bằng tốt giữa chất lượng và kích thước tệp. Trái với chất lượng video, việc tăng chất lượng âm thanh không làm tăng kích thước tệp đầu ra nhiều như vậy. Vì thế, nếu muốn âm thanh trong trẻo nhất có thể, bạn có thể tăng mức này lên ``9`` để có âm thanh *gần như không mất dữ liệu*. Điều này đặc biệt có giá trị nếu tệp đầu vào vốn đã sử dụng tính năng nén âm thanh có mất dữ liệu. Âm thanh chất lượng cao hơn làm tăng mức sử dụng CPU của bộ giải mã, vì vậy có thể dẫn đến hiện tượng mất tiếng khi hệ thống chịu tải cao. Xem `trang này <https://wiki.hydrogenaud.io/index.php?title=Recommended_Ogg_Vorbis#Recommended_Encoder_Settings>`__ để biết bảng liệt kê các preset chất lượng âm thanh Ogg Vorbis và bitrate biến đổi tương ứng của chúng.

**Kích thước GOP (Group of Pictures)** (``-g:v``) là khoảng thời gian tối đa giữa các keyframe. Việc tăng giá trị này có thể cải thiện khả năng nén mà hầu như không ảnh hưởng đến chất lượng. Kích thước mặc định (``12``) quá thấp đối với hầu hết loại nội dung, do đó bạn nên sử dụng các giá trị GOP cao hơn trước khi giảm chất lượng video. Tuy nhiên, lợi ích nén sẽ giảm dần khi kích thước GOP tăng. Các giá trị từ ``64`` đến ``512`` thường cho khả năng nén tốt nhất.

.. note::

   Kích thước GOP lớn hơn sẽ làm tăng thời gian seek tối đa, với mức tăng đột ngột khi vượt qua các lũy thừa của hai bắt đầu từ ``64``. Thời gian seek tối đa với kích thước GOP ``65`` có thể dài gần gấp đôi so với kích thước GOP ``64``, tùy thuộc vào tốc độ giải mã.

FFmpeg: Chuyển đổi và giữ nguyên độ phân giải video ban đầu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lệnh sau chuyển đổi video trong khi giữ nguyên độ phân giải ban đầu. Bitrate của video và âm thanh sẽ biến đổi để tối đa hóa chất lượng, đồng thời tiết kiệm dung lượng ở những phần video/âm thanh không cần bitrate cao (chẳng hạn các cảnh tĩnh).

::

    ffmpeg -i input.mp4 -q:v 6 -q:a 6 -g:v 64 output.ogv

FFmpeg: Thay đổi kích thước video rồi chuyển đổi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lệnh sau thay đổi kích thước video để có chiều cao 720 pixel (720p), đồng thời giữ nguyên tỷ lệ khung hình hiện có. Điều này giúp giảm đáng kể kích thước tệp nếu nguồn được ghi ở độ phân giải cao hơn 720p:

::

    ffmpeg -i input.mp4 -vf "scale=-1:720" -q:v 6 -q:a 6 -g:v 64 output.ogv


.. Chroma Key Functionality Documentation

Video Chroma Key
----------------

Chroma key, thường được gọi là hiệu ứng "màn hình xanh" hoặc "màn hình xanh dương", cho phép bạn loại bỏ một màu cụ thể khỏi hình ảnh hoặc video và thay thế bằng nền khác. Hiệu ứng này được sử dụng rộng rãi trong sản xuất video để ghép liền mạch các thành phần khác nhau.

   .. image:: img/chroma_key_video.webp

Chúng ta sẽ tạo hiệu ứng chroma key bằng cách viết một shader tùy chỉnh trong GDScript và sử dụng node `VideoStreamPlayer` để hiển thị nội dung video.

Thiết lập cảnh
~~~~~~~~~~~~~~

Đảm bảo cảnh chứa một node `VideoStreamPlayer` để phát video và một node `Control` để chứa các phần tử UI điều khiển hiệu ứng chroma key.

   .. image:: img/chroma_key_scene.webp

Viết shader tùy chỉnh
~~~~~~~~~~~~~~~~~~~~~

Để triển khai hiệu ứng chroma key, hãy làm theo các bước sau:

1. Chọn node `VideoStreamPlayer` trong scene và đi tới phần thuộc tính của node. Trong `CanvasItem > Material`, tạo một shader mới có tên "ChromaKeyShader.gdshader."

2. Trong tệp "ChromaKeyShader.gdshader", viết mã shader tùy chỉnh như bên dưới:

.. code-block:: glsl

   shader_type canvas_item;

   // Các biến uniform cho hiệu ứng chroma key
   uniform vec3 chroma_key_color : source_color = vec3(0.0, 1.0, 0.0);
   uniform float pickup_range : hint_range(0.0, 1.0) = 0.1;
   uniform float fade_amount : hint_range(0.0, 1.0) = 0.1;

   void fragment() {
       // Lấy màu từ texture tại các tọa độ UV đã cho
       vec4 color = texture(TEXTURE, UV);

       // Tính khoảng cách giữa màu hiện tại và màu chroma key
       float distance = length(color.rgb - chroma_key_color);

       // Nếu khoảng cách nằm trong phạm vi chọn, loại bỏ pixel
       // khoảng cách càng nhỏ thì màu càng có khả năng giống nhau
       if (distance <= pickup_range) {
           discard;
       }

       // Tính hệ số mờ dựa trên phạm vi chọn và mức độ mờ
       float fade_factor = smoothstep(pickup_range, pickup_range + fade_amount, distance);

       // Thiết lập màu đầu ra bằng các giá trị RGB ban đầu và hệ số mờ đã tính
       COLOR = vec4(color.rgb, fade_factor);
   }

Shader sử dụng phép tính khoảng cách để xác định các pixel gần với màu chroma key và loại bỏ chúng, qua đó xóa màu đã chọn một cách hiệu quả. Các pixel cách màu chroma key xa hơn một chút sẽ được làm mờ dựa trên fade_factor, hòa trộn mượt mà với các màu xung quanh. Quá trình này tạo ra hiệu ứng chroma key mong muốn, khiến hình ảnh giống như phần nền đã được thay thế bằng một hình ảnh hoặc video khác.

Đoạn mã trên là một minh họa đơn giản về shader Chroma Key và người dùng có thể tùy chỉnh theo yêu cầu cụ thể của mình.

Điều khiển giao diện
~~~~~~~~~~~~~~~~~~~~

Để cho phép người dùng điều chỉnh hiệu ứng chroma key theo thời gian thực, chúng ta đã tạo các thanh trượt trong node `Control`. Script của node `Control` chứa các hàm sau:

.. tabs::
 .. code-tab:: gdscript

    extends Control

    func _on_color_picker_button_color_changed(color):
        # Cập nhật tham số shader "chroma_key_color" của material của VideoStreamPlayer.
        $VideoStreamPlayer.material.set("shader_parameter/chroma_key_color", color)

    func _on_h_slider_value_changed(value):
        # Cập nhật tham số shader "pickup_range" của material của VideoStreamPlayer.
        $VideoStreamPlayer.material.set("shader_parameter/pickup_range", value)

    func _on_h_slider_2_value_changed(value):
        # Cập nhật tham số shader "fade_amount" của material của VideoStreamPlayer.
        $VideoStreamPlayer.material.set("shader_parameter/fade_amount", value)

   func _on_video_stream_player_finished():
        # Khởi động lại video khi video phát xong.
        $VideoStreamPlayer.play()

 .. code-tab:: csharp

    using Godot;

    public partial class MyControl : Control
    {
        private VideoStreamPlayer _videoStreamPlayer;

        public override void _Ready()
        {
            _videoStreamPlayer = GetNode<VideoStreamPlayer>("VideoStreamPlayer");
        }

        private void OnColorPickerButtonColorChanged(Color color)
        {
            // Cập nhật tham số shader "chroma_key_color" của material của VideoStreamPlayer.
            _videoStreamPlayer.Material.Set("shader_parameter/chroma_key_color", color);
        }

        private void OnHSliderValueChanged(double value)
        {
            // Cập nhật tham số shader "pickup_range" của material của VideoStreamPlayer.
            _videoStreamPlayer.Material.Set("shader_parameter/pickup_range", value);
        }

        private void OnHSlider2ValueChanged(double value)
        {
            // Cập nhật tham số shader "fade_amount" của material của VideoStreamPlayer.
            _videoStreamPlayer.Material.Set("shader_parameter/fade_amount", value);
        }

        private void OnVideoStreamPlayerFinished()
        {
            // Khởi động lại video khi video phát xong.
            _videoStreamPlayer.Play();
        }
    }

đồng thời hãy đảm bảo rằng phạm vi của các thanh trượt là phù hợp, các thiết lập của chúng ta là:

   .. image:: img/slider_range.webp

Xử lý signal
~~~~~~~~~~~~

Kết nối signal thích hợp từ các phần tử UI với script của node `Control`. Bạn đã tạo signal này trong script của node `Control` để điều khiển hiệu ứng chroma key. Các signal handler này sẽ cập nhật các biến uniform của shader để phản hồi thao tác nhập của người dùng.

Lưu và chạy scene để xem hiệu ứng chroma key hoạt động! Với các điều khiển UI được cung cấp, giờ đây bạn có thể điều chỉnh màu chroma key, phạm vi chọn và mức độ mờ theo thời gian thực, đạt được chức năng chroma key mong muốn cho nội dung video của mình.
