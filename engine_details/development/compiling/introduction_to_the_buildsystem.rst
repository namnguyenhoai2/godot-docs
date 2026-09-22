.. _doc_introduction_to_the_buildsystem:

Giới thiệu về hệ thống build
============================

.. highlight:: shell


Godot chủ yếu là một dự án C++ và :ref:`sử dụng hệ thống build SCons. <doc_faq_why_scons>` Chúng tôi yêu thích SCons vì khả năng bảo trì và sự dễ dàng khi thiết lập hệ thống build mà nó mang lại. Nhờ đó, việc biên dịch Godot từ mã nguồn có thể đơn giản như chạy:

::

    scons

Lệnh này tạo bản build editor cho nền tảng, hệ điều hành và kiến trúc hiện tại của bạn. Bạn có thể thay đổi những gì được build bằng cách chỉ định target, platform và/hoặc architecture. Ví dụ, để build một export template dùng để chạy các game đã export, bạn có thể chạy:

::

    scons target=template_release

Nếu dự định debug hoặc phát triển engine, bạn có thể muốn bật tùy chọn ``dev_build`` để bật mã debug chỉ dành cho việc phát triển:

::

    scons dev_build=yes

Các phần tiếp theo trong bài viết sẽ giải thích chi tiết hơn về những tùy chọn phổ biến này và các tùy chọn khác. Nhưng trước khi có thể biên dịch Godot, bạn cần cài đặt một số prerequisite. Vui lòng tham khảo tài liệu về platform để tìm hiểu thêm:

- :ref:`doc_compiling_for_android`
- :ref:`doc_compiling_for_ios`
- :ref:`doc_compiling_for_linuxbsd`
- :ref:`doc_compiling_for_macos`
- :ref:`doc_compiling_for_web`
- :ref:`doc_compiling_for_windows`

Các bài viết này trình bày rất chi tiết cả cách thiết lập môi trường để biên dịch Godot trên một platform cụ thể lẫn cách biên dịch cho platform đó. Bạn có thể tự do chuyển qua lại giữa các bài viết này và bài viết hiện tại để tham khảo các tùy chọn cấu hình dành riêng cho platform cũng như các tùy chọn phổ biến.

Sử dụng đa luồng
----------------

Quá trình build có thể mất một khoảng thời gian, tùy thuộc vào mức độ mạnh của hệ thống. Theo mặc định, thiết lập SCons của Godot được cấu hình để sử dụng tất cả các luồng CPU trừ một luồng (nhằm giữ cho hệ thống phản hồi trong quá trình biên dịch). Nếu hệ thống có 4 luồng CPU trở xuống, theo mặc định hệ thống sẽ sử dụng tất cả các luồng.

Nếu muốn điều chỉnh số luồng CPU mà SCons sẽ sử dụng, hãy dùng tham số ``-j<threads>`` để chỉ định số luồng được sử dụng cho bản build.

Ví dụ sử dụng 12 luồng:

::

    scons -j12

Chọn platform
-------------

Hệ thống build của Godot sẽ bắt đầu bằng cách phát hiện các platform mà nó có thể build cho. Nếu không được phát hiện, platform đó sẽ không xuất hiện trong danh sách các platform khả dụng. Các yêu cầu build cho từng platform được mô tả trong phần còn lại của mục hướng dẫn này.

SCons được gọi chỉ bằng cách gọi ``scons``. Nếu không chỉ định platform, SCons sẽ tự động phát hiện platform đích dựa trên platform host. Sau đó, nó sẽ bắt đầu build ngay cho platform đích.

Để liệt kê các platform đích khả dụng, hãy dùng ``scons platform=list``:

.. code:: text

    scons platform=list
    scons: Reading SConscript files ...
    The following platforms are available:

        android
        ios
        linuxbsd
        macos
        web
        windows

    Please run SCons again and select a valid platform: platform=<string>

Để build cho một platform (ví dụ: ``linuxbsd``), hãy chạy với đối số ``platform=`` (hoặc ``p=`` để viết ngắn gọn):

::

    scons platform=linuxbsd

.. _doc_introduction_to_the_buildsystem_resulting_binary:

Binary tạo ra
-------------

Các binary tạo ra sẽ được đặt trong thư mục con ``bin/``, thường theo quy ước đặt tên sau:

::

    godot.<platform>.<target>[.dev][.double].<arch>[.<extra_suffix>][.<ext>]

Đối với lần build trước đó, kết quả sẽ có dạng như sau:

.. code-block:: console

    ls bin
    bin/godot.linuxbsd.editor.x86_64

