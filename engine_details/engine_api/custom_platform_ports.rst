.. _doc_custom_platform_ports:

Các port nền tảng tùy chỉnh
===========================

Tương tự như :ref:`doc_custom_modules_in_cpp`, kiến trúc đa nền tảng của Godot được thiết kế để cho phép tạo các port nền tảng mà không cần sửa đổi bất kỳ mã nguồn hiện có nào.

Một ví dụ về port nền tảng tùy chỉnh được phân phối độc lập với engine là `FRT <https://github.com/efornara/frt>`__, nhắm đến các máy tính bo mạch đơn. Lưu ý rằng port nền tảng này hiện nhắm đến Godot 3.x; do đó, nó không sử dụng abstraction :ref:`class_DisplayServer` mới có trong Godot 4.

Một số lý do để tạo port nền tảng tùy chỉnh có thể là:

- Bạn muốn port game của mình sang console (xem thêm `trang web Godot về hỗ trợ console <https://godotengine.org/consoles/>`_), nhưng muốn tự viết platform layer. Đây là một quá trình dài và gian nan vì yêu cầu ký NDA với các nhà sản xuất console, nhưng cho phép bạn toàn quyền kiểm soát quá trình port sang console.
- Bạn muốn port Godot sang một nền tảng đặc thù hiện chưa được hỗ trợ.

Nếu bạn có câu hỏi về việc tạo port nền tảng tùy chỉnh, hãy thoải mái đặt câu hỏi trong kênh ``#platforms`` của `Godot Contributors Chat <https://chat.godotengine.org/channel/platforms>`__.

.. note::

    Godot là một engine hiện đại với các yêu cầu hiện đại. Ngay cả khi bạn chỉ định chạy các project 2D đơn giản trên nền tảng đích, engine vẫn yêu cầu lượng bộ nhớ khiến việc chạy trên hầu hết các console retro trở nên không khả thi. Để tham khảo, trong Godot 4, một project trống không hiển thị gì cần khoảng 100 MB RAM để chạy trên Linux (50 MB ở chế độ headless).

    Nếu muốn chạy Godot trên các nền tảng bị giới hạn nghiêm ngặt về bộ nhớ, các phiên bản Godot cũ hơn có yêu cầu bộ nhớ thấp hơn. Quá trình port tương tự, ngoại trừ việc :ref:`class_DisplayServer` không được tách khỏi singleton :ref:`class_OS`.

Các port nền tảng chính thức
----------------------------

Có thể sử dụng các port nền tảng chính thức làm tài liệu tham khảo khi tạo port nền tảng tùy chỉnh:

- `Windows <https://github.com/godotengine/godot/tree/master/platform/windows>`__
- `macOS <https://github.com/godotengine/godot/tree/master/platform/macos>`__
- `Linux/\*BSD <https://github.com/godotengine/godot/tree/master/platform/linuxbsd>`__
- `Android <https://github.com/godotengine/godot/tree/master/platform/android>`__
- `iOS <https://github.com/godotengine/godot/tree/master/platform/ios>`__
- `Web <https://github.com/godotengine/godot/tree/master/platform/web>`__

Mặc dù mã nền tảng thường được tự chứa, vẫn có những ngoại lệ đối với quy tắc này. Ví dụ, các audio driver được chia sẻ giữa nhiều nền tảng và các rendering driver nằm trong `thư mục drivers/ <https://github.com/godotengine/godot/tree/master/drivers>`__ của mã nguồn Godot.

Tạo port nền tảng tùy chỉnh
---------------------------

Tạo một port nền tảng tùy chỉnh là một công việc lớn, đòi hỏi kiến thức trước đó về SDK của nền tảng. Tùy thuộc vào các tính năng bạn cần, khối lượng công việc cần thiết sẽ khác nhau:

Các tính năng bắt buộc của port nền tảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tối thiểu, một port nền tảng phải triển khai các method từ singleton :ref:`class_OS` để có thể build và sử dụng cho hoạt động headless. Một vector image ``logo.svg`` (32×32) cũng phải có trong thư mục nền tảng. Logo này được hiển thị trong hộp thoại Export cho mỗi export preset nhắm đến nền tảng tương ứng.

