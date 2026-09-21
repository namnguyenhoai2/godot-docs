:github_url: hide

.. KHÔNG CHỈNH SỬA TỆP NÀY!!! .. Được tạo tự động từ các mã nguồn của Godot engine. .. Trình tạo: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. Nguồn XML: https://github.com/godotengine/godot/tree/master/doc/classes/ImageTexture3D.xml.

.. _class_ImageTexture3D:

ImageTexture3D
==============

**Kế thừa:** :ref:`Texture3D<class_Texture3D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Texture có 3 chiều.

.. rst-class:: classref-introduction-group

Mô tả
-----

**ImageTexture3D** là một :ref:`ImageTexture<class_ImageTexture>` 3 chiều có chiều rộng, chiều cao và chiều sâu. Xem thêm :ref:`ImageTextureLayered<class_ImageTextureLayered>`.

Texture 3D thường được dùng để lưu trữ các bản đồ mật độ cho :ref:`FogMaterial<class_FogMaterial>`, các LUT hiệu chỉnh màu cho :ref:`Environment<class_Environment>`, các trường vector cho :ref:`GPUParticlesAttractorVectorField3D<class_GPUParticlesAttractorVectorField3D>` và các bản đồ va chạm cho :ref:`GPUParticlesCollisionSDF3D<class_GPUParticlesCollisionSDF3D>`. Texture 3D cũng có thể được sử dụng trong các shader tùy chỉnh.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | :ref:`Error<enum_@GlobalScope_Error>` | :ref:`create<class_ImageTexture3D_method_create>`\ (\ format\: :ref:`Format<enum_Image_Format>`, width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, depth\: :ref:`int<class_int>`, use_mipmaps\: :ref:`bool<class_bool>`, data\: :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\]\ ) |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | |void|                                | :ref:`update<class_ImageTexture3D_method_update>`\ (\ data\: :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\]\ )                                                                                                                                                                                 |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_ImageTexture3D_method_create:

.. rst-class:: classref-method

:ref:`Error<enum_@GlobalScope_Error>` **create**\ (\ format\: :ref:`Format<enum_Image_Format>`, width\: :ref:`int<class_int>`, height\: :ref:`int<class_int>`, depth\: :ref:`int<class_int>`, use_mipmaps\: :ref:`bool<class_bool>`, data\: :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\]\ ) :ref:`🔗<class_ImageTexture3D_method_create>`

Tạo **ImageTexture3D** với ``format``, ``width``, ``height`` và ``depth`` được chỉ định. Nếu ``use_mipmaps`` là ``true``, các mipmap sẽ được tạo cho **ImageTexture3D**.

.. rst-class:: classref-item-separator

----

.. _class_ImageTexture3D_method_update:

.. rst-class:: classref-method

|void| **update**\ (\ data\: :ref:`Array<class_Array>`\[:ref:`Image<class_Image>`\]\ ) :ref:`🔗<class_ImageTexture3D_method_update>`

Thay thế dữ liệu hiện có của texture bằng các layer được chỉ định trong ``data``. Kích thước của ``data`` phải khớp với các tham số đã được sử dụng cho :ref:`create()<class_ImageTexture3D_method_create>`. Nói cách khác, không thể thay đổi kích thước hoặc định dạng của texture bằng cách gọi :ref:`update()<class_ImageTexture3D_method_update>`.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
