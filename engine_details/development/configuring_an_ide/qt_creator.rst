.. _doc_configuring_an_ide_qtcreator:

Qt Creator
==========

`Qt Creator <https://doc.qt.io/qtcreator/index.html>`_ là một IDE mã nguồn mở miễn phí dành cho mọi nền tảng máy tính để bàn.

Nhập project
------------

- Từ màn hình chính của Qt Creator, chọn **New Project > Import Project > Import Existing Project**.

.. figure:: img/qtcreator-new-project.png
   :figclass: figure-w480
   :align: center

- Trong **Location**, chọn thư mục gốc của Godot.

.. figure:: img/qtcreator-set-project-path.png
   :figclass: figure-w480
   :align: center

- Tiếp theo, bạn có thể chọn những thư mục và tệp sẽ hiển thị trong project. Các tệp C/C++ được tự động thêm vào, còn những phần mở rộng khác có thể hữu ích: ``*.glsl`` cho các tệp shader, ``*.py`` cho các tệp buildsystem, ``*.java`` cho việc phát triển trên nền tảng Android, ``*.mm`` cho việc phát triển trên nền tảng macOS.

.. figure:: img/qtcreator-apply-import-filter.png
   :figclass: figure-w480
   :align: center

.. note:: Bạn có thể thay đổi cấu hình này sau bằng cách nhấp chuột phải vào project rồi chọn tùy chọn **Edit Files...**.

          .. figure:: img/qtcreator-edit-files-menu.png
            :figclass: figure-w480
            :align: center


- Hoàn tất việc nhập.
- Mở tệp ``project_name.includes`` và thêm một dòng chứa ``.`` vào tệp đó để bật tính năng hoàn tất mã chính xác.

.. figure:: img/qtcreator-project-name-includes.png
   :figclass: figure-w480
   :align: center

- Từ menu bên trái, chọn **Projects** rồi mở tab **Build**.
- Xóa ``make`` build step được định nghĩa sẵn.

.. figure:: img/qtcreator-projects-build.png
   :figclass: figure-w480
   :align: center

- Nhấp vào **Add Build Step > Custom Process Step** để thêm build step mới với các cài đặt sau:

  +--------+-------------------------------------------------------------------------------------+
  | Lệnh   | **scons**                                                                           |
  +--------+-------------------------------------------------------------------------------------+
  | Đối số | Xem :ref:`doc_introduction_to_the_buildsystem` để biết danh sách đầy đủ các đối số. |
  +--------+-------------------------------------------------------------------------------------+

.. figure:: img/qtcreator-set-scons-command.png
   :figclass: figure-w480
   :align: center

.. note:: Nếu quá trình build thất bại với ``Could not start process "scons"``, điều đó có thể có nghĩa là ``scons`` không nằm trong biến môi trường ``PATH`` của bạn. Trong trường hợp này, bạn sẽ phải chỉ định đường dẫn đầy đủ đến tệp nhị phân SCons.

Gỡ lỗi project
--------------

- Từ menu bên trái, chọn **Projects** rồi mở tab **Run**.
- Trong **Executable**, chỉ định đường dẫn đến tệp thực thi nằm trong thư mục ``<Godot root directory>/bin``. Tên tệp phụ thuộc vào cấu hình build của bạn, ví dụ ``godot.linuxbsd.editor.dev.x86_64`` dành cho nền tảng LinuxBSD 64-bit với ``platform=editor`` và ``dev_build=yes``. Bạn có thể dùng ``%{buildDir}`` để tham chiếu đến thư mục gốc của project, ví dụ: ``%{buildDir}/bin/godot.linuxbsd.editor.dev.x86_64``.
- Nếu muốn chạy một project cụ thể, hãy chỉ định thư mục gốc của project đó trong **Working directory**.
- Nếu muốn chạy editor, hãy thêm ``-e`` vào trường **Command line arguments**.

.. figure:: img/qtcreator-run-command.png
   :figclass: figure-w480
   :align: center

Để tìm hiểu thêm về các đối số dòng lệnh, hãy tham khảo
:ref:`command line tutorial <doc_command_line_tutorial>`.

Cấu hình code style
-------------------

Các developer phải tuân theo `code style <https://contributing.godotengine.org/en/latest/engine/guidelines/code_style.html>`__ của project, và IDE nên hỗ trợ họ tuân theo style đó. Theo mặc định, Qt Creator sử dụng dấu cách để thụt lề, không phù hợp với hướng dẫn code style của Godot. Bạn có thể thay đổi hành vi này bằng cách thay đổi **Code Style** trong **Tools > Options > C++**.

.. figure:: img/qtcreator-options-cpp.png
   :figclass: figure-w480
   :align: center

Nhấp vào **Edit** để thay đổi các cài đặt hiện tại, sau đó nhấp vào nút **Copy Built-in Code Style** để thiết lập code style mới. Đặt tên cho style đó (ví dụ: Godot) và thay đổi chính sách Tab thành **Tabs Only**.

.. figure:: img/qtcreator-edit-codestyle.png
   :figclass: figure-w480
   :align: center

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.

.. _`Qt Creator`: https://doc.qt.io/qtcreator/index.html
