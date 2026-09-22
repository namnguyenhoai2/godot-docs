.. _doc_vulkan_validation_layers:

Các lớp validation
==================

Các lớp validation cho phép developer kiểm tra việc sử dụng Vulkan API đúng cách trong ứng dụng của họ. Có thể bật các lớp validation trong cả bản build debug và release, kể cả trong các project đã export.

.. note::

    Việc bật các lớp validation ảnh hưởng đến hiệu năng, vì vậy chỉ bật chúng khi bạn thực sự cần đầu ra để debug ứng dụng.

Windows
-------

Cài đặt Vulkan SDK ` <https://vulkan.lunarg.com/sdk/home>`__, trong đó các lớp validation được bao gồm trong bản cài đặt mặc định. Bạn không cần bật bất kỳ tính năng tùy chọn nào trong trình cài đặt; chỉ cần cài đặt Vulkan SDK core là đủ. Bạn không cần khởi động lại máy sau khi cài đặt SDK, nhưng có thể cần đóng và mở lại terminal hiện tại.

Sau khi cài đặt Vulkan SDK, hãy chạy Godot với ``--gpu-validation``
:ref:`đối số dòng lệnh <doc_command_line_tutorial>`. Bạn cũng có thể chỉ định ``--gpu-abort``, tùy chọn này sẽ khiến Godot thoát ngay khi xảy ra lỗi validation. Điều này có thể ngăn hệ thống của bạn bị treo nếu xảy ra lỗi validation.

macOS
-----

.. warning::

    Các bản build Godot macOS chính thức **không** hỗ trợ các lớp validation, vì chúng được liên kết tĩnh với Vulkan SDK. Thay vào đó, phải sử dụng liên kết động.

    Trên thực tế, điều này có nghĩa là để sử dụng các lớp validation trên macOS, bạn **phải** sử dụng bản build Godot được biên dịch với tùy chọn SCons ``use_volk=yes``.
    :ref:`doc_compiling_for_macos`. Nếu kiểm thử các lớp validation trên một project đã export, bạn phải biên dịch lại export template và chỉ định template đó làm custom export template trong export preset macOS của project.

Cài đặt Vulkan SDK ` <https://vulkan.lunarg.com/sdk/home>`__, trong đó các lớp validation được bao gồm trong bản cài đặt mặc định. Bạn không cần bật bất kỳ tính năng tùy chọn nào trong trình cài đặt; chỉ cần cài đặt Vulkan SDK core là đủ. Bạn không cần khởi động lại máy sau khi cài đặt SDK, nhưng có thể cần đóng và mở lại terminal hiện tại.

Sau khi cài đặt Vulkan SDK, hãy chạy binary Godot được biên dịch với tùy chọn SCons ``use_volk=yes``. Chỉ định ``--gpu-validation``
:ref:`đối số dòng lệnh <doc_command_line_tutorial>`. Bạn cũng có thể chỉ định ``--gpu-abort``, tùy chọn này sẽ khiến Godot thoát ngay khi xảy ra lỗi validation. Điều này có thể ngăn hệ thống của bạn bị treo nếu xảy ra lỗi validation.

Linux, \*BSD
------------

Cài đặt các lớp validation của Vulkan từ repository của bản phân phối của bạn:

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

Bạn không cần khởi động lại máy sau khi cài đặt các lớp validation, nhưng có thể cần đóng và mở lại terminal hiện tại.

Sau khi cài đặt package, hãy chạy Godot với ``--gpu-validation``
:ref:`đối số dòng lệnh <doc_command_line_tutorial>`. Bạn cũng có thể chỉ định ``--gpu-abort``, tùy chọn này sẽ khiến Godot thoát ngay khi xảy ra lỗi validation. Điều này có thể ngăn hệ thống của bạn bị treo nếu xảy ra lỗi validation.

iOS
---

Các lớp validation hiện **chưa được** hỗ trợ trên iOS.

Web
---

Các lớp validation **không được** hỗ trợ trên nền tảng web, vì nền tảng này không hỗ trợ Vulkan.

.. _doc_vulkan_validation_layers_android:

Android
-------

Sau khi bật các lớp validation trên Android, developer có thể xem các thông báo lỗi và cảnh báo trong ``adb logcat`` output.

Bật các lớp validation
~~~~~~~~~~~~~~~~~~~~~~

Build các lớp validation từ nguồn chính thức
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Để build các thư viện Android, hãy làm theo hướng dẫn trong `repository của Khronos <https://github.com/KhronosGroup/Vulkan-ValidationLayers/blob/master/BUILD.md#building-on-android>`__. Sau khi build thành công, các thư viện sẽ nằm trong ``Vulkan-ValidationLayers/build-android/libs``.

Sao chép các thư viện
^^^^^^^^^^^^^^^^^^^^^

Sao chép các thư viện từ ``Vulkan-ValidationLayers/build-android/libs`` đến ``godot/platform/android/java/app/libs/debug/vulkan_validation_layers``.

Cây thư mục source của Godot sẽ có dạng như ví dụ dưới đây:

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

Nếu subdirectory ``libs/debug/vulkan_validation_layers`` không tồn tại, hãy tạo subdirectory đó.

Biên dịch và chạy ứng dụng Android
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Các lớp validation được liên kết sẽ tự động được tải và bật trong các bản build Android debug. Bạn có thể sử dụng tính năng :ref:`doc_one-click_deploy` của Godot để nhanh chóng kiểm thử project với các lớp validation được bật.
