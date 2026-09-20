.. _doc_http_request_class:

Tạo các yêu cầu HTTP
====================

Tại sao nên sử dụng HTTP?
-------------------------

`HTTP requests <https://developer.mozilla.org/en-US/docs/Web/HTTP>`_ hữu ích để giao tiếp với máy chủ web và các chương trình không phải Godot khác.

So với các tính năng networking khác của Godot (chẳng hạn như
:ref:`High-level multiplayer <doc_high_level_multiplayer>`),
Các yêu cầu HTTP có nhiều overhead hơn và mất nhiều thời gian hơn để bắt đầu, vì vậy chúng không phù hợp cho giao tiếp theo thời gian thực và cũng không tối ưu để gửi nhiều bản cập nhật nhỏ như thường thấy trong gameplay multiplayer.

Tuy nhiên, HTTP cung cấp khả năng tương tác với các tài nguyên web bên ngoài và rất phù hợp để gửi cũng như nhận lượng dữ liệu lớn, chẳng hạn như truyền các tệp game asset. Sau đó, các asset này có thể được tải bằng
:ref:`runtime file loading and saving <doc_runtime_loading_and_saving>`.

Vì vậy, HTTP có thể hữu ích cho hệ thống đăng nhập của game, trình duyệt lobby, việc lấy một số thông tin từ web hoặc tải xuống các asset của game.

Các yêu cầu HTTP trong Godot
----------------------------

Node :ref:`HTTPRequest <class_HTTPRequest>` là cách dễ nhất để tạo các yêu cầu HTTP trong Godot. Node này được xây dựng dựa trên :ref:`HTTPClient <class_HTTPClient>` cấp thấp hơn; bạn có thể xem hướng dẫn về node này :ref:`here <doc_http_client_class>`.

Trong ví dụ này, chúng ta sẽ gửi một yêu cầu HTTP đến GitHub để lấy tên của bản phát hành Godot mới nhất.

.. warning::

    Khi export sang **Android**, hãy đảm bảo bật quyền **Internet** trong export preset của Android trước khi export project hoặc sử dụng one-click deploy. Nếu không, hệ điều hành Android sẽ chặn mọi hình thức giao tiếp mạng.

Chuẩn bị scene
--------------

Tạo một scene trống mới, thêm một :ref:`Node <class_Node>` làm root và thêm một script vào đó. Sau đó, thêm một node :ref:`HTTPRequest <class_HTTPRequest>` làm node con.

.. image:: img/rest_api_scene.webp

Viết script cho yêu cầu
-----------------------

Khi project được khởi chạy (tức là trong ``_ready()``), chúng ta sẽ gửi một yêu cầu HTTP đến Github bằng node :ref:`HTTPRequest <class_HTTPRequest>`, và khi yêu cầu hoàn tất, chúng ta sẽ phân tích dữ liệu JSON được trả về, tìm trường ``name`` rồi in trường đó ra console.

.. tabs::

    .. code-tab:: gdscript GDScript

        extends Node

        func _ready():
            $HTTPRequest.request_completed.connect(_on_request_completed)
            $HTTPRequest.request("https://api.github.com/repos/godotengine/godot/releases/latest")

        func _on_request_completed(result, response_code, headers, body):
            var json = JSON.parse_string(body.get_string_from_utf8())
            print(json["name"])

    .. code-tab:: csharp

        using Godot;
        using System.Text;

        public partial class MyNode : Node
        {
            public override void _Ready()
            {
                HttpRequest httpRequest = GetNode<HttpRequest>("HTTPRequest");
                httpRequest.RequestCompleted += OnRequestCompleted;
                httpRequest.Request("https://api.github.com/repos/godotengine/godot/releases/latest");
            }

            private void OnRequestCompleted(long result, long responseCode, string[] headers, byte[] body)
            {
                Godot.Collections.Dictionary json = Json.ParseString(Encoding.UTF8.GetString(body)).AsGodotDictionary();
                GD.Print(json["name"]);
            }
        }

Lưu script và scene, sau đó chạy project. Tên của bản phát hành Godot gần đây nhất trên Github sẽ được in vào output log. Để biết thêm thông tin về cách phân tích JSON, hãy xem các tài liệu tham chiếu class của :ref:`JSON <class_JSON>`.

Lưu ý rằng bạn có thể muốn kiểm tra xem ``result`` có bằng ``RESULT_SUCCESS`` hay không và liệu có xảy ra lỗi phân tích JSON hay không; hãy xem tài liệu tham chiếu class JSON và
:ref:`HTTPRequest <class_HTTPRequest>` for more.

Bạn phải đợi một yêu cầu hoàn tất trước khi gửi yêu cầu khác. Để thực hiện nhiều yêu cầu cùng lúc, bạn cần có một node cho mỗi yêu cầu. Một chiến lược phổ biến là tạo và xóa các node HTTPRequest trong runtime khi cần.

Gửi dữ liệu đến máy chủ
-----------------------

Cho đến nay, chúng ta chỉ giới hạn ở việc yêu cầu dữ liệu từ máy chủ. Nhưng nếu bạn cần gửi dữ liệu đến máy chủ thì sao? Sau đây là một cách phổ biến để thực hiện việc đó:

.. tabs::

    .. code-tab:: gdscript GDScript

        var json = JSON.stringify(data_to_send)
        var headers = ["Content-Type: application/json"]
        $HTTPRequest.request(url, headers, HTTPClient.METHOD_POST, json)

    .. code-tab:: csharp

        string json = Json.Stringify(dataToSend);
        string[] headers = ["Content-Type: application/json"];
        HttpRequest httpRequest = GetNode<HttpRequest>("HTTPRequest");
        httpRequest.Request(url, headers, HttpClient.Method.Post, json);

Thiết lập HTTP header tùy chỉnh
-------------------------------

Tất nhiên, bạn cũng có thể thiết lập các HTTP header tùy chỉnh. Các header này được truyền dưới dạng một mảng chuỗi, trong đó mỗi chuỗi chứa một header theo định dạng ``"header: value"``. Ví dụ, để thiết lập user agent tùy chỉnh (HTTP ``User-Agent`` header), bạn có thể sử dụng đoạn mã sau:

.. tabs::

    .. code-tab:: gdscript GDScript

        $HTTPRequest.request("https://api.github.com/repos/godotengine/godot/releases/latest", ["User-Agent: YourCustomUserAgent"])

    .. code-tab:: csharp

        HttpRequest httpRequest = GetNode<HttpRequest>("HTTPRequest");
        httpRequest.Request("https://api.github.com/repos/godotengine/godot/releases/latest", ["User-Agent: YourCustomUserAgent"]);

.. danger::

    Hãy lưu ý rằng ai đó có thể phân tích và decompile ứng dụng bạn phát hành, từ đó có thể truy cập mọi thông tin xác thực được nhúng trong ứng dụng, chẳng hạn như token, username hoặc password. Điều đó có nghĩa là thông thường bạn không nên nhúng những thông tin như thông tin đăng nhập cơ sở dữ liệu vào trong game. Khi có thể, hãy tránh cung cấp thông tin hữu ích cho kẻ tấn công.
