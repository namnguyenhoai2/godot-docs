:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/FramebufferCacheRD.xml.

.. _class_FramebufferCacheRD:

FramebufferCacheRD
==================

**Kế thừa:** :ref:`Object<class_Object>`

Trình quản lý bộ nhớ đệm framebuffer cho các renderer dựa trên Rendering Device.

.. rst-class:: classref-introduction-group

Mô tả
-----

Trình quản lý bộ nhớ đệm framebuffer cho các renderer dựa trên :ref:`RenderingDevice<class_RenderingDevice>`. Cung cấp cách tạo một framebuffer và tái sử dụng nó trong các lần gọi tiếp theo chừng nào các texture được sử dụng còn tồn tại. Các framebuffer sẽ tự động được dọn dẹp khi các đối tượng phụ thuộc được giải phóng.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`RID<class_RID>` | :ref:`get_cache_multipass<class_FramebufferCacheRD_method_get_cache_multipass>`\ (\ textures\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\], passes\: :ref:`Array<class_Array>`\[:ref:`RDFramebufferPass<class_RDFramebufferPass>`\], views\: :ref:`int<class_int>`\ ) |static| |
   +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_FramebufferCacheRD_method_get_cache_multipass:

.. rst-class:: classref-method

:ref:`RID<class_RID>` **get_cache_multipass**\ (\ textures\: :ref:`Array<class_Array>`\[:ref:`RID<class_RID>`\], passes\: :ref:`Array<class_Array>`\[:ref:`RDFramebufferPass<class_RDFramebufferPass>`\], views\: :ref:`int<class_int>`\ ) |static| :ref:`🔗<class_FramebufferCacheRD_method_get_cache_multipass>`

Tạo hoặc lấy một framebuffer đã được lưu trong bộ nhớ đệm. ``textures`` liệt kê các texture được truy cập. ``passes`` xác định các subpass và việc cấp phát texture; nếu để trống, một pass đơn sẽ được tạo và các texture sẽ được cấp phát tùy theo cờ sử dụng của chúng. ``views`` xác định số lượng view được sử dụng khi render.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
