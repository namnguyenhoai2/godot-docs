.. _doc_exporting_for_web:

Xuất bản cho Web
================

.. seealso::

    Trang này mô tả cách xuất một dự án Godot sang HTML5. Nếu bạn muốn biên dịch editor hoặc các binary export template từ mã nguồn thay vào đó, hãy đọc :ref:`doc_compiling_for_web`.

Tính năng xuất HTML5 cho phép đưa các game được tạo bằng Godot Engine lên trình duyệt. Điều này yêu cầu trình duyệt của người dùng hỗ trợ `WebAssembly <https://webassembly.org/>`__ và `WebGL 2.0 <https://www.khronos.org/webgl/>`__.

.. attention::

    Các dự án viết bằng C# sử dụng Godot 4 hiện chưa thể xuất lên web. Xem `bài blog này <https://godotengine.org/article/platform-state-in-csharp-for-godot-4-2/#web>`__ để biết thêm thông tin.

    Để sử dụng C# trên các nền tảng web, hãy dùng Godot 3.

.. tip::

    Hãy sử dụng console dành cho nhà phát triển được tích hợp trong trình duyệt, thường mở bằng :kbd:`F12` hoặc :kbd:`Ctrl + Shift + I` (:kbd:`Cmd + Option + I` trên macOS), để xem **thông tin debug** như các lỗi JavaScript, engine và WebGL.

    Nếu phím tắt không hoạt động, đó là vì Godot thực sự đang bắt thao tác nhập. Bạn vẫn có thể mở console dành cho nhà phát triển bằng cách truy cập menu của trình duyệt.

.. note::

    Do các vấn đề bảo mật với ``SharedArrayBuffer`` do nhiều lỗ hổng khác nhau, việc sử dụng nhiều thread cho nền tảng Web có một số nhược điểm, bao gồm yêu cầu các header cụ thể ở phía server và cách ly hoàn toàn giữa các origin (nghĩa là không có quảng cáo hoặc tích hợp bên thứ ba nào trên website lưu trữ game của bạn).

    Kể từ Godot 4.3, Godot hỗ trợ xuất game trên một thread duy nhất, giúp giải quyết vấn đề này. Mặc dù bản thân cách này có một số nhược điểm (không thể sử dụng thread và không có hiệu năng tốt bằng bản xuất đa thread), nó không yêu cầu nhiều overhead để cài đặt. Cách này cũng tương thích tổng thể tốt hơn với các store như `itch.io <https://itch.io/>`__ hoặc các nhà phát hành Web như `Poki <https://poki.com/>`__ hay `CrazyGames <https://crazygames.com/>`__. Bản xuất một thread hoạt động rất tốt trên macOS và iOS, nơi bản xuất đa thread vốn luôn gặp vấn đề về khả năng tương thích.

    Vì những lý do này, đây là cách được ưu tiên và hiện là cách mặc định để xuất game lên Web.

    Để biết thêm thông tin, hãy xem `bài blog này về tính năng xuất Web một thread <https://godotengine.org/article/progress-report-web-export-in-4-3/#single-threaded-web-export>`__.

.. seealso::

    Xem `danh sách các issue đang mở trên GitHub liên quan đến tính năng xuất web <https://github.com/godotengine/godot/issues?q=is%3Aopen+is%3Aissue+label%3Aplatform%3Aweb>`__ để biết danh sách các lỗi đã biết.

Tên file export
---------------

Chúng tôi khuyên bạn nên xuất các dự án Web với ``index.html`` làm tên file. ``index.html`` thường là file mặc định được web server tải khi truy cập thư mục cha, thường khiến tên của file đó bị ẩn.

.. attention::

    Bản xuất Web của Godot 4 yêu cầu một số file được đặt cùng tên với tên đã thiết lập trong lần xuất ban đầu. Một số vấn đề có thể xảy ra nếu các file đã xuất bị đổi tên, bao gồm cả file HTML chính.

Phiên bản WebGL
---------------

