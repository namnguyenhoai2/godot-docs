:allow_comments: False

.. _doc_system_requirements:

Yêu cầu hệ thống
================

Trang này chứa các yêu cầu hệ thống đối với trình chỉnh sửa và các dự án đã xuất. Các thông số kỹ thuật này chỉ nhằm mục đích tham khảo, nhưng bạn có thể xem chúng nếu đang muốn xây dựng hoặc nâng cấp một hệ thống để sử dụng Godot.

Trình chỉnh sửa Godot
---------------------

Đây là các thông số **tối thiểu** cần thiết để chạy trình chỉnh sửa Godot và làm việc trên một dự án 2D hoặc 3D đơn giản:

PC để bàn hoặc máy tính xách tay - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. Khi điều chỉnh thông số kỹ thuật, hãy đảm bảo chỉ đề cập đến phần cứng có thể chạy phiên bản hệ điều hành cần thiết. .. Ví dụ: mẫu Mac cũ nhất có thể chạy macOS 13 là iMac 2017, .. vì vậy yêu cầu CPU x86 cho macOS không nên được đặt trước mẫu đó.

+----------------------+-----------------------------------------------------------------------------------------+ | **CPU** | - **Windows:** CPU x86_32 hỗ trợ SSE2, CPU x86_64 hỗ trợ SSE4.2, CPU ARMv8 | | | | | | - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Snapdragon X Elite* | | | | | | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon) | | | | | | - *Ví dụ: CPU Intel thế hệ 7 (Kaby Lake), Apple M1* | | | | | | - **Linux:** CPU x86_32 hỗ trợ SSE2, CPU x86_64 hỗ trợ SSE4.2, CPU ARMv7 hoặc | | | ARMv8 | | | |
| | - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Raspberry Pi 4* |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** Đồ họa tích hợp hỗ trợ đầy đủ Vulkan 1.0 | | | | | | - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)* | | | | | | - **Trình kết xuất Mobile:** Đồ họa tích hợp hỗ trợ đầy đủ Vulkan 1.0 | | | | | | - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)* | | | | | | - **Trình kết xuất Compatibility:** Đồ họa tích hợp hỗ trợ đầy đủ OpenGL 3.3 | | | |
| | - *Ví dụ: Intel HD Graphics 2500 (Ivy Bridge), AMD Radeon R5 Graphics (Kaveri)* |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Trình chỉnh sửa Native:** 4 GB |
| | - **Trình chỉnh sửa Web:** 8 GB |
+++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 200 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm). | | | Việc xuất dự án yêu cầu tải riêng các mẫu xuất |
| | (lên đến 1,5 GB sau khi cài đặt, tùy thuộc vào các nền tảng đích được chọn). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Trình chỉnh sửa Native:** Windows 10, macOS 11 (máy Mac Intel), macOS 13 (máy Mac Apple Silicon), | | | bản phân phối Linux phát hành sau năm 2018 | | | - **Trình chỉnh sửa Web:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể |
| | (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. note::

    Nếu CPU x86_64 của bạn không hỗ trợ SSE4.2, bạn vẫn có thể chạy tệp thực thi Godot 32-bit, vốn chỉ yêu cầu SSE2 (tất cả CPU x86_64 đều hỗ trợ SSE2).

    Mặc dù được hỗ trợ trên Linux, chúng tôi không có yêu cầu tối thiểu chính thức để chạy trên rv64 (RISC-V), ppc64 và ppc32 (PowerPC), cũng như loongarch64. Ngoài ra, bạn phải tự biên dịch trình chỉnh sửa cho nền tảng đó (cũng như các mẫu xuất); hiện chưa có bản tải xuống chính thức. Bạn có thể tìm thấy hướng dẫn biên dịch RISC-V trên trang :ref:`doc_compiling_for_linuxbsd`.

Thiết bị di động (điện thoại thông minh/máy tính bảng) - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+ | **CPU** | - **Android:** SoC với CPU ARM hoặc x86 32-bit hoặc 64-bit bất kỳ | | | | | | - *Ví dụ: Qualcomm Snapdragon 430, Samsung Exynos 5 Octa 5430* | | | |
| | - **iOS:** *Không thể chạy trình chỉnh sửa* |
+++++++++++++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.0 | | | | | | - *Ví dụ: Qualcomm Adreno 505, Mali-G71 MP2* | | | | | | - **Trình kết xuất Mobile:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.0 | | | | | | - *Ví dụ: Qualcomm Adreno 505, Mali-G71 MP2* | | | | | | - **Trình kết xuất Compatibility:** SoC tích hợp GPU hỗ trợ đầy đủ OpenGL ES 3.0 | | | |
| | - *Ví dụ: Qualcomm Adreno 306, Mali-T628 MP6* |
+++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Trình chỉnh sửa Native:** 3 GB |
| | - **Trình chỉnh sửa Web:** 6 GB |
+++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 200 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm). | | | Việc xuất dự án yêu cầu tải riêng các mẫu xuất |
| | (lên đến 1,5 GB sau khi cài đặt, tùy thuộc vào các nền tảng đích được chọn). |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Trình chỉnh sửa Native:** Android 7.0 (Compatibility) hoặc Android 9.0 (Forward+/Mobile) | | | - **Trình chỉnh sửa Web:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể |
| | (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Đây là các thông số **khuyến nghị** để có trải nghiệm mượt mà với trình chỉnh sửa Godot trên một dự án 2D hoặc 3D đơn giản:

PC để bàn hoặc máy tính xách tay - Khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+---------------------------------------------------------------------------------------------+ | **CPU** | - **Windows:** CPU x86_64 hỗ trợ SSE4.2, có từ 4 lõi vật lý trở lên, CPU ARMv8 | | | | | | - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite* | | | | | | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon) | | | | | | - *Ví dụ: Intel Core i5-8500, Apple M1* | | | | | | - **Linux:** CPU x86_64 hỗ trợ SSE4.2, CPU ARMv7 hoặc ARMv8 | | | |
| | - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 có ép xung* |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** Đồ họa rời hỗ trợ đầy đủ Vulkan 1.2 | | | | | | - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)* | | | | | | - **Trình kết xuất Mobile:** Đồ họa rời hỗ trợ đầy đủ Vulkan 1.2 | | | | | | - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)* | | | | | | - **Trình kết xuất Compatibility:** Đồ họa rời hỗ trợ đầy đủ OpenGL 4.6 | | | |
| | - *Ví dụ: NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0)* |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Trình chỉnh sửa Native:** 8 GB |
| | - **Trình chỉnh sửa Web:** 12 GB |
++++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 2 GB (dùng cho tệp thực thi, tệp dự án, tất cả mẫu xuất và bộ nhớ đệm) |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Trình chỉnh sửa Native:** Windows 11, macOS 13, bản phân phối Linux phát hành sau năm 2020 |
| | - **Trình chỉnh sửa Web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Thiết bị di động (điện thoại thông minh/máy tính bảng) - Khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+ | **CPU** | - **Android:** SoC với CPU ARM hoặc x86 64-bit, có từ 3 lõi "hiệu năng" trở lên | | | | | | - *Ví dụ: Qualcomm Snapdragon 845, Samsung Exynos 9810* | | | |
| | - **iOS:** *Không thể chạy trình chỉnh sửa* |
+++++++++++++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.2 | | | | | | - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18* | | | | | | - **Trình kết xuất Mobile:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.2 | | | | | | - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18* | | | | | | - **Trình kết xuất Compatibility:** SoC tích hợp GPU hỗ trợ đầy đủ OpenGL ES 3.2 | | | |
| | - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18* |
+++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Trình chỉnh sửa Native:** 6 GB |
| | - **Trình chỉnh sửa Web:** 8 GB |
+++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 2 GB (dùng cho tệp thực thi, tệp dự án, tất cả mẫu xuất và bộ nhớ đệm) |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Trình chỉnh sửa Native:** Android 11.0 | | | - **Trình chỉnh sửa Web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera, |
| | Samsung Internet |
++++++++++++++++++++++

