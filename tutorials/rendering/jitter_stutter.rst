.. _doc_jitter_stutter:

Khắc phục jitter, stutter và input lag
======================================

Jitter, stutter và input lag là gì?
-----------------------------------

*Jitter* và *stutter* là hai dạng biến đổi khác nhau của chuyển động hiển thị của các đối tượng trên màn hình, có thể ảnh hưởng đến game ngay cả khi game đang chạy ở tốc độ tối đa. Những hiệu ứng này dễ thấy nhất trong các game có thế giới di chuyển với tốc độ không đổi theo một hướng cố định, chẳng hạn như game endless runner hoặc platformer.

*Input lag* không liên quan đến jitter và stutter, nhưng đôi khi được thảo luận cùng nhau. Input lag là độ trễ hiển thị trên màn hình khi thực hiện thao tác bằng chuột, bàn phím, controller hoặc màn hình cảm ứng. Nguyên nhân có thể liên quan đến code của game, code của engine hoặc các yếu tố bên ngoài (chẳng hạn như phần cứng). Input lag dễ nhận thấy nhất trong các game sử dụng chuột để ngắm, chẳng hạn như game góc nhìn thứ nhất. Không thể loại bỏ hoàn toàn input lag, nhưng có thể giảm hiện tượng này bằng một số cách.

Phân biệt jitter và stutter
---------------------------

Một game chạy ở framerate bình thường mà không xuất hiện hiệu ứng nào sẽ trông mượt mà:

.. image:: img/motion_normal.gif

Một game xuất hiện *jitter* sẽ rung liên tục theo một cách rất nhẹ:

.. image:: img/motion_jitter.gif

Cuối cùng, một game xuất hiện *stutter* sẽ trông mượt mà, nhưng cứ sau vài giây lại có vẻ *dừng lại* hoặc *lùi lại một frame*:

.. image:: img/motion_stutter.gif

Jitter
------

Jitter có thể do nhiều nguyên nhân. Nguyên nhân điển hình nhất xảy ra khi *tần số physics* của game (thường là 60 Hz) chạy ở độ phân giải khác với refresh rate của màn hình. Hãy kiểm tra xem refresh rate của màn hình có khác 60 Hz hay không.

Đôi khi, chỉ một số đối tượng xuất hiện jitter (nhân vật hoặc background). Điều này xảy ra khi chúng được xử lý theo các nguồn thời gian khác nhau (một đối tượng được xử lý trong physics step, còn đối tượng kia được xử lý trong idle step).

Có thể giảm nguyên nhân gây jitter này bằng cách bật
:ref:`physics interpolation <doc_physics_interpolation_quick_start_guide>`
trong Project Settings. Physics interpolation sẽ làm mượt các bản cập nhật physics bằng cách nội suy các transform của các đối tượng physics giữa các physics frame. Nhờ đó, biểu diễn trực quan của các đối tượng physics sẽ luôn trông mượt mà, bất kể framerate và physics tick rate.

Việc bật physics interpolation có một số điểm cần lưu ý. Ví dụ, cần cẩn thận khi teleport các đối tượng để chúng không bị nội suy hiển thị giữa vị trí cũ và vị trí mới khi điều đó không được mong muốn. Xem
:ref:`doc_physics_interpolation` documentation for details.

.. note::

    Việc bật physics interpolation sẽ làm tăng input lag đối với các hành vi phụ thuộc vào physics tick, chẳng hạn như chuyển động của người chơi. Trong hầu hết các game, điều này thường được ưu tiên hơn jitter, nhưng hãy cân nhắc kỹ đối với các game hoạt động ở framerate cố định (chẳng hạn như game đối kháng hoặc game nhịp điệu). Có thể bù cho mức tăng input lag này bằng cách tăng physics tick rate như mô tả trong phần :ref:`doc_jitter_stutter_input_lag`.

Stutter
-------

Stutter có thể xảy ra vì nhiều lý do khác nhau. Một nguyên nhân là game không thể duy trì hiệu năng framerate tối đa do bottleneck CPU hoặc GPU. Cách khắc phục phụ thuộc vào từng game và sẽ yêu cầu
:ref:`optimization <doc_general_optimization>`.

