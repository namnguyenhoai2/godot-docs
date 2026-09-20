:allow_comments: False

.. _doc_system_requirements:

Yêu cầu hệ thống
================

Trang này nêu các yêu cầu hệ thống đối với trình chỉnh sửa và các dự án được xuất. Các thông số kỹ thuật này chỉ nhằm mục đích tham khảo, nhưng bạn có thể xem chúng nếu muốn xây dựng hoặc nâng cấp một hệ thống để sử dụng Godot.

Trình chỉnh sửa Godot
---------------------

Đây là các thông số kỹ thuật **tối thiểu** cần thiết để chạy trình chỉnh sửa Godot và làm việc trên một dự án 2D hoặc 3D đơn giản:

PC để bàn hoặc laptop - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. Khi điều chỉnh các thông số kỹ thuật, hãy chỉ đề cập đến phần cứng có thể chạy phiên bản OS bắt buộc. .. Ví dụ, mẫu Mac cũ nhất có thể chạy macOS 13 là iMac 2017, .. vì vậy không nên đặt yêu cầu CPU x86 cho macOS ở thời điểm sớm hơn mẫu này.

+----------------------+-----------------------------------------------------------------------------------------+
| **CPU**              | - **Windows:** x86_32 CPU with SSE2 support, x86_64 CPU with SSE4.2 support, ARMv8 CPU  |
|                      |                                                                                         |
|                      |   - *Example: Intel Core 2 Duo E8200, AMD FX-4100, Snapdragon X Elite*                  |
|                      |                                                                                         |
|                      | - **macOS:** x86_64 or ARM CPU (Apple Silicon)                                          |
|                      |                                                                                         |
|                      |   - *Example: Intel 7th Gen (Kaby Lake) CPU, Apple M1*                                  |
|                      |                                                                                         |
|                      | - **Linux:** x86_32 CPU with SSE2 support, x86_64 CPU with SSE4.2 support, ARMv7 or     |
|                      |   ARMv8 CPU                                                                             |
|                      |                                                                                         |
|                      |   - *Example: Intel Core 2 Duo E8200, AMD FX-4100, Raspberry Pi 4*                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** Integrated graphics with full Vulkan 1.0 support               |
|                      |                                                                                         |
|                      |   - *Example: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*         |
|                      |                                                                                         |
|                      | - **Mobile renderer:** Integrated graphics with full Vulkan 1.0 support                 |
|                      |                                                                                         |
|                      |   - *Example: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*         |
|                      |                                                                                         |
|                      | - **Compatibility renderer:** Integrated graphics with full OpenGL 3.3 support          |
|                      |                                                                                         |
|                      |   - *Example: Intel HD Graphics 2500 (Ivy Bridge), AMD Radeon R5 Graphics (Kaveri)*     |
+----------------------+-----------------------------------------------------------------------------------------+
| **RAM**              | - **Native editor:** 4 GB                                                               |
|                      | - **Web editor:** 8 GB                                                                  |
+----------------------+-----------------------------------------------------------------------------------------+
| **Storage**          | 200 MB (used for the executable, project files, and cache).                             |
|                      | Exporting projects requires downloading export templates separately                     |
|                      | (up to 1.5 GB after installation, depending on the target platforms chosen).            |
+----------------------+-----------------------------------------------------------------------------------------+
| **Operating system** | - **Native editor:** Windows 10, macOS 11 (Intel Macs, Compatibility), macOS 12 (Intel  |
|                      |   Macs, Forward+/Mobile), macOS 13 (Apple Silicon Macs), Linux distribution released    |
|                      |   after 2018                                                                            |
|                      | - **Web editor:** Recent versions of mainstream browsers: Firefox and derivatives       |
|                      |   (including ESR), Chrome and Chromium derivatives, Safari and WebKit derivatives.      |
+----------------------+-----------------------------------------------------------------------------------------+

.. note::

    Nếu CPU x86_64 của bạn không hỗ trợ SSE4.2, bạn vẫn có thể chạy tệp thực thi Godot 32-bit, vốn chỉ yêu cầu SSE2 (tất cả CPU x86_64 đều hỗ trợ SSE2).

    Mặc dù được hỗ trợ trên Linux, chúng tôi không có yêu cầu tối thiểu chính thức để chạy trên rv64 (RISC-V), ppc64 & ppc32 (PowerPC) và loongarch64. Ngoài ra, bạn phải tự biên dịch trình chỉnh sửa cho nền tảng đó (cũng như các export template); hiện chưa có bản tải xuống chính thức. Bạn có thể tìm thấy hướng dẫn biên dịch RISC-V trên trang :ref:`doc_compiling_for_linuxbsd`.

