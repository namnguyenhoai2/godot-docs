:allow_comments: False

.. _doc_your_first_3d_game:

Trò chơi 3D đầu tiên của bạn
============================

Trong loạt hướng dẫn từng bước này, bạn sẽ tạo trò chơi 3D hoàn chỉnh đầu tiên của mình với Godot. Khi hoàn thành loạt bài, bạn sẽ có một dự án đơn giản nhưng hoàn chỉnh do chính mình thực hiện, giống như ảnh GIF động bên dưới.

|image0|

Trò chơi chúng ta sẽ lập trình ở đây tương tự :ref:`doc_your_first_2d_game`, nhưng có một điểm khác biệt: giờ đây bạn có thể nhảy và mục tiêu của bạn là nghiền bẹp những con quái. Nhờ đó, bạn vừa **nhận ra các mẫu** đã học trong hướng dẫn trước, vừa **xây dựng dựa trên chúng** bằng mã và tính năng mới.

Bạn sẽ học cách:

- Làm việc với tọa độ 3D bằng cơ chế nhảy.
- Sử dụng các vật thể động học để di chuyển nhân vật 3D và phát hiện thời điểm cũng như cách chúng va chạm.
- Sử dụng các lớp vật lý và một group để phát hiện tương tác với những thực thể cụ thể.
- Lập trình gameplay thủ tục cơ bản bằng cách tạo instance các quái vật theo những khoảng thời gian đều đặn.
- Thiết kế animation chuyển động và thay đổi tốc độ của nó trong runtime.
- Vẽ giao diện người dùng trên trò chơi 3D.

Và nhiều nội dung khác.

Hướng dẫn này dành cho những người mới bắt đầu đã hoàn thành toàn bộ loạt bài nhập môn. Chúng ta sẽ bắt đầu chậm rãi với các hướng dẫn chi tiết, rồi rút gọn khi thực hiện những bước tương tự. Nếu bạn là một lập trình viên có kinh nghiệm, bạn có thể xem mã nguồn của bản demo hoàn chỉnh tại đây:

- `Mã nguồn Squash the Creeps (GDScript) <https://github.com/godotengine/godot-demo-projects/tree/master/3d/squash_the_creeps>`__
- `Mã nguồn Squash the Creeps (C#) <https://github.com/godotengine/godot-demo-projects/tree/master/mono/squash_the_creeps>`__

.. note::

    Bạn có thể theo dõi loạt bài này mà không cần hoàn thành loạt bài 2D. Tuy nhiên, nếu bạn mới làm game, chúng tôi khuyên bạn nên bắt đầu với 2D. Mã game 3D luôn phức tạp hơn, và loạt bài 2D sẽ cung cấp cho bạn nền tảng để theo dõi các bài học một cách dễ dàng hơn.

Chúng tôi đã chuẩn bị sẵn một số tài nguyên game để có thể bắt tay ngay vào viết mã. Bạn có thể tải chúng tại đây: `Tài nguyên Squash the Creeps <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/3d_squash_the_creeps_starter.zip>`__.

Trước tiên, chúng ta sẽ xây dựng prototype cơ bản cho chuyển động của người chơi. Sau đó, chúng ta sẽ thêm các quái vật được tạo ngẫu nhiên xung quanh màn hình. Tiếp theo, chúng ta sẽ triển khai cơ chế nhảy và nghiền bẹp trước khi hoàn thiện trò chơi bằng một số animation đẹp mắt. Cuối cùng, chúng ta sẽ thêm điểm số và màn hình chơi lại.

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
