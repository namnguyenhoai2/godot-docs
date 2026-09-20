:article_outdated: True

.. _doc_html5_shell_classref:

Tham chiếu lớp HTML5 shell
==========================

Các project được export cho Web expose lớp :js:class:`Engine` vào môi trường JavaScript, cho phép kiểm soát chi tiết quá trình khởi động của engine.

API này được xây dựng theo phương thức bất đồng bộ và yêu cầu hiểu biết cơ bản về `Promises <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises>`__.

Engine
------

Lớp ``Engine`` cung cấp các method để load và start các project đã export trên Web. Với các thiết lập export mặc định, lớp này đã là một phần của trang HTML được export. Để hiểu cách sử dụng thực tế lớp ``Engine``, hãy xem :ref:`Custom HTML page for Web export <doc_customizing_html5_shell>`.

Static Methods
~~~~~~~~~~~~~~

+---------+-----------------------------------------------------------------------------------------------+
| Promise | :js:attr:`load <Engine.load>` **(** string basePath **)**                                     |
+---------+-----------------------------------------------------------------------------------------------+
| void    | :js:attr:`unload <Engine.unload>` **(** **)**                                                 |
+---------+-----------------------------------------------------------------------------------------------+
| boolean | :js:attr:`isWebGLAvailable <Engine.isWebGLAvailable>` **(** *[ number majorVersion=1 ]* **)** |
+---------+-----------------------------------------------------------------------------------------------+

Instance Methods
~~~~~~~~~~~~~~~~

+---------+---------------------------------------------------------------------------------------------------------------+
| Promise | :js:attr:`init <Engine.prototype.init>` **(** *[ string basePath ]* **)**                                     |
+---------+---------------------------------------------------------------------------------------------------------------+
| Promise | :js:attr:`preloadFile <Engine.prototype.preloadFile>` **(** string\|ArrayBuffer file *[, string path ]* **)** |
+---------+---------------------------------------------------------------------------------------------------------------+
| Promise | :js:attr:`start <Engine.prototype.start>` **(** EngineConfig override **)**                                   |
+---------+---------------------------------------------------------------------------------------------------------------+
| Promise | :js:attr:`startGame <Engine.prototype.startGame>` **(** EngineConfig override **)**                           |
+---------+---------------------------------------------------------------------------------------------------------------+
| void    | :js:attr:`copyToFS <Engine.prototype.copyToFS>` **(** string path, ArrayBuffer buffer **)**                   |
+---------+---------------------------------------------------------------------------------------------------------------+
| void    | :js:attr:`requestQuit <Engine.prototype.requestQuit>` **(** **)**                                             |
+---------+---------------------------------------------------------------------------------------------------------------+

