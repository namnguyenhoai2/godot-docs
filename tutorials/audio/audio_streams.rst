:article_outdated: True

.. _doc_audio_streams:

Luồng âm thanh
==============

Giới thiệu
----------

Như bạn có thể đã đọc trong :ref:`doc_audio_buses`, âm thanh được gửi đến từng bus thông qua một node AudioStreamPlayer. Có nhiều loại AudioStreamPlayer khác nhau. Mỗi loại sẽ tải một AudioStream và phát lại nó.

AudioStream
-----------

AudioStream là một đối tượng trừu tượng phát ra âm thanh. Âm thanh có thể đến từ nhiều nơi, nhưng thường được tải từ filesystem nhất. Các tệp âm thanh có thể được tải dưới dạng AudioStream và đặt bên trong một AudioStreamPlayer. Bạn có thể tìm thông tin về các định dạng được hỗ trợ và điểm khác biệt trong :ref:`doc_importing_audio_samples`.

Có các loại AudioStream khác, chẳng hạn như :ref:`AudioStreamRandomizer<class_AudioStreamRandomizer>`. Loại này chọn một audio stream khác từ danh sách các stream mỗi lần được phát lại, đồng thời áp dụng thay đổi ngẫu nhiên về cao độ và âm lượng. Điều này hữu ích để tạo sự đa dạng cho những âm thanh được phát lại thường xuyên.

AudioStreamPlayer
-----------------

.. image:: img/audio_stream_player.webp

Đây là stream player tiêu chuẩn, không có vị trí. Nó có thể phát đến bất kỳ bus nào. Trong các thiết lập âm thanh 5.1, nó có thể gửi âm thanh đến bản trộn stereo hoặc các loa phía trước.

.. CẬP NHẬT: Thử nghiệm. Khi Playback Type không còn là tính năng thử nghiệm, hãy cập nhật .. đoạn này.

Playback Type là một thiết lập thử nghiệm và có thể thay đổi trong các phiên bản Godot tương lai. Thiết lập này tồn tại để các bản export Web sử dụng các sample dựa trên Web Audio-API thay vì streaming tất cả âm thanh đến trình duyệt, không giống như hầu hết các nền tảng. Điều này ngăn âm thanh bị méo trong các bản export Web đơn luồng. Theo mặc định, chỉ nền tảng Web sử dụng sample. Không khuyến nghị thay đổi thiết lập này, trừ khi bạn có lý do cụ thể. Bạn có thể thay đổi playback type mặc định cho web và các nền tảng khác trong project settings, tại **Audio > General** (phải bật các thiết lập nâng cao để thấy thiết lập này).

AudioStreamPlayer2D
-------------------

.. image:: img/audio_stream_2d.webp

Đây là một biến thể của AudioStreamPlayer, nhưng phát ra âm thanh trong môi trường có vị trí 2D. Khi ở gần phía bên trái màn hình, âm thanh sẽ được pan sang trái. Khi ở gần phía bên phải, âm thanh sẽ được pan sang phải.

.. note::

    Có thể sử dụng Area2D để chuyển hướng âm thanh từ bất kỳ AudioStreamPlayer2D nào nằm bên trong nó đến các bus cụ thể. Điều này cho phép tạo các bus có reverb hoặc chất lượng âm thanh khác nhau để xử lý hành động diễn ra tại một phần cụ thể trong thế giới game.

.. image:: img/audio_stream_2d_area.webp

AudioStreamPlayer3D
-------------------

.. image:: img/audio_stream_3d.webp

Đây là một biến thể của AudioStreamPlayer, nhưng phát ra âm thanh trong môi trường có vị trí 3D. Tùy thuộc vào vị trí của player so với màn hình, nó có thể định vị âm thanh ở dạng stereo, 5.1 hoặc 7.1, tùy theo thiết lập âm thanh đã chọn.

Tương tự AudioStreamPlayer2D, Area3D có thể chuyển hướng âm thanh đến một audio bus.

.. image:: img/audio_stream_3d_area.webp

Không giống như phiên bản 2D, phiên bản 3D của AudioStreamPlayer có thêm một số tùy chọn nâng cao:

.. _doc_audio_streams_reverb_buses:

Các bus reverb
~~~~~~~~~~~~~~

.. warning::

    Tính năng này không được hỗ trợ trên nền tảng web nếu playback mode của AudioStreamPlayer được đặt thành **Sample**, đây là giá trị mặc định. Tính năng này chỉ hoạt động khi playback mode được đặt thành **Stream**, với cái giá là latency tăng nếu không bật thread.

    Xem :ref:`Audio playback in the Exporting for the Web documentation <doc_exporting_for_web_audio_playback>` để biết chi tiết.

Godot cho phép các audio stream 3D đi vào một node Area3D cụ thể gửi âm thanh dry và wet đến các bus riêng biệt. Điều này hữu ích khi bạn có nhiều cấu hình reverb cho các loại phòng khác nhau. Để thực hiện, hãy bật loại reverb này trong phần **Reverb Bus** thuộc các thuộc tính của Area3D:

.. image:: img/audio_stream_reverb_bus.webp

Đồng thời, một bus layout đặc biệt được tạo, trong đó mỗi Area3D nhận thông tin reverb từ từng Area3D. Cần tạo và cấu hình một hiệu ứng Reverb trong mỗi bus reverb để hoàn tất thiết lập cho hiệu ứng mong muốn:

.. image:: img/audio_stream_reverb_bus2.webp

Phần **Reverb Bus** của Area3D cũng có một tham số tên là **Uniformity**. Một số loại phòng phản xạ âm thanh nhiều hơn các loại khác (chẳng hạn như nhà kho), vì vậy âm vang có thể được nghe gần như đồng đều khắp phòng dù nguồn âm thanh có thể ở rất xa. Việc điều chỉnh tham số này có thể mô phỏng hiệu ứng đó.

Doppler
~~~~~~~

.. warning::

    Tính năng này không được hỗ trợ trên nền tảng web nếu playback mode của AudioStreamPlayer được đặt thành **Sample**, đây là giá trị mặc định. Tính năng này chỉ hoạt động khi playback mode được đặt thành **Stream**, với cái giá là latency tăng nếu không bật thread.

    Xem :ref:`Audio playback in the Exporting for the Web documentation <doc_exporting_for_web_audio_playback>` để biết chi tiết.

Khi vận tốc tương đối giữa emitter và listener thay đổi, điều này được cảm nhận như sự tăng hoặc giảm cao độ của âm thanh được phát ra. Godot có thể theo dõi các thay đổi vận tốc trong các node AudioStreamPlayer3D và Camera. Cả hai node đều có thuộc tính này, nhưng phải bật thủ công:

.. image:: img/audio_stream_doppler.webp

Bật tính năng này bằng cách đặt nó tùy theo cách các đối tượng sẽ được di chuyển: sử dụng **Idle** cho các đối tượng được di chuyển bằng ``_process``, hoặc **Physics** cho các đối tượng được di chuyển bằng ``_physics_process``. Việc theo dõi sẽ diễn ra tự động.
