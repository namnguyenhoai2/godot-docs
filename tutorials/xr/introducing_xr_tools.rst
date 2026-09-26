.. _doc_introducing_xr_tools:

Giới thiệu các công cụ XR
=========================

Ngay khi cài đặt, Godot cung cấp cho bạn mọi hỗ trợ cơ bản để thiết lập một dự án XR. Tuy nhiên, các cơ chế gameplay dành riêng cho XR cần được triển khai dựa trên nền tảng này. Mặc dù Godot giúp việc này tương đối dễ dàng, đây vẫn có thể là một nhiệm vụ đáng ngại.

Vì lý do này, Godot đã phát triển một bộ công cụ có tên là `Godot XR Tools <https://github.com/GodotVR/godot-xr-tools>`_, triển khai nhiều cơ chế cơ bản thường thấy trong các game XR, từ di chuyển đến tương tác với đối tượng và tương tác với UI.

Bộ công cụ này được thiết kế để hoạt động với cả runtime OpenXR và WebXR. Chúng ta sẽ sử dụng bộ công cụ này làm nền tảng cho tài liệu ở đây. Nó giúp các nhà phát triển bắt tay vào thực hiện ngay, nhưng với những trường hợp sử dụng cụ thể hơn, việc tự xây dựng logic cũng hoàn toàn hợp lý. Trong trường hợp đó, XR tools có thể giúp cung cấp ý tưởng.

Cài đặt XR Tools
----------------

Tiếp tục từ dự án chúng ta đã bắt đầu trong :ref:`doc_setting_up_xr`, chúng ta muốn thêm thư viện Godot XR Tools. Bạn có thể tải thư viện này từ `trang phát hành Godot XR Tools <https://github.com/GodotVR/godot-xr-tools/releases>`_. Tìm bản phát hành mới nhất và trong **Assets**, tải xuống tệp ``godot-xr-tools.zip``. Bạn cũng có thể tìm thấy thư viện này trong Asset Store với tiêu đề "Godot XR Tools".

Nếu bạn sử dụng tệp zip, hãy giải nén tệp sau khi tải xuống. Bạn sẽ nhận thấy các tệp nằm trong một thư mục con ``godot-xr-tools``. Bên trong thư mục này, bạn sẽ tìm thấy một thư mục ``addons``. Đây là thư mục bạn cần sao chép toàn bộ vào thư mục dự án Godot của mình. Lúc này, dự án của bạn sẽ trông gần giống như sau:

.. image:: img/godot_xr_tools_root_folder.webp

Bây giờ hãy mở dự án trong Godot nếu bạn chưa mở, rồi chờ khoảng một phút để Godot nhập tất cả tài nguyên của plugin. Nếu Godot yêu cầu thiết lập đường dẫn đến Blender, bạn chỉ cần nhấp vào tùy chọn tắt tính năng nhập blender rồi khởi động lại trình chỉnh sửa.

Sau khi quá trình nhập hoàn tất, bạn có thể thấy một số thông báo "failed to load script" xuất hiện; điều đó là bình thường, plugin chỉ cần được bật trong phần cài đặt dự án.

Tiếp theo, mở menu ``Project`` và chọn ``Project Settings..``. Sau đó chuyển đến tab ``Plugins`` và bật plugin.

.. image:: img/godot_xr_tools_enable.webp

Sau khi thực hiện việc đó, bạn cần đóng rồi mở lại dự án để mọi thứ được bật đúng cách.

Bàn tay cơ bản
--------------

Để làm quen với mọi thứ, chúng ta sẽ thêm một vài thành phần tiêu chuẩn nhằm hoàn thiện cảnh, bắt đầu với bàn tay cho nhân vật người chơi.

OpenXR hỗ trợ theo dõi toàn bộ bàn tay, tuy nhiên hiện tại có sự khác biệt đáng kể về khả năng giữa các XR Runtime khác nhau.

Là một lựa chọn thay thế đáng tin cậy, Godot XR Tools đi kèm một số cảnh bàn tay đã được rig, phản ứng với đầu vào trigger và grip của bộ điều khiển. Các bàn tay này có phiên bản low poly và high poly, một số cấu hình, nhiều tệp animation để điều khiển vị trí các ngón tay và một số texture khác nhau.

Trong scene tree, hãy chọn node bàn tay trái :ref:`XRController3D <class_xrcontroller3d>`. Bây giờ nhấp vào nút **instantiate Child Scene** để thêm một cảnh con. Nhấp vào công tắc **addons** để có thể tìm kiếm trong thư mục addons. Sau đó tìm kiếm ``left_hand_low.tscn`` và chọn mục đó.

Như bạn có thể thấy từ đường dẫn của cảnh này, các model low poly nằm trong thư mục con ``lowpoly``, còn các model high poly nằm trong thư mục con ``highpoly``. Bạn nên sử dụng các phiên bản low poly nếu dự định phát hành game trên thiết bị di động.

Bàn tay mặc định chúng ta đã chọn chỉ là một bàn tay. Các tùy chọn khác là:

  * tac_glove - bàn tay đeo găng tay để hở các ngón
  * full_glove - bàn tay đeo găng tay che kín toàn bộ bàn tay

Cuối cùng, mỗi bàn tay đều có phiên bản ``physics``. Phiên bản này hiển thị toàn bộ các xương. Chúng ta sẽ xem cách sử dụng tính năng đó trong một tutorial khác.

Chúng ta lặp lại các bước tương tự cho bàn tay phải.

.. image:: img/xr_tools_basic_hands.webp

Thông tin thêm
--------------

Chúng ta sẽ tiếp tục thêm các tính năng vào dự án tutorial bằng Godot XR tools trong vài trang tiếp theo. Bạn có thể tìm thấy thông tin chi tiết hơn về bộ công cụ này `trong các trang trợ giúp của bộ công cụ <https://godotvr.github.io/godot-xr-tools/>`_.

.. _`Godot XR Tools`: https://github.com/GodotVR/godot-xr-tools
.. _`Godot XR Tools releases page`: https://github.com/GodotVR/godot-xr-tools/releases
.. _`on the toolkits help pages`: https://godotvr.github.io/godot-xr-tools/
