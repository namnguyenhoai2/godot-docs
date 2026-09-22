.. _doc_compiling_for_windows:

Biên dịch cho Windows
=====================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân của editor Windows và export template từ mã nguồn. Nếu bạn muốn export dự án của mình sang Windows, hãy đọc :ref:`doc_exporting_for_windows`.

Yêu cầu
-------

Để biên dịch trên Windows, cần có những thành phần sau:

- Trình biên dịch C++. Sử dụng một trong các lựa chọn sau:

    - `Visual Studio Community <https://www.visualstudio.com/vs/community/>`_, phiên bản 2019 trở lên. Khuyến nghị sử dụng Visual Studio 2022. **Trong quá trình cài đặt, hãy chọn C++ trong danh sách workflow và chọn các thành phần riêng lẻ sau đây:**

      .. tabs::

          .. tab:: Visual Studio 2019
              - **MSVC v142 - VS 2019 C++ {arch} build tools (Latest)** cho các kiến trúc đích.
              - **Windows 11 SDK (10.0.22621.0)** (đúng phiên bản này).

          .. tab:: Visual Studio 2022
              - **MSVC v143 - VS 2022 C++ {arch} build tools (Latest)** cho các kiến trúc đích.
              - **Windows 11 SDK (10.0.22621.0)** hoặc mới hơn.

          .. tab:: Visual Studio 2026
              - **MSVC Build Tools for {arch} (Latest)** cho các kiến trúc đích.
              - **Windows 11 SDK (10.0.22621.0)** hoặc mới hơn.

      Nếu bạn đã cài đặt Visual Studio mà không có hỗ trợ C++ cho kiến trúc đích hoặc không có Windows SDK, hãy chạy lại trình cài đặt; trình cài đặt sẽ hiển thị nút **Modify**. Hỗ trợ ``x86_64``, ``x86_32`` và ``arm64``.
    - `MinGW-w64 <https://mingw-w64.org/>`_ đi kèm GCC có thể được sử dụng thay cho Visual Studio. Hãy đảm bảo cài đặt/cấu hình để sử dụng mô hình luồng ``posix``. **Quan trọng:** Khi sử dụng MinGW để biên dịch nhánh ``master``, bạn cần GCC 12 trở lên. Chỉ hỗ trợ ``x86_64`` và ``x86_32``.
    - `MinGW-LLVM <https://github.com/mstorsjo/llvm-mingw/releases>`_ đi kèm clang có thể được sử dụng thay cho Visual Studio và MinGW-w64. **Quan trọng:** Khi sử dụng MinGW để biên dịch nhánh ``master``, bạn cần clang 14 trở lên. Hỗ trợ ``x86_64``, ``x86_32`` và ``arm64``.
- `Python 3.9+ <https://www.python.org/downloads/windows/>`_. **Hãy bật tùy chọn thêm Python vào** ``PATH`` **trong trình cài đặt.**
- `SCons 4.4+ <https://scons.org/pages/download.html>`_ build system. Khuyến nghị sử dụng bản phát hành mới nhất, đặc biệt để hỗ trợ đúng các bản phát hành Visual Studio gần đây.
- :ref:`Các dependency của Direct3D 12 <doc_compiling_for_windows_installing_d3d12_requirements>` (có thể bỏ qua bằng tùy chọn ``d3d12=no`` của SCons nếu không cần hỗ trợ Direct3D 12).

.. note:: Nếu đã cài đặt `Scoop <https://scoop.sh/>`_, bạn có thể dễ dàng cài đặt MinGW và các dependency khác bằng lệnh sau:

          ::

              scoop install python mingw

          Vẫn cần cài đặt Scons thông qua pip
.. note:: Nếu đã cài đặt `MSYS2 <https://www.msys2.org/>`_, bạn có thể dễ dàng cài đặt MinGW và các dependency khác bằng lệnh sau:

          ::

              pacman -S mingw-w64-x86_64-gcc mingw-w64-i686-gcc make python-pip

          Sau đó, đối với mỗi subsystem MinGW của MSYS2, bạn nên chạy `pip3 install scons` trong shell tương ứng.

.. seealso:: Để lấy mã nguồn Godot phục vụ việc biên dịch, hãy xem
             :ref:`doc_getting_source`.

             Để biết tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Thiết lập SCons
---------------

