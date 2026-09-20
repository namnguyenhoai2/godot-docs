.. _doc_introducing_xr_tools:

Giới thiệu về các công cụ XR
============================

Godot cung cấp sẵn mọi hỗ trợ cơ bản để thiết lập một dự án XR. Tuy nhiên, các cơ chế gameplay dành riêng cho XR cần được triển khai trên nền tảng này. Mặc dù Godot giúp việc đó tương đối dễ dàng, đây vẫn có thể là một nhiệm vụ đáng ngại.

Vì lý do này, Godot đã phát triển một bộ công cụ có tên `Godot XR Tools <https://github.com/GodotVR/godot-xr-tools>`_, triển khai nhiều cơ chế cơ bản thường thấy trong các game XR, từ locomotion đến tương tác với vật thể và tương tác với UI.

Bộ công cụ này được thiết kế để hoạt động với cả runtime OpenXR và WebXR. Chúng ta sẽ sử dụng nó làm nền tảng cho tài liệu này. Nó giúp các nhà phát triển bắt tay vào làm ngay, nhưng với các trường hợp sử dụng cụ thể hơn, việc tự xây dựng logic cũng hoàn toàn hợp lý. Trong trường hợp đó, XR tools có thể cung cấp nguồn cảm hứng.

Cài đặt XR Tools
----------------

Tiếp tục từ dự án mà chúng ta đã bắt đầu trong :ref:`doc_setting_up_xr`, chúng ta muốn thêm thư viện Godot XR Tools. Bạn có thể tải thư viện này từ `Godot XR Tools releases page <https://github.com/GodotVR/godot-xr-tools/releases>`_. Tìm bản phát hành mới nhất và trong mục **Assets**, tải xuống tệp ``godot-xr-tools.zip``. Bạn cũng có thể tìm thấy nó trong Asset Store với tiêu đề "Godot XR Tools".

Nếu bạn sử dụng tệp zip, hãy giải nén sau khi tải xuống. Bạn sẽ nhận thấy các tệp nằm trong một thư mục con ``godot-xr-tools``. Bên trong thư mục này, bạn sẽ tìm thấy một thư mục ``addons``. Đây là thư mục bạn cần sao chép toàn bộ vào thư mục dự án Godot. Lúc này, dự án của bạn sẽ có cấu trúc tương tự như sau:

.. image:: img/godot_xr_tools_root_folder.webp

Bây giờ hãy mở dự án trong Godot nếu bạn chưa mở, rồi chờ khoảng một phút để Godot import toàn bộ resource của plugin. Nếu Godot yêu cầu thiết lập đường dẫn đến Blender, bạn chỉ cần nhấp vào tùy chọn tắt tính năng import blender rồi khởi động lại editor.

Sau khi quá trình import hoàn tất, bạn có thể nhận thấy một số thông báo "failed to load script" xuất hiện. Điều này là bình thường; plugin chỉ cần được bật trong project settings.

Tiếp theo, mở menu ``Project`` và chọn ``Project Settings..``. Sau đó chuyển đến tab ``Plugins`` và bật plugin.

.. image:: img/godot_xr_tools_enable.webp

Sau khi thực hiện việc đó, bạn cần đóng rồi mở lại dự án để mọi thứ được bật đúng cách.

Bàn tay cơ bản
--------------

Để làm quen với mọi thứ, chúng ta sẽ thêm một vài component tiêu chuẩn để hoàn thiện scene, bắt đầu với bàn tay cho người chơi.

OpenXR hỗ trợ hand tracking đầy đủ, tuy nhiên hiện tại khả năng giữa các XR Runtime khác nhau có sự chênh lệch đáng kể.

Một lựa chọn thay thế đáng tin cậy là Godot XR Tools đi kèm một số scene bàn tay đã được rig, phản ứng với các input trigger và grip của controller. Những bàn tay này có các phiên bản low poly và high poly, một số cấu hình, nhiều tệp animation để điều khiển vị trí các ngón tay và nhiều texture khác nhau.

Trong scene tree, chọn node :ref:`XRController3D <class_xrcontroller3d>` của bàn tay trái. Bây giờ hãy nhấp vào nút **instantiate Child Scene** để thêm một child scene. Nhấp vào toggle **addons** để có thể tìm kiếm trong thư mục addons. Sau đó tìm kiếm ``left_hand_low.tscn`` và chọn nó.

Như bạn có thể thấy từ đường dẫn của scene này, các model low poly nằm trong thư mục con ``lowpoly``, còn các model high poly nằm trong thư mục con ``highpoly``. Bạn nên sử dụng các phiên bản low poly nếu dự định phát hành game trên thiết bị di động.

Bàn tay mặc định mà chúng ta chọn chỉ là một bàn tay. Các tùy chọn khác là:

  * tac_glove - bàn tay đeo găng với các ngón tay để lộ * full_glove - bàn tay đeo găng che phủ toàn bộ bàn tay

Cuối cùng, mỗi bàn tay đều có phiên bản ``physics``. Phiên bản này hiển thị tất cả các bone. Chúng ta sẽ xem cách sử dụng nó trong một tutorial khác.

Chúng ta thực hiện tương tự cho bàn tay phải.

.. image:: img/xr_tools_basic_hands.webp

Thông tin thêm
--------------

Trong vài trang tiếp theo, chúng ta sẽ tiếp tục thêm các tính năng vào dự án tutorial bằng Godot XR tools. Bạn có thể tìm thấy thông tin chi tiết hơn về bộ công cụ `on the toolkits help pages <https://godotvr.github.io/godot-xr-tools/>`_.
