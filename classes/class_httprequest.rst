:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/HTTPRequest.xml.

.. _class_HTTPRequest:

HTTPRequest
===========

**Kế thừa:** :ref:`Node<class_Node>` **<** :ref:`Object<class_Object>`

Một node có khả năng gửi các request HTTP(S).

.. rst-class:: classref-introduction-group

Mô tả
-----

Một node có khả năng gửi các request HTTP. Sử dụng :ref:`HTTPClient<class_HTTPClient>` ở bên trong.

Có thể được dùng để thực hiện các request HTTP, chẳng hạn như tải xuống hoặc tải lên tệp hay nội dung web qua HTTP.

\ **Cảnh báo:** Hãy xem các ghi chú và cảnh báo về :ref:`HTTPClient<class_HTTPClient>` để biết các giới hạn, đặc biệt là về bảo mật TLS.

\ **Lưu ý:** Khi export sang Android, hãy đảm bảo bật quyền ``INTERNET`` trong export preset của Android trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi loại giao tiếp mạng.

\ **Ví dụ:** Liên hệ với một REST API và in ra một trong các trường được trả về:


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        # Tạo một node HTTP request và kết nối signal hoàn tất của nó.
        var http_request = HTTPRequest.new()
        add_child(http_request)
        http_request.request_completed.connect(self._http_request_completed)

        # Thực hiện request GET. URL bên dưới trả về JSON tại thời điểm viết tài liệu này.
        var error = http_request.request("https://httpbin.org/get")
        if error != OK:
            push_error("An error occurred in the HTTP request.")

        # Thực hiện request POST. URL bên dưới trả về JSON tại thời điểm viết tài liệu này.
        # Note: Don't make simultaneous requests using a single HTTPRequest node.
        # Đoạn mã bên dưới chỉ được cung cấp để tham khảo.
        var body = JSON.stringify({"name": "Godette"})
        error = http_request.request("https://httpbin.org/post", [], HTTPClient.METHOD_POST, body)
        if error != OK:
            push_error("An error occurred in the HTTP request.")

    # Được gọi khi HTTP request hoàn tất.
    func _http_request_completed(result, response_code, headers, body):
        var json = JSON.new()
        json.parse(body.get_string_from_utf8())
        var response = json.get_data()

        # Sẽ in ra chuỗi user agent được node HTTPRequest sử dụng (theo nhận diện của httpbin.org).
        print(response.headers["User-Agent"])

 .. code-tab:: csharp

    public override void _Ready()
    {
        // Tạo một node HTTP request và kết nối signal hoàn tất của nó.
        var httpRequest = new HttpRequest();
        AddChild(httpRequest);
        httpRequest.RequestCompleted += HttpRequestCompleted;

        // Thực hiện request GET. URL bên dưới trả về JSON tại thời điểm viết tài liệu này.
        Error error = httpRequest.Request("https://httpbin.org/get");
        if (error != Error.Ok)
        {
            GD.PushError("An error occurred in the HTTP request.");
        }

        // Thực hiện request POST. URL bên dưới trả về JSON tại thời điểm viết tài liệu này.
        // Note: Don't make simultaneous requests using a single HTTPRequest node.
        // Đoạn mã bên dưới chỉ được cung cấp để tham khảo.
        string body = Json.Stringify(new Godot.Collections.Dictionary
        {
            { "name", "Godette" }
        });
        error = httpRequest.Request("https://httpbin.org/post", null, HttpClient.Method.Post, body);
        if (error != Error.Ok)
        {
            GD.PushError("An error occurred in the HTTP request.");
        }
    }

    // Được gọi khi HTTP request hoàn tất.
    private void HttpRequestCompleted(long result, long responseCode, string[] headers, byte[] body)
    {
        var json = new Json();
        json.Parse(body.GetStringFromUtf8());
        var response = json.GetData().AsGodotDictionary();

        // Sẽ in ra chuỗi user agent được node HTTPRequest sử dụng (theo nhận diện của httpbin.org).
        GD.Print((response["headers"].AsGodotDictionary())["User-Agent"]);
    }



