:github_url: hide

.. KHÔNG ĐƯỢC CHỈNH SỬA TỆP NÀY!!! .. Được tự động tạo từ mã nguồn của Godot engine. .. Generator: https://github.com/godotengine/godot/tree/master/doc/tools/make_rst.py. .. XML source: https://github.com/godotengine/godot/tree/master/modules/noise/doc_classes/NoiseTexture3D.xml.

.. _class_NoiseTexture3D:

NoiseTexture3D
==============

**Kế thừa:** :ref:`Texture3D<class_Texture3D>` **<** :ref:`Texture<class_Texture>` **<** :ref:`Resource<class_Resource>` **<** :ref:`RefCounted<class_RefCounted>` **<** :ref:`Object<class_Object>`

Một texture 3D được lấp đầy bằng nhiễu do một đối tượng :ref:`Noise<class_Noise>` tạo ra.

.. rst-class:: classref-introduction-group

Mô tả
-----

Sử dụng thư viện :ref:`FastNoiseLite<class_FastNoiseLite>` hoặc các trình tạo nhiễu khác để lấp đầy dữ liệu texture với kích thước mong muốn.

Lớp này sử dụng :ref:`Thread<class_Thread>`\ s để tạo dữ liệu texture nội bộ, vì vậy :ref:`Texture3D.get_data()<class_Texture3D_method_get_data>` có thể trả về ``null`` nếu quá trình tạo chưa hoàn tất. Trong trường hợp đó, bạn cần đợi texture được tạo xong trước khi truy cập image:

::

    var texture = NoiseTexture3D.new()
    texture.noise = FastNoiseLite.new()
    await texture.changed
    var data = texture.get_data()

.. rst-class:: classref-reftable-group

Các thuộc tính
--------------

.. table::
   :widths: auto

   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`Gradient<class_Gradient>` | :ref:`color_ramp<class_NoiseTexture3D_property_color_ramp>`                     |           |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`           | :ref:`depth<class_NoiseTexture3D_property_depth>`                               | ``64``    |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`           | :ref:`height<class_NoiseTexture3D_property_height>`                             | ``64``    |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`         | :ref:`invert<class_NoiseTexture3D_property_invert>`                             | ``false`` |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`Noise<class_Noise>`       | :ref:`noise<class_NoiseTexture3D_property_noise>`                               |           |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`         | :ref:`normalize<class_NoiseTexture3D_property_normalize>`                       | ``true``  |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`bool<class_bool>`         | :ref:`seamless<class_NoiseTexture3D_property_seamless>`                         | ``false`` |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`float<class_float>`       | :ref:`seamless_blend_skirt<class_NoiseTexture3D_property_seamless_blend_skirt>` | ``0.1``   |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+
   | :ref:`int<class_int>`           | :ref:`width<class_NoiseTexture3D_property_width>`                               | ``64``    |
   +---------------------------------+---------------------------------------------------------------------------------+-----------+

.. rst-class:: classref-section-separator

----

.. rst-class:: classref-descriptions-group

Mô tả thuộc tính
----------------

.. _class_NoiseTexture3D_property_color_ramp:

.. rst-class:: classref-property

:ref:`Gradient<class_Gradient>` **color_ramp** :ref:`🔗<class_NoiseTexture3D_property_color_ramp>`

.. rst-class:: classref-property-setget

- |void| **set_color_ramp**\ (\ value\: :ref:`Gradient<class_Gradient>`\ ) - :ref:`Gradient<class_Gradient>` **get_color_ramp**\ (\ )

Một :ref:`Gradient<class_Gradient>` được dùng để ánh xạ độ sáng của từng pixel thành một giá trị màu.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_depth:

.. rst-class:: classref-property

:ref:`int<class_int>` **depth** = ``64`` :ref:`🔗<class_NoiseTexture3D_property_depth>`

.. rst-class:: classref-property-setget

- |void| **set_depth**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_depth**\ (\ )

Độ sâu của texture được tạo (tính bằng pixel).

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_height:

.. rst-class:: classref-property

:ref:`int<class_int>` **height** = ``64`` :ref:`🔗<class_NoiseTexture3D_property_height>`

.. rst-class:: classref-property-setget

- |void| **set_height**\ (\ value\: :ref:`int<class_int>`\ ) - :ref:`int<class_int>` **get_height**\ (\ )

