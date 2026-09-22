:allow_comments: False

.. _doc_system_requirements:

Yêu cầu hệ thống
================

Trang này nêu các yêu cầu hệ thống đối với editor và các project đã export. Các thông số kỹ thuật này chỉ nhằm mục đích tham khảo, nhưng bạn có thể xem chúng nếu đang muốn xây dựng hoặc nâng cấp một hệ thống để sử dụng Godot.

Godot editor
------------

Đây là các thông số **tối thiểu** cần thiết để chạy Godot editor và làm việc trên một project 2D hoặc 3D đơn giản:

PC để bàn hoặc laptop - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. When adjusting specifications, make sure to only mention hardware that can run the required OS version.
.. For example, the oldest Mac model that can run macOS 13 is the 2017 iMac,
.. so the x86 CPU requirement for macOS should not be set earlier than that.

+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **CPU**              | - **Windows:** CPU x86_32 hỗ trợ SSE2, CPU x86_64 hỗ trợ SSE4.2, CPU ARMv8                                                                                                                     |
|                      |                                                                                                                                                                                                |
|                      |   - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Snapdragon X Elite*                                                                                                                           |
|                      |                                                                                                                                                                                                |
|                      | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon)                                                                                                                                               |
|                      |                                                                                                                                                                                                |
|                      |   - *Ví dụ: CPU Intel thế hệ thứ 7 (Kaby Lake), Apple M1*                                                                                                                                      |
|                      |                                                                                                                                                                                                |
|                      | - **Linux:** CPU x86_32 hỗ trợ SSE2, CPU x86_64 hỗ trợ SSE4.2, CPU ARMv7 hoặc ARMv8                                                                                                            |
|                      |                                                                                                                                                                                                |
|                      |   - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Raspberry Pi 4*                                                                                                                               |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** Đồ họa tích hợp hỗ trợ đầy đủ Vulkan 1.0                                                                                                                              |
|                      |                                                                                                                                                                                                |
|                      |   - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*                                                                                                                  |
|                      |                                                                                                                                                                                                |
|                      | - **Mobile renderer:** Đồ họa tích hợp hỗ trợ đầy đủ Vulkan 1.0                                                                                                                                |
|                      |                                                                                                                                                                                                |
|                      |   - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*                                                                                                                  |
|                      |                                                                                                                                                                                                |
|                      | - **Compatibility renderer:** Đồ họa tích hợp hỗ trợ đầy đủ OpenGL 3.3                                                                                                                         |
|                      |                                                                                                                                                                                                |
|                      |   - *Ví dụ: Intel HD Graphics 2500 (Ivy Bridge), AMD Radeon R5 Graphics (Kaveri)*                                                                                                              |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **RAM**              | - **Native editor:** 4 GB                                                                                                                                                                      |
|                      | - **Web editor:** 8 GB                                                                                                                                                                         |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Storage**          | 200 MB (dùng cho executable, các file project và cache). Việc export project yêu cầu tải riêng các export template (tối đa 1,5 GB sau khi cài đặt, tùy thuộc vào các nền tảng đích được chọn). |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Operating system** | - **Native editor:** Windows 10, macOS 11 (Intel Mac, Compatibility), macOS 12 (Intel Mac, Forward+/Mobile), macOS 13 (Apple Silicon Mac), bản phân phối Linux phát hành sau năm 2018          |
|                      | - **Web editor:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit.                 |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

    Nếu CPU x86_64 của bạn không hỗ trợ SSE4.2, bạn vẫn có thể chạy executable Godot 32-bit, vốn chỉ yêu cầu SSE2 (tất cả CPU x86_64 đều hỗ trợ SSE2).

    Mặc dù được hỗ trợ trên Linux, chúng tôi không có yêu cầu tối thiểu chính thức cho việc chạy trên rv64 (RISC-V), ppc64 và ppc32 (PowerPC), cũng như loongarch64. Ngoài ra, bạn phải tự biên dịch editor cho nền tảng đó (cũng như các export template); hiện chưa có bản tải xuống chính thức nào được cung cấp. Bạn có thể tìm hướng dẫn biên dịch RISC-V trên trang :ref:`doc_compiling_for_linuxbsd`.

