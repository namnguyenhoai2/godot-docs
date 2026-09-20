:article_outdated: True

.. _doc_http_client_class:

lớp HTTP client
===============

:ref:`HTTPClient <class_HTTPClient>` provides low-level access to HTTP communication.
Đối với một interface cấp cao hơn, trước tiên bạn có thể xem :ref:`HTTPRequest <class_HTTPRequest>`, trong đó có sẵn một tutorial :ref:`here <doc_http_request_class>`.

.. warning::

    Khi export sang Android, hãy đảm bảo bật permission ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi loại giao tiếp mạng.

Sau đây là ví dụ về cách sử dụng lớp :ref:`HTTPClient <class_HTTPClient>`. Đây chỉ là một script, vì vậy bạn có thể chạy bằng cách thực thi:

.. tabs::

 .. code-tab:: console GDScript

    c:\godot> godot -s http_test.gd

 .. code-tab:: console C#

    c:\godot> godot -s HTTPTest.cs

Nó sẽ kết nối và tải một website.

.. tabs::

 .. code-tab:: gdscript GDScript

    extends SceneTree

    # Bản demo HTTPClient
    # Lớp đơn giản này có thể thực hiện các HTTP request; nó không block, nhưng cần được poll.

    func _init():
        var err = 0
        var http = HTTPClient.new() # Tạo Client.

        err = http.connect_to_host("www.php.net", 80) # Kết nối đến host/port.
        assert(err == OK) # Đảm bảo kết nối OK.

        # Chờ cho đến khi được phân giải và kết nối.
        while http.get_status() == HTTPClient.STATUS_CONNECTING or http.get_status() == HTTPClient.STATUS_RESOLVING:
            http.poll()
            print("Connecting...")
            await get_tree().process_frame

        assert(http.get_status() == HTTPClient.STATUS_CONNECTED) # Kiểm tra xem kết nối có được thiết lập thành công hay không.

        # Một số header
        var headers = [
            "User-Agent: Pirulo/1.0 (Godot)",
            "Accept: */*"
        ]

        err = http.request(HTTPClient.METHOD_GET, "/ChangeLog-5.php", headers) # Yêu cầu một trang từ site (trang này được chia thành các chunk..)
        assert(err == OK) # Đảm bảo mọi thứ đều OK.

        while http.get_status() == HTTPClient.STATUS_REQUESTING:
            # Tiếp tục poll trong suốt thời gian request đang được xử lý.
            http.poll()
            print("Requesting...")
            await get_tree().process_frame

        assert(http.get_status() == HTTPClient.STATUS_BODY or http.get_status() == HTTPClient.STATUS_CONNECTED) # Đảm bảo request đã hoàn tất thành công.

        print("response? ", http.has_response()) # Site có thể không có response.

        if http.has_response():
            # Nếu có response...

            headers = http.get_response_headers_as_dictionary() # Lấy các response header.
            print("code: ", http.get_response_code()) # Hiển thị response code.
            print("**headers:\\n", headers) # Hiển thị các header.

            # Lấy HTTP Body

            if http.is_response_chunked():
                # Nó có sử dụng chunk không?
                print("Response is Chunked!")
            else:
                # Hay chỉ sử dụng Content-Length
                var bl = http.get_response_body_length()
                print("Response Length: ", bl)

            # Dù thế nào thì method này cũng hoạt động cho cả hai trường hợp

            var rb = PackedByteArray() # Mảng sẽ chứa dữ liệu.

            while http.get_status() == HTTPClient.STATUS_BODY:
                # Trong khi vẫn còn body chưa được đọc
                http.poll()
                # Lấy một chunk.
                var chunk = http.read_response_body_chunk()
                if chunk.size() == 0:
                    await get_tree().process_frame
                else:
                    rb = rb + chunk # Thêm vào read buffer.
            # Hoàn tất!

            print("bytes got: ", rb.size())
            var text = rb.get_string_from_ascii()
            print("Text: ", text)

        quit()

 .. code-tab:: csharp

    using Godot;

    public partial class HTTPTest : SceneTree
    {
        // Bản demo HTTPClient.
        // Lớp đơn giản này có thể thực hiện các HTTP request; nó không block, nhưng cần được poll.
        public override async void _Initialize()
        {
            Error err;
            HTTPClient http = new HTTPClient(); // Tạo client.

            err = http.ConnectToHost("www.php.net", 80); // Kết nối đến host/port.
            Debug.Assert(err == Error.Ok); // Đảm bảo kết nối OK.

            // Chờ cho đến khi được phân giải và kết nối.
            while (http.GetStatus() == HTTPClient.Status.Connecting || http.GetStatus() == HTTPClient.Status.Resolving)
            {
                http.Poll();
                GD.Print("Connecting...");
                OS.DelayMsec(500);
            }

            Debug.Assert(http.GetStatus() == HTTPClient.Status.Connected); // Kiểm tra xem kết nối có được thiết lập thành công hay không.

            // Một số header.
            string[] headers =
            [
                "User-Agent: Pirulo/1.0 (Godot)",
                "Accept: */*",
            ];

            err = http.Request(HTTPClient.Method.Get, "/ChangeLog-5.php", headers); // Yêu cầu một trang từ site.
            Debug.Assert(err == Error.Ok); // Đảm bảo mọi thứ đều OK.

            // Tiếp tục poll trong suốt thời gian request đang được xử lý.
            while (http.GetStatus() == HTTPClient.Status.Requesting)
            {
                http.Poll();
                GD.Print("Requesting...");
                if (OS.HasFeature("web"))
                {
                    // HTTP request đồng bộ không được hỗ trợ trên web,
                    // vì vậy hãy chờ đến lần lặp main loop tiếp theo.
                    await ToSignal(Engine.GetMainLoop(), "idle_frame");
                }
                else
                {
                    OS.DelayMsec(500);
                }
            }

            Debug.Assert(http.GetStatus() == HTTPClient.Status.Body || http.GetStatus() == HTTPClient.Status.Connected); // Đảm bảo request đã hoàn tất thành công.

            GD.Print("Response? ", http.HasResponse()); // Site có thể không có response.

            // Nếu có response...
            if (http.HasResponse())
            {
                headers = http.GetResponseHeaders(); // Lấy các response header.
                GD.Print("Code: ", http.GetResponseCode()); // Hiển thị response code.
                GD.Print("Headers:");
                foreach (string header in headers)
                {
                    // Hiển thị các header.
                    GD.Print(header);
                }

                if (http.IsResponseChunked())
                {
                    // Nó có sử dụng chunk không?
                    GD.Print("Response is Chunked!");
                }
                else
                {
                    // Hay chỉ sử dụng Content-Length.
                    GD.Print("Response Length: ", http.GetResponseBodyLength());
                }

                // Dù thế nào thì method này cũng hoạt động cho cả hai trường hợp.
                List<byte> rb = new List<byte>(); // List sẽ chứa dữ liệu.

                // Trong khi vẫn còn dữ liệu chưa được đọc...
                while (http.GetStatus() == HTTPClient.Status.Body)
                {
                    http.Poll();
                    byte[] chunk = http.ReadResponseBodyChunk(); // Đọc một chunk.
                    if (chunk.Length == 0)
                    {
                        // Nếu không đọc được gì, hãy chờ buffer đầy.
                        OS.DelayMsec(500);
                    }
                    else
                    {
                        // Thêm chunk vào read buffer.
                        rb.AddRange(chunk);
                    }
                }

                // Hoàn tất!
                GD.Print("Bytes Downloaded: ", rb.Count);
                string text = Encoding.ASCII.GetString(rb.ToArray());
                GD.Print(text);
            }
            Quit();
        }
    }
