.. _doc_audio_effects:

Hiệu ứng âm thanh
=================

Godot bao gồm một số hiệu ứng âm thanh có thể được thêm vào một audio bus để thay đổi mọi âm thanh đi qua bus đó.

.. image:: img/audio_buses4.webp

Hiểu cách hoạt động của từng hiệu ứng có thể khó, vì vậy đừng nản lòng nếu bạn phải tra cứu! Nếu bạn mới làm quen với âm thanh, hiểu các hiệu ứng thiết yếu có thể giúp ích trong hầu hết trường hợp! Đó là:

- Equalizer & Filter
- Limiter
- Delay & Reverb

Hãy thử từng hiệu ứng để cảm nhận cách chúng thay đổi âm thanh.

.. note::

  :ref:`AudioSample <class_AudioSample>` không hỗ trợ các hiệu ứng này.

Sau đây là mô tả ngắn về các hiệu ứng hiện có:

Amplify
~~~~~~~

Thay đổi âm lượng của âm thanh. Tuy nhiên, cần thận trọng: đặt mức âm lượng quá cao có thể khiến âm thanh bị clip kỹ thuật số, tạo ra những tiếng lách tách và bụp khó chịu. Hãy cân nhắc sử dụng một
:ref:`hard limiter <doc_hard_limiter>` hoặc :ref:`compressor <doc_compressor>` để ngăn clipping, hoặc :ref:`distortion <doc_distortion>` ở chế độ clip nếu muốn clipping ở mức 0 dB hoặc thấp hơn.

.. _doc_band_limit_filter:

BandLimitFilter
~~~~~~~~~~~~~~~

Bộ lọc "band-limit" làm suy giảm các tần số tại điểm *cutoff*, đồng thời cho phép các tần số bên ngoài điểm đó đi qua không thay đổi. Nó tương tự :ref:`notch filter <doc_notch_filter>`, nhưng yếu hơn. Đây là đối lập của :ref:`band-pass filter <doc_band_pass_filter>`. Bộ lọc này có thể được dùng để tạo thêm không gian cho các âm thanh khác phát ở điểm cutoff.

.. _doc_band_pass_filter:

BandPassFilter
~~~~~~~~~~~~~~

Bộ lọc "band-pass" cho phép các tần số tại điểm *cutoff* đi qua không thay đổi, đồng thời làm suy giảm các tần số bên ngoài điểm đó. Đây là đối lập của
:ref:`band-limit filter <doc_band_limit_filter>` và
:ref:`notch filter <doc_notch_filter>`. Bộ lọc này có thể được dùng để mô phỏng âm thanh truyền qua đường dây điện thoại cũ hoặc loa phóng thanh. Điều biến điểm cutoff có thể mô phỏng âm thanh của bàn đạp wah-wah cho guitar, chẳng hạn tiếng guitar trong *Voodoo Child (Slight Return)* của Jimi Hendrix.

Capture
~~~~~~~

Sao chép các mẫu âm thanh của audio bus mà hiệu ứng này được gắn vào một ring buffer nội bộ. Tính năng này có thể được dùng để thu thập dữ liệu từ microphone hoặc truyền âm thanh qua mạng theo thời gian thực. Nhìn chung, nó có thể được dùng để lưu trữ dữ liệu âm thanh theo thời gian thực nhằm phát lại, thậm chí tạo hình ảnh trực quan hóa âm thanh theo thời gian thực, chẳng hạn như một oscilloscope. Hiệu ứng này không thay đổi âm thanh.

Chorus
~~~~~~

Hiệu ứng "chorus" nhân đôi một tín hiệu rồi thay đổi rất nhẹ thời điểm và cao độ của từng bản sao, đồng thời điều biến chúng theo thời gian thông qua một LFO (low-frequency oscillator). Các bản sao (còn gọi là "voice") sau đó được trộn lại với tín hiệu gốc, tạo cảm giác âm thanh phát ra từ nhiều nguồn. Trong thực tế, loại hiệu ứng này có trong piano, hợp xướng và các nhóm nhạc cụ. Hiệu ứng này cũng có thể được dùng để mở rộng âm thanh mono và khiến âm thanh kỹ thuật số có chất lượng tự nhiên hoặc analog hơn.

.. _doc_compressor:

Compressor
~~~~~~~~~~

