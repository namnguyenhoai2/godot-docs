:allow_comments: False

.. _doc_compiling_index:

Xây dựng từ mã nguồn
====================

.. highlight:: shell

Godot tự hào vì rất dễ build theo tiêu chuẩn của các dự án C++.
:ref:`Godot sử dụng hệ thống build SCons <doc_faq_why_scons>`, và sau khi hoàn tất thiết lập ban đầu, việc biên dịch engine cho nền tảng hiện tại của bạn sẽ dễ dàng như chạy lệnh:

::

    scons

Tuy nhiên, có thể bạn sẽ cần sử dụng ít nhất một số tùy chọn hiện có để cấu hình bản build phù hợp với nhu cầu cụ thể, dù đó là một fork engine tùy chỉnh, một bản build nhẹ đã loại bỏ các module bổ sung, hay một executable nhắm đến việc phát triển engine.

Các bài viết dưới đây sẽ giúp bạn tìm hiểu các tùy chọn cấu hình hiện có, cũng như những điều kiện tiên quyết cần thiết để biên dịch Godot chính xác theo nhu cầu của bạn.

.. rubric:: Kiến thức cơ bản về build Godot
   :heading-level: 2

Hãy bắt đầu với những kiến thức cơ bản: tìm hiểu cách lấy mã nguồn Godot, sau đó tìm hiểu các tùy chọn cần sử dụng để biên dịch mã nguồn này bất kể nền tảng đích của bạn là gì.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-compiling

   getting_source
   introduction_to_the_buildsystem

.. rubric:: Build cho các nền tảng đích
   :heading-level: 2

Dưới đây là hướng dẫn biên dịch engine cho nền tảng đích cụ thể của bạn. Lưu ý rằng Godot hỗ trợ cross-compilation, nghĩa là bạn có thể biên dịch engine cho một nền tảng đích khác với nền tảng hiện tại (chẳng hạn, nhắm đến Linux khi đang sử dụng Windows). Các hướng dẫn sẽ cố gắng bao quát mọi tình huống có thể xảy ra.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-compiling-platforms

   compiling_for_windows
   compiling_for_linuxbsd
   compiling_for_macos
   compiling_for_android
   compiling_for_ios
   compiling_for_visionos
   compiling_for_web
   cross-compiling_for_ios_on_linux

.. rubric:: Các đích và tùy chọn biên dịch khác
   :heading-level: 2

Một số tùy chọn biên dịch bổ sung áp dụng trên mọi nền tảng cần được thiết lập thêm. Cụ thể, mặc dù Godot có hỗ trợ C#/.NET trong codebase chính, tính năng này không được biên dịch theo mặc định nhằm giảm kích thước executable cho những người dùng không cần C# trong dự án của mình.

Các bài viết dưới đây giải thích cách cấu hình buildsystem cho những trường hợp như vậy, đồng thời trình bày một số kỹ thuật tối ưu hóa.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-compiling-options

   compiling_with_dotnet
   compiling_with_script_encryption_key
   optimizing_for_size
