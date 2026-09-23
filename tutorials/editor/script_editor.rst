.. _doc_script_editor:

Trình chỉnh sửa Script
======================

.. _doc_script_editor_introduction:

Giới thiệu
----------

Trình chỉnh sửa script của Godot Engine là một trình soạn thảo văn bản mạnh mẽ và được tích hợp hoàn toàn, không chỉ giúp đơn giản hóa quá trình viết và gỡ lỗi mã được viết bằng GDScript mà còn cho phép làm việc với các tệp văn bản thuần túy, mang đến cho nhà phát triển một môi trường liền mạch để viết script cho logic và hành vi của trò chơi. Trình chỉnh sửa có thể tô sáng mã, tự động thụt lề, kiểm tra cú pháp và nhiều tính năng khác. Bạn cũng có thể tạo breakpoint để gỡ lỗi dự án mà không cần chuyển sang cửa sổ khác. Trình soạn thảo văn bản cũng đóng vai trò là trình xem tài liệu tham khảo class ngoại tuyến, có thể được truy cập bằng một số cách như mô tả trong
:ref:`doc_intro_to_the_editor_interface_integrated_class_reference`.

.. image:: img/script_editor_icons/text_editor.webp

.. _doc_script_editor_features:

Tính năng
---------

Dưới đây là một số tính năng chính của trình soạn thảo văn bản:

- Trình chỉnh sửa mã được tích hợp hoàn toàn cho GDScript.
- Hỗ trợ tô sáng cú pháp cho các tệp GDScript và JSON.
- Kiểm tra cú pháp cho các tệp GDScript và JSON.
- Hỗ trợ bookmark và breakpoint.
- Tự động thụt lề.
- Thu gọn mã.
- Theme có thể tùy chỉnh.
- Nhiều caret, có thể được bật bằng :kbd:`Alt + Left Click`.
- Tự động hoàn thành biến, hàm, hằng số, v.v.
- Refactor symbol ngay trong dòng bằng cách chọn chúng và sử dụng :kbd:`Ctrl + D`.
- Tìm và thay thế hàng loạt trong các tệp của dự án.

.. _doc_script_editor_usage:

Cách sử dụng
------------

Nếu bạn đang sử dụng GDScript trong dự án, trình soạn thảo văn bản tích hợp sẵn trong Godot cung cấp mọi thứ bạn cần, đóng vai trò là nơi duy nhất để tận dụng đầy đủ Godot Engine. Gần như mọi tham số có thể điều chỉnh thông qua giao diện người dùng cũng có thể được sửa đổi trực tiếp bằng mã.

.. note:: Nếu bạn muốn sử dụng trình soạn thảo văn bản bên ngoài hoặc thích sử dụng C# trong dự án, hãy xem :ref:`doc_external_editor` và
  :ref:`doc_c_sharp_setup_external_editor`.

.. tip:: Tương tự như nhiều phần khác trong giao diện của Godot, trình soạn thảo văn bản cũng có thể được tùy chỉnh bằng cách thay đổi các thiết lập theo ý muốn. Bạn có thể truy cập các thiết lập này bằng cách mở **Editor > Editor Settings** rồi đi đến nhóm **Text Editor**.

.. image:: img/editor_ui_script_editor_open.webp

Bạn có thể mở Trình chỉnh sửa Script bằng nút **Script** trong bộ chọn workspace, nằm ở chính giữa phía trên giao diện của Godot. Ngoài ra, bạn có thể sử dụng nút **Open Script** bên cạnh một node trong dock Scene Tree, hoặc nhấp đúp vào tệp ``.gd`` hoặc một tệp văn bản được nhận diện trong dock FileSystem để mở trực tiếp trong Trình chỉnh sửa Script.

.. image:: img/editor_ui_script_editor_menu.webp

Sau khi mở, bạn sẽ thấy các menu của trình soạn thảo văn bản ở phía trên, bên dưới bộ chuyển scene. Bên cạnh các menu là các nút để mở tài liệu trực tuyến hoặc tìm kiếm trong tài liệu tham khảo class tích hợp sẵn. Ở bên phải các nút này là hai mũi tên điều hướng, cho phép bạn di chuyển qua lịch sử xem. Cuối cùng, bạn có thể sử dụng nút float để tách trình soạn thảo văn bản khỏi cửa sổ của Godot, rất hữu ích khi bạn làm việc với nhiều màn hình.

