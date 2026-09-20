.. _doc_compiling_for_macos:

Biên dịch cho macOS
===================

.. highlight:: shell

.. note::

    Trang này mô tả cách biên dịch các tệp nhị phân của trình chỉnh sửa macOS và các mẫu xuất từ mã nguồn. Nếu bạn muốn xuất dự án của mình sang macOS, hãy đọc :ref:`doc_exporting_for_macos`.

Yêu cầu
-------

Để biên dịch trên macOS, cần có những thành phần sau:

- `Python 3.9+ <https://www.python.org/downloads/macos/>`_. - hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`_. - `Xcode <https://apps.apple.com/us/app/xcode/id497799835>`_ (hoặc Command Line Tools for Xcode nhẹ hơn). - `Vulkan SDK <https://sdk.lunarg.com/sdk/download/latest/mac/vulkan-sdk.dmg>`_ cho MoltenVK (macOS không hỗ trợ Vulkan ngay từ đầu). Có thể nhanh chóng cài đặt phiên bản Vulkan SDK mới nhất bằng cách chạy ``misc/scripts/install_vulkan_sdk_macos.sh`` trong kho mã nguồn Godot.

.. note:: If you have `Homebrew <https://brew.sh/>`_ installed, you can easily
          cài đặt SCons bằng lệnh sau:

          ::

              brew install scons

          Việc cài đặt Homebrew cũng sẽ tự động tải Command Line Tools for Xcode nếu bạn chưa có.

          Tương tự, nếu đã cài đặt `MacPorts <https://www.macports.org/>`_, bạn có thể dễ dàng cài đặt SCons bằng lệnh sau:

          ::

              sudo port install scons

.. seealso:: To get the Godot source code for compiling, see
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Biên dịch
---------

Mở terminal và đi đến thư mục gốc của mã nguồn engine.

Để biên dịch cho máy Mac sử dụng Intel (x86-64), hãy dùng:

::

    scons platform=macos arch=x86_64

Để biên dịch cho máy Mac sử dụng Apple Silicon (ARM64), hãy dùng:

::

    scons platform=macos arch=arm64

.. tip::
    Nếu đang biên dịch Godot để thực hiện thay đổi hoặc đóng góp cho engine, bạn có thể muốn sử dụng các tùy chọn SCons ``dev_build=yes`` hoặc ``dev_mode=yes``. Xem :ref:`doc_introduction_to_the_buildsystem_development_and_production_aliases` để biết thêm thông tin.

Nếu mọi việc diễn ra suôn sẻ, tệp thực thi nhị phân thu được sẽ được đặt trong thư mục con ``bin/``. Tệp thực thi này chứa toàn bộ engine và chạy mà không cần bất kỳ phần phụ thuộc nào. Việc thực thi tệp sẽ mở Project Manager.

.. note:: Using a standalone editor executable is not recommended, it should be always packaged into a
          gói ``.app`` để tránh các vấn đề kích hoạt giao diện người dùng.

.. note:: If you want to use separate editor settings for your own Godot builds
          và các bản phát hành chính thức, bạn có thể bật
          :ref:`doc_data_paths_self_contained_mode` by creating a file called
          ``._sc_`` hoặc ``_sc_`` trong thư mục ``bin/``.

Biên dịch với hỗ trợ AccessKit
------------------------------

AccessKit cung cấp hỗ trợ cho trình đọc màn hình.

Việc biên dịch với AccessKit yêu cầu cài đặt thêm các phần phụ thuộc. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``accesskit=no``.

Bạn có thể cài đặt các phần phụ thuộc bắt buộc bằng cách chạy ``python misc/scripts/install_accesskit.py`` trong kho mã nguồn Godot. Sau khi chạy tập lệnh này, hãy biên dịch Godot như bình thường.

.. note:: You can optionally build the godot-accesskit-static libraries yourself with
          các bước sau:

          1. Sao chép thư mục `godot-accesskit-c-static <https://github.com/godotengine/godot-accesskit-c-static/>`_ và đi đến thư mục đó. 2. Chạy lệnh sau:

          ::

              cd accesskit-c
              cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
              cmake --build build
              cmake --install build

          Thư viện tĩnh AccessKit phải được build bằng cùng trình biên dịch mà bạn sử dụng để build Godot.

          Để biên dịch Godot với bản build tùy chỉnh của AccessKit, hãy thêm ``accesskit_sdk_path={path}`` để cho SCons biết nơi tìm các thư viện AccessKit:

          ::

              scons platform=macos accesskit_sdk_path=<...>

Biên dịch với hỗ trợ ANGLE
--------------------------

ANGLE cung cấp một lớp chuyển đổi từ OpenGL ES 3.x sang Metal và có thể được dùng để cải thiện khả năng hỗ trợ trình kết xuất Compatibility trên một số GPU cũ hơn có trình điều khiển OpenGL lỗi thời.

Việc biên dịch với ANGLE yêu cầu cài đặt thêm các phần phụ thuộc. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``angle=no``.

