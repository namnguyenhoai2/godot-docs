.. _doc_exporting_for_android:

Xuất sang Android
=================


.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang Android. Nếu bạn muốn biên dịch các tệp nhị phân export template từ mã nguồn thay vào đó, hãy đọc :ref:`doc_compiling_for_android`.

Xuất sang Android có ít yêu cầu hơn so với việc biên dịch Godot cho Android. Các bước sau đây trình bày chi tiết những gì cần thiết để thiết lập Android SDK và engine.

.. attention::

    Các dự án viết bằng C# có thể được xuất sang Android kể từ Godot 4.2, nhưng tính năng này đang ở giai đoạn thử nghiệm và :ref:`có một số hạn chế <doc_c_sharp_platforms>`.

Thiết lập trên Android
----------------------

Khi xuất sang Android từ trình chỉnh sửa Android, bạn **không** cần cài đặt OpenJDK hoặc Android SDK khi xuất sang Android, bất kể phương thức export được sử dụng (APK dựng sẵn hay bản dựng Gradle).

Tuy nhiên, nếu đang thực hiện bản dựng Gradle, bạn sẽ cần làm theo một số bước được mô tả trong :ref:`doc_android_gradle_build`.

Sau đó, bạn có thể chuyển đến :ref:`doc_exporting_for_android_providing_launcher_icons`.

Thiết lập trên Windows, macOS và Linux
--------------------------------------

Cài đặt OpenJDK 17
^^^^^^^^^^^^^^^^^^

Tải xuống và cài đặt `OpenJDK 17 <https://adoptium.net/temurin/releases/?variant=openjdk17&version=17&os=any&arch=any>`__.

.. note::

    Các phiên bản JDK cao hơn cũng được hỗ trợ, nhưng chúng tôi khuyến nghị sử dụng JDK 17 để có khả năng tương thích và độ ổn định tối ưu.

Tải xuống Android SDK
^^^^^^^^^^^^^^^^^^^^^

Tải xuống và cài đặt Android SDK.

- Bạn có thể cài đặt Android SDK bằng `Android Studio Iguana (phiên bản 2023.2.1) hoặc mới hơn <https://developer.android.com/studio/>`__.

  - Chạy công cụ này một lần để hoàn tất thiết lập SDK theo `hướng dẫn <https://developer.android.com/studio/intro/update#sdk-manager>`__ này.
  - Đảm bảo rằng `các gói bắt buộc <https://developer.android.com/studio/intro/update#required>`__ cũng đã được cài đặt.

    - Android SDK Platform-Tools phiên bản 35.0.0 hoặc mới hơn
    - Android SDK Build-Tools phiên bản 35.0.1
    - Android SDK Platform 35
    - Android SDK Command-line Tools (latest)

  - Đảm bảo rằng `NDK và CMake đã được cài đặt và cấu hình <https://developer.android.com/studio/projects/install-ndk>`__.

    - CMake phiên bản 3.10.2.4988404
    - NDK phiên bản r28b (28.1.13356709)

- Ngoài ra, bạn có thể cài đặt Android SDK bằng công cụ `sdkmanager` dòng lệnh.

  - Cài đặt gói command line tools theo `hướng dẫn <https://developer.android.com/tools/sdkmanager>`__ này.
  - Sau khi cài đặt command line tools, hãy chạy lệnh `sdkmanager` sau để hoàn tất quá trình thiết lập:

::

    sdkmanager --sdk_root=<android_sdk_path> "platform-tools" "build-tools;35.0.1" "platforms;android-35" "cmdline-tools;latest" "cmake;3.10.2.4988404" "ndk;28.1.13356709"

.. note::

    Nếu đang sử dụng Linux, **không sử dụng Android SDK do kho phần mềm của bản phân phối cung cấp vì SDK này thường đã lỗi thời**.

Thiết lập trong Godot
^^^^^^^^^^^^^^^^^^^^^

Mở màn hình Editor Settings (trong tab Godot trên macOS hoặc tab Editor trên các nền tảng khác). Màn hình này chứa các thiết lập trình chỉnh sửa cho tài khoản người dùng trên máy tính (độc lập với dự án).

