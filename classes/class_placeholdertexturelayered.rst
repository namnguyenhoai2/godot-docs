:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/PlaceholderTextureLayered.xml.

.. _class_PlaceholderTextureLayered:

PlaceholderTextureLayered
=========================

**Kế thừa:** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`PlaceholderCubemap<class_PlaceholderCubemap>`, :ref:`PlaceholderCubemapArray<class_PlaceholderCubemapArray>`, :ref:`PlaceholderTexture2DArray<class_PlaceholderTexture2DArray>`

Lớp placeholder cho một mảng texture 2 chiều.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp này được sử dụng khi tải một project sử dụng lớp con của :ref:`TextureLayered<class_TextureLayered>` trong 2 trường hợp:

- Khi chạy project được export ở chế độ dedicated server, chỉ các kích thước của texture được giữ lại (vì chúng có thể được sử dụng cho mục đích gameplay hoặc để định vị các phần tử khác). Điều này giúp giảm đáng kể kích thước của PCK được export.

- Khi lớp con này bị thiếu do sử dụng phiên bản hoặc bản build engine khác (ví dụ: các module bị vô hiệu hóa).

\ **Lưu ý:** Lớp này không được dùng làm texture thực tế để render. Không đảm bảo lớp này hoạt động như texture trong shader hoặc material (ví dụ khi tính UV).

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +---------------------------------+----------------------------------------------------------------+--------------------+
   | :ref:`int<class_int>`           | :ref:`layers<class_PlaceholderTextureLayered_property_layers>` | ``1``              |
   +---------------------------------+----------------------------------------------------------------+--------------------+
   | :ref:`Vector2i<class_Vector2i>` | :ref:`size<class_PlaceholderTextureLayered_property_size>`     | ``Vector2i(1, 1)`` |
   +---------------------------------+----------------------------------------------------------------+--------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_PlaceholderTextureLayered_property_layers:

.. rst-class:: classref-property

:ref:`int<class_int>` **layers** = ``1`` :ref:`🔗<class_PlaceholderTextureLayered_property_layers>`

.. rst-class:: classref-property-setget

- |void| **set_layers**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_layers**\ (\ )

Số lượng layer trong mảng texture.

.. rst-class:: classref-item-separator

----

.. _class_PlaceholderTextureLayered_property_size:

.. rst-class:: classref-property

:ref:`Vector2i<class_Vector2i>` **size** = ``Vector2i(1, 1)`` :ref:`🔗<class_PlaceholderTextureLayered_property_size>`

.. rst-class:: classref-property-setget

- |void| **set_size**\ (\ value\: :ref:`Vector2i<class_Vector2i>`\ ) - :ref:`Vector2i<class_Vector2i>` **get_size**\ (\ )

Kích thước của mỗi layer texture (tính bằng pixel).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
