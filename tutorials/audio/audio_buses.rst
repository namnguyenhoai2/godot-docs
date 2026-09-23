.. _doc_audio_buses:

Bus âm thanh
============

Giới thiệu
----------

Mã xử lý âm thanh của Godot được viết với game làm trọng tâm, nhằm đạt được sự cân bằng tối ưu giữa hiệu năng và chất lượng âm thanh.

Audio engine của Godot cho phép tạo bất kỳ số lượng bus âm thanh nào và thêm bất kỳ số lượng bộ xử lý hiệu ứng nào vào mỗi bus. Chỉ phần cứng của thiết bị chạy game mới giới hạn số lượng bus và hiệu ứng có thể sử dụng trước khi hiệu năng bắt đầu suy giảm.

Thang decibel
-------------

Giao diện âm thanh của Godot được thiết kế để đáp ứng kỳ vọng của các chuyên gia thiết kế âm thanh. Vì vậy, giao diện này chủ yếu sử dụng thang decibel.

Nếu chưa quen với thang này, bạn có thể hiểu qua một vài thông tin sau:

- Thang decibel (dB) là một thang tương đối. Thang này biểu diễn tỷ lệ công suất âm thanh bằng 20 lần logarit cơ số 10 của tỷ lệ (20 × log\ :sub:`10`\ (P/P\ :sub:`0`\ )).
- Cứ mỗi 6 dB, biên độ âm thanh sẽ tăng gấp đôi hoặc giảm một nửa. 12 dB biểu thị hệ số 4, 18 dB là hệ số 8, 20 dB là hệ số 10, 40 dB là hệ số 100, v.v.
- Vì đây là thang logarit nên không thể biểu diễn giá trị 0 thực sự (không có âm thanh).
- 0 dB là biên độ tối đa có thể có trong một hệ thống âm thanh kỹ thuật số. Đây không phải là giới hạn của con người mà là giới hạn của phần cứng âm thanh. Âm thanh có biên độ quá cao, không thể được biểu diễn chính xác dưới 0 dB, sẽ tạo ra một dạng méo gọi là *clipping*.
- Để tránh clipping, bạn nên sắp xếp bản phối âm sao cho đầu ra của *master bus* (sẽ nói thêm về phần này sau) không bao giờ vượt quá 0 dB.
- Cứ mỗi 6 dB dưới giới hạn 0 dB, năng lượng âm thanh sẽ *giảm một nửa*. Điều đó có nghĩa là âm lượng ở -6 dB bằng một nửa âm lượng ở 0 dB. -12 dB bằng một nửa âm lượng ở -6 dB, v.v.
- Khi làm việc với decibel, âm thanh được xem là không còn nghe được trong khoảng từ -60 dB đến -80 dB. Vì vậy, phạm vi làm việc của bạn nhìn chung nằm trong khoảng từ -60 dB đến 0 dB.

Ban đầu có thể hơi khó làm quen, nhưng về lâu dài cách này dễ sử dụng hơn và giúp bạn giao tiếp tốt hơn với các chuyên gia âm thanh.

Bus âm thanh
------------

Bạn có thể tìm thấy các bus âm thanh trong panel phía dưới của trình chỉnh sửa Godot:

.. image:: img/audio_buses1.webp

Một *audio bus* (còn gọi là *audio channel*) có thể được xem là nơi âm thanh đi qua trên đường đến thiết bị phát qua loa. Dữ liệu âm thanh có thể được một bus âm thanh *biến đổi* và *định tuyến lại*. Một bus âm thanh có đồng hồ VU (các thanh sáng lên khi phát âm thanh), cho biết biên độ của tín hiệu đi qua.

Bus ngoài cùng bên trái là *master bus*. Bus này xuất bản phối âm ra loa, vì vậy như đã đề cập trong phần *Thang decibel* ở trên, hãy đảm bảo mức bản phối âm của bạn không chạm tới 0 dB trên bus này. Các bus âm thanh còn lại có thể được định tuyến linh hoạt. Sau khi biến đổi âm thanh, chúng gửi âm thanh đó đến một bus khác ở bên trái. Có thể chỉ định bus đích cho từng bus âm thanh không phải master. Việc định tuyến luôn truyền âm thanh từ các bus bên phải đến các bus ở xa hơn về bên trái. Điều này tránh các vòng lặp định tuyến vô hạn.

.. image:: img/audio_buses2.webp

Trong hình trên, đầu ra của *Bus 2* đã được định tuyến đến bus *Master*.

Phát âm thanh qua một bus
-------------------------

Để thử truyền âm thanh đến một bus, hãy tạo một node AudioStreamPlayer, tải một AudioStream và chọn bus đích để phát:

.. image:: img/audio_buses3.webp

Cuối cùng, chuyển thuộc tính **Playing** sang **On** và âm thanh sẽ bắt đầu phát.

.. seealso::

    Bạn cũng có thể muốn đọc về :ref:`doc_audio_streams` ngay bây giờ.

Thêm hiệu ứng
-------------

.. warning::

    Tính năng này không được hỗ trợ trên nền tảng web nếu chế độ phát của AudioStreamPlayer được đặt thành **Sample**, đây là chế độ mặc định. Tính năng này chỉ hoạt động nếu chế độ phát được đặt thành **Stream**, với cái giá là độ trễ tăng lên nếu các thread chưa được bật.

    Xem :ref:`Audio playback in the Exporting for the Web documentation <doc_exporting_for_web_audio_playback>` để biết chi tiết.

Các bus âm thanh có thể chứa đủ loại hiệu ứng. Những hiệu ứng này biến đổi âm thanh theo cách này hay cách khác và được áp dụng theo thứ tự.

.. image:: img/audio_buses4.webp

Để biết mỗi hiệu ứng thực hiện chức năng gì, hãy xem :ref:`doc_audio_effects`.

Tự động vô hiệu hóa bus
-----------------------

Bạn không cần tự vô hiệu hóa các bus khi không sử dụng. Godot phát hiện bus đã im lặng trong vài giây và vô hiệu hóa bus đó (bao gồm tất cả hiệu ứng).

.. figure:: img/audio_buses5.webp

   Các bus bị vô hiệu hóa có đồng hồ VU màu xanh lam đậm thay vì đồng hồ màu đỏ-xanh lá.

Sắp xếp lại bus
---------------

Stream Player sử dụng tên bus để nhận diện bus, cho phép thêm, xóa và di chuyển các bus mà vẫn giữ được tham chiếu đến chúng. Tuy nhiên, nếu một bus được đổi tên, tham chiếu sẽ bị mất và Stream Player sẽ xuất ra Master. Hệ thống này được chọn vì việc sắp xếp lại bus phổ biến hơn việc đổi tên chúng.

Bố cục bus mặc định
-------------------

Bố cục bus mặc định được tự động lưu vào tệp ``res://default_bus_layout.tres``. Bạn có thể lưu các cách sắp xếp bus tùy chỉnh và tải chúng từ đĩa.
