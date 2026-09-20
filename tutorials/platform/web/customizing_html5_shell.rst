.. _doc_customizing_html5_shell:

Trang HTML tùy chỉnh cho Web export
===================================

Mặc dù các template Web export cung cấp một trang HTML mặc định có đầy đủ khả năng khởi chạy project mà không cần tùy chỉnh thêm, việc tạo một trang HTML tùy chỉnh có thể hữu ích. Mặc dù hiện tại bản thân game chưa thể dễ dàng được điều khiển trực tiếp từ bên ngoài, trang này cho phép tùy chỉnh quá trình khởi tạo engine.

Một số trường hợp việc tùy chỉnh trang mặc định có thể hữu ích gồm:

- Tải các file từ một thư mục khác với thư mục chứa trang; - Tải file ``.zip`` thay vì file ``.pck`` làm pack chính; - Tải engine từ một thư mục khác với thư mục chứa file pack chính; - Thêm nút click-to-play để có thể khởi chạy game ở chế độ fullscreen; - Tải một số file bổ sung trước khi engine khởi động, giúp chúng có sẵn trong file system của project sớm nhất có thể; - Truyền các đối số dòng lệnh tùy chỉnh, chẳng hạn như ``-s``, để khởi chạy script ``MainLoop``.

Trang HTML mặc định có sẵn trong repository của Godot Engine tại `/misc/dist/html/full-size.html <https://github.com/godotengine/godot/blob/master/misc/dist/html/full-size.html>`__ nhưng bạn có thể sử dụng template sau đây như một ví dụ đơn giản hơn nhiều:

.. code-block:: html

    <!DOCTYPE html>
    <html>
        <head>
            <title>My Template</title>
            <meta charset="UTF-8">
        </head>
        <body>
            <canvas id="canvas"></canvas>
            <script src="$GODOT_URL"></script>
            <script>
                var engine = new Engine($GODOT_CONFIG);
                engine.startGame();
            </script>
        </body>
    </html>

Thiết lập
---------
Như ví dụ trên cho thấy, đây phần lớn là một tài liệu HTML thông thường, với một vài placeholder cần được thay thế trong quá trình export, một phần tử html ``<canvas>``, và một số mã JavaScript đơn giản gọi class :js:class:`Engine`.

Các placeholder bắt buộc duy nhất là:

- ``$GODOT_URL``: Tên của file JavaScript chính, cung cấp class :js:class:`Engine` cần thiết để khởi động engine và phải được đưa vào HTML dưới dạng ``<script>``. Tên này được tạo từ *Export Path* trong quá trình export.

- ``$GODOT_CONFIG``: Một object JavaScript chứa các tùy chọn export và có thể được ghi đè về sau. Xem :js:attr:`EngineConfig` để biết danh sách đầy đủ các tùy chọn ghi đè.

Các placeholder tùy chọn sau đây sẽ bật một số tính năng bổ sung trong template HTML tùy chỉnh của bạn.

- ``$GODOT_PROJECT_NAME``: Tên project được định nghĩa trong
  :ref:`Name <class_ProjectSettings_property_application/config/name>` setting
  trong **Project Settings > Application > Config**. Bạn nên sử dụng nó làm ``<title>`` trong template của mình.

- ``$GODOT_HEAD_INCLUDE``: Một chuỗi tùy chỉnh được đưa vào tài liệu HTML ngay trước phần cuối của thẻ ``<head>``. Chuỗi này được tùy chỉnh trong các tùy chọn export, tại phần *Html / Head Include*. Mặc dù bạn toàn quyền kiểm soát trang HTML mình tạo, biến này có thể hữu ích khi cấu hình các phần của phần tử HTML ``head`` từ Godot Editor, chẳng hạn như cho các Web export preset khác nhau.

- ``$GODOT_SPLASH``: Đường dẫn đến hình ảnh được sử dụng làm boot splash, được định nghĩa trong
  :ref:`Image <class_ProjectSettings_property_application/boot_splash/image>` setting
  trong **Project Settings > Application > Boot Splash**.

- ``$GODOT_SPLASH_COLOR`` Màu nền của splash screen, được định nghĩa trong
  :ref:`BG Color <class_ProjectSettings_property_application/boot_splash/bg_color>` setting
  trong **Project Settings > Application > Boot Splash**, được chuyển đổi thành mã màu hex.

