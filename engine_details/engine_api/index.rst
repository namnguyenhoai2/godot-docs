:allow_comments: False

.. _doc_engine_module_api:

API mở rộng engine
==================

Phần này giới thiệu nhiều cách khác nhau để bạn mở rộng engine bằng mã C++. Bạn có thể sử dụng các API này bằng cách tạo một :ref:`module <doc_custom_modules_in_cpp>`. Lưu ý rằng bạn có thể thay đổi engine theo nhiều cách hơn những cách được trình bày ở đây — phần này chỉ giới thiệu một số cách phổ biến và hữu ích để thực hiện việc đó.

Ngoài ra, một số hàm được trình bày ở đây cũng có sẵn thông qua
:ref:`GDExtension <doc_what_is_gdextension>` API. Bạn có thể sử dụng chúng trong C++ bằng cách tạo một GDExtension dựa trên :ref:`godot-cpp <doc_about_godot_cpp>`, hoặc với bất kỳ :ref:`triển khai GDExtension nào do cộng đồng tạo <doc_scripting_languages>`. Tuy nhiên, lưu ý rằng một số khía cạnh của mã hoặc cấu trúc thư mục có thể khác trong GDExtension so với các API module.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-cpp-source-advanced

   custom_modules_in_cpp
   vendor_runtime_module
   gdextension/index
   binding_to_external_libraries
   custom_resource_format_loaders
   custom_audiostreams
   custom_platform_ports
