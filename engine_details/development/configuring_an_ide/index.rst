:allow_comments: False

.. _doc_configuring_an_ide:

Cấu hình IDE
============

Chúng tôi giả định rằng bạn đã `cloned <https://github.com/godotengine/godot>`_ và :ref:`compiled <toc-devel-compiling>` Godot.

Bạn có thể dễ dàng phát triển Godot bằng bất kỳ trình soạn thảo văn bản nào và bằng cách gọi ``scons`` trên dòng lệnh, nhưng nếu muốn làm việc với một IDE (Môi trường Phát triển Tích hợp), dưới đây là hướng dẫn thiết lập cho một số IDE phổ biến:

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

Bạn có thể sử dụng các IDE khác, nhưng hiện chưa có tài liệu hướng dẫn thiết lập cho chúng.

Bạn có thể sử dụng `clangd <https://clangd.llvm.org>`__ để hoàn thành mã, chẩn đoán lỗi và nhiều tính năng khác nếu trình soạn thảo của bạn hỗ trợ `language server protocol <https://microsoft.github.io/language-server-protocol/>`__. Bạn có thể tạo cơ sở dữ liệu biên dịch để sử dụng với clangd theo một trong hai cách sau:

.. code-block:: shell

   # Generate compile_commands.json while compiling
   scons compiledb=yes

   # Generate compile_commands.json without compiling
   scons compiledb=yes compile_commands.json
