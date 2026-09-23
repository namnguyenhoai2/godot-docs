.. _doc_using_the_android_editor:

Sử dụng editor trên Android
===========================

Vào năm 2023, chúng tôi đã bổ sung `bản port Android của editor <https://godotengine.org/article/android_godot_editor_play_store_beta_release/>`__, cho phép tạo, phát triển và export các dự án 2D và 3D trên thiết bị Android.

Bạn có thể tải ứng dụng xuống từ `trang tải xuống Godot <https://godotengine.org/download/android/>`__ hoặc từ `Google Play Store <https://play.google.com/store/apps/details?id=org.godotengine.editor.v4>`__.

.. note::

    Editor trên Android hiện đang ở giai đoạn early access, trong khi chúng tôi tiếp tục hoàn thiện trải nghiệm. Xem :ref:`doc_using_the_android_editor_limitations` bên dưới.

Thiết bị Android được hỗ trợ
----------------------------

Editor trên Android yêu cầu thiết bị chạy Android 5 Lollipop trở lên và hỗ trợ ít nhất OpenGL 3. Danh sách này bao gồm (nhưng không giới hạn):

- Máy tính bảng, thiết bị gập và điện thoại màn hình lớn Android
- Netbook chạy Android
- Chromebook hỗ trợ ứng dụng Android

Quyền runtime
-------------

- `Quyền truy cập tất cả tệp <https://developer.android.com/training/data-storage/manage-all-files#all-files-access>`__: Cho phép editor tạo, import và đọc các tệp dự án từ mọi vị trí tệp trên thiết bị. Không có quyền này, editor vẫn hoạt động nhưng bị giới hạn quyền truy cập vào các tệp và thư mục của thiết bị.
- `REQUEST_INSTALL_PACKAGES <https://developer.android.com/reference/android/Manifest.permission#REQUEST_INSTALL_PACKAGES>`__: Cho phép editor cài đặt các APK của dự án đã export.
- `RECORD_AUDIO <https://developer.android.com/reference/android/Manifest.permission#RECORD_AUDIO>`__: Được yêu cầu khi thiết lập dự án `audio/driver/enable_input <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-audio-driver-enable-input>`__ được bật.

Mẹo và thủ thuật
----------------

**Input**

- Để có trải nghiệm tốt nhất và năng suất cao, bạn nên kết nối bàn phím và chuột bluetooth để tương tác với editor trên Android. Editor trên Android hỗ trợ tất cả `phím tắt và ánh xạ phím thường dùng <https://docs.godotengine.org/en/stable/tutorials/editor/default_key_mapping.html>`__.
- Khi tương tác bằng bàn phím và chuột, bạn có thể giảm kích thước thanh cuộn bằng thiết lập editor `interface/touchscreen/increase_scrollbar_touch_area <https://docs.godotengine.org/en/stable/classes/class_editorsettings.html#class-editorsettings-property-interface-touchscreen-increase-scrollbar-touch-area>`__.
- Đối với các dự án 2D, `plugin block coding <https://godotengine.org/asset-library/asset/3095>`__ có thể cung cấp một giải pháp trực quan dựa trên block, thay thế cho việc soạn script khi không có bàn phím phần cứng được kết nối.

**Đa nhiệm**

- Trên các thiết bị nhỏ hơn, việc bật và sử dụng chế độ picture-in-picture (PiP) cho phép dễ dàng chuyển đổi giữa *Editor* và *cửa sổ Play*.

  - Có thể bật PiP thông qua thiết lập editor `run/window_placement/play_window_pip_mode <https://docs.godotengine.org/en/latest/classes/class_editorsettings.html#class-editorsettings-property-run-window-placement-play-window-pip-mode>`__.
  - Có thể sử dụng thiết lập editor `run/window_placement/android_window <https://docs.godotengine.org/en/latest/classes/class_editorsettings.html#class-editorsettings-property-run-window-placement-android-window>`__ để chỉ định liệu cửa sổ *Play* có luôn khởi chạy ở chế độ PiP hay không.
  - **Lưu ý:** Ở chế độ PiP, cửa sổ *Play* không có quyền truy cập input.

**Đồng bộ dự án**

- Có thể đồng bộ dự án thông qua Git bằng cách tải xuống một Git client trên Android. Chúng tôi khuyên dùng `terminal Termux <https://termux.dev/en/>`__, một trình giả lập terminal trên Android cung cấp quyền truy cập vào các tiện ích terminal phổ biến như Git và SSH.

  - **Lưu ý:** Để sử dụng Git với terminal Termux, bạn cần cấp quyền *WRITE* cho terminal. Bạn có thể thực hiện việc này bằng cách `chạy lệnh sau <https://wiki.termux.com/wiki/Termux-setup-storage>`__ trong terminal: ``termux-setup-storage``

**Plugin**

- Các plugin GDExtension hoạt động như mong đợi, nhưng yêu cầu nhà phát triển plugin cung cấp các binary Android native.

.. _doc_using_the_android_editor_limitations:

Các giới hạn và vấn đề đã biết
------------------------------

Sau đây là các giới hạn và vấn đề đã biết của editor trên Android:

- Không hỗ trợ C#/Mono.
- Không hỗ trợ editor script bên ngoài.
- Mặc dù có sẵn, renderer Forward+ không được khuyến nghị do các vấn đề nghiêm trọng về hiệu suất.
- UX chưa được tối ưu cho form factor điện thoại Android.
- `Thiết bị Android Go <https://developer.android.com/guide/topics/androidgo>`__ không có quyền *All files access* cần thiết để đọc/ghi thiết bị. Để khắc phục, khi sử dụng thiết bị Android Go, bạn chỉ nên tạo dự án mới trong các thư mục Android *Documents* hoặc *Downloads*.
- Editor không tiếp tục hoạt động đúng cách khi *Don't keep activities* được bật trong *Developer Options*.
- Có một `lỗi <https://github.com/godotengine/godot/issues/70751>`__ với bàn phím Samsung khiến input ngẫu nhiên được chèn vào khi viết script. Bạn nên sử dụng `bàn phím Google (Gboard) <https://play.google.com/store/apps/details?id=com.google.android.inputmethod.latin>`__ thay thế.

.. seealso::

    Xem `danh sách các issue đang mở trên GitHub liên quan đến editor trên Android <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Aplatform%3Aandroid+label%3Atopic%3Aeditor>`__ để biết danh sách các bug đã biết.