Thiết bị di động (smartphone/tablet) - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **CPU**                | - **Android:** SoC với CPU ARM hoặc x86 bất kỳ, 32-bit hoặc 64-bit                                                                                                                      |
|                        |                                                                                                                                                                                         |
|                        |   - *Ví dụ: Qualcomm Snapdragon 430, Samsung Exynos 5 Octa 5430*                                                                                                                        |
|                        |                                                                                                                                                                                         |
|                        | - **iOS:** *Không thể chạy trình chỉnh sửa*                                                                                                                                             |
+------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **GPU**                | - **Bộ kết xuất Forward+:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.0                                                                                                                   |
|                        |                                                                                                                                                                                         |
|                        |   - *Ví dụ: Qualcomm Adreno 505, Mali-G71 MP2*                                                                                                                                          |
|                        |                                                                                                                                                                                         |
|                        | - **Bộ kết xuất Mobile:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.0                                                                                                                     |
|                        |                                                                                                                                                                                         |
|                        |   - *Ví dụ: Qualcomm Adreno 505, Mali-G71 MP2*                                                                                                                                          |
|                        |                                                                                                                                                                                         |
|                        | - **Bộ kết xuất Compatibility:** SoC tích hợp GPU hỗ trợ đầy đủ OpenGL ES 3.0                                                                                                           |
|                        |                                                                                                                                                                                         |
|                        |   - *Ví dụ: Qualcomm Adreno 306, Mali-T628 MP6*                                                                                                                                         |
+------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **RAM**                | - **Trình chỉnh sửa native:** 3 GB                                                                                                                                                      |
|                        | - **Trình chỉnh sửa web:** 6 GB                                                                                                                                                         |
+------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Dung lượng lưu trữ** | 200 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm). Để export dự án, cần tải riêng các export template (tối đa 1.5 GB sau khi cài đặt, tùy thuộc vào các nền tảng đích được chọn). |
+------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Hệ điều hành**       | - **Trình chỉnh sửa native:** Android 7.0 (Compatibility) hoặc Android 9.0 (Forward+/Mobile)                                                                                            |
|                        | - **Trình chỉnh sửa web:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit. |
+------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Đây là các thông số **được khuyến nghị** để có trải nghiệm mượt mà với trình chỉnh sửa Godot trong một dự án 2D hoặc 3D đơn giản:

PC để bàn hoặc laptop - Được khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------+-----------------------------------------------------------------------------------------------------+
| **CPU**                | - **Windows:** CPU x86_64 hỗ trợ SSE4.2, với ít nhất 4 lõi vật lý, CPU ARMv8                        |
|                        |                                                                                                     |
|                        |   - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite*                              |
|                        |                                                                                                     |
|                        | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon)                                                    |
|                        |                                                                                                     |
|                        |   - *Ví dụ: Intel Core i5-8500, Apple M1*                                                           |
|                        |                                                                                                     |
|                        | - **Linux:** CPU x86_64 hỗ trợ SSE4.2, CPU ARMv7 hoặc ARMv8                                         |
|                        |                                                                                                     |
|                        |   - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 được ép xung*                     |
+------------------------+-----------------------------------------------------------------------------------------------------+
| **GPU**                | - **Bộ kết xuất Forward+:** Card đồ họa rời hỗ trợ đầy đủ Vulkan 1.2                                |
|                        |                                                                                                     |
|                        |   - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                          |
|                        |                                                                                                     |
|                        | - **Bộ kết xuất Mobile:** Card đồ họa rời hỗ trợ đầy đủ Vulkan 1.2                                  |
|                        |                                                                                                     |
|                        |   - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                          |
|                        |                                                                                                     |
|                        | - **Bộ kết xuất tương thích:** Đồ họa chuyên dụng với hỗ trợ OpenGL 4.6 đầy đủ                      |
|                        |                                                                                                     |
|                        |   - *Ví dụ: NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0)*                          |
+------------------------+-----------------------------------------------------------------------------------------------------+
| **RAM**                | - **Trình chỉnh sửa native:** 8 GB                                                                  |
|                        | - **Trình chỉnh sửa web:** 12 GB                                                                    |
+------------------------+-----------------------------------------------------------------------------------------------------+
| **Dung lượng lưu trữ** | 2 GB (dùng cho tệp thực thi, tệp dự án, tất cả export template và bộ nhớ đệm)                       |
+------------------------+-----------------------------------------------------------------------------------------------------+
| **Hệ điều hành**       | - **Trình chỉnh sửa native:** Windows 11, macOS 14, bản phân phối Linux được phát hành sau năm 2020 |
|                        | - **Trình chỉnh sửa web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera              |
+------------------------+-----------------------------------------------------------------------------------------------------+

