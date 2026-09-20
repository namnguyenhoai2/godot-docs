.. _doc_audio_effects:

Hiệu ứng âm thanh
=================

Godot bao gồm một số hiệu ứng âm thanh có thể được thêm vào một audio bus để thay đổi mọi âm thanh đi qua bus đó.

.. image:: img/audio_buses4.webp

Việc hiểu cách hoạt động của từng hiệu ứng có thể khó, vì vậy đừng nản lòng nếu bạn phải tra cứu! Nếu bạn mới làm quen với âm thanh, hiểu các hiệu ứng thiết yếu có thể giúp ích trong hầu hết trường hợp! Đó là:

- Equalizer & Filter - Limiter - Delay & Reverb

Hãy thử từng hiệu ứng để cảm nhận cách chúng thay đổi âm thanh.

.. note::

  :ref:`AudioSample <class_AudioSample>` does not support these effects.

Sau đây là mô tả ngắn về các hiệu ứng hiện có:

Amplify
~~~~~~~

Thay đổi âm lượng của âm thanh. Tuy nhiên, cần cẩn thận: đặt mức âm lượng quá cao có thể khiến âm thanh bị clip kỹ thuật số, tạo ra những tiếng lách tách và bụp khó chịu. Hãy cân nhắc sử dụng một
:ref:`hard limiter <doc_hard_limiter>` or a :ref:`compressor <doc_compressor>`
để ngăn clipping, hoặc :ref:`distortion <doc_distortion>` ở chế độ clip nếu muốn clipping ở mức 0 dB hoặc thấp hơn.

.. _doc_band_limit_filter:

BandLimitFilter
~~~~~~~~~~~~~~~

Bộ lọc "band-limit" làm suy giảm các tần số tại điểm *cutoff* và cho phép các tần số bên ngoài điểm đó đi qua không thay đổi. Nó tương tự như :ref:`notch filter <doc_notch_filter>`, nhưng yếu hơn. Nó đối lập với :ref:`band-pass filter <doc_band_pass_filter>`. Có thể sử dụng bộ lọc này để tạo thêm khoảng trống cho các âm thanh khác phát ở điểm cutoff.

.. _doc_band_pass_filter:

BandPassFilter
~~~~~~~~~~~~~~

Bộ lọc "band-pass" cho phép các tần số tại điểm *cutoff* đi qua không thay đổi và làm suy giảm các tần số bên ngoài điểm đó. Nó đối lập với
:ref:`band-limit filter <doc_band_limit_filter>` and
:ref:`notch filter <doc_notch_filter>`. This filter can be used to simulate
âm thanh truyền qua đường dây điện thoại cũ hoặc loa phóng thanh. Việc điều biến điểm cutoff có thể mô phỏng âm thanh của pedal guitar wah-wah; hãy nghĩ đến tiếng guitar trong *Voodoo Child (Slight Return)* của Jimi Hendrix.

Capture
~~~~~~~

Sao chép các mẫu âm thanh của audio bus mà hiệu ứng này được gắn vào một ring buffer nội bộ. Có thể dùng tính năng này để thu dữ liệu từ microphone hoặc truyền âm thanh qua mạng theo thời gian thực. Nhìn chung, tính năng này có thể được dùng để lưu trữ dữ liệu âm thanh theo thời gian thực để phát lại, thậm chí tạo trực quan hóa âm thanh theo thời gian thực, chẳng hạn như oscilloscope. Hiệu ứng này không thay đổi âm thanh.

Chorus
~~~~~~

Hiệu ứng "chorus" nhân bản một tín hiệu rồi thay đổi rất nhẹ thời điểm và cao độ của từng bản sao, đồng thời điều biến chúng theo thời gian bằng LFO (low-frequency oscillator). Các bản sao (còn gọi là "voices") sau đó được trộn lại với tín hiệu gốc, tạo cảm giác âm thanh phát ra từ nhiều nguồn. Trong thực tế, loại hiệu ứng này thường có trong piano, hợp xướng và các nhóm nhạc cụ. Hiệu ứng này cũng có thể được dùng để mở rộng âm thanh mono và khiến âm thanh kỹ thuật số có chất lượng tự nhiên hoặc analog hơn.

.. _doc_compressor:

Compressor
~~~~~~~~~~

