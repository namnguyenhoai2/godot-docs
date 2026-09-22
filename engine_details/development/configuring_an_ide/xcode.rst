.. _doc_configuring_an_ide_xcode:

Xcode
=====

`Xcode <https://developer.apple.com/xcode>`_ là một IDE miễn phí chỉ dành cho macOS. Bạn có thể tải xuống IDE này từ Mac App Store.

Nhập project
------------

- Từ màn hình chính của Xcode, hãy tạo một project mới bằng template **Other > External Build System**.

.. figure:: img/xcode_1_create_external_build_project.webp
   :figclass: figure-w480
   :align: center

- Bây giờ hãy chọn tên cho project và đặt đường dẫn đến executable scons trong build tool (để tìm đường dẫn, bạn có thể nhập ``where scons`` trong terminal).

.. figure:: img/xcode_2_set_external_build_project_parameters.webp
   :figclass: figure-w480
   :align: center

- Mở target chính từ phần **Targets** và chọn tab **Info**.

.. figure:: img/xcode_3_configure_scons.webp
   :figclass: figure-w480
   :align: center

- Điền biểu mẫu với các cài đặt sau:

  +-----------+-------------------------------------------------------------------------------------+
  | Arguments | Xem :ref:`doc_introduction_to_the_buildsystem` để biết danh sách đầy đủ các đối số. |
  +-----------+-------------------------------------------------------------------------------------+
  | Directory | Đường dẫn đầy đủ đến thư mục gốc của Godot                                          |
  +-----------+-------------------------------------------------------------------------------------+

- Thêm target Command Line Tool, target này sẽ được dùng để lập chỉ mục project, bằng cách chọn **File > New > Target...**.

.. figure:: img/xcode_4_add_new_target.webp
   :figclass: figure-w480
   :align: center

- Chọn **macOS > Application > Command Line Tool**.

.. figure:: img/xcode_5_select_command_line_target.webp
   :figclass: figure-w480
   :align: center

.. note:: Đặt tên sao cho bạn biết không được biên dịch bằng target này (ví dụ: ``GodotXcodeIndex``).

- Đối với target này, hãy mở tab **Build Settings** và tìm **Header Search Paths**.
- Đặt **Header Search Paths** thành đường dẫn tuyệt đối đến thư mục gốc của Godot. Bạn cũng cần bao gồm các thư mục con. Để thực hiện việc đó, hãy thêm hai dấu hoa thị (``**``) vào cuối đường dẫn, ví dụ: ``/Users/me/repos/godot-source/**``.

- Thêm mã nguồn Godot vào project bằng cách kéo và thả mã nguồn vào trình duyệt file của project.
- Chọn **Create groups** cho tùy chọn **Added folders** và chỉ chọn *only* target lập chỉ mục bằng command line của bạn trong phần **Add to targets**.

.. figure:: img/xcode_6_after_add_godot_source_to_project.webp
   :figclass: figure-w480
   :align: center

- Xcode sẽ lập chỉ mục các file ngay lúc này. Quá trình này có thể mất vài phút.
- Sau khi Xcode lập chỉ mục xong, bạn sẽ có tính năng chuyển đến định nghĩa, tự động hoàn thành mã và tô sáng cú pháp đầy đủ.

Debug project
-------------

Để bật hỗ trợ debugging, bạn cần chỉnh sửa các scheme build và run của external build target.

- Mở trình chỉnh sửa scheme của external build target.
- Tìm phần **Build > Post Actions**.
- Thêm một script run action mới
- Trong **Provide build settings from**, hãy chọn project của bạn. Việc này cho phép tham chiếu đến thư mục project trong script.
- Tạo một script để đặt tên cho binary mà Xcode có thể nhận dạng, ví dụ:

.. code-block:: shell

  ln -f ${PROJECT_DIR}/godot/bin/godot.macos.tools.64 ${PROJECT_DIR}/godot/bin/godot

.. figure:: img/xcode_7_setup_build_post_action.webp
   :figclass: figure-w480
   :align: center

- Build external build target.

- Mở lại trình chỉnh sửa scheme và chọn **Run**.

.. figure:: img/xcode_8_setup_run_scheme.webp
   :figclass: figure-w480
   :align: center

- Đặt **Executable** thành file mà bạn đã liên kết trong script post-build action.
- Chọn **Debug executable**.
- Bạn có thể thêm hai đối số trong tab **Arguments**: cờ ``-e`` sẽ mở editor thay vì Project Manager, còn đối số ``--path`` yêu cầu executable mở project được chỉ định (phải cung cấp dưới dạng đường dẫn *absolute* đến thư mục gốc của project, không phải file ``project.godot``).

Để kiểm tra mọi thứ có hoạt động hay không, hãy đặt breakpoint trong ``platform/macos/godot_main_macos.mm`` rồi chạy project.

Nếu gặp vấn đề, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.

.. _`Xcode`: https://developer.apple.com/xcode
