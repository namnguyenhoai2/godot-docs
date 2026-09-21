:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/noise/doc_classes/NoiseTexture2D.xml.

.. _class_NoiseTexture2D:

NoiseTexture2D
==============

**Kế thừa:** :ref:`Texture2D<class_Texture2D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture 2D được lấp đầy bằng nhiễu do một đối tượng :ref:`Noise<class_Noise>` tạo ra.

.. rst-class:: classref-introduction-group

Mô tả
-----

Sử dụng thư viện :ref:`FastNoiseLite<class_FastNoiseLite>` hoặc các noise generator khác để lấp đầy dữ liệu texture với kích thước mong muốn. **NoiseTexture2D** cũng có thể tạo texture normal map.

Lớp này sử dụng :ref:`Thread<class_Thread>`\ s để tạo dữ liệu texture ở bên trong, vì vậy :ref:`Texture2D.get_image()<class_Texture2D_method_get_image>` có thể trả về ``null`` nếu quá trình tạo vẫn chưa hoàn tất. Trong trường hợp đó, bạn cần đợi texture được tạo xong trước khi truy cập image và dữ liệu byte đã tạo:

::

    var texture = NoiseTexture2D.new()
    texture.noise = FastNoiseLite.new()
    await texture.changed
    var image = texture.get_image()
    var data = image.get_data()

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`as_normal_map<class_NoiseTexture2D_property_as_normal_map>`               | ``false``                                                                              |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`       | :ref:`bump_strength<class_NoiseTexture2D_property_bump_strength>`               | ``8.0``                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Gradient<class_Gradient>` | :ref:`color_ramp<class_NoiseTexture2D_property_color_ramp>`                     |                                                                                        |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`generate_mipmaps<class_NoiseTexture2D_property_generate_mipmaps>`         | ``true``                                                                               |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`           | :ref:`height<class_NoiseTexture2D_property_height>`                             | ``512``                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`in_3d_space<class_NoiseTexture2D_property_in_3d_space>`                   | ``false``                                                                              |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`invert<class_NoiseTexture2D_property_invert>`                             | ``false``                                                                              |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`Noise<class_Noise>`       | :ref:`noise<class_NoiseTexture2D_property_noise>`                               |                                                                                        |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`normalize<class_NoiseTexture2D_property_normalize>`                       | ``true``                                                                               |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | resource_local_to_scene                                                         | ``false`` (overrides :ref:`Resource<class_Resource_property_resource_local_to_scene>`) |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`bool<class_bool>`         | :ref:`seamless<class_NoiseTexture2D_property_seamless>`                         | ``false``                                                                              |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`float<class_float>`       | :ref:`seamless_blend_skirt<class_NoiseTexture2D_property_seamless_blend_skirt>` | ``0.1``                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+
   | :ref:`int<class_int>`           | :ref:`width<class_NoiseTexture2D_property_width>`                               | ``512``                                                                                |
   +---------------------------------+---------------------------------------------------------------------------------+----------------------------------------------------------------------------------------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NoiseTexture2D_property_as_normal_map:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **as_normal_map** = ``false`` :ref:`🔗<class_NoiseTexture2D_property_as_normal_map>`

.. rst-class:: classref-property-setget

- |void| **set_as_normal_map**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_normal_map**\ (\ )

Nếu ``true``, texture kết quả chứa một normal map được tạo từ noise gốc, được diễn giải như một bump map.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_bump_strength:

.. rst-class:: classref-property

:ref:`float<class_float>` **bump_strength** = ``8.0`` :ref:`🔗<class_NoiseTexture2D_property_bump_strength>`

.. rst-class:: classref-property-setget

- |void| **set_bump_strength**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_bump_strength**\ (\ )

Cường độ của các bump map được sử dụng trong texture này. Giá trị cao hơn sẽ làm bump map trông lớn hơn, trong khi giá trị thấp hơn sẽ làm chúng trông mềm hơn.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_color_ramp:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **color_ramp** :ref:`🔗<class_NoiseTexture2D_property_color_ramp>`

.. rst-class:: classref-property-setget

- |void| **set_color_ramp**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_color_ramp**\ (\ )

Một :ref:`Gradient<class_Gradient>` được dùng để ánh xạ độ sáng của từng pixel thành một giá trị màu.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_generate_mipmaps:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **generate_mipmaps** = ``true`` :ref:`🔗<class_NoiseTexture2D_property_generate_mipmaps>`

.. rst-class:: classref-property-setget

- |void| **set_generate_mipmaps**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_generating_mipmaps**\ (\ )

Xác định có tạo mipmap cho texture này hay không. Việc bật tùy chọn này giúp giảm hiện tượng aliasing của texture ở khoảng cách xa, nhưng làm tăng mức sử dụng bộ nhớ khoảng 33% và khiến quá trình tạo noise texture mất nhiều thời gian hơn.

\ **Lưu ý:** :ref:`generate_mipmaps<class_NoiseTexture2D_property_generate_mipmaps>` yêu cầu bật mipmap filtering trên material sử dụng **NoiseTexture2D** thì mới có tác dụng.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_height:

.. rst-class:: classref-property

