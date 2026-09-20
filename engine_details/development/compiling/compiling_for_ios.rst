.. _doc_compiling_for_ios:

Biên dịch cho iOS
=================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân mẫu xuất iOS từ mã nguồn. Nếu bạn muốn xuất dự án của mình sang iOS, hãy đọc :ref:`doc_exporting_for_ios`.

Yêu cầu
-------

- `Python 3.9+ <https://www.python.org/downloads/macos/>`_. - Hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`_. - `Xcode <https://apps.apple.com/us/app/xcode/id497799835>`_. - Khởi chạy Xcode một lần và cài đặt hỗ trợ iOS. Nếu bạn đã khởi chạy Xcode và cần cài đặt hỗ trợ iOS, hãy đi đến *Xcode -> Settings... -> Platforms*. - Đi đến *Xcode -> Settings... -> Locations -> Command Line Tools* và chọn một phiên bản đã cài đặt. Ngay cả khi đã có một phiên bản được chọn, hãy chọn lại phiên bản đó. - Tải xuống và làm theo hướng dẫn trong README để build một ``.xcframework`` tĩnh từ `MoltenVK SDK <https://github.com/KhronosGroup/MoltenVK#fetching-moltenvk-source-code>`__.

.. note:: If you have `Homebrew <https://brew.sh/>`_ installed, you can easily
          cài đặt SCons bằng lệnh sau:

          ::

              brew install scons

          Việc cài đặt Homebrew cũng sẽ tự động tải Command Line Tools cho Xcode nếu bạn chưa có.

          Tương tự, nếu bạn đã cài đặt `MacPorts <https://www.macports.org/>`_, bạn có thể dễ dàng cài đặt SCons bằng lệnh sau:

          ::

              sudo port install scons

.. seealso:: To get the Godot source code for compiling, see
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Biên dịch
---------

Mở Terminal, đi đến thư mục gốc của mã nguồn engine và nhập lệnh sau để biên dịch bản build debug:

::

    scons platform=ios target=template_debug generate_bundle=yes

Để biên dịch bản build release:

::

    scons platform=ios target=template_release generate_bundle=yes

Để tạo một dự án Xcode như trong các bản build chính thức, bạn cần sử dụng template nằm tại ``misc/dist/apple_embedded_xcode``. Các thư viện release và debug lần lượt nên được đặt tại ``libgodot.ios.debug.xcframework`` và ``libgodot.ios.release.xcframework``. Các thư viện module Camera nên được đặt tại ``libgodot_camera.ios.debug.xcframework`` và ``libgodot_camera.ios.release.xcframework``. Bạn có thể tự động hóa quy trình này bằng cách sử dụng tùy chọn ``generate_bundle=yes`` trong lệnh SCons *cuối cùng* được dùng để build các template xuất (để có thể đưa tất cả tệp nhị phân vào).

Thư mục ``.xcframework`` tĩnh của MoltenVK cũng phải được đặt trong thư mục ``apple_embedded_xcode`` sau khi thư mục này được tạo. MoltenVK luôn được liên kết tĩnh trên iOS; không có tùy chọn liên kết động, không giống như trên macOS.

.. warning::

    Trình mô phỏng iOS chỉ hỗ trợ trình kết xuất ``Compatibility``.

    Máy Mac Apple Silicon có thể chạy ứng dụng iOS nguyên bản, vì vậy bạn có thể chạy trực tiếp các dự án iOS đã xuất trên máy Mac Apple Silicon mà không bị giới hạn bởi trình mô phỏng iOS.

Chạy
----

Để chạy trên thiết bị, hãy làm theo các hướng dẫn sau:
:ref:`doc_exporting_for_ios`.

Các bản xuất iOS có thể chạy trực tiếp trên máy Mac Apple Silicon. Để chạy dự án iOS đã xuất trên máy Mac, hãy mở dự án đã xuất trong Xcode và chọn ``My Mac`` trong danh sách thả xuống ``Run Destinations``.

Khắc phục sự cố
---------------

Lỗi nghiêm trọng: không tìm thấy tệp 'cstdint'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn gặp lỗi biên dịch dạng này ngay từ đầu, có khả năng là do cần sửa chữa cài đặt các công cụ dòng lệnh của Xcode sau khi cập nhật macOS hoặc Xcode:

::

    ./core/typedefs.h:45:10: fatal error: 'cstdint' file not found
    45 | #include <cstdint>
       |          ^~~~~~~~~

Chạy hai lệnh này để cài đặt lại các công cụ dòng lệnh của Xcode (nhập mật khẩu quản trị viên khi được yêu cầu):

::

    sudo rm -rf /Library/Developer/CommandLineTools
    sudo xcode-select --install

Nếu vẫn không hoạt động, hãy thử cập nhật Xcode từ Mac App Store rồi thử lại.
