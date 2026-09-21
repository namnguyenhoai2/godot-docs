:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CompressedTexture2D.xml.

.. _class_CompressedTexture2D:

CompressedTexture2D
===================

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture có 2 chiều, có thể được nén.

.. rst-class:: classref-introduction-group

Mô tả
-----

Texture được tải từ tệp ``.ctex``. Định dạng tệp này là định dạng nội bộ của Godot; tệp được tạo bằng cách import các định dạng hình ảnh khác thông qua hệ thống import. **CompressedTexture2D** có thể sử dụng 1 trong 4 phương pháp nén (bao gồm cả không nén):

- Lossless (WebP hoặc PNG, không nén trên GPU)

- Lossy (WebP, không nén trên GPU)

- VRAM Compressed (nén trên GPU)

- VRAM Uncompressed (không nén trên GPU)

- Basis Universal (nén trên GPU. Kích thước tệp nhỏ hơn VRAM Compressed, nhưng nén chậm hơn và chất lượng thấp hơn VRAM Compressed)

Chỉ **VRAM Compressed** mới thực sự làm giảm mức sử dụng bộ nhớ trên GPU. Các phương pháp nén **Lossless** và **Lossy** sẽ giảm dung lượng lưu trữ cần thiết trên ổ đĩa, nhưng không làm giảm mức sử dụng bộ nhớ trên GPU vì texture được gửi đến GPU ở dạng không nén.

Sử dụng **VRAM Compressed** cũng cải thiện thời gian tải, vì texture được nén VRAM tải nhanh hơn so với texture sử dụng phương pháp nén lossless hoặc lossy. Nén VRAM có thể tạo ra các hiện tượng dễ nhận thấy và được thiết kế để sử dụng cho kết xuất 3D, không phải 2D.

.. rst-class:: classref-reftable-group

Thuộc tính
----------

.. table::
   :widths: auto

   +-----------------------------+----------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`String<class_String>` | :ref:`load_path<class_CompressedTexture2D_property_load_path>` | ``""``                                                                                 |
   +-----------------------------+----------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`     | resource_local_to_scene                                        | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-----------------------------+----------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Phương thức
-----------

.. table::
   :widths: auto

   +---------------------------------------+----------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`load<class_CompressedTexture2D_method_load>`\ (\ path\: :ref:`String<class_String>`\ ) |
   +---------------------------------------+----------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CompressedTexture2D_property_load_path:

.. rst-class:: classref-property

:ref:`String<class_String>` **load_path** = ``""`` :ref:`🔗<class_CompressedTexture2D_property_load_path>`

.. rst-class:: classref-property-setget

- :ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) - :ref:`String<class_String>` **get_load_path**\ (\ )

Đường dẫn tệp của **CompressedTexture2D** đến tệp ``.ctex``.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CompressedTexture2D_method_load:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **load**\ (\ path\: :ref:`String<class_String>`\ ) :ref:`🔗<class_CompressedTexture2D_method_load>`

Tải texture từ ``path`` được chỉ định.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
