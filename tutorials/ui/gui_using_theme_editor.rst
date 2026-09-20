.. _doc_gui_using_theme_editor:

Sử dụng trình chỉnh sửa theme
=============================

Bài viết này giải thích cách tạo và quản lý UI theme bằng trình chỉnh sửa Godot và công cụ theme editor. Chúng tôi khuyến nghị bạn làm quen với những kiến thức cơ bản về GUI skinning/theming bằng cách đọc :ref:`doc_gui_skinning` trước khi bắt đầu.

Theme editor là một công cụ trên panel phía dưới, tự động kích hoạt khi một resource :ref:`Theme <class_Theme>` được chọn để chỉnh sửa. Công cụ này chứa UI cần thiết để thêm, xóa và điều chỉnh các theme type và theme item. Công cụ có một khu vực preview để kiểm tra trực tiếp các thay đổi, cũng như một window dialog để thực hiện các thao tác hàng loạt với theme item.

Tạo theme
---------

Giống như mọi resource khác, theme có thể được tạo trực tiếp trong file system dock bằng cách nhấp chuột phải và chọn **New Resource...**, sau đó chọn **Theme** và nhấp vào **Create**. Cách này đặc biệt hữu ích khi tạo theme cho toàn bộ project.

Theme cũng có thể được tạo từ bất kỳ control node nào. Chọn một control node trong scene hierarchy, sau đó trong inspector đi đến thuộc tính ``theme``. Từ đó, bạn có thể chọn **New Theme**.

.. figure:: img/new_theme.webp
   :align: center

Thao tác này sẽ tạo một theme trống và mở theme editor. Hãy lưu ý rằng các resource được tạo theo cách này mặc định sẽ được đóng gói cùng scene. Hãy sử dụng context menu để lưu theme mới vào một file thay thế.

Mặc dù theme editor cung cấp các công cụ để quản lý theme type và item, theme cũng bao gồm font mặc định, fallback mà bạn chỉ có thể chỉnh sửa bằng Inspector dock. Điều tương tự cũng áp dụng cho nội dung của các loại resource phức tạp, chẳng hạn như :ref:`StyleBoxes <class_StyleBox>` và icon — chúng sẽ được mở để chỉnh sửa trong Inspector.

.. figure:: img/default_font.webp
   :align: center

Tổng quan về theme editor
-------------------------

.. figure:: img/theme_editor.webp
   :align: center

Theme editor có hai phần chính. Theme editor chính, nằm ở phía dưới trình chỉnh sửa Godot, nhằm cung cấp cho người dùng các công cụ để nhanh chóng tạo, chỉnh sửa và xóa theme item và type. Công cụ này cung cấp các công cụ trực quan để chọn và thay đổi control, trừu tượng hóa các khái niệm theme bên dưới. Mặt khác, dialog **Manage Theme Items** hướng đến việc đáp ứng nhu cầu của những người muốn thay đổi theme theo cách thủ công. Dialog này cũng hữu ích khi tạo theme editor mới.

Theme preview
~~~~~~~~~~~~~

Phía bên trái của editor chính có một tập hợp các tab preview. Tab **Default Preview** hiển thị sẵn và chứa hầu hết các control thường được sử dụng ở nhiều trạng thái khác nhau. Preview có tính tương tác, vì vậy bạn cũng có thể xem trước các trạng thái trung gian (ví dụ: hover).

.. figure:: img/default_preview.webp
   :align: center

Bạn có thể tạo thêm các tab từ những scene bất kỳ trong project. Scene phải có một control node làm root để hoạt động như một preview. Để thêm tab mới, hãy nhấp vào nút **Add Preview** và chọn scene đã lưu từ file system.

.. figure:: img/scene_preview.webp
   :align: center

Nếu bạn thay đổi scene, các thay đổi đó sẽ không được tự động phản ánh trong preview. Để cập nhật preview, hãy nhấp vào nút reload trên toolbar.

Preview cũng có thể được dùng để nhanh chóng chọn theme type cần chỉnh sửa. Chọn công cụ picker trên toolbar và di chuột qua khu vực preview để làm nổi bật các control node. Các control node được làm nổi bật sẽ hiển thị tên class hoặc type variation nếu có. Nhấp vào control node được làm nổi bật để mở nó chỉnh sửa ở phía bên phải.

.. figure:: img/theme_preview_picker.webp
   :align: center

Theme type và item
~~~~~~~~~~~~~~~~~~

