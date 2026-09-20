.. _doc_compiling_for_web:

Biên dịch cho Web
=================

.. seealso::

    Trang này mô tả cách biên dịch trình chỉnh sửa HTML5 và các tệp nhị phân mẫu xuất từ mã nguồn. Nếu bạn muốn xuất dự án của mình sang HTML5, hãy đọc :ref:`doc_exporting_for_web`.

.. highlight:: shell

Yêu cầu
-------

Để biên dịch các mẫu xuất cho Web, cần có những thành phần sau:

- `Emscripten 4.0.0+ <https://emscripten.org>`__. - `Python 3.9+ <https://www.python.org/>`__. - hệ thống xây dựng `SCons 4.4+ <https://scons.org/pages/download.html>`__.

.. seealso:: To get the Godot source code for compiling, see
             :ref:`doc_getting_source`.

             Để xem tổng quan chung về cách sử dụng SCons cho Godot, hãy xem
             :ref:`doc_introduction_to_the_buildsystem`.

Xây dựng các mẫu xuất
---------------------

Trước khi bắt đầu, hãy xác nhận rằng ``emcc`` có trong PATH của bạn. Thông thường, điều này được cấu hình bởi Emscripten SDK, chẳng hạn khi gọi ``emsdk activate`` và ``source ./emsdk_env.sh``/``emsdk_env.bat``.

Mở một terminal và chuyển đến thư mục gốc của mã nguồn engine. Sau đó, yêu cầu SCons xây dựng nền tảng Web. Chỉ định ``target`` là ``template_release`` cho bản dựng phát hành hoặc ``template_debug`` cho bản dựng gỡ lỗi:

::

    scons platform=web target=template_release
    scons platform=web target=template_debug

Theo mặc định, :ref:`JavaScriptBridge singleton <doc_web_javascript_bridge>` sẽ được xây dựng vào engine. Các mẫu xuất chính thức cũng bật singleton JavaScript. Vì các lệnh gọi ``eval()`` có thể gây ra vấn đề bảo mật, có thể sử dụng tùy chọn ``javascript_eval`` để xây dựng mà không có singleton:

::

    scons platform=web target=template_release javascript_eval=no
    scons platform=web target=template_debug javascript_eval=no

Theo mặc định, hỗ trợ các luồng WebWorker được bật. Để tắt tính năng này và chỉ sử dụng một luồng, có thể dùng tùy chọn ``threads`` để xây dựng mẫu web không có hỗ trợ luồng:

::

    scons platform=web target=template_release threads=no
    scons platform=web target=template_debug threads=no

Engine giờ đây sẽ được Emscripten biên dịch sang WebAssembly. Khi hoàn tất, tệp kết quả sẽ được đặt trong thư mục con ``bin``. Tên của tệp là ``godot.web.template_release.wasm32.zip`` đối với bản phát hành hoặc ``godot.web.template_debug.wasm32.zip`` đối với bản gỡ lỗi.

Cuối cùng, đổi tên tệp lưu trữ zip thành ``web_release.zip`` cho mẫu phát hành:

::

    mv bin/godot.web.template_release.wasm32.zip bin/web_release.zip

Và ``web_debug.zip`` cho mẫu gỡ lỗi:

::

    mv bin/godot.web.template_debug.wasm32.zip bin/web_debug.zip

GDExtension
-----------

Các mẫu xuất mặc định không bao gồm hỗ trợ GDExtension vì lý do hiệu năng và khả năng tương thích. Hãy xem
:ref:`export page <doc_javascript_export_options>` for more info.

Bạn có thể xây dựng các mẫu xuất bằng tùy chọn ``dlink_enabled=yes`` để bật hỗ trợ GDExtension:

::

    scons platform=web dlink_enabled=yes target=template_release
    scons platform=web dlink_enabled=yes target=template_debug

Khi hoàn tất, tệp kết quả sẽ được đặt trong thư mục con ``bin``. Tên của tệp sẽ được thêm ``_dlink``.

Cuối cùng, đổi tên các tệp lưu trữ zip thành ``web_dlink_release.zip`` và ``web_dlink_release.zip`` cho mẫu phát hành:

::

    mv bin/godot.web.template_release.wasm32.dlink.zip bin/web_dlink_release.zip
    mv bin/godot.web.template_debug.wasm32.dlink.zip bin/web_dlink_debug.zip

Xây dựng trình chỉnh sửa
------------------------

Bạn cũng có thể xây dựng một phiên bản trình chỉnh sửa Godot có thể chạy trong trình duyệt. Không nên sử dụng phiên bản trình chỉnh sửa này thay cho bản dựng gốc. Bạn có thể xây dựng trình chỉnh sửa bằng:

::

    scons platform=web target=editor

Khi hoàn tất, tệp kết quả sẽ được đặt trong thư mục con ``bin``. Tên của tệp sẽ là ``godot.web.editor.wasm32.zip``. Bạn có thể tải nội dung tệp zip lên máy chủ web của mình và truy cập bằng trình duyệt để sử dụng trình chỉnh sửa.

Tham khảo :ref:`export page <doc_javascript_export_options>` để biết các yêu cầu đối với máy chủ web.

.. tip::

    Kho lưu trữ Godot bao gồm một `Tập lệnh Python để lưu trữ máy chủ web cục bộ <https://raw.githubusercontent.com/godotengine/godot/master/platform/web/serve.py>`__. Có thể dùng tập lệnh này để kiểm thử trình chỉnh sửa web trên máy cục bộ.

    Sau khi biên dịch trình chỉnh sửa, hãy giải nén tệp lưu trữ ZIP được tạo trong thư mục ``bin/``, sau đó chạy lệnh sau trong thư mục gốc của kho lưu trữ Godot:

    ::

        # You may need to replace `python` with `python3` on some platforms.
        python platform/web/serve.py

    Lệnh này sẽ cung cấp nội dung của thư mục ``bin/`` và tự động mở trình duyệt web mặc định. Trong trang được mở, truy cập ``godot.editor.html`` và bạn sẽ có thể kiểm thử trình chỉnh sửa web theo cách này.

    Lưu ý rằng không nên sử dụng máy chủ web dựa trên Python này cho các trường hợp sử dụng trong môi trường production. Thay vào đó, bạn nên sử dụng một máy chủ web đã được thiết lập như Apache hoặc nginx.
