:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderCubemap.xml.

.. _class_PlaceholderCubemap:

PlaceholderCubemap
==================

**Kế thừa:** :ref:`PlaceholderTextureLayered<class_PlaceholderTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`Cubemap<class_Cubemap>` không có dữ liệu hình ảnh.

.. rst-class:: classref-introduction-group

Mô tả
-----

Class này thay thế một :ref:`Cubemap<class_Cubemap>` hoặc một class dẫn xuất từ :ref:`Cubemap<class_Cubemap>` trong 2 trường hợp:

- Trong chế độ dedicated server, khi dữ liệu hình ảnh không nên ảnh hưởng đến logic game. Điều này cho phép giảm đáng kể kích thước của PCK đã export.

- Khi class dẫn xuất từ :ref:`Cubemap<class_Cubemap>` bị thiếu, chẳng hạn khi sử dụng một phiên bản engine khác.

\ **Lưu ý:** Class này không предназначена cho việc rendering hoặc sử dụng trong shader. Các thao tác như tính toán UV không được đảm bảo sẽ hoạt động.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
