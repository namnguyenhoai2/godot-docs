.. _doc_jitter_stutter:

Khắc phục hiện tượng giật, khựng hình và độ trễ đầu vào
=======================================================

Giật, khựng hình và độ trễ đầu vào là gì?
-----------------------------------------

*Giật* và *khựng hình* là hai dạng biến đổi khác nhau của chuyển động hiển thị của các đối tượng trên màn hình, có thể ảnh hưởng đến trò chơi ngay cả khi trò chơi đang chạy ở tốc độ tối đa. Những hiệu ứng này dễ thấy nhất trong các trò chơi mà thế giới di chuyển với tốc độ không đổi theo một hướng cố định, chẳng hạn như game chạy vô tận hoặc game platformer.

*Độ trễ đầu vào* không liên quan đến hiện tượng giật và khựng hình, nhưng đôi khi được thảo luận cùng với chúng. Độ trễ đầu vào là độ trễ có thể nhìn thấy trên màn hình khi thực hiện thao tác bằng chuột, bàn phím, tay cầm hoặc màn hình cảm ứng. Hiện tượng này có thể liên quan đến mã trò chơi, mã engine hoặc các yếu tố bên ngoài (chẳng hạn như phần cứng). Độ trễ đầu vào dễ nhận thấy nhất trong các trò chơi dùng chuột để ngắm, chẳng hạn như game góc nhìn thứ nhất. Không thể loại bỏ hoàn toàn độ trễ đầu vào, nhưng có thể giảm độ trễ theo nhiều cách.

Phân biệt hiện tượng giật và khựng hình
---------------------------------------

Một trò chơi chạy ở tốc độ khung hình bình thường mà không có bất kỳ hiệu ứng nào sẽ trông mượt mà:

.. image:: img/motion_normal.gif

Một trò chơi có hiện tượng *giật* sẽ rung liên tục theo một cách rất nhẹ:

.. image:: img/motion_jitter.gif

Cuối cùng, một trò chơi có hiện tượng *khựng hình* sẽ trông mượt mà, nhưng có vẻ như *dừng lại* hoặc *quay lui một khung hình* sau mỗi vài giây:

.. image:: img/motion_stutter.gif

Giật
----

Có thể có nhiều nguyên nhân gây ra hiện tượng giật. Nguyên nhân thường gặp nhất xảy ra khi *tần số vật lý* của trò chơi (thường là 60 Hz) chạy ở độ phân giải khác với tần số quét của màn hình. Hãy kiểm tra xem tần số quét của màn hình có khác 60 Hz hay không.

Đôi khi, chỉ một số đối tượng có vẻ bị giật (nhân vật hoặc nền). Điều này xảy ra khi chúng được xử lý ở các nguồn thời gian khác nhau (một đối tượng được xử lý trong bước vật lý, còn đối tượng kia được xử lý trong bước idle).

Có thể giảm bớt nguyên nhân gây giật này bằng cách bật
:ref:`nội suy vật lý <doc_physics_interpolation_quick_start_guide>` trong Project Settings. Nội suy vật lý sẽ làm mượt các cập nhật vật lý bằng cách nội suy các phép biến đổi của những đối tượng vật lý giữa các khung hình vật lý. Nhờ đó, biểu diễn trực quan của các đối tượng vật lý sẽ luôn trông mượt mà, bất kể tốc độ khung hình và tốc độ tick vật lý.

Việc bật nội suy vật lý có một số điểm cần lưu ý. Ví dụ, cần cẩn thận khi dịch chuyển tức thời các đối tượng để chúng không bị nội suy một cách dễ thấy giữa vị trí cũ và vị trí mới khi đó không phải là chủ ý. Xem
:ref:`doc_physics_interpolation` tài liệu để biết thêm chi tiết.

.. note::

    Việc bật nội suy vật lý sẽ làm tăng độ trễ đầu vào đối với các hành vi phụ thuộc vào tick vật lý, chẳng hạn như chuyển động của người chơi. Trong hầu hết trò chơi, điều này thường tốt hơn so với hiện tượng giật, nhưng hãy cân nhắc kỹ đối với các trò chơi hoạt động ở tốc độ khung hình cố định (chẳng hạn như game đối kháng hoặc game nhịp điệu). Có thể bù đắp phần độ trễ đầu vào tăng thêm này bằng cách tăng tốc độ tick vật lý như mô tả trong phần :ref:`doc_jitter_stutter_input_lag`.

Khựng hình
----------