Thiết bị di động (điện thoại thông minh/máy tính bảng) - Khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------+----------------------------------------------------------------------------------------------------------+
| **CPU**                | - **Android:** SoC có CPU ARM 64-bit hoặc x86, với từ 3 lõi "hiệu năng" trở lên                          |
|                        |                                                                                                          |
|                        |   - *Ví dụ: Qualcomm Snapdragon 845, Samsung Exynos 9810*                                                |
|                        |                                                                                                          |
|                        | - **iOS:** *Không thể chạy trình chỉnh sửa*                                                              |
+------------------------+----------------------------------------------------------------------------------------------------------+
| **GPU**                | - **Bộ kết xuất Forward+:** SoC tích hợp GPU với hỗ trợ Vulkan 1.2 đầy đủ                                |
|                        |                                                                                                          |
|                        |   - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18*                                                          |
|                        |                                                                                                          |
|                        | - **Bộ kết xuất di động:** SoC tích hợp GPU với hỗ trợ Vulkan 1.2 đầy đủ                                 |
|                        |                                                                                                          |
|                        |   - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18*                                                          |
|                        |                                                                                                          |
|                        | - **Bộ kết xuất tương thích:** SoC tích hợp GPU với hỗ trợ OpenGL ES 3.2 đầy đủ                          |
|                        |                                                                                                          |
|                        |   - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18*                                                          |
+------------------------+----------------------------------------------------------------------------------------------------------+
| **RAM**                | - **Trình chỉnh sửa native:** 6 GB                                                                       |
|                        | - **Trình chỉnh sửa web:** 8 GB                                                                          |
+------------------------+----------------------------------------------------------------------------------------------------------+
| **Dung lượng lưu trữ** | 2 GB (dùng cho tệp thực thi, tệp dự án, tất cả export template và bộ nhớ đệm)                            |
+------------------------+----------------------------------------------------------------------------------------------------------+
| **Hệ điều hành**       | - **Trình chỉnh sửa native:** Android 11.0                                                               |
|                        | - **Trình chỉnh sửa web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera, Samsung Internet |
+------------------------+----------------------------------------------------------------------------------------------------------+

Dự án Godot đã export
---------------------

.. warning::

    Các yêu cầu dưới đây là mức cơ bản cho một dự án 2D hoặc 3D **đơn giản**, có scripting cơ bản và ít hiệu ứng hình ảnh. Yêu cầu về CPU, GPU, RAM và bộ nhớ lưu trữ sẽ thay đổi đáng kể tùy thuộc vào phạm vi dự án, renderer, độ phân giải viewport và các thiết lập đồ họa được chọn. Các chương trình khác đang chạy trên hệ thống trong khi dự án hoạt động cũng sẽ cạnh tranh tài nguyên, bao gồm RAM và video RAM.

    Bạn nên tự kiểm thử trên phần cứng cấp thấp để đảm bảo dự án chạy ở tốc độ mong muốn. Để cung cấp khả năng mở rộng cho phần cứng cấp thấp, bạn cũng cần thêm `menu tùy chọn đồ họa <https://github.com/godotengine/godot-demo-projects/tree/master/3d/graphics_settings>`__ vào dự án.

