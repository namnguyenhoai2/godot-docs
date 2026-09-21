:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/JavaScriptBridge.xml.

.. _class_JavaScriptBridge:

JavaScriptBridge
================

**Kế thừa:** :ref:`Object<class_Object>`

Singleton kết nối engine với context JavaScript của trình duyệt trong bản export Web.

.. rst-class:: classref-introduction-group

Mô tả
-----

Singleton JavaScriptBridge chỉ được triển khai trong bản export Web. Singleton này được dùng để truy cập context JavaScript của trình duyệt. Điều này cho phép tương tác với các trang nhúng hoặc gọi các API JavaScript của bên thứ ba.

\ **Lưu ý:** Có thể vô hiệu hóa singleton này tại thời điểm build để tăng cường bảo mật. Theo mặc định, singleton JavaScriptBridge được bật. Các export template chính thức cũng bật singleton JavaScriptBridge. Xem :doc:`Biên dịch cho Web <../engine_details/development/compiling/compiling_for_web>` trong tài liệu để biết thêm thông tin.

.. rst-class:: classref-introduction-group

Tutorial
--------

- :doc:`Singleton JavaScriptBridge <../tutorials/platform/web/javascript_bridge>`

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaScriptObject<class_JavaScriptObject>` | :ref:`create_callback<class_JavaScriptBridge_method_create_callback>`\ (\ callable\: :ref:`Callable<class_Callable>`\ )                                                                                                                  |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                   | :ref:`create_object<class_JavaScriptBridge_method_create_object>`\ (\ object\: :ref:`String<class_String>`, ...\ ) |vararg|                                                                                                              |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`download_buffer<class_JavaScriptBridge_method_download_buffer>`\ (\ buffer\: :ref:`PackedByteArray<class_PackedByteArray>`, name\: :ref:`String<class_String>`, mime\: :ref:`String<class_String>` = "application/octet-stream"\ ) |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Variant<class_Variant>`                   | :ref:`eval<class_JavaScriptBridge_method_eval>`\ (\ code\: :ref:`String<class_String>`, use_global_execution_context\: :ref:`bool<class_bool>` = false\ )                                                                                |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                          | :ref:`force_fs_sync<class_JavaScriptBridge_method_force_fs_sync>`\ (\ )                                                                                                                                                                  |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`JavaScriptObject<class_JavaScriptObject>` | :ref:`get_interface<class_JavaScriptBridge_method_get_interface>`\ (\ interface\: :ref:`String<class_String>`\ )                                                                                                                         |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`is_js_buffer<class_JavaScriptBridge_method_is_js_buffer>`\ (\ javascript_object\: :ref:`JavaScriptObject<class_JavaScriptObject>`\ )                                                                                               |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedByteArray<class_PackedByteArray>`   | :ref:`js_buffer_to_packed_byte_array<class_JavaScriptBridge_method_js_buffer_to_packed_byte_array>`\ (\ javascript_buffer\: :ref:`JavaScriptObject<class_JavaScriptObject>`\ )                                                           |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                         | :ref:`pwa_needs_update<class_JavaScriptBridge_method_pwa_needs_update>`\ (\ ) |const|                                                                                                                                                    |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`           | :ref:`pwa_update<class_JavaScriptBridge_method_pwa_update>`\ (\ )                                                                                                                                                                        |
   +-------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_JavaScriptBridge_signal_pwa_update_available:

.. rst-class:: classref-signal

**pwa_update_available**\ (\ ) :ref:`🔗<class_JavaScriptBridge_signal_pwa_update_available>`

Được phát ra khi phát hiện bản cập nhật cho progressive web app này nhưng bản cập nhật đang chờ được kích hoạt vì một phiên bản trước đó đang hoạt động. Xem :ref:`pwa_update()<class_JavaScriptBridge_method_pwa_update>` để buộc cập nhật diễn ra ngay lập tức.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_JavaScriptBridge_method_create_callback:

.. rst-class:: classref-method

:ref:`JavaScriptObject<class_JavaScriptObject>` **create_callback**\ (\ callable\: :ref:`Callable<class_Callable>`\ ) :ref:`🔗<class_JavaScriptBridge_method_create_callback>`

Tạo một tham chiếu đến :ref:`Callable<class_Callable>` có thể được JavaScript sử dụng làm callback. Phải giữ tham chiếu này cho đến khi callback xảy ra, nếu không callback sẽ hoàn toàn không được gọi. Xem :ref:`JavaScriptObject<class_JavaScriptObject>` để biết cách sử dụng.

\ **Lưu ý:** Hàm callback phải nhận chính xác một đối số :ref:`Array<class_Array>`, đối số này sẽ là `arguments object <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments>`__ JavaScript được chuyển đổi thành một mảng.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_create_object:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **create_object**\ (\ object\: :ref:`String<class_String>`, ...\ ) |vararg| :ref:`🔗<class_JavaScriptBridge_method_create_object>`

Tạo một object JavaScript mới bằng constructor ``new``. ``object`` phải là một thuộc tính hợp lệ của ``window`` JavaScript. Xem :ref:`JavaScriptObject<class_JavaScriptObject>` để biết cách sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_download_buffer:

.. rst-class:: classref-method

|void| **download_buffer**\ (\ buffer\: :ref:`PackedByteArray<class_PackedByteArray>`, name\: :ref:`String<class_String>`, mime\: :ref:`String<class_String>` = "application/octet-stream"\ ) :ref:`🔗<class_JavaScriptBridge_method_download_buffer>`

Nhắc người dùng tải xuống một tệp chứa ``buffer`` được chỉ định. Tệp sẽ có kiểu ``name`` và ``mime`` đã cho.

\ **Lưu ý:** Trình duyệt có thể ghi đè `MIME type <https://en.wikipedia.org/wiki/Media_type>`__ được cung cấp dựa trên phần mở rộng của ``name`` tệp.

\ **Lưu ý:** Trình duyệt có thể chặn quá trình tải xuống nếu :ref:`download_buffer()<class_JavaScriptBridge_method_download_buffer>` không được gọi từ một tương tác của người dùng (ví dụ: nhấp vào nút).

\ **Lưu ý:** Trình duyệt có thể yêu cầu người dùng cấp quyền hoặc chặn quá trình tải xuống nếu có nhiều yêu cầu tải xuống được thực hiện liên tiếp trong thời gian ngắn.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_eval:

.. rst-class:: classref-method

:ref:`Variant<class_Variant>` **eval**\ (\ code\: :ref:`String<class_String>`, use_global_execution_context\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_JavaScriptBridge_method_eval>`

Thực thi chuỗi ``code`` dưới dạng mã JavaScript trong cửa sổ trình duyệt. Đây là một lệnh gọi đến hàm JavaScript toàn cục thực tế ``eval()``.

Nếu ``use_global_execution_context`` là ``true``, mã sẽ được đánh giá trong execution context toàn cục. Nếu không, mã được đánh giá trong execution context của một hàm bên trong môi trường runtime của engine.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_force_fs_sync:

.. rst-class:: classref-method

|void| **force_fs_sync**\ (\ ) :ref:`🔗<class_JavaScriptBridge_method_force_fs_sync>`

Buộc đồng bộ hóa hệ thống tệp persistent (khi được bật).

\ **Lưu ý:** Điều này chỉ hữu ích đối với các module hoặc extension không thể sử dụng :ref:`FileAccess<class_FileAccess>` để ghi tệp.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_get_interface:

.. rst-class:: classref-method

:ref:`JavaScriptObject<class_JavaScriptObject>` **get_interface**\ (\ interface\: :ref:`String<class_String>`\ ) :ref:`🔗<class_JavaScriptBridge_method_get_interface>`

Trả về một interface đến một object JavaScript có thể được các script sử dụng. ``interface`` phải là một thuộc tính hợp lệ của ``window`` JavaScript. Callback phải chấp nhận một đối số :ref:`Array<class_Array>` duy nhất, đối số này sẽ chứa ``arguments`` JavaScript. Xem :ref:`JavaScriptObject<class_JavaScriptObject>` để biết cách sử dụng.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_is_js_buffer:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **is_js_buffer**\ (\ javascript_object\: :ref:`JavaScriptObject<class_JavaScriptObject>`\ ) :ref:`🔗<class_JavaScriptBridge_method_is_js_buffer>`

Trả về ``true`` nếu ``javascript_object`` đã cho thuộc kiểu `ArrayBuffer <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer>`__, `DataView <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DataView>`__ hoặc một trong nhiều `typed array objects <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray>`__.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_js_buffer_to_packed_byte_array:

.. rst-class:: classref-method

:ref:`PackedByteArray<class_PackedByteArray>` **js_buffer_to_packed_byte_array**\ (\ javascript_buffer\: :ref:`JavaScriptObject<class_JavaScriptObject>`\ ) :ref:`🔗<class_JavaScriptBridge_method_js_buffer_to_packed_byte_array>`

Trả về một bản sao nội dung của ``javascript_buffer`` dưới dạng :ref:`PackedByteArray<class_PackedByteArray>`. Xem thêm :ref:`is_js_buffer()<class_JavaScriptBridge_method_is_js_buffer>`.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_pwa_needs_update:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **pwa_needs_update**\ (\ ) |const| :ref:`🔗<class_JavaScriptBridge_method_pwa_needs_update>`

Trả về ``true`` nếu một phiên bản mới của progressive web app đang chờ được kích hoạt.

\ **Lưu ý:** Chỉ liên quan khi được export dưới dạng Progressive Web App.

.. rst-class:: classref-item-separator

----

.. _class_JavaScriptBridge_method_pwa_update:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **pwa_update**\ (\ ) :ref:`🔗<class_JavaScriptBridge_method_pwa_update>`

Thực hiện live update cho progressive web app. Buộc cài đặt phiên bản mới và tải lại trang.

\ **Lưu ý:** Ứng dụng của bạn sẽ được **tải lại trong tất cả các tab trình duyệt**.

\ **Lưu ý:** Chỉ liên quan khi được export dưới dạng Progressive Web App và :ref:`pwa_needs_update()<class_JavaScriptBridge_method_pwa_needs_update>` trả về ``true``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
