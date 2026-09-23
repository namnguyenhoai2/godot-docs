.. _doc_importing_audio_samples:

Nhập các mẫu âm thanh
=====================

Các định dạng âm thanh được hỗ trợ
----------------------------------

Godot cung cấp 3 tùy chọn để nhập dữ liệu âm thanh: WAV, Ogg Vorbis và MP3.

Mỗi định dạng có những ưu điểm khác nhau:

- Các tệp WAV sử dụng dữ liệu thô hoặc tính năng nén nhẹ (IMA ADPCM hoặc Quite OK Audio). Hiện tại, chúng chỉ có thể được nhập ở định dạng thô, nhưng Godot cho phép nén sau khi nhập. Việc phát lại chúng tiêu tốn ít tài nguyên CPU (có thể phát đồng thời hàng trăm voice ở định dạng này). Nhược điểm là chúng chiếm nhiều dung lượng đĩa.
- Các tệp Ogg Vorbis sử dụng tính năng nén mạnh hơn, giúp kích thước tệp nhỏ hơn nhiều, nhưng cần năng lực xử lý lớn hơn đáng kể để phát lại.
- Các tệp MP3 sử dụng tính năng nén tốt hơn WAV với IMA ADPCM hoặc Quite OK Audio, nhưng kém hơn Ogg Vorbis. Điều này có nghĩa là một tệp MP3 có chất lượng gần tương đương Ogg Vorbis sẽ lớn hơn đáng kể. Mặt tích cực là MP3 sử dụng ít CPU hơn Ogg Vorbis khi phát lại.

.. note::

    Nếu bạn đã biên dịch trình chỉnh sửa Godot từ mã nguồn với một số module cụ thể bị vô hiệu hóa, một số định dạng có thể không khả dụng.

Sau đây là biểu đồ so sánh kích thước tệp của 1 giây âm thanh ở mỗi định dạng:

+------------------------------+-----------------+
| Định dạng                    | 1 giây âm thanh |
+==============================+=================+
| WAV 24-bit, 96 kHz, stereo   | 576 KB          |
+------------------------------+-----------------+
| WAV 16-bit, 44 kHz, mono     | 88 KB           |
+------------------------------+-----------------+
| WAV IMA ADPCM, 44 kHz, mono  | 22 KB           |
+------------------------------+-----------------+
| Quite OK Audio, 44 kHz, mono | 17 KB           |
+------------------------------+-----------------+
| MP3 192 Kb/s, stereo         | 24 KB           |
+------------------------------+-----------------+
| Ogg Vorbis 128 Kb/s, stereo  | 16 KB           |
+------------------------------+-----------------+
| Ogg Vorbis 96 Kb/s, stereo   | 12 KB           |
+------------------------------+-----------------+

Lưu ý rằng các con số của MP3 và Ogg Vorbis có thể thay đổi tùy thuộc vào kiểu mã hóa. Để đơn giản, các con số trên sử dụng tính năng mã hóa :abbr:`CBR (Constant Bit Rate)`, nhưng hầu hết các tệp Ogg Vorbis và MP3 bạn tìm thấy trên mạng đều được mã hóa bằng tính năng mã hóa :abbr:`VBR (Variable Bit Rate)`, vốn hiệu quả hơn. Mã hóa VBR khiến kích thước tệp âm thanh thực tế phụ thuộc vào độ "phức tạp" của âm thanh nguồn.

.. tip::

    Hãy cân nhắc sử dụng WAV cho các hiệu ứng âm thanh ngắn và lặp lại, còn Ogg Vorbis cho nhạc, lời nói và các hiệu ứng âm thanh dài. MP3 hữu ích cho các dự án mobile và web, nơi tài nguyên CPU bị hạn chế, đặc biệt khi phát nhiều âm thanh đã nén cùng lúc (chẳng hạn như các âm thanh môi trường dài).

Nhập các mẫu âm thanh
---------------------

Sau khi chọn một tệp WAV trong dock FileSystem, bạn có thể sử dụng một số tùy chọn trong dock Import:

.. figure:: img/importing_audio_samples_import_options_wav.webp
   :align: center
   :alt: Các tùy chọn nhập trong dock Import sau khi chọn một tệp WAV trong dock FileSystem

   Các tùy chọn nhập trong dock Import sau khi chọn một tệp WAV trong dock FileSystem

Bộ tùy chọn khả dụng sau khi chọn một tệp Ogg Vorbis hoặc MP3 sẽ khác:

.. figure:: img/importing_audio_samples_import_options_mp3.webp
   :align: center
   :alt: Các tùy chọn nhập trong dock Import sau khi chọn một tệp MP3 trong dock FileSystem

   Các tùy chọn nhập trong dock Import sau khi chọn một tệp MP3 trong dock FileSystem. Các tùy chọn này giống hệt đối với tệp Ogg Vorbis.

Sau khi nhập một âm thanh, bạn có thể phát lại âm thanh đó bằng các node AudioStreamPlayer, AudioStreamPlayer2D hoặc AudioStreamPlayer3D. Xem :ref:`doc_audio_streams` để biết thêm thông tin.

Các tùy chọn nhập (WAV)
-----------------------

Force > 8 Bit
-------------

Nếu được bật, tùy chọn này buộc âm thanh đã nhập sử dụng lượng tử hóa 8-bit nếu tệp nguồn là 16-bit trở lên.

Nhìn chung, không nên bật tùy chọn này vì lượng tử hóa 8-bit làm giảm đáng kể chất lượng âm thanh. Nếu cần kích thước tệp nhỏ hơn, hãy cân nhắc sử dụng âm thanh Ogg Vorbis hoặc MP3.

Force > Mono
------------

Nếu được bật, tùy chọn này buộc âm thanh đã nhập chuyển thành mono nếu tệp nguồn là stereo. Tùy chọn này giảm kích thước tệp 50% bằng cách gộp hai kênh thành một.

Force > Max Rate
----------------

Nếu được đặt thành giá trị lớn hơn ``0``, tùy chọn này buộc sample rate của âm thanh giảm xuống một giá trị nhỏ hơn hoặc bằng giá trị được chỉ định tại đây.

Tùy chọn này có thể làm giảm đáng kể kích thước tệp đối với một số âm thanh nhất định mà không ảnh hưởng đến chất lượng, tùy thuộc vào nội dung thực tế của âm thanh. Xem
:ref:`doc_importing_audio_samples_best_practices` để biết thêm thông tin.

Edit > Trim
-----------

Tệp âm thanh nguồn có thể chứa những khoảng lặng dài ở đầu và/hoặc cuối. Các khoảng lặng này được :abbr:`DAWs (Digital Audio Workstations)` chèn vào khi lưu thành waveform, khiến kích thước tệp tăng không cần thiết và làm tăng độ trễ trước thời điểm âm thanh được phát lại.

Việc bật **Trim** sẽ tự động cắt phần đầu và cuối của âm thanh nếu mức của chúng thấp hơn -50 dB *sau khi* chuẩn hóa (xem **Edit > Normalize** bên dưới). Trong quá trình cắt, khoảng fade-in/fade-out 500 sample cũng được sử dụng để tránh tiếng tách có thể nghe thấy.

Edit > Normalize
----------------

Nếu được bật, âm lượng sẽ được *normalized* để âm lượng đỉnh bằng 0 dB. Khi được bật, tính năng chuẩn hóa sẽ khiến âm thanh to hơn tùy thuộc vào âm lượng đỉnh ban đầu của nó.

Edit > Loop Mode
----------------

Không giống Ogg Vorbis và MP3, các tệp WAV có thể chứa metadata cho biết chúng có lặp hay không (ngoài các điểm lặp). Theo mặc định, Godot sẽ tuân theo metadata này, nhưng bạn có thể chọn áp dụng một chế độ lặp cụ thể:

- **Detect from WAV:** Sử dụng thông tin lặp từ metadata của WAV.
- **Disabled:** Không lặp âm thanh, ngay cả khi metadata cho biết tệp nên được phát theo chế độ lặp.
- **Forward:** Lặp âm thanh tiêu chuẩn. Phát âm thanh theo chiều tiến từ đầu đến cuối vòng lặp, sau đó quay lại đầu vòng lặp và lặp lại.
- **Ping-Pong:** Phát âm thanh theo chiều tiến đến cuối vòng lặp, sau đó theo chiều ngược lại đến đầu vòng lặp và lặp lại chu kỳ này.
- **Backward:** Phát âm thanh theo chiều ngược lại từ cuối vòng lặp đến đầu vòng lặp, sau đó lặp lại.

