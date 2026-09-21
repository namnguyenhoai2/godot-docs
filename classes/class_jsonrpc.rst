:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/JSONRPC.xml.

.. _class_JSONRPC:

JSONRPC
=======

**Kế thừa:** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`GDScriptLanguageProtocol<class_GDScriptLanguageProtocol>`

Một helper để xử lý các dictionary có dạng như tài liệu JSONRPC.

.. rst-class:: classref-introduction-group

Mô tả
-----

`JSON-RPC <https://www.jsonrpc.org/>`__ là một tiêu chuẩn bọc một lời gọi phương thức trong một đối tượng :ref:`JSON<class_JSON>`. Đối tượng này có một cấu trúc cụ thể và xác định phương thức nào được gọi, các tham số truyền cho hàm đó, đồng thời mang theo một ID để theo dõi các phản hồi. Class này triển khai tiêu chuẩn đó trên :ref:`Dictionary<class_Dictionary>`; bạn sẽ phải chuyển đổi giữa :ref:`Dictionary<class_Dictionary>` và :ref:`JSON<class_JSON>` bằng các hàm khác.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`make_notification<class_JSONRPC_method_make_notification>`\ (\ method\: :ref:`String<class_String>`, params\: :ref:`Variant<class_Variant>`\ )                                               |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`make_request<class_JSONRPC_method_make_request>`\ (\ method\: :ref:`String<class_String>`, params\: :ref:`Variant<class_Variant>`, id\: :ref:`Variant<class_Variant>`\ )                     |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`make_response<class_JSONRPC_method_make_response>`\ (\ result\: :ref:`Variant<class_Variant>`, id\: :ref:`Variant<class_Variant>`\ )                                                         |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Dictionary<class_Dictionary>` | :ref:`make_response_error<class_JSONRPC_method_make_response_error>`\ (\ code\: :ref:`int<class_int>`, message\: :ref:`String<class_String>`, id\: :ref:`Variant<class_Variant>` = null\ ) |const| |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`       | :ref:`process_action<class_JSONRPC_method_process_action>`\ (\ action\: :ref:`Variant<class_Variant>`, recurse\: :ref:`bool<class_bool>` = false\ )                                                |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`         | :ref:`process_string<class_JSONRPC_method_process_string>`\ (\ action\: :ref:`String<class_String>`\ )                                                                                             |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                              | :ref:`set_method<class_JSONRPC_method_set_method>`\ (\ name\: :ref:`String<class_String>`, callback\: :ref:`Callable<class_Callable>`\ )                                                           |
   +-------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_JSONRPC_ErrorCode:

.. rst-class:: classref-enumeration

enum **ErrorCode**: :ref:`🔗<enum_JSONRPC_ErrorCode>`

.. _class_JSONRPC_constant_PARSE_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorCode<enum_JSONRPC_ErrorCode>` **PARSE_ERROR** = ``-32700``

Yêu cầu không thể được phân tích cú pháp vì không hợp lệ theo tiêu chuẩn JSON (:ref:`JSON.parse()<class_JSON_method_parse>` failed).

.. _class_JSONRPC_constant_INVALID_REQUEST:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorCode<enum_JSONRPC_ErrorCode>` **INVALID_REQUEST** = ``-32600``

Một lời gọi phương thức đã được yêu cầu, nhưng định dạng của yêu cầu không hợp lệ.

.. _class_JSONRPC_constant_METHOD_NOT_FOUND:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorCode<enum_JSONRPC_ErrorCode>` **METHOD_NOT_FOUND** = ``-32601``

Một lời gọi phương thức đã được yêu cầu, nhưng không có hàm nào mang tên đó trong subclass JSONRPC.

.. _class_JSONRPC_constant_INVALID_PARAMS:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorCode<enum_JSONRPC_ErrorCode>` **INVALID_PARAMS** = ``-32602``

Một lời gọi phương thức đã được yêu cầu, nhưng các tham số phương thức được cung cấp không hợp lệ. Không được JSONRPC tích hợp sẵn sử dụng.

.. _class_JSONRPC_constant_INTERNAL_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`ErrorCode<enum_JSONRPC_ErrorCode>` **INTERNAL_ERROR** = ``-32603``

Đã xảy ra lỗi nội bộ trong khi xử lý yêu cầu. Không được JSONRPC tích hợp sẵn sử dụng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_JSONRPC_method_make_notification:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **make_notification**\ (\ method\: :ref:`String<class_String>`, params\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_JSONRPC_method_make_notification>`