Dự án Godot đã xuất
-------------------

.. warning::

    Các yêu cầu dưới đây là mức cơ sở cho một dự án 2D hoặc 3D **đơn giản**, với tập lệnh cơ bản và ít hiệu ứng hình ảnh. Yêu cầu về CPU, GPU, RAM và bộ nhớ lưu trữ sẽ thay đổi đáng kể tùy thuộc vào phạm vi dự án, trình kết xuất, độ phân giải khung nhìn và các cài đặt đồ họa được chọn. Các chương trình khác đang chạy trên hệ thống trong khi dự án chạy cũng sẽ tranh giành tài nguyên, bao gồm RAM và RAM video.

    Bạn được khuyến nghị mạnh mẽ nên tự kiểm thử trên phần cứng cấp thấp để đảm bảo dự án chạy ở tốc độ mong muốn. Để cung cấp khả năng mở rộng cho phần cứng cấp thấp, bạn cũng cần thêm một `graphics options menu <https://github.com/godotengine/godot-demo-projects/tree/master/3d/graphics_settings>`__ vào dự án.

Đây là các thông số **tối thiểu** cần thiết để chạy một dự án 2D hoặc 3D đơn giản được xuất bằng Godot:

PC để bàn hoặc máy tính xách tay - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. Khi điều chỉnh thông số kỹ thuật, hãy đảm bảo chỉ đề cập đến phần cứng có thể chạy phiên bản hệ điều hành cần thiết. .. Ví dụ: mẫu Mac cũ nhất có thể chạy macOS 13 là iMac 2017, .. vì vậy yêu cầu CPU x86 cho macOS không nên được đặt trước mẫu đó.