Bên dưới các menu ở bên trái, bạn sẽ thấy bảng script. Ở giữa, cạnh bảng script, là khu vực viết mã. Bên dưới khu vực viết mã là thanh trạng thái, hiển thị số lỗi và cảnh báo trong mã. Nhấp vào biểu tượng lỗi hoặc cảnh báo sẽ hiển thị danh sách lỗi cùng số dòng. Nhấp vào một lỗi sẽ chuyển đến dòng đó. Bạn cũng có thể bỏ qua cảnh báo bằng cách mở danh sách và nhấp vào ``Ignore``. Thanh trạng thái cũng cho phép bạn thay đổi mức thu phóng của mã bằng cách nhấp vào giá trị phần trăm. Bạn cũng có thể sử dụng :kbd:`Ctrl + Mouse Wheel` (:kbd:`Cmd + Mouse Wheel` trên Mac) để đạt được hiệu quả tương tự. Thanh trạng thái cũng hiển thị vị trí hiện tại của caret theo dòng và cột, cũng như cho biết thụt lề được thực hiện bằng tab hay dấu cách.

Nhiều thao tác được thực hiện trong trình soạn thảo văn bản cũng có thể được thực hiện bằng shortcut. Các thao tác hiển thị shortcut tương ứng bên cạnh chúng. Ngay trong Godot, bạn có thể tìm và gán lại tất cả shortcut bằng cách đi đến
:menu:`Editor > Editor Settings... > Shortcuts`.

Trong các phần tiếp theo, chúng ta sẽ tìm hiểu các khía cạnh khác nhau của trình soạn thảo văn bản. Bạn cũng có thể chọn một phần bên dưới để chuyển đến chủ đề cụ thể:

.. contents::
   :local:
   :depth: 3
   :backlinks: none

.. _doc_script_editor_script_panel:

Bảng Script
~~~~~~~~~~~

.. |script| image:: img/script_editor_icons/Script.webp
.. |scriptcsharp| image:: img/script_editor_icons/ScriptCSharp.webp
.. |documentation| image:: img/script_editor_icons/Documentation.webp
.. |toolscript| image:: img/script_editor_icons/ToolScript.webp

.. image:: img/editor_ui_script_editor_script_panel.webp

Bên dưới các menu, ở bảng bên trái, bạn sẽ thấy danh sách các tệp và trang tài liệu đã mở. Tùy thuộc vào loại tệp, danh sách này sẽ có một biểu tượng bên cạnh tên tệp. Ví dụ, biểu tượng |script| có nghĩa đây là một GDScript. |scriptcsharp| có nghĩa đây là một script C#. |documentation| có nghĩa đây là tài liệu tham khảo class tích hợp sẵn. Cuối cùng, |toolscript| có nghĩa đây là một script đang chạy (xem :ref:`tool annotation <doc_running_code_in_the_editor>` để biết thêm). Di chuột lên một tệp sẽ hiển thị tooltip với vị trí tương đối của tệp trong thư mục dự án.

Trên thanh trạng thái, nhấp vào mũi tên trái sẽ ẩn bảng script, còn nhấp vào mũi tên phải sẽ hiển thị bảng này.

Nếu bạn chưa thay đổi thiết lập nào, tên tệp cũng có thể có màu khác nhau. Điều này giúp bạn xác định các tệp vừa được chỉnh sửa bằng cách làm nổi bật chúng. Bạn có thể thay đổi hành vi này trong **Editor > Editor Settings** bằng cách điều chỉnh các thuộc tính **Script Temperature** trong phần **Text Editor**.

Thanh bộ lọc phía trên tên tệp cung cấp tính năng tìm kiếm không phân biệt chữ hoa chữ thường tiện lợi để tìm một tệp cụ thể. Ngay cả khi bạn chỉ nhập các chữ cái trong tên tệp vào thanh này, những tệp chứa các chữ cái đó theo đúng thứ tự cũng sẽ xuất hiện. Giả sử danh sách có một tệp tên là ``button.gd``. Nếu bạn nhập ``btn`` vào thanh bộ lọc, tệp này sẽ xuất hiện trong kết quả. Để đặt lại bộ lọc, hãy xóa nội dung trong thanh bộ lọc.

Dấu hoa thị (*) bên cạnh tên tệp cho biết tệp có các thay đổi chưa được lưu.

