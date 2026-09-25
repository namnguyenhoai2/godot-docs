:allow_comments: False

.. _doc_c_sharp:

C#/.NET
=======

C# là một ngôn ngữ lập trình cấp cao do Microsoft phát triển. Godot hỗ trợ C# như một lựa chọn ngôn ngữ scripting, bên cạnh
:ref:`GDScript <doc_gdscript>`.

Tệp thực thi Godot tiêu chuẩn không tích hợp sẵn hỗ trợ C#. Thay vào đó, để bật hỗ trợ C# cho dự án, bạn cần `tải xuống phiên bản .NET <https://godotengine.org/download/>`_ của trình chỉnh sửa từ trang web Godot.

.. toctree::
   :maxdepth: 1
   :name: toc-learn-scripting-C#

   c_sharp_basics
   c_sharp_features
   c_sharp_style_guide
   diagnostics/index

API Godot cho C#
----------------

Là một game engine đa dụng, Godot cung cấp một số tính năng cấp cao như một phần của API. Các bài viết dưới đây giải thích cách những tính năng này tích hợp với C# và API C# có thể khác GDScript như thế nào.

.. toctree::
   :maxdepth: 1
   :name: toc-learn-scripting-C#-differences

   c_sharp_differences
   c_sharp_collections
   c_sharp_variant
   c_sharp_signals
   c_sharp_exports
   c_sharp_global_classes

.. _doc_c_sharp_platforms:

Hỗ trợ nền tảng C#
------------------

.. seealso::

    Xem :ref:`doc_system_requirements` để biết các yêu cầu về phiên bản phần cứng và phần mềm đối với game engine Godot.

.. note::

    Vì các dự án C# sử dụng runtime .NET, bạn cũng cần kiểm tra yêu cầu hệ thống đối với phiên bản .NET mà bạn sẽ sử dụng. Xem `hệ điều hành được hỗ trợ <https://github.com/dotnet/core/tree/main/release-notes#supported-os>`_.

Kể từ Godot 4.2, các dự án viết bằng C# hỗ trợ tất cả nền tảng máy tính để bàn (Windows, Linux và macOS), cũng như Android và iOS.

Hiện tại, hỗ trợ Android vẫn đang ở trạng thái thử nghiệm.

Hiện tại, hỗ trợ iOS vẫn đang ở trạng thái thử nghiệm và có một số hạn chế.

- Các export template chính thức cho trình mô phỏng iOS chỉ hỗ trợ kiến trúc ``x64``.

- Chỉ có thể export sang iOS từ thiết bị macOS.

Hiện tại, các dự án viết bằng C# không thể được export sang nền tảng web. Để sử dụng C# trên nền tảng đó, hãy cân nhắc sử dụng Godot 3.

.. _`download a .NET version`: https://godotengine.org/download/
.. _`supported OS`: https://github.com/dotnet/core/tree/main/release-notes#supported-os
