:allow_comments: False

.. _doc_your_first_2d_game:

Trò chơi 2D đầu tiên của bạn
============================

Trong loạt hướng dẫn từng bước này, bạn sẽ tạo trò chơi 2D hoàn chỉnh đầu tiên của mình với Godot. Khi hoàn thành loạt hướng dẫn, bạn sẽ có một trò chơi đơn giản nhưng hoàn chỉnh do chính mình tạo ra, giống như hình ảnh bên dưới.

|image0|

Bạn sẽ học cách trình chỉnh sửa Godot hoạt động, cách cấu trúc một dự án và cách xây dựng một trò chơi 2D.

.. note:: Dự án này là phần giới thiệu về engine Godot. Dự án giả định rằng bạn đã có một số kinh nghiệm lập trình. Nếu hoàn toàn mới làm quen với lập trình, bạn nên bắt đầu tại đây: :ref:`doc_scripting`.

Trò chơi có tên là "Dodge the Creeps!". Nhân vật của bạn phải di chuyển và tránh kẻ địch càng lâu càng tốt.

Bạn sẽ học cách:

- Tạo một trò chơi 2D hoàn chỉnh bằng trình chỉnh sửa Godot.
- Cấu trúc một dự án trò chơi đơn giản.
- Di chuyển nhân vật người chơi và thay đổi sprite của nhân vật.
- Sinh ra các kẻ địch ngẫu nhiên.
- Tính điểm.

Và nhiều nội dung khác.

Bạn sẽ tìm thấy một loạt hướng dẫn khác, trong đó bạn sẽ tạo một trò chơi tương tự nhưng ở dạng 3D. Tuy vậy, chúng tôi khuyên bạn nên bắt đầu với loạt hướng dẫn này.

**Tại sao nên bắt đầu với 2D?**

Nếu mới làm quen với việc phát triển trò chơi hoặc chưa quen với Godot, chúng tôi khuyên bạn nên bắt đầu với các trò chơi 2D. Điều này sẽ giúp bạn làm quen với cả hai trước khi bắt tay vào các trò chơi 3D, vốn thường phức tạp hơn.

Bạn có thể tìm thấy phiên bản hoàn chỉnh của dự án này tại vị trí sau:

- `Mã nguồn Dodge the Creeps (GDScript) <https://github.com/godotengine/godot-demo-projects/tree/master/2d/dodge_the_creeps>`__
- `Mã nguồn Dodge the Creeps (C#) <https://github.com/godotengine/godot-demo-projects/tree/master/mono/dodge_the_creeps>`__

Điều kiện tiên quyết
--------------------

Hướng dẫn từng bước này dành cho người mới bắt đầu đã hoàn thành toàn bộ
:ref:`doc_step_by_step`.

Nếu là một lập trình viên có kinh nghiệm, bạn có thể tìm mã nguồn của bản demo hoàn chỉnh tại đây: `Mã nguồn Dodge the Creeps <https://github.com/godotengine/godot-demo-projects/tree/master/2d/dodge_the_creeps>`__.

Chúng tôi đã chuẩn bị một số game asset mà bạn cần tải xuống để có thể bắt đầu ngay với phần code.

Bạn có thể tải chúng xuống bằng cách nhấp vào liên kết bên dưới.

`dodge_the_creeps_2d_assets.zip <https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/dodge_the_creeps_2d_assets.zip>`_.

Nội dung
--------

.. toctree::
   :maxdepth: 1
   :name: toc-learn-first_2d_game

   01.project_setup
   02.player_scene
   03.coding_the_player
   04.creating_the_enemy
   05.the_main_game_scene
   06.heads_up_display
   07.finishing-up

.. |image0| image:: img/dodge_preview.gif

.. _`dodge_the_creeps_2d_assets.zip`: https://github.com/godotengine/godot-docs-project-starters/releases/download/latest-4.x/dodge_the_creeps_2d_assets.zip