.. js:class:: Engine( initConfig )

   Tạo một instance Engine mới với cấu hình đã cho.

   :param EngineConfig initConfig: Cấu hình ban đầu cho instance này.

   **Static Methods**

   .. js:function:: load( basePath )

      Load engine từ base path được chỉ định.

      :param string basePath: Base path của engine cần load.

      :return:
         Một Promise được resolve sau khi engine được load.

      :rtype: Promise

   .. js:function:: unload( )

      Unload engine để giải phóng bộ nhớ.

      Method này sẽ được tự động gọi tùy theo cấu hình. Xem :js:attr:`unloadAfterInit`.

   .. js:function:: isWebGLAvailable( [ majorVersion=1 ] )

      Kiểm tra xem WebGL có khả dụng hay không. Có thể chỉ định một phiên bản WebGL cụ thể để kiểm tra.

      :param number majorVersion: Phiên bản WebGL chính cần kiểm tra.

      :return:
         Nếu phiên bản WebGL chính đã cho khả dụng.

      :rtype: boolean

   **Instance Methods**

   .. js:function:: prototype.init( [ basePath ] )

      Khởi tạo instance engine. Có thể truyền base path của engine để load engine nếu engine chưa được load. Xem :js:meth:`Engine.load`.

      :param string basePath: Base path của engine cần load.

      :return:
         Một ``Promise`` được resolve sau khi engine được load và khởi tạo.

      :rtype: Promise

   .. js:function:: prototype.preloadFile( file [, path ] )

      Load một file để file này có sẵn trong file system của instance khi instance chạy. Phải được gọi **trước** khi start instance.

      Nếu không được cung cấp, ``path`` sẽ được suy ra từ URL của file đã load.

      :param string\|ArrayBuffer file: File cần preload.

         Nếu là một ``string``, file sẽ được load từ path đó.

         Nếu là một ``ArrayBuffer`` hoặc một view trên đó, buffer sẽ được sử dụng làm nội dung của file.

      :param string path: Path mà qua đó file sẽ có thể được truy cập. Bắt buộc nếu ``file`` không phải là một string.

      :return:
         Một Promise được resolve sau khi file được load.

      :rtype: Promise

   .. js:function:: prototype.start( override )

      Start instance engine bằng cấu hình override đã cho (nếu có).
      :js:meth:`startGame <Engine.prototype.startGame>` can be used in typical cases instead.

      Thao tác này sẽ khởi tạo instance nếu instance chưa được khởi tạo. Để khởi tạo thủ công, hãy xem :js:meth:`init <Engine.prototype.init>`. Engine phải được load trước.

      Thao tác này sẽ thất bại nếu không tìm thấy canvas trên trang hoặc canvas không được chỉ định trong cấu hình.

      :param EngineConfig override: Cấu hình override tùy chọn.

      :return:
         Promise được resolve sau khi engine start.

      :rtype: Promise

   .. js:function:: prototype.startGame( override )

      Start instance game bằng cấu hình override đã cho (nếu có).

      Thao tác này sẽ khởi tạo instance nếu instance chưa được khởi tạo. Để khởi tạo thủ công, hãy xem :js:meth:`init <Engine.prototype.init>`.

      Thao tác này sẽ load engine nếu engine chưa được load và preload pck chính.

      Method này yêu cầu config ban đầu (hoặc override) có cả hai property :js:attr:`executable` và :js:attr:`mainPack` được thiết lập (thông thường được thực hiện bởi editor trong quá trình export).

      :param EngineConfig override: Cấu hình override tùy chọn.

      :return:
         Promise được resolve sau khi game start.

      :rtype: Promise

   .. js:function:: prototype.copyToFS( path, buffer )

      Tạo một file tại ``path`` đã chỉ định với giá trị được truyền vào dưới dạng ``buffer`` trong file system của instance.

      :param string path: Vị trí nơi file sẽ được tạo.

      :param ArrayBuffer buffer: Nội dung của file.

   .. js:function:: prototype.requestQuit( )

      Yêu cầu instance hiện tại thoát.

      Thao tác này tương tự như việc người dùng nhấn nút đóng trong window manager và sẽ không có tác dụng nếu engine đã bị crash hoặc bị mắc kẹt trong một vòng lặp.

Cấu hình engine
---------------

Một object được dùng để cấu hình instance Engine dựa trên các tùy chọn export của godot và override các tùy chọn đó trong custom HTML template nếu cần.

Properties
~~~~~~~~~~

+-------------------+-------------------------------+
| type              | name                          |
+-------------------+-------------------------------+
| boolean           | :js:attr:`unloadAfterInit`    |
+-------------------+-------------------------------+
| HTMLCanvasElement | :js:attr:`canvas`             |
+-------------------+-------------------------------+
| string            | :js:attr:`executable`         |
+-------------------+-------------------------------+
| string            | :js:attr:`mainPack`           |
+-------------------+-------------------------------+
| string            | :js:attr:`locale`             |
+-------------------+-------------------------------+
| number            | :js:attr:`canvasResizePolicy` |
+-------------------+-------------------------------+
| Array.<string>    | :js:attr:`args`               |
+-------------------+-------------------------------+
| function          | :js:attr:`onExecute`          |
+-------------------+-------------------------------+
| function          | :js:attr:`onExit`             |
+-------------------+-------------------------------+
| function          | :js:attr:`onProgress`         |
+-------------------+-------------------------------+
| function          | :js:attr:`onPrint`            |
+-------------------+-------------------------------+
| function          | :js:attr:`onPrintError`       |
+-------------------+-------------------------------+

