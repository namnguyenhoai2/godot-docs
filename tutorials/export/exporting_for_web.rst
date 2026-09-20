.. _doc_exporting_for_web:

Xuất bản cho Web
================

.. seealso::

    Trang này mô tả cách xuất một project Godot sang HTML5. Nếu bạn muốn biên dịch editor hoặc xuất các binary của export template từ mã nguồn, hãy đọc :ref:`doc_compiling_for_web`.

Export HTML5 cho phép xuất bản các game được tạo bằng Godot Engine lên trình duyệt. Việc này yêu cầu trình duyệt của người dùng hỗ trợ `WebAssembly <https://webassembly.org/>`__ và `WebGL 2.0 <https://www.khronos.org/webgl/>`__.

.. attention::

    Các project viết bằng C# sử dụng Godot 4 hiện chưa thể xuất lên web. Xem `this blog post <https://godotengine.org/article/platform-state-in-csharp-for-godot-4-2/#web>`__ để biết thêm thông tin.

    Để sử dụng C# trên các nền tảng web, hãy dùng Godot 3.

.. tip::

    Sử dụng developer console tích hợp trong trình duyệt, thường được mở bằng :kbd:`F12` hoặc :kbd:`Ctrl + Shift + I` (:kbd:`Cmd + Option + I` trên macOS), để xem **thông tin debug** như các lỗi JavaScript, engine và WebGL.

    Nếu phím tắt không hoạt động, đó là vì Godot thực sự bắt đầu vào. Bạn vẫn có thể mở developer console bằng cách truy cập menu của trình duyệt.

.. note::

    Do các vấn đề bảo mật với ``SharedArrayBuffer`` bắt nguồn từ nhiều lỗ hổng, việc sử dụng nhiều thread cho nền tảng Web có nhiều nhược điểm, bao gồm yêu cầu các header cụ thể ở phía server và cross-origin isolation hoàn toàn (nghĩa là không có quảng cáo cũng như tích hợp bên thứ ba trên website lưu trữ game của bạn).

    Kể từ Godot 4.3, Godot hỗ trợ xuất game trên một thread duy nhất, giải quyết được vấn đề này. Mặc dù bản thân nó có một số nhược điểm (không thể sử dụng thread và không có hiệu năng tốt bằng bản export đa thread), nó không yêu cầu nhiều overhead để cài đặt. Nhìn chung, nó cũng tương thích tốt hơn với các store như `itch.io <https://itch.io/>`__ hoặc các nhà xuất bản Web như `Poki <https://poki.com/>`__ hoặc `CrazyGames <https://crazygames.com/>`__. Bản export một thread hoạt động rất tốt trên macOS và iOS, nơi bản export nhiều thread trước đây luôn gặp vấn đề về khả năng tương thích.

    Vì những lý do này, đây là cách được ưu tiên và hiện là cách mặc định để xuất game lên Web.

    Để biết thêm thông tin, xem `this blog post about single-threaded Web export <https://godotengine.org/article/progress-report-web-export-in-4-3/#single-threaded-web-export>`__.

.. seealso::

    Xem `list of open issues on GitHub related to the web export <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Aplatform%3Aweb>`__ để biết danh sách các lỗi đã biết.

Tên file export
---------------

Chúng tôi khuyến nghị người dùng xuất các project Web với ``index.html`` làm tên file. ``index.html`` thường là file mặc định được web server tải khi truy cập thư mục cha, thường ẩn tên của file đó.

.. attention::

    Web export của Godot 4 yêu cầu một số file phải được đặt cùng tên với tên đã thiết lập trong lần export ban đầu. Có thể xảy ra một số vấn đề nếu các file đã export bị đổi tên, bao gồm cả file HTML chính.

Phiên bản WebGL
---------------

Godot 4 chỉ có thể nhắm đến WebGL 2.0 (sử dụng phương thức render Compatibility). Forward+/Mobile không được hỗ trợ trên nền tảng web, vì các phương thức render này được thiết kế xoay quanh các graphics API low-level hiện đại. Godot hiện chưa hỗ trợ WebGPU, vốn là điều kiện tiên quyết để Forward+/Mobile có thể chạy trên nền tảng web.

