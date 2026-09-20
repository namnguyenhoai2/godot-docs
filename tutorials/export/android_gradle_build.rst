.. _doc_android_gradle_build:

Build Gradle cho Android
========================

Godot cung cấp tùy chọn build bằng hệ thống build `Gradle <https://gradle.org/>`__ . Thay vì sử dụng template đã được build sẵn đi kèm với Godot, một dự án Android Java sẽ được cài đặt vào thư mục dự án của bạn. Sau đó, Godot sẽ build dự án này và sử dụng nó làm export template mỗi khi bạn export dự án.

Có một số lý do khiến bạn có thể muốn thực hiện việc này:

- Export tệp AAB cho Google Play. - Sửa đổi dự án trước khi build. - Thêm các SDK bên ngoài được build cùng với dự án của bạn.

Phần native của template (thư viện ``.so`` được tích hợp trong APK) vẫn được biên dịch sẵn. Điều này có nghĩa là, không giống như
:ref:`compiling a custom Android export template <doc_compiling_for_android>`,
bạn không cần cài đặt toolchain C++ hoặc clone mã nguồn Godot.

Cấu hình Gradle build là một quy trình khá đơn giản. Nhưng trước tiên, bạn cần làm theo các bước trong :ref:`exporting for android <doc_exporting_for_android>` cho đến **Setting it up in Godot**. Sau đó, hãy làm theo các bước bên dưới.

Thiết lập môi trường Gradle build
---------------------------------

Mở menu Project và cài đặt template *Gradle Build*:

.. image:: img/gradle_build_install_template.webp

Hãy đảm bảo các export template đã được tải xuống. Nếu chưa, menu này sẽ giúp bạn tải chúng xuống.

Một dự án Android dựa trên Gradle sẽ được tạo trong ``res://android/build``. Bạn không cần chỉnh sửa các tệp này trừ khi thực sự cần sửa đổi dự án.

Thực hiện Gradle build từ Android editor
----------------------------------------

Kể từ Godot 4.6, bạn có thể thực hiện Gradle build từ Android editor. Việc này yêu cầu cài đặt ứng dụng `Godot Android Build Environment (GABE) <https://godotengine.org/download/android/#gabe>`__ trên cùng thiết bị đang chạy editor.

.. note::

    Ứng dụng này *không* bắt buộc khi export từ Android editor bằng các APK template đã được build sẵn hoặc khi export sang các nền tảng khác.

Ứng dụng này cho phép bạn cài đặt mọi thành phần cần thiết để build các dự án Android bằng Gradle. Editor sẽ gọi ứng dụng này để thực hiện Gradle build khi export sang Android.

Để thiết lập môi trường build, hãy mở ứng dụng và làm theo các hướng dẫn sau:

- Đảm bảo bạn có kết nối Internet đang hoạt động. - Mở tab :menu:`Rootfs` từ thanh điều hướng phía dưới. - Nhấp vào :button:`Install Rootfs`.

Sau khi quá trình cài đặt hoàn tất, bạn có thể export các dự án bằng Gradle build từ Godot editor.

Bật Gradle build và export
--------------------------

Khi thiết lập dự án Android trong hộp thoại **Project > Export**, cần bật **Gradle Build**:

.. image:: img/gradle_build_enable.webp

Từ lúc này, mỗi lần bạn cố gắng export dự án hoặc one-click deploy, hệ thống sẽ gọi hệ thống Gradle build để tạo các template mới. Các template đã build sẽ tự động được sử dụng sau đó, vì vậy không cần cấu hình thêm.

.. note::

    Khi sử dụng hệ thống Android build dựa trên Gradle, các asset được đặt trong một thư mục có tên bắt đầu bằng dấu gạch dưới sẽ không được đưa vào APK được tạo. Điều này không áp dụng cho các asset có tên *tệp* bắt đầu bằng dấu gạch dưới.

    Ví dụ: ``_example/image.png`` sẽ **không** được đưa vào dưới dạng asset, nhưng ``_image.png`` thì có.
