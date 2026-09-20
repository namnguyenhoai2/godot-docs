:allow_comments: False

.. _doc_compiling_index:

Xây dựng từ mã nguồn
====================

.. highlight:: shell

Godot tự hào vì việc xây dựng rất dễ dàng theo tiêu chuẩn của các dự án C++.
:ref:`Godot uses the SCons build system <doc_faq_why_scons>`, and after the initial
thiết lập việc biên dịch engine cho nền tảng hiện tại của bạn sẽ dễ dàng như chạy:

::

    scons

Tuy nhiên, có lẽ bạn sẽ cần sử dụng ít nhất một số tùy chọn có sẵn để cấu hình bản build phù hợp với nhu cầu cụ thể của mình, dù đó là một nhánh engine tùy chỉnh, một bản build nhẹ đã lược bỏ các mô-đun bổ sung, hay một tệp thực thi nhắm đến việc phát triển engine.

Các bài viết dưới đây sẽ giúp bạn tìm hiểu các tùy chọn cấu hình hiện có, cũng như những điều kiện tiên quyết cần thiết để biên dịch Godot đúng theo cách bạn muốn.

.. rubric:: Basics of building Godot
   :heading-level: 2

Hãy bắt đầu với những điều cơ bản: tìm hiểu cách lấy mã nguồn của Godot, sau đó là những tùy chọn cần sử dụng để biên dịch mã nguồn này bất kể nền tảng đích của bạn là gì.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-compiling

   getting_source
   introduction_to_the_buildsystem

.. rubric:: Building for target platforms
   :heading-level: 2

Bên dưới, bạn có thể tìm thấy hướng dẫn biên dịch engine cho nền tảng đích cụ thể của mình. Lưu ý rằng Godot hỗ trợ biên dịch chéo, nghĩa là bạn có thể biên dịch cho một nền tảng đích không trùng với nền tảng hiện tại (ví dụ: nhắm đến Linux khi đang sử dụng Windows). Các hướng dẫn sẽ cố gắng bao quát mọi tình huống có thể xảy ra.

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

.. rubric:: Other compilation targets and options
   :heading-level: 2

Một số tùy chọn biên dịch chung bổ sung yêu cầu thiết lập thêm. Cụ thể, mặc dù Godot có hỗ trợ C#/.NET trong phần mã nguồn chính, tính năng này không được biên dịch theo mặc định để giảm kích thước tệp thực thi cho những người dùng không cần C# trong dự án của họ.

Các bài viết dưới đây giải thích cách cấu hình hệ thống build cho những trường hợp như vậy, đồng thời trình bày một số kỹ thuật tối ưu hóa.

.. toctree::
   :maxdepth: 1
   :name: toc-devel-compiling-options

   compiling_with_dotnet
   compiling_with_script_encryption_key
   optimizing_for_size
