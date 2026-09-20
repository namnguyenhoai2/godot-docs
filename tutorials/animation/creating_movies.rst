.. _doc_creating_movies:

Tạo phim
========

Godot có thể ghi video và âm thanh **không theo thời gian thực** từ bất kỳ dự án 2D hoặc 3D nào. Kiểu ghi này còn được gọi là *kết xuất ngoại tuyến (offline rendering)*. Có nhiều trường hợp việc này hữu ích:

- Ghi trailer game để quảng bá. - Ghi các đoạn cắt cảnh sẽ được :ref:`displayed as pre-recorded videos <doc_playing_videos>` trong game cuối cùng. Điều này cho phép sử dụng các thiết lập chất lượng cao hơn (đổi lại là kích thước tệp lớn hơn), bất kể phần cứng của người chơi. - Ghi các animation được tạo theo quy trình (procedurally generated) hoặc motion design. Tương tác của người dùng vẫn khả dụng trong khi ghi video, đồng thời có thể đưa âm thanh vào (mặc dù bạn sẽ không thể nghe thấy âm thanh đó trong khi video đang được ghi). - So sánh đầu ra hình ảnh của các thiết lập đồ họa, shader hoặc kỹ thuật kết xuất trong một cảnh animation.

Với các tính năng animation của Godot như node AnimationPlayer, Tweener, particle và shader, Godot có thể được sử dụng hiệu quả để tạo mọi loại animation 2D và 3D (cũng như hình ảnh tĩnh).

Nếu đã quen với workflow của Godot, bạn có thể làm việc hiệu quả hơn khi sử dụng Godot để kết xuất video thay vì Blender. Tuy vậy, các renderer được thiết kế cho việc sử dụng không theo thời gian thực như Cycles và Eevee có thể tạo ra hình ảnh đẹp hơn (đổi lại thời gian kết xuất lâu hơn).

So với việc ghi video theo thời gian thực, một số ưu điểm của ghi không theo thời gian thực gồm:

- Sử dụng bất kỳ thiết lập đồ họa nào (bao gồm cả các thiết lập cực kỳ nặng) bất kể khả năng của phần cứng. Video đầu ra sẽ *luôn* có nhịp khung hình hoàn hảo; không bao giờ xuất hiện hiện tượng rớt khung hình hoặc giật hình. Phần cứng nhanh hơn sẽ cho phép bạn kết xuất một animation nhất định trong thời gian ngắn hơn, nhưng đầu ra hình ảnh vẫn giống hệt nhau. - Kết xuất ở độ phân giải cao hơn độ phân giải màn hình mà không cần dựa vào các công cụ riêng của driver như Dynamic Super Resolution của NVIDIA hoặc Virtual Super Resolution của AMD. - Kết xuất ở framerate cao hơn framerate mục tiêu của video, sau đó
  :ref:`post-process to generate high-quality motion blur <doc_creating_movies_motion_blur>`.
  Điều này cũng giúp các hiệu ứng hội tụ qua nhiều khung hình (chẳng hạn như temporal antialiasing, SDFGI và volumetric fog) trông đẹp hơn.

.. warning::

    **Tính năng này không được thiết kế để ghi lại footage theo thời gian thực trong khi chơi game.**

    Người chơi nên sử dụng các công cụ như `OBS Studio <https://obsproject.com/>`__ hoặc `SimpleScreenRecorder <https://www.maartenbaert.be/simplescreenrecorder/>`__ để ghi video gameplay, vì chúng làm tốt hơn nhiều việc chặn compositor so với khả năng của Godot khi sử dụng Vulkan hoặc OpenGL nguyên bản.

    Tuy vậy, nếu game của bạn chạy ở tốc độ gần thời gian thực khi ghi, bạn vẫn có thể sử dụng tính năng này (nhưng sẽ không có phát âm thanh để nghe, vì âm thanh được lưu trực tiếp vào tệp video).

Bật chế độ Movie Maker
----------------------

Để bật chế độ Movie Maker, hãy nhấp vào nút "movie reel" ở góc trên bên phải của editor *trước khi* chạy project:

.. figure:: img/creating_movies_enable_movie_maker_mode.webp
   :align: center
   :alt: Movie Maker mode is disabled, click the "movie reel" icon to enable

   Movie Maker mode is disabled, click the "movie reel" icon to enable