Một nguyên nhân phổ biến khác gây stutter là *shader compilation stutter*. Hiện tượng này xảy ra khi một shader cần được compile vào lần đầu tiên một material hoặc particle effect mới được spawn trong game. Loại stutter này thường chỉ xảy ra trong lần chơi đầu tiên hoặc sau khi cập nhật graphics driver, khi shader cache bị invalidated.

Kể từ Godot 4.4, khi sử dụng Forward+ hoặc Mobile renderer, engine cố gắng tránh shader compilation stutter bằng cách tiếp cận ubershader. Để cách tiếp cận này đạt hiệu quả cao nhất, cần cẩn thận khi thiết kế scene và resource để Godot có thể thu thập nhiều thông tin nhất có thể khi scene/resource được load, thay vì khi chúng được draw lần đầu tiên. Xem :ref:`doc_pipeline_compilations` để biết thêm thông tin.

Tuy nhiên, khi sử dụng Compatibility renderer, không thể dùng cách tiếp cận ubershader này do các giới hạn kỹ thuật trong OpenGL. Vì vậy, để tránh shader compilation stutter trong Compatibility renderer, bạn cần spawn mọi mesh và visual effect trước camera trong một frame duy nhất khi level đang load. Điều này sẽ đảm bảo shader được compile khi level được load, thay vì xảy ra trong lúc chơi game. Có thể thực hiện việc này phía sau UI 2D cố định (chẳng hạn như một
:ref:`class_ColorRect` node) so that it's not visible to the player.

.. note::

    Trên các platform hỗ trợ tắt V-Sync, có thể làm cho stutter khó nhận thấy hơn bằng cách tắt V-Sync trong project settings. Tuy nhiên, việc này sẽ gây ra hiện tượng tearing, đặc biệt trên các màn hình có refresh rate thấp. Nếu màn hình hỗ trợ, hãy cân nhắc bật variable refresh rate (G-Sync/FreeSync) trong khi vẫn để V-Sync bật. Điều này giúp giảm một số dạng stutter mà không gây ra tearing. Tuy nhiên, cách này không giúp ích khi stutter lớn, chẳng hạn như stutter do shader compilation stutter gây ra.

    Buộc card đồ họa sử dụng profile hiệu năng tối đa cũng có thể giúp giảm stutter, nhưng sẽ làm tăng mức tiêu thụ điện của GPU.

Ngoài ra, stutter có thể do hệ điều hành bên dưới gây ra. Dưới đây là một số thông tin về stutter trên các OS khác nhau:

Windows
~~~~~~~

Windows được biết đến là nguyên nhân gây stutter trong các game chạy ở chế độ cửa sổ. Điều này chủ yếu phụ thuộc vào phần cứng được cài đặt, phiên bản driver và các process chạy song song (ví dụ: mở nhiều tab trình duyệt có thể gây stutter trong một game đang chạy). Để tránh điều này, Godot tăng priority của game lên "Above Normal". Cách này giúp cải thiện đáng kể, nhưng có thể không loại bỏ hoàn toàn stutter.

Để loại bỏ hoàn toàn hiện tượng này, cần cấp cho game đầy đủ đặc quyền để trở thành "Time Critical", nhưng không được khuyến nghị. Một số game có thể làm như vậy, nhưng bạn nên học cách chấp nhận vấn đề này, vì đây là hiện tượng phổ biến ở các game Windows và hầu hết người dùng sẽ không chơi game ở chế độ cửa sổ (các game được chơi trong cửa sổ, chẳng hạn như game giải đố, thường sẽ không gặp vấn đề này).

Khi chạy toàn màn hình, Windows cấp priority đặc biệt cho game, vì vậy stutter không còn hiển thị và rất hiếm khi xảy ra. Đây là cách hầu hết các game được chơi.

Khi sử dụng chuột có polling rate từ 1.000 Hz trở lên, hãy cân nhắc sử dụng bản cài đặt Windows 11 hoàn toàn mới nhất, đi kèm các bản sửa lỗi liên quan đến mức sử dụng CPU cao với chuột có polling rate cao. Những bản sửa lỗi này không có trong Windows 10 và các phiên bản cũ hơn.

