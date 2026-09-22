.. _doc_compiling_for_android:

Biên dịch cho Android
=====================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các binary export template Android từ mã nguồn. Nếu bạn muốn export dự án sang Android, hãy đọc :ref:`doc_exporting_for_android`.

Lưu ý
-----

Trong hầu hết trường hợp, sử dụng deployer tích hợp sẵn và các export template là đủ. Việc biên dịch APK Android thủ công chủ yếu hữu ích cho các bản build tùy chỉnh hoặc các package tùy chỉnh cho deployer.

Ngoài ra, bạn vẫn cần làm theo các bước được đề cập trong
:ref:`doc_exporting_for_android` tutorial trước khi thử build một export template tùy chỉnh.

Yêu cầu
-------

Để biên dịch trên Windows, Linux hoặc macOS, cần có những thành phần sau:

- `Python 3.9+ <https://www.python.org/downloads/>`_.
- `Hệ thống build <https://scons.org/pages/download.html>`_ SCons 4.4+.
- Android SDK

   - Để cài đặt Android SDK, hãy làm theo các bước `tại đây <https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html>`_.
   - Trên Linux, **không sử dụng Android SDK do repository của bản phân phối cung cấp**, vì SDK này thường đã lỗi thời.
   - Trên macOS, **không sử dụng Android SDK do Homebrew cung cấp**, vì SDK sẽ không được cài đặt tại một vị trí thống nhất.

- Gradle (sẽ được tự động tải xuống và cài đặt nếu chưa có).
- JDK 17 (OpenJDK hoặc Oracle JDK).

   - Bạn có thể tải một bản build từ `Adoptium <https://adoptium.net/temurin/releases?variant=openjdk17&version=17&os=any&arch=any>`_.

.. seealso:: Để lấy mã nguồn Godot phục vụ việc biên dịch, hãy xem
             :ref:`doc_getting_source`.

             Để biết tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

.. _doc_android_setting_up_the_buildsystem:

Thiết lập hệ thống build
------------------------

-  Đặt biến môi trường ``ANDROID_HOME`` trỏ đến Android SDK. Nếu bạn đã tải xuống các command-line tools của Android, đây sẽ là thư mục mà bạn đã giải nén nội dung của tệp ZIP.

    -  Windows: Nhấn :kbd:`Windows + R`, nhập "control system", sau đó nhấp vào **Advanced system settings** trong ngăn bên trái, rồi nhấp vào **Environment variables** trong cửa sổ xuất hiện.

    -  Linux hoặc macOS: Thêm nội dung ``export ANDROID_HOME="/path/to/android-sdk"`` vào ``.bashrc`` hoặc ``.zshrc`` của bạn, trong đó ``/path/to/android-sdk`` trỏ đến thư mục gốc của các thư mục SDK.

-  Sau khi thiết lập SDK và các biến môi trường, hãy **khởi động lại terminal** để áp dụng thay đổi. Nếu bạn đang sử dụng IDE có terminal tích hợp, cần khởi động lại IDE.

-  Chạy ``scons platform=android``. Nếu lệnh này không thành công, hãy quay lại và kiểm tra các bước. Nếu bạn đã hoàn tất thiết lập đúng cách, NDK sẽ bắt đầu được tải xuống. Nếu bạn đang cố biên dịch GDExtension, trước tiên cần biên dịch engine để tải xuống NDK, sau đó bạn có thể biên dịch GDExtension.

Build các export template
-------------------------

Godot cần ba export template cho Android: template "release" được tối ưu hóa (``android_release.apk``), template debug (``android_debug.apk``) và template Gradle build (``android_source.zip``). Vì Google yêu cầu tất cả APK phải bao gồm các thư viện ARMv8 (64-bit) kể từ tháng 8 năm 2019, các lệnh dưới đây sẽ build các template chứa cả thư viện ARMv7 và ARMv8.

Biên dịch các export template tiêu chuẩn được thực hiện bằng cách gọi SCons từ thư mục gốc của Godot với các đối số sau:

-  Template release (được sử dụng khi export với **Debugging Enabled** không được chọn)

::

    scons platform=android target=template_release arch=arm32 scons platform=android target=template_release arch=arm64 generate_android_binaries=yes

-  Template debug (được sử dụng khi export với **Debugging Enabled** được chọn)

::

    scons platform=android target=template_debug arch=arm32 scons platform=android target=template_debug arch=arm64 generate_android_binaries=yes

