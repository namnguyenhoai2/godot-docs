:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của engine Godot. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CompressedTextureLayered.xml.

.. _class_CompressedTextureLayered:

CompressedTextureLayered
========================

**Kế thừa:** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

**Được kế thừa bởi:** :ref:`CompressedCubemap<class_CompressedCubemap>`, :ref:`CompressedCubemapArray<class_CompressedCubemapArray>`, :ref:`CompressedTexture2DArray<class_CompressedTexture2DArray>`

Lớp cơ sở cho các texture array có thể được nén tùy chọn.

.. rst-class:: classref-introduction-group

Mô tả
-----

Lớp cơ sở cho :ref:`CompressedTexture2DArray<class_CompressedTexture2DArray>` và :ref:`CompressedTexture3D<class_CompressedTexture3D>`. Không thể được sử dụng trực tiếp, nhưng chứa tất cả các hàm cần thiết để truy cập những kiểu resource dẫn xuất. Xem thêm :ref:`TextureLayered<class_TextureLayered>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-----------------------------+---------------------------------------------------------------------+--------+
   | :ref:`String<class_String>` | :ref:`load_path<class_CompressedTextureLayered_property_load_path>` | ``""`` |
   +-----------------------------+---------------------------------------------------------------------+--------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+---------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`load<class_CompressedTextureLayered_method_load>`\ (\ path\: :ref:`String<class_String>`\ ) |
   +---------------------------------------+---------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CompressedTextureLayered_property_load_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **load_path** = ``""`` :ref:`🔗<class_CompressedTextureLayered_property_load_path>`

.. rst-class:: classref-property-setget

- :ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_load_path**\ (\ )

Đường dẫn mà texture sẽ được tải từ đó.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CompressedTextureLayered_method_load:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_CompressedTextureLayered_method_load>`

Tải texture tại ``path``.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