\ **Ví dụ:** Tải một hình ảnh bằng **HTTPRequest** và hiển thị hình ảnh đó:


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        # Tạo một node HTTP request và kết nối signal hoàn tất của nó.
        var http_request = HTTPRequest.new()
        add_child(http_request)
        http_request.request_completed.connect(self._http_request_completed)

        # Thực hiện HTTP request. URL bên dưới trả về hình ảnh PNG tại thời điểm viết tài liệu này.
        var error = http_request.request("https://placehold.co/512.png")
        if error != OK:
            push_error("An error occurred in the HTTP request.")

    # Được gọi khi HTTP request hoàn tất.
    func _http_request_completed(result, response_code, headers, body):
        if result != HTTPRequest.RESULT_SUCCESS:
            push_error("Image couldn't be downloaded. Try a different image.")

        var image = Image.new()
        var error = image.load_png_from_buffer(body)
        if error != OK:
            push_error("Couldn't load the image.")

        var texture = ImageTexture.create_from_image(image)

        # Hiển thị hình ảnh trong một node TextureRect.
        var texture_rect = TextureRect.new()
        add_child(texture_rect)
        texture_rect.texture = texture

 .. code-tab:: csharp

    public override void _Ready()
    {
        // Tạo một node HTTP request và kết nối signal hoàn tất của nó.
        var httpRequest = new HttpRequest();
        AddChild(httpRequest);
        httpRequest.RequestCompleted += HttpRequestCompleted;

        // Thực hiện HTTP request. URL bên dưới trả về hình ảnh PNG tại thời điểm viết tài liệu này.
        Error error = httpRequest.Request("https://placehold.co/512.png");
        if (error != Error.Ok)
        {
            GD.PushError("An error occurred in the HTTP request.");
        }
    }

    // Được gọi khi HTTP request hoàn tất.
    private void HttpRequestCompleted(long result, long responseCode, string[] headers, byte[] body)
    {
        if (result != (long)HttpRequest.Result.Success)
        {
            GD.PushError("Image couldn't be downloaded. Try a different image.");
        }
        var image = new Image();
        Error error = image.LoadPngFromBuffer(body);
        if (error != Error.Ok)
        {
            GD.PushError("Couldn't load the image.");
        }

        var texture = ImageTexture.CreateFromImage(image);

        // Hiển thị hình ảnh trong một node TextureRect.
        var textureRect = new TextureRect();
        AddChild(textureRect);
        textureRect.Texture = texture;
    }



\ **Lưu ý:** Các node **HTTPRequest** sẽ tự động xử lý việc giải nén response body. Một header ``Accept-Encoding`` sẽ được tự động thêm vào mỗi request của bạn, trừ khi header đó đã được chỉ định. Bất kỳ response nào có header ``Content-Encoding: gzip`` sẽ được tự động giải nén và gửi đến bạn dưới dạng các byte chưa nén.

.. rst-class:: classref-introduction-group

Hướng dẫn
---------

- :doc:`Tạo HTTP request <../tutorials/networking/http_request_class>`

