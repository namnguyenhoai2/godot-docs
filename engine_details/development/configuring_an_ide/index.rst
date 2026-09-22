:allow_comments: False

.. _doc_configuring_an_ide:

Cấu hình một IDE
================

Chúng tôi giả định rằng bạn đã `cloned <https://github.com/godotengine/godot>`_ và :ref:`compiled <toc-devel-compiling>` Godot.

Bạn có thể dễ dàng phát triển Godot bằng bất kỳ trình soạn thảo văn bản nào và gọi ``scons`` trên dòng lệnh, nhưng nếu muốn làm việc với một IDE (Môi trường phát triển tích hợp), dưới đây là hướng dẫn thiết lập cho một số IDE phổ biến:

.. toctree::
   :maxdepth: 1
   :name: toc-devel-configuring_an_ide

   android_studio
   clion
   code_blocks
   kdevelop
   qt_creator
   rider
   visual_studio
   visual_studio_code
   xcode

Bạn cũng có thể sử dụng các IDE khác, nhưng cách thiết lập cho chúng vẫn chưa được ghi lại.

Nếu trình soạn thảo của bạn hỗ trợ `language server protocol <https://microsoft.github.io/language-server-protocol/>`__, bạn có thể sử dụng `clangd <https://clangd.llvm.org>`__ để hoàn tất mã, chẩn đoán lỗi và hơn thế nữa. Bạn có thể tạo cơ sở dữ liệu biên dịch để sử dụng với clangd theo một trong hai cách sau:

.. code-block:: shell

   # Tạo compile_commands.json trong khi biên dịch
   scons compiledb=yes

   # Tạo compile_commands.json mà không biên dịch
   scons compiledb=yes compile_commands.json

.. _`cloned`: https://github.com/godotengine/godot