Xem `implementation này <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/os_linuxbsd.cpp>`__ của nền tảng Linux/\*BSD làm ví dụ. Đồng thời xem `header của singleton OS <https://github.com/godotengine/godot/blob/master/core/os/os.h>`__ để tham khảo.

.. note::

    Nếu nền tảng đích của bạn giống UNIX, hãy cân nhắc kế thừa từ ``OS_Unix`` class để tự động hoàn thành phần lớn công việc.

    Nếu nền tảng không giống UNIX, bạn có thể dùng `Windows port <https://github.com/godotengine/godot/blob/master/platform/windows/os_windows.cpp>`__ làm tài liệu tham khảo.

**tệp detect.py**

Phải tạo một ``detect.py`` file trong thư mục của nền tảng với tất cả các method đã được triển khai. Tệp này cần thiết để SCons phát hiện nền tảng là một tùy chọn hợp lệ khi biên dịch. Xem `tệp detect.py <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/detect.py>`__ của nền tảng Linux/\*BSD làm ví dụ.

Tất cả các method phải được triển khai trong ``detect.py`` như sau:

- ``is_active()``: Có thể được dùng để tạm thời vô hiệu hóa việc build cho một nền tảng. Thông thường, method này luôn phải trả về ``True``.
- ``get_name()``: Trả về tên hiển thị với người dùng của nền tảng dưới dạng chuỗi.
- ``can_build()``: Trả về ``True`` nếu hệ thống host có thể build cho nền tảng đích, ngược lại trả về ``False``. Không thực hiện các kiểm tra chậm ở đây vì method này được truy vấn khi người dùng yêu cầu danh sách nền tảng. Thay vào đó, hãy dùng ``configure()`` cho các kiểm tra dependency mở rộng.
- ``get_opts()``: Trả về danh sách các tùy chọn build SCons mà người dùng có thể định nghĩa cho nền tảng này.
- ``get_flags()``: Trả về danh sách các cờ SCons bị override cho nền tảng này.
- ``configure()``: Thực hiện cấu hình build, chẳng hạn như chọn các tùy chọn compiler tùy theo những tùy chọn SCons đã chọn.

Các tính năng tùy chọn của port nền tảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trên thực tế, hoạt động headless là chưa đủ nếu bạn muốn thấy nội dung trên màn hình và xử lý các thiết bị input. Với hầu hết game, bạn cũng có thể cần audio output.

*Một số liên kết trong danh sách này trỏ đến implementation của nền tảng Linux/\*BSD để tham khảo.*

- Một hoặc nhiều `DisplayServers <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/display_server_x11.cpp>`__, với các method windowing đã được triển khai. DisplayServer cũng bao gồm các tính năng như hỗ trợ chuột, hỗ trợ touchscreen và tablet driver (cho input bằng bút). Xem `header của singleton DisplayServer <https://github.com/godotengine/godot/blob/master/servers/display_server.h>`__ để tham khảo.

  - Đối với các nền tảng không có hỗ trợ windowing đầy đủ (hoặc nếu tính năng này không liên quan đến port bạn đang tạo), hầu hết các hàm windowing có thể gần như không cần triển khai. Có thể để các hàm này chỉ kiểm tra xem window ID có phải là ``MAIN_WINDOW_ID`` hay không, và các thao tác cụ thể như thay đổi kích thước có thể gắn với tính năng độ phân giải màn hình của nền tảng (nếu phù hợp). Có thể từ chối mọi nỗ lực tạo hoặc thao tác với các window ID khác.