Một menu sẽ hiển thị các tùy chọn để bật chế độ Movie Maker và đi đến phần cài đặt. Khi chế độ Movie Maker được bật, biểu tượng sẽ có nền trùng với màu nhấn:

.. figure:: img/creating_movies_disable_movie_maker_mode.webp
   :align: center
   :alt: Movie Maker mode is enabled, click the "movie reel" icon again to disable

   Movie Maker mode is enabled, click the "movie reel" icon again to disable

Trạng thái Movie Maker **không** được lưu lại khi editor thoát, vì vậy nếu cần, bạn phải bật lại chế độ Movie Maker sau khi khởi động lại editor.

.. note::

    Việc bật hoặc tắt chế độ Movie Maker trong khi project đang chạy sẽ không có hiệu lực cho đến khi project được khởi động lại.

Trước khi có thể ghi video bằng cách chạy project, bạn vẫn cần cấu hình đường dẫn tệp đầu ra. Có thể thiết lập đường dẫn này cho tất cả các scene trong Project Settings:

.. figure:: img/creating_movies_project_settings.webp
   :align: center
   :alt: Movie Maker project settings (with Advanced toggle enabled)

   Movie Maker project settings (with Advanced toggle enabled)

Ngoài ra, bạn có thể thiết lập đường dẫn tệp đầu ra cho từng scene bằng cách thêm metadata kiểu String có tên ``movie_file`` vào **root node** của scene. Tùy chọn này chỉ được sử dụng khi scene chính được đặt thành scene tương ứng, hoặc khi chạy trực tiếp scene bằng cách nhấn :kbd:`F6` (:kbd:`Cmd + R` trên macOS).

.. figure:: img/creating_movies_set_per_scene_metadata.webp
   :align: center
   :alt: Inspector view after creating a ``movie_file`` metadata of type String

   Inspector view after creating a ``movie_file`` metadata of type String

Đường dẫn được chỉ định trong project settings hoặc metadata có thể là đường dẫn tuyệt đối hoặc đường dẫn tương đối so với project root.

Sau khi đã cấu hình và bật chế độ Movie Maker, chế độ này sẽ tự động được sử dụng khi chạy project từ editor.

Sử dụng dòng lệnh
~~~~~~~~~~~~~~~~~

Movie Maker cũng có thể được bật từ :ref:`command line <doc_command_line_tutorial>`:

::

    godot --path /path/to/your_project --write-movie output.avi

Nếu đường dẫn đầu ra là đường dẫn tương đối, thì nó **tương đối so với thư mục project**, không phải thư mục làm việc hiện tại. Trong ví dụ trên, tệp sẽ được ghi vào ``/path/to/your_project/output.avi``. Hành vi này tương tự đối số dòng lệnh ``--export-release``.

Vì độ phân giải đầu ra của Movie Maker được thiết lập bởi kích thước viewport, bạn có thể điều chỉnh kích thước cửa sổ khi khởi động để ghi đè giá trị này nếu project sử dụng ``disabled`` hoặc ``canvas_items`` :ref:`stretch mode <doc_multiple_resolutions>`:

::

    godot --path /path/to/your_project --write-movie output.avi --resolution 1280x720

Lưu ý rằng kích thước cửa sổ bị giới hạn bởi độ phân giải của màn hình. Xem
:ref:`doc_creating_movies_recording_at_higher_resolution` if you need to record
video ở độ phân giải cao hơn độ phân giải màn hình.

FPS ghi cũng có thể được ghi đè trên dòng lệnh mà không cần chỉnh sửa Project Settings:

::

    godot --path /path/to/your_project --write-movie output.avi --fixed-fps 30

.. note::

    Cả hai đối số dòng lệnh ``--write-movie`` và ``--fixed-fps`` đều khả dụng trong các project đã export. Không thể bật hoặc tắt chế độ Movie Maker khi project đang chạy, nhưng bạn có thể sử dụng phương thức :ref:`OS.execute() <class_OS_method_execute>` để chạy một instance thứ hai của project đã export nhằm ghi một tệp video.

Chọn định dạng đầu ra
---------------------

