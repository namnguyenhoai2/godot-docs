.. _doc_compiling_for_ios:

Biên dịch cho iOS
=================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân của export template iOS từ mã nguồn. Nếu bạn muốn export dự án của mình sang iOS, hãy đọc :ref:`doc_exporting_for_ios`.

Yêu cầu
-------

- `Python 3.9+ <https://www.python.org/downloads/macos/>`_.
- Hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`_.
- `Xcode <https://apps.apple.com/us/app/xcode/id497799835>`_.
    - Khởi chạy Xcode một lần và cài đặt hỗ trợ iOS. Nếu bạn đã khởi chạy Xcode và cần cài đặt hỗ trợ iOS, hãy vào *Xcode -> Settings... -> Platforms*.
    - Vào *Xcode -> Settings... -> Locations -> Command Line Tools* và chọn một phiên bản đã cài đặt. Ngay cả khi đã có một phiên bản được chọn, hãy chọn lại phiên bản đó.
-  Tải xuống và làm theo hướng dẫn trong README để build một ``.xcframework`` static từ `MoltenVK SDK <https://github.com/KhronosGroup/MoltenVK#fetching-moltenvk-source-code>`__.

.. note:: Nếu bạn đã cài đặt `Homebrew <https://brew.sh/>`_, bạn có thể dễ dàng cài đặt SCons bằng lệnh sau:

          ::

              brew install scons

          Việc cài đặt Homebrew cũng sẽ tự động tải Command Line Tools cho Xcode nếu bạn chưa có.

          Tương tự, nếu bạn đã cài đặt `MacPorts <https://www.macports.org/>`_, bạn có thể dễ dàng cài đặt SCons bằng lệnh sau:

          ::

              sudo port install scons

.. seealso:: Để lấy mã nguồn Godot phục vụ việc biên dịch, hãy xem
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Biên dịch
---------

Mở Terminal, đi đến thư mục gốc của mã nguồn engine và nhập lệnh sau để biên dịch bản debug:

::

    scons platform=ios target=template_debug generate_bundle=yes

Để biên dịch bản release:

::

    scons platform=ios target=template_release generate_bundle=yes

Để tạo một dự án Xcode như trong các bản build chính thức, bạn cần sử dụng template nằm tại ``misc/dist/apple_embedded_xcode``. Các thư viện release và debug lần lượt phải được đặt tại ``libgodot.ios.debug.xcframework`` và ``libgodot.ios.release.xcframework``. Các thư viện module Camera phải được đặt tại ``libgodot_camera.ios.debug.xcframework`` và ``libgodot_camera.ios.release.xcframework``. Bạn có thể tự động hóa quy trình này bằng cách sử dụng tùy chọn ``generate_bundle=yes`` trên lệnh SCons *cuối cùng* được dùng để build export template, để tất cả tệp nhị phân đều được đưa vào.

Thư mục ``.xcframework`` static của MoltenVK cũng phải được đặt trong thư mục ``apple_embedded_xcode`` sau khi thư mục này được tạo. MoltenVK luôn được liên kết tĩnh trên iOS; không có tùy chọn liên kết động, không giống như trên macOS.

.. warning::

    Trình mô phỏng iOS chỉ hỗ trợ renderer ``Compatibility``.

    Các máy Mac dùng Apple Silicon có thể chạy ứng dụng iOS nguyên bản, vì vậy bạn có thể chạy trực tiếp các dự án iOS đã export trên máy Mac dùng Apple Silicon mà không bị giới hạn của trình mô phỏng iOS.

Chạy
----

Để chạy trên thiết bị, hãy làm theo hướng dẫn sau:
:ref:`doc_exporting_for_ios`.

Các bản export iOS có thể chạy trực tiếp trên máy Mac dùng Apple Silicon. Để chạy dự án iOS đã export trên Mac, hãy mở dự án đã export trong Xcode và chọn ``My Mac`` trong danh sách thả xuống ``Run Destinations``.

Xử lý sự cố
-----------

Lỗi nghiêm trọng: không tìm thấy tệp 'cstdint'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn gặp lỗi biên dịch dạng này ngay từ đầu, có thể cần sửa lại bản cài đặt công cụ dòng lệnh của Xcode sau khi cập nhật macOS hoặc Xcode:

::

    ./core/typedefs.h:45:10: fatal error: 'cstdint' file not found 45 | #include <cstdint>
       |          ^~~~~~~~~

Chạy hai lệnh này để cài đặt lại công cụ dòng lệnh của Xcode (nhập mật khẩu quản trị viên khi được yêu cầu):

::

    sudo rm -rf /Library/Developer/CommandLineTools sudo xcode-select --install

Nếu vẫn không hoạt động, hãy thử cập nhật Xcode từ Mac App Store rồi thử lại.

.. _`Python 3.9+`: https://www.python.org/downloads/macos/
.. _`SCons 4.4+`: https://scons.org/pages/download.html
.. _`Xcode`: https://apps.apple.com/us/app/xcode/id497799835
.. _`Homebrew`: https://brew.sh/
.. _`MacPorts`: https://www.macports.org/
