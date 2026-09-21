:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ImageFormatLoaderExtension.xml.

.. _class_ImageFormatLoaderExtension:

ImageFormatLoaderExtension
==========================

**Kế thừa:** :ref:`ImageFormatLoader<class_ImageFormatLoader>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp cơ sở để tạo các extension :ref:`ImageFormatLoader<class_ImageFormatLoader>` (bổ sung hỗ trợ cho các định dạng ảnh khác).

.. rst-class:: classref-introduction-group

Mô tả
-----

Engine hỗ trợ nhiều định dạng ảnh ngay từ đầu (PNG, SVG, JPEG, WebP và một số định dạng khác), nhưng bạn có thể chọn triển khai hỗ trợ cho các định dạng ảnh bổ sung bằng cách mở rộng lớp này.

Hãy đảm bảo tuân thủ các kiểu và giá trị trả về được ghi trong tài liệu. Bạn nên tạo một instance của lớp này và gọi :ref:`add_format_loader()<class_ImageFormatLoaderExtension_method_add_format_loader>` để đăng ký loader đó trong giai đoạn khởi tạo.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`PackedStringArray<class_PackedStringArray>` | :ref:`_get_recognized_extensions<class_ImageFormatLoaderExtension_private_method__get_recognized_extensions>`\ (\ ) |virtual| |const|                                                                                                                                                                 |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>`             | :ref:`_load_image<class_ImageFormatLoaderExtension_private_method__load_image>`\ (\ image\: :ref:`Image<class_Image>`, fileaccess\: :ref:`FileAccess<class_FileAccess>`, flags\: |bitfield|\[:ref:`LoaderFlags<enum_ImageFormatLoader_LoaderFlags>`\], scale\: :ref:`float<class_float>`\ ) |virtual| |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`add_format_loader<class_ImageFormatLoaderExtension_method_add_format_loader>`\ (\ )                                                                                                                                                                                                             |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                            | :ref:`remove_format_loader<class_ImageFormatLoaderExtension_method_remove_format_loader>`\ (\ )                                                                                                                                                                                                       |
   +---------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ImageFormatLoaderExtension_private_method__get_recognized_extensions:

.. rst-class:: classref-method

:ref:`PackedStringArray<class_PackedStringArray>` **_get_recognized_extensions**\ (\ ) |virtual| |const| :ref:`🔗<class_ImageFormatLoaderExtension_private_method__get_recognized_extensions>`

Trả về danh sách phần mở rộng tệp cho định dạng ảnh này. Các tệp có phần mở rộng đã cho sẽ được xử lý như tệp ảnh và được tải bằng lớp này.

.. rst-class:: classref-item-separator

----

.. _class_ImageFormatLoaderExtension_private_method__load_image:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **_load_image**\ (\ image\: :ref:`Image<class_Image>`, fileaccess\: :ref:`FileAccess<class_FileAccess>`, flags\: |bitfield|\[:ref:`LoaderFlags<enum_ImageFormatLoader_LoaderFlags>`\], scale\: :ref:`float<class_float>`\ ) |virtual| :ref:`🔗<class_ImageFormatLoaderExtension_private_method__load_image>`

Tải nội dung của ``fileaccess`` vào ``image`` được cung cấp.

.. rst-class:: classref-item-separator

----

.. _class_ImageFormatLoaderExtension_method_add_format_loader:

.. rst-class:: classref-method

|void| **add_format_loader**\ (\ ) :ref:`🔗<class_ImageFormatLoaderExtension_method_add_format_loader>`

Thêm format loader này vào engine, cho phép nó nhận diện các phần mở rộng tệp được :ref:`_get_recognized_extensions()<class_ImageFormatLoaderExtension_private_method__get_recognized_extensions>` trả về.

.. rst-class:: classref-item-separator

----

.. _class_ImageFormatLoaderExtension_method_remove_format_loader:

.. rst-class:: classref-method

|void| **remove_format_loader**\ (\ ) :ref:`🔗<class_ImageFormatLoaderExtension_method_remove_format_loader>`

Xóa format loader này khỏi engine.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