.. tip:: Nếu chỉ nhập "*" vào thanh bộ lọc, bạn có thể hiển thị tất cả các tệp chưa được lưu.

Bạn có thể kéo một tệp để thay đổi thứ tự. Nhấp chuột giữa vào một tệp sẽ đóng tệp đó. Nhấp chuột phải vào một tệp sẽ cung cấp một số tùy chọn để lưu hoặc đóng tệp, hoặc sao chép đường dẫn tương đối của tệp. Trong menu này:

Bạn cũng có thể sử dụng **Move Up** và **Move Down** để thay đổi thứ tự tệp, hoặc sử dụng **Sort** để sắp xếp tất cả tệp theo thứ tự bảng chữ cái. **Toggle Files Panel** ẩn bảng này; bạn có thể hiển thị lại bằng mũi tên phải trên thanh trạng thái. **Close Docs** đóng tất cả tài liệu tham khảo class đang mở, chỉ để lại các tệp script. **Show in FileSystem** tìm và làm nổi bật tệp trong dock FileSystem.

Bên dưới danh sách tệp, bạn sẽ thấy tên của tệp hiện đang mở. Nút bên cạnh tên này chuyển đổi thứ tự các method được định nghĩa trong tệp giữa thứ tự bảng chữ cái và thứ tự xuất hiện. Bên dưới là dàn ý của tệp. Nếu đây là một tệp script, dàn ý sẽ chứa danh sách các method đã định nghĩa. Tuy nhiên, nếu một trang tài liệu tham khảo class đang mở, khu vực này sẽ hiển thị mục lục của tài liệu. Nhấp vào một mục trong danh sách sẽ chuyển đến hàm hoặc phần tương ứng trong tệp. Tương tự, thanh **Filter Methods** cho phép bạn tìm kiếm một hàm hoặc phần cụ thể trong tài liệu đã chọn, với cách hoạt động giống như khi lọc script.

.. _doc_script_editor_menus:

Menu
~~~~

Các menu của trình soạn thảo văn bản nằm bên dưới bộ chuyển scene và cho phép bạn truy cập nhiều công cụ cũng như tùy chọn, chẳng hạn như quản lý tệp, tìm kiếm và thay thế, các điều khiển gỡ lỗi và các tính năng định dạng mã.

.. tip:: Dấu hoa thị (*) bên cạnh một thao tác cho biết thao tác này cũng có trong menu ngữ cảnh, có thể mở bằng cách nhấp chuột phải trong trình soạn thảo mã.

.. image:: img/script_editor_icons/text_editor_menu.webp

Menu **File** cung cấp các tùy chọn sau:

.. image:: img/script_editor_icons/text_editor_file_menu.webp