Xem `Can I use WebGL 2.0 <https://caniuse.com/webgl2>`__ để biết danh sách các phiên bản trình duyệt hỗ trợ WebGL 2.0. Lưu ý rằng Safari có một số vấn đề với hỗ trợ WebGL 2.0 mà các trình duyệt khác không gặp phải, vì vậy chúng tôi khuyến nghị sử dụng trình duyệt dựa trên Chromium hoặc Firefox nếu có thể.

Các lưu ý trên thiết bị di động
-------------------------------

Web export có thể chạy trên các nền tảng di động với một số điểm cần lưu ý. Mặc dù các bản
:ref:`Android <doc_exporting_for_android>` and :ref:`iOS <doc_exporting_for_ios>`
export native luôn có hiệu năng tốt hơn đáng kể, Web export cho phép mọi người chạy project của bạn mà không cần thông qua app store.

Hãy nhớ rằng hiệu năng CPU và GPU rất quan trọng khi chạy trên các thiết bị di động. Điều này càng rõ hơn khi chạy một project được xuất sang Web (vì đó là WebAssembly thay vì mã native). Xem phần :ref:`doc_performance` trong tài liệu để biết hướng dẫn tối ưu hóa project. Nếu project của bạn chạy trên các nền tảng khác ngoài Web, bạn có thể sử dụng :ref:`doc_feature_tags` để áp dụng các thiết lập hướng đến thiết bị cấu hình thấp khi chạy project được xuất sang Web.

Để tăng tốc thời gian tải trên các thiết bị di động, bạn cũng nên
:ref:`compile an optimized export template <doc_optimizing_for_size>`
với các tính năng không được sử dụng đã bị vô hiệu hóa. Tùy thuộc vào các tính năng mà project sử dụng, việc này có thể giảm đáng kể kích thước payload WebAssembly, giúp tải xuống và khởi tạo nhanh hơn (ngay cả khi đã được cache).

.. _doc_exporting_for_web_audio_playback:

Phát âm thanh
-------------

Kể từ Godot 4.3, việc phát âm thanh trên nền tảng web được thực hiện bằng Web Audio API. Chế độ phát **Sample** này cho phép độ trễ thấp ngay cả khi project được xuất mà không hỗ trợ thread, nhưng có một số hạn chế:

- AudioEffects không được hỗ trợ. - Các effect :ref:`Reverberation and doppler <doc_audio_streams_reverb_buses>` không được hỗ trợ. - Không hỗ trợ tạo âm thanh procedural. - Âm thanh theo vị trí có thể không luôn hoạt động chính xác, tùy thuộc vào các thuộc tính của node.

Để sử dụng hệ thống phát âm thanh riêng của Godot trên nền tảng web, bạn có thể thay đổi chế độ phát mặc định bằng thiết lập project **Audio > General > Default Playback Type.web**, hoặc thay đổi thuộc tính **Playback Type** thành **Stream** trên một
:ref:`class_AudioStreamPlayer`, :ref:`class_AudioStreamPlayer2D` or
:ref:`class_AudioStreamPlayer3D` node. This leads to increased latency
(đặc biệt khi tắt hỗ trợ thread), nhưng cho phép toàn bộ các tính năng âm thanh của Godot hoạt động.

.. _doc_javascript_export_options:

Các tùy chọn export
-------------------

Nếu có export template web có thể chạy, một nút sẽ xuất hiện giữa các nút *Stop scene* và *Play edited Scene* trong editor để nhanh chóng mở game trong trình duyệt mặc định nhằm kiểm thử.

Nếu project của bạn sử dụng GDExtension, cần bật **Extension Support**.

Nếu bạn định sử dụng :ref:`VRAM compression <doc_importing_images>` hãy đảm bảo rằng **VRAM Texture Compression** được bật cho các nền tảng mục tiêu (bật cả **For Desktop** và **For Mobile** sẽ tạo ra bản export lớn hơn nhưng tương thích tốt hơn).

Nếu cung cấp đường dẫn đến file **Custom HTML shell**, file đó sẽ được sử dụng thay cho trang HTML mặc định. Xem :ref:`doc_customizing_html5_shell`.

**Head Include** được thêm vào phần tử ``<head>`` của trang HTML được tạo. Điều này cho phép, chẳng hạn, tải webfont và JavaScript API của bên thứ ba, thêm CSS hoặc chạy mã JavaScript.