Phía bên phải của theme editor cung cấp danh sách các theme type có trong theme resource đang được chỉnh sửa, cùng nội dung của type được chọn. Danh sách item của type được chia thành nhiều tab, tương ứng với từng kiểu dữ liệu có trong theme (color, constant, style, v.v.). Nếu tùy chọn **Show Default** được bật, các giá trị theme mặc định của từng type tích hợp sẵn sẽ được hiển thị với màu xám. Nếu tùy chọn này bị tắt, chỉ các item có trong chính theme đang được chỉnh sửa mới được hiển thị.

.. figure:: img/theme_type_editor.webp
   :align: center

Bạn có thể thêm từng item từ theme mặc định vào theme hiện tại bằng cách nhấp vào nút **Override** bên cạnh item đó. Bạn cũng có thể override tất cả item mặc định của theme type đã chọn bằng cách nhấp vào nút **Override All**. Sau đó, có thể xóa các thuộc tính đã được override bằng nút **Remove Item**. Bạn cũng có thể đổi tên thuộc tính bằng nút **Rename Item**, và thêm các thuộc tính tùy chỉnh hoàn toàn vào danh sách bằng trường văn bản bên dưới.

Các theme item đã được override có thể được chỉnh sửa trực tiếp trong panel bên phải, trừ khi chúng là resource. Resource có các control cơ bản để thao tác, nhưng phải được chỉnh sửa trong Inspector dock.

.. figure:: img/theme_item_inspector.webp
   :align: center

Stylebox có một tính năng đặc biệt: bạn có thể ghim một stylebox riêng lẻ trong danh sách. Stylebox được ghim sẽ hoạt động như stylebox dẫn đầu, và tất cả stylebox cùng loại sẽ được cập nhật theo nó khi bạn thay đổi các thuộc tính của nó. Điều này cho phép bạn chỉnh sửa thuộc tính của nhiều stylebox cùng lúc.

.. figure:: img/theme_pin_the_stylebox.webp
   :align: center

Mặc dù có thể chọn theme type từ preview, bạn cũng có thể thêm chúng theo cách thủ công. Nhấp vào nút dấu cộng bên cạnh danh sách type sẽ mở menu **Add item Type**. Trong menu này, bạn có thể chọn một type từ danh sách hoặc nhập một tên bất kỳ để tạo type tùy chỉnh. Trường văn bản cũng lọc danh sách control node.

.. figure:: img/add_item_type.webp
   :align: center

Quản lý và import item
----------------------

Nhấp vào nút **Manage Items** sẽ mở dialog **Manage Theme Items**.

.. figure:: img/manage_items_button.webp
   :align: center

Trong tab **Edit Items**, bạn có thể xem và thêm theme type, cũng như xem và chỉnh sửa theme item của type đã chọn.

.. figure:: img/manage_items.webp
   :align: center

Bạn có thể tạo, đổi tên và xóa từng theme item tại đây bằng cách nhấp vào **Add X Item** tương ứng và chỉ định tên của chúng. Bạn cũng có thể xóa hàng loạt theme item theo kiểu dữ liệu của chúng (bằng biểu tượng brush trong danh sách) hoặc theo chất lượng của chúng. **Remove Class Items** sẽ xóa tất cả theme item tích hợp sẵn mà bạn đã tùy chỉnh cho một loại control node. **Remove Custom Items** sẽ xóa tất cả theme item tùy chỉnh của type đã chọn. Cuối cùng, **Remove All Items** sẽ xóa mọi thứ khỏi type.

Từ tab **Import Items**, bạn có thể import theme item từ các theme khác. Bạn có thể import item từ theme Godot mặc định, theme của trình chỉnh sửa Godot hoặc một theme tùy chỉnh khác. Bạn có thể import từng item hoặc nhiều item, đồng thời quyết định có sao chép hay bỏ qua dữ liệu của chúng. Có nhiều cách để chọn và bỏ chọn item, bao gồm chọn thủ công, theo hierarchy, theo kiểu dữ liệu hoặc chọn tất cả. Nếu chọn bao gồm dữ liệu, tất cả theme item sẽ được sao chép nguyên trạng vào theme của bạn. Nếu bỏ qua dữ liệu, các item có kiểu dữ liệu và tên tương ứng sẽ được tạo nhưng để trống, theo cách này sẽ tạo ra một template theme.

.. figure:: img/import_items.webp
   :align: center
