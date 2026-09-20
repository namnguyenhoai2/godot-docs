.. _doc_compiling_for_windows:

Biên dịch cho Windows
=====================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân của trình chỉnh sửa Windows và các mẫu xuất từ mã nguồn. Nếu bạn muốn xuất dự án của mình sang Windows, hãy đọc :ref:`doc_exporting_for_windows`.

Yêu cầu
-------

Để biên dịch trên Windows, cần có những thành phần sau:

- Một trình biên dịch C++. Sử dụng một trong các tùy chọn sau:

    - `Visual Studio Community <https://www.visualstudio.com/vs/community/>`_, phiên bản 2019 trở lên. Khuyến nghị sử dụng Visual Studio 2022. **Trong quá trình cài đặt, hãy nhớ chọn C++ trong danh sách quy trình làm việc và chọn các thành phần riêng lẻ sau:**

      .. tabs::

          .. tab:: Visual Studio 2019
              - **MSVC v142 - VS 2019 C++ {arch} build tools (Latest)** cho các kiến trúc đích. - **Windows 11 SDK (10.0.22621.0)** (đúng phiên bản).

          .. tab:: Visual Studio 2022
              - **MSVC v143 - VS 2022 C++ {arch} build tools (Latest)** cho các kiến trúc đích. - **Windows 11 SDK (10.0.22621.0)** hoặc mới hơn.

          .. tab:: Visual Studio 2026
              - **MSVC Build Tools for {arch} (Latest)** cho các kiến trúc đích. - **Windows 11 SDK (10.0.22621.0)** hoặc mới hơn.

      Nếu bạn đã cài đặt Visual Studio nhưng không có hỗ trợ C++ cho kiến trúc đích hoặc không có Windows SDK, hãy chạy lại trình cài đặt; trình cài đặt sẽ hiển thị nút **Modify**. Hỗ trợ ``x86_64``, ``x86_32`` và ``arm64``. - Có thể sử dụng `MinGW-w64 <https://mingw-w64.org/>`_ với GCC thay cho Visual Studio. Hãy đảm bảo cài đặt/cấu hình để sử dụng mô hình luồng ``posix``. **Quan trọng:** Khi sử dụng MinGW để biên dịch nhánh ``master``, bạn cần GCC 12 trở lên. Chỉ hỗ trợ ``x86_64`` và ``x86_32``. - Có thể sử dụng `MinGW-LLVM <https://github.com/mstorsjo/llvm-mingw/releases>`_ với clang thay cho Visual Studio và MinGW-w64. **Quan trọng:** Khi sử dụng MinGW để biên dịch nhánh ``master``, bạn cần clang 14 trở lên. Hỗ trợ ``x86_64``, ``x86_32`` và ``arm64``. - `Python 3.9+ <https://www.python.org/downloads/windows/>`_. **Hãy nhớ bật tùy chọn thêm Python vào** ``PATH`` **trong trình cài đặt.** - Hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`_. Khuyến nghị sử dụng bản phát hành mới nhất, đặc biệt để hỗ trợ tốt các bản Visual Studio gần đây. - :ref:`Direct3D 12 dependencies <doc_compiling_for_windows_installing_d3d12_requirements>` (có thể bỏ qua bằng tùy chọn SCons ``d3d12=no`` nếu không cần hỗ trợ Direct3D 12).

.. note:: If you have `Scoop <https://scoop.sh/>`_ installed, you can easily
          cài đặt MinGW và các phần phụ thuộc khác bằng lệnh sau:

          ::

              scoop install python mingw

          Scons vẫn cần được cài đặt thông qua pip
.. note:: If you have `MSYS2 <https://www.msys2.org/>`_ installed, you can easily
          cài đặt MinGW và các phần phụ thuộc khác bằng lệnh sau:

          ::

              pacman -S mingw-w64-x86_64-gcc mingw-w64-i686-gcc make python-pip

          Đối với mỗi hệ thống con MSYS2 MinGW, bạn nên chạy `pip3 install scons` trong shell của hệ thống đó.

.. seealso:: To get the Godot source code for compiling, see
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Thiết lập SCons
---------------

