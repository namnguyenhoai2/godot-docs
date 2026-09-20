.. _doc_compiling_for_android:

Biên dịch cho Android
=====================

.. highlight:: shell

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân mẫu xuất Android từ mã nguồn. Nếu bạn muốn xuất dự án của mình sang Android, hãy đọc :ref:`doc_exporting_for_android`.

Lưu ý
-----

Trong hầu hết trường hợp, sử dụng trình triển khai tích hợp sẵn và các mẫu xuất là đủ tốt. Việc biên dịch APK Android thủ công chủ yếu hữu ích cho các bản dựng tùy chỉnh hoặc các gói tùy chỉnh dành cho trình triển khai.

Ngoài ra, bạn vẫn cần làm theo các bước được đề cập trong
:ref:`doc_exporting_for_android` tutorial before attempting to build
mẫu xuất tùy chỉnh.

Yêu cầu
-------

Để biên dịch trên Windows, Linux hoặc macOS, cần có những thành phần sau:

- `Python 3.9+ <https://www.python.org/downloads/>`_. - hệ thống dựng `SCons 4.4+ <https://scons.org/pages/download.html>`_. - Android SDK

   - Để cài đặt Android SDK, hãy làm theo các bước `tại đây <https://docs.godotengine.org/en/stable/tutorials/export/exporting_for_android.html>`_. - Trên Linux, **không sử dụng Android SDK do kho của bản phân phối cung cấp** vì SDK này thường đã lỗi thời. - Trên macOS, **không sử dụng Android SDK do Homebrew cung cấp** vì SDK sẽ không được cài đặt tại một vị trí thống nhất.

- Gradle (sẽ được tự động tải xuống và cài đặt nếu chưa có). - JDK 17 (OpenJDK hoặc Oracle JDK).

   - Bạn có thể tải xuống một bản dựng từ `Adoptium <https://adoptium.net/temurin/releases?variant=openjdk17&version=17&os=any&arch=any>`_.

.. seealso:: To get the Godot source code for compiling, see
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

.. _doc_android_setting_up_the_buildsystem:

Thiết lập hệ thống dựng
-----------------------

-  Đặt biến môi trường ``ANDROID_HOME`` trỏ đến Android SDK. Nếu bạn đã tải xuống các công cụ dòng lệnh Android, đây sẽ là thư mục nơi bạn đã giải nén nội dung của tệp lưu trữ ZIP.

    -  Windows: Nhấn :kbd:`Windows + R`, nhập "control system", sau đó nhấp vào **Advanced system settings** trong ngăn bên trái, rồi nhấp vào **Environment variables** trong cửa sổ xuất hiện.

    -  Linux hoặc macOS: Thêm văn bản ``export ANDROID_HOME="/path/to/android-sdk"`` vào ``.bashrc`` hoặc ``.zshrc`` của bạn, trong đó ``/path/to/android-sdk`` trỏ đến thư mục gốc của các thư mục SDK.

-  Sau khi thiết lập SDK và các biến môi trường, hãy nhớ **khởi động lại terminal** để áp dụng các thay đổi. Nếu bạn đang sử dụng IDE có terminal tích hợp, bạn cần khởi động lại IDE.

-  Chạy ``scons platform=android``. Nếu lệnh này không thành công, hãy quay lại và kiểm tra các bước. Nếu bạn đã hoàn tất thiết lập đúng cách, NDK sẽ bắt đầu được tải xuống. Nếu bạn đang cố biên dịch GDExtension, trước tiên bạn cần biên dịch engine để tải xuống NDK, sau đó mới có thể biên dịch GDExtension.

Xây dựng các mẫu xuất
---------------------

Godot cần ba mẫu xuất cho Android: mẫu "release" được tối ưu hóa (``android_release.apk``), mẫu debug (``android_debug.apk``) và mẫu dựng Gradle (``android_source.zip``). Vì Google yêu cầu tất cả APK phải bao gồm các thư viện ARMv8 (64-bit) kể từ tháng 8 năm 2019, các lệnh dưới đây sẽ xây dựng các mẫu chứa cả thư viện ARMv7 và ARMv8.

Việc biên dịch các mẫu xuất tiêu chuẩn được thực hiện bằng cách gọi SCons từ thư mục gốc của Godot với các đối số sau:

-  Mẫu Release (được sử dụng khi xuất với **Debugging Enabled** không được chọn)

::

    scons platform=android target=template_release arch=arm32
    scons platform=android target=template_release arch=arm64 generate_android_binaries=yes

-  Mẫu Debug (được sử dụng khi xuất với **Debugging Enabled** được chọn)