- ``$GODOT_SPLASH_CLASSES``: Placeholder này cung cấp một chuỗi gồm tên các setting và giá trị của chúng, ảnh hưởng đến splash screen. Chuỗi này được dùng làm một tập hợp tên class CSS, cho phép tạo style cho hình ảnh splash dựa trên các setting của project. Các setting sau đây từ **Project Settings > Application > Boot Splash** được cung cấp, được biểu diễn bằng các tên class bên dưới tùy theo giá trị boolean của setting:

  - :ref:`Show Image <class_ProjectSettings_property_application/boot_splash/show_image>`: ``show-image--true``, ``show-image--false`` - :ref:`Stretch Mode <class_ProjectSettings_property_application/boot_splash/stretch_mode>`: ``fullsize--true`` (nếu **not** Disabled), ``fullsize--false`` - :ref:`Use Filter <class_ProjectSettings_property_application/boot_splash/use_filter>`: ``use-filter--true``, ``use-filter--false``

Khi trang tùy chỉnh đã sẵn sàng, bạn có thể chọn trang này trong các tùy chọn export, tại phần *Html / Custom Html Shell*.

.. image:: img/html5_export_options.png

Khởi chạy project
-----------------
Để có thể khởi chạy game, bạn cần viết một script khởi tạo engine — phần code điều khiển. Quy trình này gồm ba bước, nhưng như minh họa ở đây, phần lớn các bước có thể được bỏ qua tùy theo mức độ tùy chỉnh cần thiết.

Xem :ref:`HTML5 shell class reference <doc_html5_shell_classref>` để biết danh sách đầy đủ các method và tùy chọn hiện có.

Trước tiên, engine phải được tải, sau đó cần được khởi tạo, và cuối cùng project mới có thể được khởi chạy. Bạn có thể thực hiện thủ công từng bước với mức độ kiểm soát cao. Tuy nhiên, trong trường hợp đơn giản nhất, bạn chỉ cần tạo một instance của class :js:class:`Engine` với cấu hình đã export, sau đó gọi method :js:meth:`engine.startGame <Engine.prototype.startGame>`, tùy chọn ghi đè bất kỳ tham số :js:attr:`EngineConfig` nào.

.. code-block:: js

    const engine = new Engine($GODOT_CONFIG);
    engine.startGame({
        // Cấu hình ghi đè tùy chọn, ví dụ:
        // unloadAfterInit: false,
        // canvasResizePolicy: 0,
        // ...
    });

Đoạn code này tự động tải và khởi tạo engine trước khi khởi chạy game. Đoạn code sử dụng cấu hình đã cho để tải engine. Method :js:meth:`engine.startGame <Engine.prototype.startGame>` là asynchronous và trả về một ``Promise``. Nhờ đó, code điều khiển của bạn có thể theo dõi xem game đã được tải đúng cách hay chưa mà không chặn việc thực thi hoặc phụ thuộc vào polling.

Nếu project của bạn cần kiểm soát đặc biệt đối với các đối số khởi chạy và file dependency, bạn có thể sử dụng method :js:meth:`engine.start <Engine.prototype.start>` thay thế. Lưu ý rằng method này không tự động preload file ``pck``, vì vậy có lẽ bạn sẽ muốn tự preload file đó (cùng với bất kỳ file bổ sung nào khác) thông qua method :js:meth:`engine.preloadFile <Engine.prototype.preloadFile>`.

Ngoài ra, bạn cũng có thể tự :js:meth:`engine.init <Engine.prototype.init>` để thực hiện các hành động cụ thể sau khi module được khởi tạo nhưng trước khi engine khởi chạy.

Quy trình này phức tạp hơn một chút, nhưng cho phép bạn toàn quyền kiểm soát quá trình khởi động engine.

.. code-block:: js

    const myWasm = 'mygame.wasm';
    const myPck = 'mygame.pck';
    const engine = new Engine();
    Promise.all([
        // Tải và khởi tạo engine
        engine.init(myWasm),
        // Và pck đồng thời
        engine.preloadFile(myPck),
    ]).then(() => {
        // Bây giờ khởi chạy engine.
        return engine.start({ args: ['--main-pack', myPck] });
    }).then(() => {
        console.log('Engine has started!');
    });

Để tải engine thủ công, phải gọi static method :js:meth:`Engine.load`. Vì method này là static, nhiều instance engine có thể được tạo nếu chúng dùng chung ``wasm``.

.. note:: Multiple instances cannot be spawned by default, as the engine is immediately unloaded after it is initialized.
          Để ngăn điều này xảy ra, hãy xem tùy chọn ghi đè :js:attr:`unloadAfterInit`. Sau đó, bạn vẫn có thể unload engine thủ công bằng cách gọi static method :js:meth:`Engine.unload`. Việc unload engine giải phóng bộ nhớ của trình duyệt bằng cách unload các file không còn cần thiết sau khi instance được khởi tạo.

Tùy chỉnh hành vi
-----------------
Trong môi trường Web, có thể sử dụng một số method để đảm bảo game hoạt động như dự kiến.

Nếu bạn nhắm đến một phiên bản WebGL cụ thể hoặc chỉ muốn kiểm tra xem WebGL có khả dụng hay không, bạn có thể gọi method :js:meth:`Engine.isWebGLAvailable`. Method này nhận một đối số tùy chọn, cho phép kiểm tra một major version cụ thể của WebGL.

Vì file executable thực tế không tồn tại trong môi trường Web, engine chỉ lưu một filename ảo được tạo từ base name của các file engine đã tải. Giá trị này ảnh hưởng đến output của
:ref:`OS.get_executable_path() <class_OS_method_get_executable_path>` method and defines the name of
pack chính được tự động khởi chạy. Tùy chọn ghi đè :js:attr:`executable` có thể được sử dụng để ghi đè giá trị này.

Tùy chỉnh phần hiển thị
-----------------------
Có thể sử dụng một số tùy chọn cấu hình để tùy chỉnh thêm giao diện và hành vi của game trên trang của bạn.

Theo mặc định, phần tử canvas đầu tiên trên trang được sử dụng để render. Để sử dụng một phần tử canvas khác, bạn có thể dùng tùy chọn ghi đè :js:attr:`canvas`. Tùy chọn này yêu cầu một tham chiếu đến chính phần tử DOM đó.

.. code-block:: js

    const canvasElement = document.querySelector("#my-canvas-element");
    engine.startGame({ canvas: canvasElement });

Cách engine resize canvas có thể được cấu hình thông qua tùy chọn ghi đè :js:attr:`canvasResizePolicy`.

Nếu game của bạn mất một khoảng thời gian để tải, việc hiển thị một loading UI tùy chỉnh để theo dõi tiến trình có thể hữu ích. Bạn có thể thực hiện điều này bằng tùy chọn callback :js:attr:`onProgress`, cho phép thiết lập một callback function được gọi thường xuyên khi engine tải các byte mới.

.. code-block:: js

    function printProgress(current, total) {
        console.log("Loaded " + current + " of " + total + " bytes");
    }
    engine.startGame({ onProgress: printProgress });

Hãy lưu ý rằng trong một số trường hợp, ``total`` có thể là ``0``. Điều này có nghĩa là không thể tính toán giá trị đó.

Nếu game của bạn hỗ trợ nhiều ngôn ngữ, tùy chọn ghi đè :js:attr:`locale` có thể được sử dụng để buộc chọn một locale cụ thể, miễn là bạn có một chuỗi mã ngôn ngữ hợp lệ. Bạn có thể sử dụng logic phía server để xác định ngôn ngữ nào người dùng có thể ưu tiên. Theo cách này, mã ngôn ngữ có thể được lấy từ HTTP header ``Accept-Language`` hoặc được xác định bởi một dịch vụ GeoIP.

Debugging
---------
Để debug các project đã export, việc đọc các stream output và error tiêu chuẩn do engine tạo ra có thể hữu ích. Điều này tương tự output hiển thị trong cửa sổ console của editor. Theo mặc định, standard ``console.log`` và ``console.warn`` lần lượt được sử dụng cho các stream output và error. Bạn có thể tùy chỉnh hành vi này bằng cách thiết lập các function riêng để xử lý message.

Sử dụng tùy chọn ghi đè :js:attr:`onPrint` để thiết lập callback function cho stream output, và tùy chọn ghi đè :js:attr:`onPrintError` để thiết lập callback function cho stream error.

.. code-block:: js

    function print(text) {
        console.log(text);
    }
    function printError(text) {
        console.warn(text);
    }
    engine.startGame({ onPrint: print, onPrintError: printError });

Hãy nhớ rằng khi xử lý output của engine, việc in output đó ra trong sản phẩm hoàn thiện có thể không phải là điều mong muốn.
