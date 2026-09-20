.. _doc_introduction_to_the_buildsystem:

Giới thiệu về buildsystem
=========================

.. highlight:: shell


Godot chủ yếu là một dự án C++ và nó :ref:`uses the SCons build system. <doc_faq_why_scons>` Chúng tôi yêu thích SCons vì tính dễ bảo trì và dễ thiết lập mà nó mang lại cho buildsystem của chúng tôi. Nhờ đó, việc biên dịch Godot từ mã nguồn có thể đơn giản như chạy:

::

    scons

Thao tác này tạo một bản build editor cho nền tảng, hệ điều hành và kiến trúc hiện tại của bạn. Bạn có thể thay đổi nội dung được build bằng cách chỉ định target, nền tảng và/hoặc kiến trúc. Ví dụ, để build một export template dùng cho việc chạy các game đã export, bạn có thể chạy:

::

    scons target=template_release

Nếu dự định debug hoặc phát triển engine, bạn có thể muốn bật tùy chọn ``dev_build`` để bật mã debug chỉ dành cho dev:

::

    scons dev_build=yes

Các phần tiếp theo trong bài viết sẽ giải thích chi tiết hơn về những tùy chọn phổ dụng này và các tùy chọn khác. Tuy nhiên, trước khi có thể biên dịch Godot, bạn cần cài đặt một số điều kiện tiên quyết. Vui lòng tham khảo tài liệu dành cho nền tảng để tìm hiểu thêm:

- :ref:`doc_compiling_for_android` - :ref:`doc_compiling_for_ios` - :ref:`doc_compiling_for_linuxbsd` - :ref:`doc_compiling_for_macos` - :ref:`doc_compiling_for_web` - :ref:`doc_compiling_for_windows`

Các bài viết này trình bày rất chi tiết cả cách thiết lập môi trường để biên dịch Godot trên một nền tảng cụ thể, lẫn cách biên dịch cho nền tảng đó. Bạn có thể thoải mái chuyển qua lại giữa các bài viết này và bài viết hiện tại để tham khảo các tùy chọn cấu hình dành riêng cho nền tảng cũng như các tùy chọn phổ dụng.

Sử dụng đa luồng
----------------

Quá trình build có thể mất một khoảng thời gian, tùy thuộc vào mức độ mạnh của hệ thống. Theo mặc định, thiết lập SCons của Godot được cấu hình để sử dụng tất cả các luồng CPU trừ một luồng (nhằm giữ cho hệ thống phản hồi trong quá trình biên dịch). Nếu hệ thống có 4 luồng CPU trở xuống, theo mặc định hệ thống sẽ sử dụng tất cả các luồng.

Nếu muốn điều chỉnh số luồng CPU mà SCons sử dụng, hãy dùng tham số ``-j<threads>`` để chỉ định số luồng sẽ được dùng cho bản build.

Ví dụ sử dụng 12 luồng:

::

    scons -j12

Lựa chọn nền tảng
-----------------

Build system của Godot sẽ bắt đầu bằng cách phát hiện các nền tảng mà nó có thể build. Nếu không được phát hiện, nền tảng đó sẽ không xuất hiện trong danh sách các nền tảng khả dụng. Các yêu cầu build cho từng nền tảng được mô tả trong phần còn lại của mục hướng dẫn này.

SCons được gọi chỉ bằng cách gọi ``scons``. Nếu không chỉ định nền tảng, SCons sẽ tự động phát hiện nền tảng target dựa trên nền tảng host. Sau đó, SCons sẽ ngay lập tức bắt đầu build cho nền tảng target.

Để liệt kê các nền tảng target khả dụng, hãy dùng ``scons platform=list``:

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

Để build cho một nền tảng (ví dụ: ``linuxbsd``), hãy chạy với đối số ``platform=`` (hoặc ``p=`` để viết ngắn):

::

    scons platform=linuxbsd

.. _doc_introduction_to_the_buildsystem_resulting_binary:

Binary tạo ra
-------------

Các binary tạo ra sẽ được đặt trong thư mục con ``bin/``, thường theo quy ước đặt tên sau:

::

    godot.<platform>.<target>[.dev][.double].<arch>[.<extra_suffix>][.<ext>]

Đối với lần thử build trước đó, kết quả sẽ có dạng như sau:

.. code-block:: console

    ls bin
    bin/godot.linuxbsd.editor.x86_64

