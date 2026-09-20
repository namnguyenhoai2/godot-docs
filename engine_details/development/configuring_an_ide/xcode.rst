.. _doc_configuring_an_ide_xcode:

Xcode
=====

`Xcode <https://developer.apple.com/xcode>`_ là một IDE miễn phí, chỉ dành cho macOS. Bạn có thể tải xuống từ Mac App Store.

Nhập dự án
----------

- Từ màn hình chính của Xcode, hãy tạo một dự án mới bằng mẫu **Other > External Build System**.

.. figure:: img/xcode_1_create_external_build_project.webp
   :figclass: figure-w480
   :align: center

- Bây giờ hãy chọn tên cho dự án và đặt đường dẫn đến tệp thực thi scons trong công cụ build (để tìm đường dẫn, bạn có thể nhập ``where scons`` trong terminal).

.. figure:: img/xcode_2_set_external_build_project_parameters.webp
   :figclass: figure-w480
   :align: center

- Mở target chính trong phần **Targets** rồi chọn tab **Info**.

.. figure:: img/xcode_3_configure_scons.webp
   :figclass: figure-w480
   :align: center

- Điền vào biểu mẫu bằng các cài đặt sau:

  +------------+------------------------------------------------------------------------------+ | Arguments | Xem :ref:`doc_introduction_to_the_buildsystem` để biết danh sách đầy đủ các đối số. | +------------+------------------------------------------------------------------------------+ | Directory | Đường dẫn đầy đủ đến thư mục gốc của Godot | +------------+------------------------------------------------------------------------------+

- Thêm một target Command Line Tool, target này sẽ được dùng để lập chỉ mục dự án, bằng cách chọn **File > New > Target...**.

.. figure:: img/xcode_4_add_new_target.webp
   :figclass: figure-w480
   :align: center

- Chọn **macOS > Application > Command Line Tool**.

.. figure:: img/xcode_5_select_command_line_target.webp
   :figclass: figure-w480
   :align: center

.. note:: Name it something so you know not to compile with this target (e.g. ``GodotXcodeIndex``).

- Đối với target này, hãy mở tab **Build Settings** và tìm **Header Search Paths**. - Đặt **Header Search Paths** thành đường dẫn tuyệt đối đến thư mục gốc của Godot. Bạn cũng cần bao gồm các thư mục con. Để thực hiện việc đó, hãy thêm hai dấu hoa thị (``**``) vào cuối đường dẫn, ví dụ: ``/Users/me/repos/godot-source/**``.

- Thêm mã nguồn Godot vào dự án bằng cách kéo và thả mã nguồn vào trình duyệt tệp của dự án. - Chọn **Create groups** cho tùy chọn **Added folders** và chỉ chọn target lập chỉ mục dòng lệnh của bạn trong phần **Add to targets**.

.. figure:: img/xcode_6_after_add_godot_source_to_project.webp
   :figclass: figure-w480
   :align: center

- Xcode giờ sẽ lập chỉ mục các tệp. Quá trình này có thể mất vài phút. - Khi Xcode lập chỉ mục xong, bạn sẽ có tính năng chuyển đến định nghĩa, tự động hoàn thành và tô sáng cú pháp đầy đủ.

Gỡ lỗi dự án
------------

Để bật hỗ trợ gỡ lỗi, bạn cần chỉnh sửa các scheme build và run của target build bên ngoài.

- Mở trình chỉnh sửa scheme của target build bên ngoài. - Tìm phần **Build > Post Actions**. - Thêm một script run action mới - Trong **Provide build settings from**, hãy chọn dự án của bạn. Điều này cho phép tham chiếu đến thư mục dự án trong script. - Tạo một script đặt tên cho tệp nhị phân để Xcode có thể nhận diện, ví dụ:

.. code-block:: shell

  ln -f ${PROJECT_DIR}/godot/bin/godot.macos.tools.64 ${PROJECT_DIR}/godot/bin/godot

.. figure:: img/xcode_7_setup_build_post_action.webp
   :figclass: figure-w480
   :align: center

- Build target build bên ngoài.

- Mở lại trình chỉnh sửa scheme và chọn **Run**.

.. figure:: img/xcode_8_setup_run_scheme.webp
   :figclass: figure-w480
   :align: center

- Đặt **Executable** thành tệp bạn đã liên kết trong script post-build action. - Chọn **Debug executable**. - Bạn có thể thêm hai đối số trong tab **Arguments**: cờ ``-e`` sẽ mở trình chỉnh sửa thay vì Project Manager, còn đối số ``--path`` yêu cầu tệp thực thi mở dự án được chỉ định (phải được cung cấp dưới dạng đường dẫn *tuyệt đối* đến thư mục gốc của dự án, không phải tệp ``project.godot``).

Để kiểm tra mọi thứ đang hoạt động, hãy đặt một breakpoint trong ``platform/macos/godot_main_macos.mm`` và chạy dự án.

Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `kênh cộng đồng của Godot <https://godotengine.org/community>`__.