Để cài đặt SCons, hãy mở command prompt và chạy lệnh sau:

::

    python -m pip install scons

Nếu bạn nhận được thông báo ``Defaulting to user installation because normal site-packages is not writeable``, có thể bạn phải chạy lại lệnh đó với quyền nâng cao. Hãy mở một command prompt mới với tư cách Administrator, sau đó chạy lại lệnh để đảm bảo SCons khả dụng từ ``PATH``.

Để kiểm tra xem bạn đã cài đặt Python và SCons đúng cách chưa, bạn có thể nhập ``python --version`` và ``scons --version`` vào command prompt (``cmd.exe``).

Nếu các lệnh trên không hoạt động, hãy đảm bảo thêm Python vào biến môi trường ``PATH`` sau khi cài đặt, rồi kiểm tra lại. Bạn có thể thực hiện việc này bằng cách chạy lại trình cài đặt Python và bật tùy chọn thêm Python vào ``PATH``.

Nếu SCons không phát hiện được bản cài đặt Visual Studio, có thể phiên bản SCons của bạn quá cũ. Hãy cập nhật lên phiên bản mới nhất bằng ``python -m pip install --upgrade scons``.

.. _doc_compiling_for_windows_install_vs:

Tải mã nguồn Godot
------------------

Tham khảo :ref:`doc_getting_source` để xem hướng dẫn chi tiết.

Từ đây về sau, hướng dẫn sẽ giả định rằng bạn đã đặt mã nguồn tại ``C:\godot``.

.. warning::

    Để tránh tình trạng chậm do quá trình quét virus liên tục trong khi biên dịch, hãy thêm thư mục mã nguồn Godot vào danh sách ngoại lệ trong phần mềm antivirus của bạn.

    Đối với Windows Defender, nhấn phím :kbd:`Windows`, nhập "Windows Security", rồi nhấn :kbd:`Enter`. Nhấp vào **Virus & threat protection** trong bảng bên trái. Trong mục **Virus & threat protection settings**, nhấp vào **Manage Settings** rồi cuộn xuống **Exclusions**. Nhấp vào **Add or remove exclusions**, sau đó thêm thư mục mã nguồn Godot.

Biên dịch
---------

Chọn trình biên dịch
~~~~~~~~~~~~~~~~~~~~

SCons sẽ tự động tìm và sử dụng bản cài đặt Visual Studio hiện có. Nếu chưa cài đặt Visual Studio, SCons sẽ thử sử dụng MinGW thay thế. Nếu đã cài đặt Visual Studio và muốn sử dụng MinGW-w64, hãy truyền ``use_mingw=yes`` vào dòng lệnh SCons. Lưu ý rằng không thể thực hiện các bản build MSVC từ shell MSYS2 hoặc MinGW. Thay vào đó, hãy sử dụng ``cmd.exe`` hoặc PowerShell. Nếu đang sử dụng MinGW-LLVM, hãy truyền cả ``use_mingw=yes`` và ``use_llvm=yes`` vào dòng lệnh SCons.

.. tip::

    Trong quá trình phát triển, sử dụng trình biên dịch Visual Studio thường là lựa chọn tốt hơn, vì nó liên kết binary Godot nhanh hơn nhiều so với MinGW. Tuy nhiên, MinGW có thể tạo ra các binary được tối ưu hóa tốt hơn nhờ link-time optimization (xem bên dưới), khiến nó phù hợp hơn cho việc sử dụng trong production. Điều này đặc biệt đúng với GDScript VM, vốn hoạt động tốt hơn nhiều với MinGW so với MSVC. Vì vậy, khuyến nghị sử dụng MinGW để tạo các build phân phối cho người chơi.

    Tất cả binary Godot chính thức đều được build trong `custom containers <https://github.com/godotengine/build-containers>`__ bằng MinGW.

Chạy SCons
~~~~~~~~~~

Sau khi mở command prompt, hãy chuyển đến thư mục gốc của mã nguồn engine (bằng ``cd``) và nhập:

.. code-block:: doscon

    C:\godot> scons platform=windows

.. note:: Khi biên dịch với nhiều CPU thread, SCons có thể cảnh báo rằng pywin32 bị thiếu. Bạn có thể an toàn bỏ qua cảnh báo này.