+----------------------+-----------------------------------------------------------------------------------------+ | **CPU** | - **Windows:** CPU x86_32 hỗ trợ SSE2, CPU x86_64 hỗ trợ SSE4.2, | | | ARMv8 CPU | | | | | | - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Snapdragon X Elite* | | | | | | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon) | | | | | | - *Ví dụ: CPU Intel thế hệ 7 (Kaby Lake), Apple M1* | | | | | | - **Linux:** CPU x86_32 hỗ trợ SSE2, CPU x86_64 hỗ trợ SSE4.2, | | | CPU ARMv7 hoặc ARMv8 | | | |
| | - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Raspberry Pi 4* |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** Đồ họa tích hợp với hỗ trợ đầy đủ Vulkan 1.0, | | | hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (cấp tính năng 12_0) (Windows) | | | | | | - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)* | | | | | | - **Trình kết xuất Mobile:** Đồ họa tích hợp với hỗ trợ đầy đủ Vulkan 1.0, | | | hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (cấp tính năng 12_0) (Windows) | | | | | | - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)* | | | | | | - **Trình kết xuất Compatibility:** Đồ họa tích hợp với hỗ trợ đầy đủ OpenGL 3.3 | | | hoặc hỗ trợ Direct3D 11 (Windows). | | | |
| | - *Ví dụ: Intel HD Graphics 2500 (Ivy Bridge), AMD Radeon R5 Graphics (Kaveri)* |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Đối với bản xuất native:** 2 GB |
| | - **Đối với bản xuất web:** 4 GB |
++++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm) |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Đối với bản xuất native:** Windows 10, macOS 11 (máy Mac Intel), macOS 13 (máy | | | Mac Apple Silicon), bản phân phối Linux phát hành sau năm 2018 | | | - **Trình chỉnh sửa web:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể |
| | (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Thiết bị di động (điện thoại thông minh/máy tính bảng) - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+ | **CPU** | - **Android:** SoC với bất kỳ CPU ARM hoặc x86 32-bit hay 64-bit nào | | | | | | - *Ví dụ: Qualcomm Snapdragon 430, Samsung Exynos 5 Octa 5430* | | | | | | - **iOS:** SoC với bất kỳ CPU ARM 64-bit nào | | | |
| | - *Ví dụ: Apple A7 (iPhone 5S)* |
+++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** SoC có GPU với hỗ trợ đầy đủ Vulkan 1.0 hoặc | | | hỗ trợ Metal 3 (iOS/iPadOS) | | | | | | - *Ví dụ (Vulkan): Qualcomm Adreno 505, Mali-G71 MP2, Apple A12 (iPhone XR/XS)* | | | - *Ví dụ (Metal): Apple A12 (iPhone XR/XS)* | | | | | | - **Trình kết xuất Mobile:** SoC có GPU với hỗ trợ đầy đủ Vulkan 1.0 hoặc | | | hỗ trợ Metal 3 (iOS/iPadOS) | | | | | | - *Ví dụ (Vulkan): Qualcomm Adreno 505, Mali-G71 MP2, Apple A12 (iPhone XR/XS)* | | | - *Ví dụ (Metal): Apple A12 (iPhone XR/XS)* | | | | | | - **Trình kết xuất Compatibility:** SoC có GPU với hỗ trợ đầy đủ OpenGL ES 3.0 | | | |
| | - *Ví dụ: Qualcomm Adreno 306, Mali-T628 MP6, Apple A7 (iPhone 5S)* |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Đối với bản xuất native:** 1 GB |
| | - **Đối với bản xuất web:** 2 GB |
++++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm) |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Đối với bản xuất native:** Android 7.0 (Compatibility), Android 9.0 (Forward+/Mobile), | | | iOS 15.0 (Forward+/Mobile với Vulkan), iOS 16.0 (Forward+/Mobile với Metal) | | | - **Trình chỉnh sửa web:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể |
| | (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit. |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Đây là các thông số **khuyến nghị** để có trải nghiệm mượt mà với một dự án 2D hoặc 3D đơn giản được xuất bằng Godot:

PC để bàn hoặc máy tính xách tay - Khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------------------------------------------------------+ | **CPU** | - **Windows:** CPU x86_64 hỗ trợ SSE4.2, với từ 4 lõi vật lý trở lên, CPU ARMv8 | | | | | | - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite* | | | | | | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon) | | | | | | - *Ví dụ: Intel Core i5-8500, Apple M1* | | | | | | - **Linux:** CPU x86_64 hỗ trợ SSE4.2, với từ 4 lõi vật lý trở lên, | | | CPU ARMv7 hoặc ARMv8 | | | |
| | - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 có ép xung* |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** Đồ họa rời với hỗ trợ đầy đủ Vulkan 1.2, | | | hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (cấp tính năng 12_0) (Windows) | | | | | | - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)* | | | | | | - **Trình kết xuất Mobile:** Đồ họa rời với hỗ trợ đầy đủ Vulkan 1.2, | | | hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (cấp tính năng 12_0) (Windows) | | | | | | - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)* | | | | | | - **Trình kết xuất Compatibility:** Đồ họa rời với hỗ trợ đầy đủ OpenGL 4.6 | | | |
| | - *Ví dụ: NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0)* |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Đối với bản xuất native:** 4 GB |
| | - **Đối với bản xuất web:** 8 GB |
++++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm) |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Đối với bản xuất native:** Windows 11, macOS 13, bản phân phối Linux phát hành sau năm 2020 |
| | - **Đối với bản xuất web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera |
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Thiết bị di động (điện thoại thông minh/máy tính bảng) - Khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+ | **CPU** | - **Android:** SoC với CPU ARM hoặc x86 64-bit, có từ 3 lõi "hiệu năng" trở lên | | | | | | - *Ví dụ: Qualcomm Snapdragon 845, Samsung Exynos 9810* | | | | | | - **iOS:** SoC với CPU ARM 64-bit | | | |
| | - *Ví dụ: Apple A14 (iPhone 12)* |
++++++++++++++++++++++++++++++++++++++
| **GPU** | - **Trình kết xuất Forward+:** SoC có GPU với hỗ trợ đầy đủ Vulkan 1.2 hoặc | | | hỗ trợ Metal 3 (iOS/iPadOS) | | | | | | - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)* | | | | | | - **Trình kết xuất Mobile:** SoC có GPU với hỗ trợ đầy đủ Vulkan 1.2 hoặc | | | hỗ trợ Metal 3 (iOS/iPadOS) | | | | | | - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)* | | | | | | - **Trình kết xuất Compatibility:** SoC có GPU với hỗ trợ đầy đủ OpenGL ES 3.2 | | | |
| | - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)* |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **RAM** | - **Đối với bản xuất native:** 2 GB |
| | - **Đối với bản xuất web:** 4 GB |
++++++++++++++++++++++++++++++++++++++
| **Bộ nhớ lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm) |
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
| **Hệ điều hành** | - **Đối với bản xuất native:** Android 9.0, iOS 16.0 | | | - **Đối với bản xuất web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera, |
| | Samsung Internet |
++++++++++++++++++++++

.. note::

    Godot không sử dụng các phần mở rộng OpenGL/OpenGL ES được giới thiệu sau OpenGL 3.3/OpenGL ES 3.0, nhưng GPU hỗ trợ các phiên bản OpenGL/OpenGL ES mới hơn nhìn chung sẽ ít gặp sự cố trình điều khiển hơn.