Khựng hình có thể xảy ra vì nhiều nguyên nhân khác nhau. Một nguyên nhân là trò chơi không thể duy trì hiệu suất ở tốc độ khung hình tối đa do CPU hoặc GPU bị nghẽn. Cách khắc phục tùy thuộc vào từng trò chơi và sẽ cần đến
:ref:`tối ưu hóa <doc_general_optimization>`.

Một nguyên nhân phổ biến khác gây khựng hình là *khựng hình do biên dịch shader*. Hiện tượng này xảy ra khi một shader cần được biên dịch vào lần đầu tiên một material hoặc hiệu ứng particle mới được tạo ra trong trò chơi. Kiểu khựng hình này thường chỉ xảy ra trong lần chơi đầu tiên hoặc sau khi cập nhật driver đồ họa, khi bộ nhớ đệm shader bị vô hiệu hóa.

Kể từ Godot 4.4, khi sử dụng renderer Forward+ hoặc Mobile, engine cố gắng tránh hiện tượng khựng hình do biên dịch shader bằng cách tiếp cận ubershader. Để cách tiếp cận này đạt hiệu quả cao nhất, cần cẩn thận khi thiết kế các scene và resource để Godot có thể thu thập nhiều thông tin nhất có thể khi scene/resource được tải, thay vì khi chúng được vẽ lần đầu. Xem :ref:`doc_pipeline_compilations` để biết thêm thông tin.

Tuy nhiên, khi sử dụng renderer Compatibility, không thể dùng cách tiếp cận ubershader này do các hạn chế kỹ thuật trong OpenGL. Vì vậy, để tránh hiện tượng khựng hình do biên dịch shader trong renderer Compatibility, bạn cần tạo mọi mesh và hiệu ứng hình ảnh ở phía trước camera trong một khung hình duy nhất khi level đang tải. Điều này đảm bảo shader được biên dịch khi level được tải, thay vì được biên dịch trong lúc chơi. Bạn có thể thực hiện việc này phía sau UI 2D đặc (chẳng hạn như một
:ref:`class_ColorRect` node) để người chơi không nhìn thấy.

.. note::

    Trên các nền tảng hỗ trợ tắt V-Sync, có thể làm hiện tượng khựng hình khó nhận thấy hơn bằng cách tắt V-Sync trong phần cài đặt dự án. Tuy nhiên, thao tác này sẽ gây ra hiện tượng xé hình, đặc biệt trên các màn hình có tần số quét thấp. Nếu màn hình hỗ trợ, hãy cân nhắc bật tốc độ làm mới biến đổi (G-Sync/FreeSync) đồng thời vẫn bật V-Sync. Cách này giúp giảm một số dạng khựng hình mà không gây xé hình. Tuy nhiên, nó không giúp ích đối với các hiện tượng khựng hình lớn, chẳng hạn như hiện tượng khựng hình do biên dịch shader gây ra.

    Buộc card đồ họa sử dụng cấu hình hiệu suất tối đa cũng có thể giúp giảm hiện tượng khựng hình, đổi lại GPU sẽ tiêu thụ nhiều điện hơn.

Ngoài ra, khựng hình có thể do hệ điều hành bên dưới gây ra. Dưới đây là một số thông tin về hiện tượng khựng hình trên các hệ điều hành khác nhau:

Windows
~~~~~~~

Windows được biết là có thể gây khựng hình trong các trò chơi chạy ở chế độ cửa sổ. Điều này chủ yếu phụ thuộc vào phần cứng được cài đặt, phiên bản driver và các tiến trình chạy song song (ví dụ: mở nhiều tab trình duyệt có thể gây khựng hình trong trò chơi đang chạy). Để tránh điều này, Godot nâng mức ưu tiên của trò chơi lên "Above Normal". Cách này giúp cải thiện đáng kể, nhưng có thể không loại bỏ hoàn toàn hiện tượng khựng hình.

Để loại bỏ hoàn toàn hiện tượng này, cần cấp cho trò chơi đầy đủ đặc quyền để trở thành "Time Critical", nhưng không nên làm vậy. Một số trò chơi có thể thực hiện điều đó, nhưng bạn nên học cách chấp nhận vấn đề này, vì đây là hiện tượng phổ biến đối với trò chơi Windows và hầu hết người dùng sẽ không chơi game ở chế độ cửa sổ (các trò chơi được chơi trong cửa sổ, chẳng hạn như game giải đố, thường vốn không gặp vấn đề này).

