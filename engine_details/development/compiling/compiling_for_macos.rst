.. _doc_compiling_for_macos:

Biên dịch cho macOS
===================

.. highlight:: shell

.. note::

    Trang này mô tả cách biên dịch các binary của editor macOS và export template từ mã nguồn. Nếu bạn muốn export project sang macOS, hãy đọc :ref:`doc_exporting_for_macos`.

Yêu cầu
-------

Để biên dịch trên macOS, cần có những thành phần sau:

- `Python 3.9+ <https://www.python.org/downloads/macos/>`_.
- Hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`_.
- `Xcode <https://apps.apple.com/us/app/xcode/id497799835>`_ (hoặc Command Line Tools for Xcode nhẹ hơn).
- `Vulkan SDK <https://sdk.lunarg.com/sdk/download/latest/mac/vulkan-sdk.dmg>`_ cho MoltenVK (macOS không hỗ trợ Vulkan theo mặc định). Có thể nhanh chóng cài đặt phiên bản Vulkan SDK mới nhất bằng cách chạy ``misc/scripts/install_vulkan_sdk_macos.sh`` trong repository mã nguồn Godot.

.. note:: Nếu đã cài đặt `Homebrew <https://brew.sh/>`_, bạn có thể dễ dàng cài đặt SCons bằng lệnh sau:

          ::

              brew install scons

          Việc cài đặt Homebrew cũng sẽ tự động tải Command Line Tools for Xcode nếu bạn chưa có.

          Tương tự, nếu đã cài đặt `MacPorts <https://www.macports.org/>`_, bạn có thể dễ dàng cài đặt SCons bằng lệnh sau:

          ::

              sudo port install scons

.. seealso:: Để lấy mã nguồn Godot phục vụ việc biên dịch, hãy xem
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Biên dịch
---------

Mở terminal, rồi chuyển đến thư mục gốc của mã nguồn engine.

Để biên dịch cho các máy Mac chạy Intel (x86-64), hãy dùng:

::

    scons platform=macos arch=x86_64

Để biên dịch cho các máy Mac chạy Apple Silicon (ARM64), hãy dùng:

::

    scons platform=macos arch=arm64

.. tip::
    Nếu biên dịch Godot để thực hiện thay đổi hoặc đóng góp cho engine, bạn có thể muốn sử dụng các tùy chọn SCons ``dev_build=yes`` hoặc ``dev_mode=yes``. Xem :ref:`doc_introduction_to_the_buildsystem_development_and_production_aliases` để biết thêm thông tin.

Nếu mọi việc diễn ra suôn sẻ, binary executable kết quả sẽ được đặt trong thư mục con ``bin/``. Tệp executable này chứa toàn bộ engine và chạy mà không cần dependency nào. Khi thực thi, tệp sẽ mở Project Manager.

.. note:: Không khuyến nghị sử dụng executable editor độc lập; luôn nên đóng gói nó vào bundle ``.app`` để tránh các vấn đề kích hoạt UI.

.. note:: Nếu muốn sử dụng các thiết lập editor riêng cho bản build Godot của mình và các bản phát hành chính thức, bạn có thể bật
          :ref:`doc_data_paths_self_contained_mode` by creating a file called
          ``._sc_`` hoặc ``_sc_`` trong thư mục ``bin/``.

Biên dịch với hỗ trợ AccessKit
------------------------------

AccessKit cung cấp hỗ trợ cho trình đọc màn hình.

Việc biên dịch với AccessKit yêu cầu cài đặt thêm dependency. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``accesskit=no``.

Bạn có thể cài đặt các dependency bắt buộc bằng cách chạy ``python misc/scripts/install_accesskit.py`` trong repository mã nguồn Godot. Sau khi chạy script này, hãy biên dịch Godot như bình thường.

.. note:: Bạn cũng có thể tự build các thư viện godot-accesskit-static theo các bước sau:

          1. Clone thư mục `godot-accesskit-c-static <https://github.com/godotengine/godot-accesskit-c-static/>`_ rồi chuyển đến thư mục đó.
          2. Chạy lệnh sau:

          ::

              cd accesskit-c cmake -S . -B build -DCMAKE_BUILD_TYPE=Release cmake --build build cmake --install build

          Thư viện tĩnh AccessKit phải được build bằng cùng compiler mà bạn sử dụng để build Godot.

          Để biên dịch Godot với bản build AccessKit tùy chỉnh, thêm ``accesskit_sdk_path={path}`` để cho SCons biết nơi tìm các thư viện AccessKit:

          ::

              scons platform=macos accesskit_sdk_path=<...>

Biên dịch với hỗ trợ ANGLE
--------------------------

ANGLE cung cấp một lớp chuyển đổi từ OpenGL ES 3.x sang Metal và có thể được sử dụng để cải thiện hỗ trợ cho renderer Compatibility trên một số GPU cũ có driver OpenGL lỗi thời.

Việc biên dịch với ANGLE yêu cầu cài đặt thêm dependency. Nếu muốn bỏ qua bước này, bạn có thể sử dụng tùy chọn SCons ``angle=no``.

