:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderTexture2DArray.xml.

.. _class_PlaceholderTexture2DArray:

PlaceholderTexture2DArray
=========================

**Kế thừa:** :ref:`PlaceholderTextureLayered<class_PlaceholderTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Lớp placeholder cho một mảng texture 2 chiều.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được sử dụng khi tải một project sử dụng một subclass :ref:`Texture2D<class_Texture2D>` trong 2 trường hợp:

- Khi chạy project được export ở chế độ dedicated server, chỉ các chiều của texture được giữ lại (vì chúng có thể được sử dụng cho gameplay hoặc để định vị các thành phần khác). Điều này giúp giảm đáng kể kích thước của PCK được export.

- Khi subclass này bị thiếu do sử dụng phiên bản hoặc bản build engine khác (ví dụ: các module bị tắt).

\ **Lưu ý:** Lớp này không предназначена để được sử dụng như một texture thực tế cho việc render. Không đảm bảo lớp này hoạt động giống texture trong shader hoặc material (ví dụ: khi tính toán UV).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
