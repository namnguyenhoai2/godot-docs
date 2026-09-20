.. _doc_using_the_android_editor:

Sử dụng trình chỉnh sửa trên Android
====================================

Vào năm 2023, chúng tôi đã bổ sung một `Android port of the editor <https://godotengine.org/article/android_godot_editor_play_store_beta_release/>`__ có thể được sử dụng để tạo, phát triển và xuất các dự án 2D và 3D trên thiết bị Android.

Bạn có thể tải ứng dụng từ `Godot download page <https://godotengine.org/download/android/>`__ hoặc `Google Play Store <https://play.google.com/store/apps/details?id=org.godotengine.editor.v4>`__.

.. note::

    Trình chỉnh sửa Android đang ở giai đoạn early access trong khi chúng tôi tiếp tục hoàn thiện trải nghiệm. Xem :ref:`doc_using_the_android_editor_limitations` bên dưới.

Thiết bị Android được hỗ trợ
----------------------------

Trình chỉnh sửa Android yêu cầu thiết bị chạy Android 5 Lollipop trở lên và hỗ trợ ít nhất OpenGL 3. Danh sách này bao gồm (không đầy đủ):

- Máy tính bảng, thiết bị gập và điện thoại cỡ lớn Android - Netbook chạy Android - Chromebook hỗ trợ ứng dụng Android

Quyền runtime
-------------

- `All files access permission <https://developer.android.com/training/data-storage/manage-all-files#all-files-access>`__: Cho phép trình chỉnh sửa tạo, nhập và đọc các tệp dự án từ mọi vị trí tệp trên thiết bị. Nếu không có quyền này, trình chỉnh sửa vẫn hoạt động nhưng quyền truy cập vào các tệp và thư mục trên thiết bị bị hạn chế. - `REQUEST_INSTALL_PACKAGES <https://developer.android.com/reference/android/Manifest.permission#REQUEST_INSTALL_PACKAGES>`__: Cho phép trình chỉnh sửa cài đặt các APK dự án đã xuất. - `RECORD_AUDIO <https://developer.android.com/reference/android/Manifest.permission#RECORD_AUDIO>`__: Được yêu cầu khi thiết lập dự án `audio/driver/enable_input <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-audio-driver-enable-input>`__ được bật.

Mẹo & thủ thuật
---------------

**Input**

- Để có trải nghiệm tốt nhất và năng suất cao, bạn nên kết nối bàn phím và chuột bluetooth để tương tác với trình chỉnh sửa Android. Trình chỉnh sửa Android hỗ trợ tất cả `usual shortcuts and key mappings <https://docs.godotengine.org/en/stable/tutorials/editor/default_key_mapping.html>`__. - Khi tương tác bằng bàn phím và chuột, bạn có thể giảm kích thước thanh cuộn bằng thiết lập trình chỉnh sửa `interface/touchscreen/increase_scrollbar_touch_area <https://docs.godotengine.org/en/stable/classes/class_editorsettings.html#class-editorsettings-property-interface-touchscreen-increase-scrollbar-touch-area>`__. - Đối với các dự án 2D, `block coding plugin <https://godotengine.org/asset-library/asset/3095>`__ có thể cung cấp một giải pháp trực quan dựa trên khối thay thế cho việc soạn script khi không có bàn phím phần cứng được kết nối.

**Đa nhiệm**

- Trên các thiết bị nhỏ hơn, việc bật và sử dụng chế độ picture-in-picture (PiP) cho phép dễ dàng chuyển đổi giữa *Editor* và *Play window*.

  - Có thể bật PiP thông qua thiết lập trình chỉnh sửa `run/window_placement/play_window_pip_mode <https://docs.godotengine.org/en/latest/classes/class_editorsettings.html#class-editorsettings-property-run-window-placement-play-window-pip-mode>`__. - Thiết lập trình chỉnh sửa `run/window_placement/android_window <https://docs.godotengine.org/en/latest/classes/class_editorsettings.html#class-editorsettings-property-run-window-placement-android-window>`__ có thể được sử dụng để chỉ định liệu cửa sổ *Play* có luôn khởi chạy ở chế độ PiP hay không. - **Lưu ý:** Ở chế độ PiP, cửa sổ *Play* không có quyền truy cập input.

**Đồng bộ hóa dự án**

- Có thể đồng bộ hóa các dự án qua Git bằng cách tải xuống một Git client dành cho Android. Chúng tôi khuyến nghị `Termux terminal <https://termux.dev/en/>`__, một trình giả lập terminal trên Android cung cấp quyền truy cập vào các tiện ích terminal phổ biến như Git và SSH.

  - **Lưu ý:** Để sử dụng Git với terminal Termux, bạn cần cấp quyền *WRITE* cho terminal. Bạn có thể thực hiện việc này bằng cách `running the following command <https://wiki.termux.com/wiki/Termux-setup-storage>`__ từ bên trong terminal: ``termux-setup-storage``

**Plugins**

- Các plugin GDExtension hoạt động như mong đợi, nhưng yêu cầu nhà phát triển plugin cung cấp các binary Android native.

.. _doc_using_the_android_editor_limitations:

Hạn chế & sự cố đã biết
-----------------------

Dưới đây là các hạn chế và sự cố đã biết của trình chỉnh sửa Android:

- Không hỗ trợ C#/Mono. - Không hỗ trợ các trình chỉnh sửa script bên ngoài. - Mặc dù có sẵn, renderer Forward+ không được khuyến nghị do các vấn đề nghiêm trọng về hiệu suất. - UX chưa được tối ưu hóa cho kiểu dáng điện thoại Android. - `Android Go devices <https://developer.android.com/guide/topics/androidgo>`__ thiếu quyền *All files access* cần thiết để đọc/ghi thiết bị. Giải pháp tạm thời là khi sử dụng thiết bị Android Go, bạn chỉ nên tạo dự án mới trong các thư mục Android *Documents* hoặc *Downloads*. - Trình chỉnh sửa không tiếp tục hoạt động đúng cách khi *Don't keep activities* được bật trong *Developer Options*. - Có `bug <https://github.com/godotengine/godot/issues/70751>`__ với bàn phím Samsung khiến input ngẫu nhiên được chèn vào khi viết script. Bạn nên sử dụng `Google keyboard (Gboard) <https://play.google.com/store/apps/details?id=com.google.android.inputmethod.latin>`__ thay thế.

.. seealso::

    Xem `list of open issues on GitHub related to the Android editor <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Aplatform%3Aandroid+label%3Atopic%3Aeditor>`__ để biết danh sách các lỗi đã biết.
