.. This page is only here to introduce the interface to the user broadly. To
   cover individual areas in greater detail, write the corresponding pages in
   the most appropriate section, and link them. E.g. the animation editor goes
   to the animation section. General pages, for instance, about the Project
   Manager, should go in the editor manual.

.. _doc_intro_to_the_editor_interface:

Tìm hiểu nhanh về giao diện của Godot
=====================================

Trang này sẽ cung cấp cho bạn cái nhìn tổng quan ngắn gọn về giao diện của Godot. Chúng ta sẽ xem qua các màn hình chính và dock khác nhau để giúp bạn làm quen với bố cục.

.. seealso:: Để xem phân tích toàn diện về giao diện của editor và cách sử dụng, hãy xem :ref:`Editor manual <doc_editor_introduction>`.

Project Manager
---------------

Khi khởi chạy Godot, cửa sổ đầu tiên bạn thấy là Project Manager. Trong tab mặc định **Projects**, bạn có thể quản lý các project hiện có, import hoặc tạo project mới và thực hiện nhiều thao tác khác.

.. image:: img/editor_intro_project_manager.webp

Ở phía trên cửa sổ còn có một tab khác tên là **Asset Library**. Lần đầu truy cập tab này, bạn sẽ thấy nút "Go Online". Vì lý do riêng tư, trình quản lý project của Godot không truy cập Internet theo mặc định. Để thay đổi điều này, hãy nhấp vào nút "Go Online". Bạn có thể thay đổi tùy chọn này sau trong phần cài đặt.

Sau khi đặt chế độ mạng thành "online", bạn có thể tìm kiếm các project demo trong thư viện asset mã nguồn mở, nơi bao gồm nhiều project do cộng đồng phát triển:

.. image:: img/editor_intro_project_templates.webp

Bạn có thể mở phần cài đặt của Project Manager bằng menu **Settings**:

.. image:: img/editor_intro_settings.webp

Tại đây, bạn có thể thay đổi ngôn ngữ của editor (mặc định là ngôn ngữ hệ thống), theme của giao diện, tỉ lệ hiển thị, chế độ mạng và cả quy ước đặt tên thư mục.

.. seealso:: Để tìm hiểu mọi khía cạnh của Project Manager, hãy đọc
             :ref:`doc_project_manager`.


Tìm hiểu nhanh về editor của Godot
----------------------------------

Khi mở một project mới hoặc project hiện có, giao diện editor sẽ xuất hiện. Hãy cùng xem các khu vực chính của giao diện:

.. image:: img/editor_intro_editor_empty.webp

Theo mặc định, dọc theo cạnh trên của cửa sổ có **main menu** ở bên trái, các nút chuyển **workspace** ở giữa (workspace đang hoạt động được tô sáng), và các nút **playtest** cùng nút chuyển đổi **Movie Maker Mode** ở bên phải:

.. image:: img/editor_intro_top_menus.webp

Ngay bên dưới các nút workspace là các :ref:`scenes <doc_key_concepts_overview_scenes>` đang mở dưới dạng các tab. Nút dấu cộng (+) ngay cạnh các tab sẽ thêm một scene mới vào project. Với nút ở ngoài cùng bên phải, bạn có thể bật hoặc tắt chế độ không gây xao nhãng; chế độ này tối đa hóa hoặc khôi phục kích thước của **viewport** bằng cách ẩn các **docks** trong giao diện:

.. image:: img/editor_intro_scene_selector.webp

Ở giữa, bên dưới bộ chọn scene là **viewport** với **toolbar** ở phía trên. Tại đây, bạn sẽ tìm thấy các công cụ khác nhau để di chuyển, thay đổi tỉ lệ hoặc khóa các node của scene (hiện workspace 3D đang hoạt động):

.. image:: img/editor_intro_3d_viewport.webp

Toolbar này thay đổi tùy theo ngữ cảnh và node được chọn. Đây là toolbar 2D:

.. image:: img/editor_intro_toolbar_2d.webp

Bên dưới là toolbar 3D:

.. image:: img/editor_intro_toolbar_3d.webp

.. seealso:: Để tìm hiểu thêm về workspace, hãy đọc :ref:`doc_intro_to_the_editor_interface_five_screens`.

.. seealso:: Để tìm hiểu thêm về viewport 3D và 3D nói chung, hãy đọc :ref:`doc_introduction_to_3d`.

Hai bên viewport là các **docks**. Ở cuối cửa sổ là **bottom panel**.

Hãy xem qua các dock. Dock **FileSystem** liệt kê các file của project, bao gồm script, hình ảnh, mẫu âm thanh và nhiều loại khác:

.. image:: img/editor_intro_filesystem_dock.webp

Dock **Scene** liệt kê các node của scene đang hoạt động:

.. image:: img/editor_intro_scene_dock.webp