Để cài đặt SCons, hãy mở command prompt và chạy lệnh sau:

::

    python -m pip install scons

Nếu bạn nhận được thông báo ``Defaulting to user installation because normal site-packages is not writeable``, có thể bạn phải chạy lại lệnh đó với quyền nâng cao. Hãy mở một command prompt mới với tư cách Administrator rồi chạy lại lệnh để đảm bảo SCons khả dụng từ ``PATH``.

Để kiểm tra xem bạn đã cài đặt Python và SCons đúng cách chưa, bạn có thể nhập ``python --version`` và ``scons --version`` vào command prompt (``cmd.exe``).

Nếu các lệnh trên không hoạt động, hãy đảm bảo thêm Python vào biến môi trường ``PATH`` sau khi cài đặt, rồi kiểm tra lại. Bạn có thể thực hiện việc này bằng cách chạy lại trình cài đặt Python và bật tùy chọn thêm Python vào ``PATH``.

Nếu SCons không thể phát hiện bản cài đặt Visual Studio của bạn, có thể phiên bản SCons đã quá cũ. Hãy cập nhật lên phiên bản mới nhất bằng ``python -m pip install --upgrade scons``.

.. _doc_compiling_for_windows_install_vs:

Tải mã nguồn Godot
------------------

Tham khảo :ref:`doc_getting_source` để xem hướng dẫn chi tiết.

Từ đây trở đi, hướng dẫn sẽ giả định rằng bạn đã đặt mã nguồn tại ``C:\godot``.

.. warning::

    Để tránh tình trạng chậm do quá trình quét vi-rút liên tục trong khi biên dịch, hãy thêm thư mục mã nguồn Godot vào danh sách ngoại lệ trong phần mềm diệt vi-rút của bạn.

    Đối với Windows Defender, nhấn phím :kbd:`Windows`, nhập "Windows Security" rồi nhấn :kbd:`Enter`. Nhấp vào **Virus & threat protection** ở bảng bên trái. Trong **Virus & threat protection settings**, nhấp vào **Manage Settings** rồi cuộn xuống **Exclusions**. Nhấp vào **Add or remove exclusions**, sau đó thêm thư mục mã nguồn Godot.

Biên dịch
---------

Chọn trình biên dịch
~~~~~~~~~~~~~~~~~~~~

SCons sẽ tự động tìm và sử dụng bản cài đặt Visual Studio hiện có. Nếu bạn chưa cài đặt Visual Studio, SCons sẽ thử sử dụng MinGW. Nếu bạn đã cài đặt Visual Studio nhưng muốn sử dụng MinGW-w64, hãy truyền ``use_mingw=yes`` vào dòng lệnh SCons. Lưu ý rằng không thể thực hiện bản build MSVC từ shell MSYS2 hoặc MinGW. Thay vào đó, hãy sử dụng ``cmd.exe`` hoặc PowerShell. Nếu bạn sử dụng MinGW-LLVM, hãy truyền cả ``use_mingw=yes`` và ``use_llvm=yes`` vào dòng lệnh SCons.

.. tip::

    Trong quá trình phát triển, việc sử dụng trình biên dịch Visual Studio thường là lựa chọn tốt hơn, vì nó liên kết tệp nhị phân Godot nhanh hơn nhiều so với MinGW. Tuy nhiên, MinGW có thể tạo ra các tệp nhị phân được tối ưu hóa tốt hơn bằng cách sử dụng tối ưu hóa lúc liên kết (xem bên dưới), khiến nó trở thành lựa chọn tốt hơn cho việc sử dụng trong môi trường sản xuất. Điều này đặc biệt đúng với GDScript VM, vốn hoạt động tốt hơn nhiều với MinGW so với MSVC. Do đó, bạn nên sử dụng MinGW để tạo các bản build phân phối cho người chơi.

    Tất cả các tệp nhị phân Godot chính thức đều được build trong `custom containers <https://github.com/godotengine/build-containers>`__ bằng MinGW.

Chạy SCons
~~~~~~~~~~

Sau khi mở command prompt, chuyển đến thư mục gốc của mã nguồn engine (bằng ``cd``) rồi nhập:

.. code-block:: doscon

    C:\godot> scons platform=windows

