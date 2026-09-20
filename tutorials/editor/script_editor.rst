.. _doc_script_editor:

Trình soạn thảo Script
======================

.. _doc_script_editor_introduction:

Giới thiệu
----------

Trình soạn thảo script của Godot Engine là một trình soạn thảo văn bản mạnh mẽ và được tích hợp đầy đủ, không chỉ giúp đơn giản hóa quy trình viết và debug mã được viết bằng GDScript mà còn cho phép làm việc với các tệp văn bản thuần túy, cung cấp cho nhà phát triển một môi trường liền mạch để viết script cho logic và hành vi của game. Trình soạn thảo có thể tô sáng mã, tự động thụt lề, kiểm tra cú pháp và nhiều tính năng khác. Bạn cũng có thể tạo breakpoint để debug project mà không cần chuyển sang cửa sổ khác. Trình soạn thảo văn bản cũng đóng vai trò là trình xem tham chiếu class ngoại tuyến, có thể được truy cập theo một số cách như được mô tả trong
:ref:`doc_intro_to_the_editor_interface_integrated_class_reference`.

.. image:: img/script_editor_icons/text_editor.webp

.. _doc_script_editor_features:

Tính năng
---------

Một số tính năng chính của trình soạn thảo văn bản được liệt kê bên dưới:

- Trình soạn thảo mã được tích hợp đầy đủ cho GDScript. - Hỗ trợ tô sáng cú pháp cho các tệp GDScript và JSON. - Kiểm tra cú pháp cho các tệp GDScript và JSON. - Hỗ trợ bookmark và breakpoint. - Tự động thụt lề. - Thu gọn mã. - Theme có thể tùy chỉnh. - Nhiều caret, có thể bật bằng :kbd:`Alt + Left Click`. - Tự động hoàn tất biến, hàm, hằng số, v.v. - Refactor symbol trực tiếp bằng cách chọn chúng và sử dụng :kbd:`Ctrl + D`. - Tìm và thay thế hàng loạt trên các tệp trong project.

.. _doc_script_editor_usage:

Cách sử dụng
------------

Nếu bạn đang sử dụng GDScript trong project, trình soạn thảo văn bản tích hợp sẵn trong Godot cung cấp mọi thứ bạn cần, đóng vai trò là một nơi duy nhất để tận dụng đầy đủ Godot Engine. Gần như mọi tham số có thể điều chỉnh thông qua giao diện người dùng cũng có thể được thay đổi trực tiếp bằng mã.

.. note:: If you would like to use an external text editor or prefer to use C#
  trong project của bạn, hãy xem :ref:`doc_external_editor` và
  :ref:`doc_c_sharp_setup_external_editor`.

.. tip:: Similar to many parts of the Godot's interface, the text editor can
  cũng có thể được tùy chỉnh bằng cách thay đổi các thiết lập theo ý muốn. Bạn có thể truy cập các thiết lập này bằng cách mở **Editor > Editor Settings** và đi đến nhóm **Text Editor**.

.. image:: img/editor_ui_script_editor_open.webp

Bạn có thể mở Trình soạn thảo Script bằng nút **Script** trong bộ chọn workspace, nằm ở chính giữa phía trên giao diện Godot. Ngoài ra, bạn có thể sử dụng nút **Open Script** bên cạnh một node trong dock Scene Tree, hoặc nhấp đúp vào tệp ``.gd`` hay một tệp văn bản được nhận diện trong dock FileSystem để mở trực tiếp bằng Trình soạn thảo Script.

.. image:: img/editor_ui_script_editor_menu.webp

Sau khi mở, bạn sẽ thấy các menu của trình soạn thảo văn bản ở phía trên, bên dưới bộ chuyển đổi scene. Bên cạnh các menu, bạn sẽ thấy các nút để mở tài liệu trực tuyến hoặc tìm kiếm trong tham chiếu class tích hợp sẵn. Ở bên phải các nút này là hai mũi tên điều hướng cho phép bạn duyệt qua lịch sử xem. Cuối cùng, bạn có thể sử dụng nút float để tách trình soạn thảo văn bản khỏi cửa sổ Godot, rất hữu ích khi bạn làm việc với nhiều màn hình.

