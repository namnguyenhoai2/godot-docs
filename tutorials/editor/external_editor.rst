.. _doc_external_editor:

Sử dụng trình soạn thảo văn bản bên ngoài
=========================================

Trang này giải thích cách lập trình bằng trình soạn thảo văn bản bên ngoài.

.. note::

    Để lập trình C# trong trình soạn thảo bên ngoài, hãy xem
    :ref:`hướng dẫn C# để cấu hình trình soạn thảo bên ngoài <doc_c_sharp_setup_external_editor>`.

Godot có thể được sử dụng với trình soạn thảo văn bản bên ngoài, chẳng hạn như Sublime Text hoặc Visual Studio Code. Đi đến phần cài đặt của trình soạn thảo tương ứng: **Editor > Editor Settings > Text Editor > External**

.. figure:: img/editor_external_editor_settings.webp
   :align: center
   :alt: Phần Text Editor > External của Editor Settings

   Phần **Text Editor > External** của Editor Settings

Có hai trường văn bản: đường dẫn đến tệp thực thi và các cờ dòng lệnh. Các cờ này cho phép bạn tích hợp trình soạn thảo với Godot, truyền cho trình soạn thảo đường dẫn tệp cần mở và các đối số liên quan khác. Godot sẽ thay thế các placeholder sau trong chuỗi cờ:

+-------------------------+---------------------------------------+
| Trường trong Exec Flags | Được thay thế bằng                    |
+=========================+=======================================+
| ``{project}``           | Đường dẫn tuyệt đối đến thư mục dự án |
+-------------------------+---------------------------------------+
| ``{file}``              | Đường dẫn tuyệt đối đến tệp           |
+-------------------------+---------------------------------------+
| ``{col}``               | Số cột của lỗi                        |
+-------------------------+---------------------------------------+
| ``{line}``              | Số dòng của lỗi                       |
+-------------------------+---------------------------------------+

Một số **Exec Flags** mẫu cho các trình soạn thảo khác nhau:

+--------------------+------------------------------------------+
| Trình soạn thảo    | Exec Flags                               |
+====================+==========================================+
| Geany/Kate         | ``{file} --line {line} --column {col}``  |
+--------------------+------------------------------------------+
| Atom               | ``{file}:{line}``                        |
+--------------------+------------------------------------------+
| JetBrains Rider    | ``{project} --line {line} {file}``       |
+--------------------+------------------------------------------+
| Visual Studio Code | ``{project} --goto {file}:{line}:{col}`` |
+--------------------+------------------------------------------+
| Vim (gVim)         | ``"+call cursor({line}, {col})" {file}`` |
+--------------------+------------------------------------------+
| Emacs              | ``emacs +{line}:{col} {file}``           |
+--------------------+------------------------------------------+
| Sublime Text/Zed   | ``{project} {file}:{line}:{col}``        |
+--------------------+------------------------------------------+
| Visual Studio*     | ``/edit "{file}"``                       |
+--------------------+------------------------------------------+

\*: Các đối số không được tự động phát hiện, vì vậy bạn phải điền chúng theo cách thủ công.

Kể từ Godot 4.5, **Exec Flags** được tự động phát hiện cho tất cả các trình soạn thảo được liệt kê ở trên (trừ những trình soạn thảo được đánh dấu bằng dấu hoa thị). Bạn không cần dán chúng từ trang này để sử dụng, trừ khi trình soạn thảo của bạn có tên tệp thực thi không được tự động nhận diện (ví dụ: một bản fork của trình soạn thảo được liệt kê ở đây).

.. note::

    Đối với Visual Studio Code trên Windows, bạn sẽ phải trỏ đến tệp ``code.cmd``.

    Đối với Emacs, bạn có thể gọi ``emacsclient`` thay cho ``emacs`` nếu sử dụng server mode.

    Đối với Visual Studio, bạn sẽ phải mở tệp solution ``.sln`` theo cách thủ công để truy cập các tính năng của IDE. Ngoài ra, trình soạn thảo sẽ không đi đến một dòng cụ thể.

Tự động tải lại các thay đổi của bạn
------------------------------------
Để Godot Editor tự động tải lại mọi script đã được trình soạn thảo văn bản bên ngoài thay đổi, hãy bật **Editor > Editor Settings > Text Editor > Behavior > Auto Reload Scripts on External Change**.

