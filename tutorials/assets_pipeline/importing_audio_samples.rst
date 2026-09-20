.. _doc_importing_audio_samples:

Nhập các mẫu âm thanh
=====================

Các định dạng âm thanh được hỗ trợ
----------------------------------

Godot cung cấp 3 tùy chọn để nhập dữ liệu âm thanh của bạn: WAV, Ogg Vorbis và MP3.

Mỗi định dạng có những ưu điểm khác nhau:

- Tệp WAV sử dụng dữ liệu thô hoặc phương pháp nén nhẹ (IMA ADPCM hoặc Quite OK Audio). Hiện tại, chúng chỉ có thể được nhập ở định dạng thô, nhưng Godot cho phép nén sau khi nhập. Chúng nhẹ khi phát lại trên CPU (hàng trăm voice đồng thời ở định dạng này vẫn ổn). Nhược điểm là chúng chiếm nhiều dung lượng đĩa. - Tệp Ogg Vorbis sử dụng phương pháp nén mạnh hơn, cho kích thước tệp nhỏ hơn nhiều, nhưng cần nhiều năng lực xử lý hơn đáng kể để phát lại. - Tệp MP3 sử dụng phương pháp nén tốt hơn WAV với IMA ADPCM hoặc Quite OK Audio, nhưng kém hơn Ogg Vorbis. Điều này có nghĩa là một tệp MP3 có chất lượng gần tương đương Ogg Vorbis sẽ lớn hơn đáng kể. Điểm thuận lợi là MP3 yêu cầu ít CPU hơn để phát lại so với Ogg Vorbis.

.. note::

    Nếu bạn đã biên dịch trình chỉnh sửa Godot từ mã nguồn với một số module cụ thể bị vô hiệu hóa, một số định dạng có thể không khả dụng.

Dưới đây là biểu đồ so sánh biểu diễn kích thước tệp của 1 giây âm thanh ở mỗi định dạng:

+------------------------------+-------------------+
| Format                       | 1 second of audio |
+==============================+===================+
| WAV 24-bit, 96 kHz, stereo   | 576 KB            |
+------------------------------+-------------------+
| WAV 16-bit, 44 kHz, mono     | 88 KB             |
+------------------------------+-------------------+
| WAV IMA ADPCM, 44 kHz, mono  | 22 KB             |
+------------------------------+-------------------+
| Quite OK Audio, 44 kHz, mono | 17 KB             |
+------------------------------+-------------------+
| MP3 192 Kb/s, stereo         | 24 KB             |
+------------------------------+-------------------+
| Ogg Vorbis 128 Kb/s, stereo  | 16 KB             |
+------------------------------+-------------------+
| Ogg Vorbis 96 Kb/s, stereo   | 12 KB             |
+------------------------------+-------------------+

Lưu ý rằng các số liệu của MP3 và Ogg Vorbis có thể thay đổi tùy thuộc vào loại encoding. Các số liệu trên sử dụng encoding :abbr:`CBR (Constant Bit Rate)` để đơn giản hóa, nhưng hầu hết tệp Ogg Vorbis và MP3 bạn tìm thấy trên mạng đều được mã hóa bằng encoding :abbr:`VBR (Variable Bit Rate)`, vốn hiệu quả hơn. Encoding VBR khiến kích thước tệp âm thanh thực tế phụ thuộc vào mức độ "phức tạp" của âm thanh nguồn.

.. tip::

    Hãy cân nhắc sử dụng WAV cho các hiệu ứng âm thanh ngắn và lặp lại, còn Ogg Vorbis cho nhạc, lời nói và các hiệu ứng âm thanh dài. MP3 hữu ích cho các dự án di động và web, nơi tài nguyên CPU bị hạn chế, đặc biệt khi phát nhiều âm thanh đã nén cùng lúc (chẳng hạn như các âm thanh môi trường dài).

Nhập các mẫu âm thanh
---------------------

