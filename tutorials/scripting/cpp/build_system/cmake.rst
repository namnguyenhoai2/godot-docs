.. _doc_godot_cpp_build_system_cmake:

Hệ thống build thứ cấp: Làm việc với CMake
==========================================

.. seealso::

    Trang này trình bày cách biên dịch godot-cpp. Nếu bạn muốn biên dịch Godot thay vì godot-cpp, hãy xem :ref:`doc_introduction_to_the_buildsystem`.

Bên cạnh hệ thống build dựa trên SCons_, godot-cpp cũng cung cấp tệp CMakeLists.txt_ để hỗ trợ người dùng muốn sử dụng CMake_ thay cho SCons làm hệ thống build.

Mặc dù vẫn được hỗ trợ tích cực, hệ thống CMake được xem là thứ cấp so với hệ thống build SCons. Điều này có nghĩa là hệ thống này có thể thiếu một số tính năng hiện có trong các project sử dụng SCons.

.. _CMakeLists.txt: https://github.com/godotengine/godot-cpp/blob/master/CMakeLists.txt
.. _CMake: http://cmake.org
.. _Scons: http://scons.org

.. _`Introduction`:

Giới thiệu
----------

Việc biên dịch godot-cpp độc lập với một project extension chủ yếu dành cho các developer godot-cpp, người duy trì package và CI/CD.

Các ví dụ về cách sử dụng CMake để dùng thư viện godot-cpp như một phần của project extension:

* `godot-cpp-template <https://github.com/godotengine/godot-cpp-template/>`__
* `godot_roguelite <https://github.com/vorlac/godot-roguelite/>`__
* `godot-orchestrator <https://github.com/CraterCrash/godot-orchestrator/>`__

Các ví dụ về cách cấu hình godot-cpp được liệt kê ở cuối trang; nhiều ví dụ trong số đó có thể hữu ích khi cấu hình project của bạn.

``Debug`` của CMake so với ``template_debug`` của Godot
-------------------------------------------------------

Một vấn đề xuất hiện trong nhiều cuộc thảo luận là sự nhầm lẫn giữa việc biên dịch mã nguồn C++ với debug symbol được bật và việc biên dịch một Godot extension với các tính năng debug được bật. Hai khái niệm này không loại trừ lẫn nhau.

Tính năng debug
~~~~~~~~~~~~~~~

Bật một định nghĩa tiền xử lý để biên dịch có chọn lọc mã giúp người dùng Godot extension làm việc với project của riêng họ.

Các tính năng debug được bật trong các bản build ``editor`` và ``template_debug``, có thể được chỉ định trong giai đoạn configure như sau:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -DGODOTCPP_TARGET=<target choice>

Debug
~~~~~

Thiết lập các compiler flag để tạo debug symbol, giúp developer Godot extension debug extension của họ.

``Debug`` là kiểu build mặc định cho các project CMake; cách chọn kiểu khác tùy thuộc vào generator được sử dụng:

* Đối với generator cấu hình đơn, thêm ``-DCMAKE_BUILD_TYPE=<type>`` vào lệnh configure.
* Đối với generator đa cấu hình, thêm ``--config <type>`` vào lệnh build.

Trong đó ``<type>`` là một trong ``Debug``, ``Release``, ``RelWithDebInfo`` và ``MinSizeRel``.

Khác biệt so với SCons
----------------------

Không phải mọi mã từ hệ thống SCons đều có thể được biểu diễn hoàn hảo trong CMake. Sau đây là những khác biệt đáng chú ý:

- ``debug_symbols``

    Không còn là một tùy chọn tường minh và được bật khi sử dụng các cấu hình build CMake; ``Debug``, ``RelWithDebInfo``.

- ``dev_build``

    Không định nghĩa ``NDEBUG`` khi bị tắt; ``NDEBUG`` được thiết lập khi sử dụng các cấu hình build CMake; ``Release``, ``MinSizeRel``.

- ``arch``

    CMake thiết lập architecture thông qua các toolchain file; macOS universal được điều khiển thông qua property ``CMAKE_OSX_ARCHITECTURES``, property này được sao chép sang các target khi chúng được định nghĩa.

