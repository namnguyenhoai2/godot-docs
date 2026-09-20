.. _doc_audio_buses:

Các bus âm thanh
================

Giới thiệu
----------

Mã xử lý âm thanh của Godot được viết dành cho game, nhằm đạt được sự cân bằng tối ưu giữa hiệu năng và chất lượng âm thanh.

Audio engine của Godot cho phép tạo bất kỳ số lượng bus âm thanh nào và thêm bất kỳ số lượng effect processor nào vào mỗi bus. Chỉ phần cứng của thiết bị chạy game mới giới hạn số lượng bus và effect có thể sử dụng trước khi hiệu năng bắt đầu suy giảm.

Thang decibel
-------------

Giao diện âm thanh của Godot được thiết kế để đáp ứng kỳ vọng của các chuyên gia sound design. Vì mục đích này, giao diện chủ yếu sử dụng thang decibel.

Đối với những người chưa quen với thang này, có thể giải thích bằng một vài điểm sau:

- Thang decibel (dB) là một thang tương đối. Nó biểu thị tỷ lệ công suất âm thanh bằng cách sử dụng 20 lần logarit cơ số 10 của tỷ lệ (20 × log\ :sub:`10`\ (P/P\ :sub:`0`\ )). - Với mỗi 6 dB, biên độ âm thanh tăng gấp đôi hoặc giảm một nửa. 12 dB biểu thị hệ số 4, 18 dB là hệ số 8, 20 dB là hệ số 10, 40 dB là hệ số 100, v.v. - Vì đây là thang logarit nên không thể biểu thị giá trị 0 thực sự (không có âm thanh). - 0 dB là biên độ tối đa có thể có trong một hệ thống âm thanh kỹ thuật số. Đây không phải là giới hạn của con người mà là giới hạn của phần cứng âm thanh. Âm thanh có biên độ quá cao để được biểu thị chính xác dưới 0 dB sẽ tạo ra một dạng méo gọi là *clipping*. - Để tránh clipping, bản mix âm thanh của bạn nên được sắp xếp sao cho đầu ra của *master bus* (sẽ nói thêm về bus này sau) không bao giờ vượt quá 0 dB. - Cứ mỗi 6 dB dưới giới hạn 0 dB, năng lượng âm thanh lại *giảm một nửa*. Điều đó có nghĩa là âm lượng ở -6 dB chỉ bằng một nửa 0 dB. -12 dB chỉ bằng một nửa -6 dB, v.v. - Khi làm việc với decibel, âm thanh được xem là không còn nghe được trong khoảng từ -60 dB đến -80 dB. Vì vậy, phạm vi làm việc của bạn thường nằm trong khoảng từ -60 dB đến 0 dB.

Có thể bạn sẽ cần một chút thời gian để làm quen, nhưng về sau cách này sẽ dễ sử dụng hơn và giúp bạn giao tiếp tốt hơn với các chuyên gia âm thanh.

Các bus âm thanh
----------------

Bạn có thể tìm thấy các bus âm thanh trong panel phía dưới của Godot editor:

.. image:: img/audio_buses1.webp

Một *audio bus* (còn gọi là *audio channel*) có thể được xem là nơi âm thanh đi qua trên đường đến quá trình phát bằng loa của thiết bị. Dữ liệu âm thanh có thể được *sửa đổi* và *định tuyến lại* bởi một audio bus. Một audio bus có VU meter (các thanh sáng lên khi âm thanh được phát), cho biết biên độ của tín hiệu đi qua.

Bus ngoài cùng bên trái là *master bus*. Bus này xuất bản mix đến loa, vì vậy, như đã đề cập trong phần *Thang decibel* ở trên, hãy đảm bảo mức mix của bạn trong bus này không đạt đến 0 dB. Các bus âm thanh còn lại có thể được định tuyến linh hoạt. Sau khi sửa đổi âm thanh, chúng sẽ gửi âm thanh đó đến một bus khác ở bên trái. Có thể chỉ định bus đích cho từng audio bus không phải master. Việc định tuyến luôn truyền âm thanh từ các bus bên phải đến các bus xa hơn về bên trái. Điều này tránh các vòng lặp định tuyến vô hạn.

.. image:: img/audio_buses2.webp

Trong hình trên, đầu ra của *Bus 2* đã được định tuyến đến bus *Master*.

Phát âm thanh qua một bus
-------------------------

Để kiểm tra việc truyền âm thanh đến một bus, hãy tạo một node AudioStreamPlayer, tải một AudioStream và chọn bus đích để phát:

.. image:: img/audio_buses3.webp

Cuối cùng, chuyển thuộc tính **Playing** sang **On** để âm thanh bắt đầu phát.

.. seealso::

    Bạn cũng có thể quan tâm đến việc đọc về :ref:`doc_audio_streams` ngay bây giờ.

Thêm effect
-----------

.. warning::

    Tính năng này không được hỗ trợ trên nền tảng web nếu playback mode của AudioStreamPlayer được đặt thành **Sample**, là giá trị mặc định. Tính năng này chỉ hoạt động khi playback mode được đặt thành **Stream**, với cái giá là latency tăng nếu các thread chưa được bật.

    Xem :ref:`Audio playback in the Exporting for the Web documentation <doc_exporting_for_web_audio_playback>` để biết chi tiết.

Các bus âm thanh có thể chứa đủ loại effect. Những effect này sửa đổi âm thanh theo cách này hay cách khác và được áp dụng theo thứ tự.

.. image:: img/audio_buses4.webp

Để biết từng effect thực hiện chức năng gì, hãy xem :ref:`doc_audio_effects`.

Tự động vô hiệu hóa bus
-----------------------

Bạn không cần phải vô hiệu hóa bus theo cách thủ công khi không sử dụng. Godot phát hiện bus đã im lặng trong vài giây và vô hiệu hóa bus đó (bao gồm tất cả effect).

.. figure:: img/audio_buses5.webp

   Disabled buses have a dark blue VU meter instead of a red-green one.

Sắp xếp lại bus
---------------

Stream Player sử dụng tên bus để nhận diện một bus, cho phép thêm, xóa và di chuyển các bus mà vẫn giữ nguyên tham chiếu đến chúng. Tuy nhiên, nếu một bus được đổi tên, tham chiếu sẽ bị mất và Stream Player sẽ xuất âm thanh đến Master. Hệ thống này được chọn vì việc sắp xếp lại bus phổ biến hơn việc đổi tên chúng.

Bố cục bus mặc định
-------------------

Bố cục bus mặc định được tự động lưu vào tệp ``res://default_bus_layout.tres``. Bạn có thể lưu các cách sắp xếp bus tùy chỉnh vào ổ đĩa và tải chúng từ đó.