.. note:: When compiling with multiple CPU threads, SCons may warn about
          Thiếu pywin32. Bạn có thể an toàn bỏ qua cảnh báo này.

.. tip::
    Nếu bạn đang biên dịch Godot để thực hiện thay đổi hoặc đóng góp cho engine, bạn có thể muốn sử dụng các tùy chọn SCons ``dev_build=yes`` hoặc ``dev_mode=yes``. Xem :ref:`doc_introduction_to_the_buildsystem_development_and_production_aliases` để biết thêm thông tin.

Nếu mọi việc diễn ra thuận lợi, tệp thực thi nhị phân kết quả sẽ được đặt tại ``C:\godot\bin\`` với tên ``godot.windows.editor.x86_32.exe`` hoặc ``godot.windows.editor.x86_64.exe``. Theo mặc định, SCons sẽ build một tệp nhị phân phù hợp với kiến trúc CPU của bạn, nhưng bạn có thể ghi đè bằng ``arch=x86_64``, ``arch=x86_32`` hoặc ``arch=arm64``.

Tệp thực thi này chứa toàn bộ engine và chạy mà không cần bất kỳ phần phụ thuộc nào. Chạy tệp này sẽ mở Project Manager.

.. tip:: If you are compiling Godot for production use, you can
         làm cho tệp thực thi cuối cùng nhỏ hơn và nhanh hơn bằng cách thêm tùy chọn SCons ``production=yes``. Tùy chọn này bật các tối ưu hóa bổ sung của trình biên dịch và tối ưu hóa lúc liên kết.

         LTO cần một khoảng thời gian để chạy và yêu cầu tối đa 30 GB RAM khả dụng trong quá trình biên dịch (tùy thuộc vào toolchain). Nếu bạn hết bộ nhớ khi sử dụng tùy chọn trên, hãy dùng ``production=yes lto=none`` hoặc ``production=yes lto=thin`` (chỉ LLVM) để có một dạng LTO nhẹ hơn nhưng kém hiệu quả hơn.

.. note:: If you want to use separate editor settings for your own Godot builds
          và các bản phát hành chính thức, bạn có thể bật
          :ref:`doc_data_paths_self_contained_mode` by creating a file called
          ``._sc_`` hoặc ``_sc_`` trong thư mục ``bin/``.

.. _doc_compiling_for_windows_installing_d3d12_requirements:

Cài đặt các yêu cầu của Direct3D 12
-----------------------------------

Theo mặc định, các bản build Godot trên Windows có hỗ trợ API đồ họa Direct3D 12. Việc biên dịch với hỗ trợ Direct3D 12 yêu cầu cài đặt thêm các phần phụ thuộc. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``d3d12=no``; khi đó, hỗ trợ Vulkan và OpenGL vẫn khả dụng.

Bạn có thể cài đặt các phần phụ thuộc cần thiết bằng cách chạy ``python misc/scripts/install_d3d12_sdk_windows.py`` trong kho mã nguồn Godot. Sau khi chạy tập lệnh này, hãy biên dịch Godot như bình thường. Tập lệnh sẽ sử dụng các đường dẫn mặc định cho từng phần phụ thuộc, trùng với các đường dẫn được dùng trong tập lệnh.

Nếu muốn thiết lập các phần phụ thuộc theo cách thủ công, bạn có thể tìm thấy các bước chi tiết bên dưới, nhưng tập lệnh trên sẽ xử lý mọi việc cho bạn (bao gồm cả các thành phần PIX và Agility SDK tùy chọn).

- `godot-nir-static library <https://github.com/godotengine/godot-nir-static/releases/>`_. Chúng tôi biên dịch các thư viện Mesa bạn cần thành một thư viện tĩnh. Hãy tải thư viện này đến bất kỳ vị trí nào, giải nén và ghi nhớ đường dẫn đến thư mục đã giải nén, vì bạn sẽ cần đường dẫn đó ở các bước bên dưới.

