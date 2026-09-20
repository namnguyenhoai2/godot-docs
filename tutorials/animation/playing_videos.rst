.. _doc_playing_videos:

Phát video
==========

Godot hỗ trợ phát video bằng node :ref:`class_VideoStreamPlayer`.

Các định dạng phát được hỗ trợ
------------------------------

Định dạng duy nhất được hỗ trợ trong core là **Ogg Theora** (không nên nhầm với âm thanh Ogg Vorbis), cùng các track âm thanh Ogg Vorbis tùy chọn. Các extension có thể bổ sung hỗ trợ cho những định dạng khác.

H.264 và H.265 không thể được hỗ trợ trong core Godot vì cả hai đều bị ràng buộc bởi các bằng sáng chế phần mềm. AV1 không yêu cầu phí bản quyền, nhưng vẫn chậm khi decode trên CPU và hỗ trợ hardware decoding hiện chưa sẵn có trên tất cả GPU đang được sử dụng.

WebM từng được hỗ trợ trong core ở Godot 3.x, nhưng đã bị gỡ bỏ ở 4.0 vì có quá nhiều lỗi và khó bảo trì.

.. note::

    Bạn có thể bắt gặp các video có phần mở rộng ``.ogg`` hoặc ``.ogx``, vốn là các phần mở rộng chung cho dữ liệu bên trong một container Ogg.

    Đổi tên các phần mở rộng tệp này thành ``.ogv`` *có thể* cho phép video được import vào Godot. Tuy nhiên, không phải mọi tệp có phần mở rộng ``.ogg`` hoặc ``.ogx`` đều là video — một số tệp có thể chỉ chứa âm thanh.

Thiết lập VideoStreamPlayer
---------------------------

1. Tạo một node VideoStreamPlayer bằng hộp thoại Create New Node. 2. Chọn node VideoStreamPlayer trong scene tree dock, đi đến inspector và load một tệp ``.ogv`` vào thuộc tính Stream.

   - Nếu video của bạn chưa ở định dạng Ogg Theora, hãy chuyển đến
     :ref:`doc_playing_videos_recommended_theora_encoding_settings`.

3. Nếu muốn video phát ngay khi scene được load, hãy chọn **Autoplay** trong inspector. Nếu không, hãy để **Autoplay** bị tắt và gọi ``play()`` trên node VideoStreamPlayer trong một script để bắt đầu phát khi cần.

Xử lý việc thay đổi kích thước và các aspect ratio khác nhau
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Theo mặc định, VideoStreamPlayer sẽ tự động được thay đổi kích thước để khớp với độ phân giải của video. Bạn có thể để nó tuân theo cách sizing thông thường của :ref:`class_Control` bằng cách bật **Expand** trên node VideoStreamPlayer.

Để điều chỉnh cách node VideoStreamPlayer thay đổi kích thước theo kích thước cửa sổ, hãy điều chỉnh các anchor bằng menu **Layout** ở đầu viewport của 2D editor. Tuy nhiên, thiết lập này có thể không đủ mạnh để xử lý mọi use case, chẳng hạn như phát video fullscreen mà không làm biến dạng video (thay vào đó để trống ở các cạnh). Để có nhiều quyền kiểm soát hơn, bạn có thể sử dụng một
:ref:`class_AspectRatioContainer` node, which is designed to handle this kind of
use case:

Thêm một node AspectRatioContainer. Đảm bảo node này không phải là node con của bất kỳ node container nào khác. Chọn node AspectRatioContainer, sau đó đặt **Layout** của nó ở đầu 2D editor thành **Full Rect**. Đặt **Ratio** trong node AspectRatioContainer để khớp với aspect ratio của video. Bạn có thể sử dụng các công thức toán học trong inspector để hỗ trợ. Hãy nhớ biến một trong các toán hạng thành float. Nếu không, kết quả của phép chia sẽ luôn là một số nguyên.

