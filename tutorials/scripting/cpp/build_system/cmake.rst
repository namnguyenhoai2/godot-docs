.. _doc_godot_cpp_build_system_cmake:

Hệ thống build phụ: Làm việc với CMake
======================================

.. seealso::

    Trang này hướng dẫn cách biên dịch godot-cpp. Nếu bạn muốn biên dịch Godot thay vì godot-cpp, hãy xem :ref:`doc_introduction_to_the_buildsystem`.

Bên cạnh hệ thống build dựa trên SCons_, godot-cpp cũng cung cấp tệp CMakeLists.txt_ để hỗ trợ người dùng muốn sử dụng CMake_ thay cho SCons làm hệ thống build.

Mặc dù vẫn được tích cực hỗ trợ, hệ thống CMake được xem là thứ cấp so với hệ thống build SCons. Điều này có nghĩa là nó có thể thiếu một số tính năng có sẵn trong các project sử dụng SCons.

.. _CMakeLists.txt: https://github.com/godotengine/godot-cpp/blob/master/CMakeLists.txt
.. _CMake: http://cmake.org
.. _Scons: http://scons.org

Giới thiệu
----------

Việc biên dịch godot-cpp độc lập với một project extension chủ yếu dành cho các nhà phát triển godot-cpp, những người duy trì package và CI/CD.

Ví dụ về cách sử dụng CMake để dùng thư viện godot-cpp như một phần của project extension:

* `godot-cpp-template <https://github.com/godotengine/godot-cpp-template/>`__ * `godot_roguelite <https://github.com/vorlac/godot-roguelite/>`__ * `godot-orchestrator <https://github.com/CraterCrash/godot-orchestrator/>`__

Các ví dụ về cách cấu hình godot-cpp được liệt kê ở cuối trang; nhiều ví dụ trong số đó có thể hữu ích khi cấu hình project của bạn.

``Debug`` của CMake so với ``template_debug`` của Godot
-------------------------------------------------------

Một vấn đề đã xuất hiện trong nhiều cuộc thảo luận là việc đánh đồng quá trình biên dịch mã nguồn C++ khi bật debug symbols với việc biên dịch một Godot extension khi bật các debug features. Hai khái niệm này không loại trừ lẫn nhau.

Debug Features
~~~~~~~~~~~~~~

Bật một định nghĩa pre-processor để biên dịch có chọn lọc phần code hỗ trợ người dùng Godot extension với project riêng của họ.

Debug features được bật trong các build ``editor`` và ``template_debug``, có thể chỉ định trong giai đoạn configure như sau:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -DGODOTCPP_TARGET=<target choice>

Debug
~~~~~

Thiết lập các compiler flags để tạo debug symbols, hỗ trợ các nhà phát triển Godot extension debug extension của họ.

``Debug`` là build type mặc định cho các project CMake; cách chọn build type khác tùy thuộc vào generator được sử dụng:

* Đối với generator single-config, thêm ``-DCMAKE_BUILD_TYPE=<type>`` vào configure command. * Đối với generator multi-config, thêm ``--config <type>`` vào build command.

Trong đó ``<type>`` là một trong ``Debug``, ``Release``, ``RelWithDebInfo`` và ``MinSizeRel``.

Các khác biệt so với SCons
--------------------------

Không phải toàn bộ code từ hệ thống SCons đều có thể được biểu diễn hoàn hảo trong CMake; sau đây là những khác biệt đáng chú ý:

- ``debug_symbols``

    Không còn là một tùy chọn rõ ràng và được bật khi sử dụng các cấu hình build CMake; ``Debug``, ``RelWithDebInfo``.

- ``dev_build``

    Không định nghĩa ``NDEBUG`` khi bị tắt; ``NDEBUG`` được thiết lập khi sử dụng các cấu hình build CMake; ``Release``, ``MinSizeRel``.

- ``arch``

    CMake thiết lập architecture thông qua các toolchain files; macOS universal được điều khiển thông qua property ``CMAKE_OSX_ARCHITECTURES``, property này được sao chép vào các target khi chúng được định nghĩa.

- ``debug_crt``

    CMake điều khiển việc liên kết với các Windows runtime libraries bằng cách sao chép giá trị của ``CMAKE_MSVC_RUNTIME_LIBRARIES`` vào các target khi chúng được định nghĩa. godot-cpp sẽ thiết lập biến này nếu biến chưa được thiết lập. Vì vậy, hãy include nó trước các dependency khác để giá trị được truyền qua các project.

Hướng dẫn cơ bản
----------------

Clone git repository
~~~~~~~~~~~~~~~~~~~~