.. note:: You can optionally build the godot-nir-static libraries yourself with
          các bước sau:

          1. Cài đặt gói Python `mako <https://www.makotemplates.org>`_ cần thiết để tạo một số tệp. 2. Sao chép thư mục `godot-nir-static <https://github.com/godotengine/godot-nir-static>`_ và chuyển đến thư mục đó. 3. Chạy lệnh sau:

          ::

              git submodule update --init
              ./update_mesa.sh
              scons

          Nếu bạn đang build bằng MinGW-w64, hãy thêm ``use_mingw=yes`` vào lệnh ``scons``; bạn cũng có thể chỉ định kiến trúc build bằng ``arch={architecture}``. Nếu bạn đang build bằng MinGW-LLVM, hãy thêm cả ``use_mingw=yes`` và ``use_llvm=yes`` vào lệnh ``scons``.

          Nếu bạn đang build bằng MinGW và các tệp nhị phân không nằm trong ``PATH``, hãy thêm ``mingw_prefix="/path/to/mingw"`` vào lệnh ``scons``.

          Thư viện tĩnh Mesa nên được build bằng cùng trình biên dịch và cùng CRT (nếu bạn đang build bằng MinGW) mà bạn sử dụng để build Godot.

Bạn cũng có thể biên dịch với các tùy chọn sau để có thêm tính năng:

- `PIX <https://devblogs.microsoft.com/pix/download>`_ là một ứng dụng tinh chỉnh hiệu năng và gỡ lỗi dành cho các ứng dụng Direct3D12. Nếu bạn biên dịch tích hợp hỗ trợ cho ứng dụng này, bạn có thể nhận được nhiều thông tin chi tiết hơn thông qua PIX, giúp bạn tối ưu hóa trò chơi và khắc phục các lỗi đồ họa. Để sử dụng, hãy tải gói WinPixEventRuntime xuống. Bạn sẽ được chuyển đến trang gói NuGet, tại đó bạn có thể nhấp vào "Download package" để tải gói. Sau khi tải xuống, hãy đổi phần mở rộng tệp thành .zip và giải nén tệp vào một đường dẫn bất kỳ. - `Agility SDK <https://devblogs.microsoft.com/directx/directx12agility>`_ có thể được sử dụng để cung cấp quyền truy cập vào các tính năng Direct3D 12 mới nhất mà không phụ thuộc vào các bản cập nhật trình điều khiển. Để sử dụng, hãy tải gói Agility SDK mới nhất xuống. Bạn sẽ được chuyển đến trang gói NuGet, tại đó bạn có thể nhấp vào "Download package" để tải gói. Sau khi tải xuống, hãy đổi phần mở rộng tệp thành .zip và giải nén tệp vào một đường dẫn bất kỳ.

.. note:: If you use a preview version of the Agility SDK, remember to enable
          chế độ nhà phát triển trong Windows; nếu không, nó sẽ không được sử dụng.

.. note:: If you want to use a PIX with MinGW build, navigate to PIX runtime
          thư mục đó và sử dụng các lệnh sau để tạo thư viện import:

          ::

            # For x86-64:
            gendef ./bin/x64/WinPixEventRuntime.dll
            dlltool --machine i386:x86-64 --no-leading-underscore -d WinPixEventRuntime.def -D WinPixEventRuntime.dll -l ./bin/x64/libWinPixEventRuntime.a

            # For ARM64:
            gendef ./bin/ARM64/WinPixEventRuntime.dll
            dlltool --machine arm64 --no-leading-underscore -d WinPixEventRuntime.def -D WinPixEventRuntime.dll -l ./bin/ARM64/libWinPixEventRuntime.a

Khi xây dựng Godot, bạn cần cho SCons biết nơi tìm các thư viện bổ sung:

.. code-block:: doscon

    C:\godot> scons platform=windows mesa_libs=<...>

Hoặc với tất cả tùy chọn được bật:

.. code-block:: doscon

    C:\godot> scons platform=windows mesa_libs=<...> agility_sdk_path=<...> pix_path=<...>

.. note::

    Hỗ trợ PIX bị tắt theo mặc định, ngay cả khi bạn đã cài đặt nó. Để bật, hãy truyền ``use_pix=yes`` cho SCons.