::

    scons platform=android target=template_debug arch=arm32
    scons platform=android target=template_debug arch=arm64 generate_android_binaries=yes

Các mẫu kết quả sẽ nằm trong thư mục ``bin``:

- ``bin/android_release.apk`` cho mẫu release - ``bin/android_debug.apk`` cho mẫu debug - ``bin/android_source.zip`` cho mẫu dựng Gradle

.. note::

   - Nếu bạn thay đổi danh sách các kiến trúc đang xây dựng, hãy nhớ thêm ``generate_android_binaries=yes`` vào kiến trúc *cuối cùng* mà bạn xây dựng, để các tệp mẫu được tạo sau khi quá trình xây dựng hoàn tất.

   - Để bật bản dựng dev (dùng khi khắc phục sự cố) trong các mẫu được tạo, hãy thêm các tham số ``dev_build=yes`` vào lệnh SCons.

   - Để đưa các ký hiệu debug vào các mẫu được tạo, hãy thêm các tham số ``debug_symbols=yes`` vào lệnh SCons.

       - Lưu ý rằng bạn có thể thêm ``separate_debug_symbols=yes`` để tạo các ký hiệu debug trong một tệp ``*-native-debug-symbols.zip`` riêng.

.. seealso::

    Nếu muốn bật các lớp xác thực Vulkan, hãy xem
    :ref:`Vulkan validation layers on Android <doc_vulkan_validation_layers_android>`.

Thêm hỗ trợ cho thiết bị x86
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu cũng muốn bao gồm hỗ trợ cho các thiết bị x86 và x86_64, hãy chạy lệnh SCons lần thứ ba và thứ tư với các đối số ``arch=x86_32`` và ``arch=x86_64`` trước khi xây dựng APK bằng Gradle. Ví dụ, đối với mẫu release:

::

    scons platform=android target=template_release arch=arm32
    scons platform=android target=template_release arch=arm64
    scons platform=android target=template_release arch=x86_32
    scons platform=android target=template_release arch=x86_64 generate_android_binaries=yes

Thao tác này sẽ tạo các tệp nhị phân mẫu hoạt động trên tất cả các nền tảng. Kích thước tệp nhị phân cuối cùng của các dự án đã xuất sẽ phụ thuộc vào những nền tảng bạn chọn hỗ trợ khi xuất; nói cách khác, các nền tảng không được sử dụng sẽ bị loại bỏ khỏi tệp nhị phân.

Dọn dẹp các mẫu xuất đã tạo
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Bạn có thể sử dụng các lệnh sau để xóa các mẫu xuất đã tạo:

::

    cd platform/android/java
    # On Windows
    .\gradlew clean
    # On Linux and macOS
    ./gradlew clean


Sử dụng các mẫu xuất
--------------------

Godot cần các tệp nhị phân release và debug được biên dịch dựa trên cùng phiên bản/commit với trình chỉnh sửa. Nếu bạn đang sử dụng các tệp nhị phân chính thức cho trình chỉnh sửa, hãy đảm bảo cài đặt các mẫu xuất tương ứng hoặc tự xây dựng chúng từ cùng phiên bản.

Khi xuất trò chơi, Godot sử dụng các mẫu làm nền tảng và cập nhật nội dung của chúng khi cần.

Cài đặt các mẫu
~~~~~~~~~~~~~~~

Các mẫu mới biên dịch (``android_debug.apk``, ``android_release.apk`` và ``android_source.zip``) phải được sao chép vào thư mục mẫu của Godot với tên tương ứng. Thư mục mẫu có thể nằm tại:

-  Windows: ``%APPDATA%\Godot\export_templates\<version>\`` - Linux: ``$HOME/.local/share/godot/export_templates/<version>/`` - macOS: ``$HOME/Library/Application Support/Godot/export_templates/<version>/``

``<version>`` có dạng ``major.minor[.patch].status`` và sử dụng các giá trị từ ``version.py`` trong kho mã nguồn Godot của bạn (ví dụ: ``4.1.3.stable`` hoặc ``4.2.dev``). Bạn cũng cần ghi chuỗi phiên bản này vào tệp ``version.txt`` nằm cạnh các mẫu xuất.

.. TODO: Di chuyển các đường dẫn này đến một trang tham chiếu chung

Tuy nhiên, nếu bạn đang viết các mô-đun tùy chỉnh hoặc mã C++ tùy chỉnh, thay vào đó bạn có thể muốn cấu hình các tệp nhị phân mẫu của mình thành các mẫu xuất tùy chỉnh trong menu xuất dự án. Bạn phải bật **Advanced Options** để thiết lập tùy chọn này.

.. image:: img/andtemplates.webp

Bạn thậm chí không cần sao chép chúng; chỉ cần tham chiếu đến tệp kết quả trong thư mục ``bin\`` của thư mục mã nguồn Godot, để lần tiếp theo bạn xây dựng, các mẫu tùy chỉnh sẽ tự động được tham chiếu.

Xây dựng trình chỉnh sửa Godot
------------------------------

Việc biên dịch trình chỉnh sửa được thực hiện bằng cách gọi SCons từ thư mục gốc của Godot với các đối số sau:

::

   scons platform=android arch=arm32 production=yes target=editor
   scons platform=android arch=arm64 production=yes target=editor
   scons platform=android arch=x86_32 production=yes target=editor
   scons platform=android arch=x86_64 production=yes target=editor generate_android_binaries=yes

- Bạn có thể thêm tham số ``dev_build=yes`` để tạo bản dựng dev của trình chỉnh sửa Godot.

- Bạn có thể thêm các tham số ``debug_symbols=yes`` để đưa các ký hiệu debug vào bản dựng được tạo.

    - Lưu ý rằng bạn có thể thêm ``separate_debug_symbols=yes`` vào kiến trúc *cuối cùng* đang xây dựng để tạo các ký hiệu debug trong một tệp ``*-native-debug-symbols.zip`` riêng.

- Bạn có thể bỏ qua một số kiến trúc nhất định tùy thuộc vào thiết bị đích để tăng tốc quá trình biên dịch.

Hãy nhớ thêm ``generate_android_binaries=yes`` vào kiến trúc *cuối cùng* đang xây dựng để các tệp nhị phân được tạo sau khi quá trình xây dựng hoàn tất.

Các tệp nhị phân kết quả sẽ nằm trong ``bin/android_editor_builds/``.

Xóa các tệp nhị phân của trình chỉnh sửa
----------------------------------------

Bạn có thể sử dụng các lệnh sau để xóa các tệp nhị phân của trình chỉnh sửa đã tạo:

::

    cd platform/android/java
    # On Windows
   .\gradlew clean
   # On Linux and macOS
   ./gradlew clean

Cài đặt APK trình chỉnh sửa Godot
---------------------------------

Khi đã bật Developer Options trên thiết bị Android, hãy kết nối thiết bị Android với máy tính bằng cáp sạc của thiết bị qua cổng USB/USB-C. Mở Terminal/Command Prompt và chạy các lệnh sau từ thư mục gốc với các đối số sau:

::

   adb install ./bin/android_editor_builds/android_editor-android-debug.apk

Khắc phục sự cố
---------------

Nền tảng không xuất hiện trong SCons
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Kiểm tra lại để đảm bảo bạn đã đặt biến môi trường ``ANDROID_HOME``. Đây là yêu cầu để nền tảng xuất hiện trong danh sách các nền tảng được SCons phát hiện. Xem :ref:`Setting up the buildsystem <doc_android_setting_up_the_buildsystem>` để biết thêm thông tin.

Ứng dụng không được cài đặt
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Android có thể báo rằng ứng dụng chưa được cài đặt chính xác. Nếu vậy:

-  Kiểm tra xem debug keystore đã được tạo đúng cách chưa. - Kiểm tra xem tệp thực thi jarsigner có phải đến từ JDK 8 hay không.

Nếu vẫn không thành công, hãy mở dòng lệnh và chạy `logcat <https://developer.android.com/studio/command-line/logcat>`_:

::

    adb logcat

Sau đó kiểm tra đầu ra trong khi ứng dụng được cài đặt; thông báo lỗi sẽ xuất hiện ở đó. Hãy tìm sự trợ giúp nếu bạn không thể xác định nguyên nhân.

Ứng dụng thoát ngay lập tức
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu ứng dụng chạy nhưng thoát ngay lập tức, nguyên nhân có thể là một trong những lý do sau:

-  Đảm bảo sử dụng các mẫu xuất khớp với phiên bản trình chỉnh sửa; nếu sử dụng phiên bản Godot mới, bạn *phải* cập nhật cả các mẫu. - ``libgodot_android.so`` không nằm trong ``libs/<arch>/``, trong đó ``<arch>`` là kiến trúc của thiết bị. - Kiến trúc của thiết bị không khớp với kiến trúc đã xuất. Hãy đảm bảo các mẫu được xây dựng cho kiến trúc của thiết bị đó và cài đặt xuất đã bao gồm hỗ trợ cho kiến trúc đó.

Trong mọi trường hợp, ``adb logcat`` cũng sẽ hiển thị nguyên nhân của lỗi.