.. tip::
    Nếu đang biên dịch Godot để thực hiện thay đổi hoặc đóng góp cho engine, bạn có thể muốn sử dụng các tùy chọn SCons ``dev_build=yes`` hoặc ``dev_mode=yes``. Xem :ref:`doc_introduction_to_the_buildsystem_development_and_production_aliases` để biết thêm thông tin.

Nếu mọi việc diễn ra suôn sẻ, tệp binary executable kết quả sẽ được đặt trong ``C:\godot\bin\`` với tên ``godot.windows.editor.x86_32.exe`` hoặc ``godot.windows.editor.x86_64.exe``. Theo mặc định, SCons sẽ build một binary phù hợp với kiến trúc CPU của bạn, nhưng bạn có thể ghi đè bằng ``arch=x86_64``, ``arch=x86_32`` hoặc ``arch=arm64``.

Tệp executable này chứa toàn bộ engine và chạy mà không cần dependency nào. Chạy tệp này sẽ mở Project Manager.

.. tip:: Nếu bạn đang compile Godot để sử dụng trong production, bạn có thể làm cho executable cuối cùng nhỏ hơn và nhanh hơn bằng cách thêm tùy chọn SCons ``production=yes``. Tùy chọn này bật thêm các compiler optimization và link-time optimization.

         LTO cần một khoảng thời gian để chạy và yêu cầu tối đa 30 GB RAM khả dụng trong khi compile (tùy thuộc vào toolchain). Nếu bạn hết bộ nhớ khi sử dụng tùy chọn trên, hãy dùng ``production=yes lto=none`` hoặc ``production=yes lto=thin`` (chỉ LLVM) để sử dụng một dạng LTO nhẹ hơn nhưng kém hiệu quả hơn.

.. note:: Nếu bạn muốn sử dụng các thiết lập editor riêng cho các bản build Godot của mình và các bản phát hành chính thức, bạn có thể bật
          :ref:`doc_data_paths_self_contained_mode` by creating a file called
          ``._sc_`` hoặc ``_sc_`` trong thư mục ``bin/``.

.. _doc_compiling_for_windows_installing_d3d12_requirements:

Cài đặt các yêu cầu của Direct3D 12
-----------------------------------

Theo mặc định, các bản build Godot trên Windows có hỗ trợ graphics API Direct3D 12. Việc compile với hỗ trợ Direct3D 12 yêu cầu cài đặt thêm các dependency. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``d3d12=no``; khi đó, hỗ trợ Vulkan và OpenGL vẫn khả dụng.

Bạn có thể cài đặt các dependency bắt buộc bằng cách chạy ``python misc/scripts/install_d3d12_sdk_windows.py`` trong repository mã nguồn Godot. Sau khi chạy script này, hãy compile Godot như bình thường. Thao tác này sẽ sử dụng các path mặc định cho nhiều dependency khác nhau, tương ứng với các path được sử dụng trong script.

Nếu muốn thiết lập dependency theo cách thủ công, bạn có thể xem các bước chi tiết bên dưới, nhưng script trên sẽ xử lý mọi thứ cho bạn (bao gồm cả các component PIX và Agility SDK tùy chọn).

- `thư viện godot-nir-static <https://github.com/godotengine/godot-nir-static/releases/>`_. Chúng tôi compile các thư viện Mesa bạn cần thành một thư viện static. Hãy tải thư viện này xuống bất kỳ đâu, giải nén và ghi nhớ path đến thư mục đã giải nén, vì bạn sẽ cần dùng path này bên dưới.

.. note:: Bạn cũng có thể tự build các thư viện godot-nir-static theo các bước sau:

          1. Cài đặt package Python `mako <https://www.makotemplates.org>`_, package này cần thiết để generate một số tệp.
          2. Clone thư mục `godot-nir-static <https://github.com/godotengine/godot-nir-static>`_ và điều hướng đến thư mục đó.
          3. Chạy lệnh sau:

          ::

              git submodule update --init
              ./update_mesa.sh
              scons

          Nếu bạn đang build bằng MinGW-w64, hãy thêm ``use_mingw=yes`` vào lệnh ``scons``; bạn cũng có thể chỉ định kiến trúc build bằng ``arch={architecture}``. Nếu bạn đang build bằng MinGW-LLVM, hãy thêm cả ``use_mingw=yes`` và ``use_llvm=yes`` vào lệnh ``scons``.

          Nếu bạn đang build bằng MinGW và các binary không nằm trong ``PATH``, hãy thêm ``mingw_prefix="/path/to/mingw"`` vào lệnh ``scons``.

          Thư viện static Mesa phải được build bằng cùng compiler và cùng CRT (nếu bạn build bằng MinGW) mà bạn sử dụng để build Godot.

