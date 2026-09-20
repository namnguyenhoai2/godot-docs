.. Trang này chỉ nhằm giới thiệu khái quát giao diện cho người dùng. Để trình bày chi tiết hơn từng khu vực, hãy viết các trang tương ứng trong phần thích hợp nhất và liên kết đến chúng. Ví dụ: trình chỉnh sửa hoạt ảnh nằm trong phần hoạt ảnh. Các trang tổng quan, chẳng hạn như về Project Manager, nên được đặt trong sổ tay trình chỉnh sửa.

.. _doc_intro_to_the_editor_interface:

Tìm hiểu nhanh về giao diện của Godot
=====================================

Trang này sẽ cung cấp cho bạn cái nhìn tổng quan ngắn gọn về giao diện của Godot. Chúng ta sẽ xem xét các màn hình chính và dock khác nhau để giúp bạn định hướng.

.. seealso:: For a comprehensive breakdown of the editor's interface and how to
             sử dụng nó, hãy xem :ref:`Editor manual <doc_editor_introduction>`.

Project Manager
---------------

Khi khởi chạy Godot, cửa sổ đầu tiên bạn thấy là Project Manager. Trong tab mặc định **Projects**, bạn có thể quản lý các dự án hiện có, nhập hoặc tạo dự án mới, và nhiều thao tác khác.

.. image:: img/editor_intro_project_manager.webp

Ở đầu cửa sổ có một tab khác tên là **Asset Library**. Lần đầu truy cập tab này, bạn sẽ thấy nút "Go Online". Vì lý do bảo mật, trình quản lý dự án Godot không truy cập internet theo mặc định. Để thay đổi điều này, hãy nhấp vào nút "Go Online". Bạn có thể thay đổi tùy chọn này sau trong phần cài đặt.

Sau khi đặt chế độ mạng thành "online", bạn có thể tìm kiếm các dự án mẫu trong thư viện tài nguyên mã nguồn mở, nơi có nhiều dự án do cộng đồng phát triển:

.. image:: img/editor_intro_project_templates.webp

Có thể mở phần cài đặt của Project Manager bằng menu **Settings**:

.. image:: img/editor_intro_settings.webp

Tại đây, bạn có thể thay đổi ngôn ngữ của trình chỉnh sửa (mặc định là ngôn ngữ hệ thống), giao diện chủ đề, tỉ lệ hiển thị, chế độ mạng và cả quy ước đặt tên thư mục.

.. seealso:: To learn the Project Manager's ins and outs, read
             :ref:`doc_project_manager`.


Tìm hiểu nhanh về trình chỉnh sửa của Godot
-------------------------------------------

Khi mở một dự án mới hoặc dự án hiện có, giao diện của trình chỉnh sửa sẽ xuất hiện. Hãy cùng xem các khu vực chính của giao diện:

.. image:: img/editor_intro_editor_empty.webp

Theo mặc định, dọc theo cạnh trên của cửa sổ là **main menu** ở bên trái, các nút chuyển đổi **workspace** ở giữa (workspace đang hoạt động được tô sáng), cùng các nút **playtest** và công tắc **Movie Maker Mode** ở bên phải:

.. image:: img/editor_intro_top_menus.webp

Ngay bên dưới các nút workspace, :ref:`scenes <doc_key_concepts_overview_scenes>` đã mở được hiển thị dưới dạng các tab. Nút dấu cộng (+) ngay cạnh các tab sẽ thêm một cảnh mới vào dự án. Với nút ở ngoài cùng bên phải, bạn có thể bật chế độ không gây xao nhãng, chế độ này phóng to hoặc khôi phục kích thước của **viewport** bằng cách ẩn các **docks** trong giao diện:

.. image:: img/editor_intro_scene_selector.webp

Ở giữa, bên dưới bộ chọn cảnh là **viewport**, với **toolbar** ở phía trên. Tại đây, bạn sẽ tìm thấy các công cụ khác nhau để di chuyển, thay đổi tỉ lệ hoặc khóa các node của cảnh (hiện workspace 3D đang hoạt động):

.. image:: img/editor_intro_3d_viewport.webp

Thanh công cụ này thay đổi tùy theo ngữ cảnh và node được chọn. Dưới đây là thanh công cụ 2D:

.. image:: img/editor_intro_toolbar_2d.webp

Bên dưới là thanh công cụ 3D:

.. image:: img/editor_intro_toolbar_3d.webp

.. seealso:: To learn more on workspaces, read :ref:`doc_intro_to_the_editor_interface_five_screens`.

.. seealso:: To learn more on the 3D viewport and 3D in general, read :ref:`doc_introduction_to_3d`.

Hai bên viewport là các **docks**. Ở phía dưới cửa sổ là **bottom panel**.

Hãy cùng xem các dock. Dock **FileSystem** liệt kê các tệp trong dự án, bao gồm script, hình ảnh, mẫu âm thanh và nhiều loại khác:

.. image:: img/editor_intro_filesystem_dock.webp

Dock **Scene** liệt kê các node của cảnh đang hoạt động:

