:allow_comments: False

.. _doc_gdextension:

Hệ thống GDExtension
====================

**GDExtension** là một công nghệ dành riêng cho Godot, cho phép engine tương tác với các `thư viện dùng chung <https://en.wikipedia.org/wiki/Shared_library>`__ native trong thời gian chạy. Bạn có thể sử dụng công nghệ này để chạy mã native mà không cần biên dịch mã đó cùng với engine.

.. note:: GDExtension *không phải là* một ngôn ngữ scripting và không liên quan đến
          :ref:`GDScript <doc_gdscript>`.

Phần này mô tả cách GDExtension hoạt động và nhìn chung hướng đến những người muốn tạo một GDExtension từ đầu, chẳng hạn để tạo language bindings. Nếu bạn muốn sử dụng các language bindings hiện có, vui lòng tham khảo các bài viết khác, chẳng hạn như các bài viết về :ref:`C++ (godot-cpp) <doc_godot_cpp>` hoặc một trong số
:ref:`các language bindings do cộng đồng tạo ra <doc_what_is_gdnative_third_party_bindings>`.

.. toctree::
   :maxdepth: 1
   :name: toc-tutorials-gdextension

   what_is_gdextension
   gdextension_file
   gdextension_interface_json_file
   gdextension_c_example