Các định dạng đầu ra được cung cấp bởi class :ref:`MovieWriter <class_MovieWriter>`. Godot có 3 :ref:`MovieWriters <class_MovieWriter>` tích hợp sẵn, và có thể triển khai thêm bằng extension:

OGV (khuyến nghị)
~~~~~~~~~~~~~~~~~

Container OGV với Theora cho video và Vorbis cho âm thanh. Có tính năng nén video và âm thanh có mất dữ liệu, với sự cân bằng tốt giữa kích thước tệp và tốc độ encoding, đồng thời cho chất lượng hình ảnh tốt hơn MJPEG. Có 4 mức tốc độ, có thể điều chỉnh bằng cách thay đổi **Editor > Movie Writer > Encoding Speed**, trong đó mức nhanh nhất có tốc độ gần tương đương AVI nhưng nén tốt hơn. Ở các mức tốc độ thấp hơn, có thể nén tốt hơn nữa mà vẫn giữ nguyên chất lượng hình ảnh. Có thể điều chỉnh chất lượng nén có mất dữ liệu bằng cách thay đổi **Editor > Movie Writer > Video Quality** cho video và **Editor > Movie Writer > Audio Quality** cho âm thanh.

Có thể điều chỉnh Keyframe Interval bằng cách thay đổi **Editor > Movie Writer > Keyframe Interval**. Trong một số trường hợp, việc tăng thiết lập này có thể cải thiện hiệu quả nén mà không gây bất lợi.

Tệp kết quả có thể được xem trong Godot bằng :ref:`VideoStreamPlayer <class_VideoStreamPlayer>` và hầu hết các trình phát video, nhưng không thể xem bằng trình duyệt web. OGV không hỗ trợ transparency.

Để sử dụng OGV, hãy chỉ định đường dẫn đến tệp ``.ogv`` sẽ được tạo trong project setting **Editor > Movie Writer > Movie File**.

.. note::

   OGV chỉ có thể được ghi trong các bản build editor. Ngược lại, :ref:`OGV playback <doc_playing_videos>` có thể được thực hiện trong cả các bản build editor và export template.

AVI
~~~

Container AVI với MJPEG cho video và âm thanh không nén. Có tính năng nén video có mất dữ liệu, tạo ra kích thước tệp trung bình và tốc độ encoding nhanh. Có thể điều chỉnh chất lượng nén có mất dữ liệu bằng cách thay đổi **Editor > Movie Writer > Video Quality**.

Tệp kết quả có thể được xem trong hầu hết các trình phát video, nhưng phải được chuyển đổi sang định dạng khác để xem trên web hoặc xem bằng Godot với node VideoStreamPlayer. MJPEG không hỗ trợ transparency. Đầu ra AVI hiện bị giới hạn ở tệp có kích thước tối đa 4 GB.

Để sử dụng AVI, hãy chỉ định đường dẫn đến tệp ``.avi`` sẽ được tạo trong project setting **Editor > Movie Writer > Movie File**.

PNG
~~~

Chuỗi hình ảnh PNG cho video và WAV cho âm thanh. Có tính năng nén video không mất dữ liệu, đổi lại là kích thước tệp lớn và tốc độ encoding chậm. Tùy chọn này được thiết kế để
:ref:`encoded to a video file with an external tool after recording <doc_creating_movies_converting_avi>`.

Transparency được hỗ trợ, nhưng viewport gốc **phải** có thuộc tính ``transparent_bg`` được đặt thành ``true`` để transparency hiển thị trong hình ảnh đầu ra. Có thể thực hiện việc này bằng cách bật project setting nâng cao **Rendering > Transparent Background**. Có thể tùy chọn bật **Display > Window > Size > Transparent** và **Display > Window > Per Pixel Transparency > Enabled** để xem trước transparency trong khi ghi video, nhưng không cần bật các tùy chọn này để hình ảnh đầu ra có transparency.

Để sử dụng PNG, hãy chỉ định tệp ``.png`` sẽ được tạo trong project setting **Editor > Movie Writer > Movie File**. Tệp ``.wav`` được tạo sẽ có cùng tên với tệp ``.png`` (bỏ phần mở rộng).

Tùy chỉnh
~~~~~~~~~

