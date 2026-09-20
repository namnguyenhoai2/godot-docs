.. _doc_vulkan_validation_layers:

Các lớp xác thực
================

Các lớp xác thực cho phép nhà phát triển kiểm tra việc sử dụng API Vulkan của ứng dụng có chính xác hay không. Có thể bật các lớp xác thực trong cả bản dựng debug và release, bao gồm cả trong các dự án đã xuất.

.. note::

    Việc bật các lớp xác thực ảnh hưởng đến hiệu năng, vì vậy chỉ bật chúng khi bạn thực sự cần đầu ra để gỡ lỗi ứng dụng.

Windows
-------

Cài đặt Vulkan SDK `<https://vulkan.lunarg.com/sdk/home>`__, trong đó các lớp xác thực được bao gồm trong quá trình cài đặt mặc định. Không cần bật bất kỳ tính năng tùy chọn nào trong trình cài đặt; chỉ cần cài đặt Vulkan SDK cốt lõi là đủ. Bạn không cần khởi động lại sau khi cài đặt SDK, nhưng có thể cần đóng rồi mở lại terminal hiện tại.

Sau khi cài đặt Vulkan SDK, chạy Godot với ``--gpu-validation``
:ref:`command line argument <doc_command_line_tutorial>`. You can also specify
``--gpu-abort`` sẽ khiến Godot thoát ngay khi xảy ra lỗi xác thực. Điều này có thể ngăn hệ thống bị treo nếu xảy ra lỗi xác thực.

macOS
-----

.. warning::

    Các bản dựng Godot macOS chính thức **không** hỗ trợ các lớp xác thực, vì chúng được liên kết tĩnh với Vulkan SDK. Thay vào đó, phải sử dụng liên kết động.

    Trên thực tế, điều này có nghĩa là để sử dụng các lớp xác thực trên macOS, bạn **phải** sử dụng bản dựng Godot được biên dịch với tùy chọn SCons ``use_volk=yes``.
    :ref:`doc_compiling_for_macos`. If testing validation layers on an exported
    dự án, bạn phải biên dịch lại mẫu xuất và chỉ định mẫu đó làm mẫu xuất tùy chỉnh trong thiết lập xuất macOS của dự án.

Cài đặt Vulkan SDK `<https://vulkan.lunarg.com/sdk/home>`__, trong đó các lớp xác thực được bao gồm trong quá trình cài đặt mặc định. Không cần bật bất kỳ tính năng tùy chọn nào trong trình cài đặt; chỉ cần cài đặt Vulkan SDK cốt lõi là đủ. Bạn không cần khởi động lại sau khi cài đặt SDK, nhưng có thể cần đóng rồi mở lại terminal hiện tại.

Sau khi cài đặt Vulkan SDK, chạy một tệp nhị phân Godot được biên dịch với tùy chọn SCons ``use_volk=yes``. Chỉ định ``--gpu-validation``
:ref:`command line argument <doc_command_line_tutorial>`.
Bạn cũng có thể chỉ định ``--gpu-abort``, tùy chọn này sẽ khiến Godot thoát ngay khi xảy ra lỗi xác thực. Điều này có thể ngăn hệ thống bị treo nếu xảy ra lỗi xác thực.

Linux, \*BSD
------------

Cài đặt các lớp xác thực Vulkan từ kho lưu trữ của bản phân phối:

.. tabs::

    .. tab:: Alpine Linux

        ::

            vulkan-validation-layers

    .. tab:: Arch Linux

        ::

            pacman -S vulkan-validation-layers

    .. tab:: Debian/Ubuntu

        ::

            apt install vulkan-validationlayers

    .. tab:: Fedora

        ::

            dnf install vulkan-validation-layers

    .. tab:: FreeBSD

        ::

            pkg install graphics/vulkan-validation-layers

    .. tab:: Gentoo

        ::

            emerge -an media-libs/vulkan-layers

    .. tab:: Mageia

        ::

            urpmi vulkan-validation-layers

    .. tab:: OpenBSD

        ::

            pkg_add graphics/vulkan-validation-layers

    .. tab:: openSUSE

        ::

            zypper install vulkan-validationlayers

    .. tab:: Solus

        ::

            eopkg install -c vulkan-validation-layers

Bạn không cần khởi động lại sau khi cài đặt các lớp xác thực, nhưng có thể cần đóng rồi mở lại terminal hiện tại.

Sau khi cài đặt gói, chạy Godot với ``--gpu-validation``
:ref:`command line argument <doc_command_line_tutorial>`. You can also specify
``--gpu-abort`` sẽ khiến Godot thoát ngay khi xảy ra lỗi xác thực. Điều này có thể ngăn hệ thống bị treo nếu xảy ra lỗi xác thực.

iOS
---

Các lớp xác thực hiện **không** được hỗ trợ trên iOS.

Web
---

Các lớp xác thực **không** được hỗ trợ trên nền tảng web, vì nền tảng này không hỗ trợ Vulkan.

.. _doc_vulkan_validation_layers_android:

Android
-------

Sau khi bật các lớp xác thực trên Android, nhà phát triển có thể xem thông báo lỗi và cảnh báo trong đầu ra ``adb logcat``.

Bật các lớp xác thực
~~~~~~~~~~~~~~~~~~~~

Xây dựng các lớp xác thực từ nguồn chính thức
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Để xây dựng các thư viện Android, hãy làm theo hướng dẫn trong `kho lưu trữ của Khronos <https://github.com/KhronosGroup/Vulkan-ValidationLayers/blob/master/BUILD.md#building-on-android>`__. Sau khi xây dựng thành công, các thư viện sẽ nằm tại ``Vulkan-ValidationLayers/build-android/libs``.

Sao chép thư viện
^^^^^^^^^^^^^^^^^

Sao chép các thư viện từ ``Vulkan-ValidationLayers/build-android/libs`` sang ``godot/platform/android/java/app/libs/debug/vulkan_validation_layers``.

Cây thư mục mã nguồn Godot của bạn sẽ có dạng như ví dụ dưới đây:

::

    godot
    |-- platform
        |-- android
            |-- java
                |-- app
                    |-- libs
                        |-- debug
                            |-- vulkan_validation_layers
                                |-- arm64-v8a
                                |-- armeabi-v7a
                                |-- x86
                                |-- x86_64

Nếu thư mục con ``libs/debug/vulkan_validation_layers`` không tồn tại, hãy tạo thư mục đó.

Biên dịch và chạy ứng dụng Android
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các lớp xác thực được liên kết sẽ tự động được tải và bật trong các bản dựng debug của Android. Bạn có thể sử dụng tính năng :ref:`doc_one-click_deploy` của Godot để nhanh chóng kiểm thử dự án với các lớp xác thực đã bật.