Bạn cũng có thể compile với các tùy chọn sau để bật thêm tính năng:

- `PIX <https://devblogs.microsoft.com/pix/download>`_ là một ứng dụng performance tuning và debugging dành cho các ứng dụng Direct3D12. Nếu compile kèm hỗ trợ này, bạn có thể nhận được thông tin chi tiết hơn nhiều thông qua PIX, giúp bạn tối ưu game và khắc phục sự cố graphics bug. Để sử dụng, hãy tải package WinPixEventRuntime. Bạn sẽ được chuyển đến trang package NuGet, tại đó bạn có thể nhấp vào "Download package" để tải xuống. Sau khi tải xuống, hãy đổi phần mở rộng tệp thành .zip và giải nén tệp vào một path bất kỳ.
- `Agility SDK <https://devblogs.microsoft.com/directx/directx12agility>`_ có thể được sử dụng để cung cấp quyền truy cập vào các tính năng Direct3D 12 mới nhất mà không phụ thuộc vào các bản cập nhật driver. Để sử dụng, hãy tải package Agility SDK mới nhất. Bạn sẽ được chuyển đến trang package NuGet, tại đó bạn có thể nhấp vào "Download package" để tải xuống. Sau khi tải xuống, hãy đổi phần mở rộng tệp thành .zip và giải nén tệp vào một path bất kỳ.

.. note:: Nếu sử dụng phiên bản preview của Agility SDK, hãy nhớ bật developer mode trong Windows; nếu không, nó sẽ không được sử dụng.

.. note:: Nếu muốn sử dụng PIX với bản build MinGW, hãy điều hướng đến thư mục runtime của PIX và sử dụng các lệnh sau để generate import library:

          ::

            # For x86-64:
            gendef ./bin/x64/WinPixEventRuntime.dll
            dlltool --machine i386:x86-64 --no-leading-underscore -d WinPixEventRuntime.def -D WinPixEventRuntime.dll -l ./bin/x64/libWinPixEventRuntime.a

            # For ARM64:
            gendef ./bin/ARM64/WinPixEventRuntime.dll
            dlltool --machine arm64 --no-leading-underscore -d WinPixEventRuntime.def -D WinPixEventRuntime.dll -l ./bin/ARM64/libWinPixEventRuntime.a

Khi build Godot, bạn sẽ cần cho SCons biết nơi tìm các thư viện bổ sung:

.. code-block:: doscon

    C:\godot> scons platform=windows mesa_libs=<...>

Hoặc, khi đã bật tất cả tùy chọn:

.. code-block:: doscon

    C:\godot> scons platform=windows mesa_libs=<...> agility_sdk_path=<...> pix_path=<...>

.. note::

    Hỗ trợ PIX bị tắt theo mặc định, ngay cả khi bạn đã cài đặt PIX. Để bật hỗ trợ này, hãy truyền ``use_pix=yes`` cho SCons.

.. note::

    Đối với các DLL của Agility SDK, bạn phải chỉ định rõ loại workflow. Single-arch là mặc định (các DLL được sao chép vào ``bin/``). Nếu truyền ``agility_sdk_multi_arch=yes`` cho SCons, bạn sẽ chọn sử dụng multi-arch. Các DLL sẽ được sao chép vào các thư mục con ``bin/<arch>/`` thích hợp và khi runtime, thư mục phù hợp sẽ được tải.

Compile với hỗ trợ AccessKit
----------------------------

AccessKit cung cấp hỗ trợ cho screen reader.

Việc compile với AccessKit yêu cầu cài đặt thêm các dependency. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``accesskit=no``.

Bạn có thể cài đặt các dependency bắt buộc bằng cách chạy ``python misc/scripts/install_accesskit.py`` trong repository mã nguồn Godot. Sau khi chạy script này, hãy compile Godot như bình thường.