**Inspector** cho phép bạn chỉnh sửa các thuộc tính của node được chọn:

.. image:: img/editor_intro_inspector_dock.webp

.. seealso:: Để đọc thêm về inspector, hãy xem :ref:`doc_editor_inspector_dock`.

.. seealso:: Bạn có thể tùy chỉnh các dock. Đọc thêm về :ref:`doc_customizing_editor_moving_docks`.

**bottom panel**, nằm bên dưới viewport, là nơi chứa debug console, animation editor, audio mixer và nhiều công cụ khác. Các panel này có thể chiếm không gian quý giá, vì vậy theo mặc định chúng được thu gọn:

.. image:: img/editor_intro_bottom_panels.webp

Khi nhấp vào một panel, panel đó sẽ mở rộng theo chiều dọc. Bên dưới là animation editor đang được mở:

.. image:: img/editor_intro_bottom_panel_animation.webp

Bạn cũng có thể hiện hoặc ẩn các bottom panel bằng các phím tắt được định nghĩa trong **Editor Settings > Shortcuts**, thuộc danh mục **Bottom Panels**.

.. _doc_intro_to_the_editor_interface_five_screens:

Năm màn hình chính
------------------

Có năm nút màn hình chính nằm ở giữa phía trên editor: 2D, 3D, Script, Game và Asset Library.

Bạn sẽ sử dụng **2D screen** cho mọi loại game. Ngoài game 2D, 2D screen còn là nơi bạn xây dựng giao diện.

.. image:: img/editor_intro_workspace_2d.webp

Trong **3D screen**, bạn có thể làm việc với mesh, ánh sáng và thiết kế level cho game 3D.

.. image:: img/editor_intro_workspace_3d.webp

.. note:: Đọc :ref:`doc_introduction_to_3d` để biết thêm chi tiết về **3D main screen**.

**Game screen** là nơi project của bạn sẽ xuất hiện khi được chạy từ editor. Bạn có thể thao tác trong project để kiểm thử, đồng thời tạm dừng và điều chỉnh project theo thời gian thực. Lưu ý rằng tính năng này chỉ dùng để kiểm tra cách các điều chỉnh sẽ hoạt động; mọi thay đổi được thực hiện tại đây sẽ không được lưu khi game dừng chạy.

.. image:: img/editor_intro_workspace_game.webp

**Script screen** là một code editor hoàn chỉnh với debugger, tính năng auto-completion phong phú và tài liệu tham chiếu code tích hợp sẵn.

.. image:: img/editor_intro_workspace_script.webp

Cuối cùng, **Asset Library** là thư viện các add-on, script và asset miễn phí, mã nguồn mở để sử dụng trong project của bạn.

.. image:: img/editor_intro_workspace_assetlib.webp

.. seealso:: Bạn có thể tìm hiểu thêm về asset library trong
             :ref:`doc_what_is_assetlib`.

.. _doc_intro_to_the_editor_interface_integrated_class_reference:

Tài liệu tham chiếu class tích hợp
----------------------------------

Godot đi kèm với tài liệu tham chiếu class tích hợp sẵn.

Bạn có thể tìm kiếm thông tin về một class, method, property, constant hoặc signal bằng bất kỳ cách nào sau đây:

* Nhấn :kbd:`F1` (hoặc :kbd:`Opt + Space` trên macOS, hoặc :kbd:`Fn + F1` đối với laptop có phím :kbd:`Fn`) ở bất kỳ đâu trong editor.
* Nhấp vào nút "Search Help" ở góc trên bên phải của màn hình chính Script.
* Nhấp vào menu Help rồi chọn Search Help.
* :kbd:`Ctrl + Click` (:kbd:`Cmd + Click` trên macOS) trên tên class, tên function hoặc biến tích hợp trong script editor.

.. image:: img/editor_intro_search_help_button.webp

Khi thực hiện bất kỳ thao tác nào trong số này, một cửa sổ sẽ bật lên. Nhập nội dung để tìm kiếm bất kỳ mục nào. Bạn cũng có thể sử dụng cửa sổ này để duyệt qua các object và method có sẵn.

.. image:: img/editor_intro_search_help.webp

Nhấp đúp vào một mục để mở trang tương ứng trong màn hình chính Script.

.. image:: img/editor_intro_help_class_animated_sprite.webp

Ngoài ra,

* Nhấp chuột đồng thời nhấn :kbd:`Ctrl` (:kbd:`Cmd` trên macOS) vào tên lớp, tên hàm hoặc biến dựng sẵn trong trình chỉnh sửa script.
* Nhấp chuột phải vào các node rồi chọn **Open Documentation** hoặc chọn **Lookup Symbol** cho các phần tử trong trình chỉnh sửa script sẽ trực tiếp mở tài liệu của chúng.
