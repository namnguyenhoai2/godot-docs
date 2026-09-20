.. _doc_compiling_for_linuxbsd:

Biên dịch cho Linux, \*BSD
==========================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân của trình chỉnh sửa Linux và các template xuất từ mã nguồn. Nếu bạn muốn xuất dự án sang Linux, hãy đọc :ref:`doc_exporting_for_linux`.

Yêu cầu
-------

Để biên dịch trên Linux hoặc các biến thể Unix khác, cần có những thành phần sau:

- GCC 9+ hoặc Clang 6+. - `Python 3.9+ <https://www.python.org/downloads/>`_. - Hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`_. - pkg-config (dùng để phát hiện các thư viện phát triển được liệt kê bên dưới). - Các thư viện phát triển:

  - X11, Xcursor, Xinerama, Xi và XRandR. - Wayland và wayland-scanner. - Mesa. - ALSA. - PulseAudio.

- *Tùy chọn* - libudev (build với ``udev=yes``).

.. seealso::

    Để lấy mã nguồn Godot dùng cho việc biên dịch, xem :ref:`doc_getting_source`.

    Để xem tổng quan về cách sử dụng SCons cho Godot, xem :ref:`doc_introduction_to_the_buildsystem`.

.. _doc_compiling_for_linuxbsd_oneliners:

Các lệnh một dòng theo bản phân phối
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. tabs::

    .. tab:: Alpine Linux

        ::

            apk add \
              scons \
              pkgconf \
              gcc \
              g++ \
              libx11-dev \
              libxcursor-dev \
              libxinerama-dev \
              libxi-dev \
              libxrandr-dev \
              mesa-dev \
              eudev-dev \
              alsa-lib-dev \
              pulseaudio-dev

    .. tab:: Arch Linux

        ::

            pacman -Sy --noconfirm --needed \
              scons \
              pkgconf \
              gcc \
              libxcursor \
              libxinerama \
              libxi \
              libxrandr \
              wayland-utils \
              mesa \
              glu \
              libglvnd \
              alsa-lib \
              pulseaudio

    .. tab:: Debian/Ubuntu

        ::

            sudo apt-get update
            sudo apt-get install -y \
              build-essential \
              scons \
              pkg-config \
              libx11-dev \
              libxcursor-dev \
              libxinerama-dev \
              libgl1-mesa-dev \
              libglu1-mesa-dev \
              libasound2-dev \
              libpulse-dev \
              libudev-dev \
              libxi-dev \
              libxrandr-dev \
              libwayland-dev

    .. tab:: Fedora

        ::

            sudo dnf install -y \
              scons \
              pkgconfig \
              gcc-c++ \
              libstdc++-static \
              wayland-devel

    .. tab:: FreeBSD

        ::

            pkg install -y \
              devel/scons \
              pkgconf \
              xorg-libraries \
              libXcursor \
              libXrandr \
              libXi \
              xorgproto \
              libGLU \
              alsa-lib \
              pulseaudio \
              wayland

    .. tab:: Gentoo

        ::

            emerge --sync
            emerge -an \
              dev-build/scons \
              x11-libs/libX11 \
              x11-libs/libXcursor \
              x11-libs/libXinerama \
              x11-libs/libXi \
              dev-util/wayland-scanner \
              media-libs/mesa \
              media-libs/glu \
              media-libs/alsa-lib \
              media-sound/pulseaudio

    .. tab:: Mageia

        ::

            sudo urpmi --auto \
              scons \
              task-c++-devel \
              wayland-devel \
              "pkgconfig(alsa)" \
              "pkgconfig(glu)" \
              "pkgconfig(libpulse)" \
              "pkgconfig(udev)" \
              "pkgconfig(x11)" \
              "pkgconfig(xcursor)" \
              "pkgconfig(xinerama)" \
              "pkgconfig(xi)" \
              "pkgconfig(xrandr)"

    .. tab:: NetBSD

        ::

            pkg_add pkgin
            pkgin -y install \
              pkg-config \
              py313-scons \
              wayland \
              pulseaudio

    .. tab:: OpenBSD

        ::

            pkg_add -I \
              scons \
              wayland \
              pulseaudio

    .. tab:: openKylin

        ::

            sudo apt update
            sudo apt install -y \
              python3-pip \
              build-essential \
              pkg-config \
              libx11-dev \
              libxcursor-dev \
              libxinerama-dev \
              libgl1-mesa-dev \
              libglu1-mesa-dev \
              libasound2-dev \
              libpulse-dev \
              libudev-dev \
              libxi-dev \
              libxrandr-dev \
              libwayland-dev
            sudo pip install scons

    .. tab:: openSUSE

        ::

            sudo zypper install -y \
              scons \
              pkgconfig \
              libX11-devel \
              libXcursor-devel \
              libXrandr-devel \
              libXinerama-devel \
              libXi-devel \
              wayland-devel \
              Mesa-libGL-devel \
              alsa-devel \
              libpulse-devel \
              libudev-devel \
              gcc-c++ \
              libGLU1

    .. tab:: Solus

        ::

            eopkg install -y \
              -c system.devel \
              scons \
              libxcursor-devel \
              libxinerama-devel \
              libxi-devel \
              libxrandr-devel \
              wayland-devel \
              mesalib-devel \
              libglu \
              alsa-lib-devel \
              pulseaudio-devel

Biên dịch
---------

Mở terminal, đi đến thư mục gốc của mã nguồn engine rồi nhập:

::

    scons platform=linuxbsd

.. note::

    Trước Godot 4.0, target Linux/\*BSD được gọi là ``x11`` thay vì ``linuxbsd``. Nếu bạn muốn biên dịch Godot 3.x, hãy đảm bảo sử dụng `nhánh 3.x của tài liệu này <https://docs.godotengine.org/en/3.6/development/compiling/compiling_for_x11.html>`__.