.. code-block:: shell

    git clone https://github.com/godotengine/godot-cpp.git
    Cloning into 'godot-cpp'...
    ...

Configure build
~~~~~~~~~~~~~~~

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -G Ninja

- ``-S`` Chỉ định source directory là ``godot-cpp`` - ``-B`` Chỉ định build directory là ``cmake-build`` - ``-G`` Chỉ định Generator là ``Ninja``

Source directory trong ví dụ này là source root của godot-cpp vừa được clone. CMake cũng sẽ diễn giải path đầu tiên trong command là source path; hoặc nếu đã chỉ định một build path hiện có, nó sẽ suy ra source path từ build cache.

Ba command sau đây là tương đương:

.. code-block:: shell

    # Current working directory là source root của godot-cpp.
    cmake . -B build-dir

    # Current working directory là một godot-cpp/build-dir trống.
    cmake ../

    # Current working directory là một build path hiện có.
    cmake .

Build directory được chỉ định để các file được tạo không làm lộn xộn source tree bằng các build artifacts.

CMake không build code; nó tạo các file mà một build tool sử dụng. Trong trường hợp này, generator ``Ninja`` tạo các build files của Ninja_.

Để xem danh sách các generator, chạy ``cmake --help``.

.. _Ninja: https://ninja-build.org/

Các tùy chọn build
~~~~~~~~~~~~~~~~~~

Để liệt kê các tùy chọn khả dụng, sử dụng các command flags ``-L[AH]``. ``A`` dùng cho các tùy chọn nâng cao, còn ``H`` dùng cho các chuỗi trợ giúp:

.. code-block:: shell

    cmake -S godot-cpp -LH

Các tùy chọn được chỉ định trên command line khi configure, ví dụ:

.. code-block:: shell

    cmake -S godot-cpp -DGODOTCPP_USE_HOT_RELOAD:BOOL=ON \
        -DGODOTCPP_PRECISION:STRING=double \
        -DCMAKE_BUILD_TYPE:STRING=Debug

Xem setting-build-variables_ và build-configurations_ để biết thêm thông tin.

.. _setting-build-variables: https://cmake.org/cmake/help/latest/guide/user-interaction/index.html#setting-build-variables
.. _build-configurations: https://cmake.org/cmake/help/latest/manual/cmake-buildsystem.7.html#build-configurations

Danh sách tùy chọn không đầy đủ:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: text

    // Path đến tệp GDExtension API JSON tùy chỉnh.
    // (được ưu tiên hơn GODOTCPP_GDEXTENSION_DIR)
    // ( /path/to/custom_api_file )
    GODOTCPP_CUSTOM_API_FILE:FILEPATH=

    // Buộc tắt exception handling code. (ON|OFF)
    GODOTCPP_DISABLE_EXCEPTIONS:BOOL=ON

    // Path đến directory tùy chỉnh chứa GDExtension interface
    // header và API JSON file. ( /path/to/gdextension_dir )
    GODOTCPP_GDEXTENSION_DIR:PATH=gdextension

    // Thiết lập mức precision của floating-point. (single|double)
    GODOTCPP_PRECISION:STRING=single

    // Bật phần accounting bổ sung cần thiết để hỗ trợ hot reload. (ON|OFF)
    GODOTCPP_USE_HOT_RELOAD:BOOL=

Biên dịch
~~~~~~~~~

Yêu cầu CMake gọi build system mà nó đã tạo trong directory được chỉ định. Target mặc định là ``template_debug`` và build configuration mặc định là Debug.

.. code-block:: shell

    cmake --build cmake-build

Ví dụ
-----

Mặc dù dành cho các nhà phát triển godot-cpp, những người duy trì package và CI/CD, các ví dụ này có thể giúp bạn cấu hình project extension của riêng mình.

Các ví dụ thực tế về cách dùng thư viện godot-cpp như một phần của project extension được liệt kê trong `Giới thiệu`_.

Bật Integration Testing
~~~~~~~~~~~~~~~~~~~~~~~

Testing target ``godot-cpp-test`` được bảo vệ bởi ``GODOTCPP_ENABLE_TESTING``, tùy chọn này mặc định bị tắt.

Để configure và build project godot-cpp nhằm bật các integration testing targets, command sẽ có dạng như sau:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -DGODOTCPP_ENABLE_TESTING=YES
    cmake --build cmake-build --target godot-cpp-test

Windows và MSVC - Release
~~~~~~~~~~~~~~~~~~~~~~~~~

Miễn là CMake được cài đặt từ trang `CMake Downloads`_ và nằm trong PATH, đồng thời Microsoft Visual Studio được cài đặt với hỗ trợ C++, CMake sẽ phát hiện compiler MSVC.

