.. _doc_output_panel:

Bảng Output
===========

Bảng Output nằm ở cuối màn hình. Nhấp vào **Output** để mở bảng.

.. image:: img/overview_output.webp

Bảng Output cung cấp một số tính năng giúp việc xem văn bản được project (và editor) in ra dễ dàng hơn.

.. note::

    Theo mặc định, bảng Output sẽ tự động mở khi chạy project. Bạn có thể kiểm soát hành vi này bằng cách thay đổi thiết lập editor **Run > Bottom Panel > Action on Play**.

Các danh mục thông báo
----------------------

Có bốn danh mục thông báo:

- **Log:** Các thông báo tiêu chuẩn được project in ra. Hiển thị bằng màu trắng hoặc đen (tùy theo theme của editor). - **Error:** Các thông báo do project hoặc editor in ra, cho biết đã xảy ra một dạng lỗi nào đó. Hiển thị bằng màu đỏ. - **Warning:** Các thông báo do project hoặc editor in ra, cung cấp thông tin quan trọng nhưng không cho biết đã xảy ra lỗi. Hiển thị bằng màu vàng. - **Editor:** Các thông báo do editor in ra, thường dùng để theo dõi các thao tác undo/redo. Hiển thị bằng màu xám.

Lọc thông báo
-------------

Bằng cách nhấp vào các nút ở bên phải, bạn có thể ẩn một số danh mục thông báo nhất định. Điều này giúp bạn dễ dàng tìm thấy các thông báo cụ thể mà mình đang cần.

Bạn cũng có thể lọc thông báo theo nội dung văn bản bằng hộp **Filter Messages** ở cuối bảng Output.

Xóa thông báo
-------------

Khi chạy project, các thông báo hiện có sẽ được tự động xóa theo mặc định. Bạn có thể kiểm soát điều này bằng thiết lập editor **Run > Output > Always Clear Output on Play**. Ngoài ra, bạn có thể xóa thông báo theo cách thủ công bằng cách nhấp vào biểu tượng "chổi vệ sinh" ở góc trên bên phải của bảng Output.

.. _doc_output_panel_printing_messages:

In thông báo
------------

Có một số phương thức để in thông báo:

- :ref:`print() <class_@GlobalScope_method_print>`: In một thông báo. Phương thức này nhận nhiều đối số và nối chúng lại với nhau khi in. Phương thức này có các biến thể, lần lượt phân tách các đối số bằng tab và dấu cách:
  :ref:`printt() <class_@GlobalScope_method_printt>` and :ref:`prints() <class_@GlobalScope_method_prints>`.
- :ref:`print_rich() <class_@GlobalScope_method_print_rich>`: Tương tự ``print()``, nhưng có thể sử dụng BBCode để định dạng văn bản được in (xem bên dưới). - :ref:`push_error() <class_@GlobalScope_method_push_error>`: In một thông báo lỗi. Khi một lỗi được in trong project đang chạy, thông báo đó sẽ được hiển thị trong tab **Debugger > Errors**. - :ref:`push_warning() <class_@GlobalScope_method_push_warning>`: In một thông báo cảnh báo. Khi một cảnh báo được in trong project đang chạy, thông báo đó sẽ được hiển thị trong tab **Debugger > Errors**.

Đối với các trường hợp sử dụng phức tạp hơn, bạn có thể dùng các phương thức sau:

- :ref:`print_verbose() <class_@GlobalScope_method_print_verbose>`: Tương tự ``print()``, nhưng chỉ in khi chế độ verbose được bật trong Project Settings hoặc khi project được chạy với đối số dòng lệnh ``--verbose``. - :ref:`printerr() <class_@GlobalScope_method_printerr>`: Tương tự ``print()``, nhưng in ra standard error stream thay vì standard output string. Trong hầu hết trường hợp, nên ưu tiên ``push_error()``. - :ref:`printraw() <class_@GlobalScope_method_printraw>`: Tương tự ``print()``, nhưng không in dòng trống ở cuối. Đây là phương thức duy nhất **không** in vào bảng Output của editor. Phương thức này **chỉ** in ra standard output stream, nghĩa là nội dung vẫn được ghi vào file logging. - :ref:`print_debug() <class_@GDScript_method_print_debug>`: Tương tự ``print()``, nhưng thêm stack frame hiện tại vào một dòng mới ở cuối. Chỉ được hỗ trợ khi chạy từ editor hoặc khi project được export ở debug mode. - :ref:`print_stack() <class_@GDScript_method_print_stack>`: In stack trace từ vị trí hiện tại. Chỉ được hỗ trợ khi chạy từ editor hoặc khi project được export ở debug mode. - :ref:`print_tree() <class_Node_method_print_tree>`: In scene tree tương đối với node hiện tại. Hữu ích khi debug các cấu trúc node được tạo trong runtime. - :ref:`print_tree_pretty() <class_Node_method_print_tree_pretty>`: Tương tự ``print_tree()``, nhưng sử dụng các ký tự Unicode để tạo giao diện giống cây hơn. Phương thức này dựa vào `box-drawing characters <https://en.wikipedia.org/wiki/Box-drawing_characters>`__, vì vậy có thể không hiển thị chính xác với mọi font.

Để có các khả năng định dạng nâng cao hơn, hãy cân nhắc sử dụng
:ref:`doc_gdscript_printf` along with the above printing functions.

.. seealso::

    Các tính năng logging của engine được trình bày trong tài liệu :ref:`logging <doc_logging>`.

.. _doc_output_panel_printing_rich_text:

In rich text
~~~~~~~~~~~~

Bằng cách sử dụng :ref:`print_rich() <class_@GlobalScope_method_print_rich>`, bạn có thể in rich text vào bảng Output của editor và standard output (hiển thị khi người dùng chạy project từ terminal). Cơ chế này hoạt động bằng cách chuyển đổi BBCode thành `ANSI escape codes <https://en.wikipedia.org/wiki/ANSI_escape_code>`__ mà terminal có thể hiểu.

Trong output của editor, tất cả các thẻ BBCode đều được nhận diện như bình thường. Trong output của terminal, chỉ một số thẻ BBCode nhất định hoạt động, như được mô tả trong phần mô tả phương thức ``print_rich()`` được liên kết ở trên. Trong terminal, màu sắc sẽ hiển thị khác nhau tùy theo theme của người dùng, còn màu sắc trong editor sẽ sử dụng cùng các màu như khi hiển thị trong project.

.. note::

    Mức độ hỗ trợ mã escape ANSI khác nhau tùy terminal emulator. Màu sắc chính xác hiển thị trong output của terminal cũng phụ thuộc vào theme terminal do người dùng chọn.