Godot 4 chỉ có thể nhắm đến WebGL 2.0 (sử dụng phương thức render Compatibility). Forward+/Mobile không được hỗ trợ trên nền tảng web, vì các phương thức render này được thiết kế dựa trên các graphics API cấp thấp hiện đại. Godot hiện chưa hỗ trợ WebGPU, vốn là điều kiện tiên quyết để cho phép Forward+/Mobile chạy trên nền tảng web.

Xem `Tôi có thể sử dụng WebGL 2.0 không <https://caniuse.com/webgl2>`__ để biết danh sách các phiên bản trình duyệt hỗ trợ WebGL 2.0. Lưu ý rằng Safari có một số vấn đề với khả năng hỗ trợ WebGL 2.0 mà các trình duyệt khác không gặp phải, vì vậy nếu có thể, chúng tôi khuyên bạn nên sử dụng trình duyệt dựa trên Chromium hoặc Firefox.

Các lưu ý trên thiết bị di động
-------------------------------

Bản xuất Web có thể chạy trên các nền tảng di động với một số điểm cần lưu ý. Mặc dù bản native
:ref:`Android <doc_exporting_for_android>` và :ref:`iOS <doc_exporting_for_ios>` luôn có hiệu năng tốt hơn đáng kể, bản xuất Web cho phép mọi người chạy dự án của bạn mà không cần thông qua các app store.

Hãy nhớ rằng hiệu năng CPU và GPU rất quan trọng khi chạy trên thiết bị di động. Điều này càng rõ rệt hơn khi chạy một dự án được xuất sang Web (vì đó là WebAssembly thay vì mã native). Xem :ref:`doc_performance` phần tài liệu để biết các hướng dẫn tối ưu hóa dự án. Nếu dự án của bạn chạy trên các nền tảng khác ngoài Web, bạn có thể sử dụng :ref:`doc_feature_tags` để áp dụng các thiết lập hướng đến thiết bị cấu hình thấp khi chạy dự án đã xuất sang Web.

Để tăng tốc thời gian tải trên thiết bị di động, bạn cũng nên
:ref:`biên dịch một export template đã tối ưu <doc_optimizing_for_size>` với các tính năng không sử dụng được tắt. Tùy thuộc vào các tính năng mà dự án sử dụng, cách này có thể giảm đáng kể kích thước payload WebAssembly, giúp tải xuống và khởi tạo nhanh hơn (ngay cả khi đã được cache).

.. _doc_exporting_for_web_audio_playback:

Phát âm thanh
-------------

Kể từ Godot 4.3, việc phát âm thanh trên nền tảng web được thực hiện bằng Web Audio API. Chế độ phát **Sample** này cho phép đạt độ trễ thấp ngay cả khi dự án được xuất mà không hỗ trợ thread, nhưng có một số hạn chế:

- AudioEffects không được hỗ trợ.
- Các hiệu ứng :ref:`Reverberation and doppler <doc_audio_streams_reverb_buses>` không được hỗ trợ.
- Tính năng tạo âm thanh procedural không được hỗ trợ.
- Âm thanh định vị có thể không phải lúc nào cũng hoạt động chính xác, tùy thuộc vào các thuộc tính của node.

Để sử dụng hệ thống phát âm thanh riêng của Godot trên nền tảng web, bạn có thể thay đổi chế độ phát mặc định bằng thiết lập project **Audio > General > Default Playback Type.web**, hoặc thay đổi thuộc tính **Playback Type** thành **Stream** trên một
:ref:`class_AudioStreamPlayer`, :ref:`class_AudioStreamPlayer2D` hoặc
:ref:`class_AudioStreamPlayer3D` node. Điều này làm tăng độ trễ (đặc biệt khi tắt hỗ trợ thread), nhưng cho phép toàn bộ các tính năng âm thanh của Godot hoạt động.

.. _doc_javascript_export_options:

Tùy chọn export
---------------

