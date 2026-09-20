.. _doc_data_paths:

Đường dẫn tệp trong các project Godot
=====================================

Trang này giải thích cách đường dẫn tệp hoạt động bên trong các project Godot. Bạn sẽ tìm hiểu cách truy cập các đường dẫn trong project bằng ký hiệu ``res://`` và ``user://``, cũng như nơi Godot lưu trữ các tệp của project và editor trên hệ thống của bạn và người dùng.

Dấu phân cách đường dẫn
-----------------------

Để hỗ trợ nhiều nền tảng dễ dàng hơn, Godot sử dụng **dấu phân cách đường dẫn kiểu UNIX** (dấu gạch chéo xuôi ``/``). Các dấu này hoạt động trên mọi nền tảng, **bao gồm cả Windows**.

Thay vì viết các đường dẫn như ``C:\Projects\Game``, trong Godot, bạn nên viết ``C:/Projects/Game``.

Dấu phân cách đường dẫn kiểu Windows (dấu gạch chéo ngược ``\``) cũng được hỗ trợ trong một số phương thức liên quan đến đường dẫn, nhưng chúng cần được nhân đôi (``\\``), vì ``\`` thường được dùng làm ký tự escape cho các ký tự có ý nghĩa đặc biệt.

Điều này giúp bạn có thể làm việc với các đường dẫn được trả về bởi những ứng dụng Windows khác. Tuy nhiên, chúng tôi vẫn khuyến nghị chỉ sử dụng dấu gạch chéo xuôi trong code của bạn để đảm bảo mọi thứ hoạt động như mong đợi.

.. tip::

    Lớp String cung cấp hơn một chục phương thức để làm việc với các chuỗi biểu diễn đường dẫn tệp:

    - :ref:`String.filecasecmp_to() <class_String_method_filecasecmp_to>` - :ref:`String.filenocasecmp_to() <class_String_method_filenocasecmp_to>` - :ref:`String.get_base_dir() <class_String_method_get_base_dir>` - :ref:`String.get_basename() <class_String_method_get_basename>` - :ref:`String.get_extension() <class_String_method_get_extension>` - :ref:`String.get_file() <class_String_method_get_file>` - :ref:`String.is_absolute_path() <class_String_method_is_absolute_path>` - :ref:`String.is_relative_path() <class_String_method_is_relative_path>` - :ref:`String.is_valid_filename() <class_String_method_is_valid_filename>` - :ref:`String.path_join() <class_String_method_path_join>` - :ref:`String.simplify_path() <class_String_method_simplify_path>` - :ref:`String.validate_filename() <class_String_method_validate_filename>`