Một "compressor" tự động làm suy giảm (hoặc "duck") âm lượng của tín hiệu đầu vào khi biên độ của nó vượt quá một ngưỡng âm lượng nhất định. Mức suy giảm được áp dụng tỷ lệ thuận với mức độ âm thanh đầu vào vượt ngưỡng. Tham số Ratio của compressor điều khiển mức độ suy giảm. Một trong những công dụng chính của compressor là giảm dải động của các tín hiệu có những phần rất to và rất nhỏ. Giảm dải động của tín hiệu có thể giúp tín hiệu hòa trộn dễ dàng hơn trong một bản mix.

Compressor có nhiều công dụng. Ví dụ:

- Có thể dùng trong Master bus để nén toàn bộ đầu ra trước khi tín hiệu chạm đến ngưỡng trần của limiter, giúp hiệu ứng của limiter tinh tế hơn nhiều.
- Có thể dùng cho các voice clip để đảm bảo chúng có âm lượng đồng đều nhất có thể.
- Có thể được *sidechained* bởi một nguồn âm thanh khác. Điều này có nghĩa là nó có thể giảm âm lượng của một tín hiệu bằng cách sử dụng âm lượng của một audio bus khác để phát hiện ngưỡng. Kỹ thuật này rất phổ biến trong việc mixing game để "duck" âm lượng của nhạc hoặc hiệu ứng âm thanh khi giọng nói trong game hoặc multiplayer cần được nghe rõ hoàn toàn.
- Có thể làm nổi bật *transients* bằng cách sử dụng attack chậm hơn, cho phép các phần lớn hơn đi qua trước khi bị nén. Điều này có thể nhấn mạnh độ "punchy" của các hiệu ứng âm thanh.

.. note::

  Nếu mục tiêu duy nhất của bạn là ngăn tín hiệu vượt quá một biên độ nhất định, :ref:`hard limiter <doc_hard_limiter>` có thể là lựa chọn phù hợp hơn compressor cho mục đích này. Tuy nhiên, áp dụng compression trước limiter vẫn là một cách làm tốt.

.. _doc_delay:

Delay
~~~~~

Hiệu ứng "delay" nhân đôi một tín hiệu và lặp lại nhiều lần, với một khoảng thời gian ngắn giữa mỗi lần lặp (còn gọi là "tap"). Âm lượng của các tap giảm dần theo thời gian. Tất cả tạo ra hiệu ứng tiếng vang. Delay rất phù hợp để mô phỏng không gian âm học của hẻm núi hoặc căn phòng lớn, nơi âm thanh dội lại từ các bề mặt và đến tai người nghe sau một khoảng *delay*. Điều này tương tự
:ref:`reverb <doc_reverb>`, vốn có âm thanh tự nhiên và mờ hơn. Sử dụng delay kết hợp với reverb có thể tạo ra môi trường âm thanh rất tự nhiên.

.. _doc_distortion:

Distortion
~~~~~~~~~~

Hiệu ứng "distortion" thay đổi âm lượng của âm thanh theo cách làm biến đổi waveform, có thể tạo ra âm thanh "gắt" và "sáng".

Sau đây là một số loại distortion mà Godot cung cấp:

- *Clip*: giới hạn âm lượng của âm thanh, khiến âm thanh trở nên gắt.
- *Overdrive*: tạo âm thanh giống bàn đạp distortion cho guitar hoặc loa phóng thanh.
- *Lo-fi*: giảm *bit depth* của tín hiệu, mô phỏng loa cũ.

Mọi loại distortion đều có thể thêm các tần số cao hơn vào âm thanh gốc, giúp âm thanh nổi bật hơn trong một bản mix.

.. warning::

  Hãy thận trọng với lượng distortion được thêm vào, vì nó có thể tạo ra âm thanh rất gắt và lớn.

EQ
~~

Một "equalizer" cho phép bạn kiểm soát gain của các tần số trong toàn bộ phổ âm, thông qua việc sử dụng các "band" đại diện cho những vùng khác nhau của phổ. Equalizer có thể rất cần thiết để tạo ra một bản mix sạch hơn, cho phép nhiều âm thanh phát cùng nhau mà không cạnh tranh tần số. Equalizer trên Master bus có thể hữu ích để làm suy giảm các tần số thấp và cao mà loa của thiết bị không thể tái tạo tốt. Ví dụ, loa điện thoại và máy tính bảng thường không tái tạo tốt các âm thanh tần số thấp, đồng thời có thể khiến limiter hoặc compressor làm suy giảm âm lượng Master nhiều hơn mức cần thiết. Có thể tắt hiệu ứng này khi cắm tai nghe, nhờ đó người dùng có được lợi ích tốt nhất trong cả hai trường hợp.