Nếu có export template web có thể chạy, một nút sẽ xuất hiện giữa các nút *Stop scene* và *Play edited Scene* trong editor để nhanh chóng mở game bằng trình duyệt mặc định nhằm kiểm thử.

Nếu dự án của bạn sử dụng GDExtension, cần bật **Extension Support**.

Nếu bạn dự định sử dụng :ref:`VRAM compression <doc_importing_images>`, hãy đảm bảo **VRAM Texture Compression** được bật cho các nền tảng mục tiêu (bật cả **For Desktop** và **For Mobile** sẽ tạo ra bản export lớn hơn nhưng tương thích hơn).

Nếu cung cấp đường dẫn đến file **Custom HTML shell**, file đó sẽ được sử dụng thay cho trang HTML mặc định. Xem :ref:`doc_customizing_html5_shell`.

**Head Include** được thêm vào phần tử ``<head>`` của trang HTML được tạo. Điều này cho phép, chẳng hạn, tải webfont và JavaScript API của bên thứ ba, thêm CSS hoặc chạy mã JavaScript.

Theo mặc định, kích thước cửa sổ sẽ tự động khớp với kích thước cửa sổ trình duyệt. Nếu muốn sử dụng kích thước cố định bất kể kích thước cửa sổ trình duyệt, hãy đổi **Canvas Resize Policy** thành **None**. Điều này cho phép kiểm soát kích thước cửa sổ bằng mã JavaScript tùy chỉnh trong HTML shell. Bạn cũng có thể đặt thành **Project** để hoạt động gần giống hơn với bản export native, theo
:ref:`cài đặt dự án <doc_multiple_resolutions>`.

.. important:: Mỗi dự án phải tạo tệp HTML riêng. Khi export, một số placeholder văn bản sẽ được thay thế trong tệp HTML được tạo, cụ thể theo các tùy chọn export đã cho. Mọi chỉnh sửa trực tiếp đối với tệp HTML đó sẽ bị mất trong các lần export sau. Để tùy chỉnh tệp được tạo, hãy sử dụng tùy chọn **Custom HTML shell**.

.. _doc_exporting_for_web_thread_extension_support:

Hỗ trợ thread và extension
~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bật **Thread Support**, dự án được export sẽ có thể
:ref:`sử dụng đa luồng <doc_using_multiple_threads>` để cải thiện hiệu suất. Điều này cũng cho phép phát âm thanh có độ trễ thấp khi kiểu phát được đặt thành **Stream** (thay vì **Sample** mặc định được sử dụng trong các bản export web). Việc bật tính năng này yêu cầu sử dụng các header cross-origin isolation, được mô tả trong
:ref:`doc_exporting_for_web_serving_the_files` phần bên dưới.

Nếu bật **Extensions Support**, các :ref:`GDExtensions <doc_what_is_gdextension>` sẽ có thể được tải. Lưu ý rằng GDExtensions vẫn cần được biên dịch riêng cho nền tảng web thì mới hoạt động. Giống như hỗ trợ thread, việc bật tính năng này yêu cầu sử dụng các header cross-origin isolation.

Export dưới dạng Progressive Web App (PWA)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bật **Progressive Web App > Enable**, tùy chọn này sẽ có một số tác động:

- Cấu hình các biểu tượng độ phân giải cao, chế độ hiển thị và hướng màn hình. Các tùy chọn này được cấu hình ở cuối phần Progressive Web App trong các tùy chọn export. Chúng được sử dụng khi người dùng thêm dự án vào màn hình chính của thiết bị, điều thường thấy trên các nền tảng di động. Tính năng này cũng được hỗ trợ trên các nền tảng máy tính để bàn, dù với khả năng hạn chế hơn.