.. figure:: img/playing_videos_aspect_ratio_container.png
   :figclass: figure-w480
   :align: center
   :alt: AspectRatioContainer's Ratio property being modified in the editor inspector

   This will evaluate to (approximately) 1.777778


Sau khi cấu hình AspectRatioContainer, hãy reparent node VideoStreamPlayer để nó trở thành node con của node AspectRatioContainer. Đảm bảo **Expand** được bật trên VideoStreamPlayer. Video của bạn giờ sẽ tự động scale để vừa toàn bộ màn hình mà không bị biến dạng.

.. seealso::

    Xem :ref:`doc_multiple_resolutions` để biết thêm mẹo hỗ trợ nhiều aspect ratio trong project của bạn.

Hiển thị video trên bề mặt 3D
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bằng cách sử dụng node VideoStreamPlayer làm node con của node :ref:`class_SubViewport`, bạn có thể hiển thị bất kỳ node 2D nào trên một bề mặt 3D. Ví dụ, cách này có thể được dùng để hiển thị các billboard động khi animation theo từng frame yêu cầu quá nhiều bộ nhớ.

Bạn có thể thực hiện việc này theo các bước sau:

1. Tạo một node :ref:`class_SubViewport`. Đặt kích thước của node này để khớp với kích thước video theo pixel. 2. Tạo một node VideoStreamPlayer *làm node con của node SubViewport* và chỉ định đường dẫn video cho node này. Đảm bảo **Expand** bị tắt và bật **Autoplay** nếu cần. 3. Tạo một node MeshInstance3D với tài nguyên PlaneMesh hoặc QuadMesh trong thuộc tính Mesh. Thay đổi kích thước mesh để khớp với aspect ratio của video (nếu không, video sẽ bị biến dạng). 4. Tạo một tài nguyên StandardMaterial3D mới trong thuộc tính **Material Override** thuộc phần GeometryInstance3D. 5. Bật **Local To Scene** trong phần Resource của StandardMaterial3D (ở cuối). Điều này *bắt buộc* trước khi bạn có thể sử dụng ViewportTexture trong thuộc tính Albedo Texture của nó. 6. Trong StandardMaterial3D, đặt thuộc tính **Albedo > Texture** thành **New ViewportTexture**. Chỉnh sửa tài nguyên mới bằng cách nhấp vào tài nguyên đó, sau đó chỉ định đường dẫn đến node SubViewport trong thuộc tính **Viewport Path**. 7. Bật **Albedo Texture Force sRGB** trong StandardMaterial3D để tránh màu sắc bị nhạt. 8. Nếu billboard được cho là sẽ tự phát ra ánh sáng, hãy đặt **Shading Mode** thành **Unshaded** để cải thiện hiệu suất rendering.

Xem :ref:`doc_viewports` và `GUI in 3D demo <https://github.com/godotengine/godot-demo-projects/tree/master/viewport/gui_in_3d>`__ để biết thêm thông tin về cách thiết lập này.

Lặp video
~~~~~~~~~

Để lặp video, bạn có thể bật thuộc tính **Loop**. Video sẽ được khởi động lại liền mạch khi phát đến cuối.

Lưu ý rằng việc đặt project setting **Video Delay Compensation** thành một giá trị khác 0 có thể khiến vòng lặp của bạn không liền mạch, vì quá trình đồng bộ âm thanh và video diễn ra ở đầu mỗi vòng lặp, gây ra việc bỏ lỡ frame không thường xuyên. Đặt **Video Delay Compensation** trong project settings thành **0** để tránh vấn đề dropped frame.

Điều kiện decode video và độ phân giải được khuyến nghị
-------------------------------------------------------

Việc decode video được thực hiện trên CPU, vì GPU không có hardware acceleration để decode video Theora. CPU desktop hiện đại có thể decode video Ogg Theora ở 1440p @ 60 FPS hoặc cao hơn, nhưng CPU mobile cấp thấp có thể gặp khó khăn với video độ phân giải cao.

Để đảm bảo video được decode mượt mà trên nhiều loại phần cứng:

- Khi phát triển game cho các nền tảng desktop, bạn nên encode tối đa ở 1080p (tốt nhất là 30 FPS). Hầu hết mọi người vẫn đang sử dụng màn hình có độ phân giải 1080p hoặc thấp hơn, vì vậy encode video ở độ phân giải cao hơn có thể không đáng với dung lượng tệp và yêu cầu CPU tăng thêm. - Khi phát triển game cho nền tảng mobile hoặc web, bạn nên encode tối đa ở 720p (tốt nhất là 30 FPS hoặc thậm chí thấp hơn). Khác biệt về hình ảnh giữa video 720p và 1080p trên thiết bị mobile thường không quá đáng kể.

Các giới hạn khi phát
---------------------

Việc triển khai phát video hiện tại trong Godot có một số giới hạn:

- Không hỗ trợ streaming video từ URL. - Chỉ hỗ trợ đầu ra âm thanh mono và stereo. Video có 4, 5.1 và 7.1 kênh âm thanh được hỗ trợ nhưng sẽ được down-mix thành stereo.

.. _doc_playing_videos_recommended_theora_encoding_settings:

Thiết lập encode Theora được khuyến nghị
----------------------------------------

Một lời khuyên là **tránh phụ thuộc vào các Ogg Theora exporter tích hợp sẵn** (hầu hết thời gian). Có 2 lý do khiến bạn nên ưu tiên sử dụng một chương trình bên ngoài để encode video:

- Một số chương trình như Blender có thể render sang Ogg Theora. Tuy nhiên, các preset chất lượng mặc định thường rất thấp theo tiêu chuẩn hiện nay. Bạn có thể tăng các tùy chọn chất lượng trong phần mềm đang sử dụng, nhưng có thể nhận thấy chất lượng đầu ra vẫn chưa lý tưởng (xét đến dung lượng tệp tăng thêm). Điều này thường có nghĩa là phần mềm chỉ hỗ trợ encode với constant bit rate (CBR), thay vì variable bit rate (VBR). Trong hầu hết trường hợp, nên ưu tiên encode VBR vì cho tỷ lệ chất lượng trên dung lượng tệp tốt hơn. - Một số chương trình khác hoàn toàn không thể render sang Ogg Theora.

Trong trường hợp này, bạn có thể **render video sang một định dạng trung gian chất lượng cao** (chẳng hạn như video H.264 bitrate cao), sau đó re-encode sang Ogg Theora. Tốt nhất, bạn nên sử dụng định dạng lossless hoặc không nén làm định dạng trung gian để tối đa hóa chất lượng của video Ogg Theora đầu ra, nhưng việc này có thể yêu cầu rất nhiều dung lượng đĩa.

`FFmpeg <https://ffmpeg.org/>`__ (CLI) là một công cụ mã nguồn mở phổ biến cho mục đích này. FFmpeg có learning curve khá dốc, nhưng là một công cụ mạnh mẽ.

Dưới đây là các lệnh FFmpeg mẫu để chuyển đổi video MP4 sang Ogg Theora. Vì FFmpeg hỗ trợ rất nhiều định dạng đầu vào, bạn có thể sử dụng các lệnh dưới đây với hầu hết mọi định dạng video đầu vào (AVI, MOV, WebM, …).

.. note::

   Đảm bảo bản FFmpeg của bạn được compile với hỗ trợ libtheora và libvorbis. Bạn có thể kiểm tra điều này bằng cách chạy ``ffmpeg`` mà không có argument nào, sau đó xem dòng ``configuration:`` trong output của lệnh.

.. warning::

   Các bản phát hành FFmpeg chính thức hiện tại có một số bug trong Ogg/Theora multiplexer. Bạn nên sử dụng một trong các static daily build mới nhất hoặc build từ master branch của họ để nhận được các bản sửa mới nhất.

   Trên Windows, hãy đảm bảo sử dụng bản build 32-bit của FFmpeg. Các bản build 64-bit của Windows có các vấn đề đã biết với việc encode Theora, dẫn đến artifact trong tệp đầu ra.

