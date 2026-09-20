:allow_comments: False

.. _doc_gdextension:

Hệ thống GDExtension
====================

**GDExtension** là một công nghệ dành riêng cho Godot, cho phép engine tương tác với các `thư viện dùng chung <https://en.wikipedia.org/wiki/Shared_library>`__ gốc trong thời gian chạy. Bạn có thể sử dụng công nghệ này để chạy mã gốc mà không cần biên dịch mã đó cùng với engine.

.. note:: GDExtension is *not* a scripting language and has no relation to
          :ref:`GDScript <doc_gdscript>`.

Phần này mô tả cách GDExtension hoạt động và nhìn chung dành cho những người muốn tự xây dựng một GDExtension từ đầu, chẳng hạn như để tạo các binding ngôn ngữ. Nếu bạn muốn sử dụng các binding ngôn ngữ hiện có, vui lòng tham khảo các bài viết khác, chẳng hạn như các bài viết về :ref:`C++ (godot-cpp) <doc_godot_cpp>` hoặc một trong các
:ref:`community-made ones <doc_what_is_gdnative_third_party_bindings>`.

.. toctree::
   :maxdepth: 1
   :name: toc-tutorials-gdextension

   what_is_gdextension
   gdextension_file
   gdextension_interface_json_file
   gdextension_c_example