.. note::

    Đối với các DLL của Agility SDK, bạn phải chọn rõ loại quy trình làm việc. Single-arch là mặc định (các DLL được sao chép vào ``bin/``). Nếu truyền ``agility_sdk_multi_arch=yes`` cho SCons, bạn sẽ chọn multi-arch. Các DLL sẽ được sao chép vào các thư mục con ``bin/<arch>/`` thích hợp và trong thời gian chạy, thư mục phù hợp sẽ được tải.

Biên dịch với hỗ trợ AccessKit
------------------------------

AccessKit cung cấp hỗ trợ cho trình đọc màn hình.

Việc biên dịch với AccessKit yêu cầu cài đặt thêm các phần phụ thuộc. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``accesskit=no``.

Bạn có thể cài đặt các phần phụ thuộc bắt buộc bằng cách chạy ``python misc/scripts/install_accesskit.py`` trong kho mã nguồn Godot. Sau khi chạy tập lệnh này, hãy biên dịch Godot như bình thường.

.. note:: You can optionally build the AccessKit libraries yourself with
          các bước sau:

          1. Sao chép thư mục `godot-accesskit-c-static <https://github.com/godotengine/godot-accesskit-c-static/>`_ và chuyển đến thư mục đó. 2. Chạy lệnh sau:

          ::

              cd accesskit-c
              cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
              cmake --build build
              cmake --install build

          Thư viện tĩnh AccessKit phải được xây dựng bằng cùng trình biên dịch và cùng CRT (nếu bạn xây dựng bằng MinGW) mà bạn sử dụng để xây dựng Godot.

          Để biên dịch Godot với bản dựng tùy chỉnh của AccessKit, hãy thêm ``accesskit_sdk_path={path}`` để cho SCons biết nơi tìm các thư viện AccessKit:

          ::

              scons platform=windows accesskit_sdk_path=<...>

Biên dịch với hỗ trợ WinRT
--------------------------

WinRT cung cấp hỗ trợ cho OneCore TTS (truy cập các giọng nói Windows 10+), giám sát thông tin màu HDR và bộ chọn emoji.

Nếu bạn xây dựng bằng MinGW, việc biên dịch với WinRT yêu cầu cài đặt thêm các phần phụ thuộc. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``winrt=no``.

Bạn có thể cài đặt các phần phụ thuộc bắt buộc bằng cách chạy ``python misc/scripts/install_winrt.py`` trong kho mã nguồn Godot. Sau khi chạy tập lệnh này, hãy biên dịch Godot như bình thường.

.. note:: You can optionally build the WinRT headers yourself with
          các bước sau:

          1. Sao chép thư mục `winrt-mingw <https://github.com/godotengine/winrt-mingw>`_ và chuyển đến thư mục đó. 2. Chạy lệnh sau:

          ::

              cmake -Bbuild -DCMAKE_BUILD_TYPE=Release -DCPPWINRT_BUILD_VERSION=2.0.250303.1 -DBUILD_TESTING=OFF cppwinrt/
              echo "" > build/app.manifest.rc
              cmake --build build
              ./build/cppwinrt.exe -input windows-rs/crates/libs/bindgen/default/ -output include/

          Để biên dịch Godot với bản dựng tùy chỉnh của WinRT, hãy thêm ``winrt_path={path}`` để cho SCons biết nơi tìm các header AccessKit:

          ::

              scons platform=windows winrt_path=<...>

Biên dịch với hỗ trợ ANGLE
--------------------------

ANGLE cung cấp một lớp chuyển đổi từ OpenGL ES 3.x sang Direct3D 11 và có thể được sử dụng để cải thiện khả năng hỗ trợ trình kết xuất Compatibility trên một số GPU cũ có trình điều khiển OpenGL lỗi thời, cũng như trên Windows dành cho ARM.

Việc biên dịch với ANGLE yêu cầu cài đặt thêm các phần phụ thuộc. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``angle=no``.

Bạn có thể cài đặt các phần phụ thuộc bắt buộc bằng cách chạy ``python misc/scripts/install_angle.py`` trong kho mã nguồn Godot. Sau khi chạy tập lệnh này, hãy biên dịch Godot như bình thường.

