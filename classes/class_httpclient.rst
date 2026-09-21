:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/HTTPClient.xml.

.. _class_HTTPClient:

HTTPClient
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Client giao thức truyền siêu văn bản cấp thấp.

.. rst-class:: classref-introduction-group

Mô tả
-----

Client giao thức truyền siêu văn bản (đôi khi được gọi là "User Agent"). Được dùng để thực hiện các HTTP request nhằm tải xuống nội dung web, tải lên tệp và dữ liệu khác hoặc giao tiếp với nhiều dịch vụ khác nhau, cùng các trường hợp sử dụng khác.

Xem node :ref:`HTTPRequest<class_HTTPRequest>` để sử dụng giải pháp ở cấp cao hơn.

\ **Lưu ý:** Client này chỉ cần kết nối với một host một lần (xem :ref:`connect_to_host()<class_HTTPClient_method_connect_to_host>`) để gửi nhiều request. Vì vậy, các method nhận URL thường chỉ nhận phần sau host thay vì toàn bộ URL, vì client đã được kết nối với host. Xem :ref:`request()<class_HTTPClient_method_request>` để xem ví dụ đầy đủ và bắt đầu sử dụng.

Nên tái sử dụng một **HTTPClient** cho nhiều request hoặc để kết nối với các host khác nhau, thay vì tạo một client cho mỗi request. Hỗ trợ Transport Layer Security (TLS), bao gồm xác minh chứng chỉ server. Các HTTP status code trong khoảng 2xx cho biết request thành công, 3xx cho biết chuyển hướng (tức là "thử lại, nhưng ở đây"), 4xx cho biết đã xảy ra lỗi với request và 5xx cho biết đã xảy ra lỗi ở phía server.

Để biết thêm thông tin về HTTP, hãy xem `MDN's documentation on HTTP <https://developer.mozilla.org/en-US/docs/Web/HTTP>`__ (hoặc đọc `RFC 2616 <https://tools.ietf.org/html/rfc2616>`__ để tìm hiểu trực tiếp từ nguồn).

\ **Lưu ý:** Khi export sang Android, hãy bật permission ``INTERNET`` trong Android export preset trước khi export project hoặc sử dụng one-click deploy. Nếu không, Android sẽ chặn mọi loại network communication.

\ **Lưu ý:** Bạn nên sử dụng mã hóa truyền tải (TLS) và tránh gửi thông tin nhạy cảm (chẳng hạn như thông tin đăng nhập) trong các URL parameter của HTTP GET. Thay vào đó, hãy cân nhắc sử dụng HTTP POST request hoặc HTTP header cho những thông tin như vậy.

\ **Lưu ý:** Khi thực hiện HTTP request từ một project được export sang Web, hãy lưu ý rằng remote server có thể không cho phép request từ các origin bên ngoài do `CORS <https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS>`__. Nếu bạn host server đó, hãy sửa backend của server để cho phép request từ các origin bên ngoài bằng cách thêm HTTP header ``Access-Control-Allow-Origin: *``.

\ **Lưu ý:** Hiện tại, hỗ trợ TLS chỉ giới hạn ở TLSv1.2 và TLSv1.3. Việc cố gắng kết nối với server chỉ hỗ trợ các phiên bản TLS cũ hơn (không an toàn) sẽ trả về lỗi.