Nếu cần encoding trực tiếp sang một định dạng khác hoặc pipe một stream qua phần mềm bên thứ ba, bạn có thể mở rộng class MovieWriter để tạo movie writer của riêng mình. Thông thường nên thực hiện việc này bằng GDExtension vì lý do hiệu năng.

Cấu hình
--------

Trong phần **Editor > Movie Writer** của Project Settings, có một số tùy chọn bạn có thể cấu hình. Một số tùy chọn chỉ hiển thị sau khi bật toggle **Advanced** ở góc trên bên phải của hộp thoại Project Settings.

- **Tần số mix Hz:** Tần số mix âm thanh được sử dụng trong âm thanh đã ghi khi ghi movie. Giá trị này có thể khác với tần số mix của project, nhưng phải chia hết cho FPS đã ghi để tránh âm thanh bị mất đồng bộ theo thời gian. - **Chế độ loa:** Chế độ loa được sử dụng trong âm thanh đã ghi khi ghi movie (stereo, surround 5.1 hoặc surround 7.1). - **Chất lượng video:** Chất lượng hình ảnh được sử dụng khi ghi video vào tệp OGV hoặc AVI, trong khoảng từ ``0.01`` đến ``1.0`` (bao gồm cả hai giá trị). Giá trị chất lượng cao hơn tạo ra đầu ra đẹp hơn nhưng tệp có dung lượng lớn hơn. Giá trị chất lượng được khuyến nghị nằm trong khoảng từ ``0.75`` đến ``0.9``. Ngay cả ở chất lượng ``1.0``, quá trình nén vẫn là nén mất dữ liệu. Thiết lập này không ảnh hưởng đến chất lượng âm thanh và bị bỏ qua khi ghi vào chuỗi hình ảnh PNG. - **Tệp movie:** Đường dẫn đầu ra của movie. Đường dẫn này có thể là đường dẫn tuyệt đối hoặc tương đối so với thư mục gốc của project. - **Tắt V-Sync:** Nếu bật, yêu cầu tắt V-Sync khi ghi movie. Điều này có thể tăng tốc độ ghi video nếu phần cứng đủ nhanh để render, encode và lưu video ở framerate cao hơn tần số quét của màn hình. Thiết lập này không có tác dụng nếu hệ điều hành hoặc graphics driver bắt buộc sử dụng V-Sync mà không cho phép ứng dụng tắt tính năng này. - **FPS:** Số khung hình mỗi giây được render trong movie đầu ra. Giá trị cao hơn tạo ra animation mượt hơn nhưng thời gian render lâu hơn và tệp đầu ra lớn hơn. Hầu hết các nền tảng lưu trữ video không hỗ trợ giá trị FPS cao hơn 60, nhưng bạn có thể sử dụng giá trị cao hơn để tạo motion blur. - **Chất lượng âm thanh:** Chất lượng âm thanh được sử dụng khi ghi video vào tệp OGV, trong khoảng từ ``-0.1`` đến ``1.0`` (bao gồm cả hai giá trị). Giá trị chất lượng cao hơn tạo ra âm thanh chất lượng tốt hơn nhưng tệp có dung lượng lớn hơn một chút. Giá trị chất lượng được khuyến nghị nằm trong khoảng từ ``0.3`` đến ``0.5``. Ngay cả ở chất lượng ``1.0``, quá trình nén vẫn là nén mất dữ liệu. - **Tốc độ encoding:** Mức tốc độ được sử dụng khi ghi video vào tệp OGV. Các mức tốc độ nhanh hơn có hiệu quả nén thấp hơn. Chất lượng hình ảnh hầu như không thay đổi. - **Khoảng cách keyframe:** Còn được gọi là GOP (Group Of Pictures), đây là số lượng inter-frame tối đa được sử dụng khi ghi vào tệp OGV. Giá trị cao hơn có thể cải thiện hiệu quả nén mà không làm giảm chất lượng, nhưng khiến việc seek video chậm hơn.

.. note::

    Khi sử dụng ``disabled`` hoặc ``2d`` :ref:`stretch modes <doc_multiple_resolutions>`, độ phân giải của tệp đầu ra được đặt theo kích thước cửa sổ. Hãy đảm bảo thay đổi kích thước cửa sổ *trước khi* splash screen kết thúc. Để thực hiện việc này, bạn nên điều chỉnh các thiết lập project nâng cao **Display > Window > Size > Window Width Override** và **Window Height Override**.

    Xem thêm :ref:`doc_creating_movies_recording_at_higher_resolution`.