- *Nếu nền tảng đích hỗ trợ các graphics API tương ứng:* Rendering context cho `Vulkan <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/rendering_context_driver_vulkan_x11.cpp>`__, `Direct3D 12 <https://github.com/godotengine/godot/blob/master/drivers/d3d12/rendering_context_driver_d3d12.cpp>`__ `OpenGL 3.3 hoặc OpenGL ES 3.0 <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/gl_manager_x11.cpp>`__.
- Các input handler cho `keyboard <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/key_mapping_x11.cpp>`__ và `controller <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/joypad_linux.cpp>`__.
- Một hoặc nhiều `trình điều khiển âm thanh <https://github.com/godotengine/godot/blob/master/drivers/pulseaudio/audio_driver_pulseaudio.cpp>`__. Trình điều khiển âm thanh có thể nằm trong thư mục ``platform/`` (cách này được sử dụng cho các nền tảng Android và Web), hoặc trong thư mục ``drivers/`` nếu nhiều nền tảng có thể sử dụng trình điều khiển âm thanh này. Xem `tệp tiêu đề singleton AudioServer <https://github.com/godotengine/godot/blob/master/servers/audio_server.h>`__ để tham khảo.
- `Bộ xử lý sự cố <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/crash_handler_linuxbsd.cpp>`__, dùng để in backtrace khi game bị crash. Điều này giúp việc khắc phục sự cố dễ dàng hơn trên các nền tảng mà log không dễ truy cập.
- `Trình điều khiển chuyển văn bản thành giọng nói <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/tts_linux.cpp>`__ (cho khả năng tiếp cận).
- `Bộ xử lý export <https://github.com/godotengine/godot/tree/master/platform/linuxbsd/export>`__ (để export từ editor, bao gồm :ref:`doc_one-click_deploy`). Không bắt buộc nếu bạn chỉ định export PCK từ editor, sau đó chạy trực tiếp binary export template bằng cách đổi tên nó để khớp với tên tệp PCK. Xem `tệp tiêu đề EditorExportPlatform <https://github.com/godotengine/godot/blob/master/editor/export/editor_export_platform.h>`__ để tham khảo. ``run_icon.svg`` (16×16) phải nằm trong thư mục nền tảng nếu
  :ref:`doc_one-click_deploy` được triển khai cho nền tảng đích. Biểu tượng này được hiển thị ở đầu editor khi one-click deploy được thiết lập cho nền tảng đích.

Nếu nền tảng đích không hỗ trợ chạy Vulkan, Direct3D 12, OpenGL 3.3 hoặc OpenGL ES 3.0, bạn có hai lựa chọn:

- Sử dụng một thư viện trong runtime để chuyển các lệnh gọi Vulkan hoặc OpenGL sang một graphics API khác. Ví dụ: `MoltenVK <https://moltengl.com/moltenvk/>`__ được sử dụng trên macOS để chuyển Vulkan sang Metal trong runtime.
- Tạo một renderer mới từ đầu. Đây là một công việc lớn, đặc biệt nếu bạn muốn hỗ trợ cả rendering 2D và 3D với các tính năng nâng cao.

Phân phối một bản port nền tảng tùy chỉnh
-----------------------------------------

.. danger::

    Trước khi phân phối một bản port nền tảng tùy chỉnh, hãy đảm bảo bạn được phép phân phối toàn bộ mã được liên kết. SDK console thường chịu các NDA, ngăn việc phân phối lại cho công chúng.

Các bản port nền tảng được thiết kế để tự chứa nhiều nhất có thể. Phần lớn mã có thể được giữ trong một thư mục duy nhất nằm tại ``platform/``. Như
:ref:`doc_custom_modules_in_cpp`, điều này giúp đơn giản hóa quy trình build bằng cách cho phép bạn ``git clone`` một thư mục nền tảng trong thư mục ``platform/`` của bản clone repository Godot, sau đó chạy ``scons platform=<name>``. Không cần thực hiện thêm bước nào để build, trừ khi trước tiên cần cài đặt các dependency dành riêng cho nền tảng của bên thứ ba.

Tuy nhiên, khi cần một trình điều khiển rendering tùy chỉnh, phải thêm một thư mục khác trong ``drivers/``. Trong trường hợp này, bản port nền tảng có thể được phân phối dưới dạng fork của repository Godot hoặc dưới dạng một tập hợp gồm nhiều thư mục có thể được thêm vào bản clone Git repository Godot.

.. _`Godot website on console support`: https://godotengine.org/consoles/