.. note:: Bạn cũng có thể tự build các thư viện AccessKit theo các bước sau:

          1. Clone thư mục `godot-accesskit-c-static <https://github.com/godotengine/godot-accesskit-c-static/>`_ và điều hướng đến thư mục đó.
          2. Chạy lệnh sau:

          ::

              cd accesskit-c
              cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
              cmake --build build
              cmake --install build

          Thư viện static AccessKit phải được build bằng cùng compiler và cùng CRT (nếu bạn build bằng MinGW) mà bạn sử dụng để build Godot.

          Để compile Godot với bản build AccessKit tùy chỉnh, hãy thêm ``accesskit_sdk_path={path}`` để cho SCons biết nơi tìm các thư viện AccessKit:

          ::

              scons platform=windows accesskit_sdk_path=<...>

Compile với hỗ trợ WinRT
------------------------

WinRT cung cấp hỗ trợ cho OneCore TTS (truy cập các voice của Windows 10 trở lên), giám sát thông tin màu HDR và emoji picker.

Nếu bạn đang build bằng MinGW, việc compile với WinRT yêu cầu cài đặt thêm các dependency. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``winrt=no``.

Bạn có thể cài đặt các dependency bắt buộc bằng cách chạy ``python misc/scripts/install_winrt.py`` trong repository mã nguồn Godot. Sau khi chạy script này, hãy compile Godot như bình thường.

.. note:: Bạn cũng có thể tự build các header WinRT theo các bước sau:

          1. Sao chép thư mục `winrt-mingw <https://github.com/godotengine/winrt-mingw>`_ và điều hướng đến thư mục đó.
          2. Chạy lệnh sau:

          ::

              cmake -Bbuild -DCMAKE_BUILD_TYPE=Release -DCPPWINRT_BUILD_VERSION=2.0.250303.1 -DBUILD_TESTING=OFF cppwinrt/
              echo "" > build/app.manifest.rc
              cmake --build build
              ./build/cppwinrt.exe -input windows-rs/crates/libs/bindgen/default/ -output include/

          Để biên dịch Godot bằng bản dựng tùy chỉnh của WinRT, hãy thêm ``winrt_path={path}`` để cho SCons biết nơi tìm các header của AccessKit:

          ::

              scons platform=windows winrt_path=<...>

Biên dịch với hỗ trợ ANGLE
--------------------------

ANGLE cung cấp một lớp chuyển đổi từ OpenGL ES 3.x sang Direct3D 11 và có thể được sử dụng để cải thiện khả năng hỗ trợ renderer Compatibility trên một số GPU cũ hơn có driver OpenGL lỗi thời, cũng như trên Windows cho ARM.

Việc biên dịch với ANGLE yêu cầu cài đặt thêm các dependency. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``angle=no``.

Bạn có thể cài đặt các dependency bắt buộc bằng cách chạy ``python misc/scripts/install_angle.py`` trong repository mã nguồn Godot. Sau khi chạy script này, hãy biên dịch Godot như bình thường.

.. note:: Bạn cũng có thể tự mình build các thư viện godot-angle-static theo các bước sau:

          1. Sao chép thư mục `godot-angle-static <https://github.com/godotengine/godot-angle-static>`_ và điều hướng đến thư mục đó.
          2. Chạy lệnh sau:

          ::

              git submodule update --init
              ./update_angle.sh
              scons

          Nếu build bằng MinGW, hãy thêm ``use_mingw=yes`` vào lệnh; bạn cũng có thể chỉ định kiến trúc build bằng ``arch={architecture}``. Nếu build bằng MinGW-LLVM, hãy thêm cả ``use_mingw=yes`` và ``use_llvm=yes`` vào lệnh ``scons``.

          Nếu build bằng MinGW và các binary không nằm trong ``PATH``, hãy thêm ``mingw_prefix="/path/to/mingw"`` vào lệnh ``scons``.

          Thư viện tĩnh ANGLE nên được build bằng cùng compiler và cùng CRT (nếu bạn build bằng MinGW) mà bạn sử dụng để build Godot.

          Để biên dịch Godot bằng bản build tùy chỉnh của ANGLE, hãy thêm ``angle_libs={path}`` để cho SCons biết nơi tìm các thư viện ANGLE:

          ::

              scons platform=windows angle_libs=<...>

Phát triển trong Visual Studio
------------------------------