.. image:: img/editorsettings.webp

Cuộn xuống phần chứa các thiết lập Android:

.. image:: img/android_editor_settings.webp

Trong màn hình đó, cần thiết lập 2 đường dẫn:

- ``Java SDK Path`` phải là vị trí đã cài đặt OpenJDK 17.

- ``Android SDK Path`` phải là vị trí đã cài đặt Android SDK. Thư mục này phải chứa ``platform-tools/adb``.
  - Ví dụ: ``%LOCALAPPDATA%\Android\Sdk\`` trên Windows hoặc ``/Users/$USER/Library/Android/sdk/`` trên macOS.

Sau khi cấu hình xong, mọi thứ đã sẵn sàng để export sang Android!

.. note::

    Nếu bạn gặp lỗi có nội dung *"Could not install to device."*, hãy đảm bảo rằng trên thiết bị không có ứng dụng nào có cùng tên package Android nhưng được ký bằng một khóa khác.

    Nếu trên thiết bị đã cài đặt một ứng dụng có cùng tên package Android nhưng dùng khóa ký khác, bạn **phải** gỡ ứng dụng đó khỏi thiết bị Android trước khi tiếp tục export sang Android.

.. _doc_exporting_for_android_providing_launcher_icons:

Cung cấp biểu tượng launcher
----------------------------

Biểu tượng launcher được các ứng dụng launcher của Android sử dụng để hiển thị ứng dụng của bạn cho người dùng. Godot chỉ yêu cầu các biểu tượng có độ phân giải cao (cho màn hình mật độ ``xxxhdpi``) và sẽ tự động tạo các biến thể có độ phân giải thấp hơn.

Có ba loại biểu tượng:

- **Main Icon:** Biểu tượng "cổ điển". Biểu tượng này sẽ được sử dụng trên tất cả phiên bản Android đến trước Android 8 (Oreo). Kích thước tối thiểu là 192×192 px.
- **Adaptive Icons:** Kể từ Android 8 (bao gồm cả phiên bản này), `Adaptive Icons <https://developer.android.com/develop/ui/compose/system/icon_design_adaptive>`_ được giới thiệu. Các ứng dụng cần bao gồm các biểu tượng nền và tiền cảnh riêng biệt để có giao diện gốc. Ứng dụng launcher của người dùng sẽ điều khiển hiệu ứng động và việc tạo mặt nạ cho biểu tượng. Kích thước tối thiểu là 432×432 px.
- **Themed Icons (tùy chọn):** Kể từ Android 13 (bao gồm cả phiên bản này), Themed Icons được giới thiệu. Các ứng dụng cần bao gồm một biểu tượng đơn sắc để bật tính năng này. Ứng dụng launcher của người dùng sẽ điều khiển chủ đề của biểu tượng. Kích thước tối thiểu là 432×432 px.

.. seealso:: Điều quan trọng là phải tuân thủ một số quy tắc khi thiết kế adaptive icons. `Google Design đã cung cấp một bài viết hữu ích <https://medium.com/google-design/designing-adaptive-icons-515af294c783>`_ giúp tìm hiểu các quy tắc đó cũng như một số khả năng của adaptive icons.

.. caution:: Quy tắc thiết kế adaptive icon quan trọng nhất là đặt các thành phần cốt lõi của biểu tượng bên trong vùng an toàn: một hình tròn ở giữa có đường kính 66dp (264 pixel trên ``xxxhdpi``) để tránh bị launcher cắt mất.

Nếu bạn không cung cấp các biểu tượng được yêu cầu (ngoại trừ Monochrome), Godot sẽ thay thế chúng bằng một chuỗi dự phòng, thử mục tiếp theo khi mục hiện tại không thành công:

- **Main Icon:** Biểu tượng main được cung cấp -> Biểu tượng project -> Biểu tượng main mặc định của Godot.
- **Adaptive Icon Foreground:** Biểu tượng tiền cảnh được cung cấp -> Biểu tượng main được cung cấp -> Biểu tượng project -> Biểu tượng tiền cảnh mặc định của Godot.
- **Adaptive Icon Background:** Biểu tượng nền được cung cấp -> Biểu tượng nền mặc định của Godot.

