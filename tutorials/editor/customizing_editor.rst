.. _doc_customizing_editor:

Tùy chỉnh giao diện
===================

Theo mặc định, giao diện của Godot nằm trong một cửa sổ duy nhất. Kể từ Godot 4.0, bạn có thể tách một số thành phần thành các cửa sổ riêng để tận dụng tốt hơn thiết lập nhiều màn hình.

.. _doc_customizing_editor_moving_docks:

Di chuyển và thay đổi kích thước dock
-------------------------------------

Nhấp và kéo cạnh của bất kỳ dock hoặc panel nào để thay đổi kích thước theo chiều ngang hoặc chiều dọc:

.. figure:: img/editor_ui_resize_dock.webp
   :align: center
   :alt: Resizing a dock in the editor

   Resizing a dock in the editor

Nhấp vào biểu tượng "3 vertical dots" ở đầu bất kỳ dock nào để thay đổi vị trí của dock, hoặc tách dock thành một cửa sổ riêng bằng cách chọn **Make Floating** trong submenu xuất hiện:

.. figure:: img/editor_ui_move_dock.webp
   :align: center
   :alt: Moving a dock in the editor

   Moving a dock in the editor

Để đưa dock nổi trở lại cửa sổ editor, hãy đóng cửa sổ dock bằng nút **×** ở góc trên bên phải cửa sổ (hoặc ở góc trên bên trái trên macOS). Ngoài ra, bạn có thể nhấn :kbd:`Alt + F4` khi cửa sổ được tách đang được focus.

.. Trang này thiếu thông tin về:

    - Các thiết lập editor hữu ích hoặc các phần trong cửa sổ settings liên quan đến việc tùy chỉnh giao diện. - Layouts

Tách script hoặc shader editor thành cửa sổ riêng
-------------------------------------------------

.. note::

    Tính năng này chỉ khả dụng trên các nền tảng hỗ trợ tạo nhiều cửa sổ: Windows, macOS và Linux.

    Tính năng này cũng không khả dụng nếu **Single Window Mode** được bật trong Editor Settings.

Kể từ Godot 4.1, bạn có thể tách script hoặc shader editor thành cửa sổ riêng.

Để tách script editor thành cửa sổ riêng, hãy nhấp vào nút tương ứng ở góc trên bên phải của script editor:

.. figure:: img/editor_ui_split_script_editor.webp
   :align: center
   :alt: Splitting the script editor to its own window

   Splitting the script editor to its own window

Để tách shader editor thành cửa sổ riêng, hãy nhấp vào nút tương ứng ở góc trên bên phải của script editor:

.. figure:: img/editor_ui_split_shader_editor.webp
   :align: center
   :alt: Splitting the shader editor to its own window

   Splitting the shader editor to its own window

Để quay lại trạng thái trước đó (khi script/shader editor được nhúng trong cửa sổ editor), hãy đóng cửa sổ được tách bằng nút **×** ở góc trên bên phải cửa sổ (hoặc ở góc trên bên trái trên macOS). Ngoài ra, bạn có thể nhấn :kbd:`Alt + F4` khi cửa sổ được tách đang được focus.

Tùy chỉnh bố cục editor
-----------------------

Bạn có thể muốn lưu và tải cấu hình dock tùy theo loại tác vụ đang thực hiện. Chẳng hạn, khi làm việc với việc tạo animation cho một nhân vật, việc sắp xếp các dock theo cách khác có thể thuận tiện hơn so với khi bạn thiết kế một level.

Với mục đích này, Godot cung cấp cách lưu và khôi phục bố cục editor. Trước khi lưu một bố cục, hãy thực hiện các thay đổi đối với những dock mà bạn muốn lưu. Các thay đổi sau sẽ được lưu trong bố cục đã lưu:

- Di chuyển một dock. - Thay đổi kích thước một dock. - Chuyển một dock thành dock nổi. - Thay đổi vị trí hoặc kích thước của một dock nổi. - Các thuộc tính của FileSystem dock: chế độ chia, chế độ hiển thị, thứ tự sắp xếp, chế độ hiển thị danh sách tệp, các đường dẫn được chọn và các đường dẫn được mở rộng.

Sau khi thực hiện các thay đổi, hãy mở menu **Editor** ở đầu editor rồi chọn **Editor Layouts > Save**. Nhập tên cho bố cục, sau đó nhấp vào **Save**. Nếu bạn đã lưu một bố cục editor, bạn có thể chọn ghi đè một bố cục hiện có bằng danh sách này.

