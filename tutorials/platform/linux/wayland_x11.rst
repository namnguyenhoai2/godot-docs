.. _doc_wayland_x11:

Wayland/X11
===========

Tổng quan
---------

Một trong những thành phần quan trọng của mọi hệ điều hành là máy chủ hiển thị. Windows, macOS, iOS, visionOS và Android chỉ cung cấp một tùy chọn. Tuy nhiên, Linux có hai tùy chọn: X11 và Wayland.

X11 là một tiêu chuẩn cũ hơn và đang dần bị phần lớn các bản phân phối Linux loại bỏ để chuyển sang hỗ trợ Wayland, vốn được phát triển nhằm thay thế X11. Wayland hướng đến việc cung cấp các chức năng hiện đại, đồng thời có mô hình bảo mật mạnh mẽ hơn so với X11. Các ứng dụng chạy trên X11 vẫn có thể hoạt động khi bản phân phối sử dụng Wayland nhờ một lớp tương thích có tên là Xwayland.

Việc hỗ trợ Wayland của Godot vẫn đang được phát triển, vì vậy hiện tại X11 vẫn là thiết lập mặc định cho các project. Điều này có thể sẽ thay đổi trong một phiên bản tương lai.

Khi nào nên sử dụng Wayland
---------------------------

Nếu bạn là một engine developer muốn giúp cải thiện khả năng hỗ trợ, hoặc nếu bạn cho rằng Xwayland có thể đang gây ra các lỗi hiển thị trong project đã export của mình vì bất kỳ lý do nào, chúng tôi khuyến nghị bạn sử dụng Wayland. Tuy nhiên, ngoài những trường hợp đó, hiện tại bạn nên tiếp tục sử dụng X11. Điều quan trọng cần lưu ý là mặc dù các ứng dụng X11 có thể chạy trên Wayland, điều ngược lại thì không đúng.

Tính đến tháng 6 năm 2026, hầu hết các bản phân phối phổ biến đều sử dụng Wayland theo mặc định, bao gồm nhưng không giới hạn ở các bản sau:

- SteamOS
- Bazzite
- CachyOS
- Fedora
- Fedora Silverblue
- Ubuntu
- OpenSUSE

Hãy lưu ý rằng với một số bản phân phối như Ubuntu, người dùng có thể đã tự thay đổi máy chủ hiển thị sang X11 theo cách thủ công.

.. _doc_wayland_x11_changing_display_server:

Thay đổi thiết lập máy chủ hiển thị
-----------------------------------

Để đổi máy chủ hiển thị sang Wayland, hãy nhấp vào :menu:`Project > Project Settings`, sau đó đi tới :button:`Display Server` và đổi tùy chọn :button:`driver.linuxbsd` thành ``wayland``.

Bạn cũng có thể tạm thời ghi đè máy chủ hiển thị bằng ``--display-server <x11|wayland>`` :ref:`command line argument <doc_command_line_tutorial>` khi khởi chạy project.

.. note::

    Bất kể máy chủ hiển thị được xác định bằng cách nào, nếu project được cấu hình để sử dụng Wayland, project sẽ tự động chuyển về X11 nếu Wayland không khả dụng.

    Điều này cũng xảy ra theo chiều ngược lại; nếu project được cấu hình để sử dụng X11, project sẽ chuyển về Wayland nếu X11 không khả dụng (tức là khi Xwayland không hiện diện trên hệ thống).

Tắt việc tải libdecor
---------------------

Việc tải `libdecor <https://github.com/neonkore/libdecor>`__ trên Wayland có một số điểm bất thường; tùy vào tình huống, việc tắt tính năng này có thể hữu ích. Để thực hiện, bạn cần đặt biến môi trường ``GODOT_WAYLAND_DISABLE_LIBDECOR`` thành ``1`` như sau:

.. tabs::
 .. code-tab:: gdscript GDScript

    OS.set_environment("GODOT_WAYLAND_DISABLE_LIBDECOR", "1")

Hỗ trợ dải động cao
-------------------

Godot hỗ trợ :ref:`HDR output <doc_hdr_output>` trên Linux kể từ phiên bản 4.7. Tuy nhiên, do các hạn chế của máy chủ hiển thị, HDR output chỉ được hỗ trợ trên Wayland, không được hỗ trợ trên X11 (kể cả thông qua Xwayland).

Do đó, để sử dụng HDR output, bạn phải
:ref:`đặt máy chủ hiển thị thành Wayland <doc_wayland_x11_changing_display_server>`.

.. note::

   Các phiên bản GNOME trước phiên bản 50 có một lỗi khiến HDR output không hoạt động trên Wayland. Nếu đang sử dụng phiên bản GNOME cũ hơn, bạn cần nâng cấp lên phiên bản 50 trở lên để sử dụng HDR output trên Wayland.