Không bắt buộc phải sử dụng IDE để biên dịch Godot vì SCons sẽ xử lý mọi việc. Tuy nhiên, nếu định phát triển engine hoặc debug mã C++ của engine, bạn có thể muốn cấu hình một code editor hoặc IDE.

Các editor dựa trên thư mục không yêu cầu thiết lập cụ thể nào để bắt đầu làm việc với codebase của Godot. Để chỉnh sửa các project bằng Visual Studio, chúng cần được thiết lập dưới dạng một solution.

Bạn có thể tạo một solution Visual Studio thông qua SCons bằng cách chạy SCons với tham số ``vsproj=yes``, như sau:

::

   scons platform=windows vsproj=yes

Giờ đây, bạn có thể mở mã nguồn Godot trong một solution Visual Studio và build Godot bằng nút **Build** của Visual Studio.

.. seealso:: Xem :ref:`doc_configuring_an_ide_vs` để biết thêm chi tiết.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Nếu biên dịch thất bại khi sử dụng MSVC, hãy đảm bảo bạn đã cài đặt các bản cập nhật mới nhất. Bạn có thể thực hiện việc này bằng cách khởi động IDE Visual Studio và sử dụng
:button:`Continue without code`, sau đó là :menu:`Help > Check for Updates` trên thanh menu ở phía trên. Hãy cài đặt tất cả bản cập nhật, rồi thử biên dịch lại.

Cross-compile cho Windows từ các hệ điều hành khác
--------------------------------------------------

Nếu bạn là người dùng Linux hoặc macOS, bạn cần cài đặt `MinGW-w64 <https://www.mingw-w64.org/>`__, thường có các biến thể 32-bit và 64-bit, hoặc `MinGW-LLVM <https://github.com/mstorsjo/llvm-mingw/releases>`_, được cung cấp dưới dạng một archive duy nhất cho mọi kiến trúc đích. Tên package có thể khác nhau tùy theo distribution của bạn; dưới đây là một số tên phổ biến:

+-------------------------+--------------------------------------------------------------+
| **Arch Linux**          | ::                                                           |
|                         |                                                              |
|                         |     pacman -S mingw-w64                                      |
+-------------------------+--------------------------------------------------------------+
| **Debian** / **Ubuntu** | ::                                                           |
|                         |                                                              |
|                         |     apt install mingw-w64                                    |
+-------------------------+--------------------------------------------------------------+
| **Fedora**              | ::                                                           |
|                         |                                                              |
|                         |     dnf install mingw64-gcc-c++ mingw64-winpthreads-static \ |
|                         |                 mingw32-gcc-c++ mingw32-winpthreads-static   |
+-------------------------+--------------------------------------------------------------+
| **macOS**               | ::                                                           |
|                         |                                                              |
|                         |     brew install mingw-w64                                   |
+-------------------------+--------------------------------------------------------------+
| **Mageia**              | ::                                                           |
|                         |                                                              |
|                         |     urpmi mingw64-gcc-c++ mingw64-winpthreads-static \       |
|                         |           mingw32-gcc-c++ mingw32-winpthreads-static         |
+-------------------------+--------------------------------------------------------------+

Trước khi bắt đầu biên dịch, SCons sẽ kiểm tra các binary sau trong biến môi trường ``PATH`` của bạn:

::

    # for MinGW-w64
    i686-w64-mingw32-gcc
    x86_64-w64-mingw32-gcc

    # for MinGW-LLVM
    aarch64-w64-mingw32-clang
    i686-w64-mingw32-clang
    x86_64-w64-mingw32-clang

Nếu các binary không nằm trong ``PATH`` (ví dụ: ``/usr/bin``), bạn có thể định nghĩa biến môi trường sau để cung cấp gợi ý cho build system:

::

    export MINGW_PREFIX="/path/to/mingw"

Trong đó ``/path/to/mingw`` là đường dẫn chứa thư mục ``bin``, nơi ``i686-w64-mingw32-gcc`` và ``x86_64-w64-mingw32-gcc`` nằm (ví dụ: ``/opt/mingw-w64`` nếu các binary nằm trong ``/opt/mingw-w64/bin``).

Để đảm bảo bạn đang thực hiện đúng, việc thực thi lệnh sau trong shell sẽ cho ra một compiler hoạt động (kết quả phiên bản có thể khác tùy theo hệ thống của bạn):

::

    ${MINGW_PREFIX}/bin/x86_64-w64-mingw32-gcc --version
    # x86_64-w64-mingw32-gcc (GCC) 13.2.0