Đây là các thông số **tối thiểu** cần thiết để chạy một dự án 2D hoặc 3D đơn giản được export bằng Godot:

PC để bàn hoặc laptop - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. When adjusting specifications, make sure to only mention hardware that can run the required OS version.
.. For example, the oldest Mac model that can run macOS 13 is the 2017 iMac,
.. so the x86 CPU requirement for macOS should not be set earlier than that.

+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **CPU**              | - **Windows:** CPU x86_32 có hỗ trợ SSE2, CPU x86_64 có hỗ trợ SSE4.2, CPU ARMv8                                                                                                                           |
|                      |                                                                                                                                                                                                            |
|                      |   - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Snapdragon X Elite*                                                                                                                                       |
|                      |                                                                                                                                                                                                            |
|                      | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon)                                                                                                                                                           |
|                      |                                                                                                                                                                                                            |
|                      |   - *Ví dụ: CPU Intel thế hệ thứ 7 (Kaby Lake), Apple M1*                                                                                                                                                  |
|                      |                                                                                                                                                                                                            |
|                      | - **Linux:** CPU x86_32 có hỗ trợ SSE2, CPU x86_64 có hỗ trợ SSE4.2, CPU ARMv7 hoặc ARMv8                                                                                                                  |
|                      |                                                                                                                                                                                                            |
|                      |   - *Ví dụ: Intel Core 2 Duo E8200, AMD FX-4100, Raspberry Pi 4*                                                                                                                                           |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** Đồ họa tích hợp có hỗ trợ đầy đủ Vulkan 1.0, hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (mức tính năng 12_0) (Windows)                                                        |
|                      |                                                                                                                                                                                                            |
|                      |   - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*                                                                                                                              |
|                      |                                                                                                                                                                                                            |
|                      | - **Mobile renderer:** Đồ họa tích hợp có hỗ trợ đầy đủ Vulkan 1.0, hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (mức tính năng 12_0) (Windows)                                                          |
|                      |                                                                                                                                                                                                            |
|                      |   - *Ví dụ: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*                                                                                                                              |
|                      |                                                                                                                                                                                                            |
|                      | - **Compatibility renderer:** Đồ họa tích hợp có hỗ trợ đầy đủ OpenGL 3.3 hoặc hỗ trợ Direct3D 11 (Windows).                                                                                               |
|                      |                                                                                                                                                                                                            |
|                      |   - *Ví dụ: Intel HD Graphics 2500 (Ivy Bridge), AMD Radeon R5 Graphics (Kaveri)*                                                                                                                          |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **RAM**              | - **Đối với native exports:** 2 GB                                                                                                                                                                         |
|                      | - **Đối với web exports:** 4 GB                                                                                                                                                                            |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Storage**          | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm)                                                                                                                                                    |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Operating system** | - **Đối với native exports:** Windows 10, macOS 11 (máy Mac Intel, Compatibility), macOS 12 (máy Mac Intel, Forward+/Mobile), macOS 13 (máy Mac Apple Silicon), bản phân phối Linux phát hành sau năm 2018 |
|                      | - **Đối với web exports:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các biến thể (bao gồm ESR), Chrome và các biến thể Chromium, Safari và các biến thể WebKit.                    |
+----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Thiết bị di động (smartphone/tablet) - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **CPU**                | - **Android:** SoC với CPU ARM hoặc x86 bất kỳ, 32-bit hoặc 64-bit                                                                                                                                                                        |
|                        |                                                                                                                                                                                                                                           |
|                        |   - *Ví dụ: Qualcomm Snapdragon 430, Samsung Exynos 5 Octa 5430*                                                                                                                                                                          |
|                        |                                                                                                                                                                                                                                           |
|                        | - **iOS:** SoC với CPU ARM 64-bit                                                                                                                                                                                                         |
|                        |                                                                                                                                                                                                                                           |
|                        |   - *Ví dụ: Apple A9 (iPhone 6S)*                                                                                                                                                                                                         |
+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **GPU**                | - **Bộ kết xuất Forward+:** SoC có GPU hỗ trợ đầy đủ Vulkan 1.0 hoặc hỗ trợ Metal 3 (iOS/iPadOS)                                                                                                                                          |
|                        |                                                                                                                                                                                                                                           |
|                        |   - *Ví dụ (Vulkan): Qualcomm Adreno 505, Mali-G71 MP2, Apple A12 (iPhone XR/XS)*                                                                                                                                                         |
|                        |   - *Ví dụ (Metal): Apple A12 (iPhone XR/XS)*                                                                                                                                                                                             |
|                        |                                                                                                                                                                                                                                           |
|                        | - **Bộ kết xuất Mobile:** SoC có GPU hỗ trợ đầy đủ Vulkan 1.0 hoặc hỗ trợ Metal 3 (iOS/iPadOS)                                                                                                                                            |
|                        |                                                                                                                                                                                                                                           |
|                        |   - *Ví dụ (Vulkan): Qualcomm Adreno 505, Mali-G71 MP2, Apple A12 (iPhone XR/XS)*                                                                                                                                                         |
|                        |   - *Ví dụ (Metal): Apple A12 (iPhone XR/XS)*                                                                                                                                                                                             |
|                        |                                                                                                                                                                                                                                           |
|                        | - **Bộ kết xuất Compatibility:** SoC tích hợp GPU hỗ trợ đầy đủ OpenGL ES 3.0                                                                                                                                                             |
|                        |                                                                                                                                                                                                                                           |
|                        |   - *Ví dụ: Qualcomm Adreno 306, Mali-T628 MP6, Apple A9 (iPhone 6S)*                                                                                                                                                                     |
+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **RAM**                | - **Đối với bản export native:** 1 GB                                                                                                                                                                                                     |
|                        | - **Đối với bản export web:** 2 GB                                                                                                                                                                                                        |
+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Dung lượng lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm)                                                                                                                                                                                   |
+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| **Hệ điều hành**       | - **Đối với bản export native:** Android 7.0 (Compatibility), Android 9.0 (Forward+/Mobile), iOS 15.0 (Forward+/Mobile với Vulkan), iOS 16.0 (Forward+/Mobile với Metal)                                                                  |
|                        | - **Đối với bản export web:** Các phiên bản gần đây của những trình duyệt phổ biến: Firefox và các trình duyệt phái sinh (bao gồm ESR), Chrome và các trình duyệt phái sinh của Chromium, Safari và các trình duyệt phái sinh của WebKit. |
+------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Đây là các thông số **được khuyến nghị** để có trải nghiệm mượt mà với một dự án 2D hoặc 3D đơn giản được export bằng Godot:

PC để bàn hoặc laptop - Được khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
| **CPU**                | - **Windows:** CPU x86_64 hỗ trợ SSE4.2, với ít nhất 4 lõi vật lý, CPU ARMv8                                                                |
|                        |                                                                                                                                             |
|                        |   - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite*                                                                      |
|                        |                                                                                                                                             |
|                        | - **macOS:** CPU x86_64 hoặc ARM (Apple Silicon)                                                                                            |
|                        |                                                                                                                                             |
|                        |   - *Ví dụ: Intel Core i5-8500, Apple M1*                                                                                                   |
|                        |                                                                                                                                             |
|                        | - **Linux:** CPU x86_64 hỗ trợ SSE4.2, có từ 4 lõi vật lý trở lên, CPU ARMv7 hoặc ARMv8                                                     |
|                        |                                                                                                                                             |
|                        |   - *Ví dụ: Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 được ép xung*                                                             |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
| **GPU**                | - **Forward+ renderer:** Đồ họa rời hỗ trợ đầy đủ Vulkan 1.2, hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (cấp tính năng 12_0) (Windows) |
|                        |                                                                                                                                             |
|                        |   - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                                                                  |
|                        |                                                                                                                                             |
|                        | - **Mobile renderer:** Đồ họa rời hỗ trợ đầy đủ Vulkan 1.2, hỗ trợ Metal 3 (macOS) hoặc hỗ trợ Direct3D 12 (cấp tính năng 12_0) (Windows)   |
|                        |                                                                                                                                             |
|                        |   - *Ví dụ: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                                                                  |
|                        |                                                                                                                                             |
|                        | - **Bộ kết xuất tương thích:** Đồ họa chuyên dụng với hỗ trợ OpenGL 4.6 đầy đủ                                                              |
|                        |                                                                                                                                             |
|                        |   - *Ví dụ: NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0)*                                                                  |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
| **RAM**                | - **Đối với native exports:** 4 GB                                                                                                          |
|                        | - **Đối với web exports:** 8 GB                                                                                                             |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
| **Dung lượng lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm)                                                                                     |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+
| **Hệ điều hành**       | - **Đối với native exports:** Windows 11, macOS 14, bản phân phối Linux phát hành sau năm 2020                                              |
|                        | - **Đối với web exports:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera                                                      |
+------------------------+---------------------------------------------------------------------------------------------------------------------------------------------+

