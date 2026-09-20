.. _doc_configuring_an_ide_kdevelop:

KDevelop
========

`KDevelop <https://www.kdevelop.org>`_ là một IDE miễn phí, mã nguồn mở dành cho mọi nền tảng máy tính để bàn.

Nhập dự án
----------

- Từ màn hình chính của KDevelop, chọn **Open Project**.

.. figure:: img/kdevelop_newproject.webp
   :figclass: figure-w480
   :align: center

   KDevelop's main screen.

- Đi tới thư mục gốc của Godot và chọn thư mục đó. - Ở màn hình tiếp theo, chọn **Custom Build System** cho **Project Manager**.

.. figure:: img/kdevelop_custombuild.webp
   :figclass: figure-w480
   :align: center

- Sau khi dự án đã được nhập, mở cấu hình dự án bằng cách nhấp chuột phải vào dự án trong bảng **Projects** và chọn tùy chọn **Open Configuration..**.

.. figure:: img/kdevelop_openconfig.webp
   :figclass: figure-w480
   :align: center

- Trong **Language Support**, mở tab **Includes/Imports** và thêm các đường dẫn sau:

  .. code-block:: none

     .  // A dot, to indicate the root of the Godot project
     core/
     core/os/
     core/math/
     drivers/
     platform/<your_platform>/  // Replace <your_platform> with a folder
                                   corresponding to your current platform

.. figure:: img/kdevelop_addincludes.webp
   :figclass: figure-w480
   :align: center

- Áp dụng các thay đổi. - Trong **Custom Build System**, thêm một cấu hình biên dịch mới với các thiết lập sau:

  +-----------------+------------------------------------------------------------------------------+ | Build Directory | *blank* | +-----------------+------------------------------------------------------------------------------+ | Enable | **True** | +-----------------+------------------------------------------------------------------------------+ | Executable | **scons** | +-----------------+------------------------------------------------------------------------------+ | Arguments | Xem :ref:`doc_introduction_to_the_buildsystem` để biết danh sách đầy đủ các đối số. | +-----------------+------------------------------------------------------------------------------+

.. figure:: img/kdevelop_buildconfig.webp
   :figclass: figure-w480
   :align: center

- Áp dụng các thay đổi và đóng cửa sổ cấu hình.

Gỡ lỗi dự án
------------

- Chọn **Run > Configure Launches...** từ menu trên cùng.

.. figure:: img/kdevelop_configlaunches.webp
   :figclass: figure-w480
   :align: center

- Nhấp **Add** để tạo cấu hình khởi chạy mới. - Chọn tùy chọn **Executable** và chỉ định đường dẫn đến tệp thực thi nằm trong thư mục ``<Godot root directory>/bin``. Tên tệp phụ thuộc vào cấu hình biên dịch của bạn, ví dụ ``godot.linuxbsd.editor.dev.x86_64`` cho nền tảng LinuxBSD 64-bit với ``platform=linuxbsd``, ``target=editor`` và ``dev_build=yes``.

.. figure:: img/kdevelop_configlaunches2.webp
   :figclass: figure-w480
   :align: center

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.