\ **Cảnh báo:** Hiện tại chưa hỗ trợ thu hồi chứng chỉ TLS và ghim chứng chỉ. Các chứng chỉ đã bị thu hồi vẫn được chấp nhận miễn là chúng vẫn hợp lệ ở các khía cạnh khác. Nếu đây là vấn đề đáng lo ngại, bạn có thể muốn sử dụng các chứng chỉ được quản lý tự động với thời hạn hiệu lực ngắn.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Lớp HTTP client <../tutorials/networking/http_client_class>`

- :doc:`Chứng chỉ TLS <../tutorials/networking/ssl_certificates>`

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`             | :ref:`blocking_mode_enabled<class_HTTPClient_property_blocking_mode_enabled>` | ``false`` |
   +-------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`StreamPeer<class_StreamPeer>` | :ref:`connection<class_HTTPClient_property_connection>`                       |           |
   +-------------------------------------+-------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`               | :ref:`read_chunk_size<class_HTTPClient_property_read_chunk_size>`             | ``65536`` |
   +-------------------------------------+-------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Method
------

.. table::
   :widths: auto

   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`close<class_HTTPClient_method_close>`\ (\ )                                                                                                                                                                                                                   |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`connect_to_host<class_HTTPClient_method_connect_to_host>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>` = -1, tls_options\: :ref:`TLSOptions<class_TLSOptions>` = null\ )                                                              |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_response_body_length<class_HTTPClient_method_get_response_body_length>`\ (\ ) |const|                                                                                                                                                                     |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_response_code<class_HTTPClient_method_get_response_code>`\ (\ ) |const|                                                                                                                                                                                   |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`get_response_headers<class_HTTPClient_method_get_response_headers>`\ (\ )                                                                                                                                                                                     |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>`               | :ref:`get_response_headers_as_dictionary<class_HTTPClient_method_get_response_headers_as_dictionary>`\ (\ )                                                                                                                                                         |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Status<enum_HTTPClient_Status>`             | :ref:`get_status<class_HTTPClient_method_get_status>`\ (\ ) |const|                                                                                                                                                                                                 |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`has_response<class_HTTPClient_method_has_response>`\ (\ ) |const|                                                                                                                                                                                             |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`is_response_chunked<class_HTTPClient_method_is_response_chunked>`\ (\ ) |const|                                                                                                                                                                               |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`poll<class_HTTPClient_method_poll>`\ (\ )                                                                                                                                                                                                                     |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`query_string_from_dict<class_HTTPClient_method_query_string_from_dict>`\ (\ fields\: :ref:`Dictionary<class_Dictionary>`\ )                                                                                                                                   |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`     | :ref:`read_response_body_chunk<class_HTTPClient_method_read_response_body_chunk>`\ (\ )                                                                                                                                                                             |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`request<class_HTTPClient_method_request>`\ (\ method\: :ref:`Method<enum_HTTPClient_Method>`, url\: :ref:`String<class_String>`, headers\: :ref:`PackedStringArray<class_PackedStringArray>`, body\: :ref:`String<class_String>` = ""\ )                      |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`request_raw<class_HTTPClient_method_request_raw>`\ (\ method\: :ref:`Method<enum_HTTPClient_Method>`, url\: :ref:`String<class_String>`, headers\: :ref:`PackedStringArray<class_PackedStringArray>`, body\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_http_proxy<class_HTTPClient_method_set_http_proxy>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ )                                                                                                                               |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_https_proxy<class_HTTPClient_method_set_https_proxy>`\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ )                                                                                                                             |
   +---------------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Enumeration
-----------

.. _enum_HTTPClient_Method:

.. rst-class:: classref-enumeration

enum **Method**: :ref:`🔗<enum_HTTPClient_Method>`

.. _class_HTTPClient_constant_METHOD_GET:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_GET** = ``0``

HTTP GET method. GET method yêu cầu biểu diễn của resource được chỉ định. Các request sử dụng GET chỉ nên truy xuất dữ liệu.

.. _class_HTTPClient_constant_METHOD_HEAD:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_HEAD** = ``1``

HTTP HEAD method. HEAD method yêu cầu một response giống với response của GET request, nhưng không có response body. Điều này hữu ích khi yêu cầu metadata như HTTP header hoặc kiểm tra xem một resource có tồn tại hay không.

.. _class_HTTPClient_constant_METHOD_POST:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_POST** = ``2``

HTTP POST method. POST method được dùng để gửi một entity đến resource được chỉ định, thường làm thay đổi state hoặc gây ra side effect trên server. Method này thường được dùng cho form, gửi dữ liệu hoặc tải lên tệp.

.. _class_HTTPClient_constant_METHOD_PUT:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_PUT** = ``3``

HTTP PUT method. PUT method yêu cầu thay thế tất cả biểu diễn hiện tại của target resource bằng request payload. (Bạn có thể hiểu POST là "tạo hoặc cập nhật" và PUT là "cập nhật", mặc dù nhiều service thường không phân biệt rõ ràng hoặc thay đổi ý nghĩa của chúng).

.. _class_HTTPClient_constant_METHOD_DELETE:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_DELETE** = ``4``

HTTP DELETE method. DELETE method yêu cầu xóa resource được chỉ định.

.. _class_HTTPClient_constant_METHOD_OPTIONS:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_OPTIONS** = ``5``

HTTP OPTIONS method. OPTIONS method yêu cầu mô tả về các tùy chọn giao tiếp của target resource. Hiếm khi được sử dụng.

.. _class_HTTPClient_constant_METHOD_TRACE:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_TRACE** = ``6``

HTTP TRACE method. TRACE method thực hiện kiểm tra loop-back của message dọc theo đường dẫn đến target resource. Trả về toàn bộ HTTP request đã nhận trong response body. Hiếm khi được sử dụng.

.. _class_HTTPClient_constant_METHOD_CONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_CONNECT** = ``7``

HTTP CONNECT method. CONNECT method thiết lập một tunnel đến server được xác định bởi target resource. Hiếm khi được sử dụng.

.. _class_HTTPClient_constant_METHOD_PATCH:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_PATCH** = ``8``

HTTP PATCH method. PATCH method được dùng để áp dụng các sửa đổi một phần cho một resource.

.. _class_HTTPClient_constant_METHOD_MAX:

.. rst-class:: classref-enumeration-constant

:ref:`Method<enum_HTTPClient_Method>` **METHOD_MAX** = ``9``

Đại diện cho kích thước của enum :ref:`Method<enum_HTTPClient_Method>`.

.. rst-class:: classref-item-separator

----

.. _enum_HTTPClient_Status:

.. rst-class:: classref-enumeration

enum **Status**: :ref:`🔗<enum_HTTPClient_Status>`

.. _class_HTTPClient_constant_STATUS_DISCONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_DISCONNECTED** = ``0``

Trạng thái: Đã ngắt kết nối khỏi server.

.. _class_HTTPClient_constant_STATUS_RESOLVING:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_RESOLVING** = ``1``

Trạng thái: Đang phân giải hostname của URL đã cho thành IP.

.. _class_HTTPClient_constant_STATUS_CANT_RESOLVE:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_CANT_RESOLVE** = ``2``

Trạng thái: Lỗi DNS: Không thể phân giải hostname của URL đã cho.

.. _class_HTTPClient_constant_STATUS_CONNECTING:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_CONNECTING** = ``3``

Trạng thái: Đang kết nối với server.

.. _class_HTTPClient_constant_STATUS_CANT_CONNECT:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_CANT_CONNECT** = ``4``

Trạng thái: Không thể kết nối với server.

.. _class_HTTPClient_constant_STATUS_CONNECTED:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_CONNECTED** = ``5``

Trạng thái: Đã thiết lập kết nối.

.. _class_HTTPClient_constant_STATUS_REQUESTING:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_REQUESTING** = ``6``

Trạng thái: Đang gửi request.

.. _class_HTTPClient_constant_STATUS_BODY:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_BODY** = ``7``

Trạng thái: Đã nhận HTTP body.

.. _class_HTTPClient_constant_STATUS_CONNECTION_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_CONNECTION_ERROR** = ``8``

Trạng thái: Lỗi trong kết nối HTTP.

.. _class_HTTPClient_constant_STATUS_TLS_HANDSHAKE_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`Status<enum_HTTPClient_Status>` **STATUS_TLS_HANDSHAKE_ERROR** = ``9``

Trạng thái: Lỗi trong quá trình bắt tay TLS.

.. rst-class:: classref-item-separator

----

.. _enum_HTTPClient_ResponseCode:

.. rst-class:: classref-enumeration

enum **ResponseCode**: :ref:`🔗<enum_HTTPClient_ResponseCode>`

.. _class_HTTPClient_constant_RESPONSE_CONTINUE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_CONTINUE** = ``100``

HTTP status code ``100 Continue``. Response trung gian cho biết mọi thứ cho đến thời điểm hiện tại đều ổn và client nên tiếp tục request (hoặc bỏ qua status này nếu đã hoàn tất).

.. _class_HTTPClient_constant_RESPONSE_SWITCHING_PROTOCOLS:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_SWITCHING_PROTOCOLS** = ``101``

HTTP status code ``101 Switching Protocol``. Được gửi để phản hồi HTTP request header ``Upgrade`` từ client. Cho biết protocol mà server đang chuyển sang.

.. _class_HTTPClient_constant_RESPONSE_PROCESSING:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PROCESSING** = ``102``

HTTP status code ``102 Processing`` (WebDAV). Cho biết server đã nhận và đang xử lý request, nhưng chưa có response nào khả dụng.

.. _class_HTTPClient_constant_RESPONSE_OK:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_OK** = ``200``

HTTP status code ``200 OK``. Request đã thành công. Response mặc định cho các request thành công. Ý nghĩa thay đổi tùy thuộc vào request:

- :ref:`METHOD_GET<class_HTTPClient_constant_METHOD_GET>`: Resource đã được tải xuống và được truyền trong message body.

- :ref:`METHOD_HEAD<class_HTTPClient_constant_METHOD_HEAD>`: Entity header nằm trong message body.

- :ref:`METHOD_POST<class_HTTPClient_constant_METHOD_POST>`: Resource mô tả kết quả của action được truyền trong message body.

- :ref:`METHOD_TRACE<class_HTTPClient_constant_METHOD_TRACE>`: Message body chứa request message như đã được server nhận.

.. _class_HTTPClient_constant_RESPONSE_CREATED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_CREATED** = ``201``

HTTP status code ``201 Created``. Request đã thành công và một resource mới đã được tạo ra do kết quả của request. Đây thường là response được gửi sau một PUT request.

.. _class_HTTPClient_constant_RESPONSE_ACCEPTED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_ACCEPTED** = ``202``

HTTP status code ``202 Accepted``. Request đã được nhận nhưng chưa được xử lý. Đây là response không mang tính cam kết, nghĩa là HTTP không có cách nào để sau đó gửi một asynchronous response cho biết kết quả xử lý request. Response này được dùng trong các trường hợp một process hoặc server khác xử lý request, hoặc khi xử lý theo batch.

.. _class_HTTPClient_constant_RESPONSE_NON_AUTHORITATIVE_INFORMATION:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NON_AUTHORITATIVE_INFORMATION** = ``203``

HTTP status code ``203 Non-Authoritative Information``. Response code này có nghĩa là tập hợp meta-information được trả về không phải là tập hợp chính xác như dữ liệu có trên origin server, mà được thu thập từ một bản sao cục bộ hoặc bản sao của bên thứ ba. Ngoài trường hợp này, nên ưu tiên response 200 OK thay vì response này.

.. _class_HTTPClient_constant_RESPONSE_NO_CONTENT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NO_CONTENT** = ``204``

Mã trạng thái HTTP ``204 No Content``. Không có nội dung nào để gửi cho yêu cầu này, nhưng các header có thể hữu ích. User-agent có thể cập nhật các header được lưu trong cache cho tài nguyên này bằng các header mới.

.. _class_HTTPClient_constant_RESPONSE_RESET_CONTENT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_RESET_CONTENT** = ``205``

Mã trạng thái HTTP ``205 Reset Content``. Server đã hoàn tất yêu cầu và muốn client đặt lại "document view" đã khiến yêu cầu được gửi về trạng thái ban đầu như khi nhận từ origin server.

.. _class_HTTPClient_constant_RESPONSE_PARTIAL_CONTENT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PARTIAL_CONTENT** = ``206``

Mã trạng thái HTTP ``206 Partial Content``. Mã phản hồi này được sử dụng do client đã gửi một range header để chia quá trình download thành nhiều stream.

.. _class_HTTPClient_constant_RESPONSE_MULTI_STATUS:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_MULTI_STATUS** = ``207``

Mã trạng thái HTTP ``207 Multi-Status`` (WebDAV). Phản hồi Multi-Status truyền đạt thông tin về nhiều resource trong các tình huống có thể cần nhiều mã trạng thái.

.. _class_HTTPClient_constant_RESPONSE_ALREADY_REPORTED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_ALREADY_REPORTED** = ``208``

Mã trạng thái HTTP ``208 Already Reported`` (WebDAV). Được sử dụng bên trong phần tử phản hồi DAV: propstat để tránh liệt kê lặp lại các member nội bộ của nhiều binding tới cùng một collection.

.. _class_HTTPClient_constant_RESPONSE_IM_USED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_IM_USED** = ``226``

Mã trạng thái HTTP ``226 IM Used`` (WebDAV). Server đã hoàn tất một yêu cầu GET cho resource và phản hồi là một representation của kết quả từ một hoặc nhiều phép biến đổi instance được áp dụng cho instance hiện tại.

.. _class_HTTPClient_constant_RESPONSE_MULTIPLE_CHOICES:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_MULTIPLE_CHOICES** = ``300``

Mã trạng thái HTTP ``300 Multiple Choice``. Yêu cầu có nhiều phản hồi khả dĩ và không có cách chuẩn hóa nào để chọn một trong các phản hồi đó. User-agent hoặc người dùng phải chọn một phản hồi.

.. _class_HTTPClient_constant_RESPONSE_MOVED_PERMANENTLY:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_MOVED_PERMANENTLY** = ``301``

Mã trạng thái HTTP ``301 Moved Permanently``. Chuyển hướng. Mã phản hồi này có nghĩa là URI của resource được yêu cầu đã thay đổi. URI mới thường được включ trong phản hồi.

.. _class_HTTPClient_constant_RESPONSE_FOUND:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_FOUND** = ``302``

Mã trạng thái HTTP ``302 Found``. Chuyển hướng tạm thời. Mã phản hồi này có nghĩa là URI của resource được yêu cầu đã tạm thời thay đổi. URI có thể tiếp tục được thay đổi trong tương lai. Vì vậy, client nên sử dụng cùng URI này trong các yêu cầu sau đó.

.. _class_HTTPClient_constant_RESPONSE_SEE_OTHER:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_SEE_OTHER** = ``303``

Mã trạng thái HTTP ``303 See Other``. Server đang chuyển hướng user-agent đến một resource khác, như được chỉ ra bởi URI trong trường header Location; URI này nhằm cung cấp một phản hồi gián tiếp cho yêu cầu ban đầu.

.. _class_HTTPClient_constant_RESPONSE_NOT_MODIFIED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NOT_MODIFIED** = ``304``

Mã trạng thái HTTP ``304 Not Modified``. Đã nhận một yêu cầu GET hoặc HEAD có điều kiện và yêu cầu đó sẽ tạo ra phản hồi 200 OK nếu điều kiện không được đánh giá là ``false``.

.. _class_HTTPClient_constant_RESPONSE_USE_PROXY:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_USE_PROXY** = ``305``

**Đã deprecated:** Nhiều client bỏ qua mã phản hồi này vì lý do bảo mật. Mã này cũng đã bị HTTP standard deprecated.

Mã trạng thái HTTP ``305 Use Proxy``.

.. _class_HTTPClient_constant_RESPONSE_SWITCH_PROXY:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_SWITCH_PROXY** = ``306``

**Đã deprecated:** Nhiều client bỏ qua mã phản hồi này vì lý do bảo mật. Mã này cũng đã bị HTTP standard deprecated.

Mã trạng thái HTTP ``306 Switch Proxy``.

.. _class_HTTPClient_constant_RESPONSE_TEMPORARY_REDIRECT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_TEMPORARY_REDIRECT** = ``307``

Mã trạng thái HTTP ``307 Temporary Redirect``. Resource đích tạm thời nằm dưới một URI khác và user-agent MUST NOT thay đổi request method nếu thực hiện chuyển hướng tự động đến URI đó.

.. _class_HTTPClient_constant_RESPONSE_PERMANENT_REDIRECT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PERMANENT_REDIRECT** = ``308``

Mã trạng thái HTTP ``308 Permanent Redirect``. Resource đích đã được gán một URI cố định mới và mọi tham chiếu trong tương lai đến resource này nên sử dụng một trong các URI đi kèm.

.. _class_HTTPClient_constant_RESPONSE_BAD_REQUEST:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_BAD_REQUEST** = ``400``

Mã trạng thái HTTP ``400 Bad Request``. Yêu cầu không hợp lệ. Server không thể hoặc sẽ không xử lý yêu cầu do một vấn đề được xem là lỗi từ phía client (ví dụ: cú pháp yêu cầu không đúng định dạng, framing của request message không hợp lệ, nội dung yêu cầu không hợp lệ hoặc định tuyến yêu cầu mang tính đánh lừa).

.. _class_HTTPClient_constant_RESPONSE_UNAUTHORIZED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_UNAUTHORIZED** = ``401``

Mã trạng thái HTTP ``401 Unauthorized``. Yêu cầu credentials. Yêu cầu chưa được áp dụng vì thiếu credentials xác thực hợp lệ cho resource đích.

.. _class_HTTPClient_constant_RESPONSE_PAYMENT_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PAYMENT_REQUIRED** = ``402``

Mã trạng thái HTTP ``402 Payment Required``. Mã phản hồi này được dành riêng cho việc sử dụng trong tương lai. Mục đích ban đầu khi tạo mã này là sử dụng cho các hệ thống thanh toán kỹ thuật số, tuy nhiên hiện tại mã này chưa được sử dụng.

.. _class_HTTPClient_constant_RESPONSE_FORBIDDEN:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_FORBIDDEN** = ``403``

Mã trạng thái HTTP ``403 Forbidden``. Client không có quyền truy cập nội dung, tức là không được xác thực, nên server từ chối cung cấp phản hồi phù hợp. Không giống ``401``, danh tính của client đã được server biết.

.. _class_HTTPClient_constant_RESPONSE_NOT_FOUND:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NOT_FOUND** = ``404``

Mã trạng thái HTTP ``404 Not Found``. Server không thể tìm thấy resource được yêu cầu. URL không được nhận diện hoặc endpoint hợp lệ nhưng bản thân resource không tồn tại. Cũng có thể được gửi thay cho 403 để che giấu sự tồn tại của resource nếu client không được cấp quyền.

.. _class_HTTPClient_constant_RESPONSE_METHOD_NOT_ALLOWED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_METHOD_NOT_ALLOWED** = ``405``

Mã trạng thái HTTP ``405 Method Not Allowed``. HTTP method của yêu cầu được server nhận biết nhưng đã bị vô hiệu hóa và không thể sử dụng. Ví dụ, một API có thể cấm DELETE một resource. Hai method bắt buộc là GET và HEAD không bao giờ được vô hiệu hóa và không nên trả về mã lỗi này.

.. _class_HTTPClient_constant_RESPONSE_NOT_ACCEPTABLE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NOT_ACCEPTABLE** = ``406``

Mã trạng thái HTTP ``406 Not Acceptable``. Resource đích không có representation hiện tại nào được user-agent chấp nhận, theo các trường header thương lượng chủ động nhận được trong yêu cầu. Được sử dụng khi thương lượng nội dung.

.. _class_HTTPClient_constant_RESPONSE_PROXY_AUTHENTICATION_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PROXY_AUTHENTICATION_REQUIRED** = ``407``

Mã trạng thái HTTP ``407 Proxy Authentication Required``. Tương tự 401 Unauthorized, nhưng cho biết client cần tự xác thực để sử dụng proxy.

.. _class_HTTPClient_constant_RESPONSE_REQUEST_TIMEOUT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_REQUEST_TIMEOUT** = ``408``

Mã trạng thái HTTP ``408 Request Timeout``. Server không nhận được một request message hoàn chỉnh trong khoảng thời gian mà server đã chuẩn bị chờ.

.. _class_HTTPClient_constant_RESPONSE_CONFLICT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_CONFLICT** = ``409``

Mã trạng thái HTTP ``409 Conflict``. Không thể hoàn tất yêu cầu do xung đột với trạng thái hiện tại của resource đích. Mã này được sử dụng trong các tình huống mà người dùng có thể giải quyết xung đột và gửi lại yêu cầu.

.. _class_HTTPClient_constant_RESPONSE_GONE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_GONE** = ``410``

Mã trạng thái HTTP ``410 Gone``. Resource đích không còn khả dụng trên origin server và tình trạng này có khả năng là vĩnh viễn.

.. _class_HTTPClient_constant_RESPONSE_LENGTH_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_LENGTH_REQUIRED** = ``411``

Mã trạng thái HTTP ``411 Length Required``. Server từ chối chấp nhận yêu cầu nếu không có header Content-Length được xác định.

.. _class_HTTPClient_constant_RESPONSE_PRECONDITION_FAILED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PRECONDITION_FAILED** = ``412``

Mã trạng thái HTTP ``412 Precondition Failed``. Một hoặc nhiều điều kiện được cung cấp trong các trường header của yêu cầu được đánh giá là ``false`` khi được kiểm tra trên server.

.. _class_HTTPClient_constant_RESPONSE_REQUEST_ENTITY_TOO_LARGE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_REQUEST_ENTITY_TOO_LARGE** = ``413``

Mã trạng thái HTTP ``413 Entity Too Large``. Server từ chối xử lý yêu cầu vì payload của yêu cầu lớn hơn khả năng hoặc mức server sẵn sàng xử lý.

.. _class_HTTPClient_constant_RESPONSE_REQUEST_URI_TOO_LONG:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_REQUEST_URI_TOO_LONG** = ``414``

Mã trạng thái HTTP ``414 Request-URI Too Long``. Server từ chối phục vụ yêu cầu vì request-target dài hơn mức server sẵn sàng diễn giải.

.. _class_HTTPClient_constant_RESPONSE_UNSUPPORTED_MEDIA_TYPE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_UNSUPPORTED_MEDIA_TYPE** = ``415``

Mã trạng thái HTTP ``415 Unsupported Media Type``. Origin server từ chối phục vụ yêu cầu vì payload có định dạng không được method này hỗ trợ trên resource đích.

.. _class_HTTPClient_constant_RESPONSE_REQUESTED_RANGE_NOT_SATISFIABLE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_REQUESTED_RANGE_NOT_SATISFIABLE** = ``416``

Mã trạng thái HTTP ``416 Requested Range Not Satisfiable``. Không có range nào trong trường Range của yêu cầu chồng lấp với phạm vi hiện tại của resource được chọn, hoặc tập hợp các range được yêu cầu đã bị từ chối do các range không hợp lệ hoặc yêu cầu quá nhiều range nhỏ hay chồng lấp.

.. _class_HTTPClient_constant_RESPONSE_EXPECTATION_FAILED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_EXPECTATION_FAILED** = ``417``

Mã trạng thái HTTP ``417 Expectation Failed``. Expectation được cung cấp trong trường Expect của yêu cầu không thể được đáp ứng bởi ít nhất một inbound server.

.. _class_HTTPClient_constant_RESPONSE_IM_A_TEAPOT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_IM_A_TEAPOT** = ``418``

Mã trạng thái HTTP ``418 I'm A Teapot``. Mọi nỗ lực pha cà phê bằng ấm trà phải dẫn đến mã lỗi "418 I'm a teapot". Phần thân thực thể kết quả CÓ THỂ ngắn và chắc.

.. _class_HTTPClient_constant_RESPONSE_MISDIRECTED_REQUEST:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_MISDIRECTED_REQUEST** = ``421``

Mã trạng thái HTTP ``421 Misdirected Request``. Yêu cầu được gửi đến một server không thể tạo phản hồi. Điều này có thể được gửi bởi một server chưa được cấu hình để tạo phản hồi cho tổ hợp scheme và authority có trong URI yêu cầu.

.. _class_HTTPClient_constant_RESPONSE_UNPROCESSABLE_ENTITY:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_UNPROCESSABLE_ENTITY** = ``422``

Mã trạng thái HTTP ``422 Unprocessable Entity`` (WebDAV). Server hiểu content type của entity yêu cầu (do đó mã trạng thái 415 Unsupported Media Type là không phù hợp), và cú pháp của entity yêu cầu là chính xác (do đó mã trạng thái 400 Bad Request là không phù hợp), nhưng không thể xử lý các chỉ thị chứa trong đó.

.. _class_HTTPClient_constant_RESPONSE_LOCKED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_LOCKED** = ``423``

Mã trạng thái HTTP ``423 Locked`` (WebDAV). Resource nguồn hoặc đích của một method đang bị khóa.

.. _class_HTTPClient_constant_RESPONSE_FAILED_DEPENDENCY:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_FAILED_DEPENDENCY** = ``424``

Mã trạng thái HTTP ``424 Failed Dependency`` (WebDAV). Method không thể được thực hiện trên resource vì hành động được yêu cầu phụ thuộc vào một hành động khác và hành động đó đã thất bại.

.. _class_HTTPClient_constant_RESPONSE_UPGRADE_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_UPGRADE_REQUIRED** = ``426``

Mã trạng thái HTTP ``426 Upgrade Required``. Server từ chối thực hiện yêu cầu bằng protocol hiện tại nhưng có thể sẵn sàng thực hiện sau khi client nâng cấp lên một protocol khác.

.. _class_HTTPClient_constant_RESPONSE_PRECONDITION_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_PRECONDITION_REQUIRED** = ``428``

Mã trạng thái HTTP ``428 Precondition Required``. Origin server yêu cầu yêu cầu phải có điều kiện.

.. _class_HTTPClient_constant_RESPONSE_TOO_MANY_REQUESTS:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_TOO_MANY_REQUESTS** = ``429``

Mã trạng thái HTTP ``429 Too Many Requests``. Người dùng đã gửi quá nhiều yêu cầu trong một khoảng thời gian nhất định (xem "rate limiting"). Hãy giảm tốc độ và tăng khoảng thời gian giữa các yêu cầu, hoặc thử lại sau.

.. _class_HTTPClient_constant_RESPONSE_REQUEST_HEADER_FIELDS_TOO_LARGE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_REQUEST_HEADER_FIELDS_TOO_LARGE** = ``431``

Mã trạng thái HTTP ``431 Request Header Fields Too Large``. Server không muốn xử lý yêu cầu vì các header field của yêu cầu quá lớn. Yêu cầu CÓ THỂ được gửi lại sau khi giảm kích thước các header field của yêu cầu.

.. _class_HTTPClient_constant_RESPONSE_UNAVAILABLE_FOR_LEGAL_REASONS:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_UNAVAILABLE_FOR_LEGAL_REASONS** = ``451``

Mã trạng thái HTTP ``451 Response Unavailable For Legal Reasons``. Server từ chối quyền truy cập vào resource do một yêu cầu pháp lý.

.. _class_HTTPClient_constant_RESPONSE_INTERNAL_SERVER_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_INTERNAL_SERVER_ERROR** = ``500``

Mã trạng thái HTTP ``500 Internal Server Error``. Server gặp một điều kiện không mong đợi khiến server không thể hoàn tất yêu cầu.

.. _class_HTTPClient_constant_RESPONSE_NOT_IMPLEMENTED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NOT_IMPLEMENTED** = ``501``

Mã trạng thái HTTP ``501 Not Implemented``. Server không hỗ trợ chức năng cần thiết để hoàn tất yêu cầu.

.. _class_HTTPClient_constant_RESPONSE_BAD_GATEWAY:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_BAD_GATEWAY** = ``502``

Mã trạng thái HTTP ``502 Bad Gateway``. Khi hoạt động với vai trò gateway hoặc proxy, server nhận được phản hồi không hợp lệ từ inbound server mà server đã truy cập trong khi cố gắng hoàn tất yêu cầu. Thường được trả về bởi load balancer hoặc proxy.

.. _class_HTTPClient_constant_RESPONSE_SERVICE_UNAVAILABLE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_SERVICE_UNAVAILABLE** = ``503``

Mã trạng thái HTTP ``503 Service Unavailable``. Server hiện không thể xử lý yêu cầu do quá tải tạm thời hoặc đang bảo trì theo lịch, tình trạng này có thể sẽ giảm bớt sau một khoảng thời gian. Hãy thử lại sau.

.. _class_HTTPClient_constant_RESPONSE_GATEWAY_TIMEOUT:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_GATEWAY_TIMEOUT** = ``504``

Mã trạng thái HTTP ``504 Gateway Timeout``. Khi hoạt động với vai trò gateway hoặc proxy, server không nhận được phản hồi kịp thời từ upstream server mà server cần truy cập để hoàn tất yêu cầu. Thường được trả về bởi load balancer hoặc proxy.

.. _class_HTTPClient_constant_RESPONSE_HTTP_VERSION_NOT_SUPPORTED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_HTTP_VERSION_NOT_SUPPORTED** = ``505``

Mã trạng thái HTTP ``505 HTTP Version Not Supported``. Server không hỗ trợ hoặc từ chối hỗ trợ major version của HTTP được sử dụng trong message yêu cầu.

.. _class_HTTPClient_constant_RESPONSE_VARIANT_ALSO_NEGOTIATES:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_VARIANT_ALSO_NEGOTIATES** = ``506``

Mã trạng thái HTTP ``506 Variant Also Negotiates``. Server gặp lỗi cấu hình nội bộ: resource variant được chọn được cấu hình để tự thực hiện transparent content negotiation, do đó không phải là endpoint thích hợp trong quy trình negotiation.

.. _class_HTTPClient_constant_RESPONSE_INSUFFICIENT_STORAGE:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_INSUFFICIENT_STORAGE** = ``507``

HTTP status code ``507 Insufficient Storage``. The method could not be performed on the resource because the server is unable to store the representation needed to successfully complete the request.

.. _class_HTTPClient_constant_RESPONSE_LOOP_DETECTED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_LOOP_DETECTED** = ``508``

Mã trạng thái HTTP ``508 Loop Detected``. Server đã chấm dứt một operation vì phát hiện vòng lặp vô hạn khi xử lý yêu cầu có "Depth: infinity". Trạng thái này cho biết toàn bộ operation đã thất bại.

.. _class_HTTPClient_constant_RESPONSE_NOT_EXTENDED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NOT_EXTENDED** = ``510``

Mã trạng thái HTTP ``510 Not Extended``. Policy truy cập resource chưa được đáp ứng trong yêu cầu. Server nên gửi lại toàn bộ thông tin cần thiết để client tạo một yêu cầu mở rộng.

.. _class_HTTPClient_constant_RESPONSE_NETWORK_AUTH_REQUIRED:

.. rst-class:: classref-enumeration-constant

:ref:`ResponseCode<enum_HTTPClient_ResponseCode>` **RESPONSE_NETWORK_AUTH_REQUIRED** = ``511``

Mã trạng thái HTTP ``511 Network Authentication Required``. Client cần xác thực để có quyền truy cập mạng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Property
--------------

.. _class_HTTPClient_property_blocking_mode_enabled:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **blocking_mode_enabled** = ``false`` :ref:`🔗<class_HTTPClient_property_blocking_mode_enabled>`

.. rst-class:: classref-property-setget

- |void| **set_blocking_mode**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_blocking_mode_enabled**\ (\ )

Nếu ``true``, execution sẽ bị block cho đến khi toàn bộ dữ liệu được đọc từ response.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_property_connection:

.. rst-class:: classref-property

:ref:`StreamPeer<class_StreamPeer>` **connection** :ref:`🔗<class_HTTPClient_property_connection>`

.. rst-class:: classref-property-setget

- |void| **set_connection**\ (\ value\: :ref:`StreamPeer<class_StreamPeer>`\ ) - :ref:`StreamPeer<class_StreamPeer>` **get_connection**\ (\ )

Connection được sử dụng cho client này.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_property_read_chunk_size:

.. rst-class:: classref-property

:ref:`int<class_int>` **read_chunk_size** = ``65536`` :ref:`🔗<class_HTTPClient_property_read_chunk_size>`

.. rst-class:: classref-property-setget

- |void| **set_read_chunk_size**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_read_chunk_size**\ (\ )

Kích thước buffer được sử dụng và số byte tối đa cần đọc trong mỗi iteration. Xem :ref:`read_response_body_chunk()<class_HTTPClient_method_read_response_body_chunk>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả Method
------------

