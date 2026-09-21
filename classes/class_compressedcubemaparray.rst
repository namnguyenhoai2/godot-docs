:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CompressedCubemapArray.xml.

.. _class_CompressedCubemapArray:

CompressedCubemapArray
======================

**Kế thừa:** :ref:`CompressedTextureLayered<class_CompressedTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một :ref:`CubemapArray<class_CubemapArray>` có thể được nén.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một mảng cubemap được tải từ tệp ``.ccubearray``. Định dạng tệp này là định dạng nội bộ của Godot; tệp được tạo bằng cách import các định dạng hình ảnh khác thông qua hệ thống import. **CompressedCubemapArray** có thể sử dụng 4 phương pháp nén:

- Không mất dữ liệu (WebP hoặc PNG, không nén trên GPU)

- Có mất dữ liệu (WebP, không nén trên GPU)

- Nén VRAM (nén trên GPU)

- Không nén VRAM (không nén trên GPU)

- Basis Universal (nén trên GPU. Kích thước tệp nhỏ hơn Nén VRAM, nhưng nén chậm hơn và chất lượng thấp hơn Nén VRAM)

Chỉ **Nén VRAM** thực sự làm giảm mức sử dụng bộ nhớ trên GPU. Các phương pháp nén **Không mất dữ liệu** và **Có mất dữ liệu** sẽ giảm dung lượng lưu trữ cần thiết trên đĩa, nhưng không làm giảm mức sử dụng bộ nhớ trên GPU vì texture được gửi đến GPU ở dạng không nén.

Sử dụng **Nén VRAM** cũng cải thiện thời gian tải, vì texture được nén VRAM tải nhanh hơn so với texture sử dụng phương pháp nén không mất dữ liệu hoặc có mất dữ liệu. Nén VRAM có thể tạo ra các hiện tượng đáng chú ý và được dùng cho việc render 3D, không phải 2D.

Xem :ref:`CubemapArray<class_CubemapArray>` để biết mô tả chung về các mảng cubemap.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