.. tip::
    Nếu bạn biên dịch Godot để thực hiện thay đổi hoặc đóng góp cho engine, bạn có thể muốn sử dụng các tùy chọn SCons ``dev_build=yes`` hoặc ``dev_mode=yes``. Xem :ref:`doc_introduction_to_the_buildsystem_development_and_production_aliases` để biết thêm thông tin.

Nếu mọi việc diễn ra suôn sẻ, tệp thực thi nhị phân kết quả sẽ được đặt trong thư mục con "bin". Tệp thực thi này chứa toàn bộ engine và chạy mà không cần bất kỳ dependency nào. Thực thi tệp này sẽ mở Project Manager.

.. note::

    Nếu muốn biên dịch bằng Clang thay vì GCC, hãy sử dụng lệnh này:

    ::

        scons platform=linuxbsd use_llvm=yes

    Việc sử dụng Clang dường như là yêu cầu đối với OpenBSD, nếu không font sẽ không được build. Đối với các thiết bị có kiến trúc RISC-V, hãy sử dụng trình biên dịch Clang thay cho trình biên dịch GCC.

.. note::

    Việc biên dịch trên một số nền tảng như OpenBSD có thể cần nhiều bộ nhớ hơn mức mặc định. Để tăng giới hạn bộ nhớ trên OpenBSD trong phạm vi giới hạn tối đa dành cho người dùng hiện tại, hãy chạy ``ulimit -d {new amount in kB}``.

.. tip:: If you are compiling Godot for production use, you can
         làm cho tệp thực thi cuối cùng nhỏ hơn và nhanh hơn bằng cách thêm tùy chọn SCons ``production=yes``. Tùy chọn này bật các tối ưu hóa trình biên dịch bổ sung và tối ưu hóa khi liên kết.

         LTO cần một khoảng thời gian để chạy và yêu cầu khoảng 7 GB RAM khả dụng trong khi biên dịch. Nếu hết bộ nhớ khi dùng tùy chọn trên, hãy sử dụng ``production=yes lto=none`` hoặc ``production=yes lto=thin`` để có một dạng LTO nhẹ hơn nhưng kém hiệu quả hơn.

.. note:: If you want to use separate editor settings for your own Godot builds
          và các bản phát hành chính thức, bạn có thể bật
          :ref:`doc_data_paths_self_contained_mode` by creating a file called
          ``._sc_`` hoặc ``_sc_`` trong thư mục ``bin/``.

Biên dịch với hỗ trợ AccessKit
------------------------------

