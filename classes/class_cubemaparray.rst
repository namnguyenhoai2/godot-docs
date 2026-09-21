:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CubemapArray.xml.

.. _class_CubemapArray:

CubemapArray
============

**Kế thừa:** :ref:`ImageTextureLayered<class_ImageTextureLayered>` **<** :ref:`TextureLayered<class_TextureLayered>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

An array of :ref:`Cubemap<class_Cubemap>`\ s, stored together and with a single reference.

.. rst-class:: classref-introduction-group

Mô tả
-----

**CubemapArray**\ s are made of an array of :ref:`Cubemap<class_Cubemap>`\ s. Like :ref:`Cubemap<class_Cubemap>`\ s, they are made of multiple textures, the amount of which must be divisible by 6 (one for each face of the cube).

The primary benefit of **CubemapArray**\ s is that they can be accessed in shader code using a single texture reference. In other words, you can pass multiple :ref:`Cubemap<class_Cubemap>`\ s into a shader using a single **CubemapArray**. :ref:`Cubemap<class_Cubemap>`\ s are allocated in adjacent cache regions on the GPU, which makes **CubemapArray**\ s the most efficient way to store multiple :ref:`Cubemap<class_Cubemap>`\ s.

Godot sử dụng **CubemapArray**\ s internally cho nhiều hiệu ứng, bao gồm :ref:`Sky<class_Sky>` nếu bạn đặt :ref:`ProjectSettings.rendering/reflections/sky_reflections/texture_array_reflections<class_ProjectSettings_property_rendering/reflections/sky_reflections/texture_array_reflections>` thành ``true``.

Để tự tạo tệp texture như vậy, hãy reimport các tệp hình ảnh bằng import presets của Godot Editor. Để tạo một CubemapArray từ code, hãy sử dụng :ref:`ImageTextureLayered.create_from_images()<class_ImageTextureLayered_method_create_from_images>` trên một instance của lớp CubemapArray.

Thứ tự hình ảnh dự kiến là X+, X-, Y+, Y-, Z+, Z- (theo hệ tọa độ của Godot, nên Y+ là "lên" và Z- là "ra trước"). Bạn có thể sử dụng một trong các template sau làm cơ sở:

- `2×3 cubemap template (default layout option) <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_2x3.webp>`__\

- `3×2 cubemap template <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_3x2.webp>`__\

- `1×6 cubemap template <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_1x6.webp>`__\

- `6×1 cubemap template <https://raw.githubusercontent.com/godotengine/godot-docs/master/tutorials/assets_pipeline/img/cubemap_template_6x1.webp>`__\

Nhiều layer được xếp chồng lên nhau khi sử dụng tùy chọn import dọc mặc định (với layer đầu tiên ở trên cùng). Ngoài ra, bạn có thể chọn bố cục ngang trong các tùy chọn import (với layer đầu tiên ở bên trái).

\ **Lưu ý:** **CubemapArray** không được hỗ trợ trong Compatibility renderer do các giới hạn của graphics API.

.. rst-class:: classref-reftable-group

Các phương thức
---------------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------------+
   | :ref:`Resource<class_Resource>` | :ref:`create_placeholder<class_CubemapArray_method_create_placeholder>`\ (\ ) |const| |
   +---------------------------------+---------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả phương thức
-----------------

.. _class_CubemapArray_method_create_placeholder:

.. rst-class:: classref-method

:ref:`Resource<class_Resource>` **create_placeholder**\ (\ ) |const| :ref:`🔗<class_CubemapArray_method_create_placeholder>`

Tạo một phiên bản placeholder của resource này (:ref:`PlaceholderCubemapArray<class_PlaceholderCubemapArray>`).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