.. _class_HTTPClient_method_close:

.. rst-class:: classref-method

|void| **close**\ (\ ) :ref:`🔗<class_HTTPClient_method_close>`

Đóng connection hiện tại, cho phép tái sử dụng **HTTPClient** này.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_connect_to_host:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **connect_to_host**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>` = -1, tls_options\: :ref:`TLSOptions<class_TLSOptions>` = null\ ) :ref:`🔗<class_HTTPClient_method_connect_to_host>`

Kết nối đến một host. Việc này phải được thực hiện trước khi gửi bất kỳ yêu cầu nào.

Nếu không chỉ định ``port`` (hoặc sử dụng ``-1``), giá trị này sẽ tự động được đặt thành 80 cho HTTP và 443 cho HTTPS. Bạn có thể truyền tham số tùy chọn ``tls_options`` để tùy chỉnh các certification authority được tin cậy hoặc việc xác minh common name khi sử dụng HTTPS. Xem :ref:`TLSOptions.client()<class_TLSOptions_method_client>` và :ref:`TLSOptions.client_unsafe()<class_TLSOptions_method_client_unsafe>`.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_get_response_body_length:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_response_body_length**\ (\ ) |const| :ref:`🔗<class_HTTPClient_method_get_response_body_length>`

Trả về độ dài body của response.

\ **Lưu ý:** Một số Web server có thể không gửi độ dài body. Trong trường hợp này, giá trị được trả về sẽ là ``-1``. Nếu sử dụng chunked transfer encoding, độ dài body cũng sẽ là ``-1``.

\ **Lưu ý:** Hàm này luôn trả về ``-1`` trên Web platform do các hạn chế của trình duyệt.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_get_response_code:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_response_code**\ (\ ) |const| :ref:`🔗<class_HTTPClient_method_get_response_code>`

Trả về HTTP status code của response.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_get_response_headers:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_response_headers**\ (\ ) :ref:`🔗<class_HTTPClient_method_get_response_headers>`

Trả về các header của response.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_get_response_headers_as_dictionary:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **get_response_headers_as_dictionary**\ (\ ) :ref:`🔗<class_HTTPClient_method_get_response_headers_as_dictionary>`

Trả về tất cả header của response dưới dạng một :ref:`Dictionary<class_Dictionary>`. Mỗi entry gồm tên header và một :ref:`String<class_String>` chứa các giá trị được phân tách bằng ``"; "``. Kiểu chữ được giữ nguyên như khi nhận các header.

::

    {
        "content-length": 12,
        "Content-Type": "application/json; charset=UTF-8",
    }

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_get_status:

.. rst-class:: classref-method

:ref:`Status<enum_HTTPClient_Status>` **get_status**\ (\ ) |const| :ref:`🔗<class_HTTPClient_method_get_status>`

Trả về một constant :ref:`Status<enum_HTTPClient_Status>`. Cần gọi :ref:`poll()<class_HTTPClient_method_poll>` để nhận các cập nhật trạng thái.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_has_response:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **has_response**\ (\ ) |const| :ref:`🔗<class_HTTPClient_method_has_response>`

Nếu ``true``, **HTTPClient** này có một response khả dụng.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_is_response_chunked:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_response_chunked**\ (\ ) |const| :ref:`🔗<class_HTTPClient_method_is_response_chunked>`

Nếu ``true``, **HTTPClient** này có một response được chia thành các chunk.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_poll:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **poll**\ (\ ) :ref:`🔗<class_HTTPClient_method_poll>`

Điều này cần được gọi để bất kỳ request nào cũng được xử lý. Kiểm tra kết quả bằng :ref:`get_status()<class_HTTPClient_method_get_status>`.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_query_string_from_dict:

.. rst-class:: classref-method

:ref:`String<class_String>` **query_string_from_dict**\ (\ fields\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_HTTPClient_method_query_string_from_dict>`