AccessKit cung cấp hỗ trợ cho trình đọc màn hình.

Theo mặc định, Godot được build với AccessKit liên kết động. Bạn có thể sử dụng tính năng này bằng cách đặt ``accesskit.so`` cùng với tệp thực thi.

.. note:: You can use dynamically linked AccessKit with export templates as well, rename
          SO vào ``accesskit.{architecture}.so`` và đặt chúng cùng với các tệp thực thi template xuất, các thư viện sẽ được tự động sao chép trong quá trình xuất.

Để biên dịch Godot với AccessKit liên kết tĩnh:

- Tải các thư viện tĩnh dựng sẵn từ `thư viện godot-accesskit-c-static <https://github.com/godotengine/godot-accesskit-c-static/releases>`_, rồi giải nén. - Khi build Godot, thêm ``accesskit_sdk_path={path}`` để cho SCons biết nơi tìm các thư viện AccessKit:

    ::

        scons platform=linuxbsd accesskit_sdk_path=<...>

.. note:: You can optionally build the godot-angle-static libraries yourself with
          các bước sau:

          1. Sao chép thư mục `godot-accesskit-c-static <https://github.com/godotengine/godot-accesskit-c-static/>`_ và điều hướng đến đó. 2. Chạy lệnh sau:

          ::

              cd accesskit-c
              cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
              cmake --build build
              cmake --install build

          Thư viện tĩnh AccessKit nên được build bằng cùng trình biên dịch mà bạn đang dùng để build Godot.

Chạy bản build headless/server
------------------------------

Để chạy ở chế độ *headless*, cung cấp chức năng của trình chỉnh sửa nhằm xuất dự án theo cách tự động, hãy sử dụng bản build thông thường:

::

    scons platform=linuxbsd target=editor

Sau đó sử dụng đối số dòng lệnh ``--headless``:

::

    ./bin/godot.linuxbsd.editor.x86_64 --headless

Để biên dịch bản build *server* debug có thể được sử dụng với
:ref:`remote debugging tools <doc_command_line_tutorial>`, use:

::

    scons platform=linuxbsd target=template_debug

Để biên dịch bản build *server* được tối ưu hóa để chạy các máy chủ game chuyên dụng, hãy sử dụng:

::

    scons platform=linuxbsd target=template_release production=yes

Build các template xuất
-----------------------

.. warning:: Linux binaries usually won't run on distributions that are
             cũ hơn bản phân phối nơi chúng được build. Nếu muốn phân phối các tệp nhị phân hoạt động trên hầu hết các bản phân phối, bạn nên build chúng trên một bản phân phối cũ như Ubuntu 20.04. Bạn có thể sử dụng máy ảo hoặc container để thiết lập môi trường build phù hợp.


Để build các template xuất Linux hoặc \*BSD, hãy chạy hệ thống build với các tham số sau:

-  (32 bit)

::

    scons platform=linuxbsd target=template_release arch=x86_32
    scons platform=linuxbsd target=template_debug arch=x86_32

-  (64 bit)

::

    scons platform=linuxbsd target=template_release arch=x86_64
    scons platform=linuxbsd target=template_debug arch=x86_64

Lưu ý rằng việc cross-compile cho số bit đối lập (64/32) so với nền tảng máy chủ không phải lúc nào cũng đơn giản và có thể cần môi trường chroot.

Để tạo các template xuất tiêu chuẩn, các tệp kết quả trong thư mục ``bin/`` phải được sao chép vào:

::

    $HOME/.local/share/godot/export_templates/<version>/

và được đặt tên như sau (kể cả với \*BSD, hệ điều hành được Godot xem là "Linux/X11"):

.. code:: text

    linux_debug.arm32
    linux_debug.arm64
    linux_debug.x86_32
    linux_debug.x86_64
    linux_release.arm32
    linux_release.arm64
    linux_release.x86_32
    linux_release.x86_64

Tuy nhiên, nếu bạn viết các module tùy chỉnh hoặc mã C++ tùy chỉnh, thay vào đó bạn có thể muốn cấu hình các tệp nhị phân của mình làm template xuất tùy chỉnh trong menu xuất dự án. Bạn phải bật **Advanced Options** để thiết lập tùy chọn này.