Thoát chế độ Movie Maker
------------------------

Để thoát an toàn khỏi một project đang sử dụng chế độ Movie Maker, hãy sử dụng nút X ở phía trên cửa sổ hoặc gọi ``get_tree().quit()`` trong script. Bạn cũng có thể sử dụng đối số dòng lệnh ``--quit-after N``, trong đó ``N`` là số frame cần render trước khi thoát.

Nhấn :kbd:`F8` (:kbd:`Cmd + .` trên macOS) hoặc nhấn :kbd:`Ctrl + C` trên terminal đang chạy Godot **không được khuyến nghị**, vì thao tác này sẽ tạo ra tệp AVI có định dạng không đúng và không có thông tin thời lượng. Đối với chuỗi hình ảnh PNG, các hình ảnh PNG sẽ không bị ảnh hưởng, nhưng tệp WAV đi kèm vẫn thiếu thông tin thời lượng. Các tệp OGV có thể có track video và âm thanh với thời lượng hơi khác nhau nhưng vẫn hợp lệ.

Một số trình phát video vẫn có thể phát tệp AVI hoặc WAV với video và âm thanh hoạt động bình thường. Tuy nhiên, phần mềm sử dụng tệp AVI hoặc WAV, chẳng hạn như các trình chỉnh sửa video, có thể không mở được tệp.
:ref:`Using a video converter program <doc_creating_movies_converting_avi>`
có thể giúp ích trong những trường hợp đó.

Nếu bạn sử dụng AnimationPlayer để điều khiển một "main action" trong scene (chẳng hạn như chuyển động camera), bạn có thể bật thuộc tính **Movie Quit On Finish** trên node AnimationPlayer tương ứng. Khi được bật, thuộc tính này sẽ khiến Godot tự thoát khi animation phát xong *và* engine đang chạy ở chế độ Movie Maker. Lưu ý rằng *thuộc tính này không có tác dụng với các animation lặp*. Vì vậy, bạn cần đảm bảo animation được đặt ở chế độ không lặp.

Sử dụng thiết lập graphics chất lượng cao
-----------------------------------------

``movie`` :ref:`feature tag <doc_feature_tags>` có thể được sử dụng để override các thiết lập project cụ thể. Điều này hữu ích khi bật các thiết lập graphics chất lượng cao vốn không đủ nhanh để chạy theo thời gian thực trên phần cứng của bạn. Hãy nhớ rằng việc đặt mọi thiết lập ở giá trị tối đa vẫn có thể làm chậm tốc độ lưu movie, đặc biệt khi ghi ở độ phân giải cao hơn. Vì vậy, bạn vẫn chỉ nên tăng các thiết lập graphics nếu chúng tạo ra sự khác biệt đáng kể trong hình ảnh đầu ra.

Feature tag này cũng có thể được truy vấn trong script để tăng các thiết lập chất lượng được đặt trong resource Environment. Ví dụ, để cải thiện thêm chi tiết SDFGI và giảm hiện tượng light leaking:

.. tabs::
 .. code-tab:: gdscript

    extends Node3D

    func _ready():
        if OS.has_feature("movie"):
            # Khi ghi movie, tăng mật độ cell SDFGI
            # mà không giảm khoảng cách tối đa của nó.
            get_viewport().world_3d.environment.sdfgi_min_cell_size *= 0.25
            get_viewport().world_3d.environment.sdfgi_cascades = 8

 .. code-tab:: csharp

    using Godot;

    public partial class MyNode3D : Node3D
    {
        public override void _Ready()
        {
            if (OS.HasFeature("movie"))
            {
                // Khi ghi movie, tăng mật độ cell SDFGI
                // mà không giảm khoảng cách tối đa của nó.
                GetViewport().World3D.Environment.SdfgiMinCellSize *= 0.25f;
                GetViewport().World3D.Environment.SdfgiCascades = 8;
            }
        }
    }

.. _doc_creating_movies_recording_at_higher_resolution:

Render ở độ phân giải cao hơn độ phân giải màn hình
---------------------------------------------------