Bạn nên cung cấp tất cả các biểu tượng được yêu cầu với độ phân giải đã chỉ định. Nhờ đó, ứng dụng của bạn sẽ hiển thị đẹp trên mọi thiết bị và phiên bản Android.

Xuất cho Google Play Store
--------------------------

Tất cả ứng dụng mới được tải lên Google Play sau tháng 8 năm 2021 phải là tệp AAB (Android App Bundle). Để xuất tệp AAB, bạn cần thiết lập :ref:`doc_android_gradle_build`.

Việc tải AAB hoặc APK lên Play Store của Google yêu cầu bạn ký bằng tệp keystore không ở chế độ debug; bạn có thể tạo tệp này như sau:

.. code-block:: shell

    keytool -v -genkey -keystore mygame.keystore -alias mygame -keyalg RSA -validity 10000

Keystore và key này được dùng để xác minh danh tính nhà phát triển của bạn. Hãy ghi nhớ mật khẩu và cất giữ ở nơi an toàn! Bạn nên chỉ sử dụng chữ hoa, chữ thường và chữ số. Các ký tự đặc biệt có thể gây lỗi. Hãy xem hướng dẫn Android Developer của Google để tìm hiểu thêm về `app signing <https://developer.android.com/studio/publish/app-signing>`__.

Bây giờ hãy điền các biểu mẫu sau trong Android Export Presets:

.. image:: img/editor-export-presets-android.webp

- **Release:** Nhập đường dẫn đến tệp keystore bạn vừa tạo.
- **Release User:** Thay thế bằng bí danh của key.
- **Release Password:** Mật khẩu của key. Lưu ý rằng hiện tại mật khẩu keystore và mật khẩu key phải giống nhau.

Đừng quên bỏ chọn hộp kiểm **Export With Debug** trong khi xuất.

.. image:: img/export-with-debug-button.webp

Tối ưu hóa kích thước tệp
-------------------------

Bạn có thể tối ưu hóa kích thước ứng dụng bằng cách biên dịch Android export template chỉ với các tính năng cần thiết. Xem :ref:`doc_optimizing_for_size` để biết thêm thông tin.

Thực hiện custom Gradle build
-----------------------------

Nếu cần sửa đổi mã Java của template hoặc tích hợp với các Android SDK của bên thứ ba, bạn có thể muốn sử dụng custom Gradle build thay cho APK template dựng sẵn mặc định. Điều này cho phép bạn kiểm soát nhiều hơn quy trình build và project được tạo, đồng thời bạn có thể sử dụng nó làm nền tảng để tùy chỉnh thêm.

Xem :ref:`doc_android_gradle_build` để biết hướng dẫn thiết lập custom Gradle build.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập các tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè những giá trị bạn đã thiết lập trong menu export.

.. list-table:: Các biến môi trường export Android
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``
   * - Options / Keystore / Debug
     - ``GODOT_ANDROID_KEYSTORE_DEBUG_PATH``
   * - Options / Keystore / Debug User
     - ``GODOT_ANDROID_KEYSTORE_DEBUG_USER``
   * - Options / Keystore / Debug Password
     - ``GODOT_ANDROID_KEYSTORE_DEBUG_PASSWORD``
   * - Options / Keystore / Release
     - ``GODOT_ANDROID_KEYSTORE_RELEASE_PATH``
   * - Options / Keystore / Release User
     - ``GODOT_ANDROID_KEYSTORE_RELEASE_USER``
   * - Options / Keystore / Release Password
     - ``GODOT_ANDROID_KEYSTORE_RELEASE_PASSWORD``

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có sẵn trong
:ref:`class_EditorExportPlatformAndroid` class reference.

.. _`Adaptive Icons`: https://developer.android.com/develop/ui/compose/system/icon_design_adaptive
.. _`Google Design has provided a nice article`: https://medium.com/google-design/designing-adaptive-icons-515af294c783
