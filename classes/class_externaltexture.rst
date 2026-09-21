:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ExternalTexture.xml.

.. _class_ExternalTexture:

ExternalTexture
===============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture hiển thị nội dung của một buffer bên ngoài.

.. rst-class:: classref-introduction-group

Mô tả
-----

Hiển thị nội dung của một buffer bên ngoài do platform cung cấp.

Yêu cầu extension `OES_EGL_image_external <https://registry.khronos.org/OpenGL/extensions/OES/OES_EGL_image_external.txt>`__ (OpenGL) hoặc extension `VK_ANDROID_external_memory_android_hardware_buffer <https://registry.khronos.org/vulkan/specs/1.1-extensions/html/vkspec.html#VK_ANDROID_external_memory_android_hardware_buffer>`__ (Vulkan).

\ **Lưu ý:** Hiện tại, tính năng này chỉ được hỗ trợ trong các bản build Android.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------------+--------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`       | resource_local_to_scene                          | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------------+--------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Vector2<class_Vector2>` | :ref:`size<class_ExternalTexture_property_size>` | ``Vector2(256, 256)``                                                                  |
   +-------------------------------+--------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`int<class_int>` | :ref:`get_external_texture_id<class_ExternalTexture_method_get_external_texture_id>`\ (\ ) |const|                                   |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                | :ref:`set_external_buffer_id<class_ExternalTexture_method_set_external_buffer_id>`\ (\ external_buffer_id\: :ref:`int<class_int>`\ ) |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_ExternalTexture_property_size:

.. rst-class:: classref-property

:ref:`Vector2<class_Vector2>` **size** = ``Vector2(256, 256)`` :ref:`🔗<class_ExternalTexture_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector2<class_Vector2>`\ ) - :ref:`Vector2<class_Vector2>` **get_size**\ (\ )

Kích thước của texture bên ngoài.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ExternalTexture_method_get_external_texture_id:

.. rst-class:: classref-method

:ref:`int<class_int>` **get_external_texture_id**\ (\ ) |const| :ref:`🔗<class_ExternalTexture_method_get_external_texture_id>`

Trả về ID của texture bên ngoài.

Tùy thuộc vào trường hợp sử dụng, bạn có thể cần truyền giá trị này cho các API của platform, chẳng hạn khi tạo một ``android.graphics.SurfaceTexture`` trên Android.

.. rst-class:: classref-item-separator

----

.. _class_ExternalTexture_method_set_external_buffer_id:

.. rst-class:: classref-method

|void| **set_external_buffer_id**\ (\ external_buffer_id\: :ref:`int<class_int>`\ ) :ref:`🔗<class_ExternalTexture_method_set_external_buffer_id>`

Đặt ID của buffer bên ngoài.

Tùy thuộc vào trường hợp sử dụng, bạn có thể cần gọi hàm này với dữ liệu nhận được từ một API của platform, chẳng hạn ``SurfaceTexture.getHardwareBuffer()`` trên Android.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