Chiều cao của texture được tạo (tính bằng pixel).

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_invert:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **invert** = ``false`` :ref:`🔗<class_NoiseTexture3D_property_invert>`

.. rst-class:: classref-property-setget

- |void| **set_invert**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_invert**\ (\ )

Nếu ``true``, đảo ngược texture nhiễu. Màu trắng trở thành màu đen, màu đen trở thành màu trắng.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_noise:

.. rst-class:: classref-property

:ref:`Noise<class_Noise>` **noise** :ref:`🔗<class_NoiseTexture3D_property_noise>`

.. rst-class:: classref-property-setget

- |void| **set_noise**\ (\ value\: :ref:`Noise<class_Noise>`\ ) - :ref:`Noise<class_Noise>` **get_noise**\ (\ )

Instance của đối tượng :ref:`Noise<class_Noise>`.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_normalize:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **normalize** = ``true`` :ref:`🔗<class_NoiseTexture3D_property_normalize>`

.. rst-class:: classref-property-setget

- |void| **set_normalize**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **is_normalized**\ (\ )

Nếu ``true``, ảnh nhiễu từ trình tạo nhiễu sẽ được chuẩn hóa về phạm vi từ ``0.0`` đến ``1.0``.

Tắt việc chuẩn hóa có thể ảnh hưởng đến độ tương phản và cho phép bạn tạo các texture nhiễu dạng tileable không lặp lại.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_seamless:

.. rst-class:: classref-property

:ref:`bool<class_bool>` **seamless** = ``false`` :ref:`🔗<class_NoiseTexture3D_property_seamless>`

.. rst-class:: classref-property-setget

- |void| **set_seamless**\ (\ value\: :ref:`bool<class_bool>`\ ) - :ref:`bool<class_bool>` **get_seamless**\ (\ )

Nếu ``true``, một texture seamless sẽ được yêu cầu từ resource :ref:`Noise<class_Noise>`.

\ **Lưu ý:** Texture nhiễu seamless có thể mất nhiều thời gian hơn để tạo và/hoặc có độ tương phản thấp hơn so với nhiễu không seamless, tùy thuộc vào resource :ref:`Noise<class_Noise>` được sử dụng. Điều này là do một số implementation sử dụng các chiều cao hơn để tạo nhiễu seamless.

\ **Lưu ý:** Implementation :ref:`FastNoiseLite<class_FastNoiseLite>` mặc định sử dụng fallback path để tạo seamless. Nếu sử dụng :ref:`width<class_NoiseTexture3D_property_width>`, :ref:`height<class_NoiseTexture3D_property_height>` hoặc :ref:`depth<class_NoiseTexture3D_property_depth>` thấp hơn giá trị mặc định, bạn có thể cần tăng :ref:`seamless_blend_skirt<class_NoiseTexture3D_property_seamless_blend_skirt>` để việc blending seamless hiệu quả hơn.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_seamless_blend_skirt:

.. rst-class:: classref-property

:ref:`float<class_float>` **seamless_blend_skirt** = ``0.1`` :ref:`🔗<class_NoiseTexture3D_property_seamless_blend_skirt>`

.. rst-class:: classref-property-setget

- |void| **set_seamless_blend_skirt**\ (\ value\: :ref:`float<class_float>`\ ) - :ref:`float<class_float>` **get_seamless_blend_skirt**\ (\ )

Được sử dụng cho implementation mặc định/fallback của việc tạo texture seamless. Thuộc tính này xác định khoảng cách mà các đường nối được blend. Giá trị cao có thể dẫn đến ít chi tiết và độ tương phản thấp hơn. Xem :ref:`Noise<class_Noise>` để biết thêm chi tiết.

\ **Lưu ý:** Nếu sử dụng :ref:`width<class_NoiseTexture3D_property_width>`, :ref:`height<class_NoiseTexture3D_property_height>` hoặc :ref:`depth<class_NoiseTexture3D_property_depth>` thấp hơn giá trị mặc định, bạn có thể cần tăng :ref:`seamless_blend_skirt<class_NoiseTexture3D_property_seamless_blend_skirt>` để việc blending seamless hiệu quả hơn.

.. rst-class:: classref-item-separator

----

.. _class_NoiseTexture3D_property_width:

.. rst-class:: classref-property

:ref:`int<class_int>` **width** = ``64`` :ref:`🔗<class_NoiseTexture3D_property_width>`

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
