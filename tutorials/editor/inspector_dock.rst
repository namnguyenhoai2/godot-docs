.. _doc_editor_inspector_dock:

Dock Inspector
==============

Dock Inspector liệt kê tất cả thuộc tính của một đối tượng, resource hoặc node. Danh sách thuộc tính sẽ được cập nhật khi bạn chọn một node khác trong dock Scene Tree hoặc sử dụng lệnh **Open** từ menu ngữ cảnh của FileSystem.

.. image:: img/inspector_overview.webp

Trang này giải thích chi tiết cách dock Inspector hoạt động. Bạn sẽ học cách chỉnh sửa thuộc tính, mở rộng và thu gọn các khu vực, sử dụng thanh tìm kiếm và nhiều thao tác khác.

Cách sử dụng
------------

Nếu dock Inspector đang hiển thị, việc nhấp vào một node trong scene tree sẽ tự động hiển thị các thuộc tính của node đó. Nếu dock không hiển thị, bạn có thể mở nó bằng cách đi tới **Editor > Editor Docks > Inspector**.

Ở đầu dock là các nút tệp và điều hướng.

.. image:: img/inspector_top_buttons.webp

Từ trái sang phải:

- Mở một cửa sổ mới để chọn và tạo một resource trong bộ nhớ, rồi chỉnh sửa resource đó.
- Mở một resource từ FileSystem để chỉnh sửa.
- Lưu resource đang được chỉnh sửa vào ổ đĩa.
- Cung cấp các tùy chọn để:

  - **Edit Resource from Clipboard** bằng cách dán resource đã sao chép.
  - **Copy Resource** vào clipboard.
  - **Show in FileSystem** nếu resource đã được lưu.
  - **Make Resource Built-In** để làm việc với một resource tích hợp sẵn thay vì resource trên ổ đĩa.

- Các mũi tên "<" và ">" cho phép bạn điều hướng qua lịch sử các đối tượng đã chỉnh sửa.
- Nút bên cạnh chúng mở danh sách lịch sử để điều hướng nhanh hơn. Nếu bạn đã tạo nhiều resource trong bộ nhớ, chúng cũng sẽ xuất hiện ở đây.

Bên dưới, bạn sẽ thấy biểu tượng của node đã chọn, tên node và nút nhanh để mở tài liệu của node ở phía bên phải. Nhấp vào chính tên node sẽ liệt kê các sub-resource của node nếu có.

Tiếp theo là thanh tìm kiếm. Nhập bất kỳ nội dung nào vào đó để lọc các thuộc tính được hiển thị. Xóa văn bản để xóa tìm kiếm. Tìm kiếm này không phân biệt chữ hoa chữ thường và cũng tìm kiếm theo từng chữ cái khi bạn nhập. Chẳng hạn, nếu bạn nhập ``vsb``, một trong các kết quả bạn thấy sẽ là thuộc tính Visibility vì thuộc tính này chứa tất cả các chữ cái đó.

Trước khi thảo luận về nút công cụ bên cạnh thanh bộ lọc, cần đề cập đến những gì bạn thực sự thấy bên dưới thanh này và cách chúng được sắp xếp.

.. image:: img/inspector_dock_overlay.webp

Các thuộc tính được nhóm trong các *classes* tương ứng dưới dạng *sections*. Bạn có thể mở rộng từng section để xem các thuộc tính liên quan.

Bạn cũng có thể mở tài liệu của từng class bằng cách nhấp chuột phải vào class rồi chọn **Open Documentation**. Tương tự, bạn có thể nhấp chuột phải vào một thuộc tính để sao chép hoặc dán giá trị của nó, sao chép đường dẫn thuộc tính, đánh dấu yêu thích để thuộc tính được hiển thị ở đầu Inspector hoặc mở trang tài liệu của thuộc tính.

Nếu di chuột qua một thuộc tính, bạn sẽ thấy mô tả về chức năng của thuộc tính cũng như cách gọi thuộc tính đó trong script.

Bạn có thể trực tiếp thay đổi các giá trị bằng cách nhấp, nhập hoặc chọn từ menu. Nếu thuộc tính là một số hoặc thanh trượt, bạn có thể giữ nút chuột trái và kéo để thay đổi giá trị.