Thiết bị di động (smartphone/tablet) - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+
| **CPU**              | - **Android:** SoC with any 32-bit or 64-bit ARM or x86 CPU                             |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Snapdragon 430, Samsung Exynos 5 Octa 5430*                      |
|                      |                                                                                         |
|                      | - **iOS:** *Cannot run the editor*                                                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** SoC featuring GPU with full Vulkan 1.0 support                 |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 505, Mali-G71 MP2*                                        |
|                      |                                                                                         |
|                      | - **Mobile renderer:** SoC featuring GPU with full Vulkan 1.0 support                   |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 505, Mali-G71 MP2*                                        |
|                      |                                                                                         |
|                      | - **Compatibility renderer:** SoC featuring GPU with full OpenGL ES 3.0 support         |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 306, Mali-T628 MP6*                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **RAM**              | - **Native editor:** 3 GB                                                               |
|                      | - **Web editor:** 6 GB                                                                  |
+----------------------+-----------------------------------------------------------------------------------------+
| **Storage**          | 200 MB (used for the executable, project files, and cache).                             |
|                      | Exporting projects requires downloading export templates separately                     |
|                      | (up to 1.5 GB after installation, depending on the target platforms chosen).            |
+----------------------+-----------------------------------------------------------------------------------------+
| **Operating system** | - **Native editor:** Android 7.0 (Compatibility) or Android 9.0 (Forward+/Mobile)       |
|                      | - **Web editor:** Recent versions of mainstream browsers: Firefox and derivatives       |
|                      |   (including ESR), Chrome and Chromium derivatives, Safari and WebKit derivatives.      |
+----------------------+-----------------------------------------------------------------------------------------+

Đây là các thông số kỹ thuật **được khuyến nghị** để có trải nghiệm mượt mà với trình chỉnh sửa Godot trên một dự án 2D hoặc 3D đơn giản:

PC để bàn hoặc laptop - Được khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+---------------------------------------------------------------------------------------------+
| **CPU**              | - **Windows:** x86_64 CPU with SSE4.2 support, with 4 physical cores or more, ARMv8 CPU     |
|                      |                                                                                             |
|                      |   - *Example: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite*                    |
|                      |                                                                                             |
|                      | - **macOS:** x86_64 or ARM CPU (Apple Silicon)                                              |
|                      |                                                                                             |
|                      |   - *Example: Intel Core i5-8500, Apple M1*                                                 |
|                      |                                                                                             |
|                      | - **Linux:** x86_64 CPU with SSE4.2 support, ARMv7 or ARMv8 CPU                             |
|                      |                                                                                             |
|                      |   - *Example: Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 with overclocking*      |
+----------------------+---------------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** Dedicated graphics with full Vulkan 1.2 support                    |
|                      |                                                                                             |
|                      |   - *Example: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                |
|                      |                                                                                             |
|                      | - **Mobile renderer:** Dedicated graphics with full Vulkan 1.2 support                      |
|                      |                                                                                             |
|                      |   - *Example: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                |
|                      |                                                                                             |
|                      | - **Compatibility renderer:** Dedicated graphics with full OpenGL 4.6 support               |
|                      |                                                                                             |
|                      |   - *Example: NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0)*                |
+----------------------+---------------------------------------------------------------------------------------------+
| **RAM**              | - **Native editor:** 8 GB                                                                   |
|                      | - **Web editor:** 12 GB                                                                     |
+----------------------+---------------------------------------------------------------------------------------------+
| **Storage**          | 2 GB (used for the executable, project files, all export templates, and cache)              |
+----------------------+---------------------------------------------------------------------------------------------+
| **Operating system** | - **Native editor:** Windows 11, macOS 14, Linux distribution released after 2020           |
|                      | - **Web editor:** Latest version of Firefox, Chrome, Edge, Safari, Opera                    |
+----------------------+---------------------------------------------------------------------------------------------+