Ở chế độ toàn màn hình, Windows dành mức ưu tiên đặc biệt cho trò chơi, vì vậy hiện tượng khựng hình sẽ không còn nhìn thấy và rất hiếm xảy ra. Đây là cách hầu hết trò chơi được chơi.

Khi sử dụng chuột có polling rate từ 1.000 Hz trở lên, hãy cân nhắc dùng bản cài đặt Windows 11 hoàn toàn cập nhật, vốn có các bản sửa lỗi liên quan đến mức sử dụng CPU cao với chuột có polling rate cao. Các bản sửa lỗi này không có trong Windows 10 và các phiên bản cũ hơn.

.. tip::

    Trò chơi nên sử dụng chế độ cửa sổ **Exclusive Fullscreen**, thay vì **Fullscreen**, vốn được thiết kế để ngăn Windows tự động xử lý cửa sổ như thể đó là chế độ toàn màn hình độc quyền.

    **Fullscreen** được dùng cho các ứng dụng GUI muốn sử dụng độ trong suốt theo từng pixel mà không có nguy cơ bị hệ điều hành vô hiệu hóa. Chế độ này đạt được điều đó bằng cách chừa lại một dòng 1 pixel ở cuối màn hình. Ngược lại, **Exclusive Fullscreen** sử dụng kích thước màn hình thực tế và cho phép Windows giảm hiện tượng giật cũng như độ trễ đầu vào đối với các trò chơi toàn màn hình.

Linux
~~~~~

Hiện tượng giật hình có thể xuất hiện trên Linux dành cho máy tính để bàn, nhưng thường liên quan đến các driver video và compositor khác nhau. Một số compositor cũng có thể gây ra vấn đề này (ví dụ: KWin), vì vậy bạn nên thử dùng một compositor khác để loại trừ nguyên nhân này. Một số window manager như KWin và Xfwm cho phép bạn tắt compositing theo cách thủ công, việc này có thể cải thiện hiệu năng (đổi lại sẽ xuất hiện hiện tượng xé hình).

Không có cách khắc phục hiện tượng giật hình do driver hoặc compositor, ngoài việc báo cáo vấn đề cho các nhà phát triển driver hoặc compositor. Hiện tượng giật hình có thể rõ rệt hơn khi chạy ở chế độ cửa sổ thay vì toàn màn hình, ngay cả khi đã tắt compositing.

`Feral GameMode <https://github.com/FeralInteractive/gamemode>`__ có thể được dùng để tự động áp dụng các tối ưu hóa (chẳng hạn như buộc GPU sử dụng cấu hình hiệu năng) khi chạy các process cụ thể.

macOS
~~~~~

Nhìn chung, macOS không bị giật hình, mặc dù gần đây đã có một số lỗi được báo cáo khi chạy ở chế độ toàn màn hình (đây là lỗi của macOS). Nếu bạn có một máy gặp phải hiện tượng này, vui lòng cho chúng tôi biết.

Android
~~~~~~~

Nhìn chung, Android không bị giật hình hoặc rung hình vì activity đang chạy được ưu tiên toàn bộ. Tuy vậy, một số thiết bị có thể gặp vấn đề (Kindle Fire đời cũ là một thiết bị được biết đến với vấn đề này). Nếu bạn gặp vấn đề này trên Android, vui lòng cho chúng tôi biết.

iOS
~~~

Các thiết bị iOS nhìn chung không bị giật hình, nhưng những thiết bị cũ chạy phiên bản mới hơn của hệ điều hành có thể gặp vấn đề. Nhìn chung, điều này không thể tránh khỏi.

.. _doc_jitter_stutter_input_lag:

Độ trễ đầu vào
--------------

Cấu hình project
~~~~~~~~~~~~~~~~

Trên các nền tảng hỗ trợ tắt V-Sync, bạn có thể làm cho độ trễ đầu vào ít đáng chú ý hơn bằng cách tắt V-Sync trong cài đặt project. Tuy nhiên, việc này sẽ khiến hiện tượng xé hình xuất hiện, đặc biệt trên các màn hình có tần số quét thấp. Bạn nên cung cấp V-Sync dưới dạng một tùy chọn để người chơi bật hoặc tắt.