.. js:attribute:: EngineConfig

   Object cấu hình Engine. Đây chỉ là một typedef; hãy tạo nó như một object thông thường, ví dụ:

   ``const MyConfig = { executable: 'godot', unloadAfterInit: false }``

   **Mô tả Property**

   .. js:attribute:: unloadAfterInit

      Có unload engine tự động sau khi instance được khởi tạo hay không.

      :type: boolean

      :value: ``true``

   .. js:attribute:: canvas

      HTML DOM Canvas object cần sử dụng.

      Theo mặc định, phần tử canvas đầu tiên trong document sẽ được sử dụng nếu không có phần tử nào được chỉ định.

      :type: HTMLCanvasElement

      :value: ``null``

   .. js:attribute:: executable

      Tên của file WASM không có phần mở rộng. (Được thiết lập bởi quy trình export của Godot Editor).

      :type: string

      :value: ``""``

   .. js:attribute:: mainPack

      Tên thay thế cho game pck cần load. Nếu không, tên executable sẽ được sử dụng.

      :type: string

      :value: ``null``

   .. js:attribute:: locale

      Chỉ định mã ngôn ngữ để chọn bản localization phù hợp cho game.

      Locale của browser sẽ được sử dụng nếu không được chỉ định. Xem danh sách đầy đủ của
      :ref:`supported locales <doc_locales>`.

      :type: string

      :value: ``null``

   .. js:attribute:: canvasResizePolicy

      Chính sách resize canvas xác định cách canvas được Godot resize.

      ``0`` có nghĩa là Godot sẽ không thực hiện resize nào. Điều này hữu ích nếu bạn muốn kiểm soát kích thước canvas từ code JavaScript trong template.

      ``1`` có nghĩa là Godot sẽ resize canvas khi start và khi thay đổi kích thước cửa sổ thông qua các function của engine.

      ``2`` có nghĩa là Godot sẽ điều chỉnh kích thước canvas để khớp với toàn bộ cửa sổ browser.

      :type: number

      :value: ``2``

   .. js:attribute:: args

      Các argument sẽ được truyền dưới dạng command-line argument khi khởi động.

      Xem :ref:`command line tutorial <doc_command_line_tutorial>`.

      **Lưu ý**: :js:meth:`startGame <Engine.prototype.startGame>` sẽ luôn thêm argument ``--main-pack``.

      :type: Array.<string>

      :value: ``[]``

   .. js:function:: onExecute( path, args )

      Một callback function để xử lý các lệnh gọi ``OS.execute`` của Godot.

      Ví dụ, function này được sử dụng trong Web Editor template để chuyển đổi giữa Project Manager và editor, cũng như để chạy game.

      :param string path: Path mà Godot muốn thực thi.

      :param Array.<string> args: Các argument của "command" cần thực thi.

   .. js:function:: onExit( status_code )

      Một callback function để thông báo khi instance Godot thoát.

      **Lưu ý**: Function này sẽ không được gọi nếu engine bị crash hoặc trở nên không phản hồi.

      :param number status_code: Status code do Godot trả về khi thoát.

   .. js:function:: onProgress( current, total )

      Một callback function để hiển thị tiến trình download.

      Function được gọi một lần mỗi frame trong khi download file, vì vậy không cần sử dụng ``requestAnimationFrame()``.

      Nếu callback function nhận tổng số byte là 0, điều đó có nghĩa là không thể tính toán. Các lý do có thể gồm:

      -  File được phân phối bằng chunked compression phía server - File được phân phối bằng compression phía server trên Chromium - Chưa bắt đầu download tất cả file (thường xảy ra trên các server không hỗ trợ multi-threading)

      :param number current: Số byte hiện đã download được.

      :param number total: Tổng số byte cần download.

   .. js:function:: onPrint( [ ...var_args ] )

      Một callback function để xử lý standard output stream. Method này thường chỉ nên được sử dụng trong các debug page.

      Theo mặc định, ``console.log()`` được sử dụng.

      :param * var_args: Số lượng argument biến thiên cần được in.

   .. js:function:: onPrintError( [ ...var_args ] )

      Một callback function để xử lý standard error stream. Method này thường chỉ nên được sử dụng trong các debug page.

      Theo mặc định, ``console.error()`` được sử dụng.

      :param * var_args: Số lượng argument biến thiên cần được in dưới dạng lỗi.
