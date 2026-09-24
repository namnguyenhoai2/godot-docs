.. _doc_data_paths:

Đường dẫn tệp trong các dự án Godot
===================================

Trang này giải thích cách đường dẫn tệp hoạt động bên trong các dự án Godot. Bạn sẽ học cách truy cập các đường dẫn trong dự án bằng ký hiệu ``res://`` và ``user://``, cũng như nơi Godot lưu trữ các tệp dự án và trình chỉnh sửa trên hệ thống của bạn và người dùng.

Dấu phân cách đường dẫn
-----------------------

Để hỗ trợ nhiều nền tảng dễ dàng hơn, Godot sử dụng **dấu phân cách đường dẫn theo kiểu UNIX** (dấu gạch chéo xuôi ``/``). Các dấu này hoạt động trên mọi nền tảng, **bao gồm Windows**.

Thay vì viết các đường dẫn như ``C:\Projects\Game``, trong Godot, bạn nên viết ``C:/Projects/Game``.

Dấu phân cách đường dẫn theo kiểu Windows (dấu gạch chéo ngược ``\``) cũng được hỗ trợ trong một số phương thức liên quan đến đường dẫn, nhưng chúng cần được nhân đôi (``\\``), vì ``\`` thường được dùng làm ký tự escape cho các ký tự có ý nghĩa đặc biệt.

Điều này giúp bạn có thể làm việc với các đường dẫn do những ứng dụng Windows khác trả về. Tuy nhiên, chúng tôi vẫn khuyến nghị chỉ sử dụng dấu gạch chéo xuôi trong mã của bạn để đảm bảo mọi thứ hoạt động như dự kiến.

.. tip::

    Lớp String cung cấp hơn một chục phương thức để làm việc với các chuỗi biểu diễn đường dẫn tệp:

    - :ref:`String.filecasecmp_to() <class_String_method_filecasecmp_to>`
    - :ref:`String.filenocasecmp_to() <class_String_method_filenocasecmp_to>`
    - :ref:`String.get_base_dir() <class_String_method_get_base_dir>`
    - :ref:`String.get_basename() <class_String_method_get_basename>`
    - :ref:`String.get_extension() <class_String_method_get_extension>`
    - :ref:`String.get_file() <class_String_method_get_file>`
    - :ref:`String.is_absolute_path() <class_String_method_is_absolute_path>`
    - :ref:`String.is_relative_path() <class_String_method_is_relative_path>`
    - :ref:`String.is_valid_filename() <class_String_method_is_valid_filename>`
    - :ref:`String.path_join() <class_String_method_path_join>`
    - :ref:`String.simplify_path() <class_String_method_simplify_path>`
    - :ref:`String.validate_filename() <class_String_method_validate_filename>`

