:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CameraFeed.xml.

.. _class_CameraFeed:

CameraFeed
==========

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một camera feed cho phép bạn truy cập vào một camera vật lý duy nhất được gắn với thiết bị của bạn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một camera feed cho phép bạn truy cập vào một camera vật lý duy nhất được gắn với thiết bị của bạn. Khi được bật, Godot sẽ bắt đầu thu thập các khung hình từ camera để sử dụng. Xem thêm :ref:`CameraServer<class_CameraServer>`.

\ **Lưu ý:** Nhiều camera sẽ trả về hình ảnh YCbCr được tách thành hai texture và cần được kết hợp trong một shader. Godot sẽ tự động thực hiện việc này cho bạn nếu bạn đặt môi trường để hiển thị hình ảnh camera ở nền.

\ **Lưu ý:** Class này hiện chỉ được triển khai trên Linux, Android, macOS và iOS. Trên các nền tảng khác, sẽ không có **CameraFeed**\ nào khả dụng. Để lấy một **CameraFeed** trên iOS, hãy bật :ref:`EditorExportPlatformIOS.modules/camera<class_EditorExportPlatformIOS_property_modules/camera>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------+-----------------------------------------------------------------+------------------------------------+
   | :ref:`bool<class_bool>`               | :ref:`feed_is_active<class_CameraFeed_property_feed_is_active>` | ``false``                          |
   +---------------------------------------+-----------------------------------------------------------------+------------------------------------+
   | :ref:`Transform2D<class_Transform2D>` | :ref:`feed_transform<class_CameraFeed_property_feed_transform>` | ``Transform2D(1, 0, 0, -1, 0, 1)`` |
   +---------------------------------------+-----------------------------------------------------------------+------------------------------------+
   | :ref:`Array<class_Array>`             | :ref:`formats<class_CameraFeed_property_formats>`               | ``[]``                             |
   +---------------------------------------+-----------------------------------------------------------------+------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`_activate_feed<class_CameraFeed_private_method__activate_feed>`\ (\ ) |virtual|                                                                            |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`_deactivate_feed<class_CameraFeed_private_method__deactivate_feed>`\ (\ ) |virtual|                                                                        |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`                         | :ref:`_get_formats<class_CameraFeed_private_method__get_formats>`\ (\ ) |virtual| |const|                                                                        |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`_set_format<class_CameraFeed_private_method__set_format>`\ (\ index\: :ref:`int<class_int>`, parameters\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`FeedDataType<enum_CameraFeed_FeedDataType>` | :ref:`get_datatype<class_CameraFeed_method_get_datatype>`\ (\ ) |const|                                                                                          |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_id<class_CameraFeed_method_get_id>`\ (\ ) |const|                                                                                                      |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`String<class_String>`                       | :ref:`get_name<class_CameraFeed_method_get_name>`\ (\ ) |const|                                                                                                  |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`FeedPosition<enum_CameraFeed_FeedPosition>` | :ref:`get_position<class_CameraFeed_method_get_position>`\ (\ ) |const|                                                                                          |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`get_texture_tex_id<class_CameraFeed_method_get_texture_tex_id>`\ (\ feed_image_type\: :ref:`FeedImage<enum_CameraServer_FeedImage>`\ )                     |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_external<class_CameraFeed_method_set_external>`\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`\ )                                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | :ref:`set_format<class_CameraFeed_method_set_format>`\ (\ index\: :ref:`int<class_int>`, parameters\: :ref:`Dictionary<class_Dictionary>`\ )                     |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_name<class_CameraFeed_method_set_name>`\ (\ name\: :ref:`String<class_String>`\ )                                                                      |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_position<class_CameraFeed_method_set_position>`\ (\ position\: :ref:`FeedPosition<enum_CameraFeed_FeedPosition>`\ )                                    |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_rgb_image<class_CameraFeed_method_set_rgb_image>`\ (\ rgb_image\: :ref:`Image<class_Image>`\ )                                                         |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_ycbcr_image<class_CameraFeed_method_set_ycbcr_image>`\ (\ ycbcr_image\: :ref:`Image<class_Image>`\ )                                                   |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`set_ycbcr_images<class_CameraFeed_method_set_ycbcr_images>`\ (\ y_image\: :ref:`Image<class_Image>`, cbcr_image\: :ref:`Image<class_Image>`\ )             |
   +---------------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các signal
----------

.. _class_CameraFeed_signal_format_changed:

.. rst-class:: classref-signal

**format_changed**\ (\ ) :ref:`🔗<class_CameraFeed_signal_format_changed>`

Được phát ra khi định dạng đã thay đổi.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_signal_frame_changed:

.. rst-class:: classref-signal

**frame_changed**\ (\ ) :ref:`🔗<class_CameraFeed_signal_frame_changed>`

Được phát ra khi có khung hình mới.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_CameraFeed_FeedDataType:

.. rst-class:: classref-enumeration

enum **FeedDataType**: :ref:`🔗<enum_CameraFeed_FeedDataType>`

.. _class_CameraFeed_constant_FEED_NOIMAGE:

.. rst-class:: classref-enumeration-constant

:ref:`FeedDataType<enum_CameraFeed_FeedDataType>` **FEED_NOIMAGE** = ``0``

Chưa đặt hình ảnh cho feed.

.. _class_CameraFeed_constant_FEED_RGB:

.. rst-class:: classref-enumeration-constant

:ref:`FeedDataType<enum_CameraFeed_FeedDataType>` **FEED_RGB** = ``1``

Feed cung cấp hình ảnh RGB.

.. _class_CameraFeed_constant_FEED_YCBCR:

.. rst-class:: classref-enumeration-constant

:ref:`FeedDataType<enum_CameraFeed_FeedDataType>` **FEED_YCBCR** = ``2``

Feed cung cấp hình ảnh YCbCr cần được chuyển đổi sang RGB.

.. _class_CameraFeed_constant_FEED_YCBCR_SEP:

.. rst-class:: classref-enumeration-constant

:ref:`FeedDataType<enum_CameraFeed_FeedDataType>` **FEED_YCBCR_SEP** = ``3``

Feed cung cấp các hình ảnh Y và CbCr riêng biệt cần được kết hợp và chuyển đổi sang RGB.

.. _class_CameraFeed_constant_FEED_EXTERNAL:

.. rst-class:: classref-enumeration-constant

:ref:`FeedDataType<enum_CameraFeed_FeedDataType>` **FEED_EXTERNAL** = ``4``

Feed cung cấp hình ảnh bên ngoài.

.. rst-class:: classref-item-separator

----

.. _enum_CameraFeed_FeedPosition:

.. rst-class:: classref-enumeration

enum **FeedPosition**: :ref:`🔗<enum_CameraFeed_FeedPosition>`

.. _class_CameraFeed_constant_FEED_UNSPECIFIED:

.. rst-class:: classref-enumeration-constant

:ref:`FeedPosition<enum_CameraFeed_FeedPosition>` **FEED_UNSPECIFIED** = ``0``

Vị trí không được chỉ định.

.. _class_CameraFeed_constant_FEED_FRONT:

.. rst-class:: classref-enumeration-constant

:ref:`FeedPosition<enum_CameraFeed_FeedPosition>` **FEED_FRONT** = ``1``

Camera được gắn ở mặt trước của thiết bị.

.. _class_CameraFeed_constant_FEED_BACK:

.. rst-class:: classref-enumeration-constant

:ref:`FeedPosition<enum_CameraFeed_FeedPosition>` **FEED_BACK** = ``2``

Camera được gắn ở mặt sau của thiết bị.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CameraFeed_property_feed_is_active:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **feed_is_active** = ``false`` :ref:`🔗<class_CameraFeed_property_feed_is_active>`

.. rst-class:: classref-property-setget

- |void| **set_active**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_active**\ (\ )

Nếu ``true``, feed đang hoạt động.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_property_feed_transform:

.. rst-class:: classref-property

:ref:`Transform2D<class_Transform2D>` **feed_transform** = ``Transform2D(1, 0, 0, -1, 0, 1)`` :ref:`🔗<class_CameraFeed_property_feed_transform>`

.. rst-class:: classref-property-setget

- |void| **set_transform**\ (\ value\: :ref:`Transform2D<class_Transform2D>`\ ) - :ref:`Transform2D<class_Transform2D>` **get_transform**\ (\ )

Phép biến đổi được áp dụng cho hình ảnh của camera.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_property_formats:

.. rst-class:: classref-property

:ref:`Array<class_Array>` **formats** = ``[]`` :ref:`🔗<class_CameraFeed_property_formats>`

.. rst-class:: classref-property-setget

- :ref:`Array<class_Array>` **get_formats**\ (\ )

Các định dạng được feed hỗ trợ. Mỗi mục là một :ref:`Dictionary<class_Dictionary>` mô tả các tham số định dạng.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CameraFeed_private_method__activate_feed:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_activate_feed**\ (\ ) |virtual| :ref:`🔗<class_CameraFeed_private_method__activate_feed>`

Được gọi khi camera feed được kích hoạt.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_private_method__deactivate_feed:

.. rst-class:: classref-method

|void| **_deactivate_feed**\ (\ ) |virtual| :ref:`🔗<class_CameraFeed_private_method__deactivate_feed>`

Được gọi khi camera feed bị vô hiệu hóa.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_private_method__get_formats:

.. rst-class:: classref-method

:ref:`Array<class_Array>` **_get_formats**\ (\ ) |virtual| |const| :ref:`🔗<class_CameraFeed_private_method__get_formats>`

Ghi đè phương thức này để định nghĩa các định dạng được camera feed hỗ trợ.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_private_method__set_format:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **_set_format**\ (\ index\: :ref:`int<class_int>`, parameters\: :ref:`Dictionary<class_Dictionary>`\ ) |virtual| :ref:`🔗<class_CameraFeed_private_method__set_format>`

Ghi đè phương thức này để đặt định dạng của camera feed.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_get_datatype:

.. rst-class:: classref-method

:ref:`FeedDataType<enum_CameraFeed_FeedDataType>` **get_datatype**\ (\ ) |const| :ref:`🔗<class_CameraFeed_method_get_datatype>`

Trả về kiểu dữ liệu hình ảnh của feed.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_get_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_id**\ (\ ) |const| :ref:`🔗<class_CameraFeed_method_get_id>`

Trả về ID duy nhất của feed này.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_get_name:

.. rst-class:: classref-method

:ref:`String<class_String>` **get_name**\ (\ ) |const| :ref:`🔗<class_CameraFeed_method_get_name>`

Trả về tên của camera.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_get_position:

.. rst-class:: classref-method

:ref:`FeedPosition<enum_CameraFeed_FeedPosition>` **get_position**\ (\ ) |const| :ref:`🔗<class_CameraFeed_method_get_position>`

Trả về vị trí của camera trên thiết bị.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_get_texture_tex_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_texture_tex_id**\ (\ feed_image_type\: :ref:`FeedImage<enum_CameraServer_FeedImage>`\ ) :ref:`🔗<class_CameraFeed_method_get_texture_tex_id>`

Trả về ID của texture backend (có thể được một số thư viện bên ngoài sử dụng khi cần handle của texture để ghi dữ liệu).

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_external:

.. rst-class:: classref-method

|void| **set_external**\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CameraFeed_method_set_external>`

Đặt feed thành external feed do một thư viện khác cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_format:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **set_format**\ (\ index\: :ref:`int<class_int>`, parameters\: :ref:`Dictionary<class_Dictionary>`\ ) :ref:`🔗<class_CameraFeed_method_set_format>`

Sets the feed format parameters for the given ``index`` in the :ref:`formats<class_CameraFeed_property_formats>` array. Returns ``true`` on success. By default, the YUYV encoded stream is transformed to :ref:`FEED_RGB<class_CameraFeed_constant_FEED_RGB>`. The YUYV encoded stream output format can be changed by setting ``parameters``'s ``output`` entry to one of the following:

- ``"separate"`` sẽ cho kết quả là :ref:`FEED_YCBCR_SEP<class_CameraFeed_constant_FEED_YCBCR_SEP>`;

- ``"grayscale"`` sẽ cho kết quả là :ref:`FEED_RGB<class_CameraFeed_constant_FEED_RGB>` đã giảm bão hòa;

- ``"copy"`` sẽ cho kết quả là :ref:`FEED_YCBCR<class_CameraFeed_constant_FEED_YCBCR>`.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_name:

.. rst-class:: classref-method

|void| **set_name**\ (\ name\: :ref:`String<class_String>`\ ) :ref:`🔗<class_CameraFeed_method_set_name>`

Đặt tên của camera.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_position:

.. rst-class:: classref-method

|void| **set_position**\ (\ position\: :ref:`FeedPosition<enum_CameraFeed_FeedPosition>`\ ) :ref:`🔗<class_CameraFeed_method_set_position>`

Đặt vị trí của camera này.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_rgb_image:

.. rst-class:: classref-method

|void| **set_rgb_image**\ (\ rgb_image\: :ref:`Image<class_Image>`\ ) :ref:`🔗<class_CameraFeed_method_set_rgb_image>`

Đặt hình ảnh RGB cho feed này.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_ycbcr_image:

.. rst-class:: classref-method

|void| **set_ycbcr_image**\ (\ ycbcr_image\: :ref:`Image<class_Image>`\ ) :ref:`🔗<class_CameraFeed_method_set_ycbcr_image>`

Đặt hình ảnh YCbCr cho feed này.

.. rst-class:: classref-item-separator

----

.. _class_CameraFeed_method_set_ycbcr_images:

.. rst-class:: classref-method

|void| **set_ycbcr_images**\ (\ y_image\: :ref:`Image<class_Image>`, cbcr_image\: :ref:`Image<class_Image>`\ ) :ref:`🔗<class_CameraFeed_method_set_ycbcr_images>`

Đặt các hình ảnh Y và CbCr cho feed này.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
