.. _doc_configuring_an_ide_qtcreator:

Qt Creator
==========

`Qt Creator <https://doc.qt.io/qtcreator/index.html>`_ là một IDE mã nguồn mở, miễn phí dành cho tất cả các nền tảng máy tính để bàn.

Nhập dự án
----------

- Từ màn hình chính của Qt Creator, chọn **New Project > Import Project > Import Existing Project**.

.. figure:: img/qtcreator-new-project.png
   :figclass: figure-w480
   :align: center

- Trong **Location**, chọn thư mục gốc của Godot.

.. figure:: img/qtcreator-set-project-path.png
   :figclass: figure-w480
   :align: center

- Tiếp theo, bạn có thể chọn những thư mục và tệp sẽ hiển thị trong dự án. Mặc dù các tệp C/C++ được tự động thêm vào, các phần mở rộng khác cũng có thể hữu ích: ``*.glsl`` cho các tệp shader, ``*.py`` cho các tệp hệ thống xây dựng, ``*.java`` cho việc phát triển trên nền tảng Android, ``*.mm`` cho việc phát triển trên nền tảng macOS.

.. figure:: img/qtcreator-apply-import-filter.png
   :figclass: figure-w480
   :align: center

.. note:: You can change this configuration later by right-clicking on your project
          và chọn tùy chọn **Edit Files...**.

          .. figure:: img/qtcreator-edit-files-menu.png
            :figclass: figure-w480
            :align: center


- Hoàn tất việc nhập. - Mở tệp ``project_name.includes`` và thêm một dòng chứa ``.`` vào tệp để bật tính năng tự động hoàn thành mã một cách chính xác.

.. figure:: img/qtcreator-project-name-includes.png
   :figclass: figure-w480
   :align: center

- Từ menu bên trái, chọn **Projects** và mở tab **Build**. - Xóa bước xây dựng ``make`` được định sẵn.

.. figure:: img/qtcreator-projects-build.png
   :figclass: figure-w480
   :align: center

- Nhấp vào **Add Build Step > Custom Process Step** để thêm một bước xây dựng mới với các cài đặt sau:

  +-----------+------------------------------------------------------------------------------+ | Command | **scons** | +-----------+------------------------------------------------------------------------------+ | Arguments | Xem :ref:`doc_introduction_to_the_buildsystem` để biết danh sách đầy đủ các đối số. | +-----------+------------------------------------------------------------------------------+

.. figure:: img/qtcreator-set-scons-command.png
   :figclass: figure-w480
   :align: center

.. note:: If the build fails with ``Could not start process "scons"``, it can mean that ``scons``
          không nằm trong biến môi trường ``PATH`` của bạn. Trong trường hợp này, bạn sẽ phải chỉ định đường dẫn đầy đủ đến tệp nhị phân SCons.

Gỡ lỗi dự án
------------

- Từ menu bên trái, chọn **Projects** và mở tab **Run**. - Trong **Executable**, chỉ định đường dẫn đến tệp thực thi nằm trong thư mục ``<Godot root directory>/bin``. Tên tệp phụ thuộc vào cấu hình xây dựng của bạn, ví dụ ``godot.linuxbsd.editor.dev.x86_64`` cho nền tảng LinuxBSD 64-bit với ``platform=editor`` và ``dev_build=yes``. Bạn có thể sử dụng ``%{buildDir}`` để tham chiếu đến thư mục gốc của dự án, ví dụ: ``%{buildDir}/bin/godot.linuxbsd.editor.dev.x86_64``. - Nếu muốn chạy một dự án cụ thể, hãy chỉ định thư mục gốc của dự án đó trong **Working directory**. - Nếu muốn chạy trình chỉnh sửa, hãy thêm ``-e`` vào trường **Command line arguments**.

.. figure:: img/qtcreator-run-command.png
   :figclass: figure-w480
   :align: center

Để tìm hiểu thêm về các đối số dòng lệnh, hãy tham khảo
:ref:`command line tutorial <doc_command_line_tutorial>`.

Cấu hình kiểu mã
----------------

Các nhà phát triển phải tuân theo `kiểu mã <https://contributing.godotengine.org/en/latest/engine/guidelines/code_style.html>`__ của dự án và IDE phải hỗ trợ họ tuân theo kiểu mã đó. Theo mặc định, Qt Creator sử dụng khoảng trắng để thụt lề, điều này không phù hợp với hướng dẫn về kiểu mã của Godot. Bạn có thể thay đổi hành vi này bằng cách thay đổi **Code Style** trong **Tools > Options > C++**.

.. figure:: img/qtcreator-options-cpp.png
   :figclass: figure-w480
   :align: center

Nhấp vào **Edit** để thay đổi cài đặt hiện tại, sau đó nhấp vào nút **Copy Built-in Code Style** để thiết lập một kiểu mã mới. Đặt tên cho kiểu mã đó (ví dụ: Godot) và thay đổi chính sách Tab thành **Tabs Only**.

.. figure:: img/qtcreator-edit-codestyle.png
   :figclass: figure-w480
   :align: center

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.
