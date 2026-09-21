:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderCubemapArray.xml.

.. _class_PlaceholderCubemapArray:

PlaceholderCubemapArray
=======================

**Kế thừa:** :ref:`PlaceholderTextureLayered<class_PlaceholderTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`CubemapArray<class_CubemapArray>` không có dữ liệu hình ảnh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này thay thế một :ref:`CubemapArray<class_CubemapArray>` hoặc một lớp dẫn xuất từ :ref:`CubemapArray<class_CubemapArray>` trong 2 trường hợp:

- Trong chế độ dedicated server, khi dữ liệu hình ảnh không nên ảnh hưởng đến logic trò chơi. Điều này cho phép giảm đáng kể kích thước của PCK được export.

- Khi lớp dẫn xuất từ :ref:`CubemapArray<class_CubemapArray>` bị thiếu, chẳng hạn như khi sử dụng một phiên bản engine khác.

\ **Lưu ý:** Lớp này không dành cho việc rendering hoặc sử dụng trong shader. Các thao tác như tính toán UV không được đảm bảo sẽ hoạt động.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
