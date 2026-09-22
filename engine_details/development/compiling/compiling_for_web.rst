.. _doc_compiling_for_web:

Biên dịch cho Web
=================

.. seealso::

    Trang này mô tả cách biên dịch các tệp nhị phân của trình chỉnh sửa HTML5 và template export từ mã nguồn. Nếu bạn muốn export dự án sang HTML5, hãy đọc :ref:`doc_exporting_for_web`.

.. highlight:: shell

Yêu cầu
-------

Để biên dịch các template export cho Web, cần có những thành phần sau:

- `Emscripten 4.0.0+ <https://emscripten.org>`__.
- `Python 3.9+ <https://www.python.org/>`__.
- Hệ thống build `SCons 4.4+ <https://scons.org/pages/download.html>`__.

.. seealso:: Để lấy mã nguồn Godot nhằm biên dịch, hãy xem
             :ref:`doc_getting_source`.

             Để xem tổng quan về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Build các template export
-------------------------

Trước khi bắt đầu, hãy xác nhận rằng ``emcc`` có sẵn trong PATH. Thông thường, thiết lập này được thực hiện bởi Emscripten SDK, chẳng hạn khi gọi ``emsdk activate`` và ``source ./emsdk_env.sh``/``emsdk_env.bat``.

Mở terminal và chuyển đến thư mục gốc của mã nguồn engine. Sau đó yêu cầu SCons build nền tảng Web. Chỉ định ``target`` là ``template_release`` cho bản build release hoặc ``template_debug`` cho bản build debug:

::

    scons platform=web target=template_release scons platform=web target=template_debug

Theo mặc định, singleton :ref:`JavaScriptBridge <doc_web_javascript_bridge>` sẽ được build vào engine. Các template export chính thức cũng bật singleton JavaScript. Vì các lệnh gọi ``eval()`` có thể gây lo ngại về bảo mật, có thể dùng tùy chọn ``javascript_eval`` để build mà không có singleton:

::

    scons platform=web target=template_release javascript_eval=no scons platform=web target=template_debug javascript_eval=no

Theo mặc định, hỗ trợ các thread WebWorker được bật. Để tắt tính năng này và chỉ sử dụng một thread, có thể dùng tùy chọn ``threads`` để build template web mà không hỗ trợ thread:

::

    scons platform=web target=template_release threads=no scons platform=web target=template_debug threads=no

Engine giờ sẽ được Emscripten biên dịch thành WebAssembly. Sau khi hoàn tất, tệp kết quả sẽ được đặt trong thư mục con ``bin``. Tên của tệp là ``godot.web.template_release.wasm32.zip`` đối với release hoặc ``godot.web.template_debug.wasm32.zip`` đối với debug.

Cuối cùng, đổi tên tệp lưu trữ zip thành ``web_release.zip`` cho template release:

::

    mv bin/godot.web.template_release.wasm32.zip bin/web_release.zip

Và ``web_debug.zip`` cho template debug:

::

    mv bin/godot.web.template_debug.wasm32.zip bin/web_debug.zip

GDExtension
-----------

Các template export mặc định không bao gồm hỗ trợ GDExtension vì lý do hiệu năng và khả năng tương thích. Xem
:ref:`trang export <doc_javascript_export_options>` để biết thêm thông tin.

Bạn có thể build các template export bằng tùy chọn ``dlink_enabled=yes`` để bật hỗ trợ GDExtension:

::

    scons platform=web dlink_enabled=yes target=template_release scons platform=web dlink_enabled=yes target=template_debug

Sau khi hoàn tất, tệp kết quả sẽ được đặt trong thư mục con ``bin``. Tên của tệp sẽ được thêm ``_dlink``.

Cuối cùng, đổi tên các tệp lưu trữ zip thành ``web_dlink_release.zip`` và ``web_dlink_release.zip`` cho template release:

::

    mv bin/godot.web.template_release.wasm32.dlink.zip bin/web_dlink_release.zip mv bin/godot.web.template_debug.wasm32.dlink.zip bin/web_dlink_debug.zip

Build trình chỉnh sửa
---------------------

Bạn cũng có thể build một phiên bản trình chỉnh sửa Godot có thể chạy trong trình duyệt. Không nên sử dụng phiên bản trình chỉnh sửa này thay cho bản build native. Bạn có thể build trình chỉnh sửa bằng lệnh:

::

    scons platform=web target=editor

Sau khi hoàn tất, tệp kết quả sẽ được đặt trong thư mục con ``bin``. Tên của tệp sẽ là ``godot.web.editor.wasm32.zip``. Bạn có thể tải nội dung của tệp zip lên web server rồi truy cập bằng trình duyệt để sử dụng trình chỉnh sửa.

Tham khảo :ref:`trang export <doc_javascript_export_options>` để biết các yêu cầu đối với web server.

.. tip::

    Repository Godot bao gồm `một script Python để lưu trữ web server cục bộ <https://raw.githubusercontent.com/godotengine/godot/master/platform/web/serve.py>`__. Bạn có thể dùng script này để kiểm thử trình chỉnh sửa web cục bộ.

    Sau khi biên dịch trình chỉnh sửa, hãy giải nén tệp lưu trữ ZIP được tạo trong thư mục ``bin/``, rồi chạy lệnh sau trong thư mục gốc của repository Godot:

    ::

        # Trên một số nền tảng, bạn có thể cần thay `python` bằng `python3`. python platform/web/serve.py

    Lệnh này sẽ phục vụ nội dung của thư mục ``bin/`` và tự động mở trình duyệt web mặc định. Trong trang được mở, truy cập ``godot.editor.html`` và bạn sẽ có thể kiểm thử trình chỉnh sửa web theo cách này.

    Lưu ý rằng không nên sử dụng web server dựa trên Python này cho các trường hợp sử dụng trong môi trường production. Thay vào đó, bạn nên dùng một web server phổ biến như Apache hoặc nginx.
