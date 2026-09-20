.. _doc_custom_platform_ports:

Các bản chuyển nền tảng tùy chỉnh
=================================

Tương tự như :ref:`doc_custom_modules_in_cpp`, kiến trúc đa nền tảng của Godot được thiết kế theo cách cho phép tạo các bản chuyển nền tảng mà không cần sửa đổi bất kỳ mã nguồn hiện có nào.

Một ví dụ về bản chuyển nền tảng tùy chỉnh được phân phối độc lập với engine là `FRT <https://github.com/efornara/frt>`__, nhắm đến các máy tính bo mạch đơn. Lưu ý rằng bản chuyển nền tảng này hiện nhắm đến Godot 3.x; do đó, nó không sử dụng lớp trừu tượng :ref:`class_DisplayServer` mới có trong Godot 4.

Một số lý do để tạo bản chuyển nền tảng tùy chỉnh có thể là:

- Bạn muốn chuyển trò chơi của mình sang console (xem thêm `trang web Godot về hỗ trợ console <https://godotengine.org/consoles/>`_), nhưng muốn tự viết lớp nền tảng. Đây là một quá trình dài và gian nan vì cần ký NDA với các nhà sản xuất console, nhưng cho phép bạn toàn quyền kiểm soát quá trình chuyển sang console. - Bạn muốn chuyển Godot sang một nền tảng đặc thù hiện chưa được hỗ trợ.

Nếu có câu hỏi về việc tạo bản chuyển nền tảng tùy chỉnh, bạn có thể hỏi trong kênh ``#platforms`` của `Godot Contributors Chat <https://chat.godotengine.org/channel/platforms>`__.

.. note::

    Godot là một engine hiện đại với các yêu cầu hiện đại. Ngay cả khi bạn chỉ định chạy các dự án 2D đơn giản trên nền tảng đích, nó vẫn yêu cầu lượng bộ nhớ khiến việc chạy trên hầu hết các console cổ điển trở nên không khả thi. Để tham khảo, trong Godot 4, một dự án trống không hiển thị gì cần khoảng 100 MB RAM để chạy trên Linux (50 MB ở chế độ headless).

    Nếu muốn chạy Godot trên các nền tảng bị giới hạn bộ nhớ nghiêm ngặt, các phiên bản Godot cũ hơn có yêu cầu bộ nhớ thấp hơn. Quy trình chuyển nền tảng tương tự, ngoại trừ việc :ref:`class_DisplayServer` không được tách khỏi singleton :ref:`class_OS`.

Các bản chuyển nền tảng chính thức
----------------------------------

Có thể dùng các bản chuyển nền tảng chính thức làm tài liệu tham khảo khi tạo bản chuyển nền tảng tùy chỉnh:

- `Windows <https://github.com/godotengine/godot/tree/master/platform/windows>`__ - `macOS <https://github.com/godotengine/godot/tree/master/platform/macos>`__ - `Linux/\*BSD <https://github.com/godotengine/godot/tree/master/platform/linuxbsd>`__ - `Android <https://github.com/godotengine/godot/tree/master/platform/android>`__ - `iOS <https://github.com/godotengine/godot/tree/master/platform/ios>`__ - `Web <https://github.com/godotengine/godot/tree/master/platform/web>`__

Mặc dù mã nền tảng thường độc lập và khép kín, vẫn có ngoại lệ cho quy tắc này. Chẳng hạn, các trình điều khiển âm thanh được chia sẻ giữa nhiều nền tảng và các trình điều khiển kết xuất nằm trong `thư mục drivers/ <https://github.com/godotengine/godot/tree/master/drivers>`__ của mã nguồn Godot.

Tạo bản chuyển nền tảng tùy chỉnh
---------------------------------

Tạo một bản chuyển nền tảng tùy chỉnh là một công việc lớn, đòi hỏi phải có kiến thức trước về các SDK của nền tảng. Tùy thuộc vào những tính năng bạn cần, khối lượng công việc sẽ thay đổi:

Các tính năng bắt buộc của bản chuyển nền tảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Tối thiểu, một bản chuyển nền tảng phải triển khai các phương thức từ singleton :ref:`class_OS` để có thể build và sử dụng cho hoạt động headless. Một ảnh vector ``logo.svg`` (32×32) cũng phải có trong thư mục nền tảng. Logo này được hiển thị trong hộp thoại Export cho mỗi cấu hình export nhắm đến nền tảng tương ứng.