Thiết bị di động (điện thoại thông minh/máy tính bảng) - Khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+------------------------+-----------------------------------------------------------------------------------------------------------+
| **CPU**                | - **Android:** SoC có CPU ARM 64-bit hoặc x86, với từ 3 lõi "hiệu năng" trở lên                           |
|                        |                                                                                                           |
|                        |   - *Ví dụ: Qualcomm Snapdragon 845, Samsung Exynos 9810*                                                 |
|                        |                                                                                                           |
|                        | - **iOS:** SoC có CPU ARM 64-bit                                                                          |
|                        |                                                                                                           |
|                        |   - *Ví dụ: Apple A14 (iPhone 12)*                                                                        |
+------------------------+-----------------------------------------------------------------------------------------------------------+
| **GPU**                | - **Forward+ renderer:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.2 hoặc hỗ trợ Metal 3 (iOS/iPadOS)       |
|                        |                                                                                                           |
|                        |   - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)*                                    |
|                        |                                                                                                           |
|                        | - **Mobile renderer:** SoC tích hợp GPU hỗ trợ đầy đủ Vulkan 1.2 hoặc hỗ trợ Metal 3 (iOS/iPadOS)         |
|                        |                                                                                                           |
|                        |   - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)*                                    |
|                        |                                                                                                           |
|                        | - **Bộ kết xuất tương thích:** SoC tích hợp GPU với hỗ trợ OpenGL ES 3.2 đầy đủ                           |
|                        |                                                                                                           |
|                        |   - *Ví dụ: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)*                                    |
+------------------------+-----------------------------------------------------------------------------------------------------------+
| **RAM**                | - **Đối với native exports:** 2 GB                                                                        |
|                        | - **Đối với bản xuất web:** 4 GB                                                                          |
+------------------------+-----------------------------------------------------------------------------------------------------------+
| **Dung lượng lưu trữ** | 150 MB (dùng cho tệp thực thi, tệp dự án và bộ nhớ đệm)                                                   |
+------------------------+-----------------------------------------------------------------------------------------------------------+
| **Hệ điều hành**       | - **Đối với bản xuất native:** Android 9.0, iOS 16.0                                                      |
|                        | - **Đối với bản xuất web:** Phiên bản mới nhất của Firefox, Chrome, Edge, Safari, Opera, Samsung Internet |
+------------------------+-----------------------------------------------------------------------------------------------------------+

.. note::

    Godot không sử dụng các phần mở rộng OpenGL/OpenGL ES được giới thiệu sau OpenGL 3.3/OpenGL ES 3.0, nhưng GPU hỗ trợ các phiên bản OpenGL/OpenGL ES mới hơn nhìn chung có ít vấn đề về driver hơn.