Theo mặc định, kích thước cửa sổ sẽ tự động khớp với kích thước cửa sổ trình duyệt. Nếu bạn muốn sử dụng kích thước cố định bất kể kích thước cửa sổ trình duyệt, hãy đổi **Canvas Resize Policy** thành **None**. Điều này cho phép kiểm soát kích thước cửa sổ bằng mã JavaScript tùy chỉnh trong HTML shell. Bạn cũng có thể đặt thành **Project** để hành vi gần giống hơn với một bản export native, theo
:ref:`project settings <doc_multiple_resolutions>`.

.. important:: Each project must generate their own HTML file. On export,
               một số placeholder văn bản sẽ được thay thế trong file HTML được tạo, cụ thể theo các tùy chọn export đã cho. Mọi chỉnh sửa trực tiếp đối với file HTML đó sẽ bị mất trong các lần export sau. Để tùy chỉnh file được tạo, hãy sử dụng tùy chọn **Custom HTML shell**.

.. _doc_exporting_for_web_thread_extension_support:

Hỗ trợ thread và extension
~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bật **Thread Support**, project được export sẽ có thể
:ref:`make use of multithreading <doc_using_multiple_threads>` to improve
hiệu năng. Điều này cũng cho phép phát âm thanh với độ trễ thấp khi kiểu phát được đặt thành **Stream** (thay vì **Sample** mặc định được sử dụng trong web export). Việc bật tính năng này yêu cầu sử dụng các header cross-origin isolation, được mô tả trong
:ref:`doc_exporting_for_web_serving_the_files` section below.

Nếu bật **Extensions Support**, :ref:`GDExtensions <doc_what_is_gdextension>` sẽ có thể được load. Lưu ý rằng GDExtension vẫn cần được biên dịch riêng cho nền tảng web thì mới hoạt động. Giống như hỗ trợ thread, việc bật tính năng này yêu cầu sử dụng các header cross-origin isolation.

Xuất dưới dạng Progressive Web App (PWA)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bật **Progressive Web App > Enable**, tính năng này sẽ có một số tác động:

- Cấu hình icon độ phân giải cao, chế độ hiển thị và hướng màn hình. Các tùy chọn này được cấu hình ở cuối phần Progressive Web App trong các tùy chọn export. Chúng được sử dụng khi người dùng thêm project vào màn hình chính của thiết bị, điều thường thấy trên các nền tảng di động. Tính năng này cũng được hỗ trợ trên các nền tảng desktop, mặc dù với khả năng hạn chế hơn.

- Cho phép load project mà không cần kết nối Internet nếu trước đó project đã được load ít nhất một lần. Điều này hoạt động nhờ *service worker* được cài đặt khi project được load lần đầu trong trình duyệt của người dùng. Service worker này cung cấp phương án dự phòng cục bộ khi không có kết nối Internet.

  - Lưu ý rằng trình duyệt web có thể chọn xóa dữ liệu đã cache nếu người dùng sắp hết dung lượng đĩa hoặc nếu người dùng đã không mở project trong một thời gian. Để đảm bảo dữ liệu được cache trong thời gian dài hơn, người dùng có thể bookmark trang hoặc tốt nhất là thêm trang đó vào màn hình chính của thiết bị.

  - Nếu dữ liệu offline không khả dụng vì đã bị xóa khỏi cache, bạn có thể cấu hình một **Offline Page** sẽ được hiển thị trong trường hợp này. Trang này phải ở định dạng HTML và sẽ được lưu trên máy của client vào lần đầu project được load.

- Đảm bảo các header cross-origin isolation luôn hiện diện, ngay cả khi web server chưa được cấu hình để gửi chúng. Điều này cho phép các bản export bật thread hoạt động khi được host trên bất kỳ website nào, ngay cả khi bạn không có cách kiểm soát các header mà website đó gửi.

  - Có thể tắt hành vi này bằng cách bỏ chọn **Enable Cross Origin Isolation Headers** trong phần Progressive Web App.

Các hạn chế
-----------

Vì lý do bảo mật và quyền riêng tư, nhiều tính năng hoạt động dễ dàng trên các nền tảng native lại phức tạp hơn trên nền tảng web. Sau đây là danh sách các hạn chế bạn nên biết khi port một game Godot lên web.

.. _doc_javascript_secure_contexts:

.. important:: Browser vendors are making more and more functionalities only
               có trong `secure contexts <https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts>`_, điều này có nghĩa là các tính năng đó chỉ khả dụng nếu trang web được cung cấp qua kết nối HTTPS bảo mật (localhost thường được miễn yêu cầu này).