Xem `phần triển khai này <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/os_linuxbsd.cpp>`__ của nền tảng Linux/\*BSD làm ví dụ. Đồng thời xem `tiêu đề singleton OS <https://github.com/godotengine/godot/blob/master/core/os/os.h>`__ để tham khảo.

.. note::

    Nếu nền tảng đích của bạn tương tự UNIX, hãy cân nhắc kế thừa từ lớp ``OS_Unix`` để tự động hoàn thành phần lớn công việc.

    Nếu nền tảng không tương tự UNIX, bạn có thể dùng `bản chuyển Windows <https://github.com/godotengine/godot/blob/master/platform/windows/os_windows.cpp>`__ làm tài liệu tham khảo.

**tệp detect.py**

Phải tạo một tệp ``detect.py`` trong thư mục của nền tảng, với tất cả các phương thức được triển khai. Tệp này cần thiết để SCons phát hiện nền tảng là một tùy chọn hợp lệ khi biên dịch. Xem `tệp detect.py <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/detect.py>`__ của nền tảng Linux/\*BSD làm ví dụ.

Tất cả các phương thức phải được triển khai trong ``detect.py`` như sau:

- ``is_active()``: Có thể dùng để tạm thời vô hiệu hóa việc build cho một nền tảng. Thông thường, phương thức này luôn phải trả về ``True``. - ``get_name()``: Trả về tên hiển thị với người dùng của nền tảng dưới dạng chuỗi. - ``can_build()``: Trả về ``True`` nếu hệ thống máy chủ có thể build cho nền tảng đích, nếu không thì trả về ``False``. Không thực hiện các kiểm tra chậm ở đây, vì phương thức này được truy vấn khi người dùng yêu cầu danh sách nền tảng. Thay vào đó, hãy dùng ``configure()`` cho các kiểm tra phụ thuộc mở rộng. - ``get_opts()``: Trả về danh sách các tùy chọn build của SCons mà người dùng có thể định nghĩa cho nền tảng này. - ``get_flags()``: Trả về danh sách các cờ SCons bị ghi đè cho nền tảng này. - ``configure()``: Thực hiện cấu hình build, chẳng hạn như chọn các tùy chọn trình biên dịch tùy theo các tùy chọn SCons đã chọn.

Các tính năng tùy chọn của bản chuyển nền tảng
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Trên thực tế, hoạt động headless là chưa đủ nếu bạn muốn nhìn thấy bất kỳ thứ gì trên màn hình và xử lý các thiết bị đầu vào. Với hầu hết trò chơi, bạn cũng có thể muốn có đầu ra âm thanh.

*Một số liên kết trong danh sách này trỏ đến phần triển khai nền tảng Linux/\*BSD để tham khảo.*

