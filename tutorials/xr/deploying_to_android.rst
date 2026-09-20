.. _doc_deploying_to_android:

Triển khai lên Android
======================

Thiết lập
---------
Hầu hết các headset độc lập đều chạy trên Android và hỗ trợ OpenXR đang dần được triển khai trên các nền tảng này.

Trước khi làm theo các hướng dẫn dành riêng cho OpenXR tại đây, trước tiên bạn cần thiết lập hệ thống để xuất sang Android nói chung, bao gồm:

- Cài đặt OpenJDK 17 - Cài đặt Android Studio - Cấu hình vị trí của Android SDK trong Godot

Xem :ref:`doc_exporting_for_android` để biết đầy đủ chi tiết, rồi quay lại đây sau khi hoàn tất các bước này.

.. warning::

    Mặc dù renderer Mobile Vulkan có nhiều tối ưu hóa hướng đến các thiết bị di động, chúng tôi vẫn đang khắc phục một số vấn đề. Hiện tại, khi nhắm đến các thiết bị XR dựa trên Android, bạn rất nên sử dụng renderer compatibility (OpenGL).

Bản build Android bằng Gradle
-----------------------------

.. note::

    Hỗ trợ chính thức cho nền tảng Android ban đầu chưa được thêm vào đặc tả OpenXR, dẫn đến việc nhiều vendor tạo các loader tùy chỉnh để cung cấp OpenXR trên headset của họ. Mặc dù về lâu dài, dự kiến tất cả vendor sẽ áp dụng OpenXR loader chính thức, hiện tại bạn vẫn cần thêm các loader này vào project của mình.

Để đưa OpenXR loader dành riêng cho vendor vào project, bạn cần thiết lập một bản build Android bằng Gradle.

Chọn **Install Android Build Template...** từ menu **Project**:

.. image:: img/android_gradle_build.webp

Thao tác này sẽ tạo một thư mục có tên **android** bên trong project, chứa tất cả các tệp runtime cần thiết trên Android. Giờ bạn có thể tùy chỉnh bản cài đặt này. Godot sẽ không hiển thị thư mục này trong editor, nhưng bạn có thể tìm thấy nó bằng trình duyệt tệp.

Bạn có thể đọc thêm về các bản build Gradle tại đây: :ref:`doc_android_gradle_build`.

Cài đặt plugin của vendor
-------------------------

Bạn có thể tải plugin của vendor từ Asset Store, hãy tìm kiếm "OpenXR vendors".

.. image:: img/openxr_loader_asset_lib.webp

Bạn sẽ tìm thấy các tệp đã cài đặt bên trong thư mục **addons**. Ngoài ra, bạn có thể cài đặt thủ công plugin của vendor bằng cách tải xuống `from the release page here <https://github.com/GodotVR/godot_openxr_vendors/releases>`__. Bạn cần sao chép thư mục `assets/addons/godotopenxrvendors` từ tệp zip vào thư mục `addons` của project.

Bạn có thể tìm repository chính của plugin vendor `here <https://github.com/GodotVR/godot_openxr_vendors>`__.

.. note::

    Từ Godot 4.6 trở đi, plugin vendor là một plugin tùy chọn nhưng được khuyến nghị. Godot có thể xuất trực tiếp sang hầu hết các thiết bị tương thích với Android. Điều này có thể hữu ích cho các project minh họa và hướng dẫn, trong đó một APK duy nhất có thể được triển khai lên nhiều thiết bị. Plugin vendor mở khóa các triển khai và thiết lập dành riêng cho vendor, đồng thời có thể là yêu cầu để phát hành trên các app store.

Tạo các export preset
---------------------
Bạn cần thiết lập một export preset riêng cho từng thiết bị, vì mỗi thiết bị sẽ cần loader riêng được đưa vào.

Mở **Project** và chọn **Export..**. Nhấp vào **Add..** rồi chọn **Android**. Tiếp theo, đổi tên export preset theo thiết bị mà bạn đang thiết lập, chẳng hạn **Meta Quest**. Sau đó bật **Use Gradle Build**. Tiếp theo, đổi **XR Mode** thành **OpenXR**. Nếu muốn sử dụng one-click deploy (được mô tả bên dưới), hãy đảm bảo **Runnable** được bật.

Nếu đã cài plugin vendor, bạn cũng sẽ thấy các mục dành cho những headset khác nhau trong **XR Features**. Hãy chọn mục tương ứng với headset của bạn nếu có. Nếu không, hãy bật plugin Khronos.

.. image:: img/android_meta_quest.webp

Cuộn xuống cuối danh sách và bạn sẽ thấy các phần tính năng XR bổ sung; hiện chỉ có **Meta XR Features**, **Pico XR Features**, **Magicleap XR Features** và **Khronos XR Features** cho HTC. Bạn cần chọn các thiết lập phù hợp nếu muốn sử dụng những tính năng này.

Chạy trên thiết bị từ Godot editor
----------------------------------
Nếu bạn đã thiết lập các tùy chọn export như mô tả ở trên, đồng thời headset đã được kết nối với máy tính và được nhận diện chính xác, bạn có thể khởi chạy trực tiếp từ Godot editor bằng :ref:`doc_one-click_deploy`:

.. image:: img/android_one_click_deploy.webp

Đối với một số thiết bị trên một số nền tảng, bạn có thể cần thực hiện thêm một số bước để thiết bị được nhận diện chính xác, vì vậy hãy nhớ xem tài liệu dành cho developer từ vendor của headset.

Ví dụ, với Meta Quest 2, bạn cần bật chế độ developer trên headset; nếu đang sử dụng Windows, bạn cũng cần cài đặt các ADB driver đặc biệt. Xem `official Meta Quest developer documentation <https://developer.oculus.com/documentation/native/android/mobile-device-setup/>`_ để biết thêm chi tiết.

Nếu gặp bất kỳ vấn đề nào với one-click deploy, hãy kiểm tra :ref:`Troubleshooting section <doc_one-click_deploy_troubleshooting>`.