Các template tạo ra sẽ nằm trong thư mục ``bin``:

- ``bin/android_release.apk`` cho template release
- ``bin/android_debug.apk`` cho template debug
- ``bin/android_source.zip`` cho template Gradle build

.. note::

   - Nếu bạn thay đổi danh sách các kiến trúc đang build, hãy nhớ thêm ``generate_android_binaries=yes`` vào kiến trúc *cuối cùng* đang build để các tệp template được tạo sau khi build.

   - Để bật dev build (dùng khi khắc phục sự cố) trong các template được tạo, hãy thêm các tham số ``dev_build=yes`` vào lệnh SCons.

   - Để đưa debug symbol vào các template được tạo, hãy thêm các tham số ``debug_symbols=yes`` vào lệnh SCons.

       - Lưu ý rằng bạn có thể thêm ``separate_debug_symbols=yes`` để tạo debug symbol trong một tệp ``*-native-debug-symbols.zip`` riêng.

.. seealso::

    Nếu bạn muốn bật các lớp xác thực Vulkan, hãy xem
    :ref:`các lớp xác thực Vulkan trên Android <doc_vulkan_validation_layers_android>`.

Thêm hỗ trợ cho thiết bị x86
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn cũng muốn thêm hỗ trợ cho các thiết bị x86 và x86_64, hãy chạy lệnh SCons lần thứ ba và thứ tư với các đối số ``arch=x86_32`` và ``arch=x86_64`` trước khi build APK bằng Gradle. Ví dụ, đối với template release:

::

    scons platform=android target=template_release arch=arm32 scons platform=android target=template_release arch=arm64 scons platform=android target=template_release arch=x86_32 scons platform=android target=template_release arch=x86_64 generate_android_binaries=yes

Thao tác này sẽ tạo các binary template hoạt động trên tất cả nền tảng. Kích thước binary cuối cùng của các dự án được export sẽ phụ thuộc vào những nền tảng bạn chọn hỗ trợ khi export; nói cách khác, các nền tảng không được sử dụng sẽ bị xóa khỏi binary.

Xóa các export template đã tạo
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể sử dụng các lệnh sau để xóa các export template đã tạo:

::

    cd platform/android/java # Trên Windows .\gradlew clean # Trên Linux và macOS ./gradlew clean


Sử dụng các export template
---------------------------

Godot cần các binary release và debug được biên dịch từ cùng phiên bản/commit với editor. Nếu bạn đang sử dụng binary chính thức cho editor, hãy đảm bảo cài đặt các export template tương ứng hoặc tự build chúng từ cùng phiên bản đó.

Khi xuất game, Godot sử dụng các template làm cơ sở và cập nhật nội dung của chúng khi cần.

Cài đặt các template
~~~~~~~~~~~~~~~~~~~~

Các template mới biên dịch (``android_debug.apk`` , ``android_release.apk`` và ``android_source.zip``) phải được sao chép vào thư mục template của Godot với đúng tên tương ứng. Thư mục template có thể nằm tại:

-  Windows: ``%APPDATA%\Godot\export_templates\<version>\``
-  Linux: ``$HOME/.local/share/godot/export_templates/<version>/``
-  macOS: ``$HOME/Library/Application Support/Godot/export_templates/<version>/``

``<version>`` có dạng ``major.minor[.patch].status`` với các giá trị lấy từ ``version.py`` trong repository mã nguồn Godot của bạn (ví dụ: ``4.1.3.stable`` hoặc ``4.2.dev``). Bạn cũng cần ghi chuỗi phiên bản này vào tệp ``version.txt`` nằm cạnh các template xuất của bạn.

.. TODO: Move these paths to a common reference page

Tuy nhiên, nếu bạn đang viết các module tùy chỉnh hoặc mã C++ tùy chỉnh, thay vào đó bạn có thể muốn cấu hình các binary template của mình thành template xuất tùy chỉnh trong menu xuất của project. Bạn phải bật **Advanced Options** để thực hiện việc này.

.. image:: img/andtemplates.webp

Bạn thậm chí không cần sao chép chúng; chỉ cần tham chiếu đến tệp kết quả trong thư mục ``bin\`` của thư mục mã nguồn Godot, để lần build tiếp theo tự động tham chiếu đến các template tùy chỉnh.

Build trình chỉnh sửa Godot
---------------------------