.. note:: You can optionally build the godot-angle-static libraries yourself with
          các bước sau:

          1. Sao chép thư mục `godot-angle-static <https://github.com/godotengine/godot-angle-static>`_ và chuyển đến thư mục đó. 2. Chạy lệnh sau:

          ::

              git submodule update --init
              ./update_angle.sh
              scons

          Nếu bạn xây dựng bằng MinGW, hãy thêm ``use_mingw=yes`` vào lệnh; bạn cũng có thể chỉ định kiến trúc bản dựng bằng ``arch={architecture}``. Nếu bạn xây dựng bằng MinGW-LLVM, hãy thêm cả ``use_mingw=yes`` và ``use_llvm=yes`` vào lệnh ``scons``.

          Nếu bạn xây dựng bằng MinGW và các tệp nhị phân không nằm trong ``PATH``, hãy thêm ``mingw_prefix="/path/to/mingw"`` vào lệnh ``scons``.

          Thư viện tĩnh ANGLE phải được xây dựng bằng cùng trình biên dịch và cùng CRT (nếu bạn xây dựng bằng MinGW) mà bạn sử dụng để xây dựng Godot.

          Để biên dịch Godot với bản dựng tùy chỉnh của ANGLE, hãy thêm ``angle_libs={path}`` để cho SCons biết nơi tìm các thư viện ANGLE:

          ::

              scons platform=windows angle_libs=<...>

Phát triển trong Visual Studio
------------------------------

Không bắt buộc phải sử dụng IDE để biên dịch Godot vì SCons xử lý mọi việc. Tuy nhiên, nếu bạn định phát triển engine hoặc gỡ lỗi mã C++ của engine, bạn có thể quan tâm đến việc cấu hình trình chỉnh sửa mã hoặc IDE.

Các trình chỉnh sửa dựa trên thư mục không yêu cầu thiết lập cụ thể nào để bắt đầu làm việc với mã nguồn Godot. Để chỉnh sửa các dự án bằng Visual Studio, chúng cần được thiết lập dưới dạng một solution.

Bạn có thể tạo solution Visual Studio thông qua SCons bằng cách chạy SCons với tham số ``vsproj=yes``, như sau:

::

   scons platform=windows vsproj=yes

Bây giờ bạn có thể mở mã nguồn Godot trong một solution Visual Studio và xây dựng Godot bằng nút **Build** của Visual Studio.

.. seealso:: See :ref:`doc_configuring_an_ide_vs` for further details.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Nếu gặp lỗi biên dịch khi sử dụng MSVC, hãy đảm bảo đã cài đặt các bản cập nhật mới nhất. Bạn có thể thực hiện việc này bằng cách khởi động IDE Visual Studio và sử dụng
:button:`Continue without code`, then :menu:`Help > Check for Updates` in the
thanh menu ở trên cùng. Cài đặt tất cả bản cập nhật, sau đó thử biên dịch lại.

Biên dịch chéo cho Windows từ các hệ điều hành khác
---------------------------------------------------

Nếu bạn là người dùng Linux hoặc macOS, bạn cần cài đặt `MinGW-w64 <https://www.mingw-w64.org/>`__, thường có các biến thể 32-bit và 64-bit, hoặc `MinGW-LLVM <https://github.com/mstorsjo/llvm-mingw/releases>`_, được cung cấp dưới dạng một kho lưu trữ duy nhất cho mọi kiến trúc đích. Tên gói có thể khác nhau tùy theo bản phân phối của bạn; dưới đây là một số tên phổ biến:

+----------------+--------------------------------------------------------------+ | **Arch Linux** | :: | | | |
| | pacman -S mingw-w64 |
+++++++++++++++++++++++++
| **Debian** / | :: | | **Ubuntu** | |
| | apt install mingw-w64 |
+++++++++++++++++++++++++++
| **Fedora** | :: | | | | | | dnf install mingw64-gcc-c++ mingw64-winpthreads-static \ |
| | mingw32-gcc-c++ mingw32-winpthreads-static |
++++++++++++++++++++++++++++++++++++++++++++++++
| **macOS** | :: | | | |
| | brew install mingw-w64 |
++++++++++++++++++++++++++++
| **Mageia** | :: | | | | | | urpmi mingw64-gcc-c++ mingw64-winpthreads-static \ |
| | mingw32-gcc-c++ mingw32-winpthreads-static |
++++++++++++++++++++++++++++++++++++++++++++++++