.. tip::

    Các game nên sử dụng chế độ cửa sổ **Exclusive Fullscreen**, thay vì **Fullscreen**, vốn được thiết kế để ngăn Windows tự động xử lý cửa sổ như thể đó là exclusive fullscreen.

    **Fullscreen** được dùng cho các ứng dụng GUI muốn sử dụng transparency theo từng pixel mà không có nguy cơ bị OS tắt. Chế độ này đạt được điều đó bằng cách chừa lại một đường 1 pixel ở phía dưới màn hình. Ngược lại, **Exclusive Fullscreen** sử dụng kích thước màn hình thực tế và cho phép Windows giảm jitter và input lag cho các game fullscreen.

Linux
~~~~~

Stutter có thể xuất hiện trên Linux desktop, nhưng nguyên nhân thường liên quan đến các video driver và compositor khác nhau. Một số compositor cũng có thể kích hoạt vấn đề này (ví dụ: KWin), vì vậy bạn nên thử sử dụng một compositor khác để loại trừ nó là nguyên nhân. Một số window manager như KWin và Xfwm cho phép bạn tắt compositing thủ công, việc này có thể cải thiện hiệu năng (đổi lại sẽ gây tearing).

Không có cách khắc phục tạm thời nào cho stutter do driver hoặc compositor, ngoài việc báo cáo vấn đề cho các developer của driver hoặc compositor. Stutter có thể xuất hiện nhiều hơn khi chơi ở chế độ cửa sổ thay vì fullscreen, ngay cả khi đã tắt compositing.

Có thể sử dụng `Feral GameMode <https://github.com/FeralInteractive/gamemode>`__ để tự động áp dụng các tối ưu hóa (chẳng hạn như buộc profile hiệu năng của GPU) khi chạy các process cụ thể.

macOS
~~~~~

Nhìn chung, macOS không bị stutter, mặc dù gần đây đã có một số bug được báo cáo khi chạy ở chế độ fullscreen (đây là bug của macOS). Nếu bạn có một máy gặp hiện tượng này, hãy cho chúng tôi biết.

Android
~~~~~~~

Nhìn chung, Android không bị stutter và jitter vì activity đang chạy được cấp toàn bộ priority. Tuy vậy, có thể có những thiết bị gặp vấn đề (Kindle Fire đời cũ được biết là một trong số đó). Nếu bạn gặp vấn đề này trên Android, hãy cho chúng tôi biết.

iOS
~~~

Các thiết bị iOS nhìn chung không bị stutter, nhưng những thiết bị cũ chạy các phiên bản mới hơn của hệ điều hành có thể gặp vấn đề. Điều này nhìn chung không thể tránh được.

.. _doc_jitter_stutter_input_lag:

Input lag
---------

Cấu hình project
~~~~~~~~~~~~~~~~

Trên các platform hỗ trợ tắt V-Sync, có thể làm cho input lag khó nhận thấy hơn bằng cách tắt V-Sync trong project settings. Tuy nhiên, việc này sẽ gây ra hiện tượng tearing, đặc biệt trên các màn hình có refresh rate thấp. Bạn nên cung cấp V-Sync dưới dạng một tùy chọn để người chơi bật hoặc tắt.

Khi sử dụng phương pháp render Forward+ hoặc Mobile, một cách khác để giảm độ trễ hình ảnh khi V-Sync được bật là sử dụng V-Sync với double buffering thay vì V-Sync với triple buffering mặc định. Kể từ Godot 4.3, bạn có thể thực hiện việc này bằng cách giảm thiết lập project **Display > Window > V-Sync > Swapchain Image Count** xuống ``2``. Nhược điểm của double buffering là framerate sẽ kém ổn định hơn nếu không thể đạt tần số quét của màn hình do CPU hoặc GPU bị nghẽn. Chẳng hạn, trên màn hình 60 Hz, nếu framerate thường giảm xuống 55 FPS trong lúc chơi với triple buffering, thì với double buffering, framerate sẽ phải tạm thời giảm xuống 30 FPS (sau đó trở lại 60 FPS khi có thể). Do đó, V-Sync với double buffering chỉ được khuyến nghị nếu bạn có thể *liên tục* đạt tần số quét của màn hình trên phần cứng mục tiêu.