Sử dụng cookie để lưu trữ dữ liệu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Người dùng phải **cho phép cookie** (cụ thể là IndexedDB) nếu muốn duy trì hệ thống tệp ``user://``. Khi chơi một trò chơi được trình bày trong ``iframe``, cũng phải bật cookie **bên thứ ba**. Chế độ ẩn danh/duyệt web riêng tư cũng ngăn việc duy trì dữ liệu.

Có thể sử dụng phương thức ``OS.is_userfs_persistent()`` để kiểm tra xem hệ thống tệp ``user://`` có được duy trì hay không, nhưng trong một số trường hợp có thể cho kết quả dương tính giả.

Xử lý nền
~~~~~~~~~

Trình duyệt sẽ tạm dừng project khi tab không còn là tab đang hoạt động trong trình duyệt của người dùng. Điều này có nghĩa là các hàm như ``_process()`` và ``_physics_process()`` sẽ không còn chạy cho đến khi người dùng kích hoạt lại tab (bằng cách chuyển về tab đó). Điều này có thể khiến các game có kết nối mạng bị ngắt kết nối nếu người dùng chuyển tab trong thời gian dài.

Giới hạn này không áp dụng cho các *cửa sổ* trình duyệt không được focus. Do đó, ở phía người dùng, có thể khắc phục bằng cách chạy project trong một *cửa sổ* riêng thay vì một tab riêng.

Toàn màn hình và bắt chuột
~~~~~~~~~~~~~~~~~~~~~~~~~~

Trình duyệt không cho phép **vào chế độ toàn màn hình** tùy ý. Điều tương tự cũng áp dụng cho **bắt con trỏ**. Thay vào đó, các thao tác này phải diễn ra để phản hồi một sự kiện input JavaScript. Trong Godot, điều này có nghĩa là vào chế độ toàn màn hình từ bên trong callback sự kiện input được nhấn, chẳng hạn như ``_input`` hoặc ``_unhandled_input``. Chỉ truy vấn singleton :ref:`class_Input` là chưa đủ; sự kiện input liên quan phải đang hoạt động.

Vì lý do tương tự, thiết lập project toàn màn hình sẽ không hoạt động trừ khi engine được khởi động từ bên trong một trình xử lý sự kiện input hợp lệ. Điều này yêu cầu
:ref:`customization of the HTML page <doc_customizing_html5_shell>`.

Âm thanh
~~~~~~~~

Một số trình duyệt hạn chế tính năng tự động phát âm thanh trên các website. Cách dễ nhất để khắc phục giới hạn này là yêu cầu người chơi nhấp chuột, chạm hoặc nhấn một phím/nút để bật âm thanh, chẳng hạn như khi hiển thị màn hình splash lúc bắt đầu game.

.. seealso:: Google offers additional information about their `Web Audio autoplay
             các chính sách <https://www.chromium.org/audio-video/autoplay/>`__.

             Đội ngũ Safari của Apple cũng đăng thêm thông tin về `Auto-Play Policy Changes for macOS <https://webkit.org/blog/7734/auto-play-policy-changes-for-macos/>`__.

.. warning:: Access to microphone requires a
             :ref:`secure context <doc_javascript_secure_contexts>`.

.. warning::

        Kể từ Godot 4.3, theo mặc định, các bản export Web sẽ sử dụng sample thay vì stream để phát âm thanh.

        Điều này là do cách trình duyệt ưu tiên phát âm thanh và năng lực xử lý hạn chế khi export game Web với tùy chọn export **Use Threads** bị tắt.

        Xin lưu ý rằng các hiệu ứng âm thanh hiện chưa được triển khai cho sample.


Networking
~~~~~~~~~~

.. CẬP NHẬT: Chưa được triển khai. Khi networking cấp thấp được triển khai, hãy xóa .. đoạn này.

Networking cấp thấp chưa được triển khai do trình duyệt thiếu hỗ trợ.

Hiện tại, chỉ :ref:`HTTP client <doc_http_client_class>`,
:ref:`HTTP requests <doc_http_request_class>`,
:ref:`WebSocket (client) <doc_websocket>` and :ref:`WebRTC <doc_webrtc>` are
được hỗ trợ.