Trước khi bắt đầu biên dịch, SCons sẽ kiểm tra các tệp nhị phân sau trong biến môi trường ``PATH`` của bạn:

::

    # for MinGW-w64
    i686-w64-mingw32-gcc
    x86_64-w64-mingw32-gcc

    # for MinGW-LLVM
    aarch64-w64-mingw32-clang
    i686-w64-mingw32-clang
    x86_64-w64-mingw32-clang

Nếu các tệp nhị phân không nằm trong ``PATH`` (ví dụ: ``/usr/bin``), bạn có thể định nghĩa biến môi trường sau để cung cấp gợi ý cho hệ thống xây dựng:

::

    export MINGW_PREFIX="/path/to/mingw"

Trong đó ``/path/to/mingw`` là đường dẫn chứa thư mục ``bin``, nơi ``i686-w64-mingw32-gcc`` và ``x86_64-w64-mingw32-gcc`` được đặt (ví dụ: ``/opt/mingw-w64`` nếu các tệp nhị phân nằm trong ``/opt/mingw-w64/bin``).

Để đảm bảo bạn đang thực hiện đúng, việc chạy lệnh sau trong shell sẽ cho kết quả là một trình biên dịch hoạt động được (đầu ra phiên bản có thể khác nhau tùy theo hệ thống của bạn):

::

    ${MINGW_PREFIX}/bin/x86_64-w64-mingw32-gcc --version
    # x86_64-w64-mingw32-gcc (GCC) 13.2.0

.. note:: If you are building with MinGW-LLVM, add ``use_llvm=yes`` to the ``scons`` command.
.. note:: When cross-compiling for Windows using MinGW-w64, keep in mind only
          Các kiến trúc ``x86_64`` và ``x86_32`` được hỗ trợ. MinGW-LLVM cũng hỗ trợ ``arm64``. Hãy đảm bảo chỉ định đúng tùy chọn ``arch=`` khi gọi SCons nếu xây dựng từ một kiến trúc khác.

Khắc phục sự cố
~~~~~~~~~~~~~~~

Biên dịch chéo từ một số phiên bản Ubuntu có thể dẫn đến `lỗi này <https://github.com/godotengine/godot/issues/9258>`_, do cấu hình mặc định không hỗ trợ luồng POSIX.

Bạn có thể thay đổi cấu hình đó bằng cách làm theo các hướng dẫn sau, đối với 64-bit:

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

Tạo template xuất Windows
-------------------------

Các template xuất Windows được tạo bằng cách biên dịch Godot mà không có editor, với các cờ sau:

.. code-block:: doscon

    C:\godot> scons platform=windows target=template_debug arch=x86_32
    C:\godot> scons platform=windows target=template_release arch=x86_32
    C:\godot> scons platform=windows target=template_debug arch=x86_64
    C:\godot> scons platform=windows target=template_release arch=x86_64
    C:\godot> scons platform=windows target=template_debug arch=arm64
    C:\godot> scons platform=windows target=template_release arch=arm64

Nếu dự định thay thế các template xuất tiêu chuẩn, hãy sao chép chúng vào vị trí sau, thay ``<version>`` bằng mã nhận dạng phiên bản (chẳng hạn như ``4.2.1.stable`` hoặc ``4.3.dev``):

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

Tuy nhiên, nếu đang sử dụng các module tùy chỉnh hoặc mã engine tùy chỉnh, thay vào đó bạn có thể muốn cấu hình các tệp nhị phân của mình dưới dạng template xuất tùy chỉnh trong menu xuất dự án. Bạn phải bật **Advanced Options** để thiết lập tùy chọn này.

.. image:: img/wintemplates.webp

Trong trường hợp này, bạn không cần sao chép chúng; chỉ cần tham chiếu đến các tệp kết quả trong thư mục ``bin\`` của thư mục mã nguồn Godot, để lần xây dựng tiếp theo sẽ tự động tham chiếu các template tùy chỉnh.