- Cho phép tải dự án mà không cần kết nối Internet nếu dự án đã được tải ít nhất một lần trước đó. Điều này hoạt động nhờ *service worker* được cài đặt khi dự án được tải lần đầu trong trình duyệt của người dùng. Service worker này cung cấp phương án dự phòng cục bộ khi không có kết nối Internet.

  - Lưu ý rằng trình duyệt web có thể chọn xóa dữ liệu đã lưu trong bộ nhớ đệm nếu người dùng sắp hết dung lượng ổ đĩa hoặc nếu người dùng không mở dự án trong một thời gian. Để đảm bảo dữ liệu được lưu trong bộ nhớ đệm lâu hơn, người dùng có thể đánh dấu trang hoặc tốt nhất là thêm trang vào màn hình chính của thiết bị.

  - Nếu dữ liệu ngoại tuyến không khả dụng vì đã bị xóa khỏi bộ nhớ đệm, bạn có thể cấu hình **Offline Page** để hiển thị trong trường hợp này. Trang này phải ở định dạng HTML và sẽ được lưu trên máy của client vào lần đầu tiên dự án được tải.

- Đảm bảo các header cross-origin isolation luôn hiện diện, ngay cả khi máy chủ web chưa được cấu hình để gửi chúng. Điều này cho phép các bản export bật thread hoạt động khi được lưu trữ trên bất kỳ website nào, ngay cả khi bạn không có cách kiểm soát các header mà website đó gửi.

  - Có thể tắt hành vi này bằng cách bỏ chọn **Enable Cross Origin Isolation Headers** trong phần Progressive Web App.

Hạn chế
-------

Vì lý do bảo mật và quyền riêng tư, nhiều tính năng hoạt động dễ dàng trên các nền tảng native lại phức tạp hơn trên nền tảng web. Sau đây là danh sách các hạn chế bạn cần biết khi chuyển một game Godot sang web.

.. _doc_javascript_secure_contexts:

.. important:: Các nhà cung cấp trình duyệt đang ngày càng chỉ cung cấp nhiều chức năng hơn trong `secure contexts <https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts>`_, nghĩa là những tính năng đó chỉ khả dụng nếu trang web được phân phối qua kết nối HTTPS an toàn (localhost thường được miễn yêu cầu này).

Sử dụng cookie để lưu trữ dữ liệu
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Người dùng phải **cho phép cookie** (cụ thể là IndexedDB) nếu muốn duy trì ``user://`` file system. Khi chơi một game được cung cấp trong ``iframe``, cookie **bên thứ ba** cũng phải được bật. Chế độ ẩn danh/duyệt web riêng tư cũng ngăn việc duy trì dữ liệu.

Có thể sử dụng phương thức ``OS.is_userfs_persistent()`` để kiểm tra xem ``user://`` file system có được duy trì hay không, nhưng trong một số trường hợp có thể cho kết quả dương tính giả.

Xử lý nền
~~~~~~~~~

Trình duyệt sẽ tạm dừng dự án khi tab không còn là tab đang hoạt động trong trình duyệt của người dùng. Điều này có nghĩa là các hàm như ``_process()`` và ``_physics_process()`` sẽ không còn chạy cho đến khi người dùng kích hoạt lại tab (bằng cách chuyển về tab đó). Điều này có thể khiến các game mạng bị ngắt kết nối nếu người dùng chuyển tab trong thời gian dài.

Hạn chế này không áp dụng cho các *cửa sổ* trình duyệt không được focus. Do đó, ở phía người dùng, có thể khắc phục bằng cách chạy dự án trong một *cửa sổ* riêng thay vì một tab riêng.

Toàn màn hình và bắt chuột
~~~~~~~~~~~~~~~~~~~~~~~~~~

Trình duyệt không cho phép **vào chế độ toàn màn hình** tùy ý. Điều tương tự cũng áp dụng cho **bắt con trỏ**. Thay vào đó, các thao tác này phải xảy ra để phản hồi một sự kiện input JavaScript. Trong Godot, điều này có nghĩa là vào chế độ toàn màn hình từ bên trong callback của một sự kiện input được nhấn, chẳng hạn như ``_input`` hoặc ``_unhandled_input``. Việc truy vấn singleton :ref:`class_Input` là chưa đủ; sự kiện input liên quan hiện phải đang hoạt động.

