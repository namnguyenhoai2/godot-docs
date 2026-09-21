:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CameraServer.xml.

.. _class_CameraServer:

CameraServer
============

**Kế thừa:** :ref:`Object<class_Object>`

Server theo dõi các camera khác nhau có thể truy cập trong Godot.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CameraServer** theo dõi các camera khác nhau có thể truy cập trong Godot. Đây là các camera bên ngoài như webcam hoặc camera trên điện thoại của bạn.

Nó đặc biệt được dùng để cung cấp luồng video từ camera cho các module AR.

\ **Note:** This class is currently only implemented on Linux, Android, macOS, and iOS. On other platforms no :ref:`CameraFeed<class_CameraFeed>`\ s will be available. To get a :ref:`CameraFeed<class_CameraFeed>` on iOS, enable :ref:`EditorExportPlatformIOS.modules/camera<class_EditorExportPlatformIOS_property_modules/camera>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+-----------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>` | :ref:`monitoring_feeds<class_CameraServer_property_monitoring_feeds>` | ``false`` |
   +-------------------------+-----------------------------------------------------------------------+-----------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`add_feed<class_CameraServer_method_add_feed>`\ (\ feed\: :ref:`CameraFeed<class_CameraFeed>`\ )       |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`Array<class_Array>`\[:ref:`CameraFeed<class_CameraFeed>`\] | :ref:`feeds<class_CameraServer_method_feeds>`\ (\ )                                                         |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`CameraFeed<class_CameraFeed>`                              | :ref:`get_feed<class_CameraServer_method_get_feed>`\ (\ index\: :ref:`int<class_int>`\ )                    |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                                            | :ref:`get_feed_count<class_CameraServer_method_get_feed_count>`\ (\ )                                       |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+
   | |void|                                                           | :ref:`remove_feed<class_CameraServer_method_remove_feed>`\ (\ feed\: :ref:`CameraFeed<class_CameraFeed>`\ ) |
   +------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Signals
-------

.. _class_CameraServer_signal_camera_feed_added:

.. rst-class:: classref-signal

**camera_feed_added**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CameraServer_signal_camera_feed_added>`

Được phát ra khi một :ref:`CameraFeed<class_CameraFeed>` được thêm vào (ví dụ: khi một webcam được cắm vào).

.. rst-class:: classref-item-separator

----

.. _class_CameraServer_signal_camera_feed_removed:

.. rst-class:: classref-signal

**camera_feed_removed**\ (\ id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CameraServer_signal_camera_feed_removed>`

Được phát ra khi một :ref:`CameraFeed<class_CameraFeed>` bị xóa (ví dụ: khi một webcam bị rút ra).

.. rst-class:: classref-item-separator

----

.. _class_CameraServer_signal_camera_feeds_updated:

.. rst-class:: classref-signal

**camera_feeds_updated**\ (\ ) :ref:`🔗<class_CameraServer_signal_camera_feeds_updated>`

Được phát ra khi các camera feed được cập nhật.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enum
--------

.. _enum_CameraServer_FeedImage:

.. rst-class:: classref-enumeration

enum **FeedImage**: :ref:`🔗<enum_CameraServer_FeedImage>`

.. _class_CameraServer_constant_FEED_RGBA_IMAGE:

.. rst-class:: classref-enumeration-constant

:ref:`FeedImage<enum_CameraServer_FeedImage>` **FEED_RGBA_IMAGE** = ``0``

Hình ảnh camera RGBA.

.. _class_CameraServer_constant_FEED_YCBCR_IMAGE:

.. rst-class:: classref-enumeration-constant

:ref:`FeedImage<enum_CameraServer_FeedImage>` **FEED_YCBCR_IMAGE** = ``0``

Hình ảnh camera thành phần `YCbCr <https://en.wikipedia.org/wiki/YCbCr>`_.

.. _class_CameraServer_constant_FEED_Y_IMAGE:

.. rst-class:: classref-enumeration-constant

:ref:`FeedImage<enum_CameraServer_FeedImage>` **FEED_Y_IMAGE** = ``0``

Hình ảnh camera thành phần Y.

.. _class_CameraServer_constant_FEED_CBCR_IMAGE:

.. rst-class:: classref-enumeration-constant

:ref:`FeedImage<enum_CameraServer_FeedImage>` **FEED_CBCR_IMAGE** = ``1``

Hình ảnh camera thành phần CbCr.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CameraServer_property_monitoring_feeds:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **monitoring_feeds** = ``false`` :ref:`🔗<class_CameraServer_property_monitoring_feeds>`

.. rst-class:: classref-property-setget

- |void| **set_monitoring_feeds**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_monitoring_feeds**\ (\ )

Nếu ``true``, server sẽ chủ động theo dõi các camera feed hiện có.

Điều này làm giảm hiệu năng, vì vậy chỉ đặt thành ``true`` khi bạn đang chủ động truy cập camera.

\ **Lưu ý:** Sau khi đặt thành ``true``, bạn có thể nhận được các camera feed đã cập nhật thông qua signal :ref:`camera_feeds_updated<class_CameraServer_signal_camera_feeds_updated>`.


.. tabs::

 .. code-tab:: gdscript

    func _ready():
        CameraServer.camera_feeds_updated.connect(_on_camera_feeds_updated)
        CameraServer.monitoring_feeds = true

    func _on_camera_feeds_updated():
        var feeds = CameraServer.feeds()

 .. code-tab:: csharp

    public override void _Ready()
    {
        CameraServer.CameraFeedsUpdated += OnCameraFeedsUpdated;
        CameraServer.MonitoringFeeds = true;
    }

    void OnCameraFeedsUpdated()
    {
        var feeds = CameraServer.Feeds();
    }



.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CameraServer_method_add_feed:

.. rst-class:: classref-method

|void| **add_feed**\ (\ feed\: :ref:`CameraFeed<class_CameraFeed>`\ ) :ref:`🔗<class_CameraServer_method_add_feed>`

Thêm camera ``feed`` vào camera server.

.. rst-class:: classref-item-separator

----

.. _class_CameraServer_method_feeds:

.. rst-class:: classref-method

:ref:`Array<class_Array>`\[:ref:`CameraFeed<class_CameraFeed>`\] **feeds**\ (\ ) :ref:`🔗<class_CameraServer_method_feeds>`

Returns an array of :ref:`CameraFeed<class_CameraFeed>`\ s.

.. rst-class:: classref-item-separator

----

.. _class_CameraServer_method_get_feed:

.. rst-class:: classref-method

:ref:`CameraFeed<class_CameraFeed>` **get_feed**\ (\ index\: :ref:`int<class_int>`\ ) :ref:`🔗<class_CameraServer_method_get_feed>`

Trả về :ref:`CameraFeed<class_CameraFeed>` tương ứng với camera có ``index`` đã cho.

.. rst-class:: classref-item-separator

----

.. _class_CameraServer_method_get_feed_count:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_feed_count**\ (\ ) :ref:`🔗<class_CameraServer_method_get_feed_count>`

Returns the number of :ref:`CameraFeed<class_CameraFeed>`\ s registered.

.. rst-class:: classref-item-separator

----

.. _class_CameraServer_method_remove_feed:

.. rst-class:: classref-method

|void| **remove_feed**\ (\ feed\: :ref:`CameraFeed<class_CameraFeed>`\ ) :ref:`🔗<class_CameraServer_method_remove_feed>`

Xóa camera ``feed`` được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