Các class HTTP cũng có một số hạn chế trên nền tảng HTML5:

 -  Không thể truy cập hoặc thay đổi ``StreamPeer`` - Không có chế độ Threaded/Blocking - Không thể tiến triển nhiều hơn một lần trong mỗi frame, vì vậy polling trong một vòng lặp sẽ làm treo - Không có phản hồi chunked - Không thể tắt xác minh host - Chịu ảnh hưởng của `same-origin policy <https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy>`__

Clipboard
~~~~~~~~~

Việc đồng bộ clipboard giữa engine và hệ điều hành yêu cầu trình duyệt hỗ trợ `Clipboard API <https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API>`__; ngoài ra, do tính bất đồng bộ của API, việc truy cập từ GDScript có thể không đáng tin cậy.

.. warning:: Requires a :ref:`secure context <doc_javascript_secure_contexts>`.

Gamepad
~~~~~~~

Gamepad sẽ không được phát hiện cho đến khi một trong các nút của nó được nhấn. Gamepad có thể có mapping không đúng tùy thuộc vào tổ hợp trình duyệt/hệ điều hành/gamepad; đáng tiếc là `Gamepad API <https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API/Using_the_Gamepad_API>`__ không cung cấp cách đáng tin cậy để phát hiện thông tin gamepad cần thiết nhằm remap chúng dựa trên model/vendor/OS do các cân nhắc về quyền riêng tư.

.. warning:: Requires a :ref:`secure context <doc_javascript_secure_contexts>`.

.. _doc_exporting_for_web_serving_the_files:

Phân phối các tệp
-----------------

Việc export cho web tạo ra một số tệp cần được phân phối từ web server, bao gồm một trang HTML mặc định để trình bày. Có thể sử dụng tệp HTML tùy chỉnh, xem :ref:`doc_customizing_html5_shell`.

.. warning::

    Chỉ khi export với **Use Threads**, để đảm bảo độ trễ âm thanh thấp và khả năng sử dụng :ref:`class_Thread` trong các bản export web, các bản export web của Godot 4 sẽ sử dụng `SharedArrayBuffer <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer>`__. Điều này yêu cầu :ref:`secure context <doc_javascript_secure_contexts>`, đồng thời yêu cầu đặt các header CORS sau khi phân phối tệp:

    ::

        Cross-Origin-Opener-Policy: same-origin
        Cross-Origin-Embedder-Policy: require-corp

    Nếu bạn không kiểm soát web server hoặc không thể thêm response header, hãy chọn **Progressive Web App > Enable** trong các tùy chọn export. Tùy chọn này áp dụng một giải pháp dựa trên service worker, cho phép project chạy bằng cách mô phỏng sự hiện diện của các response header này. Trong trường hợp này vẫn yêu cầu secure context.

    Nếu client không nhận được các response header cần thiết hoặc giải pháp dựa trên service worker không được áp dụng, **project sẽ không chạy**.

Tệp ``.html`` được tạo có thể được sử dụng làm ``DirectoryIndex`` trong các server Apache và có thể được đổi tên, chẳng hạn thành ``index.html``, bất cứ lúc nào. Theo mặc định, tên của tệp này không bao giờ được phụ thuộc vào.

Trang HTML vẽ game ở kích thước tối đa trong cửa sổ trình duyệt. Nhờ vậy, trang có thể được chèn vào một ``<iframe>`` có kích thước tương ứng với game, như thường thấy trên hầu hết các website lưu trữ game web.

Các tệp được export còn lại được phân phối nguyên trạng, nằm cạnh tệp ``.html``, với tên không thay đổi. Tệp ``.wasm`` là một module WebAssembly nhị phân triển khai engine. Tệp ``.pck`` là main pack của Godot chứa game của bạn. Tệp ``.js`` chứa mã khởi động và được tệp ``.html`` sử dụng để truy cập engine. Tệp ``.png`` chứa ảnh splash khởi động.

Tệp ``.pck`` là tệp nhị phân, thường được phân phối với MIME-type
:mimetype:`application/octet-stream`. The ``.wasm`` file is delivered as
:mimetype:`application/wasm`.

.. warning::

    Việc phân phối module WebAssembly (``.wasm``) với MIME-type khác :mimetype:`application/wasm` có thể ngăn một số tối ưu hóa khởi động.