Sử dụng External Editor trong Debugger
--------------------------------------

Việc sử dụng trình soạn thảo bên ngoài trong debugger được xác định bởi một tùy chọn riêng trong phần cài đặt. Để biết chi tiết, hãy xem :ref:`các công cụ và tùy chọn debug của trình soạn thảo script <doc_debugger_tools_and_options>`.

Các plugin trình soạn thảo chính thức
-------------------------------------

Chúng tôi có các plugin chính thức cho những trình soạn thảo mã sau:

- `Visual Studio Code <https://github.com/godotengine/godot-vscode-plugin>`_
- `Emacs <https://github.com/godotengine/emacs-gdscript-mode>`_

Hỗ trợ LSP/DAP
--------------

Godot hỗ trợ `Language Server Protocol <https://microsoft.github.io/language-server-protocol/>`_ (**LSP**) để hoàn tất mã và `Debug Adapter Protocol <https://microsoft.github.io/debug-adapter-protocol/>`_ (**DAP**) để debug. Bạn có thể kiểm tra `danh sách client LSP <https://microsoft.github.io/language-server-protocol/implementors/tools/>`_ và `danh sách client DAP <https://microsoft.github.io/debug-adapter-protocol/implementors/tools/>`_ để xem trình soạn thảo của bạn có hỗ trợ chúng hay không. Nếu có, bạn sẽ có thể tận dụng các tính năng này mà không cần plugin tùy chỉnh.

Để sử dụng các protocol này, một instance Godot phải đang chạy trong dự án hiện tại của bạn. Sau đó, bạn nên cấu hình trình soạn thảo để giao tiếp với các cổng adapter đang chạy trong Godot, theo mặc định là ``6005`` cho **LSP**, và ``6006`` cho **DAP**. Bạn có thể thay đổi các cổng này và những cài đặt khác trong **Editor Settings**, lần lượt tại các phần **Network > Language Server** và **Network > Debug Adapter**.

Dưới đây là một số bước cấu hình cho các trình soạn thảo cụ thể:

Visual Studio Code
~~~~~~~~~~~~~~~~~~

Bạn cần cài đặt `plugin Visual Studio Code chính thức <https://github.com/godotengine/godot-vscode-plugin>`_.

Đối với **LSP**, hãy làm theo `hướng dẫn này <https://github.com/godotengine/godot-vscode-plugin#gdscript_lsp_server_port>`_ để thay đổi cổng LSP mặc định. Bạn có thể kiểm tra trạng thái kết nối trên thanh trạng thái:

.. image:: img/lsp_vscode_status.png

Đối với **DAP**, hãy chỉ định thuộc tính ``debugServer`` trong tệp ``launch.json`` của bạn:

.. code-block:: json

    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "GDScript Godot",
                "type": "godot",
                "request": "launch",
                "project": "${workspaceFolder}",
                "port": 6007,
                "debugServer": 6006,
            }
        ]
    }

Emacs
~~~~~

Hãy xem hướng dẫn chính thức để cấu hình `LSP <https://github.com/godotengine/emacs-gdscript-mode#auto-completion-with-the-language-server-protocol-lsp>`_ và `DAP <https://github.com/godotengine/emacs-gdscript-mode#using-the-debugger>`_.

.. _`Visual Studio Code`: https://github.com/godotengine/godot-vscode-plugin
.. _`Emacs`: https://github.com/godotengine/emacs-gdscript-mode
.. _`Language Server Protocol`: https://microsoft.github.io/language-server-protocol/
.. _`Debug Adapter Protocol`: https://microsoft.github.io/debug-adapter-protocol/
.. _`LSP client list`: https://microsoft.github.io/language-server-protocol/implementors/tools/
.. _`DAP client list`: https://microsoft.github.io/debug-adapter-protocol/implementors/tools/
.. _`Visual Studio Code plugin`: https://github.com/godotengine/godot-vscode-plugin
.. _`these instructions`: https://github.com/godotengine/godot-vscode-plugin#gdscript_lsp_server_port
.. _`LSP`: https://github.com/godotengine/emacs-gdscript-mode#auto-completion-with-the-language-server-protocol-lsp
.. _`DAP`: https://github.com/godotengine/emacs-gdscript-mode#using-the-debugger
