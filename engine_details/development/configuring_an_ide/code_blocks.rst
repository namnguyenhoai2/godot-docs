.. _doc_configuring_an_ide_code_blocks:

Code::Blocks
============

`Code::Blocks <https://codeblocks.org/>`_ là một IDE miễn phí, mã nguồn mở và đa nền tảng.

Tạo dự án mới
-------------

Từ màn hình chính của Code::Blocks, nhấp vào **Create a new project** hoặc chọn **File > New > Project...**.

.. figure:: img/code_blocks_file_new_project.png
   :figclass: figure-w480
   :align: center

Trong cửa sổ **New from template**, từ **Projects**, chọn **Empty project**, rồi nhấp vào **Go**.

.. figure:: img/code_blocks_new_empty_project.png
   :figclass: figure-w480
   :align: center

Nhấp vào Next để bỏ qua lời chào của trình hướng dẫn tạo dự án trống mới.

.. figure:: img/code_blocks_wizard_welcome.png
   :figclass: figure-w480
   :align: center

Tệp dự án phải được tạo trong thư mục gốc của thư mục dự án đã clone. Để thực hiện việc này, trước tiên hãy đảm bảo **Project title** giống với tên thư mục mà Godot được clone vào. Trừ khi bạn clone dự án vào một thư mục có tên khác, giá trị này sẽ là ``godot``.

Thứ hai, hãy đảm bảo **Folder to create project in** là thư mục mà bạn đã chạy lệnh Git clone, không phải thư mục dự án ``godot``. Xác nhận rằng trường **Resulting filename** sẽ tạo tệp dự án trong thư mục gốc của thư mục dự án đã clone.

.. figure:: img/code_blocks_project_title_and_location.png
   :figclass: figure-w480
   :align: center

Trình biên dịch và các thiết lập cấu hình được quản lý thông qua **SCons** và sẽ được cấu hình sau. Tuy nhiên, bạn nên bỏ chọn tùy chọn **Create "Release" configuration**, để chỉ một build target được tạo trước khi nhấp vào **Finish**.

.. figure:: img/code_blocks_compiler_and_configuration.png
   :figclass: figure-w480
   :align: center

Cấu hình build
--------------

Bước đầu tiên là thay đổi các thuộc tính của dự án. Nhấp chuột phải vào dự án mới và chọn **Properties...**.

.. figure:: img/code_blocks_open_properties.png
   :figclass: figure-w480
   :align: center

Chọn thuộc tính **This is a custom Makefile**. Nhấp vào OK để lưu các thay đổi.

.. figure:: img/code_blocks_project_properties.png
   :figclass: figure-w480
   :align: center

Bước tiếp theo là thay đổi các tùy chọn build. Nhấp chuột phải vào dự án mới và chọn **Build Options...**.

.. figure:: img/code_blocks_open_build_options.png
   :figclass: figure-w480
   :align: center

Chọn tab **"Make" commands** và xóa tất cả các lệnh hiện có cho mọi build target. Với mỗi build target, nhập lệnh **SCons** để tạo build mong muốn vào trường **Build project/target**. Giá trị tối thiểu là ``scons``. Để biết chi tiết về các tùy chọn build của **SCons**, hãy xem :ref:`doc_introduction_to_the_buildsystem`. Bạn cũng nên thêm lệnh ``scons --clean`` vào trường **Clean project/target** trong các lệnh mặc định của dự án.

Nếu bạn sử dụng Windows, tất cả các lệnh cần được đặt sau ``cmd /c`` để khởi tạo trình thông dịch lệnh.

.. figure:: img/code_blocks_scons_minimum.png
   :figclass: figure-w480
   :align: center

.. figure:: img/code_blocks_scons_clean.png
   :figclass: figure-w480
   :align: center

Ví dụ trên Windows:

.. figure:: img/code_blocks_scons_windows.png
   :figclass: figure-w480
   :align: center

Code::Blocks hiện đã được cấu hình để build Godot; vì vậy bạn có thể chọn **Build > Build**, nhấp vào nút bánh răng hoặc nhấn :kbd:`Ctrl + F9`.

Cấu hình việc chạy
------------------

Sau khi **SCons** build thành công target mong muốn, mở lại **Properties...** của dự án và chọn tab **Build targets**. Trong trường **Output filename**, duyệt đến thư mục ``bin`` và chọn tệp đã biên dịch.

Bỏ chọn các tùy chọn **Auto-generate filename prefix** và **Auto-generate filename extension**.

.. figure:: img/code_blocks_build_targets.png
   :figclass: figure-w480
   :align: center

Code::Blocks hiện đã được cấu hình để chạy tệp thực thi Godot đã biên dịch của bạn; vì vậy bạn có thể chọn **Build > Run**, nhấp vào nút mũi tên màu xanh lá hoặc nhấn :kbd:`Ctrl + F10`.

Có hai điểm bổ sung đáng lưu ý. Thứ nhất, nếu cần, có thể sử dụng trường **Execution working dir** để kiểm thử các dự án cụ thể bằng cách đặt trường này thành thư mục chứa tệp ``project.godot``. Thứ hai, có thể sử dụng tab **Build targets** để thêm và xóa các build target nhằm làm việc với và tạo các build khác nhau.

Thêm tệp vào dự án
------------------

Để thêm tất cả các tệp mã Godot vào dự án, nhấp chuột phải vào dự án mới và chọn **Add files recursively...**.

.. figure:: img/code_blocks_add_files_recursively.png
   :figclass: figure-w480
   :align: center

Thư mục dự án sẽ được tự động chọn; vì vậy chỉ cần nhấp vào **Open**. Theo mặc định, tất cả các tệp mã đều được bao gồm, vì vậy chỉ cần nhấp vào **OK**.

.. figure:: img/code_blocks_select_files.png
   :figclass: figure-w480
   :align: center

Cấu hình code style
-------------------

Trước khi chỉnh sửa bất kỳ tệp nào, hãy nhớ rằng tất cả mã phải tuân thủ `code style guidelines <https://contributing.godotengine.org/en/latest/engine/guidelines/code_style.html>`__. Một điểm khác biệt quan trọng với Godot là việc sử dụng tab để thụt lề. Vì vậy, thiết lập editor mặc định quan trọng cần thay đổi trong Code::Blocks là bật tab để thụt lề. Có thể tìm thấy thiết lập này bằng cách chọn **Settings > Editor**.

.. figure:: img/code_blocks_update_editor_settings.png
   :figclass: figure-w480
   :align: center

Trong **General Settings**, trên tab **Editor Settings**, bên dưới **Tab Options**, chọn **Use TAB character**.

.. figure:: img/code_block_use_tab_character.png
   :figclass: figure-w480
   :align: center

Vậy là xong. Bạn đã sẵn sàng bắt đầu đóng góp cho Godot bằng IDE Code::Blocks. Hãy nhớ lưu tệp dự án và **Workspace**. Nếu gặp bất kỳ vấn đề nào, hãy yêu cầu trợ giúp trong một trong các `Godot's community channels <https://godotengine.org/community>`__.

.. _`Code::Blocks`: https://codeblocks.org/