.. note::

  Hiệu ứng âm thanh này là lớp cơ sở mà mọi equalizer khác kế thừa. Có thể mở rộng nó bằng các script tùy chỉnh để tạo một equalizer với số lượng band tùy chỉnh.

EQ6, EQ10, EQ21
~~~~~~~~~~~~~~~

Godot cung cấp ba bộ equalizer với số lượng dải tần khác nhau, được thể hiện trong tiêu đề (lần lượt là 6, 10 và 21 dải).

Filter
~~~~~~

Một "filter" điều khiển gain của các tần số bằng cách sử dụng *cutoff* làm ngưỡng tần số. Filter khác với equalizer ở chỗ nó sử dụng các "hình dạng" khác nhau để điều khiển tần số; nghĩa là gain của các tần số sẽ được điều chỉnh tùy thuộc vào việc chúng thấp hơn, cao hơn, nằm tại hoặc nằm ngoài điểm cutoff, tùy theo loại filter. Filter có thể giúp tạo không gian cho từng âm thanh và tạo ra các hiệu ứng thú vị.

.. note::

  Hiệu ứng âm thanh này là lớp mà tất cả các filter khác kế thừa. Không nên sử dụng trực tiếp hiệu ứng này.

.. _doc_hard_limiter:

HardLimiter
~~~~~~~~~~~

Một "limiter" ngăn tín hiệu âm thanh vượt quá mức ngưỡng âm lượng đã cho. Hard limiter dự đoán các đỉnh âm lượng và áp dụng giảm gain một cách mượt mà khi âm lượng vượt qua mức ngưỡng trần. Nó hoạt động tương tự compressor, nhưng được thiết kế để hoàn toàn không cho âm lượng vượt qua một mức nhất định. Thêm limiter làm hiệu ứng cuối cùng của bus Master là một thực hành tốt, vì nó cung cấp một biện pháp bảo vệ đơn giản chống clipping. Nếu muốn clipping, hãy cân nhắc sử dụng hiệu ứng :ref:`distortion <doc_distortion>` ở chế độ clip.

HighPassFilter
~~~~~~~~~~~~~~

Filter "high-pass" làm suy giảm các tần số thấp hơn điểm *cutoff* và cho phép các tần số cao hơn đi qua mà không thay đổi. Có thể sử dụng filter này để loại bỏ thành phần bass của tín hiệu, khiến âm thanh trở nên "mỏng" hơn.

HighShelfFilter
~~~~~~~~~~~~~~~

Filter "high-shelf" điều khiển gain của tất cả các tần số cao hơn điểm *cutoff*. Có thể sử dụng filter này để tăng hoặc giảm độ rõ của âm thanh.

Limiter
~~~~~~~

.. note::

  Đây là hiệu ứng limiter cũ và nên sử dụng hiệu ứng mới
  :ref:`hard limiter <doc_hard_limiter>` thay thế. Hiệu ứng này được giữ lại để duy trì khả năng tương thích, tuy nhiên nên xem là đã deprecated.

Ví dụ về cách hiệu ứng này hoạt động: nếu mức trần được đặt thành -12 dB và ngưỡng là 0 dB, tất cả sample đi qua sẽ bị giảm 12 dB. Điều này làm thay đổi waveform của âm thanh và tạo ra distortion.

LowPassFilter
~~~~~~~~~~~~~

Filter "low-pass" làm suy giảm các tần số cao hơn điểm *cutoff* và cho phép các tần số thấp hơn đi qua mà không thay đổi. Có thể sử dụng filter low-pass để mô phỏng âm thanh "bị nghẹt". Ví dụ: âm thanh dưới nước, âm thanh bị tường chắn hoặc âm thanh từ xa.

LowShelfFilter
~~~~~~~~~~~~~~

Filter "low-shelf" điều khiển gain của tất cả các tần số thấp hơn điểm *cutoff*. Có thể sử dụng filter này để điều chỉnh "độ mạnh" của âm thanh bằng cách tăng hoặc giảm gain của dải bass.

.. _doc_notch_filter:

NotchFilter
~~~~~~~~~~~