Khi chọn một trong các chế độ lặp **Forward**, **Ping-Pong** hoặc **Backward**, bạn cũng có thể xác định các điểm lặp để chỉ lặp một phần cụ thể của âm thanh. **Loop Begin** được đặt theo số mẫu tính từ đầu tệp âm thanh. **Loop End** cũng được đặt theo số mẫu tính từ đầu tệp âm thanh, nhưng sẽ sử dụng cuối tệp âm thanh nếu được đặt thành ``-1``.

.. warning::

    Trong AudioStreamPlayer, tín hiệu ``finished`` sẽ không được phát ra đối với âm thanh lặp khi âm thanh đến cuối tệp, vì âm thanh sẽ tiếp tục phát vô thời hạn.

Chế độ Compress
---------------

Có thể chọn một trong ba chế độ nén cho các tệp WAV: **PCM (Uncompressed)**, **IMA ADPCM** hoặc **Quite OK Audio** (mặc định). **IMA ADPCM** giảm đôi chút kích thước tệp và mức sử dụng bộ nhớ, nhưng làm giảm chất lượng theo cách có thể nghe thấy. **Quite OK Audio** giảm kích thước tệp nhiều hơn một chút so với **IMA ADPCM** và mức giảm chất lượng khó nhận thấy hơn nhiều, nhưng sử dụng CPU cao hơn một chút (vẫn thấp hơn MP3 nhiều).

Ogg Vorbis và MP3 không làm giảm chất lượng nhiều như vậy và có thể giảm kích thước tệp đáng kể hơn, nhưng sử dụng CPU nhiều hơn trong khi phát. Mức sử dụng CPU cao hơn này thường không phải vấn đề (đặc biệt với MP3), trừ khi phát hàng chục âm thanh đã nén cùng lúc trên các nền tảng di động/web.

Tùy chọn import (Ogg Vorbis và MP3)
-----------------------------------

Lặp
~~~

Nếu được bật, âm thanh sẽ bắt đầu phát lại từ đầu sau khi quá trình phát kết thúc do đến cuối âm thanh.

.. warning::

    Trong AudioStreamPlayer, tín hiệu ``finished`` sẽ không được phát ra đối với âm thanh lặp khi âm thanh đến cuối tệp, vì âm thanh sẽ tiếp tục phát vô thời hạn.

Độ lệch vòng lặp
~~~~~~~~~~~~~~~~

Độ lệch vòng lặp xác định vị trí âm thanh sẽ bắt đầu lặp sau khi quá trình phát đến cuối âm thanh. Bạn có thể dùng tùy chọn này để chỉ lặp một phần của tệp âm thanh, hữu ích với một số âm thanh môi trường hoặc nhạc. Giá trị được xác định theo giây tính từ đầu âm thanh, vì vậy ``0`` sẽ lặp toàn bộ tệp âm thanh.

Chỉ có tác dụng khi **Loop** được bật.

Một trình chỉnh sửa thuận tiện hơn cho **Loop Offset** được cung cấp trong
hộp thoại :ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`, cho phép bạn xem trước các thay đổi mà không cần import lại âm thanh.

BPM
~~~

Số nhịp mỗi phút của bản nhạc. Giá trị này phải khớp với số đo BPM được sử dụng để soạn bản nhạc. Giá trị này chỉ liên quan đến nhạc muốn sử dụng chức năng nhạc tương tác, không áp dụng cho hiệu ứng âm thanh.

Một trình chỉnh sửa thuận tiện hơn cho **BPM** được cung cấp trong
hộp thoại :ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`, cho phép bạn xem trước các thay đổi mà không cần import lại âm thanh.

Số phách
~~~~~~~~

Số phách của bản nhạc. Giá trị này chỉ liên quan đến nhạc muốn sử dụng chức năng nhạc tương tác, không áp dụng cho hiệu ứng âm thanh.

Một trình chỉnh sửa thuận tiện hơn cho **Beat Count** được cung cấp trong
hộp thoại :ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`, cho phép bạn xem trước các thay đổi mà không cần import lại âm thanh.

Số phách mỗi ô nhịp
~~~~~~~~~~~~~~~~~~~

Số ô nhịp trong một phách của bản nhạc. Giá trị này chỉ liên quan đến nhạc muốn sử dụng chức năng nhạc tương tác, không áp dụng cho hiệu ứng âm thanh.

Một trình chỉnh sửa thuận tiện hơn cho **Bar Beats** được cung cấp trong
hộp thoại :ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`, cho phép bạn xem trước các thay đổi mà không cần import lại âm thanh.

