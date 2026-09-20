.. _doc_xr_terminology:

Thuật ngữ XR
============

Trang này định nghĩa cách sử dụng các thuật ngữ như *XR*, *VR* và *AR* trong Godot.

Các thuật ngữ này không phải lúc nào cũng được sử dụng nhất quán trong toàn ngành. Trong Godot, chúng tôi sử dụng các định nghĩa rõ ràng và thực tế để tránh sự mơ hồ, đồng thời phản ánh tốt hơn cách các công nghệ này thực sự được triển khai.

XR (Extended Reality)
---------------------

**XR** là thuật ngữ bao quát tất cả các công nghệ extended reality được Godot hỗ trợ.

Trên thực tế, XR đề cập đến toàn bộ hệ thống được cung cấp thông qua
:ref:`XRServer <class_xrserver>` and related APIs. This system abstracts away platform
các khác biệt và cung cấp một cách thống nhất để xây dựng các ứng dụng XR.

XR bao gồm:

- Virtual Reality (VR) - Augmented Reality (AR)

Xét từ góc độ phát triển, XR là điểm khởi đầu để làm việc với cả những trải nghiệm hoàn toàn ảo và những trải nghiệm kết hợp các yếu tố ảo với thế giới thực.

VR (Virtual Reality)
--------------------

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube-nocookie.com/embed/xJKQ2ca5zVw" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

**Virtual Reality (VR)** đề cập đến những trải nghiệm **immersive** hoàn toàn, trong đó người dùng được đặt bên trong một môi trường hoàn toàn ảo.

Khi sử dụng VR, người dùng không nhìn thấy thế giới thực. Thay vào đó, mọi thứ họ nhìn thấy đều được ứng dụng render, còn chuyển động của họ được theo dõi và áp dụng cho camera ảo và các controller.

Trong Godot, VR thường bao gồm:

- Head-mounted display (HMD) - Các cảnh 3D hoàn toàn ảo - Tracking 6DOF (sáu bậc tự do) cho đầu và controller

Đây là cách sử dụng XR phổ biến nhất trong Godot. Xem
:ref:`Setting up XR <doc_setting_up_xr>` for how to get started.

.. note::

    Ngay cả trong các ứng dụng VR, passthrough vẫn có thể được sử dụng nếu headset hỗ trợ.

    Trong trường hợp này, passthrough thường được sử dụng để hiển thị các thành phần cụ thể của thế giới thực, chẳng hạn như bàn phím, chuột hoặc các thiết bị ngoại vi khác, trong khi phần còn lại của trải nghiệm vẫn hoàn toàn ảo.

    Đây là một trường hợp sử dụng hybrid và khác với Augmented Reality, vì passthrough không được sử dụng để đặt nội dung ảo vào thế giới thực, mà để chọn lọc hiển thị các phần của thế giới thực bên trong một trải nghiệm VR.

AR (Augmented Reality)
----------------------

.. raw:: html

    <div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%; height: auto;">
        <iframe src="https://www.youtube-nocookie.com/embed/8B8RnFokAFc" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>

**Augmented Reality (AR)** đề cập đến những trải nghiệm trong đó nội dung ảo được phủ lên thế giới thực.

Người dùng vẫn tiếp tục nhìn thấy môi trường xung quanh trong thế giới thực, trong khi các vật thể ảo được render theo cách khiến chúng trông như một phần của môi trường đó.

Trong Godot, AR được xem là một khái niệm duy nhất, bất kể loại thiết bị được sử dụng. Điều này bao gồm các headset XR sử dụng camera passthrough, kính see-through có màn hình hiển thị và các thiết bị cầm tay như điện thoại, máy tính bảng.

Đối với các thiết bị XR và kính AR hỗ trợ những standard như OpenXR hoặc WebXR, chức năng AR được cung cấp thông qua hệ thống XR. Trong các trường hợp này, ứng dụng có thể chạy trên nhiều thiết bị khác nhau với rất ít thay đổi. Passthrough trên các headset VR là một ví dụ về điều này và đơn giản chỉ là một phương pháp kỹ thuật được sử dụng để kích hoạt các khả năng AR trên những thiết bị đó.

Bên ngoài Godot, loại trải nghiệm này đôi khi được gọi là "Mixed Reality (MR)". Trong tài liệu Godot, loại trải nghiệm này được xem là Augmented Reality để tránh sự mơ hồ. Passthrough được xem là một chi tiết triển khai, không phải một danh mục riêng biệt.

Xem :ref:`AR passthrough <doc_openxr_passthrough>` để biết ví dụ về AR sử dụng hệ thống XR.

.. note::

    Các nền tảng cầm tay như điện thoại và máy tính bảng hiện chưa cung cấp hỗ trợ OpenXR.

    Thay vào đó, chức năng AR được cung cấp thông qua các API độc quyền và yêu cầu các plugin dành riêng cho từng nền tảng:

	- `ARCore plugin (Android) <https://github.com/godotvr/godot_arcore>`_

    Điều này dẫn đến các cách triển khai dành riêng cho từng nền tảng và không hoàn toàn portable.

    OpenXR có khả năng hỗ trợ AR trên các thiết bị cầm tay. Nếu được các nhà cung cấp nền tảng áp dụng, điều này sẽ cho phép các ứng dụng AR chạy trên điện thoại, headset và kính bằng một codebase dùng chung.