Thiết bị di động (smartphone/tablet) - Được khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+
| **CPU**              | - **Android:** SoC with 64-bit ARM or x86 CPU, with 3 "performance" cores or more       |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Snapdragon 845, Samsung Exynos 9810*                             |
|                      |                                                                                         |
|                      | - **iOS:** *Cannot run the editor*                                                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** SoC featuring GPU with full Vulkan 1.2 support                 |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 630, Mali-G72 MP18*                                       |
|                      |                                                                                         |
|                      | - **Mobile renderer:** SoC featuring GPU with full Vulkan 1.2 support                   |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 630, Mali-G72 MP18*                                       |
|                      |                                                                                         |
|                      | - **Compatibility renderer:** SoC featuring GPU with full OpenGL ES 3.2 support         |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 630, Mali-G72 MP18*                                       |
+----------------------+-----------------------------------------------------------------------------------------+
| **RAM**              | - **Native editor:** 6 GB                                                               |
|                      | - **Web editor:** 8 GB                                                                  |
+----------------------+-----------------------------------------------------------------------------------------+
| **Storage**          | 2 GB (used for the executable, project files, all export templates, and cache)          |
+----------------------+-----------------------------------------------------------------------------------------+
| **Operating system** | - **Native editor:** Android 11.0                                                       |
|                      | - **Web editor:** Latest version of Firefox, Chrome, Edge, Safari, Opera,               |
|                      |   Samsung Internet                                                                      |
+----------------------+-----------------------------------------------------------------------------------------+

Dự án Godot được xuất
---------------------

.. warning::

    Các yêu cầu dưới đây là mức cơ sở cho một dự án 2D hoặc 3D **đơn giản**, với scripting cơ bản và ít hiệu ứng hình ảnh. Yêu cầu về CPU, GPU, RAM và dung lượng lưu trữ sẽ thay đổi đáng kể tùy thuộc vào phạm vi dự án, renderer, độ phân giải viewport và các thiết lập đồ họa được chọn. Những chương trình khác đang chạy trên hệ thống trong khi dự án hoạt động cũng sẽ cạnh tranh tài nguyên, bao gồm RAM và video RAM.

    Bạn rất nên tự kiểm thử trên phần cứng cấp thấp để đảm bảo dự án chạy ở tốc độ mong muốn. Để cung cấp khả năng mở rộng cho phần cứng cấp thấp, bạn cũng sẽ cần thêm `trình đơn tùy chọn đồ họa <https://github.com/godotengine/godot-demo-projects/tree/master/3d/graphics_settings>`__ vào dự án.

Đây là các thông số kỹ thuật **tối thiểu** cần thiết để chạy một dự án 2D hoặc 3D đơn giản được xuất bằng Godot:

PC để bàn hoặc laptop - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. Khi điều chỉnh các thông số kỹ thuật, hãy chỉ đề cập đến phần cứng có thể chạy phiên bản OS bắt buộc. .. Ví dụ, mẫu Mac cũ nhất có thể chạy macOS 13 là iMac 2017, .. vì vậy không nên đặt yêu cầu CPU x86 cho macOS ở thời điểm sớm hơn mẫu này.

+----------------------+-----------------------------------------------------------------------------------------+
| **CPU**              | - **Windows:** x86_32 CPU with SSE2 support, x86_64 CPU with SSE4.2 support,            |
|                      |   ARMv8 CPU                                                                             |
|                      |                                                                                         |
|                      |   - *Example: Intel Core 2 Duo E8200, AMD FX-4100, Snapdragon X Elite*                  |
|                      |                                                                                         |
|                      | - **macOS:** x86_64 or ARM CPU (Apple Silicon)                                          |
|                      |                                                                                         |
|                      |   - *Example: Intel 7th Gen (Kaby Lake) CPU, Apple M1*                                  |
|                      |                                                                                         |
|                      | - **Linux:** x86_32 CPU with SSE2 support, x86_64 CPU with SSE4.2 support,              |
|                      |   ARMv7 or ARMv8 CPU                                                                    |
|                      |                                                                                         |
|                      |   - *Example: Intel Core 2 Duo E8200, AMD FX-4100, Raspberry Pi 4*                      |
+----------------------+-----------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** Integrated graphics with full Vulkan 1.0 support,              |
|                      |   Metal 3 support (macOS) or Direct3D 12 (12_0 feature level) support (Windows)         |
|                      |                                                                                         |
|                      |   - *Example: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*         |
|                      |                                                                                         |
|                      | - **Mobile renderer:** Integrated graphics with full Vulkan 1.0 support,                |
|                      |   Metal 3 support (macOS) or Direct3D 12 (12_0 feature level) support (Windows)         |
|                      |                                                                                         |
|                      |   - *Example: Intel HD Graphics 510 (Skylake), AMD Radeon R5 Graphics (Kaveri)*         |
|                      |                                                                                         |
|                      | - **Compatibility renderer:** Integrated graphics with full OpenGL 3.3 support          |
|                      |   or Direct3D 11 support (Windows).                                                     |
|                      |                                                                                         |
|                      |   - *Example: Intel HD Graphics 2500 (Ivy Bridge), AMD Radeon R5 Graphics (Kaveri)*     |
+----------------------+-----------------------------------------------------------------------------------------+
| **RAM**              | - **For native exports:** 2 GB                                                          |
|                      | - **For web exports:** 4 GB                                                             |
+----------------------+-----------------------------------------------------------------------------------------+
| **Storage**          | 150 MB (used for the executable, project files, and cache)                              |
+----------------------+-----------------------------------------------------------------------------------------+
| **Operating system** | - **For native exports:** Windows 10, macOS 11 (Intel Macs, Compatibility), macOS 12    |
|                      |   (Intel Macs, Forward+/Mobile), macOS 13 (Apple Silicon Macs), Linux distribution      |
|                      |   released after 2018                                                                   |
|                      | - **For web exports:** Recent versions of mainstream browsers: Firefox and derivatives  |
|                      |   (including ESR), Chrome and Chromium derivatives, Safari and WebKit derivatives.      |
+----------------------+-----------------------------------------------------------------------------------------+