Vì cùng lý do đó, cài đặt dự án về chế độ toàn màn hình sẽ không hoạt động trừ khi engine được khởi động từ bên trong một trình xử lý sự kiện input hợp lệ. Điều này yêu cầu
:ref:`tùy chỉnh trang HTML <doc_customizing_html5_shell>`.

Âm thanh
~~~~~~~~

Một số trình duyệt hạn chế việc tự động phát âm thanh trên website. Cách dễ nhất để khắc phục hạn chế này là yêu cầu người chơi nhấp chuột, chạm hoặc nhấn một phím/nút để bật âm thanh, chẳng hạn khi hiển thị màn hình splash lúc bắt đầu game.

.. seealso:: Google cung cấp thêm thông tin về `các chính sách tự động phát Web Audio <https://www.chromium.org/audio-video/autoplay/>`__.

             Nhóm Safari của Apple cũng đã đăng thêm thông tin về `các thay đổi trong Chính sách tự động phát cho macOS <https://webkit.org/blog/7734/auto-play-policy-changes-for-macos/>`__.

.. warning:: Việc truy cập microphone yêu cầu một
             :ref:`secure context <doc_javascript_secure_contexts>`.

.. warning::

        Kể từ Godot 4.3, theo mặc định, các bản export Web sẽ sử dụng sample thay vì stream để phát âm thanh.

        Điều này là do cách trình duyệt ưu tiên phát âm thanh và năng lực xử lý hạn chế khi export game Web với tùy chọn export **Use Threads** bị tắt.

        Lưu ý rằng các hiệu ứng âm thanh vẫn chưa được triển khai cho sample.


Mạng
~~~~

.. UPDATE: Not implemented. When low-level networking is implemented, remove
.. this paragraph.

Mạng cấp thấp chưa được triển khai do trình duyệt không hỗ trợ.

Hiện tại, chỉ :ref:`HTTP client <doc_http_client_class>`,
:ref:`HTTP requests <doc_http_request_class>`,
:ref:`WebSocket (client) <doc_websocket>` và :ref:`WebRTC <doc_webrtc>` được hỗ trợ.

Các lớp HTTP cũng có một số hạn chế trên nền tảng HTML5:

 -  Không thể truy cập hoặc thay đổi ``StreamPeer``
 -  Chế độ Threaded/Blocking không khả dụng
 -  Không thể tiến triển nhiều hơn một lần mỗi frame, vì vậy việc polling trong vòng lặp sẽ làm đóng băng chương trình
 -  Không có response dạng chunked
 -  Không thể tắt tính năng xác minh host
 -  Tuân theo `same-origin policy <https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy>`__

Clipboard
~~~~~~~~~

Việc đồng bộ clipboard giữa engine và hệ điều hành yêu cầu trình duyệt hỗ trợ `Clipboard API <https://developer.mozilla.org/en-US/docs/Web/API/Clipboard_API>`__; ngoài ra, do API này có tính bất đồng bộ nên việc truy cập từ GDScript có thể không đáng tin cậy.

.. warning:: Yêu cầu :ref:`secure context <doc_javascript_secure_contexts>`.

Gamepad
~~~~~~~

Gamepad sẽ không được phát hiện cho đến khi một trong các nút của nó được nhấn. Gamepad có thể có mapping không chính xác tùy thuộc vào tổ hợp trình duyệt/OS/gamepad; đáng tiếc là `Gamepad API <https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API/Using_the_Gamepad_API>`__ không cung cấp cách đáng tin cậy để phát hiện thông tin gamepad cần thiết nhằm remap chúng dựa trên model/vendor/OS do các cân nhắc về quyền riêng tư.

.. warning:: Yêu cầu :ref:`secure context <doc_javascript_secure_contexts>`.

.. _doc_exporting_for_web_serving_the_files:

Cung cấp các tệp
----------------

Việc export cho web sẽ tạo ra một số tệp để được cung cấp từ web server, bao gồm một trang HTML mặc định để trình bày. Có thể sử dụng tệp HTML tùy chỉnh, xem :ref:`doc_customizing_html5_shell`.