- Một hoặc nhiều `DisplayServers <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/display_server_x11.cpp>`__, với các phương thức quản lý cửa sổ được triển khai. DisplayServer cũng bao gồm các tính năng như hỗ trợ chuột, hỗ trợ màn hình cảm ứng và trình điều khiển máy tính bảng (cho đầu vào bằng bút). Xem `tiêu đề singleton DisplayServer <https://github.com/godotengine/godot/blob/master/servers/display_server.h>`__ để tham khảo.

  - Đối với các nền tảng không có hỗ trợ quản lý cửa sổ đầy đủ (hoặc nếu điều đó không liên quan đến bản chuyển nền tảng bạn đang tạo), hầu hết các hàm quản lý cửa sổ có thể được để gần như chưa triển khai. Các hàm này chỉ cần kiểm tra xem ID cửa sổ có phải là ``MAIN_WINDOW_ID`` hay không; các thao tác cụ thể như thay đổi kích thước có thể gắn với tính năng độ phân giải màn hình của nền tảng (nếu phù hợp). Mọi nỗ lực tạo hoặc thao tác với các ID cửa sổ khác đều có thể bị từ chối. - *Nếu nền tảng đích hỗ trợ các API đồ họa tương ứng:* Ngữ cảnh kết xuất cho `Vulkan <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/rendering_context_driver_vulkan_x11.cpp>`__, `Direct3D 12 <https://github.com/godotengine/godot/blob/master/drivers/d3d12/rendering_context_driver_d3d12.cpp>`__ `OpenGL 3.3 or OpenGL ES 3.0 <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/gl_manager_x11.cpp>`__. - Trình xử lý đầu vào cho `keyboard <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/x11/key_mapping_x11.cpp>`__ và `controller <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/joypad_linux.cpp>`__. - Một hoặc nhiều `audio drivers <https://github.com/godotengine/godot/blob/master/drivers/pulseaudio/audio_driver_pulseaudio.cpp>`__. Trình điều khiển âm thanh có thể nằm trong thư mục ``platform/`` (cách này được dùng cho các nền tảng Android và Web), hoặc trong thư mục ``drivers/`` nếu nhiều nền tảng có thể sử dụng trình điều khiển âm thanh này. Xem `tiêu đề singleton AudioServer <https://github.com/godotengine/godot/blob/master/servers/audio_server.h>`__ để tham khảo. - `Crash handler <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/crash_handler_linuxbsd.cpp>`__, dùng để in backtrace của sự cố khi trò chơi gặp sự cố. Điều này giúp khắc phục sự cố dễ dàng hơn trên các nền tảng không dễ truy cập nhật ký. - `Text-to-speech driver <https://github.com/godotengine/godot/blob/master/platform/linuxbsd/tts_linux.cpp>`__ (cho khả năng tiếp cận). - `Export handler <https://github.com/godotengine/godot/tree/master/platform/linuxbsd/export>`__ (để export từ trình chỉnh sửa, bao gồm :ref:`doc_one-click_deploy`). Không bắt buộc nếu bạn chỉ định export PCK từ trình chỉnh sửa, sau đó chạy trực tiếp tệp nhị phân export template bằng cách đổi tên nó để khớp với tệp PCK. Xem `tiêu đề EditorExportPlatform <https://github.com/godotengine/godot/blob/master/editor/export/editor_export_platform.h>`__ để tham khảo. ``run_icon.svg`` (16×16) phải có trong thư mục nền tảng nếu
  :ref:`doc_one-click_deploy` is implemented for the target platform. This icon
  được hiển thị ở đầu trình chỉnh sửa khi one-click deploy được thiết lập cho nền tảng đích.

Nếu nền tảng đích không hỗ trợ chạy Vulkan, Direct3D 12, OpenGL 3.3 hoặc OpenGL ES 3.0, bạn có hai lựa chọn:

- Sử dụng một thư viện trong thời gian chạy để chuyển đổi các lời gọi Vulkan hoặc OpenGL sang một API đồ họa khác. Ví dụ, `MoltenVK <https://moltengl.com/moltenvk/>`__ được dùng trên macOS để chuyển Vulkan sang Metal trong thời gian chạy. - Tạo một trình kết xuất mới từ đầu. Đây là một công việc lớn, đặc biệt nếu bạn muốn hỗ trợ cả kết xuất 2D và 3D với các tính năng nâng cao.

Phân phối bản chuyển nền tảng tùy chỉnh
---------------------------------------

.. danger::

    Trước khi phân phối một bản chuyển nền tảng tùy chỉnh, hãy đảm bảo rằng bạn được phép phân phối toàn bộ mã được liên kết. Các SDK dành cho console thường thuộc NDA, ngăn việc phân phối công khai.

Các bản chuyển nền tảng được thiết kế để tự chứa nhiều nhất có thể. Phần lớn mã có thể được giữ trong một thư mục duy nhất nằm trong ``platform/``. Giống như
:ref:`doc_custom_modules_in_cpp`, this allows for streamlining the build process
bằng cách cho phép bạn ``git clone`` một thư mục nền tảng trong thư mục ``platform/`` của bản sao clone kho lưu trữ Godot, sau đó chạy ``scons platform=<name>``. Không cần thêm bước nào để build, trừ khi trước tiên cần cài đặt các phần phụ thuộc dành riêng cho nền tảng của bên thứ ba.

Tuy nhiên, khi cần một trình điều khiển kết xuất tùy chỉnh, phải thêm một thư mục khác vào ``drivers/``. Trong trường hợp này, bản chuyển nền tảng có thể được phân phối dưới dạng một fork của kho lưu trữ Godot, hoặc dưới dạng một tập hợp gồm nhiều thư mục có thể thêm vào bản sao clone của kho lưu trữ Git Godot.