Điều này có nghĩa là binary dành cho Linux *hoặc* \*BSD (*không phải* cả hai), không được tối ưu hóa, được biên dịch với toàn bộ editor và dành cho 64 bit.

Một binary Windows với cùng cấu hình sẽ có dạng như sau:

.. code-block:: doscon

    C:\godot> dir bin/
    godot.windows.editor.64.exe

Bạn có thể sao chép binary đó đến bất kỳ vị trí nào, vì nó chứa Project Manager, editor và mọi thứ cần thiết để thực thi game. Tuy nhiên, nó thiếu dữ liệu để export game sang các platform khác nhau. Vì vậy, cần có các export template (có thể tải xuống từ `godotengine.org <https://godotengine.org/>`__, hoặc bạn có thể tự build chúng).

Ngoài ra, có một số tùy chọn tiêu chuẩn có thể thiết lập trong tất cả các target build và sẽ được giải thích bên dưới.

.. _doc_introduction_to_the_buildsystem_target:

Target
------

Tùy chọn ``target`` kiểm soát việc editor có được biên dịch hay không và có sử dụng các cờ debug hay không. Các mức tối ưu hóa (``optimize``) và việc mỗi bản build có chứa debug symbol hay không (``debug_symbols``) được điều khiển riêng với target. Mỗi chế độ có ý nghĩa như sau:

-  ``target=editor``: Build một binary editor (định nghĩa ``TOOLS_ENABLED`` và ``DEBUG_ENABLED``)
-  ``target=template_debug``: Build một debug export template (định nghĩa ``DEBUG_ENABLED``)
-  ``target=template_release``: Build một release export template

Editor được bật theo mặc định trong tất cả target PC (Linux, Windows, macOS) và bị tắt đối với mọi target khác. Việc tắt editor tạo ra một binary có thể chạy các project nhưng không bao gồm editor hoặc Project Manager.

Danh sách :ref:`đối số dòng lệnh <doc_command_line_tutorial>` khả dụng thay đổi tùy thuộc vào loại build.

::

    scons platform=<platform> target=editor|template_debug|template_release

.. _doc_introduction_to_the_buildsystem_development_and_production_aliases:

Bí danh development và production
---------------------------------

Khi tạo các bản build cho development (chạy các công cụ debug/:ref:`profiling <doc_using_cpp_profilers>`), bạn thường có các mục tiêu khác so với các bản build production (tạo binary nhanh và nhỏ nhất có thể).

Godot cung cấp hai bí danh cho mục đích này:

- ``dev_mode=yes`` là bí danh của ``verbose=yes warnings=extra werror=yes tests=yes``. Tùy chọn này bật hành vi warnings-as-errors (tương tự thiết lập continuous integration của Godot) và cũng build :ref:`unit test <doc_unit_testing>` để bạn có thể chạy chúng cục bộ.
- ``production=yes`` là bí danh của ``use_static_cpp=yes debug_symbols=no lto=auto``. Việc liên kết tĩnh libstdc++ cho khả năng portability của binary tốt hơn khi biên dịch cho Linux. Bí danh này cũng bật link-time optimization khi biên dịch cho Linux, Web và Windows với MinGW, nhưng giữ LTO ở trạng thái tắt khi biên dịch cho macOS, iOS hoặc Windows với MSVC. Điều này là do LTO trên các platform đó liên kết rất chậm hoặc gặp vấn đề với mã được tạo ra.

Bạn có thể ghi đè thủ công các tùy chọn từ những bí danh đó bằng cách chỉ định chúng trên cùng dòng lệnh với các giá trị khác. Ví dụ, bạn có thể sử dụng ``scons production=yes debug_symbols=yes`` để tạo các binary được tối ưu hóa cho production nhưng vẫn bao gồm debug symbol.

Dev build
---------

.. note::

    ``dev_build`` nên **không** bị nhầm lẫn với ``dev_mode``, vốn là bí danh cho một số tùy chọn liên quan đến phát triển (xem ở trên).

Khi phát triển engine, có thể sử dụng tùy chọn ``dev_build`` cùng với ``target`` để bật mã dành riêng cho dev. ``dev_build`` định nghĩa ``DEV_ENABLED``, tắt tối ưu hóa (``-O0``/``/0d``), bật việc tạo debug symbol và không định nghĩa ``NDEBUG`` (để ``assert()`` hoạt động trong các thư viện thirdparty).

::

    scons platform=<platform> dev_build=yes

Cờ này thêm hậu tố ``.dev`` (dành cho development) vào tên binary được tạo ra.

.. seealso::

    Có thêm các tùy chọn SCons để bật *sanitizer*, là những công cụ có thể bật khi biên dịch để debug tốt hơn một số vấn đề nhất định của engine. Xem :ref:`doc_using_sanitizers` để biết thêm thông tin.

.. _doc_introduction_to_the_buildsystem_debugging_symbols:

Debug symbol
------------

Theo mặc định, ``debug_symbols=no`` được sử dụng, nghĩa là **không** có debug symbol trong các binary đã biên dịch. Sử dụng ``debug_symbols=yes`` để đưa debug symbol vào các binary đã biên dịch, cho phép debugger và profiler hoạt động chính xác. Debug symbol cũng cần thiết để stacktrace khi crash của Godot hiển thị tham chiếu đến các tệp và dòng mã nguồn.

Nhược điểm là các symbol debug là những tệp lớn (lớn hơn đáng kể so với chính các binary). Do đó, các binary chính thức hiện không bao gồm symbol debug. Điều này có nghĩa là bạn cần tự biên dịch Godot để có quyền truy cập vào các symbol debug.

Khi sử dụng ``debug_symbols=yes``, bạn cũng có thể sử dụng ``separate_debug_symbols=yes`` để đưa thông tin debug vào một tệp riêng có hậu tố ``.debug``. Điều này cho phép phân phối độc lập cả hai tệp. Lưu ý rằng trên Windows, khi biên dịch bằng MSVC, thông tin debug *luôn* được ghi vào một tệp ``.pdb`` riêng bất kể ``separate_debug_symbols``.

.. tip::

    Sử dụng lệnh ``strip <path/to/binary>`` để xóa các symbol debug khỏi một binary mà bạn đã biên dịch.

Mức độ tối ưu hóa
-----------------

Có thể chọn một trong các mức độ tối ưu hóa compiler sau:

- ``optimize=speed_trace`` *(mặc định khi nhắm đến các nền tảng không phải Web)*: Ưu tiên tốc độ thực thi với đánh đổi là kích thước binary lớn hơn. Việc tối ưu hóa đôi khi có thể ảnh hưởng tiêu cực đến việc sử dụng debugger (stack trace có thể kém chính xác hơn). Nếu bạn gặp trường hợp này, hãy sử dụng ``optimize=debug`` thay thế.
- ``optimize=speed``: Ưu tiên tốc độ thực thi cao hơn nữa, với đánh đổi là kích thước binary thậm chí còn lớn hơn so với ``optimize=speed_trace``. Khó debug hơn nữa so với ``optimize=debug``, vì mức này sử dụng các tối ưu hóa mạnh nhất hiện có.
- ``optimize=size`` *(mặc định khi nhắm đến nền tảng Web)*: Ưu tiên binary nhỏ với đánh đổi là tốc độ thực thi chậm hơn.
- ``optimize=size_extra``: Ưu tiên binary thậm chí còn nhỏ hơn, với đánh đổi là tốc độ thực thi thậm chí còn chậm hơn so với ``optimize=size``.
- ``optimize=debug``: Chỉ bật các tối ưu hóa không ảnh hưởng đến việc debug theo bất kỳ cách nào. Kết quả là binary nhanh hơn ``optimize=none``, nhưng chậm hơn ``optimize=speed_trace``.
- ``optimize=none``: Không thực hiện bất kỳ tối ưu hóa nào. Cách này cung cấp thời gian build nhanh nhất, nhưng thời gian thực thi chậm nhất.
- ``optimize=custom`` *(chỉ dành cho người dùng nâng cao)*: Không truyền các đối số tối ưu hóa cho compiler C/C++. Bạn sẽ phải truyền các đối số theo cách thủ công bằng các tùy chọn SCons ``cflags``, ``ccflags`` và ``cxxflags``.

Kiến trúc
---------

Tùy chọn ``arch`` dùng để kiểm soát phiên bản CPU hoặc OS mà binary được dự định chạy trên đó. Tùy chọn này chủ yếu tập trung vào các nền tảng desktop và bị bỏ qua ở mọi nơi khác.

Các giá trị được hỗ trợ cho tùy chọn ``arch`` là **auto**, **x86_32**, **x86_64**, **arm32**, **arm64**, **rv64**, **ppc32**, **ppc64** và **wasm32**.

::

    scons platform=<platform> arch={auto|x86_32|x86_64|arm32|arm64|rv64|ppc32|ppc64|wasm32}

Flag này nối giá trị của ``arch`` vào các binary kết quả khi thích hợp. Giá trị mặc định ``arch=auto`` sẽ phát hiện kiến trúc phù hợp với nền tảng host.

.. _doc_buildsystem_custom_modules:

Module tùy chỉnh
----------------

Có thể biên dịch các module nằm bên ngoài cây thư mục của Godot cùng với các module tích hợp sẵn.

Có thể truyền tùy chọn build ``custom_modules`` vào command line trước khi biên dịch. Tùy chọn này biểu thị một danh sách phân tách bằng dấu phẩy gồm các đường dẫn thư mục chứa một tập hợp các module C++ độc lập, có thể được xem như các package C++, tương tự thư mục ``modules/`` tích hợp sẵn.

Ví dụ, bạn có thể cung cấp các đường dẫn tương đối, tuyệt đối và đường dẫn thư mục người dùng chứa những module như vậy:

::

    scons custom_modules="../modules,/abs/path/to/modules,~/src/godot_modules"

.. note::

    Nếu có module tùy chỉnh có tên thư mục trùng khớp chính xác với một module tích hợp sẵn, engine sẽ chỉ biên dịch module tùy chỉnh đó. Có thể sử dụng logic này để ghi đè các triển khai module tích hợp sẵn.

.. seealso::

    :ref:`doc_custom_modules_in_cpp`

Dọn dẹp các tệp được tạo
------------------------

Đôi khi, bạn có thể gặp lỗi do các tệp được tạo vẫn tồn tại. Bạn có thể xóa chúng bằng cách sử dụng ``scons --clean <options>``, trong đó ``<options>`` là danh sách các tùy chọn build mà trước đó bạn đã sử dụng để build Godot.

Ngoài ra, bạn có thể sử dụng ``git clean -fixd``, thao tác này sẽ dọn dẹp các build artifact cho mọi nền tảng và cấu hình. Hãy cẩn thận vì thao tác này sẽ xóa tất cả các tệp chưa được theo dõi và bị ignore trong repository. Đừng chạy lệnh này nếu bạn có công việc chưa commit!

Các tùy chọn build khác
-----------------------

Có một số tùy chọn build khác mà bạn có thể sử dụng để cấu hình cách Godot được build (compiler, tùy chọn debug, v.v.) cũng như các tính năng cần bao gồm/tắt.

Kiểm tra output của ``scons --help`` để biết chi tiết về từng tùy chọn cho phiên bản mà bạn muốn biên dịch.

.. _doc_overriding_build_options:

Ghi đè các tùy chọn build
~~~~~~~~~~~~~~~~~~~~~~~~~

Sử dụng tệp
^^^^^^^^^^^

Có thể tạo tệp ``custom.py`` mặc định tại thư mục gốc của source Godot Engine để khởi tạo mọi tùy chọn build SCons được truyền qua command line:

.. code-block:: python
    :caption: custom.py

    optimize = "size"
    module_mono_enabled = "yes"
    use_llvm = "yes"
    extra_suffix = "game_title"

Bạn cũng có thể tắt một số module tích hợp sẵn trước khi biên dịch, giúp tiết kiệm thời gian build engine. Xem trang :ref:`doc_optimizing_for_size` để biết thêm chi tiết.

.. seealso::

    Bạn có thể sử dụng `trình tạo tùy chọn build Godot <https://godot-build-options-generator.github.io/>`__ trực tuyến để tạo tệp ``custom.py`` chứa các tùy chọn SCons. Sau đó, bạn có thể lưu tệp này và đặt nó tại thư mục gốc của thư mục source Godot.

Có thể chỉ định rõ một tệp tùy chỉnh khác bằng tùy chọn command line ``profile``, đồng thời ghi đè cấu hình build mặc định:

.. code-block:: shell

    scons profile=path/to/custom.py

.. note:: Các tùy chọn build được thiết lập từ tệp có thể bị ghi đè bằng các tùy chọn command line.

Bạn cũng có thể ghi đè các tùy chọn theo điều kiện:

.. code-block:: python
    :caption: custom.py

    import version

    # Ghi đè các tùy chọn dành riêng cho phiên bản Godot 3.x và 4.x.
    if version.major == 3:
        pass
    elif version.major == 4:
        pass

Sử dụng SCONSFLAGS
^^^^^^^^^^^^^^^^^^

``SCONSFLAGS`` là một biến môi trường được SCons sử dụng để tự động thiết lập các tùy chọn mà không cần cung cấp chúng qua command line.

Ví dụ, bạn có thể muốn buộc sử dụng một số lượng CPU thread nhất định với tùy chọn ``-j`` nói trên cho tất cả các bản build sau này:

.. tabs::
 .. code-tab:: bash Linux/macOS

     export SCONSFLAGS="-j4"

 .. code-tab:: bat Windows (cmd)

     set SCONSFLAGS=-j4

 .. code-tab:: powershell Windows (PowerShell)

     $env:SCONSFLAGS="-j4"

Build SCU (single compilation unit)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các bản build thông thường thường bị nghẽn do phải include số lượng lớn header trong mỗi translation unit. Chủ yếu để tăng tốc quá trình phát triển (thay vì các bản build production), Godot cung cấp bản build "single compilation unit" (còn gọi là bản build "Unity / Jumbo").

Đối với các thư mục được tăng tốc bằng tùy chọn này, nhiều tệp ``.cpp`` được biên dịch trong mỗi translation unit, nhờ đó các header có thể được chia sẻ giữa nhiều tệp, giúp giảm đáng kể thời gian build.

Để thực hiện build SCU, hãy sử dụng tùy chọn SCons ``scu_build=yes``.

.. note:: Khi phát triển một pull request bằng các bản build SCU, hãy nhớ thực hiện một bản build thông thường trước khi gửi PR. Lý do là các bản build SCU về bản chất bao gồm các header từ những ``.cpp`` tệp trước đó trong đơn vị biên dịch, do đó sẽ không phát hiện tất cả các include cần thiết trong một bản build thông thường. CI sẽ phát hiện các lỗi này, nhưng thường sẽ nhanh hơn nếu bạn phát hiện chúng bằng một bản build cục bộ trên máy của mình.

Các template export
-------------------

Các template export chính thức được tải xuống từ trang web của Godot Engine: `godotengine.org <https://godotengine.org/>`__. Tuy nhiên, bạn có thể muốn tự build chúng (trong trường hợp muốn có các template mới hơn, đang sử dụng các module tùy chỉnh hoặc đơn giản là không tin tưởng vào bản thân).

Nếu tải xuống package template export chính thức và giải nén, bạn sẽ nhận thấy rằng hầu hết các tệp là binary hoặc package đã được tối ưu hóa cho từng nền tảng:

.. code-block:: none

    android_debug.apk
    android_release.apk
    android_source.zip
    ios.zip
    linux_debug.arm32
    linux_debug.arm64
    linux_debug.x86_32
    linux_debug.x86_64
    linux_release.arm32
    linux_release.arm64
    linux_release.x86_32
    linux_release.x86_64
    macos.zip
    version.txt
    web_debug.zip
    web_dlink_debug.zip
    web_dlink_nothreads_debug.zip
    web_dlink_nothreads_release.zip
    web_dlink_release.zip
    web_nothreads_debug.zip
    web_nothreads_release.zip
    web_release.zip
    windows_debug_x86_32_console.exe
    windows_debug_x86_32.exe
    windows_debug_x86_64_console.exe
    windows_debug_x86_64.exe
    windows_debug_arm64_console.exe
    windows_debug_arm64.exe
    windows_release_x86_32_console.exe
    windows_release_x86_32.exe
    windows_release_x86_64_console.exe
    windows_release_x86_64.exe
    windows_release_arm64_console.exe
    windows_release_arm64.exe

Để tự tạo các template đó, hãy làm theo hướng dẫn chi tiết cho từng nền tảng trong cùng phần hướng dẫn này. Mỗi nền tảng đều giải thích cách tạo template riêng.

Tệp ``version.txt`` phải chứa mã định danh phiên bản Godot tương ứng. Tệp này được dùng để cài đặt các template export vào một thư mục dành riêng cho từng phiên bản nhằm tránh xung đột. Ví dụ, nếu bạn đang build các template export cho Godot 4.4.1, ``version.txt`` phải chứa ``4.4.1.stable`` trên dòng đầu tiên (và không có gì khác). Mã định danh phiên bản này dựa trên các dòng ``major``, ``minor``, ``patch`` (nếu có) và ``status`` của tệp `version.py trong kho Git của Godot <https://github.com/godotengine/godot/blob/master/version.py>`__.

Nếu phát triển cho nhiều nền tảng, macOS chắc chắn là nền tảng máy chủ thuận tiện nhất cho việc cross-compile, vì bạn có thể cross-compile cho mọi mục tiêu. Linux và Windows đứng thứ hai, nhưng Linux có lợi thế là nền tảng dễ thiết lập việc này hơn.
