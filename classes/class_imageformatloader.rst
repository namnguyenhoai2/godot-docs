:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Tự động được tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/ImageFormatLoader.xml.

.. _class_ImageFormatLoader:

ImageFormatLoader
=================

**Kế thừa:** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`ImageFormatLoaderExtension<class_ImageFormatLoaderExtension>`

Lớp cơ sở để thêm hỗ trợ cho các định dạng hình ảnh cụ thể.

.. rst-class:: classref-introduction-group

Mô tả
-----

Engine hỗ trợ sẵn nhiều định dạng hình ảnh (PNG, SVG, JPEG, WebP và một số định dạng khác), nhưng bạn có thể chọn triển khai hỗ trợ cho các định dạng hình ảnh bổ sung bằng cách mở rộng :ref:`ImageFormatLoaderExtension<class_ImageFormatLoaderExtension>`.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_ImageFormatLoader_LoaderFlags:

.. rst-class:: classref-enumeration

flags **LoaderFlags**: :ref:`🔗<enum_ImageFormatLoader_LoaderFlags>`

.. _class_ImageFormatLoader_constant_FLAG_NONE:

.. rst-class:: classref-enumeration-constant

:ref:`LoaderFlags<enum_ImageFormatLoader_LoaderFlags>` **FLAG_NONE** = ``0``

Hành vi tải mặc định. Không áp dụng xử lý nào cho hình ảnh.

.. _class_ImageFormatLoader_constant_FLAG_FORCE_LINEAR:

.. rst-class:: classref-enumeration-constant

:ref:`LoaderFlags<enum_ImageFormatLoader_LoaderFlags>` **FLAG_FORCE_LINEAR** = ``1``

Nếu được thiết lập, hình ảnh sẽ được chuyển đổi từ mã hóa sRGB sang mã hóa tuyến tính.

.. _class_ImageFormatLoader_constant_FLAG_CONVERT_COLORS:

.. rst-class:: classref-enumeration-constant

:ref:`LoaderFlags<enum_ImageFormatLoader_LoaderFlags>` **FLAG_CONVERT_COLORS** = ``2``

Nếu được thiết lập, một bảng ánh xạ màu được xác định trước sẽ được áp dụng cho hình ảnh. Được sử dụng khi :ref:`ResourceImporterTexture.editor/convert_colors_with_editor_theme<class_ResourceImporterTexture_property_editor/convert_colors_with_editor_theme>` là ``true``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
