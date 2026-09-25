.. _doc_about_godot_cpp:

Giới thiệu về godot-cpp
=======================

`godot-cpp <https://github.com/godotengine/godot-cpp>`__ là các binding GDExtension C++ chính thức, được duy trì như một phần của dự án Godot.

godot-cpp được xây dựng bằng :ref:`hệ thống GDExtension <doc_gdextension>`, cho phép truy cập Godot gần như theo cách tương tự :ref:`module <doc_custom_modules_in_cpp>`: Bạn có thể sử dụng rất nhiều `mã engine <https://github.com/godotengine/godot>`__ trong dự án godot-cpp gần như nguyên trạng.

Cụ thể, godot-cpp có quyền truy cập vào tất cả các hàm mà :ref:`GDScript <doc_gdscript>` và :ref:`C# <doc_c_sharp>` có, đồng thời có thêm quyền truy cập vào một số hàm khác để truy cập dữ liệu cấp thấp nhanh hơn hoặc tích hợp sâu hơn với Godot.

Sự khác biệt giữa godot-cpp và C++ module
-----------------------------------------

Bạn có thể sử dụng cả `godot-cpp <https://github.com/godotengine/godot-cpp>`__ và :ref:`C++ module <doc_custom_modules_in_cpp>` để chạy mã C hoặc C++ trong một dự án Godot.

Cả hai cũng cho phép bạn tích hợp các thư viện bên thứ ba vào Godot. Lựa chọn nào phù hợp tùy thuộc vào nhu cầu của bạn.

Ưu điểm của godot-cpp
~~~~~~~~~~~~~~~~~~~~~

Không giống module, godot-cpp (và GDExtension nói chung) không yêu cầu biên dịch mã nguồn của engine, nhờ đó việc phân phối sản phẩm của bạn trở nên dễ dàng hơn. Nó cho phép bạn truy cập hầu hết API có sẵn cho GDScript và C#, giúp bạn viết logic game với toàn quyền kiểm soát hiệu năng. Đây là lựa chọn lý tưởng nếu bạn cần mã hiệu năng cao và muốn phân phối mã đó dưới dạng một add-on trên
:ref:`Asset Store <doc_what_is_asset_store>`.

Ngoài ra:

- Bạn có thể sử dụng cùng một thư viện godot-cpp đã biên dịch trong editor và dự án đã export. Với C++ module, bạn phải biên dịch lại tất cả export template dự định sử dụng nếu cần chức năng của module đó trong runtime.
- godot-cpp chỉ yêu cầu bạn biên dịch thư viện của mình, không phải toàn bộ engine. Điều này khác với C++ module, vốn được biên dịch tĩnh vào engine. Mỗi khi thay đổi một module, bạn cần biên dịch lại engine. Ngay cả với các bản build incremental, quy trình này vẫn chậm hơn so với việc sử dụng godot-cpp.

Ưu điểm của C++ module
~~~~~~~~~~~~~~~~~~~~~~

Chúng tôi khuyến nghị sử dụng :ref:`C++ module <doc_custom_modules_in_cpp>` trong những trường hợp godot-cpp (hoặc một hệ thống GDExtension khác) không đáp ứng đủ nhu cầu:

- C++ module cung cấp khả năng tích hợp sâu hơn vào engine. Quyền truy cập của GDExtension không sâu bằng module tĩnh.
- Bạn có thể sử dụng C++ module để cung cấp các tính năng bổ sung trong một dự án mà không cần mang theo các tệp thư viện native. Điều này cũng áp dụng cho các dự án đã export.

.. note::

    Nếu nhận thấy một số hệ thống cụ thể không thể truy cập thông qua godot-cpp nhưng có thể truy cập thông qua custom module, bạn có thể mở issue trên `repository godot-cpp <https://github.com/godotengine/godot-cpp>`__ để thảo luận về các phương án triển khai nhằm cung cấp chức năng còn thiếu.

.. _doc_what_is_gdextension_version_compatibility:

Tính tương thích phiên bản
--------------------------

GDExtension nhắm đến một phiên bản Godot cũ hơn sẽ hoạt động trong các phiên bản minor mới hơn, nhưng không ngược lại. Ví dụ, GDExtension nhắm đến Godot 4.2 sẽ hoạt động bình thường trong Godot 4.3, nhưng GDExtension nhắm đến Godot 4.3 sẽ không hoạt động trong Godot 4.2.

Vì lý do này, khi tạo GDExtension, bạn có thể muốn nhắm đến phiên bản Godot thấp nhất có các tính năng mình cần, *không phải* phiên bản Godot mới nhất. Điều này có thể giúp bạn không phải tạo nhiều bản build cho các phiên bản Godot khác nhau.

Có một ngoại lệ: các extension nhắm đến Godot 4.0 **sẽ không** hoạt động với Godot 4.1 trở lên (xem :ref:`updating_your_gdextension_for_godot_4_1`).

GDExtension cũng chỉ tương thích với các bản build engine sử dụng cùng mức độ chính xác dấu phẩy động mà extension được biên dịch cho. Điều này có nghĩa là nếu bạn sử dụng bản build engine với số thực độ chính xác kép, extension cũng phải được biên dịch cho số thực độ chính xác kép và sử dụng một tệp ``extension_api.json`` được tạo bởi bản build engine tùy chỉnh của bạn. Xem :ref:`doc_large_world_coordinates` để biết chi tiết.

Nhìn chung, nếu xây dựng một phiên bản Godot tùy chỉnh, bạn nên tạo một ``extension_api.json`` từ phiên bản đó cho các GDExtension của mình, vì nó có thể có một số khác biệt so với các bản build Godot chính thức. Bạn có thể tìm hiểu thêm về quy trình sử dụng các tệp ``extension_api.json`` tùy chỉnh trong :ref:`phần hệ thống build <doc_godot_cpp_build_system>`.