- **New Script...**: Mở hộp thoại tạo script mới để tạo và thêm script vào project. Nếu tạo thành công, script sẽ được mở trực tiếp trong trình soạn thảo văn bản. Tùy thuộc vào phiên bản Godot (có hỗ trợ C# hay không), bạn có thể chọn ``.gd`` hoặc ``.cs`` làm phần mở rộng.
- **New Text File...**: Mở hộp thoại tệp để tạo một tệp văn bản thuần túy với một trong các định dạng được nhận diện. Godot cũng có thể tô sáng các tệp ``json``.
- **Open...**: Mở hộp thoại tệp để bạn duyệt bên trong máy tính và chọn bất kỳ tệp văn bản được nhận diện nào để mở.
- **Reopen Closed Script**: Mở lại các script vừa đóng gần đây. Bạn có thể sử dụng tùy chọn này nhiều lần để mở lại các script khác đã đóng nếu bạn đóng nhiều hơn một script.
- **Open Recent**: Cung cấp danh sách các script được mở gần đây. Bạn cũng có thể xóa danh sách bằng tùy chọn được cung cấp ở cuối danh sách.
- **Save**: Lưu script hiện đang được chọn.
- **Save As...**: Mở hộp thoại tệp để lưu script đang mở với tên khác.
- **Save All**: Lưu tất cả script đang mở và chưa được lưu trong trình soạn thảo văn bản. Các script có thay đổi chưa được lưu sẽ có dấu hoa thị (*) bên cạnh tên trong danh sách script.
- **Soft Reload Tool Script**: Nếu script được chọn là một
  :ref:`tool <doc_running_code_in_the_editor>`, tải lại script để thực thi nó lần nữa.
- **Copy Script Path**: Sao chép đường dẫn tương đối của script đang được chọn trong project bằng tiền tố ``res://``.
- **Show in FileSystem**: Tìm và tô sáng tệp được chọn trong dock FileSystem.
- **History Previous**: Chuyển script hiện hoạt sang script đã được mở trước đó. Tùy chọn này hữu ích khi bạn mở nhiều script và muốn nhanh chóng quay lại script vừa chỉnh sửa. Nếu bạn cũng đã thay đổi vị trí caret hơn 10 dòng, trước tiên caret sẽ được chuyển về vị trí trước đó trong cùng tệp.
- **History Next**: Sau khi sử dụng `History Previous` để quay lại một script trước đó, tính năng này cho phép bạn tiến về phía trước trong lịch sử script, chuyển sang các script đã được truy cập trước đó. Tương tự như trên, nếu bạn cũng đã thay đổi vị trí caret hơn 10 dòng, trước tiên caret sẽ được chuyển đến vị trí tiếp theo trong cùng tệp.
- **Theme**: Cung cấp các tùy chọn để nhập theme hiện có, lưu hoặc tải lại theme. Việc thay đổi cài đặt theme được thực hiện qua `Editor Settings`.
- **Close**: Đóng script hiện hoạt.
- **Close All**: Đóng tất cả script đang mở và yêu cầu lưu nếu có thay đổi chưa được lưu.
- **Close Other Tabs**: Đóng tất cả script đang mở ngoại trừ script được chọn.
- **Close Docs**: Đóng các trang tài liệu tham chiếu lớp, chỉ giữ lại các script.
- **Run**: Nếu script kế thừa :ref:`EditorScript <class_EditorScript>` và được dự định thực thi mà không chạy project, tùy chọn này sẽ chạy script. Xem :ref:`doc_running_code_in_the_editor_editorscript` để biết thêm.
- **Toggle Files Panel**: Hiển thị hoặc ẩn bảng script ở bên trái trình soạn thảo văn bản, cho phép bạn mở rộng khu vực viết mã. Thông tin thêm về `Scripts Panel` được giải thích :ref:`ở trên <doc_script_editor_script_panel>`.

Menu **Edit** cung cấp một số tùy chọn cho các thao tác trên dòng:

.. image:: img/script_editor_icons/text_editor_edit_menu.webp

- **Undo***: Cho phép hoàn tác thao tác hoặc chuỗi thao tác gần đây nhất, khôi phục tài liệu hoặc mã về trạng thái trước khi thay đổi.
- **Redo***: Cho phép áp dụng lại một thao tác đã được hoàn tác trước đó, thực hiện lại thao tác cuối cùng đã bị hàm Undo hoàn tác.
- **Cut***: Cắt phần lựa chọn vào clipboard.
- **Copy***: Sao chép phần lựa chọn vào clipboard.
- **Paste***: Dán nội dung của clipboard nếu nội dung đó chứa văn bản.
- **Select All***: Chọn toàn bộ mã trong trình soạn thảo văn bản.
- **Duplicate Selection**: Sao chép phần lựa chọn và thêm bản sao ngay bên cạnh phần lựa chọn.
- **Duplicate Lines**: Nhân bản dòng hiện tại và thêm dòng đó làm một dòng mới bên dưới dòng hiện tại.
- **Evaluate Selection***: Tính các giá trị của phần văn bản được chọn nếu phần đó chứa `only` một biểu thức toán học, chẳng hạn như ``83 * 3`` hoặc ``pow(2,3)``.
- **Toggle Word Wrap**: Tắt thanh cuộn ngang bằng cách ngắt các dòng dài sang dòng tiếp theo. Lưu ý rằng đây chỉ là thay đổi hiển thị và không thêm dấu ngắt dòng mới.
- **Line**: Cung cấp một nhóm thao tác trên dòng. Tùy thuộc vào tệp đang mở, các tùy chọn này cũng có thể nằm trực tiếp trong menu Edit thay vì trong menu con.

  - **Move Up**: Di chuyển dòng hiện tại hoặc (các) dòng được chọn lên một dòng.
  - **Move Down**: Di chuyển dòng hiện tại hoặc (các) dòng được chọn xuống một dòng.
  - **Indent***: Thụt lề văn bản từ caret hoặc (các) dòng được chọn, theo cài đặt thụt lề.
  - **Unindent***: Bỏ thụt lề văn bản từ caret hoặc (các) dòng được chọn, theo cài đặt thụt lề.
  - **Delete Line**: Xóa dòng hiện tại hoặc (các) dòng được chọn.
  - **Toggle Comment***: Bật hoặc tắt comment cho dòng hiện tại hoặc (các) dòng được chọn. Bạn cũng có thể thực hiện thao tác tương tự bằng cách chọn (các) dòng rồi chọn cùng thao tác sau khi nhấp chuột phải vào phần văn bản đã chọn.

- **Folding**: Cung cấp một nhóm tùy chọn thu gọn cho phần văn bản được chọn. Tùy thuộc vào tệp đang mở, các tùy chọn này cũng có thể nằm trực tiếp trong menu Edit thay vì trong menu con.

  - **Fold/Unfold Line***: Nếu mã trong dòng hiện tại có một khối mã hoặc vùng mã bên dưới, tùy chọn này sẽ ẩn khối đó bằng cách thu gọn các dòng. Sau đó, bạn có thể mở rộng khối bằng cách sử dụng lại tùy chọn này, sử dụng mũi tên ">" bên cạnh số dòng trong khu vực viết mã hoặc nhấp vào biểu tượng dấu ba chấm "..." ở cuối dòng đã thu gọn.
  - **Fold All Lines**: Thu gọn tất cả khối mã hoặc vùng mã trong tài liệu đang mở.
  - **Unfold All Lines**: Mở rộng tất cả các khối mã và vùng mã trong tài liệu đang mở.
  - **Create Code Region***: Đặt văn bản đã chọn vào một vùng mã có thể thu gọn để cải thiện khả năng đọc các script lớn hơn. Xem :ref:`doc_gdscript_code_regions` để biết thêm.

- **Completion Query**: Đề xuất các symbol tích hợp sẵn hoặc do người dùng tạo để tự động hoàn thành đoạn mã đang viết dở. Các mũi tên :kbd:`Up` và :kbd:`Down` dùng để di chuyển lên và xuống, nhấn
  :kbd:`Enter` hoặc :kbd:`Tab` để chấp nhận và thêm symbol được tô sáng vào mã. :kbd:`Tab` cũng sẽ thay thế văn bản hiện có ở bên phải con trỏ.
- **Trim Trailing Whitespaces**: Xóa khoảng trắng thừa ở cuối mỗi dòng trong tệp.
- **Trim Final Newlines**: Xóa các dòng mới thừa ở cuối tệp.
- **Indentation**: Cung cấp các tùy chọn thụt lề cho tệp đang mở. Tùy thuộc vào tệp đã mở, các tùy chọn này cũng có thể nằm trực tiếp trong menu Edit thay vì một submenu.

  - **Convert Indent to Spaces**: Chuyển toàn bộ thụt lề trong tệp thành dấu cách.
  - **Convert Indent to Tabs**: Chuyển toàn bộ thụt lề trong tệp thành tab.
  - **Auto Indent**: Chuyển thụt lề của các dòng đã chọn (hoặc toàn bộ tệp) theo thiết lập thụt lề.

- **Convert Case**: Thay đổi kiểu chữ của văn bản đã chọn thành `Upper Case*`, `Lower Case*`, hoặc viết hoa chữ cái đầu tiên của mỗi từ.
- **Syntax Highlighter**: Cho phép bạn chọn trình tô sáng cú pháp.

  - **Plain Text**: Tắt tính năng tô sáng.
  - **Standard**: Tính năng tô sáng mặc định cho các script C#.
  - **JSON**: Tô sáng cú pháp cho các tệp JSON.
  - **GDScript**: Tô sáng cú pháp cho các tệp GDScript.

Menu **Search** cung cấp các tùy chọn sau:

.. image:: img/script_editor_icons/text_editor_search_menu.webp

- **Find...**: Mở thanh tìm nhanh bên dưới thanh trạng thái để tìm văn bản trong tệp đang mở. Bạn có thể dùng các mũi tên lên và xuống để lần lượt chuyển đến kết quả khớp tiếp theo và trước đó. Chọn **Match Case** để tìm kiếm phân biệt chữ hoa chữ thường. Chọn **Whole Words** nghĩa là văn bản không được có bất kỳ chữ cái hoặc chữ số nào ngay bên cạnh, chỉ được có ký hiệu và khoảng trắng.
- **Find Next**: Tương tự mũi tên xuống, hiển thị lần xuất hiện tiếp theo.
- **Find Previous**: Tương tự mũi tên lên, hiển thị lần xuất hiện trước đó.


- **Replace...**: Mở thanh tìm và thay thế bên dưới thanh trạng thái để tìm văn bản và thay thế văn bản đó trong tệp đang mở. Bạn có thể chọn thay thế từng mục một hoặc tất cả cùng lúc. Ngoài ra, bạn có thể giới hạn việc thay thế trong văn bản đã chọn bằng cách chọn hộp kiểm **Selection Only** trên thanh tìm và thay thế. Bạn cũng có thể dùng :kbd:`Ctrl + D` để chọn thêm phiên bản tiếp theo của văn bản hiện đang được chọn, cho phép bạn thực hiện thay thế trực tiếp trên nhiều lần xuất hiện.
- **Find in Files...**: Mở một cửa sổ để tìm văn bản trong các tệp thuộc thư mục dự án. Việc chọn "Find..." sẽ bắt đầu với thư mục đã chọn và bao gồm các phần mở rộng tệp được đánh dấu trong bộ lọc. Kết quả được hiển thị trong panel phía dưới cùng với số kết quả khớp và tổng số tệp được tìm thấy, trong tab **Search Results**. Nhấp vào một kết quả sẽ mở tệp và chuyển đến dòng tương ứng.
- **Replace in Files...**: Mở một cửa sổ để tìm và thay thế văn bản bằng văn bản khác trong các tệp được tìm thấy thuộc thư mục dự án. Sau khi nhấp vào **Replace...**, bạn có thể chọn các tệp cần thay thế trong tab **Search Results** ở panel phía dưới bằng cách đánh dấu (hoặc bỏ đánh dấu) chúng và sử dụng nút **Replace All**.

.. image:: img/editor_ui_script_editor_replaceinfiles.webp

.. warning:: Lưu ý rằng thao tác "Replace in Files" không thể hoàn tác!

.. tip:: Cả hai cửa sổ **Find in Files** và **Replace in Files** đều dùng chung các nút **Search...** và **Replace...**. Điểm khác biệt duy nhất ở cửa sổ sau là có thêm một trường văn bản tự động điền vào panel kết quả tìm kiếm khi nhấp vào nút **Replace...**. Thao tác thay thế chỉ được thực hiện khi bạn nhấp vào nút **Replace All** trong panel phía dưới này, cho phép bạn cũng chỉnh sửa từ cần thay thế sau đó ngay trong panel.

.. image:: img/editor_ui_script_editor_replace_all.webp

- **Contextual Help***: Mở danh sách tham chiếu lớp tích hợp sẵn, tương tự như khi nhấn :kbd:`F1` trên một symbol hoặc chọn **Lookup Symbol** từ menu ngữ cảnh.

Menu **Go To** cho phép bạn dễ dàng di chuyển trong mã bằng các tùy chọn sau:

.. image:: img/script_editor_icons/text_editor_goto_menu.webp

- **Go to Function...**: Mở danh sách hàm để chuyển đến một hàm. Bạn cũng có thể đạt được kết quả tương tự bằng cách nhập vào thanh lọc phương thức trong panel script.
- **Go to Line...**: Chuyển đến số dòng đã nhập trong trình soạn thảo mã.
- **Bookmarks**: Chứa các thao tác dành cho chức năng bookmark, giúp bạn dễ dàng tìm đường trong mã, chẳng hạn như đến một phần chưa hoàn thiện. Các dòng được đánh dấu bookmark sẽ có biểu tượng bookmark màu xanh lam ở bên trái số dòng.

  - **Toggle Bookmark***: Thêm hoặc xóa bookmark trên dòng có con trỏ. Bạn cũng có thể nhấp chuột phải vào một dòng để thực hiện việc này.
  - **Remove All Bookmarks**: Xóa tất cả bookmark trong tài liệu đang mở.
  - **Go to Next Bookmark**: Chuyển đến bookmark tiếp theo trong tài liệu đang mở.
  - **Go to Previous Bookmark**: Chuyển đến bookmark trước đó trong tài liệu đang mở.
  - Menu **Bookmarks** cũng sẽ chứa danh sách các dòng được đánh dấu bookmark, bao gồm số dòng và nội dung rút gọn của dòng đó.

- **Breakpoints**: Breakpoint rất hữu ích khi debug mã. Tương tự menu **Bookmarks**, menu này cho phép bạn thêm hoặc xóa breakpoint, di chuyển giữa chúng và chuyển trực tiếp đến một breakpoint cụ thể. Một cách dễ dàng để thêm breakpoint là di chuột qua vùng trống bên trái số dòng. Một vòng tròn đỏ mờ sẽ xuất hiện. Nhấp vào đó sẽ thêm breakpoint và vòng tròn sẽ giữ nguyên tại vị trí đó. Nhấp vào vòng tròn sẽ xóa breakpoint.

Menu **Debug** cung cấp các thao tác có thể dùng khi debug. Xem
:ref:`doc_debugger_tools_and_options` để biết thêm.

.. _doc_script_editor_coding_area:

Khu vực viết mã
~~~~~~~~~~~~~~~

.. note:: Phần này chỉ trình bày những kiến thức cơ bản về khu vực viết mã xét trên phương diện giao diện người dùng. Để tìm hiểu thêm về scripting trong Godot, hãy tham khảo :ref:`doc_gdscript` hoặc
  :ref:`Scripting <toc-learn-scripting>` documentation.

.. image:: img/editor_ui_script_editor_coding_area.webp

Khu vực viết mã là nơi bạn sẽ nhập các script nếu đang sử dụng trình soạn thảo văn bản tích hợp. Khu vực này cung cấp các tính năng tô sáng và tự động hoàn thành để hỗ trợ bạn khi viết mã.

Khu vực viết mã hiển thị số dòng ở bên trái. Bên dưới các mũi tên điều hướng ở bên phải là một minimap có thể nhấp vào, cung cấp cái nhìn tổng quan về toàn bộ script và cho phép bạn cuộn qua script.

Nếu một dòng mã đủ dài (theo mặc định là hơn 80 ký tự), trình soạn thảo văn bản sẽ hiển thị một đường dọc có thể được dùng làm đường hướng dẫn mềm. Đối với đường hướng dẫn cứng, giá trị này mặc định là 100 ký tự. Bạn có thể thay đổi cả hai giá trị hoặc bật tắt hiển thị đường này trong phần "Appearance" của trình soạn thảo văn bản.

.. |override| image:: img/script_editor_icons/override.webp
.. |receiver| image:: img/script_editor_icons/receiver.webp
.. |foldable| image:: img/script_editor_icons/Foldable.webp

Trong script, ở bên trái phần định nghĩa hàm, bạn có thể thấy các biểu tượng bổ sung. Biểu tượng |override| cho biết hàm này là một hàm :ref:`ghi đè <doc_overridable_functions>` lên một hàm hiện có. Nhấp vào biểu tượng này sẽ mở tài liệu của hàm gốc. Biểu tượng |receiver| cho biết đây là phương thức nhận của một signal. Nhấp vào biểu tượng này sẽ hiển thị nơi signal phát ra. Biểu tượng |foldable| ở bên trái dòng cho biết một khối có thể thu gọn. Bạn có thể nhấp vào đó để thu gọn hoặc mở rộng khối. Ngoài ra, cũng có thể nhấp vào biểu tượng dấu ba chấm (...) để mở rộng một khối đang được thu gọn.

Ví dụ bên dưới tóm tắt đoạn văn trên. Các dòng 52, 56 và 58 là những khối có thể thu gọn; dòng 57 là một vùng mã có tên "New Code Region", cũng có thể được thu gọn; còn dòng 62 là một khối đang được thu gọn. Dòng 53 là một bookmark, có thể nhanh chóng chuyển đến bằng menu **Go To > Bookmarks**. Dòng 55 là một breakpoint có thể được sử dụng trong :ref:`debugging <doc_overview_of_debugging_tools>`.

.. image:: img/script_editor_icons/text_editor_coding_area_indicators.webp

Bạn có thể tùy chỉnh nhiều màu của trình soạn thảo văn bản, chẳng hạn như màu tô sáng, hoặc thậm chí màu biểu tượng breakpoint hay bookmark. Bạn có thể thử nghiệm với các màu này bằng cách mở phần cài đặt của trình soạn thảo văn bản và chuyển đến mục **Editor > Editor Settings > Text Editor**.
