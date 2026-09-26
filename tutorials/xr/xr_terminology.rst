.. _doc_xr_terminology:

Thuật ngữ XR
============

Trang này định nghĩa cách sử dụng các thuật ngữ như *XR*, *VR* và *AR* trong Godot.

Các thuật ngữ này không phải lúc nào cũng được sử dụng nhất quán trong ngành. Trong Godot, chúng tôi sử dụng các định nghĩa rõ ràng và thực tế để tránh sự mơ hồ, đồng thời phản ánh chính xác hơn cách những công nghệ này được triển khai trên thực tế.

XR (Extended Reality)
---------------------

**XR** là thuật ngữ bao quát tất cả công nghệ thực tế mở rộng được Godot hỗ trợ.

Trên thực tế, XR đề cập đến toàn bộ hệ thống được cung cấp thông qua
:ref:`XRServer <class_xrserver>` và các API liên quan. Hệ thống này trừu tượng hóa sự khác biệt giữa các nền tảng và cung cấp một cách thống nhất để xây dựng các ứng dụng XR.

XR bao gồm:

- Thực tế ảo (VR)
- Thực tế tăng cường (AR)

Từ góc độ phát triển, XR là điểm khởi đầu để làm việc với cả những trải nghiệm hoàn toàn ảo lẫn những trải nghiệm kết hợp các yếu tố ảo và thế giới thực.

VR (Virtual Reality)
--------------------

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube-nocookie.com/embed/xJKQ2ca5zVw" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

**Virtual Reality (VR)** đề cập đến các trải nghiệm **đắm chìm** hoàn toàn, trong đó người dùng được đặt vào một môi trường hoàn toàn ảo.

Khi sử dụng VR, người dùng không nhìn thấy thế giới thực. Thay vào đó, mọi thứ họ nhìn thấy đều được ứng dụng kết xuất, còn chuyển động của họ được theo dõi và áp dụng cho camera ảo cùng các controller.

Trong Godot, VR thường bao gồm:

- Thiết bị hiển thị đeo trên đầu (HMD)
- Các cảnh 3D hoàn toàn ảo
- Tracking 6DOF (sáu bậc tự do) cho đầu và controller

Đây là cách sử dụng XR phổ biến nhất trong Godot. Xem
:ref:`Thiết lập XR <doc_setting_up_xr>` để biết cách bắt đầu.

.. note::

    Ngay cả trong các ứng dụng VR, vẫn có thể sử dụng passthrough nếu headset hỗ trợ tính năng này.

    Trong trường hợp này, passthrough thường được dùng để hiển thị các yếu tố cụ thể của thế giới thực, chẳng hạn như bàn phím, chuột hoặc các thiết bị ngoại vi khác, trong khi phần còn lại của trải nghiệm vẫn hoàn toàn ảo.

    Đây là một trường hợp sử dụng kết hợp và khác với Augmented Reality, vì passthrough không được dùng để đặt nội dung ảo vào thế giới thực mà để chọn lọc hiển thị các phần của thế giới thực bên trong trải nghiệm VR.

AR (Augmented Reality)
----------------------

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube-nocookie.com/embed/8B8RnFokAFc" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

**Augmented Reality (AR)** đề cập đến các trải nghiệm trong đó nội dung ảo được phủ lên thế giới thực.

Người dùng vẫn nhìn thấy môi trường xung quanh trong thế giới vật lý, trong khi các vật thể ảo được kết xuất theo cách khiến chúng trông như là một phần của môi trường đó.

Trong Godot, AR được xem là một khái niệm duy nhất, bất kể loại thiết bị được sử dụng. Khái niệm này bao gồm các headset XR sử dụng camera passthrough, kính see-through có màn hình, và các thiết bị cầm tay như điện thoại và máy tính bảng.

Đối với các thiết bị XR và kính AR hỗ trợ những tiêu chuẩn như OpenXR hoặc WebXR, chức năng AR được cung cấp thông qua hệ thống XR. Trong những trường hợp này, ứng dụng có thể chạy trên nhiều thiết bị khác nhau với rất ít thay đổi. Passthrough trên các headset VR là một ví dụ về điều này và đơn giản là một phương pháp kỹ thuật được sử dụng để bật các khả năng AR trên những thiết bị đó.

Bên ngoài Godot, loại trải nghiệm này đôi khi được gọi là "Mixed Reality (MR)". Trong tài liệu Godot, khái niệm này được xem là Augmented Reality để tránh sự mơ hồ. Passthrough được coi là một chi tiết triển khai, không phải một danh mục riêng.

Xem :ref:`AR passthrough <doc_openxr_passthrough>` để biết ví dụ về AR sử dụng hệ thống XR.

.. note::

    Các nền tảng cầm tay như điện thoại và máy tính bảng hiện chưa cung cấp hỗ trợ OpenXR.

    Thay vào đó, chức năng AR được cung cấp thông qua các API độc quyền và yêu cầu các plugin dành riêng cho từng nền tảng:

	- `ARCore plugin (Android) <https://github.com/godotvr/godot_arcore>`_

    This results in platform-specific implementations that are not fully portable.

    OpenXR is capable of supporting handheld AR. If adopted by platform vendors, this would
    allow AR applications to run across phones, headsets, and glasses using a shared codebase.