Tăng số lần lặp physics mỗi giây cũng có thể giảm độ trễ đầu vào do physics gây ra. Điều này đặc biệt dễ nhận thấy khi sử dụng physics interpolation (giúp chuyển động mượt hơn nhưng làm tăng độ trễ). Để thực hiện việc này, hãy đặt **Physics > Common > Physics Ticks Per Second** thành giá trị cao hơn mặc định ``60``, hoặc đặt ``Engine.physics_ticks_per_second`` tại runtime trong một script. Các giá trị là bội số của tần số quét màn hình (thường là ``60``) hoạt động tốt nhất khi physics interpolation bị tắt, vì chúng sẽ tránh được hiện tượng jitter. Điều này có nghĩa là các giá trị như ``120``, ``180`` và ``240`` là những điểm bắt đầu tốt. Ngoài ra, physics FPS cao hơn cũng làm giảm khả năng xảy ra các vấn đề tunneling và bất ổn physics.

Nhược điểm của việc tăng physics FPS là mức sử dụng CPU sẽ tăng, điều này có thể dẫn đến các điểm nghẽn hiệu năng trong những game có mã mô phỏng physics nặng. Bạn có thể giảm thiểu vấn đề này bằng cách chỉ tăng physics FPS trong những tình huống mà độ trễ thấp là yếu tố quan trọng, hoặc cho phép người chơi điều chỉnh physics FPS để phù hợp với phần cứng của họ. Tuy nhiên, physics FPS khác nhau sẽ dẫn đến các kết quả khác nhau trong mô phỏng physics, ngay cả khi ``delta`` được sử dụng nhất quán trong logic game của bạn. Điều này có thể tạo lợi thế cho một số người chơi so với những người khác. Vì vậy, nên tránh cho phép người chơi tự thay đổi physics FPS trong các game multiplayer cạnh tranh.

Cuối cùng, bạn có thể tắt input buffering trên mỗi frame được render bằng cách gọi ``Input.set_use_accumulated_input(false)`` trong một script. Khi đó, các hàm ``_input()`` và ``_unhandled_input()`` trong script của bạn sẽ được gọi trên mỗi input, thay vì tích lũy input và chờ một frame được render. Việc tắt input accumulation sẽ làm tăng mức sử dụng CPU, vì vậy cần thực hiện thận trọng.

.. tip::

    Trong bất kỳ project Godot nào, bạn có thể sử dụng ``--disable-vsync``
    :ref:`command line argument <doc_command_line_tutorial>` to forcibly disable V-Sync.
    Kể từ Godot 4.2, ``--max-fps <fps>`` cũng có thể được dùng để đặt giới hạn FPS (``0`` là không giới hạn). Bạn có thể sử dụng các đối số này cùng lúc.

Đặc thù phần cứng/hệ điều hành
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu màn hình của bạn hỗ trợ, hãy cân nhắc bật variable refresh rate (G-Sync/FreeSync) trong khi vẫn để V-Sync bật, sau đó giới hạn framerate trong phần thiết lập project ở một giá trị thấp hơn một chút so với tần số quét tối đa của màn hình, theo `this page <https://blurbusters.com/howto-low-lag-vsync-on/>`__.

Thoạt đầu điều này có thể trái với trực giác, nhưng việc giới hạn FPS thấp hơn phạm vi tần số quét tối đa đảm bảo rằng hệ điều hành không bao giờ phải chờ quá trình vertical blanking hoàn tất. Điều này tạo ra độ trễ đầu vào *tương tự* như khi tắt V-Sync với cùng giới hạn framerate (thường chỉ cao hơn dưới 1 ms), nhưng không xảy ra hiện tượng tearing.

Công thức được sử dụng để xác định giới hạn framerate là ``refresh - (refresh * refresh / 3600.0)``, trong đó ``refresh`` là tần số quét của màn hình tính bằng Hz. Bảng này cho biết giới hạn framerate nên dùng cho các tần số quét phổ biến (giới hạn được làm tròn xuống số nguyên gần nhất):