.. image:: img/lintemplates.webp

Bạn thậm chí không cần sao chép chúng; chỉ cần tham chiếu đến các tệp kết quả trong thư mục ``bin/`` của thư mục mã nguồn Godot, để lần build tiếp theo, bạn tự động có các template tùy chỉnh được tham chiếu.

Cross-compile cho thiết bị RISC-V
---------------------------------

Để cross-compile Godot cho các thiết bị RISC-V, chúng ta cần thiết lập các thành phần sau:

- `riscv-gnu-toolchain <https://github.com/riscv-collab/riscv-gnu-toolchain/releases>`__. Mặc dù chúng ta sẽ không sử dụng trực tiếp công cụ này, nó cung cấp cho chúng ta một sysroot, cùng các tệp header và thư viện cần thiết. Có nhiều phiên bản để lựa chọn; tuy nhiên, toolchain càng cũ thì các tệp nhị phân cuối cùng càng tương thích. Nếu không chắc chắn, `hãy sử dụng phiên bản này <https://github.com/riscv-collab/riscv-gnu-toolchain/releases/tag/2023.07.07>`__, và tải xuống ``riscv64-glibc-ubuntu-20.04-gcc-nightly-2023.07.07-nightly.tar.gz``. Giải nén nó vào một nơi nào đó và ghi nhớ đường dẫn. - `mold <https://github.com/rui314/mold/releases>`__. Trình liên kết nhanh này là trình duy nhất liên kết chính xác tệp nhị phân kết quả. Hãy tải xuống, giải nén và đảm bảo thêm thư mục ``bin`` của nó vào PATH. Chạy ``mold --help | grep support`` để kiểm tra xem phiên bản Mold của bạn có hỗ trợ RISC-V hay không. Nếu không thấy RISC-V, có thể Mold của bạn cần được cập nhật.

Để việc tham chiếu đến toolchain dễ dàng hơn, chúng ta có thể đặt một biến môi trường như sau:

::

    export RISCV_TOOLCHAIN_PATH="path to toolchain here"

Như vậy, chúng ta sẽ không phải tự đặt vị trí thư mục mỗi lần muốn tham chiếu đến nó.

Với toàn bộ thiết lập trên, giờ chúng ta đã sẵn sàng build Godot.

Đi đến thư mục gốc của mã nguồn và thực thi lệnh build sau:

::

    PATH="$RISCV_TOOLCHAIN_PATH/bin:$PATH" \
    scons arch=rv64 use_llvm=yes linker=mold lto=none target=editor \
        ccflags="--sysroot=$RISCV_TOOLCHAIN_PATH/sysroot --gcc-toolchain=$RISCV_TOOLCHAIN_PATH -target riscv64-unknown-linux-gnu" \
        linkflags="--sysroot=$RISCV_TOOLCHAIN_PATH/sysroot --gcc-toolchain=$RISCV_TOOLCHAIN_PATH -target riscv64-unknown-linux-gnu"

.. note::

    RISC-V GCC có `lỗi trong các thao tác atomic <https://github.com/riscv-collab/riscv-gcc/issues/15>`__ khiến nó không thể biên dịch Godot chính xác. Đó là lý do Clang được sử dụng thay thế. Hãy đảm bảo rằng nó *có thể* biên dịch sang RISC-V. Bạn có thể xác minh bằng cách thực thi lệnh này ``clang -print-targets``, đảm bảo bạn thấy ``riscv64`` trong danh sách các target.

.. warning:: The code above includes adding ``$RISCV_TOOLCHAIN_PATH/bin`` to the PATH,
             nhưng chỉ dành cho lệnh ``scons`` sau đây. Vì riscv-gnu-toolchain sử dụng Clang riêng nằm trong thư mục ``bin``, việc thêm ``$RISCV_TOOLCHAIN_PATH/bin`` vào biến môi trường PATH của người dùng có thể khiến bạn không truy cập được phiên bản Clang khác nếu đã cài đặt. Vì lý do này, không nên thêm vĩnh viễn thư mục bin. Bạn cũng có thể bỏ qua dòng ``PATH="$RISCV_TOOLCHAIN_PATH/bin:$PATH"`` nếu muốn sử dụng scons với phiên bản Clang tự cài đặt, nhưng phiên bản đó có thể gặp vấn đề tương thích với riscv-gnu-toolchain.

