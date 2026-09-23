:article_outdated: Đúng

.. _doc_using_the_web_editor:

Sử dụng trình chỉnh sửa web
===========================

Có một `trình chỉnh sửa web <https://editor.godotengine.org/>`__ mà bạn có thể sử dụng để làm việc với các dự án mới hoặc hiện có.

.. note::

    Trình chỉnh sửa web hiện đang ở giai đoạn sơ khai. Mặc dù bộ tính năng của nó có thể đủ cho mục đích giáo dục, hiện tại **không được khuyến nghị sử dụng cho công việc production**. Xem :ref:`doc_using_the_web_editor_limitations` bên dưới.

Hỗ trợ trình duyệt
------------------

Trình chỉnh sửa web yêu cầu WebAssembly hỗ trợ SharedArrayBuffer. Đổi lại, điều này là cần thiết để hỗ trợ threading trong trình duyệt.

Xem :ref:`doc_system_requirements` để biết danh sách các trình duyệt web được hỗ trợ. Trình duyệt trên thiết bị di động được hỗ trợ, nhưng sẽ không mang lại trải nghiệm tối ưu do những hạn chế về hiệu năng và phương thức nhập liệu.

Trình chỉnh sửa web chỉ hỗ trợ renderer Compatibility, vì hiện vẫn chưa có cách ổn định để chạy các ứng dụng Vulkan trên web.

.. note::

    Nếu gặp vấn đề về hiệu năng trên Firefox, hãy thử sử dụng trình duyệt dựa trên Chromium vì chúng có thể hoạt động tốt hơn với các ứng dụng WebGL.

.. _doc_using_the_web_editor_limitations:

Các hạn chế
-----------

Do những hạn chế ở phía Godot hoặc nền tảng Web, các tính năng sau hiện chưa có:

- Không hỗ trợ C#/Mono.
- Không hỗ trợ GDExtension.
- Không hỗ trợ debugging. Điều này có nghĩa là debugging/profiling GDScript, chỉnh sửa scene trực tiếp, dock Remote Scene tree và các tính năng khác phụ thuộc vào giao thức debugger sẽ không hoạt động.
- Không hỗ trợ export dự án. Cách khắc phục là bạn có thể tải mã nguồn dự án xuống bằng **Project > Tools > Download Project Source** rồi export bằng `phiên bản native của trình chỉnh sửa Godot <https://godotengine.org/download>`__.
- Trình chỉnh sửa sẽ không cảnh báo bạn khi đóng tab có các thay đổi chưa được lưu.
- Không hỗ trợ baking lightmap. Bạn vẫn có thể sử dụng các lightmap hiện có nếu chúng được bake bằng phiên bản native của trình chỉnh sửa Godot (ví dụ: bằng cách import một dự án hiện có).

Các tính năng sau đây khó có khả năng được hỗ trợ do những hạn chế vốn có của nền tảng Web:

- Không hỗ trợ các trình chỉnh sửa script bên ngoài.
- Không hỗ trợ deploy Android bằng một cú nhấp chuột.

.. seealso::

    Xem `danh sách các issue đang mở trên GitHub liên quan đến trình chỉnh sửa web <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Aplatform%3Aweb+label%3Atopic%3Aeditor>`__ để biết danh sách các bug đã biết.

Import một dự án
----------------

Để import một dự án hiện có, quy trình hiện tại như sau:

- Chỉ định một tệp ZIP để preload vào hệ thống tệp HTML5 bằng input **Preload project ZIP**.
- Chạy trình chỉnh sửa bằng cách nhấp vào **Start Godot editor**. Godot Project Manager sẽ xuất hiện sau 10-20 giây. Trên các máy hoặc kết nối chậm hơn, quá trình tải có thể mất tối đa một phút.
- Trong hộp thoại xuất hiện ở giữa cửa sổ, chỉ định tên cho thư mục cần tạo rồi nhấp vào nút **Create Folder** (tên này không nhất thiết phải trùng với tên của tệp lưu trữ ZIP).
- Nhấp vào **Install & Edit** và dự án sẽ mở trong trình chỉnh sửa.

.. attention::

    Điều quan trọng là đặt thư mục dự án ở đâu đó trong ``/home/web_user/``. Nếu thư mục dự án được đặt bên ngoài ``/home/web_user/``, bạn sẽ mất dự án khi đóng trình chỉnh sửa!

    Khi làm theo các bước được mô tả ở trên, thư mục dự án sẽ luôn nằm trong ``/home/web_user/projects``, nhờ đó được an toàn.

Chỉnh sửa và chạy một dự án
---------------------------

Không giống phiên bản native của Godot, trình chỉnh sửa web bị giới hạn trong một cửa sổ duy nhất. Vì vậy, nó không thể mở một cửa sổ mới khi chạy dự án. Thay vào đó, khi bạn chạy dự án bằng cách nhấp vào nút Run hoặc nhấn
:kbd:`F5`, nó sẽ xuất hiện để "thay thế" cửa sổ trình chỉnh sửa.

Trình chỉnh sửa web cung cấp một cách khác để xử lý các cửa sổ trình chỉnh sửa và game (hiện là các "tab"). Bạn có thể chuyển đổi giữa các tab **Editor** và **Game** bằng các nút ở phía trên. Bạn cũng có thể đóng game hoặc trình chỉnh sửa đang chạy bằng cách nhấp vào nút **×** bên cạnh các tab đó.

Các tệp dự án của tôi ở đâu?
----------------------------

Do các hạn chế về bảo mật của trình duyệt, trình chỉnh sửa sẽ lưu các tệp dự án vào bộ nhớ IndexedDB của trình duyệt. Bộ nhớ này không thể truy cập như một thư mục thông thường trên máy của bạn mà được trừu tượng hóa trong một cơ sở dữ liệu.

.. UPDATE: Not supported yet. When exporting from the web editor is supported,
.. update this paragraph.

Bạn có thể tải các tệp dự án xuống dưới dạng một tệp lưu trữ ZIP bằng cách sử dụng **Project > Tools > Download Project Source**. Bạn có thể dùng cách này để export dự án bằng `trình chỉnh sửa Godot native <https://godotengine.org/download>`__, vì hiện chưa hỗ trợ export từ trình chỉnh sửa web.

Trong tương lai, có thể sẽ sử dụng `HTML5 FileSystem API <https://developer.mozilla.org/en-US/docs/Web/API/FileSystem>`__ để lưu các tệp dự án trên hệ thống tệp của người dùng như trình chỉnh sửa native vẫn làm. Tuy nhiên, tính năng này vẫn chưa được triển khai.
