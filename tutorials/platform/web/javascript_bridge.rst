.. _doc_web_javascript_bridge:

Singleton JavaScriptBridge
==========================

Trong các bản build web, singleton :ref:`JavaScriptBridge <class_JavaScriptBridge>` cho phép tương tác với JavaScript và trình duyệt web, đồng thời có thể được dùng để triển khai một số chức năng đặc thù của nền tảng web.

Tương tác với JavaScript
------------------------

Đôi khi, khi export Godot cho Web, bạn có thể cần tương tác với mã JavaScript bên ngoài như SDK của bên thứ ba, thư viện, hoặc chỉ đơn giản là truy cập các tính năng của trình duyệt chưa được Godot cung cấp trực tiếp.

Singleton ``JavaScriptBridge`` cung cấp các phương thức để bọc một đối tượng JavaScript native thành một :ref:`JavaScriptObject <class_JavaScriptObject>` của Godot, nhằm mang lại cảm giác tự nhiên trong ngữ cảnh viết script cho Godot (ví dụ: GDScript và C#).

Phương thức :ref:`JavaScriptBridge.get_interface() <class_JavaScriptBridge_method_get_interface>` lấy một đối tượng trong phạm vi global.

.. code-block:: gdscript

    extends Node

    func _ready():
        # Lấy đối tượng `window.console`.
        var console = JavaScriptBridge.get_interface("console")
        # Gọi phương thức `window.console.log()`.
        console.log("test")

:ref:`JavaScriptBridge.create_object() <class_JavaScriptBridge_method_create_object>` tạo một đối tượng mới thông qua constructor ``new`` của JavaScript.

.. code-block:: gdscript

    extends Node

    func _ready():
        # Gọi toán tử `new` của JavaScript trên đối tượng `window.Array`.
        # Truyền 10 làm đối số cho constructor:
        # JS: `new Array(10);`
        var arr = JavaScriptBridge.create_object("Array", 10)
        # Đặt phần tử đầu tiên của mảng JavaScript thành số 42.
        arr[0] = 42
        # Gọi hàm `pop` trên mảng JavaScript.
        arr.pop()
        # In giá trị thuộc tính `length` của mảng (bằng 9 sau khi pop).
        print(arr.length)

Như bạn thấy, bằng cách bọc các đối tượng JavaScript trong ``JavaScriptObject``, bạn có thể tương tác với chúng như thể chúng là các đối tượng native của Godot, gọi các phương thức và lấy (hoặc thậm chí đặt) các thuộc tính của chúng.

Các kiểu cơ bản (int, float, string, boolean) được tự động chuyển đổi (float có thể mất độ chính xác khi được chuyển từ Godot sang JavaScript). Mọi kiểu khác (tức là đối tượng, mảng, hàm) đều được xem là chính ``JavaScriptObjects``.

Callback
--------

Gọi mã JavaScript từ Godot rất tiện, nhưng đôi khi bạn lại cần gọi một hàm Godot từ JavaScript.

Trường hợp này phức tạp hơn một chút. JavaScript dựa vào garbage collection, còn Godot sử dụng reference counting để quản lý bộ nhớ. Điều này có nghĩa là bạn phải tạo callback một cách rõ ràng (được trả về dưới dạng chính ``JavaScriptObjects``) và phải giữ reference của chúng.

Các đối số mà JavaScript truyền vào callback sẽ được truyền dưới dạng một ``Array`` duy nhất của Godot.

.. code-block:: gdscript

    extends Node

    # Tại đây, chúng ta tạo một reference đến hàm `_my_callback` (bên dưới).
    # Reference này sẽ được giữ cho đến khi node được giải phóng.
    var _callback_ref = JavaScriptBridge.create_callback(_my_callback)

    func _ready():
        # Lấy đối tượng `window` của JavaScript.
        var window = JavaScriptBridge.get_interface("window")
        # Đặt trình lắng nghe sự kiện DOM `window.onbeforeunload`.
        window.onbeforeunload = _callback_ref

    func _my_callback(args):
        # Lấy đối số đầu tiên (trong trường hợp này là sự kiện DOM).
        var js_event = args[0]
        # Gọi preventDefault và đặt thuộc tính `returnValue` của sự kiện DOM.
        js_event.preventDefault()
        js_event.returnValue = ''

.. warning::

    Các phương thức callback được tạo thông qua :ref:`JavaScriptBridge.get_interface() <class_JavaScriptBridge_method_get_interface>` (``_my_callback`` trong ví dụ trên) **must** nhận chính xác một đối số :ref:`Array<class_Array>`, là `arguments object <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments>`__ của JavaScript được chuyển đổi thành một mảng. Nếu không, phương thức callback sẽ không được gọi.

Dưới đây là một ví dụ khác, yêu cầu người dùng cấp quyền `Notification permission <https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API>`__ và chờ bất đồng bộ để gửi thông báo nếu được cấp quyền:

.. code-block:: gdscript

    extends Node

    # Tại đây, chúng ta tạo một reference đến hàm `_on_permissions` (bên dưới).
    # Reference này sẽ được giữ cho đến khi node được giải phóng.
    var _permission_callback = JavaScriptBridge.create_callback(_on_permissions)

    func _ready():
        # LƯU Ý: Để đơn giản, việc này được thực hiện trong `_ready`, nhưng ĐÁNG RA PHẢI được thực hiện khi phản hồi
        # thao tác nhập của người dùng (ví dụ: trong `_input`, hoặc sự kiện `button_pressed`, v.v.),
        # nếu không, thao tác này có thể không hoạt động.

        # Lấy đối tượng JavaScript `window.Notification`.
        var notification = JavaScriptBridge.get_interface("Notification")
        # Gọi phương thức `window.Notification.requestPermission`, phương thức này trả về một JavaScript
        # Promise, rồi bind callback của chúng ta vào đó.
        notification.requestPermission().then(_permission_callback)

    func _on_permissions(args):
        # Đối số đầu tiên của callback này là chuỗi "granted" nếu quyền được cấp.
        var permission = args[0]
        if permission == "granted":
            print("Permission granted, sending notification.")
            # Tạo thông báo: `new Notification("Hi there!")`
            JavaScriptBridge.create_object("Notification", "Hi there!")
        else:
            print("No notification permission.")

Tôi có thể sử dụng thư viện yêu thích của mình không?
-----------------------------------------------------

Nhiều khả năng là có. Trước tiên, bạn phải đưa thư viện vào trang. Bạn có thể tùy chỉnh
:ref:`Head Include <doc_javascript_export_options>` trong quá trình export (xem bên dưới), hoặc thậm chí :ref:`tự viết template của riêng mình <doc_customizing_html5_shell>`.

Trong ví dụ bên dưới, chúng ta tùy chỉnh ``Head Include`` để thêm một thư viện bên ngoài (`axios <https://axios-http.com/>`__) từ một content delivery network, và thêm một thẻ ``<script>`` thứ hai để định nghĩa hàm tùy chỉnh của riêng mình:

.. code-block:: html

    <!-- Axios -->
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <!-- Hàm tùy chỉnh -->
    <script>
    function myFunc() {
        alert("My func!");
    }
    </script>

Sau đó, chúng ta có thể truy cập cả thư viện lẫn hàm từ Godot, như trong các ví dụ trước:

.. code-block:: gdscript

    extends Node

    # Tại đây, tạo một reference đến hàm `_on_get` (bên dưới).
    # Reference này sẽ được giữ cho đến khi node được giải phóng.
    var _callback = JavaScriptBridge.create_callback(_on_get)

    func _ready():
        # Lấy đối tượng `window`, nơi chứa các hàm được định nghĩa global.
        var window = JavaScriptBridge.get_interface("window")
        # Gọi hàm JavaScript `myFunc` được định nghĩa trong phần đầu HTML tùy chỉnh.
        window.myFunc()
        # Lấy thư viện `axios` (được tải từ CDN trong phần đầu HTML tùy chỉnh).
        var axios = JavaScriptBridge.get_interface("axios")
        # Gửi yêu cầu GET đến vị trí hiện tại và nhận callback khi hoàn tất.
        axios.get(window.location.toString()).then(_callback)

    func _on_get(args):
        OS.alert("On Get")


Giao diện eval
--------------

Phương thức ``eval`` hoạt động tương tự hàm JavaScript cùng tên. Phương thức này nhận một chuỗi làm đối số và thực thi chuỗi đó dưới dạng mã JavaScript. Điều này cho phép tương tác với trình duyệt theo những cách không thể thực hiện bằng các ngôn ngữ script được tích hợp vào Godot.

.. tabs::
 .. code-tab:: gdscript

    func my_func():
        JavaScriptBridge.eval("alert('Calling JavaScript per GDScript!');")

 .. code-tab:: csharp

    private void MyFunc()
    {
        JavaScriptBridge.Eval("alert('Calling JavaScript per C#!');")
    }

Giá trị của câu lệnh JavaScript cuối cùng được chuyển đổi thành giá trị GDScript và được ``eval()`` trả về trong một số trường hợp nhất định:

 * JavaScript ``number`` được trả về dưới dạng :ref:`class_float`
 * JavaScript ``boolean`` được trả về dưới dạng :ref:`class_bool`
 * JavaScript ``string`` được trả về dưới dạng :ref:`class_String`
 * JavaScript ``ArrayBuffer``, ``TypedArray`` và ``DataView`` được trả về dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`

.. tabs::
 .. code-tab:: gdscript

    func my_func2():
        var js_return = JavaScriptBridge.eval("var myNumber = 1; myNumber + 2;")
        print(js_return) # in ra '3.0'

 .. code-tab:: csharp

    private void MyFunc2()
    {
        var jsReturn = JavaScriptBridge.Eval("var myNumber = 1; myNumber + 2;");
        GD.Print(jsReturn); // in ra '3.0'
    }

Mọi giá trị JavaScript khác được trả về dưới dạng ``null``.

Các template xuất HTML5 có thể được :ref:`biên dịch <doc_compiling_for_web>` mà không hỗ trợ singleton này để tăng cường bảo mật. Với các template như vậy và trên những nền tảng khác HTML5, việc gọi ``JavaScriptBridge.eval`` cũng sẽ trả về ``null``. Có thể kiểm tra khả năng sẵn có của singleton bằng thẻ ``web`` :ref:`feature tag <doc_feature_tags>`:

.. tabs::
 .. code-tab:: gdscript

    func my_func3():
        if OS.has_feature('web'):
            JavaScriptBridge.eval("""
                console.log('The JavaScriptBridge singleton is available')
            """)
        else:
            print("The JavaScriptBridge singleton is NOT available")

 .. code-tab:: csharp

    private void MyFunc3()
    {
        if (OS.HasFeature("web"))
        {
            JavaScriptBridge.Eval("console.log('The JavaScriptBridge singleton is available')");
        }
        else
        {
            GD.Print("The JavaScriptBridge singleton is NOT available");
        }
    }

.. tip:: Các chuỗi nhiều dòng của GDScript, được bao quanh bởi 3 dấu ngoặc kép ``"""`` như trong ``my_func3()`` ở trên, hữu ích để giữ cho mã JavaScript dễ đọc.

Phương thức ``eval`` cũng chấp nhận một đối số Boolean tùy chọn thứ hai, chỉ định có thực thi mã trong ngữ cảnh thực thi toàn cục hay không; mặc định là ``false`` để tránh làm ô nhiễm namespace toàn cục:

.. tabs::
 .. code-tab:: gdscript

    func my_func4():
        # thực thi trong ngữ cảnh thực thi toàn cục,
        # do đó thêm một biến toàn cục JavaScript mới `SomeGlobal`
        JavaScriptBridge.eval("var SomeGlobal = {};", true)

 .. code-tab:: csharp

    private void MyFunc4()
    {
        // thực thi trong ngữ cảnh thực thi toàn cục,
        // do đó thêm một biến toàn cục JavaScript mới `SomeGlobal`
        JavaScriptBridge.Eval("var SomeGlobal = {};", true);
    }


.. _doc_web_downloading_files:

Tải xuống tệp
-------------

Có thể tải các tệp (ví dụ: tệp lưu trò chơi) từ bản xuất Godot Web xuống máy tính của người dùng bằng cách tương tác trực tiếp với JavaScript. Tuy nhiên, vì đây là một trường hợp sử dụng rất phổ biến, Godot cung cấp chức năng này cho scripting thông qua hàm :ref:`JavaScriptBridge.download_buffer() <class_JavaScriptBridge_method_download_buffer>` chuyên dụng, cho phép bạn tải xuống bất kỳ buffer nào đã tạo.

Sau đây là ví dụ tối giản về cách sử dụng:

extends Node

.. code-block:: gdscript

    func _ready():
        # Yêu cầu người dùng tải xuống một tệp có tên "hello.txt" với nội dung là chuỗi "Hello".
        JavaScriptBridge.download_buffer("Hello".to_utf8_buffer(), "hello.txt")

Sau đây là ví dụ đầy đủ hơn về cách tải xuống một tệp đã được lưu trước đó:

.. code-block:: gdscript

    extends Node

    # Mở một tệp để đọc và tải xuống tệp đó thông qua singleton JavaScript.
    func _download_file(path):
        var file = FileAccess.open(path, FileAccess.READ)
        if file == null:
            push_error("Failed to load file")
            return
        # Lấy tên tệp.
        var fname = path.get_file()
        # Đọc toàn bộ tệp vào bộ nhớ.
        var buffer = file.get_buffer(file.get_len())
        # Nhắc người dùng tải xuống tệp (tệp sẽ có cùng tên với tệp đầu vào).
        JavaScriptBridge.download_buffer(buffer, fname)

    func _ready():
        # Tạo một tệp tạm thời.
        var config = ConfigFile.new()
        config.set_value("option", "one", false)
        config.save("/tmp/test.cfg")

        # Tải xuống tệp đó
        _download_file("/tmp/test.cfg")