Bên dưới các menu ở bên trái, bạn sẽ thấy script panel. Ở chính giữa, cạnh script panel, là khu vực viết mã. Bên dưới khu vực viết mã là thanh trạng thái, hiển thị số lượng lỗi và cảnh báo trong mã. Nhấp vào biểu tượng lỗi hoặc cảnh báo sẽ hiển thị danh sách lỗi cùng số dòng. Nhấp vào một lỗi sẽ chuyển đến dòng đó. Bạn cũng có thể chọn bỏ qua cảnh báo bằng cách mở danh sách và nhấp vào ``Ignore``. Thanh trạng thái cũng cho phép bạn thay đổi mức thu phóng của mã bằng cách nhấp vào giá trị phần trăm. Bạn cũng có thể sử dụng :kbd:`Ctrl + Mouse Wheel` (:kbd:`Cmd + Mouse Wheel` trên Mac) để đạt được hiệu ứng tương tự. Thanh trạng thái cũng hiển thị vị trí hiện tại của caret theo dòng và cột, cũng như cho biết thụt lề được thực hiện bằng tab hay khoảng trắng.

Nhiều thao tác được thực hiện trong trình soạn thảo văn bản cũng có thể được thực hiện bằng shortcut. Các thao tác hiển thị shortcut tương ứng bên cạnh chúng. Trong chính Godot, bạn có thể tìm và gán lại tất cả shortcut bằng cách đi đến
:menu:`Editor > Editor Settings... > Shortcuts`.

Trong các phần tiếp theo, chúng ta sẽ tìm hiểu những khía cạnh khác nhau của trình soạn thảo văn bản. Bạn cũng có thể chọn một phần bên dưới để chuyển đến chủ đề cụ thể:

.. contents::
   :local:
   :depth: 3
   :backlinks: none

.. _doc_script_editor_script_panel:

Script Panel
~~~~~~~~~~~~

.. |script| image:: img/script_editor_icons/Script.webp
.. |scriptcsharp| image:: img/script_editor_icons/ScriptCSharp.webp
.. |documentation| image:: img/script_editor_icons/Documentation.webp
.. |toolscript| image:: img/script_editor_icons/ToolScript.webp

.. image:: img/editor_ui_script_editor_script_panel.webp

Bên dưới các menu, ở panel bên trái, bạn sẽ thấy danh sách các tệp và trang tài liệu đang mở. Tùy thuộc vào loại tệp, danh sách này sẽ có một biểu tượng bên cạnh tên tệp. Ví dụ, biểu tượng |script| có nghĩa đây là một GDScript. |scriptcsharp| có nghĩa đây là một C# script. |documentation| có nghĩa đây là một tham chiếu class tích hợp sẵn. Cuối cùng, |toolscript| có nghĩa đây là script đang chạy (xem :ref:`tool annotation <doc_running_code_in_the_editor>` để biết thêm). Di chuột lên một tệp sẽ hiển thị tooltip với vị trí tương đối của tệp trong thư mục project.

Trên thanh trạng thái, nhấp vào mũi tên trái để ẩn script panel, nhấp vào mũi tên phải để hiển thị panel.

Nếu bạn không thay đổi thiết lập nào, tên tệp cũng có thể có màu khác nhau. Điều này giúp bạn nhận diện các tệp vừa được chỉnh sửa bằng cách làm nổi bật chúng. Bạn có thể thay đổi hành vi này trong **Editor > Editor Settings** bằng cách điều chỉnh các thuộc tính **Script Temperature** trong phần **Text Editor**.

Thanh bộ lọc phía trên tên tệp cung cấp tính năng tìm kiếm không phân biệt chữ hoa chữ thường tiện lợi để tìm một tệp cụ thể. Ngay cả khi bạn chỉ nhập các chữ cái của tên tệp vào thanh này, những tệp chứa các chữ cái đó theo đúng thứ tự cũng sẽ xuất hiện. Giả sử danh sách có một tệp tên là ``button.gd``. Nếu bạn nhập ``btn`` vào thanh bộ lọc, tệp này sẽ xuất hiện trong kết quả. Để đặt lại bộ lọc, hãy xóa nội dung trong thanh bộ lọc.