.. _doc_importing_audio_samples_advanced_import_settings:

Cài đặt import nâng cao (Ogg Vorbis và MP3)
-------------------------------------------

Nếu bạn nhấp đúp vào tệp Ogg Vorbis hoặc MP3 trong dock FileSystem (hoặc chọn **Advanced…** trong dock Import), một hộp thoại sẽ xuất hiện:

.. figure:: img/importing_audio_samples_advanced_import_settings.webp
   :align: center
   :alt: Hộp thoại nâng cao khi nhấp đúp vào tệp Ogg Vorbis hoặc MP3 trong dock FileSystem

   Hộp thoại nâng cao khi nhấp đúp vào tệp Ogg Vorbis hoặc MP3 trong dock FileSystem

Hộp thoại này cho phép bạn chỉnh sửa điểm lặp của âm thanh với bản xem trước theo thời gian thực, cùng với :abbr:`BPM (Beats Per Minute)`, số phách và số phách mỗi ô nhịp. Ba cài đặt này được dùng cho nhạc tương tác, để chuyển mượt mà giữa các bản nhạc khác nhau.

.. note::

    Không giống các tệp WAV, Ogg Vorbis và MP3 chỉ hỗ trợ điểm lặp "loop begin", không hỗ trợ điểm "loop end". Việc lặp cũng chỉ có thể là lặp theo chiều tiến tiêu chuẩn, không hỗ trợ ping-pong hoặc chiều ngược lại.

.. _doc_importing_audio_samples_best_practices:

Các phương pháp hay nhất
------------------------

Sử dụng cài đặt chất lượng phù hợp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù việc lưu giữ các nguồn âm thanh có chất lượng nguyên bản rất quan trọng khi bạn thực hiện chỉnh sửa, nhưng không cần sử dụng cùng chất lượng trong project đã export. Đối với các tệp WAV, Godot cung cấp một số tùy chọn import để giảm kích thước tệp cuối cùng mà không sửa đổi tệp nguồn trên đĩa.

Để giảm mức sử dụng bộ nhớ và kích thước tệp, hãy chọn quantization, sample rate và số kênh phù hợp cho âm thanh của bạn:

- Không có lợi ích *audible* nào khi sử dụng âm thanh 24-bit, đặc biệt trong game nơi thường có nhiều âm thanh phát cùng lúc (khiến việc cảm nhận từng âm thanh riêng lẻ trở nên khó hơn).
- Trừ khi bạn giảm tốc độ âm thanh trong runtime, không có lợi ích *nghe được* nào khi sử dụng sample rate cao hơn 48 kHz. Nếu muốn giữ lại nguồn có sample rate cao hơn để chỉnh sửa, hãy sử dụng tùy chọn import **Force > Max Rate** để giới hạn sample rate của âm thanh được import (chỉ khả dụng cho tệp WAV).
- Nói chung, nhiều hiệu ứng âm thanh có thể được chuyển đổi sang mono thay vì stereo. Nếu muốn giữ lại nguồn stereo để chỉnh sửa, hãy sử dụng tùy chọn import **Force > Mono** để chuyển đổi âm thanh được import sang mono (chỉ khả dụng cho tệp WAV).
- Nói chung, giọng nói có thể được chuyển đổi sang mono, nhưng cũng có thể giảm sample rate xuống 22 kHz mà không làm giảm chất lượng đáng kể (trừ khi giọng nói có cao độ rất cao). Điều này là do hầu hết giọng nói của con người không bao giờ vượt quá 11 kHz.

Sử dụng hiệu ứng âm thanh real-time để giảm kích thước tệp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot có :ref:`hệ thống bus phong phú <doc_audio_buses>` với các hiệu ứng tích hợp sẵn. Điều này giúp các nghệ sĩ SFX không cần thêm reverb vào hiệu ứng âm thanh, nhờ đó giảm đáng kể kích thước của chúng và đảm bảo việc cắt âm thanh chính xác.

.. image:: img/reverb.png

Như bạn có thể thấy ở trên, hiệu ứng âm thanh sẽ có kích thước tệp lớn hơn nhiều khi được thêm reverb.

.. seealso::

    Mẫu âm thanh có thể được tải và lưu trong runtime bằng
    :ref:`việc tải và lưu tệp trong runtime <doc_runtime_file_loading_and_saving_audio_video_files>`, kể cả từ một project đã export.