.. note:: Nếu build bằng MinGW-LLVM, hãy thêm ``use_llvm=yes`` vào lệnh ``scons``.
.. note:: Khi cross-compile cho Windows bằng MinGW-w64, hãy lưu ý rằng chỉ các kiến trúc ``x86_64`` và ``x86_32`` được hỗ trợ. MinGW-LLVM cũng hỗ trợ ``arm64``. Hãy đảm bảo chỉ định đúng tùy chọn ``arch=`` khi gọi SCons nếu build từ một kiến trúc khác.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Cross-compile từ một số phiên bản Ubuntu có thể dẫn đến `lỗi này <https://github.com/godotengine/godot/issues/9258>`_, do cấu hình mặc định thiếu hỗ trợ cho POSIX threading.

Bạn có thể thay đổi cấu hình đó theo các hướng dẫn sau đối với 64-bit:

::

    sudo update-alternatives --config x86_64-w64-mingw32-gcc
    <choose x86_64-w64-mingw32-gcc-posix from the list>
    sudo update-alternatives --config x86_64-w64-mingw32-g++
    <choose x86_64-w64-mingw32-g++-posix from the list>

Và đối với 32-bit:

::

    sudo update-alternatives --config i686-w64-mingw32-gcc
    <choose i686-w64-mingw32-gcc-posix from the list>
    sudo update-alternatives --config i686-w64-mingw32-g++
    <choose i686-w64-mingw32-g++-posix from the list>

Tạo export template cho Windows
-------------------------------

Export template cho Windows được tạo bằng cách biên dịch Godot mà không có editor, với các flag sau:

.. code-block:: doscon

    C:\godot> scons platform=windows target=template_debug arch=x86_32
    C:\godot> scons platform=windows target=template_release arch=x86_32
    C:\godot> scons platform=windows target=template_debug arch=x86_64
    C:\godot> scons platform=windows target=template_release arch=x86_64
    C:\godot> scons platform=windows target=template_debug arch=arm64
    C:\godot> scons platform=windows target=template_release arch=arm64

Nếu dự định thay thế các export template tiêu chuẩn, hãy sao chép chúng vào vị trí sau, thay ``<version>`` bằng mã định danh phiên bản (chẳng hạn như ``4.2.1.stable`` hoặc ``4.3.dev``):

.. code-block:: none

    %APPDATA%\Godot\export_templates\<version>\

Với các tên sau:

::

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

Tuy nhiên, nếu đang sử dụng các module tùy chỉnh hoặc mã engine tùy chỉnh, bạn có thể muốn cấu hình các binary của mình làm export template tùy chỉnh trong menu export của project. Bạn phải bật **Advanced Options** để thiết lập mục này.

.. image:: img/wintemplates.webp

Trong trường hợp này, bạn không cần sao chép chúng, chỉ cần tham chiếu đến các tệp kết quả trong thư mục ``bin\`` của thư mục mã nguồn Godot, để lần xây dựng tiếp theo sẽ tự động tham chiếu đến các template tùy chỉnh.

.. _`Visual Studio Community`: https://www.visualstudio.com/vs/community/
.. _`MinGW-w64`: https://mingw-w64.org/
.. _`MinGW-LLVM`: https://github.com/mstorsjo/llvm-mingw/releases
.. _`Python 3.9+`: https://www.python.org/downloads/windows/
.. _`SCons 4.4+`: https://scons.org/pages/download.html
.. _`Scoop`: https://scoop.sh/
.. _`MSYS2`: https://www.msys2.org/
.. _`godot-nir-static library`: https://github.com/godotengine/godot-nir-static/releases/
.. _`mako`: https://www.makotemplates.org
.. _`godot-nir-static`: https://github.com/godotengine/godot-nir-static
.. _`PIX`: https://devblogs.microsoft.com/pix/download
.. _`Agility SDK`: https://devblogs.microsoft.com/directx/directx12agility
.. _`godot-accesskit-c-static`: https://github.com/godotengine/godot-accesskit-c-static/
.. _`winrt-mingw`: https://github.com/godotengine/winrt-mingw
.. _`godot-angle-static`: https://github.com/godotengine/godot-angle-static
.. _`this bug`: https://github.com/godotengine/godot/issues/9258