Sau khi chọn một tệp WAV trong dock FileSystem, bạn có thể sử dụng một số tùy chọn trong dock Import:

.. figure:: img/importing_audio_samples_import_options_wav.webp
   :align: center
   :alt: Import options in the Import dock after selecting a WAV file in the FileSystem dock

   Import options in the Import dock after selecting a WAV file in the FileSystem dock

Bộ tùy chọn khả dụng sau khi chọn tệp Ogg Vorbis hoặc MP3 sẽ khác:

.. figure:: img/importing_audio_samples_import_options_mp3.webp
   :align: center
   :alt: Import options in the Import dock after selecting an MP3 file in the FileSystem dock

   Import options in the Import dock after selecting an MP3 file in the
   FileSystem dock. Options are identical for Ogg Vorbis files.

Sau khi nhập âm thanh, bạn có thể phát âm thanh bằng các node AudioStreamPlayer, AudioStreamPlayer2D hoặc AudioStreamPlayer3D. Xem :ref:`doc_audio_streams` để biết thêm thông tin.

Tùy chọn nhập (WAV)
-------------------

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
:ref:`doc_importing_audio_samples_best_practices` for more information.

Edit > Trim
-----------

Tệp âm thanh nguồn có thể chứa những khoảng im lặng dài ở đầu và/hoặc cuối. Những khoảng im lặng này được :abbr:`DAWs (Digital Audio Workstations)` chèn vào khi lưu thành waveform, làm tăng kích thước một cách không cần thiết và tạo độ trễ trước thời điểm chúng được phát lại.

Bật **Trim** sẽ tự động cắt phần đầu và cuối của âm thanh nếu mức âm thấp hơn -50 dB *sau khi* normalization (xem **Edit > Normalize** bên dưới). Trong quá trình cắt, một khoảng fade-in/fade-out gồm 500 sample cũng được sử dụng để tránh tiếng pop có thể nghe thấy.

Edit > Normalize
----------------

Nếu được bật, âm lượng sẽ được *normalize* để âm lượng đỉnh bằng 0 dB. Khi được bật, normalization sẽ khiến âm thanh nghe to hơn tùy thuộc vào âm lượng đỉnh ban đầu của nó.

Edit > Loop Mode
----------------

Không giống Ogg Vorbis và MP3, tệp WAV có thể chứa metadata cho biết chúng có lặp hay không (ngoài các loop point). Theo mặc định, Godot sẽ tuân theo metadata này, nhưng bạn có thể chọn áp dụng một loop mode cụ thể:

- **Detect from WAV:** Sử dụng thông tin lặp từ metadata của WAV. - **Disabled:** Không lặp âm thanh, ngay cả khi metadata cho biết tệp nên được phát lặp. - **Forward:** Lặp âm thanh tiêu chuẩn. Phát âm thanh theo chiều thuận từ đầu đến loop end, sau đó quay lại loop beginning và lặp lại. - **Ping-Pong:** Phát âm thanh theo chiều thuận đến loop end, sau đó phát ngược về loop beginning và lặp lại chu kỳ này. - **Backward:** Phát âm thanh ngược từ loop end đến loop beginning, sau đó lặp lại.

Khi chọn một trong các loop mode **Forward**, **Ping-Pong** hoặc **Backward**, bạn cũng có thể xác định loop point để chỉ lặp một phần cụ thể của âm thanh. **Loop Begin** được đặt theo số sample tính từ đầu tệp âm thanh. **Loop End** cũng được đặt theo số sample tính từ đầu tệp âm thanh, nhưng sẽ sử dụng cuối tệp âm thanh nếu được đặt thành ``-1``.

.. warning::

    Trong AudioStreamPlayer, signal ``finished`` sẽ không được phát cho âm thanh lặp khi âm thanh chạm đến cuối tệp, vì âm thanh sẽ tiếp tục phát vô thời hạn.

Compress > Mode
---------------