Hiệu ứng "compressor" tự động làm suy giảm (hoặc "duck") âm lượng của tín hiệu đầu vào khi biên độ của nó vượt quá một ngưỡng âm lượng nhất định. Mức suy giảm được áp dụng tỷ lệ thuận với mức tín hiệu âm thanh đầu vào vượt quá ngưỡng. Tham số Ratio của compressor kiểm soát mức độ suy giảm. Một trong những công dụng chính của compressor là giảm dynamic range của các tín hiệu có những phần rất lớn và rất nhỏ. Giảm dynamic range của tín hiệu có thể giúp tín hiệu hòa trộn thoải mái hơn trong một mix.

Compressor có nhiều công dụng. Ví dụ:

- Có thể dùng nó trên Master bus để nén toàn bộ đầu ra trước khi tín hiệu chạm đến ceiling của limiter, khiến hiệu ứng của limiter tinh tế hơn nhiều. - Có thể dùng nó trong các voice clip để đảm bảo chúng có âm lượng đồng đều nhất có thể. - Nó có thể được *sidechain* bởi một nguồn âm thanh khác. Điều này nghĩa là nó có thể giảm âm lượng của một tín hiệu bằng cách sử dụng âm lượng của một audio bus khác để phát hiện ngưỡng. Kỹ thuật này rất phổ biến trong việc mixing game để "duck" âm lượng của nhạc hoặc hiệu ứng âm thanh khi giọng nói trong game hoặc multiplayer cần được nghe rõ hoàn toàn. - Nó có thể làm nổi bật các *transient* bằng cách sử dụng attack chậm hơn, cho phép những phần lớn hơn đi qua trước khi bị nén. Điều này có thể nhấn mạnh độ "punchy" của hiệu ứng âm thanh.

.. note::

  Nếu mục tiêu duy nhất của bạn là ngăn tín hiệu hoàn toàn vượt quá một biên độ nhất định, :ref:`hard limiter <doc_hard_limiter>` có thể là lựa chọn phù hợp hơn compressor cho mục đích này. Tuy nhiên, áp dụng compression trước limiter vẫn là một thực hành tốt.

.. _doc_delay:

Delay
~~~~~

Hiệu ứng "delay" nhân bản một tín hiệu và lặp lại tín hiệu đó nhiều lần, với một khoảng thời gian ngắn giữa mỗi lần lặp (còn gọi là "tap"). Âm lượng của các tap giảm dần theo thời gian. Tất cả những điều này tạo ra hiệu ứng echo. Delay rất phù hợp để mô phỏng không gian âm học của hẻm núi hoặc căn phòng lớn, nơi âm thanh dội lại từ các bề mặt và đến tai người nghe sau một khoảng *delay*. Điều này tương tự như
:ref:`reverb <doc_reverb>`, which has a more natural and blurred sound to it.
Sử dụng delay kết hợp với reverb có thể tạo ra môi trường âm thanh rất tự nhiên.

.. _doc_distortion:

Distortion
~~~~~~~~~~

Hiệu ứng "distortion" thay đổi âm lượng của âm thanh theo cách làm biến đổi waveform của nó, từ đó có thể tạo ra âm thanh "gắt" và "sáng".

Dưới đây là một số loại distortion mà Godot cung cấp:

- *Clip*: giới hạn âm lượng của âm thanh, khiến âm thanh trở nên gắt. - *Overdrive*: cho âm thanh giống pedal distortion của guitar hoặc loa phóng thanh. - *Lo-fi*: giảm *bit depth* của tín hiệu, mô phỏng các loa cũ.

Mọi loại distortion đều có thể thêm các tần số cao hơn vào âm thanh gốc, giúp âm thanh nổi bật hơn trong một mix.

.. warning::

  Hãy cẩn thận với lượng distortion được thêm vào, vì nó có thể tạo ra âm thanh rất gắt và lớn.

EQ ~~

Một "equalizer" cho phép bạn kiểm soát gain của các tần số trong toàn bộ spectrum thông qua việc sử dụng các "band" đại diện cho những vùng khác nhau của spectrum. Equalizer có thể rất cần thiết để tạo ra một mix sạch hơn, cho phép nhiều âm thanh phát cùng nhau mà không cạnh tranh tần số với nhau. Equalizer trên Master bus có thể hữu ích để làm suy giảm các tần số thấp và cao mà loa của thiết bị không thể tái tạo tốt. Ví dụ, loa điện thoại và máy tính bảng thường không tái tạo tốt âm thanh tần số thấp, và có thể khiến limiter hoặc compressor làm suy giảm âm lượng Master nhiều hơn mức cần thiết. Có thể tắt hiệu ứng này khi cắm tai nghe, giúp người dùng có được lợi ích tốt nhất trong cả hai trường hợp.

.. note::

  Hiệu ứng âm thanh này là lớp mà mọi equalizer khác kế thừa. Có thể mở rộng nó bằng các script tùy chỉnh để tạo một equalizer với số lượng band tùy chỉnh.

EQ6, EQ10, EQ21
~~~~~~~~~~~~~~~

Godot cung cấp ba equalizer với số lượng band khác nhau, được thể hiện trong tiêu đề (lần lượt là 6, 10 và 21 band).

Filter
~~~~~~

Một "filter" kiểm soát gain của các tần số thông qua *cutoff* được dùng làm ngưỡng tần số. Nó khác equalizer ở chỗ sử dụng các "shape" khác nhau để kiểm soát tần số; nghĩa là gain của các tần số sẽ được điều chỉnh tùy theo chúng thấp hơn, cao hơn, tại hoặc bên ngoài điểm cutoff, dựa trên loại filter. Filter có thể giúp tạo khoảng trống cho từng âm thanh và tạo ra các hiệu ứng thú vị.

.. note::

  Hiệu ứng âm thanh này là lớp mà mọi filter khác kế thừa. Không nên sử dụng trực tiếp.

.. _doc_hard_limiter:

HardLimiter
~~~~~~~~~~~

Một "limiter" không cho phép tín hiệu âm thanh vượt quá mức ngưỡng âm lượng nhất định. Hard limiter dự đoán các đỉnh âm lượng và áp dụng giảm gain một cách mượt mà khi âm lượng vượt qua mức ngưỡng ceiling. Nó hoạt động tương tự compressor, nhưng được thiết kế để hoàn toàn không cho âm lượng vượt qua một mức nhất định. Thêm limiter làm hiệu ứng cuối cùng của Master bus là một thực hành tốt, vì nó cung cấp biện pháp bảo vệ đơn giản chống clipping. Nếu muốn clipping, hãy cân nhắc sử dụng hiệu ứng :ref:`distortion <doc_distortion>` ở chế độ clip.

HighPassFilter
~~~~~~~~~~~~~~

Bộ lọc "high-pass" làm suy giảm các tần số thấp hơn điểm *cutoff* và cho phép các tần số cao hơn đi qua không thay đổi. Có thể sử dụng bộ lọc này để loại bỏ nội dung bass của tín hiệu, khiến âm thanh trở nên "mỏng" hơn.

HighShelfFilter
~~~~~~~~~~~~~~~

Bộ lọc "high-shelf" kiểm soát gain của mọi tần số cao hơn điểm *cutoff*. Có thể sử dụng bộ lọc này để tăng hoặc giảm độ rõ của âm thanh.

Limiter
~~~~~~~

.. note::

  Đây là hiệu ứng limiter cũ và nên sử dụng limiter mới
  :ref:`hard limiter <doc_hard_limiter>` effect instead. This effect is kept to
  để duy trì khả năng tương thích; tuy nhiên, nó nên được xem là đã lỗi thời.

Dưới đây là ví dụ về cách hiệu ứng này hoạt động: nếu ceiling được đặt ở -12 dB và threshold là 0 dB, mọi sample đi qua sẽ bị giảm 12 dB. Điều này thay đổi waveform của âm thanh và tạo ra distortion.

LowPassFilter
~~~~~~~~~~~~~

Bộ lọc "low-pass" làm suy giảm các tần số cao hơn điểm *cutoff* và cho phép các tần số thấp hơn đi qua không thay đổi. Có thể sử dụng low-pass filter để mô phỏng âm thanh "bị nghẹt", chẳng hạn như âm thanh dưới nước, âm thanh bị tường chặn hoặc âm thanh ở xa.

LowShelfFilter
~~~~~~~~~~~~~~

Bộ lọc "low-shelf" kiểm soát gain của mọi tần số thấp hơn điểm *cutoff*. Có thể sử dụng bộ lọc này để điều chỉnh "độ mạnh" của âm thanh bằng cách tăng hoặc giảm gain của dải bass.

.. _doc_notch_filter:

NotchFilter
~~~~~~~~~~~

