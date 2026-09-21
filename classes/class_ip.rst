:github_url: hide

.. meta::
	:keywords: dns

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ các mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/IP.xml.

.. _class_IP:

IP ==

**Kế thừa:** :ref:`Object<class_Object>`

Các hàm hỗ trợ giao thức Internet (IP), chẳng hạn như phân giải DNS.

.. rst-class:: classref-introduction-group

Mô tả
-----

IP chứa các hàm hỗ trợ cho Internet Protocol (IP). Hỗ trợ TCP/IP nằm trong các class khác (xem :ref:`StreamPeerTCP<class_StreamPeerTCP>` và :ref:`TCPServer<class_TCPServer>`). IP cung cấp hỗ trợ phân giải hostname DNS, cả dạng blocking và dạng threaded.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`clear_cache<class_IP_method_clear_cache>`\ (\ hostname\: :ref:`String<class_String>` = ""\ )                                                                 |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`erase_resolve_item<class_IP_method_erase_resolve_item>`\ (\ id\: :ref:`int<class_int>`\ )                                                                    |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`get_local_addresses<class_IP_method_get_local_addresses>`\ (\ ) |const|                                                                                      |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] | :ref:`get_local_interfaces<class_IP_method_get_local_interfaces>`\ (\ ) |const|                                                                                    |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`get_resolve_item_address<class_IP_method_get_resolve_item_address>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                                        | :ref:`get_resolve_item_addresses<class_IP_method_get_resolve_item_addresses>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                            |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`ResolverStatus<enum_IP_ResolverStatus>`                    | :ref:`get_resolve_item_status<class_IP_method_get_resolve_item_status>`\ (\ id\: :ref:`int<class_int>`\ ) |const|                                                  |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                                      | :ref:`resolve_hostname<class_IP_method_resolve_hostname>`\ (\ host\: :ref:`String<class_String>`, ip_type\: :ref:`Type<enum_IP_Type>` = 3\ )                       |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>`                | :ref:`resolve_hostname_addresses<class_IP_method_resolve_hostname_addresses>`\ (\ host\: :ref:`String<class_String>`, ip_type\: :ref:`Type<enum_IP_Type>` = 3\ )   |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`resolve_hostname_queue_item<class_IP_method_resolve_hostname_queue_item>`\ (\ host\: :ref:`String<class_String>`, ip_type\: :ref:`Type<enum_IP_Type>` = 3\ ) |
   +------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_IP_ResolverStatus:

.. rst-class:: classref-enumeration

enum **ResolverStatus**: :ref:`🔗<enum_IP_ResolverStatus>`

.. _class_IP_constant_RESOLVER_STATUS_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`ResolverStatus<enum_IP_ResolverStatus>` **RESOLVER_STATUS_NONE** = ``0``

Trạng thái DNS hostname resolver: Không có trạng thái.

.. _class_IP_constant_RESOLVER_STATUS_WAITING:

.. rst-class:: classref-enumeration-constant

:ref:`ResolverStatus<enum_IP_ResolverStatus>` **RESOLVER_STATUS_WAITING** = ``1``

Trạng thái DNS hostname resolver: Đang chờ.

.. _class_IP_constant_RESOLVER_STATUS_DONE:

.. rst-class:: classref-enumeration-constant

:ref:`ResolverStatus<enum_IP_ResolverStatus>` **RESOLVER_STATUS_DONE** = ``2``

Trạng thái DNS hostname resolver: Hoàn tất.

.. _class_IP_constant_RESOLVER_STATUS_ERROR:

.. rst-class:: classref-enumeration-constant

:ref:`ResolverStatus<enum_IP_ResolverStatus>` **RESOLVER_STATUS_ERROR** = ``3``

Trạng thái DNS hostname resolver: Lỗi.

.. rst-class:: classref-item-separator

----

.. _enum_IP_Type:

.. rst-class:: classref-enumeration

enum **Type**: :ref:`🔗<enum_IP_Type>`

.. _class_IP_constant_TYPE_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`Type<enum_IP_Type>` **TYPE_NONE** = ``0``

Loại địa chỉ: Không có.

.. _class_IP_constant_TYPE_IPV4:

.. rst-class:: classref-enumeration-constant

:ref:`Type<enum_IP_Type>` **TYPE_IPV4** = ``1``

Loại địa chỉ: Internet protocol version 4 (IPv4).

.. _class_IP_constant_TYPE_IPV6:

.. rst-class:: classref-enumeration-constant

:ref:`Type<enum_IP_Type>` **TYPE_IPV6** = ``2``

Loại địa chỉ: Internet protocol version 6 (IPv6).

.. _class_IP_constant_TYPE_ANY:

.. rst-class:: classref-enumeration-constant

:ref:`Type<enum_IP_Type>` **TYPE_ANY** = ``3``

Loại địa chỉ: Bất kỳ.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các hằng số
-----------

.. _class_IP_constant_RESOLVER_MAX_QUERIES:

.. rst-class:: classref-constant

**RESOLVER_MAX_QUERIES** = ``256`` :ref:`🔗<class_IP_constant_RESOLVER_MAX_QUERIES>`

Số lượng truy vấn DNS resolver đồng thời tối đa được phép; nếu vượt quá, :ref:`RESOLVER_INVALID_ID<class_IP_constant_RESOLVER_INVALID_ID>` sẽ được trả về.

.. _class_IP_constant_RESOLVER_INVALID_ID:

.. rst-class:: classref-constant

**RESOLVER_INVALID_ID** = ``-1`` :ref:`🔗<class_IP_constant_RESOLVER_INVALID_ID>`

Hằng số ID không hợp lệ. Được trả về nếu vượt quá :ref:`RESOLVER_MAX_QUERIES<class_IP_constant_RESOLVER_MAX_QUERIES>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_IP_method_clear_cache:

.. rst-class:: classref-method

|void| **clear_cache**\ (\ hostname\: :ref:`String<class_String>` = ""\ ) :ref:`🔗<class_IP_method_clear_cache>`

Xóa tất cả các tham chiếu đã lưu trong cache của ``hostname``. Nếu không cung cấp ``hostname``, tất cả địa chỉ IP đã lưu trong cache sẽ bị xóa.

.. rst-class:: classref-item-separator

----

.. _class_IP_method_erase_resolve_item:

.. rst-class:: classref-method

|void| **erase_resolve_item**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_IP_method_erase_resolve_item>`

Xóa một mục ``id`` đã cho khỏi queue. Nên dùng phương thức này để giải phóng một queue sau khi hoàn tất, cho phép thực hiện thêm các truy vấn.

.. rst-class:: classref-item-separator

----

.. _class_IP_method_get_local_addresses:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **get_local_addresses**\ (\ ) |const| :ref:`🔗<class_IP_method_get_local_addresses>`

Trả về tất cả địa chỉ IPv4 và IPv6 hiện tại của người dùng dưới dạng một array.

.. rst-class:: classref-item-separator

----

.. _class_IP_method_get_local_interfaces:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`Dictionary<class_Dictionary>`\] **get_local_interfaces**\ (\ ) |const| :ref:`🔗<class_IP_method_get_local_interfaces>`

Trả về tất cả network adapter dưới dạng một array.

Mỗi adapter là một dictionary có dạng:

::

    {
        "index": "1", # Chỉ mục interface.
        "name": "eth0", # Tên interface.
        "friendly": "Ethernet One", # Tên thân thiện (có thể rỗng).
        "addresses": ["192.168.1.101"], # Một array gồm các địa chỉ IP liên kết với interface này.
    }

.. rst-class:: classref-item-separator

----

.. _class_IP_method_get_resolve_item_address:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_resolve_item_address**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IP_method_get_resolve_item_address>`

Trả về địa chỉ IP của hostname trong queue, dựa trên ``id`` của queue đó. Trả về một chuỗi rỗng nếu xảy ra lỗi hoặc quá trình phân giải chưa diễn ra (xem :ref:`get_resolve_item_status()<class_IP_method_get_resolve_item_status>`).

.. rst-class:: classref-item-separator

----

.. _class_IP_method_get_resolve_item_addresses:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **get_resolve_item_addresses**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IP_method_get_resolve_item_addresses>`

Trả về các địa chỉ đã phân giải hoặc một array rỗng nếu xảy ra lỗi hoặc quá trình phân giải chưa diễn ra (xem :ref:`get_resolve_item_status()<class_IP_method_get_resolve_item_status>`).

.. rst-class:: classref-item-separator

----

.. _class_IP_method_get_resolve_item_status:

.. rst-class:: classref-method

:ref:`ResolverStatus<enum_IP_ResolverStatus>` **get_resolve_item_status**\ (\ id\: :ref:`int<class_int>`\ ) |const| :ref:`🔗<class_IP_method_get_resolve_item_status>`

Trả về trạng thái của hostname trong queue dưới dạng một hằng số :ref:`ResolverStatus<enum_IP_ResolverStatus>`, dựa trên ``id`` của queue đó.

.. rst-class:: classref-item-separator

----

.. _class_IP_method_resolve_hostname:

.. rst-class:: classref-method

:ref:`String<class_String>` **resolve_hostname**\ (\ host\: :ref:`String<class_String>`, ip_type\: :ref:`Type<enum_IP_Type>` = 3\ ) :ref:`🔗<class_IP_method_resolve_hostname>`

Trả về địa chỉ IPv4 hoặc IPv6 của hostname đã cho sau khi được phân giải (phương thức dạng blocking). Loại địa chỉ được trả về phụ thuộc vào hằng số :ref:`Type<enum_IP_Type>` được cung cấp dưới dạng ``ip_type``.

.. rst-class:: classref-item-separator

----

.. _class_IP_method_resolve_hostname_addresses:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **resolve_hostname_addresses**\ (\ host\: :ref:`String<class_String>`, ip_type\: :ref:`Type<enum_IP_Type>` = 3\ ) :ref:`🔗<class_IP_method_resolve_hostname_addresses>`

Phân giải hostname đã cho theo cách blocking. Các địa chỉ được trả về dưới dạng một :ref:`Array<class_Array>` gồm các địa chỉ IPv4 hoặc IPv6, tùy thuộc vào ``ip_type``.

.. rst-class:: classref-item-separator

----

.. _class_IP_method_resolve_hostname_queue_item:

.. rst-class:: classref-method

:ref:`int<class_int>` **resolve_hostname_queue_item**\ (\ host\: :ref:`String<class_String>`, ip_type\: :ref:`Type<enum_IP_Type>` = 3\ ) :ref:`🔗<class_IP_method_resolve_hostname_queue_item>`

Tạo một mục queue để phân giải hostname thành địa chỉ IPv4 hoặc IPv6, tùy thuộc vào hằng số :ref:`Type<enum_IP_Type>` được cung cấp dưới dạng ``ip_type``. Trả về ID của queue nếu thành công hoặc :ref:`RESOLVER_INVALID_ID<class_IP_constant_RESOLVER_INVALID_ID>` nếu xảy ra lỗi.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
