.. _doc_exporting_for_android:

Xuất cho Android
================


.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang Android. Nếu bạn muốn biên dịch các binary của export template từ mã nguồn thay vào đó, hãy đọc :ref:`doc_compiling_for_android`.

Xuất cho Android có ít yêu cầu hơn so với việc biên dịch Godot cho Android. Các bước sau đây trình bày chi tiết những gì cần thiết để thiết lập Android SDK và engine.

.. attention::

    Các dự án viết bằng C# có thể được xuất sang Android kể từ Godot 4.2, nhưng tính năng hỗ trợ đang ở trạng thái thử nghiệm và :ref:`some limitations apply <doc_c_sharp_platforms>`.

Thiết lập trên Android
----------------------

Khi xuất sang Android từ trình chỉnh sửa Android, bạn **không** cần cài đặt OpenJDK hoặc Android SDK khi xuất sang Android, bất kể sử dụng phương thức xuất nào (APK dựng sẵn hoặc Gradle build).

Tuy nhiên, nếu bạn đang thực hiện Gradle build, bạn sẽ cần làm theo một số bước được mô tả trong :ref:`doc_android_gradle_build`.

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

- Bạn có thể cài đặt Android SDK bằng `Android Studio Iguana (version 2023.2.1) or later <https://developer.android.com/studio/>`__.

  - Chạy công cụ này một lần để hoàn tất việc thiết lập SDK bằng các `instructions <https://developer.android.com/studio/intro/update#sdk-manager>`__. - Đảm bảo rằng `required packages <https://developer.android.com/studio/intro/update#required>`__ cũng được cài đặt.

    - Android SDK Platform-Tools phiên bản 35.0.0 trở lên - Android SDK Build-Tools phiên bản 35.0.1 - Android SDK Platform 35 - Android SDK Command-line Tools (latest)

  - Đảm bảo rằng `NDK and CMake are installed and configured <https://developer.android.com/studio/projects/install-ndk>`__.

    - CMake phiên bản 3.10.2.4988404. - NDK phiên bản r28b (28.1.13356709)

- Ngoài ra, bạn có thể cài đặt Android SDK bằng công cụ dòng lệnh `sdkmanager`.

  - Cài đặt gói command line tools bằng các `instructions <https://developer.android.com/tools/sdkmanager>`__. - Sau khi cài đặt command line tools, chạy lệnh `sdkmanager` sau đây để hoàn tất quá trình thiết lập:

::

    sdkmanager --sdk_root=<android_sdk_path> "platform-tools" "build-tools;35.0.1" "platforms;android-35" "cmdline-tools;latest" "cmake;3.10.2.4988404" "ndk;28.1.13356709"

.. note::

    Nếu bạn đang sử dụng Linux, **không sử dụng Android SDK do các repository của bản phân phối cung cấp vì SDK này thường đã lỗi thời**.

Thiết lập trong Godot
^^^^^^^^^^^^^^^^^^^^^

Mở màn hình Editor Settings (trong tab Godot trên macOS hoặc tab Editor trên các nền tảng khác). Màn hình này chứa các cài đặt editor cho tài khoản người dùng trên máy tính (độc lập với dự án).

.. image:: img/editorsettings.webp

Cuộn xuống phần chứa các cài đặt Android:

.. image:: img/android_editor_settings.webp

Trong màn hình đó, cần thiết lập 2 đường dẫn:

- ``Java SDK Path`` phải là vị trí đã cài đặt OpenJDK 17.

- ``Android SDK Path`` phải là vị trí đã cài đặt Android SDK. Thư mục này phải chứa ``platform-tools/adb``. - Ví dụ: ``%LOCALAPPDATA%\Android\Sdk\`` trên Windows hoặc ``/Users/$USER/Library/Android/sdk/`` trên macOS.

Sau khi cấu hình xong, mọi thứ đã sẵn sàng để xuất sang Android!

.. note::

    Nếu bạn gặp lỗi có nội dung *"Could not install to device."*, hãy đảm bảo rằng trên thiết bị chưa cài đặt một ứng dụng có cùng tên gói Android (nhưng được ký bằng một key khác).

    Nếu trên thiết bị đã cài đặt một ứng dụng có cùng tên gói Android nhưng dùng key ký khác, bạn **phải** gỡ ứng dụng đó khỏi thiết bị Android trước khi xuất sang Android lần nữa.

.. _doc_exporting_for_android_providing_launcher_icons:

Cung cấp launcher icon
----------------------

Launcher icon được các ứng dụng Android launcher sử dụng để đại diện cho ứng dụng của bạn với người dùng. Godot chỉ yêu cầu icon độ phân giải cao (cho màn hình mật độ ``xxxhdpi``) và sẽ tự động tạo các biến thể có độ phân giải thấp hơn.

Có ba loại icon:

