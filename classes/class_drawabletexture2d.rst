:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn engine Godot. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/DrawableTexture2D.xml.

.. _class_DrawableTexture2D:

DrawableTexture2D
=================

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture 2D hỗ trợ vẽ lên chính nó thông qua các lệnh gọi Blit.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một texture 2D có thể được sửa đổi thông qua các lệnh gọi blit, sao chép từ một texture đích vào chính nó. Chủ yếu được thiết kế để quản lý trong code, người dùng phải gọi :ref:`setup()<class_DrawableTexture2D_method_setup>` để khởi tạo trạng thái trước khi vẽ. Mỗi lệnh gọi :ref:`blit_rect()<class_DrawableTexture2D_method_blit_rect>` nhận ít nhất một hình chữ nhật, là vùng cần vẽ, và một texture khác, là nội dung cần vẽ. Các lệnh gọi vẽ sử dụng một Texture_Blit Shader để xử lý và tính toán kết quả theo từng pixel. Người dùng có thể cung cấp ShaderMaterial riêng với các Texture_Blit shader tùy chỉnh để thực hiện các hành vi phức tạp hơn.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +-------------------------+-------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | resource_local_to_scene | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +-------------------------+-------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`blit_rect<class_DrawableTexture2D_method_blit_rect>`\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, source\: :ref:`Texture2D<class_Texture2D>`, modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1), mipmap\: :ref:`int<class_int>` = 0, material\: :ref:`Material<class_Material>` = null\ )                                                                                                                                           |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`blit_rect_multi<class_DrawableTexture2D_method_blit_rect_multi>`\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, sources\: :ref:`Array<class_Array>`\[:ref:`Texture2D<class_Texture2D>`\], extra_targets\: :ref:`Array<class_Array>`\[:ref:`DrawableTexture2D<class_DrawableTexture2D>`\], modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1), mipmap\: :ref:`int<class_int>` = 0, material\: :ref:`Material<class_Material>` = null\ ) |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`generate_mipmaps<class_DrawableTexture2D_method_generate_mipmaps>`\ (\ )                                                                                                                                                                                                                                                                                                                                                              |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>` | :ref:`get_use_mipmaps<class_DrawableTexture2D_method_get_use_mipmaps>`\ (\ ) |const|                                                                                                                                                                                                                                                                                                                                                        |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_format<class_DrawableTexture2D_method_set_format>`\ (\ format\: :ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>`\ )                                                                                                                                                                                                                                                                                                   |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`set_use_mipmaps<class_DrawableTexture2D_method_set_use_mipmaps>`\ (\ mipmaps\: :ref:`bool<class_bool>`\ )                                                                                                                                                                                                                                                                                                                             |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                  | :ref:`setup<class_DrawableTexture2D_method_setup>`\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, format\: :ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>`, color\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1), use_mipmaps\: :ref:`bool<class_bool>` = false\ )                                                                                                                                        |
   +-------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các enumeration
---------------

.. _enum_DrawableTexture2D_DrawableFormat:

.. rst-class:: classref-enumeration

enum **DrawableFormat**: :ref:`🔗<enum_DrawableTexture2D_DrawableFormat>`

.. _class_DrawableTexture2D_constant_DRAWABLE_FORMAT_RGBA8:

.. rst-class:: classref-enumeration-constant

:ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>` **DRAWABLE_FORMAT_RGBA8** = ``0``

Định dạng texture OpenGL RGBA với bốn thành phần, mỗi thành phần có độ sâu bit là 8.

.. _class_DrawableTexture2D_constant_DRAWABLE_FORMAT_RGBA8_SRGB:

.. rst-class:: classref-enumeration-constant

:ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>` **DRAWABLE_FORMAT_RGBA8_SRGB** = ``1``

Định dạng texture OpenGL RGBA với bốn thành phần, mỗi thành phần có độ sâu bit là 8.

Khi được vẽ lên, một phép chuyển đổi không gian màu từ sRGB sang tuyến tính sẽ được thực hiện.

.. _class_DrawableTexture2D_constant_DRAWABLE_FORMAT_RGBAH:

.. rst-class:: classref-enumeration-constant

:ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>` **DRAWABLE_FORMAT_RGBAH** = ``2``

Định dạng texture OpenGL GL_RGBA16F, trong đó có bốn thành phần, mỗi thành phần là một giá trị dấu phẩy động "half-precision" 16 bit.

.. _class_DrawableTexture2D_constant_DRAWABLE_FORMAT_RGBAF:

.. rst-class:: classref-enumeration-constant

:ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>` **DRAWABLE_FORMAT_RGBAF** = ``3``