Bạn có thể cài đặt các dependency bắt buộc bằng cách chạy ``python misc/scripts/install_angle.py`` trong repository mã nguồn Godot. Sau khi chạy script này, hãy biên dịch Godot như bình thường.

.. note:: Bạn cũng có thể tự build các thư viện godot-angle-static theo các bước sau:

          1. Clone thư mục `godot-angle-static <https://github.com/godotengine/godot-angle-static>`_ rồi chuyển đến thư mục đó.
          2. Chạy lệnh sau:

          ::

              git submodule update --init ./update_angle.sh scons

          Bạn cũng có thể chỉ định architecture build bằng ``arch={architecture}``.

          Thư viện tĩnh ANGLE phải được build bằng cùng compiler mà bạn sử dụng để build Godot.

          Để biên dịch Godot với bản build ANGLE tùy chỉnh, thêm ``angle_libs={path}`` để cho SCons biết nơi tìm các thư viện ANGLE:

          ::

              scons platform=macos angle_libs=<...>

Tự động tạo bundle ``.app``
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để tự động tạo bundle ``.app`` như trong các bản build chính thức, hãy sử dụng tùy chọn ``generate_bundle=yes`` trên lệnh SCons *last* được dùng để build editor:

::

    scons platform=macos arch=x86_64 scons platform=macos arch=arm64 generate_bundle=yes

Tạo bundle ``.app`` thủ công
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Để hỗ trợ cả hai architecture trong một binary "Universal 2", hãy chạy hai lệnh trên rồi sử dụng ``lipo`` để gộp chúng lại:

::

    lipo -create bin/godot.macos.editor.x86_64 bin/godot.macos.editor.arm64 -output bin/godot.macos.editor.universal

Để tạo bundle ``.app``, bạn cần sử dụng template nằm trong ``misc/dist/macos_tools.app``. Thông thường, đối với binary editor đã được tối ưu build bằng ``dev_build=yes``:

::

    cp -r misc/dist/macos_tools.app ./bin/Godot.app mkdir -p bin/Godot.app/Contents/MacOS cp bin/godot.macos.editor.universal bin/Godot.app/Contents/MacOS/Godot chmod +x bin/Godot.app/Contents/MacOS/Godot codesign --force --timestamp --options=runtime --entitlements misc/dist/macos/editor.entitlements -s - bin/Godot.app

.. note::

    Nếu bạn đang build nhánh ``master``, bạn cũng cần bao gồm hỗ trợ cho thư viện portability Vulkan MoltenVK. Theo mặc định, thư viện này sẽ được liên kết tĩnh từ bản cài đặt Vulkan SDK for macOS của bạn. Bạn cũng có thể chọn liên kết động bằng cách truyền ``use_volk=yes`` và đưa thư viện động vào bundle ``.app`` của bạn:

    ::

        mkdir -p <Godot bundle name>.app/Contents/Frameworks cp <Vulkan SDK path>/macOS/lib/libMoltenVK.dylib <Godot bundle name>.app/Contents/Frameworks/libMoltenVK.dylib

Chạy bản build headless/server
------------------------------

Để chạy ở chế độ *headless*, cung cấp chức năng editor để export project theo cách tự động, hãy sử dụng bản build thông thường:

::

    scons platform=macos target=editor

Sau đó sử dụng đối số dòng lệnh ``--headless``:

::

    ./bin/godot.macos.editor.x86_64 --headless

Để biên dịch bản build *server* debug có thể được sử dụng với
:ref:`các công cụ remote debugging <doc_command_line_tutorial>`, hãy sử dụng:

::

    scons platform=macos target=template_debug

Để biên dịch bản build *server* release được tối ưu hóa để chạy các dedicated game server, hãy sử dụng:

::

    scons platform=macos target=template_release production=yes

Build export template
---------------------

Để build export template cho macOS, bạn phải biên dịch bằng các target không có editor: ``target=template_release`` (release template) và ``target=template_debug``.

Các template chính thức là các binary *Universal 2*, hỗ trợ cả kiến trúc ARM64 và Intel x86_64.

- Để hỗ trợ ARM64 (Apple Silicon) + Intel x86_64:

    ::

        scons platform=macos target=template_debug arch=arm64 scons platform=macos target=template_release arch=arm64 scons platform=macos target=template_debug arch=x86_64 scons platform=macos target=template_release arch=x86_64 generate_bundle=yes

- Chỉ hỗ trợ ARM64 (Apple Silicon) (kích thước file nhỏ hơn nhưng tương thích kém hơn với phần cứng cũ):

    ::

        scons platform=macos target=template_debug arch=arm64 scons platform=macos target=template_release arch=arm64 generate_bundle=yes

Để tạo một bundle ``.app`` giống như trong các bản build chính thức, bạn cần sử dụng template nằm tại ``misc/dist/macos_template.app``. Có thể tự động hóa quy trình này bằng cách sử dụng tùy chọn ``generate_bundle=yes`` trong lệnh SCons *cuối cùng* được dùng để build export template (để tất cả binary đều được đưa vào). Thao tác này sẽ tạo file ``godot_macos.zip`` tại ``bin/`` và đồng thời gọi ``lipo`` để tạo một binary *Universal 2* từ hai binary ARM64 và x86_64 riêng biệt (nếu cả hai đã được biên dịch trước đó).

