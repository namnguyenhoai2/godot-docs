:allow_comments: False

.. _doc_your_first_3d_game:

Trò chơi 3D đầu tiên của bạn
============================

Trong loạt hướng dẫn từng bước này, bạn sẽ tạo trò chơi 3D hoàn chỉnh đầu tiên của mình với Godot. Khi hoàn thành loạt bài, bạn sẽ có một dự án đơn giản nhưng hoàn chỉnh của riêng mình, giống như ảnh gif động bên dưới.

|image0|

Trò chơi chúng ta sẽ viết mã ở đây tương tự :ref:`doc_your_first_2d_game`, nhưng có một điểm khác biệt: giờ đây bạn có thể nhảy và mục tiêu của bạn là nghiền bẹp những con quái. Nhờ vậy, bạn vừa có thể **nhận ra các mẫu** đã học trong hướng dẫn trước, vừa **phát triển chúng thêm** bằng mã và tính năng mới.

Bạn sẽ học cách:

- Làm việc với các tọa độ 3D bằng cơ chế nhảy. - Sử dụng các vật thể động học để di chuyển nhân vật 3D và phát hiện thời điểm cũng như cách chúng va chạm. - Sử dụng các lớp vật lý và một nhóm để phát hiện tương tác với những thực thể cụ thể. - Lập trình lối chơi thủ tục cơ bản bằng cách tạo các thể hiện của quái vật theo những khoảng thời gian đều đặn. - Thiết kế hoạt ảnh chuyển động và thay đổi tốc độ của nó khi chạy. - Vẽ giao diện người dùng trong trò chơi 3D.

Và hơn thế nữa.

Hướng dẫn này dành cho người mới bắt đầu đã hoàn thành toàn bộ loạt bài nhập môn. Chúng ta sẽ bắt đầu chậm rãi với các hướng dẫn chi tiết, rồi rút gọn khi thực hiện những bước tương tự. Nếu bạn là một lập trình viên có kinh nghiệm, bạn có thể xem mã nguồn của bản demo hoàn chỉnh tại đây:

- `Mã nguồn Squash the Creeps (GDScript) <https://github.com/godotengine/godot-demo-projects/tree/master/3d/squash_the_creeps>`__ - `Mã nguồn Squash the Creeps (C#) <https://github.com/godotengine/godot-demo-projects/tree/master/mono/squash_the_creeps>`__

.. note::

    Bạn có thể theo dõi loạt bài này mà không cần hoàn thành loạt bài 2D. Tuy nhiên, nếu bạn mới làm quen với phát triển trò chơi, chúng tôi khuyên bạn nên bắt đầu với 2D. Mã trò chơi 3D luôn phức tạp hơn, và loạt bài 2D sẽ cung cấp cho bạn nền tảng để theo dõi thoải mái hơn.

Chúng tôi đã chuẩn bị một số tài nguyên trò chơi để có thể bắt tay ngay vào phần mã. Bạn có thể tải chúng tại đây: `tài nguyên Squash the Creeps <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/3d_squash_the_creeps_starter.zip>`__.

Trước tiên, chúng ta sẽ xây dựng một nguyên mẫu cơ bản cho chuyển động của người chơi. Sau đó, chúng ta sẽ thêm những con quái vật được tạo ngẫu nhiên xung quanh màn hình. Tiếp theo, chúng ta sẽ triển khai cơ chế nhảy và nghiền bẹp, rồi hoàn thiện trò chơi bằng một số hoạt ảnh đẹp mắt. Cuối cùng, chúng ta sẽ thêm điểm số và màn hình thử lại.

Nội dung
--------

.. toctree::
   :maxdepth: 1
   :name: toc-learn-first_3d_game

   01.game_setup
   02.player_input
   03.player_movement_code
   04.mob_scene
   05.spawning_mobs
   06.jump_and_squash
   07.killing_player
   08.score_and_replay
   09.adding_animations
   going_further

.. |image0| image:: img/squash-the-creeps-final.gif