Chất lượng render tổng thể có thể được cải thiện đáng kể bằng cách render ở độ phân giải cao như 4K hoặc 8K.

.. note::

    Đối với 3D rendering, Godot cung cấp thiết lập project nâng cao **Rendering > Scaling 3D > Scale**, có thể đặt cao hơn ``1.0`` để tạo *supersample antialiasing*. Sau đó, 3D rendering sẽ được *downsample* khi được vẽ trên viewport. Điều này cung cấp một hình thức antialiasing chất lượng cao nhưng tốn tài nguyên, mà không làm tăng độ phân giải đầu ra cuối cùng.

    Hãy cân nhắc sử dụng thiết lập project này trước, vì nó tránh làm chậm tốc độ ghi movie và tăng dung lượng tệp đầu ra so với việc thực sự tăng độ phân giải đầu ra.

Nếu bạn muốn render 2D ở độ phân giải cao hơn hoặc thực sự cần đầu ra pixel thô cao hơn cho 3D rendering, bạn có thể tăng độ phân giải vượt quá mức màn hình cho phép.

Theo mặc định, Godot sử dụng ``disabled`` :ref:`stretch modes <doc_multiple_resolutions>` trong các project. Nếu sử dụng chế độ stretch ``disabled`` hoặc ``canvas_items``, kích thước cửa sổ sẽ quyết định độ phân giải video đầu ra.

Mặt khác, nếu project được cấu hình sử dụng chế độ stretch ``viewport``, độ phân giải viewport sẽ quyết định độ phân giải video đầu ra. Độ phân giải viewport được thiết lập bằng các thiết lập project **Display > Window > Size > Viewport Width** và **Viewport Height**. Bạn có thể sử dụng cách này để render video ở độ phân giải cao hơn độ phân giải màn hình.

Để làm cửa sổ nhỏ hơn trong quá trình ghi mà không ảnh hưởng đến độ phân giải video đầu ra, bạn có thể đặt các thiết lập project nâng cao **Display > Window > Size > Window Width Override** và **Window Height Override** thành các giá trị lớn hơn ``0``.

Để chỉ áp dụng override độ phân giải khi ghi movie, bạn có thể override các thiết lập đó bằng ``movie`` :ref:`feature tag <doc_feature_tags>`.

Các bước hậu kỳ
---------------

Một số bước hậu kỳ phổ biến được liệt kê bên dưới.

.. note::

    Khi sử dụng nhiều bước hậu kỳ, hãy cố gắng thực hiện tất cả trong một lệnh FFmpeg duy nhất. Điều này sẽ tiết kiệm thời gian encoding và cải thiện chất lượng bằng cách tránh nhiều bước encoding mất dữ liệu.

.. _doc_creating_movies_converting_avi:

Chuyển đổi video OGV/AVI sang MP4
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù một số nền tảng như YouTube hỗ trợ tải trực tiếp tệp AVI lên, nhiều nền tảng khác sẽ yêu cầu thực hiện bước chuyển đổi trước. `HandBrake <https://handbrake.fr/>`__ (GUI) và `FFmpeg <https://ffmpeg.org/>`__ (CLI) là các công cụ mã nguồn mở phổ biến cho mục đích này. FFmpeg có đường cong học tập dốc hơn, nhưng mạnh mẽ hơn.

Lệnh bên dưới chuyển đổi video OGV/AVI thành video MP4 (H.264) với Constant Rate Factor (CRF) là 15. Kết quả là một tệp tương đối lớn, nhưng rất phù hợp với các nền tảng sẽ re-encode video của bạn để giảm dung lượng (chẳng hạn như hầu hết các website chia sẻ video):

::

    ffmpeg -i input.avi -crf 15 output.mp4

Để có tệp nhỏ hơn với sự đánh đổi về chất lượng, hãy *tăng* giá trị CRF trong lệnh trên.

Để có tệp với tỷ lệ dung lượng/chất lượng tốt hơn (đánh đổi bằng thời gian encoding lâu hơn), hãy thêm ``-preset veryslow`` trước ``-crf 15`` trong lệnh trên. Ngược lại, có thể sử dụng ``-preset veryfast`` để encoding nhanh hơn nhưng tỷ lệ dung lượng/chất lượng kém hơn.