.. image:: img/editor_intro_scene_dock.webp

**Inspector** cho phép bạn chỉnh sửa các thuộc tính của node được chọn:

.. image:: img/editor_intro_inspector_dock.webp

.. seealso:: To read more on inspector, see :ref:`doc_editor_inspector_dock`.

.. seealso:: Docks can be customized. Read more on :ref:`doc_customizing_editor_moving_docks`.

**bottom panel**, nằm bên dưới viewport, là nơi chứa bảng điều khiển gỡ lỗi, trình chỉnh sửa hoạt ảnh, bộ trộn âm thanh và nhiều công cụ khác. Chúng có thể chiếm không gian đáng kể, vì vậy theo mặc định chúng được thu gọn:

.. image:: img/editor_intro_bottom_panels.webp

Khi nhấp vào một mục, mục đó sẽ mở rộng theo chiều dọc. Bên dưới, bạn có thể thấy trình chỉnh sửa hoạt ảnh đã được mở:

.. image:: img/editor_intro_bottom_panel_animation.webp

Các bottom panel cũng có thể được hiển thị hoặc ẩn bằng các phím tắt được xác định trong **Editor Settings > Shortcuts**, thuộc danh mục **Bottom Panels**.

.. _doc_intro_to_the_editor_interface_five_screens:

Năm màn hình chính
------------------

Có năm nút màn hình chính nằm ở giữa phía trên trình chỉnh sửa: 2D, 3D, Script, Game và Asset Library.

Bạn sẽ sử dụng **2D screen** cho mọi loại trò chơi. Ngoài trò chơi 2D, 2D screen cũng là nơi bạn xây dựng giao diện.

.. image:: img/editor_intro_workspace_2d.webp

Trong **3D screen**, bạn có thể làm việc với mesh, ánh sáng và thiết kế các màn chơi cho trò chơi 3D.

.. image:: img/editor_intro_workspace_3d.webp

.. note:: Read :ref:`doc_introduction_to_3d` for more detail about the **3D
          màn hình chính**.

**Game screen** là nơi dự án của bạn sẽ xuất hiện khi chạy từ trình chỉnh sửa. Bạn có thể duyệt qua dự án để kiểm thử, đồng thời tạm dừng và điều chỉnh dự án theo thời gian thực. Lưu ý rằng tính năng này chỉ dùng để kiểm tra cách các điều chỉnh sẽ hoạt động; mọi thay đổi được thực hiện tại đây sẽ không được lưu khi trò chơi dừng chạy.

.. image:: img/editor_intro_workspace_game.webp

**Script screen** là một trình chỉnh sửa mã hoàn chỉnh với trình gỡ lỗi, tính năng tự động hoàn thành phong phú và tài liệu tham khảo mã tích hợp.

.. image:: img/editor_intro_workspace_script.webp

Cuối cùng, **Asset Library** là thư viện các tiện ích bổ sung, script và tài nguyên miễn phí, mã nguồn mở để sử dụng trong dự án của bạn.

.. image:: img/editor_intro_workspace_assetlib.webp

.. seealso:: You can learn more about the asset library in
             :ref:`doc_what_is_assetlib`.

.. _doc_intro_to_the_editor_interface_integrated_class_reference:

Tài liệu tham khảo class tích hợp
---------------------------------

Godot có sẵn tài liệu tham khảo class tích hợp.

Bạn có thể tìm kiếm thông tin về một class, method, property, constant hoặc signal bằng bất kỳ phương pháp nào sau đây:

* Nhấn :kbd:`F1` (hoặc :kbd:`Opt + Space` trên macOS, hoặc :kbd:`Fn + F1` đối với máy tính xách tay có phím :kbd:`Fn`) ở bất kỳ đâu trong trình chỉnh sửa. * Nhấp vào nút "Search Help" ở góc trên bên phải của Script main screen. * Nhấp vào menu Help rồi chọn Search Help. * :kbd:`Ctrl + Click` (:kbd:`Cmd + Click` trên macOS) trên tên class, tên hàm hoặc biến tích hợp trong trình chỉnh sửa script.

.. image:: img/editor_intro_search_help_button.webp

Khi thực hiện bất kỳ thao tác nào trong số này, một cửa sổ sẽ bật lên. Nhập nội dung để tìm kiếm bất kỳ mục nào. Bạn cũng có thể sử dụng cửa sổ này để duyệt qua các đối tượng và method có sẵn.

.. image:: img/editor_intro_search_help.webp

Nhấp đúp vào một mục để mở trang tương ứng trong Script main screen.

.. image:: img/editor_intro_help_class_animated_sprite.webp

Ngoài ra,

* Nhấp trong khi nhấn :kbd:`Ctrl` (:kbd:`Cmd` trên macOS) trên tên class, tên hàm hoặc biến tích hợp trong trình chỉnh sửa script. * Nhấp chuột phải vào các node và chọn **Open Documentation**, hoặc chọn **Lookup Symbol** cho các phần tử trong trình chỉnh sửa script để mở trực tiếp tài liệu tương ứng.
