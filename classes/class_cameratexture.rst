:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/CameraTexture.xml.

.. _class_CameraTexture:

CameraTexture
=============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture được cung cấp bởi một :ref:`CameraFeed<class_CameraFeed>`.

.. rst-class:: classref-introduction-group

Mô tả
-----

Texture này cho phép truy cập vào texture camera được cung cấp bởi một :ref:`CameraFeed<class_CameraFeed>`.

\ **Lưu ý:** Nhiều camera cung cấp hình ảnh YCbCr, cần được chuyển đổi trong shader.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------------------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                         | :ref:`camera_feed_id<class_CameraTexture_property_camera_feed_id>`     | ``0``                                                                                  |
   +-----------------------------------------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | :ref:`camera_is_active<class_CameraTexture_property_camera_is_active>` | ``false``                                                                              |
   +-----------------------------------------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                       | resource_local_to_scene                                                | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-----------------------------------------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`FeedImage<enum_CameraServer_FeedImage>` | :ref:`which_feed<class_CameraTexture_property_which_feed>`             | ``0``                                                                                  |
   +-----------------------------------------------+------------------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CameraTexture_property_camera_feed_id:

.. rst-class:: classref-property

:ref:`int<class_int>` **camera_feed_id** = ``0`` :ref:`🔗<class_CameraTexture_property_camera_feed_id>`

.. rst-class:: classref-property-setget

- |void| **set_camera_feed_id**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_camera_feed_id**\ (\ )

ID của :ref:`CameraFeed<class_CameraFeed>` mà chúng ta muốn hiển thị hình ảnh.

.. rst-class:: classref-item-separator

----

.. _class_CameraTexture_property_camera_is_active:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **camera_is_active** = ``false`` :ref:`🔗<class_CameraTexture_property_camera_is_active>`

.. rst-class:: classref-property-setget

- |void| **set_camera_active**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_camera_active**\ (\ )

Thuộc tính tiện ích cho phép truy cập vào thuộc tính active của :ref:`CameraFeed<class_CameraFeed>`.

.. rst-class:: classref-item-separator

----

.. _class_CameraTexture_property_which_feed:

.. rst-class:: classref-property

:ref:`FeedImage<enum_CameraServer_FeedImage>` **which_feed** = ``0`` :ref:`🔗<class_CameraTexture_property_which_feed>`

.. rst-class:: classref-property-setget

- |void| **set_which_feed**\ (\ value\: :ref:`FeedImage<enum_CameraServer_FeedImage>`\ ) - :ref:`FeedImage<enum_CameraServer_FeedImage>` **get_which_feed**\ (\ )

Hình ảnh nào trong :ref:`CameraFeed<class_CameraFeed>` mà chúng ta muốn truy cập; điều này rất quan trọng nếu hình ảnh camera được chia thành thành phần Y và CbCr.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