Lệnh này tương tự về bản chất, nhưng có một số thay đổi quan trọng. ``ccflags`` và ``linkflags`` thêm các cờ bổ sung vào bản build. ``--sysroot`` trỏ đến một thư mục mô phỏng hệ thống Linux, chứa tất cả header, thư viện và các tệp ``.so`` mà Clang sẽ sử dụng. ``--gcc-toolchain`` cho Clang biết toolchain hoàn chỉnh nằm ở đâu, còn ``-target riscv64-unknown-linux-gnu`` cho Clang biết kiến trúc đích và hệ điều hành mà chúng ta muốn build.

Nếu mọi việc diễn ra suôn sẻ, bây giờ bạn sẽ thấy một thư mục ``bin``, bên trong có một tệp nhị phân tương tự như sau:

.. code:: text

    godot.linuxbsd.editor.rv64.llvm

Giờ bạn có thể sao chép tệp thực thi này vào thiết bị RISC-V yêu thích, rồi khởi chạy tại đó bằng cách nhấp đúp; thao tác này sẽ mở trình quản lý dự án.

Nếu sau đó bạn quyết định biên dịch các template xuất, hãy sao chép lệnh build ở trên nhưng thay đổi giá trị của ``target`` thành ``template_debug`` cho bản build debug hoặc ``template_release`` cho bản build release.

Sử dụng Clang và LLD để phát triển nhanh hơn
--------------------------------------------

Bạn cũng có thể sử dụng Clang và LLD để build Godot. So với thiết lập GCC + GNU ld mặc định, cách này có hai ưu điểm:

- LLD liên kết Godot nhanh hơn đáng kể so với GNU ld hoặc gold. Điều này giúp rút ngắn thời gian lặp lại. - Clang thường cung cấp các thông báo lỗi hữu ích hơn so với GCC.

Để thực hiện việc này, hãy cài đặt Clang và gói ``lld`` từ trình quản lý gói của bản phân phối, sau đó sử dụng lệnh SCons sau:

::

    scons platform=linuxbsd use_llvm=yes linker=lld

Sau khi quá trình build hoàn tất, một tệp nhị phân mới có hậu tố ``.llvm`` sẽ được tạo trong thư mục ``bin/``.

Bạn vẫn nên sử dụng GCC cho các bản build dùng trong môi trường production vì đây là trình biên dịch được sử dụng cho các bản build chính thức và đã được kiểm thử nghiêm ngặt hơn.

Nếu xảy ra lỗi này:

.. code:: text

    /usr/bin/ld: cannot find -l:libatomic.a: No such file or directory

Có hai giải pháp:

- Trong lệnh SCons, hãy thêm tham số ``use_static_cpp=no``. - Làm theo `các hướng dẫn này <https://github.com/ivmai/libatomic_ops#installation-and-usage>`__ để cấu hình, build và cài đặt ``libatomic_ops``. Sau đó, sao chép ``/usr/lib/libatomic_ops.a`` vào ``/usr/lib/libatomic.a``, hoặc tạo liên kết mềm đến ``libatomic_ops`` bằng lệnh ``ln -s /usr/lib/libatomic_ops.a /usr/lib/libatomic.a``. Liên kết mềm đảm bảo ``libatomic_ops`` mới nhất sẽ được sử dụng mà không cần sao chép mỗi lần nó được cập nhật.

Sử dụng mold để phát triển nhanh hơn
------------------------------------

Để liên kết nhanh hơn nữa so với LLD, bạn có thể sử dụng `mold <https://github.com/rui314/mold>`__. mold có thể được sử dụng với GCC hoặc Clang.

.. tabs::
    .. tab:: Debian/Ubuntu

        ::

            sudo apt-get update
            sudo apt-get install -y mold

    .. tab:: Fedora

        ::

            sudo dnf install -y mold

    .. tab:: Arch Linux

        ::

            pacman -Sy --noconfirm --needed mold

Sau khi cài đặt mold, hãy sử dụng lệnh SCons sau khi biên dịch Godot:

  ::

    scons platform=linuxbsd linker=mold

