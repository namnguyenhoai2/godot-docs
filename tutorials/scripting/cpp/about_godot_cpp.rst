.. _doc_about_godot_cpp:

Giới thiệu về godot-cpp
=======================

`godot-cpp <https://github.com/godotengine/godot-cpp>`__ là các binding C++ GDExtension chính thức, được duy trì như một phần của dự án Godot.

godot-cpp được xây dựng bằng :ref:`GDExtension system <doc_gdextension>`, cho phép truy cập Godot gần như theo cùng cách với :ref:`modules <doc_custom_modules_in_cpp>`: Bạn có thể sử dụng rất nhiều `engine code <https://github.com/godotengine/godot>`__ trong dự án godot-cpp gần như nguyên trạng.

Cụ thể, godot-cpp có quyền truy cập vào tất cả các hàm mà :ref:`GDScript <doc_gdscript>` và :ref:`C# <doc_c_sharp>` có, đồng thời có thêm quyền truy cập vào một số hàm khác để truy cập dữ liệu cấp thấp nhanh hơn hoặc tích hợp sâu hơn với Godot.

Sự khác biệt giữa godot-cpp và các C++ module
---------------------------------------------

Bạn có thể sử dụng cả `godot-cpp <https://github.com/godotengine/godot-cpp>`__ và :ref:`C++ modules <doc_custom_modules_in_cpp>` để chạy mã C hoặc C++ trong một dự án Godot.

Cả hai cũng cho phép bạn tích hợp các thư viện bên thứ ba vào Godot. Lựa chọn phù hợp phụ thuộc vào nhu cầu của bạn.

Ưu điểm của godot-cpp
~~~~~~~~~~~~~~~~~~~~~

Không giống các module, godot-cpp (và GDExtension nói chung) không yêu cầu biên dịch mã nguồn của engine, giúp phân phối sản phẩm của bạn dễ dàng hơn. Nó cho phép bạn truy cập hầu hết API có sẵn cho GDScript và C#, cho phép bạn viết logic game với toàn quyền kiểm soát hiệu năng. Đây là lựa chọn lý tưởng nếu bạn cần mã hiệu năng cao và muốn phân phối mã đó dưới dạng một add-on trong
:ref:`Asset Store <doc_what_is_asset_store>`.

Ngoài ra:

- Bạn có thể sử dụng cùng một thư viện godot-cpp đã biên dịch trong editor và project đã export. Với các C++ module, bạn phải biên dịch lại tất cả export template mà mình định sử dụng nếu cần chức năng của module đó khi runtime. - godot-cpp chỉ yêu cầu bạn biên dịch thư viện của mình, không phải toàn bộ engine. Điều này khác với các C++ module, vốn được biên dịch tĩnh vào engine. Mỗi khi thay đổi một module, bạn cần biên dịch lại engine. Ngay cả với incremental build, quy trình này vẫn chậm hơn so với sử dụng godot-cpp.

Ưu điểm của các C++ module
~~~~~~~~~~~~~~~~~~~~~~~~~~

Chúng tôi khuyến nghị :ref:`C++ modules <doc_custom_modules_in_cpp>` trong những trường hợp godot-cpp (hoặc một hệ thống GDExtension khác) không đủ đáp ứng:

- Các C++ module cung cấp khả năng tích hợp sâu hơn vào engine. Khả năng truy cập của GDExtension không sâu bằng các static module. - Bạn có thể sử dụng các C++ module để cung cấp thêm tính năng cho một dự án mà không cần mang theo các tệp native library. Điều này cũng áp dụng cho các project đã export.

.. note::

    Nếu nhận thấy một số hệ thống cụ thể không thể truy cập thông qua godot-cpp nhưng lại có thể truy cập thông qua custom module, bạn có thể mở issue trên `godot-cpp repository <https://github.com/godotengine/godot-cpp>`__ để thảo luận về các phương án triển khai nhằm cung cấp chức năng còn thiếu.

.. _doc_what_is_gdextension_version_compatibility:

Khả năng tương thích phiên bản
------------------------------

Các GDExtension nhắm đến một phiên bản Godot cũ hơn sẽ hoạt động trong các phiên bản minor mới hơn, nhưng không hoạt động theo chiều ngược lại. Ví dụ, một GDExtension nhắm đến Godot 4.2 sẽ hoạt động bình thường trong Godot 4.3, nhưng một GDExtension nhắm đến Godot 4.3 sẽ không hoạt động trong Godot 4.2.

Vì lý do này, khi tạo GDExtension, bạn nên nhắm đến phiên bản Godot thấp nhất có các tính năng mình cần, *không phải* phiên bản Godot mới nhất. Điều này có thể giúp bạn không phải tạo nhiều bản build cho các phiên bản Godot khác nhau.

Có một ngoại lệ: các extension nhắm đến Godot 4.0 **sẽ không** hoạt động với Godot 4.1 trở lên (xem :ref:`updating_your_gdextension_for_godot_4_1`).

Nói chung, các GDExtension chỉ tương thích với những bản build của engine sử dụng cùng mức độ chính xác số thực như mức mà extension được biên dịch. Điều này có nghĩa là nếu bạn sử dụng một bản build của engine với số thực độ chính xác kép, extension cũng phải được biên dịch cho số thực độ chính xác kép và sử dụng tệp ``extension_api.json`` được tạo bởi bản build engine tùy chỉnh của bạn. Xem :ref:`doc_large_world_coordinates` để biết chi tiết.

Nói chung, nếu bạn build một phiên bản Godot tùy chỉnh, bạn nên tạo một ``extension_api.json`` từ phiên bản đó cho các GDExtension của mình, vì nó có thể có một số điểm khác biệt so với các bản build Godot chính thức. Bạn có thể tìm hiểu thêm về quy trình sử dụng các tệp ``extension_api.json`` tùy chỉnh trong :ref:`build system section <doc_godot_cpp_build_system>`.