Biên dịch trình chỉnh sửa được thực hiện bằng cách gọi SCons từ thư mục gốc Godot với các đối số sau:

::

   scons platform=android arch=arm32 production=yes target=editor scons platform=android arch=arm64 production=yes target=editor scons platform=android arch=x86_32 production=yes target=editor scons platform=android arch=x86_64 production=yes target=editor generate_android_binaries=yes

- Bạn có thể thêm tham số ``dev_build=yes`` để tạo bản build dev của trình chỉnh sửa Godot.

- Bạn có thể thêm các tham số ``debug_symbols=yes`` để đưa các symbol debug vào bản build được tạo.

    - Lưu ý rằng bạn có thể thêm ``separate_debug_symbols=yes`` vào kiến trúc *last* mà bạn đang build để tạo các symbol debug trong một tệp ``*-native-debug-symbols.zip`` riêng.

- Bạn có thể bỏ qua một số kiến trúc tùy theo thiết bị đích để tăng tốc quá trình biên dịch.

Hãy nhớ thêm ``generate_android_binaries=yes`` vào kiến trúc *last* mà bạn đang build để các binary được tạo sau khi build.

Các binary kết quả sẽ nằm trong ``bin/android_editor_builds/``.

Xóa các binary của trình chỉnh sửa
----------------------------------

Bạn có thể sử dụng các lệnh sau để xóa các binary của trình chỉnh sửa đã tạo:

::

    cd platform/android/java # Trên Windows
   .\gradlew clean # Trên Linux và macOS ./gradlew clean

Cài đặt APK của trình chỉnh sửa Godot
-------------------------------------

Khi đã bật Developer Options trên thiết bị Android, hãy kết nối thiết bị Android với máy tính bằng cáp sạc qua cổng USB/USB-C. Mở Terminal/Command Prompt và chạy các lệnh sau từ thư mục gốc với các đối số sau:

::

   adb install ./bin/android_editor_builds/android_editor-android-debug.apk

Xử lý sự cố
-----------

Nền tảng không xuất hiện trong SCons
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kiểm tra lại để chắc chắn rằng bạn đã thiết lập biến môi trường ``ANDROID_HOME``. Biến này là bắt buộc để nền tảng xuất hiện trong danh sách các nền tảng được SCons phát hiện. Xem :ref:`Setting up the buildsystem <doc_android_setting_up_the_buildsystem>` để biết thêm thông tin.

Ứng dụng chưa được cài đặt
~~~~~~~~~~~~~~~~~~~~~~~~~~

Android có thể báo rằng ứng dụng chưa được cài đặt đúng cách. Nếu vậy:

-  Kiểm tra để chắc chắn rằng debug keystore đã được tạo đúng cách.
-  Kiểm tra để chắc chắn rằng tệp thực thi jarsigner đến từ JDK 8.

Nếu vẫn không thành công, hãy mở dòng lệnh và chạy `logcat <https://developer.android.com/studio/command-line/logcat>`_:

::

    adb logcat

Sau đó kiểm tra đầu ra trong khi ứng dụng được cài đặt; thông báo lỗi sẽ xuất hiện ở đó. Hãy tìm trợ giúp nếu bạn không thể xác định nguyên nhân.

Ứng dụng thoát ngay lập tức
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu ứng dụng chạy nhưng thoát ngay lập tức, nguyên nhân có thể là một trong những lý do sau:

-  Đảm bảo sử dụng các template xuất khớp với phiên bản trình chỉnh sửa của bạn; nếu sử dụng phiên bản Godot mới, bạn *have* cập nhật cả các template.
-  ``libgodot_android.so`` không nằm trong ``libs/<arch>/``, trong đó ``<arch>`` là kiến trúc của thiết bị.
-  Kiến trúc của thiết bị không khớp với kiến trúc đã xuất. Hãy đảm bảo các template của bạn được build cho kiến trúc của thiết bị đó và phần cài đặt xuất đã bao gồm hỗ trợ cho kiến trúc đó.

Trong mọi trường hợp, ``adb logcat`` cũng sẽ hiển thị nguyên nhân của lỗi.

.. _`Python 3.9+`: https://www.python.org/downloads/
.. _`SCons 4.4+`: https://scons.org/pages/download.html
.. _`here`: https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html
.. _`Adoptium`: https://adoptium.net/temurin/releases?variant=openjdk17&version=17&os=any&arch=any
.. _`logcat`: https://developer.android.com/studio/command-line/logcat