:ref:`int<class_int>` **height** = ``512`` :ref:`🔗<class_NoiseTexture2D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_height**\ (\ )

Chiều cao của texture được tạo (tính bằng pixel).

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_in_3d_space:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **in_3d_space** = ``false`` :ref:`🔗<class_NoiseTexture2D_property_in_3d_space>`

.. rst-class:: classref-property-setget

- |void| **set_in_3d_space**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_in_3d_space**\ (\ )

Xác định có tính toán noise image trong không gian 3D hay không. Điều này có thể làm giảm độ tương phản.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_invert:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **invert** = ``false`` :ref:`🔗<class_NoiseTexture2D_property_invert>`

.. rst-class:: classref-property-setget

- |void| **set_invert**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_invert**\ (\ )

Nếu ``true``, đảo ngược noise texture. Màu trắng trở thành màu đen, màu đen trở thành màu trắng.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_noise:

.. rst-class:: classref-property

:ref:`Noise<class_Noise>` **noise** :ref:`🔗<class_NoiseTexture2D_property_noise>`

.. rst-class:: classref-property-setget

- |void| **set_noise**\ (\ value\: :ref:`Noise<class_Noise>`\ ) - :ref:`Noise<class_Noise>` **get_noise**\ (\ )

Instance của đối tượng :ref:`Noise<class_Noise>`.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_normalize:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **normalize** = ``true`` :ref:`🔗<class_NoiseTexture2D_property_normalize>`

.. rst-class:: classref-property-setget

- |void| **set_normalize**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_normalized**\ (\ )

Nếu ``true``, noise image từ noise generator được chuẩn hóa về phạm vi từ ``0.0`` đến ``1.0``.

Tắt tính năng chuẩn hóa có thể ảnh hưởng đến độ tương phản và cho phép bạn tạo các noise texture dạng tileable không lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_seamless:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **seamless** = ``false`` :ref:`🔗<class_NoiseTexture2D_property_seamless>`

.. rst-class:: classref-property-setget

- |void| **set_seamless**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_seamless**\ (\ )

Nếu ``true``, một texture seamless sẽ được yêu cầu từ resource :ref:`Noise<class_Noise>`.

\ **Lưu ý:** Noise texture seamless có thể mất nhiều thời gian hơn để tạo và/hoặc có độ tương phản thấp hơn noise không seamless, tùy thuộc vào resource :ref:`Noise<class_Noise>` được sử dụng. Điều này là do một số implementation sử dụng số chiều cao hơn để tạo seamless noise.

\ **Lưu ý:** Implementation :ref:`FastNoiseLite<class_FastNoiseLite>` mặc định sử dụng fallback path để tạo seamless. Nếu sử dụng :ref:`width<class_NoiseTexture2D_property_width>` hoặc :ref:`height<class_NoiseTexture2D_property_height>` thấp hơn mặc định, bạn có thể cần tăng :ref:`seamless_blend_skirt<class_NoiseTexture2D_property_seamless_blend_skirt>` để việc blending seamless hiệu quả hơn.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_seamless_blend_skirt:

.. rst-class:: classref-property

:ref:`float<class_float>` **seamless_blend_skirt** = ``0.1`` :ref:`🔗<class_NoiseTexture2D_property_seamless_blend_skirt>`

.. rst-class:: classref-property-setget

- |void| **set_seamless_blend_skirt**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_seamless_blend_skirt**\ (\ )

Được sử dụng cho implementation mặc định/fallback của quá trình tạo texture seamless. Nó xác định khoảng cách mà các đường nối được blend. Giá trị cao có thể làm giảm mức độ chi tiết và độ tương phản. Xem :ref:`Noise<class_Noise>` để biết thêm chi tiết.

\ **Lưu ý:** Nếu sử dụng :ref:`width<class_NoiseTexture2D_property_width>` hoặc :ref:`height<class_NoiseTexture2D_property_height>` thấp hơn mặc định, bạn có thể cần tăng :ref:`seamless_blend_skirt<class_NoiseTexture2D_property_seamless_blend_skirt>` để việc blending seamless hiệu quả hơn.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture2D_property_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **width** = ``512`` :ref:`🔗<class_NoiseTexture2D_property_width>`

.. rst-class:: classref-property-setget

- |void| **set_width**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_width**\ (\ )

Chiều rộng của texture được tạo (tính bằng pixel).

.. |virtual| replace:: :abbr:`virtual (This method should typically be overridden by the user to have any effect.)`
.. |required| replace:: :abbr:`required (This method is required to be overridden when extending its base class.)`
.. |const| replace:: :abbr:`const (This method has no side effects. It doesn't modify any of the instance's member variables.)`
.. |vararg| replace:: :abbr:`vararg (This method accepts any number of arguments after the ones described here.)`
.. |constructor| replace:: :abbr:`constructor (This method is used to construct a type.)`
.. |static| replace:: :abbr:`static (This method doesn't need an instance to be called, so it can be called directly using the class name.)`
.. |operator| replace:: :abbr:`operator (This method describes a valid operator to use with this type as left-hand operand.)`
.. |bitfield| replace:: :abbr:`BitField (This value is an integer composed as a bitmask of the following flags.)`
.. |void| replace:: :abbr:`void (No return value.)`