Cân bằng chất lượng và dung lượng tệp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mức **video quality** (``-q:v``) phải nằm giữa ``1`` và ``10``. Quality ``6`` là một thỏa hiệp tốt giữa chất lượng và dung lượng tệp. Nếu encode ở độ phân giải cao (chẳng hạn như 1440p hoặc 4K), có lẽ bạn sẽ muốn giảm ``-q:v`` xuống ``5`` để giữ dung lượng tệp ở mức hợp lý. Vì mật độ pixel cao hơn trên video 1440p hoặc 4K, các preset chất lượng thấp hơn ở độ phân giải cao sẽ cho hình ảnh đẹp tương đương hoặc tốt hơn so với video độ phân giải thấp.

Mức **chất lượng âm thanh** (``-q:a``) phải nằm trong khoảng từ ``-1`` đến ``10``. Chất lượng ``6`` mang đến sự cân bằng tốt giữa chất lượng và kích thước tệp. Không giống như chất lượng video, việc tăng chất lượng âm thanh gần như không làm tăng kích thước tệp đầu ra nhiều đến vậy. Vì thế, nếu muốn âm thanh trong trẻo nhất có thể, bạn có thể tăng giá trị này lên ``9`` để có âm thanh *gần như không mất mát theo cảm nhận*. Điều này đặc biệt hữu ích nếu tệp đầu vào của bạn đã sử dụng tính năng nén âm thanh có mất dữ liệu. Âm thanh chất lượng cao hơn sẽ làm tăng mức sử dụng CPU của decoder, vì vậy có thể dẫn đến hiện tượng âm thanh bị ngắt quãng khi hệ thống chịu tải cao. Xem `this page <https://wiki.hydrogenaud.io/index.php?title=Recommended_Ogg_Vorbis#Recommended_Encoder_Settings>`__ để biết bảng liệt kê các preset chất lượng âm thanh Ogg Vorbis và bitrate biến thiên tương ứng của chúng.

**Kích thước GOP (Group of Pictures)** (``-g:v``) là khoảng thời gian tối đa giữa các keyframe. Việc tăng giá trị này có thể cải thiện khả năng nén mà hầu như không ảnh hưởng đến chất lượng. Kích thước mặc định (``12``) quá thấp đối với hầu hết các loại nội dung, vì vậy bạn nên sử dụng giá trị GOP cao hơn trước khi giảm chất lượng video. Tuy nhiên, lợi ích nén sẽ giảm dần khi kích thước GOP tăng. Các giá trị từ ``64`` đến ``512`` thường cho khả năng nén tốt nhất.

.. note::

   Kích thước GOP lớn hơn sẽ làm tăng thời gian seek tối đa, với mức tăng đột ngột khi vượt qua các lũy thừa của hai, bắt đầu từ ``64``. Thời gian seek tối đa với kích thước GOP ``65`` có thể dài gần gấp đôi so với kích thước GOP ``64``, tùy thuộc vào tốc độ decoding.

FFmpeg: Chuyển đổi trong khi giữ nguyên độ phân giải video gốc
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lệnh sau đây chuyển đổi video trong khi giữ nguyên độ phân giải gốc. Bitrate của video và âm thanh sẽ thay đổi để tối đa hóa chất lượng, đồng thời tiết kiệm dung lượng ở những phần video/âm thanh không cần bitrate cao (chẳng hạn như các cảnh tĩnh).

::

    ffmpeg -i input.mp4 -q:v 6 -q:a 6 -g:v 64 output.ogv

FFmpeg: Thay đổi kích thước video rồi chuyển đổi
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Lệnh sau đây thay đổi kích thước video để có chiều cao 720 pixel (720p), đồng thời giữ nguyên tỷ lệ khung hình hiện có. Điều này giúp giảm đáng kể kích thước tệp nếu nguồn được ghi ở độ phân giải cao hơn 720p:

