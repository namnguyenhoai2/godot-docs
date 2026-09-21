:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CompressedTexture2DArray.xml.

.. _class_CompressedTexture2DArray:

CompressedTexture2DArray
========================

**Kế thừa:** :ref:`CompressedTextureLayered<class_CompressedTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Mảng các texture 2 chiều, có thể được nén.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng texture được tải từ tệp ``.ctexarray``. Định dạng tệp này là định dạng nội bộ của Godot; nó được tạo bằng cách import các định dạng hình ảnh khác với hệ thống import. **CompressedTexture2DArray** có thể sử dụng 1 trong 4 phương pháp nén:

- Lossless (WebP hoặc PNG, không nén trên GPU)

- Lossy (WebP, không nén trên GPU)

- VRAM Compressed (nén trên GPU)

- VRAM Uncompressed (không nén trên GPU)

- Basis Universal (nén trên GPU. Kích thước tệp nhỏ hơn VRAM Compressed, nhưng tốc độ nén chậm hơn và chất lượng thấp hơn VRAM Compressed)

Chỉ **VRAM Compressed** thực sự làm giảm mức sử dụng bộ nhớ trên GPU. Các phương pháp nén **Lossless** và **Lossy** sẽ làm giảm dung lượng lưu trữ cần thiết trên đĩa, nhưng không làm giảm mức sử dụng bộ nhớ trên GPU vì texture được gửi đến GPU ở dạng không nén.

Việc sử dụng **VRAM Compressed** cũng cải thiện thời gian tải, vì các texture được nén VRAM tải nhanh hơn so với các texture sử dụng phương pháp nén lossless hoặc lossy. Nén VRAM có thể tạo ra các hiện tượng dễ nhận thấy và được thiết kế để sử dụng cho việc render 3D, không phải 2D.

Xem :ref:`Texture2DArray<class_Texture2DArray>` để biết mô tả chung về các mảng texture.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
