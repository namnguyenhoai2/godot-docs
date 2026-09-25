.. _doc_gui_using_theme_editor:

Sử dụng trình chỉnh sửa theme
=============================

Bài viết này giải thích cách tạo và quản lý UI theme bằng trình chỉnh sửa Godot và công cụ chỉnh sửa theme. Trước khi bắt đầu, chúng tôi khuyên bạn nên làm quen với những kiến thức cơ bản về GUI skinning/theming bằng cách đọc :ref:`doc_gui_skinning`.

Trình chỉnh sửa theme là một công cụ trong bảng điều khiển phía dưới, tự động kích hoạt khi tài nguyên :ref:`Theme <class_Theme>` được chọn để chỉnh sửa. Công cụ này chứa UI cần thiết để thêm, xóa và điều chỉnh các theme type và theme item. Công cụ có một phần xem trước để kiểm thử trực tiếp các thay đổi, cũng như một cửa sổ dialog để thực hiện các thao tác hàng loạt với theme item.

Tạo theme
---------

Giống như mọi resource khác, bạn có thể tạo theme trực tiếp trong dock hệ thống tệp bằng cách nhấp chuột phải và chọn **New Resource...**, sau đó chọn **Theme** rồi nhấp vào **Create**. Cách này đặc biệt hữu ích để tạo theme dùng cho toàn project.

Bạn cũng có thể tạo theme từ bất kỳ control node nào. Chọn một control node trong hệ thống phân cấp của scene, sau đó trong Inspector đi đến thuộc tính ``theme``. Tại đó, bạn có thể chọn **New Theme**.

.. figure:: img/new_theme.webp
   :align: center

Thao tác này sẽ tạo một theme trống và mở trình chỉnh sửa theme. Hãy nhớ rằng các resource được tạo theo cách này mặc định sẽ được đóng gói cùng scene. Hãy sử dụng context menu để thay vào đó lưu theme mới vào một tệp.

Mặc dù trình chỉnh sửa theme cung cấp các công cụ để quản lý theme type và item, theme cũng bao gồm font mặc định dùng làm fallback mà bạn chỉ có thể chỉnh sửa bằng dock Inspector. Điều tương tự cũng áp dụng cho nội dung của các loại resource phức tạp, chẳng hạn như :ref:`StyleBoxes <class_StyleBox>` và icon — chúng sẽ được mở để chỉnh sửa trong Inspector.

.. figure:: img/default_font.webp
   :align: center

Tổng quan về trình chỉnh sửa theme
----------------------------------

.. figure:: img/theme_editor.webp
   :align: center

Trình chỉnh sửa theme có hai phần chính. Trình chỉnh sửa theme chính, nằm ở phía dưới trình chỉnh sửa Godot, nhằm cung cấp cho người dùng các công cụ để nhanh chóng tạo, chỉnh sửa và xóa theme item và type. Công cụ này cung cấp các công cụ trực quan để chọn và thay đổi control, giúp trừu tượng hóa các khái niệm theme bên dưới. Mặt khác, dialog **Manage Theme Items** hướng đến nhu cầu của những người muốn thay đổi theme theo cách thủ công. Dialog này cũng hữu ích để tạo theme editor mới.

Xem trước theme
~~~~~~~~~~~~~~~

Phía bên trái của trình chỉnh sửa chính có một tập hợp các tab xem trước. Tab **Default Preview** hiển thị ngay từ đầu và chứa hầu hết các control thường dùng ở nhiều trạng thái khác nhau. Các bản xem trước có tính tương tác, vì vậy bạn cũng có thể xem trước các trạng thái trung gian (ví dụ: hover).

.. figure:: img/default_preview.webp
   :align: center

Bạn có thể tạo thêm các tab từ những scene tùy ý trong project. Scene phải có một control node làm node gốc thì mới hoạt động như bản xem trước. Để thêm tab mới, hãy nhấp vào nút **Add Preview** và chọn scene đã lưu từ hệ thống tệp.

.. figure:: img/scene_preview.webp
   :align: center

Nếu bạn thay đổi scene, các thay đổi đó sẽ không tự động được phản ánh trong bản xem trước. Để cập nhật bản xem trước, hãy nhấp vào nút reload trên thanh công cụ.

Bạn cũng có thể dùng các bản xem trước để nhanh chóng chọn theme type cần chỉnh sửa. Chọn công cụ picker trên thanh công cụ rồi di chuột qua khu vực xem trước để làm nổi bật các control node. Các control node được làm nổi bật sẽ hiển thị tên class hoặc type variation nếu có. Nhấp vào control đang được làm nổi bật để mở control đó và chỉnh sửa ở phía bên phải.