Có thể chọn một trong ba compression mode cho tệp WAV: **PCM (Uncompressed)**, **IMA ADPCM** hoặc **Quite OK Audio** (mặc định). **IMA ADPCM** giảm một phần kích thước tệp và mức sử dụng bộ nhớ, đổi lại chất lượng giảm theo cách có thể nghe thấy. **Quite OK Audio** giảm kích thước tệp nhiều hơn một chút so với **IMA ADPCM** và mức giảm chất lượng khó nhận thấy hơn nhiều, đổi lại mức sử dụng CPU cao hơn một chút (vẫn thấp hơn MP3 rất nhiều).

Ogg Vorbis và MP3 không làm giảm chất lượng nhiều như vậy và có thể giảm kích thước tệp nhiều hơn, đổi lại mức sử dụng CPU cao hơn trong khi phát lại. Mức sử dụng CPU cao hơn này thường không phải vấn đề (đặc biệt với MP3), trừ khi phát hàng chục âm thanh đã nén cùng lúc trên các nền tảng di động/web.

Tùy chọn nhập (Ogg Vorbis và MP3)
---------------------------------

Loop
~~~~

Nếu được bật, âm thanh sẽ bắt đầu phát lại từ đầu sau khi quá trình phát kết thúc do chạm đến cuối âm thanh.

.. warning::

    Trong AudioStreamPlayer, signal ``finished`` sẽ không được phát cho âm thanh lặp khi âm thanh chạm đến cuối tệp, vì âm thanh sẽ tiếp tục phát vô thời hạn.

Loop Offset
~~~~~~~~~~~

Loop offset xác định vị trí âm thanh sẽ bắt đầu lặp sau khi quá trình phát chạm đến cuối âm thanh. Tùy chọn này có thể được dùng để chỉ lặp một phần của tệp âm thanh, rất hữu ích cho một số âm thanh môi trường hoặc nhạc. Giá trị được xác định theo giây tính từ đầu âm thanh, vì vậy ``0`` sẽ lặp toàn bộ tệp âm thanh.

Chỉ có tác dụng khi **Loop** được bật.

Một trình chỉnh sửa thuận tiện hơn cho **Loop Offset** được cung cấp trong
:ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`
hộp thoại, cho phép bạn xem trước các thay đổi mà không cần nhập lại âm thanh.

BPM
~~~

Beats Per Minute của track âm thanh. Giá trị này phải khớp với số đo BPM được sử dụng để soạn track. Tùy chọn này chỉ liên quan đến nhạc muốn sử dụng chức năng interactive music, không áp dụng cho hiệu ứng âm thanh.

Một trình chỉnh sửa thuận tiện hơn cho **BPM** được cung cấp trong
:ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`
hộp thoại, cho phép bạn xem trước các thay đổi mà không cần nhập lại âm thanh.

Beat Count
~~~~~~~~~~

Số nhịp của track âm thanh. Tùy chọn này chỉ liên quan đến nhạc muốn sử dụng chức năng interactive music, không áp dụng cho hiệu ứng âm thanh.

Một trình chỉnh sửa thuận tiện hơn cho **Beat Count** được cung cấp trong
:ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`
hộp thoại, cho phép bạn xem trước các thay đổi mà không cần nhập lại âm thanh.

Bar Beats
~~~~~~~~~

Số ô nhịp trong một beat của track âm thanh. Tùy chọn này chỉ liên quan đến nhạc muốn sử dụng chức năng interactive music, không áp dụng cho hiệu ứng âm thanh.

Một trình chỉnh sửa thuận tiện hơn cho **Bar Beats** được cung cấp trong
:ref:`Advanced import settings <doc_importing_audio_samples_advanced_import_settings>`
hộp thoại, cho phép bạn xem trước các thay đổi mà không cần nhập lại âm thanh.

.. _doc_importing_audio_samples_advanced_import_settings:

Cài đặt nhập nâng cao (Ogg Vorbis và MP3)
-----------------------------------------

Nếu bạn nhấp đúp vào tệp Ogg Vorbis hoặc MP3 trong dock FileSystem (hoặc chọn **Advanced…** trong dock Import), một hộp thoại sẽ xuất hiện:

.. figure:: img/importing_audio_samples_advanced_import_settings.webp
   :align: center
   :alt: Advanced dialog when double-clicking an Ogg Vorbis or MP3 file in the FileSystem dock

   Advanced dialog when double-clicking an Ogg Vorbis or MP3 file in the FileSystem dock

Hộp thoại này cho phép bạn chỉnh sửa loop point của âm thanh với chế độ xem trước theo thời gian thực, cùng với :abbr:`BPM (Beats Per Minute)`, beat count và bar beats. 3 cài đặt này được sử dụng cho interactive music, giúp chuyển đổi mượt mà giữa các track nhạc khác nhau.

.. note::

    Không giống tệp WAV, Ogg Vorbis và MP3 chỉ hỗ trợ loop point "loop begin", không hỗ trợ điểm "loop end". Việc lặp cũng chỉ có thể là lặp theo chiều thuận tiêu chuẩn, không hỗ trợ ping-pong hoặc backward.

.. _doc_importing_audio_samples_best_practices:

Các phương pháp hay nhất
------------------------

Sử dụng cài đặt chất lượng phù hợp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mặc dù việc giữ các nguồn âm thanh có chất lượng nguyên bản là quan trọng nếu bạn thực hiện chỉnh sửa, nhưng không cần thiết phải sử dụng cùng chất lượng đó trong project đã export. Đối với tệp WAV, Godot cung cấp một số tùy chọn nhập để giảm kích thước tệp cuối cùng mà không sửa đổi tệp nguồn trên đĩa.

Để giảm mức sử dụng bộ nhớ và kích thước tệp, hãy chọn quantization, sample rate và số lượng kênh phù hợp cho âm thanh của bạn:

- Không có lợi ích *nghe được* nào khi sử dụng âm thanh 24-bit, đặc biệt là trong game nơi thường có nhiều âm thanh phát cùng lúc (khiến việc cảm nhận từng âm thanh riêng lẻ trở nên khó hơn). - Trừ khi bạn làm chậm âm thanh trong runtime, không có lợi ích *nghe được* nào khi sử dụng sample rate cao hơn 48 kHz. Nếu muốn giữ lại nguồn có sample rate cao hơn để chỉnh sửa, hãy sử dụng tùy chọn import **Force > Max Rate** để giới hạn sample rate của âm thanh được import (chỉ khả dụng cho các tệp WAV). - Nói chung, nhiều sound effect có thể được chuyển đổi sang mono thay vì stereo. Nếu muốn giữ lại nguồn stereo để chỉnh sửa, hãy sử dụng tùy chọn import **Force > Mono** để chuyển đổi âm thanh được import sang mono (chỉ khả dụng cho các tệp WAV). - Nói chung, voice có thể được chuyển đổi sang mono, đồng thời sample rate cũng có thể được giảm xuống 22 kHz mà không làm giảm chất lượng đáng kể (trừ khi voice có cao độ rất cao). Điều này là do hầu hết giọng người không bao giờ vượt quá 11 kHz.

Sử dụng hiệu ứng âm thanh theo thời gian thực để giảm kích thước tệp
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Godot có :ref:`extensive bus system <doc_audio_buses>` với các hiệu ứng được tích hợp sẵn. Điều này giúp các nghệ sĩ SFX không cần thêm reverb vào sound effect, nhờ đó giảm đáng kể kích thước của chúng và đảm bảo việc cắt đúng cách.

.. image:: img/reverb.png

Như bạn có thể thấy ở trên, kích thước tệp của sound effect tăng lên đáng kể khi được thêm reverb.

.. seealso::

    Các sample âm thanh có thể được tải và lưu trong runtime bằng
    :ref:`runtime file loading and saving <doc_runtime_file_loading_and_saving_audio_video_files>`,
    kể cả từ một project đã export.