Bạn có thể cài đặt các phần phụ thuộc bắt buộc bằng cách chạy ``python misc/scripts/install_angle.py`` trong kho mã nguồn Godot. Sau khi chạy tập lệnh này, hãy biên dịch Godot như bình thường.

.. note:: You can optionally build the godot-angle-static libraries yourself with
          các bước sau:

          1. Sao chép thư mục `godot-angle-static <https://github.com/godotengine/godot-angle-static>`_ và đi đến thư mục đó. 2. Chạy lệnh sau:

          ::

              git submodule update --init
              ./update_angle.sh
              scons

          Bạn cũng có thể chỉ định kiến trúc build bằng ``arch={architecture}``.

          Thư viện tĩnh ANGLE phải được build bằng cùng trình biên dịch mà bạn sử dụng để build Godot.

          Để biên dịch Godot với bản build tùy chỉnh của ANGLE, hãy thêm ``angle_libs={path}`` để cho SCons biết nơi tìm các thư viện ANGLE:

          ::

              scons platform=macos angle_libs=<...>

Tự động tạo gói ``.app``
~~~~~~~~~~~~~~~~~~~~~~~~

Để tự động tạo gói ``.app`` như trong các bản build chính thức, hãy sử dụng tùy chọn ``generate_bundle=yes`` trong lệnh SCons *cuối cùng* dùng để build trình chỉnh sửa:

::

    scons platform=macos arch=x86_64
    scons platform=macos arch=arm64 generate_bundle=yes

Tạo gói ``.app`` thủ công
~~~~~~~~~~~~~~~~~~~~~~~~~

Để hỗ trợ cả hai kiến trúc trong một tệp nhị phân "Universal 2", hãy chạy hai lệnh ở trên rồi sử dụng ``lipo`` để gộp chúng lại:

::

    lipo -create bin/godot.macos.editor.x86_64 bin/godot.macos.editor.arm64 -output bin/godot.macos.editor.universal

Để tạo gói ``.app``, bạn cần sử dụng mẫu nằm tại ``misc/dist/macos_tools.app``. Thông thường, đối với tệp nhị phân trình chỉnh sửa đã tối ưu được build bằng ``dev_build=yes``:

::

    cp -r misc/dist/macos_tools.app ./bin/Godot.app
    mkdir -p bin/Godot.app/Contents/MacOS
    cp bin/godot.macos.editor.universal bin/Godot.app/Contents/MacOS/Godot
    chmod +x bin/Godot.app/Contents/MacOS/Godot
    codesign --force --timestamp --options=runtime --entitlements misc/dist/macos/editor.entitlements -s - bin/Godot.app

.. note::

    Nếu đang build nhánh ``master``, bạn cũng cần thêm hỗ trợ cho thư viện khả chuyển Vulkan MoltenVK. Theo mặc định, thư viện này sẽ được liên kết tĩnh từ bản cài đặt Vulkan SDK cho macOS. Bạn cũng có thể chọn liên kết động bằng cách truyền ``use_volk=yes`` và đưa thư viện động vào gói ``.app`` của mình:

    ::

        mkdir -p <Godot bundle name>.app/Contents/Frameworks
        cp <Vulkan SDK path>/macOS/lib/libMoltenVK.dylib <Godot bundle name>.app/Contents/Frameworks/libMoltenVK.dylib

Chạy bản build headless/server
------------------------------

Để chạy ở chế độ *headless*, cung cấp chức năng của trình chỉnh sửa nhằm xuất dự án theo cách tự động, hãy sử dụng bản build thông thường:

::

    scons platform=macos target=editor

Sau đó sử dụng đối số dòng lệnh ``--headless``:

::

    ./bin/godot.macos.editor.x86_64 --headless

Để biên dịch bản build *server* debug có thể sử dụng với
:ref:`remote debugging tools <doc_command_line_tutorial>`, use:

::

    scons platform=macos target=template_debug

Để biên dịch bản build *server* release được tối ưu để chạy các máy chủ game chuyên dụng, hãy dùng:

::

    scons platform=macos target=template_release production=yes

Build các mẫu xuất
------------------

Để build các mẫu xuất macOS, bạn phải biên dịch bằng các target không có trình chỉnh sửa: ``target=template_release`` (mẫu release) và ``target=template_debug``.

Các mẫu chính thức là các tệp nhị phân *Universal 2*, hỗ trợ cả kiến trúc ARM64 và Intel x86_64.

- Để hỗ trợ ARM64 (Apple Silicon) + Intel x86_64:

    ::

        scons platform=macos target=template_debug arch=arm64
        scons platform=macos target=template_release arch=arm64
        scons platform=macos target=template_debug arch=x86_64
        scons platform=macos target=template_release arch=x86_64 generate_bundle=yes

- Để chỉ hỗ trợ ARM64 (Apple Silicon) (kích thước tệp nhỏ hơn nhưng kém tương thích hơn với phần cứng cũ):

    ::

        scons platform=macos target=template_debug arch=arm64
        scons platform=macos target=template_release arch=arm64 generate_bundle=yes