.. figure:: img/theme_preview_picker.webp
   :align: center

Theme type và item
~~~~~~~~~~~~~~~~~~

Phía bên phải của trình chỉnh sửa theme cung cấp danh sách các theme type có trong theme resource đang chỉnh sửa và nội dung của type được chọn. Danh sách item của type được chia thành một số tab, tương ứng với từng loại dữ liệu có trong theme (color, constant, style, v.v.). Nếu tùy chọn **Show Default** được bật, các giá trị theme mặc định của từng type tích hợp sẵn sẽ được hiển thị dưới dạng bị làm mờ. Nếu tắt tùy chọn này, chỉ các item có trong chính theme đang chỉnh sửa mới được hiển thị.

.. figure:: img/theme_type_editor.webp
   :align: center

Bạn có thể thêm từng item từ theme mặc định vào theme hiện tại bằng cách nhấp vào nút **Override** bên cạnh item đó. Bạn cũng có thể override tất cả item mặc định của theme type đã chọn bằng cách nhấp vào nút **Override All**. Sau đó, có thể xóa các thuộc tính đã override bằng nút **Remove Item**. Bạn cũng có thể đổi tên thuộc tính bằng nút **Rename Item** và thêm các thuộc tính tùy chỉnh hoàn toàn vào danh sách bằng trường văn bản bên dưới.

Bạn có thể chỉnh sửa trực tiếp các theme item đã override trong panel bên phải, trừ khi chúng là resource. Resource có các control cơ bản, nhưng phải được chỉnh sửa trong dock Inspector.

.. figure:: img/theme_item_inspector.webp
   :align: center

Stylebox có một tính năng riêng: bạn có thể ghim một stylebox trong danh sách. Stylebox được ghim sẽ đóng vai trò là stylebox dẫn đầu, và tất cả stylebox cùng type sẽ được cập nhật theo khi bạn thay đổi thuộc tính của nó. Điều này cho phép bạn chỉnh sửa thuộc tính của nhiều stylebox cùng lúc.

.. figure:: img/theme_pin_the_stylebox.webp
   :align: center

Mặc dù có thể chọn theme type từ bản xem trước, bạn cũng có thể thêm chúng theo cách thủ công. Nhấp vào nút dấu cộng bên cạnh danh sách type sẽ mở menu **Add item Type**. Trong menu đó, bạn có thể chọn một type từ danh sách hoặc nhập một tên tùy ý để tạo type tùy chỉnh. Trường văn bản cũng lọc danh sách các control node.

.. figure:: img/add_item_type.webp
   :align: center

Quản lý và nhập item
--------------------

Nhấp vào nút **Manage Items** sẽ mở dialog **Manage Theme Items**.

.. figure:: img/manage_items_button.webp
   :align: center

Trong tab **Edit Items**, bạn có thể xem và thêm theme type, cũng như xem và chỉnh sửa theme item của type đã chọn.

.. figure:: img/manage_items.webp
   :align: center

Tại đây, bạn có thể tạo, đổi tên và xóa từng theme item bằng cách nhấp vào **Add X Item** tương ứng rồi chỉ định tên của chúng. Bạn cũng có thể xóa hàng loạt theme item theo data type (bằng biểu tượng cọ trong danh sách) hoặc theo quality. **Remove Class Items** sẽ xóa tất cả theme item tích hợp sẵn mà bạn đã tùy chỉnh cho một loại control node. **Remove Custom Items** sẽ xóa tất cả theme item tùy chỉnh của type đã chọn. Cuối cùng, **Remove All Items** sẽ xóa mọi thứ khỏi type.

Trong tab **Import Items**, bạn có thể nhập theme item từ các theme khác. Bạn có thể nhập item từ theme Godot mặc định, theme trình chỉnh sửa Godot hoặc một theme tùy chỉnh khác. Bạn có thể nhập từng item hoặc nhiều item, đồng thời quyết định có sao chép hay bỏ qua dữ liệu của chúng. Có nhiều cách để chọn và bỏ chọn item, bao gồm chọn thủ công, theo hệ thống phân cấp, theo data type hoặc chọn tất cả. Nếu chọn bao gồm dữ liệu, tất cả theme item sẽ được sao chép nguyên trạng vào theme của bạn. Nếu bỏ qua dữ liệu, các item có data type và tên tương ứng sẽ được tạo nhưng để trống, qua đó tạo ra một template theme.

.. figure:: img/import_items.webp
   :align: center