- :doc:`Chứng chỉ TLS <../tutorials/networking/ssl_certificates>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`     | :ref:`accept_gzip<class_HTTPRequest_property_accept_gzip>`                 | ``true``  |
   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`       | :ref:`body_size_limit<class_HTTPRequest_property_body_size_limit>`         | ``-1``    |
   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`       | :ref:`download_chunk_size<class_HTTPRequest_property_download_chunk_size>` | ``65536`` |
   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`String<class_String>` | :ref:`download_file<class_HTTPRequest_property_download_file>`             | ``""``    |
   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`       | :ref:`max_redirects<class_HTTPRequest_property_max_redirects>`             | ``8``     |
   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`   | :ref:`timeout<class_HTTPRequest_property_timeout>`                         | ``0.0``   |
   +-----------------------------+----------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`     | :ref:`use_threads<class_HTTPRequest_property_use_threads>`                 | ``false`` |
   +-----------------------------+----------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`cancel_request<class_HTTPRequest_method_cancel_request>`\ (\ )                                                                                                                                                                                                                                                                  |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`get_body_size<class_HTTPRequest_method_get_body_size>`\ (\ ) |const|                                                                                                                                                                                                                                                            |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                 | :ref:`get_downloaded_bytes<class_HTTPRequest_method_get_downloaded_bytes>`\ (\ ) |const|                                                                                                                                                                                                                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Status<enum_HTTPClient_Status>` | :ref:`get_http_client_status<class_HTTPRequest_method_get_http_client_status>`\ (\ ) |const|                                                                                                                                                                                                                                          |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`request<class_HTTPRequest_method_request>`\ (\ url\: :ref:`String<class_String>`, custom_headers\: :ref:`PackedStringArray<class_PackedStringArray>` = PackedStringArray(), method\: :ref:`Method<enum_HTTPClient_Method>` = 0, request_data\: :ref:`String<class_String>` = ""\ )                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`request_raw<class_HTTPRequest_method_request_raw>`\ (\ url\: :ref:`String<class_String>`, custom_headers\: :ref:`PackedStringArray<class_PackedStringArray>` = PackedStringArray(), method\: :ref:`Method<enum_HTTPClient_Method>` = 0, request_data_raw\: :ref:`PackedByteArray<class_PackedByteArray>` = PackedByteArray()\ ) |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_http_proxy<class_HTTPRequest_method_set_http_proxy>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ )                                                                                                                                                                                                |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_https_proxy<class_HTTPRequest_method_set_https_proxy>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ )                                                                                                                                                                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`set_tls_options<class_HTTPRequest_method_set_tls_options>`\ (\ client_options\: :ref:`TLSOptions<class_TLSOptions>`\ )                                                                                                                                                                                                          |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_HTTPRequest_signal_request_completed:

.. rst-class:: classref-signal

