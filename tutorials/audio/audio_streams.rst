:article_outdated: True

.. _doc_audio_streams:

Các luồng âm thanh
==================

Giới thiệu
----------

Như bạn có thể đã đọc trong :ref:`doc_audio_buses`, âm thanh được gửi đến từng bus thông qua một node AudioStreamPlayer. Có nhiều loại AudioStreamPlayer khác nhau. Mỗi loại tải một AudioStream và phát lại nó.

AudioStream
-----------

Một luồng âm thanh là một đối tượng trừu tượng phát ra âm thanh. Âm thanh có thể đến từ nhiều nguồn, nhưng thường được tải từ hệ thống tệp nhất. Các tệp âm thanh có thể được tải dưới dạng AudioStream và đặt bên trong một AudioStreamPlayer. Bạn có thể tìm thông tin về các định dạng được hỗ trợ và sự khác biệt trong :ref:`doc_importing_audio_samples`.

Có các loại AudioStream khác, chẳng hạn như :ref:`AudioStreamRandomizer<class_AudioStreamRandomizer>`. Loại này chọn một luồng âm thanh khác trong danh sách các luồng mỗi khi được phát lại, đồng thời áp dụng thay đổi ngẫu nhiên về cao độ và âm lượng. Điều này hữu ích để tạo sự đa dạng cho những âm thanh thường xuyên được phát lại.

AudioStreamPlayer
-----------------

.. image:: img/audio_stream_player.webp

Đây là trình phát luồng tiêu chuẩn, không có vị trí. Nó có thể phát đến bất kỳ bus nào. Trong các thiết lập âm thanh 5.1, nó có thể gửi âm thanh đến bản trộn stereo hoặc các loa phía trước.

.. UPDATE: Experimental. When Playback Type is no longer experimental, update
.. this paragraph.

Playback Type là một thiết lập thử nghiệm và có thể thay đổi trong các phiên bản Godot tương lai. Thiết lập này tồn tại để các bản export Web sử dụng các sample dựa trên Web Audio-API thay vì stream toàn bộ âm thanh đến trình duyệt, không giống như hầu hết các nền tảng. Điều này ngăn âm thanh bị méo trong các bản export Web đơn luồng. Theo mặc định, chỉ nền tảng Web sử dụng sample. Bạn không nên thay đổi thiết lập này trừ khi có lý do cụ thể. Bạn có thể thay đổi playback type mặc định cho web và các nền tảng khác trong phần cài đặt dự án tại **Audio > General** (phải bật cài đặt nâng cao để thấy thiết lập này).

AudioStreamPlayer2D
-------------------

.. image:: img/audio_stream_2d.webp

Đây là một biến thể của AudioStreamPlayer, nhưng phát ra âm thanh trong môi trường có vị trí 2D. Khi ở gần phía bên trái màn hình, âm thanh sẽ được pan sang trái. Khi ở gần phía bên phải, âm thanh sẽ được pan sang phải.

.. note::

    Có thể sử dụng Area2D để chuyển hướng âm thanh từ bất kỳ AudioStreamPlayer2D nào nằm bên trong chúng đến các bus cụ thể. Điều này cho phép tạo các bus có reverb hoặc chất lượng âm thanh khác nhau để xử lý hành động diễn ra ở một khu vực cụ thể trong thế giới game.

.. image:: img/audio_stream_2d_area.webp

AudioStreamPlayer3D
-------------------

.. image:: img/audio_stream_3d.webp

Đây là một biến thể của AudioStreamPlayer, nhưng phát ra âm thanh trong môi trường có vị trí 3D. Tùy vào vị trí của player so với màn hình, nó có thể định vị âm thanh theo stereo, 5.1 hoặc 7.1, tùy thuộc vào thiết lập âm thanh đã chọn.

Tương tự AudioStreamPlayer2D, một Area3D có thể chuyển hướng âm thanh đến một audio bus.

.. image:: img/audio_stream_3d_area.webp

Không giống như phiên bản 2D, phiên bản 3D của AudioStreamPlayer có thêm một số tùy chọn nâng cao:

.. _doc_audio_streams_reverb_buses:

Các bus reverb
~~~~~~~~~~~~~~

.. warning::

    Tính năng này không được hỗ trợ trên nền tảng web nếu playback mode của AudioStreamPlayer được đặt thành **Sample**, đây là giá trị mặc định. Tính năng này chỉ hoạt động khi playback mode được đặt thành **Stream**, với cái giá là độ trễ tăng lên nếu không bật thread.

    Xem :ref:`Audio playback in the Exporting for the Web documentation <doc_exporting_for_web_audio_playback>` để biết chi tiết.

Godot cho phép các luồng âm thanh 3D đi vào một node Area3D cụ thể gửi âm thanh khô và ướt đến các bus riêng biệt. Điều này hữu ích khi bạn có nhiều cấu hình reverb cho các loại phòng khác nhau. Để thực hiện, hãy bật loại reverb này trong phần **Reverb Bus** thuộc các thuộc tính của Area3D:

.. image:: img/audio_stream_reverb_bus.webp

Đồng thời, một bố cục bus đặc biệt được tạo, trong đó mỗi Area3D nhận thông tin reverb từ từng Area3D. Cần tạo và cấu hình một hiệu ứng Reverb trong mỗi bus reverb để hoàn tất thiết lập cho hiệu ứng mong muốn:

.. image:: img/audio_stream_reverb_bus2.webp

Phần **Reverb Bus** của Area3D cũng có một tham số tên là **Uniformity**. Một số loại phòng phản xạ âm thanh nhiều hơn những loại khác (chẳng hạn như nhà kho), vì vậy có thể nghe thấy tiếng vang gần như đồng đều khắp phòng dù nguồn âm thanh có thể ở rất xa. Điều chỉnh tham số này có thể mô phỏng hiệu ứng đó.

Doppler
~~~~~~~

.. warning::

    Tính năng này không được hỗ trợ trên nền tảng web nếu playback mode của AudioStreamPlayer được đặt thành **Sample**, đây là giá trị mặc định. Tính năng này chỉ hoạt động khi playback mode được đặt thành **Stream**, với cái giá là độ trễ tăng lên nếu không bật thread.

    Xem :ref:`Audio playback in the Exporting for the Web documentation <doc_exporting_for_web_audio_playback>` để biết chi tiết.

Khi vận tốc tương đối giữa nguồn phát và bộ nghe thay đổi, điều này được cảm nhận như sự tăng hoặc giảm cao độ của âm thanh phát ra. Godot có thể theo dõi các thay đổi vận tốc trong các node AudioStreamPlayer3D và Camera. Cả hai node đều có thuộc tính này, nhưng phải bật thủ công:

.. image:: img/audio_stream_doppler.webp

Bật tính năng này bằng cách đặt giá trị tùy thuộc vào cách các đối tượng được di chuyển: dùng **Idle** cho các đối tượng được di chuyển bằng ``_process``, hoặc **Physics** cho các đối tượng được di chuyển bằng ``_physics_process``. Việc theo dõi sẽ diễn ra tự động.