Lưu ý rằng Visual Studio là Multi-Config Generator, vì vậy build configuration cần được chỉ định trong thời điểm build, ví dụ ``--config Release``.

.. _CMake downloads: https://cmake.org/download/

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -DGODOTCPP_ENABLE_TESTING=YES
    cmake --build cmake-build -t godot-cpp-test --config Release

MSys2/clang64, "Ninja" - Debug
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Assumes the ``ming-w64-clang-x86_64``-toolchain is installed.

Lưu ý rằng Ninja là Single-Config Generator, vì vậy build type cần được chỉ định trong thời điểm configure.

Sử dụng shell ``msys2/clang64``:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -G"Ninja" \
        -DGODOTCPP_ENABLE_TESTING=YES -DCMAKE_BUILD_TYPE=Release
    cmake --build cmake-build -t godot-cpp-test

MSys2/clang64, "Ninja Multi-Config" - dev_build, Debug Symbols
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Assumes the ``ming-w64-clang-x86_64``-toolchain is installed.

Lần này, chúng ta chọn generator 'Ninja Multi-Config', vì vậy build type được chỉ định trong thời điểm build.

Sử dụng shell ``msys2/clang64``:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -G"Ninja Multi-Config" \
        -DGODOTCPP_ENABLE_TESTING=YES -DGODOTCPP_DEV_BUILD:BOOL=ON
    cmake --build cmake-build -t godot-cpp-test --config Debug

Emscripten cho nền tảng web
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cho đến nay, quy trình này mới chỉ được kiểm thử trên Windows. Bạn có thể sử dụng workflow ví dụ sau:

- Clone và cài đặt các công cụ Emscripten mới nhất vào ``c:\emsdk``. - Sử dụng ``C:\emsdk\emsdk.ps1 activate latest`` để bật environment từ powershell trong shell hiện tại. - Utility ``emcmake.bat`` thêm emscripten toolchain vào command CMake. Bạn cũng có thể thêm thủ công; location được liệt kê bên trong tệp ``emcmake.bat``

.. code-block:: powershell

    C:\emsdk\emsdk.ps1 activate latest
    emcmake.bat cmake -S godot-cpp -B cmake-build-web -DCMAKE_BUILD_TYPE=Release
    cmake --build cmake-build-web

Cross Compile Android từ Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có hai hướng riêng biệt mà bạn có thể chọn khi configure cho android.

Sử dụng các biến ``CMAKE_ANDROID_*`` được chỉ định trên command line hoặc trong toolchain file của riêng bạn, như được liệt kê trong tài liệu cmake-toolchains_.

.. _cmake-toolchains: https://cmake.org/cmake/help/latest/manual/cmake-toolchains.7.html#cross-compiling-for-android-with-the-ndk

Hoặc sử dụng toolchain và các script do Android SDK cung cấp, rồi thực hiện thay đổi bằng các biến ``ANDROID_*`` được liệt kê tại đó. Trong đó ``<version>`` là phiên bản NDK bạn đã cài đặt (đã kiểm thử với `28.1.13356709`), còn ``<platform>`` là dành cho Android sdk platform (đã kiểm thử với ``android-29``).

.. warning::

    Website Android SDK nêu rõ rằng họ không hỗ trợ sử dụng phương thức tích hợp sẵn của CMake và khuyến nghị bạn sử dụng các toolchain files của họ.

    .. _website: https://developer.android.com/ndk/guides/cmake

Sử dụng toolchain file của riêng bạn
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Như được mô tả trong tài liệu CMake:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build --toolchain my_toolchain.cmake
    cmake --build cmake-build -t template_release

Thực hiện thao tác tương đương chỉ bằng command line:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build \
        -DCMAKE_SYSTEM_NAME=Android \
        -DCMAKE_SYSTEM_VERSION=<platform> \
        -DCMAKE_ANDROID_ARCH_ABI=<arch> \
        -DCMAKE_ANDROID_NDK=/path/to/android-ndk
    cmake --build cmake-build

Sử dụng Android SDK toolchain file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Mặc định này sử dụng phiên bản được hỗ trợ tối thiểu và armv7-a:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build \
        --toolchain $ANDROID_HOME/ndk/<version>/build/cmake/android.toolchain.cmake
    cmake --build cmake-build

Chỉ định Android platform và ABI:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build \
        --toolchain $ANDROID_HOME/ndk/<version>/build/cmake/android.toolchain.cmake \
        -DANDROID_PLATFORM:STRING=android-29 \
        -DANDROID_ABI:STRING=armeabi-v7a
    cmake --build cmake-build