Để tạo gói ``.app`` như trong các bản build chính thức, bạn cần sử dụng mẫu nằm tại ``misc/dist/macos_template.app``. Có thể tự động hóa quy trình này bằng cách sử dụng tùy chọn ``generate_bundle=yes`` trong lệnh SCons *cuối cùng* dùng để build các mẫu xuất (để tất cả tệp nhị phân có thể được đưa vào). Thao tác này sẽ tạo tệp ``godot_macos.zip`` trong ``bin/`` và đồng thời đảm nhiệm việc gọi ``lipo`` để tạo một tệp nhị phân *Universal 2* từ hai tệp nhị phân ARM64 và x86_64 riêng biệt (nếu cả hai đã được biên dịch trước đó).

.. note::

    Bạn cũng cần thêm hỗ trợ cho thư viện khả chuyển Vulkan MoltenVK. Theo mặc định, thư viện này sẽ được liên kết tĩnh từ bản cài đặt Vulkan SDK cho macOS. Bạn cũng có thể chọn liên kết động bằng cách truyền ``use_volk=yes`` và đưa thư viện động vào gói ``.app`` của mình:

    ::

        mkdir -p macos_template.app/Contents/Frameworks
        cp <Vulkan SDK path>/macOS/libs/libMoltenVK.dylib macos_template.app/Contents/Frameworks/libMoltenVK.dylib

    Trong hầu hết trường hợp, nên ưu tiên liên kết tĩnh vì việc phân phối sẽ dễ dàng hơn. Ưu điểm chính của liên kết động là cho phép cập nhật MoltenVK mà không cần biên dịch lại các mẫu xuất.

Nếu đã tạo ``.app`` theo cách thủ công, bạn có thể nén thư mục ``macos_template.app`` để tái tạo mẫu ``macos.zip`` từ bản phân phối Godot chính thức:

::

    zip -r9 macos.zip macos_template.app

Để sử dụng các mẫu xuất tùy chỉnh, bạn có thể chọn tệp ``godot_macos.zip`` trong các tùy chọn nâng cao của các cấu hình xuất:

.. image:: img/mactemplates.webp

Ngoài ra, nếu muốn tất cả cấu hình xuất sử dụng mẫu xuất tùy chỉnh, bạn có thể đổi tên tệp ``godot_macos.zip`` thành ``macos.zip`` rồi di chuyển tệp đến vị trí mặc định của các mẫu xuất:

:: ~/Library/Application Support/Godot/export_templates/<GODOT_VERSION>/macos.zip

Biên dịch chéo cho macOS từ Linux
---------------------------------

Có thể biên dịch cho macOS trong môi trường Linux (và có thể cả trên Windows bằng Windows Subsystem for Linux). Để thực hiện việc này, bạn cần cài đặt `OSXCross <https://github.com/tpoechtrager/osxcross>`__ để có thể sử dụng macOS làm target. Trước tiên, hãy làm theo hướng dẫn để cài đặt:

Sao chép `kho OSXCross <https://github.com/tpoechtrager/osxcross>`__ vào một vị trí nào đó trên máy (hoặc tải xuống tệp ZIP rồi giải nén vào một vị trí), ví dụ:

::

    git clone --depth=1 https://github.com/tpoechtrager/osxcross.git "$HOME/osxcross"

1. Làm theo hướng dẫn để đóng gói SDK: https://github.com/tpoechtrager/osxcross#packaging-the-sdk 2. Làm theo hướng dẫn để cài đặt OSXCross: https://github.com/tpoechtrager/osxcross#installation

Sau đó, bạn cần định nghĩa ``OSXCROSS_ROOT`` là đường dẫn đến bản cài đặt OSXCross (cùng vị trí mà bạn đã sao chép kho lưu trữ/giải nén tệp zip), ví dụ:

::

    export OSXCROSS_ROOT="$HOME/osxcross"

Bây giờ bạn có thể biên dịch bằng SCons như bình thường:

::

    scons platform=macos

Nếu bạn có phiên bản SDK OSXCross khác với phiên bản mà hệ thống build SCons mong đợi, bạn có thể chỉ định phiên bản tùy chỉnh bằng đối số ``osxcross_sdk``:

::

    scons platform=macos osxcross_sdk=darwin15

Khắc phục sự cố
---------------

Lỗi nghiêm trọng: không tìm thấy tệp 'cstdint'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu gặp lỗi biên dịch có dạng này ngay từ đầu, nguyên nhân có thể là do cần sửa chữa việc cài đặt các công cụ dòng lệnh Xcode sau khi cập nhật macOS hoặc Xcode:

.. code:: text

    ./core/typedefs.h:45:10: fatal error: 'cstdint' file not found
    45 | #include <cstdint>
       |          ^~~~~~~~~

Chạy hai lệnh này để cài đặt lại các công cụ dòng lệnh Xcode (nhập mật khẩu quản trị viên khi được yêu cầu):

::

    sudo rm -rf /Library/Developer/CommandLineTools
    sudo xcode-select --install

Nếu vẫn không hoạt động, hãy thử cập nhật Xcode từ Mac App Store rồi thử lại.