.. note::

    Bạn cũng cần bao gồm hỗ trợ cho thư viện portability Vulkan MoltenVK. Theo mặc định, thư viện này sẽ được liên kết tĩnh từ bản cài đặt Vulkan SDK for macOS của bạn. Bạn cũng có thể chọn liên kết động bằng cách truyền ``use_volk=yes`` và đưa thư viện động vào bundle ``.app`` của bạn:

    ::

        mkdir -p macos_template.app/Contents/Frameworks cp <Vulkan SDK path>/macOS/libs/libMoltenVK.dylib macos_template.app/Contents/Frameworks/libMoltenVK.dylib

    Trong hầu hết trường hợp, nên ưu tiên liên kết tĩnh vì việc phân phối sẽ dễ dàng hơn. Ưu điểm chính của liên kết động là cho phép cập nhật MoltenVK mà không cần biên dịch lại export template.

Nếu bạn đã tạo ``.app`` theo cách thủ công, bạn có thể zip thư mục ``macos_template.app`` để tái tạo template ``macos.zip`` từ bản phân phối Godot chính thức:

::

    zip -r9 macos.zip macos_template.app

Để sử dụng export template tùy chỉnh, bạn có thể chọn file ``godot_macos.zip`` trong các tùy chọn nâng cao của export preset:

.. image:: img/mactemplates.webp

Ngoài ra, nếu muốn tất cả preset sử dụng export template tùy chỉnh, bạn có thể đổi tên file ``godot_macos.zip`` thành ``macos.zip`` và di chuyển file đó đến vị trí mặc định dành cho export template:

::
    ~/Library/Application Support/Godot/export_templates/<GODOT_VERSION>/macos.zip

Cross-compile cho macOS từ Linux
--------------------------------

Bạn có thể biên dịch cho macOS trong môi trường Linux (và có thể cả trong Windows bằng Windows Subsystem for Linux). Để làm vậy, bạn cần cài đặt `OSXCross <https://github.com/tpoechtrager/osxcross>`__ để có thể sử dụng macOS làm target. Trước tiên, hãy làm theo hướng dẫn để cài đặt công cụ này:

Clone `repository OSXCross <https://github.com/tpoechtrager/osxcross>`__ vào một vị trí nào đó trên máy (hoặc tải file ZIP xuống và giải nén ở một vị trí nào đó), ví dụ:

::

    git clone --depth=1 https://github.com/tpoechtrager/osxcross.git "$HOME/osxcross"

1. Làm theo hướng dẫn để đóng gói SDK: https://github.com/tpoechtrager/osxcross#packaging-the-sdk
2. Làm theo hướng dẫn để cài đặt OSXCross: https://github.com/tpoechtrager/osxcross#installation

Sau đó, bạn cần định nghĩa ``OSXCROSS_ROOT`` là đường dẫn đến nơi cài đặt OSXCross (cùng vị trí bạn đã clone repository/giải nén file zip), ví dụ:

::

    export OSXCROSS_ROOT="$HOME/osxcross"

Bây giờ bạn có thể biên dịch bằng SCons như bình thường:

::

    scons platform=macos

Nếu bạn có phiên bản SDK OSXCross khác với phiên bản mà SCons buildsystem mong đợi, bạn có thể chỉ định phiên bản tùy chỉnh bằng đối số ``osxcross_sdk``:

::

    scons platform=macos osxcross_sdk=darwin15

Khắc phục sự cố
---------------

Lỗi nghiêm trọng: không tìm thấy file 'cstdint'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn gặp lỗi biên dịch dạng này ngay từ đầu, nguyên nhân có thể là do cần sửa chữa cài đặt Xcode command line tools sau khi macOS hoặc Xcode được cập nhật:

.. code:: text

    ./core/typedefs.h:45:10: fatal error: 'cstdint' file not found
    45 | #include <cstdint>
       |          ^~~~~~~~~

Chạy hai lệnh này để cài đặt lại Xcode command line tools (nhập mật khẩu quản trị viên khi được yêu cầu):

::

    sudo rm -rf /Library/Developer/CommandLineTools sudo xcode-select --install

Nếu vẫn không hoạt động, hãy thử cập nhật Xcode từ Mac App Store rồi thử lại.

.. _`Python 3.9+`: https://www.python.org/downloads/macos/
.. _`SCons 4.4+`: https://scons.org/pages/download.html
.. _`Xcode`: https://apps.apple.com/us/app/xcode/id497799835
.. _`Vulkan SDK`: https://sdk.lunarg.com/sdk/download/latest/mac/vulkan-sdk.dmg
.. _`Homebrew`: https://brew.sh/
.. _`MacPorts`: https://www.macports.org/
.. _`godot-accesskit-c-static`: https://github.com/godotengine/godot-accesskit-c-static/
.. _`godot-angle-static`: https://github.com/godotengine/godot-angle-static