+--------------+---------------+
| Refresh rate | Framerate cap |
+==============+===============+
| 60 Hz        | 58 FPS        |
+--------------+---------------+
| 75 Hz        | 73 FPS        |
+--------------+---------------+
| 120 Hz       | 115 FPS       |
+--------------+---------------+
| 144 Hz       | 138 FPS       |
+--------------+---------------+
| 165 Hz       | 157 FPS       |
+--------------+---------------+
| 240 Hz       | 224 FPS       |
+--------------+---------------+
| 360 Hz       | 324 FPS       |
+--------------+---------------+
| 480 Hz       | 416 FPS       |
+--------------+---------------+

Bạn có thể đặt giới hạn framerate này bằng cách thay đổi thiết lập project **Application > Run > Max FPS** hoặc gán ``Engine.max_fps`` tại runtime trong một script. Ở các tần số quét cao hơn, cần dùng giới hạn thấp hơn để đảm bảo các sai số về thời gian không khiến màn hình bật V-Sync (điều này sẽ làm tăng độ trễ đầu vào).

Trên một số nền tảng, bạn cũng có thể bật chế độ low-latency trong tùy chọn của graphics driver (chẳng hạn NVIDIA Control Panel trên Windows). Thiết lập **Ultra** sẽ mang lại độ trễ thấp nhất có thể, đổi lại framerate trung bình sẽ thấp hơn một chút. Buộc GPU sử dụng profile hiệu năng tối đa cũng có thể giảm thêm độ trễ đầu vào, đổi lại mức tiêu thụ điện năng cao hơn (và nhiệt độ/tiếng ồn quạt tăng theo).

Cuối cùng, hãy đảm bảo màn hình của bạn đang chạy ở tần số quét cao nhất có thể trong thiết lập hiển thị của hệ điều hành.

Ngoài ra, hãy đảm bảo mouse của bạn được cấu hình để sử dụng polling rate cao nhất (thường là 1.000 Hz đối với mouse gaming, đôi khi cao hơn). Tuy nhiên, polling rate USB cao có thể dẫn đến mức sử dụng CPU cao, vì vậy 500 Hz có thể là lựa chọn an toàn hơn trên các CPU cấp thấp. Nếu mouse của bạn cung cấp nhiều thiết lập :abbr:`DPI (Dots Per Inch)`, bạn cũng nên cân nhắc `using the highest possible setting and reducing in-game sensitivity to reduce mouse latency <https://www.youtube.com/watch?v=6AoRfv9W110>`__.

Trên Linux khi sử dụng X11, việc tắt compositing trong các window manager cho phép thực hiện điều này (chẳng hạn KWin hoặc Xfwm) có thể giảm đáng kể độ trễ đầu vào.

Báo cáo vấn đề jitter, stutter hoặc độ trễ đầu vào
--------------------------------------------------

Nếu bạn báo cáo vấn đề stutter hoặc jitter (mở issue) không bắt nguồn từ bất kỳ lý do nào nêu trên, hãy nêu thật rõ ràng mọi thông tin có thể về thiết bị, hệ điều hành, phiên bản driver, v.v. Điều này có thể giúp việc khắc phục sự cố hiệu quả hơn.

Nếu bạn báo cáo vấn đề độ trễ đầu vào, hãy đính kèm bản ghi được quay bằng camera tốc độ cao (chẳng hạn chế độ quay slow motion trên điện thoại). Bản ghi **phải** hiển thị cả màn hình và thiết bị đầu vào để có thể đếm số frame giữa một input và kết quả hiển thị trên màn hình. Ngoài ra, hãy nhớ cho biết tần số quét của màn hình và polling rate của thiết bị đầu vào (đặc biệt là mouse).

Ngoài ra, hãy đảm bảo sử dụng đúng thuật ngữ (jitter, stutter, input lag) dựa trên hành vi được thể hiện. Điều này sẽ giúp hiểu vấn đề của bạn nhanh hơn nhiều. Hãy cung cấp một project có thể dùng để tái hiện vấn đề và nếu có thể, hãy đính kèm bản ghi màn hình minh họa lỗi.