.. warning::

    Chỉ khi export với **Use Threads**, để đảm bảo độ trễ âm thanh thấp và khả năng sử dụng :ref:`class_Thread` trong các bản export web, các bản export web của Godot 4 sử dụng `SharedArrayBuffer <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer>`__. Điều này yêu cầu :ref:`secure context <doc_javascript_secure_contexts>`, đồng thời yêu cầu thiết lập các header CORS sau khi cung cấp các tệp:

    ::

        Cross-Origin-Opener-Policy: same-origin
        Cross-Origin-Embedder-Policy: require-corp

    Nếu bạn không kiểm soát web server hoặc không thể thêm response header, hãy kiểm tra **Progressive Web App > Enable** trong các tùy chọn export. Tùy chọn này áp dụng một giải pháp dựa trên service worker, cho phép project chạy bằng cách mô phỏng sự hiện diện của các response header này. Trong trường hợp này vẫn yêu cầu secure context.

    Nếu client không nhận được các response header bắt buộc hoặc giải pháp dựa trên service worker chưa được áp dụng, **project sẽ không chạy**.

Tệp ``.html`` được tạo ra có thể được sử dụng làm ``DirectoryIndex`` trên các Apache server và có thể được đổi tên thành ví dụ như ``index.html`` bất kỳ lúc nào. Theo mặc định, tên của tệp này không bao giờ được dùng làm tham chiếu.

Trang HTML hiển thị game ở kích thước tối đa trong cửa sổ trình duyệt. Nhờ đó, game có thể được chèn vào một ``<iframe>`` với kích thước của game, như thường thấy trên hầu hết các trang hosting web game.

Các tệp export khác được cung cấp nguyên trạng, nằm cạnh tệp ``.html``, với tên không thay đổi. Tệp ``.wasm`` là một module WebAssembly nhị phân triển khai engine. Tệp ``.pck`` là main pack của Godot chứa game của bạn. Tệp ``.js`` chứa mã khởi động và được tệp ``.html`` sử dụng để truy cập engine. Tệp ``.png`` chứa ảnh splash khi khởi động.

Tệp ``.pck`` là tệp nhị phân, thường được cung cấp với MIME-type
:mimetype:`application/octet-stream`. Tệp ``.wasm`` được cung cấp dưới dạng
:mimetype:`application/wasm`.

.. warning::

    Việc cung cấp module WebAssembly (``.wasm``) với MIME-type khác :mimetype:`application/wasm` có thể ngăn một số tối ưu hóa khởi động.

Khuyến nghị sử dụng tính năng nén phía server khi cung cấp các tệp, đặc biệt là các tệp ``.pck`` và ``.wasm``, vốn thường có kích thước lớn. Module WebAssembly nén đặc biệt hiệu quả, giảm xuống khoảng một phần tư kích thước ban đầu khi nén bằng gzip. Hãy cân nhắc sử dụng tính năng nén trước bằng Brotli nếu web server của bạn hỗ trợ, để tiếp tục giảm kích thước tệp.

**Các host cung cấp tính năng nén on-the-fly:** GitHub Pages (gzip)

**Các host không cung cấp tính năng nén on-the-fly:** itch.io, GitLab Pages (`hỗ trợ nén trước thủ công bằng gzip <https://docs.gitlab.com/user/project/pages/introduction/#serving-compressed-assets>`__)

