.. _doc_resolving_crashes_on_android:

Khắc phục lỗi crash trên Android
================================

Khi game của bạn bị crash trên Android, bạn thường thấy stack trace bị làm rối trong Play Console hoặc các công cụ báo cáo crash khác như Firebase Crashlytics. Để làm cho các stack trace này dễ đọc (symbolicate), bạn cần các native debug symbols tương ứng với build đã export của game.

Godot hiện cung cấp native debug symbols có thể tải xuống cho từng export template chính thức.

Lấy Native debug symbols cho các template chính thức
----------------------------------------------------

Các file native debug symbols được cung cấp cho mọi bản phát hành Godot ổn định và có thể tải xuống từ `GitHub release page <https://github.com/godotengine/godot/releases/>`_.

Ví dụ, để lấy native debug symbols cho phiên bản ``4.5.1.stable``:

- Truy cập `4.5.1.stable release page <https://github.com/godotengine/godot/releases/>`_ - Tải artifact phát hành ``Godot_native_debug_symbols.4.5.1.stable.template_release.android.zip``

Lấy Native debug symbols cho các build tùy chỉnh
------------------------------------------------

Export template và native debug symbols của bạn phải đến từ **cùng một build**, vì vậy bạn chỉ có thể sử dụng symbols chính thức nếu đang dùng **export template chính thức**. Nếu đang build **export template tùy chỉnh**, bạn cần tự tạo các file symbol tương ứng.

Để thực hiện việc này, thêm ``debug_symbols=yes separate_debug_symbols=yes`` vào lệnh build scons của bạn. Thao tác này sẽ tạo một file có tên ``android-template-release-native-symbols.zip`` chứa native debug symbols cho build tùy chỉnh của bạn.

Ví dụ,

::

    scons platform=android target=template_release debug_symbols=yes separate_debug_symbols=yes generate_android_binaries=yes

Nếu đang build cho nhiều architecture, bạn chỉ nên thêm ``separate_debug_symbols=yes`` vào lệnh build cuối cùng, tương tự như cách sử dụng ``generate_android_binaries=yes``.

::

    scons platform=android arch=arm32 target=template_release debug_symbols=yes
    scons platform=android arch=arm64 target=template_release debug_symbols=yes
    scons platform=android arch=x86_32 target=template_release debug_symbols=yes
    scons platform=android arch=x86_64 target=template_release debug_symbols=yes separate_debug_symbols=yes generate_android_binaries=yes

Upload Symbols lên Google Play Console
--------------------------------------

Hãy làm theo các bước sau để upload native debug symbols:

1. Mở `Play Console <https://play.google.com/console>`_. 2. Chọn một app bất kỳ. 3. Trong menu bên trái, đi tới ``Test and release > Latest releases and bundles``.

.. image:: img/play_console_latest_release_bundles.webp

4. Bây giờ hãy chọn bundle tương ứng và mở nó.

.. image:: img/play_console_latest_release_bundles2.webp

5. Chọn tab ``Downloads`` và cuộn xuống phần ``Assets``.

.. image:: img/play_console_app_bundle_explorer.webp

6. Bên cạnh ``Native debug symbols``, hãy nhấp vào biểu tượng mũi tên upload.

.. image:: img/play_console_app_bundle_explorer2.webp

7. Chọn và upload file native debug symbols tương ứng với phiên bản build đó.

.. image:: img/play_console_upload_native_debug_symbols.webp

Ngoài ra, bạn có thể upload symbols khi tạo bản phát hành mới:

1. Trên trang Create release, tìm bundle của bản phát hành mới.

.. image:: img/play_console_create_new_release.webp

2. Nhấp vào menu ba chấm bên cạnh bundle đó. 3. Chọn ``Upload native debug symbols (.zip)`` từ menu.

.. image:: img/play_console_create_new_release2.webp

4. Chọn và upload file native debug symbols tương ứng với phiên bản build đó.

Symbolicate Crash Logs thủ công
-------------------------------

Bạn cũng có thể symbolicate crash logs thủ công bằng công cụ `ndk-stack <https://developer.android.com/ndk/guides/ndk-stack>`_ đi kèm Android NDK.

.. note::

    Nếu Android SDK đã được cài đặt, bạn có thể tìm công cụ ``ndk-stack`` trong thư mục ``ndk`` tại vị trí SDK của mình. Nếu không, bạn có thể tải NDK trực tiếp từ `NDK downloads page <https://developer.android.com/ndk/downloads>`_.

1. Giải nén zip native debug symbols bạn đã tải xuống trước đó (hoặc tạo bằng custom build). 2. Lưu crash log vào một file văn bản (ví dụ: ``crash.txt``).

.. important::

    ``ndk-stack`` tìm dòng đầu tiên gồm các dấu hoa thị khi phân tích crash log. Hãy đảm bảo ``crash.txt`` của bạn bắt đầu bằng dòng sau:

    ::

        *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***

3. Chạy ndk-stack với đường dẫn đến thư mục symbol khớp với CPU architecture của crash (ví dụ: ``arm64-v8a``):

::

    ndk-stack -sym path/to/native_debug_symbols/arm64-v8a/ -dump crash.txt

4. Kết quả sẽ hiển thị một trace đã được symbolicate, cho biết tên file và số dòng trong source code của Godot (hoặc custom build của bạn).