Khi sử dụng phương thức render Forward+ hoặc Mobile, một cách khác để giảm độ trễ hình ảnh khi V-Sync được bật là sử dụng V-Sync với bộ đệm kép thay vì V-Sync với bộ đệm ba mặc định. Kể từ Godot 4.3, bạn có thể thực hiện việc này bằng cách giảm cài đặt project **Display > Window > V-Sync > Swapchain Image Count** xuống ``2``. Nhược điểm của bộ đệm kép là tốc độ khung hình sẽ kém ổn định hơn nếu không thể đạt được tần số quét của màn hình do nút thắt cổ chai ở CPU hoặc GPU. Ví dụ, trên màn hình 60 Hz, nếu tốc độ khung hình thường giảm xuống 55 FPS khi chơi game với bộ đệm ba, thì với bộ đệm kép, tốc độ này sẽ phải tạm thời giảm xuống 30 FPS (sau đó trở lại 60 FPS khi có thể). Vì vậy, V-Sync với bộ đệm kép chỉ được khuyến nghị nếu bạn có thể đạt *ổn định* tần số quét của màn hình trên phần cứng mục tiêu.

Tăng số lần lặp vật lý mỗi giây cũng có thể giảm độ trễ đầu vào do vật lý gây ra. Điều này đặc biệt dễ nhận thấy khi sử dụng nội suy vật lý (giúp chuyển động mượt hơn nhưng làm tăng độ trễ). Để thực hiện việc này, hãy đặt **Physics > Common > Physics Ticks Per Second** thành một giá trị cao hơn mặc định là ``60``, hoặc đặt ``Engine.physics_ticks_per_second`` trong script khi runtime. Các giá trị là bội số của tần số quét màn hình (thường là ``60``) hoạt động tốt nhất khi tắt nội suy vật lý, vì chúng sẽ tránh được hiện tượng rung hình. Điều này có nghĩa là các giá trị như ``120``, ``180`` và ``240`` là những điểm bắt đầu tốt. Ngoài ra, FPS vật lý cao hơn cũng làm giảm khả năng xảy ra các vấn đề xuyên vật thể và mất ổn định vật lý.

Nhược điểm của việc tăng FPS vật lý là mức sử dụng CPU sẽ tăng, điều này có thể dẫn đến các nút thắt cổ chai về hiệu năng trong những game có mã mô phỏng vật lý nặng. Bạn có thể giảm tác động này bằng cách chỉ tăng FPS vật lý trong những tình huống mà độ trễ thấp là yếu tố quan trọng, hoặc cho phép người chơi điều chỉnh FPS vật lý để phù hợp với phần cứng của họ. Tuy nhiên, FPS vật lý khác nhau sẽ dẫn đến các kết quả khác nhau trong mô phỏng vật lý, ngay cả khi ``delta`` được sử dụng nhất quán trong logic game. Điều này có thể mang lại lợi thế cho một số người chơi so với những người khác. Vì vậy, không nên cho phép người chơi tự thay đổi FPS vật lý trong các game multiplayer cạnh tranh.

Cuối cùng, bạn có thể tắt bộ đệm đầu vào trên cơ sở mỗi frame được render bằng cách gọi ``Input.set_use_accumulated_input(false)`` trong một script. Khi đó, các hàm ``_input()`` và ``_unhandled_input()`` trong script của bạn sẽ được gọi cho mỗi input, thay vì tích lũy input và chờ một frame được render. Việc tắt tích lũy input sẽ làm tăng mức sử dụng CPU, vì vậy cần thực hiện một cách thận trọng.

.. tip::

    Trên bất kỳ project Godot nào, bạn có thể sử dụng ``--disable-vsync``
    :ref:`command line argument <doc_command_line_tutorial>` để buộc tắt V-Sync. Kể từ Godot 4.2, ``--max-fps <fps>`` cũng có thể được dùng để đặt giới hạn FPS (``0`` là không giới hạn). Bạn có thể sử dụng đồng thời các đối số này.

Theo phần cứng/hệ điều hành
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu màn hình của bạn hỗ trợ, hãy cân nhắc bật variable refresh rate (G-Sync/FreeSync) trong khi vẫn bật V-Sync, sau đó giới hạn tốc độ khung hình trong cài đặt project ở một giá trị thấp hơn một chút so với tần số quét tối đa của màn hình, như mô tả trên `trang này <https://blurbusters.com/howto-low-lag-vsync-on/>`__.

Điều này thoạt đầu có thể trái với trực giác, nhưng giới hạn FPS thấp hơn phạm vi tần số quét tối đa sẽ đảm bảo hệ điều hành không bao giờ phải chờ quá trình blanking dọc hoàn tất. Nhờ đó, độ trễ đầu vào sẽ *tương tự* như khi tắt V-Sync với cùng giới hạn tốc độ khung hình (thường chỉ cao hơn dưới 1 ms), nhưng không xảy ra hiện tượng xé hình.