.. tip::

    Repository Godot có một `Python script để host web server cục bộ <https://raw.githubusercontent.com/godotengine/godot/master/platform/web/serve.py>`__. Script này предназначен cho việc kiểm thử web editor, nhưng cũng có thể được dùng để kiểm thử các project đã export.

    Lưu script được liên kết vào một tệp có tên ``serve.py``, di chuyển tệp này vào thư mục chứa ``index.html`` của project đã export, sau đó chạy lệnh sau trong command prompt tại cùng thư mục:

    ::

        # You may need to replace `python` with `python3` on some platforms.
        python serve.py --root .

    Trên Windows, bạn có thể mở command prompt tại thư mục hiện tại bằng cách giữ
    :kbd:`Shift` rồi nhấp chuột phải vào khoảng trống trong Windows Explorer, sau đó chọn **Open PowerShell window here**.

    Thao tác này sẽ cung cấp nội dung của thư mục hiện tại và tự động mở trình duyệt web mặc định.

    Lưu ý rằng không nên sử dụng web server dựa trên Python này cho các trường hợp sử dụng trong môi trường production. Thay vào đó, bạn nên sử dụng một web server phổ biến như Apache hoặc nginx.

Tương tác với trình duyệt và JavaScript
---------------------------------------

Xem :ref:`trang chuyên dụng <doc_web_javascript_bridge>` để biết cách tương tác với JavaScript và truy cập một số tính năng độc đáo của trình duyệt web.

Các biến môi trường
-------------------

Bạn có thể sử dụng các biến môi trường sau để thiết lập tùy chọn export bên ngoài editor. Trong quá trình export, các biến này sẽ ghi đè các giá trị bạn đã đặt trong menu export.

.. list-table:: Các biến môi trường export HTML5
   :header-rows: 1

   * - Tùy chọn export
     - Biến môi trường
   * - Mã hóa / Khóa mã hóa
     - ``GODOT_SCRIPT_ENCRYPTION_KEY``

.. _doc_exporting_for_web_troubleshooting:

Khắc phục sự cố
---------------

Chạy bản export cục bộ lại hiển thị một project khác
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Nếu bạn sử dụng one-click deploy trong nhiều project, bạn có thể nhận thấy một trong các project đã deploy trước đó được hiển thị thay vì project bạn đang làm việc. Nguyên nhân là do bộ nhớ đệm của service worker hiện chưa có cơ chế tự động bust cache.

Để khắc phục tạm thời, bạn có thể hủy đăng ký service worker hiện tại theo cách thủ công để đặt lại cache. Việc này cũng cho phép đăng ký một service worker mới. Trong các trình duyệt dựa trên Chromium, hãy mở Developer Tools bằng cách nhấn
:kbd:`F12` hoặc :kbd:`Ctrl + Shift + I` (:kbd:`Cmd + Option + I` trên macOS), sau đó nhấp vào tab Application trong DevTools (tab này có thể bị ẩn sau biểu tượng dấu ngoặc nhọn nếu khung devtools hẹp). Bạn có thể chọn
:button:`Update on reload` rồi tải lại trang hoặc nhấp vào :button:`Unregister` bên cạnh service worker hiện đang được đăng ký, sau đó tải lại trang.

.. figure:: img/exporting_for_web_reset_unregister_service_worker_chromium.webp
   :align: center
   :alt: Hủy đăng ký service worker trong DevTools của các trình duyệt dựa trên Chromium

   Hủy đăng ký service worker trong DevTools của các trình duyệt dựa trên Chromium

Quy trình này tương tự trong Firefox. Mở công cụ dành cho nhà phát triển bằng cách nhấn
:kbd:`F12` hoặc :kbd:`Ctrl + Shift + I` (:kbd:`Cmd + Option + I` trên macOS), nhấp vào tab Application trong DevTools (tab này có thể bị ẩn sau biểu tượng dấu ngoặc nhọn nếu khung devtools hẹp). Nhấp vào :button:`Unregister` bên cạnh service worker hiện đang được đăng ký, sau đó tải lại trang.

.. figure:: img/exporting_for_web_reset_unregister_service_worker_firefox.webp
   :align: center
   :alt: Hủy đăng ký service worker trong DevTools của Firefox

   Hủy đăng ký service worker trong DevTools của Firefox

Tùy chọn export
---------------

Bạn có thể tìm thấy danh sách đầy đủ các tùy chọn export hiện có trong tài liệu tham chiếu lớp
:ref:`class_EditorExportPlatformWeb`.

.. _`secure contexts`: https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts
