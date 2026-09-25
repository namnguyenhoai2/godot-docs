.. _doc_customizing_html5_shell:

Trang HTML tùy chỉnh cho việc export Web
========================================

Mặc dù các template export Web cung cấp một trang HTML mặc định hoàn toàn có thể khởi chạy project mà không cần tùy chỉnh thêm, việc tạo một trang HTML tùy chỉnh vẫn có thể hữu ích. Mặc dù hiện tại chưa dễ dàng điều khiển trực tiếp game từ bên ngoài, một trang như vậy cho phép tùy chỉnh quá trình khởi tạo engine.

Một số trường hợp sử dụng mà việc tùy chỉnh trang mặc định sẽ hữu ích bao gồm:

- Tải các file từ một thư mục khác với thư mục chứa trang;
- Tải file ``.zip`` thay vì file ``.pck`` làm pack chính;
- Tải engine từ một thư mục khác với thư mục chứa file pack chính;
- Thêm nút click-to-play để có thể khởi động game ở chế độ fullscreen;
- Tải một số file bổ sung trước khi engine khởi động, giúp chúng có sẵn trong file system của project sớm nhất có thể;
- Truyền các đối số dòng lệnh tùy chỉnh, chẳng hạn như ``-s`` để khởi động một script ``MainLoop``.

Trang HTML mặc định có sẵn trong repository Godot Engine tại `/misc/dist/html/full-size.html <https://github.com/godotengine/godot/blob/master/misc/dist/html/full-size.html>`__ nhưng template sau đây có thể được dùng làm một ví dụ đơn giản hơn nhiều:

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
Như ví dụ trên cho thấy, đây phần lớn là một tài liệu HTML thông thường, với một vài placeholder cần được thay thế trong quá trình export, một phần tử html ``<canvas>``, và một đoạn mã JavaScript đơn giản gọi đến class :js:class:`Engine`.

Các placeholder bắt buộc duy nhất là:

- ``$GODOT_URL``: Tên của file JavaScript chính, cung cấp class :js:class:`Engine` cần thiết để khởi động engine và phải được đưa vào HTML dưới dạng ``<script>``. Tên này được tạo từ *Export Path* trong quá trình export.

- ``$GODOT_CONFIG``: Một đối tượng JavaScript chứa các tùy chọn export và có thể được ghi đè về sau. Xem :js:attr:`EngineConfig` để biết danh sách đầy đủ các giá trị ghi đè.

Các placeholder tùy chọn sau đây sẽ bật một số tính năng bổ sung trong template HTML tùy chỉnh của bạn.

- ``$GODOT_PROJECT_NAME``: Tên project được định nghĩa trong
  cài đặt :ref:`Name <class_ProjectSettings_property_application/config/name>` trong **Project Settings > Application > Config**. Bạn nên sử dụng nó làm một ``<title>`` trong template.

- ``$GODOT_HEAD_INCLUDE``: Một chuỗi tùy chỉnh được đưa vào tài liệu HTML ngay trước thẻ ``<head>`` kết thúc. Chuỗi này được tùy chỉnh trong các tùy chọn export, tại phần *Html / Head Include*. Mặc dù bạn hoàn toàn kiểm soát trang HTML mình tạo, biến này có thể hữu ích để cấu hình các phần của phần tử HTML ``head`` từ Godot Editor, chẳng hạn cho các preset export Web khác nhau.

- ``$GODOT_SPLASH``: Đường dẫn đến image được dùng làm boot splash, như được định nghĩa trong
  cài đặt :ref:`Image <class_ProjectSettings_property_application/boot_splash/image>` trong **Project Settings > Application > Boot Splash**.

- ``$GODOT_SPLASH_COLOR`` Màu nền của splash screen, như được định nghĩa trong
  cài đặt :ref:`BG Color <class_ProjectSettings_property_application/boot_splash/bg_color>` trong **Project Settings > Application > Boot Splash**, được chuyển đổi thành mã màu hex.

- ``$GODOT_SPLASH_CLASSES``: Placeholder này cung cấp một chuỗi gồm tên các cài đặt và giá trị của chúng, có ảnh hưởng đến splash screen. Chuỗi này được dùng làm một tập hợp tên class CSS, cho phép tạo kiểu cho splash image dựa trên các cài đặt splash của project. Các cài đặt sau đây trong **Project Settings > Application > Boot Splash** được cung cấp, và được biểu diễn bằng các tên class hiển thị bên dưới tùy theo giá trị boolean của cài đặt:

  - :ref:`Show Image <class_ProjectSettings_property_application/boot_splash/show_image>`: ``show-image--true``, ``show-image--false``
  - :ref:`Stretch Mode <class_ProjectSettings_property_application/boot_splash/stretch_mode>`: ``fullsize--true`` (nếu **not** Disabled), ``fullsize--false``
  - :ref:`Use Filter <class_ProjectSettings_property_application/boot_splash/use_filter>`: ``use-filter--true``, ``use-filter--false``

Khi trang tùy chỉnh đã sẵn sàng, bạn có thể chọn trang này trong các tùy chọn export, tại phần *Html / Custom Html Shell*.

.. image:: img/html5_export_options.png

Khởi động project
-----------------
Để có thể khởi động game, bạn cần viết một script khởi tạo engine — mã điều khiển. Quy trình này gồm ba bước, nhưng như minh họa ở đây, bạn có thể bỏ qua phần lớn các bước tùy thuộc vào mức độ tùy chỉnh cần thiết.

Xem :ref:`HTML5 shell class reference <doc_html5_shell_classref>` để biết danh sách đầy đủ các method và tùy chọn hiện có.

Trước tiên, engine phải được tải, sau đó được khởi tạo, và cuối cùng project mới có thể được khởi động. Bạn có thể thực hiện thủ công từng bước với mức độ kiểm soát cao. Tuy nhiên, trong trường hợp đơn giản nhất, bạn chỉ cần tạo một instance của class :js:class:`Engine` với cấu hình đã export, rồi gọi method :js:meth:`engine.startGame <Engine.prototype.startGame>`, đồng thời tùy chọn ghi đè bất kỳ tham số :js:attr:`EngineConfig` nào.

.. code-block:: js

    const engine = new Engine($GODOT_CONFIG);
    engine.startGame({
        // Cấu hình ghi đè tùy chọn, ví dụ:
        // hủy tải sau khi khởi tạo: false,
        // chính sách thay đổi kích thước canvas: 0,
        // ...
    });

Đoạn mã này tự động tải và khởi tạo engine trước khi khởi động game. Nó sử dụng cấu hình đã cho để tải engine. Method :js:meth:`engine.startGame <Engine.prototype.startGame>` là bất đồng bộ và trả về một ``Promise``. Nhờ đó, mã điều khiển của bạn có thể theo dõi xem game đã được tải đúng cách hay chưa mà không chặn việc thực thi hoặc phụ thuộc vào polling.

Nếu project của bạn cần kiểm soát đặc biệt các đối số khởi động và các file phụ thuộc, bạn có thể sử dụng method :js:meth:`engine.start <Engine.prototype.start>`. Lưu ý rằng method này không tự động preload file ``pck``, vì vậy có thể bạn sẽ muốn tự preload file đó (cùng mọi file bổ sung khác) bằng method :js:meth:`engine.preloadFile <Engine.prototype.preloadFile>`.

Tùy chọn, bạn cũng có thể gọi thủ công :js:meth:`engine.init <Engine.prototype.init>` để thực hiện các hành động cụ thể sau khi module được khởi tạo nhưng trước khi engine khởi động.

Quy trình này phức tạp hơn một chút nhưng cho phép bạn kiểm soát hoàn toàn quá trình khởi động engine.

.. code-block:: js

    const myWasm = 'mygame.wasm';
    const myPck = 'mygame.pck';
    const engine = new Engine();
    Promise.all([
        // Tải và khởi tạo engine
        engine.init(myWasm),
        // Và tải pck đồng thời
        engine.preloadFile(myPck),
    ]).then(() => {
        // Bây giờ khởi động engine.
        return engine.start({ args: ['--main-pack', myPck] });
    }).then(() => {
        console.log('Engine has started!');
    });

Để tải engine thủ công, phải gọi :js:meth:`Engine.load` static method. Vì method này là static, bạn có thể tạo nhiều instance engine nếu chúng dùng chung ``wasm``.

.. note:: Theo mặc định, không thể khởi chạy nhiều instance vì engine được dỡ tải ngay sau khi khởi tạo. Để ngăn điều này xảy ra, hãy xem tùy chọn override :js:attr:`unloadAfterInit`. Sau đó, bạn vẫn có thể dỡ tải engine theo cách thủ công bằng cách gọi static method :js:meth:`Engine.unload`. Việc dỡ tải engine giải phóng bộ nhớ trình duyệt bằng cách dỡ các tệp không còn cần thiết sau khi instance được khởi tạo.

Tùy chỉnh hành vi
-----------------
Trong môi trường Web, có thể sử dụng một số method để đảm bảo game hoạt động như mong muốn.

Nếu bạn nhắm đến một phiên bản WebGL cụ thể hoặc chỉ muốn kiểm tra xem WebGL có khả dụng hay không, bạn có thể gọi method :js:meth:`Engine.isWebGLAvailable`. Method này có thể nhận một đối số tùy chọn để kiểm tra một major version cụ thể của WebGL.

Vì tệp thực thi thực tế không tồn tại trong môi trường Web, engine chỉ lưu trữ một tên tệp ảo được tạo từ tên cơ sở của các tệp engine đã tải. Giá trị này ảnh hưởng đến đầu ra của
method :ref:`OS.get_executable_path() <class_OS_method_get_executable_path>` và xác định tên của main pack được tự động khởi động. Có thể sử dụng tùy chọn override :js:attr:`executable` để ghi đè giá trị này.

Tùy chỉnh phần trình bày
------------------------
Có thể sử dụng một số tùy chọn cấu hình để tùy chỉnh thêm giao diện và hành vi của game trên trang của bạn.

Theo mặc định, phần tử canvas đầu tiên trên trang được sử dụng để render. Để sử dụng một phần tử canvas khác, có thể dùng tùy chọn override :js:attr:`canvas`. Tùy chọn này yêu cầu tham chiếu đến chính phần tử DOM đó.

.. code-block:: js

    const canvasElement = document.querySelector("#my-canvas-element");
    engine.startGame({ canvas: canvasElement });

Có thể cấu hình cách engine thay đổi kích thước canvas thông qua tùy chọn override :js:attr:`canvasResizePolicy`.

Nếu game của bạn mất một khoảng thời gian để tải, việc hiển thị một loading UI tùy chỉnh để theo dõi tiến trình có thể hữu ích. Bạn có thể thực hiện điều này với tùy chọn callback :js:attr:`onProgress`, cho phép thiết lập một callback function sẽ được gọi thường xuyên khi engine tải các byte mới.

.. code-block:: js

    function printProgress(current, total) {
        console.log("Loaded " + current + " of " + total + " bytes");
    }
    engine.startGame({ onProgress: printProgress });

Lưu ý rằng trong một số trường hợp, ``total`` có thể là ``0``. Điều này có nghĩa là không thể tính toán giá trị đó.

Nếu game của bạn hỗ trợ nhiều ngôn ngữ, có thể sử dụng tùy chọn override :js:attr:`locale` để buộc dùng một locale cụ thể, miễn là bạn có một chuỗi mã ngôn ngữ hợp lệ. Bạn nên sử dụng logic phía server để xác định những ngôn ngữ mà người dùng có thể ưu tiên. Bằng cách này, mã ngôn ngữ có thể được lấy từ HTTP header ``Accept-Language`` hoặc được xác định bằng dịch vụ GeoIP.

Gỡ lỗi
------
Để gỡ lỗi các project đã export, việc đọc các stream standard output và error do engine tạo ra có thể hữu ích. Điều này tương tự đầu ra được hiển thị trong cửa sổ console của editor. Theo mặc định, standard ``console.log`` và ``console.warn`` lần lượt được sử dụng cho các stream output và error. Có thể tùy chỉnh hành vi này bằng cách đặt các function riêng để xử lý message.

Sử dụng tùy chọn override :js:attr:`onPrint` để đặt callback function cho stream output và tùy chọn override :js:attr:`onPrintError` để đặt callback function cho stream error.

.. code-block:: js

    function print(text) {
        console.log(text);
    }
    function printError(text) {
        console.warn(text);
    }
    engine.startGame({ onPrint: print, onPrintError: printError });

Khi xử lý output của engine, hãy nhớ rằng việc in output đó trong sản phẩm hoàn thiện có thể không phù hợp.