Điều này có nghĩa binary dành cho Linux *hoặc* \*BSD (*không phải* cả hai), chưa được tối ưu hóa, có toàn bộ editor được biên dịch bên trong và dành cho 64 bit.

Một binary Windows với cùng cấu hình sẽ có dạng như sau:

.. code-block:: doscon

    C:\godot> dir bin/
    godot.windows.editor.64.exe

Sao chép binary đó đến bất kỳ vị trí nào bạn muốn, vì nó chứa Project Manager, editor và mọi thành phần cần thiết để thực thi game. Tuy nhiên, nó thiếu dữ liệu để export sang các nền tảng khác nhau. Để làm được điều đó, cần có các export template (có thể tải xuống từ `godotengine.org <https://godotengine.org/>`__, hoặc tự build chúng).

Ngoài ra, có một số tùy chọn tiêu chuẩn có thể được thiết lập trong tất cả các target build và sẽ được giải thích bên dưới.

.. _doc_introduction_to_the_buildsystem_target:

Target
------

Tùy chọn ``target`` kiểm soát việc editor có được biên dịch hay không và có sử dụng các cờ debug hay không. Các mức tối ưu hóa (``optimize``) và việc mỗi bản build có chứa debug symbol hay không (``debug_symbols``) được kiểm soát riêng với target. Mỗi chế độ có nghĩa là:

-  ``target=editor``: Build một editor binary (định nghĩa ``TOOLS_ENABLED`` và ``DEBUG_ENABLED``) - ``target=template_debug``: Build một debug export template (định nghĩa ``DEBUG_ENABLED``) - ``target=template_release``: Build một release export template

Editor được bật theo mặc định trong tất cả target PC (Linux, Windows, macOS) và bị tắt trong mọi target khác. Việc tắt editor tạo ra một binary có thể chạy các project nhưng không bao gồm editor hoặc Project Manager.

Danh sách :ref:`command line arguments <doc_command_line_tutorial>` khả dụng thay đổi tùy theo loại build.

::

    scons platform=<platform> target=editor|template_debug|template_release

.. _doc_introduction_to_the_buildsystem_development_and_production_aliases:

Bí danh dành cho development và production
------------------------------------------

Khi tạo các bản build cho development (chạy các công cụ debugging/:ref:`profiling <doc_using_cpp_profilers>`), bạn thường có các mục tiêu khác so với các bản build production (tạo binary nhanh và nhỏ nhất có thể).

Godot cung cấp hai bí danh cho mục đích này:

- ``dev_mode=yes`` là bí danh cho ``verbose=yes warnings=extra werror=yes tests=yes``. Bí danh này bật cơ chế warnings-as-errors (tương tự thiết lập continuous integration của Godot) và cũng build :ref:`unit tests <doc_unit_testing>` để bạn có thể chạy chúng cục bộ. - ``production=yes`` là bí danh cho ``use_static_cpp=yes debug_symbols=no lto=auto``. Việc liên kết tĩnh libstdc++ cho phép binary có tính di động tốt hơn khi biên dịch cho Linux. Bí danh này cũng bật link-time optimization khi biên dịch cho Linux, Web và Windows với MinGW, nhưng giữ LTO ở trạng thái tắt khi biên dịch cho macOS, iOS hoặc Windows với MSVC. Nguyên nhân là LTO trên các nền tảng đó liên kết rất chậm hoặc gặp vấn đề với mã được tạo ra.

Bạn có thể ghi đè thủ công các tùy chọn từ những bí danh đó bằng cách chỉ định chúng trên cùng dòng lệnh với các giá trị khác. Ví dụ, bạn có thể dùng ``scons production=yes debug_symbols=yes`` để tạo các binary được tối ưu hóa cho production nhưng vẫn bao gồm debug symbol.

Dev build
---------

.. note::

    ``dev_build`` **không nên** bị nhầm với ``dev_mode``, vốn là bí danh cho một số tùy chọn liên quan đến development (xem ở trên).

Khi phát triển engine, có thể sử dụng tùy chọn ``dev_build`` cùng với ``target`` để bật mã dành riêng cho dev. ``dev_build`` định nghĩa ``DEV_ENABLED``, tắt tối ưu hóa (``-O0``/``/0d``), bật việc tạo debug symbol và không định nghĩa ``NDEBUG`` (để ``assert()`` hoạt động trong các thư viện thirdparty).

::

    scons platform=<platform> dev_build=yes

Cờ này thêm hậu tố ``.dev`` (dành cho development) vào tên binary được tạo ra.

.. seealso::

    Có thêm các tùy chọn SCons để bật *sanitizer*, là những công cụ bạn có thể bật trong thời gian biên dịch nhằm debug tốt hơn một số vấn đề nhất định của engine. Xem :ref:`doc_using_sanitizers` để biết thêm thông tin.

.. _doc_introduction_to_the_buildsystem_debugging_symbols:

Debug symbol
------------

Theo mặc định, ``debug_symbols=no`` được sử dụng, nghĩa là **không** có debug symbol nào được đưa vào các binary đã biên dịch. Hãy dùng ``debug_symbols=yes`` để đưa debug symbol vào các binary đã biên dịch, cho phép debugger và profiler hoạt động chính xác. Debug symbol cũng cần thiết để stacktrace crash của Godot hiển thị tham chiếu đến các tệp và dòng mã nguồn.

Nhược điểm là debug symbol là các tệp lớn (lớn hơn đáng kể so với bản thân các binary). Vì vậy, các binary chính thức hiện không bao gồm debug symbol. Điều này có nghĩa là bạn cần tự biên dịch Godot để có quyền truy cập vào debug symbol.

Khi sử dụng ``debug_symbols=yes``, bạn cũng có thể dùng ``separate_debug_symbols=yes`` để đặt thông tin debug vào một tệp riêng với hậu tố ``.debug``. Điều này cho phép phân phối hai tệp độc lập với nhau. Lưu ý rằng trên Windows, khi biên dịch bằng MSVC, thông tin debug *luôn* được ghi vào một tệp ``.pdb`` riêng bất kể ``separate_debug_symbols``.

.. tip::

    Dùng lệnh ``strip <path/to/binary>`` để xóa debug symbol khỏi một binary mà bạn đã biên dịch.

Mức tối ưu hóa
--------------

Có thể chọn một trong các mức tối ưu hóa compiler sau:

- ``optimize=speed_trace`` *(mặc định khi target các nền tảng không phải Web)*: Ưu tiên tốc độ thực thi với đánh đổi là kích thước binary lớn hơn. Việc tối ưu hóa đôi khi có thể ảnh hưởng tiêu cực đến việc sử dụng debugger (stack trace có thể kém chính xác hơn. Nếu gặp trường hợp này, hãy dùng ``optimize=debug`` thay thế. - ``optimize=speed``: Ưu tiên tốc độ thực thi cao hơn nữa, với đánh đổi là kích thước binary còn lớn hơn so với ``optimize=speed_trace``. Ít thân thiện với việc debug hơn ``optimize=debug``, vì sử dụng các tối ưu hóa mạnh nhất hiện có. - ``optimize=size`` *(mặc định khi target nền tảng Web)*: Ưu tiên binary nhỏ với đánh đổi là tốc độ thực thi chậm hơn. - ``optimize=size_extra``: Ưu tiên binary còn nhỏ hơn nữa, với đánh đổi là tốc độ thực thi còn chậm hơn so với ``optimize=size``. - ``optimize=debug``: Chỉ bật các tối ưu hóa không ảnh hưởng đến việc debug theo bất kỳ cách nào. Kết quả là binary nhanh hơn ``optimize=none``, nhưng chậm hơn ``optimize=speed_trace``. - ``optimize=none``: Không thực hiện bất kỳ tối ưu hóa nào. Cách này mang lại thời gian build nhanh nhất nhưng thời gian thực thi chậm nhất. - ``optimize=custom`` *(chỉ dành cho người dùng nâng cao)*: Không truyền các đối số tối ưu hóa cho compiler C/C++. Bạn sẽ phải truyền các đối số thủ công bằng các tùy chọn SCons ``cflags``, ``ccflags`` và ``cxxflags``.

Kiến trúc
---------

Tùy chọn ``arch`` dùng để kiểm soát phiên bản CPU hoặc OS dự kiến sẽ chạy các binary. Tùy chọn này chủ yếu tập trung vào các nền tảng desktop và bị bỏ qua ở mọi nơi khác.

Các giá trị được hỗ trợ cho tùy chọn ``arch`` là **auto**, **x86_32**, **x86_64**, **arm32**, **arm64**, **rv64**, **ppc32**, **ppc64** và **wasm32**.

::

    scons platform=<platform> arch={auto|x86_32|x86_64|arm32|arm64|rv64|ppc32|ppc64|wasm32}

Cờ này sẽ nối giá trị của ``arch`` vào các tệp nhị phân tạo ra khi thích hợp. Giá trị mặc định ``arch=auto`` sẽ phát hiện kiến trúc khớp với nền tảng máy chủ.

.. _doc_buildsystem_custom_modules:

Mô-đun tùy chỉnh
----------------

Bạn có thể biên dịch các mô-đun nằm bên ngoài cây thư mục của Godot cùng với các mô-đun tích hợp sẵn.

Có thể truyền tùy chọn xây dựng ``custom_modules`` vào dòng lệnh trước khi biên dịch. Tùy chọn này biểu thị một danh sách đường dẫn thư mục được phân tách bằng dấu phẩy, chứa một tập hợp các mô-đun C++ độc lập có thể được xem như các gói C++, tương tự như thư mục ``modules/`` tích hợp sẵn.

Ví dụ, bạn có thể cung cấp các đường dẫn thư mục tương đối, tuyệt đối và thư mục người dùng chứa những mô-đun như vậy:

::

    scons custom_modules="../modules,/abs/path/to/modules,~/src/godot_modules"

.. note::

    Nếu có mô-đun tùy chỉnh có tên thư mục trùng khớp hoàn toàn với một mô-đun tích hợp sẵn, engine sẽ chỉ biên dịch mô-đun tùy chỉnh đó. Logic này có thể được dùng để ghi đè các phần triển khai mô-đun tích hợp sẵn.

.. seealso::

    :ref:`doc_custom_modules_in_cpp`

Dọn dẹp các tệp đã tạo
----------------------

Đôi khi, bạn có thể gặp lỗi do các tệp đã tạo vẫn còn tồn tại. Bạn có thể xóa chúng bằng cách sử dụng ``scons --clean <options>``, trong đó ``<options>`` là danh sách các tùy chọn xây dựng bạn đã dùng trước đó để xây dựng Godot.

Ngoài ra, bạn có thể sử dụng ``git clean -fixd``, lệnh này sẽ dọn dẹp các phần tử tạo tác xây dựng cho mọi nền tảng và cấu hình. Hãy cẩn thận vì lệnh này sẽ xóa tất cả các tệp chưa được theo dõi và bị bỏ qua trong kho lưu trữ. Đừng chạy lệnh này nếu bạn có công việc chưa commit!

Các tùy chọn xây dựng khác
--------------------------

Có một số tùy chọn xây dựng khác mà bạn có thể sử dụng để cấu hình cách Godot được xây dựng (trình biên dịch, các tùy chọn gỡ lỗi, v.v.) cũng như những tính năng cần включ vào hoặc tắt đi.

Kiểm tra đầu ra của ``scons --help`` để xem chi tiết về từng tùy chọn cho phiên bản mà bạn muốn biên dịch.

.. _doc_overriding_build_options:

Ghi đè các tùy chọn xây dựng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sử dụng tệp
^^^^^^^^^^^

Có thể tạo tệp ``custom.py`` mặc định tại thư mục gốc của mã nguồn Godot Engine để khởi tạo mọi tùy chọn xây dựng SCons được truyền qua dòng lệnh:

.. code-block:: python
    :caption: custom.py

    optimize = "size"
    module_mono_enabled = "yes"
    use_llvm = "yes"
    extra_suffix = "game_title"

Bạn cũng có thể tắt một số mô-đun tích hợp sẵn trước khi biên dịch, nhờ đó tiết kiệm một phần thời gian xây dựng engine. Xem trang :ref:`doc_optimizing_for_size` để biết thêm chi tiết.

.. seealso::

    Bạn có thể sử dụng `Godot build options generator <https://godot-build-options-generator.github.io/>`__ trực tuyến để tạo tệp ``custom.py`` chứa các tùy chọn SCons. Sau đó, bạn có thể lưu tệp này và đặt nó tại thư mục gốc của thư mục mã nguồn Godot.

Bạn có thể chỉ định rõ một tệp tùy chỉnh khác bằng tùy chọn dòng lệnh ``profile``, đồng thời ghi đè cấu hình xây dựng mặc định:

.. code-block:: shell

    scons profile=path/to/custom.py

.. note:: Build options set from the file can be overridden by the command line
          các tùy chọn.

Bạn cũng có thể ghi đè các tùy chọn theo điều kiện:

.. code-block:: python
    :caption: custom.py

    import version

    # Override options specific for Godot 3.x and 4.x versions.
    if version.major == 3:
        pass
    elif version.major == 4:
        pass

Sử dụng SCONSFLAGS
^^^^^^^^^^^^^^^^^^

``SCONSFLAGS`` là một biến môi trường được SCons sử dụng để tự động thiết lập các tùy chọn mà không cần cung cấp chúng qua dòng lệnh.

Ví dụ: bạn có thể muốn buộc sử dụng một số lượng luồng CPU nhất định bằng tùy chọn ``-j`` đã đề cập ở trên cho tất cả các lần xây dựng sau này:

.. tabs::
 .. code-tab:: bash Linux/macOS

     export SCONSFLAGS="-j4"

 .. code-tab:: bat Windows (cmd)

     set SCONSFLAGS=-j4

 .. code-tab:: powershell Windows (PowerShell)

     $env:SCONSFLAGS="-j4"

Bản dựng SCU (single compilation unit)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các bản dựng thông thường thường bị nghẽn do phải đưa một số lượng lớn tệp tiêu đề vào mỗi đơn vị biên dịch. Chủ yếu nhằm tăng tốc quá trình phát triển (thay vì các bản dựng sản phẩm), Godot cung cấp bản dựng "single compilation unit" (còn gọi là bản dựng "Unity / Jumbo").

Đối với các thư mục được tùy chọn này tăng tốc, nhiều tệp ``.cpp`` được biên dịch trong mỗi đơn vị biên dịch, nhờ đó các tệp tiêu đề có thể được chia sẻ giữa nhiều tệp, giúp giảm đáng kể thời gian xây dựng.

Để thực hiện bản dựng SCU, hãy sử dụng tùy chọn SCons ``scu_build=yes``.

.. note:: When developing a pull request using SCU builds, be sure to make a
          bản dựng thông thường trước khi gửi PR. Nguyên nhân là do các bản dựng SCU vốn đưa các tệp tiêu đề từ những tệp ``.cpp`` trước đó vào đơn vị biên dịch, vì vậy sẽ không phát hiện được tất cả các tệp tiêu đề mà bạn cần trong bản dựng thông thường. CI sẽ phát hiện những lỗi này, nhưng thông thường việc phát hiện chúng trong một bản dựng cục bộ trên máy của bạn sẽ nhanh hơn.

Mẫu xuất
--------

Các mẫu xuất chính thức được tải xuống từ trang Godot Engine: `godotengine.org <https://godotengine.org/>`__. Tuy nhiên, bạn có thể muốn tự xây dựng chúng (trong trường hợp muốn có các mẫu mới hơn, đang sử dụng mô-đun tùy chỉnh hoặc đơn giản là không tin vào cái bóng của chính mình).

Nếu tải xuống gói mẫu xuất chính thức và giải nén, bạn sẽ nhận thấy hầu hết các tệp là tệp nhị phân hoặc gói đã được tối ưu hóa cho từng nền tảng:

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

Để tự tạo các mẫu đó, hãy làm theo hướng dẫn chi tiết cho từng nền tảng trong cùng phần hướng dẫn này. Mỗi nền tảng đều giải thích cách tạo mẫu riêng.

Tệp ``version.txt`` phải chứa mã định danh phiên bản Godot tương ứng. Tệp này được sử dụng để cài đặt các mẫu xuất vào một thư mục dành riêng cho từng phiên bản nhằm tránh xung đột. Ví dụ: nếu bạn đang xây dựng mẫu xuất cho Godot 4.4.1, ``version.txt`` phải chứa ``4.4.1.stable`` ở dòng đầu tiên (và không có gì khác). Mã định danh phiên bản này dựa trên các dòng ``major``, ``minor``, ``patch`` (nếu có) và ``status`` trong `version.py file in the Godot Git repository <https://github.com/godotengine/godot/blob/master/version.py>`__.

Nếu bạn phát triển cho nhiều nền tảng, macOS chắc chắn là nền tảng máy chủ thuận tiện nhất để biên dịch chéo, vì bạn có thể biên dịch chéo cho mọi mục tiêu. Linux và Windows đứng thứ hai, nhưng Linux có lợi thế là nền tảng dễ thiết lập hơn.