Dấu hoa thị (*) bên cạnh tên tệp cho biết tệp đó có các thay đổi chưa được lưu.

.. tip:: If you just enter "*" in the filter bar, you can display all unsaved files.

Bạn có thể kéo một tệp để thay đổi thứ tự. Nhấp chuột giữa vào một tệp sẽ đóng tệp đó. Nhấp chuột phải vào một tệp sẽ cung cấp một số tùy chọn để lưu hoặc đóng tệp, hoặc sao chép đường dẫn tương đối của tệp. Trong menu này:

Bạn cũng có thể sử dụng **Move Up** và **Move Down** để thay đổi thứ tự của tệp, hoặc sử dụng **Sort** để sắp xếp tất cả tệp theo thứ tự alphabet. **Toggle Files Panel** ẩn panel; bạn có thể hiển thị lại panel bằng mũi tên phải trên thanh trạng thái. **Close Docs** đóng tất cả tài liệu tham chiếu class đang mở, chỉ để lại các tệp script đang mở. **Show in FileSystem** tìm và làm nổi bật tệp trong dock FileSystem.

Bên dưới danh sách tệp, bạn sẽ thấy tên của tệp hiện đang mở. Nút bên cạnh tên này chuyển đổi thứ tự của các method được định nghĩa trong tệp giữa thứ tự alphabet và thứ tự xuất hiện trong tệp. Bên dưới là outline của tệp. Nếu đây là tệp script, outline sẽ chứa danh sách các method được định nghĩa. Tuy nhiên, nếu một trang tham chiếu class đang mở, khu vực này sẽ hiển thị mục lục của tài liệu. Nhấp vào một mục trong danh sách sẽ chuyển đến function hoặc phần tương ứng trong tệp. Tương tự, thanh **Filter Methods** cho phép bạn tìm kiếm một function hoặc phần cụ thể trong tài liệu đã chọn với cách hoạt động giống như khi lọc script.

.. _doc_script_editor_menus:

Menu
~~~~

Các menu của trình soạn thảo văn bản nằm bên dưới bộ chuyển đổi scene và cho phép bạn truy cập nhiều công cụ và tùy chọn, chẳng hạn như quản lý tệp, tìm kiếm và thay thế, các điều khiển debug và các tính năng định dạng mã.

.. tip:: An asterisk (*) next to an action means that this operation is also available
  trong menu ngữ cảnh, có thể mở bằng cách nhấp chuột phải trong trình soạn thảo mã.

.. image:: img/script_editor_icons/text_editor_menu.webp

Menu **File** cung cấp các tùy chọn sau:

.. image:: img/script_editor_icons/text_editor_file_menu.webp