.. image:: img/inspector_dock_subresource.webp

Nếu thuộc tính của một node là sub-resource, bạn có thể nhấp vào mũi tên xuống để chọn một loại resource hoặc tải resource bằng các tùy chọn **Quick Load** hoặc **Load**. Ngoài ra, bạn có thể kéo một resource được hỗ trợ từ FileSystem. Khi bắt đầu kéo, thuộc tính tương thích sẽ được làm nổi bật. Chỉ cần thả resource vào giá trị của thuộc tính tương ứng.

Sau khi tải một sub-resource, bạn có thể nhấp vào resource đó để xem hoặc điều chỉnh các thuộc tính của nó.

.. |undo| image:: img/inspector_dock_revert.webp

Các giá trị khác với giá trị ban đầu sẽ có biểu tượng hoàn nguyên (|undo|). Nhấp vào biểu tượng này sẽ hoàn nguyên giá trị về trạng thái ban đầu. Nếu các giá trị được liên kết với nhau, chúng sẽ có biểu tượng chuỗi và việc thay đổi một giá trị sẽ thay đổi các giá trị khác. Bạn có thể bỏ liên kết giữa chúng bằng cách nhấp vào biểu tượng này.

Nếu bạn thường xuyên thay đổi một thuộc tính, bạn có thể đánh dấu thuộc tính đó là yêu thích bằng cách nhấp chuột phải và chọn **Favorite Property**. Thao tác này sẽ hiển thị thuộc tính ở đầu Inspector cho tất cả đối tượng thuộc class này.

Sau khi đã hiểu rõ hơn về các thuật ngữ, chúng ta có thể tiếp tục với menu công cụ. Nếu nhấp vào biểu tượng menu công cụ bên cạnh thanh bộ lọc, một menu thả xuống sẽ cung cấp nhiều tùy chọn xem và chỉnh sửa.

.. image:: img/inspector_tools_menu.webp

- **Expand All**: Mở rộng tất cả section để hiển thị mọi thuộc tính hiện có.
- **Collapse All**: Thu gọn tất cả thuộc tính, chỉ hiển thị các class và section.
- **Expand Non-Default**: Chỉ mở rộng các section mà giá trị ban đầu khác với giá trị hiện tại (các thuộc tính có biểu tượng hoàn nguyên (|undo|)).
- **Property Name Style**: Section này xác định cách hiển thị văn bản thuộc tính trong Inspector. ``Raw`` sử dụng cách đặt tên riêng của thuộc tính, ``Capitalized`` sử dụng kiểu chữ tiêu đề bằng cách viết hoa chữ cái đầu của mỗi từ và loại bỏ dấu gạch dưới, còn ``Localized`` hiển thị bản dịch của các thuộc tính nếu bạn sử dụng Editor bằng ngôn ngữ khác tiếng Anh.
- **Copy Properties**: Sao chép tất cả thuộc tính của node hiện tại cùng các giá trị hiện tại của chúng.
- **Paste Properties**: Dán các thuộc tính đã sao chép từ clipboard. Hữu ích khi áp dụng các thuộc tính chung của một node cho node khác.
- **Make Sub-Resources Unique**: Theo mặc định, một node được nhân bản sẽ dùng chung các sub-resource của node ban đầu. Việc thay đổi một tham số của sub-resource trong một node sẽ ảnh hưởng đến node còn lại. Nhấp vào tùy chọn này sẽ làm cho mỗi sub-resource được node này sử dụng trở nên duy nhất và tách biệt với các node khác.

.. tip:: Nếu một node có các biến được export trong script đính kèm, bạn cũng sẽ thấy chúng trong Inspector. Hình ảnh đầu tiên trong section này có một biến cho node Player: `Action Suffix`. Xem :ref:`doc_gdscript_exports` để biết thêm về chủ đề này.

.. seealso:: Tham khảo :ref:`doc_customizing_editor` để biết các tùy chọn tùy chỉnh dock.


.. break down inspector content in class name, property categories that are foldable, and individual properties.

.. Using the buttons at the top.
.. Using the tool menu
.. List each property type and how to edit it
.. For numerical inputs, mention and link to a page about formulas
.. Refer to :ref:`doc_filesystem_dock`