- ``debug_crt``

    CMake kiểm soát việc liên kết với các thư viện runtime của Windows bằng cách sao chép giá trị của ``CMAKE_MSVC_RUNTIME_LIBRARIES`` sang các target khi chúng được định nghĩa. godot-cpp sẽ thiết lập biến này nếu biến chưa được thiết lập. Vì vậy, hãy include nó trước các dependency khác để giá trị được truyền qua các project.

Hướng dẫn cơ bản
----------------

Clone git repository
~~~~~~~~~~~~~~~~~~~~

.. code-block:: shell

    git clone https://github.com/godotengine/godot-cpp.git
    Cloning into 'godot-cpp'...
    ...

Cấu hình build
~~~~~~~~~~~~~~

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -G Ninja

- ``-S`` Chỉ định source directory là ``godot-cpp``
- ``-B`` Chỉ định build directory là ``cmake-build``
- ``-G`` Chỉ định Generator là ``Ninja``

Source directory trong ví dụ này là source root của godot-cpp vừa được clone. CMake cũng sẽ diễn giải path đầu tiên trong lệnh là source path hoặc, nếu một build path hiện có được chỉ định, sẽ suy ra source path từ build cache.

Ba lệnh sau đây tương đương:

.. code-block:: shell

    # Thư mục làm việc hiện tại là source root của godot-cpp.
    cmake . -B build-dir

    # Thư mục làm việc hiện tại là một godot-cpp/build-dir trống.
    cmake ../

    # Thư mục làm việc hiện tại là một build path hiện có.
    cmake .

Build directory được chỉ định để các file được tạo ra không làm lộn xộn source tree bằng các build artifact.

CMake không build code mà tạo ra các file được build tool sử dụng; trong trường hợp này, generator ``Ninja`` tạo các file build Ninja_.

Để xem danh sách generator, hãy chạy ``cmake --help``.

.. _Ninja: https://ninja-build.org/

Tùy chọn build
~~~~~~~~~~~~~~

Để liệt kê các tùy chọn hiện có, hãy sử dụng các command flag ``-L[AH]``. ``A`` dành cho các tùy chọn nâng cao, còn ``H`` dành cho các chuỗi trợ giúp:

.. code-block:: shell

    cmake -S godot-cpp -LH

Các tùy chọn được chỉ định trên command line khi cấu hình, ví dụ:

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

    // Path to a custom GDExtension API JSON file.
    // (takes precedence over GODOTCPP_GDEXTENSION_DIR)
    // ( /path/to/custom_api_file )
    GODOTCPP_CUSTOM_API_FILE:FILEPATH=

    // Force disabling exception handling code. (ON|OFF)
    GODOTCPP_DISABLE_EXCEPTIONS:BOOL=ON

    // Path to a custom directory containing the GDExtension interface
    // header and API JSON file. ( /path/to/gdextension_dir )
    GODOTCPP_GDEXTENSION_DIR:PATH=gdextension

    // Set the floating-point precision level. (single|double)
    GODOTCPP_PRECISION:STRING=single

    // Enable the extra accounting required to support hot reload. (ON|OFF)
    GODOTCPP_USE_HOT_RELOAD:BOOL=

Biên dịch
~~~~~~~~~

Yêu cầu CMake gọi hệ thống build mà nó đã tạo trong directory được chỉ định. Target mặc định là ``template_debug`` và cấu hình build mặc định là Debug.

.. code-block:: shell

    cmake --build cmake-build

Ví dụ
-----

Mặc dù dành cho các developer godot-cpp, người duy trì package và CI/CD, những ví dụ này có thể giúp bạn cấu hình project extension của riêng mình.

Các ví dụ thực tế về cách dùng thư viện godot-cpp như một phần của project extension được liệt kê trong `Introduction`_.

Bật kiểm thử integration
~~~~~~~~~~~~~~~~~~~~~~~~

Testing target ``godot-cpp-test`` được bảo vệ bởi ``GODOTCPP_ENABLE_TESTING``, tùy chọn này mặc định được tắt.

Để cấu hình và build project godot-cpp nhằm bật các testing target integration, lệnh sẽ có dạng như sau:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -DGODOTCPP_ENABLE_TESTING=YES
    cmake --build cmake-build --target godot-cpp-test