**request_completed**\ (\ result\: :ref:`int<class_int>`, response_code\: :ref:`int<class_int>`, headers\: :ref:`PackedStringArray<class_PackedStringArray>`, body\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_HTTPRequest_signal_request_completed>`

Được phát ra khi một request hoàn tất.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_HTTPRequest_Result:

.. rst-class:: classref-enumeration

enum **Result**: :ref:`🔗<enum_HTTPRequest_Result>`

.. _class_HTTPRequest_constant_RESULT_SUCCESS:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_SUCCESS** = ``0``

Request thành công.

.. _class_HTTPRequest_constant_RESULT_CHUNKED_BODY_SIZE_MISMATCH:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_CHUNKED_BODY_SIZE_MISMATCH** = ``1``

Request thất bại do kích thước chunked body dự kiến không khớp với kích thước thực tế trong quá trình truyền. Các nguyên nhân có thể bao gồm lỗi mạng, cấu hình máy chủ không đúng hoặc sự cố với chunked encoding.

.. _class_HTTPRequest_constant_RESULT_CANT_CONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_CANT_CONNECT** = ``2``

Request thất bại trong khi kết nối.

.. _class_HTTPRequest_constant_RESULT_CANT_RESOLVE:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_CANT_RESOLVE** = ``3``

Request thất bại trong khi phân giải.

.. _class_HTTPRequest_constant_RESULT_CONNECTION_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_CONNECTION_ERROR** = ``4``

Request thất bại do lỗi kết nối (đọc/ghi).

.. _class_HTTPRequest_constant_RESULT_TLS_HANDSHAKE_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_TLS_HANDSHAKE_ERROR** = ``5``

Request thất bại trong quá trình bắt tay TLS.

.. _class_HTTPRequest_constant_RESULT_NO_RESPONSE:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_NO_RESPONSE** = ``6``

Request chưa có response (tại thời điểm này).

.. _class_HTTPRequest_constant_RESULT_BODY_SIZE_LIMIT_EXCEEDED:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_BODY_SIZE_LIMIT_EXCEEDED** = ``7``

Request đã vượt quá giới hạn kích thước tối đa, xem :ref:`body_size_limit<class_HTTPRequest_property_body_size_limit>`.

.. _class_HTTPRequest_constant_RESULT_BODY_DECOMPRESS_FAILED:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_BODY_DECOMPRESS_FAILED** = ``8``

Request thất bại do lỗi trong khi giải nén response body. Các nguyên nhân có thể bao gồm định dạng nén không được hỗ trợ hoặc không đúng, dữ liệu bị hỏng hoặc quá trình truyền chưa hoàn tất.

.. _class_HTTPRequest_constant_RESULT_REQUEST_FAILED:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_REQUEST_FAILED** = ``9``

Request thất bại (hiện chưa được sử dụng).

.. _class_HTTPRequest_constant_RESULT_DOWNLOAD_FILE_CANT_OPEN:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_DOWNLOAD_FILE_CANT_OPEN** = ``10``

HTTPRequest không thể mở tệp tải xuống.

.. _class_HTTPRequest_constant_RESULT_DOWNLOAD_FILE_WRITE_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_DOWNLOAD_FILE_WRITE_ERROR** = ``11``

HTTPRequest không thể ghi vào tệp tải xuống.

.. _class_HTTPRequest_constant_RESULT_REDIRECT_LIMIT_REACHED:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_REDIRECT_LIMIT_REACHED** = ``12``

Request đã đạt đến giới hạn redirect tối đa, xem :ref:`max_redirects<class_HTTPRequest_property_max_redirects>`.

.. _class_HTTPRequest_constant_RESULT_TIMEOUT:

.. rst-class:: classref-enumeration-constant

:ref:`Result<enum_HTTPRequest_Result>` **RESULT_TIMEOUT** = ``13``

Request thất bại do timeout. Nếu bạn dự kiến request sẽ mất nhiều thời gian, hãy thử tăng giá trị của :ref:`timeout<class_HTTPRequest_property_timeout>` hoặc đặt nó thành ``0.0`` để loại bỏ hoàn toàn timeout.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_HTTPRequest_property_accept_gzip:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **accept_gzip** = ``true`` :ref:`🔗<class_HTTPRequest_property_accept_gzip>`

.. rst-class:: classref-property-setget

- |void| **set_accept_gzip**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_accepting_gzip**\ (\ )

Nếu ``true``, header này sẽ được thêm vào mỗi request: ``Accept-Encoding: gzip, deflate``, cho máy chủ biết rằng có thể nén response body.

Mọi Response body khai báo ``Content-Encoding`` là ``gzip`` hoặc ``deflate`` sau đó sẽ được tự động giải nén, và các byte chưa nén sẽ được gửi qua :ref:`request_completed<class_HTTPRequest_signal_request_completed>`.

Nếu người dùng đã chỉ định header ``Accept-Encoding`` của riêng mình thì sẽ không có header nào được thêm vào, bất kể :ref:`accept_gzip<class_HTTPRequest_property_accept_gzip>`.

Nếu ``false`` thì sẽ không có header nào được thêm vào và không thực hiện giải nén response body. Các byte thô của response body sẽ được trả về qua :ref:`request_completed<class_HTTPRequest_signal_request_completed>`.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_property_body_size_limit:

.. rst-class:: classref-property

:ref:`int<class_int>` **body_size_limit** = ``-1`` :ref:`🔗<class_HTTPRequest_property_body_size_limit>`

.. rst-class:: classref-property-setget

- |void| **set_body_size_limit**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_body_size_limit**\ (\ )

Kích thước tối đa cho phép của response body. Nếu response body được nén, giá trị này sẽ được dùng làm kích thước tối đa cho phép của body sau khi giải nén.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_property_download_chunk_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **download_chunk_size** = ``65536`` :ref:`🔗<class_HTTPRequest_property_download_chunk_size>`

.. rst-class:: classref-property-setget

- |void| **set_download_chunk_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_download_chunk_size**\ (\ )

Kích thước của buffer được sử dụng và số byte tối đa được đọc trong mỗi lần lặp. Xem :ref:`HTTPClient.read_chunk_size<class_HTTPClient_property_read_chunk_size>`.

Đặt giá trị này thấp hơn (ví dụ: 4096 cho 4 KiB) khi tải xuống các tệp nhỏ để giảm mức sử dụng bộ nhớ, đổi lại tốc độ tải xuống sẽ thấp hơn.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_property_download_file:

.. rst-class:: classref-property

:ref:`String<class_String>` **download_file** = ``""`` :ref:`🔗<class_HTTPRequest_property_download_file>`

.. rst-class:: classref-property-setget

- |void| **set_download_file**\ (\ value\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_download_file**\ (\ )

Tệp để tải xuống. Mọi tệp nhận được sẽ được ghi vào tệp này.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_property_max_redirects:

.. rst-class:: classref-property

:ref:`int<class_int>` **max_redirects** = ``8`` :ref:`🔗<class_HTTPRequest_property_max_redirects>`

.. rst-class:: classref-property-setget

- |void| **set_max_redirects**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_max_redirects**\ (\ )

Số redirect tối đa được phép.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_property_timeout:

.. rst-class:: classref-property

:ref:`float<class_float>` **timeout** = ``0.0`` :ref:`🔗<class_HTTPRequest_property_timeout>`

.. rst-class:: classref-property-setget

- |void| **set_timeout**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_timeout**\ (\ )

Khoảng thời gian chờ trước khi một request timeout, tính bằng giây (độc lập với :ref:`Engine.time_scale<class_Engine_property_time_scale>`). Nếu :ref:`timeout<class_HTTPRequest_property_timeout>` được đặt thành ``0.0``, request sẽ không bao giờ timeout.

Đối với các request đơn giản, chẳng hạn như giao tiếp với một REST API, bạn nên đặt :ref:`timeout<class_HTTPRequest_property_timeout>` thành giá trị phù hợp với thời gian response của máy chủ (thường nằm trong khoảng từ ``1.0`` đến ``10.0``). Điều này giúp ngăn timeout không mong muốn do thời gian response thay đổi, đồng thời vẫn cho phép ứng dụng phát hiện khi request đã timeout. Đối với các request lớn hơn như tải tệp xuống, bạn nên đặt :ref:`timeout<class_HTTPRequest_property_timeout>` thành ``0.0``, để tắt chức năng timeout. Điều này giúp ngăn các lần truyền dữ liệu lớn thất bại do vượt quá giá trị timeout.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_property_use_threads:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **use_threads** = ``false`` :ref:`🔗<class_HTTPRequest_property_use_threads>`

.. rst-class:: classref-property-setget

- |void| **set_use_threads**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_using_threads**\ (\ )

Nếu ``true``, tính đa luồng được sử dụng để cải thiện hiệu suất.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_HTTPRequest_method_cancel_request:

.. rst-class:: classref-method

|void| **cancel_request**\ (\ ) :ref:`🔗<class_HTTPRequest_method_cancel_request>`

Hủy request hiện tại.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_get_body_size:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_body_size**\ (\ ) |const| :ref:`🔗<class_HTTPRequest_method_get_body_size>`

Trả về độ dài body của response.

\ **Lưu ý:** Một số Web server có thể không gửi độ dài body. Trong trường hợp này, giá trị được trả về sẽ là ``-1``. Nếu sử dụng chunked transfer encoding, độ dài body cũng sẽ là ``-1``.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_get_downloaded_bytes:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_downloaded_bytes**\ (\ ) |const| :ref:`🔗<class_HTTPRequest_method_get_downloaded_bytes>`

Trả về số byte mà HTTPRequest này đã tải xuống.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_get_http_client_status:

.. rst-class:: classref-method

:ref:`Status<enum_HTTPClient_Status>` **get_http_client_status**\ (\ ) |const| :ref:`🔗<class_HTTPRequest_method_get_http_client_status>`

Trả về trạng thái hiện tại của :ref:`HTTPClient<class_HTTPClient>` bên dưới.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_request:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **request**\ (\ url\: :ref:`String<class_String>`, custom_headers\: :ref:`PackedStringArray<class_PackedStringArray>` = PackedStringArray(), method\: :ref:`Method<enum_HTTPClient_Method>` = 0, request_data\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_HTTPRequest_method_request>`

Tạo request trên :ref:`HTTPClient<class_HTTPClient>` bên dưới. Nếu không có lỗi cấu hình, phương thức này sẽ cố gắng kết nối bằng :ref:`HTTPClient.connect_to_host()<class_HTTPClient_method_connect_to_host>` và truyền các tham số cho :ref:`HTTPClient.request()<class_HTTPClient_method_request>`.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu request được tạo thành công. (Điều này không có nghĩa là server đã phản hồi), :ref:`@GlobalScope.ERR_UNCONFIGURED<class_@GlobalScope_constant_ERR_UNCONFIGURED>` nếu không ở trong tree, :ref:`@GlobalScope.ERR_BUSY<class_@GlobalScope_constant_ERR_BUSY>` nếu vẫn đang xử lý request trước đó, :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu chuỗi đã cho không có định dạng URL hợp lệ hoặc :ref:`@GlobalScope.ERR_CANT_CONNECT<class_@GlobalScope_constant_ERR_CANT_CONNECT>` nếu không sử dụng thread và :ref:`HTTPClient<class_HTTPClient>` không thể kết nối đến host.

\ **Lưu ý:** Khi ``method`` là :ref:`HTTPClient.METHOD_GET<class_HTTPClient_constant_METHOD_GET>`, payload được gửi qua ``request_data`` có thể bị server bỏ qua hoặc thậm chí khiến server từ chối request (xem `RFC 7231 section 4.3.1 <https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.1>`__ để biết thêm chi tiết). Một cách khắc phục là gửi dữ liệu dưới dạng query string trong URL (xem :ref:`String.uri_encode()<class_String_method_uri_encode>` để biết ví dụ).

\ **Lưu ý:** Bạn nên sử dụng mã hóa truyền tải (TLS) và tránh gửi thông tin nhạy cảm (chẳng hạn như thông tin đăng nhập) trong các tham số URL của HTTP GET. Thay vào đó, hãy cân nhắc sử dụng request HTTP POST hoặc HTTP headers cho những thông tin này.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_request_raw:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **request_raw**\ (\ url\: :ref:`String<class_String>`, custom_headers\: :ref:`PackedStringArray<class_PackedStringArray>` = PackedStringArray(), method\: :ref:`Method<enum_HTTPClient_Method>` = 0, request_data_raw\: :ref:`PackedByteArray<class_PackedByteArray>` = PackedByteArray()\ ) :ref:`🔗<class_HTTPRequest_method_request_raw>`

Tạo request trên :ref:`HTTPClient<class_HTTPClient>` bên dưới bằng một mảng byte thô cho body của request. Nếu không có lỗi cấu hình, phương thức này sẽ cố gắng kết nối bằng :ref:`HTTPClient.connect_to_host()<class_HTTPClient_method_connect_to_host>` và truyền các tham số cho :ref:`HTTPClient.request()<class_HTTPClient_method_request>`.

Trả về :ref:`@GlobalScope.OK<class_@GlobalScope_constant_OK>` nếu request được tạo thành công. (Điều này không có nghĩa là server đã phản hồi), :ref:`@GlobalScope.ERR_UNCONFIGURED<class_@GlobalScope_constant_ERR_UNCONFIGURED>` nếu không ở trong tree, :ref:`@GlobalScope.ERR_BUSY<class_@GlobalScope_constant_ERR_BUSY>` nếu vẫn đang xử lý request trước đó, :ref:`@GlobalScope.ERR_INVALID_PARAMETER<class_@GlobalScope_constant_ERR_INVALID_PARAMETER>` nếu chuỗi đã cho không có định dạng URL hợp lệ hoặc :ref:`@GlobalScope.ERR_CANT_CONNECT<class_@GlobalScope_constant_ERR_CANT_CONNECT>` nếu không sử dụng thread và :ref:`HTTPClient<class_HTTPClient>` không thể kết nối đến host.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_set_http_proxy:

.. rst-class:: classref-method

|void| **set_http_proxy**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ ) :ref:`🔗<class_HTTPRequest_method_set_http_proxy>`

Đặt proxy server cho các request HTTP.

Proxy server bị bỏ đặt nếu ``host`` rỗng hoặc ``port`` là -1.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_set_https_proxy:

.. rst-class:: classref-method

|void| **set_https_proxy**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ ) :ref:`🔗<class_HTTPRequest_method_set_https_proxy>`

Đặt proxy server cho các request HTTPS.

Proxy server bị bỏ đặt nếu ``host`` rỗng hoặc ``port`` là -1.

.. rst-class:: classref-item-separator

----

.. _class_HTTPRequest_method_set_tls_options:

.. rst-class:: classref-method

|void| **set_tls_options**\ (\ client_options\: :ref:`TLSOptions<class_TLSOptions>`\ ) :ref:`🔗<class_HTTPRequest_method_set_tls_options>`

Đặt :ref:`TLSOptions<class_TLSOptions>` sẽ được sử dụng khi kết nối đến server HTTPS. Xem :ref:`TLSOptions.client()<class_TLSOptions_method_client>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