Bộ lọc "notch" làm suy giảm các tần số tại điểm *cutoff* và cho phép các tần số bên ngoài điểm đó đi qua không thay đổi. Nó đối lập với
:ref:`band-pass filter <doc_band_pass_filter>`. This filter can be used to give
tạo thêm khoảng trống cho các âm thanh khác phát ở điểm cutoff. Do mức độ suy giảm tần số lớn, nó cũng có thể được dùng để loại bỏ hoàn toàn những tần số rất cụ thể và không mong muốn.

Panner
~~~~~~

Di chuyển âm thanh sang trái hoặc phải. Bạn nên sử dụng tai nghe khi cấu hình hiệu ứng này.

.. note::

  Hiệu ứng này có thể không cần thiết khi
  :ref:`AudioStreamPlayer2D <class_AudioStreamPlayer2D>` and
  :ref:`AudioStreamPlayer3D <class_AudioStreamPlayer3D>`, since they handle
  panning tự động.

Phaser
~~~~~~

Hiệu ứng "phaser" tạo ra một bản sao lệch pha rồi trộn lại với bản gốc. Sau đó, bản sao được điều biến bởi một LFO (bộ dao động tần số thấp), khiến một số tần số triệt tiêu lẫn nhau theo những cách thú vị. Kết quả là một loạt đỉnh và đáy quét qua toàn bộ phổ tần. Hiệu ứng này có thể được dùng để tạo ra các hiệu ứng khoa học viễn tưởng hoặc giọng nói giống Darth Vader.

PitchShift
~~~~~~~~~~

Cho phép điều chỉnh cao độ của tín hiệu một cách độc lập với tốc độ của tín hiệu. Tất cả các tần số có thể được tăng hoặc giảm với ảnh hưởng tối thiểu đến các *transient*. Hiệu ứng này hữu ích khi tạo ra những giọng nói cao hoặc trầm bất thường. Lưu ý rằng việc thay đổi cao độ có thể nghe không tự nhiên nếu đẩy ra ngoài một khoảng hẹp.

Record
~~~~~~

Lưu dữ liệu âm thanh vào một :ref:`AudioStreamWAV <class_AudioStreamWAV>`. Một ví dụ sử dụng hiệu ứng này là ghi âm đầu vào từ microphone và lưu dưới dạng tệp WAV.

.. _doc_reverb:

Reverb
~~~~~~

Hiệu ứng "reverb" liên tục phát lại một bản sao của âm thanh đầu vào; bản sao này suy giảm theo thời gian và tạo ra hiệu ứng tiếng vọng mờ (hay "reverberation"). Reverb rất phù hợp để mô phỏng âm thanh trong nhiều loại không gian khác nhau, từ những căn phòng nhỏ đến các hang động lớn. Hiệu ứng này tương tự :ref:`delay <doc_delay>`, nhưng có âm thanh ít mờ hơn. Sử dụng reverb cùng với delay có thể tạo ra môi trường âm thanh rất tự nhiên.

Reverb thường được xuất ra từ :ref:`Area3Ds <class_Area3D>` (xem :ref:`Reverb buses <doc_audio_streams_reverb_buses>`).

SpectrumAnalyzer
~~~~~~~~~~~~~~~~

Biểu diễn biên độ của tín hiệu âm thanh trong các dải tần được chỉ định. Tính năng này thường được dùng để trực quan hóa âm thanh theo thời gian thực, chẳng hạn như spectrogram. Trực quan hóa giọng nói có thể là một cách hiệu quả để thu hút sự chú ý đến chúng mà không cần tăng âm lượng. Hiệu ứng này không làm thay đổi âm thanh.

.. note::

  Truy cập
  :ref:`AudioEffectSpectrumAnalyzerInstance <class_AudioEffectSpectrumAnalyzerInstance>`
  là cần thiết để sử dụng hiệu ứng này. Bạn có thể tìm thấy một dự án demo sử dụng tính năng này `here <https://github.com/godotengine/godot-demo-projects/tree/master/audio/spectrum>`__.

StereoEnhance
~~~~~~~~~~~~~

Điều chỉnh gain của các kênh trái và phải, đồng thời biến âm thanh mono thành stereo thông qua dịch pha. Tính năng này có thể được dùng để mở rộng hoặc thu hẹp âm thanh. Bạn nên sử dụng tai nghe khi cấu hình hiệu ứng này.
