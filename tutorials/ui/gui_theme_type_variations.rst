.. _doc_gui_theme_type_variations:

Các biến thể kiểu theme
=======================

Khi thiết kế giao diện người dùng, đôi khi một node :ref:`Control <class_Control>` cần có giao diện khác với giao diện thường được định nghĩa bởi :ref:`Theme <class_Theme>`. Mỗi control node đều có các thuộc tính ghi đè theme, cho phép bạn định nghĩa lại kiểu dáng cho từng phần tử UI riêng lẻ.

.. figure:: img/themecheck.webp
   :align: center

Cách tiếp cận này nhanh chóng trở nên khó quản lý nếu bạn cần chia sẻ cùng một giao diện tùy chỉnh giữa nhiều control. Hãy tưởng tượng bạn sử dụng các biến thể màu xám, xanh dương và đỏ của :ref:`Button <class_Button>` trong toàn bộ project. Việc thiết lập lại mỗi lần thêm một button mới vào giao diện là một công việc tẻ nhạt.

Để giúp tổ chức tốt hơn và tận dụng :ref:`power of themes <doc_gui_skinning>` hiệu quả hơn, bạn có thể sử dụng các biến thể kiểu theme. Chúng hoạt động giống như các kiểu theme thông thường, nhưng thay vì độc lập và tự đầy đủ, chúng mở rộng một kiểu cơ sở khác.

Theo ví dụ trước, theme của bạn có thể định nghĩa một số style, màu sắc và font cho kiểu ``Button``, tùy chỉnh giao diện của mọi button trong UI. Sau đó, để có button màu xám, đỏ hoặc xanh dương, bạn sẽ tạo một kiểu mới, chẳng hạn ``GrayButton``, và đánh dấu kiểu đó là một biến thể của kiểu cơ sở ``Button``.

Các biến thể kiểu có thể thay thế một số khía cạnh của kiểu cơ sở nhưng giữ lại những khía cạnh khác. Chúng cũng có thể định nghĩa các thuộc tính mà style cơ sở chưa định nghĩa. Ví dụ, ``GrayButton`` của bạn có thể ghi đè style ``normal`` từ kiểu cơ sở ``Button`` và thêm ``font_color`` mà ``Button`` chưa từng định nghĩa. Control sẽ sử dụng sự kết hợp của cả hai kiểu, trong đó ưu tiên biến thể kiểu.

.. note::
   Cách các control xác định những mục theme chúng sử dụng từ từng kiểu và từng theme được mô tả rõ hơn trong phần :ref:`Customizing a project <doc_gui_theme_in_project>` của bài viết "Giới thiệu về GUI skinning".

Tạo một biến thể kiểu
---------------------

Để tạo một biến thể kiểu, hãy mở theme editor, sau đó nhấp vào biểu tượng dấu cộng bên cạnh menu thả xuống **Type** ở phía bên phải của editor. Nhập tên bạn muốn đặt cho biến thể kiểu theme vào hộp văn bản, rồi nhấp vào **Add Type**.

Bên dưới menu thả xuống **Type** là các tab thuộc tính. Chuyển sang tab có biểu tượng cờ lê và tua vít.

.. figure:: img/base_type.webp
   :align: center

Nhấp vào biểu tượng dấu cộng bên cạnh trường **Base Type**. Tại đây, bạn có thể chọn kiểu cơ sở, thường là tên của một class control node (ví dụ: ``Button``, ``Label``, v.v.). Các biến thể kiểu cũng có thể liên kết chuỗi và mở rộng các biến thể kiểu khác. Cơ chế này giống như cách các control node kế thừa style từ base class của chúng. Ví dụ, ``CheckButton`` kế thừa style từ ``Button`` vì các kiểu node tương ứng mở rộng lẫn nhau.

Sau khi chọn kiểu cơ sở, bạn sẽ có thể thấy các thuộc tính của kiểu đó trên những tab khác trong theme editor. Bạn có thể chỉnh sửa chúng như bình thường.

Sử dụng một biến thể kiểu
-------------------------

Sau khi đã tạo một biến thể kiểu, bạn có thể áp dụng nó cho các node của mình. Trong inspector dock, bên dưới thuộc tính **Theme** của một control node, bạn sẽ tìm thấy thuộc tính **Theme Type Variation**. Theo mặc định, thuộc tính này để trống, nghĩa là chỉ kiểu cơ sở có tác động đến node này.

Bạn có thể chọn một biến thể kiểu từ danh sách thả xuống hoặc nhập tên của biến thể theo cách thủ công. Các biến thể chỉ xuất hiện trong danh sách nếu biến thể kiểu đó thuộc về theme ở cấp project, được cấu hình trong phần cài đặt project. Trong mọi trường hợp khác, bạn phải nhập tên biến thể theo cách thủ công. Nhấp vào biểu tượng bút chì ở bên phải. Sau đó nhập tên biến thể kiểu và nhấp vào biểu tượng dấu kiểm hoặc nhấn enter. Nếu tồn tại một biến thể kiểu có tên đó, node sẽ sử dụng biến thể này.