- **New Script...**: Mở hộp thoại tạo script mới để tạo và thêm script vào project. Nếu tạo thành công, script sẽ được mở trực tiếp trong trình soạn thảo văn bản. Tùy thuộc vào phiên bản Godot (có hỗ trợ C# hay không), bạn có thể chọn ``.gd`` hoặc ``.cs`` làm phần mở rộng. - **New Text File...**: Mở hộp thoại tệp để tạo một tệp văn bản thuần túy với một trong các định dạng được nhận diện. Godot cũng có thể tô sáng các tệp ``json``. - **Open...**: Mở hộp thoại tệp để bạn duyệt trong máy tính và chọn bất kỳ tệp văn bản được nhận diện nào để mở. - **Reopen Closed Script**: Mở lại các script vừa đóng gần đây nhất. Bạn có thể sử dụng tùy chọn này nhiều lần để mở lại các script đã đóng khác nếu bạn đã đóng nhiều hơn một script. - **Open Recent**: Cung cấp danh sách các script được mở gần đây nhất. Bạn cũng có thể xóa danh sách bằng tùy chọn được cung cấp ở cuối danh sách. - **Save**: Lưu script hiện đang được chọn. - **Save As...**: Mở hộp thoại tệp để lưu script hiện đang mở với tên khác. - **Save All**: Lưu tất cả script đang mở và chưa được lưu trong trình soạn thảo văn bản. Các script có thay đổi chưa được lưu sẽ có dấu hoa thị (*) bên cạnh tên trong danh sách script. - **Soft Reload Tool Script**: Nếu script được chọn là một
  :ref:`tool <doc_running_code_in_the_editor>`, reloads the script to execute it again.
- **Copy Script Path**: Sao chép đường dẫn tương đối của script hiện được chọn trong project bằng tiền tố ``res://``. - **Show in FileSystem**: Tìm và làm nổi bật file được chọn trong dock FileSystem. - **History Previous**: Chuyển script đang hoạt động sang script đã được mở trước đó. Tùy chọn này hữu ích khi bạn mở nhiều script và muốn nhanh chóng quay lại script được chỉnh sửa gần đây nhất. Nếu bạn cũng đã thay đổi vị trí caret hơn 10 dòng, trước tiên caret sẽ được đưa về vị trí trước đó trong cùng file. - **History Next**: Sau khi sử dụng `History Previous` để quay lại script trước đó, tính năng này cho phép bạn tiến về phía trước trong lịch sử script, chuyển sang các script đã được truy cập trước đó. Tương tự như trên, nếu bạn cũng đã thay đổi vị trí caret hơn 10 dòng, trước tiên caret sẽ được đưa đến vị trí tiếp theo trong cùng file. - **Theme**: Cung cấp các tùy chọn để import theme hiện có, lưu hoặc reload theme. Việc thay đổi cài đặt theme được thực hiện thông qua `Editor Settings`. - **Close**: Đóng script đang hoạt động. - **Close All**: Đóng tất cả script đang mở và yêu cầu lưu nếu có thay đổi chưa được lưu. - **Close Other Tabs**: Đóng tất cả script đang mở ngoại trừ script được chọn. - **Close Docs**: Đóng các trang tài liệu tham chiếu class, chỉ giữ lại các script. - **Run**: Nếu script kế thừa :ref:`EditorScript <class_EditorScript>` và được dự định thực thi mà không chạy project, tùy chọn này sẽ chạy script. Xem :ref:`doc_running_code_in_the_editor_editorscript` để biết thêm. - **Toggle Files Panel**: Hiển thị hoặc ẩn panel script nằm ở bên trái trình soạn thảo văn bản, cho phép bạn mở rộng vùng coding khả dụng. Xem thêm về `Scripts Panel` :ref:`above <doc_script_editor_script_panel>`.

Menu **Edit** cung cấp một số tùy chọn cho các thao tác trên dòng:

.. image:: img/script_editor_icons/text_editor_edit_menu.webp

- **Undo***: Cho phép bạn hoàn tác hành động gần đây nhất hoặc một chuỗi hành động, khôi phục tài liệu hoặc code về trạng thái trước khi các thay đổi được thực hiện. - **Redo***: Cho phép bạn thực hiện lại một hành động đã được hoàn tác trước đó, tức là thực hiện lại hành động cuối cùng đã bị hàm Undo hoàn tác. - **Cut***: Cắt phần lựa chọn vào clipboard. - **Copy***: Sao chép phần lựa chọn vào clipboard. - **Paste***: Dán nội dung của clipboard nếu nội dung đó chứa văn bản. - **Select All***: Chọn toàn bộ code trong trình soạn thảo văn bản. - **Duplicate Selection**: Sao chép phần lựa chọn và thêm bản sao ngay bên cạnh phần lựa chọn. - **Duplicate Lines**: Nhân đôi dòng hiện tại và thêm dòng đó làm dòng mới bên dưới dòng hiện tại. - **Evaluate Selection***: Tính toán các giá trị của văn bản được chọn nếu văn bản đó chỉ chứa một biểu thức toán học, chẳng hạn như ``83 * 3`` hoặc ``pow(2,3)``. - **Toggle Word Wrap**: Vô hiệu hóa thanh cuộn ngang bằng cách ngắt các dòng dài sang dòng tiếp theo. Lưu ý rằng đây chỉ là thay đổi về mặt hiển thị và không thêm linebreak mới. - **Line**: Cung cấp một nhóm thao tác trên dòng. Tùy thuộc vào file đang mở, các tùy chọn này cũng có thể nằm trực tiếp trong menu Edit thay vì một submenu.

  - **Move Up**: Di chuyển dòng hiện tại hoặc (các) dòng được chọn lên một dòng. - **Move Down**: Di chuyển dòng hiện tại hoặc (các) dòng được chọn xuống một dòng. - **Indent***: Thụt lề văn bản từ caret hoặc (các) dòng được chọn, theo cài đặt thụt lề. - **Unindent***: Bỏ thụt lề văn bản từ caret hoặc (các) dòng được chọn, theo cài đặt thụt lề. - **Delete Line**: Xóa dòng hiện tại hoặc (các) dòng được chọn. - **Toggle Comment***: Comment hoặc bỏ comment cho dòng hiện tại hoặc (các) dòng được chọn. Bạn cũng có thể thực hiện thao tác tương tự bằng cách chọn (các) dòng rồi chọn cùng thao tác đó sau khi nhấp chuột phải vào văn bản được chọn.

- **Folding**: Cung cấp một nhóm tùy chọn folding cho văn bản được chọn. Tùy thuộc vào file đang mở, các tùy chọn này cũng có thể nằm trực tiếp trong menu Edit thay vì một submenu.

  - **Fold/Unfold Line***: Nếu code trong dòng hiện tại có code block hoặc code region bên dưới, tùy chọn này sẽ ẩn block đó bằng cách collapse các dòng. Sau đó, bạn có thể unfold block bằng cách sử dụng lại tùy chọn này, sử dụng mũi tên ">" bên cạnh số dòng trong vùng coding hoặc nhấp vào biểu tượng dấu ba chấm "..." ở cuối dòng đã được fold. - **Fold All Lines**: Fold tất cả code block hoặc code region trong tài liệu đang mở. - **Unfold All Lines**: Unfold tất cả code block và code region trong tài liệu đang mở. - **Create Code Region***: Bọc văn bản được chọn trong một code region có thể fold để cải thiện khả năng đọc các script lớn. Xem :ref:`doc_gdscript_code_regions` để biết thêm.

- **Completion Query**: Gợi ý các symbol tích hợp sẵn hoặc do người dùng tạo để tự động hoàn tất code đang được viết dở. Các mũi tên :kbd:`Up` và :kbd:`Down` dùng để điều hướng lên và xuống, nhấn
  :kbd:`Enter` or :kbd:`Tab` accepts and adds the highlighted symbol to the code. :kbd:`Tab` will also replace existing text to the right of the caret.
- **Trim Trailing Whitespaces**: Xóa khoảng trắng thừa ở cuối mỗi dòng trong file. - **Trim Final Newlines**: Xóa các dòng mới thừa ở cuối file. - **Indentation**: Cung cấp các tùy chọn thụt lề cho file đang mở. Tùy thuộc vào file đang mở, các tùy chọn này cũng có thể nằm trực tiếp trong menu Edit thay vì một submenu.

  - **Convert Indent to Spaces**: Chuyển toàn bộ thụt lề trong file thành dấu cách. - **Convert Indent to Tabs**: Chuyển toàn bộ thụt lề trong file thành tab. - **Auto Indent**: Chuyển thụt lề của các dòng được chọn (hoặc toàn bộ file) theo cài đặt thụt lề.

- **Convert Case**: Thay đổi kiểu chữ của văn bản được chọn thành `Upper Case*`, `Lower Case*` hoặc viết hoa chữ cái đầu tiên của mỗi từ. - **Syntax Highlighter**: Cho phép bạn chọn syntax highlighter.

  - **Plain Text**: Tắt highlighting. - **Standard**: Highlighting mặc định cho các script C#. - **JSON**: Syntax highlighting cho các file JSON. - **GDScript**: Syntax highlighting cho các file GDScript.

Menu **Search** cung cấp các tùy chọn sau:

.. image:: img/script_editor_icons/text_editor_search_menu.webp

- **Find...**: Mở thanh quick-find bên dưới status bar để tìm văn bản trong file đang mở. Bạn có thể điều hướng đến kết quả khớp tiếp theo và kết quả khớp trước đó bằng mũi tên lên và xuống tương ứng. Chọn **Match Case** sẽ khiến tìm kiếm phân biệt chữ hoa chữ thường. Chọn **Whole Words** nghĩa là văn bản không được có chữ cái hoặc số nào ngay bên cạnh, chỉ có symbol và khoảng trắng. - **Find Next**: Tương tự mũi tên xuống, hiển thị kết quả xuất hiện tiếp theo. - **Find Previous**: Tương tự mũi tên lên, hiển thị kết quả xuất hiện trước đó.


- **Replace...**: Mở thanh tìm và thay thế bên dưới status bar để tìm văn bản và thay thế văn bản đó trong file đang mở. Bạn có thể chọn thay thế từng mục một hoặc tất cả cùng lúc. Ngoài ra, bạn có thể giới hạn việc thay thế trong văn bản được chọn bằng cách chọn checkbox **Selection Only** trên thanh tìm và thay thế. Bạn cũng có thể sử dụng :kbd:`Ctrl + D` để chọn thêm instance tiếp theo của văn bản hiện đang được chọn, cho phép bạn thực hiện thay thế inline trên nhiều lần xuất hiện. - **Find in Files...**: Mở một cửa sổ để tìm văn bản trong các file thuộc thư mục project. Chọn "Find..." sẽ bắt đầu từ thư mục đã chọn và bao gồm các phần mở rộng file được chọn trong bộ lọc. Kết quả được hiển thị trong panel phía dưới, cùng với số kết quả khớp và tổng số file được tìm thấy, trong tab **Search Results**. Nhấp vào một kết quả sẽ mở file và chuyển đến dòng tương ứng. - **Replace in Files...**: Mở một cửa sổ để tìm và thay thế văn bản bằng văn bản khác trong các file được tìm thấy thuộc thư mục project. Sau khi nhấp **Replace...**, bạn có thể chọn các file cần thay thế trong tab **Search Results** của panel phía dưới bằng cách (bỏ) chọn chúng và sử dụng nút **Replace All**.

.. image:: img/editor_ui_script_editor_replaceinfiles.webp

.. warning:: Note that "Replace in Files" operation cannot be undone!

.. tip:: Both the **Find in Files** and **Replace in Files** windows share the **Search...**
  và các nút **Replace...**. Điểm khác biệt duy nhất trong cửa sổ sau là có thêm một trường văn bản tự động điền vào panel kết quả tìm kiếm khi nhấp vào nút **Replace...**. Thao tác thay thế chỉ được thực hiện nếu bạn nhấp vào nút **Replace All** trong panel phía dưới này, nhờ đó bạn cũng có thể chỉnh sửa từ cần thay thế sau đó ngay trong panel.

.. image:: img/editor_ui_script_editor_replace_all.webp

- **Contextual Help***: Mở danh sách class reference tích hợp sẵn, tương tự như khi nhấn :kbd:`F1` trên một symbol hoặc chọn **Lookup Symbol** từ context menu.

Menu **Go To** cho phép bạn dễ dàng điều hướng trong code bằng các tùy chọn sau:

.. image:: img/script_editor_icons/text_editor_goto_menu.webp

- **Go to Function...**: Mở danh sách function để chuyển đến function mong muốn. Bạn có thể đạt được kết quả tương tự bằng cách nhập vào thanh filter methods trong script panel. - **Go to Line...**: Chuyển đến số dòng đã nhập trong code editor. - **Bookmarks**: Chứa các thao tác cho chức năng bookmark, giúp bạn dễ dàng tìm đường trong code, chẳng hạn như một section chưa hoàn chỉnh. Các dòng được bookmark sẽ có biểu tượng bookmark màu xanh ở bên trái số dòng.

  - **Toggle Bookmark***: Thêm hoặc xóa bookmark trên dòng đặt caret. Bạn cũng có thể nhấp chuột phải vào một dòng để thực hiện thao tác này. - **Remove All Bookmarks**: Xóa tất cả bookmark trong tài liệu đang mở. - **Go to Next Bookmark**: Chuyển đến bookmark tiếp theo trong tài liệu đang mở. - **Go to Previous Bookmark**: Chuyển đến bookmark trước đó trong tài liệu đang mở. - Menu **Bookmarks** cũng sẽ chứa danh sách các dòng được bookmark, bao gồm số dòng và phần nội dung được hiển thị một phần trên dòng đó.

- **Breakpoints**: Breakpoint rất hữu ích khi debug code. Tương tự menu **Bookmarks**, menu này cho phép bạn thêm hoặc xóa breakpoint, điều hướng giữa chúng và chuyển trực tiếp đến một breakpoint cụ thể. Một cách dễ dàng để thêm breakpoint là di chuột lên vùng trống bên trái số dòng. Một vòng tròn đỏ mờ sẽ xuất hiện. Nhấp vào đó để thêm breakpoint và vòng tròn sẽ vẫn ở đó. Nhấp vào vòng tròn để xóa breakpoint.

Menu **Debug** cung cấp các thao tác có thể sử dụng trong khi debug. Xem
:ref:`doc_debugger_tools_and_options` for more.

.. _doc_script_editor_coding_area:

Khu vực viết mã
~~~~~~~~~~~~~~~

.. note:: This section will only cover the basics of the coding area in terms of the user
  giao diện. Để tìm hiểu thêm về scripting trong Godot, hãy tham khảo :ref:`doc_gdscript` hoặc
  :ref:`Scripting <toc-learn-scripting>` documentation.

.. image:: img/editor_ui_script_editor_coding_area.webp

Khu vực viết mã là nơi bạn sẽ nhập các script nếu sử dụng trình soạn thảo văn bản tích hợp sẵn. Khu vực này cung cấp các tính năng tô sáng và tự động hoàn thành để hỗ trợ bạn trong quá trình viết mã.

Khu vực viết mã hiển thị số dòng ở phía bên trái. Bên dưới các mũi tên điều hướng ở phía bên phải là một minimap có thể nhấp vào, cung cấp cái nhìn tổng quan về toàn bộ script và cho phép bạn cuộn qua script đó.

Nếu một dòng mã đủ dài (theo mặc định là hơn 80 ký tự), trình soạn thảo văn bản sẽ hiển thị một đường dọc có thể được dùng làm đường hướng dẫn mềm. Đối với đường hướng dẫn cứng, giá trị này theo mặc định được đặt thành 100 ký tự. Bạn có thể thay đổi cả hai giá trị hoặc bật/tắt việc hiển thị đường này trong phần cài đặt "Appearance" của trình soạn thảo văn bản.

.. |override| image:: img/script_editor_icons/override.webp
.. |receiver| image:: img/script_editor_icons/receiver.webp
.. |foldable| image:: img/script_editor_icons/Foldable.webp

Trong script, ở bên trái phần định nghĩa hàm, bạn có thể thấy các biểu tượng bổ sung. Biểu tượng |override| cho biết hàm này là một :ref:`override <doc_overridable_functions>` của một hàm hiện có. Nhấp vào biểu tượng này sẽ mở tài liệu của hàm gốc. Biểu tượng |receiver| có nghĩa là đây là một phương thức nhận tín hiệu. Nhấp vào biểu tượng này sẽ hiển thị nơi tín hiệu được phát ra. Biểu tượng |foldable| ở bên trái dòng cho biết đây là một khối có thể thu gọn. Bạn có thể nhấp vào đó để thu gọn hoặc mở rộng khối. Ngoài ra, cũng có thể nhấp vào biểu tượng dấu ba chấm (...) để mở rộng một khối đã được thu gọn.

Ví dụ dưới đây tóm tắt đoạn văn ở trên. Các dòng 52, 56 và 58 là những khối có thể thu gọn; dòng 57 là một code region có tên "New Code Region", cũng có thể được thu gọn; còn dòng 62 là một khối đã được thu gọn. Dòng 53 là một bookmark, bạn có thể nhanh chóng chuyển đến đó bằng menu **Go To > Bookmarks**. Dòng 55 là một breakpoint có thể được sử dụng trong :ref:`debugging <doc_overview_of_debugging_tools>`.

.. image:: img/script_editor_icons/text_editor_coding_area_indicators.webp

Bạn có thể tùy chỉnh nhiều màu sắc của trình soạn thảo văn bản, chẳng hạn như màu tô sáng hoặc thậm chí màu của các biểu tượng breakpoint hay bookmark. Bạn có thể thử nghiệm bằng cách mở phần cài đặt của trình soạn thảo văn bản và chuyển đến mục **Editor > Editor Settings > Text Editor**.