.. _doc_creating_movies_converting_image_sequence:

Chuyển đổi chuỗi hình ảnh PNG + âm thanh WAV thành video
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn chọn ghi một chuỗi hình ảnh PNG cùng với tệp WAV bên cạnh, bạn cần chuyển đổi chúng thành video trước khi có thể sử dụng ở nơi khác.

Tên tệp của chuỗi hình ảnh PNG do Godot tạo luôn chứa 8 chữ số, bắt đầu từ 0 với các số được thêm số 0 ở đầu. Nếu bạn chỉ định đường dẫn đầu ra ``folder/example.png``, Godot sẽ ghi ``folder/example00000000.png``, ``folder/example00000001.png``, v.v. vào thư mục đó. Âm thanh sẽ được lưu tại ``folder/example.wav``.

FPS được chỉ định bằng đối số ``-r``. Giá trị này phải khớp với FPS được chỉ định trong quá trình ghi. Nếu không, video sẽ có vẻ bị làm chậm hoặc tăng tốc, và âm thanh sẽ không đồng bộ với video.

::

    ffmpeg -r 60 -i input%08d.png -i input.wav -crf 15 output.mp4

Nếu bạn đã ghi một chuỗi hình ảnh PNG với tính năng trong suốt được bật, bạn cần sử dụng định dạng video hỗ trợ lưu độ trong suốt. MP4/H.264 không hỗ trợ lưu độ trong suốt, vì vậy bạn có thể sử dụng WebM/VP9 thay thế:

::

    ffmpeg -r 60 -i input%08d.png -i input.wav -c:v libvpx-vp9 -crf 15 -pix_fmt yuva420p output.webm

.. _doc_creating_movies_motion_blur:

Cắt video
~~~~~~~~~

Bạn có thể cắt bỏ những phần video không muốn giữ lại sau khi đã ghi video. Ví dụ, để loại bỏ mọi thứ trước giây thứ 12.1 và chỉ giữ lại 5.2 giây video sau thời điểm đó:

::

    ffmpeg -i input.avi -ss 00:00:12.10 -t 00:00:05.20 -crf 15 output.mp4

Bạn cũng có thể cắt video bằng công cụ GUI `LosslessCut <https://losslesscut.app/>`__.

Thay đổi kích thước video
~~~~~~~~~~~~~~~~~~~~~~~~~

Lệnh sau thay đổi kích thước video để có chiều cao 1080 pixel (1080p), đồng thời giữ nguyên tỷ lệ khung hình hiện có:

::

    ffmpeg -i input.avi -vf "scale=-1:1080" -crf 15 output.mp4


.. _doc_creating_movies_reducing_framerate:

Giảm framerate
~~~~~~~~~~~~~~

Lệnh sau thay đổi framerate của video thành 30 FPS, loại bỏ một số frame ban đầu nếu video đầu vào có nhiều frame hơn:

::

    ffmpeg -i input.avi -r 30 -crf 15 output.mp4

Tạo motion blur tích lũy bằng FFmpeg
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot không có hỗ trợ tích hợp cho motion blur, nhưng bạn vẫn có thể tạo hiệu ứng này trong các video đã ghi.

Nếu ghi video ở bội số của framerate ban đầu, bạn có thể trộn các frame lại với nhau rồi giảm framerate để tạo video có *motion blur tích lũy*. Hiệu ứng motion blur này có thể trông rất đẹp, nhưng sẽ mất nhiều thời gian để tạo vì bạn phải render nhiều frame hơn mỗi giây (ngoài thời gian xử lý hậu kỳ).

Ví dụ với video nguồn 240 FPS, tạo motion blur 4× và giảm framerate đầu ra xuống 60 FPS:

::

    ffmpeg -i input.avi -vf "tmix=frames=4, fps=60" -crf 15 output.mp4

Điều này cũng giúp các hiệu ứng hội tụ qua nhiều frame (chẳng hạn như temporal antialiasing, SDFGI và volumetric fog) hội tụ nhanh hơn và do đó trông đẹp hơn, vì chúng có thể làm việc với nhiều dữ liệu hơn tại một thời điểm nhất định. Xem :ref:`doc_creating_movies_reducing_framerate` nếu bạn muốn có lợi ích này mà không thêm motion blur.