Định dạng texture OpenGL GL_RGBA32F, trong đó có bốn thành phần, mỗi thành phần là một giá trị dấu phẩy động 32 bit.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả các phương thức
---------------------

.. _class_DrawableTexture2D_method_blit_rect:

.. rst-class:: classref-method

|void| **blit_rect**\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, source\: :ref:`Texture2D<class_Texture2D>`, modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1), mipmap\: :ref:`int<class_int>` = 0, material\: :ref:`Material<class_Material>` = null\ ) :ref:`🔗<class_DrawableTexture2D_method_blit_rect>`

**Thử nghiệm:** Phương thức này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Vẽ lên ``rect`` đã cho trên texture này bằng cách sao chép từ ``source`` đã cho. Có thể truyền vào một màu ``modulate`` để shader sử dụng, nhưng mặc định là White. Giá trị ``mipmap`` có thể chỉ định việc vẽ vào một mức mipmap thấp hơn. Tham số ``material`` có thể nhận một ShaderMaterial với TextureBlit Shader để tùy chỉnh hành vi vẽ.

.. rst-class:: classref-item-separator

----

.. _class_DrawableTexture2D_method_blit_rect_multi:

.. rst-class:: classref-method

|void| **blit_rect_multi**\ (\ rect\: :ref:`Rect2i<class_Rect2i>`, sources\: :ref:`Array<class_Array>`\[:ref:`Texture2D<class_Texture2D>`\], extra_targets\: :ref:`Array<class_Array>`\[:ref:`DrawableTexture2D<class_DrawableTexture2D>`\], modulate\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1), mipmap\: :ref:`int<class_int>` = 0, material\: :ref:`Material<class_Material>` = null\ ) :ref:`🔗<class_DrawableTexture2D_method_blit_rect_multi>`

**Thử nghiệm:** Phương thức này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Vẽ lên ``rect`` đã cho trên texture này, cũng như trên tối đa 3 ``extra_targets`` DrawableTexture. Tất cả ``extra_targets`` phải có cùng kích thước và DrawableFormat với đích ban đầu; nếu không, Shader có thể gặp lỗi. Phương thức này yêu cầu tối đa 4 ``sources`` Texture, nhưng sẽ thay thế các ``sources`` bị thiếu bằng các Texture Black mặc định.

.. rst-class:: classref-item-separator

----

.. _class_DrawableTexture2D_method_generate_mipmaps:

.. rst-class:: classref-method

|void| **generate_mipmaps**\ (\ ) :ref:`🔗<class_DrawableTexture2D_method_generate_mipmaps>`

Tính toán lại các mipmap cho texture này theo yêu cầu.

.. rst-class:: classref-item-separator

----

.. _class_DrawableTexture2D_method_get_use_mipmaps:

.. rst-class:: classref-method

:ref:`bool<class_bool>` **get_use_mipmaps**\ (\ ) |const| :ref:`🔗<class_DrawableTexture2D_method_get_use_mipmaps>`

Trả về ``true`` nếu mipmap được đặt là sẽ sử dụng trên DrawableTexture này.

.. rst-class:: classref-item-separator

----

.. _class_DrawableTexture2D_method_set_format:

.. rst-class:: classref-method

|void| **set_format**\ (\ format\: :ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>`\ ) :ref:`🔗<class_DrawableTexture2D_method_set_format>`

Đặt format cho DrawableTexture này.

.. rst-class:: classref-item-separator

----

.. _class_DrawableTexture2D_method_set_use_mipmaps:

.. rst-class:: classref-method

|void| **set_use_mipmaps**\ (\ mipmaps\: :ref:`bool<class_bool>`\ ) :ref:`🔗<class_DrawableTexture2D_method_set_use_mipmaps>`

Đặt liệu mipmap có được sử dụng trên DrawableTexture này hay không.

.. rst-class:: classref-item-separator

----

.. _class_DrawableTexture2D_method_setup:

.. rst-class:: classref-method

|void| **setup**\ (\ width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, format\: :ref:`DrawableFormat<enum_DrawableTexture2D_DrawableFormat>`, color\: :ref:`Color<class_Color>` = Color(1, 1, 1, 1), use_mipmaps\: :ref:`bool<class_bool>` = false\ ) :ref:`🔗<class_DrawableTexture2D_method_setup>`

**Thử nghiệm:** Phương thức này có thể bị thay đổi hoặc loại bỏ trong các phiên bản tương lai.

Khởi tạo DrawableTexture thành một texture White với ``width``, ``height`` và ``format`` đã cho.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