Truy cập các tệp trong thư mục project (``res://``)
---------------------------------------------------

Godot coi một project tồn tại trong bất kỳ thư mục nào chứa tệp văn bản ``project.godot``, ngay cả khi tệp đó trống. Thư mục chứa tệp này là thư mục gốc của project.

Bạn có thể truy cập bất kỳ tệp nào bằng đường dẫn tương đối so với thư mục này bằng cách viết các đường dẫn bắt đầu bằng ``res://``, đại diện cho resources. Ví dụ, bạn có thể truy cập tệp ảnh ``character.png`` nằm trong thư mục gốc của project trong code bằng đường dẫn sau: ``res://character.png``.

.. _doc_data_paths_accessing_persistent_user_data:

Truy cập dữ liệu người dùng liên tục (``user://``)
--------------------------------------------------

Để lưu trữ các tệp dữ liệu liên tục, chẳng hạn như file save hoặc các cài đặt của người chơi, bạn nên sử dụng ``user://`` thay vì ``res://`` làm tiền tố cho đường dẫn. Lý do là khi game đang chạy, hệ thống tệp của project có thể ở chế độ chỉ đọc.

Tiền tố ``user://`` trỏ đến một thư mục khác trên thiết bị của người dùng. Không giống ``res://``, thư mục được ``user://`` trỏ đến sẽ được tự động tạo và *được đảm bảo* có thể ghi, ngay cả trong project đã export.

Vị trí của thư mục ``user://`` phụ thuộc vào cấu hình trong Project Settings:

- Theo mặc định, thư mục ``user://`` được tạo bên trong thư mục
  :ref:`editor data path <doc_data_paths_editor_data_paths>` in the
  ``app_userdata/[project_name]``. Đây là mặc định để các prototype và project thử nghiệm được giữ độc lập trong thư mục dữ liệu của Godot. - Nếu :ref:`application/config/use_custom_user_dir <class_ProjectSettings_property_application/config/use_custom_user_dir>` được bật trong Project Settings, thư mục ``user://`` sẽ được tạo **bên cạnh** đường dẫn dữ liệu của editor Godot, tức là tại vị trí tiêu chuẩn dành cho dữ liệu ứng dụng.

  * Theo mặc định, tên thư mục sẽ được suy ra từ tên project, nhưng bạn có thể tùy chỉnh thêm bằng
    :ref:`application/config/custom_user_dir_name <class_ProjectSettings_property_application/config/custom_user_dir_name>`.
    Đường dẫn này có thể chứa các dấu phân cách đường dẫn, vì vậy bạn có thể sử dụng nó, chẳng hạn, để nhóm các project của một studio theo cấu trúc ``Studio Name/Game Name``.

Trên các nền tảng desktop, đường dẫn thư mục thực tế cho ``user://`` là:

+---------------------+------------------------------------------------------------------------------+
| Type                | Location                                                                     |
+=====================+==============================================================================+
| Default             | | Windows: ``%APPDATA%\Godot\app_userdata\[project_name]``                   |
|                     | | macOS: ``~/Library/Application Support/Godot/app_userdata/[project_name]`` |
|                     | | Linux: ``~/.local/share/godot/app_userdata/[project_name]``                |
+---------------------+------------------------------------------------------------------------------+
| Custom dir          | | Windows: ``%APPDATA%\[project_name]``                                      |
|                     | | macOS: ``~/Library/Application Support/[project_name]``                    |
|                     | | Linux: ``~/.local/share/[project_name]``                                   |
+---------------------+------------------------------------------------------------------------------+
| Custom dir and name | | Windows: ``%APPDATA%\[custom_user_dir_name]``                              |
|                     | | macOS: ``~/Library/Application Support/[custom_user_dir_name]``            |
|                     | | Linux: ``~/.local/share/[custom_user_dir_name]``                           |
+---------------------+------------------------------------------------------------------------------+

``[project_name]`` dựa trên tên ứng dụng được xác định trong Project Settings, nhưng bạn có thể ghi đè tên này riêng cho từng nền tảng bằng :ref:`feature tags <doc_feature_tags>`.

Trên các nền tảng mobile, đường dẫn này là duy nhất cho project và các ứng dụng khác không thể truy cập vì lý do bảo mật.

Trong các bản export HTML5, ``user://`` sẽ trỏ đến một hệ thống tệp ảo được lưu trữ trên thiết bị thông qua IndexedDB. (Bạn vẫn có thể tương tác với hệ thống tệp chính thông qua singleton :ref:`JavaScriptBridge <class_JavaScriptBridge>`.)

Ghi nhật ký vào tệp
-------------------

.. seealso::

    Tài liệu về việc ghi nhật ký vào tệp đã được chuyển sang :ref:`doc_logging`.

Chuyển đổi đường dẫn thành đường dẫn tuyệt đối hoặc đường dẫn "local"
---------------------------------------------------------------------

Bạn có thể sử dụng :ref:`ProjectSettings.globalize_path() <class_ProjectSettings_method_globalize_path>` để chuyển đổi một đường dẫn "local" như ``res://path/to/file.txt`` thành đường dẫn OS tuyệt đối. Ví dụ, có thể sử dụng :ref:`ProjectSettings.globalize_path() <class_ProjectSettings_method_globalize_path>` để mở các đường dẫn "local" trong trình quản lý tệp của OS bằng :ref:`OS.shell_open() <class_OS_method_shell_open>`, vì trình này chỉ chấp nhận các đường dẫn OS gốc.

Để chuyển đổi một đường dẫn OS tuyệt đối thành đường dẫn "local" bắt đầu bằng ``res://`` hoặc ``user://``, hãy sử dụng :ref:`ProjectSettings.localize_path() <class_ProjectSettings_method_localize_path>`. Cách này chỉ hoạt động với các đường dẫn tuyệt đối trỏ đến tệp hoặc thư mục trong thư mục gốc của project hoặc các thư mục ``user://`` của project.

.. _doc_data_paths_editor_data_paths:

Đường dẫn dữ liệu của editor
----------------------------

Editor sử dụng các đường dẫn khác nhau cho dữ liệu editor, cài đặt editor và cache, tùy thuộc vào nền tảng. Theo mặc định, các đường dẫn này là:

+-----------------+---------------------------------------------------+
| Type            | Location                                          |
+=================+===================================================+
| Editor data     | | Windows: ``%APPDATA%\Godot\``                   |
|                 | | macOS: ``~/Library/Application Support/Godot/`` |
|                 | | Linux: ``~/.local/share/godot/``                |
+-----------------+---------------------------------------------------+
| Editor settings | | Windows: ``%APPDATA%\Godot\``                   |
|                 | | macOS: ``~/Library/Application Support/Godot/`` |
|                 | | Linux: ``~/.config/godot/``                     |
+-----------------+---------------------------------------------------+
| Cache           | | Windows: ``%TEMP%\Godot\``                      |
|                 | | macOS: ``~/Library/Caches/Godot/``              |
|                 | | Linux: ``~/.cache/godot/``                      |
+-----------------+---------------------------------------------------+

- **Dữ liệu editor** chứa các export template và dữ liệu riêng của project. - **Cài đặt editor** chứa tệp cấu hình cài đặt chính của editor cùng nhiều tùy chỉnh khác dành riêng cho người dùng (bố cục editor, feature profile, script template, v.v.). - **Cache** chứa dữ liệu do editor tạo ra hoặc được lưu trữ tạm thời. Bạn có thể xóa dữ liệu này an toàn khi Godot đã đóng.

Godot tuân thủ `XDG Base Directory Specification <https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html>`__ trên Linux/\*BSD. Bạn có thể ghi đè các biến môi trường ``XDG_DATA_HOME``, ``XDG_CONFIG_HOME`` và ``XDG_CACHE_HOME`` để thay đổi đường dẫn dữ liệu của editor và project.

.. note:: If you use `Godot packaged as a Flatpak
          <https://flathub.org/apps/details/org.godotengine.Godot>`__, các đường dẫn dữ liệu của editor sẽ nằm trong các thư mục con của ``~/.var/app/org.godotengine.Godot/``.

.. _doc_data_paths_self_contained_mode:

Chế độ độc lập
~~~~~~~~~~~~~~

Nếu bạn tạo một tệp có tên ``._sc_`` hoặc ``_sc_`` trong cùng thư mục với binary của editor (hoặc trong `MacOS/Contents/` đối với editor .app của macOS), Godot sẽ bật *chế độ độc lập*. Chế độ này khiến Godot ghi toàn bộ dữ liệu editor, cài đặt và cache vào một thư mục có tên ``editor_data/`` trong cùng thư mục với binary của editor. Bạn có thể dùng chế độ này để tạo bản cài đặt editor portable.

`Steam release of Godot <https://store.steampowered.com/app/404790/>`__ mặc định sử dụng chế độ độc lập.

.. CẬP NHẬT: Chưa được hỗ trợ. Khi chế độ độc lập được hỗ trợ trong các project .. đã export, hãy xóa hoặc cập nhật ghi chú này.

.. note::

    Chế độ độc lập hiện chưa được hỗ trợ trong các project đã export. Để đọc và ghi các tệp tương đối với đường dẫn của executable, hãy sử dụng
    :ref:`OS.get_executable_path() <class_OS_method_get_executable_path>`.
    Lưu ý rằng việc ghi tệp vào đường dẫn của executable chỉ hoạt động nếu executable được đặt tại một vị trí có thể ghi (tức là **không phải** Program Files hoặc một thư mục khác ở chế độ chỉ đọc đối với người dùng thông thường).