- **Main Icon:** Icon "cổ điển". Icon này sẽ được sử dụng trên tất cả phiên bản Android đến trước Android 8 (Oreo). Kích thước tối thiểu là 192×192 px. - **Adaptive Icons:** Kể từ Android 8 (bao gồm cả phiên bản này), `Adaptive Icons <https://developer.android.com/develop/ui/compose/system/icon_design_adaptive>`_ được giới thiệu. Ứng dụng cần bao gồm các icon background và foreground riêng biệt để có giao diện gốc. Ứng dụng launcher của người dùng sẽ kiểm soát hiệu ứng chuyển động và việc mask icon. Kích thước tối thiểu là 432×432 px. - **Themed Icons (optional):** Kể từ Android 13 (bao gồm cả phiên bản này), Themed Icons được giới thiệu. Ứng dụng cần bao gồm một icon monochrome để bật tính năng này. Ứng dụng launcher của người dùng sẽ kiểm soát theme của icon. Kích thước tối thiểu là 432×432 px.

.. seealso:: It's important to adhere to some rules when designing adaptive icons. `Google Design has provided a nice article <https://medium.com/google-design/designing-adaptive-icons-515af294c783>`_ that helps to understand those rules and some of the capabilities of adaptive icons.

.. caution:: The most important adaptive icon design rule is to have your icon critical elements inside the safe zone: a centered circle with a diameter of 66dp (264 pixels on ``xxxhdpi``) to avoid being clipped by the launcher.

Nếu bạn không cung cấp các icon được yêu cầu (ngoại trừ Monochrome), Godot sẽ thay thế chúng bằng fallback chain, thử icon tiếp theo khi icon hiện tại không thành công:

- **Main Icon:** Main icon được cung cấp -> Project icon -> Main icon mặc định của Godot. - **Adaptive Icon Foreground:** Foreground icon được cung cấp -> Main icon được cung cấp -> Project icon -> Foreground icon mặc định của Godot. - **Adaptive Icon Background:** Background icon được cung cấp -> Background icon mặc định của Godot.

Bạn nên cung cấp tất cả icon được yêu cầu với độ phân giải đã chỉ định. Nhờ vậy, ứng dụng của bạn sẽ hiển thị đẹp trên mọi thiết bị và phiên bản Android.

Xuất cho Google Play Store
--------------------------

Tất cả ứng dụng mới được tải lên Google Play sau tháng 8 năm 2021 phải là tệp AAB (Android App Bundle). Để xuất tệp AAB, bạn cần thiết lập :ref:`doc_android_gradle_build`.

Việc tải AAB hoặc APK lên Play Store của Google yêu cầu bạn ký bằng một tệp keystore không ở chế độ debug; bạn có thể tạo tệp như sau:

.. code-block:: shell

    keytool -v -genkey -keystore mygame.keystore -alias mygame -keyalg RSA -validity 10000

Keystore và key này được dùng để xác minh danh tính developer của bạn; hãy nhớ mật khẩu và cất giữ ở nơi an toàn! Bạn nên chỉ sử dụng chữ hoa, chữ thường và chữ số. Ký tự đặc biệt có thể gây lỗi. Hãy sử dụng hướng dẫn Android Developer của Google để tìm hiểu thêm về `app signing <https://developer.android.com/studio/publish/app-signing>`__.

Bây giờ hãy điền các biểu mẫu sau trong Android Export Presets:

.. image:: img/editor-export-presets-android.webp

- **Release:** Nhập đường dẫn đến tệp keystore bạn vừa tạo. - **Release User:** Thay thế bằng key alias. - **Release Password:** Mật khẩu key. Lưu ý rằng hiện tại mật khẩu keystore và mật khẩu key phải giống nhau.

Đừng quên bỏ chọn checkbox **Export With Debug** trong khi xuất.

.. image:: img/export-with-debug-button.webp

Tối ưu hóa kích thước tệp
-------------------------

Bạn có thể tối ưu kích thước ứng dụng bằng cách biên dịch một export template Android chỉ với các tính năng bạn cần. Xem :ref:`doc_optimizing_for_size` để biết thêm thông tin.

Thực hiện custom Gradle build
-----------------------------

Nếu cần sửa đổi mã Java của template hoặc tích hợp với các Android SDK của bên thứ ba, bạn có thể muốn sử dụng custom Gradle build thay vì template APK dựng sẵn mặc định. Điều này cho phép bạn kiểm soát nhiều hơn đối với quá trình build và project được tạo, đồng thời bạn có thể sử dụng nó làm nền tảng để tùy chỉnh thêm.

Xem :ref:`doc_android_gradle_build` để biết hướng dẫn thiết lập custom Gradle build.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập tùy chọn xuất bên ngoài editor. Trong quá trình xuất, các biến này sẽ ghi đè các giá trị bạn đã thiết lập trong menu xuất.

.. list-table:: Android export environment variables
   :header-rows: 1

   * - Tùy chọn xuất
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

Tùy chọn xuất
-------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn xuất có sẵn trong
:ref:`class_EditorExportPlatformAndroid` class reference.