Khuyến nghị phân phối các tệp bằng compression phía server, đặc biệt là các tệp ``.pck`` và ``.wasm``, vốn thường có kích thước lớn. Module WebAssembly nén đặc biệt hiệu quả, giảm xuống còn khoảng một phần tư kích thước ban đầu khi dùng gzip compression. Nếu web server hỗ trợ, hãy cân nhắc sử dụng Brotli precompression để tiếp tục giảm kích thước tệp.

**Các host cung cấp compression on-the-fly:** GitHub Pages (gzip)

**Các host không cung cấp compression on-the-fly:** itch.io, GitLab Pages (`supports manual gzip precompression <https://docs.gitlab.com/user/project/pages/introduction/#serving-compressed-assets>`__)

.. tip::

    Repository Godot có chứa `Python script to host a local web server <https://raw.githubusercontent.com/godotengine/godot/master/platform/web/serve.py>`__. Script này предназначed để kiểm thử web editor, nhưng cũng có thể được dùng để kiểm thử các project đã export.

    Lưu script được liên kết vào một tệp có tên ``serve.py``, di chuyển tệp này vào thư mục chứa ``index.html`` của project đã export, sau đó chạy lệnh sau trong command prompt tại cùng thư mục:

    ::

        # Trên một số nền tảng, bạn có thể cần thay `python` bằng `python3`.
        python serve.py --root .

    Trên Windows, bạn có thể mở command prompt tại thư mục hiện tại bằng cách giữ
    :kbd:`Shift` and right-clicking on empty space in Windows Explorer, then
    rồi chọn **Open PowerShell window here**.

    Thao tác này sẽ phân phối nội dung của thư mục hiện tại và tự động mở web browser mặc định.

    Lưu ý rằng không nên sử dụng web server dựa trên Python này cho các trường hợp sử dụng trong production. Thay vào đó, bạn nên sử dụng một web server phổ biến như Apache hoặc nginx.

Tương tác với browser và JavaScript
-----------------------------------

Xem :ref:`dedicated page <doc_web_javascript_bridge>` để biết cách tương tác với JavaScript và truy cập một số tính năng Web browser đặc thù.

Biến môi trường
---------------

Bạn có thể sử dụng các biến môi trường sau để đặt tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè các giá trị bạn đã đặt trong menu export.

.. list-table:: HTML5 export environment variables
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Encryption / Encryption Key
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``

.. _doc_exporting_for_web_troubleshooting:

Khắc phục sự cố
---------------

Chạy bản export cục bộ lại hiển thị một project khác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn sử dụng one-click deploy trong nhiều project, bạn có thể nhận thấy một trong các project đã deploy trước đó được hiển thị thay vì project bạn đang làm việc. Điều này là do việc caching của service worker hiện chưa có cơ chế tự động cache busting.

Để khắc phục tạm thời, bạn có thể hủy đăng ký service worker hiện tại theo cách thủ công để reset cache. Thao tác này cũng cho phép đăng ký một service worker mới. Trong các browser dựa trên Chromium, mở Developer Tools bằng cách nhấn
:kbd:`F12` or :kbd:`Ctrl + Shift + I` (:kbd:`Cmd + Option + I` on macOS),
sau đó nhấp vào tab Application trong DevTools (tab này có thể bị ẩn sau biểu tượng chevron nếu ngăn devtools hẹp). Bạn có thể chọn
:button:`Update on reload` and reload the page, or click :button:`Unregister`
bên cạnh service worker hiện đang được đăng ký, sau đó reload trang.

.. figure:: img/exporting_for_web_reset_unregister_service_worker_chromium.webp
   :align: center
   :alt: Unregistering the service worker in Chromium-based browsers' DevTools

   Unregistering the service worker in Chromium-based browsers' DevTools

Quy trình trong Firefox cũng tương tự. Mở developer tools bằng cách nhấn
:kbd:`F12` or :kbd:`Ctrl + Shift + I` (:kbd:`Cmd + Option + I` on macOS),
nhấp vào tab Application trong DevTools (tab này có thể bị ẩn sau biểu tượng chevron nếu ngăn devtools hẹp). Nhấp vào :button:`Unregister` bên cạnh service worker hiện đang được đăng ký, sau đó reload trang.

.. figure:: img/exporting_for_web_reset_unregister_service_worker_firefox.webp
   :align: center
   :alt: Unregistering the service worker in Firefox's DevTools

   Unregistering the service worker in Firefox's DevTools

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export có sẵn trong
:ref:`class_EditorExportPlatformWeb` class reference.