Trả về một dictionary có dạng notification JSON-RPC. Notification là các thông báo chỉ được gửi một lần và không chờ phản hồi.

- ``method``: Tên của phương thức đang được gọi.

- ``params``: Một array hoặc dictionary chứa các tham số được truyền cho phương thức.

.. rst-class:: classref-item-separator

----

.. _class_JSONRPC_method_make_request:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **make_request**\ (\ method\: :ref:`String<class_String>`, params\: :ref:`Variant<class_Variant>`, id\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_JSONRPC_method_make_request>`

Trả về một dictionary có dạng request JSON-RPC. Request được gửi đến server với kỳ vọng nhận được phản hồi. Trường ID được server sử dụng để chỉ định chính xác request nào mà server đang phản hồi.

- ``method``: Tên của phương thức đang được gọi.

- ``params``: Một array hoặc dictionary chứa các tham số được truyền cho phương thức.

- ``id``: Xác định duy nhất request này. Server được kỳ vọng sẽ gửi phản hồi có cùng ID.

.. rst-class:: classref-item-separator

----

.. _class_JSONRPC_method_make_response:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **make_response**\ (\ result\: :ref:`Variant<class_Variant>`, id\: :ref:`Variant<class_Variant>`\ ) :ref:`🔗<class_JSONRPC_method_make_response>`

Khi server đã nhận và xử lý một request, server được kỳ vọng sẽ gửi phản hồi. Nếu bạn không muốn nhận phản hồi, bạn cần gửi Notification thay thế.

- ``result``: Giá trị trả về của hàm đã được gọi.

- ``id``: ID của request mà phản hồi này hướng đến.

.. rst-class:: classref-item-separator

----

.. _class_JSONRPC_method_make_response_error:

.. rst-class:: classref-method

:ref:`Dictionary<class_Dictionary>` **make_response_error**\ (\ code\: :ref:`int<class_int>`, message\: :ref:`String<class_String>`, id\: :ref:`Variant<class_Variant>` = null\ ) |const| :ref:`🔗<class_JSONRPC_method_make_response_error>`

Tạo một phản hồi cho biết một phản hồi trước đó đã thất bại theo một cách nào đó.

- ``code``: Mã lỗi tương ứng với loại lỗi này. Xem các hằng số :ref:`ErrorCode<enum_JSONRPC_ErrorCode>`.

- ``message``: Một thông báo tùy chỉnh về lỗi này.

- ``id``: Request mà lỗi này là phản hồi.

.. rst-class:: classref-item-separator

----

.. _class_JSONRPC_method_process_action:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **process_action**\ (\ action\: :ref:`Variant<class_Variant>`, recurse\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_JSONRPC_method_process_action>`

Với một Dictionary có dạng request JSON-RPC: giải nén request và chạy nó. Các phương thức được phân giải bằng cách xem trường có tên "method" và tìm một hàm có tên tương ứng trong đối tượng JSONRPC. Nếu tìm thấy, phương thức đó sẽ được gọi.

Để thêm các phương thức được hỗ trợ mới, hãy mở rộng class JSONRPC và gọi :ref:`process_action()<class_JSONRPC_method_process_action>` trên subclass của bạn.

\ ``action``: Action sẽ được chạy, dưới dạng một Dictionary có dạng request hoặc notification JSON-RPC.

.. rst-class:: classref-item-separator

----

.. _class_JSONRPC_method_process_string:

.. rst-class:: classref-method

:ref:`String<class_String>` **process_string**\ (\ action\: :ref:`String<class_String>`\ ) :ref:`🔗<class_JSONRPC_method_process_string>`

.. container:: contribute

	Hiện chưa có mô tả cho phương thức này. Hãy giúp chúng tôi bằng cách `contributing one <https://contributing.godotengine.org/en/latest/documentation/class_reference.html>`__!

.. rst-class:: classref-item-separator

----

.. _class_JSONRPC_method_set_method:

.. rst-class:: classref-method

|void| **set_method**\ (\ name\: :ref:`String<class_String>`, callback\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_JSONRPC_method_set_method>`

Đăng ký một callback cho tên phương thức đã cho.

- ``name``: Tên mà client có thể sử dụng để truy cập callback.

- ``callback``: Callback sẽ xử lý phương thức được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