Filter "notch" làm suy giảm các tần số tại điểm *cutoff* và cho phép các tần số nằm ngoài điểm đó đi qua mà không thay đổi. Đây là điều ngược lại với
:ref:`band-pass filter <doc_band_pass_filter>`. Có thể sử dụng filter này để tạo thêm không gian cho các âm thanh khác phát tại điểm cutoff. Do làm suy giảm tần số mạnh, filter này cũng có thể được sử dụng để loại bỏ hoàn toàn các tần số rất cụ thể và không mong muốn.

Panner
~~~~~~

Di chuyển âm thanh sang trái hoặc phải. Nên sử dụng tai nghe khi cấu hình hiệu ứng này.

.. note::

  Hiệu ứng này có thể không cần thiết với
  :ref:`AudioStreamPlayer2D <class_AudioStreamPlayer2D>` và
  :ref:`AudioStreamPlayer3D <class_AudioStreamPlayer3D>`, vì chúng tự động xử lý việc panning.

Phaser
~~~~~~

Hiệu ứng "phaser" tạo ra một bản sao lệch pha rồi trộn lại với bản gốc. Sau đó, bản sao được điều biến bởi một LFO (bộ dao động tần số thấp), khiến một số tần số triệt tiêu lẫn nhau theo những cách thú vị. Kết quả là một chuỗi các đỉnh và đáy quét qua phổ tần. Có thể sử dụng hiệu ứng này để tạo các hiệu ứng khoa học viễn tưởng hoặc giọng nói giống Darth Vader.

PitchShift
~~~~~~~~~~

Cho phép điều chỉnh cao độ của tín hiệu độc lập với tốc độ của tín hiệu. Có thể tăng hoặc giảm tất cả các tần số với ảnh hưởng tối thiểu đến *transients*. Hiệu ứng này hữu ích để tạo ra giọng nói cao bất thường hoặc trầm sâu. Lưu ý rằng việc thay đổi cao độ có thể tạo âm thanh không tự nhiên khi bị đẩy ra ngoài một khoảng hẹp.

Record
~~~~~~

Lưu dữ liệu âm thanh vào một :ref:`AudioStreamWAV <class_AudioStreamWAV>`. Một ví dụ sử dụng hiệu ứng này là ghi đầu vào từ microphone và lưu dưới dạng tệp WAV.

.. _doc_reverb:

Reverb
~~~~~~

Hiệu ứng "reverb" liên tục phát lại một bản sao của âm thanh đầu vào, bản sao này suy giảm theo thời gian và tạo ra hiệu ứng tiếng vọng mờ (hay "reverberation"). Reverb rất phù hợp để mô phỏng âm thanh trong nhiều loại không gian khác nhau, từ các căn phòng nhỏ đến những hang động lớn. Hiệu ứng này tương tự :ref:`delay <doc_delay>`, nhưng có âm thanh ít mờ hơn. Sử dụng reverb cùng với delay có thể tạo ra môi trường âm thanh rất tự nhiên.

Reverb thường được xuất ra từ :ref:`Area3Ds <class_Area3D>` (xem :ref:`Reverb buses <doc_audio_streams_reverb_buses>`).

SpectrumAnalyzer
~~~~~~~~~~~~~~~~

Vẽ biên độ của tín hiệu âm thanh trong các khoảng tần số được chỉ định. Thông thường, hiệu ứng này được dùng để trực quan hóa âm thanh theo thời gian thực, chẳng hạn như spectrogram. Trực quan hóa giọng nói có thể là một cách hiệu quả để thu hút sự chú ý đến giọng nói mà không cần tăng âm lượng. Hiệu ứng này không làm thay đổi âm thanh.

.. note::

  Accessing
  Cần có :ref:`AudioEffectSpectrumAnalyzerInstance <class_AudioEffectSpectrumAnalyzerInstance>` để sử dụng hiệu ứng này. Bạn có thể tìm thấy một dự án demo sử dụng hiệu ứng này `here <https://github.com/godotengine/godot-demo-projects/tree/master/audio/spectrum>`__.

StereoEnhance
~~~~~~~~~~~~~

Điều chỉnh gain của các kênh trái và phải, đồng thời biến âm thanh mono thành stereo thông qua dịch pha. Có thể sử dụng hiệu ứng này để mở rộng hoặc thu hẹp âm thanh. Nên sử dụng tai nghe khi cấu hình hiệu ứng này.