Tạo một query string theo kiểu application/x-www-form-urlencoded cho GET/POST từ một dictionary được cung cấp, ví dụ:


.. tabs::

 .. code-tab:: gdscript

    var fields = { "username": "user", "password": "pass" }
    var query_string = http_client.query_string_from_dict(fields)
    # Trả về "username=user&password=pass"

 .. code-tab:: csharp

    var fields = new Godot.Collections.Dictionary { { "username", "user" }, { "password", "pass" } };
    string queryString = httpClient.QueryStringFromDict(fields);
    // Trả về "username=user&password=pass"



Ngoài ra, nếu một key có giá trị ``null``, chỉ bản thân key được thêm vào, không có dấu bằng và value. Nếu value là một array, một cặp có cùng key sẽ được thêm vào cho mỗi value trong đó.


.. tabs::

 .. code-tab:: gdscript

    var fields = { "single": 123, "not_valued": null, "multiple": [22, 33, 44] }
    var query_string = http_client.query_string_from_dict(fields)
    # Trả về "single=123&not_valued&multiple=22&multiple=33&multiple=44"

 .. code-tab:: csharp

    var fields = new Godot.Collections.Dictionary
    {
        { "single", 123 },
        { "notValued", default },
        { "multiple", new Godot.Collections.Array { 22, 33, 44 } },
    };
    string queryString = httpClient.QueryStringFromDict(fields);
    // Trả về "single=123&not_valued&multiple=22&multiple=33&multiple=44"