Sử dụng các thư viện hệ thống để phát triển nhanh hơn
-----------------------------------------------------

`Godot tích hợp mã nguồn của nhiều thư viện bên thứ ba. <https://github.com/godotengine/godot/tree/master/thirdparty>`__ Thay vào đó, bạn có thể chọn sử dụng các phiên bản hệ thống của thư viện bên thứ ba. Điều này giúp liên kết tệp nhị phân Godot nhanh hơn, vì các thư viện bên thứ ba được liên kết động. Do đó, chúng không cần được liên kết tĩnh mỗi lần bạn build engine (kể cả khi chỉ có những thay đổi gia tăng nhỏ).

Tuy nhiên, không phải tất cả các bản phân phối Linux đều có sẵn các gói cho thư viện bên thứ ba (hoặc các gói này có thể chưa được cập nhật).

Việc chuyển sang sử dụng các thư viện hệ thống có thể giảm thời gian liên kết vài giây trên các CPU chậm, nhưng bạn cần kiểm thử thủ công tùy theo bản phân phối Linux của mình. Ngoài ra, bạn có thể không sử dụng được thư viện hệ thống cho mọi thứ do lỗi trong các gói thư viện hệ thống (hoặc trong hệ thống build, vì tính năng này ít được kiểm thử hơn).

Để biên dịch Godot với các thư viện hệ thống, hãy cài đặt các phần phụ thuộc này **bổ sung** cho những phần được liệt kê trong :ref:`doc_compiling_for_linuxbsd_oneliners`:

.. tabs::

    .. tab:: Debian/Ubuntu

        ::

            sudo apt-get update
            sudo apt-get install -y \
              libembree-dev \
              libenet-dev \
              libfreetype-dev \
              libpng-dev \
              zlib1g-dev \
              libgraphite2-dev \
              libharfbuzz-dev \
              libogg-dev \
              libtheora-dev \
              libvorbis-dev \
              libwebp-dev \
              libmbedtls-dev \
              libminiupnpc-dev \
              libpcre2-dev \
              libsdl3-dev \
              libzstd-dev \
              libsquish-dev \
              libicu-dev

    .. tab:: Fedora

        ::

            sudo dnf install -y \
              embree-devel \
              enet-devel \
              glslang-devel \
              graphite2-devel \
              harfbuzz-devel \
              libicu-devel \
              libsquish-devel \
              libtheora-devel \
              libvorbis-devel \
              libwebp-devel \
              libzstd-devel \
              mbedtls-devel \
              miniupnpc-devel \
              SDL3-devel

Sau khi cài đặt tất cả các gói bắt buộc, hãy sử dụng lệnh sau để build Godot:

.. NOTE: Một số tùy chọn `builtin_` không được sử dụng ở đây vì chúng làm hỏng quá trình build kể từ tháng 1 năm 2023 (đã kiểm thử trên Fedora 37).

::

    scons platform=linuxbsd builtin_embree=no builtin_enet=no builtin_freetype=no builtin_graphite=no builtin_harfbuzz=no builtin_libogg=no builtin_libpng=no builtin_libtheora=no builtin_libvorbis=no builtin_libwebp=no builtin_mbedtls=no builtin_miniupnpc=no builtin_pcre2=no builtin_sdl=no builtin_zlib=no builtin_zstd=no

Trên Debian stable, bạn sẽ cần xóa `builtin_embree=no` vì phiên bản Embree do hệ thống cung cấp quá cũ để hoạt động với nhánh `master` mới nhất của Godot (yêu cầu Embree 4).

Bạn có thể xem danh sách tất cả các thư viện tích hợp có thư viện thay thế trong hệ thống bằng cách chạy ``scons -h``, sau đó tìm các tùy chọn bắt đầu bằng ``builtin_``.

.. warning::

    Khi sử dụng các thư viện hệ thống, tệp nhị phân kết quả sẽ **không** còn khả chuyển giữa các bản phân phối Linux. Không sử dụng phương pháp này để tạo các tệp nhị phân mà bạn dự định phân phối cho người khác, trừ khi bạn đang tạo một gói cho một bản phân phối Linux.
