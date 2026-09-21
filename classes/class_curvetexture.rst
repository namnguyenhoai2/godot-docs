:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/doc/classes/CurveTexture.xml.

.. _class_CurveTexture:

CurveTexture
============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture 1D trong đó độ sáng của pixel tương ứng với các điểm trên một đường cong.

.. rst-class:: classref-introduction-group

Mô tả
-----

Một texture 1D trong đó độ sáng của pixel tương ứng với các điểm trên một resource :ref:`Curve<class_Curve>` đơn vị, ở dạng grayscale hoặc màu đỏ. Biểu diễn trực quan này giúp đơn giản hóa việc lưu các đường cong dưới dạng tệp hình ảnh.

Nếu cần lưu trữ tối đa 3 đường cong trong một texture duy nhất, hãy sử dụng :ref:`CurveXYZTexture<class_CurveXYZTexture>` thay thế. Xem thêm :ref:`GradientTexture1D<class_GradientTexture1D>` và :ref:`GradientTexture2D<class_GradientTexture2D>`.

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Curve<class_Curve>`                         | :ref:`curve<class_CurveTexture_property_curve>`               |                                                                                        |
   +---------------------------------------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`                           | resource_local_to_scene                                       | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +---------------------------------------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`TextureMode<enum_CurveTexture_TextureMode>` | :ref:`texture_mode<class_CurveTexture_property_texture_mode>` | ``0``                                                                                  |
   +---------------------------------------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`                             | :ref:`width<class_CurveTexture_property_width>`               | ``256``                                                                                |
   +---------------------------------------------------+---------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Các kiểu liệt kê
----------------

.. _enum_CurveTexture_TextureMode:

.. rst-class:: classref-enumeration

enum **TextureMode**: :ref:`🔗<enum_CurveTexture_TextureMode>`

.. _class_CurveTexture_constant_TEXTURE_MODE_RGB:

.. rst-class:: classref-enumeration-constant

:ref:`TextureMode<enum_CurveTexture_TextureMode>` **TEXTURE_MODE_RGB** = ``0``

Lưu đường cong đồng đều trên các kênh đỏ, xanh lá và xanh dương. Cách này sử dụng nhiều video memory hơn, nhưng tương thích tốt hơn với các shader chỉ đọc các giá trị xanh lá và xanh dương.

.. _class_CurveTexture_constant_TEXTURE_MODE_RED:

.. rst-class:: classref-enumeration-constant

:ref:`TextureMode<enum_CurveTexture_TextureMode>` **TEXTURE_MODE_RED** = ``1``

Chỉ lưu đường cong trong kênh đỏ. Cách này tiết kiệm video memory, nhưng một số shader tùy chỉnh có thể không hoạt động với cách này.

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_CurveTexture_property_curve:

.. rst-class:: classref-property

:ref:`Curve<class_Curve>` **curve** :ref:`🔗<class_CurveTexture_property_curve>`

.. rst-class:: classref-property-setget

- |void| **set_curve**\ (\ value\: :ref:`Curve<class_Curve>`\ ) - :ref:`Curve<class_Curve>` **get_curve**\ (\ )

:ref:`Curve<class_Curve>` được kết xuất lên texture. Phải là một :ref:`Curve<class_Curve>` đơn vị.

.. rst-class:: classref-item-separator

----

.. _class_CurveTexture_property_texture_mode:

.. rst-class:: classref-property

:ref:`TextureMode<enum_CurveTexture_TextureMode>` **texture_mode** = ``0`` :ref:`🔗<class_CurveTexture_property_texture_mode>`

.. rst-class:: classref-property-setget

- |void| **set_texture_mode**\ (\ value\: :ref:`TextureMode<enum_CurveTexture_TextureMode>`\ ) - :ref:`TextureMode<enum_CurveTexture_TextureMode>` **get_texture_mode**\ (\ )

Định dạng mà texture sẽ được tạo. Khi truyền một CurveTexture làm đầu vào cho :ref:`Shader<class_Shader>`, có thể cần điều chỉnh định dạng này.

.. rst-class:: classref-item-separator

----

.. _class_CurveTexture_property_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **width** = ``256`` :ref:`🔗<class_CurveTexture_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_width**\ (\ )

Chiều rộng của texture (tính bằng pixel). Giá trị cao hơn giúp biểu diễn dữ liệu có tần số cao tốt hơn (chẳng hạn như các thay đổi hướng đột ngột), nhưng làm tăng thời gian tạo và mức sử dụng bộ nhớ.

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