Sau khi thực hiện các thay đổi, hãy mở menu **Editor** ở đầu editor rồi chọn **Editor Layouts**. Trong danh sách dropdown, bạn sẽ thấy danh sách các bố cục editor đã lưu, cùng với **Default**, là một bố cục editor được định nghĩa cố định và không thể xóa. Bố cục mặc định giống với một bản cài đặt Godot mới, trong đó vị trí và kích thước của các dock chưa được thay đổi và không có dock nổi.

Bạn có thể xóa một bố cục bằng tùy chọn **Delete** trong dropdown **Editor Layouts**.

.. tip::

    Nếu đặt tên bố cục đã lưu là ``Default`` (phân biệt chữ hoa chữ thường), bố cục editor mặc định sẽ bị ghi đè. Lưu ý rằng ``Default`` không xuất hiện trong danh sách các bố cục để ghi đè cho đến khi bạn ghi đè nó một lần, nhưng bạn vẫn có thể tự nhập tên đó.

    Bạn có thể quay lại bố cục mặc định tiêu chuẩn bằng cách xóa bố cục ``Default`` sau khi ghi đè nó. (Tùy chọn này không xuất hiện nếu bạn chưa ghi đè bố cục mặc định.)

Các bố cục editor được lưu vào một tệp có tên ``editor_layouts.cfg`` trong đường dẫn cấu hình của :ref:`doc_data_paths_editor_data_paths`.

Tùy chỉnh thiết lập editor
--------------------------

Trong menu **Editor** ở đầu editor, bạn có thể tìm thấy tùy chọn **Editor Settings**. Tùy chọn này mở một cửa sổ tương tự Project Settings, nhưng chứa các thiết lập được editor sử dụng. Các thiết lập này được dùng chung cho tất cả dự án và không được lưu trong các tệp dự án.

.. figure:: img/editor_settings.webp
   :align: center
   :alt: The Editor Settings window

   The Editor Settings window

Một số thiết lập thường được thay đổi là:

- **Interface > Editor > Editor Language:** Kiểm soát ngôn ngữ mà editor hiển thị. Để dễ theo dõi các tutorial bằng tiếng Anh hơn, bạn có thể muốn đổi tùy chọn này thành English để tên menu giống với tên được nhắc đến trong các tutorial. Ngôn ngữ cũng có thể được thay đổi ở góc trên bên phải của project manager. - **Interface > Editor > Display Scale:** Kiểm soát kích thước hiển thị của các thành phần UI trên màn hình. Thiết lập **Auto** mặc định sẽ tìm một giá trị phù hợp dựa trên DPI và độ phân giải của màn hình. Do các giới hạn của engine, trên macOS, thiết lập này chỉ lấy hệ số scaling do màn hình cung cấp, không làm vậy trên Windows hoặc Linux. - **Interface > Editor > Single Window Mode:** Khi được bật, tùy chọn này buộc editor sử dụng một cửa sổ duy nhất. Tùy chọn này vô hiệu hóa một số tính năng, chẳng hạn như tách script/shaders editor thành cửa sổ riêng. Chế độ một cửa sổ có thể ổn định hơn, đặc biệt trên Linux khi sử dụng Wayland. - **Interface > Theme > Preset:** Preset theme mà editor sẽ sử dụng. Preset theme **Light** có thể dễ đọc hơn nếu bạn ở ngoài trời hoặc trong phòng có ánh nắng. Preset **Black (OLED)** có thể giảm mức tiêu thụ điện năng trên màn hình OLED, vốn ngày càng phổ biến trên laptop và điện thoại/máy tính bảng. - **FileSystem > Directories > Autoscan Project Path:** Có thể đặt tùy chọn này thành đường dẫn thư mục sẽ được tự động quét để tìm các dự án trong project manager mỗi khi project manager khởi động. - **FileSystem > Directories > Default Project Path:** Kiểm soát vị trí mặc định nơi các dự án mới được tạo trong project manager. - **Editors > 3D > Emulate Numpad:** Cho phép sử dụng các phím 0-9 ở hàng trên cùng trong 3D editor như các phím numpad tương ứng. Bạn nên bật tùy chọn này nếu bàn phím không có cụm phím số. - **Editors > 3D > Emulate 3 Button Mouse:** Cho phép sử dụng các modifier pan, zoom và orbit trong 3D editor ngay cả khi không nhấn giữ nút chuột nào. Bạn nên bật tùy chọn này nếu đang sử dụng trackpad.

Xem tài liệu tham chiếu lớp :ref:`class_EditorSettings` để biết mô tả đầy đủ về hầu hết các thiết lập editor. Bạn cũng có thể di chuột lên tên của một thiết lập editor trong Editor Settings để hiển thị mô tả của thiết lập đó.