::

    ffmpeg -i input.mp4 -vf "scale=-1:720" -q:v 6 -q:a 6 -g:v 64 output.ogv


.. Tài liệu về chức năng Chroma Key

Video Chroma Key
----------------

Chroma key, thường được biết đến là hiệu ứng "green screen" hoặc "blue screen", cho phép bạn loại bỏ một màu cụ thể khỏi hình ảnh hoặc video và thay thế màu đó bằng một background khác. Hiệu ứng này được sử dụng rộng rãi trong sản xuất video để compositing các thành phần khác nhau một cách liền mạch.

   .. image:: img/chroma_key_video.webp

Chúng ta sẽ tạo hiệu ứng chroma key bằng cách viết một shader tùy chỉnh trong GDScript và sử dụng node `VideoStreamPlayer` để hiển thị nội dung video.

Thiết lập Scene
~~~~~~~~~~~~~~~

Đảm bảo scene chứa một node `VideoStreamPlayer` để phát video và một node `Control` để chứa các thành phần UI điều khiển hiệu ứng chroma key.

   .. image:: img/chroma_key_scene.webp

Viết Shader tùy chỉnh
~~~~~~~~~~~~~~~~~~~~~

Để triển khai hiệu ứng chroma key, hãy thực hiện các bước sau:

1. Chọn node `VideoStreamPlayer` trong scene và đi đến các thuộc tính của node. Trong `CanvasItem > Material`, hãy tạo một shader mới có tên "ChromaKeyShader.gdshader."

2. Trong tệp "ChromaKeyShader.gdshader", hãy viết mã shader tùy chỉnh như dưới đây:

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

       // Nếu khoảng cách nằm trong phạm vi loại bỏ, loại bỏ pixel
       // khoảng cách càng nhỏ thì màu càng có khả năng tương đồng
       if (distance <= pickup_range) {
           discard;
       }

       // Tính hệ số fade dựa trên phạm vi loại bỏ và lượng fade
       float fade_factor = smoothstep(pickup_range, pickup_range + fade_amount, distance);

       // Thiết lập màu đầu ra với các giá trị RGB gốc và hệ số fade đã tính
       COLOR = vec4(color.rgb, fade_factor);
   }

Shader sử dụng phép tính khoảng cách để xác định các pixel gần với màu chroma key và loại bỏ chúng, qua đó loại bỏ màu đã chọn một cách hiệu quả. Các pixel cách màu chroma key xa hơn một chút sẽ được fade dựa trên fade_factor, hòa trộn mượt mà với các màu xung quanh. Quá trình này tạo ra hiệu ứng chroma key mong muốn, khiến background trông như đã được thay thế bằng một hình ảnh hoặc video khác.

Đoạn mã trên là một minh họa đơn giản về shader Chroma Key và người dùng có thể tùy chỉnh nó theo các yêu cầu cụ thể của mình.

Các điều khiển UI
~~~~~~~~~~~~~~~~~

Để cho phép người dùng điều chỉnh hiệu ứng chroma key theo thời gian thực, chúng ta đã tạo các slider trong node `Control`. Script của node `Control` chứa các hàm sau:

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
        # Khởi động lại video playback khi video kết thúc.
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
            // Khởi động lại video playback khi video kết thúc.
            _videoStreamPlayer.Play();
        }
    }

đồng thời đảm bảo range của các slider là phù hợp, các thiết lập của chúng ta là:

   .. image:: img/slider_range.webp

Xử lý Signal
~~~~~~~~~~~~

Kết nối signal thích hợp từ các thành phần UI với script của node `Control` mà bạn đã tạo để điều khiển hiệu ứng chroma key. Các signal handler này sẽ cập nhật các biến uniform của shader để phản hồi thao tác nhập của người dùng.

Lưu và chạy scene để xem hiệu ứng chroma key hoạt động! Với các điều khiển UI được cung cấp, giờ đây bạn có thể điều chỉnh màu chroma key, pickup range và fade amount theo thời gian thực, đạt được chức năng chroma key mong muốn cho nội dung video của mình.
