.. _doc_gui_theme_type_variations:

Các biến thể loại theme
=======================

Khi thiết kế giao diện người dùng, đôi khi một node :ref:`Control <class_Control>` cần có diện mạo khác với diện mạo thường được định nghĩa bởi một :ref:`Theme <class_Theme>`. Mỗi control node đều có các ghi đè thuộc tính theme, cho phép bạn định nghĩa lại kiểu dáng cho từng phần tử UI riêng lẻ.

.. figure:: img/themecheck.webp
   :align: center

Cách tiếp cận này nhanh chóng trở nên khó quản lý nếu bạn cần dùng chung một diện mạo tùy chỉnh cho nhiều control. Hãy tưởng tượng bạn sử dụng các biến thể màu xám, xanh dương và đỏ của :ref:`Button <class_Button>` trong toàn bộ project. Việc thiết lập lại mỗi lần thêm một button element mới vào giao diện là một công việc tẻ nhạt.

Để giúp sắp xếp tốt hơn và tận dụng :ref:`sức mạnh của theme <doc_gui_skinning>`, bạn có thể sử dụng các biến thể loại theme. Chúng hoạt động giống như các loại theme thông thường, nhưng thay vì độc lập và tự chứa, chúng mở rộng một loại cơ sở khác.

Theo ví dụ trước, theme của bạn có thể định nghĩa một số kiểu dáng, màu sắc và font cho loại ``Button``, tùy chỉnh diện mạo của mọi button element trong UI. Để có button màu xám, đỏ hoặc xanh dương, bạn sẽ tạo một loại mới, chẳng hạn như ``GrayButton``, và đánh dấu nó là biến thể của loại cơ sở ``Button``.

Các biến thể loại có thể thay thế một số khía cạnh của loại cơ sở nhưng vẫn giữ lại những khía cạnh khác. Chúng cũng có thể định nghĩa các thuộc tính mà kiểu cơ sở chưa định nghĩa. Ví dụ, ``GrayButton`` của bạn có thể ghi đè kiểu ``normal`` từ loại cơ sở ``Button`` và thêm ``font_color`` mà ``Button`` chưa từng định nghĩa. Control sẽ sử dụng sự kết hợp của cả hai loại, trong đó ưu tiên biến thể loại.

.. note::
   Cách control xác định các mục theme cần sử dụng từ từng loại và từng theme được mô tả rõ hơn trong phần :ref:`Tùy chỉnh một project <doc_gui_theme_in_project>` của bài viết "Giới thiệu về GUI skinning".

Tạo một biến thể loại
---------------------

Để tạo một biến thể loại, hãy mở trình chỉnh sửa theme, sau đó nhấp vào biểu tượng dấu cộng bên cạnh menu thả xuống **Type** ở bên phải trình chỉnh sửa. Nhập tên bạn muốn đặt cho biến thể loại theme vào hộp văn bản, sau đó nhấp vào **Add Type**.

Bên dưới menu thả xuống **Type** là các tab thuộc tính. Chuyển sang tab có biểu tượng cờ lê và tua vít.

.. figure:: img/base_type.webp
   :align: center

Nhấp vào biểu tượng dấu cộng bên cạnh trường **Base Type**. Tại đó, bạn có thể chọn loại cơ sở, thường là tên của một lớp control node, chẳng hạn như ``Button``, ``Label``, v.v. Các biến thể loại cũng có thể liên kết chuỗi và mở rộng các biến thể loại khác. Cách này tương tự như việc control node kế thừa kiểu dáng từ lớp cơ sở của chúng. Ví dụ, ``CheckButton`` kế thừa kiểu dáng từ ``Button`` vì các loại node tương ứng mở rộng lẫn nhau.

Sau khi chọn loại cơ sở, bạn sẽ có thể thấy các thuộc tính của loại đó trên những tab khác trong trình chỉnh sửa theme. Bạn có thể chỉnh sửa chúng như bình thường.

Sử dụng một biến thể loại
-------------------------

Bây giờ bạn đã tạo một biến thể loại và có thể áp dụng nó cho các node. Trong inspector dock, bên dưới thuộc tính **Theme** của một control node, bạn có thể tìm thấy thuộc tính **Theme Type Variation**. Theo mặc định, thuộc tính này trống, nghĩa là chỉ loại cơ sở có ảnh hưởng đến node này.

Bạn có thể chọn một biến thể loại từ danh sách thả xuống hoặc nhập tên của biến thể theo cách thủ công. Các biến thể chỉ xuất hiện trong danh sách nếu biến thể loại đó thuộc theme trên toàn project, được cấu hình trong phần cài đặt project. Trong mọi trường hợp khác, bạn phải nhập thủ công tên của biến thể. Nhấp vào biểu tượng bút chì ở bên phải. Sau đó nhập tên của biến thể loại và nhấp vào biểu tượng dấu kiểm hoặc nhấn enter. Nếu tồn tại một biến thể loại có tên đó, node sẽ sử dụng biến thể này.
