.. _doc_wayland_x11:

Wayland/X11
===========

Tổng quan
---------

Một trong những thành phần quan trọng của bất kỳ hệ điều hành nào là display server. Windows, macOS, iOS, visionOS và Android chỉ cung cấp một tùy chọn. Tuy nhiên, Linux có hai tùy chọn: X11 và Wayland.

X11 là một tiêu chuẩn cũ hơn và đang dần được phần lớn các Linux distribution loại bỏ để chuyển sang hỗ trợ Wayland, vốn được phát triển nhằm thay thế X11. Wayland hướng đến việc cung cấp các chức năng hiện đại, đồng thời có mô hình bảo mật mạnh mẽ hơn so với X11. Các ứng dụng chạy trên X11 vẫn có thể hoạt động khi distribution sử dụng Wayland, nhờ một compatibility layer có tên là Xwayland.

Hỗ trợ Wayland của Godot vẫn đang trong quá trình hoàn thiện, vì vậy hiện tại X11 vẫn là thiết lập mặc định cho các project. Điều này nhiều khả năng sẽ thay đổi trong một phiên bản tương lai.

Khi nào nên sử dụng Wayland
---------------------------

Nếu bạn là engine developer muốn giúp cải thiện khả năng hỗ trợ, hoặc nếu bạn cho rằng Xwayland có thể đang gây ra các lỗi hiển thị trong project đã export của mình vì bất kỳ lý do nào, chúng tôi khuyến nghị bạn sử dụng Wayland. Ngoài những trường hợp đó, hiện tại bạn nên tiếp tục sử dụng X11. Điều quan trọng cần lưu ý là mặc dù các ứng dụng X11 có thể chạy trên Wayland, điều ngược lại thì không đúng.

Tính đến tháng 6 năm 2026, hầu hết các distribution phổ biến đều sử dụng Wayland theo mặc định, bao gồm (nhưng không giới hạn ở) các distribution sau:

- SteamOS - Bazzite - CachyOS - Fedora - Fedora Silverblue - Ubuntu - OpenSUSE

Hãy lưu ý rằng đối với một số distribution như Ubuntu, người dùng có thể đã tự thay đổi display server sang X11 theo cách thủ công.

.. _doc_wayland_x11_changing_display_server:

Thay đổi thiết lập display server
---------------------------------

Để thay đổi display server sang Wayland, hãy nhấp vào :menu:`Project > Project Settings`, sau đó đi đến :button:`Display Server` và thay đổi tùy chọn :button:`driver.linuxbsd` thành ``wayland``.

Bạn cũng có thể tạm thời ghi đè display server bằng ``--display-server <x11|wayland>`` :ref:`command line argument <doc_command_line_tutorial>` khi khởi chạy project.

.. note::

    Bất kể display server được xác định như thế nào, nếu project được cấu hình để sử dụng Wayland, project sẽ tự động chuyển về X11 nếu Wayland không khả dụng.

    Điều này cũng xảy ra theo chiều ngược lại; nếu project được cấu hình để sử dụng X11, project sẽ chuyển về Wayland nếu X11 không khả dụng (tức là khi Xwayland không có trên hệ thống).

Tắt tải libdecor
----------------

`libdecor <https://github.com/neonkore/libdecor>`__ loading trên Wayland có một số điểm bất thường; tùy vào tình huống, việc tắt nó có thể hữu ích. Để thực hiện việc đó, bạn cần đặt biến môi trường ``GODOT_WAYLAND_DISABLE_LIBDECOR`` thành ``1`` như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    OS.set_environment("GODOT_WAYLAND_DISABLE_LIBDECOR", "1")

Hỗ trợ dải tương phản động cao
------------------------------

Godot hỗ trợ :ref:`HDR output <doc_hdr_output>` trên Linux kể từ phiên bản 4.7. Tuy nhiên, do các hạn chế của display server, đầu ra HDR chỉ được hỗ trợ trên Wayland, không phải trên X11 (kể cả thông qua Xwayland).

Do đó, để sử dụng đầu ra HDR, bạn phải
:ref:`set the display server to Wayland <doc_wayland_x11_changing_display_server>`.

.. note::

   Các phiên bản GNOME trước phiên bản 50 có một lỗi khiến đầu ra HDR không hoạt động trên Wayland. Nếu bạn đang sử dụng phiên bản GNOME cũ hơn, bạn sẽ cần nâng cấp lên phiên bản 50 hoặc mới hơn để sử dụng đầu ra HDR trên Wayland.