Truy cập các tệp trong thư mục dự án (``res://``)
-------------------------------------------------

Godot coi mọi thư mục chứa tệp văn bản ``project.godot`` là một dự án, ngay cả khi tệp đó trống. Thư mục chứa tệp này là thư mục gốc của dự án.

Bạn có thể truy cập mọi tệp tương đối so với thư mục này bằng cách viết các đường dẫn bắt đầu bằng ``res://``, đại diện cho tài nguyên. Ví dụ: bạn có thể truy cập tệp hình ảnh ``character.png`` nằm trong thư mục gốc của dự án bằng mã với đường dẫn sau: ``res://character.png``.

.. _doc_data_paths_accessing_persistent_user_data:

Truy cập dữ liệu người dùng liên tục (``user://``)
--------------------------------------------------

Để lưu trữ các tệp dữ liệu liên tục, chẳng hạn như tệp lưu hoặc cài đặt của người chơi, bạn nên sử dụng ``user://`` thay vì ``res://`` làm tiền tố cho đường dẫn. Lý do là khi trò chơi đang chạy, hệ thống tệp của dự án có thể sẽ ở chế độ chỉ đọc.

Tiền tố ``user://`` trỏ đến một thư mục khác trên thiết bị của người dùng. Không giống ``res://``, thư mục được ``user://`` trỏ đến sẽ được tự động tạo và *được đảm bảo* có thể ghi, kể cả trong một dự án đã export.

Vị trí của thư mục ``user://`` phụ thuộc vào cấu hình trong Project Settings:

- Theo mặc định, thư mục ``user://`` được tạo bên trong
  :ref:`đường dẫn dữ liệu của trình chỉnh sửa <doc_data_paths_editor_data_paths>` trong thư mục ``app_userdata/[project_name]``. Đây là mặc định để các prototype và dự án thử nghiệm vẫn nằm độc lập trong thư mục dữ liệu của Godot.
- Nếu :ref:`application/config/use_custom_user_dir <class_ProjectSettings_property_application/config/use_custom_user_dir>` được bật trong Project Settings, thư mục ``user://`` sẽ được tạo **bên cạnh** đường dẫn dữ liệu của trình chỉnh sửa Godot, tức là tại vị trí tiêu chuẩn dành cho dữ liệu ứng dụng.

  * Theo mặc định, tên thư mục sẽ được suy ra từ tên dự án, nhưng có thể tùy chỉnh thêm bằng
    :ref:`application/config/custom_user_dir_name <class_ProjectSettings_property_application/config/custom_user_dir_name>`. Đường dẫn này có thể chứa các dấu phân cách đường dẫn, vì vậy bạn có thể dùng nó, chẳng hạn, để nhóm các dự án của một studio với cấu trúc ``Studio Name/Game Name``.

Trên các nền tảng máy tính để bàn, đường dẫn thư mục thực tế cho ``user://`` là:

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

``[project_name]`` được dựa trên tên ứng dụng được xác định trong Project Settings, nhưng bạn có thể ghi đè tên này theo từng nền tảng bằng cách sử dụng :ref:`feature tags <doc_feature_tags>`.

Trên các nền tảng di động, đường dẫn này là duy nhất cho dự án và các ứng dụng khác không thể truy cập vì lý do bảo mật.

Khi export sang HTML5, ``user://`` sẽ trỏ đến một hệ thống tệp ảo được lưu trữ trên thiết bị thông qua IndexedDB. (Bạn vẫn có thể tương tác với hệ thống tệp chính thông qua singleton :ref:`JavaScriptBridge <class_JavaScriptBridge>`.)

Ghi nhật ký vào tệp
-------------------

.. seealso::

    Tài liệu về việc ghi nhật ký vào tệp đã được chuyển đến :ref:`doc_logging`.

Chuyển đổi đường dẫn sang đường dẫn tuyệt đối hoặc đường dẫn "local"
--------------------------------------------------------------------

Bạn có thể sử dụng :ref:`ProjectSettings.globalize_path() <class_ProjectSettings_method_globalize_path>` để chuyển đổi một đường dẫn "local" như ``res://path/to/file.txt`` thành đường dẫn tuyệt đối của hệ điều hành. Ví dụ, có thể dùng :ref:`ProjectSettings.globalize_path() <class_ProjectSettings_method_globalize_path>` để mở các đường dẫn "local" trong trình quản lý tệp của hệ điều hành bằng :ref:`OS.shell_open() <class_OS_method_shell_open>`, vì trình quản lý này chỉ chấp nhận các đường dẫn gốc của hệ điều hành.

Để chuyển đổi một đường dẫn tuyệt đối của hệ điều hành thành đường dẫn "local" bắt đầu bằng ``res://`` hoặc ``user://``, hãy sử dụng :ref:`ProjectSettings.localize_path() <class_ProjectSettings_method_localize_path>`. Cách này chỉ hoạt động với các đường dẫn tuyệt đối trỏ đến tệp hoặc thư mục trong thư mục gốc của dự án hoặc các thư mục ``user://``.

.. _doc_data_paths_editor_data_paths:

Đường dẫn dữ liệu của trình chỉnh sửa
-------------------------------------

Trình chỉnh sửa sử dụng các đường dẫn khác nhau cho dữ liệu, cài đặt và bộ nhớ đệm của trình chỉnh sửa, tùy thuộc vào nền tảng. Theo mặc định, các đường dẫn này là:

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

- **Dữ liệu trình chỉnh sửa** chứa các export template và dữ liệu dành riêng cho dự án.
- **Cài đặt trình chỉnh sửa** chứa tệp cấu hình cài đặt chính của trình chỉnh sửa, cùng nhiều tùy chỉnh khác dành riêng cho người dùng (bố cục trình chỉnh sửa, feature profiles, script templates, v.v.).
- **Bộ nhớ đệm** chứa dữ liệu do trình chỉnh sửa tạo ra hoặc lưu tạm thời. Bạn có thể xóa dữ liệu này an toàn khi Godot đã đóng.

Godot tuân thủ `XDG Base Directory Specification <https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html>`__ trên Linux/\*BSD. Bạn có thể ghi đè các biến môi trường ``XDG_DATA_HOME``, ``XDG_CONFIG_HOME`` và ``XDG_CACHE_HOME`` để thay đổi đường dẫn dữ liệu của trình chỉnh sửa và dự án.

.. note:: Nếu bạn sử dụng `Godot packaged as a Flatpak <https://flathub.org/apps/details/org.godotengine.Godot>`__, các đường dẫn dữ liệu của trình chỉnh sửa sẽ nằm trong các thư mục con của ``~/.var/app/org.godotengine.Godot/``.

.. _doc_data_paths_self_contained_mode:

Chế độ độc lập
~~~~~~~~~~~~~~

Nếu bạn tạo một tệp có tên ``._sc_`` hoặc ``_sc_`` trong cùng thư mục với tệp nhị phân của trình chỉnh sửa (hoặc trong `MacOS/Contents/` đối với gói ứng dụng .app của trình chỉnh sửa macOS), Godot sẽ bật *chế độ độc lập*. Chế độ này khiến Godot ghi toàn bộ dữ liệu, cài đặt và bộ nhớ đệm của trình chỉnh sửa vào một thư mục có tên ``editor_data/`` trong cùng thư mục với tệp nhị phân của trình chỉnh sửa. Bạn có thể dùng chế độ này để tạo một bản cài đặt trình chỉnh sửa có tính di động.

`Bản phát hành Godot trên Steam <https://store.steampowered.com/app/404790/>`__ sử dụng chế độ độc lập theo mặc định.

.. UPDATE: Not supported yet. When self-contained mode is supported in exported
.. projects, remove or update this note.

.. note::

    Chế độ độc lập hiện chưa được hỗ trợ trong các dự án đã export. Để đọc và ghi các tệp tương đối so với đường dẫn của tệp thực thi, hãy sử dụng
    :ref:`OS.get_executable_path() <class_OS_method_get_executable_path>`. Lưu ý rằng việc ghi tệp vào đường dẫn thực thi chỉ hoạt động nếu tệp thực thi được đặt trong một vị trí có thể ghi (tức là **không phải** Program Files hoặc một thư mục khác chỉ cho phép người dùng thông thường đọc).
