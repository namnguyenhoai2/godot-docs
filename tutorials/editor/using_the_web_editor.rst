:article_outdated: True

.. _doc_using_the_web_editor:

Sử dụng trình chỉnh sửa Web
===========================

Có một `Web editor <https://editor.godotengine.org/>`__ mà bạn có thể sử dụng để làm việc với các dự án mới hoặc hiện có.

.. note::

    Trình chỉnh sửa web hiện đang ở giai đoạn sơ bộ. Mặc dù bộ tính năng của nó có thể đủ cho mục đích giáo dục, hiện tại **không được khuyến nghị sử dụng cho công việc production**. Xem :ref:`doc_using_the_web_editor_limitations` bên dưới.

Hỗ trợ trình duyệt
------------------

Trình chỉnh sửa Web yêu cầu WebAssembly hỗ trợ SharedArrayBuffer. Đây cũng là yêu cầu cần thiết để hỗ trợ threading trong trình duyệt.

Xem :ref:`doc_system_requirements` để biết danh sách các trình duyệt web được hỗ trợ. Các trình duyệt trên thiết bị di động được hỗ trợ, nhưng sẽ không mang lại trải nghiệm lý tưởng do các hạn chế về hiệu năng và phương thức nhập liệu.

Trình chỉnh sửa web chỉ hỗ trợ renderer Compatibility, vì hiện chưa có cách ổn định để chạy các ứng dụng Vulkan trên web.

.. note::

    Nếu gặp vấn đề về hiệu năng trên Firefox, hãy thử sử dụng trình duyệt dựa trên Chromium vì chúng có thể hoạt động tốt hơn trong các ứng dụng WebGL.

.. _doc_using_the_web_editor_limitations:

Hạn chế
-------

Do các hạn chế ở phía Godot hoặc nền tảng Web, hiện đang thiếu các tính năng sau:

- Không hỗ trợ C#/Mono. - Không hỗ trợ GDExtension. - Không hỗ trợ debugging. Điều này có nghĩa là debugging/profiling GDScript, chỉnh sửa scene trực tiếp, dock Remote Scene tree và các tính năng khác dựa trên debugger protocol sẽ không hoạt động. - Không hỗ trợ exporting project. Để khắc phục, bạn có thể tải source project xuống bằng **Project > Tools > Download Project Source** rồi export bằng một `native version of the Godot editor <https://godotengine.org/download>`__. - Trình chỉnh sửa sẽ không cảnh báo khi bạn đóng tab trong lúc có các thay đổi chưa được lưu. - Không hỗ trợ lightmap baking. Bạn vẫn có thể sử dụng các lightmap hiện có nếu chúng được bake bằng phiên bản Godot editor native (ví dụ: bằng cách import một project hiện có).

Các tính năng sau đây khó có khả năng được hỗ trợ do những hạn chế cố hữu của nền tảng Web:

- Không hỗ trợ các trình chỉnh sửa script bên ngoài. - Không hỗ trợ one-click deploy cho Android.

.. seealso::

    Xem `list of open issues on GitHub related to the web editor <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Aplatform%3Aweb+label%3Atopic%3Aeditor>`__ để biết danh sách các lỗi đã biết.

Import một project
------------------

Để import một project hiện có, quy trình hiện tại như sau:

- Chỉ định một tệp ZIP để preload vào HTML5 filesystem bằng input **Preload project ZIP**. - Chạy trình chỉnh sửa bằng cách nhấp vào **Start Godot editor**. Godot Project Manager sẽ xuất hiện sau 10-20 giây. Trên các máy hoặc kết nối chậm hơn, quá trình tải có thể mất tối đa một phút. - Trong hộp thoại xuất hiện ở giữa cửa sổ, chỉ định tên cho thư mục cần tạo rồi nhấp vào nút **Create Folder** (tên này không nhất thiết phải trùng với tên của ZIP archive). - Nhấp vào **Install & Edit** và project sẽ mở trong trình chỉnh sửa.

.. attention::

    Điều quan trọng là đặt thư mục project ở đâu đó trong ``/home/web_user/``. Nếu thư mục project được đặt bên ngoài ``/home/web_user/``, bạn sẽ mất project khi đóng trình chỉnh sửa!

    Khi làm theo các bước được mô tả ở trên, thư mục project sẽ luôn nằm trong ``/home/web_user/projects``, giúp bảo toàn project.

Chỉnh sửa và chạy một project
-----------------------------

Không giống phiên bản native của Godot, trình chỉnh sửa web bị giới hạn trong một cửa sổ duy nhất. Do đó, trình chỉnh sửa không thể mở một cửa sổ mới khi chạy project. Thay vào đó, khi chạy project bằng cách nhấp vào nút Run hoặc nhấn
:kbd:`F5`, it will appear to "replace" the editor window.

Trình chỉnh sửa web cung cấp một cách khác để xử lý các cửa sổ trình chỉnh sửa và game (hiện là các "tab"). Bạn có thể chuyển đổi giữa các tab **Editor** và **Game** bằng các nút ở phía trên. Bạn cũng có thể đóng game hoặc trình chỉnh sửa đang chạy bằng cách nhấp vào nút **×** bên cạnh các tab đó.

Các tệp project của tôi ở đâu?
------------------------------

Do các hạn chế về bảo mật của trình duyệt, trình chỉnh sửa sẽ lưu các tệp project vào bộ nhớ IndexedDB của trình duyệt. Bộ nhớ này không thể được truy cập như một thư mục thông thường trên máy của bạn, mà được trừu tượng hóa trong một cơ sở dữ liệu.

.. CẬP NHẬT: Chưa được hỗ trợ. Khi việc export từ trình chỉnh sửa web được hỗ trợ, .. cập nhật đoạn này.

Bạn có thể tải các tệp project xuống dưới dạng ZIP archive bằng cách sử dụng **Project > Tools > Download Project Source**. Bạn có thể dùng cách này để export project bằng một `native Godot editor <https://godotengine.org/download>`__, vì việc export từ trình chỉnh sửa web hiện chưa được hỗ trợ.

Trong tương lai, có thể sẽ có khả năng sử dụng `HTML5 FileSystem API <https://developer.mozilla.org/en-US/docs/Web/API/FileSystem>`__ để lưu các tệp project trên filesystem của người dùng như trình chỉnh sửa native vẫn làm. Tuy nhiên, tính năng này vẫn chưa được triển khai.