Windows và MSVC - Release
~~~~~~~~~~~~~~~~~~~~~~~~~

Miễn là CMake được cài đặt từ trang `CMake Downloads <CMake Downloads_>`_ và nằm trong PATH, đồng thời Microsoft Visual Studio được cài đặt với hỗ trợ C++, CMake sẽ phát hiện compiler MSVC.

Lưu ý rằng Visual Studio là một Multi-Config Generator, vì vậy cấu hình build cần được chỉ định tại thời điểm build, ví dụ: ``--config Release``.

.. _CMake downloads: https://cmake.org/download/

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -DGODOTCPP_ENABLE_TESTING=YES
    cmake --build cmake-build -t godot-cpp-test --config Release

MSys2/clang64, "Ninja" - Debug
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Giả định rằng ``ming-w64-clang-x86_64``-toolchain đã được cài đặt.

Lưu ý rằng Ninja là một Single-Config Generator, vì vậy build type cần được chỉ định tại thời điểm cấu hình.

Sử dụng shell ``msys2/clang64``:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -G"Ninja" \
        -DGODOTCPP_ENABLE_TESTING=YES -DCMAKE_BUILD_TYPE=Release
    cmake --build cmake-build -t godot-cpp-test

MSys2/clang64, "Ninja Multi-Config" - dev_build, Debug Symbols
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Giả định rằng ``ming-w64-clang-x86_64``-toolchain đã được cài đặt.

Lần này, chúng ta chọn generator 'Ninja Multi-Config', vì vậy build type được chỉ định tại thời điểm build.

Sử dụng shell ``msys2/clang64``:

.. code-block:: shell

    cmake -S godot-cpp -B cmake-build -G"Ninja Multi-Config" \
        -DGODOTCPP_ENABLE_TESTING=YES -DGODOTCPP_DEV_BUILD:BOOL=ON
    cmake --build cmake-build -t godot-cpp-test --config Debug

Emscripten cho nền tảng web
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Cho đến nay, quy trình này mới chỉ được kiểm thử trên Windows. Bạn có thể sử dụng quy trình mẫu sau:

- Clone và cài đặt các công cụ Emscripten mới nhất vào ``c:\emsdk``.
- Sử dụng ``C:\emsdk\emsdk.ps1 activate latest`` để bật môi trường từ powershell trong shell hiện tại.
- Tiện ích ``emcmake.bat`` thêm emscripten toolchain vào lệnh CMake. Bạn cũng có thể thêm thủ công; vị trí được liệt kê trong tệp ``emcmake.bat``

.. code-block:: powershell

    C:\emsdk\emsdk.ps1 activate latest
    emcmake.bat cmake -S godot-cpp -B cmake-build-web -DCMAKE_BUILD_TYPE=Release
    cmake --build cmake-build-web

Cross Compile Android từ Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Có hai hướng riêng biệt mà bạn có thể chọn khi cấu hình cho android.

Sử dụng các biến ``CMAKE_ANDROID_*`` được chỉ định trên command line hoặc trong toolchain file của riêng bạn, như được liệt kê trong tài liệu cmake-toolchains_.

.. _cmake-toolchains: https://cmake.org/cmake/help/latest/manual/cmake-toolchains.7.html#cross-compiling-for-android-with-the-ndk

Hoặc sử dụng toolchain và các script do Android SDK cung cấp, rồi thực hiện thay đổi bằng các biến ``ANDROID_*`` được liệt kê ở đó. Trong đó, ``<version>`` là phiên bản NDK bạn đã cài đặt (đã kiểm thử với `28.1.13356709`) và ``<platform>`` là phiên bản dành cho Android sdk platform (đã kiểm thử với ``android-29``).

.. warning::

    website_ của Android SDK nêu rõ rằng họ không hỗ trợ sử dụng phương thức tích hợp sẵn của CMake và khuyến nghị bạn dùng các toolchain file của họ.

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

Sử dụng toolchain file của Android SDK
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Theo mặc định, phiên bản tối thiểu được hỗ trợ và armv7-a sẽ được sử dụng:

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