Công thức được sử dụng để xác định giới hạn tốc độ khung hình là ``refresh - (refresh * refresh / 3600.0)`` trong đó ``refresh`` là tần số quét của màn hình tính bằng Hz. Bảng này cho biết giới hạn tốc độ khung hình cần dùng cho các tần số quét phổ biến (giới hạn được làm tròn xuống số nguyên gần nhất):

+-------------+----------------------------+
| Tần số quét | Giới hạn tốc độ khung hình |
+=============+============================+
| 60 Hz       | 58 FPS                     |
+-------------+----------------------------+
| 75 Hz       | 73 FPS                     |
+-------------+----------------------------+
| 120 Hz      | 115 FPS                    |
+-------------+----------------------------+
| 144 Hz      | 138 FPS                    |
+-------------+----------------------------+
| 165 Hz      | 157 FPS                    |
+-------------+----------------------------+
| 240 Hz      | 224 FPS                    |
+-------------+----------------------------+
| 360 Hz      | 324 FPS                    |
+-------------+----------------------------+
| 480 Hz      | 416 FPS                    |
+-------------+----------------------------+

Giới hạn framerate này có thể được thiết lập bằng cách thay đổi cài đặt project **Application > Run > Max FPS** hoặc gán ``Engine.max_fps`` tại runtime trong một script. Ở tần số quét cao hơn, cần giới hạn thấp hơn để đảm bảo các sai số về thời gian không khiến màn hình bật V-Sync (điều này sẽ làm tăng input lag).

Trên một số nền tảng, bạn cũng có thể bật chế độ độ trễ thấp trong các tùy chọn driver đồ họa (chẳng hạn NVIDIA Control Panel trên Windows). Cài đặt **Ultra** sẽ mang lại độ trễ thấp nhất có thể, đổi lại framerate trung bình sẽ thấp hơn một chút. Buộc GPU sử dụng profile hiệu năng tối đa cũng có thể tiếp tục giảm input lag, nhưng sẽ làm tăng mức tiêu thụ điện (và kéo theo nhiệt độ/tiếng ồn quạt cao hơn).

Cuối cùng, hãy đảm bảo màn hình đang chạy ở tần số quét cao nhất có thể trong cài đặt hiển thị của hệ điều hành.

Ngoài ra, hãy đảm bảo chuột được cấu hình để sử dụng polling rate cao nhất (thường là 1.000 Hz đối với chuột gaming, đôi khi cao hơn). Tuy nhiên, polling rate USB cao có thể dẫn đến mức sử dụng CPU cao, vì vậy 500 Hz có thể là lựa chọn an toàn hơn trên các CPU cấp thấp. Nếu chuột của bạn cung cấp nhiều cài đặt :abbr:`DPI (Dots Per Inch)`, hãy cân nhắc `using the highest possible setting and reducing in-game sensitivity to reduce mouse latency <https://www.youtube.com/watch?v=6AoRfv9W110>`__.

Trên Linux khi sử dụng X11, việc tắt compositing trong các window manager cho phép thực hiện điều này (chẳng hạn KWin hoặc Xfwm) có thể giảm đáng kể input lag.

Báo cáo các vấn đề về jitter, stutter hoặc input lag
----------------------------------------------------

Nếu bạn đang báo cáo vấn đề stutter hoặc jitter (mở issue) không do bất kỳ nguyên nhân nào nêu trên gây ra, vui lòng nêu thật rõ tất cả thông tin có thể về thiết bị, hệ điều hành, phiên bản driver, v.v. Điều này có thể giúp việc khắc phục sự cố hiệu quả hơn.

Nếu bạn đang báo cáo vấn đề input lag, vui lòng kèm theo bản ghi được thực hiện bằng camera tốc độ cao (chẳng hạn chế độ quay slow motion trên điện thoại). Bản ghi **must** phải hiển thị cả màn hình và thiết bị nhập để có thể đếm số khung hình giữa một thao tác nhập và kết quả trên màn hình. Ngoài ra, hãy nhớ đề cập tần số quét của màn hình và polling rate của thiết bị nhập (đặc biệt là chuột).

Ngoài ra, hãy đảm bảo sử dụng đúng thuật ngữ (jitter, stutter, input lag) dựa trên hành vi quan sát được. Điều này sẽ giúp hiểu vấn đề của bạn nhanh hơn nhiều. Hãy cung cấp một project có thể dùng để tái hiện vấn đề và nếu có thể, kèm theo bản ghi màn hình minh họa lỗi.