Thiết bị di động (smartphone/tablet) - Tối thiểu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+
| **CPU**              | - **Android:** SoC with any 32-bit or 64-bit ARM or x86 CPU                             |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Snapdragon 430, Samsung Exynos 5 Octa 5430*                      |
|                      |                                                                                         |
|                      | - **iOS:** SoC with 64-bit ARM CPU                                                      |
|                      |                                                                                         |
|                      |   - *Example: Apple A9 (iPhone 6S)*                                                     |
+----------------------+-----------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** SoC featuring GPU with full Vulkan 1.0 support, or             |
|                      |   Metal 3 support (iOS/iPadOS)                                                          |
|                      |                                                                                         |
|                      |   - *Example (Vulkan): Qualcomm Adreno 505, Mali-G71 MP2, Apple A12 (iPhone XR/XS)*     |
|                      |   - *Example (Metal): Apple A12 (iPhone XR/XS)*                                         |
|                      |                                                                                         |
|                      | - **Mobile renderer:** SoC featuring GPU with full Vulkan 1.0 support, or               |
|                      |   Metal 3 support (iOS/iPadOS)                                                          |
|                      |                                                                                         |
|                      |   - *Example (Vulkan): Qualcomm Adreno 505, Mali-G71 MP2, Apple A12 (iPhone XR/XS)*     |
|                      |   - *Example (Metal): Apple A12 (iPhone XR/XS)*                                         |
|                      |                                                                                         |
|                      | - **Compatibility renderer:** SoC featuring GPU with full OpenGL ES 3.0 support         |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 306, Mali-T628 MP6, Apple A9 (iPhone 6S)*                 |
+----------------------+-----------------------------------------------------------------------------------------+
| **RAM**              | - **For native exports:** 1 GB                                                          |
|                      | - **For web exports:** 2 GB                                                             |
+----------------------+-----------------------------------------------------------------------------------------+
| **Storage**          | 150 MB (used for the executable, project files, and cache)                              |
+----------------------+-----------------------------------------------------------------------------------------+
| **Operating system** | - **For native exports:** Android 7.0 (Compatibility), Android 9.0 (Forward+/Mobile),   |
|                      |   iOS 15.0 (Forward+/Mobile with Vulkan), iOS 16.0 (Forward+/Mobile with Metal)         |
|                      | - **For web exports:** Recent versions of mainstream browsers: Firefox and derivatives  |
|                      |   (including ESR), Chrome and Chromium derivatives, Safari and WebKit derivatives.      |
+----------------------+-----------------------------------------------------------------------------------------+

Đây là các thông số kỹ thuật **được khuyến nghị** để có trải nghiệm mượt mà với một dự án 2D hoặc 3D đơn giản được xuất bằng Godot:

PC để bàn hoặc laptop - Được khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+----------------------------------------------------------------------------------------------+
| **CPU**              | - **Windows:** x86_64 CPU with SSE4.2 support, with 4 physical cores or more, ARMv8 CPU      |
|                      |                                                                                              |
|                      |   - *Example: Intel Core i5-6600K, AMD Ryzen 5 1600, Snapdragon X Elite*                     |
|                      |                                                                                              |
|                      | - **macOS:** x86_64 or ARM CPU (Apple Silicon)                                               |
|                      |                                                                                              |
|                      |   - *Example: Intel Core i5-8500, Apple M1*                                                  |
|                      |                                                                                              |
|                      | - **Linux:** x86_64 CPU with SSE4.2 support, with 4 physical cores or more,                  |
|                      |   ARMv7 or ARMv8 CPU                                                                         |
|                      |                                                                                              |
|                      |   - *Example: Intel Core i5-6600K, AMD Ryzen 5 1600, Raspberry Pi 5 with overclocking*       |
+----------------------+----------------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** Dedicated graphics with full Vulkan 1.2 support,                    |
|                      |   Metal 3 support (macOS), or Direct3D 12 (12_0 feature level) support (Windows)             |
|                      |                                                                                              |
|                      |   - *Example: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                 |
|                      |                                                                                              |
|                      | - **Mobile renderer:** Dedicated graphics with full Vulkan 1.2 support,                      |
|                      |   Metal 3 support (macOS), or Direct3D 12 (12_0 feature level) support (Windows)             |
|                      |                                                                                              |
|                      |   - *Example: NVIDIA GeForce GTX 1050 (Pascal), AMD Radeon RX 460 (GCN 4.0)*                 |
|                      |                                                                                              |
|                      | - **Compatibility renderer:** Dedicated graphics with full OpenGL 4.6 support                |
|                      |                                                                                              |
|                      |   - *Example: NVIDIA GeForce GTX 650 (Kepler), AMD Radeon HD 7750 (GCN 1.0)*                 |
+----------------------+----------------------------------------------------------------------------------------------+
| **RAM**              | - **For native exports:** 4 GB                                                               |
|                      | - **For web exports:** 8 GB                                                                  |
+----------------------+----------------------------------------------------------------------------------------------+
| **Storage**          | 150 MB (used for the executable, project files, and cache)                                   |
+----------------------+----------------------------------------------------------------------------------------------+
| **Operating system** | - **For native exports:** Windows 11, macOS 14, Linux distribution released after 2020       |
|                      | - **For web exports:** Latest version of Firefox, Chrome, Edge, Safari, Opera                |
+----------------------+----------------------------------------------------------------------------------------------+

Thiết bị di động (smartphone/tablet) - Được khuyến nghị
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------+-----------------------------------------------------------------------------------------+
| **CPU**              | - **Android:** SoC with 64-bit ARM or x86 CPU, with 3 "performance" cores or more       |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Snapdragon 845, Samsung Exynos 9810*                             |
|                      |                                                                                         |
|                      | - **iOS:** SoC with 64-bit ARM CPU                                                      |
|                      |                                                                                         |
|                      |   - *Example: Apple A14 (iPhone 12)*                                                    |
+----------------------+-----------------------------------------------------------------------------------------+
| **GPU**              | - **Forward+ renderer:** SoC featuring GPU with full Vulkan 1.2 support, or             |
|                      |   Metal 3 support (iOS/iPadOS)                                                          |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)*                |
|                      |                                                                                         |
|                      | - **Mobile renderer:** SoC featuring GPU with full Vulkan 1.2 support, or               |
|                      |   Metal 3 support (iOS/iPadOS)                                                          |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)*                |
|                      |                                                                                         |
|                      | - **Compatibility renderer:** SoC featuring GPU with full OpenGL ES 3.2 support         |
|                      |                                                                                         |
|                      |   - *Example: Qualcomm Adreno 630, Mali-G72 MP18, Apple A14 (iPhone 12)*                |
+----------------------+-----------------------------------------------------------------------------------------+
| **RAM**              | - **For native exports:** 2 GB                                                          |
|                      | - **For web exports:** 4 GB                                                             |
+----------------------+-----------------------------------------------------------------------------------------+
| **Storage**          | 150 MB (used for the executable, project files, and cache)                              |
+----------------------+-----------------------------------------------------------------------------------------+
| **Operating system** | - **For native exports:** Android 9.0, iOS 16.0                                         |
|                      | - **For web exports:** Latest version of Firefox, Chrome, Edge, Safari, Opera,          |
|                      |   Samsung Internet                                                                      |
+----------------------+-----------------------------------------------------------------------------------------+

.. note::

    Godot không sử dụng các extension OpenGL/OpenGL ES được giới thiệu sau OpenGL 3.3/OpenGL ES 3.0, nhưng GPU hỗ trợ các phiên bản OpenGL/OpenGL ES mới hơn thường có ít vấn đề về driver hơn.