.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_read_response_body_chunk:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **read_response_body_chunk**\ (\ ) :ref:`🔗<class_HTTPClient_method_read_response_body_chunk>`

Đọc một chunk từ response.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_request:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **request**\ (\ method\: :ref:`Method<enum_HTTPClient_Method>`, url\: :ref:`String<class_String>`, headers\: :ref:`PackedStringArray<class_PackedStringArray>`, body\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_HTTPClient_method_request>`

Gửi một HTTP request đến host đã kết nối với ``method`` được cung cấp.

Tham số URL thường chỉ là phần nằm sau host, vì vậy đối với ``https://example.com/index.php``, nó là ``/index.php``. Khi gửi request đến HTTP proxy server, tham số này phải là một absolute URL. Đối với request :ref:`METHOD_OPTIONS<class_HTTPClient_constant_METHOD_OPTIONS>`, ``*`` cũng được cho phép. Đối với request :ref:`METHOD_CONNECT<class_HTTPClient_constant_METHOD_CONNECT>`, tham số này phải là authority component (``host:port``).

\ ``headers`` là các HTTP request header.

Để tạo một POST request có query string nhằm gửi dữ liệu lên server, hãy thực hiện:


.. tabs::

 .. code-tab:: gdscript

    var fields = { "username": "user", "password": "pass" }
    var query_string = http_client.query_string_from_dict(fields)
    var headers = ["Content-Type: application/x-www-form-urlencoded", "Content-Length: " + str(query_string.length())]
    var result = http_client.request(http_client.METHOD_POST, "/index.php", headers, query_string)

 .. code-tab:: csharp

    var fields = new Godot.Collections.Dictionary { { "username", "user" }, { "password", "pass" } };
    string queryString = new HttpClient().QueryStringFromDict(fields);
    string[] headers = ["Content-Type: application/x-www-form-urlencoded", $"Content-Length: {queryString.Length}"];
    var result = new HttpClient().Request(HttpClient.Method.Post, "index.php", headers, queryString);



\ **Lưu ý:** Tham số ``body`` bị bỏ qua nếu ``method`` là :ref:`METHOD_GET<class_HTTPClient_constant_METHOD_GET>`. Điều này là do các method GET không thể chứa request data. Cách khắc phục là truyền request data dưới dạng query string trong URL. Xem :ref:`String.uri_encode()<class_String_method_uri_encode>` để biết ví dụ.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_request_raw:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **request_raw**\ (\ method\: :ref:`Method<enum_HTTPClient_Method>`, url\: :ref:`String<class_String>`, headers\: :ref:`PackedStringArray<class_PackedStringArray>`, body\: :ref:`PackedByteArray<class_PackedByteArray>`\ ) :ref:`🔗<class_HTTPClient_method_request_raw>`

Gửi một HTTP request thô đến host đã kết nối với ``method`` được cung cấp.

Tham số URL thường chỉ là phần nằm sau host, vì vậy đối với ``https://example.com/index.php``, nó là ``/index.php``. Khi gửi request đến HTTP proxy server, tham số này phải là một absolute URL. Đối với request :ref:`METHOD_OPTIONS<class_HTTPClient_constant_METHOD_OPTIONS>`, ``*`` cũng được cho phép. Đối với request :ref:`METHOD_CONNECT<class_HTTPClient_constant_METHOD_CONNECT>`, tham số này phải là authority component (``host:port``).

\ ``headers`` là các HTTP request header.

Gửi body data ở dạng raw, dưới dạng một byte array và không encode theo bất kỳ cách nào.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_set_http_proxy:

.. rst-class:: classref-method

|void| **set_http_proxy**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ ) :ref:`🔗<class_HTTPClient_method_set_http_proxy>`

Thiết lập proxy server cho các HTTP request.

Proxy server sẽ được unset nếu ``host`` rỗng hoặc ``port`` là -1.

.. rst-class:: classref-item-separator

----

.. _class_HTTPClient_method_set_https_proxy:

.. rst-class:: classref-method

|void| **set_https_proxy**\ (\ host\: :ref:`String<class_String>`, port\: :ref:`int<class_int>`\ ) :ref:`🔗<class_HTTPClient_method_set_https_proxy>`

Thiết lập proxy server cho các HTTPS request.

Proxy server sẽ được unset nếu ``host`` rỗng hoặc ``port`` là -1.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
