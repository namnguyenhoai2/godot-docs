.. _doc_using_the_xr_editor:

Sử dụng trình chỉnh sửa XR
==========================

Vào năm 2024, chúng tôi đã giới thiệu `Godot XR editor <https://godotengine.org/article/godot-editor-horizon-store-early-access-release/>`__, một phiên bản của trình chỉnh sửa Godot **được thiết kế để chạy nguyên bản trên các thiết bị XR**, cho phép tạo, phát triển và xuất các ứng dụng và trò chơi 2D, 3D và **XR** trực tiếp trên thiết bị.

Bạn có thể tải ứng dụng xuống từ `Google Play Store <https://play.google.com/store/apps/details?id=org.godotengine.editor.v4>`__, `Meta Horizon Store <https://www.meta.com/experiences/godot-game-engine/7713660705416473/>`__ hoặc `Godot download page <https://godotengine.org/download/preview/>`__.

.. note::

    The XR editor is in early access, while we continue to refine the experience. See :ref:`doc_using_the_xr_editor_limitations` below.

Hỗ trợ thiết bị XR
------------------

Hiện tại, trình chỉnh sửa Godot XR chỉ khả dụng trên các thiết bị Android XR và các thiết bị `Meta Quest <https://www.meta.com/quest/>`__ sau đây chạy **Meta Horizon OS v69 trở lên**:

 - Meta Quest 2 - Meta Quest 3 - Meta Quest 3s - Meta Quest Pro

.. note::

    Chúng tôi đang làm việc để bổ sung hỗ trợ cho nhiều thiết bị XR hơn, bao gồm các thiết bị PCVR.

Quyền runtime
-------------

- `All files access permission <https://developer.android.com/training/data-storage/manage-all-files#all-files-access>`__: Cho phép trình chỉnh sửa tạo, nhập và đọc các tệp dự án từ mọi vị trí tệp trên thiết bị. Nếu không có quyền này, trình chỉnh sửa vẫn hoạt động nhưng chỉ có quyền truy cập hạn chế vào các tệp và thư mục của thiết bị. - `REQUEST_INSTALL_PACKAGES <https://developer.android.com/reference/android/Manifest.permission#REQUEST_INSTALL_PACKAGES>`__: Cho phép trình chỉnh sửa cài đặt các APK của dự án đã xuất. - `RECORD_AUDIO <https://developer.android.com/reference/android/Manifest.permission#RECORD_AUDIO>`__: Được yêu cầu khi bật thiết lập dự án `audio/driver/enable_input <https://docs.godotengine.org/en/stable/classes/class_projectsettings.html#class-projectsettings-property-audio-driver-enable-input>`__. - `USE_SCENE (META ONLY) <https://developers.meta.com/horizon/documentation/native/native-spatial-data-perm/>`__: Bắt buộc để bật và truy cập các scene API khi chạy một dự án XR.

Mẹo & thủ thuật
---------------

**Input**

- Để có trải nghiệm tốt nhất và năng suất cao, bạn nên kết nối bàn phím và chuột bluetooth để tương tác với trình chỉnh sửa XR. Trình chỉnh sửa XR hỗ trợ tất cả `usual shortcuts and key mappings <https://docs.godotengine.org/en/stable/tutorials/editor/default_key_mapping.html>`__. - Khi tương tác với các controller được theo dõi hoặc bàn tay được theo dõi, bạn có thể bật thiết lập trình chỉnh sửa `interface/touchscreen/enable_long_press_as_right_click <https://docs.godotengine.org/en/stable/classes/class_editorsettings.html#class-editorsettings-property-interface-touchscreen-enable-long-press-as-right-click>`__ để bật thao tác nhấp chuột phải bằng cách nhấn giữ. - Khi tương tác với các controller được theo dõi hoặc bàn tay được theo dõi, bạn có thể tăng kích thước thanh cuộn bằng thiết lập trình chỉnh sửa `interface/touchscreen/increase_scrollbar_touch_area <https://docs.godotengine.org/en/stable/classes/class_editorsettings.html#class-editorsettings-property-interface-touchscreen-increase-scrollbar-touch-area>`__.

**Đa nhiệm trên Quest**

- `Theater View <https://www.meta.com/blog/quest/meta-quest-v67-update-new-window-layout-creator-content-horizon-feed/>`__ có thể được sử dụng để đưa *Editor window* sang chế độ toàn màn hình. - Bật `Seamless Multitasking <https://www.uploadvr.com/seamless-multitasking-experimental-quest/>`__, có trong *Experimental Settings* của Quest, để bật khả năng nhanh chóng chuyển đổi giữa một dự án XR đang chạy và *Editor window*. - Khi phát triển một dự án không phải XR, biểu tượng ứng dụng trình chỉnh sửa Godot sẽ cung cấp khả năng chuyển đổi giữa *Editor window* và *Play window* khi cửa sổ sau đang hoạt động, bằng tính năng *App menu* của Quest. - Khi phát triển và chạy một dự án XR, bạn có thể gọi lại *Editor window* bằng cách:

  - Nhấn nút *Meta* để gọi thanh menu - Nhấp vào biểu tượng ứng dụng trình chỉnh sửa Godot để mở *App menu* và chọn ô *Editor window*.

**Đồng bộ dự án**

- Có thể đồng bộ dự án qua Git bằng cách tải xuống một Git client cho Android. Chúng tôi khuyến nghị `Termux terminal <https://termux.dev/en/>`__, một trình giả lập terminal trên Android cung cấp quyền truy cập vào các tiện ích terminal phổ biến như Git và SSH.

  - **Lưu ý:** Để sử dụng Git với terminal Termux, bạn cần cấp quyền *WRITE* cho terminal. Bạn có thể thực hiện việc này bằng cách `running the following command <https://wiki.termux.com/wiki/Termux-setup-storage>`__ từ trong terminal: ``termux-setup-storage``

**Plugin**

- Các plugin GDExtension hoạt động như mong đợi, nhưng yêu cầu nhà phát triển plugin cung cấp các binary Android native.

.. _doc_using_the_xr_editor_limitations:

Hạn chế & sự cố đã biết
-----------------------

Dưới đây là các hạn chế và sự cố đã biết của trình chỉnh sửa XR:

- Không hỗ trợ C#/Mono. - Không hỗ trợ các trình chỉnh sửa script bên ngoài. - Mặc dù khả dụng, renderer *Vulkan Forward+* không được khuyến nghị do các vấn đề nghiêm trọng về hiệu năng.
